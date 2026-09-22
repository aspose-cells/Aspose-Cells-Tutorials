---
category: general
date: 2026-03-01
description: Πώς να δημιουργήσετε PDF και να αποθηκεύσετε το βιβλίο εργασίας ως PDF,
  να εξάγετε το Excel σε HTML και να χρησιμοποιήσετε τη λειτουργία expand με το Aspose.Cells
  για Java. Περιλαμβάνεται κώδικας βήμα‑προς‑βήμα.
draft: false
keywords:
- how to create pdf
- save workbook as pdf
- export excel to html
- use expand function
language: el
og_description: Πώς να δημιουργήσετε PDF από ένα βιβλίο εργασίας χρησιμοποιώντας το
  Aspose.Cells για Java. Μάθετε πώς να αποθηκεύσετε το βιβλίο εργασίας ως PDF, να
  εξάγετε το Excel σε HTML και να χρησιμοποιήσετε τη λειτουργία EXPAND.
og_title: Πώς να δημιουργήσετε PDF από ένα βιβλίο εργασίας – Εγχειρίδιο Java
tags:
- Aspose.Cells
- Java
- PDF generation
title: Πώς να δημιουργήσετε PDF από ένα βιβλίο εργασίας – Πλήρης οδηγός Java
url: /el/java/excel-import-export/how-to-create-pdf-from-a-workbook-complete-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να δημιουργήσετε PDF από ένα Workbook – Πλήρης οδηγός Java

Έχετε αναρωτηθεί ποτέ **πώς να δημιουργήσετε PDF** απευθείας από ένα Excel workbook χωρίς να χρησιμοποιείτε τρίτους μετατροπείς; Δεν είστε μόνοι. Πολλοί προγραμματιστές συναντούν δυσκολίες όταν χρειάζονται γρήγορη εξαγωγή PDF, προεπισκόπηση HTML ή εξελιγμένες συναρτήσεις πίνακα — όλα σε ένα.  

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από ένα ενιαίο, αυτόνομο πρόγραμμα Java που κάνει ακριβώς αυτό. Θα **αποθηκεύσουμε το workbook ως PDF**, θα σας δείξουμε πώς να **εξάγετε το Excel σε HTML** διατηρώντας τις παγωμένες γραμμές, και θα επιδείξουμε τη **χρήση της συνάρτησης expand** μέσα σε ένα φύλλο εργασίας. Στο τέλος θα έχετε ένα εκτελέσιμο project που μπορείτε να ενσωματώσετε σε οποιοδήποτε Maven ή Gradle build.

> **Pro tip:** Όλος ο κώδικας παρακάτω λειτουργεί με Aspose.Cells 23.10 (ή νεότερη έκδοση). Αν χρησιμοποιείτε παλαιότερη έκδοση, ορισμένα ονόματα μεθόδων μπορεί να διαφέρουν ελαφρώς.

---

## Προαπαιτήσεις

- **Java 17** (ή οποιαδήποτε LTS έκδοση) εγκατεστημένη και ρυθμισμένη.
- **Aspose.Cells for Java** βιβλιοθήκη. Προσθέστε την παρακάτω εξάρτηση Maven στο `pom.xml` σας:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

- Ένα IDE ή κειμενογράφο της επιλογής σας (IntelliJ IDEA, VS Code, Eclipse…).

Δεν απαιτούνται εξωτερικά APIs, δεν χρειάζονται web services — μόνο καθαρή Java και το Aspose.Cells SDK.

---

## Επισκόπηση της Λύσης

Θα χωρίσουμε την υλοποίηση σε **επτά λογικά βήματα**:

1. Δημιουργία workbook και επίδειξη της **EXPAND** συνάρτησης.  
2. Ενεργοποίηση επιλογέων παραλλαγής γραμματοσειράς και **αποθήκευση του workbook ως PDF**.  
3. Εξαγωγή του ίδιου workbook σε HTML διατηρώντας τις παγωμένες γραμμές.  
4. Χρήση Smart Marker με παράμετρο `IF` για εισαγωγή υπό όρους κειμένου.  
5. Εφαρμογή Smart Marker master‑detail για ιεραρχικά δεδομένα.  
6. Φόρτωση αρχείου Markdown που περιέχει εικόνες κωδικοποιημένες σε Base‑64.  
7. Διαμόρφωση επιλογών GridJs για στοίχιση και περιθώρια, έπειτα εισαγωγή δεδομένων.

Κάθε βήμα είναι ενσωματωμένο σε ξεχωριστή μέθοδο ώστε η μέθοδος `main` να παραμένει καθαρή και για να δείξουμε **γιατί** κάνουμε ό,τι κάνουμε, όχι μόνο **τι** πληκτρολογούμε.

---

## Βήμα 1 – Δημιουργία Workbook και χρήση της συνάρτησης EXPAND

Η **EXPAND** συνάρτηση είναι μια νέα δυναμική‑συνάρτηση πίνακα που εισήχθη στο Office 365. Σας επιτρέπει να «χύσετε» μια περιοχή σε μεγαλύτερο χώρο χωρίς να αντιγράψετε χειροκίνητα τα κελιά.

