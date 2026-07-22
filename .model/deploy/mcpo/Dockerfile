# mcpo-Bridge: exponiert einen stdio-MCP-Server (codebase-memory-mcp) als OpenAPI-Tool-Server,
# damit open-webui (das kein stdio-MCP spricht) den Code-Wissensgraphen als Tools nutzen kann.
# Braucht Python (mcpo) + Node (npx codebase-memory-mcp).
FROM python:3.12-slim

RUN apt-get update \
 && apt-get install -y --no-install-recommends nodejs npm ca-certificates \
 && rm -rf /var/lib/apt/lists/*
RUN pip install --no-cache-dir mcpo

WORKDIR /code
EXPOSE 8000
# mcpo startet den MCP-Server als Subprozess und spiegelt seine Tools als OpenAPI (/docs).
CMD ["sh", "-c", "mcpo --host 0.0.0.0 --port 8000 -- npx -y codebase-memory-mcp"]
