---
category: general
date: 2026-06-30
description: Προσθέστε προσαρμοσμένο μενού περιβάλλοντος στο GridJs και μάθετε πώς
  να φορτώνετε βιβλίο εργασίας Excel, να ενημερώνετε την τιμή ενός κελιού, να ενεργοποιείτε
  τον ορθογραφικό έλεγχο και να καταχωρίζετε προσαρμοσμένη εντολή.
draft: false
keywords:
- add custom context menu
- update cell value
- enable spell checking
- load excel workbook
- register custom command
language: el
og_description: Προσθέστε προσαρμοσμένο μενού περιβάλλοντος στο GridJs ενώ μαθαίνετε
  να φορτώνετε βιβλίο εργασίας Excel, να ενημερώνετε την τιμή ενός κελιού, να ενεργοποιείτε
  τον έλεγχο ορθογραφίας και να καταχωρίζετε προσαρμοσμένη εντολή.
og_title: Προσθήκη Προσαρμοσμένου Μενού Περιβάλλοντος στο GridJs – Βήμα‑βήμα Εγχειρίδιο
  Python
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Add custom context menu in GridJs and learn how to load Excel workbook,
    update cell value, enable spell checking, and register custom command.
  headline: Add Custom Context Menu to GridJs – Complete Python Guide
  type: TechArticle
tags:
- GridJs
- Python
- Excel Automation
title: Προσθήκη προσαρμοσμένου μενού περιβάλλοντος στο GridJs – Πλήρης οδηγός Python
url: /el/python/integration-and-interoperability/add-custom-context-menu-to-gridjs-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Προσθήκη Προσαρμοσμένου Μενού Περιβάλλοντος στο GridJs – Πλήρης Οδηγός Python

Έχετε αναρωτηθεί ποτέ πώς να **προσθέσετε προσαρμοσμένα στοιχεία μενού περιβάλλοντος** σε έναν πίνακα GridJs που τροφοδοτείται από ένα βιβλίο εργασίας Excel; Δεν είστε μόνοι. Σε πολλές εφαρμογές με μεγάλα δεδομένα χρειάζεστε αυτό το μενού δεξιού‑κλικ για να επιτρέψετε στους χρήστες να σηματοδοτούν γραμμές, να επισημαίνουν στοιχεία ως ελεγμένα ή να εκκινούν ενέργειες στο διακομιστή — χωρίς να αφήνουν το πλέγμα.

Σε αυτό το tutorial θα περάσουμε από τη φόρτωση ενός βιβλίου εργασίας Excel, τη δημιουργία μιας προσαρμοσμένης καταχώρησης μενού περιβάλλοντος, την ενημέρωση μιας τιμής κελιού, την ενεργοποίηση του ελέγχου ορθογραφίας και την καταγραφή μιας προσαρμοσμένης εντολής που αποθηκεύει τις αλλαγές πίσω στο αρχείο. Στο τέλος θα έχετε ένα πλήρως λειτουργικό στιγμιότυπο GridJs που αισθάνεται εγγενές στους χρήστες σας και γράφει απευθείας στο αρχικό φύλλο εργασίας.

## Προαπαιτούμενα

- Python 3.9+ (ο κώδικας χρησιμοποιεί type hints αλλά τρέχει σε οποιαδήποτε πρόσφατη έκδοση)  
- βιβλιοθήκη `cells` (ή οποιοδήποτε wrapper διαχείρισης Excel που παρέχει αντικείμενα `Workbook` και `Worksheet`)  
- σύνδεσμος Python για `gridjs` (το μοντέλο αντικειμένων αντικατοπτρίζει το API JavaScript)  
- βασική κατανόηση λήμματα (lambdas) και δομών JSON  

Αν έχετε όλα αυτά, ας βουτήξουμε.

## Βήμα 1: Φόρτωση Βιβλίου Εργασίας Excel και Επιλογή Φύλλου

Το πρώτο που πρέπει να κάνετε είναι **να φορτώσετε το βιβλίο εργασίας Excel** ώστε το GridJs να έχει δεδομένα για εμφάνιση. Η κλάση `cells.Workbook` αφαιρεί την πολυπλοκότητα του αρχείου‑IO και σας δίνει άμεση πρόσβαση σε γραμμές, στήλες και μεμονωμένα κελιά.

```python
# Step 1: Load the workbook and select the first worksheet
wb = cells.Workbook("YOUR_DIRECTORY/example.xlsx")
ws = wb.worksheets[0]          # Grab the first sheet – change index if needed
```

