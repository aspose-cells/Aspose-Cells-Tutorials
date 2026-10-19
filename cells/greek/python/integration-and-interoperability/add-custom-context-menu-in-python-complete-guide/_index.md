---
category: general
date: 2026-06-30
description: Προσθέστε προσαρμοσμένο μενού περιβάλλοντος σε ένα πλέγμα Excel σε Python
  και γράψτε τιμή σε κελί Excel ενώ αποθηκεύετε το ενημερωμένο αρχείο. Μάθετε πώς
  να δημιουργήσετε μενού δεξί κλικ και να ενημερώσετε την τιμή του κελιού με στυλ
  Python.
draft: false
keywords:
- add custom context menu
- write value to excel cell
- create right‑click menu
- update cell value python
- save updated excel file
language: el
og_description: Προσθέστε προσαρμοσμένο μενού περιβάλλοντος στο Python για να γράψετε
  τιμή σε κελί Excel και να αποθηκεύσετε το ενημερωμένο αρχείο Excel. Αυτός ο οδηγός
  σας καθοδηγεί στη δημιουργία μενού δεξί κλικ με το GridJs.
og_title: Προσθήκη προσαρμοσμένου μενού περιβάλλοντος στο Python – Βήμα‑βήμα οδηγός
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Add custom context menu to a Python Excel grid and write value to excel
    cell while saving the updated file. Learn to create right‑click menu and update
    cell value python style.
  headline: Add Custom Context Menu in Python – Complete Guide
  type: TechArticle
tags:
- Python
- Excel Automation
- GridJs
- Context Menu
title: Προσθήκη Προσαρμοσμένου Μενού Περιβάλλοντος στην Python – Πλήρης Οδηγός
url: /el/python/integration-and-interoperability/add-custom-context-menu-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Προσθήκη Προσαρμοσμένου Μενού Περιβάλλοντος σε Python – Πλήρης Οδηγός

Έχετε αναρωτηθεί ποτέ πώς να **προσθέσετε προσαρμοσμένα στοιχεία μενού περιβάλλοντος** σε ένα πλέγμα υπολογιστικού φύλλου που εξυπηρετείτε από Python; Ίσως χρειάζεστε ένα γρήγορο κουμπί “Σήμανση ως Ελεγμένο” που εμφανίζεται όταν ο χρήστης κάνει δεξί‑κλικ σε ένα κελί, γράφει μια τιμή στο κελί του Excel και στη συνέχεια αποθηκεύει το ενημερωμένο βιβλίο εργασίας—όλα χωρίς να εγκαταλείψετε το web UI.  

Σε αυτό το tutorial θα δημιουργήσουμε ακριβώς αυτό: ένα **προσαρμοσμένο μενού δεξιού‑κλικ** με τη βοήθεια του GridJs, έναν server‑side handler που **γράφει τιμή σε κελί excel**, και ένα τελικό βήμα που **αποθηκεύει το ενημερωμένο αρχείο excel** στο δίσκο. Στο τέλος θα έχετε ένα επαναχρησιμοποιήσιμο μοτίβο που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο Flask, FastAPI ή Django.

> **Γιατί να το κάνετε;**  
> Η προσθήκη προσαρμοσμένου μενού περιβάλλοντος απλοποιεί τις ροές εργασίας ελέγχου δεδομένων, μειώνει την ανάγκη για χειροκίνητη αντιγραφή‑επικόλληση και προσφέρει στους τελικούς χρήστες μια εμπειρία “φυσική” μέσα στο πλέγμα. Επιπλέον, θα δείτε πώς να **ενημερώνετε τιμή κελιού σε στυλ python**, μια βασική δεξιότητα για κάθε εργασία αυτοματοποίησης Excel.

## Προαπαιτούμενα

- Python 3.9+ (ο κώδικας λειτουργεί και σε 3.10)  
- `openpyxl` για διαχείριση αρχείων Excel  
- `gridjs` Python wrapper (ή η βιβλιοθήκη JS αν προτιμάτε το front‑end)  
- Ένα βασικό web framework (παράδειγμα με Flask)  
- Ένα αρχείο βιβλίου εργασίας με όνομα `sample.xlsx` στον φάκελο του έργου σας  

