---
category: general
date: 2026-10-07
description: Μάθετε πώς να αντιγράφετε πίνακες Pivot στο Excel χρησιμοποιώντας Java
  και Aspose.Cells. Αντιγράψτε έναν πίνακα Pivot αντιγράφοντας την περιοχή του μεταξύ
  βιβλίων εργασίας γρήγορα.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to duplicate pivot
- copy pivot table
- copy excel range
- copy range between workbooks
- how to copy pivot table
language: el
lastmod: 2026-10-07
og_description: Πώς να αντιγράψετε πίνακες Pivot στο Excel χρησιμοποιώντας Java και
  Aspose.Cells. Ακολουθήστε αυτόν τον οδηγό για να αντιγράψετε έναν πίνακα Pivot αντιγράφοντας
  την περιοχή του μεταξύ βιβλίων εργασίας.
og_image_alt: Illustration of copying an Excel pivot table from one workbook to another
og_title: Πώς να αντιγράψετε πίνακες Pivot στο Excel με Java – πλήρης οδηγός
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Learn how to duplicate pivot tables in Excel using Java and Aspose.Cells.
    Copy a pivot table by copying its range between workbooks quickly.
  headline: How to duplicate pivot tables in Excel with Java – step‑by‑step guide
  type: TechArticle
- description: Learn how to duplicate pivot tables in Excel using Java and Aspose.Cells.
    Copy a pivot table by copying its range between workbooks quickly.
  name: How to duplicate pivot tables in Excel with Java – step‑by‑step guide
  steps:
  - name: Explanation of each step
    text: '| Step | What the code does | Why it matters for **copy pivot table** |
      |------|-------------------|----------------------------------------| | **1️⃣
      Load source workbook** | `new Workbook(srcPath)` reads `Source.xlsx`. | The
      source file is the only place where the original pivot exists. | | **2️⃣ D'
  - name: 1️⃣ Copying a pivot that spans multiple sheets
    text: 'If the pivot’s source data lives on a different sheet than the pivot itself,
      include both sheets in the copy operation. The simplest approach is to copy
      the entire source sheet first, then copy the pivot sheet:'
  - name: 2️⃣ Dealing with named ranges
    text: 'Aspose.Cells preserves named ranges when you copy a range. However, if
      the destination workbook already contains a name with the same identifier, a
      `CellsException` is thrown. Resolve this by renaming the conflicting name before
      the copy:'
  - name: 3️⃣ Large workbooks and performance
    text: 'Copying very large ranges (hundreds of thousands of rows) can be memory‑intensive.
      Enable **memory optimization**:'
  - name: 4️⃣ Keeping formulas intact
    text: If the source range contains formulas that reference cells outside the copied
      area, those references become broken after the copy. To avoid this, expand the
      range to include all dependent cells, or use `copyRange` with the `CopyOptions`
      flag `CopyOptions.COPY_FORMULA`.
  type: HowTo
tags:
- Excel
- Java
- Aspose.Cells
- PivotTable
- Data manipulation
title: Πώς να αντιγράψετε πίνακες Pivot στο Excel με Java – βήμα‑βήμα οδηγός
url: /el/java/excel-pivot-tables/how-to-duplicate-pivot-tables-in-excel-with-java-step-by-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να αντιγράψετε πίνακες pivot στο Excel με Java – οδηγός βήμα‑βήμα

Αν χρειάζεστε **how to duplicate pivot** πίνακες σε ένα βιβλίο εργασίας Excel, αυτό το tutorial σας παρουσιάζει μια πλήρη, έτοιμη προς εκτέλεση λύση. Χρησιμοποιώντας το Aspose.Cells for Java μπορείτε να αντιγράψετε έναν πίνακα pivot μαζί με τα δεδομένα προέλευσής του αντιγράφοντας την υποκείμενη περιοχή, και στη συνέχεια να αποθηκεύσετε το αποτέλεσμα ως νέο βιβλίο εργασίας.

Η αντιγραφή ενός πίνακα pivot συχνά φαίνεται δύσκολη επειδή η κρυφή μνήμη (pivot cache) είναι κρυμμένη μέσα στο φύλλο. Αντιγράφοντας ολόκληρη την περιοχή που περιέχει το pivot, το Aspose.Cells δημιουργεί αυτόματα τη μνήμη στο βιβλίο εργασίας προορισμού, έτσι λαμβάνετε ένα πλήρως λειτουργικό αντίγραφο χωρίς χειροκίνητη επεξεργασία XML.

