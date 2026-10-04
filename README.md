# sean.cc

Personal website and writing home base: articles, resume, photography, and fitness.
Built with [Astro](https://docs.astro.build) (blog starter) and deployed to Cloudflare Workers as a static site.

## Run it locally

Requires Node.js 22.12 or newer.

```sh
npm install          # first time, or after package changes
npm run dev          # http://localhost:4321
```

To test the production build the way Cloudflare serves it:

```sh
npx astro build && npx wrangler dev
```

## Deploying

- A push to `main` builds and deploys to https://sean.cc automatically (Cloudflare Workers Builds).
- Pushing any other branch creates a preview build. Use a branch for anything you want to look at before it goes live.
- A failed build does not replace the live site. Build logs: Cloudflare dashboard, Worker `sean-cc`, Deployments.
- `www.sean.cc` redirects to `sean.cc` with a Cloudflare Redirect Rule (not in this repo).

## Working on two Macs

`git pull` before starting, `git push` when done. The repo lives at `~/Code/sean-cc` on each machine, outside iCloud.

## Where things live

| Path | What it is |
| :--- | :--- |
| `src/content/blog/` | Posts (Markdown or MDX) |
| `src/pages/` | Pages; each file becomes a URL |
| `src/components/` | Header, footer, and other shared pieces |
| `src/styles/global.css` | Site-wide styles and the color palette |
| `src/consts.ts` | Site title and description |
| `public/` | Files served as-is (favicon, etc.); images here are not optimized |
| `astro.config.mjs` | Astro settings, including `site: 'https://sean.cc'` |
| `wrangler.jsonc` | Cloudflare Worker settings; `name` must stay `sean-cc` |

## Writing workflow

1. Draft in the Obsidian vault (iCloud, not in this repo).
2. Move finished posts to the vault's `Published` folder.
3. Copy them into `src/content/blog/`, then commit and push. *(A script to do the copying and convert Obsidian-only syntax is still on the to-do list.)*

Edit published posts in the vault, not in the repo copy. Use lowercase-hyphenated filenames (`my-first-post.md`) with title and date in the front matter.

## Theme

Monochrome dark theme with the system font (San Francisco on Macs). Colors are CSS variables at the top of `src/styles/global.css`, with a matching light version that follows the visitor's device setting. Code blocks are shown in grayscale by one CSS rule in the same file.
The starter's variable names were kept, so some names no longer describe the color: `--black` is the lightest text (headings), `--gray-dark` is body text, and `--gray-light` is a dark border tone.

## Email DNS (currently set to "no email")

sean.cc has records that tell other servers it never sends or receives mail. Before using an @sean.cc address or sending a newsletter from it:

1. Delete the null MX record (`MX @ 0 .`).
2. Replace the SPF record (`v=spf1 -all`) with the provider's.
3. Delete the empty `*._domainkey` record and add the provider's DKIM.
4. Set DMARC to `p=none` while testing, then back to `p=reject`.

## Credit

The base styles come from [Bear Blog](https://github.com/HermanMartinus/bearblog/) (MIT license), by way of the Astro blog starter.
