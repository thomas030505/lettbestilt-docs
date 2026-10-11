# LettBestilt API docs

Source for [docs.lettbestilt.no](https://docs.lettbestilt.no), built with [Fern](https://buildwithfern.com).

```
fern/
  docs.yml                navigation (Guides and API reference tabs), colors, logo, domain
  generators.yml          points Fern at the spec and the overrides
  openapi/openapi.json    the public API contract, copied from the platform
  openapi/overrides.yml   everything the docs add on top: English text, tags,
                          examples, missing error responses, webhooks
  pages/                  guides (MDX)
  assets/                 logo and favicon
```

## Check and preview

Use the pinned CLI version:

```bash
npx fern-api@5.152.2 check
npx fern-api@5.152.2 generate --docs --preview   # prints a preview URL
```

## Publish

Every push to `main` publishes through `.github/workflows/publish-docs.yml`. It needs the `FERN_TOKEN` repository secret (create it with `fern token`).

## Updating the API reference

`fern/openapi/openapi.json` is a copy of the spec the platform serves at `/api/v1/openapi.json` (source: `src/app/api/v1/openapi.json/route.ts`). Copy it as it is; never edit it by hand.

All presentation lives in `fern/openapi/overrides.yml`, which Fern merges into the spec: objects are deep-merged, `parameters` are matched by `in` and `name`, other arrays of objects (such as `oneOf`) are merged by index, and arrays of plain values (such as `enum`) are replaced. The overrides also set `servers` to `https://www.lettbestilt.no`.

After copying a new spec, run `fern check` and look through the preview. When the platform spec gets English text, tags or operation IDs of its own, delete the same entries from the overrides.
