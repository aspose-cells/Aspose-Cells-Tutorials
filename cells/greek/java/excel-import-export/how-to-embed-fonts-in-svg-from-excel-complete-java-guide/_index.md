---
category: general
date: 2026-06-27
description: Πώς να ενσωματώσετε γραμματοσειρές σε SVG από το Excel χρησιμοποιώντας
  το Aspose.Cells. Μάθετε να εξάγετε το Excel σε SVG, να μετατρέψετε xlsx σε SVG και
  να ενσωματώσετε γραμματοσειρές σε SVG αποδοτικά.
draft: false
keywords:
- how to embed fonts
- export excel to svg
- convert excel to vector
- embed fonts in svg
- convert xlsx to svg
language: el
og_description: Πώς να ενσωματώσετε γραμματοσειρές σε SVG από το Excel χρησιμοποιώντας
  το Aspose.Cells. Οδηγός βήμα-βήμα για εξαγωγή του Excel σε SVG, ενσωμάτωση γραμματοσειρών
  και μετατροπή xlsx σε SVG.
og_title: Πώς να ενσωματώσετε γραμματοσειρές σε SVG από το Excel – Εγχειρίδιο Java
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: How to embed fonts in SVG from Excel using Aspose.Cells. Learn to export
    Excel to SVG, convert xlsx to SVG, and embed fonts in SVG efficiently.
  headline: How to Embed Fonts in SVG from Excel – Complete Java Guide
  type: TechArticle
- description: How to embed fonts in SVG from Excel using Aspose.Cells. Learn to export
    Excel to SVG, convert xlsx to SVG, and embed fonts in SVG efficiently.
  name: How to Embed Fonts in SVG from Excel – Complete Java Guide
  steps:
  - name: Why This Matters
    text: Think of the SVG as a web page. If you link to an external stylesheet that
      references a font not present on the visitor’s device, the browser falls back
      to Arial or Times New Roman. By embedding, we ship the exact glyph outlines,
      just like a PDF does. This is why **embed fonts in svg** is a non‑nego
  - name: 1. Missing Custom Fonts on the Server
    text: If the source Excel references a font that isn’t installed on the machine
      running the conversion, Aspose.Cells will fall back to a default font **before**
      embedding. To avoid this, install the required fonts on the server or copy the
      `.ttf`/`.otf` files into a known directory and add them to the Jav
  - name: 2. Very Large Fonts Blow Up SVG Size
    text: Embedding a full TrueType collection can balloon the SVG to several megabytes.
      If size is a concern, consider subsetting the font to only the glyphs used in
      the sheet. Aspose.Cells doesn’t expose subsetting directly, but you can post‑process
      the SVG with tools like **fonttools** to trim unused glyph
  - name: 3. Color Profiles and Transparency
    text: SVG handles transparency natively, but some older Excel themes use indexed
      colors that may render differently. Test with a few sample sheets to ensure
      colors stay true. Adjust the `options.setTransparent(true)` flag if you need
      a transparent background.
  - name: 4. Converting Excel to Vector Formats Other Than SVG
    text: Because we’ve already set up the `ImageOrPrintOptions`, swapping `SaveFormat.SVG`
      for `SaveFormat.PDF` or `SaveFormat.EMF` is trivial. This satisfies the **convert
      excel to vector** requirement without rewriting any logic.
  type: HowTo
tags:
- Aspose.Cells
- Java
- SVG
- Excel
- Font Embedding
title: Πώς να ενσωματώσετε γραμματοσειρές σε SVG από το Excel – Πλήρης οδηγός Java
url: /el/java/excel-import-export/how-to-embed-fonts-in-svg-from-excel-complete-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να ενσωματώσετε γραμματοσειρές σε SVG από το Excel – Πλήρης Οδηγός Java

Το πώς να ενσωματώσετε γραμματοσειρές σε SVG από ένα βιβλίο εργασίας Excel είναι συχνή ερώτηση μεταξύ των προγραμματιστών που χρειάζονται καθαρά, κλιμακώσιμα γραφικά για το web. Είτε μετατρέπετε έναν πίνακα ελέγχου πωλήσεων σε εικονογράφηση διανύσματος είτε απλώς θέλετε τα διαγράμματα που προέρχονται από το Excel να φαίνονται ακριβώς το ίδιο σε έναν περιηγητή, η σωστή διαχείριση των γραμματοσειρών είναι κρίσιμη. Σε αυτό το tutorial θα περάσουμε από **export Excel to SVG** διασφαλίζοντας ότι κάθε γλύφη παραμένει ενσωματωμένη, ώστε το τελικό αρχείο να είναι πραγματικά αυτόνομο.

