---
category: general
date: 2026-06-21
description: Οδηγός μορφοποίησης ημερομηνίας Aspose Cells – μάθετε πώς να ορίσετε
  προσαρμοσμένη μορφή ημερομηνίας, να αλλάξετε τη γλώσσα του βιβλίου εργασίας και
  να εφαρμόσετε μια παγκόσμια μορφή ημερομηνίας σε Java.
draft: false
keywords:
- aspose cells date format
- set custom date format
- how to set date format
- change workbook locale
- set global date format
language: el
og_description: 'Οδηγός μορφοποίησης ημερομηνίας Aspose Cells: μάθετε πώς να ορίσετε
  προσαρμοσμένη μορφή ημερομηνίας, να αλλάξετε τη γλώσσα του βιβλίου εργασίας και
  να ορίσετε καθολική μορφή ημερομηνίας για έργα Java.'
og_title: Μορφή Ημερομηνίας Aspose Cells – Ορισμός Προσαρμοσμένης Μορφής Ημερομηνίας
  σε Java
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Aspose Cells date format guide – learn how to set custom date format,
    change workbook locale, and apply a global date format in Java.
  headline: 'Aspose Cells Date Format: How to Set Custom Date Format in Java'
  type: TechArticle
- description: Aspose Cells date format guide – learn how to set custom date format,
    change workbook locale, and apply a global date format in Java.
  name: 'Aspose Cells Date Format: How to Set Custom Date Format in Java'
  steps:
  - name: 1. Overriding the Global Format at the Cell Level
    text: 'If a cell already has a style with a specific number format, the global
      setting is ignored for that cell. To force the global format, clear the cell’s
      style:'
  - name: 2. Changing Workbook Locale Without a Custom Pattern
    text: 'Sometimes you just want to **change workbook locale** so that built‑in
      date formats (like `14‑03‑2024`) follow regional conventions. You can do this
      without a `DateTimeFormatter`:'
  - name: 3. Using Multiple Custom Formats in One Workbook
    text: 'Aspose Cells allows you to define several custom formats and apply them
      selectively:'
  - name: 4. Resetting to the Default Format
    text: 'If you need to revert to Aspose’s default date handling, simply pass `null`:'
  type: HowTo
- questions:
  - answer: Yes—any worksheet loaded into the `Workbook` after you set the global
      format will inherit it, unless a cell already has an explicit style.
    question: Does this affect existing worksheets?
  - answer: Absolutely. The global format is applied at render time, so you can populate
      cells first and set the format later.
    question: Can I set the format after writing data?
  - answer: Use the appropriate `CultureInfo` code (`"th-TH"`), and the formatter
      will respect that calendar automatically.
    question: What if I need a locale‑specific calendar (e.g., Thai Buddhist)?
  - answer: Negligible. The formatter is cached inside `WorkbookSettings`, so the
      overhead is only incurred once per workbook.
    question: Is there a performance penalty?
  type: FAQPage
tags:
- aspose-cells
- java
- date-formatting
title: 'Μορφή Ημερομηνίας Aspose Cells: Πώς να ορίσετε προσαρμοσμένη μορφή ημερομηνίας
  σε Java'
url: /el/java/formatting/aspose-cells-date-format-how-to-set-custom-date-format-in-ja/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose Cells Date Format – Πλήρης Οδηγός Java

Έχετε αναρωτηθεί ποτέ πώς να ορίσετε προσαρμοσμένη μορφή ημερομηνίας στο Aspose Cells για Java; Δεν είστε οι μόνοι. Είτε δημιουργείτε αναφορές για έναν Ιάπωνα πελάτη είτε χρειάζεστε ένα συνεπές στυλ ημερομηνίας σε ολόκληρο το βιβλίο εργασίας, η κατάκτηση του **aspose cells date format** είναι απαραίτητη.

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από ένα πρακτικό, ολοκληρωμένο παράδειγμα που δείχνει **πώς να ορίσετε μορφή ημερομηνίας** παγκοσμίως, να αλλάξετε τη γλώσσα του βιβλίου εργασίας και να εφαρμόσετε ένα προσαρμοσμένο μοτίβο όπως το έτος της ιαπωνικής εποχής. Στο τέλος θα έχετε ένα επαναχρησιμοποιήσιμο snippet που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο — χωρίς εικασίες.

## What This Guide Covers

