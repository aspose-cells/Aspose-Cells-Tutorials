---
category: general
date: 2026-03-01
description: Αντιγράψτε τον συγκεντρωτικό πίνακα σε Java διατηρώντας τον συγκεντρωτικό,
  στη συνέχεια εξάγετε το Excel σε PPTX, απενεργοποιήστε το AutoFilter του Excel και
  χρησιμοποιήστε το Smart Marker για πίνακες JSON – πλήρης οδηγός βήμα‑προς‑βήμα.
draft: false
keywords:
- copy pivot table
- preserve pivot table
- use smart marker
- disable excel autofilter
- export excel to pptx
language: el
og_description: Αντιγραφή πίνακα Pivot σε Java, διατήρηση του ορισμού του Pivot, εξαγωγή
  σε PPTX, απενεργοποίηση του AutoFilter και χρήση Smart Marker – πλήρης οδηγός για
  προγραμματιστές.
og_title: Αντιγραφή Πίνακα Pivot σε Java – Διατήρηση, Εξαγωγή σε PPTX
tags:
- Aspose.Cells
- Java
- Excel Automation
title: Αντιγραφή Πίνακα Pivot σε Java – Διατήρηση, Εξαγωγή σε PPTX
url: /el/java/excel-pivot-tables/copy-pivot-table-in-java-preserve-it-export-to-pptx/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Αντιγραφή Πίνακα Pivot σε Java – Διατήρηση, Εξαγωγή σε PPTX

Ποτέ χρειάστηκε να **αντιγράψετε πίνακα pivot** από ένα βιβλίο εργασίας σε άλλο χωρίς να χάσετε τον υποκείμενο ορισμό του pivot; Δεν είστε ο μόνος που το σκέφτεται. Σε πολλά πραγματικά έργα θα βρείτε τον εαυτό σας να μετακινεί δεδομένα, και το τελευταίο που θέλετε είναι ένας σπασμένος pivot που πετάει σφάλματα κατά το χρόνο εκτέλεσης.  

Σε αυτό το tutorial θα περάσουμε από μια πλήρη λύση που όχι μόνο **αντιγράφει πίνακα pivot** αλλά επίσης σας δείχνει πώς να **διατηρήσετε τον πίνακα pivot** κατά την αντιγραφή, **εξάγετε Excel σε PPTX**, **απενεργοποιήσετε το Excel AutoFilter**, και **χρησιμοποιήσετε smart marker** για να τοποθετήσετε έναν JSON array σε ένα μόνο κελί. Στο τέλος θα έχετε ένα ενιαίο, εκτελέσιμο πρόγραμμα Java που καλύπτει και τις τέσσερις περιπτώσεις.

## Προαπαιτούμενα

- Java 8 ή νεότερη (ο κώδικας λειτουργεί επίσης με Java 11)  
- Βιβλιοθήκη Aspose.Cells for Java (έκδοση 23.9 ή νεότερη) – μπορείτε να την κατεβάσετε από το Maven Central  
- Βασική εξοικείωση με έννοιες του Excel όπως πίνακες pivot, πίνακες και πλαίσια κειμένου  

Αν λείπει το JAR του Aspose.Cells, προσθέστε το στο `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
</dependency>
```

Τώρα, ας ξεκινήσουμε.

## Βήμα 1: Αντιγραφή Πίνακα Pivot – Διατήρηση του Ορισμού Pivot

Όταν απλώς αντιγράφετε την περιοχή κελιών που περιέχει έναν πίνακα pivot, τα μεταδεδομένα του pivot συχνά μένουν πίσω. Το Aspose.Cells μας παρέχει έναν εύκολο τρόπο να διατηρήσουμε τον ορισμό αμετάβλητο χρησιμοποιώντας `copyRange` με μια παρουσία `CopyOptions`.

