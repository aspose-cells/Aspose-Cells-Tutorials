---
category: general
date: 2026-07-06
description: Δημιουργήστε βιβλίο εργασίας Excel με Python, με κώδικα για ορισμό χρώματος
  φόντου κελιού, προγραμματιστικό ορισμό στυλ κελιού και προσθήκη υπό‑συνθήκη μορφοποίησης
  σε Python για επισήμανση της σημερινής ημερομηνίας.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- set cell style programmatically
- highlight today date excel
- add conditional formatting python
language: el
lastmod: 2026-07-06
og_description: Δημιουργήστε άμεσα ένα βιβλίο εργασίας Excel με Python. Μάθετε πώς
  να ορίζετε το χρώμα φόντου των κελιών, να ρυθμίζετε το στυλ των κελιών προγραμματιστικά
  και να προσθέτετε μορφοποίηση υπό όρους με Python για να επισημαίνετε την τρέχουσα
  ημερομηνία.
og_image_alt: Screenshot of an Excel workbook created with Python showing colored
  cells and today’s date highlighted
og_title: Δημιουργία φύλλου εργασίας Excel με Python – Στυλ κελιών & Επισήμανση της
  σημερινής ημέρας
schemas:
- author: Aspose
  dateModified: '2026-07-06'
  description: Create Excel workbook Python with code to set cell background color,
    set cell style programmatically, and add conditional formatting python for highlighting
    today’s date.
  headline: Create Excel Workbook Python – Full Guide to Styling & Conditional Formatting
  type: TechArticle
- description: Create Excel workbook Python with code to set cell background color,
    set cell style programmatically, and add conditional formatting python for highlighting
    today’s date.
  name: Create Excel Workbook Python – Full Guide to Styling & Conditional Formatting
  steps:
  - name: Converting a range like `"A1:C3"` into a `CellArea`.
    text: Converting a range like `"A1:C3"` into a `CellArea`.
  - name: Filling every cell in that area with a sequential number (just for demo
      purposes).
    text: Filling every cell in that area with a sequential number (just for demo
      purposes).
  - name: Applying a solid **set cell background color**.
    text: Applying a solid **set cell background color**.
  - name: Adding a conditional rule that **highlight today date excel**.
    text: Adding a conditional rule that **highlight today date excel**.
  type: HowTo
tags:
- Python
- Aspose.Cells
- Excel Automation
- Conditional Formatting
title: Δημιουργία βιβλίου εργασίας Excel με Python – Πλήρης οδηγός για το στυλ και
  τη μορφοποίηση υπό όρους
url: /el/python/formatting/create-excel-workbook-python-full-guide-to-styling-condition/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία Excel Workbook με Python – Πλήρης Οδηγός για Στυλ & Μορφοποίηση υπό Όρους

Έχετε αναρωτηθεί ποτέ πώς να **create Excel workbook Python** από το μηδέν χωρίς να ανοίξετε το Excel; Δεν είστε μόνοι. Πολλοί προγραμματιστές χρειάζονται να δημιουργούν αναφορές, πίνακες ελέγχου ή ακόμη και απλούς καταγραφείς δεδομένων σε πραγματικό χρόνο, και η προγραμματιστική προσέγγιση εξοικονομεί ώρες χειροκίνητης εργασίας.

Σε αυτόν τον οδηγό θα περάσουμε από τη δημιουργία ενός ολοκαίνουργιου workbook, στο **set cell background color**, στο **set cell style programmatically**, και τέλος στο **highlight today date excel** χρησιμοποιώντας **add conditional formatting python**. Στο τέλος θα έχετε ένα έτοιμο script που παράγει ένα γυαλιστερό αρχείο .xlsx σε δευτερόλεπτα.

---

## Τι Θα Δημιουργήσετε

- Ένα νέο αρχείο Excel με μερικά γεμισμένα κελιά.  
- Κελιά χρωματισμένα με προσαρμοσμένο φόντο.  
- Αριθμητικές και ημερομηνίες μορφοποιημένες με συγκεκριμένο στυλ αριθμού.  
- Ένας κανόνας μορφοποίησης υπό όρους που αυτόματα επισημαίνει το κελί που περιέχει την σημερινή ημερομηνία.  

