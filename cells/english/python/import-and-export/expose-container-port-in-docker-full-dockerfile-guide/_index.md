---
category: general
date: 2026-06-21
description: Expose container port in Docker while setting the working directory and
  copying your app source. Learn how to dockerize a Python API step‑by‑step.
draft: false
keywords:
- expose container port
- set working directory docker
- dockerfile copy app
- copy source into container
- dockerize python api
language: en
og_description: Expose container port in Docker, set the working directory, and copy
  your source into the container. This tutorial shows how to dockerize a Python API.
og_title: Expose Container Port in Docker – Complete Guide
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
title: Expose Container Port in Docker – Full Dockerfile Guide
url: /python/import-and-export/expose-container-port-in-docker-full-dockerfile-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Expose Container Port in Docker – Full Dockerfile Guide

Ever wondered how to **expose container port** when you’re containerizing a Python API? You’re not alone. Most developers hit the same snag: the app runs locally, but once it’s inside Docker, the outside world can’t reach it. In this tutorial we’ll walk through a complete Dockerfile that not only **expose container port** but also **set working directory docker**, **dockerfile copy app**, and **copy source into container**—all the pieces you need to **dockerize python api** without breaking a sweat.

We’ll start with a tiny Flask app, then build a Docker image from scratch, explain each instruction, and finally run the container so you can hit `http://localhost:5000/health`. By the end you’ll have a production‑ready Docker image that you can push to any registry.

## Prerequisites

Before we dive in, make sure you have:

- Docker Engine ≥ 20.10 installed (Docker Desktop works fine on Windows/macOS, Docker Engine on Linux).
- Basic familiarity with Python and Flask (or any WSGI‑compatible framework).
- A text editor or IDE (VS Code, PyCharm, etc.) to edit the Dockerfile and Python code.

No additional libraries are required beyond what the official Aspose.Cells Python.NET base image provides.

## Step 1: Create a Minimal Python API

First, let’s write a tiny Flask service that we’ll later **dockerize python api**. Save this as `api_server.py` in an empty folder.

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

Why `host="0.0.0.0"`? Inside a container, `localhost` refers to the container itself. Binding to `0.0.0.0` tells Flask to accept connections from any network interface, which is essential for the **expose container port** step later.

## Step 2: Choose the Right Base Image

For this example we’ll use Aspose’s official **Aspose.Cells Python.NET base image** (`aspose/cells-pythonnet:6.22`). It already ships with .NET runtime, Python 3.9, and the Aspose.Cells library—perfect if your API needs Excel manipulation.

```dockerfile
# Use the official Aspose.Cells Python.NET base image
FROM aspose/cells-pythonnet:6.22
```

If you don’t need Aspose, you could swap this for `python:3.11-slim`. The rest of the Dockerfile stays the same.

## Step 3: **Dockerfile Copy App** – Copy Your Source Into the Container

Next, we need to bring our code into the image. This is where the **dockerfile copy app** instruction shines.

```dockerfile
# Copy the entire current directory (your app) into /app inside the container
COPY . /app
```

The `.` represents the build context—the folder where you run `docker build`. By copying everything, you also bring in `requirements.txt` (if you have one) and any static assets. If you prefer a tighter image, list only the files you actually need.

## Step 4: **Set Working Directory Docker** – Define the Working Directory

After copying, we tell Docker where to run subsequent commands. This is the **set working directory docker** step.

```dockerfile
# Set /app as the working directory for the rest of the build
WORKDIR /app
```

Why bother? It saves you from typing full paths later (e.g., `python api_server.py` instead of `python /app/api_server.py`). It also makes the container’s file system layout clearer for anyone reading the image later.

## Step 5: Install Python Dependencies (Optional but Recommended)

If your API relies on external packages, create a `requirements.txt` and install them in a separate layer. This improves caching.

```dockerfile
# Install Python dependencies (if requirements.txt exists)
RUN if [ -f requirements.txt ]; then pip install --no-cache-dir -r requirements.txt; fi
```

The conditional ensures the build won’t fail if you don’t have a `requirements.txt`—handy for the minimal example above.

## Step 6: **Expose Container Port** – Make the API Reachable from Outside

Now we get to the star of the show: **expose container port**. This tells Docker which port the container will listen on, enabling port‑mapping at runtime.

```dockerfile
# Expose the Flask port (5000) so the host can forward traffic
EXPOSE 5000
```

