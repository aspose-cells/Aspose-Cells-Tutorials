---
category: general
date: 2026-06-21
description: Aprende cómo crear una imagen Docker y ejecutar un contenedor Docker
  con el mapeo de puertos adecuado. Incluye el mapeo de puertos con docker run y la
  exposición de puertos en Docker.
draft: false
keywords:
- build docker image
- run docker container
- docker run port mapping
- expose port in docker
- docker build from dockerfile
language: es
og_description: Construye la imagen Docker y ejecuta el contenedor Docker con la asignación
  de puertos correcta. Domina la asignación de puertos al ejecutar Docker y expón
  puertos en Docker en minutos.
og_title: Crear imagen Docker y ejecutar contenedor Docker – Guía completa
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Learn how to build docker image and run docker container with proper
    port mapping. Includes docker run port mapping and expose port in docker.
  headline: Build Docker Image and Run Docker Container – Complete Guide
  type: TechArticle
- description: Learn how to build docker image and run docker container with proper
    port mapping. Includes docker run port mapping and expose port in docker.
  name: Build Docker Image and Run Docker Container – Complete Guide
  steps:
  - name: Prerequisites
    text: '- Docker Engine installed (Desktop or Engine 20.10+). - Basic familiarity
      with the command line. - A tiny web app (we’ll use a one‑line Python Flask server,
      but you can swap it for anything).'
  - name: Verify the Image Exists
    text: 'Run `docker images` and look for `myflaskapp`:'
  - name: Detaching the Container (Optional)
    text: 'If you don’t want the terminal to be blocked, add `-d` to run in the background:'
  - name: Using `docker run` with Different Host Ports
    text: 'Sometimes you might already have something listening on host port 5000.
      No problem—just map to a different host port:'
  - name: Building Multi‑Stage Images (Advanced)
    text: 'If you ever need a smaller final image, you can **build docker image**
      with a multi‑stage Dockerfile:'
  type: HowTo
tags:
- docker
- containers
- devops
title: Construir imagen Docker y ejecutar contenedor Docker – Guía completa
url: /es/python/import-and-export/build-docker-image-and-run-docker-container-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Construir Imagen Docker y Ejecutar Contenedor Docker – Guía Completa

¿Alguna vez te has preguntado cómo **build docker image** para una aplicación web simple y luego ponerla en marcha sin problemas? No estás solo—muchos desarrolladores se topan con la misma barrera cuando se introducen en la contenedorización. En este tutorial recorreremos todo el proceso, desde escribir un Dockerfile hasta exponer el puerto correcto y finalmente usar `docker run` para mapear ese puerto a tu host. Al final sabrás exactamente cómo **run docker container** con el mapeo de puertos adecuado, y verás por qué exponer un puerto en Docker es importante.

Cubrirémos todo lo que necesitas: el comando exacto `docker build`, cómo **docker build from Dockerfile**, los matices de `docker run port mapping`, e incluso una rápida verificación para asegurarnos de que el contenedor realmente está escuchando donde esperas. Sin rodeos, solo una guía práctica, paso a paso, que puedes copiar y pegar en tu terminal.

## Lo Que Lograrás

- Escribe un Dockerfile mínimo para una aplicación Node.js (o cualquier otra).  
- **Build docker image** usando la sintaxis oficial de la CLI.  
- Entiende la diferencia entre `EXPOSE` en el Dockerfile y la bandera `-p` en `docker run`.  
- **Run docker container** con `docker run port mapping` para que puedas acceder al servicio en `http://localhost:5000`.  
- Diagnostica problemas comunes como puertos olvidados o puertos host‑contenedor descoordinados.

### Requisitos Previos

- Docker Engine instalado (Desktop o Engine 20.10+).  
- Familiaridad básica con la línea de comandos.  
- Una pequeña aplicación web (usaremos un servidor Flask de una sola línea en Python, pero puedes cambiarlo por cualquier otra).  

Si tienes eso, vamos a sumergirnos.

---

## Paso 1: Crear una Aplicación Simple

Primero, necesitamos algo para contenedorizzar. Crea una carpeta llamada `myapp` y coloca un único archivo `app.py` dentro:

```python
# app.py
from flask import Flask
app = Flask(__name__)

@app.route("/")
def hello():
    return "Hello from Docker!"

if __name__ == "__main__":
    app.run(host="0.0.0.0", port=5000)
```

