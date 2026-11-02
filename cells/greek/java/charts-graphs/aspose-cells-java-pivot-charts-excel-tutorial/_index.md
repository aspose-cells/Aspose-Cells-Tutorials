---
date: '2026-07-07'
description: Μάθετε το παράδειγμα γραφήματος Aspose Cells για τη δημιουργία δυναμικών
  pivot charts στο Excel χρησιμοποιώντας Java. Ακολουθήστε step‑by‑step οδηγίες για
  απρόσκοπτη data analysis.
keywords:
- aspose cells chart example
- how to create pivot chart
- dynamic pivot chart excel
- export pivot chart excel
- add pivot chart workbook
og_description: Μάθετε το παράδειγμα γραφήματος Aspose Cells για τη δημιουργία δυναμικών
  pivot charts στο Excel χρησιμοποιώντας Java. Ακολουθήστε step‑by‑step οδηγίες για
  απρόσκοπτη data analysis.
og_title: 'Παράδειγμα γραφήματος Aspose Cells: Κατάκτηση των Pivot Charts σε Java'
schemas:
- author: Aspose
  dateModified: '2026-07-07'
  description: Learn the Aspose Cells chart example to create dynamic pivot charts
    in Excel using Java. Follow step‑by‑step instructions for seamless data analysis.
  headline: 'Aspose Cells Chart Example: Mastering Pivot Charts in Java'
  type: TechArticle
- description: Learn the Aspose Cells chart example to create dynamic pivot charts
    in Excel using Java. Follow step‑by‑step instructions for seamless data analysis.
  name: 'Aspose Cells Chart Example: Mastering Pivot Charts in Java'
  steps:
  - name: Load the Source Workbook
    text: The `Workbook` class is Aspose.Cells' top‑level object that represents a
      single Excel file in memory.
  - name: Add a Worksheet for the Pivot Chart
    text: Create a dedicated chart sheet to keep the visual separate from raw data.
  - name: Insert a Pivot Table
    text: First, define the data range for the pivot table, then add it to the chart
      sheet. The `PivotTable` class represents a pivot table in a worksheet and provides
      methods to define its data source, layout, and calculations.
  - name: Create and Configure the Pivot Chart
    text: The `Chart` class represents any Excel chart. Here we create a column chart
      linked to the pivot table.
  - name: Export the Workbook
    text: Save the workbook with the new pivot chart to an `.xlsx` file, or directly
      to PDF if you need a static report.
  type: HowTo
- questions:
  - answer: Yes, call `chart.toImage("chart.png", ImageFormat.PNG)` after configuring
      the chart.
    question: Can I export a pivot chart directly to an image file?
  - answer: The library can preserve existing VBA macros, but it does not create or
      modify them programmatically.
    question: Does Aspose.Cells support Excel macros in pivot charts?
  - answer: Absolutely—invoke `pivotTable.refreshData()` and then `chart.refresh()`
      to reflect the latest values.
    question: Is it possible to update the pivot chart after changing the source data?
  - answer: Over 40 types, including column, line, area, pie, radar, and stacked bar,
      all fully supported for pivot data.
    question: Which chart types are available for pivot charts?
  - answer: Yes, a purchased license removes evaluation limits and enables full feature
      set.
    question: Do I need a license to use the Maven/Gradle setup in production?
  type: FAQPage
title: 'Παράδειγμα γραφήματος Aspose Cells: Κατάκτηση των Pivot Charts σε Java'
url: /el/java/charts-graphs/aspose-cells-java-pivot-charts-excel-tutorial/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Παράδειγμα Διαγράμματος Aspose Cells: Κατάκτηση Πίνακων Pivot σε Java

