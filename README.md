# Personal Blog

An Astro static blog ready for GitHub Pages and a custom domain.

## 写作与发布指南

中文操作文档见 [`docs/blog-writing-publishing-guide.md`](docs/blog-writing-publishing-guide.md)。

## Local Development

```powershell
npm install
npm run dev
```

## Build

```powershell
npm run build
```

The generated site is written to `dist/`.

## Publish With GitHub Pages

1. Create a GitHub repository and push this project.
2. In the repository, open **Settings > Pages**.
3. Set **Source** to **GitHub Actions**.
4. Push to `main` or `master`; the workflow in `.github/workflows/deploy.yml` will deploy the site.

## Custom Domain

This project is configured for:

```text
mwnostop.cn
```

Then configure DNS at your domain provider:

- For an apex domain like `example.com`, add GitHub Pages `A` records.
- For a subdomain like `www.example.com`, add a `CNAME` record pointing to your GitHub Pages host.

Update `astro.config.mjs` with your production URL when the domain is ready:

```js
export default defineConfig({
  site: "https://mwnostop.cn",
  output: "static"
});
```