> **Consejo profesional:** La línea `host="0.0.0.0"` indica a Flask que escuche en todas las interfaces, lo cual es necesario para que Docker reenvíe el tráfico desde el host.

Ahora tienes un pequeño servicio web que escucha en el puerto 5000 dentro del contenedor.

## Paso 2: Escribir el Dockerfile (Docker Build from Dockerfile)

A continuación, necesitamos un **Dockerfile** que indique a Docker cómo ensamblar la imagen. Coloca este archivo junto a `app.py`:

```dockerfile
# Dockerfile
FROM python:3.11-slim

# Install Flask
RUN pip install flask

# Copy our app into the image
COPY app.py /app/app.py

WORKDIR /app

# Expose the internal port (does NOT publish it yet)
EXPOSE 5000

# Default command to run the app
CMD ["python", "app.py"]
```

- `FROM python:3.11-slim` nos proporciona una imagen base ligera.  
- `EXPOSE 5000` **expose port in docker** – es una pista para quien lea el Dockerfile, pero no abre realmente el puerto en el host.  
- La línea `CMD` ejecuta nuestro servidor Flask cuando el contenedor se inicia.

## Paso 3: **Build Docker Image** desde el Dockerfile

Abre una terminal, `cd` a la carpeta que contiene el Dockerfile, y ejecuta:

```bash
docker build -t myflaskapp .
```

Desglosaremos ese comando:

- `docker build` es el verbo que **builds docker image** capas basadas en las instrucciones del Dockerfile.  
- `-t myflaskapp` etiqueta la imagen resultante con un nombre amigable que podrás referenciar después.  
- El `.` final indica a Docker que use el directorio actual como contexto de construcción (el lugar donde busca el Dockerfile y cualquier archivo que `COPY`).

Deberías ver una salida similar a:

```
Sending build context to Docker daemon  3.072kB
Step 1/6 : FROM python:3.11-slim
 ---> 3b6c0f...
Step 2/6 : RUN pip install flask
 ---> Using cache
 ---> 9e2b7a...
...
Successfully built 1c2d3e4f5g6h
Successfully tagged myflaskapp:latest
```

Si detectas algún error, verifica la sintaxis del Dockerfile y asegúrate de que el archivo `app.py` esté en la misma carpeta.

### Verificar que la Imagen Existe

Ejecuta `docker images` y busca `myflaskapp`:

```bash
docker images | grep myflaskapp
```

Verás algo como:

```
myflaskapp   latest   1c2d3e4f5g6h   2 minutes ago   120MB
```

¡Felicidades—acabas de **built docker image** exitosamente!

## Paso 4: **Run Docker Container** con Mapeo de Puertos

Ahora que la imagen está lista, es momento de **run docker container** y hacer que la aplicación Flask sea accesible desde tu máquina host. Usa la bandera `-p` para realizar **docker run port mapping**:

```bash
docker run -p 5000:5000 myflaskapp
```

Explicación:

- El primer `5000` (lado izquierdo) es el **puerto del host**.  
- El segundo `5000` (lado derecho) es el **puerto del contenedor** que expusimos antes.  
- Docker reenviará el tráfico de `localhost:5000` en tu máquina al puerto 5000 dentro del contenedor.

Deberías ver los logs de inicio de Flask:

```
 * Running on http://0.0.0.0:5000/ (Press CTRL+C to quit)
```

Abre un navegador y navega a `http://localhost:5000`. Verás “Hello from Docker!”—el contenedor está sirviendo tráfico exactamente como esperábamos.

### Desacoplar el Contenedor (Opcional)

Si no quieres que la terminal quede bloqueada, agrega `-d` para ejecutarlo en segundo plano:

```bash
docker run -d -p 5000:5000 myflaskapp
```

Puedes detenerlo más tarde con `docker stop <container-id>`.

## Paso 5: Análisis Profundo – **Expose Port in Docker** vs. **Docker Run Port Mapping**

Es fácil confundir la instrucción `EXPOSE` con la bandera `-p`, pero cumplen propósitos diferentes:

| Concepto | Qué hace | ¿Abre el puerto en el host? |
|----------|----------|----------------------------|
| `EXPOSE` (en Dockerfile) | Documenta qué puertos el contenedor *pretende* escuchar. | **No** – solo metadatos. |
| `-p host:container` (docker run) | Crea una regla NAT que reenvía el tráfico del puerto del host al puerto del contenedor. | **Sí** – reenvío real de puertos. |

