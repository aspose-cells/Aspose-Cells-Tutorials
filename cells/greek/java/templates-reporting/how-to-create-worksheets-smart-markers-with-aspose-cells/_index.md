---
category: general
date: 2026-08-20
description: Δημιουργήστε έξυπνους δείκτες σε φύλλα εργασίας σε Java χρησιμοποιώντας
  το Aspose.Cells και ελέγξτε την ονομασία των φύλλων λεπτομερειών με το SmartMarkerOptions.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create worksheets smart markers
- Aspose.Cells Java
- smart marker options
- duplicate sheet names
- detail sheet naming
language: el
lastmod: 2026-08-20
og_description: Δημιουργήστε smart markers φύλλων εργασίας σε Java με το Aspose.Cells.
  Μάθετε πώς να ονομάζετε δυναμικά τα φύλλα λεπτομερειών χρησιμοποιώντας το SmartMarkerOptions.
og_image_alt: create worksheets smart markers example diagram
og_title: Δημιουργία έξυπνων δεικτών σε φύλλα εργασίας – Οδηγός Java με το Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Create worksheets smart markers in Java using Aspose.Cells and control
    detail sheet naming with SmartMarkerOptions.
  headline: How to create worksheets smart markers with Aspose.Cells
  type: TechArticle
- description: Create worksheets smart markers in Java using Aspose.Cells and control
    detail sheet naming with SmartMarkerOptions.
  name: How to create worksheets smart markers with Aspose.Cells
  steps:
  - name: Set up the Maven project and add Aspose.Cells
    text: 'Create a new Maven module (or Gradle project) and add the Aspose.Cells
      dependency:'
  - name: Load the master workbook that contains smart markers
    text: '```java import com.aspose.cells.*;'
  - name: Configure SmartMarkerOptions for custom detail sheet names
    text: '```java // Define naming pattern for detail sheets. SmartMarkerOptions
      smartMarkerOptions = new SmartMarkerOptions(); // {0} is automatically replaced
      by the row index (starting at 1). smartMarkerOptions.setDetailSheetNewName("DetailSheet_{0}");
      ```'
  - name: Build a DataTable that matches the smart marker fields
    text: '```java // Build a simple DataTable with two columns. DataTable data =
      new DataTable(); data.getColumns().add("Id", DataType.INTEGER); data.getColumns().add("Value",
      DataType.STRING); // Add sample rows. data.getRows().add(new Object[] { 1, "A"
      }); data.getRows().add(new Object[] { 2, "B" }); ```'
  - name: Apply the data to the smart markers with the naming options
    text: '```java // Apply the data to the first worksheet (index 0). workbook.getWorksheets().get(0).getSmartMarkers().apply(data,
      smartMarkerOptions); ```'
  - name: Save the workbook and verify the result
    text: '```java // Save the expanded workbook. workbook.save("YOUR_DIRECTORY/MasterDetailDuplicatedNames.xlsx");
      } } ```'
  - name: Multiple master sheets
    text: 'If your template contains more than one master sheet, iterate over each
      sheet’s smart markers:'
  - name: Custom naming beyond the row index
    text: 'You can embed any data column into the sheet name by using placeholders
      like `{ColumnName}`:'
  - name: Preventing overly long sheet names
    text: 'Excel limits sheet names to 31 characters. If your naming pattern risks
      exceeding this limit, truncate or hash the value:'
  type: HowTo
tags:
- Java
- Aspose.Cells
- Smart Markers
- Excel Automation
title: Πώς να δημιουργήσετε έξυπνους δείκτες φύλλων εργασίας με το Aspose.Cells
url: /el/java/templates-reporting/how-to-create-worksheets-smart-markers-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να δημιουργήσετε smart markers φύλλων εργασίας με το Aspose.Cells

Αν χρειάζεστε **να δημιουργήσετε smart markers φύλλων εργασίας** σε ένα βιβλίο εργασίας Java, αυτός ο οδηγός σας δείχνει τα ακριβή βήματα για να το κάνετε με το Aspose.Cells. Θα δείτε πώς να ρυθμίσετε το `SmartMarkerOptions` ώστε κάθε φύλλο λεπτομερειών να λαμβάνει ένα μοναδικό, προβλέψιμο όνομα.

Η δημιουργία αναφορών Excel που επεκτείνουν ένα master‑detail πρότυπο είναι κοινή απαίτηση σε χρηματοοικονομικά, αποθέματα και συστήματα αναφορών. Η χρήση smart markers εξαλείφει την χειροκίνητη αντιγραφή φύλλων και σας επιτρέπει να εστιάσετε στα δεδομένα αντί στην υποδομή.

## Τι θα μάθετε

* Πώς να φορτώσετε ένα κύριο βιβλίο εργασίας που περιέχει smart markers.  
* Πώς να ορίσετε το `SmartMarkerOptions` για να ελέγξετε την ονομασία των παραγόμενων φύλλων λεπτομερειών.  
* Πώς να παρέχετε ένα `DataTable` με δείγμα δεδομένων και να το εφαρμόσετε στα smart markers.  
* Πώς να αποθηκεύσετε το αποτέλεσμα ώστε κάθε φύλλο λεπτομερειών να έχει διαφορετικό όνομα, αποφεύγοντας διπλότυπα ονόματα φύλλων.

**Προαπαιτούμενα**  
* Java 17 ή νεότερη (ο κώδικας συντάσσεται επίσης με JDK 8+).  
* Aspose.Cells for Java 23.9 ή νεότερη – η βιβλιοθήκη παρέχει τις κλάσεις `Workbook`, `SmartMarkerOptions` και σχετικές.  
* Ένα IDE όπως IntelliJ IDEA, Eclipse ή VS Code.

Δευτερεύοντες όροι που θα συναντήσετε περιλαμβάνουν **Aspose.Cells Java**, **smart marker options**, και τη διαχείριση **duplicate sheet names** όταν το πρότυπο επεκτείνεται.

## Δημιουργία smart markers φύλλων εργασίας – οδηγός βήμα‑βήμα

Οι παρακάτω ενότητες χωρίζουν τη διαδικασία σε διακριτά, επαναχρησιμοποιήσιμα βήματα. Κάθε βήμα περιλαμβάνει ένα απόσπασμα κώδικα, εξήγηση του γιατί είναι σημαντικό και πρακτικές συμβουλές για την αποφυγή κοινών παγίδων.

### Βήμα 1: Ρυθμίστε το έργο Maven και προσθέστε το Aspose.Cells

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
</dependency>
```

