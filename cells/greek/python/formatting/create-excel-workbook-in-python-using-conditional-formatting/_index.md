---
category: general
date: 2026-09-21
description: Μάθετε πώς να δημιουργήσετε ένα βιβλίο εργασίας Excel σε Python, να ορίσετε
  το χρώμα φόντου των κελιών και να εφαρμόσετε μορφοποίηση υπό όρους βάσει ημερομηνίας
  με το Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- format cells by date
- excel conditional formatting python
- date based conditional formatting
language: el
lastmod: 2026-09-21
og_description: Δημιουργήστε βιβλίο εργασίας Excel σε Python, ορίστε το χρώμα φόντου
  των κελιών και εφαρμόστε μορφοποίηση υπό όρους βάσει ημερομηνίας χρησιμοποιώντας
  το Aspose.Cells. Ακολουθήστε τον οδηγό βήμα‑βήμα.
og_image_alt: Screenshot of an Excel sheet showing a yellow‑green cell background
  for yesterday's dates
og_title: Δημιουργία βιβλίου εργασίας Excel σε Python με μορφοποίηση υπό όρους
schemas:
- author: Aspose
  dateModified: '2026-09-21'
  description: Learn how to create Excel workbook in Python, set cell background color,
    and apply date based conditional formatting with Aspose.Cells.
  headline: Create Excel workbook in Python using conditional formatting
  type: TechArticle
tags:
- Python
- Excel
- Aspose.Cells
title: Δημιουργία βιβλίου εργασίας Excel σε Python με μορφοποίηση υπό συνθήκη
url: /el/python/formatting/create-excel-workbook-in-python-using-conditional-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία βιβλίου εργασίας Excel σε Python με μορφοποίηση υπό όρους

Αν χρειάζεστε **scripts create Excel workbook python** που επισημαίνουν αυτόματα ημερομηνίες, αυτός ο οδηγός σας δείχνει ακριβώς πώς. Θα δείτε πώς να **ορίσετε το χρώμα φόντου κελιού**, να προσθέσετε έναν κανόνα “Yesterday”, και να αποθηκεύσετε το αρχείο—όλα με το Aspose.Cells for Python.

Η εργασία με αρχεία Excel προγραμματιστικά συχνά σημαίνει επανάληψη της ίδιας λογικής μορφοποίησης σε πολλά φύλλα. Στο τέλος αυτού του tutorial θα έχετε ένα επαναχρησιμοποιήσιμο μοτίβο για **excel conditional formatting python** που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο.

## Προαπαιτούμενα

- Python 3.8+ εγκατεστημένο  
- Πακέτο `aspose-cells` (`pip install aspose-cells`)  
- Βασική εξοικείωση με συναρτήσεις Python και το module datetime  

Δεν απαιτούνται πρόσθετες βιβλιοθήκες· το Aspose.Cells διαχειρίζεται όλες τις λειτουργίες Excel.

## Βήμα 1: Δημιουργία του βιβλίου εργασίας και πρόσβαση στο πρώτο φύλλο

Το πρώτο βήμα είναι να **create excel workbook python** αντικείμενα και να πάρετε το προεπιλεγμένο φύλλο. Αυτό σας δίνει έναν καθαρό καμβά για περαιτέρω στυλιζάρισμα.

```python
# Import required Aspose.Cells classes
from aspose.cells import (
    Workbook, FormatConditionType, TimePeriodType,
    BackgroundType, Color, SaveFormat
)
from datetime import datetime
import os

# Create a new workbook; the first worksheet is at index 0
workbook = Workbook()
worksheet = workbook.worksheets[0]
```

*Γιατί είναι σημαντικό:* `Workbook()` δημιουργεί ένα Excel αρχείο στη μνήμη. Η πρόσβαση στο `worksheets[0]` αποφεύγει το σκληρό κωδικοποίηση ονομάτων φύλλων και λειτουργεί ακόμη και αν το προεπιλεγμένο όνομα αλλάξει.

## Βήμα 2: Βοηθητική συνάρτηση για προσθήκη μορφοποίησης υπό όρους TIME_PERIOD

Για να διατηρήσουμε τον κώδικα τακτοποιημένο, τυλίγουμε τη δημιουργία conditional‑format σε μια βοηθητική συνάρτηση. Λαμβάνει μια περιοχή κελιών, ένα χρώμα φόντου, και τον επιθυμητό κανόνα χρονικής περιόδου.

