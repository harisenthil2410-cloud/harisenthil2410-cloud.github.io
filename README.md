# Haripriya S — portfolio & project blog (Jekyll)

This is a full rebuild of your GitHub Pages site as a real Jekyll blog: a homepage with a
"project status board," a `/projects/` log (one post per project, newest first), and a
`/studies/` page for your academic background and certifications. Every post lives as its
own Markdown file in `_posts/`, so adding a new project later is just adding one new file.

## How to add this to your existing repo

Your current repo (`harisenthil2410-cloud.github.io`) already has `profile.jpeg` and
`resume.pdf` at the root — **keep both**, this site links to them directly.

1. Copy everything in this folder into the root of your repo, **except** don't overwrite
   `profile.jpeg` or `resume.pdf` if you already have them there.
2. If your repo currently has a `README.md` being used as the homepage content, delete or
   rename it — this project ships its own `index.md` as the homepage.
3. If there's an existing `_config.yml` in your repo with a `theme:` line (e.g.
   `jekyll-theme-minimal`), remove it — this site uses its own custom layouts in
   `_layouts/` and `_includes/`, not a theme gem.
4. Commit and push. GitHub Pages will build automatically — check the **Actions** tab (or
   **Settings → Pages**) for the build status. First build can take a minute or two.

## Adding a new project later

Create a new file in `_posts/` named `YYYY-MM-DD-your-project-slug.md`:

```yaml
---
title: "Project Title"
dek: "One-sentence hook — what it does and why it's interesting."
status: completed        # or: ongoing
type: "Mini project"     # or: "Team dissertation project", etc.
tags: [Tag One, Tag Two]
images:
  - src: /assets/images/projects/your-project/photo.jpg
    caption: "What this photo shows"
report_pdf: /assets/docs/your-report.pdf   # optional
demo_url: https://...                       # optional
video_url: https://...                      # optional
github_url: https://...                     # optional
---

Your write-up in Markdown goes here.
```

Drop any images in `assets/images/projects/<slug>/` and any PDF reports in `assets/docs/`,
then reference them with the paths above. That's it — it'll show up on the homepage,
`/projects/`, and get its own page automatically.

## Local preview (optional)

If you have Ruby installed:

```bash
bundle install
bundle exec jekyll serve
```

Then open `http://localhost:4000`. If you don't want to install Ruby locally, just push to
GitHub — Pages builds it for you.

## What's already in here

- 7 projects logged: water quality monitoring, Smart Warehouse Security (Renesas), 8051
  first-fault identification, slow-start motor circuit, LM380 audio amplifier, bidirectional
  shift register, and the light/rain automation window.
- A couple of posts mention "I recorded a demo video" without a link (first-fault ID, LM380
  amp) — add `video_url: https://...` to those two files' front matter once you've uploaded
  them (e.g. to YouTube or Drive).
- Dates on the four mini-projects without a certificate/report to pin down an exact date
  (audio amp, shift register, rain automation, slow-start circuit) are estimated in a
  reasonable order — rename the files (`YYYY-MM-DD-...`) if you want to correct them.
