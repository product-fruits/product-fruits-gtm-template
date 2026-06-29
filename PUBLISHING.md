# Publishing the Product Fruits template to the GTM Community Template Gallery

This guide covers everything from validating the template to getting it listed in the
[Community Template Gallery](https://tagmanager.google.com/gallery/).

Reference: <https://developers.google.com/tag-platform/tag-manager/templates>

## 1. Prepare the GitHub repository

The gallery pulls templates directly from a **public** GitHub repository. The repo must
contain these files in its root:

- `template.tpl` — the template (already in this repo).
- `metadata.yaml` — homepage + version-to-commit mapping.
- `LICENSE` — must be an OSI-approved license (this repo uses **MIT**).
- `README.md` — recommended.

This repo (`product-fruits/product-fruits-gtm-template`) already has all of these.

## 2. Validate the template in GTM

Before submitting, confirm the template imports and runs:

1. Open [Google Tag Manager](https://tagmanager.google.com/) → any container → **Templates**.
2. Under *Tag Templates* click **New**.
3. In the template editor open the **⋮** (top right) → **Import**, and select `template.tpl`.
4. Check the **Code** and **Permissions** tabs — there should be no errors.
5. Click **Preview**, fill in a test Workspace ID + Username, and confirm on a real page that:
   - `https://app.productfruits.com/static/script.js` is loaded,
   - `window.$productFruits` contains the `init` call,
   - Product Fruits initializes for the test user.

## 3. Commit and record the version SHA

The gallery requires each released version in `metadata.yaml` to point at a real commit.

```bash
git add template.tpl metadata.yaml LICENSE README.md PUBLISHING.md
git commit -m "Add Product Fruits GTM template"

# Get the commit hash and put it into metadata.yaml -> versions[0].sha
git rev-parse HEAD
```

Edit `metadata.yaml` and replace `REPLACE_WITH_COMMIT_SHA` with that hash, then commit again:

```bash
git add metadata.yaml
git commit -m "Record initial release SHA in metadata.yaml"
git push origin main
```

> Tip: keep the repo on the `main` branch — the gallery reads from the default branch.

## 4. Submit to the Community Template Gallery

1. Go to <https://tagmanager.google.com/gallery/> and sign in with the Google account
   that owns (or is an admin of) the GitHub repo.
2. Click **Add a template** (a.k.a. "Submit your template").
3. Authorize Google to access GitHub if prompted, then select the
   `product-fruits/product-fruits-gtm-template` repository.
4. The gallery validates the repo (checks for `template.tpl`, `metadata.yaml`, `LICENSE`).
5. Fix any reported issues, push, and re-validate.
6. Submit. Google reviews the submission; once approved it appears in the gallery and is
   discoverable via **Tag Configuration → Discover more tag types in the Community Template Gallery**.

## 5. Releasing updates later

For every change to `template.tpl`:

1. Bump the `version` number inside the `___INFO___` block of `template.tpl`.
2. Commit the change.
3. Add a **new** entry to the top of `versions:` in `metadata.yaml` with the new commit SHA
   and short `changeNotes`. Keep older entries for history.
4. Push to `main`. The gallery picks up the new version automatically.

## Notes specific to this template

- **Permissions**: it requests `inject_script` for `https://app.productfruits.com/*`,
  `access_globals` for `$productFruits` (read/write/execute) and `productFruits` (read/write),
  and `logging` in debug only. Reviewers expect these to be minimal — do not widen them.
- **Brand icon**: the `brand.thumbnail` in `template.tpl` is the Product Fruits logo encoded as
  a base64 PNG data URI. Replace it if branding changes.
- **No tests yet**: `___TESTS___` is empty. Adding test scenarios is optional but improves the
  review experience.
