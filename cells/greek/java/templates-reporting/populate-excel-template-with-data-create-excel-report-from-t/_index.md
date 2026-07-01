---
category: general
date: 2026-06-30
description: Συμπληρώστε το πρότυπο Excel με δεδομένα χρησιμοποιώντας το SmartMarkerProcessor
  και μάθετε πώς να δημιουργήσετε αναφορά Excel από το πρότυπο σε Java – οδηγός βήμα‑προς‑βήμα.
draft: false
keywords:
- populate excel template with data
- create excel report from template
- smartmarkerprocessor java
- excel automation java
- java data source excel
language: el
og_description: Συμπληρώστε το πρότυπο Excel με δεδομένα χρησιμοποιώντας το SmartMarkerProcessor.
  Αυτός ο οδηγός δείχνει πώς να δημιουργήσετε αναφορά Excel από το πρότυπο σε Java,
  με πλήρες κώδικα.
og_title: Συμπλήρωση προτύπου Excel με δεδομένα – Δημιουργία αναφοράς Excel από το
  πρότυπο
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Populate Excel template with data using SmartMarkerProcessor and learn
    how to create Excel report from template in Java – step‑by‑step guide.
  headline: Populate Excel Template with Data – Create Excel Report from Template
  type: TechArticle
- description: Populate Excel template with data using SmartMarkerProcessor and learn
    how to create Excel report from template in Java – step‑by‑step guide.
  name: Populate Excel Template with Data – Create Excel Report from Template
  steps:
  - name: Instantiate the SmartMarkerProcessor
    text: The processor is the engine that scans your workbook, finds Smart Markers,
      and replaces them with real values.
  - name: '(Optional): Rename the Detail Sheet'
    text: Smart Markers often generate a hidden “detail” sheet that holds intermediate
      data. Renaming it makes the final workbook easier to navigate.
  - name: Load the Template Workbook
    text: This is where you point the processor at the Excel file that contains the
      markers.
  - name: Prepare a Data Source
    text: SmartMarkerProcessor expects an `IDataSource` implementation that knows
      how to fetch values for each marker. Below is a minimal **in‑memory** data source
      that uses a `Map<String, Object>`.
  - name: Apply the Data to the Workbook
    text: Now the magic happens—Smart Markers are replaced with the values from your
      `IDataSource`.
  - name: Save the Processed Workbook
    text: Finally, write the populated workbook to disk (or stream it directly to
      HTTP response if you’re in a web app).
  - name: 'H3: Handling Collections (Tables)'
    text: If your template contains a repeating block like a sales table, replace
      the marker with an array in your data source.
  - name: 'H3: Formatting Dates and Numbers'
    text: 'Smart Markers respect cell formatting. If you pre‑format a cell as *Currency*
      in the template, the numeric value you push through will automatically display
      with the correct symbol and decimal places. No extra code needed—just make sure
      the data type you return (`Double`, `BigDecimal`, `LocalDate`) '
  - name: 'H3: Performance Considerations'
    text: '- **Reuse the processor** if you generate dozens of reports in a batch;
      just call `processor.clear()` between runs. - **Turn off calculation** (`workbook.getSettings().setRecalcOnLoad(false)`)
      when you only need to write values, not recalculate formulas. - **Stream the
      output** to avoid large tempor'
  type: HowTo
tags:
- excel
- java
- reporting
- smartmarker
title: Συμπλήρωση προτύπου Excel με δεδομένα – Δημιουργία αναφοράς Excel από το πρότυπο
url: /el/java/templates-reporting/populate-excel-template-with-data-create-excel-report-from-t/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Συμπλήρωση προτύπου Excel με δεδομένα – Δημιουργία αναφοράς Excel από πρότυπο

Έχετε ποτέ χρειαστεί να **συμπληρώσετε πρότυπο Excel με δεδομένα** αλλά δεν ήσασταν σίγουροι ποια βιβλιοθήκη μπορεί να αναλάβει τη βαριά δουλειά; Δεν είστε οι μόνοι. Όταν δημιουργείτε μηνιαίες πίνακες ελέγχου, τιμολόγια ή οποιοδήποτε φύλλο εργασίας που βασίζεται σε δεδομένα, η χειροκίνητη διαδικασία γρήγορα γίνεται εφιάλτης.  

