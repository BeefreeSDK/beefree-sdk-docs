---
description: >-
  Let the AI place your users' own saved rows instead of generating new content
  from scratch.
---

# Reusable Rows for AI

{% hint style="info" %}
Reusable Rows for AI are available to SDK customers on Core, Superpowers, and Enterprise plans. We'd love your feedback at [beta-feedback@beefree.io](mailto:beta-feedback@beefree.io).
{% endhint %}

[Brand Rules](brand-rules-for-ai.md) tell the AI what the content it creates should look like. Reusable Rows go one step further: instead of asking the agent to build a brand-approved header, you hand it the header your users already approved, and the agent places that one.

### Why give the AI a row library

A generated row is new content that has to be checked. A reusable row is content that was already reviewed, is already on brand, and in the case of a synced row is still maintained at its source. For the designs where your users have a right answer on file, retrieving it beats regenerating it.

With a row library attached to the session, the agent can:

* search the library in the words the user actually used;
* read what a row contains before choosing it;
* place the right row into the design.

The agent never sees a row's raw JSON. It sees enough to choose, and it places by id.

### Attach a library to a session

A row library is attached when the session the agent works in is created. There are three ways to pass it, depending on how you use AI in the editor. In all three, the library is a `reusableRows` object with an `entries` array.

#### With the AI Co-Pilot

Pass the library as `reusableRows` in the settings of the `ai-agent` addon. The Co-Pilot attaches it to every MCP session it starts.

{% code overflow="wrap" %}
```javascript
const beeConfig = {
  // ...your standard config
  addOns: [
    {
      id: 'ai-agent',
      settings: {
        reusableRows: { entries: [ /* saved rows */ ] },
      },
    },
  ],
}
```
{% endcode %}

