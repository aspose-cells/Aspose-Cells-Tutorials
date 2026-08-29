---
category: general
date: 2026-07-20
description: Εφαρμόστε μορφοποίηση αριθμών στο Excel χρησιμοποιώντας Java και Aspose.Cells.
  Μάθετε πώς να εφαρμόζετε στυλ νομίσματος στο Excel, να δημιουργείτε βιβλίο εργασίας
  Excel με Java και να εισάγετε αποτελεσματικά DataTable στο Excel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- apply number format excel
- apply currency style excel
- create excel workbook java
- import datatable to excel
language: el
lastmod: 2026-07-20
og_description: Εφαρμόστε μορφοποίηση αριθμών στο Excel με Java. Αυτός ο οδηγός σας
  δείχνει πώς να εφαρμόσετε το στυλ νομίσματος στο Excel, να δημιουργήσετε βιβλίο
  εργασίας Excel με Java και να εισάγετε datatable στο Excel βήμα‑βήμα.
og_image_alt: Screenshot of an Excel workbook where apply number format excel has
  been applied to a currency column
og_title: Εφαρμογή μορφοποίησης αριθμών στο Excel με Java – Πλήρης οδηγός Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-07-20'
  description: Apply number format excel using Java and Aspose.Cells. Learn how to
    apply currency style excel, create excel workbook java, and import datatable to
    excel efficiently.
  headline: Apply Number Format Excel in Java – Complete Aspose.Cells Guide
  type: TechArticle
- questions:
  - answer: Absolutely. Open the workbook with `new Workbook("Existing.xlsx")`, fetch
      the target worksheet, and follow steps 3‑5 to apply the style array to new data.
    question: Can I apply the number format to an existing workbook?
  - answer: Use a different built‑in number index (`14` for short date, `22` for long
      date) or a custom format like `yyyy‑mm‑dd`. The workflow stays the same.
    question: What if I need to format dates instead of currency?
  - answer: 'Yes. Just change the file extension in `workbook.save("MyFile.xls")`.
      Aspose will automatically switch to the binary format. ## Wrap‑Up – What We
      Achieved We have **applied number format excel** to a column of monetary values,
      demonstrated how to **apply currency style excel**, shown the simplest wa'
    question: Does this work with older Excel versions (.xls)?
  type: FAQPage
tags:
- Aspose.Cells
- Java
- Excel Automation
title: Εφαρμογή Μορφής Αριθμού Excel σε Java – Πλήρης Οδηγός Aspose.Cells
url: /el/java/formatting/apply-number-format-excel-in-java-complete-aspose-cells-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εφαρμογή Μορφής Αριθμού Excel σε Java – Πλήρης Οδηγός Aspose.Cells

Έχετε αναρωτηθεί ποτέ πώς να **apply number format excel** απευθείας από κώδικα Java; Ίσως δημιουργείτε οικονομικές αναφορές ή χρειάζεστε έναν γρήγορο τρόπο να μορφοποιήσετε μια στήλη ποσών χωρίς να ανοίξετε το Excel χειροκίνητα. Τα καλά νέα; Με το Aspose.Cells μπορείτε να το κάνετε σε λίγες γραμμές, και θα μάθετε επίσης πώς να **apply currency style excel**, **create excel workbook java**, και **import datatable to excel** όλα σε μια τακτοποιημένη ρουτίνα.

Σε αυτό το tutorial θα περάσουμε από ένα πραγματικό παράδειγμα: μια λίστα ποσών αποθηκευμένη σε ένα Java `List<Map<String,Object>>` εισάγεται σε ένα νέο workbook, η πρώτη στήλη λαμβάνει μια ενσωματωμένη μορφή νομίσματος, και το αρχείο αποθηκεύεται έτοιμο για διανομή. Έτοιμοι να δείτε πόσο εύκολο είναι; Ας βουτήξουμε.

## Προαπαιτούμενα – Τι Θα Χρειαστείτε