Τα καλά νέα είναι ότι ο SmartMarkerProcessor από το Aspose.Cells το κάνει αβίαστο—απλώς δώστε του ένα πρότυπο και μια πηγή δεδομένων και θα έχετε μια επαγγελματική αναφορά Excel σε δευτερόλεπτα. Σε αυτό το tutorial θα σας δείξουμε επίσης **πώς να δημιουργήσετε αναφορά Excel από πρότυπο** χρησιμοποιώντας απλό Java, ώστε να μπορείτε να ενσωματώσετε τη λύση απευθείας στο έργο σας.

## Προαπαιτούμενα (Τι θα χρειαστεί)

- Java 17 ή νεότερη (ο κώδικας μεταγλωττίζεται και με παλαιότερες εκδόσεις, αλλά η 17 προσφέρει τα πιο πρόσφατα χαρακτηριστικά της γλώσσας).  
- Aspose.Cells for Java (το Maven artifact `com.aspose:aspose-cells` έκδοση 24.9 ή νεότερη).  
- Ένα αρχείο Excel που περιέχει Smart Markers (π.χ. `input.xlsx`).  
- Μια απλή πηγή δεδομένων που υλοποιεί το `IDataSource` (θα δημιουργήσουμε μία για εσάς).  

Δεν απαιτείται ειδικό IDE—οποιοσδήποτε επεξεργαστής που μπορεί να μεταγλωττίσει Java αρκεί.  

---

## Συμπλήρωση προτύπου Excel με δεδομένα – Βήμα‑βήμα

Παρακάτω χωρίζουμε τη διαδικασία σε έξι λογικά βήματα. Κάθε βήμα περιλαμβάνει **γιατί** είναι σημαντικό, όχι μόνο **τι** πρέπει να πληκτρολογήσετε.

### Βήμα 1: Δημιουργία του SmartMarkerProcessor  

Ο επεξεργαστής είναι η μηχανή που σαρώει το βιβλίο εργασίας σας, εντοπίζει Smart Markers και τα αντικαθιστά με πραγματικές τιμές.

```java
// Step 1: Create a SmartMarkerProcessor instance
SmartMarkerProcessor processor = new SmartMarkerProcessor();
```

*Γιατί;*  
Η δημιουργία ενός νέου επεξεργαστή εξασφαλίζει ότι ξεκινάτε με καθαρή κατάσταση. Αν επαναχρησιμοποιήσετε μια παλιά παρουσία, οι απομεινάρια ρυθμίσεων μπορεί να διαρρεύσουν στην επόμενη εκτέλεση—κάτι που σίγουρα θέλετε να αποφύγετε σε παραγωγική εργασία.

### Βήμα 2 (Προαιρετικό): Μετονομασία του φύλλου Detail  

Τα Smart Markers συχνά δημιουργούν ένα κρυφό φύλλο “detail” που κρατά ενδιάμεσα δεδομένα. Η μετονομασία του κάνει το τελικό βιβλίο εργασίας πιο εύκολο στην πλοήγηση.

```java
// Step 2: (Optional) Set a new name for the detail sheet that will be generated
processor.setDetailSheetNewName("CopyOfDetail");
```

*Συμβουλή:*  
Αν το πρότυπό σας περιέχει ήδη ένα φύλλο με όνομα “Detail”, δώστε στο παραγόμενο φύλλο ένα μοναδικό επίθημα (π.χ. `CopyOfDetail_2024`) για να αποτρέψετε συγκρούσεις ονομάτων.

### Βήμα 3: Φόρτωση του προτύπου βιβλίου εργασίας  

Εδώ κατευθύνετε τον επεξεργαστή στο αρχείο Excel που περιέχει τα markers.

```java
// Step 3: Load the workbook that contains Smart Markers
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

*Γιατί;*  
Η φόρτωση του βιβλίου εργασίας στη μνήμη επιτρέπει στο Aspose.Cells να το επεξεργαστεί χωρίς να αγγίξει το αρχικό αρχείο στο δίσκο. Μπορείτε να χρησιμοποιήσετε το ίδιο αρχείο προτύπου για πολλαπλές αναφορές με ασφάλεια.

### Βήμα 4: Προετοιμασία πηγής δεδομένων  

Ο SmartMarkerProcessor αναμένει μια υλοποίηση του `IDataSource` που ξέρει πώς να ανακτά τιμές για κάθε marker. Παρακάτω υπάρχει μια ελάχιστη **in‑memory** πηγή δεδομένων που χρησιμοποιεί ένα `Map<String, Object>`.

```java
// Step 4: Prepare the data source that provides values for the markers
class MapDataSource implements IDataSource {
    private final Map<String, Object> data;

