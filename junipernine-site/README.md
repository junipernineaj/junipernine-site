# junipernine.com

Static site for junipernine.com, built with [Astro](https://astro.build) and hosted on Cloudflare Pages. It's plain HTML at build time, so nothing runs on the home server.

## Run it locally

Requires Node.js 20 or later.

```bash
npm install
npm run dev
```

Then open http://localhost:4321.

To build a production copy into `dist/`:

```bash
npm run build
npm run preview
```

## Where things live

- `src/styles/global.css`: colours, fonts and layout. Change the values at the top to restyle the whole site.
- `src/layouts/Base.astro`: header navigation and footer, shared by every page.
- `src/pages/`: one file per page. The URL follows the file path, so `src/pages/services/observability.astro` becomes `/services/observability/`.
- `src/pages/index.astro`: the home page, including the list of services.
- `astro.config.mjs`: the site URL, used for sitemaps and canonical links.

## Editing content

Each page is plain text inside an `<Base>` tag. Edit the words directly. To add a service, copy one of the files in `src/pages/services/`, change the title and text, and add a link to it in `src/pages/services/index.astro` and `src/pages/index.astro`.

## Deploying to Cloudflare Pages

1. Push this repository to GitHub.
2. In the Cloudflare dashboard, go to Workers & Pages → Create → Pages → Connect to Git, and select the repository.
3. Use these build settings:
   - Framework preset: Astro
   - Build command: `npm run build`
   - Build output directory: `dist`
4. Save and deploy. Every push to `main` deploys automatically.
5. Under the project's Custom domains, add `junipernine.com` and `www.junipernine.com`.

The apex domain `junipernine.com` is served from Pages, not from the home server, so it stays up when the server is off. The recipe and photo apps stay on their own subdomains through the tunnel.

## Things to check before going live

- Replace `you@junipernine.com` with the real address in `src/layouts/Base.astro` and `src/pages/contact.astro`.
- Check the GitHub link in the footer.
- The Apps page links to `recipes.junipernine.com`. Its Cloudflare Access policy should stay in place.
