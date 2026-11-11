---
category: general
date: 2026-10-26
description: Μάθετε πώς να αντιγράψετε έναν συγκεντρωτικό πίνακα σε ένα νέο βιβλίο
  εργασίας χρησιμοποιώντας τη Java, διατηρώντας τη μορφοποίηση και τον ορισμό του
  πίνακα, ενώ αντιγράφετε ένα εύρος Excel με μορφοποίηση μέσω του Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- how to copy pivot
- copy excel range
- create empty workbook
- copy range with formatting
language: el
lastmod: 2026-10-26
og_description: Αντιγράψτε τον πίνακα Pivot σε νέο βιβλίο εργασίας σε Java με το Aspose.Cells.
  Αυτός ο οδηγός δείχνει πώς να αντιγράψετε το εύρος Excel, να διατηρήσετε τη μορφοποίηση
  και να δημιουργήσετε κενό βιβλίο εργασίας αποδοτικά.
og_image_alt: Screenshot of a Java program that copies a pivot table to a new Excel
  workbook
og_title: Αντιγραφή πίνακα Pivot σε νέο βιβλίο εργασίας σε Java – οδηγός βήμα‑βήμα
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to copy pivot table to a new workbook using Java, preserving
    formatting and the pivot definition while you copy excel range with formatting
    via Aspose.Cells.
  headline: How to copy pivot table to a new workbook in Java
  type: TechArticle
- description: Learn how to copy pivot table to a new workbook using Java, preserving
    formatting and the pivot definition while you copy excel range with formatting
    via Aspose.Cells.
  name: How to copy pivot table to a new workbook in Java
  steps:
  - name: Prerequisites
    text: '* Java 17 or later. * Aspose.Cells for Java (version 23.10 or newer). *
      Basic familiarity with Java IDEs (IntelliJ IDEA, Eclipse, etc.).'
  - name: Why this works
    text: '* `new Workbook()` **creates empty workbook** with a default sheet, avoiding
      the need to delete existing data. * `CopyOptions` tells Aspose.Cells to copy
      **pivot table** metadata, not just raw values. The `PASTE_ALL` mode also carries
      cell styles, number formats, and conditional formatting—fulfillin'
  - name: Edge cases to consider
    text: '| Situation | Recommended handling | |----------------------------------------|----------------------|
      | Source workbook has multiple pivots | Copy each pivot’s range separately or
      copy the whole sheet. | | Destination already contains data | Choose a non‑conflicting
      start cell (e.g., "H1") when cal'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Πώς να αντιγράψετε έναν συγκεντρωτικό πίνακα σε νέο βιβλίο εργασίας στη Java
url: /el/java/excel-pivot-tables/how-to-copy-pivot-table-to-a-new-workbook-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να αντιγράψετε έναν πίνακα Pivot σε νέο βιβλίο εργασίας σε Java

Αν χρειάζεται να **αντιγράψετε έναν πίνακα pivot** από ένα αρχείο Excel σε άλλο, αυτός ο οδηγός σας παρουσιάζει μια πλήρη, εκτελέσιμη λύση. Θα δείτε πώς να διατηρήσετε τον ορισμό του pivot, να κρατήσετε όλη τη μορφοποίηση και να αποφύγετε κοινά προβλήματα κατά την αντιγραφή μιας περιοχής Excel.

Η αντιγραφή ενός πίνακα pivot συχνά εγείρει ερωτήματα όπως *πώς να αντιγράψετε pivot* χωρίς να σπάσει η πηγή δεδομένων ή να χαθούν τα στυλ. Στο τέλος αυτού του tutorial θα έχετε ένα αυτόνομο πρόγραμμα Java που δημιουργεί ένα κενό βιβλίο εργασίας, αντιγράφει την επιθυμητή περιοχή και αποθηκεύει το αποτέλεσμα με τον pivot αμετάβλητο.

## Τι θα πετύχετε

* Φόρτωση ενός βιβλίου εργασίας πηγής που περιέχει πίνακα pivot.  
* **Create empty workbook** που θα λάβει τα αντιγραμμένα δεδομένα.  
* **Copy excel range** που περιλαμβάνει τον pivot, χρησιμοποιώντας επιλογές που διατηρούν τον pivot και τη μορφοποίηση.  
* Αποθήκευση του αρχείου προορισμού και επαλήθευση ότι ο pivot λειτουργεί ακριβώς όπως το αρχικό.

### Προαπαιτούμενα

