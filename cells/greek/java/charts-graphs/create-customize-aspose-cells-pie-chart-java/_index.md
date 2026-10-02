---
date: '2026-09-27'
description: Μάθετε πώς να δημιουργήσετε διάγραμμα πίτας java χρησιμοποιώντας Aspose.Cells.
  Οδηγός βήμα‑βήμα για την προσαρμογή διαγράμματος πίτας Excel, τη ρύθμιση εξάρτησης
  Maven και τη δημιουργία επαγγελματικών διαγραμμάτων.
keywords:
- create pie chart java
- customize excel pie chart
- maven dependency aspose cells
lastmod: '2026-09-27'
og_description: Δημιουργήστε διάγραμμα πίτας java χρησιμοποιώντας Aspose.Cells για
  Java. Μάθετε πώς να προσαρμόσετε διάγραμμα πίτας Excel, να προσθέσετε εξάρτηση Maven
  και να δημιουργήσετε επαγγελματικά διαγράμματα σε λίγα λεπτά.
og_image_alt: Java code generating a customized pie chart in Excel with Aspose.Cells
og_title: Δημιουργήστε διάγραμμα πίτας java με Aspose.Cells – Πλήρης Οδηγός Java
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Learn how to create pie chart java using Aspose.Cells. Step‑by‑step
    guide to customize Excel pie chart, set up Maven dependency, and generate professional
    charts.
  headline: How to create pie chart java with Aspose.Cells
  type: TechArticle
- questions:
  - answer: Yes, repeat the chart‑creation steps for each data range; each chart is
      independent.
    question: Can I generate multiple pie charts in the same workbook?
  - answer: It does; set the chart type to `ChartType.PIE_3D` when adding the chart.
    question: Does Aspose.Cells support 3‑D pie charts?
  - answer: Use the `Workbook.setDefaultTheme` method before creating any charts.
    question: How do I apply a custom theme to all charts?
  - answer: Over 30 formats, including XLSX, CSV, PDF, and HTML.
    question: What file formats can I export the workbook to?
  - answer: Yes, a valid license removes evaluation watermarks and unlocks full functionality.
    question: Is a license required for commercial deployment?
  type: FAQPage
tags:
- Aspose.Cells
- Java charting
- Excel automation
- data visualization
title: Πώς να δημιουργήσετε διάγραμμα πίτας java με Aspose.Cells
url: /el/java/charts-graphs/create-customize-aspose-cells-pie-chart-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να δημιουργήσετε διάγραμμα πίτας java με Aspose.Cells

## Εισαγωγή
Η δημιουργία ενός **pie chart** προγραμματιστικά συχνά μοιάζει με γρίφο, ειδικά όταν χρειάζεστε λεπτομερή έλεγχο πάνω στα χρώματα, τα υπομνήματα και τους τίτλους. Σε αυτόν τον οδηγό θα μάθετε πώς να **create pie chart java** χρησιμοποιώντας το Aspose.Cells, και στη συνέχεια να προσαρμόσετε το διάγραμμα πίτας του Excel ώστε να ταιριάζει με το εμπορικό σας σήμα ή το στυλ αναφοράς. Θα περάσουμε από τη ρύθμιση του περιβάλλοντος, την πληρότητα των δεδομένων, τη δημιουργία του διαγράμματος και τις οπτικές προσαρμογές—όλα χωρίς να αφήσετε το Java IDE σας.

**Τι θα μάθετε**
- Προσθέστε την **Maven dependency Aspose.Cells** στο έργο σας.
- Δημιουργήστε ένα βιβλίο εργασίας, γεμίστε τα κελιά με δεδομένα και δημιουργήστε ένα διάγραμμα πίτας.
- Εφαρμόστε προσαρμοσμένα χρώματα, τίτλους και υπομνήματα στο διάγραμμα.
- Εξάγετε το βιβλίο εργασίας σε αρχείο XLSX έτοιμο για κοινή χρήση.

Πριν ξεκινήσετε, θα πρέπει να είστε άνετοι με τη βασική σύνταξη της Java και να έχετε εγκατεστημένο το Maven ή το Gradle.

## Γρήγορες απαντήσεις
- **Ποια βιβλιοθήκη δημιουργεί διαγράμματα πίτας στην Java;** Aspose.Cells for Java.
- **Χρειάζομαι άδεια;** Μια δωρεάν δοκιμή λειτουργεί για ανάπτυξη· απαιτείται πληρωμένη άδεια για παραγωγή.
- **Ποιες Maven συντεταγμένες απαιτούνται;** `com.aspose:aspose-cells:24.10`.
- **Μπορώ να αλλάξω τα χρώματα των τμημάτων;** Ναι, μέσω της μεθόδου `setAreaColor` σε κάθε σειρά.
- **Μπορεί το διάγραμμα να εξαχθεί σε XLSX;** Απόλυτα—απλώς καλέστε `workbook.save("output.xlsx")`.

