---
category: general
date: 2026-06-21
description: Ενεργοποιήστε τον ορθογραφικό έλεγχο κατά την εξαγωγή JSON από το Excel
  χρησιμοποιώντας το GridJs. Μάθετε πώς να μετατρέπετε xlsx σε JSON, να ρυθμίζετε
  τη lazy loading και να φορτώνετε αποδοτικά το βιβλίο εργασίας Excel.
draft: false
keywords:
- enable spell check
- export excel json
- convert xlsx to json
- configure lazy loading
- load excel workbook
language: el
og_description: Ενεργοποιήστε τον ορθογραφικό έλεγχο κατά την εξαγωγή JSON από Excel
  με το GridJs. Αυτός ο οδηγός δείχνει πώς να μετατρέψετε xlsx σε JSON, να διαμορφώσετε
  τη lazy loading και να φορτώσετε ένα βιβλίο εργασίας Excel.
og_title: Ενεργοποίηση ορθογραφικού ελέγχου & εξαγωγή Excel JSON με GridJs
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Enable spell check while you export Excel JSON using GridJs. Learn
    to convert xlsx to JSON, configure lazy loading, and load Excel workbook efficiently.
  headline: Enable Spell Check & Export Excel JSON with GridJs
  type: TechArticle
tags:
- GridJs
- Excel
- JSON
- Python
title: Ενεργοποίηση ορθογραφικού ελέγχου & εξαγωγή Excel JSON με GridJs
url: /el/python/import-and-export/enable-spell-check-export-excel-json-with-gridjs/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ενεργοποίηση Ορθογραφικού Ελέγχου & Εξαγωγή Excel JSON με GridJs

Ποτέ δεν χρειάστηκε να **ενεργοποιήσετε ορθογραφικό έλεγχο** σε μια διεπαφή υπολογιστικού φύλλου βασισμένη στο web και να σκεφτείτε πώς να εξάγετε τα δεδομένα ως JSON ταυτόχρονα; Δεν είστε μόνοι. Πολλοί προγραμματιστές αντιμετωπίζουν το ίδιο πρόβλημα όταν προσπαθούν να **εξάγουν Excel JSON** από ένα βιβλίο εργασίας διατηρώντας ταυτόχρονα προηγμένες λειτουργίες όπως η επικύρωση τύπων.

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από ένα πλήρες, εκτελέσιμο παράδειγμα που δείχνει πώς να **φορτώσετε βιβλίο εργασίας Excel**, να το μετατρέψετε σε JSON payload με GridJs, να **ρυθμίσετε lazy loading**, και φυσικά να **ενεργοποιήσετε ορθογραφικό έλεγχο**. Στο τέλος θα μπορείτε να **μετατρέψετε xlsx σε JSON** με λίγες μόνο γραμμές—χωρίς μυστικά, χωρίς ελλείψεις.

> **Τι θα αποκομίσετε**  
> * Ένα script Python που διαβάζει ένα αρχείο `.xlsx`, δημιουργεί ένα αντικείμενο GridJs server και γράφει `grid_data.json`.  
> * Κατανόηση του γιατί κάθε επιλογή είναι σημαντική (ορθογραφικός έλεγχος, έλεγχος τύπων, lazy loading).  
> * Συμβουλές για κλιμάκωση της λύσης σε μεγαλύτερα βιβλία εργασίας.

---

## Προαπαιτούμενα

Πριν βουτήξουμε, βεβαιωθείτε ότι έχετε τα παρακάτω στη μηχανή σας:

| Απαίτηση | Γιατί είναι σημαντικό |
|----------|------------------------|
| Python 3.9+ | Απαιτείται για το πακέτο `cells` που χρησιμοποιείται παρακάτω. |
| Βιβλιοθήκη `cells` (`pip install cells`) | Παρέχει τις κλάσεις `Workbook` και `GridJs`. |
| Ένα δείγμα αρχείου Excel (`sample.xlsx`) | Αυτό είναι το πηγαίο αρχείο από το οποίο θα **φορτώσουμε βιβλίο εργασίας Excel**. |
| Δικαίωμα εγγραφής στον φάκελο εξόδου | Απαιτείται για το βήμα `grid.save()`. |

