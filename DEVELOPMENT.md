# Running Mastodon with Docker locally

## Pre-reqs

- Docker
- `mkcert`
- clone `https://github.com/jho-zzan/mastodon.git`

## Steps

1. Copy env config file

```bash
cp .env.production.sample .env.production
```

2. Generate local certs

```bash
mkcert -cert-file certs/local-cert.pem -key-file certs/local-key.pem "docker.localhost" "*.docker.localhost" "domain.local" "*.domain.local"
```

3. Setup Mastodon

```bash
docker compose run --rm web rake mastodon:setup
```

4. Answer with the following,
- Local domain: `localhost`
- When prompted to test out email, choose `N`
- When prompted to save config, choose `Y`

5. Print the config, copy the content into `.env.production` (replace everything)

6. Start it up!

```bash
docker compose up -d
```

## Create a user

1. Log in to the API server

```bash
docker exec -it mastodon-streaming-1 /bin/bash
```

2. Create a user with `tootctl`

```bash
 RAILS_ENV=production bin/tootctl accounts create <USERNAME> --email=<USERNAME>@localhost --confirmed --role=Admin
```

3. Remember the password that is printed!

## References

- https://github.com/felx/mastodon-documentation/blob/master/Running-Mastodon/Docker-Guide.md
