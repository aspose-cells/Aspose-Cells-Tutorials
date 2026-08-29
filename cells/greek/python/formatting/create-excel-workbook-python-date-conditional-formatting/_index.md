---
category: general
date: 2026-08-08
description: Δημιουργήστε βιβλίο εργασίας Excel με Python και προσθέστε μορφοποίηση
  υπό όρους βάσει ημερομηνίας. Οδηγός βήμα‑βήμα χρησιμοποιώντας το Aspose.Cells για
  να επισημάνετε τα κελιά της χθεσινής ημέρας.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- conditional formatting based on date
- Aspose.Cells Python example
- Excel date formatting Python
- Python Excel automation
language: el
lastmod: 2026-08-08
og_description: Δημιουργήστε βιβλίο εργασίας Excel με Python και Aspose.Cells και
  εφαρμόστε μορφοποίηση υπό όρους βάσει ημερομηνίας για δυναμικά φύλλα εργασίας.
og_image_alt: Screenshot of an Excel sheet created with Python showing cells highlighted
  by date conditional formatting
og_title: Δημιουργία βιβλίου εργασίας Excel με Python – μορφοποίηση υπό όρους ημερομηνίας
schemas:
- author: Aspose
  dateModified: '2026-08-08'
  description: Create Excel workbook Python and add conditional formatting based on
    date. Step‑by‑step guide using Aspose.Cells to highlight yesterday’s cells.
  headline: Create Excel workbook Python date conditional formatting
  type: TechArticle
tags:
- Python
- Excel
- Aspose.Cells
title: Δημιουργία βιβλίου εργασίας Excel με Python και μορφοποίηση υπό συνθήκη ημερομηνίας
url: /el/python/formatting/create-excel-workbook-python-date-conditional-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία βιβλίου εργασίας Excel με Python και μορφοποίηση υπό συνθήκη βάσει ημερομηνίας

Αν χρειάζεστε **create Excel workbook Python** και αυτόματα να επισημαίνετε κελιά που ταιριάζουν με συγκεκριμένη ημερομηνία, αυτό το tutorial σας δείχνει ακριβώς πώς. Θα μάθετε να εφαρμόζετε **conditional formatting based on date** ώστε οι ημερομηνίες του χθες να φωτίζονται σε ροζ, χρησιμοποιώντας τη βιβλιοθήκη Aspose.Cells.

Ο οδηγός περνάει από κάθε βήμα — από την εγκατάσταση του SDK μέχρι την αποθήκευση του τελικού αρχείου .xlsx — ώστε να μπορείτε να αντιγράψετε‑επικολλήσετε ένα λειτουργικό παράδειγμα στο δικό σας έργο. Δεν απαιτείται εξωτερική τεκμηρίωση· όλος ο κώδικας και οι εξηγήσεις είναι αυτοσχέδια.

## Προαπαιτούμενα

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

* Python 3.8 ή νεότερη έκδοση εγκατεστημένη.  
* Πακέτο `aspose-cells` (το Python wrapper για Aspose.Cells). Εγκαταστήστε το με:
  ```bash
  pip install aspose-cells
  ```
* Βασική εξοικείωση με Python και έννοιες του Excel όπως φύλλα εργασίας και στυλ κελιών.

> **Pro tip:** Το Aspose.Cells λειτουργεί χωρίς την εγκατάσταση του Microsoft Excel, καθιστώντας το ιδανικό για αυτοματοποίηση στο διακομιστή.

## Βήμα 1: Δημιουργία του βιβλίου εργασίας Excel σε Python

Η πρώτη εργασία είναι η δημιουργία ενός νέου workbook και η λήψη του προεπιλεγμένου worksheet. Αυτό το αντικείμενο αντιπροσωπεύει ολόκληρο το αρχείο Excel και παρέχει πρόσβαση σε γραμμές, στήλες και APIs μορφοποίησης.

```python
from aspose.cells import Workbook, SaveFormat

# Create a new workbook – this automatically adds one worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]   # reference to the first (default) sheet
```

Η δημιουργία του workbook είναι η βάση για οποιαδήποτε περαιτέρω επεξεργασία, είτε προσθέτετε δεδομένα, τύπους ή κανόνες μορφοποίησης.

## Βήμα 2: Ορισμός μορφοποίησης υπό συνθήκη βάσει ημερομηνίας

Τώρα προσθέτουμε **conditional formatting based on date**. Η απαρίθμηση `FormatConditionType.TIME_PERIOD` μας επιτρέπει να ορίσουμε ενσωματωμένες χρονικές περιόδους όπως Yesterday, Today ή LastWeek.