Αν κάποιο από αυτά σας είναι άγνωστο, κάντε παύση και εγκαταστήστε το πρώτα—διαφορετικά το script θα εμφανίσει σφάλμα εισαγωγής.

---

## Βήμα 1: Φόρτωση Βιβλίου Excel

Το πρώτο πράγμα που κάνετε όταν θέλετε να **μετατρέψετε xlsx σε json** είναι να ανοίξετε το βιβλίο εργασίας. Σκεφτείτε το σαν να ξεκλειδώνετε την πόρτα πριν διακοσμήσετε το δωμάτιο.

```python
import cells

# Replace YOUR_DIRECTORY with the actual path on your system
workbook_path = "YOUR_DIRECTORY/sample.xlsx"

# Load the workbook – this is the entry point for all further operations
workbook = cells.Workbook(workbook_path)
print(f"Workbook loaded: {workbook_path}")
```

> **Συμβουλή:** Αν το αρχείο σας είναι τεράστιο, σκεφτείτε να χρησιμοποιήσετε `cells.Workbook(..., read_only=True)` για να μειώσετε την κατανάλωση μνήμης.

---

## Βήμα 2: Δημιουργία Αντικειμένου Server GridJs

Τώρα που το βιβλίο εργασίας είναι στη μνήμη, χρειαζόμαστε ένα αντικείμενο **GridJs** που θα μεταφράσει τα φύλλα σε JSON που μπορεί να καταναλώσει η διεπαφή του πελάτη.

```python
# Create a GridJs instance linked to the workbook
grid = cells.GridJs(workbook)
print("GridJs server object created.")
```

Η μεταβλητή `grid` είναι ουσιαστικά μια ελαφριά περιτύλιξη γύρω από το βιβλίο εργασίας που ξέρει πώς να σειριοποιεί κελιά, τύπους και ακόμη πληροφορίες μορφοποίησης.

---

## Βήμα 3: Ενεργοποίηση Ορθογραφικού Ελέγχου (και Ελεγκτή Τύπων)

Εδώ λάμπει η κύρια λέξη‑κλειδί. Με την εναλλαγή της σημαίας `enableSpellCheck`, παρέχετε στους τελικούς χρήστες ένα δίχτυ ασφαλείας ενάντια σε τυπογραφικά λάθη—όπως στο desktop Excel.

```python
# Turn on advanced validation features
grid.options["enableFormulaChecker"] = True   # optional but handy
grid.options["enableSpellCheck"] = True       # <-- enable spell check
print("Spell check and formula checker enabled.")
```

Γιατί να ενεργοποιήσετε και τα δύο; Ο ορθογραφικός έλεγχος εντοπίζει λανθασμένο κείμενο, ενώ ο ελεγκτής τύπων προστατεύει από σπασμένους υπολογισμούς. Μαζί κάνουν τη web UI να νιώθει τόσο επαγγελματική όσο η εγγενής εμπειρία του Excel.

---

## Βήμα 4: Διαμόρφωση Lazy Loading

Αν δουλεύετε με χιλιάδες γραμμές, η αποστολή ολόκληρου του συνόλου δεδομένων σε ένα payload θα “πνίξει” τον περιηγητή. **Διαμορφώστε lazy loading** για να στέλνετε τα δεδομένα σε μικρά κομμάτια (500 γραμμές ανά αίτηση στο παράδειγμά μας).

```python
# Lazy loading improves performance for large sheets
grid.options["lazyLoading"] = {"pageSize": 500}
print("Lazy loading configured: 500 rows per request.")
```

Μπορείτε να ρυθμίσετε το `pageSize` ανάλογα με τις συνθήκες του δικτύου σας. Μικρότερες σελίδες σημαίνουν περισσότερα round‑trips αλλά πιο ομαλή UI· μεγαλύτερες σελίδες μειώνουν τις κλήσεις αλλά μπορεί να προκαλέσουν καθυστέρηση.

---

## Βήμα 5: Εξαγωγή Excel JSON

Όλη η βαριά δουλειά τώρα εκτελείται στο παρασκήνιο. Η τελική ενέργεια είναι να **εξάγετε excel json** σε ένα αρχείο που το front‑end σας μπορεί να ζητήσει.

```python
# Destination for the generated JSON
output_path = "YOUR_DIRECTORY/grid_data.json"

# Persist the JSON representation
grid.save(output_path)
print(f"JSON exported to: {output_path}")
```

