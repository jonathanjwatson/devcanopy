# DevCanopy

The static homepage for [devcanopy.co](https://devcanopy.co/). It uses plain HTML and CSS: no packages, build process, or server are required.

## Edit the site

Most page content lives in `index.html`; visual design is in `styles.css`.

- Product links and descriptions: the `#products` section in `index.html`
- Page title and social/SEO metadata: the `<head>` in `index.html`
- Colors and fonts: the variables at the top of `styles.css`
- Custom domain: `CNAME`

Open `index.html` in a browser to preview changes locally.

## Publish with GitHub Pages

1. Create a public GitHub repository and push these files to its `main` branch.
2. In the repository, go to **Settings → Pages**.
3. Under **Build and deployment**, select **Deploy from a branch**, then choose `main` and `/(root)`.
4. Confirm `devcanopy.co` as the custom domain, then enable **Enforce HTTPS** once it becomes available.
5. At your domain registrar, add the DNS records GitHub Pages supplies for the apex domain and `www` version. Verify the domain in GitHub before connecting its DNS records.

GitHub Pages can publish a public repository at no hosting cost. See [GitHub’s custom domain instructions](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site) for the current DNS values and HTTPS guidance.
