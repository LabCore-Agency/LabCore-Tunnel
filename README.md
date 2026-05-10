# LabCore Tunnel 🚀

A high-performance, self-hosted reverse tunnel service (like localtunnel or ngrok) built entirely in Node.js. 
Supports dynamic subdomains for HTTP, and raw TCP/UDP tunneling for games and databases.

---

## ☁️ 1. Deploying the Server on your VPS

Ensure Node.js is installed on your VPS.
Upload the `server` folder to your VPS and install dependencies:

```bash
cd server
npm install
```

Start the server:
```bash
# Optionally, set your custom base domain:
export BASE_DOMAIN="tunnel.labcore.es"
export PORT="80" # or 8080 if behind Nginx
node server.js
```

*(It is highly recommended to use `pm2` to run the process in the background: `pm2 start server.js --name labcore-tunnel`)*

### ⚠️ DNS Configuration
In your domain provider's dashboard (e.g. Cloudflare), create two A records:
1. **A Record:** `tunnel.labcore.es` -> Your VPS IP
2. **A Record (Wildcard):** `*.tunnel.labcore.es` -> Your VPS IP

### ⚠️ Firewall Configuration
For TCP and UDP tunneling to work, you must open ports 30000 to 40000 on your VPS:
```bash
sudo ufw allow 30000:40000/tcp
sudo ufw allow 30000:40000/udp
```

---

## 💻 2. Using the Client

Install the client globally via npm:
```bash
npm install -g labcore-tunnel
```

### Tunneling HTTP (Web Apps, APIs)
Expose a local web server running on port `3000`:
```bash
labtunnel 3000
```
With a custom subdomain (`https://my-app.tunnel.labcore.es`):
```bash
labtunnel 3000 -s my-app
```

### Tunneling TCP (Minecraft, MySQL, SSH)
Expose a local TCP server running on port `25565`:
```bash
labtunnel 25565 --tcp
```
With a custom subdomain:
```bash
labtunnel 25565 --tcp -s my-server
```

### Tunneling UDP (Real-time Games)
Expose a local UDP server running on port `7777`:
```bash
labtunnel 7777 --udp
```
With a custom subdomain:
```bash
labtunnel 7777 --udp -s my-game
```

### Forward to a Local IP (Not Localhost)
If your app is running on another device in your LAN (like a Raspberry Pi or Docker container):
```bash
labtunnel 80 --host 192.168.1.50
```

The client will automatically handle connection multiplexing, reconnections, and Base64 streaming to ensure binary compatibility across platforms.
