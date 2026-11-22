---
category: general
date: 2026-11-22
description: Αφαιρέστε το autofilter από τον πίνακα στο Excel χρησιμοποιώντας Java.
  Μάθετε πώς να απενεργοποιήσετε το autofilter στο Excel, να φορτώσετε ένα βιβλίο
  εργασίας Excel με Java και να κρύψετε το autofilter στο Excel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- remove autofilter from table
- disable autofilter in excel
- load excel workbook java
- how to hide autofilter in excel
language: el
lastmod: 2026-11-22
og_description: Αφαιρέστε το αυτόματο φίλτρο από πίνακα στο Excel χρησιμοποιώντας
  Java. Αυτό το σεμινάριο δείχνει πώς να απενεργοποιήσετε το αυτόματο φίλτρο στο Excel,
  να φορτώσετε ένα βιβλίο εργασίας Excel με Java και να κρύψετε το αυτόματο φίλτρο
  στο Excel.
og_image_alt: Java code snippet that removes autofilter from an Excel table
og_title: Αφαίρεση του αυτόματου φίλτρου από πίνακα στο Excel – Οδηγός Java
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Remove autofilter from table in Excel using Java. Learn to disable
    autofilter in Excel, load Excel workbook Java, and hide autofilter in Excel.
  headline: How to remove autofilter from table in Excel using Java
  type: TechArticle
tags:
- Excel
- Java
- Aspose.Cells
- Automation
title: Πώς να αφαιρέσετε το αυτόματο φίλτρο από πίνακα στο Excel χρησιμοποιώντας Java
url: /el/java/spreadsheet-automation/how-to-remove-autofilter-from-table-in-excel-using-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να αφαιρέσετε το autofilter από πίνακα στο Excel χρησιμοποιώντας Java

Αν χρειάζεται να **αφαιρέσετε το autofilter από πίνακα** σε ένα βιβλίο εργασίας Excel, αυτός ο οδηγός σας δείχνει ακριβώς πώς. Θα μάθετε να **απενεργοποιήσετε το autofilter στο Excel**, να φορτώσετε το βιβλίο εργασίας με Java και, προαιρετικά, να κρύψετε τα βέλη φίλτρου για πιο καθαρή εμφάνιση.

Το tutorial καλύπτει όλα, από τη ρύθμιση του έργου μέχρι την αποθήκευση του τροποποιημένου αρχείου, ώστε να μπορείτε να ενσωματώσετε τη λύση σε οποιοδήποτε pipeline αναφορών ή επεξεργασίας δεδομένων βασισμένο σε Java.

## Προαπαιτούμενα

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

