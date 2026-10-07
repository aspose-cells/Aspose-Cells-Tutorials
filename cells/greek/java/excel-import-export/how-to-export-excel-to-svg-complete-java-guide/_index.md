---
category: general
date: 2026-06-18
description: Μάθετε πώς να εξάγετε το Excel σε SVG γρήγορα και επίσης πώς να δημιουργήσετε
  SVG από το Excel χρησιμοποιώντας το Aspose.Cells για Java. Περιλαμβάνεται κώδικας
  βήμα‑βήμα.
draft: false
keywords:
- how to export excel to svg
- generate svg from excel
language: el
og_description: Πώς να εξάγετε το Excel σε SVG με το Aspose.Cells για Java. Ακολουθήστε
  αυτό το σεμινάριο για να δημιουργήσετε SVG από αρχεία Excel χωρίς κόπο.
og_title: Πώς να εξάγετε το Excel σε SVG – Πλήρης οδηγός Java
schemas:
- author: Aspose
  dateModified: '2026-06-18'
  description: Learn how to export Excel to SVG quickly and also how to generate SVG
    from Excel using Aspose.Cells for Java. Step‑by‑step code included.
  headline: How to Export Excel to SVG – Complete Java Guide
  type: TechArticle
- description: Learn how to export Excel to SVG quickly and also how to generate SVG
    from Excel using Aspose.Cells for Java. Step‑by‑step code included.
  name: How to Export Excel to SVG – Complete Java Guide
  steps:
  - name: Maven
    text: 'Add the following dependency to your `pom.xml`:'
  - name: Gradle
    text: '```groovy implementation ''com.aspose:aspose-cells:24.9:jdk17'' ```'
  - name: Expected SVG Output
    text: "Open `varSvg.svg` in any modern browser or graphics editor. You should
      see a single‑page view with the cell **A1** displaying the character `\U0001D7D8`
      (double‑struck zero). The SVG markup will contain `<text>` elements with the
      Unicode code points preserved, ensuring crisp rendering at any zoom level."
  - name: Customizing Styles
    text: 'If you want a different font or color, adjust the cell style before saving:'
  type: HowTo
- questions:
  - answer: Aspose treats each worksheet as a separate page. To combine them, export
      each sheet individually and then merge the SVG files with a tool like Inkscape
      or a simple XML concatenation script.
    question: Can I export multiple worksheets to a single SVG?
  - answer: Yes. Load the workbook with `Workbook workbook = new Workbook("protected.xlsx",
      new LoadOptions(LoadFormat.XLSX) {{ setPassword("myPwd"); }});` before saving
      to SVG.
    question: Does the library support password‑protected workbooks?
  - answer: 'For massive workbooks, consider using `SaveOptions` to limit rows/columns
      or enable streaming (`Workbook.setForceCalculation(true)`) to reduce memory
      overhead. ## Next Steps Now that you know **how to export Excel to SVG**, you
      might want to explore: - **Generating SVG from Excel** with custom theme'
    question: What about performance for huge files?
  type: FAQPage
tags:
- Aspose.Cells
- Java
- Excel automation
title: Πώς να εξάγετε το Excel σε SVG – Πλήρης οδηγός Java
url: /el/java/excel-import-export/how-to-export-excel-to-svg-complete-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Εξάγετε το Excel σε SVG – Πλήρης Οδηγός Java

Έχετε αναρωτηθεί ποτέ **πώς να εξάγετε το Excel σε SVG** χωρίς να παλεύετε με τρίτους μετατροπείς; Δεν είστε μόνοι. Πολλοί προγραμματιστές χρειάζονται μια καθαρή διανυσματική αναπαράσταση των δεδομένων του υπολογιστικού φύλλου για αναφορές, πίνακες ελέγχου ή γραφικά έτοιμα για το web. Τα καλά νέα; Με το Aspose.Cells for Java μπορείτε να **δημιουργήσετε SVG από Excel** με λίγες μόνο γραμμές κώδικα—χωρίς χειροκίνητη παρέμβαση.

Σε αυτό το tutorial θα καλύψουμε όλα όσα χρειάζεται να γνωρίζετε: από τη ρύθμιση της βιβλιοθήκης, τη δημιουργία ενός workbook, την εισαγωγή ειδικών χαρακτήρων Unicode, μέχρι την τελική αποθήκευση του αρχείου ως SVG (και XPS για σύγκριση). Στο τέλος θα έχετε ένα πλήρως λειτουργικό απόσπασμα Java που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο.

## Προαπαιτήσεις

