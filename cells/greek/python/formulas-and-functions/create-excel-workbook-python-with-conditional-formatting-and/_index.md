---
category: general
date: 2026-10-04
description: Δημιουργήστε βιβλίο εργασίας Excel με Python χρησιμοποιώντας το Aspose.Cells.
  Μάθετε τη μορφοποίηση υπό όρους του Excel με Python, το χρώμα φόντου κελιού με Python
  και τη μορφοποίηση ημερομηνίας κελιών με Python σε ένα πλήρες παράδειγμα.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create Excel workbook python
- excel conditional formatting python
- cell background color python
- format cells date python
language: el
lastmod: 2026-10-04
og_description: Δημιουργήστε βιβλίο εργασίας Excel με Python και Aspose.Cells. Αυτό
  το σεμινάριο δείχνει τη μορφοποίηση υπό όρους στο Excel με Python, το χρώμα φόντου
  κελιού με Python και τη μορφοποίηση ημερομηνίας κελιών με Python βήμα‑βήμα.
og_image_alt: Screenshot of an Excel workbook created with Python showing highlighted
  yesterday dates
og_title: Δημιουργία βιβλίου εργασίας Excel με Python – πλήρης οδηγός με μορφοποίηση
  υπό όρους
schemas:
- author: Aspose
  dateModified: '2026-10-04'
  description: Create Excel workbook python using Aspose.Cells. Learn excel conditional
    formatting python, cell background color python, and format cells date python
    in a full example.
  headline: Create Excel workbook python with conditional formatting and cell background
    color
  type: TechArticle
- description: Create Excel workbook python using Aspose.Cells. Learn excel conditional
    formatting python, cell background color python, and format cells date python
    in a full example.
  name: Create Excel workbook python with conditional formatting and cell background
    color
  steps:
  - name: '**create Excel workbook python** using the Aspose.Cells library.'
    text: '**create Excel workbook python** using the Aspose.Cells library.'
  - name: Apply **excel conditional formatting python** that automatically highlights
      dates that fall on “Yesterday”.
    text: Apply **excel conditional formatting python** that automatically highlights
      dates that fall on “Yesterday”.
  - name: Set the **cell background color python** to pink (or any color you prefer).
    text: Set the **cell background color python** to pink (or any color you prefer).
  - name: '**format cells date python** so the dates appear in the standard Excel
      date style.'
    text: '**format cells date python** so the dates appear in the standard Excel
      date style.'
  type: HowTo
tags:
- Aspose.Cells
- Python
- Excel automation
title: Δημιουργία βιβλίου εργασίας Excel με Python, με μορφοποίηση υπό όρους και χρώμα
  φόντου κελιού
url: /el/python/formulas-and-functions/create-excel-workbook-python-with-conditional-formatting-and/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create Excel workbook python with conditional formatting and cell background color

Αν χρειάζεστε να **create Excel workbook python** γρήγορα, αυτός ο οδηγός σας δείχνει ακριβώς πώς. Θα δείτε ένα πλήρες, εκτελέσιμο παράδειγμα που προσθέτει **excel conditional formatting python**, αλλάζει το **cell background color python**, και **format cells date python** για επισήμανση «Yesterday».

Σε πολλές περιπτώσεις αναφοράς, η οπτική ένδειξη ενός χρωματισμένου κελιού κάνει τα δεδομένα άμεσα κατανοητά. Αυτό το tutorial σας καθοδηγεί βήμα‑βήμα μέσα από κάθε γραμμή κώδικα, εξηγεί γιατί κάθε βήμα είναι σημαντικό, και σας παρέχει ένα έτοιμο‑για‑εκτέλεση script που μπορείτε να προσαρμόσετε στα δικά σας έργα.

## What you’ll accomplish

Στο τέλος αυτού του άρθρου θα μπορείτε:

1. **create Excel workbook python** χρησιμοποιώντας τη βιβλιοθήκη Aspose.Cells.  
2. Εφαρμόζετε **excel conditional formatting python** που επισημαίνει αυτόματα ημερομηνίες που αντιστοιχούν στο «Yesterday».  
3. Ορίζετε το **cell background color python** σε ροζ (ή σε οποιοδήποτε χρώμα προτιμάτε).  
4. **format cells date python** ώστε οι ημερομηνίες να εμφανίζονται στο τυπικό στυλ ημερομηνίας του Excel.  

Δεν απαιτείται προηγούμενη εμπειρία με Aspose.Cells — αρκεί ένα λειτουργικό περιβάλλον Python 3 και πρόσβαση στο pip.

## Prerequisites

- Python 3.8 ή νεότερη εγκατεστημένη.  
- Πακέτα `aspose-cells` και `aspose-pydrawing` εγκατεστημένα μέσω `pip install aspose-cells aspose-pydrawing`.  
- Βασική εξοικείωση με τη σύνταξη της Python και τις έννοιες του Excel (workbooks, worksheets, cells).  

> **Pro tip:** Αν εκτελείτε το script σε εικονικό περιβάλλον, αποφεύγετε συγκρούσεις εκδόσεων με άλλα έργα.

## Step 1: Set up the project and import required classes

Το πρώτο βήμα όταν **create Excel workbook python** είναι η εισαγωγή των κλάσεων Aspose.Cells που θα χρειαστείτε. Αυτές οι κλάσεις σας δίνουν άμεση πρόσβαση στη δημιουργία βιβλίου εργασίας, στη μορφοποίηση υπό όρους και στο styling.

```python
# Import Aspose.Cells core classes
from aspose.cells import (
    Workbook, FormatConditionType, BackgroundType,
    TimePeriodType, SaveFormat
)

# Import Aspose.PyDrawing for color handling
from aspose.pydrawing import Color

# Standard library for date values
from datetime import datetime
```

*Why this matters:* Η εισαγωγή μόνο των απαραίτητων συμβόλων διατηρεί το namespace καθαρό και κάνει το script πιο ευανάγνωστο. Η `Workbook` είναι το σημείο εισόδου για **create Excel workbook python**, ενώ οι `FormatConditionType` και `TimePeriodType` είναι ουσιώδεις για **excel conditional formatting python**.

## Step 2: Create a new workbook and obtain the first worksheet

Τώρα δημιουργούμε πραγματικά το **create Excel workbook python**. Ο κατασκευαστής `Workbook()` σας δίνει ένα κενό αρχείο Excel με ένα προεπιλεγμένο φύλλο εργασίας.

```python
# Step 2: Initialize a new workbook
workbook = Workbook()

# Grab the first worksheet (index 0)
worksheet = workbook.worksheets[0]
```

*Explanation:* Κάθε αρχείο Excel ξεκινάει με τουλάχιστον ένα φύλλο εργασίας. Από προεπιλογή, το Aspose.Cells το ονομάζει «Sheet1». Μπορείτε να προσθέσετε περισσότερα φύλλα αργότερα, αλλά για αυτήν την επίδειξη ένα μόνο φύλλο κρατά το παράδειγμα εστιασμένο.

## Step 3: Define the target range for conditional formatting

Η μορφοποίηση υπό όρους λειτουργεί σε ένα ορθογώνιο εύρος. Εδώ επιλέγουμε το εύρος `I19:K20`, που μας δίνει τρεις στήλες και δύο γραμμές για να εργαστούμε.

```python
# Define the range that will receive conditional formatting
target_range = "I19:K20"

# Retrieve (or create) the ConditionalFormatting collection for that range
conditional_formatting = worksheet.conditional_formattings.get(target_range)
```

*Why we do this:* Η μέθοδος `get` επιστρέφει ένα αντικείμενο `ConditionalFormatting` συνδεδεμένο με το συγκεκριμένο εύρος. Αν το εύρος δεν έχει ακόμη μορφοποίηση, το Aspose.Cells δημιουργεί αυτόματα μια νέα συλλογή.

## Step 4: Add a TIME_PERIOD condition and set the background color

