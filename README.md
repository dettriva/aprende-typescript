[![License: CC BY-SA 4.0](https://img.shields.io/badge/License-CC%20BY--SA%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by-sa/4.0/)
[![Built with MkDocs Material](https://img.shields.io/badge/Built%20with-Material%20for%20MkDocs-526CFE.svg)](https://squidfunk.github.io/mkdocs-material/)
[![Deploy](https://github.com/dettriva/aprende-typescript/actions/workflows/deploy.yml/badge.svg)](https://github.com/dettriva/aprende-typescript/actions/workflows/deploy.yml)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)

# Aprende TypeScript si ya sabes Python

**Guia interactiva completa — De Python a TypeScript profesional**

Una guia de 28 capitulos con 17 componentes pedagogicos interactivos, disenada para desarrolladores con nivel intermedio en Python que quieran dominar TypeScript a nivel profesional.

<!-- TODO: Anadir screenshot del sitio desplegado -->

---

## Para quien es esta guia

- Desarrolladores con nivel intermedio en Python que quieran aprender TypeScript
- Estudiantes de DAW/DAM que vienen de Python/Django
- Pythonistas que quieran trabajar con Vue 3, Node.js o desarrollo web frontend/backend

**Prerequisitos:** Saber programar en Python (funciones, clases, modulos, tipos basicos). No necesitas saber JavaScript — las Bases lo cubren.

---

## Que incluye

| Parte | Capitulos | Contenido |
|-------|-----------|-----------|
| **Parte 0 — Bases JavaScript** | 4 caps | Conceptos de programacion, JavaScript core, ES6+, asincronia |
| **Parte I — Fundamentos** | 4 caps | Bienvenido a TS, tipos basicos, interfaces, funciones |
| **Parte II — Intermedio** | 4 caps | Uniones discriminadas, generics, enums, utility types |
| **Parte III — Avanzado** | 4 caps | Clases, modulos, tipos avanzados, type guards |
| **Parte IV — Ecosistema** | 4 caps | Type-level programming, Vue 3, Node.js, proyecto final |
| **Parte V — Maestria** | 4 caps | Varianza/nominal, patrones/librerias, rendimiento, testing |

**Total:** 28 capitulos · 277 elementos interactivos · Proyecto integrador MakeMenu

---

## Metodologia

La guia aplica 6 tecnicas de aprendizaje basadas en evidencia:

| Tecnica | Componente |
|---------|------------|
| Repeticion espaciada | Flashcards con sistema de repaso |
| Recuerdo activo | Quizzes interactivos, preguntas conceptuales |
| Interrogacion elaborativa | Preguntas "por que" antes de cada seccion |
| Entrelazado | Conexiones entre capitulos, proyecto progresivo |
| Ejemplos concretos | Comparaciones Python vs TypeScript lado a lado |
| Doble codificacion | Diagramas Mermaid + codigo + explicacion textual |

---

## Componentes interactivos

Cada capitulo incluye hasta 17 componentes pedagogicos:

| Componente | Descripcion |
|------------|-------------|
| Flashcards | Tarjetas de repaso con flip interactivo |
| Quizzes | Preguntas con feedback inmediato |
| Ejercicios guiados | Paso a paso con solucion completa |
| Mini-proyectos | Aplicacion practica en 3 pasos |
| Comparaciones | Bloques Python vs TypeScript lado a lado |
| Preguntas conceptuales | Reflexion antes de cada tema |
| Micro-ejercicios | Retos de 2-5 minutos |
| Evolucion del codigo | De novato a profesional en 3 versiones |
| Errores reales | Mensajes de error del compilador explicados |
| Misconception boxes | Mitos desmentidos con la realidad |
| Pro Tips | Consejos de nivel profesional |
| Connection boxes | Conexiones con capitulos anteriores y siguientes |
| Self-checks | Autoevaluacion con checkboxes |
| Checkpoints | Verificacion de comprension por seccion |
| Chapter objectives | Objetivo claro al inicio de cada capitulo |
| Chapter maps | Mapa visual del capitulo con Mermaid |
| Chapter meta | Tiempo estimado, nivel y semana |

---

## Quick Start

```bash
# Clonar el repositorio
git clone https://github.com/dettriva/aprende-typescript.git
cd aprende-typescript

# Crear entorno virtual (recomendado)
python -m venv .venv
source .venv/bin/activate

# Instalar dependencias
pip install -r requirements.txt

# Servir localmente con hot-reload
mkdocs serve
```

Abre [http://localhost:8000](http://localhost:8000) en tu navegador.

---

## Estructura del proyecto

```
aprende-typescript/
├── mkdocs.yml                 # Configuracion MkDocs Material
├── requirements.txt           # Dependencias Python
├── docs/
│   ├── index.md               # Pagina de inicio
│   ├── plan.md                # Plan de estudio 8 semanas
│   ├── antes-de-empezar.md    # Guia de preparacion
│   ├── referencia-rapida.md   # Cheatsheet
│   ├── recursos.md            # Enlaces y herramientas
│   ├── assets/
│   │   ├── extra.css          # Sistema de diseno (17 componentes)
│   │   └── extra.js           # Logica interactiva (flashcards, quizzes, progreso)
│   └── capitulos/
│       ├── bases-1-conceptos.md
│       ├── bases-2-javascript.md
│       ├── bases-3-es6.md
│       ├── bases-4-asincronia.md
│       ├── 01-bienvenido.md ... 20-testing-libreria.md
└── .github/
    ├── workflows/deploy.yml   # CI/CD GitHub Pages
    └── ISSUE_TEMPLATE/        # Templates de issues
```

---

## Contribuir

Las contribuciones son bienvenidas. Consulta [CONTRIBUTING.md](CONTRIBUTING.md) para la guia de contribucion.

## Licencia

Este proyecto esta licenciado bajo [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/) — puedes compartir y adaptar el contenido con atribucion.

---

Hecho con amor por [dettriva](https://github.com/dettriva) · Construido con [MkDocs Material](https://squidfunk.github.io/mkdocs-material/)
