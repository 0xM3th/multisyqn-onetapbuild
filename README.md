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

## ⚙️ Installation

### 1. Install the Synchronizer CLI

```bash
npm install -g synqchronizer
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

---

## 📋 Monitoring

To view real-time logs:

```bash
journalctl -u synchronizer-cli -f
```

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
* Reach out to the [Multisynq Discord](https://discord.gg/5PhnYm5z) or create an issue in this repo.

---

## 📝 License

MIT License
