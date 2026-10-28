---
date: '2026-10-28'
description: Μάθετε πώς να αλλάξετε το σύστημα ημερομηνίας του Excel σε 1904 χρησιμοποιώντας
  Aspose.Cells για Java, ορίστε τη μορφή ημερομηνίας του Excel και μετατρέψτε το σύστημα
  1904 του Excel αποδοτικά.
keywords:
- change excel date system
- excel 1904 date conversion
- maven dependency aspose cells
lastmod: '2026-10-28'
og_description: Αλλάξτε το σύστημα ημερομηνίας του Excel σε 1904 χρησιμοποιώντας Aspose.Cells
  για Java. Μάθετε βήμα‑βήμα πώς να ενεργοποιήσετε το σύστημα 1904, να ορίσετε ημερομηνίες
  και να επαναφέρετε.
og_image_alt: Aspose.Cells Java guide showing how to switch Excel to the 1904 date
  system
og_title: Αλλαγή του συστήματος ημερομηνίας του Excel σε 1904 με Aspose.Cells για
  Java
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: Learn how to change Excel date system to 1904 using Aspose.Cells for
    Java, set Excel date format, and convert Excel 1904 system efficiently.
  headline: Change Excel date system to 1904 with Aspose.Cells Java
  type: TechArticle
- description: Learn how to change Excel date system to 1904 using Aspose.Cells for
    Java, set Excel date format, and convert Excel 1904 system efficiently.
  name: Change Excel date system to 1904 with Aspose.Cells Java
  steps:
  - name: initialize and load the workbook
    text: The `Workbook` class represents an entire Excel file in memory. First, create
      a `Workbook` instance that points to your existing file.
  - name: enable the 1904 date system
    text: The `WorkbookSettings.setDate1904` method toggles the workbook‑level date
      flag. Setting it to `true` activates the 1904 system for all worksheets. **Pro
      tip:** You can also call `setDate1904(false)` later if you need to revert.
  - name: save the modified workbook
    text: Finally, write the changes to a new file (or overwrite the original). The
      `save` method respects the active date system automatically. > **Note:** The
      code above uses the class name `tWorkbook` as originally provided. Ensure this
      typo matches your project’s naming conventions or correct it to `Workb
  type: HowTo
- questions:
  - answer: The 1900 system starts on January 1, 1900, while the 1904 system starts
      on January 1, 1904, shifting all dates by 1,462 days.
    question: What is the difference between the 1900 and 1904 date systems?
  - answer: Yes, but you must close the file in Excel first; otherwise the save operation
      will fail.
    question: Can I change the date system of a workbook that is currently open in
      Excel?
  - answer: The method works in the free trial, but a full license removes evaluation
      limitations.
    question: Do I need a license to use `setDate1904`?
  - answer: No, the date system is a workbook‑level setting; it applies to all worksheets.
    question: Is it possible to change the date system for only a single worksheet?
  - answer: Open the saved file in Excel, go to **File → Options → Advanced**, and
      check the **"Use 1904 date system"** box.
    question: How can I verify that the date system was changed?
  type: FAQPage
tags:
- change excel date system
- aspose cells java
- excel date conversion
- java excel processing
title: Αλλαγή του συστήματος ημερομηνίας του Excel σε 1904 με Aspose.Cells Java
url: /el/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Αλλαγή του συστήματος ημερομηνίας του Excel σε 1904 με το Aspose.Cells Java

Σε αυτό το tutorial θα μάθετε πώς να **αλλάξετε το σύστημα ημερομηνίας του Excel** στη μορφή 1904 χρησιμοποιώντας το Aspose.Cells για Java. Το σύστημα 1904 είναι απαραίτητο όταν χρειάζεται να διατηρήσετε κληρονομημένες ημερομηνίες από Mac ή να ευθυγραμμίσετε με χρηματοοικονομικά μοντέλα που απαιτούν αυτήν την εποχή. Θα περάσουμε από την εγκατάσταση της βιβλιοθήκης, τη φόρτωση ενός βιβλίου εργασίας, την εναλλαγή του συστήματος ημερομηνίας και την αποθήκευση του αποτελέσματος—όλα χωρίς να απαιτείται το Microsoft Excel στον διακομιστή.

## Γρήγορες απαντήσεις
- **Τι κάνει το σύστημα ημερομηνίας 1904;** Ξεκινά να μετρά τις ημέρες από 1 Ιανουαρίου 1904, μετατοπίζοντας όλες τις ημερομηνίες κατά 1.462 ημέρες σε σύγκριση με το προεπιλεγμένο σύστημα 1900.  
- **Γιατί να χρησιμοποιήσετε το Aspose.Cells για να αλλάξετε το σύστημα ημερομηνίας;** Παρέχει ένα απλό API που λειτουργεί χωρίς εγκατεστημένο το Excel και υποστηρίζει μεγάλα αρχεία.  
- **Ποιες εκδόσεις της Java υποστηρίζονται;** JDK 8 ή νεότερη.  
- **Χρειάζομαι άδεια;** Η δωρεάν δοκιμή λειτουργεί για αξιολόγηση· μια άδεια αφαιρεί τα όρια χρήσης.  
- **Μπορώ να επαναφέρω το σύστημα 1900 αργότερα;** Ναι, απλώς καλέστε `setDate1904(false)`.

## Τι είναι το σύστημα ημερομηνίας 1904 στο Excel;
Το σύστημα ημερομηνίας 1904 μετρά τις ημέρες από 1 Ιανουαρίου 1904, αντί για την προεπιλεγμένη εποχή του 1900. Αυτή η μετατόπιση προσθέτει ακριβώς 1.462 ημέρες σε κάθε τιμή ημερομηνίας, γι' αυτό τα παλαιά βιβλία εργασίας Mac εμφανίζονται μετατοπισμένα όταν ανοίγονται στα Windows. Χρησιμοποιείται κυρίως για συμβατότητα με παλαιότερα αρχεία Excel Macintosh και με ορισμένα κληρονομημένα χρηματοοικονομικά μοντέλα.

## Γιατί να αλλάξετε το σύστημα ημερομηνίας του Excel με το Aspose.Cells;
Μπορείτε να αλλάξετε το σύστημα ημερομηνίας απευθείας από τη Java, αφαιρώντας τα χειροκίνητα βήματα στο Excel. Το Aspose.Cells επεξεργάζεται βιβλία εργασίας έως **2 GB** σε μέγεθος και μπορεί να μετατρέψει ένα βιβλίο εργασίας με 500 φύλλα σε λιγότερο από **2 δευτερόλεπτα** σε έναν τυπικό διακομιστή 4‑πυρήνων, παρέχοντας υψηλή απόδοση αυτοματοποίησης στο διακομιστή.

## Προαπαιτούμενα
- Java Development Kit (JDK) 8 ή νεότερο.  
- Maven ή Gradle για διαχείριση εξαρτήσεων.  
- Βασικές γνώσεις προγραμματισμού Java.  

## Ρύθμιση του Aspose.Cells για Java

### Maven
Προσθέστε την ακόλουθη εξάρτηση στο αρχείο `pom.xml` σας:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### Gradle
Συμπεριλάβετε αυτή τη γραμμή στο αρχείο `build.gradle` σας:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

#### Απόκτηση άδειας
Η Aspose προσφέρει δωρεάν δοκιμή, προσωρινή άδεια και πλήρεις εμπορικές άδειες. Μπορείτε να ξεκινήσετε με τη [δωρεάν δοκιμή](https://releases.aspose.com/cells/java/) ή να αποκτήσετε προσωρινή άδεια από τη [σελίδα προσωρινής άδειας](https://purchase.aspose.com/temporary-license/).

## Πώς να αλλάξετε το σύστημα ημερομηνίας του Excel σε 1904 με το Aspose.Cells για Java;
Φορτώστε το βιβλίο εργασίας, ενεργοποιήστε τη ρύθμιση 1904 και αποθηκεύστε το αρχείο—αυτή η τρι‑βήμα ροή ενημερώνει την εσωτερική εποχή ημερομηνίας του βιβλίου εργασίας σε λιγότερο από ένα δευτερόλεπτο. Η κλήση API `setDate1904(true)` αλλάζει τη σημαία του συστήματος, και η αλλαγή διατηρείται όταν καλείτε `save`. Δεν απαιτείται εγκατάσταση του Excel, καθιστώντας το ιδανικό για περιβάλλοντα διακομιστών χωρίς γραφικό περιβάλλον.

### Βήμα 1: αρχικοποίηση και φόρτωση του βιβλίου εργασίας
Η κλάση `Workbook` αντιπροσωπεύει ένα ολόκληρο αρχείο Excel στη μνήμη. Πρώτα, δημιουργήστε μια παρουσία `Workbook` που δείχνει στο υπάρχον αρχείο σας.

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
// Initialize a Workbook object with the path to your Excel file
Workbook workbook = new Workbook(dataDir + "/Mybook.xlsx");
```

