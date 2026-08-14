# Streakticle

Plataforma social de aprendizaje que transforma artículos en flashcards inteligentes. Lee un artículo al día, genera tarjetas de estudio con IA y compite con tus amigos manteniendo tu racha activa.

## Qué es Streakticle

Streakticle combina lectura diaria de artículos técnicos con un sistema de flashcards generadas automáticamente mediante RAG (Retrieval-Augmented Generation). Los usuarios pueden seleccionar la complejidad de cada artículo, competir con amigos a través de tablas de clasificación y construir un hábito de estudio consistente — todo de forma gratuita.

El enfoque inicial es **inteligencia artificial y machine learning**, con la arquitectura preparada para expandirse a cualquier área del conocimiento.

## Funcionalidades principales

### Lectura diaria de artículos
- Artículos curados organizados por área temática
- Tres niveles de complejidad: introductorio, intermedio y avanzado
- Sistema de áreas expandible (IA/ML como primera vertical)
- Historial de lectura y progreso por usuario

### Generación inteligente de flashcards
- Pipeline RAG que analiza cada artículo y extrae conceptos clave
- Generación automática de preguntas y respuestas
- Flashcards adaptadas al nivel de complejidad seleccionado
- Algoritmo de repetición espaciada para optimizar retención

### Red social y gamificación
- Perfiles de usuario con estadísticas de estudio
- Sistema de streaks (rachas diarias de lectura)
- Tablas de clasificación entre amigos
- Comparación de progreso por área temática
- Logros y badges por hitos de aprendizaje

### Motor RAG interno
- Indexación y análisis semántico de artículos
- Búsqueda contextual dentro del contenido leído
- Respuestas a preguntas basadas en el corpus personal del usuario
- Generación de resúmenes y puntos clave por artículo

## Arquitectura

```
┌─────────────┐     ┌──────────────────┐     ┌─────────────────┐
│   Frontend   │────▶│   Backend (Go)   │────▶│  AI Service     │
│   React      │◀────│   REST API       │◀────│  (Python)       │
└─────────────┘     └──────────────────┘     └─────────────────┘
                           │                        │
                           ▼                        ▼
                    ┌──────────────┐         ┌──────────────┐
                    │  PostgreSQL  │         │ Vector Store │
                    │  (datos)     │         │ (embeddings) │
                    └──────────────┘         └──────────────┘
```

### Stack tecnológico

| Capa | Tecnología | Propósito |
|------|-----------|-----------|
| Frontend | React | Interfaz de usuario, SPA |
| Backend API | Go | API REST, autenticación, lógica de negocio |
| Servicio IA | Python | Inferencia local, pipeline RAG, generación de flashcards |
| Base de datos | PostgreSQL | Usuarios, artículos, flashcards, progreso |
| Vector store | ChromaDB / Qdrant | Embeddings de artículos para RAG |
| Cache | Redis | Sesiones, leaderboards, rate limiting |

## Estructura del proyecto

```
streakticle/
├── backend/                 # Servicio API en Go
│   ├── cmd/api/             # Punto de entrada del servidor
│   ├── internal/
│   │   ├── handlers/        # Handlers HTTP
│   │   ├── models/          # Modelos de datos
│   │   ├── services/        # Lógica de negocio
│   │   ├── repository/      # Capa de acceso a datos
│   │   ├── middleware/       # Auth, CORS, logging
│   │   └── config/          # Configuración del servicio
│   ├── pkg/
│   │   ├── rag/             # Cliente para comunicación con servicio RAG
│   │   └── flashcard/       # Lógica de flashcards y repetición espaciada
│   └── migrations/          # Migraciones de base de datos
├── ai/                      # Servicio de IA en Python
│   ├── services/            # Servicios de inferencia y RAG
│   ├── models/              # Modelos y schemas
│   ├── rag/                 # Pipeline RAG (indexación, retrieval, generación)
│   └── tests/               # Tests del servicio IA
├── frontend/                # Aplicación React
│   ├── src/
│   │   ├── components/      # Componentes reutilizables
│   │   ├── pages/           # Vistas principales
│   │   ├── hooks/           # Custom hooks
│   │   ├── services/        # Clientes API
│   │   ├── store/           # Estado global
│   │   └── assets/          # Recursos estáticos
│   └── public/              # Archivos públicos
└── docs/                    # Documentación del proyecto
```

## Roadmap de desarrollo

### Fase 1 — Fundamentos
- [ ] Configuración del proyecto Go (módulos, estructura, servidor HTTP)
- [ ] Esquema de base de datos (usuarios, artículos, flashcards, streaks)
- [ ] Endpoints de autenticación (registro, login, JWT)
- [ ] CRUD de artículos con niveles de complejidad
- [ ] Scaffold del frontend React con routing básico
- [ ] Sistema de áreas temáticas configurable

### Fase 2 — Motor de flashcards
- [ ] Servicio Python con FastAPI para inferencia
- [ ] Pipeline RAG: ingesta de artículos, chunking, embeddings
- [ ] Generación de flashcards a partir de análisis RAG
- [ ] API de flashcards (crear, listar, revisar, evaluar respuesta)
- [ ] Algoritmo de repetición espaciada (SM-2 o similar)
- [ ] UI de estudio con flashcards (flip, calificar, siguiente)

### Fase 3 — Social y gamificación
- [ ] Sistema de amigos (solicitudes, aceptar, bloquear)
- [ ] Cálculo y persistencia de streaks diarios
- [ ] Leaderboards (global, entre amigos, por área)
- [ ] Perfiles de usuario con estadísticas
- [ ] Notificaciones (recordatorios de racha, actividad de amigos)
- [ ] Logros y badges

### Fase 4 — Expansión
- [ ] Soporte para múltiples áreas temáticas más allá de IA
- [ ] Búsqueda semántica en artículos leídos (RAG personal)
- [ ] Flashcards colaborativas (compartir mazos entre usuarios)
- [ ] API pública para integración con terceros
- [ ] App móvil (React Native o PWA)
- [ ] Sistema de contribución de artículos por la comunidad

## Requisitos previos

- Go 1.22+
- Python 3.11+
- Node.js 20+
- PostgreSQL 16+
- Redis 7+

## Inicio rápido

> El proyecto está en fase inicial de desarrollo. Las instrucciones de setup se actualizarán conforme se implementen los servicios.

```bash
# Clonar el repositorio
git clone https://github.com/tu-usuario/streakticle.git
cd streakticle

# Backend (Go)
cd backend
go mod tidy
go run cmd/api/main.go

# Servicio IA (Python)
cd ai
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
uvicorn main:app --reload

# Frontend (React)
cd frontend
npm install
npm run dev
```

## Contribuir

Streakticle es un proyecto open source. Si quieres contribuir, revisa los issues abiertos o propón nuevas funcionalidades.

## Licencia

MIT
