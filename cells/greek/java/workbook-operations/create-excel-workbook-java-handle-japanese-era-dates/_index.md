---
category: general
date: 2026-08-04
description: Δημιουργήστε βιβλίο εργασίας Excel με Java και αναλύστε ημερομηνίες ιαπωνικής
  εποχής, στη συνέχεια αποθηκεύστε το βιβλίο εργασίας ως xlsx χρησιμοποιώντας το Aspose.Cells
  για Java.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook java
- save workbook as xlsx
- java excel date conversion
- Aspose.Cells Java
- japanese era date parsing
language: el
lastmod: 2026-08-04
og_description: Δημιουργήστε βιβλίο εργασίας Excel με Java και μετατρέψτε αυτόματα
  τις ημερομηνίες ιαπωνικής εποχής σε Γρηγοριανές, στη συνέχεια αποθηκεύστε το βιβλίο
  εργασίας ως xlsx με το Aspose.Cells.
og_image_alt: Java code creating an Excel workbook and converting a Japanese era date
  to Gregorian
og_title: Δημιουργία βιβλίου εργασίας Excel Java – Οδηγός μετατροπής ιαπωνικών ημερομηνιών
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Create excel workbook java and parse Japanese era dates, then save
    workbook as xlsx using Aspose.Cells for Java.
  headline: 'Create excel workbook java: handle Japanese era dates'
  type: TechArticle
tags:
- java
- excel
- Aspose.Cells
- date conversion
- xlsx
title: 'Δημιουργία βιβλίου εργασίας Excel σε Java: διαχείριση ημερομηνιών ιαπωνικής
  εποχής'
url: /el/java/workbook-operations/create-excel-workbook-java-handle-japanese-era-dates/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία excel workbook java: διαχείριση ημερομηνιών ιαπωνικής εποχής

Αν χρειάζεστε να **create excel workbook java** και να δουλέψετε με ημερομηνίες ιαπωνικής εποχής, αυτό το tutorial σας δείχνει ακριβώς πώς. Θα μάθετε να εισάγετε μια ημερομηνία όπως “R3/05/01”, να αφήσετε το Aspose.Cells να την ερμηνεύσει ως ημερομηνία Γρηγοριανού ημερολογίου, και στη συνέχεια **save workbook as xlsx**.

Η εργασία με ημερολόγια βασισμένα σε εποχές μπορεί να είναι συγκεχυμένη, ειδικά όταν ο προεπιλεγμένος parser του Excel αναμένει μια τυπική μορφή Γρηγοριανού ημερολογίου. Ενεργοποιώντας την ανάλυση ιαπωνικής εποχής, αποφεύγετε την χειροκίνητη επεξεργασία συμβολοσειρών και αφήνετε τη βιβλιοθήκη να διαχειριστεί τη μετατροπή για εσάς. Αυτός ο οδηγός καλύπτει επίσης το τελικό βήμα της αποθήκευσης του αρχείου ως αρχείο `.xlsx`.

## Προαπαιτούμενα

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

* Java 17 ή νεότερη εγκατεστημένη.
* Maven 3.6+ (ή Gradle) για διαχείριση εξαρτήσεων.
* Ένα IDE όπως IntelliJ IDEA ή Eclipse.
* Τη βιβλιοθήκη Aspose.Cells for Java (το παράδειγμα χρησιμοποιεί την έκδοση 23.10, αλλά οποιαδήποτε πρόσφατη έκδοση λειτουργεί).

## Βήμα 1: Προσθέστε το Aspose.Cells στο έργο σας

Η βιβλιοθήκη παρέχει τις κλάσεις `Workbook`, `Worksheet` και `WorkbookSettings` που χρησιμοποιούνται σε όλο το tutorial.

**Maven**

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

**Gradle**

```gradle
implementation 'com.aspose:aspose-cells:23.10:jdk17'
```

> **Pro tip:** Χρησιμοποιήστε το JAR `javadoc` για να έχετε ενσωματωμένη τεκμηρίωση ενώ γράφετε κώδικα.

## Βήμα 2: Δημιουργήστε το βιβλίο εργασίας και αποκτήστε πρόσβαση στο πρώτο φύλλο εργασίας

