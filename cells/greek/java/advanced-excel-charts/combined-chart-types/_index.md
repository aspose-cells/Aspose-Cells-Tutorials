---
date: 2026-09-02
description: Μάθετε πώς να εξάγετε διάγραμμα σε PNG, να προσθέσετε σειρά δεδομένων,
  να συνδυάσετε διάγραμμα γραμμής-στήλης, να αποθηκεύσετε το βιβλίο εργασίας ως XLSX
  και να προσθέσετε υπόμνημα διαγράμματος χρησιμοποιώντας το Aspose.Cells for Java.
keywords:
- export chart to png
- combine line and column chart
- save workbook as xlsx
- generate chart image java
lastmod: 2026-09-02
linktitle: Εξαγωγή διαγράμματος σε PNG και προσθήκη σειράς δεδομένων για συνδυαστικό
  διάγραμμα
og_description: Εξαγωγή διαγράμματος σε PNG με το Aspose.Cells for Java, συνδυασμός
  γραμμής και στήλης διαγράμματος, προσθήκη σειράς δεδομένων και αποθήκευση του βιβλίου
  εργασίας ως XLSX σε ένα ενιαίο tutorial.
og_image_alt: Developer guide showing combined line‑column chart export to PNG using
  Aspose.Cells for Java
og_title: Εξαγωγή διαγράμματος σε PNG και προσθήκη σειράς δεδομένων για συνδυαστικό
  διάγραμμα
schemas:
- author: Aspose
  dateModified: '2026-09-02'
  description: Learn how to export chart to PNG, add data series, combine line column
    chart, save workbook as XLSX and add legend chart using Aspose.Cells for Java.
  headline: Export chart to PNG and add data series for combined chart
  type: TechArticle
- description: Learn how to export chart to PNG, add data series, combine line column
    chart, save workbook as XLSX and add legend chart using Aspose.Cells for Java.
  name: Export chart to PNG and add data series for combined chart
  steps:
  - name: import aspose.cells classes
    text: '`Workbook` is Aspose.Cells’ core object that represents an entire Excel
      file in memory.'
  - name: create a new workbook
    text: '`Worksheet` represents a single sheet inside a `Workbook` and provides
      access to cells, rows, and charts.'
  - name: access the first worksheet
    text: '`Chart` is the object that holds all chart‑related settings, series, and
      rendering options.'
  - name: add a combined chart object to the worksheet
    text: We’ll start with a line chart and later add a column series to achieve a
      **combined line column chart** effect.
  - name: define the data ranges and add data series
    text: '`NSeries` is the collection that stores each data series for a chart. Adding
      a series links a range of cells to the chart. > **Pro tip:** The first parameter
      (`"A1:A5"`) is the range for the first series, and the second (`"B1:B5"`) creates
      a second series that will be combined with the first.'
  - name: set the category (X‑axis) data
    text: '`CategoryAxis` represents the horizontal axis of the chart, controlling
      the labels displayed along the X‑axis.'
  - name: set chart axis labels and title
    text: '`Title` sets the main title of the chart, and `Axis` objects represent
      the X and Y axes.'
  - name: add legend chart and adjust its position
    text: '`Legend` controls the placement and appearance of the series legend in
      the chart.'
  - name: save the workbook as an Excel file (XLSX)
    text: '`Workbook.save` writes the in‑memory workbook to a file in the specified
      format.'
  - name: export chart to PNG
    text: '`Chart.toImage` renders the chart as an image file in the chosen format.
      > The `chart.toImage` method **generates Excel chart** images that can be used
      in web pages, reports, or emails.'
  type: HowTo
