# Product Fruits — Google Tag Manager template

A custom Google Tag Manager (GTM) tag template that loads [Product Fruits](https://www.productfruits.com/)
and identifies the current user. It is built so non-technical users can install Product Fruits
through GTM by filling in a few fields — no editing of code snippets required.

## What it does

When the tag fires it:

1. Loads the Product Fruits loader script from `https://app.productfruits.com/static/script.js`.
2. Queues an `init` call with your Workspace ID, language and the current user.

It is the GTM equivalent of the standard Product Fruits snippet:

```html
<script>
  (function(w,d,u){
    w.$productFruits = w.$productFruits || [];
    w.productFruits = w.productFruits || {}; w.productFruits.scrV = '2';
    var a=d.getElementsByTagName('head')[0];var r=d.createElement('script');r.async=1;r.src=u;a.appendChild(r);
  })(window,document,'https://app.productfruits.com/static/script.js');
  $productFruits.push(['init', 'WORKSPACE_ID', 'en', { username: 'USERNAME' }]);
</script>
```

## Fields

| Field | Required | Description |
| --- | --- | --- |
| **Workspace ID** | Yes | Your Product Fruits workspace code (Installation page in the Product Fruits app). |
| **Username** | Yes | A unique identifier of the logged-in user. Usually a GTM variable. |
| **Language** | No | Two-letter language code. Defaults to `en`. |
| **Custom user properties** | No | Name/value pairs passed to Product Fruits inside `props`. |

## Files

- `template.tpl` — the GTM template definition (info, parameters, sandboxed JS, permissions).
- `metadata.yaml` — gallery metadata: homepage and released version → commit SHA mapping.
- `LICENSE` — MIT license.

## Local development / testing

1. Open [Google Tag Manager](https://tagmanager.google.com/) → your container → **Templates**.
2. Click **New** under *Tag Templates* → open the **⋮** menu → **Import** → select `template.tpl`.
3. Use the **Code** and **Permissions** tabs to review, then run the built-in **Preview** to test it on a page.

## Publishing to the Community Template Gallery

See [`PUBLISHING.md`](./PUBLISHING.md) for the full step-by-step guide.

## License

MIT — see [`LICENSE`](./LICENSE).
