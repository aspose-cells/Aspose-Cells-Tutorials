---
category: general
date: 2026-06-18
description: Πώς να χρησιμοποιήσετε το SmartMarkerProcessor για τη δυναμική ονομασία
  φύλλων εργασίας σε έργα Excel – ένας πλήρης, βήμα‑βήμα οδηγός με πλήρες κώδικα Java.
draft: false
keywords:
- how to use smartmarkerprocessor
- dynamic worksheet naming excel
language: el
og_description: Μάθετε πώς να χρησιμοποιείτε το SmartMarkerProcessor για τη δυναμική
  ονομασία φύλλων εργασίας σε αρχεία Excel με ένα πρακτικό παράδειγμα Java.
og_title: Πώς να χρησιμοποιήσετε το SmartMarkerProcessor για τη δυναμική ονομασία
  φύλλων
schemas:
- author: Aspose
  dateModified: '2026-06-18'
  description: How to use SmartMarkerProcessor for dynamic worksheet naming Excel
    projects – a complete, step‑by‑step guide with full Java code.
  headline: How to Use SmartMarkerProcessor for Dynamic Sheet Naming
  type: TechArticle
- description: How to use SmartMarkerProcessor for dynamic worksheet naming Excel
    projects – a complete, step‑by‑step guide with full Java code.
  name: How to Use SmartMarkerProcessor for Dynamic Sheet Naming
  steps:
  - name: Expected Output
    text: 'When you open `detailSheets.xlsx` you should see:'
  - name: How does the processor know which row maps to which sheet?
    text: The library internally uses the order of the collection. The first element
      becomes `Detail_1`, the second `Detail_2`, and so on. If you need a custom order,
      sort the collection before calling `process`.
  - name: What if my sheet name needs to include a date?
    text: 'Just embed another placeholder and make sure the data source provides it:'
  - name: Can I prevent certain columns from being copied to the new sheets?
    text: Yes—use the `SmartMarkerOptions` object to specify `setIgnoreUnusedColumns(true)`.
      That way only markers you’ve placed will be evaluated.
  - name: Is there a performance impact with very large data sets?
    text: Processing is O(n) where *n* is the number of rows. For tens of thousands
      of rows, consider streaming the data or batching the workbook saves to avoid
      excessive memory consumption.
  type: HowTo
tags:
- Excel
- SmartMarkerProcessor
- Java
- Automation
title: Πώς να χρησιμοποιήσετε το SmartMarkerProcessor για δυναμική ονομασία φύλλων
url: /el/java/worksheet-management/how-to-use-smartmarkerprocessor-for-dynamic-sheet-naming/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Χρησιμοποιήσετε το SmartMarkerProcessor για Δυναμική Ονομασία Φύλλων

Έχετε αναρωτηθεί ποτέ **πώς να χρησιμοποιήσετε το SmartMarkerProcessor** όταν χρειάζεται να δημιουργήσετε μια σειρά από φύλλα λεπτομερειών από ένα πρότυπο; Δεν είστε οι μόνοι—οι προγραμματιστές συχνά αντιμετωπίζουν το πρόβλημα της διατήρησης των ονομάτων των φύλλων τακτοποιημένα ενώ τα δεδομένα παράγουν δεκάδες γραμμές. Το καλό νέο; Με λίγες γραμμές Java μπορείτε να αφήσετε το SmartMarkerProcessor να κάνει το βαριά δουλειά και να δώσει σε κάθε παραγόμενο φύλλο εργασίας ένα σημασιολογικό όνομα αυτόματα.

Σε αυτό το tutorial θα περάσουμε από ένα πραγματικό σενάριο: παίρνουμε ένα πρότυπο βιβλίο εργασίας, του παρέχουμε μια πηγή δεδομένων, και καταλήγουμε με ένα αρχείο όπου κάθε φύλλο λεπτομερειών ονομάζεται **dynamic worksheet naming Excel**‑style (σκεφτείτε `Detail_1`, `Detail_2`, …). Στο τέλος θα γνωρίζετε ακριβώς τι κάνει κάθε γραμμή, γιατί έχει σημασία το πρότυπο ονομασίας, και πώς να προσαρμόσετε τον κώδικα για ειδικές περιπτώσεις όπως ειδικούς χαρακτήρες ή προσαρμοσμένες τοποθεσίες φακέλων.

