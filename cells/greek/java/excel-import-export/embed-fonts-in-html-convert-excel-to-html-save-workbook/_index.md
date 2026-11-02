---
category: general
date: 2026-06-27
description: Ενσωματώστε γραμματοσειρές σε HTML όταν μετατρέπετε το Excel σε HTML.
  Μάθετε πώς να αποθηκεύετε το βιβλίο εργασίας ως HTML με ενσωματωμένες γραμματοσειρές
  χρησιμοποιώντας απλό κώδικα Java.
draft: false
keywords:
- embed fonts in html
- convert excel to html
- save workbook as html
- Java Excel to HTML conversion
- Aspose.Cells HTML export
language: el
og_description: Ενσωματώστε γραμματοσειρές σε HTML κατά τη μετατροπή του Excel σε
  HTML. Αυτός ο οδηγός δείχνει πώς να αποθηκεύσετε το βιβλίο εργασίας ως HTML με ενσωματωμένες
  γραμματοσειρές χρησιμοποιώντας Java.
og_title: Ενσωμάτωση γραμματοσειρών σε HTML – Μετατροπή Excel σε HTML & Αποθήκευση
  βιβλίου εργασίας
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Embed fonts in HTML when you convert Excel to HTML. Learn how to save
    workbook as HTML with embedded fonts using simple Java code.
  headline: Embed Fonts in HTML – Convert Excel to HTML & Save Workbook
  type: TechArticle
- description: Embed fonts in HTML when you convert Excel to HTML. Learn how to save
    workbook as HTML with embedded fonts using simple Java code.
  name: Embed Fonts in HTML – Convert Excel to HTML & Save Workbook
  steps:
  - name: Right‑click the page → “View Page Source”.
    text: Right‑click the page → “View Page Source”.
  - name: 'Search for `@font-face`. You’ll find a CSS rule that contains a `src: url(data:font/ttf;base64,…)`
      line—this is the Base64‑encoded font data.'
    text: 'Search for `@font-face`. You’ll find a CSS rule that contains a `src: url(data:font/ttf;base64,…)`
      line—this is the Base64‑encoded font data.'
  - name: Load or create the workbook.
    text: Load or create the workbook.
  - name: Create `HtmlSaveOptions` and enable `setEmbedFonts(true)`.
    text: Create `HtmlSaveOptions` and enable `setEmbedFonts(true)`.
  - name: Call `Workbook.save` with those options.
    text: Call `Workbook.save` with those options.
  type: HowTo
tags:
- Java
- Aspose.Cells
- HTML
- Excel
title: Ενσωμάτωση γραμματοσειρών σε HTML – Μετατροπή Excel σε HTML & Αποθήκευση βιβλίου
  εργασίας
url: /el/java/excel-import-export/embed-fonts-in-html-convert-excel-to-html-save-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ενσωμάτωση Γραμματοσειρών σε HTML – Μετατροπή Excel σε HTML & Αποθήκευση Βιβλίου Εργασίας

Έχετε ποτέ χρειαστεί να **ενσωματώσετε γραμματοσειρές σε HTML** όταν *μετατρέπετε το Excel σε HTML*; Ίσως να δημιουργείτε μια πύλη αναφορών και οι προεπιλεγμένες γραμματοσειρές web δεν είναι επαρκείς. Τα καλά νέα είναι ότι δεν χρειάζεται να συμβιβαστείτε με την απλή, γενική εμφάνιση — το Aspose.Cells σας επιτρέπει να συσκευάσετε τις ακριβείς γραμματοσειρές που χρησιμοποιήσατε στο φύλλο εργασίας απευθείας στο παραγόμενο αρχείο HTML.

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα ένα πλήρες, έτοιμο‑για‑εκτέλεση παράδειγμα Java που **αποθηκεύει το βιβλίο εργασίας ως HTML** με ενσωματωμένες γραμματοσειρές, εξηγεί γιατί θα θέλατε να το κάνετε και επισημαίνει μερικά πιθανά προβλήματα. Στο τέλος θα έχετε μια αυτόνομη σελίδα HTML που φαίνεται ακριβώς όπως το αρχικό φύλλο Excel, χωρίς ελλιπείς χαρακτήρες, χωρίς προβλήματα εξωτερικού CSS.

## Τι Θα Μάθετε

