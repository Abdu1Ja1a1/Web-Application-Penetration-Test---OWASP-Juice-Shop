# Environment Setup

## Application

- **App:** OWASP Juice Shop (Docker image: `bkimminich/juice-shop`)
- **Platform:** Docker Desktop, Windows
- **Host port:** 3007 (mapped to container port 3000)
- **Date started:** 04/08/2026

## Deployment

Deployed via Docker Desktop (GUI):

1. Pulled the `bkimminich/juice-shop` image via the Docker Desktop Search tab.
2. Ran the container with host port 3007 mapped to container port 3000.
3. Accessed the app at `http://localhost:3007`.

## Tools Used

| Tool | Purpose |
|---|---|
| Docker Desktop | Hosting the vulnerable application |
| Browser dev tools | Manual recon, DOM inspection, local storage/token access |
| Burp Suite (Community Edition) | Intercepting/manipulating HTTP traffic, Intruder-based brute force |
| curl | Manual request testing |
| SecLists (`xato-net-10-million-passwords-1000.txt`) | Password wordlist for brute-force testing |