Πριν βουτήξουμε, βεβαιωθείτε ότι έχετε:

- **Java Development Kit (JDK) 8+** – ο κώδικας εκτελείται σε οποιοδήποτε σύγχρονο JDK.
- **Aspose.Cells for Java** (έκδοση 24.9 ή νεότερη) – μπορείτε να κατεβάσετε δωρεάν δοκιμαστική έκδοση από τον ιστότοπο της Aspose ή να προσθέσετε την εξάρτηση Maven.
- Ένα **IDE** της επιλογής σας (IntelliJ IDEA, Eclipse, VS Code κ.λπ.).
- Βασική εξοικείωση με τις έννοιες της Java και του Excel.

Αν κάποιο από αυτά σας είναι άγνωστο, κάντε παύση και εγκαταστήστε τα πρώτα· το υπόλοιπο του οδηγού υποθέτει ότι είναι έτοιμα.

## Βήμα 1: Προσθέστε το Aspose.Cells στο Έργο σας

### Maven

Προσθέστε την ακόλουθη εξάρτηση στο `pom.xml` σας:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version>
    <classifier>jdk17</classifier> <!-- adjust classifier for your JDK -->
</dependency>
```

### Gradle

```groovy
implementation 'com.aspose:aspose-cells:24.9:jdk17'
```

> **Συμβουλή:** Αν χρησιμοποιείτε μη‑Maven build, κατεβάστε το JAR απευθείας και προσθέστε το στο classpath σας.

## Βήμα 2: Δημιουργήστε ένα Νέο Workbook και Πρόσβαση στο Πρώτο Worksheet

Το πρώτο που χρειάζεστε είναι ένα νέο αντικείμενο `Workbook`. Σκεφτείτε το ως ένα κενό αρχείο Excel που περιμένει δεδομένα.

```java
import com.aspose.cells.*;

