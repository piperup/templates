---
description: "GitHub Copilot Markdown authoring instructions"
applyTo: "**/*.md"
---

## Goal

You are assisting in creating, improving, or maintaining Markdown (`.md`) files.
Your sole focus is to generate **clear, properly formatted Markdown** that follows best practices for documentation and readability.

## General Guidelines

- Always output **valid Markdown syntax**.
- Avoid any programming code unless it’s inside fenced code blocks.
- Never include HTML unless explicitly requested.
- Ensure consistent heading hierarchy (`#`, `##`, `###`, etc.).
- Maintain proper spacing:
  - Blank line **after each heading**.
  - Blank line **before and after lists, code blocks, and blockquotes**.
- Use proper list markers:
  - `-` for unordered lists.
  - `1.` for ordered lists.
- Prefer readability over compactness.

## Structure

When creating a new Markdown file:

1. Start with a **top-level heading** (`# Title`).
2. Follow with a short **summary paragraph**.
3. Use subsections with `##` for major sections.
4. Use `###` or deeper levels only when necessary.
5. Add code examples using fenced blocks with proper language tags:

```language
code here
```

6. End with a **conclusion** or **next steps** section if appropriate.

## Formatting Rules

- Bold: `**text**` for emphasis.
- Italic: `_text_` for subtle emphasis.
- Inline code: `` `code` ``.
- Blockquotes: `> text`.
- Links: `[label](url)`.
- Images: `![alt text](path_or_url)`.

## Tone & Style

- Use **concise**, **instructional**, and **neutral** language.
- Avoid first-person phrasing (no "I" or "we").
- Prefer imperative style (e.g., “Run this command”, “Add this section”).
- Maintain consistent capitalization for headings.
- Include examples when useful.

## What Not to Do

- Do not output plain text outside of Markdown format.
- Do not generate HTML or other markup languages.
- Do not include explanation about how Markdown works unless requested.
- Do not output ChatGPT-style commentary or metadata.

**Example Output Template**

````markdown
# Example Title

A short description of what this document covers.

## Section 1

Clear, readable content here.

- Key point 1
- Key point 2

## Section 2

Here’s an example code block:

```bash
npm install
```
````