* Java 17 ή νεότερη εγκατεστημένη.
* Τη βιβλιοθήκη Aspose.Cells for Java (έκδοση 23.12 ή νεότερη). Μπορείτε να την αποκτήσετε από την [Aspose website](https://purchase.aspose.com/).
* Βασική κατανόηση του προγραμματισμού Java και της δομής αρχείων Excel.

> **Pro tip:** Αν προτιμάτε μια ανοιχτού κώδικα εναλλακτική, το Apache POI μπορεί επίσης να χειριστεί πίνακες, αλλά το API για έλεγχο autofilter σε επίπεδο πίνακα διαφέρει. Ο κώδικας παρακάτω χρησιμοποιεί το Aspose.Cells επειδή παρέχει τη βολική μέθοδο `Table.setShowAutoFilter`.

## Βήμα 1: Φόρτωση βιβλίου εργασίας Excel με Java

Η πρώτη ενέργεια είναι η φόρτωση του υπάρχοντος βιβλίου εργασίας στη μνήμη. Αυτό το βήμα είναι απαραίτητο επειδή όλες οι επόμενες αλλαγές εξαρτώνται από ένα έγκυρο αντικείμενο `Workbook`.

```java
import com.aspose.cells.*;

public class RemoveAutoFilter {
    public static void main(String[] args) throws Exception {
        // Path to the source workbook
        String inputPath = "YOUR_DIRECTORY/input.xlsx";

        // Load the workbook (load Excel workbook Java)
        Workbook wb = new Workbook(inputPath);
```

*Γιατί είναι σημαντικό:* Η φόρτωση του βιβλίου εργασίας αναλύει τη μορφή του αρχείου, δημιουργεί το εσωτερικό μοντέλο αντικειμένων και προετοιμάζει τη συλλογή φύλλων εργασίας για επεξεργασία. Αν το αρχείο δεν βρεθεί, το Aspose.Cells ρίχνει `FileNotFoundException`, οπότε βεβαιωθείτε ότι η διαδρομή είναι σωστή.

## Βήμα 2: Πρόσβαση στο στόχο φύλλου εργασίας

Τα περισσότερα βιβλία εργασίας περιέχουν περισσότερα από ένα φύλλο. Πρέπει να αναφερθείτε στο φύλλο που περιέχει τον πίνακα που θέλετε να τροποποιήσετε.

```java
        // Access the first worksheet (index 0)
        Worksheet ws = wb.getWorksheets().get(0);
```

*Γιατί είναι σημαντικό:* Τα φύλλα εργασίας είναι μηδενικής βάσης, έτσι το `get(0)` επιστρέφει το πρώτο φύλλο. Αν ο πίνακάς σας βρίσκεται σε διαφορετικό φύλλο, προσαρμόστε το δείκτη ή χρησιμοποιήστε `get("SheetName")`.

## Βήμα 3: Ανάκτηση του συγκεκριμένου πίνακα

Οι πίνακες Excel αποθηκεύονται σε μια συλλογή που συνδέεται με κάθε φύλλο εργασίας. Μπορείτε να ανακτήσετε έναν πίνακα με βάση τη θέση ή το όνομά του.

```java
        // Retrieve the first table on the worksheet
        Table tbl = ws.getTables().get(0);
```

*Γιατί είναι σημαντικό:* Το αντικείμενο `Table` σας δίνει άμεσο έλεγχο στις λειτουργίες επιπέδου πίνακα, συμπεριλαμβανομένης της ορατότητας του βέλους autofilter. Αν το φύλλο εργασίας περιέχει πολλούς πίνακες, επαναλάβετε μέσω `ws.getTables()` και επιλέξτε τον κατάλληλο.

## Βήμα 4: Απενεργοποίηση autofilter στο Excel

Τώρα μπορείτε να απενεργοποιήσετε τα βέλη φίλτρου που εμφανίζονται στην κεφαλίδα του πίνακα.

```java
        // Disable the AutoFilter feature for the table (remove autofilter from table)
        tbl.setShowAutoFilter(false);
```

*Γιατί είναι σημαντικό:* Ορίζοντας το `ShowAutoFilter` σε `false` κρύβει τα βέλη χωρίς να επηρεάζει τα υποκείμενα δεδομένα. Αυτή είναι η κύρια ενέργεια που **αφαιρεί το autofilter από πίνακα**.

## Βήμα 5: Αποθήκευση του τροποποιημένου βιβλίου εργασίας

Μετά την αλλαγή των ρυθμίσεων του πίνακα, αποθηκεύστε το βιβλίο εργασίας σε νέο αρχείο (ή αντικαταστήστε το αρχικό).

```java
        // Optional: Save the workbook with the updated settings
        String outputPath = "YOUR_DIRECTORY/output.xlsx";
        wb.save(outputPath);
    }
}
```

*Γιατί είναι σημαντικό:* Η αποθήκευση γράφει τις αλλαγές στη μνήμη στο δίσκο. Το παραγόμενο αρχείο θα ανοίξει στο Excel με τα βέλη autofilter κρυμμένα, επιτυγχάνοντας τον στόχο του **πώς να κρύψετε το autofilter στο Excel**.

## Διαχείριση κοινών σεναρίων

| Σενάριο | Σε τι πρέπει να προσέξετε | Προτεινόμενη προσέγγιση |
|----------|-------------------|----------------------|
| Πολλοί πίνακες στο ίδιο φύλλο | `ws.getTables().get(0)` επηρεάζει μόνο τον πρώτο πίνακα. | Επανάληψη μέσω `ws.getTables()` και αντιστοίχιση με `tbl.getName()` ή δείκτη. |
| Ο πίνακας δεν έχει ήδη autofilter | Η κλήση `setShowAutoFilter(false)` είναι idempotent. | Δεν απαιτείται επιπλέον κώδικας· η μέθοδος αφήνει την κατάσταση αμετάβλητη. |
| Μεγάλο βιβλίο εργασίας (> 50 MB) | Η φόρτωση ολόκληρου του αρχείου μπορεί να καταναλώσει μνήμη. | Χρησιμοποιήστε `Workbook.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` πριν τη φόρτωση. |
| Απαιτείται επανενεργοποίηση αργότερα | Μπορεί να θέλετε να εναλλάξετε τη ρύθμιση. | Κλήση `tbl.setShowAutoFilter(true)` όταν χρειαστεί ξανά το φίλτρο. |

## Αναμενόμενο αποτέλεσμα

Όταν ανοίξετε το `output.xlsx` στο Microsoft Excel:

* Η γραμμή κεφαλίδας του πίνακα δεν εμφανίζει πλέον τα βέλη φίλτρου.
* Όλα τα δεδομένα παραμένουν αμετάβλητα· μόνο η οπτική διεπαφή φίλτρου κρύβεται.
* Δεν εμφανίζονται μηνύματα σφάλματος κατά τη φόρτωση ή αποθήκευση.

Έχετε επιτυχώς **αφαιρέσει το autofilter από πίνακα** χρησιμοποιώντας Java.

## Συμπέρασμα

Αυτό το tutorial έδειξε πώς να **αφαιρέσετε το autofilter από πίνακα** σε αρχείο Excel με Java. Φορτώνοντας το βιβλίο εργασίας, εντοπίζοντας το στόχο φύλλο και πίνακα, και καλώντας `setShowAutoFilter(false)`, μπορείτε να **απενεργοποιήσετε το autofilter στο Excel** προγραμματιστικά. Το ίδιο μοτίβο λειτουργεί για οποιονδήποτε αριθμό πινάκων και μπορείτε εύκολα να το επεκτείνετε για επανενεργοποίηση του φίλτρου όταν χρειαστεί.

Στη συνέχεια, μπορείτε να εξερευνήσετε σχετικές θεματικές όπως **πώς να κρύψετε το autofilter στο Excel** για συγκεκριμένες γραμμές, την εφαρμογή conditional formatting με Aspose.Cells, ή την αυτοματοποίηση δημιουργίας γραφημάτων από το ίδιο βιβλίο εργασίας. Πειραματιστείτε με διαφορετικές επιλογές πινάκων και συνδυάστε αυτήν την τεχνική με άλλες εργασίες αυτοματοποίησης Excel για να δημιουργήσετε ισχυρά pipelines επεξεργασίας δεδομένων.

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε επιπλέον δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Remove Autofilter from Excel with Java – Complete Guide](/cells/english/java/spreadsheet-automation/remove-autofilter-from-excel-with-java-complete-guide/)
- [How to Clear AutoFilter in Excel Using Java – Complete Guide](/cells/english/java/spreadsheet-automation/how-to-clear-autofilter-in-excel-using-java-complete-guide/)
- [How to Turn Off AutoFilter in Excel with Java – Complete Guide](/cells/english/java/spreadsheet-automation/how-to-turn-off-autofilter-in-excel-with-java-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}