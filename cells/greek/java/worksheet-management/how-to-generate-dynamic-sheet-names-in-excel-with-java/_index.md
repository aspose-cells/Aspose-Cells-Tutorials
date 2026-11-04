---
category: general
date: 2026-09-27
description: Μάθετε πώς να δημιουργείτε δυναμικά ονόματα φύλλων στο Excel με τη Java,
  ενώ συμπληρώνετε ένα πρότυπο Excel και δημιουργείτε φύλλα από δεδομένα για ισχυρή
  αναφορά.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- dynamic sheet names
- generate multiple sheets
- create sheets from data
- populate excel template java
language: el
lastmod: 2026-09-27
og_description: Δυναμικά ονόματα φύλλων σάς επιτρέπουν να δημιουργείτε πολλαπλά φύλλα
  από ένα σύνολο δεδομένων. Αυτό το σεμινάριο δείχνει πώς να γεμίσετε ένα πρότυπο
  Excel σε Java και να δημιουργήσετε φύλλα από δεδομένα χρησιμοποιώντας το Aspose.Cells.
og_image_alt: Screenshot showing an Excel workbook with dynamically generated sheet
  names using Java
og_title: Δημιουργήστε δυναμικά ονόματα φύλλων στο Excel με Java
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Learn how to generate dynamic sheet names in Excel with Java while
    you populate an Excel template and create sheets from data for robust reporting.
  headline: How to generate dynamic sheet names in Excel with Java
  type: TechArticle
- description: Learn how to generate dynamic sheet names in Excel with Java while
    you populate an Excel template and create sheets from data for robust reporting.
  name: How to generate dynamic sheet names in Excel with Java
  steps:
  - name: Add the Aspose.Cells for Java JAR to your project’s classpath (available
      from Maven Central or the Aspose website).
    text: Add the Aspose.Cells for Java JAR to your project’s classpath (available
      from Maven Central or the Aspose website).
  - name: Place `MasterDetailTemplate.xlsx` in `templates/` relative to the project
      root.
    text: Place `MasterDetailTemplate.xlsx` in `templates/` relative to the project
      root.
  - name: Execute the `main` method. The `output/` folder will contain the generated
      file.
    text: Execute the `main` method. The `output/` folder will contain the generated
      file.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Πώς να δημιουργήσετε δυναμικά ονόματα φύλλων στο Excel με Java
url: /el/java/worksheet-management/how-to-generate-dynamic-sheet-names-in-excel-with-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να δημιουργήσετε δυναμικά ονόματα φύλλων στο Excel με Java

Αν χρειάζεστε **δυναμικά ονόματα φύλλων** όταν συμπληρώνετε ένα πρότυπο Excel σε Java, αυτός ο οδηγός σας καθοδηγεί μέσα από τη διαδικασία. Θα δείτε πώς να *δημιουργήσετε πολλαπλά φύλλα* από μια συλλογή δεδομένων, και πώς κάθε φύλλο λαμβάνει αυτόματα ένα μοναδικό όνομα. Στο τέλος θα έχετε ένα εκτελέσιμο παράδειγμα που δημιουργεί φύλλα από δεδομένα και αποθηκεύει το αποτέλεσμα με την επιθυμητή συμβατότητα ονοματοδοσίας.

Η δημιουργία φύλλων κατά τη διάρκεια εκτέλεσης είναι μια κοινή απαίτηση για πίνακες αναφοράς, παρτίδες τιμολογίων ή οποιοδήποτε σενάριο όπου ο αριθμός των λεπτομερών ενοτήτων δεν είναι γνωστός εκ των προτέρων. Η μηχανή Smart Marker του Aspose.Cells κάνει αυτήν την εργασία σύντομη και αξιόπιστη, και ο παρακάτω κώδικας δείχνει την προτεινόμενη προσέγγιση.

## Χρήση δυναμικών ονομάτων φύλλων με Aspose.Cells

