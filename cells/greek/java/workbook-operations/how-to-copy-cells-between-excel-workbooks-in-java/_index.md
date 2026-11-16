---
category: general
date: 2026-11-16
description: Πώς να αντιγράψετε κελιά μεταξύ βιβλίων εργασίας Excel σε Java – φορτώστε
  ένα βιβλίο εργασίας, αντιγράψτε μια περιοχή μεταξύ βιβλίων εργασίας (συμπεριλαμβανομένου
  ενός πίνακα Pivot) και αποθηκεύστε το αρχείο του βιβλίου εργασίας.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy cells
- copy range between workbooks
- copy pivot table workbook
- save workbook file
- load excel workbook java
language: el
lastmod: 2026-11-16
og_description: Πώς να αντιγράψετε κελιά μεταξύ βιβλίων εργασίας Excel σε Java. Μάθετε
  πώς να φορτώνετε ένα βιβλίο εργασίας Excel, να αντιγράφετε μια περιοχή (συμπεριλαμβανομένου
  ενός πίνακα Pivot) μεταξύ βιβλίων εργασίας και να αποθηκεύετε το αρχείο του βιβλίου
  εργασίας.
og_image_alt: Screenshot of Java code copying a cell range from one Excel workbook
  to another
og_title: Πώς να αντιγράψετε κελιά μεταξύ βιβλίων εργασίας Excel σε Java – πλήρης
  οδηγός
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: How to copy cells between Excel workbooks in Java – load a workbook,
    copy range between workbooks (including a pivot table), and save the workbook
    file.
  headline: How to copy cells between Excel workbooks in Java
  type: TechArticle
- description: How to copy cells between Excel workbooks in Java – load a workbook,
    copy range between workbooks (including a pivot table), and save the workbook
    file.
  name: How to copy cells between Excel workbooks in Java
  steps:
  - name: Load the source workbook
    text: '```java import com.aspose.cells.*;'
  - name: Define the range that includes the pivot table
    text: '```java // Define the cell range that you want to copy. // Adjust "A1:G20"
      to match the area that contains your data/pivot table. Range srcRange = srcWs.getCells().createRange("A1:G20");
      ```'
  - name: Create the destination workbook
    text: '```java // Create a new, empty workbook that will receive the copied range.
      Workbook destWb = new Workbook(); // defaults to a single empty sheet Worksheet
      destWs = destWb.getWorksheets().get(0); ```'
  - name: Copy the range to the destination workbook
    text: '```java // Copy the source range to cell A1 of the destination worksheet.
      destWs.getCells().copyRange(srcRange, destWs.getCells().get("A1")); ```'
  - name: Save the destination workbook
    text: '```java // Save the new workbook to disk. destWb.save("YOUR_DIRECTORY/dest.xlsx");
      } } ```'
  type: HowTo
tags:
- Java
- Excel
- Aspose.Cells
- Workbook manipulation
title: Πώς να αντιγράψετε κελιά μεταξύ βιβλίων εργασίας Excel σε Java
url: /el/java/workbook-operations/how-to-copy-cells-between-excel-workbooks-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να αντιγράψετε κελιά μεταξύ βιβλίων εργασίας Excel σε Java

Αν χρειάζεστε **copy cells** από ένα βιβλίο εργασίας Excel σε άλλο χρησιμοποιώντας Java, αυτός ο οδηγός σας δείχνει έναν αξιόπιστο τρόπο για να το κάνετε. Θα μάθετε πώς να **load Excel workbook Java**, να αντιγράψετε μια περιοχή που μπορεί να περιέχει pivot table, και τελικά να **save workbook file** με τα αντιγραμμένα δεδομένα.

Αυτός ο οδηγός καλύπτει:

* Φόρτωση ενός πηγαίου βιβλίου εργασίας και επιλογή φύλλου εργασίας.  
* Ορισμός της ακριβούς περιοχής που θέλετε να μετακινήσετε (συμπεριλαμβανομένου ενός pivot table).  
* Δημιουργία ενός προορισμού βιβλίου εργασίας και αντιγραφή της περιοχής.  
* Αποθήκευση του αρχείου προορισμού.  

Το παράδειγμα χρησιμοποιεί τη βιβλιοθήκη Aspose.Cells for Java, η οποία λειτουργεί με αρχεία Excel χωρίς να απαιτεί Microsoft Office. Ο κώδικας εκτελείται σε Java 8+ και σε οποιοδήποτε σύγχρονο IDE (IntelliJ IDEA, Eclipse, VS Code, κλ.).

---

## Προαπαιτούμενα

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

| Απαίτηση | Αιτιολογία |
|-------------|--------|
| Java Development Kit (JDK) 8 or newer | Απαιτείται για τη μεταγλώττιση και εκτέλεση του κώδικα. |
| Maven or Gradle build tool | Απλοποιεί την προσθήκη της εξάρτησης Aspose.Cells. |
| Aspose.Cells for Java library (latest version) | Παρέχει τις κλάσεις `Workbook`, `Worksheet`, και `Range` που χρησιμοποιούνται στο παράδειγμα. |
| Two Excel files (`source.xlsx` and an empty folder for `dest.xlsx`) | Το αρχείο προέλευσης πρέπει να περιέχει τα δεδομένα και, προαιρετικά, ένα pivot table που θέλετε να αντιγράψετε. |

Προσθέστε την εξάρτηση Aspose.Cells στο `pom.xml` (Maven) ή στο `build.gradle` (Gradle). Παράδειγμα για Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- use the latest version -->
</dependency>
```

