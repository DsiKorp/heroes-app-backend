# 🦸‍♂️ Heroes Backend - NestJS API

API RESTful desarrollada con NestJS para la gestión de héroes y villanos. Este backend proporciona un sistema completo de CRUD con características avanzadas de búsqueda, paginación y estadísticas.

## 📋 Descripción

Backend desarrollado con NestJS que permite gestionar una base de datos de héroes y villanos con sus características, poderes, estadísticas y más. Ideal para aplicaciones de catálogo de superhéroes, sistemas de gestión de personajes o cualquier proyecto relacionado con el universo de cómics.

## ✨ Características

- ✅ CRUD completo de héroes (Crear, Leer, Actualizar, Eliminar)
- 🔍 Búsqueda avanzada por múltiples criterios
- 📄 Paginación de resultados
- 📊 Dashboard con estadísticas y resúmenes
- 🎯 Filtrado por categorías (Héroes/Villanos)
- 🌐 CORS habilitado
- ✔️ Validación de datos con class-validator
- 🚀 Transformación automática de DTOs
- 📁 Servicio de archivos estáticos

## 🛠️ Tecnologías

- **Framework:** NestJS 11.0.1
- **Runtime:** Node.js
- **Lenguaje:** TypeScript 5.7.3
- **Validación:** class-validator 0.14.2 & class-transformer 0.5.1
- **Testing:** Jest 29.7.0
- **Linting:** ESLint 9.18.0
- **Formateo:** Prettier 3.4.2

### Dependencias principales

```json
{
  "@nestjs/common": "^11.0.1",
  "@nestjs/core": "^11.0.1",
  "@nestjs/platform-express": "^11.0.1",
  "@nestjs/serve-static": "^5.0.3",
  "@nestjs/mapped-types": "*",
  "class-transformer": "^0.5.1",
  "class-validator": "^0.14.2",
  "uuid": "^11.1.0"
}
```

## 📋 Prerequisitos

- Node.js 18 o superior
- npm o yarn

## 🚀 Instalación

1. Clona el repositorio:
```bash
git clone <url-del-repositorio>
cd sec14-Backend-nest-heroes
```

2. Instala las dependencias:
```bash
npm install
```

3. (Opcional) Crea un archivo `.env` en la raíz del proyecto:
```bash
# .env
PORT=3000
```

## 🔧 Variables de Entorno

Crea un archivo `.env` en la raíz del proyecto con las siguientes variables:

```env
# Puerto del servidor
PORT=3000

# Otras configuraciones según necesites
# NODE_ENV=development
```

> **Nota:** Si no se especifica el puerto, la aplicación usará el puerto 3000 por defecto.

## 📦 Scripts Disponibles

```bash
# Desarrollo
npm run start:dev          # Inicia el servidor en modo desarrollo con hot-reload

# Producción
npm run build              # Compila el proyecto
npm run start:prod         # Inicia el servidor en modo producción

# Testing
npm run test               # Ejecuta los tests unitarios
npm run test:watch         # Tests en modo observación
npm run test:cov           # Tests con cobertura
npm run test:e2e           # Tests end-to-end

# Linting y formato
npm run lint               # Ejecuta ESLint
npm run format             # Formatea el código con Prettier
```

## 🌐 Ejecutar la aplicación

### Modo desarrollo
```bash
npm run start:dev
```

El servidor estará disponible en `http://localhost:3000`

### Modo producción
```bash
npm run build
npm run start:prod
```

## 📚 API Endpoints

Base URL: `http://localhost:3000/api`

### Heroes

| Método | Endpoint | Descripción |
|--------|----------|-------------|
| GET | `/api/heroes` | Obtiene todos los héroes (con paginación) |
| GET | `/api/heroes/:id` | Obtiene un héroe por ID o slug |
| GET | `/api/heroes/search` | Búsqueda avanzada de héroes |
| GET | `/api/heroes/summary` | Obtiene estadísticas y resumen |
| POST | `/api/heroes` | Crea un nuevo héroe |
| PATCH | `/api/heroes/:id` | Actualiza un héroe existente |
| DELETE | `/api/heroes/:id` | Elimina un héroe |

### Ejemplos de uso

#### Obtener todos los héroes (paginado)
```bash
GET /api/heroes?limit=10&offset=0&category=all
```

**Query Parameters:**
- `limit`: Número de resultados por página (default: 6)
- `offset`: Número de registros a omitir (default: 0)
- `category`: Filtrar por categoría - "Hero", "Villain", "all" (default: all)

**Respuesta:**
```json
{
  "total": 50,
  "pages": 5,
  "heroes": [...]
}
```

#### Obtener un héroe específico
```bash
GET /api/heroes/1
GET /api/heroes/spider-man
```

