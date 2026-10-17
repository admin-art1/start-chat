# PWA integration for start-chat

I added the PWA assets on branch `pwa/add-pwa-assets` so you can enable install & offline support.

Files added at repository root:
- `manifest.json` — app metadata
- `service-worker.js` — simple cache-first service worker with offline fallback
- `offline.html` — offline fallback page
- `/icons/icon-192.png` and `/icons/icon-512.png` — placeholder icons

What you still need to do
1. Add these lines inside the `<head>` of `index.html` (near your other meta/link tags):

```html
<link rel="manifest" href="/manifest.json">
<meta name="theme-color" content="#0d47a1">
<link rel="icon" href="/icons/icon-192.png">
```

2. Register the service worker by adding this before `</body>` in `index.html`:

```html
<script>
if ('serviceWorker' in navigator) {
  window.addEventListener('load', () => {
    navigator.serviceWorker.register('/service-worker.js')
      .then(reg => console.log('ServiceWorker registered:', reg.scope))
      .catch(err => console.log('ServiceWorker registration failed:', err));
  });
}
</script>
```

Testing locally
- `python -m http.server 8000` or `npx serve .` and open http://localhost:8000
- DevTools → Application → Manifest and Service Workers
- Run Lighthouse → PWA for a score & fixes

If you want, I can also update `index.html` directly on this branch and open a pull request.
