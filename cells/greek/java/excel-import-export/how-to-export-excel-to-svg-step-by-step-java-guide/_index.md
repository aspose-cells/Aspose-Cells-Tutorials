---
category: general
date: 2026-06-30
description: Μάθετε πώς να εξάγετε το Excel σε SVG με το Aspose.Cells, να ενσωματώσετε
  γραμματοσειρές και επίσης να λάβετε έξοδο XPS. Ιδανικό για προγραμματιστές Java
  που χρειάζονται αξιόπιστη εξαγωγή SVG.
draft: false
keywords:
- how to export excel to svg
- aspose cells svg export
- embed fonts in svg
- excel to xps conversion
- java excel export tutorial
language: el
og_description: Πώς να εξάγετε το Excel σε SVG με ενσωματωμένες γραμματοσειρές χρησιμοποιώντας
  το Aspose.Cells. Ακολουθήστε αυτόν τον οδηγό για ένα καθαρό SVG και προαιρετική
  έξοδο XPS.
og_title: Πώς να εξάγετε το Excel σε SVG – Πλήρης οδηγός Java
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Learn how to export Excel to SVG with Aspose.Cells, embed fonts, and
    also get XPS output. Perfect for Java developers needing reliable SVG export.
  headline: How to Export Excel to SVG – Step‑by‑Step Java Guide
  type: TechArticle
tags:
- Aspose.Cells
- Java
- SVG
- Excel
title: Πώς να εξάγετε το Excel σε SVG – Οδηγός Java βήμα‑προς‑βήμα
url: /el/java/excel-import-export/how-to-export-excel-to-svg-step-by-step-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Εξάγετε το Excel σε SVG – Πλήρης Οδηγός Java

Έχετε αναρωτηθεί ποτέ **πώς να εξάγετε το Excel σε SVG** χωρίς να χάσετε εκείνες τις κομψές παραλλαγές γραμματοσειρών; Δεν είστε μόνοι. Πολλοί προγραμματιστές συναντούν πρόβλημα όταν το παραγόμενο SVG φαίνεται απλό επειδή οι γραμματοσειρές δεν ενσωματώθηκαν.  

Σε αυτόν τον οδηγό θα περάσουμε βήμα‑βήμα μια σύντομη, ολοκληρωμένη λύση χρησιμοποιώντας το **Aspose.Cells for Java** που όχι μόνο εξάγει σε SVG αλλά επίσης διατηρεί τις πληροφορίες γραμματοσειράς. Επιπλέον, θα σας δείξουμε μια γρήγορη εξαγωγή XPS ώστε να μπορείτε να συγκρίνετε τις δύο μορφές πλευρά‑προς‑πλευρά.  

Θα ολοκληρώσετε με ένα έτοιμο‑για‑εκτέλεση Java snippet, μια εξήγηση κάθε επιλογής, και μερικές επαγγελματικές συμβουλές για να αποφύγετε τα κοινά προβλήματα που παρενοχλούν τους αρχάριους.

---

## Τι Θα Δημιουργήσετε

Στο τέλος αυτού του οδηγού θα έχετε:

* Ένα πρόγραμμα Java που φορτώνει ένα βιβλίο εργασίας Excel (`varfont.xlsx`).
* Λογική εξαγωγής που αποθηκεύει το βιβλίο εργασίας ως αρχείο **SVG** με ενσωματωμένες γραμματοσειρές (`out.svg`).
* Προαιρετική έξοδος XPS (`out.xps`) για περιπτώσεις όπου χρειάζεστε μια σελιδοποιημένη προεπισκόπηση.
* Σαφείς οδηγίες για τη διαχείριση περιπτώσεων άκρων σχετικών με γραμματοσειρές, όπως ελλιπείς γραμματοσειρές ή προσαρμοσμένα γλυφίδες.

Δεν απαιτούνται εξωτερικά εργαλεία πέρα από το Aspose.Cells JAR, και ο κώδικας εκτελείται σε οποιοδήποτε runtime Java 8+.

## Προαπαιτούμενα

