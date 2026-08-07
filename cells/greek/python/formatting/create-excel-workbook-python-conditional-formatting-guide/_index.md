---
category: general
date: 2026-07-20
description: Δημιουργήστε βιβλίο εργασίας Excel με Python και Aspose.Cells, ορίστε
  το χρώμα φόντου των κελιών και προσθέστε μορφοποίηση υπό όρους με Python για να
  μορφοποιήσετε τα κελιά ανά ημερομηνία.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- format cells by date
- aspose cells conditional formatting
- add conditional formatting python
language: el
lastmod: 2026-07-20
og_description: Δημιουργήστε βιβλίο εργασίας Excel με Python χρησιμοποιώντας το Aspose.Cells.
  Μάθετε πώς να ορίσετε το χρώμα φόντου των κελιών και να προσθέσετε μορφοποίηση υπό
  όρους με Python για να μορφοποιήσετε τα κελιά κατά ημερομηνία.
og_image_alt: Screenshot of an Excel workbook created with Python showing conditional
  formatting applied to date cells
og_title: Δημιουργία βιβλίου εργασίας Excel με Python – Προσθήκη υπό συνθήκη μορφοποίησης
schemas:
- author: Aspose
  dateModified: '2026-07-20'
  description: Create Excel workbook Python with Aspose.Cells, set cell background
    color, and add conditional formatting python to style cells by date.
  headline: Create Excel Workbook Python – Conditional Formatting Guide
  type: TechArticle
- questions:
  - answer: Absolutely. Change `"I19:K20"` to any A1‑style range, and adjust the sample
      dates accordingly.
    question: Can I target a different date range?
  - answer: Use `FormatConditionType.FORMULA` and set `condition.formula1 = "YOUR_FORMULA"`—for
      example, `=TODAY()-A1=1` to mimic yesterday.
    question: What if I need a custom formula instead of `YESTERDAY`?
  - answer: Call `conditions.add_condition` again with a different `FormatConditionType`.
      The order matters; later rules can override earlier ones.
    question: How do I apply multiple rules to the same range?
  - answer: Yes—modify `condition.style.font.color = Color.white` (or any other `Color`).
    question: Is there a way to set font colour together with background?
  type: FAQPage
tags:
- Aspose.Cells
- Python
- Excel Automation
title: Δημιουργία βιβλίου εργασίας Excel με Python – Οδηγός μορφοποίησης υπό συνθήκες
url: /el/python/formatting/create-excel-workbook-python-conditional-formatting-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία Excel Workbook με Python – Οδηγός Μορφοποίησης υπό Συνθήκες

Έχετε αναρωτηθεί ποτέ πώς να **create Excel workbook Python** από την αρχή και να το κάνετε να φαίνεται επαγγελματικό χωρίς να ανοίξετε το UI; Δεν είστε μόνοι. Πολλοί προγραμματιστές συναντούν δυσκολίες όταν χρειάζεται να **set cell background color** ή να εφαρμόσουν στυλ βάσει ημερομηνίας προγραμματιστικά.  

Σε αυτό το tutorial θα περάσουμε βήμα-βήμα ένα πλήρες, εκτελέσιμο παράδειγμα που χρησιμοποιεί το Aspose.Cells για να **add conditional formatting python** κανόνες, να μορφοποιήσει κελιά βάσει ημερομηνίας και να αποθηκεύσει το αποτέλεσμα ως σύγχρονο αρχείο XLSX. Στο τέλος θα έχετε ένα αυτόνομο script που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο.

## Τι Θα Μάθετε

- Πώς να αρχικοποιήσετε ένα workbook και να αποκτήσετε το πρώτο worksheet.  
- Τρόποι για **set cell background color** για ολόκληρο ένα εύρος.  
- Χρήση του **aspose cells conditional formatting** για να επισημάνετε ημερομηνίες “Yesterday”.  
- Αυτόματη προσαρμογή στηλών και αποθήκευση του αρχείου στο δίσκο.  

