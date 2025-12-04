# Backend - Proyecto Buenaventura

API REST Laravel 11 para el sistema de recolección de basura en Buenaventura.

## 🚀 Despliegue en Railway - PASO A PASO

### PASO 1: Verificar archivos (YA COMPLETADO ✅)
- ✅ `Procfile` - Configuración de ejecución
- ✅ `runtime.txt` - Versión de PHP 8.2.14
- ✅ `composer.json` - Dependencias
- ✅ `.env.example` - Variables de ejemplo

### PASO 2: En Railway Dashboard

**2.1 Conectar repositorio:**
1. Ve a https://railway.app
2. Nuevo proyecto → Deploy from GitHub
3. Selecciona: `junior1318/backend-buenaventura`

**2.2 Agregar MySQL:**
1. En el proyecto → Create
2. Selecciona MySQL
3. Espera a que se configure

**2.3 Configurar Variables de Entorno:**
1. En el proyecto → Variables
2. Copia y pega EXACTAMENTE esto:

```
APP_NAME=Proyecto Buenaventura
APP_ENV=production
APP_DEBUG=false
APP_KEY=base64:OGY3NDI5ZjctZWQyYS00ZDJmLWFkZDMtMjM1MjUxMjc1ZDhhODk5MDMxOWYtY2U1MS00NTg5LWJiYzEtN2IyOTE4OWEzMGUz
LOG_CHANNEL=stack
LOG_LEVEL=debug
CACHE_DRIVER=database
QUEUE_CONNECTION=database
SESSION_DRIVER=database
SESSION_LIFETIME=120
EXTERNAL_API_BASE_URL=http://apirecoleccion.gonzaloandreslucio.com/api
EXTERNAL_API_TIMEOUT=10
GLOBAL_PERFIL_ID=
DB_CONNECTION=mysql
DB_HOST=${{ Mysql.MYSQL_HOST }}
DB_PORT=3306
DB_DATABASE=${{ Mysql.MYSQL_DATABASE }}
DB_USERNAME=${{ Mysql.MYSQL_USER }}
DB_PASSWORD=${{ Mysql.MYSQL_PASSWORD }}
APP_URL=https://tu-dominio.up.railway.app
```

⚠️ IMPORTANTE:
- NO cambies las variables `${{ }}` - Railway las completa automáticamente
- Reemplaza `tu-dominio` con tu dominio real de Railway

**2.4 Redeploy:**
1. Click en **Redeploy** (arriba a la derecha)
2. Espera a que termine
3. Verifica en **Logs** que no haya errores

### PASO 3: Verificar que funciona

```bash
curl https://tu-dominio.up.railway.app
```

## 📁 Estructura del Proyecto

```
app/              - Código de la aplicación
config/           - Configuración
database/         - Migraciones y seeders
public/           - Punto de entrada (index.php)
routes/           - Rutas API
storage/          - Caché y logs
tests/            - Tests unitarios
```

## 🔧 Desarrollo local

```bash
# Instalar dependencias
composer install

# Copiar .env
cp .env.example .env

# Generar APP_KEY
php artisan key:generate

# Ejecutar migraciones
php artisan migrate

# Iniciar servidor
php artisan serve
```

## 📝 Requisitos

- PHP: 8.2+
- MySQL: 5.7+
- Composer: 2.0+
- Laravel: 11.0

```
DB_DATABASE=laravel_db
DB_USERNAME=laravel_user
DB_PASSWORD=laravel_pass
```
