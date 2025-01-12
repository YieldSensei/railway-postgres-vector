# Railway Postgres with pgvector

This repository contains a custom PostgreSQL Docker image for Railway that includes the [pgvector](https://github.com/pgvector/pgvector) extension. This allows you to use vector similarity search capabilities in your Railway PostgreSQL database.

The image is based on Railway's official PostgreSQL image (`ghcr.io/railwayapp-templates/postgres-ssl:16`) and adds pgvector support.

## Features

- PostgreSQL 16 with SSL support
- pgvector extension (v0.5.1) for vector similarity search
- Built on Railway's official Postgres image
- Automatic configuration of shared preload libraries

## Quick Start

1. Fork this repository or create a new one using these files
2. In Railway:
   - Create a new project (or use existing)
   - Add a new service
   - Choose "Empty Service"
   - Connect your GitHub repository
   - Add required environment variables (see below)

### Required Environment Variables

Add these in your Railway service settings:

```
POSTGRES_USER=postgres
POSTGRES_PASSWORD=<your-desired-password>
POSTGRES_DB=railway
```

## Verifying Installation

Once deployed, connect to your database using psql:

```bash
psql <your-railway-connection-string>
```

Then create and test the vector extension:

```sql
-- Create the extension
CREATE EXTENSION vector;

-- Test with a simple vector
CREATE TABLE items (id bigserial PRIMARY KEY, embedding vector(3));
INSERT INTO items (embedding) VALUES ('[1,2,3]');
SELECT * FROM items;
```

## Common Issues

1. If the database crashes on deployment:
   - Check Railway logs for specific error messages
   - Verify environment variables are set correctly
   - Ensure you have sufficient resources allocated

2. If vector extension creation fails:
   - Verify the database has fully started (check logs)
   - Ensure you're using the correct connection string
   - Check if the extension is already created

## Migration Guide

If you're migrating from a standard Railway Postgres database:

1. Create a backup of your existing database:
   ```bash
   pg_dump -h old-host -U old-user -d old-db > backup.sql
   ```

2. Deploy this new database service

3. Restore your data:
   ```bash
   psql -h new-host -U new-user -d new-db < backup.sql
   ```

4. Create the vector extension:
   ```sql
   CREATE EXTENSION vector;
   ```

## Why Use This?

- Need vector similarity search in your Railway PostgreSQL database
- Want to store and query embeddings (e.g., for AI/ML applications)
- Need compatibility with tools like LangChain, LlamaIndex that expect pgvector

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

MIT License - feel free to use this in your own projects.