Δεν απαιτείται εξωτερική εγκατάσταση του Excel — το Aspose.Cells for Python μέσω .NET εκτελεί όλη τη βαριά δουλειά.

## Προαπαιτούμενα

| Απαίτηση | Γιατί είναι σημαντικό |
|----------|------------------------|
| Python 3.8+ | Σύγχρονη σύνταξη και υποδείξεις τύπων |
| `aspose-cells` package | Κύρια βιβλιοθήκη για τη διαχείριση των workbook |
| `aspose-pydrawing` (installed with Aspose.Cells) | Παρέχει την κλάση `Color` |
| Basic familiarity with Excel concepts (cells, ranges, formatting) | Κάνει την ροή του οδηγού πιο ομαλή |

Εγκαταστήστε τη βιβλιοθήκη με:

```bash
pip install aspose-cells
```

## Βήμα 1: Αρχικοποίηση του Workbook και του Worksheet

Το πρώτο πράγμα που κάνετε όταν **create excel workbook python** είναι να δημιουργήσετε ένα αντικείμενο `Workbook` και να πάρετε το προεπιλεγμένο worksheet. Σκεφτείτε το workbook ως ολόκληρο το αρχείο Excel, ενώ το worksheet είναι μια μεμονωμένη καρτέλα μέσα σε αυτό.

```python
from aspose.cells import Workbook

# Create a new workbook – this is our empty Excel file
book = Workbook()

# Grab the first (default) worksheet
sheet = book.worksheets[0]
```

> **Συμβουλή:** Αν χρειάζεστε πολλαπλά φύλλα, χρησιμοποιήστε `book.worksheets.add("MySheet")` για να προσθέσετε περισσότερες καρτέλες.

## Βήμα 2: Βοηθητική Κλάση για Στυλ & Μορφοποίηση υπό Όρους

Παρακάτω βρίσκεται μια συμπαγής αλλά πλήρης κλάση `ConditionalFormatting`. Περιβάλλει τις επαναλαμβανόμενες εργασίες:

1. Μετατροπή μιας περιοχής όπως `"A1:C3"` σε `CellArea`.  
2. Γέμισμα κάθε κελιού σε αυτήν την περιοχή με διαδοχικό αριθμό (μόνο για σκοπούς επίδειξης).  
3. Εφαρμογή συμπαγούς **set cell background color**.  
4. Προσθήκη κανόνα μορφοποίησης υπό όρους που **highlight today date excel**.  

```python
from aspose.cells import (
    CellArea, FormatConditionType, BackgroundType,
    TimePeriodType, SaveFormat, CellsHelper
)
from aspose.pydrawing import Color
from datetime import datetime

class ConditionalFormatting:
    """
    Utility class that demonstrates how to:
    • set cell background color
    • set cell style programmatically
    • add conditional formatting python
    """
    def __init__(self, worksheet):
        self._sheet = worksheet

    def get_format_condition(self, cell_range: str, color: Color):
        """
        Creates a conditional formatting object for the given range
        and fills the range with a background color.
        """
        index = self._sheet.conditional_formattings.add()
        cf = self._sheet.conditional_formattings[index]

        # Convert "A1:C3" → CellArea object
        area = self.get_cell_area_by_name(cell_range)
        cf.add_area(area)

        # Paint the whole area with the supplied color
        self.fill_cell(cell_range, color)
        return cf

    def fill_cell(self, cell_range: str, color: Color):
        """
        Populates each cell in the range with an incrementing integer
        and applies the supplied background color.
        """
        area = self.get_cell_area_by_name(cell_range)
        counter = 0
        for col in range(area.start_column, area.end_column + 1):
            for row in range(area.start_row, area.end_row + 1):
                cell = self._sheet.cells.get(row, col)

                # Apply background only if a real color is supplied
                if color != Color.empty:
                    style = cell.get_style()
                    style.foreground_color = color
                    style.pattern = BackgroundType.SOLID
                    cell.set_style(style)

                cell.put_value(counter)
                counter += 1

    @staticmethod
    def get_cell_area_by_name(name: str) -> CellArea:
        """
        Parses an Excel‑style address (e.g. "B2:D4") into a CellArea.
        """
        area = CellArea()
        parts = name.replace("$", "").split(':')

        start_row, start_col = CellsHelper.cell_name_to_index(parts[0])
        area.start_row = start_row
        area.start_column = start_col

        if len(parts) == 2:
            end_row, end_col = CellsHelper.cell_name_to_index(parts[1])
            area.end_row = end_row
            area.end_column = end_col
        else:
            area.end_row = start_row
            area.end_column = start_col
        return area

    # -----------------------------------------------------------------
    # Step 2: Add conditional formatting for TODAY
    # -----------------------------------------------------------------
    def add_time_period_1(self):
        """
        Demonstrates add conditional formatting python that highlights
        cells containing today’s date.
        """
        # 1️⃣ Create a formatting range and give it a neutral background
        cf = self.get_format_condition("I1:K2", Color.light_slate_gray)

        # 2️⃣ Add a TIME_PERIOD condition (Today)
        idx = cf.add_condition(FormatConditionType.TIME_PERIOD)
        cond = cf[idx]
        cond.time_period = TimePeriodType.TODAY
        cond.style.background_color = Color.pink
        cond.style.pattern = BackgroundType.SOLID

        # 3️⃣ Populate the cells with date values
        # Cell I1 – today’s date, formatted as a date
        cell = self._sheet.cells.get("I1")
        style = cell.get_style()
        style.number = 30               # 30 = “mm-dd-yy” style in Aspose
        cell.set_style(style)
        cell.put_value(datetime.today())

        # Cell K2 – an arbitrary past date for contrast
        self._sheet.cells.get("K2").put_value(datetime(2008, 7, 30))

        # Cell I2 – a label so the reader knows what’s being highlighted
        self._sheet.cells.get("I2").put_value("Today")
```

