---
category: general
date: 2026-03-30
description: Δημιουργήστε βιβλίο εργασίας Excel με C# με μορφοποίηση νομίσματος. Μάθετε
  πώς να εισάγετε ένα DataTable, να προσθέσετε μορφοποίηση αριθμών στο Excel και να
  εφαρμόσετε μορφοποίηση νομίσματος σε στήλη μέσα σε λίγα λεπτά.
draft: false
keywords:
- create excel workbook c#
- format cells currency
- import datatable to excel
- add number format excel
- apply currency format column
language: el
og_description: Δημιουργήστε βιβλίο εργασίας Excel με C# και μορφοποιήστε αμέσως τα
  κελιά ως νόμισμα. Αυτός ο οδηγός βήμα‑βήμα δείχνει πώς να εισάγετε ένα DataTable
  στο Excel και να προσθέσετε μορφοποίηση αριθμού για μια στήλη.
og_title: Δημιουργία βιβλίου εργασίας Excel C# – Οδηγός μορφοποίησης νομίσματος
tags:
- Aspose.Cells
- C#
- Excel automation
title: Δημιουργία βιβλίου εργασίας Excel C# – Εφαρμογή μορφής νομίσματος και εισαγωγή
  DataTable
url: /el/net/excel-data-import-export/create-excel-workbook-c-apply-currency-format-and-import-dat/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία Excel Workbook C# – Εφαρμογή Μορφής Νομίσματος και Εισαγωγή DataTable

Κάποτε χρειάστηκε να **δημιουργήσετε Excel workbook C#** που να μοιάζει ήδη με ένα επαγγελματικό αναφορά; Ίσως εξάγετε αριθμούς πωλήσεων από μια βάση δεδομένων και θέλετε η στήλη τιμής να εμφανίζεται σε δολάρια χωρίς να παίζετε με το Excel χειροκίνητα. Ακούγεται γνώριμο; Δεν είστε μόνοι—πολλοί προγραμματιστές αντιμετωπίζουν αυτό το πρόβλημα όταν αυτοματοποιούν τις εξαγωγές Excel για πρώτη φορά.

Σε αυτόν τον οδηγό θα περάσουμε βήμα‑βήμα από μια πλήρη, έτοιμη‑για‑εκτέλεση λύση που **δημιουργεί ένα Excel workbook C#**, εισάγει ένα `DataTable`, και **μορφοποιεί τη στήλη Price ως νόμισμα**. Στο τέλος θα έχετε ένα αρχείο που ονομάζεται `StyledTable.xlsx` το οποίο μπορείτε να ανοίξετε και να δείτε αριθμούς ωραία μορφοποιημένους. Δεν απαιτείται επιπλέον επεξεργασία.

> **Τι θα μάθετε**
> - Πώς να ρυθμίσετε το Aspose.Cells σε ένα .NET project  
> - Πώς να **import datatable to excel** με ένα style array  
> - Πώς να **add number format excel** για μια συγκεκριμένη στήλη  
> - Συμβουλές για τη διαχείριση περισσότερων στηλών ή διαφορετικών τοπικών ρυθμίσεων  

> **Προαπαιτούμενα**  
> - .NET 6+ (ή .NET Framework 4.6+) εγκατεστημένο  
> - Πακέτο NuGet Aspose.Cells for .NET (`Install-Package Aspose.Cells`)  
> - Βασική εξοικείωση με C# και DataTables  

---

## Step 1: Prepare the DataTable (import datatable to excel)

Πρώτα, χρειαζόμαστε κάποια δείγμα δεδομένων. Σε μια πραγματική εφαρμογή πιθανότατα θα γεμίσετε αυτόν τον πίνακα από ένα ερώτημα DB, αλλά ένα σκληρά κωδικοποιημένο παράδειγμα κρατά τα πράγματα απλά.

```csharp
using System.Data;

// Create a DataTable with two columns: Product (string) and Price (double)
DataTable dataTable = new DataTable();
dataTable.Columns.Add("Product", typeof(string));
dataTable.Columns.Add("Price", typeof(double));

// Add a few rows – you can add as many as you like
dataTable.Rows.Add("Apple", 1.23);
dataTable.Rows.Add("Banana", 0.78);
dataTable.Rows.Add("Cherry", 2.50);
```

*Γιατί είναι σημαντικό*: Το `DataTable` είναι η γέφυρα μεταξύ των επιχειρηματικών σας δεδομένων και του αρχείου Excel. Το Aspose.Cells μπορεί να το εισάγει απευθείας, διατηρώντας τα ονόματα στηλών και τους τύπους δεδομένων.