```python
from aspose.cells import FormatConditionType, BackgroundType, TimePeriodType
from aspose.pydrawing import Color

# Target range I19:K20 – three columns by two rows
range_obj = worksheet.get_range("I19:K20")
conditions = range_obj.format_conditions

# Add a new time‑period condition (e.g., Yesterday)
condition_index = conditions.add_condition(FormatConditionType.TIME_PERIOD)
condition = conditions[condition_index]

# Set the visual style: pink solid background
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID

# Specify that the condition should trigger for "Yesterday"
condition.time_period = TimePeriodType.YESTERDAY
```

Γιατί είναι σημαντικό αυτό το βήμα: Το Excel αξιολογεί τη συνθήκη για κάθε κελί στην περιοχή. Όταν η τιμή ενός κελιού εμπίπτει στην καθορισμένη περίοδο (χθες), το στυλ που ορίσαμε εφαρμόζεται αυτόματα.

## Βήμα 3: Συμπλήρωση της περιοχής με δείγμα ημερομηνιών

Για να δείτε τον κανόνα σε δράση, γράφουμε μερικά αντικείμενα `datetime` στα επιλεγμένα κελιά. Ένα από αυτά έχει οριστεί σκόπιμα στην ημερομηνία του χθες σε σχέση με το εσωτερικό σύστημα ημερομηνιών του workbook.

```python
from datetime import datetime

# Cell I19 – yesterday’s date (will be highlighted)
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))   # This date matches the "Yesterday" rule
style_i19 = cell_i19.get_style()
style_i19.number = 30                       # Excel’s built‑in date format
cell_i19.set_style(style_i19)

# Cell K20 – a random later date (no highlight)
cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))    # Not yesterday, so no formatting
style_k20 = cell_k20.get_style()
style_k20.number = 30
cell_k20.set_style(style_k20)

# Optional label for clarity
worksheet.cells.get("I20").put_value("Yesterday")
```

Η γραμμή `number = 30` λέει στο Excel να εμφανίσει την τιμή χρησιμοποιώντας το τυπικό σύντομο μορφότυπο ημερομηνίας. Μπορείτε να αλλάξετε αυτόν τον δείκτη σε οποιονδήποτε ενσωματωμένο αριθμητικό μορφότυπο αν προτιμάτε διαφορετική παρουσίαση.

## Βήμα 4: Προσαρμογή του πλάτους στήλης για ευανάγνωστη εμφάνιση

Η αυτόματη προσαρμογή του πλάτους της στήλης που περιέχει τις ημερομηνίες κάνει το αποτέλεσμα πιο ευανάγνωστο, ειδικά όταν το workbook ανοίγει στο Excel ή σε προβολέα.

```python
# Column 12 corresponds to column L (zero‑based indexing)
worksheet.auto_fit_column(12)
```

## Βήμα 5: Αποθήκευση του workbook στον δίσκο

Τέλος, αποθηκεύστε το workbook ως αρχείο .xlsx. Αντικαταστήστε το `"YOUR_DIRECTORY"` με πραγματική διαδρομή στο σύστημά σας.

```python
import os

output_path = os.path.join("YOUR_DIRECTORY", "TimePeriodDemo.out.xlsx")
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

Όταν ανοίξετε το `TimePeriodDemo.out.xlsx` στο Excel, το κελί **I19** θα εμφανιστεί με ροζ φόντο επειδή η τιμή του ταιριάζει με τον κανόνα “Yesterday”, ενώ το **K20** παραμένει αμετάβλητο.

### Αναμενόμενο αποτέλεσμα

| I19 (ημερομηνία) | I20 (ετικέτα) | J19 | J20 | K19 | K20 (ημερομηνία) |
|------------------|--------------|-----|-----|-----|-----------------|
| *2008‑07‑30* (ροζ φόντο) | Χθες | – | – | – | *2008‑08‑03* (χωρίς μορφοποίηση) |

Η ροζ σκίαση επιβεβαιώνει ότι **conditional formatting based on date** λειτουργεί όπως προβλέπεται.

## Κοινές παραλλαγές και ειδικές περιπτώσεις

| Κατάσταση | Πώς να προσαρμόσετε τον κώδικα |
|-----------|-------------------------------|
| **Επισήμανση “Σήμερα” αντί για “Χθες”** | Αλλάξτε `condition.time_period = TimePeriodType.TODAY` |
| **Εφαρμογή του κανόνα σε ολόκληρη τη στήλη** | Χρησιμοποιήστε `worksheet.get_range("A:A").format_conditions` |
| **Χρήση προσαρμοσμένου εύρους ημερομηνιών (π.χ., τις τελευταίες 7 ημέρες)** | Αντικαταστήστε την συνθήκη χρονικής περιόδου με συνθήκη τύπου: <br>```python<br>condition = conditions.add_condition(FormatConditionType.FORMULA)<br>condition.formula1 = 'AND(A1>=TODAY()-7, A1<=TODAY())'<br>``` |
| **Διαφορετικά χρώματα φόντου** | Ορίστε `condition.style.background_color = Color.light_green` (ή οποιοδήποτε `Color` προτιμάτε) |
| **Εκτέλεση σε Linux χωρίς οθόνη** | Το Aspose.Cells είναι πλήρως headless· δεν απαιτείται επιπλέον διαμόρφωση. |

## Πλήρες, εκτελέσιμο παράδειγμα

Παρακάτω βρίσκεται το πλήρες script που μπορείτε να εκτελέσετε όπως είναι (αφού ενημερώσετε το φάκελο εξόδου). Όλες οι εισαγωγές, τα σχόλια και τα βασικά στοιχεία διαχείρισης σφαλμάτων περιλαμβάνονται.

```python
# -*- coding: utf-8 -*-
"""
Create Excel workbook Python with date conditional formatting.
Demonstrates how to highlight yesterday’s dates using Aspose.Cells.
"""

