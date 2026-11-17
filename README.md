# Requesting a new public trashcan, explained

A four-slide FAQ carousel for Signal Cleveland, to run alongside the public
trash can map.

`index.html` is the whole thing — markup, styles and script in one block, with
no build step and nothing to install.

## Using it

Paste the entire contents of `index.html` into a WordPress **Custom HTML**
block. It is a fragment, not a page: no `<html>`, `<head>` or `<body>`, because
WordPress supplies those.

It inherits the Newspack theme's heading and body fonts through
`var(--newspack-theme-font-heading)` and `var(--newspack-theme-font-body)`,
falling back to Roboto Condensed and Inter, so it picks up the site's
typography wherever it lands.

Everything is scoped under `#faqss`, so it cannot leak styles into the rest of
the page. The script guards on `data-ready`, so it is safe if the block ends up
on a page twice.

## Editing the slides

Each slide is one `div.faqss-slide`:

```html
<div class="faqss-slide" role="group" aria-roledescription="slide" hidden>
  <p class="faqss-q">The question, as a short imperative</p>
  <p class="faqss-a">The answer.</p>
</div>
```

Add or delete slides freely — the "X of Y" counter counts them at run time, and
the arrows disable themselves at each end. Every slide except the first carries
`hidden`; the script sets it on load anyway, so a slide that keeps or loses it
by accident still behaves.

## Before this runs

Slide 2 has unfilled placeholders:

> only **x%** of the city's 2,338 GCRTA stops have a public can within 100
> feet, and **x** stops have no can nearby at all

Both need real figures, which means crossing the receptacle list against GCRTA
stop locations. Those are not in this repo.

## Caveat if you serve this file directly

As a WordPress block this is correct as it stands. Opened on its own — through
GitHub Pages, say — it has no `<!doctype html>`, so browsers fall back to quirks
mode, and no `<meta charset="utf-8">`, so the curly quotes in the copy can come
out as mojibake. That only matters if the file is ever served as a page in its
own right; it would need a wrapper for that.

## Related

The public trash can map that this FAQ accompanies:
https://github.com/eesedla/public-can-locations
