# 🚀 Deploy fondika-go en Easypanel

Este documento describe el despliegue de fondika-go en Easypanel.

## ✅ Estado Actual del Deployment

- **URL**: https://tools-fondika-go.lpb9aq.easypanel.host
- **Proyecto**: tools
- **Servicio**: fondika-go
- **Commit**: 6c0143a3
- **Estado**: Activo ✓

## Variables de Entorno Configuradas

```bash
# Server Configuration
SERVER_PORT=80
CLIENT_NAME=evolution

# API Security
GLOBAL_API_KEY=9719549FD0D877B1B95C0518A156C92C

# Database Configuration
POSTGRES_AUTH_DB=postgresql://postgres:***@fondika-go-db:5432/evogo_auth
POSTGRES_USERS_DB=postgresql://postgres:***@fondika-go-db:5432/evogo_users

# Redis Configuration
REDIS_URL=redis://:***@fondika-go-redis:6379

# Database Options
DATABASE_SAVE_MESSAGES=true

# Logging
WADEBUG=DEBUG
LOGTYPE=console

# Startup
CONNECT_ON_STARTUP=true

# Branding
OS_NAME=fondika-go Easypanel

# Webhook
WEBHOOK_FILES=true
```

## Servicios Relacionados

El proyecto `tools` incluye:

### Servicios fondika-go (dedicados)

1. **fondika-go** - API principal
2. **fondika-go-db** - PostgreSQL 17 (dedicado)
3. **fondika-go-redis** - Redis 7 (dedicado)

### Servicios Evolution API (legacy)

4. **evolution-api** - Evolution API v2.3.7
5. **evolution-api-db** - PostgreSQL 17
6. **evolution-api-redis** - Redis 7

## Configuración con Easypanel CLI

### Prerequisitos

```bash
# Instalar Easypanel CLI (Windows)
irm https://get.easypanel.io/cli.ps1 | iex

# Conectar al servidor
easypanel server add production https://panel.dev.bepp.mx
```

### Comandos Útiles

```bash
# Ver información del servicio
easypanel app inspect tools/fondika-go

# Ver logs
easypanel app logs tools/fondika-go --tail 50

# Redesplegar
easypanel app deploy tools/fondika-go --yes

# Reiniciar
easypanel app restart tools/fondika-go --yes

# Actualizar variables de entorno
easypanel app update-env tools/fondika-go --env "KEY=VALUE" --yes
```

## Build Configuration

- **Source**: GitHub (johndiazfondika/fondika-go)
- **Branch**: main
- **Build Type**: Dockerfile
- **Dockerfile**: `/Dockerfile`
- **Auto Deploy**: Deshabilitado (deploy manual)

## Domain Configuration

- **Host**: tools-fondika-go.lpb9aq.easypanel.host
- **HTTPS**: Habilitado (Let's Encrypt)
- **Port**: 80 (interno)
- **Protocol**: HTTP (interno)

## Health Check

Verificar que el servicio esté corriendo:

```bash
curl https://tools-fondika-go.lpb9aq.easypanel.host/instance/all \
  -H "apikey: 9719549FD0D877B1B95C0518A156C92C"
```

Respuesta esperada:
```json
{
  "instances": [...]
}
```

## GitHub Actions Integration

El workflow `.github/workflows/daily-message.yml` usa este deployment:

```yaml
env:
  FONDIKA_API_URL: https://tools-fondika-go.lpb9aq.easypanel.host
  FONDIKA_API_KEY: ${{ secrets.FONDIKA_API_KEY }}
  CANAL_AKOMO_ID: ${{ secrets.CANAL_AKOMO_ID }}
```

### Secrets Requeridos

En GitHub Settings → Secrets → Actions:

1. **FONDIKA_API_URL**: `https://tools-fondika-go.lpb9aq.easypanel.host`
2. **FONDIKA_API_KEY**: `9719549FD0D877B1B95C0518A156C92C`
3. **CANAL_AKOMO_ID**: `120363411916092325@newsletter`

## Troubleshooting

### Verificar logs en tiempo real

```bash
easypanel app logs tools/fondika-go --follow
```

### Reiniciar servicio

```bash
easypanel app restart tools/fondika-go --yes
```

### Redesplegar desde GitHub

```bash
easypanel app deploy tools/fondika-go --yes
```

### Ver información completa del proyecto

```bash
easypanel projects inspect tools --format json
```

## Deployment URL (Webhook)

Para triggers automáticos desde CI/CD:

```
http://158.23.177.12:3000/api/deploy/0a885314a83de85039ccc10a18b39b7aaedd9670c20485e6
```

## Monitoreo

- Panel Web: https://panel.dev.bepp.mx
- Logs: `easypanel app logs tools/fondika-go`
- Uptime: Monitoreado por Easypanel
- SSL: Auto-renovado por Let's Encrypt

## Costos

- **Hosting**: Según plan Easypanel contratado
- **GitHub Actions**: $0/mes (Free tier)
- **Total workflow (1 mensaje/día)**: ~$0/mes en ejecución

## Soporte

- Easypanel Docs: https://easypanel.io/docs
- GitHub Issues: https://github.com/johndiazfondika/fondika-go/issues
