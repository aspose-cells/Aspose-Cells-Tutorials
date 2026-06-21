---
category: general
date: 2026-06-21
description: Αποκάλυψη θύρας του container στο Docker ενώ ορίζετε τον κατάλογο εργασίας
  και αντιγράφετε την πηγή της εφαρμογής σας. Μάθετε πώς να Dockerize ένα Python API
  βήμα‑βήμα.
draft: false
keywords:
- expose container port
- set working directory docker
- dockerfile copy app
- copy source into container
- dockerize python api
language: el
og_description: Ανοίξτε τη θύρα του container στο Docker, ορίστε τον κατάλογο εργασίας
  και αντιγράψτε τον πηγαίο κώδικά σας στο container. Αυτό το σεμινάριο δείχνει πώς
  να dockerize μια Python API.
og_title: Αποκάλυψη θύρας κοντέινερ στο Docker – Πλήρης οδηγός
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
title: Αποκάλυψη Θύρας Κοντέινερ στο Docker – Πλήρης Οδηγός Dockerfile
url: /el/python/import-and-export/expose-container-port-in-docker-full-dockerfile-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εκθέστε τη Θύρα του Container σε Docker – Πλήρης Οδηγός Dockerfile

Έχετε αναρωτηθεί ποτέ πώς να **expose container port** όταν κάνετε containerize ένα Python API; Δεν είστε μόνοι. Οι περισσότεροι προγραμματιστές αντιμετωπίζουν το ίδιο πρόβλημα: η εφαρμογή τρέχει τοπικά, αλλά μόλις βρίσκεται μέσα σε Docker, ο έξω κόσμος δεν μπορεί να την προσεγγίσει. Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από ένα πλήρες Dockerfile που όχι μόνο **expose container port** αλλά και **set working directory docker**, **dockerfile copy app**, και **copy source into container**—όλα τα στοιχεία που χρειάζεστε για να **dockerize python api** χωρίς κόπο.

Θα ξεκινήσουμε με μια μικρή εφαρμογή Flask, μετά θα δημιουργήσουμε μια εικόνα Docker από το μηδέν, θα εξηγήσουμε κάθε εντολή και τέλος θα τρέξουμε το container ώστε να μπορείτε να προσπελάσετε το `http://localhost:5000/health`. Στο τέλος θα έχετε μια έτοιμη για παραγωγή εικόνα Docker που μπορείτε να σπρώξετε σε οποιοδήποτε registry.

## Προαπαιτούμενα

- Docker Engine ≥ 20.10 εγκατεστημένο (Docker Desktop λειτουργεί καλά σε Windows/macOS, Docker Engine σε Linux).
- Βασική εξοικείωση με Python και Flask (ή οποιοδήποτε WSGI‑compatible framework).
- Ένας επεξεργαστής κειμένου ή IDE (VS Code, PyCharm κ.λπ.) για την επεξεργασία του Dockerfile και του κώδικα Python.

Δεν απαιτούνται πρόσθετες βιβλιοθήκες πέρα από αυτές που παρέχει η επίσημη εικόνα base Aspose.Cells Python.NET.

## Βήμα 1: Δημιουργία Ελάχιστου Python API

Πρώτα, ας γράψουμε μια μικρή υπηρεσία Flask που θα **dockerize python api** αργότερα. Αποθηκεύστε το ως `api_server.py` σε έναν κενό φάκελο.

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

Γιατί `host="0.0.0.0"`; Μέσα σε ένα container, το `localhost` αναφέρεται στο ίδιο το container. Η δέσμευση στο `0.0.0.0` λέει στο Flask να δέχεται συνδέσεις από οποιοδήποτε δίκτυο, κάτι που είναι ουσιώδες για το βήμα **expose container port** αργότερα.

## Βήμα 2: Επιλογή της Κατάλληλης Εικόνας Base

Για αυτό το παράδειγμα θα χρησιμοποιήσουμε την επίσημη **Aspose.Cells Python.NET base image** της Aspose (`aspose/cells-pythonnet:6.22`). Περιλαμβάνει ήδη .NET runtime, Python 3.9 και τη βιβλιοθήκη Aspose.Cells—τέλεια αν το API σας χρειάζεται χειρισμό Excel.

```dockerfile
# Use the official Aspose.Cells Python.NET base image
FROM aspose/cells-pythonnet:6.22
```

Αν δεν χρειάζεστε την Aspose, μπορείτε να την αντικαταστήσετε με `python:3.11-slim`. Το υπόλοιπο του Dockerfile παραμένει το ίδιο.

## Βήμα 3: **Dockerfile Copy App** – Αντιγραφή του Κώδικα Σας στο Container

Στη συνέχεια, πρέπει να φέρουμε τον κώδικά μας στην εικόνα. Εδώ η εντολή **dockerfile copy app** ξεχωρίζει.

