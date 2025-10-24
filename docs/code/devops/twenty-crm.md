# Installing Twenty CRM on Hetzner

This guide walks you through deploying [Twenty CRM](https://github.com/TwentyHQ/twenty-docker) on a Hetzner server. It assumes you have already completed the [Coolify + Hetzner Deployment](hetzner-server-setup.md) with Docker and NGINX Proxy Manager installed.

## Prerequisites

- A Hetzner server with Docker and NGINX Proxy Manager installed
- A domain name (we'll use Porkbun in this example)
- Basic command line knowledge

---

## 🌐 1. Point DNS to Your Server

On [Porkbun](https://porkbun.com):

| Type | Host | Answer (IP Address) | TTL |
|------|------|---------------------|-----|
| A    | crm  | your.server.ip      | 300 |

📝 This will resolve `crm.yourdomain.com` to your VPS.

---

## 📁 2. Clone and Configure Twenty CRM

Here are the offical install docs to Twenty CRM:

[Official Twenty CRM Docs](https://twenty.com/developers/section/self-hosting/docker-compose)

### One-line Docker Install

Install the latest stable version of Twenty with a single command:

```bash
bash <(curl -sL https://git.new/20)
```
To install a specific version or branch:

```bash
VERSION=vx.y.z BRANCH=branch-name bash <(curl -sL https://git.new/20)
```
- Replace x.y.z with the desired version number.
- Replace branch-name with the name of the branch you want to install.


### Alternatively, Clone the repo:
```bash
git clone https://github.com/TwentyHQ/twenty-docker.git
cd twenty-docker
```

### Create a `.env` file:
```bash
nano .env
```

Example contents:

```env
PG_DATABASE_USER=postgres
PG_DATABASE_PASSWORD=your_password
PG_DATABASE_HOST=db
PG_DATABASE_PORT=5432

NODE_PORT=3000
SERVER_URL=https://crm.yourdomain.com

REDIS_URL=redis://redis:6379

STORAGE_TYPE=local

APP_SECRET=your_random_secret
```

Generate a secure secret:
```bash
openssl rand -hex 32
```

### Add `restart: always` to `docker-compose.yml`

Add this line under each service in your `docker-compose.yml`:
```yaml
restart: always
```

---

## 🧱 3. Start Twenty CRM

```bash
docker compose up -d
```

---

## 🔁 4. Configure NGINX Proxy Manager

1. Open `http://your.server.ip:81`
2. Go to **Proxy Hosts** > **Add Proxy Host**
3. Fill in:
   - **Domain Names**: `crm.yourdomain.com`
   - **Forward Hostname / IP**: `localhost`
   - **Forward Port**: `3000`
   - ✅ Websockets Support
   - ✅ Block Common Exploits
4. Go to the **SSL** tab:
   - Enable SSL
   - Request a new Let's Encrypt certificate
   - Accept terms and enter a valid email
5. Save

---

## ✅ 5. Test Your Installation

Visit:

https://crm.yourdomain.com


You should see the live Twenty CRM instance with a green padlock ✅

---

## 📋 Post-Installation Checklist

- [ ] All containers are running (`docker ps`)
- [ ] DNS is resolving properly
- [ ] SSL certificate is working
- [ ] `.env` file and secrets are backed up securely
- [ ] All services have `restart: always` set

---

## 🔧 Troubleshooting

If you encounter issues:

1. Check container logs:
   ```bash
   docker logs twenty-docker-web-1
   ```
2. Verify all services are running:
   ```bash
   docker compose ps
   ```
3. Ensure DNS has propagated:
   ```bash
   dig crm.yourdomain.com
   ```

---

**Author:** Wesley Ordonez 
**Last updated:** April 14, 2025