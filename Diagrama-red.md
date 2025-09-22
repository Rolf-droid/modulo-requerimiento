# Diagrama de Red - Arquitectura de Conectividad


## Diagrama de Flujo de Datos

```mermaid
sequenceDiagram
    participant U as Usuario
    participant F as Frontend
    participant B as Backend
    participant DB as Base de Datos
    participant E as Servicios Externos

    U->>F: 1. Acceso a aplicación
    F->>B: 2. Autenticación
    B->>DB: 3. Validar credenciales
    DB-->>B: 4. Datos de usuario
    B-->>F: 5. Token válido
    
    U->>F: 6. Operación
    F->>B: 7. Request + Token
    B->>B: 8. Validar token
    B->>DB: 9. Consulta/Actualización
    DB-->>B: 10. Resultados
    B->>E: 11. Notificaciones
    B-->>F: 12. Respuesta
    F-->>U: 13. Datos actualizados
```

## Configuración de Puertos

| Servicio | Puerto | Protocolo |
|----------|--------|-----------|
| Frontend | 443 | HTTPS |
| Backend Principal | 8080 | HTTPS |
| Backend Secundario | 443 | HTTPS |
| Base de Datos | 27017 | SSL/TLS |
| Servicios Externos | 443/587 | HTTPS/TLS |

## Flujo de Seguridad

```mermaid
graph TD
    A[Cliente] --> B[CDN]
    B --> C[Validación CORS]
    C --> D[Frontend]
    D --> E[Validación JWT]
    E --> F[Backend]
    F --> G[Validación de Entrada]
    G --> H[Base de Datos]
    H --> I[Respuesta Encriptada]
    I --> J[Cliente Seguro]

    subgraph "Capas de Seguridad"
        K[HTTPS/TLS]
        L[JWT Authentication]
        M[Input Validation]
        N[Database Encryption]
        O[CORS Protection]
    end
```

## Características de Red

### Frontend
- **CDN Global**: Distribución de contenido
- **HTTPS Obligatorio**: Conexiones encriptadas
- **Auto-scaling**: Escalado automático

### Backend
- **Container-based**: Despliegue en contenedores
- **Auto-scaling**: Escalado según demanda
- **Load Balancing**: Distribución de carga
- **Health Checks**: Monitoreo continuo