- **Java Development Kit (JDK) 8+** – ο κώδικας εκτελείται σε οποιοδήποτε πρόσφατο JDK.
- **Aspose.Cells for Java** library (the Maven artifact `com.aspose:aspose-cells`) – αυτό είναι η μηχανή που μας επιτρέπει να χειριζόμαστε αρχεία Excel χωρίς εγκατεστημένο Office.
- A **favorite IDE** (IntelliJ IDEA, Eclipse, VS Code…) – οποιοσδήποτε επεξεργαστής θα κάνει, αλλά ένα IDE επιταχύνει τον εντοπισμό σφαλμάτων.
- Basic familiarity with **Java collections** – θα χρησιμοποιήσουμε ένα `List` of `Map`s για να προσομοιώσουμε ένα DataTable.

Αυτό είναι όλο. Χωρίς εξωτερικές υπηρεσίες, χωρίς εγκατάσταση Excel, μόνο καθαρή Java.

## Βήμα 1: Create Excel Workbook Java – Δημιουργία του Workbook

Το πρώτο πράγμα που χρειαζόμαστε είναι ένα αντικείμενο workbook. Σκεφτείτε το ως το κενό καμβά όπου θα ζήσουν όλα.

```java
// Step 1: Create a new workbook instance
Workbook workbook = new Workbook(); // creates an in‑memory Excel file
```

Γιατί να δημιουργήσουμε πρώτα το workbook; Το Aspose.Cells λειτουργεί εξ ολοκλήρου στη μνήμη, έτσι μπορείτε να προσθέσετε φύλλα, στυλ και δεδομένα πριν αγγίξετε το δίσκο. Αυτή η προσέγγιση είναι γρήγορη και διατηρεί τον κώδικά σας δοκιμαστέο.

## Βήμα 2: Prepare Data – Εισαγωγή Datatable στο Excel Χρησιμοποιώντας μια Λίστα από Maps

Σε πολλές επιχειρησιακές εφαρμογές τα δεδομένα προέρχονται από βάσεις δεδομένων ως πίνακες. Εδώ το προσομοιώνουμε με ένα `List<Map<String,Object>>`. Κάθε map αντιπροσωπεύει μια γραμμή, και το κλειδί `"Amount"` αντιστοιχεί σε μια αριθμητική τιμή.

```java
// Step 2: Build a DataTable‑like structure (list of maps)
List<Map<String, Object>> dataRows = new ArrayList<>();

// Row 1
dataRows.add(new HashMap<>() {{
    put("Amount", 1234.56);
}});
// Row 2
dataRows.add(new HashMap<>() {{
    put("Amount", 7890.12);
}});
```

Μπορεί να αναρωτηθείτε, “Γιατί να μην χρησιμοποιήσουμε ένα `ResultSet` ή POJOs;” Η μέθοδος `importDataTable` δέχεται οποιαδήποτε συλλογή που συμπεριφέρεται σαν DataTable, και μια λίστα από maps είναι ο πιο απλός τρόπος να δείξουμε την έννοια χωρίς να προσθέσουμε επιπλέον εξαρτήσεις.

## Βήμα 3: Define the Number Format – Apply Currency Style Excel

Τώρα έρχεται η καρδιά του tutorial: **apply number format excel**. Το Aspose.Cells παρέχει ενσωματωμένες μορφές αριθμών· η μορφή νομίσματος είναι στο index 5. Παίρνουμε το προεπιλεγμένο στυλ από το πρώτο φύλλο, τροποποιούμε τη μορφή αριθμού και το αποθηκεύουμε για μελλοντική χρήση.

```java
// Step 3: Get the default style and set a currency number format
Style currencyStyle = workbook.getWorksheets().get(0).getCells().getDefaultStyle();
currencyStyle.setNumber(5); // 5 = built‑in currency format ($#,##0.00)
```

