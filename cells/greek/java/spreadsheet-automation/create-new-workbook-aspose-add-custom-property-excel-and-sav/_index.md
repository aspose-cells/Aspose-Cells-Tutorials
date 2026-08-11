---
category: general
date: 2026-08-11
description: Δημιουργήστε νέο βιβλίο εργασίας Aspose σε Java, προσθέστε μια προσαρμοσμένη
  ιδιότητα Excel, στη συνέχεια αποθηκεύστε το βιβλίο εργασίας ως XLSB με ένα πλήρες
  βήμα‑προς‑βήμα παράδειγμα.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create new workbook aspose
- save workbook as xlsb
- add custom property excel
- Aspose.Cells Java
- custom properties Excel
- workbook serialization
language: el
lastmod: 2026-08-11
og_description: Δημιουργήστε νέο βιβλίο εργασίας Aspose σε Java, προσθέστε μια προσαρμοσμένη
  ιδιότητα Excel και αποθηκεύστε το βιβλίο εργασίας ως XLSB με ένα πλήρες, έτοιμο
  προς εκτέλεση παράδειγμα.
og_image_alt: Java code screenshot that creates a new workbook Aspose, adds a custom
  Excel property, and saves it as an XLSB file
og_title: Δημιουργία νέου βιβλίου εργασίας Aspose – προσθήκη προσαρμοσμένης ιδιότητας
  Excel
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: Create new workbook Aspose in Java, add a custom property Excel, then
    save workbook as XLSB with a full step‑by‑step example.
  headline: Create new workbook Aspose – add custom property Excel and save as XLSB
  type: TechArticle
- description: Create new workbook Aspose in Java, add a custom property Excel, then
    save workbook as XLSB with a full step‑by‑step example.
  name: Create new workbook Aspose – add custom property Excel and save as XLSB
  steps:
  - name: What if I need to store a string property?
    text: '```java worksheet.getCustomProperties().add("Owner", "Alice"); ```'
  - name: Can I add multiple custom properties at once?
    text: Yes. Call `add` repeatedly for each name/value pair. Aspose.Cells does not
      limit the number of custom properties, but keep the total size reasonable to
      avoid bloating the file.
  - name: How does the binary format affect performance?
    text: XLSB files load faster because they avoid XML parsing. This is especially
      noticeable for workbooks with many rows, formulas, or embedded images.
  - name: What if I need to work with an existing XLSX file?
    text: Replace the `new Workbook()` constructor with `new Workbook("ExistingFile.xlsx")`.
      The rest of the steps (adding properties, saving as XLSB) remain identical.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- XLSB
- Custom Properties
title: Δημιουργία νέου βιβλίου εργασίας Aspose – προσθήκη προσαρμοσμένης ιδιότητας
  Excel και αποθήκευση ως XLSB
url: /el/java/spreadsheet-automation/create-new-workbook-aspose-add-custom-property-excel-and-sav/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία νέου βιβλίου εργασίας Aspose – προσθήκη προσαρμοσμένης ιδιότητας Excel και αποθήκευση ως XLSB

Εάν χρειάζεστε **να δημιουργήσετε νέο βιβλίο εργασίας Aspose** σε μια εφαρμογή Java, αυτός ο οδηγός σας δείχνει ακριβώς πώς να το κάνετε. Θα μάθετε να **προσθέτετε προσαρμοσμένη ιδιότητα Excel**, να ανακτάτε την τιμή και να **αποθηκεύετε το βιβλίο εργασίας ως XLSB** χωρίς να χάσετε μεταδεδομένα.

Το tutorial καλύπτει όλα, από τη ρύθμιση του έργου μέχρι την επαλήθευση του αποθηκευμένου αρχείου. Δεν απαιτείται εξωτερική τεκμηρίωση· ακολουθήστε τα βήματα και εκτελέστε τον κώδικα.

## Προαπαιτούμενα

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

- Java Development Kit (JDK) 8 ή νεότερο εγκατεστημένο.
- Maven ή Gradle για διαχείριση εξαρτήσεων (το παράδειγμα χρησιμοποιεί Maven).
- Ένα ενεργό license του Aspose.Cells for Java (ή χρησιμοποιήστε τη δωρεάν λειτουργία αξιολόγησης για δοκιμές).

## Βήμα 1: Προσθήκη Aspose.Cells στο έργο σας

