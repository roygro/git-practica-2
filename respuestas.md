# Respuestas - Práctica 2: Taller Git

---

## Pregunta 1

### ¿Qué sucede cuando hacemos un `git add`?

**Respuesta:**
El archivo pasa del directorio de trabajo al **área de preparación (staging area)**. Git registra el estado actual de ese archivo y lo marca para incluirse en el próximo commit. El repositorio local todavía no cambia; simplemente le estamos indicando a Git qué cambios queremos guardar en el siguiente paso.

---

## Pregunta 2

### ¿Qué sucede cuando hacemos un `git commit`? ¿Dónde está ese commit?

**Respuesta:**
Git toma todos los archivos que estaban en el staging area y los guarda de forma permanente en el **historial del repositorio local** (dentro de la carpeta oculta `.git`). Ese commit vive únicamente en nuestra máquina. Contiene un identificador único (hash SHA-1), el mensaje que escribimos, el nombre del autor y la fecha.

---

## Pregunta 3

### ¿Por qué al hacer `git commit` todavía no está disponible ese commit en el repositorio remoto?

**Respuesta:**
Porque `git commit` solo guarda los cambios de forma **local**. Git es un sistema de control de versiones distribuido, lo que significa que el repositorio de nuestra computadora y el repositorio remoto en GitHub son independientes entre sí. Ningún comando ha enviado esos cambios a internet todavía; la sincronización no es automática.

---

## Pregunta 4

### ¿Qué hay que hacer para que veamos este commit en nuestro repositorio remoto de GitHub?

**Respuesta:**
Hay que ejecutar el comando:

```bash
git push origin <nombre-de-la-rama>
```

Este comando "empuja" los commits del repositorio local hacia el repositorio remoto en GitHub. Solo después de ejecutarlo el commit es visible en la plataforma y para otros colaboradores.

---

## Pregunta 5

### ¿Qué diferencia hay entre hacer un fork o crear una nueva rama?

**Respuesta:**

|                              | Fork                                                                         | Nueva rama                                                        |
| ---------------------------- | ---------------------------------------------------------------------------- | ----------------------------------------------------------------- |
| **Qué es**                   | Una copia completa del repositorio en nuestra propia cuenta de GitHub        | Una línea paralela de desarrollo dentro del mismo repositorio     |
| **Para qué sirve**           | Contribuir a proyectos ajenos sin tener permisos de escritura en el original | Desarrollar features o correcciones sin afectar la rama principal |
| **Relación con el original** | Repositorio separado; se puede proponer cambios mediante un Pull Request     | Mismo repositorio y misma historia base                           |
| **Uso típico**               | Proyectos de código abierto o colaboración externa                           | Trabajo en equipo dentro de un mismo proyecto                     |

En resumen: un **fork** es una copia del repositorio completo en otra cuenta, mientras que una **rama** es una bifurcación del historial dentro del mismo repositorio.

---

## Pregunta 6

### ¿Qué comando se utiliza para crear una nueva rama sin cambiarte a ella?

**Respuesta:**

```bash
git branch <nombre-de-la-rama>
```

Este comando crea la rama pero nos mantiene en la rama actual. Si quisiéramos además cambiarnos a ella, usaríamos `git checkout -b <nombre>` o `git switch -c <nombre>`.

---

## Pregunta 7

### ¿Cuál es la diferencia entre los comandos `git switch` y `git checkout` al trabajar con ramas?

**Respuesta:**
Ambos permiten cambiar de rama, pero:

- `git checkout` es el comando **clásico y multipropósito**: sirve para cambiar de rama, crear ramas, restaurar archivos, y más. Su uso múltiple puede generar confusión.
- `git switch` es un comando **más moderno y específico** (introducido en Git 2.23) que solo sirve para cambiar o crear ramas, haciendo el flujo más claro y legible.

Ejemplos equivalentes:

```bash
git checkout develop       →   git switch develop
git checkout -b develop    →   git switch -c develop
```

Para proyectos nuevos se recomienda usar `git switch` por ser más intuitivo.

---

## Pregunta 8

### ¿Qué es una rama por defecto (como `main` o `master`) y por qué es importante?

**Respuesta:**
Es la rama principal del repositorio que se crea automáticamente al inicializar el proyecto. Históricamente se llamaba `master`; GitHub adoptó `main` como nombre estándar desde 2020.

Su importancia radica en que representa el **código estable y funcional** del proyecto. Es la versión que se considera "oficial" o lista para producción. Todo el flujo de trabajo (ramas de features, correcciones, etc.) gira en torno a ella: el trabajo se desarrolla en ramas secundarias y solo se fusiona a `main` cuando está revisado y aprobado.

---

## Pregunta 9

### ¿Qué comando te permite ver la lista de todas las ramas locales de tu repositorio?

**Respuesta:**

```bash
git branch
```

La rama en la que nos encontramos actualmente aparece marcada con un asterisco `*`. Si también queremos ver las ramas remotas, usamos:

```bash
git branch -a
```

---

## Pregunta 10

### En el contexto de Git, explica con tus propias palabras qué es una rama (branch) y cuál es su beneficio principal al trabajar en un proyecto de software.

**Respuesta:**
Una rama es como una **copia paralela del proyecto** que parte de un punto específico del historial. Puedo hacer cambios en esa copia sin tocar el código principal; si todo sale bien, los fusiono de vuelta; si algo falla, simplemente descarto la rama sin haber dañado nada.

Su beneficio principal es permitir que **varias personas trabajen simultáneamente** en distintas funcionalidades o correcciones sin interferirse entre sí. Cada quien trabaja en su propia rama y el código estable permanece intacto en `main` hasta que los cambios estén listos y revisados.

---

## Pregunta 11

### ¿Qué ha pasado con el contenido de la carpeta `practica-taller-git`? ¿Por qué no la podemos ver en nuestro repositorio remoto de GitHub?

**Respuesta:**
La carpeta `practica-taller-git` es un repositorio Git **separado e independiente** que inicializamos localmente con `git init`. Nunca lo conectamos a ningún repositorio remoto ni hicimos `git push` desde esa carpeta.

El repositorio que subimos a GitHub (`git-practica-2`) es el que obtuvimos mediante el **fork**, que es un proyecto distinto. La carpeta `practica-taller-git` solo existe en nuestra computadora local y no tiene ningún remoto configurado, por lo que GitHub no tiene conocimiento de su existencia.

Para que apareciera en GitHub habría que:

1. Crear un nuevo repositorio en GitHub.
2. Vincularlo como remoto: `git remote add origin <url>`.
3. Subir los cambios: `git push -u origin main`.
