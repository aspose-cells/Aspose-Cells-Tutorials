---
date: '2026-08-16'
description: Μάθετε πώς να προσθέσετε παγκοσμιοποίηση στη Java χρησιμοποιώντας το
  Aspose.Cells, να προσαρμόσετε τα μηνύματα σφαλμάτων του Excel και να ρυθμίσετε την
  εξάρτηση Maven.
keywords:
- how to add globalization
- custom excel error messages
- aspose.cells maven dependency
lastmod: '2026-08-16'
og_description: Μάθετε πώς να προσθέσετε παγκοσμιοποίηση στη Java χρησιμοποιώντας
  το Aspose.Cells, να προσαρμόσετε τα μηνύματα σφαλμάτων του Excel και να ρυθμίσετε
  την εξάρτηση Maven. Ακολουθήστε τον οδηγό βήμα προς βήμα.
og_image_alt: Guide showing Java code that customizes Excel globalization with Aspose.Cells
og_title: Πώς να προσθέσετε παγκοσμιοποίηση στη Java με το Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-08-16'
  description: Learn how to add globalization in Java using Aspose.Cells, customize
    Excel error messages, and set up the Maven dependency.
  headline: How to add globalization in Java with Aspose.Cells
  type: TechArticle
- questions:
  - answer: Yes. Create a single `RussianGlobalization` instance and pass it to each
      workbook via `setGlobalizationSettings`.
    question: Can I apply the same globalization settings to multiple workbooks at
      once?
  - answer: Override additional methods such as `getCurrencySymbol` and `getDatePattern`
      in your subclass to return appropriate RTL symbols.
    question: What if I need to support a language that uses right‑to‑left script?
  - answer: No. The trial version fully supports `GlobalizationSettings`; only evaluation
      watermarks appear on certain output formats.
    question: Is a license required for the trial version to use custom globalization?
  - answer: Insert `System.out.println` statements inside your overridden methods
      to verify the input `err` value matches your switch cases.
    question: How do I debug incorrect error strings?
  - answer: Negligibly. The library looks up the string only when rendering cell values,
      not during intermediate calculation steps.
    question: Does this affect formula calculation speed?
  type: FAQPage
tags:
- globalization
- Aspose.Cells
- Java internationalization
- Excel localization
title: Πώς να προσθέσετε παγκοσμιοποίηση στη Java με το Aspose.Cells
url: /el/java/calculation-engine/custom-globalization-aspose-cells-java/
weight: 1
---

{{< blocks/products/pf/main-container >}}

