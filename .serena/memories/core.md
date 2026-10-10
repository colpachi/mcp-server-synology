# mcp-server-synology

Servidor **MCP** (Model Context Protocol) para NAS Synology: gerencia arquivos e downloads via autenticacao/sessao. Python 3.13.

- Suporta **dois transportes simultaneos**: stdio (Claude/Cursor) e WebSocket (Xiaozhi) - "unified server".
- Layout: `src/{auth,downloadstation,filestation}`, `tests/`, `assets/`, `logs/`.
- Deps: `mcp>=1.9.0`, `pycryptodome`, `requests`, `websockets>=11.0.3`; testes com pytest+pytest-asyncio.
- Config via `.env` (copiar de `env.example`): `SYNOLOGY_URL`, `SYNOLOGY_USERNAME`, `SYNOLOGY_PASSWORD`, `AUTO_LOGIN`, `VERIFY_SSL`.
- Docker: `FROM python:3.13-slim`, `docker-compose` servico `synology-mcp`.
- Repo **publico** (`github.com/atom2ueki/mcp-server-synology` - remote real, projeto de terceiro/open-source usado internamente).

## Invariantes
- **`VERIFY_SSL=false` e o default documentado** - normalmente indica NAS com certificado self-signed na rede local; nao "corrigir" para `true` sem checar se ha certificado valido configurado.
- Este e provavelmente a origem das ferramentas MCP de Synology usadas por agentes no ambiente - mudanca de contrato aqui pode afetar integracoes que dependem dele.
