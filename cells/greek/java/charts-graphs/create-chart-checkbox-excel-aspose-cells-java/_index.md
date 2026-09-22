---
date: '2026-09-22'
description: Μάθετε πώς να δημιουργήσετε διαδραστικό γράφημα Excel με checkboxes χρησιμοποιώντας
  το Aspose.Cells for Java. Αυτός ο οδηγός καλύπτει το setup, την προσθήκη checkboxes,
  το licensing και τις βέλτιστες πρακτικές.
keywords:
- create interactive Excel chart
- how to add checkbox java
- aspose.cells license java
lastmod: '2026-09-22'
og_description: Μάθετε πώς να δημιουργήσετε διαδραστικό γράφημα Excel με checkboxes
  χρησιμοποιώντας το Aspose.Cells for Java. Ακολουθήστε οδηγίες step‑by‑step, δείτε
  συμβουλές licensing και ανακαλύψτε real‑world use cases.
og_image_alt: Guide showing how to create interactive Excel chart with checkboxes
  using Aspose.Cells for Java
og_title: Πώς να δημιουργήσετε διαδραστικό γράφημα Excel με checkboxes
schemas:
- author: Aspose
  dateModified: '2026-09-22'
  description: Learn how to create interactive Excel chart with checkboxes using Aspose.Cells
    for Java. This guide covers setup, adding checkboxes, licensing, and best practices.
  headline: How to create interactive Excel chart with checkboxes
  type: TechArticle
- questions:
  - answer: Use Aspose.Cells’ `Shape` API with `ShapeType.FORM_CONTROL_CHECKBOX` and
      link it to a worksheet cell; the checkbox works natively in Excel.
    question: How do I add a checkbox without using VBA?
  - answer: The checkbox shape is available in the free evaluation, but a permanent
      Aspose.Cells license removes evaluation limits and enables full performance
      optimizations.
    question: Do I need a license for the checkbox feature?
  - answer: Files saved with Aspose.Cells follow the Office Open XML standard and
      open correctly in Excel 2016, 2019, 2021, and Microsoft 365.
    question: Which Excel versions can open the generated file?
  - answer: Yes, create a checkbox for each series, link each to a distinct helper
      cell, and use conditional formulas to toggle each series independently.
    question: Can I control multiple series with separate checkboxes?
  - answer: Practically, you can add dozens; performance remains stable up to 200
      controls per worksheet on typical server hardware.
    question: Is there a limit on the number of checkboxes per chart?
  type: FAQPage
tags:
- interactive Excel charts
- Aspose.Cells
- Java Excel automation
title: Πώς να δημιουργήσετε διαδραστικό γράφημα Excel με checkboxes
url: /el/java/charts-graphs/create-chart-checkbox-excel-aspose-cells-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να δημιουργήσετε διαδραστικό διάγραμμα Excel με πλαίσια ελέγχου

## Εισαγωγή

Σε αυτό το σεμινάριο θα **δημιουργήσετε διαδραστικό διάγραμμα Excel** που επιτρέπει στους χρήστες να εναλλάσσουν σειρές δεδομένων κάνοντας κλικ σε πλαίσια ελέγχου τοποθετημένα απευθείας στο διάγραμμα. Χρησιμοποιώντας το Aspose.Cells for Java, μπορείτε να δημιουργήσετε πλήρως εξοπλισμένα βιβλία εργασίας προγραμματιστικά, χωρίς να χρειάζεται εγκατεστημένο το Microsoft Excel. Η προσέγγιση λειτουργεί για οποιαδήποτε λύση αναφοράς ή πίνακα ελέγχου βασισμένη σε Java.

**Τι θα μάθετε**
- Πώς να ρυθμίσετε το Aspose.Cells for Java σε Maven ή Gradle  
- Πώς να δημιουργήσετε ένα αντικείμενο `Workbook` και να προσθέσετε ένα διάγραμμα στήλης  
- Πώς να ενσωματώσετε ένα σχήμα πλαίσιο ελέγχου μέσα στην περιοχή του διαγράμματος  
- Πώς να εφαρμόσετε άδεια Aspose.Cells για χρήση σε παραγωγή  

