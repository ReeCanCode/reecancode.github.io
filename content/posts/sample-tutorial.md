---
title: "Sample Tutorial"
date: 2026-02-20
draft: false
description: "A sample post with code blocks, image, table, and a callout."
tags:
  - tutorial
  - sample
  - markdown
categories:
  - Tutorials
featured: false
cover:
  image: "/images/placeholder-cover.jpg"
  alt: "Tutorial cover"
showToc: true
tocOpen: true
---

This post shows several elements you can use in your articles.

## Code blocks

Plain code with language:

```python
def greet(name: str) -> str:
    return f"Hello, {name}!"
```

With a filename (Hugo allows this via `highlight` shortcode or code block options; here we show a comment as a label):

```javascript
// utils.js
export function add(a, b) {
  return a + b;
}
```

## Image with caption

Use the `figure` shortcode for an image and caption:

{{< figure src="/images/placeholder-cover.jpg" alt="Sample image" caption="This is a caption below the image." >}}

## Table

| Column A | Column B | Column C |
|----------|----------|----------|
| One      | Two      | Three    |
| Alpha    | Beta     | Gamma    |

## Callout / note

Use the `collapse` shortcode for a note or callout:

{{< collapse summary="**Note:** Important tip" >}}
This is the content inside the collapsible note. Readers can expand it to read more.
{{< /collapse >}}

## Summary

You now have examples of code, images with captions, tables, and callouts. Reuse these patterns in your own posts.
