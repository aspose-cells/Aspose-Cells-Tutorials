---
category: general
date: 2026-09-08
description: Πώς να αντιγράψετε περιοχή σε Java χρησιμοποιώντας το Aspose.Cells –
  μάθετε πώς να αντιγράψετε έναν πίνακα Pivot, να δημιουργήσετε αντίγραφο του πίνακα
  Pivot και να εξάγετε τον πίνακα Pivot διατηρώντας τη μορφοποίηση.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy range
- copy pivot table
- duplicate pivot table
- export pivot table
- copy range with formatting
language: el
lastmod: 2026-09-08
og_description: Πώς να αντιγράψετε μια περιοχή σε Java με το Aspose.Cells. Αυτό το
  σεμινάριο δείχνει πώς να αντιγράψετε έναν πίνακα Pivot, να δημιουργήσετε αντίγραφο
  του πίνακα Pivot και να εξάγετε τον πίνακα Pivot διατηρώντας τη μορφοποίηση.
og_image_alt: Screenshot of Java code copying a pivot table range in Aspose.Cells
og_title: Πώς να αντιγράψετε περιοχή σε Java – πλήρης οδηγός Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-09-08'
  description: How to copy range in Java using Aspose.Cells – learn to copy pivot
    table, duplicate pivot table, and export pivot table while preserving formatting.
  headline: How to copy range in Java with Aspose.Cells
  type: TechArticle
- description: How to copy range in Java using Aspose.Cells – learn to copy pivot
    table, duplicate pivot table, and export pivot table while preserving formatting.
  name: How to copy range in Java with Aspose.Cells
  steps:
  - name: Copy pivot table to an existing workbook
    text: 'If you need to **duplicate pivot table** inside a workbook that already
      has data, use the same `copyRange` call but point to a different destination
      address:'
  - name: Export pivot table only (without surrounding data)
    text: 'Sometimes you want just the pivot table, not the source data. Identify
      the pivot table’s display range via its `getPivotTable` method:'
  - name: Preserve conditional formatting
    text: 'Conditional formatting rules are part of the style collection. The `PasteType.ALL`
      flag already copies them, but you can be explicit:'
  - name: Edge cases and troubleshooting
    text: '| Situation | What to watch for | Recommended fix | |-----------|-------------------|-----------------|
      | Source and destination workbooks use different Excel versions | Some newer
      pivot features (e.g., data model) may not render correctly | Use the latest
      Aspose.Cells version and set `Workbook.setF'
  - name: Next steps
    text: '- Explore **copy range with formatting** for charts and images (use `PasteType.PICTURES`).
      - Automate batch processing: loop over multiple source files and consolidate
      their pivot tables into a summary workbook. - Combine this technique with Aspose.Slides
      to generate PowerPoint reports that embed th'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Πώς να αντιγράψετε εύρος στη Java με το Aspose.Cells
url: /el/java/range-management/how-to-copy-range-in-java-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να αντιγράψετε περιοχή σε Java με Aspose.Cells

Αν χρειάζεστε **how to copy range** σε Java, το Aspose.Cells κάνει την εργασία απλή. Είτε μετακινείτε ένα κανονικό μπλοκ κελιών είτε έναν πλήρη πίνακα Pivot, η βιβλιοθήκη διαχειρίζεται την ενέργεια αντιγραφής διατηρώντας τους τύπους, τα στυλ και την κρυφή μνήμη του Pivot. Σε αυτόν τον οδηγό θα μάθετε να **copy pivot table**, **duplicate pivot table**, και ακόμη **export pivot table** σε νέο βιβλίο εργασίας με πλήρη μορφοποίηση.

Το tutorial καλύπτει τα πάντα, από τη ρύθμιση του έργου μέχρι το τελικό βήμα επαλήθευσης, ώστε να μπορείτε να εκτελέσετε τον κώδικα αμέσως μετά την ανάγνωση. Δεν απαιτούνται εξωτερικά εργαλεία πέρα από το Aspose.Cells for Java JAR.

## Προαπαιτούμενα

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

- Java 17 (ή οποιοδήποτε υποστηριζόμενο JDK) εγκατεστημένο και ρυθμισμένο στο IDE σας.
- Maven ή Gradle για διαχείριση εξαρτήσεων (τα παραδείγματα χρησιμοποιούν Maven).
- Ένα αρχείο Excel πηγής (`source.xlsx`) που περιέχει έναν πίνακα Pivot στην περιοχή `A1:H20`.
- Βασική εξοικείωση με τον προγραμματισμό σε Java.

## Βήμα 1: Προσθέστε το Aspose.Cells στο έργο σας

Το Aspose.Cells είναι εμπορική βιβλιοθήκη, αλλά είναι διαθέσιμη μια δωρεάν έκδοση αξιολόγησης. Προσθέστε την εξάρτηση στο `pom.xml` σας:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest version -->
</dependency>
```

