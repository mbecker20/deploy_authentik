# Deploy Authentik

Runs Authentik using their default setup:
https://docs.goauthentik.io/docs/install-config/install/docker-compose

## Komodo Resource TOML

```toml
[[stack]]
name = "authentik"
[stack.config]
repo = "mbecker20/deploy_authentik"
file_paths = [
	"compose.yaml",
	# "caddy.compose.yaml" # Deploy https proxy
]
environment = """
	AUTHENTIK_IMAGE=ghcr.io/goauthentik/server
	AUTHENTIK_TAG=latest
	AUTHENTIK_SECRET_KEY=[[AUTHENTIK_SECRET_KEY]]
	PG_PASS=[[AUTHENTIK_PG_PASS]]
	PG_USER=authentik
	PG_DB=authentik

	CADDY_TAG=latest
	# Required for Caddy deploy
	AUTHENTIK_DOMAIN=authentik.example.com
"""

[[variable]]
name = "AUTHENTIK_SECRET_KEY"
value = "your_secret_key"
is_secret = true

[[variable]]
name = "AUTHENTIK_PG_PASS"
value = "your_pg_pass"
is_secret = true
```