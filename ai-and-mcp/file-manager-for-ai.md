---
description: >-
  Let the AI find, save, and clean up images in your users' File Manager while
  it designs, only in the folders you allow.
---

# File Manager for AI

{% hint style="info" %}
File Manager for AI is available to all Beefree SDK customers who use the [MCP Server](getting-started/) or the [AI Co-Pilot](ai-co-pilot-beta/), on any plan that includes them. We'd love your feedback at [beta-feedback@beefree.io](mailto:beta-feedback@beefree.io).
{% endhint %}

The agent can already find stock images with `beefree_search_stock_images`. File Manager for AI goes one step further: the agent works with the images your users already have, and saves the ones it brings in where your users will find them again, in the folders you allow.

### Why give the AI access to the File Manager

The right image for a design is often one your users already uploaded: their logo, a product shot, the hero of last month's campaign. Without the File Manager, the agent can only reach for a stock photo or ask the user for a link. An image placed from a link also stays a link: it never reaches your users' File Manager, so they cannot find it there and reuse it in their next design.

With the File Manager attached to the session, the agent can:

* list a folder and search files by name;
* reuse an image your user already has;
* save an image from a URL into the File Manager, then place it in the design;
* delete a file it no longer needs.

The agent works in one user's File Manager and, for each operation, only in the folders you allow. It handles files, not folders: it never deletes a folder, and the only folders it can create are the upload folders you list and the folders that lead to them.

### Attach the File Manager to a session

