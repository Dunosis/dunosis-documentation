# Hetzner Server Setup with Docker & NGINX

This guide walks you through setting up a fresh Hetzner VPS with Docker, NGINX Proxy Manager, and Portainer for container management.

---

## 🧱 1. Initialize Hetzner Ubuntu Server

### Connect to your server:

Can be done through SSH
```bash
ssh root@your.server.ip
```

Or through the Hetzner Server Console

### Create a new user (optional but recommended):
```bash
adduser youruser
usermod -aG sudo youruser
su - youruser
```

### Update system:
```bash
sudo apt update && sudo apt upgrade -y
```

---

## 🐳 2. Install Docker (Quick Install)

```bash
curl -fsSL https://get.docker.com | sudo sh
sudo usermod -aG docker $USER
newgrp docker  # OR log out and back in
```

Enable Docker to start on boot:
```bash
sudo systemctl enable docker
```

---

## 🧭 3. Install Docker Compose

```bash
sudo apt install docker-compose-plugin -y
```

---

## 📦 4. Deploy NGINX Proxy Manager

### Create folder and Docker Compose file:
```bash
mkdir -p ~/npm && cd ~/npm
nano docker-compose.yml
```

Paste:

```yaml
version: '3'
services:
  npm:
    image: jc21/nginx-proxy-manager:latest
    container_name: nginx-proxy-manager
    restart: always
    ports:
      - "80:80"
      - "81:81"
      - "443:443"
    volumes:
      - ./data:/data
      - ./letsencrypt:/etc/letsencrypt
```

### Launch:
```bash
docker compose up -d
```

### Access Web UI:
`http://your.server.ip:81`  
_Default login: `admin@example.com` / `changeme`_

---

## 🎯 5. Install Portainer (Optional but Recommended)

### Create Docker volume for Portainer:
```bash
docker volume create portainer_data
```

### Deploy Portainer:
```bash
docker run -d \
  -p 8000:8000 \
  -p 9443:9443 \
  --name portainer \
  --restart=always \
  -v /var/run/docker.sock:/var/run/docker.sock \
  -v portainer_data:/data \
  portainer/portainer-ce:latest
```

### Access Portainer:
Visit `https://your.server.ip:9443` to set up your admin account.

---

## 📋 Post-Setup Checklist

- [ ] Docker is running and enabled at boot
- [ ] NGINX Proxy Manager is accessible
- [ ] Portainer is accessible (if installed)
- [ ] All containers have `restart: always` set
- [ ] Basic firewall rules are in place (if needed)

---

## 🔒 Security Recommendations

1. **Update the default NGINX Proxy Manager credentials**
2. **Set a strong Portainer admin password**
3. **Consider setting up UFW (Uncomplicated Firewall):**
   ```bash
   sudo ufw allow ssh
   sudo ufw allow http
   sudo ufw allow https
   sudo ufw allow 9443  # For Portainer
   sudo ufw enable
   ```

---

**Author:** Wesley Ordonez  
**Last updated:** April 14, 2025
