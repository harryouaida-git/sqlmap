# DVWA SQL Injection Tutorial

This repository contains a hands-on lab for demonstrating **SQL Injection** using  
[Damn Vulnerable Web Application (DVWA)](http://www.dvwa.co.uk/) and [sqlmap](https://sqlmap.org/).

⚠️ **Disclaimer:** For educational purposes only. Run in a controlled lab environment.

---

## Contents
- `tutorial.md` – Step-by-step guide (converted from the original DOCX).
- `lab-setup/` – (Optional) Scripts and instructions for setting up DVWA with Docker.

---

## Quick Start

### 1. Clone Repository
```bash
git clone https://github.com/<your-username>/DVWA-SQLi-Tutorial.git
cd DVWA-SQLi-Tutorial
```

### 2. Run DVWA with Docker (Optional)
If you want to spin up DVWA locally:

```bash
cd lab-setup
docker-compose up -d
```

### 3. Access DVWA
- Open [http://localhost:8080](http://localhost:8080)
- Login with `admin` / `password`

### 4. Follow the Tutorial
Open [tutorial.md](tutorial.md) and begin at Step 1.

---

## Notes
- Requires Docker & Docker Compose (if using lab-setup).
- Do **NOT** expose DVWA to the internet.
- Intended for labs, training, and demo purposes only.