> **Pro tip:** Αν προτιμάτε Gradle, η ισοδύναμη καταχώρηση είναι:
> ```gradle
> implementation 'com.aspose:aspose-cells:24.9'
> ```

Η προσθήκη του JAR σας δίνει πρόσβαση στις κλάσεις `Workbook`, `Worksheet`, `Range` και `CopyOptions` που χρησιμοποιούνται σε όλο τον οδηγό.

## Βήμα 2: Φορτώστε το βιβλίο εργασίας πηγής και επιλέξτε το πρώτο φύλλο

Το πρώτο μέρος του **how to copy range** είναι το άνοιγμα του βιβλίου εργασίας που περιέχει τα δεδομένα που θέλετε να μετακινήσετε.

```java
import com.aspose.cells.*;

public class CopyRangeDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        // Select the first worksheet (index 0)
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);
```

> **Why this matters:** Το άνοιγμα του βιβλίου εργασίας δημιουργεί μια αναπαράσταση στη μνήμη που το API μπορεί να χειριστεί χωρίς να αγγίξει το αρχικό αρχείο στο δίσκο.

## Βήμα 3: Ορίστε την περιοχή που περιέχει τον πίνακα Pivot

Ένας πίνακας Pivot ζει μέσα σε ένα ορθογώνιο μπλοκ. Πρέπει να καθορίσετε αυτό το μπλοκ ώστε το Aspose.Cells να ξέρει τι να αντιγράψει.

```java
        // Define the range that holds the pivot table and its source data
        Range sourceRange = sourceSheet.getCells().createRange("A1:H20");
```

> **Note:** Η μέθοδος `createRange` **δεν** αντιγράφει τίποτα ακόμη· δημιουργεί μόνο ένα αντικείμενο `Range` που δείχνει στα κελιά που προτίθεστε να διπλασιάσετε.

## Βήμα 4: Δημιουργήστε ένα νέο βιβλίο εργασίας και πάρτε το πρώτο του φύλλο

Τώρα δημιουργήστε το βιβλίο εργασίας προορισμού όπου θα τοποθετηθεί η αντιγραμμένη περιοχή.

```java
        // Create an empty workbook for the destination
        Workbook destWorkbook = new Workbook();
        // Get its first (and only) worksheet
        Worksheet destSheet = destWorkbook.getWorksheets().get(0);
```

> **Why a new workbook?** Η χρήση ενός φρέσκου αρχείου εγγυάται ότι δεν υπάρχουν κρυφά στυλ ή ονομαστικές περιοχές που να επηρεάζουν την ενέργεια αντιγραφής, κάτι ιδιαίτερα σημαντικό όταν **export pivot table** σε ξεχωριστό αρχείο.

## Βήμα 5: Αντιγράψτε την περιοχή (συμπεριλαμβανομένου του πίνακα Pivot) στο φύλλο προορισμού

