---
date: '2026-04-08'
description: Μάθετε πώς να δημιουργήσετε γράφημα στήλης σε Java χρησιμοποιώντας το
  Aspose.Cells, καλύπτοντας τη δημιουργία γραφήματος Java, την προσθήκη φύλλου γραφήματος
  και την εξαγωγή του βιβλίου εργασίας σε Excel.
keywords:
- generate column chart
- create chart java
- add chart sheet
- populate excel cells
- set chart title
- export workbook excel
title: Δημιουργία γραφήματος στήλης με το Aspose.Cells Java – Οδηγός
url: /el/java/charts-graphs/aspose-cells-java-create-customize-charts/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία Γραφήματος Στήλης με Aspose.Cells Java

Στις σύγχρονες εφαρμογές που βασίζονται στα δεδομένα, η **δημιουργία γραφήματος στήλης** γρήγορα και προγραμματιστικά μπορεί να μετατρέψει ακατέργαστους αριθμούς σε σαφείς οπτικές πληροφορίες. Είτε δημιουργείτε έναν πίνακα αναφορών, ένα εργαλείο ανάλυσης ή μια απλή λειτουργία εξαγωγής, το Aspose.Cells for Java σας παρέχει ένα ευέλικτο API για **δημιουργία chart java** έργων χωρίς να χρειάζεται να ασχοληθείτε με το UI του Excel. Σε αυτό το tutorial θα μάθετε πώς να ρυθμίσετε τη βιβλιοθήκη, **να γεμίσετε κελιά Excel**, να προσθέσετε ένα **φύλλο γραφήματος**, να προσαρμόσετε τον **τίτλο γραφήματος**, και τελικά **να εξάγετε το workbook excel** σε ένα αρχείο.

## Γρήγορες Απαντήσεις
- **Τι σημαίνει “generate column chart”;** Δημιουργεί μια κατακόρυφη οπτικοποίηση τύπου μπάρας από δεδομένα σε πίνακα.  
- **Ποια βιβλιοθήκη απαιτείται;** Aspose.Cells for Java (διαθέσιμο δωρεάν δοκιμαστικό).  
- **Χρειάζομαι εγκατάσταση του Excel;** Όχι, η βιβλιοθήκη λειτουργεί ανεξάρτητα από το Microsoft Excel.  
- **Μπορώ να εξάγω σε μορφές εκτός του XLS;** Ναι – PDF, PNG, SVG κ.λπ., μέσω `workbook.save()`.  
- **Απαιτείται άδεια για παραγωγή;** Ναι, απαιτείται αγορασμένη ή προσωρινή άδεια.

## Τι είναι ένα generate column chart;
Ένα γράφημα στήλης εμφανίζει σειρές δεδομένων ως κατακόρυφες μπάρες, καθιστώντας εύκολη τη σύγκριση τιμών μεταξύ κατηγοριών όπως περιοχές, μήνες ή γραμμές προϊόντων. Το Aspose.Cells σας επιτρέπει να δημιουργήσετε αυτό το γράφημα εξ ολοκλήρου με κώδικα, παρέχοντάς σας πλήρη έλεγχο πάνω στα δεδομένα, το στυλ και τη μορφή εξόδου.

## Γιατί να χρησιμοποιήσετε το Aspose.Cells για να δημιουργήσετε chart java;
- **Χωρίς COM interop** – λειτουργεί σε οποιοδήποτε OS με JVM.  
- **Πλούσιες επιλογές στυλ** – εικόνες, διαβαθμίσεις, υπομνήματα και προσαρμοσμένες γραμματοσειρές.  
- **Υψηλή απόδοση** – κατάλληλο για μεγάλα σύνολα δεδομένων.  
- **Πολλαπλές μορφές εξαγωγής** – XLS, XLSX, PDF, PNG και άλλα.

## Προαπαιτούμενα
- **Java Development Kit (JDK) 8+** εγκατεστημένο.  
- Βασικές γνώσεις Java και εξοικείωση με έννοιες του Excel.  

### Απαιτούμενες Βιβλιοθήκες
Προσθέστε το Aspose.Cells στο έργο σας χρησιμοποιώντας ένα από τα παρακάτω αποσπάσματα.

#### Maven
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