#### Crear un héroe
```bash
POST /api/heroes
Content-Type: application/json

{
  "name": "Spider-Man",
  "slug": "spider-man",
  "alias": "Peter Parker",
  "powers": ["Super fuerza", "Sentido arácnido", "Trepar paredes"],
  "description": "Un estudiante mordido por una araña radioactiva",
  "strength": 85,
  "intelligence": 90,
  "speed": 75,
  "durability": 80,
  "team": "Los Vengadores",
  "image": "/images/spider-man.jpg",
  "firstAppearance": "1962",
  "status": "Activo",
  "category": "Hero",
  "universe": "Marvel"
}
```

#### Búsqueda avanzada
```bash
GET /api/heroes/search?name=spider&category=Hero&minStrength=70
```

**Query Parameters disponibles:**
- `name`: Buscar por nombre
- `category`: Filtrar por categoría
- `universe`: Filtrar por universo
- `minStrength`: Fuerza mínima
- `minIntelligence`: Inteligencia mínima
- `team`: Filtrar por equipo

#### Obtener resumen y estadísticas
```bash
GET /api/heroes/summary
```

**Respuesta:**
```json
{
  "totalHeroes": 50,
  "strongestHero": {...},
  "smartestHero": {...},
  "heroCount": 30,
  "villainCount": 20,
  "antiHeroCount": 0,
  "avgStrength": 75.5,
  "avgIntelligence": 80.2,
  "avgSpeed": 70.8,
  "avgDurability": 78.3,
  "topTeams": [...]
}
```

## 📁 Estructura del Proyecto

```
src/
├── app.module.ts                 # Módulo principal de la aplicación
├── main.ts                       # Punto de entrada de la aplicación
├── common/                       # Elementos compartidos
│   └── dto/
│       └── pagination.dto.ts     # DTO para paginación
├── data/
│   └── heroes.data.ts            # Datos iniciales de héroes
└── heroes/                       # Módulo de héroes
    ├── heroes.controller.ts      # Controlador REST
    ├── heroes.service.ts         # Lógica de negocio
    ├── heroes.module.ts          # Módulo de héroes
    ├── dto/
    │   ├── create-hero.dto.ts    # DTO para crear héroe
    │   ├── update-hero.dto.ts    # DTO para actualizar héroe
    │   └── advande-search.dto.ts # DTO para búsqueda avanzada
    └── entities/
        └── hero.entity.ts        # Entidad de héroe
```

## 🗂️ Modelo de Datos

### Hero Entity

```typescript
{
  id: string;                    // ID único
  name: string;                  // Nombre del héroe
  slug: string;                  // URL-friendly name
  alias: string;                 // Identidad secreta
  powers: string[];              // Lista de poderes
  description: string;           // Descripción
  strength: number;              // Fuerza (0-100)
  intelligence: number;          // Inteligencia (0-100)
  speed: number;                 // Velocidad (0-100)
  durability: number;            // Durabilidad (0-100)
  team: string;                  // Equipo
  image: string;                 // URL de imagen
  firstAppearance: string;       // Año de primera aparición
  status: string;                // Estado (Activo/Retirado/etc)
  category: string;              // Categoría (Hero/Villain)
  universe: string;              // Universo (Marvel/DC/etc)
}
```

## 🔒 Validaciones

El proyecto utiliza `class-validator` para validar todos los datos de entrada:

- ✅ Campos requeridos validados
- ✅ Tipos de datos verificados
- ✅ Números mínimos validados
- ✅ Arrays con elementos tipados
- ✅ Whitelist activo (rechaza propiedades no definidas)
- ✅ Transformación automática de tipos

## 🌍 CORS

CORS está habilitado globalmente, permitiendo peticiones desde cualquier origen. Para configurar dominios específicos, modifica el archivo `main.ts`.

## 📄 Archivos de Configuración

### package.json
Contiene todas las dependencias, scripts y configuración del proyecto.

### tsconfig.json
Configuración de TypeScript con opciones optimizadas para NestJS.

### nest-cli.json
Configuración del CLI de NestJS.

### eslint.config.mjs
Reglas de linting para mantener código limpio y consistente.

## 🧪 Testing

El proyecto está configurado con Jest para testing:

```bash
# Tests unitarios
npm run test

# Tests con cobertura
npm run test:cov

# Tests en modo watch
npm run test:watch
```

## 🚀 Deploy

Para desplegar en producción:

1. Compila el proyecto:
```bash
npm run build
```

2. Los archivos compilados estarán en la carpeta `dist/`

3. Ejecuta en producción:
```bash
npm run start:prod
```

## 📝 Notas

- Este proyecto utiliza datos en memoria (sin base de datos persistente)
- Los cambios se pierden al reiniciar el servidor
- Ideal para desarrollo y testing
- Para producción, considera integrar una base de datos (MongoDB, PostgreSQL, etc.)

## 👨‍💻 Desarrollo

Este proyecto fue creado como parte del curso "React De cero a experto" - Sección 14: Backend con NestJS.

## 📄 Licencia

UNLICENSED - Este proyecto es privado y no tiene licencia pública.

---

Desarrollado con ❤️ usando [NestJS](https://nestjs.com/)
