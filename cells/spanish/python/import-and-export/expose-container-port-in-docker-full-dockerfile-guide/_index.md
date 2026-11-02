---
category: general
date: 2026-06-21
description: Exponer el puerto del contenedor en Docker mientras se establece el directorio
  de trabajo y se copia el código fuente de la aplicación. Aprende a dockerizar una
  API de Python paso a paso.
draft: false
keywords:
- expose container port
- set working directory docker
- dockerfile copy app
- copy source into container
- dockerize python api
language: es
og_description: Expone el puerto del contenedor en Docker, establece el directorio
  de trabajo y copia tu código fuente en el contenedor. Este tutorial muestra cómo
  dockerizar una API de Python.
og_title: Exponer el puerto del contenedor en Docker – Guía completa
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Expose container port in Docker while setting the working directory
    and copying your app source. Learn how to dockerize a Python API step‑by‑step.
  headline: Expose Container Port in Docker – Full Dockerfile Guide
  type: TechArticle
- description: Expose container port in Docker while setting the working directory
    and copying your app source. Learn how to dockerize a Python API step‑by‑step.
  name: Expose Container Port in Docker – Full Dockerfile Guide
  steps:
  - name: 1. Changing the Host Port
    text: 'Sometimes port 5000 is already in use on your machine. No problem—just
      change the host side of the mapping:'
  - name: 2. Multi‑Stage Builds for Smaller Images
    text: If you don’t need the full Aspose.Cells runtime in production, you can create
      a multi‑stage build that compiles assets in a heavy image then copies only the
      runtime bits into a lightweight `python:3.11-slim` final stage. This reduces
      the final image size dramatically.
  - name: 3. Using Docker Compose
    text: 'For more complex setups (e.g., a database alongside the API), put the same
      instructions into a `docker-compose.yml`:'
  - name: 4. Environment Variables
    text: 'If your API needs configuration (like a secret key), pass them at runtime:'
  type: HowTo
- questions:
  - answer: Check the logs with `docker logs api_container`. A common mistake is forgetting
      `host="0.0.0.0"` in Flask.
    question: Container exits immediately?
  - answer: Verify with `docker ps` and `netstat -tulpn`. Use a different host port
      as shown above.
    question: Port already in use?
  - answer: Ensure your `requirements.txt` is present before the `RUN pip install`
      step, or add the packages directly in the Dockerfile.
    question: Missing dependencies?
  type: FAQPage
tags:
- Docker
- Python
- API
title: Exponer el puerto del contenedor en Docker – Guía completa del Dockerfile
url: /es/python/import-and-export/expose-container-port-in-docker-full-dockerfile-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exponer el Puerto del Contenedor en Docker – Guía Completa del Dockerfile

¿Alguna vez te has preguntado cómo **expose container port** cuando estás containerizando una API de Python? No estás solo. La mayoría de los desarrolladores se topan con el mismo problema: la aplicación funciona localmente, pero una vez dentro de Docker, el mundo exterior no puede alcanzarla. En este tutorial recorreremos un Dockerfile completo que no solo **expose container port** sino también **set working directory docker**, **dockerfile copy app**, y **copy source into container**—todas las piezas que necesitas para **dockerize python api** sin esfuerzo.

Comenzaremos con una pequeña aplicación Flask, luego construiremos una imagen Docker desde cero, explicaremos cada instrucción y finalmente ejecutaremos el contenedor para que puedas acceder a `http://localhost:5000/health`. Al final tendrás una imagen Docker lista para producción que podrás subir a cualquier registro.

## Requisitos Previos

- Docker Engine ≥ 20.10 instalado (Docker Desktop funciona bien en Windows/macOS, Docker Engine en Linux).
- Familiaridad básica con Python y Flask (o cualquier framework compatible con WSGI).
- Un editor de texto o IDE (VS Code, PyCharm, etc.) para editar el Dockerfile y el código Python.

No se requieren bibliotecas adicionales más allá de lo que proporciona la imagen base oficial Aspose.Cells Python.NET.

## Paso 1: Crear una API Python Minimalista

Primero, escribamos un pequeño servicio Flask que más adelante **dockerize python api**. Guárdalo como `api_server.py` en una carpeta vacía.

```python
# api_server.py
from flask import Flask, jsonify

app = Flask(__name__)

@app.route("/health")
def health():
    return jsonify(status="OK", message="API is running")

if __name__ == "__main__":
    # Listen on all interfaces so Docker can forward the port
    app.run(host="0.0.0.0", port=5000)
```