- Δημιουργία μιας νέας παρουσίας `Workbook`.
- Αλλαγή της γλώσσας του βιβλίου εργασίας ώστε οι ενσωματωμένες μορφές να σέβονται τους περιφερειακούς κανόνες.
- Ορισμός **set custom date format** χρησιμοποιώντας `DateTimeFormatter`.
- Εφαρμογή αυτής της μορφής παγκοσμίως με `WorkbookSettings`.
- Συνηθισμένα προβλήματα (π.χ. υπερίσχυση μορφών σε επίπεδο κελιού) και πώς να τα αποφύγετε.
- Γρήγορες παραλλαγές για άλλες γλώσσες ή αλφαριθμητικά μορφής.

Χρειάζεστε μόνο ένα περιβάλλον ανάπτυξης Java, Maven ή Gradle για να προσθέσετε το Aspose Cells, και μια βασική κατανόηση της σύνταξης Java. Έτοιμοι; Ας βουτήξουμε.

## Step 1: Set Up Your Project and Import Aspose Cells

Πρώτα απ' όλα—βεβαιωθείτε ότι το Aspose Cells for Java βρίσκεται στο classpath σας. Αν χρησιμοποιείτε Maven, προσθέστε την παρακάτω εξάρτηση στο `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest stable version -->
</dependency>
```

Οι χρήστες Gradle μπορούν να προσθέσουν:

```gradle
implementation 'com.aspose:aspose-cells:24.9'
```

> **Pro tip:** Το Aspose προσφέρει δωρεάν άδεια δοκιμής 30 ημερών. Τοποθετήστε το αρχείο `Aspose.Cells.lic` στη ρίζα του έργου σας και καλέστε `License license = new License(); license.setLicense("Aspose.Cells.lic");` πριν δημιουργήσετε οποιοδήποτε βιβλίο εργασίας.

Τώρα εισάγουμε τις κλάσεις που θα χρειαστούμε:

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.WorkbookSettings;
import com.aspose.cells.DateTimeFormatter;
import com.aspose.cells.CultureInfo;
```

Αυτές οι εισαγωγές μας δίνουν πρόσβαση στον container του βιβλίου εργασίας, στις ρυθμίσεις του και στον formatter που σέβεται την τοπική γλώσσα.

## Step 2: Create a New Workbook and Access Its Settings

Μια νέα `Workbook` ξεκινά με την προεπιλεγμένη (συνήθως US) γλώσσα. Για να ελέγξετε τη διαχείριση ημερομηνιών παγκοσμίως, πρέπει να πάρουμε το αντικείμενο `WorkbookSettings`:

```java
// Step 2: Initialize a new workbook
Workbook workbook = new Workbook();

// Grab the settings object – this is where we’ll apply the date format
WorkbookSettings settings = workbook.getSettings();
```

Το αντικείμενο `settings` είναι το κεντρικό σημείο. Οτιδήποτε αλλάξετε εδώ — όπως η μορφή ημερομηνίας — επηρεάζει κάθε κελί που **δεν** έχει ήδη ένα ρητό στυλ που το υπερισχύει.

## Step 3: Define a Custom Date/Time Format (Japanese Era Example)

Ας υποθέσουμε ότι χρειάζεστε ημερομηνίες στο ιαπωνικό φορμά εποχής, π.χ. “令和04.10.01”. Το μοτίβο `"ggyy.MM.dd"` κάνει τη δουλειά όταν συνδυαστεί με ιαπωνική κουλτούρα:

```java
// Step 3: Build a formatter for the Japanese era year
DateTimeFormatter formatter = new DateTimeFormatter(
        "ggyy.MM.dd",                // Pattern: era (gg), year (yy), month, day
        new CultureInfo("ja-JP")    // Locale: Japanese (Japan)
);
```

Αν προτιμάτε ένα πιο απλό στυλ ISO (`"yyyy-MM-dd"`), απλώς αντικαταστήστε το αλφαριθμητικό μοτίβο — δεν απαιτούνται άλλες αλλαγές.

## Step 4: Apply the Custom Format as the Global Date Format

Τώρα συνδέουμε τον formatter με τις παγκόσμιες ρυθμίσεις του βιβλίου εργασίας. Αυτό είναι το βήμα **set global date format** που εξασφαλίζει ότι οποιοδήποτε κελί εμφανίζει ημερομηνία θα χρησιμοποιεί αυτόματα το μοτίβό μας:

```java
// Step 4: Apply the custom formatter globally
settings.setDateTimeFormat(formatter);
```

Σε αυτό το σημείο, οποιαδήποτε ημερομηνία γράψετε στο φύλλο — είτε μέσω `Cell.putValue(new Date())` είτε διαβάζοντας από πηγή δεδομένων — θα εμφανίζεται με το ιαπωνικό μοτίβο εποχής.