    public MapDataSource(Map<String, Object> data) {
        this.data = data;
    }

    @Override
    public Object getValue(String key) {
        return data.get(key);
    }

    @Override
    public boolean isArray(String key) {
        // For this simple example we never return arrays
        return false;
    }

    @Override
    public int getLength(String key) {
        return 0; // not an array
    }

    @Override
    public Object getValue(String key, int index) {
        return null; // not an array
    }
}

// Example data that matches the markers in input.xlsx
Map<String, Object> values = new HashMap<>();
values.put("EmployeeName", "Jane Doe");
values.put("Department", "Engineering");
values.put("Salary", 95000);
values.put("ReportDate", LocalDate.now().toString());

IDataSource dataSource = new MapDataSource(values);
```

*Γιατί αυτή η υλοποίηση;*  
Είναι ελαφριά, δεν απαιτεί εξωτερική βάση δεδομένων και είναι ιδανική για demos ή μονάδες δοκιμών. Σε πραγματικό σενάριο θα αντικαταστήσετε το `MapDataSource` με κάτι που αντλεί δεδομένα από JDBC result set, REST API ή ORM entity.

### Βήμα 5: Εφαρμογή των δεδομένων στο βιβλίο εργασίας  

Τώρα συμβαίνει η μαγεία—τα Smart Markers αντικαθίστανται με τις τιμές από το `IDataSource` σας.

```java
// Step 5: Apply the data to the workbook, generating the detail sheet
processor.apply(workbook, dataSource);
```

*Τι συμβαίνει στο παρασκήνιο;*  
Το Aspose.Cells διατρέχει κάθε κελί που περιέχει marker όπως `${EmployeeName}`. Για κάθε marker, καλεί το `IDataSource.getValue("EmployeeName")` και γράφει την επιστρεφόμενη τιμή στο κελί. Αν είχατε marker πίνακα (`${Employees}`), ο επεξεργαστής θα επεκτείνει αυτόματα τις γραμμές βάσει του μήκους του πίνακα.

### Βήμα 6: Αποθήκευση του επεξεργασμένου βιβλίου εργασίας  

Τέλος, γράψτε το συμπληρωμένο βιβλίο εργασίας στο δίσκο (ή ρέξτε το απευθείας σε HTTP response αν βρίσκεστε σε web εφαρμογή).

```java
// Step 6: Save the processed workbook
workbook.save("YOUR_DIRECTORY/output.xlsx");
```

*Συμβουλή:*  
Χρησιμοποιήστε την υπερφόρτωση `workbook.save(OutputStream, SaveFormat.XLSX)` όταν χρειάζεται να στείλετε το αρχείο σε πελάτη χωρίς να αγγίξετε το σύστημα αρχείων.

---

## Δημιουργία αναφοράς Excel από πρότυπο – Προχωρημένες Συμβουλές

Τώρα που η βασική ροή λειτουργεί, ας εξερευνήσουμε μερικές κοινές βελτιώσεις που κάνουν την **αναφορά Excel από πρότυπο** έτοιμη για παραγωγή.

### H3: Διαχείριση Συλλογών (Πίνακες)

Αν το πρότυπό σας περιέχει ένα επαναλαμβανόμενο τμήμα όπως ένας πίνακας πωλήσεων, αντικαταστήστε το marker με έναν πίνακα στην πηγή δεδομένων.

```java
class ListDataSource implements IDataSource {
    private final Map<String, List<Map<String, Object>>> tables = new HashMap<>();

    public void addTable(String name, List<Map<String, Object>> rows) {
        tables.put(name, rows);
    }

    @Override
    public boolean isArray(String key) {
        return tables.containsKey(key);
    }

    @Override
    public int getLength(String key) {
        List<Map<String, Object>> rows = tables.get(key);
        return rows == null ? 0 : rows.size();
    }

    @Override
    public Object getValue(String key, int index) {
        List<Map<String, Object>> rows = tables.get(key);
        return rows != null ? rows.get(index) : null;
    }

    @Override
    public Object getValue(String key) {
        // Not used for arrays
        return null;
    }
}

// Sample table data
List<Map<String, Object>> sales = new ArrayList<>();
sales.add(Map.of("Product", "Widget A", "Qty", 120, "Revenue", 4800));
sales.add(Map.of("Product", "Widget B", "Qty", 75,  "Revenue", 3375));

ListDataSource listSource = new ListDataSource();
listSource.addTable("SalesData", sales);

