---
category: general
date: 2026-03-01
description: Μάθετε πώς να ενσωματώνετε γραμματοσειρές σε HTML και άλλα μορφότυπα.
  Αναλυτικό βήμα‑βήμα tutorial που καλύπτει την ενσωμάτωση γραμματοσειρών σε HTML,
  τη μετατροπή του Excel σε HTML, πώς να εξάγετε OLE και τη μετατροπή του Excel σε
  XPS.
draft: false
keywords:
- how to embed fonts
- embed fonts in html
- convert excel to html
- how to export ole
- convert excel to xps
language: el
og_description: Πώς να ενσωματώσετε γραμματοσειρές σε εξαγωγές HTML, XPS και OLE.
  Μάθετε τη πλήρη ροή εργασίας, δείτε εκτελέσιμο κώδικα Java και κατακτήστε την ενσωμάτωση
  γραμματοσειρών σε HTML για μετατροπές Excel.
og_title: Πώς να ενσωματώσετε γραμματοσειρές – Πλήρης οδηγός Java
tags:
- Aspose.Cells
- Java
- Document Export
title: Πώς να ενσωματώσετε γραμματοσειρές – Πλήρης οδηγός για εξαγωγή HTML, XPS και
  OLE
url: /el/java/ole-objects-embedded-content/how-to-embed-fonts-complete-guide-for-html-xps-and-ole-expor/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Ενσωματώσετε Γραμματοσειρές – Πλήρης Οδηγός για HTML, XPS και Εξαγωγή OLE

Έχετε αναρωτηθεί ποτέ **πώς να ενσωματώσετε γραμματοσειρές** όταν μετατρέπετε ένα βιβλίο εργασίας του Excel σε ιστοσελίδα ή σε εκτυπώσιμο έγγραφο; Δεν είστε μόνοι. Πολλοί προγραμματιστές συναντούν πρόβλημα όταν το αποτέλεσμα φαίνεται σωστό στον δικό τους υπολογιστή αλλά σπάει σε άλλο επειδή λείπουν οι απαιτούμενες γραμματοσειρές.  

Σε αυτό το tutorial θα περάσουμε από ένα πραγματικό σενάριο χρησιμοποιώντας το Aspose.Cells for Java: θα ενσωματώσουμε γραμματοσειρές σε HTML, θα διατηρήσουμε τους επιλογείς παραλλαγής emoji κατά τη μετατροπή σε XPS, και ακόμη θα κρατήσουμε ένα αντικείμενο OLE επεξεργάσιμο κατά την εξαγωγή σε PPTX. Στο τέλος θα έχετε μια σταθερή λύση copy‑and‑paste που απαντά στο “πώς να ενσωματώσετε γραμματοσειρές” και επίσης αγγίζει τα **embed fonts in html**, **convert excel to html**, **how to export ole**, και **convert excel to xps**.

## Προαπαιτούμενα

- Java 17 (ή οποιοδήποτε πρόσφατο JDK)  
- Aspose.Cells for Java 25.x ή νεότερο  
- Ένα IDE ανάπτυξης (IntelliJ IDEA, Eclipse ή VS Code)  
- Βασική εξοικείωση με τις δομές δεδομένων του Excel  

Δεν απαιτούνται εξωτερικές υπηρεσίες—όλα εκτελούνται τοπικά.

## Επισκόπηση της Λύσης

1. **Δημιουργήστε ένα βιβλίο εργασίας** και χρησιμοποιήστε τη λειτουργία `WRAPCOLS` για να μετατρέψετε μια κάθετη περιοχή σε διάταξη τριών στηλών.  
2. **Αποθηκεύστε το βιβλίο εργασίας ως XPS** ενεργοποιώντας τους επιλογείς παραλλαγής γραμματοσειράς ώστε τα emoji να παραμείνουν αμετάβλητα.  
3. **Εξαγωγή σε HTML** με ενσωματωμένες γραμματοσειρές, εξασφαλίζοντας ότι η σελίδα φαίνεται το ίδιο παντού.  
4. **Εξαγωγή ενός βιβλίου εργασίας που περιέχει αντικείμενο OLE σε PPTX**, διατηρώντας τη δυνατότητα επεξεργασίας.  
5. **Εφαρμογή προτύπου Smart Marker** που δείχνει τη σύνδεση δεδομένων master‑detail.  