Αυτό είναι το βασικό στοιχείο του **excel conditional formatting python**. Προσθέτουμε έναν κανόνα `TIME_PERIOD` που επισημαίνει κελιά με ημερομηνίες που αντιστοιχούν στο «Yesterday».

```python
# Add a TIME_PERIOD condition to the range
condition_index = conditional_formatting.add_condition(FormatConditionType.TIME_PERIOD)

# Access the newly created condition
condition = conditional_formatting[condition_index]

# Configure the condition to target “Yesterday”
condition.time_period = TimePeriodType.YESTERDAY

# Set the cell background color – this is the cell background color python part
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID
```

*Deep dive:*  
- `FormatConditionType.TIME_PERIOD` λέει στο Excel να αξιολογεί ημερομηνίες σε σχέση με την τρέχουσα ημερομηνία.  
- `TimePeriodType.YESTERDAY` είναι μια ενσωματωμένη enum που ενημερώνεται αυτόματα κάθε μέρα, ώστε το βιβλίο εργασίας να επισημαίνει πάντα το πιο πρόσφατο «Yesterday».  
- Ορίζοντας `background_color` σε `Color.pink` και το pattern σε `SOLID`, επιτυγχάνουμε το **cell background color python** χωρίς επιπλέον κώδικα VBA.

## Step 5: Populate the range with sample dates and apply date formatting

Για να δείτε τη μορφοποίηση υπό όρους σε δράση, χρειάζονται πραγματικές τιμές ημερομηνίας. Επίσης πρέπει να **format cells date python** ώστε το Excel να τις αντιμετωπίζει ως ημερομηνίες και όχι ως απλούς αριθμούς.

```python
# Helper function to set a cell's date style and value
def set_date(cell_name: str, date_value: datetime):
    cell = worksheet.cells.get(cell_name)
    style = cell.get_style()
    # Excel’s built‑in date format code 30 = "m/d/yy"
    style.number = 30
    cell.set_style(style)
    cell.put_value(date_value)

# Populate I19 with a date that is “yesterday” relative to the sample data
set_date("I19", datetime(2008, 7, 30))   # Example “yesterday”

# Populate K20 with another arbitrary date
set_date("K20", datetime(2008, 8, 3))    # Not “yesterday”
```

*Explanation:*  
- Η γραμμή `style.number = 30` είναι το βήμα **format cells date python**. Ο κωδικός μορφής 30 αντιστοιχεί στη σύντομη μορφή ημερομηνίας (`m/d/yy`).  
- Η χρήση μιας βοηθητικής συνάρτησης κρατά τον κώδικα DRY (Don’t Repeat Yourself) και διευκολύνει την προσθήκη περισσότερων ημερομηνιών αργότερα.

## Step 6: Add a descriptive label

Μια μικρή ετικέτα βοηθά όποιον ανοίγει το βιβλίο εργασίας να καταλάβει γιατί τα κελιά είναι χρωματισμένα.

```python
# Place a label next to the formatted range
worksheet.cells.get("I20").put_value("Yesterday")
```

## Step 7: Save the workbook to disk

Τέλος, **create Excel workbook python** στο δίσκο καλώντας τη μέθοδο `save`. Η σταθερά `SaveFormat.XLSX` εξασφαλίζει ότι το αρχείο είναι σε σύγχρονη μορφή Office Open XML.

