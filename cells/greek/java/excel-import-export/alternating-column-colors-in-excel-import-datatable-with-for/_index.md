---
category: general
date: 2026-06-27
description: Μάθετε πώς να εισάγετε DataTable στο Excel με εναλλασσόμενα χρώματα στηλών.
  Οδηγός βήμα‑προς‑βήμα για την εισαγωγή δεδομένων με μορφοποίηση και τον ορισμό χρώματος
  γραμματοσειράς στη στήλη χρησιμοποιώντας Java.
draft: false
keywords:
- alternating column colors
- import data with formatting
- import datatable to excel
- set column font color
- how to import datatable
language: el
og_description: Αποκτήστε τον έλεγχο των εναλλασσόμενων χρωμάτων στηλών κατά την εισαγωγή
  ενός DataTable στο Excel. Αυτός ο οδηγός δείχνει πώς να εισάγετε δεδομένα με μορφοποίηση
  και να ορίσετε το χρώμα γραμματοσειράς της στήλης σε Java.
og_title: Εναλλασσόμενα Χρώματα Στηλών στο Excel – Εισαγωγή DataTable με Μορφοποίηση
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Learn how to import DataTable to Excel with alternating column colors.
    Step‑by‑step guide on import data with formatting and set column font color using
    Java.
  headline: Alternating Column Colors in Excel – Import DataTable with Formatting
  type: TechArticle
- description: Learn how to import DataTable to Excel with alternating column colors.
    Step‑by‑step guide on import data with formatting and set column font color using
    Java.
  name: Alternating Column Colors in Excel – Import DataTable with Formatting
  steps:
  - name: Prerequisites
    text: '- Java 8+ (the code works with newer releases as well). - Apache POI 5.x
      on your classpath – the library that talks to Excel files. - A `DataTable` implementation
      that offers `getColumns()` and `size()` (or adapt the example to a `ResultSet`).'
  - name: – Obtain the DataTable You Want to Export
    text: First, you need a source of rows and columns. In real projects this might
      be a database query, a CSV parser, or an in‑memory collection. The example assumes
      a helper method `getDataTable()` that returns a ready‑to‑use `DataTable`.
  - name: – Prepare a Style for Each Column
    text: We create a `Style[]` whose length matches the number of columns. Each entry
      will hold a font color that alternates between blue and green.
  - name: – Create Styles with Alternating Font Colors
    text: 'Now the fun part: loop through the array and assign a blue font to even‑indexed
      columns and a green font to odd‑indexed ones. This is where **alternating column
      colors** is implemented.'
  - name: – Import the DataTable with the Style Array
    text: Finally, we hand the `DataTable` and the `columnStyles` array to POI’s `importDataTable`
      method. The `true` flag tells POI to treat the first row as column headers.
  - name: – Save the Workbook (Optional but Recommended)
    text: After the import, you’ll probably want to write the workbook to disk or
      stream it to a client.
  type: HowTo
- questions:
  - answer: Replace `setFontColor` with `setPatternForegroundColor` and call `setPattern(BackgroundType.SOLID)`
      on the style.
    question: What if I need background colors instead of font colors?
  - answer: 'Absolutely—just swap the loop logic: iterate over rows and assign a style
      per row index.'
    question: Can I apply the same color scheme to rows instead of columns?
  - answer: Excel caps at 16,384 columns (XFD). The code will throw an exception once
      you exceed that limit. Guard against it by checking `columnCount` against `SpreadsheetVersion.EXCEL2007.getMaxColumns()`.
    question: What if the DataTable has more columns than the worksheet can handle?
  - answer: Yes, POI abstracts the format. However, the older binary format supports
      fewer colors, so you might see a fallback to the nearest palette entry.
    question: Does this work with .xls (Excel 97‑2003) files?
  type: FAQPage
tags:
- excel
- java
- datatable
- formatting
- apache-poi
title: Εναλλασσόμενα χρώματα στηλών στο Excel – Εισαγωγή DataTable με μορφοποίηση
url: /el/java/excel-import-export/alternating-column-colors-in-excel-import-datatable-with-for/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εναλλασσόμενα Χρώματα Στηλών στο Excel – Εισαγωγή DataTable με Μορφοποίηση

