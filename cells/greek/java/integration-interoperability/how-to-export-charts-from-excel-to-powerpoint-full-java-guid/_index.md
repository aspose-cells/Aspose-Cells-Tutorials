---
category: general
date: 2026-06-27
description: Πώς να εξάγετε γραφήματα από το Excel στο PowerPoint χρησιμοποιώντας
  Java. Μάθετε πώς να μετατρέψετε το λογιστικό φύλλο σε PowerPoint, να αποθηκεύετε
  αρχεία PPTX και να εξάγετε δεδομένα Excel σε PPT χωρίς κόπο.
draft: false
keywords:
- how to export charts
- convert spreadsheet to powerpoint
- how to save pptx
- excel to powerpoint slide
- export excel data ppt
language: el
og_description: Πώς να εξάγετε γραφήματα από το Excel στο PowerPoint με Java. Αυτός
  ο οδηγός βήμα‑βήμα σας δείχνει πώς να μετατρέψετε ένα φύλλο εργασίας σε PowerPoint,
  να αποθηκεύσετε αρχεία PPTX και να εξάγετε δεδομένα Excel σε PPT.
og_title: Πώς να εξάγετε διαγράμματα από το Excel στο PowerPoint – Java Tutorial
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: How to export charts from Excel to PowerPoint using Java. Learn to
    convert spreadsheet to PowerPoint, save PPTX files, and export Excel data PPT
    effortlessly.
  headline: How to Export Charts from Excel to PowerPoint – Full Java Guide
  type: TechArticle
- description: How to export charts from Excel to PowerPoint using Java. Learn to
    convert spreadsheet to PowerPoint, save PPTX files, and export Excel data PPT
    effortlessly.
  name: How to Export Charts from Excel to PowerPoint – Full Java Guide
  steps:
  - name: '**Load** the workbook you want to transform.'
    text: '**Load** the workbook you want to transform.'
  - name: '**Configure** a `PresentationOptions` instance to tell Aspose which elements
      (charts, OLE objects, etc.) should make it into the slide deck.'
    text: '**Configure** a `PresentationOptions` instance to tell Aspose which elements
      (charts, OLE objects, etc.) should make it into the slide deck.'
  - name: '**Save** the workbook using the `PPTX` format and the options you configured.'
    text: '**Save** the workbook using the `PPTX` format and the options you configured.'
  type: HowTo
tags:
- Java
- Aspose.Cells
- Excel
- PowerPoint
title: Πώς να εξάγετε διαγράμματα από το Excel στο PowerPoint – Πλήρης οδηγός Java
url: /el/java/integration-interoperability/how-to-export-charts-from-excel-to-powerpoint-full-java-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Εξάγετε Διαγράμματα από το Excel στο PowerPoint – Πλήρης Οδηγός Java

Έχετε αναρωτηθεί ποτέ **πώς να εξάγετε διαγράμματα** από ένα βιβλίο εργασίας του Excel απευθείας σε μια διαφάνεια του PowerPoint; Δεν είστε οι μόνοι—οι προγραμματιστές συχνά χρειάζονται να μετατρέψουν τα δεδομένα‑οδηγούμενα υπολογιστικά φύλλα σε παρουσιάσεις έτοιμες για προβολή χωρίς το εφιάλτη της χειροκίνητης αντιγραφής‑επικόλλησης. Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από μια καθαρή, προγραμματιστική λύση που σας επιτρέπει να **μετατρέψετε το spreadsheet σε PowerPoint**, να αποθηκεύσετε το αποτέλεσμα ως PPTX και ακόμη να ρυθμίσετε λεπτομερώς τη διαχείριση των διαγραμμάτων σε πραγματικό χρόνο.

Αυτό που θα έχετε στο τέλος είναι ένα έτοιμο‑για‑εκτέλεση Java snippet που παίρνει οποιοδήποτε βιβλίο εργασίας, εξάγει τα διαγράμματά του (και τα OLE objects αν το θέλετε), και δημιουργεί ένα επαγγελματικό αρχείο **excel to powerpoint slide**. Χωρίς επιπλέον UI, χωρίς περίπλοκο VBA, μόνο καθαρός κώδικας Java που μπορείτε να ενσωματώσετε στο πρόγραμμά σας σήμερα.

