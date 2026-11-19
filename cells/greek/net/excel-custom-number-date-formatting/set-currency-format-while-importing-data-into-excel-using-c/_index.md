---
category: general
date: 2026-11-19
description: Ορίστε μορφή νομίσματος στο Excel με C# – μάθετε πώς να ορίζετε μορφή
  αριθμού και στυλ των στηλών του Excel κατά την εισαγωγή ενός φύλλου εργασίας.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set currency format
- how to set number format
- assign number format
- excel worksheet import
- style excel columns
language: el
lastmod: 2026-11-19
og_description: Ορίστε μορφή νομίσματος στο Excel με C# και ανακαλύψτε πώς να ορίσετε
  μορφή αριθμού, να αναθέσετε μορφή αριθμού και να μορφοποιήσετε στήλες του Excel
  κατά την εισαγωγή φύλλου εργασίας Excel.
og_image_alt: Screenshot showing Excel cells formatted as currency after import
og_title: Ορισμός μορφής νομίσματος στο Excel με C# – πλήρης οδηγός βήμα‑προς‑βήμα
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Set currency format in Excel with C# – learn how to set number format
    and style excel columns during an excel worksheet import.
  headline: Set currency format while importing data into Excel using C#
  type: TechArticle
- description: Set currency format in Excel with C# – learn how to set number format
    and style excel columns during an excel worksheet import.
  name: Set currency format while importing data into Excel using C#
  steps:
  - name: Expected result
    text: 'When you open **FinancialReport.xlsx**, you’ll see:'
  - name: Assign number format to date columns
    text: '```csharp // Suppose column 2 contains dates and you want "dd-MMM-yyyy"
      columnStyles[2].Number = 14; // 14 = built‑in short date ```'
  - name: Use custom number formats for percentages
    text: '```csharp columnStyles[3].Custom = "0.00%"; // Shows 0.75 as 75.00% ```'
  - name: Styling beyond number formats
    text: 'You can also set font, background color, or alignment on the same `Style`
      object:'
  type: HowTo
tags:
- C#
- Excel
- DataTable
- Aspose.Cells
- Formatting
title: Ορισμός μορφής νομίσματος κατά την εισαγωγή δεδομένων στο Excel χρησιμοποιώντας
  C#
url: /el/net/excel-custom-number-date-formatting/set-currency-format-while-importing-data-into-excel-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ορισμός μορφής νομίσματος κατά την εισαγωγή δεδομένων στο Excel χρησιμοποιώντας C#

Αν χρειάζεται να **ορίσετε μορφή νομίσματος** σε ένα φύλλο εργασίας του Excel, αυτός ο οδηγός σας δείχνει πώς να **ορίσετε μορφή αριθμού** και να μορφοποιήσετε τις στήλες κατά την εκτέλεση μιας **εισαγωγής φύλλου εργασίας Excel**. Θα δείτε ένα πλήρες, εκτελέσιμο παράδειγμα που αναθέτει τη σωστή μορφή αριθμού σε κάθε στήλη ενός `DataTable` και εισάγει τα δεδομένα με το επιθυμητό στυλ.

Η εργασία με το Excel από C# συχνά απαιτεί περισσότερα από το απλό άδειο γράψιμο τιμών — πρέπει επίσης να ελέγχετε πώς εμφανίζονται οι αριθμοί. Είτε δημιουργείτε τιμολόγια, οικονομικές αναφορές ή πίνακες ελέγχου, η σωστή μορφοποίηση νομίσματος, ποσοστών ή ημερομηνιών κάνει το αποτέλεσμα άμεσα αναγνώσιμο.

## Προαπαιτούμενα

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

* .NET 6.0 (ή νεότερη) εγκατεστημένη.
* Αναφορά στο **Aspose.Cells for .NET** (ή οποιαδήποτε βιβλιοθήκη που εκθέτει μια κλάση `Style` με ιδιότητα `Number`).  
  *NuGet*: `Install-Package Aspose.Cells`.
* Βασική εξοικείωση με `DataTable` και συλλογές C#.
* Ένα IDE όπως το Visual Studio 2022 ή το VS Code.

## Βήμα 1: Ανάκτηση των δεδομένων που θα γραφτούν στο φύλλο εργασίας

