---
category: general
date: 2026-06-30
description: Πώς να εξάγετε έναν πίνακα Pivot σε Java και να αποθηκεύσετε μια περιοχή
  ως PNG χρησιμοποιώντας το Aspose.Cells. Οδηγός βήμα‑προς‑βήμα με πλήρη κώδικα και
  συμβουλές.
draft: false
keywords:
- how to export pivot
- save range as png
- Aspose.Cells export image
- Java pivot table image
- workbook to PNG
language: el
og_description: Μάθετε πώς να εξάγετε έναν συγκεντρωτικό πίνακα σε Java και να αποθηκεύσετε
  την περιοχή ως PNG. Πλήρες παράδειγμα, εξηγήσεις και συμβουλές βέλτιστων πρακτικών.
og_title: Πώς να εξάγετε τον Πίνακα Pivot ως PNG – Java Tutorial
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: How to export pivot table in Java and save range as PNG using Aspose.Cells.
    Step‑by‑step guide with full code and tips.
  headline: How to Export Pivot Table as PNG – Complete Java Guide
  type: TechArticle
tags:
- Aspose.Cells
- Java
- PivotTable
- ImageExport
title: Πώς να εξάγετε Πίνακα Pivot ως PNG – Πλήρης Οδηγός Java
url: /el/java/excel-pivot-tables/how-to-export-pivot-table-as-png-complete-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Εξάγετε Pivot Table ως PNG – Πλήρης Οδηγός Java

Έχετε αναρωτηθεί ποτέ **πώς να εξάγετε δεδομένα pivot** από ένα βιβλίο εργασίας Excel χωρίς να χάσετε το στυλ του; Ίσως χρειάζεστε αυτό το pivot chart για μια αναφορά, ένα συνημμένο email ή μια γρήγορη μικρογραφία σε έναν πίνακα ελέγχου. Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα τις ακριβείς ενέργειες για **αποθήκευση περιοχής ως PNG** χρησιμοποιώντας το Aspose.Cells for Java, και θα εξηγήσουμε γιατί κάθε γραμμή είναι σημαντική. Χωρίς περιττές πληροφορίες, μόνο μια εκτελέσιμη λύση που μπορείτε να αντιγράψετε‑επικολλήσετε σήμερα.

Θα ολοκληρώσετε αυτόν τον οδηγό με ένα αυτόνομο πρόγραμμα Java που φορτώνει ένα αρχείο `.xlsx`, παίρνει τον πρώτο pivot table και το γράφει απευθείας σε εικόνα PNG διατηρώντας το οπτικό στυλ του pivot. Έτοιμοι; Ας ξεκινήσουμε.

---

## Τι Θα Χρειαστεί

- **Java 8+** (ο κώδικας μεταγλωττίζεται με JDK 8 και νεότερο)
- **Aspose.Cells for Java** library – version 23.10 ή νεότερη (κατεβάστε από την επίσημη ιστοσελίδα ή χρησιμοποιήστε Maven)
- Ένα βιβλίο εργασίας Excel (`pt.xlsx`) που περιέχει τουλάχιστον έναν pivot table
- Ένας φάκελος όπου έχετε δικαιώματα ανάγνωσης/εγγραφής (θα τον ονομάσουμε `YOUR_DIRECTORY`)

Αν κάτι από αυτά σας φαίνεται άγνωστο, μην ανησυχείτε. Η εγκατάσταση μιας εξάρτησης Maven είναι τόσο εύκολη όσο η προσθήκη μιας γραμμής στο `pom.xml`. Εδώ είναι το απόσπασμα:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

Αντικαταστήστε το `jdk17` με τον κατάλληλο classifier για την έκδοση του JDK σας. Αυτό είναι—το πρόγραμμά σας είναι έτοιμο να αλληλεπιδρά με αρχεία Excel.

## Βήμα 1 – Φόρτωση του Workbook που Περιέχει τον Pivot Table

Το πρώτο που πρέπει να κάνουμε είναι να ανοίξουμε το αρχείο Excel. Το Aspose.Cells αφαιρεί την πολυπλοκότητα του συστήματος αρχείων ώστε να μπορείτε να δουλεύετε με τοπικά αρχεία, ροές ή ακόμη και αποθήκευση στο cloud. Σε αυτό το παράδειγμα θα το κρατήσουμε απλό και θα διαβάσουμε από το δίσκο.

```java
import com.aspose.cells.*;

public class ExportPivotAsPng {
    public static void main(String[] args) throws Exception {
        // Load the workbook that holds the pivot table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/pt.xlsx");
```

> **Γιατί είναι σημαντικό:** Το αντικείμενο `Workbook` είναι η πύλη σε κάθε φύλλο, πίνακα, γράφημα και pivot στο αρχείο. Αν το αρχείο δεν μπορεί να ανοιχθεί, η υπόλοιπη διαδικασία ακυρώνεται, επομένως ο έγκαιρος χειρισμός του `Exception` σας εξοικονομεί χρόνο εντοπισμού σφαλμάτων.

