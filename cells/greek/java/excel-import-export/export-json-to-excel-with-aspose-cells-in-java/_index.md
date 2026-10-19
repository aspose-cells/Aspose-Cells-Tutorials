---
category: general
date: 2026-09-18
description: Εξαγωγή JSON σε Excel χρησιμοποιώντας το Aspose.Cells σε Java. Μάθετε
  πώς να εισάγετε JSON στο Excel, να μετατρέψετε JSON σε Excel και να αποθηκεύσετε
  το βιβλίο εργασίας ως XLSX.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export json to excel
- insert json into excel
- how to insert json
- convert json to excel
- save workbook as xlsx
language: el
lastmod: 2026-09-18
og_description: Εξαγωγή JSON σε Excel χρησιμοποιώντας το Aspose.Cells για Java. Ο
  αναλυτικός οδηγός βήμα‑βήμα δείχνει πώς να εισάγετε JSON στο Excel, να μετατρέψετε
  JSON σε Excel και να αποθηκεύσετε το βιβλίο εργασίας ως XLSX.
og_image_alt: Aspose.Cells Java code inserting JSON array into a single Excel cell
og_title: Εξαγωγή JSON σε Excel με το Aspose.Cells – Οδηγός Java
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: Export JSON to Excel using Aspose.Cells in Java. Learn to insert JSON
    into Excel, convert JSON to Excel, and save workbook as XLSX.
  headline: Export JSON to Excel with Aspose.Cells in Java
  type: TechArticle
- description: Export JSON to Excel using Aspose.Cells in Java. Learn to insert JSON
    into Excel, convert JSON to Excel, and save workbook as XLSX.
  name: Export JSON to Excel with Aspose.Cells in Java
  steps:
  - name: Prepare your development environment.
    text: Prepare your development environment.
  - name: Define the JSON data source.
    text: Define the JSON data source.
  - name: Create a workbook and worksheet.
    text: Create a workbook and worksheet.
  - name: Insert JSON into Excel using a Smart Marker.
    text: Insert JSON into Excel using a Smart Marker.
  - name: Process the Smart Marker so the JSON appears in a single cell.
    text: Process the Smart Marker so the JSON appears in a single cell.
  - name: Save the workbook as an XLSX file.
    text: Save the workbook as an XLSX file.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Εξαγωγή JSON σε Excel με το Aspose.Cells σε Java
url: /el/java/excel-import-export/export-json-to-excel-with-aspose-cells-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή JSON σε Excel με το Aspose.Cells σε Java

Αν χρειάζεστε **εξαγωγή JSON σε Excel**, αυτός ο οδηγός παρουσιάζει μια πλήρη λύση χρησιμοποιώντας το Aspose.Cells για Java. Θα δείτε ακριβώς πώς να εισάγετε JSON στο Excel, να μετατρέψετε JSON σε Excel και τελικά **αποθηκεύσετε το βιβλίο εργασίας ως XLSX** χωρίς να αφήσετε το IDE σας.

Η εργασία με δεδομένα JSON είναι συνηθισμένη όταν δημιουργείτε APIs, πίνακες ελέγχου αναφορών ή εργαλεία μεταφοράς δεδομένων. Αντί για χειροκίνητη αντιγραφή‑επικόλληση, η παρακάτω προσέγγιση αυτοματοποιεί ολόκληρη τη διαδικασία ώστε να μπορείτε να δημιουργείτε αρχεία Excel προγραμματιστικά.

## Εξαγωγή JSON σε Excel – βήμα‑βήμα οδηγός

Οι παρακάτω ενότητες σας καθοδηγούν μέσα από κάθε απαιτούμενο βήμα:

1. Προετοιμάστε το περιβάλλον ανάπτυξής σας.  
2. Ορίστε την πηγή δεδομένων JSON.  
3. Δημιουργήστε ένα βιβλίο εργασίας και ένα φύλλο εργασίας.  
4. Εισάγετε JSON στο Excel χρησιμοποιώντας Smart Marker.  
5. Επεξεργαστείτε το Smart Marker ώστε το JSON να εμφανίζεται σε ένα μόνο κελί.  
6. Αποθηκεύστε το βιβλίο εργασίας ως αρχείο XLSX.

