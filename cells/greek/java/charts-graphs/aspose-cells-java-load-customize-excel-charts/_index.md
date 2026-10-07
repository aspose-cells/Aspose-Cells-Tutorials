---
date: '2026-06-12'
description: Μάθετε πώς να εξάγετε διάγραμμα σε PNG με Aspose.Cells Java, να δημιουργείτε
  εικόνες διαγραμμάτων, να αποδίδετε διαγράμματα Excel ως PNG και να προσαρμόζετε
  τις απεικονίσεις αποτελεσματικά.
keywords:
- export chart to png
- java generate chart image
- render excel chart image
- java chart visualization library
- Aspose.Cells Java
schemas:
- author: Aspose
  dateModified: '2026-06-12'
  description: Learn how to export chart to PNG with Aspose.Cells Java, generate chart
    images, render Excel charts as PNG, and customize visualizations efficiently.
  headline: Export chart to PNG using Aspose.Cells Java
  type: TechArticle
- description: Learn how to export chart to PNG with Aspose.Cells Java, generate chart
    images, render Excel charts as PNG, and customize visualizations efficiently.
  name: Export chart to PNG using Aspose.Cells Java
  steps:
  - name: Verify that **JDK 8** or newer is on your `PATH`.
    text: Verify that **JDK 8** or newer is on your `PATH`.
  - name: Open your preferred IDE and create a new Maven/Gradle Java project.
    text: Open your preferred IDE and create a new Maven/Gradle Java project.
  - name: Add the Aspose.Cells dependency using the snippets above.
    text: Add the Aspose.Cells dependency using the snippets above.
  - name: Add the Maven or Gradle dependency as shown earlier.
    text: Add the Maven or Gradle dependency as shown earlier.
  - name: Place your license file (`Aspose.Cells.lic`) in the project’s resources
      folder.
    text: Place your license file (`Aspose.Cells.lic`) in the project’s resources
      folder.
  - name: 'Load the license at runtime:'
    text: 'Load the license at runtime:'
  type: HowTo
- questions:
  - answer: Place the `Aspose.Cells.lic` file in the resources folder and load it
      with `License license = new License(); license.setLicense("Aspose.Cells.lic");`.
    question: How do I resolve license activation issues?
  - answer: Yes, it integrates seamlessly with Spring Boot, Jakarta EE, or any servlet
      container.
    question: Can I use Aspose.Cells for Java in a web application?
  - answer: Forgetting to update the source data before calling `calculate()` leads
      to stale visuals.
    question: What are common pitfalls when refreshing charts?
  - answer: Use `Workbook.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` and process
      worksheets in streams.
    question: How do I handle large Excel files efficiently?
  - answer: PNG, JPEG, BMP, and TIFF are fully supported; choose PNG for loss‑less
      quality.
    question: What image formats are supported for rendering charts?
  type: FAQPage
title: Εξαγωγή διαγράμματος σε PNG χρησιμοποιώντας Aspose.Cells Java
url: /el/java/charts-graphs/aspose-cells-java-load-customize-excel-charts/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή γραφήματος σε PNG χρησιμοποιώντας το Aspose.Cells Java

## Εισαγωγή

Η εξαγωγή ενός γραφήματος σε PNG είναι μια συνηθισμένη απαίτηση όταν χρειάζεται να ενσωματώσετε οπτικά δεδομένα σε αναφορές, παρουσιάσεις ή ιστοσελίδες. Με **Aspose.Cells for Java**, μπορείτε να φορτώσετε ένα υπάρχον βιβλίο εργασίας Excel, να ανανεώσετε τα δεδομένα του γραφήματος, να εφαρμόσετε ρυθμίσεις παγκοσμιοποίησης και να αποδώσετε το γράφημα απευθείας ως εικόνα PNG υψηλής ποιότητας — όλα χωρίς την ανάγκη εγκατάστασης του Microsoft Excel. Σε αυτό το μάθημα θα ανακαλύψετε πώς να **εξάγετε γράφημα σε PNG**, να δημιουργήσετε εικόνες γραφημάτων προγραμματιστικά και να προσαρμόσετε την έξοδο για παγκόσμια κοινά.