## Βήμα 2 – Πρόσβαση στο Πρώτο Worksheet

Τα περισσότερα workbooks έχουν ένα προεπιλεγμένο φύλλο όπου βρίσκεται το pivot. Θα πάρουμε το πρώτο φύλλο (δείκτης 0). Αν το pivot σας βρίσκεται σε διαφορετικό φύλλο, απλώς αλλάξτε το δείκτη ή χρησιμοποιήστε `getSheetByName`.

```java
        // Get the first worksheet (index 0)
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

> **Συμβουλή:** Χρησιμοποιήστε `worksheet.getName()` για να εκτυπώσετε το όνομα του φύλλου αν δεν είστε σίγουροι πού βρίσκεται το pivot. Αυτός ο μικρός έλεγχος μπορεί να αποτρέψει εκπλήξεις «null pointer» αργότερα.

## Βήμα 3 – Ανάκτηση της Περιοχής του Πρώτου Pivot Table

Ένας pivot table μπορεί να καλύπτει πολλές σειρές και στήλες, αλλά το Aspose.Cells σας επιτρέπει να λάβετε την ακριβή του περιοχή με μία κλήση. Αυτή η περιοχή είναι αυτή που θα μετατρέψουμε σε εικόνα.

```java
        // Retrieve the range of the first pivot table on the worksheet
        PivotTable pivotTable = worksheet.getPivotTables().get(0);
        Range pivotRange = pivotTable.getPivotTableRange();
```

> **Γιατί χρησιμοποιούμε το `getPivotTableRange()`:** Επιστρέφει το ακριβές μπλοκ κελιών που καταλαμβάνει το pivot, συμπεριλαμβανομένων των κεφαλίδων και των συνολικών. Η εξαγωγή ολόκληρου του worksheet θα έριχνε πολλά άσχετα δεδομένα, ενώ η εξαγωγή μόνο του pivot κρατά το PNG καθαρό και εστιασμένο.

## Βήμα 4 – Διαμόρφωση Επιλογών Εικόνας για Διατήρηση του Στυλ του Pivot

Από προεπιλογή, το Aspose.Cells μπορεί να αποδώσει το pivot χωρίς το ενσωματωμένο του στυλ. Για να διατηρήσουμε την εμφάνιση (σκιές, γραμματοσειρές, περιγράμματα) ενεργοποιούμε το `RenderPivotTableStyle`.

```java
        // Set image options to keep the pivot’s visual style
        ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
        imgOptions.setRenderPivotTableStyle(true);   // critical for preserving style
```

> **Ακραία περίπτωση:** Αν εξάγετε ένα pivot που χρησιμοποιεί προσαρμοσμένα θέματα, ίσως χρειαστεί επίσης να ορίσετε `setRenderGridLines(true)` για να διατηρήσετε τις γραμμές πλέγματος. Πειραματιστείτε με αυτές τις σημαίες μέχρι το αποτέλεσμα να ταιριάζει με τις προσδοκίες σας.

## Βήμα 5 – Εξαγωγή της Περιοχής Pivot ως Αρχείο PNG

Τώρα η στιγμή της αλήθειας: γράφουμε την περιοχή σε αρχείο PNG. Η μέθοδος `toImage` αναλαμβάνει τη βαριά δουλειά, μετατρέποντας τα κελιά σε εικονοστοιχεία στο παρασκήνιο.

```java
        // Export the pivot range to a PNG image
        String outputPath = "YOUR_DIRECTORY/pivot.png";
        pivotRange.toImage(outputPath, imgOptions);

        System.out.println("Pivot table exported successfully to " + outputPath);
    }
}
```

> **Αποτέλεσμα που θα δείτε:** Ένα καθαρό `pivot.png` που φαίνεται ακριβώς όπως το pivot στο Excel, πλήρες με slicers, μορφοποίηση υπό όρους και σύνολα. Ανοίξτε το σε οποιονδήποτε προβολέα εικόνων για να το επαληθεύσετε.

## Προαιρετικό – Εξαγωγή Πολλαπλών Pivot Tables ή Συγκεκριμένων Περιοχών

Αν το workbook σας περιέχει πολλαπλά pivots, μπορείτε να τα επαναλάβετε σε βρόχο:

```java
        for (int i = 0; i < worksheet.getPivotTables().getCount(); i++) {
            PivotTable pt = worksheet.getPivotTables().get(i);
            Range rng = pt.getPivotTableRange();
            String fileName = "YOUR_DIRECTORY/pivot_" + i + ".png";
            rng.toImage(fileName, imgOptions);
        }