{{< /blocks/products/pf/tutorial-page-section >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να προσθέσετε παγκοσμιοποίηση σε Java με Aspose.Cells

## Εισαγωγή

Η προσθήκη παγκοσμιοποίησης στο Java workbook σας επιτρέπει να παρουσιάζετε μηνύματα σφάλματος, τιμές boolean και άλλες συμβολοσειρές που εξαρτώνται από την τοπική ρύθμιση στη γλώσσα που αναμένουν οι χρήστες σας. Σε αυτό το μάθημα θα μάθετε **πώς να προσθέσετε παγκοσμιοποίηση** για τη Ρωσική, αλλά το ίδιο μοτίβο λειτουργεί για οποιαδήποτε γλώσσα. Στο τέλος του οδηγού θα μπορείτε να:

- Παρακάμψετε το προεπιλεγμένο κείμενο σφάλματος και τις αναπαραστάσεις boolean.
- Εφαρμόσετε τις προσαρμοσμένες ρυθμίσεις σας σε οποιοδήποτε αντικείμενο `Workbook`.
- Ενσωματώσετε τη λύση σε ένα τυπικό Maven‑based Java project.

Έτοιμοι να κάνετε τα Excel αρχεία σας πραγματικά πολυγλωσσικά; Ας ελέγξουμε πρώτα ότι το περιβάλλον ανάπτυξής σας πληροί τις προαπαιτήσεις.

## Γρήγορες απαντήσεις
- **Τι είναι η παγκοσμιοποίηση στο Aspose.Cells;** Είναι ένα σύνολο συμβολοσειρών που εξαρτώνται από την τοπική ρύθμιση (σφάλματα, boolean κ.λπ.) που μπορείτε να αντικαταστήσετε με προσαρμοσμένο κείμενο.  
- **Ποιο Maven artifact απαιτείται;** `com.aspose:aspose-cells:25.3`.  
- **Μπορώ να στοχεύσω γλώσσες εκτός της Ρωσικής;** Ναι – επεκτείνετε το `GlobalizationSettings` και παρακάμψτε τις απαιτούμενες μεθόδους για κάθε τοπική ρύθμιση.  
- **Χρειάζομαι άδεια για ανάπτυξη;** Μια δωρεάν δοκιμή λειτουργεί για δοκιμές· μια μόνιμη άδεια αφαιρεί τα υδατογράμματα αξιολόγησης.  
- **Είναι η λύση thread‑safe;** Εφαρμόστε τις ρυθμίσεις ανά workbook· το αντικείμενο `GlobalizationSettings` είναι αμετάβλητο μετά τη δημιουργία.

## Τι είναι η παγκοσμιοποίηση στο Aspose.Cells;

`GlobalizationSettings` είναι το αντικείμενο διαμόρφωσης του Aspose.Cells που ελέγχει τις συμβολοσειρές που εξαρτώνται από την τοπική ρύθμιση, όπως μηνύματα σφάλματος, τιμές boolean, σύμβολα νομισμάτων και πρότυπα ημερομηνίας. Παρέχοντας τη δική σας υποκλάση, λέτε στη βιβλιοθήκη ποιο κείμενο να εμφανίζει για κάθε πολιτισμό, επιτρέποντας την αντικατάσταση των προεπιλεγμένων αγγλικών συμβολοσειρών με μεταφράσεις που ταιριάζουν στη γλώσσα και τις περιφερειακές συνήθειες του τελικού χρήστη.

## Γιατί να προσθέσετε προσαρμοσμένη παγκοσμιοποίηση;

Το Aspose.Cells υποστηρίζει **50+ μορφές εισόδου και εξόδου** – συμπεριλαμβανομένων των XLSX, CSV, PDF και ODS – και μπορεί να επεξεργαστεί workbooks με **έως 200 000 γραμμές** χωρίς να φορτώνει ολόκληρο το αρχείο στη μνήμη. Η προσαρμοσμένη παγκοσμιοποίηση εξασφαλίζει ότι οι τελικοί χρήστες βλέπουν τα μηνύματα στη μητρική τους γλώσσα, μειώνοντας τα αιτήματα υποστήριξης κατά εκτιμώμενο **30 %** για πολυεθνικές εγκαταστάσεις.

## Προαπαιτούμενα

- **Java Development Kit** 8 ή νεότερο.
- **IDE** όπως IntelliJ IDEA ή Eclipse.
- **Aspose.Cells for Java** έκδοση 25.3 (ή νεότερη) προστιθέμενη μέσω Maven ή Gradle.

### Ρύθμιση του Aspose.Cells για Java

Προσθέστε την εξάρτηση Maven στο `pom.xml` σας:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
    <classifier>jdk17</classifier>
</dependency>
```
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

Ή, αν προτιμάτε Gradle, εισάγετε τα παρακάτω στο `build.gradle`:

```gradle
implementation 'com.aspose:aspose-cells:25.3'
```
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### Απόκτηση άδειας

Το Aspose προσφέρει διάφορες επιλογές αδειοδότησης:

- **Δωρεάν δοκιμή** – πλήρης αξιολόγηση λειτουργιών για 30 ημέρες.  
- **Προσωρινή άδεια** – απεριόριστη αξιολόγηση χωρίς υδατογράμματα.  
- **Εμπορική άδεια** – έτοιμη για παραγωγή, με προτεραιότητα υποστήριξης.

Αφού αποκτήσετε το αρχείο άδειας, ορίστε το μία φορά κατά την εκκίνηση της εφαρμογής:

```java
com.aspose.cells.License license = new com.aspose.cells.License();
license.setLicense("Aspose.Cells.lic");
```
```java
import com.aspose.cells.*;

public class InitializeAspose {
    public static void main(String[] args) {
        // Set the license if you have one
        License license = new License();
        try {
            license.setLicense("PathToYourLicenseFile.lic");
        } catch (Exception e) {
            System.out.println("Error setting license: " + e.getMessage());
        }

        // Create a new workbook instance
        Workbook workbook = new Workbook();
    }
}
```

## Πώς να προσθέσετε παγκοσμιοποίηση για τη Ρωσική;

Ένα αντικείμενο `Workbook` αντιπροσωπεύει ένα αρχείο Excel που έχει φορτωθεί στη μνήμη, παρέχοντας πρόσβαση στα φύλλα, τα κελιά και τις ρυθμίσεις του. Φορτώστε το workbook σας, δημιουργήστε μια υποκλάση του `GlobalizationSettings` και συνδέστε την με το workbook. Η άμεση απάντηση είναι: **δημιουργήστε μια προσαρμοσμένη κλάση `GlobalizationSettings`, παρακάμψτε τις μεθόδους `getErrorValueString` και `getBooleanValueString`, έπειτα καλέστε `workbook.setGlobalizationSettings(customSettings)`**. Αυτή η διπλή προσέγγιση αντικαθιστά τις προεπιλεγμένες ρωσικές συμβολοσειρές με τις δικές σας.

### Ορισμός των προσαρμοσμένων ρυθμίσεων

Την πρώτη φορά που αναφέρετε το `GlobalizationSettings` σε αυτόν τον οδηγό, σημειώστε τον ορισμό:

`GlobalizationSettings` είναι η βασική κλάση που χρησιμοποιεί το Aspose.Cells για την ανάκτηση συμβολοσειρών που εξαρτώνται από την τοπική ρύθμιση.  

Τώρα δημιουργήστε μια υποκλάση που επιστρέφει κείμενο ειδικό για τη Ρωσική:

```java
class RussianGlobalization extends GlobalizationSettings {
    @Override
    public String getErrorValueString(String err) {
        switch (err) {
            case "#DIV/0!": return "Деление на ноль";
            case "#N/A":    return "Недоступно";
            default:        return err; // fallback to original
        }
    }

    @Override
    public String getBooleanValueString(Boolean bv) {
        return bv ? "ИСТИНА" : "ЛОЖЬ";
    }
}
```
```java
import com.aspose.cells.*;

class RussianGlobalization extends GlobalizationSettings {
    public String getErrorValueString(String err) {
        switch (err.toUpperCase()) {
            case "#NAME?":
                return "#RussianName-имя?";
        }
        return "RussianError-ошибка";
    }

    public String getBooleanValueString(Boolean bv) {
        return bv ? "RussianTrue-правда" : "RussianFalse-ложный";
    }
}
```

### Εφαρμογή των ρυθμίσεων σε ένα βιβλίο εργασίας

Αφού ορίσετε την υποκλάση, συνδέστε την με οποιοδήποτε αντικείμενο `Workbook`:

```java
Workbook wb = new Workbook("input.xlsx");
wb.setGlobalizationSettings(new RussianGlobalization());
wb.save("output.xlsx");
```
```java
import com.aspose.cells.*;
import AsposeCellsExamples.Utils; // Placeholder import

public void Run() throws Exception {
    String dataDir = "YOUR_DATA_DIRECTORY";
    String outDir = "YOUR_OUTPUT_DIRECTORY";

    Workbook wb = new Workbook(dataDir + "/sampleRussianGlobalization.xlsx");
    wb.getSettings().setGlobalizationSettings(new RussianGlobalization());
    
    wb.calculateFormula();
    wb.save(outDir + "/outputRussianGlobalization.pdf");
}
```

## Πρακτικές εφαρμογές

- **Οικονομική αναφορά** – εμφάνιση κωδικών σφάλματος στη μητρική γλώσσα του λογιστή, μειώνοντας τις παρερμηνείες.  
- **Εργαλεία σε επίπεδο επιχείρησης** – ενσωμάτωση της ίδιας λογικής παγκοσμιοποίησης σε δεκάδες εσωτερικά εργαλεία βασισμένα σε Excel.  
- **Αυτοματοποιημένες ροές δεδομένων** – διασφάλιση ότι τα downstream συστήματα λαμβάνουν τιμές με γνώση τοπικής ρύθμισης χωρίς επιπλέον βήματα μετάφρασης.

## Σκέψεις απόδοσης

Όταν ενεργοποιείτε προσαρμοσμένη παγκοσμιοποίηση, το Aspose.Cells εξακολουθεί να επεξεργάζεται τύπους και I/O με την ίδια υψηλή απόδοση. Για να διατηρήσετε τη χρήση μνήμης χαμηλή:

- Απελευθερώστε τις αναφορές στο workbook (`wb.dispose()`) μετά την αποθήκευση.  
- Χρησιμοποιήστε `CalculationOptions.setEnableIterativeCalculation(true)` μόνο όταν είναι απαραίτητο.  
- Ρυθμίστε το heap της JVM (`-Xmx2g`) για workbooks μεγαλύτερα από 100 MB.

## Συχνές ερωτήσεις

**Ε: Μπορώ να εφαρμόσω τις ίδιες ρυθμίσεις παγκοσμιοποίησης σε πολλά workbooks ταυτόχρονα;**  
Α: Ναι. Δημιουργήστε μια ενιαία παρουσία `RussianGlobalization` και περάστε την σε κάθε workbook μέσω `setGlobalizationSettings`.

**Ε: Τι γίνεται αν πρέπει να υποστηρίξω γλώσσα που χρησιμοποιεί δεξιά‑προς‑αριστερά σενάριο;**  
Α: Παρακάμψτε επιπλέον μεθόδους όπως `getCurrencySymbol` και `getDatePattern` στην υποκλάση σας για να επιστρέψετε τα κατάλληλα RTL σύμβολα.

**Ε: Απαιτείται άδεια για τη δοκιμαστική έκδοση ώστε να χρησιμοποιηθεί προσαρμοσμένη παγκοσμιοποίηση;**  
Α: Όχι. Η δοκιμαστική έκδοση υποστηρίζει πλήρως το `GlobalizationSettings`; εμφανίζονται μόνο υδατογράμματα αξιολόγησης σε ορισμένες μορφές εξόδου.

**Ε: Πώς εντοπίζω λανθασμένες συμβολοσειρές σφάλματος;**  
Α: Εισάγετε δηλώσεις `System.out.println` μέσα στις παραμετροποιημένες μεθόδους σας για να επαληθεύσετε ότι η τιμή `err` ταιριάζει με τις περιπτώσεις του `switch`.

**Ε: Επηρεάζει αυτό την ταχύτητα υπολογισμού τύπων;**  
Α: Παραβρετανικά. Η βιβλιοθήκη αναζητά τη συμβολοσειρά μόνο κατά την απόδοση τιμών κελιών, όχι κατά τα ενδιάμεσα βήματα υπολογισμού.

## Πρόσθετοι πόροι

- **Τεκμηρίωση**: Εξερευνήστε λεπτομερείς οδηγούς στο [Aspose.Cells Documentation](https://reference.aspose.com/cells/java/)  
- **Λήψη**: Πρόσβαση στις τελευταίες εκδόσεις στο [Aspose Downloads](https://releases.aspose.com/cells/java/)  
- **Αγορά**: Αγοράστε άδεια για εμπορική χρήση στο [Aspose Purchase](https://purchase.aspose.com/buy)  
- **Δωρεάν δοκιμή**: Ξεκινήστε με μια δωρεάν δοκιμή από το [Aspose Free Trial](https://releases.aspose.com/cells/java/)  
- **Προσωρινή άδεια**: Αποκτήστε προσωρινή άδεια μέσω του [Aspose Temporary License](https://purchase.aspose.com/temporary-license/)  
- **Υποστήριξη**: Λάβετε βοήθεια από την κοινότητα στο [Aspose Support Forum](https://forum.aspose.com/c/cells/9)

---

**Τελευταία ενημέρωση:** 2026-08-16  
**Δοκιμή με:** Aspose.Cells 25.3 for Java  
**Συγγραφέας:** Aspose

## Σχετικά μαθήματα

- [Aspose.Cells Java: Custom Calculation Engine Guide](/cells/java/calculation-engine/aspose-cells-java-custom-engine-guide/)
- [How to Use Aspose Cells – Excel Engine Tutorials for Java](/cells/java/calculation-engine/)
- [Aspose Cells Maven Dependency – Manage Excel Data Connections with Aspose.Cells in Java](/cells/java/advanced-features/aspose-cells-java-excel-external-data-connections/)


{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

{{< /blocks/products/pf/main-container >}}

{{< blocks/products/pf/main-wrap-class >}}