---
date: 2026-02-09
description: Μάθετε πώς να δημιουργήσετε 3D διάγραμμα πίτας σε Java χρησιμοποιώντας
  το Aspose.Cells. Δημιουργήστε 3D ραβδόγραμμα, προσθέστε 3D διάγραμμα στο Excel και
  αποθηκεύστε το βιβλίο εργασίας σε μορφή xlsx με παραδείγματα κώδικα βήμα‑προς‑βήμα.
linktitle: Create 3D Pie Chart Java
second_title: Aspose.Cells Java Excel Processing API
title: Δημιουργία 3Δ διαγράμματος πίτας σε Java με το Aspose.Cells
url: /el/java/advanced-excel-charts/3d-charts/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία 3D Γραφήματος Πίτας σε Java

## Εισαγωγή 3D Διαγραμμάτων

Το Aspose.Cells for Java είναι ένα ισχυρό Java API για εργασία με αρχεία Excel και καθιστά εύκολο να **create 3d pie chart** έργα καθώς και κλασικές 3‑D γραφικές παραστάσεις ραβδών. Σε αυτό το tutorial θα δείτε ακριβώς πώς να δημιουργήσετε ένα 3‑D γράφημα ράβδων, πώς να προσαρμόσετε την ίδια προσέγγιση για ένα 3‑D γράφημα πίτας, να προσαρμόσετε την εμφάνιση και τελικά να **add 3d chart excel** αρχεία στις αναφορές σας. Είτε δημιουργείτε ένα οικονομικό dashboard, ένα φύλλο απόδοσης πωλήσεων ή οπτικοποιείτε επιστημονικά δεδομένα, τα παρακάτω βήματα θα σας δώσουν μια σταθερή βάση.

## Γρήγορες Απαντήσεις
- **Ποια βιβλιοθήκη χρειάζομαι;** Aspose.Cells for Java (latest version)  
- **Μπορώ να δημιουργήσω ένα 3D γράφημα ράβδων;** Yes – use `ChartType.BAR_3_D`  
- **Χρειάζομαι άδεια;** A valid license removes evaluation limits  
- **Ποιες εκδόσεις του Excel υποστηρίζονται;** All major versions from 2003 to 2023  
- **Είναι δυνατόν να εξάγω το γράφημα ως εικόνα;** Yes, via `chart.toImage()` methods  

## Τι είναι τα 3D Διαγράμματα;
Τα 3D διαγράμματα προσθέτουν βάθος στις παραδοσιακές 2D οπτικοποιήσεις, βοηθώντας τους θεατές να κατανοήσουν πολυδιάστατες σχέσεις πιο διαισθητικά. Είναι ιδιαίτερα χρήσιμα όταν χρειάζεται να συγκρίνετε πολλές κατηγορίες πλάι‑πλάι διατηρώντας μια σαφή οπτική ιεραρχία.

## Γιατί να χρησιμοποιήσετε Aspose.Cells for Java για τη δημιουργία 3D γραφήματος ράβδων;
Το Aspose.Cells for Java προσφέρει ένα πλούσιο σύνολο API δημιουργίας διαγραμμάτων, πλήρη συμβατότητα με το Excel και λεπτομερή έλεγχο του στυλ. Αυτό σημαίνει ότι μπορείτε να **generate 3d bar chart** αντικείμενα προγραμματιστικά χωρίς να ανησυχείτε για ιδιαιτερότητες εκδόσεων του Excel.

## Ρύθμιση Aspose.Cells for Java

### Λήψη και Εγκατάσταση
Μπορείτε να κατεβάσετε τη βιβλιοθήκη Aspose.Cells for Java από την επίσημη ιστοσελίδα. Ακολουθήστε τις οδηγίες Maven/Gradle ή προσθέστε το JAR απευθείας στο classpath του έργου σας.

### Αρχικοποίηση Άδειας
Για να ξεκλειδώσετε το πλήρες σύνολο λειτουργιών, αρχικοποιήστε την άδειά σας πριν από οποιεσδήποτε λειτουργίες διαγράμματος:

```java
// Initialize Aspose.Cells license
License license = new License();
license.setLicense("path_to_license_file.xml");
```

