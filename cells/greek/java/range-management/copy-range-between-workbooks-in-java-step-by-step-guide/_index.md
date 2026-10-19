---
category: general
date: 2026-08-14
description: Αντιγραφή περιοχής μεταξύ βιβλίων εργασίας με Java χρησιμοποιώντας το
  Aspose.Cells. Μάθετε πώς να αντιγράψετε το βιβλίο εργασίας του Pivot Table, να εξάγετε
  εικόνα στο PowerPoint και να αφαιρέσετε το AutoFilter από τον πίνακα Excel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy range between workbooks
- copy pivot table workbook
- export picture to powerpoint
- copy excel range to new workbook
- remove autofilter from excel table
language: el
lastmod: 2026-08-14
og_description: Αντιγραφή περιοχής μεταξύ βιβλίων εργασίας σε Java. Αυτός ο οδηγός
  δείχνει πώς να αντιγράψετε το βιβλίο εργασίας με τον συγκεντρωτικό πίνακα, να εξάγετε
  εικόνα στο PowerPoint και να αφαιρέσετε το AutoFilter από τον πίνακα του Excel.
og_image_alt: Screenshot of Java code copying range between workbooks with Aspose.Cells
og_title: Αντιγραφή περιοχής μεταξύ βιβλίων εργασίας σε Java – πλήρης οδηγός Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: Copy range between workbooks with Java using Aspose.Cells. Learn to
    copy pivot table workbook, export picture to PowerPoint and remove AutoFilter
    from Excel table.
  headline: Copy range between workbooks in Java – step‑by‑step guide
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
- PowerPoint export
title: Αντιγραφή περιοχής μεταξύ βιβλίων εργασίας σε Java – βήμα‑βήμα οδηγός
url: /el/java/range-management/copy-range-between-workbooks-in-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Αντιγραφή περιοχής μεταξύ βιβλίων εργασίας σε Java – οδηγός βήμα‑βήμα

Αν χρειάζεστε να **αντιγράψετε περιοχή μεταξύ βιβλίων εργασίας** σε Java, το Aspose.Cells παρέχει ένα καθαρό API που διαχειρίζεται σύνθετα αντικείμενα όπως πίνακες Pivot και εικόνες. Αυτό το tutorial δείχνει πώς να **αντιγράψετε βιβλίο εργασίας πίνακα Pivot**, **εξάγετε εικόνα σε PowerPoint**, και **αφαιρέσετε AutoFilter από πίνακα Excel** διατηρώντας τον κώδικα εύκολο στην ανάγνωση και συντήρηση.

Θα μάθετε πώς να:

* Φορτώσετε ένα πηγαίο βιβλίο εργασίας και ορίσετε την πηγαία περιοχή.  
* Δημιουργήσετε ένα προορισμό βιβλίου εργασίας και αντιγράψετε την περιοχή ώστε ο πίνακας Pivot να παραμείνει αμετάβλητος.  
* Εξάγετε την πρώτη εικόνα στο φύλλο ως επεξεργάσιμο αντικείμενο PowerPoint.  
* Αφαιρέσετε ένα AutoFilter από τον πρώτο πίνακα Excel.  
* Φορτώσετε ένα βιβλίο εργασίας με `SmartMarkerOptions` για να αντιμετωπίσετε πίνακες JSON ως μία μόνο τιμή κελιού.

Το παράδειγμα χρησιμοποιεί Aspose.Cells 23.10 για Java, αλλά οι έννοιες ισχύουν και για παλαιότερες εκδόσεις.

---

## Προαπαιτούμενα

| Απαίτηση | Γιατί είναι σημαντικό |
|----------|------------------------|
| Java 17 ή νεότερη | Απαιτείται από το πιο πρόσφατο runtime του Aspose.Cells. |
| Aspose.Cells for Java (Maven artifact `com.aspose:aspose-cells`) | Παρέχει τις κλάσεις `Workbook`, `Worksheet`, `Range` και σχετικές κλάσεις που χρησιμοποιούνται στον κώδικα. |
| Ένα πηγαίο αρχείο Excel (`src.xlsx`) που περιέχει πίνακα Pivot, εικόνα και πίνακα με AutoFilter. | Το tutorial χειρίζεται αυτά τα αντικείμενα για να δείξει κάθε δυνατότητα. |

Προσθέστε την εξάρτηση Maven στο `pom.xml` σας:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

---

## Αντιγραφή περιοχής μεταξύ βιβλίων εργασίας – φόρτωση πηγής και προορισμού

