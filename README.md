# Práctica 4. Gestión Avanzada de Ramas y Resolución de Conflictos

## 1. Introducción

### 1.1 Crear el directorio del proyecto

![Captura 1 - Creación del directorio](Imagenes/1.png)

### 1.2 Configurar la rama predeterminada e inicializar el repositorio

![Captura 2 - git init](Imagenes/2.png)

### 1.3 Crear el archivo base `index.html`

![Captura 3 - index.html inicial](Imagenes/3.png)

### 1.4 Primer commit (C1)

![Captura 4 - Commit C1](Imagenes/4.png)

---

## 2. Desarrollo del proyecto

### 2.1 Creación de las ramas de características

Comprobación de que las ramas existen y de que seguimos en `main`:

![Captura 5 - Listado de ramas](Imagenes/5.png)

### 2.2 Desarrollo en la rama `cabecera`

![Captura 6 - Rama cabecera y commit C2](Imagenes/6.png)

![Captura 7 - Rama cabecera y commit C2](Imagenes/7.png)

![Captura 8 - Rama cabecera y commit C2](Imagenes/8.png)

### 2.3 Desarrollo en la rama `contenido`

![Captura 9 - Rama contenido y commit C3](Imagenes/9.png)

![Captura 10 - Rama cabecera y commit C2](Imagenes/10.png)

![Captura 11 - Rama cabecera y commit C2](Imagenes/11.png)

### 2.4 Desarrollo en la rama `pie`

![Captura 12 - Rama cabecera y commit C2](Imagenes/12.png)

![Captura 13 - Rama cabecera y commit C2](Imagenes/13.png)

---

### 2.5 Volver a `main` y fusionar las ramas

![Captura 14 - Fusiones sin conflicto](Imagenes/14.png)

![Captura 15 - Rama cabecera y commit C2](Imagenes/15.png)

### 2.6 Unificar el código en `index.html`

![Captura 16 - index.html consolidado](Imagenes/16.png)

### 2.7 Commit de consolidación (C5)

![Captura 17 - Commit C5](Imagenes/17.png)

### 2.8 Limpieza: eliminar las ramas de desarrollo

![Captura 18 - Ramas eliminadas](Imagenes/18.png)

---

## PARTE 3: Provocando y resolviendo un conflicto

### 3.1 La rama de rediseño

![Captura 19 - Rama rediseño y commit C6](Imagenes/19.png)

![Captura 20 - Rama rediseño y commit C6](Imagenes/20.png)

![Captura 21 - Rama rediseño y commit C6](Imagenes/21.png)

### 3.2 Trabajo divergente en `main`

![Captura 22 - Cambio a main](Imagenes/22.png)

![Captura 23 - Commit C7 en main](Imagenes/23.png)

![Captura 24 - Commit C7 en main](Imagenes/24.png)

### 3.3 La fusión y el conflicto

![Captura 25 - Mensaje de conflicto](Imagenes/25.png)

### 3.4 Resolución del conflicto

**Estado del archivo con las marcas de conflicto:**

![Captura 26 - Marcas de conflicto](Imagenes/26.png)


**Finalizar la fusión:**

![Captura 27 - Commit de resolución C8](Imagenes/27.png)

---

## PARTE 4: Visualización del historial

![Captura 28 - git log --graph](Imagenes/28.png)

---

## 4. Reflexión teórica

### 4.1 ¿Por qué ocurrió el conflicto en la PARTE 3 y por qué no ocurrió en la PARTE 2?

En la PARTE 2 no hubo conflicto porque cada rama modificó un archivo distinto header.html, content.html y footer.html. Al fusionar, Git pudo combinar los cambios automáticamente, ya que ninguna rama tocaba las mismas 
líneas de un mismo archivo. Además, que ni siquiera requiere combinar contenido.
En la PARTE 3 el conflicto apareció porque las dos ramas main y rediseño modificaron la misma línea <h1> del mismo archivo index.html a partir de un ancestro común, con valores distintos. Git no puede decidir 
automáticamente cuál de las dos versiones es la correcta, así que detiene la fusión, marca el conflicto en el archivo y delega la decisión en el desarrollador.

### 4.2 Al ejecutar git switch main en la PARTE 3.2, ¿qué ocurrió con los archivos de tu directorio de trabajo?

Git actualizó el directorio de trabajo para reflejar el último commit de la rama main. Como index.html en rediseño tenía el <h1> modificado (WebNova - Sitio oficial (Rediseño 2026)), al cambiar a main el archivo volvió 
automáticamente a su versión anterior, con el título original de main. Los cambios de rediseño no se pierden: quedan guardados en su commit (C6), y Git solo reescribe el contenido del directorio para que coincida con la 
rama activa.

---

## 5. Conclusiones

Con esta práctica se ha trabajado la creación y navegación de ramas con git switch, la identificación y resolución manual de un conflicto de fusión y la visualización del historial con git log --oneline --graph --all, 
manteniendo un historial estructurado y limpio.
