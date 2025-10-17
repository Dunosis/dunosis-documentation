# 🌩️ Dunosis Wasabi Cloud Storage - Team Onboarding Guide

This guide will walk you through accessing and configuring our cloud storage system hosted on **Wasabi**, using a simple tool called **Cyberduck**.

> ✅ No need to create a Wasabi account — your access keys have already been created by the admin. Just follow the steps below.

---
## Overview

### 📂 What is Wasabi?

Wasabi is a secure and affordable cloud storage platform — think of it like a vault for our media files (photos, videos, designs, and more).

- 🔐 Safe and encrypted  
- 🏃‍♀️ Fast uploads/downloads  
- 📦 Used for archiving final edits and raw content

---

### 🦆 What is Cyberduck?

Cyberduck is a free app that lets you easily upload and download files to cloud storage (like Wasabi), using a clean and simple interface. It's like Google Drive, but directly connected to our long-term cloud archive.

🔗 [Download Cyberduck here](https://cyberduck.io/)

---

### 🧰 What You’ll Need

Your team admin will provide you with:

- ✅ Your **Access Key ID**
- ✅ Your **Secret Access Key** (Keep this private!)
- ✅ Your **Wasabi bucket name** (e.g., `dunosis-archive`)
- ✅ The correct **endpoint URL** (e.g., `s3.us-east-1.wasabisys.com`)

---

## 🧑‍💻 Step-by-Step: Set Up Cyberduck

1. Open **Cyberduck** and click `Open Connection` (top left).

    ![Cyberduck](./assets/du-docs-cyberduck-config.png)

2. From the dropdown, select **Amazon S3** (yes, even for Wasabi).
3. Fill in the fields:
    - **Server**: `s3.us-east-1.wasabisys.com` *(or the endpoint given to you)*
    - **Access Key ID**: *(provided by admin)*
    - **Secret Access Key**: *(provided by admin — keep private!)*
    - Leave other fields blank for now
4. Click **Connect**

    ![Cyberduck](./assets/du-docs-cyberduck-config-end.png)

5. You’ll now see our storage bucket(s). Double-click to open.

> ✅ Recommended: Click the `Add to Keychain` option to save the credentials (on Mac OS)

---

## 📁 Uploading & Downloading Files

### Uploading:
- Simply **drag & drop files** into the appropriate client folders.
- Create subfolders as needed by right-clicking.

### Downloading:
- Right-click any file → choose **Download**

⚠️ Be careful not to delete anything unless you’re 100% sure!

---

## Final Notes
- 🔐 Never share your secret access key

---

## Español

## 🌩️ Guía de Incorporación - Almacenamiento en la Nube Wasabi de Dunosis

Esta guía te mostrará cómo acceder y usar nuestro sistema de almacenamiento en la nube usando **Wasabi** y la herramienta sencilla **Cyberduck**.

> ✅ No necesitas crear una cuenta de Wasabi. El administrador ya ha creado tus credenciales. Solo sigue los pasos de abajo.

---

## 📂 ¿Qué es Wasabi?

Wasabi es una plataforma de almacenamiento en la nube segura y asequible. Piensa en ella como una bóveda para nuestros archivos multimedia (fotos, videos, diseños, etc).

- 🔐 Segura y cifrada  
- 🏃‍♀️ Rápida para subir y descargar  
- 📦 Usada para archivar contenido final y archivos RAW

---

## 🦆 ¿Qué es Cyberduck?

Cyberduck es una aplicación gratuita que te permite subir y descargar archivos a la nube de forma sencilla. Es como Google Drive, pero directamente conectado a nuestro archivo en la nube.

🔗 [Descargar Cyberduck aquí](https://cyberduck.io/)

---

## 🧰 Lo que Necesitarás

El administrador te proporcionará:

- ✅ Tu **Access Key ID**
- ✅ Tu **Secret Access Key** (¡Guárdala en privado!)
- ✅ El **nombre del bucket** (por ejemplo, `dunosis-archive`)
- ✅ La **URL del endpoint** (por ejemplo, `s3.us-east-1.wasabisys.com`)

---

## 🧑‍💻 Paso a Paso: Configurar Cyberduck

1. Abre **Cyberduck** y haz clic en `Open Connection` (parte superior izquierda).

    ![Cyberduck](./assets/du-docs-cyberduck-config.png)

2. En el menú desplegable, selecciona **Amazon S3** (aunque sea Wasabi).
3. Rellena los campos:
   - **Server**: `s3.us-east-1.wasabisys.com` *(o el endpoint que te indiquen)*
   - **Access Key ID**: *(proporcionado por el administrador)*
   - **Secret Access Key**: *(proporcionado por el administrador)*
   - Deja los demás campos en blanco por ahora
4. Haz clic en **Connect**

    ![Cyberduck](./assets/du-docs-cyberduck-config-end.png)

5. Ahora deberías ver el bucket de almacenamiento. Haz doble clic para abrirlo.

> ✅ Recomendado: Haz clic en la opción `Add to Keychain` para guardar las credenciales (en Mac OS)

---

## 📁 Subir y Descargar Archivos

### Subir:
- Simplemente **arrastra y suelta archivos** dentro de la carpeta que te asignaron.
- Puedes crear subcarpetas (por ejemplo, `ClienteX/FinalEdits/`)

### Descargar:
- Haz clic derecho en un archivo → elige **Download**

⚠️ ¡Ten cuidado de no borrar nada por accidente!

---

## ✅ Buenas Prácticas
- 🔐 Nunca compartas tu Secret Access Key

---

