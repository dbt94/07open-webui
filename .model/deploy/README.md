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

## graph-memory im Web-Chat (Wissensgraph als Tools)
> **Kanonisch: über das Brain.** Im vollen Self-Host-Stack liefert **`model-chat`** Graph-Memory
> bereits selbst (Werkzeug `graph`, mcpo-Sidecar) — dann bekommen **Web *und* Telegram** ihn
> automatisch, **ohne** die Registrierung unten. Diese Sektion ist nur für **Standalone-open-webui**
> (ohne Brain-Graph) oder wenn du die Graph-Tools zusätzlich direkt in open-webui willst.

Der hier mitgelieferte **`mcpo`-Dienst** exponiert den Code-Wissensgraphen (`codebase-memory-mcp`,
Skill `graph-memory`) als **OpenAPI-Tool-Server** — open-webui spricht kein stdio-MCP direkt.
- `CODEBASE_DIR` in `.env` auf den zu indizierenden Code zeigen (read-only gemountet).
- Nach `docker compose up -d`: in open-webui unter **Einstellungen → Tools** den Server
  `http://mcpo-codebase:8000` registrieren → die Code-Graph-Tools stehen im Chat zur Verfügung
  (strukturelle Fragen, Call-Chains, ~99% weniger Tokens statt Datei-für-Datei-Lesen).

## Voraussetzung
`model-chat` läuft im selben Netz `model-net` (Backend `dbt94/model-chat`), ebenso OmniRoute + Supabase.

> Turnkey mit dem offiziellen open-webui-Image. Willst du **deinen Fork** laufen lassen, baue ein
> Image daraus und trage es als `OPENWEBUI_IMAGE` in der `.env` ein.
