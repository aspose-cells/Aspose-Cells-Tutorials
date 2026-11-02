---
category: general
date: 2026-08-11
description: Πώς να αφαιρέσετε το αυτόματο φίλτρο στο Excel με το Aspose.Cells για
  Java – μάθετε πώς να αφαιρέσετε το αυτόματο φίλτρο από το Excel, να απενεργοποιήσετε
  το αυτόματο φίλτρο στο Excel και να αφαιρέσετε το φίλτρο του Excel προγραμματιστικά.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to clear autofilter
- remove autofilter from excel
- remove excel filter
- how to remove autofilter
- disable autofilter in excel
language: el
lastmod: 2026-08-11
og_description: Πώς να καθαρίσετε το αυτόματο φίλτρο στο Excel χρησιμοποιώντας το
  Aspose.Cells για Java. Ακολουθήστε αυτό το πλήρες σεμινάριο για να αφαιρέσετε το
  αυτόματο φίλτρο από το Excel, να απενεργοποιήσετε το αυτόματο φίλτρο στο Excel και
  να καθαρίσετε τα φύλλα εργασίας σας.
og_image_alt: Screenshot showing Java code that clears an autofilter in an Excel file
  with Aspose.Cells
og_title: Πώς να διαγράψετε το αυτόματο φίλτρο στο Excel με το Aspose.Cells (Java)
  – οδηγός βήμα‑προς‑βήμα
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: How to clear autofilter in Excel with Aspose.Cells for Java – learn
    to remove autofilter from Excel, disable autofilter in Excel, and remove Excel
    filter programmatically.
  headline: How to clear autofilter in Excel with Aspose.Cells (Java)
  type: TechArticle
- description: How to clear autofilter in Excel with Aspose.Cells for Java – learn
    to remove autofilter from Excel, disable autofilter in Excel, and remove Excel
    filter programmatically.
  name: How to clear autofilter in Excel with Aspose.Cells (Java)
  steps:
  - name: '`TableWithFilter.xlsx` remains unchanged.'
    text: '`TableWithFilter.xlsx` remains unchanged.'
  - name: '`NoAutoFilter.xlsx` contains the same data, but the AutoFilter drop‑down
      arrows are no longer visible.'
    text: '`NoAutoFilter.xlsx` contains the same data, but the AutoFilter drop‑down
      arrows are no longer visible.'
  - name: If you open the file, the **remove autofilter from excel** operation will
      be evident in the UI (no filter icons on column headers).
    text: If you open the file, the **remove autofilter from excel** operation will
      be evident in the UI (no filter icons on column headers).
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Πώς να καθαρίσετε το autofilter στο Excel με το Aspose.Cells (Java)
url: /el/java/worksheet-management/how-to-clear-autofilter-in-excel-with-aspose-cells-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να αφαιρέσετε το autofilter στο Excel με το Aspose.Cells (Java)

Η αφαίρεση του autofilter στο Excel με το Aspose.Cells για Java είναι μια κοινή ανάγκη όταν δημιουργείτε αναφορές προγραμματιστικά. Αυτός ο οδηγός σας δείχνει πώς να αφαιρέσετε το autofilter από φύλλα εργασίας Excel γρήγορα και με ασφάλεια, ώστε το τελικό αρχείο να φαίνεται καθαρό για τους τελικούς χρήστες.

Θα δείτε ένα πλήρες, εκτελέσιμο παράδειγμα που φορτώνει ένα βιβλίο εργασίας, προσπελαύνει τον πρώτο πίνακα, καθαρίζει το AutoFilter και αποθηκεύει το αποτέλεσμα. Ο οδηγός καλύπτει επίσης παραλλαγές όπως η διαχείριση πολλαπλών πινάκων, η εργασία με παλαιότερες εκδόσεις του Aspose.Cells και η αποφυγή κοινών παγίδων. Δεν απαιτείται εξωτερική τεκμηρίωση — απλώς αντιγράψτε τον κώδικα, προσαρμόστε τις διαδρομές αρχείων και τρέξτε.

