---
category: general
date: 2026-06-08
description: Μάθετε πώς να μετατρέπετε XLSX σε PPTX και να διατηρείτε τα σχήματα επεξεργάσιμα
  χρησιμοποιώντας το Aspose. Ο βήμα‑βήμα κώδικας Java δείχνει πώς να εξάγετε τα σχήματα
  χωρίς να χάσετε την επεξεργασιμότητά τους.
draft: false
keywords:
- convert xlsx to pptx
- how to export shapes
- how to keep shapes
- aspose export pptx
language: el
og_description: Μετατρέψτε XLSX σε PPTX διατηρώντας την επεξεργασιμότητα των σχημάτων.
  Αυτός ο οδηγός σας καθοδηγεί μέσω του κώδικα Java και εξηγεί πώς να διατηρήσετε
  τα σχήματα χρησιμοποιώντας το Aspose.
og_title: Μετατροπή XLSX σε PPTX – Εξαγωγή επεξεργάσιμων σχημάτων με το Aspose
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Learn how to convert XLSX to PPTX and keep shapes editable using Aspose.
    Step‑by‑step Java code shows how to export shapes without losing editability.
  headline: Convert XLSX to PPTX – Complete Guide to Export Editable Shapes
  type: TechArticle
- description: Learn how to convert XLSX to PPTX and keep shapes editable using Aspose.
    Step‑by‑step Java code shows how to export shapes without losing editability.
  name: Convert XLSX to PPTX – Complete Guide to Export Editable Shapes
  steps:
  - name: Expected Output
    text: '- A PowerPoint file named `editable.pptx` located in the directory you
      specified. - Each worksheet appears as a separate slide. - All shapes (text
      boxes, arrows, charts) remain fully editable, just as they were in Excel.'
  - name: 1. Shapes Turn Into Images
    text: '> **Symptom:** After conversion, clicking a shape shows no resize handles.'
  - name: 2. Missing Slides for Some Worksheets
    text: '> **Symptom:** Only the first sheet appears in the PPTX.'
  - name: 3. File Not Found Exceptions
    text: '> **Symptom:** Java throws `FileNotFoundException` for the source Excel.'
  - name: Wrap‑Up
    text: We’ve walked through the entire process of **convert xlsx to pptx**, showing
      exactly **how to export shapes** and **how to keep shapes** editable using the
      Aspose API. The complete Java program is ready to drop into any Maven project,
      and the optional tweaks let you tailor the conversion to your exa
  type: HowTo
- questions:
  - answer: Yes, you could use OpenXML SDK, but you’d lose the high‑level shape preservation
      that Aspose handles automatically.
    question: Can I convert XLSX to PPTX without Aspose?
  - answer: The conversion strips out VBA; only visual elements are transferred. If
      you need macro logic in PowerPoint, you’ll have to recreate it manually.
    question: Does this work with macros or VBA code inside the workbook?
  - answer: Aspose processes them efficiently, but memory usage can spike. Consider
      converting sheet‑by‑sheet or increasing the JVM heap (`-Xmx2g`).
    question: What about large workbooks with hundreds of shapes?
  type: FAQPage
tags:
- Aspose.Cells
- Aspose.Slides
- Java
- File Conversion
title: Μετατροπή XLSX σε PPTX – Πλήρης Οδηγός για την Εξαγωγή Επεξεργάσιμων Σχημάτων
url: /el/java/excel-import-export/convert-xlsx-to-pptx-complete-guide-to-export-editable-shape/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Μετατροπή XLSX σε PPTX – Πλήρης Οδηγός για Εξαγωγή Επεξεργάσιμων Σχημάτων