Σε αυτόν τον οδηγό θα:

* Φορτώσετε ένα βιβλίο εργασίας προέλευσης που περιέχει πίνακα pivot.  
* Ορίσετε την ακριβή περιοχή που περιέχει το pivot.  
* Αντιγράψετε αυτήν την περιοχή σε ένα νέο βιβλίο εργασίας, διατηρώντας τον ορισμό του pivot.  
* Αποθηκεύσετε το νέο αρχείο και επαληθεύσετε ότι το pivot λειτουργεί.  

Τα βήματα λειτουργούν με οποιαδήποτε έκδοση του Excel που υποστηρίζεται από το Aspose.Cells (2007‑2024) και απαιτούν μόνο λίγες γραμμές κώδικα Java.

## Προαπαιτούμενα

| Απαίτηση | Γιατί είναι σημαντικό |
|----------|------------------------|
| **Java 8 or newer** | Το Aspose.Cells είναι κατασκευασμένο για Java 8+. |
| **Aspose.Cells for Java** (latest version) | Παρέχει τα API `Workbook`, `Range` και `CopyRange` που χρησιμοποιούνται στο παράδειγμα. |
| **Source workbook** with a pivot table (e.g., `Source.xlsx`) | Το pivot που θέλετε να αντιγράψετε. |
| **Write permission** to the target directory | Απαιτείται για την αποθήκευση του `CopyWithPivot.xlsx`. |

Προσθέστε την εξάρτηση Aspose.Cells Maven στο `pom.xml` (ή κατεβάστε το JAR χειροκίνητα):

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>   <!-- use the latest stable version -->
</dependency>
```

## Πώς να αντιγράψετε πίνακες pivot – πλήρης υλοποίηση

Παρακάτω υπάρχει ένα αυτόνομο πρόγραμμα Java που δείχνει **how to duplicate pivot** πίνακες αντιγράφοντας την περιοχή που περιέχει το pivot. Ο κώδικας περιλαμβάνει διαχείριση σφαλμάτων, σχόλια και ένα βήμα επαλήθευσης.

```java
// File: DuplicatePivot.java
import com.aspose.cells.*;

