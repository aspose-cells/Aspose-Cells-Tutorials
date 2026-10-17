---
category: general
date: 2026-09-15
description: Μάθετε πώς να εφαρμόζετε μορφοποίηση υπό όρους βάσει χρονικής περιόδου
  και να αποθηκεύετε το βιβλίο εργασίας ως XLSX με το Aspose.Cells σε Python. Περιλαμβάνει
  κώδικα βήμα‑βήμα.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- time period conditional formatting
- save workbook as xlsx
- how to create excel workbook python
- how to highlight yesterday in excel
- add conditional formatting python
language: el
lastmod: 2026-09-15
og_description: Εφαρμόστε μορφοποίηση υπό όρους με βάση την περίοδο χρόνου στο Excel
  χρησιμοποιώντας Python και αποθηκεύστε το βιβλίο εργασίας ως XLSX. Ακολουθήστε αυτόν
  τον πλήρη οδηγό για το Aspose.Cells.
og_image_alt: Screenshot of an Excel sheet where the cells for yesterday are highlighted
  in pink
og_title: Εφαρμόστε μορφοποίηση υπό όρους χρονικής περιόδου στο Excel με Python
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Learn how to apply time period conditional formatting and save workbook
    as XLSX with Aspose.Cells in Python. Includes step‑by‑step code.
  headline: How to apply time period conditional formatting in Excel using Python
  type: TechArticle
- description: Learn how to apply time period conditional formatting and save workbook
    as XLSX with Aspose.Cells in Python. Includes step‑by‑step code.
  name: How to apply time period conditional formatting in Excel using Python
  steps:
  - name: '**Creating the workbook** gives you an in‑memory Excel file you can manipulate
      without opening Excel.'
    text: '**Creating the workbook** gives you an in‑memory Excel file you can manipulate
      without opening Excel.'
  - name: '**Defining the range** (`I19:K20`) tells Aspose.Cells where the rule applies,
      keeping the logic isolated.'
    text: '**Defining the range** (`I19:K20`) tells Aspose.Cells where the rule applies,
      keeping the logic isolated.'
  - name: '**Adding a TIME_PERIOD condition** uses Aspose’s built‑in enumeration `TimePeriodType.YESTERDAY`.
      This avoids manual date calculations and automatically updates when the file
      is opened on a different day.'
    text: '**Adding a TIME_PERIOD condition** uses Aspose’s built‑in enumeration `TimePeriodType.YESTERDAY`.
      This avoids manual date calculations and automatically updates when the file
      is opened on a different day.'
  - name: '**Setting the style** (`background_color` and `pattern`) determines how
      the highlighted cells appear. Using `Color.pink` makes the rule easy to spot.'
    text: '**Setting the style** (`background_color` and `pattern`) determines how
      the highlighted cells appear. Using `Color.pink` makes the rule easy to spot.'
  - name: '**Writing sample dates** with number format 30 ensures Excel displays them
      as short dates rather than serial numbers.'
    text: '**Writing sample dates** with number format 30 ensures Excel displays them
      as short dates rather than serial numbers.'
  - name: '**Auto‑fitting the column** improves readability for anyone opening the
      file later.'
    text: '**Auto‑fitting the column** improves readability for anyone opening the
      file later.'
  - name: '**Saving as XLSX** produces a widely compatible file that can be opened
      in Excel, Google Sheets, or any modern spreadsheet program.'
    text: '**Saving as XLSX** produces a widely compatible file that can be opened
      in Excel, Google Sheets, or any modern spreadsheet program.'
  - name: Cells `I19` and `K20` contain the dates `30‑07‑2008` and `03‑08‑2008`.
    text: Cells `I19` and `K20` contain the dates `30‑07‑2008` and `03‑08‑2008`.
  - name: The cell `I20` shows the text “Yesterday”.
    text: The cell `I20` shows the text “Yesterday”.
  - name: If you change your system date to **July 30 2008** and reopen the file,
      the cells with matching dates are automatically filled with pink.
    text: If you change your system date to **July 30 2008** and reopen the file,
      the cells with matching dates are automatically filled with pink.
  type: HowTo
tags:
- Aspose.Cells
- Python
- Excel automation
title: Πώς να εφαρμόσετε μορφοποίηση υπό όρους χρονικής περιόδου στο Excel χρησιμοποιώντας
  Python
url: /el/python/formatting/how-to-apply-time-period-conditional-formatting-in-excel-usi/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να εφαρμόσετε μορφοποίηση υπό όρους με βάση την χρονική περίοδο στο Excel χρησιμοποιώντας Python