- Πώς να φορτώσετε ένα υπάρχον βιβλίο εργασίας Excel (ή να δημιουργήσετε ένα από το μηδέν) σε Java.  
- Πώς να διαμορφώσετε το `HtmlSaveOptions` ώστε να ενσωματώνει τις γραμματοσειρές του βιβλίου εργασίας απευθείας στην έξοδο HTML.  
- Πώς να καλέσετε το `Workbook.save` ώστε το αρχείο να γραφτεί ως **HTML με ενσωματωμένες γραμματοσειρές**.  
- Συμβουλές για τη διαχείριση μεγάλων αρχείων γραμματοσειρών, προσαρμοσμένων καταλόγων γραμματοσειρών και την αντιμετώπιση κοινών προβλημάτων.

> **Προαπαιτούμενο:** Χρειάζεστε το Aspose.Cells for Java (τελευταία έκδοση) στο classpath σας και ένα runtime Java 8+. Δεν απαιτούνται άλλες βιβλιοθήκες τρίτων.

---

## Βήμα 1: Ρύθμιση του Έργου και Εισαγωγή Απαιτούμενων Κλάσεων

Πριν βουτήξουμε στον κώδικα, ας βεβαιωθούμε ότι το περιβάλλον ανάπτυξης είναι έτοιμο. Αν χρησιμοποιείτε Maven, προσθέστε την εξάρτηση Aspose.Cells στο `pom.xml` σας:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- Use the newest version available -->
</dependency>
```

Αν προτιμάτε Gradle, το ισοδύναμο είναι:

```gradle
implementation 'com.aspose:aspose-cells:23.12'
```

> **Συμβουλή:** Κρατήστε τη βιβλιοθήκη ενημερωμένη. Οι νέες εκδόσεις συχνά βελτιώνουν τη διαχείριση γραμματοσειρών και μειώνουν το μέγεθος των ενσωματωμένων δεδομένων.

Τώρα, εισάγετε τις κλάσεις που θα χρειαστούμε:

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.HtmlSaveOptions;
import com.aspose.cells.SaveFormat;
import java.io.File;
```

Αυτές οι εισαγωγές μας δίνουν πρόσβαση στο μοντέλο του βιβλίου εργασίας, στις επιλογές εξαγωγής HTML και σε μερικές βοηθητικές κλάσεις.

---

## Βήμα 2: Φόρτωση (ή Δημιουργία) του Βιβλίου Εργασίας Excel

Μπορείτε είτε να φορτώσετε ένα υπάρχον αρχείο `.xlsx` είτε να δημιουργήσετε ένα βιβλίο εργασίας άμεσα. Για παράδειγμα, ας υποθέσουμε ότι έχουμε ένα αρχείο με όνομα `Sample.xlsx` στον φάκελο `resources` του έργου.

```java
// Load an existing workbook
String inputPath = "resources/Sample.xlsx";
Workbook wb = new Workbook(inputPath);
```

Αν δεν έχετε αρχείο προέλευσης, μπορείτε να δημιουργήσετε γρήγορα ένα βιβλίο εργασίας:

```java
// Create a workbook from scratch (optional)
Workbook wb = new Workbook();               // creates a new empty workbook
wb.getWorksheets().get(0).getCells().putValue("A1", "Hello, world!");
```

> **Γιατί είναι σημαντικό:** Όταν ενσωματώνετε γραμματοσειρές, το Aspose.Cells εξάγει τις ακριβείς ορισμούς γραμματοσειρών που χρησιμοποιούνται στο βιβλίο εργασίας. Αν το βιβλίο εργασίας περιέχει προσαρμοσμένες γραμματοσειρές, αυτές θα μεταφερθούν με το HTML, εξασφαλίζοντας οπτική πιστότητα.

---

## Βήμα 3: Διαμόρφωση του HtmlSaveOptions για Ενσωμάτωση Γραμματοσειρών

Αυτό είναι το κεντρικό μέρος του tutorial. Από προεπιλογή, το `HtmlSaveOptions` γράφει CSS που αναφέρεται σε γραμματοσειρές συστήματος. Για να αλλάξουμε αυτή τη συμπεριφορά, ενεργοποιούμε τη σημαία `setEmbedFonts(true)`.

```java
// Step 1: Create HTML save options
HtmlSaveOptions htmlOpts = new HtmlSaveOptions(SaveFormat.HTML);

// Step 2: Enable embedding of fonts in the HTML output
htmlOpts.setEmbedFonts(true);

// (Optional) Reduce the size of embedded fonts by subsetting only used glyphs
htmlOpts.setSubsetFonts(true);
```

### Τι Κάνουν οι Επιλογές

