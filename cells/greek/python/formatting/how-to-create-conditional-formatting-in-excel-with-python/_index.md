---
category: general
date: 2026-11-16
description: Δημιουργήστε μορφοποίηση υπό όρους στο Excel χρησιμοποιώντας Python.
  Μάθετε πώς να προσθέτετε μια περιοχή μορφοποίησης υπό όρους, να επισημαίνετε ημερομηνίες
  και να δημιουργείτε ένα βιβλίο εργασίας προγραμματιστικά.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create conditional formatting
- create excel workbook python
- how to highlight dates
- add conditional formatting range
- add conditional formatting python
language: el
lastmod: 2026-11-16
og_description: Δημιουργήστε μορφοποίηση υπό όρους στο Excel με Python. Αυτό το σεμινάριο
  δείχνει πώς να προσθέσετε μια περιοχή μορφοποίησης υπό όρους, να επισημάνετε ημερομηνίες
  και να δημιουργήσετε ένα βιβλίο εργασίας.
og_image_alt: Screenshot of Excel sheet with conditional formatting applied using
  Python
og_title: Δημιουργήστε μορφοποίηση υπό όρους στο Excel με Python – βήμα‑βήμα οδηγός
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Create conditional formatting in Excel using Python. Learn to add a
    conditional formatting range, highlight dates, and build a workbook programmatically.
  headline: How to create conditional formatting in Excel with Python
  type: TechArticle
tags:
- Excel
- Python
- Aspose.Cells
- Conditional Formatting
title: Πώς να δημιουργήσετε μορφοποίηση υπό όρους στο Excel με Python
url: /el/python/formatting/how-to-create-conditional-formatting-in-excel-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να δημιουργήσετε μορφοποίηση υπό όρους στο Excel με Python

Αν χρειάζεστε **δημιουργία μορφοποίησης υπό όρους** σε ένα αρχείο Excel ενώ εργάζεστε με Python, αυτός ο οδηγός σας δείχνει ακριβώς πώς να το κάνετε. Θα μάθετε να **create excel workbook python**‑style, να ορίσετε μια περιοχή μορφοποίησης και να επισημάνετε ημερομηνίες χωρίς να αφήσετε το IDE.

Η μορφοποίηση υπό όρους σας επιτρέπει να επισημαίνετε οπτικά κελιά που πληρούν συγκεκριμένα κριτήρια—ιδανική για πίνακες ελέγχου, αναφορές ή φύλλα επαλήθευσης δεδομένων. Στο τέλος αυτού του οδηγού θα έχετε ένα πλήρως λειτουργικό βιβλίο εργασίας που χρωματίζει τα κελιά με ημερομηνία “Yesterday” σε ροζ, ενώ το υπόλοιπο της περιοχής παραμένει πράσινο.

## Τι θα επιτύχετε

* Δημιουργήστε ένα νέο βιβλίο εργασίας από το μηδέν.  
* Προσθέστε μια συλλογή conditional‑format για ένα συγκεκριμένο μπλοκ κελιών.  
* Εφαρμόστε έναν κανόνα **TIME_PERIOD** που επισημαίνει ημερομηνίες (το σενάριο “how to highlight dates”).  
* Αποθηκεύστε το αρχείο ως βιβλίο εργασίας XLSX έτοιμο για επεξεργασία downstream.

**Απαιτούμενα**  
* Python 3.8+  
* `aspose-cells` Python package (`pip install aspose-cells`)  
* Βασική εξοικείωση με το `datetime` module της Python  

---

## Πώς να δημιουργήσετε μορφοποίηση υπό όρους σε Python

Το πρώτο βήμα είναι να ρυθμίσετε το βιβλίο εργασίας και το φύλλο εργασίας που θα φιλοξενήσει τους κανόνες μορφοποίησης.

