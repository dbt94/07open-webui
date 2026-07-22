# open-webui als Web-Chat des Systems

Macht open-webui zur **Web-Oberfläche** des einheitlichen System-Chats — vorkonfiguriert auf das
`model-chat`-Backend (OmniRoute-Brain + Gedächtnis + mm-Werkzeug). Kein manuelles Verbinden nötig.

## Start
```bash
docker network create model-net 2>/dev/null || true
cd .model/deploy
cp .env.example .env         # WEBUI_SECRET_KEY setzen (openssl rand -hex 24)
docker compose up -d
```
Öffne `http://localhost:3000`, lege beim ersten Start ein Konto an → das Modell **`model-chat`**
steht bereits zur Wahl. Du chattest damit mit dem ganzen System (Gedächtnis + alle Fähigkeiten).

## Voraussetzung
`model-chat` läuft im selben Netz `model-net` (Backend `dbt94/model-chat`), ebenso OmniRoute + Supabase.

> Turnkey mit dem offiziellen open-webui-Image. Willst du **deinen Fork** laufen lassen, baue ein
> Image daraus und trage es als `OPENWEBUI_IMAGE` in der `.env` ein.