Αν λείπει κάποιο από αυτά, τρέξτε:

```bash
pip install openpyxl flask gridjs
```

Τώρα ας βουτήξουμε.

---

## Βήμα 1 – Προσθήκη Προσαρμοσμένου Μενού Περιβάλλοντος: Αρχικοποίηση GridJs και Σύνδεση Φύλλου Εργασίας

Το πρώτο πράγμα που πρέπει να κάνετε είναι να δημιουργήσετε ένα στιγμιότυπο `GridJs` και να το συνδέσετε με το φύλλο εργασίας που σκοπεύετε να χρησιμοποιήσετε. Εδώ εμφανίζεται για πρώτη φορά η φράση **add custom context menu** στον κώδικά μας, και θέτει τις βάσεις για όλα τα επόμενα.

```python
# step_1_initialize.py
import openpyxl
from gridjs import GridJs

# Load the workbook – this could be any .xlsx file you own
wb = openpyxl.load_workbook("sample.xlsx")
ws = wb["Sheet1"]                     # Grab the sheet you’ll display

# Create the GridJs object and bind it to the worksheet
grid = GridJs()
grid.set_worksheet(ws)                # <-- add custom context menu works on this sheet
```

**Τι συμβαίνει;**  
`grid.set_worksheet(ws)` λέει στο GridJs να χρησιμοποιήσει τα δεδομένα από το `ws` ως πηγή δεδομένων. Από εδώ και πέρα, οποιεσδήποτε τροποποιήσεις μενού περιβάλλοντος θα στοχεύουν αυτόματα στο ίδιο φύλλο, διατηρώντας το UI και το αρχείο σε συγχρονισμό.

> **Συμβουλή:** Ανοίξτε το βιβλίο εργασίας σε λειτουργία ανάγνωσης/εγγραφής μόνο μία φορά. Το άνοιγμα επανειλημμένα μέσα σε έναν handler αιτήματος μπορεί να προκαλέσει προβλήματα κλειδώματος αρχείου στα Windows.

---

## Βήμα 2 – Εγγραφή Τιμής σε Κελί Excel: Ορισμός Ενέργειας για το Στοιχείο Μενού

Τώρα που το πλέγμα είναι έτοιμο, πρέπει να **write value to excel cell** όταν ο χρήστης επιλέγει την προσαρμοσμένη εντολή μας. Θα προσθέσουμε μια καταχώρηση μενού με όνομα “Mark as Reviewed” και θα της δώσουμε το αναγνωριστικό `markReviewed`. Το αναγνωριστικό είναι αυτό που θα στείλει η JavaScript πλευρά του client πίσω στον server.

```python
# step_2_menu_item.py
# Append a custom item to the right‑click context menu
grid.settings.context_menu.custom_items.append({
    "text": "Mark as Reviewed",      # Text shown in the UI
    "action": "markReviewed",        # Identifier used on the client side
    "icon": "check_circle"           # Optional Material‑Icons name
})
```

**Γιατί να χρησιμοποιήσετε προσαρμοσμένο αναγνωριστικό;**  
Το αναγνωριστικό αποσυνδέει το κείμενο UI από τη λογική του server, επιτρέποντάς σας να αλλάξετε την ετικέτα χωρίς να τροποποιήσετε τον κώδικα backend. Επίσης, κάνει τη λειτουργία **create right‑click menu** σαφή και επαναχρησιμοποιήσιμη.

---

## Βήμα 3 – Δημιουργία Μενού Δεξιού‑Κλικ: Καταχώρηση Server‑Side Handler

Με το στοιχείο μενού στη θέση του, πρέπει να πούμε στο GridJs τι να κάνει όταν ο χρήστης το πατήσει. Εδώ υλοποιούμε τη λειτουργία **create right‑click menu** που στέλνει πραγματικό αίτημα πίσω στο Python.

