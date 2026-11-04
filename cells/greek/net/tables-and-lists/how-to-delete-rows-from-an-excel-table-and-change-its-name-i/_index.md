---
category: general
date: 2026-10-01
description: Μάθετε πώς να διαγράφετε γραμμές από έναν πίνακα Excel και να αλλάζετε
  το όνομα του πίνακα Excel χρησιμοποιώντας C#. Οδηγός βήμα‑προς‑βήμα με πλήρες κώδικα
  και βέλτιστες πρακτικές.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- delete rows excel table
- change excel table name
- load excel workbook c#
- remove rows from excel table
- update excel table name
language: el
lastmod: 2026-10-01
og_description: Διαγράψτε γραμμές από έναν πίνακα Excel και αλλάξτε το όνομα του πίνακα
  Excel σε C#. Ακολουθήστε αυτό το πλήρες σεμινάριο για να φορτώσετε ένα βιβλίο εργασίας,
  να τροποποιήσετε τον πίνακα και να αποθηκεύσετε το αποτέλεσμα.
og_image_alt: Screenshot showing C# code that deletes rows from an Excel table and
  updates the table name
og_title: Διαγραφή γραμμών από πίνακα Excel και αλλαγή του ονόματός του σε C# – πλήρης
  οδηγός
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn to delete rows from an Excel table and change the Excel table
    name using C#. Step‑by‑step guide with full code and best practices.
  headline: How to delete rows from an Excel table and change its name in C#
  type: TechArticle
tags:
- C#
- Aspose.Cells
- Excel automation
title: Πώς να διαγράψετε γραμμές από έναν πίνακα Excel και να αλλάξετε το όνομά του
  σε C#
url: /el/net/tables-and-lists/how-to-delete-rows-from-an-excel-table-and-change-its-name-i/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να διαγράψετε γραμμές από έναν πίνακα Excel και να αλλάξετε το όνομά του σε C#

Αν χρειάζεται να **διαγράψετε γραμμές από έναν πίνακα Excel** ενώ εργάζεστε με C#, αυτός ο οδηγός δείχνει τα ακριβή βήματα που απαιτούνται. Θα δείτε πώς να **φορτώσετε ένα βιβλίο εργασίας Excel σε C#**, να αφαιρέσετε συγκεκριμένες γραμμές από έναν πίνακα και, στη συνέχεια, να **ενημερώσετε το όνομα του πίνακα Excel** ώστε το αρχείο να παραμένει συνεπές.

Ο οδηγός καλύπτει όλα όσα χρειάζεστε: τα απαιτούμενα πακέτα NuGet, πλήρη εκτελέσιμο κώδικα και κοινά προβλήματα όπως παραβιάσεις της δομής του πίνακα. Στο τέλος του άρθρου μπορείτε να τροποποιήσετε οποιονδήποτε πίνακα Excel προγραμματιστικά χωρίς χειροκίνητη παρέμβαση.

## Προαπαιτούμενα

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

