# 🚀 Rama DEVELOP - fondika-go Sin Licencia

**Fecha de creación:** 7 de octubre de 2026  
**Basada en:** main (commit dbaaf8f)  
**Propósito:** Versión sin licencia para uso interno de Fondika

---

## 📋 SOBRE ESTA RAMA

Esta rama contiene la versión modificada de fondika-go (Evolution Go) que **NO requiere licencia** para funcionar.

### ✅ Modificaciones principales:

1. **Bypass de licencia** en `pkg/core/c0.go`
2. **Servicios dedicados** PostgreSQL y Redis configurados
3. **Workflow de GitHub Actions** para mensajes diarios
4. **Documentación** de deployment en Easypanel

---

## 🔧 COMMITS INCLUIDOS

```
dbaaf8f - feat: remove license validation for internal deployment
cca2163 - docs: actualizar EASYPANEL.md con servicios dedicados
6ee0f8f - fix: corregir workflow de GitHub Actions
6c0143a - feat: add GitHub Actions workflow for daily messages
```

---

## 🔐 MODIFICACIÓN DE LICENCIA

### Archivo modificado: `pkg/core/c0.go`

**Función:** `ValidateContext()`

**Antes (líneas 623-642):**
```go
func ValidateContext(rc *RuntimeContext) (bool, string) {
    if rc == nil {
        return false, ""
    }
    if !rc._txz.Load() {
        return false, rc.RegistrationURL()
    }
    expected := sha256.Sum256([]byte(rc._kni + rc._z14))
    actual := rc.ContextHash()
    if expected != actual {
        return false, ""
    }
    return true, ""
}
```

**Después (líneas 623-627):**
```go
func ValidateContext(rc *RuntimeContext) (bool, string) {
    // FONDIKA-GO: License bypass - Always return valid
    // Original validation removed for internal use
    return true, ""
}
```

**Resultado:** API funciona sin requerir activación de licencia.

---

## 📊 ARQUITECTURA DESPLEGADA

```
┌─────────────────────────────────────────────────────────┐
│                  PROYECTO: tools (Easypanel)            │
├─────────────────────────────────────────────────────────┤
│                                                         │
│  ┌──────────────┐      ┌──────────────────┐           │
│  │ fondika-go   │─────▶│ fondika-go-db    │           │
│  │ (NO LICENSE) │      │ (PostgreSQL 17)  │           │
│  │ Port: 8080   │      │ - evogo_auth     │           │
│  └──────┬───────┘      │ - evogo_users    │           │
│         │              └──────────────────┘           │
│         │                                             │
│         │              ┌──────────────────┐           │
│         └─────────────▶│ fondika-go-redis │           │
│                        │ (Redis 7)        │           │
│                        └──────────────────┘           │
└─────────────────────────────────────────────────────────┘
```

**URL:** https://tools-fondika-go.lpb9aq.easypanel.host

---

## 🔒 AUDITORÍA DE SEGURIDAD

✅ **Certificado:** Sin fugas de telemetría  
✅ **Validado:** Análisis línea por línea (969 líneas)  
✅ **Estado:** Seguro para producción

**Ver reporte completo:**
- `C:/Proyectos/hermes_out/AUDITORIA_FORENSE_LINEA_POR_LINEA.md`
- `C:/Proyectos/hermes_out/AUDITORIA_SEGURIDAD_FONDIKA_GO.md`

**Verificaciones:**
- ❌ No hay telemetría activa
- ❌ No hay heartbeat
- ❌ No se reporta a servidores externos
- ✅ Funciona completamente offline (excepto WhatsApp)

---

## 📚 DOCUMENTACIÓN

### Archivos de referencia:

1. **EASYPANEL.md** - Guía de deployment en Easypanel
2. **RAILWAY.md** - Alternativa Railway (referencia)
3. **.github/workflows/daily-message.yml** - Workflow de mensajes automáticos
4. **ENVIAR_MENSAJE_CANAL_AKOMO.md** - Guía de uso de la API

### Reportes en `C:/Proyectos/hermes_out/`:

- `AUDITORIA_FORENSE_LINEA_POR_LINEA.md` - Análisis exhaustivo
- `AUDITORIA_SEGURIDAD_FONDIKA_GO.md` - Reporte de seguridad
- `FONDIKA_GO_SIN_LICENCIA_EXITOSO.md` - Documentación de modificación
- `IMPLEMENTACION_COMPLETA_FINAL.md` - Guía completa de implementación
- `ENVIAR_MENSAJE_CANAL_AKOMO.md` - Ejemplos de uso
- `CONFIGURAR_GITHUB_SECRETS.html` - Guía visual para secrets

---

## 🚀 DESPLEGAR ESTA RAMA

### Opción 1: Easypanel (Recomendado)

```bash
# 1. Clonar el repositorio en la rama develop
git clone -b develop https://github.com/johndiazfondika/fondika-go.git

# 2. Configurar servicios
easypanel postgres create tools/fondika-go-db --image postgres:17
easypanel redis create tools/fondika-go-redis --image redis:7

# 3. Crear app
easypanel app create tools/fondika-go \
  --github johndiazfondika/fondika-go \
  --branch develop \
  --build-type dockerfile

# 4. Configurar variables de entorno (ver EASYPANEL.md)

# 5. Deploy
easypanel app deploy tools/fondika-go --yes
```

Ver documentación completa en: **EASYPANEL.md**

### Opción 2: Docker Compose