```python
# step_3_handler.py
def on_custom_command(request):
    """
    Server‑side handler for the 'markReviewed' custom command.
    It receives a JSON payload like {"cell": "C12"}.
    """
    # Extract the cell address from the incoming request
    cell_address = request["cell"]           # e.g., "C12"

    # Write the word "Reviewed" into that cell
    ws[cell_address] = "Reviewed"            # <-- write value to excel cell

    # Persist the change to disk (see next step)
    # We'll return a simple JSON response to the client
    return {"status": "ok"}
```

Μερικά σημεία που πρέπει να σημειώσετε:

1. **`ws[cell_address] = "Reviewed"`** είναι ο πιο απλός τρόπος να **update cell value python**. Στο παρασκήνιο, το `openpyxl` μετατρέπει τη διεύθυνση στυλ A1 σε δείκτες γραμμής/στήλης.
2. Ο handler επιστρέφει ένα μικρό JSON payload. Το GridJs αναμένει έναν δείκτη κατάστασης· μπορείτε να το επεκτείνετε ώστε να περιλαμβάνει μηνύματα σφάλματος αν χρειαστεί.

Τώρα συνδέουμε το αναγνωριστικό με τον handler:

```python
# step_3_register.py
grid.register_custom_command("markReviewed", on_custom_command)
```

**Τι γίνεται αν το κελί είναι κενό ή προστατευμένο;**  
- Τα κενά κελιά δεν αποτελούν πρόβλημα—το `openpyxl` θα τα δημιουργήσει αυτόματα.  
- Για προστατευμένα φύλλα, πρέπει πρώτα να αφαιρέσετε την προστασία (`ws.protection.sheet = False`) ή να πιάσετε ένα `PermissionError`.

---

## Βήμα 4 – Ενημέρωση Τιμής Κελιού Python: Διατήρηση της Αλλαγής με Αποθήκευση του Βιβλίου Εργασίας

Η εγγραφή μιας τιμής είναι μόνο το ήμισυ της ιστορίας· πρέπει να **save updated excel file** ώστε η αλλαγή να παραμείνει μετά το τρέχον session. Εδώ ολοκληρώνουμε το κύκλο από UI σε δίσκο.

```python
# step_4_save.py
def on_custom_command(request):
    cell_address = request["cell"]
    ws[cell_address] = "Reviewed"

    # Save the workbook to a known location
    wb.save("output/sample-updated.xlsx")   # <-- save updated excel file
    return {"status": "ok"}
```

**Γιατί ξεχωριστός φάκελος;**  
Η αποθήκευση σε φάκελο `output/` διατηρεί το αρχικό πρότυπο άθικτο, κάτι χρήσιμο για ιχνηλασιμότητα. Προσαρμόστε τη διαδρομή ώστε να ταιριάζει με το περιβάλλον ανάπτυξής σας.

> **Προσοχή:** Αν εξυπηρετείτε πολλούς ταυτόχρονους χρήστες, σκεφτείτε τη χρήση κλειδώματος thread‑safe (`threading.Lock`) γύρω από το `wb.save()` για να αποφύγετε συνθήκες αγώνα.

---

## Βήμα 5 – Δημιουργία JSON Ρυθμίσεων Client και Σύνδεση Όλων Μαζί

Τέλος, πρέπει να παραγάγουμε το JSON που θα καταναλώσει το front‑end GridJs. Αυτό το JSON περιέχει τα δεδομένα του φύλλου εργασίας **και** τον ορισμό του προσαρμοσμένου μενού.

```python
# step_5_config.py
config_json = grid.get_client_config()
print(config_json)   # You can pipe this to your template engine
```

Όταν ενσωματώσετε το `config_json` στη σελίδα HTML, το GridJs θα αποδώσει το πλέγμα με την καταχώρηση “Mark as Reviewed” διαθέσιμη σε δεξί‑κλικ σε κάθε κελί.

### Πλήρες Παράδειγμα Flask

Παρακάτω υπάρχει μια ελάχιστη εφαρμογή Flask που ενώνει όλα τα κομμάτια. Τρέξτε την, ανοίξτε `http://localhost:5000` και κάντε δεξί‑κλικ σε οποιοδήποτε κελί για να δείτε το προσαρμοσμένο μενού σε δράση.