Κάθε βήμα είναι απομονωμένο στη δική του ενότητα H2, καθιστώντας τον οδηγό εύκολο στην περιήγηση τόσο για τις μηχανές αναζήτησης όσο και για τους βοηθούς AI.

![Εικόνα για το πώς να ενσωματώσετε γραμματοσειρές](image.png "πώς να ενσωματώσετε γραμματοσειρές")

*Κείμενο alt εικόνας: διάγραμμα που δείχνει τη ροή εργασίας από το Excel στο HTML, XPS και PPTX.*

---

## Βήμα 1 – Δημιουργία Βιβλίου Εργασίας και Χρήση WRAPCOLS (Γιατί Αυτό Σημαίνει για embed fonts in html)

Πριν μπορέσουμε να μιλήσουμε για την ενσωμάτωση γραμματοσειρών, χρειαζόμαστε ένα βιβλίο εργασίας που να περιέχει πραγματικά δεδομένα. Η λειτουργία `WRAPCOLS` είναι ένας βολικός τρόπος για να χωρίσετε μια στήλη σε πολλές στήλες, κάτι που συχνά κάνει το τελικό HTML πιο ευανάγνωστο.

```java
import com.aspose.cells.*;

public class EmbedFontsDemo {
    public static void main(String[] args) throws Exception {
        // Initialize a new workbook
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.getWorksheets().get(0);

        // Populate A2:A10 with sample data
        for (int i = 2; i <= 10; i++) {
            sheet.getCells().get("A" + i).putValue("Item " + (i - 1));
        }

        // Use WRAPCOLS to create a 3‑column block starting at A1
        Cell resultCell = sheet.getCells().get("A1");
        resultCell.setFormula("=WRAPCOLS(A2:A10,3)");
        workbook.calculateFormula();

        System.out.println("WRAPCOLS result: " + resultCell.getStringValue());
        // -----------------------------------------------------------------
        // The rest of the steps are demonstrated after this point.
        // -----------------------------------------------------------------
```

**Γιατί αυτό το βήμα;**  
Η κλήση `WRAPCOLS` δημιουργεί μια πολλαπλών στηλών περιοχή που αργότερα εμφανίζεται στο HTML ως πίνακας. Όταν αργότερα **embed fonts in html**, η μορφοποίηση του πίνακα θα εξαρτηθεί από τις γραμματοσειρές που ενσωματώνουμε, εξασφαλίζοντας συνεπή απόδοση σε όλα τα προγράμματα περιήγησης.

## Βήμα 2 – Αποθήκευση του Βιβλίου Εργασίας ως XPS Διατηρώντας τα Emoji (convert excel to xps)

Αν χρειάζεστε μια μορφή έτοιμη για εκτύπωση, το XPS είναι μια αξιόπιστη επιλογή. Ωστόσο, τα σύγχρονα έγγραφα συχνά περιέχουν emoji ή σύμβολα που χρησιμοποιούν επιλογείς παραλλαγής. Η ενεργοποίηση του `EnableFontVariationSelectors` εξασφαλίζει ότι αυτοί οι χαρακτήρες θα παραμείνουν μετά τη μετατροπή.

```java
        // --------------------------------------------------------------
        // Step 2: Save as XPS with font variation selectors enabled
        // --------------------------------------------------------------
        WorkbookSettings settings = workbook.getSettings();
        settings.setEnableFontVariationSelectors(true); // crucial for emoji

        String xpsPath = "output/withVariations.xps";
        workbook.save(xpsPath, SaveFormat.XPS);
        System.out.println("Workbook saved as XPS at: " + xpsPath);
```

**Τι λαμβάνετε:**  
Ένα αρχείο XPS που εμφανίζει οποιοδήποτε ενσωματωμένο emoji ακριβώς όπως στο πηγαίο βιβλίο εργασίας. Αυτό ικανοποιεί την απαίτηση **convert excel to xps** και δείχνει ότι η διαχείριση γραμματοσειρών δεν περιορίζεται μόνο στο HTML.

## Βήμα 3 – Εξαγωγή σε HTML με Ενσωματωμένες Γραμματοσειρές (how to embed fonts & embed fonts in html)

