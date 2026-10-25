# Práctica 4. Gestión Avanzada de Ramas y Resolución de Conflictos

## 1. Introducción

### 1.1 Crear el directorio del proyecto

```bash
mkdir webnova
cd webnova
```

![Captura 1 - Creación del directorio](Imagenes/1.png)

### 1.2 Configurar la rama predeterminada e inicializar el repositorio

```bash
git config --global init.defaultBranch main
git init
```

![Captura 2 - git init](Imagenes/1.png)

### 1.3 Crear el archivo base `index.html`

```html
<h1>Bienvenido a WebNova</h1>
<p>Versión inicial del proyecto</p>
```

![Captura 3 - index.html inicial](Imagenes/1.png)

### 1.4 Primer commit (C1)

```bash
git add .
git commit -m "C1: Versión inicial de WebNova"
```

![Captura 4 - Commit C1](Imagenes/1.png)

---

## 2. Desarrollo del proyecto

### 2.1 Creación de las ramas de características

```bash
git branch cabecera
git branch contenido
git branch pie
```

Comprobación de que las ramas existen y de que seguimos en `main`:

```bash
git branch
```

![Captura 5 - Listado de ramas](Imagenes/1.png)

### 2.2 Desarrollo en la rama `cabecera`

```bash
git switch cabecera
```

Contenido de `header.html`:

```html
<header>
    <h2>WebNova - Innovación en la web</h2>
    <nav>
        <a href="#">Inicio</a> | <a href="#">Servicios</a> | <a href="#">Contacto</a>
    </nav>
</header>
```

```bash
git add header.html
git commit -m "C2: Añadido encabezado con navegación"
```

![Captura 6 - Rama cabecera y commit C2](Imagenes/1.png)

### 2.3 Desarrollo en la rama `contenido`

```bash
git switch contenido
```

Contenido de `content.html`:

```html
<main>
    <h3>Nuestros servicios</h3>
    <p>Ofrecemos soluciones de desarrollo web a medida.</p>
</main>
```

```bash
git add content.html
git commit -m "C3: Creado contenido principal"
```

![Captura 7 - Rama contenido y commit C3](Imagenes/1.png)

### 2.4 Desarrollo en la rama `pie`

```bash
git switch pie
```

Contenido de `footer.html`:

```html
<footer>
    <p>&copy; 2026 WebNova. Todos los derechos reservados.</p>
</footer>
```

```bash
git add footer.html
git commit -m "C4: Añadido pie de página"
```

![Captura 8 - Rama pie y commit C4](Imagenes/1.png)

---

### 2.5 Volver a `main` y fusionar las ramas

```bash
git switch main
git merge cabecera
git merge contenido
git merge pie
```

Tipo de fusión realizada por Git en cada caso:

| Rama | Tipo de fusión | Motivo |
|------|----------------|--------|
| `cabecera` | **Fast-Forward** | `main` no había avanzado desde C1; Git solo mueve el puntero. |
| `contenido` | **3-Way Merge (ort)** | `main` ya contiene C2 y `contenido` parte de C1: las historias divergen. |
| `pie` | **3-Way Merge (ort)** | Mismo caso: `main` ya tiene cambios que `pie` no tiene. |

![Captura 9 - Fusiones sin conflicto](Imagenes/1.png)

### 2.6 Unificar el código en `index.html`

Se copia el contenido de `header.html`, `content.html` y `footer.html` dentro de `index.html`:

```html
<h1>Bienvenido a WebNova</h1>
<p>Versión inicial del proyecto</p>

<header>
    <h2>WebNova - Innovación en la web</h2>
    <nav>
        <a href="#">Inicio</a> | <a href="#">Servicios</a> | <a href="#">Contacto</a>
    </nav>
</header>

<main>
    <h3>Nuestros servicios</h3>
    <p>Ofrecemos soluciones de desarrollo web a medida.</p>
</main>

<footer>
    <p>&copy; 2026 WebNova. Todos los derechos reservados.</p>
</footer>
```

![Captura 10 - index.html consolidado](Imagenes/1.png)

### 2.7 Commit de consolidación (C5)

```bash
git commit -a -m "C5: Integrados cabecera, contenido y pie en index.html"
```

