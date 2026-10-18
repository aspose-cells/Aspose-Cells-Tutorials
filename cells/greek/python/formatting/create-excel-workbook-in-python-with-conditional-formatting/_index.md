---
category: general
date: 2026-09-05
description: Δημιουργήστε βιβλίο εργασίας Excel σε Python και προσθέστε μορφοποίηση
  υπό όρους για να επισημάνετε τα κελιά της χθεσινής ημέρας. Μάθετε τον πλήρη κώδικα
  και γιατί κάθε βήμα είναι σημαντικό.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- add conditional formatting excel
- highlight cells based on date
- add conditional formatting range
- how to highlight yesterday cells
language: el
lastmod: 2026-09-05
og_description: Δημιουργήστε βιβλίο εργασίας Excel σε Python και προσθέστε μορφοποίηση
  υπό όρους για να επισημάνετε τα κελιά της χθεσινής ημέρας. Ακολουθήστε αυτόν τον
  οδηγό βήμα‑προς‑βήμα για μια πλήρη λύση.
og_image_alt: Screenshot of an Excel sheet where cells are highlighted after creating
  Excel workbook in Python
og_title: Δημιουργία βιβλίου εργασίας Excel σε Python – προσθήκη μορφοποίησης υπό
  όρους
schemas:
- author: Aspose
  dateModified: '2026-09-05'
  description: Create Excel workbook in Python and add conditional formatting to highlight
    yesterday cells. Learn the full code and why each step matters.
  headline: Create Excel workbook in Python with conditional formatting
  type: TechArticle
tags:
- Excel
- Python
- Aspose.Cells
- Conditional Formatting
title: Δημιουργία βιβλίου εργασίας Excel σε Python με μορφοποίηση υπό όρους
url: /el/python/formatting/create-excel-workbook-in-python-with-conditional-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία βιβλίου εργασίας Excel σε Python με μορφοποίηση υπό όρους

Αν χρειάζεστε **create Excel workbook python** για μια εργασία αναφοράς, αυτός ο οδηγός σας δείχνει πώς να δημιουργήσετε ένα βιβλίο εργασίας και να εφαρμόσετε έναν κανόνα μορφοποίησης υπό όρους που επισημαίνει τις ημερομηνίες του χθες. Θα δείτε τον ακριβή κώδικα, γιατί υπάρχει κάθε γραμμή, και πώς να προσαρμόσετε τη λύση για άλλες χρονικές περιόδους.

Η μορφοποίηση υπό όρους είναι ένας ισχυρός τρόπος να τραβήξετε την προσοχή σε δεδομένα που ικανοποιούν μια συγκεκριμένη προϋπόθεση. Σε αυτό το tutorial χρησιμοποιούμε τη βιβλιοθήκη Aspose.Cells για Python via .NET, η οποία παρέχει πλήρη υποστήριξη λειτουργιών του Excel χωρίς να απαιτείται το Microsoft Office. Στο τέλος του οδηγού θα έχετε ένα αρχείο όπου τα κελιά στην περιοχή *I19:K20* γίνονται ροζ όταν περιέχουν την ημερομηνία του χθες.

## Προαπαιτούμενα

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

* Python 3.9+ εγκατεστημένο
* Πακέτο `aspose-cells` (εγκατάσταση με `pip install aspose-cells`)
* Βασική εξοικείωση με τη σύνταξη της Python
* Δικαιώματα εγγραφής στον φάκελο όπου θα αποθηκευτεί το βιβλίο εργασίας

Ο κώδικας λειτουργεί σε Windows, macOS και Linux εφόσον είναι διαθέσιμο το .NET runtime.

## Δημιουργία βιβλίου εργασίας Excel σε Python

Το πρώτο βήμα είναι η δημιουργία ενός αντικειμένου `Workbook` και η λήψη του προεπιλεγμένου φύλλου εργασίας. Αυτό το αντικείμενο αντιπροσωπεύει ολόκληρο το αρχείο Excel στη μνήμη.

```python
from aspose.cells import Workbook, SaveFormat

# Create a new workbook and select the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]
```

*Γιατί είναι σημαντικό*: `Workbook()` δημιουργεί ένα κενό βιβλίο εργασίας με ένα φύλλο. Η πρόσβαση στο `worksheets[0]` σας δίνει έναν δείκτη για να προσθέσετε δεδομένα, στυλ και μορφοποίηση αργότερα.

## Προσθήκη περιοχής μορφοποίησης υπό όρους

