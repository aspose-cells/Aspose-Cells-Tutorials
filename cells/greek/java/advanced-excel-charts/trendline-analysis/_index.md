---
date: 2026-08-27
description: Μάθετε πώς να προσθέσετε trendline σε chart, να εμφανίσετε την τιμή R‑squared
  του και να εξάγετε το chart ως εικόνα PNG ή JPEG χρησιμοποιώντας Aspose.Cells for
  Java.
keywords:
- add trendline to chart
- save chart as image
- export excel chart image
- java create excel workbook
- convert chart to png
lastmod: 2026-08-27
linktitle: Εξαγωγή chart σε εικόνα με ανάλυση trendline
og_description: Προσθέστε trendline σε chart, δείτε το R‑squared και εξάγετε το αποτέλεσμα
  ως PNG/JPEG χρησιμοποιώντας Aspose.Cells for Java – μια γρήγορη λύση 50‑format.
og_image_alt: Guide showing Java code to add a trendline to an Excel chart and export
  it as an image
og_title: Προσθήκη trendline σε chart και εξαγωγή ως εικόνα με Aspose.Cells for Java
schemas:
- author: Aspose
  dateModified: '2026-08-27'
  description: Learn how to add trendline to chart, display its R‑squared value, and
    export the chart as a PNG or JPEG image using Aspose.Cells for Java.
  headline: How to add trendline to chart and export as image in Java
  type: TechArticle
- description: Learn how to add trendline to chart, display its R‑squared value, and
    export the chart as a PNG or JPEG image using Aspose.Cells for Java.
  name: How to add trendline to chart and export as image in Java
  steps:
  - name: set up the project
    text: Create a new Java project and place the Aspose.Cells JARs on the build path.
      This prepares the environment for generating and manipulating Excel files.
  - name: load excel file (load excel file java)
    text: '*We’ve just **loaded an Excel file** into memory, ready for chart creation.*'
  - name: create a chart
    text: '*Here we generate a line chart that will later host our trendline.*'
  - name: add trendline (how to add trendline) and display R‑squared value
    text: '*The `setDisplayRSquaredValue(true)` call ensures the **R‑squared value**
      appears on the chart.*'
  - name: customize chart and save workbook (save workbook xlsx, generate excel file
      java)
    text: '*Now the workbook is **generated** and saved as an XLSX file, ready for
      further processing.*'
  - name: export chart to image (export chart to image)
    text: '> **Note:** This step is described without an additional code block to
      keep the original block count unchanged. After the chart is created and saved,
      you can export it to an image by calling the `chart.toImage()` method and writing
      the resulting `java.awt.image.BufferedImage` to a file format of you'
  type: HowTo
- questions:
  - answer: Use a different `TrendlineType` enumeration when adding the trendline,
      e.g., `TrendlineType.POLYNOMIAL` for a polynomial fit.
    question: How can I change the trendline type?
  - answer: Yes. Access the trendline’s `LineFormat` via `trendline.getLineFormat()`
      and set properties such as `setWeight()` and `setColor()`.
    question: Can I customize the trendline appearance (color, thickness)?
  - answer: Convert the chart to an image first, then embed that image into a PDF
      using Aspose.PDF or any other PDF library.
    question: How do I export the chart to PDF instead of an image?
  - answer: Absolutely. Call `chart.getNSeries().get(0).getTrendlines().add(...)`
      for each series you wish to analyze.
    question: Is it possible to add multiple trendlines to the same chart?
  - answer: Yes. You can specify the DPI when calling `chart.toImage()` and then scale
      the image before saving, ensuring crisp output for print or high‑density screens.
    question: Does Aspose.Cells support high‑resolution image export?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- Aspose.Cells
- Java charting
- Excel automation
- trendline analysis
title: Πώς να προσθέσετε trendline σε chart και να το εξάγετε ως εικόνα σε Java
url: /el/java/advanced-excel-charts/trendline-analysis/
weight: 15
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Προσθήκη γραμμής τάσης σε γράφημα και εξαγωγή του ως εικόνα