## Τι είναι ένα διάγραμμα πίτας στο Excel;
Ένα διάγραμμα πίτας οπτικοποιεί μια μοναδική σειρά δεδομένων ως αναλογικά τμήματα ενός κύκλου, καθιστώντας εύκολη τη σύγκριση μερών ενός συνόλου. Η γωνία κάθε τμήματος αντιστοιχεί στην τιμή του σε σχέση με το σύνολο, επιτρέποντας γρήγορη κατανόηση της κατανομής μεταξύ κατηγοριών όπως μερίδιο αγοράς, κατανομή προϋπολογισμού ή δημογραφικά ποσοστά.

## Γιατί να χρησιμοποιήσετε το Aspose.Cells για να δημιουργήσετε ένα διάγραμμα πίτας java;
Το Aspose.Cells υποστηρίζει πάνω από 50 τύπους διαγραμμάτων και μπορεί να χειριστεί φύλλα εργασίας με έως ένα εκατομμύριο γραμμές χωρίς να φορτώνει ολόκληρο το αρχείο στη μνήμη. Αυτό το πλεονέκτημα απόδοσης σας επιτρέπει να δημιουργείτε μεγάλες αναφορές σε μέτριο υλικό, προσφέροντας λεπτομερή έλεγχο στην εμφάνιση του διαγράμματος, τη σύνδεση δεδομένων και τις μορφές εξαγωγής, καθιστώντας το ανώτερο σε σχέση με πολλές ανοιχτές βιβλιοθήκες.

## Προαπαιτούμενα
- **Java Development Kit (JDK)** 8 ή νεότερο.
- **IDE** όπως IntelliJ IDEA ή Eclipse.
- **Maven** ή **Gradle** για διαχείριση εξαρτήσεων.
- Μια **trial ή αγορασμένη άδεια Aspose.Cells**.

### Απαιτούμενες βιβλιοθήκες και εξαρτήσεις
Προσθέστε το Maven artifact του Aspose.Cells στο `pom.xml` σας:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

Ή το ισοδύναμο Gradle:

```gradle
implementation 'com.aspose:aspose-cells:25.3'
```

