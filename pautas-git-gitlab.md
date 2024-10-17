# Manual de Pautas para el Trabajo Coordinado usando Git y Gitlab

## Introducción
Este manual tiene como objetivo establecer un conjunto de pautas y estándares para asegurar un trabajo coordinado y eficiente entre los desarrolladores de nuestro equipo utilizando Git y Gitlab. Se abordarán cuestiones relativas a la generación de commits, nombres de ramas, forks personales, merge requests y buenas prácticas en Git.

## 1. Estándares para Generar Commits

### 1.1. Formato del Mensaje del Commit
Cada commit debe seguir el siguiente formato para asegurar claridad y trazabilidad:

**Título del Commit:**
- Debe ser breve y descriptivo (máximo 50 caracteres).
- Comenzar con un verbo en infinitivo (Ej. "Agregar", "Corregir", "Actualizar").
- Incluir la referencia de la tarjeta en el título usando el formato #<número-de-la-tarjeta>. Ejemplo: Agregar funcionalidad de login #123.

**Descripción del Commit:**
- Proveer una descripción detallada y clara del cambio realizado.
- Incluir la relación del commit con la tarjeta o tarea específica.
- Describir cualquier impacto relevante en otras partes del proyecto.

**Ejemplo de Mensaje de Commit:**

Agregar funcionalidad de login #123

- Implementada la lógica de autenticación en el backend.
- Añadidos campos de validación en el frontend.
- Probado el flujo completo de inicio de sesión.
- Relacionado con la tarjeta #123 del tablero de tareas.
Copiar


### 1.2. Buenas Prácticas de Commits
- Cada commit debe tener un objetivo claro y realizar una única tarea.
- Realizar commits frecuentemente para evitar grandes cambios en una sola vez.
- Evitar commits con mensajes genéricos como "Arreglos varios" o "Cambios menores".

## 2. Nombres de las Ramas

### 2.1. Estándar para Nombres de Ramas
Las ramas deben ser nombradas de manera consistente para facilitar su identificación y manejo:

**Formato:**

<tipo>/<número-de-la-tarjeta>-<descripción-corta>
Copiar


**Tipos de Ramas:**
- feature: Nueva funcionalidad.
- bugfix: Corrección de errores.
- hotfix: Cambios urgentes en producción.
- refactor: Refactorización de código.
- test: Implementación o actualización de tests.

**Ejemplo de Nombre de Rama:**

feature/123-agregar-login
bugfix/456-corregir-bug-navbar
Copiar


## 3. Uso de Forks Personales

### 3.1. Subida de Cambios
- Cada desarrollador debe trabajar en su propio fork del repositorio principal.
- Los cambios deben ser empujados a las ramas correspondientes en el fork personal.
- Realizar merge requests desde el fork personal al repositorio principal.

## 4. Creación de Merge Requests

### 4.1. Requisitos para Merge Requests
- Cada merge request debe estar asociado a una sola rama con cambios específicos.
- El título del merge request debe seguir el mismo formato que el título de un commit.
- Incluir una descripción detallada de los cambios, su propósito y cómo han sido probados.
- Enlazar la tarjeta o tarea correspondiente en la descripción del merge request.

### 4.2. Proceso de Revisión
- Asignar revisores específicos para cada merge request.
- Asegurar que los revisores sean notificados y que se realice una revisión minuciosa antes de aprobar.
- Implementar mecanismos para evitar aprobaciones automáticas sin revisión detallada.

## 5. Buenas Prácticas en Git

### 5.1. Uso de Branches
- Trabajar siempre en una rama separada para cada nueva funcionalidad, corrección de errores o mejora.
- La rama main (o master) debe permanecer estable y desplegable en todo momento.

### 5.2. Sincronización y Actualización
- Actualizar regularmente la rama principal (main o master) en el fork personal antes de iniciar nuevas tareas.
- Resolver conflictos localmente y probar antes de realizar un merge request.

### 5.3. Documentación y Comentarios
- Documentar el código adecuadamente dentro de los commits.
- Mantener comentarios claros y relevantes dentro del código base.

### 5.4. Testing y Validación
- Escribir tests para cualquier nueva funcionalidad o corrección de errores.
- Asegurarse de que todos los tests pasen antes de realizar un merge request.

## 6. Adicionales y Buenas Prácticas Relacionadas

### 6.1. Uso de Etiquetas y Milestones
- Utilizar etiquetas en Gitlab para categorizar y priorizar tareas.
- Definir milestones para agrupar tareas relacionadas a objetivos específicos.

### 6.2. Integración Continua
- Configurar pipelines de integración continua (CI) para automatizar pruebas y despliegues.
- Asegurar que todos los cambios pasen por un pipeline de CI antes de ser fusionados en la rama principal.

### 6.3. Comunicación y Colaboración
- Mantener una comunicación abierta y constante dentro del equipo.
- Utilizar herramientas de colaboración como Slack o Microsoft Teams para discusiones rápidas y aclaraciones.

## Conclusión
Seguir estas pautas ayudará a mantener un flujo de trabajo ordenado y eficiente, facilitando la colaboración y el control de versiones dentro del equipo. Asegurémonos de seguir estas prácticas y actualizarlas conforme sea necesario para mejorar continuamente nuestro proceso de desarrollo.