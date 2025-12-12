# mysql-mcp

*Enterprise-grade MySQL MCP Server with OAuth 2.0 authentication, connection pooling & tool filtering – TypeScript Edition*

> **⚠️ UNDER DEVELOPMENT** - This project is actively being developed and is not yet ready for production use.

[![GitHub](https://img.shields.io/badge/GitHub-neverinfamous/mysql--mcp-blue?logo=github)](https://github.com/neverinfamous/mysql-mcp)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![CodeQL](https://github.com/neverinfamous/mysql-mcp/actions/workflows/codeql.yml/badge.svg)](https://github.com/neverinfamous/mysql-mcp/actions/workflows/codeql.yml)
![Version](https://img.shields.io/badge/version-0.1.0-green)
![Status](https://img.shields.io/badge/status-Under%20Development-orange)
[![Security](https://img.shields.io/badge/Security-Enhanced-green.svg)](SECURITY.md)
![TypeScript](https://img.shields.io/badge/TypeScript-Strict-blue.svg)

A **MySQL MCP Server** with OAuth 2.0 authentication, connection pooling, and granular access control. Written in TypeScript.

**[Wiki](https://github.com/neverinfamous/mysql-mcp/wiki)** • **[Changelog](CHANGELOG.md)** • **[Security](SECURITY.md)**

---

## 📋 Table of Contents

### Quick Start
- [🚀 Quick Start](#-quick-start)
- [⚡ Install to Cursor IDE](#-install-to-cursor-ide)

### Configuration & Usage
- [📚 MCP Client Configuration](#-mcp-client-configuration)
- [🔌 Connection Pooling](#-connection-pooling)
- [🎛️ Tool Filtering](#️-tool-filtering)
- [📊 Tool Categories](#-tool-categories)

### Features & Resources
- [🔥 Core Capabilities](#-core-capabilities)
- [🔐 OAuth 2.0 Implementation](#-oauth-20-implementation)
- [🏆 Why Choose mysql-mcp?](#-why-choose-mysql-mcp)

---

## 🚀 Quick Start

### Prerequisites

- Node.js 18+
- MySQL 5.7+ or 8.0+ server
- npm or yarn

### Installation

Clone the repository:
```bash
git clone https://github.com/neverinfamous/mysql-mcp.git
```

Navigate to directory:
```bash
cd mysql-mcp
```

Install dependencies:
```bash
npm install
```

Build the project:
```bash
npm run build
```

Run the server:
```bash
node dist/cli.js --transport stdio --mysql mysql://user:password@localhost:3306/database
```

[⬆️ Back to Table of Contents](#-table-of-contents)

---

## ⚡ Install to Cursor IDE

### Manual Configuration

Add to your Cursor MCP settings:

```json
{
  "mcpServers": {
    "mysql-mcp": {
      "command": "node",
      "args": [
        "C:/path/to/mysql-mcp/dist/cli.js",
        "--transport", "stdio",
        "--mysql", "mysql://user:password@localhost:3306/database"
      ]
    }
  }
}
```

### Prerequisites
- ✅ Node.js 18+
- ✅ MySQL server running and accessible

[⬆️ Back to Table of Contents](#-table-of-contents)

---

## 📚 MCP Client Configuration

### Cursor IDE

```json
{
  "mcpServers": {
    "mysql-mcp": {
      "command": "node",
      "args": [
        "C:/path/to/mysql-mcp/dist/cli.js",
        "--transport", "stdio",
        "--mysql", "mysql://user:password@localhost:3306/database"
      ]
    }
  }
}
```

### Claude Desktop

```json
{
  "mcpServers": {
    "mysql-mcp": {
      "command": "node",
      "args": [
        "/path/to/mysql-mcp/dist/cli.js",
        "--transport", "stdio",
        "--mysql", "mysql://user:password@localhost:3306/database"
      ]
    }
  }
}
```

### Environment Variables

For security, use environment variables instead of connection strings:

```json
{
  "mcpServers": {
    "mysql-mcp": {
      "command": "node",
      "args": [
        "C:/path/to/mysql-mcp/dist/cli.js",
        "--transport", "stdio"
      ],
      "env": {
        "MYSQL_HOST": "localhost",
        "MYSQL_PORT": "3306",
        "MYSQL_USER": "your_user",
        "MYSQL_PASSWORD": "your_password",
        "MYSQL_DATABASE": "your_database"
      }
    }
  }
}
```

[⬆️ Back to Table of Contents](#-table-of-contents)

---

## 🔌 Connection Pooling

Unlike SQLite (file-based), MySQL is a server-based database that benefits from connection pooling. This server uses `mysql2` with built-in connection pooling.

### Configuration

| Option | Default | Description |
|--------|---------|-------------|
| `MYSQL_POOL_SIZE` | 10 | Maximum connections in pool |
| `MYSQL_POOL_TIMEOUT` | 10000 | Connection timeout (ms) |

### Example with Pool Settings

```json
{
  "env": {
    "MYSQL_HOST": "localhost",
    "MYSQL_PORT": "3306",
    "MYSQL_USER": "app_user",
    "MYSQL_PASSWORD": "secure_password",
    "MYSQL_DATABASE": "production",
    "MYSQL_POOL_SIZE": "20",
    "MYSQL_POOL_TIMEOUT": "30000"
  }
}
```

[⬆️ Back to Table of Contents](#-table-of-contents)

---

## 🎛️ Tool Filtering

> [!IMPORTANT]
> **AI-enabled IDEs like Cursor have tool limits.** Use tool filtering to stay within limits.

### Tool Groups

| Group | Description |
|-------|-------------|
| `core` | Basic CRUD, schema, tables |
| `json` | JSON operations (MySQL 5.7+) |
| `text` | FULLTEXT, LIKE, REGEXP |
| `performance` | EXPLAIN, query analysis |
| `replication` | Master/slave status |
| `backup` | mysqldump integration |
| `monitoring` | SHOW PROCESSLIST, status |
| `admin` | OPTIMIZE, ANALYZE, FLUSH |

### Custom Filtering

```bash
# Disable performance and replication tools
--tool-filter "-performance,-replication"
```

[⬆️ Back to Table of Contents](#-table-of-contents)

---

## 📊 Tool Categories

> **Coming Soon** - Tool implementation is in progress.

| Category | Estimated Tools | Description |
|----------|-----------------|-------------|
| Core Database | 8 | Schema, SQL, CRUD operations |
| JSON Operations | 8 | Native JSON functions (MySQL 5.7+) |
| Text Processing | 5 | FULLTEXT, LIKE, REGEXP |
| Performance | 8 | EXPLAIN, query analysis, index hints |
| Replication | 5 | Master/slave status, binlog |
| Backup/Recovery | 4 | mysqldump integration |
| Monitoring | 7 | SHOW PROCESSLIST, status vars |
| Admin | 5 | OPTIMIZE, ANALYZE, FLUSH |
| **Total** | **~50** | |

[⬆️ Back to Table of Contents](#-table-of-contents)

---

## 🔥 Core Capabilities

- 📊 **Full SQL Support** - Execute any MySQL query with parameter binding
- 🔍 **JSON Operations** - Native JSON functions (MySQL 5.7+)
- 🔐 **Connection Pooling** - Efficient connection management
- 🎛️ **Tool Filtering** - Control which operations are exposed
- ⚡ **Performance Tools** - EXPLAIN, query analysis, optimization hints

### 🏢 Enterprise Features

- 🔐 **OAuth 2.0 Authentication** - RFC 9728/8414 compliant
- 🛡️ **Tool Filtering** - Control which database operations are exposed
- 👥 **Access Control** - Granular scopes for read-only, write, and admin access
- 📈 **Monitoring** - Process lists, status variables, performance metrics

[⬆️ Back to Table of Contents](#-table-of-contents)

---

## 🔐 OAuth 2.0 Implementation

| Component | Status | Description |
|-----------|--------|-------------|
| Protected Resource Metadata | 🔄 | RFC 9728 `/.well-known/oauth-protected-resource` |
| Auth Server Discovery | 🔄 | RFC 8414 metadata discovery |
| Token Validation | 🔄 | JWT validation with JWKS support |
| Scope Enforcement | 🔄 | Granular `read`, `write`, `admin` scopes |
| HTTP Transport | 🔄 | Streamable HTTP with OAuth middleware |

### Supported Scopes

| Scope | Description |
|-------|-------------|
| `read` | Read-only access to all databases |
| `write` | Read and write access to all databases |
| `admin` | Full administrative access |
| `db:{name}` | Access to specific database only |
| `table:{db}:{table}` | Access to specific table only |

[⬆️ Back to Table of Contents](#-table-of-contents)

---

## 🏆 Why Choose mysql-mcp?

✅ **TypeScript Native** - Full type safety with strict mode  
✅ **Connection Pooling** - Efficient MySQL connection management  
✅ **OAuth 2.0 Built-in** - Enterprise-grade authentication  
✅ **Tool Filtering** - Stay within AI IDE tool limits  
✅ **Modern Architecture** - Built on MCP SDK  
✅ **Active Development** - Regular updates and improvements

[⬆️ Back to Table of Contents](#-table-of-contents)

---

## Configuration

### Environment Variables

Copy `.env.example` to `.env` and configure:

```bash
MYSQL_HOST=localhost
MYSQL_PORT=3306
MYSQL_USER=root
MYSQL_PASSWORD=your_password_here
MYSQL_DATABASE=your_database
MYSQL_POOL_SIZE=10
```

---

## Contributing

Contributions are welcome! Please read our [Contributing Guidelines](CONTRIBUTING.md) before submitting a pull request.

## Security

For security concerns, please see our [Security Policy](SECURITY.md).

> **⚠️ Never commit credentials** - Store secrets in `.env` (gitignored)

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Code of Conduct

Please read our [Code of Conduct](CODE_OF_CONDUCT.md) before participating in this project.
