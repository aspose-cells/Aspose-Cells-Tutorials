---
category: general
date: 2026-09-27
description: Μάθετε πώς να αφαιρέσετε το autofilter από το Excel χρησιμοποιώντας το
  Aspose.Cells για Java. Οδηγός βήμα‑προς‑βήμα για την εκκαθάριση του autofilter σε
  βιβλίο εργασίας, την αφαίρεση του φίλτρου πίνακα Excel και την αποθήκευση του αρχείου.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- remove autofilter from excel
- remove excel table filter
- remove filter from excel table
- clear autofilter in workbook
language: el
lastmod: 2026-09-27
og_description: Αφαιρέστε το αυτόματο φίλτρο από το Excel χρησιμοποιώντας το Aspose.Cells
  για Java. Αυτό το σεμινάριο δείχνει πώς να καθαρίσετε το αυτόματο φίλτρο σε ένα
  βιβλίο εργασίας, να αφαιρέσετε το φίλτρο πίνακα Excel και να αποθηκεύσετε το ενημερωμένο
  αρχείο.
og_image_alt: Screenshot of an Excel worksheet after remove autofilter from excel
  using Java
og_title: Αφαίρεση του αυτόματου φίλτρου από το Excel με το Aspose.Cells Java – πλήρης
  οδηγός
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Learn how to remove autofilter from Excel using Aspose.Cells for Java.
    Step‑by‑step guide to clear autofilter in workbook, remove excel table filter
    and save the file.
  headline: How to remove autofilter from Excel with Aspose.Cells Java
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel
- AutoFilter
title: Πώς να αφαιρέσετε το autofilter από το Excel με το Aspose.Cells Java
url: /el/java/data-manipulation/how-to-remove-autofilter-from-excel-with-aspose-cells-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να αφαιρέσετε το autofilter από το Excel με το Aspose.Cells για Java

Αν χρειάζεται να αφαιρέσετε το autofilter από το Excel, αυτός ο οδηγός δείχνει τα ακριβή βήματα που μπορείτε να ακολουθήσετε με το Aspose.Cells για Java. Θα δείτε πώς να καθαρίσετε το autofilter σε ένα βιβλίο εργασίας, να διαγράψετε το φίλτρο που είναι προσαρτημένο σε έναν πίνακα Excel και να αποθηκεύσετε το αποτέλεσμα χωρίς να χάσετε δεδομένα.

Η εργασία με το Excel προγραμματιστικά συχνά σημαίνει διαχείριση πινάκων που ήδη περιέχουν φίλτρα. Η αφαίρεση αυτών των φίλτρων αποτρέπει τυχαία απόκρυψη δεδομένων όταν επεξεργάζεστε αργότερα το βιβλίο εργασίας. Αυτό το tutorial καλύπτει όλα όσα χρειάζεστε: απαιτούμενες βιβλιοθήκες, εξήγηση κώδικα, διαχείριση ειδικών περιπτώσεων και επαλήθευση του τελικού αρχείου.

## Προαπαιτούμενα

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

* Java Development Kit 8 ή νεότερο.
* Maven ή Gradle για διαχείριση εξαρτήσεων (το παράδειγμα χρησιμοποιεί Maven).
* Aspose.Cells for Java 23.8 ή νεότερη – μπορείτε να αποκτήσετε δωρεάν προσωρινή άδεια από την ιστοσελίδα της Aspose.
* Ένα δείγμα βιβλίου εργασίας (`TableWithFilter.xlsx`) που περιέχει έναν πίνακα με εφαρμοσμένο AutoFilter.

## Βήμα 1: Ρύθμιση του έργου Maven

Δημιουργήστε ένα αρχείο `pom.xml` (ή προσθέστε στο υπάρχον έργο σας) και συμπεριλάβετε την εξάρτηση Aspose.Cells:

```xml
<project>
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>ExcelFilterRemoval</artifactId>
    <version>1.0.0</version>
    <dependencies>
        <dependency>
            <groupId>com.aspose</groupId>
            <artifactId>aspose-cells</artifactId>
            <version>23.8</version>
        </dependency>
    </dependencies>
</project>
```

Η προσθήκη της εξάρτησης εξασφαλίζει ότι οι κλάσεις `com.aspose.cells.*` είναι διαθέσιμες κατά τη μεταγλώττιση. Αφού αποθηκεύσετε το αρχείο, εκτελέστε `mvn clean install` για να κατεβάσετε τη βιβλιοθήκη.

## Βήμα 2: Φόρτωση του βιβλίου εργασίας που περιέχει έναν φιλτραρισμένο πίνακα

Η πρώτη γραμμή κώδικα δημιουργεί μια παρουσία `Workbook` που δείχνει στο αρχείο προέλευσης. Η φόρτωση του βιβλίου εργασίας στη μνήμη είναι απαραίτητη πριν μπορέσετε να αλληλεπιδράσετε με οποιοδήποτε αντικείμενο φύλλου.

