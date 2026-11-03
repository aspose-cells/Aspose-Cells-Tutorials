---
category: general
date: 2026-10-01
description: Μάθετε πώς να αντιγράφετε πίνακες Pivot μεταξύ βιβλίων εργασίας Excel
  χρησιμοποιώντας Java. Αυτός ο οδηγός βήμα‑βήμα δείχνει επίσης πώς να αντιγράψετε
  περιοχές μεταξύ βιβλίων εργασίας και να δημιουργήσετε αντίγραφα ασφαλώς των περιοχών
  Excel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot
- copy range between workbooks
- how to copy excel
- duplicate excel range
- copy range to workbook
language: el
lastmod: 2026-10-01
og_description: Πώς να αντιγράψετε πίνακες Pivot μεταξύ βιβλίων εργασίας Excel χρησιμοποιώντας
  Java. Ακολουθήστε αυτόν τον οδηγό για να αντιγράψετε περιοχή σε βιβλίο εργασίας,
  να αντιγράψετε περιοχές Excel και να διατηρήσετε τα δεδομένα Pivot.
og_image_alt: Screenshot of Java code that copies a pivot table from one Excel workbook
  to another
og_title: Πώς να αντιγράψετε πίνακες Pivot μεταξύ βιβλίων εργασίας Excel σε Java –
  πλήρης οδηγός
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to copy pivot tables between Excel workbooks using Java.
    This step‑by‑step guide also shows how to copy range between workbooks and duplicate
    Excel ranges safely.
  headline: How to copy pivot tables between Excel workbooks in Java
  type: TechArticle
- description: Learn how to copy pivot tables between Excel workbooks using Java.
    This step‑by‑step guide also shows how to copy range between workbooks and duplicate
    Excel ranges safely.
  name: How to copy pivot tables between Excel workbooks in Java
  steps:
  - name: Expected output
    text: '* Console: `Pivot table copied successfully.` * `destination.xlsx` opens
      in Excel with a pivot table identical to the one in `source.xlsx`. Refreshing
      the pivot shows the same data source, proving that **how to copy pivot** works
      as intended.'
  - name: Copying multiple worksheets
    text: If your project requires copying several sheets, loop through the workbook’s
      worksheets and repeat steps 2‑4 for each sheet. The pivot in each sheet will
      be preserved independently.
  - name: Preserving external data connections
    text: Pivot tables that rely on external data sources keep the connection string
      after copying. However, the destination file must have access to the same data
      source. Verify the connection by opening the pivot and checking the **Data**
      tab.
  - name: Dealing with merged cells
    text: If the source range contains merged cells, Aspose.Cells copies the merge
      layout automatically. Still, validate the result if the destination workbook
      uses a different default column width.
  type: HowTo
tags:
- Excel
- Java
- Aspose.Cells
- Pivot table
- Data manipulation
title: Πώς να αντιγράψετε δυναμικούς πίνακες μεταξύ βιβλίων εργασίας Excel σε Java
url: /el/java/excel-pivot-tables/how-to-copy-pivot-tables-between-excel-workbooks-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να αντιγράψετε πίνακες Pivot μεταξύ βιβλίων εργασίας Excel σε Java

Αν χρειάζεστε **how to copy pivot** πίνακες από ένα αρχείο Excel σε άλλο, αυτός ο οδηγός σας παρέχει μια έτοιμη προς εκτέλεση λύση. Μέχρι το τέλος των πρώτων δύο προτάσεων θα γνωρίζετε ακριβώς ποιες κλήσεις API διατηρούν τον ορισμό του pivot ενώ αντιγράφετε το εύρος δεδομένων.

Θα μάθετε επίσης πώς να **copy range between workbooks**, **duplicate Excel range** αντικείμενα, και με ασφάλεια **copy range to workbook** χωρίς να χάσετε τύπους ή μορφοποίηση. Δεν απαιτούνται εξωτερικά σενάρια — απλώς ένα μόνο έργο Java που χρησιμοποιεί το Aspose.Cells for Java.

## Προαπαιτούμενα

