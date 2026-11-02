---
category: general
date: 2026-07-16
description: Εξαγωγή Excel σε TXT χρησιμοποιώντας το Aspose.Cells σε Java. Μάθετε
  πώς να ορίζετε τα σημαντικά ψηφία, να αποθηκεύετε το Excel ως αρχείο κειμένου και
  να ελέγχετε τη μορφή εξόδου.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to txt
- how to set significant digits
- save excel as text file
- save workbook as txt
language: el
lastmod: 2026-07-16
og_description: Εξαγωγή Excel σε TXT σε Java με το Aspose.Cells. Αυτό το σεμινάριο
  σας δείχνει πώς να ορίσετε σημαντικά ψηφία, να αποθηκεύσετε το Excel ως αρχείο κειμένου
  και να έχετε αξιόπιστα αποτελέσματα.
og_image_alt: Screenshot of Java code exporting an Excel workbook to a TXT file with
  4 significant digits
og_title: Εξαγωγή Excel σε TXT σε Java – Οδηγός βήμα‑προς‑βήμα
schemas:
- author: Aspose
  dateModified: '2026-07-16'
  description: Export Excel to TXT using Aspose.Cells in Java. Learn how to set significant
    digits, save Excel as text file, and control the output format.
  headline: Export Excel to TXT with Java – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Export Excel to TXT using Aspose.Cells in Java. Learn how to set significant
    digits, save Excel as text file, and control the output format.
  name: Export Excel to TXT with Java – Complete Step‑by‑Step Guide
  steps:
  - name: Prerequisites
    text: '- Java Development Kit (JDK) 8 or newer. - Maven or Gradle to manage the
      Aspose.Cells dependency (we’ll show the Maven snippet). - A basic understanding
      of Java syntax (if you’ve written a “Hello World”, you’re good).'
  - name: Understanding `setSignificantDigits`
    text: '- **Definition:** The number of digits that remain after the decimal point,
      *including* leading digits. For `123.456789` with `4` significant digits, the
      output becomes `123.5`. - **When to use:** If the downstream system expects
      a fixed precision (e.g., scientific data files), or you need to trunca'
  - name: Folder Considerations
    text: '- The `output` folder must exist, or you’ll get an `IOException`. You can
      create it programmatically:'
  - name: 1️⃣ What if I need a different delimiter?
    text: "`TxtSaveOptions` also offers `setSeparator('\t')` for tabs or `setSeparator(',')`
      for CSV‑style output. Example:"
  - name: 2️⃣ How does locale affect decimal separators?
    text: 'By default Aspose uses the system locale. If you need a period (`.`) regardless
      of locale, set:'
  - name: 3️⃣ Large worksheets – memory concerns?
    text: Aspose.Cells streams data to disk when working with worksheets larger than
      1 GB, so you usually won’t hit an `OutOfMemoryError`. Still, avoid loading massive
      sheets into memory if you only need a subset; use `Workbook.getWorksheets().get(index)`
      to target a specific sheet.
  - name: 4️⃣ Can I export only a range?
    text: Yes. Use `txtOptions.setExportRange("A1:B10")` to restrict the output to
      a specific area. This reduces file size and speeds up the export.
  - name: 5️⃣ What if I don’t have a license?
    text: The evaluation mode adds a watermark line (`"Aspose.Cells for Java Evaluation
      Version"`). For production you’ll need a license; otherwise the watermark may
      break downstream parsers.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Εξαγωγή Excel σε TXT με Java – Πλήρης Οδηγός Βήμα‑βήμα
url: /el/java/excel-import-export/export-excel-to-txt-with-java-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή Excel σε TXT με Java – Πλήρης Οδηγός Βήμα‑Βήμα

Αναρωτηθήκατε ποτέ **πώς να εξάγετε Excel σε TXT** χωρίς να χάσετε την αριθμητική ακρίβεια; Ίσως χρειάζεστε μια απλή εξαγωγή κειμένου για ένα παλαιό σύστημα, ή τροφοδοτείτε δεδομένα σε μια επιστημονική αλυσίδα που απαιτεί συγκεκριμένο αριθμό σημαντικών ψηφίων. Σε αυτό το tutorial θα περάσουμε από ένα **πλήρες, εκτελέσιμο παράδειγμα Java** που σας δείχνει ακριβώς αυτό—συμπεριλαμβανομένου του **πώς να ορίσετε σημαντικά ψηφία**, **να αποθηκεύσετε το Excel ως αρχείο κειμένου**, και **να αποθηκεύσετε το βιβλίο εργασίας ως txt** χρησιμοποιώντας το Aspose.Cells.