| Option | Default | Effect when changed |
|--------|---------|---------------------|
| `setEmbedFonts(true)` | `false` | Ενσωματώνει τα πλήρη αρχεία γραμματοσειρών (συνήθως ως Base64‑κωδικοποιημένα data URIs) μέσα στο παραγόμενο HTML. |
| `setSubsetFonts(true)` | `false` | Περιορίζει τη ενσωματωμένη γραμματοσειρά μόνο στους χαρακτήρες που χρησιμοποιούνται, μειώνοντας δραστικά το μέγεθος του αρχείου. |
| `setFontEmbeddingMode(HtmlSaveOptions.FontEmbeddingMode.EMBED_ALL)` | `EMBED_ALL` | Μπορείτε να επιλέξετε να ενσωματώσετε μόνο συγκεκριμένες γραμματοσειρές εάν υπάρχουν περιορισμοί αδειοδότησης. |

> **Ακραία περίπτωση:** Αν το βιβλίο εργασίας χρησιμοποιεί γραμματοσειρά που δεν είναι εγκατεστημένη στον διακομιστή, το Aspose.Cells επιστρέφει σε προεπιλεγμένη γραμματοσειρά συστήματος. Για να αποφύγετε εκπλήξεις, βεβαιωθείτε ότι όλες οι προσαρμοσμένες γραμματοσειρές είναι διαθέσιμες στον φάκελο γραμματοσειρών του Java runtime ή καταχωρίστε τις χειροκίνητα μέσω `FontConfig`.

---

## Βήμα 4: Αποθήκευση του Βιβλίου Εργασίας ως HTML με Ενσωματωμένες Γραμματοσειρές

Τώρα που οι επιλογές έχουν οριστεί, απλώς καλούμε το `save`. Η έξοδος θα είναι ένα μοναδικό αρχείο `.html` που περιέχει τα δεδομένα του βιβλίου εργασίας **και** τα αρχεία γραμματοσειρών κωδικοποιημένα απευθείας στο markup.

```java
// Step 3: Save the workbook as an HTML file with embedded fonts
String outputDir = "output";
new File(outputDir).mkdirs(); // Ensure the folder exists

String outputPath = outputDir + File.separator + "page.html";
wb.save(outputPath, htmlOpts);

System.out.println("HTML file with embedded fonts created at: " + outputPath);
```

Όταν ανοίξετε το `page.html` σε οποιονδήποτε σύγχρονο περιηγητή, η σελίδα θα εμφανιστεί με την ακριβή ίδια τυπογραφία που είδατε στο Excel — χωρίς εξωτερικά αρχεία γραμματοσειρών, χωρίς ελλιπείς χαρακτήρες.

---

## Βήμα 5: Επαλήθευση του Αποτελέσματος και Κατανόηση της Εξόδου

Ανοίξτε το παραγόμενο αρχείο HTML σε έναν περιηγητή (Chrome, Firefox, Edge — όποιον προτιμάτε). Θα πρέπει να δείτε το φύλλο εργασίας να αποδίδεται πιστά. Για να ελέγξετε ξανά ότι οι γραμματοσειρές είναι πραγματικά ενσωματωμένες:

1. Κάντε δεξί κλικ στη σελίδα → “View Page Source”.  
2. Αναζητήστε `@font-face`. Θα βρείτε έναν κανόνα CSS που περιέχει μια γραμμή `src: url(data:font/ttf;base64,…)` — αυτό είναι το Base64‑κωδικοποιημένο δεδομένο γραμματοσειράς.

Αν το δείτε, το βήμα **ενσωμάτωσης γραμματοσειρών σε HTML** πέτυχε.

### Συχνές Ερωτήσεις

- **“Γιατί το αρχείο HTML είναι μεγαλύτερο από το αναμενόμενο?”**  
  Η ενσωμάτωση πλήρων αρχείων γραμματοσειρών μπορεί να προσθέσει μερικές εκατοντάδες kilobytes. Χρησιμοποιήστε το `setSubsetFonts(true)` για να το μειώσετε, ή σκεφτείτε να μετατρέψετε μόνο τα απαραίτητα φύλλα.

- **“Μπορώ να ενσωματώσω μόνο μια συγκεκριμένη γραμματοσειρά?”**  
  Ναι. Ορίστε `htmlOpts.setFontEmbeddingMode(HtmlSaveOptions.FontEmbeddingMode.EMBED_SPECIFIED)` και στη συνέχεια καθορίστε τα ονόματα γραμματοσειρών μέσω `htmlOpts.getSpecifiedFontNames().add("MyCustomFont")`.

- **“Τι γίνεται αν η γραμματοσειρά είναι αδειοδοτημένη και δεν μπορώ να την ενσωματώσω?”**  
  Απενεργοποιήστε τη σημαία (`setEmbedFonts(false)`) και παρέχετε μια εναλλακτική web‑safe μέσω CSS, ή φιλοξενήστε τη γραμματοσειρά σε CDN όπου έχετε άδεια.