* Java Development Kit 17 ή νεότερο.
* Maven ή Gradle για τη διαχείριση εξαρτήσεων.
* Έγκυρη άδεια Aspose.Cells for Java (η δωρεάν δοκιμαστική έκδοση λειτουργεί για δοκιμές).
* Δύο αρχεία Excel: `source.xlsx` (περιέχει τον πίνακα pivot) και ένα κενό `destination.xlsx` (ή αφήστε τον κώδικα να το δημιουργήσει).

## Βήμα 1: Ρύθμιση του έργου Maven

Δημιουργήστε ένα `pom.xml` που περιλαμβάνει το Aspose.Cells. Αυτή η εξάρτηση σας παρέχει τις κλάσεις `Workbook`, `Worksheet` και `Range` που χρησιμοποιούνται στο παράδειγμα.

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" 
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 
         http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.example</groupId>
    <artifactId>excel-pivot-copy</artifactId>
    <version>1.0.0</version>
    <properties>
        <java.version>17</java.version>
    </properties>

    <dependencies>
        <dependency>
            <groupId>com.aspose</groupId>
            <artifactId>aspose-cells</artifactId>
            <version>24.10</version> <!-- latest at time of writing -->
        </dependency>
    </dependencies>
</project>
```

> **Pro tip:** Διατηρήστε την έκδοση του Aspose.Cells ενημερωμένη· οι νεότερες εκδόσεις προσφέρουν καλύτερη υποστήριξη για σύνθετες δομές cache pivot.

## Βήμα 2: Φόρτωση του πηγαίου βιβλίου εργασίας που περιέχει τον πίνακα pivot

Το πρώτο μπλοκ κώδικα δείχνει **how to copy excel** δεδομένα φορτώνοντας το πηγαίο αρχείο. Ο κατασκευαστής `Workbook` διαβάζει ολόκληρο το αρχείο στη μνήμη, διατηρώντας όλα τα αντικείμενα φύλλων, συμπεριλαμβανομένων των pivot.

```java
import com.aspose.cells.*;

public class PivotCopyDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook containing the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");

        // Access the first worksheet (index 0) where the pivot resides
        Worksheet srcWs = srcWb.getWorksheets().get(0);
```

*Γιατί είναι σημαντικό:* Το Aspose.Cells αποθηκεύει τους πίνακες pivot ως μέρος του εσωτερικού μοντέλου του φύλλου εργασίας. Η φόρτωση του βιβλίου εργασίας εξασφαλίζει ότι η cache του pivot είναι διαθέσιμη για μετέπειτα αντιγραφή.

## Βήμα 3: Ορισμός του εύρους που περιλαμβάνει τον πίνακα pivot

Ένας πίνακας pivot μπορεί να εκτείνεται σε πολλές γραμμές και στήλες. Στις περισσότερες περιπτώσεις μπορείτε να αντιγράψετε ολόκληρο το χρησιμοποιημένο εύρος του φύλλου. Η μέθοδος `createRange` δημιουργεί ένα αντικείμενο `Range` που θα διαχειριστεί η λειτουργία αντιγραφής.

```java
        // Define the range to copy – includes the pivot table and its source data
        // Adjust the address if your pivot occupies a different block
        Range srcRange = srcWs.getCells().createRange("A1:H20");
```

Αν το pivot επεκταθεί πέρα από το `H20`, απλώς αλλάξτε τη συμβολοσειρά διεύθυνσης. Αυτό το βήμα είναι ο πυρήνας της διαχείρισης **duplicate excel range**· το αντικείμενο range γνωρίζει τους τύπους, τα στυλ και τις κρυφές γραμμές.

## Βήμα 4: Δημιουργία νέου βιβλίου εργασίας που θα λάβει το αντιγραμμένο εύρος

Μπορείτε είτε να ξεκινήσετε με ένα κενό βιβλίο εργασίας είτε να φορτώσετε ένα υπάρχον αρχείο προορισμού. Εδώ δημιουργούμε ένα νέο βιβλίο εργασίας, που είναι ο πιο καθαρός τρόπος για **copy range to workbook**.

```java
        // Create a new workbook for the destination
        Workbook destWb = new Workbook(); // starts with one default sheet
        Worksheet destWs = destWb.getWorksheets().get(0);
