# Dev Container Templates

This repository contains a Dev Container templates for development.

## Templates

### python-node-postgres

Development container with Python, Node.js, PostgreSQL, and modern tooling (mise, uv, just).

**Features:**

- Python
- Node.js
- PostgreSQL (via Docker Compose)
- Modern tooling: mise, uv, just
- Ubuntu base image

**Options:**

- `pythonVersion`: Python version to install via mise (default: 3.14.2)
- `nodeVersion`: Node.js version to install via mise (default: 24.12.0)
- `postgresVersion`: PostgreSQL version for the database service (default: 18.1)
- `ubuntuVersion`: Ubuntu base image version (default: 25.04)
- `packageManager`: Node.js package manager to install (default: pnpm)

## License

See repository license file for details.
