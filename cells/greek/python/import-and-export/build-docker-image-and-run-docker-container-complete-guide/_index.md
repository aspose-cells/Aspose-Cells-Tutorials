---
category: general
date: 2026-06-21
description: Μάθετε πώς να δημιουργήσετε εικόνα Docker και να εκτελέσετε κοντέινερ
  Docker με σωστή αντιστοίχιση θυρών. Περιλαμβάνει αντιστοίχιση θυρών με την εντολή docker run
  και έκθεση θύρας στο Docker.
draft: false
keywords:
- build docker image
- run docker container
- docker run port mapping
- expose port in docker
- docker build from dockerfile
language: el
og_description: Δημιουργήστε εικόνα Docker και εκτελέστε κοντέινερ Docker με σωστή
  αντιστοίχιση θυρών. Κατακτήστε την αντιστοίχιση θυρών κατά την εκτέλεση Docker και
  εκθέστε τη θύρα στο Docker σε λίγα λεπτά.
og_title: Δημιουργία εικόνας Docker και εκτέλεση κοντέινερ Docker – Πλήρης οδηγός
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
title: Δημιουργία εικόνας Docker και εκτέλεση κοντέινερ Docker – Πλήρης οδηγός
url: /el/python/import-and-export/build-docker-image-and-run-docker-container-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία Docker Image και Εκτέλεση Docker Container – Πλήρης Οδηγός

Έχετε αναρωτηθεί ποτέ πώς να **build docker image** για μια απλή web εφαρμογή και μετά να την εκτελέσετε χωρίς προβλήματα; Δεν είστε μόνοι—πολλοί προγραμματιστές συναντούν το ίδιο εμπόδιο όταν αρχίζουν με τον containerization. Σε αυτόν τον οδηγό θα περάσουμε από όλη τη διαδικασία, από τη συγγραφή ενός Dockerfile μέχρι την έκθεση της σωστής θύρας και, τέλος, τη χρήση του `docker run` για να αντιστοιχίσουμε τη θύρα στο host σας. Στο τέλος θα ξέρετε ακριβώς πώς να **run docker container** με σωστή αντιστοίχιση θυρών και θα καταλάβετε γιατί η έκθεση θύρας στο Docker είναι σημαντική.

Θα καλύψουμε όλα όσα χρειάζεστε: την ακριβή εντολή `docker build`, πώς να **docker build from Dockerfile**, τις λεπτομέρειες του `docker run port mapping`, και ακόμη έναν γρήγορο έλεγχο για να βεβαιωθείτε ότι το container ακούει στη σωστή θύρα. Χωρίς περιττές πληροφορίες, μόνο πρακτικός, βήμα‑βήμα οδηγός που μπορείτε να αντιγράψετε‑επικολλήσετε στο τερματικό σας.

## What You'll Achieve

- Γράψτε ένα ελάχιστο Dockerfile για μια εφαρμογή Node.js (ή οποιαδήποτε) .  
- **Build docker image** χρησιμοποιώντας την επίσημη σύνταξη CLI.  
- Κατανοήστε τη διαφορά μεταξύ `EXPOSE` στο Dockerfile και της σημαίας `-p` στο `docker run`.  
- **Run docker container** με `docker run port mapping` ώστε να μπορείτε να προσεγγίσετε την υπηρεσία στο `http://localhost:5000`.  
- Διαγνώστε κοινά προβλήματα όπως ξεχασμένες θύρες ή μη αντιστοιχισμένες θύρες host‑container.

### Prerequisites

- Docker Engine εγκατεστημένο (Desktop ή Engine 20.10+).  
- Βασική εξοικείωση με τη γραμμή εντολών.  
- Μια μικρή web εφαρμογή (θα χρησιμοποιήσουμε έναν μονό‑γραμμή Python Flask server, αλλά μπορείτε να την αντικαταστήσετε με οτιδήποτε).  

Αν έχετε όλα αυτά, ας ξεκινήσουμε.

---

## Step 1: Create a Simple Application

Πρώτα, χρειαζόμαστε κάτι για να containerize. Δημιουργήστε έναν φάκελο που ονομάζεται `myapp` και τοποθετήστε μέσα ένα μόνο αρχείο `app.py`:

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

> **Pro tip:** Η γραμμή `host="0.0.0.0"` λέει στο Flask να ακούει σε όλα τα interfaces, κάτι που απαιτείται για το Docker να προωθήσει την κίνηση από το host.