Αν χρειάζεστε **μορφοποίηση υπό όρους με βάση την χρονική περίοδο** σε ένα αρχείο Excel, αυτό το tutorial σας δείχνει ακριβώς πώς να το κάνετε με Python. Θα δείτε ένα πλήρες, εκτελέσιμο παράδειγμα που δημιουργεί ένα βιβλίο εργασίας, επισημαίνει τις ημερομηνίες του χθες και **αποθηκεύει το βιβλίο εργασίας ως XLSX** με λίγες μόνο γραμμές κώδικα.

Η μορφοποίηση υπό όρους είναι ένας ισχυρός τρόπος για να τραβήξετε την προσοχή σε δεδομένα που πληρούν έναν συγκεκριμένο κανόνα. Σε αυτόν τον οδηγό εστιάζουμε στην χρονική περίοδο “Yesterday”, αλλά το ίδιο μοτίβο λειτουργεί για άλλες ενσωματωμένες περιόδους όπως Today, LastWeek και NextMonth. Στο τέλος του tutorial θα μπορείτε να δημιουργήσετε σενάρια **how to create excel workbook python**‑style που είναι έτοιμα για παραγωγή.

## Προαπαιτούμενα

- Python 3.8+ εγκατεστημένο  
- Πακέτα `aspose-cells` και `aspose-pydrawing` (`pip install aspose-cells aspose-pydrawing`)  
- Βασική εξοικείωση με τη σύνταξη της Python  

Δεν απαιτείται πρόσθετη εγκατάσταση του Office επειδή το Aspose.Cells διαχειρίζεται τη δημιουργία του αρχείου εσωτερικά.

## Μορφοποίηση υπό όρους με βάση την χρονική περίοδο με το Aspose.Cells σε Python

Αυτή η ενότητα περνάει βήμα-βήμα κάθε γραμμή κώδικα που απαιτείται για την κύρια εργασία. Το παρακάτω μπλοκ κώδικα είναι το πλήρες script· τα σχόλια εξηγούν τον σκοπό κάθε βήματος.