## Γρήγορες Απαντήσεις
- **Πώς μπορώ να εξάγω ένα γράφημα σε PNG;** Φορτώστε το βιβλίο εργασίας, αποκτήστε πρόσβαση στο γράφημα και καλέστε `chart.toImage()` με `ImageOrPrintOptions` ορισμένο σε PNG.  
- **Ποια βιβλιοθήκη υποστηρίζει τη δημιουργία εικόνων γραφημάτων σε Java;** Το Aspose.Cells for Java παρέχει πλήρη API για την απόδοση γραφημάτων Excel ως εικόνες.  
- **Χρειάζομαι άδεια για εξαγωγή PNG;** Μια δωρεάν δοκιμή λειτουργεί, αλλά μια εμπορική άδεια αφαιρεί τους περιορισμούς αξιολόγησης.  
- **Μπορώ να προσαρμόσω τις μορφές αριθμών παγκοσμίως;** Ναι, χρησιμοποιήστε `Workbook.getSettings().setGlobalizationSettings()` πριν από την απόδοση.  
- **Είναι το PNG η μόνη μορφή;** Όχι, μπορείτε επίσης να αποδώσετε σε JPEG, BMP ή TIFF αλλάζοντας την επιλογή μορφής εικόνας.

## Τι είναι το Aspose.Cells for Java;
`Aspose.Cells for Java` είναι μια **βιβλιοθήκη επεξεργασίας λογιστικών φύλλων βασισμένη σε Java** που επιτρέπει στους προγραμματιστές να δημιουργούν, τροποποιούν, μετατρέπουν και αποδίδουν αρχεία Excel χωρίς το Microsoft Office. Υποστηρίζει πάνω από 50 μορφές αρχείων, διαχειρίζεται βιβλία εργασίας με χιλιάδες γραμμές και μπορεί να αποδώσει γραφήματα σε εικόνες σε λιγότερο από ένα δευτερόλεπτο σε τυπικό εξοπλισμό διακομιστή.

## Γιατί να εξάγετε γράφημα σε PNG με το Aspose.Cells;
Η εξαγωγή γραφημάτων σε PNG με το Aspose.Cells προσφέρει υψηλή απόδοση, χαμηλή χρήση μνήμης και ευελιξία μορφών, ενώ εξαλείφει την ανάγκη για Microsoft Excel. Η βιβλιοθήκη αποδίδει γραφήματα σε λιγότερο από ένα δευτερόλεπτο, διατηρεί τη χρήση heap σε μέτρια επίπεδα και υποστηρίζει PNG, JPEG, BMP και TIFF, καθιστώντας την ιδανική για web, εκτύπωση και διασυνοριακές εφαρμογές.

## Προαπαιτούμενα

- **Aspose.Cells for Java** v25.3 (ή νεότερη).  
- **JDK 8+** εγκατεστημένο στο μηχάνημά σας.  
- **IDE** όπως IntelliJ IDEA ή Eclipse.  
- **Maven ή Gradle** για διαχείριση εξαρτήσεων.  

### Απαιτούμενες Βιβλιοθήκες και Εξαρτήσεις

**Maven**  
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```  

**Gradle**  
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```  

### Ρύθμιση Περιβάλλοντος

1. Επαληθεύστε ότι το **JDK 8** ή νεότερο βρίσκεται στο `PATH`.  
2. Ανοίξτε το προτιμώμενο IDE και δημιουργήστε ένα νέο Maven/Gradle Java έργο.  
3. Προσθέστε την εξάρτηση Aspose.Cells χρησιμοποιώντας τα παραπάνω αποσπάσματα.  

### Απόκτηση Άδειας

Aspose.Cells προσφέρει δωρεάν δοκιμή για αξιολόγηση των δυνατοτήτων του:

- [Λήψη Δωρεάν Δοκιμής](https://releases.aspose.com/cells/java/)  
- Για παραγωγική χρήση, αγοράστε άδεια στο [Purchase Aspose.Cells](https://purchase.aspose.com/buy).  
- Μπορείτε να ζητήσετε προσωρινή άδεια για εκτεταμένη δοκιμή.

## Ρύθμιση Aspose.Cells για Java

Μόλις το περιβάλλον σας είναι έτοιμο, αρχικοποιήστε το Aspose.Cells στο έργο σας:

1. Προσθέστε την εξάρτηση Maven ή Gradle όπως φαίνεται παραπάνω.  
2. Τοποθετήστε το αρχείο άδειας (`Aspose.Cells.lic`) στο φάκελο resources του έργου.  
3. Φορτώστε την άδεια κατά την εκτέλεση:

```java
   License license = new License();
   license.setLicense("path/to/Aspose.Total.Java.lic");
   ```  

## Οδηγός Υλοποίησης

Θα εξετάσουμε τρία βασικά σενάρια: φόρτωση & ανανέωση γραφήματος, προσαρμογή ρυθμίσεων παγκοσμιοποίησης και απόδοση του γραφήματος σε PNG.

### Πώς να εξάγετε γράφημα σε PNG με το Aspose.Cells Java;

Για να εξάγετε ένα γράφημα σε PNG με το Aspose.Cells for Java, πρώτα φορτώστε το βιβλίο εργασίας χρησιμοποιώντας την κλάση `Workbook`, στη συνέχεια ανακτήστε το επιθυμητό αντικείμενο `Chart` από το κατάλληλο φύλλο εργασίας. Διαμορφώστε το `ImageOrPrintOptions` ώστε να ορίσετε τη μορφή εικόνας σε PNG και, τέλος, καλέστε `chart.toImage(outputStream, options)`. Η προκύπτουσα ροή περιέχει ένα PNG υψηλής ποιότητας που μπορεί να αποθηκευτεί ή να σταλεί απευθείας σε πελάτη.

### Φόρτωση και Ανανέωση Γραφήματος από Αρχείο Excel

**Επισκόπηση**: Φορτώστε ένα υπάρχον βιβλίο εργασίας, βεβαιωθείτε ότι το γράφημα αντανακλά τα πιο πρόσφατα δεδομένα και προετοιμάστε το για απόδοση.

#### 1. Φόρτωση του Workbook  
```java
String dataDir = "YOUR_DATA_DIRECTORY";
Workbook book = new Workbook(dataDir + "sample.xlsx");
```  
*Definition anchor*: Η κλάση `Workbook` αντιπροσωπεύει ένα ολόκληρο αρχείο Excel στη μνήμη, παρέχοντας πρόσβαση σε φύλλα εργασίας, γραφήματα και κελιά.

#### 2. Πρόσβαση στο Worksheet και στο Chart  
```java
Worksheet sheet = book.getWorksheets().get(0);
Chart chart = sheet.getCharts().get(0);
```  
*Definition anchor*: Το αντικείμενο `Worksheet` παρέχει πρόσβαση σε γραμμές/στήλες, ενώ το αντικείμενο `Chart` περιλαμβάνει όλες τις ιδιότητες του γραφήματος.

#### 3. Ανανέωση του Γραφήματος  
```java
chart.calculate();
```  
Η κλήση `calculate()` αναγκάζει το γράφημα να επανυπολογίσει τις σειρές του βάσει τυχόν αλλαγμένων δεδομένων πηγής, εξασφαλίζοντας οπτική ακρίβεια.

### Προσαρμογή Ρυθμίσεων Παγκοσμιοποίησης για Γραφήματα

**Επισκόπηση**: Προσαρμόστε μορφές ημερομηνίας, ώρας και αριθμών ώστε να ταιριάζουν με τις περιφερειακές συμβάσεις πριν από την απόδοση.

#### 1. Φόρτωση του Workbook  
```java
Workbook book = new Workbook(dataDir + "sample.xlsx");
```  

#### 2. Ορισμός Προσαρμοσμένων Ρυθμίσεων Παγκοσμιοποίησης  
```java
CustomSettings customGlobalizationSettings = new CustomSettings();
customGlobalizationSettings.setChartSettings(new CustomChartGlobalizationSettings());
book.getSettings().setGlobalizationSettings(customGlobalizationSettings);
```  
Μπορείτε να ορίσετε πρότυπα ειδικά για την τοπική ρύθμιση, όπως `"dd-MMM-yyyy"` για ημερομηνίες ή `"#,##0.00"` για αριθμούς, διασφαλίζοντας ότι το εξαγόμενο PNG σέβεται τα τοπικά πρότυπα.

### Απόδοση Γραφήματος σε Εικόνα

**Επισκόπηση**: Μετατρέψτε το ανανεωμένο γράφημα σε αρχείο PNG που μπορεί να χρησιμοποιηθεί σε παρουσιάσεις, PDF ή ιστοσελίδες.

#### 1. Φόρτωση του Workbook και Πρόσβαση στο Chart  
```java
String outDir = "YOUR_OUTPUT_DIRECTORY";
Workbook book = new Workbook(dataDir + "sample.xlsx");
Worksheet sheet = book.getWorksheets().get(0);
Chart chart = sheet.getCharts().get(0);
chart.calculate();
```  

#### 2. Απόδοση σε Εικόνα  
```java
ImageOrPrintOptions options = new ImageOrPrintOptions();
chart.toImage(outDir + "CustomTextforOtherLabelofPieChart_out.png", options);
```  
Η μέθοδος `toImage()` γράφει το γράφημα σε ένα `java.io.OutputStream`. Ορίζοντας `ImageOrPrintOptions.setImageFormat(ImageFormat.png)`, λαμβάνετε ένα καθαρό αρχείο PNG.

## Πρακτικές Εφαρμογές

- **Business Reports** – Ενσωματώστε PNG γραφήματα σε PDF ή Word έγγραφα για διανομή σε ενδιαφερόμενους.  
- **Data Dashboards** – Ανανεώστε γραφήματα σε πραγματικό χρόνο καθώς έρχονται νέα δεδομένα, και στη συνέχεια αποδώστε σε PNG για γρήγορη παράδοση στο web.  
- **Global Compliance** – Εφαρμόστε τοπικές μορφές αριθμών και ημερομηνιών για να πληροίτε τις περιφερειακές κανονιστικές απαιτήσεις.

## Παρατηρήσεις Απόδοσης

- **Memory Management**: Χρησιμοποιήστε `Workbook.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` για μεγάλα αρχεία.  
- **Selective Refresh**: Καλέστε `chart.calculate()` μόνο στα γραφήματα των οποίων τα δεδομένα πηγής έχουν αλλάξει.  
- **Thread Safety**: Δημιουργήστε ένα ξεχωριστό `Workbook` ανά νήμα για να αποφύγετε προβλήματα ταυτόχρονης πρόσβασης.

## Κοινά Προβλήματα και Λύσεις

| Πρόβλημα | Λύση |
|----------|------|
| Δεν βρέθηκε η άδεια | Επαληθεύστε τη διαδρομή `Aspose.Cells.lic` και βεβαιωθείτε ότι βρίσκεται στο classpath. |
| Η έξοδος PNG είναι κενή | Επιβεβαιώστε ότι το γράφημα δεν είναι κρυφό και ότι έχει κληθεί `calculate()` πριν από την απόδοση. |
| Αργή απόδοση σε μεγάλα αρχεία | Ενεργοποιήστε το `MemorySetting.MEMORY_PREFERENCE` και αποδώστε μόνο το απαιτούμενο φύλλο εργασίας. |

## Συχνές Ερωτήσεις

**Ε: Πώς μπορώ να λύσω προβλήματα ενεργοποίησης άδειας;**  
Α: Τοποθετήστε το αρχείο `Aspose.Cells.lic` στο φάκελο resources και φορτώστε το με `License license = new License(); license.setLicense("Aspose.Cells.lic");`.

**Ε: Μπορώ να χρησιμοποιήσω το Aspose.Cells for Java σε εφαρμογή web;**  
Α: Ναι, ενσωματώνεται άψογα με Spring Boot, Jakarta EE ή οποιονδήποτε servlet container.

**Ε: Ποια είναι τα κοινά λάθη κατά την ανανέωση γραφημάτων;**  
Α: Η παράλειψη ενημέρωσης των δεδομένων πηγής πριν την κλήση `calculate()` οδηγεί σε παλαιά οπτικά στοιχεία.

**Ε: Πώς να διαχειριστώ μεγάλα αρχεία Excel αποδοτικά;**  
Α: Χρησιμοποιήστε `Workbook.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` και επεξεργαστείτε τα φύλλα εργασίας σε ροές.

**Ε: Ποιες μορφές εικόνας υποστηρίζονται για την απόδοση γραφημάτων;**  
Α: PNG, JPEG, BMP και TIFF υποστηρίζονται πλήρως· επιλέξτε PNG για απώλεια‑μη‑συμπιεσμένη ποιότητα.

## Πόροι

- **Τεκμηρίωση**: [Aspose.Cells Java API](https://reference.aspose.com/cells/java/)  
- **Λήψεις**: [Aspose.Cells Releases](https://releases.aspose.com/cells/java/)  
- **Αγορά και Άδειες**: [Buy Aspose.Cells](https://purchase.aspose.com/buy)  
- **Δωρεάν Δοκιμή**: [Get a Free Trial of Aspose.Cells](https://releases.aspose.com/cells/java/)  
- **Προσωρινή Άδεια**: [Request a Temporary License](https://purchase.aspose.com/temporary-license/)  
- **Υποστήριξη και Φόρουμ**: [Aspose Support Forum](https://forum.aspose.com/c/cells/9)

Με την εξοικείωση με αυτά τα βήματα, μπορείτε αξιόπιστα **εξάγετε γράφημα σε PNG** και να ενσωματώσετε υψηλής ποιότητας οπτικοποιήσεις σε οποιαδήποτε λύση βασισμένη σε Java.

---

**Τελευταία Ενημέρωση:** 2026-06-12  
**Δοκιμή με:** Aspose.Cells 25.3 for Java  
**Συγγραφέας:** Aspose  

{{< blocks/products/products-backtop-button >}}

## Σχετικά Μαθήματα

- [How to Export Excel Charts as SVG Using Aspose.Cells Java for Scalable Vector Graphics](/cells/java/charts-graphs/export-excel-charts-svg-aspose-cells-java/)
- [Export Excel Charts to PDF Using Aspose.Cells for Java: Custom Page Sizes Guide](/cells/java/charts-graphs/export-excel-charts-pdf-aspose-cells-java/)
- [How to Customize Excel Charts with Theme Colors Using Aspose.Cells Java](/cells/java/charts-graphs/customize-excel-charts-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

```text
// Direct answer (no code block needed here as per preservation rules)
```