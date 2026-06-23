---
category: general
date: 2026-06-18
description: Αναλύστε ημερομηνία ιαπωνικής εποχής σε Java με τη χρήση του Aspose.Cells.
  Μάθετε πώς να διαβάζετε ημερομηνία από κελί Excel και να εξάγετε γρήγορα ημερομηνία/ώρα
  από κελί Excel.
draft: false
keywords:
- parse japanese era date
- read date from excel cell
- extract datetime from excel cell
language: el
og_description: Αναλύστε ημερομηνία ιαπωνικής εποχής σε Java με το Aspose.Cells. Αυτός
  ο οδηγός σας δείχνει πώς να διαβάσετε την ημερομηνία από κελί Excel και να εξάγετε
  την ημερομηνία/ώρα από κελί Excel σε λίγα μόνο βήματα.
og_title: Ανάλυση ημερομηνίας ιαπωνικής εποχής από το Excel σε Java – Πλήρης οδηγός
schemas:
- author: Aspose
  dateModified: '2026-06-18'
  description: Parse Japanese era date in Java using Aspose.Cells. Learn how to read
    date from Excel cell and extract datetime from Excel cell quickly.
  headline: Parse Japanese Era Date from Excel in Java – Full Guide
  type: TechArticle
- description: Parse Japanese era date in Java using Aspose.Cells. Learn how to read
    date from Excel cell and extract datetime from Excel cell quickly.
  name: Parse Japanese Era Date from Excel in Java – Full Guide
  steps:
  - name: Multiple Eras
    text: Japan has had several eras (Meiji, Taishō, Shōwa, Heisei, Reiwa). The `setParseDateUsingJapaneseEra(true)`
      flag covers all of them automatically, but be aware that older dates may fall
      outside the library’s supported range (typically 1868‑present). If you encounter
      a date like “昭和45年12月31日”, the sam
  - name: Blank or Invalid Cells
    text: 'If a cell is empty or contains a malformed string, `cell.getDateTime()`
      throws a `CellsException`. Guard against this with a simple check:'
  - name: Time Component
    text: The example only includes a date, but if your Excel file also stores time
      (e.g., “令和3年5月10日 14:30”), Aspose.Cells will preserve the time portion. The
      `LocalDateTime` you receive will include hours, minutes, and seconds.
  type: HowTo
tags:
- Java
- Excel
- DateTime
title: Ανάλυση ημερομηνίας ιαπωνικής εποχής από το Excel σε Java – Πλήρης Οδηγός
url: /el/java/cell-operations/parse-japanese-era-date-from-excel-in-java-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ανάλυση ημερομηνίας ιαπωνικής εποχής από το Excel σε Java – Πλήρης Οδηγός

Έχετε ποτέ χρειαστεί να **parse Japanese era date** αποθηκευμένη σε ένα βιβλίο εργασίας Excel αλλά δεν ήξερες πώς να τη μετατρέψεις σε κανονική Γρηγοριανή `DateTime`; Δεν είστε μόνοι—πολλοί προγραμματιστές αντιμετωπίζουν αυτό το πρόβλημα όταν δουλεύουν με παλαιές ιαπωνικές λογιστικές φύλλες ή κυβερνητικές φόρμες. Τα καλά νέα είναι ότι με λίγες γραμμές Java και τη σωστή βιβλιοθήκη, μπορείτε να **read date from Excel cell** και **extract datetime from Excel cell** χωρίς καμία χειροκίνητη επεξεργασία συμβολοσειρών.

Σε αυτό το tutorial θα περάσουμε βήμα-βήμα ένα πλήρες, εκτελέσιμο παράδειγμα που δείχνει ακριβώς πώς να **parse Japanese era date** συμβολοσειρές όπως “令和3年5月10日” σε ένα Java `java.time.LocalDateTime`. Θα καλύψουμε την απαιτούμενη εξάρτηση Maven, θα εξηγήσουμε γιατί πρέπει να ενεργοποιήσετε την ανάλυση με γνώση εποχής, και θα επισημάνουμε κοινές παγίδες που μπορεί να συναντήσετε. Στο τέλος, θα έχετε ένα σταθερό, έτοιμο για παραγωγή snippet που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο Java.

## Προαπαιτούμενα