---

## Πώς να αντιγράψετε κελιά με Aspose.Cells

Τα παρακάτω βήματα σας καθοδηγούν στη πλήρη διαδικασία. Κάθε βήμα περιλαμβάνει τον κώδικα Java, μια εξήγηση του **Γιατί** το βήμα είναι σημαντικό, και μια συμβουλή για την αποφυγή κοινών παγίδων.

### Βήμα 1: Φόρτωση του πηγαίου βιβλίου εργασίας

```java
import com.aspose.cells.*;

public class ExcelCopyDemo {
    public static void main(String[] args) throws Exception {
        // Load the source Excel file (replace with your actual path)
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");

        // Get the first worksheet (index 0)
        Worksheet srcWs = srcWb.getWorksheets().get(0);
```

**Γιατί;**  
`Workbook` αντιπροσωπεύει ολόκληρο το αρχείο Excel. Η φόρτωσή του σας δίνει πρόσβαση σε όλα τα φύλλα εργασίας, τα κελιά και αντικείμενα όπως τα pivot tables. Η χρήση του πρώτου φύλλου είναι κοινή, αλλά μπορείτε να επιλέξετε οποιοδήποτε φύλλο με το όνομα (`srcWb.getWorksheets().get("Sheet2")`).

**Συμβουλή:**  
Αν το πηγαίο αρχείο είναι μεγάλο, σκεφτείτε να το φορτώσετε σε *memory‑efficient* λειτουργία: `new Workbook("file.xlsx", new LoadOptions(LoadFormat.XLSX) {{ setMemorySetting(MemorySetting.MEMORY_PREFERENCE); }});`

### Βήμα 2: Ορισμός της περιοχής που περιλαμβάνει το pivot table

```java
        // Define the cell range that you want to copy.
        // Adjust "A1:G20" to match the area that contains your data/pivot table.
        Range srcRange = srcWs.getCells().createRange("A1:G20");
```

**Γιατί;**  
Ένα αντικείμενο `Range` αφηρημένα αναπαριστά ένα ορθογώνιο μπλοκ κελιών. Καθορίζοντας το `"A1:G20"` λέτε στο Aspose.Cells ακριβώς ποια κελιά—συμπεριλαμβανομένου οποιουδήποτε ενσωματωμένου pivot table—να αντιγράψει. Η βιβλιοθήκη αντιγράφει αυτόματα τα υποκείμενα δεδομένα, τα στυλ και τους ορισμούς του pivot.