Τώρα φτάνουμε στον πυρήνα του tutorial: **how to embed fonts** κατά τη μετατροπή του Excel σε HTML. Το Aspose.Cells μας επιτρέπει να ενσωματώσουμε τις γραμματοσειρές απευθείας στο παραγόμενο αρχείο HTML, εξαλείφοντας την ανάγκη για εξωτερικά αρχεία γραμματοσειρών.

```java
        // --------------------------------------------------------------
        // Step 3: Export to HTML with embedded fonts
        // --------------------------------------------------------------
        HtmlSaveOptions htmlOptions = new HtmlSaveOptions();
        htmlOptions.setEmbedFonts(true); // this is the key line for embed fonts in html
        htmlOptions.setExportImagesAsBase64(true); // optional, keeps all assets in one file

        String htmlPath = "output/embeddedFonts.html";
        workbook.save(htmlPath, htmlOptions);
        System.out.println("HTML with embedded fonts saved at: " + htmlPath);
```

**Πώς λειτουργεί:**  
`setEmbedFonts(true)` λέει στον renderer να διαβάσει τα αρχεία γραμματοσειρών που χρησιμοποιούνται στο βιβλίο εργασίας και να τα ενσωματώσει ως κανόνες `@font-face` κωδικοποιημένους σε Base64 μέσα στην ετικέτα `<style>`. Το παραγόμενο HTML είναι αυτόνομο, ώστε να μπορείτε να το ανεβάσετε σε οποιονδήποτε διακομιστή και οι γραμματοσειρές θα εμφανιστούν σωστά—ακριβώς αυτό που ζητούν οι προγραμματιστές όταν ψάχνουν για **how to embed fonts**.

**Αναμενόμενο απόσπασμα εξόδου (μέσα στο `embeddedFonts.html`):**

```html
<style>
@font-face{font-family:"Arial";src:url(data:font/ttf;base64,AAEAAA... ) format('truetype');}
</style>
<table>
  <tr><td>Item 1</td><td>Item 4</td><td>Item 7</td></tr>
  <tr><td>Item 2</td><td>Item 5</td><td>Item 8</td></tr>
  <tr><td>Item 3</td><td>Item 6</td><td>Item 9</td></tr>
</table>
```

Παρατηρήστε τον κανόνα `@font-face`—αυτή είναι η συγκεκριμένη απάντηση στο **embed fonts in html**.

## Βήμα 4 – Εξαγωγή Βιβλίου Εργασίας που Περιέχει Αντικείμενο OLE σε PPTX (how to export ole)

Πολλές επιχειρηματικές αναφορές ενσωματώνουν έγγραφα Word, PDF ή άλλα φύλλα Excel ως αντικείμενα OLE. Όταν εξάγετε ένα τέτοιο βιβλίο εργασίας σε PowerPoint, συχνά χάνετε τη δυνατότητα επεξεργασίας του αντικειμένου. Το Aspose.Cells διατηρεί τη δυνατότητα επεξεργασίας από την αρχή.

```java
        // --------------------------------------------------------------
        // Step 4: Export a workbook with an OLE object to PPTX
        // --------------------------------------------------------------
        // Load a workbook that already contains an OLE object.
        Workbook oleWorkbook = new Workbook("input/oleObject.xlsx");

        String pptxPath = "output/oleEditable.pptx";
        oleWorkbook.save(pptxPath, SaveFormat.PPTX);
        System.out.println("PPTX with editable OLE object saved at: " + pptxPath);
```

**Γιατί είναι σημαντικό:**  
Αν ψάχνετε για **how to export ole**, αυτό το απόσπασμα δείχνει την ακριβή κλήση API. Η προκύπτουσα διαφάνεια PowerPoint περιέχει το αντικείμενο OLE ως ζωντανό στοιχείο διπλού‑κλικ‑για‑επεξεργασία—χωρίς επιπλέον επεξεργασία.

## Βήμα 5 – Εφαρμογή Προτύπου Smart Marker (master‑detail) και Ολοκλήρωση της Επίδειξης

Τα Smart Markers σας επιτρέπουν να συνδέσετε μια πηγή δεδομένων (Map, JSON, DataTable) απευθείας με ένα πρότυπο Excel. Ακολουθεί ένα ελάχιστο παράδειγμα που εκτυπώνει γραμμές master‑detail.

