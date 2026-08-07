---
date: '2026-04-08'
description: Μάθετε πώς να δημιουργήσετε ένα γράφημα γραμμής με δείκτες χρησιμοποιώντας
  το Aspose.Cells για Java, να προσθέσετε το γράφημα στο φύλλο εργασίας και να προσαρμόσετε
  τα γραφήματα Excel για αυτοματοποιημένη αναφορά.
keywords:
- line chart with markers
- add chart to worksheet
- automate excel chart creation
- populate data for chart
- export styled chart excel
title: Δημιουργία γραμμικού διαγράμματος με δείκτες χρησιμοποιώντας το Aspose.Cells
  για Java
url: /el/java/charts-graphs/aspose-cells-java-excel-charts-creation/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία και Στυλιζάρισμα Διαγραμμάτων Excel με Aspose.Cells Java

## Εισαγωγή

Στον σημερινό κόσμο που βασίζεται στα δεδομένα, ένα **διάγραμμα γραμμής με σημεία** είναι ένας από τους πιο αποτελεσματικούς τρόπους για να οπτικοποιήσετε τάσεις και ακραίες τιμές. Είτε δημιουργείτε αυτοματοποιημένες αναφορές είτε έναν πίνακα ελέγχου που ενημερώνεται καθημερινά, η δυνατότητα να προσθέσετε προγραμματιστικά ένα διάγραμμα γραμμής με σημεία σε ένα φύλλο εργασίας εξοικονομεί αμέτρητα χειροκίνητα βήματα. Αυτό το σεμινάριο σας καθοδηγεί στη χρήση του Aspose.Cells for Java για τη δημιουργία, το στυλ και την εξαγωγή τέτοιων διαγραμμάτων, ώστε να εστιάσετε στις αναλύσεις αντί στην επίπονη δουλειά με το Excel.

**Τι Θα Μάθετε**
- Αρχικοποίηση ενός βιβλίου εργασίας (workbook) και συμπλήρωση δεδομένων χρησιμοποιώντας το Aspose.Cells.  
- **Πώς να προσθέσετε ένα διάγραμμα γραμμής με σημεία σε ένα φύλλο εργασίας** και να διαμορφώσετε την εμφάνισή του.  
- Προσαρμογή χρωμάτων σειράς, σημείων και άλλων επιλογών στυλ.  
- Αποθήκευση του βιβλίου εργασίας ως αρχείο Excel που περιλαμβάνει το στυλιζαρισμένο διάγραμμα.

## Γρήγορες Απαντήσεις
- **Ποια είναι η κύρια κλάση για εκκίνηση;** `Workbook` αρχικοποιεί ένα νέο αρχείο Excel.  
- **Ποιος τύπος διαγράμματος δημιουργεί ένα διάγραμμα γραμμής με σημεία;** `ChartType.LINE_WITH_DATA_MARKERS`.  
- **Πώς ορίζω προσαρμοσμένα χρώματα για τα σημεία της σειράς;** Χρησιμοποιήστε `chart.getNSeries().setColorVaried(true)` και ορίστε τα χρώματα της περιοχής των σημείων.  
- **Χρειάζομαι άδεια για πλήρη λειτουργικότητα;** Ναι, μια επί πληρωμή ή προσωρινή άδεια Aspose.Cells αφαιρεί τους περιορισμούς αξιολόγησης.  
- **Μπορώ να εξάγω το αποτέλεσμα ως XLSX;** Απόλυτα—`workbook.save("StyledChart.xlsx")` δημιουργεί ένα αρχείο XLSX.

## Προαπαιτούμενα

Πριν δημιουργήσετε και στυλιζάρετε διαγράμματα χρησιμοποιώντας το Aspose.Cells for Java, βεβαιωθείτε ότι έχετε την ακόλουθη ρύθμιση:

### Απαιτούμενες Βιβλιοθήκες

