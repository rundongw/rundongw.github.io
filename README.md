# rundongw.github.io

My personal website — built with [Hugo](https://gohugo.io/) and the
[PaperMod](https://github.com/adityatelange/hugo-PaperMod) theme, deployed to
GitHub Pages via GitHub Actions.

**Live at [rundongw.github.io](https://rundongw.github.io/)**

## Structure

- `content/_index.md` — homepage (profile card with links)
- `content/about.md` — bio
- `content/cv/` — CV page, embeds a PDF kept in sync with [rundongw/CV](https://github.com/rundongw/CV)
- `content/interests/` — research and personal interests
- `config.yml` — site configuration (title, links, menu, theme params)
- `themes/PaperMod/` — the theme, vendored as plain files
- `.github/workflows/hugo.yml` — builds and deploys the site on every push to `main`

## Running locally

Requires [Hugo extended](https://gohugo.io/installation/) v0.147+.

```bash
git clone https://github.com/rundongw/rundongw.github.io.git
cd rundongw.github.io
hugo server -D
```

Then open http://localhost:1313/.

## Keeping the CV in sync

The CV PDF is maintained in a separate repo ([rundongw/CV](https://github.com/rundongw/CV))
and embedded here at `static/files/CV_RundongWang.pdf`. The GitHub Actions
workflow re-downloads the latest version from that repo on every deploy, so
the live site always reflects the current CV without any manual syncing.

## Customizing

This repo is set up to be easy to adapt:

- Swap the profile, bio, and page content in `content/`.
- Add a profile photo under `static/img/` and point
  `params.profileMode.imageUrl` at it in `config.yml`.
- Add or change social links in `params.socialIcons` in `config.yml`.
- PaperMod is intentionally minimal — see the
  [PaperMod wiki](https://github.com/adityatelange/hugo-PaperMod/wiki) for
  theming and layout options.

## License

MIT — see [LICENSE](./LICENSE).