## Προαπαιτούμενα

Πριν βουτήξουμε, βεβαιωθείτε ότι έχετε:

* Εγκατεστημένο Java 8+ (ο κώδικας χρησιμοποιεί την τυπική σύνταξη Java).
* Aspose.Cells for Java (ή οποιαδήποτε βιβλιοθήκη που παρέχει `SmartMarkerProcessor`).
* Ένα πρότυπο αρχείο Excel (`template.xlsx`) με Smart Markers τοποθετημένα όπου θέλετε τα δεδομένα.
* Ένα απλό POJO ή `Map<String, Object>` που λειτουργεί ως πηγή δεδομένων.

Τα έχετε όλα; Τέλεια—ας ξεκινήσουμε.

## Βήμα 1: Φόρτωση του Πρότυπου Βιβλίου Εργασίας

Το πρώτο που χρειάζεστε είναι ένα αντικείμενο `Workbook` που δείχνει στο αρχείο πρότυπο. Σκεφτείτε το ως το άνοιγμα ενός φρέσκου καμβά που ήδη περιέχει τα placeholders.

```java
// Step 1: Load the template workbook
Workbook workbook = new Workbook("YOUR_DIRECTORY/template.xlsx");
```

*Γιατί είναι σημαντικό*: Η φόρτωση του βιβλίου εργασίας μία φορά κρατά τη χρήση μνήμης χαμηλή. Αν δημιουργούσατε νέο βιβλίο εργασίας για κάθε γραμμή, θα εξαντλούσατε γρήγορα τον χώρο heap.

> **Συμβουλή**: Χρησιμοποιήστε απόλυτη διαδρομή ή πόρο classpath (`getClass().getResourceAsStream`) αν η εφαρμογή σας τρέχει από JAR.

## Βήμα 2: Δημιουργία SmartMarkerProcessor

Τώρα δημιουργούμε τον επεξεργαστή που θα σαρώσει το βιβλίο εργασίας για Smart Markers και θα τα αντικαταστήσει με δεδομένα.

```java
// Step 2: Create a SmartMarkerProcessor for the workbook
SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);
```

`SmartMarkerProcessor` είναι η μηχανή πίσω από τη μαγεία. Ξέρει πώς να διαβάζει markers όπως `&=Customers.Name` και να τα μετατρέπει σε πραγματικές τιμές κελιών.

## Βήμα 3: Ορισμός Προτύπου Ονομασίας για Φύλλα Λεπτομερειών

Εδώ όπου **dynamic worksheet naming Excel** λάμπει. Λέτε στον επεξεργαστή πώς πρέπει να φαίνεται το νέο όνομα φύλλου, χρησιμοποιώντας το `{0}` ως placeholder για το δείκτη γραμμής (ή οποιαδήποτε άλλη μεταβλητή επιλέξετε).

```java
// Step 3: Define a naming pattern for the detail sheets (row index will replace {0})
processor.setDetailSheetNewName("Detail_{0}");
```

Όταν ο επεξεργαστής δημιουργεί νέο φύλλο για κάθε γραμμή δεδομένων, θα αντικαταστήσει το `{0}` με `1`, `2`, `3`, … παράγοντας `Detail_1`, `Detail_2`, κ.λπ. Αυτό κρατά το βιβλίο εργασίας οργανωμένο και κάνει την επεξεργασία downstream (όπως VBA macros) παιχνιδάκι.

> **Τι‑αν** χρειάζεστε πιο περιγραφικό όνομα, όπως `Invoice_2024_01`; απλώς αλλάξτε το πρότυπο: `"Invoice_{0}_{1}"` και παρέχετε επιπλέον placeholders στην πηγή δεδομένων.

## Βήμα 4: Επεξεργασία Smart Markers με την Πηγή Δεδομένων Σας