Όταν η μέθοδος `save` ολοκληρωθεί, θα έχετε ένα τακτοποιημένο `grid_data.json` που περιέχει:

* Ονόματα φύλλων και IDs  
* Δεδομένα γραμμών (τιμές, τύποι και μορφοποίηση)  
* Μεταδεδομένα για τις ενεργοποιημένες λειτουργίες (ορθογραφικός έλεγχος, lazy loading κ.λπ.)

Μπορείτε να επαληθεύσετε το αποτέλεσμα ανοίγοντας το αρχείο σε έναν επεξεργαστή κειμένου ή φορτώνοντάς το στην κονσόλα του προγράμματος περιήγησης:

```json
{
  "sheets": [
    {
      "name": "Sheet1",
      "rows": [
        {"c": [{"v": "Hello"}, {"v": 123}]},
        {"c": [{"v": "World"}, {"v": 456}]}
      ]
    }
  ],
  "options": {
    "enableSpellCheck": true,
    "enableFormulaChecker": true,
    "lazyLoading": {"pageSize": 500}
  }
}
```

Αυτή είναι μια **πλήρης, αυτόνομη λύση** για τη μετατροπή ενός αρχείου Excel σε JSON payload ενώ διατηρείται ο ορθογραφικός έλεγχος.

---

## Πλήρες Script – Συνδυάστε τα Όλα

Παρακάτω είναι ολόκληρο το πρόγραμμα που μπορείτε να αντιγράψετε‑επικολλήσετε, να προσαρμόσετε τις διαδρομές και να τρέξετε. Δεν υπάρχουν κρυφά βήματα, δεν χρειάζονται εξωτερικά scripts—μόνο ένα αρχείο.

```python
import cells

# ----------------------------------------------------------------------
# Configuration – adjust these variables to match your environment
# ----------------------------------------------------------------------
WORKBOOK_PATH = "YOUR_DIRECTORY/sample.xlsx"
OUTPUT_JSON = "YOUR_DIRECTORY/grid_data.json"
PAGE_SIZE = 500   # rows per lazy‑load request

# ----------------------------------------------------------------------
# 1️⃣ Load the Excel workbook
# ----------------------------------------------------------------------
workbook = cells.Workbook(WORKBOOK_PATH)
print(f"[✓] Loaded workbook from {WORKBOOK_PATH}")

# ----------------------------------------------------------------------
# 2️⃣ Create GridJs server object
# ----------------------------------------------------------------------
grid = cells.GridJs(workbook)
print("[✓] GridJs instance ready")

# ----------------------------------------------------------------------
# 3️⃣ Enable spell check + formula checking
# ----------------------------------------------------------------------
grid.options["enableFormulaChecker"] = True
grid.options["enableSpellCheck"] = True
print("[✓] Spell check and formula checker enabled")

# ----------------------------------------------------------------------
# 4️⃣ Configure lazy loading for performance
# ----------------------------------------------------------------------
grid.options["lazyLoading"] = {"pageSize": PAGE_SIZE}
print(f"[✓] Lazy loading set to {PAGE_SIZE} rows per request")

# ----------------------------------------------------------------------
# 5️⃣ Export the workbook as JSON
# ----------------------------------------------------------------------
grid.save(OUTPUT_JSON)
print(f"[✓] Exported JSON to {OUTPUT_JSON}")
```

Αποθηκεύστε το ως `export_gridjs.py` και τρέξτε:

```bash
python export_gridjs.py
```

Θα πρέπει να δείτε μια σειρά από μηνύματα `[✓]` που επιβεβαιώνουν ότι κάθε βήμα ολοκληρώθηκε επιτυχώς.

---

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

**Τι γίνεται αν το βιβλίο εργασίας μου περιέχει πολλαπλά φύλλα;**  
Το GridJs επαναλαμβάνει αυτόματα κάθε φύλλο, έτσι το παραγόμενο JSON θα έχει έναν πίνακα `sheets`. Μπορείτε να φιλτράρετε στην πλευρά του πελάτη αν χρειάζεστε μόνο ένα υποσύνολο.