Note that `EXPOSE` is merely a documentation hint; the actual mapping happens when you run `docker run -p`. Still, declaring the port is a best practice and helps tools like Docker Compose automatically forward the correct ports.

## Step 7: Define the Startup Command

Finally, we tell Docker how to launch the API. This is the `CMD` instruction.

```dockerfile
# Start the Flask API when the container launches
CMD ["python", "api_server.py"]
```

Using the JSON array form avoids shell interpretation issues and makes the command more portable.

## Full Dockerfile Recap

Putting all the pieces together, here’s the complete Dockerfile you can copy‑paste:

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

> **Pro tip:** Keep the `COPY` line *before* the `RUN pip install` line if you have many dependencies. Docker will cache the layer with installed packages, so rebuilding after a code change won’t reinstall everything.

## Step 8: Build the Docker Image

Open a terminal in the folder containing `Dockerfile` and `api_server.py`, then run:

```bash
docker build -t my-python-api .
```

Docker will stream each step, showing cached layers where possible. If everything goes smoothly you’ll see `Successfully tagged my-python-api:latest`.

## Step 9: Run the Container and Verify the Port Mapping

Now launch the container, mapping the internal `5000` to your host’s `5000` (or any other host port you prefer):

```bash
docker run -d -p 5000:5000 --name api_container my-python-api
```

- `-d` runs it in detached mode.
- `-p 5000:5000` tells Docker to forward host port 5000 to container port 5000—exactly what the **expose container port** directive prepared for.

You can test the endpoint with `curl`:

```bash
curl http://localhost:5000/health
```

Expected output:

```json
{
  "status": "OK",
  "message": "API is running"
}
```

If you see this JSON, congratulations—you’ve successfully **dockerized python api** and made the port accessible.

## Common Edge Cases & How to Handle Them

### 1. Changing the Host Port

Sometimes port 5000 is already in use on your machine. No problem—just change the host side of the mapping:

```bash
docker run -d -p 8080:5000 my-python-api
```

Now `http://localhost:8080/health` will work while the container still listens on `5000`.

### 2. Multi‑Stage Builds for Smaller Images

If you don’t need the full Aspose.Cells runtime in production, you can create a multi‑stage build that compiles assets in a heavy image then copies only the runtime bits into a lightweight `python:3.11-slim` final stage. This reduces the final image size dramatically.

### 3. Using Docker Compose

For more complex setups (e.g., a database alongside the API), put the same instructions into a `docker-compose.yml`:

```yaml
version: "3.9"
services:
  api:
    build: .
    ports:
      - "5000:5000"
    restart: unless-stopped
```

Compose automatically respects the `EXPOSE` directive, so you won’t need to repeat the port mapping.

### 4. Environment Variables

If your API needs configuration (like a secret key), pass them at runtime:

```bash
docker run -d -p 5000:5000 -e SECRET_KEY=supersecret my-python-api
```

Inside Python you can read `os.getenv("SECRET_KEY")`.

## Debugging Tips

- **Container exits immediately?** Check the logs with `docker logs api_container`. A common mistake is forgetting `host="0.0.0.0"` in Flask.
- **Port already in use?** Verify with `docker ps` and `netstat -tulpn`. Use a different host port as shown above.
- **Missing dependencies?** Ensure your `requirements.txt` is present before the `RUN pip install` step, or add the packages directly in the Dockerfile.

## Recap

We started with a simple Flask app, chose a robust base image, **dockerfile copy app** to bring the code inside, **set working directory docker** for clean execution, declared `EXPOSE 5000` to **expose container port**, and finished with a `CMD` that launches the service. Building and running the image gave us a fully functional **dockerize python api** that anyone can pull and run.

## What’s Next?

- **Add a health‑check** in the Dockerfile (`HEALTHCHECK CMD curl -f http://localhost:5000/health || exit 1`).
- **Implement logging** to stdout so Docker can capture it.
- **Secure the API** with HTTPS


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Copy Sheets Within Workbook Using Aspose.Cells for .NET - Step-by-Step Guide](/cells/english/net/worksheet-management/copy-sheets-within-workbook-aspose-cells-net/)
- [Copy Data in Excel Using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)
- [How to Import DataTable into Excel Using Aspose.Cells for .NET (Step-by-Step Guide)](/cells/english/net/import-export/import-datatable-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}