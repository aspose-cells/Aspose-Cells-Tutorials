---
category: general
date: 2026-08-01
description: Δημιουργήστε βιβλίο εργασίας Excel με Python χρησιμοποιώντας το Aspose.Cells
  – μάθετε πώς να προσαρμόζετε αυτόματα το πλάτος των στηλών, να μορφοποιείτε κελιά
  με ημερομηνία, να ορίζετε μορφή ημερομηνίας κελιού και να εφαρμόζετε υπό συνθήκη
  μορφοποίηση.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- auto fit excel column
- format cells by date
- set cell date format
- aspose cells conditional formatting
language: el
lastmod: 2026-08-01
og_description: Δημιουργήστε άμεσα βιβλίο εργασίας Excel με Python. Ακολουθήστε αυτόν
  τον οδηγό για αυτόματη προσαρμογή στηλών Excel, μορφοποίηση κελιών κατά ημερομηνία,
  ορισμό μορφής ημερομηνίας κελιού και μάθετε την υπό συνθήκη μορφοποίηση του Aspose
  Cells.
og_image_alt: Screenshot showing a Python script that creates an Excel workbook using
  Aspose.Cells
og_title: Δημιουργία βιβλίου εργασίας Excel με Python – Βήμα προς βήμα με το Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-08-01'
  description: Create Excel workbook python using Aspose.Cells – learn auto fit excel
    column, format cells by date, set cell date format and apply conditional formatting.
  headline: Create Excel Workbook Python – Full Guide with Aspose.Cells
  type: TechArticle
tags:
- Aspose Cells
- Python
- Excel automation
- Conditional Formatting
- Date handling
title: Δημιουργία βιβλίου εργασίας Excel με Python – Πλήρης οδηγός με Aspose.Cells
url: /el/python/formatting/create-excel-workbook-python-full-guide-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία βιβλίου εργασίας Excel με Python – Πλήρης Οδηγός με Aspose.Cells

Έχετε αναρωτηθεί ποτέ πώς να **create Excel workbook python** σενάρια που φαίνονται επαγγελματικά χωρίς να ανοίγετε το Excel χειροκίνητα; Δεν είστε ο μόνος. Είτε δημιουργείτε έναν πίνακα αναφορών είτε αυτοματοποιείτε καθημερινές εξαγωγές δεδομένων, η δυνατότητα δημιουργίας αρχείου Excel από Python είναι πραγματικά αλλαγή παιχνιδιού.

Σε αυτό το tutorial θα περάσουμε βήμα-βήμα ένα πλήρες, εκτελέσιμο παράδειγμα που όχι μόνο δημιουργεί ένα βιβλίο εργασίας αλλά επίσης δείχνει **auto fit excel column**, **format cells by date**, **set cell date format**, και εφαρμόζει **aspose cells conditional formatting**. Στο τέλος, θα έχετε ένα αυτόνομο script που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο.

> **Συμβουλή επαγγελματία:** Aspose.Cells for Python via .NET σας επιτρέπει να εργάζεστε με αρχεία Excel χωρίς εξάρτηση COM, καθιστώντας το ιδανικό για Linux containers ή CI pipelines.

## Τι Θα Χρειαστεί

- **Python 3.8+** (ο κώδικας εκτελείται σε οποιαδήποτε πρόσφατη έκδοση)  
- **Aspose.Cells for Python via .NET** – εγκαταστήστε με `pip install aspose-cells`  
- Ένας φάκελος στον οποίο μπορείτε να γράψετε (θα τον ονομάσουμε `YOUR_DIRECTORY`)  
- Βασική κατανόηση των συναρτήσεων και αντικειμένων Python (χωρίς ανάγκη βαθιάς γνώσης του Excel)  

Αν έχετε ήδη όλα αυτά, υπέροχα—ας ξεκινήσουμε.

## Βήμα 1: Create Excel Workbook Python – Αρχικοποίηση του Workbook

Το πρώτο που κάνουμε είναι να δημιουργήσουμε ένα νέο αντικείμενο workbook. Σκεφτείτε το ως έναν κενό καμβά όπου κάθε επόμενη ενέργεια προσθέτει ένα νέο στοιχείο.

```python
from aspose.cells import Workbook, SaveFormat, FormatConditionType, BackgroundType, TimePeriodType
from aspose.pydrawing import Color
from datetime import datetime
import os

# Create a new workbook and grab the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]
```

> **Γιατί είναι σημαντικό:** `Workbook()` δημιουργεί μια αναπαράσταση στη μνήμη ενός αρχείου `.xlsx`. Με την πρόσβαση στο `worksheets[0]` παίρνουμε το προεπιλεγμένο φύλλο, έτοιμο για δεδομένα και μορφοποίηση.