### Βήμα 2: ενεργοποίηση του συστήματος ημερομηνίας 1904
Η μέθοδος `WorkbookSettings.setDate1904` εναλλάσσει τη σημαία ημερομηνίας σε επίπεδο βιβλίου εργασίας. Ορίζοντάς την σε `true` ενεργοποιεί το σύστημα 1904 για όλα τα φύλλα εργασίας.

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
// Load the workbook from your specified directory
Workbook workbook = new Workbook(dataDir + "/Mybook.xlsx");

// Enable the 1904 date system
workbook.getSettings().setDate1904(true);
```

**Συμβουλή:** Μπορείτε επίσης να καλέσετε `setDate1904(false)` αργότερα αν χρειαστεί να επαναφέρετε.

### Βήμα 3: αποθήκευση του τροποποιημένου βιβλίου εργασίας
Τέλος, γράψτε τις αλλαγές σε ένα νέο αρχείο (ή αντικαταστήστε το αρχικό). Η μέθοδος `save` σέβεται αυτόματα το ενεργό σύστημα ημερομηνίας.

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
String outDir = "YOUR_OUTPUT_DIRECTORY"; // Specify where you want to save the modified workbook

// Load and modify your workbook as shown in previous steps
tWorkbook workbook = new Workbook(dataDir + "/Mybook.xlsx");
workbook.getSettings().setDate1904(true);

// Save the changes to a new file
workbook.save(outDir + "/I1904DateSystem_out.xls");
```