Στο τέλος αυτού του οδηγού θα έχετε ένα εκτελέσιμο πρόγραμμα Java που παράγει ένα αρχείο `JsonExport.xlsx` που περιέχει τον πίνακα JSON στο κελί **A1**.

## Προαπαιτούμενα

- Java Development Kit 8 ή νεότερο.  
- Maven ή Gradle για διαχείριση εξαρτήσεων.  
- Aspose.Cells for Java (η τελευταία έκδοση τη στιγμή της συγγραφής, 24.10).  
- Βασικές γνώσεις σύνταξης Java και μορφής JSON.

> **Συμβουλή:** Το Aspose.Cells είναι εμπορική βιβλιοθήκη, αλλά μια δωρεάν άδεια αξιολόγησης λειτουργεί για ανάπτυξη και δοκιμές.

## Βήμα 1: Ρυθμίστε το έργο Java σας

Προσθέστε την εξάρτηση Aspose.Cells στο `pom.xml` (Maven) ή στο `build.gradle` (Gradle).

**Maven**

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version>
</dependency>
```

**Gradle**

```groovy
implementation 'com.aspose:aspose-cells:24.10'
```

Αφού η εξάρτηση λυθεί, μπορείτε να εισάγετε τις απαιτούμενες κλάσεις:

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
import com.aspose.cells.SmartMarkerException;
```

## Βήμα 2: Ορίστε την πηγή δεδομένων JSON

Η συμβολοσειρά JSON αντιπροσωπεύει έναν πίνακα αντικειμένων. Σε ένα πραγματικό έργο μπορεί να διαβάσετε αυτό από αρχείο, από ένα REST endpoint ή από μια βάση δεδομένων. Για παράδειγμα ενσωματώνουμε το JSON απευθείας στον κώδικα.

```java
// Step 2: Define the JSON data source (an array of objects)
String jsonData = "[{\"Name\":\"John\",\"Score\":85},{\"Name\":\"Anna\",\"Score\":92}]";
```

**Γιατί είναι σημαντικό:** Το Aspose.Cells μπορεί να αντιμετωπίσει έναν πίνακα JSON ως ένα μόνο κελί όταν χρησιμοποιείτε την επιλογή `ArrayAsSingle`. Αυτό αποφεύγει την ανάγκη διαχωρισμού του πίνακα σε σειρές και στήλες, κάτι που είναι ιδανικό για εξαγωγή ακατέργαστων φορτίων JSON.

## Βήμα 3: Δημιουργήστε ένα βιβλίο εργασίας και αποκτήστε το πρώτο φύλλο εργασίας

Ένα αντικείμενο `Workbook` αντιπροσωπεύει ολόκληρο το αρχείο Excel. Το πρώτο φύλλο εργασίας (δείκτης 0) είναι όπου θα τοποθετήσουμε το JSON.

```java
// Step 3: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```

**Εξήγηση:** Η δημιουργία ενός `Workbook` χωρίς παραμέτρους δημιουργεί ένα κενό βιβλίο εργασίας με προεπιλεγμένο φύλλο. Μπορείτε αργότερα να προσθέσετε περισσότερα φύλλα εάν το σενάριό σας απαιτεί πολλαπλά σύνολα δεδομένων.

## Βήμα 4: Εισάγετε JSON στο Excel χρησιμοποιώντας Smart Marker

Τα Smart Markers είναι σύμβολα κράτησης θέσης που το Aspose.Cells αντικαθιστά με δεδομένα κατά την εκτέλεση. Το σύμβολο `&=jsonArray(ArrayAsSingle)` λέει στη μηχανή να γράψει ολόκληρο τον πίνακα JSON σε ένα μόνο κελί.

