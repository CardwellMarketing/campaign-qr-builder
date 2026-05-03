# Campaign QR Builder
### Cardwell Communications Playground

A polished, fully static micro-tool that helps nonprofits and small businesses instantly generate a QR code and matching campaign copy for events, donation pages, volunteer signups, surveys, workshops, and general campaigns.

---

## Files Created

| File | Description |
|---|---|
| `index.html` | The entire application — HTML structure, CSS styles, and JavaScript logic in a single self-contained file |
| `README.md` | This documentation file |

No build step, no dependencies to install, no server required.

---

## Is This App Static?

**Yes, fully static.** The app is a single `index.html` file with no backend, no database, no login system, and no API keys. Everything runs entirely in the visitor's browser:

- QR code generation happens client-side via the QRCode.js library (loaded from jsDelivr CDN)
- All campaign copy is generated with plain JavaScript string templates
- Copy-to-clipboard uses the native `navigator.clipboard` API (with a `document.execCommand` fallback)
- PNG download uses the HTML5 Canvas API

The only network request the page makes is loading the QRCode.js library from the CDN on first load. The app can also be used fully offline if the library is bundled locally (see below).

---

## Deploying to GitHub Pages

### Option A — Direct upload (simplest)

1. Create a new GitHub repository (e.g. `campaign-qr-builder`).
2. Upload `index.html` (and optionally `README.md`) to the repository root.
3. Go to **Settings → Pages**.
4. Under **Source**, select **Deploy from a branch**, choose `main` (or `master`), and set the folder to `/ (root)`.
5. Click **Save**. GitHub will publish the site at:
   ```
   https://<your-username>.github.io/campaign-qr-builder/
   ```

### Option B — Git CLI

```bash
git init
git add index.html README.md
git commit -m "Initial commit: Campaign QR Builder"
git branch -M main
git remote add origin https://github.com/<your-username>/campaign-qr-builder.git
git push -u origin main
```
Then enable GitHub Pages in the repository settings as described above.

### Option C — Bundle QRCode.js locally (offline-capable)

To avoid any CDN dependency, download the library and reference it locally:

```bash
curl -o qrcode.min.js https://cdn.jsdelivr.net/npm/qrcodejs@1.0.0/qrcode.min.js
```

Then replace the `<script src="...">` tag in `index.html` with:

```html
<script src="qrcode.min.js"></script>
```

Commit both files to the repository. The app will then work entirely offline.

---

## Open-Source QR Library

| Detail | Info |
|---|---|
| **Library** | [QRCode.js](https://github.com/davidshimjs/qrcodejs) by Shim Sangmin (davidshimjs) |
| **CDN used** | `https://cdn.jsdelivr.net/npm/qrcodejs@1.0.0/qrcode.min.js` |
| **License** | [MIT License](https://github.com/davidshimjs/qrcodejs/blob/master/LICENSE) |
| **Rendering** | HTML5 Canvas (with DOM table fallback for older browsers) |
| **Dependencies** | None |

The MIT License permits free use, modification, and distribution in both personal and commercial projects, provided the copyright notice is retained.

---

## Features at a Glance

- **7 input fields:** Organization name, campaign name, destination URL, campaign type (6 options), call-to-action, optional description, optional brand color
- **6 outputs:** QR code, short CTA line, printable label text, social media caption, email blurb, button/link text
- **User actions:** Generate kit, copy any output field individually, download QR as PNG (with white padding for print), copy destination URL, reset form
- **UX details:** Input validation with shake animation, toast notifications, responsive two-column layout, mobile-friendly single-column fallback

---

## Customization Tips

- **Change the default brand color:** Edit the `value="#2563EB"` attribute on the `<input type="color">` element.
- **Add more campaign types:** Extend the `templates` object in the `<script>` section with a new key and matching copy properties.
- **Embed in an existing site:** The entire app is self-contained and can be dropped into any `<iframe>` or adapted into a component.

---

*Prototype created by Cardwell Communications.*