---

## Step 2: Spin Up a New Workbook (create excel workbook c#)

Τώρα δημιουργούμε το πραγματικό αντικείμενο αρχείου Excel. Σκεφτείτε το ως το κενό καμβά πάνω στον οποίο θα ζωγραφίσετε.

```csharp
using Aspose.Cells;

// Instantiate a fresh workbook – this is the core of create excel workbook c#
Workbook workbook = new Workbook();

// Grab the first worksheet (index 0). You could also add more sheets later.
Worksheet worksheet = workbook.Worksheets[0];
```

> **Pro tip:** Αν χρειάζεστε πολλαπλά φύλλα, καλέστε `workbook.Worksheets.Add()` και δώστε σε κάθε ένα ένα περιγραφικό όνομα.

---

## Step 3: Define a Currency Style (format cells currency)

Το Aspose.Cells σας επιτρέπει να δημιουργήσετε ένα αντικείμενο `Style` που περιγράφει πώς πρέπει να φαίνονται τα κελιά. Για νόμισμα χρησιμοποιούμε το ενσωματωμένο number format ID 164 (`"$#,##0.00"`).

```csharp
// Create a new style object for the price column
Style priceStyle = workbook.CreateStyle();
priceStyle.Number = 164; // Built‑in currency format "$#,##0.00"
```

*Γιατί να μην ορίσετε απλώς τη συμβολοσειρά μορφής;* Η χρήση του ενσωματωμένου ID εξασφαλίζει συμβατότητα μεταξύ εκδόσεων του Excel και αποφεύγει ιδιαιτερότητες τοπικών ρυθμίσεων.

---

## Step 4: Build the Style Array (apply currency format column)

Κατά την εισαγωγή ενός `DataTable`, μπορείτε να περάσετε έναν πίνακα αντικειμένων `Style`—ένα για κάθε στήλη. `null` σημαίνει “χρησιμοποίησε το προεπιλεγμένο στυλ”. Εδώ εφαρμόζουμε το `priceStyle` μόνο στη δεύτερη στήλη.

```csharp
// Column 0 (Product) gets the default style, Column 1 (Price) gets the currency style
Style[] columnStyles = { null, priceStyle };
```

Αν αργότερα προσθέσετε περισσότερες στήλες, απλώς επεκτείνετε τον πίνακα αναλόγως. Το μήκος του `columnStyles` πρέπει να ταιριάζει με τον αριθμό των στηλών που εισάγετε, διαφορετικά το Aspose θα πετάξει εξαίρεση.

---

## Step 5: Import the DataTable with Styles (import datatable to excel)

Τώρα συμβαίνει η μαγεία—το `DataTable` μας καταλήγει στο φύλλο εργασίας, και η στήλη τιμής εμφανίζεται αμέσως ως νόμισμα.

```csharp
// Parameters:
//  - dataTable: source data
//  - true: include column headers
//  - startRow: 0 (top of sheet)
//  - startColumn: 0 (first column)
//  - columnStyles: style array defined above
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
```

*Τι γίνεται αν έχετε περισσότερες από δύο στήλες;* Απλώς επεκτείνετε το `columnStyles` ώστε κάθε στήλη να λαμβάνει το κατάλληλο στυλ (ή `null` για προεπιλογή). Αυτός είναι ο πιο καθαρός τρόπος να **add number format excel** επιλεκτικά.

---

## Step 6: Save the Workbook (create excel workbook c#)

Τέλος, γράφουμε το αρχείο στο δίσκο. Επιλέξτε οποιονδήποτε φάκελο στον οποίο έχετε δικαίωμα εγγραφής.

```csharp
// Save the workbook as an XLSX file
workbook.Save("YOUR_DIRECTORY/StyledTable.xlsx");
```

Ανοίξτε το `StyledTable.xlsx` στο Excel και θα πρέπει να δείτε:

| Product | Price |
|---------|-------|
| Apple   | $1.23 |
| Banana  | $0.78 |
| Cherry  | $2.50 |

Η στήλη **Price** είναι ήδη μορφοποιημένη ως νόμισμα—χωρίς επιπλέον βήματα.

---

## Edge Cases & Variations

### More Columns, Different Formats

Αν χρειάζεται να **format cells currency** για πολλές στήλες (π.χ. Cost, Tax, Total), δημιουργήστε ξεχωριστό `Style` για κάθε μία και γεμίστε το `columnStyles` αναλόγως:

```csharp
Style costStyle = workbook.CreateStyle();
costStyle.Number = 164; // currency

Style taxStyle = workbook.CreateStyle();
taxStyle.Number = 164;

// Assuming columns: Product, Cost, Tax, Total
Style[] styles = { null, costStyle, taxStyle, priceStyle };
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, styles);
```

