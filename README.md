# OpenBAS Docker Deployment

Welcome to the OpenBAS Docker deployment guide! This guide provides resources and information to help you deploy and
manage OpenBAS using Docker.

---

## 📚 Documentation

For detailed instructions on installing OpenBAS using Docker, refer to
the [OpenBAS documentation space](https://docs.openbas.io/latest/deployment/installation/#using-docker).

---

## 👥 Community

### 🛠️ Status & Bugs

OpenBAS is actively under development. If you encounter bugs, have feature requests, or need help, please report them
using the [GitHub Issues module](https://github.com/OpenBAS-Platform/openbas/issues). We appreciate your feedback and
contributions to improve the platform.

### 💬 Discussions

Join our community to engage in discussions, share ideas, and get support:

- **Slack Channel:** Connect with us on [Slack](https://community.filigran.io)

---

## 🔧 Deployment Overview

### Quick Start with Docker Compose

The OpenBAS stack is modular and uses multiple Docker Compose files for easier configuration:

> [!IMPORTANT]
> Remember to create a .env file from .env.sample and customize the configuration as needed.

To start OpenBAS with the essential services, run:
```bash
   docker compose -p openbas -f docker-compose.yml up -d
```

To start OpenBAS with the Caldera executor (Caldera used as an agent), run:
```bash
   docker compose -p openbas -f docker-compose.yml -f docker-compose.caldera.yml -f docker-compose.caldera-executor.yml up -d
```

To start OpenBAS with the Caldera injector (Caldera used as an implant), run:
```bash
   docker compose -p openbas -f docker-compose.yml -f docker-compose.caldera.yml -f docker-compose.caldera-injector.yml up -d
```

#### Build Your Own Stack
OpenBAS allows you to customize your stack by selecting specific collectors and injectors to meet your unique needs:

- Additional Collectors: Explore a variety of collectors available [here](https://filigran.notion.site/OpenBAS-Ecosystem-30d8eb73d7d04611843e758ddef8941b#fb5f20e515df428994bed1438131cbd1).
- Additional Injectors: Discover injectors to enhance your simulations [here](https://filigran.notion.site/OpenBAS-Ecosystem-30d8eb73d7d04611843e758ddef8941b#90cfcc2895d441d68b54eda9b57d5d31).

## About

OpenBAS is a product designed and developed by the company [Filigran](https://filigran.io).

<a href="https://filigran.io" alt="Filigran"><img src="https://github.com/OpenBAS-Platform/openbas/raw/master/.github/img/logo_filigran.png" width="300" /></a>
