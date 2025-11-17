# Docker Development Environment Template

A fully-featured Docker-based development environment template designed for Next.js applications with PostgreSQL database and MCP (Model Context Protocol) server support.

## Overview

This repository provides a complete, containerized development environment that includes:

- **Next.js Application** - Modern React framework with TypeScript
- **PostgreSQL Database** - Persistent data storage
- **MCP Server** - Model Context Protocol server for AI integrations
- **Pre-configured Tooling** - Essential development tools and VS Code extensions

## Architecture

The environment consists of three Docker services orchestrated via Docker Compose:

### Services

1. **app** - Main application container
   - Based on Node.js 24
   - Runs the Next.js application
   - Exposed on port `3000`
   - Includes pnpm package manager

2. **psql** - PostgreSQL database
   - PostgreSQL server with persistent storage
   - Exposed on port `5432`
   - Default credentials: `root/root`
   - Default database: `db`

3. **mcp** - MCP server container
   - Separate container for MCP server functionality
   - Exposed on port `3001`
   - Shares the same Node.js environment as the app

## Features

### Development Tools

The Docker image includes:
- **pnpm** - Fast, disk space efficient package manager
- **PostgreSQL client** - For database interactions
- **ripgrep** - Fast text search tool
- **fd-find** - Fast file finder
- **git** - Version control
- **net-tools** - Network utilities
- **sudo** - Passwordless sudo access for the node user

### VS Code Integration

Pre-configured with essential extensions:
- Claude Code (Anthropic.claude-code)
- React and Next.js snippets
- Prisma ORM support
- Tailwind CSS IntelliSense
- PostgreSQL client
- Prettier code formatter
- And more...

### Custom Shell Environment

Includes a customizable bash prompt with:
- Git branch display
- Dirty state indicator
- Color-coded status
- Username integration

## Getting Started

### Prerequisites

- Docker and Docker Compose installed
- VS Code with Remote Containers extension (recommended)

### Quick Start

1. Clone this repository:
   ```bash
   git clone <your-repo-url>
   cd <repo-name>
   ```

2. Open in VS Code:
   ```bash
   code .
   ```

3. When prompted, click "Reopen in Container" or use Command Palette:
   - `Remote-Containers: Reopen in Container`

4. The environment will build and start automatically. This may take a few minutes on first run.

5. Once started, your Next.js app will be available at:
   - Application: http://localhost:3000
   - MCP Server: http://localhost:3001
   - PostgreSQL: localhost:5432

## Scripts

### `psql.sh`

Convenience script to connect to the PostgreSQL database.

**Usage:**
```bash
./psql.sh
```

**What it does:**
- Connects to the PostgreSQL container using the psql client
- Uses the default credentials (root/root)
- Connects to the default database (db)
- Connection string: `postgres://root:root@psql/db`

**Example:**
```bash
# Make executable (if needed)
chmod +x psql.sh

# Connect to database
./psql.sh

# You'll be in the PostgreSQL prompt
db=# SELECT version();
```

## Database Configuration

### Default Credentials

- **Host:** `psql` (container name) or `localhost` (from host machine)
- **Port:** `5432`
- **Database:** `db`
- **Username:** `root`
- **Password:** `root`

### Connection Strings

From within containers:
```
postgres://root:root@psql:5432/db
```

From host machine:
```
postgres://root:root@localhost:5432/db
```

### Persistent Storage

Database data is persisted in a Docker volume named `psql`, ensuring your data survives container restarts.

## Customization

### Changing Database Credentials

Edit `.devcontainer/docker-compose.yml`:

```yaml
psql:
  environment:
    POSTGRES_USER: your_username
    POSTGRES_PASSWORD: your_password
    POSTGRES_DB: your_database
```

Remember to update `psql.sh` accordingly.

### Adding More Tools

Edit `.devcontainer/Dockerfile` and add to the apt install section:

```dockerfile
RUN apt -y install postgresql \
    postgresql-client \
    ripgrep \
    your-new-tool
```

### Adding VS Code Extensions

Edit `.devcontainer/devcontainer.json` under `customizations.vscode.extensions`:

```json
"extensions": [
  "existing.extension",
  "your.new-extension"
]
```