* **Java Development Kit (JDK) 8 ή νεότερο** – μπορείτε να το επαληθεύσετε με `java -version`.
* **Aspose.Cells for Java** – κατεβάστε το τελευταίο JAR από την ιστοσελίδα Aspose ή προσθέστε την εξάρτηση Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- check for the newest version -->
</dependency>
```

* Ένα δείγμα αρχείου Excel (`varfont.xlsx`) που περιέχει μερικά κελιά με διαφορετικές γραμματοσειρές ή χαρακτήρες Unicode.  
* Ένα IDE ή απλός επεξεργαστής κειμένου· ο κώδικας λειτουργεί σε IntelliJ, Eclipse ή ακόμη και VS Code.

## Βήμα 1: Φόρτωση του Βιβλίου Εργασίας Excel  

Το πρώτο που κάνουμε είναι να δημιουργήσουμε μια παρουσία `Workbook` που δείχνει στο πηγαίο αρχείο μας. Αυτό το αντικείμενο αντιπροσωπεύει ολόκληρο το λογιστικό φύλλο στη μνήμη.

```java
// Step 1: Load the Excel workbook
Workbook workbook = new Workbook("YOUR_DIRECTORY/varfont.xlsx");
```

> **Γιατί είναι σημαντικό:** Η φόρτωση του βιβλίου εργασίας μία φορά διατηρεί το υπόλοιπο της διαδικασίας γρήγορο. Εάν το αρχείο δεν βρεθεί, το Aspose ρίχνει μια σαφή `FileNotFoundException`, ώστε να ξέρετε ακριβώς τι πρέπει να διορθώσετε.

## Βήμα 2: Προετοιμασία Επιλογών Αποθήκευσης XPS (Προαιρετικό)  

Εάν χρειάζεστε επίσης μια σελιδοποιημένη προβολή — π.χ. για εκτύπωση ή προεπισκόπηση — μπορείτε να εξάγετε σε XPS. Η βασική ρύθμιση είναι `setEmbedFonts(true)`, η οποία εξασφαλίζει ότι το XPS περιέχει τα ίδια γλυφίδες με το αρχικό αρχείο Excel.

```java
// Step 2: Set up XPS save options to embed fonts (preserves variation selectors)
XpsSaveOptions xpsOptions = new XpsSaveOptions();
xpsOptions.setEmbedFonts(true);
```

> **Συμβουλή επαγγελματία:** Το XPS είναι χρήσιμο για έγγραφα που θα προβληθούν σε συσκευές Windows. Διατηρεί τη διάταξη ακριβώς όπως εμφανίζεται στο Excel, σε αντίθεση με το SVG που είναι βασισμένο σε διανύσματα αλλά μπορεί να ερμηνεύσει διαφορετικά ορισμένες λεπτομέρειες διάταξης.

## Βήμα 3: Αποθήκευση ως XPS (Προαιρετικό)  

Τώρα γράφουμε πραγματικά το αρχείο XPS. Εάν δεν χρειάζεστε XPS, μπορείτε να παραλείψετε εντελώς τα Βήματα 2‑3.

```java
// Step 3: Save the workbook as an XPS document with embedded fonts
workbook.save("YOUR_DIRECTORY/out.xps", xpsOptions);
```

**Αναμενόμενο αποτέλεσμα:** Το `out.xps` εμφανίζεται στον φάκελο προορισμού. Ανοίγοντάς το σε Windows XPS Viewer θα πρέπει να δείτε το λογιστικό φύλλο με τις ίδιες γραμματοσειρές.

## Βήμα 4: Διαμόρφωση Επιλογών Αποθήκευσης SVG – Ενσωμάτωση Γραμματοσειρών  

Εδώ συμβαίνει η μαγεία της **aspose cells svg export**. Ενεργοποιώντας το `setEmbedFonts(true)` λέμε στο Aspose να ενσωματώσει τα αρχεία γραμματοσειρών απευθείας στην ενότητα `<defs>` του SVG, διατηρώντας τους Unicode variation selectors και τα προσαρμοσμένα γλυφίδες.

```java
// Step 4: Set up SVG save options to embed fonts
SvgSaveOptions svgOptions = new SvgSaveOptions();
svgOptions.setEmbedFonts(true);
```

> **Γιατί να ενσωματώσετε γραμματοσειρές;** Χωρίς ενσωμάτωση, το SVG εξαρτάται από τις εγκατεστημένες γραμματοσειρές του θεατή. Εάν ένας χρήστης δεν διαθέτει την ακριβή γραμματοσειρά, το κείμενο μπορεί να επιστρέψει σε μια γενική οικογένεια, διασπώντας την οπτική πιστότητα — ιδιαίτερα προβληματικό για διαγράμματα ή αναφορές συγκεκριμένων εμπορικών σημάτων.

## Βήμα 5: Εξαγωγή του Βιβλίου Εργασίας σε SVG  

Τέλος, γράφουμε το αρχείο SVG. Η ίδια μέθοδος `Workbook.save` δέχεται το `SvgSaveOptions` που μόλις διαμορφώσαμε.

```java
// Step 5: Save the workbook as an SVG file with embedded fonts
workbook.save("YOUR_DIRECTORY/out.svg", svgOptions);
```

**Τι θα δείτε:** Ανοίξτε το `out.svg` σε οποιονδήποτε σύγχρονο περιηγητή (Chrome, Edge, Firefox) και θα έχετε μια καθαρή, κλιμακώσιμη αναπαράσταση του λογιστικού σας φύλλου. Περνάτε το ποντίκι πάνω από τα στοιχεία κειμένου στην πηγή για να επιβεβαιώσετε ότι οι ορισμοί `<font-face>` είναι παρόντες.

## Διαχείριση Συνηθισμένων Περιπτώσεων Άκρων  

| **Απουσία Αρχείων Γραμματοσειρών** | Το Aspose μπορεί να ενσωματώσει εναλλακτική εάν η γραμματοσειρά δεν είναι εγκατεστημένη στο μηχάνημα. | Εγκαταστήστε τις απαιτούμενες γραμματοσειρές στον διακομιστή ή αντιγράψτε τα αρχεία `.ttf/.otf` σε γνωστό φάκελο και ορίστε `svgOptions.setFontFolderPath("path/to/fonts")`. |
| **Μεγάλα Βιβλία Εργασίας** | Η εξαγωγή ενός τεράστιου φύλλου μπορεί να παράγει ένα τεράστιο SVG (μεγabytes). | Χρησιμοποιήστε `svgOptions.setCompress(true)` για συμπίεση gzip του αποτελέσματος, ή χωρίστε το βιβλίο εργασίας σε πολλαπλά φύλλα πριν την εξαγωγή. |
| **Unicode Variation Selectors** | Κάποιοι σπάνιοι χαρακτήρες μπορεί ακόμη να μην αποδίδονται σωστά. | Βεβαιωθείτε ότι το πηγαίο Excel χρησιμοποιεί μια γραμματοσειρά που υποστηρίζει πλήρως αυτούς τους επιλογείς, π.χ., Noto Sans. |
| **Απόδοση** | Η επαναφόρτωση του βιβλίου εργασίας για κάθε μορφή προσθέτει επιπλέον φόρτο. | Επαναχρησιμοποιήστε την ίδια παρουσία `Workbook` για XPS και SVG όπως φαίνεται παραπάνω. |

## Συμβουλές Επαγγελματία & Καλές Πρακτικές  

* **Cache the Workbook** – Εάν εξάγετε το ίδιο αρχείο σε πολλαπλές μορφές σε μια υπηρεσία web, κρατήστε το `Workbook` στη μνήμη (ή σε ελαφρύ cache) για να αποφύγετε I/O δίσκου σε κάθε αίτημα.  
* **Set `svgOptions.setPageSize()`** – Για βιβλία εργασίας με πολλαπλά φύλλα μπορείτε να ελέγξετε το μέγεθος του καμβά SVG, αποτρέποντας απροσδόκητες διακοπές σελίδας.  
* **Validate the SVG** – Χρησιμοποιήστε έναν διαδικτυακό επικυρωτή (π.χ., W3C SVG Validator) για να διασφαλίσετε ότι το παραγόμενο markup συμμορφώνεται με τα πρότυπα, ειδικά αν σκοπεύετε να το επεξεργαστείτε περαιτέρω.  
* **Security** – Ποτέ μην εκθέτετε το ακατέργαστο μονοπάτι αρχείου (`YOUR_DIRECTORY`) στους τελικούς χρήστες. Επίλυση σχετικού με ασφαλές βασικό κατάλογο και καθαρισμός οποιασδήποτε εισόδου χρήστη.  

## Πλήρες Παράδειγμα Εργασίας  

Παρακάτω υπάρχει μια πλήρης, αυτόνομη κλάση Java που μπορείτε να αντιγράψετε‑επικολλήσετε στο έργο σας. Προσαρμόστε τις σταθερές `INPUT_PATH` και `OUTPUT_PATH` ώστε να ταιριάζουν με το περιβάλλον σας.

```java
import com.aspose.cells.*;

