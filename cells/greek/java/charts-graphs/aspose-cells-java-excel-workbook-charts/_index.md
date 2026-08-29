---
date: '2026-04-11'
description: Μάθετε αυτοματοποίηση Excel με Java χρησιμοποιώντας το Aspose.Cells.
  Αυτό το σεμινάριο δείχνει πώς να δημιουργήσετε ένα βιβλίο εργασίας Excel με Java,
  να γεμίσετε δεδομένα Excel με Java και να αποθηκεύσετε αρχείο Excel με Java με γραφήματα.
keywords:
- excel automation java
- create excel workbook java
- save excel file java
- populate excel data java
- aspose cells java
title: 'Αυτοματοποίηση Excel με Java: Δημιουργία βιβλίων εργασίας και γραφημάτων με
  Aspose'
url: /el/java/charts-graphs/aspose-cells-java-excel-workbook-charts/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Αυτοματοποίηση Excel με Java: Δημιουργία Βιβλίων Εργασίας & Διαγραμμάτων με Aspose

## Εισαγωγή

Η αυτοματοποίηση εργασιών Excel με Java μπορεί να εξοικονομήσει ώρες χειροκίνητης εργασίας, ειδικά όταν χρειάζεται να δημιουργήσετε αναφορές, πίνακες ελέγχου ή διαγράμματα βάσει δεδομένων σε πραγματικό χρόνο. **Excel automation java** με Aspose.Cells σας παρέχει ένα καθαρό, υψηλής απόδοσης API που διαχειρίζεται τα πάντα, από τη δημιουργία βιβλίου εργασίας έως την προηγμένη μορφοποίηση διαγραμμάτων. Σε αυτό το tutorial θα μάθετε πώς να ρυθμίσετε το Aspose.Cells, **create an Excel workbook java**, να το γεμίσετε με δεδομένα, να προσθέσετε ένα διάγραμμα, να εφαρμόσετε 3‑Δ μορφοποίηση και, τέλος, **save the Excel file java**.

### Γρήγορες Απαντήσεις
- **Ποια βιβλιοθήκη απλοποιεί την αυτοματοποίηση Excel σε Java;** Aspose.Cells for Java.  
- **Μπορώ να προσθέσω 3‑Δ διαγράμματα προγραμματιστικά;** Yes – the API supports 3‑D formatting and lighting effects.  
- **Χρειάζομαι άδεια για ανάπτυξη;** A free trial license is available; a commercial license is required for production.  
- **Ποια εργαλεία κατασκευής Java υποστηρίζονται;** Maven and Gradle are both fully supported.  
- **Ποια μορφές αρχείων μπορώ να εξάγω;** XLS, XLSX, CSV, PDF and many more.

## Τι είναι η αυτοματοποίηση Excel java;

Η αυτοματοποίηση Excel java αναφέρεται στη διαδικασία δημιουργίας, τροποποίησης και αποθήκευσης βιβλίων εργασίας Excel προγραμματιστικά χρησιμοποιώντας κώδικα Java. Απομακρύνει την χειροκίνητη επεξεργασία υπολογιστικών φύλλων, εξασφαλίζει συνέπεια και επιτρέπει ενσωμάτωση με άλλα συστήματα όπως βάσεις δεδομένων ή web services.

## Γιατί να χρησιμοποιήσετε Aspose.Cells για Java;

- **Πλούσιο σύνολο λειτουργιών** – from simple cell values to complex charts, pivot tables, and conditional formatting.  
- **Χωρίς εξάρτηση από Microsoft Office** – works on any server‑side environment.  
- **Υψηλή απόδοση** – optimized for large data sets and multi‑threaded scenarios.  
- **Ευρεία υποστήριξη μορφών** – read/write XLS, XLSX, ODS, CSV, PDF, HTML, and more.

## Προαπαιτούμενα

- **Java Development Kit (JDK) 8+**  
- **Maven or Gradle** for dependency management  
- **Aspose.Cells for Java 25.3 or later** (trial or licensed)  

## Ρύθμιση Aspose.Cells για Java

Προσθέστε τη βιβλιοθήκη στο έργο σας χρησιμοποιώντας μία από τις παρακάτω ρυθμίσεις.

### Maven
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### Gradle
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

#### Απόκτηση Άδειας

Ζητήστε μια δωρεάν άδεια δοκιμής από την ιστοσελίδα Aspose ή αγοράστε πλήρη άδεια για παραγωγική χρήση. Τοποθετήστε το αρχείο άδειας στο έργο σας και φορτώστε το κατά το χρόνο εκτέλεσης.

## Βασική Αρχικοποίηση και Ρύθμιση

Μόλις επιλυθεί η εξάρτηση, μπορείτε να αρχίσετε τον κώδικα.

```java
import com.aspose.cells.Workbook;

public class ExcelDemo {
    public static void main(String[] args) throws Exception {
        String dataDir = "YOUR_DATA_DIRECTORY";
        String outDir = "YOUR_OUTPUT_DIRECTORY";

        // Initialize a new Workbook object
        Workbook book = new Workbook();
        System.out.println("Workbook initialized successfully.");
    }
}
```

## Οδηγός Βήμα‑βήμα

### Βήμα 1: Πώς να δημιουργήσετε excel workbook java

```java
import com.aspose.cells.Workbook;
// Initialize a new Workbook object
Workbook book = new Workbook();
```

### Βήμα 2: Προσθήκη φύλλων εργασίας (συμπεριλαμβανομένου φύλλου διαγράμματος)

```java
import com.aspose.cells.Worksheet;
Worksheet dataSheet = book.getWorksheets().add("DataSheet");
Worksheet chartSheet = book.getWorksheets().add("MyChart");
System.out.println("Worksheets added successfully.");
```

