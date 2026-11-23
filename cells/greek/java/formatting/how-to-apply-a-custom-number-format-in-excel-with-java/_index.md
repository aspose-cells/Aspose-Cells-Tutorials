---
category: general
date: 2026-11-22
description: Μάθετε πώς να χρησιμοποιείτε προσαρμοσμένη μορφή αριθμού για να μορφοποιήσετε
  μια στήλη ως νόμισμα στο Excel χρησιμοποιώντας Java. Ορίστε τη μορφή αριθμού του
  Excel γρήγορα με ένα απλό στυλ.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- custom number format
- format column as currency
- set excel number format
- set currency format
- style first column
language: el
lastmod: 2026-11-22
og_description: Εφαρμόστε προσαρμοσμένη μορφή αριθμού στο Excel με Java. Αυτό το σεμινάριο
  δείχνει πώς να ορίσετε τη μορφή αριθμού στο Excel και να μορφοποιήσετε την πρώτη
  στήλη ως νόμισμα.
og_image_alt: Java code snippet that applies a custom number format to an Excel column
og_title: Εφαρμόστε προσαρμοσμένη μορφή αριθμού στο Excel με Java – οδηγός βήμα‑προς‑βήμα
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Learn how to use a custom number format to format a column as currency
    in Excel using Java. Set Excel number format quickly with a simple style.
  headline: How to apply a custom number format in Excel with Java
  type: TechArticle
tags:
- Java
- Excel
- Apache POI
- Spreadsheet Automation
title: Πώς να εφαρμόσετε προσαρμοσμένη μορφή αριθμού στο Excel με τη Java
url: /el/java/formatting/how-to-apply-a-custom-number-format-in-excel-with-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να εφαρμόσετε προσαρμοσμένη μορφή αριθμού στο Excel με Java

Αν χρειάζεται να **προσαρμόσετε τη μορφή αριθμού** μιας στήλης σε ένα φύλλο εργασίας του Excel, αυτός ο οδηγός σας δείχνει ακριβώς πώς να το κάνετε χρησιμοποιώντας Java. Είτε δημιουργείτε οικονομικές αναφορές είτε εξάγετε λογιστικά δεδομένα, η μορφοποίηση της πρώτης στήλης ως νόμισμα κάνει το αποτέλεσμα άμεσα αναγνώσιμο.

Στο παρακάτω παράδειγμα θα **μορφοποιήσουμε τη στήλη ως νόμισμα**, θα εφαρμόσουμε το στυλ στην πρώτη στήλη και στη συνέχεια θα εισάγουμε ένα `DataTable` στο φύλλο εργασίας. Η ίδια προσέγγιση λειτουργεί για οποιαδήποτε αριθμητική μορφή θέλετε να εμφανίσετε.

## Τι θα μάθετε

* Πώς να δημιουργήσετε μια **custom number format** με το αντικείμενο `Style` του Apache POI.  
* Πώς να **set Excel number format** για μια συγκεκριμένη στήλη, συμπεριλαμβανομένης της περίπτωσης **set currency format**.  
* Πώς να **style first column** κατά την εισαγωγή ενός `DataTable`.  
* Πώς να αποθηκεύσετε το βιβλίο εργασίας και να επαληθεύσετε ότι η μορφοποίηση εμφανίζεται σωστά.

### Προαπαιτούμενα

* Java 17 ή νεότερη.  
* Apache POI 5.x (η βιβλιοθήκη που παρέχει `Workbook`, `Worksheet` και `Style`).  
* Μια υλοποίηση `DataTable` που μπορεί να επαναληφθεί όπως αυτή στο δείγμα κώδικα.  
* Βασική εξοικείωση με τις έννοιες της Java και του Excel.

---

## Βήμα 1: Ρύθμιση του έργου και εισαγωγή των δεδομένων

Πρώτα, προσθέστε το Apache POI στο έργο σας. Αν χρησιμοποιείτε Maven, συμπεριλάβετε την ακόλουθη εξάρτηση:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>org.apache.poi</groupId>
    <artifactId>poi-ooxml</artifactId>
    <version>5.2.3</version>
</dependency>
```

Στη συνέχεια, αποκτήστε τα δεδομένα πηγής ως `DataTable`. Σε ένα πραγματικό σενάριο αυτό μπορεί να προέρχεται από ερώτημα βάσης δεδομένων, αρχείο CSV ή απόκριση API.

```java
// Step 1: Obtain the source data as a DataTable
DataTable dataTable = getData();   // replace with your own data‑fetching logic
```

> **Pro tip:** Βεβαιωθείτε ότι οι στήλες του `DataTable` έχουν τους σωστούς τύπους Java (`Integer`, `Double` κ.λπ.) επειδή η μορφή αριθμού επηρεάζει μόνο τα αριθμητικά κελιά.

---

## Βήμα 2: Δημιουργία **custom number format** για την πρώτη στήλη

Μια **custom number format** λέει στο Excel πώς να εμφανίζει αριθμητικές τιμές. Για να εμφανίσετε τιμές ως νόμισμα χρησιμοποιούμε την ενσωματωμένη μορφή `CURRENCY`, αλλά μπορείτε επίσης να ορίσετε μοτίβα όπως `"$#,##0.00"`.

```java
// Step 2: Prepare a Style array – one entry per column in the DataTable
Style[] columnStyles = new Style[dataTable.getColumns().size()];

