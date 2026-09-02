# Security policy

## Supported versions

Only the **latest release** on the [Releases page](https://github.com/Techniche-Labs/codayak-releases/releases/latest) receives fixes. Upgrade by running the new installer over the top — settings, sessions and memories are preserved.

| Version | Supported |
|---|---|
| 1.6.x (latest) | ✅ |
| Earlier | ❌ |

## Reporting a vulnerability

Please **do not** open a public issue for security problems.

Email **contact@technichelabs.com.au** with the subject line `Codayak security report` and include:

- the Codayak version (Help → About, or the installer file name),
- Windows version,
- steps to reproduce, and
- what you believe the impact is (for example: key disclosure, unintended file write outside the working repository, unintended network egress).

You will receive an acknowledgement within **5 business days** and a status update within **14 days**. We will credit you in the release notes when the fix ships unless you ask us not to.

## Verifying what you download

- The installer and application are digitally signed by **TECHNICHE LABS PTY. LTD.** (EV code-signing certificate). Right-click the `.exe` → **Properties** → **Digital Signatures** to check the signer.
- The **SHA-256** hash of each installer is published on its release page.
- Windows SmartScreen may show *"Windows protected your PC"* until the new certificate earns reputation — see [#2](https://github.com/Techniche-Labs/codayak-releases/issues/2). Confirm the publisher name before choosing *Run anyway*; if it reads "Unknown publisher", discard the file and download again from this repository only.

## What Codayak sends off your machine

Codayak runs client-side with no account and no server. Network egress is limited to:

1. the LLM, speech, image or search API calls **you** configured with your own keys;
2. any optional integration you switch on (Azure DevOps, GitHub, web search);
3. a once-a-day update check carrying exactly two values — a random install identifier generated at install time and the version number.

Your files, prompts, conversations, API keys and machine details are never transmitted by Codayak itself. Learning-memory text is embedded on-device and stored in a local SQLite file. Full detail: [README → Safety and privacy](README.md#safety-and-privacy).

## Scope

In scope: the Codayak application, its installer, and this repository. Out of scope: the third-party LLM, speech, image and search services Codayak calls on your behalf — report those to the respective vendor.
