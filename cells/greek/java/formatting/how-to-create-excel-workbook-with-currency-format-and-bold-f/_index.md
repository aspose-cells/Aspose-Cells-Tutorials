---
category: general
date: 2026-08-20
description: Δημιουργήστε βιβλίο εργασίας Excel σε Java χρησιμοποιώντας το Aspose.Cells,
  ορίστε μορφή νομίσματος, προσθέστε έντονη γραμματοσειρά και εισάγετε πίνακα στυλ
  για μορφοποιημένα κελιά.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- set currency format
- format cells currency
- how to import style
- add bold font
language: el
lastmod: 2026-08-20
og_description: Δημιουργήστε βιβλίο εργασίας Excel σε Java, ορίστε μορφή νομίσματος,
  προσθέστε έντονη γραμματοσειρά και μάθετε πώς να εισάγετε στυλ χρησιμοποιώντας το
  Aspose.Cells.
og_image_alt: Screenshot of an excel workbook created with currency format and bold
  font using Aspose.Cells
og_title: Δημιουργήστε βιβλίο εργασίας Excel με μορφοποιημένα κελιά νομίσματος σε
  Java
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Create excel workbook in Java using Aspose.Cells, set currency format,
    add bold font, and import style array for styled cells.
  headline: How to create excel workbook with currency format and bold font in Java
  type: TechArticle
- description: Create excel workbook in Java using Aspose.Cells, set currency format,
    add bold font, and import style array for styled cells.
  name: How to create excel workbook with currency format and bold font in Java
  steps:
  - name: Initialise the workbook and worksheet
    text: Creating a fresh workbook gives you a clean container for all subsequent
      formatting.
  - name: Build a DataTable with numeric data
    text: A `DataTable` mimics a database table, making it easy to import rows in
      bulk.
  - name: Define a style – currency format and bold font
    text: Here we **set currency format** and **add bold font** to a `Style` object.
  - name: Configure import options to use the style array
    text: Aspose.Cells lets you pass a `Style[]` via `ImportTableOptions`. This is
      the official **how to import style** method.
  - name: Import the DataTable into the worksheet
    text: Now we bring the data into the sheet at cell `A1`, applying the style array
      automatically.
  - name: Save the workbook to disk
    text: Finally, write the in‑memory workbook to a physical file.
  - name: Expected output
    text: 'When you open `DataTableWithStyleArray.xlsx` in Microsoft Excel, you should
      see:'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- Formatting
title: Πώς να δημιουργήσετε βιβλίο εργασίας Excel με μορφή νομίσματος και έντονη γραμματοσειρά
  σε Java
url: /el/java/formatting/how-to-create-excel-workbook-with-currency-format-and-bold-f/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να δημιουργήσετε excel workbook με μορφή νομίσματος και έντονη γραμματοσειρά σε Java

Αν χρειάζεστε να **create excel workbook** προγραμματιστικά, αυτός ο οδηγός σας δείχνει ακριβώς πώς. Θα περάσουμε από τη δημιουργία ενός βιβλίου εργασίας, την εφαρμογή μορφής νομίσματος, την προσθήκη έντονης γραμματοσειράς, και τη χρήση της δυνατότητας **how to import style** του Aspose.Cells ώστε κάθε εισαγόμενο κελί να φαίνεται συνεπές.

Θα ολοκληρώσετε με ένα έτοιμο προς χρήση αρχείο `DataTableWithStyleArray.xlsx` που εμφανίζει τους αριθμούς ως δολάρια και τους επισημαίνει με έντονη γραμματοσειρά. Δεν απαιτείται χειροκίνητη μορφοποίηση στο Excel.

## Προαπαιτήσεις

- Java 17 ή νεότερη εγκατεστημένη.
- Άδεια Aspose.Cells for Java (ή ένα δωρεάν κλειδί αξιολόγησης).
- Maven ή Gradle για τη διαχείριση της εξάρτησης `aspose-cells`.
- Βασική εξοικείωση με τις συλλογές Java και το `DataTable`.

