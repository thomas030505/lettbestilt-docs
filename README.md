# LettBestilt API docs

Source for [docs.lettbestilt.no](https://docs.lettbestilt.no), built with [Fern](https://buildwithfern.com).

```
fern/
  docs.yml            site config: navigation, colors, logo, domain
  generators.yml      points Fern at the OpenAPI spec
  openapi/openapi.json  the public API contract (copied from the platform)
  pages/              guides (MDX)
  assets/             logo and favicon
```

## Run locally

```bash
npm install -g fern-api
fern check
fern docs dev
```

## Publish

Every push to `main` publishes through `.github/workflows/publish-docs.yml`. It needs the `FERN_TOKEN` repository secret (create it with `fern token`).

## Updating the API reference

`fern/openapi/openapi.json` is a copy of the spec served by the platform at `/api/v1/openapi.json`. When the API changes, copy the new spec here. The only intended difference is `servers`, which points to `https://www.lettbestilt.no`.