- Java 17 ή νεότερη (ο κώδικας λειτουργεί επίσης σε Java 8+)
- Σύστημα κατασκευής Maven ή Gradle
- Βασική εξοικείωση με αρχεία Excel
- Η βιβλιοθήκη **Aspose.Cells for Java** (η δωρεάν δοκιμή λειτουργεί για δοκιμές)

Αν κάποιο από αυτά σας φαίνεται άγνωστο, μην ανησυχείτε—θα σας δείξω ακριβώς πώς να προσθέσετε τη βιβλιοθήκη και να ξεκινήσετε.

## Βήμα 1: Προσθήκη Aspose.Cells στο Πρόγραμμά σας

Πρώτα απ' όλα: χρειάζεστε τη βιβλιοθήκη που καταλαβαίνει τις ημερομηνίες ιαπωνικής εποχής. Το Aspose.Cells κάνει το σκληρό έργο για εσάς.

**Maven**:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- check for latest version -->
</dependency>
```

**Gradle**:

```groovy
implementation 'com.aspose:aspose-cells:24.9'
```

Μόλις η εξάρτηση επιλυθεί, μπορείτε να αρχίσετε να γράφετε κώδικα που *reads date from Excel cell* και *extracts datetime from Excel cell*.

## Βήμα 2: Δημιουργία Workbook και Στόχευση του Πρώτου Worksheet

Θα ξεκινήσουμε δημιουργώντας ένα νέο workbook στη μνήμη και λαμβάνοντας το πρώτο φύλλο. Αυτό αντικατοπτρίζει τις πρώτες δύο γραμμές του αρχικού παραδείγματος.

```java
import com.aspose.cells.*;

