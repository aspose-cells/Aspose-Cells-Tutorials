---
category: general
date: 2026-07-03
description: Πώς να μορφοποιήσετε αρχεία Excel χρησιμοποιώντας Java. Μάθετε να μορφοποιείτε
  ημερομηνίες στήλης στο Excel, να εφαρμόζετε μορφή αριθμού στο Excel, να εξάγετε
  DataTable σε XLSX και να εισάγετε DataTable στο Excel με το Aspose Cells.
draft: false
keywords:
- how to style excel
- format column date excel
- apply number format excel
- export datatable to xlsx
- import datatable into excel
language: el
og_description: Πώς να μορφοποιήσετε αρχεία Excel σε Java. Αυτό το σεμινάριο δείχνει
  πώς να μορφοποιήσετε την ημερομηνία στήλης στο Excel, να εφαρμόσετε μορφή αριθμού
  στο Excel, να εξάγετε DataTable σε XLSX και να εισάγετε DataTable στο Excel.
og_title: Πώς να στυλιζάρετε το Excel – Οδηγός Java για προσαρμοσμένη μορφοποίηση
  στήλης
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: How to style Excel files using Java. Learn to format column date Excel,
    apply number format Excel, export DataTable to XLSX and import DataTable into
    Excel with Aspose Cells.
  headline: How to Style Excel – Import DataTable with Custom Formatting in Java
  type: TechArticle
tags:
- Java
- Excel
- Aspose.Cells
title: Πώς να μορφοποιήσετε το Excel – Εισαγωγή DataTable με προσαρμοσμένη μορφοποίηση
  στην Java
url: /el/java/excel-import-export/how-to-style-excel-import-datatable-with-custom-formatting-i/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να μορφοποιήσετε το Excel – Εισαγωγή DataTable με προσαρμοσμένη μορφοποίηση σε Java

Έχετε αναρωτηθεί ποτέ **πώς να μορφοποιήσετε το Excel** φύλλα προγραμματιστικά χωρίς να ανοίξετε το αρχείο χειροκίνητα; Δεν είστε μόνοι. Πολλοί προγραμματιστές χρειάζονται να δημιουργούν αναφορές όπου η πρώτη στήλη είναι έντονη, η δεύτερη εμφανίζει ημερομηνίες, και οι υπόλοιπες ακολουθούν καθαρή διάταξη. Σε αυτόν τον οδηγό θα περάσουμε από ένα πλήρες, εκτελέσιμο παράδειγμα που **εισάγει ένα DataTable στο Excel**, εφαρμόζει έντονη κεφαλίδα, μορφοποιεί μια στήλη ημερομηνίας και τελικά **εξάγει το DataTable σε XLSX**.  

Θα χρησιμοποιήσουμε το Aspose.Cells for Java, αλλά οι έννοιες μεταφράζονται σε οποιαδήποτε βιβλιοθήκη που σας επιτρέπει να εργάζεστε με στυλ. Στο τέλος θα έχετε ένα επαναχρησιμοποιήσιμο μοτίβο για **apply number format Excel** κελιά, **format column date Excel**, και να παραδίδετε ένα επαγγελματικό βιβλίο εργασίας στους χρήστες σας.

## Απαιτούμενα

- Java 17 (ή οποιοδήποτε πρόσφατο JDK)  
- Aspose.Cells for Java 23.9 ή νεότερο (η δωρεάν δοκιμή λειτουργεί καλά)  
- Μια δομή τύπου `DataTable` (το παράδειγμα χρησιμοποιεί ένα απλό mock)  
- Το αγαπημένο σας IDE (IntelliJ IDEA, Eclipse, VS Code…)

Δεν απαιτούνται πρόσθετα Maven plugins· απλώς προσθέστε το Aspose.Cells JAR στην classpath σας.

---

## Βήμα 1: Απόκτηση του πηγαίου DataTable – Προετοιμασία «Export DataTable to XLSX»