```java
// Step 4: Insert a Smart Marker that tells Aspose.Cells to treat the JSON array as a single cell
worksheet.getCells().putValue(0, 0, "&=jsonArray(ArrayAsSingle)");
```

**Γιατί να χρησιμοποιήσετε Smart Marker;** Αποσπά τη λογική σύνδεσης δεδομένων, επιτρέποντάς σας να εστιάσετε στη μορφή πηγής (JSON) αντί για χαμηλού επιπέδου χειρισμό κελιών.

## Βήμα 5: Συσχετίστε το όνομα του Smart Marker με τα δεδομένα JSON

Πρέπει να συνδέσετε το αναγνωριστικό του marker (`jsonArray`) με την πραγματική συμβολοσειρά JSON.

```java
// Step 5: Associate the Smart Marker name with the JSON data
workbook.getSmartMarkers().setDataSource("jsonArray", jsonData);
```

**Σημείωση:** Η μέθοδος `setDataSource` δέχεται οποιοδήποτε αντικείμενο που η μηχανή Smart Marker μπορεί να σειριοποιήσει, συμπεριλαμβανομένων συμβολοσειρών JSON, συλλογών Java ή DataTables.

## Βήμα 6: Επεξεργαστείτε τα Smart Markers ώστε ο πίνακας JSON να γραφτεί στο κελί

Η κλήση της `processSmartMarkers()` ενεργοποιεί την αντικατάσταση του marker με το συνδεδεμένο JSON.

```java
// Step 6: Process the Smart Markers so the JSON array is written into the cell
workbook.processSmartMarkers();
```

Εάν το JSON είναι κακοδιατυπωμένο, το Aspose.Cells ρίχνει μια `SmartMarkerException`. Τυλίξτε την κλήση σε μπλοκ try‑catch για ανθεκτικότητα επιπέδου παραγωγής.

## Βήμα 7: Αποθηκεύστε το βιβλίο εργασίας ως αρχείο XLSX

Τέλος, γράψτε το βιβλίο εργασίας στο δίσκο. Η επέκταση αρχείου καθορίζει τη μορφή εξόδου· η χρήση `.xlsx` εξασφαλίζει τη σύγχρονη μορφή Office Open XML.

```java
// Step 7: Save the workbook to a file
String outputPath = "YOUR_DIRECTORY/JsonExport.xlsx";
workbook.save(outputPath);
System.out.println("Workbook saved to " + outputPath);
```

**Αποτέλεσμα:** Το άνοιγμα του `JsonExport.xlsx` εμφανίζει τον πίνακα JSON ακριβώς όπως εμφανίζεται στο `jsonData`, τοποθετημένο στο κελί **A1**.

## Πλήρες εκτελέσιμο παράδειγμα

Παρακάτω υπάρχει μια αυτόνομη κλάση Java που μπορείτε να αντιγράψετε, επικολλήσετε και να εκτελέσετε.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
import com.aspose.cells.SmartMarkerException;

/**
 * Demonstrates how to export JSON to Excel using Aspose.Cells.
 * The program inserts a JSON array into a single cell and saves the workbook as XLSX.
 */