```python
# -*- coding: utf-8 -*-
"""
Apply time period conditional formatting to highlight yesterday's dates
and save the workbook as XLSX using Aspose.Cells for Python.
"""

from aspose.cells import (
    Workbook, FormatConditionType, BackgroundType,
    TimePeriodType, SaveFormat
)
from aspose.pydrawing import Color
from datetime import datetime

# Step 1: Create a new workbook and select the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Step 2: Define the range that will receive the conditional formatting rule
cell_range = "I19:K20"
cond_format = worksheet.conditional_formattings.add(cell_range)

# Step 3: Add a TIME_PERIOD condition for “Yesterday” and style it
condition_index = cond_format.add_condition(FormatConditionType.TIME_PERIOD)
condition = cond_format[condition_index]
condition.style.background_color = Color.pink          # Highlight colour
condition.style.pattern = BackgroundType.SOLID        # Solid fill
condition.time_period = TimePeriodType.YESTERDAY      # Built‑in “Yesterday” period

# Step 4: Populate the range with sample dates (Excel number format 30 = short date)
date_cells = ["I19", "K20"]                           # Cells that will contain dates
sample_dates = [datetime(2008, 7, 30), datetime(2008, 8, 3)]
for cell_ref, date_val in zip(date_cells, sample_dates):
    cell = worksheet.cells.get(cell_ref)
    cell.put_value(date_val)                         # Write the Python datetime
    style = cell.get_style()
    style.number = 30                                 # Excel short date format
    cell.set_style(style)

# Step 5: Add a label so the user knows what the rule represents
worksheet.cells.get("I20").put_value("Yesterday")

# Step 6: Auto‑fit the column for better readability (column L is index 12)
worksheet.auto_fit_column(12)

# Step 7: Save the workbook – this demonstrates “save workbook as xlsx”
output_path = "TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

### Γιατί κάθε βήμα είναι σημαντικό

1. **Creating the workbook** σας παρέχει ένα αρχείο Excel στη μνήμη που μπορείτε να επεξεργαστείτε χωρίς να ανοίξετε το Excel.  
2. **Defining the range** (`I19:K20`) λέει στο Aspose.Cells πού εφαρμόζεται ο κανόνας, διατηρώντας τη λογική απομονωμένη.  
3. **Adding a TIME_PERIOD condition** χρησιμοποιεί την ενσωματωμένη απαρίθμηση του Aspose `TimePeriodType.YESTERDAY`. Αυτό αποφεύγει χειροκίνητους υπολογισμούς ημερομηνιών και ενημερώνεται αυτόματα όταν το αρχείο ανοίγει σε διαφορετική ημέρα.  
4. **Setting the style** (`background_color` και `pattern`) καθορίζει πώς εμφανίζονται τα επισημασμένα κελιά. Η χρήση του `Color.pink` κάνει τον κανόνα εύκολο να εντοπιστεί.  
5. **Writing sample dates** με μορφή αριθμού 30 εξασφαλίζει ότι το Excel εμφανίζει τις ημερομηνίες ως σύντομες ημερομηνίες αντί για σειριακούς αριθμούς.  
6. **Auto‑fitting the column** βελτιώνει την αναγνωσιμότητα για όποιον ανοίξει το αρχείο αργότερα.  
7. **Saving as XLSX** παράγει ένα ευρέως συμβατό αρχείο που μπορεί να ανοιχθεί στο Excel, Google Sheets ή σε οποιοδήποτε σύγχρονο πρόγραμμα λογιστικών φύλλων.

## Πώς να δημιουργήσετε βιβλίο εργασίας Excel σε στυλ Python με το Aspose.Cells

Το παραπάνω script ήδη δείχνει τα ελάχιστα βήματα για **how to create excel workbook python**. Στην πράξη μπορεί να θέλετε να:

- Προσθέσετε πολλαπλά φύλλα εργασίας (`workbook.worksheets.add("Report")`).  
- Συμπληρώσετε μεγάλους πίνακες δεδομένων με βρόχους ή pandas DataFrames (`worksheet.cells.import_data_table`).  
- Εφαρμόσετε επιπλέον μορφοποίηση (γραμματοσειρές, περιγράμματα) χρησιμοποιώντας `cell.get_style()`.

Όλες αυτές οι ενέργειες ακολουθούν το ίδιο μοτίβο: λαμβάνετε το αντικείμενο, τροποποιείτε τις ιδιότητές του και καλείτε `set_style` ή `save`.

## Προσθήκη μορφοποίησης υπό όρους Python – άλλα χρήσιμα μοτίβα

Πέρα από το παράδειγμα “Yesterday”, το Aspose.Cells υποστηρίζει πολλούς τύπους μορφοποίησης υπό όρους:

| FormatConditionType | Τυπική περίπτωση χρήσης |
|---------------------|--------------------------|
| `FORMAT_CONDITION_TYPE_EXPRESSION` | Προσαρμοσμένοι τύποι (`=A1>100`) |
| `FORMAT_CONDITION_TYPE_CELL_VALUE` | Απλές συγκρίσεις (`>`, `<`, `=`) |
| `FORMAT_CONDITION_TYPE_COLOR_SCALE` | Κλίμακες χρωμάτων με διαβάθμιση |
| `FORMAT_CONDITION_TYPE_DATA_BAR`   | Οπτικοποίηση γραμμής μέσα στο κελί |

Για να **add conditional formatting python** για ένα αριθμητικό όριο, θα αντικαταστήσετε το `FormatConditionType.TIME_PERIOD` με `FormatConditionType.CELL_VALUE` και θα ορίσετε `condition.operator_type` και `condition.formula1`.

```python
# Example: highlight values greater than 500
idx = cond_format.add_condition(FormatConditionType.CELL_VALUE)
cond = cond_format[idx]
cond.operator_type = ConditionOperatorType.GREATER_THAN
cond.formula1 = "500"
cond.style.background_color = Color.light_green
```

## Αποθήκευση βιβλίου εργασίας ως XLSX – βέλτιστες πρακτικές

Όταν **save workbook as xlsx**, λάβετε υπόψη:

- **Specifying the correct `SaveFormat`** (`SaveFormat.XLSX`) για να αποφύγετε παλαιές μορφές.  
- **Using a deterministic file name** εάν το script εκτελείται σε βρόχο (`f"report_{datetime.now():%Y%m%d}.xlsx"`).  
- **Closing resources** (`workbook.dispose()`) σε υπηρεσίες που τρέχουν πολύ ώρα για να ελευθερώσετε τη φυσική μνήμη.  

Το παράδειγμα χρησιμοποιεί ήδη το `SaveFormat.XLSX`, το οποίο παράγει ένα σύγχρονο, βασισμένο σε zip, βιβλίο εργασίας που διατηρεί όλους τους κανόνες μορφοποίησης υπό όρους.

## Επισημάνετε το χθες στο Excel – βήματα επαλήθευσης

Μετά την εκτέλεση του script, ανοίξτε το `TimePeriodExample.xlsx`:

1. Τα κελιά `I19` και `K20` περιέχουν τις ημερομηνίες `30‑07‑2008` και `03‑08‑2008`.  
2. Το κελί `I20` εμφανίζει το κείμενο “Yesterday”.  
3. Αν αλλάξετε την ημερομηνία του συστήματός σας σε **July 30 2008** και ανοίξετε ξανά το αρχείο, τα κελιά με τις αντίστοιχες ημερομηνίες γεμίζουν αυτόματα με ροζ.  
4. Αλλάζοντας την ημερομηνία του συστήματος σε οποιαδήποτε άλλη ημέρα αφαιρεί το ροζ γέμισμα, επιβεβαιώνοντας ότι ο κανόνας αντιδρά στη λογική **time period conditional formatting**.

## Συνηθισμένα προβλήματα και πώς να τα αποφύγετε

- **Missing `aspose-pydrawing`** – η κλάση `Color` βρίσκεται σε αυτό το πακέτο· η παράλειψη της εγκατάστασής του προκαλεί `ImportError`.  
- **Incorrect number format** – η χρήση της προεπιλεγμένης μορφής General εμφανίζει σειριακούς αριθμούς (π.χ., 39822). Πάντα ορίστε `style.number = 30` για σύντομες ημερομηνίες.  
- **Range mismatch** – η περιοχή μορφοποίησης υπό όρους πρέπει να περιλαμβάνει τα κελιά που θέλετε να επισημάνετε· διαφορετικά ο κανόνας δεν έχει αποτέλεσμα.

## Συμβουλή επαγγελματία: επαναχρησιμοποίηση της ρουτίνας μορφοποίησης

Αν χρειάζεστε τον ίδιο κανόνα “Yesterday” σε πολλαπλά βιβλία εργασίας, τυλίξτε τη λογική σε μια βοηθητική συνάρτηση:

```python
def apply_yesterday_highlight(worksheet, address):
    cf = worksheet.conditional_formattings.add(address)
    idx = cf.add_condition(FormatConditionType.TIME_PERIOD)
    cond = cf[idx]
    cond.style.background_color = Color.pink
    cond.style.pattern = BackgroundType.SOLID
    cond.time_period = TimePeriodType.YESTERDAY