## Προαπαιτούμενα

- **Java 17** ή νεότερη (το API λειτουργεί σε οποιοδήποτε πρόσφατο JDK)
- **Aspose.Cells for Java** βιβλιοθήκη (ο κώδικας χρησιμοποιεί `PresentationOptions` και `SaveFormat.PPTX`)
- Βασική κατανόηση της ρύθμισης έργου Java (Maven/Gradle)
- Ένα αρχείο Excel (`.xlsx`) που περιέχει τουλάχιστον ένα διάγραμμα που θέλετε να εξάγετε

Αν λείπει το JAR του Aspose.Cells, προσθέστε το μέσω Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- check for the latest version -->
</dependency>
```

Ή κατεβάστε το JAR απευθείας από τον ιστότοπο της Aspose και τοποθετήστε το στο classpath σας.

## Πώς να Εξάγετε Διαγράμματα – Επισκόπηση

Σε υψηλό επίπεδο η διαδικασία είναι:

1. **Φορτώστε** το βιβλίο εργασίας που θέλετε να μετατρέψετε.
2. **Διαμορφώστε** μια παρουσίαση `PresentationOptions` ώστε να πείτε στο Aspose ποια στοιχεία (διαγράμματα, OLE objects κ.λπ.) πρέπει να συμπεριληφθούν στην παρουσίαση.
3. **Αποθηκεύστε** το βιβλίο εργασίας χρησιμοποιώντας τη μορφή `PPTX` και τις επιλογές που διαμορφώσατε.

Αυτό είναι όλο. Η βιβλιοθήκη κάνει τη σκληρή δουλειά—αποδίδει κάθε διάγραμμα ως διανυσματικό γραφικό, διατηρεί τη διάταξη και δημιουργεί ένα αρχείο PowerPoint που το ίδιο το PowerPoint μπορεί να ανοίξει χωρίς προβλήματα.

Παρακάτω θα αναλύσουμε κάθε βήμα, θα εξηγήσουμε *γιατί* είναι σημαντικό και θα δείξουμε τον ακριβή κώδικα που χρειάζεστε.

## Βήμα 1: Φορτώστε το Βιβλίο Εργασίας και Διαμορφώστε τις Επιλογές Εξαγωγής

Πρώτα, πρέπει να πούμε στο Aspose τι να συμπεριλάβει όταν δημιουργεί το PowerPoint. Η κλάση `PresentationOptions` μας δίνει λεπτομερή έλεγχο. Η ρύθμιση `setExportCharts(true)` εξασφαλίζει ότι κάθε διάγραμμα γίνεται στοιχείο διαφάνειας, ενώ το `setExportOleObjects(true)` προσθέτει τυχόν ενσωματωμένα αντικείμενα (όπως πίνακες Excel) που μπορεί να έχετε.

```java
import com.aspose.cells.*;

public class ExcelToPowerPointExporter {