Δεν απαιτείται εξωτερική διαμόρφωση—μόνο Python 3 και το πακέτο Aspose.Cells. Αν έχετε ήδη εγκαταστήσει το `aspose-cells`, είστε έτοιμοι· διαφορετικά, ένα γρήγορο `pip install aspose-cells` αρκεί.

## Προαπαιτούμενα

- Python 3.8+ (ο κώδικας λειτουργεί σε 3.9, 3.10 και νεότερες εκδόσεις).  
- Aspose.Cells for Python via .NET (`aspose-cells` NuGet wrapper).  
- Βασική εξοικείωση με τις έννοιες του Excel (cells, ranges, formatting).  

Τα έχετε; Τέλεια—ας βουτήξουμε.

## Δημιουργία Excel Workbook Python – Ρυθμίσεις και Worksheet

Πρώτα απ' όλα: χρειαζόμαστε ένα νέο αντικείμενο workbook και μια αναφορά στο προεπιλεγμένο worksheet. Αυτό είναι ο καμβάς όπου θα πραγματοποιηθούν όλες οι επόμενες ενέργειες.

```python
# Import the necessary Aspose.Cells classes
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime

# Step 1: Create a new workbook and grab the first sheet
workbook = Workbook()                     # create excel workbook python
worksheet = workbook.worksheets[0]        # default is the first worksheet
```

> **Γιατί είναι σημαντικό:** `Workbook()` δημιουργεί ένα Excel αρχείο στη μνήμη, εξαλείφοντας την ανάγκη για προσωρινά αρχεία. Η μεταβλητή `worksheet` είναι το σημείο εισόδου μας για ενέργειες σε επίπεδο κελιού.

## Ορισμός Χρώματος Φόντου Κελιού

Πριν προσθέσουμε κανόνες, είναι καλό να δώσουμε στο επιλεγμένο εύρος ένα βασικό χρώμα ώστε η μορφοποίηση υπό συνθήκες να ξεχωρίζει. Η βοηθητική συνάρτηση παρακάτω ανακτά (ή δημιουργεί) ένα `FormatConditionCollection` για ένα δεδομένο εύρος και χρωματίζει τα κελιά με ένα ενιαίο φόντο.

```python
def get_format_condition(cell_range: str, base_color: Color):
    """
    Obtain (or create) a FormatConditionCollection for `cell_range`.
    Also set a base background colour for the whole range.
    """
    # Retrieve or add a conditional formatting entry for the range
    condition_collection = worksheet.conditional_formattings.get(
        worksheet.conditional_formattings.add(cell_range)
    )
    # Apply the base colour to every cell in the range
    for cell_name in cell_range.split(":"):
        cell = worksheet.cells.get(cell_name)
        cell.style.background_color = base_color          # set cell background color
        cell.style.pattern = BackgroundType.SOLID
    return condition_collection
```

> **Συμβουλή:** Αν σκοπεύετε να επαναχρησιμοποιήσετε το ίδιο εύρος με πολλαπλούς κανόνες, καλέστε αυτή τη βοηθητική συνάρτηση μία φορά και κρατήστε τη συλλογή που επιστρέφει· εξοικονομεί μερικές κλήσεις API.

## Προσθήκη Μορφοποίησης Υπό Συνθήκες Python για Εύρη Ημερομηνίας

Τώρα το διασκεδαστικό μέρος: θα δημιουργήσουμε έναν κανόνα **time‑period conditional formatting** που επισημαίνει κελιά που περιέχουν την ημερομηνία του χθες. Αυτό δείχνει τη δύναμη του **format cells by date** χρησιμοποιώντας το Aspose.Cells.

