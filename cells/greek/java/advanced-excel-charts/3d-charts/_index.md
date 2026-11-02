---
date: 2026-08-21
description: Μάθετε πώς να εξάγετε chart ως image και να δημιουργήσετε 3D pie charts
  σε Java με Aspose.Cells. Δημιουργήστε 3D bar charts, προσθέστε 3D charts στο Excel
  και αποθηκεύστε workbooks ως XLSX.
keywords:
- export chart as image
- 3d pie chart java
- 3d bar chart java
- save workbook as xlsx
- add 3d chart excel
lastmod: 2026-08-21
linktitle: Δημιουργήστε 3D Pie Chart Java
og_description: Εξαγωγή chart ως image και δημιουργία 3D pie charts σε Java χρησιμοποιώντας
  Aspose.Cells. Οδηγός βήμα‑βήμα για τη δημιουργία 3D bar και pie charts, την προσαρμογή
  τους και την αποθήκευση workbooks ως XLSX.
og_image_alt: Developer guide showing how to export a 3D chart as an image with Aspose.Cells
  for Java
og_title: Εξαγωγή chart ως image και δημιουργία 3D pie chart σε Java
schemas:
- author: Aspose
  dateModified: '2026-08-21'
  description: Learn how to export chart as image and create 3D pie charts in Java
    with Aspose.Cells. Generate 3D bar charts, add 3D charts to Excel, and save workbooks
    as XLSX.
  headline: How to export chart as image and create 3D pie chart in Java
  type: TechArticle
