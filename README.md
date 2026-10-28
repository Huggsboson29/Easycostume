# EasyCostume – Wizard Face AR

Single-file WebAR demo (`index.html`) using A-Frame 1.5.0 + MindAR 1.2.5 face tracking.
It uses the back camera by default (add `?cam=front` or tap "Switch camera" for the selfie camera) and puts a wizard hat (anchor 10), a white beard (anchor 152), a moustache and a
rotating magic ring with sparkles on your face, using only A-Frame primitives.

## Live demo (GitHub Pages)

https://huggsboson29.github.io/Easycostume/

GitHub Pages serves over HTTPS, so the camera works on phones too. To (re)enable it:
**Settings → Pages → Build and deployment → Source: Deploy from a branch →
Branch: `ccr-64c4cb79-mbjbjl` / `(root)` → Save.** (`.nojekyll` makes Pages serve the files as-is.)

## Run locally

Browsers only allow camera access on `localhost` or HTTPS.

**Desktop (localhost):**

```bash
npx http-server -p 8080 -c-1        # or: python3 -m http.server 8080
# open http://localhost:8080
```

**Phone on the same Wi-Fi (needs HTTPS):**

```bash
npx http-server -p 8443 -S -C cert.pem -K key.pem   # after generating a cert:
# openssl req -x509 -newkey rsa:2048 -nodes -days 30 -keyout key.pem -out cert.pem -subj "/CN=localhost"
# open https://<your-computer-ip>:8443 and accept the self-signed warning
```

Or tunnel the localhost server instead: `npx localtunnel --port 8080` (or `cloudflared tunnel --url http://localhost:8080`) gives you a public HTTPS URL.

Opening `index.html` directly via `file://` will **not** work: the camera and MindAR's model loading need a server.