public class JsonToExcelExporter {
    public static void main(String[] args) {
        // 1. Define the JSON data source (an array of objects)
        String jsonData = "[{\"Name\":\"John\",\"Score\":85},{\"Name\":\"Anna\",\"Score\":92}]";

        try {
            // 2. Create a new workbook and obtain the first worksheet
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.getWorksheets().get(0);

            // 3. Insert a Smart Marker that treats the JSON array as a single cell
            worksheet.getCells().putValue(0, 0, "&=jsonArray(ArrayAsSingle)");

            // 4. Bind the Smart Marker name to the JSON string
            workbook.getSmartMarkers().setDataSource("jsonArray", jsonData);

            // 5. Process Smart Markers – this writes the JSON into cell A1
            workbook.processSmartMarkers();

            // 6. Save the workbook as an XLSX file
            String outputPath = "JsonExport.xlsx";
            workbook.save(outputPath);
            System.out.println("Workbook saved to " + outputPath);
        } catch (SmartMarkerException e) {
            System.err.println("Error processing Smart Markers: " + e.getMessage());
        } catch (Exception e) {
            System.err.println("Unexpected error: " + e.getMessage());
        }
    }
}
```

### Αναμενόμενη έξοδος

Η εκτέλεση του προγράμματος εκτυπώνει:

```
Workbook saved to JsonExport.xlsx
```

Το άνοιγμα του **JsonExport.xlsx** εμφανίζει το κελί **A1** που περιέχει:

```
[{"Name":"John","Score":85},{"Name":"Anna","Score":92}]
```

## Συνηθισμένες παραλλαγές και ειδικές περιπτώσεις

| Κατάσταση | Πώς να προσαρμόσετε τον κώδικα |
|-----------|------------------------------|
| **Μεγάλο φορτίο JSON** ( > 1 MB) | Αυξήστε το μέγεθος heap της JVM (`-Xmx2g`) για να αποφύγετε το `OutOfMemoryError`. |
| **Πολλαπλά αντικείμενα JSON** που απαιτούν ξεχωριστές σειρές | Χρησιμοποιήστε `ArrayAsRows` αντί για `ArrayAsSingle` και αντιστοιχίστε το marker σε μια συλλογή POJO. |
| **Αποθήκευση σε CSV** | Αντικαταστήστε το `workbook.save(outputPath)` με `workbook.save(outputPath, com.aspose.cells.SaveFormat.CSV);`. |
| **Προσθήκη γραμμής κεφαλίδας** | Γράψτε μια στατική συμβολοσειρά στο `worksheet.getCells().putValue(0, 0, "JSON Payload");` πριν την εισαγωγή του Smart Marker. |
| **Χρήση διαφορετικού καταλόγου** | Βεβαιωθείτε ότι ο κατάλογος υπάρχει ή δημιουργήστε τον με `new java.io.File(dir).mkdirs();`. |

## Συμβουλές για χρήση σε παραγωγή

- **Επικυρώστε το JSON** πριν το περάσετε στο Aspose.Cells για να αποτρέψετε εξαιρέσεις χρόνου εκτέλεσης.  
- **Χρησιμοποιήστε try‑with‑resources** για οποιαδήποτε ροή ανοίγετε όταν διαβάζετε JSON από εξωτερικές πηγές.  
- **Κλειδώστε το βιβλίο εργασίας** εάν πολλαπλά νήματα μπορεί να γράψουν στο ίδιο αρχείο ταυτόχρονα.  
- **Καταχώρηση άδειας**: καλέστε `com.aspose.cells.License license = new com.aspose.cells.License(); license.setLicense("Aspose.Cells.lic");` κατά την εκκίνηση της εφαρμογής.

## Επόμενα βήματα

Τώρα που μπορείτε **να εξάγετε JSON σε Excel**, εξετάστε την εξερεύνηση σχετικών δυνατοτήτων:

- **Εισαγωγή JSON στο Excel** με μορφοποίηση: εφαρμόστε στυλ κελιών μετά την επεξεργασία του Smart Marker.  
- **Μετατροπή JSON σε πίνακες Excel**: αντιστοιχίστε αντικείμενα JSON σε σειρές και στήλες

## Τι Θα Πρέπει Να Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που βασίζονται στις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Εισαγωγή Δεδομένων JSON σε Excel Χρησιμοποιώντας Aspose.Cells Java: Ένας Πλήρης Οδηγός](/cells/english/java/import-export/import-json-data-excel-aspose-cells-java/)
- [Πώς να Εισάγετε Πολλαπλές Γραμμές σε Excel Χρησιμοποιώντας Aspose.Cells για Java](/cells/english/java/cell-operations/excel-automation-aspose-cells-java-insert-multiple-rows/)
- [Πώς να Εισάγετε Εικόνες σε Excel Χρησιμοποιώντας Java και Aspose.Cells](/cells/english/java/images-shapes/insert-image-into-excel-java-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}