// Apply as before
processor.apply(workbook, listSource);
```

Στο πρότυπο θα έχετε markers όπως `${SalesData.Product}`, `${SalesData.Qty}` κ.λπ., μέσα σε μια γραμμή που το Aspose θα αντιγράψει για κάθε εγγραφή.

### H3: Μορφοποίηση Ημερομηνιών και Αριθμών

Τα Smart Markers σέβονται τη μορφοποίηση των κελιών. Αν προμορφοποιήσετε ένα κελί ως *Currency* στο πρότυπο, η αριθμητική τιμή που θα περάσετε θα εμφανιστεί αυτόματα με το σωστό σύμβολο και δεκαδικά ψηφία. Δεν απαιτείται επιπλέον κώδικας—απλώς βεβαιωθείτε ότι ο τύπος δεδομένων που επιστρέφετε (`Double`, `BigDecimal`, `LocalDate`) ταιριάζει με τη μορφή που περιμένετε.

### H3: Σκέψεις για Απόδοση

- **Επαναχρησιμοποίηση του επεξεργαστή** αν παράγετε δεκάδες αναφορές σε batch· απλώς καλέστε `processor.clear()` μεταξύ των εκτελέσεων.  
- **Απενεργοποίηση υπολογισμών** (`workbook.getSettings().setRecalcOnLoad(false)`) όταν χρειάζεται μόνο η εγγραφή τιμών, όχι ο επαναυπολογισμός τύπων.  
- **Ροή εξόδου** (stream) για αποφυγή μεγάλων προσωρινών αρχείων όταν τρέχετε σε περιορισμένο περιβάλλον.

---

## Αναμενόμενο Αποτέλεσμα

Μετά την εκτέλεση του παραδείγματος έξι βημάτων, το `output.xlsx` θα περιέχει:

| A               | B          | C            |
|-----------------|------------|--------------|
| EmployeeName    | Jane Doe   |              |
| Department      | Engineering|              |
| Salary          | 95,000     |              |
| ReportDate      | 2026‑06‑30 |              |
| …               | …          | …            |

Αν προσθέσατε το παράδειγμα πίνακα, θα δείτε έναν πλήρως συμπληρωμένο πίνακα πωλήσεων ακριβώς κάτω από τις γραμμές κεφαλίδας. Όλη η μορφοποίηση που εφαρμόσατε στο `input.xlsx` (σύμβολα νομισμάτων, μοτίβα ημερομηνίας, έντονες κεφαλίδες) παραμένει αμετάβλητη.

---

## Συμπέρασμα

Μόλις περάσαμε από το **συμπλήρωση προτύπου Excel με δεδομένα** χρησιμοποιώντας το `SmartMarkerProcessor` του Aspose.Cells, και τώρα γνωρίζετε τα ακριβή βήματα για **δημιουργία αναφοράς Excel από πρότυπο** σε Java. Η βασική ιδέα είναι απλή: ορίστε Smart Markers σε ένα επαναχρησιμοποιήσιμο βιβλίο εργασίας, τροφοδοτήστε το με ένα συμβατό `IDataSource` και αφήστε τη βιβλιοθήκη να κάνει τη βαριά δουλειά.  

Από εδώ μπορείτε:

- Να ενσωματώσετε μια πραγματική βάση δεδομένων αντί του `MapDataSource`.  
- Να προσθέσετε γραφήματα που θα ενημερώνονται αυτόματα με τα νέα δεδομένα.  
- Να αναπτύξετε τον κώδικα ως μικροϋπηρεσία που επιστρέφει το παραγόμενο αρχείο Excel κατόπιν αιτήματος.  

Δοκιμάστε το, τροποποιήστε τα markers, και δείτε τη ροή αναφοράς σας να γίνεται πολύ πιο αποδοτική. Έχετε ερωτήσεις ή κάποιο δύσκολο σενάριο marker; Αφήστε ένα σχόλιο παρακάτω—καλή προγραμματιστική!

## Τι πρέπει να μάθετε στη συνέχεια;

Οι παρακάτω οδηγίες καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κυριαρχήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στην υλοποίηση των δικών σας έργων.

- [Populate Excel with Nested Data Using Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/data-manipulation/populate-excel-nested-data-aspose-cells-java/)
- [Export XML Data from Excel using Aspose.Cells in Java: Step‑By‑Step Guide](/cells/english/java/import-export/export-excel-xml-data-aspose-cells-java/)
- [How to Create & Format Excel Cells Using Aspose.Cells for Java: A Step‑By‑Step Guide](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}