Το Aspose.Cells for Java παρέχει έναν επεξεργαστή **Smart Marker** που μπορεί να διαβάσει placeholders σε ένα πρότυπο βιβλίο εργασίας και να τα επεκτείνει σε σειρές, στήλες ή ακόμη και νέα φύλλα εργασίας. Με τη ρύθμιση του `SmartMarkerOptions.DetailSheetNewName` ελέγχετε το όνομα κάθε παραγόμενου φύλλου. Το placeholder `{0}` αντικαθίσταται με τον μηδενικά‑βασισμένο δείκτη της τρέχουσας σειράς δεδομένων, παρέχοντάς σας πλήρως **δυναμικά ονόματα φύλλων** όπως `Detail_0`, `Detail_1`, …​.

> **Pro tip:** Διατηρήστε το πρότυπο βιβλίο εργασίας σε έναν αφιερωμένο φάκελο πόρων και χρησιμοποιήστε σχετική διαδρομή όποτε είναι δυνατόν. Αυτό αποφεύγει την σκληρή κωδικοποίηση απόλυτων διαδρομών που σπάζουν σε διαφορετικά περιβάλλοντα.

## Βήμα 1: Φόρτωση του προτύπου Excel (populate excel template java)

Αρχικά, φορτώστε το βιβλίο εργασίας που περιέχει τις ετικέτες Smart Marker. Το πρότυπο πρέπει να έχει ένα φύλλο με όνομα, για παράδειγμα, `Detail`, με έναν δείκτη όπως `&=Orders!A1` που λέει στον επεξεργαστή πού να αρχίσει η εισαγωγή σειρών.

```java
import com.aspose.cells.*;

public class DynamicSheetNamesExample {

    public static void main(String[] args) throws Exception {
        // Load the template workbook that already contains Smart Markers.
        // Replace "templates/MasterDetailTemplate.xlsx" with the actual path.
        Workbook templateWorkbook = new Workbook("templates/MasterDetailTemplate.xlsx");
```

*Γιατί αυτό το βήμα είναι σημαντικό:* Το πρότυπο ορίζει τη διάταξη (κεφαλίδες, τύπους, μορφοποίηση) που θα αντιγραφεί σε κάθε παραγόμενο φύλλο. Χωρίς κατάλληλο πρότυπο, η έξοδος θα χάσει το στυλ και τους τύπους.

## Βήμα 2: Προετοιμασία της πηγής δεδομένων για δημιουργία φύλλων από δεδομένα

Στη συνέχεια, δημιουργήστε μια πηγή δεδομένων που ο επεξεργαστής Smart Marker μπορεί να επαναλάβει. Σε αυτό το παράδειγμα χρησιμοποιούμε ένα `Map<String, Object>` όπου το κλειδί `"Orders"` ταιριάζει με το όνομα του δείκτη στο πρότυπο.

```java
        // Prepare a data source with multiple detail rows.
        java.util.Map<String, Object> dataSource = new java.util.HashMap<>();

        // Each element of the Object[] array represents one row.
        dataSource.put("Orders", new Object[] {
            new Object[] { 101, "Alice", 250.00 },
            new Object[] { 102, "Bob",   175.50 },
            new Object[] { 103, "Carol", 320.75 }
        });
```

*Γιατί αυτό το βήμα είναι σημαντικό:* Η μηχανή Smart Marker διαβάζει τον πίνακα, δημιουργεί μια σειρά για κάθε εσωτερικό `Object[]`, και—επειδή θα ζητήσουμε να δημιουργήσει νέα φύλλα—δημιουργεί ξεχωριστό φύλλο εργασίας για κάθε σειρά. Αυτό είναι ο πυρήνας της **δημιουργίας φύλλων από δεδομένα**.

## Βήμα 3: Διαμόρφωση του SmartMarkerOptions για δημιουργία πολλαπλών φύλλων με μοναδικά ονόματα

Τώρα πείτε στο Aspose.Cells πώς να ονομάσει κάθε νέο φύλλο εργασίας. Το placeholder `{0}` αντικαθίσταται με τον τρέχοντα δείκτη σειράς.

```java
        // Configure options so every generated sheet gets a unique name.
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions();
        // {0} → row index (0‑based). Resulting names: Detail_0, Detail_1, …
        smartMarkerOptions.setDetailSheetNewName("Detail_{0}");
```

*Γιατί αυτό το βήμα είναι σημαντικό:* Χωρίς τον ορισμό του `DetailSheetNewName`, ο επεξεργαστής θα επαναχρησιμοποιούσε το αρχικό όνομα φύλλου για κάθε σειρά, αντικαθιστώντας τα δεδομένα. Αυτή η επιλογή είναι αυτή που ενεργοποιεί τα **δυναμικά ονόματα φύλλων**.