## Βήμα 2: Define the Target Range and Base Colour – Προετοιμασία για Conditional Formatting

Πριν προσθέσουμε οποιαδήποτε λογική υπό συνθήκη, χρειαζόμαστε μια περιοχή που θα φιλοξενήσει τον κανόνα. Η περιοχή `I19:K20` είναι αυθαίρετη αλλά αρκετά μεγάλη για να παρουσιάσει πολλαπλά κελιά.

```python
# Add a conditional formatting collection to the range and set a base colour
conds = worksheet.conditional_formattings.add("I19:K20", Color.medium_sea_green)
```

Η μέθοδος `add` δημιουργεί το αντικείμενο μορφοποίησης και του δίνει ένα προεπιλεγμένο φόντο, κάνοντας τον επόμενο κανόνα πιο εμφανή.

## Βήμα 3: Aspose Cells Conditional Formatting – Εφαρμογή κανόνα TIME_PERIOD για YESTERDAY

Τώρα φτάνουμε στην καρδιά της επίδειξης: μια συνθήκη **TIME_PERIOD** που επισημαίνει κελιά που περιέχουν την ημερομηνία του χθες.

```python
# Insert a TIME_PERIOD condition for YESTERDAY
condition_index = conds.add_condition(FormatConditionType.TIME_PERIOD)
condition = conds[condition_index]

# Configure the rule – yesterday, pink background, solid fill
condition.time_period = TimePeriodType.YESTERDAY
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID
```

> **Εξήγηση:** `FormatConditionType.TIME_PERIOD` λέει στο Aspose ότι ασχολούμαστε με κανόνα βασισμένο σε ημερομηνία. Ορίζοντας το `time_period` σε `YESTERDAY`, η μηχανή αξιολογεί αυτόματα την τιμή κάθε κελιού σε σχέση με την προηγούμενη ημερολογιακή ημέρα.

## Βήμα 4: Populate Sample Dates – Ορισμός μορφής ημερομηνίας κελιού και επαλήθευση του κανόνα

Για να δείτε τον κανόνα σε δράση χρειάζονται πραγματικές ημερομηνίες. Θα **set cell date format** επίσης ώστε οι τιμές να εμφανίζονται ως αναγνώσιμες ημερομηνίες.

```python
# Cell I19 – a date that falls on “yesterday”
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))          # July 30, 2008 is “yesterday” for demo purposes
style_i19 = cell_i19.get_style()
style_i19.number = 30          # 30 = built‑in Excel date format (e.g., mm/dd/yyyy)
cell_i19.set_style(style_i19)

# Cell K20 – a date outside the period (no formatting applied)
cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))
style_k20 = cell_k20.get_style()
style_k20.number = 30
cell_k20.set_style(style_k20)
```

Παρατηρήστε πώς χρησιμοποιούμε τον ίδιο αριθμό **format cells by date** (`30`) για και τα δύο κελιά. Αυτό εξασφαλίζει ότι οι ημερομηνίες εμφανίζονται σταθερά, ανεξάρτητα από τη γλώσσα του συστήματος.

## Βήμα 5: Add a Descriptive Label – Κάντε το φύλλο αυτοεπεξηγηματικό

Μια μικρή ετικέτα βοηθά όποιον ανοίγει το αρχείο να καταλάβει τι αντιπροσωπεύουν τα χρωματισμένα κελιά.

```python
worksheet.cells.get("I20").put_value("Yesterday")
```

## Βήμα 6: Auto Fit Excel Column – Αυτόματη προσαρμογή του πλάτους των στηλών

Όταν δημιουργείτε δεδομένα προγραμματιστικά, το πλάτος των στηλών συχνά παραμένει στο προεπιλεγμένο στενό μέγεθος. Η μέθοδος **auto fit excel column** τις επεκτείνει ακριβώς όσο χρειάζεται για να εμφανίσει το περιεχόμενο.

```python
# Auto‑fit the 12th column (which corresponds to column L) so the label is fully visible
worksheet.auto_fit_column(12)
```

> **Γιατί η στήλη 12;** Σε μηδενική αρίθμηση, η στήλη `12` αντιστοιχεί στη στήλη Excel `L`. Προσαρμόστε το δείκτη αν αλλάξετε τη διάταξη.

## Βήμα 7: Save the Workbook – Εξαγωγή σε πραγματικό αρχείο

Τέλος, αποθηκεύουμε τα πάντα στο δίσκο. Η σημαία `SaveFormat.XLSX` εξασφαλίζει ένα σύγχρονο, βασισμένο σε zip βιβλίο εργασίας.