```

> **Πότε να το χρησιμοποιήσετε:** Δημιουργία μικρογραφιών για μια πύλη αναφορών, ή αρχειοθέτηση κάθε pivot σε ένα οικονομικό μοντέλο. Η ίδια λογική `save range as png` ισχύει—απλώς επαναλάβετε την εντολή μέσα σε βρόχο.

## Συνηθισμένα Προβλήματα & Επαγγελματικές Συμβουλές

| Πρόβλημα | Γιατί συμβαίνει | Διόρθωση |
|----------|----------------|----------|
| **Κενή εικόνα** | `RenderPivotTableStyle` έμεινε `false` ή το pivot είναι κρυφό. | Βεβαιωθείτε ότι `setRenderPivotTableStyle(true)` και ότι το pivot δεν είναι φιλτραρισμένο ώστε να κρύβει όλες τις γραμμές. |
| **Παραμορφωμένες γραμματοσειρές** | Το DPI προεπιλογή είναι 96, κάτι που μπορεί να φαίνεται μικρό σε οθόνες υψηλής ανάλυσης. | Καλέστε `imgOptions.setResolution(150);` για να αυξήσετε το DPI. |
| **Αρχείο δεν βρέθηκε** | Λάθος διαδρομή `YOUR_DIRECTORY` ή έλλειψη δικαιωμάτων εγγραφής. | Χρησιμοποιήστε `new File("YOUR_DIRECTORY").mkdirs();` πριν από την εξαγωγή. |
| **Έλλειψη μνήμης για τεράστιους pivots** | Μεγάλες περιοχές δημιουργούν τεράστιες bitmap. | Εξάγετε μια μικρότερη περιοχή (`pivotRange.setFirstRow`, `setLastRow`) ή αυξήστε τη μνήμη heap του JVM (`-Xmx2g`). |

## Πλήρες Παράδειγμα Εργασίας (Έτοιμο για Αντιγραφή‑Επικόλληση)

```java
import com.aspose.cells.*;

public class ExportPivotAsPng {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/pt.xlsx");

        // 2️⃣ Access the first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 3️⃣ Get the first pivot table's range
        PivotTable pivotTable = worksheet.getPivotTables().get(0);
        Range pivotRange = pivotTable.getPivotTableRange();

        // 4️⃣ Prepare image options – keep style, set DPI if needed
        ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
        imgOptions.setRenderPivotTableStyle(true);
        imgOptions.setResolution(150);           // optional: sharper image

        // 5️⃣ Export to PNG
        String outPath = "YOUR_DIRECTORY/pivot.png";
        pivotRange.toImage(outPath, imgOptions);

        System.out.println("✅ Pivot exported! Check: " + outPath);
    }
}
```

Εκτελέστε την κλάση, και θα βρείτε το `pivot.png` ακριβώς εκεί που ορίσατε το `YOUR_DIRECTORY`. Ανοίξτε το—μπαμ, μόλις **αποθηκεύσατε την περιοχή ως PNG** χωρίς να βγείτε από το Excel.

## Συμπέρασμα

Συζητήσαμε **πώς να εξάγετε δεδομένα pivot** από ένα βιβλίο εργασίας Excel χρησιμοποιώντας Java, και σας δείξαμε ακριβώς πώς να **αποθηκεύσετε την περιοχή ως PNG** με το στυλ αμετάβλητο. Η διαδικασία είναι απλή: φόρτωση, εντοπισμός, λήψη της περιοχής, ρύθμιση επιλογών εικόνας και εγγραφή του αρχείου. Ακολουθώντας τα παραπάνω βήματα αποφεύγετε κοινά προβλήματα όπως κενές εικόνες ή εξόδους χαμηλής ανάλυσης.

Τι θα ακολουθήσει; Δοκιμάστε να προσθέσετε υδατογραφήματα, να συγχωνεύσετε πολλαπλές εικόνες pivot σε PDF, ή να αυτοματοποιήσετε ολόκληρη τη διαδικασία σε μια υπηρεσία web. Οι ίδιες έννοιες—`Workbook`, `PivotTable`, `ImageOrPrintOptions`—εφαρμόζονται σε αυτά τα σενάρια, έτσι είστε ήδη εξοπλισμένοι να εξερευνήσετε περαιτέρω.

Αν αντιμετωπίσετε κάποιο πρόβλημα, ελέγξτε ξανά τις διαδρομές αρχείων, βεβαιωθείτε ότι χρησιμοποιείτε την πιο πρόσφατη έκδοση του Aspose.Cells, και θυμηθείτε τις επαγγελματικές συμβουλές στον πίνακα. Καλή προγραμματιστική, και εύχομαι οι PNG σας να είναι πάντα καθαρές!

![παράδειγμα εξαγωγής pivot](pivot_export_example.png "παράδειγμα εξαγωγής pivot – Java Aspose.Cells PNG εξαγωγή")

## Τι Θα Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετικές θεματικές που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να Εξάγετε ένα Worksheet Excel σε PNG Χρησιμοποιώντας Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)
- [Εξαγωγή Excel Workbook ως Εικόνα Χρησιμοποιώντας Aspose.Cells for Java: Οδηγός Βήμα‑Βήμα](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)
- [Πώς να Δημιουργήσετε Pivot Tables στο Excel Χρησιμοποιώντας Aspose.Cells for Java: Αναλυτικός Οδηγός](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}