# Jan Burczak — personal website (Markdown / Jekyll)

Content lives in six Markdown files. GitHub turns them into the website automatically —
no software to install, nothing to build on your computer.

```
_config.yml        name, email, address, photo, CV file, the top menu
index.md           home page
research.md        research
publications.md    publication list
talks.md           talks & visits
teaching.md        teaching, supervision, service
cv.md              positions, education, grants, contact
assets/style.css   all styling (colours are at the top)
assets/            put photo.jpg and BurczakCV.pdf here
_layouts/          page frame (header, menu, footer) — rarely touched
```

---

## Part 1 — Putting this into your existing GitHub repository

**Important: the old files must be deleted, not just added to.** If an old `index.html`
stays in the repo, GitHub will keep showing it instead of the new `index.md`.

### The easy way (browser only)

1. Open your repository on github.com.
2. **Delete the old site files.** For each old file: click it → the "..." menu at the top
   right of the file view → **Delete file** → scroll down → **Commit changes**.
   Delete every old `.html` and `.css` file, and — this one matters — delete
   **`.nojekyll`** if it exists, because that file tells GitHub *not* to build Markdown.
   Keep anything you still want, such as PDFs or images.
3. **Upload the new files.** Click **Add file → Upload files**, then drag in the *contents*
   of this folder (not the folder itself): `_config.yml`, the six `.md` files, and the
   `_layouts` and `assets` folders. Commit.
4. Wait about a minute. Your site rebuilds by itself. If something in the Markdown is
   malformed, GitHub emails you and the **Actions** tab shows a failed "pages build and
   deployment" — the old version stays live until the new one builds cleanly.

Note: browsers can be fussy about dragging folders. If `_layouts` or `assets` won't drag,
upload the loose files first, then use **Add file → Create new file** and type
`_layouts/default.html` as the name — GitHub creates the folder for you — and paste the
contents in. Same for `_layouts/home.html` and `assets/style.css`.

### The git way, if you prefer the terminal

```bash
git clone https://github.com/USERNAME/REPO.git
cd REPO
git rm -r *.html *.css .nojekyll        # remove the old site (ignore errors for files that don't exist)
cp -r /path/to/this/folder/. .          # copy the new site in
git add -A
git commit -m "Rebuild site with Jekyll"
git push
```

### Two settings to check once

- **Settings → Pages**: source should be "Deploy from a branch", branch `main`,
  folder `/ (root)`.
- **`_config.yml`, the `baseurl` line**: if your site's address is
  `https://USERNAME.github.io` leave it as `baseurl: ""`. If it is
  `https://USERNAME.github.io/REPO/` then set `baseurl: "/REPO"`.

---

## Part 2 — Editing, day to day

Click any `.md` file on github.com, click the pencil icon, edit, and commit. The site
rebuilds in about a minute. Everything below is the entire syntax you need.

### Add a paper

Open `publications.md` and copy an existing line to the top:

```
1. **Title of the paper** (with A. Coauthor) — Journal Name 12 (2027), 1–20
```

Every line starts with `1.` — that is not a mistake. The numbers are generated, counting
down from the newest, so adding a paper never means renumbering anything. `**bold**` is
the title, `*italic*` is emphasis, `[text](https://link)` is a link.

### Add a talk, a course, a position, a grant

These are all the same shape: a date line, then a line starting with a colon and a space.
Leave a blank line between entries.

```
May 2027
: *Name of the Conference*, City, Country. Talk: Title of my talk
```

### Add a section

A line starting with `## ` is a section heading. `### ` is a sub-heading.

### Change your name, email, address, menu

All in `_config.yml`.

### Add your photo

Upload the image into `assets/`, then in `_config.yml` set:

```
photo: assets/photo.jpg
```

Until you do, a grey placeholder appears. Same idea for the CV: upload
`assets/BurczakCV.pdf` and the "CV (PDF)" links start working.

### Change colours or spacing

`assets/style.css`, the block at the very top:

```css
--accent: #7a2f2f;    /* the deep red used for links */
--bg: #fbfbf9;        /* page background */
```

### One optional trick

`*JEMS, to appear*{: .venue}` renders that bit small and grey. Plain `*italics*` works
fine too if you'd rather not bother.

---

## Previewing before you publish

You don't need to. Commit, wait a minute, look at the live site; if you dislike it, GitHub
keeps every previous version and you can revert a commit in two clicks. If you ever *do*
want a local preview, that's when you'd install Ruby and Jekyll — not before.
