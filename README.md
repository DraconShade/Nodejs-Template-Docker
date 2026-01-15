![Docker](https://img.shields.io/badge/docker-ready-blue)
![Node.js](https://img.shields.io/badge/node.js-ready-green)
![npm](https://img.shields.io/badge/npm-ready-red)
![npx](https://img.shields.io/badge/npx-ready-black)

# Nodejs-Template-Docker 🐳

Plantilla para iniciar un entorno **Node.js** con **npx** y **npm** usando **Docker**.  
Este proyecto facilita levantar un contenedor Node.js listo para desarrollo y pruebas.

---

## 1. Requisitos

- [Docker](https://www.docker.com/get-started) instalado en tu máquina
- [Docker Compose](https://docs.docker.com/compose/install/) (v2+) disponible
- Conocimientos básicos de terminal / consola

---

## 2. Crear carpeta del proyecto

Crea la carpeta donde quieras levantar tu aplicación Node.js:

```bash
mkdir my-node-app
cd my-node-app
```
Dentro de esta carpeta estará tu `docker-compose.yml` y cualquier proyecto que crees con `npx`

---

## 3. Levantar el contenedor

Para iniciar el entorno Node.js en segundo plano:

```bash
docker compose up -d
```

`-d` indica que se ejecute en background (detached). Esto creará un contenedor llamado `nodejs` según tu `docker-compose.yml`.

---

## 4. Detener y limpiar el contenedor

Cuando quieras cerrar el entorno y eliminar volúmenes asociados:

```bash
docker compose down -v
```
`-v` elimina los volúmenes para limpiar datos temporales del contenedor. Útil si quieres reiniciar el proyecto desde cero.

---

## 5. Entrar al terminal del contenedor

Para ejecutar comandos dentro del contenedor Node.js:

```bash
docker exec -it nodejs sh
```
- `exec` inicia un nuevo shell en el contenedor existente.

- `-it` permite interacción (entrada de teclado + salida en pantalla).

- `sh` abre el shell de Alpine Linux (la base de la imagen `node:lts-alpine`).

```bash
npm install
npx create-expo-app@latest
node app.js
```
---

## 6. Reingresar a la misma consola si el terminal se cierra

Si tu terminal se cierra pero el contenedor sigue corriendo, puedes reconectarte al mismo proceso:

```bash
docker attach nodejs
```

Esto te devuelve al mismo shell interactivo donde estabas trabajando. Para salir sin detener el contenedor, usa: `Ctrl + P` seguido de `Ctrl + Q`.

---

## 7. Entrar a la consola temporalmente

Si solo quieres abrir una consola interactiva temporal y cerrar el contenedor al salir:

```bash
docker compose run --rm nodejs sh
```

- `run` crea un nuevo contenedor temporal.

- `--rm` elimina el contenedor automáticamente al cerrar el shell.
Útil para ejecutar comandos rápidos sin afectar el contenedor principal.

---

## 8. Flujo recomendado

1. Levantar contenedor: `docker compose up -d`

2. Entrar al shell principal: `docker exec -it nodejs sh`

3. Trabajar en tu proyecto

4. Salir con `exit` o `Ctrl+P` + `Ctrl+Q` para mantener el contenedor

5. Cuando termines todo: `docker compose down -v`

---

## 9. Notas finales

- Todos los cambios dentro del contenedor se mantendrán si usas volúmenes correctamente.

- `tty: true` y `stdin_open: true` en tu `docker-compose.yml` permiten interacción completa con el shell.

- Esta plantilla es ideal para desarrollo local de proyectos Node.js, scripts o pruebas rápidas.