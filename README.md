# 🔮 QR Grimoire

A self-contained, single-file QR code scanner and decoder with a dark "ancient grimoire" aesthetic. Scan with your camera or upload an image, and get a structured breakdown of what the code contains — URLs, Wi-Fi credentials, contact cards, calendar events, crypto addresses, emails, phone numbers, SMS, and geolocation — along with a plain-language security assessment for each.

No backend, no build step, no dependencies to install. It's one `index.html` file.

Download APK and iso zip from here : https://drive.google.com/drive/folders/1yUm6_U5pxCR99dBA_LIc35ySZNTiSYDC

---

## ✨ Features

- **Live camera scanning** — real-time QR detection via your device camera, with a visual scan frame and bounding-box overlay on detected codes.
- **Image upload scanning** — drop in a photo or screenshot containing a QR code instead of using the camera.
- **Smart content parsing** for:
  - URLs (with HTTPS/HTTP and shortened-link detection)
  - Wi-Fi credentials (`WIFI:`)
  - Contact cards (vCard)
  - Calendar events (vEvent)
  - Email (`mailto:`), phone (`tel:`), and SMS (`sms:`/`smsto:`)
  - Cryptocurrency payment links (Bitcoin, Ethereum, Litecoin, Dogecoin)
  - Geographic coordinates (`geo:`) with a direct Google Maps link
  - Plain text fallback with encoding detection
- **Security verdicts** — every scan is labeled safe / caution / danger with a short explanation (e.g. flags insecure HTTP links, shortened URLs, Wi-Fi credential exposure, crypto-address risk).
- **Scan history** — keeps your last 20 scans locally in the page session; click any entry to re-open its details.
- **One-click copy** of the raw scanned content or any parsed value.
- **Friendly camera error handling** — clear, actionable guidance for denied permissions, missing cameras, cameras in use by another app, or unsupported/insecure browser contexts.
- **Battery-aware** — camera automatically pauses when you switch tabs and releases fully when you navigate away.
- **Fully responsive**, mobile-first layout with reduced-motion support for accessibility.

---

## 🛠 Tech Stack

- Vanilla HTML, CSS, and JavaScript — no frameworks, no build tools.
- [jsQR](https://github.com/cozmo/jsQR) (via CDN) for QR decoding from camera frames and uploaded images.
- Google Fonts (Cinzel, Cormorant Garamond, JetBrains Mono) for the thematic typography.
- Optional Google AdSense integration (can be removed — see [Configuration](#-configuration) below).

---

## 🚀 Getting Started

### Run it locally

Since it's a single static file, you can just open it directly:

```bash
# Clone or download the repo, then:
open index.html        # macOS
start index.html        # Windows
xdg-open index.html      # Linux
```

> **Note:** Camera access (`getUserMedia`) requires a **secure context** — that means **HTTPS**, or `localhost`. Opening the file directly (`file://`) will work for image uploads, but the live camera scanner needs to be served over `http://localhost` or HTTPS. A quick local server works:
> ```bash
> python3 -m http.server 8000
> # then visit http://localhost:8000
> ```

### Deploy it for free

This is a static file, so any static host works. All of the following are free with automatic HTTPS:

| Host | How |
|---|---|
| **Netlify** | Drag and drop `index.html` onto [app.netlify.com](https://app.netlify.com) — instant `*.netlify.app` URL |
| **Cloudflare Pages** | Pages → Create project → Direct Upload — instant `*.pages.dev` URL |
| **Vercel** | Drag-and-drop deploy or connect a GitHub repo — instant `*.vercel.app` URL |
| **GitHub Pages** | Push to a repo → Settings → Pages → deploy from `main` branch — `*.github.io/<repo>` URL |

A custom domain can be attached to any of these for free (you only pay for domain registration itself, e.g. via Namecheap or Cloudflare Registrar).

---

## ⚙️ Configuration

### Removing or changing ads

The page includes Google AdSense slots (banner, mid-page, and footer) tied to a placeholder publisher ID (`ca-pub-8463414369456138`). To use your own:

1. Replace `ca-pub-8463414369456138` with your AdSense publisher ID throughout the file.
2. Replace the `data-ad-slot` values with your own ad unit slot IDs.

To remove ads entirely, delete the `<script>` tag in `<head>` referencing `adsbygoogle.js`, and the three `.ad-banner` / `.ad-slot` / `.footer-ad` blocks in the body.

### Changing the theme

All colors, fonts, and spacing are controlled by CSS custom properties at the top of the `<style>` block (under `:root`). Adjust `--gold`, `--bg`, `--crimson`, etc. to restyle the whole app without touching component CSS.

---

## 🔒 Privacy & Security

- All QR decoding happens **entirely client-side** in the browser — no scanned content, images, or camera frames are ever sent to a server.
- Scan history is kept only in memory for the current page session and is cleared on reload.
- User-generated/scanned content is HTML-escaped before rendering and never executed, so a malicious QR code cannot inject scripts into the page.
- Camera streams are released automatically when the tab is hidden or the page is closed.

---

## 📋 Browser Support

Works in all modern evergreen browsers (Chrome, Edge, Firefox, Safari) on desktop and mobile. The live camera scanner specifically requires:

- A secure context (HTTPS or `localhost`)
- `navigator.mediaDevices.getUserMedia` support (all modern browsers)

If the camera is unavailable, the app gracefully falls back to image-upload scanning with a clear in-app explanation.

---

## 📄 License

Add your preferred license here (e.g. MIT) before distributing or open-sourcing this project.