Τώρα δημιουργούμε ένα νέο αντικείμενο workbook και παίρνουμε το προεπιλεγμένο πρώτο φύλλο.

```java
import com.aspose.cells.*;

public class JapaneseEraExample {
    public static void main(String[] args) throws Exception {
        // Step 2: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();                // create an empty workbook
        Worksheet worksheet = workbook.getWorksheets().get(0); // first sheet (index 0)
```

*Γιατί είναι σημαντικό αυτό το βήμα:* Το `Workbook` αντιπροσωπεύει ολόκληρο το αρχείο Excel, ενώ το `Worksheet` είναι ο καμβάς όπου τοποθετείτε τα κελιά. Ξεκινώντας με ένα καθαρό workbook διασφαλίζετε ότι δεν υπάρχει κρυφή μορφοποίηση που να επηρεάζει την ανάλυση της ημερομηνίας.

## Βήμα 3: Εισάγετε μια ημερομηνία ιαπωνικής εποχής σε ένα κελί

Οι ημερομηνίες ιαπωνικής εποχής ακολουθούν το μοτίβο “<EraLetter><Year>/<Month>/<Day>”. Σε αυτό το παράδειγμα χρησιμοποιούμε “R3” (Reiwa 3 = 2021).

```java
        // Step 3: Put a Japanese era date into cell A1
        Cell dateCell = worksheet.getCells().get("A1");
        dateCell.putValue("R3/05/01");   // Reiwa 3, May 1st
```

*Γιατί είναι σημαντικό αυτό το βήμα:* Γράφοντας τη συμβολοσειρά εποχής απευθείας, αφήνετε το Aspose.Cells να διαχειριστεί τη μετατροπή αργότερα. Αποφεύγετε την ανάγκη να μετατρέψετε το “R3” σε “2021” εσείς.

## Βήμα 4: Ενεργοποιήστε την ανάλυση ιαπωνικής εποχής και επανυπολογίστε τους τύπους

Ενημερώστε το workbook ώστε να θεωρεί τις συμβολοσειρές εποχής ως ημερομηνίες. Μετά την αλλαγή της ρύθμισης, καλέστε `calculateFormula()` ώστε τυχόν εξαρτημένοι τύποι (αν τους προσθέσετε αργότερα) να δουν τη σωστή Γρηγοριανή τιμή.

```java
        // Step 4: Turn on Japanese era parsing
        WorkbookSettings settings = workbook.getSettings();
        settings.setUseJapaneseEra(true);   // enable era conversion
        workbook.calculateFormula();        // refresh any formulas
```

*Γιατί είναι σημαντικό αυτό το βήμα:* Η σημαία `setUseJapaneseEra(true)` υποδεικνύει στο Aspose.Cells να ερμηνεύσει συμβολοσειρές όπως “R3/05/01” ως Γρηγοριανές ημερομηνίες. Χωρίς αυτήν, το κελί θα διατηρούσε το κυριολεκτικό κείμενο, διακόπτοντας τις επόμενες υπολογιστικές διαδικασίες.

## Βήμα 5: Επαληθεύστε τη μετατροπή και **save workbook as xlsx**

Εκτυπώστε την μετατρεπόμενη τιμή στην κονσόλα και αποθηκεύστε το workbook.

```java
        // Step 5: Verify conversion and save the file
        System.out.println("Converted date: " + dateCell.getStringValue()); // → 2021-05-01
        workbook.save("JapaneseEra.xlsx");   // saves as .xlsx by default
    }
}
```

**Αναμενόμενη έξοδος κονσόλας**

```
Converted date: 2021-05-01
```

Το αρχείο `JapaneseEra.xlsx` περιέχει τώρα τη Γρηγοριανή ημερομηνία `2021‑05‑01` στο κελί A1, παρόλο που η αρχική συμβολοσειρά χρησιμοποιούσε τη μορφή ιαπωνικής εποχής.

## Βήμα 6: Συνηθισμένες παραλλαγές και διαχείριση ακραίων περιπτώσεων

