# Patrones de diseño

- [Patrones de diseño](#patrones-de-diseño)
  - [Patrones SOLID](#patrones-solid)
    - [\[MUST\] Principio de Responsabilidad Única](#must-principio-de-responsabilidad-única)
      - [Ejemplo](#ejemplo)
    - [\[MUST\] Principio de Abierto/Cerrado](#must-principio-de-abiertocerrado)
      - [Ejemplo](#ejemplo-1)
    - [\[MUST\] Principio de Sustitución de Liskov](#must-principio-de-sustitución-de-liskov)
      - [Ejemplo](#ejemplo-2)
    - [\[MUST\] Principio de Segregación de Interfaces](#must-principio-de-segregación-de-interfaces)
      - [Ejemplo](#ejemplo-3)
    - [\[MUST\] Principio de Inversión de Dependencias](#must-principio-de-inversión-de-dependencias)
      - [Ejemplo](#ejemplo-4)
  - [Patrones ligados a Symfony](#patrones-ligados-a-symfony)
    - [Singleton](#singleton)
    - [Observer](#observer)
    - [Factory](#factory)
    - [Repository](#repository)
    - [Dependency Injection](#dependency-injection)
  - [Otros Patrones de Diseño](#otros-patrones-de-diseño)
    - [\[MUST\] Speaking Code Principle (SCP)](#must-speaking-code-principle-scp)
    - [\[MUST\] Keep It Simple, Stupid (KISS)](#must-keep-it-simple-stupid-kiss)
    - [\[MUST\] Don't Repeat Yourself (DRY)](#must-dont-repeat-yourself-dry)
    - [\[SHOULD\] You Ain't Gonna Need It! (YAGNI)](#should-you-aint-gonna-need-it-yagni)
    - [\[SHOULD\] Law Of Demeter](#should-law-of-demeter)


## Patrones SOLID

### [MUST] Principio de Responsabilidad Única

El **S**ingle **R**esponsibility **P**rinciple(SRP) es uno de los principios fundamentales del diseño de software y establece que una clase o módulo debe tener una única razón para cambiar. En otras palabras, cada clase debería tener una única responsabilidad y debería haber una sola razón por la cual una clase deba ser modificada.

#### Ejemplo

```php
class BookRegistration {
    public function registerBook($bookTitle, $author) {
        // Lógica para registrar el libro en la base de datos
        // ...
    }
}

class BookDisplay {
    public function displayBook($bookId) {
        // Lógica para recuperar la información del libro de la base de datos
        // y mostrarla en pantalla
        // ...
    }
}
```

En este ejemplo, la clase `BookRegistration` se encarga únicamente de la lógica de registro de libros, mientras que la clase `BookDisplay` se encarga únicamente de la lógica de visualización. De esta manera, cada clase tiene una única responsabilidad y una única razón para cambiar. Si en el futuro necesitamos modificar la lógica de registro, solo tendremos que hacer cambios en la clase `BookRegistration`, sin afectar la lógica de visualización.

Aplicar el principio de responsabilidad única tiene varios beneficios, como mejorar la mantenibilidad del código, facilitar la reutilización de clases y reducir el acoplamiento entre componentes.

### [MUST] Principio de Abierto/Cerrado

El principio Open Closed (OCP) es un concepto fundamental en la ingeniería de software que establece que las entidades de software (clases, módulos, funciones, etc.) deben estar abiertas para su extensión pero cerradas para su modificación. En pocas palabras, significa que deberíamos poder extender el comportamiento de una clase sin modificar el código fuente existente.

#### Ejemplo

Supongamos que tenemos una aplicación que permite calcular el área de diferentes formas geométricas, como círculos y rectángulos. Podríamos tener una clase "Shape" que contiene un método "calculateArea()" para calcular el área de la forma geométrica:  

```php
class Shape {
  // ...
  
  public function calculateArea() {
    // Cálculo de área genérico
  }
}
```

Ahora, si queremos agregar una nueva forma geométrica, como un triángulo, podríamos simplemente extender la clase "Shape" y proporcionar una implementación específica para el cálculo del área del triángulo:  
  

```php

class Triangle extends Shape {
  // ...
  
  public function calculateArea() {
    // Cálculo de área específico para triángulos
  }
}
```

De esta manera, podemos agregar una nueva forma geométrica sin modificar el código existente en la clase "Shape". La clase "Shape" está cerrada para modificaciones, pero abierta para extensiones a través de la herencia.

El principio Open Closed nos permite agregar nuevas funcionalidades sin afectar el código existente, lo que facilita la mantenibilidad y la reutilización del código. Además, ayuda a evitar efectos secundarios no deseados al modificar clases existentes.

### [MUST] Principio de Sustitución de Liskov

El principio de Liskov Substitution se refiere a la capacidad de usar una clase base y sus subclases de manera indistinta, sin afectar el correcto funcionamiento del programa. Para entenderlo mejor, imagina una jerarquía de clases que representan diferentes formas geométricas, como un cuadrado, un rectángulo y un triángulo.

#### Ejemplo

```php
class Forma {
    protected $ancho;
    protected $alto;
    
    public function setAncho($ancho) {
        $this->ancho = $ancho;
    }
    
    public function setAlto($alto) {
        $this->alto = $alto;
    }
    
    public function getArea() {
        return $this->ancho * $this->alto;
    }
}

class Cuadrado extends Forma {
    public function setAncho($ancho) {
        $this->ancho = $ancho;
        $this->alto = $ancho;
    }
    
    public function setAlto($alto) {
        $this->alto = $alto;
        $this->ancho = $alto;
    }
}

class Rectangulo extends Forma {
    // no se necesitan cambios en esta clase
}

function imprimirArea(Forma $forma) {
    $forma->setAncho(5);
    $forma->setAlto(10);
    echo "El área es: " . $forma->getArea();
}

// Ejemplo de uso
$forma1 = new Forma();
$forma2 = new Cuadrado();
$forma3 = new Rectangulo();

imprimirArea($forma1);   // Salida: El área es: 50
imprimirArea($forma2);   // Salida: El área es: 25
imprimirArea($forma3);   // Salida: El área es: 50
```

En este ejemplo, tenemos una clase base llamada "Forma" que tiene propiedades de ancho y alto, y un método "getArea" para calcular el área de la forma geométrica. Luego, tenemos dos subclases: "Cuadrado" y "Rectangulo".  

Según el Principio de Sustitución de Liskov, podemos pasar una instancia de la clase base o cualquiera de sus subclases como argumento a la función "imprimirArea". Esto significa que podemos tratar un cuadrado o un rectángulo como una forma genérica sin afectar el resultado.  

En el caso del cuadrado, hemos sobreescrito los métodos "setAncho" y "setAlto" para asegurarnos de que el ancho y el alto sean siempre iguales, ya que en un cuadrado ambos lados deben tener la misma longitud.  

### [MUST] Principio de Segregación de Interfaces

El Principio de Segregación de Interfaces (ISP por sus siglas en inglés) establece que una clase no debe depender de interfaces que no utiliza. En otras palabras, es preferible tener varias interfaces específicas que una interfaz grande y genérica.

#### Ejemplo

Imaginemos que tenemos una interfaz llamada `EmailServiceInterface` que contiene métodos como `sendEmail()`, `receiveEmail()`, `deleteEmail()`, etc. Además, tenemos dos clases que implementan esta interfaz: `GmailService` y `OutlookService`.

```php
interface EmailServiceInterface {
    public function sendEmail($to, $subject, $message);
    public function receiveEmail();
    public function deleteEmail($email);
}

class GmailService implements EmailServiceInterface {
    public function sendEmail($to, $subject, $message) {
        // Implementación específica para Gmail
    }

    public function receiveEmail() {
        // Implementación específica para Gmail
    }

    public function deleteEmail($email) {
        // Implementación específica para Gmail
    }
}

class OutlookService implements EmailServiceInterface {
    public function sendEmail($to, $subject, $message) {
        // Implementación específica para Outlook
    }

    public function receiveEmail() {
        // Implementación específica para Outlook
    }

    public function deleteEmail($email) {
        // Implementación específica para Outlook
    }
}
```

Hasta aquí, todo parece estar bien según el principio de segregación de interfaces. Sin embargo, imaginemos que más tarde necesitamos agregar una nueva funcionalidad para adjuntar archivos a los correos electrónicos. Siguiendo el ISP, deberíamos crear una nueva interfaz específica para esta funcionalidad, en lugar de modificar la interfaz existente.

```php
interface AttachmentsInterface {
    public function attachFile($file);
}

class GmailService implements EmailServiceInterface, AttachmentsInterface {
    public function sendEmail($to, $subject, $message) {
        // Implementación específica para Gmail
    }

    public function receiveEmail() {
        // Implementación específica para Gmail
    }

    public function deleteEmail($email) {
        // Implementación específica para Gmail
    }
    
    public function attachFile($file) {
        // Implementación específica para Gmail
    }
}

class OutlookService implements EmailServiceInterface, AttachmentsInterface {
    public function sendEmail($to, $subject, $message) {
        // Implementación específica para Outlook
    }

    public function receiveEmail() {
        // Implementación específica para Outlook
    }

    public function deleteEmail($email) {
        // Implementación específica para Outlook
    }
    
    public function attachFile($file) {
        // Implementación específica para Outlook
    }
}
```

De esta manera, hemos aplicado el principio de segregación de interfaces al crear una nueva interfaz `AttachmentsInterface` específica para la funcionalidad de adjuntar archivos, evitando así modificar la interfaz `EmailServiceInterface` original.

### [MUST] Principio de Inversión de Dependencias

El Principio de Inversión de Dependencias establece que los módulos de alto nivel no deben depender de módulos de bajo nivel. Ambos deben depender de abstracciones. Se recomienda utilizar la inyección de dependencias y los contenedores de inversión de control para lograr una mayor flexibilidad y facilidad de mantenimiento.

#### Ejemplo

Imaginemos que estamos desarrollando una aplicación de comercio electrónico y tenemos una clase llamada ShoppingCart (Carrito de compras) que se encarga de manejar el proceso de compra de un cliente. Esta clase tiene una dependencia directa con la clase PaymentProcessor (Procesador de pagos), ya que necesita comunicarse con esta clase para procesar los pagos de los productos en el carrito.  

Sin embargo, según el principio de inversión de dependencia, las clases de alto nivel no deben depender de las clases de bajo nivel. En cambio, ambos niveles deben depender de abstracciones. En este caso, la clase ShoppingCart no debe depender directamente de la implementación concreta de PaymentProcessor, sino de una interfaz que defina la funcionalidad necesaria para procesar pagos.  

En PHP, podríamos tener una interfaz llamada PaymentProcessorInterface que declare los métodos necesarios para procesar pagos, como procesarPago() y cancelarPago(). La clase ShoppingCart aceptará una instancia de PaymentProcessorInterface en su constructor en lugar de una instancia concreta de PaymentProcessor.  

```php
interface PaymentProcessorInterface {
    public function procesarPago(float $monto): bool;
    public function cancelarPago(float $monto): bool;
}

class PaymentProcessor implements PaymentProcessorInterface {
    public function procesarPago(float $monto): bool {
        // Lógica para procesar el pago concreto
    }

    public function cancelarPago(float $monto): bool {
        // Lógica para cancelar el pago concreto
    }
}

class ShoppingCart {
    private $paymentProcessor;

    public function __construct(PaymentProcessorInterface $paymentProcessor) {
        $this->paymentProcessor = $paymentProcessor;
    }

    public function procesarCompra(float $monto) {
        // Lógica para procesar la compra
        $pagoExitoso = $this->paymentProcessor->procesarPago($monto);
        // Más lógica para completar la compra
    }
}
```

En este ejemplo, podemos ver que ShoppingCart depende de PaymentProcessorInterface en lugar de la implementación concreta de PaymentProcessor. Esto permite que podamos cambiar o agregar diferentes implementaciones de PaymentProcessor (por ejemplo, PayPalProcessor, StripeProcessor, etc.) sin afectar a ShoppingCart, ya que todas las implementaciones cumplen con la interfaz PaymentProcessorInterface.

Este enfoque nos permite tener un código más flexible, mantenible y fácilmente testeable, ya que podemos reemplazar las dependencias con mocks o stubs durante las pruebas unitarias, y también nos permite extender y modificar el sistema de manera más sencilla.


## Patrones ligados a Symfony

### Singleton

El patrón de diseño Singleton es un patrón de creación que se utiliza para garantizar que solo exista una única instancia de una clase en todo el programa. Esto es particularmente útil cuando se requiere un acceso global a un objeto, pero solo debe haber una sola instancia del mismo.  

La implementación básica del patrón Singleton consiste en una clase con un constructor privado, que evita que la clase pueda ser instanciada directamente. En su lugar, la clase proporciona un método estático para obtener la instancia única de la misma.

El patrón Singleton se utiliza principalmente cuando se necesita una única instancia compartida en todo el programa. Algunos casos de uso típicos incluyen la gestión de conexiones a bases de datos, la creación de logs o registros de eventos, y la gestión de configuraciones globales.

Es importante tener en cuenta que el patrón Singleton puede introducir ciertos desafíos, como problemas de concurrencia cuando se accede a la instancia desde múltiples hilos. Para abordar esto, se pueden utilizar técnicas como la sincronización o el uso de inicialización perezosa con doble bloqueo.

### Observer

El patrón de diseño Observer es un patrón de comportamiento que se utiliza para establecer una comunicación de tipo uno a muchos entre objetos, de manera que cuando un objeto cambia su estado, todos los objetos dependientes son notificados y actualizados automáticamente.

A continuación, te presentaré los elementos clave y su funcionamiento en el patrón Observer:  

1. Sujeto (Subject): es el objeto que tiene la información o estado que otros objetos desean observar. El sujeto mantiene una lista de observadores y proporciona métodos para que los observadores se registren, cancelen el registro y notifiquen cambios de estado.

2. Observador (Observer): es la interfaz o clase base que define los métodos que los observadores deben implementar para recibir notificaciones de cambios en el sujeto. Los observadores pueden ser múltiples y no tienen conocimiento entre sí.  

3. Observadores concretos (Concrete Observers): son las clases que implementan la interfaz de observador. Estas clases se registran en el sujeto y reciben notificaciones cuando el estado del sujeto cambia. Pueden acceder al sujeto para obtener información adicional si es necesario.  

4. Evento (Event): es la estructura de datos que se utiliza para transmitir los detalles del cambio de estado desde el sujeto a los observadores. Puede contener información específica sobre el cambio o simplemente notificar que ha ocurrido un cambio.  

Este patrón es útil en situaciones en las que se requiere una comunicación flexible y acoplada débilmente entre objetos. Al usar el patrón Observer, los objetos pueden recibir notificaciones en tiempo real sobre cambios en el estado de otros objetos sin acoplarse directamente.  

### Factory

El patrón de diseño Factory (o fábrica) es un patrón creacional que se utiliza para crear objetos de un tipo específico sin exponer la lógica de creación directamente al cliente. Básicamente, el patrón Factory encapsula la creación de objetos y proporciona una interfaz común para crear múltiples tipos de objetos. 

La idea principal detrás del patrón Factory es tener una clase abstracta o una interfaz que define un método para crear objetos. Luego, hay varias implementaciones concretas de esta interfaz, cada una de las cuales puede crear diferentes tipos de objetos. Esto permite la creación dinámica de objetos sin que el cliente tenga que conocer los detalles de cómo se crean.

Un ejemplo común del patrón Factory es la creación de diferentes tipos de objetos de una clase base o interfaz común. Imagina que tienes una interfaz llamada "Transporte" y varias implementaciones de esta interfaz, como "Coche", "Bicicleta" y "Avión". En lugar de que el cliente tenga que conocer los detalles de creación de cada tipo de transporte, el patrón Factory se encarga de ello.

El patrón Factory es útil cuando se necesita abstraer la lógica de creación de objetos y proporcionar una forma flexible de crear diferentes tipos de objetos. Además, también ayuda a mantener el principio de responsabilidad única al separar la creación de objetos de su uso. 

### Repository

El patrón de diseño Repository es un patrón arquitectónico utilizado en el desarrollo de software para separar la lógica de la aplicación de la forma en que los datos son almacenados y accedidos. Su objetivo principal es proporcionar una capa de abstracción entre la capa de negocio de la aplicación y la capa de acceso a datos.  
  
En términos simples, el patrón de diseño Repository permite centralizar todas las operaciones de persistencia de datos en un solo lugar, llamado repositorio. Este repositorio actúa como una abstracción de la fuente de datos subyacente, ya sea una base de datos, un servicio web, un archivo, etc.  

La idea detrás del patrón Repository es proporcionar una interfaz común para acceder a los datos y ocultar los detalles de implementación subyacentes. Esto significa que los componentes de la capa de negocio de la aplicación no necesitan preocuparse por cómo se almacenan o recuperan los datos, sino que simplemente interactúan con el repositorio a través de una interfaz bien definida.

### Dependency Injection

El patrón de diseño Dependency Injection (DI), también conocido como inyección de dependencias, es un patrón que se utiliza para gestionar las dependencias entre objetos en una aplicación. En lugar de que un objeto cree directamente sus dependencias, se le suministran desde el exterior, lo que permite una mayor flexibilidad y facilita la prueba y el mantenimiento del código.

La idea principal detrás de Dependency Injection es separar la creación de objetos de su utilización. En lugar de que un objeto cree o busque sus dependencias, se le pasan como parámetros en lugar de que las busque o las instancie por sí mismo. Esto promueve una mejor modularidad y desacoplamiento, ya que los objetos no están acoplados directamente a sus dependencias.

Hay tres formas comunes de aplicar Dependency Injection: Constructor Injection, Setter Injection y Interface Injection.

1. Constructor Injection: En este enfoque, las dependencias se pasan al constructor de la clase. El objeto dependiente declara sus dependencias a través de los parámetros de su constructor, y luego se usa el constructor para pasar las instancias de las dependencias requeridas. Este enfoque garantiza que las dependencias estén disponibles cuando se crea el objeto y que sean inmutables una vez establecidas.  

2. Setter Injection: En este enfoque, las dependencias se pasan a través de los métodos setter del objeto. El objeto dependiente declara los métodos setter correspondientes para cada una de sus dependencias, y luego se utilizan estos métodos para inyectar las instancias de las dependencias requeridas. Este enfoque permite la flexibilidad de cambiar las dependencias en cualquier momento durante el ciclo de vida del objeto.  

3. Interface Injection: En este enfoque, las dependencias se pasan a través de una interfaz común que el objeto dependiente implementa. El objeto dependiente declara un método en la interfaz para recibir las dependencias requeridas, y luego se utiliza este método para inyectar las instancias de las dependencias. Este enfoque permite una mayor flexibilidad en la configuración de las dependencias, ya que se pueden proporcionar diferentes implementaciones de la interfaz.  

La inyección de dependencias tiene varios beneficios. En primer lugar, facilita la prueba unitaria, ya que se pueden proporcionar fácilmente dependencias simuladas o falsas durante las pruebas. Además, promueve la reutilización de código, ya que las dependencias pueden ser compartidas entre varios objetos. También mejora la legibilidad y mantenibilidad del código, ya que las dependencias se declaran explícitamente.


## Otros Patrones de Diseño

### [MUST] Speaking Code Principle (SCP)

El patrón de diseño "Speaking Code Principle", que en español podríamos llamar el "Principio del Código Expresivo" se centra en escribir código de manera clara y comprensible, de modo que pueda "hablar" por sí mismo, haciéndolo fácil de entender y mantener.

El objetivo principal del Speaking Code Principle es mejorar la legibilidad y mantenibilidad del código fuente. A medida que los proyectos de software crecen en tamaño y complejidad, se vuelve esencial que el código sea fácil de entender tanto para el desarrollador original como para aquellos que trabajen en él en el futuro.

Aquí hay algunas pautas clave para seguir el Speaking Code Principle:  

1. Nombres descriptivos de variables y funciones: Es fundamental utilizar nombres que reflejen claramente el propósito y la función de una variable o función. Evita nombres genéricos como "var1" o "func1". En su lugar, utiliza nombres descriptivos como "contadorDeUsuarios" o "calcularPromedio".  

2. Comentarios claros y concisos: Los comentarios deben ser utilizados para explicar partes del código que no son obvias o que pueden resultar confusas para otros desarrolladores. Sin embargo, no abuses de los comentarios; solo deben usarse cuando sea necesario y deben ser breves y al punto.

3. Estructura de código bien organizada: Organiza tu código de manera lógica y coherente. Utiliza espacios en blanco y sangrías adecuadas para mejorar la legibilidad. Divide el código en bloques lógicos, utilizando funciones y clases para agrupar funcionalidades relacionadas.

4. Evita la duplicación de código: La duplicación de código no solo es ineficiente, sino que también dificulta la comprensión y el mantenimiento. En su lugar, utiliza funciones o métodos reutilizables para evitar redundancias.

5. Orientación a objetos: Aplica los principios de la programación orientada a objetos (POO) para estructurar tu código de manera más clara. Utiliza clases, objetos, herencia y polimorfismo de manera adecuada para organizar y representar las diferentes entidades y comportamientos en tu aplicación.  

6. Pruebas unitarias: Incluye pruebas unitarias para validar el comportamiento esperado de tu código. Las pruebas unitarias no solo mejoran la calidad del código, sino que también sirven como documentación viva de cómo se supone que deben funcionar las diferentes partes del sistema.  

7. Refactorización: La refactorización es el proceso de mejorar el código existente sin cambiar su comportamiento. Aplica técnicas de refactorización regularmente para eliminar código duplicado, mejorar la estructura y aumentar la legibilidad.  

Siguiendo estas pautas, el Speaking Code Principle nos ayuda a mantener un código fuente claro, fácil de leer y mantener. Esto facilita la colaboración en el desarrollo de software y reduce los errores que pueden ocurrir debido a la falta de comprensión del código. Al utilizar este patrón de diseño, promovemos la calidad del software y la productividad del equipo de desarrollo.

### [MUST] Keep It Simple, Stupid (KISS)

El patrón de diseño KISS es un principio fundamental en el desarrollo de software que aboga por la simplicidad en el diseño y la implementación de sistemas. Su objetivo principal es evitar la complejidad innecesaria y mantener las soluciones lo más simples posible.  
  
La idea detrás de KISS es que los sistemas simples son más fáciles de entender, mantener y mejorar. Al mantener las cosas simples, reducimos la posibilidad de errores y facilitamos la colaboración entre equipos. Además, los sistemas simples tienden a ser más eficientes en términos de rendimiento y recursos.

Aquí hay algunos principios clave asociados con el patrón KISS:  

1. Eliminar la complejidad innecesaria: Esto implica evitar características y funcionalidades que no son esenciales para el sistema. Si algo no es absolutamente necesario, es mejor no incluirlo.  

2. Mantener la claridad y la legibilidad: El código debe ser fácil de leer y entender para cualquier desarrollador. Esto implica utilizar nombres de variables descriptivos, estructuras de código ordenadas y comentarios claros.

3. No reinventar la rueda: En lugar de construir algo desde cero, es mejor utilizar bibliotecas, frameworks y soluciones existentes que ya han sido probados y se sabe que funcionan correctamente. Esto reduce la complejidad y el riesgo de errores.  

4. Evitar soluciones demasiado generales: A veces, los desarrolladores tienden a construir sistemas excesivamente flexibles y complejos que pueden manejar cualquier caso de uso posible. Esto puede llevar a un código complicado y difícil de mantener. Es mejor construir soluciones simples y específicas para los problemas actuales.

5. Iterar y refactorizar: A medida que avanzamos en el desarrollo de software, es esencial iterar y refactorizar el código para mantenerlo simple y limpio. A medida que aprendemos más sobre el sistema y sus necesidades, podemos eliminar la complejidad innecesaria y mejorar continuamente la simplicidad del diseño.

### [MUST] Don't Repeat Yourself (DRY)

El principio DRY, también conocido como "No te repitas" en español, es un concepto fundamental en la programación que promueve la reutilización de código y la eliminación de duplicación. Básicamente, significa que cada pieza de conocimiento en un sistema debe tener una representación única y clara en todo el código fuente.

El objetivo principal de seguir este principio es reducir la duplicación de código y evitar la dispersión de la lógica de negocio en diferentes partes del sistema. Al evitar la repetición, se puede mejorar la legibilidad, mantenibilidad y escalabilidad del software.

Existen diferentes técnicas y enfoques para aplicar el principio DRY en el desarrollo de software. Algunas de ellas incluyen:

1. Abstracción: Identificar partes comunes o similares del código y extraerlas en funciones, clases o módulos reutilizables. De esta manera, en lugar de repetir el mismo código en múltiples lugares, simplemente se llama a la función o se utiliza la clase/módulo correspondiente.

2. Separación de responsabilidades: Asegurarse de que cada componente del sistema tenga una única responsabilidad y no esté involucrado en múltiples tareas. Esto ayuda a evitar la duplicación de lógica y facilita la comprensión y el mantenimiento del código.

3. Uso de bibliotecas y frameworks: Aprovechar las bibliotecas y frameworks existentes que ofrecen funcionalidades comunes y probadas. En lugar de implementar esas funcionalidades desde cero, podemos utilizar las soluciones existentes, ahorrando tiempo y evitando errores.

4. Automatización: Utilizar herramientas y scripts para automatizar tareas repetitivas, como pruebas unitarias, construcción y despliegue. Esto no solo ahorra tiempo, sino que también minimiza los errores humanos y asegura la coherencia en el proceso de desarrollo.

Es importante tener en cuenta que aplicar el principio DRY no significa eliminar toda la repetición de código a cualquier costo. A veces, puede haber situaciones donde la repetición es necesaria debido a diferencias específicas de contexto. En esos casos, es importante encontrar un equilibrio y no abusar de la abstracción excesiva.

### [SHOULD] You Ain't Gonna Need It! (YAGNI)

El patrón de diseño YAGNI es un principio general en el desarrollo de software que se centra en evitar la implementación de funcionalidades o características que no son necesarias en el momento actual. La idea detrás del patrón YAGNI es mantener el código simple y evitar el desperdicio de tiempo y recursos en la creación de funcionalidades innecesarias que podrían no ser utilizadas.

En lugar de anticiparse a posibles futuros requerimientos o casos de uso, el patrón YAGNI nos insta a enfocarnos en las necesidades actuales del proyecto. Esto implica escribir código que cumpla con los requisitos actuales sin agregar funcionalidades adicionales que podrían no ser necesarias.

Una de las principales razones para aplicar el patrón YAGNI es mantener la simplicidad del código. Al evitar la implementación de funcionalidades innecesarias, podemos reducir la complejidad del sistema y facilitar su mantenimiento. Además, el principio YAGNI nos ayuda a evitar el sobre-diseño y la sobreingeniería, que pueden llevar a la creación de código complicado e innecesario.

Es importante tener en cuenta que el patrón YAGNI no significa que debamos ignorar por completo los posibles futuros requerimientos. En su lugar, nos insta a esperar hasta que realmente necesitemos una funcionalidad antes de implementarla. Esto ayuda a evitar gastar tiempo y recursos en características que pueden cambiar o incluso no ser utilizadas en absoluto.

### [SHOULD] Law Of Demeter

La Ley de Demeter, también conocida como el principio de menor conocimiento, es un patrón de diseño que se enfoca en minimizar las dependencias entre los objetos. Fue formulado por el ingeniero de software estadounidense, Karl Lieberherr, en honor al principio del mismo nombre en el Derecho.  

El objetivo principal de la Ley de Demeter es promover el acoplamiento débil y la alta cohesión en un sistema de software. Esto se logra siguiendo una regla sencilla: un objeto solo debe interactuar directamente con sus vecinos inmediatos y no con objetos más lejanos.  

En términos prácticos, esto significa que un objeto solo debe llamar a métodos de otros objetos que sean:  

1. Métodos propios del objeto: El objeto puede llamar a sus propios métodos sin restricciones.

2. Métodos de parámetros: El objeto puede llamar a los métodos de los objetos que se le han pasado como parámetros en sus propios métodos.

3. Métodos de variables de instancia: El objeto puede llamar a los métodos de sus variables de instancia.

4. Métodos de objetos creados dentro del método: El objeto puede llamar a los métodos de los objetos creados internamente en sus propios métodos.

Sin embargo, un objeto no debe acceder a los métodos de otros objetos a través de métodos que devuelve o retorna, ni debe acceder a los métodos de los objetos a los que se accede a través de métodos de otros objetos. Esto ayuda a reducir la dependencia de los objetos y mejora la flexibilidad y mantenibilidad del sistema.  

La Ley de Demeter promueve la encapsulación y el ocultamiento de información. Al limitar las interacciones directas entre objetos, se reduce la cantidad de código que necesita ser modificado cuando se realizan cambios en un objeto específico. Además, facilita la reutilización de código, ya que los objetos se vuelven más independientes y pueden ser utilizados en diferentes contextos sin problemas.