public class JapaneseEraDateParser {
    public static void main(String[] args) throws Exception {
        // Step 2: Initialize workbook and worksheet
        Workbook workbook = new Workbook();               // creates a blank workbook
        Worksheet sheet = workbook.getWorksheets().get(0); // first (and only) sheet
```

Γιατί να ξεκινήσουμε με ένα φρέσκο workbook; Εγγυάται ένα καθαρό περιβάλλον όπου μπορούμε να ελέγξουμε κάθε ρύθμιση—σημαντικό όταν αργότερα ενεργοποιήσετε την ανάλυση με γνώση εποχής.

## Βήμα 3: Τοποθέτηση Συμβολοσειράς Ημερομηνίας Ιαπωνικής Εποχής στο Κελί A1

Τώρα προσομοιώνουμε ένα αρχείο Excel που περιέχει ήδη μια ημερομηνία ιαπωνικής εποχής. Στην πραγματική ζωή πιθανότατα θα φορτώνετε ένα υπάρχον `.xlsx`, αλλά για την επεξήγηση θα **write** την τιμή μόνοι μας.

```java
        // Step 3: Insert a Japanese era date string into A1
        Cell cell = sheet.getCells().get("A1");
        cell.putValue("令和3年5月10日"); // Reiwa 3rd year = 2021-05-10
```

Η συμβολοσειρά ακολουθεί την τυπική ιαπωνική σημειογραφία: *Era* + *Year* + *Month* + *Day*. Χωρίς επιπλέον ρύθμιση, το Aspose.Cells θα τη θεωρήσει απλό κείμενο, όχι ημερομηνία.

## Βήμα 4: Ενεργοποίηση Ανάλυσης Ημερομηνίας με Γνώση Εποχής

Αυτό είναι το κρίσιμο μέρος: πείτε στο workbook να **parse Japanese era date** τις συμβολοσειρές όταν τις συναντά. Αυτό γίνεται μέσω της σημαίας `ParseDateUsingJapaneseEra`.

```java
        // Step 4: Turn on era‑aware parsing
        workbook.getSettings().setParseDateUsingJapaneseEra(true);
```

Γιατί είναι απαραίτητο; Από προεπιλογή το Aspose.Cells υποθέτει το Γρηγοριανό ημερολόγιο, έτσι το “令和3年5月10日” θα παραμείνει ως συμβολοσειρά. Η ενεργοποίηση της σημαίας υποδεικνύει στη μηχανή να το μετατρέψει σε `java.util.Date` (ή ισοδύναμο `java.time`) στο παρασκήνιο.

## Βήμα 5: Ανάκτηση της Αναλυμένης Τιμής DateTime

Τώρα που το workbook ξέρει πώς να ερμηνεύσει την εποχή, μπορούμε να ζητήσουμε από το κελί την αναπαράστασή του σε `DateTime`.

```java
        // Step 5: Extract the parsed DateTime
        java.util.Date javaDate = cell.getDateTime(); // returns java.util.Date
        // Convert to java.time.LocalDateTime for modern APIs
        java.time.Instant instant = javaDate.toInstant();
        java.time.ZoneId zone = java.time.ZoneId.systemDefault();
        java.time.LocalDateTime dateTime = java.time.LocalDateTime.ofInstant(instant, zone);
```

Παρατηρήστε ότι **read date from Excel cell** χρησιμοποιώντας `cell.getDateTime()`. Η μέθοδος επιστρέφει ένα `java.util.Date`, το οποίο μετατρέπουμε αμέσως σε `LocalDateTime` για καλύτερη ασφάλεια τύπου. Αυτό ικανοποιεί την απαίτηση **extract datetime from excel cell** με έναν καθαρό, ιδιωματικό τρόπο.

## Βήμα 6: Επαλήθευση του Αποτελέσματος

Τέλος, ας εκτυπώσουμε την Γρηγοριανή ημερομηνία για να επιβεβαιώσουμε ότι η μετατροπή πέτυχε.

```java
        // Step 6: Output the Gregorian date
        System.out.println(dateTime); // Expected output: 2021-05-10T00:00
    }
}
```

Όταν εκτελέσετε το πρόγραμμα, θα πρέπει να δείτε:

```
2021-05-10T00:00
```

Αυτή η έξοδος αποδεικνύει ότι επιτυχώς **parse Japanese era date**, **read date from Excel cell**, και **extract datetime from Excel cell** σε μια ενιαία ροή.

## Διαχείριση Πραγματικών Περιπτώσεων Άκρων

### Πολλαπλές Εποχές

Η Ιαπωνία έχει περάσει από πολλές εποχές (Meiji, Taishō, Shōwa, Heisei, Reiwa). Η σημαία `setParseDateUsingJapaneseEra(true)` καλύπτει όλες αυτόματα, αλλά να γνωρίζετε ότι παλαιότερες ημερομηνίες μπορεί να βρίσκονται εκτός του υποστηριζόμενου εύρους της βιβλιοθήκης (συνήθως 1868‑σήμερα). Αν συναντήσετε ημερομηνία όπως “昭和45年12月31日”, ο ίδιος κώδικας θα τη μετατρέψει σε 1970‑12‑31.

### Κενά ή Μη Έγκυρα Κελιά

Αν ένα κελί είναι κενό ή περιέχει κακώς διαμορφωμένη συμβολοσειρά, το `cell.getDateTime()` ρίχνει ένα `CellsException`. Προστατέψτε το με έναν απλό έλεγχο:

```java
if (cell.getType() == CellValueType.IS_DATE) {
    // safe to call getDateTime()
} else {
    System.out.println("Cell does not contain a parsable date.");
}
```

### Στοιχείο Χρόνου

Το παράδειγμα περιλαμβάνει μόνο ημερομηνία, αλλά αν το αρχείο Excel σας αποθηκεύει επίσης χρόνο (π.χ., “令和3年5月10日 14:30”), το Aspose.Cells θα διατηρήσει το τμήμα του χρόνου. Το `LocalDateTime` που λαμβάνετε θα περιλαμβάνει ώρες, λεπτά και δευτερόλεπτα.

## Πλήρες Παράδειγμα Εργασίας

Συνδυάζοντας όλα, εδώ είναι το πλήρες, έτοιμο για αντιγραφή‑και‑επικόλληση πρόγραμμα:

```java
import com.aspose.cells.*;
import java.time.*;

