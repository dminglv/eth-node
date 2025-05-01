# 🚀 Ethereum Full Node via Docker Compose

This repository provides a clean and ready-to-use setup for running an **Ethereum Full Node** using Docker Compose with the official Geth client.

> ✅ **Pre-configured for Mainnet**  
> 🐳 Runs in a Docker container with persistent storage
> 🔐 Uses a JWT secret for secure communication with a consensus client
---

## 📦 Requirements

- [Docker](https://www.docker.com/)
- [Docker Compose](https://docs.docker.com/compose/)
- `openssl` (for generating JWT secret)
---

## 🔐 Generate JWT Secret

Before starting the node, generate a JWT secret file. This is required for communication between execution and consensus clients.

```bash
mkdir -p jwt
openssl rand -hex 32 > jwt/jwt.hex
```
This will create a `jwt.hex` file inside the `jwt` directory.


## 📝 Environment Configuration

You need to create a `.env` file based on the provided `.env.example`.  
This file allows you to configure your node, including checkpoint sync support.

You can choose a valid checkpoint sync URL from the official community list:
👉 https://eth-clients.github.io/checkpoint-sync-endpoints/

## ⚙️ Optional Parameters (set inside `docker-compose.yml` under `command:`)

### 🔁 `--syncmode`

Defines the synchronization method:

- `snap` *(default)* – Fast sync using state snapshots
- `full` – Full sync with all historical data

### 🧱 `--gcmode`

Controls how much state data is retained:

- `full` *(default)* – Prunes old state data
- `archive` – Retains **all** historical states (heavy disk usage, for analytics and historical queries)
---

### ✅ Start the Node

```bash
docker compose up --build -d
```