**Γιατί είναι σημαντικό αυτό το βήμα** – Η βιβλιοθήκη παρέχει την κλάση `Workbook` που διαβάζει και γράφει αρχεία Excel, καθώς και τη μηχανή smart‑marker που επεκτείνει αυτόματα το πρότυπό σας. Χωρίς τη σωστή εξάρτηση, ο μεταγλωττιστής δεν μπορεί να εντοπίσει τις κλήσεις API που χρησιμοποιούνται αργότερα.

> **Συμβουλή:** Εάν εργάζεστε πίσω από εταιρικό proxy, ρυθμίστε το `settings.xml` του Maven για να κατεβάσετε το αποθετήριο Aspose με ασφάλεια.

### Βήμα 2: Φορτώστε το κύριο βιβλίο εργασίας που περιέχει smart markers

```java
import com.aspose.cells.*;

public class DuplicateDetailSheetNames {
    public static void main(String[] args) throws Exception {
        // Load the template that holds the smart marker tags.
        Workbook workbook = new Workbook("YOUR_DIRECTORY/MasterDetailTemplate.xlsx");
```

**Γιατί είναι σημαντικό αυτό το βήμα** – Το κύριο βιβλίο εργασίας ορίζει τη διάταξη, τους τύπους και τις ετικέτες placeholder (`«SmartMarker»`) που η μηχανή θα αντικαταστήσει. Η φόρτωση του αρχείου μία φορά διατηρεί τη χρήση μνήμης χαμηλή και σας επιτρέπει να επαναχρησιμοποιήσετε το ίδιο βιβλίο εργασίας για πολλαπλά σύνολα δεδομένων.