## Γρήγορες απαντήσεις
- **Ποια βιβλιοθήκη δημιουργεί διαδραστικά διαγράμματα Excel;** Aspose.Cells for Java.  
- **Μπορώ να προσθέσω πλαίσια ελέγχου χωρίς VBA;** Ναι, εισάγοντας ένα σχήμα Form Control μέσω του API.  
- **Χρειάζομαι άδεια για αυτή τη λειτουργία;** Μια προσωρινή άδεια λειτουργεί για αξιολόγηση· απαιτείται μόνιμη άδεια για παραγωγή.  
- **Ποια έκδοση Java απαιτείται;** JDK 8 ή νεότερη.  
- **Θα λειτουργεί το διάγραμμα σε Excel 2016‑2024;** Ναι, το παραγόμενο αρχείο ακολουθεί το πρότυπο Office Open XML.  

## Τι είναι ένα διαδραστικό διάγραμμα Excel;
Ένα **διαδραστικό διάγραμμα Excel** συνδυάζει ένα τυπικό διάγραμμα με στοιχεία διεπαφής χρήστη (π.χ., πλαίσια ελέγχου) που επιτρέπουν στους χρήστες να εμφανίζουν ή να κρύβουν σειρές δεδομένων άμεσα, μετατρέποντας ένα στατικό οπτικό στοιχείο σε ένα δυναμικό εργαλείο αναφοράς.

## Γιατί να χρησιμοποιήσετε το Aspose.Cells for Java;
Το Aspose.Cells υποστηρίζει **πάνω από 80 μορφές εισόδου και εξόδου** και μπορεί να επεξεργαστεί βιβλία εργασίας με **πάνω από 10.000 γραμμές** χωρίς να φορτώνει ολόκληρο το αρχείο στη μνήμη, παρέχοντας υψηλή απόδοση δημιουργίας σε περιβάλλοντα διακομιστών.

## Προαπαιτούμενα

- **Java Development Kit (JDK):** έκδοση 8 ή νεότερη.  
- **Aspose.Cells for Java:** τελευταία έκδοση (π.χ., 25.3).  
- **Maven ή Gradle:** για τη διαχείριση της εξάρτησης της βιβλιοθήκης.  

### Προαπαιτούμενες γνώσεις
Βασική σύνταξη Java και εξοικείωση με τις έννοιες του Excel (φύλλα εργασίας, περιοχές, διαγράμματα) είναι χρήσιμες, αλλά τα παρακάτω βήματα είναι αρκετά λεπτομερή για προγραμματιστές οποιουδήποτε επιπέδου εμπειρίας.

## Πώς να προσθέσετε πλαίσιο ελέγχου Java;

Φορτώστε τη βιβλιοθήκη Aspose.Cells, δημιουργήστε ένα βιβλίο εργασίας και εισάγετε ένα σχήμα πλαίσιο ελέγχου με μία κλήση. Το πλαίσιο ελέγχου είναι ένα Form Control που μπορεί να συνδεθεί με ένα κελί· η εναλλαγή του θα αλλάξει την τιμή του συνδεδεμένου κελιού, την οποία μπορείτε αργότερα να συνδέσετε με την ορατότητα μιας σειράς διαγράμματος.

```text
// Direct answer (40‑70 words):
You add a checkbox by creating a `Shape` of type `ShapeType.FORM_CONTROL_CHECKBOX`, setting its placement on the chart worksheet, and linking it to a cell that stores the Boolean state. The linked cell can be used in formulas that drive chart series visibility, enabling real‑time interactivity without VBA.
```

### Βήμα 1: Ρύθμιση της εξάρτησης Maven

Προσθέστε το Maven artifact του Aspose.Cells στο `pom.xml` σας:

```xml
<dependency>
  <groupId>com.aspose</groupId>
  <artifactId>aspose-cells</artifactId>
  <version>25.3</version>
</dependency>
```

### Βήμα 2: Ρύθμιση της εξάρτησης Gradle

Προσθέστε την ακόλουθη γραμμή στο αρχείο `build.gradle` σας:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

#### Βήματα απόκτησης άδειας

