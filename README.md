# Qwik + Vercel without the Edge

## Steps to deploy Qwik on Vercel without the Edge

1. Add Express adapter to your Qwik app

```bash
pnpm qwik add express
```

2. Create `api/index.js` file to the root of your project and add the following code:

```javascript
export * from '../server/entry.express.js';
```

3. Add `vercel.json` file to the root of your project with the following content:

```json
{
  "rewrites": [
    {
      "source": "/(.*)",
      "destination": "/api"
    }
  ],
  "headers": [
    {
      "source": "/build/(.*)",
      "headers": [
        {
          "key": "Cache-Control",
          "value": "public, max-age=31536000, s-maxage=31536000, immutable"
        }
      ]
    }
  ]
}
```