    public static void main(String[] args) throws Exception {
        // -------------------------------------------------
        // 1️⃣ Load the source Excel workbook
        // -------------------------------------------------
        String srcPath = "C:/data/sourceWorkbook.xlsx";
        Workbook workbook = new Workbook(srcPath);

        // -------------------------------------------------
        // 2️⃣ Configure presentation export options
        // -------------------------------------------------
        PresentationOptions presentationOptions = new PresentationOptions();
        presentationOptions.setExportCharts(true);          // <-- how to export charts
        presentationOptions.setExportOleObjects(true);     // include embedded OLE objects

        // The next lines are optional but often useful:
        presentationOptions.setExportFormulas(false);      // skip raw formulas if you only need visuals
        presentationOptions.setExportImages(true);         // grab any pictures as well
```

**Γιατί αυτό το βήμα είναι σημαντικό:**  
Αν παραλείψετε το `setExportCharts(true)`, το Aspose θα αντιμετωπίσει τα διαγράμματα σαν κανονικά κελιά, ρίχνοντας τα δεδομένα τους στη διαφάνεια αντί για ένα οπτικό διάγραμμα. Αυτό αντιτίθεται στον σκοπό μιας παρουσίασης. Ομοίως, η ενεργοποίηση της εξαγωγής OLE σας επιτρέπει να διατηρήσετε σύνθετα αντικείμενα (όπως πίνακες pivot) χωρίς επιπλέον κώδικα.

> **Συμβουλή:** Όταν εργάζεστε με τεράστια βιβλία εργασίας, σκεφτείτε να απενεργοποιήσετε το `setExportFormulas` για να επιταχύνετε τη μετατροπή. Η οπτική έξοδος παραμένει η ίδια, αλλά η διαδικασία είναι πιο ελαφριά στη μνήμη.

## Βήμα 2: Αποθηκεύστε το Βιβλίο Εργασίας ως Αρχείο PowerPoint

Τώρα που οι επιλογές είναι έτοιμες, η πραγματική μετατροπή είναι μια μόνο γραμμή: καλέστε `workbook.save(...)` με το enum `SaveFormat.PPTX`. Αυτό είναι το τμήμα όπου απαντάμε στο **πώς να αποθηκεύσετε pptx** σε Java.

```java
        // -------------------------------------------------
        // 3️⃣ Save the workbook as a PowerPoint file
        // -------------------------------------------------
        String outPath = "C:/output/slide.pptx";
        workbook.save(outPath, SaveFormat.PPTX, presentationOptions);

        System.out.println("✅ Conversion complete! Check " + outPath);
    }
}
```

**Τι συμβαίνει στο παρασκήνιο;**  
Το Aspose διασχίζει κάθε φύλλο εργασίας, εξάγει κάθε διάγραμμα, το μετατρέπει σε σχήμα PowerPoint (συνήθως ένα διανυσματικό EMF) και το τοποθετεί σε νέα διαφάνεια. Αν έχετε πολλά φύλλα, το καθένα παίρνει τη δική του διαφάνεια από προεπιλογή. Μπορείτε αργότερα να αναδιατάξετε τις διαφάνειες χρησιμοποιώντας το Apache POI ή το ίδιο το PowerPoint.

### Αναμενόμενο Αποτέλεσμα

Ανοίξτε το `slide.pptx` στο Microsoft PowerPoint και θα πρέπει να δείτε:

- Μία διαφάνεια ανά φύλλο εργασίας (ή ανά διάγραμμα, ανάλογα με την πηγή σας)
- Διαγράμματα εμφανιζόμενα καθαρά, διατηρώντας χρώματα και ετικέτες δεδομένων
- Οποιαδήποτε OLE objects (όπως ενσωματωμένοι πίνακες Excel) να εμφανίζονται ως επεξεργάσιμα αντικείμενα

Αν δεν δείτε διάγραμμα, ελέγξτε ξανά ότι το πηγαίο βιβλίο εργασίας περιέχει πραγματικά ένα αντικείμενο διαγράμματος και ότι το `setExportCharts(true)` δεν έχει αντικατασταθεί κάπου αλλού.

## Εναλλακτικό: Εξαγωγή Μονού Διαγράμματος σε Αυτόνομο PPTX

Μερικές φορές χρειάζεστε μόνο **excel to powerpoint slide** για ένα συγκεκριμένο διάγραμμα, όχι ολόκληρο το βιβλίο εργασίας. Μπορείτε να το πετύχετε δημιουργώντας ένα προσωρινό βιβλίο εργασίας που περιέχει μόνο το διάγραμμα που σας ενδιαφέρει.

```java
        // -------------------------------------------------
        // 4️⃣ Export a single chart (optional)
        // -------------------------------------------------
        // Assume the chart is on the first worksheet, first chart
        Worksheet sheet = workbook.getWorksheets().get(0);
        int chartIndex = 0; // change if you have multiple charts
        Chart chart = sheet.getCharts().get(chartIndex);

        // Clone the chart into a new workbook
        Workbook singleChartWb = new Workbook();
        Worksheet newSheet = singleChartWb.getWorksheets().get(0);
        newSheet.getCharts().addCopy(chart);

        // Use the same PresentationOptions
        singleChartWb.save("C:/output/singleChart.pptx", SaveFormat.PPTX, presentationOptions);