```python
def apply_yesterday_rule():
    """
    Apply a “Yesterday” conditional formatting rule to the range I19:K20.
    Cells that match will turn pink; others stay with the base colour.
    """
    # Obtain the condition collection for the target range
    conditions = get_format_condition("I19:K20", Color.medium_sea_green)

    # Create a TIME_PERIOD condition (this is the aspose cells conditional formatting type we need)
    index = conditions.add_condition(FormatConditionType.TIME_PERIOD)
    condition = conditions[index]

    # Define the appearance for cells that meet the condition
    condition.style.background_color = Color.pink
    condition.style.pattern = BackgroundType.SOLID

    # Set the time period to “Yesterday”
    condition.time_period = TimePeriodType.YESTERDAY

    # Populate sample dates to demonstrate the rule
    cell_i19 = worksheet.cells.get("I19")
    cell_i19.put_value(datetime(2008, 7, 30))   # matches “Yesterday”
    cell_i19.style.number = 30                 # Excel number format for dates
    cell_i19.set_style(cell_i19.style)

    cell_k20 = worksheet.cells.get("K20")
    cell_k20.put_value(datetime(2008, 8, 3))    # does NOT match
    cell_k20.style.number = 30
    cell_k20.set_style(cell_k20.style)

    # Add a label for clarity
    worksheet.cells.get("I20").put_value("Yesterday")
```

> **Γιατί να χρησιμοποιήσετε `TIME_PERIOD`;** Απομακρύνει την ανάγκη γραφής προσαρμοσμένων τύπων. Το Aspose.Cells αξιολογεί την ημερομηνία σε σχέση με την τρέχουσα ημερομηνία του συστήματος, έτσι ο κανόνας παραμένει πάντα σχετικός.

### Εκτέλεση του Κανόνα

```python
apply_yesterday_rule()
```

Όταν ανοίξετε το παραγόμενο αρχείο, τα κελιά `I19` θα λάμπουν ροζ (επειδή είναι “Yesterday”), ενώ το `K20` παραμένει το βασικό πράσινο χρώμα.

## Αυτόματη Προσαρμογή Στηλών και Αποθήκευση Workbook

Ένα τακτοποιημένο spreadsheet φαίνεται επαγγελματικό. Η αυτόματη προσαρμογή εξασφαλίζει ότι τα δεδομένα μας δεν είναι σφιχτά.

```python
# Step 4: Auto‑fit the column width for a tidy appearance
worksheet.auto_fit_column(12)   # column index is zero‑based; 12 corresponds to column M

# Step 5: Save the workbook to disk
output_path = "YOUR_DIRECTORY/TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

> **Ακρόατο σενάριο:** Αν στοχεύσετε σε κατάλογο που δεν υπάρχει, το `workbook.save` θα προκαλέσει σφάλμα. Τυλίξτε την κλήση αποθήκευσης σε ένα μπλοκ `try/except` αν χρειάζεστε ευγενική διαχείριση.

### Πλήρες Script (Έτοιμο για Αντιγραφή‑Επικόλληση)

Παρακάτω βρίσκεται ολόκληρο το script, έτοιμο για εκτέλεση. Απλώς αντικαταστήστε το `YOUR_DIRECTORY` με έναν έγκυρο φάκελο στο μηχάνημά σας.

```python
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime

# Create the workbook and worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

def get_format_condition(cell_range: str, base_color: Color):
    condition_collection = worksheet.conditional_formattings.get(
        worksheet.conditional_formattings.add(cell_range)
    )
    for cell_name in cell_range.split(":"):
        cell = worksheet.cells.get(cell_name)
        cell.style.background_color = base_color
        cell.style.pattern = BackgroundType.SOLID
    return condition_collection

