# Local certificates

## !! Only needed for running mastodon with Docker locally !!

At the root of this repo, run:

```bash
mkcert -cert-file certs/local-cert.pem -key-file certs/local-key.pem "docker.localhost" "*.docker.localhost" "domain.local" "*.domain.local"
```