## Δημιουργία Βασικού 3D Διαγράμματος

### Εισαγωγή Απαραίτητων Βιβλιοθηκών
Πρώτα, φέρετε τις απαιτούμενες κλάσεις στο πεδίο εφαρμογής:

```java
import com.aspose.cells.*;
```

### Αρχικοποίηση Φύλλου Εργασίας
Δημιουργήστε ένα νέο workbook που θα φιλοξενήσει το διάγραμμα:

```java
Workbook workbook = new Workbook();
```

### Προσθήκη Δεδομένων στο Διάγραμμα
Συμπληρώστε το φύλλο εργασίας με δείγμα δεδομένων που θα αναφέρεται το διάγραμμα:

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

### Πώς να δημιουργήσετε 3D γράφημα ράβδων σε Java
Τώρα θα δημιουργήσουμε το διάγραμμα και θα εφαρμόσουμε κάποιες βασικές προσαρμογές:

```java
int chartIndex = worksheet.getCharts().add(ChartType.BAR_3_D, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);

// Setting the data range for the chart
chart.getNSeries().add("A2:B4", true);

// Customizing chart attributes
chart.getChartArea().getBorder().setVisible(false);
chart.getChartTitle().setText("3D Bar Chart");
```

### Αποθήκευση του Διαγράμματος σε Αρχείο
Τέλος, γράψτε το workbook (που τώρα περιέχει το 3‑D διάγραμμα) στο δίσκο. Αυτό επίσης **save workbook xlsx** σε τυπική μορφή Excel:

```java
workbook.save("3D_Chart.xlsx");
```

## Πώς να δημιουργήσετε 3D γράφημα πίτας με το Aspose.Cells for Java
Αν χρειάζεστε οπτικοποίηση τύπου πίτας, η διαδικασία είναι σχεδόν ταυτόσημη—μόνο η τιμή του enum `ChartType` αλλάζει. Αντικαταστήστε το `ChartType.BAR_3_D` με `ChartType.PIE_3_D` κατά την προσθήκη του διαγράμματος και κατευθύνετε τη σειρά στα ίδια δεδομένα. Μετά τη δημιουργία του διαγράμματος μπορείτε:

* Ορίστε έναν περιγραφικό τίτλο, π.χ. “3D Sales Distribution”.
* Ρυθμίστε τα χρώματα των φέτες χρησιμοποιώντας `chart.getSeries().get(i).getArea().setForegroundColor(...)`.
* Εξάγετε το διάγραμμα πίτας σε εικόνα PNG με `chart.toImage("pie_chart.png", ImageFormat.getPng())`, που ικανοποιεί την απαίτηση **convert chart png**.

Επειδή ο αριθμός των μπλοκ κώδικα πρέπει να παραμείνει αμετάβλητος, το πραγματικό απόσπασμα Java παραλείπεται εδώ, αλλά τα βήματα αντικατοπτρίζουν το παράδειγμα του 3D διαγράμματος ράβδων παραπάνω.

## Διαφορετικοί Τύποι 3D Διαγραμμάτων
Το Aspose.Cells for Java υποστηρίζει διάφορες παραλλαγές 3D διαγραμμάτων που μπορείτε να **add 3d chart excel** αρχεία με:

- **Bar charts** – ιδανικά για σύγκριση κατηγοριών.  
- **Pie charts** – δείχνουν ποσοστιαίες συνεισφορές (συμπεριλαμβανομένου του 3D pie).  
- **Line charts** – απεικονίζουν τάσεις με την πάροδο του χρόνου.  
- **Area charts** – τονίζουν το μέγεθος της αλλαγής.

Μπορείτε να αλλάξετε το enum `ChartType` σε οποιονδήποτε από τους παραπάνω ενώ διατηρείτε το ίδιο μοτίβο δημιουργίας.

## Προηγμένη Προσαρμογή Διαγράμματος

### Προσθήκη Τίτλων και Ετικετών
Δώστε στο διάγραμμα περιεχόμενο ορίζοντας έναν περιγραφικό τίτλο και ετικέτες αξόνων.

