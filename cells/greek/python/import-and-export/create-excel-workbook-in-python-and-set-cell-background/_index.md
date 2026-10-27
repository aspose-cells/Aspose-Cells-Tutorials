---
category: general
date: 2026-10-07
description: Δημιουργήστε βιβλίο εργασίας Excel σε Python, ορίστε το χρώμα φόντου
  των κελιών, προσαρμόστε αυτόματα το πλάτος των στηλών και συμπληρώστε ημερομηνίες
  στο Excel με ένα σύντομο παράδειγμα κώδικα.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- auto fit excel columns
- populate dates in excel
- how to create excel
language: el
lastmod: 2026-10-07
og_description: Δημιουργήστε βιβλίο εργασίας Excel με Python, στη συνέχεια ορίστε
  το χρώμα φόντου των κελιών, προσαρμόστε αυτόματα τις στήλες και προσθέστε ημερομηνίες
  στο Excel. Ακολουθήστε αυτόν τον οδηγό βήμα‑βήμα για να δημιουργήσετε το αρχείο
  TimePeriodDemo.xlsx.
og_image_alt: Screenshot of a Python‑generated Excel workbook with pink highlighted
  cells
og_title: Δημιουργία βιβλίου εργασίας Excel σε Python – ορισμός φόντου & αυτόματη
  προσαρμογή
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Create Excel workbook in Python, set cell background color, auto‑fit
    columns, and populate dates in Excel with a concise code example.
  headline: Create Excel workbook in Python and set cell background
  type: TechArticle