**Μπορώ να απενεργοποιήσω τον ορθογραφικό έλεγχο για ένα συγκεκριμένο φύλλο;**  
Το λεξικό `options` εφαρμόζεται παγκοσμίως. Για εναλλαγή ανά φύλλο θα χρειαστεί να δημιουργήσετε ξεχωριστά αντικείμενα `GridJs` ή να επεξεργαστείτε το JSON μετά την εξαγωγή.

**Το αρχείο μου είναι μεγαλύτερο από 10 MB—θα βοηθήσει ακόμα το lazy loading;**  
Απόλυτα. Το lazy loading λειτουργεί σε επίπεδο API· ο διακομιστής στέλνει μόνο τη ζητούμενη σελίδα. Ωστόσο, σκεφτείτε να αυξήσετε το `pageSize` στα 1000 αν η καθυστέρηση του δικτύου σας είναι χαμηλή.

**Πρέπει να ανησυχώ για χαρακτήρες Unicode;**  
Η βιβλιοθήκη `cells` διαχειρίζεται UTF‑8 από την αρχή, έτσι χαρακτήρες όπως emojis ή μη‑λατινικά αλφάβητα διατηρούνται στη μεταφορά.

---

## Συμβουλές για Παραγωγή

* **Cache το JSON** – Αν το βιβλίο εργασίας αλλάζει σπάνια, αποθηκεύστε το `grid_data.json` σε CDN για αστραπιαία φόρτωση.  
* **Ασφάλεια** – Ποτέ μην εκθέτετε το ακατέργαστο αρχείο Excel· σερβίρετε μόνο το παραγόμενο JSON.  
* **Versioning** – Συμπεριλάβετε αριθμό έκδοσης στο όνομα του αρχείου JSON (π.χ., `grid_data_v2.json`) για να αποφύγετε παλαιά δεδομένα μετά από ενημερώσεις.  
* **Testing** – Γράψτε ένα μικρό unit test που φορτώνει το JSON και ελέγχει ότι το `enableSpellCheck` είναι `true`. Συλλαμβάνει regressions νωρίς.

---

## Συμπέρασμα

Τώρα έχετε μια σταθερή, end‑to‑end συνταγή για να **ενεργοποιήσετε ορθογραφικό έλεγχο** ενώ **εξάγετε Excel JSON** χρησιμοποιώντας GridJs. Από το **φόρτωμα βιβλίου εργασίας Excel** μέχρι τη **διαμόρφωση lazy loading** και τελικά τη **μετατροπή xlsx σε json**, η διαδικασία είναι απλή και έτοιμη για παραγωγή.

Τι θα κάνετε στη συνέχεια; Δοκιμάστε να ενσωματώσετε το παραγόμενο `grid_data.json` σε μια απλή HTML σελίδα που χρησιμοποιεί τη βιβλιοθήκη πελάτη GridJs, πειραματιστείτε με προσαρμοσμένους renderers κελιών ή προσθέστε έλεγχο ταυτοποίησης γύρω από το endpoint JSON. Ο ουρανός είναι το όριο όταν συνδυάζετε ορθογραφικό έλεγχο, lazy loading και αδιάλειπτη μετατροπή Excel‑σε‑JSON.

Έχετε περισσότερες ερωτήσεις ή ένα δύσκολο βιβλίο εργασίας που σας προβληματίζει; Αφήστε ένα σχόλιο παρακάτω, και καλή προγραμματιστική!

---

![Ενεργοποίηση ορθογραφικού ελέγχου στο GridJs](/images/enable-spell-check-gridjs.png "Στιγμιότυπο οθόνης που δείχνει ενεργοποιημένο ορθογραφικό έλεγχο στο UI του GridJs")

## Τι Θα Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να κατακτήσετε επιπλέον δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στα δικά σας έργα.

- [Εξαγωγή Excel σε JSON](/cells/english/java/excel-import-export/export-excel-to-json/)
- [Εισαγωγή Δεδομένων JSON στο Excel Χρησιμοποιώντας Aspose.Cells Java: Ένας Πλήρης Οδηγός](/cells/english/java/import-export/import-json-data-excel-aspose-cells-java/)
- [Πώς να Φιλτράρετε Αποτελεσματικά Δεδομένα Κατά τη Φόρτωση Βιβλίων Excel Χρησιμοποιώντας Aspose.Cells σε Java](/cells/english/java/data-analysis/filter-data-excel-aspose-cells-java-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}