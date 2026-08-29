---
category: general
date: 2026-06-08
description: Δημιουργήστε παράδειγμα Python για βιβλίο εργασίας Excel που δείχνει
  πώς να χρησιμοποιήσετε τη συνάρτηση λ (lambda) στο Excel, να αθροίζετε γραμμές με
  τη λειτουργία BYROW και να αυτοματοποιείτε υπολογισμούς σε λίγα βήματα.
draft: false
keywords:
- create excel workbook python
- how to use lambda
- how to sum rows
- use lambda excel
language: el
og_description: Δημιουργήστε βιβλίο εργασίας Excel με Python και μάθετε πώς να χρησιμοποιείτε
  τη λειτουργία λήμμα (lambda) στο Excel για να αθροίζετε γραμμές αποδοτικά με τύπους
  BYROW.
og_title: Δημιουργία βιβλίου εργασίας Excel με Python – Πλήρης οδηγός
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Create Excel workbook Python example that shows how to use lambda in
    Excel, sum rows with BYROW, and automate calculations in a few steps.
  headline: Create Excel Workbook Python – Complete Guide with Lambda
  type: TechArticle
tags:
- python
- excel
- automation
title: Δημιουργία βιβλίου εργασίας Excel με Python – Πλήρης οδηγός με Lambda
url: /el/python/formulas-and-functions/create-excel-workbook-python-complete-guide-with-lambda/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία Excel Workbook με Python – Πλήρης Οδηγός με Lambda

Ever wondered how to **create Excel workbook Python** scripts that automate boring number‑crunching? You're not alone—many developers hit a wall when they need to generate a sheet, drop a formula in, and pull the results back into their code.  

Σε αυτό το tutorial θα δείξουμε επίσης **how to use lambda** στο Excel, θα εξηγήσουμε **how to sum rows** με τη σύγχρονη συνάρτηση `BYROW`, και θα σας δώσουμε ένα καθαρό, ολοκληρωμένο παράδειγμα που μπορείτε να αντιγράψετε‑επικολλήσετε και να τρέξετε σήμερα.

## Τι Θα Μάθετε

- Δημιουργήστε ένα νέο workbook από την Python χωρίς να ανοίξετε το Excel χειροκίνητα.  
- Συμπληρώστε μια περιοχή με έναν πίνακα 3 × 3 αριθμών.  
- Εισάγετε έναν τύπο `BYROW` που αξιοποιεί τη σύνταξη **use lambda excel** για να αθροίσει κάθε σειρά.  
- Επαναϋπολογίστε το φύλλο ώστε ο τύπος να αξιολογηθεί, και στη συνέχεια διαβάστε τα αποτελέσματα πίσω στην Python.  

Στο τέλος αυτού του οδηγού θα έχετε ένα αυτόνομο script που μπορείτε να προσαρμόσετε για τιμολόγια, score‑cards, ή οποιαδήποτε κατάσταση όπου χρειάζεται να **sum rows** άμεσα.

### Προαπαιτούμενα

- Εγκατεστημένη Python 3.8+.  
- Η βιβλιοθήκη `openpyxl` (ή `xlwings` αν προτιμάτε μια προσέγγιση βασισμένη σε COM). Θα χρησιμοποιήσουμε το `openpyxl` επειδή είναι καθαρά‑Python και λειτουργεί σε όλες τις πλατφόρμες.  
- Μια πρόσφατη έκδοση του Microsoft Excel (365 ή 2021) που υποστηρίζει τη συνάρτηση `BYROW` και τύπους Lambda.  

Εγκαταστήστε τη βιβλιοθήκη με:

```bash
pip install openpyxl
```

> **Συμβουλή:** Αν αντιμετωπίσετε προβλήματα δικαιωμάτων στα Windows, χρησιμοποιήστε `python -m pip install --user openpyxl`.

---

## Δημιουργία Excel Workbook Python – Αρχικοποίηση Workbook

Το πρώτο που χρειαζόμαστε είναι ένα ολοκαίνουργιο αντικείμενο workbook που ζει εξ ολοκλήρου στη μνήμη. Με το `openpyxl` αυτό είναι μια γραμμή κώδικα:

```python
from openpyxl import Workbook

# Step 1: Create a new workbook and grab the first worksheet
wb = Workbook()
ws = wb.active   # .active is the first sheet by default
```

