# Convenciones y Estilos de Codificación en JavaScript

- [Convenciones y Estilos de Codificación en JavaScript](#convenciones-y-estilos-de-codificación-en-javascript)
    - [Introducción](#introducción)
    - [1. Convención de Nombres](#1-convención-de-nombres)
    - [2. Nombres de archivos](#2-nombres-de-archivos)
    - [3. Modularización](#3-modularización)
    - [4. Convenciones generales de codificación](#4-convenciones-generales-de-codificación)
    - [5. Buenas prácticas](#5-buenas-prácticas)
    - [6. Estilo de Comentarios](#6-estilo-de-comentarios)
    - [7. Pruebas y Validación](#7-pruebas-y-validación)
    - [Recursos adicionales](#recursos-adicionales)

## Introducción

El presente documento tiene como objetivo establecer las convenciones y estilos de codificación a seguir para el desarrollo de código en JavaScript en el proyecto actual. Estas convenciones y estilos están diseñados para mejorar la legibilidad, mantenibilidad y eficiencia del código, así como para fomentar las mejores prácticas de programación.

## 1. Convención de Nombres

- Utiliza nombres descriptivos y significativos para las variables y funciones, evitando abreviaciones confusas.
- Utiliza **camelCase** (con la primera letra en minúscula) para las variables y funciones. **Ejemplo:** `miVariable`, `calcularPrecioTotal()`.
- Utiliza siempre **UPPERCASE** y separación de palabras con guiones bajos para las constantes y variables globales. **Ejemplo:** `MAXIMO_INTENTOS`, `VALOR_PI`.
- Utiliza **UpperCamelCase** para los nombres de las clases. **Ejemplo:** `MiClase`, `UsuarioRegistrado`.

## 2. Nombres de archivos

- Utiliza nombres descriptivos y significativos para los archivos.
- Utiliza **kebab-case** para los nombres de archivos, comenzando con una letra minúscula. **Ejemplo:** `mi-archivo.js`.
- Los nombres de los directorios deben ser en plural y representar la categoría de los archivos contenidos.

## 3. Modularización

- Separa el código en módulos y archivos según su funcionalidad y responsabilidad.
- Utiliza nombres descriptivos y significativos para los módulos. **Ejemplo:** `usuarios.js`, `productos.js`.
- Importa y exporta módulos de forma consistente usando import y export en ES6.

## 4. Convenciones generales de codificación

- Utilizar líneas de código de un máximo de 80 caracteres, evitando líneas largas que dificulten la lectura.
- Utiliza una indentación consistente de 2 espacios para mejorar la legibilidad del código.
- Usa punto y coma (;) al final de cada declaración para evitar errores inesperados.
- Utiliza un espacio entre los operadores y operandos para mejorar la claridad del código. **Ejemplo:** `total = precio * cantidad;`
- Utilizar una sola instrucción por línea de código.
- Evitar el uso de comentarios innecesarios o confusos.

## 5. Buenas prácticas

- Evitar siempre el uso de variables globales.
- Siempre declarar variables locales con las palabras claves `let` o `const`. Preferir `const` cuando la variable no será reasignada.
- Es una buena práctica poner todas las declaraciones de variables al inicio de cada script o función.
- Inicializar siempre las variables una vez son declaradas.
- Declarar Objects con `const` para evitar cambios accidentales de tipo.

```js
const car = { type: "Fiat", model: "500", color: "white" };
// car = "Fiat"; // Not possible
```

- Declarar Arrays con const para evitar cambios accidentales de tipo.

```js
const cars = ["Saab", "Volvo", "BMW"];
// cars = 3; // Not possible
```

- No usar `new Object()`.
- Usar `""` en vez de `new String()`
- Usar `0` en vez de `new Number()`
- Usar `false` en vez de `new Boolean()`
- Usar `{}` en vez de `new Object()`
- Usar `[]` en vez de `new Array()`
- Usar `/()/` en vez de `new RegExp()`
- Usar `function (){}` en vez de `new Function()`
- Usar el operador de comparación estricto `===` y `!==`. Estos operadores fuerzan la comparación del valor y el tipo.
- Evitar el uso de `eval()`, ya que podría permitir la ejecución de código arbitrario y representar un problema de seguridad.

## 6. Estilo de Comentarios

- Utiliza comentarios para explicar el "por qué" detrás de un bloque de código complejo.
- Prefiere comentarios de línea (//) para anotaciones breves.
- Utiliza comentarios de bloque (/* */) para descripciones más largas o cuando es necesario comentar varias líneas.
- Utiliza JSDoc para documentar funciones, métodos y clases.

**Ejemplo de JSDoc:**

```js
/**
 * Suma dos números.
 * @param {number} a - El primer número.
 * @param {number} b - El segundo número.
 * @returns {number} La suma de los dos números.
 */
function sumar(a, b) {
  return a + b;
}
```


## 7. Pruebas y Validación

- Validar el código con herramientas de linters como ESLint para mantener la calidad del código.

**Ejemplo de configuración básica de ESLint:**

```yaml
{
  "extends": "eslint:recommended",
  "env": {
    "browser": true,
    "es2021": true
  },
  "parserOptions": {
    "ecmaVersion": 12,
    "sourceType": "module"
  },
  "rules": {
    "indent": ["error", 2],
    "linebreak-style": ["error", "unix"],
    "quotes": ["error", "single"],
    "semi": ["error", "always"]
  }
}
```

- Asegurarse de que todas las pruebas pasen antes de fusionar código en la rama principal.
- (opcional) Escribir pruebas unitarias para todas las funciones y métodos importantes.
- (opcional) Utilizar frameworks de pruebas como Jest o Mocha para estructurar y ejecutar los tests.


## Recursos adicionales

- [JavaScript Coding Conventions](https://www.w3schools.com/js/js_conventions.asp)
- [Google JavaScript Style Guide](https://google.github.io/styleguide/jsguide.html)
- [JavaScript Coding Standards](https://developer.wordpress.org/coding-standards/wordpress-coding-standards/javascript/)