* Java 17 ή νεότερη.  
* Aspose.Cells for Java (έκδοση 23.10 ή νεότερη).  
* Βασική εξοικείωση με IDE Java (IntelliJ IDEA, Eclipse κ.λπ.).  

> **Συμβουλή:** Χρησιμοποιήστε την δωρεάν άδεια αξιολόγησης του Aspose.Cells για γρήγορο testing· αντικαταστήστε την με πλήρη άδεια πριν την παραγωγική χρήση.

## Αντιγραφή πίνακα pivot σε νέο βιβλίο εργασίας

Το πρώτο βήμα είναι η ρύθμιση των βιβλίων εργασίας πηγής και προορισμού. Ο προορισμός ξεκινά ως κλήση **create empty workbook**, η οποία δημιουργεί ένα καθαρό αρχείο με ένα μόνο φύλλο.

```java
import com.aspose.cells.*;

public class CopyPivotExample {
    public static void main(String[] args) throws Exception {
        // Load the source workbook that holds the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");

        // Create an empty workbook that will receive the copied range
        Workbook destWb = new Workbook();

        // Get the first worksheet from each workbook
        Worksheet srcSheet = srcWb.getWorksheets().get(0);
        Worksheet destSheet = destWb.getWorksheets().get(0);

        // Configure copy options to preserve the pivot table and formatting
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.PASTE_ALL); // ensures pivot and styles are kept

        // Copy the range that contains the pivot table
        srcSheet.getCells().copyRange("A1:D20", destSheet.getCells(), "A1", copyOptions);

        // Save the destination workbook
        destWb.save("YOUR_DIRECTORY/destination.xlsx");
    }
}
```

### Γιατί λειτουργεί αυτό

* `new Workbook()` **creates empty workbook** με προεπιλεγμένο φύλλο, αποφεύγοντας την ανάγκη διαγραφής υπαρχόντων δεδομένων.  
* `CopyOptions` λέει στο Aspose.Cells να αντιγράψει τα μεταδεδομένα του **pivot table**, όχι μόνο τις ακατέργαστες τιμές. Η λειτουργία `PASTE_ALL` μεταφέρει επίσης στυλ κελιών, μορφές αριθμών και conditional formatting—ικανοποιώντας την απαίτηση **copy range with formatting**.  
* `copyRange` εκτελεί μια λειτουργία **copy excel range** που σέβεται τις εσωτερικές δομές της πηγής, ώστε ο pivot να παραμείνει λειτουργικός μετά την αντιγραφή.

## Πώς να αντιγράψετε pivot χωρίς να χάσετε τη μορφοποίηση

Αν χρησιμοποιήσετε μόνο τις προεπιλεγμένες `CopyOptions`, κάποιες πληροφορίες στυλ μπορεί να παραλειφθούν σε παλαιότερες εκδόσεις του Aspose.Cells. Ορίζοντας ρητά τον τύπο επικόλλησης εξασφαλίζει ότι **copy range with formatting** τηρείται.

```java
CopyOptions copyOptions = new CopyOptions();
copyOptions.setPasteType(PasteType.PASTE_ALL);          // copy values, formulas, formats
copyOptions.setPasteSpecialType(PasteSpecialType.ALL); // include column widths and row heights
```

Η προσθήκη `setPasteSpecialType` διασφαλίζει ότι τα πλάτη των στηλών, τα ύψη των γραμμών και ακόμη και οι κανόνες επικύρωσης δεδομένων μεταφέρονται μαζί με την περιοχή. Αυτό είναι ιδιαίτερα χρήσιμο όταν ο πίνακας pivot εκτείνεται σε πολλές στήλες με προσαρμοσμένα πλάτη.

## Δημιουργία κενού βιβλίου εργασίας πριν την αντιγραφή

Μερικές φορές οι προγραμματιστές προσπαθούν να αντιγράψουν σε ένα υπάρχον βιβλίο εργασίας που ήδη περιέχει δεδομένα. Αυτό μπορεί να προκαλέσει επικάλυψη περιοχών ή απρόσμενες αντικαταστάσεις. Ξεκινώντας με μια κλήση **create empty workbook** απομονώνει τη λειτουργία:

```java
Workbook destWb = new Workbook(); // fresh file with one sheet
Worksheet destSheet = destWb.getWorksheets().get(0); // reference the clean sheet
```

Αν χρειάζεστε περισσότερα από ένα φύλλα στον προορισμό, μπορείτε να τα προσθέσετε μετά την αντιγραφή:

```java
destWb.getWorksheets().add("Summary");
```