Πρώτα αποκτήστε ένα `DataTable` που περιέχει τα ακατέργαστα δεδομένα που θέλετε να εξάγετε. Σε πραγματικά έργα αυτό μπορεί να προέρχεται από ερώτημα βάσης δεδομένων, κλήση API ή parser CSV.

```csharp
using System.Data;

/// <summary>
/// Returns a sample DataTable with three columns:
/// Id (int), Amount (decimal), and Description (string).
/// </summary>
DataTable GetData()
{
    var table = new DataTable();
    table.Columns.Add("Id", typeof(int));
    table.Columns.Add("Amount", typeof(decimal));
    table.Columns.Add("Description", typeof(string));

    // Sample rows
    table.Rows.Add(1, 1234.56m, "Office supplies");
    table.Rows.Add(2, 98765.43m, "Consulting fees");
    table.Rows.Add(3, 0.99m, "Miscellaneous");

    return table;
}

// Retrieve the data
DataTable dataTable = GetData();
```

> **Γιατί είναι σημαντικό:** Η εισαγωγή ενός πλήρως γεμάτου `DataTable` σας επιτρέπει να διαχωρίσετε τη λογική ανάκτησης δεδομένων από τη λογική δημιουργίας Excel, βελτιώνοντας τη δοκιμασιμότητα και τη συντηρησιμότητα.

## Βήμα 2: Δημιουργία πίνακα στυλ – μία καταχώρηση ανά στήλη του DataTable

Το Aspose.Cells αναμένει ένα `Style[]` του οποίου το μήκος ταιριάζει με τον αριθμό των στηλών που σκοπεύετε να εισάγετε. Κάθε στοιχείο μπορεί να περιέχει μια συγκεκριμένη μορφή αριθμού.

```csharp
// Allocate a Style object for each column
Style[] columnStyles = new Style[dataTable.Columns.Count];

// Initialize each Style instance (required before assigning properties)
for (int i = 0; i < columnStyles.Length; i++)
{
    columnStyles[i] = ws.Workbook.CreateStyle();
}
```

> **Pro tip:** Ακόμη και αν χρειάζεστε μορφοποίηση μόνο για ένα υποσύνολο στηλών, πρέπει να δημιουργήσετε μια παρουσία `Style` για κάθε στήλη· διαφορετικά θα λάβετε `NullReferenceException` κατά την εισαγωγή.

## Βήμα 3: Ανάθεση μορφής αριθμού στις επιθυμητές στήλες

Οι ενσωματωμένοι αριθμοί στυλ διαφέρουν ανά βιβλιοθήκη. Στο Aspose.Cells:

* `0` → Γενική (ακέραιος)  
* `2` → Νόμισμα (π.χ., `$#,##0.00`)  
* `3` → Ημερομηνία, κ.λπ.

Εδώ **αναθέτουμε μορφή αριθμού** σε δύο στήλες: η πρώτη στήλη (Id) παραμένει ακέραιος, ενώ η δεύτερη στήλη (Amount) λαμβάνει μορφή νομίσματος.

```csharp
// Column 0 → integer format (style number 0)
columnStyles[0].Number = 0;

// Column 1 → currency format (style number 2)
columnStyles[1].Number = 2;

// If you need a custom format, you can also use a format string:
// columnStyles[1].Custom = "$#,##0.00";
```

> **Πώς να ορίσετε μορφή αριθμού:** Η χρήση της ιδιότητας `Number` είναι ο πιο γρήγορος τρόπος για να επιλέξετε μια ενσωματωμένη μορφή. Για νομίσματα ειδικών τοπικών ρυθμίσεων, σκεφτείτε να χρησιμοποιήσετε μια προσαρμοσμένη συμβολοσειρά μορφής που περιλαμβάνει το κατάλληλο σύμβολο νομίσματος.

## Βήμα 4: Εισαγωγή του DataTable στο φύλλο εργασίας, εφαρμόζοντας τα στυλ των στηλών

Τώρα που ο πίνακας στυλ είναι έτοιμος, εισάγετε τα δεδομένα. Η μέθοδος `ImportDataTable` σέβεται τα στυλ που περάσατε.