**Ακραία περίπτωση:**  
Αν το pivot table εκτείνεται πέρα από την καθορισμένη περιοχή, επεκτείνετε τη διεύθυνση (π.χ., `"A1:Z100"`). Μπορείτε επίσης να χρησιμοποιήσετε `srcWs.getCells().getMaxDataColumn()` και `getMaxDataRow()` για να υπολογίσετε δυναμικά την χρησιμοποιημένη περιοχή.

### Βήμα 3: Δημιουργία του προορισμού βιβλίου εργασίας

```java
        // Create a new, empty workbook that will receive the copied range.
        Workbook destWb = new Workbook();               // defaults to a single empty sheet
        Worksheet destWs = destWb.getWorksheets().get(0);
```

**Γιατί;**  
Ένα νέο βιβλίο εργασίας εξασφαλίζει ότι δεν θα υπάρξει ανεπιθύμητη μορφοποίηση ή κρυφά φύλλα που θα επηρεάσουν το αντιγραμμένο περιεχόμενο. Το προεπιλεγμένο βιβλίο εργασίας περιέχει ήδη ένα φύλλο, το οποίο θα χρησιμοποιήσουμε ως προορισμό.

### Βήμα 4: Αντιγραφή της περιοχής στο προορισμό βιβλίου εργασίας

```java
        // Copy the source range to cell A1 of the destination worksheet.
        destWs.getCells().copyRange(srcRange, destWs.getCells().get("A1"));
```

**Γιατί;**  
`copyRange` διαχειρίζεται όλα τα χαρακτηριστικά των κελιών: τιμές, τύπους, μορφοποίηση και ακόμη και τις κρυφές μνήμες του pivot. Αντιγράφοντας στο `"A1"` τοποθετείτε την περιοχή στην επάνω‑αριστερή γωνία του προορισμού φύλλου, διατηρώντας την αρχική διάταξη.

**Συχνή ερώτηση:** *Will the pivot table remain functional?*  
Ναι. Το Aspose.Cells αντιγράφει τον ορισμό του pivot table και τη μνήμη του, έτσι το pivot λειτουργεί ακριβώς όπως στο πηγαίο βιβλίο εργασίας.

### Βήμα 5: Αποθήκευση του προορισμού βιβλίου εργασίας

```java
        // Save the new workbook to disk.
        destWb.save("YOUR_DIRECTORY/dest.xlsx");
    }
}
```

**Γιατί;**  
Καλώντας το `save` γράφει το βιβλίο εργασίας στη μνήμη σε ένα φυσικό αρχείο `.xlsx`. Μπορείτε επίσης να αποθηκεύσετε σε άλλες μορφές (`.xls`, `.csv`, `.pdf`) αλλάζοντας την επέκταση του αρχείου ή χρησιμοποιώντας το `SaveOptions`.

**Συμβουλή:**  
Αν χρειάζεται να μεταφέρετε το αρχείο ως ροή σε απάντηση web, χρησιμοποιήστε `destWb.save(OutputStream, SaveFormat.XLSX);` αντί για διαδρομή αρχείου.

---

## Αντιγραφή περιοχής μεταξύ βιβλίων εργασίας – πλήρης κώδικας πηγής

Παρακάτω βρίσκεται η πλήρης, έτοιμη προς εκτέλεση κλάση Java. Αντικαταστήστε το `YOUR_DIRECTORY` με τον πραγματικό φάκελο στο μηχάνημά σας.

```java
import com.aspose.cells.*;

public class ExcelCopyDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // Define the range that includes the data and pivot table
        Range srcRange = srcWs.getCells().createRange("A1:G20");

        // Create a new destination workbook
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);

        // Copy the defined range to the destination workbook
        destWs.getCells().copyRange(srcRange, destWs.getCells().get("A1"));

        // Save the destination workbook
        destWb.save("YOUR_DIRECTORY/dest.xlsx");
    }
}
```

**Αναμενόμενο αποτέλεσμα:**  
`dest.xlsx` περιέχει ένα ακριβές αντίγραφο της περιοχής `A1:G20` από το `source.xlsx`. Αν η πηγαία περιοχή περιείχε pivot table, το αρχείο προορισμού εμφανίζει το ίδιο pivot με την πηγή δεδομένων σωστά συνδεδεμένη στα αντιγραμμένα κελιά.

