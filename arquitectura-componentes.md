# Diagrama de Despliegue - Arquitectura Completa del Ecosistema

## Arquitectura General

```mermaid
graph TB
    subgraph "FRONTEND EN VERCEL"
        Vercel["Vercel<br/>Plataforma de Despliegue Frontend"]
        
        subgraph "Aplicación Frontend"
            KapoMain["Kapo Main<br/>React<br/>Aplicación principal"]
        end
    end

    subgraph "BACKEND PRINCIPAL EN GCP"
        GCP["Google Cloud<br/>Google Cloud Platform"]
        
        subgraph "Contenedor Docker Principal"
            BackendMain["Backend API Principal<br/>Node.js<br/>API REST principal con Express"]
        end
    end

    subgraph "BACKEND SECUNDARIO EN RAILWAY"
        Railway["Railway<br/>Plataforma de Despliegue"]
        
        subgraph "Contenedor Docker Operaciones"
            BackendOps["Backend Operaciones<br/>Node.js + GraphQL<br/>API GraphQL para operaciones"]
        end
    end

    subgraph "BASES DE DATOS"
        AWS["AWS<br/>MongoDB Atlas - Principal"]
        
        subgraph "MongoDB Atlas"
            MongoDBMain["Database Principal<br/>MongoDB<br/>Almacena datos principales de la aplicación"]
        end
    end

    %% Conexiones
    KapoMain --> BackendMain
    
    BackendMain --> MongoDBMain
    BackendOps --> MongoDBMain

    %% Estilos
    classDef frontend fill:#e1f5fe,stroke:#01579b,stroke-width:2px
    classDef backend fill:#f3e5f5,stroke:#4a148c,stroke-width:2px
    classDef database fill:#e8f5e8,stroke:#1b5e20,stroke-width:2px
    classDef platform fill:#fff3e0,stroke:#e65100,stroke-width:2px

    class KapoMain frontend
    class BackendMain,BackendOps backend
    class MongoDBMain database
    class Vercel,GCP,Railway,AWS platform
```

## Arquitectura Simplificada

```mermaid
graph LR
    subgraph "Frontend - Vercel"
        F1[Kapo Main]
    end

    subgraph "Backend - GCP"
        B1[API Principal<br/>Node.js + Express]
    end

    subgraph "Backend - Railway"
        B2[API Operaciones<br/>Node.js + GraphQL]
    end

    subgraph "Database - AWS"
        DB[MongoDB Atlas]
    end

    F1 --> B1
    
    B1 --> DB
    B2 --> DB
```

## Descripción de Componentes

### Frontend (Vercel)
- **Kapo Main**: Aplicación principal desarrollada en React

### Backend Principal (GCP)
- **API Principal**: Node.js con Express para operaciones principales
- **Despliegue**: Contenedor Docker en Google Cloud Platform


### Base de Datos (AWS)
- **MongoDB Atlas**: Base de datos principal que almacena todos los datos de la aplicación

## Flujo de Datos

1. El frontend se comunica con el backend principal.
2. Los backends procesan las solicitudes y acceden a la base de datos.
3. La base de datos MongoDB Atlas almacena toda la información.

## Tecnologías Utilizadas

- **Frontend**: React
- **Backend**: Node.js, Express, GraphQL
- **Base de Datos**: MongoDB Atlas
- **Despliegue**: Vercel, Google Cloud Platform, Railway
- **Contenedores**: Docker
