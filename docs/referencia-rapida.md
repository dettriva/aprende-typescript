---
title: "Referencia rápida"
description: "Cheat sheet completo de TypeScript"
---

# :zap: Referencia rápida — TypeScript Cheat Sheet

<div class="chapter-meta">
  <span class="meta-item">🔷 TypeScript 5.x</span>
  <span class="meta-item">🎯 Todas las secciones</span>
  <span class="meta-item">⌨️ Alt+F / Alt+R para flashcards</span>
</div>

!!! tip "Cómo usar esta referencia"
    Esta página es un **resumen compacto** de todo TypeScript. Úsala como consulta rápida, no como tutorial. Cada sección enlaza con el capítulo correspondiente del curso.

<div class="quick-nav" markdown>
<div class="cheat-grid" markdown>
<div class="cheat-card" markdown>

[1. Primitivos](#1-tipos-primitivos) · [2. Arrays](#2-arrays-y-tuplas) · [3. Objetos](#3-objetos-e-interfaces) · [4. Funciones](#4-funciones)

</div>
<div class="cheat-card" markdown>

[5. Uniones](#5-uniones-y-narrowing) · [6. Generics](#6-generics) · [7. Utility](#7-utility-types) · [8. Enums](#8-enums-y-literales)

</div>
<div class="cheat-card" markdown>

[9. Clases](#9-clases) · [10. Módulos](#10-modulos) · [11. Avanzados](#11-tipos-avanzados) · [12. Guards](#12-type-guards)

</div>
<div class="cheat-card" markdown>

[13. tsconfig](#13-configuracion-tsconfigjson) · [14. Patrones](#14-patrones-comunes)

</div>
<div class="cheat-card" markdown>

[15. Varianza](#15-varianza-y-tipos-nominales) · [16. Patrones de librerías](#16-patrones-de-librerias) · [17. Escala](#17-rendimiento-y-escala) · [18. Type Testing](#18-testing-de-tipos)

</div>
</div>
</div>

---

## 1. Tipos primitivos

> :book: [Ver capítulo completo](capitulos/02-tipos-basicos.md)

Los 7 tipos primitivos de TypeScript:

```typescript
let nombre: string = "Daniele";
let edad: number = 42;                // enteros, decimales, NaN, Infinity
let activo: boolean = true;
let nada: null = null;
let indefinido: undefined = undefined;
let grande: bigint = 100n;            // números enormes
let id: symbol = Symbol("único");     // identificador único
```

| Tipo | Descripción | Ejemplo |
|------|-------------|---------|
| `string` | Cadena de texto | `"hola"`, `` `${x}` `` |
| `number` | Número (entero o decimal) | `42`, `3.14`, `NaN` |
| `boolean` | Verdadero o falso | `true`, `false` |
| `null` | Ausencia intencional | `null` |
| `undefined` | No asignado | `undefined` |
| `bigint` | Entero de precisión arbitraria | `9007199254740991n` |
| `symbol` | Valor único e inmutable | `Symbol("id")` |

Tipos especiales:

```typescript
let cualquiera: any = "sin verificación";  // ❌ evitar
let desconocido: unknown = getData();       // ✅ seguro — requiere narrowing
let nunca: never;                           // funciones que nunca retornan
let vacio: void = undefined;               // funciones sin retorno
```

---

## 2. Arrays y Tuplas

> :book: [Ver capítulo completo](capitulos/02-tipos-basicos.md)

<div class="cheat-grid" markdown>
<div class="cheat-card" markdown>

##### Arrays

```typescript
// Dos sintaxis equivalentes
let nums: number[] = [1, 2, 3];
let strs: Array<string> = ["a", "b"];

// Array de solo lectura
let fijo: readonly number[] = [1, 2];
// fijo.push(4); // ❌ Error
```

</div>
<div class="cheat-card" markdown>

##### Tuplas

```typescript
// Longitud y tipos fijos
let punto: [number, number] = [10, 20];
let entrada: [string, number] = ["edad", 30];

// Tupla con nombre (legibilidad)
type Coord = [x: number, y: number, z: number];

// Tupla readonly
let rgb: readonly [number, number, number] = [255, 0, 0];
```

</div>
</div>

```typescript
// Rest en tuplas
type StringYNúmeros = [string, ...number[]];
let datos: StringYNúmeros = ["precios", 10, 20, 30];

// Tupla opcional
type Rango = [inicio: number, fin?: number];
```

---

## 3. Objetos e Interfaces

> :book: [Ver capítulo completo](capitulos/03-interfaces.md)

=== "Interface"

    ```typescript
    interface Usuario {
      nombre: string;
      edad: number;
      email?: string;              // opcional
      readonly id: number;         // solo lectura
    }

    // Extensión
    interface Admin extends Usuario {
      permisos: string[];
    }

    // Index signature
    interface Diccionario {
      [clave: string]: number;
    }
    ```

=== "Type Alias"

    ```typescript
    type Punto = {
      x: number;
      y: number;
    };

    // Intersección (combinar tipos)
    type PuntoConColor = Punto & { color: string };

    // Unión
    type ID = string | number;

    // Tipo literal
    type Dirección = "norte" | "sur" | "este" | "oeste";
    ```

=== "Interface vs Type"

    | Característica | `interface` | `type` |
    |----------------|-------------|--------|
    | Extensión | `extends` | `&` (intersección) |
    | Declaración fusionada | Si | No |
    | Primitivos/uniones | No | Si |
    | Tuplas/utility types | Limitado | Si |
    | **Recomendación** | Objetos/APIs | Uniones/utilidades |

---

## 4. Funciones

> :book: [Ver capítulo completo](capitulos/04-funciones.md)

<div class="cheat-grid" markdown>
<div class="cheat-card" markdown>

##### Parámetros y retorno

```typescript
// Tipos explícitos
function suma(a: number, b: number): number {
  return a + b;
}

// Arrow function
const doble = (n: number): number => n * 2;

// Retorno void
function log(msg: string): void {
  console.log(msg);
}
```

</div>
<div class="cheat-card" markdown>

##### Opcionales, default, rest

```typescript
// Opcional
function saludo(nombre: string, titulo?: string): string {
  return titulo ? `${titulo} ${nombre}` : nombre;
}

// Valor por defecto
function crear(nombre: string, activo = true) { }

// Rest params
function sumaTotal(...nums: number[]): number {
  return nums.reduce((a, b) => a + b, 0);
}
```

</div>
</div>

```typescript
// Overloads (sobrecargas)
function procesar(input: string): string;
function procesar(input: number): number;
function procesar(input: string | number): string | number {
  return typeof input === "string" ? input.toUpperCase() : input * 2;
}

// Función genérica
function primero<T>(arr: T[]): T | undefined {
  return arr[0];
}

// Función que nunca retorna
function error(msg: string): never {
  throw new Error(msg);
}

// Tipo función (callback)
type Callback = (dato: string) => void;
type Comparador<T> = (a: T, b: T) => number;
```

---

## 5. Uniones y Narrowing

> :book: [Ver capítulo completo](capitulos/05-uniones.md)

```typescript
// Unión simple
type Resultado = string | number;

// Discriminated union (unión discriminada)
type Forma =
  | { tipo: "circulo"; radio: number }
  | { tipo: "rectangulo"; ancho: number; alto: number };

function área(forma: Forma): number {
  switch (forma.tipo) {
    case "circulo":
      return Math.PI * forma.radio ** 2;     // TS sabe que es círculo
    case "rectangulo":
      return forma.ancho * forma.alto;        // TS sabe que es rectángulo
  }
}
```

**Técnicas de narrowing:**

| Técnica | Ejemplo | Cuándo usar |
|---------|---------|-------------|
| `typeof` | `typeof x === "string"` | Primitivos |
| `instanceof` | `x instanceof Date` | Clases |
| `in` | `"nombre" in x` | Propiedades de objeto |
| Igualdad | `x === null` | Valores específicos |
| Predicado | `function isAdmin(u): u is Admin` | Lógica personalizada |
| `asserts` | `function assert(x): asserts x is string` | Aserciones |

```typescript
// Predicado personalizado (type predicate)
function esString(valor: unknown): valor is string {
  return typeof valor === "string";
}

// Assertion function
function assertDefined<T>(val: T | undefined): asserts val is T {
  if (val === undefined) throw new Error("Valor indefinido");
}
```

---

## 6. Generics

> :book: [Ver capítulo completo](capitulos/06-generics.md)

```typescript
// Función genérica básica
function identidad<T>(valor: T): T {
  return valor;
}

// Restricción con extends
function longitud<T extends { length: number }>(item: T): number {
  return item.length;
}

// Múltiples parámetros
function par<K, V>(clave: K, valor: V): [K, V] {
  return [clave, valor];
}

// Valor por defecto
function crearLista<T = string>(): T[] {
  return [];
}
```

```typescript
// Interface genérica
interface Respuesta<T> {
  datos: T;
  error: string | null;
  status: number;
}

// Clase genérica
class Pila<T> {
  private items: T[] = [];
  push(item: T): void { this.items.push(item); }
  pop(): T | undefined { return this.items.pop(); }
}

// Restricción con keyof
function obtener<T, K extends keyof T>(obj: T, clave: K): T[K] {
  return obj[clave];
}
```

---

## 7. Utility Types

> :book: [Ver capítulo completo](capitulos/08-utility-types.md)

Todos los tipos utilitarios integrados de TypeScript:

### Transformación de objetos

| Utility | Descripción | Ejemplo |
|---------|-------------|---------|
| `Partial<T>` | Todas las propiedades opcionales | `Partial<Usuario>` |
| `Required<T>` | Todas las propiedades requeridas | `Required<Config>` |
| `Readonly<T>` | Todas de solo lectura | `Readonly<Estado>` |
| `Pick<T, K>` | Seleccionar propiedades | `Pick<Usuario, "nombre" \| "email">` |
| `Omit<T, K>` | Excluir propiedades | `Omit<Usuario, "password">` |
| `Record<K, V>` | Objeto con claves K y valores V | `Record<string, number>` |

### Transformación de uniones

| Utility | Descripción | Ejemplo |
|---------|-------------|---------|
| `Exclude<T, U>` | Quitar tipos de una unión | `Exclude<string \| number, string>` → `number` |
| `Extract<T, U>` | Extraer tipos de una unión | `Extract<string \| number, string>` → `string` |
| `NonNullable<T>` | Eliminar `null` y `undefined` | `NonNullable<string \| null>` → `string` |

### Tipos de funciones

| Utility | Descripción | Ejemplo |
|---------|-------------|---------|
| `ReturnType<T>` | Tipo de retorno de función | `ReturnType<typeof fn>` |
| `Parameters<T>` | Tupla de parámetros | `Parameters<typeof fn>` |
| `ConstructorParameters<T>` | Parámetros del constructor | `ConstructorParameters<typeof Clase>` |
| `InstanceType<T>` | Tipo de instancia de clase | `InstanceType<typeof Clase>` |
| `ThisParameterType<T>` | Tipo de `this` en función | `ThisParameterType<typeof fn>` |
| `OmitThisParameter<T>` | Quitar `this` de función | `OmitThisParameter<typeof fn>` |

### Otros

| Utility | Descripción | Ejemplo |
|---------|-------------|---------|
| `Awaited<T>` | Desenvolver `Promise` | `Awaited<Promise<string>>` → `string` |

```typescript
// Ejemplo práctico: actualización parcial
interface Usuario {
  id: number;
  nombre: string;
  email: string;
}

function actualizar(id: number, cambios: Partial<Usuario>): void { }
actualizar(1, { nombre: "Ana" }); // ✅ solo lo que cambia

// Record para mapas
const precios: Record<string, number> = {
  manzana: 1.5,
  banana: 0.8,
};

// Pick/Omit para vistas
type UsuarioPublico = Omit<Usuario, "email">;
type UsuarioResumen = Pick<Usuario, "id" | "nombre">;
```

---

## 8. Enums y Literales

> :book: [Ver capítulo completo](capitulos/07-enums.md)

=== "Enums"

    ```typescript
    // Enum numérico
    enum Dirección {
      Norte,      // 0
      Sur,        // 1
      Este,       // 2
      Oeste,      // 3
    }

    // Enum string
    enum Estado {
      Activo = "ACTIVO",
      Inactivo = "INACTIVO",
      Pendiente = "PENDIENTE",
    }

    // const enum (eliminado en compilación)
    const enum Color {
      Rojo = "#FF0000",
      Verde = "#00FF00",
      Azul = "#0000FF",
    }
    ```

=== "Literales y as const"

    ```typescript
    // Tipo literal
    type Tema = "claro" | "oscuro" | "sistema";

    // as const — inmutable y tipos literales
    const CONFIG = {
      api: "https://api.ejemplo.com",
      timeout: 5000,
      reintentos: 3,
    } as const;
    // typeof CONFIG.timeout → 5000 (no number)

    // Template literal types
    type Evento = `on${Capitalize<string>}`;
    type CSSProp = `${string}-${string}`;
    type Método = `get${string}` | `set${string}`;
    ```

=== "Branded Types"

    ```typescript
    // Tipos nominales con branding
    type UserId = number & { readonly __brand: "UserId" };
    type OrderId = number & { readonly __brand: "OrderId" };

    function crearUserId(id: number): UserId {
      return id as UserId;
    }

    function buscarUsuario(id: UserId): void { }

    const uid = crearUserId(42);
    buscarUsuario(uid);        // ✅
    // buscarUsuario(42);      // ❌ number no es UserId
    ```

---

## 9. Clases

> :book: [Ver capítulo completo](capitulos/09-clases.md)

```typescript
class Animal {
  // Propiedades del parámetro (shorthand)
  constructor(
    public nombre: string,
    private _edad: number,
    protected tipo: string,
    readonly id: number,
  ) {}

  // Getter
  get edad(): number {
    return this._edad;
  }

  // Setter
  set edad(valor: number) {
    if (valor < 0) throw new Error("Edad inválida");
    this._edad = valor;
  }

  // Método
  describir(): string {
    return `${this.nombre} (${this.tipo})`;
  }

  // Método estático
  static crear(nombre: string): Animal {
    return new Animal(nombre, 0, "desconocido", Date.now());
  }
}
```

```typescript
// Clase abstracta
abstract class Forma {
  abstract área(): number;
  abstract perímetro(): number;

  describir(): string {
    return `Área: ${this.área().toFixed(2)}`;
  }
}

class Círculo extends Forma {
  constructor(private radio: number) { super(); }
  área(): number { return Math.PI * this.radio ** 2; }
  perímetro(): number { return 2 * Math.PI * this.radio; }
}

// Implements (interfaz)
interface Serializable {
  toJSON(): string;
}

class Producto implements Serializable {
  constructor(public nombre: string, public precio: number) {}
  toJSON(): string { return JSON.stringify(this); }
}
```

| Modificador | Acceso | Descripción |
|-------------|--------|-------------|
| `public` | Todos | Por defecto |
| `private` | Solo la clase | No accesible fuera |
| `protected` | Clase + hijas | Herencia |
| `readonly` | Solo lectura | Asignar solo en constructor |
| `static` | Sin instancia | Acceso vía `Clase.método()` |
| `abstract` | Solo en abstractas | Debe ser implementado |

---

## 10. Módulos

> :book: [Ver capítulo completo](capitulos/10-modulos.md)

=== "Exportar"

    ```typescript
    // Named exports
    export const PI = 3.14159;
    export function sumar(a: number, b: number): number {
      return a + b;
    }
    export interface Config { debug: boolean; }

    // Default export
    export default class Logger { }

    // Re-export
    export { sumar } from "./math";
    export { default as Logger } from "./logger";
    export * from "./utils";
    export * as Utils from "./utils";
    ```

=== "Importar"

    ```typescript
    // Named imports
    import { sumar, PI } from "./math";

    // Renombrar
    import { sumar as add } from "./math";

    // Default import
    import Logger from "./logger";

    // Namespace import
    import * as Math from "./math";

    // Type-only imports (eliminados en compilación)
    import type { Config } from "./config";
    import { type Usuario, crearUsuario } from "./users";
    ```

=== "Declaraciones"

    ```typescript
    // Archivo .d.ts (declaración de tipos)
    declare module "mi-librería" {
      export function hacerAlgo(x: string): number;
      export interface Opciones {
        verbose: boolean;
      }
    }

    // Declarar variable global
    declare const __VERSION__: string;

    // Augmentar módulo existente
    declare module "express" {
      interface Request {
        usuario?: { id: string; rol: string };
      }
    }
    ```

---

## 11. Tipos avanzados

> :book: [Ver capítulo completo](capitulos/11-tipos-avanzados.md)

### Mapped Types

```typescript
// Tipo mapeado básico
type Opcional<T> = {
  [K in keyof T]?: T[K];
};

// Con modificadores
type SoloLectura<T> = {
  readonly [K in keyof T]: T[K];
};

// Remapeo de claves (as)
type Getters<T> = {
  [K in keyof T as `get${Capitalize<string & K>}`]: () => T[K];
};
// Getters<{ nombre: string }> → { getNombre: () => string }
```

### Conditional Types

```typescript
// Tipo condicional básico
type EsString<T> = T extends string ? true : false;

// Con infer (extraer tipo)
type ElementoDe<T> = T extends Array<infer E> ? E : never;
type X = ElementoDe<string[]>;  // string

// Extraer retorno de Promise
type Desenvuelto<T> = T extends Promise<infer R> ? R : T;

// Distributivo sobre uniones
type SinNull<T> = T extends null | undefined ? never : T;
```

### Operadores de tipo

| Operador | Descripción | Ejemplo |
|----------|-------------|---------|
| `keyof T` | Unión de claves de T | `keyof Usuario` → `"nombre" \| "edad"` |
| `typeof x` | Tipo de una variable | `typeof config` |
| `T[K]` | Acceso indexado | `Usuario["nombre"]` → `string` |
| `T[number]` | Elementos de array | `(typeof arr)[number]` |

```typescript
// Combinar operadores
const colores = ["rojo", "verde", "azul"] as const;
type Color = (typeof colores)[number]; // "rojo" | "verde" | "azul"

// Template literal types avanzados
type EventName<T extends string> = `${T}Changed`;
type PropEvents<T> = {
  [K in keyof T as EventName<string & K>]: (val: T[K]) => void;
};
```

---

## 12. Type Guards

> :book: [Ver capítulo completo](capitulos/12-type-guards.md)

```typescript
// typeof — primitivos
function procesar(valor: string | number) {
  if (typeof valor === "string") {
    valor.toUpperCase();   // TS sabe que es string
  } else {
    valor.toFixed(2);      // TS sabe que es number
  }
}

// instanceof — clases
function manejarError(err: Error | string) {
  if (err instanceof Error) {
    console.log(err.message);
  } else {
    console.log(err);
  }
}

// in — propiedades
interface Pez { nadar(): void; }
interface Ave { volar(): void; }

function mover(animal: Pez | Ave) {
  if ("nadar" in animal) {
    animal.nadar();        // Pez
  } else {
    animal.volar();        // Ave
  }
}
```

```typescript
// Predicado personalizado (is)
function esAdmin(usuario: Usuario): usuario is Admin {
  return "permisos" in usuario;
}

// Assertion function (asserts)
function assertNonNull<T>(val: T): asserts val is NonNullable<T> {
  if (val == null) throw new Error("Valor nulo");
}

// satisfies — validar sin ampliar el tipo
const paleta = {
  rojo: [255, 0, 0],
  verde: "#00FF00",
} satisfies Record<string, string | number[]>;
// paleta.rojo sigue siendo number[] (no string | number[])
```

---

## 13. Configuración (tsconfig.json)

> :book: [Ver capítulo completo](capitulos/01-bienvenido.md)

```json
{
  "compilerOptions": {
    // ── Tipado estricto ──
    "strict": true,                    // activa todas las comprobaciones estrictas
    "noUncheckedIndexedAccess": true,   // acceso a índice puede ser undefined

    // ── Entorno de ejecución ──
    "target": "ES2022",                // versión JS de salida
    "lib": ["ES2022", "DOM"],          // APIs disponibles
    "module": "ESNext",                // sistema de módulos
    "moduleResolution": "bundler",     // resolución de módulos

    // ── Interoperabilidad ──
    "esModuleInterop": true,           // import x from "cjs"
    "allowSyntheticDefaultImports": true,
    "isolatedModules": true,           // compatible con esbuild/swc

    // ── Rutas ──
    "baseUrl": ".",
    "paths": {
      "@/*": ["src/*"]                 // alias de importación
    },
    "outDir": "dist",
    "rootDir": "src",

    // ── Declaraciones ──
    "declaration": true,               // generar .d.ts
    "declarationMap": true,            // sourcemaps de declaraciones
    "sourceMap": true,

    // ── Calidad de código ──
    "noUnusedLocals": true,
    "noUnusedParameters": true,
    "noFallthroughCasesInSwitch": true,
    "forceConsistentCasingInFileNames": true,
    "skipLibCheck": true
  },
  "include": ["src/**/*"],
  "exclude": ["node_modules", "dist"]
}
```

!!! info "Opciones más importantes"
    | Opción | Efecto |
    |--------|--------|
    | `strict` | Activa `strictNullChecks`, `noImplicitAny`, `strictFunctionTypes`, etc. |
    | `target` | Qué versión de JS generar (`ES5`, `ES2020`, `ESNext`) |
    | `module` | Sistema de módulos (`CommonJS`, `ESNext`, `NodeNext`) |
    | `moduleResolution` | Cómo resolver imports (`node`, `bundler`, `nodenext`) |
    | `paths` | Alias como `@/componentes` → `src/componentes` |
    | `declaration` | Genera archivos `.d.ts` para librerías |

---

## 14. Patrones comunes

> :book: [Ver capítulo completo](capitulos/12-type-guards.md)

### Optional chaining y Nullish coalescing

```typescript
// Optional chaining (?.)
const ciudad = usuario?.dirección?.ciudad;       // string | undefined
const primero = lista?.[0];                       // acceso seguro a índice
const resultado = obj?.método?.();                // llamada segura a método

// Nullish coalescing (??)
const nombre = input ?? "Anónimo";                // solo si null/undefined
const puerto = config.puerto ?? 3000;

// Combinados
const tema = usuario?.preferencias?.tema ?? "claro";
```

### Aserciones de tipo

```typescript
// Type assertion (as)
const canvas = document.getElementById("c") as HTMLCanvasElement;

// Non-null assertion (!)
const elemento = document.querySelector(".btn")!;  // promesa de no-null

// Const assertion
const rutas = ["inicio", "perfil", "ajustes"] as const;
// tipo: readonly ["inicio", "perfil", "ajustes"]
```

### Patrón Result

```typescript
// Result<T, E> — manejo de errores sin excepciones
type Result<T, E = Error> =
  | { ok: true; valor: T }
  | { ok: false; error: E };

function dividir(a: number, b: number): Result<number, string> {
  if (b === 0) return { ok: false, error: "División por cero" };
  return { ok: true, valor: a / b };
}

const res = dividir(10, 3);
if (res.ok) {
  console.log(res.valor);   // number — TS lo sabe
} else {
  console.log(res.error);   // string
}
```

### Más patrones útiles

```typescript
// Exhaustive check (verificación exhaustiva)
function assertNever(x: never): never {
  throw new Error(`Caso no manejado: ${x}`);
}

// Builder pattern tipado
class QueryBuilder<T> {
  where<K extends keyof T>(campo: K, valor: T[K]): this { return this; }
  orderBy(campo: keyof T): this { return this; }
}

// Type-safe event emitter
type EventMap = {
  login: { userId: string };
  logout: undefined;
  error: { message: string; code: number };
};

function emit<K extends keyof EventMap>(
  evento: K,
  ...args: EventMap[K] extends undefined ? [] : [EventMap[K]]
): void { }

emit("login", { userId: "abc" }); // ✅
emit("logout");                    // ✅
// emit("login");                  // ❌ falta payload
```

---

## 15. Varianza y Tipos Nominales

> :book: [Ver capítulo completo](capitulos/17-varianza-nominal.md)

### Branded Types (tipos nominales)

```typescript
// Problema: MesaId y PedidoId son ambos number
declare const EntityBrand: unique symbol;

type EntityId<Tag extends string> = number & {
  readonly [EntityBrand]: Tag;
};

type MesaId   = EntityId<"Mesa">;
type PedidoId = EntityId<"Pedido">;

function crearMesaId(n: number): MesaId {
  return n as MesaId;
}

function buscarMesa(id: MesaId): void { }

const mid = crearMesaId(1);
buscarMesa(mid);         // ✅
// buscarMesa(42);       // ❌ number ≠ MesaId
// buscarMesa(pedidoId); // ❌ PedidoId ≠ MesaId
```

### Covarianza y contravarianza

| Posición | Varianza | Regla | Anotación |
|----------|----------|-------|-----------|
| Retorno | **Covariante** | `Dog → Animal` ✅ | `out T` |
| Parámetro | **Contravariante** | `Animal → Dog` ✅ | `in T` |
| Ambas | **Invariante** | Solo el mismo tipo | — |

```typescript
// TS 4.7+ — anotaciones explícitas
interface Productor<out T> {
  obtener(): T;
}

interface Consumidor<in T> {
  procesar(item: T): void;
}

// Mutable = invariante (lee Y escribe)
interface Contenedor<in out T> {
  valor: T;
}
```

### Phantom Types (máquinas de estado)

```typescript
type EstadoPedido = "pendiente" | "preparando" | "listo" | "entregado";

interface Pedido<E extends EstadoPedido> {
  readonly id: PedidoId;
  readonly _estado: E;  // phantom — no existe en runtime
  items: string[];
}

// Solo se puede avanzar, no retroceder
function confirmar(p: Pedido<"pendiente">): Pedido<"preparando"> {
  return { ...p, _estado: "preparando" };
}
```

---

## 16. Patrones de librerías

> :book: [Ver capítulo completo](capitulos/18-patrones-librerias.md)

### Query Builder tipado (DSL)

```typescript
interface QueryBuilder<Table, Selected extends keyof Table, Filtered> {
  where<K extends keyof Table>(
    campo: K,
    op: "=" | ">" | "<",
    valor: Table[K]
  ): QueryBuilder<Table, Selected, Filtered & Pick<Table, K>>;

  select<K extends keyof Table>(
    ...campos: K[]
  ): QueryBuilder<Table, K, Filtered>;

  execute(): Promise<Pick<Table, Selected>[]>;
}
```

### Declaration Merging / Module Augmentation

```typescript
// Extender Express Request
declare module "express-serve-static-core" {
  interface Request {
    usuario?: { id: string; rol: string };
  }
}

// Extender Vue ComponentCustomProperties
declare module "vue" {
  interface ComponentCustomProperties {
    $api: ApiClient;
  }
}
```

### Pipe tipado con variadic tuples

```typescript
type PipeFn<A, B> = (a: A) => B;

function pipe<A, B>(value: A, f1: PipeFn<A, B>): B;
function pipe<A, B, C>(value: A, f1: PipeFn<A, B>, f2: PipeFn<B, C>): C;
function pipe<A, B, C, D>(
  value: A, f1: PipeFn<A, B>, f2: PipeFn<B, C>, f3: PipeFn<C, D>
): D;
function pipe(value: unknown, ...fns: Function[]): unknown {
  return fns.reduce((acc, fn) => fn(acc), value);
}
```

### Const type parameters (TS 5.0+)

```typescript
// Sin const — se pierde la literalidad
function rutas<T extends Record<string, string>>(r: T): T { return r; }
rutas({ home: "/" }); // { home: string }  😞

// Con const — preserva literales
function rutas<const T extends Record<string, string>>(r: T): T { return r; }
rutas({ home: "/" }); // { readonly home: "/" }  ✅
```

| Patrón | Cuándo usar | Ejemplo real |
|--------|-------------|-------------|
| Overloads | 2-3 firmas distintas | `createElement()` |
| Conditional types | Retorno depende del input | `Awaited<T>` |
| `const` type param | Preservar literales | `defineRoutes()` |
| Declaration merging | Extender librerías | Plugin systems |
| Builder pattern | API fluida | Query builders |

---

## 17. Rendimiento y escala

> :book: [Ver capítulo completo](capitulos/19-rendimiento-escala.md)

### Project References

```json
// tsconfig.json (raíz del monorepo)
{
  "references": [
    { "path": "packages/shared" },
    { "path": "packages/api" },
    { "path": "packages/web" }
  ]
}

// packages/shared/tsconfig.json
{
  "compilerOptions": {
    "composite": true,
    "declaration": true,
    "declarationMap": true,
    "outDir": "dist"
  }
}
```

```bash
# Build incremental (solo lo que cambió)
tsc --build --verbose

# Limpiar archivos de build
tsc --build --clean
```

### Module Resolution

| Opción | Cuándo usar | `import "./foo"` resuelve |
|--------|-------------|--------------------------|
| `node16` | Node.js puro (ESM) | `./foo.js` obligatorio |
| `bundler` | Vite, esbuild, webpack | `./foo` (sin extensión) |
| `nodenext` | Node.js latest | Igual que `node16` |

### Exports map (package.json)

```json
{
  "name": "@makemenu/validation",
  "exports": {
    ".": {
      "types": "./dist/index.d.ts",
      "import": "./dist/index.mjs",
      "require": "./dist/index.cjs"
    }
  }
}
```

!!! warning "Orden de exports"
    `"types"` siempre debe ir **primero** en cada entrada del exports map.

### Flags de rendimiento

| Flag | Efecto | Cuándo activar |
|------|--------|---------------|
| `isolatedModules` | 1 archivo = 1 unidad | Siempre con esbuild/swc |
| `verbatimModuleSyntax` | Import = lo que escribes | TS 5.0+ |
| `skipLibCheck` | No chequear `.d.ts` | Siempre (velocidad) |
| `incremental` | Cache de `.tsbuildinfo` | Proyectos grandes |

---

## 18. Testing de tipos

> :book: [Ver capítulo completo](capitulos/20-testing-libreria.md)

### `expectTypeOf` (Vitest)

```typescript
import { expectTypeOf } from "vitest";

// Verificar tipo exacto
expectTypeOf(miVariable).toEqualTypeOf<string>();

// Verificar compatibilidad (más flexible)
expectTypeOf(miVariable).toMatchTypeOf<string>();

// Verificar parámetros de función
expectTypeOf(miFn).parameter(0).toEqualTypeOf<number>();

// Verificar retorno
expectTypeOf(miFn).returns.toEqualTypeOf<string>();
```

### `@ts-expect-error` como assertion

```typescript
// Verificar que algo NO compila (es un error)
// @ts-expect-error — MesaId no es asignable a PedidoId
const pid: PedidoId = mesaId;

// @ts-expect-error — faltan propiedades requeridas
const mesa: Mesa = { id: 1 };
```

### API completa de `expectTypeOf`

| Método | Verifica |
|--------|----------|
| `.toEqualTypeOf<T>()` | Tipo exacto (bidireccional) |
| `.toMatchTypeOf<T>()` | Compatible (unidireccional) |
| `.toBeString()` | Es `string` |
| `.toBeNumber()` | Es `number` |
| `.toBeNullable()` | Incluye `null \| undefined` |
| `.toBeCallableWith(args)` | Se puede llamar con esos args |
| `.parameter(n)` | Tipo del parámetro n |
| `.returns` | Tipo de retorno |
| `.items` | Tipo de elementos de array |

### Checklist de publicación de librería

```typescript
// ✅ Lista de verificación antes de publicar
// 1. exports map con "types" primero
// 2. declaration: true, declarationMap: true
// 3. attw (Are The Types Wrong?) pasa
// 4. Tests de tipos con expectTypeOf
// 5. Dual CJS/ESM si es necesario
// 6. README con ejemplos tipados
```

---

## 19. Glosario TypeScript

Referencia alfabética de los términos clave del sistema de tipos de TypeScript.

| Término | Definición | Capítulo |
|---------|-----------|----------|
| **Branded type** | Tipo nominal simulado mediante una propiedad fantasma (`& { __brand: Tag }`). Evita mezclar valores que comparten el mismo tipo base (ej. `UserId` vs `OrderId`). | [8. Enums y Literales](#8-enums-y-literales), [15. Varianza](#15-varianza-y-tipos-nominales) |
| **Conditional type** | Tipo que selecciona entre dos ramas con la sintaxis `T extends U ? A : B`. Permite transformaciones dependientes del tipo de entrada. | [11. Tipos avanzados](#11-tipos-avanzados) |
| **Contravariance** | Propiedad de un parámetro de tipo que permite sustituir por un tipo **más general** (supertipo). Se da en posiciones de parámetros de función. Anotación: `in T`. | [15. Varianza](#15-varianza-y-tipos-nominales) |
| **Covariance** | Propiedad de un parámetro de tipo que permite sustituir por un tipo **más específico** (subtipo). Se da en posiciones de retorno. Anotación: `out T`. | [15. Varianza](#15-varianza-y-tipos-nominales) |
| **Declaration merging** | Capacidad de TypeScript para fusionar múltiples declaraciones de la misma `interface` en una sola definición. Permite extender tipos de librerías externas. | [3. Objetos](#3-objetos-e-interfaces), [16. Patrones de librerías](#16-patrones-de-librerias) |
| **Discriminated union** | Unión de tipos objeto donde cada miembro tiene una propiedad literal común (el "discriminante") que permite a TypeScript hacer narrowing automático en un `switch` o `if`. | [5. Uniones y Narrowing](#5-uniones-y-narrowing) |
| **Higher-kinded types (HKT)** | Tipos que aceptan otros constructores de tipo como parámetros. TypeScript no los soporta nativamente, pero se pueden simular con interfaces y mapped types. | [11. Tipos avanzados](#11-tipos-avanzados) |
| **Mapped type** | Tipo que transforma cada propiedad de otro tipo usando la sintaxis `{ [K in keyof T]: ... }`. Base de utility types como `Partial`, `Readonly`, `Pick`. | [11. Tipos avanzados](#11-tipos-avanzados) |
| **Module augmentation** | Técnica para agregar declaraciones a un módulo existente usando `declare module "nombre" { ... }`. Útil para extender tipos de librerías de terceros. | [10. Módulos](#10-modulos), [16. Patrones de librerías](#16-patrones-de-librerias) |
| **Narrowing** | Proceso por el cual TypeScript reduce un tipo amplio a uno más específico dentro de un bloque condicional (ej. `typeof`, `instanceof`, `in`, predicados). | [5. Uniones y Narrowing](#5-uniones-y-narrowing), [12. Type Guards](#12-type-guards) |
| **Nominal typing** | Sistema de tipos donde la compatibilidad se basa en el **nombre** del tipo, no en su estructura. TypeScript es estructural por defecto; se simula con branded types. | [15. Varianza](#15-varianza-y-tipos-nominales) |
| **Phantom type** | Parámetro de tipo genérico que no se usa en la estructura de datos en runtime, pero restringe operaciones a nivel de tipo. Útil para máquinas de estado. | [15. Varianza](#15-varianza-y-tipos-nominales) |
| **Structural typing** | Sistema de tipos de TypeScript donde la compatibilidad se determina por la **forma** (propiedades y sus tipos), no por el nombre o la declaración del tipo. | [3. Objetos](#3-objetos-e-interfaces) |
| **Template literal type** | Tipo construido con template strings a nivel de tipos: `` type EventName = `on${string}` ``. Permite patrones de cadenas tipados. | [8. Enums y Literales](#8-enums-y-literales), [11. Tipos avanzados](#11-tipos-avanzados) |
| **Type annotation** | Sintaxis explícita para declarar el tipo de una variable, parámetro o retorno usando `:` (ej. `let x: number`). | [1. Tipos primitivos](#1-tipos-primitivos) |
| **Type assertion** | Expresión que le dice al compilador que trate un valor como un tipo específico usando `as T` o `<T>`. No cambia el valor en runtime. | [14. Patrones comunes](#14-patrones-comunes) |
| **Type guard** | Expresión condicional que permite a TypeScript estrechar (narrow) el tipo de una variable. Incluye `typeof`, `instanceof`, `in`, predicados `is` y funciones `asserts`. | [12. Type Guards](#12-type-guards) |
| **Type inference** | Capacidad de TypeScript para deducir automáticamente el tipo de una variable o expresión sin necesidad de anotación explícita. | [1. Tipos primitivos](#1-tipos-primitivos) |
| **Type predicate** | Tipo de retorno especial de la forma `param is Type` que actúa como type guard personalizado. Permite lógica de narrowing definida por el usuario. | [5. Uniones y Narrowing](#5-uniones-y-narrowing), [12. Type Guards](#12-type-guards) |
| **Type-level programming** | Técnica de programar lógica exclusivamente en el sistema de tipos usando conditional types, mapped types, recursión y `infer`. El código solo existe en compilación. | [11. Tipos avanzados](#11-tipos-avanzados) |
| **Utility type** | Tipo genérico integrado en TypeScript que transforma otros tipos. Incluye `Partial`, `Required`, `Readonly`, `Pick`, `Omit`, `Record`, `Exclude`, `Extract`, `ReturnType`, etc. | [7. Utility Types](#7-utility-types) |
| **Variance** | Propiedad que describe cómo la relación de subtipo entre tipos genéricos se ve afectada por sus parámetros de tipo. Incluye covarianza, contravarianza e invarianza. | [15. Varianza](#15-varianza-y-tipos-nominales) |
| **Widening** | Comportamiento por defecto donde TypeScript amplía tipos literales a su tipo base (ej. `"hola"` se convierte en `string`). Se previene con `as const` o anotaciones literales. | [8. Enums y Literales](#8-enums-y-literales) |
| **`infer` keyword** | Palabra clave usada dentro de conditional types para extraer y capturar un tipo: `T extends Array<infer E> ? E : never`. | [11. Tipos avanzados](#11-tipos-avanzados) |
| **`keyof` operator** | Operador de tipo que produce una unión de las claves (propiedades) de un tipo objeto: `keyof Usuario` resulta en `"nombre" \| "edad"`. | [6. Generics](#6-generics), [11. Tipos avanzados](#11-tipos-avanzados) |
| **`satisfies` operator** | Operador (TS 4.9+) que valida que un valor cumple con un tipo sin ampliar su tipo inferido. Combina seguridad de tipo con inferencia precisa. | [12. Type Guards](#12-type-guards) |

---

## 20. Snippets reutilizables

Patrones de tipo copy-paste listos para usar en tus proyectos.

### Result\<T, E\>

Manejo de errores tipado sin excepciones, inspirado en Rust.

```typescript
type Result<T, E = Error> =
  | { ok: true; valor: T }
  | { ok: false; error: E };

function ok<T>(valor: T): Result<T, never> {
  return { ok: true, valor };
}

function err<E>(error: E): Result<never, E> {
  return { ok: false, error };
}
```

### ApiResponse\<T\>

Respuesta de API estandarizada con soporte para paginacion y errores.

```typescript
type ApiResponse<T> =
  | { status: "success"; data: T; meta?: { page: number; total: number } }
  | { status: "error"; error: { code: number; message: string } };

async function fetchApi<T>(url: string): Promise<ApiResponse<T>> {
  const res = await fetch(url);
  if (!res.ok) {
    return { status: "error", error: { code: res.status, message: res.statusText } };
  }
  return { status: "success", data: await res.json() };
}
```

### EntityId\<Tag\>

Branded type generico para IDs nominales que evita mezclar entidades.

```typescript
declare const EntityBrand: unique symbol;

type EntityId<Tag extends string> = number & {
  readonly [EntityBrand]: Tag;
};

function createId<Tag extends string>(value: number): EntityId<Tag> {
  return value as EntityId<Tag>;
}

// Uso:
type UserId = EntityId<"User">;
type OrderId = EntityId<"Order">;
const uid = createId<"User">(1);
const oid = createId<"Order">(1);
// uid === oid  → error de tipo ✅
```

### DeepPartial\<T\>

Hace opcionales todas las propiedades de forma recursiva, incluyendo objetos anidados.

```typescript
type DeepPartial<T> = T extends object
  ? { [K in keyof T]?: DeepPartial<T[K]> }
  : T;

// Uso:
interface Config {
  db: { host: string; port: number; ssl: { enabled: boolean; cert: string } };
  log: { level: string };
}
type PatchConfig = DeepPartial<Config>;
// PatchConfig.db?.ssl?.enabled es boolean | undefined ✅
```

### Prettify\<T\>

Aplana intersecciones para que el tooltip del IDE muestre las propiedades directamente.

```typescript
type Prettify<T> = {
  [K in keyof T]: T[K];
} & {};

// Uso:
type Merged = Prettify<{ a: string } & { b: number }>;
// Tooltip muestra: { a: string; b: number } en vez de { a: string } & { b: number }
```

### StrictOmit\<T, K\>

Version segura de `Omit` que solo permite omitir claves que realmente existen en `T`.

```typescript
type StrictOmit<T, K extends keyof T> = Omit<T, K>;

// Uso:
interface Usuario {
  id: number;
  nombre: string;
  email: string;
}
type SinEmail = StrictOmit<Usuario, "email">;     // ✅ compila
// type Mal = StrictOmit<Usuario, "noExiste">;     // ❌ error de compilacion
```

### Discriminated union con exhaustive switch

Patron completo de union discriminada con verificacion exhaustiva.

```typescript
type Accion =
  | { tipo: "crear"; payload: { nombre: string } }
  | { tipo: "editar"; payload: { id: number; nombre: string } }
  | { tipo: "borrar"; payload: { id: number } };

function assertNever(x: never): never {
  throw new Error(`Caso no manejado: ${JSON.stringify(x)}`);
}

function reducer(estado: Estado, accion: Accion): Estado {
  switch (accion.tipo) {
    case "crear":
      return { ...estado, items: [...estado.items, accion.payload] };
    case "editar":
      return { ...estado, /* actualizar item */ };
    case "borrar":
      return { ...estado, items: estado.items.filter(i => i.id !== accion.payload.id) };
    default:
      return assertNever(accion); // ❌ error si falta un caso
  }
}
```

### Type-safe event emitter

Emisor de eventos con tipado completo de nombres y payloads.

```typescript
type EventMap = Record<string, unknown>;

class TypedEmitter<Events extends EventMap> {
  private listeners = new Map<keyof Events, Set<Function>>();

  on<K extends keyof Events>(
    evento: K,
    handler: (payload: Events[K]) => void
  ): void {
    if (!this.listeners.has(evento)) this.listeners.set(evento, new Set());
    this.listeners.get(evento)!.add(handler);
  }

  emit<K extends keyof Events>(
    evento: K,
    ...args: Events[K] extends undefined ? [] : [Events[K]]
  ): void {
    this.listeners.get(evento)?.forEach(fn => fn(...args));
  }
}

// Uso:
interface AppEvents {
  login: { userId: string; timestamp: number };
  logout: undefined;
  error: { message: string; code: number };
}

const bus = new TypedEmitter<AppEvents>();
bus.on("login", ({ userId }) => console.log(userId)); // ✅ tipado
bus.emit("logout");                                     // ✅ sin payload
// bus.emit("login");                                   // ❌ falta payload
```

---

## 21. Python ↔ TypeScript equivalencias rapidas

Tabla de referencia para programadores que vienen de Python.

| Python | TypeScript | Notas |
|--------|-----------|-------|
| `dict` | `Record<K, V>` o `Map<K, V>` | `Record` para objetos planos, `Map` para claves no-string |
| `list` | `T[]` o `Array<T>` | Ambas sintaxis son equivalentes |
| `tuple` | `[T1, T2, ...]` | Tuplas con longitud y tipos fijos |
| `set` | `Set<T>` | Misma semantica que en Python |
| `Optional[str]` | `string \| undefined` | En TS se usa union con `undefined` (o `null`) |
| `Union[str, int]` | `string \| number` | Union nativa con `\|` |
| `TypedDict` | `interface` | Interfaz con propiedades tipadas |
| `Protocol` | `interface` | Ambos son tipado estructural |
| `@dataclass` | `class` con parameter properties | `constructor(public x: number)` genera la propiedad |
| `Enum` | `enum` o `as const` | `as const` es mas idiomatico en TS moderno |
| `*args` | `...args: T[]` | Rest parameters tipados |
| `**kwargs` | `options: Partial<Config>` | Objeto de opciones con propiedades opcionales |
| `@property` | `get` / `set` | Accessors nativos de JS/TS |
| `__init__` | `constructor` | Mismo proposito, sintaxis diferente |
| `type[T]` (la clase misma) | `new (...args: any[]) => T` | Constructor signature para pasar clases como valor |
| `Callable[[int], str]` | `(n: number) => string` | Tipo funcion con firma explicita |
| `Generator[Y, S, R]` | `Generator<Y, R, N>` | Generadores tipados (orden de parametros difiere) |
| `Any` | `any` (evitar) o `unknown` (preferido) | `unknown` obliga a hacer narrowing, mas seguro |
| `None` | `void` (retorno) o `undefined` (valor) | `void` para funciones, `undefined` para variables |
| `assert isinstance(x, str)` | Type guard o assertion function | `asserts x is string` o `if (typeof x === "string")` |

**Ejemplo comparativo completo:**

=== "Python"

    ```python
    from dataclasses import dataclass
    from typing import Optional, Union

    @dataclass
    class Usuario:
        id: int
        nombre: str
        email: Optional[str] = None

    def buscar(
        query: str,
        *tags: str,
        limite: int = 10,
        **opciones: Union[str, int]
    ) -> list[Usuario]:
        ...
    ```

=== "TypeScript"

    ```typescript
    class Usuario {
      constructor(
        public id: number,
        public nombre: string,
        public email?: string,   // undefined si no se pasa
      ) {}
    }

    function buscar(
      query: string,
      ...tags: string[]
    ): Usuario[];
    function buscar(
      query: string,
      opciones?: { limite?: number } & Record<string, string | number>
    ): Usuario[];
    function buscar(query: string, ...args: unknown[]): Usuario[] {
      // implementación
    }
    ```

---

## Atajos de teclado

| Atajo | Acción |
|-------|--------|
| ++alt+f++ | Siguiente flashcard (foco) |
| ++alt+r++ | Revelar / ocultar todas las flashcards |
| ++enter++ o ++space++ | Voltear flashcard actual |

!!! note "Navegación rápida"
    Usa la **tabla de contenidos** de la derecha para saltar directamente a cualquier sección. En móvil, toca el icono de menú (:material-table-of-contents:).
