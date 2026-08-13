# RVG Outline Panel V1

A small Persian RTL management panel designed to deploy on Railway and manage Outline Server access keys through Outline's Management API.

## Features
- Persian RTL dashboard
- Admin login
- PostgreSQL support via DATABASE_URL
- Add multiple Outline servers
- Create/list/delete/disable access keys
- Optional traffic limit in GB
- QR code generation for access keys
- Railway/Docker ready
- Health endpoint

## Railway deployment
1. Put this project in a GitHub repository.
2. In Railway: New Project -> Deploy from GitHub Repo.
3. Add a PostgreSQL service.
4. Add these variables to the panel service:
   - DATABASE_URL=${{Postgres.DATABASE_URL}}
   - SESSION_SECRET=<long random secret>
   - ADMIN_USERNAME=admin
   - ADMIN_PASSWORD=<strong password>
   - OUTLINE_VERIFY_TLS=false
5. Generate a public domain under Networking.
6. Open the domain and log in.

Railway can build directly from a repository containing a Dockerfile. The included railway.toml also defines the health check.

## Outline server
From Outline Manager, obtain the server's Management API URL (apiUrl). Paste that URL into the panel. The API certificate is commonly self-signed, so V1 has OUTLINE_VERIFY_TLS=false by default. Use HTTPS and restrict access to the panel.

## Important
Railway is the control panel host, not the VPN data-plane server. Your Outline server should run on a VPS or other suitable host. Never commit API URLs, API certificates, admin passwords, or session secrets to GitHub.
