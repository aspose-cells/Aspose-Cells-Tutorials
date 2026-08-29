---
category: general
date: 2026-06-21
description: Learn how to build docker image and run docker container with proper
  port mapping. Includes docker run port mapping and expose port in docker.
draft: false
keywords:
- build docker image
- run docker container
- docker run port mapping
- expose port in docker
- docker build from dockerfile
language: en
og_description: Build docker image and run docker container with correct port mapping.
  Master docker run port mapping and expose port in docker in minutes.
og_title: Build Docker Image and Run Docker Container – Complete Guide
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
title: Build Docker Image and Run Docker Container – Complete Guide
url: /python/import-and-export/build-docker-image-and-run-docker-container-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Build Docker Image and Run Docker Container – Complete Guide

Ever wondered how to **build docker image** for a simple web app and then get it up and running without a hitch? You're not alone—many devs hit the same wall when they first dabble with containerization. In this tutorial we’ll walk through the entire process, from writing a Dockerfile to exposing the right port and finally using `docker run` to map that port to your host. By the end you’ll know exactly how to **run docker container** with proper port mapping, and you’ll see why exposing a port in Docker matters.

We'll cover everything you need: the exact `docker build` command, how to **docker build from Dockerfile**, the nuances of `docker run port mapping`, and even a quick sanity check to make sure the container is really listening where you expect. No fluff, just a hands‑on, step‑by‑step guide that you can copy‑paste into your terminal.

## What You'll Achieve

- Write a minimal Dockerfile for a Node.js (or any) app.  
- **Build docker image** using the official CLI syntax.  
- Understand the difference between `EXPOSE` in the Dockerfile and the `-p` flag in `docker run`.  
- **Run docker container** with `docker run port mapping` so you can reach the service at `http://localhost:5000`.  
- Diagnose common pitfalls like forgotten ports or mismatched host‑container ports.

### Prerequisites

- Docker Engine installed (Desktop or Engine 20.10+).  
- Basic familiarity with the command line.  
- A tiny web app (we’ll use a one‑line Python Flask server, but you can swap it for anything).  

If you’ve got those, let’s dive in.

---

## Step 1: Create a Simple Application

First, we need something to containerize. Create a folder called `myapp` and drop a single file `app.py` inside:

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

> **Pro tip:** The `host="0.0.0.0"` line tells Flask to listen on all interfaces, which is required for Docker to forward traffic from the host.

Now you have a tiny web service that listens on port 5000 inside the container.

## Step 2: Write the Dockerfile (Docker Build from Dockerfile)

Next, we need a **Dockerfile** that tells Docker how to assemble the image. Place this file next to `app.py`:

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

A few things to note:

- `FROM python:3.11-slim` gives us a lightweight base image.  
- `EXPOSE 5000` **expose port in docker** – it’s a hint for anyone reading the Dockerfile, but it doesn’t actually open the port on the host.  
- The `CMD` line runs our Flask server when the container starts.

## Step 3: **Build Docker Image** from the Dockerfile

Open a terminal, `cd` into the folder containing the Dockerfile, and run:

```bash
docker build -t myflaskapp .
```

Let’s unpack that command:

- `docker build` is the verb that **builds docker image** layers based on the Dockerfile instructions.  
- `-t myflaskapp` tags the resulting image with a friendly name you can reference later.  
- The trailing `.` tells Docker to use the current directory as the build context (the place where it looks for the Dockerfile and any files you `COPY`).

You should see output similar to:

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

If you spot any errors, double‑check the Dockerfile syntax and make sure the `app.py` file is in the same folder.

### Verify the Image Exists

Run `docker images` and look for `myflaskapp`:

```bash
docker images | grep myflaskapp
```

You’ll see something like:

```
myflaskapp   latest   1c2d3e4f5g6h   2 minutes ago   120MB
```

Congrats—you’ve just **built docker image** successfully!

## Step 4: **Run Docker Container** with Port Mapping

Now that the image is ready, it’s time to **run docker container** and make the Flask app reachable from your host machine. Use the `-p` flag to perform **docker run port mapping**:

```bash
docker run -p 5000:5000 myflaskapp
```

Explanation:

- The first `5000` (left side) is the **host port**.  
- The second `5000` (right side) is the **container port** we exposed earlier.  
- Docker will forward traffic from `localhost:5000` on your machine to port 5000 inside the container.

You should see Flask’s startup logs:

```
 * Running on http://0.0.0.0:5000/ (Press CTRL+C to quit)
```

Open a browser and navigate to `http://localhost:5000`. You’ll see “Hello from Docker!”—the container is serving traffic exactly as we expected.

### Detaching the Container (Optional)

If you don’t want the terminal to be blocked, add `-d` to run in the background:

```bash
docker run -d -p 5000:5000 myflaskapp
```

You can later stop it with `docker stop <container-id>`.

## Step 5: Deep Dive – **Expose Port in Docker** vs. **Docker Run Port Mapping**

It’s easy to conflate the `EXPOSE` instruction with the `-p` flag, but they serve different purposes:

| Concept | What it does | Does it open the port on the host? |
|---------|--------------|------------------------------------|
| `EXPOSE` (in Dockerfile) | Documents which ports the container *intends* to listen on. | **No** – just metadata. |
| `-p host:container` (docker run) | Creates a NAT rule that forwards traffic from the host port to the container port. | **Yes** – actual port forwarding. |

If you forget to include `EXPOSE`, the `docker run -p` command still works, but you lose the helpful documentation for downstream users. Conversely, if you only `EXPOSE` but never use `-p`, the service stays inaccessible from the host.

### Using `docker run` with Different Host Ports

Sometimes you might already have something listening on host port 5000. No problem—just map to a different host port:

```bash
docker run -p 8080:5000 myflaskapp
```

Now the app is reachable at `http://localhost:8080`, while still listening on 5000 inside the container. This flexibility is one of the core strengths of **docker run port mapping**.

## Step 6: Common Pitfalls & Edge Cases

| Issue | Symptom | Fix |
|-------|---------|-----|
| Forgetting `EXPOSE` | New developers can’t tell which port to map. | Add `EXPOSE 5000` (or whatever your app uses). |
| Using the wrong host port | Browser returns “connection refused”. | Verify the left side of `-p` matches the port you’re trying to reach. |
| Container crashes on start | No logs, container exits instantly. | Run `docker logs <container-id>` to see error messages; often caused by missing dependencies or wrong `CMD`. |
| Port already in use on host | Docker prints “bind: address already in use”. | Choose a different host port (`-p 8080:5000`). |
| Not binding to `0.0.0.0` | Service only reachable from inside container. | In Flask, set `host="0.0.0.0"`; other frameworks have similar settings. |

### Building Multi‑Stage Images (Advanced)

If you ever need a smaller final image, you can **build docker image** with a multi‑stage Dockerfile:

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

This technique strips out build‑time layers, resulting in a leaner image—great for production.

## Step 7: Clean Up

When you’re done experimenting, tidy up:

```bash
# Stop all running containers derived from the image
docker ps --filter "ancestor=myflaskapp" -q | xargs -r docker stop

# Remove the image
docker rmi myflaskapp
```

Cleaning up prevents disk bloat and keeps your Docker environment tidy.

---

## Conclusion

You now have a solid, end‑to‑end workflow for **build docker image** and **run docker container** with proper **docker run port mapping**. By understanding how to **expose port in docker** and how the `-p` flag actually forwards traffic, you can confidently containerize any service and make it reachable from your host or the wider network.

What’s next? Try swapping the Flask app for a Go binary, add environment variables with `-e`, or push your freshly‑built image to Docker Hub using `docker push`. The sky’s the limit, and you’ve just earned a new superpower in the world of DevOps.

Happy container


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Master Image Rendering in Excel Using Aspose.Cells for .NET: A Comprehensive Guide](/cells/english/net/images-shapes/master-image-rendering-excel-aspose-cells-net/)
- [How to Add an Image to a Chart with Aspose.Cells for .NET: A Step-by-Step Guide](/cells/english/net/charts-graphs/add-image-chart-aspose-cells-dotnet/)
- [How to Add Image Hyperlinks in .NET Workbooks Using Aspose.Cells for Enhanced Interactivity](/cells/english/net/images-shapes/adding-image-hyperlinks-net-workbooks-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}