// Step 3: Create a style for the first column and set it to display values as currency
// wb – existing Workbook instance (e.g., XSSFWorkbook for .xlsx files)
Workbook wb = new XSSFWorkbook();
columnStyles[0] = wb.createCellStyle();               // style first column
columnStyles[0].setDataFormat(
        wb.createDataFormat().getFormat(Style.CustomNumberFormat.CURRENCY));
```

**Γιατί λειτουργεί αυτό:**  
* `createCellStyle()` επιστρέφει ένα επαναχρησιμοποιήσιμο αντικείμενο στυλ.  
* `setDataFormat()` συνδέει το **set currency format** με το στυλ, το οποίο το Excel εφαρμόζει σε κάθε κελί που χρησιμοποιεί αυτό το στυλ.  
* Αποθηκεύοντας το στυλ στο `columnStyles[0]` διασφαλίζουμε ότι μόνο η πρώτη στήλη λαμβάνει τη μορφοποίηση νομίσματος.

---

## Βήμα 3: Εισαγωγή του `DataTable` εφαρμόζοντας τα στυλ στήλης

Τώρα εισάγουμε τα δεδομένα στο φύλλο εργασίας. Η μέθοδος `importDataTable` δέχεται τον πίνακα στυλ, επιτρέποντάς μας να **style first column** και να αφήσουμε τις υπόλοιπες στήλες με προεπιλεγμένη μορφοποίηση.

```java
// Step 4: Import the DataTable into the worksheet, applying the column styles
// ws – existing Worksheet instance
Worksheet ws = wb.createSheet("Report");

// true  → import column headers
// 0,0   → start at cell A1
ws.getCells().importDataTable(dataTable, true, 0, 0, columnStyles);
```

Η παραπάνω κλήση **sets Excel number format** μόνο για την πρώτη στήλη. Όλες οι άλλες στήλες κληρονομούν το προεπιλεγμένο στυλ του βιβλίου εργασίας, κάτι που κρατά τον κώδικα απλό και αποδοτικό.

---

## Βήμα 4: Αποθήκευση του βιβλίου εργασίας και επαλήθευση του αποτελέσματος

Τέλος, γράψτε το βιβλίο εργασίας σε αρχείο και ανοίξτε το στο Excel για να επιβεβαιώσετε ότι η πρώτη στήλη εμφανίζει σύμβολα νομίσματος.

```java
// Step 5: Save the workbook to disk
try (FileOutputStream fileOut = new FileOutputStream("FormattedReport.xlsx")) {
    wb.write(fileOut);
}
System.out.println("Workbook saved as FormattedReport.xlsx");
```

**Αναμενόμενο αποτέλεσμα:**  
Όταν ανοίξετε το *FormattedReport.xlsx*, οι τιμές στη στήλη A εμφανίζονται με το κατάλληλο σύμβολο νομίσματος (π.χ., `$1,234.00`). Όλες οι άλλες στήλες διατηρούν την αρχική αριθμητική τους αναπαράσταση.

---

## Συνηθισμένες παραλλαγές και ειδικές περιπτώσεις

| Κατάσταση | Προσαρμογή |
|-----------|------------|
| **Διαφορετικό νόμισμα** (π.χ., Ευρώ) | Αντικαταστήστε το `Style.CustomNumberFormat.CURRENCY` με ένα προσαρμοσμένο μοτίβο: <br>`wb.createDataFormat().getFormat("\"€\"#,##0.00")` |
| **Περισσότερες από μία στυλιζαρισμένες στήλες** | Συμπληρώστε επιπλέον καταχωρήσεις στο `columnStyles[]` με τα δικά τους αντικείμενα `CellStyle`. |
| **Μεγάλα σύνολα δεδομένων** | Χρησιμοποιήστε το `importDataTable` σε παρτίδες ή ροή γραμμών για να αποφύγετε `OutOfMemoryError`. |
| **Διαχωριστές ειδικές για τοπική ρύθμιση** | Χρησιμοποιήστε `java.text.NumberFormat` για να δημιουργήσετε μοτίβο προσαρμοσμένο στην τοπική ρύθμιση και περάστε το στο `setDataFormat`. |

> **Watch out for:** Η επαναχρησιμοποίηση ενός μόνο αντικειμένου `CellStyle` σε πολλές στήλες μπορεί να προκαλέσει απρόσμενη μορφοποίηση, επειδή το Excel περιορίζει τον αριθμό των διαφορετικών στυλ ανά βιβλίο εργασίας. Δημιουργήστε ξεχωριστό στυλ για κάθε μοναδική μορφή που χρειάζεστε.

---

## Πλήρες παραδειγματικό πρόγραμμα

Παρακάτω υπάρχει ένα αυτόνομο πρόγραμμα που δείχνει ολόκληρη τη ροή, από τη δημιουργία δεδομένων μέχρι την αποθήκευση του μορφοποιημένου βιβλίου εργασίας.

```java
import java.io.FileOutputStream;
import java.util.ArrayList;
import java.util.List;