```java
import com.aspose.cells.*;

public class RemoveAutoFilter {
    public static void main(String[] args) throws Exception {
        // Load the workbook that contains a table with an AutoFilter
        Workbook workbook = new Workbook("YOUR_DIRECTORY/TableWithFilter.xlsx");
```

Αν το αρχείο δεν υπάρχει, το Aspose.Cells ρίχνει `FileNotFoundException`. Επαληθεύστε τη διαδρομή και το όνομα του αρχείου πριν τρέξετε το πρόγραμμα.

## Βήμα 3: Πρόσβαση στο φύλλο εργασίας που περιέχει τον πίνακα

Τα περισσότερα βιβλία εργασίας έχουν ένα προεπιλεγμένο φύλλο στη θέση 0. Μπορείτε επίσης να ανακτήσετε ένα φύλλο με το όνομά του αν το βιβλίο εργασίας περιέχει πολλά φύλλα.

```java
        // Access the first worksheet (where the table resides)
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

Η σωστή επιλογή του φύλλου είναι κρίσιμη επειδή η `removeAutoFilter` λειτουργεί σε ένα `ListObject` (τον πίνακα) που βρίσκεται μέσα σε ένα συγκεκριμένο φύλλο.

## Βήμα 4: Εντοπισμός του ListObject (πίνακα Excel) και αφαίρεση του φίλτρου του

Ένα `ListObject` αντιπροσωπεύει έναν πίνακα Excel. Η μέθοδος `removeAutoFilter` διαγράφει το στοιχείο UI του AutoFilter που είναι προσαρτημένο σε αυτόν τον πίνακα. Αν ο πίνακας δεν έχει φίλτρο, η μέθοδος δεν κάνει τίποτα, καθιστώντας την ασφαλή για επαναλαμβανόμενη εκτέλεση.

```java
        // Retrieve the first ListObject (table) from the worksheet
        ListObject table = worksheet.getListObjects().get(0);

        // Remove the AutoFilter element from the table
        table.removeAutoFilter();
```

**Γιατί είναι σημαντικό αυτό το βήμα:**  
* Η `removeAutoFilter` καθαρίζει τα βέλη φίλτρου και τυχόν κρυμμένες γραμμές που προκλήθηκαν από το φίλτρο.  
* Τα υποκείμενα δεδομένα παραμένουν αμετάβλητα, ώστε να μπορείτε ακόμη να διαβάζετε ή να τροποποιείτε τις γραμμές προγραμματιστικά.  
* Αν αργότερα χρειαστεί να εφαρμόσετε ξανά φίλτρο, μπορείτε να καλέσετε ξανά `table.setAutoFilter()`.

### Διαχείριση πολλαπλών πινάκων

Αν το φύλλο εργασίας περιέχει περισσότερους από έναν πίνακα, επαναλάβετε τη συλλογή:

```java
        for (int i = 0; i < worksheet.getListObjects().getCount(); i++) {
            worksheet.getListObjects().get(i).removeAutoFilter();
        }
```

Αυτός ο βρόχος εξασφαλίζει ότι **remove excel table filter** εφαρμόζεται σε κάθε πίνακα, αποτρέποντας κρυμμένες γραμμές σε μεγαλύτερα βιβλία εργασίας.

## Βήμα 5: Αποθήκευση του βιβλίου εργασίας χωρίς το AutoFilter

Αφού το φίλτρο καθαριστεί, γράψτε το βιβλίο εργασίας σε νέο αρχείο. Η μέθοδος `save` υποστηρίζει πολλές μορφές· το παράδειγμα αποθηκεύει ως αρχείο `.xlsx`.

```java
        // Save the modified workbook without the AutoFilter
        workbook.save("YOUR_DIRECTORY/TableNoFilter.xlsx");
    }
}
```

Η αποθήκευση δημιουργεί ένα καθαρό αντίγραφο (`TableNoFilter.xlsx`) που δεν εμφανίζει πλέον βέλη φίλτρου. Ανοίξτε το αρχείο στο Excel για να επιβεβαιώσετε ότι **remove filter from excel table** ήταν επιτυχές.

## Πλήρες, εκτελέσιμο παράδειγμα

Συνδυάζοντας όλα τα βήματα παίρνετε ένα αυτόνομο πρόγραμμα που μπορείτε να μεταγλωττίσετε και να τρέξετε:

```java
import com.aspose.cells.*;

