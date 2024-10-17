# Estilos de Codificación en PHP con Symfony

- [Estilos de Codificación en PHP con Symfony](#estilos-de-codificación-en-php-con-symfony)
    - [1. Introducción](#1-introducción)
    - [2. Convenciones generales de codificación](#2-convenciones-generales-de-codificación)
    - [3. Nombres de archivos y directorios](#3-nombres-de-archivos-y-directorios)
    - [4. Nombres de clases](#4-nombres-de-clases)
    - [5. Nombres de variables y constantes](#5-nombres-de-variables-y-constantes)
    - [6. Estilo de código](#6-estilo-de-código)
    - [7. Estructura de archivos y directorios](#7-estructura-de-archivos-y-directorios)
    - [8. Comentarios y documentación de código](#8-comentarios-y-documentación-de-código)
    - [9. Control de versiones](#9-control-de-versiones)
    - [10. Pruebas unitarias y de integración](#10-pruebas-unitarias-y-de-integración)
    - [11. Patrones de diseño](#11-patrones-de-diseño)
    - [12. Recursos adicionales](#12-recursos-adicionales)

## 1. Introducción

El presente documento establece los estilos de codificación recomendados para el desarrollo del proyecto en lenguaje PHP utilizando el framework Symfony. Estos estilos tienen como objetivo mejorar la legibilidad, mantenibilidad y colaboración en el código fuente del proyecto.

Indistintamente de que el documento hace anotaciones sobre los principales estándares de codificación, o hace énfasis en aquellos que son más importantes, estos son una reducción de los estándares de codificación PSR-1 y PSR-12 (PSR-2 queda deprecated) los cuales son de obligatorio cumplimiento en el desarrollo de los sistemas implementados.

## 2. Convenciones generales de codificación

- Utilizar siempre indentación de 4 espacios, sin tabulaciones.
- Utilizar siempre el formato de codificación UTF-8 sin BOM.
- Utilizar líneas de código de un máximo de 80 caracteres, evitando líneas largas que dificulten la lectura.
- Utilizar una sola instrucción por línea de código.
- Utilizar siempre llaves de apertura en la misma línea que la declaración, y llaves de cierre en su propia línea.
- Utilizar nombres descriptivos para las variables y funciones, evitando abreviaturas o nombres poco claros.
- Evitar el uso de comentarios innecesarios o confusos.

## 3. Nombres de archivos y directorios

- Los nombres de los archivos deben ser descriptivos y relacionados con su contenido.
- Los nombres de los directorios deben ser en plural y representar la categoría de los archivos contenidos.

**Ejemplo:**

- Directorio: controladores/

## 4. Nombres de clases

- Utilizar el estándar de nomenclatura de clases de Symfony.
- Utilizar el patrón de nomenclatura **UpperCamelCase** para los nombres de clases.
- Utilizar nombres descriptivos y significativos para las clases.

**Ejemplo:**

```php
namespace App\Controller;

use Symfony\Bundle\FrameworkBundle\Controller\AbstractController;
use Symfony\Component\HttpFoundation\Response;

class MiControlador extends AbstractController
{
    // ...
}
```


## 5. Nombres de variables y constantes

- Utilizar el patrón de nomenclatura **lowerCamelCase** para los nombres de variables.
- Utilizar siempre **UPPERCASE** y separación de palabras con guiones bajos para las constantes.
- Utilizar nombres descriptivos y significativos para las variables y constantes.
- Evitar el uso de nombres genéricos o abreviaturas que dificulten la comprensión del código.

**Ejemplo:**

```php
$nombreUsuario = 'John Doe';
const RUTA_ARCHIVOS = '/var/www/proyecto/archivos/';
```


## 6. Estilo de código

- Utilizar espacios alrededor de los operadores para mejorar la legibilidad del código.
- Utilizar espacios después de las comas en listas de argumentos o elementos de arrays.
- Utilizar una sola línea en sentencias if, else, foreach, etc., cuando sea posible y no se sacrifique la legibilidad.

**Ejemplo:**

```php
if ($condicion) {
    // ...
} else {
    // ...
}

foreach ($array as $elemento) {
    // ...
}
```


## 7. Estructura de archivos y directorios

- Utilizar la estructura recomendada por Symfony para organizar el código del proyecto.
- Separar el código en directorios lógicos (controladores, modelos, vistas, etc.) para facilitar la navegación y mantenimiento del mismo.

**Ejemplo:**

```
src/
├── Controller/
├── Model/
├── View/
└── ...
```


## 8. Comentarios y documentación de código

- Utilizar comentarios claros y concisos para explicar el propósito y funcionamiento del código.
- Documentar las clases, métodos y funciones utilizando anotaciones de PHPDoc.
- Asegurarse de que la documentación esté actualizada y refleje los cambios realizados en el código.

**Ejemplo:**

```php
/**
 * Clase que representa un usuario en el sistema.
 *
 * @ORM\Entity
 * @ORM\Table(name="usuarios")
 */
class Usuario
{
    // ...
}
```


## 9. Control de versiones

- Utilizar un sistema de control de versiones como Git para gestionar el código fuente del proyecto.
- Utilizar ramas (branches) para trabajar en nuevas funcionalidades o correcciones de errores, y fusionarlas al tronco principal (main) una vez completadas y probadas.
- Utilizar mensajes de confirmación claros y descriptivos al realizar cambios en el código.

## 10. Pruebas unitarias y de integración

- Implementar pruebas unitarias y de integración utilizando herramientas como PHPUnit.
- Escribir pruebas para cubrir diferentes escenarios y asegurar la calidad del código.
- Ejecutar las pruebas de forma regular y corregir los errores identificados.

**Ejemplo de prueba unitaria:**

```php
use PHPUnit\Framework\TestCase;

class UsuarioTest extends TestCase
{
    public function testNombreUsuario()
    {
        $usuario = new Usuario();
        $usuario->setNombre('John Doe');
        $this->assertEquals('John Doe', $usuario->getNombre());
    }
}
```


## 11. Patrones de diseño

- Utilizar patrones de diseño recomendados por Symfony y la comunidad PHP cuando sea necesario para mejorar la estructura y modularidad del código.
- Evitar el uso excesivo de patrones de diseño que puedan complicar innecesariamente el código.

**Ejemplo:**

- Utilizar el patrón de diseño Singleton para asegurarse de que una clase tenga solo una instancia.
- Utilizar el patrón de diseño Factory para la creación de objetos.

## 12. Recursos adicionales

- Symfony Coding Standards: [Symfony Coding Standards](https://symfony.com/doc/current/contributing/code/standards.html)
- PSR-1: Basic Coding Standard: [PSR-1](https://www.php-fig.org/psr/psr-1/)
- PSR-12: Extended Coding Style Guide: [PSR-12](https://www.php-fig.org/psr/psr-12/)
