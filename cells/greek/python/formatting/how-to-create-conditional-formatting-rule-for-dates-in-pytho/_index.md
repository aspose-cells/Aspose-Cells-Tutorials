---
category: general
date: 2026-08-24
description: Δημιουργήστε κανόνα μορφοποίησης υπό όρους σε Python χρησιμοποιώντας
  το Aspose.Cells για να επισημάνετε ημερομηνίες, με αυτόματη προσαρμογή στήλης και
  μορφοποίηση χρώματος φόντου.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create conditional formatting rule
- auto fit column
- conditional formatting by date
- background color conditional format
- date based conditional format
language: el
lastmod: 2026-08-24
og_description: Δημιουργήστε κανόνα μορφοποίησης υπό όρους σε Python με το Aspose.Cells.
  Μάθετε πώς να επισημαίνετε ημερομηνίες, να ορίζετε χρώματα φόντου και να προσαρμόζετε
  αυτόματα το πλάτος των στηλών με λίγες μόνο γραμμές κώδικα.
og_image_alt: Screenshot of an Excel sheet where yesterday's date cells are highlighted
  in pink
og_title: Δημιουργήστε έναν κανόνα μορφοποίησης υπό όρους για ημερομηνίες σε Python
  – οδηγός βήμα‑προς‑βήμα
schemas:
- author: Aspose
  dateModified: '2026-08-24'
  description: Create conditional formatting rule in Python using Aspose.Cells to
    highlight dates, with auto‑fit column and background color formatting.
  headline: How to create conditional formatting rule for dates in Python
  type: TechArticle
tags:
- Aspose.Cells
- Python
- Excel automation
- Conditional formatting
title: Πώς να δημιουργήσετε κανόνα μορφοποίησης υπό όρους για ημερομηνίες στην Python
url: /el/python/formatting/how-to-create-conditional-formatting-rule-for-dates-in-pytho/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να δημιουργήσετε κανόνα μορφοποίησης υπό όρους για ημερομηνίες σε Python

Αν χρειάζεστε **να δημιουργήσετε κανόνα μορφοποίησης υπό όρους** που αντιδρά σε ημερομηνίες, αυτός ο οδηγός σας δείχνει ακριβώς πώς να το κάνετε με το Aspose.Cells for Python. Είτε δημιουργείτε έναν πίνακα αναφορών είτε ένα αυτοματοποιημένο φύλλο εργασίας, θα δείτε πώς να επισημάνετε τις ημερομηνίες του χθες, να εφαρμόσετε προσαρμοσμένο χρώμα φόντου και **να προσαρμόσετε αυτόματα** το πλάτος των στηλών ώστε το αποτέλεσμα να φαίνεται επαγγελματικό.

Σε αυτό το tutorial θα καλύψουμε **μορφοποίηση υπό όρους με βάση την ημερομηνία**, θα επιδείξουμε **μορφοποίηση υπό όρους με χρώμα φόντου** και θα ολοκληρώσουμε με την αποθήκευση του βιβλίου εργασίας ως αρχείο XLSX. Στο τέλος θα έχετε ένα επαναχρησιμοποιήσιμο helper που μπορείτε να προσαρμόσετε σε οποιονδήποτε **κανόνα μορφοποίησης υπό όρους με βάση την ημερομηνία** χρειάζεστε.

## Τι θα μάθετε

* Να δημιουργήσετε ένα βιβλίο εργασίας και ένα φύλλο εργασίας χρησιμοποιώντας το Aspose.Cells.  
* Να γράψετε μια βοηθητική συνάρτηση που προσθέτει **μορφοποίηση υπό όρους με βάση την ημερομηνία** σε οποιοδήποτε εύρος κελιών.  
* Να γεμίσετε τα κελιά με δείγμα ημερομηνιών ώστε ο κανόνας να αξιολογηθεί.  
* Να εφαρμόσετε **αυτόματη προσαρμογή στήλης** για να είναι το περιεχόμενο ευανάγνωστο.  
* Να αποθηκεύσετε το βιβλίο εργασίας και να επαληθεύσετε τα επισημασμένα κελιά.