Γιατί να χρησιμοποιήσουμε το προεπιλεγμένο στυλ ως βάση; Περιέχει ήδη τη προεπιλεγμένη γραμματοσειρά, στοίχιση και άλλες ρυθμίσεις του workbook, έτσι χρειάζεται να αλλάξετε μόνο ό,τι είναι σημαντικό—σε αυτήν την περίπτωση, τη μορφή αριθμού. Αν χρειάζεστε προσαρμοσμένη μορφή (π.χ., “€#,##0.00”), μπορείτε να καλέσετε `currencyStyle.setCustom("#,##0.00 €")`.

## Βήμα 4: Set Up Import Options – Σύνδεση του Πίνακα Στυλ

Το Aspose.Cells σας επιτρέπει να περάσετε έναν πίνακα αντικειμένων `Style` που αντιστοιχούν στις στήλες που εισάγονται. Επειδή τα δεδομένα μας έχουν μόνο μία στήλη, παρέχουμε έναν μονοστοιχειώδη πίνακα που περιέχει το στυλ νομίσματος.

```java
// Step 4: Configure import options with the style array
ImportTableOptions importOptions = new ImportTableOptions();
importOptions.setStyleArray(new Style[] { currencyStyle });
```

Αν ποτέ χρειαστεί να μορφοποιήσετε πολλές στήλες διαφορετικά, απλώς επεκτείνετε τον πίνακα: `new Style[] { styleForCol1, styleForCol2, … }`. Η σειρά των στυλ ταιριάζει με τη σειρά των στηλών στα δεδομένα προέλευσης.

## Βήμα 5: Import Data – Εισαγωγή του Datatable στο Worksheet

Με το workbook έτοιμο, τα δεδομένα προετοιμασμένα και τα στυλ ορισμένα, τελικά **import datatable to excel**. Ξεκινάμε από το κελί `A1`, συμπεριλαμβάνουμε τις επικεφαλίδες στηλών (`true`), και παραδίδουμε το `ImportTableOptions`.

```java
// Step 5: Perform the import
Worksheet worksheet = workbook.getWorksheets().get(0);
worksheet.getCells().importDataTable(dataRows, true, "A1", importOptions);
```

Παρατηρήστε τη σημαία `true`—το Aspose.Cells θα δημιουργήσει αυτόματα μια σειρά επικεφαλίδας βάσει των κλειδιών του map (`"Amount"`). Αν τη θέσετε σε `false`, η επικεφαλίδα θα παραλειφθεί, δίνοντάς σας μεγαλύτερο έλεγχο πάνω στην τελική διάταξη.

## Βήμα 6: Save the File – Create Excel Workbook Java στο Δίσκο

Το τελευταίο κομμάτι του παζλ είναι η αποθήκευση του workbook στη μνήμη σε ένα φυσικό αρχείο. Μπορείτε να επιλέξετε οποιαδήποτε μορφή υποστηρίζει το Aspose (`.xlsx`, `.xls`, `.csv`, …). Εδώ αποθηκεύουμε ως αρχείο XLSX.

```java
// Step 6: Save the workbook to disk
String outputPath = "DataTableWithCurrencyStyle.xlsx";
workbook.save(outputPath);
System.out.println("Workbook saved to " + outputPath);
```

Μετά την εκτέλεση του προγράμματος, ανοίξτε το παραγόμενο αρχείο. Θα δείτε τη στήλη `"Amount"` μορφοποιημένη με σύμβολο δολαρίου, δύο δεκαδικά ψηφία και σωστούς διαχωριστές χιλιάδων—ακριβώς αυτό που περιμένετε όταν **apply number format excel** για νομισματικές τιμές.

## Αναμενόμενο Αποτέλεσμα

| Amount |
|--------|
| $1,234.56 |
| $7,890.12 |

Η επικεφαλίδα “Amount” εμφανίζεται με έντονη γραφή (προεπιλεγμένο στυλ), και κάθε κελί κάτω από αυτήν δείχνει τη μορφή νομίσματος που ορίσαμε. Δεν απαιτείται χειροκίνητη μορφοποίηση στο Excel.

## Συμβουλές & Συνηθισμένα Παγίδες

- **Reuse Styles Wisely** – Τα στυλ είναι ελαφριά, αλλά η δημιουργία ενός νέου `Style` για κάθε κελί μπορεί να επηρεάσει την απόδοση. Πάντα επαναχρησιμοποιείτε ένα αντικείμενο στυλ όταν εφαρμόζετε την ίδια μορφή σε πολλά κελιά, όπως κάναμε με το `currencyStyle`.
- **Custom Formats** – Αν η περιοχή σας χρησιμοποιεί διαφορετικό σύμβολο νομίσματος, αντικαταστήστε το `currencyStyle.setNumber(5)` με `currencyStyle.setCustom("€#,##0.00")`. Δοκιμάστε τη μορφή στο Excel για να βεβαιωθείτε ότι λειτουργεί όπως αναμένεται.
- **Large Datasets** – Για χιλιάδες γραμμές, σκεφτείτε να χρησιμοποιήσετε το `importDataTable` με τη σημαία `ImportTableOptions.setImportDataOnly(true)` για να παραλείψετε τη δημιουργία επικεφαλίδας και να επιταχύνετε την εισαγωγή.
- **Thread Safety** – Τα αντικείμενα Aspose.Cells **δεν** είναι thread‑safe. Δημιουργήστε ένα ξεχωριστό `Workbook` ανά νήμα αν παράγετε αναφορές παράλληλα.

## Συχνές Ερωτήσεις

**Q: Μπορώ να εφαρμόσω τη μορφή αριθμού σε υπάρχον workbook;**  
A: Απόλυτα. Ανοίξτε το workbook με `new Workbook("Existing.xlsx")`, ανακτήστε το στοχευόμενο worksheet, και ακολουθήστε τα βήματα 3‑5 για να εφαρμόσετε τον πίνακα στυλ στα νέα δεδομένα.

**Q: Τι γίνεται αν χρειαστεί να μορφοποιήσω ημερομηνίες αντί για νόμισμα;**  
A: Χρησιμοποιήστε διαφορετικό ενσωματωμένο δείκτη αριθμού (`14` για σύντομη ημερομηνία, `22` για μακρά ημερομηνία) ή προσαρμοσμένη μορφή όπως `yyyy‑mm‑dd`. Η διαδικασία παραμένει η ίδια.

**Q: Λειτουργεί αυτό με παλαιότερες εκδόσεις του Excel (.xls);**  
A: Ναι. Απλώς αλλάξτε την επέκταση του αρχείου στο `workbook.save("MyFile.xls")`. Το Aspose θα μεταβεί αυτόματα στη δυαδική μορφή.

## Συμπέρασμα – Τι Καταφέραμε

Έχουμε **applied number format excel** σε μια στήλη χρηματικών τιμών, δείξαμε πώς να **apply currency style excel**, παρουσιάσαμε τον πιο απλό τρόπο για **create excel workbook java**, και χρησιμοποιήσαμε το Aspose.Cells για **import datatable to excel** χωρίς να αγγίξουμε το UI. Όλα αυτά έγιναν σε ένα σύντομο, αυτόνομο πρόγραμμα που μπορείτε να αντιγράψετε, επικολλήσετε και εκτελέσετε.

Τι ακολουθεί; Δοκιμάστε να επεκτείνετε το παράδειγμα:

- Προσθέστε περισσότερες στήλες (π.χ., “Date”, “Description”) και αναθέστε διαφορετικά στυλ ανά στήλη.
- Εξάγετε τα ίδια δεδομένα σε CSV και συγκρίνετε πώς χάνονται οι μορφές αριθμών.
- Ενσωματώστε τον κώδικα σε μια υπηρεσία Spring Boot που επιστρέφει το workbook ως λήψιμο HTTP response.

Μη διστάσετε να πειραματιστείτε, και αν αντιμετωπίσετε προβλήματα, αφήστε ένα σχόλιο παρακάτω. Καλή προγραμματιστική!

## Τι Θα Μάθετε Στη Σύντομη Μελλοντική;

Τα παρακάτω tutorials καλύπτουν στενά σχετικές θεματικές που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε σε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να Εφαρμόσετε Στυλ σε Κελιά Excel Χρησιμοποιώντας Aspose.Cells για Java - Πλήρης Οδηγός](/cells/english/java/formatting/apply-styles-excel-aspose-cells-java/)
- [Συγχώνευση Κελιών & Εφαρμογή Στυλ σε Excel χρησιμοποιώντας Aspose.Cells για Java - Πλήρης Οδηγός](/cells/english/java/formatting/merge-cells-apply-styles-aspose-cells-java/)
- [Aspose.Cells for Java&#58; Πώς να Δημιουργήσετε και να Μορφοποιήσετε Excel Workbooks Αποτελεσματικά](/cells/english/java/getting-started/aspose-cells-java-workbook-creation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}