```python
# Step 1: Import required classes and create a new workbook
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime

# Instantiate a blank workbook and grab the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Optional: auto‑fit column 12 (L) to make the output readable
worksheet.auto_fit_column(12)
```

**Γιατί είναι σημαντικό** – `Workbook` είναι το σημείο εισόδου για όλες τις λειτουργίες του Excel. Η δημιουργία του βιβλίου εργασίας προγραμματιστικά αντικαθιστά το χειροκίνητο βήμα “File → New”, επιτρέποντας αυτοματοποιημένες pipelines αναφορών.

---

## Προετοιμασία της συλλογής conditional‑format – προσθήκη περιοχής μορφοποίησης υπό όρους

Στη συνέχεια ορίζουμε το μπλοκ κελιών που θα λάβει τον κανόνα. Σε αυτό το παράδειγμα η περιοχή είναι **I19:K20**.

```python
# Step 2: Create a conditional‑format collection for the target range
conds = worksheet.conditional_formattings.add("I19:K20")

# Apply a base style (green background) that will show when no rule matches
conds[0].style.background_color = Color.medium_sea_green
conds[0].style.pattern = BackgroundType.SOLID
```

**Explanation** – `conditional_formattings.add` καταχωρεί μια νέα συλλογή συνδεδεμένη με τη συμβολοσειρά διεύθυνσης. Η πρώτη συνθήκη (`conds[0]`) λειτουργεί ως στυλ “default”; ο επόμενος κανόνας θα την αντικαταστήσει όταν πληρούνται τα κριτήριά του.

---

## Προσθήκη συνθήκης TIME_PERIOD – πώς να επισημάνετε ημερομηνίες

Τώρα προσθέτουμε την πραγματική λογική που εντοπίζει τις ημερομηνίες “Yesterday” και τις χρωματίζει ροζ.

```python
# Step 3: Add a TIME_PERIOD condition that highlights cells dated “Yesterday”
idx = conds.add_condition(FormatConditionType.TIME_PERIOD)   # returns the new index
condition = conds[idx]

# Define the visual style for cells that satisfy the condition
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID

# Set the rule to the built‑in YESTERDAY period
condition.time_period = TimePeriodType.YESTERDAY
```

**Why use TIME_PERIOD?** – Η Aspose.Cells παρέχει ενσωματωμένες απαριθμήσεις όπως `YESTERDAY`, `TODAY` και `LAST_WEEK`. Αξιολογούν την τιμή ημερομηνίας του κελιού σε σχέση με την τρέχουσα ημερομηνία του συστήματος, αφαιρώντας την ανάγκη για προσαρμοσμένους τύπους.

---

## Συμπλήρωση δείγματος δεδομένων – επίδειξη του κανόνα

Για να δείτε τη μορφοποίηση σε δράση, εισάγουμε μια ημερομηνία που ταιριάζει με τον κανόνα και μια άλλη που δεν ταιριάζει.

```python
# Step 4: Populate sample dates so the rule can be seen

# Cell I19 gets a date that is “yesterday” relative to 2008‑07‑31
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))  # yesterday for the example
style = cell_i19.get_style()
style.number = 30                         # full date format (e.g., 7/30/2008)
cell_i19.set_style(style)

# Cell K20 gets a later date – it should stay green
cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))   # a future date
style = cell_k20.get_style()
style.number = 30
cell_k20.set_style(style)

# Optional label for clarity
worksheet.cells.get("I20").put_value("Yesterday")
```

**Edge case note** – Ο κανόνας `TIME_PERIOD` λειτουργεί μόνο με *πραγματικές* ημερομηνίες. Αν ένα κελί περιέχει κείμενο (π.χ., “N/A”), ο κανόνας αγνοείται, αποτρέποντας ανεπιθύμητες αλλαγές χρώματος.

---

## Αποθήκευση του βιβλίου εργασίας – add conditional formatting python