def apply_yesterday_rule():
    conditions = get_format_condition("I19:K20", Color.medium_sea_green)
    index = conditions.add_condition(FormatConditionType.TIME_PERIOD)
    condition = conditions[index]
    condition.style.background_color = Color.pink
    condition.style.pattern = BackgroundType.SOLID
    condition.time_period = TimePeriodType.YESTERDAY

    cell_i19 = worksheet.cells.get("I19")
    cell_i19.put_value(datetime(2008, 7, 30))
    cell_i19.style.number = 30
    cell_i19.set_style(cell_i19.style)

    cell_k20 = worksheet.cells.get("K20")
    cell_k20.put_value(datetime(2008, 8, 3))
    cell_k20.style.number = 30
    cell_k20.set_style(cell_k20.style)

    worksheet.cells.get("I20").put_value("Yesterday")

apply_yesterday_rule()
worksheet.auto_fit_column(12)

output_path = "YOUR_DIRECTORY/TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

Η εκτέλεση αυτού του script θα δημιουργήσει το `TimePeriodExample.xlsx` με τη μορφοποίηση υπό συνθήκες που περιγράψαμε.

## Συχνές Ερωτήσεις & Συμβουλές

- **Μπορώ να στοχεύσω διαφορετικό εύρος ημερομηνίας;**  
  Απόλυτα. Αλλάξτε το `"I19:K20"` σε οποιοδήποτε εύρος τύπου A1 και προσαρμόστε τις δείγματες ημερομηνίες αναλόγως.

- **Τι γίνεται αν χρειάζομαι προσαρμοσμένο τύπο αντί του `YESTERDAY`;**  
  Χρησιμοποιήστε `FormatConditionType.FORMULA` και ορίστε `condition.formula1 = "YOUR_FORMULA"`—π.χ., `=TODAY()-A1=1` για να προσομοιώσετε το χθες.

- **Πώς εφαρμόζω πολλαπλούς κανόνες στο ίδιο εύρος;**  
  Καλέστε ξανά το `conditions.add_condition` με διαφορετικό `FormatConditionType`. Η σειρά μετράει· οι μεταγενέστεροι κανόνες μπορούν να αντικαταστήσουν τους προηγούμενους.

- **Υπάρχει τρόπος να ορίσετε το χρώμα γραμματοσειράς μαζί με το φόντο;**  
  Ναι—τροποποιήστε το `condition.style.font.color = Color.white` (ή οποιοδήποτε άλλο `Color`).

## Συμπέρασμα

Τώρα ξέρετε πώς να **create Excel workbook Python** χρησιμοποιώντας το Aspose.Cells, **set cell background color**, και **add conditional formatting python** που μορφοποιεί κελιά βάσει ημερομηνίας. Το script είναι πλήρως λειτουργικό, διαχειρίζεται ακρόατα σενάρια όπως ελλιπείς κατάλογοι, και μπορεί να επεκταθεί σε πιο σύνθετες περιπτώσεις όπως λογική πολλαπλών κανόνων ή δυναμική ανίχνευση εύρους.

Έτοιμοι για το επόμενο βήμα; Δοκιμάστε να αντικαταστήσετε τον κανόνα “Yesterday” με “Last Week”, πειραματιστείτε με διαβαθμισμένα γέμισματα ή δημιουργήστε μια πλήρη αναφορά με δεκάδες μορφοποιημένους πίνακες. Τα δομικά στοιχεία είναι όλα εδώ, και μόλις κατακτήσατε τον πυρήνα του **aspose cells conditional formatting** σε Python.

Καλό κώδικα, και μη διστάσετε να μοιραστείτε τις δικές σας παραλλαγές στα σχόλια!

## Τι Θα Πρέπει Να Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κατακτήσετε πρόσθετα χαρακτηριστικά του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Κατακτήστε τη Μορφοποίηση Κελιών Excel και τη Διαχείριση Workbook με Aspose.Cells για .NET](/cells/english/net/formatting/excel-formatting-aspose-cells-net/)
- [Πώς να Δημιουργήσετε και να Αποθηκεύσετε ένα Excel Workbook ως ODS Χρησιμοποιώντας Aspose.Cells για .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [Πώς να Δημιουργήσετε Named Ranges με Πεδίο Εφαρμογής Workbook στο Excel Χρησιμοποιώντας Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}