# Changelog

All notable changes to **Codayak** are listed here, newest first. Each entry links to the signed installer on the GitHub release page.

Codayak is a free AI coding workbench for Windows 10 and 11, built for .NET and Visual Studio teams — see the [README](README.md) for what it does and the [User Guide](USER_GUIDE.md) for the full reference.

---

## [1.6.0] — 2026-08-29

**First public release.**

- **Download:** [Codayak_Setup_1.6.0.exe](https://github.com/Techniche-Labs/codayak-releases/releases/tag/v1.6.0) — signed by TECHNICHE LABS PTY. LTD.
- **Requirements:** 64-bit Windows 10 (1809) or later / Windows 11 · .NET 8 Desktop Runtime · Microsoft Edge WebView2 Runtime · an API key for at least one supported LLM provider.

### What ships in 1.6.0

- **Seven LLM providers** on your own API keys — Anthropic, OpenAI, xAI, Google, MiniMax, Moonshot, Zhipu — switchable mid-conversation; **Fetch Latest** pulls each provider's current model list.
- **Whole-repo intelligence** — full source-code map (projects, types, members, dependency edges), skeleton fallback, dependency-aware working sets.
- **Read / modify / build / run tools** — patch, create, move, copy, delete (write-gated, backed up, diffed); MSBuild and `dotnet` build, test, run and scaffolding, including legacy ASP.NET projects via full MSBuild.
- **Trust Engine** — build → test → security scan → spec-compliance verification with a High / Moderate / Low trust band, confidence score, per-checker evidence and a saved report under `.coda/verification/`.
- **Real SQL** — `ExecuteSql` against SQL Server, PostgreSQL, MySQL/MariaDB, SQLite and Oracle with bundled drivers; writes gated and confirmed.
- **UI testing** — real Chrome (open / snapshot / click / type / wait) and Windows desktop apps via UI Automation; credentials pass as placeholders.
- **DevOps** — Azure DevOps and GitHub work items, wikis and line-level pull-request review under your team's rules; coding-style and PR-rule generation from your codebase.
- **Multi-file Coordinator** — plans a manifest and generates six-plus files in dependency order across worker sessions, with retry, resume and per-phase verification.
- **Research panel** — one question fanned across up to ten worker LLMs with distinct analytical framings.
- **Learning memory** — on-device embeddings (BGE-small-en-v1.5), hybrid retrieval, proactive lesson injection, confidence tracking, import/export.
- **Team Mode** — several Codayak instances collaborate over the LAN as an encrypted leader/specialist team (Ed25519, X25519, AES-256-GCM, pinned TLS, mDNS discovery); multi-repo development.
- **Skills**, **session continuity** with Restore Session summaries, **side-by-side diff** with rollback, **web search** via Google Custom Search in real Chrome.
- **Image generation** (OpenAI, Stability, xAI, Google) with reference-image editing; **text-to-video** (xAI) and **video analysis** (Gemini).
- **Speech** — TTS/STT across Deepgram, ElevenLabs, OpenAI, AssemblyAI and Azure; hands-free **Conversation Mode**.
- **Meeting Assistant** — live transcript with diarisation, live insights feed, meeting-type lens, end-of-meeting summary, optional batch re-diarisation.

### Known install notes

- **Run the installer as administrator** — a non-elevated install can stop with file-access errors ([#3](https://github.com/Techniche-Labs/codayak-releases/issues/3)).
- **Windows SmartScreen may warn on first run** until the new signing certificate earns reputation — *More info* → confirm publisher **TECHNICHE LABS PTY. LTD.** → *Run anyway* ([#2](https://github.com/Techniche-Labs/codayak-releases/issues/2)).

---

[1.6.0]: https://github.com/Techniche-Labs/codayak-releases/releases/tag/v1.6.0
