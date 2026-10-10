# blaselondono.com

My portfolio. Static HTML and one stylesheet, no build step, no JavaScript,
no dependencies. Open `index.html` in a browser and that is the site.

## Layout

```
index.html        front page
projects.html     index of all ten projects
resume.html       PDF embed plus a text version
404.html
style.css         the only stylesheet
img/              photographs and renders
files/            resume and project PDFs
projects/         one page per project
```

## Editing

Each page is self-contained, so the sidebar markup is repeated in each file.
If you change a navigation link, change it everywhere:

```bash
grep -rl 'old-link.html' --include='*.html' .
```

The current page is marked in the sidebar with `class="here"`.

## Adding a project

1. Copy an existing file out of `projects/`.
2. Change the `<title>`, the `<meta name="description">`, the `<h2>`, the deck,
   the spec table and the body.
3. Move `class="here"` onto the new project's own sidebar entry, and add that
   entry to the sidebar in every other page.
4. Add it to `projects.html`, and to `index.html` if it belongs in the
   selected work.

Images go in `img/`. Thumbnails are letterboxed rather than cropped, so a wide
render on a white background works fine as-is.

## Deploying

Pushing to `main` triggers `.github/workflows/pages.yml`, which uploads the
repository as-is to GitHub Pages. There is no build, so what is in the repo is
exactly what is served.

### Custom domain

To point `blaselondono.com` here:

1. At the DNS host for `blaselondono.com`, replace the records currently
   aimed at Google Sites with:

   | Type  | Name  | Value                   |
   |-------|-------|-------------------------|
   | A     | `@`   | `185.199.108.153`       |
   | A     | `@`   | `185.199.109.153`       |
   | A     | `@`   | `185.199.110.153`       |
   | A     | `@`   | `185.199.111.153`       |
   | CNAME | `www` | `blasejlondono.github.io.` |

2. Add a file named `CNAME` at the repository root containing one line:
   `blaselondono.com`
3. In the repository's *Settings -> Pages*, set the custom domain to
   `blaselondono.com` and tick **Enforce HTTPS** once the certificate issues
   (that can take up to an hour after DNS propagates).

Do step 1 before step 2. Adding the `CNAME` file first makes
`blasejlondono.github.io` redirect to a domain that still points at Google
Sites, which makes the new site hard to preview.