### Locale‑Specific Currency

Για Ευρώ ή Βρετανική Λίρα, χρησιμοποιήστε διαφορετικά ενσωματωμένα IDs (π.χ. 165 για `€#,##0.00`). Εναλλακτικά, ορίστε μια προσαρμοσμένη συμβολοσειρά μορφής:

```csharp
priceStyle.Custom = "€#,##0.00";
```

### Large Data Sets

Το Aspose.Cells μπορεί να διαχειριστεί εκατομμύρια γραμμές, αλλά η κατανάλωση μνήμης αυξάνεται με τα αντικείμενα στυλ. Επαναχρησιμοποιήστε ένα μόνο αντικείμενο `Style` για όλες τις στήλες νομίσματος ώστε να κρατήσετε το αποτύπωμα χαμηλό.

### Missing Styles

Αν το `columnStyles` είναι μικρότερο από τον αριθμό των στηλών, το Aspose θα εφαρμόσει το προεπιλεγμένο στυλ στις υπόλοιπες στήλες. Αυτό είναι χρήσιμο όταν σας ενδιαφέρουν μόνο λίγες στήλες.

---

## Full Working Example (All Steps Combined)

Παρακάτω είναι το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε‑και‑επικολλήσετε σε μια console app. Περιλαμβάνει όλα τα κομμάτια που συζητήσαμε, συν μερικά χρήσιμα σχόλια.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Build sample DataTable (import datatable to excel)
        // -------------------------------------------------
        DataTable dataTable = new DataTable();
        dataTable.Columns.Add("Product", typeof(string));
        dataTable.Columns.Add("Price", typeof(double));
        dataTable.Rows.Add("Apple", 1.23);
        dataTable.Rows.Add("Banana", 0.78);
        dataTable.Rows.Add("Cherry", 2.50);
        // You can add as many rows as you like here.

        // -------------------------------------------------
        // Step 2: Create a new workbook (create excel workbook c#)
        // -------------------------------------------------
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // -------------------------------------------------
        // Step 3: Define a currency style (format cells currency)
        // -------------------------------------------------
        Style priceStyle = workbook.CreateStyle();
        priceStyle.Number = 164; // "$#,##0.00" – built‑in currency format

        // -------------------------------------------------
        // Step 4: Build the style array (apply currency format column)
        // -------------------------------------------------
        // First column gets default style (null), second column uses priceStyle.
        Style[] columnStyles = { null, priceStyle };

        // -------------------------------------------------
        // Step 5: Import the DataTable with the style array
        // -------------------------------------------------
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

        // -------------------------------------------------
        // Step 6: Save the workbook to disk
        // -------------------------------------------------
        string outputPath = @"YOUR_DIRECTORY\StyledTable.xlsx";
        workbook.Save(outputPath);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

**Αναμενόμενο αποτέλεσμα:** Το άνοιγμα του `StyledTable.xlsx` δείχνει τη στήλη `Price` με σύμβολο δολαρίου και δύο δεκαδικά ψηφία, ακριβώς όπως απαιτεί η οδηγία **format cells currency**.

---

## Frequently Asked Questions

**Q: Does this work with .NET Core?**  
A: Absolutely. Aspose.Cells is .NET‑standard compliant, so you can target .NET 5, .NET 6, or later without changes.

**Q: What if my DataTable has 10 columns but I only want to format column 5?**  
A: Create a `Style[]` of length 10, fill positions 0‑4 and 6‑9 with `null`, and put your custom style at index 4 (zero‑based). Aspose will respect each entry.

**Q: Can I hide the header row?**  
A: After import, set `worksheet.Cells.Rows[0].Hidden = true;` or simply pass `false` for the `includeColumnNames` parameter in `ImportDataTable`.

---

## Conclusion

We’ve just **created an Excel workbook C#**, imported a `DataTable`, and **applied a currency format column** using Aspose.Cells. The primary steps—preparing data, defining a style, building a style array, importing with `ImportDataTable`, and saving—cover the core of most Excel‑automation tasks.

From here you might explore:

- **add number format excel** for dates or percentages  
- Exporting multiple worksheets in a single file  
- Using **format cells currency** with locale‑specific symbols  
- Automating chart creation based on the same data  

Give those a try, and you’ll quickly become the go‑to person for Excel reporting in your team. Got a twist you’d like to share? Drop a comment below—happy coding!  

![create excel workbook c# screenshot](image.png "create excel workbook c#")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}