Προσθέστε το Maven artifact του Aspose.Cells στο `pom.xml`. Αυτή η εξάρτηση παρέχει τις κλάσεις που χρειάζονται για **να δημιουργήσετε νέο βιβλίο εργασίας Aspose**.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- Use the latest stable version -->
</dependency>
```

> **Συμβουλή:** Εάν προτιμάτε Gradle, αντικαταστήστε το απόσπασμα Maven με τη σχετική γραμμή `implementation "com.aspose:aspose-cells:23.12"`.

## Βήμα 2: Δημιουργία νέου βιβλίου εργασίας Aspose

Το πρώτο λειτουργικό βήμα είναι η δημιουργία ενός αντικειμένου `Workbook`. Αυτό το αντικείμενο αντιπροσωπεύει ένα αρχείο Excel στη μνήμη και είναι το σημείο εισόδου για όλες τις περαιτέρω λειτουργίες.

```java
import com.aspose.cells.*;

public class CustomPropertiesXlsb {

    public static void main(String[] args) throws Exception {
        // Step 2: Create a new workbook Aspose
        Workbook workbook = new Workbook();               // In‑memory workbook
        Worksheet worksheet = workbook.getWorksheets().get(0); // Default first sheet
```

Η δημιουργία ενός νέου βιβλίου εργασίας Aspose σας δίνει ένα καθαρό βιβλίο με ένα προεπιλεγμένο φύλλο εργασίας, έτοιμο για προσαρμογές.

## Βήμα 3: Προσθήκη προσαρμοσμένης ιδιότητας Excel

Οι προσαρμοσμένες ιδιότητες σας επιτρέπουν να αποθηκεύετε αυθαίρετα μεταδεδομένα μέσα σε ένα αρχείο Excel. Εδώ **προσθέτουμε προσαρμοσμένη ιδιότητα Excel** με όνομα `ProjectId` και αριθμητική τιμή.

```java
        // Step 3: Add a custom property named "ProjectId" with a numeric value
        worksheet.getCustomProperties().add("ProjectId", 12345);
```

Η μέθοδος `add` δέχεται ένα όνομα ιδιότητας και μια τιμή οποιουδήποτε υποστηριζόμενου τύπου (string, number, date κ.λπ.). Αυτά τα μεταδεδομένα μεταφέρονται μαζί με το αρχείο όπου και αν το αντιγράψετε.

## Βήμα 4: Ανάκτηση και εμφάνιση της προσαρμοσμένης ιδιότητας

Η ανάγνωση της ιδιότητας επιβεβαιώνει ότι αποθηκεύτηκε σωστά. Μπορείτε επίσης να χρησιμοποιήσετε την ανακτημένη τιμή στη λογική της εφαρμογής σας.

```java
        // Step 4: Retrieve the custom property value and display it
        int projectId = (int) worksheet.getCustomProperties()
                                      .get("ProjectId")
                                      .getValue();
        System.out.println("ProjectId = " + projectId);
```

Η μετατροπή σε `int` λειτουργεί επειδή αποθηκεύσαμε αριθμητική τιμή. Εάν αποθηκεύσετε string, χρησιμοποιήστε `(String)` αντί.

## Βήμα 5: Αποθήκευση βιβλίου εργασίας ως XLSB

Τώρα **αποθηκεύετε το βιβλίο εργασίας ως XLSB**. Η μορφή XLSB αποθηκεύει το βιβλίο σε δυαδική αναπαράσταση, η οποία ανοίγει πιο γρήγορα και καταλαμβάνει λιγότερο χώρο στο δίσκο. Όλες οι προσαρμοσμένες ιδιότητες διατηρούνται αυτόματα.

```java
        // Step 5: Save the workbook as an XLSB file (custom properties are preserved)
        workbook.save("WithCustomProps.xlsb", SaveFormat.XLSB);
    }
}
```

Αντικαταστήστε το `"WithCustomProps.xlsb"` με απόλυτη διαδρομή εάν χρειάζεστε το αρχείο σε συγκεκριμένο φάκελο. Το enum `SaveFormat.XLSB` λέει στο Aspose.Cells να γράψει τη δυαδική μορφή.

## Βήμα 6: Επαλήθευση του αποτελέσματος

Εκτελέστε το πρόγραμμα από το IDE ή τη γραμμή εντολών:

```bash
mvn compile exec:java -Dexec.mainClass=CustomPropertiesXlsb
```

Θα πρέπει να δείτε:

```
ProjectId = 12345
```

Ανοίξτε το `WithCustomProps.xlsb` στο Excel. Μεταβείτε σε **File → Info → Properties → Advanced Properties → Custom**. Η καταχώρηση `ProjectId` με τιμή `12345` θα εμφανιστεί, επιβεβαιώνοντας ότι το βήμα **add custom property excel** ολοκληρώθηκε επιτυχώς και ότι η λειτουργία **save workbook as xlsb** διατήρησε τα μεταδεδομένα.

## Συχνές ερωτήσεις και ειδικές περιπτώσεις

### Τι κάνω αν χρειάζεται να αποθηκεύσω ιδιότητα τύπου string;

```java
worksheet.getCustomProperties().add("Owner", "Alice");
```

Ανακτήστε την με:

```java
String owner = (String) worksheet.getCustomProperties().get("Owner").getValue();
```

### Μπορώ να προσθέσω πολλές προσαρμοσμένες ιδιότητες ταυτόχρονα;

Ναι. Καλέστε `add` επανειλημμένα για κάθε ζεύγος όνομα/τιμή. Το Aspose.Cells δεν περιορίζει τον αριθμό των προσαρμοσμένων ιδιοτήτων, αλλά κρατήστε το συνολικό μέγεθος λογικό ώστε να μην αυξήσετε υπερβολικά το μέγεθος του αρχείου.

### Πώς επηρεάζει η δυαδική μορφή την απόδοση;

Τα αρχεία XLSB φορτώνουν πιο γρήγορα επειδή αποφεύγουν την ανάλυση XML. Αυτό είναι ιδιαίτερα εμφανές σε βιβλία εργασίας με πολλές γραμμές, τύπους ή ενσωματωμένες εικόνες.

### Τι κάνω αν πρέπει να εργαστώ με υπάρχον αρχείο XLSX;

Αντικαταστήστε τον κατασκευαστή `new Workbook()` με `new Workbook("ExistingFile.xlsx")`. Τα υπόλοιπα βήματα (προσθήκη ιδιοτήτων, αποθήκευση ως XLSB) παραμένουν αμετάβλητα.

## Πλήρης πηγαίος κώδικας

Παρακάτω βρίσκεται το πλήρες, έτοιμο‑για‑εκτέλεση παράδειγμα. Αντιγράψτε το σε ένα αρχείο με όνομα `CustomPropertiesXlsb.java` μέσα στο φάκελο `src/main/java`.

```java
import com.aspose.cells.*;