Θα χρησιμοποιήσουμε το Aspose.Cells for Java—μια βιβλιοθήκη δοκιμασμένη σε πεδία μάχης που αναλαμβάνει το βάρος της ανάγνωσης αρχείων XLSX, της μετατροπής τους σε διανυσματικές μορφές και του ελέγχου των σημάνσεων ενσωμάτωσης γραμματοσειρών. Στο τέλος του οδηγού θα μπορείτε να **convert xlsx to SVG**, **embed fonts in SVG**, και ακόμη να επαναχρησιμοποιήσετε τον ίδιο κώδικα για **convert Excel to vector** σε άλλες μορφές όπως PDF ή EMF αν το επιθυμείτε. Χωρίς εξωτερικά εργαλεία, μόνο με λίγες γραμμές Java.

## Τι θα χρειαστείτε

- **Java Development Kit (JDK) 8 ή νεότερο** – ο κώδικας εκτελείται σε οποιοδήποτε σύγχρονο JVM.
- **Aspose.Cells for Java** (η τελευταία έκδοση μέχρι τον Ιούνιο 2026). Μπορείτε να το αποκτήσετε από το Maven Central ή να κατεβάσετε το JAR από την ιστοσελίδα της Aspose.
- Ένα αρχείο **input.xlsx** που χρησιμοποιεί προσαρμοσμένες γραμματοσειρές (π.χ., “Calibri”, “Roboto”) που θέλετε να διατηρήσετε.
- Ένα ήπιο IDE (IntelliJ IDEA, Eclipse ή VS Code) – οτιδήποτε που σας επιτρέπει να μεταγλωττίσετε και να εκτελέσετε ένα πρόγραμμα Java.

Αυτό είναι όλο. Χωρίς πρόσθετους μετατροπείς, χωρίς χειρισμούς γραμμής εντολών. Ας βουτήξουμε.

![how to embed fonts in SVG from Excel](image.png){alt="πώς να ενσωματώσετε γραμματοσειρές σε SVG από το Excel"}

## Βήμα 1: Ρύθμιση του έργου σας και προσθήκη του Aspose.Cells

Πρώτα, δημιουργήστε ένα νέο έργο Maven (ή Gradle). Προσθέστε την εξάρτηση Aspose.Cells στο `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.8</version> <!-- check for the latest version -->
</dependency>
```

Αν προτιμάτε μια απλή ρύθμιση JAR, απλώς τοποθετήστε το `aspose-cells-24.8.jar` στο classpath σας. **Συμβουλή:** το Aspose παρέχει μια δοκιμαστική άδεια που εκτυπώνει υδατογράφημα· αντικαταστήστε την με ένα έγκυρο αρχείο άδειας για καθαρό SVG.

## Βήμα 2: Φόρτωση του βιβλίου εργασίας που περιέχει τις μεταβλητές γραμματοσειρές

Τώρα θα ανοίξουμε το αρχείο Excel. Η κλάση `Workbook` αφηρεί ολόκληρο το αρχείο, δίνοντάς μας πρόσβαση σε φύλλα, στυλ και, κυρίως, στις επιλογές σετ σελίδας που θα τροποποιήσουμε αργότερα.

```java
import com.aspose.cells.*;

public class ExcelToSvg {
    public static void main(String[] args) throws Exception {
        // Step 2: Load the workbook containing the variable fonts
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

Παρατηρήστε ότι δεν έχουμε κάνει κάτι περίπλοκο ακόμη—απλώς μια απλή φόρτωση. Αν το αρχείο βρίσκεται στο classpath, μπορείτε να χρησιμοποιήσετε `getClass().getResourceAsStream(...)` αντί αυτού.

## Βήμα 3: Ενεργοποίηση ενσωμάτωσης γραμματοσειρών στο παραγόμενο SVG

Η ενσωμάτωση γραμματοσειρών είναι η καρδιά του **how to embed fonts in SVG**. Χωρίς αυτή τη σημάνση, το SVG θα αναφέρεται σε συστημικές γραμματοσειρές, και όποιος το ανοίξει σε μηχάνημα χωρίς αυτές τις γραμματοσειρές θα δει εναλλακτική, συχνά καταστρέφοντας το σχέδιο.

```java
        // Step 3: Enable embedding of fonts in the generated SVG
        Worksheet worksheet = workbook.getWorksheets().get(0); // first sheet
        worksheet.getPageSetup().setSvgEmbeddedFonts(true);
