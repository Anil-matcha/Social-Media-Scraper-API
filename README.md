# Social Media Scraper API

Retrieve public social posts by profile or search query through the enabled Muapi endpoints. This guide documents platform-specific inputs and pagination/limit behavior.

[Muapi Social Media Scraper API landing page](https://muapi.ai/social-media-scraper-api) · [API reference](https://muapi.ai/docs/api-reference) · [Create an API key](https://muapi.ai/access-keys)

## Related Projects

- [Social-Media-API](https://github.com/Anil-matcha/Social-Media-API)
- [SEO-API](https://github.com/Anil-matcha/SEO-API)

## What this API covers

Use the endpoint that matches the task and input media. The routes below are enabled Muapi model IDs checked against the current model catalog; availability, request fields, and pricing can change, so verify the linked landing page and endpoint schema before production use.

| Endpoint | Purpose | Category |
|---|---|---|
| `social-read-posts` | Social Read Posts | `Text to Text` |
| `social-search-posts` | Social Search Posts | `Text to Text` |

## Quick start

Muapi uses an asynchronous REST contract. Submit a JSON request with your API key, save the returned `request_id`, then poll the result endpoint. Replace sample URLs with files you control and fields with values supported by the selected endpoint.

```bash
curl -X POST https://api.muapi.ai/api/v1/social-read-posts \
  -H "Content-Type: application/json" \
  -H "x-api-key: $MUAPI_API_KEY" \
  -d '{
    "platform": "tiktok",
    "username": "muapi_ai"
  }'
```

### Request fields in this example

| Field | Requirement | Notes |
|---|---|---|
| `platform` | Optional | Social platform to read posts from. |
| `username` | Optional | Handle/username for tiktok, instagram, linkedin, reddit; Page ID for facebook. |

### Poll for the result

```bash
curl "https://api.muapi.ai/api/v1/predictions/$REQUEST_ID/result" \
  -H "x-api-key: $MUAPI_API_KEY"
```

Poll until the task status is `completed` or `failed`. Read the response’s output URLs on completion; download outputs you need to retain, since provider-hosted URLs may expire.

## Choosing an endpoint

Compare supported inputs and output behavior first, then resolution, duration, quality controls, latency, and price for your use case. Similar names do not guarantee interchangeable request schemas. This repository lists representative routes; the [landing page](https://muapi.ai/social-media-scraper-api) contains the current task-specific explanation, examples, and pricing context.

## Errors and production notes

- Keep the API key in an environment variable; do not commit credentials.
- Validate inputs against the selected endpoint’s current schema.
- Handle non-success HTTP responses and failed task states explicitly.
- Retry only when appropriate for the error; avoid submitting duplicate billable jobs after a timeout without checking the original `request_id`.
- Confirm current pricing and availability on the Muapi page before estimating production cost.

## Links

- [Muapi Social Media Scraper API](https://muapi.ai/social-media-scraper-api)
- [API reference](https://muapi.ai/docs/api-reference)
- [Playground](https://muapi.ai/playground)
- [API key setup](https://muapi.ai/access-keys)