¿Por qué `host="0.0.0.0"`? Dentro de un contenedor, `localhost` se refiere al propio contenedor. Enlazar a `0.0.0.0` indica a Flask que acepte conexiones de cualquier interfaz de red, lo cual es esencial para el paso **expose container port** más adelante.

## Paso 2: Elegir la Imagen Base Adecuada

Para este ejemplo usaremos la **Aspose.Cells Python.NET base image** oficial de Aspose (`aspose/cells-pythonnet:6.22`). Ya incluye el runtime de .NET, Python 3.9 y la biblioteca Aspose.Cells—perfecto si tu API necesita manipulación de Excel.

```dockerfile
# Use the official Aspose.Cells Python.NET base image
FROM aspose/cells-pythonnet:6.22
```

Si no necesitas Aspose, puedes cambiarla por `python:3.11-slim`. El resto del Dockerfile permanece igual.

## Paso 3: **Dockerfile Copy App** – Copiar tu Código Fuente Dentro del Contenedor

A continuación, necesitamos llevar nuestro código a la imagen. Aquí es donde la instrucción **dockerfile copy app** destaca.

```dockerfile
# Copy the entire current directory (your app) into /app inside the container
COPY . /app
```

El `.` representa el contexto de compilación—la carpeta donde ejecutas `docker build`. Al copiar todo, también traes `requirements.txt` (si lo tienes) y cualquier recurso estático. Si prefieres una imagen más ajustada, lista solo los archivos que realmente necesitas.

## Paso 4: **Set Working Directory Docker** – Definir el Directorio de Trabajo

Después de copiar, le indicamos a Docker dónde ejecutar los comandos subsecuentes. Este es el paso **set working directory docker**.

```dockerfile
# Set /app as the working directory for the rest of the build
WORKDIR /app
```

¿Por qué molestarse? Te ahorra escribir rutas completas más adelante (p.ej., `python api_server.py` en lugar de `python /app/api_server.py`). También hace que la estructura del sistema de archivos del contenedor sea más clara para quien lea la imagen después.

## Paso 5: Instalar Dependencias de Python (Opcional pero Recomendado)

Si tu API depende de paquetes externos, crea un `requirements.txt` e instálalos en una capa separada. Esto mejora el caching.

```dockerfile
# Install Python dependencies (if requirements.txt exists)
RUN if [ -f requirements.txt ]; then pip install --no-cache-dir -r requirements.txt; fi
```

La condición garantiza que la compilación no falle si no tienes un `requirements.txt`—útil para el ejemplo minimalista anterior.

## Paso 6: **Expose Container Port** – Hacer que la API sea Accesible desde el Exterior

Ahora llegamos a la estrella del espectáculo: **expose container port**. Esto indica a Docker qué puerto escuchará el contenedor, habilitando el mapeo de puertos en tiempo de ejecución.

```dockerfile
# Expose the Flask port (5000) so the host can forward traffic
EXPOSE 5000
```

Ten en cuenta que `EXPOSE` es solo una pista de documentación; el mapeo real ocurre cuando ejecutas `docker run -p`. Aún así, declarar el puerto es una buena práctica y ayuda a herramientas como Docker Compose a reenviar automáticamente los puertos correctos.

## Paso 7: Definir el Comando de Inicio

Finalmente, le indicamos a Docker cómo lanzar la API. Esta es la instrucción `CMD`.

```dockerfile
# Start the Flask API when the container launches
CMD ["python", "api_server.py"]
```

Usar la forma de arreglo JSON evita problemas de interpretación del shell y hace el comando más portable.

## Recapitulación Completa del Dockerfile

Juntando todas las piezas, aquí tienes el Dockerfile completo que puedes copiar‑pegar:

```dockerfile
# Step 1: Use the official Aspose.Cells Python.NET base image
FROM aspose/cells-pythonnet:6.22

# Step 2: Copy your application source code into the container
COPY . /app

# Step 3: Set the working directory to the application folder
WORKDIR /app

# Optional: Install Python dependencies if you have a requirements file
RUN if [ -f requirements.txt ]; then pip install --no-cache-dir -r requirements.txt; fi

# Step 4: Expose the port your API server will listen on
EXPOSE 5000

# Step 5: Define the command to start the API server
CMD ["python", "api_server.py"]
```

> **Consejo profesional:** Mantén la línea `COPY` *antes* de la línea `RUN pip install` si tienes muchas dependencias. Docker almacenará en caché la capa con los paquetes instalados, de modo que volver a compilar después de un cambio de código no reinstalará todo.

