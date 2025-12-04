# Guía Completa para Implementar PWA en Next.js


## 📌 Versión en Español
### 1. Introducción
Una Progressive Web App (PWA) permite que tu aplicación Next.js funcione offline, pueda instalarse en dispositivos móviles y se comporte como una aplicación nativa. Esta guía cubre:
	•	Configuración básica de manifest
	•	Registro del service worker
	•	Uso o no de next-pwa
	•	Detección e instalación en Android e iOS
	•	Ejemplo de botón “Instalar App”

⸻

### 2. Crear archivo manifest.json

Crea el archivo en:
/public/manifest.json

Ejemplo:
```json
{
  "name": "Mi Aplicación PWA",
  "short_name": "MiApp",
  "start_url": "/",
  "display": "standalone",
  "background_color": "#ffffff",
  "theme_color": "#522181",
  "icons": [
    {
      "src": "/icons/icon-192x192.png",
      "type": "image/png",
      "sizes": "192x192"
    },
    {
      "src": "/icons/icon-512x512.png",
      "type": "image/png",
      "sizes": "512x512"
    }
  ]
}
```

⸻

### 3. Incluir el manifest en app/layout.tsx

```html
<link rel="manifest" href="/manifest.json" />
<meta name="theme-color" content="#522181" />
```

⸻

### 4. Crear un Service Worker

En Next.js App Router, crea:

/public/sw.js

Ejemplo básico:
```javascript
self.addEventListener("install", () => {
  console.log("Service Worker instalado");
});

self.addEventListener("fetch", event => {
  event.respondWith(fetch(event.request));
});
```

⸻

### 5. Registrar el Service Worker

Crea:

/app/sw-register.js
```javascript
if (typeof window !== "undefined" && "serviceWorker" in navigator) {
  window.addEventListener("load", () => {
    navigator.serviceWorker.register("/sw.js");
  });
}
```

Importa en layout.tsx:
```html
<Script src="/sw-register.js" strategy="afterInteractive" />
```

⸻

### 6. Botón “Instalar App” (Android + iOS)

HTML/Tailwind
```html
<a id="install-button" class="my-4 text-primary text-2xl bg-white rounded-full px-5 py-2 shadow-md cursor-pointer">
  Instalar App
</a>

<div id="ios-card" class="hidden fixed bottom-5 right-5 bg-white p-4 rounded-lg shadow-lg w-64">
  <strong>Instalar en iOS</strong>
  <p class="mt-2 text-sm">1. Abrir en Safari<br>2. Tocar Compartir<br>3. Seleccionar "Añadir al inicio"</p>
  <button onclick="document.getElementById('ios-card').classList.add('hidden')" class="mt-3 bg-gray-300 w-full py-2 rounded">Cerrar</button>
</div>
```

Script
```html
<script>
let deferredPrompt;

function isIOS() { return /iphone|ipad|ipod/i.test(navigator.userAgent); }
function isInStandalone() { return window.navigator.standalone === true; }

window.addEventListener('beforeinstallprompt', e => {
  e.preventDefault();
  deferredPrompt = e;
  const btn = document.getElementById('install-button');
  btn.onclick = async () => {
    deferredPrompt.prompt();
    deferredPrompt = null;
  };
});

window.onload = () => {
  const btn = document.getElementById('install-button');

  if (isIOS() && !isInStandalone()) {
    btn.onclick = () => {
      document.getElementById('ios-card').classList.remove('hidden');
    };
  }
};
</script>
```

⸻

## 🇺🇸 PWA Guide for Next.js

### 1. Introduction

A Progressive Web App (PWA) allows your Next.js project to behave like a native app, work offline, and be installable on Android/iOS devices.
This guide includes:
	•	Manifest setup
	•	Service worker registration
	•	Optional integration with next-pwa
	•	Install button with Android/iOS detection

⸻

### 2. Create manifest.json

Place it in:

/public/manifest.json

Example:
```json
{
  "name": "My PWA Application",
  "short_name": "MyApp",
  "start_url": "/",
  "display": "standalone",
  "background_color": "#ffffff",
  "theme_color": "#522181",
  "icons": [
    { "src": "/icons/icon-192x192.png", "sizes": "192x192", "type": "image/png" },
    { "src": "/icons/icon-512x512.png", "sizes": "512x512", "type": "image/png" }
  ]
}
```

⸻

3. Add manifest to app/layout.tsx
```html
<link rel="manifest" href="/manifest.json" />
<meta name="theme-color" content="#522181" />
```

⸻

4. Create a Service Worker

/public/sw.js
```javascript
self.addEventListener("install", () => {
  console.log("Service Worker installed");
});

self.addEventListener("fetch", event => {
  event.respondWith(fetch(event.request));
});
```

⸻

5. Register the Service Worker

/app/sw-register.js
```javascript
if (typeof window !== "undefined" && "serviceWorker" in navigator) {
  window.addEventListener("load", () => {
    navigator.serviceWorker.register("/sw.js");
  });
}

Import in layout.tsx:

<Script src="/sw-register.js" strategy="afterInteractive" />
```

⸻

6. Install App Button (Android + iOS)

HTML/Tailwind
```html
<a id="install-button" class="my-4 text-primary text-2xl bg-white rounded-full px-5 py-2 shadow-md cursor-pointer">
  Install App
</a>

<div id="ios-card" class="hidden fixed bottom-5 right-5 bg-white p-4 rounded-lg shadow-lg w-64">
  <strong>Install on iOS</strong>
  <p class="mt-2 text-sm">1. Open in Safari<br>2. Tap Share<br>3. Select "Add to Home Screen"</p>
  <button onclick="document.getElementById('ios-card').classList.add('hidden')" class="mt-3 bg-gray-300 w-full py-2 rounded">Close</button>
</div>
```

Script
```html
<script>
let deferredPrompt;

function isIOS() { return /iphone|ipad|ipod/i.test(navigator.userAgent); }
function isInStandalone() { return window.navigator.standalone === true; }

window.addEventListener('beforeinstallprompt', e => {
  e.preventDefault();
  deferredPrompt = e;
  const btn = document.getElementById('install-button');
  btn.onclick = async () => {
    deferredPrompt.prompt();
    deferredPrompt = null;
  };
});

window.onload = () => {
  const btn = document.getElementById('install-button');

  if (isIOS() && !isInStandalone()) {
    btn.onclick = () => {
      document.getElementById('ios-card').classList.remove('hidden');
    };
  }
};
</script>
```
⸻

**Author:** Andrés Ribera
**Last updated:** December 4, 2025