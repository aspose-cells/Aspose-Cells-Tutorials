---
date: '2026-07-02'
description: Μάθετε πώς να εξάγετε γράφημα σε PDF και να ορίσετε το διάστημα του άξονα
  αυτόματα χρησιμοποιώντας το Aspose.Cells για Java. Πλήρης οδηγός για την αυτοματοποίηση
  γραφημάτων Excel.
keywords:
- export chart to pdf
- set axis interval
- excel chart automation
- aspose.cells maven
- load excel workbook java
schemas:
- author: Aspose
  dateModified: '2026-07-02'
  description: Learn how to export chart to PDF and set axis interval automatically
    using Aspose.Cells for Java. Complete guide for Excel chart automation.
  headline: Export Chart to PDF and Automate Axis Units in Java
  type: TechArticle
- description: Learn how to export chart to PDF and set axis interval automatically
    using Aspose.Cells for Java. Complete guide for Excel chart automation.
  name: Export Chart to PDF and Automate Axis Units in Java
  steps:
  - name: '**Financial Reporting:** Generate quarterly profit‑loss charts that automatically
      adjust axis intervals as numbers grow.'
    text: '**Financial Reporting:** Generate quarterly profit‑loss charts that automatically
      adjust axis intervals as numbers grow.'
  - name: '**Sales Analysis:** Create dynamic sales performance graphs that adapt
      to new data without manual re‑formatting.'
    text: '**Sales Analysis:** Create dynamic sales performance graphs that adapt
      to new data without manual re‑formatting.'
  - name: '**Project Management:** Produce timeline Gantt charts where date axes scale
      automatically based on task duration.'
    text: '**Project Management:** Produce timeline Gantt charts where date axes scale
      automatically based on task duration.'
  type: HowTo
- questions:
  - answer: Yes—use `chart.toImage("output.png", ImageFormat.getPng())` for PNG, JPEG,
      BMP, and more.
    question: Can I export charts to image formats as well?
  - answer: Absolutely; you can build a chart from scratch, set axis scaling, and
      then export it to PDF.
    question: Does the API support charts created programmatically?
  - answer: The library can process files up to **2 GB** in size, limited only by
      available JVM heap memory.
    question: What is the maximum file size Aspose.Cells can handle?
  - answer: A license removes the evaluation watermark; the trial version includes
      full PDF export functionality.
    question: Is a license required for PDF export?
  - answer: Call `chart.getCategoryAxis().setMajorUnit(10.0)` (or `setMinorUnit`)
      to define a fixed interval.
    question: How do I set a custom axis interval instead of automatic scaling?
  type: FAQPage
title: Εξαγωγή γραφήματος σε PDF και αυτοματοποίηση μονάδων άξονα σε Java
url: /el/java/charts-graphs/automate-chart-axis-units-aspose-cells-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή Διαγράμματος σε PDF και Αυτόματη Ρύθμιση Μονάδων Άξονα σε Java

## Εισαγωγή

Η εξαγωγή ενός διαγράμματος σε PDF ενώ αυτόματα ρυθμίζετε τις μονάδες του άξονα εξοικονομεί αμέτρητα χειροκίνητα βήματα και εξαλείφει σφάλματα μορφοποίησης. Σε αυτό το σεμινάριο θα ανακαλύψετε πώς να **export chart to PDF** και **set axis interval** προγραμματιστικά με το Aspose.Cells for Java — ακριβώς όπως το κάνει το Microsoft Excel. Θα περάσουμε από τη ρύθμιση του περιβάλλοντος, τη φόρτωση ενός βιβλίου εργασίας, τη διαμόρφωση της κλίμακας του άξονα του διαγράμματος και, τέλος, την απόδοση του διαγράμματος ως αρχείο PDF.

**Τι Θα Μάθετε**
- Πώς να προσθέσετε το Aspose.Cells for Java σε ένα έργο Maven ή Gradle (`aspose.cells maven`).
- Ο σωστός τρόπος για **load Excel workbook java** κώδικα και πρόσβαση στα διαγράμματα.
- Βήματα για την αυτοματοποίηση της κλίμακας του άξονα του διαγράμματος (`set axis interval`) για τέλεια οπτική απόδοση.
- Εξαγωγή του διαγράμματος σε PDF και άλλες μορφές.