public class DuplicatePivot {
    public static void main(String[] args) {
        // 1️⃣ Load the source workbook that holds the pivot table.
        String srcPath = "YOUR_DIRECTORY/Source.xlsx";
        Workbook srcWb;
        try {
            srcWb = new Workbook(srcPath);
        } catch (Exception e) {
            System.err.println("Failed to load source workbook: " + e.getMessage());
            return;
        }

        // 2️⃣ Identify the range that encloses the pivot table.
        // Adjust the sheet index (0‑based) and address as needed.
        Worksheet srcSheet = srcWb.getWorksheets().get(0);
        // Example address "A1:G20" – includes the pivot and its data source.
        String pivotRangeAddress = "A1:G20";
        Range srcRange = srcSheet.getCells().createRange(pivotRangeAddress);

        // 3️⃣ Create a destination workbook and copy the identified range.
        Workbook destWb = new Workbook(); // starts with a blank workbook
        Worksheet destSheet = destWb.getWorksheets().get(0);
        try {
            // copyRange copies both values and the internal pivot cache.
            destSheet.getCells().copyRange(srcRange, "A1");
        } catch (Exception e) {
            System.err.println("Failed to copy range: " + e.getMessage());
            return;
        }

        // 4️⃣ (Optional) Refresh the pivot so it reflects the copied data.
        // Aspose.Cells automatically rebuilds the cache, but calling refresh
        // guarantees up‑to‑date results if the source data has changed.
        for (int i = 0; i < destSheet.getPivotTables().getCount(); i++) {
            destSheet.getPivotTables().get(i).refresh();
        }

        // 5️⃣ Save the new workbook that now contains the duplicated pivot.
        String destPath = "YOUR_DIRECTORY/CopyWithPivot.xlsx";
        try {
            destWb.save(destPath);
            System.out.println("Pivot table duplicated successfully to: " + destPath);
        } catch (Exception e) {
            System.err.println("Failed to save destination workbook: " + e.getMessage());
        }
    }
}
```

### Επεξήγηση κάθε βήματος

| Βήμα | Τι κάνει ο κώδικας | Γιατί είναι σημαντικό για **copy pivot table** |
|------|-------------------|----------------------------------------|
| **1️⃣ Load source workbook** | `new Workbook(srcPath)` διαβάζει το `Source.xlsx`. | Το αρχείο προέλευσης είναι το μοναδικό σημείο όπου υπάρχει το αρχικό pivot. |
| **2️⃣ Define the range** | `createRange("A1:G20")` δημιουργεί ένα αντικείμενο `Range` που καλύπτει το pivot και τα δεδομένα του. | Ένας πίνακας pivot αποθηκεύεται μαζί με τη μνήμη του (cache); η αντιγραφή ολόκληρης της περιοχής εξασφαλίζει ότι η μνήμη μετακινείται επίσης. |
| **3️⃣ Copy the range** | `copyRange(srcRange, "A1")` γράφει την περιοχή στο φύλλο προορισμού. | Αυτό είναι το βασικό στοιχείο του **copy range between workbooks** – το API διαχειρίζεται αυτόματα τα κρυφά αντικείμενα. |
| **4️⃣ Refresh pivot** | `pivotTable.refresh()` εξαναγκάζει το pivot να επαναϋπολογιστεί. | Εγγυάται ότι το αντιγραμμένο pivot εμφανίζει τις ίδιες τιμές με το αρχικό, ειδικά μετά από τροποποιήσεις. |
| **5️⃣ Save workbook** | `destWb.save(destPath)` γράφει το αρχείο στο δίσκο. | Παράγει το τελικό αποτέλεσμα **copy excel range** που μπορείτε να ανοίξετε στο Excel. |

#### Αναμενόμενο αποτέλεσμα

Μετά την εκτέλεση του προγράμματος, ανοίξτε το `CopyWithPivot.xlsx`. Θα δείτε ένα φύλλο εργασίας που είναι πανομοιότυπο με το αρχικό φύλλο, και ο πίνακας pivot λειτουργεί ακριβώς όπως το αρχικό – μπορείτε να επεκτείνετε γραμμές, να φιλτράρετε πεδία και να ανανεώσετε τα δεδομένα χωρίς σφάλματα.

## Συνηθισμένες παραλλαγές και ειδικές περιπτώσεις

### 1️⃣ Αντιγραφή pivot που εκτείνεται σε πολλά φύλλα

Αν τα δεδομένα προέλευσης του pivot βρίσκονται σε διαφορετικό φύλλο από το ίδιο το pivot, συμπεριλάβετε και τα δύο φύλλα στη λειτουργία αντιγραφής. Η πιο απλή προσέγγιση είναι να αντιγράψετε πρώτα ολόκληρο το φύλλο προέλευσης, και μετά το φύλλο του pivot:

```java
// Copy source data sheet
Workbook temp = new Workbook(); // temporary workbook for the data sheet
temp.getWorksheets().addCopy(srcWb.getWorksheets().get(0));
Workbook dest = new Workbook();
dest.getWorksheets().addCopy(temp.getWorksheets().get(0));