```python
def add_time_period(sheet, cell_range, bg_color, period_type):
    """
    Adds a TIME_PERIOD conditional formatting rule to `cell_range`.
    The rule paints the cells with `bg_color` when the date matches `period_type`.
    """
    # Retrieve (or create) the ConditionalFormatting collection for the range
    cf = sheet.conditional_formattings.get(cell_range)
    if cf is None:
        cf = sheet.conditional_formattings.add(cell_range)

    # Insert a TIME_PERIOD condition and configure its style
    idx = cf.add_condition(FormatConditionType.TIME_PERIOD)
    condition = cf[idx]
    condition.style.background_color = bg_color          # set cell background color
    condition.style.pattern = BackgroundType.SOLID
    condition.time_period = period_type                # e.g., TimePeriodType.YESTERDAY
```

*Γιατί είναι σημαντικό:* Η βοηθητική συνάρτηση αφαιρεί τα επαναλαμβανόμενα βήματα δημιουργίας conditional format, καθιστώντας εύκολη την επαναχρησιμοποίηση για άλλους κανόνες βάσει ημερομηνίας όπως “Today” ή “Last Week”.

## Βήμα 3: Εφαρμογή του κανόνα “Yesterday” σε μια περιοχή

Τώρα χρησιμοποιούμε τη βοηθητική συνάρτηση για να επισημάνουμε κελιά που περιέχουν την ημερομηνία του χθες. Η περιοχή `I19:K20` θα γίνει **medium sea green** όταν πληρωθεί η προϋπόθεση.

```python
add_time_period(
    worksheet,
    "I19:K20",                # range to format
    Color.medium_sea_green,  # set cell background color
    TimePeriodType.YESTERDAY # date based conditional formatting
)
```

*Γιατί είναι σημαντικό:* `TimePeriodType.YESTERDAY` είναι μέρος της ενσωματωμένης αρίθμησης του Aspose.Cells, οπότε δεν χρειάζεται να υπολογίζετε τις ημερομηνίες χειροκίνητα. Η βιβλιοθήκη αξιολογεί τον κανόνα κάθε φορά που ανοίγει το βιβλίο εργασίας.

## Βήμα 4: Συμπλήρωση της περιοχής με δείγμα ημερομηνιών

Για να δείτε τον κανόνα σε δράση, γράφουμε δύο ημερομηνίες—μία που ταιριάζει με το “Yesterday” και μία που δεν ταιριάζει. Το στυλ `number` `30` αντιστοιχεί σε ενσωματωμένη μορφή ημερομηνίας.

```python
# Cell I19 gets a date that is exactly yesterday (relative to the sample data)
cell = worksheet.cells.get("I19")
cell.put_value(datetime(2008, 7, 30))   # 30 July 2008
cell.style.number = 30                # date format

# Cell K20 gets a date that is outside the rule
cell = worksheet.cells.get("K20")
cell.put_value(datetime(2008, 8, 3))    # 3 August 2008
cell.style.number = 30
```

*Γιατί είναι σημαντικό:* Εισάγοντας συγκεκριμένες ημερομηνίες μπορείτε να επαληθεύσετε ότι η conditional formatting λειτουργεί χωρίς να χρειάζεται να ανοίξετε το αρχείο μια συγκεκριμένη μέρα.

## Βήμα 5: Προσθήκη περιγραφικής ετικέτας και αυτόματη προσαρμογή στήλης

Μια μικρή ετικέτα διευκρινίζει τον σκοπό της μορφοποιημένης περιοχής, και το `auto_fit_column` κάνει το φύλλο ευανάγνωστο.

```python
# Add a label under the formatted range
worksheet.cells.get("I20").put_value("Yesterday")

# Adjust column width for better visibility (column 12 = L)
worksheet.auto_fit_column(12)
```

## Βήμα 6: Αποθήκευση του βιβλίου εργασίας

Τέλος, γράφουμε το βιβλίο εργασίας στο δίσκο. Η κλήση `os.makedirs` εξασφαλίζει ότι ο φάκελος προορισμού υπάρχει.

```python
output_path = os.path.join("YOUR_DIRECTORY", "TimePeriodDemo.xlsx")
os.makedirs(os.path.dirname(output_path), exist_ok=True)

# Save as XLSX – the most widely supported Excel format
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

Όταν ανοίξετε το *TimePeriodDemo.xlsx* θα δείτε:

- Το κελί **I19** σκιαγραφημένο **medium sea green** επειδή η τιμή του ταιριάζει με τον κανόνα “Yesterday”.  
- Το κελί **K20** διατηρεί το προεπιλεγμένο φόντο επειδή η ημερομηνία του δεν ικανοποιεί την προϋπόθεση.  

Αυτό δείχνει **format cells by date** χρησιμοποιώντας μια μόνο γραμμή κώδικα Python.

## Πλήρες, εκτελέσιμο παράδειγμα

Συνδυάζοντας όλα τα κομμάτια, εδώ είναι το πλήρες script που μπορείτε να αντιγράψετε‑και‑επικολλήσετε και να τρέξετε:

```python
from aspose.cells import (
    Workbook, FormatConditionType, TimePeriodType,
    BackgroundType, Color, SaveFormat
)
from datetime import datetime
import os