import os
from datetime import datetime
from aspose.cells import (
    Workbook, SaveFormat,
    FormatConditionType, BackgroundType,
    TimePeriodType
)
from aspose.pydrawing import Color

# ----------------------------------------------------------------------
# 1️⃣ Initialize workbook
# ----------------------------------------------------------------------
workbook = Workbook()
worksheet = workbook.worksheets[0]

# ----------------------------------------------------------------------
# 2️⃣ Add conditional formatting for "Yesterday"
# ----------------------------------------------------------------------
range_obj = worksheet.get_range("I19:K20")
conditions = range_obj.format_conditions
cond_idx = conditions.add_condition(FormatConditionType.TIME_PERIOD)
condition = conditions[cond_idx]

# Visual style: pink solid fill
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID
condition.time_period = TimePeriodType.YESTERDAY

# ----------------------------------------------------------------------
# 3️⃣ Populate sample dates
# ----------------------------------------------------------------------
# Cell that should match the condition
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))   # Yesterday relative to demo data
style_i19 = cell_i19.get_style()
style_i19.number = 30                       # Excel short‑date format
cell_i19.set_style(style_i19)

# Cell that does NOT match
cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))
style_k20 = cell_k20.get_style()
style_k20.number = 30
cell_k20.set_style(style_k20)

# Optional label
worksheet.cells.get("I20").put_value("Yesterday")

# ----------------------------------------------------------------------
# 4️⃣ Auto‑fit column for better visibility
# ----------------------------------------------------------------------
worksheet.auto_fit_column(12)   # Column L (0‑based index)

# ----------------------------------------------------------------------
# 5️⃣ Save workbook
# ----------------------------------------------------------------------
output_dir = "YOUR_DIRECTORY"   # <-- replace with a real folder
os.makedirs(output_dir, exist_ok=True)
output_path = os.path.join(output_dir, "TimePeriodDemo.out.xlsx")
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

Η εκτέλεση του script παράγει ένα αρχείο Excel όπου το κελί “Yesterday” επισημαίνεται αυτόματα, δείχνοντας πώς **create Excel workbook Python** συνδυάζεται με **conditional formatting based on date**.

## Συμπέρασμα

Τώρα γνωρίζετε πώς να δημιουργείτε αντικείμενα **create Excel workbook Python**, να ορίζετε μια **date‑based conditional formatting**  

## Τι πρέπει να μάθετε στη συνέχεια;

Οι παρακάτω οδηγίες καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικά παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε επιπλέον δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στα δικά σας έργα.

- [Δημιουργία βιβλίου εργασίας Excel χρησιμοποιώντας Aspose.Cells σε Java: Οδηγός βήμα‑βήμα](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [Δημιουργία βιβλίου εργασίας Excel με γραφήματα χρησιμοποιώντας Aspose.Cells .NET | Οδηγός βήμα‑βήμα](/cells/english/net/charts-graphs/create-excel-workbook-charts-aspose-cells-net/)
- [Αυτοματοποίηση Excel: Δημιουργία βιβλίου εργασίας και προσθήκη ListBox χρησιμοποιώντας Aspose.Cells για .NET](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}