Το πρώτο βήμα είναι να ανοίξετε το πηγαίο βιβλίο εργασίας, να επιλέξετε την περιοχή που περιέχει τα δεδομένα που θέλετε να αντιγράψετε και να δημιουργήσετε ένα κενό βιβλίο εργασίας προορισμού.

```java
import com.aspose.cells.*;

public class CopyRangeDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook that holds the pivot table, picture, and table.
        Workbook sourceWb = new Workbook("YOUR_DIRECTORY/src.xlsx");
        Worksheet sourceWs = sourceWb.getWorksheets().get(0);

        // Define the range that includes the pivot table (A1:G20 in this example).
        Range sourceRange = sourceWs.getCells().createRange("A1:G20");

        // Create a new workbook that will receive the copied range.
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);
        Range destRange = destWs.getCells().createRange("A1");
```

> **Γιατί είναι σημαντικό:** Χρησιμοποιώντας το `Range.copy`, το Aspose.Cells αντιγράφει όχι μόνο τις ακατέργαστες τιμές κελιών αλλά και την υποκείμενη μνήμη cache του Pivot, διατηρώντας λειτουργικό τον πίνακα Pivot στο βιβλίο εργασίας προορισμού.

---

## Αντιγραφή βιβλίου εργασίας πίνακα Pivot κατά την αντιγραφή της περιοχής

Τώρα αντιγράψτε την ορισμένη περιοχή από το πηγαίο βιβλίο εργασίας στο βιβλίο εργασίας προορισμού. Ο πίνακας Pivot διατηρείται αυτόματα επειδή η περιοχή περιλαμβάνει την μνήμη cache του Pivot.

```java
        // Copy the source range to the destination range.
        destRange.copy(sourceRange);

        // Save the intermediate workbook to verify that the pivot table was copied.
        destWb.save("YOUR_DIRECTORY/destination.xlsx");
```

> **Αποτέλεσμα:** Το άνοιγμα του `destination.xlsx` εμφανίζει την ίδια διάταξη πίνακα Pivot με το `src.xlsx`. Δεν απαιτείται επιπλέον κώδικας για την επαναδημιουργία της μνήμης cache του Pivot.

---

## Εξαγωγή εικόνας σε PowerPoint

Το Aspose.Cells μπορεί να επισημάνει μια εικόνα για εξαγωγή σε επεξεργάσιμο αντικείμενο PowerPoint. Ο παρακάτω κώδικας επιλέγει την πρώτη εικόνα στο φύλλο προορισμού και ορίζει τη σημαία εξαγωγής.

```java
        // Retrieve the first picture on the destination sheet.
        Shape picture = destWs.getPictures().get(0);

        // Instruct Aspose.Cells to export this picture as a PowerPoint object.
        picture.getPictureFormat().setExportToPptx(true);

        // Optionally, save the workbook as PPTX to see the result.
        destWb.save("YOUR_DIRECTORY/destination.pptx");
```

> **Τι βλέπετε:** Το άνοιγμα του `destination.pptx` στο PowerPoint εμφανίζει την εικόνα ως εγγενές σχήμα που μπορείτε να επεξεργαστείτε, να αλλάξετε μέγεθος ή να προσθέσετε animation.

---

## Αφαίρεση AutoFilter από πίνακα Excel

Αν το πηγαίο φύλλο περιέχει πίνακα με AutoFilter, μπορεί να θέλετε να το καθαρίσετε μετά την αντιγραφή. Ο παρακάτω κώδικας προσπελαύνει τον πρώτο πίνακα και αφαιρεί το φίλτρο του.

```java
        // Access the first table on the destination sheet.
        Table table = destWs.getTables().get(0);

        // Remove the AutoFilter by assigning null.
        table.setAutoFilter(null);

        // Save the final workbook.
        destWb.save("YOUR_DIRECTORY/final_output.xlsx");
```

> **Επίδραση:** Ο πίνακας παραμένει στο βιβλίο εργασίας, αλλά τα βέλη φίλτρου στην πτυσσόμενη λίστα εξαφανίζονται, προσφέροντας καθαρή προβολή δεδομένων.

---

## Φόρτωση βιβλίου εργασίας με επιλογές SmartMarker – αντιμετώπιση πινάκων JSON ως μία μόνο τιμή κελιού

Όταν δημιουργείτε μια αναφορά από JSON, το Aspose.Cells μπορεί να αντιμετωπίσει ολόκληρο έναν πίνακα ως μία τιμή κελιού. Αυτό είναι χρήσιμο για την ενσωμάτωση συμβολοσειρών JSON σε ένα πρότυπο χωρίς να επεκταθούν σε πολλαπλά κελιά.