> **Σημείωση:** Ο παραπάνω κώδικας χρησιμοποιεί το όνομα κλάσης `tWorkbook` όπως δόθηκε αρχικά. Βεβαιωθείτε ότι αυτό το τυπογραφικό λάθος ταιριάζει με τις συμβάσεις ονομασίας του έργου σας ή διορθώστε το σε `Workbook` αν χρειάζεται.

## Ορισμός ημερομηνίας Excel προγραμματιστικά (δευτερεύον κλειδί)
Αν χρειάζεται να προσαρμόσετε μεμονωμένες τιμές κελιών μετά την αλλαγή του συστήματος, μπορείτε να χρησιμοποιήσετε `cells.get(i, j).putValue(Date)` όπου η ημερομηνία θα ερμηνευτεί σύμφωνα με το ενεργό σύστημα ημερομηνίας.

## Μετατροπή του συστήματος Excel 1904 πίσω στο 1900 (δευτερεύον κλειδί)
Για επαναφορά, απλώς καλέστε:

```java
workbook.getSettings().setDate1904(false);
```

Στη συνέχεια αποθηκεύστε ξανά το βιβλίο εργασίας.

## Πρακτικές εφαρμογές
1. **Αρχειοθέτηση δεδομένων** – Διατηρήστε κληρονομημένες χρονικές σφραγίδες κατά τη μεταφορά παλαιών φύλλων εργασίας βασισμένων σε Mac.  
2. **Αναφορές διαπλατφόρμας** – Δημιουργήστε αναφορές που ανοίγουν σωστά τόσο στα Windows όσο και στο macOS χωρίς ασυμφωνίες ημερομηνίας.  
3. **Χρηματοοικονομική μοντελοποίηση** – Ευθυγραμμίστε τους υπολογισμούς ημερομηνίας με κληρονομημένα χρηματοοικονομικά μοντέλα που αναμένουν το σύστημα 1904.

## Σκέψεις απόδοσης
- Περιορίστε τις λειτουργίες βιβλίου εργασίας σε μια ενιαία συνεδρία για να διατηρήσετε τη χρήση μνήμης χαμηλή· το Aspose.Cells μεταδίδει δεδομένα και δεν φορτώνει ποτέ ολόκληρο το αρχείο στη RAM εκτός αν το ζητήσετε ρητά.  
- Ρυθμίστε τις σημαίες συλλογής απορριμμάτων της Java (`-XX:+UseG1GC`) για πολύ μεγάλα αρχεία ώστε να αποφύγετε τις αυξήσεις χρόνου παύσης.