### Γιατί μια Βοηθητική Κλάση;

- **Επαναχρησιμοποίηση:** Μπορείτε να καλέσετε `add_time_period_1()` για οποιοδήποτε worksheet χωρίς να ξαναγράψετε τη λογική.  
- **Διαύγεια:** Κάθε μέθοδος κάνει ένα πράγμα – χαρακτηριστικό του καθαρού κώδικα.  
- **Επεκτασιμότητα:** Θέλετε να προσθέσετε περισσότερους κανόνες; Απλώς προσθέστε μια άλλη μέθοδο ακολουθώντας το ίδιο πρότυπο.

## Βήμα 3: Εφαρμογή της Μορφοποίησης και Αποθήκευση του Αρχείου

Τώρα συνδέουμε όλα μαζί: δημιουργούμε το αντικείμενο βοηθό, εκτελούμε τη ρουτίνα μορφοποίησης και τέλος γράφουμε το workbook στο δίσκο.

```python
# Instantiate the helper with our worksheet
formatter = ConditionalFormatting(sheet)

# Fill a demo range with numbers and a light blue background
formatter.get_format_condition("A1:C3", Color.light_sky_blue)

# Add the “today” conditional rule
formatter.add_time_period_1()

# Save the workbook – choose any location you like
output_path = "styled_workbook.xlsx"
book.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to {output_path}")
```

Όταν ανοίξετε το *styled_workbook.xlsx* θα πρέπει να δείτε:

- Κελιά **A1:C3** αριθμημένα 0‑8 με γέμισμα light‑sky‑blue.  
- Κελί **I1** που εμφανίζει την σημερινή ημερομηνία με ροζ φόντο (ευχαριστώντας τον κανόνα μορφοποίησης υπό όρους).  
- Κελί **K2** που εμφανίζει τη στατική ημερομηνία *2008‑07‑30* για σύγκριση.  
- Κελί **I2** που περιέχει το κείμενο “Today”.  

Αυτή η οπτική ένδειξη είναι ακριβώς αυτό που απαιτεί η απαίτηση **highlight today date excel**.

## Βήμα 4: Βυθιστείτε Περαιτέρω – Προσαρμογή Στυλ

Αν χρειάζεστε να τροποποιήσετε γραμματοσειρές, περιθώρια ή μορφές αριθμών, μπορείτε να επεκτείνετε τη μέθοδο `fill_cell` ή να δημιουργήσετε έναν νέο βοηθό:

```python
def apply_custom_style(cell, font_name="Calibri", font_size=11, bold=False):
    style = cell.get_style()
    style.font.name = font_name
    style.font.size = font_size
    style.font.bold = bold
    cell.set_style(style)
```

