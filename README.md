# XRail Panel

A Railway-first, single-container administration panel for managing Xray client records and generating VLESS, VMess and Trojan links, QR codes and per-user subscription URLs.

## Railway
1. Push this repository to GitHub and deploy that repository on Railway. Railway detects the root `Dockerfile`.
2. Add a Volume mounted at `/data`.
3. Set `ADMIN_PASSWORD` and a long random `JWT_SECRET`. Set `PUBLIC_BASE_URL` to the generated HTTPS domain.
4. Generate an HTTP public domain for the panel.
5. The UI/config/subscription service works immediately.
6. To run Xray too, set `ENABLE_XRAY=true`, create a Railway TCP Proxy targeting internal port `10000`, then set `XRAY_PUBLIC_HOST` and `XRAY_PUBLIC_PORT` to the generated proxy hostname/port. Redeploy.

Important: Railway's external TCP proxy port can differ from the internal Xray port. The panel therefore keeps internal listen port (10000) separate from the public client port.

## Local
```bash
cp .env.example .env
npm install
set -a; . ./.env; set +a
npm start
```
Open http://localhost:3000. Default username is `admin`; use the password you configured.

## Scope
This build intentionally supports a single TCP inbound because Railway TCP Proxy exposes a configured application port. It generates VLESS (Reality-ready fields), VMess and Trojan client links and subscriptions. Telegram's native MTProto proxy is a separate protocol/server and is not falsely represented as an Xray client type here.

Use only on systems and networks you are authorized to administer.
