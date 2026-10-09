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

{% hint style="info" %}
Unlike `brandRules` and `mergeTags`, there is no `reusableRows` property at the root of the editor configuration. Pass the library to the Co-Pilot addon or to `startMcpSession()`.
{% endhint %}

#### With an API-managed MCP session

Pass the library in the body of the template creation request, alongside `template`, `mergeTags` and `brandRules`:

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

An entry is a saved row in the shape the editor already produces (for example from `onSaveRow`), so a library you store for the row picker can be sent as it is. Only `metadata.name` and `columns` are required. Properties not listed below are kept as they are.

| Field                  | Type             | Description                                                                                                                                                        |
| ---------------------- | ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `metadata.name`        | string           | Required. What the row is called. The agent searches on it and reports it back to the user.                                                                        |
| `columns`              | array            | Required. The row's columns, at least one.                                                                                                                         |
| `metadata.category`    | string or number | A category name, or a numeric category id. Names are searched as text and filtered on case-insensitively. A numeric id can be filtered on, but is not searched as text. |
| `metadata.description` | string           | One line on what the row is for. Worth writing: the agent searches it, and it is often what settles a choice.                                                      |
| `metadata.tags`        | array            | Searched and offered as filters.                                                                                                                                   |
| `metadata.slug`        | string           | Searched as text.                                                                                                                                                  |
| `metadata.uuid`        | string           | Your own id for the row. It is kept, but the agent does not use it to address the row.                                                                             |
| `synced`               | boolean          | Marks a live shared row. See [Synced rows](#synced-rows-are-placed-never-edited).                                                                                  |
| `type`                 | string           | The row type, as the editor saves it.                                                                                                                              |
| `webFonts`             | array            | The fonts the row uses. They are added to the template when the row is placed.                                                                                     |

{% hint style="warning" %}
Do not send a `reusableRowId`. Each row gets one when the library is stored, and the agent receives it from the search tool. A row is addressed by that id for the lifetime of the session, and any `reusableRowId` you send is replaced.
{% endhint %}

#### Limits

| Limit                         | Value                                                     |
| ----------------------------- | --------------------------------------------------------- |
| Rows per library              | 1,000                                                     |
| Row data per library          | About 1.5 MB                                              |
| Whole session request         | 2 MB, template and library together                       |
| Name, category, slug, description | 200 characters each                                   |
| `uuid`, `type`                | 64 characters each                                        |
| Tags per row                  | 12, each up to 32 characters                              |

`name`, `uuid`, each tag and a string `category` must not be empty.

#### What happens when a library does not fit

The two kinds of limit behave differently:

* **Rows and row data are trimmed, not refused.** A library over 1,000 rows or about 1.5 MB of row data is stored up to the limit, keeping the rows in the order you sent them, and the session starts. Put the rows that matter most first.
* **Everything else is refused.** A row that breaks a field limit (a name over 200 characters, an empty tag, a missing `columns`...) makes the whole request fail with `400` and `{ "error": "Invalid reusableRows", "details": [...] }`, and no session is created. A request over 2 MB fails with `413` before any trimming.

When the editor starts the session (the AI Co-Pilot, or `bee.startMcpSession()`), a trimmed library is reported through the `onWarning` callback with code `5120`. The `detail` says how many rows were kept and how many were dropped. Surface it in your integration: a silently partial library makes the agent answer "no such row" about rows your user can see in the editor.

{% hint style="warning" %}
With an API-managed session, `POST /v2/sdk/mcp/template` only returns the `templateId`, not what was stored. Keep the library within the limits on your side, and validate it as described below.
{% endhint %}

#### Validate a library before starting a session

The validation endpoint checks a `reusableRows` payload against the same rules without creating a session. It also accepts `brandRules` in the same request.

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

Validation does not check the row and size limits that trim a library, only the ones that would refuse it.

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

The free-text search matches a row's name, tags, description, slug, category name and the row's own words, so the user's own phrasing usually works.

Results are capped and there is no paging. When the cap is hit, the answer says `truncated: true`, and the right move is a narrower search rather than another page.

#### An empty result is informative

When nothing matches, the answer explains which filter was too narrow and what dropping it would return. An agent that reads this recovers on its next call instead of guessing at another query.

This is also why `beefree_get_reusable_rows_facets` matters: it reports `rowsWithoutText`, the rows that carry no searchable words at all. Those cannot be found by a text search, so an empty result is not proof the library lacks what the user asked for.

#### Synced rows are placed, never edited <a href="#synced-rows-are-placed-never-edited" id="synced-rows-are-placed-never-edited"></a>

A row with `synced: true` is a live shared row. The agent is instructed to place it like any other, but never to update, restyle or delete it afterwards: a synced row is edited at its source, and changing one copy would break every design using it.

{% hint style="info" %}
This is an instruction the agent follows, not a lock on the placed blocks.
{% endhint %}

#### A placed row is refitted, not copied

`beefree_add_reusable_row` does not paste the saved JSON. The row is refitted to the template it lands in: module widths are recomputed for the template's width, and the fonts it needs are added to the page. It also gets fresh ids, so the same saved row can be placed more than once in one design.

A placed row's ids are only known once the placement has run. A direct tool call returns them as `sectionId` and `columnIds`. In [Code Mode](getting-started/mcp-server-installation-and-setup.md) the placement runs when the script ends, so a script cannot place a row and edit a block inside it in the same run: the agent places the row, then reads the content and edits it in its next step.

### Works with the rest of the session

[Brand Rules](brand-rules-for-ai.md) still apply to everything the agent builds itself.

{% hint style="warning" %}
A reusable row is placed as one unit, so `permissions.noAdd` is not applied to the blocks inside it. If your rules forbid the agent from adding an HTML block, a saved row that already contains one is still placed. Curate the library with the same care you put into the rules: the rows you attach are content you have already approved.
{% endhint %}

Reusable Rows also work in [Code Mode](getting-started/mcp-server-installation-and-setup.md), where the same four capabilities are available to the agent's scripts as `searchReusableRows`, `getReusableRowsFacets`, `getReusableRowsDetails` and `addReusableRow`.

### Writing a library the AI can actually search

The agent is only as good as the words you give it. Three things pay for themselves:

1. **Name rows the way users talk.** "Black Friday hero" is findable. "Row 12 v3 final" is not.
2. **Write the one-line description.** It is searched, and it is usually what decides between two rows that look alike from their names.
3. **Keep categories and tags small and consistent.** The agent reads the real list before filtering, so twenty tidy tags work better than two hundred near-duplicates. Prefer category names over numeric ids: names are searched as text, ids are not.

### FAQs

**What happens if I create a session without `reusableRows`?**\
The four tools are not offered at all. Nothing else changes.

**What happens on a plan below Core?**\
Creating a session with `reusableRows` is refused with `403`. The tools are not offered on those plans.

**Can the agent save a new row to the library?**\
No. The library is read-only for the session. Rows are created and maintained through the normal [Reusable Content](../rows/reusable-content/) flows.

**Can I change the library during a session?**\
No. It is attached at creation and fixed for the life of the session. Start a new session to attach a different library. The AI Co-Pilot starts a new session for every prompt, so a change to its `reusableRows` setting applies from the next prompt.

**Does the library count against the template payload?**\
The row data has its own budget of about 1.5 MB. The whole session request, template and library together, is capped at 2 MB.