```

Η κλήση `setSvgEmbeddedFonts(true)` λέει στο Aspose.Cells να ενσωματώσει τα δεδομένα της γραμματοσειράς (ως base‑64) απευθείας στην ενότητα `<style>` του SVG. Αυτό κάνει το αρχείο μεγαλύτερο—αναμένετε αύξηση 20‑30 %—αλλά εγγυάται οπτική πιστότητα σε όλους τους περιηγητές.

### Γιατί είναι σημαντικό

Σκεφτείτε το SVG ως μια ιστοσελίδα. Αν συνδέσετε ένα εξωτερικό stylesheet που αναφέρεται σε γραμματοσειρά που δεν υπάρχει στη συσκευή του επισκέπτη, ο περιηγητής θα επιστρέψει σε Arial ή Times New Roman. Με την ενσωμάτωση, στέλνουμε ακριβώς τα σχήματα των γλύφων, όπως κάνει ένα PDF. Γι' αυτό το **embed fonts in svg** είναι απαραίτητη προϋπόθεση για περιουσιακά στοιχεία branding.

## Βήμα 4: Προετοιμασία επιλογών εικόνας/εκτύπωσης και επιλογή SVG ως μορφή εξόδου

Το Aspose.Cells χρησιμοποιεί την κλάση `ImageOrPrintOptions` για τον έλεγχο της αλυσίδας απόδοσης. Θα ορίσουμε τη μορφή αποθήκευσης σε SVG και προαιρετικά θα ρυθμίσουμε ανάλυση ή κλιμάκωση αν χρειάζεστε πιο πυκνό διάνυσμα.

```java
        // Step 4: Prepare image/print options and set the output format to SVG
        ImageOrPrintOptions options = new ImageOrPrintOptions();
        options.setSaveFormat(SaveFormat.SVG);
        // Optional: increase DPI for sharper text outlines (default is 96)
        // options.setResolution(300);