```xml
<!-- Maven dependency -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version>
</dependency>
```

> **Συμβουλή επαγγελματία:** Εάν αντιμετωπίσετε ένα `LicenseException`, τοποθετήστε το αρχείο άδειας σας στο classpath και καλέστε `License license = new License(); license.setLicense("Aspose.Total.Java.lic");` πριν δημιουργήσετε το βιβλίο εργασίας.

## Πώς να δημιουργήσετε excel workbook με μορφοποιημένα κελιά νομίσματος

Αυτή η ενότητα περιέχει τα βασικά βήματα. Κάθε βήμα εξηγεί **γιατί** είναι σημαντικό, όχι μόνο **τι** πρέπει να πληκτρολογήσετε.

### Βήμα 1: Αρχικοποίηση του βιβλίου εργασίας και του φύλλου εργασίας

Η δημιουργία ενός νέου βιβλίου εργασίας σας παρέχει ένα καθαρό δοχείο για όλες τις επόμενες μορφοποιήσεις.

```java
// Step 1: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();                     // creates an empty .xlsx file in memory
Worksheet worksheet = workbook.getWorksheets().get(0); // first sheet is index 0
Cells cells = worksheet.getCells();                     // shortcut to work with cells
```

> **Γιατί:** Το αντικείμενο `Workbook` αντιπροσωπεύει ολόκληρο το αρχείο Excel. Η πρόσβαση στο πρώτο `Worksheet` σας επιτρέπει να αρχίσετε να γεμίζετε δεδομένα αμέσως.

### Βήμα 2: Δημιουργία ενός DataTable με αριθμητικά δεδομένα

Ένα `DataTable` μιμείται έναν πίνακα βάσης δεδομένων, καθιστώντας εύκολη την μαζική εισαγωγή γραμμών.

```java
// Step 2: Build a DataTable with sample numeric data
DataTable dataTable = new DataTable();
dataTable.getColumns().add("Amount", DataType.DOUBLE); // column type DOUBLE ensures numeric handling
dataTable.getRows().add(new Object[]{1234.56});
dataTable.getRows().add(new Object[]{7890.12});
```

> **Γιατί:** Η χρήση του `DOUBLE` εγγυάται ότι οι τιμές διατηρούν την δεκαδική τους ακρίβεια, κάτι που είναι απαραίτητο όταν αργότερα **format cells currency**.

### Βήμα 3: Ορισμός στυλ – μορφή νομίσματος και έντονη γραμματοσειρά

Εδώ **ορίζουμε τη μορφή νομίσματος** και **προσθέτουμε έντονη γραμματοσειρά** σε ένα αντικείμενο `Style`.

```java
// Step 3: Define a style (currency format and bold font) for the imported cells
Style currencyStyle = workbook.createStyle();                // create a reusable style instance
currencyStyle.getNumber().setFormat("$#,##0.00");            // set currency format (e.g., $1,234.56)
currencyStyle.getFont().setBold(true);                      // make the font bold
Style[] styleArray = new Style[] { currencyStyle };          // style array required by ImportTableOptions
```

> **Γιατί:** Η συμβολοσειρά μορφής `Number` `$#,##0.00` λέει στο Excel να αντιμετωπίζει το κελί ως χρηματική αξία, ενώ το `setBold(true)` τραβά την προσοχή στους αριθμούς. Η τοποθέτηση του στυλ σε έναν πίνακα μας προετοιμάζει για το βήμα **how to import style**.

### Βήμα 4: Διαμόρφωση επιλογών εισαγωγής για χρήση του πίνακα στυλ

Το Aspose.Cells σας επιτρέπει να περάσετε ένα `Style[]` μέσω `ImportTableOptions`. Αυτή είναι η επίσημη μέθοδος **how to import style**.

```java
// Step 4: Set up import options to use the style array
ImportTableOptions importOptions = new ImportTableOptions();
importOptions.setStyleArray(styleArray); // tells the importer to apply our currencyStyle to every column
```