```java
import com.aspose.cells.*;

public class PivotCopyDemo {

    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the source workbook that contains the pivot table
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/src.xlsx");
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);

        // 2️⃣ Define the range that includes the pivot (A1:G20 is just an example)
        Range pivotRange = sourceSheet.getCells().createRange("A1:G20");

        // 3️⃣ Prepare the destination workbook
        Workbook destWorkbook = new Workbook();
        Worksheet destSheet = destWorkbook.getWorksheets().get(0);

        // 4️⃣ Copy the range – the pivot definition travels with it
        destSheet.getCells().copyRange(pivotRange,
                new CellArea(0, 0, 19, 6), // destination area (rows 0‑19, cols 0‑6)
                new CopyOptions());

        // 5️⃣ Save the result
        destWorkbook.save("YOUR_DIRECTORY/dest.xlsx");
    }
}
```

**Γιατί λειτουργεί αυτό:** `CopyOptions` λέει στο Aspose.Cells να μεταφέρει τα πάντα, συμπεριλαμβανομένης της κρυφής μνήμης pivot και των ρυθμίσεων πεδίων. Χωρίς αυτό, θα καταλήξετε με απλές τιμές και θα χάσετε τη δυνατότητα ανανέωσης του pivot.

**Edge case:** Αν ο πηγαίος pivot σας εκτείνεται πέρα από το σκληρά κωδικοποιημένο `A1:G20`, προσαρμόστε την περιοχή ανάλογα ή χρησιμοποιήστε `sourceSheet.getPivotTables().get(0).getDataRange()` για να την λάβετε δυναμικά.

![Παράδειγμα αντιγραφής πίνακα pivot](image.png "Αντιγραφή πίνακα pivot σε Java")

*Κείμενο alt εικόνας: διάγραμμα αντιγραφής πίνακα pivot σε Java*

## Βήμα 2: Εξαγωγή Φύλλου Εργασίας με Επεξεργάσιμο Πλαίσιο Κειμένου σε PPTX

Συχνά χρειάζεται να μετατρέψετε ένα φύλλο Excel σε διαφάνεια PowerPoint—σκεφτείτε τα εβδομαδιαία dashboards που πρέπει να παρουσιαστούν. Το Aspose.Cells μπορεί να αποθηκεύσει απευθείας ένα φύλλο εργασίας ως αρχείο PPTX διατηρώντας σχήματα όπως τα πλαίσια κειμένου.

```java
import com.aspose.cells.*;

public class ExportToPptxDemo {

    public static void main(String[] args) throws Exception {
        // Load workbook that contains a TextBox shape
        Workbook wb = new Workbook("YOUR_DIRECTORY/textbox.xlsx");

        // Export the first worksheet to PPTX
        wb.save("YOUR_DIRECTORY/output.pptx", SaveFormat.PPTX);

        System.out.println("Worksheet exported to PPTX successfully.");
    }
}
```

**Τι συμβαίνει:** Η μέθοδος `save` με `SaveFormat.PPTX` μετατρέπει ολόκληρο το φύλλο, συμπεριλαμβανομένου οποιουδήποτε επεξεργάσιμου TextBox, σε διαφάνεια PowerPoint. Το κείμενο μέσα στο πλαίσιο παραμένει επεξεργάσιμο όταν ανοίγετε το PPTX στο PowerPoint.

**Tip:** Αν έχετε πολλά φύλλα και θέλετε μόνο ένα συγκεκριμένο, καλέστε `wb.getWorksheets().removeAt(index)` για τα υπόλοιπα πριν από την αποθήκευση.

## Βήμα 3: Απενεργοποίηση AutoFilter του Excel από Πίνακα

Το AutoFilter είναι χρήσιμο για τους τελικούς χρήστες, αλλά μερικές φορές χρειάζεται να το απενεργοποιήσετε προγραμματιστικά—ίσως πριν από την εξαγωγή δεδομένων ή όταν δημιουργείτε μια καθαρή αναφορά. Δείτε πώς να **απενεργοποιήσετε το excel autofilter** σε έναν πίνακα Excel.