public class JapaneseEraDateParser {
    public static void main(String[] args) throws Exception {
        // Create workbook and get first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.getWorksheets().get(0);

        // Insert Japanese era date string into A1
        Cell cell = sheet.getCells().get("A1");
        cell.putValue("令和3年5月10日");

        // Enable era‑aware parsing
        workbook.getSettings().setParseDateUsingJapaneseEra(true);

        // Extract the parsed DateTime
        java.util.Date javaDate = cell.getDateTime();
        LocalDateTime dateTime = javaDate.toInstant()
                                         .atZone(ZoneId.systemDefault())
                                         .toLocalDateTime();

        // Output the Gregorian date
        System.out.println(dateTime); // 2021-05-10T00:00
    }
}
```

Αποθηκεύστε το ως `JapaneseEraDateParser.java`, μεταγλωττίστε με `javac` και εκτελέστε με `java`. Αν όλα είναι ρυθμισμένα σωστά, θα δείτε την Γρηγοριανή ημερομηνία να εκτυπώνεται στην κονσόλα.

## Συμβουλές & Συνηθισμένες Παγίδες

- **Pro tip:** Πάντα ορίστε `setParseDateUsingJapaneseEra(true)` **πριν** διαβάσετε οποιεσδήποτε τιμές κελιών. Η αλλαγή της σημαίας μετά την ανάγνωση ενός κελιού δεν θα μετατρέψει παλαιότερα την τιμή.
- **Watch out for locale:** Η βιβλιοθήκη αναλύει τις συμβολοσειρές εποχής βάσει χαρακτήρων Unicode, έτσι δεν χρειάζεται να ορίσετε ρητά μια ιαπωνική τοπική ρύθμιση.
- **Performance note:** Η ενεργοποίηση της ανάλυσης εποχής προσθέτει μικρή επιβάρυνση. Αν τη χρειάζεστε μόνο για λίγα κελιά, μπορείτε προσωρινά να εναλλάξετε τη σημαία, να διαβάσετε τα κελιά, και μετά να την απενεργοποιήσετε ξανά.
- **Testing:** Χρησιμοποιήστε τη δωρεάν δοκιμή του Aspose για να επικυρώσετε έναν πραγματικό αρχείο Excel που περιέχει πολλαπλές ημερομηνίες εποχής. Αυτό εξασφαλίζει ότι ο κώδικας παραγωγής σας λειτουργεί όπως αναμένεται.

## Συμπέρασμα

Μόλις δείξαμε πώς να **parse Japanese era date** τιμές απευθείας από ένα βιβλίο εργασίας Excel χρησιμοποιώντας Java και Aspose.Cells. Ενεργοποιώντας την ανάλυση με γνώση εποχής, μπορείτε να **read date from Excel cell** και **extract datetime from Excel cell** με καθαρό, ασφαλή ως προς τον τύπο τρόπο. Η προσέγγιση λειτουργεί για οποιαδήποτε σύγχρονη ιαπωνική εποχή, διαχειρίζεται τα τμήματα χρόνου, και αντιμετωπίζει με χάρη τα μη έγκυρα δεδομένα.

Έτοιμοι για την επόμενη πρόκληση; Δοκιμάστε να φορτώσετε ένα πραγματικό αρχείο `.xlsx` που περιέχει μίξη Γρηγοριανών και ιαπωνικών ημερομηνιών εποχής, ή πειραματιστείτε με τη μορφοποίηση του προκύπτοντος `LocalDateTime` σε συμβολοσειρές που ταιριάζουν στην τοπική σας ρύθμιση. Μπορείτε επίσης να εξερευνήσετε τη γραφή των μετατρεπόμενων ημερομηνιών πίσω στο Excel για συστήματα που καταλαβαίνουν μόνο Γρηγοριανές ημερομηνίες.

Έχετε ερωτήσεις ή αντιμετωπίσατε μια περίεργη περίπτωση άκρου; Αφήστε ένα σχόλιο παρακάτω, και καλή προγραμματιστική!

## Τι Θα Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα-βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε σε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Κατακτήστε το Σύστημα Ημερομηνίας 1904 στο Excel Χρησιμοποιώντας Aspose.Cells Java για Αποτελεσματικές Λειτουργίες Κελιών](/cells/english/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/)
- [Αποτελεσματική Μετατροπή Excel σε PDF με Προσαρμοσμένες Μορφές Ημερομηνίας Χρησιμοποιώντας Aspose.Cells για Java](/cells/english/java/workbook-operations/render-excel-custom-date-formats-pdf-aspose-cells-java/)
- [Πώς να Επιλέξετε Περιοχές Κελιών στο Excel Χρησιμοποιώντας Aspose.Cells για Java (Οδηγός 2023)](/cells/english/java/range-management/aspose-cells-java-select-cell-ranges-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}