```python
# app.py
from flask import Flask, request, jsonify, render_template_string
import openpyxl
from gridjs import GridJs

app = Flask(__name__)

# Load workbook once at startup
wb = openpyxl.load_workbook("sample.xlsx")
ws = wb["Sheet1"]
grid = GridJs()
grid.set_worksheet(ws)

# ---- Add custom context menu item ----
grid.settings.context_menu.custom_items.append({
    "text": "Mark as Reviewed",
    "action": "markReviewed",
    "icon": "check_circle"
})

# ---- Server‑side handler ----
def on_custom_command(req):
    cell = req["cell"]
    ws[cell] = "Reviewed"
    wb.save("output/sample-updated.xlsx")
    return {"status": "ok"}

grid.register_custom_command("markReviewed", on_custom_command)

# ---- Routes ----
@app.route("/")
def index():
    config = grid.get_client_config()
    # Simple inline template; in production use a separate .html file
    html = f"""
    <!doctype html>
    <html>
      <head>
        <script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
        <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet" />
      </head>
      <body>
        <div id="wrapper"></div>
        <script>
          const config = {config};
          new gridjs.Grid(config).render(document.getElementById("wrapper"));
        </script>
      </body>
    </html>
    """
    return render_template_string(html)

@app.route("/custom-command", methods=["POST"])
def custom_command():
    payload = request.get_json()
    result = on_custom_command(payload)
    return jsonify(result)

if __name__ == "__main__":
    app.run(debug=True)
```

**Αναμενόμενο αποτέλεσμα:**  
- Δεξί‑κλικ σε οποιοδήποτε κελί → εμφανίζεται το “Mark as Reviewed”.  
- Κλικ → το περιεχόμενο του κελιού αλλάζει σε “Reviewed”.  
- Το βιβλίο εργασίας `output/sample-updated.xlsx` περιέχει πλέον τη νέα τιμή.

---

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

| Ερώτηση | Απάντηση |
|----------|----------|
| *Τι γίνεται αν χρειαστώ πολλαπλές προσαρμοσμένες ενέργειες;* | Απλώς προσθέστε περισσότερα αντικείμενα στο `grid.settings.context_menu.custom_items` και καταχωρήστε το καθένα με το δικό του αναγνωριστικό. |
| *Μπορώ να περάσω επιπλέον δεδομένα (π.χ. ID γραμμής) στον handler;* | Ναι. Συμπεριλάβετε επιπλέον κλειδιά στο JSON payload από την πλευρά του client, και διαβάστε τα από το `request` στο `on_custom_command`. |
| *Είναι αυτή η προσέγγιση συμβατή με async frameworks;* | Απόλυτα—απλώς κάντε το `on_custom_command` ασύγχρονη συνάρτηση και χρησιμοποιήστε `await wb.save(...)` αν μεταβείτε σε `aiofiles` ή παρόμοιο. |
| *Πώς να στυλιζάρω το εικονίδιο του μενού;* | Δώστε οποιοδήποτε όνομα Material‑Icons (`"icon": "edit"`). Το front‑end φορτώνει αυτόματα τη γραμματοσειρά εικονιδίων. |
| *Τι γίνεται με μεγάλα βιβλία εργασίας;* | Φορτώστε μόνο το απαιτούμενο φύλλο και σκεφτείτε τη ροή σειρών με `openpyxl.iter_rows()` για να περιορίσετε τη χρήση μνήμης. |

## Τι Να Μάθετε Στη Σειρά Επόμενη;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κυριαρχήσετε επιπλέον δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στα δικά σας έργα.

- [Preserve Single Quote Prefix of Cell Value or Range in Excel](/cells/english/net/excel-data-preservation-warning/preserve-single-quote-prefix-of-cell-value-or-range-in-excel/)
- [Preserve Single Quote Prefix Of Cell Value Or Range In Excel](/cells/german/net/excel-data-preservation-warning/preserve-single-quote-prefix-of-cell-value-or-range-in-excel/)
- [Preserve Single Quote Prefix Of Cell Value Or Range In Excel](/cells/french/net/excel-data-preservation-warning/preserve-single-quote-prefix-of-cell-value-or-range-in-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}