```dockerfile
# Copy the entire current directory (your app) into /app inside the container
COPY . /app
```

Το `.` αντιπροσωπεύει το build context—τον φάκελο όπου εκτελείτε `docker build`. Αντιγράφοντας όλα, φέρετε επίσης το `requirements.txt` (αν υπάρχει) και τυχόν στατικά αρχεία. Αν προτιμάτε μια πιο ελαφριά εικόνα, καταγράψτε μόνο τα αρχεία που χρειάζεστε πραγματικά.

## Βήμα 4: **Set Working Directory Docker** – Ορισμός του Καταλόγου Εργασίας

Μετά την αντιγραφή, λέμε στο Docker πού να εκτελεί τις επόμενες εντολές. Αυτό είναι το βήμα **set working directory docker**.

```dockerfile
# Set /app as the working directory for the rest of the build
WORKDIR /app
```

Γιατί να ασχοληθείτε; Σας εξοικονομεί το γράψιμο πλήρων διαδρομών αργότερα (π.χ., `python api_server.py` αντί για `python /app/api_server.py`). Επίσης κάνει τη δομή του συστήματος αρχείων του container πιο σαφή για όποιον διαβάσει την εικόνα αργότερα.

## Βήμα 5: Εγκατάσταση Εξαρτήσεων Python (Προαιρετικό αλλά Συνιστάται)

Αν το API σας εξαρτάται από εξωτερικά πακέτα, δημιουργήστε ένα `requirements.txt` και εγκαταστήστε τα σε ξεχωριστό layer. Αυτό βελτιώνει την caching.

```dockerfile
# Install Python dependencies (if requirements.txt exists)
RUN if [ -f requirements.txt ]; then pip install --no-cache-dir -r requirements.txt; fi
```

Η συνθήκη εξασφαλίζει ότι η κατασκευή δεν θα αποτύχει αν δεν έχετε `requirements.txt`—χρήσιμο για το ελάχιστο παράδειγμα παραπάνω.

## Βήμα 6: **Expose Container Port** – Καθιστώντας το API Προσβάσιμο από το Εξωτερικό

Τώρα φτάνουμε στο αστέρι της παράστασης: **expose container port**. Αυτό λέει στο Docker ποια θύρα θα ακούει το container, ενεργοποιώντας την αντιστοίχιση θυρών κατά την εκτέλεση.

```dockerfile
# Expose the Flask port (5000) so the host can forward traffic
EXPOSE 5000
```

Σημειώστε ότι το `EXPOSE` είναι μόνο μια υπόδειξη τεκμηρίωσης· η πραγματική αντιστοίχιση συμβαίνει όταν τρέχετε `docker run -p`. Παρόλα αυτά, η δήλωση της θύρας είναι καλή πρακτική και βοηθά εργαλεία όπως το Docker Compose να προωθούν αυτόματα τις σωστές θύρες.

## Βήμα 7: Ορισμός της Εντολής Εκκίνησης

Τέλος, λέμε στο Docker πώς να ξεκινήσει το API. Αυτή είναι η εντολή `CMD`.

```dockerfile
# Start the Flask API when the container launches
CMD ["python", "api_server.py"]
```

Η χρήση της μορφής JSON array αποφεύγει προβλήματα ερμηνείας του shell και κάνει την εντολή πιο φορητή.

## Πλήρης Επανάληψη Dockerfile

Συνδυάζοντας όλα τα κομμάτια, εδώ είναι το πλήρες Dockerfile που μπορείτε να αντιγράψετε‑επικολλήσετε:

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

> **Pro tip:** Κρατήστε τη γραμμή `COPY` *πριν* τη γραμμή `RUN pip install` αν έχετε πολλές εξαρτήσεις. Το Docker θα κάνει cache το layer με τα εγκατεστημένα πακέτα, έτσι η επανακατασκευή μετά από αλλαγή κώδικα δεν θα επανεγκαταστήσει τα πάντα.

## Βήμα 8: Κατασκευή της Εικόνας Docker

Ανοίξτε ένα τερματικό στον φάκελο που περιέχει το `Dockerfile` και το `api_server.py`, μετά τρέξτε:

```bash
docker build -t my-python-api .
```

Το Docker θα εμφανίζει κάθε βήμα, δείχνοντας cached layers όπου είναι δυνατόν. Αν όλα πάνε καλά, θα δείτε `Successfully tagged my-python-api:latest`.

## Βήμα 9: Εκτέλεση του Container και Επαλήθευση της Αντιστοίχισης Θυρών

Τώρα ξεκινήστε το container, αντιστοιχίζοντας το εσωτερικό `5000` στο `5000` του host σας (ή οποιαδήποτε άλλη θύρα host προτιμάτε):

```bash
docker run -d -p 5000:5000 --name api_container my-python-api
```