```java
        // --------------------------------------------------------------
        // Step 5: Apply Smart Marker template (master‑detail)
        // --------------------------------------------------------------
        String smartMarkerTemplate = "${Orders.Master:OrderID,Customer}\n${Orders.Detail:Product,Qty,Price}";
        // Simulated data source
        java.util.Map<String, Object> dataSource = new java.util.HashMap<>();
        java.util.List<java.util.Map<String, Object>> master = new java.util.ArrayList<>();
        java.util.Map<String, Object> masterRow = new java.util.HashMap<>();
        masterRow.put("OrderID", 1001);
        masterRow.put("Customer", "Acme Corp");
        master.add(masterRow);
        dataSource.put("Orders.Master", master);

        java.util.List<java.util.Map<String, Object>> detail = new java.util.ArrayList<>();
        java.util.Map<String, Object> detailRow = new java.util.HashMap<>();
        detailRow.put("Product", "Widget");
        detailRow.put("Qty", 5);
        detailRow.put("Price", 9.99);
        detail.add(detailRow);
        dataSource.put("Orders.Detail", detail);

        SmartMarkerProcessor processor = new SmartMarkerProcessor(new Workbook());
        processor.apply(smartMarkerTemplate, dataSource);
        processor.getWorkbook().save("output/smartMarkerResult.xlsx");
        System.out.println("Smart Marker workbook saved.");
    }
}
```

**Τι βλέπετε:**  
Ένα νέο βιβλίο εργασίας (`smartMarkerResult.xlsx`) όπου τα placeholders του προτύπου έχουν αντικατασταθεί με τα δεδομένα. Αυτό το βήμα δεν αφορά άμεσα τις γραμματοσειρές, αλλά ολοκληρώνει τον οδηγό δείχνοντας μια τυπική ροή αναφοράς που συχνά προηγείται μιας εξαγωγής **embed fonts in html**.

## Συνηθισμένα Παράπλευρα Προβλήματα & Συμβουλές (Διασφάλιση Επιτυχούς Ενσωμάτωσης Γραμματοσειρών)

| Πρόβλημα | Γιατί συμβαίνει | Διόρθωση |
|----------|------------------|----------|
| Οι γραμματοσειρές λείπουν από το αρχείο HTML | Το βιβλίο εργασίας χρησιμοποιεί μια σύστημα γραμματοσειρά που δεν είναι εγκατεστημένη στον διακομιστή. | Χρησιμοποιήστε `Workbook.getSettings().setDefaultFont("Arial")` πριν τη φόρτωση των δεδομένων, ή ενσωματώστε τα απαιτούμενα αρχεία γραμματοσειρών χειροκίνητα. |
| Το παραγόμενο HTML είναι τεράστιο | Η ενσωμάτωση πολλών μεγάλων γραμματοσειρών αυξάνει το μέγεθος του αρχείου. | Περιορίστε την ενσωμάτωση μόνο στις γραμματοσειρές που χρησιμοποιείτε πραγματικά: `htmlOptions.setFontEmbeddingMode(HtmlFontEmbeddingMode.EmbedSubset)`. |
| Τα emoji εξαφανίζονται μετά τη μετατροπή σε XPS | Οι επιλογείς παραλλαγής αφαιρούνται εξ ορισμού. | Ενεργοποιήστε `settings.setEnableFontVariationSelectors(true)` όπως φαίνεται στο Βήμα 2. |
| Το αντικείμενο OLE γίνεται στατική εικόνα σε PPTX | Το πηγαίο βιβλίο εργασίας αποθηκεύτηκε με `setSuppressOLEObjects(true)`. | Βεβαιωθείτε ότι **δεν** καταστέλλετε τα αντικείμενα OLE κατά την αποθήκευση σε PPTX. |

## Επαλήθευση των Αποτελεσμάτων

1. Ανοίξτε το `embeddedFonts.html` σε Chrome/Firefox. Ο πίνακας θα πρέπει να εμφανίζεται χρησιμοποιώντας την ενσωματωμένη γραμματοσειρά (π.χ., Arial) ακόμη και αν αυτή η γραμματοσειρά δεν είναι εγκατεστημένη στον υπολογιστή.  
2. Ανοίξτε το `withVariations.xps` στον Windows XPS Viewer. Τα emoji όπως 👍 πρέπει να εμφανίζονται σωστά.  
3. Ανοίξτε το `oleEditable.pptx` στο PowerPoint. Κάντε διπλό‑κλικ στο σχήμα OLE;

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}