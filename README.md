# Railway Postgres with pgvector

This repository contains a custom PostgreSQL Docker image for Railway that includes the [pgvector](https://github.com/pgvector/pgvector) extension, enabling vector similarity search capabilities.

## Quick Start

1. Create a new Railway project:
   - Go to [Railway](https://railway.app/)
   - Click "New Project"
   - Select "Empty Project"

2. Add Your Repository:
   - Fork this repository
   - In your Railway project, click "Add Service"
   - Select "GitHub Repo"
   - Choose your forked repository
   - Click "Deploy"

3. Configure Environment Variables:
   - In your service settings, add these variables:
    ```ts
    POSTGRES_USER=postgres
    POSTGRES_PASSWORD=your_secure_password
    POSTGRES_DB=railway

4. Wait for Deployment:
- Railway will automatically build and deploy your container
- You can monitor the build process in the "Deployments" tab