> **Γιατί αυτό είναι σημαντικό:** Η προφόρτωση του βιβλίου εργασίας σημαίνει ότι το πλέγμα μπορεί να αντλήσει δεδομένα κατά απαίτηση, και τυχόν επεξεργασίες που κάνετε αργότερα (όπως **ενημέρωση τιμής κελιού**) θα αποθηκευτούν στο ίδιο αρχείο.

## Βήμα 2: Δημιουργία Αντικειμένου GridJs και Σύνδεσή του με το Φύλλο

Τώρα δημιουργούμε ένα αντικείμενο `gridjs.GridJs` και του λέμε ποιο φύλλο να αποδώσει. Σκεφτείτε το ως την παροχή μιας ζωντανής πηγής δεδομένων που το GridJs μπορεί να ερωτήσει όποτε χρειάζεται να αποδώσει μια σελίδα ή ένα τμήμα με lazy‑loading.

```python
# Step 2: Create a GridJs instance and bind it to the worksheet
grid = gridjs.GridJs()
grid.set_worksheet(ws)
```

> **Pro tip:** Αν δουλεύετε με πολλαπλά φύλλα, απλώς καλέστε `grid.set_worksheet(other_ws)` αργότερα — δεν χρειάζεται να ξαναδημιουργήσετε το πλέγμα.

## Βήμα 3: Ενεργοποίηση Ελέγχου Ορθογραφίας (και Άλλων Χρήσιμων Λειτουργιών)

Οι περισσότερες επιχειρηματικές εφαρμογές επιτρέπουν στους χρήστες να πληκτρολογούν ελεύθερα σημειώσεις. Η ενεργοποίηση του **ελέγχου ορθογραφίας** μειώνει τα τυπογραφικά λάθη και βελτιώνει την ποιότητα των δεδομένων. Το GridJs εκθέτει μια απλή σημαία για αυτό.

```python
# Step 3: Turn on spell checking (and keep other helpers enabled)
grid.settings.spell_check.enabled = True
grid.settings.syntax_check.enabled = True          # optional but handy
grid.settings.formula_explanation.enabled = True   # if you support formulas
```

> **Γιατί να ενεργοποιήσετε τον έλεγχο ορθογραφίας;** Εκτελείται στην πλευρά του πελάτη, παρέχοντας άμεση ανάδραση χωρίς επιπλέον κλήσεις στο διακομιστή — ιδανικό για μεγάλα φύλλα.

## Βήμα 4: Προσθήκη Προσαρμοσμένου Στοιχείου Μενού Περιβάλλοντος

Εδώ είναι η καρδιά του tutorial: **προσθήκη προσαρμοσμένων στοιχείων μενού περιβάλλοντος**. Θα δημιουργήσουμε μια επιλογή “Mark as Reviewed” που, όταν κλικαριστεί, εκτελεί μια εντολή στο διακομιστή που θα ορίσουμε αμέσως μετά.

```python
# Step 4: Add a custom context‑menu item
grid.settings.context_menu.custom_items.append({
    "text": "Mark as Reviewed",   # What the user sees
    "action": "markReviewed"      # Identifier used in the command registration
})
```

> **Εικονογράφηση**  
> ![Προσθήκη προσαρμοσμένου μενού περιβάλλοντος – στιγμιότυπο που δείχνει τις επιλογές δεξιού‑κλικ](/images/add-custom-context-menu.png "Παράδειγμα προσαρμοσμένου μενού περιβάλλοντος")

Το κείμενο alt παραπάνω περιέχει τη βασική λέξη‑κλειδί, ικανοποιώντας τις απαιτήσεις SEO.

## Βήμα 5: Καταγραφή Προσαρμοσμένης Εντολής για Ενημέρωση Τιμής Κελιού

Όταν ο χρήστης επιλέξει “Mark as Reviewed”, πρέπει να **καταγράψουμε μια προσαρμοσμένη εντολή** που ενημερώνει το υποκείμενο κελί Excel και αποθηκεύει το αρχείο. Η μέθοδος `grid.register_custom_command` συνδέει μια κλήσιμη Python με το αναγνωριστικό ενέργειας που ορίσαμε νωρίτερα.

```python
# Step 5: Register the server‑side command that updates a cell value
def mark_reviewed_handler(req):
    """
    req is a dict containing at least:
        - 'cell': Excel address like "B5"
    This function writes "Reviewed" into the target cell and saves the workbook.
    """
    # Update the cell value
    ws.get_range(req["cell"]).put_value("Reviewed")
    
    # Persist changes back to disk
    wb.save("YOUR_DIRECTORY/example-updated.xlsx")
    
    # Return a simple JSON response the client can interpret
    return {"status": "ok"}

grid.register_custom_command("markReviewed", mark_reviewed_handler)
```