```java
import com.aspose.cells.*;

public class DisableAutoFilterDemo {

    public static void main(String[] args) throws Exception {
        Workbook wb = new Workbook("YOUR_DIRECTORY/textbox.xlsx");
        Worksheet sheet = wb.getWorksheets().get(0);

        // Assume the first table in the sheet is the target
        Table table = sheet.getTables().get(0);

        // Turn off the AutoFilter arrows
        table.setShowAutoFilter(false);

        // Save the modified workbook
        wb.save("YOUR_DIRECTORY/noFilter.xlsx");
        System.out.println("AutoFilter disabled and workbook saved.");
    }
}
```

**Γιατί μπορεί να το χρειαστείτε:** Η εξαγωγή σε μορφές που δεν υποστηρίζουν AutoFilter (όπως CSV ή PDF) μπορεί να εμφανίσει ανεπιθύμητα εικονίδια φίλτρου. Η απενεργοποίησή του εξασφαλίζει καθαρό αποτέλεσμα.

**Κοινό λάθος:** Αν το φύλλο δεν έχει πίνακες, το `getTables().get(0)` θα ρίξει `IndexOutOfBoundsException`. Πάντα ελέγχετε πρώτα το `sheet.getTables().size()` σε κώδικα παραγωγής.

## Βήμα 4: Χρήση Smart Marker – Εισαγωγή JSON Array ως Μονή Τιμή Κελιού

Το Smart Marker είναι η μηχανή προτύπων του Aspose. Ένα χρήσιμο κόλπο είναι να αντιμετωπίζετε ολόκληρο έναν JSON array ως μια μοναδική τιμή κελιού, ιδανικό για logging ή για μεταβίβαση δομημένων δεδομένων. Ας **χρησιμοποιήσουμε smart marker** για να το πετύχουμε.

```java
import com.aspose.cells.*;

public class SmartMarkerDemo {

    public static void main(String[] args) throws Exception {
        Workbook wb = new Workbook("YOUR_DIRECTORY/textbox.xlsx");

        // Initialise the SmartMarker processor with the workbook
        SmartMarkerProcessor processor = new SmartMarkerProcessor(wb);

        // JSON array we want to embed
        String jsonArray = "[{\"Name\":\"John\",\"Age\":30},{\"Name\":\"Anna\",\"Age\":28}]";

        // Configure the processor to treat arrays as a single cell
        processor.setOptions(SmartMarkerOptions.ArrayAsSingle);

        // Apply the marker – assume cell A1 contains the marker ${json}
        processor.apply(jsonArray);

        // Save the result
        wb.save("YOUR_DIRECTORY/smartMarkerResult.xlsx");
        System.out.println("JSON array inserted via Smart Marker.");
    }
}
```

**Πώς λειτουργεί:** Ο δείκτης `${json}` στο βιβλίο εργασίας αντικαθίσταται από ολόκληρη τη συμβολοσειρά JSON επειδή ορίσαμε `ArrayAsSingle`. Χωρίς αυτήν την επιλογή, το Aspose θα προσπαθούσε να επεκτείνει κάθε στοιχείο του array σε ξεχωριστές γραμμές.

**Παραλλαγή:** Αν χρειάζεστε το array να χωριστεί σε γραμμές, απλώς παραλείψτε το `ArrayAsSingle` και αφήστε το Smart Marker να διαχειριστεί αυτόματα την επέκταση.

## Πλήρες Παράδειγμα Εργασίας – Όλα τα Βήματα Συνδυασμένα

Παρακάτω υπάρχει μια μοναδική κλάση Java που ενώνει όλες τις λειτουργίες που καλύψαμε. Εκτελέστε την ως κανονική μέθοδο `main`; απλώς προσαρμόστε τις διαδρομές αρχείων ώστε να ταιριάζουν στο περιβάλλον σας.

```java
import com.aspose.cells.*;

public class CompleteExcelAutomation {

    public static void main(String[] args) throws Exception {
        // ----------- Step 1: Copy Pivot Table -----------
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/src.xlsx");
        Worksheet srcSheet = srcWb.getWorksheets

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}