Τώρα η κύρια λειτουργία—παραγωγή των δεδομένων στο πρότυπο. Η μέθοδος `process` παίρνει τρία ορίσματα: τη συλλογή κελιών προς σάρωση, την πηγή δεδομένων, και προαιρετικά ένα προσαρμοσμένο αντικείμενο επιλογών (θα χρησιμοποιήσουμε την πιο απλή υπερφόρτωση).

```java
// Step 4: Process smart markers in the first worksheet using the data source
processor.process(workbook.getWorksheets().get(0).getCells(), dataSource);
```

*Γιατί στοχεύουμε το πρώτο φύλλο*: Στα περισσότερα πρότυπα το κύριο φύλλο βρίσκεται στο index 0. Αν το πρότυπό σας τοποθετεί markers αλλού, απλώς αλλάξτε το index.

Η `dataSource` μπορεί να είναι:

* Μια `List<Map<String, Object>>` όπου κάθε χάρτης αντιπροσωπεύει μια γραμμή.
* Μια συλλογή POJOs (plain old Java objects) με getters.
* Οποιοδήποτε αντικείμενο μπορεί η βιβλιοθήκη να ανακτήσει μέσω reflection.

Ο επεξεργαστής θα επαναλάβει τη συλλογή, θα κλωνοποιήσει το κύριο φύλλο για κάθε στοιχείο, θα αντικαταστήσει τα markers, και θα μετονομάσει το κλώνο σύμφωνα με το πρότυπο που ορίσατε νωρίτερα.

## Βήμα 5: Αποθήκευση του Παραγόμενου Βιβλίου Εργασίας

Τέλος, γράψτε το βιβλίο εργασίας πίσω στο δίσκο. Το παραγόμενο αρχείο θα περιέχει ένα φύλλο για κάθε γραμμή δεδομένων, το καθένα με το σωστό όνομα.

```java
// Step 5: Save the resulting workbook with the generated detail sheets
workbook.save("YOUR_DIRECTORY/detailSheets.xlsx");
```

Τώρα μπορείτε να ανοίξετε το `detailSheets.xlsx` στο Excel και να δείτε `Detail_1`, `Detail_2`, … το καθένα γεμάτο με την αντίστοιχη εγγραφή.

> **Ειδική περίπτωση**: Αν η πηγή δεδομένων σας περιέχει περισσότερα από 255 φύλλα, το Excel θα ρίξει σφάλμα. Σκεφτείτε να χωρίσετε το αποτέλεσμα σε πολλαπλά βιβλία εργασίας ή να χρησιμοποιήσετε στρατηγική σελιδοποίησης.

## Πλήρες Παράδειγμα Εργασίας

Συνδυάζοντας τα παραπάνω, εδώ είναι ένα ελάχιστο, end‑to‑end πρόγραμμα που μπορείτε να αντιγράψετε‑και‑επικολλήσετε στο IDE σας:

```java
import com.aspose.cells.*;

import java.util.*;

public class SmartMarkerDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load template
        Workbook workbook = new Workbook("YOUR_DIRECTORY/template.xlsx");

        // 2️⃣ Create processor
        SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);

        // 3️⃣ Set naming pattern
        processor.setDetailSheetNewName("Detail_{0}");

        // 4️⃣ Build a simple data source (List of Maps)
        List<Map<String, Object>> dataSource = new ArrayList<>();

        Map<String, Object> row1 = new HashMap<>();
        row1.put("Name", "Alice");
        row1.put("Amount", 1200);
        dataSource.add(row1);

        Map<String, Object> row2 = new HashMap<>();
        row2.put("Name", "Bob");
        row2.put("Amount", 850);
        dataSource.add(row2);

        // 5️⃣ Process the first worksheet
        processor.process(workbook.getWorksheets().get(0).getCells(), dataSource);

        // 6️⃣ Save output
        workbook.save("YOUR_DIRECTORY/detailSheets.xlsx");
        System.out.println("Workbook generated with dynamic sheet names!");
    }
}
```

### Αναμενόμενο Αποτέλεσμα

Όταν ανοίξετε το `detailSheets.xlsx` θα πρέπει να δείτε:

| Όνομα Φύλλου | Κελί A1 (παράδειγμα) |
|--------------|----------------------|
| Detail_1     | Alice                |
| Detail_2     | Bob                  |

