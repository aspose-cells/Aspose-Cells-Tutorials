---
date: 2025-12-06
description: Μάθετε πώς να προσθέτετε σειρές δεδομένων, να δημιουργείτε συνδυαστικούς
  τύπους διαγραμμάτων, να αποθηκεύετε το βιβλίο εργασίας Excel και να εξάγετε το διάγραμμα
  σε PNG με το Aspose.Cells for Java.
linktitle: Add data series to create combined chart using Aspose.Cells
second_title: Aspose.Cells Java Excel Processing API
title: Προσθήκη σειρών δεδομένων για τη δημιουργία συνδυαστικού διαγράμματος με χρήση
  του Aspose.Cells
url: /el/java/advanced-excel-charts/combined-chart-types/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Προσθήκη σειράς δεδομένων για δημιουργία συνδυαστικού διαγράμματος με χρήση Aspose.Cells

Σε αυτό το tutorial θα **προσθέσετε σειρά δεδομένων** σε ένα βιβλίο εργασίας Excel και θα μάθετε πώς να **δημιουργήσετε συνδυαστικούς τύπους διαγραμμάτων** με το Aspose.Cells for Java. Θα περάσουμε από κάθε βήμα — από τη ρύθμιση του βιβλίου εργασίας, την προσθήκη σειρών, την προσαρμογή του υπομνήματος, μέχρι τη **αποθήκευση του βιβλίου εργασίας Excel** και την εξαγωγή του **διαγράμματος σε PNG**. Στο τέλος, θα έχετε ένα έτοιμο προς χρήση συνδυαστικό διάγραμμα που μπορείτε να ενσωματώσετε σε αναφορές ή πίνακες ελέγχου.

## Quick Answers
- **Ποια βιβλιοθήκη δημιουργεί συνδυαστικά διαγράμματα;** Aspose.Cells for Java  
- **Πώς προσθέτω σειρά δεδομένων;** Use `chart.getNSeries().add(...)`  
- **Μπορώ να εξάγω το διάγραμμα ως εικόνα;** Yes, with `chart.toImage(...)` (PNG)  
- **Σε ποια μορφή αρχείου μπορώ να αποθηκεύσω το βιβλίο εργασίας;** Standard `.xlsx` (Excel)  
- **Χρειάζεται άδεια για παραγωγική χρήση;** A valid Aspose.Cells license is required  

## What is **add data series** in Aspose.Cells?
Η προσθήκη σειράς δεδομένων ενημερώνει το διάγραμμα ποιες κελιά περιέχουν τις τιμές που θέλετε να σχεδιάσετε. Κάθε σειρά μπορεί να αντιπροσωπεύει μια γραμμή, στήλη ή οποιονδήποτε άλλο τύπο διαγράμματος, και μπορείτε να τις συνδυάσετε για να δημιουργήσετε ένα **συνδυαστικό διάγραμμα**.

## Why create a **combined chart**?
Ένα συνδυαστικό διάγραμμα σας επιτρέπει να εμφανίσετε διαφορετικά σύνολα δεδομένων με διαφορετικές οπτικές αναπαραστάσεις (π.χ., σειρά γραμμής πάνω από σειρά στήλης) σε μία ενιαία προβολή. Αυτό είναι ιδανικό για σύγκριση τάσεων έναντι συνόλων, ανάδειξη συσχετίσεων ή παροχή πιο πλούσιων πληροφοριών σε συμπαγή μορφή.

## Prerequisites
- Java Development Kit (JDK) 8 ή νεότερο  
- Aspose.Cells for Java library (κατεβάστε από τον παρακάτω σύνδεσμο)  
- Βασική εξοικείωση με τη σύνταξη της Java και τις έννοιες του Excel  

## Getting Started

Πρώτα, κατεβάστε τη βιβλιοθήκη Aspose.Cells for Java από την επίσημη ιστοσελίδα:

[Κατεβάστε το Aspose.Cells for Java](https://releases.aspose.com/cells/java/)

Μόλις το JAR προστεθεί στο classpath του έργου σας, μπορείτε να αρχίσετε να δημιουργείτε το διάγραμμα.

### Step 1: Import Aspose.Cells classes
```java
import com.aspose.cells.*;
```

### Step 2: Create a new workbook
```java
Workbook workbook = new Workbook();
```

### Step 3: Access the first worksheet
```java
Worksheet worksheet = workbook.getWorksheets().get(0);
```

### Step 4: Add a combined chart object  
Θα ξεκινήσουμε με ένα διάγραμμα γραμμής και αργότερα θα προσθέσουμε άλλες σειρές για να επιτύχουμε το εφέ του **συνδυαστικού διαγράμματος**.
```java
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 0, 0, 20, 10);
Chart chart = worksheet.getCharts().get(chartIndex);
```

## Adding Data to the Chart

Τώρα που υπάρχει το αντικείμενο διαγράμματος, πρέπει να το τροφοδοτήσουμε με δεδομένα.

### Step 5: Define the data ranges and **add data series**
```java
Cells cells = worksheet.getCells();
chart.getNSeries().add("A1:A5", true);
chart.getNSeries().add("B1:B5", true);
```
> **Pro tip:** Η πρώτη παράμετρος (`"A1:A5"`) είναι το εύρος για την πρώτη σειρά, και η δεύτερη (`"B1:B5"`) δημιουργεί μια δεύτερη σειρά που θα συνδυαστεί με την πρώτη.

### Step 6: Set the category (X‑axis) data
```java
chart.getNSeries().setCategoryData("C1:C5");
```

## Customizing the Chart

Ένα καλό διάγραμμα λέει μια ιστορία. Ας του δώσουμε τίτλους, ετικέτες αξόνων και ένα σαφές υπόμνημα.

### Step 7: Set chart title and axis labels
```java
chart.getTitle().setText("Combined Chart Example");
chart.getCategoryAxis().getTitle().setText("Categories");
chart.getValueAxis().getTitle().setText("Values");
```

### Step 8: **Add legend chart** and adjust its position
```java
chart.getLegend().setPosition(LegendPositionType.BOTTOM);
chart.getLegend().setOverlay(true);
```

## Saving and Exporting the Chart

Μετά την προσαρμογή, θα θέλετε να **αποθηκεύσετε το βιβλίο εργασίας Excel** και επίσης να δημιουργήσετε μια εικόνα.

### Step 9: Save the workbook as an Excel file
```java
workbook.save("CombinedChart.xlsx");
```

### Step 10: Export the **chart to PNG**
```java
chart.toImage("CombinedChart.png", ImageFormat.getPng());
```
> Η μέθοδος `chart.toImage` **δημιουργεί εικόνες διαγράμματος Excel** που μπορούν να χρησιμοποιηθούν σε ιστοσελίδες, αναφορές ή email.

## Common Issues & Troubleshooting

| Issue | Solution |
|-------|----------|
| **Δεν εμφανίζονται δεδομένα** | Επαληθεύστε ότι τα εύρη κελιών (`A1:A5`, `B1:B5`, `C1:C5`) περιέχουν πραγματικά δεδομένα πριν δημιουργήσετε το διάγραμμα. |
| **Το υπόμνημα επικαλύπτει το διάγραμμα** | Ορίστε `chart.getLegend().setOverlay(false)` ή μετακινήστε το υπόμνημα σε διαφορετική θέση (π.χ., `RIGHT`). |
| **Το αρχείο εικόνας είναι κενό** | Βεβαιωθείτε ότι το διάγραμμα έχει τουλάχιστον μία σειρά και ότι η `chart.toImage` κλήθηκε μετά από όλες τις προσαρμογές. |
| **Η αποθήκευση προκαλεί εξαίρεση** | Ελέγξτε ότι έχετε δικαιώματα εγγραφής στον προορισμό και ότι το αρχείο δεν είναι ανοιχτό στο Excel. |

## Frequently Asked Questions

**Q: Πώς εγκαθιστώ το Aspose.Cells for Java;**  
A: Κατεβάστε το JAR από την επίσημη ιστοσελίδα και προσθέστε το στο classpath του έργου σας. Ο σύνδεσμος λήψης είναι: [Κατεβάστε το Aspose.Cells for Java](https://releases.aspose.com/cells/java/).

**Q: Μπορώ να δημιουργήσω άλλους τύπους διαγραμμάτων εκτός από γραμμή και στήλη;**  
A: Ναι, το Aspose.Cells υποστηρίζει ράβδο, πίτα, scatter, area και πολλούς άλλους τύπους διαγραμμάτων. Ανατρέξτε στην τεκμηρίωση API για την πλήρη λίστα.

**Q: Απαιτείται άδεια για παραγωγική χρήση;**  
A: Ναι, απαιτείται έγκυρη άδεια Aspose.Cells για παραγωγικές εγκαταστάσεις. Διατίθεται δωρεάν δοκιμαστική έκδοση για αξιολόγηση.

**Q: Πώς μπορώ να αλλάξω τα χρώματα κάθε σειράς;**  
A: Χρησιμοποιήστε `chart.getNSeries().get(i).setAreaColor(Color.getRed())` (ή παρόμοιο) μετά την προσθήκη των σειρών.

**Q: Πού μπορώ να βρω περισσότερα παραδείγματα κώδικα;**  
A: Πλήρης τεκμηρίωση και επιπλέον παραδείγματα είναι διαθέσιμα στην ιστοσελίδα αναφοράς του Aspose: [εδώ](https://reference.aspose.com/cells/java/).

---

**Τελευταία ενημέρωση:** 2025-12-06  
**Δοκιμάστηκε με:** Aspose.Cells for Java 24.12  
**Συγγραφέας:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