> **Γιατί:** Χωρίς `ImportTableOptions`, τα εισαγόμενα κελιά θα κληρονομούσαν το προεπιλεγμένο στυλ, χάνοντας τη μορφοποίηση νομίσματος και την έντονη γραμματοσειρά που ορίσαμε.

### Βήμα 5: Εισαγωγή του DataTable στο φύλλο εργασίας

Τώρα φέρνουμε τα δεδομένα στο φύλλο στο κελί `A1`, εφαρμόζοντας αυτόματα τον πίνακα στυλ.

```java
// Step 5: Import the DataTable into the worksheet at A1, applying the style
cells.importDataTable(dataTable, true, "A1", importOptions);
```

- `true` υποδεικνύει ότι η πρώτη γραμμή του `DataTable` περιέχει τις επικεφαλίδες των στηλών.
- `"A1"` είναι η πάνω‑αριστερή γωνία όπου ξεκινά η εισαγωγή.

> **Γιατί:** Η εισαγωγή με τον πίνακα στυλ εγγυάται ότι κάθε εισαγόμενο κελί λαμβάνει το στυλ **format cells currency** που προετοιμάσαμε νωρίτερα.

### Βήμα 6: Αποθήκευση του βιβλίου εργασίας στον δίσκο

Τέλος, γράψτε το βιβλίο εργασίας στη μνήμη σε ένα φυσικό αρχείο.

```java
// Step 6: Save the workbook to a file
String outputPath = "YOUR_DIRECTORY/DataTableWithStyleArray.xlsx";
workbook.save(outputPath);
System.out.println("Workbook saved to: " + outputPath);
```

> **Γιατί:** Η αποθήκευση διατηρεί τη μορφοποίηση, επιτρέποντας σε εσάς ή σε επόμενες διεργασίες να ανοίξετε το αρχείο στο Excel με την επιθυμητή εμφάνιση.

## Πλήρης κώδικας πηγής

Ακολουθεί η πλήρης, έτοιμη προς εκτέλεση κλάση Java. Αντιγράψτε την στο IDE σας, αντικαταστήστε το `YOUR_DIRECTORY` με έναν υπάρχον φάκελο, και εκτελέστε.

```java
import com.aspose.cells.*;

public class StyleArrayImportTutorial {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);
        Cells cells = worksheet.getCells();

        // Step 2: Build a DataTable with sample numeric data
        DataTable dataTable = new DataTable();
        dataTable.getColumns().add("Amount", DataType.DOUBLE);
        dataTable.getRows().add(new Object[]{1234.56});
        dataTable.getRows().add(new Object[]{7890.12});

        // Step 3: Define a style (currency format and bold font) for the imported cells
        Style currencyStyle = workbook.createStyle();
        currencyStyle.getNumber().setFormat("$#,##0.00");   // set currency format
        currencyStyle.getFont().setBold(true);             // add bold font
        Style[] styleArray = new Style[] { currencyStyle };

        // Step 4: Set up import options to use the style array
        ImportTableOptions importOptions = new ImportTableOptions();
        importOptions.setStyleArray(styleArray);           // how to import style

        // Step 5: Import the DataTable into the worksheet at A1, applying the style
        cells.importDataTable(dataTable, true, "A1", importOptions);

        // Step 6: Save the workbook to a file
        workbook.save("YOUR_DIRECTORY/DataTableWithStyleArray.xlsx");
        System.out.println("Workbook created successfully.");
    }
}
```

### Αναμενόμενο αποτέλεσμα

Όταν ανοίξετε το `DataTableWithStyleArray.xlsx` στο Microsoft Excel, θα πρέπει να δείτε:

| Ποσό |
|------|
| **$1,234.56** |
| **$7,890.12** |