Πριν μπορέσουμε να **import datatable into excel**, χρειαζόμαστε ένα αντικείμενο `DataTable` που να αντιπροσωπεύει τα δεδομένα που θέλετε να εξάγετε. Σε πραγματικά έργα μπορεί να τα αντλήσετε από μια βάση δεδομένων, αρχείο CSV ή ένα API. Για αυτόν τον οδηγό θα δημιουργήσουμε ένα μικρό mock πίνακα:

```java
import java.util.*;
import com.aspose.cells.*;

public class DemoData {
    public static DataTable getDataTable() {
        // Create a simple table with three columns: ID, Date, Amount
        DataTable dt = new DataTable();
        dt.getColumns().add("ID", DataType.INTEGER);
        dt.getColumns().add("OrderDate", DataType.DATE_TIME);
        dt.getColumns().add("Total", DataType.DOUBLE);

        // Add a few rows
        dt.getRows().add(new Object[]{1, new Date(), 125.50});
        dt.getRows().add(new Object[]{2, new Date(System.currentTimeMillis() - 86400000L), 99.99});
        dt.getRows().add(new Object[]{3, new Date(System.currentTimeMillis() - 2*86400000L), 250.00});
        return dt;
    }
}
```

> **Γιατί αυτό είναι σημαντικό:** Η σωστή λήψη των δεδομένων από την αρχή σημαίνει ότι το υπόλοιπο λογική στυλ μπορεί να εστιάσει αποκλειστικά στην παρουσίαση, όχι στην επεξεργασία δεδομένων.

---

## Βήμα 2: Δημιουργία Πίνακα για την Καταγραφή Ορισμών Στυλ για Κάθε Στήλη

Το Aspose.Cells σας επιτρέπει να περάσετε έναν πίνακα **Style[]** κατά την εισαγωγή ενός `DataTable`. Κάθε στοιχείο αντιστοιχεί σε μια στήλη και καθορίζει πώς θα εμφανιστεί η στήλη μετά την εισαγωγή. Ας δεσμεύσουμε τον πίνακα με βάση τον αριθμό των στηλών:

```java
DataTable dataTable = DemoData.getDataTable();
Style[] columnStyles = new Style[dataTable.getColumns().size()];
```

> **Συμβουλή:** Εάν έχετε πολλές στήλες, σκεφτείτε να δημιουργήσετε τον πίνακα σε βρόχο και να επαναχρησιμοποιείτε ένα μόνο αντικείμενο `Style` όπου η μορφοποίηση είναι ίδια. Αυτό μειώνει τη χρήση μνήμης.

---

## Βήμα 3: Ορισμός Στυλ – Έντονη Κεφαλίδα & Μορφοποίηση Ημερομηνίας

Τώρα απαντάμε στην κλασική ερώτηση **format column date excel** και επίσης δείχνουμε **apply number format excel** για άλλες στήλες.

```java
// --- Style for the first column (header bold) ---
columnStyles[0] = new Style();
columnStyles[0].getFont().setBold(true);          // Makes header text bold

// --- Style for the second column (date formatting) ---
columnStyles[1] = new Style();
columnStyles[1].setNumber(StyleNumberFormat.DATE); // Uses the built‑in DATE format

// --- Optional: Style for the third column (currency) ---
columnStyles[2] = new Style();
columnStyles[2].setNumber(StyleNumberFormat.CURRENCY_USD);
```

**Τι συμβαίνει εδώ;**  
- `StyleNumberFormat.DATE` λέει στο Excel να αντιμετωπίζει την τιμή του κελιού ως σύντομη ημερομηνία (π.χ., *31/01/2024*).  
- `StyleNumberFormat.CURRENCY_USD` προσθέτει αυτόματα το σύμβολο `$` και δύο δεκαδικά ψηφία.  
- Ο καθορισμός της γραμματοσειράς σε έντονη στην πρώτη στήλη κάνει την κεφαλίδα να ξεχωρίζει, κάτι που είναι συχνή απαίτηση όταν **how to style excel** τα φύλλα για ευανάγνωστη παρουσίαση.

