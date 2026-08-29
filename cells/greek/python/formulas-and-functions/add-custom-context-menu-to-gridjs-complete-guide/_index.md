---
category: general
date: 2026-06-08
description: Προσθέστε προσαρμοσμένο μενού περιβάλλοντος στο GridJs και εξάγετε το
  πλέγμα σε CSV με ένα blob αρχείου CSV για λήψη. Ακολουθήστε αυτόν τον βήμα‑βήμα
  οδηγό για ένα πλήρως λειτουργικό παράδειγμα.
draft: false
keywords:
- add custom context menu
- export grid to csv
- download csv file blob
- GridJs context menu
- Flask CSV export
language: el
og_description: Προσθέστε προσαρμοσμένο μενού περιβάλλοντος στο GridJs και εξαγάγετε
  το πλέγμα σε CSV με ένα blob αρχείου CSV για λήψη. Μάθετε την πλήρη υλοποίηση σε
  λιγότερο από 10 λεπτά.
og_title: Προσθήκη προσαρμοσμένου μενού περιβάλλοντος στο GridJs – Πλήρης οδηγός
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Add custom context menu to GridJs and export grid to CSV with a download
    CSV file blob. Follow this step‑by‑step tutorial for a fully working example.
  headline: Add Custom Context Menu to GridJs – Complete Guide
  type: TechArticle
tags:
- GridJs
- JavaScript
- Python
- Flask
title: Προσθήκη Προσαρμοσμένου Μενού Περιβάλλοντος στο GridJs – Πλήρης Οδηγός
url: /el/python/formulas-and-functions/add-custom-context-menu-to-gridjs-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Προσθήκη Προσαρμοσμένου Μενού Περιβάλλοντος σε GridJs – Πλήρης Οδηγός

Θέλετε να **προσθέσετε προσαρμοσμένο μενού περιβάλλοντος** σε ένα στοιχείο GridJs; Σε αυτόν τον οδηγό θα σας καθοδηγήσουμε βήμα προς βήμα και θα σας δείξουμε πώς να **εξάγετε το πλέγμα σε CSV** χρησιμοποιώντας ένα **download CSV file blob**. Είτε δημιουργείτε ένα γρήγορο πίνακα διαχείρισης είτε ένα πλήρες ταμπλό αναφορών, ένα μενού δεξί‑κλικ που επιτρέπει στους χρήστες να εξάγουν δεδομένα ως CSV μπορεί να αυξήσει πραγματικά την παραγωγικότητα.

Θα καλύψουμε όλα όσα χρειάζεστε: την πλευρά Python με Flask, τον JavaScript χειριστή που δημιουργεί το Blob, και το HTML/JS που παράγει το GridJs. Στο τέλος θα έχετε ένα αυτόνομο παράδειγμα που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο.

---

## Τι Θα Χρειαστεί

- **Python 3.9+** και **Flask** εγκατεστημένα (`pip install flask`).
- Το **gridjs** Python wrapper (ή η βιβλιοθήκη JavaScript απευθείας) – για αυτόν τον οδηγό θα υποθέσουμε ένα ελαφρύ Python wrapper που αντικατοπτρίζει το JavaScript API.
- Βασική κατανόηση του **async JavaScript** (`fetch`, `Promise`) – αλλά μην ανησυχείτε, θα εξηγήσουμε κάθε γραμμή.
- Ένας επεξεργαστής που σας αρέσει (VS Code, PyCharm, ή ακόμη και ένας απλός επεξεργαστής κειμένου).

Αυτό είναι όλο. Χωρίς επιπλέον εργαλεία front‑end, χωρίς χορό με Node npm. Απλώς απλό Flask που σερβίρει το HTML που δημιουργεί το GridJs.

---

## Προσθήκη Προσαρμοσμένου Μενού Περιβάλλοντος σε GridJs

Το πρώτο που πρέπει να κάνετε είναι να ενημερώσετε το GridJs ότι θέλετε ένα προσαρμοσμένο μενού δεξί‑κλικ. Από προεπιλογή, το GridJs παρέχει ένα ελάχιστο σύνολο (copy, paste, κλπ.), αλλά μπορείτε να το αντικαταστήσετε εντελώς.

```python
# Step 1: Create a new workbook that will be displayed in the grid
workbook = Workbook()

# Step 2: Initialise the GridJs component with the workbook
grid_js = GridJs(workbook)

# Step 3: Define a custom context‑menu that includes an "Export CSV" command
grid_js.CustomContextMenu = ["Copy", "Paste", "Export CSV"]
```

**Γιατί είναι σημαντικό:**  
Η ρύθμιση του `CustomContextMenu` αντικαθιστά τη λίστα προεπιλογής με αυτήν που παρέχετε. Η συμβολοσειρά `"Export CSV"` είναι απλώς μια ετικέτα – η πραγματική εργασία συμβαίνει όταν ο χρήστης κάνει κλικ, κάτι που θα συνδέσουμε στο επόμενο βήμα.

