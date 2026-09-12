# JanitorAI Script Lab

A free, single-file tool for writing, testing, and debugging **JanitorAI Advanced Scripts** and **Lorebook Activation scripts** — entirely in your browser, with no install and no sign-up.

**[Open the live tool →](https://10010011011.github.io/Janitorai-script-lab/)** *(replace with your GitHub Pages link once published — see below)*

Made by [S-101 (link to janitorai profile)](https://janitorai.com/profiles/1df4ba6c-d08b-4557-a522-459820ab9ee1_profile-of-s-101) on JanitorAI.

## Why this exists

JanitorAI runs your script inside a locked-down sandbox. If something goes wrong in there, it usually just **fails silently** — no error, no console, nothing. You're left guessing why your character's script "isn't doing anything."

This tool rebuilds that sandbox in your browser so you can actually see what's happening:

- **Analyze** — instant static checks: syntax errors, blocked globals, risky patterns, schema mistakes, and common JanitorAI-specific pitfalls.
- **Run Test** — actually executes your script against a simulated chat, so you can catch bugs that only show up at runtime.
- **Chat Sim** — type real messages and watch your script fire on each simulated bot turn.
- **Full Test** — runs a multi-turn soak test plus any scenarios you've written, and builds a shareable report.
- **One-click fixes** — a handful of common mistakes (smart quotes, `.length()`, `parseInt` without a radix, `== NaN`, and a few others) can be fixed automatically with a single click, with a before/after preview and one-click undo.

It works fully offline after the page loads — no data is sent anywhere, nothing is uploaded, and nothing is tracked.

## Who it's for

- **JanitorAI bot/character creators** who write Advanced Scripts or Lorebook activation logic and want to catch mistakes before publishing.
- **People new to JavaScript** — findings are explained in plain language, with a one-click fix where possible, so you don't need to already know what's wrong to fix it.
- **More experienced scripters** who want a fast, transparent way to lint and stress-test a script without leaving the browser.

## Getting started

1. Open the tool (link above, or open `index.html` locally in any modern browser).
2. Paste your script into the editor, or click **Examples** to load a sample.
3. Click **Analyze** to check it, or **▶ Run Test** to also execute it.
4. Fix what comes up — click ⚡ **Apply fix** on anything that offers it, or read the plain-language explanation for anything that needs a manual change.
5. Use **Chat Sim** to simulate a real conversation, and **🧪 Full Test** when you want a full report before publishing.

Works on both desktop and mobile browsers.

## What's inside

This is a **single HTML file** — no build step, no dependencies, no server. Everything (editor, sandbox, analyzer, test runner) lives in one file so it's easy to host, fork, or run offline.

- `index.html` — the entire tool.
- No external requests are made once the page has loaded, other than the JanitorAI schema/macro reference baked into the file (see **Docs → Sources** inside the tool for what that's based on).

## Running it locally

No build tools needed. Either:

- Double-click `index.html` to open it directly in your browser, or
- Serve the folder with any static file server, e.g. `python3 -m http.server` and visit `http://localhost:8000`.

## Hosting your own copy (GitHub Pages)

1. Fork or download this repo.
2. In your repo, go to **Settings → Pages**.
3. Under **Build and deployment**, set **Source** to `Deploy from a branch`, pick your default branch and the `/ (root)` folder.
4. Save — GitHub will give you a URL like `https://yourusername.github.io/your-repo-name/`.

## Accuracy & limitations

This tool aims to be honest about what it does and doesn't know:

- Syntax errors come straight from the browser's own JavaScript engine — these are always accurate.
- Field/schema checks are based on a schema extracted from JanitorAI's app, kept in the **Docs** tab inside the tool along with its sources.
- Heuristic findings (style/pattern-based warnings) are labeled with a confidence level and are cross-checked against runtime behavior where possible — a finding marked "confirmed at runtime" was actually reproduced; one marked "static analysis" wasn't triggered in that run.
- It cannot verify anything that depends on JanitorAI's actual live servers, moderation systems, or model behavior — only what your script itself does.

Before each release, the analyzer and auto-fix engine are run against real scripts — community templates from the [Tydorius JanitorAI_Scripts repo](https://github.com/Tydorius/JanitorAI_Scripts) and official examples from JanitorAI's own help center — not just short synthetic test cases. This has caught real false positives (safe, common patterns wrongly flagged) and real bugs in the auto-fix engine itself, all documented in the [changelog](CHANGELOG.md).

If something looks wrong or a check seems to misfire, please open an issue (see below) — this is a community tool and corrections are welcome.

## Contributing

Issues and pull requests are welcome — bug reports, new example scripts, additional lint rules, or clearer explanations are all useful. Please open an issue first for anything larger than a small fix, so we can talk through the approach.

## Related resources

- [JanitorAI Scripts Centralized Repository](https://fcgod.github.io/JanitorAI-Scripts-Centralized-Repository/) — a broader collection of community scripts and documentation.

## License

MIT — see [LICENSE](LICENSE). Free to use, copy, modify, and share, including for your own fork of this tool.

## Disclaimer

This is an independent, unofficial community project. It is not affiliated with, endorsed by, or supported by JanitorAI. "JanitorAI" is referenced only to describe compatibility with its scripting system.