```python
# Define the output path – replace YOUR_DIRECTORY with a real folder
output_path = "YOUR_DIRECTORY/TimePeriodDemo.xlsx"

# Save the workbook
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

Όταν ανοίξετε το `TimePeriodDemo.xlsx` στο Excel, θα δείτε:

- Τα κελιά `I19` και `K20` περιέχουν ημερομηνίες.  
- Το κελί που ταιριάζει με το «Yesterday» (σε αυτό το στατικό παράδειγμα, το `I19`) είναι επισημασμένο ροζ.  
- Η ετικέτα «Yesterday» εμφανίζεται στο `I20`.  

> **Tip:** Αν τρέξετε το script σε διαφορετική ημέρα, η μορφοποίηση υπό όρους θα συνεχίσει να επισημαίνει το κελί της ημερομηνίας που είναι ακριβώς μία ημέρα πριν την τρέχουσα ημερομηνία του συστήματος — χωρίς αλλαγές κώδικα.

## Full script – ready to copy and run

Παρακάτω βρίσκεται το πλήρες, αυτόνομο πρόγραμμα που ενσωματώνει όλα τα παραπάνω βήματα. Αντιγράψτε το σε ένα αρχείο με όνομα `conditional_format_demo.py`, προσαρμόστε το `YOUR_DIRECTORY`, και εκτελέστε το με `python conditional_format_demo.py`.

```python
from aspose.cells import (
    Workbook, FormatConditionType, BackgroundType,
    TimePeriodType, SaveFormat
)
from aspose.pydrawing import Color
from datetime import datetime

# Step 1: Create a new workbook and get the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Step 2: Define the cell range that will receive the conditional format
target_range = "I19:K20"
conditional_formatting = worksheet.conditional_formattings.get(target_range)

# Step 3: Add a TIME_PERIOD condition to the range
condition_index = conditional_formatting.add_condition(FormatConditionType.TIME_PERIOD)

# Step 4: Configure the condition to highlight “Yesterday” dates
condition = conditional_formatting[condition_index]
condition.time_period = TimePeriodType.YESTERDAY
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID

# Helper to set date value and style
def set_date(cell_name: str, date_value: datetime):
    cell = worksheet.cells.get(cell_name)
    style = cell.get_style()
    style.number = 30          # Excel date format code 30 = short date
    cell.set_style(style)
    cell.put_value(date_value)

# Step 5: Populate the range with sample dates (excel conditional formatting python)
set_date("I19", datetime(2008, 7, 30))   # Example “yesterday”
set_date("K20", datetime(2008, 8, 3))    # Another sample date

# Step 6: Add a label describing the condition
worksheet.cells.get("I20").put_value("Yesterday")

# Step 7: Save the workbook
output_path = "YOUR_DIRECTORY/TimePeriodDemo.xlsx"
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

### Expected output

Η εκτέλεση του script εκτυπώνει μια γραμμή επιβεβαίωσης:

```
Workbook saved to YOUR_DIRECTORY/TimePeriodDemo.xlsx
```

Το άνοιγμα του παραγόμενου αρχείου δείχνει το ροζ φόντο στο κελί που ταιριάζει με τον κανόνα «Yesterday», επιβεβαιώνοντας ότι το **excel conditional formatting python** και το **cell background color python** λειτουργούν μαζί.

## Common variations and edge cases

| Situation | How to adapt the code |
|-----------|-----------------------|
| **Different highlight color** | Αλλάξτε το `Color.pink` σε οποιαδήποτε άλλη σταθερά `Color`, π.χ. `Color.light_green`. |
| **Highlight “Today” instead of “Yesterday”** | Ορίστε `condition.time_period = TimePeriodType.TODAY`. |
| **Apply formatting to an entire column** | Χρησιμοποιήστε εύρος όπως `"A:A"` και προσαρμόστε τη μεταβλητή `target_range` αναλόγως. |
| **Use a custom date format** | Αντικαταστήστε το `style.number = 30` με `style.custom = "dd-mmm-yyyy"` για πιο ευανάγνωστη μορφή. |
| **Multiple conditions on the same range** |  |

## What Should You Learn Next?

Οι παρακάτω οδηγίες καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κυριαρχήσετε επιπλέον δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στα δικά σας έργα.

- [Create Excel Workbook Python – Complete Guide with Lambda](/cells/english/python/formulas-and-functions/create-excel-workbook-python-complete-guide-with-lambda/)
- [Create and Save Excel Workbook as PDF in ASP.NET Using Aspose.Cells](/cells/english/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)
- [How to Create and Save an Excel Workbook as ODS Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}