# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Development Commands

### Primary Commands
- `yarn dev` - Start all services in development mode (web on port 4000, api on port 8081)
- `yarn build` - Build all apps and packages using Turbo
- `yarn test` - Run tests across all workspaces
- `yarn lint` - Run linting across all workspaces
- `yarn format` - Format code using Prettier

### Development Setup
- `./start-dev.sh` - Sets up development environment (creates .env files, starts Docker services)
- Docker services include PostgreSQL (port 5432), Jupyter (port 8888), and demo ecommerce DB (port 5433)

### Individual App Commands
- API: `cd apps/api && yarn dev` (starts on port 8081)
- Web: `cd apps/web && yarn dev` (starts Next.js on port 4000)
- AI service: `cd ai && python main.py` (optional, for AI features)

## Architecture Overview

Briefer is a collaborative notebook and dashboard platform with three main components:

### Core Services
- **Web App** (`apps/web/`): Next.js frontend application for creating notebooks/dashboards
- **API Server** (`apps/api/`): Node.js/Express backend handling data processing, websockets, and notebook execution
- **AI Service** (`ai/`): Optional Python service for code generation features

### Key Technologies
- **Frontend**: Next.js 13, React 18, TailwindCSS, TypeScript
- **Backend**: Node.js, Express, TypeScript, Socket.io for real-time collaboration
- **Database**: PostgreSQL with Prisma ORM
- **Real-time**: Y.js for collaborative editing, websockets for live updates
- **Code Execution**: Jupyter server integration for Python/SQL execution
- **Build System**: Turbo monorepo with Yarn workspaces

### Database Architecture
- Main PostgreSQL database for application data
- Prisma migrations in `packages/database/`
- Demo ecommerce database for examples

### Key Directories
- `apps/web/src/components/` - React components organized by feature
- `apps/web/src/pages/` - Next.js pages using file-based routing
- `apps/api/src/v1/` - REST API routes
- `apps/api/src/websocket/` - WebSocket handlers for real-time features
- `apps/api/src/yjs/` - Y.js collaboration server implementation
- `packages/` - Shared packages (database, editor, types)

### Real-time Collaboration
- Y.js for operational transformation and conflict resolution
- WebSocket connections for live cursors and presence
- Document synchronization across multiple users

### Data Sources Integration
- Supports multiple databases: PostgreSQL, MySQL, BigQuery, Snowflake, Athena, etc.
- Query execution through datasource connectors in `apps/api/src/datasources/`
- Python execution via Jupyter server integration

## Testing and Quality

### Test Commands
- `yarn test` - Run all tests using Jest
- Individual package tests with `--passWithNoTests` flag

### Code Quality
- ESLint configuration with Next.js and custom rules
- Prettier for code formatting
- TypeScript strict mode enabled
- Patch-package for npm package modifications

## Environment Configuration

Development requires specific environment variables:
- Database connection details (PostgreSQL)
- Jupyter server configuration
- JWT secrets for authentication
- Optional OpenAI API key for AI features

The `start-dev.sh` script automatically generates development `.env` files with secure defaults.

## Deployment

- Docker-based deployment with multi-service architecture
- Kubernetes Helm charts available in `chart/`
- Production builds use optimized Docker images
- Environment-specific configurations for cloud deployment