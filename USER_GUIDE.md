<p align="center">
<img src="docs/images/coda-devbot.png" alt="Codayak — the devbot" width="260">
</p>

<h1 align="center">Codayak — User Guide</h1>

<p align="center"><strong>The full reference for everyday use of Codayak — every feature, setting and workflow in one place.</strong></p>

<p align="center">
  <img src="https://img.shields.io/badge/platform-Windows-0078d4" alt="Platform: Windows">
  <img src="https://img.shields.io/badge/.NET-8-512bd4" alt="Built on .NET 8">
  <img src="https://img.shields.io/badge/licence-free%20for%20personal%20%26%20commercial%20use-2ea44f" alt="Licence: free for personal and commercial use">
  <img src="https://img.shields.io/badge/version-1.5-informational" alt="Version 1.5">
</p>

For a short overview of what Codayak is and why you'd use it, see [README.md](README.md).

If you're brand new, start with **[Get running fast](#get-running-fast)** below — it gets you to a working setup in a few minutes and tells you which options are worth switching on first. Everything after that is reference material you can dip into as you need it.

---

**Getting started** — [Get running fast](#get-running-fast) · [The activity bar](#the-activity-bar) · [Chat](#chat) · [Working with a repository](#working-with-a-repository) · [Tools](#tools)

**Feature reference** — [The Coordinator](#the-coordinator-multi-file-builds) · [Learning memory](#learning-memory) · [Trust Engine](#trust-engine-verification) · [Repository intelligence](#repository-intelligence) · [Team Mode](#team-mode) · [Image generation](#image-generation) · [Speech and Conversation Mode](#speech-tts-stt-conversation-mode) · [Meeting Assistant](#meeting-assistant) · [DevOps integration](#devops-integration) · [Skills](#skills) · [Database execution](#database-execution) · [Research panel](#research-panel) · [Worker LLM](#worker-llm)

**Reference** — [Help section](#help-section) · [Settings reference](#settings-reference) · [Keyboard shortcuts](#keyboard-shortcuts) · [Versioning](#versioning) · [Troubleshooting](#troubleshooting) · [Where things live on disk](#where-things-live-on-disk)

---

## Get running fast

The goal of this section: from a fresh install to genuinely useful in about five minutes. Codayak needs two keys to be fully capable — an **LLM provider key** (essential) and a **Google web search key** (needed for web searching) — then a couple of options are worth switching on before you start.

### 1. Add an LLM key

Nothing works until Codayak can reach a model.

1. Open **Settings** (⚙ in the activity bar) → **LLM Providers**, paste an API key for at least one provider, and click **Save**. Any one will do; if you're unsure, **Anthropic** is a strong default for code reasoning.
2. Pick a provider and model in the top toolbar. Codayak remembers the choice across restarts.

**Where to get a key** — sign up with the provider, add billing if it asks, and create a key in its developer console:

| Provider | Where to get the key |
|---|---|
| **Anthropic** | [console.anthropic.com](https://console.anthropic.com) → **API Keys** → *Create Key* |
| **OpenAI** | [platform.openai.com](https://platform.openai.com) → **API keys** → *Create new secret key* |
| **Google (Gemini)** | [aistudio.google.com](https://aistudio.google.com) → **Get API key** |
| **xAI (Grok)** | [console.x.ai](https://console.x.ai) → **API Keys** |
| **MiniMax · Moonshot · Zhipu** | Each provider's developer console → API keys |

The key is a long string (often starting `sk-`). Treat it like a password: paste it into Codayak and store it nowhere else — it lives only in your local settings file and is sent only to that provider.

More detail: **[LLM Providers](#llm-providers)** and **[Chat Models](#chat-models)** in the Settings reference.

### 2. Add web search — needed for web searching capability

Codayak's `SearchInternet` tool is Google Custom Search: without a Google API key **and** a Custom Search Engine ID it returns a configuration error and searches nothing at all. There is no built-in fallback search, and web search is the model's only window onto anything after its training cut-off — current library versions, API changes, today's error messages, release notes. Treat these two credentials as part of standard setup, not an optional extra.

1. **Google API key** — at [console.cloud.google.com](https://console.cloud.google.com), create (or pick) a project, enable the **Custom Search API** (**APIs & Services → Library** → search *Custom Search API* → **Enable**), then create the key under **APIs & Services → Credentials → Create credentials → API key**.
2. **Search Engine ID** — at [programmablesearchengine.google.com](https://programmablesearchengine.google.com), click **Add**, choose **Search the entire web**, create it, and copy the **Search engine ID** from its overview page.
3. Paste both into **Settings → Web Search** and click **Save**.

Google's free tier covers 100 searches a day; beyond that it bills about US$5 per 1,000 queries. (Fetching a direct URL you hand Codayak still works without these credentials — that path doesn't call the Google API.)

More detail: **[Web Search](#web-search)** in the Settings reference.

### 3. Other options worth switching on

- **Learning memory** — **Settings → Memory → Enable Learning Memory**. Cheap to run, and it compounds: Codayak learns from repeated failures and from anything you tell it to "remember", and surfaces those lessons automatically on later turns. The on-device embedder (~34 MB) that powers memory relevance downloads automatically on first launch; if it ever needs a manual retry, use **Download Now** at **Settings → General → Embedding Model**. More detail: [Learning memory](#learning-memory).
- **Trust Engine** — you can always ask Codayak to "verify this". Raise **Settings → Trust Engine → Self-verify** if you want it checking its own code unprompted. More detail: [Trust Engine](#trust-engine-verification).
- **Speech, images, DevOps** — add keys in **Settings → Audio Models**, **Settings → Visual Models** and **Settings → DevOps** as you need them. More detail: [Speech](#speech-tts-stt-conversation-mode) · [Image generation](#image-generation) · [DevOps integration](#devops-integration).
- **Trim the toolbox** — every enabled tool costs a little context. Switch off what you don't use in **Settings → Tools**. More detail: [Tools](#tools).

### 4. Basic usage

- **Chat** — press **Ctrl+Enter** to send (**Enter** inserts a new line; swap them in **Settings → Hot Keys**). Drag files in, or paste an image, to attach. More detail: [Chat](#chat).
- **Ask Codayak about Codayak** — Codayak can read its own README and user guide (that's the `ReadHelpDoc` tool), so questions like *"what can you do?"*, *"how do I turn on learning memory?"* or *"how do I set up a second provider?"* are answered from the real documentation, in chat, without you hunting through Settings. It is the fastest way to learn the app.
- **Point it at code** — **Select Repo** in the toolbar, then tick **Write to Repo** when you want Codayak to edit files. Codayak scans the folder (respecting `.codaignore`) and builds a source-code map. Leave **Write to Repo** *off* while you're getting comfortable — Codayak can still read, search, build and test, but can't modify anything. More detail: [Working with a repository](#working-with-a-repository).
- **Every change is reversible** — with **Write to Repo** on, every write is backed up to `.coda/backups/` first and shown as a side-by-side diff; ask Codayak to roll back if you don't like a change. More detail: [Diff view](#diff-view) and [Backups](#backups).
- **Help is always at hand** — the **❓** icon opens the README, this guide and the licence; **⚙ Settings** holds everything configurable.

That's the whole getting-started arc. The rest of this guide is per-feature depth.


---

## The activity bar

The vertical icon strip on the far left selects what fills the main panel:

| Icon | Section | Purpose |
|---|---|---|
| 💬 | Chat | The conversation. |
| 📁 | Repo | Repository selection, reference repos, source-code map preview. |
| 🤝 | Team Mode | Peer-to-peer collaboration with other Codayak instances. |
| 🎤 | Meeting | Meeting Assistant — live transcript, a curated Insights feed, and an end-of-meeting summary. |
| ❓ | Help | README and full user guide rendered inline, with Save and Print. |
| ⚙ | Settings | Everything configurable — providers, models, tools, memory, verification, code map, speech, images, web search, DevOps, skills, hotkeys, team mode. |

---

## Chat

### Sending messages

The message box at the bottom shows **"Type your message here…"** as a placeholder until you start typing. Click **Send** (or press **Ctrl+Enter**) to send. While streaming, the **Send** button becomes **Cancel**.

**Cancel stops everything, mid-flight.** Cancelling doesn't just stop the streamed text — it also stops the tool call currently running, whether that's a repository search, a file read, a network call (web search, DevOps, image generation), a `dotnet` build/test/run (the child process is killed), or a multi-file Coordinator build. Tools that modify files are careful about *where* they stop: a cancelled operation leaves either the original file or a completed write — never a torn, half-written one — and a cancelled directory copy leaves only complete files. The cancelled tool reports itself in the transcript as `[<Tool> cancelled]`.

**Send vs. new line.** The send gesture is configurable in **Settings → Hot Keys** (default **Ctrl+Enter**). A separate **New line in message box** gesture (default **Enter**) inserts a line break without sending. The two work together: if you reassign *Send message* to a bare **Enter**, set *New line in message box* to **Shift+Enter** to add a new line while composing. The input box honours both gestures directly, so Enter-to-send behaves correctly even though the box accepts multi-line text.

### Attaching files to your message

The attach buttons next to the input area let you add:
- **Files** — anything Codayak can read (PDF, DOCX, XLSX, code files, images).
- **Directories** — recursively scans for readable text and source files (up to 10 MB each).

**Drag-and-drop and paste.** You can also **drag files onto the message box** to attach them, and **paste** content directly: pasting an image from the clipboard (a screenshot or copied picture) saves it as a PNG and attaches it as a file, and pasting copied files from Explorer attaches them too. Ordinary text paste is unaffected.

**Working with Word documents.** Attach one or more `.docx` files and ask Codayak to summarise, revise, or combine them — it reads each document's text, and (via CreateWordDocument) can produce a new `.docx` that revises a single doc or merges several into one. You can also attach a `.dotx`/`.docx` template and ask Codayak to base the new document on it, so the output inherits the template's styles, headers/footers, and page layout. Note that attachment reading is **text-only**: the source documents' tables, images, and rich formatting are not carried into the merged output unless you supply a template for the look.

Attachments show as a chip on your message bubble. The full file list is preserved in the transcript even after the active attachment list is cleared for the next message.

### System prompt

The **System Prompt** section (above the message box) holds context sent on every message:
- Free-text instructions ("You are a senior C# engineer…").
- Attached reference files (always-on context).
- **Reference repositories** — code maps from other repos, shown to the LLM for pattern reference only, always in skeleton form.
- **Reference directories** — any folder you attach with **Add Directory** becomes a *browsable* read-only root: its files are attached as context AND the read tools (RequestSourceFiles, SearchCodebase, ListDirectory) can reach into it on demand via a `[Name]` path prefix (the folder's leaf name). A large directory is attached as a browsable file listing rather than inlined in full, and the model reads its files on demand. Unlike a reference repo, no source-code map is built — it's just a searchable/listable tree. It's never writable; the directory mutation tools only ever touch the working repo.
- **Reference wikis** — Azure DevOps or GitHub wiki page trees (see [Working with a repository](#reference-wikis)).

The system prompt persists across sessions.

### Streaming and tool calls

When the LLM responds, text streams in real-time. If it invokes a tool, you see a status update ("Patching file…", "Running .NET tests…") and the tool output appears as a separate block. The model then continues with the new information. This can loop up to **Max tool-call rounds** times (default 100, configurable in **Settings → Tools**).

### Browser conveniences in the chat view

The chat transcript is rendered in an embedded Chromium view (WebView2), so the standard browser niceties work inside it for free — nothing to enable:

- **Find on page** — **Ctrl+F** opens Chromium's in-page find bar to search the visible conversation (with next/previous and match count). Handy for jumping to a symbol or phrase in a long transcript.
- **Zoom** — **Ctrl++** / **Ctrl+-** to scale the chat text up and down, **Ctrl+0** to reset. (This is the view's own zoom, independent of the **Font size** setting, which sets the baseline.)
- **Select and copy** — click-drag to select any text and **Ctrl+C** to copy; code blocks keep their formatting. Right-click for the context menu (Copy, Select all).

These act only on the chat transcript pane. The composing box, system-prompt box, and other text fields are ordinary editable controls with the usual Cut/Copy/Paste/Undo (and their own right-click menu).

### Resetting the session

The **Reset** button opens a dialog with independent choices:
- **System prompt** — clear text and/or attached files.
- **Conversation** — keep all / prune older than N exchanges / **remove the most recent N exchanges** / clear everything.

This lets you pivot mid-task without losing your persona or repo context.

> **Recovering a stuck session:** try the cheapest fixes first. If a response stalls or comes back empty, simply ask Codayak to **continue** — a transient stall usually resumes cleanly. If the same model keeps stalling on the same conversation, **switch models in the toolbar and try again** (the conversation carries over); some stalls are specific to one model, and a different model — or the same one after a turn or two — often continues without issue. Only then reach for the surgical options: if a turn ends with a tool returning an enormous result, the next request can exceed the context window and fail *every* time — and "prune older than N" can't help because the offending turn is the newest one. Use **Remove the most recent N exchanges** to drop the poisoned tail while keeping your earlier work — or, more surgically, **right-click any of your messages in the transcript and choose Delete Turn**: it removes just that prompt and everything it produced (including an oversized tool result or image), even from the middle of the session. (Codayak also caps any single tool result stored in history, so this is rare — but the escape hatches are there.)

### Token meter

The top-right shows input tokens used vs the model's context window, broken down into System / Chat / Output reservation. When fill exceeds 90%, Codayak warns before sending.

### Saving and printing

The **💾 Save** button (or **Ctrl+S**) saves the conversation (Markdown, plain text, or HTML). The **🖨 Print** button (or **Ctrl+P**) prints via the native Windows pipeline.

### Auto-save

Tick the **Auto-save** checkbox (next to 💾 Save) to have Codayak re-save the full conversation as Markdown after every assistant response. Ticking it opens a folder picker; the session then writes to one timestamped `coda-conversation-YYYYMMDD-HHMMSS.md` file in that folder, overwriting it on each save so the file always holds the complete transcript. Auto-save is deliberately **session-only** — it is never restored on startup, and turning it off never deletes anything. The chosen destination shows below the user files list while active.

### Restore Session

Auto-saved (or manually saved) conversations can be brought back into a new session without flooding the context window with raw transcripts. Click **🕘 Restore Session** (below the user files list):

1. A file dialog opens — on the auto-save directory when auto-save is on, otherwise on the folder you last restored from. Multi-select the `coda-conversation-*.md` files to include.
2. If a summary already exists for that folder, choose **Yes** to update it incrementally (only conversations not already covered are processed — fast and cheap) or **No** to rebuild it from scratch (the escape hatch if the summary has drifted or been hand-edited badly).
3. Codayak distils the selected conversations with the **Worker LLM** into a compact session summary — current state, decisions with their rationale, open questions, and key facts. Tool payloads, file dumps, and oversized code blocks are stripped mechanically before the LLM sees anything, so distillation is fast and cheap relative to the transcript size. A wait cursor and status-bar progress show it working.
4. The result is written to `coda-session-summary.md` beside the transcripts and attached to the **system prompt** as a 🕘 chip. Its content is injected verbatim on every send — small, byte-stable (so it stays inside the provider's cached prompt prefix), and removable like any other chip.

Day over day, just click Restore Session again and select all the conversations including today's new one: already-covered files are skipped and only the new conversation is folded into the existing summary, preserving earlier decisions verbatim. The summary file is plain Markdown — open and hand-edit it if the distillation got something wrong (the next incremental update builds on your edits). The summary's size is capped by the Worker LLM's **Max tokens** setting. The original transcripts are never modified or deleted.

---

## Working with a repository

### Selecting a repo

Top toolbar → **Select Repo**. Codayak scans the directory tree (respecting `.codaignore`), builds a source-code map of every project and type, and injects that map into the system prompt on every send.

### The Working Folder indicator

The top toolbar opens with a **📁 Working Folder:** caption. It always shows where Codayak is working: when a repository is selected, that's the repo root (with project/file counts); when no repository is selected, it's the folder where generated files (documents, diagrams, images) are written — `MyDocuments/Codayak/Documents` — so you can always see where output will land.

### Recent repositories

The **📁 Working Folder:** caption doubles as the recent-repos picker — it shows a ▾ chevron and a hand cursor. **Click it** to drop down the last six core repositories you've connected, newest first, and pick one to reconnect without browsing for the folder. The list persists across restarts (stored in settings) and de-duplicates, so reselecting a repo moves it to the top rather than adding a duplicate. A remembered repo whose folder has since been moved or deleted is reported and pruned from the list. Only the active/core repo is tracked here — reference repos are not. (Before you've connected any repo, clicking the caption simply notes there's no history yet — use **Select Repo** to choose your first.)

### Write to Repo

The **Write to Repo** toggle (top toolbar) controls whether the LLM can modify files. When **off**, write-bearing tools (PatchFile, DeleteFile, MoveFile, RestoreBackup, dotnet scaffolding) aren't even advertised to the LLM. When **on**, they become available — and every write is preceded by an automatic backup to `.coda/backups/`.

### The source-code map

Codayak builds a structured map of your repo — projects, files, every public/internal type, every member, and the dependencies between them — so the LLM navigates by signature instead of reading every file.

**Tiered detail:**
- Small repos → full map (every member of every type).
- Large repos → automatic skeleton (types and namespaces only). The LLM calls `LoadTypeDetails(typeName)` when it needs full member signatures for a specific type. Threshold configurable in **Settings → Code Map → Source Code Map** (default: 80% of context window).
- Reference repos → always skeleton.

### Reference wikis

Click **📖 Add Ref Wiki** in the system prompt area to add an Azure DevOps or GitHub wiki as read-only reference context. The wiki's page tree (titles, paths, sections) is enumerated once — via the platform's REST API for Azure DevOps, or via a git clone of the wiki repository for GitHub (see [GitHub wiki behaviour](#github-wiki-behaviour)) — cached to disk, and injected into the system prompt — so the LLM knows what pages exist and can call `ADO_SearchWiki` / `ADO_GetWikiPage` or `GH_SearchWiki` / `GH_GetWikiPage` with accurate paths.

- If exactly one DevOps connection is configured, it's used automatically; if several are (across either platform), a picker lists them as `Platform — Connection name` so you choose which one's wiki to add.
- First load enumerates via the platform API; later sessions load instantly from the disk cache.
- The wiki appears in the system-prompt files list; remove it with the × button.
- If a wiki fails to load, an error dialog reports which wiki failed and why, the status bar shows a one-line summary of the reason, and nothing is added to the list.
- When combined reference content (code map + reference repos + wikis) exceeds the skeleton threshold, wiki maps degrade to a "search-only" view of the 25 most-recently-edited pages.
- Wiki references aren't persisted across restarts (re-adding is instant thanks to the cache). To refresh after pages change, remove and re-add.

**Requirements:** Azure DevOps needs Organisation, Project, and PAT set on a connection in Settings → DevOps; GitHub needs Repository (`owner/repo`) and PAT. Every fully-configured connection is offered in the picker — not just the active one.

### `.codaignore`

A file at the repo root, identical in syntax to `.gitignore`. Anything matched is excluded from source-map scanning and codebase searches. Codayak auto-adds generated artefacts (Mermaid HTML, Word docs, images) so they don't pollute future scans.

### Diff view

When a tool modifies an existing file, a **Show Diff** button appears in the chat. Clicking it opens a dedicated **side-by-side diff window** (backups under `.coda/backups/` are the "before"). Brand-new file creations don't get a diff button — there's no prior version to compare.

File-path links on write-bearing tool-activity lines (including the `Trust verdict: … — report: …` line) follow the same rule, decided at click time: a file that was **modified** this session (a backup exists) opens in the diff window; a **newly created** file — a verification report, a `Document created` / `Wrote` / `Saved` target, a copy or move destination — opens with its system default application instead.

The diff window is its own resizable, non-modal window — keep chatting while you review. Features:

- **Side-by-side panes** — original on the left (deletions red), modified on the right (additions green), line-aligned with padding rows.
- **AvalonEdit editors** — line numbers, monospaced font, text selection.
- **Synchronised scrolling** — always on.
- **Next / Previous change** — toolbar buttons or hotkeys (default `F8` / `Shift+F8`, configurable). Opens scrolled to the first change.
- **Ignore-whitespace toggle** — when on, indentation/trailing-whitespace edits within a line aren't flagged; blank-line add/delete still shows. Persists across sessions.
- **Change-overview minimap** — one tick per changed row; click to jump.
- **Title-bar summary** — `N additions, M deletions` with the file path.
- **Window position remembered**; **one window per file** (re-clicking focuses the existing window); **Escape closes**.

### Backups

Every write tool backs up the target first, to `.coda/backups/{yyyyMMdd_HHmmss_NNNNNN}/{relative-path}/{file}`. Retention is configurable (default 7 days). Use the `ListBackups` / `RestoreBackup` tools or the **Backups** browser in the Repo section to restore.

---

## Tools

**Settings → Tools** lists every tool Codayak can offer the LLM, with a checkbox for each. Disabled tools are removed from the model's context to save tokens. Tools that need a repository (or Write to Repo) show a small warning chip and stay invisible to the LLM until that condition is met.

All up, Codayak exposes around 50 tools — over 80 callable endpoints when everything is enabled, counting the Azure DevOps and GitHub families and the conditional tools (Team Mode peer delegation, LoadSkill) that register only when their feature is active. The full list is at the end of this section.

### How tools are gated

- **Always available** — web search, Mermaid, image generation, Word documents, document creation, search-documents (SearchDocuments + RequestDocuments — these search/read across the whole repo including `.coda/Logs/`, but never require Write to Repo since they're read-only).
- **Source-readable (read-only)** — RequestSourceFiles, ReadFileSection (read a bounded section of a large file), SearchCodebase, ListDirectory (enumerate a folder's contents): available whenever an active repo **or any reference repo / reference directory** is attached — they reach reference roots via a `[Name]` path prefix, so an active repo is not required. LoadTypeDetails, the **Build & Test** group (BuildProject, RunTests, RunProject), ListBackups, and VerifyCodeQuality genuinely require an active repo.
- **Repo-required + Write to Repo (working repo only)** — the **Patch & Scaffold** group (PatchFile, CreateTestProject, AddProjectToSolution, RunDotNetCommand, CreateDirectory, plus the additive CopyFile / CopyDirectory), plus DeleteFile / MoveFile / DeleteDirectory / MoveDirectory and RestoreBackup. All mutation is bounded to the *working* repo — reference repos and reference directories are read-only and can never be modified.
- **Database execution (no repo required)** — **ExecuteSql** runs a SQL command against a relational database. It needs no repo and no configuration (the model supplies the connection string per call), so it's gated only on the **Database Execution** toggle. Its safety gate is a per-request human consent keyed on *initiative*, not a repo/write gate — see [Database execution](#database-execution).

> **Toggle grouping:** **Build & Test** covers read-only .NET execution (needs a repo but not write access); **Patch & Scaffold** covers write-bearing project mutation (needs Write to Repo). The **Delete / Move File & Directory** toggle covers all four destructive operations — DeleteFile, MoveFile, DeleteDirectory, MoveDirectory — since they share the same safety semantics (always back up first, working-repo-bounded, refuse `.coda/`). **ListDirectory** rides on **Repository Tools** (read-only, like RequestSourceFiles/SearchCodebase), and **CreateDirectory** rides on **Patch & Scaffold** (write-bearing, like the other project-mutation tools). The additive **CopyFile / CopyDirectory** tools also ride on **Patch & Scaffold** rather than the Delete/Move toggle, since a copy is a non-destructive write (it leaves the source in place) — grouping them with the create-family tools.

### Tools managed outside the Tools list

A few tools have their own gates, called out at the bottom of the Tools tab with links to where they're configured:

- **SearchLearningMemory** and **CreateLearningMemory** — gated by **Settings → Memory → Enable Learning Memory**.
- **LoadWorkingSet** — always available whenever a repository is loaded; no toggle. Configured on **Settings → Code Map**.
- **LoadSkill** — registered only while at least one enabled skill exists; managed on **Settings → Skills**.
- **LoadTypeDetails** — gated by the *Repository Tools* toggle (the same one that gates RequestSourceFiles and SearchCodebase) plus a loaded repo; the skeleton-vs-full threshold is on **Settings → Code Map**.
- **VerifyOutput (Trust Engine)** — always available to call manually; how eagerly the model self-elects to use it is set on **Settings → Trust Engine**.
- **ADO_*** / **GH_*** — managed via the master **DevOps** toggle; per-platform credentials on **Settings → DevOps**. A blank credential silently disables that platform without affecting the other.

### The full tool list

| Tool | Purpose |
|---|---|
| RequestSourceFiles | Load full file contents from the repo |
| ReadFileSection | Read a BOUNDED SECTION of a source file instead of the whole thing — for large files where loading it all would truncate before the part you need (or waste context). Two modes: `searchText` returns ~40 lines before the first match through to EOF (capped); or `startLine`/`endLine` for an exact 1-based inclusive range. Output is line-numbered. Same reach as RequestSourceFiles (active repo + reference repos/directories via `[Name]`). SOURCE files only — use RequestDocuments for non-source files. Read-only; refuses `.coda/`. |
| SearchCodebase | Grep-style search across repo source files. Case-insensitive **plain-substring** matching by default, or full **.NET regex** with `useRegex=true` (e.g. `Task<\w+>\s+\w+Async`, `TODO\|HACK\|FIXME`). Returns each match with surrounding context (`contextLines`, default 1, max 10); pass `matchesOnly=true` for just the file list with per-file match counts (cheaper when scoping a refactor). Searches the active repo plus any reference repos/directories; skips generated artefacts (use SearchDocuments for those). Read-only; refuses `.coda/`. |
| LoadTypeDetails | Fetch full member detail for a type (skeleton-map companion) |
| ListDirectory | List the files and sub-directories inside a folder — the structural counterpart to SearchCodebase (content) and the source-code map (types). Sees non-source files and `.codaignore`'d artefacts the map omits. Works on the active repo, reference repos, or reference directories (prefix the path with `[Name]`). Non-recursive by default; `recursive=true` for a depth-bounded tree. Read-only; refuses `.coda/`. |
| PatchFile | Surgical find/replace, line-range or marker-based edits — every patch auto-backs-up the original |
| CreateDocument | Create any text file. With Write-to-Repo on, writes into the repo at the supplied `subPath`; otherwise into the session output folder |
| DeleteFile | Remove a file (with auto-backup) |
| MoveFile | Move or rename a file in one call (creates the destination directory; auto-backs-up source, and destination too when overwrite is true) |
| CopyFile | Copy a file to a new location, producing a byte-identical duplicate — the original is left in place. Creates the destination directory as needed; refuses `.coda/`, outside-the-repo, directories, and an existing destination unless `overwrite=true` (which backs up the existing destination first). Duplicating a `.cs` file copies its type declarations verbatim, so the copy needs its type/namespace renamed before it will compile. |
| CreateDirectory | Create an empty directory (parent directories created as needed). For a genuinely empty folder only — CreateDocument and MoveFile already create a file's parent folders automatically. Refuses `.coda/` and outside-the-repo; creating an existing directory is a harmless no-op. |
| MoveDirectory | Move OR rename a whole directory in one call. Backs up every file in the subtree first; creates the destination's parents; refuses the repo root, `.coda/`, moving a folder into its own descendant, an existing non-empty destination, and trees over 1000 files. |
| CopyDirectory | Copy a directory and all its contents to a new location, producing a byte-identical copy of the whole subtree — the original is left untouched. Creates the destination's parents; refuses the repo root, `.coda/`, a file path, copying a folder into its own descendant, an existing non-empty destination, and trees over 1000 files. |
| DeleteDirectory | Delete a directory and all its contents. Backs up every file in the subtree to `.coda/backups/` first (recoverable via ListBackups + RestoreBackup). Refuses the repo root, `.coda/`, a file path, and trees over 1000 files. |
| BuildProject | Run `dotnet build`, return errors + warnings |
| RunTests | Run `dotnet test`, return pass/fail + failure details |
| RunProject | Execute a .NET console app, capture stdout/stderr |
| CreateTestProject | Scaffold xunit/nunit/mstest project + project reference |
| AddProjectToSolution | Add an existing .csproj to a .sln |
| RunDotNetCommand | Arbitrary `dotnet` CLI command |
| ExecuteSql | Run a SQL command against SQL Server, PostgreSQL, MySQL/MariaDB, SQLite, or Oracle (bundled ADO.NET drivers). Needs no repo — the model supplies the engine + connection string per call. Human-consent gated by initiative (see [Database execution](#database-execution)); results return as JSON (row-capped) or rows-affected, and any database error is returned verbatim. |
| ListBackups | Browse `.coda/backups` |
| RestoreBackup | Restore a file from backup — the preferred way to undo a recent mutation (byte-identical, no patch drift) |
| VerifyCodeQuality | Build + test + security scan + spec compliance, with confidence score (lower-level entry point used inside the Trust Engine) |
| VerifyOutput | **Codayak Trust Engine** — runs every applicable checker against an artifact and returns a calibrated confidence score, evidence, recommendations. See [Trust Engine](#trust-engine-verification). |
| SearchInternet | Google Custom Search + real-Chrome page fetch |
| SearchDocuments | Search NON-SOURCE files across the whole repo — generated artefacts, stray docs/READMEs, and Codayak's own `.coda/Logs/` (excludes `.coda/backups`). Complements SearchCodebase, which refuses `.coda/`. |
| RequestDocuments | Read the full text — or a bounded SECTION — of a specific non-source file by path, including under `.coda/` (e.g. `.coda/Logs/debug.log`) and inside reference repos/directories via `[Name]`. For a large file, pass `searchText` (≈40 lines before the first match through to EOF, capped) or `startLine`/`endLine` to read a slice instead of the whole thing. The read-counterpart to SearchDocuments and the `.coda/`-capable complement to RequestSourceFiles. |
| RenderMermaidDiagram | Generate Mermaid charts as HTML |
| GenerateImage | Multi-provider image generation — OpenAI, Stability AI, xAI, Google; supports reference-image editing (OpenAI/Stability) |
| GenerateVideo | Text-to-video generation — saved as `.mp4` (see [Image generation](#image-generation)) |
| AnalyseVideo | Watch a video file and return a timestamped written description to reason about (runs on Google Gemini regardless of the chat model) |
| CreateWordDocument | .docx with headings, tables, embedded images; can base the output on an attached `.dotx`/`.docx` template (inherits its styles, headers/footers, and page setup) |
| ADO_* | Azure DevOps work items, wiki, pull requests |
| GH_* | GitHub issues, wiki, pull requests |
| ExecuteMultiFileTask | Coordinator for 6+ file generation tasks (see [The Coordinator](#the-coordinator-multi-file-builds)) |
| LoadTaskManifest / ResumeTask | Resume an interrupted Coordinator build |
| SearchLearningMemory | Search persistent memory for relevant past lessons |
| CreateLearningMemory | LLM-initiated memory creation when it discovers a durable lesson (strict gating; shares the dedup/budget/evolution machinery with user- and system-created memories) |
| LoadWorkingSet | Dependency-aware file bundle for cross-cutting work — embedding-matched seeds expanded along the dependency graph, each file annotated with why it was included (see [Repository intelligence](#repository-intelligence)) |
| ReadHelpDoc | Read Codayak's own README, user guide or EULA, so the assistant can answer "how do I…" (and licence) questions about Codayak itself |
| DeliberateResearch | Fan a research panel of worker LLMs out over one question (see [Research panel](#research-panel)) |
| BrowserOpen / BrowserSnapshot / BrowserClick / BrowserType / BrowserWait / BrowserClose | Drive a real Chrome session to TEST a web UI interactively — open the site, snapshot its elements, click and type through flows, verify the result. Credentials pass as registered-secret placeholders, never plain text. Gated by **Settings → Tools → Browser UI Testing**. |
| DesktopAttach / DesktopSnapshot / DesktopClick / DesktopType / DesktopClose | The desktop counterpart: attach to a running Windows app (WPF/WinForms/Win32) via UI Automation — or launch one — then snapshot, click, and type to test it. Gated by **Settings → Tools → Desktop UI Testing**. |
| LoadSkill | Load a skill's full body on demand (conditional — registered only while at least one enabled skill exists; see [Skills](#skills)) |
| ListTeamPeers / DelegateTaskToPeer / GetPeerTaskResult / CancelPeerTask | Team Mode delegation tools (conditional — registered while leading a session with ≥1 connected peer; see [Team Mode](#team-mode)) |
| AskLeader | Peer-side: ask the session leader a blocking question mid-task (conditional — available to a specialist during a delegated task; see [Team Mode](#team-mode)) |

---

## The Coordinator (multi-file builds)

For a build of roughly **six or more new files** (the `ExecuteMultiFileTask` tool), Codayak stops writing files one at a time and runs the Coordinator instead.

- **It plans first** — a file manifest (name, type, path, purpose, dependencies) before any code is written.
- **It generates in dependency order** across independent worker sessions, so each file is written knowing the signatures of the ones it depends on. Workers run on the [Worker LLM](#worker-llm) with their own bounded tool loop (see **Worker max tool-call rounds** under [Tools](#tools)).
- **It retries failures** instead of leaving a hole in the build.
- **It can verify each phase** — tick **Settings → Trust Engine → Verify Coordinator phases automatically** and the [Trust Engine](#trust-engine-verification) runs over each phase's output as it finishes.
- **Large builds split into sequential phases**, with a cumulative manifest at `{repo}/.coda/task_manifest.json` — per-phase confidence, band and summary, open issues, and a recovery audit trail (see [Repository intelligence](#repository-intelligence)).
- **An interrupted build resumes** — `LoadTaskManifest` reads the manifest and `ResumeTask` retries failed and pending files, leaving finished ones alone.
- **Where the files land** — straight into the repository when **Write to Repo** is on (backed up and diffable like any other write); otherwise into a timestamped session folder under `MyDocuments/Codayak/Documents/`, so a large build works without a repo loaded.

---

## Learning memory

Codayak's memory system is the closest thing to genuine cross-session learning in an AI coding tool. Enable it in **Settings → Memory → Enable Learning Memory**.

### Three ways to add a memory

- **Just type it in chat.** Send a message starting with *"remember this"*, *"please remember that…"*, *"add this as a learning"*, *"make a note that…"*, *"keep that in mind"*, *"that's worth remembering"*, or *"save to memory"*. Codayak detects the intent, distils your text into a structured memory, saves it, and confirms with the title and resolution. The match is conservative (false positives are worse than misses here), so be explicit.
- **Settings → Memory → Create memory from description.** The free-text box is the deliberate path for composing a longer memory at leisure.
- **Wait for Codayak to notice.** Repeated tool failures or successive build errors trigger reflection automatically.

### How it works

1. **Capture** via the three paths above — all feed one persistence pipeline.
2. **Embed** with the local BGE-small-en-v1.5 ONNX model. No memory text leaves your machine.
3. **De-duplicate** — hybrid search finds near-duplicates; strong matches merge into the existing row, weak ones are handled by the evolution pass.
4. **Retrieve** — before every send, hybrid retrieval (vector + lexical FTS) with reciprocal-rank fusion and confidence weighting; top matches above the relevance threshold are injected as a `<learned_lessons>` block.
5. **Evolve** — a new memory similar to existing ones triggers an async merge/supersede/link pass via the worker LLM.
6. **Track outcomes** — after each exchange, every injected memory's `Used` count ticks up (it was shown — attention only). `Validated` accrues **only when the model itself cites the lesson as applied** — the injected block asks it to mark each lesson that materially shaped its answer, and Codayak reads (and strips) those markers invisibly; a cited lesson on a failed turn gets `Contradicted` instead. Confidence is Laplace-smoothed from the validated/contradicted counters, so a memory that is merely shown a lot no longer inflates its own confidence.
7. **Retire** — a memory whose `Last Seen` is older than the retention window is archived regardless of its counters, and the Memory tab's **Flagged** view surfaces "shown often, never applied" memories (10+ uses, zero validations) for your review.

### Memory tab — what you can do

- **Browse memories** in a searchable grid. The Score column shows the hybrid-search FinalScore for the last query (or `—` for rows loaded via Refresh / Top Used / Flagged / Recent). The grid search uses the same scoring and threshold as proactive injection, so you can predict what the LLM will actually see — the only extra filter injection applies is a scope veto for memories pinned to context that actively contradicts the current session (e.g. a different provider).
- **Search** — hybrid vector + lexical across all memories; results above the configured min-score, ordered by relevance.
- **Create memory from description** — plain-English box, distilled into a structured memory.
- **Manual edits** — edit any memory's title, problem, symptom, resolution, tags. Confidence, counters, and timestamps stay system-managed.
- **Export** — save to JSON. You're asked whether to include sensitive context (filesystem paths, session GUIDs, links); the safe default scrubs them. Embeddings are always stripped (regenerated on import).
- **Import** — merge a file from another machine. Duplicates merge by semantic similarity; counters reset to zero so each user's confidence reflects their own validation.
- **Self-test** — runs the embedder + repository + retrieval + injection pipeline end-to-end and reports per-step health.

### Tuning

| Setting | What it controls |
|---|---|
| Failure repeat threshold | Same-fingerprint failures before reflection fires |
| Build error repeat threshold | Same, for build failures |
| Max memories per session | Anti-spam cap (also enforced for LLM-initiated creation) |
| Proactive top-K | How many memories inject per turn (default 5 — the injector's own filters below usually trim this to 2-3 in the final prompt) |
| Proactive min score | Relevance floor (0.0–1.0 normalised, default 0.55; the injector adds its own hard floor of 0.45, a max-one-Situational-per-turn cap, and resolution de-duplication) |
| DB size cap (MB) | Maximum SQLite database file size before archival/pruning is forced (default 500) |
| Retention (days) | Days after which low-confidence, unused memories become eligible for archival (default 365) |
| Utility boost | `(times_used × confidence) × recency` multiplier so proven, recently-used memories outrank zero-usage peers at the same tier (bounded, normalised so scores still top out at 1.0; disabled for dedup/import) |
| Recency decay | ~62-day half-life; a memory unseen for months loses most of its boost |
| Auto-evolve | Whether the async A-MEM-style **merge / supersede / link** pass runs (via the Worker LLM) after each new memory is inserted, reconciling it against existing similar memories. On by default. Unticking still saves new memories — they just aren't reconciled. |
| Embedding model URLs (advanced) | Override the HuggingFace download URLs to mirror the model internally. *These overrides — and the model's **Download Now** button and status — live on **Settings → General → Embedding Model**, since the embedder is a shared dependency, not memory-specific.* |

### Confirming a memory will be used

1. Open the Memory tab.
2. Type something semantically related into **Search**. The Score column shows the same fused score the proactive injector uses; results above min-score get injected in chat (unless a memory's scope actively contradicts the session — e.g. it is pinned to a different provider).
3. Or chat about the topic, then refresh and check whether `Used` ticked up.
4. If scores are lower than expected, drop **Proactive min score** (toward ~0.30 to inject more); if you get false positives, raise it toward 0.65.

---

## Trust Engine (verification)

<img src="docs/images/trust-engine.png" alt="" align="right" width="130">

The Trust Engine is Codayak's verification layer — it runs after generation and before you rely on the result, returning a calibrated confidence score and a persisted report.

### Defaults

There is no master on/off switch — the `VerifyOutput` tool is **always registered**, so asking Codayak to "verify this" or "check this against the spec" always works. What IS off by default is *unprompted self-election*: the **Self-verify** dial starts at **User Prompted**, meaning the model never reaches for the tool on its own initiative until you raise the dial. Hard per-verification and per-session token budgets prevent runaway spend regardless of the dial.

### Tuning it

Defaults are conservative — **Light** depth, **8,000** tokens per verification, **32,000** per session, **self-correction off**. Raise **Settings → Trust Engine → Self-verify** to Conservative/Standard/Pedantic if you want Codayak to check its own work without being asked; leave the token budgets and depth alone for the first few days, then tune from real usage.

### Depth tiers

| Tier | What runs | Typical cost |
|---|---|---|
| **Light** *(default)* | Code: build + tests + security scan + spec compliance. Any artifact: memory-grounded contradiction check. | Under 4,000 tokens |
| **Balanced** | Light, plus a self-consistency variant-generation step. | 6,000–10,000 tokens |
| **Deep** | Balanced, plus a capped self-correction loop and a second LLM-as-judge pass. Requires *Auto self-correct* enabled. | 12,000–25,000 tokens |

The engine refuses a verification that would exceed your per-verification cap, and refuses to start another once the session cap is consumed. **Reset Session** in chat resets the running total.

### Trust bands

- **High** (≥ 85% confidence) — safe to ship.
- **Moderate** (60–84%) — usable, but read the evidence.
- **Low** (< 60%) — needs your attention.

### Invoking verification

- **The LLM calls it** — when enabled, the `VerifyOutput` tool is registered; the model invokes it after significant work ("verify the changes", "check this against the spec"). How eagerly it self-elects is set by the **Self-verify** dial (User Prompted → Conservative → Standard → Pedantic). You can always ask for verification regardless of the dial.
- **At the end of a Coordinator phase** — enable *Verify Coordinator phases automatically*.
- **The lower-level `VerifyCodeQuality` tool** still works as the code-only pipeline; the Trust Engine reuses it internally.

### Checkers

- **Code checker** — delegates to `CodeQualityService` (build, tests, security scan, spec compliance). Applies to Code artifacts in a loaded repo.
- **Memory-grounded checker** — probes the learning store for lessons that contradict the artifact. Cheap (one embedding + one query), so it runs for every artifact kind when Learning Memory is enabled; matched lessons surface as advisory evidence and downgrade the result to Warning so you read them.
- **Plan checker** — activates for Plan artifacts or Deep depth; cross-checks a proposed file list against the working set and dependency graph (see [Repository intelligence](#repository-intelligence)). Deterministic and token-free.

More checkers are pluggable via `IVerificationChecker` — a single-line DI registration.

### Reports

With *Log verification reports* on (default), every report is written to `{repo}/.coda/verification/{yyyyMMdd_HHmmss}_{label}.txt` — plain text, diffable, grep-able, PR-attachable. Each includes the verdict and trust band, per-checker status and confidence, up to 40 lines of evidence per checker, recommendations, token spend, and the report's own file path (also quoted in the chat note after an automatic post-build verification, so you can open the full report directly).

### Which depth, when

- **Light** — every-turn assurance during normal development. Cheap, fast, deterministic.
- **Balanced** — before sharing work, before merging a PR, after a multi-file refactor.
- **Deep** — high-stakes deliverables, end-of-phase verification. Costly; don't use for routine work.

### Settings reference

| Setting | Default | Purpose |
|---|---|---|
| Self-verify | User Prompted | How eagerly the model self-elects (manual verify works at every setting; there is no master on/off — the tool is always registered). |
| Default depth | Light | Used when a call doesn't specify one. |
| Max tokens per verification | 8,000 | Hard cap per call. |
| Max tokens per session | 32,000 | Soft cap across calls until Reset Session. |
| Timeout (seconds) | 300 | Wall-clock ceiling per verification run; 0 disables the limit. |
| Auto self-correct | Off | Permits one corrective generation pass (Deep). |
| Max self-correction iterations | 1 (clamped to [0, 2]) | Hard upper bound. |
| Show token estimate before run | On | Surface projected cost so you can cancel. |
| Log verification reports | On | Persist to `.coda/verification/`. |
| Verify Coordinator phases automatically | Off | Hook verification into the post-phase pass. |

---

## Repository intelligence

A dedicated **Settings → Code Map** tab for everything that affects how Codayak *understands* the active repo. The source-code-map skeleton threshold sits at the top because it's the foundation. Below it is opt-in machinery for problems the Trust Engine doesn't cover: **dependency-aware working-set retrieval**, **resilient tool dispatch**, and **persisted Coordinator project state**.

### Defaults

The master toggle defaults to **off**. With it off, the working-set selector still works when called (single-stage embedding fallback), the dispatch pipeline still validates arguments but skips the circuit breaker, and Coordinator projects hold state in memory only. The source-code-map threshold at the top always applies whenever a repo is loaded, regardless of this toggle.

### What you get when you turn it on

**Working-set retrieval** (`LoadWorkingSet` tool) — the LLM calls it with a free-form intent (e.g. *"rename `IFooService` to `IFooClient` and update every implementer"*) and gets an ordered file list: embedding-matched seeds, their direct dependencies (one hop through the source-map dependency graph), optionally further transitive deps if `maxDepth` > 1, each annotated with why it was included. Cross-cutting refactors land coherent slices instead of file-by-file guessing.

**Resilient tool dispatch** — every tool call is wrapped:
- **Argument validation** against the tool's own schema — required params present, types coerced, enums honoured. Malformed calls return a structured error in < 100 ms with no method invocation. Always on (it's free).
- **Single-attempt execution** — each tool runs exactly once; failures flow back to the LLM as one clean result tagged `[Transient]` or `[NonTransient]` so the model owns the recovery decision (Codayak doesn't silently retry).
- **Per-tool circuit breaker** — opens after N consecutive failures, rejects subsequent calls within a cooldown. One tool's failures never starve another. Default threshold 3.
- **Structured audit lines** in `%LOCALAPPDATA%\Coda\logs\app.log` under source `ToolDispatchPipeline`.

**Persisted Coordinator project state** — a multi-file build maintains a `ProjectManifest` at `.coda/task_manifest.json`: current working set, per-phase verification confidence/band/summary, open issues, and a recovery-attempt audit trail with a running token total. Capped (oldest/resolved entries evicted first) so it doesn't grow without bound.

**PlanChecker** (a Trust Engine checker) — activates for Plan artifacts or Deep depth. Cross-checks a proposed file list against the working set and dependency graph, flagging **orphans** (file off-target), **missing dependencies** (a depended-on file not in the plan), and **cycle suspicion**. Deterministic, zero tokens.

### Settings reference

| Setting | Default | Purpose |
|---|---|---|
| Source-code-map skeleton threshold (%) | 80 | When the full map exceeds this fraction of the model's context window, switch to skeleton + `LoadTypeDetails`. Always applies. |
| Enable dependency-aware retrieval, dispatch breaker, project state (master toggle) | **Off** | Off ⇒ single-stage selector, no breaker, in-memory project state. |
| Enable dependency-graph expansion | On | Kill-switch for the expansion stage (A/B testing). |
| Max working-set files | 40 | Hard cap per `LoadWorkingSet` call (runtime ceiling 200). |
| Max working-set depth | 1 | Dependency hops. 0 = seeds only, 1 = direct deps, 2 = transitive. Runtime ceiling 3. |
| Circuit breaker failure threshold | 3 | Consecutive failures before a tool's breaker opens. |
| Circuit breaker cooldown (s) | 300 | How long an open breaker stays open before a half-open probe. |
| Mission token budget | 200,000 | Cap on recovery-driven token spend per Coordinator project. |
| Persist project state | On | When off, project state is in-memory only. |

### When to use it

- **Leave it off** until you feel pain on cross-cutting refactors or repeated tool failures — the Trust Engine is the higher-leverage feature.
- **Turn it on** when the LLM has wandered file-by-file through your repo, or a tool has failed repeatedly without the model changing tack.
- **Lower Max files to 20** if prompts feel context-bloated; set **Max depth to 0** to disable expansion while keeping the embedding-seeded selector.
- **Raise the breaker threshold** if you're working against a flaky external tool.

### Audit log

- **Dispatch events:** `%LOCALAPPDATA%\Coda\logs\app.log`, filtered by source `ToolDispatchPipeline`.
- **Project state:** `{repo}/.coda/task_manifest.json`.
- **Working-set selections** aren't persisted; the reasoning is in each entry's inclusion-reasons.

---

## Team Mode

Team Mode turns other Codayak instances — on the same machine or across a LAN — into **tools of your main chat LLM**. One Codayak acts as the **Leader** (its repository is the authoritative one); every Codayak that joins registers as a **peer** the leader's chat model can see and delegate work to, exactly like any other tool.

Each Codayak uses its **own** LLM provider on its **own** API key on its **own** bill — Claude on one, GPT on another, Gemini on a third — and keeps its **own system prompt and tool configuration**. That's the point: set one instance up as a QA specialist and another as a senior developer, and the leader's chat model can farm each kind of work to the right peer. There's no central server, no shared key, no cross-billing.

It's also the natural fit for **multi-repo work**: the leader develops in the main application's repository while a peer is loaded with a repository the application depends on — say, the API project the main app connects to. The leader's chat model delegates the server-side change to that peer (which works in the API repo with its own source-code map, building and testing there) while it implements the client side in the main repo — both halves of the feature land in their own repositories from one conversation.

### Peers as tools — how it operates

While you lead a session with at least one connected peer, four tools are registered to your chat LLM automatically (they disappear when the last peer leaves):

| Tool | What it does |
|---|---|
| **ListTeamPeers** | The roster: each peer's call-sign, **declared specialty**, LLM provider/model, context window, max output tokens, enabled tools, loaded repo (and whether it may write it), machine name, and whether it is idle or busy. |
| **DelegateTaskToPeer** | Farm a task out. **Asynchronous** — returns a task id immediately, so the chat model keeps working (or delegates to several peers at once). An optional role system prompt puts the peer's LLM into the right persona for the task. Each peer works one task at a time. |
| **GetPeerTaskResult** | Collect a delegated task's status or full result (blank task id lists all delegated tasks). |
| **CancelPeerTask** | Abandon a delegated task in flight; the peer stays connected. |

The connected-peer count shows as **👥 N peers**, right-justified on the model settings bar, while you lead a session with peers.

**The leader's repo is the authority.** How a peer's file work lands depends on its own setup:

- **Same machine, same repo, peer's Write-to-Repo ON** — the peer edits the shared working tree directly with its own tools; its deliverable carries the changed-file list, and the leader rescans its source-code map automatically so your next chat turn sees the changes.
- **Peer has a repo but its Write-to-Repo is OFF** — the peer reads its repo locally, but every file write it makes (PatchFile / CreateDocument) is sent to the **leader** and applied to the leader's repo — gated by the *leader's* Write-to-Repo switch.
- **Peer has no repo** — it gets a compact leader-proxied tool set (read source/search/list, patch, create, build, test) whose calls travel the encrypted session channel and execute against the leader's repo, writes again gated by the leader's Write-to-Repo.

A delegated task runs a **bounded tool loop** on the peer — reading code, patching files, building, and testing like any Codayak session — not a single text-only completion. The peer sees ONLY the instructions in the delegation (none of your conversation), so the chat model is told to make them self-contained.

### Peer specialties

Every peer advertises a one-line **specialty** when it connects, so the leader knows *what kind* of specialist each peer is:

- **Automatic by default** — the specialty is derived from the peer's own system prompt (its identity sentence, e.g. *"You are a senior QA engineer…"*, or its heading). Only that one condensed line is sent — never the full system prompt.
- **Editable** — the **My specialty** field on the peer's own Team Mode page (visible when no session is active) overrides the auto-detected value; the auto-detected text shows as a hint beneath the field until you type your own. Changes take effect the next time the peer connects.
- **Where it shows** — the leader sees it in `ListTeamPeers`, in the Team pane's peer row, and in autonomous-mode planning, where the leader's LLM is told to *prefer* matching tasks to specialties (it's advisory — a peer is never refused out-of-specialty work).

### Mid-task questions — the AskLeader relay

A specialist that hits a **genuine blocker** mid-task — a missing requirement, contradictory instructions, or a decision only the task issuer can make — no longer has to guess. During a delegated task its LLM gets an **AskLeader** tool:

1. The question travels to the leader, appears in the leader's activity feed, and the leader's own LLM attempts an answer **from the session goal and task context only** (it is instructed never to invent requirements or credentials).
2. If the question genuinely needs a human — credentials, business decisions, out-of-scope changes — the leader escalates it visibly in chat (*"❓ Specialist question needs you: …"*) and immediately tells the specialist to proceed on its best judgement and record the open question in its deliverable.
3. The specialist **never hangs**: at most 2 questions per task, and an unanswered question times out after 5 minutes with the same proceed-on-best-judgement instruction.

Questions are for genuine ambiguity only — the tool description forbids using it for anything discoverable from the repo or for progress reports.

### Quick start

**As Leader:**
1. Click 🤝 **Team Mode** in the activity bar.
2. Optionally type a short description shown to joining peers (no goal is required — you direct the work from the chat window).
3. Click **Start Session**. Codayak generates an invite code in a copyable box. (The **Port** field beside the button sets the TCP port the session listens on — default 41833 — and is saved as your new default when the session starts; joining peers need nothing, the port travels in the invite code.)
4. Share the invite code with whoever will be a peer.
5. As peers join, they appear in the **Team** pane — each with a call-sign (Specialist-1, Specialist-2…), machine name, the LLM vendor/model they're running, and their declared specialty — and the toolbar shows **👥 N peers**. The session activates itself; there is nothing further to click.
6. Go back to **Chat** and work normally. Your chat LLM now has the ListTeamPeers / DelegateTaskToPeer / GetPeerTaskResult / CancelPeerTask tools — ask it to check what peers can do and to farm work out (e.g. "delegate fixing defect D-012 to the dev peer while we keep testing"). Delegated-task deliverables also appear in the Team page's **Output** pane, rendered as markdown.
7. **✖ Cancel Task** interrupts in-flight work without ending the session; **＋ New Task** (top-right) hands the whole team an autonomous goal (see below); **⏹ Stop** ends the session cleanly.

**As Specialist:**
1. Get an invite code from a Leader.
2. Click 🤝 **Team Mode** → paste the code → **Join Session**.
3. Your Codayak dials the Leader, completes the handshake, and waits. Your header shows your **call-sign** (matching the Leader's Team pane), the goal, and whose session you're in.
4. When a task arrives, the header badge shows the **role** the Leader gave you for it (with a breadcrumb of roles played), and the **Activity** feed logs what your local LLM is doing — task received, model running, streaming progress, deliverable sent.
5. Your token usage shows on the main-window context meter, the same as in chat.

### Autonomous mode — give the team a whole job

The classic autonomous flow is still available: click **＋ New Task**, enter a goal, and set the **Revisions** limit (how many times review findings may be sent back to an author). The Leader's own LLM then takes over:

1. **Plan** — it decomposes the goal into tasks, each with an assignee, a role (e.g. Business Analyst, Developer, Reviewer), a role system prompt it authors, and optional dependencies between tasks. Each peer's **declared specialty** is shown to the planner, which prefers matching tasks to specialists (advisory only — no peer is barred from out-of-specialty work).
2. **Dependency-ordered waves** — independent tasks run in parallel; a task that depends on another waits for it and receives the finished work as context. A reviewer is therefore never dispatched alongside the work it is meant to review.
3. **Reviews with verdicts** — review tasks must end in `VERDICT: APPROVED` or `VERDICT: CHANGES REQUIRED`. (For a plan with no sequenced review of its own, the Leader adds an automatic cross-check wave where specialists review each other's work — never their own.)
4. **Revision loop** — a CHANGES REQUIRED verdict sends the work back to its original author with every finding attached; the revised work is re-reviewed. The **Revisions** dropdown caps how many rounds this can go (0 disables it); if the cap is hit with findings outstanding, they are flagged in the final result rather than hidden.
5. **Synthesis** — with all tasks in, the Leader reconciles the contributions into one final deliverable (a single contribution is promoted as-is, with no redundant rewrite).

A Specialist that fails (provider error, unreachable model) escalates to the Leader, its task is released, and the job advances with what the rest of the team produced — the session never hangs on one broken peer.

### Identity

Each Codayak has a stable Ed25519 keypair in `%APPDATA%/Coda/team-mode.key` — its identity across sessions, surviving restarts. The invite code embeds the Leader's public-key fingerprint so a Specialist can verify they're talking to the right Codayak. Every message is signed and authenticated; there's no way to spoof a peer without the matching private key.

Separately from the durable keypair, each running instance mints a **fresh session address (NodeId GUID) at startup** — so several Codayak instances on one machine (which share the keypair file) still appear to a Leader as distinct peers.

### LAN auto-discovery

Tick **Auto-advertise on LAN** in **Settings → Team Mode** and Codayak broadcasts the session via mDNS — other Codayaks on the same network see it in their discovery list, no invite code needed.

### Token accounting

Each Codayak pays for its own LLM calls on its own key. During team work, the **main-window context meter** (top-right) updates from your instance's own LLM calls — the last call's input tokens against the model's context window, exactly as in chat. Specialists also report token counts back to the Leader with each progress update.

### Security model

- Every message is Ed25519-signed, AES-256-GCM-encrypted with a session key derived via X25519 key exchange, and bound to the envelope via AEAD AAD (so a man-in-the-middle can't strip or swap the encrypted block).
- A peer can only reach the Leader's repository **through the Leader**: proxied tool calls execute on the Leader's machine, and every write-bearing one is refused outright while the Leader's **Write-to-Repo** is off. Reads are always allowed.
- A same-machine/same-repo peer edits the shared working tree only when **its own** user enabled Write-to-Repo on that instance — the same consent gate as local chat, on the machine where the writes happen. Every write is backed up to `.coda/backups/` as usual.
- The changed-file list a peer reports drives a repo-map rescan only; it grants no additional access.

### Limitations

- LAN / same-machine only. Cross-internet needs the Specialist to reach the Leader's IP directly. On the Leader's first LAN session, allow Codayak through the standard Windows Firewall prompt (private networks is sufficient) — no other setup is needed; Specialists connect outbound and need nothing.
- Specialist-side auto-accept (no Accept/Decline prompt for invitations yet).
- Reconnect after a transport drop is manual (re-paste the invite code).
- Token counts are shown, but per-model USD pricing is not computed.
- Upgrading from an older Codayak: if a leader session fails with a port-reserved warning, change the Port on the Team Mode page or restart Windows once.

---

## Image generation

The **GenerateImage** tool produces images via:
- **OpenAI** — the gpt-image family (fetched live via the model catalogue).
- **Stability AI** — Core, Ultra, SD3, SDXL.
- **xAI (Grok Imagine)** — generates new images; cannot edit an existing one.
- **Google (Imagen)** — generates new images; cannot edit an existing one.

### Let the Agent Choose (the default)

Both the **provider** and each provider's **model** default to **Let the Agent Choose**, meaning the assistant chooses per request from the providers you have keys for — including picking an **edit-capable** model when you ask for an existing image to be changed. The GenerateImage/GenerateVideo tool descriptions carry a live, key-verified list of the available providers and models, so the agent chooses from real options. Pick a specific provider or model to **pin** it; a pin always overrides the assistant's choice.

The Visual Models tab keeps **provider selection and model selection separate**: the **Default Provider** section at the top holds the **Image Provider** and **Video Provider** dropdowns (key-filtered — only providers with a usable key are listed; the image list offers the dedicated services plus one generic **LLM Provider** entry), and the sections below it carry the **model** choices — Stability AI (own key/model/style) and **LLM Provider Models** (an Image Model and a Video Model dropdown, populated from the catalogue by Fetch Latest, listed as 'Provider: model-id'). 'Let the Agent Choose' operates at both levels. LLM-provider models use their provider's key from the **LLM Providers** tab — Stability, a dedicated image service, is the only key field on this tab.

### Video generation

Ask for a video in chat and the assistant calls `GenerateVideo`; generation takes roughly 30–90 seconds and the result is saved as an `.mp4`. The **LLM Provider Models → Video Model** dropdown lists the catalogue's video models by provider (`xAI: grok-imagine-video-1.5`, key-filtered); video uses the provider's key from the **LLM Providers** tab. Limitations: **text-to-video only** — no provider currently offers video editing or animating a supplied image, and the tool says so plainly rather than substituting something else. xAI (Grok Imagine) is the only wired video endpoint today.

Stability AI has its own API key on the Visual Models tab; OpenAI, xAI, and Google visual models reuse their provider's key from **Settings → LLM Providers**.

### Image-to-image

Pass `referenceImageName` with the filename of an attached image (or any image in the repo). The output is guided by the reference's composition while applying the prompt's changes.

- **`strength`** (Stability only) controls how far the result may depart from your original: `0.2`–`0.4` for a faithful touch-up, `0.6`–`0.7` (default `0.65`) for a reinterpretation that keeps the composition, `0.8`+ to treat the reference as loose inspiration.
- **OpenAI editing needs `gpt-image-1` or `dall-e-2`.** `dall-e-3` can only generate *new* images — asking it to edit returns a clear message telling you to change the pinned model in Settings → Visual Models → LLM Provider Models, or use Stability instead.
- **The chat model reviews the result.** The generated image is attached to the next turn, so the assistant can see whether the edit matched your request and regenerate with a corrected prompt, a different strength, or the other provider if it missed.
- **It cannot upscale or denoise.** "Make it clearer" produces a *re-imagined* picture at the provider's own resolution, not a sharpened copy of your file. Your original is never modified.

### Output location

- **Write to Repo + repo loaded** → `{repo}/Documents/Images/`
- **Otherwise** → `MyDocuments/Codayak/Documents/session_{timestamp}/Images/`

Generated images are auto-registered with `.codaignore` so they don't pollute future searches.

---

## Speech (TTS, STT, Conversation Mode)

Five providers, each independently configurable in **Settings → Audio Models**:
- **Deepgram** — recommended default (Aura-2 TTS, Nova-3 STT). One key for both.
- **ElevenLabs** — TTS and STT. Highest-quality voices.
- **OpenAI** — TTS + batch STT.
- **AssemblyAI** — STT (real-time speaker separation, well suited to the Meeting Assistant).
- **Azure** — TTS (style/pitch controls) + STT.

### TTS toggle

The 🔊 icon on the chat toolbar. When on, the assistant's response is read aloud; Codayak injects a speech-friendly system prompt so the response stays in natural spoken English (no markdown, no code blocks). How much it says is set by the **Speech verbosity** dial in **Settings → General → Response Style** — Concise (default), Balanced, or Detailed. The assistant won't read out code or file contents aloud unless Speech verbosity is set to **Detailed**; otherwise it describes them in plain words.

### STT (dictation)

The 🎙 icon. Streams microphone audio to the configured STT provider; transcribed text appears in the message box as you speak. Edit and send normally.

### Conversation Mode

Toggle **both** 🔊 and 🎙 and Codayak goes hands-free:
- You speak; the transcript accumulates.
- After a configurable silence (default 800 ms), Codayak auto-sends.
- The assistant responds; TTS speaks it.
- "Stop", "wait", "cancel", "hang on" trigger immediate barge-in — TTS halts, the stream cancels, Codayak goes back to listening.

Tune the silence window, barge-in minimum length, filler-word filter, interrupt-word list, confidence floor, and auto-send minimum length in **Settings → Audio Models → Conversation Mode**.

---

## Meeting Assistant

The 🎤 **Meeting** section sits quietly in the background during a call and turns it into three things: a **live transcript**, a curated **Insights feed**, and an end-of-meeting **summary**. It hears both sides of the call — your microphone, and everyone else through your speakers — so no bot joins the meeting and the other participants need nothing installed.

A meeting flows like this:

1. **Start** — Codayak begins transcribing live and, on Microsoft Teams, reads the attendee list straight from the meeting window.
2. **During the call** — the transcript and Insights feed fill in as people speak; rename speakers whenever you like.
3. **Stop** — if **Record for batch diarisation** is on (it is by default), Codayak re-transcribes the whole meeting recording in one pass and replaces the live transcript with a noticeably cleaner, better-attributed one.
4. **Tidy up** — rename any remaining *Speaker N* voices; if you're not sure who's talking, replay that turn's audio and listen.
5. **📄 Generate Summary** — a meeting-wide brief built from the transcript exactly as you see it.

### Setting it up (Settings → Audio Models)

Everything the Meeting Assistant uses is configured on one tab — **Settings → Audio Models**:

- **Speech-to-text provider** — the same STT selection used for dictation. Deepgram, AssemblyAI and Azure separate speakers in real time (recommended for meetings); OpenAI/Whisper transcribes but can't tell speakers apart.
- **Analysis provider, model and interval** — the LLM that writes the Insights feed and the final summary, and how often the feed updates (default ~45 seconds).
- **Domain terms** — your product names, acronyms and jargon (e.g. `Codayak, consignment, earthmoving`). The recogniser is biased toward these words — the single biggest accuracy lever for a jargon-heavy meeting — and the summary treats them as the correct spellings. Set them **before** you click Start.
- **Record for batch diarisation** (on by default) — keep a recording of the meeting so that, when you click **Stop**, the whole recording is re-transcribed and re-diarised in one pass. Hearing the entire meeting at once produces a much cleaner, better-attributed transcript than live streaming can, and the kept recording is what makes **Replay this block** possible while you tidy up names afterwards. The recording never leaves your machine and is deleted when your next meeting starts. **Prefer no recording?** Turn it off — nothing is kept on disk, the live transcript is final, and Replay isn't available.
- **Audio quality (advanced)** — sample rate, confidence floor and utterance-end window; see *Audio quality* below.

### The two panes

- **Live Transcription** — the verbatim record, one line per utterance, speaker-prefixed. Speaker labels (`You`, `Speaker 1`, `Speaker 2`…) come from automatic diarisation and are imperfect — see *Renaming speakers* below.
- **Live Insights** — a curated, colour-coded feed of **decisions**, **action items**, **open questions**, **risks/blockers**, **claims to verify**, and **key points**, distilled from the conversation every ~45 seconds and deduplicated so ongoing topics don't re-surface. This is *not* a re-render of the transcript — each row is a single distilled item with an owner (when known) and a timestamp, and filter chips beside the pane's title let you show just the kinds you care about.

The Insights feed is gated by the **Live insights** checkbox, which is **on by default**. Untick it for a lower-cost, transcript-only session — the pane stays empty (the transcript still fills), and unticking mid-meeting clears whatever it was showing. The end-of-meeting summary works either way.

### Meeting type

The **Meeting type** dropdown is a lens that changes what the Insights feed watches for and how the final summary is shaped:

| Type | Insights emphasis |
|---|---|
| **General** | Decisions, actions, questions, key points |
| **Team Standup** | Progress and especially **blockers** |
| **Interview** | The candidate's claims, strengths, gaps |
| **Sales / Client Call** | Needs, pain points, objections, buying signals |
| **One-on-One** | Feedback, commitments, wellbeing signals |
| **Brainstorm** | Every distinct idea and theme (captured generously) |

The type also shapes the final summary (a standup leads with blockers, an interview ends with a hire recommendation, etc.). You can change it mid-meeting; the next analysis pass picks it up. Your choice is remembered across restarts.

### Transcription accuracy and the roster

- **The attendee roster builds itself.** On Microsoft Teams, Codayak reads the call's participant tiles and active-speaker signal, so attendees are identified automatically and lines are attributed to whoever is actually speaking; on other platforms Codayak runs diarisation-only and says so. Every name you assign via **Rename speaker** is folded into the roster and treated as ground truth for the summary's attribution.
- **You are identified automatically.** Your microphone is a separate audio channel, so everything on it is yours by definition; on Teams, Codayak also reads your own tile to put your real name on those lines without any setup — and while you're **muted in the meeting client**, anything your mic picks up (typing, room chatter) is excluded as non-meeting audio.
- **Codayak never guesses a name.** A meeting-client name is attached to a voice only when the evidence is conclusive; anything uncertain stays an honest *Speaker N* for you to name. Renaming a *Speaker N* takes a click — untangling a confidently wrong guess doesn't.

### Renaming speakers

Streaming diarisation is imperfect — it can split one person across labels or merge two people. Once a speaker has been heard, a **Rename speaker** row appears with a button per speaker; click one, type the real name, and every transcript line for that speaker is relabelled for the rest of the meeting. **Naming two speakers the same merges them into one person** — so if diarisation split one real person across two labels, giving both the same name collapses them and the duplicate button disappears.

**Correcting individual turns** — right-click a transcript turn for surgical fixes: **Rename speaker…** reassigns that turn (and the following lines from the same voice) to the right person, with a pick list of **every attendee the meeting client saw** plus free-text entry for anyone else; a turn still carrying a machine label (*Speaker N*) renames the whole cluster, exactly like the rename-bar buttons. **🔊 Replay this block** (available after Stop, once batch processing has run) plays back that turn's audio so you can *hear* who is speaking before renaming — the meeting recording is kept on your machine for exactly this purpose and deleted when your next meeting starts. If your Windows output device is muted, replay would be silent — Codayak appends **Output Muted** in red to the replay status on the meeting status line, and the status bar (bottom left) shows **Replaying...** during replay with **Output Muted** appended when the device is muted; unmute the device in Windows and replay again. **Copy transcript** puts the full transcript on the clipboard. Codayak warns before a rename that would relabel most of the meeting (a suspected merged cluster) and recommends per-turn reassignment instead.

### Audio quality (advanced)

**Settings → Audio Models → Meeting Assistant → Audio sample rate** sets the rate the mic and system audio are resampled to before transcription. A higher rate preserves more consonant detail (better word accuracy) at the cost of more bandwidth: **24 kHz** (default) balances the two and halves typical 48 kHz system audio cleanly; **16 kHz** is the leaner telephony rate; **48 kHz** sends system audio at its native rate. Most users can leave it at 24 kHz. The rate is fixed when you click Start, so change it before a meeting.

The same section holds the other fine-tuning knobs: an **STT confidence floor** (drop utterances the recogniser isn't sure about), the **utterance end (ms)** window (how long a pause closes an utterance), and crash-safe **transcript persistence** (on by default). **Record for batch diarisation** — the after-meeting reprocessing pass and its kept recording — is covered under *Setting it up* above.

### Generate Summary

After you click **Stop**, click **📄 Generate Summary** for a meeting-wide brief — key decisions, action items grouped per person, unresolved questions, and a structure shaped by the meeting type. Copy, email, print, or save it to Markdown. The summary also records **attendance** — who was present and who was absent — worked out from the roster and the transcript.

The summary is **read-only over your transcript**: it is generated from the transcript exactly as attributed (the provider's diarisation plus your renames and reassignments), with the original live transcript supplied as weaker reference material, the meeting client's attendee list, and your Domain terms as authoritative vocabulary. It never rewrites or re-attributes a transcript line — a voice you left as *Speaker N* appears as *Speaker N* in the summary — which is why naming speakers before generating gives the most readable result.

If any voices are still unnamed (labels like *Speaker 2*), Codayak asks before proceeding: a dialog lists the unnamed speakers and reminds you they will appear as *Speaker N* in the summary. **No** (the default) takes you back to name them with the Rename speaker buttons; **Yes** generates anyway — the right choice when you genuinely can't identify a voice.

All three outputs name the **meeting type** so a reader can tell at a glance which meeting it was: the email subject and print heading read e.g. `Team Standup Meeting summary — 27 July 2026`, and the default save filename is `team-standup-meeting-summary-20260727-134500.md`. The type used is the one the summary was *generated* with, so changing the dropdown afterwards doesn't relabel an existing summary.

**✉ Email…** opens your **default mail client** with a draft ready to go: a subject naming the meeting type and date and the summary as the body — add the recipients yourself. Codayak sends nothing itself and stores no mail credentials; you review the draft and press Send. If the summary is too long to pass through a `mailto:` link — which would silently truncate it — Codayak instead copies the full summary to the clipboard and opens an empty draft for you to paste into, telling you so. If Windows has no default mail app registered, you get a message explaining how to set one.

**Attendance and attribution warnings.** Before the summary is written, Codayak runs a read-only *attendance analysis* on the [Worker LLM](#worker-llm) — who actually attended, who was absent — which becomes a hard constraint on the summary (an absent person is never listed as a participant or credited with statements). Codayak also cross-checks the transcript's hand-off cues ("over to you, X") against the attribution: any mismatch is listed in the summary as an **attribution warning** for you to re-check — never silently relabelled.

> **Tip:** renaming a speaker relabels every past line for that voice retroactively — including in the buffer the summary is built from — so a name you assign at any point is applied consistently throughout. What you see in the transcript pane when you click Generate Summary is exactly what gets summarised.

---

## DevOps integration

The **Settings → DevOps** tab has three rows: platform credentials (Azure DevOps left, GitHub right), then two team-wide rule sets applying to both platforms — **Coding Style Rules** and **Pull Request Review Rules**. Both are free-text Markdown, both feed the LLM through tool descriptions, and both share a four-button toolbar: **📖 Generate from repo… / 💾 Save… / 📂 Load… / Reset to Defaults**.

### Credentials

Each platform supports **multiple connections** with one marked active. The **Connection** dropdown at the top of each side lists every connection you've configured; the fields beneath it edit whichever one is selected, and **➕ / 🗑** add and delete connections. The selected connection is the **active** one — it's what every tool call, PR review, and wiki operation for that platform uses. Give each connection a **Name** (it's what appears in the dropdown and in the *Add Ref Wiki* picker).

Switching the dropdown saves your in-progress edits into the connection you're leaving, so nothing is lost. Click **Save** at the bottom of the page to persist connections, deletions, and the active selection.

**Azure DevOps** — per connection: Name, Organisation, Project, PAT, and default repository. Tools: `ADO_SearchWorkItems`, `ADO_GetWorkItem`, `ADO_CreateWorkItem`, `ADO_UpdateWorkItem`, `ADO_DeleteWorkItem`, `ADO_ListPullRequests`, `ADO_GetPullRequest`, `ADO_GetFileAtCommit`, `ADO_ReviewPullRequest`, `ADO_SetPullRequestVote`, plus wiki tools.

**Work-item badge.** When the assistant looks up the work item you're actually *working on* (as opposed to merely referencing one), it flags the lookup and Codayak shows the work-item number in the blue repo toolbar and the window title (e.g. `Codayak — WI13914 — <title>`), so multiple Codayak windows on different work items are easy to tell apart. The badge clears on Reset Session.

**GitHub** — per connection: Name, Repository (`owner/repo`), and PAT. Tools: `GH_SearchIssues`, `GH_GetIssue`, `GH_CreateIssue`, `GH_UpdateIssue`, `GH_ListPullRequests`, `GH_GetPullRequest`, `GH_GetFileAtRef`, `GH_ReviewPullRequest`, `GH_SetPullRequestVote`, plus wiki tools.

A platform with no configured connection is silently disabled without affecting the other.

### Azure DevOps wiki behaviour

The Azure DevOps wiki tools (`ADO_SearchWiki`, `ADO_GetWikiPage`, `ADO_CreateWikiPage`, `ADO_UpdateWikiPage`) resolve and address the wiki belonging to the configured **Project** — you don't name the wiki:

- **Automatic wiki resolution.** Codayak lists the project's wikis and uses the project wiki (the one whose name is typically `{Project}.wiki`, e.g. project `Contoso Admin` → wiki `Contoso-Admin.wiki`). The resolved identifier is cached and re-resolves automatically if you change the Project setting. If the project has no wiki yet, you get a clear "create a wiki first" message rather than an opaque error.
- **Full-text content search.** `ADO_SearchWiki` searches page **body text** (via the Azure DevOps Search service) and returns matching pages with content snippets, so a term that appears only inside a page — not in its title — is still found. This needs the **Code/Wiki Search** extension installed on the organisation and a PAT with wiki read scope; when that extension isn't present, Codayak degrades gracefully to a page-name search and tells you it did so.
- **Create-or-update is unambiguous.** Both `ADO_CreateWikiPage` and `ADO_UpdateWikiPage` create the page if it's missing and update it (with the required version check) if it already exists — so whichever the model picks does the right thing, and an existing page is never accidentally clobbered.
- **Pages are addressed by path**, e.g. `/Our-People` (not the numeric page ID shown in the browser URL).

### GitHub wiki behaviour

GitHub has **no REST API for wikis** — a GitHub wiki is a plain git repository at `https://github.com/{owner}/{repo}.wiki.git`. The GitHub wiki tools (`GH_SearchWiki`, `GH_GetWikiPage`, `GH_CreateWikiPage`, `GH_UpdateWikiPage`) and the GitHub flavour of *Add Ref Wiki* therefore work by **cloning the wiki's git repository** (via LibGit2Sharp) and reading/committing its Markdown files directly:

- **Local cache.** The wiki is cloned once into `%LOCALAPPDATA%\Coda\wiki-git-cache\{owner}_{repo}` and refreshed with a pull on each use — never inside your working repository. The cache is disposable: a corrupt copy is deleted and re-cloned automatically.
- **The first page must already exist.** GitHub only creates the wiki repository when the first page is saved in the repo's **Wiki tab** — until then there is nothing to clone, and the tools report exactly that: *"No wiki exists for {owner}/{repo}. GitHub wikis are created by saving a first page in the repo's Wiki tab."*
- **PAT scope.** Reading a **private** repo's wiki and any wiki **write** needs a classic PAT with `repo` scope; public wikis can be read without special scope. The PAT is passed only through git's credential handshake — it never appears in URLs, logs, or error messages.
- **Page names are tolerant.** Pages are Markdown files at the wiki root, named per GitHub's convention (spaces become hyphens: `Deployment Guide` → `Deployment-Guide.md`). Reads resolve the name verbatim first, then with spaces→hyphens, then case-insensitively, and report which file resolved.
- **Create vs update.** `GH_CreateWikiPage` is create-or-update (an existing page is updated, matching the ADO tools); `GH_UpdateWikiPage` requires the page to exist and says so plainly when it doesn't. Writes are committed as `Coda <coda@local>` and pushed; a concurrent edit is reconciled with one automatic pull-and-retry.

### Coding Style Rules

Free-text Markdown describing your team's standards — naming, async patterns, error handling, brace style, doc expectations. Injected into the description of every write-bearing tool so the LLM matches house style *as it composes the call*, not as an afterthought. Blank ⇒ the LLM uses its own judgement.

### Pull Request Review Rules

A single Markdown box applying to **both** ADO and GitHub PR reviews (platform-specific subsections live as their own headings inside the same blob). Injected into both review tools. **Reset to Defaults** loads a sensible starter set.

Note on GitHub votes: a `GH_SetPullRequestVote` REQUEST_CHANGES vote submits a brief default comment ("Changes requested — see review comments.") because GitHub requires one on a changes-requested review, and a changes-requested review only hard-blocks merging on repositories with a branch-protection rule requiring reviews — an unprotected repo shows the state but still permits merge.

### The four buttons

- **📖 Generate from repo…** — hands the source-code map plus a sample of files to the **Worker LLM** and extracts the de-facto rules from what the codebase actually does. Asks **Replace / Append / Cancel** if the box already has content.
- **💾 Save… / 📂 Load…** — round-trip the rules to a `.md` file (source-control your standards alongside the repo).
- **Reset to Defaults** — Coding Style resets to blank; PR Review resets to the built-in starter set.

Click **Save** at the bottom of the Settings page to persist.

---

## Skills

Skills are reusable instruction documents the assistant loads **automatically when the task matches** — modelled on GitHub Copilot's Skills. Typical examples:

- *"Working on the Contoso application"* — the conventions, gotchas, and domain knowledge for one specific codebase.
- *"Creating work items for project X"* — exactly what information a work item must include, which fields to set, the team's phrasing conventions.

Manage them in **Settings → Skills**: an entry form on the left (Name, Enabled, Description, Body) and the skill list on the right (Enabled | Name | Description columns).

- **Add a skill** — type the Name/Description/Body straight into the form and click **Add**; the skill appears in the list and the form clears for the next one.
- **Edit a skill** — select it in the list; its details fill the form, the button changes to **Save**, and a **Cancel** button appears. Save writes the changes back; Cancel abandons them.
- **Delete** (below the list) removes the selected skill after confirmation.
- The **Enabled** checkbox applies to **that skill only** — untick it to park a skill without deleting it (shown by the ✔ column in the list).

Add, Save, and Delete persist **immediately** (like the Memory tab) — no separate Save click is needed.

### How activation works ("auto by intent")

Only each skill's **name and description** are advertised to the model, as part of a `LoadSkill` tool — roughly one line of context per skill, regardless of how large the bodies are. When the model judges that the current task matches a skill's description, it calls `LoadSkill` and receives the full body, then applies it. This means:

- **The description is the trigger.** Write it as a clear "load this when…" sentence: *"Load when creating or updating Azure DevOps work items for the Contoso project."* A vague description means the skill won't fire when it should.
- **A big skill library costs almost nothing** until a skill is actually used.
- **Untick Enabled** to park a skill without deleting it — it disappears from the model's view entirely. With no enabled skills, the LoadSkill tool isn't registered at all.

Skills are deliberately separate from the DevOps tab's **Coding Style Rules** and **PR Review Rules** — those are injected at specific, targeted points (write-bearing tools and the PR-review tools) and are always active; skills are general-purpose and loaded on demand.

---

## Database execution

The **ExecuteSql** tool lets Codayak run a SQL command against a relational database so it can query data, inspect schema, and — crucially — *test the database code it writes* rather than handing you SQL it has never run. On by default; turn it off at **Settings → Tools → Database Execution**.

### Engines

Five engines are supported via bundled ADO.NET drivers, so nothing needs installing:

| Engine | `engine` value | Driver |
|---|---|---|
| SQL Server / Azure SQL | `sqlserver` | Microsoft.Data.SqlClient |
| PostgreSQL | `postgresql` | Npgsql |
| MySQL / MariaDB | `mysql` | MySqlConnector |
| SQLite | `sqlite` | Microsoft.Data.Sqlite |
| Oracle | `oracle` | Oracle.ManagedDataAccess.Core |

A request for any other engine returns a clear "no bundled provider" error, which flows back to the model so it can explain the situation to you.

### No configuration — the model drives the connection

There is nothing to set up. The model supplies the **engine** and a **connection string** on each call — either found in the code it's working on (e.g. a `web.config`/`appsettings.json`) or built from connection details you give it in chat. There are no saved connections and no stored credentials.

### The safety gate: permission by initiative

Codayak must never touch a database on its **own initiative** without your permission — but when *you* directed the database work, that instruction is the permission. Concretely:

- **You asked Codayak to run/query/update the database** → it proceeds without a prompt. Your request is the consent.
- **Codayak decided to hit a database on its own** → a confirmation prompt appears first, showing the **engine**, the **target** (host/database), the **operation** (Read / Write / DDL), the **credential-masked connection string**, and the **exact SQL**. It runs only if you click **Yes**.
- **Once you approve a given database**, Codayak may keep querying and updating *that* database for the rest of the session without re-prompting — so approval is per-database, not per-statement.
- **Denied or unattended** (e.g. a headless/Team-Mode context with no one to prompt) → the command is refused and the refusal is returned to the model. Denials aren't remembered: reconnecting later simply prompts again.

Approvals are cleared when you reset the session.

### Results and errors

- **Queries** (SELECT and friends) return a row-capped JSON result set (columns + rows; default cap 200 rows, flagged when truncated).
- **INSERT / UPDATE / DELETE / DDL** return the rows-affected count.
- **Any database error** — bad credentials, unreachable host, syntax error, a missing/unsupported driver — is returned **verbatim** so the model can diagnose it and tell you how to fix it.
- Optional per-call controls: **maxRows** (default 200) and **commandTimeoutSeconds** (default 30).

---

## Research panel

The **Research panel** (the `DeliberateResearch` tool) is Codayak's "generate several alternatives before converging" capability. Instead of answering a hard question with a single line of reasoning — the failure mode where a model latches onto one plausible-but-wrong path — it fans out a small cohort of independent worker LLMs over the *same* question and hands every perspective back to the main model to judge.

### How it works

1. **Fan-out** — it spawns *N* workers (configurable 0–10, default 6). Each is given a **different analytical angle** — simplest solution, failure modes, first principles, an adjacent-field expert, the steelmanned opposite, the pragmatist on a deadline, long-term maintainability, evidence-vs-unknowns, the user's lens, and a hybrid-seeking synthesiser — and a **temperature spread** from conservative (0.2) to exploratory (1.0). Varying the *framing*, not just the temperature, is what actually widens the search of the problem space.
2. **Collate** — every worker's labelled perspective is gathered into one deliberation brief (failed/timed-out workers are reported, not silently dropped).
3. **Judge** — the **main chat model** reads the brief, compares where the angles agree and conflict, discards weak arguments, and recommends the best next step (or the best combination), citing which angles it drew on. The panel deliberately does **not** pick a winner itself, because only the main model has the full conversation context.

It **writes no files** — the output is a deliberation brief, not an artefact. The worker cohort runs on the [Worker LLM](#worker-llm), so you can point it at a cheaper/faster tier than your main chat.

### When it runs

Three independent settings — two explicit-request toggles and one self-election dial — control when the panel runs:

- **Research requests** (default **on**) — you ask for it directly: "research this from several angles", "give me the alternatives before we decide".
- **Design / requirements requests** (default **on**) — you ask Codayak to design an app, or draft a spec/requirements document; the panel fans out over the design question before Codayak commits to one structure.
- **Self-election eagerness** (default **Conservative**) — governs ONLY Codayak firing the panel unprompted, with no request for research or design. Four levels, mirroring the Trust Engine's `SelfVerifyEagerness` pattern:
  1. **User invoked** — never self-elects; the two toggles above are the only way the panel runs.
  2. **Conservative** *(default)* — self-elects when genuinely struggling to find a solution.
  3. **Standard** — as Conservative, plus before consequential or hard-to-reverse decisions.
  4. **Liberal** — as Standard, plus whenever a decision has more than one plausible approach.

It is deliberately conservative even at Liberal — the panel costs many times the tokens of a normal answer, so unprompted use is reserved for genuine impasses or high-stakes forks, not every hard question.

### Configuring it

**Settings → Tools**, in the *Research Panel* box at the top of the tab:
- **Worker perspectives (0–10)** — the default cohort size. **0 disables the tool entirely** (it disappears from the model's toolset). The model may request a different count per call, clamped to this range.
- **Research requests** / **Design / requirements requests** — the two explicit-request toggles described above.
- **Self-election eagerness** — the four-level dial described above; controls only unprompted use.
- The **Research Panel** toggle among the per-tool toggles in the same tab is the master on/off switch for everything configured above.

Live progress ("Perspective 3 (Failure modes): in") streams to the tool-output pane as each worker lands.

---

## Worker LLM

The **Worker LLM** is a single shared configuration for every background LLM call Codayak makes — the calls that aren't your main chat. It lives in the top toolbar, right of the main LLM controls.

### What uses it

- **[Coordinator](#the-coordinator-multi-file-builds)** — every worker session in a multi-file build.
- **[Research panel](#research-panel)** — every worker in the fan-out cohort.
- **[Memory evolution](#learning-memory)** — the merge/supersede/link pass after a new memory is inserted.
- **[Manual memory creation](#learning-memory)** — the *Create memory from description* box.
- **[Rule generation](#devops-integration)** — the DevOps **Generate from repo…** buttons.
- **[Session restore](#restore-session)** — distilling saved conversations into a compact session summary.
- **[Meeting Assistant](#meeting-assistant)** — the read-only attendance analysis that runs before a summary.

One control drives them all.

### Default behaviour

**Worker LLM: same as main** is ticked by default — workers mirror your main model, no extra config.

### Configuring a separate worker

Untick the box; a second toolbar row appears with its own provider, model, max-tokens, and temperature/effort. Unlike the main dropdowns, worker controls are **not** locked during an active session (worker calls are stateless). Changes persist immediately — the next worker call picks them up.

### When to use a different worker

- **Cheaper background tasks** — point the Coordinator at a fast tier while keeping chat on the strongest model.
- **Quotas** — route background work to a different provider to stay under a rate limit.

---

## Help section

The ❓ icon opens an in-app reader for README.md, USER_GUIDE.md and EULA.md.

- **Defaults to README**; the three header buttons switch between the README, this guide and the licence.
- **← / → arrows** (top right of the document) step back and forward through in-document jumps — click a Contents link, read, then click **←** to return to where you were.
- **💾 Save…** copies the raw `.md` source. **🖨 Print** opens WebView2's print dialog (PDF or physical printer).
- **Theming** matches the app; print is forced light-on-white to save ink.
- **File resolution** — Codayak looks next to the `.exe` first, then walks a few parent directories so dev builds resolve correctly. If neither file is present, a friendly explanation is shown.

---

## Settings reference

### Resetting settings
The Settings header carries two reset affordances:
- **Factory Reset…** (top-right, beside Save) — returns Codayak to a clean state. It opens a dialog of independently-tickable options (all ticked by default): it ALWAYS resets every tab to its code defaults, and additionally — for each option you leave ticked — removes all API keys & proxy details, clears all learning memories, resets the model catalog to the shipped baseline, and resets the Coding Style / PR Review rules. Untick any option to keep that data. This is the right button for handing a machine over or starting fresh.
- **Per-tab Reset to Defaults** — General, Tools, Audio Models, Code Map, and Trust Engine each have their own *Reset to Defaults* button at the foot of the tab that resets ONLY that tab's settings (the Audio Models reset keeps your API keys — use Factory Reset to remove keys). DevOps (Coding Style / PR Review) and Hot Keys have their own resets; Memory has a *Reset Behaviour to Defaults* button. Per-tab resets don't auto-save (except Tools, whose toggles persist immediately) — click Save to commit.

### General
- **Theme** — Dark / Light.
- **Font size** — main editor; chrome scales one step below.
- **Response style** — two verbosity dials that nudge how concise or thorough replies are (they add a short style hint to the system prompt; they change length and tone, not what gets answered):
  - **Standard verbosity** — for normal on-screen replies. **Concise** / **Balanced** (default) / **Detailed**. Balanced leaves the model to its own judgement (no hint injected, so it matches an unconfigured Codayak).
  - **Speech verbosity** — for spoken replies, applied only while the read-aloud (🔊 TTS) toggle is on, where it takes over from Standard. **Concise** (default) / **Balanced** / **Detailed**. All three keep replies in spoken English with no markdown; the difference is length and whether code or file contents may be read aloud — only **Detailed** reads them out, while Concise and Balanced describe them in plain words instead.
- **Backup retention (days)** — sweeps `.coda/backups/` on startup and on demand.
- **Context-window pruning** — sliding threshold between Max (≤50% fill) and Min (≥85% fill).
- **Embedding Model** — download status, a manual **Download Now** retry, and advanced URL overrides for the shared on-device embedder (see [Learning memory](#learning-memory)).
- **Diagnostics** — debug-logging toggle and app-log retention.
- **Reset General to Defaults** — resets just this tab.

### Tools
Per-tool / per-group toggles — the actual labels are: Web Search, Search Documents, Mermaid Diagrams, Document Creation, Coordinator, Research Panel, Image Generation, Word Documents, DevOps, Repository Tools, Code Quality, Build & Test, Patch & Scaffold, Backup/Restore, Delete / Move File & Directory, Database Execution, Browser UI Testing, Desktop UI Testing, Codayak Help Docs — plus **Max tool-call rounds** (default 100), **Worker max tool-call rounds** (default 4 — the per-worker ceiling for each Research Panel perspective or Coordinator file, kept tighter than the main limit because workers run in parallel), and the **Research Panel** knobs (worker count 0–10, the Research requests / Design requests toggles, and the self-election eagerness dial; see [Research panel](#research-panel)). Disabled tools leave the model's context entirely.

### LLM Providers
Per-provider: API key, default model, max tokens, temperature/effort, model-discovery URL override (and base URL / Group ID where applicable). **A provider's key is entered here once** and is reused by its chat, image, video, and speech models.

### Chat Models
The chat model catalogue — per-provider visible/hidden models and the default.

**Fetch Latest** is a review-first process: it pulls the provider's `/models` list, classifies each model (definite image/video/speech families to their tabs, the rest defaulting to Chat), live-checks each NEW chat model against the generate endpoint, then presents **every model in a review dialog** — classification (editable per row), the endpoint result, and a recommended action. Rows recommended for exclusion are pre-ticked; adjust anything you disagree with, then **Import**. **Cancel imports nothing.** The provider's image, video, and speech models are imported by the same fetch and appear on the **Visual Models** / **Audio Models** tabs — see [One fetch, three tabs](#one-fetch-three-tabs).

**Verify Endpoints** runs the same review over the models already in the catalogue: chat models get a minimal live call, non-chat models a listing check, and the same dialog lets you **reclassify** any model and tick which to remove. Because the Audio and Visual tabs are views over this one catalogue, applying the review updates the Chat Models list, the TTS/STT provider dropdowns, and the image/video provider dropdowns together — this is the single cleanup path for all three tabs.

**Delete Older** removes models released before the *Released on/after* date. **Scope follows the provider dropdown**: with a provider selected only its models are swept; with none selected the sweep covers all providers. Models with no known release date are always kept, and a provider's active default is never removed.

Chat-model classification reads the **HTTP status code** first — structured and stable, unlike error prose that gets reworded between releases — and consults the message only to disambiguate a 400/422, which providers use for all three cases. Anything unrecognised falls through to *no verdict*: leaving a dead entry in the catalog is far cheaper than inviting you to delete a model that works.

### Web Search
Google Custom Search API key + engine ID, optional proxy config, parallel page count, Offscreen browser toggle.

### Audio Models
Provider selectors (TTS, STT) — which list the dedicated speech providers **plus** the LLM providers' audio models from the catalogue (`OpenAI: gpt-4o-mini-tts` etc., key-filtered; selecting one pins that model) — the dedicated speech providers' own keys and tuning, Meeting Assistant audio quality, and Conversation Mode tuning. Audio is always a deliberate user selection; there is no agent-choose option.

### Visual Models
The **Default Provider** section (Image Provider + Video Provider, key-filtered, defaulting to *Let the Agent Choose*), then the model sections: Stability AI (own key/model/style) and **LLM Provider Models** (Image Model + Video Model dropdowns, catalogue-driven and key-filtered; provider keys come from LLM Providers).

### DevOps
ADO + GitHub connections (multiple per platform, one active each), plus the team-wide Coding Style and PR Review rules. See [DevOps integration](#devops-integration).

### Skills
Named instruction documents the assistant loads on demand when the task matches their description. See [Skills](#skills).

### Code Map
Source-code-map skeleton threshold (always applies), plus the opt-in master toggle for dependency-aware working-set retrieval, dispatch resilience, and persisted Coordinator project state. See [Repository intelligence](#repository-intelligence).

### Settings tab layout

The tabs are grouped by purpose, left to right:

| Tab | What it holds |
|---|---|
| **General** | Appearance, fonts, embedding model, factory reset. |
| **Tools** | Per-tool enable/disable toggles. |
| **LLM Providers** | API keys, discovery URLs, and base URLs for every chat provider. **This is where a provider's key lives** — the model tabs below reuse it. |
| **Chat Models** | The chat model catalogue: Add/Edit/Hide/Delete, Fetch Latest, Verify Endpoints. Lists **chat models only**. |
| **Audio Models** | Speech configuration. The TTS/STT dropdowns list the dedicated providers (Deepgram, ElevenLabs, AssemblyAI, Azure — own keys and tuning) plus the LLM providers' audio models from the catalogue (no key needed; populated by Fetch Latest). |
| **Visual Models** | Image and video. Provider selection at the top (Default Provider — key-filtered, 'Let the Agent Choose' default); model selection below (Stability AI, LLM Provider Models). |
| **Web Search** | Google Custom Search keys, proxy, scraper tuning. |
| **Skills** | On-demand instruction documents. |
| **Memory** | Learning Memory configuration and the memory browser. |
| **Trust Engine** | Verification depth, budgets, self-verify eagerness. |
| **DevOps** | Azure DevOps / GitHub connections, coding-style and PR-review rules. |
| **Code Map** | Source-map skeleton threshold plus the opt-in repository-intelligence machinery. |
| **Team Mode** | Peer-to-peer identity, port, LAN discovery. |
| **Hot Keys** | Keyboard shortcuts. |

### One fetch, three tabs

A provider's `/models` endpoint returns chat, image, video, and speech models in a single response. **Fetch Latest** (on the Chat Models tab) keeps them all, tagging each with its **modality**, so the same fetch populates Chat Models, Audio Models, and Visual Models. Consequences worth knowing:

- Non-chat models **do not appear in the Chat Models tab** or the toolbar model dropdown — they cannot answer a chat completion, so offering one would only produce a model you could select and then fail to use.
- The LLM-provider lists on the Audio and Visual tabs have **no API key field**: each model uses its provider's key from **LLM Providers**.
- Dedicated single-purpose providers (Stability, Deepgram, ElevenLabs, AssemblyAI, Azure Speech) are **not** LLM providers, so they keep their own key and tuning sections.

### Keeping the lists clean

A fetch imports whatever the provider advertises, which can include models your key can't use. Both cleanup tools live on the **Chat Models** tab and cover **every** model type, including the ones shown on Audio Models and Visual Models:

| Button | What it does |
|---|---|
| **Verify Endpoints** | Checks every model for the selected provider, by the method appropriate to each. **Chat** models get a minimal live call (cheap, and a listed-but-uncallable chat model is common). **Image, video, and speech** models are checked against the provider's own model list instead — invoking them would cost real money per probe and a video takes tens of seconds, whereas vanishing from the provider's catalogue is the signal that matters and is free. Every model is listed in the review dialog with an editable classification; only genuinely missing models are pre-ticked for removal, and applying the review updates all three tabs together. |
| **Delete Older** | Removes models released **before** the *Released on/after* date. Scope follows the provider dropdown (selected = that provider only; blank = all providers). Models with **no known release date are always kept** — an unknown date isn't evidence of age — and a provider's **active default is never removed**. Confirms first, listing what will go. |

Both fail safe: if the provider's model list can't be read (bad key, offline, outage), every model comes back as *no verdict* rather than being offered for deletion en masse.

### Memory
The full Learning Memory configuration. See [Learning memory](#learning-memory).

### Trust Engine
Verification depth, token budgets, and self-verify eagerness. See [Trust Engine](#trust-engine-verification).

### Team Mode
Display name, listening port (default 41833; the leader card on the Team Mode page has a **Port** field that edits this same value), LAN auto-advertise toggle. (The per-run **Revisions** limit is set in the **＋ New Task** dialog on the Team Mode page. Session budget defaults and trusted-node fingerprints exist as advanced entries in `coda-settings.json` only — they have no UI on this tab.) See [Team Mode](#team-mode).

### Hot Keys
Customise every keyboard shortcut. Defaults below.

---

## Keyboard shortcuts

| Action | Default | Scope |
|---|---|---|
| Send message | Ctrl+Enter | Main window |
| New line in message box | Enter | Message box |
| Cancel streaming | Escape | Main window |
| Reset session | Ctrl+Shift+N | Main window |
| Toggle theme | Ctrl+Shift+D | Main window |
| Save conversation | Ctrl+S | Main window |
| Print conversation | Ctrl+P | Main window |
| Focus input box | Ctrl+L | Main window |
| Diff: next change | F8 | Diff window |
| Diff: previous change | Shift+F8 | Diff window |

All configurable in **Settings → Hot Keys**, and your choices persist across restarts. The **New line** gesture is what lets you keep a multi-line composing key after reassigning *Send message* to a bare Enter. The two diff hotkeys only fire when the diff window has focus.

---

## Versioning

Codayak uses a four-part version: `Major.Minor.Build.0`.

All three numbers live in `Coda.UI/version.props` (checked into source control — the single source of truth).

- **Major** — manual. Edit `version.props` for a breaking change.
- **Minor** — manual. Edit `version.props` for a feature release (publish does not bump it).
- **Build** — auto-increments on every **Debug** `dotnet build`. Release builds stamp whatever is in `version.props` without changing it — shipping a release is a deliberate act: set the version first, then build Release.
- **Revision** — always 0.

The current version shows bottom-right of the main window. The installer is built by Inno Setup, which reads `version.txt` from the published output.

### Update check

Once a day, Codayak checks for updates by contacting the Techniche Labs update service (the same request counts this install as active — see the EULA, §6). The request carries exactly two values: a random install identifier generated when Codayak is installed, and the version number. Nothing else is ever sent, and the check fails silently when offline. When a newer version is available, Codayak tells you in the chat and the status bar; installing it is always your choice — download the new installer from the releases page and install it over the top (settings and memories are kept).

---

## Troubleshooting

### "No API keys configured"
**Settings → LLM Providers**, paste a key, click Save.

### Context-window exceeded errors
- **Reset** → keep last N exchanges, drop the rest.
- Lower the source-code-map threshold (forces skeleton mode sooner).
- Detach large reference files.

### Memory search shows nothing
- Confirm **Settings → Memory → Enable Learning Memory** is ticked.
- Confirm the embedding model is downloaded (banner above the grid).
- Lower **Proactive min score** temporarily to confirm the pipeline is wired up.

### Tool calls fail with "no repo loaded"
Repo-required tools need **Select Repo** first. Write-bearing tools additionally need **Write to Repo** ticked.

### Embedding model download fails
The default URL points at HuggingFace. If HF moves the file, Codayak's web-search URL resolver tries to find the new one automatically — watch the status bar. The resolved URL is persisted, so it only happens once.

### Speech doesn't work
- Check the API key for the selected provider (**Settings → Audio Models**). LLM-provider speech models use the key from **Settings → LLM Providers**; the dedicated providers (Deepgram, ElevenLabs, AssemblyAI, Azure) have their own key fields on the Audio Models tab.
- Confirm the provider dropdown matches the credentials entered.
- For Conversation Mode, both TTS and STT must be enabled.

### Log file location
- Codayak's own log: `%LOCALAPPDATA%\Coda\logs\app.log`. Always available, rotated each session; archives older than the retention window are swept on startup.
- Codayak's own debug tee (DEBUG builds run against a repo): `{repo}/.coda/Logs/debug.log` — Codayak writing its app log into the repo when *it* is the app under development. Read it via the RequestDocuments / SearchDocuments tools (which can reach `.coda/`); RequestSourceFiles cannot.
- User-app debug log (convention for apps Codayak builds): `{repo}/.coda/Logs/debug.log` — written by your app at runtime under `.coda/` so one ignore entry covers it.
- Dispatch outcomes: filter `app.log` by source `ToolDispatchPipeline`.

---

## Where things live on disk

| Location | Contents |
|---|---|
| `%LOCALAPPDATA%/Coda/coda-settings.json` | All settings |
| `%LOCALAPPDATA%/Coda/models.json` | Model catalog overlay |
| `%APPDATA%/Coda/wiki-cache/` | Cached wiki page trees (one JSON per wiki) |
| `%APPDATA%/Coda/team-mode.key` | Team Mode Ed25519 identity keypair |
| `%LOCALAPPDATA%/Coda/Sessions/` | Team Mode session state |
| `%LOCALAPPDATA%/Coda/Embeddings/` | BGE ONNX model + vocab |
| `%LOCALAPPDATA%/Coda/learning.db` | SQLite memory store |
| `{repo}/.coda/backups/{timestamp}/` | Per-write file backups |
| `{repo}/.coda/verification/` | Trust Engine reports |
| `{repo}/.coda/task_manifest.json` | Coordinator project manifest (cumulative across phases) |
| `{repo}/.coda/Logs/debug.log` | Debug log written into the repo: the user-app's own log (convention for apps Codayak generates), and Codayak's own tee when a DEBUG build of Codayak runs against a repo. Readable via RequestDocuments/SearchDocuments, not RequestSourceFiles. |
| `%LOCALAPPDATA%\Coda\logs\app.log` | Codayak's own application log (always available) |
| `{repo}/Documents/` | Codayak-generated artefacts in repo-write mode |
| `MyDocuments/Codayak/Documents/session_{timestamp}/` | Codayak-generated artefacts in scratch mode |

---

*End of guide. Suggestions and corrections welcome via GitHub issues.*