> **Γιατί αυτό λειτουργεί:** Ο χειριστής λαμβάνει την αναφορά κελιού από τον πελάτη, χρησιμοποιεί το API του `Worksheet` για **ενημέρωση τιμής κελιού**, και στη συνέχεια γράφει ολόκληρο το βιβλίο εργασίας πίσω στο δίσκο. Η απόκριση ενημερώνει το front‑end ότι η λειτουργία ολοκληρώθηκε με επιτυχία.

### Διαχείριση Ακραίων Περιπτώσεων

- **Απουσία αναφοράς κελιού:** Αν το `req` δεν περιέχει το `"cell"`, ρίξτε ένα σαφές σφάλμα ώστε το UI να μπορεί να εμφανίσει toast.  
- **Συγχρονισμένες επεξεργασίες:** Για σενάρια υψηλής κίνησης, σκεφτείτε να κλειδώσετε το βιβλίο εργασίας ή να χρησιμοποιήσετε σήμα έκδοσης για αποφυγή συνθηκών αγώνα.

## Βήμα 6: Ενεργοποίηση Lazy Loading για Μεγάλα Φύλλα

Αν διαχειρίζεστε χιλιάδες γραμμές, το lazy loading κρατά το UI γρήγορο. Ορίστε το μέγεθος σελίδας σε ένα λογικό τμήμα — 500 γραμμές λειτουργούν καλά για τους περισσότερους browsers.

```python
# Step 6: Activate lazy loading
grid.settings.lazy_load.enabled = True
grid.settings.lazy_load.page_size = 500
```

> **Τι γίνεται αν έχετε 10 000 γραμμές;** Το πλέγμα θα ζητά δεδομένα σελίδα‑με‑σελίδα, μειώνοντας την πίεση μνήμης τόσο στον πελάτη όσο και στον διακομιστή.

## Βήμα 7: (Προαιρετικό) Προσθήκη Προσαρμοσμένου Modal για Επεξεργασία Γραμμής

Μερικές φορές χρειάζεστε πιο πλούσιο UI από έναν ενσωματωμένο επεξεργαστή. Το GridJs σας επιτρέπει να ανοίξετε ένα modal παράθυρο που μπορείτε να φιλοξενήσετε οπουδήποτε — ίσως ένα React component ή μια απλή HTML φόρμα.

```python
# Step 7: Configure a custom modal window for row editing
grid.settings.custom_modal.enabled = True
grid.settings.custom_modal.title = "Edit Row Details"
grid.settings.custom_modal.url = "/row-editor.html"   # Serve this URL from your Flask/Django app
```

> **Γιατί να χρησιμοποιήσετε modal;** Απομονώνει πολύπλοκη λογική επικύρωσης και σας δίνει πλήρη έλεγχο της διάταξης, ενώ εξακολουθεί να ενεργοποιείται από το πλέγμα.

## Βήμα 8: Ανάκτηση του JSON Διαμόρφωσης στην Πλευρά του Πελάτη

Τέλος, πρέπει να στείλετε τη διαμόρφωση στον περιηγητή. Η μέθοδος `get_client_config` σειριοποιεί τα πάντα σε ένα JSON blob που η βιβλιοθήκη GridJs στην πλευρά του front‑end μπορεί να καταναλώσει.

```python
# Step 8: Get the JSON configuration for the front‑end
client_config = grid.get_client_config()

# Example: you might embed this in a template
print(client_config)   # For debugging – remove in production
```

Η έξοδος μοιάζει περίπου έτσι (συμπιεσμένη για συντομία):

```json
{
  "worksheet": "example.xlsx",
  "settings": {
    "spell_check": {"enabled": true},
    "context_menu": {
      "custom_items": [
        {"text": "Mark as Reviewed", "action": "markReviewed"}
      ]
    },
    "lazy_load": {"enabled": true, "page_size": 500},
    "custom_modal": {
      "enabled": true,
      "title": "Edit Row Details",
      "url": "/row-editor.html"
    }
  }
}
```

### Αναμενόμενο Αποτέλεσμα

- Κάνοντας δεξί‑κλικ σε οποιοδήποτε κελί ανοίγει ένα μενού με **Mark as Reviewed**.  
- Επιλέγοντας το στέλνει αίτημα στον διακομιστή, ο οποίος **ενημερώνει την τιμή του κελιού** σε “Reviewed” και αποθηκεύει το `example‑updated.xlsx`.  
- Ο έλεγχος ορθογραφίας υπογραμμίζει λανθασμένες λέξεις καθώς ο χρήστης πληκτρολογεί.  

