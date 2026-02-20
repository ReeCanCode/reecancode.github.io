# Blog Guide – Hugo + PaperMod

A single reference for writing, publishing, and managing this blog.

---

## 1. Creating a New Post

**Command:**

```bash
hugo new posts/my-post-name.md
```

This creates `content/posts/my-post-name.md` with default front matter (date, draft, title). Use a slug-style name (lowercase, hyphens).

**Front matter fields:**

| Field | Description |
|-------|-------------|
| **title** | Display title of the post. |
| **date** | Publish date (e.g. `2026-02-21`). Used for ordering and RSS. |
| **draft** | `true` = not published; `false` = published. Omit or set `false` for live posts. |
| **description** | Short summary for listings, search, and meta description (SEO). |
| **tags** | List of tags (e.g. `["tutorial", "hugo"]`). Shown on the post and on `/tags/`. |
| **categories** | List of categories (e.g. `["Tutorials"]`). One or more; shown on `/categories/`. |
| **featured** | `true` to show the post on the home “Featured” section and on `/featured/`. |
| **cover** | Cover/thumbnail: `cover.image` (path or URL), optional `cover.alt`, `cover.caption`. |
| **author** | Author name (if you use multiple authors or want it in meta). |
| **weight** | Sort order when needed (lower = earlier). Optional. |
| **showToc** | `true` to show table of contents on the post. |
| **tocopen** | `true` to open the TOC by default. |
| **math** | `true` if the post uses LaTeX math (requires theme/config support). |
| **comments** | `true` to enable comments (if configured). |

---

## 2. Front Matter Template

Copy this block into a new post and edit the values:

```yaml
---
# Required
title: "Your Post Title"
date: 2026-02-21
draft: false

# Recommended for SEO and listings
description: "One sentence summary of the post."

# Organization
tags:
  - tag1
  - tag2
categories:
  - CategoryName

# Optional: feature on home and /featured/
featured: false

# Optional: cover image (path from static/ or URL)
cover:
  image: "/images/your-image.jpg"
  alt: "Short description for accessibility"
  caption: "Optional caption below the image"

# Optional
author: "Your Name"
showToc: true
tocOpen: false
math: false
comments: false
---
```

---

## 3. Adding Images to a Post

**Where to store images:**

- **Global:** `static/images/` – reference as `/images/filename.jpg`. Good for shared assets (e.g. placeholders, logos).
- **Post bundle:** Create a folder `content/posts/my-post/`, put `index.md` and image files there; reference with `.Params.cover.image` or shortcodes using the filename. Good for post-specific images.

**Basic image (Markdown):**

```markdown
![Alt text](/images/photo.jpg)
```

**Image with caption (shortcode):**

```html
{{< figure src="/images/photo.jpg" alt="Description" caption="Caption below the image." >}}
```

**Cover/thumbnail for the post:** Set in front matter:

```yaml
cover:
  image: "/images/cover.jpg"
  alt: "Cover description"
  caption: "Optional caption (shown on single page)"
```

**Resize/align:** Use the `figure` shortcode with optional params:

```html
{{< figure src="/images/photo.jpg" alt="Desc" width="400" align="center" >}}
```

Align: use `align="center"` in the shortcode if supported; or wrap in a div with CSS.

---

## 4. Adding Code Blocks

**Fenced code with language:**

````markdown
```python
def hello():
    print("Hello")
```
````

**Filename label:** PaperMod/Chroma don’t add a filename by default. You can add a comment at the top of the block or use a shortcode if the theme provides one.

**Highlight specific lines:** With Hugo’s `highlight` shortcode (if enabled):

```html
{{< highlight python "linenos=table,hl_lines=2 4" >}}
code here
{{< /highlight >}}
```

---

## 5. Adding Other Elements

**Blockquotes:**

```markdown
> Quoted text.
```

**Tables:**

```markdown
| A   | B   |
|-----|-----|
| One | Two |
```

**Callout / note (collapse shortcode):**

```html
{{< collapse summary="**Note:** Title" >}}
Content here.
{{< /collapse >}}
```

**YouTube embed:** Use the theme’s YouTube shortcode if available (e.g. `{{< youtube ID >}}`). Check the theme docs.

**Twitter/X embed:** Theme may provide a shortcode or use Twitter’s embed code in a `rawhtml` shortcode if enabled.

**Internal link (another post):**

```markdown
[Link text](/posts/other-post/)
```

**External link (new tab):**

```markdown
[Link](https://example.com){target="_blank" rel="noopener noreferrer"}
```

Or in HTML: `<a href="..." target="_blank" rel="noopener noreferrer">...</a>`.

---

## 6. Using Categories and Tags

**Difference:**

- **Categories:** Broad sections (e.g. Tutorials, Meta, General). Usually one or two per post. Shown on `/categories/`.
- **Tags:** Many specific keywords (e.g. hugo, markdown, code). Shown on `/tags/`.

**In front matter:**

```yaml
tags:
  - tag1
  - tag2
categories:
  - CategoryName
```

**Naming:** Use consistent, lowercase-with-hyphens for tags; Title Case for categories if you prefer. Avoid special characters and spaces.

---

## 7. Featured Posts

- In front matter set **`featured: true`**.
- The post then appears in the “Featured” block on the home page and on the **[/featured/](/featured/)** page.

---

## 8. Draft Posts

- Set **`draft: true`** in front matter. The post won’t be built in production.
- **Preview drafts locally:**  
  `hugo server -D`  
  Drafts are visible at the local URL.
- **Publish:** Change to **`draft: false`** (or remove the line) and save. The next build will include the post.

---

## 9. Local Development

- **Start server:**  
  `hugo server`
- **URL:** Usually **http://localhost:1313/** (check terminal output).
- **Hot reload:** Editing content or layouts triggers an automatic refresh in the browser.

---

## 10. Publishing a New Post

1. **Write the post** in `content/posts/` and set `draft: false`.
2. **Test locally:** `hugo server` and open the site.
3. **Git:**
   ```bash
   git add content/posts/your-post.md
   git commit -m "Add: your post title"
   git push origin main
   ```
4. **Deploy:** The GitHub Actions workflow runs on push to `main`, builds with Hugo (extended), and deploys to GitHub Pages. Deployment usually finishes within 1–2 minutes.

---

## 11. Folder Structure Reference

| Folder | Purpose |
|--------|---------|
| **content/** | All content: `posts/`, `about.md`, `search.md`, `featured.md`, etc. |
| **static/** | Files served as-is: images, PDFs, favicon. e.g. `static/images/`. |
| **assets/** | Processed assets (CSS, JS). e.g. `assets/css/extended/custom.css`. |
| **layouts/** | Override theme layouts and partials: `index.html`, `_default/featured.html`, `partials/extend_head.html`. |
| **themes/PaperMod/** | Theme files. Do not edit; override in project root. |
| **config** | Site config: `hugo.toml` (or `config.yaml`). Menu, params, outputs, etc. |

---

## 12. SEO Tips

- **description:** Set a clear, short `description` in front matter for each post. Used in meta description and listings.
- **Cover image:** Set `cover.image` so Open Graph and Twitter cards use it when the post is shared.
- **Canonical URLs:** Hugo and PaperMod output canonical URLs by default. Override only if needed with `canonicalURL` in front matter.
