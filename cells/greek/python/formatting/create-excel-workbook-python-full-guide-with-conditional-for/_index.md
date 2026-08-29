---
category: general
date: 2026-07-14
description: Δημιουργήστε κώδικα Python για βιβλίο εργασίας Excel που ορίζει το χρώμα
  φόντου των κελιών, επισημαίνει κελιά βάσει εύρους ημερομηνιών και αποθηκεύει το
  βιβλίο εργασίας ως XLSX σε λίγα λεπτά.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- save workbook as xlsx
- highlight cells based on date range
- conditional formatting based on date
language: el
lastmod: 2026-07-14
og_description: Δημιουργήστε άμεσα ένα βιβλίο εργασίας Excel με Python. Μάθετε πώς
  να ορίζετε το χρώμα φόντου των κελιών, να επισημαίνετε κελιά βάσει εύρους ημερομηνιών
  και να αποθηκεύετε το βιβλίο εργασίας ως XLSX με το Aspose.Cells.
og_image_alt: Screenshot showing an Excel sheet created with Python highlighting yesterday's
  dates
og_title: Δημιουργία βιβλίου εργασίας Excel με Python – Βήμα‑βήμα μορφοποίηση υπό
  συνθήκες
schemas:
- author: Aspose
  dateModified: '2026-07-14'
  description: Create Excel workbook Python code that sets cell background color,
    highlights cells based on date range, and saves workbook as XLSX in minutes.
  headline: Create Excel Workbook Python – Full Guide with Conditional Formatting
  type: TechArticle
tags:
- Python
- Aspose.Cells
- Excel Automation
- Conditional Formatting
title: Δημιουργία Φύλλου Εργασίας Excel με Python – Πλήρης Οδηγός με Μορφοποίηση Υπό
  Όρους
url: /el/python/formatting/create-excel-workbook-python-full-guide-with-conditional-for/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία Excel Workbook Python – Πλήρης Οδηγός με Μορφοποίηση υπό Συνθήκη

Έχετε αναρωτηθεί ποτέ πώς να **create excel workbook python** σενάρια που φαίνονται επαγγελματικά χωρίς να ανοίγετε το Excel χειροκίνητα; Δεν είστε μόνοι. Σε πολλά έργα που βασίζονται σε δεδομένα, πρέπει να δημιουργούμε λογιστικά φύλλα, να χρωματίζουμε κελιά και ακόμη να επισημαίνουμε ημερομηνίες που εμπίπτουν σε συγκεκριμένο εύρος — όλα από καθαρό κώδικα Python.

Σε αυτό το tutorial θα περάσουμε βήμα-βήμα ένα πλήρες, έτοιμο προς εκτέλεση παράδειγμα που **creates an Excel workbook python** χρησιμοποιώντας τη βιβλιοθήκη Aspose.Cells, **sets cell background color**, εφαρμόζει **conditional formatting based on date**, και τελικά **saves workbook as xlsx**. Στο τέλος θα έχετε ένα επαναχρησιμοποιήσιμο απόσπασμα που μπορείτε να ενσωματώσετε σε οποιοδήποτε pipeline αυτοματοποίησης.

## Τι Θα Μάθετε

- Πώς να αρχικοποιήσετε ένα workbook και να αποκτήσετε το πρώτο worksheet.  
- Μια βοηθητική συνάρτηση που προσθέτει μια συλλογή conditional‑formatting για οποιοδήποτε εύρος κελιών.  
- Χρήση **conditional formatting based on date** για να επισημάνετε τις εγγραφές του χθες.  
- Ρύθμιση του πλάτους των στηλών για μια τακτοποιημένη διάταξη.  
- Αποθήκευση του αποτελέσματος με **save workbook as xlsx**.  

Δεν απαιτείται εξωτερική εγκατάσταση του Excel — το Aspose.Cells διαχειρίζεται τα πάντα στη μνήμη.

## Προαπαιτήσεις

- Python 3.8+ εγκατεστημένο.  
- `aspose-cells` πακέτο (`pip install aspose-cells`).  
- Βασική εξοικείωση με συναρτήσεις Python και αντικείμενα datetime.  

Αν δεν έχετε χρησιμοποιήσει ποτέ το Aspose.Cells, σκεφτείτε το ως ένα ισχυρό, pure‑Python API που μιμείται το δικό του μοντέλο αντικειμένων του Excel. Είναι ιδανικό για δημιουργία στο server όπου το Office suite δεν είναι διαθέσιμο.

## Βήμα 1: Αρχικοποίηση του Workbook (Create Excel Workbook Python)

Πρώτα απ' όλα: χρειάζεται να **create excel workbook python** με στυλ. Αυτό το βήμα δημιουργεί ένα κενό αντικείμενο workbook και μας κατευθύνει στο προεπιλεγμένο worksheet.