### Βήμα 3: Ρυθμίστε το SmartMarkerOptions για προσαρμοσμένα ονόματα φύλλων λεπτομερειών

```java
        // Define naming pattern for detail sheets.
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions();
        // {0} is automatically replaced by the row index (starting at 1).
        smartMarkerOptions.setDetailSheetNewName("DetailSheet_{0}");
```

**Γιατί είναι σημαντικό αυτό το βήμα** – Από προεπιλογή, το Aspose.Cells δημιουργεί φύλλα λεπτομερειών με γενικά ονόματα όπως “DetailSheet”. Όταν το πρότυπο επεκτείνεται για πολλές γραμμές, αυτά τα ονόματα συγκρούονται, οδηγώντας σε **duplicate sheet names** και εξαίρεση χρόνου εκτέλεσης. Το μοτίβο `"DetailSheet_{0}"` εγγυάται ένα μοναδικό όνομα ανά γραμμή, λύνοντας το πρόβλημα των διπλότυπων.

### Βήμα 4: Δημιουργήστε ένα DataTable που ταιριάζει με τα πεδία των smart markers

```java
        // Build a simple DataTable with two columns.
        DataTable data = new DataTable();
        data.getColumns().add("Id", DataType.INTEGER);
        data.getColumns().add("Value", DataType.STRING);
        // Add sample rows.
        data.getRows().add(new Object[] { 1, "A" });
        data.getRows().add(new Object[] { 2, "B" });
```

**Γιατί είναι σημαντικό αυτό το βήμα** – Το `DataTable` παρέχει τις πραγματικές τιμές που αντικαθιστούν τα placeholders των smart markers. Τα ονόματα των στηλών πρέπει να ταιριάζουν με τα ονόματα των markers στο πρότυπο· διαφορετικά η μηχανή παραλείπει την αντικατάσταση σιωπηρά.

> **Συνηθισμένο λάθος:** Η χρήση ονόματος στήλης που διαφέρει κατά πεζά/κεφαλαία (π.χ., “id” vs “Id”) οδηγεί σε ελλιπή δεδομένα στα παραγόμενα φύλλα.

### Βήμα 5: Εφαρμόστε τα δεδομένα στα smart markers με τις επιλογές ονομασίας

```java
        // Apply the data to the first worksheet (index 0).
        workbook.getWorksheets().get(0).getSmartMarkers().apply(data, smartMarkerOptions);
```

**Γιατί είναι σημαντικό αυτό το βήμα** – Η μέθοδος `apply` ενεργοποιεί τη μηχανή smart‑marker. Διαβάζει κάθε γραμμή, δημιουργεί ένα νέο φύλλο λεπτομερειών χρησιμοποιώντας το μοτίβο ονομασίας από το `SmartMarkerOptions`, και γεμίζει το φύλλο με τα δεδομένα της γραμμής. Αυτή η ενιαία κλήση αντικαθιστά δεκάδες γραμμές χειροκίνητης κλωνοποίησης φύλλων και γεμίσματος κελιών.

### Βήμα 6: Αποθηκεύστε το βιβλίο εργασίας και επαληθεύστε το αποτέλεσμα

```java
        // Save the expanded workbook.
        workbook.save("YOUR_DIRECTORY/MasterDetailDuplicatedNames.xlsx");
    }
}
```

Μετά την εκτέλεση, ανοίξτε το `MasterDetailDuplicatedNames.xlsx`. Θα πρέπει να δείτε:

* Το αρχικό master φύλλο αμετάβλητο.  
* Δύο νέα φύλλα εργασίας με ονόματα `DetailSheet_1` και `DetailSheet_2`.  
* Κάθε φύλλο λεπτομερειών περιέχει τις τιμές από την αντίστοιχη γραμμή του `DataTable`.

**Γιατί είναι σημαντικό αυτό το βήμα** – Η αποθήκευση του βιβλίου εργασίας ολοκληρώνει την επέκταση των smart markers. Το αρχείο μπορεί τώρα να σταλεί σε downstream συστήματα, να προσαρτηθεί σε email, ή να ανοιχθεί στο Excel για περαιτέρω ανάλυση.