Η μόνη προαπαιτούμενη προϋπόθεση είναι ένα λειτουργικό περιβάλλον Python με το πακέτο `aspose-cells` εγκατεστημένο.

## Προαπαιτούμενα

| Απαίτηση | Λεπτομέρειες |
|----------|--------------|
| Python | 3.8+ |
| Aspose.Cells for Python via Java | `pip install aspose-cells` |
| Βασικές γνώσεις των εννοιών του Excel | φύλλα εργασίας, κελιά, μορφοποίηση |
| Προαιρετικό: IDE (VS Code, PyCharm, κλπ.) | οποιοσδήποτε επεξεργαστής που μπορεί να εκτελέσει σενάρια Python |

## Βήμα 1: Δημιουργήστε ένα βιβλίο εργασίας και αποκτήστε το πρώτο φύλλο εργασίας

Το πρώτο βήμα είναι να **δημιουργήσετε αντικείμενα έτοιμα για κανόνα μορφοποίησης υπό όρους**: ένα `Workbook` και το προεπιλεγμένο `Worksheet` του. Αυτά τα αντικείμενα είναι το σημείο εισόδου για όλες τις επόμενες λειτουργίες.

```python
# Step 1 – initialize workbook and worksheet
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime

# Create a new, empty workbook
workbook = Workbook()

# Grab the first worksheet (index 0)
worksheet = workbook.worksheets[0]
```

*Γιατί είναι σημαντικό:* Το `Workbook` περιέχει ολόκληρο το αρχείο Excel, ενώ το `Worksheet` είναι όπου εφαρμόζετε κελιά, στυλ και **μορφοποίηση υπό όρους με βάση την ημερομηνία**. Χωρίς αυτά τα αντικείμενα, ο υπόλοιπος κώδικας δεν έχει που να ενεργήσει.

## Βήμα 2: Δημιουργήστε ένα helper για προσθήκη μορφοποίησης υπό όρους TIME_PERIOD

Αντί να επαναλαμβάνετε το ίδιο boiler‑plate για κάθε εύρος, ενσωματώνουμε τη λογική σε μια βοηθητική συνάρτηση. Αυτή η συνάρτηση προσθέτει **μορφοποίηση υπό όρους με χρώμα φόντου** που χρωματίζει τα κελιά βάσει ενός `TimePeriodType` (π.χ. Yesterday, Today, LastWeek).

```python
def add_time_period_condition(cell_range: str, bg_color: Color, period: TimePeriodType):
    """
    Attach a TIME_PERIOD conditional format to `cell_range`.
    The rule highlights cells that fall within `period` using `bg_color`.

    Args:
        cell_range: A1‑style range string, e.g., "I19:K20".
        bg_color:   Desired background color for matching cells.
        period:     Aspose.Cells TimePeriodType enum value.
    Returns:
        The FormatConditionCollection for further customization if needed.
    """
    # 1️⃣ Attach a new ConditionalFormatting block to the specified range
    worksheet.conditional_formattings.add(cell_range)

    # 2️⃣ Grab the collection of conditions for that block
    conditions = worksheet.conditional_formattings[-1].format_conditions

    # 3️⃣ (Optional) Set a default background for the whole range
    conditions.back_color = bg_color

    # 4️⃣ Add a TIME_PERIOD condition and configure its appearance
    idx = conditions.add_condition(FormatConditionType.TIME_PERIOD)
    condition = conditions[idx]

    # Apply the visual style – pink background in this example
    condition.style.background_color = Color.pink
    condition.style.pattern = BackgroundType.SOLID

    # Define which period triggers the formatting
    condition.time_period = period

    return conditions
```

*Γιατί χρησιμοποιούμε helper:* Απομονώνει τη λογική του **μορφοποίησης υπό όρους με βάση την ημερομηνία**, κάνοντας τον κώδικα πιο ευανάγνωστο, δοκιμαστέο και επαναχρησιμοποιήσιμο σε πολλαπλά φύλλα ή έργα.

## Βήμα 3: Εφαρμόστε τον κανόνα μορφοποίησης υπό όρους σε συγκεκριμένο εύρος

Τώρα χρησιμοποιούμε το helper για να επισημάνουμε τα κελιά που περιέχουν “Yesterday”. Αυτό είναι το κεντρικό μέρος της λειτουργίας **δημιουργίας κανόνα μορφοποίησης υπό όρους**.