# 1️⃣ Create workbook and get first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# 2️⃣ Helper to add TIME_PERIOD conditional formatting
def add_time_period(sheet, cell_range, bg_color, period_type):
    cf = sheet.conditional_formattings.get(cell_range)
    if cf is None:
        cf = sheet.conditional_formattings.add(cell_range)
    idx = cf.add_condition(FormatConditionType.TIME_PERIOD)
    condition = cf[idx]
    condition.style.background_color = bg_color
    condition.style.pattern = BackgroundType.SOLID
    condition.time_period = period_type

# 3️⃣ Apply “Yesterday” rule (set cell background color)
add_time_period(
    worksheet,
    "I19:K20",
    Color.medium_sea_green,
    TimePeriodType.YESTERDAY
)

# 4️⃣ Fill sample dates (format cells by date)
cell = worksheet.cells.get("I19")
cell.put_value(datetime(2008, 7, 30))
cell.style.number = 30

cell = worksheet.cells.get("K20")
cell.put_value(datetime(2008, 8, 3))
cell.style.number = 30

# 5️⃣ Add label and auto‑fit column
worksheet.cells.get("I20").put_value("Yesterday")
worksheet.auto_fit_column(12)

# 6️⃣ Save the workbook
output_path = os.path.join("YOUR_DIRECTORY", "TimePeriodDemo.xlsx")
os.makedirs(os.path.dirname(output_path), exist_ok=True)
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

Τρέξτε το script, ανοίξτε το παραγόμενο αρχείο, και θα δείτε τη conditional formatting σε δράση.

## Συχνές παραλλαγές και ειδικές περιπτώσεις

| Παραλλαγή | Πώς να το υλοποιήσετε | Πότε να το χρησιμοποιήσετε |
|-----------|----------------------|---------------------------|
| **Επισήμανση “Today”** | Αντικαταστήστε `TimePeriodType.YESTERDAY` με `TimePeriodType.TODAY` | Πίνακες ελέγχου σε πραγματικό χρόνο |
| **Πολλαπλές περιοχές** | Καλέστε `add_time_period` για κάθε περιοχή, περνώντας διαφορετικά χρώματα | Πολύπλοκες αναφορές |
| **Δυναμική περιοχή ημερομηνιών** | Χρησιμοποιήστε `TimePeriodType.LAST_7_DAYS` ή `TimePeriodType.NEXT_MONTH` | Κυλιόμενες αναφορές |
| **Προσαρμοσμένο χρώμα** | Χρησιμοποιήστε `Color.from_argb(255, r, g, b)` για να δημιουργήσετε οποιαδήποτε απόχρωση | Στυλ σύμφωνο με την εταιρική ταυτότητα |

**Pro tip:** Πάντα ορίζετε `condition.style.pattern = BackgroundType.SOLID` όταν θέλετε γεμίσμα στερεό· διαφορετικά το Excel μπορεί να εμφανίσει διαβάθμιση που φαίνεται ασυνεπής μεταξύ εκδόσεων.

## Συμπέρασμα

Τώρα ξέρετε πώς να **create Excel workbook python** scripts που **set cell background color**, εφαρμόζουν **excel conditional formatting python**, και **format cells by date** χρησιμοποιώντας το Aspose.Cells. Το παράδειγμα καλύπτει ένα σενάριο **date based conditional formatting**, αλλά το ίδιο μοτίβο λειτουργεί για οποιονδήποτε κανόνα χρονικής περιόδου.

Στη συνέχεια, μπορείτε να εξερευνήσετε:

- Προσθήκη data bars ή icon sets (`FormatConditionType.DATA_BAR`)  
- Συνδυασμό πολλαπλών conditional rules στην ίδια περιοχή  
- Εξαγωγή του βιβλίου εργασίας σε PDF (`SaveFormat.PDF`) για αναφορές  

Μη διστάσετε να πειραματιστείτε με διαφορετικά χρώματα, περιοχές, και τύπους χρονικής περιόδου ώστε να ταιριάζουν στις συγκεκριμένες ανάγκες αναφοράς σας. Καλός κώδικας!

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικά παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε επιπλέον δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στην υλοποίηση των δικών σας έργων.

- [Master Excel Cell Formatting and Workbook Management with Aspose.Cells for .NET](/cells/english/net/formatting/excel-formatting-aspose-cells-net/)
- [Excel Automation with Aspose.Cells .NET&#58; Create Workbook & Set External Links](/cells/english/net/automation-batch-processing/excel-automation-aspose-cells-net/)
- [How to Create Workbook Scoped Named Ranges in Excel Using Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}