## Προαπαιτούμενα

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

* Java 8 ή νεότερη έκδοση εγκατεστημένη.
* Aspose.Cells for Java 25.11 ή νεότερη (η μέθοδος `clear()` προστέθηκε στην 25.11).
* Ένα αρχείο Excel (`TableWithFilter.xlsx`) που περιέχει έναν πίνακα με ενεργό AutoFilter.
* Ένα περιβάλλον ανάπτυξης (IDE, Maven/Gradle ή απλό `javac`).

Αν χρησιμοποιείτε Maven, προσθέστε την εξάρτηση:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.11</version>
    <classifier>jdk17</classifier> <!-- adjust for your JDK version -->
</dependency>
```

## Πώς να αφαιρέσετε το autofilter στο Excel χρησιμοποιώντας το Aspose.Cells

Παρακάτω βρίσκεται το πλήρες πρόγραμμα Java. Κάθε βήμα περιλαμβάνει μια σύντομη εξήγηση «γιατί», ώστε να κατανοήσετε τη ροή του API, όχι μόνο τη σύνταξη.

```java
import com.aspose.cells.*;

public class RemoveAutoFilter {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the workbook that contains a table with an AutoFilter
        Workbook workbook = new Workbook("YOUR_DIRECTORY/TableWithFilter.xlsx");

        // Step 2: Access the first worksheet (index 0)
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Step 3: Retrieve the first ListObject (table) on the worksheet
        // ListObject represents an Excel table; it holds the AutoFilter object.
        ListObject table = worksheet.getListObjects().get(0);

        // Step 4: Clear the AutoFilter applied to the table (new API in 25.11)
        // The clear() method removes the filter criteria and disables the drop‑down arrows.
        table.getAutoFilter().clear();

