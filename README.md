# 🧠 Multisyqn OneTap Build

A one-tap deployment setup for running a Multisynq node using the `synchronizer` CLI. Easily initialize, configure, and manage your node and web dashboard as system services.

---

## 🚀 Features

* Fast and easy setup for Multisynq nodes
* Systemd integration for persistent services
* Optional web dashboard support
* CLI initialization with wallet & synq credentials

---
## 📦 Requirements

* Ubuntu/Debian-based Linux
* Node.js & npm
* A valid [Multisynq](https://dashboard.multisynq.com) account with:

  * Synq Key
  * Wallet Address & Password

---
## 🧰 Initial Setup (if needed)

If your VPS does **not** already have **Node.js** and **Docker**, install them first:

### ✨ Recommended System Packages
```bash
sudo apt-get update && sudo apt-get upgrade -y
```

```bash
sudo apt install curl iptables build-essential git wget lz4 jq make gcc nano automake autoconf tmux htop nvme-cli libgbm1 pkg-config libssl-dev libleveldb-dev tar clang bsdmainutils ncdu unzip libleveldb-dev screen -y
```


### 🟢 Install Latest Node.js (Global)

```bash
sudo apt update
sudo apt install -y curl
curl -fsSL https://deb.nodesource.com/setup_current.x | sudo -E bash -
sudo apt install -y nodejs
node -v
npm -v
```

### 🐳 Install Latest Docker

```bash
sudo apt update
sudo apt install -y ca-certificates curl gnupg lsb-release
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

echo \ 
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt update
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

# Test Docker
sudo docker run hello-world
```

If Node.js and Docker are already installed, skip this section and continue to the installation.

---

## ⚙️ Installation

### 1. Install the Synchronizer CLI

```bash
npm install -g synchronizer-cli
```

### 2. Initialize your Node

```bash
synchronize init
```

You'll be prompted for:

* Name of your synq
* Your Synq Key
* Wallet address
* Wallet password (for Multisynq dashboard access)

---

## 🛠 Setup as System Service

### 3. Enable CLI Service

```bash
synchronize service
sudo cp ~/.synchronizer-cli/synchronizer-cli.service /etc/systemd/system/
sudo systemctl daemon-reload
sudo systemctl enable synchronizer-cli
sudo systemctl start synchronizer-cli
```

### 4. (Optional) Enable Web Dashboard

```bash
synchronize service-web
sudo cp ~/.synchronizer-cli/synchronizer-cli-web.service /etc/systemd/system/
sudo systemctl daemon-reload
sudo systemctl enable synchronizer-cli-web
sudo systemctl start synchronizer-cli-web
```

If you're running your Multisyqn node on a VPS and want to access the web dashboard locally, you can use SSH port forwarding with a tool like [Termius](https://termius.com/):

#### 📡 Example Port Forwarding (using Termius)

* **Local port number:** `3000`
* **Bind address:** `127.0.0.1`
* **Select your vps where you run it**
* **Intermediate host:** Your VPS (e.g. `russel`)
* **Destination address:** `127.0.0.1`
* **Destination port number:** `3000`

![Termius Port Forwarding Example](./image.png)

Once set up, you can visit ```127.0.0.1:3000``` in your browser to access the Multisyqn dashboard hosted on your VPS.
![Syncqchronizer Dashboard Example](./pogi.png)
---
## 🔄 Updating to synchronizer-cli\@2.2.6

To update your synchronizer CLI to the latest version (2.2.6), run the following commands:

```bash
sudo systemctl stop synchronizer-cli
sudo systemctl stop synchronizer-cli-web
npm install -g synchronizer-cli
npm list -g synchronizer-cli --depth=0
sudo systemctl start synchronizer-cli
sudo systemctl start synchronizer-cli-web
```
![version (2.2.6)](./ras.png)
---


## 📋 Monitoring

To view real-time logs:

```bash
journalctl -u synchronizer-cli -f
```
![Logs in systemd Example](./imahe.jpg)
---

## 📁 File Locations

* Config: `~/.synchronizer-cli/config.json`
* Logs: Managed via `systemd` journal
* Services:

  * CLI: `/etc/systemd/system/synchronizer-cli.service`
  * Web: `/etc/systemd/system/synchronizer-cli-web.service`

---

## 🧩 Support

If you encounter issues:

* Double-check your Synq key and wallet credentials.
* Use `journalctl` logs for debugging.
* Reach out to the [Multisynq Discord](https://discord.gg/5PhnYm5z) [Startsynqing Website](https://www.startsynqing.com/community/drinktheblue)
* Use me referral to support me: [startsynqing](https://www.startsynqing.com/?ref=0bac73-w8yp5o)


---

## 📝 License

MIT License