```csharp
// Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();
Worksheet ws = workbook.Worksheets[0];

// Import the DataTable, starting at cell A1 (row 0, column 0)
// The third argument (true) tells the method to write column headers.
ws.Cells.ImportDataTable(
    dataTable,
    /* includeColumnNames */ true,
    /* startRow */ 0,
    /* startColumn */ 0,
    columnStyles);

// Save the workbook
workbook.Save("FinancialReport.xlsx", SaveFormat.Xlsx);
```

### Αναμενόμενο αποτέλεσμα

Όταν ανοίξετε το **FinancialReport.xlsx**, θα δείτε:

| Id | Amount      | Description      |
|----|------------|------------------|
| 1  | $1,234.56  | Office supplies |
| 2  | $98,765.43 | Consulting fees |
| 3  | $0.99      | Miscellaneous    |

*Η στήλη **Amount** εμφανίζεται με τη μορφή νομίσματος που ορίσατε, ενώ η **Id** παραμένει ακέραιος.*

## Πώς να ορίσετε μορφή αριθμού για επιπλέον σενάρια

### Ανάθεση μορφής αριθμού σε στήλες ημερομηνίας

```csharp
// Suppose column 2 contains dates and you want "dd-MMM-yyyy"
columnStyles[2].Number = 14; // 14 = built‑in short date
```

### Χρήση προσαρμοσμένων μορφών αριθμού για ποσοστά

```csharp
columnStyles[3].Custom = "0.00%"; // Shows 0.75 as 75.00%
```

### Μορφοποίηση πέρα από τις μορφές αριθμού

Μπορείτε επίσης να ορίσετε γραμματοσειρά, χρώμα φόντου ή στοίχιση στο ίδιο αντικείμενο `Style`:

```csharp
columnStyles[1].Font.IsBold = true;
columnStyles[1].ForegroundColor = Color.LightYellow;
columnStyles[1].HorizontalAlignment = TextAlignmentType.Center;
```

> **Γιατί λειτουργεί:** Το αντικείμενο `Style` συγκεντρώνει όλες τις οπτικές ιδιότητες ενός κελιού. Όταν περνάτε τον πίνακα στη `ImportDataTable`, κάθε κελί κληρονομεί αυτόματα το ορισμένο στυλ.

## Συνηθισμένα προβλήματα και πώς να τα αποφύγετε

| Πρόβλημα | Συμπτωμα | Διόρθωση |
|----------|----------|----------|
| Παράλειψη δημιουργίας κάθε `Style` | `NullReferenceException` κατά την εισαγωγή | Κάντε βρόχο στον πίνακα και καλέστε `CreateStyle()` πριν ορίσετε ιδιότητες. |
| Χρήση λανθασμένου ενσωματωμένου αριθμού μορφής | Λάθος μορφή (π.χ., οι ημερομηνίες εμφανίζονται ως ακέραιοι) | Συμβουλευτείτε την τεκμηρίωση της βιβλιοθήκης για τις σωστές σταθερές `Number`. |
| Μη αποθήκευση του βιβλίου εργασίας | Δεν δημιουργείται αρχείο ή είναι κενό | Καλέστε `workbook.Save(...)` μετά την ολοκλήρωση της εισαγωγής. |
| Ασυμφωνία τοπικής ρύθμισης για το σύμβολο νομίσματος | Το `$` εμφανίζεται ακόμη και σε μη‑αμερικανικές περιοχές | Χρησιμοποιήστε προσαρμοσμένη συμβολοσειρά μορφής με το κατάλληλο σύμβολο (π.χ., `"€#,##0.00"`). |

## Πλήρες, εκτελέσιμο παράδειγμα



## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά σχετικές θεματικές που επεκτείνουν τις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να κυριαρχήσετε σε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στα δικά σας έργα.

- [Δημιουργία αρχείου Excel c# – μορφοποίηση κελιών και ορισμός μορφής νομίσματος](/cells/english/net/excel-formatting-and-styling/create-excel-file-c-style-cells-and-set-currency-format/)
- [Πώς να μορφοποιήσετε στήλες Excel σε C# – Πλήρης Οδηγός](/cells/english/net/formatting-rows-and-columns-in-excel/how-to-format-excel-columns-in-c-complete-guide/)
- [Δημιουργία βιβλίου εργασίας Excel C# – Εφαρμογή μορφής νομίσματος και εισαγωγή DataTable](/cells/english/net/excel-data-import-export/create-excel-workbook-c-apply-currency-format-and-import-dat/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}