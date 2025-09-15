# 🐧 Complete Workflow: Ubuntu + Frappe/ERPNext

## 1. Start Ubuntu

* Open **Ubuntu** (via WSL or directly from your system).
* You’ll land in your **home directory**:

  ```bash
  cd ~
  ```

---

## 2. Go to your Frappe project

Usually, Frappe is installed inside a folder called `frappe-bench`:

```bash
cd ~/frappe-bench
```

*(If yours has another name/path, replace it with the right one.)*

---

## 3. Start Frappe/ERPNext services

Run:

```bash
bench start
```

👉 This will start:

* MariaDB (Database)
* Redis (Caching & Queues)
* Node.js + Web Server
* Frappe App Server

---

## 4. Access ERPNext

* Open your web browser.

* Go to:

  ```
  http://localhost:8000
  ```

* Login with your ERPNext account.

* Now you can work on your dashboard.

---

## 5. Work normally

* You can create apps, manage sites, and use ERPNext features.
* If you open another terminal and need to run bench commands (like migrations, new-app, backups), always go into the project folder first:

  ```bash
  cd ~/frappe-bench
  ```

---

## 6. Stop Frappe safely

When you finish working:

* In the same terminal where `bench start` is running, press:

  ```
  CTRL + C
  ```
* This stops all services gracefully.

---

## 7. Exit Ubuntu

If you’re using **WSL** (Windows Subsystem for Linux):

```bash
exit
```

This will close your Ubuntu session.

If you’re using **real Ubuntu (dual boot / VM)**:

```bash
sudo poweroff
```

This powers off the machine safely.

---

# 🔑 Quick Daily Routine (Summary)

1. **Start Ubuntu**
2. `cd ~/frappe-bench`
3. `bench start`
4. Open **[http://localhost:8000](http://localhost:8000)** in browser
5. Work 🚀
6. **CTRL + C** to stop
7. `exit` (WSL) or `sudo poweroff` (real Ubuntu)

---