# 🚀 Deploy fondika-go en Railway

Este archivo configura las variables de entorno necesarias para Railway.

## Variables de Entorno Requeridas

Configurar en Railway Dashboard → Variables:

```bash
# Server Configuration
SERVER_PORT=8080
CLIENT_NAME=evolution

# API Security
GLOBAL_API_KEY=9719549FD0D877B1B95C0518A156C92C

# Database Configuration (Railway provee automáticamente)
POSTGRES_AUTH_DB=${{Postgres.DATABASE_URL}}/evogo_auth?sslmode=require
POSTGRES_USERS_DB=${{Postgres.DATABASE_URL}}/evogo_users?sslmode=require

# Database Options
DATABASE_SAVE_MESSAGES=true

# Logging
WADEBUG=DEBUG
LOGTYPE=console

# Startup
CONNECT_ON_STARTUP=true

# Branding
OS_NAME=fondika-go Railway

# Webhook
WEBHOOK_FILES=true
```

## Databases Requeridas

1. **PostgreSQL** - Railway proveerá automáticamente `DATABASE_URL`
2. **Redis** - Railway proveerá automáticamente `REDIS_URL`

## Configuración de Bases de Datos

Después de crear PostgreSQL en Railway, crear las bases de datos:

```sql
CREATE DATABASE evogo_auth;
CREATE DATABASE evogo_users;
```

## Health Check

Una vez desplegado, verificar:

```bash
curl https://tu-app.up.railway.app/instance/all \
  -H "apikey: 9719549FD0D877B1B95C0518A156C92C"
```

## Port Configuration

Railway detecta automáticamente el puerto desde `SERVER_PORT=8080`.
No es necesario configurar `PORT` manualmente.