> *Συμβουλή:* Κρατήστε τη λίστα σύντομη. Ένα ακατάστατο μενού περιβάλλοντος αναιρεί τον σκοπό των γρήγορων ενεργειών.

---

## Εξαγωγή Πλέγματος σε CSV με Λήψη Blob

Τώρα που υπάρχει το στοιχείο του μενού, χρειαζόμαστε έναν JavaScript χειριστή που θα επικοινωνεί με τον διακομιστή, θα φέρνει το CSV, θα το μετατρέπει σε **Blob** και θα επιβάλλει λήψη. Εδώ εμφανίζεται η φράση **download CSV file blob**.

```python
# Step 4: Attach a JavaScript handler that runs when "Export CSV" is chosen.
#         The handler sends an AJAX request to a server endpoint,
#         receives the CSV file as a Blob, and triggers a download.
grid_js.CustomContextMenuHandler = """
function(action, cell) {
    if (action === "Export CSV") {
        fetch('/export/csv?sheet=' + cell.sheetName)
            .then(r => r.blob())
            .then(b => {
                const url = URL.createObjectURL(b);
                const a = document.createElement('a');
                a.href = url;
                a.download = cell.sheetName + ".csv";
                a.click();
            });
    }
}
"""
```

### Ανάλυση του Χειριστή

| Γραμμή | Τι Κάνει |
|------|--------------|
| `fetch('/export/csv?sheet=' + cell.sheetName)` | Καλεί μια διαδρομή Flask (`/export/csv`) περνώντας το όνομα του φύλλου ως query string. |
| `.then(r => r.blob())` | Μετατρέπει την HTTP απόκριση σε **Blob** – ουσιαστικά ένα δυαδικό κοντέινερ για τα δεδομένα CSV. |
| `URL.createObjectURL(b)` | Δημιουργεί ένα προσωρινό URL που το πρόγραμμα περιήγησης μπορεί να αντιμετωπίσει ως αρχείο. |
| `a.download = cell.sheetName + ".csv"` | Ορίζει το όνομα αρχείου που θα δει ο χρήστης στο παράθυρο διαλόγου λήψης. |
| `a.click()` | Προγραμματιστικά κάνει κλικ στο κρυφό anchor, προκαλώντας το πρόγραμμα περιήγησης να κατεβάσει το Blob. |

> **Γιατί να χρησιμοποιήσετε ένα Blob;**  
> Τα προγράμματα περιήγησης δεν μπορούν να κατεβάσουν απευθείας ακατέργαστο κείμενο που επιστρέφεται από το `fetch` χωρίς να το μετατρέψουν σε κάτι παρόμοιο με αρχείο. Η τεχνική Blob‑URL είναι ο πιο αξιόπιστος, διαπλατφορμικός τρόπος για να ενεργοποιήσετε ένα **download CSV file blob** χωρίς να ανανεώσετε τη σελίδα.

---

## Ρύθμιση του Backend Flask

Ο χειριστής front‑end αναμένει ένα endpoint στο `/export/csv`. Ακολουθεί μια ελάχιστη προβολή Flask που λαμβάνει το όνομα του φύλλου, εξάγει δεδομένα από το βιβλίο εργασίας και επιστρέφει ένα CSV.

```python
from flask import Flask, request, Response
import csv
import io

app = Flask(__name__)

# Assume `workbook` is a global object we created earlier
# (in a real app you’d probably fetch it from a database or session)
@app.route('/export/csv')
def export_csv():
    sheet_name = request.args.get('sheet', 'default')
    # Retrieve the sheet data – this is pseudo‑code; replace with your actual API
    sheet = workbook.get_sheet(sheet_name)

    # Convert rows to CSV in memory
    output = io.StringIO()
    writer = csv.writer(output)
    writer.writerow(sheet.headers)          # Header row
    writer.writerows(sheet.rows)            # Data rows

    # Create a Flask response with the correct MIME type
    csv_bytes = output.getvalue().encode('utf-8')
    return Response(
        csv_bytes,
        mimetype='text/csv',
        headers={'Content-Disposition': f'attachment;filename={sheet_name}.csv'}
    )
```

### Κύρια Σημεία

- **`io.StringIO`** μας επιτρέπει να δημιουργήσουμε το CSV στη μνήμη χωρίς να αγγίσουμε το σύστημα αρχείων.
- **`Content‑Disposition`** ενημερώνει το πρόγραμμα περιήγησης ότι το αρχείο είναι συνημμένο και προτείνει ένα όνομα αρχείου. Παρόλο που το front‑end επίσης ορίζει `a.download`, η παρουσία του στην πλευρά του διακομιστή παρέχει εναλλακτική λύση για πελάτες χωρίς JS.
- Η διαδρομή είναι σκόπιμα απλή· μπορείτε αργότερα να προσθέσετε έλεγχο ταυτοποίησης, ελέγχους δικαιωμάτων ή streaming για τεράστια σύνολα δεδομένων.

