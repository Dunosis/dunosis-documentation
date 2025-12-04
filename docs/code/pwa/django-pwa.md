# Guía Completa para Implementar PWA en Django (Material for MkDocs) 🚀 

## 📌 Versión en Español

### 1. Instalación de Dependencias

```bash
pip install django-pwa
npm install -D tailwindcss
```

### 2. Configurar `settings.py`

```python
INSTALLED_APPS = [
    ...
    'django.contrib.staticfiles',
    'pwa',
]

PWA_APP_NAME = 'MiAplicacion'
PWA_APP_SHORT_NAME = 'MiApp'
PWA_APP_DESCRIPTION = "Mi aplicación PWA"
PWA_APP_THEME_COLOR = '#000000'
PWA_APP_BACKGROUND_COLOR = '#ffffff'
PWA_APP_DISPLAY = 'standalone'
PWA_APP_SCOPE = '/'
PWA_APP_ORIENTATION = 'portrait'
PWA_APP_START_URL = '/'
PWA_APP_STATUS_BAR_COLOR = 'default'

PWA_APP_ICONS = [
    {
        "src": "/static/images/icons/icon-192x192.png",
        "sizes": "192x192"
    },
    {
        "src": "/static/images/icons/icon-512x512.png",
        "sizes": "512x512"
    }
]

PWA_APP_ICONS_APPLE = [
    {
        "src": "/static/images/icons/icon-192x192.png",
        "sizes": "192x192"
    },
    {
        "src": "/static/images/icons/icon-512x512.png",
        "sizes": "512x512"
    }
]

PWA_SERVICE_WORKER_PATH = BASE_DIR / "static/js/serviceworker.js"
```

### 3. Configurar URLs

```python
from django.urls import path, include

urlpatterns = [
    ...
    path('', include('pwa.urls')),
]
```

### 4. Agregar Manifest y Service Worker en la plantilla

En tu `base.html`:

```html
{% load static %}

<link rel="manifest" href="{% static 'manifest.json' %}">
<link rel="apple-touch-icon" href="{% static 'images/icons/icon-192x192.png' %}">
<meta name="theme-color" content="#000000">

{% if request.META.HTTP_USER_AGENT %}
  <script src="{% static 'js/serviceworker.js' %}"></script>
{% endif %}
```

### 5. Crear `manifest.json`

Ubicado en `static/manifest.json`:

```json
{
  "name": "MiAplicacion",
  "short_name": "MiApp",
  "start_url": "/",
  "display": "standalone",
  "background_color": "#ffffff",
  "theme_color": "#000000",
  "icons": [
    {
      "src": "/static/images/icons/icon-192x192.png",
      "sizes": "192x192"
    },
    {
      "src": "/static/images/icons/icon-512x512.png",
      "sizes": "512x512"
    }
  ]
}
```

### 6. Crear Service Worker con TailwindCSS

En `static/js/serviceworker.js`:

```js
self.addEventListener("install", (event) => {
  self.skipWaiting();
});

self.addEventListener("fetch", (event) => {
  event.respondWith(fetch(event.request));
});
```

---

## 📌 English Version

### 1. Install Dependencies

```bash
pip install django-pwa
npm install -D tailwindcss
```

### 2. Configure `settings.py`

```python
INSTALLED_APPS = [
    ...
    'django.contrib.staticfiles',
    'pwa',
]

PWA_APP_NAME = 'MiAplicacion'
PWA_APP_SHORT_NAME = 'MiApp'
PWA_APP_DESCRIPTION = "Mi aplicación PWA"
PWA_APP_THEME_COLOR = '#000000'
PWA_APP_BACKGROUND_COLOR = '#ffffff'
PWA_APP_DISPLAY = 'standalone'
PWA_APP_SCOPE = '/'
PWA_APP_ORIENTATION = 'portrait'
PWA_APP_START_URL = '/'
PWA_APP_STATUS_BAR_COLOR = 'default'

PWA_APP_ICONS = [
    {
        "src": "/static/images/icons/icon-192x192.png",
        "sizes": "192x192"
    },
    {
        "src": "/static/images/icons/icon-512x512.png",
        "sizes": "512x512"
    }
]

PWA_APP_ICONS_APPLE = [
    {
        "src": "/static/images/icons/icon-192x192.png",
        "sizes": "192x192"
    },
    {
        "src": "/static/images/icons/icon-512x512.png",
        "sizes": "512x512"
    }
]

PWA_SERVICE_WORKER_PATH = BASE_DIR / "static/js/serviceworker.js"
```

### 3. URL Configuration

```python
from django.urls import path, include

urlpatterns = [
    ...
    path('', include('pwa.urls')),
]
```

### 4. Add Manifest & Service Worker in Template

Inside `base.html`:

```html
{% load static %}

<link rel="manifest" href="{% static 'manifest.json' %}">
<link rel="apple-touch-icon" href="{% static 'images/icons/icon-192x192.png' %}">
<meta name="theme-color" content="#000000">

<script src="{% static 'js/serviceworker.js' %}"></script>
```

### 5. `manifest.json`

```json
{
  "name": "MyApplication",
  "short_name": "MyApp",
  "start_url": "/",
  "display": "standalone",
  "background_color": "#ffffff",
  "theme_color": "#000000",
  "icons": [
    {
      "src": "/static/images/icons/icon-192x192.png",
      "sizes": "192x192"
    },
    {
      "src": "/static/images/icons/icon-512x512.png",
      "sizes": "512x512"
    }
  ]
}
```

### 6. Service Worker + Tailwind

```js
self.addEventListener("install", () => self.skipWaiting());
self.addEventListener("fetch", (event) => event.respondWith(fetch(event.request)));
```

**Author:** Andrés Ribera
**Last updated:** December 4, 2025