See [Using Reusable Rows with the AI Co-Pilot](ai-co-pilot-beta/#using-reusable-rows-with-the-ai-co-pilot).

#### With an editor-managed MCP session

Pass the library to `bee.startMcpSession()`. It is attached to the session that call creates.

```javascript
const { templateId } = await bee.startMcpSession({
  reusableRows: { entries: [ /* saved rows */ ] },
})
```

See [Editor-managed session](getting-started/mcp-server-installation-and-setup.md#editor-managed-session).

#### With an API-managed MCP session

Pass the library in the body of the template creation request, alongside the other keys of the request:

```
POST https://api.getbee.io/v2/sdk/mcp/template
```

{% code overflow="wrap" %}
```json
{
  "template": { ... },
  "reusableRows": {
    "entries": [
      {
        "metadata": {
          "name": "Primary header",
          "category": "Headers",
          "description": "Logo on the left, navigation on the right.",
          "tags": ["header", "navigation"]
        },
        "columns": [ ... ],
        "synced": false
      }
    ]
  }
}
```
{% endcode %}

See [API-managed session](getting-started/mcp-server-installation-and-setup.md#api-managed-session).

### The row library

An entry is a saved row in the shape the editor already produces (for example from `onSaveRow`), so a library you store for the row picker can be sent as it is. Only `metadata.name` and `columns` are required, and `metadata.description` is highly recommended. Properties not listed below are kept as they are, but neither checked nor searched: any other metadata field (your own ids, dates, a slug...) can stay in the row.

| Field                  | Type             | Description                                                                                                                                                        |
| ---------------------- | ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `metadata.name`        | string           | Required. What the row is called. The agent searches on it and reports it back to the user.                                                                        |
| `columns`              | array            | Required. The row's columns, at least one.                                                                                                                         |
| `metadata.category`    | string or number | A category name, or a numeric category id. Names are searched as text and filtered on case-insensitively. A numeric id can be filtered on, but is not searched as text. |
| `metadata.description` | string           | Highly recommended. One line on what the row is for: the agent searches it, and it is often what settles a choice between rows that look alike.                    |
| `metadata.tags`        | array or string  | An array of strings, or one comma-separated string (`"promo, blue"`) as saved rows often store them. Searched and offered as filters. The row keeps the format you sent. |
| `synced`               | boolean          | Marks a live shared row. See [Synced rows](#synced-rows-are-placed-never-edited).                                                                                  |
| `type`                 | string           | The row's layout, as the builder saves it.                                                                                                                         |
| `webFonts`             | array            | The fonts the row uses. They are added to the template when the row is placed.                                                                                     |

#### Limits

| Limit                         | Value                                                     |
| ----------------------------- | --------------------------------------------------------- |
| Rows per library              | 1,000                                                     |
| Row data per library          | About 1.5 MB                                              |
| Name, category, description   | 200 characters each                                       |
| Tags per row                  | 12, each up to 32 characters, also once a string is split |

#### What happens when a library does not fit

When a session is created, the library goes through these checks, in this order:

| Check                                   | Limit                                               | If it does not pass                                         |
| --------------------------------------- | --------------------------------------------------- | ----------------------------------------------------------- |
| Size of the whole request               | 3.5 MB                                              | Refused with `413`, no session                              |
| Plan                                    | Core or above                                       | Refused with `403`, no session                              |
| Size of the request without the library | 2 MB                                                | Refused with `413`, no session                              |
| Fields of each row                      | See [Limits](#limits)                               | Refused with `400` `Invalid reusableRows`, no session       |
| Number of rows                          | 1,000                                               | Trimmed: the first 1,000 are kept, the session starts        |
| Row data                                | About 1.5 MB                                        | Trimmed: rows are kept in order until the budget is full     |

A library with an empty `entries` array counts as no library: it is not checked against the plan, the fields or the trimming limits, and nothing is stored.

The two kinds of limit behave differently:

* **Rows and row data are trimmed, not refused.** A library over 1,000 rows or about 1.5 MB of row data is stored up to the limit, keeping the rows in the order you sent them, and the session starts. Put the rows that matter most first.
* **Everything else is refused.** A row that breaks a field limit (a name over 200 characters, an empty tag in an array, a missing `columns`...) makes the whole request fail with `400` and `{ "error": "Invalid reusableRows", "details": [...] }`, and no session is created. A request over 3.5 MB, or whose fields other than `reusableRows` add up to more than 2 MB, fails with `413` before any trimming.

When the editor starts the session (the AI Co-Pilot, or `bee.startMcpSession()`), a trimmed library is reported through the `onWarning` callback with code [`1770`](../resources/error-management/warning-error-info-callbacks.md). The `detail` says how many rows were kept and how many were dropped. Surface it in your integration: a silently partial library makes the agent answer "no such row" about rows your user can see in the editor.

With an API-managed session, `POST /v2/sdk/mcp/template` reports what was stored next to the `templateId`:

```json
{
  "templateId": "...",
  "reusableRows": {
    "entries": 1000,
    "sentEntries": 1200,
    "droppedEntries": 200,
    "categories": 4,
    "syncedEntries": 3,
    "taggedEntries": 800,
    "webFonts": 2,
    "bytes": 1536000
  }
}
```

Check `droppedEntries` and warn your users when it is there, as the editor does with `1770`. Without a library, the response has no `reusableRows`.

#### Validate a library before starting a session

The validation endpoint checks a `reusableRows` payload against the same rules without creating a session.

```
POST https://api.getbee.io/v2/sdk/mcp/template/validate
```

```json
{
  "reusableRows": { "entries": [ ... ] }
}
```

The response lists every problem at once:

```json
{
  "valid": false,
  "errors": ["reusableRows.entries.0.metadata.name must NOT have more than 200 characters"]
}
```

### The library is a copy for the session

The library is copied when the session is created, and the agent only ever works on that copy. Your own storage is never read again, so the copy can only be as up to date as the request that created the session:

| When                          | What the session has                                                                                                                         |
| ----------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------- |
| The session is created        | A copy of the rows you sent, checked and trimmed as described above. Each row gets the `reusableRowId` the agent uses.                         |
| A saved row changes in your storage | Nothing changes for this session: it keeps the copy it was created with. The change applies to the sessions created afterwards.         |
| The agent places a row        | A copy of the stored row, refitted to the template. It keeps its `metadata`, including your own ids and the `tags` format you sent.           |
| The session ends or expires   | The library is deleted with the session.                                                                                                     |

To keep the agent working on current rows, send the library every time a session is created, built from your storage at that moment. The AI Co-Pilot starts a new session for every prompt, so it picks up a changed `reusableRows` setting from the next prompt. With `bee.startMcpSession()`, pass the current library on each call. With an API-managed session, send it with each `POST /v2/sdk/mcp/template`.

A synced row is no exception: the agent places the version that was in the library when the session started.

### What the agent can do

With a library attached, the MCP Server exposes four more tools. They are offered only when the session has a library and your plan is Core or above. Otherwise the agent does not see them at all, and a direct call to one is refused.

| Tool                                | What it does                                                                                                                                                 |
| ----------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `beefree_search_reusable_rows`      | Find rows by free text, category, tags, block types, or synced status. Returns metadata only. Where the agent always starts.                                   |
| `beefree_get_reusable_rows_facets`  | List the categories and tags this library actually uses, with a count for each. Lets the agent filter on real values rather than guessing.                     |
| `beefree_get_reusable_rows_details` | Derived facts about up to five rows at once: their text, colours, block types, columns, link and image counts, fonts. For choosing between close candidates.    |
| `beefree_add_reusable_row`          | Place one row into the template, by id, at a position. Without a position, the row is added at the end.                                                       |

#### Search returns metadata, never content

A search answer describes a row: its id, name, category, synced flag, and where available its tags, description, a preview of the row's own words, and its structure (block types, column count, whether it has images or links). It never returns the row's content. That keeps the answer small enough that an agent can look at many rows before committing to one.

The free-text search matches a row's name, tags, description, category name and the row's own words. Every word must appear somewhere in the row, in any order and in any of those fields, and the match ignores case, so the user's own phrasing usually works. Filters on category, tags, block types and synced status narrow further; by default a row must pass all of them, or any one of them when the agent asks for it.

Results are capped and there is no paging. When the cap is hit, the answer says `truncated: true`, and the right move is a narrower search rather than another page.

#### An empty result is informative

When nothing matches, the answer explains which filter was too narrow and what dropping it would return. An agent that reads this recovers on its next call instead of guessing at another query.

The answer also catches the misses that look like an empty library: a category or tag the library does not use is reported, with the nearest values it does use, and a name that matched nothing comes back with the row names spelled most like it. When two returned rows share a name, the answer says so, so the agent tells them apart before placing one.

This is also why `beefree_get_reusable_rows_facets` matters: it reports `rowsWithoutText`, the rows that carry no searchable words at all. Those cannot be found by a text search, so an empty result is not proof the library lacks what the user asked for.

#### Synced rows are placed, never edited <a href="#synced-rows-are-placed-never-edited" id="synced-rows-are-placed-never-edited"></a>

A row with `synced: true` is a live shared row. The agent places it like any other, but cannot change it afterwards: adding, updating or deleting a block in it, or changing its section or column styles, is refused. A synced row is edited at its source, and changing one copy would break every design using it. Removing the whole row from the design is allowed, unless the row is also `locked`.

#### A placed row is refitted, not copied

`beefree_add_reusable_row` does not paste the saved JSON. The row is refitted to the template it lands in: module widths are recomputed for the template's width, and the fonts it needs are added to the page. It also gets fresh ids, so the same saved row can be placed more than once in one design.

### Writing a library the AI can actually search

The agent is only as good as the words you give it. Three things pay for themselves:

1. **Name rows the way users talk.** "Black Friday hero" is findable. "Row 12 v3 final" is not.
2. **Write the one-line description.** It is highly recommended: it is searched, and it is usually what decides between two rows that look alike from their names.
3. **Keep categories and tags small and consistent.** The agent reads the real list before filtering, so twenty tidy tags work better than two hundred near-duplicates. Prefer category names over numeric ids: names are searched as text, ids are not.

### Frequently asked questions

**What happens if I create a session without `reusableRows`?**\
The four tools are not offered at all. Nothing else changes. A library with an empty `entries` array counts as no library: it is not stored and does not need a Core plan.

**What happens on a plan below Core?**\
Creating a session with `reusableRows` is refused with `403`. The tools are not offered on those plans.

**Can the agent save a new row to the library?**\
No. The library is read-only for the session. Rows are created and maintained through the normal [Reusable Content](../rows/reusable-content/) flows.

**Can I change the library during a session?**\
No. It is attached at creation and fixed for the life of the session (see [The library is a copy for the session](#the-library-is-a-copy-for-the-session)). Start a new session to attach a different library. The AI Co-Pilot starts a new session for every prompt, so a change to its `reusableRows` setting applies from the next prompt.

**Does the library count against the template payload?**\
No. The row data has its own budget of about 1.5 MB, and everything else in the request (template, merge tags, brand rules...) has 2 MB. The whole request is capped at 3.5 MB, so a library sent over its budget still reaches the session and is trimmed, as long as the request stays within 3.5 MB.