## Βήμα 4: Επεξεργασία των SmartMarkers και δημιουργία του βιβλίου εργασίας

Εκτελέστε τον επεξεργαστή με την πηγή δεδομένων και τις επιλογές που μόλις διαμορφώσαμε.

```java
        // Execute the Smart Marker processor.
        templateWorkbook.getSmartMarkerProcessor().process(dataSource, smartMarkerOptions);
```

*Γιατί αυτό το βήμα είναι σημαντικό:* Ο επεξεργαστής επεκτείνει τα markers, δημιουργεί τον απαιτούμενο αριθμό φύλλων εργασίας, αντιγράφει τη διάταξη του προτύπου και γεμίζει κάθε φύλλο με τα αντίστοιχα δεδομένα σειράς.

## Βήμα 5: Αποθήκευση και επαλήθευση του αποτελέσματος

Τέλος, γράψτε το βιβλίο εργασίας στο δίσκο. Ανοίξτε το αρχείο στο Excel για να δείτε τα αυτόματα δημιουργημένα φύλλα.

```java
        // Save the workbook containing the newly generated sheets.
        templateWorkbook.save("output/MasterDetailResult.xlsx");
    }
}
```

**Expected output**

Όταν ανοίξετε το `MasterDetailResult.xlsx` θα πρέπει να δείτε τρία νέα φύλλα εργασίας:

* `Detail_0` – περιέχει την παραγγελία 101 (Alice, 250.00)  
* `Detail_1` – περιέχει την παραγγελία 102 (Bob, 175.50)  
* `Detail_2` – περιέχει την παραγγελία 103 (Carol, 320.75)

Κάθε φύλλο διατηρεί τη μορφοποίηση, το πλάτος των στηλών και τυχόν τύπους που υπήρχαν στο αρχικό φύλλο προτύπου `Detail`.

## Πλήρες εκτελέσιμο παράδειγμα

Συνδυάζοντας όλα τα τμήματα μαζί, έχετε ένα αυτόνομο πρόγραμμα που μπορείτε να μεταγλωττίσετε και να εκτελέσετε:

```java
import com.aspose.cells.*;

public class DynamicSheetNamesExample {

    public static void main(String[] args) throws Exception {
        // 1. Load the template workbook that contains Smart Markers.
        Workbook templateWorkbook = new Workbook("templates/MasterDetailTemplate.xlsx");

        // 2. Prepare the data source with multiple detail rows.
        java.util.Map<String, Object> dataSource = new java.util.HashMap<>();
        dataSource.put("Orders", new Object[] {
            new Object[] { 101, "Alice", 250.00 },
            new Object[] { 102, "Bob",   175.50 },
            new Object[] { 103, "Carol", 320.75 }
        });

        // 3. Configure SmartMarkerOptions to give each generated sheet a unique name.
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions();
        smartMarkerOptions.setDetailSheetNewName("Detail_{0}");

        // 4. Process the Smart Markers using the data source and the configured options.
        templateWorkbook.getSmartMarkerProcessor().process(dataSource, smartMarkerOptions);

        // 5. Save the resulting workbook with the newly created sheets.
        templateWorkbook.save("output/MasterDetailResult.xlsx");
    }
}
```

### Πώς να εκτελέσετε

1. Προσθέστε το JAR του Aspose.Cells for Java στο classpath του έργου σας (διαθέσιμο από το Maven Central ή την ιστοσελίδα της Aspose).  
2. Τοποθετήστε το `MasterDetailTemplate.xlsx` στο `templates/` σχετικά με τη ρίζα του έργου.  
3. Εκτελέστε τη μέθοδο `main`. Ο φάκελος `output/` θα περιέχει το παραγόμενο αρχείο.

## Συνηθισμένες παραλλαγές και ειδικές περιπτώσεις