## Διαχείριση ειδικών περιπτώσεων και παραλλαγών

### Πολλαπλά master φύλλα

Εάν το πρότυπό σας περιέχει περισσότερα από ένα master φύλλα, επαναλάβετε για κάθε φύλλο τα smart markers του:

```java
for (int i = 0; i < workbook.getWorksheets().getCount(); i++) {
    workbook.getWorksheets().get(i).getSmartMarkers().apply(data, smartMarkerOptions);
}
```

### Προσαρμοσμένη ονομασία πέρα από το δείκτη γραμμής

Μπορείτε να ενσωματώσετε οποιαδήποτε στήλη δεδομένων στο όνομα του φύλλου χρησιμοποιώντας placeholders όπως `{ColumnName}`:

```java
smartMarkerOptions.setDetailSheetNewName("Order_{OrderId}");
```

Βεβαιωθείτε ότι η στήλη `OrderId` υπάρχει στο παρεχόμενο `DataTable`.

### Πρόληψη υπερβολικά μεγάλων ονομάτων φύλλων

Το Excel περιορίζει τα ονόματα φύλλων στα 31 χαρακτήρες. Εάν το μοτίβο ονομασίας σας ενδέχεται να υπερβεί αυτό το όριο, περικόψτε ή κάντε hash την τιμή:

```java
String pattern = "Detail_{0}_{1}";
smartMarkerOptions.setDetailSheetNewName(pattern);
```

Στη συνέχεια, επεξεργαστείτε το παραγόμενο όνομα με `StringUtils.abbreviate` πριν το περάσετε στο Aspose.

## Πλήρες εκτελέσιμο παράδειγμα

Παρακάτω βρίσκεται το πλήρες αρχείο πηγαίου κώδικα που μπορείτε να αντιγράψετε, να προσαρμόσετε τις διαδρομές αρχείων και να το εκτελέσετε απευθείας:

```java
import com.aspose.cells.*;

public class DuplicateDetailSheetNames {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the master workbook that contains smart markers
        Workbook workbook = new Workbook("YOUR_DIRECTORY/MasterDetailTemplate.xlsx");

        // 2️⃣ Define how detail sheets will be named when they are created
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions();
        // {0} is replaced by the row index (starting at 1)
        smartMarkerOptions.setDetailSheetNewName("DetailSheet_{0}");

        // 3️⃣ Prepare sample data to populate the smart markers
        DataTable data = new DataTable();
        data.getColumns().add("Id", DataType.INTEGER);
        data.getColumns().add("Value", DataType.STRING);
        data.getRows().add(new Object[] { 1, "A" });
        data.getRows().add(new Object[] { 2, "B" });

        // 4️⃣ Apply the data to the smart markers using the naming options
        workbook.getWorksheets().get(0).getSmartMarkers().apply(data, smartMarkerOptions);

        // 5️⃣ Save the workbook – each detail sheet now has a unique name
        workbook.save("YOUR_DIRECTORY/MasterDetailDuplicatedNames.xlsx");
    }
}
```

**Αναμενόμενο αποτέλεσμα**

* Το `MasterDetailDuplicatedNames.xlsx` περιέχει:

## Τι Θα Πρέπει Να Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που βασίζονται στις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικά παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κυριαρχήσετε σε επιπλέον δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Κατάκτηση Aspose.Cells Java: Χρήση Smart Markers για Δυναμικά Δεδομένα σε Φύλλα Εργασίας](/cells/english/java/worksheet-management/aspose-cells-java-smart-markers-worksheets/)
- [Δημιουργία Δυναμικών Διαγραμμάτων με Smart Markers στο Aspose.Cells για Java | Οδηγός Βήμα‑Βήμα](/cells/english/java/charts-graphs/dynamic-charts-smart-markers-aspose-cells-java/)
- [Aspose Cells Java Smart Markers Φύλλα Εργασίας](/cells/german/java/worksheet-management/aspose-cells-java-smart-markers-worksheets/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}