---

## Απόδοση του Πλέγματος στον Πελάτη

Με το μενού περιβάλλοντος και το backend έτοιμα, το τελευταίο κομμάτι είναι να αποδώσετε το στοιχείο GridJs και να στείλετε το HTML/JS στον περιηγητή.

```python
# Step 5: Render the grid to obtain the full HTML/JS needed on the client side
html_output = grid_js.Render()
print(html_output)   # Sends the HTML/JS to the client (e.g., in a Flask view)
```

Σε μια προβολή Flask συνήθως θα κάνετε:

```python
@app.route('/')
def index():
    html_output = grid_js.Render()
    return f"""
    <!doctype html>
    <html>
    <head>
        <title>Grid with Custom Context Menu</title>
        <script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
        <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet" />
    </head>
    <body>
        {html_output}
    </body>
    </html>
    """
```

Όταν η σελίδα φορτώνει, το GridJs δημιουργεί τον πίνακα, ενσωματώνει το προσαρμοσμένο μενού περιβάλλοντος, και ο JavaScript χειριστής που ορίσαμε νωρίτερα είναι έτοιμος να ενεργοποιηθεί. Κάντε δεξί‑κλικ σε οποιοδήποτε κελί, επιλέξτε **Export CSV**, και παρακολουθήστε το πρόγραμμα περιήγησης να κατεβάσει ένα αρχείο με όνομα το ίδιο με το φύλλο.

---

## Πλήρες Παράδειγμα Εργασίας (Όλα τα Αρχεία)

Παρακάτω είναι ο πλήρης, εκτελέσιμος κώδικας που μπορείτε να αντιγράψετε‑επικολλήσετε σε ένα νέο φάκελο. Εγκαταστήστε το Flask (`pip install flask`) και τρέξτε `python app.py`.

**`app.py`**

```python
from flask import Flask, request, Response
import csv, io

# Mock classes to simulate the GridJs wrapper – replace with the real library
class Workbook:
    def __init__(self):
        self.sheets = {"Sheet1": Sheet()}
    def get_sheet(self, name):
        return self.sheets.get(name, self.sheets["Sheet1"])

class Sheet:
    def __init__(self):
        self.headers = ["ID", "Name", "Score"]
        self.rows = [
            [1, "Alice", 85],
            [2, "Bob", 92],
            [3, "Charlie", 78],
        ]

class GridJs:
    def __init__(self, workbook):
        self.workbook = workbook
        self.CustomContextMenu = []
        self.CustomContextMenuHandler = ""
    def Render(self):
        # Very simplified HTML – real GridJs would generate a lot more
        return f'''
        <div id="grid"></div>
        <script>
            const grid = new gridjs.Grid({{
                columns: {self.workbook.get_sheet("Sheet1").headers},
                data: {self.workbook.get_sheet("Sheet1").rows},
                search: true,
                pagination: true,
                customContextMenu: {self.CustomContextMenu},
                customContextMenuHandler: {self.CustomContextMenuHandler}
            }}).render(document.getElementById("grid"));
        </script>
        '''

app = Flask(__name__)

# Initialise workbook and grid
workbook = Workbook()
grid_js = GridJs(workbook)

# ==== Step 3: Custom context menu ====
grid_js.CustomContextMenu = ["Copy", "Paste", "Export CSV"]

# ==== Step 4: Handler that downloads a CSV blob ====
grid_js.CustomContextMenuHandler = """
function(action, cell) {
    if (action === "Export CSV") {
        fetch('/export/csv?sheet=' + cell.sheetName)
            .then(r => r.blob())
            .then(b => {
                const url = URL.createObjectURL(b);
                const a = document.createElement('a');
                a.href = url;
                a.download = cell.sheetName + ".csv";
                a.click();
            });
    }
}
"""

@app.route('/')
def index():
    html_output = grid_js.Render()
    return f'''
    <!doctype html>
    <html>
    <head>
'''

## Τι Θα Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετικά θέματα που βασίζονται στις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Φόρτωση Αρχείων CSV με Προσαρμοσμένους Αναλυτές Aspose Cells Java](/cells/hindi/java/import-export/load-csv-files-custom-parsers-aspose-cells-java/)
- [Εξαγωγή CSV Java Κώδικας](/cells/hindi/java/excel-import-export/csv-export-java-code/)
- [Εξαγωγή Excel CSV Κενές Γραμμές Aspose Cells Net](/cells/hindi/net/workbook-operations/export-excel-csv-blank-rows-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}