Μπορείτε τότε να καλέσετε `apply_custom_style(cell, bold=True)` μέσα στον βρόχο για να **set cell style programmatically** για κάθε κελί σε μια περιοχή.

## Συνηθισμένα Πιθανά Σφάλματα & Πώς να τα Αποφύγετε

| Συμπτωμα | Πιθανή Αιτία | Διόρθωση |
|----------|--------------|----------|
| Τα κελιά παραμένουν λευκά παρόλο που χρησιμοποιείται `Color.light_sky_blue` | Το στυλ δεν εφαρμόστηκε μετά τον ορισμό του `foreground_color` | Πάντα καλέστε `cell.set_style(style)` μετά την τροποποίηση του αντικειμένου στυλ. |
| Ο κανόνας μορφοποίησης υπό όρους δεν ενεργοποιείται ποτέ | `style.number` δεν έχει οριστεί για τα κελιά ημερομηνίας, έτσι το Excel θεωρεί την τιμή ως συμβολοσειρά | Ορίστε `style.number = 30` (ή οποιαδήποτε μορφή ημερομηνίας) πριν από το `cell.put_value(datetime…)`. |
| Το workbook αποθηκεύεται ως .xls παρόλο που χρησιμοποιείται `SaveFormat.XLSX` | Παλαιότερη έκδοση του Aspose που προεπιλέγει την παλαιά μορφή | Αναβαθμίστε στην πιο πρόσφατη έκδοση του πακέτου `aspose-cells`. |
| Η περιοχή όπως `"A1"` προκαλεί σφάλμα δείκτη | Χρήση του `cells.get("A1")` σε φύλλο που δεν έχει αρχικοποιηθεί | Βεβαιωθείτε ότι το worksheet υπάρχει (υπάρχει αμέσως μετά το `Workbook()`), ή χρησιμοποιήστε `cells.get(row, col)` με δείκτες που ξεκινούν από το μηδέν. |

## Πλήρες Script για Αντιγραφή‑Επικόλληση

Παρακάτω είναι το **ολόκληρο** script που μπορείτε να τοποθετήσετε σε ένα αρχείο με όνομα `create_excel.py` και να το εκτελέσετε αμέσως.

```python
# create_excel.py
from aspose.cells import (
    Workbook, CellArea, FormatConditionType, BackgroundType,
    TimePeriodType, SaveFormat, CellsHelper
)
from aspose.pydrawing import Color
from datetime import datetime

class ConditionalFormatting:
    """Utility for styling cells and adding conditional formatting."""
    def __init__(self, worksheet):
        self._sheet = worksheet

    def get_format_condition(self, cell_range: str, color: Color):
        index = self._sheet.conditional_formattings.add()
        cf = self._sheet.conditional_formattings[index]
        area = self.get_cell_area_by_name(cell_range)
        cf.add_area(area)
        self.fill_cell(cell_range, color)
        return cf

    def fill_cell(self, cell_range: str, color: Color):
        area = self.get_cell_area_by_name(cell_range)
        counter = 0
        for col in range(area.start_column, area.end_column + 1):
            for row in range(area.start_row, area.end_row + 1):
                cell = self._sheet.cells.get(row, col)
                if color != Color.empty:
                    style = cell.get_style()
                    style.foreground_color = color
                    style.pattern = BackgroundType.SOLID
                    cell.set_style(style)
                cell.put_value(counter)
                counter += 1

    @staticmethod
    def get_cell_area_by_name(name:


## Τι Θα Μάθετε Στη Συνέχεια;

Οι παρακάτω οδηγίες καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Αυτοματοποίηση Excel με Aspose.Cells .NET: Δημιουργία Workbook & Ορισμός Εξωτερικών Συνδέσμων](/cells/english/net/automation-batch-processing/excel-automation-aspose-cells-net/)
- [Κατακτήστε τη Μορφοποίηση Κελιών Excel και τη Διαχείριση Workbook με Aspose.Cells για .NET](/cells/english/net/formatting/excel-formatting-aspose-cells-net/)
- [Αυτοματοποίηση Excel: Δημιουργία Workbook και Προσθήκη ListBox Χρησιμοποιώντας Aspose.Cells για .NET](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}