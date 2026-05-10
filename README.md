# labcore-tunnel

A high-performance reverse tunnel CLI tool to securely expose your local applications to the internet. Built entirely in Node.js, it supports dynamic subdomains for HTTP, and raw TCP/UDP tunneling for game servers and databases.

## Installation

Install the package globally via npm:

```bash
npm install -g labcore-tunnel
```

## Usage

### Tunneling HTTP (Web Apps, APIs)

Expose a local web server running on port `3000`:
```bash
labtunnel 3000
```

Request a custom subdomain (`https://my-app.tunnel.labcore.es`):
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

### Tunneling UDP (Real-time Games, VoIP)

Expose a local UDP server running on port `7777`:
```bash
labtunnel 7777 --udp
```

With a custom subdomain:
```bash
labtunnel 7777 --udp -s my-game
```

### Forwarding to a Local IP

If your application is running on another device in your LAN (such as a Raspberry Pi or a Docker container):
```bash
labtunnel 80 --host 192.168.1.50
```

## Features

- Connection multiplexing and robust reconnections.
- Base64 streaming for binary compatibility across platforms.
- Support for complex TCP and UDP routing.
- No registration or auth tokens required.
