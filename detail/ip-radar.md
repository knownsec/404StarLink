## ip-radar <https://github.com/steponeerror/ip-radar>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-python-blue)
![Author](https://img.shields.io/badge/Author-steponeerror-orange)
![GitHub stars](https://img.shields.io/github/stars/steponeerror/ip-radar.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V1.4.2-red)
![Time](https://img.shields.io/badge/Join-20261012-green)
<!--auto_detail_badge_end_fef74f2d7ea73fcc43ff78e05b1e7451-->


The whole stack — FastAPI backend + built frontend — runs in one container. Docker Compose v2.24+ required (`docker compose version` to check).

```bash
git clone https://github.com/steponeerror/ip-radar.git
cd ip-radar
docker compose up -d --build
```

Open http://127.0.0.1:8000. The container is reachable within seconds — a banner at the top tracks the keyless feeds' download/build progress live (all but the 5 keyed sources, including geo/city/ASN, the major blocklists and cloud ranges), and queries unlock automatically once the build settles. Subsequent starts load from the `ipradar-data` volume in seconds.

**All but 5 feeds need zero API keys.** To light up the 5 keyed sources, drop the keys into `.env.local` (gitignored, overrides `.env`):

```bash
cp .env .env.local   # then open .env.local in any editor, fill keys
docker compose up -d
```

| Source | Variable | Get a key |
|---|---|---|
| ipinfo_lite | `IPINFO_TOKEN` | <https://ipinfo.io/account/token> |
| abuseipdb | `ABUSEIPDB_API_KEY` | <https://www.abuseipdb.com/account> |
| otx | `OTX_API_KEY` | <https://otx.alienvault.com/settings> |
| otx_subscribed | `OTX_API_KEY`（与 otx 共用） | <https://otx.alienvault.com/settings> |
| ip2proxy | `IP2PROXY_TOKEN` | <https://www.ip2location.com/> |

Slow npm/pip downloads (common on CN networks)? Pass mirror build-args:

```bash
docker compose build --build-arg PIP_INDEX_URL=https://pypi.tuna.tsinghua.edu.cn/simple \
                      --build-arg NPM_REGISTRY=https://registry.npmmirror.com
```

Notes:

- The port binds to `127.0.0.1` by default; to go LAN/public, edit `ports` in `docker-compose.yml` — same-origin web use needs no key; programmatic/API access requires an API key issued from `/admin` (unlock it via the admin env block in `docker-compose.yml`).
- Behind a reverse proxy set `IP_RADAR_PROXY_HEADERS=1` (trusted proxies default `172.16.0.0/12`, override via `IP_RADAR_FORWARDED_ALLOW_IPS`, see `docker-compose.yml`) — otherwise per-IP rate limits only see the proxy IP.
- Each feed has its own usage terms; commercial use is your responsibility (this repo's AGPL-3.0 covers code only).
- Upgrade: `git pull && docker compose up -d --build` — the data volume stays right where it is.
- Disk: budget ≥6 GB for the data volume.
README



<!--auto_detail_active_begin_e1c6fb434b6f0baf6912c7a1934f772b-->
## 项目相关


## 最近更新

<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