Συμπεριλάβετε το Aspose.Cells ως εξάρτηση στο έργο σας. Ακολουθούν οδηγίες για χρήστες Maven και Gradle:

**Maven:**
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle:**
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### Απαιτήσεις Ρύθμισης Περιβάλλοντος
- Java Development Kit (JDK) εγκατεστημένο στο σύστημά σας.  
- Ένα ολοκληρωμένο περιβάλλον ανάπτυξης (IDE) όπως IntelliJ IDEA ή Eclipse για κωδικοποίηση και δοκιμές.

### Προαπαιτούμενες Γνώσεις
Απαιτείται βασική κατανόηση του προγραμματισμού Java, μαζί με εξοικείωση με βιβλία εργασίας Excel και έννοιες δημιουργίας διαγραμμάτων.

### Απόκτηση Άδειας
Aspose.Cells είναι εμπορικό προϊόν που απαιτεί άδεια για πλήρη λειτουργικότητα. Μπορείτε να αποκτήσετε δωρεάν δοκιμή για να αξιολογήσετε τις δυνατότητές του, να ζητήσετε προσωρινή άδεια για εκτεταμένες δοκιμές, ή να αγοράσετε το προϊόν για μακροπρόθεσμη χρήση.

- **Δωρεάν Δοκιμή:** [Download Free Trial](https://releases.aspose.com/cells/java/)  
- **Προσωρινή Άδεια:** [Request Temporary License](https://purchase.aspose.com/temporary-license/)  
- **Αγορά:** [Buy Aspose.Cells](https://purchase.aspose.com/buy)

## Ρύθμιση Aspose.Cells για Java

Μόλις εγκαταστήσετε τις απαραίτητες εξαρτήσεις, ρυθμίστε το περιβάλλον ανάπτυξής σας για χρήση του Aspose.Cells. Ξεκινήστε εισάγοντας τη βιβλιοθήκη και αρχικοποιώντας ένα αντικείμενο `Workbook` στην εφαρμογή Java:

```java
import com.aspose.cells.*;

public class SetupAsposeCells {
    public static void main(String[] args) throws Exception {
        // Initialize a new workbook instance
        Workbook workbook = new Workbook();
        
        System.out.println("Workbook initialized successfully!");
    }
}
```

## Οδηγός Υλοποίησης

Σε αυτήν την ενότητα, θα αναλύσουμε την υλοποίηση σε διακριτές λειτουργίες: Αρχικοποίηση Βιβλίου Εργασίας και Συμπλήρωση Δεδομένων, Δημιουργία και Διαμόρφωση Διαγράμματος, Προσαρμογή Σειρών, και Αποθήκευση Βιβλίου Εργασίας.

### Λειτουργία 1: Αρχικοποίηση Βιβλίου Εργασίας και Συμπλήρωση Δεδομένων

**Επισκόπηση:** Αυτή η λειτουργία εστιάζει στη δημιουργία ενός νέου βιβλίου εργασίας, στην πρόσβαση στο πρώτο του φύλλο εργασίας, και στη συμπλήρωση του με δεδομένα για τη δημιουργία διαγράμματος.

#### Βήμα 1: Αρχικοποίηση του Workbook
Ξεκινήστε δημιουργώντας ένα αντικείμενο `Workbook`:

```java
import com.aspose.cells.*;

public class FeatureWorkbookInitialization {
    public static void main(String[] args) throws Exception {
        // Instantiate a workbook
        Workbook workbook = new Workbook();
        
        // Access first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

#### Βήμα 2: Ορισμός Τίτλων Στηλών και Συμπλήρωση Δεδομένων
Ορίστε τις επικεφαλίδες των στηλών και συμπληρώστε τις γραμμές με δείγμα δεδομένων:

```java
        // Set columns title 
        worksheet.getCells().get(0, 0).setValue("X");
        worksheet.getCells().get(0, 1).setValue("Y");

        // Create random data for series 1
        for (int i = 1; i < 21; i++) {
            worksheet.getCells().get(i, 0).setValue(i);
            worksheet.getCells().get(i, 1).setValue(0.8);
        }

        // Create random data for series 2
        for (int i = 21; i < 41; i++) {
            worksheet.getCells().get(i, 0).setValue(i - 20);
            worksheet.getCells().get(i, 1).setValue(0.9);
        }
    }
}
```

### Λειτουργία 2: Δημιουργία και Διαμόρφωση Διαγράμματος

**Επισκόπηση:** Αυτή η λειτουργία δείχνει πώς να προσθέσετε ένα διάγραμμα στο φύλλο εργασίας του βιβλίου, να ορίσετε το στυλ του και να διαμορφώσετε βασικές ιδιότητες.

#### Βήμα 3: Προσθήκη Διαγράμματος στο Φύλλο Εργασίας
Προσθέστε ένα διάγραμμα γραμμής με σημεία δεδομένων:

```java
import com.aspose.cells.*;

public class FeatureChartCreation {
    public static void main(String[] args) throws Exception {
        // Instantiate a workbook
        Workbook workbook = new Workbook();
        
        // Access first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);
        
        // Add chart to the worksheet
        int idx = worksheet.getCharts().add(ChartType.LINE_WITH_DATA_MARKERS, 1, 3, 20, 20);

        // Access and configure the chart
        Chart chart = worksheet.getCharts().get(idx);
        chart.setStyle(3); // Set a predefined style
        chart.setAutoScaling(true);
        chart.getTitle().setText("Sample Chart");
        chart.getCategoryAxis().getTitle().setText("Units");
    }
}
```

### Λειτουργία 3: Διαμόρφωση και Προσαρμογή Σειρών

**Επισκόπηση:** Βελτιώστε την οπτική ελκυστικότητα των διαγραμμάτων σας προσαρμόζοντας τις ρυθμίσεις των σειρών, όπως ποικίλα χρώματα και στυλ σημείων.

#### Βήμα 4: Προσαρμογή Ρυθμίσεων Σειρών
Διαμορφώστε τα δεδομένα της σειράς, εφαρμόστε προσαρμοσμένη μορφοποίηση και προσαρμόστε τα σημεία:

```java
import com.aspose.cells.*;

public class FeatureSeriesConfiguration {
    public static void main(String[] args) throws Exception {
        // Instantiate a workbook
        Workbook workbook = new Workbook();
        
        // Access first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);
        
        // Add series to the chart
        Chart chart = worksheet.getCharts().add(ChartType.LINE_WITH_DATA_MARKERS, 1, 3, 20, 20).get(0);

        int s2_idx = chart.getNSeries().add("A2: A21", true);
        int s3_idx = chart.getNSeries().add("A22: A41", true);

        // Enable varied colors for series points
        chart.getNSeries().setColorVaried(true);

        // Customize first series marker styles and colors
        chart.getNSeries().get(s2_idx).getArea().setFormatting(FormattingType.CUSTOM);
        chart.getNSeries().get(s2_idx).getMarker().getArea().setForegroundColor(Color.getYellow());
        chart.getNSeries().get(s2_idx).getMarker().getBorder().setVisible(false);

        // Set X and Y values for the first series
        chart.getNSeries().get(s2_idx).setXValues("A2: A21");
        chart.getNSeries().get(s2_idx).setValues("B2: B21");

        // Customize second series marker styles and colors
        chart.getNSeries().get(s3_idx).getArea().setFormatting(FormattingType.CUSTOM);
        chart.getNSeries().get(s3_idx).getMarker().getArea().setForegroundColor(Color.getGreen());
        chart.getNSeries().get(s3_idx).getMarker().getBorder().setVisible(false);

        // Set X and Y values for the second series
        chart.getNSeries().get(s3_idx).setXValues("A22: A41");
        chart.getNSeries().get(s3_idx).setValues("B22: B41");
    }
}
```

### Λειτουργία 4: Αποθήκευση Βιβλίου Εργασίας

**Επισκόπηση:** Τέλος, αποθηκεύστε το βιβλίο εργασίας για να διατηρήσετε τις αλλαγές σας και να διασφαλίσετε ότι το διάγραμμα περιλαμβάνεται στο αρχείο Excel.

#### Βήμα 5: Αποθήκευση του Workbook
Αποθηκεύστε το βιβλίο εργασίας σας με τα νεοδημιουργημένα διαγράμματα:

```java
import com.aspose.cells.*;

public class FeatureWorkbookSaving {
    public static void main(String[] args) throws Exception {
        // Instantiate a workbook
        Workbook workbook = new Workbook();
        
        // Access first worksheet and add data, chart configuration as per previous steps...
        Worksheet worksheet = workbook.getWorksheets().get(0);
        // (Implementation of adding data and configuring the chart would be here)

        // Save the workbook to an Excel file
        workbook.save("StyledChart.xlsx");
    }
}
```

### Κοινά Προβλήματα και Αντιμετώπιση
- **Το διάγραμμα εμφανίζεται κενό:** Επαληθεύστε ότι οι περιοχές κελιών που χρησιμοποιούνται στο `setXValues` και `setValues` αναφέρονται σωστά σε γεμιστά κελιά.  
- **Τα χρώματα δεν εφαρμόζονται:** Βεβαιωθείτε ότι το `chart.getNSeries().setColorVaried(true)` καλείται πριν από την προσαρμογή μεμονωμένων σειρών.  
- **Σφάλματα άδειας:** Μια δοκιμαστική άδεια μπορεί να περιορίζει τον αριθμό των διαγραμμάτων· εγκαταστήστε πλήρη άδεια για να αφαιρέσετε τους περιορισμούς.

## Συχνές Ερωτήσεις

**Ε: Μπορώ να δημιουργήσω άλλους τύπους διαγραμμάτων (π.χ., ράβδους, πίτες) με το Aspose.Cells;**  
Α: Ναι, το Aspose.Cells υποστηρίζει μια μεγάλη γκάμα τύπων διαγραμμάτων· απλώς αντικαταστήστε το `ChartType.LINE_WITH_DATA_MARKERS` με την επιθυμητή τιμή enum.

**Ε: Χρειάζεται να κλείσω το βιβλίο εργασίας ή να απελευθερώσω πόρους;**  
Α: Η κλάση `Workbook` διαχειρίζεται αυτόματα τους πόρους, αλλά μπορείτε να καλέσετε `workbook.dispose()` σε εφαρμογές που τρέχουν για μεγάλο χρονικό διάστημα για να ελευθερώσετε μνήμη.

**Ε: Είναι δυνατόν να προσθέσω πολλαπλά διαγράμματα στο ίδιο φύλλο εργασίας;**  
Α: Απόλυτα—καλέστε `worksheet.getCharts().add(...)` για κάθε διάγραμμα που θέλετε να εισάγετε.

**Ε: Πώς εξάγω το αρχείο σε παλαιότερη μορφή Excel (XLS);**  
Α: Χρησιμοποιήστε `workbook.save("StyledChart.xls", SaveFormat.EXCEL_97_TO_2003);`.

**Ε: Θα διατηρήσει το διάγραμμα το στυλ του όταν ανοίξει στο Microsoft Excel;**  
Α: Ναι, το Aspose.Cells γράφει εγγενή αντικείμενα διαγράμματος Excel, έτσι ώστε όλα τα στυλ, τα χρώματα και τα σημεία να εμφανίζονται ακριβώς όπως ορίστηκαν.

---

**Τελευταία Ενημέρωση:** 2026-04-08  
**Δοκιμή Με:** Aspose.Cells 25.3 for Java  
**Συγγραφέας:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}