Θα καλύψουμε τα πάντα από τη ρύθμιση του έργου μέχρι το τελικό βήμα επαλήθευσης, ώστε να μπορείτε να αντιγράψετε‑επικολλήσετε τον κώδικα, να τον εκτελέσετε και να δείτε το αποτέλεσμα άμεσα. Χωρίς μυστικές εξαρτήσεις, χωρίς συντομεύσεις “δείτε τα έγγραφα”—απλώς μια σαφής, ολοκληρωμένη λύση.

---

## Τι Θα Μάθετε

- Πώς να δημιουργήσετε ένα βιβλίο εργασίας προγραμματιστικά με το Aspose.Cells.
- Η ακριβής κλήση API για **ορισμό σημαντικών ψηφίων** για εξαγωγή TXT.
- Η διαφορά μεταξύ `TxtSaveOptions` και άλλων επιλογών αποθήκευσης.
- Πώς να **αποθηκεύσετε το Excel ως αρχείο κειμένου** σε οποιοδήποτε OS (Windows, macOS, Linux).
- Κοινά προβλήματα (διαχωριστές δεκαδικών ανάλογα με την τοπική ρύθμιση, μεγάλα φύλλα εργασίας) και πώς να τα αποφύγετε.
- Μια πλήρης, έτοιμη προς εκτέλεση κλάση Java που μπορείτε να προσαρμόσετε στα δικά σας έργα.

### Προαπαιτούμενα

- Java Development Kit (JDK) 8 ή νεότερο.
- Maven ή Gradle για τη διαχείριση της εξάρτησης Aspose.Cells (θα δείξουμε το απόσπασμα Maven).
- Βασική κατανόηση της σύνταξης Java (αν έχετε γράψει ένα “Hello World”, είστε εντάξει).

---

## Βήμα 1: Ρύθμιση του Έργου και Προσθήκη Aspose.Cells

Αρχικά, ας προσθέσουμε τη βιβλιοθήκη στο build μας. Αν χρησιμοποιείτε Maven, προσθέστε αυτό στο `pom.xml` σας:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest stable version -->
</dependency>
```

> **Συμβουλή επαγγελματία:** Το Aspose προσφέρει δωρεάν άδεια αξιολόγησης 30 ημερών. Τοποθετήστε το αρχείο `Aspose.Total.lic` στη ρίζα του έργου σας, ή καλέστε `License.setLicense("path/to/license")` πριν από οποιαδήποτε χρήση του API.

Μόλις η εξάρτηση λυθεί, μπορείτε να αρχίσετε τον κώδικα. Αν προτιμάτε Gradle, το ισοδύναμο είναι:

```gradle
implementation 'com.aspose:aspose-cells:24.9'
```

---

## Βήμα 2: Εξαγωγή Excel σε TXT – Δημιουργία Βιβλίου Εργασίας

Τώρα θα δημιουργήσουμε ένα νέο βιβλίο εργασίας, θα προσθέσουμε μια αριθμητική τιμή και θα το προετοιμάσουμε για εξαγωγή. Αυτό είναι η ουσία του **export excel to txt**.

```java
import com.aspose.cells.*;

public class ExportExcelToTxtDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create a fresh workbook (in‑memory Excel file)
        Workbook workbook = new Workbook();

        // 2️⃣ Grab the first worksheet – it's created by default
        Worksheet sheet = workbook.getWorksheets().get(0);

        // 3️⃣ Put a numeric value into cell A1
        Cell cell = sheet.getCells().get("A1");
        cell.putValue(123.456789); // Example number with many decimals
```

**Γιατί είναι σημαντικό:** Με την κατασκευή του βιβλίου εργασίας μέσω κώδικα αποφεύγουμε τυχόν κρυφή μορφοποίηση που μπορεί να προέλθει από ένα αρχείο προτύπου. Η μέθοδος `putValue` εντοπίζει αυτόματα τον τύπο δεδομένων, έτσι το κελί γίνεται **αριθμητικό**—όχι συμβολοσειρά.

---

## Βήμα 3: Πώς να Ορίσετε Σημαντικά Ψηφία για Έξοδο TXT

Όταν εξάγετε σε απλό κείμενο, το Aspose.Cells γράφει την ακατέργαστη αριθμητική τιμή εξ ορισμού. Για να περιορίσετε την έξοδο, π.χ., σε **4 σημαντικά ψηφία**, πρέπει να τροποποιήσετε το `TxtSaveOptions`.

```java
        // 4️⃣ Configure TXT save options – this is where we set the precision
        TxtSaveOptions txtOptions = new TxtSaveOptions();
        txtOptions.setSignificantDigits(4); // <-- controls significant digits