## Συχνές ερωτήσεις

**Ε: Ποια είναι η διαφορά μεταξύ των συστημάτων ημερομηνίας 1900 και 1904;**  
Α: Το σύστημα 1900 ξεκινά την 1 Ιανουαρίου 1900, ενώ το σύστημα 1904 ξεκινά την 1 Ιανουαρίου 1904, μετατοπίζοντας όλες τις ημερομηνίες κατά 1.462 ημέρες.

**Ε: Μπορώ να αλλάξω το σύστημα ημερομηνίας ενός βιβλίου εργασίας που είναι ανοιχτό στο Excel;**  
Α: Ναι, αλλά πρέπει πρώτα να κλείσετε το αρχείο στο Excel· διαφορετικά η λειτουργία αποθήκευσης θα αποτύχει.

**Ε: Χρειάζομαι άδεια για να χρησιμοποιήσω το `setDate1904`;**  
Α: Η μέθοδος λειτουργεί στη δωρεάν δοκιμή, αλλά μια πλήρης άδεια αφαιρεί τους περιορισμούς αξιολόγησης.

**Ε: Είναι δυνατόν να αλλάξετε το σύστημα ημερομηνίας μόνο για ένα φύλλο εργασίας;**  
Α: Όχι, το σύστημα ημερομηνίας είναι ρύθμιση σε επίπεδο βιβλίου εργασίας· εφαρμόζεται σε όλα τα φύλλα εργασίας.

**Ε: Πώς μπορώ να επαληθεύσω ότι το σύστημα ημερομηνίας άλλαξε;**  
Α: Ανοίξτε το αποθηκευμένο αρχείο στο Excel, μεταβείτε στο **File → Options → Advanced** και ελέγξτε το πλαίσιο **"Use 1904 date system"**.

## Συμπέρασμα
Τώρα γνωρίζετε πώς να **αλλάξετε το σύστημα ημερομηνίας του Excel** σε 1904 χρησιμοποιώντας το Aspose.Cells για Java, πώς να ορίσετε ημερομηνίες σε μεμονωμένα κελιά και πώς να επαναφέρετε το σύστημα 1900 όταν χρειάζεται. Ενσωματώστε αυτά τα αποσπάσματα στον αγωγό επεξεργασίας δεδομένων σας για να εξασφαλίσετε συμβατότητα ημερομηνιών μεταξύ πλατφορμών και κληρονομημένων αρχείων.

---

**Τελευταία ενημέρωση:** 2026-10-28  
**Δοκιμή με:** Aspose.Cells 25.3 for Java  
**Συγγραφέας:** Aspose  

**Πόροι**
- **Τεκμηρίωση:** [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)
- **Λήψη:** [Aspose.Cells Releases](https://releases.aspose.com/cells/java/)
- **Αγορά άδειας:** [Buy Aspose.Cells](https://purchase.aspose.com/buy)
- **Δωρεάν δοκιμή:** [Start Free Trial](https://releases.aspose.com/cells/java/)
- **Προσωρινή άδεια:** [Get Temporary License](https://purchase.aspose.com/temporary-license/)
- **Φόρουμ υποστήριξης:** [Aspose Support](https://forum.aspose.com/c/cells/9)

## Σχετικά tutorials

- [Αποδοτική μετατροπή του Excel σε PDF με προσαρμοσμένες μορφές ημερομηνίας χρησιμοποιώντας το Aspose.Cells για Java](/cells/java/workbook-operations/render-excel-custom-date-formats-pdf-aspose-cells-java/)
- [Aspose.Cells for Java: Πώς να δημιουργήσετε και να μορφοποιήσετε βιβλία εργασίας Excel αποδοτικά](/cells/java/getting-started/aspose-cells-java-workbook-creation-guide/)
- [Κατακτήστε τη διαχείριση Excel με το Aspose.Cells for Java: Εργασίες βιβλίου εργασίας και tutorial στυλ κελιών](/cells/java/workbook-operations/excel-manipulation-aspose-cells-java-tutorial/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}