Τέλος, γράψτε το βιβλίο εργασίας στο δίσκο. Το αρχείο μπορεί να ανοιχθεί σε οποιοδήποτε πρόγραμμα λογιστικού φύλλου για να επαληθεύσετε τα χρώματα.

```python
# Step 5: Save the workbook
output_path = "TimePeriodExample.out.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to {output_path}")
```

**Expected result**  

| I19 (green → pink) | J19 (green) | K19 (green) |
|--------------------|------------|------------|
| 7/30/2008 (yesterday) | – | – |
| **I20**: “Yesterday” label | – | – |
| I21‑K21 (green)    | – | – |

Το κελί **I19** εμφανίζεται με ροζ φόντο επειδή η ημερομηνία του ταιριάζει με την περίοδο “Yesterday”, ενώ το **K20** παραμένει πράσινο.

---

## Συχνές ερωτήσεις και πρακτικές συμβουλές

* **Μπορώ να χρησιμοποιήσω προσαρμοσμένο εύρος ημερομηνιών αντί για ενσωματωμένη περίοδο;**  
  Ναι. Αντικαταστήστε `condition.time_period` με `condition.formula1 = "TODAY()-1"` και ορίστε `condition.type = FormatConditionType.FORMULA`.

* **Τι γίνεται αν το βιβλίο εργασίας μου περιέχει ήδη δεδομένα;**  
  Χρησιμοποιήστε `worksheet.cells.import_data` για μαζική φόρτωση δεδομένων πριν προσθέσετε τη συλλογή μορφοποίησης υπό όρους.

* **Απόδοση με μεγάλα φύλλα;**  
  Η προσθήκη πολλών συνθηκών μπορεί να επιβραδύνει την απόδοση. Ομαδοποιήστε κελιά με τον ίδιο κανόνα σε μια ενιαία περιοχή (π.χ., “A1:C1000”) για να διατηρήσετε τον αριθμό των συνθηκών χαμηλό.

* **Συμβατότητα μεταξύ πλατφορμών;**  
  Το παραγόμενο αρχείο XLSX ακολουθεί το πρότυπο Office Open XML, επομένως λειτουργεί σε εφαρμογές λογιστικών φύλλων σε Windows, macOS και Linux.

---

## Συμπέρασμα

Τώρα ξέρετε πώς να **create conditional formatting** σε ένα βιβλίο εργασίας Excel χρησιμοποιώντας Python. Ο οδηγός κάλυψε τη δημιουργία του βιβλίου εργασίας, τον ορισμό μιας **add conditional formatting range**, την εφαρμογή ενός κανόνα **how to highlight dates**, και την αποθήκευση του αρχείου—όλα με την προσέγγιση **add conditional formatting python** που παρέχει η Aspose.Cells.

Από εδώ μπορείτε:

* Επεκτείνετε το σύνολο κανόνων με άλλες τιμές `TimePeriodType` (π.χ., `TODAY`, `LAST_MONTH`).  
* Συνδυάστε πολλαπλές συνθήκες στην ίδια περιοχή για πιο πλούσιες οπτικές ενδείξεις.  
* Ενσωματώστε αυτή τη ροή εργασίας σε αυτοματοποιημένα pipelines αναφορών ή web services.

Καλή προγραμματιστική δουλειά, και μη διστάσετε να πειραματιστείτε με διαφορετικά χρώματα, περιοχές και λογική ημερομηνιών για να ταιριάζουν στις ανάγκες αναφοράς σας!

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κυριαρχήσετε σε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Create Excel workbook Python date conditional formatting](/cells/english/python/formatting/create-excel-workbook-python-date-conditional-formatting/)
- [How to apply time period conditional formatting in Excel using Python](/cells/english/python/formatting/how-to-apply-time-period-conditional-formatting-in-excel-usi/)
- [Create Excel Workbook Python – Full Guide to Styling & Conditional Formatting](/cells/english/python/formatting/create-excel-workbook-python-full-guide-to-styling-condition/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}