```

### Κατανόηση του `setSignificantDigits`

- **Ορισμός:** Ο αριθμός των ψηφίων που παραμένουν μετά το δεκαδικό σημείο, *συμπεριλαμβανομένων* των αρχικών ψηφίων. Για `123.456789` με `4` σημαντικά ψηφία, η έξοδος γίνεται `123.5`.
- **Πότε να το χρησιμοποιήσετε:** Αν το σύστημα-παραλήπτης απαιτεί σταθερή ακρίβεια (π.χ., επιστημονικά αρχεία δεδομένων), ή χρειάζεται να περικόψετε για να αποφύγετε θόρυβο κινητής υποδιαστολής.
- **Ακραία περίπτωση:** Αν ο αριθμός έχει λιγότερα ψηφία από τον καθορισμένο αριθμό, το Aspose θα διατηρήσει την αρχική τιμή (χωρίς συμπλήρωση μηδενικών).

> **Γιατί όχι `setDecimalPlaces`;** Αυτή η ιδιότητα ελέγχει *μόνο* τα ψηφία μετά το δεκαδικό σημείο, αγνοώντας τα αρχικά ψηφία. Για επιστημονικά δεδομένα, το `significantDigits` είναι συνήθως η σωστή επιλογή.

---

## Βήμα 4: Αποθήκευση Excel ως Αρχείο Κειμένου (TXT)

Με τις επιλογές έτοιμες, τελικά γράφουμε το βιβλίο εργασίας σε αρχείο `.txt`. Αυτό είναι το βήμα **save workbook as txt**.

```java
        // 5️⃣ Persist the workbook as a TXT file
        String outputPath = "output/SignificantDigits.txt";
        workbook.save(outputPath, txtOptions);

        System.out.println("Excel exported to TXT at: " + outputPath);
    }
}
```

### Σκέψεις για Φάκελο

- Ο φάκελος `output` πρέπει να υπάρχει, αλλιώς θα προκύψει `IOException`. Μπορείτε να τον δημιουργήσετε προγραμματιστικά:

```java
new java.io.File("output").mkdirs();
```

- Σε Linux/macOS, οι διαδρομές είναι ευαίσθητες σε πεζά/κεφαλαία γράμματα· στα Windows δεν είναι. Χρησιμοποιήστε ονόματα φακέλων με πεζά γράμματα για ασφαλή διασυστημική χρήση.

---

## Βήμα 5: Επαλήθευση του Αποτελέσματος

Εκτελέστε το πρόγραμμα (`mvn compile exec:java -Dexec.mainClass=ExportExcelToTxtDemo`) και ανοίξτε το `output/SignificantDigits.txt`. Θα πρέπει να δείτε:

```
123.5
```

Αυτή η μοναδική γραμμή επιβεβαιώνει:

- Το βιβλίο εργασίας αποθηκεύτηκε επιτυχώς **ως αρχείο κειμένου**.
- Η αριθμητική τιμή σέβεται τα **4 σημαντικά ψηφία** που ορίσαμε.
- Δεν υπάρχουν επιπλέον κόμματα, στηλοθέτες ή μεταδεδομένα ειδικά για το Excel που έχουν διαρρεύσει στο αρχείο.

Αν χρειάζεστε διάταξη με διαχωριστικό στηλοθέτη για πολλές στήλες, απλώς γεμίστε περισσότερα κελιά και το Aspose θα εισάγει αυτόματα τα tabs.

---

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

### 1️⃣ Τι γίνεται αν χρειάζομαι διαφορετικό διαχωριστικό;

`TxtSaveOptions` προσφέρει επίσης `setSeparator('\t')` για tabs ή `setSeparator(',')` για έξοδο τύπου CSV. Παράδειγμα:

```java
txtOptions.setSeparator('\t'); // Tab delimiter
```

### 2️⃣ Πώς επηρεάζει η τοπική ρύθμιση τους διαχωριστές δεκαδικών;

Από προεπιλογή το Aspose χρησιμοποιεί τη τοπική ρύθμιση του συστήματος. Αν χρειάζεστε τελεία (`.`) ανεξάρτητα από τη ρύθμιση, ορίστε:

```java
txtOptions.setCultureInfo(java.util.Locale.US);
```

### 3️⃣ Μεγάλα φύλλα εργασίας – ανησυχίες μνήμης;

Το Aspose.Cells μεταφέρει δεδομένα στο δίσκο όταν εργάζεται με φύλλα μεγαλύτερα από 1 GB, έτσι συνήθως δεν θα αντιμετωπίσετε `OutOfMemoryError`. Παρόλα αυτά, αποφύγετε τη φόρτωση τεράστιων φύλλων στη μνήμη αν χρειάζεστε μόνο ένα υποσύνολο· χρησιμοποιήστε `Workbook.getWorksheets().get(index)` για να στοχεύσετε ένα συγκεκριμένο φύλλο.

### 4️⃣ Μπορώ να εξάγω μόνο μια περιοχή;

Ναι. Χρησιμοποιήστε `txtOptions.setExportRange("A1:B10")` για να περιορίσετε την έξοδο σε συγκεκριμένη περιοχή. Αυτό μειώνει το μέγεθος του αρχείου και επιταχύνει την εξαγωγή.

### 5️⃣ Τι γίνεται αν δεν έχω άδεια;

Η λειτουργία αξιολόγησης προσθέτει μια γραμμή υδατογράφημα (`"Aspose.Cells for Java Evaluation Version"`). Για παραγωγή θα χρειαστείτε άδεια· διαφορετικά το υδατογράφημα μπορεί να διακόψει τους επεξεργαστές που ακολουθούν.

---

## Πλήρες Παράδειγμα Εργασίας (Έτοιμο για Αντιγραφή‑Επικόλληση)

```java
import com.aspose.cells.*;