Τώρα έχετε μια μικρή web υπηρεσία που ακούει στη θύρα 5000 μέσα στο container.

## Step 2: Write the Dockerfile (Docker Build from Dockerfile)

Στη συνέχεια, χρειαζόμαστε ένα **Dockerfile** που να λέει στο Docker πώς να συναρμολογήσει το image. Τοποθετήστε αυτό το αρχείο δίπλα στο `app.py`:

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

Μερικά σημεία που πρέπει να προσέξετε:

- `FROM python:3.11-slim` μας δίνει μια ελαφριά βάση.  
- `EXPOSE 5000` **expose port in docker** – είναι μια υπόδειξη για όποιον διαβάζει το Dockerfile, αλλά δεν ανοίγει πραγματικά τη θύρα στο host.  
- Η γραμμή `CMD` εκτελεί τον Flask server όταν ξεκινά το container.

## Step 3: **Build Docker Image** from the Dockerfile

Ανοίξτε ένα τερματικό, `cd` στον φάκελο που περιέχει το Dockerfile, και τρέξτε:

```bash
docker build -t myflaskapp .
```

Ας εξηγήσουμε αυτήν την εντολή:

- `docker build` είναι το ρήμα που **builds docker image** τα layers βάσει των οδηγιών του Dockerfile.  
- `-t myflaskapp` προσθέτει ετικέτα στην παραγόμενη εικόνα με ένα φιλικό όνομα που μπορείτε να χρησιμοποιήσετε αργότερα.  
- Το τελικό `.` λέει στο Docker να χρησιμοποιήσει τον τρέχοντα φάκελο ως build context (το μέρος όπου ψάχνει για το Dockerfile και τυχόν αρχεία που `COPY`).  

Θα πρέπει να δείτε έξοδο παρόμοια με:

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

Αν εντοπίσετε σφάλματα, ελέγξτε ξανά τη σύνταξη του Dockerfile και βεβαιωθείτε ότι το αρχείο `app.py` βρίσκεται στον ίδιο φάκελο.

### Verify the Image Exists

Τρέξτε `docker images` και ψάξτε για το `myflaskapp`:

```bash
docker images | grep myflaskapp
```

Θα δείτε κάτι σαν:

```
myflaskapp   latest   1c2d3e4f5g6h   2 minutes ago   120MB
```

Συγχαρητήρια—μόλις **built docker image** με επιτυχία!

## Step 4: **Run Docker Container** with Port Mapping

Τώρα που το image είναι έτοιμο, ήρθε η ώρα να **run docker container** και να κάνετε το Flask app προσβάσιμο από το μηχάνημά σας. Χρησιμοποιήστε τη σημαία `-p` για να κάνετε **docker run port mapping**:

```bash
docker run -p 5000:5000 myflaskapp
```

Εξήγηση:

- Το πρώτο `5000` (αριστερά) είναι η **host port**.  
- Το δεύτερο `5000` (δεξιά) είναι η **container port** που εκθέσαμε νωρίτερα.  
- Το Docker θα προωθήσει την κίνηση από `localhost:5000` στο μηχάνημά σας στη θύρα 5000 μέσα στο container.

Θα πρέπει να δείτε τα logs εκκίνησης του Flask:

```
 * Running on http://0.0.0.0:5000/ (Press CTRL+C to quit)
```

Ανοίξτε έναν browser και μεταβείτε στο `http://localhost:5000`. Θα δείτε το “Hello from Docker!”—το container εξυπηρετεί την κίνηση ακριβώς όπως περιμέναμε.

### Detaching the Container (Optional)

Αν δεν θέλετε το τερματικό να παραμείνει μπλοκαρισμένο, προσθέστε `-d` για να τρέξει στο παρασκήνιο:

```bash
docker run -d -p 5000:5000 myflaskapp
```

Μπορείτε αργότερα να το σταματήσετε με `docker stop <container-id>`.

## Step 5: Deep Dive – **Expose Port in Docker** vs. **Docker Run Port Mapping**

Είναι εύκολο να συγχέουμε την εντολή `EXPOSE` με τη σημαία `-p`, αλλά εξυπηρετούν διαφορετικούς σκοπούς:

| Concept | What it does | Does it open the port on the host? |
|---------|--------------|------------------------------------|
| `EXPOSE` (in Dockerfile) | Καταγράφει ποιες θύρες προτίθεται να ακούει το container. | **No** – απλώς μεταδεδομένα. |
| `-p host:container` (docker run) | Δημιουργεί κανόνα NAT που προωθεί την κίνηση από τη θύρα του host στη θύρα του container. | **Yes** – πραγματική προώθηση θυρών. |

Αν παραλείψετε το `EXPOSE`, η εντολή `docker run -p` λειτουργεί ακόμα, αλλά χάνετε την τεκμηρίωση για τους χρήστες που θα ακολουθήσουν. Αντίστροφα, αν μόνο `EXPOSE` και ποτέ `-p`, η υπηρεσία παραμένει μη προσβάσιμη από το host.

### Using `docker run` with Different Host Ports

Μερικές φορές μπορεί να έχετε ήδη κάτι που ακούει στη θύρα 5000 του host. Κανένα πρόβλημα—απλώς αντιστοιχίστε σε διαφορετική θύρα host:

```bash
docker run -p 8080:5000 myflaskapp
```

Τώρα η εφαρμογή είναι προσβάσιμη στο `http://localhost:8080`, ενώ συνεχίζει να ακούει στο 5000 μέσα στο container. Αυτή η ευελιξία είναι ένα από τα κύρια πλεονεκτήματα του **docker run port mapping**.

## Step 6: Common Pitfalls & Edge Cases

| Issue | Symptom | Fix |
|-------|---------|-----|
| Forgetting `EXPOSE` | Νέοι προγραμματιστές δεν ξέρουν ποια θύρα να αντιστοιχίσουν. | Προσθέστε `EXPOSE 5000` (ή όποια θύρα χρησιμοποιεί η εφαρμογή σας). |
| Using the wrong host port | Ο browser επιστρέφει “connection refused”. | Επαληθεύστε ότι το αριστερό μέρος του `-p` ταιριάζει με τη θύρα που προσπαθείτε να προσεγγίσετε. |
| Container crashes on start | Δεν υπάρχουν logs, το container τερματίζει αμέσως. | Εκτελέστε `docker logs <container-id>` για να δείτε τα σφάλματα· συχνά οφείλεται σε ελλιπείς εξαρτήσεις ή λανθασμένο `CMD`. |
| Port already in use on host | Το Docker εμφανίζει “bind: address already in use”. | Επιλέξτε διαφορετική θύρα host (`-p 8080:5000`). |
| Not binding to `0.0.0.0` | Η υπηρεσία είναι προσβάσιμη μόνο από μέσα στο container. | Στο Flask, ορίστε `host="0.0.0.0"`· άλλα frameworks έχουν παρόμοιες ρυθμίσεις. |

### Building Multi‑Stage Images (Advanced)

Αν χρειαστείτε μικρότερο τελικό image, μπορείτε να **build docker image** με ένα multi‑stage Dockerfile:

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

Αυτή η τεχνική αφαιρεί τα layers χρόνου build, δημιουργώντας ένα πιο ελαφρύ image—ιδανικό για παραγωγή.

## Step 7: Clean Up

Όταν τελειώσετε με τα πειράματα, καθαρίστε:

```bash
# Stop all running containers derived from the image
docker ps --filter "ancestor=myflaskapp" -q | xargs -r docker stop

# Remove the image
docker rmi myflaskapp
```

Ο καθαρισμός αποτρέπει την υπερφόρτωση του δίσκου και διατηρεί το περιβάλλον Docker σας τακτοποιημένο.

---

## Conclusion

Τώρα έχετε μια ολοκληρωμένη, end‑to‑end ροή εργασίας για **build docker image** και **run docker container** με σωστή **docker run port mapping**. Κατανοώντας πώς να **expose port in docker** και πώς η σημαία `-p` προωθεί πραγματικά την κίνηση, μπορείτε να containerize οποιαδήποτε υπηρεσία και να την κάνετε προσβάσιμη από το host ή το ευρύτερο δίκτυο.

Τι ακολουθεί; Δοκιμάστε να αντικαταστήσετε το Flask app με ένα Go binary, προσθέστε μεταβλητές περιβάλλοντος με `-e`, ή σπρώξτε το φρέσκο image σας στο Docker Hub χρησιμοποιώντας `docker push`. Οι δυνατότητες είναι απεριόριστες, και μόλις αποκτήσατε μια νέα υπερδύναμη στον κόσμο του DevOps.

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