---
category: general
date: 2026-08-07
description: Αφαιρέστε το αυτόματο φίλτρο από το Excel σε C# γρήγορα. Μάθετε πώς να
  απενεργοποιήσετε το φίλτρο του Excel, να διαγράψετε το φίλτρο πίνακα του Excel και
  να καθαρίσετε το αυτόματο φίλτρο πίνακα του Excel με το Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- remove autofilter from excel
- how to turn off excel filter
- delete excel table filter
- clear excel table autofilter
language: el
lastmod: 2026-08-07
og_description: Αφαιρέστε το αυτόματο φίλτρο από το Excel σε C# και δείτε πώς να απενεργοποιήσετε
  το φίλτρο του Excel, να διαγράψετε το φίλτρο πίνακα του Excel και να καθαρίσετε
  το αυτόματο φίλτρο πίνακα του Excel χρησιμοποιώντας το Aspose.Cells.
og_image_alt: Screenshot showing an Excel sheet after remove autofilter from excel
og_title: Αφαίρεση του αυτόματου φίλτρου από το Excel σε C# – βήμα‑βήμα οδηγός
schemas:
- author: Aspose
  dateModified: '2026-08-07'
  description: Remove autofilter from Excel in C# quickly. Learn how to turn off Excel
    filter, delete Excel table filter, and clear Excel table autofilter with Aspose.Cells.
  headline: Remove autofilter from Excel in C# – complete guide
  type: TechArticle
- description: Remove autofilter from Excel in C# quickly. Learn how to turn off Excel
    filter, delete Excel table filter, and clear Excel table autofilter with Aspose.Cells.
  name: Remove autofilter from Excel in C# – complete guide
  steps:
  - name: Expected output
    text: 'Open `output.xlsx` in Excel:'
  - name: Multiple tables in the same worksheet
    text: 'If the worksheet contains more than one table, iterate over the collection:'
  - name: Removing filter from a specific column only
    text: 'Aspose.Cells does not expose a column‑level `AutoFilter` removal, but you
      can recreate the table without the filter:'
  - name: Working with older Excel formats (*.xls)
    text: Aspose.Cells supports the legacy binary format automatically. The same code
      works; just ensure the file extension matches the input file.
  - name: Handling large workbooks
    text: For files larger than 100 MB, enable the **LoadOptions** to use the **MemoryOptimized**
      mode, which reduces memory pressure while still allowing table manipulation.
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: Αφαίρεση του αυτόματου φίλτρου από το Excel σε C# – πλήρης οδηγός
url: /el/net/excel-autofilter-validation/remove-autofilter-from-excel-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Αφαίρεση autofilter από το Excel σε C# – πλήρης οδηγός

Αν χρειάζεστε **αφαίρεση autofilter από το Excel** κατά την επεξεργασία αρχείων προγραμματιστικά, αυτός ο οδηγός σας δείχνει ακριβώς πώς. Θα μάθετε τον πιο γρήγορο τρόπο για να **απενεργοποιήσετε το φίλτρο του Excel**, **διαγράψετε το φίλτρο πίνακα Excel** και **καθαρίσετε το autofilter πίνακα Excel** χρησιμοποιώντας τη βιβλιοθήκη Aspose.Cells.

Το tutorial καλύπτει τα πάντα, από τη ρύθμιση του έργου μέχρι την επαλήθευση ότι το παραγόμενο βιβλίο εργασίας δεν εμφανίζει πλέον βέλη φίλτρου. Δεν απαιτούνται χειροκίνητα βήματα και ο κώδικας λειτουργεί με οποιοδήποτε αρχείο .xlsx που περιέχει πίνακα με AutoFilter.

## Προαπαιτούμενα