## Step 5: Populate the Workbook with Sample Dates (Optional)

Ας προσθέσουμε μερικές γραμμές ώστε να δείτε τη μορφή σε δράση. Αυτό το τμήμα δεν είναι απολύτως απαραίτητο για τη λογική μορφοποίησης, αλλά βοηθάει στην επαλήθευση ότι όλα λειτουργούν:

```java
// Step 5: Insert sample dates into the first sheet
var sheet = workbook.getWorksheets().get(0);
var cells = sheet.getCells();

cells.get("A1").putValue(new java.util.Date()); // Today’s date
cells.get("A2").putValue(java.sql.Date.valueOf("2024-12-31")); // Specific date
cells.get("A3").putValue(java.time.LocalDateTime.now()); // Date‑time now
```

Όταν αποθηκεύσετε το βιβλίο εργασίας, αυτά τα κελιά θα εμφανίσουν κάτι όπως:

```
A1: 令和05.04.21
A2: 令和06.12.31
A3: 令和05.04.21 14:37:12
```

(Το ακριβές έτος εποχής εξαρτάται από το τρέχον ιαπωνικό ημερολόγιο.)

## Step 6: Save the Workbook and Verify the Output

Τέλος, γράψτε το βιβλίο εργασίας σε αρχείο ώστε να το ανοίξετε στο Excel, LibreOffice ή οποιονδήποτε προβολέα που σέβεται τη μορφή:

```java
// Step 6: Save the workbook
workbook.save("CustomDateFormatDemo.xlsx");
System.out.println("Workbook saved with custom date format.");
```

Ανοίξτε το `CustomDateFormatDemo.xlsx` και θα δείτε τις ημερομηνίες να αποδίδονται σύμφωνα με το μοτίβο που ορίσαμε. Αν παρατηρήσετε ασυμφωνία, ελέγξτε ξανά ότι κανένα στυλ σε επίπεδο κελιού δεν υπερισχύει της παγκόσμιας ρύθμισης (δείτε την ενότητα “Edge Cases” παρακάτω).

## Edge Cases & Variations

### 1. Overriding the Global Format at the Cell Level

Αν ένα κελί έχει ήδη στυλ με συγκεκριμένη μορφή αριθμού, η παγκόσμια ρύθμιση αγνοείται για εκείνο το κελί. Για να επιβάλετε τη παγκόσμια μορφή, καθαρίστε το στυλ του κελιού:

```java
cells.get("A1").getStyle().setNumber(0); // Reset number format to default
```

### 2. Changing Workbook Locale Without a Custom Pattern

Μερικές φορές θέλετε απλώς να **change workbook locale** ώστε οι ενσωματωμένες μορφές ημερομηνίας (π.χ. `14‑03‑2024`) να ακολουθούν τις περιφερειακές συμβάσεις. Μπορείτε να το κάνετε αυτό χωρίς `DateTimeFormatter`:

```java
WorkbookSettings localeSettings = workbook.getSettings();
localeSettings.setCultureInfo(new CultureInfo("fr-FR")); // French (France)
```

Τώρα οποιαδήποτε προεπιλεγμένη μορφή ημερομηνίας θα εμφανίζεται ως `21/04/2025` αντί για `04/21/2025`.

### 3. Using Multiple Custom Formats in One Workbook

Το Aspose Cells επιτρέπει τον ορισμό πολλαπλών προσαρμοσμένων μορφών και την εφαρμογή τους επιλεκτικά:

```java
// Define two formatters
DateTimeFormatter usFormatter = new DateTimeFormatter("MM/dd/yyyy", new CultureInfo("en-US"));
DateTimeFormatter jpFormatter = new DateTimeFormatter("ggyy.MM.dd", new CultureInfo("ja-JP"));

// Apply US format globally
settings.setDateTimeFormat(usFormatter);

// Later, apply Japanese format to a specific range
var style = workbook.createStyle();
style.setCustom(usFormatter.getFormatString()); // Or jpFormatter.getFormatString()
cells.get("B1").setStyle(style);
```

### 4. Resetting to the Default Format

Αν χρειαστεί να επανέλθετε στην προεπιλεγμένη διαχείριση ημερομηνίας του Aspose, απλώς περάστε `null`:

```java
settings.setDateTimeFormat(null); // Clears the custom global format
```

## Common Questions Answered

- **Does this affect existing worksheets?**  
  Ναι — οποιοδήποτε φύλλο εργασίας φορτωθεί στο `Workbook` μετά τον ορισμό της παγκόσμιας μορφής θα το κληρονομήσει, εκτός αν το κελί έχει ήδη ρητό στυλ.