Έχετε ποτέ αναρωτηθεί πώς να δώσετε στο εξαγόμενο Excel σας μια δόση οπτικού polish χωρίς να βγείτε από τον κώδικα; **Alternating column colors** είναι ένας γρήγορος τρόπος να κάνετε μεγάλους πίνακες πιο αναγνώσιμους, και μπορείτε να το κάνετε ενώ **import datatable to excel**. Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από μια πλήρη λύση Java που όχι μόνο φέρνει τα δεδομένα σας σε ένα φύλλο εργασίας αλλά εφαρμόζει επίσης ένα μοτίβο γραμματοσειράς μπλε‑πράσινο στήλη‑με‑στήλη.

Θα δείτε πώς να **import data with formatting**, να ορίσετε το χρώμα γραμματοσειράς για κάθε στήλη, και να απαντήσετε στην επίμονη ερώτηση “**how to import datatable**” μια και για πάντα. Χωρίς εξωτερικά εργαλεία, μόνο καθαρή Java και μια δημοφιλής βιβλιοθήκη υπολογιστικών φύλλων.

## Τι Θα Κατασκευάσετε

Στο τέλος αυτού του οδηγού θα έχετε ένα εκτελέσιμο απόσπασμα Java που:

1. Ανακτά ένα `DataTable` (ή οποιαδήποτε συλλογή τύπου `ResultSet`).  
2. Δημιουργεί έναν πίνακα `Style` όπου οι ζυγές στήλες είναι μπλε και οι περιττές στήλες είναι πράσινες.  
3. Καλεί `importDataTable` για να τοποθετήσει τα δεδομένα στο κελί **A1** εφαρμόζοντας τα στυλ.  

Όλα αυτά συμβαίνουν σε λίγες γραμμές, αλλά το αποτέλεσμα μοιάζει με μια χειροποίητη αναφορά.

### Προαπαιτούμενα

- Java 8+ (ο κώδικας λειτουργεί και με νεότερες εκδόσεις).  
- Apache POI 5.x στο classpath σας – η βιβλιοθήκη που επικοινωνεί με αρχεία Excel.  
- Μια υλοποίηση `DataTable` που προσφέρει `getColumns()` και `size()` (ή προσαρμόστε το παράδειγμα σε `ResultSet`).  

Αν ήδη χρησιμοποιείτε το POI για άλλες εργασίες Excel, μπορείτε να ενσωματώσετε αυτό το κομμάτι άμεσα.  

---

## Εναλλασσόμενα Χρώματα Στηλών Κατά την Εισαγωγή DataTable στο Excel

Η καρδιά της λύσης βρίσκεται σε τέσσερα σύντομα βήματα. Ας τα αναλύσουμε.

### Βήμα 1 – Λάβετε το DataTable που Θέλετε να Εξάγετε

Πρώτα, χρειάζεστε μια πηγή γραμμών και στηλών. Σε πραγματικά έργα αυτό μπορεί να είναι ένα ερώτημα βάσης δεδομένων, ένας parser CSV ή μια συλλογή στη μνήμη. Το παράδειγμα υποθέτει μια βοηθητική μέθοδο `getDataTable()` που επιστρέφει ένα έτοιμο `DataTable`.

```java
// Step 1: Obtain the data to be imported
DataTable dataTable = getDataTable();   // your own method that fills the table
```

> **Γιατί είναι σημαντικό:**  
> Η λήψη των δεδομένων πρώτα σας επιτρέπει να ελέγξετε τον αριθμό των στηλών, κάτι που καθορίζει το μέγεθος του πίνακα στυλ αργότερα. Επίσης, εξασφαλίζει ότι το βήμα εισαγωγής έχει ένα συγκεκριμένο αντικείμενο με το οποίο να δουλέψει.

### Βήμα 2 – Προετοιμάστε ένα Στυλ για Κάθε Στήλη

Δημιουργούμε ένα `Style[]` του μήκους που ταιριάζει με τον αριθμό των στηλών. Κάθε στοιχείο θα κρατά ένα χρώμα γραμματοσειράς που εναλλάσσεται μεταξύ μπλε και πράσινου.

```java
// Step 2: Prepare a style for each column (same count as the number of columns)
int columnCount = dataTable.getColumns().size();
Style[] columnStyles = new Style[columnCount];
```

> **Pro tip:** Αν το `DataTable` σας μπορεί να αλλάξει σχήμα κατά το runtime, υπολογίστε ξανά το `columnCount` κάθε φορά που εξάγετε. Αυτό αποτρέπει το `ArrayIndexOutOfBoundsException`.

### Βήμα 3 – Δημιουργήστε Στυλ με Εναλλασσόμενα Χρώματα Γραμματοσειράς