```

Μπορείτε επίσης να ενεργοποιήσετε `setOnePagePerSheet(true)` αν θέλετε κάθε φύλλο να γίνει ξεχωριστό αρχείο SVG αντί για ένα πολυσελίδες έγγραφο. Για τις περισσότερες πίνακες ελέγχου, η προεπιλογή ενός σελίδας λειτουργεί καλά.

## Βήμα 5: Αποθήκευση του βιβλίου εργασίας ως αρχείο SVG με ενσωματωμένες γραμματοσειρές

Τέλος, καλούμε το `save`. Η μέθοδος δέχεται τη διαδρομή εξόδου και τις `ImageOrPrintOptions` που διαμορφώσαμε. Το αποτέλεσμα είναι ένα πλήρως αυτόνομο SVG που μπορείτε να ενσωματώσετε σε οποιαδήποτε σελίδα HTML.

```java
        // Step 5: Save the workbook as an SVG file with embedded fonts
        workbook.save("YOUR_DIRECTORY/output.svg", options);
        System.out.println("SVG exported successfully with embedded fonts.");
    }
}
```

Τρέξτε το πρόγραμμα, ανοίξτε το `output.svg` στο Chrome ή Firefox, και θα δείτε το φύλλο Excel σας αποδομένο ακριβώς όπως εμφανίζεται στην επιφάνεια εργασίας—γραμματοσειρές και όλα.

## Επαλήθευση των ενσωματωμένων γραμματοσειρών

Για να βεβαιωθείτε ότι οι γραμματοσειρές είναι πράγματι ενσωματωμένες:

1. Ανοίξτε το SVG σε έναν επεξεργαστή κειμένου.
2. Αναζητήστε `@font-face`. Θα δείτε ένα μακρύ `src: url(data:font/ttf;base64,…)` block.
3. Αν εντοπίσετε αυτό το block, η ενσωμάτωση πέτυχε.

Μπορείτε επίσης να χρησιμοποιήσετε τα εργαλεία προγραμματιστή του περιηγητή → “Computed” → “font-family” για να επιβεβαιώσετε ότι το όνομα γραμματοσειράς ταιριάζει με το αρχικό.

## Περιπτώσεις Ακρότητας και Συνηθισμένα Πιθανά Προβλήματα

### 1. Έλλειψη προσαρμοσμένων γραμματοσειρών στον διακομιστή

Αν το πηγαίο Excel αναφέρει μια γραμματοσειρά που δεν είναι εγκατεστημένη στη μηχανή που εκτελεί τη μετατροπή, το Aspose.Cells θα επιστρέψει σε προεπιλεγμένη γραμματοσειρά **πριν** την ενσωμάτωση. Για να το αποφύγετε, εγκαταστήστε τις απαιτούμενες γραμματοσειρές στον διακομιστή ή αντιγράψτε τα αρχεία `.ttf`/`.otf` σε έναν γνωστό φάκελο και προσθέστε τα στο Java `GraphicsEnvironment`:

```java
GraphicsEnvironment ge = GraphicsEnvironment.getLocalGraphicsEnvironment();
ge.registerFont(Font.createFont(Font.TRUETYPE_FONT, new File("fonts/Roboto-Regular.ttf")));
```

### 2. Πολύ μεγάλες γραμματοσειρές αυξάνουν το μέγεθος του SVG

Η ενσωμάτωση μιας πλήρους συλλογής TrueType μπορεί να φουσκώσει το SVG σε αρκετά megabytes. Αν το μέγεθος αποτελεί πρόβλημα, σκεφτείτε την υποσύνολο της γραμματοσειράς μόνο στα γλύφη που χρησιμοποιούνται στο φύλλο. Το Aspose.Cells δεν εκθέτει άμεσα υποσύνολο, αλλά μπορείτε να επεξεργαστείτε το SVG με εργαλεία όπως το **fonttools** για να αφαιρέσετε αχρησιμοποίητα γλύφη.

### 3. Χρωματικά προφίλ και διαφάνεια

Το SVG διαχειρίζεται τη διαφάνεια εγγενώς, αλλά ορισμένα παλαιότερα θέματα Excel χρησιμοποιούν χρωματιστές παλέτες που μπορεί να αποδοθούν διαφορετικά. Δοκιμάστε με μερικά δείγματα φύλλων για να βεβαιωθείτε ότι τα χρώματα παραμένουν ακριβή. Ρυθμίστε τη σημάνση `options.setTransparent(true)` αν χρειάζεστε διαφανές φόντο.

### 4. Μετατροπή Excel σε διανυσματικές μορφές εκτός του SVG

Αφού έχουμε ήδη διαμορφώσει τις `ImageOrPrintOptions`, η αλλαγή του `SaveFormat.SVG` σε `SaveFormat.PDF` ή `SaveFormat.EMF` είναι τριβιακή. Αυτό ικανοποιεί την απαίτηση **convert excel to vector** χωρίς να ξαναγράψουμε λογική.

```java
options.setSaveFormat(SaveFormat.PDF); // for PDF
options.setSaveFormat(SaveFormat.EMF); // for EMF
```

## Πλήρες Παράδειγμα Εργασίας (Όλα τα Βήματα Μαζί)

Παρακάτω βρίσκεται το πλήρες, έτοιμο‑για‑εκτέλεση πρόγραμμα Java που ενσωματώνει κάθε κομμάτι που συζητήσαμε. Αντιγράψτε‑επικολλήστε, προσαρμόστε τις διαδρομές, και είστε έτοιμοι.

```java
import com.aspose.cells.*;
import java.awt.Font;
import java.awt.GraphicsEnvironment;
import java.io.File;

public class ExcelToSvg {
    public static void main(String[] args) throws Exception {
        // Optional: Register custom fonts if they aren't installed on the host OS
        GraphicsEnvironment ge = GraphicsEnvironment.getLocalGraphicsEnvironment();
        ge.registerFont(Font.createFont(Font.TRUETYPE_FONT, new File("fonts/Roboto-Regular.ttf")));

        // Load the workbook (Step 2)
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Enable font embedding (Step 3)
        Worksheet worksheet = workbook.getWorksheets().get(0);
        worksheet.getPageSetup().setSvgEmbeddedFonts(true);

        // Configure SVG options (Step 4)
        ImageOrPrintOptions options = new ImageOrPrintOptions();
        options.setSaveFormat(SaveFormat.SVG);
        // options.setResolution(300); // uncomment for higher DPI if needed

        // Save as SVG with embedded fonts (Step 5)
        workbook.save("YOUR_DIRECTORY/output.svg", options);
        System.out.println("SVG exported successfully with embedded fonts.");


## Τι πρέπει να μάθετε στη συνέχεια;

Οι παρακάτω οδηγίες καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κυριαρχήσετε επιπλέον δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Convert Excel to SVG Using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/workbook-operations/convert-excel-to-svg-aspose-cells-net/)
- [Convert Excel Sheets to SVG using Aspose.Cells Java&#58; A Comprehensive Guide](/cells/english/java/workbook-operations/convert-excel-to-svg-aspose-cells-java/)
- [How to Convert Excel Charts to SVG Using Aspose.Cells for .NET (Step-by-Step Guide)](/cells/english/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}