- questions:
  - answer: Use `chart.getNSeries().add()` for each series range and ensure the chart
      type remains 3‑D (e.g., `ChartType.BAR_3_D` or `ChartType.PIE_3_D`).
    question: How can I add multiple data series to a 3D chart?
  - answer: Yes, you can save the chart as PNG, JPEG, or PDF by calling the appropriate
      `chart.toImage()` overload or `workbook.save()` with an image or PDF format,
      satisfying the **convert chart png** requirement.
    question: Can I export 3D charts created with Aspose.Cells for Java to other formats?
  - answer: Aspose.Cells focuses on static Excel charts. For interactive web‑based
      3‑D visualizations, consider coupling Excel data with JavaScript libraries such
      as Three.js.
    question: Is it possible to create interactive 3D charts with Aspose.Cells for
      Java?
  - answer: Absolutely. Load new data into the worksheet programmatically and refresh
      the chart range; the next time the workbook is opened, the chart reflects the
      updated values.
    question: Can I automate the process of updating data in my 3D charts?
  - answer: 'You can find comprehensive documentation and resources for Aspose.Cells
      for Java at the website: [Aspose.Cells for Java Documentation](https://reference.aspose.com/cells/java/).'
    question: Where can I find more resources and documentation for Aspose.Cells for
      Java?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- export chart as image
- 3d pie chart
- Aspose.Cells Java
- Excel chart automation
title: Πώς να εξάγετε chart ως image και να δημιουργήσετε 3D pie chart σε Java
url: /el/java/advanced-excel-charts/3d-charts/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία 3D διαγράμματος πίτας Java

## Εισαγωγή στα 3D διαγράμματα

Aspose.Cells for Java είναι ένα ισχυρό Java API για εργασία με αρχεία Excel και καθιστά εύκολο να **create 3d pie chart** έργα καθώς και κλασικές 3‑D οριζόντιες απεικονίσεις. Σε αυτό το tutorial θα δείτε ακριβώς πώς να **export chart as image**, να δημιουργήσετε ένα 3‑D bar chart, να προσαρμόσετε την ίδια προσέγγιση για ένα 3‑D pie chart, να προσαρμόσετε την εμφάνιση και τελικά να **add 3d chart excel** αρχεία στις αναφορές σας. Είτε δημιουργείτε ένα οικονομικό ταμπλό, ένα φύλλο απόδοσης πωλήσεων ή οπτικοποιείτε επιστημονικά δεδομένα, τα παρακάτω βήματα θα σας δώσουν μια σταθερή βάση.

## Σύντομες απαντήσεις

- **Ποια βιβλιοθήκη χρειάζομαι;** Aspose.Cells for Java (latest version)  
- **Μπορώ να δημιουργήσω ένα 3D bar chart;** Yes – use `ChartType.BAR_3_D`  
- **Χρειάζομαι άδεια;** A valid license removes evaluation limits  
- **Ποιες εκδόσεις του Excel υποστηρίζονται;** All major versions from 2003 to 2023  
- **Είναι δυνατόν να εξάγετε το διάγραμμα ως εικόνα;** Yes – call `chart.toImage()` after the chart is created  

## Τι είναι τα 3D διαγράμματα;

Τα 3D διαγράμματα προσθέτουν βάθος στις παραδοσιακές 2D απεικονίσεις, βοηθώντας τους θεατές να κατανοήσουν πολυδιάστατες σχέσεις πιο διαισθητικά. Είναι ιδιαίτερα χρήσιμα όταν χρειάζεται να συγκρίνετε πολλές κατηγορίες πλάι-πλάι διατηρώντας μια σαφή οπτική ιεραρχία. Προσθέτοντας μια τρίτη διάσταση, αυτά τα διαγράμματα μπορούν να αναδείξουν διαφορές στο μέγεθος που μπορεί να είναι λιγότερο εμφανείς σε επίπεδες αναπαραστάσεις, καθιστώντας τα σύνθετα δεδομένα πιο εύκολα στην ερμηνεία για επιχειρηματικούς ενδιαφερόμενους.

## Γιατί να χρησιμοποιήσετε Aspose.Cells for Java για τη δημιουργία 3D bar chart;

Aspose.Cells for Java παρέχει πάνω από 150 ενσωματωμένους τύπους διαγραμμάτων και υποστηρίζει 100+ συναρτήσεις Excel, προσφέροντας μια πλήρη μηχανή που λειτουργεί σε όλες τις εκδόσεις Excel από 2003 έως 2023 χωρίς την ανάγκη Microsoft Office. Αυτό σημαίνει ότι μπορείτε να **generate 3d bar chart** αντικείμενα προγραμματιστικά με προβλέψιμα αποτελέσματα και ελάχιστο κόστος.

## Ρύθμιση Aspose.Cells for Java

### Λήψη και εγκατάσταση

Μπορείτε να κατεβάσετε τη βιβλιοθήκη Aspose.Cells for Java από την επίσημη ιστοσελίδα. Ακολουθήστε τις οδηγίες Maven/Gradle ή προσθέστε το JAR απευθείας στο classpath του έργου σας.

### Αρχικοποίηση άδειας

Η κλάση `License` χρησιμοποιείται για την εφαρμογή της άδειας Aspose.Cells και την ενεργοποίηση της πλήρους λειτουργικότητας.  
```java
// Initialize Aspose.Cells license
License license = new License();
license.setLicense("path_to_license_file.xml");
```

## Δημιουργία βασικού 3D διαγράμματος

### Εισαγωγή απαραίτητων βιβλιοθηκών

Πρώτα, φέρτε τις απαιτούμενες κλάσεις στο πεδίο ορατότητας:  
```java
import com.aspose.cells.*;
```

### Αρχικοποίηση βιβλίου εργασίας

Δημιουργήστε ένα νέο workbook που θα φιλοξενήσει το διάγραμμα:  
```java
Workbook workbook = new Workbook();
```

### Προσθήκη δεδομένων στο διάγραμμα

Συμπληρώστε το φύλλο εργασίας με δείγμα δεδομένων που θα χρησιμοποιήσει το διάγραμμα:  
```java
Worksheet worksheet = workbook.getWorksheets().get(0);

// Adding data to cells
worksheet.getCells().get("A1").putValue("Category");
worksheet.getCells().get("A2").putValue("A");
worksheet.getCells().get("A3").putValue("B");
worksheet.getCells().get("A4").putValue("C");

worksheet.getCells().get("B1").putValue("Value");
worksheet.getCells().get("B2").putValue(10);
worksheet.getCells().get("B3").putValue(20);
worksheet.getCells().get("B4").putValue(30);
```

## Πώς να δημιουργήσετε 3D bar chart σε Java

Για να δημιουργήσετε ένα 3D bar chart, προσθέτετε ένα αντικείμενο διαγράμματος στο φύλλο, ορίζετε τον τύπο του σε `ChartType.BAR_3_D` και στη συνέχεια συνδέετε τις σειρές δεδομένων στα κελιά που περιέχουν τις τιμές σας. Μετά τη διαμόρφωση της εμφάνισης του διαγράμματος, μπορείτε να το αποδώσετε ή να το εξάγετε όπως χρειάζεται.  
```java
int chartIndex = worksheet.getCharts().add(ChartType.BAR_3_D, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);

// Setting the data range for the chart
chart.getNSeries().add("A2:B4", true);

// Customizing chart attributes
chart.getChartArea().getBorder().setVisible(false);
chart.getChartTitle().setText("3D Bar Chart");
```

## Αποθήκευση του διαγράμματος σε αρχείο

Τέλος, γράψτε το workbook (που τώρα περιέχει το 3‑D διάγραμμα) στο δίσκο. Αυτό επίσης **save workbook xlsx** σε τυπική μορφή Excel:  
```java
workbook.save("3D_Chart.xlsx");
```

## Πώς να δημιουργήσετε 3D pie chart με Aspose.Cells for Java

Αν χρειάζεστε μια οπτικοποίηση τύπου πίτας, η διαδικασία είναι σχεδόν η ίδια—απλώς αλλάζει το enum `ChartType`. Αντικαταστήστε το `ChartType.BAR_3_D` με `ChartType.PIE_3_D` όταν προσθέτετε το διάγραμμα και κατευθύνετε τις σειρές στα ίδια δεδομένα. Μετά τη δημιουργία του διαγράμματος μπορείτε να ορίσετε έναν περιγραφικό τίτλο, να προσαρμόσετε τα χρώματα των φέτας και να εξάγετε το αποτέλεσμα ως εικόνα. Αυτή η προσέγγιση σας επιτρέπει να επαναχρησιμοποιήσετε τον ίδιο κώδικα προετοιμασίας δεδομένων ενώ παρέχετε διαφορετική οπτική προοπτική.

## Πώς να εξάγετε το διάγραμμα ως εικόνα σε Java

Η μέθοδος `toImage` του αντικειμένου `Chart` αποθηκεύει το διάγραμμα ως αρχείο εικόνας. Μπορείτε να εξάγετε οποιοδήποτε 3D διάγραμμα σε raster εικόνα με μία κλήση: `chart.toImage("myChart.png", ImageFormat.getPng())`. Αυτή η μέθοδος αποδίδει το διάγραμμα ακριβώς όπως εμφανίζεται στο Excel, διατηρώντας το 3‑D βάθος, τα χρώματα και τις υπομνήματα, και γράφει το αποτέλεσμα στο καθορισμένο μονοπάτι αρχείου. Χρησιμοποιήστε PNG για απώλεια‑απαγόρευση ποιότητας ή JPEG για μικρότερα μεγέθη αρχείων όταν ενσωματώνετε την εικόνα σε διαδικτυακές αναφορές.

## Διαφορετικοί τύποι 3D διαγραμμάτων

Aspose.Cells for Java υποστηρίζει διάφορες παραλλαγές 3D διαγραμμάτων που μπορείτε να **add 3d chart excel** αρχεία με:

- **Bar charts** – ιδανικά για σύγκριση κατηγοριών.  
- **Pie charts** – δείχνουν αναλογικές συνεισφορές (συμπεριλαμβανομένου του 3D pie).  
- **Line charts** – απεικονίζουν τάσεις με την πάροδο του χρόνου.  
- **Area charts** – τονίζουν το μέγεθος της αλλαγής.

Μπορείτε να αλλάξετε το enum `ChartType` σε οποιονδήποτε από τους παραπάνω ενώ διατηρείτε το ίδιο μοτίβο δημιουργίας.

## Προηγμένη προσαρμογή διαγράμματος

### Προσθήκη τίτλων και ετικετών

Δώστε στο διάγραμμα πλαίσιο θέτοντας έναν περιγραφικό τίτλο και ετικέτες αξόνων.

### Προσαρμογή χρωμάτων και στυλ

Χρησιμοποιήστε τη μέθοδο `chart.getSeries().get(i).getArea().setForegroundColor(Color.getRGB(...))` για να ταιριάξετε το εταιρικό branding.

### Εργασία με άξονες διαγράμματος

Ρυθμίστε τις κλίμακες των αξόνων, τα διαστήματα και τα σημεία σήμανσης για βελτιωμένη αναγνωσιμότητα.

### Προσθήκη υπομνήματος

Ενεργοποιήστε τα υπομνήματα με `chart.getLegend().setVisible(true)` ώστε οι θεατές να μπορούν να αναγνωρίσουν κάθε σειρά δεδομένων.

### Εξαγωγή διαγραμμάτων ως εικόνες

Όταν χρειάζεστε μια στατική εικόνα για διαδικτυακή αναφορά, καλέστε `chart.toImage("chart.png", ImageFormat.getPng())`. Αυτό καλύπτει τη χρήση **convert chart png** χωρίς να αφήνει το workbook.

## Ενσωμάτωση δεδομένων

Aspose.Cells for Java μπορεί να αντλήσει δεδομένα από βάσεις δεδομένων, αρχεία CSV ή ζωντανά APIs. Απλώς συμπληρώστε τα κελιά του φύλλου εργασίας με τα ληφθέντα δεδομένα πριν συνδέσετε την περιοχή στο διάγραμμα. Αυτό διατηρεί τη ροή εργασίας **add 3d chart excel** δυναμική και ενημερωμένη.

## Συμπέρασμα

Σε αυτόν τον οδηγό περάσαμε από το πώς να **create 3d pie chart** και **create 3d bar chart** έργα από την αρχή μέχρι το τέλος—ρυθμίζοντας τη βιβλιοθήκη, προσθέτοντας δεδομένα, δημιουργώντας ένα 3‑D bar chart, προσαρμόζοντας τα ίδια βήματα για ένα 3‑D pie chart, και εφαρμόζοντας προχωρημένο styling. Με το Aspose.Cells for Java έχετε έναν αξιόπιστο, ανεξάρτητο από εκδόσεις τρόπο ενσωμάτωσης πλούσιων 3‑D οπτικοποιήσεων απευθείας σε βιβλία εργασίας Excel και ακόμη **export chart as image** για χρήση σε ταμπλό ή αναφορές.

## Συχνές ερωτήσεις

**Q: Πώς μπορώ να προσθέσω πολλαπλές σειρές δεδομένων σε ένα 3D διάγραμμα;**  
A: Χρησιμοποιήστε `chart.getNSeries().add()` για κάθε περιοχή σειράς και βεβαιωθείτε ότι ο τύπος του διαγράμματος παραμένει 3‑D (π.χ., `ChartType.BAR_3_D` ή `ChartType.PIE_3_D`).

**Q: Μπορώ να εξάγω 3D διαγράμματα που δημιουργήθηκαν με Aspose.Cells for Java σε άλλες μορφές;**  
A: Ναι, μπορείτε να αποθηκεύσετε το διάγραμμα ως PNG, JPEG ή PDF καλώντας την κατάλληλη υπερφόρτωση της `chart.toImage()` ή `workbook.save()` με μορφή εικόνας ή PDF, ικανοποιώντας την απαίτηση **convert chart png**.

**Q: Είναι δυνατόν να δημιουργήσετε διαδραστικά 3D διαγράμματα με Aspose.Cells for Java;**  
A: Το Aspose.Cells εστιάζει σε στατικά διαγράμματα Excel. Για διαδραστικές web‑based 3‑D οπτικοποιήσεις, σκεφτείτε τη σύνδεση των δεδομένων Excel με βιβλιοθήκες JavaScript όπως το Three.js.

**Q: Μπορώ να αυτοματοποιήσω τη διαδικασία ενημέρωσης των δεδομένων στα 3D διαγράμματά μου;**  
A: Απόλυτα. Φορτώστε νέα δεδομένα στο φύλλο εργασίας προγραμματιστικά και ανανεώστε την περιοχή του διαγράμματος· την επόμενη φορά που θα ανοίξει το workbook, το διάγραμμα θα αντανακλά τις ενημερωμένες τιμές.

**Q: Πού μπορώ να βρω περισσότερους πόρους και τεκμηρίωση για το Aspose.Cells for Java;**  
A: Μπορείτε να βρείτε πλήρη τεκμηρίωση και πόρους για το Aspose.Cells for Java στην ιστοσελίδα: [Aspose.Cells for Java Documentation](https://reference.aspose.com/cells/java/).

**Last Updated:** 2026-08-21  
**Tested With:** Aspose.Cells for Java 24.12 (latest)  
**Author:** Aspose

## Σχετικά Μαθήματα

- [Create Pie Charts in Excel Using Aspose.Cells for Java: A Comprehensive Guide](/cells/java/charts-graphs/master-pie-chart-creation-excel-aspose-cells-java/)
- [aspose cells java – Create Excel Chart with Annotations](/cells/java/advanced-excel-charts/chart-annotations/)
- [Add Data Labels to Excel Chart with Aspose.Cells Java](/cells/java/advanced-excel-charts/chart-interactivity/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}