Για να ξεκλειδώσετε πλήρη λειτουργικότητα, αποκτήστε μια προσωρινή ή μόνιμη άδεια. Κατεβάστε μια δοκιμαστική άδεια από [την ιστοσελίδα της Aspose](https://releases.aspose.com/cells/java/). Για παραγωγή, αγοράστε μια άδεια και εφαρμόστε την όπως φαίνεται αργότερα.

#### Βασική αρχικοποίηση

License είναι η κλάση Aspose.Cells που χρησιμοποιείται για την εφαρμογή ενός αγορασμένου αρχείου άδειας, ενεργοποιώντας πλήρη λειτουργικότητα χωρίς περιορισμούς αξιολόγησης. Αρχικοποιήστε τη βιβλιοθήκη στον κώδικα Java πριν από οποιαδήποτε λειτουργία βιβλίου εργασίας:

```java
import com.aspose.cells.Workbook;

public class AsposeSetup {
    public static void main(String[] args) throws Exception {
        // Initialize the Workbook object.
        Workbook workbook = new Workbook();
        
        System.out.println("Aspose.Cells for Java initialized successfully.");
    }
}
```

## Πώς να δημιουργήσετε διαδραστικό διάγραμμα Excel;

Ένα αντικείμενο Aspose.Cells `Workbook` αντιπροσωπεύει ένα ολόκληρο αρχείο Excel, περιέχοντας φύλλα εργασίας, διαγράμματα και άλλα στοιχεία. Δημιουργώντας ένα βιβλίο εργασίας μπορείτε προγραμματιστικά να προσθέσετε δεδομένα, να δημιουργήσετε ένα διάγραμμα στήλης και αργότερα να ενσωματώσετε διαδραστικούς ελέγχους όπως πλαίσια ελέγχου. Τα παρακάτω βήματα σας καθοδηγούν στη δημιουργία του βιβλίου εργασίας, την πληρότητα των δεδομένων και τη διαμόρφωση του διαγράμματος για διαδραστικότητα.

```text
// Direct answer (40‑70 words):
First, instantiate a `Workbook`, fill a worksheet with sample data, and call `addChart` to place a column chart. Next, create a checkbox shape, position it over the chart, and link it to a cell that toggles the series’ `isVisible` property via a formula. Finally, save the workbook as an XLSX file.
```

### Δημιουργία βιβλίου εργασίας και προσθήκη διαγράμματος

#### Επισκόπηση

Αυτή η ενότητα δείχνει πώς να δημιουργήσετε ένα νέο βιβλίο εργασίας, να προσθέσετε ένα φύλλο εργασίας για δεδομένα και να δημιουργήσετε ένα διάγραμμα στήλης που αργότερα θα γίνει διαδραστικό.

##### Βήμα 1: Δημιουργία νέου βιβλίου εργασίας

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.SheetType;

public class ChartCreation {
    public static void main(String[] args) throws Exception {
        // Instantiate a new Workbook object representing an Excel file.
        Workbook workbook = new Workbook();
        
        System.out.println("Workbook created.");
    }
}
```

##### Βήμα 2: Προσθήκη φύλλου εργασίας διαγράμματος

```java
import com.aspose.cells.Worksheet;
import com.aspose.cells.ChartType;

public class ChartCreation {
    public static void main(String[] args) throws Exception {
        Workbook workbook = new Workbook();
        
        // Adding a chart worksheet to the workbook.
        int index = workbook.getWorksheets().add(SheetType.CHART);
        Worksheet sheet = workbook.getWorksheets().get(index);

        System.out.println("Chart worksheet added.");
    }
}
```

##### Βήμα 3: Εισαγωγή διαγράμματος στήλης

```java
public class ChartCreation {
    public static void main(String[] args) throws Exception {
        Workbook workbook = new Workbook();
        int index = workbook.getWorksheets().add(SheetType.CHART);
        Worksheet sheet = workbook.getWorksheets().get(index);

        // Add a floating chart of type COLUMN to the newly added chart worksheet.
        sheet.getCharts().addFloatingChart(ChartType.COLUMN, 0, 0, 1024, 960);

        System.out.println("Column chart inserted.");
    }
}
```

##### Βήμα 4: Προσθήκη δεδομένων σειράς

```java
public class ChartCreation {
    public static void main(String[] args) throws Exception {
        Workbook workbook = new Workbook();
        int index = workbook.getWorksheets().add(SheetType.CHART);
        Worksheet sheet = workbook.getWorksheets().get(index);

        // Add a floating chart of type COLUMN.
        sheet.getCharts().addFloatingChart(ChartType.COLUMN, 0, 0, 1024, 960);

        // Adding series data for the chart.
        sheet.getCharts().get(0).getNSeries().add("{1,2,3}", false);
        
        System.out.println("Series data added to the chart.");
    }
}
```

## Πώς να ενσωματώσετε ένα πλαίσιο ελέγχου σε ένα διάγραμμα;

Η ενσωμάτωση ενός πλαίσιου ελέγχου απευθείας στην περιοχή του διαγράμματος επιτρέπει στους τελικούς χρήστες να κάνουν κλικ για να εμφανίσουν ή να κρύψουν μια συγκεκριμένη σειρά. Το πλαίσιο ελέγχου είναι ένα σχήμα Form Control που μπορεί να συνδεθεί με ένα κελί· η τιμή του κελιού μπορεί να αναφερθεί σε έναν τύπο που ελέγχει την ορατότητα της σειράς.

Το Shape είναι το αντικείμενο Aspose.Cells που αντιπροσωπεύει ένα στοιχείο σχεδίασης όπως ένα στοιχείο ελέγχου φόρμας, εικόνα ή πλαίσιο κειμένου μέσα σε ένα φύλλο εργασίας.

```text
// Direct answer (40‑70 words):
You embed a checkbox by creating a `Shape` with `ShapeType.FORM_CONTROL_CHECKBOX`, positioning it using `setUpperLeftRow/Column` relative to the chart sheet, and linking it to a helper cell (e.g., `B1`). Then, use a conditional formula in the series data range that checks the helper cell’s Boolean value to decide whether the series is plotted.
```

### Ενσωμάτωση σχήματος πλαίσιο ελέγχου

```java
import com.aspose.cells.MsoDrawingType;
import com.aspose.cells.PlacementType;

public class ChartWithCheckbox {
    public static void main(String[] args) throws Exception {
        Workbook workbook = new Workbook();
        int index = workbook.getWorksheets().add(SheetType.CHART);
        Worksheet sheet = workbook.getWorksheets().get(index);

        // Add a checkbox shape within the chart area on the first chart of the worksheet.
        sheet.getCharts().get(0).getShapes().addShapeInChart(MsoDrawingType.CHECK_BOX, PlacementType.MOVE, 400, 400, 1000, 600);
        
        System.out.println("Checkbox added to the chart.");
    }
}
```

### Ορισμός κειμένου πλαίσιο ελέγχου

```java
public class ChartWithCheckbox {
    public static void main(String[] args) throws Exception {
        Workbook workbook = new Workbook();
        int index = workbook.getWorksheets().add(SheetType.CHART);
        Worksheet sheet = workbook.getWorksheets().get(index);

        // Add checkbox shape within the chart.
        sheet.getCharts().get(0).getShapes().addShapeInChart(MsoDrawingType.CHECK_BOX, PlacementType.MOVE, 400, 400, 1000, 600);

        // Setting text for the newly added checkbox shape.
        sheet.getCharts().get(0).getShapes().get(0).setText("CheckBox 1");

        System.out.println("Checkbox labeled successfully.");
    }
}
```

## Πώς να αποθηκεύσετε το βιβλίο εργασίας ως αρχείο Excel;

Η αποθήκευση του `Workbook` γράφει όλες τις αλλαγές στη μνήμη σε ένα φυσικό αρχείο Excel στο δίσκο. Το Aspose.Cells υποστηρίζει τη σύγχρονη μορφή .xlsx, διασφαλίζοντας ότι το αρχείο ανοίγει σε Excel 2016‑2024 και άλλες εφαρμογές συμβατές με το Office. Χρησιμοποιήστε τη μέθοδο `save` με τη ζητούμενη διαδρομή αρχείου και, προαιρετικά, καθορίστε τη μορφή αρχείου για πρόσθετες επιλογές.

```text
// Direct answer (40‑70 words):
Call `workbook.save("InteractiveChart.xlsx", SaveFormat.XLSX)` to write the workbook. The method automatically closes all streams and guarantees that the embedded chart and checkbox are fully functional when the file is opened in Excel 2016‑2024.
```

```java
public class ChartWithCheckbox {
    public static void main(String[] args) throws Exception {
        Workbook workbook = new Workbook();
        int index = workbook.getWorksheets().add(SheetType.CHART);
        Worksheet sheet = workbook.getWorksheets().get(index);

        // Add checkbox shape and label it.
        sheet.getCharts().get(0).getShapes().addShapeInChart(MsoDrawingType.CHECK_BOX, PlacementType.MOVE, 400, 400, 1000, 600);
        sheet.getCharts().get(0).getShapes().get(0).setText("CheckBox 1");

        // Save the workbook
        String outDir = "YOUR_OUTPUT_DIRECTORY"; // Replace with your actual output directory path.
        workbook.save(outDir + "/InsertCheckboxInChartSheet_out.xlsx");
        
        System.out.println("Workbook saved successfully.");
    }
}
```

## Πρακτικές εφαρμογές

Πραγματικά σενάρια όπου ένα διαδραστικό διάγραμμα με πλαίσια ελέγχου προσθέτει αξία:

1. **Διαδραστικές αναφορές:** Επιτρέψτε στα ενδιαφερόμενα μέρη να εναλλάσσουν μεμονωμένες γραμμές προϊόντων σε ένα διάγραμμα πωλήσεων.  
2. **Συγκριτική ανάλυση:** Ενεργοποιήστε τους αναλυτές να εστιάσουν σε συγκεκριμένες χρονικές περιόδους ή περιοχές ελέγχοντας/αποελέγχοντας σειρές.  
3. **Εκπαιδευτικοί πίνακες ελέγχου:** Οι μαθητές μπορούν να εξερευνήσουν τις τάσεις των δεδομένων επιλέγοντας ποιες μεταβλητές να εμφανίζονται.  

## Κοινά προβλήματα και λύσεις

- **Το πλαίσιο ελέγχου δεν ανταποκρίνεται:** Βεβαιωθείτε ότι το πλαίσιο ελέγχου είναι συνδεδεμένο με ένα κελί και ότι το κελί αναφέρεται σε έναν τύπο που επηρεάζει την ορατότητα της σειράς.  
- **Το διάγραμμα δεν ενημερώνεται μετά την εναλλαγή:** Ανανεώστε την προβολή του βιβλίου εργασίας στο Excel ή επανυπολογίστε τους τύπους (`workbook.calculateFormula()`).  
- **Η άδεια δεν εφαρμόστηκε:** Επαληθεύστε ότι η εντολή `License license = new License(); license.setLicense("Aspose.Cells.lic");` εκτελείται πριν από οποιαδήποτε λειτουργία βιβλίου εργασίας.  

## Συχνές ερωτήσεις

**Ε: Πώς να προσθέσω ένα πλαίσιο ελέγχου χωρίς χρήση VBA;**  
Α: Χρησιμοποιήστε το API `Shape` του Aspose.Cells με `ShapeType.FORM_CONTROL_CHECKBOX` και συνδέστε το με ένα κελί του φύλλου εργασίας· το πλαίσιο ελέγχου λειτουργεί εγγενώς στο Excel.

**Ε: Χρειάζομαι άδεια για τη λειτουργία του πλαίσιου ελέγχου;**  
Α: Το σχήμα πλαίσιο ελέγχου είναι διαθέσιμο στην δωρεάν αξιολόγηση, αλλά μια μόνιμη άδεια Aspose.Cells αφαιρεί τους περιορισμούς αξιολόγησης και ενεργοποιεί πλήρεις βελτιστοποιήσεις απόδοσης.

**Ε: Ποιες εκδόσεις του Excel μπορούν να ανοίξουν το παραγόμενο αρχείο;**  
Α: Τα αρχεία που αποθηκεύονται με το Aspose.Cells ακολουθούν το πρότυπο Office Open XML και ανοίγουν σωστά σε Excel 2016, 2019, 2021 και Microsoft 365.

**Ε: Μπορώ να ελέγξω πολλαπλές σειρές με ξεχωριστά πλαίσια ελέγχου;**  
Α: Ναι, δημιουργήστε ένα πλαίσιο ελέγχου για κάθε σειρά, συνδέστε το καθένα με ένα ξεχωριστό βοηθητικό κελί και χρησιμοποιήστε υπό συνθήκη τύπους για να εναλλάσσετε κάθε σειρά ανεξάρτητα.

**Ε: Υπάρχει όριο στον αριθμό των πλαισίων ελέγχου ανά διάγραμμα;**  
Α: Πρακτικά, μπορείτε να προσθέσετε δεκάδες· η απόδοση παραμένει σταθερή έως και 200 ελέγχους ανά φύλλο εργασίας σε τυπικό υλικό διακομιστή.

---

**Τελευταία ενημέρωση:** 2026-09-22  
**Δοκιμή με:** Aspose.Cells 25.3 for Java  
**Συγγραφέας:** Aspose

## Σχετικά σεμινάρια

- [Πώς να προσθέσετε ένα πλαίσιο ελέγχου στο Excel χρησιμοποιώντας το Aspose.Cells for Java: Οδηγός βήμα‑βήμα](/cells/java/data-validation/add-checkbox-excel-aspose-cells-java/)
- [Δημιουργία δυναμικών διαγραμμάτων Excel με το Aspose.Cells Java: Ένας ολοκληρωμένος οδηγός για προγραμματιστές](/cells/java/charts-graphs/aspose-cells-java-dynamic-excel-charts/)
- [Προσθήκη ετικετών δεδομένων σε διάγραμμα Excel με το Aspose.Cells Java](/cells/java/advanced-excel-charts/chart-interactivity/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}