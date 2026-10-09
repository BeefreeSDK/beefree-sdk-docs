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

A row library is attached when the MCP session is created, the same way `brandRules` and `mergeTags` are. Pass a `reusableRows` object in the body of the template creation request:

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

An entry is a saved row in the shape the editor already produces, so a library you store for the row picker can be sent as it is. Only `metadata.name` and `columns` are required.

| Field                  | Type    | Description                                                                                                  |
| ---------------------- | ------- | ------------------------------------------------------------------------------------------------------------ |
| `metadata.name`        | string  | Required. What the row is called. The agent searches on it and reports it back to the user.                   |
| `columns`              | array   | Required. The row's columns, at least one.                                                                    |
| `metadata.category`    | string  | A plain human-readable name, filtered on as it is written.                                                   |
| `metadata.description` | string  | One line on what the row is for. Worth writing: the agent searches it, and it is often what settles a choice. |
| `metadata.tags`        | array   | Up to 12 tags, searched and offered as filters.                                                              |
| `synced`               | boolean | Marks a live shared row. See [Synced rows](#synced-rows-are-placed-never-edited).                             |

{% hint style="warning" %}
Do not send a `reusableRowId`. It is assigned when the library is stored and returned to the agent by the search tool. A row is addressed by that id for the lifetime of the session.
{% endhint %}

#### Limits

A library is trimmed to fit, in the order you sent it, and the creation response tells you what was stored.

| Limit        | Value                             |
| ------------ | --------------------------------- |
| Entries      | 1,000                             |
| Payload      | 1.5 MB, shared with the template   |
| Name         | 200 characters                    |
| Description  | 200 characters                    |
| Tags per row | 12, each up to 32 characters      |

The response carries a `reusableRows` summary rather than the library you just sent:

```json
{
  "sessionId": "...",
  "reusableRows": {
    "entries": 112,
    "categories": 9,
    "syncedEntries": 15,
    "taggedEntries": 74,
    "bytes": 384210,
    "webFonts": 3
  }
}
```

{% hint style="warning" %}
When a library does not fit whole, the summary also carries `sentEntries` and `droppedEntries`. Surface that in your integration. A silently partial library makes the agent answer "no such row" about rows your user can see in the editor.
{% endhint %}

### What the agent can do

With a library attached, the MCP Server exposes four more tools. They appear only in sessions that have a library, so an agent working on a session without one is never tempted to look for rows that are not there.

| Tool                                | What it does                                                                                                                                                 |
| ----------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `beefree_search_reusable_rows`      | Find rows by free text, category, tags, block types, or synced status. Returns metadata only. Where the agent always starts.                                   |
| `beefree_get_reusable_rows_facets`  | List the categories and tags this library actually uses, with a count for each. Lets the agent filter on real values rather than guessing.                     |
| `beefree_get_reusable_rows_details` | Derived facts about up to five rows at once: their text, colours, block types, columns, link and image counts, fonts. For choosing between close candidates.    |
| `beefree_add_reusable_row`          | Place one row into the template, by id, at a position.                                                                                                        |

#### Search returns metadata, never content

A search answer describes a row: its id, name, category, synced flag, and where available its tags, description, a preview of the row's own words, and its structure (block types, column count, whether it has images or links). It never returns the row's content. That keeps the answer small enough that an agent can look at many rows before committing to one.

Results are capped and there is no paging. When the cap is hit, the answer says `truncated: true`, and the right move is a narrower search rather than another page.

#### An empty result is informative

When nothing matches, the answer explains which filter was too narrow and what dropping it would return. An agent that reads this recovers on its next call instead of guessing at another query.

This is also why `beefree_get_reusable_rows_facets` matters: it reports `rowsWithoutText`, the rows that carry no searchable words at all. Those cannot be found by a text search, so an empty result is not proof the library lacks what the user asked for.

#### Synced rows are placed, never edited <a href="#synced-rows-are-placed-never-edited" id="synced-rows-are-placed-never-edited"></a>

A row with `synced: true` is a live shared row. The agent may place it like any other, but never updates, restyles or deletes it afterwards. A synced row is edited at its source, and changing one copy would break every design using it.

#### A placed row is refitted, not copied

`beefree_add_reusable_row` does not paste the saved JSON. The row is refitted to the template it lands in: module widths are recomputed for the template's width, and the fonts it needs are added to the page. It also gets fresh ids, so the same saved row can be placed more than once in one design.

Those ids are only known once the call returns, as `sectionId` and `columnIds`. An agent therefore cannot place a row and edit a block inside it in the same operation. It places the row, reads the response, and edits on the next turn.

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
3. **Keep categories and tags small and consistent.** The agent reads the real list before filtering, so twenty tidy tags work better than two hundred near-duplicates.

### FAQs

**What happens if I create a session without `reusableRows`?**\
The four tools are not offered at all. Nothing else changes.

**Can the agent save a new row to the library?**\
No. The library is read-only for the session. Rows are created and maintained through the normal [Reusable Content](../rows/reusable-content/) flows.

**Can I change the library during a session?**\
No. It is attached at creation and fixed for the life of the session. Create a new session to attach a different library.

**Does the library count against the template payload?**\
Yes. The 1.5 MB budget is shared with the template in the same request.