```

Καλέστε `apply_yesterday_highlight(worksheet, "A1:A10")` όπου χρειάζεται.

## Συμπέρασμα

Αυτός ο οδηγός σας έδειξε πώς να εφαρμόσετε **time period conditional formatting** στο Excel χρησιμοποιώντας Python, πώς να **save workbook as XLSX**, και πώς να **highlight yesterday in Excel** με ένα ενιαίο, επαναχρησιμοποιήσιμο script. Τώρα έχετε μια σταθερή βάση για να προσθέσετε κώδικα **add conditional formatting python** σε οποιοδήποτε έργο αυτοματοποίησης, είτε δημιουργείτε καθημερινές αναφορές, χτίζετε πίνακες ελέγχου, είτε προετοιμάζετε εξαγωγές δεδομένων.

**Επόμενα βήματα**

- Εξερευνήστε άλλες τιμές `TimePeriodType` όπως `TODAY` ή `LAST_WEEK`.  
- Συνδυάστε πολλαπλούς κανόνες μορφοποίησης υπό όρους στην ίδια περιοχή για πιο πλούσιες οπτικές ενδείξεις.  
- Ενσωματώστε τη δημιουργία του βιβλίου εργασίας σε μια υπηρεσία web ή σε προγραμματισμένη εργασία.

Καλό κώδικα, και απολαύστε την οπτική σαφήνεια που προσφέρει η μορφοποίηση υπό όρους στην αυτοματοποίηση του Excel!

## Τι θα πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε σε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Κατακτήστε τη μορφοποίηση υπό όρους στο Excel χρησιμοποιώντας Aspose.Cells .NET : Ένας ολοκληρωμένος οδηγός](/cells/english/net/formatting/mastering-aspose-cells-net-conditional-formatting/)
- [Κατακτήστε το Aspose.Cells .NET : Εφαρμογή μορφοποίησης υπό όρους σε εναλλασσόμενες γραμμές στο Excel](/cells/english/net/formatting/aspose-cells-net-conditional-formatting-alternate-rows/)
- [Κατακτήστε τη μορφοποίηση υπό όρους με προσαρμοσμένες γραμματοσειρές στο Excel χρησιμοποιώντας Aspose.Cells για .NET και C#](/cells/english/net/formatting/conditional-formatting-custom-fonts-aspose-csharp/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}