Τώρα το διασκεδαστικό μέρος: κάντε βρόχο στον πίνακα και αναθέστε μια μπλε γραμματοσειρά στις στήλες με ζυγό δείκτη και μια πράσινη γραμματοσειρά στις στήλες με περιττό δείκτη. Εδώ υλοποιείται το **alternating column colors**.

```java
// Step 3: Create styles with alternating font colors for visual distinction
for (int i = 0; i < columnStyles.length; i++) {
    columnStyles[i] = workbook.createStyle();               // create a fresh style
    // Even columns → blue, odd columns → green
    columnStyles[i].setFontColor(
        (i % 2 == 0) ? Color.getBlue() : Color.getGreen()
    );
}
```

> **Γιατί εναλλασσόμενα χρώματα;**  
> Τα ανθρώπινα μάτια διαβάζουν πιο εύκολα τις γραμμές όταν οι γειτονικές στήλες ξεχωρίζουν. Ένας ρυθμός μπλε‑πράσινου μειώνει την οπτική κόπωση, ειδικά σε ευρείς πίνακες.

### Βήμα 4 – Εισάγετε το DataTable με τον Πίνακα Στυλ

Τέλος, παραδίδουμε το `DataTable` και τον πίνακα `columnStyles` στη μέθοδο `importDataTable` του POI. Η σημαία `true` λέει στο POI να θεωρήσει την πρώτη γραμμή ως επικεφαλίδες στηλών.

```java
// Step 4: Import the data table into the worksheet starting at cell A1, applying the styles
worksheet.getCells().importDataTable(dataTable, true, "A1", columnStyles);
```

> **Τι συμβαίνει στο παρασκήνιο;**  
> Το POI διασχίζει κάθε στήλη, παίρνει το αντίστοιχο `Style` από τον πίνακα και γράφει κάθε κελί χρησιμοποιώντας αυτό το στυλ. Επειδή ορίσαμε μόνο το χρώμα γραμματοσειράς, τα άλλα στοιχεία (περιγράμματα, φόντο) παραμένουν προεπιλεγμένα — μπορείτε να επεκτείνετε το στυλ αν χρειάζεστε περισσότερη διακόσμηση.

### Βήμα 5 – Αποθηκεύστε το Workbook (Προαιρετικό αλλά Συνιστώμενο)

Μετά την εισαγωγή, πιθανότατα θα θέλετε να γράψετε το workbook στο δίσκο ή να το στείλετε σε έναν client.

```java
// Optional: write the workbook to a file
try (FileOutputStream fos = new FileOutputStream("ExportedReport.xlsx")) {
    workbook.save(fos);
}
```

> **Edge case:** Αν το αρχείο προορισμού υπάρχει ήδη, το `FileOutputStream` θα το αντικαταστήσει. Περιβάλλετε την κλήση με έναν έλεγχο ή ζητήστε επιβεβαίωση από τον χρήστη σε περιβάλλον UI.

---

## Συχνές Ερωτήσεις & Πιθανά Προβλήματα

- **Τι αν χρειάζομαι χρώματα φόντου αντί για χρώματα γραμματοσειράς;**  
  Αντικαταστήστε το `setFontColor` με `setPatternForegroundColor` και καλέστε `setPattern(BackgroundType.SOLID)` στο στυλ.

- **Μπορώ να εφαρμόσω το ίδιο σχήμα χρωμάτων σε γραμμές αντί για στήλες;**  
  Απόλυτα — απλώς αλλάξτε τη λογική του βρόχου: διασχίστε τις γραμμές και αναθέστε ένα στυλ ανά δείκτη γραμμής.

- **Τι γίνεται αν το DataTable έχει περισσότερες στήλες από ό,τι μπορεί να διαχειριστεί το φύλλο εργασίας;**  
  Το Excel περιορίζεται σε 16.384 στήλες (XFD). Ο κώδικας θα πετάξει εξαίρεση όταν υπερβείτε αυτό το όριο. Προστατέψτε το ελέγχοντας το `columnCount` έναντι του `SpreadsheetVersion.EXCEL2007.getMaxColumns()`.

- **Λειτουργεί αυτό με αρχεία .xls (Excel 97‑2003);**  
  Ναι, το POI αφαιρεί τη διαφορά μορφής. Ωστόσο, η παλαιότερη δυαδική μορφή υποστηρίζει λιγότερα χρώματα, οπότε μπορεί να δείτε μια προσαρμογή στο πλησιέστερο χρώμα της παλέτας.