public class ExcelToSvgDemo {
    public static void main(String[] args) throws Exception {
        // Step 2: Initialize a new workbook
        Workbook workbook = new Workbook();

        // Access the first worksheet (index 0)
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

Γιατί να πάρετε το πρώτο worksheet; Από προεπιλογή το Aspose δημιουργεί ένα φύλλο με όνομα *Sheet1*, το οποίο είναι τέλειο για μια γρήγορη επίδειξη. Φυσικά, μπορείτε να προσθέσετε περισσότερα φύλλα αργότερα.

## Βήμα 3: Εισάγετε μια Τιμή που Περιέχει Variation Selector (U+E0101)

Οι variation selectors σας επιτρέπουν να προσαρμόσετε τον τρόπο απόδοσης ορισμένων χαρακτήρων Unicode. Σε αυτό το παράδειγμα τοποθετούμε το μαθηματικό διπλό‑σκαλιστό μηδέν (`𝟘`) ακολουθούμενο από τον selector `U+E0101`. Αυτό δείχνει ότι η έξοδος SVG διατηρεί σύνθετες ακολουθίες Unicode.

```java
        // Step 3: Put a value with a variation selector into cell A1
        // The string consists of the double‑struck zero (U+1D7D8) and U+E0101
        String value = "\uD835\uDFD8\uE0101"; // 𝟘\uE0101
        worksheet.getCells().get("A1").putValue(value);
```

> **Τι γίνεται αν χρειάζεστε διαφορετικό χαρακτήρα;** Απλώς αντικαταστήστε την ακολουθία Unicode escape με αυτή που χρειάζεστε· το Aspose θα το διαχειριστεί αυτόματα.

## Βήμα 4: Αποθηκεύστε το Workbook σε Μορφή XPS (Προαιρετική Σύγκριση)

Η αποθήκευση σε XPS δεν απαιτείται για τη δημιουργία SVG, αλλά είναι χρήσιμη για να δείτε πώς φαίνεται το ίδιο workbook σε άλλη διανυσματική μορφή.

```java
        // Step 4: Save as XPS (optional)
        workbook.save("output/varXps.xps", SaveFormat.XPS);
```

Θα παρατηρήσετε ότι το αρχείο XPS αντικατοπτρίζει το περιεχόμενο των κελιών, συμπεριλαμβανομένου του variation selector.

## Βήμα 5: Αποθηκεύστε το Workbook ως SVG

Τώρα το κύριο γεγονός—η εξαγωγή σε SVG.

```java
        // Step 5: Save as SVG
        workbook.save("output/varSvg.svg", SaveFormat.SVG);
    }
}
```

Αυτό είναι! Η εκτέλεση του προγράμματος παράγει δύο αρχεία:

- `output/varXps.xps` – ένα σελιδοποιημένο έγγραφο XPS.
- `output/varSvg.svg` – ένα διανυσματικό γραφικό SVG που αντιπροσωπεύει το worksheet.

### Αναμενόμενη Έξοδος SVG

Ανοίξτε το `varSvg.svg` σε οποιονδήποτε σύγχρονο περιηγητή ή πρόγραμμα επεξεργασίας γραφικών. Θα πρέπει να δείτε μια προβολή μίας σελίδας με το κελί **A1** να εμφανίζει τον χαρακτήρα `𝟘` (διπλό‑σκαλιστό μηδέν). Το markup του SVG θα περιέχει στοιχεία `<text>` με τα σημεία κώδικα Unicode διατηρημένα, εξασφαλίζοντας καθαρή απόδοση σε οποιοδήποτε επίπεδο ζουμ.

## Κατανόηση της Δομής του SVG

Αν ρίξετε μια ματιά μέσα στο παραγόμενο SVG, θα βρείτε κάτι σαν:

```xml
<svg xmlns="http://www.w3.org/2000/svg" ...>
  <text x="10" y="20" font-family="Arial" font-size="12">𝟘&#xE0101;</text>
</svg>
```

- **`<text>`** περιέχει το περιεχόμενο του κελιού.
- **`x`/`y`** συντεταγμένες τοποθετούν το κείμενο σε σχέση με τη σελίδα.
- **`font-family`** προεπιλογή είναι Arial αλλά μπορεί να προσαρμοστεί μέσω των ρυθμίσεων στυλ του `Workbook` ή του `Worksheet`.

### Προσαρμογή Στυλ

Αν θέλετε διαφορετική γραμματοσειρά ή χρώμα, προσαρμόστε το στυλ του κελιού πριν την αποθήκευση:

```java
Style style = worksheet.getCells().get("A1").getStyle();
style.getFont().setColor(Color.getBlue());
style.getFont().setSize(14);
worksheet.getCells().get("A1").setStyle(style);
```

Τώρα το SVG θα αντικατοπτρίζει το μπλε, μεγαλύτερο κείμενο.

## Περιπτώσεις Άκρων & Συνηθισμένα Πιθανά Σφάλματα

| Κατάσταση | Τι να Προσέξετε | Διόρθωση |
|-----------|-------------------|-----|
| **Μεγάλα worksheets** (χιλιάδες γραμμές) | Τα αρχεία SVG μπορούν να γίνουν τεράστια επειδή κάθε κελί γίνεται στοιχείο `<text>`. | Χρησιμοποιήστε το `SaveOptions` για να περιορίσετε την περιοχή εξαγωγής: `options.setPageSetup().setPrintArea("A1:D50");` |
| **Συγχωνευμένα κελιά** | Οι συγχωνευμένες περιοχές μπορεί να αποδοθούν ως ξεχωριστά μπλοκ κειμένου. | Βεβαιωθείτε ότι η συγχώνευση έχει γίνει πριν την αποθήκευση, ή προσαρμόστε το στυλ χειροκίνητα μετά την εξαγωγή. |
| **Τύποι** | Οι τύποι αξιολογούνται και μόνο η προκύπτουσα τιμή εμφανίζεται στο SVG. | Αν χρειάζεστε τον ίδιο τον τύπο, γράψτε τον ως συμβολοσειρά πριν την εξαγωγή. |
| **Ειδικές γραμματοσειρές** (π.χ., Symbol) | Δεν ενσωματώνονται σωστά όλες οι γραμματοσειρές στο SVG. | Ενσωματώστε τη γραμματοσειρά ή μεταβείτε σε μια εναλλακτική web‑safe. |

## Πλήρες Παράδειγμα Εργασίας

Παρακάτω είναι το **πλήρες, αυτόνομο** πρόγραμμα Java που μπορείτε να αντιγράψετε‑επικολλήσετε σε ένα αρχείο με όνομα `ExcelToSvgDemo.java`. Περιλαμβάνει εισαγωγές, διαχείριση σφαλμάτων και σχόλια για σαφήνεια.

```java
import com.aspose.cells.*;
import java.awt.Color;

/**
 * Demonstrates how to export Excel to SVG using Aspose.Cells for Java.
 * This example also shows how to generate SVG from Excel with a variation selector.
 */
public class ExcelToSvgDemo {
    public static void main(String[] args) {
        try {
            // Initialize a new workbook (Step 1)
            Workbook workbook = new Workbook();

            // Access the first worksheet (Step 2)
            Worksheet worksheet = workbook.getWorksheets().get(0);

            // Insert a value with a variation selector into cell A1 (Step 3)
            // 𝟘 (U+1D7D8) + Variation Selector-17 (U+E0101)
            String value = "\uD835\uDFD8\uE0101";
            worksheet.getCells().get("A1").putValue(value);

            // Optional: style the cell to make the output clearer
            Style style = worksheet.getCells().get("A1").getStyle();
            style.getFont().setSize(16);
            style.getFont().setColor(Color.BLUE);
            worksheet.getCells().get("A1").setStyle(style);

            // Save as XPS for comparison (Step 4)
            workbook.save("output/varXps.xps", SaveFormat.XPS);

            // Save as SVG – this is the core answer to how to export excel to svg (Step 5)
            workbook.save("output/varSvg.svg", SaveFormat.SVG);

            System.out.println("Export completed. Check the 'output' folder for varSvg.svg and varXps.xps.");
        } catch (Exception e) {
            System.err.println("An error occurred during export: " + e.getMessage());
            e.printStackTrace();
        }
    }
}
```

Εκτελέστε το πρόγραμμα (`java ExcelToSvgDemo`) και εξετάστε το φάκελο `output`. Τώρα έχετε μια διανυσματική αναπαράσταση των δεδομένων του Excel, έτοιμη να ενσωματωθεί σε ιστοσελίδες, αναφορές ή παρουσιάσεις.

## Συχνές Ερωτήσεις

**Ε: Μπορώ να εξάγω πολλαπλά worksheets σε ένα μόνο SVG;**  
Α: Το Aspose θεωρεί κάθε worksheet ως ξεχωριστή σελίδα. Για να τα συνδυάσετε, εξάγετε κάθε φύλλο ξεχωριστά και στη συνέχεια συγχωνεύστε τα αρχεία SVG με ένα εργαλείο όπως το Inkscape ή ένα απλό script συγχώνευσης XML.

**Ε: Υποστηρίζει η βιβλιοθήκη βιβλία εργασίας με κωδικό πρόσβασης;**  
Α: Ναι. Φορτώστε το βιβλίο εργασίας με `Workbook workbook = new Workbook("protected.xlsx", new LoadOptions(LoadFormat.XLSX) {{ setPassword("myPwd"); }});` πριν την αποθήκευση σε SVG.

**Ε: Πώς είναι η απόδοση για τεράστια αρχεία;**  
Α: Για τεράστια βιβλία εργασίας, σκεφτείτε τη χρήση του `SaveOptions` για περιορισμό γραμμών/στηλών ή ενεργοποιήστε τη ροή (`Workbook.setForceCalculation(true)`) για μείωση της μνήμης.

## Επόμενα Βήματα

Τώρα που ξέρετε **πώς να εξάγετε το Excel σε SVG**, ίσως θέλετε να εξερευνήσετε:

- **Δημιουργία SVG από Excel** με προσαρμοσμένα θέματα (χρησιμοποιήστε `Workbook.getWorksheets().get(i).getPageSetup().setPrintArea(...)`).
- Μετατροπή του SVG σε **PDF** για εκτυπώσιμες αναφορές (`SaveFormat.PDF`).
- Ενσωμάτωση του SVG απευθείας σε πίνακες ελέγχου **HTML** για διαδραστικές απεικονίσεις δεδομένων.
- Αυτοματοποίηση μαζικών μετατροπών για ολόκληρο φάκελο αρχείων Excel.

Κάθε ένα από αυτά τα θέματα βασίζεται στις ίδιες βασικές έννοιες που καλύψαμε, οπότε είστε καλά προετοιμασμένοι να προχωρήσετε πιο βαθιά.

*Καλό προγραμματισμό! Αν αντιμετωπίσετε δυσκολίες, αφήστε ένα σχόλιο παρακάτω ή ελέγξτε την τεκμηρίωση του Aspose.Cells για πιο προχωρημένα σενάρια.*

## Τι Θα Πρέπει Να Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [How to Export Excel Charts as SVG Using Aspose.Cells Java for Scalable Vector Graphics](/cells/english/java/charts-graphs/export-excel-charts-svg-aspose-cells-java/)
- [How to Convert Excel Charts to SVG Using Aspose.Cells in Java](/cells/english/java/charts-graphs/convert-excel-charts-svg-aspose-cells-java/)
- [How to Create and Save an Excel Workbook as SVG using Aspose.Cells for Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}