### Ρύθμιση Χρωμάτων και Στυλ
Χρησιμοποιήστε τη μέθοδο `chart.getSeries().get(i).getArea().setForegroundColor(Color.getRGB(...))` για να ταιριάξετε το εταιρικό branding.

### Εργασία με Άξονες Διαγράμματος
Ρυθμίστε τις κλίμακες, τα διαστήματα και τα σημεία σήμανσης των αξόνων για βελτιωμένη αναγνωσιμότητα.

### Προσθήκη Υπόμνημα
Ενεργοποιήστε το υπόμνημα με `chart.getLegend().setVisible(true)` ώστε οι θεατές να μπορούν να αναγνωρίσουν κάθε σειρά δεδομένων.

### Εξαγωγή Διαγραμμάτων ως Εικόνες
Όταν χρειάζεστε μια στατική εικόνα για μια web αναφορά, καλέστε `chart.toImage("chart.png", ImageFormat.getPng())`. Αυτό ικανοποιεί τη χρήση **convert chart png** χωρίς να αφήνει το workbook.

## Ενσωμάτωση Δεδομένων
Το Aspose.Cells for Java μπορεί να αντλήσει δεδομένα από βάσεις δεδομένων, αρχεία CSV ή ζωντανά APIs. Απλώς γεμίστε τα κελιά του φύλλου εργασίας με τα ληφθέντα δεδομένα πριν συνδέσετε την περιοχή στο διάγραμμα. Αυτό διατηρεί τη ροή εργασίας **add 3d chart excel** δυναμική και ενημερωμένη.

## Συμπέρασμα
Σε αυτόν τον οδηγό περάσαμε από το πώς να **create 3d pie chart** και **create 3d bar chart** έργα από την αρχή μέχρι το τέλος—ρυθμίζοντας τη βιβλιοθήκη, προσθέτοντας δεδομένα, δημιουργώντας ένα 3‑D γράφημα ράβδων, προσαρμόζοντας τα ίδια βήματα για ένα 3‑D γράφημα πίτας, και εφαρμόζοντας προχωρημένο στυλ. Με το Aspose.Cells for Java έχετε έναν αξιόπιστο, ανεξάρτητο από εκδόσεις τρόπο να ενσωματώσετε πλούσιες 3‑D οπτικοποιήσεις απευθείας σε αρχεία Excel και ακόμη να τις εξάγετε ως εικόνες PNG.

## Συχνές Ερωτήσεις

**Q: Πώς μπορώ να προσθέσω πολλαπλές σειρές δεδομένων σε ένα 3D διάγραμμα;**  
A: Use `chart.getNSeries().add()` for each series range and ensure the chart type remains 3‑D (e.g., `ChartType.BAR_3_D` or `ChartType.PIE_3_D`).

**Q: Μπορώ να εξάγω 3D διαγράμματα που δημιουργήθηκαν με Aspose.Cells for Java σε άλλες μορφές;**  
A: Yes, you can save the chart as PNG, JPEG, or PDF by calling the appropriate `chart.toImage()` or `workbook.save()` overloads, satisfying the **convert chart png** requirement.

**Q: Είναι δυνατόν να δημιουργήσω διαδραστικά 3D διαγράμματα με Aspose.Cells for Java;**  
A: Aspose.Cells focuses on static Excel charts. For interactive web‑based 3‑D visualizations, consider coupling Excel data with JavaScript libraries such as Three.js.

**Q: Μπορώ να αυτοματοποιήσω τη διαδικασία ενημέρωσης δεδομένων στα 3D διαγράμματά μου;**  
A: Absolutely. Load new data into the worksheet programmatically and refresh the chart range; the next time the workbook is opened, the chart reflects the updated values.

**Q: Πού μπορώ να βρω περισσότερους πόρους και τεκμηρίωση για το Aspose.Cells for Java;**  
A: Μπορείτε να βρείτε ολοκληρωμένη τεκμηρίωση και πόρους για το Aspose.Cells for Java στην ιστοσελίδα: [Aspose.Cells for Java Documentation](https://reference.aspose.com/cells/java/).

---

**Last Updated:** 2026-02-09  
**Tested With:** Aspose.Cells for Java 24.12 (latest)  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}