## Paso 8: Construir la Imagen Docker

Abre una terminal en la carpeta que contiene `Dockerfile` y `api_server.py`, luego ejecuta:

```bash
docker build -t my-python-api .
```

Docker mostrará cada paso, indicando capas en caché cuando sea posible. Si todo va bien verás `Successfully tagged my-python-api:latest`.

## Paso 9: Ejecutar el Contenedor y Verificar el Mapeo de Puertos

Ahora lanza el contenedor, mapeando el `5000` interno al `5000` de tu host (o cualquier otro puerto del host que prefieras):

```bash
docker run -d -p 5000:5000 --name api_container my-python-api
```

- `-d` lo ejecuta en modo desacoplado.
- `-p 5000:5000` indica a Docker que reenvíe el puerto 5000 del host al puerto 5000 del contenedor—exactamente lo que preparó la directiva **expose container port**.

Puedes probar el endpoint con `curl`:

```bash
curl http://localhost:5000/health
```

Salida esperada:

```json
{
  "status": "OK",
  "message": "API is running"
}
```

Si ves este JSON, felicidades—has **dockerized python api** con éxito y has hecho el puerto accesible.

## Casos Límite Comunes y Cómo Manejarlo

### 1. Cambiar el Puerto del Host

A veces el puerto 5000 ya está en uso en tu máquina. No hay problema—simplemente cambia el lado del host del mapeo:

```bash
docker run -d -p 8080:5000 my-python-api
```

Ahora `http://localhost:8080/health` funcionará mientras el contenedor sigue escuchando en `5000`.

### 2. Construcciones Multi‑Stage para Imágenes Más Pequeñas

Si no necesitas el runtime completo de Aspose.Cells en producción, puedes crear una construcción multi‑stage que compile los recursos en una imagen pesada y luego copie solo los componentes de runtime a una etapa final ligera `python:3.11-slim`. Esto reduce drásticamente el tamaño de la imagen final.

### 3. Usar Docker Compose

Para configuraciones más complejas (p.ej., una base de datos junto a la API), coloca las mismas instrucciones en un `docker-compose.yml`:

```yaml
version: "3.9"
services:
  api:
    build: .
    ports:
      - "5000:5000"
    restart: unless-stopped
```

Compose respeta automáticamente la directiva `EXPOSE`, por lo que no necesitarás repetir el mapeo de puertos.

### 4. Variables de Entorno

Si tu API necesita configuración (como una clave secreta), pásalas en tiempo de ejecución:

```bash
docker run -d -p 5000:5000 -e SECRET_KEY=supersecret my-python-api
```

Dentro de Python puedes leer `os.getenv("SECRET_KEY")`.

## Consejos de Depuración

- **¿El contenedor sale inmediatamente?** Revisa los logs con `docker logs api_container`. Un error común es olvidar `host="0.0.0.0"` en Flask.
- **¿Puerto ya en uso?** Verifica con `docker ps` y `netstat -tulpn`. Usa un puerto de host diferente como se mostró arriba.
- **¿Faltan dependencias?** Asegúrate de que tu `requirements.txt` esté presente antes del paso `RUN pip install`, o agrega los paquetes directamente en el Dockerfile.

## Recapitulación

Comenzamos con una sencilla aplicación Flask, elegimos una imagen base robusta, **dockerfile copy app** para llevar el código dentro, **set working directory docker** para una ejecución limpia, declaramos `EXPOSE 5000` para **expose container port**, y terminamos con un `CMD` que lanza el servicio. Construir y ejecutar la imagen nos dio una **dockerize python api** totalmente funcional que cualquiera puede descargar y ejecutar.

## ¿Qué Sigue?

- **Agregar un health‑check** en el Dockerfile (`HEALTHCHECK CMD curl -f http://localhost:5000/health || exit 1`).
- **Implementar logging** a stdout para que Docker pueda capturarlo.
- **Asegurar la API** con HTTPS

## ¿Qué Deberías Aprender a Continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Copy Sheets Within Workbook Using Aspose.Cells for .NET - Step-by-Step Guide](/cells/english/net/worksheet-management/copy-sheets-within-workbook-aspose-cells-net/)
- [Copy Data in Excel Using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)
- [How to Import DataTable into Excel Using Aspose.Cells for .NET (Step-by-Step Guide)](/cells/english/net/import-export/import-datatable-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}