Μπορείτε να ανοίξετε το `dest.xlsx` σε Excel, LibreOffice ή οποιονδήποτε προβολέα που υποστηρίζει `.xlsx` για να επαληθεύσετε ότι οι τιμές, η μορφοποίηση και η λειτουργικότητα του pivot διατηρούνται.

---

## Αντιγραφή βιβλίου εργασίας pivot table – τι πρέπει να γνωρίζετε

* **Pivot cache is copied automatically.** Η βιβλιοθήκη μεταφέρει τη βασική μνήμη, έτσι το pivot δεν χρειάζεται να ανανεωθεί χειροκίνητα.
* **External data sources are not transferred.** Αν το pivot αντλεί δεδομένα από εξωτερική βάση, πρέπει να διασφαλίσετε ότι το βιβλίο προορισμού μπορεί να έχει πρόσβαση στην ίδια πηγή, ή να δημιουργήσετε ξανά τη μνήμη τοπικά.
* **Large pivot tables may increase memory usage.** Για πολύ μεγάλα βιβλία εργασίας, σκεφτείτε να αυξήσετε τη μνήμη heap της JVM (`-Xmx2g`) για να αποφύγετε `OutOfMemoryError`.

---

## Αποθήκευση αρχείου βιβλίου εργασίας σε διαφορετικές μορφές

Το Aspose.Cells σας επιτρέπει να αποθηκεύσετε το αποτέλεσμα σε πολλές μορφές χωρίς επιπλέον αλλαγές κώδικα:

```java
// Save as XLS (Excel 97-2003)
destWb.save("dest.xls");

// Save as CSV (first worksheet only)
destWb.save("dest.csv");

// Save as PDF (visual representation)
destWb.save("dest.pdf");
```

Επιλέξτε τη μορφή που ταιριάζει στη διαδικασία σας. Η ίδια λογική `copyRange` λειτουργεί ανεξάρτητα από την τελική μορφή.

---

## Φόρτωση Excel workbook Java – πρόσθετες συμβουλές

* **Loading encrypted files:** Χρησιμοποιήστε `LoadOptions` με κωδικό πρόσβασης:  
  ```java
  LoadOptions opt = new LoadOptions(LoadFormat.XLSX);
  opt.setPassword("myPassword");
  Workbook wb = new Workbook("encrypted.xlsx", opt);
  ```
* **Reading only specific sheets:**  
  ```java
  LoadOptions opt = new LoadOptions(LoadFormat.XLSX);
  opt.setLoadDataOnly(true); // faster if you only need values
  Workbook wb = new Workbook("file.xlsx", opt);
  ```

Αυτές οι επιλογές μπορούν να επιταχύνουν το βήμα **load excel workbook java**, ειδικά για μεγάλα αρχεία.

---

## Συμπέρασμα

Τώρα γνωρίζετε **how to copy cells** μεταξύ βιβλίων εργασίας Excel σε Java, πώς να **copy range between workbooks** που περιέχει **pivot table**, και πώς να **save workbook file** στη μορφή που χρειάζεστε. Ακολουθώντας τα παραπάνω βήματα, μπορείτε να ενσωματώσετε τη διαχείριση δεδομένων Excel σε οποιαδήποτε εφαρμογή Java—είτε δημιουργείτε μηχανή αναφορών, pipeline ETL, ή απλό εργαλείο μετατροπής αρχείων.

**Next steps** που μπορείτε να εξερευνήσετε:

* Χρησιμοποιήστε **copy range between workbooks** για συγχώνευση πολλαπλών αναφορών σε

## Τι Θα Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που βασίζονται στις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Save New Workbook in Java – Copy Range Between Workbooks Tutorial](/cells/english/java/workbook-operations/save-new-workbook-in-java-copy-range-between-workbooks-tutor/)
- [How to copy pivot tables between Excel workbooks in Java](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-tables-between-excel-workbooks-in-java/)
- [How to copy range in Java – Copy Pivot Table with Aspose.Cells](/cells/english/java/excel-pivot-tables/how-to-copy-range-in-java-copy-pivot-table-with-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}