```

**Γιατί μπορεί να το θέλετε:**  
Αν δημιουργείτε μια παρουσίαση εν κινήσει (π.χ., μια υπηρεσία αναφοράς που στέλνει ένα διάγραμμα ανά email), η δημιουργία ενός ελάχιστου βιβλίου εργασίας μειώνει τη χρήση μνήμης και επιταχύνει τη λειτουργία.

## Συνηθισμένα Προβλήματα & Πώς να τα Αποφύγετε

| Πρόβλημα | Σύμπτωμα | Διόρθωση |
|----------|----------|----------|
| Διαγράμματα εξαφανίζονται | Οι διαφάνειες είναι κενές ή περιέχουν μόνο πίνακες δεδομένων | Βεβαιωθείτε ότι το `presentationOptions.setExportCharts(true)` καλείται **πριν** το `workbook.save`. |
| Μεγάλο μέγεθος αρχείου | PPTX > 30 MB για λίγα διαγράμματα | Απενεργοποιήστε την εξαγωγή εικόνων (`setExportImages(false)`) ή συμπιέστε τις εικόνες στο PowerPoint μετά τη δημιουργία. |
| Απουσία OLE objects | Οι ενσωματωμένοι πίνακες Excel μετατρέπονται σε στατικές εικόνες | Ορίστε `setExportOleObjects(true)`· επίσης ελέγξτε ότι τα πηγαία OLE objects δεν είναι προστατευμένα. |
| Σφάλμα συμβατότητας | Το PowerPoint αναφέρει ότι το αρχείο είναι κατεστραμμένο | Χρησιμοποιήστε την πιο πρόσφατη έκδοση του Aspose.Cells· παλαιότερες εκδόσεις μπορεί να έχουν σφάλματα με τη δημιουργία PPTX. |

## Πώς να Εξάγετε Διαγράμματα σε CI/CD Pipeline

Αν αυτοματοποιείτε τη δημιουργία αναφορών ως μέρος μιας κατασκευής, μπορείτε να ενσωματώσετε τον παραπάνω κώδικα σε ένα Maven plugin ή σε ένα Gradle task. Απλώς βεβαιωθείτε ότι η JVM έχει αρκετό heap (π.χ., `-Xmx2g`) όταν επεξεργάζεται τεράστια βιβλία εργασίας.

```groovy
task exportCharts(type: JavaExec) {
    classpath = sourceSets.main.runtimeClasspath
    main = 'com.example.ExcelToPowerPointExporter'
    args = []
    jvmArgs = ['-Xmx2g']
}
```

Η εκτέλεση του `./gradlew exportCharts` θα παραγάγει το PPTX χωρίς καμία χειροκίνητη παρέμβαση—ιδανικό για εργασίες αναφοράς νυχτερινής εκτέλεσης.

## Πλήρες Παράδειγμα Εργασίας (Έτοιμο για Αντιγραφή‑Επικόλληση)

Παρακάτω είναι η πλήρης, αυτόνομη κλάση Java που μπορείτε να ενσωματώσετε σε οποιοδήποτε IDE. Περιλαμβάνει όλες τις εισαγωγές, τη διαχείριση σφαλμάτων και σχόλια που εξηγούν κάθε γραμμή.

```java
// FullExample.java
import com.aspose.cells.*;

