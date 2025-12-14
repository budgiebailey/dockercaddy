# dockercaddy

Custom Caddy Docker image with additional plugins, built and published to GitHub Container Registry (GHCR).

## Features

This Docker image includes:
- **Caddy 2** - Modern web server with automatic HTTPS
- **caddy-geoip2** - GeoIP2 module for geographic location-based routing

## Usage

### Pulling the Image

Pull the latest image from GHCR:

```bash
docker pull ghcr.io/budgiebailey/dockercaddy:latest
```

### Running the Container

Basic usage:

```bash
docker run -d \
  -p 80:80 \
  -p 443:443 \
  -v caddy_data:/data \
  -v caddy_config:/config \
  -v $PWD/Caddyfile:/etc/caddy/Caddyfile \
  ghcr.io/budgiebailey/dockercaddy:latest
```

### Using with Docker Compose

Create a `docker-compose.yml` file:

```yaml
version: '3.8'

services:
  caddy:
    image: ghcr.io/budgiebailey/dockercaddy:latest
    ports:
      - "80:80"
      - "443:443"
    volumes:
      - ./Caddyfile:/etc/caddy/Caddyfile
      - caddy_data:/data
      - caddy_config:/config
    restart: unless-stopped

volumes:
  caddy_data:
  caddy_config:
```

Then run:

```bash
docker compose up -d
```

## Building Locally

To build the image locally:

```bash
docker build -t custom-caddy .
```

## Automatic Builds

This image is automatically built and pushed to GHCR via GitHub Actions when:
- Code is pushed to the `main` or `master` branch
- A new tag is created (e.g., `v1.0.0`)
- Weekly on Sundays at midnight UTC (to keep dependencies up to date)
- Manually triggered via workflow dispatch

## Available Tags

- `latest` - Latest build from the default branch
- `<branch-name>` - Latest build from a specific branch
- `v<version>` - Semantic version tags (e.g., `v1.0.0`, `v1.0`, `v1`)
- `<branch>-<sha>` - Build from a specific commit

## Plugins Included

- [caddy-geoip2](https://github.com/zhangjiayin/caddy-geoip2) - GeoIP2 module for geographic location-based routing

## License

This project uses Caddy, which is licensed under the Apache License 2.0.