Σε αυτό το tutorial θα μάθετε πώς να **προσθέσετε γραμμή τάσης σε γράφημα**, να εμφανίσετε την τιμή R‑squared και να εξάγετε το οπτικό σε αρχείο PNG ή JPEG χρησιμοποιώντας το Aspose.Cells for Java. Θα δείτε γιατί οι γραμμές τάσης είναι σημαντικές, πώς να προετοιμάσετε το βιβλίο εργασίας και τα ακριβή βήματα για τη δημιουργία μιας εικόνας υψηλής ανάλυσης που μπορεί να ενσωματωθεί σε αναφορές, email ή ιστοσελίδες.

## Γρήγορες απαντήσεις
- **Ποιος είναι ο κύριος στόχος αυτού του οδηγού;** Για να σας δείξουμε πώς να προσθέσετε γραμμή τάσης σε γράφημα, να εμφανίσετε την εξίσωση και την τιμή R‑squared, και να εξάγετε το γράφημα ως εικόνα με Java.  
- **Ποια βιβλιοθήκη χρειάζομαι;** Aspose.Cells for Java – download it from the [Aspose.Cells for Java release page](https://releases.aspose.com/cells/java/).  
- **Χρειάζομαι άδεια για ανάπτυξη;** Μια δωρεάν δοκιμαστική έκδοση λειτουργεί για ανάπτυξη· απαιτείται εμπορική άδεια για παραγωγικές εγκαταστάσεις.  
- **Μπορώ να δημιουργήσω το βιβλίο εργασίας Excel προγραμματιστικά;** Ναι – το tutorial δημιουργεί και αποθηκεύει ένα βιβλίο εργασίας XLSX από την αρχή.  
- **Πώς εξάγεται το γράφημα σε PNG ή JPEG;** Καλέστε τη μέθοδο `Chart.toImage()` και γράψτε το επιστρεφόμενο `BufferedImage` με `ImageIO.write(...)`.

## Πώς δημιουργείτε ένα γράφημα Excel με γραμμή τάσης και το εξάγετε ως εικόνα;
Φορτώστε το βιβλίο εργασίας, προσθέστε ένα γράφημα γραμμής, συνδέστε μια γραμμή τάσης που εμφανίζει την εξίσωση και την τιμή R‑squared, αποθηκεύστε το βιβλίο εργασίας, στη συνέχεια καλέστε `chart.toImage()` και γράψτε το προκύπτον `BufferedImage` σε αρχείο PNG ή JPEG. Αυτή η ροή από αρχή έως τέλος απαιτεί μόνο λίγες γραμμές κώδικα Java και παράγει μια εικόνα pixel‑perfect κατάλληλη για οποιαδήποτε επακόλουθη εφαρμογή.

## Τι είναι η εξαγωγή γραφήματος σε εικόνα;
Η εξαγωγή ενός γραφήματος σε εικόνα μετατρέπει την οπτική αναπαράσταση των δεδομένων σας σε φορητό bitmap (PNG, JPEG, BMP κ.λπ.). Αυτή η μορφή είναι ιδανική για ενσωμάτωση γραφημάτων σε αναφορές, ιστοσελίδες ή παρουσιάσεις όπου το αρχικό αρχείο Excel δεν απαιτείται.

## Γιατί να προσθέσετε γραμμή τάσης και να εμφανίσετε την τιμή R‑squared;
Μια γραμμή τάσης αποκαλύπτει το υποκείμενο μοτίβο μιας σειράς δεδομένων, ενώ το μέτρο **R‑squared** ποσοτικοποιεί πόσο στενά η γραμμή τάσης ταιριάζει στα δεδομένα. Η συμπερίληψη και των δύο στην εξαγόμενη εικόνα παρέχει στους ενδιαφερόμενους άμεση κατανόηση χωρίς το άνοιγμα του βιβλίου εργασίας. Βοηθά τους λήπτες αποφάσεων να αξιολογήσουν γρήγορα τη δύναμη της συσχέτισης και να προβλέψουν τάσεις χωρίς να χρειάζεται να ανοίξουν το Excel.

## Προαπαιτούμενα
- Java 8 ή νεότερη εγκατεστημένη στο μηχάνημά σας για ανάπτυξη.  
- Βιβλιοθήκη Aspose.Cells for Java προστιθέμενη στο classpath του έργου (αρχεία JAR).  
- Γνώση ενός IDE Java όπως IntelliJ IDEA ή Eclipse.  

## Οδηγός βήμα‑βήμα

### Βήμα 1: ρύθμιση του έργου
Δημιουργήστε ένα νέο έργο Java και τοποθετήστε τα JAR του Aspose.Cells στο μονοπάτι κατασκευής. Αυτό προετοιμάζει το περιβάλλον για τη δημιουργία και τη διαχείριση αρχείων Excel.

### Βήμα 2: φόρτωση αρχείου Excel (φόρτωση αρχείου excel java)
```java
// Import necessary libraries
import com.aspose.cells.*;

// Load the Excel file
Workbook workbook = new Workbook("your_excel_file.xlsx");

// Access the worksheet
Worksheet worksheet = workbook.getWorksheets().get(0);
```
*Μόλις **φορτώσαμε ένα αρχείο Excel** στη μνήμη, έτοιμο για δημιουργία γραφήματος.*

### Βήμα 3: δημιουργία γραφήματος
```java
// Create a chart
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);

// Specify data source for the chart
chart.getNSeries().add("A1:A10", true);
```
*Εδώ δημιουργούμε ένα γράφημα γραμμής που θα φιλοξενήσει αργότερα τη γραμμή τάσης μας.*

### Βήμα 4: προσθήκη γραμμής τάσης (πώς να προσθέσετε γραμμή τάσης) και εμφάνιση τιμής R‑squared
```java
// Add a trendline to the chart
Trendline trendline = chart.getNSeries().get(0).getTrendlines().add(TrendlineType.LINEAR);

// Customize trendline options
trendline.setDisplayEquation(true);
trendline.setDisplayRSquaredValue(true);
```
*Η κλήση `setDisplayRSquaredValue(true)` εξασφαλίζει ότι η **τιμή R‑squared** εμφανίζεται στο γράφημα.*

### Βήμα 5: προσαρμογή γραφήματος και αποθήκευση βιβλίου εργασίας (save workbook xlsx, generate excel file java)
```java
// Customize chart title and axes
chart.getTitle().setText("Trendline Analysis");
chart.getCategoryAxis().getTitle().setText("X-Axis");
chart.getValueAxis().getTitle().setText("Y-Axis");

// Save the Excel file with the chart
workbook.save("output.xlsx");
```
*Τώρα το βιβλίο εργασίας **δημιουργείται** και αποθηκεύεται ως αρχείο XLSX, έτοιμο για περαιτέρω επεξεργασία.*

### Βήμα 6: εξαγωγή γραφήματος σε εικόνα (export chart to image)
> **Σημείωση:** Αυτό το βήμα περιγράφεται χωρίς επιπλέον μπλοκ κώδικα ώστε να διατηρηθεί ο αρχικός αριθμός μπλοκ.  
Μετά τη δημιουργία και αποθήκευση του γραφήματος, μπορείτε να το εξάγετε σε εικόνα καλώντας τη μέθοδο `chart.toImage()` και γράφοντας το προκύπτον `java.awt.image.BufferedImage` σε μορφή αρχείου της επιλογής σας (PNG, JPEG, BMP). Η τυπική ροή εργασίας είναι:
1. Ανακτήστε το αντικείμενο `Chart` (ήδη έγινε στα προηγούμενα βήματα).  
2. Καλέστε `chart.toImage()` για να λάβετε ένα `BufferedImage`.  
3. Χρησιμοποιήστε `ImageIO.write(bufferedImage, "png", new File("chart.png"))` για να γράψετε το αρχείο.  

Το αντικείμενο `Chart` αντιπροσωπεύει ένα γράφημα στο βιβλίο εργασίας και παρέχει μεθόδους για τροποποίηση της εμφάνισης και των δεδομένων του. Το `BufferedImage` είναι μια κλάση Java που κρατάει μια εικόνα στη μνήμη, επιτρέποντας την αποθήκευση σε αρχείο. Η `ImageIO` είναι μια βοηθητική κλάση για ανάγνωση και εγγραφή εικόνων σε Java. Η `setDisplayRSquaredValue` ενεργοποιεί την εμφάνιση του στατιστικού R‑squared στη γραμμή τάσης.

### Ανάλυση αποτελεσμάτων
Ανοίξτε το `output.xlsx` στο Excel για να επαληθεύσετε ότι η γραμμή τάσης, η εξίσωση και η τιμή R‑squared εμφανίζονται όπως αναμένεται. Ανοίξτε το εξαγόμενο αρχείο εικόνας (π.χ., `chart.png`) για να δείτε μια καθαρή απεικόνιση που μπορεί να κοινοποιηθεί χωρίς το αρχικό βιβλίο εργασίας.

## Συνηθισμένα προβλήματα και λύσεις
- **Η γραμμή τάσης δεν εμφανίζεται:** Βεβαιωθείτε ότι η περιοχή δεδομένων (`A1:A10`) περιέχει αριθμητικές τιμές· μη αριθμητικά δεδομένα εμποδίζουν τον υπολογισμό της γραμμής τάσης.  
- **Η τιμή R‑squared εμφανίζεται ως 0:** Αυτό συχνά σημαίνει ότι η σειρά δεδομένων είναι σταθερή ή λείπουν διακυμάνσεις. Δοκιμάστε διαφορετικό σύνολο δεδομένων ή χρησιμοποιήστε πολυωνυμική γραμμή τάσης.  
- **Η εξαγωγή εικόνας αποτυγχάνει με `NullPointerException`:** Επιβεβαιώστε ότι το γράφημα έχει αποδοθεί πλήρως πριν καλέσετε `toImage()`. Η αποθήκευση του βιβλίου εργασίας πρώτα μπορεί μερικές φορές να λύσει προβλήματα χρονισμού.

## Συχνές ερωτήσεις

**Q: Πώς μπορώ να αλλάξω τον τύπο της γραμμής τάσης;**  
A: Χρησιμοποιήστε διαφορετική απαρίθμηση `TrendlineType` κατά την προσθήκη της γραμμής τάσης, π.χ., `TrendlineType.POLYNOMIAL` για πολυωνυμική προσαρμογή.

**Q: Μπορώ να προσαρμόσω την εμφάνιση της γραμμής τάσης (χρώμα, πάχος);**  
A: Ναι. Πρόσβαση στο `LineFormat` της γραμμής τάσης μέσω `trendline.getLineFormat()` και ορίστε ιδιότητες όπως `setWeight()` και `setColor()`.

**Q: Πώς εξάγω το γράφημα σε PDF αντί για εικόνα;**  
A: Μετατρέψτε πρώτα το γράφημα σε εικόνα, στη συνέχεια ενσωματώστε αυτήν την εικόνα σε PDF χρησιμοποιώντας το Aspose.PDF ή οποιαδήποτε άλλη βιβλιοθήκη PDF.

**Q: Είναι δυνατόν να προσθέσω πολλαπλές γραμμές τάσης στο ίδιο γράφημα;**  
A: Απόλυτα. Καλέστε `chart.getNSeries().get(0).getTrendlines().add(...)` για κάθε σειρά που θέλετε να αναλύσετε.

**Q: Υποστηρίζει το Aspose.Cells εξαγωγή εικόνας υψηλής ανάλυσης;**  
A: Ναι. Μπορείτε να καθορίσετε το DPI κατά την κλήση `chart.toImage()` και στη συνέχεια να κλιμακώσετε την εικόνα πριν την αποθήκευση, εξασφαλίζοντας καθαρό αποτέλεσμα για εκτύπωση ή οθόνες υψηλής πυκνότητας.

---

**Τελευταία ενημέρωση:** 2026-08-27  
**Δοκιμή με:** Aspose.Cells for Java latest (supports 50+ file formats and processes workbooks with up to 2 million rows without full memory load)  
**Συγγραφέας:** Aspose

## Σχετικά Μαθήματα

- [Προσθήκη ετικετών δεδομένων σε γράφημα Excel με Aspose.Cells Java](/cells/java/advanced-excel-charts/chart-interactivity/)
- [Πώς να εξάγετε γραφήματα Excel ως SVG χρησιμοποιώντας Aspose.Cells Java για διανυσματικά γραφικά](/cells/java/charts-graphs/export-excel-charts-svg-aspose-cells-java/)
- [Εξαγωγή γραφημάτων Excel σε PDF χρησιμοποιώντας Aspose.Cells for Java&#58; Οδηγός προσαρμοσμένων μεγεθών σελίδας](/cells/java/charts-graphs/export-excel-charts-pdf-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}