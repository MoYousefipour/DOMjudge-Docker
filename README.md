# DOMjudge Setup Guide (Docker)

This guide explains how to set up **DOMjudge** using **Docker** and **Docker Compose**.
You will run the *domserver* first, retrieve the necessary passwords, configure the *judgehost*, and then access the system from your browser.

---

## ✅ Prerequisites

Make sure the following are installed:

* **Docker**
* **Docker Compose**

---

## 🚀 Step 1 — Start the DOMserver

Run the DOMserver using:

```bash
docker compose -f domserver.yml up -d
```

This starts the DOMjudge server in the background.

---

## 🔑 Step 2 — Retrieve Admin & Judgehost Passwords

After the server starts, fetch the initial passwords:

### Admin Password

```bash
docker exec -it domserver cat /opt/domjudge/domserver/etc/initial_admin_password.secret
```

### Judgehost Password (REST API secret)

```bash
docker exec -it domserver cat /opt/domjudge/domserver/etc/restapi.secret
```

* The **first** password is the **admin login** password.
* The **second** password is the **judgehost authentication token**.

---

## 🛠 Step 3 — Configure the Judgehost

Copy the judgehost password from above and set it in your `judgehost.yml` file:

```yaml
- JUDGEDAEMON_PASSWORD="<paste the password here>"
```

---

## ▶️ Step 4 — Start the Judgehost

Run:

```bash
docker compose -f judgehost.yml up -d
```

This launches the judgehost(s) that will evaluate submissions.

---

## 🌐 Step 5 — Access DOMjudge

Open your browser and go to:

```
http://localhost:80
```

Log in using:

* **Username**: `admin`
* **Password**: (the admin password retrieved earlier)

---

## ⚠️ Notes

* You may see some warnings during startup — these are normal and can be safely ignored unless they indicate a critical error.
* Make sure both the **domserver** and **judgehost** containers stay running.