Κάθε φύλλο περιέχει τα δεδομένα από τον αντίστοιχο χάρτη, και τα ονόματα των φύλλων ακολουθούν το πρότυπο που ορίσαμε.

## Συχνές Ερωτήσεις & Συμβουλές

### Πώς γνωρίζει ο επεξεργαστής ποια γραμμή αντιστοιχεί σε ποιο φύλλο;

Η βιβλιοθήκη εσωτερικά χρησιμοποιεί τη σειρά της συλλογής. Το πρώτο στοιχείο γίνεται `Detail_1`, το δεύτερο `Detail_2`, κ.λπ. Αν χρειάζεστε προσαρμοσμένη σειρά, ταξινομήστε τη συλλογή πριν καλέσετε το `process`.

### Τι γίνεται αν το όνομα του φύλλου πρέπει να περιλαμβάνει ημερομηνία;

Απλώς ενσωματώστε ένα ακόμη placeholder και βεβαιωθείτε ότι η πηγή δεδομένων το παρέχει:

```java
processor.setDetailSheetNewName("Report_{0}_{1}");
```

Όπου το `{0}` μπορεί να είναι ο δείκτης γραμμής και το `{1}` μια μορφοποιημένη συμβολοσειρά ημερομηνίας που προσθέτετε σε κάθε χάρτη (`"Date", "2024-01-31"`).

### Μπορώ να αποτρέψω την αντιγραφή ορισμένων στηλών στα νέα φύλλα;

Ναι—χρησιμοποιήστε το αντικείμενο `SmartMarkerOptions` για να ορίσετε `setIgnoreUnusedColumns(true)`. Έτσι θα αξιολογηθούν μόνο τα markers που έχετε τοποθετήσει.

### Υπάρχει αντίκτυπος στην απόδοση με πολύ μεγάλα σύνολα δεδομένων;

Η επεξεργασία είναι O(n) όπου *n* είναι ο αριθμός των γραμμών. Για δεκάδες χιλιάδες γραμμές, σκεφτείτε να κάνετε streaming των δεδομένων ή να κάνετε batch αποθηκεύσεις του βιβλίου εργασίας για να αποφύγετε υπερβολική κατανάλωση μνήμης.

## Συμπέρασμα

Τώρα έχετε μια σταθερή κατανόηση του **πώς να χρησιμοποιήσετε το SmartMarkerProcessor** για αυτοματοποίηση **dynamic worksheet naming Excel**‑style. Φορτώνοντας ένα πρότυπο, ορίζοντας πρότυπο ονομασίας, παρέχοντας πηγή δεδομένων και αποθηκεύοντας το αποτέλεσμα, μπορείτε να δημιουργήσετε καθαρά, καλά ονομασμένα φύλλα λεπτομερειών με λίγες μόνο γραμμές κώδικα.

Τι θα κάνετε στη συνέχεια; Δοκιμάστε να προσθέσετε γραφήματα, conditional formatting, ή ακόμη και προστασία στα παραγόμενα φύλλα. Και αν εργάζεστε με πηγές CSV, απλώς μετατρέψτε τις σε λίστα χάρτες πριν τις περάσετε στον επεξεργαστή.

Πειραματιστείτε ελεύθερα—αλλάξτε το πρότυπο ονομασίας, παίξτε με διαφορετικές δομές δεδομένων, ή ενσωματώστε αυτό το snippet σε μια μεγαλύτερη pipeline αναφορών. Καλή προγραμματιστική!

## Τι Πρέπει Να Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε επιπλέον δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στην υλοποίηση των δικών σας έργων.

- [How to Use Aspose.Cells for Excel Slicer Automation in Java](/cells/english/java/advanced-features/excel-slicer-modifications-java-aspose-cells/)
- [How to Use Aspose to Manage Excel Hyperlinks in Java](/cells/english/java/advanced-features/manage-excel-hyperlinks-aspose-cells-java/)
- [How to Convert Excel to PDF in Java Using Aspose.Cells: A Step-by-Step Guide](/cells/english/java/workbook-operations/convert-excel-to-pdf-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}