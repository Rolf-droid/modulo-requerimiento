# Seguridad de la aplicacion

## 🔐 Autenticación y Autorización

### Sistema de Autenticación
- **JWT (JSON Web Tokens)** con expiración de 12 horas
- **Validación automática** de tokens en todas las operaciones GraphQL
- **Middleware personalizado** (`jwtValidationMiddleware`) para verificación
- **Operaciones públicas** definidas: `login`, `authenticate`, `vlogin`, `VLogin`

### Control de Acceso
- **Rutas protegidas** en frontend con `ProtectedRoute`
- **Sistema de roles** con permisos granulares por menú
- **Validación de permisos** basada en `menusPermissions`
- **Acceso denegado** automático para usuarios sin permisos

## 🛡️ Validación y Sanitización

### Validaciones de Entrada
- **Validación de RUC** (11 dígitos obligatorios)
- **Campos requeridos** con validación de longitud
- **Sanitización de strings** (trim, validación de vacíos)
- **Validación de tipos** para arrays y objetos
- **Conversión segura** de ObjectIds de MongoDB

### Protección de Datos
- **Hashing de contraseñas** con bcrypt
- **Actualización automática** de contraseñas en texto plano
- **Validación de formato** en documentos y archivos
- **Límites de tamaño** para carga de archivos (50MB)

## 🌐 Configuración de Red

### CORS (Cross-Origin Resource Sharing)
- **Orígenes permitidos** específicos y controlados
- **Desarrollo local** habilitado para localhost
- **Producción** restringida a dominios autorizados
- **Headers seguros** configurados

### Configuración de Servidor
- **Límites de payload** (1GB para JSON)
- **Timeouts configurados** (900s para operaciones)
- **Headers personalizados** con límites de tamaño
- **Keep-alive** optimizado

## 🔒 Gestión de Secretos

### Variables de Entorno
- **JWT_SECRET** para firmar tokens
- **JWT_REFRESH_SECRET** para tokens de renovación
- **Credenciales de base de datos** por ambiente
- **Configuración SMTP** separada por entorno
- **Modo de desarrollo** con validación deshabilitada

### Configuración por Ambiente
- **Desarrollo**: Mailtrap para emails de prueba
- **Producción**: SMTP real con credenciales seguras
- **Base de datos**: URLs diferentes por ambiente
- **CORS**: Configuración específica por entorno

## 📧 Seguridad de Comunicaciones

### Servicios de Email
- **Configuración dual** (desarrollo/producción)
- **Validación de credenciales** antes del envío
- **Manejo de errores** sin exposición de datos sensibles
- **Verificación de conexión** al inicializar

### APIs Externas
- **Validación de parámetros** antes de llamadas externas
- **Manejo de errores** sin exposición de detalles internos
- **Timeouts configurados** para evitar bloqueos

## 🗄️ Seguridad de Base de Datos

### MongoDB Atlas
- **Conexión encriptada** con SSL/TLS
- **Autenticación** con credenciales seguras
- **Índices optimizados** para consultas seguras
- **Validación de esquemas** en modelos

### Protección de Datos
- **ObjectIds** para referencias seguras
- **Validación de tipos** en esquemas Mongoose
- **Sanitización** de datos antes de guardar
- **Manejo de errores** sin exposición de estructura

## 🚀 Despliegue Seguro

### Contenedores Docker
- **Imagen base** Node.js 20-slim (ligera y segura)
- **Variables de entorno** inyectadas en runtime
- **Puerto dinámico** asignado por Google Cloud Run
- **Recursos limitados** (2Gi RAM, 2 CPU cores)

### Google Cloud Run
- **HTTPS obligatorio** en producción
- **Timeouts configurados** para evitar ataques DoS
- **Escalado automático** con límites definidos
- **Logs centralizados** para monitoreo

