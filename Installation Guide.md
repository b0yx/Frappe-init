# 🚀 Frappe Framework Installation & Project Setup

This repository documents the step-by-step installation of **Frappe Framework (v15)** on **Ubuntu (via WSL)** and shows how to create your own apps and sites.

---

## 📑 Table of Contents

* [📋 Prerequisites](#-prerequisites)
* [🔧 Installation Steps](#-installation-steps)

  * [1. Update System](#1-update-system)
  * [2. Install Dependencies](#2-install-dependencies)
  * [3. Configure MariaDB](#3-configure-mariadb)
  * [4. Install Node.js & Yarn](#4-install-nodejs--yarn)
  * [5. Install wkhtmltopdf](#5-install-wkhtmltopdf)
  * [6. Create Frappe User](#6-create-frappe-user-recommended)
  * [7. Setup Bench](#7-setup-bench)
  * [8. Initialize Bench](#8-initialize-bench)
  * [9. Create Site](#9-create-site)
  * [10. Start Development Server](#10-start-development-server)
  * [11. (Optional) Install ERPNext](#11-optional-install-erpnext)
* [📚 Creating Your Own App](#-creating-your-own-app)
* [📚 Adding Another Project](#-adding-another-project)
* [⚡ Troubleshooting](#-troubleshooting)
* [✅ Summary](#-summary)
* [📄 License](#-license)

---

## 📋 Prerequisites

* Windows 10/11 with **WSL2** and Ubuntu
* At least **4 GB RAM** and **20 GB free disk space**
* Basic Linux knowledge

---

## 🔧 Installation Steps

### 1. Update System

```bash
sudo apt update && sudo apt upgrade -y
```

### 2. Install Dependencies

```bash
sudo apt install -y python3-dev python3-setuptools python3-pip python3-distutils python3.12-venv \
redis-server software-properties-common mariadb-server mariadb-client \
curl wget git xvfb libfontconfig libxrender1 libjpeg-dev zlib1g-dev libssl-dev \
libffi-dev libmysqlclient-dev liblcms2-dev libblas-dev libatlas-base-dev libwebp-dev \
libharfbuzz-dev libfribidi-dev libxcb1-dev
```

### 3. Configure MariaDB

```bash
sudo mysql_secure_installation
```

Recommended answers: `n, Y, Y, Y, Y, Y`

Edit config:

```bash
sudo nano /etc/mysql/mariadb.conf.d/50-server.cnf
```

Add:

```ini
[mysqld]
innodb-file-format=barracuda
innodb-file-per-table=1
innodb-large-prefix=1
character-set-client-handshake = FALSE
character-set-server = utf8mb4
collation-server = utf8mb4_unicode_ci
```

Restart:

```bash
sudo service mysql restart
```

### 4. Install Node.js & Yarn

```bash
curl -sL https://deb.nodesource.com/setup_18.x | sudo -E bash -
sudo apt install -y nodejs
sudo npm install -g yarn
```

### 5. Install wkhtmltopdf

```bash
sudo apt install -y wkhtmltopdf
```

### 6. Create Frappe User (Recommended)

```bash
sudo adduser frappe
sudo usermod -aG sudo frappe
su - frappe
```

### 7. Setup Bench

```bash
mkdir ~/frappe_projects && cd ~/frappe_projects
python3 -m venv env
source env/bin/activate
pip install frappe-bench
```

### 8. Initialize Bench

```bash
bench init frappe-bench --frappe-branch version-15
cd frappe-bench
```

### 9. Create Site

```bash
bench new-site mysite.localhost
```

* Enter MariaDB root password
* Set Administrator password

Update Windows hosts file:

```
127.0.0.1   mysite.localhost
```

### 10. Start Development Server

```bash
bench start
```

Open [http://mysite.localhost:8000](http://mysite.localhost:8000)

### 11. (Optional) Install ERPNext

```bash
bench get-app erpnext --branch version-15
bench --site mysite.localhost install-app erpnext
bench build
bench start
```

---

## 📚 Creating Your Own App

Example: Library Management

```bash
bench new-app library
bench --site mysite.localhost install-app library
bench build
bench start
```

---

## 📚 Adding Another Project

Example: School Management

```bash
bench new-site school.localhost
bench new-app school
bench --site school.localhost install-app school
```

---

## ⚡ Troubleshooting

* **No module named 'frappe'**

  ```bash
  pip install -e apps/frappe
  ```

* **Socket.IO errors**

  ```bash
  cd apps/frappe && yarn install && cd ../.. && bench build
  ```

* **Assets missing**

  ```bash
  bench build
  ```

* **Git TLS errors during init**

  ```bash
  git config --global http.version HTTP/1.1
  git config --global http.postBuffer 524288000
  ```

---

## ✅ Summary

You now have:

* A working **Frappe v15** dev environment
* Ability to create **multiple sites** and **custom apps**
* Optional **ERPNext** installation

---

## 📄 License

This guide is open-source. Feel free to fork, improve, and share 🚀

---