import java.io.File;

public class ExportExcelToTxtDemo {
    public static void main(String[] args) throws Exception {
        // Ensure output directory exists
        new File("output").mkdirs();

        // 1️⃣ Create workbook and get first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.getWorksheets().get(0);

        // 2️⃣ Put several numbers to illustrate formatting
        sheet.getCells().get("A1").putValue(123.456789);
        sheet.getCells().get("A2").putValue(0.0012345);
        sheet.getCells().get("A3").putValue(98765.4321);

        // 3️⃣ Configure TXT options – 4 significant digits, tab delimiter
        TxtSaveOptions txtOptions = new TxtSaveOptions();
        txtOptions.setSignificantDigits(4);
        txtOptions.setSeparator('\t'); // optional, defaults to tab
        txtOptions.setCultureInfo(java.util.Locale.US); // enforce dot as decimal separator

        // 4️⃣ Save as TXT
        String outPath = "output/SignificantDigits.txt";
        workbook.save(outPath, txtOptions);

        System.out.println("Export completed: " + outPath);
    }
}
```

Η εκτέλεση του παραπάνω παράγει ένα `output/SignificantDigits.txt` με:

```
123.5
0.001235
98770
```

Παρατηρήστε πώς κάθε αριθμός σέβεται τον κανόνα των **4 σημαντικών ψηφίων**, ακόμη και οι πολύ μικρές και πολύ μεγάλες τιμές.

---

## Συμπέρασμα

Μόλις παρουσιάσαμε έναν **πλήρη, αυτόνομο τρόπο εξαγωγής Excel σε TXT** χρησιμοποιώντας Java και Aspose.Cells, καλύπτοντας **πώς να ορίσετε σημαντικά ψηφία**, **να αποθηκεύσετε το excel ως αρχείο κειμένου**, και **να αποθηκεύσετε το βιβλίο εργασίας ως txt**. Τα κύρια συμπεράσματα:

- Χρησιμοποιήστε `TxtSaveOptions.setSignificantDigits` για να ελέγξετε την αριθμητική ακρίβεια.
- Ρυθμίστε διαχωριστικά, πολιτισμό και περιοχές εξαγωγής όπως χρειάζεται.
- Ο κώδικας λειτουργεί σε οποιαδήποτε πλατφόρμα, απαιτεί μόνο μία βιβλιοθήκη και παράγει καθαρό κείμενο χωρισμένο με κενά, έτοιμο για επεξεργασία.

Έτοιμοι για το επόμενο βήμα; Δοκιμάστε να προσθέσετε πολλές στήλες, να πειραματιστείτε με διαφορετικά διαχωριστικά, ή να ενσωματώσετε την εξαγωγή σε μια μεγαλύτερη διαδικασία ETL. Αν αντιμετωπίσετε προβλήματα—ίσως θέμα τοπικής ρύθμισης ή τεράστιο φύλλο—ανατρέξτε ξανά στην ενότητα “Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις” παραπάνω.

Έχετε μια περίπτωση χρήσης που θέλετε να μοιραστείτε; Αφήστε ένα σχόλιο, ή κάντε fork το αποθετήριο και ανοίξτε ένα pull request. Καλή προγραμματιστική, και απολαύστε την απλότητα του να μετατρέπετε υπολογιστικά φύλλα σε απλό κείμενο!

## Τι Θα Μάθετε Στη Σύντομη Επόμενη

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να Αποθηκεύσετε Αρχεία Excel σε Διάφορες Μορφές Χρησιμοποιώντας Aspose.Cells Java](/cells/english/java/workbook-operations/save-excel-files-aspose-cells-java/)
- [Πώς να Φορτώσετε και Αποθηκεύσετε Excel ως CSV Χρησιμοποιώντας Aspose.Cells για Java&#58; Ένας Πλήρης Οδηγός](/cells/english/java/workbook-operations/aspose-cells-java-load-save-excel-csv/)
- [Πώς να Δημιουργήσετε και Εξάγετε Excel σε HTML Χρησιμοποιώντας Aspose.Cells Java | Οδηγός Λειτουργιών Βιβλίου Εργασίας](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}