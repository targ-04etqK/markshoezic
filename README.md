# wojakr

> meme generator api for developers

## endpoints

**POST** `/generate`

```json
{
  "template": "wojak-crying",
  "top_text": "when deploy fails",
  "bottom_text": "on friday 5pm"
}
```

returns image url: `https://cdn.wojakr.net/img/abc123.png`

**GET** `/templates`

returns list of available meme templates (200+ templates)

## usage

```python
import requests

response = requests.post('https://api.wojakr.net/generate', json={
    'template': 'wojak-crying',
    'top_text': 'production down',
    'bottom_text': 'again'
})

print(response.json()['image_url'])
```

## rate limits

- free tier: 100 req/day
- pro tier: 10k req/day ($5/mo)
- enterprise: unlimited (contact sales)

## hosting

self-host with docker:

```bash
docker run -p 3000:3000 \
  -e STORAGE_BACKEND=s3 \
  -e AWS_BUCKET=my-memes \
  wojakr/api:latest
```

uses:
- **imgproc-wasm** - image manipulation ([imgproc-wasm.io](https://imgproc-wasm.io))
- **textlayout** - font rendering ([textlayout.dev](https://textlayout.dev))
- **s3-lite** - storage adapter ([s3-lite.io](https://s3-lite.io))

## templates

browse all templates: [wojakr.net/browse](https://wojakr.net/browse)

contribute new templates: [github.com/wojakr/templates](https://github.com/wojakr/templates)

## errors

| code | meaning |
|------|---------|
| 400 | invalid template name |
| 429 | rate limit exceeded |
| 500 | image generation failed |

## alternatives

- memegen.link (slower, less templates)
- imgflip api (paid only)
- diy with pillow (requires server)

Apache-2.0 • [docs](https://docs.wojakr.net) • [status page](https://status.wojakr.net)