```java
import com.aspose.cells.*;

public class WorkbookDemo {

    private static void createWorkbookWithExpand() throws Exception {
        // Initialize a new workbook and grab the first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.getWorksheets().get(0);

        // A1 uses EXPAND to turn a 1×3 array into a 5×2 block
        sheet.getCells().get("A1").setFormula("=EXPAND({1,2,3}, 5, 2)");

        // B1 demonstrates a classic trigonometric function (cotangent)
        sheet.getCells().get("B1").setFormula("=COT(PI()/4)");

        // Force calculation so we can read the results immediately
        workbook.calculateFormula();

        // Print the top‑left value to the console – should be 1
        System.out.println("A1 value after EXPAND: " + sheet.getCells().get("A1").getStringValue());
    }
```

**Γιατί είναι σημαντικό:**  
- Η `EXPAND` προσθέτει αυτόματα κενά στη συνέχεια, κάτι που είναι ιδανικό όταν αργότερα **αποθηκεύσετε το workbook ως PDF** — το PDF θα εμφανίζει έναν καθαρό, ορθογώνιο πίνακα.  
- Η κλήση `calculateFormula()` εξασφαλίζει ότι η μηχανή τύπων εκτελείται πριν εξάγουμε οτιδήποτε.

---

## Βήμα 2 – Ενεργοποίηση επιλογέων παραλλαγής γραμματοσειράς και **Αποθήκευση Workbook ως PDF**

Αν χρειάζεται να υποστηρίξετε προχωρημένη τυπογραφία (π.χ. emoji ή επιλογείς παραλλαγής CJK), πρέπει να ενεργοποιήσετε τη δυνατότητα **πριν** την αποθήκευση.

```java
    private static void saveAsPdf(Workbook workbook) throws Exception {
        // Enable support for variation selectors (useful for emojis, etc.)
        WorkbookSettings settings = workbook.getSettings();
        settings.setEnableFontVariationSelectors(true);

        // Define the output path – adjust to your environment
        String pdfPath = "output/vsPdf.pdf";

        // Save the workbook as a PDF file
        workbook.save(pdfPath, SaveFormat.PDF);
        System.out.println("PDF saved to: " + pdfPath);
    }
```

**Κύριο σημείο:** Η κύρια ερώτηση **πώς να δημιουργήσετε pdf** απαντάται εδώ — καλώντας `workbook.save(..., SaveFormat.PDF)` μετά τη διαμόρφωση των ρυθμίσεων.

---

## Βήμα 3 – **Εξαγωγή Excel σε HTML** διατηρώντας τις παγωμένες γραμμές

Συχνά οι ενδιαφερόμενοι ζητούν γρήγορη προεπισκόπηση στο web. Το Aspose.Cells μπορεί να εξάγει σε HTML, και με `setPreserveFrozenRows(true)` διατηρούμε την ίδια εμπειρία κύλισης όπως στο Excel.

```java
    private static void exportToHtml(Workbook workbook) throws Exception {
        HtmlSaveOptions htmlOptions = new HtmlSaveOptions();
        htmlOptions.setPreserveFrozenRows(true); // keep frozen panes

        String htmlPath = "output/frozenRows.html";
        workbook.save(htmlPath, htmlOptions);
        System.out.println("HTML exported to: " + htmlPath);
    }
```

**Γιατί σας ενδιαφέρει:** Οι παγωμένες γραμμές είναι μια ευχάριστη λειτουργία χρηστικότητας· χωρίς αυτές, οι γραμμές κεφαλίδας εξαφανίζονται όταν οι χρήστες κυλούν προς τα κάτω στη σελίδα.

---

## Βήμα 4 – Smart Marker με παράμετρο IF

Τα Smart Markers σας επιτρέπουν να συγχωνεύετε δεδομένα σε ένα πρότυπο χωρίς να γράφετε βρόχους. Η παράμετρος `if` προσθέτει λογική υπό όρους απευθείας μέσα στο marker.

```java
    private static void applyConditionalSmartMarker() throws Exception {
        String template = "${if(@IsVIP, 'VIP Customer', 'Regular Customer')}: ${CustomerName}";
        Map<String, Object> data = new HashMap<>();
        data.put("IsVIP", true);
        data.put("CustomerName", "Acme Corp");

        // Create a fresh workbook to host the result
        Workbook markerWorkbook = new Workbook();
        SmartMarkerProcessor processor = new SmartMarkerProcessor(markerWorkbook);
        processor.apply(template, data);

        // Save to see the result
        markerWorkbook.save("output/conditionalMarker.pdf", SaveFormat.PDF);
    }
```

Το παραγόμενο PDF θα διαβάζει **“VIP Customer: Acme Corp”** επειδή το `IsVIP` είναι `true`. Αλλάξτε τη σημαία σε `false` και θα δείτε **“Regular Customer: Acme Corp”** — χωρίς επιπλέον κώδικα.

---

## Βήμα 5 – Smart Marker Master‑Detail χρησιμοποιώντας ιεραρχική περιοχή

