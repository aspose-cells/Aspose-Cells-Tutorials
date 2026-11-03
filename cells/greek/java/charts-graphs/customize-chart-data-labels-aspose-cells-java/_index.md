---
date: '2026-10-17'
description: Μάθετε πώς να ορίσετε το shape των ετικετών δεδομένων γραφήματος Excel
  σε Java χρησιμοποιώντας το Aspose.Cells. Αυτός ο οδηγός σας δείχνει πώς να τροποποιήσετε
  τις ετικέτες γραφήματος Excel γρήγορα και αποδοτικά.
keywords:
- how to set shape
- modify excel chart labels
- customize chart data labels
- add data label shape
lastmod: '2026-10-17'
og_description: Μάθετε πώς να ορίσετε το shape των ετικετών δεδομένων γραφήματος Excel
  σε Java χρησιμοποιώντας το Aspose.Cells. Αυτός ο οδηγός βήμα‑βήμα σας βοηθά να τροποποιήσετε
  τις ετικέτες γραφήματος Excel γρήγορα.
og_image_alt: Guide showing how to set shape of Excel chart data labels using Aspose.Cells
  for Java
og_title: Πώς να ορίσετε το shape των ετικετών δεδομένων γραφήματος Excel σε Java
schemas:
- author: Aspose
  dateModified: '2026-10-17'
  description: Learn how to set shape of Excel chart data labels in Java using Aspose.Cells.
    This guide shows you how to modify Excel chart labels quickly and efficiently.
  headline: How to set shape of Excel chart data labels in Java
  type: TechArticle