| Σενάριο | Πώς να προσαρμόσετε τον κώδικα |
|----------|-----------------------|
| Διαφορετική εποχή (π.χ., Heisei) | Χρησιμοποιήστε “H30/12/31” για Heisei 30 = 2018‑12‑31. Η ίδια σημαία `setUseJapaneseEra(true)` λειτουργεί για όλες τις υποστηριζόμενες εποχές. |
| Κενή ή κακώς διαμορφωμένη συμβολοσειρά | Τυλίξτε το `putValue` σε μπλοκ try‑catch και επικυρώστε με regex όπως `^[RHS][0-9]+/[0-9]{2}/[0-9]{2}$`. |
| Απαιτείται η διατήρηση της αρχικής συμβολοσειράς εποχής για έλεγχο | Αποθηκεύστε τη ακατέργαστη συμβολοσειρά σε κρυφή στήλη πριν τη μετατροπή, έπειτα κρύψτε αυτή τη στήλη στο τελικό workbook. |
| Μεγάλα σύνολα δεδομένων | Ενεργοποιήστε `WorkbookSettings.setEnableThreadedCalculation(true)` για να επιταχύνετε τον επανυπολογισμό τύπων όταν πολλές γραμμές χρησιμοποιούν ημερομηνίες εποχής. |

> **Watch out for:** Η χρήση παλαιότερης έκδοσης του Aspose.Cells που προέρχεται πριν από την υποστήριξη ιαπωνικής εποχής (προ‑2020) θα αγνοήσει τη σημαία `setUseJapaneseEra`, αφήνοντας το κελί αμετάβλητο.

## Βήμα 7: Εκτελέστε το παράδειγμα

Συγκεντρώστε και τρέξτε την κλάση από το IDE ή μέσω γραμμής εντολών:

```bash
javac -cp "path/to/aspose-cells-23.10.jar" JapaneseEraExample.java
java -cp ".:path/to/aspose-cells-23.10.jar" JapaneseEraExample
```

Μετά την εκτέλεση, ανοίξτε το `JapaneseEra.xlsx` στο Excel. Το κελί A1 εμφανίζει `2021-05-01`, επιβεβαιώνοντας ότι η **java excel date conversion** ολοκληρώθηκε με επιτυχία.

## Συμπέρασμα

Τώρα ξέρετε πώς να **create excel workbook java**, να εισάγετε μια ημερομηνία ιαπωνικής εποχής, να ενεργοποιήσετε την αυτόματη ανάλυση εποχής, και να **save workbook as xlsx**. Αυτή η προσέγγιση εξαλείφει τις χειροκίνητες αριθμητικές πράξεις με ημερομηνίες και εξασφαλίζει ότι τα αρχεία Excel σας παραμένουν συμβατά με τα τυπικά Γρηγοριανά ημερολόγια.

### Τι να εξερευνήσετε στη συνέχεια

* **Μορφοποίηση ημερομηνιών** – εφαρμόστε στυλ κελιών (`Style style = workbook.createStyle(); style.setNumber(14);`) για να εμφανίζετε ημερομηνίες στην προτιμώμενη τοπική ρύθμιση.
* **Μαζική μετατροπή** – επαναλάβετε πάνω σε μια στήλη συμβολοσειρών εποχής και μετατρέψτε κάθε κελί σε βρόχο.
* **Εξαγωγή σε άλλες μορφές** – το Aspose.Cells υποστηρίζει επίσης PDF, CSV και ODS· απλώς αλλάξτε την επέκταση αρχείου στο `workbook.save(...)`.

Νιώστε ελεύθεροι να πειραματιστείτε με άλλες εποχές, προσαρμοσμένες μορφές ή να συνδυάσετε αυτήν την τεχνική με αναφορές που βασίζονται σε τύπους. Καλή προγραμματιστική!

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε επιπλέον δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να δημιουργήσετε και να αποθηκεύσετε ένα βιβλίο εργασίας Excel ως SVG χρησιμοποιώντας το Aspose.Cells για Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [Δημιουργία και αποθήκευση βιβλίου εργασίας Excel Aspose Cells Java](/cells/german/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)
- [Δημιουργία και αποθήκευση βιβλίου εργασίας Excel Aspose Cells Java](/cells/french/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}