Έχετε αναρωτηθεί ποτέ πώς να **convert XLSX to PPTX** χωρίς να μετατρέπετε τα όμορφα διαγράμματα και τις εικόνες σας σε επίπεδες εικόνες; Δεν είστε μόνοι. Πολλοί προγραμματιστές συναντούν πρόβλημα όταν χρειάζονται μια παρουσίαση PowerPoint που εξακολουθεί να επιτρέπει στον παραλήπτη να τροποποιήσει σχήματα, να αλλάξει το μέγεθος των πλαισίων κειμένου ή να προσαρμόσει συνδέσμους. Τα καλά νέα; Η Aspose το κάνει αυτό χωρίς κόπο, και σε αυτό το tutorial θα σας δείξουμε ακριβώς **how to export shapes** και **how to keep shapes** επεξεργάσιμα κατά τη μετατροπή.

Θα περάσουμε από ένα πραγματικό παράδειγμα Java που φορτώνει ένα βιβλίο εργασίας Excel, ενεργοποιεί τη σωστή επιλογή και γράφει ένα αρχείο PPTX που μπορείτε να ανοίξετε στο PowerPoint και να επεξεργαστείτε αμέσως. Στο τέλος θα γνωρίζετε όχι μόνο *what* να καλέσετε, αλλά και *why* κάθε ρύθμιση είναι σημαντική, καθώς και μια σειρά συμβουλών για να αποφύγετε τα συνηθισμένα προβλήματα.

## Προαπαιτούμενα – Τι Χρειάζεστε Πριν Ξεκινήσετε

- **Java Development Kit (JDK) 8 ή νεότερο** – ο κώδικας μεταγλωττίζεται με οποιοδήποτε πρόσφατο JDK.
- **Aspose.Cells for Java** και **Aspose.Slides for Java** JARs – μπορείτε να τα αποκτήσετε από το αποθετήριο Maven της Aspose ή να κατεβάσετε την τελευταία έκδοση από τον ιστότοπο της Aspose.
- Ένα **αρχείο Excel (`shapes.xlsx`)** που περιέχει τα σχήματα που θέλετε να διατηρήσετε. Ένα απλό βιβλίο εργασίας με μερικά σχεδιασμένα αντικείμενα αρκεί για δοκιμές.
- Το αγαπημένο σας IDE (IntelliJ IDEA, Eclipse, VS Code…) ή απλώς έναν απλό επεξεργαστή κειμένου και ένα τερματικό.

Αν κάποιο από αυτά σας φαίνεται άγνωστο, μην πανικοβληθείτε. Η εγκατάσταση των JAR είναι τόσο εύκολη όσο η προσθήκη δύο εξαρτήσεων στο `pom.xml` σας:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- check for the latest -->
</dependency>
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-slides</artifactId>
    <version>23.12</version>
</dependency>
```

Τώρα που καλύψαμε τα βασικά, ας βάλουμε τα χέρια μας στη δουλειά.

## Βήμα 1: Φόρτωση του Βιβλίου Εργασίας Excel που Περιέχει τα Σχήματα

Το πρώτο πράγμα που πρέπει να κάνετε είναι να διαβάσετε το αρχείο `.xlsx` που περιέχει τα διανυσματικά αντικείμενα. Η Aspose.Cells αφαιρεί τις λεπτομέρειες χαμηλού επιπέδου του OpenXML, έτσι απλώς δημιουργείτε ένα αντικείμενο `Workbook`.

```java
import com.aspose.cells.*;