- `-d` το τρέχει σε αποσπασμένη λειτουργία.
- `-p 5000:5000` λέει στο Docker να προωθήσει τη θύρα 5000 του host στη θύρα 5000 του container—ακριβώς αυτό που προετοίμασε η οδηγία **expose container port**.

Μπορείτε να δοκιμάσετε το endpoint με `curl`:

```bash
curl http://localhost:5000/health
```

Αναμενόμενη έξοδος:

```json
{
  "status": "OK",
  "message": "API is running"
}
```

Αν δείτε αυτό το JSON, συγχαρητήρια—έχετε επιτυχώς **dockerized python api** και έχετε κάνει τη θύρα προσβάσιμη.

## Συνηθισμένες Ακραίες Περιπτώσεις & Πώς να τις Διαχειριστείτε

### 1. Αλλαγή της Θύρας Host

Μερικές φορές η θύρα 5000 είναι ήδη σε χρήση στο μηχάνημά σας. Κανένα πρόβλημα—απλώς αλλάξτε την πλευρά του host στην αντιστοίχιση:

```bash
docker run -d -p 8080:5000 my-python-api
```

Τώρα το `http://localhost:8080/health` θα λειτουργεί ενώ το container εξακολουθεί να ακούει στη `5000`.

### 2. Πολυ‑Στάδια Κατασκευές για Μικρότερες Εικόνες

Αν δεν χρειάζεστε το πλήρες runtime της Aspose.Cells στην παραγωγή, μπορείτε να δημιουργήσετε μια multi‑stage κατασκευή που συνθέτει τα assets σε μια βαριά εικόνα και στη συνέχεια αντιγράφει μόνο τα runtime στοιχεία σε ένα ελαφρύ τελικό στάδιο `python:3.11-slim`. Αυτό μειώνει δραστικά το τελικό μέγεθος της εικόνας.

### 3. Χρήση Docker Compose

Για πιο σύνθετες ρυθμίσεις (π.χ., μια βάση δεδομένων μαζί με το API), τοποθετήστε τις ίδιες εντολές σε ένα `docker-compose.yml`:

```yaml
version: "3.9"
services:
  api:
    build: .
    ports:
      - "5000:5000"
    restart: unless-stopped
```

Το Compose σέβεται αυτόματα την οδηγία `EXPOSE`, οπότε δεν χρειάζεται να επαναλάβετε την αντιστοίχιση θυρών.

### 4. Μεταβλητές Περιβάλλοντος

Αν το API σας χρειάζεται ρυθμίσεις (όπως ένα μυστικό κλειδί), περάστε τις κατά την εκτέλεση:

```bash
docker run -d -p 5000:5000 -e SECRET_KEY=supersecret my-python-api
```

Μέσα στο Python μπορείτε να διαβάσετε `os.getenv("SECRET_KEY")`.

## Συμβουλές Εντοπισμού Σφαλμάτων

- **Container exits immediately?** Ελέγξτε τα logs με `docker logs api_container`. Ένα κοινό λάθος είναι η παράλειψη του `host="0.0.0.0"` στο Flask.
- **Port already in use?** Επαληθεύστε με `docker ps` και `netstat -tulpn`. Χρησιμοποιήστε διαφορετική θύρα host όπως φαίνεται παραπάνω.
- **Missing dependencies?** Βεβαιωθείτε ότι το `requirements.txt` υπάρχει πριν από το βήμα `RUN pip install`, ή προσθέστε τα πακέτα απευθείας στο Dockerfile.

## Ανακεφαλαίωση

Ξεκινήσαμε με μια απλή εφαρμογή Flask, επιλέξαμε μια ισχυρή εικόνα base, **dockerfile copy app** για να φέρουμε τον κώδικα μέσα, **set working directory docker** για καθαρή εκτέλεση, δηλώσαμε `EXPOSE 5000` για **expose container port**, και ολοκληρώσαμε με ένα `CMD` που εκκινεί την υπηρεσία. Η κατασκευή και η εκτέλεση της εικόνας μας έδωσε ένα πλήρως λειτουργικό **dockerize python api** που όποιος μπορεί να το κατεβάσει και να το τρέξει.

## Τι Ακολουθεί;

- **Προσθήκη health‑check** στο Dockerfile (`HEALTHCHECK CMD curl -f http://localhost:5000/health || exit 1`).
- **Υλοποίηση logging** στο stdout ώστε το Docker να το καταγράφει.
- **Ασφάλιση του API** με HTTPS

## Τι Πρέπει Να Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετικές θεματικές που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες λειτουργίες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Copy Sheets Within Workbook Using Aspose.Cells for .NET - Step-by-Step Guide](/cells/english/net/worksheet-management/copy-sheets-within-workbook-aspose-cells-net/)
- [Copy Data in Excel Using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)
- [How to Import DataTable into Excel Using Aspose.Cells for .NET (Step-by-Step Guide)](/cells/english/net/import-export/import-datatable-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}