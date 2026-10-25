# SATIT Glory League

SATIT Glory League is hosted at the existing GitHub Pages URL:

- Public site: https://wictorz.github.io/football-league/
- Persistent API and D1 database: https://satit-glory-league.ewikzorpc.workers.dev

GitHub Pages serves the static HTML and team badges from this repository. Cloudflare Workers serves the API and D1 data. The browser app is configured to call that Worker API from `https://wictorz.github.io`, with credentialed CORS and partitioned HttpOnly admin-session cookies.

## Cloudflare setup

The existing D1 ID is already in `wrangler.jsonc`. From the repository root, use Node.js 20+ and Wrangler:

```sh
npm install
npx wrangler login
npm run db:migrate:remote
npx wrangler secret put ADMIN_PASSWORD
npm run deploy
```

The Worker name in `wrangler.jsonc` must remain `satit-glory-league`. Enter an Admin password of at least 16 characters when Wrangler prompts for the secret. Never commit the secret.

After the Worker is deployed, GitHub Pages continues to serve the UI at the URL above. For automatic Worker builds, connect this repository under Cloudflare Workers & Pages > Settings > Builds.

## Local development

```sh
npm install
npm run db:migrate:local
npm run dev
```

Local development uses Wrangler's local D1 database. Production data remains in the configured remote D1 database.