```

> **Note:** Αν χρειάζεται να αντιγράψετε το pivot σε ένα συγκεκριμένο όνομα φύλλου, μετονομάστε το `destWs` με `destWs.setName("Report")` πριν την επικόλληση.

## Βήμα 5: Αντιγραφή του εύρους – το Aspose.Cells διατηρεί αυτόματα το pivot

Η μέθοδος `copy` μεταφέρει όλα τα στοιχεία εντός του πηγαίου εύρους, συμπεριλαμβανομένου του ορισμού του pivot, της cache και της μορφοποίησης. Δεν απαιτείται επιπλέον κώδικας για να παραμείνει λειτουργικό το pivot.

```java
        // Copy the range to the destination worksheet; pivot tables are preserved automatically
        srcRange.copy(destWs.getCells().createRange("A1"));
```

*Γιατί λειτουργεί:* Το Aspose.Cells αντιμετωπίζει το pivot ως μια συλλογή κρυφών κελιών και μεταδεδομένων που είναι συνδεδεμένα με το εύρος. Όταν καλείτε το `copy`, η βιβλιοθήκη αντιγράφει αυτά τα μεταδεδομένα στο βιβλίο εργασίας προορισμού.

## Βήμα 6: Αποθήκευση του βιβλίου εργασίας προορισμού

Τέλος, γράψτε το αποτέλεσμα στο δίσκο. Το αποθηκευμένο αρχείο περιέχει έναν ταυτόσημο πίνακα pivot που μπορείτε να ανανεώσετε ή να τροποποιήσετε όπως το αρχικό.

```java
        // Save the destination workbook
        destWb.save("YOUR_DIRECTORY/destination.xlsx");

        System.out.println("Pivot table copied successfully.");
    }
}
```

Η εκτέλεση του προγράμματος εκτυπώνει μια επιβεβαίωση και δημιουργεί το `destination.xlsx` με έναν πλήρως λειτουργικό pivot.

## Πλήρες, εκτελέσιμο παράδειγμα

Συνδυάζοντας όλα τα βήματα, η πλήρης κλάση Java φαίνεται ως εξής:

```java
import com.aspose.cells.*;