## Αντιγραφή περιοχής Excel με μορφοποίηση χρησιμοποιώντας CopyOptions

Πέρα από πίνακες pivot, το ίδιο μοτίβο λειτουργεί για οποιοδήποτε **copy excel range** που απαιτεί διατήρηση μορφοποίησης—γράφηματα, πίνακες ή conditional formats.

```java
// Example: copy a styled table from A1 to G15
srcSheet.getCells().copyRange("A1:G15", destSheet.getCells(), "A1", copyOptions);
```

Η παρουσίαση `CopyOptions` παραμένει η ίδια, έτσι λαμβάνετε συνεπή συμπεριφορά σε διαφορετικές περιοχές.

### Περιπτώσεις άκρων που πρέπει να ληφθούν υπόψη

| Κατάσταση                              | Προτεινόμενη αντιμετώπιση |
|----------------------------------------|---------------------------|
| Το βιβλίο εργασίας πηγής έχει πολλαπλούς pivots | Αντιγράψτε την περιοχή κάθε pivot ξεχωριστά ή αντιγράψτε ολόκληρο το φύλλο. |
| Ο προορισμός περιέχει ήδη δεδομένα      | Επιλέξτε ένα μη συγκρουόμενο κελί εκκίνησης (π.χ., "H1") κατά την κλήση `copyRange`. |
| Η πηγή δεδομένων του pivot είναι εξωτερική (π.χ., DB) | Βεβαιωθείτε ότι το βιβλίο εργασίας προορισμού δείχνει στην ίδια εξωτερική πηγή ή ανανεώστε τον pivot μετά την αντιγραφή. |
| Μεγάλο βιβλίο εργασίας ( > 10 MB )       | Αυξήστε το μέγεθος heap της Java (`-Xmx2g`) για να αποφύγετε `OutOfMemoryError`. |

## Επαλήθευση του αποτελέσματος

Μετά την εκτέλεση του προγράμματος, ανοίξτε το `destination.xlsx`. Θα πρέπει να δείτε:

* Την ίδια διάταξη πίνακα pivot όπως στο `source.xlsx`.  
* Όλα τα χρώματα κελιών, μορφές αριθμών και πλάτη στηλών διατηρημένα.  
* Η πηγή δεδομένων του pivot να δείχνει ακόμη στην αρχική περιοχή δεδομένων μέσα στο νέο αρχείο, ώστε η ανανέωση του pivot να ενημερώνει τις τιμές σωστά.

Αν ο pivot εμφανίζεται ως στατικός πίνακας, ελέγξτε ξανά ότι έχει οριστεί `CopyOptions.setPasteType(PasteType.PASTE_ALL)`. Χωρίς αυτήν την επιλογή το Aspose.Cells αντιμετωπίζει τον pivot ως απλά δεδομένα.

## Συμπέρασμα

Τώρα ξέρετε πώς να **αντιγράψετε έναν πίνακα pivot** σε νέο βιβλίο εργασίας σε Java, διατηρώντας μορφοποίηση, συνδέσεις δεδομένων και διάταξη φύλλου. Η πλήρης λύση δείχνει πώς να φορτώσετε ένα αρχείο πηγής, **create empty workbook**, να ρυθμίσετε τις επιλογές **copy excel range** και να αποθηκεύσετε το αποτέλεσμα.  

Από εδώ μπορείτε να εξερευνήσετε σχετικές θεματικές όπως **πώς να αντιγράψετε pivot** μεταξύ διαφορετικών φύλλων, να ενσωματώσετε γραφήματα δίπλα σε pivots ή να αυτοματοποιήσετε μαζική επεξεργασία πολλαπλών βιβλίων εργασίας. Πειραματιστείτε με τις ρυθμίσεις του `CopyOptions` ώστε να ταιριάζουν στις συγκεκριμένες ανάγκες αυτοματοποίησής σας, και θα έχετε ένα ισχυρό εργαλείο διαχείρισης Excel στα χέρια σας.

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε επιπλέον δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Create New Workbook in Java – Full Guide to Copy Pivot Table](/cells/english/java/excel-pivot-tables/create-new-workbook-in-java-full-guide-to-copy-pivot-table/)
- [Copy Pivot Table Between Workbooks – Step‑by‑Step Java Guide](/cells/english/java/excel-pivot-tables/copy-pivot-table-between-workbooks-step-by-step-java-guide/)
- [How to copy range and preserve a pivot table in Java](/cells/english/java/excel-pivot-tables/how-to-copy-range-and-preserve-a-pivot-table-in-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}