public class ExportEditableShapes {
    public static void main(String[] args) throws Exception {
        // Load the source workbook – replace the path with your actual file location
        Workbook workbook = new Workbook("YOUR_DIRECTORY/shapes.xlsx");
        // From here on we can manipulate the workbook or pass it straight to Slides
```

> **Why this matters:** Η σωστή φόρτωση του βιβλίου εργασίας εξασφαλίζει ότι τυχόν ενσωματωμένα αντικείμενα σχεδίασης (διαγράμματα, SmartArt, ελεύθερα σχήματα) διατηρούνται στη μνήμη ως εγγενή αντικείμενα Aspose. Εάν παραλείψετε αυτό το βήμα ή χρησιμοποιήσετε γενικό ρεύμα αρχείου, η μηχανή μετατροπής μπορεί να αντιμετωπίσει το φύλλο ως στατική εικόνα, χάνοντας την επεξεργασιμότητα.

## Βήμα 2: Ενημέρωση της Aspose για Διατήρηση των Σχημάτων Επεξεργάσιμων

Η Aspose.Slides προσφέρει μια σημαία που ονομάζεται `setSaveEditableShape`. Όταν οριστεί σε `true`, η βιβλιοθήκη διατηρεί τα αρχικά δεδομένα του σχήματος αντί να τα μετατρέπει σε raster. Αυτό είναι το μέρος **how to keep shapes** του tutorial μας.

```java
        // Create save options for PPTX output
        ImageOrPrintOptions pptxSaveOptions = new ImageOrPrintOptions();

        // Enable editable shape preservation – this is the key switch
        pptxSaveOptions.setSaveEditableShape(true);
```

> **Pro tip:** Η προεπιλεγμένη τιμή για `SaveEditableShape` είναι `false`. Η παράλειψη της ενεργοποίησής του είναι ο πιο κοινός λόγος που οι προγραμματιστές καταλήγουν με ένα PPTX γεμάτο επίπεδες εικόνες. Ελέγξτε ξανά αυτή τη γραμμή αν το αποτέλεσμα φαίνεται “κολλημένο”.

## Βήμα 3: Μετατροπή και Αποθήκευση του Βιβλίου Εργασίας ως PPTX

Τώρα καλούμε τη μέθοδο `save`, περνώντας το enum `SaveFormat.PPTX` και τις προσαρμοσμένες επιλογές μας. Αυτό είναι η ουσία του **convert xlsx to pptx**.

```java
        // Save the workbook as a PPTX file with editable shapes preserved
        workbook.save("YOUR_DIRECTORY/editable.pptx", SaveFormat.PPTX, pptxSaveOptions);
    }
}
```

Όταν εκτελέσετε το πρόγραμμα, η Aspose διαβάζει το φύλλο Excel, μετατρέπει κάθε φύλλο εργασίας σε διαφάνεια και γράφει το αρχείο στο `editable.pptx`. Ανοίξτε αυτό το αρχείο στο PowerPoint και θα δείτε τα αρχικά σχήματα άθικτα—έτοιμα να μετακινηθούν, να αλλάξουν χρώμα ή μέγεθος.

### Αναμενόμενο Αποτέλεσμα

- Ένα αρχείο PowerPoint με όνομα `editable.pptx` τοποθετημένο στον φάκελο που καθορίσατε.
- Κάθε φύλλο εργασίας εμφανίζεται ως ξεχωριστή διαφάνεια.
- Όλα τα σχήματα (πλαίσια κειμένου, βέλη, διαγράμματα) παραμένουν πλήρως επεξεργάσιμα, όπως ήταν στο Excel.

Αν ανοίξετε το PPTX και προσπαθήσετε να επεξεργαστείτε ένα σχήμα, θα πρέπει να δείτε τις ίδιες λαβές που λαμβάνετε όταν δημιουργείτε ένα σχήμα από την αρχή στο PowerPoint.

## Συνηθισμένα Προβλήματα και Πώς να τα Αποφύγετε

### 1. Τα Σχήματα Μετατρέπονται σε Εικόνες

> **Symptom:** Μετά τη μετατροπή, κάνοντας κλικ σε ένα σχήμα δεν εμφανίζονται λαβές αλλαγής μεγέθους.

**Cause:** `setSaveEditableShape(false)` (η προεπιλογή) ή χρήση παλαιότερης έκδοσης Aspose που δεν υποστηρίζει τη σημαία.

**Fix:** Βεβαιωθείτε ότι καλείτε `pptxSaveOptions.setSaveEditableShape(true);` *πριν* την κλήση `save`, και ελέγξτε ότι χρησιμοποιείτε Aspose.Cells/Slides 23.x ή νεότερη έκδοση.

### 2. Λείπουν Διαφάνειες για Κάποια Φύλλα Εργασίας

> **Symptom:** Μόνο το πρώτο φύλλο εμφανίζεται στο PPTX.

**Cause:** Το βιβλίο εργασίας αποθηκεύτηκε με κρυφά φύλλα, ή οι `SaveOptions` ρυθμίστηκαν λανθασμένα.

**Fix:** Χρησιμοποιήστε `workbook.getWorksheets().setVisible(true);` για να βεβαιωθείτε ότι όλα τα φύλλα είναι ορατά, ή προσαρμόστε τις `LoadOptions` αν φορτώνετε αρχείο με προστασία κωδικού.

### 3. Εξαιρέσεις File Not Found

> **Symptom:** Η Java ρίχνει `FileNotFoundException` για το πηγαίο αρχείο Excel.

**Cause:** Λανθασμένη διαδρομή ή έλλειψη δικαιωμάτων αρχείου.

**Fix:** Χρησιμοποιήστε απόλυτη διαδρομή ή τοποθετήστε το αρχείο στον φάκελο `resources` του έργου και φορτώστε το μέσω `getClass().getResourceAsStream("/shapes.xlsx")`.

## Προχωρημένο: Μετατροπή Μόνο Συγκεκριμένων Φύλλων

Μερικές φορές δεν χρειάζεστε ολόκληρο το βιβλίο εργασίας—ίσως μόνο το φύλλο “Dashboard” πρέπει να γίνει διαφάνεια. Εδώ είναι μια γρήγορη τροποποίηση:

```java
        // Create a new workbook that contains only the desired sheet
        Workbook source = new Workbook("YOUR_DIRECTORY/shapes.xlsx");
        int sheetIndex = source.getWorksheets().get("Dashboard").getIndex();

        // Clone the target sheet into a fresh workbook
        Workbook singleSheet = new Workbook();
        singleSheet.getWorksheets().addCopy(source.getWorksheets().get(sheetIndex));

        // Save the single‑sheet workbook as PPTX
        singleSheet.save("YOUR_DIRECTORY/dashboard.pptx", SaveFormat.PPTX, pptxSaveOptions);