---

## Βήμα 6: Διαχείριση Μεγάλων Βιβλίων Εργασίας και Συμβουλές Απόδοσης

Η ενσωμάτωση γραμματοσειρών λειτουργεί καλά για μικρά λογιστικά φύλλα, αλλά ένα βιβλίο εργασίας με δεκάδες προσαρμοσμένες γραμματοσειρές μπορεί να αυξήσει το μέγεθος του HTML. Εδώ είναι μερικές προτάσεις προσανατολισμένες στην απόδοση:

- **Υποσύνολο γραμματοσειρών** (όπως ήδη δείξαμε) για να διατηρηθούν μόνο τα χρησιμοποιούμενα γλύφια.  
- **Εξαγωγή μόνο των απαραίτητων φύλλων εργασίας** χρησιμοποιώντας `htmlOpts.setExportActiveWorksheetOnly(true)`.  
- **Συμπίεση του HTML** μετά τη δημιουργία (π.χ., gzip στον διακομιστή) για μείωση της καθυστέρησης δικτύου.  
- **Cache του παραγόμενου HTML** εάν το ίδιο αρχείο Excel ζητείται συχνά.

---

## Βήμα 7: Επόμενα Βήματα – Πέρα από τη Βασική Εξαγωγή

Τώρα που έχετε κατακτήσει την **ενσωμάτωση γραμματοσειρών σε HTML**, ίσως θέλετε να εξερευνήσετε σχετικές δυνατότητες:

- **Μετατροπή Excel σε HTML με εικόνες** (`htmlOpts.setExportImagesAsBase64(true)`).  
- **Δημιουργία PDF αντί για HTML** (`wb.save("output.pdf", SaveFormat.PDF)`).  
- **Δημιουργία responsive HTML** τροποποιώντας `htmlOpts.setExportActiveWorksheetOnly` και `htmlOpts.setExportGridLines`.  

Όλες αυτές οι δυνατότητες ακολουθούν το ίδιο μοτίβο: διαμορφώστε ένα αντικείμενο `*SaveOptions`, ενεργοποιήστε τις κατάλληλες σημαίες και καλέστε το `Workbook.save`.

---

## Συμπέρασμα

Μόλις μάθατε πώς να **ενσωματώνετε γραμματοσειρές σε HTML** ενώ **μετατρέπετε το Excel σε HTML** και **αποθηκεύετε το βιβλίο εργασίας ως HTML** χρησιμοποιώντας το Aspose.Cells for Java. Τα βασικά βήματα είναι:

1. Φορτώστε ή δημιουργήστε το βιβλίο εργασίας.  
2. Δημιουργήστε `HtmlSaveOptions` και ενεργοποιήστε το `setEmbedFonts(true)`.  
3. Καλέστε το `Workbook.save` με αυτές τις επιλογές.

Το αποτέλεσμα είναι ένα μοναδικό, φορητό αρχείο HTML που φαίνεται ακριβώς όπως το αρχικό σας λογιστικό φύλλο — χωρίς ελλιπείς τύπους γραμματοσειρών, χωρίς επιπλέον αρχεία CSS, και χωρίς εξάρτηση από τις γραμματοσειρές που είναι εγκατεστημένες στον πελάτη.

Μη διστάσετε να πειραματιστείτε με υποσύνολο γραμματοσειρών, επιλεκτική ενσωμάτωση, ή ακόμη και συνδυασμό με caching στο server για σενάρια υψηλής κίνησης. Αν αντιμετωπίσετε οποιαδήποτε ιδιωματισμούς (όπως απροσδόκητα μεγάλα αρχεία ή ελλιπείς γλύφια), επανεξετάστε τις προαιρετικές ρυθμίσεις που καλύψαμε και προσαρμόστε ανάλογα.

Καλή προγραμματιστική δουλειά, και απολαύστε το pixel‑perfect HTML που μπορείτε τώρα να σερβίρετε απευθείας από τις Java εφαρμογές σας!

## Τι Θα Μάθετε Στη Σύντομη Μελλοντική Περίοδο;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Convert Excel to HTML in Java Using Aspose.Cells: A Step-by-Step Guide](/cells/english/java/workbook-operations/convert-excel-html-aspose-cells-java/)
- [Export Excel to HTML Using Aspose.Cells for Java: A Complete Guide](/cells/english/java/workbook-operations/export-excel-to-html-aspose-cells-java/)
- [Export Excel to HTML using IStreamProvider & Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/workbook-operations/export-excel-html-streamprovider-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}