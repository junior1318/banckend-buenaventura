# Despliegue en Railway

## Requisitos previos
- Cuenta en [Railway.app](https://railway.app)
- Repositorio en GitHub
- Backend Laravel en la carpeta `proyecto-buenaventura/backend-laravel`

## Pasos para desplegar

### 1. Conectar el repositorio a Railway
1. Ve a [railway.app](https://railway.app) y crea un nuevo proyecto
2. Selecciona "Deploy from GitHub"
3. Conecta tu repositorio `proyecto-basura`

### 2. Configurar la raíz del proyecto
En Railway, en la configuración del servicio:
- Root Directory: `proyecto-buenaventura/backend-laravel`

### 3. Configurar variables de entorno
Railway detectará automáticamente que es un proyecto Laravel. Agrega estas variables en el dashboard:

```
APP_ENV=production
APP_DEBUG=false
APP_URL=https://your-app-name.up.railway.app
APP_KEY=base64:YOUR_GENERATED_KEY_HERE
LOG_CHANNEL=stack

DB_CONNECTION=mysql
DB_HOST=${{ Railway MySQL Host }}
DB_PORT=3306
DB_DATABASE=railway
DB_USERNAME=${{ Railway MySQL User }}
DB_PASSWORD=${{ Railway MySQL Password }}

CACHE_DRIVER=database
QUEUE_CONNECTION=database
SESSION_DRIVER=database

EXTERNAL_API_BASE_URL=http://apirecoleccion.gonzaloandreslucio.com/api
EXTERNAL_API_TIMEOUT=10
```

### 4. Generar APP_KEY
Ejecuta localmente:
```bash
php artisan key:generate --show
```
Copia el valor y pégalo en `APP_KEY` en Railway.

### 5. Agregar base de datos MySQL
1. En el proyecto de Railway, agrega un plugin MySQL
2. Railway automáticamente inyectará las variables `DB_*`

### 6. Build & Deploy
Railway construirá y desplegará automáticamente:
- Instala dependencias con Composer
- Ejecuta migraciones (configurado en `Procfile`)
- Sirve la aplicación con Apache

## Archivos importantes

- **Procfile** - Configuración de cómo se ejecuta la app
- **.env.example** - Variables de entorno de ejemplo
- **.gitignore** - Archivos a ignorar en Git

## Verificar el despliegue

Una vez desplegado, verifica:
```bash
# Health check
curl https://your-app.up.railway.app

# Ver logs
railway logs
```

## Troubleshooting

- **Error de base de datos**: Asegúrate que MySQL está disponible
- **Error de APP_KEY**: Genera una nueva clave con `php artisan key:generate`
- **Permisos de carpeta**: Railway ejecuta con permisos limitados
- **Logs**: Revisa los logs en el dashboard de Railway

## Base de datos

Las migraciones se ejecutarán automáticamente en cada deploy gracias a:
```
release: php artisan migrate --force
```

Si necesitas hacer rollback:
```bash
railway run php artisan migrate:rollback
```