- .NET 6.0 ή νεότερο εγκατεστημένο  
- Visual Studio 2022 (ή οποιοδήποτε IDE C#)  
- Άδεια για **Aspose.Cells for .NET** (η δωρεάν αξιολόγηση λειτουργεί για δοκιμές)  
- Ένα αρχείο Excel (`input.xlsx`) που περιέχει τουλάχιστον έναν πίνακα με ενεργό AutoFilter  

Θα χρειαστεί επίσης να προσθέσετε το πακέτο NuGet Aspose.Cells στο έργο σας:

```bash
dotnet add package Aspose.Cells
```

> **Pro tip:** Κρατήστε το βιβλίο εργασίας σε φάκελο που η εφαρμογή σας μπορεί να διαβάσει/γράψει χωρίς ανύψωση δικαιωμάτων για να αποφύγετε το `UnauthorizedAccessException`.

![αφαίρεση autofilter από το excel](/assets/remove-autofilter.png "αφαίρεση autofilter από το excel – Φύλλο Excel χωρίς βέλη φίλτρου")

## Αφαίρεση autofilter από το Excel – βήμα 1: φόρτωση του βιβλίου εργασίας

Η πρώτη ενέργεια είναι το άνοιγμα του πηγαίου βιβλίου εργασίας. Η φόρτωση του αρχείου στη μνήμη σας δίνει πλήρη πρόσβαση στα φύλλα εργασίας, τους πίνακες και τις ιδιότητές τους.

```csharp
using Aspose.Cells;

// Step 1: Load the workbook containing a table with an AutoFilter
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

*Γιατί είναι σημαντικό:* `Workbook` είναι το κεντρικό αντικείμενο στο Aspose.Cells. Αναλύει το πακέτο XLSX και δημιουργεί ένα μοντέλο αντικειμένων που αντικατοπτρίζει την εσωτερική δομή του Excel, επιτρέποντάς σας να χειρίζεστε τους πίνακες άμεσα.

## Πώς να απενεργοποιήσετε το φίλτρο του Excel – βήμα 2: πρόσβαση στο στόχο φύλλο εργασίας

Τα αρχεία Excel μπορούν να έχουν πολλά φύλλα εργασίας, αλλά το παράδειγμα εστιάζει στο πρώτο. Προσαρμόστε το δείκτη εάν τα δεδομένα σας βρίσκονται αλλού.

```csharp
// Step 2: Access the first worksheet (index 0)
Worksheet worksheet = workbook.Worksheets[0];
```

*Γιατί είναι σημαντικό:* Κάθε `Worksheet` περιέχει τη δική του συλλογή πινάκων. Ανακτώντας το σωστό φύλλο, διασφαλίζετε ότι τροποποιείτε τον επιθυμητό πίνακα.

## Διαγραφή φίλτρου πίνακα Excel – βήμα 3: εντοπισμός του πρώτου πίνακα

Οι πίνακες αποθηκεύονται στη συλλογή `Tables` ενός φύλλου εργασίας. Μπορείτε να τα επαναλάβετε, αλλά για απλότητα παίρνουμε τον πρώτο πίνακα.

```csharp
// Step 3: Retrieve the first table on the worksheet
Table table = worksheet.Tables[0];
```

*Γιατί είναι σημαντικό:* Το αντικείμενο `Table` περιέχει την ιδιότητα `AutoFilter` που ελέγχει το UI του φίλτρου. Η πρόσβαση στον πίνακα είναι προαπαιτούμενο για την αφαίρεση του φίλτρου.

## Καθαρισμός autofilter πίνακα Excel – βήμα 4: αφαίρεση του AutoFilter

Ορισμός της ιδιότητας `AutoFilter` σε `null` αφαιρεί εντελώς το UI του φίλτρου. Τα υποκείμενα δεδομένα παραμένουν αμετάβλητα.

```csharp
// Step 4: Remove the AutoFilter by setting it to null
table.AutoFilter = null;
```

*Γιατί είναι σημαντικό:* Όταν το `AutoFilter` είναι `null`, το Excel δεν εμφανίζει πλέον τα βέλη πτυσσόμενου μενού, και όλα τα προηγούμενα κριτήρια φίλτρου διαγράφονται. Αυτή είναι η βασική λειτουργία για **διαγραφή φίλτρου πίνακα Excel**.

## Αποθήκευση του βιβλίου εργασίας – βήμα 5: επαλήθευση του αποτελέσματος

Τέλος, γράψτε το τροποποιημένο βιβλίο εργασίας στο δίσκο. Το αποθηκευμένο αρχείο θα ανοίξει στο Excel χωρίς βέλη φίλτρου.

```csharp
// Step 5: Save the workbook; the table is now a plain data table without filter UI
workbook.Save("YOUR_DIRECTORY/output.xlsx");
```

### Αναμενόμενο αποτέλεσμα

Ανοίξτε το `output.xlsx` στο Excel:

- Ο πίνακας εμφανίζεται ως απλά δεδομένα—δεν εμφανίζονται βέλη φίλτρου στη γραμμή κεφαλίδας.  
- Όλες οι γραμμές είναι ορατές, επιβεβαιώνοντας ότι το φίλτρο έχει διαγραφεί.  

Αν εξακολουθείτε να βλέπετε βέλη, ελέγξτε ξανά ότι το πηγαίο αρχείο περιείχε πράγματι AutoFilter και ότι στοχεύσατε το σωστό δείκτη πίνακα.

## Συνηθισμένες παραλλαγές και ειδικές περιπτώσεις

### Πολλαπλοί πίνακες στο ίδιο φύλλο εργασίας

Αν το φύλλο εργασίας περιέχει περισσότερους από έναν πίνακες, επαναλάβετε τη συλλογή:

```csharp
foreach (Table tbl in worksheet.Tables)
{
    tbl.AutoFilter = null; // clear filter for each table
}
```

### Αφαίρεση φίλτρου μόνο από συγκεκριμένη στήλη

Το Aspose.Cells δεν εκθέτει αφαίρεση `AutoFilter` σε επίπεδο στήλης, αλλά μπορείτε να δημιουργήσετε ξανά τον πίνακα χωρίς το φίλτρο:

```csharp
// Capture existing data range
CellArea range = table.DisplayRange;

// Remove the table (including filter)
worksheet.Tables.RemoveAt(table.Index);

// Re‑add the table without AutoFilter
Table newTable = worksheet.Tables[worksheet.Tables.Add(range.StartRow, range.StartColumn, range.EndRow, range.EndColumn, true)];
```

### Εργασία με παλαιότερες μορφές Excel (*.xls)

Το Aspose.Cells υποστηρίζει αυτόματα τη παλαιότερη δυαδική μορφή. Ο ίδιος κώδικας λειτουργεί· απλώς βεβαιωθείτε ότι η επέκταση αρχείου ταιριάζει με το αρχείο εισόδου.

### Διαχείριση μεγάλων βιβλίων εργασίας

Για αρχεία μεγαλύτερα από 100 MB, ενεργοποιήστε τις **LoadOptions** για χρήση της λειτουργίας **MemoryOptimized**, η οποία μειώνει την πίεση μνήμης ενώ εξακολουθεί να επιτρέπει τη διαχείριση πινάκων.

```csharp
LoadOptions options = new LoadOptions(LoadFormat.Xlsx) { MemoryOptimization = true };
Workbook largeWorkbook = new Workbook("large_input.xlsx", options);
```

## Πλήρες, εκτελέσιμο παράδειγμα

Παρακάτω βρίσκεται το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε, επικολλήσετε και να εκτελέσετε ως εφαρμογή κονσόλας.

```csharp
using System;
using Aspose.Cells;

namespace RemoveExcelAutoFilter
{
    class Program
    {
        static void Main()
        {
            // Define file paths
            string inputPath = @"YOUR_DIRECTORY\input.xlsx";
            string outputPath = @"YOUR_DIRECTORY\output.xlsx";

            // Load the workbook
            Workbook workbook = new Workbook(inputPath);

            // Access the first worksheet
            Worksheet worksheet = workbook.Worksheets[0];

            // Ensure the worksheet contains at least one table
            if (worksheet.Tables.Count == 0)
            {
                Console.WriteLine("No tables found on the first worksheet.");
                return;
            }

            // Retrieve the first table and clear its AutoFilter
            Table table = worksheet.Tables[0];
            table.AutoFilter = null;

            // Save the modified workbook
            workbook.Save(outputPath);

            Console.WriteLine($"AutoFilter removed. Saved to {outputPath}");
        }
    }
}
```

Εκτελέστε το πρόγραμμα, στη συνέχεια ανοίξτε το `output.xlsx`. Θα δείτε ότι η λειτουργία **αφαίρεση autofilter από το excel** ολοκληρώθηκε με επιτυχία και το φύλλο εμφανίζει έναν απλό πίνακα δεδομένων.

## Συμπέρασμα

Τώρα ξέρετε πώς να **αφαιρέσετε autofilter από το Excel** χρησιμοποιώντας C#. Φορτώνοντας το βιβλίο εργασίας, προσπερνώντας τον στόχο πίνακα και ορίζοντας το `AutoFilter` σε `null`, μπορείτε να **απενεργοποιήσετε το φίλτρο του Excel**, **διαγράψετε το φίλτρο πίνακα Excel** και **καθαρίσετε το autofilter πίνακα Excel** σε ένα ενιαίο, αξιόπιστο βήμα.  

Στη συνέχεια, σκεφτείτε να εξερευνήσετε συναφή θέματα όπως **μορφοποίηση πινάκων Excel με Aspose.Cells**, **εξαγωγή φιλτραρισμένων δεδομένων σε CSV**, ή **εφαρμογή υπό συνθήκη μορφοποίησης προγραμματιστικά**. Κάθε ένα από αυτά βασίζεται στο ίδιο μοντέλο αντικειμένων που μόλις κατακτήσατε.

Μη διστάσετε να πειραματιστείτε με πολλαπλούς πίνακες, μεγάλα βιβλία εργασίας ή διαφορετικές μορφές αρχείων—η νέα σας δεξιότητα θα κάνει την αυτοματοποίηση του Excel πιο ομαλή και προβλέψιμη. Καλή προγραμματιστική!

## Τι Θα Πρέπει Να Μάθετε Στη Σύντομη Μελλοντική

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Καθαρισμός UI φίλτρου στο Excel με C# – Αφαίρεση κουμπιού AutoFilter](/cells/english/net/excel-autofilter-validation/clear-filter-ui-in-excel-with-c-remove-autofilter-button/)
- [Πώς να εφαρμόσετε AutoFilter στο Excel χρησιμοποιώντας Aspose.Cells για .NET (Οδηγός Ανάλυσης Δεδομένων)](/cells/english/net/data-analysis/implement-autofilter-excel-aspose-cells-dotnet/)
- [Πώς να εφαρμόσετε Excel Autofilter 'EndsWith' χρησιμοποιώντας Aspose.Cells για .NET](/cells/english/net/data-analysis/implement-autofilter-endswith-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}