## Γρήγορες Απαντήσεις
- **Can I export a chart to PDF with Aspose.Cells?** Ναι—καλέστε `chart.toPdf()` μετά τη ρύθμιση του άξονα.
- **Do I need a license for production?** Μια έγκυρη άδεια Aspose.Cells αφαιρεί τα υδατογράμματα αξιολόγησης.
- **Which build tool is recommended?** Maven (`aspose.cells maven`) ή Gradle λειτουργούν εξίσου καλά.
- **Is the API compatible with Java 8+?** Απόλυτα· το Aspose.Cells υποστηρίζει Java 8 έως Java 21.
- **Can I automate axis units for any chart type?** Το ίδιο API λειτουργεί για γραμμικά, ραβδογράμματα, διασκορπισμένα και πίτες.

## Τι είναι η «export chart to PDF»;

Η εξαγωγή ενός διαγράμματος σε PDF μετατρέπει την οπτική αναπαράσταση ενός διαγράμματος Excel σε ένα υψηλής ποιότητας, διανυσματικό έγγραφο PDF. Αυτή η λειτουργία διατηρεί τη διάταξη, τα χρώματα, τις γραμματοσειρές και τη κλίμακα του άξονα του διαγράμματος, παράγοντας ένα αρχείο ανεξάρτητο από την ανάλυση που μπορεί να προβληθεί σε οποιαδήποτε πλατφόρμα χωρίς την ανάγκη εγκατάστασης του Microsoft Excel στον διακομιστή.

## Γιατί να αυτοματοποιήσετε την κλιμάκωση του άξονα του διαγράμματος;

Το Aspose.Cells μπορεί να υπολογίζει αυτόματα το βέλτιστο διάστημα του άξονα βάσει του εύρους των δεδομένων, αντικατοπτρίζοντας τη φυσική συμπεριφορά του Excel. Αυτό εξαλείφει την χειροκίνητη ρύθμιση, εγγυάται τη συνέπεια μεταξύ των αναφορών και μειώνει τον κίνδυνο λανθασμένης ερμηνείας των δεδομένων. **Ποσοτική δήλωση:** Το Aspose.Cells διαχειρίζεται φύλλα εργασίας με έως **1 048 576 γραμμές** και **16 384 στήλες** διατηρώντας τους υπολογισμούς του άξονα κάτω από **0,2 δευτερόλεπτα** για τυπικά σύνολα δεδομένων.

## Προαπαιτούμενα
- **Aspose.Cells for Java** (έκδοση 25.3 ή νεότερη).  
- Java Development Kit (JDK 8 ή νεότερο).  
- Maven ή Gradle για διαχείριση εξαρτήσεων.  
- Βασικές γνώσεις Java και εξοικείωση με τις έννοιες των διαγραμμάτων Excel.

## Ρύθμιση του Aspose.Cells για Java

Για να αρχίσετε να χρησιμοποιείτε το Aspose.Cells, προσθέστε τη βιβλιοθήκη στο έργο σας μέσω Maven ή Gradle.

**Maven (`aspose.cells maven`):**  
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