- Οι αριθμοί εμφανίζονται με **μορφή νομίσματος** (σύμβολο `$`, δύο δεκαδικά ψηφία).
- Η γραμματοσειρά και για τα δύο κελιά είναι **έντονη**, κάνοντάς τα να ξεχωρίζουν.

## Συνηθισμένες παραλλαγές και ειδικές περιπτώσεις

| Σενάριο | Τι να αλλάξετε | Αιτία |
|----------|----------------|--------|
| **Διαφορετικό νόμισμα** | `currencyStyle.getNumber().setFormat("€#,##0.00");` | Χρησιμοποιήστε το σύμβολο του ευρώ ή οποιαδήποτε μορφή ειδική για την περιοχή. |
| **Πολλαπλές στήλες με διαφορετικά στυλ** | Create multiple `Style` objects, populate `styleArray` in the same order as columns. | Κάθε στήλη μπορεί να έχει τη δική της μορφή αριθμού, γραμματοσειρά, φόντο, κ.λπ. |
| **Μεγάλα σύνολα δεδομένων** | Use `cells.importDataTable(dataTable, false, "A1", importOptions);` and set `importOptions.setImportDataOptions(ImportDataOptions.DATA_ONLY);` | Βελτιώνει την απόδοση παραλείποντας τις γραμμές επικεφαλίδας ή περιττά μεταδεδομένα. |
| **Εφαρμογή στυλ μετά την εισαγωγή** | Call `cells.get("A2").setStyle(currencyStyle);` for individual cells. | Χρήσιμο όταν μόνο ένα υποσύνολο γραμμών χρειάζεται ειδική μορφοποίηση. |

## Συμβουλές για χρήση σε παραγωγή

- **License early**: Καταχωρίστε την άδεια Aspose.Cells πριν δημιουργήσετε το βιβλίο εργασίας για να αποφύγετε το υδατογράφημα αξιολόγησης.
- **Thread safety**: Τα αντικείμενα `Workbook` **δεν** είναι ασφαλή για νήματα. Δημιουργήστε ξεχωριστό στιγμιότυπο ανά νήμα εάν δημιουργείτε πολλά αρχεία ταυτόχρονα.
- **Memory management**: Για πολύ μεγάλα φύλλα, σκεφτείτε τη χρήση του streaming API του `Workbook` (`Workbook` → `WorkbookDesigner`) για να κρατήσετε τη χρήση μνήμης χαμηλή.
- **Testing**: Συμπεριλάβετε μια μονάδα δοκιμής που ανοίγει το αποθηκευμένο αρχείο με το Apache POI και ελέγχει ότι η μορφή αριθμού του στυλ του κελιού ταιριάζει με `"$#,##0.00"`.

## Συμπέρασμα

Τώρα ξέρετε πώς να **create excel workbook** σε Java, **set currency format**, **add bold font**, και σωστά **how to import style** χρησιμοποιώντας το `ImportTableOptions` του Aspose.Cells. Αυτή η ολοκληρωμένη λύση εξαλείφει τα χειροκίνητα βήματα στο Excel και εγγυάται ότι κάθε εισαγόμενο κελί ακολουθεί το ίδιο στυλ **format cells currency**.

Έτοιμοι για την επόμενη πρόκληση; Δοκιμάστε να προσθέσετε μορφοποίηση υπό όρους, ενσωμάτωση γραφημάτων ή εξαγωγή του βιβλίου εργασίας σε PDF—όλα ενώ επαναχρησιμοποιείτε την ίδια τεχνική style‑array. Καλή προγραμματιστική!

## Τι πρέπει να μάθετε επόμενα;

Τα παρακάτω tutorials καλύπτουν στενά σχετικότατα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε επιπλέον δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Create an Excel Workbook using Aspose.Cells in Java: A Step-by-Step Guide](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [How to Create & Format Excel Cells Using Aspose.Cells for Java: A Step-by-Step Guide](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)
- [How to Style Excel Cells and Add Hyperlinks Using Aspose.Cells for Java](/cells/english/java/formatting/style-excel-cells-hyperlinks-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}