        // Step 5: Save the modified workbook without the AutoFilter
        workbook.save("YOUR_DIRECTORY/NoAutoFilter.xlsx");
    }
}
```

### Γιατί κάθε γραμμή είναι σημαντική

| Βήμα | Σκοπός |
|------|--------|
| **Φόρτωση του βιβλίου εργασίας** | Ανοίγει το αρχείο Excel στη μνήμη ώστε το Aspose.Cells να μπορεί να χειριστεί το περιεχόμενό του. |
| **Πρόσβαση στο φύλλο εργασίας** | Τα αρχεία Excel μπορούν να περιέχουν πολλά φύλλα· χρειάζεστε το σωστό για να εργαστείτε με τον πίνακα. |
| **Ανάκτηση του ListObject** | Ένα ListObject είναι η προγραμματιστική αναπαράσταση ενός πίνακα Excel. Ο πίνακας κρατά το αντικείμενο AutoFilter. |
| **Καθαρισμός του AutoFilter** | `clear()` αφαιρεί τα κριτήρια φίλτρου και κρύβει τα βέλη φίλτρου. Αυτή είναι η κύρια λειτουργία για *remove autofilter from excel*. |
| **Αποθήκευση του βιβλίου εργασίας** | Γράφει τις αλλαγές πίσω στο δίσκο, παράγοντας ένα αρχείο όπου το φίλτρο είναι απενεργοποιημένο. |

## Αφαίρεση φίλτρου Excel από πολλαπλούς πίνακες (προαιρετικό)

Αν το βιβλίο εργασίας σας περιέχει περισσότερους από έναν πίνακες, επαναλάβετε τη συλλογή `ListObjects`:

```java
Worksheet ws = workbook.getWorksheets().get(0);
for (int i = 0; i < ws.getListObjects().getCount(); i++) {
    ListObject tbl = ws.getListObjects().get(i);
    tbl.getAutoFilter().clear();   // disables filter for each table
}
```

Αυτό το απόσπασμα κώδικα δείχνει **how to remove autofilter** από κάθε πίνακα σε ένα φύλλο, κάτι που είναι χρήσιμο για επεξεργασία παρτίδων αναφορών.

## Διαχείριση βιβλίων εργασίας χωρίς AutoFilter

Κλήση του `clear()` σε έναν πίνακα που δεν έχει φίλτρο δεν προκαλεί εξαίρεση — είναι μια λειτουργία χωρίς αποτέλεσμα. Ωστόσο, αν προσπαθήσετε να προσπελάσετε έναν μη‑υπάρχοντα πίνακα (`get(0)` όταν η συλλογή είναι κενή), το Aspose.Cells θα ρίξει `IndexOutOfRangeException`. Προστατέψτε τον κώδικα με έναν απλό έλεγχο:

```java
if (worksheet.getListObjects().getCount() > 0) {
    ListObject firstTable = worksheet.getListObjects().get(0);
    firstTable.getAutoFilter().clear();
}
```

Αυτό το αμυντικό μοτίβο σας βοηθά να **disable autofilter in excel** με ασφάλεια σε διαφορετικά αρχεία εισόδου.

## Συμβατότητα με παλαιότερες εκδόσεις του Aspose.Cells

Η μέθοδος `clear()` εισήχθη στην έκδοση 25.11. Για παλαιότερες εκδόσεις, πρέπει να επαναφέρετε το εύρος φίλτρου χειροκίνητα:

```java
AutoFilter filter = table.getAutoFilter();
filter.setRange("");               // removes the filter range
filter.setShowFilter(false);       // hides filter arrows
```

Αν και αυτό λειτουργεί, το νεότερο API `clear()` είναι πιο ευανάγνωστο και λιγότερο επιρρεπές σε σφάλματα. Αν μπορείτε να αναβαθμίσετε, κάντε το για να απλοποιήσετε τον κώδικά σας.

## Συνηθισμένα λάθη και επαγγελματικές συμβουλές

* **Διαχωριστές διαδρομής αρχείου** – Χρησιμοποιήστε `File.separator` ή διαγώνιες γραμμές (`/`) για να αποφύγετε προβλήματα ειδικά για πλατφόρμες.
* **Κλείδωμα βιβλίου εργασίας** – Βεβαιωθείτε ότι το πηγαίο αρχείο δεν είναι ανοιχτό στο Excel όταν η διαδικασία Java γράφει σε αυτό· διαφορετικά, το `save()` θα ρίξει `IOException`.
* **Μεγάλα βιβλία εργασίας** – Για αρχεία >100 MB, εξετάστε το ενδεχόμενο χρήσης της παραμέτρου `loadOptions` για να φορτώσετε μόνο τα απαιτούμενα φύλλα, μειώνοντας τη χρήση μνήμης.
* **Δοκιμή του αποτελέσματος** – Ανοίξτε το αποθηκευμένο `NoAutoFilter.xlsx` στο Excel και ελέγξτε ότι τα βέλη του φίλτρου έχουν εξαφανιστεί. Μπορείτε επίσης προγραμματιστικά να ελέγξετε `table.getAutoFilter().isShowFilter()`· θα πρέπει να επιστρέφει `false`.

## Αναμενόμενο αποτέλεσμα

Μετά την εκτέλεση του προγράμματος:

1. `TableWithFilter.xlsx` παραμένει αμετάβλητο.
2. `NoAutoFilter.xlsx` περιέχει τα ίδια δεδομένα, αλλά τα βέλη του AutoFilter δεν είναι πλέον ορατά.
3. Αν ανοίξετε το αρχείο, η λειτουργία **remove autofilter from excel** θα είναι εμφανής στη διεπαφή (χωρίς εικονίδια φίλτρου στις κεφαλίδες των στηλών).

## Πλήρες αρχείο πηγαίου κώδικα για αντιγραφή‑και‑επικόλληση

Αποθηκεύστε το παρακάτω ως `RemoveAutoFilter.java`. Προσαρμόστε το placeholder `YOUR_DIRECTORY` σε απόλυτη ή σχετική διαδρομή στο σύστημά σας.

```java
import com.aspose.cells.*;