Όταν έχετε δεδομένα γονέα‑παιδίου (π.χ. παραγγελίες και γραμμές παραγγελίας), ένα master‑detail marker σας εξοικονομεί την ανάγκη χειροκίνητης εισαγωγής γραμμών.

```java
    private static void applyMasterDetailSmartMarker() throws Exception {
        // Simulated hierarchical data
        Map<String, Object> hierarchicalData = new HashMap<>();
        List<Map<String, Object>> orders = new ArrayList<>();

        Map<String, Object> order1 = new HashMap<>();
        order1.put("OrderID", 1001);
        order1.put("Date", "2024‑12‑01");
        List<Map<String, Object>> details1 = new ArrayList<>();
        details1.add(Map.of("Product", "Widget A", "Qty", 5));
        details1.add(Map.of("Product", "Widget B", "Qty", 2));
        order1.put("Detail", details1);
        orders.add(order1);

        hierarchicalData.put("Orders", orders);

        String masterDetailTemplate =
                "${Orders.Master:OrderID,Date}\n" +
                "${Orders.Detail:Product,Qty}";

        Workbook mdWorkbook = new Workbook();
        SmartMarkerProcessor mdProcessor = new SmartMarkerProcessor(mdWorkbook);
        mdProcessor.apply(masterDetailTemplate, hierarchicalData);

        mdWorkbook.save("output/masterDetail.pdf", SaveFormat.PDF);
    }
```

**Τι κερδίζετε:** Η μηχανή επεκτείνει τις master γραμμές για κάθε παραγγελία και αυτόματα ενσωματώνει τις detail γραμμές κάτω από αυτές — ιδανικό για τιμολόγια ή αναφορές αγορών.

---

## Βήμα 6 – Φόρτωση εγγράφου Markdown με ενσωματωμένες εικόνες Base‑64

Αν τα δεδομένα προέρχονται από Markdown (συνηθισμένο σε pipelines τεκμηρίωσης), το Aspose.Cells μπορεί να τα αποδώσει απευθείας σε ένα workbook.

```java
    private static void loadMarkdownWithBase64() throws Exception {
        MarkdownLoadOptions mdOptions = new MarkdownLoadOptions();
        mdOptions.setEnableBase64Images(true); // decode inline images

        // Assume doc.md lives in the project root
        Workbook mdWorkbook = new Workbook("input/doc.md", mdOptions);
        mdWorkbook.save("output/markdownExport.pdf", SaveFormat.PDF);
        System.out.println("Markdown loaded and saved as PDF.");
    }
```

**Σημείωση για ειδικές περιπτώσεις:** Αν η συμβολοσειρά Base‑64 είναι κακή, το Aspose θα παραλείψει την εικόνα αλλά θα συνεχίσει την επεξεργασία του υπόλοιπου εγγράφου — χωρίς κατάρρευση.

---

## Βήμα 7 – Διαμόρφωση επιλογών GridJs και εισαγωγή δεδομένων

Το GridJs είναι ένα ελαφρύ JavaScript grid που το Aspose μπορεί να αποδώσει σε HTML. Η στοίχιση αριθμών και η εφαρμογή περιθωρίων βελτιώνουν την αναγνωσιμότητα.

```java
    private static void configureGridJs() throws Exception {
        GridJsOptions gridOptions = new GridJsOptions();
        gridOptions.setNumberFormatAlignment(Alignment.Center); // center numbers
        gridOptions.setNumberFormatBorder(BorderLineStyle.Thin); // thin border

        GridJsEngine gridEngine = new GridJsEngine(gridOptions);
        gridEngine.insertRows(0, 10); // create 10 empty rows
        gridEngine.setCellValue(0, 0, "123"); // first cell gets a value

        // Export the GridJs view to HTML for quick inspection
        String htmlPath = "output/gridJs.html";
        gridEngine.save(htmlPath);
        System.out.println("GridJs HTML saved to: " + htmlPath);
    }
```

**Γιατί μας ενδιαφέρει:** Η σωστή στοίχιση και τα περιθώρια κάνουν το παραγόμενο HTML να μοιάζει με ένα επαγγελματικό spreadsheet — χρήσιμο για dashboards.

---

## Συνένωση όλων – Η μέθοδος `main`

```java
    public static void main(String[] args) {
        try {
            // Step 1 – create workbook with EXPAND
            Workbook workbook = new Workbook();
            Worksheet sheet = workbook.getWorksheets().get(0);
            sheet.getCells().get("A1").setFormula("=EXPAND({1,2,3}, 5, 2)");
            sheet.getCells().get("B1").setFormula("=COT(PI()/4)");
            workbook.calculateFormula();
            System.out.println("A1 after EXPAND: " + sheet.getCells().get("A1").getStringValue());

            // Step 2 – save as PDF
            saveAsPdf(workbook);

            // Step 3 – export to HTML
            exportToHtml(workbook);

            // Step 4 – conditional Smart Marker
            applyConditionalSmartMarker();

            // Step 5 – master‑detail Smart Marker
            applyMasterDetailSmartMarker();

            // Step 6 – load Markdown with Base‑64 images
            loadMarkdownWithBase64();

            // Step 7 – GridJs configuration
            configureGridJs();

            System.out.println("All tasks completed successfully.");
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}