* .NET 6.0 SDK ή νεότερη έκδοση εγκατεστημένη.
* Visual Studio 2022 (ή οποιοδήποτε IDE C#) ρυθμισμένο για ανάπτυξη .NET.
* Η βιβλιοθήκη **Aspose.Cells for .NET** προστέθηκε μέσω NuGet (`Install-Package Aspose.Cells`).
* Ένα υπάρχον βιβλίο εργασίας Excel (`Table.xlsx`) που περιέχει τουλάχιστον ένα φύλλο εργασίας με πίνακα.

Αυτά τα στοιχεία παρέχουν το περιβάλλον που απαιτείται για τον κώδικα **load Excel workbook c#** και την αξιόπιστη εκτέλεση των λειτουργιών.

## Βήμα 1: Φορτώστε το βιβλίο εργασίας που περιέχει τον πίνακα

Η πρώτη ενέργεια είναι το άνοιγμα του αρχείου βιβλίου εργασίας. Το Aspose.Cells διαβάζει ολόκληρο το βιβλίο εργασίας στη μνήμη, παρέχοντάς σας πλήρη έλεγχο πάνω στα φύλλα εργασίας, τους πίνακες και τα δεδομένα των κελιών.

```csharp
using Aspose.Cells;

string inputPath = @"C:\Data\Table.xlsx";

// Load the workbook from disk
Workbook workbook = new Workbook(inputPath);
```

*Γιατί είναι σημαντικό*: Η φόρτωση του βιβλίου εργασίας είναι η βάση για οποιαδήποτε επόμενη επεξεργασία πίνακα. Το αντικείμενο `Workbook` εκθέτει τη συλλογή `Worksheets`, την οποία θα χρησιμοποιήσετε για να εντοπίσετε τον στόχο πίνακα.

## Βήμα 2: Πρόσβαση στο πρώτο φύλλο εργασίας και στον πρώτο του πίνακα

Τα περισσότερα αρχεία Excel αποθηκεύουν πίνακες στο πρώτο φύλλο εργασίας, αλλά μπορείτε να προσαρμόσετε το δείκτη εάν χρειάζεται. Ο παρακάτω κώδικας ανακτά το πρώτο αντικείμενο `Table`.

```csharp
// Access the first worksheet (index 0)
Worksheet sheet = workbook.Worksheets[0];

// Retrieve the first table on that worksheet
Table table = sheet.Tables[0];
```

Εάν το φύλλο εργασίας δεν περιέχει πίνακα, το `sheet.Tables.Count` θα είναι μηδέν και θα πρέπει να διαχειριστείτε αυτήν την περίπτωση. Η προσπάθεια πρόσβασης στο `sheet.Tables[0]` όταν δεν υπάρχουν πίνακες προκαλεί εξαίρεση, γι' αυτό συνιστάται η χρήση guard clause σε κώδικα παραγωγής.

## Βήμα 3: Διαγραφή γραμμών από τον πίνακα Excel

Για να **αφαιρέσετε γραμμές από έναν πίνακα Excel**, καλέστε τη μέθοδο `DeleteRows(startRow, totalRows)`. Η παράμετρος `startRow` είναι μηδενική βάση σε σχέση με την πρώτη γραμμή δεδομένων του πίνακα (η γραμμή μετά την κεφαλίδα).

```csharp
// Delete two rows starting from the second data row (index 1)
int startRow = 1;   // second row within the table
int rowsToDelete = 2;

table.DeleteRows(startRow, rowsToDelete);
```

### Γιατί να χρησιμοποιήσετε το `DeleteRows` αντί για τη διαγραφή γραμμών φύλλου εργασίας;

Το `DeleteRows` ενημερώνει το εσωτερικό εύρος του πίνακα, διατηρώντας τύπους, στυλ και ορισμένα ονόματα που ανήκουν στον πίνακα. Η άμεση διαγραφή γραμμών φύλλου εργασίας θα μπορούσε να σπάσει τη δομή του πίνακα και να προκαλέσει εξαίρεση.

**Περίπτωση άκρης**: Εάν η διαγραφή θα άφηνε τον πίνακα χωρίς γραμμές δεδομένων, το Aspose.Cells ρίχνει `ArgumentException`. Προστατέψτε το ελέγχοντας το `table.RowCount` πριν τη διαγραφή.

```csharp
if (table.RowCount - rowsToDelete < 1)
{
    throw new InvalidOperationException("Cannot delete all data rows from the table.");
}
```

## Βήμα 4: Αλλαγή του ονόματος του πίνακα Excel

Αφού αφαιρεθούν οι γραμμές, μπορεί να θέλετε να δώσετε στον πίνακα ένα πιο περιγραφικό αναγνωριστικό. Η ιδιότητα `Name` ορίζει το καθορισμένο όνομα του πίνακα, το οποίο χρησιμοποιείται σε τύπους και VBA.

```csharp
// Assign a new name to the table
string newTableName = "SalesData2026";

if (workbook.Worksheets.GetDefinedNames().Any(d => d.Text == newTableName))
{
    throw new InvalidOperationException($"The name '{newTableName}' already exists as a defined name.");
}

table.Name = newTableName;
```

*Γιατί να μετονομάσετε;* Ένα σαφές όνομα πίνακα βελτιώνει την αναγνωσιμότητα σε τύπους (`=SUM(SalesData2026[Amount])`) και αποτρέπει συγκρούσεις ονομάτων όταν πολλοί πίνακες έχουν παρόμοιους σκοπούς.

## Βήμα 5: Αποθήκευση του τροποποιημένου βιβλίου εργασίας (προαιρετικό)

Διατηρήστε τις αλλαγές αποθηκεύοντας σε νέο αρχείο ή αντικαθιστώντας το αρχικό. Η αποθήκευση σε νέα θέση είναι πιο ασφαλής κατά την ανάπτυξη.

```csharp
string outputPath = @"C:\Data\ModifiedTable.xlsx";
workbook.Save(outputPath);
```

Η μέθοδος `Save` γράφει το ενημερωμένο βιβλίο εργασίας, συμπεριλαμβανομένου του τροποποιημένου εύρους πίνακα και του νέου ονόματος πίνακα, στο δίσκο.

## Πλήρες λειτουργικό παράδειγμα

Συνδυάζοντας όλα τα βήματα δημιουργείται ένα αυτόνομο πρόγραμμα που μπορείτε να εκτελέσετε αμέσως.

```csharp
using System;
using System.Linq;
using Aspose.Cells;

class ExcelTableModifier
{
    static void Main()
    {
        // ----- Step 1: Load workbook -----
        string inputPath = @"C:\Data\Table.xlsx";
        Workbook workbook = new Workbook(inputPath);

        // ----- Step 2: Access worksheet and table -----
        Worksheet sheet = workbook.Worksheets[0];
        if (sheet.Tables.Count == 0)
        {
            Console.WriteLine("No tables found on the first worksheet.");
            return;
        }

        Table table = sheet.Tables[0];

        // ----- Step 3: Delete rows -----
        int startRow = 1;      // second data row (zero‑based)
        int rowsToDelete = 2;

        if (table.RowCount - rowsToDelete < 1)
        {
            Console.WriteLine("Deletion would remove all data rows; operation aborted.");
            return;
        }

        table.DeleteRows(startRow, rowsToDelete);
        Console.WriteLine($"{rowsToDelete} rows removed starting at index {startRow}.");

        // ----- Step 4: Change table name -----
        string newTableName = "SalesData2026";

        bool nameExists = workbook.Worksheets.GetDefinedNames()
                               .Any(d => d.Text.Equals(newTableName, StringComparison.OrdinalIgnoreCase));

        if (nameExists)
        {
            Console.WriteLine($"The name '{newTableName}' already exists. Choose a different name.");
            return;
        }

        table.Name = newTableName;
        Console.WriteLine($"Table renamed to '{newTableName}'.");

        // ----- Step 5: Save workbook -----
        string outputPath = @"C:\Data\ModifiedTable.xlsx";
        workbook.Save(outputPath);
        Console.WriteLine($"Modified workbook saved to '{outputPath}'.");
    }
}
```

**Αναμενόμενο αποτέλεσμα** (υπόθεση ότι το αρχείο και ο πίνακας υπάρχουν):

```
2 rows removed starting at index 1.
Table renamed to 'SalesData2026'.
Modified workbook saved to 'C:\Data\ModifiedTable.xlsx'.
```

Η εκτέλεση του προγράμματος ενημερώνει το αρχείο Excel ακριβώς όπως περιγράφεται: οι γραμμές αφαιρούνται, το όνομα του πίνακα αλλάζει και το αποτέλεσμα αποθηκεύεται χωρίς χειροκίνητη επεξεργασία.

## Συχνές ερωτήσεις και αντιμετώπιση προβλημάτων

| Ερώτηση | Απάντηση |
|----------|--------|
| *Τι συμβαίνει αν ο πίνακας εκτείνεται σε συγχωνευμένα κελιά;* | `DeleteRows` σέβεται τις συγχωνευμένες περιοχές. Εάν ένα συγχωνευμένο κελί διασχίζει το όριο της διαγραφής, το Aspose.Cells προσαρμόζει αυτόματα τη συγχώνευση. Επαληθεύστε το αποτέλεσμα οπτικά εάν βασίζεστε σε σύνθετες συγχωνεύσεις. |
| *Μπορώ να διαγράψω γραμμές από έναν πίνακα που αποτελεί μέρος ενός pivot cache;* | Η διαγραφή γραμμών από έναν πίνακα προέλευσης που τροφοδοτεί έναν πίνακα pivot **δεν** ανανεώνει αυτόματα το pivot cache. Καλέστε `pivotTable.RefreshData()` μετά την τροποποίηση του πίνακα προέλευσης. |
| *Μπορεί να διαγραφούν γραμμές βάσει συνθήκης (π.χ., τιμή < 0);* | Ναι. Επανάληψη μέσω `table.ListObjects` ή `table.Rows` για να εντοπίσετε τις αντίστοιχες γραμμές, στη συνέχεια συλλέξτε τα ευρετήρια τους και καλέστε `DeleteRows` για κάθε εύρος. |
| *Πρέπει να απελευθερώσω το αντικείμενο `Workbook`;* | `Workbook` υλοποιεί το `IDisposable`. Τυλίξτε το σε ένα μπλοκ `using` για καθοριστική απελευθέρωση πόρων, ειδικά όταν επεξεργάζεστε μεγάλα αρχεία. |
| *Πώς διαφέρει αυτό από τη χρήση του EPPlus;* | Το EPPlus επίσης υποστηρίζει τη διαχείριση πινάκων, αλλά χρησιμοποιεί διαφορετικό API (`ExcelTable`). Οι έννοιες της φόρτωσης βιβλίου εργασίας, της διαγραφής γραμμών και της μετονομασίας του πίνακα είναι ανάλογες. Επιλέξτε τη βιβλιοθήκη που ταιριάζει στις απαιτήσεις αδειοδότησής σας. |

## Καλές πρακτικές κατά την τροποποίηση πινάκων Excel σε C#

* **Επικύρωση δεικτών** – Οι δείκτες γραμμών του πίνακα είναι μηδενικής βάσης· σφάλματα off‑by‑one προκαλούν απροσδόκητες διαγραφές.
* **Έλεγχος συγκρούσεων ονομάτων** – Το Excel δεν επιτρέπει διπλά ορισμένα ονόματα· πάντα επαληθεύετε τη μοναδικότητα πριν αναθέσετε νέο όνομα.
* **Δημιουργία αντιγράφου ασφαλείας των αρχικών αρχείων** – Τα αυτοματοποιημένα σενάρια μπορούν να καταστρέψουν δεδομένα· διατηρήστε ένα αντίγραφο του πηγαίου βιβλίου εργασίας.
* **Χρήση δηλώσεων `using`** – Εγγυάται ότι οι χειριστές αρχείων απελευθερώνονται άμεσα:

```csharp
using (Workbook wb = new Workbook(inputPath))
{
    // modify workbook
}
```

* **Δοκιμή με ακραίες περιπτώσεις** – Πίνακες με μία μόνο γραμμή δεδομένων, πίνακες που καλύπτουν ολόκληρο το φύλλο εργασίας και πίνακες συνδεδεμένοι με γραφήματα πρέπει να ελέγχονται μετά τις αλλαγές.

## Συμπέρασμα

Τώρα γνωρίζετε πώς να **διαγράψετε γραμμές από έναν πίνακα Excel** και να **αλλάξετε το όνομα του πίνακα Excel** χρησιμοποιώντας C#. Η πλήρης λύση φορτώνει το βιβλίο εργασίας, προσπελαύνει τον στόχο πίνακα, αφαιρεί τις επιθυμητές γραμμές, μετονομάζει τον πίνακα και αποθηκεύει το αποτέλεσμα. Εφαρμόστε αυτές τις τεχνικές για αυτοματοποίηση δημιουργίας αναφορών, καθαρισμού δεδομένων ή οποιασδήποτε ροής εργασίας που απαιτεί προγραμματισμένη διαχείριση πινάκων Excel.

Στη συνέχεια, εξερευνήστε συναφή θέματα όπως **ενημέρωση τιμών κελιών σε πίνακα Excel**, **προσθήκη νέων γραμμών προγραμματιστικά** και **εξαγωγή δεδομένων πίνακα σε CSV**. Η εξοικείωση με αυτές τις λειτουργίες θα σας δώσει πλήρη έλεγχο στα αρχεία Excel από τις εφαρμογές C#.

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά σχετικά θέματα που βασίζονται στις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να μετονομάσετε πίνακα στο Excel με C# – Οδηγός βήμα‑βήμα](/cells/english/net/tables-and-lists/how-to-rename-table-in-excel-with-c-step-by-step-guide/)
- [Δημιουργία πίνακα Excel σε C# – Οδηγός βήμα‑βήμα](/cells/english/net/tables-and-lists/create-excel-table-in-c-step-by-step-guide/)
- [Λήψη πρώτου πίνακα από βιβλίο εργασίας Excel σε C# – Πλήρης οδηγός](/cells/english/net/excel-autofilter-validation/get-first-table-from-excel-workbook-in-c-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}