> **Ακραία περίπτωση:** Εάν τα πηγαία δεδομένα σας περιέχουν ήδη μορφοποιημένες συμβολοσειρές, ίσως χρειαστεί να τις μετατρέψετε σε αντικείμενα `java.util.Date` πριν την εισαγωγή· διαφορετικά το Excel θα τις αντιμετωπίσει ως απλό κείμενο.

---

## Βήμα 4: Δημιουργία Νέου Workbook και Πρόσβαση στο Πρώτο Worksheet

Ένα νέο workbook μας παρέχει καθαρό καμβά. Θα πάρουμε το πρώτο worksheet, όπου θα γίνει η εισαγωγή.

```java
Workbook workbook = new Workbook();               // New empty workbook
Worksheet worksheet = workbook.getWorksheets().get(0); // First sheet (index 0)
```

> **Γιατί νέο workbook;** Ξεκινώντας από το μηδέν εξασφαλίζουμε ότι δεν υπάρχουν υπολειπόμενα στυλ ή κρυφές γραμμές που να επηρεάζουν το τελικό αποτέλεσμα—σημαντικό όταν **how to style excel** αρχεία με συνέπεια σε πολλαπλές εκτελέσεις.

---

## Βήμα 5: Εισαγωγή του DataTable με τα Στυλ Στηλών

Αυτή είναι η καρδιά της λειτουργίας: η τροφοδότηση του `DataTable` στο φύλλο ενώ εφαρμόζουμε τον πίνακα στυλ που δημιουργήσαμε.

```java
// The third argument (true) tells Aspose.Cells to include column headers.
worksheet.getCells().importDataTable(dataTable, true, columnStyles);
```

**Εξήγηση:**  
- `importDataTable` αντιγράφει τόσο τη γραμμή κεφαλίδας όσο και τις γραμμές δεδομένων.  
- Ο πίνακας `columnStyles` ευθυγραμμίζεται με κάθε στήλη, έτσι η κεφαλίδα της πρώτης στήλης γίνεται έντονη, η δεύτερη στήλη εμφανίζει ημερομηνίες, και η τρίτη στήλη εμφανίζεται ως νόμισμα.  
- Αυτή η μοναδική γραμμή αντικαθιστά δεκάδες χειροκίνητες μορφοποιήσεις κελιού‑κατά‑κελί, δείχνοντας έναν καθαρό τρόπο για **apply number format excel** προγραμματιστικά.

---

## Βήμα 6: Αποθήκευση του Στυλιζαμένου Workbook – Ολοκλήρωση του «Export DataTable to XLSX»

Τέλος αποθηκεύουμε το workbook στο δίσκο. Προσαρμόστε τη διαδρομή σε έναν φάκελο με δικαιώματα εγγραφής στο σύστημά σας.

```java
String outputPath = "C:/temp/styledImport.xlsx";
workbook.save(outputPath);
System.out.println("Workbook saved to " + outputPath);
```

Ανοίξτε το αρχείο στο Excel και θα πρέπει να δείτε:

- Η κεφαλίδα της στήλης **ID** σε έντονη γραφή.  
- Η στήλη **OrderDate** μορφοποιημένη ως ημερομηνίες (π.χ., *27/04/2024*).  
- Η στήλη **Total** εμφανίζεται με σύμβολο δολαρίου και δύο δεκαδικά ψηφία.

> **Pro tip:** Εάν χρειάζεται να υποστηρίξετε παλαιότερες εκδόσεις του Excel, καλέστε `workbook.save(outputPath, SaveFormat.XLS)` αντί για το προεπιλεγμένο XLSX.

---

## Βήμα 7: Επαλήθευση του Αποτελέσματος & Προαιρετικές Ρυθμίσεις

Είναι καλή πρακτική να ελέγχετε διπλά το παραγόμενο αρχείο, ειδικά όταν αυτοματοποιείτε αναφορές για ενδιαφερόμενους.

```java
// Quick verification: read the first cell's style
Cell firstHeader = worksheet.getCells().get(0, 0);
boolean isBold = firstHeader.getStyle().getFont().isBold();
System.out.println("Header bold? " + isBold);
```

Αν το `isBold` εκτυπώνει `true`, η ρουτίνα **how to style excel** λειτουργεί όπως προβλέπεται. Από εδώ μπορείτε να:

- Προσθέσετε conditional formatting (π.χ., επισήμανση συνόλων > $200).  
- Παγώσετε την πρώτη γραμμή για πιο εύκολη κύλιση.  
- Εισάγετε ένα γράφημα που αναφέρεται στα εισαγόμενα δεδομένα.

Όλες αυτές οι επεκτάσεις ακολουθούν το ίδιο μοτίβο: ορίζετε ένα `Style`, το εφαρμόζετε και αποθηκεύετε.

---

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

| Ερώτηση | Απάντηση |
|----------|--------|
| **Μπορώ να μορφοποιήσω περισσότερες από μία στήλες με τον ίδιο τρόπο;** | Ναι—επαναχρησιμοποιήστε ένα μόνο αντικείμενο `Style` για όλες τις στήλες που μοιράζονται την ίδια μορφοποίηση. |
| **Τι γίνεται αν το DataTable μου έχει περισσότερες στήλες από στυλ;** | Οποιαδήποτε στήλη χωρίς αντίστοιχο στοιχείο στο `columnStyles` θα χρησιμοποιήσει το προεπιλεγμένο στυλ. |
| **Πώς αλλάζω τη μορφή ημερομηνίας σε “dd‑MMM‑yyyy”;** | Χρησιμοποιήστε `columnStyles[1].setCustom("#dd-MMM-yyyy#");` αντί του ενσωματωμένου `DATE`. |
| **Υπάρχει τρόπος να προσαρμόσω αυτόματα το πλάτος των στηλών μετά την εισαγωγή;** | Κλήστε `worksheet.autoFitColumns();` μετά το `importDataTable`. |
| **Θα λειτουργήσει αυτό σε Linux/macOS;** | Απόλυτα—το Aspose.Cells είναι ανεξάρτητο πλατφόρμας εφόσον έχετε ένα συμβατό JDK. |

---

## Συμπέρασμα

Τώρα έχετε ένα στέρεο, ολοκληρωμένο παράδειγμα του **how to style Excel** βιβλίων εργασίας μέσω **importing datatable into excel**, **format column date excel**, και **apply number format excel** χρησιμοποιώντας Java. Ο κώδικας δείχνει τη πλήρη ροή από **export datatable to xlsx** μέχρι το άνοιγμα του αρχείου στο Excel, καλύπτοντας τόσο το *τι* όσο και το *γιατί* κάθε βήματος.  

Δοκιμάστε το: προσαρμόστε τον πίνακα στυλ, προσθέστε περισσότερες στήλες ή ενσωματώστε ένα πραγματικό ερώτημα βάσης δεδομένων. Το ίδιο μοτίβο θα σας επιτρέψει να δημιουργείτε επαγγελματικές αναφορές με ένα κλικ, χωρίς χειροκίνητη μορφοποίηση.

![Styled Excel worksheet generated by the tutorial code](https://example.com/images/styled-worksheet.png "Στιγμιότυπο οθόνης του στυλιζαμένου φύλλου Excel που δημιουργήθηκε με Java και Aspose.Cells")

*Image alt text: “Φύλλο Excel με στυλ που δημιουργήθηκε με Java και Aspose.Cells, εμφανίζει έντονη κεφαλίδα και μορφοποιημένη στήλη ημερομηνίας.”*

## Τι Θα Πρέπει Να Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε σε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να Δημιουργήσετε & Μορφοποιήσετε Κελιά Excel Χρησιμοποιώντας Aspose.Cells for Java: Οδηγός Βήμα‑Βήμα](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)
- [Πώς να Στυλιζάτε Κελιά Excel και να Προσθέσετε Υπερσυνδέσμους Χρησιμοποιώντας Aspose.Cells for Java](/cells/english/java/formatting/style-excel-cells-hyperlinks-aspose-cells-java/)
- [Aspose.Cells for Java: Πώς να Δημιουργήσετε και να Μορφοποιήσετε Βιβλία Εργασίας Excel Αποτελεσματικά](/cells/english/java/getting-started/aspose-cells-java-workbook-creation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}