// Then copy the pivot sheet as shown earlier
```

### 2️⃣ Διαχείριση ονομασμένων περιοχών

Το Aspose.Cells διατηρεί τις ονομασμένες περιοχές όταν αντιγράφετε μια περιοχή. Ωστόσο, εάν το βιβλίο εργασίας προορισμού περιέχει ήδη ένα όνομα με το ίδιο αναγνωριστικό, θα προκληθεί `CellsException`. Επίλυση: μετονομάστε το συγκρουόμενο όνομα πριν από την αντιγραφή:

```java
if (destWb.getWorksheets().get(0).getNames().containsKey("MyRange")) {
    destWb.getWorksheets().get(0).getNames().remove("MyRange");
}
```

### 3️⃣ Μεγάλα βιβλία εργασίας και απόδοση

Η αντιγραφή πολύ μεγάλων περιοχών (εκατοντάδες χιλιάδες γραμμές) μπορεί να είναι απαιτητική σε μνήμη. Ενεργοποιήστε **memory optimization**:

```java
LoadOptions loadOptions = new LoadOptions(LoadFormat.XLSX);
loadOptions.setMemorySetting(MemorySetting.MEMORY_PREFERENCE);
Workbook largeSrc = new Workbook(srcPath, loadOptions);
```

### 4️⃣ Διατήρηση των τύπων αμετάβλητων

Εάν η περιοχή προέλευσης περιέχει τύπους που αναφέρονται σε κελιά εκτός της αντιγραμμένης περιοχής, αυτές οι αναφορές θα σπάσουν μετά την αντιγραφή. Για να το αποφύγετε, επεκτείνετε την περιοχή ώστε να περιλαμβάνει όλα τα εξαρτημένα κελιά, ή χρησιμοποιήστε `copyRange` με τη σημαία `CopyOptions` `CopyOptions.COPY_FORMULA`.

```java
CopyOptions options = new CopyOptions();
options.setCopyFormula(true);
destSheet.getCells().copyRange(srcRange, "A1", options);
```

## Επαγγελματικές συμβουλές για αξιόπιστο **copy range between workbooks**

* **Always use absolute addresses** (`$A$1:$G$20`) όταν το φύλλο προέλευσης μπορεί να μετονομαστεί.  
* **Refresh after copy** – ακόμη και αν το Aspose.Cells επαναδημιουργεί τη μνήμη, η κλήση `refresh()` εξαλείφει περιστασιακές προειδοποιήσεις παλαιάς μνήμης στο Excel.  
* **Validate the pivot**: μετά την αποθήκευση, ανοίξτε το αρχείο προγραμματιστικά και καλέστε `pivotTable.validate()` για να βεβαιωθείτε ότι δεν υπάρχουν σπασμένες αναφορές.  
* **Version compatibility**: ο κώδικας λειτουργεί με αρχεία Excel 2007‑2024 (`.xlsx`, `.xlsm`). Για παλαιότερα αρχεία `.xls`, ορίστε `LoadOptions.setLoadFormat(LoadFormat.XLS)`.

## Πλήρης λίστα κώδικα (έτοιμο για μεταγλώττιση)

```java
import com.aspose.cells.*;

public class DuplicatePivot {
    public static void main(String[] args) {
        // --------------------------------------------------------------------
        // 1️⃣ Load source workbook
        // --------------------------------------------------------------------
        String srcPath = "YOUR_DIRECTORY/Source.xlsx";
        Workbook srcWb;
        try {
            srcWb = new Workbook(srcPath);
        } catch (Exception e) {
            System.err.println("Failed to load source workbook: " + e.getMessage());
            return;
        }

        // --------------------------------------------------------------------
        // 2️⃣ Define the range that contains the pivot table
        // --------------------------------------------------------------------
        Worksheet srcSheet = srcWb.getWorksheets().get(0);
        String pivotRangeAddress = "A1:G20"; // adjust to your pivot's actual area
        Range srcRange = srcSheet.getCells().createRange(pivotRangeAddress);

        // --------------------------------------------------------------------
        // 3️⃣ Copy the range (including the pivot) to a new workbook
        // --------------------------------------------------------------------
        Workbook destWb = new Workbook(); // blank workbook
        Worksheet destSheet = destWb.getWorksheets().get(0);
        try {
            destSheet.getCells().copyRange(srcRange, "A1");
        } catch (Exception e) {
            System.err.println("Failed to copy range: " + e.getMessage());
            return;
        }

        // --------------------------------------------------------------------
        // 4️⃣ Refresh the duplicated pivot (ensures correct values)
        // --------------------------------------------------------------------
        for (int i = 0; i < destSheet.getPivotTables().getCount(); i++) {
            destSheet


## Τι πρέπει να μάθετε στη συνέχεια;

Οι παρακάτω οδηγίες καλύπτουν στενά συναφή θέματα που βασίζονται στις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικά παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να αντιγράψετε πίνακα Pivot σε Java – Πλήρης οδηγός Aspose.Cells](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-complete-aspose-cells-guide/)
- [Πώς να δημιουργήσετε πίνακες Pivot στο Excel χρησιμοποιώντας Aspose.Cells for Java: Ένας ολοκληρωμένος οδηγός](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [Πώς να ενημερώσετε την πηγή πίνακα Pivot στο Excel με Aspose.Cells for Java: Ένας ολοκληρωμένος οδηγός](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}