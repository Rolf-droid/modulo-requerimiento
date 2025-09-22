# Diagrama de Despliegue - Arquitectura Completa del Ecosistema

## Arquitectura General del modulo presupuesto

```mermaid
graph TB

    subgraph "FRONTENDS EN VERCEL"
        Vercel["Vercel<br/>Plataforma de Despliegue Frontend"]
        
        subgraph "Aplicaciones Frontend"
            KapoMain["Kapo Main<br/>React<br/>Aplicación principal"]
            KapoInformes["Kapo Informes<br/>Angular<br/>Sistema de informes offline"]
            KapoDocumentos["Kapo Documentos<br/>Angular<br/>Gestión documental offline"]
            KapoActivoFijo["Kapo Activo Fijo<br/>Angular<br/>Control de activos fijos"]
            Velimaq["Velimaq<br/>React<br/>Sistema de gestión vehicular"]
            InaconsCombustible["Inacons Combustible<br/>React<br/>Control de combustible"]
            KapoOperacionesFront["Kapo Operaciones<br/>React<br/>Frontend operaciones"]
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
    KapoInformes --> BackendMain
    KapoDocumentos --> BackendMain
    KapoActivoFijo --> BackendMain
    Velimaq --> BackendMain
    InaconsCombustible --> BackendMain
    KapoOperacionesFront --> BackendOps
    
    BackendMain --> MongoDBMain
    BackendOps --> MongoDBMain

    %% Estilos
    classDef frontend fill:#e1f5fe,stroke:#01579b,stroke-width:2px
    classDef backend fill:#f3e5f5,stroke:#4a148c,stroke-width:2px
    classDef database fill:#e8f5e8,stroke:#1b5e20,stroke-width:2px
    classDef platform fill:#fff3e0,stroke:#e65100,stroke-width:2px

    class KapoMain,KapoInformes,KapoDocumentos,KapoActivoFijo,Velimaq,InaconsCombustible,KapoOperacionesFront frontend
    class BackendMain,BackendOps backend
    class MongoDBMain database
    class Vercel,GCP,Railway,AWS platform
```

## Arquitectura Simplificada

```mermaid
graph LR
    subgraph "Frontend - Vercel"
        F1[Kapo Main]
        F2[Kapo Informes]
        F3[Kapo Documentos]
        F4[Kapo Activo Fijo]
        F5[Velimaq]
        F6[Inacons Combustible]
        F7[Kapo Operaciones]
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
    F2 --> B1
    F3 --> B1
    F4 --> B1
    F5 --> B1
    F6 --> B1
    F7 --> B2
    
    B1 --> DB
    B2 --> DB
```

## Descripción de Componentes

### Frontend (Vercel)
- **Kapo Main**: Aplicación principal desarrollada en React
- **Kapo Informes**: Sistema de informes offline en Angular
- **Kapo Documentos**: Gestión documental offline en Angular
- **Kapo Activo Fijo**: Control de activos fijos en Angular
- **Velimaq**: Sistema de gestión vehicular en React
- **Inacons Combustible**: Control de combustible en React
- **Kapo Operaciones**: Frontend de operaciones en React

### Backend Principal (GCP)
- **API Principal**: Node.js con Express para operaciones principales
- **Despliegue**: Contenedor Docker en Google Cloud Platform

### Backend Operaciones (Railway)
- **API Operaciones**: Node.js con GraphQL para operaciones específicas
- **Despliegue**: Contenedor Docker en Railway

### Base de Datos (AWS)
- **MongoDB Atlas**: Base de datos principal que almacena todos los datos de la aplicación

## Flujo de Datos

1. Los frontends se comunican con sus respectivos backends
2. Los backends procesan las solicitudes y acceden a la base de datos
3. La base de datos MongoDB Atlas almacena toda la información
4. Los datos se sincronizan entre los diferentes sistemas

## Tecnologías Utilizadas

- **Frontend**: React, Angular
- **Backend**: Node.js, Express, GraphQL
- **Base de Datos**: MongoDB Atlas
- **Despliegue**: Vercel, Google Cloud Platform, Railway
- **Contenedores**: Docker
