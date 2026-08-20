# rundongw.github.io

Personal website, built with [Hugo](https://gohugo.io/) and the
[PaperMod](https://github.com/adityatelange/hugo-PaperMod) theme, deployed
to GitHub Pages via GitHub Actions.

## Structure

- `content/_index.md` — homepage (profile card with links)
- `content/about.md` — longer bio
- `content/cv/` — CV page, embeds the PDF in `static/files/CV_RundongWang.pdf`
- `content/blog/` — blog posts
- `content/interests/` — research + personal interests
- `config.yml` — site configuration (title, links, menu, theme params)
- `themes/PaperMod/` — the theme, vendored as plain files (not a git submodule)
- `.github/workflows/hugo.yml` — builds and deploys the site on every push to `main`

## First-time setup (this folder isn't a git repo yet)

Requires [Hugo extended](https://gohugo.io/installation/) (this site was built
against v0.147.9) and Git.

The PaperMod theme is already vendored in `themes/PaperMod` (plain files, not
a git submodule) — no extra download step needed.

```bash
cd personal_website   # this folder
git init -b main
git add -A
git commit -m "Initial commit"
```

Then create an empty repo on GitHub named exactly `rundongw.github.io`
(no README/license/gitignore — this folder already has them), and:

```bash
git remote add origin https://github.com/rundongw/rundongw.github.io.git
git push -u origin main
```

Finally, in the new repo's **Settings → Pages**, set **Source** to
**GitHub Actions**. The included workflow (`.github/workflows/hugo.yml`) will
build and deploy the site automatically — it'll be live at
`https://rundongw.github.io/` a minute or two after the push.

## Local preview

```bash
hugo server -D
```

Then open http://localhost:1313/.

## Adding a blog post

```bash
hugo new blog/my-post-title.md
```

Edit the new file under `content/blog/`, then flip `draft: false` when it's
ready to publish. Pushing to `main` triggers the GitHub Actions workflow,
which builds the site and deploys it to Pages automatically.

### The blog is unlisted, not private

There's no "Blog" link anywhere in the nav or homepage buttons anymore.
Instead, typing a secret word anywhere on the site sends you to `/blog/` —
see `layouts/_partials/extend_footer.html` (the word is set in the
`secretWord` variable near the top, currently `"storm"`; change it to
whatever you like).

Keep in mind this is an easter egg, not real access control: the blog is
still a public page at `/blog/` once the site is deployed — anyone with the
direct link (or who reads the page source / this README) can reach it. It
just isn't advertised anywhere on the site itself.

## Keeping the CV in sync

Your CV lives in a separate repo ([rundongw/CV](https://github.com/rundongw/CV))
so you only maintain the PDF in one place. The CV page here embeds a local
copy at `static/files/CV_RundongWang.pdf` — same-origin embedding is what lets
the PDF actually render inline on the page, rather than just linking out to
GitHub (browsers block PDFs from being framed cross-origin).

Two things keep that local copy fresh:

- **On every deploy**, the GitHub Actions workflow downloads the latest PDF
  from the CV repo into `static/files/` before building, so the live site
  always shows the current version — you never have to update it here by hand.
- **For local preview**, a copy is committed directly in this repo (so
  `hugo server -D` has something to embed offline). After you update the CV
  repo, you can refresh this local copy too:

  ```bash
  curl -L "https://raw.githubusercontent.com/rundongw/CV/main/CV_RundongWang.pdf" \
    -o static/files/CV_RundongWang.pdf
  ```

  This step is optional — skip it and the deployed site will still be correct,
  only your local preview will show the older committed copy until you pull
  the fresh one.

## Customizing

- Add a profile photo: drop an image under `static/img/` and set
  `params.profileMode.imageUrl` in `config.yml` to its path (e.g. `/img/me.jpg`).
- Add more links/social icons: edit `params.socialIcons` in `config.yml`.
- Change colors/fonts: PaperMod is intentionally minimal; see the
  [PaperMod wiki](https://github.com/adityatelange/hugo-PaperMod/wiki) for
  supported customization options.