- description: Learn how to set shape of Excel chart data labels in Java using Aspose.Cells.
    This guide shows you how to modify Excel chart labels quickly and efficiently.
  name: How to set shape of Excel chart data labels in Java
  steps:
  - name: load your workbook
    text: The `Workbook` class is Aspose.Cells' top‑level object that represents a
      single Excel file in memory. Use `new Workbook("input.xlsx")` to load the file
      you want to modify.
  - name: access the chart
    text: '`Worksheet` represents a single sheet within a workbook. `Worksheet ws
      = workbook.getWorksheets().get(0);` retrieves the first worksheet. `Chart` is
      an object that represents a chart embedded in a worksheet. `Chart chart = ws.getCharts().get(0);`
      obtains the first chart on that sheet.'
  - name: retrieve series and modify data labels
    text: '`Series` represents a data series plotted on a chart. Each `Series` object
      contains a `DataLabel` collection. `DataLabel` controls the appearance of a
      data label for a series. `DataLabelShapeType` is an enumeration of possible
      shapes for data labels. Call `series.getDataLabels().setShapeType(DataLab'
  - name: save your workbook
    text: After applying the shape, invoke `workbook.save("output.xlsx");` to write
      the changes back to disk.
  type: HowTo
- questions:
  - answer: Loop through each series in the chart and call `setShapeType` on the series’
      `DataLabel` object.
    question: How do I change the shape of multiple data labels at once?
  - answer: Yes. With proper memory management, it processes workbooks containing
      hundreds of thousands of rows without loading the entire file into memory.
    question: Can Aspose.Cells for Java handle large Excel files efficiently?
  - answer: Missing Maven dependencies, using an outdated library version, or providing
      an invalid license file are typical pitfalls.
    question: What are common issues when setting up Aspose.Cells?
  - answer: Set the shape type to `DataLabelShapeType.DEFAULT` to restore the original
      appearance.
    question: Is there a way to revert data label shapes to default?
  - answer: Iterate over `ws.getCharts()` and apply the same `setShapeType` logic
      to each chart’s series collection.
    question: How can I apply this customization to multiple charts in a workbook?
  type: FAQPage
tags:
- excel chart
- aspose.cells
- java chart customization
- data label shape
title: Πώς να ορίσετε το shape των ετικετών δεδομένων γραφήματος Excel σε Java
url: /el/java/charts-graphs/customize-chart-data-labels-aspose-cells-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Κατακτώντας την προσαρμογή διαγραμμάτων σε Java με Aspose.Cells: τροποποίηση σχήματος ετικετών δεδομένων

## Εισαγωγή

Η ενίσχυση της οπτικής ελκυστικότητας των διαγραμμάτων Excel είναι κρίσιμη όταν ετοιμάζετε αναφορές ή πίνακες ελέγχου, ειδικά αν χρησιμοποιείτε Java. Με το Aspose.Cells—μια ισχυρή βιβλιοθήκη για διαχείριση και επεξεργασία υπολογιστικών φύλλων—μπορείτε **πώς να ορίσετε σχήμα** των ετικετών δεδομένων του διαγράμματος με λίγες μόνο γραμμές κώδικα. Αυτό το εκπαιδευτικό υλικό θα σας καθοδηγήσει στη αλλαγή του σχήματος των ετικετών δεδομένων σε ένα διάγραμμα Excel χρησιμοποιώντας Aspose.Cells για Java. Στο τέλος, θα γνωρίζετε πώς να:

- Πρόσβαση και τροποποίηση ετικετών δεδομένων διαγράμματος
- Ορισμός προσαρμοσμένων σχημάτων για ετικέτες δεδομένων
- Αποθήκευση αλλαγών στο βιβλίο εργασίας σας

## Γρήγορες απαντήσεις
- **Ποια είναι η κύρια κλάση για εργασία με αρχεία Excel;** `Workbook` αντιπροσωπεύει ένα ολόκληρο αρχείο Excel στη μνήμη.  
- **Ποια μέθοδος ορίζει το σχήμα της ετικέτας;** `setShapeType(DataLabelShapeType shape)` σε ένα αντικείμενο `DataLabel`.  
- **Χρειάζομαι άδεια για ανάπτυξη;** Μια δωρεάν προσωρινή άδεια λειτουργεί για αξιολόγηση· απαιτείται πλήρης άδεια για παραγωγή.  
- **Μπορώ να εφαρμόσω το σχήμα σε πολλές σειρές;** Ναι—επανάληψη σε κάθε σειρά και κλήση του `setShapeType`.  
- **Είναι αυτή η προσέγγιση συμβατή με μεγάλα βιβλία εργασίας;** Το Aspose.Cells επεξεργάζεται βιβλία εργασίας με εκατοντάδες σελίδες χωρίς να φορτώνει ολόκληρο το αρχείο στη μνήμη.

## Τι σημαίνει πώς να ορίσετε σχήμα;
Η φράση **how to set shape** αναφέρεται στη διαμόρφωση του οπτικού περιγράμματος μιας ετικέτας δεδομένων διαγράμματος, όπως η μετατροπή ενός απλού ορθογωνίου σε ένα callout ή έλλειψη. Η αλλαγή του σχήματος βελτιώνει την αναγνωσιμότητα και τονίζει βασικά σημεία δεδομένων. Επιλέγοντας το κατάλληλο σχήμα, μπορείτε να κάνετε την ετικέτα να ξεχωρίζει, να ομαδοποιήσετε σχετικούς δείκτες ή να ταιριάξετε τις οδηγίες εταιρικής ταυτότητας, βελτιώνοντας έτσι τη συνολική αναγνωσιμότητα του διαγράμματος.

## Γιατί να χρησιμοποιήσετε το Aspose.Cells για προσαρμογή ετικετών διαγράμματος;
Το Aspose.Cells υποστηρίζει **πάνω από 50 μορφές εισόδου και εξόδου**—συμπεριλαμβανομένων των XLSX, CSV, ODS και PDF—και μπορεί να επεξεργαστεί βιβλία εργασίας που περιέχουν **έως 1 εκατομμύριο γραμμές** χωρίς εξάντληση μνήμης. Το API του επιτρέπει την προγραμματιστική τροποποίηση διαγραμμάτων, εξαλείφοντας την ανάγκη χειροκίνητων επεμβάσεων στο Excel και εξασφαλίζοντας συνεπή στυλ σε αυτοματοποιημένες αναφορές.

## Προαπαιτούμενα

- **Aspose.Cells for Java Library**: Απαιτείται η έκδοση 25.3 ή νεότερη.  
- **Java Development Environment**: Εγκατεστημένο JDK στο μηχάνημά σας.  
- **IDE Setup**: Χρησιμοποιήστε ένα IDE όπως IntelliJ IDEA ή Eclipse για τη συγγραφή και εκτέλεση του κώδικά σας.

### Απαιτούμενες βιβλιοθήκες και εξαρτήσεις

Για χρήστες Maven, συμπεριλάβετε την ακόλουθη εξάρτηση στο `pom.xml` σας:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

Οι χρήστες Gradle πρέπει να προσθέσουν αυτό στο αρχείο `build.gradle` τους:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### Απόκτηση άδειας

Το Aspose.Cells προσφέρει δωρεάν δοκιμαστική άδεια, την οποία μπορείτε να αποκτήσετε από τη [σελίδα προσωρινής άδειας Aspose](https://purchase.aspose.com/temporary-license/). Αυτό παρέχει πλήρη πρόσβαση σε όλες τις λειτουργίες χωρίς περιορισμούς για περιορισμένο χρόνο.

## Ρύθμιση Aspose.Cells για Java

Μόλις το περιβάλλον σας είναι έτοιμο, ας ρυθμίσουμε το Aspose.Cells. Δείτε πώς να ξεκινήσετε:

### Βήματα εγκατάστασης

1. **Κατεβάστε τη βιβλιοθήκη**: Χρησιμοποιήστε Maven ή Gradle όπως φαίνεται παραπάνω.  
2. **Διαμόρφωση άδειας**:  
   - `License` είναι μια κλάση που εφαρμόζει το αρχείο άδειας Aspose.Cells για πλήρη λειτουργικότητα.  
   - Κατεβάστε και εφαρμόστε μια προσωρινή άδεια χρησιμοποιώντας αυτό το απόσπασμα κώδικα μετά την αρχικοποίηση του αντικειμένου `Workbook`:

    ```java
    License license = new License();
    license.setLicense("path/to/your/license/file");
    ```
3. **Βασική αρχικοποίηση**: Δημιουργήστε ένα στιγμιότυπο `Workbook` για να αρχίσετε να εργάζεστε με αρχεία Excel.

## Πώς να ορίσετε το σχήμα των ετικετών δεδομένων σε ένα διάγραμμα;

Φορτώστε το βιβλίο εργασίας σας, εντοπίστε το στοχευόμενο διάγραμμα και εφαρμόστε το επιθυμητό σχήμα στις ετικέτες δεδομένων του. Τα παρακάτω άμεσα βήματα το επιτυγχάνουν σε λιγότερο από ένα λεπτό.

### Οδηγός βήμα‑βήμα

#### Βήμα 1: φορτώστε το βιβλίο εργασίας σας

Η κλάση `Workbook` είναι το κορυφαίο αντικείμενο του Aspose.Cells που αντιπροσωπεύει ένα μόνο αρχείο Excel στη μνήμη. Χρησιμοποιήστε `new Workbook("input.xlsx")` για να φορτώσετε το αρχείο που θέλετε να τροποποιήσετε.

#### Βήμα 2: προσπελάστε το διάγραμμα

`Worksheet` αντιπροσωπεύει ένα φύλλο μέσα σε ένα βιβλίο εργασίας.  
`Worksheet ws = workbook.getWorksheets().get(0);` ανακτά το πρώτο φύλλο.  
`Chart` είναι ένα αντικείμενο που αντιπροσωπεύει ένα διάγραμμα ενσωματωμένο σε ένα φύλλο.  
`Chart chart = ws.getCharts().get(0);` παίρνει το πρώτο διάγραμμα σε αυτό το φύλλο.

#### Βήμα 3: ανακτήστε τις σειρές και τροποποιήστε τις ετικέτες δεδομένων

`Series` αντιπροσωπεύει μια σειρά δεδομένων που σχεδιάζεται σε ένα διάγραμμα.  
Κάθε αντικείμενο `Series` περιέχει μια συλλογή `DataLabel`.  
`DataLabel` ελέγχει την εμφάνιση μιας ετικέτας δεδομένων για μια σειρά.  
`DataLabelShapeType` είναι μια απαρίθμηση των πιθανών σχημάτων για ετικέτες δεδομένων.  
Καλέστε `series.getDataLabels().setShapeType(DataLabelShapeType.WEDGE_ELLIPSE_CALLOUT);` για να ορίσετε το σχήμα. Η απαρίθμηση παρέχει δεκάδες επιλογές, όπως `RECTANGLE`, `CLOUD` και `WEDGE_ELLIPSE_CALLOUT`.

#### Βήμα 4: αποθηκεύστε το βιβλίο εργασίας σας

Μετά την εφαρμογή του σχήματος, καλέστε `workbook.save("output.xlsx");` για να γράψετε τις αλλαγές στο δίσκο.

## Συμβουλές αντιμετώπισης προβλημάτων

- **Θέματα διαδρομής αρχείου**: Βεβαιωθείτε ότι η διαδρομή του αρχείου είναι απόλυτη ή σωστά σχετική με τον κατάλογο εργασίας του έργου σας.  
- **Ασυμφωνία έκδοσης βιβλιοθήκης**: Βεβαιωθείτε ότι χρησιμοποιείτε την έκδοση Aspose.Cells 25.3 ή νεότερη· οι παλαιότερες εκδόσεις δεν διαθέτουν τη μέθοδο `setShapeType`.  
- **Μη υποστηριζόμενοι τύποι διαγραμμάτων**: Ορισμένοι παλαιοί τύποι διαγραμμάτων (π.χ., radar) μπορεί να μην εκθέτουν ιδιότητες σχήματος ετικετών· μεταβείτε σε έναν υποστηριζόμενο τύπο όπως στήλη ή γραμμή.

## Πρακτικές εφαρμογές

1. **Οικονομική αναφορά** – Επισημάνετε τα βασικά περιθώρια κέρδους με ετικέτες σε στυλ callout.  
2. **Εκπαιδευτικό περιεχόμενο** – Χρησιμοποιήστε ετικέτες σε σχήμα σύννεφου για να τραβήξετε την προσοχή σε σημαντικά σημεία δεδομένων σε διδακτικό υλικό.  
3. **Αναλύσεις μάρκετινγκ** – Εφαρμόστε προσαρμοσμένα σχήματα για να διαφοροποιήσετε μετρικές απόδοσης καμπάνιας σε πίνακες ελέγχου.

Η ενσωμάτωση του Aspose.Cells με αγωγούς δεδομένων ή συστήματα CRM σας επιτρέπει να δημιουργείτε πλήρως μορφοποιημένες αναφορές αυτόματα, μειώνοντας την χειροκίνητη εργασία και εξασφαλίζοντας οπτικό περιεχόμενο σύμφωνο με την εταιρική ταυτότητα.

## Παράγοντες απόδοσης

Κατά την εργασία με μεγάλα αρχεία Excel:

- **Βελτιστοποίηση χρήσης μνήμης**: Καλέστε `workbook.dispose();` μετά την αποθήκευση για άμεση απελευθέρωση των εγγενών πόρων.  
- **Επεξεργασία σε παρτίδες**: Επεξεργαστείτε τα διαγράμματα σε ομάδες αντί για ένα‑προς‑ένα για ελαχιστοποίηση του κόστους δημιουργίας αντικειμένων.  
- **Αποτελεσματική διαχείριση δεδομένων**: Αποφύγετε βαριές υπολογιστικές λειτουργίες μέσα σε βρόχους που διατρέχουν χιλιάδες γραμμές· υπολογίστε τις τιμές εκ των προτέρων.

## Συμπέρασμα

Τώρα γνωρίζετε **πώς να ορίσετε σχήμα** των ετικετών δεδομένων διαγράμματος Excel σε Java χρησιμοποιώντας Aspose.Cells. Αυτή η δυνατότητα όχι μόνο ενισχύει την αισθητική των διαγραμμάτων αλλά και βελτιώνει την κατανόηση των δεδομένων από τους τελικούς χρήστες. Εξερευνήστε πρόσθετες επιλογές προσαρμογής—όπως χρώματα ετικετών, γραμματοσειρές και γραμμές οδηγού—για περαιτέρω βελτίωση των οπτικοποιήσεων σας.

Για οποιεσδήποτε ερωτήσεις ή βοήθεια, ανατρέξτε στο [φόρουμ υποστήριξης Aspose](https://forum.aspose.com/c/cells/9).

## Συχνές ερωτήσεις

**Ε: Πώς αλλάζω το σχήμα πολλαπλών ετικετών δεδομένων ταυτόχρονα;**  
Α: Επανάληψη σε κάθε σειρά του διαγράμματος και κλήση του `setShapeType` στο αντικείμενο `DataLabel` της σειράς.

**Ε: Μπορεί το Aspose.Cells για Java να διαχειριστεί μεγάλα αρχεία Excel αποδοτικά;**  
Α: Ναι. Με σωστή διαχείριση μνήμης, επεξεργάζεται βιβλία εργασίας που περιέχουν εκατοντάδες χιλιάδες γραμμές χωρίς να φορτώνει ολόκληρο το αρχείο στη μνήμη.

**Ε: Ποια είναι τα κοινά προβλήματα κατά τη ρύθμιση του Aspose.Cells;**  
Α: Ελλιπείς εξαρτήσεις Maven, χρήση παλαιάς έκδοσης βιβλιοθήκης ή παροχή μη έγκυρου αρχείου άδειας είναι τυπικά εμπόδια.

**Ε: Υπάρχει τρόπος να επαναφέρω τα σχήματα ετικετών στην προεπιλογή;**  
Α: Ορίστε τον τύπο σχήματος σε `DataLabelShapeType.DEFAULT` για να επαναφέρετε την αρχική εμφάνιση.

**Ε: Πώς μπορώ να εφαρμόσω αυτήν την προσαρμογή σε πολλαπλά διαγράμματα σε ένα βιβλίο εργασίας;**  
Α: Επανάληψη στο `ws.getCharts()` και εφαρμογή της ίδιας λογικής `setShapeType` στη συλλογή σειρών κάθε διαγράμματος.

## Πόροι

- [Τεκμηρίωση Aspose.Cells](https://reference.aspose.com/cells/java/)
- [Λήψη Aspose.Cells για Java](https://releases.aspose.com/cells/java/)
- [Αγορά άδειας](https://purchase.aspose.com/buy)
- [Δωρεάν δοκιμαστική άδεια](https://releases.aspose.com/cells/java/)
- [Προσωρινή άδεια](https://purchase.aspose.com/temporary-license/)

---  

**Τελευταία ενημέρωση:** 2026-10-17  
**Δοκιμασμένο με:** Aspose.Cells 25.3 for Java  
**Συγγραφέας:** Aspose  



```java
Workbook wb = new Workbook("YOUR_DATA_DIRECTORY/sampleSetShapeTypeOfDataLabelsOfChart.xlsx");
```
```java
Worksheet ws = wb.getWorksheets().get(0);
Chart ch = ws.getCharts().get(0);
```
```java
Series srs = ch.getNSeries().get(0);
srs.getDataLabels().setShapeType(DataLabelShapeType.WEDGE_ELLIPSE_CALLOUT);
```
```java
wb.save("YOUR_OUTPUT_DIRECTORY/outputSetShapeTypeOfDataLabelsOfChart.xlsx");
```

## Σχετικά μαθήματα

- [Τροποποίηση ετικετών δεδομένων διαγράμματος Excel χρησιμοποιώντας Aspose.Cells Java](/cells/java/charts-graphs/modify-excel-chart-data-labels-aspose-cells-java/)
- [Πώς να αλλάξετε το μέγεθος των ετικετών σε διαγράμματα Excel με Aspose.Cells για Java](/cells/java/charts-graphs/aspose-cells-java-auto-resize-chart-data-labels/)
- [Προσθήκη ετικετών σε διαγράμματα Excel με Aspose Cells για Java](/cells/java/charts-graphs/adding-labels-to-charts-aspose-cells-java-tutorial/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}