```python
# Step 3 – highlight cells I19:K20 that contain “Yesterday”
add_time_period_condition(
    cell_range="I19:K20",
    bg_color=Color.medium_sea_green,   # optional default background for the whole range
    period=TimePeriodType.YESTERDAY   # the date‑based trigger
)
```

Όταν ανοίξει το βιβλίο εργασίας, οποιοδήποτε κελί στο `I19:K20` του οποίου η ημερομηνία ισούται με τη χθεσινή ημερομηνία θα εμφανιστεί με ροζ γέμισμα (το στυλ που ορίσαμε στο helper). Το όρισμα `bg_color` δείχνει πώς μπορείτε να προσθέσετε ένα προεπιλεγμένο φόντο πίσω από το χρώμα υπό όρους, εάν το επιθυμείτε.

## Βήμα 4: Συμπληρώστε το εύρος με δείγμα ημερομηνιών

Ένας κανόνας υπό όρους γίνεται ορατός μόνο αφού το φύλλο εργασίας περιέχει δεδομένα που ικανοποιούν την προϋπόθεση. Θα εισάγουμε δύο ημερομηνίες: μία που ταιριάζει με το “Yesterday” και μία που βρίσκεται εκτός της περιόδου.

```python
# Step 4 – insert sample dates for demonstration

# Cell I19 will match the YESTERDAY period
yesterday_cell = worksheet.cells.get("I19")
yesterday_cell.put_value(datetime(2008, 7, 30))   # 30‑Jul‑2008 is “yesterday” relative to 31‑Jul‑2008
yesterday_cell.get_style().number = 30          # 30 = built‑in date format
yesterday_cell.set_style(yesterday_cell.get_style())

# Cell K20 will NOT match the period (it’s a later date)
outside_cell = worksheet.cells.get("K20")
outside_cell.put_value(datetime(2008, 8, 3))     # 03‑Aug‑2008 is outside “Yesterday”
outside_cell.get_style().number = 30
outside_cell.set_style(outside_cell.get_style())

# Optional label for clarity – not part of the rule
worksheet.cells.get("I20").put_value("Yesterday")
```

*Γιατί είναι σημαντικό:* Χρησιμοποιώντας αντικείμενα `datetime` διασφαλίζουμε ότι το Excel αντιμετωπίζει τις τιμές ως πραγματικές ημερομηνίες, κάτι που απαιτείται για τη σωστή λειτουργία της **μορφοποίησης υπό όρους με βάση την ημερομηνία**. Η αριθμητική μορφή (`30`) εγγυάται ότι τα κελιά εμφανίζονται ως αναγνωρίσιμες ημερομηνίες.

## Βήμα 5: Αυτόματη προσαρμογή στήλης και αποθήκευση του βιβλίου εργασίας

Αφού τα δεδομένα και η μορφοποίηση είναι στη θέση τους, το τελευταίο βήμα είναι να **προσαρμόσετε αυτόματα** το πλάτος των στηλών ώστε οι ημερομηνίες να είναι πλήρως ορατές. Στη συνέχεια γράφουμε το αρχείο στο δίσκο.

```python
# Step 5 – adjust column width and save the file

# Auto‑fit column 12 (the column that contains our sample data)
worksheet.auto_fit_column(12)

# Save the workbook as an XLSX file
output_path = "YOUR_DIRECTORY/TimePeriodDemo.out.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to {output_path}")
```

Η κλήση `auto_fit_column` εξετάζει το μεγαλύτερο περιεχόμενο στη στήλη 12 (που αντιστοιχεί στη στήλη **L** του Excel) και επεκτείνει το πλάτος αναλόγως. Αυτό το μικρό βήμα αποτρέπει την αποκοπή των ημερομηνιών και κάνει τη **μορφοποίηση υπό όρους με χρώμα φόντου** σαφώς ορατή.

### Αναμενόμενο αποτέλεσμα

Όταν ανοίξετε το `TimePeriodDemo.out.xlsx`:

| I19 (date) | I20 (label) | K20 (date) |
|------------|------------|------------|
| 30‑Jul‑2008 (highlighted pink) | Yesterday | 03‑Aug‑2008 (no highlight) |