```python
output_file = os.path.join("YOUR_DIRECTORY", "TimePeriodDemo.out.xlsx")
workbook.save(output_file, SaveFormat.XLSX)
print(f"Workbook saved to {output_file}")
```

### Αναμενόμενο Αποτέλεσμα

Ανοίξτε το `TimePeriodDemo.out.xlsx` στο Excel (ή σε οποιονδήποτε προβολέα) και θα πρέπει να δείτε:

- Κελί **I19** επισημασμένο σε **ροζ** επειδή η ημερομηνία του ταιριάζει με το “χθες”.  
- Κελί **K20** αμετάβλητο, δείχνοντας ότι ο κανόνας υπό συνθήκη αγνόησε σωστά ημερομηνίες εκτός της περιόδου.  
- Στήλη **L** αυτόματα προσαρμοσμένη ώστε η ετικέτα “Yesterday” να μην περικόπτεται.

![Create Excel workbook python example](/images/create_excel_workbook_python.png){: .center-image alt="Create Excel workbook python example showing conditional formatting for yesterday's date"}

## Συνηθισμένες Παραλλαγές & Ακραίες Περιπτώσεις

| Situation | How to Adjust |
|-----------|---------------|
| **Διαφορετικό εύρος ημερομηνιών** | Αλλάξτε το `condition.time_period` σε `TimePeriodType.TODAY`, `TimePeriodType.LAST_7_DAYS`, κ.λπ. |
| **Πολλαπλές συνθήκες** | Κληθείτε ξανά το `conds.add_condition()` και διαμορφώστε ένα νέο `FormatConditionType` (π.χ., `FORMAT_CONDITION_TYPE.EXPRESSION`). |
| **Προσαρμοσμένη μορφή ημερομηνίας** | Χρησιμοποιήστε το `style_i19.number = 14` για `mm-dd-yy` ή ορίστε μια προσαρμοσμένη συμβολοσειρά μορφής μέσω `style_i19.custom = "dd-mmm-yyyy"`. |
| **Μεγάλα φύλλα εργασίας** | Τυλίξτε την κλήση `auto_fit_column` σε μπλοκ try/except για να αποφύγετε προβλήματα απόδοσης σε τεράστια αρχεία. |
| **Εκτέλεση σε headless CI** | Δεν απαιτείται UI· το Aspose λειτουργεί εξ ολοκλήρου στη μνήμη, ώστε να μπορείτε να δημιουργήσετε το αρχείο σε Docker container χωρίς εγκατεστημένο Excel. |

## Ανακεφαλαίωση – Τι Καλύψαμε

- **Create Excel workbook python** από την αρχή με Aspose.Cells.  
- **Auto fit excel column** για να διατηρείτε το αποτέλεσμα σας τακτοποιημένο.  
- **Format cells by date** και **set cell date format** για συνεπή εμφάνιση.  
- Εφαρμόστε **aspose cells conditional formatting** χρησιμοποιώντας τον τύπο `TIME_PERIOD`.

## Επόμενα Βήματα

Αν έχετε κατακτήσει τα βασικά, σκεφτείτε να εξερευνήσετε:

- **Data bars, color scales, and icon sets** για πιο πλούσια conditional styling.  
- **PivotTable generation** μέσω `worksheet.pivot_tables.add()`.  
- **Exporting to PDF** με `workbook.save("report.pdf", SaveFormat.PDF)`.  

Κάθε ένα από αυτά τα θέματα βασίζεται στις ίδιες θεμελιώδεις έννοιες που χρησιμοποιήσαμε εδώ, οπότε θα νιώσετε άνετα.

---

*Καλό προγραμματισμό! Αν αντιμετωπίσετε προβλήματα, αφήστε ένα σχόλιο παρακάτω ή ελέγξτε την τεκμηρίωση Aspose.Cells for Python για πιο λεπτομερείς πληροφορίες.*

## Τι Θα Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετικά θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα-βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Αυτόματη Προσαρμογή Γραμμών & Στηλών σε Excel χρησιμοποιώντας Aspose.Cells Java για Απρόσκοπτη Διαχείριση Βιβλίου Εργασίας](/cells/english/java/range-management/aspose-cells-java-auto-fit-rows-columns/)
- [Δημιουργία Βιβλίου Εργασίας Excel χρησιμοποιώντας Aspose.Cells σε Java&#58; Οδηγός Βήμα-Βήμα](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [Αυτοματοποιήστε το Πλάτος Στηλών Excel&#58; Auto-Fit Columns χρησιμοποιώντας Aspose.Cells για .NET](/cells/english/net/range-management/excel-automation-auto-fit-columns-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}