Αυτό είναι το κέντρο του **how to copy range with formatting**. Το αντικείμενο `CopyOptions` λέει στο Aspose.Cells να διατηρήσει τα πάντα: τιμές, τύπους, στυλ και κρυφή μνήμη Pivot.

```java
        // Prepare copy options – preserve formatting and pivot cache
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.ALL); // copies everything
        copyOptions.setSkipBlanks(false);        // keep blank cells

        // Copy the defined range to cell A1 of the destination sheet
        destSheet.getCells().copyRange(sourceRange, "A1", copyOptions);
```

> **Copy pivot table:** Επειδή η περιοχή προέλευσης περιλαμβάνει τον πίνακα Pivot, το API αυτόματα διπλασιάζει την κρυφή μνήμη, έτσι ώστε το νέο φύλλο να περιέχει έναν πλήρως λειτουργικό πίνακα Pivot που συμπεριφέρεται ακριβώς όπως ο αρχικός.

## Βήμα 6: Αποθηκεύστε το βιβλίο εργασίας προορισμού

Τέλος, γράψτε το αποτέλεσμα στο δίσκο.

```java
        // Save the destination workbook
        destWorkbook.save("YOUR_DIRECTORY/dest.xlsx");
    }
}
```

Όταν ανοίξετε το `dest.xlsx`, θα δείτε ένα ακριβές αντίγραφο του αρχικού πίνακα Pivot, συμπεριλαμβανομένης της μορφοποίησης, των slicers και των υπολογιζόμενων πεδίων.

## Αναμενόμενο αποτέλεσμα

- Το `dest.xlsx` περιέχει ένα φύλλο με όνομα **Sheet1**.
- Τα κελιά `A1:H20` κρατούν τα ίδια δεδομένα και τον ίδιο πίνακα Pivot με την πηγή.
- Όλα τα στυλ κελιών (γραμματοσειρές, χρώματα, περιγράμματα) διατηρούνται.
- Ο πίνακας Pivot είναι πλήρως διαδραστικός· η ανανέωσή του αντανακλά τα υποκείμενα δεδομένα στην αντιγραμμένη περιοχή.

## Πώς να αντιγράψετε περιοχή με μορφοποίηση – πιο βαθιά ανάλυση

Το προηγούμενο παράδειγμα δείχνει το πιο απλό σενάριο, αλλά μπορεί να συναντήσετε παραλλαγές που απαιτούν ελαφρώς διαφορετική προσέγγιση.

### Αντιγραφή πίνακα Pivot σε υπάρχον βιβλίο εργασίας

Αν χρειάζεται να **duplicate pivot table** μέσα σε βιβλίο εργασίας που ήδη περιέχει δεδομένα, χρησιμοποιήστε την ίδια κλήση `copyRange` αλλά δείξτε σε διαφορετική διεύθυνση προορισμού:

```java
// Assume destWorkbook already contains other sheets
Worksheet targetSheet = destWorkbook.getWorksheets().get(2);
targetSheet.getCells().copyRange(sourceRange, "B5", copyOptions);
```

### Εξαγωγή μόνο του πίνακα Pivot (χωρίς τα γύρω δεδομένα)

Μερικές φορές θέλετε μόνο τον πίνακα Pivot, όχι τα δεδομένα προέλευσης. Εντοπίστε την περιοχή εμφάνισης του πίνακα Pivot μέσω της μεθόδου `getPivotTable`:

```java
PivotTable pt = sourceSheet.getPivotTables().get(0);
String ptArea = pt.getDisplayRange(); // e.g., "C5:G15"
Range pivotOnly = sourceSheet.getCells().createRange(ptArea);
destSheet.getCells().copyRange(pivotOnly, "A1", copyOptions);
```

### Διατήρηση υπό όρους μορφοποίησης

Οι κανόνες υπό όρους μορφοποίησης είναι μέρος της συλλογής στυλ. Η σημαία `PasteType.ALL` τα αντιγράφει ήδη, αλλά μπορείτε να το δηλώσετε ρητά:

```java
copyOptions.setPasteType(PasteType.FORMATS);
copyOptions.setPasteType(PasteType.ALL); // overrides previous, ensures everything
```

### Ακραίες περιπτώσεις και αντιμετώπιση προβλημάτων

| Situation | What to watch for | Recommended fix |
|-----------|-------------------|-----------------|
| Source and destination workbooks use different Excel versions | Some newer pivot features (e.g., data model) may not render correctly | Use the latest Aspose.Cells version and set `Workbook.setFileFormatType(FileFormatType.XLSX)` for both workbooks |
| Very large pivot tables ( > 10 000 rows) cause memory pressure | Out‑of‑memory errors during copy | Enable `Workbook.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` before loading |
| Destination sheet already contains a named range with the same name as the source | Name collision leads to `CopyOptions` failure | Call `copyOptions.setIgnoreNameConflicts(true)` |

## Πλήρες, εκτελέσιμο παράδειγμα

Παρακάτω βρίσκεται το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε‑επικολλήσετε σε μια κλάση Java. Περιλαμβάνει όλες τις εισαγωγές, τον χειρισμό σφαλμάτων και σχόλια.

```java
import com.aspose.cells.*;

public class CopyRangeDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the source workbook
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);

        // 2️⃣ Define the range that includes the pivot table
        Range sourceRange = sourceSheet.getCells().createRange("A1:H20");

        // 3️⃣ Create a new destination workbook
        Workbook destWorkbook = new Workbook();
        Worksheet destSheet = destWorkbook.getWorksheets().get(0);

        // 4️⃣ Configure copy options to keep everything (values, formulas, formatting, pivot cache)
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.ALL);
        copyOptions.setSkipBlanks(false);
        copyOptions.setIgnoreNameConflicts(true); // avoid name collisions

        // 5️⃣ Perform the copy
        destSheet.getCells().copyRange(sourceRange, "A1", copyOptions);

        // 6️⃣ Save the result
        destWorkbook.save("YOUR_DIRECTORY/dest.xlsx");
        System.out.println("Copy completed – dest.xlsx now contains the duplicated pivot table.");
    }
}
```

Τρέξτε το πρόγραμμα, μετά ανοίξτε το `dest.xlsx` για να επαληθεύσετε ότι ο πίνακας Pivot λειτουργεί ακριβώς όπως ο αρχικός.

## Συμπέρασμα

Τώρα γνωρίζετε **how to copy range** σε Java χρησιμοποιώντας το Aspose.Cells, συμπεριλαμβανομένου του πώς να **copy pivot table**, **duplicate pivot table**, και **export pivot table** διατηρώντας όλη τη μορφοποίηση. Η βιβλιοθήκη αφαιρεί τις λεπτομέρειες χαμηλού επιπέδου της δομής XML του Excel, επιτρέποντάς σας να εστιάσετε στη λογική της επιχείρησης.

### Επόμενα βήματα

- Εξερευνήστε **copy range with formatting** για γραφήματα και εικόνες (χρησιμοποιήστε `PasteType.PICTURES`).
- Αυτοματοποιήστε επεξεργασία σε παρτίδες: κάντε βρόχο πάνω από πολλά αρχεία προέλευσης και ενοποιήστε τους πίνακες Pivot τους σε ένα βιβλίο εργασίας σύνοψης.
- Συνδυάστε αυτήν την τεχνική με το Aspose.Slides για να δημιουργήσετε αναφορές PowerPoint που ενσωματώνουν τον αντιγραμμένο πίνακα Pivot.

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικά παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε επιπλέον δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στην υλοποίηση των δικών σας έργων.

- [How to Update Excel Pivot Table Source with Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Optimize Pivot Table Loading in Java using Aspose.Cells – A Comprehensive Guide](/cells/english/java/data-analysis/optimize-pivot-table-loading-aspose-cells-java/)
- [How to Copy Pivot Table in C# – Convert Excel to PPTX, Copy Range & Make Textbox](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}