public class CustomPropertiesXlsb {
    public static void main(String[] args) throws Exception {
        // Step 2: Create a new workbook Aspose
        Workbook workbook = new Workbook();                       // In‑memory workbook
        Worksheet worksheet = workbook.getWorksheets().get(0);    // Default first sheet

        // Step 3: Add a custom property named "ProjectId" with a numeric value
        worksheet.getCustomProperties().add("ProjectId", 12345);

        // Step 4: Retrieve the custom property value and display it
        int projectId = (int) worksheet.getCustomProperties()
                                      .get("ProjectId")
                                      .getValue();
        System.out.println("ProjectId = " + projectId);

        // Step 5: Save the workbook as an XLSB file (custom properties are preserved)
        workbook.save("WithCustomProps.xlsb", SaveFormat.XLSB);
    }
}
```

Η εκτέλεση αυτής της κλάσης παράγει ένα αρχείο XLSB που περιέχει την προσαρμοσμένη ιδιότητα και μπορεί να ανοιχθεί σε οποιαδήποτε σύγχρονη έκδοση του Microsoft Excel.

## Συμπέρασμα

Τώρα ξέρετε πώς να **δημιουργήσετε νέο βιβλίο εργασίας Aspose**, **να προσθέσετε προσαρμοσμένη ιδιότητα Excel**, και **να αποθηκεύσετε το βιβλίο εργασίας ως XLSB** χρησιμοποιώντας Java. Το παράδειγμα δείχνει ολόκληρο τον κύκλο ζωής: αρχικοποίηση, ένεση μεταδεδομένων, επαλήθευση και δυαδική σειριοποίηση.

Στη συνέχεια, εξερευνήστε σχετικά θέματα όπως **ορισμός ιδιοτήτων εγγράφου**, **εργασία με τύπους Excel**, ή **μετατροπή μεταξύ XLSX και XLSB**. Κάθε ένα από αυτά βασίζεται στο ίδιο API του Aspose.Cells που μόλις χρησιμοποιήσατε, ώστε να μπορείτε να επεκτείνετε τη λύση χωρίς να μάθετε νέες βιβλιοθήκες.

Μη διστάσετε να πειραματιστείτε με διαφορετικούς τύπους δεδομένων, πολλαπλά φύλλα εργασίας ή προστασία με κωδικό—το Aspose.Cells υποστηρίζει όλα αυτά τα σενάρια έτοιμα. Καλή προγραμματιστική!

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κυριαρχήσετε επιπλέον δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Create Save Excel Workbook Aspose Cells Java](/cells/english/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)
- [How to Create and Save an Excel Workbook as SVG using Aspose.Cells for Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [Create Excel Workbook and Add Labels with Aspose.Cells for Java](/cells/english/java/advanced-excel-charts/data-labeling/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}