Στον σημερινό κόσμο που βασίζεται στα δεδομένα, η μετατροπή των ακατέργαστων αριθμών σε σαφή οπτικά ευρήματα είναι απαραίτητη. Αυτό το tutorial σας δείχνει το **aspose cells chart example** που χρειάζεστε για να δημιουργήσετε δυναμικά pivot charts στο Excel με Java. Στο τέλος αυτού του οδηγού θα μπορείτε να φορτώσετε ένα workbook, να προσθέσετε ένα αφιερωμένο φύλλο διαγράμματος, να συνδέσετε έναν πίνακα pivot και να εξάγετε το αποτέλεσμα—όλα με λίγες μόνο γραμμές κώδικα.

## Γρήγορες Απαντήσεις
- **Ποια είναι η κύρια κλάση για εργασία με αρχεία Excel;** `Workbook` αντιπροσωπεύει ένα πλήρες αρχείο Excel στη μνήμη.  
- **Ποιο Maven artifact προσθέτει το Aspose.Cells σε ένα έργο;** `com.aspose:aspose-cells` (version 25.3 or newer).  
- **Μπορώ να δημιουργήσω ένα pivot chart χωρίς άδεια;** Ναι, μια δωρεάν δοκιμή λειτουργεί για ανάπτυξη, αλλά μια άδεια αφαιρεί τα όρια αξιολόγησης.  
- **Πόσους τύπους διαγραμμάτων υποστηρίζει το Aspose.Cells;** Πάνω από 40 τύπους διαγραμμάτων, συμπεριλαμβανομένων των γραμμικών, στηλών, πίτας και ραδάρ.  
- **Ποιος είναι ο πιο γρήγορος τρόπος για εξαγωγή ενός pivot chart σε PDF;** Καλέστε `chart.toPdf("output.pdf")` μετά τη διαμόρφωση της πηγής δεδομένων του διαγράμματος.

## Τι είναι ένα Pivot Chart στο Excel;
Ένα **pivot chart** είναι μια διαδραστική οπτική αναπαράσταση ενός pivot table, που επιτρέπει στους χρήστες να εξερευνούν τα συγκεντρωμένα δεδομένα δυναμικά. Χρησιμοποιώντας το Aspose.Cells, μπορείτε να δημιουργήσετε αυτά τα διαγράμματα προγραμματιστικά χωρίς να ανοίξετε το Excel. Ενημερώνεται αυτόματα όταν αλλάζει το υποκείμενο pivot table, υποστηρίζει φιλτράρισμα και μπορεί να προσαρμοστεί με διάφορους τύπους διαγραμμάτων, τίτλους και υπομνήματα, καθιστώντας το ένα ισχυρό εργαλείο ανάλυσης δεδομένων.

## Γιατί να χρησιμοποιήσετε το Aspose.Cells για Java για τη δημιουργία pivot charts;
Το Aspose.Cells επεξεργάζεται **πάνω από 50 μορφές εισόδου και εξόδου** και μπορεί να διαχειριστεί workbooks με **εκατοντάδες φύλλα εργασίας** ενώ διατηρεί τη χρήση μνήμης κάτω από 200 MB. Το API του δημιουργεί, τροποποιεί και αποδίδει διαγράμματα σε **κάτω από 2 δευτερόλεπτα** για τυπικά σύνολα δεδομένων 10 KB, καθιστώντας το ιδανικό για αναφορές από τον διακομιστή.

## Προαπαιτούμενα

- **Aspose.Cells for Java** έκδοση 25.3 ή νεότερη.  
- Σύστημα κατασκευής Maven ή Gradle.  
- JDK 8 ή νεότερο και ένα IDE όπως IntelliJ IDEA, Eclipse ή NetBeans.  
- Βασικές γνώσεις Java· η εξοικείωση με το Excel είναι χρήσιμη αλλά όχι απαραίτητη.

### Απαιτούμενες Βιβλιοθήκες και Εξαρτήσεις
- **Maven:** προσθέστε την εξάρτηση Aspose.Cells (δείτε την ενότητα *aspose cells maven setup* παρακάτω).  
- **Gradle:** συμπεριλάβετε το ίδιο artifact στο `build.gradle`.

