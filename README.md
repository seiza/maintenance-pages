# maintenance-pages

Static maintenance pages, served with GitHub Pages and used as the custom
maintenance page of a Heroku app (`MAINTENANCE_PAGE_URL`).

## Pages

| Folder | Purpose |
|---|---|
| [`out-of-service/`](out-of-service/index.html) | The site is permanently out of service |

Each page lives in its own folder, so that any asset it needs can sit next to
its `index.html` and be referenced with a relative path.

## Rules for a page

- Static HTML, self-contained: inline CSS, no external requests (fonts, scripts, analytics).
- Heroku displays it in an iframe: no links without `target="_blank"`.
- `https://` URL only (Heroku asks for the app and the page to use the same protocol).

## Use with Heroku

Two equivalent ways: the CLI or the Heroku dashboard.

### With the CLI

```bash
heroku config:set MAINTENANCE_PAGE_URL=https://<account>.github.io/maintenance-pages/out-of-service/index.html -a <app>
heroku maintenance:on -a <app>
```

Back to normal: `heroku maintenance:off -a <app>`.

### With the Heroku dashboard

Open the app, then its **Settings** tab:

1. **Config Vars**: click *Reveal Config Vars*, then add a variable named
   `MAINTENANCE_PAGE_URL`, with the page URL as its value (same URL as in the
   CLI example above).
2. **Maintenance Mode** (further down the page): switch the toggle on; it then
   reads "Maintenance mode is on". Switch it off to go back to normal.

Do not use a `raw.githubusercontent.com` or `github.com/.../blob/...` URL: they
are not served as a web page.
