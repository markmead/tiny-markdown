# Tiny Markdown

Tiny Markdown is a fast, single-file markdown editor with live preview.

![](https://tiny-markdown.mm-dev.workers.dev/cover.jpg)

## What It Does

- Writes markdown with toolbar shortcuts.
- Renders live preview safely with HTML sanitization.
- Ticks task list checkboxes in the preview, writing back to the source.
- Keeps the editor and preview scrolled together.
- Indents with Tab; press Esc first to tab out of the editor.
- Saves revision snapshots to `localStorage`.
- Loads, deletes, and clears saved revisions from the revision menu.
- Copies markdown to clipboard.
- Exports markdown as `.md`.
- Supports dark mode and fullscreen editing.

## Tech Stack

- Alpine JS
- Alpine JS Persist
- Tailwind CSS
- Marked
- DOMPurify