* Το κελί με τη χθεσινή ημερομηνία εμφανίζει ροζ φόντο επειδή ο **κανόνας μορφοποίησης υπό όρους** ταιριάζει με την περίοδο `YESTERDAY`.  
* Όλα τα άλλα κελιά διατηρούν το προεπιλεγμένο φόντο (ή το προαιρετικό `medium_sea_green` που δώσατε).  
* Η στήλη L έχει αυτόματα αυξηθεί σε πλάτος, ώστε οι ημερομηνίες να είναι πλήρως αναγνώσιμες.

## Κοινές παραλλαγές και ειδικές περιπτώσεις

| Κατάσταση | Πώς να προσαρμόσετε τον κώδικα |
|-----------|------------------------------|
| **Επισημάνετε “Today” αντί για “Yesterday”** | Αντικαταστήστε `TimePeriodType.YESTERDAY` με `TimePeriodType.TODAY`. |
| **Χρησιμοποιήστε διαφορετικό χρώμα φόντου** | Αλλάξτε `condition.style.background_color = Color.pink` σε οποιοδήποτε άλλο `Color` (π.χ. `Color.light_sky_blue`). |
| **Εφαρμόστε τον κανόνα σε μη συνεχές εύρος** | Καλέστε `add_time_period_condition` πολλές φορές με διαφορετικά `cell_range` strings (π.χ. `"A1:A10", "C1:C10"`). |
| **Δουλέψτε με προϋπάρχον βιβλίο εργασίας** | Φορτώστε το αρχείο με `Workbook("myfile.xlsx")` αντί να δημιουργήσετε νέο. |
| **Πολλαπλές συνθήκες βάσει ημερομηνίας στο ίδιο εύρος** | Μετά την πρώτη κλήση `add_time_period_condition`, προσθέστε άλλη συνθήκη με `conditions.add_condition(FormatConditionType.TIME_PERIOD)` και ορίστε διαφορετικό `time_period`. |

## Συμπέρασμα

Τώρα ξέρετε πώς να **δημιουργήσετε κανόνα μορφοποίησης υπό όρους** που αντιδρά σε ημερομηνίες, να εφαρμόσετε **μορφοποίηση υπό όρους με χρώμα φόντου** και να **προσαρμόσετε αυτόματα** το πλάτος των στηλών χρησιμοποιώντας το Aspose.Cells for Python. Η βοηθητική συνάρτηση αφαιρεί τη λογική, επιτρέποντάς σας να επαναχρησιμοποιήσετε το ίδιο μοτίβο για οποιοδήποτε σενάριο **μορφοποίησης υπό όρους με βάση την ημερομηνία**—είτε είναι “Yesterday”, “LastWeek” ή μια προσαρμοσμένη περίοδος.

Στη συνέχεια, μπορείτε να εξερευνήσετε:

* Προσθήκη **icon sets** ή **data bars** παράλληλα με τους κανόνες ημερομηνίας.  
* Δημιουργία δυναμικών αναφορών που αντλούν ημερομηνίες από βάση δεδομένων.  
* Συνδυασμό πολλαπλών **κανόνων μορφοποίησης υπό όρους με βάση την ημερομηνία** σε ένα φύλλο.

Μη διστάσετε να πειραματιστείτε με διαφορετικά χρώματα, περιόδους και εύρη ώστε να ταιριάζουν στις ανάγκες του έργου σας. Καλό κώδικα!

## Τι θα πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κυριαρχήσετε επιπλέον δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στην υλοποίηση των δικών σας έργων.

- [Master Conditional Formatting in Excel Using Aspose.Cells .NET: A Comprehensive Guide](/cells/english/net/formatting/mastering-aspose-cells-net-conditional-formatting/)
- [How to Extract Conditional Formatting Colors Using Aspose.Cells for .NET](/cells/english/net/formatting/extract-conditional-formatting-colors-aspose-cells-net/)
- [Master Conditional Formatting with Custom Fonts in Excel using Aspose.Cells for .NET and C#](/cells/english/net/formatting/conditional-formatting-custom-fonts-aspose-csharp/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}