# PocketBase Docker

- *This is not an official nor affiliated repository of PocketBase*
- This has been forked from BakirGracic for the arm64 image.
- Images have `latest` and PocketBase version tags (e.g. `0.27.2`)
- Original Author's GitHub: [github.com/BakirGracic/pocketbase-docker](https://github.com/BakirGracic/pocketbase-docker)
- Original Author's Docker Hub: [bakirg/pocketbase-docker](https://hub.docker.com/repository/docker/bakirg/pocketbase-docker)
- My GitHub: [github.com/hamzazafarc/pocketbase-docker-arm64](https://github.com/hamzazafarc/pocketbase-docker-arm64)
- Original Author's Docker Hub: [hyzkin/pocketbase-docker-arm64](https://hub.docker.com/repository/docker/hyzkin/pocketbase-docker-arm64)


---

![PocketBase](https://i.imgur.com/5qimnm5.png)

## What is PocketBase

PocketBase is an open-source backend (or BaaS) built as a single Go binary that provides:
- **Embedded SQLite Database** with real-time subscriptions
- **Authentication** and **User Management**
- **File Storage** and **Static File Serving**
- **Admin Dashboard** for easy management
- **REST-ish API** server for integrations
- Extendable using **Go** or **JavaScript**
- and much [more](https://pocketbase.io/)

## Features of `pocketbase-docker`

- **Lean & Secure:** Optimized using lightweight Alpine images and operation layering
- **Data Persistence:** Configurable volumes for `pb_data`, `pb_public`, `pb_migrations` and `pb_hooks` persistance
- **Health Checks:** Built‑in support for Docker health checks
- **Unofficial:** Not opinionated, welcoming contributions
- **Configurable:** Ability to configure some parameters

## Getting Started

### Prerequisites

- Docker Engine (v20.10+)
- Docker Compose (if using compose)

### Defaults

- Before starting PocketBase service, default superuser is created (in case `pb_data` directory doesn't exist) with `test@test.com` & `Test123!!!` credentials. Make sure to change credentials later!

### Building the Image Yourself

```bash
git clone https://github.com/BakirGracic/pocketbase-docker
cd pocketbase-docker
docker build -t pocketbase:test_build .
```

### Running the Container

#### Using Docker CLI

```bash
docker run -d \
  --name pocketbase \
  -p 8090:8090 \
  -v ~/pb/data:/pb_data \
  -v ~/pb/migrations:/pb_migrations \
  -v ~/pb/hooks:/pb_hooks \
  -v ~/pb/public:/pb_public \
  docker.io/bakirg/pocketbase-docker:latest
```

#### Using Docker Compose

```yaml
services:
  pocketbase_service:
    image: docker.io/hyzkin/pocketbase-docker-arm64:latest
    container_name: pocketbase_container
    restart: unless-stopped
    ports:
      - "8090:8090"
    volumes:
      - "~/pb/data:/pb_data"
      - "~/pb/migrations:/pb_migrations" 
      - "~/pb/hooks:/pb_hooks" 
      - "~/pb/public:/pb_public" 
    healthcheck:
      test: wget -q --spider http://localhost:8090/api/health || exit 1
      interval: 30s
      timeout: 5s
      retries: 3
      start_period: 5s
```

### Accessing PocketBase

- **Admin UI:** [http://localhost:8090/_/](http://localhost:8090/_/)
- **API Endpoint:** [http://localhost:8090/api/](http://localhost:8090/api/)
- **Health Check** [http://localhost:8090/api/health](http://localhost:8090/api/health)

## Contributing

I welcome contributions to improve the Docker images and configurations. Please open issues or pull requests on GitHub.

## License

This project is licensed under the [MIT License](LICENSE).

## Contact

For any (adequate) inquiries, please contact [me@bakir.dev](mailto:me@bakir.dev).
