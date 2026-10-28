# EasyCostume – Wizard Body AR

Single-file WebAR demo (`index.html`). It opens the phone's **back camera**, finds people with
MediaPipe Pose Landmarker (body tracking, up to 3 people), and dresses each person in the textured
wizard model from `wizard_costume.glb`:

- **Costume** mesh (robe, sleeves) – scaled to the shoulder width and placed on the shoulders.
- **Hat** + **Beard** meshes (the beard includes the hair and covers the face) – moved together as one head
  piece, sized to the head and centred between the ears, with a spinning magic ring at the hat tip.
- Sparkles on the right wrist.

To fine-tune the fit, edit the `MODEL` constants near the top of the script in `index.html`.
Textures were downsized at import (costume 2048², the rest 1024²) so the model fits in phone GPU memory.

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