### Βήματα Απόκτησης Άδειας
- **Free Trial:** ξεκινήστε με μια δωρεάν δοκιμή για να εξερευνήσετε το aspose cells chart example.  
- **Temporary License:** αποκτήστε ένα προσωρινό κλειδί για εκτεταμένη δοκιμή.  
- **Purchase:** αγοράστε πλήρη άδεια από [Aspose’s official website](https://purchase.aspose.com/buy).

## Πώς να Ρυθμίσετε το Aspose.Cells για Java

### Εξάρτηση Maven (aspose cells maven setup)

Προσθέστε το παρακάτω απόσπασμα στο `pom.xml` σας:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
    <classifier>jdk17</classifier>
</dependency>
```

### Εξάρτηση Gradle

```gradle
implementation 'com.aspose:aspose-cells:25.3'
```

### Βασική Αρχικοποίηση
Αφού προσθέσετε την εξάρτηση, αρχικοποιήστε τη βιβλιοθήκη όπως φαίνεται παρακάτω:

```java
// Initialize license (optional for trial)
License license = new License();
license.setLicense("Aspose.Cells.lic");

// Create a Workbook object – this loads or creates an Excel file.
Workbook workbook = new Workbook();
```

## Πώς να Δημιουργήσετε ένα Pivot Chart Χρησιμοποιώντας το Aspose.Cells για Java;

Φορτώστε τα δεδομένα πηγής σας, δημιουργήστε έναν πίνακα pivot και συνδέστε τον με ένα διάγραμμα—όλα σε λίγα απλά βήματα. Η διαδικασία περιλαμβάνει τη φόρτωση ενός workbook που περιέχει τα δεδομένα πηγής, τη δημιουργία ενός pivot table για σύνοψη των δεδομένων, την προσθήκη ενός αφιερωμένου φύλλου διαγράμματος, τη σύνδεση του pivot table με ένα διάγραμμα, την προσαρμογή της εμφάνισης του διαγράμματος και, τέλος, την αποθήκευση του workbook στην επιθυμητή μορφή.

### Βήμα 1: Φόρτωση του Workbook Πηγής
Η κλάση `Workbook` είναι το αντικείμενο υψηλότερου επιπέδου του Aspose.Cells που αντιπροσωπεύει ένα μόνο αρχείο Excel στη μνήμη.

```java
Workbook workbook = new Workbook("data.xlsx");
```

### Βήμα 2: Προσθήκη Φύλλου Εργασίας για το Pivot Chart
Δημιουργήστε ένα αφιερωμένο φύλλο διαγράμματος για να κρατήσετε το οπτικό ξεχωριστό από τα ακατέργαστα δεδομένα.

```java
int chartSheetIndex = workbook.getWorksheets().addChart("PivotChartSheet");
Worksheet chartSheet = workbook.getWorksheets().get(chartSheetIndex);
```

### Βήμα 3: Εισαγωγή Pivot Table
Πρώτα, ορίστε την περιοχή δεδομένων για το pivot table, στη συνέχεια προσθέστε το στο φύλλο διαγράμματος.

Η κλάση `PivotTable` αντιπροσωπεύει ένα pivot table σε ένα φύλλο εργασίας και παρέχει μεθόδους για τον ορισμό της πηγής δεδομένων, της διάταξης και των υπολογισμών του.

```java
int pivotTableIndex = chartSheet.getPivotTables().add("A1:D100", "PivotTable1", 0, 0);
PivotTable pivotTable = chartSheet.getPivotTables().get(pivotTableIndex);
pivotTable.addFieldToArea(PivotFieldType.ROW, 0);   // Category
pivotTable.addFieldToArea(PivotFieldType.DATA, 1);  // Values
```

### Βήμα 4: Δημιουργία και Διαμόρφωση του Pivot Chart
Η κλάση `Chart` αντιπροσωπεύει οποιοδήποτε διάγραμμα Excel. Εδώ δημιουργούμε ένα διάγραμμα στήλης συνδεδεμένο με το pivot table.

```java
int chartIndex = chartSheet.getCharts().add(ChartType.COLUMN, 5, 0, 25, 10);
Chart chart = chartSheet.getCharts().get(chartIndex);
chart.getNSeries().add("=PivotTable1!$B$2:$B$5", true);
chart.setTitle("Sales by Region");
```

### Βήμα 5: Εξαγωγή του Workbook
Αποθηκεύστε το workbook με το νέο pivot chart σε αρχείο `.xlsx`, ή απευθείας σε PDF αν χρειάζεστε μια στατική αναφορά.

```java
workbook.save("PivotChartResult.xlsx", SaveFormat.XLSX);
// Optional PDF export
workbook.save("PivotChartResult.pdf", SaveFormat.PDF);
```

## Πρακτικές Εφαρμογές Δυναμικών Pivot Charts

- **Financial Reporting:** Αυτόματη δημιουργία τριμηνιαίων ταμπλό που ενημερώνονται καθώς εισάγονται νέα δεδομένα.  
- **Sales Analysis:** Οπτικοποίηση των περιφερειακών τάσεων πωλήσεων με μία κλήση API.  
- **Inventory Management:** Παρακολούθηση επιπέδων αποθέματος και σημείων επαναπαραγγελίας σε πραγματικό χρόνο.  
- **Customer Insights:** Συνδυάστε δημογραφικά δεδομένα με το ιστορικό αγορών για διαδραστικά διαγράμματα.  
- **Project Management:** Εμφανίστε την κατανομή πόρων και τις αποκλίσεις χρονοδιαγράμματος χρησιμοποιώντας pivot charts.

## Συμβουλές Απόδοσης για Μεγάλα Σύνολα Δεδομένων

- **Memory Management:** Καλέστε `workbook.dispose()` μετά την αποθήκευση για να απελευθερώσετε τους εγγενείς πόρους.  
- **Batch Operations:** Χρησιμοποιήστε `CellsHelper.copyRange` για μετακίνηση μεγάλων μπλοκ δεδομένων αντί για βρόχους κελί‑με‑κελί.  
- **Lazy Loading:** Όταν επεξεργάζεστε αρχεία μεγαλύτερα από 100 MB, ενεργοποιήστε το `LoadOptions.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` για να διατηρήσετε τη χρήση μνήμης χαμηλή.

## Κοινά Προβλήματα και Λύσεις

| Πρόβλημα | Λύση |
|----------|------|
| **Pivot table δεν αντικατοπτρίζει νέα δεδομένα** | Ανανεώστε το pivot table με `pivotTable.refreshData()` πριν δημιουργήσετε το διάγραμμα. |
| **Το διάγραμμα εμφανίζεται κενό** | Βεβαιωθείτε ότι η περιοχή πηγής δεδομένων του διαγράμματος ταιριάζει με την περιοχή αποτελεσμάτων του pivot table. |
| **Σφάλματα έλλειψης μνήμης σε τεράστια αρχεία** | Χρησιμοποιήστε `LoadOptions` με `MemorySetting.MEMORY_PREFERENCE` και κλείστε φύλλα εργασίας που δεν χρειάζεστε πλέον. |

## Συχνές Ερωτήσεις

**Q: Μπορώ να εξάγω ένα pivot chart απευθείας σε αρχείο εικόνας;**  
A: Ναι, καλέστε `chart.toImage("chart.png", ImageFormat.PNG)` μετά τη διαμόρφωση του διαγράμματος.

**Q: Υποστηρίζει το Aspose.Cells μακροεντολές Excel σε pivot charts;**  
A: Η βιβλιοθήκη μπορεί να διατηρήσει υπάρχουσες μακροεντολές VBA, αλλά δεν μπορεί να τις δημιουργήσει ή να τις τροποποιήσει προγραμματιστικά.

**Q: Είναι δυνατόν να ενημερώσετε το pivot chart μετά την αλλαγή των δεδομένων πηγής;**  
A: Απόλυτα—εκτελέστε `pivotTable.refreshData()` και στη συνέχεια `chart.refresh()` για να αντικατοπτριστούν οι τελευταίες τιμές.

**Q: Ποιοι τύποι διαγραμμάτων είναι διαθέσιμοι για pivot charts;**  
A: Πάνω από 40 τύποι, συμπεριλαμβανομένων των στηλών, γραμμών, περιοχών, πίτας, ραδάρ και στοίβαξης μπαρ, όλοι πλήρως υποστηριζόμενοι για δεδομένα pivot.

**Q: Χρειάζομαι άδεια για τη χρήση της ρύθμισης Maven/Gradle στην παραγωγή;**  
A: Ναι, μια αγορασμένη άδεια αφαιρεί τα όρια αξιολόγησης και ενεργοποιεί το πλήρες σύνολο λειτουργιών.

---

**Τελευταία Ενημέρωση:** 2026-07-07  
**Δοκιμή με:** Aspose.Cells 25.3 for Java  
**Συγγραφέας:** Aspose  

## Πόροι

- [Τεκμηρίωση Aspose.Cells](https://reference.aspose.com/cells/java/)
- [Λήψη Aspose.Cells για Java](https://releases.aspose.com/cells/java/)
- [Αγορά Άδειας](https://purchase.aspose.com/buy)
- [Δωρεάν Δοκιμή και Προσωρινές Άδειες](https://releases.aspose.com/cells/java/)
- [Φόρουμ Υποστήριξης Aspose](https://forum.aspose.com/c/cells/9)

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

```java
import com.aspose.cells.Workbook;

// Load an existing workbook
String dataDir = "YOUR_DATA_DIRECTORY";
Workbook workbook = new Workbook(dataDir + "/pivotTable_test.xls");
```

```java
   import com.aspose.cells.Workbook;
   ```

```java
   String dataDir = "YOUR_DATA_DIRECTORY";
   Workbook workbook = new Workbook(dataDir + "/pivotTable_test.xls");
   ```

```java
   import com.aspose.cells.SheetType;
   import com.aspose.cells.Worksheet;
   ```

```java
   int sheetIndex = workbook.getWorksheets().add(SheetType.CHART);
   Worksheet sheet3 = workbook.getWorksheets().get(sheetIndex);
   sheet3.setName("PivotChart");
   ```

```java
   import com.aspose.cells.Chart;
   import com.aspose.cells.ChartType;
   ```

```java
   int chartIndex = sheet3.getCharts().add(ChartType.COLUMN, 0, 5, 28, 16);
   Chart chart = sheet3.getCharts().get(chartIndex);
   ```

```java
   chart.setPivotSource("PivotTable!PivotTable1");
   chart.setHidePivotFieldButtons(false);
   ```

```java
   String outDir = "YOUR_OUTPUT_DIRECTORY";
   workbook.save(outDir + "/CPCBasedOnPTable_out.xls");
   ```

## Σχετικά Μαθήματα

- [Κατάκτηση Πίνακες Pivot στο Excel χρησιμοποιώντας Aspose.Cells για Java: Ένας Πλήρης Οδηγός για Ανάλυση Δεδομένων](/cells/java/data-analysis/excel-pivot-tables-aspose-cells-java-tutorial/)
- [Δημιουργία Workbook & Προσθήκη Διαγραμμάτων με Aspose.Cells για Java: Ένας Πλήρης Οδηγός](/cells/java/charts-graphs/create-workbook-add-charts-aspose-cells-java/)
- [Προσαρμογή Διαγραμμάτων Excel σε Java: Κατάκτηση Aspose.Cells για Απρόσκοπτη Οπτικοποίηση Δεδομένων](/cells/java/charts-graphs/excel-chart-customization-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}