Si olvidas incluir `EXPOSE`, el comando `docker run -p` sigue funcionando, pero pierdes la documentación útil para los usuarios posteriores. Por el contrario, si solo `EXPOSE` pero nunca usas `-p`, el servicio permanece inaccesible desde el host.

### Usando `docker run` con Puertos de Host Diferentes

A veces ya puedes tener algo escuchando en el puerto 5000 del host. No hay problema—simplemente mapea a un puerto de host diferente:

```bash
docker run -p 8080:5000 myflaskapp
```

Ahora la aplicación es accesible en `http://localhost:8080`, mientras sigue escuchando en 5000 dentro del contenedor. Esta flexibilidad es una de las principales fortalezas de **docker run port mapping**.

## Paso 6: Problemas Comunes y Casos Extremos

| Problema | Síntoma | Solución |
|----------|---------|----------|
| Olvidar `EXPOSE` | Los nuevos desarrolladores no pueden saber qué puerto mapear. | Añadir `EXPOSE 5000` (o el puerto que use tu aplicación). |
| Usar el puerto de host incorrecto | El navegador devuelve “connection refused”. | Verifica que el lado izquierdo de `-p` coincida con el puerto que intentas alcanzar. |
| El contenedor se bloquea al iniciar | No hay logs, el contenedor sale instantáneamente. | Ejecuta `docker logs <container-id>` para ver los mensajes de error; a menudo se debe a dependencias faltantes o `CMD` incorrecto. |
| Puerto ya en uso en el host | Docker muestra “bind: address already in use”. | Elige un puerto de host diferente (`-p 8080:5000`). |
| No enlazar a `0.0.0.0` | El servicio solo es accesible desde dentro del contenedor. | En Flask, establece `host="0.0.0.0"`; otros frameworks tienen configuraciones similares. |

### Construcción de Imágenes Multi‑Stage (Avanzado)

Si alguna vez necesitas una imagen final más pequeña, puedes **build docker image** con un Dockerfile multi‑stage:

```dockerfile
# Stage 1: Build
FROM python:3.11-slim AS builder
RUN pip install --target=/app flask
COPY app.py /app/

# Stage 2: Runtime
FROM python:3.11-slim
COPY --from=builder /app /app
WORKDIR /app
EXPOSE 5000
CMD ["python", "app.py"]
```

Esta técnica elimina las capas de tiempo de construcción, resultando en una imagen más ligera—ideal para producción.

## Paso 7: Limpieza

Cuando termines de experimentar, limpia:

```bash
# Stop all running containers derived from the image
docker ps --filter "ancestor=myflaskapp" -q | xargs -r docker stop

# Remove the image
docker rmi myflaskapp
```

Limpiar evita la hinchazón del disco y mantiene tu entorno Docker ordenado.

---

## Conclusión

Ahora tienes un flujo de trabajo sólido, de extremo a extremo, para **build docker image** y **run docker container** con el **docker run port mapping** adecuado. Al comprender cómo **expose port in docker** y cómo la bandera `-p` realmente reenvía el tráfico, puedes contenedorizzar con confianza cualquier servicio y hacerlo accesible desde tu host o la red más amplia.

¿Qué sigue? Prueba cambiar la aplicación Flask por un binario Go, agrega variables de entorno con `-e`, o envía tu imagen recién **build docker image** a Docker Hub usando `docker push`. El cielo es el límite, y acabas de obtener un nuevo superpoder en el mundo de DevOps.

Feliz contenedorización

## ¿Qué Deberías Aprender Después?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Domina el Renderizado de Imágenes en Excel Usando Aspose.Cells para .NET: Guía Completa](/cells/english/net/images-shapes/master-image-rendering-excel-aspose-cells-net/)
- [Cómo Añadir una Imagen a un Gráfico con Aspose.Cells para .NET: Guía Paso a Paso](/cells/english/net/charts-graphs/add-image-chart-aspose-cells-dotnet/)
- [Cómo Añadir Hipervínculos de Imagen en Libros de Trabajo .NET Usando Aspose.Cells para Mayor Interactividad](/cells/english/net/images-shapes/adding-image-hyperlinks-net-workbooks-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}