public class ExcelToSvgExporter {

    // Adjust these paths before running
    private static final String INPUT_PATH  = "YOUR_DIRECTORY/varfont.xlsx";
    private static final String OUTPUT_SVG  = "YOUR_DIRECTORY/out.svg";
    private static final String OUTPUT_XPS  = "YOUR_DIRECTORY/out.xps";

    public static void main(String[] args) {
        try {
            // 1️⃣ Load workbook
            Workbook workbook = new Workbook(INPUT_PATH);

            // 2️⃣ (Optional) Export to XPS with embedded fonts
            XpsSaveOptions xpsOptions = new XpsSaveOptions();
            xpsOptions.setEmbedFonts(true);
            workbook.save(OUTPUT_XPS, xpsOptions);
            System.out.println("XPS saved to: " + OUTPUT_XPS);

            // 3️⃣ Configure SVG options – embed fonts
            SvgSaveOptions svgOptions = new SvgSaveOptions();
            svgOptions.setEmbedFonts(true);
            // Uncomment to compress the SVG (gzip)
            // svgOptions.setCompress(true);

            // 4️⃣ Export to SVG
            workbook.save(OUTPUT_SVG, svgOptions);
            System.out.println("SVG saved to: " + OUTPUT_SVG);

        } catch (Exception e) {
            System.err.println("Export failed: " + e.getMessage());
            e.printStackTrace();
        }
    }
}
```

**Εκτέλεση του προγράμματος:**  
```bash
javac -cp "aspose-cells-23.12.jar" ExcelToSvgExporter.java
java -cp ".:aspose-cells-23.12.jar" ExcelToSvgExporter
```

Θα πρέπει να δείτε δύο γραμμές στην κονσόλα που επιβεβαιώνουν τις θέσεις των `out.xps` και `out.svg`. Ανοίξτε το SVG σε έναν περιηγητή για να επαληθεύσετε ότι το κείμενο φαίνεται ταυτόσημο με την αρχική προβολή του Excel.

## Συμπέρασμα  

Μόλις καλύψαμε **πώς να εξάγετε το Excel σε SVG** χρησιμοποιώντας το Aspose.Cells for Java, με τις γραμματοσειρές ασφαλώς ενσωματωμένες ώστε τα γραφικά σας να παραμένουν πιστά σε οποιονδήποτε θεατή. Το ίδιο βιβλίο εργασίας μπορεί επίσης να αποθηκευτεί ως XPS, παρέχοντάς σας μια σελιδοποιημένη εναλλακτική όταν χρειάζεται.  

Θυμηθείτε να ενσωματώνετε τις γραμματοσειρές, να διαχειρίζεστε περιπτώσεις ελλιπών γραμματοσειρών, και να λαμβάνετε υπόψη την απόδοση εάν κλιμακώνετε αυτό σε μια υπηρεσία web. Με αυτές τις τεχνικές στο εργαλείο σας, η δημιουργία υψηλής ποιότητας SVG από Excel γίνεται παιχνιδάκι — χωρίς σπασμένα γλυφίδες ή θολό κείμενο.

### Τι Ακολουθεί;

* Βυθιστείτε περισσότερο στην **aspose cells svg export** προσαρμόζοντας παλέτες χρωμάτων ή αφαιρώντας γραμμές πλέγματος.  
* Εξερευνήστε την **ενσωμάτωση γραμματοσειρών σε SVG** για άλλους τύπους εγγράφων, όπως Word ή PowerPoint, χρησιμοποιώντας τις αντίστοιχες βιβλιοθήκες Aspose.  
* Δημιουργήστε ένα μικρό REST API που δέχεται ένα ανεβασμένο αρχείο Excel και επιστρέφει ένα ρεύμα SVG — ιδανικό για SaaS πίνακες αναφορών.  

Έχετε ερωτήσεις ή μια ιδιότυπη περίπτωση χρήσης; Αφήστε ένα σχόλιο παρακάτω, και καλή προγραμματιστική!

## Τι Θα Μάθετε Στη Σύντομη Μελλοντική Περίοδο;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να Εξάγετε Διαγράμματα Excel ως SVG Χρησιμοποιώντας το Aspose.Cells Java για Κλιμακώσιμα Διανυσματικά Γραφικά](/cells/english/java/charts-graphs/export-excel-charts-svg-aspose-cells-java/)
- [Εξαγωγή Διαγραμμάτων Excel σε SVG με Aspose Cells Java](/cells/german/java/charts-graphs/export-excel-charts-svg-aspose-cells-java/)
- [Εξαγωγή Διαγραμμάτων Excel σε SVG με Aspose Cells Java](/cells/french/java/charts-graphs/export-excel-charts-svg-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}