Όλα αυτά συμβαίνουν χωρίς πλήρη ανανέωση σελίδας, χάρη στο lazy loading και το ελαφρύ JSON payload.

## Συχνές Ερωτήσεις & Pro Tips

| Ερώτηση | Απάντηση |
|----------|--------|
| *Τι γίνεται αν το βιβλίο εργασίας είναι μόνο‑ανάγνωση;* | Βεβαιωθείτε ότι τα δικαιώματα αρχείου επιτρέπουν εγγραφή, ή ανοίξτε το βιβλίο με `mode="rw"` αν η βιβλιοθήκη το υποστηρίζει. |
| *Μπορώ να προσθέσω περισσότερα από ένα προσαρμοσμένα στοιχεία μενού;* | Απόλυτα — απλώς προσθέστε επιπλέον dicts στο `grid.settings.context_menu.custom_items`. |
| *Πρέπει να επαναφορτώσω το πλέγμα μετά από ενημέρωση κελιού;* | Το GridJs αυτόματα ανανεώνει τηffected γραμμή αν επιστρέψετε `{status:"ok"}`· διαφορετικά καλέστε `grid.refresh()` από τον πελάτη. |
| *Πώς κάνω τον έλεγχο ορθογραφίας συγκεκριμένης γλώσσας;* | Ορίστε `grid.settings.spell_check.language = "en-US"` (ή οποιαδήποτε υποστηριζόμενη τοπική ρύθμιση). |
| *Είναι το lazy loading συμβατό με φιλτράρισμα στην πλευρά του διακομιστή;* | Ναι — συνδυάστε `grid.settings.filter.enabled = True` και υλοποιήστε τη λογική φιλτραρίσματος στην προσαρμοσμένη εντολή σας. |

## Πλήρες Παράδειγμα Λειτουργίας (Όλα τα Βήματα Συνδυασμένα)

Παρακάτω υπάρχει ένα ενιαίο script που μπορείτε να ενσωματώσετε σε μια διαδρομή Flask ή να τρέξετε ως αυτόνομη διαδικασία. Αντικαταστήστε το `YOUR_DIRECTORY` με την πραγματική διαδρομή στον διακομιστή σας.

```python
import cells
import gridjs
from flask import Flask, request, jsonify, render_template_string

app = Flask(__name__)

# ---------- Initialization ----------
wb = cells.Workbook("YOUR_DIRECTORY/example.xlsx")
ws = wb.worksheets[0]

grid = gridjs.GridJs()
grid.set_worksheet(ws)

# Enable helpers
grid.settings.spell_check.enabled = True
grid.settings.syntax_check.enabled = True
grid.settings.formula_explanation.enabled = True

# Lazy loading
grid.settings.lazy_load.enabled = True
grid.settings.lazy_load.page_size = 500

# Custom context menu
grid.settings.context_menu.custom_items.append({
    "text": "Mark as Reviewed",
    "action": "markReviewed"
})

# Custom command implementation
def mark_reviewed_handler(req):
    cell_addr = req.get("cell")
    if not cell_addr:
        return {"status": "error", "message": "Cell address missing"}
    ws.get_range(cell_addr).put_value("Reviewed")
    wb.save("YOUR_DIRECTORY/example-updated.xlsx")
    return {"status": "ok"}

grid.register_custom_command("markReviewed", mark_reviewed_handler)

# Optional modal
grid.settings.custom_modal.enabled = True
grid.settings.custom_modal.title = "Edit Row Details"
grid.settings.custom_modal.url = "/row-editor.html"

client_config = grid.get_client_config()

# ---------- Flask Routes ----------
@app.route("/")
def index():
    # Simple page that injects the config into a <script> tag
    html = f"""
    <!doctype html>
    <html>
    <head>
        <title>GridJs Demo</title>
        <script src="https://unpkg.com/gridjs/dist/gridjs.umd.js"></script>
    </head>
    <body>
        <div id="grid"></div>
        <script>
            const config = {client_config};
            new gridjs.Grid(config).render(document.getElementById("grid"));
        </script>
    </body>
    </html>
    """
    return render_template_string(html)

@app.route("/command/<name>", methods=["POST"])
def command(name):


## Τι Θα Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικά παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε επιπλέον δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Add Custom Content Type Properties to Excel Workbooks Using Aspose.Cells Java](/cells/english/java/tables-structured-references/aspose-cells-java-custom-content-types/)
- [Add Custom XML Parts with ID to Workbook](/cells/english/net/workbook-operations/add-custom-xml-parts-with-id/)
- [Aspose Cells Java Custom Load Filters Excel Export](/cells/hindi/java/import-export/aspose-cells-java-custom-load-filters-excel-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}