public class PivotCopyDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load source workbook with pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // 2️⃣ Define the range that contains the pivot and its source data
        Range srcRange = srcWs.getCells().createRange("A1:H20");

        // 3️⃣ Prepare destination workbook (blank by default)
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);

        // 4️⃣ Copy range – pivot table is kept intact
        srcRange.copy(destWs.getCells().createRange("A1"));

        // 5️⃣ Save the new file
        destWb.save("YOUR_DIRECTORY/destination.xlsx");
        System.out.println("Pivot table copied successfully.");
    }
}
```

### Αναμενόμενη έξοδος

* Κονσόλα: `Pivot table copied successfully.`
* Το `destination.xlsx` ανοίγει στο Excel με έναν πίνακα pivot ταυτόσημο με αυτόν του `source.xlsx`. Η ανανέωση του pivot εμφανίζει την ίδια πηγή δεδομένων, αποδεικνύοντας ότι το **how to copy pivot** λειτουργεί όπως προβλέπεται.

## Διαχείριση κοινών παραλλαγών

### Αντιγραφή πολλαπλών φύλλων εργασίας

Αν το έργο σας απαιτεί την αντιγραφή πολλών φύλλων, κάντε βρόχο μέσω των φύλλων εργασίας του βιβλίου και επαναλάβετε τα βήματα 2‑4 για κάθε φύλλο. Το pivot σε κάθε φύλλο θα διατηρηθεί ανεξάρτητα.

```java
for (int i = 0; i < srcWb.getWorksheets().getCount(); i++) {
    Worksheet src = srcWb.getWorksheets().get(i);
    Worksheet dest = destWb.getWorksheets().add();
    src.getCells().copy(dest.getCells());
}
```

### Διατήρηση εξωτερικών συνδέσεων δεδομένων

Οι πίνακες pivot που βασίζονται σε εξωτερικές πηγές δεδομένων διατηρούν τη συμβολοσειρά σύνδεσης μετά την αντιγραφή. Ωστόσο, το αρχείο προορισμού πρέπει να έχει πρόσβαση στην ίδια πηγή δεδομένων. Επαληθεύστε τη σύνδεση ανοίγοντας το pivot και ελέγχοντας την καρτέλα **Data**.

### Διαχείριση συγχωνευμένων κελιών

Αν το πηγαίο εύρος περιέχει συγχωνευμένα κελιά, το Aspose.Cells αντιγράφει αυτόματα τη διάταξη συγχώνευσης. Παρόλα αυτά, επαληθεύστε το αποτέλεσμα αν το βιβλίο προορισμού χρησιμοποιεί διαφορετικό προεπιλεγμένο πλάτος στήλης.

## Καλές πρακτικές για αξιόπιστη αντιγραφή

| Πρακτική | Αιτία |
|----------|--------|
| Χρησιμοποιήστε το ακριβές χρησιμοποιημένο εύρος (`srcWs.getCells().getMaxDisplayRange()`) αντί για σκληρά κωδικοποιημένη διεύθυνση | Εγγυάται ότι περιλαμβάνονται ολόκληρος ο pivot και τα δεδομένα πηγής του. |
| Εφαρμόστε άδεια πριν από βαριές λειτουργίες | Αποτρέπει το υδατογράφημα αξιολόγησης και βελτιώνει την απόδοση. |
| Ανανεώστε το pivot μετά την αντιγραφή (`pivotTable.refresh()`) εάν τα δεδομένα πηγής έχουν αλλάξει | Εξασφαλίζει ότι ο προορισμός αντανακλά τις τελευταίες τιμές. |
| Γράψτε μονάδες δοκιμών που ανοίγουν το βιβλίο εργασίας προορισμού και ελέγχουν ότι το `pivotTable.getPivotFields().size()` ταιριάζει με το πηγαίο | Ανιχνεύει τυχαία απώλεια πεδίων κατά τις μελλοντικές αλλαγές κώδικα. |

## Συμπέρασμα

Τώρα γνωρίζετε **how to copy pivot** πίνακες μεταξύ βιβλίων εργασίας Excel σε Java, καθώς και πώς να **copy range between workbooks**, **duplicate excel range**, και **copy range to workbook** διατηρώντας όλη τη μορφοποίηση και τους τύπους. Το παράδειγμα χρησιμοποιεί το Aspose.Cells, το οποίο αφαιρεί την ανάγκη για χαμηλού επιπέδου διαχείριση XML που απαιτεί το OpenXML SDK.

Στη συνέχεια, εξερευνήστε συναφή θέματα όπως **updating pivot cache programmatically**, **exporting pivot data to CSV**, ή **creating pivot tables from scratch**. Κάθε ένα από αυτά βασίζεται στις ίδιες έννοιες που παρουσιάζονται εδώ.

Καλό κώδικα, και μη διστάσετε να πειραματιστείτε με μεγαλύτερα εύρη, πολλαπλά pivots ή προσαρμοσμένο στυλ — το ίδιο μοτίβο ισχύει για όλα τα σενάρια.

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που βασίζονται στις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κυριαρχήσετε σε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να δημιουργήσετε πίνακες Pivot στο Excel χρησιμοποιώντας το Aspose.Cells for Java: Ένας ολοκληρωμένος οδηγός](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [Πώς να αντιγράψετε πολλαπλές στήλες στο Excel χρησιμοποιώντας το Aspose.Cells Java: Ένας πλήρης οδηγός](/cells/english/java/range-management/copy-multiple-columns-excel-aspose-cells-java/)
- [Αντιγραφή εικόνων μεταξύ φύλλων στο Excel χρησιμοποιώντας το Aspose.Cells for Java: Ένας ολοκληρωμένος οδηγός](/cells/english/java/images-shapes/copy-images-between-sheets-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}