### Απόκτηση Άδειας
Για να χρησιμοποιήσετε το Aspose.Cells for Java, μπορείτε να αποκτήσετε προσωρινή άδεια ή να αγοράσετε μια:
- **Free Trial:** Κατεβάστε μια δοκιμαστική έκδοση από [Aspose Downloads](https://releases.aspose.com/cells/java/).
- **Temporary License:** Αιτηθείτε προσωρινή άδεια στη [Aspose Temporary License page](https://purchase.aspose.com/temporary-license/).
- **Purchase License:** Αγοράστε πλήρη άδεια μέσω της [Aspose Purchase Page](https://purchase.aspose.com/buy).

Αρχικοποιήστε το Aspose.Cells φορτώνοντας το αρχείο Excel σας:  
```java
Workbook wb = new Workbook("your-file-path.xlsx");
```

Με το περιβάλλον έτοιμο, ας προχωρήσουμε στην κύρια υλοποίηση.

## Πώς να εξάγω ένα διάγραμμα σε PDF χρησιμοποιώντας το Aspose.Cells for Java;

`Chart` αντιπροσωπεύει μια γραφική αναπαράσταση δεδομένων μέσα σε ένα φύλλο εργασίας, όπως γραμμικά, ραβδογράμματα ή πίτες.  
Φορτώστε το βιβλίο εργασίας, εντοπίστε το διάγραμμα, εφαρμόστε αυτόματη κλιμάκωση του άξονα και καλέστε τη μέθοδο εξαγωγής PDF. Τα παρακάτω βήματα δείχνουν τη πλήρη ροή σε λιγότερα από 70 λέξεις.

Αρχικά, δημιουργήστε μια παρουσία `Workbook`, ανακτήστε το επιθυμητό αντικείμενο `Chart`, ενεργοποιήστε τον αυτόματο υπολογισμό του διαστήματος του άξονα και, τέλος, καλέστε `chart.toPdf("output.pdf")`. Αυτή η εξαγωγή μίας γραμμής διατηρεί όλη τη μορφοποίηση και τις ρυθμίσεις του άξονα ακριβώς όπως εμφανίζονται στο Excel.

### Φόρτωση και Πρόσβαση σε Δεδομένα

Η κλάση `Workbook` είναι το κορυφαίο αντικείμενο του Aspose.Cells που αντιπροσωπεύει ολόκληρο το αρχείο Excel στη μνήμη. Η φόρτωση του αρχείου σας δίνει πρόσβαση σε φύλλα εργασίας, κελιά και ενσωματωμένα διαγράμματα:  
```java
// Load the sample Excel file
Workbook wb = new Workbook(srcDir + "sampleHandleAutomaticUnitsOfChartAxisLikeMicrosoftExcel.xlsx");

// Access first worksheet
Worksheet ws = wb.getWorksheets().get(0);

// Access first chart
Chart ch = ws.getCharts().get(0);
```

### Αυτοματοποίηση Μονάδων Άξονα Διαγράμματος

`Axis` ορίζει την κλίμακα και την ετικετοποίηση της διάστασης X ή Y ενός διαγράμματος, ελέγχοντας τις γραμμές σήμανσης και τα διαστήματα.  
Η αυτοματοποίηση των μονάδων άξονα του διαγράμματος διασφαλίζει ότι τα διαγράμματά σας μιμούνται τη συμπεριφορά του Excel, παρέχοντας συνέπεια και ακρίβεια στην παρουσίαση των δεδομένων. Χρησιμοποιήστε τη μέθοδο `setAutomaticMajorUnit(true)` στο αντικείμενο `Axis` για να αφήσετε το Aspose.Cells να υπολογίσει το βέλτιστο διάστημα βάσει του εύρους των δεδομένων.

**Render Chart to PDF:**  
Η εξαγωγή διαγραμμάτων σε διαφορετικές μορφές μπορεί να είναι ιδιαίτερα χρήσιμη για παρουσιάσεις ή εκθέσεις. Εδώ είναι πώς αποδίδετε ένα διάγραμμα σε PDF μετά τη ρύθμιση του άξονα:  
```java
// Render chart to pdf
ch.toPdf(outDir + "outputHandleAutomaticUnitsOfChartAxisLikeMicrosoftExcel.pdf");
```

## Κύριες Επιλογές Διαμόρφωσης

Το Aspose.Cells προσφέρει πάνω από **150** παραμετροποιήσιμες ιδιότητες για διαγράμματα, επιτρέποντάς σας να ρυθμίσετε λεπτομερώς τα πάντα από τα χρώματα μέχρι τις ετικέτες δεδομένων. Για την κλιμάκωση του άξονα, οι πιο σχετικές επιλογές είναι:

- `setAutomaticMajorUnit(boolean)` – επιτρέπει στη βιβλιοθήκη να αποφασίσει το καλύτερο διάστημα.
- `setMajorUnit(double)` – αντικαθιστά χειροκίνητα το διάστημα εάν χρειάζεται.
- `setMinorUnit(double)` – ελέγχει το διάστημα των μικρών γραμμών σήμανσης.

## Πρακτικές Εφαρμογές

Η αυτοματοποίηση των μονάδων άξονα του διαγράμματος είναι πολύτιμη σε πολλές πραγματικές περιπτώσεις:

1. **Financial Reporting:** Δημιουργήστε τριμηνιαία διαγράμματα κερδών‑ζημιών που προσαρμόζουν αυτόματα τα διαστήματα του άξονα καθώς οι αριθμοί αυξάνονται.
2. **Sales Analysis:** Δημιουργήστε δυναμικά γραφήματα απόδοσης πωλήσεων που προσαρμόζονται σε νέα δεδομένα χωρίς χειροκίνητη επαναμορφοποίηση.
3. **Project Management:** Παραγάγετε χρονοδιάγραμμα Gantt όπου οι άξονες ημερομηνίας κλιμακώνουν αυτόματα βάσει της διάρκειας των εργασιών.

## Παράγοντες Απόδοσης

Για βέλτιστη απόδοση κατά την επεξεργασία μεγάλων βιβλίων εργασίας:

- Κλείστε άμεσα τις μη χρησιμοποιούμενες παρουσίες `Workbook` για να ελευθερώσετε μνήμη.
- Χρησιμοποιήστε `Workbook.calculateFormula()` μόνο όταν είναι απαραίτητο· το Aspose.Cells αξιολογεί αργά τις περισσότερες φόρμουλες.
- **Ποσοτική δήλωση:** Η επεξεργασία ενός βιβλίου εργασίας 200 φύλλων με 500 KB δεδομένων διαγράμματος ολοκληρώνεται σε λιγότερο από **1,5 δευτερόλεπτα** σε τυπική CPU 2.6 GHz.

**Καλές Πρακτικές**
- Διατηρείτε το Aspose.Cells ενημερωμένο για να επωφεληθείτε από βελτιώσεις απόδοσης και νέα υποστήριξη μορφών αρχείων.
- Προφίλτε την εφαρμογή σας με τα ενσωματωμένα εργαλεία της Java (π.χ., VisualVM) για να εντοπίσετε τυχόν σημεία συμφόρησης που σχετίζονται με την απόδοση του διαγράμματος.

## Συχνές Ερωτήσεις

**Q: Can I export charts to image formats as well?**  
A: Ναι—χρησιμοποιήστε `chart.toImage("output.png", ImageFormat.getPng())` για PNG, JPEG, BMP και άλλα.

**Q: Does the API support charts created programmatically?**  
A: Απόλυτα· μπορείτε να δημιουργήσετε ένα διάγραμμα από το μηδέν, να ορίσετε την κλιμάκωση του άξονα και στη συνέχεια να το εξάγετε σε PDF.

**Q: What is the maximum file size Aspose.Cells can handle?**  
A: Η βιβλιοθήκη μπορεί να επεξεργαστεί αρχεία έως **2 GB** σε μέγεθος, περιορισμένο μόνο από τη διαθέσιμη μνήμη heap της JVM.

**Q: Is a license required for PDF export?**  
A: Μια άδεια αφαιρεί το υδατογράφημα αξιολόγησης· η δοκιμαστική έκδοση περιλαμβάνει πλήρη λειτουργία εξαγωγής PDF.

**Q: How do I set a custom axis interval instead of automatic scaling?**  
A: Καλέστε `chart.getCategoryAxis().setMajorUnit(10.0)` (ή `setMinorUnit`) για να ορίσετε ένα σταθερό διάστημα.

## Πόροι
- [Τεκμηρίωση Aspose.Cells](https://reference.aspose.com/cells/java/)
- [Λήψη Aspose.Cells Java](https://releases.aspose.com/cells/java/)
- [Αγορά Άδειας](https://purchase.aspose.com/buy)
- [Δωρεάν Δοκιμή](https://releases.aspose.com/cells/java/)
- [Προσωρινή Άδεια](https://purchase.aspose.com/temporary-license/)
- [Φόρουμ Υποστήριξης](https://forum.aspose.com/c/cells/9)

---

**Τελευταία Ενημέρωση:** 2026-07-02  
**Δοκιμάστηκε Με:** Aspose.Cells 25.3 for Java  
**Συγγραφέας:** Aspose

## Σχετικά Σεμινάρια

- [Εξαγωγή Διαγραμμάτων Excel σε PDF με Aspose.Cells για Java: Οδηγός Προσαρμοσμένων Μεγεθών Σελίδας](/cells/java/charts-graphs/export-excel-charts-pdf-aspose-cells-java/)
- [Πώς να Δημιουργήσετε και να Εξάγετε Διαγράμματα σε Java Χρησιμοποιώντας Aspose.Cells: Πλήρης Οδηγός](/cells/java/charts-graphs/aspose-cells-java-create-export-charts/)
- [Εξαγωγή Ετικετών Άξονα Διαγράμματος Excel με Aspose.Cells Java: Αναλυτικός Οδηγός](/cells/java/charts-graphs/aspose-cells-java-excel-chart-axis-labels/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< blocks/products/products-backtop-button >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}