### Βήμα 3: Πώς να γεμίσετε δεδομένα excel java

```java
import com.aspose.cells.Cells;
Cells cells = dataSheet.getCells();
cells.get("B1").putValue(1);
cells.get("B2").putValue(2);
cells.get("B3").putValue(3);
cells.get("A1").putValue("A");
cells.get("A2").putValue("B");
cells.get("A3").putValue("C");
System.out.println("Data populated successfully.");
```

### Βήμα 4: Προσθήκη στηλογράμματος στο βιβλίο εργασίας

```java
import com.aspose.cells.Chart;
import com.aspose.cells.ChartCollection;
import com.aspose.cells.ChartType;
ChartCollection charts = chartSheet.getCharts();
charts.add(ChartType.COLUMN, 5, 0, 25, 15);
Chart chart = book.getWorksheets().get(2).getCharts().get(0);
System.out.println("Chart added successfully.");
```

### Βήμα 5: Εφαρμογή χρωματικής μορφοποίησης στην περιοχή διαγράμματος

```java
import com.aspose.cells.Color;
chart.getPlotArea().getArea().setBackgroundColor(Color.getWhite());
chart.getChartArea().getArea().setBackgroundColor(Color.getWhite());
chart.getPlotArea().getArea().setForegroundColor(Color.getWhite());
chart.getChartArea().getArea().setForegroundColor(Color.getWhite());
System.out.println("Color formatting applied successfully.");
```

### Βήμα 6: Διαμόρφωση υπομνήματος και σειράς δεδομένων

```java
import com.aspose.cells.Series;
chart.setShowLegend(false);
chart.getNSeries().add("DataSheet!B1:B3", true);
chart.getNSeries().setCategoryData("DataSheet!A1:A3");
Series ser = chart.getNSeries().get(0);
System.out.println("Chart series configured successfully.");
```

### Βήμα 7: Εφαρμογή 3Δ μορφοποίησης στη σειρά

```java
import com.aspose.cells.Bevel;
import com.aspose.cells.BevelPresetType;
import com.aspose.cells.Format3D;
import com.aspose.cells.LightRigType;
import com.aspose.cells.PresetMaterialType;
import com.aspose.cells.ShapePropertyCollection;
ShapePropertyCollection spPr = ser.getShapeProperties();
Format3D fmt3d = spPr.getFormat3D();

Bevel bevel = fmt3d.getTopBevel();
bevel.setType(BevelPresetType.CIRCLE);
bevel.setHeight(5);
bevel.setWidth(9);
fmt3d.setSurfaceMaterialType(PresetMaterialType.WARM_MATTE);
fmt3d.setSurfaceLightingType(LightRigType.THREE_POINT);
fmt3d.setLightingAngle(20);
System.out.println("3D formatting applied successfully.");
```

### Βήμα 8: Ορισμός χρωμάτων σειράς για καλύτερη οπτική διάκριση

```java
ser.getArea().setBackgroundColor(Color.getMaroon());
ser.getArea().setForegroundColor(Color.getMaroon());
ser.getBorder().setColor(Color.getMaroon());
System.out.println("Series color formatting applied successfully.");
```

### Βήμα 9: Πώς να αποθηκεύσετε αρχείο excel java

```java
book.save(outDir + "A3DFormat_out.xls");
System.out.println("Workbook saved successfully.");
```

## Πρακτικές Εφαρμογές

- **Οικονομική Αναφορά** – Generate quarterly statements with dynamic charts.  
- **Πίνακες Ελέγχου Ανάλυσης Δεδομένων** – Build interactive dashboards that refresh automatically.  
- **Διαχείριση Αποθεμάτων** – Export stock levels and trends to Excel for stakeholder review.  
- **Σχεδιασμός Έργου** – Create Gantt‑style charts directly from Java‑based scheduling systems.

## Συμβουλές Απόδοσης για Excel Automation Java

- **Επαναχρησιμοποίηση Αντικειμένων Workbook** when processing multiple sheets to reduce memory churn.  
- **Ομαδικές Ενημερώσεις Κελιών** using `Cells.importArray` for large data sets instead of individual `putValue` calls.  
- **Αποδέσμευση Πόρων** by calling `book.dispose()` after saving large files.

## Συχνές Ερωτήσεις

**Q: Μπορώ να δημιουργήσω XLSX αντί για XLS;**  
A: Ναι – απλώς αλλάξτε την επέκταση του αρχείου σε `book.save("output.xlsx")`; το Aspose επιλέγει αυτόματα τη σωστή μορφή.

**Q: Απαιτείται άδεια για ανάπτυξη;**  
A: Μια δωρεάν άδεια δοκιμής λειτουργεί για ανάπτυξη και δοκιμές. Οι παραγωγικές εγκαταστάσεις απαιτούν αγορασμένη άδεια.

**Q: Πώς μπορώ να προσθέσω περισσότερους τύπους διαγραμμάτων;**  
A: Χρησιμοποιήστε το enum `ChartType` (π.χ., `ChartType.PIE`, `ChartType.LINE`) όταν καλείτε `charts.add(...)`.

**Q: Τι κάνω αν χρειάζεται να προστατεύσω το βιβλίο εργασίας;**  
A: Καλέστε `book.getSettings().setPassword("yourPassword")` πριν από την αποθήκευση.

**Q: Υποστηρίζει το Aspose.Cells αρχεία με ενεργοποιημένα μακροεντολές;**  
A: Ναι – μπορείτε να δημιουργήσετε ή να διατηρήσετε VBA μακροεντολές σε βιβλία εργασίας XLSM.

**Last Updated:** 2026-04-11  
**Tested With:** Aspose.Cells 25.3 (Java)  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}