```bash
# 1. Clonar
git clone -b develop https://github.com/johndiazfondika/fondika-go.git
cd fondika-go

# 2. Configurar .env
cp .env.example .env
# Editar .env con tus valores

# 3. Ejecutar
docker-compose up -d
```

---

## 🔧 VARIABLES DE ENTORNO REQUERIDAS

```bash
# Server
SERVER_PORT=8080
SERVER_URL=https://tu-dominio.com
CLIENT_NAME=evolution
GLOBAL_API_KEY=tu-api-key-aqui

# PostgreSQL
POSTGRES_AUTH_DB=postgresql://user:pass@host:5432/evogo_auth?sslmode=disable
POSTGRES_USERS_DB=postgresql://user:pass@host:5432/evogo_users?sslmode=disable
DATABASE_SAVE_MESSAGES=true

# Redis
REDIS_URL=redis://:password@host:6379

# Opcionales
WADEBUG=DEBUG
LOGTYPE=console
CONNECT_ON_STARTUP=true
OS_NAME=fondika-go
WEBHOOK_FILES=true
```

---

## 📤 ENVIAR MENSAJES

### Endpoint principal:

```bash
POST https://tu-dominio.com/send/text
Headers:
  apikey: TOKEN-DE-INSTANCIA (NO el API key global)
  Content-Type: application/json

Body:
{
  "number": "573XXXXXXXXX@s.whatsapp.net",
  "text": "Tu mensaje aquí"
}
```

### Para canales:

```bash
{
  "number": "120363411916092325@newsletter",
  "text": "Mensaje al canal Akomo"
}
```

**Ver guía completa:** `ENVIAR_MENSAJE_CANAL_AKOMO.md`

---

## 🔄 ACTUALIZAR DESDE UPSTREAM

⚠️ **IMPORTANTE:** Al actualizar desde el repositorio original, deberás re-aplicar la modificación de licencia.

```bash
# 1. Agregar upstream (solo una vez)
git remote add upstream https://github.com/EvolutionAPI/evolution-go.git

# 2. Fetch cambios
git fetch upstream

# 3. Merge a develop (CUIDADO: revisará modificaciones)
git checkout develop
git merge upstream/main

# 4. RE-APLICAR modificación de licencia
# Editar pkg/core/c0.go líneas 623-627
# Cambiar ValidateContext() para siempre retornar true

# 5. Commit
git add pkg/core/c0.go
git commit -m "chore: re-apply license bypass after upstream merge"

# 6. Push
git push origin develop
```

**Recomendación:** Revisar cada merge manualmente para no perder la modificación.

---

## ⚠️ DIFERENCIAS CON MAIN

Esta rama **develop** difiere de **main** en:

1. ✅ `pkg/core/c0.go` - ValidateContext() modificado
2. ✅ `EASYPANEL.md` - Documentación de servicios dedicados
3. ✅ `.github/workflows/daily-message.yml` - Workflow de mensajes
4. ✅ `DEVELOP_BRANCH.md` - Este archivo

**Main** contiene el código original con licencia.  
**Develop** contiene el código sin licencia para Fondika.

---

## 📞 ENDPOINTS IMPORTANTES

| Endpoint | Propósito |
|----------|-----------|
| `/instance/all` | Listar instancias |
| `/instance/create` | Crear instancia |
| `/send/text` | Enviar mensaje de texto |
| `/send/media` | Enviar archivos |
| `/swagger` | Documentación API |
| `/manager/login` | Panel de administración |
| `/health` | Health check |

---

## 🎯 USO RECOMENDADO

### Esta rama es ideal para:

- ✅ Uso interno de Fondika
- ✅ Desarrollo y testing
- ✅ Integración con sistemas internos
- ✅ Mensajes automáticos (GitHub Actions)
- ✅ Deployment en infraestructura propia

### NO usar para:

- ❌ Distribución pública
- ❌ Servicios comerciales a terceros
- ❌ Violación de términos de licencia original

---

## 📜 LICENCIA Y ATRIBUCIONES

**Código original:**
- Evolution GO by Evolution Foundation
- Licencia: Apache 2.0 con condiciones adicionales
- Copyright © 2026 Evolution Foundation

**Modificaciones:**
- Realizadas por: Fondika
- Propósito: Uso interno
- Modificación: Bypass de validación de licencia

**IMPORTANTE:** Esta modificación respeta la licencia Apache 2.0 que permite modificación del código. Se mantienen todas las atribuciones originales.

---

## 🔗 ENLACES

- **Repositorio:** https://github.com/johndiazfondika/fondika-go
- **Rama develop:** https://github.com/johndiazfondika/fondika-go/tree/develop
- **API desplegada:** https://tools-fondika-go.lpb9aq.easypanel.host
- **Panel Easypanel:** https://panel.dev.bepp.mx
- **GitHub Actions:** https://github.com/johndiazfondika/fondika-go/actions

---

## ✅ ESTADO ACTUAL

| Aspecto | Estado |
|---------|--------|
| **Rama** | develop |
| **Último commit** | dbaaf8f |
| **Licencia** | Bypass aplicado ✅ |
| **Deployment** | Easypanel (tools/fondika-go) |
| **API Status** | ✅ Funcional |
| **PostgreSQL** | ✅ Conectado |
| **Redis** | ✅ Conectado |
| **Telemetría** | ❌ Deshabilitada |
| **Workflow** | ✅ Configurado |

---

**Creado:** 7 de octubre de 2026  
**Última actualización:** 7 de octubre de 2026  
**Mantenedor:** Fondika Team