| Situation | What to change |
|-----------|----------------|
| **Διαφορετικό πρότυπο ονοματοδοσίας** | Χρησιμοποιήστε `"OrderSheet_{0}_v{1}"` και συμπεριλάβετε πρόσθετα placeholders όπως `{1}` για έναν δεύτερο δείκτη (π.χ., αριθμός σελίδας). |
| **Μεγάλα σύνολα δεδομένων** | Αυξήστε τη μνήμη heap της JVM (`-Xmx2g`) για να αποφύγετε `OutOfMemoryError` όταν δημιουργείτε εκατοντάδες φύλλα. |
| **Δημιουργία φύλλων υπό συνθήκη** | Πριν καλέσετε το `process`, φιλτράρετε τον πίνακα δεδομένων ώστε οι σειρές που δεν πληρούν ένα κριτήριο να παραλειφθούν, αποτρέποντας έτσι περιττά φύλλα. |
| **Διατήρηση τύπων που αναφέρονται σε άλλα φύλλα** | Διατηρήστε το αρχικό όνομα φύλλου ως κρυφό placeholder (π.χ., `DetailTemplate`) και χρησιμοποιήστε το `SmartMarkerOptions.setDetailSheetNewName` μόνο για το ορατό όνομα· οι τύποι που αναφέρονται στο κρυφό όνομα θα εξακολουθούν να λύνουν σωστά. |

## Συμβουλές για αξιόπιστη αυτοματοποίηση Excel

* **Validate the data source** – Βεβαιωθείτε ότι κάθε εσωτερικός πίνακας έχει τον ίδιο αριθμό στοιχείων με τις στήλες που ορίζονται στο πρότυπο· διαφορετικά μήκη προκαλούν σφάλματα χρόνου εκτέλεσης.  
* **Use named ranges** – Στο πρότυπο χρησιμοποιήστε ονομασμένες περιοχές για πιο σαφή σύνταξη Smart Marker (`&=Orders!A1`).  
* **Close resources** – Αν και το Aspose.Cells διαχειρίζεται τις ροές εσωτερικά, η ρητή κλήση του `templateWorkbook.dispose()` σε ένα `finally` block μπορεί να ελευθερώσει τη φυσική μνήμη πιο γρήγορα.  
* **Test with edge values** – Μηδενικές σειρές πρέπει να παράγουν ένα βιβλίο εργασίας μόνο με το αρχικό φύλλο προτύπου· μια κενή πηγή δεδομένων επαληθεύει ότι ο κώδικάς σας διαχειρίζεται το “χωρίς δεδομένα” ομαλά.

## Συμπέρασμα

Τώρα γνωρίζετε πώς να **δημιουργήσετε δυναμικά ονόματα φύλλων** στο Excel χρησιμοποιώντας Java, πώς να **συμπληρώσετε ένα πρότυπο Excel** και **να δημιουργήσετε φύλλα από δεδομένα**, και πώς να **δημιουργήσετε πολλαπλά φύλλα** αυτόματα με τα Smart Markers του Aspose.Cells. Ακολουθώντας τα παραπάνω βήματα μπορείτε να προσαρμόσετε το πρότυπο σε οποιοδήποτε σενάριο αναφοράς—είτε χρειάζεστε δεκάδες φύλλα λεπτομερειών, προσαρμοσμένες συμβάσεις ονοματοδοσίας, ή δημιουργία φύλλων υπό συνθήκη.

Έτοιμοι να επεκτείνετε αυτή τη λύση; Δοκιμάστε να προσθέσετε γραφήματα σε κάθε παραγόμενο φύλλο ή να εξάγετε το βιβλίο εργασίας σε PDF χρησιμοποιώντας `Workbook.save("result.pdf", SaveFormat.PDF)`. Και οι δύο τεχνικές βασίζονται στην ίδια βάση των δυναμικών φύλλων που μόλις κατακτήσατε. Καλή προγραμματιστική!

## Τι Θα Πρέπει Να Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Κατακτήστε τα Δυναμικά Φύλλα Excel σε Java με Aspose.Cells: Ένας Πλήρης Οδηγός](/cells/english/java/formulas-functions/dynamic-excel-sheets-aspose-cells-java-guide/)
- [Οδηγός Δυναμικών Φύλλων Excel Aspose Cells Java](/cells/german/java/formulas-functions/dynamic-excel-sheets-aspose-cells-java-guide/)
- [Οδηγός Δυναμικών Φύλλων Excel Aspose Cells Java](/cells/french/java/formulas-functions/dynamic-excel-sheets-aspose-cells-java-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}