### Βήματα απόκτησης άδειας
Το Aspose.Cells for Java είναι εμπορικό, αλλά μπορείτε να ξεκινήσετε με μια δωρεάν δοκιμή. Επισκεφθείτε τη [purchase page](https://purchase.aspose.com/buy) για να αποκτήσετε ένα προσωρινό κλειδί άδειας.

## Ρύθμιση του Aspose.Cells για Java
Πρώτα, βεβαιωθείτε ότι η βιβλιοθήκη βρίσκεται στο classpath σας. Αφού προσθέσετε την εξάρτηση, μπορείτε να αρχικοποιήσετε το API όπως φαίνεται παρακάτω.

```java
import com.aspose.cells.Workbook;

// Initialize a new workbook instance
Workbook workbook = new Workbook();
```

## Οδηγός υλοποίησης

### Δημιουργία και διαμόρφωση βιβλίου εργασίας
Η κλάση `Workbook` αντιπροσωπεύει ολόκληρο το αρχείο Excel στη μνήμη.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
import com.aspose.cells.Cells;
import com.aspose.cells.ChartType;
import com.aspose.cells.Chart;
import com.aspose.cells.Series;
import com.aspose.cells.Color;
import com.aspose.cells.LegendPositionType;
import com.aspose.cells.SaveFormat;
```

#### Βήμα 1: δημιουργία ενός βιβλίου εργασίας
```java
// Creates an empty workbook instance to work with.
Workbook workbook = new Workbook();
```  
Αυτό δημιουργεί ένα νέο, κενό βιβλίο εργασίας που μπορείτε αμέσως να αρχίσετε να γεμίζετε.

### Πρόσβαση ή τροποποίηση κελιών φύλλου εργασίας
Ένα `Worksheet` αντιπροσωπεύει ένα μοναδικό φύλλο μέσα στο βιβλίο εργασίας, περιέχοντας κελιά, γραμμές και στήλες.  
Θα γράψετε τα δεδομένα που τροφοδοτούν το διάγραμμα πίτας σε ένα φύλλο εργασίας.

#### Βήμα 2: λήψη του πρώτου φύλλου εργασίας και των κελιών του
```java
// Access the first worksheet in the workbook.
Worksheet worksheet = workbook.getWorksheets().get(0);
Cells cells = worksheet.getCells();

// Put sample values used for a pie chart into specific cells.
cells.get("C3").putValue("India");
cells.get("C4").putValue("China");
cells.get("C5").parseNumber("United States", true, null);
cells.get("C6").setValue("Russia");
cells.get("C7").setValue("United Kingdom");
cells.get("C8").setValue("Others");

// Put percentage values for a pie chart into specific cells.
cells.get("D2").putValue("% of world population");
cells.get("D3").putValue(25);
cells.get("D4").putValue(30);
cells.get("D5").putValue(10);
cells.get("D6").putValue(13);
cells.get("D7").putValue(9);
cells.get("D8").putValue(13);
```  
Συμπληρώστε τα κελιά με ονόματα κατηγοριών και τιμές που θα καταναλώσει το διάγραμμα.

### Δημιουργία διαγράμματος πίτας
Τα αντικείμενα `Chart` οπτικοποιούν δεδομένα σε ένα φύλλο εργασίας και υποστηρίζουν διάφορους τύπους όπως πίτα, στήλη και γραμμή.

#### Βήμα 3: προσθήκη διαγράμματος πίτας στο φύλλο εργασίας
```java
// Create a pie chart in the worksheet.
int pieIdx = worksheet.getCharts().add(ChartType.PIE, 1, 6, 15, 14);
Chart pie = worksheet.getCharts().get(pieIdx);
```  

### Διαμόρφωση σειρών και δεδομένων διαγράμματος πίτας
Η κλάση `Series` ορίζει το εύρος δεδομένων και τη μορφοποίηση για ένα διάγραμμα, συνδέοντας κελιά του φύλλου εργασίας με οπτικά στοιχεία.

#### Βήμα 4: ορισμός σειράς για το διάγραμμα
```java
// Configure the series data range for the chart.
pie.getNSeries().add("D3:D8", true);
pie.getNSeries().setCategoryData("=Sheet1!$C$3:$C$8");

// Link the pie chart title to a cell containing the title text.
pie.getTitle().setLinkedSource("D2");
```  

### Διαμόρφωση εμφάνισης υπομνήματος και τίτλου διαγράμματος
Ένα `Legend` του διαγράμματος εμφανίζει τα ονόματα των σειρών και τα χρώματα, βοηθώντας τους αναγνώστες να ταυτοποιήσουν κάθε τμήμα.

#### Βήμα 5: προσαρμογή υπομνήματος και τίτλου διαγράμματος
```java
// Set legend position at bottom of the chart.
pie.getLegend().setPosition(LegendPositionType.BOTTOM);

// Set font properties for the chart title.
pie.getTitle().getFont().setName("Calibri");
pie.getTitle().getFont().setSize(18);
```  

### Προσαρμογή χρωμάτων σειρών διαγράμματος
Η μέθοδος `setAreaColor` ορίζει το χρώμα γεμίσματος ενός τμήματος σειράς διαγράμματος χρησιμοποιώντας τιμή RGB.

#### Βήμα 6: αλλαγή χρωμάτων τμημάτων πίτας
```java
import com.aspose.cells.Color;

// Access and customize colors of individual pie chart segments.
Series srs = pie.getNSeries().get(0);
srs.getPoints().get(0).getArea().setForegroundColor(Color.fromArgb(0, 246, 22, 219));
srs.getPoints().get(1).getArea().setForegroundColor(Color.fromArgb(0, 51, 34, 84));
srs.getPoints().get(2).getArea().setForegroundColor(Color.fromArgb(0, 46, 74, 44));
srs.getPoints().get(3).getArea().setForegroundColor(Color.fromArgb(0, 19, 99, 44));
srs.getPoints().get(4).getArea().setForegroundColor(Color.fromArgb(0, 208, 223, 7));
srs.getPoints().get(5).getArea().setForegroundColor(Color.fromArgb(0, 222, 69, 8));
```  

### Αυτόματη προσαρμογή στηλών και αποθήκευση βιβλίου εργασίας
Η μέθοδος `autoFitColumns` προσαρμόζει αυτόματα το πλάτος των στηλών ώστε να ταιριάζει στο περιεχόμενο των κελιών.

#### Βήμα 7: προσαρμογή πλάτους στηλών και αποθήκευση αρχείου
```java
// Autofit all columns.
worksheet.autoFitColumns();

// Define output directory placeholder path for saving the workbook.
String outDir = "YOUR_OUTPUT_DIRECTORY";

// Save the modified workbook to an Excel file in the specified directory.
workbook.save(outDir + "/CSOrSColorsPieChart_out.xlsx", SaveFormat.XLSX);
```  

## Συνηθισμένες περιπτώσεις χρήσης
- **Ανάλυση δημογραφικών:** Εμφάνιση κατανομής πληθυσμού ανά περιοχές.
- **Αναφορά μεριδίου αγοράς:** Οπτικοποίηση του μεριδίου κάθε ανταγωνιστή με μια ματιά.
- **Κατανομή προϋπολογισμού:** Ανάδειξη του πώς τα κεφάλαια διανέμονται μεταξύ τμημάτων.

## Σκέψεις απόδοσης
- Απελευθερώστε αντικείμενα (`workbook.dispose()`) όταν δεν χρειάζονται πια για να ελευθερώσετε τη φυσική μνήμη.
- Για τεράστιες συλλογές δεδομένων, χρησιμοποιήστε το `WorkbookDesigner` για ροή δεδομένων αντί να φορτώνετε τα πάντα ταυτόχρονα.
- Κάντε profiling με το Java Flight Recorder για να εντοπίσετε τυχόν bottlenecks στη δημιουργία διαγράμματος.

## Συχνές ερωτήσεις

**Q: Μπορώ να δημιουργήσω πολλαπλά διαγράμματα πίτας στο ίδιο βιβλίο εργασίας;**  
A: Ναι, επαναλάβετε τα βήματα δημιουργίας διαγράμματος για κάθε εύρος δεδομένων· κάθε διάγραμμα είναι ανεξάρτητο.

**Q: Υποστηρίζει το Aspose.Cells διαγράμματα πίτας 3‑Δ;**  
A: Ναι· ορίστε τον τύπο διαγράμματος σε `ChartType.PIE_3D` όταν προσθέτετε το διάγραμμα.

**Q: Πώς εφαρμόζω προσαρμοσμένο θέμα σε όλα τα διαγράμματα;**  
A: Χρησιμοποιήστε τη μέθοδο `Workbook.setDefaultTheme` πριν δημιουργήσετε οποιαδήποτε διαγράμματα.

**Q: Σε ποιες μορφές αρχείων μπορώ να εξάγω το βιβλίο εργασίας;**  
A: Πάνω από 30 μορφές, συμπεριλαμβανομένων των XLSX, CSV, PDF και HTML.

**Q: Απαιτείται άδεια για εμπορική χρήση;**  
A: Ναι, μια έγκυρη άδεια αφαιρεί τα υδατογραφήματα αξιολόγησης και ξεκλειδώνει πλήρη λειτουργικότητα.

## Συμπέρασμα
Τώρα έχετε μια πλήρη, ολοκληρωμένη συνταγή για **create pie chart java** με το Aspose.Cells. Ακολουθώντας τα παραπάνω βήματα μπορείτε να δημιουργήσετε επαγγελματικά διαγράμματα πίτας στο Excel, να προσαρμόσετε χρώματα και τίτλους και να τα ενσωματώσετε σε οποιοδήποτε pipeline αναφορών. Εξερευνήστε άλλους τύπους διαγραμμάτων—στήλη, γραμμή, ραδιογράφημα—για να διευρύνετε το εργαλείο οπτικοποίησης δεδομένων σας.

---

**Τελευταία ενημέρωση:** 2026-09-27  
**Δοκιμάστηκε με:** Aspose.Cells 24.10 for Java  
**Συγγραφέας:** Aspose

## Σχετικά μαθήματα

- [Προσαρμογή ετικετών δεδομένων διαγράμματος Excel χρησιμοποιώντας Aspose.Cells for Java: Οδηγός βήμα‑βήμα](/cells/java/charts-graphs/customize-chart-data-labels-aspose-cells-java/)
- [Δημιουργία δυναμικών διαγραμμάτων Excel με Aspose.Cells Java: Ολοκληρωμένος οδηγός για προγραμματιστές](/cells/java/charts-graphs/aspose-cells-java-dynamic-excel-charts/)
- [Δημιουργία και προσαρμογή βιβλίων εργασίας Excel χρησιμοποιώντας Aspose.Cells Java: Οδηγός βήμα‑βήμα](/cells/java/workbook-operations/create-customize-excel-workbooks-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}