public class RemoveAutoFilter {
    public static void main(String[] args) throws Exception {
        // 1. Load the workbook containing a filtered table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/TableWithFilter.xlsx");

        // 2. Get the first worksheet (adjust index if needed)
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 3. Remove AutoFilter from each table on the sheet
        for (int i = 0; i < worksheet.getListObjects().getCount(); i++) {
            worksheet.getListObjects().get(i).removeAutoFilter();
        }

        // 4. Save the workbook – the AutoFilter is now cleared
        workbook.save("YOUR_DIRECTORY/TableNoFilter.xlsx");
    }
}
```

**Αναμενόμενη έξοδος:**  
Όταν ανοίξετε το `TableNoFilter.xlsx` στο Microsoft Excel, τα βέλη του φίλτρου έχουν εξαφανιστεί και όλες οι γραμμές είναι ορατές. Δεν χάθηκαν δεδομένα και το βιβλίο εργασίας συμπεριφέρεται ακριβώς όπως ένα αρχείο που δεν είχε ποτέ AutoFilter.

## Συχνές ερωτήσεις και διαχείριση ειδικών περιπτώσεων

| Ερώτηση | Απάντηση |
|----------|--------|
| *Τι γίνεται αν το βιβλίο εργασίας δεν έχει πίνακες;* | Η κλήση `getListObjects().getCount()` επιστρέφει 0, οπότε ο βρόχος τερματίζει χωρίς σφάλμα. |
| *Μπορώ να αφαιρέσω το φίλτρο μόνο από μια συγκεκριμένη στήλη;* | Το Aspose.Cells δεν εκθέτει αφαίρεση σε επίπεδο στήλης· πρέπει να καθαρίσετε ολόκληρο το AutoFilter του πίνακα. |
| *Επηρεάζει η `removeAutoFilter` τη μορφοποίηση υπό όρους;* | Όχι. Η μορφοποίηση υπό όρους παραμένει αμετάβλητη επειδή η μέθοδος αγγίζει μόνο το UI του φίλτρου. |
| *Είναι η λειτουργία γρήγορη για μεγάλα βιβλία εργασίας;* | Ναι. Η αφαίρεση του φίλτρου είναι λειτουργία O(1) ανά πίνακα· το κυρίαρχο κόστος είναι η φόρτωση και η αποθήκευση του βιβλίου εργασίας. |
| *Χρειάζομαι άδεια για παραγωγική χρήση;* | Μια έγκυρη άδεια Aspose.Cells αφαιρεί τα υδατογράμματα αξιολόγησης και ενεργοποιεί πλήρη απόδοση. |

## Pro tips

* **Άδεια νωρίς** – καλέστε `License license = new License(); license.setLicense("Aspose.Total.Java.lic");` πριν φορτώσετε το βιβλίο εργασίας για να αποφύγετε το banner αξιολόγησης.  
* **Επεξεργασία κατά παρτίδες** – όταν επεξεργάζεστε δεκάδες αρχεία, επαναχρησιμοποιήστε μία μόνο παρουσία `Workbook` φορτώνοντας, καθαρίζοντας, αποθηκεύοντας και στη συνέχεια καλώντας `workbook.dispose();` για απελευθέρωση μνήμης.  
* **Σκριπτ επαλήθευσης** – μετά την αποθήκευση, μπορείτε προγραμματιστικά να επιβεβαιώσετε ότι το φίλτρο έχει αφαιρεθεί:

```java
Workbook check = new Workbook("YOUR_DIRECTORY/TableNoFilter.xlsx");
boolean hasFilter = check.getWorksheets().get(0).getListObjects().get(0).isAutoFilterEnabled();
System.out.println("Filter present? " + hasFilter); // should print false
```

## Συμπέρασμα

Τώρα ξέρετε πώς να **remove autofilter from Excel** χρησιμοποιώντας το Aspose.Cells για Java, πώς να **remove excel table filter** για κάθε πίνακα σε ένα φύλλο εργασίας, και πώς να **clear autofilter in workbook** πριν αποθηκεύσετε το αρχείο. Το πλήρες παράδειγμα κώδικα δείχνει ένα αξιόπιστο μοτίβο που μπορείτε να ενσωματώσετε σε μεγαλύτερα pipelines αυτοματοποίησης, εργαλεία μετεγκατάστασης δεδομένων ή υπηρεσίες αναφορών.

Επόμενα βήματα που μπορείτε να εξερευνήσετε:

* Προσθήκη επικύρωσης δεδομένων μετά τον καθαρισμό του φίλτρου.  
* Εξαγωγή του καθαρισμένου βιβλίου εργασίας σε CSV ή PDF.  
* Χρήση του Aspose.Cells για προγραμματιστική εφαρμογή νέου φίλτρου βάσει επιχειρηματικών κανόνων.

Μη διστάσετε να πειραματιστείτε με διαφορετικές δομές βιβλίου εργασίας και να μοιραστείτε τα ευρήματά σας στα σχόλια. Καλή προγραμματιστική διασκέδαση!

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε επιπλέον δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Clear filter UI in Excel with C# – Remove AutoFilter Button](/cells/english/net/excel-autofilter-validation/clear-filter-ui-in-excel-with-c-remove-autofilter-button/)
- [Implement 'Ends With' Autofilter in Excel Using Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/data-analysis/aspose-cells-java-autofilter-ends-with/)
- [Implement AutoFilter 'Begins With' in Excel using Aspose.Cells Java](/cells/english/java/data-analysis/implement-autofilter-begins-with-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}