Στη συνέχεια ορίζουμε την περιοχή που θα αξιολογείται από τον κανόνα μορφοποίησης. Η περιοχή `I19:K20` καλύπτει έξι κελιά σε δύο σειρές.

```python
# Define the range that will receive the conditional formatting rule
condition_collection = worksheet.conditional_formattings.add("I19:K20")
```

*Γιατί είναι σημαντικό*: Η προσθήκη μιας συλλογής μορφοποίησης υπό όρους σε συγκεκριμένη περιοχή απομονώνει τον κανόνα, αποτρέποντας την επηρεασία μη σχετικών κελιών. Αυτό ικανοποιεί την απαίτηση **add conditional formatting range**.

## Ορισμός του κανόνα: επισήμανση κελιών βάσει ημερομηνίας

Τώρα δημιουργούμε μια συνθήκη τύπου `TIME_PERIOD`. Αυτό λέει στο Excel να συγκρίνει την τιμή κάθε κελιού με ένα προ‑ορισμένο χρονικό παράθυρο.

```python
from aspose.cells import FormatConditionType, TimePeriodType

# Add a TIME_PERIOD condition to the collection
condition_index = condition_collection.add_condition(FormatConditionType.TIME_PERIOD)
condition = condition_collection[condition_index]

# Set the time period to “Yesterday”
condition.time_period = TimePeriodType.YESTERDAY
```

*Γιατί είναι σημαντικό*: `TIME_PERIOD` είναι ο μοναδικός ενσωματωμένος τύπος που υποστηρίζει άμεσα “Yesterday”, “Today”, “Last Week” κ.λπ. Ορίζοντας `condition.time_period` σε `YESTERDAY`, ο κανόνας αξιολογεί αυτόματα την ημερομηνία του κάθε κελιού σε σχέση με την ημέρα πριν από την τρέχουσα.

## Στυλ των κελιών που ικανοποιούν τη συνθήκη

Η μορφοποίηση υπό όρους χρειάζεται επίσης ένα οπτικό στυλ. Εδώ επιλέγουμε γεμιστό ροζ χρώμα για να ξεχωρίζουν τα κελιά που ταιριάζουν.

```python
from aspose.pydrawing import Color as DrawingColor
from aspose.cells import BackgroundType

# Apply a pink solid background to cells that satisfy the condition
condition.style.background_color = DrawingColor.pink
condition.style.pattern = BackgroundType.SOLID
```

*Γιατί είναι σημαντικό*: Το αντικείμενο στυλ ορίζει πώς θα αποτυπώσει το Excel τα κελιά που ικανοποιούν τη συνθήκη. Η χρήση γεμιστού ροζ χρώματος ικανοποιεί την απαίτηση **highlight cells based on date** και κάνει το αποτέλεσμα εύκολο στην επαλήθευση.

## Συμπλήρωση δείγματος ημερομηνιών για αξιολόγηση

Για να δείτε τον κανόνα σε δράση, εισάγουμε δύο ημερομηνίες — μία που αντιστοιχεί στην ημερομηνία του χθες και μία που δεν αντιστοιχεί. Η μορφή `number` `30` αντιστοιχεί στην ενσωματωμένη μορφή ημερομηνίας `mm-dd-yy`.

```python
from datetime import datetime

# Cell I19: a date that matches “Yesterday”
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))   # Example date; adjust as needed
cell_i19.style.number = 30
cell_i19.set_style(cell_i19.style)

# Cell K20: a date outside the “Yesterday” period
cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))    # Example date; adjust as needed
cell_k20.style.number = 30
cell_k20.set_style(cell_k20.style)

# Optional label for the range
worksheet.cells.get("I20").put_value("Yesterday")
```

*Γιατί είναι σημαντικό*: Η παροχή τόσο μιας ταιριαστής όσο και μιας μη ταιριαστής ημερομηνίας σας επιτρέπει να επαληθεύσετε ότι η μορφοποίηση υπό όρους λειτουργεί σωστά. Προσαρμόστε τις ημερομηνίες στον τρέχοντα μήνα όταν εκτελείτε το script, ή αντικαταστήστε τες με δυναμικές τιμές.

## Αποθήκευση του βιβλίου εργασίας

Τέλος, γράφουμε το αρχείο στο δίσκο. Η σταθερά `SaveFormat.XLSX` διασφαλίζει ότι η έξοδος είναι σύγχρονο αρχείο Excel.