Γιατί χρησιμοποιούμε το `wb.active` αντί για την πρόσβαση με `Worksheets[0]`; Το `openpyxl` εκθέτει το ενεργό φύλλο απευθείας, κάτι που είναι πιο σαφές και αποφεύγει μια επιπλέον αναζήτηση λίστας. Αν χρειαστεί ποτέ να δουλέψετε με πολλά φύλλα, μπορείτε πάντα να τα προσθέσετε με `wb.create_sheet(title="MySheet")`.

---

## Συμπλήρωση του Worksheet με Δεδομένα – Ένας Απλός Πίνακας 3×3

Στη συνέχεια, γεμίζουμε το φύλλο με έναν μικρό πίνακα. Αυτό αντικατοπτρίζει το κλασικό παράδειγμα “sum each row” και διατηρεί τον κώδικα σύντομο.

```python
# Step 2: Define a 3×3 matrix of numbers
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

# Import the matrix into the worksheet starting at cell A1
for r_idx, row in enumerate(matrix, start=1):
    for c_idx, value in enumerate(row, start=1):
        ws.cell(row=r_idx, column=c_idx, value=value)
```

Μπορεί να αναρωτιέστε γιατί κάνουμε βρόχο χειροκίνητα αντί για `ws.append()` ή `ws.values`. Οι ρητοί βρόχοι μας δίνουν πλήρη έλεγχο στο αρχικό κελί και καθιστούν εύκολη την προσαρμογή των μετατοπίσεων αργότερα—χρήσιμο όταν θέλετε να αφήσετε κενή μια γραμμή ή στήλη κεφαλίδας.

---

## Πώς να Χρησιμοποιήσετε Lambda σε Τύπους Excel

Η δυνατότητα **use lambda excel** του Excel σας επιτρέπει να γράφετε ανώνυμες συναρτήσεις απευθείας σε ένα κελί. Σκεφτείτε το ως το `lambda` της Python αλλά ενσωματωμένο στη μηχανή του φύλλου. Η σύνταξη είναι:

```
=LAMBDA(parameter1, parameter2, …, calculation)
```

Όταν συνδυαστεί με το `BYROW`, μπορείτε να εφαρμόσετε αυτό το lambda σε κάθε σειρά ενός εύρους, παράγοντας μια στήλη αποτελεσμάτων. Αυτό είναι το κέντρο του κόλπου **how to sum rows**.

```python
# Step 3: Insert a BYROW formula that sums each row using a Lambda
ws["D1"] = "=BYROW(A1:C3, LAMBDA(r, SUM(r)))"
```

Τι συμβαίνει στο παρασκήνιο;

- `A1:C3` είναι το εύρος προέλευσης (ο πίνακάς μας).  
- `LAMBDA(r, SUM(r))` ορίζει μια προσωρινή συνάρτηση που λαμβάνει μια μόνο σειρά (`r`) και επιστρέφει το άθροισμά της.  
- `BYROW` εκτελεί αυτό το lambda για **κάθε σειρά** και ρίχνει τα αποτελέσματα στη στήλη D, ξεκινώντας από το `D1`.  

Επειδή το `BYROW` είναι μια λειτουργία *dynamic array*, το Excel γεμίζει αυτόματα το `D1:D3` με τα τρία αθροίσματα.

> **Σημείωση:** Τα `BYROW` και οι τύποι Lambda είναι διαθέσιμα μόνο στο Excel 365/2021 και νεότερες εκδόσεις. Αν χρησιμοποιείτε παλαιότερη έκδοση, θα πρέπει να επιστρέψετε σε παραδοσιακούς τύπους `SUM` ή VBA.

## Πώς να Αθροίσετε Σειρές με BYROW και Lambda

Τώρα που ο τύπος βρίσκεται στο φύλλο, πρέπει να πούμε στο Excel να τον αξιολογήσει. Το `openpyxl` από μόνο του δεν υπολογίζει τύπους· μόνο διαβάζει/γράφει. Για να ενεργοποιήσουμε έναν υπολογισμό μπορούμε είτε:

1. Να αποθηκεύσουμε το workbook και να το ανοίξουμε στο Excel (χειροκίνητα).  
2. Να χρησιμοποιήσουμε τη μηχανή COM του `xlwings` για να εξαναγκάσουμε επαναϋπολογισμό (απαιτεί εγκατεστημένο Excel).  

Για μια λύση καθαρά‑Python θα χρησιμοποιήσουμε το `xlwings` μόνο για το βήμα υπολογισμού—τίποτα άλλο.