public class RemoveAutoFilter {
    public static void main(String[] args) throws Exception {
        // Load the workbook that contains a table with an AutoFilter
        Workbook workbook = new Workbook("YOUR_DIRECTORY/TableWithFilter.xlsx");

        // Access the first worksheet (index 0)
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Retrieve the first ListObject (table) on the worksheet
        ListObject table = worksheet.getListObjects().get(0);

        // Clear the AutoFilter applied to the table (new API in 25.11)
        table.getAutoFilter().clear();

        // Save the modified workbook without the AutoFilter
        workbook.save("YOUR_DIRECTORY/NoAutoFilter.xlsx");
    }
}
```

Συμπιέστε (compile) και εκτελέστε:

```bash
javac -cp "path/to/aspose-cells-25.11.jar" RemoveAutoFilter.java
java -cp ".:path/to/aspose-cells-25.11.jar" RemoveAutoFilter
```

Δεν θα πρέπει να δείτε έξοδο στην κονσόλα εάν όλα ολοκληρωθούν επιτυχώς· το παραγόμενο αρχείο θα βρίσκεται στον ίδιο φάκελο.

## Συμπέρασμα

Τώρα γνωρίζετε **how to clear autofilter** στο Excel χρησιμοποιώντας το Aspose.Cells για Java. Ο οδηγός κάλυψε τα βασικά βήματα, πώς να **remove autofilter from excel** για πολλαπλούς πίνακες, πώς να διαχειριστείτε βιβλία εργασίας χωρίς φίλτρα, και τι να κάνετε όταν χρησιμοποιείτε παλαιότερες εκδόσεις της βιβλιοθήκης. Ακολουθώντας το πλήρες παράδειγμα, μπορείτε να ενσωματώσετε την αφαίρεση φίλτρων σε οποιοδήποτε αυτοματοποιημένο pipeline αναφορών.

**Επόμενα βήματα**

* Εξερευνήστε άλλες δυνατότητες του Aspose.Cells όπως **disable autofilter in excel** διατηρώντας τη μορφοποίηση του πίνακα.
* Συνδυάστε αυτήν την τεχνική με την αφαίρεση επικύρωσης δεδομένων (`ListObject.getValidation().clear()`) για μια πλήρως καθαρή εξαγωγή.
* Ανασκοπήστε την αναφορά API του Aspose.Cells για πρόσθετες επεμβάσεις σε πίνακες, όπως προσθήκη γραμμών ή στυλ κελιών.

Νιώστε ελεύθεροι να πειραματιστείτε με διαφορετικές δομές αρχείων και να μοιραστείτε τα ευρήματά σας. Καλή προγραμματιστική διασκέδαση!

## Τι πρέπει να μάθετε στη συνέχεια;

Οι παρακάτω οδηγίες καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε πρόσθετες λειτουργίες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Αυτοματοποίηση Φίλτρου Excel με Aspose.Cells σε Java: Ένας Πλήρης Οδηγός για την Υλοποίηση AutoFilter Implementation](/cells/english/java/data-analysis/aspose-cells-java-apply-autofilter-excel/)
- [Υλοποίηση AutoFilter 'Ξεκινά με' στο Excel χρησιμοποιώντας Aspose.Cells Java](/cells/english/java/data-analysis/implement-autofilter-begins-with-aspose-cells-java/)
- [Υλοποίηση 'Τελειώνει με' Autofilter στο Excel χρησιμοποιώντας Aspose.Cells for Java: Ένας Πλήρης Οδηγός](/cells/english/java/data-analysis/aspose-cells-java-autofilter-ends-with/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}