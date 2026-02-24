---
title: "Antes de empezar"
description: "Configura tu entorno, conoce las herramientas y haz tu primer ejercicio guiado"
---

# :rocket: Antes de empezar

<div class="chapter-meta">
  <span class="meta-item">🕐 30 minutos</span>
  <span class="meta-item">📊 Nivel: Setup</span>
  <span class="meta-item">🎯 Prerrequisito</span>
</div>

<div class="chapter-objective">
  <span class="objective-icon">🎯</span>
  <span class="objective-text">Al terminar esta página, tendrás tu entorno configurado, habrás ejecutado tu primer programa TypeScript y sabrás cómo usar el sistema interactivo de este libro.</span>
</div>

---

## :wrench: 1. Configura tu entorno

### Paso 1: Instala Node.js

TypeScript necesita Node.js para funcionar. Descárgalo de [nodejs.org](https://nodejs.org/) (versión LTS recomendada).

```bash
# Verifica la instalación
node --version   # v20.x o superior
npm --version    # 10.x o superior
```

### Paso 2: Instala TypeScript globalmente

```bash
npm install -g typescript
tsc --version  # Versión 5.x
```

### Paso 3: Instala Git

Git es necesario para el proyecto MakeMenu y para gestionar tu código:

```bash
git --version  # 2.x o superior
```

Si no lo tienes, instálalo desde [git-scm.com](https://git-scm.com/).

### Paso 4: Instala tu editor

Recomendamos **VS Code** con estas extensiones:

| Extensión | Para qué |
|-----------|----------|
| **TypeScript** | Ya viene incluida en VS Code |
| **Error Lens** | Muestra errores inline, al lado del código |
| **Pretty TypeScript Errors** | Errores de TS más legibles |
| **ESLint** | Linting de código |

!!! note "Windows / WSL"
    Si usas Windows, recomendamos trabajar dentro de **WSL 2** (Windows Subsystem for Linux). Todas las instrucciones de terminal de este libro asumen un entorno Unix. [Guía de instalación de WSL](https://learn.microsoft.com/es-es/windows/wsl/install).

---

## :zap: 2. Tu primer programa en 2 minutos

Abre una terminal y ejecuta:

```bash
# Crea un directorio para practicar
mkdir aprende-ts && cd aprende-ts
npm init -y
npm install -D typescript tsx

# Crea tu primer archivo
mkdir src
```

Crea el archivo `src/hola.ts`:

```typescript title="src/hola.ts"
// Tu primer programa TypeScript
function saludar(nombre: string): string {
  return `Hola ${nombre}, bienvenido a TypeScript!`;
}

console.log(saludar("Daniele"));

// Intenta descomentar esta línea y mira qué pasa:
// console.log(saludar(42));  // Error: number no es string
```

Ejecútalo:

```bash
npx tsx src/hola.ts
# Output: Hola Daniele, bienvenido a TypeScript!
```

✅ **Si ves el mensaje, tu entorno está listo.**

---

## :video_game: 3. Cómo usar este libro

### Flashcards interactivas

Cada capítulo tiene flashcards para reforzar conceptos. Haz **click** para revelar la respuesta:

<div class="flashcard">
<div class="front">Prueba: haz click aquí para revelar la respuesta</div>
<div class="back">Las flashcards funcionan. Usa <strong>Alt+F</strong> para navegar entre ellas y <strong>Alt+R</strong> para revelar todas.</div>
</div>

### Quizzes de autoevaluación

Después de cada capítulo, pon a prueba lo aprendido:

<div class="quiz" data-quiz-id="setup-q1">
<h4>Prueba: ¿Qué es TypeScript?</h4>
<button class="quiz-option" data-correct="false">Un framework de JavaScript</button>
<button class="quiz-option" data-correct="true">Un superset de JavaScript con tipos estáticos</button>
<button class="quiz-option" data-correct="false">Un lenguaje completamente diferente</button>
<div class="quiz-feedback" data-correct="¡Correcto! Los quizzes funcionan perfectamente." data-incorrect="No exactamente. TypeScript es un superset de JavaScript — todo JS válido es TS válido."></div>
</div>

### Comparaciones Python → TypeScript

Si vienes de Python, cada concepto incluye su equivalente:

<div class="comparison" markdown>
<div class="lang-box python" markdown>

#### :snake: En Python

```python
def saludar(nombre: str) -> str:
    return f"Hola {nombre}"
```

</div>
<div class="lang-box typescript" markdown>

#### 🔷 En TypeScript

```typescript
function saludar(nombre: string): string {
  return `Hola ${nombre}`;
}
```

</div>
</div>

### Pregunta conceptual

Antes de secciones clave, te haremos pensar:

<div class="concept-question">
<h4>🤔 Pregunta conceptual</h4>
<p>Si Python tiene type hints opcionales y TypeScript tiene tipos obligatorios, ¿qué ventaja real tiene TypeScript? Piensa 10 segundos antes de seguir leyendo.</p>
</div>

### Autoevaluación

Marca lo que puedas hacer al final de cada capítulo:

<div class="self-check" markdown>
<h4>Prueba el sistema de autoevaluación:</h4>
<label><input type="checkbox"> Puedo marcar casillas para rastrear mi progreso</label>
<label><input type="checkbox"> Entiendo que el progreso se guarda en mi navegador</label>
</div>

---

## :calendar: 4. Plan recomendado

| Semana | Capítulos | Tema |
|:------:|:---------:|------|
| 1-2 | 1-4 | Fundamentos: tipos básicos, interfaces, funciones |
| 3-4 | 5-8 | Tipos intermedios: uniones, generics, utility types |
| 5-7 | 9-13 | Avanzado: clases, módulos, type-level programming |
| 8 | 14-16 | Ecosistema: Vue 3, Node.js, proyecto MakeMenu |
| 9-10 | 17-20 | Experto: varianza, librerías, rendimiento, testing |

!!! tip "Ritmo ideal"
    **1-2 capítulos por semana**. Dedica al menos 2-3 horas por capítulo: leer, hacer ejercicios, y repasar flashcards.

---

## 🎯 5. Tu primer micro-ejercicio

<div class="micro-exercise">
<h4>🧪 Micro-ejercicio: Función tipada (2 min)</h4>
<p>Crea un archivo <code>src/suma.ts</code> con una función que sume dos números. Debe fallar si le pasas strings.</p>
</div>

??? success "Solución"
    ```typescript title="src/suma.ts"
    function sumar(a: number, b: number): number {
      return a + b;
    }

    console.log(sumar(3, 7));   // 10
    // sumar("3", "7");         // ❌ Error de compilación!
    ```

    ```bash
    npx tsx src/suma.ts
    ```

---

## ✅ ¿Todo listo?

<div class="self-check" markdown>
<h4>Verifica antes de continuar:</h4>
<label><input type="checkbox"> Node.js v20+ instalado</label>
<label><input type="checkbox"> TypeScript 5.x instalado</label>
<label><input type="checkbox"> Git instalado</label>
<label><input type="checkbox"> VS Code configurado con extensiones</label>
<label><input type="checkbox"> He ejecutado mi primer programa TypeScript</label>
<label><input type="checkbox"> Entiendo cómo usar flashcards, quizzes y ejercicios</label>
</div>

<div class="checkpoint">
<h4>🏁 Checkpoint</h4>
<p>Si has marcado todas las casillas, estás listo para el <a href="capitulos/01-bienvenido/">Capítulo 1: Bienvenido a TypeScript</a>.</p>
</div>