#### Gradle
```gradle
implementation group: 'com.aspose', name: 'aspose-cells', version: '25.3'
```

### Απόκτηση Άδειας
Η Aspose προσφέρει δωρεάν δοκιμαστική έκδοση και προσωρινή άδεια για εκτενή δοκιμή.

- **Free Trial**: [Download Free](https://releases.aspose.com/cells/java/)  
- **Temporary License**: [Request Here](https://purchase.aspose.com/temporary-license/)

## Ρύθμιση Aspose.Cells για Java
Πρώτα, δημιουργήστε ένα αντικείμενο `Workbook` – αυτό θα είναι ο καμβάς για τα δεδομένα και το γράφημα μας.

```java
import com.aspose.cells.Workbook;

// Initialize a new Workbook
Workbook workbook = new Workbook();
```

## Οδηγός Βήμα‑Βήμα

### 1. Δημιουργία και Ονομασία Φύλλου Εργασίας
Θα αποθηκεύσουμε τα ακατέργαστα δεδομένα σε ένα φύλλο που ονομάζεται **Data**.

```java
import com.aspose.cells.Worksheet;

// Create a new Workbook instance
Workbook workbook = new Workbook();
```

```java
// Access the first worksheet and set its name to "Data"
Worksheet sheet = workbook.getWorksheets().get(0);
sheet.setName("Data");
```

### 2. Συμπλήρωση Κελιών Excel
Εισάγετε ονόματα περιοχών και αριθμούς πωλήσεων που θα οπτικοποιήσει το γράφημα στήλης.

```java
import com.aspose.cells.Cells;

// Get the cells collection from the "Data" sheet
Cells cells = sheet.getCells();
```

```java
// Insert region names and sales figures
cells.get("A1").putValue("Region");
cells.get("B1").putValue("Sale");

String[] regions = {"France", "Germany", "England", "Sweden", "Italy", "Spain", "Portugal"};
int[] sales = {70000, 55000, 30000, 40000, 35000, 32000, 10000};

for (int i = 0; i < regions.length; i++) {
    cells.get("A" + (i+2)).putValue(regions[i]);
    cells.get("B" + (i+2)).putValue(sales[i]);
}
```

### 3. Προσθήκη Φύλλου Γραφήματος
Ο διαχωρισμός του γραφήματος από τα ακατέργαστα δεδομένα διατηρεί το βιβλίο εργασίας τακτικό.

```java
import com.aspose.cells.SheetType;

// Add a new chart sheet
int sheetIndex = workbook.getWorksheets().add(SheetType.CHART);
Worksheet chartSheet = workbook.getWorksheets().get(sheetIndex);

// Name the worksheet "Chart"
chartSheet.setName("Chart");
```

### 4. Δημιουργία Γραφήματος Στήλης
Τώρα δημιουργούμε πραγματικά αντικείμενα **generate column chart**.

```java
import com.aspose.cells.Chart;
import com.aspose.cells.ChartType;

// Add a new column chart to the "Chart" sheet
int chartIndex = chartSheet.getCharts().add(ChartType.COLUMN, 1, 1, 25, 10);
Chart chart = chartSheet.getCharts().get(chartIndex);
```

### 5. Ορισμός Εικόνας ως Γέμισμα Φόντου στην Περιοχή Σχεδίασης
Μια εικόνα φόντου μπορεί να κάνει το γράφημα πιο εντυπωσιακό.

```java
import java.io.FileInputStream;
import com.aspose.cells.Color;

String dataDir = "YOUR_DATA_DIRECTORY";
File file = new FileInputStream(dataDir + "aspose-logo.png");
byte[] data = new byte[(int)file.length()];
file.read(data);

chart.getPlotArea().getArea().getFillFormat().setImageData(data);
chart.getPlotArea().getBorder().setVisible(false);
```

### 6. Ορισμός Τίτλου Γραφήματος
Η προσαρμογή του **set chart title** βελτιώνει την αναγνωσιμότητα.

```java
// Configure the chart's title properties
chart.getTitle().setText("Sales By Region");
chart.getTitle().getFont().setColor(Color.getBlue());
chart.getTitle().getFont().setBold(true);
chart.getTitle().getFont().setSize(12);
```

### 7. Διαμόρφωση Δεδομένων Σειράς και Υπομνήματος
Συνδέστε την περιοχή δεδομένων με το γράφημα και τοποθετήστε το υπόμνημα.

```java
// Set series and category data for the chart
chart.getNSeries().add("Data!B2:B8", true);
chart.getNSeries().setCategoryData("Data!A2:A8");
chart.getNSeries().setColorVaried(true);

// Position the legend at the top of the chart
import com.aspose.cells.Legend;
import com.aspose.cells.LegendPositionType;

Legend legend = chart.getLegend();
legend.setPosition(LegendPositionType.TOP);
```

### 8. Εξαγωγή Workbook Excel
Τέλος, **export workbook excel** σε αρχείο XLS (ή σε οποιαδήποτε υποστηριζόμενη μορφή).

```java
String outDir = "YOUR_OUTPUT_DIRECTORY";
workbook.save(outDir + "SPAsBFillInChart_out.xls");
```

## Πρακτικές Εφαρμογές
- **Business Reports** – Αυτόματη δημιουργία γραφημάτων πωλήσεων για μηνιαία PDF.  
- **Data Analysis Tools** – Ενσωμάτωση δυναμικών γραφημάτων σε προσαρμοσμένους πίνακες αναλύσεων.  
- **Enterprise Dashboards** – Ανανέωση εικόνων γραφήματος σε πραγματικό χρόνο για παρακολούθηση.

## Σκέψεις Απόδοσης
- Ενημερώσεις κελιών σε παρτίδες όταν εργάζεστε με μεγάλα σύνολα δεδομένων για μείωση του φόρτου.  
- Απελευθερώστε πόρους (`workbook.dispose()`) εάν επεξεργάζεστε πολλά βιβλία εργασίας σε βρόχο.  

## Συχνά Προβλήματα και Λύσεις
- **Image not showing** – Επαληθεύστε τη διαδρομή του αρχείου και ότι η μορφή εικόνας (PNG, JPEG) υποστηρίζεται.  
- **Chart appears blank** – Βεβαιωθείτε ότι οι αναφορές περιοχής δεδομένων (`Data!B2:B8`) ταιριάζουν με τα γεμισμένα κελιά.  
- **Out‑of‑memory errors** – Επεξεργαστείτε τα δεδομένα σε τμήματα και καλέστε `System.gc()` μετά από μεγάλες αποθηκεύσεις.  

## Συχνές Ερωτήσεις

**Q: Πώς προσθέτω πολλαπλές σειρές σε ένα γράφημα στήλης;**  
A: Call `chart.getNSeries().add()` repeatedly with different data ranges, e.g., `"Data!C2:C8"` for a second series.

**Q: Μπορώ να αλλάξω τις ετικέτες των αξόνων;**  
A: Yes. Use `chart.getCategoryAxis().setTitle("Regions")` and `chart.getValueAxis().setTitle("Sales")`.

**Q: Σε ποιες μορφές μπορώ να εξάγω εκτός του XLS;**  
A: Use `workbook.save("chart.pdf")`, `workbook.save("chart.png")`, or `workbook.save("chart.xlsx")` for PDF, PNG, and XLSX respectively.

**Q: Απαιτείται άδεια για εκδόσεις ανάπτυξης;**  
A: A free trial works for evaluation, but a permanent or temporary license is needed for production deployments.

**Q: Πώς μπορώ να βελτιώσω την ταχύτητα απόδοσης για χιλιάδες γραμμές;**  
A: Populate cells using `cells.importArray()` and minimize chart redraws by creating the chart after all data is loaded.

---

**Τελευταία Ενημέρωση:** 2026-04-08  
**Δοκιμή Με:** Aspose.Cells 25.3 for Java  
**Συγγραφέας:** Aspose  

## Πόροι

- [Τεκμηρίωση Aspose.Cells](https://reference.aspose.com/cells/java/)
- [Λήψη Aspose.Cells](https://releases.aspose.com/cells/java/)
- [Αγορά Άδειας](https://purchase.aspose.com/buy)
- [Δωρεάν Δοκιμή](https://releases.aspose.com/cells/java/)
- [Αίτηση για Προσωρινή Άδεια](https://purchase.aspose.com/temporary-license/)
- [Φόρουμ Υποστήριξης](https://forum.aspose.com/c/cells/9)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}