```java
        // Configure LoadOptions to enable SmartMarker array handling.
        LoadOptions loadOptions = new LoadOptions();
        SmartMarkerOptions smOptions = new SmartMarkerOptions();
        smOptions.setArrayAsSingle(true);
        loadOptions.setSmartMarkerOptions(smOptions);

        // Load a template workbook using the configured options.
        Workbook smartMarkerWb = new Workbook("YOUR_DIRECTORY/template.xlsx", loadOptions);

        // Continue processing (e.g., populate markers) as needed.
        // ...

        // Save the processed workbook.
        smartMarkerWb.save("YOUR_DIRECTORY/template_filled.xlsx");
    }
}
```

> **Γιατί μπορεί να το χρησιμοποιήσετε:** Αν το JSON payload σας περιέχει έναν πίνακα που πρέπει να εμφανίζεται ως συμβολοσειρά JSON σε ένα μόνο κελί, το `setArrayAsSingle(true)` εμποδίζει το Aspose.Cells να επεκτείνει τον πίνακα σε ξεχωριστές γραμμές ή στήλες.

![Copy range between workbooks in Java – Aspose.Cells code example](copy-range-workbooks.png)

*Image alt text:* **Αντιγραφή περιοχής μεταξύ βιβλίων εργασίας σε Java – παράδειγμα κώδικα Aspose.Cells** (matches the primary keyword).

---

## Αναμενόμενο αποτέλεσμα

| Όνομα αρχείου            | Περιέχει |
|--------------------------|----------|
| `destination.xlsx`       | Αντιγραμμένη περιοχή με λειτουργικό πίνακα Pivot. |
| `destination.pptx`       | Εξαγόμενη εικόνα ως επεξεργάσιμο σχήμα PowerPoint. |
| `final_output.xlsx`      | Πίνακας χωρίς βέλη AutoFilter. |
| `template_filled.xlsx`   | Πίνακας JSON αποθηκευμένος ως μία μόνο τιμή κελιού. |

Ανοίξτε κάθε αρχείο στην αντίστοιχη εφαρμογή (Excel ή PowerPoint) για να επαληθεύσετε ότι οι λειτουργίες ολοκληρώθηκαν επιτυχώς.

---

## Συμπέρασμα

Τώρα γνωρίζετε πώς να **αντιγράψετε περιοχή μεταξύ βιβλίων εργασίας** σε Java χρησιμοποιώντας το Aspose.Cells, διατηρώντας έναν πίνακα Pivot, εξάγοντας εικόνα σε PowerPoint και αφαιρώντας AutoFilter από πίνακα Excel. Το ίδιο μοτίβο μπορεί να επεκταθεί για την αντιγραφή οποιασδήποτε περιοχής Excel σε νέο βιβλίο εργασίας, τη διαχείριση πινάκων JSON με SmartMarker ή την αλυσίδωση πρόσθετων μετασχηματισμών.

Επόμενα βήματα που μπορείτε να εξερευνήσετε:

* **Αντιγραφή περιοχής Excel σε νέο βιβλίο εργασίας** με πολλαπλά φύλλα.  
* Χρησιμοποιήστε **εξαγωγή εικόνας σε PowerPoint** για μαζική εξαγωγή εικόνων.  
* Εφαρμόστε **αφαίρεση autofilter από πίνακα excel** σε μεγαλύτερα pipelines αναφοράς.  
* Συνδυάστε αυτές τις τεχνικές με το Aspose.Slides για πλήρη αυτοματοποίηση Excel‑σε‑PowerPoint.

Νιώστε ελεύθεροι να πειραματιστείτε με διαφορετικές διευθύνσεις περιοχών, πολλαπλούς πίνακες Pivot ή προσαρμοσμένες μορφές εικόνων. Το API του Aspose.Cells έχει σχεδιαστεί για προγραμματιστική ευελιξία, ώστε να μπορείτε να προσαρμόσετε τα δείγματα που παρουσιάζονται εδώ σε οποιοδήποτε σενάριο επιχειρησιακού αυτοματισμού Excel.

## Τι Θα Μάθετε Στη Στη συνέχεια;

Οι παρακάτω οδηγίες καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικά παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Copy Images Between Sheets in Excel Using Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/images-shapes/copy-images-between-sheets-excel-aspose-cells-java/)
- [Copy Page Setup Settings Between Worksheets in Excel Using Aspose.Cells Java](/cells/english/java/headers-footers/copy-page-setup-excel-aspose-cells-java/)
- [Excel Copy Worksheets Between Workbooks](/cells/english/net/excel-copy-worksheet/excel-copy-worksheets-between-workbooks/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}