```python
# Step 1 – create a fresh workbook and get the first sheet
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, Color, SaveFormat
from datetime import datetime

workbook = Workbook()                     # <-- creates a new Excel file in memory
worksheet = workbook.worksheets[0]        # the default (first) sheet
```

> **Γιατί είναι σημαντικό:** Η κλάση `Workbook` είναι το σημείο εισόδου για κάθε λειτουργία του Excel. Δημιουργώντας την προγραμματιστικά αποφεύγουμε οποιαδήποτε χειροκίνητη διαχείριση αρχείων.

## Βήμα 2: Βοηθός για Προσθήκη Συλλογής Conditional‑Formatting (Set Cell Background Color)

Η conditional formatting βρίσκεται μέσα σε μια *συλλογή* που είναι συνδεδεμένη σε ένα εύρος. Ας τυλίξουμε αυτό το boilerplate σε έναν μικρό βοηθό που επίσης μας επιτρέπει να **set cell background color** για ολόκληρο το εύρος.

```python
def add_time_period_condition(cell_range: str, highlight_color: Color):
    """
    Adds a conditional‑formatting collection to `cell_range` and
    applies `highlight_color` as the base fill.
    """
    worksheet.conditional_formattings.add(cell_range)   # attach to the range
    cf = worksheet.conditional_formattings[-1]           # grab the newly added collection
    cf.style.background_color = highlight_color
    cf.style.pattern = BackgroundType.SOLID
    return cf
```

> **Συμβουλή:** Η χρήση ενός βοηθού διατηρεί το κύριο ρεύμα καθαρό και καθιστά εύκολη την επαναχρησιμοποίηση της ίδιας λογικής για πολλαπλά εύρη.

## Βήμα 3: Εφαρμογή Conditional Formatting Based on Date (Highlight Cells Based on Date Range)

Τώρα θα **highlight cells based on date range**. Το παράδειγμα εστιάζει στο “χθες”, αλλά μπορείτε να αντικαταστήσετε το `TimePeriodType.YESTERDAY` με `TODAY`, `LAST_WEEK`, κλπ.

```python
# Step 3 – create a TIME_PERIOD rule for I19:K20 (yesterday)
cf = add_time_period_condition("I19:K20", Color.medium_sea_green)

condition_index = cf.add_condition(FormatConditionType.TIME_PERIOD)
condition = cf[condition_index]

# Define the visual style for the matching cells
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID

# The actual rule: any cell whose date is yesterday gets the pink fill
condition.time_period = TimePeriodType.YESTERDAY
```

> **Τι συμβαίνει;**  
> 1. Αρχικά δίνουμε σε όλο το εύρος ένα ουδέτερο πράσινο φόντο.  
> 2. Στη συνέχεια προσθέτουμε μια συνθήκη `TIME_PERIOD` που αντικαθιστά το γέμισμα με ροζ **μόνο** όταν η ημερομηνία του κελιού ισούται με το χθες.  
> 3. Το enum `TimePeriodType` αφαιρεί την ανάγκη για προσαρμοσμένη λογική υπολογισμού ημερομηνίας.

## Βήμα 4: Συμπλήρωση Δειγματικών Ημερομηνιών (So the Rule Can Be Evaluated)

Για να δείτε τον κανόνα σε δράση, θα προσθέσουμε μερικές ημερομηνίες στο φύλλο. Μία εμπίπτει στο παράθυρο “χθες”, η άλλη όχι.

```python
# Populate I19 with a date that is yesterday (relative to the hard‑coded date)
date_cell = worksheet.cells.get("I19")
date_cell.put_value(datetime(2008, 7, 30))   # 30‑Jul‑2008
date_style = date_cell.get_style()
date_style.number = 30                     # Excel’s built‑in date format
date_cell.set_style(date_style)

# Populate K20 with a date that is NOT yesterday
date_cell = worksheet.cells.get("K20")
date_cell.put_value(datetime(2008, 8, 3))    # 03‑Aug‑2008
date_style = date_cell.get_style()
date_style.number = 30
date_cell.set_style(date_style)

# Add a label for clarity
worksheet.cells.get("I20").put_value("Yesterday")
```

> **Σημείωση για ειδική περίπτωση:** Αν το workbook σας θα ανοίξει σε διαφορετικές τοπικές ρυθμίσεις, σκεφτείτε να χρησιμοποιήσετε `date_style.custom = "dd‑mm‑yyyy"` για να επιβάλετε μια συνεπή εμφάνιση.

## Βήμα 5: Τακτοποίηση Διάταξης (Auto‑Fit Columns)

Ένα στενός λογιστικός πίνακας φαίνεται μη επαγγελματικός. Ας **adjust column width for a tidy output**.