```

Αυτό το απόσπασμα δείχνει **how to export shapes** από ένα μόνο φύλλο εργασίας ενώ διατηρεί την επεξεργασιμότητα.

## Ανακεφαλαίωση Βήμα‑βήμα (Γρήγορη Αναφορά)

| Βήμα | Δράση | Key API |
|------|--------|----------|
| 1 | Load `.xlsx` | `new Workbook(path)` |
| 2 | Enable editable shapes | `pptxSaveOptions.setSaveEditableShape(true)` |
| 3 | Save as PPTX | `workbook.save(pptPath, SaveFormat.PPTX, pptxSaveOptions)` |

Η διατήρηση αυτού του πίνακα κοντά σας μπορεί να σας εξοικονομήσει μερικά κλικ όταν ξαναδείτε τον κώδικα αργότερα.

## Δοκιμή του Αποτελέσματος

Αφού εκτελέσετε το πρόγραμμα, ανοίξτε το `editable.pptx` στο PowerPoint και:

1. Κάντε κλικ σε οποιοδήποτε σχήμα – θα πρέπει να δείτε το συνηθισμένο πλαίσιο περιγράμματος.
2. Προσπαθήστε να αλλάξετε το χρώμα γεμίσματος – θα πρέπει να ενημερωθεί άμεσα.
3. Μετακινήστε το σχήμα σε νέα θέση – το PowerPoint θα πρέπει να διατηρήσει τις νέες συντεταγμένες.

Αν όλες οι τρεις ενέργειες λειτουργούν, έχετε επιτυχώς **convert xlsx to pptx** διατηρώντας τα σχήματα επεξεργάσιμα. Αν κάτι φαίνεται λανθασμένο, ελέγξτε ξανά τη σημαία `setSaveEditableShape` και επαληθεύστε την έκδοση της Aspose.

## Συχνές Ερωτήσεις

- **Can I convert XLSX to PPTX without Aspose?**  
  Ναι, θα μπορούσατε να χρησιμοποιήσετε το OpenXML SDK, αλλά θα χάνατε τη υψηλού επιπέδου διατήρηση σχημάτων που η Aspose διαχειρίζεται αυτόματα.

- **Does this work with macros or VBA code inside the workbook?**  
  Η μετατροπή αφαιρεί το VBA· μόνο τα οπτικά στοιχεία μεταφέρονται. Αν χρειάζεστε λογική μακροεντολών στο PowerPoint, θα πρέπει να την αναδημιουργήσετε χειροκίνητα.

- **What about large workbooks with hundreds of shapes?**  
  Η Aspose τα επεξεργάζεται αποδοτικά, αλλά η χρήση μνήμης μπορεί να αυξηθεί. Σκεφτείτε τη μετατροπή φύλλο‑με‑φύλλο ή αυξήστε το heap της JVM (`-Xmx2g`).

## Επόμενα Βήματα – Αναπτύξτε περαιτέρω τις Δεξιότητές σας στη Μετατροπή

Τώρα που έχετε κατακτήσει τα βασικά του **convert xlsx to pptx** με επεξεργάσιμα αντικείμενα, μπορείτε να εξερευνήσετε:

- **Embedding videos or audio** χρησιμοποιώντας τα media APIs της Aspose.Slides.
- **Applying slide themes** προγραμματιστικά για να δώσετε στην παρουσίαση μια ενιαία εμφάνιση.
- **Batch converting multiple workbooks** με έναν απλό βρόχο—ιδανικό για αυτοματοποιημένες ροές αναφορών.
- **Exporting to other formats** όπως PDF ή HTML ενώ διατηρείτε τα δεδομένα σχήματος (`SaveFormat.PDF` με παρόμοιες επιλογές).

Κάθε ένα από αυτά τα θέματα βασίζεται στις ίδιες βασικές έννοιες που καλύψαμε, έτσι η καμπύλη εκμάθησης είναι ήπια.

---

![μετατροπή xlsx σε pptx διάγραμμα](image.png "Διάγραμμα που δείχνει Excel φύλλο → μετατροπή Aspose → Επεξεργάσιμο PPTX")

*Image alt text: “διαγράμματα ροής μετατροπής xlsx σε pptx”*

### Συμπέρασμα

Διασχίσαμε όλη τη διαδικασία του **convert xlsx to pptx**, δείχνοντας ακριβώς **how to export shapes** και **how to keep shapes** επεξεργάσιμα χρησιμοποιώντας το API της Aspose. Το πλήρες πρόγραμμα Java είναι έτοιμο να ενσωματωθεί σε οποιοδήποτε έργο Maven, και οι προαιρετικές προσαρμογές σας επιτρέπουν να προσαρμόσετε τη μετατροπή στις ακριβείς ανάγκες σας. Δοκιμάστε το, πειραματιστείτε με διαφορετικά φύλλα, και αφήστε τη δύναμη της Aspose να αναλάβει το δύσκολο κομμάτι.

Αν αντιμετωπίσετε προβλήματα, ελέγξτε την τεκμηρίωση της Aspose για τις πιο πρόσφατες ιδιότητες `ImageOrPrintOptions`, ή αφήστε ένα σχόλιο παρακάτω. Καλή προγραμματιστική δουλειά, και απολαύστε την ελευθερία των επεξεργάσιμων παρουσιάσεων PowerPoint που δημιουργούνται απευθείας από το Excel!

## Τι Θα Πρέπει Να Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να Μετατρέψετε το Excel σε PDF σε Java Χρησιμοποιώντας το Aspose.Cells: Ένας Οδηγός Βήμα‑Βήμα](/cells/english/java/workbook-operations/convert-excel-to-pdf-aspose-cells-java/)
- [Μετατροπή SmartArt σε Ομαδικά Σχήματα σε Java χρησιμοποιώντας το Aspose.Cells: Ένας Εκτενής Οδηγός](/cells/english/java/images-shapes/convert-smartart-group-shapes-java/)
- [Πώς να Προσθέσετε και να Στυλιζάσετε Σχήματα στο Excel Χρησιμοποιώντας το Aspose.Cells Java](/cells/english/java/images-shapes/aspose-cells-java-add-styling-shapes-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}