---

## Πλήρες Παράδειγμα Εργασίας

Παρακάτω βρίσκεται μια αυτόνομη κλάση που μπορείτε να επικολλήσετε σε ένα Maven project που ήδη περιλαμβάνει `org.apache.poi:poi-ooxml:5.2.3`. Προσαρμόστε τη `getDataTable()` ώστε να επιστρέφει την πραγματική πηγή δεδομένων σας.

```java
import com.aspose.cells.*;
import java.io.FileOutputStream;

public class ExcelAlternatingColorsExport {

    public static void main(String[] args) throws Exception {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 1️⃣ Obtain the data to be imported
        DataTable dataTable = getDataTable(); // implement this method

        // 2️⃣ Prepare a style for each column
        int columnCount = dataTable.getColumns().size();
        Style[] columnStyles = new Style[columnCount];

        // 3️⃣ Create alternating font colors (blue for even, green for odd)
        for (int i = 0; i < columnStyles.length; i++) {
            columnStyles[i] = workbook.createStyle();
            columnStyles[i].setFontColor(
                (i % 2 == 0) ? Color.getBlue() : Color.getGreen()
            );
        }

        // 4️⃣ Import the data with formatting
        worksheet.getCells().importDataTable(dataTable, true, "A1", columnStyles);

        // 5️⃣ Save the file
        try (FileOutputStream fos = new FileOutputStream("AlternatingColorsReport.xlsx")) {
            workbook.save(fos);
        }

        System.out.println("Export complete – open AlternatingColorsReport.xlsx to see the result.");
    }

    // Dummy implementation – replace with real data retrieval
    private static DataTable getDataTable() {
        DataTable dt = new DataTable();
        dt.getColumns().add("ID");
        dt.getColumns().add("Name");
        dt.getColumns().add("Score");
        dt.getRows().add(new DataRow(new Object[]{1, "Alice", 85}));
        dt.getRows().add(new DataRow(new Object[]{2, "Bob", 92}));
        dt.getRows().add(new DataRow(new Object[]{3, "Carol", 78}));
        return dt;
    }
}
```

**Αναμενόμενο αποτέλεσμα:** Ανοίξτε το `AlternatingColorsReport.xlsx`. Οι στήλες A και C (ζυγοί δείκτες) εμφανίζουν το κείμενο τους σε μπλε, ενώ η στήλη B (περιττός δείκτης) δείχνει πράσινη γραμματοσειρά. Η πρώτη γραμμή είναι έντονη ως επικεφαλίδα επειδή το `importDataTable` τη θεωρεί ως τέτοια.

---

## Συμπέρασμα

Καλύψαμε όλα όσα χρειάζεστε για να **import datatable to excel** ενώ εφαρμόζετε **alternating column colors** και **set column font color** προγραμματιστικά. Η προσέγγιση είναι ελαφριά, βασίζεται μόνο στο Apache POI, και μπορεί να επεκταθεί για άλλες ανάγκες μορφοποίησης όπως περιγράμματα ή φόντο κελιών.

Σκεφτείτε να πειραματιστείτε με:

- **Import data with formatting** για γραμμές (εναλλασσόμενα χρώματα γραμμών).  
- Προσθήκη **conditional formatting** για να επισημάνετε υψηλές τιμές.  
- Εξαγωγή απευθείας σε HTTP response για web εφαρμογές.

Αισθανθείτε ελεύθεροι να προσαρμόσετε το μοτίβο στη δική σας αλυσίδα αναφορών — μόλις κυριαρχήσετε τα βασικά, ο ουρανός είναι το όριο. Καλή προγραμματιστική!

## Τι Θα Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετα χαρακτηριστικά του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στα δικά σας έργα.

- [Πώς να ταξινομήσετε δεδομένα Excel κατά χρώμα στήλης χρησιμοποιώντας Aspose.Cells Java: Πλήρης Οδηγός](/cells/english/java/formatting/sort-excel-data-by-column-color-aspose-cells-java/)
- [Κατακτήστε την προστασία στηλών Excel χρησιμοποιώντας Aspose.Cells για Java: Ένας ολοκληρωμένος οδηγός](/cells/english/java/security-protection/excel-column-protection-aspose-cells-java/)
- [Πώς να εισάγετε μια στήλη στο Excel χρησιμοποιώντας Aspose.Cells για Java - Ένας ολοκληρωμένος οδηγός](/cells/english/java/worksheet-management/aspose-cells-java-insert-column-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}