- description: Create Excel workbook in Python, set cell background color, auto‑fit
    columns, and populate dates in Excel with a concise code example.
  name: Create Excel workbook in Python and set cell background
  steps:
  - name: Import required namespaces and define a helper function
    text: '```python # Step 1: Import Aspose.Cells classes and supporting modules
      from aspose.cells import Workbook, FormatConditionType, TimePeriodType, BackgroundType,
      SaveFormat from aspose.pydrawing import Color from datetime import datetime
      import os ```'
  - name: Create the workbook and get the first worksheet
    text: '```python def create_workbook(): # Step 2: Instantiate a new workbook (empty
      Excel file) book = Workbook() # Aspose.Cells creates a default worksheet; we
      retrieve it for further work sheet = book.worksheets[0] return book, sheet ```'
  - name: Set cell background color with a conditional format
    text: '```python def add_yesterday_rule(sheet): # Define a conditional format
      for the range I19:K20 (Yesterday) conds = sheet.get_range("I19:K20").format_conditions
      idx = conds.add_condition(FormatConditionType.TIME_PERIOD) cond = conds[idx]'
  - name: Populate dates in Excel
    text: '```python def populate_sample_dates(sheet): # Insert a date that falls
      on yesterday relative to the demo data cell = sheet.cells.get("I19") cell.put_value(datetime(2008,
      7, 30)) # sample date cell.style.number = 30 # Excel’s date format ID cell.set_style(cell.style)'
  - name: Auto‑fit Excel columns for better visibility
    text: '```python def auto_fit_columns(sheet): # Auto‑fit column L (index 12) so
      the content is fully visible sheet.auto_fit_column(12) # <-- auto fit excel
      columns ```'
  - name: Save the workbook
    text: '```python def save_workbook(book, filename="TimePeriodDemo.xlsx"): out_path
      = os.path.join("YOUR_DIRECTORY", filename) os.makedirs(os.path.dirname(out_path),
      exist_ok=True) book.save(out_path, SaveFormat.XLSX) print(f"Workbook saved to:
      {out_path}") ```'
  - name: Full script – putting it all together
    text: '```python def main(): # Create workbook and obtain the first worksheet
      book, sheet = create_workbook()'
  type: HowTo
tags:
- Excel
- Python
- Aspose.Cells
title: Δημιουργία βιβλίου εργασίας Excel σε Python και ορισμός φόντου κελιού
url: /el/python/import-and-export/create-excel-workbook-in-python-and-set-cell-background/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία βιβλίου εργασίας Excel σε Python και ορισμός φόντου κελιού

Δημιουργήστε βιβλίο εργασίας Excel σε Python και εφαρμόστε μορφοποίηση υπό όρους με λίγες μόνο γραμμές κώδικα. Αυτό το σεμινάριο σας δείχνει **πώς να δημιουργήσετε αρχεία excel** προγραμματιστικά, να ορίσετε το χρώμα φόντου του κελιού, να προσαρμόσετε αυτόματα τις στήλες του Excel και να συμπληρώσετε ημερομηνίες στο Excel χρησιμοποιώντας τη βιβλιοθήκη Aspose.Cells.

Θα μάθετε πώς να:
* Αρχικοποιήσετε ένα βιβλίο εργασίας και να αποκτήσετε το πρώτο φύλλο εργασίας.  
* Ορίσετε μια μορφοποίηση υπό όρους που επισημαίνει ημερομηνίες «Χθες».  
* Εισάγετε δείγμα ημερομηνιών σε συγκεκριμένα κελιά.  
* Προσαρμόσετε αυτόματα τις στήλες ώστε τα δεδομένα να είναι καθαρά ορατά.  
* Αποθηκεύσετε το βιβλίο εργασίας σε έναν επιλεγμένο φάκελο.

Η μόνη προαπαιτούμενη προϋπόθεση είναι ένα λειτουργικό περιβάλλον Python 3 με τα πακέτα `aspose-cells` και `aspose-pydrawing` εγκατεστημένα:

```bash
pip install aspose-cells aspose-pydrawing
```

---

## Δημιουργία βιβλίου εργασίας Excel σε Python – βήμα προς βήμα

Οι παρακάτω ενότητες χωρίζουν τη διαδικασία σε διαχειρίσιμα βήματα. Κάθε βήμα περιλαμβάνει τον απαιτούμενο κώδικα, μια εξήγηση του **γιατί** είναι σημαντικό, και μια συμβουλή για αποφυγή κοινών παγίδων.

### Βήμα 1: Εισαγωγή απαιτούμενων namespaces και ορισμός βοηθητικής συνάρτησης

```python
# Step 1: Import Aspose.Cells classes and supporting modules
from aspose.cells import Workbook, FormatConditionType, TimePeriodType, BackgroundType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime
import os
```

*Γιατί είναι σημαντικό*: Η εισαγωγή των σωστών κλάσεων σας δίνει πρόσβαση στη δημιουργία βιβλίου εργασίας, στη μορφοποίηση υπό όρους και στη διαχείριση χρωμάτων.  
**Συμβουλή**: Κρατήστε τις εισαγωγές στην αρχή του αρχείου· καθιστά το script πιο ευανάγνωστο και αποτρέπει σφάλματα κυκλικής εισαγωγής.

### Βήμα 2: Δημιουργία του βιβλίου εργασίας και λήψη του πρώτου φύλλου

```python
def create_workbook():
    # Step 2: Instantiate a new workbook (empty Excel file)
    book = Workbook()
    # Aspose.Cells creates a default worksheet; we retrieve it for further work
    sheet = book.worksheets[0]
    return book, sheet
```

Ο κατασκευαστής `Workbook()` δημιουργεί ένα κενό βιβλίο εργασίας Excel στη μνήμη.  
**Γιατί**: Ξεκινώντας με ένα φρέσκο βιβλίο εργασίας εξασφαλίζετε ότι δεν υπάρχουν υπολειπόμενες μορφοποιήσεις από προηγούμενες εκτελέσεις.

### Βήμα 3: Ορισμός χρώματος φόντου κελιού με μορφοποίηση υπό όρους

```python
def add_yesterday_rule(sheet):
    # Define a conditional format for the range I19:K20 (Yesterday)
    conds = sheet.get_range("I19:K20").format_conditions
    idx = conds.add_condition(FormatConditionType.TIME_PERIOD)
    cond = conds[idx]

    # Apply visual style – this is where we set the cell background color
    cond.style.background_color = Color.pink          # <-- set cell background color
    cond.style.pattern = BackgroundType.SOLID
    cond.time_period = TimePeriodType.YESTERDAY
```

*Γιατί*: Η χρήση μιας συνθήκης **χρονικής περιόδου** επισημαίνει αυτόματα οποιοδήποτε κελί περιέχει την ημερομηνία του χθες, εξαλείφοντας τις χειροκίνητες ελέγχους ημερομηνίας.  
**Συμβουλή**: Το `Color.pink` είναι μόνο ένα παράδειγμα· μπορείτε να χρησιμοποιήσετε οποιοδήποτε αντικείμενο `Color` (`Color.yellow`, `Color.light_green`, κ.λπ.).

### Βήμα 4: Συμπλήρωση ημερομηνιών στο Excel

```python
def populate_sample_dates(sheet):
    # Insert a date that falls on yesterday relative to the demo data
    cell = sheet.cells.get("I19")
    cell.put_value(datetime(2008, 7, 30))   # sample date
    cell.style.number = 30                 # Excel’s date format ID
    cell.set_style(cell.style)

    # Insert another date outside the “Yesterday” range
    cell = sheet.cells.get("K20")
    cell.put_value(datetime(2008, 8, 3))
    cell.style.number = 30
    cell.set_style(cell.style)

    # Add a label for the rule
    sheet.cells.get("I20").put_value("Yesterday")
```

Εδώ **συμπληρώνουμε ημερομηνίες** στα κελιά `I19` και `K20`. Η πρώτη ημερομηνία θα ενεργοποιήσει τη μορφοποίηση υπό όρους, ενώ η δεύτερη όχι.  
**Γιατί είναι σημαντικό**: Η επίδειξη τόσο των τιμών που ταιριάζουν όσο και των μη‑ταίριαστων βοηθά στην επαλήθευση ότι ο κανόνας λειτουργεί όπως αναμένεται.

### Βήμα 5: Αυτόματη προσαρμογή στηλών Excel για καλύτερη ορατότητα

```python
def auto_fit_columns(sheet):
    # Auto‑fit column L (index 12) so the content is fully visible
    sheet.auto_fit_column(12)   # <-- auto fit excel columns
```

Η μέθοδος `auto_fit_column` προσαρμόζει το πλάτος της στήλης βάσει της μεγαλύτερης τιμής κελιού.  
**Συμβουλή**: Καλέστε τη μετά την εισαγωγή όλων των δεδομένων· διαφορετικά το πλάτος μπορεί να υπολογιστεί με βάση ελλιπές περιεχόμενο.

### Βήμα 6: Αποθήκευση του βιβλίου εργασίας

```python
def save_workbook(book, filename="TimePeriodDemo.xlsx"):
    out_path = os.path.join("YOUR_DIRECTORY", filename)
    os.makedirs(os.path.dirname(out_path), exist_ok=True)
    book.save(out_path, SaveFormat.XLSX)
    print(f"Workbook saved to: {out_path}")
```

Η αποθήκευση του αρχείου γράφει το βιβλίο εργασίας που βρίσκεται στη μνήμη στο δίσκο σε σύγχρονη μορφή XLSX.  

### Πλήρης σενάριο – όλα μαζί

```python
def main():
    # Create workbook and obtain the first worksheet
    book, sheet = create_workbook()

    # Apply conditional formatting (set cell background color)
    add_yesterday_rule(sheet)

    # Populate the demo dates (populate dates in excel)
    populate_sample_dates(sheet)

    # Auto‑fit the relevant column (auto fit excel columns)
    auto_fit_columns(sheet)

    # Persist the file
    save_workbook(book)

if __name__ == "__main__":
    main()
```

**Αναμενόμενο αποτέλεσμα**

```
Workbook saved to: YOUR_DIRECTORY/TimePeriodDemo.xlsx
```

Ανοίξτε το παραγόμενο αρχείο στο Excel – τα κελιά `I19:K20` θα εμφανίζουν ροζ φόντο για την ημερομηνία που αντιστοιχεί στο «Χθες», και η στήλη L θα είναι αρκετά πλατιά ώστε να εμφανίζει την ετικέτα χωρίς αποκοπή.

---

## Γιατί αυτή η προσέγγιση λειτουργεί καλύτερα

* **Ροή εργασίας μονής διέλευσης** – Όλες οι λειτουργίες εκτελούνται στο ίδιο αντικείμενο `Workbook`, αποφεύγοντας περιττές εισόδους/εξόδους.  
* **Μορφοποίηση υπό όρους** – Η χρήση του `FormatConditionType.TIME_PERIOD` επιτρέπει στο Excel να διαχειριστεί τη λογική ημερομηνίας, κάτι που είναι πιο αξιόπιστο από την υλοποίηση προσαρμοσμένων ελέγχων ημερομηνίας σε Python.  
* **Σαφής στυλ** – Ο ορισμός του `background_color` και του `pattern` εγγυάται το οπτικό αποτέλεσμα σε όλες τις εκδόσεις του Excel.  
* **Αυτόματη προσαρμογή μετά τα δεδομένα**

## Τι Θα Πρέπει Να Μάθετε Στη Σειρά;

Τα παρακάτω σεμινάρια καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικά παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε επιπλέον δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Create Excel Workbook Python – Full Guide](/cells/english/python/import-and-export/create-excel-workbook-python-full-guide/)
- [Create Excel Workbook Python – Complete Step‑by‑Step Guide](/cells/english/python/import-and-export/create-excel-workbook-python-complete-step-by-step-guide/)
- [Create Excel Workbook Python – Complete Guide with Lambda](/cells/english/python/formulas-and-functions/create-excel-workbook-python-complete-guide-with-lambda/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}