# 🚀 Deploying a MERN Stack Project on Hostinger VPS

This guide explains how to deploy a **production-ready MERN stack application (MongoDB, Express, React, Node.js)** on a Linux VPS using:

- Node.js (via NVM)
- PM2 (Process Manager)
- Nginx (Reverse Proxy)
- SSL with Certbot
- UFW Firewall

---

## 1. 🌐 VPS Hosting Used in This Tutorial

👉 https://hostinger.com/AICODING10

---

## 📦 Deployment Architecture

```
User → Domain → Nginx → Node.js (PM2) → MongoDB
```

---

# 2. Connect to VPS

Log in to Your VPS in Terminal 

```bash
 ssh root@your_vps_ip
```

Update and Upgrade Your System

```bash
  sudo apt update
```
```bash
  sudo apt upgrade -y
```

Install Node.js and npm ( if not pre-installed)

```bash
  curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | bash
```
```bash
  \. "$HOME/.nvm/nvm.sh"
```
```bash
  nvm install 22
```
Install Git 
```bash
  sudo apt install -y git
```

---

# 3. Setup MongoDB

You can either:

- If you want to setup MongoDB on VPS Follow this Guide: [click here](https://github.com/GreatStackDev/notes/blob/main/MongoDB_Setup_on_VPS.md) 
OR  
- Use **MongoDB Atlas (Recommended)**

Make sure to update your `.env` file with correct connection string.

---

# 4. Deploy Backend (Node + Express)

Clone Your Backend Repository

```bash
 mkdir /var/www
```

```bash
 cd /var/www
```
```bash
 git clone https://github.com/yourusername/your-repo.git
```
```bash
 cd your-repo/backend
```

Install Dependencies

```bash
 npm install
```
Create .env file & configure Environment Variables

```bash
 nano .env
```

add environment variables then save and exit (Ctrl + X, then Y and Enter).


Installing pm2 to Start Backend

```bash
 npm install -g pm2
```
```bash
 pm2 start src/index.js --name project-backend
```
Start Backend on startup
```bash
 pm2 startup
```
```bash
 pm2 save
```
Allowing backend port in firewall 

```bash
 sudo ufw status
```
If firewall is disable then enable it using 
```bash
 sudo ufw enable
```
```bash
 sudo ufw allow 'OpenSSH'
```
```bash
 sudo ufw allow 3000
```
Install Nginx

```bash
 sudo apt install -y nginx
```

adding Nginx in firewall

```bash
 sudo ufw status
```
```bash
 sudo ufw allow 'Nginx Full'
```
---

# 5. Configure Nginx Reverse Proxy

Update Backend Nginx Configuration

```bash
nano /etc/nginx/sites-available/api.yourdomain.com.conf
```
```bash
server {
    listen 80;
    server_name api.yourdomain.com.;

    location / {
        proxy_pass http://localhost:3000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```
Save and exit (Ctrl + X, then Y and Enter).
---
Create symbolic links to enable the sites.

```bash
ln -s /etc/nginx/sites-available/api.yourdomain.com.conf /etc/nginx/sites-enabled/
```

Restart nginx

```bash
systemctl restart nginx
```
---

# 6. Configure Firewall (UFW)

Enable firewall:

```bash
ufw enable
```

Allow required services:

```bash
ufw allow OpenSSH
ufw allow 'Nginx Full'
```

Remove backend port exposure:

```bash
ufw delete allow 3000
```

---

# 7. Connect Domain to VPS

- Go to your domain DNS manager
- Add A record
- Point domain/subdomain to VPS IP

DNS propagation may take up to 24 hours.

---

# 8. Install SSL Certificate (HTTPS)

Install Certbot

```bash
sudo apt install -y certbot python3-certbot-nginx
```

Obtain SSL Certificates

```bash
certbot --nginx -d yourdomain1.com -d www.yourdomain1.com -d yourdomain2.com -d api.yourdomain.com
```

Verify Auto-Renewal

```bash
certbot renew --dry-run
```

---

# 🔐 Production Checklist

- [ ] Node installed via NVM
- [ ] Backend running with PM2
- [ ] Nginx reverse proxy configured
- [ ] Firewall secured
- [ ] SSL certificate installed
- [ ] Domain connected

---

# 🎯 Conclusion

You now have a **production-ready MERN stack deployment** running on a VPS with:

- Secure HTTPS
- Reverse proxy architecture
- Managed backend process
- Firewall protection

This setup is suitable for:

- SaaS Applications
- Production APIs
- App Store Backend Deployments
- Real-world Projects

---

If this guide helped you, consider supporting the project 🚀
