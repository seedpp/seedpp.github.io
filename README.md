# Seed Publications Program — website

A static site for the Seed Publications Program: a non-profit initiative that
coaches young Vietnamese scholars through writing and publishing their first international
review paper.

Everything needed to render the page lives in `index.html` — HTML, CSS, JavaScript, and both
portrait photos embedded as base64. Open it anywhere and it works, with no folder next to it.
No build step and no dependencies; the only external request is the Google Fonts stylesheet.

`images/` holds the same three photos as ordinary files. The page does not need them, but they
are useful as the originals, and `og:image` points at one of them so shared links show a
thumbnail.

```
index.html
images/
  an-nguyen.jpg
  dan-tong.jpg
  phu-nguyen.jpg
README.md
```

## Put it online with GitHub Pages

1. Create a new repository on GitHub (public).
2. Upload `index.html` and the `images/` folder to the repository root, keeping the folder
   structure above. Add this `README.md` too if you want.
3. Go to **Settings → Pages**.
4. Under **Build and deployment → Source**, choose **Deploy from a branch**.
5. Set branch to `main` and folder to `/ (root)`, then **Save**.
6. Wait about a minute. The site appears at `https://<your-username>.github.io/<repo-name>/`.

To use a custom domain later, add it under **Settings → Pages → Custom domain** and create
the matching DNS records at your registrar.

## Editing the content

| What you want to change | Where to look in `index.html` |
| --- | --- |
| Headline, intro paragraph, CTA | `<section ... id="home">` |
| The four counters | the `#counters` block — edit `data-count` on each `<b>` |
| Aim of the project (six cards) | `<section ... id="aim">` |
| Program detail accordion, deadline banner | `<section ... id="program">` |
| Cohort buttons and their pop-up windows | the `COHORTS` array in `<script>` |
| Publications, under review, in progress | `<div class="pubs" id="pubs">` — each `<article>` has `data-status="pub \| rev \| prog"` |
| Program history and name history | `<div class="history-block">` |
| Team cards and personnel-file data | `<article class="person">` — the `data-file`, `data-role`, `data-field`, `data-status`, `data-since` attributes |
| FAQ | `<section ... id="faq">` |
| Colours | the CSS variables at the top: `--seed-cream`, `--seed-gold`, `--seed-orange`, `--seed-crimson`, `--seed-teal` |

### Adding a cohort

Add one object to the `COHORTS` array. The button and its pop-up window are generated from
it, so nothing else needs touching:

```js
{
  id:"K8", tone:"c-soon", flag:"var(--hair)", tag:"Coming",
  title:"K8 — Coming",
  kicker:"Not yet open",
  stats:[],
  text:`<p>K8 is coming. Details will be published here once the cohort is scheduled.</p>`
}
```

Use `tone:"c-now"` with `flag:"var(--seed-teal)"` for an intake that is currently open, and
`tone:"c-exp"` with `flag:"var(--seed-cream)"` once it closes.

### Swapping a team photo

Point that person's `<img class="avatar avatar--photo">` at a new file — `src="images/name.jpg"`
works, as long as the `images/` folder ships with the page. A square image around 420×420 is
the right size: the existing three are that size, which is why they stay sharp in both the
round card avatar and the larger personnel-file view.

Note that all three photos are embedded as base64 inside `index.html`, which is why the page
renders on its own. If you replace them with file paths, `index.html` and `images/` must
then travel together.

## Notes

- The counters show the K1–K4 tally as of 10 August 2026: 103 awardees, 64 topics, 15
  manuscripts in progress, 3 under review, 3 published. Edit `data-count` on each `<b>` in
  the `#counters` block to update them.
- The Publications section lists individual papers, so its tab counts are smaller than the
  counters: only the 2 PROSPERO-registered manuscripts appear under "In progress" out of the
  15 in the tally.
- The application deadline is shown as expired. When a new intake opens, edit the banner in
  the Program detail section and the "How to apply" accordion item.