```python
output_path = "YOUR_DIRECTORY/TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

*Γιατί είναι σημαντικό*: Η αποθήκευση του βιβλίου εργασίας σας επιτρέπει να το ανοίξετε στο Excel, LibreOffice ή οποιονδήποτε προβολέα που υποστηρίζει XLSX. Η εκτύπωση της διαδρομής επιβεβαιώνει πού γράφτηκε το αρχείο.

## Πλήρες script

Συνδυάζοντας όλα τα κομμάτια, το πλήρες, εκτελέσιμο script είναι το εξής:

```python
# -*- coding: utf-8 -*-
"""
Create an Excel workbook in Python, add a conditional formatting rule,
and highlight yesterday's cells.
"""

from aspose.cells import (
    Workbook, SaveFormat, FormatConditionType,
    BackgroundType, TimePeriodType
)
from aspose.pydrawing import Color as DrawingColor
from datetime import datetime

# Step 1: Create a new workbook and access the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Step 2: Add a conditional formatting rule for the range I19:K20
condition_collection = worksheet.conditional_formattings.add("I19:K20")
condition_index = condition_collection.add_condition(FormatConditionType.TIME_PERIOD)
condition = condition_collection[condition_index]

# Step 3: Define the visual style for cells that meet the condition
condition.style.background_color = DrawingColor.pink
condition.style.pattern = BackgroundType.SOLID

# Step 4: Set the time‑period to “Yesterday”
condition.time_period = TimePeriodType.YESTERDAY

# Step 5: Populate sample dates for evaluation
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))   # yesterday relative to the example
cell_i19.style.number = 30
cell_i19.set_style(cell_i19.style)

cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))    # outside the period
cell_k20.style.number = 30
cell_k20.set_style(cell_k20.style)

# Step 6: Add a label for the formatted range
worksheet.cells.get("I20").put_value("Yesterday")

# Step 7: Save the workbook
output_path = "YOUR_DIRECTORY/TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

### Αναμενόμενο αποτέλεσμα

Όταν ανοίξετε το `TimePeriodExample.xlsx`:

* Το κελί **I19** εμφανίζεται με ροζ φόντο επειδή η τιμή του ταιριάζει με το χθες.
* Το κελί **K20** διατηρεί το προεπιλεγμένο φόντο επειδή η ημερομηνία του είναι εκτός της περιόδου.
* Η ετικέτα **“Yesterday”** βρίσκεται στο κελί I20 για σαφήνεια.

## Κοινές παραλλαγές και ακραίες περιπτώσεις

| Κατάσταση | Προσαρμογή |
|-----------|------------|
| **Επισήμανση της σημερινής ημέρας αντί του χθες** | Αλλάξτε `condition.time_period = TimePeriodType.TODAY`. |
| **Εφαρμογή του κανόνα σε μεγαλύτερη περιοχή** | Ενημερώστε το string περιοχής στο `add("I19:K20")` σε κάτι όπως `"A1:Z100"`. |
| **Χρήση διαφορετικού χρώματος γεμίσματος** | Αντικαταστήστε `DrawingColor.pink` με οποιοδήποτε άλλο `DrawingColor` (π.χ., `DrawingColor.light_green`). |
| **Εργασία με δυναμικές ημερομηνίες** | Υπολογίστε `datetime.now() - timedelta(days=1)` για το χθες και γράψτε αυτήν την τιμή στα κελιά πριν εφαρμόσετε τον κανόνα. |

**Συμβουλή:** Όταν δημιουργείτε το βιβλίο εργασίας προγραμματιστικά για πολλούς χρήστες, κρατήστε τον ορισμό της μορφοποίησης υπό όρους ξεχωριστό από την εισαγωγή δεδομένων. Έτσι μπορείτε να επαναχρησιμοποιήσετε το ίδιο στυλ σε πολλά φύλλα χωρίς να διπλασιάζετε κώδικα.

## Επαλήθευση του αποτελέσματος προγραμματιστικά (προαιρετικό)

Αν θέλετε να επιβεβαιώσετε τη μορφοποίηση χωρίς να ανοίξετε το Excel, μπορείτε να ελέγξετε το στυλ ενός κελιού μετά την αποθήκευση:



## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά σχετικές θεματικές που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κυριαρχήσετε επιπλέον δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Excel Automation: Create a Workbook and Add a ListBox Using Aspose.Cells for .NET](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)
- [Create Excel Workbook and Add Labels with Aspose.Cells for Java](/cells/english/java/advanced-excel-charts/data-labeling/)
- [Excel Automation Create Workbook Add Listbox Aspose Cells](/cells/german/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}