![Captura 11 - Commit C5](Imagenes/1.png)

### 2.8 Limpieza: eliminar las ramas de desarrollo

```bash
git branch -d cabecera contenido pie
git branch
```

![Captura 12 - Ramas eliminadas](Imagenes/1.png)

---

## PARTE 3: Provocando y resolviendo un conflicto

### 3.1 La rama de rediseño

```bash
git switch -c rediseño
```

Se modifica la etiqueta `<h1>` de `index.html`:

```html
<h1>WebNova - Sitio oficial (Rediseño 2026)</h1>
```

```bash
git commit -a -m "C6: Rediseño del título principal"
```

![Captura 13 - Rama rediseño y commit C6](Imagenes/1.png)

### 3.2 Trabajo divergente en `main`

```bash
git switch main
```

![Captura 14 - Cambio a main](Imagenes/1.png)

Se cambia el `<h1>` en `index.html` a:

```html
<h1>WebNova - Portal principal corporativo</h1>
```

```bash
git commit -a -m "C7: Cambio de título corporativo en main"
```

![Captura 15 - Commit C7 en main](Imagenes/1.png)

### 3.3 La fusión y el conflicto

```bash
git merge rediseño
```

Git pausa la fusión y avisa de un conflicto de contenido en `index.html`.

![Captura 16 - Mensaje de conflicto](Imagenes/1.png)

### 3.4 Resolución del conflicto

**a) Estado del archivo con las marcas de conflicto:**

```html
<<<<<<< HEAD
<h1>WebNova - Portal principal corporativo</h1>
=======
<h1>WebNova - Sitio oficial (Rediseño 2026)</h1>
>>>>>>> rediseño
```

![Captura 17 - Marcas de conflicto](Imagenes/1.png)

**b) Edición manual:** se eliminan las marcas de Git y se fusionan ambas ideas:

```html
<h1>WebNova - Portal principal (Rediseño 2026)</h1>
```

![Captura 18 - Archivo resuelto](Imagenes/1.png)

**c) Finalizar la fusión:**

```bash
git add index.html
git commit -m "C8: Conflicto resuelto entre main y rediseño en el H1"
```

![Captura 19 - Commit de resolución C8](Imagenes/1.png)

---

## PARTE 4: Visualización del historial

```bash
git log --oneline --graph --all
```

![Captura 20 - git log --graph](Imagenes/1.png)

---

## 4. Reflexión teórica

### 4.1 ¿Por qué ocurrió el conflicto en la PARTE 3 y por qué no ocurrió en la PARTE 2?

En la **PARTE 2** no hubo conflicto porque cada rama modificó **un archivo distinto** (`header.html`, `content.html` y `footer.html`). Al fusionar, Git pudo combinar los cambios automáticamente, ya que ninguna rama tocaba las mismas líneas de un mismo archivo. Además, la primera fusión (`cabecera`) fue un *Fast-Forward*, que ni siquiera requiere combinar contenido.

En la **PARTE 3** el conflicto apareció porque las dos ramas (`main` y `rediseño`) **modificaron la misma línea (`<h1>`) del mismo archivo (`index.html`)** a partir de un ancestro común, con valores distintos. Git no puede decidir automáticamente cuál de las dos versiones es la correcta, así que detiene la fusión, marca el conflicto en el archivo y delega la decisión en el desarrollador.

### 4.2 Al ejecutar `git switch main` en la PARTE 3.2, ¿qué ocurrió con los archivos de tu directorio de trabajo?

Git **actualizó el directorio de trabajo para reflejar el último commit de la rama `main`**. Como `index.html` en `rediseño` tenía el `<h1>` modificado (`WebNova - Sitio oficial (Rediseño 2026)`), al cambiar a `main` el archivo volvió automáticamente a su versión anterior, con el título original de `main`. Los cambios de `rediseño` no se pierden: quedan guardados en su commit (C6), y Git solo reescribe el contenido del directorio para que coincida con la rama activa.

---

## 5. Conclusiones

Con esta práctica se han trabajado la creación y navegación de ramas con `git switch`, las fusiones Fast-Forward y a tres bandas, la identificación y resolución manual de un conflicto de fusión y la visualización del historial con `git log --oneline --graph --all`, manteniendo un historial estructurado y limpio.