public class FullExample {
    public static void main(String[] args) {
        try {
            // 👉 1️⃣ Load the Excel workbook you want to convert
            String srcFile = "C:/data/analysis.xlsx";
            Workbook wb = new Workbook(srcFile);

            // 👉 2️⃣ Set up export options – this is the core of how to export charts
            PresentationOptions opts = new PresentationOptions();
            opts.setExportCharts(true);          // include every chart
            opts.setExportOleObjects(true);     // keep OLE objects (tables, etc.)
            opts.setExportImages(true);         // optionally keep pictures
            opts.setExportFormulas(false);      // skip formulas for speed

            // 👉 3️⃣ Choose where the PPTX will be saved – answer to how to save pptx
            String outFile = "C:/output/analysis.pptx";

            // 👉 4️⃣ Perform the conversion
            wb.save(outFile, SaveFormat.PPTX, opts);

            System.out.println("✅ Excel file converted to PowerPoint successfully!");
        } catch (Exception e) {
            System.err.println("❌ Conversion failed: " + e.getMessage());
            e.printStackTrace();
        }
    }
}
```

Εκτελέστε την κλάση, ανοίξτε το `analysis.pptx` και θα δείτε κάθε διάγραμμα από το αρχικό σας υπολογιστικό φύλλο να ζει ευτυχισμένα μέσα σε μια παρουσίαση PowerPoint. Αυτή είναι η ουσία του **export excel data ppt**—χωρίς χειροκίνητα βήματα, χωρίς σφάλματα αντιγραφής‑επικόλλησης.

## Οπτική Σύνοψη

![Διάγραμμα που δείχνει πώς να εξάγετε διαγράμματα από το Excel στο PowerPoint χρησιμοποιώντας Aspose.Cells](/images/export-charts-diagram.png "Πώς να εξάγετε διαγράμματα από το Excel στο PowerPoint")

*Η παραπάνω εικονογράφηση απεικονίζει τη ροή από ένα βιβλίο εργασίας Excel → PresentationOptions → αρχείο PPTX.*

## Συμπέρασμα

Καλύψαμε **πώς να εξάγετε διαγράμματα** από το Excel στο PowerPoint χρησιμοποιώντας Java, παρουσιάσαμε τον ακριβή κώδικα που χρειάζεστε για **convert spreadsheet to PowerPoint**, και εξηγήσαμε **πώς να αποθηκεύσετε αρχεία pptx** αξιόπιστα. Με την τροποποίηση του `PresentationOptions` μπορείτε να ελέγξετε τα πάντα, από την ένταξη διαγραμμάτων μέχρι τη διαχείριση OLE objects, παρέχοντας μια ευέλικτη γέφυρα μεταξύ ανάλυσης δεδομένων και επιπέδων παρουσίασης.

Επόμενα βήματα; Δοκιμάστε να συνδυάσετε αυτή τη μετατροπή με **Apache POI** για προγραμματιστική αναδιάταξη των διαφανειών, ή ενσωματώστε τη ρουτίνα σε μια μικροϋπηρεσία Spring Boot που παρέχει αναφορές PPTX κατόπιν ζήτησης. Μπορείτε επίσης να εξερευνήσετε την εξαγωγή σε **PDF** ή **HTML** χρησιμοποιώντας την ίδια βιβλιοθήκη—το Aspose.Cells το κάνει απλό.

Έχετε ερωτήσεις σχετικά με ειδικές περιπτώσεις,

## Τι Θα Πρέπει Να Μάθετε Στη Σύντομη Μελλοντική

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να Δημιουργήσετε και να Εξάγετε Διαγράμματα σε Java Χρησιμοποιώντας Aspose.Cells: Πλήρης Οδηγός](/cells/english/java/charts-graphs/aspose-cells-java-create-export-charts/)
- [Πώς να Εξάγετε Διαγράμματα Excel ως SVG Χρησιμοποιώντας Aspose.Cells Java για Κλιμακώσιμα Διανυσματικά Γραφικά](/cells/english/java/charts-graphs/export-excel-charts-svg-aspose-cells-java/)
- [Εξαγωγή Διαγραμμάτων Excel σε PDF Χρησιμοποιώντας Aspose.Cells για Java: Οδηγός Προσαρμοσμένων Μεγεθών Σελίδας](/cells/english/java/charts-graphs/export-excel-charts-pdf-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}