- questions:
  - answer: 'Download the JAR from the official site and add it to your project’s
      classpath. The download link is: [Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/).'
    question: How do I install Aspose.Cells for Java?
  - answer: Yes, Aspose.Cells supports bar, pie, scatter, area, and many more chart
      types. Refer to the API documentation for the full list.
    question: Can I create other chart types besides line and column?
  - answer: A valid Aspose.Cells license is required for production deployments. A
      free trial is available for evaluation.
    question: Is a license required for production use?
  - answer: Use `chart.getNSeries().get(i).setAreaColor(Color.getRed())` (or similar)
      after adding the series.
    question: How can I change the colors of each series?
  - answer: 'Comprehensive documentation and additional samples are available at the
      Aspose reference site: [Aspose Cells Java reference documentation](https://reference.aspose.com/cells/java/).'
    question: Where can I find more code examples?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- export chart to png
- Aspose.Cells
- Java Excel charts
title: Εξαγωγή διαγράμματος σε PNG και προσθήκη σειράς δεδομένων για συνδυαστικό διάγραμμα
url: /el/java/advanced-excel-charts/combined-chart-types/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή διαγράμματος σε PNG και προσθήκη σειράς δεδομένων για συνδυαστικό διάγραμμα

Σε αυτό το μάθημα θα **προσθέσετε σειρά δεδομένων** σε ένα βιβλίο εργασίας Excel, θα **συνδυάσετε στοιχεία γραμμικού και στήλης διαγράμματος**, και θα μάθετε πώς να **εξάγετε το διάγραμμα σε PNG** χρησιμοποιώντας το Aspose.Cells for Java. Θα περάσουμε βήμα‑βήμα από τη δημιουργία του βιβλίου εργασίας, την προσθήκη του διαγράμματος σε ένα φύλλο εργασίας, την προσαρμογή της υπομνήσεως, μέχρι το **αποθήκευση του βιβλίου εργασίας ως XLSX** και τη δημιουργία εικόνας PNG του διαγράμματος. Στο τέλος, θα έχετε ένα έτοιμο συνδυαστικό διάγραμμα που μπορείτε να ενσωματώσετε σε αναφορές ή πίνακες ελέγχου.

## Γρήγορες απαντήσεις
- **Ποια βιβλιοθήκη δημιουργεί συνδυαστικά διαγράμματα;** Aspose.Cells for Java.  
- **Πώς προσθέτω μια σειρά δεδομένων;** Κλήση `chart.getNSeries().add(...)` με το κατάλληλο εύρος.  
- **Πώς μπορώ να εξάγω το διάγραμμα σε PNG;** Χρήση `chart.toImage("chart.png", ImageFormat.getPng())`.  
- **Σε ποια μορφή αρχείου μπορώ να αποθηκεύσω το βιβλίο εργασίας;** Standard `.xlsx` (αποθήκευση βιβλίου εργασίας ως XLSX).  
- **Χρειάζομαι άδεια για παραγωγή;** Ναι – απαιτείται έγκυρη άδεια Aspose.Cells για παραγωγικές εγκαταστάσεις.

## Τι είναι η εξαγωγή διαγράμματος σε PNG στο Aspose.Cells;
Η εξαγωγή ενός διαγράμματος σε PNG δημιουργεί μια ραστερ εικόνα του διαγράμματος Excel που μπορεί να εμφανιστεί σε ιστοσελίδες, αναφορές ή email χωρίς να απαιτείται η εφαρμογή Excel. Αυτή η μέθοδος καταγράφει την ακριβή οπτική διάταξη, τα χρώματα και τα σημεία δεδομένων, παράγοντας ένα φορητό αρχείο εικόνας.

## Γιατί να δημιουργήσετε ένα συνδυαστικό διάγραμμα γραμμής‑στήλης;
Ένα συνδυαστικό διάγραμμα γραμμής‑στήλης σας επιτρέπει να εμφανίσετε διαφορετικά σύνολα δεδομένων με διαφορετικές οπτικές αναπαραστάσεις (π.χ., σειρά γραμμής πάνω σε σειρά στήλης) σε μία ενιαία προβολή. Αυτή η προσέγγιση είναι ιδανική για σύγκριση τάσεων με συνολικά ποσά, ανάδειξη συσχετίσεων ή παροχή πιο πλούσιων πληροφοριών διατηρώντας το οπτικό αποτύπωμα μικρό.

## Προαπαιτούμενα
- Java Development Kit (JDK) 8 ή νεότερο  
- Βιβλιοθήκη Aspose.Cells for Java (λήψη από τον παρακάτω σύνδεσμο)  
- Βασική εξοικείωση με τη σύνταξη Java και τις έννοιες του Excel  

## Έναρξη

Πρώτα, κατεβάστε τη βιβλιοθήκη Aspose.Cells for Java από τον επίσημο ιστότοπο:

[Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/)

Μόλις το JAR προστεθεί στο classpath του έργου σας, μπορείτε να αρχίσετε να δημιουργείτε το διάγραμμα.

### Βήμα 1: εισαγωγή κλάσεων aspose.cells
```java
import com.aspose.cells.*;
```

### Βήμα 2: δημιουργία νέου βιβλίου εργασίας
```java
Workbook workbook = new Workbook();
```

### Βήμα 3: πρόσβαση στο πρώτο φύλλο εργασίας
```java
Worksheet worksheet = workbook.getWorksheets().get(0);
```

### Βήμα 4: προσθήκη αντικειμένου συνδυαστικού διαγράμματος στο φύλλο εργασίας  
Θα ξεκινήσουμε με ένα διάγραμμα γραμμής και αργότερα θα προσθέσουμε μια σειρά στήλης για να επιτύχουμε το εφέ **συνδυαστικού διαγράμματος γραμμής‑στήλης**.  
```java
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 0, 0, 20, 10);
Chart chart = worksheet.getCharts().get(chartIndex);
```

## Προσθήκη δεδομένων στο διάγραμμα

Τώρα που υπάρχει το κοντέινερ του διαγράμματος, πρέπει να το τροφοδοτήσουμε με δεδομένα.

### Βήμα 5: ορισμός των περιοχών δεδομένων και προσθήκη σειράς δεδομένων
`NSeries` είναι η συλλογή που αποθηκεύει κάθε σειρά δεδομένων για ένα διάγραμμα. Η προσθήκη μιας σειράς συνδέει ένα εύρος κελιών με το διάγραμμα.  
```java
Cells cells = worksheet.getCells();
chart.getNSeries().add("A1:A5", true);
chart.getNSeries().add("B1:B5", true);
```
> **Συμβουλή:** Η πρώτη παράμετρος (`"A1:A5"`) είναι το εύρος για την πρώτη σειρά, και η δεύτερη (`"B1:B5"`) δημιουργεί μια δεύτερη σειρά που θα συνδυαστεί με την πρώτη.

### Βήμα 6: ορισμός των δεδομένων της κατηγορίας (άξονας X)
`CategoryAxis` αντιπροσωπεύει τον οριζόντιο άξονα του διαγράμματος, ελέγχοντας τις ετικέτες που εμφανίζονται κατά μήκος του άξονα X.  
```java
chart.getNSeries().setCategoryData("C1:C5");
```

## Προσαρμογή του διαγράμματος

Ένα καλό διάγραμμα λέει μια ιστορία. Ας του δώσουμε τίτλους, ετικέτες άξονα και μια σαφή υπόμνηση.

### Βήμα 7: ορισμός ετικετών άξονα και τίτλου διαγράμματος
`Title` ορίζει τον κύριο τίτλο του διαγράμματος, και τα αντικείμενα `Axis` αντιπροσωπεύουν τους άξονες X και Y.  
```java
chart.getTitle().setText("Combined Chart Example");
chart.getCategoryAxis().getTitle().setText("Categories");
chart.getValueAxis().getTitle().setText("Values");
```

### Βήμα 8: προσθήκη υπομνήσεως διαγράμματος και προσαρμογή θέσης
`Legend` ελέγχει τη θέση και την εμφάνιση της υπομνήσεως των σειρών στο διάγραμμα.  
```java
chart.getLegend().setPosition(LegendPositionType.BOTTOM);
chart.getLegend().setOverlay(true);
```

## Αποθήκευση και εξαγωγή του διαγράμματος

Μετά την προσαρμογή, θα θέλετε να **αποθηκεύσετε το βιβλίο εργασίας ως XLSX** και επίσης να δημιουργήσετε μια εικόνα.

### Βήμα 9: αποθήκευση του βιβλίου εργασίας ως αρχείο Excel (XLSX)
`Workbook.save` γράφει το βιβλίο εργασίας στη μνήμη σε ένα αρχείο στην καθορισμένη μορφή.  
```java
workbook.save("CombinedChart.xlsx");
```

### Βήμα 10: εξαγωγή διαγράμματος σε PNG
`Chart.toImage` αποδίδει το διάγραμμα ως αρχείο εικόνας στην επιλεγμένη μορφή.  
```java
chart.toImage("CombinedChart.png", ImageFormat.getPng());
```
> Η μέθοδος `chart.toImage` **δημιουργεί εικόνες διαγράμματος Excel** που μπορούν να χρησιμοποιηθούν σε ιστοσελίδες, αναφορές ή email.

## Κοινά προβλήματα & αντιμετώπιση

| Πρόβλημα | Λύση |
|-------|----------|
| **Δεν εμφανίζονται δεδομένα** | Επαληθεύστε ότι οι περιοχές κελιών (`A1:A5`, `B1:B5`, `C1:C5`) περιέχουν πραγματικά δεδομένα πριν δημιουργήσετε το διάγραμμα. |
| **Η υπόμνηση επικαλύπτει το διάγραμμα** | Ορίστε `chart.getLegend().setOverlay(false)` ή μετακινήστε την υπόμνηση σε διαφορετική θέση (π.χ., `RIGHT`). |
| **Το αρχείο εικόνας είναι κενό** | Βεβαιωθείτε ότι το διάγραμμα έχει τουλάχιστον μία σειρά και ότι το `chart.toImage` κλήθηκε μετά από όλες τις προσαρμογές. |
| **Η αποθήκευση προκαλεί εξαίρεση** | Ελέγξτε ότι έχετε δικαιώματα εγγραφής στον προορισμό και ότι το αρχείο δεν είναι ανοιχτό στο Excel. |

## Συχνές ερωτήσεις

**Π: Πώς εγκαθιστώ το Aspose.Cells for Java;**  
Α: Κατεβάστε το JAR από τον επίσημο ιστότοπο και προσθέστε το στο classpath του έργου σας. Ο σύνδεσμος λήψης είναι: [Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/).

**Π: Μπορώ να δημιουργήσω άλλους τύπους διαγραμμάτων εκτός από γραμμικά και στήλες;**  
Α: Ναι, το Aspose.Cells υποστηρίζει ράβδους, πίτες, διασπορά, περιοχές και πολλούς άλλους τύπους διαγραμμάτων. Ανατρέξτε στην τεκμηρίωση API για την πλήρη λίστα.

**Π: Απαιτείται άδεια για χρήση σε παραγωγή;**  
Α: Απαιτείται έγκυρη άδεια Aspose.Cells για παραγωγικές εγκαταστάσεις. Διατίθεται δωρεάν δοκιμαστική έκδοση για αξιολόγηση.

**Π: Πώς μπορώ να αλλάξω τα χρώματα κάθε σειράς;**  
Α: Χρησιμοποιήστε `chart.getNSeries().get(i).setAreaColor(Color.getRed())` (ή παρόμοια) μετά την προσθήκη της σειράς.

**Π: Πού μπορώ να βρω περισσότερα παραδείγματα κώδικα;**  
Α: Αναλυτική τεκμηρίωση και επιπλέον δείγματα είναι διαθέσιμα στον ιστότοπο αναφοράς Aspose: [Aspose Cells Java reference documentation](https://reference.aspose.com/cells/java/).

**Τελευταία ενημέρωση:** 2026-09-02  
**Δοκιμή με:** Aspose.Cells for Java τελευταία έκδοση  
**Συγγραφέας:** Aspose

## Σχετικά Μαθήματα

- [Πώς να προσθέσετε ετικέτες σε διαγράμματα Excel χρησιμοποιώντας Aspose.Cells for Java](/cells/java/charts-graphs/adding-labels-to-charts-aspose-cells-java-tutorial/)
- [Πώς να δημιουργήσετε διάγραμμα Excel με γραμμή τάσης και εξαγωγή σε εικόνα χρησιμοποιώντας Aspose.Cells for Java](/cells/java/advanced-excel-charts/trendline-analysis/)
- [Εξαγωγή διαγραμμάτων Excel σε PDF χρησιμοποιώντας Aspose.Cells for Java: Οδηγός προσαρμοσμένων μεγεθών σελίδας](/cells/java/charts-graphs/export-excel-charts-pdf-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}