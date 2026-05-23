# Cubbie Assets

Public CSS, fonts, and other web assets for Cubbie's marketing technology integrations. Maintained by [Keystone MarTech](https://keystonemartech.com) (KMT) as part of the Cubbie consulting engagement.

## What's in here

| Path | Purpose |
|------|---------|
| `mautic/form-theme.css` | Styling for Cubbie's Mautic forms. Referenced via `@import` from each form's HTML Area "custom css" field. |

## Why a public repo?

The CSS is served via [jsDelivr](https://www.jsdelivr.com) (free CDN backed by GitHub) so that Mautic forms embedded on cubbie-hub.com can `@import` it. jsDelivr requires public repositories on the free tier. There are no secrets or sensitive logic in this repo — only presentational CSS that's already visible to anyone who inspects the rendered form.

Anything sensitive (workflow JSONs, configs, internal docs) lives in a separate private repo, not here.

## How the Mautic forms use this

Each Cubbie Mautic form has an HTML Area field at order 0 (label: "custom css", show label: no, save result: no). The field's content is a one-liner:

```html
<style>@import url('https://cdn.jsdelivr.net/gh/KeystoneMarTech/cubbie-assets@main/mautic/form-theme.css?v=N');</style>
```

The `?v=N` is a cache-buster. Bump it after each CSS update to force browsers to fetch fresh.

Full architecture, design decisions, and lessons learned: see the companion vault note `PROSPECTS AND CLIENTS/Cubbie/Mautic Assets/Forms/cubbie-contact-form-test.md` (private to KMT).

## Updating the CSS

1. Edit `mautic/form-theme.css` here on github.com (pencil icon), commit on `main`
2. Purge jsDelivr cache:
   ```bash
   curl -s "https://purge.jsdelivr.net/gh/KeystoneMarTech/cubbie-assets@main/mautic/form-theme.css"
   ```
3. Bump `?v=N` to `?v=N+1` in each Mautic form's HTML Area
4. Hard refresh the embed page

**Important:** purge BEFORE bumping the version. If you bump first, jsDelivr can cache stale content under the new URL.

## License

No license specified (default copyright). Files are publicly readable for CDN access but not licensed for reuse. If you're not KMT or Cubbie and want to use anything in here, get in touch.