```python
import xlwings as xw

# Step 4: Recalculate the workbook so the BYROW formula is evaluated
# Save the workbook to a temporary file first
temp_path = "temp_workbook.xlsx"
wb.save(temp_path)

# Open the file with xlwings, force a calculation, then close
app = xw.App(visible=False)
book = app.books.open(temp_path)
book.api.CalculateFull()          # Full recalculation
book.save()
book.close()
app.quit()
```

Γιατί δεν καλούμε `wb.calculate()`; Το `openpyxl` δεν διαθέτει ενσωματωμένο μηχανισμό, έτσι βασιζόμαστε στο ίδιο το Excel μέσω του `xlwings`. Το κόστος είναι ελάχιστο για μικρά φύλλα και μας δίνει το ακριβές αποτέλεσμα που θα έδειχνε το Excel.

## Επαναϋπολογισμός και Ανάκτηση Αποτελεσμάτων – Εξαγωγή των Αθροισμάτων Πίσω στην Python

Τέλος, διαβάζουμε τα αποτελέσματα που έριξε η στήλη D. Το `openpyxl` το κάνει αυτό απλό:

```python
# Step 5: Load the recalculated workbook and grab the results
wb = Workbook()  # re‑open the saved file
wb = xw.Book(temp_path).api  # alternative: use xlwings again to read values

# Using xlwings to fetch the range values as a Python list
results = xw.Range('D1:D3').value
print(results)   # Expected output: [6, 15, 24]
```

Αν προτιμάτε να παραμείνετε μέσα στο `openpyxl`, μπορείτε να διαβάσετε τα κελιά μετά τον επαναϋπολογισμό του Excel:

```python
from openpyxl import load_workbook

wb = load_workbook(temp_path, data_only=True)  # data_only reads calculated values
ws = wb.active
results = [ws[f"D{row}"].value for row in range(1, 4)]
print(results)   # -> [6, 15, 24]
```

Και οι δύο προσεγγίσεις σας δίνουν την ίδια λίστα `[6, 15, 24]`, επιβεβαιώνοντας ότι το **how to sum rows** με `BYROW` + Lambda λειτουργεί όπως περιγράφεται.

## Περιπτώσεις Ορίων & Συνηθισμένα Πιθανά Προβλήματα

| Κατάσταση | Τι να Προσέξετε | Διόρθωση |
|-----------|-------------------|-----|
| Έκδοση Excel παλαιότερη από 365 | `BYROW` και `LAMBDA` εμφανίζονται ως `#NAME?` | Χρησιμοποιήστε τον κλασικό `=SUM(A1:C1)` αντιγραφόμενο χειροκίνητα, ή αναβαθμίστε το Excel. |
| Μεγάλοι πίνακες (10 k+ σειρές) | Ο επαναϋπολογισμός μπορεί να γίνει αργός | Καλέστε `book.api.CalculateFullRebuild()` μόνο μία φορά, ή χωρίστε το workbook. |
| Εκτέλεση σε headless server χωρίς Excel | `xlwings` δεν μπορεί να εκκινήσει το Excel | Μεταβείτε σε μια καθαρά‑Python βιβλιοθήκη όπως `pandas` + `numpy` για υπολογισμούς, και στη συνέχεια γράψτε τα αποτελέσματα. |
| Θέματα τοπικής ρύθμισης (κόμμα vs. ερωτηματικό) | Ο τύπος μπορεί να απορριφθεί | Χρησιμοποιήστε `ws["D1"].value = "=BYROW(A1:C3; LAMBDA(r; SUM(r)))"` για τοπικές ρυθμίσεις που χρησιμοποιούν `;`. |

## Πλήρες Παράδειγμα Εργασίας (Έτοιμο για Αντιγραφή‑Επικόλληση)

```python
# ------------------------------------------------------------
# create_excel_workbook_python – full script
# ------------------------------------------------------------
import os
from openpyxl import Workbook, load_workbook
import xlwings as xw

# 1️⃣ Initialize workbook
wb = Workbook()
ws = wb.active

# 2️⃣ Populate with a 3×3 matrix
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]
for r_idx, row in enumerate(matrix, start=1):
    for c_idx, val in enumerate(row, start=1):
        ws.cell(row=r_idx, column=c_idx, value=val)

# 3️⃣ Insert BYROW + Lambda formula


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Create Excel Workbook with Aspose.Cells Java - Complete Guide](/cells/english/java/automation-batch-processing/excel-automation-aspose-cells-java-guide/)
- [Create Excel Workbook & Automate Reports with Aspose.Cells](/cells/english/java/automation-batch-processing/aspose-cells-java-two-three-color-scales/)
- [How to Create and Save an Excel Workbook as ODS Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}