The File Manager is attached when the session the agent works in is created, and it stays the same for the life of the session. There are three ways to pass it, depending on how you use AI in the editor. In all three, it is a `fileManager` object with the folders the agent can use for each operation, and [Code Mode](getting-started/mcp-server-installation-and-setup.md#code-mode) works with all three. The examples below give the agent the same access: it can read the whole File Manager, save files to `/AI Generated Images`, and delete nothing.

From the editor, with the AI Co-Pilot or `bee.startMcpSession()`, you pass only the folders: the agent works in the File Manager of the `uid` the editor was started with (see [Whose File Manager the agent works in](#whose-file-manager-the-agent-works-in)).

#### With the AI Co-Pilot

Pass the folders as `fileManager` in the settings of the `ai-agent` addon. The Co-Pilot attaches them to the MCP session it starts for a prompt. If the session of an earlier prompt is still open, or the editor joined a session with `bee.join()`, the prompt runs in that session instead, and the File Manager that session was created with applies.

{% code overflow="wrap" %}
```javascript
const beeConfig = {
  // ...your standard config
  addOns: [
    {
      id: 'ai-agent',
      settings: {
        fileManager: {
          readPaths: ['/'],
          uploadPaths: ['/AI Generated Images'],
          deletePaths: [],
        },
      },
    },
  ],
}
```
{% endcode %}

See [Using the File Manager with the AI Co-Pilot](ai-co-pilot-beta/#using-the-file-manager-with-the-ai-co-pilot).

#### With an editor-managed MCP session

Pass the folders to `bee.startMcpSession()`. They are attached to the session that call creates. `fileManager` has no equivalent at the root of the editor configuration.

```javascript
const { templateId } = await bee.startMcpSession({
  fileManager: {
    readPaths: ['/'],
    uploadPaths: ['/AI Generated Images'],
    deletePaths: [],
  },
})
```

Calling it without `fileManager` starts a session without the file tools. If the editor is already in an MCP session, because one is still running or because it joined one with `bee.join()`, the call returns that session's `templateId` and the `fileManager` you pass is not applied: the session keeps the File Manager it was created with. See [Editor-managed session](getting-started/mcp-server-installation-and-setup.md#editor-managed-session).

#### With an API-managed MCP session

Pass a `fileManager` object in the body of the template creation request, alongside the other keys of the request. Here the object also names the end user whose File Manager the agent works in, with `uid`.

```
POST https://api.getbee.io/v2/sdk/mcp/template
```

{% code overflow="wrap" %}
```json
{
  "template": { ... },
  "fileManager": {
    "uid": "user-1234",
    "readPaths": ["/"],
    "uploadPaths": ["/AI Generated Images"],
    "deletePaths": []
  }
}
```
{% endcode %}

Connect the agent with the `templateId` the request returns, as in any API-managed session. This works in a headless session and in a session the editor joins with `bee.join()`. Joining the editor requires [co-editing](../other-customizations/collaborative-editing/), available on the Superpowers and Enterprise plans. See [API-managed session](getting-started/mcp-server-installation-and-setup.md#api-managed-session).

### The `fileManager` object

The object names the folders the agent can use for each operation. In an API-managed session, its `uid` also names whose File Manager the agent works in, and is the only required field. From the editor, every field is optional, and `fileManager: {}` is enough to turn the tools on.

| Field         | Type             | Description                                                                                                                                                                                                      |
| ------------- | ---------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `uid`         | string           | Required in an API-managed session: the end user whose File Manager the agent works in, the same `uid` you use to start the editor for that user. From the editor, leave it out: the `uid` the editor was started with is used, and a `uid` you send is ignored. See [Whose File Manager the agent works in](#whose-file-manager-the-agent-works-in). |
| `readPaths`   | array of strings | The folders the agent can list and search, with every folder inside them. Defaults to `["/AI Generated Images"]`. `[]` turns listing and searching off.                                                          |
| `uploadPaths` | array of strings | The folders the agent can save files to, directly or in a folder that already exists inside them. Defaults to `["/AI Generated Images"]`. `[]` turns uploading off.                                              |
| `deletePaths` | array of strings | The folders the agent can delete files from, with every folder inside them. Defaults to `["/AI Generated Images"]`. `[]` turns deleting off.                                                                     |

Each list stands on its own, and leaving one out is not the same as sending it empty:

* **A list you leave out is not empty.** It falls back to `/AI Generated Images`. Unless your application has a [Customer Shared Folder](#whose-file-manager-the-agent-works-in), a `fileManager` with only a `uid`, or `fileManager: {}` from the editor, lets the agent list, search, save, and delete files in that one folder.
* **An empty list turns the operation off.** With `"deletePaths": []`, the agent has no tool to delete files at all.
* **Without a `fileManager`, there are no file tools.** Leaving out the whole object is not the same as sending `{}` from the editor.

#### Folder paths

* A path starts with `/` and names a folder from the root of the File Manager, for example `/Brand/Logos`. `/` alone is the whole File Manager.
* Matching is exact, case included: `/brand` is not `/Brand`.

#### Limits

| Limit                      | Value |
| -------------------------- | ----- |
| Folders per list           | 20    |
| Upload file types and size | Whatever your application allows for File Manager uploads: by default, images, videos, and PDFs up to 20 MB. See [Mime Types and Groups](../file-manager/file-manager-application-overview/file-extensions-and-groups.md). |

#### What happens when a configuration is invalid

A `fileManager` that breaks one of these rules (a path that does not start with `/`, a `..` segment, more than 20 folders on a list, a missing `uid` in an API-managed session...) makes the whole request fail with `400`, and no session is created. `details` lists what is wrong:

```json
{
  "error": "Invalid fileManager",
  "details": [
    "fileManager must have required property 'uid'",
    "fileManager.uploadPaths.0 must match pattern \"^/\""
  ]
}
```

Problems with the shape of the object (a missing `uid`, a wrong type, a value too long or too short, a path without the leading `/`) are reported together. The check for `.`, `..`, and empty segments runs once those pass.

From the editor, no session is created either. `bee.startMcpSession()` is rejected with the message `Failed to start MCP session: Invalid fileManager`, with `400` in `detail.status` and the same list in `detail.details` (see [Error handling](getting-started/mcp-server-installation-and-setup.md#error-handling)). The AI Co-Pilot does not send the prompt, and shows a generic error with a Retry button: check its `fileManager` with the [validation endpoint](#validate-a-configuration-before-starting-a-session) to find what is wrong.

A valid configuration is always attached to the session the request creates, and the response is the same `{ "templateId": "..." }` as without one.

#### Validate a configuration before starting a session

The validation endpoint checks a `fileManager` object against the same rules without creating a session. It always requires a `uid`. To check the folders you pass from the editor, add the `uid` the editor was started with to the object you validate: the endpoint requires it, while the editor ignores a `uid` you send.

```
POST https://api.getbee.io/v2/sdk/mcp/template/validate
```

```json
{
  "fileManager": {
    "uid": "user-1234",
    "readPaths": ["Brand"]
  }
}
```

The response lists what is wrong:

```json
{
  "valid": false,
  "errors": ["fileManager.readPaths.0 must match pattern \"^/\""]
}
```

### Whose File Manager the agent works in

The `uid` names the end user. The agent works in that user's File Manager: the same files your user sees in the File Manager inside the editor, and the same ones the [File Manager endpoints](../apis/content-services-api/file-manager.md) of the Content Services API reach with that `uid` in `X-BEE-Uid`. Users who share a `uid` share a File Manager, as they do in the editor. See [How the UID parameter works](../getting-started/readme/installation/how-the-uid-parameter-works.md).

Where the `uid` comes from depends on how the session is created:

* **From the editor**, with the AI Co-Pilot or `bee.startMcpSession()`, it is the `uid` the editor was started with: the one your server sent to `/loginV2` when it requested the editor's token (see [Authorization Process](../getting-started/readme/installation/authorization-process-in-detail.md#beefree-sdk-server-side-login)). A `uid` in `fileManager` is ignored, so a page cannot point the agent at another user's files.
* **In an API-managed session**, it is the `uid` in `fileManager`.

When the editor has joined an API-managed session with `bee.join()`, the AI Co-Pilot and `bee.startMcpSession()` do not create a session of their own: the agent works in the joined session, with the `fileManager` of its template creation request, `uid` included, or without the file tools if that request had none.

The `uid` is fixed when the session is created and no tool takes one, so the agent cannot reach another user's files, whatever it is asked. An editor-managed session has a single real user, the person using the editor. In an API-managed session the editor joins with `bee.join()`, several users can prompt the agent, but it always works in the File Manager of the `uid` in `fileManager`, whoever asks. Use the `uid` of the user who owns the design, or keep `uploadPaths` and `deletePaths` narrow.

A file the agent saves is an ordinary file in that File Manager. Your user finds it there the next time they open the File Manager, and can use, move, or delete it like any other.

The tools have the same [storage requirements](../apis/content-services-api/file-manager.md#storage-requirements) as the File Manager endpoints. File Manager for AI does not support applications configured with CDN segmentation, a custom domain, or a custom file system provider.

If your application has a Customer Shared Folder, your users' own files are in `/myfiles`, and `/shared` is read-only. The default `/AI Generated Images` sits at the root, outside `/myfiles`, so do not rely on the defaults: set `uploadPaths` and `deletePaths` to folders inside `/myfiles`, for example `["/myfiles/AI Generated Images"]`, and `readPaths` to the folders the agent should read. See [The storage root and reserved directories](../apis/content-services-api/file-manager.md#the-storage-root-and-reserved-directories).

### What the agent can do

With a `fileManager` attached, the MCP Server exposes up to four more tools; in Code Mode, up to four more functions the script can call. Each one is offered only when the list for its operation has at least one folder. Otherwise the agent does not see it at all: a direct call to the tool is refused, and in Code Mode the function is not defined.

| Tool                   | Needs         | What it does                                                                                          |
| ---------------------- | ------------- | ----------------------------------------------------------------------------------------------------- |
| `beefree_list_files`   | `readPaths`   | List the files and folders directly inside a folder, with no paging.                                  |
| `beefree_search_files` | `readPaths`   | Find files by name in a folder and every folder inside it, or in all the folders the agent can read. |
| `beefree_upload_file`  | `uploadPaths` | Save a file from a URL into a folder, and return it with its public URL.                              |
| `beefree_remove_file`  | `deletePaths` | Delete one file. Folders are never deleted.                                                           |

A file is always addressed by its full path, such as `/AI Generated Images/hero.jpg`. Every file the tools return has the same fields: `name`, `filePath` (its full path, as the other tools take it), `folderPath`, `type`, `mimeType`, `size` in bytes, `url` (its public URL), `thumbnailUrl`, and, when known, `modifiedAt`.

#### Search matches file names

`beefree_search_files` looks through a folder and every folder inside it, or through all the folders the agent can read. It matches file names, not what a file contains, and it ignores case. By default, the term can be any part of the name. The agent can also match the start of the name, the exact name with its extension, or similar names: a fuzzy match tolerates typos and several words, and puts the best match first.

Results are capped and there is no paging. A search returns at most 200 files across all the folders it covers. When the cap is hit, the answer says `truncated: true`, and the right move is a narrower search rather than another page.

#### Uploads come from a URL

`beefree_upload_file` takes the file as a `sourceUrl`: Beefree SDK fetches the file from that URL, server-side. File content cannot be sent inline, as base64 or otherwise: a model copying a long file's bytes into a call can corrupt them without noticing, and the broken file would be stored as if it were fine.

The URL must be reachable from Beefree SDK's servers with a plain request, without credentials, and must return the file itself once any redirects are followed. A public URL, a stock image URL, or a pre-signed link that is still valid all work; a page behind a login does not. A URL that contains a comma (`,`) is not supported, which rules out some image CDN transformation URLs.

The file name must end with an extension, and the extension decides the stored file type. Beyond that, an upload goes through the same checks as any other upload to your File Manager, and a file the File Manager refuses comes back to the agent with the File Manager's own error.

The download counts toward the 30 seconds a tool call has. If an upload times out, the file may still have been saved: list the folder before trying again, or the new attempt can store a second, numbered copy.

#### Uploads do not create subfolders

The agent saves a file directly into an upload folder, or into a folder inside one that already exists. A folder inside an upload folder that does not exist is refused, never created, and the refusal tells the agent where to store the file instead. Subfolders are created in the File Manager, by your users or through the [File Manager endpoints](../apis/content-services-api/file-manager.md#create-a-directory).

An upload folder that does not exist yet, such as `/AI Generated Images` before its first file, is created by the first upload into it, together with any missing folders above it.

#### When a file already exists

The agent chooses what happens when the name it saves to is taken:

* **Keep both, the default.** The new file is saved under a numbered name: `hero.jpg` becomes `hero_1.jpg`, with its own URL. The answer returns the name and URL actually stored, and those are the ones to use.
* **Replace.** The file's content is overwritten, and its name and public URL stay the same. Anything that already links to that URL, in other designs or in emails already sent, shows the new file once caches refresh, although some email clients can keep showing a copy they cached earlier.
* **Fail.** Nothing is saved, and the agent is told that a file with that name already exists.

If the files in a folder must never change, keep that folder out of `uploadPaths`.

#### Deletion removes one file, never a folder

`beefree_remove_file` deletes one file, by its full path, in a folder of `deletePaths` or a folder inside one. It never deletes a folder. A file that does not exist is reported as not found, and nothing is deleted.

A deleted file's public URL stops working, so a design or an email already sent that shows the file loses that image. Allow deletion only in folders whose files are safe to remove.

#### A saved image is placed by its URL

The `url` of a stored file is what the agent uses as the image source when it adds or updates an image block. A typical flow: the agent finds a photo with `beefree_search_stock_images`, saves it with `beefree_upload_file`, and places it with `beefree_add_image` using the `url` the upload returns. The design then uses the copy in your user's File Manager, which your user can find and reuse in the next design.

In Code Mode, the file tools run as soon as the script calls them, so one script can save an image and place it with the returned `url`.

#### When a call is refused

A refused call is not an error in your integration: the agent gets a message that says what went wrong, and it usually recovers on its next call. In Code Mode, the script gets an error with the same message, prefixed with the function name. These are the messages to look for in your agent's logs when a file is not where you expected it:

| Message contains                            | Why                                                                                                                                                                      |
| ------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `is not enabled for this session`           | The session has no `fileManager`, or the list for that operation is `[]`. In Code Mode, the function is not defined instead.                                             |
| `is outside the folders this session can`   | The path is not in the list for that operation (`read`, `upload to`, or `delete from`), often because of case. The message ends with the folders that are allowed.      |
| `does not exist (paths are case-sensitive)` | An upload into a folder that does not exist inside an upload folder. The message says where to store the file instead.                                                  |
| `must end with the file name and extension` | An upload path without a file extension.                                                                                                                                 |
| `a file with that name already exists`      | An upload that asked to fail when the name is taken.                                                                                                                     |
| `not found`                                 | The folder or file does not exist.                                                                                                                                       |
| `only files can be removed`                 | A deletion pointed at a folder.                                                                                                                                          |
| `failed (status <code>)`                    | The File Manager refused the request, for example a file type or size it does not allow, or a `sourceUrl` it could not download. The rest of the message is the File Manager's own error. |
| `upstream error` or `internal error`        | The File Manager did not answer in time, for example because the download from `sourceUrl` was too slow. An upload may still have been saved.                           |

### Choosing folders for the agent

The agent can only be as careful as the folders you give it. Four things pay for themselves:

1. **Name the folders in your prompt.** The agent is not told which folders it can use: it finds out when a call is refused. Say it up front, in your system prompt or in the request: "Brand images are in /Brand. Save new images to /AI Generated Images." With the AI Co-Pilot, let your users name the folders in their prompts; on the Superpowers and Enterprise plans, you can also name them in its [`systemPrompt`](ai-co-pilot-beta/#custom-system-prompt) setting.
2. **Read wide, write narrow.** Reading changes nothing; saving and deleting change what your users see. A safe start reads the whole File Manager (`"readPaths": ["/"]`), saves to one folder, and deletes nowhere. A list left out falls back to `/AI Generated Images`, so pass `"deletePaths": []` unless the agent should clean up after itself.
3. **Create subfolders ahead of time.** The agent cannot create a folder inside an upload folder. To have it file images by campaign or brand, create those folders first, in the File Manager or with the [File Manager endpoints](../apis/content-services-api/file-manager.md#create-a-directory).
4. **Say when images must be saved first.** The agent can also place an image straight from its URL, without saving it. If every image in your users' designs should come from their File Manager, say so in your prompt.

### Frequently asked questions

**What happens if I create a session without `fileManager`?**\
The four tools are not offered at all. Nothing else changes: the agent can still find stock images and place images from a URL.

**Can I attach the File Manager to an editor-managed session or to the AI Co-Pilot?**\
Yes. Pass the folders as `fileManager` to `bee.startMcpSession()`, or in the `settings` of the `ai-agent` addon for the AI Co-Pilot. See [Attach the File Manager to a session](#attach-the-file-manager-to-a-session).

**Can the agent reach another user's files?**\
No. The `uid` is fixed when the session is created, and no tool takes one. From the editor, it is the `uid` the editor was started with, whatever the page sends, unless the editor joined an API-managed session with `bee.join()`: then it is the `uid` in that session's `fileManager`. See [Whose File Manager the agent works in](#whose-file-manager-the-agent-works-in).

**Can the agent upload a file as base64, or a file from my computer?**\
No. Uploads take a URL only. Put the file where Beefree SDK's servers can reach it, such as a pre-signed link that stays valid while the agent works, and give the agent that URL. See [Uploads come from a URL](#uploads-come-from-a-url).

**Can the agent create, move, or delete folders?**\
It creates only the upload folders you list, with any missing folders above them, on the first upload into them. It never creates a folder inside one, never moves or renames a file or a folder, and deletes files only. Folders are managed in the File Manager or with the [File Manager endpoints](../apis/content-services-api/file-manager.md).

**Can I change the folders during a session?**\
No. The `fileManager` object is fixed for the life of the session. Create a new session to change it. The AI Co-Pilot attaches its `fileManager` setting when it starts a session for a prompt, so a change applies from the next session it starts (see [With the AI Co-Pilot](#with-the-ai-co-pilot)).

**How do I know the agent has the file tools?**\
List the session's tools from your MCP client once the agent is connected. In Code Mode, read the description of the single tool Code Mode exposes instead: the file functions are documented there only when the session has them. The template creation response is the same with or without a `fileManager`.