import org.apache.poi.ss.usermodel.*;
import org.apache.poi.xssf.usermodel.XSSFWorkbook;

/* Mock DataTable implementation for demonstration purposes */
class DataTable {
    private final List<String> columns = List.of("Amount", "Description");
    private final List<Object[]> rows = new ArrayList<>();

    public DataTable() {
        rows.add(new Object[]{1234.5, "Consulting"});
        rows.add(new Object[]{5678.9, "Licensing"});
    }

    public List<String> getColumns() { return columns; }
    public List<Object[]> getRows() { return rows; }
}

/* Helper that mimics the importDataTable method used in the original snippet */
class WorksheetHelper {
    private final Sheet sheet;
    private final Workbook wb;

    public WorksheetHelper(Workbook wb, Sheet sheet) {
        this.wb = wb;
        this.sheet = sheet;
    }

    public void importDataTable(DataTable dt, boolean includeHeaders,
                                int startRow, int startCol, Style[] styles) {
        int rowIdx = startRow;
        if (includeHeaders) {
            Row header = sheet.createRow(rowIdx++);
            for (int c = 0; c < dt.getColumns().size(); c++) {
                Cell cell = header.createCell(startCol + c);
                cell.setCellValue(dt.getColumns().get(c));
            }
        }
        for (Object[] rowData : dt.getRows()) {
            Row row = sheet.createRow(rowIdx++);
            for (int c = 0; c < rowData.length; c++) {
                Cell cell = row.createCell(startCol + c);
                Object value = rowData[c];
                if (value instanceof Number) {
                    cell.setCellValue(((Number) value).doubleValue());
                } else {
                    cell.setCellValue(value.toString());
                }
                // Apply custom style if provided
                if (styles != null && c < styles.length && styles[c] != null) {
                    cell.setCellStyle((CellStyle) styles[c]);
                }
            }
        }
    }
}

/* Main class that puts everything together */
public class CustomNumberFormatDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Obtain the source data
        DataTable dataTable = new DataTable();

        // 2️⃣ Create a workbook and a sheet
        Workbook wb = new XSSFWorkbook();
        Sheet ws = wb.createSheet("Report");

        // 3️⃣ Prepare a style array – one entry per column
        Style[] columnStyles = new Style[dataTable.getColumns().size()];

        // 4️⃣ Create a style for the first column (currency)
        CellStyle currencyStyle = wb.createCellStyle();
        DataFormat fmt = wb.createDataFormat();
        currencyStyle.setDataFormat(fmt.getFormat("$#,##0.00"));
        columnStyles[0] = currencyStyle;   // style first column

        // 5️⃣ Import the DataTable, applying the column styles
        WorksheetHelper helper = new WorksheetHelper(wb, ws);
        helper.importDataTable(dataTable, true, 0, 0, columnStyles);

        // 6️⃣ Save the workbook
        try (FileOutputStream out = new FileOutputStream("FormattedReport.xlsx")) {
            wb.write(out);
        }
        System.out.println("Workbook written to FormattedReport.xlsx");
    }
}
```

Η εκτέλεση του προγράμματος δημιουργεί το **FormattedReport.xlsx** όπου η στήλη A (η στήλη “Amount”) εμφανίζεται με μια **custom number format** που δείχνει το σύμβολο δολαρίου και δύο δεκαδικά ψηφία.

---

## Συμπέρασμα

Τώρα ξέρετε πώς να **custom number format** ένα φύλλο Excel από τη Java, **format column as currency**, και **style first column** κατά την εισαγωγή δεδομένων. Δημιουργώντας ένα επαναχρησιμοποιήσιμο `CellStyle` και περνώντας το στη `importDataTable`, μπορείτε να **set Excel number format** για οποιαδήποτε στήλη χωρίς να χρειάζεται βρόχος σε κάθε κελί.

Επόμενα, δοκιμάστε:

* Χρήση του `setDataFormat` με μοτίβα προσαρμοσμένα σε τοπική ρύθμιση για **set currency format**

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικά παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε πρόσθετα χαρακτηριστικά του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Set Number Format Excel in Java – Complete Guide](/cells/english/java/formatting/set-number-format-excel-in-java-complete-guide/)
- [Apply Number Format Excel in Java – Complete Aspose.Cells Guide](/cells/english/java/formatting/apply-number-format-excel-in-java-complete-aspose-cells-guid/)
- [How to create excel workbook with currency format and bold font in Java](/cells/english/java/formatting/how-to-create-excel-workbook-with-currency-format-and-bold-f/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}