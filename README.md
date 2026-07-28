# Amine Security Jekyll Blog

A dark neon cybersecurity portfolio/blog built with Jekyll for GitHub Pages.

## Structure

- `_posts/` - blog posts. Jekyll requires filenames like `2026-06-18-my-post.md`.
- `_writeups/` - CTF and Hack The Box writeups.
- `_notes/` - notes, cheatsheets, commands, and checklists.
- `_projects/` - portfolio projects.
- `_layouts/` - page templates.
- `_includes/` - reusable pieces like navigation and cards.
- `assets/css/main.css` - the dark neon security theme.
- `assets/images/` - logos and thumbnails.

## Run Locally

```bash
bundle install
bundle exec jekyll serve
```

Open `http://127.0.0.1:4000/amine-cyber-blog-v2/`.

## GitHub Pages

This site is configured for a project repository:

```yml
baseurl: "/amine-cyber-blog-v2"
```

If your repository name is different, update `baseurl` in `_config.yml`.

If you deploy as `https://yourusername.github.io/`, set:

```yml
baseurl: ""
```

## Add A Blog Post

Create a file in `_posts/`:

```md
---
title: "My New Blog Post"
description: "Short summary shown on cards."
date: 2026-06-18
reading_time: "4 min read"
tags: ["learning", "web"]
---

Write your post here.
```

Filename example:

```text
_posts/2026-06-18-my-new-blog-post.md
```

## Add A Writeup

Create a file in `_writeups/`:

```md
---
title: "HTB: Machine Name"
description: "One sentence about the attack path."
date: 2026-06-18
platform: "Hack The Box"
difficulty: "Easy"
os: "Linux"
thumbnail: "/assets/images/writeup-cicada.svg"
reading_time: "8 min read"
tags: ["linux", "suid", "web"]
---

## Enumeration

## Foothold

## Privilege Escalation

## Lessons Learned
```

URL example: `_writeups/machine-name.md` becomes `/writeups/machine-name/`.

## Add A Note

Create a file in `_notes/`:

```md
---
title: "SMB Cheat Sheet"
description: "Commands and checks for SMB enumeration."
date: 2026-06-18
area: "Enumeration"
tags: ["smb", "windows", "recon"]
---

Add commands, reminders, and examples here.
```

## Add A Project

Create a file in `_projects/`:

```md
---
title: "Detection Lab"
description: "Small lab for collecting logs and writing detections."
date: 2026-06-18
status: "Building"
tags: ["lab", "blue-team", "logs"]
repo: "https://github.com/yourusername/detection-lab"
---

Describe the goal, architecture, setup, and what you learned.
```

`repo` is optional.