- **Can I set the format after writing data?**  
  Απόλυτα. Η παγκόσμια μορφή εφαρμόζεται κατά το χρόνο απόδοσης, οπότε μπορείτε να γεμίσετε τα κελιά πρώτα και να ορίσετε τη μορφή αργότερα.

- **What if I need a locale‑specific calendar (e.g., Thai Buddhist)?**  
  Χρησιμοποιήστε τον κατάλληλο κωδικό `CultureInfo` (`"th-TH"`), και ο formatter θα σέβεται αυτό το ημερολόγιο αυτόματα.

- **Is there a performance penalty?**  
  Αμελητέος. Ο formatter αποθηκεύεται στην κρυφή μνήμη του `WorkbookSettings`, οπότε το κόστος είναι μόνο μία φορά ανά βιβλίο εργασίας.

## Full Working Example

Παρακάτω βρίσκεται το πλήρες, έτοιμο‑για‑εκτέλεση πρόγραμμα που ενσωματώνει κάθε βήμα που συζητήθηκε:

```java
import com.aspose.cells.*;

public class AsposeCellsDateFormatDemo {
    public static void main(String[] args) throws Exception {
        // Apply license if you have one
        // License lic = new License();
        // lic.setLicense("Aspose.Cells.lic");

        // 1️⃣ Create workbook
        Workbook workbook = new Workbook();

        // 2️⃣ Access settings
        WorkbookSettings settings = workbook.getSettings();

        // 3️⃣ Define custom Japanese era format
        DateTimeFormatter jpFormatter = new DateTimeFormatter(
                "ggyy.MM.dd",
                new CultureInfo("ja-JP")
        );

        // 4️⃣ Set as global date format
        settings.setDateTimeFormat(jpFormatter);

        // 5️⃣ Add sample dates
        var sheet = workbook.getWorksheets().get(0);
        var cells = sheet.getCells();

        cells.get("A1").putValue(new java.util.Date());                     // Today
        cells.get("A2").putValue(java.sql.Date.valueOf("2024-12-31"));      // Fixed date
        cells.get("A3").putValue(java.time.LocalDateTime.now());           // Date‑time now

        // 6️⃣ Save to file
        workbook.save("AsposeCellsCustomDateFormat.xlsx");
        System.out.println("Workbook saved with custom Japanese era date format.");
    }
}
```

**Αναμενόμενη έξοδος στο Excel:**

| Cell | Rendered Value |
|------|----------------|
| A1   | 令和05.04.21   |
| A2   | 令和06.12.31   |
| A3   | 令和05.04.21 14:45:03 (το τμήμα ώρας μπορεί να διαφέρει) |

Ανοίξτε το αρχείο και θα δείτε τις ημερομηνίες μορφοποιημένες ακριβώς όπως ορίσατε.

## Conclusion

Μόλις μάθατε πώς να **aspose cells date format** ένα βιβλίο εργασίας σε Java, από την αλλαγή της γλώσσας μέχρι την εφαρμογή ενός **set custom date format** που λειτουργεί παγκοσμίως. Με τη χρήση του `WorkbookSettings` και του `DateTimeFormatter`, αποκτάτε ακριβή έλεγχο πάνω στο πώς εμφανίζεται κάθε ημερομηνία — χωρίς να χρειάζεται χειροκίνητη μορφοποίηση.

Στη συνέχεια, μπορείτε να εξερευνήσετε **how to set date format** για συγκεκριμένες στήλες μόνο, ή να συνδυάσετε προσαρμοσμένες μορφές αριθμών με conditional formatting για ένα πιο επαγγελματικό report. Οι ίδιες αρχές ισχύουν: ορίστε έναν formatter, συνδέστε τον μέσω στυλ, και αφήστε το Aspose να κάνει το υπόλοιπο.

Καλή προγραμματιστική δουλειά, και μη διστάσετε να πειραματιστείτε με άλλες γλώσσες — οι χρήστες σας θα εκτιμήσουν τα καλοσχεδιασμένα, πολιτιστικά προσαρμοσμένα spreadsheets!

## What Should You Learn Next?

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Efficiently Convert Excel to PDF with Custom Date Formats Using Aspose.Cells for Java](/cells/english/java/workbook-operations/render-excel-custom-date-formats-pdf-aspose-cells-java/)
- [Mastering Data Presentation in Excel: Number and Custom Date Formatting with Aspose.Cells for Java](/cells/english/java/formatting/aspose-cells-java-data-formatting-excel/)
- [How to Create & Format Excel Cells Using Aspose.Cells for Java: A Step‑By‑Step Guide](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}