```python
# Auto‑fit column L (index 12) to show the full content without truncation
worksheet.auto_fit_column(12)
```

> **Γιατί auto‑fit;** Εξασφαλίζει ότι τυχόν μακριές ετικέτες ή ημερομηνίες είναι πλήρως ορατές, κάτι που είναι ιδιαίτερα σημαντικό όταν μοιράζεστε το αρχείο με μη‑τεχνικούς ενδιαφερόμενους.

## Βήμα 6: Αποθήκευση του Workbook (Save Workbook As XLSX)

Τέλος, **save workbook as xlsx** σε μια τοποθεσία της επιλογής σας. Η σταθερά `SaveFormat.XLSX` λέει στο Aspose.Cells να γράψει το σύγχρονο φορμά OpenXML.

```python
output_path = "YOUR_DIRECTORY/TimePeriodDemo.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

> **Αποτέλεσμα που θα δείτε:**  
> - Τα κελιά I19 και K20 περιέχουν ημερομηνίες.  
> - Το I19 (χθες) είναι επισημασμένο ροζ, ενώ το K20 παραμένει πράσινο.  
> - Η στήλη L επεκτείνεται αυτόματα ώστε να χωράει την ετικέτα “Yesterday”.  

Αν ανοίξετε το `TimePeriodDemo.xlsx` στο Excel, η conditional formatting θα είναι ήδη εφαρμοσμένη — δεν χρειάζονται επιπλέον βήματα.

![Φύλλο Excel που δείχνει την επισημασμένη ημερομηνία του χθες](https://example.com/images/excel-demo.png "Στιγμιότυπο του παραγόμενου αρχείου Excel με επισημασμένα κελιά")

*Η παραπάνω εικόνα απεικονίζει το τελικό workbook· παρατηρήστε το ροζ χρώμα στο κελί που περιέχει την ημερομηνία του χθες.*

## Ανακεφαλαίωση: Τι Καταφέραμε

- **Created an Excel workbook python** από την αρχή χρησιμοποιώντας το Aspose.Cells.  
- **Set cell background color** για ολόκληρο το εύρος ώστε να δώσει στο φύλλο ένα οπτικό σήμα.  
- Εφαρμόστηκε **conditional formatting based on date** για αυτόματη επισήμανση των εγγραφών του χθες.  
- **Saved workbook as xlsx**, έτοιμο για διανομή ή περαιτέρω επεξεργασία.  

Όλα αυτά έγιναν σε λιγότερες από 60 γραμμές Python, και ο κώδικας λειτουργεί σε οποιαδήποτε πλατφόρμα που υποστηρίζει το runtime του Aspose.Cells.

## Επόμενα Βήματα & Σχετικά Θέματα

Αν βρήκατε αυτό χρήσιμο, ίσως θέλετε επίσης να εξερευνήσετε:

- **set cell background color** για ολόκληρες γραμμές βάσει τιμών κατάστασης (π.χ., “Completed”, “Pending”).  
- Χρήση **highlight cells based on date range** για δημιουργία κυλιόμενων παραθύρων (τελευταίες 7 ημέρες, τρέχων μήνας).  
- Εξαγωγή σε άλλες μορφές όπως **CSV** ή **PDF** με `SaveFormat.CSV` ή `SaveFormat.PDF`.  
- Προσθήκη **charts** προγραμματιστικά για την οπτικοποίηση των δεδομένων που μόλις μορφοποιήσατε.  

Μη διστάσετε να τροποποιήσετε τη λογική ημερομηνίας, να αλλάξετε την παλέτα χρωμάτων ή να επεκτείνετε το εύρος ώστε να καλύπτει ολόκληρες στήλες. Το μοτίβο παραμένει το ίδιο: δημιουργήστε ένα workbook, συνδέστε μια συλλογή conditional‑formatting, ορίστε τον κανόνα και αποθηκεύστε.

Έχετε ερωτήσεις σχετικά με μια συγκεκριμένη περίπτωση χρήσης; Αφήστε ένα σχόλιο παρακάτω, και καλή προγραμματιστική!

## Τι Θα Μάθετε Στη Σύντομη Μελλοντική

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα-βήμα εξηγήσεις για να σας βοηθήσει να κυριαρχήσετε σε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Αυτοματοποίηση Excel με Aspose.Cells .NET: Δημιουργία Workbook & Ορισμός Εξωτερικών Συνδέσμων](/cells/english/net/automation-batch-processing/excel-automation-aspose-cells-net/)
- [Δημιουργία & Αποθήκευση Excel Workbook Aspose Cells Java](/cells/hongkong/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)
- [Δημιουργία & Αποθήκευση Excel Workbook Aspose Cells Dotnet](/cells/hongkong/net/workbook-operations/create-save-excel-workbook-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}