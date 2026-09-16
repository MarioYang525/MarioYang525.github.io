---
title: "Example Writeup (delete me)"
date: 2026-09-16
description: "A template post showing how to write posts and attach report files."
---

This is a **template post**. Copy its folder structure when you write your own
posts, then delete it.

## Folder structure

```text
content/writeups/example-writeup/
├── index.md            <- this post (Markdown content)
└── files/              <- any attachments (PDF, MD, zip, images...)
    └── example-report.txt
```

## Writing content

Everything below the front matter is plain Markdown. Code blocks get syntax
highlighting automatically:

```python
print("hello, world")
```

## Attaching files

Every file you put in the `files/` subfolder is **automatically listed** at
the bottom of this page under "Files".

You can also link a file inline, anywhere in the text, with the attachment
shortcode:

{{</* attachment src="files/example-report.txt" title="Full report (MD)" */>}}
