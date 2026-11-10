---
category: general
date: 2026-09-27
description: Μάθετε πώς να διαγράψετε γραμμές από πίνακα Excel σε C# με έναν οδηγό
  βήμα‑βήμα που δείχνει επίσης πώς να φορτώσετε γρήγορα ένα βιβλίο εργασίας Excel
  σε C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- delete rows from Excel table
- load Excel workbook C#
language: el
lastmod: 2026-09-27
og_description: Διαγράψτε γραμμές από πίνακα Excel σε C# με ένα σαφές παράδειγμα.
  Αυτό το σεμινάριο καλύπτει επίσης πώς να φορτώσετε ένα βιβλίο εργασίας Excel σε
  C# και να αντιμετωπίσετε κοινές ειδικές περιπτώσεις.
og_image_alt: Screenshot illustrating delete rows from Excel table using C# code
og_title: Διαγραφή γραμμών από πίνακα Excel σε C# – πλήρης οδηγός κώδικα
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Learn how to delete rows from Excel table in C# with a step‑by‑step
    guide that also shows how to load Excel workbook C# quickly.
  headline: How to delete rows from Excel table using C#
  type: TechArticle
- description: Learn how to delete rows from Excel table in C# with a step‑by‑step
    guide that also shows how to load Excel workbook C# quickly.
  name: How to delete rows from Excel table using C#
  steps:
  - name: What if the table has a different name or position?
    text: '* **Named table:** Use `ws.ListObjects["MyTableName"]` instead of the index.
      * **Multiple tables:** Loop through `ws.ListObjects` and pick the one that matches
      a condition (e.g., column header names). * **Dynamic row count:** You can compute
      `rowCount` at runtime by inspecting `ws.ListObjects[0].Dat'
  - name: Edge‑case handling
    text: '| Situation | Recommended code change | |----------------------------------------|--------------------------------------------------------------|
      | Table is empty or has fewer rows | Check `ws.ListObjects[0].DataRange.RowCount`
      before deleting. | | Rows to delete exceed table size | Clamp `rowCount`'
  - name: How do I delete rows from **all** tables in a workbook?
    text: '```csharp foreach (Worksheet sheet in workbook.Worksheets) { foreach (ListObject
      tbl in sheet.ListObjects) { // Example: delete the first data row of each table
      if (tbl.DataRange.RowCount > 1) tbl.DeleteRows(1, 1); } } ```'
  - name: Can I delete rows based on a **cell value**?
    text: 'Yes. Scan the `DataRange` for matching cells, collect their zero‑based
      indices, then delete in descending order:'
  - name: What if I need to **preserve formatting**?
    text: '`DeleteRows` removes the entire row from the table but retains the table’s
      style for remaining rows. If you need to keep specific formatting on a row you’re
      deleting, copy the style to another row before deletion.'
  - name: Does this work with **.xls** (Excel 97‑2003) files?
    text: Yes. Aspose.Cells automatically detects the file format, so the same code
      works with `.xls`. Just change the file extension in the `Workbook` constructor.
  - name: Next steps
    text: '* Explore **ClosedXML** or **EPPlus** if you prefer a fully open‑source
      stack. * Combine row deletion with **data validation** to clean spreadsheets
      before importing into a database. * Automate the process for a folder of workbooks
      using `Directory.GetFiles` and a loop.'
  type: HowTo
tags:
- Excel
- C#
- .NET
title: Πώς να διαγράψετε γραμμές από πίνακα Excel χρησιμοποιώντας C#
url: /el/net/row-and-column-management/how-to-delete-rows-from-excel-table-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Διαγραφή γραμμών από πίνακα Excel σε C# – πλήρης προγραμματιστικός οδηγός

Αν χρειάζεστε **διαγραφή γραμμών από πίνακα Excel** σε αρχείο .xlsx, αυτό το tutorial σας δείχνει ακριβώς πώς να το κάνετε με C#. Θα δείτε ένα σύντομο, εκτελέσιμο παράδειγμα που φορτώνει ένα βιβλίο εργασίας Excel, αφαιρεί συγκεκριμένες γραμμές από τον πρώτο πίνακα και αποθηκεύει το αποτέλεσμα. Η προσέγγιση λειτουργεί με τη δημοφιλή βιβλιοθήκη Aspose.Cells και μπορεί να προσαρμοστεί σε άλλες .NET Excel APIs.

Η διαγραφή γραμμών από έναν πίνακα είναι μια συνηθισμένη εργασία όταν καθαρίζετε εισαγόμενα δεδομένα, περικόπτετε τμήματα αναφορών ή αυτοματοποιείτε ενημερώσεις υπολογιστικών φύλλων. Στο τέλος αυτού του οδηγού θα μπορείτε να **φορτώσετε βιβλίο εργασίας Excel C#**, να εντοπίσετε έναν πίνακα (ListObject), να διαγράψετε τις γραμμές που επιλέγετε και να γράψετε το τροποποιημένο αρχείο πίσω στο δίσκο.

## Προαπαιτούμενα

* .NET 6.0 ή νεότερο εγκατεστημένο (ο κώδικας λειτουργεί επίσης με .NET Framework 4.7+).
* Μια αναφορά στο πακέτο NuGet **Aspose.Cells** (ή οποιαδήποτε συμβατή βιβλιοθήκη που εκθέτει τύπους `Workbook`, `Worksheet` και `ListObject`).
* Ένα αρχείο εισόδου με όνομα `input.xlsx` τοποθετημένο σε φάκελο που μπορείτε να αναφέρετε από το έργο σας.
* Βασική εξοικείωση με τη σύνταξη C# και το Visual Studio (ή το προτιμώμενο IDE σας).

> **Συμβουλή:** Αν προτιμάτε μια ανοιχτού κώδικα εναλλακτική, η ίδια λογική μπορεί να εφαρμοστεί με **ClosedXML** – απλώς αντικαταστήστε τις κλάσεις ειδικές για Aspose με `XLWorkbook`, `IXLWorksheet` και `IXLTable`.

## Βήμα 1: Φόρτωση του βιβλίου εργασίας Excel σε C#

Η πρώτη ενέργεια είναι η ανάγνωση του αρχείου προέλευσης στη μνήμη. Η φόρτωση του βιβλίου εργασίας είναι ελαφριά για τυπικά μεγέθη υπολογιστικών φύλλων και σας δίνει πλήρη πρόσβαση σε φύλλα εργασίας, πίνακες και τιμές κελιών.

```csharp
using Aspose.Cells;

// Step 1: Load the workbook
// Replace YOUR_DIRECTORY with the actual folder path, e.g. @"C:\Data"
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");
```

*Γιατί είναι σημαντικό:* `Workbook` αναλύει τη δομή Open XML του αρχείου .xlsx, εκθέτοντας μια συλλογή από αντικείμενα `Worksheet`. Αν το αρχείο δεν βρεθεί, το Aspose ρίχνει ένα `FileNotFoundException`, οπότε βεβαιωθείτε ότι η διαδρομή είναι σωστή.

## Βήμα 2: Πρόσβαση στο στοχευμένο φύλλο εργασίας

Τα περισσότερα υπολογιστικά φύλλα περιέχουν πολλαπλά φύλλα· πρέπει να επιλέξετε αυτό που περιέχει τον πίνακα που θέλετε να τροποποιήσετε. Εδώ χρησιμοποιούμε το πρώτο φύλλο (`Worksheets[0]`), που είναι μια ασφαλής προεπιλογή για απλά αρχεία.

```csharp
// Step 2: Access the first worksheet
Worksheet ws = workbook.Worksheets[0];
```

*Γιατί είναι σημαντικό:* `Worksheet` είναι ο container για πίνακες (`ListObjects`). Η πρόσβαση στο σωστό φύλλο αποτρέπει τυχαίες αλλαγές σε μη σχεδεμένα δεδομένα.

## Βήμα 3: Διαγραφή γραμμών από πίνακα Excel

Οι πίνακες Excel αντιπροσωπεύονται από αντικείμενα `ListObject`. Ο πρώτος πίνακας στο φύλλο είναι `ListObjects[0]`. Η μέθοδος `DeleteRows(startIndex, rowCount)` αφαιρεί γραμμές **σχετικά με την περιοχή δεδομένων του πίνακα**, όχι με τους απόλυτους αριθμούς γραμμών του φύλλου.  

Σε αυτό το παράδειγμα διαγράφουμε τη δεύτερη και τρίτη γραμμή του πίνακα (η κεφαλίδα είναι γραμμή 0, οπότε ξεκινάμε από το index 1).

```csharp
// Step 3: Delete rows 1 and 2 from the first table (ListObject)
// The first row (index 0) is the header, so we start at index 1
ws.ListObjects[0].DeleteRows(1, 2);
```

### Τι γίνεται αν ο πίνακας έχει διαφορετικό όνομα ή θέση;

* **Ονομαστικός πίνακας:** Χρησιμοποιήστε `ws.ListObjects["MyTableName"]` αντί για το index.  
* **Πολλαπλοί πίνακες:** Κάντε βρόχο μέσω `ws.ListObjects` και επιλέξτε αυτόν που ταιριάζει με μια συνθήκη (π.χ., ονόματα κεφαλίδων στηλών).  
* **Δυναμικός αριθμός γραμμών:** Μπορείτε να υπολογίσετε το `rowCount` κατά την εκτέλεση εξετάζοντας το `ws.ListObjects[0].DataRange.RowCount`.

### Διαχείριση περιπτώσεων άκρων

| Κατάσταση                              | Συνιστώμενη αλλαγή κώδικα                                      |
|----------------------------------------|--------------------------------------------------------------|
| Ο πίνακας είναι κενός ή έχει λιγότερες γραμμές      | Ελέγξτε `ws.ListObjects[0].DataRange.RowCount` πριν τη διαγραφή. |
| Οι γραμμές προς διαγραφή υπερβαίνουν το μέγεθος του πίνακα       | Περιορίστε το `rowCount` σε `DataRange.RowCount - startIndex`.       |
| Χρειάζεται διαγραφή γραμμών βάσει συνθήκης (π.χ., τιμή στη στήλη C) | Επανάληψη στα `DataRange.Rows` και συλλογή των αντίστοιχων δεικτών, έπειτα διαγραφή με αντίστροφη σειρά για σταθερότητα δεικτών. |

## Βήμα 4: Αποθήκευση του τροποποιημένου βιβλίου εργασίας

Μετά τη διαγραφή, γράψτε το βιβλίο εργασίας πίσω σε νέο αρχείο (ή αντικαταστήστε το αρχικό αν προτιμάτε). Η αποθήκευση δημιουργεί ένα νέο .xlsx που αντικατοπτρίζει τον ενημερωμένο πίνακα.

```csharp
// Step 4: Save the modified workbook
workbook.Save(@"YOUR_DIRECTORY\output.xlsx");
```

*Γιατί είναι σημαντικό:* `Save` σειριοποιεί την αναπαράσταση στη μνήμη στο δίσκο. Αν χρειάζεται να διατηρήσετε το αρχικό αρχείο, πάντα γράψτε σε διαφορετική διαδρομή.

## Πλήρες, εκτελέσιμο παράδειγμα

Συνδυάζοντας όλα τα βήματα μαζί σας παρέχει ένα αυτόνομο πρόγραμμα που μπορείτε να αντιγράψετε, επικολλήσετε και εκτελέσετε.

```csharp
using System;
using Aspose.Cells;

class ExcelRowDeletion
{
    static void Main()
    {
        // Adjust the folder path as needed
        const string folder = @"YOUR_DIRECTORY";

        // Load the workbook (load Excel workbook C#)
        Workbook workbook = new Workbook($"{folder}\\input.xlsx");

        // Access the first worksheet
        Worksheet ws = workbook.Worksheets[0];

        // Ensure the worksheet contains at least one table
        if (ws.ListObjects.Count == 0)
        {
            Console.WriteLine("No tables found on the first worksheet.");
            return;
        }

        // Delete rows 1 and 2 from the first table (skip header)
        ListObject table = ws.ListObjects[0];
        int rowsToDelete = Math.Min(2, table.DataRange.RowCount - 1); // guard against short tables
        if (rowsToDelete > 0)
        {
            table.DeleteRows(1, rowsToDelete);
            Console.WriteLine($"Deleted {rowsToDelete} row(s) from table \"{table.Name}\".");
        }
        else
        {
            Console.WriteLine("Table does not have enough rows to delete.");
        }

        // Save the result
        workbook.Save($"{folder}\\output.xlsx");
        Console.WriteLine("Workbook saved as output.xlsx");
    }
}
```

**Αναμενόμενη έξοδος** (console):

```
Deleted 2 row(s) from table "Table1".
Workbook saved as output.xlsx
```

Ανοίξτε το `output.xlsx` – ο πρώτος πίνακας τώρα λείπουν οι γραμμές που αφαιρέσατε, ενώ η γραμμή κεφαλίδας παραμένει αμετάβλητη.

## Συχνές ερωτήσεις και παραλλαγές

### Πώς διαγράφω γραμμές από **όλους** τους πίνακες σε ένα βιβλίο εργασίας;

```csharp
foreach (Worksheet sheet in workbook.Worksheets)
{
    foreach (ListObject tbl in sheet.ListObjects)
    {
        // Example: delete the first data row of each table
        if (tbl.DataRange.RowCount > 1)
            tbl.DeleteRows(1, 1);
    }
}
```

### Μπορώ να διαγράψω γραμμές βάσει **τιμής κελιού**;

Ναι. Σαρώστε το `DataRange` για ταιριαστά κελιά, συλλέξτε τους μηδενικούς δείκτες, έπειτα διαγράψτε με φθίνουσα σειρά:

```csharp
var rowsToRemove = new List<int>();
for (int i = 0; i < table.DataRange.RowCount; i++)
{
    var cell = table.DataRange[i, 2]; // column C (zero‑based)
    if (cell.StringValue == "Obsolete")
        rowsToRemove.Add(i);
}

// Delete rows from bottom to top to keep indices valid
rowsToRemove.Sort((a, b) => b.CompareTo(a));
foreach (int rowIdx in rowsToRemove)
    table.DeleteRows(rowIdx, 1);
```

### Τι γίνεται αν χρειάζεται να **διατηρήσω τη μορφοποίηση**;

`DeleteRows` αφαιρεί ολόκληρη τη γραμμή από τον πίνακα αλλά διατηρεί το στυλ του πίνακα για τις υπόλοιπες γραμμές. Αν χρειάζεται να διατηρήσετε συγκεκριμένη μορφοποίηση σε μια γραμμή που διαγράφετε, αντιγράψτε το στυλ σε άλλη γραμμή πριν τη διαγραφή.

### Λειτουργεί αυτό με αρχεία **.xls** (Excel 97‑2003);

Ναι. Το Aspose.Cells εντοπίζει αυτόματα τη μορφή του αρχείου, έτσι ο ίδιος κώδικας λειτουργεί με `.xls`. Απλώς αλλάξτε την επέκταση του αρχείου στον κατασκευαστή `Workbook`.

## Συμβουλές απόδοσης

* **Διαγραφή σε παρτίδες:** Η διαγραφή πολλών γραμμών μία-μία μπορεί να είναι πιο αργή. Χρησιμοποιήστε μία κλήση `DeleteRows(start, count)` όταν είναι δυνατόν.  
* **Αποφυγή φραγής του UI thread:** Αν ενσωματώσετε αυτό σε εφαρμογή desktop, εκτελέστε τη διαχείριση του βιβλίου εργασίας σε νήμα παρασκηνίου για να διατηρήσετε το UI ανταποκρινόμενο.  
* **Κατάλληλη απελευθέρωση πόρων:** Παρόλο που το Aspose.Cells χρησιμοποιεί διαχειριζόμενη μνήμη, τυλίξτε το `Workbook` σε μπλοκ `using` αν εργάζεστε με μεγάλα αρχεία για να ελευθερώσετε τους πόρους άμεσα.

## Συμπέρασμα

Τώρα έχετε ένα πλήρες, έτοιμο για παραγωγή παράδειγμα που **διαγράφει γραμμές από πίνακα Excel** χρησιμοποιώντας C#. Ο οδηγός κάλυψε πώς να **φορτώσετε βιβλίο εργασίας Excel C#**, να εντοπίσετε το επιθυμητό `ListObject`, να αφαιρέσετε με ασφάλεια γραμμές και να αποθηκεύσετε το ενημερωμένο αρχείο. Με τη διαχείριση περιπτώσεων άκρων και τις συμβουλές απόδοσης που περιλαμβάνονται, μπορείτε να προσαρμόσετε αυτό το μοτίβο σε πιο σύνθετα σενάρια όπως διαγραφές βάσει συνθήκης, πολλαπλούς πίνακες ή εναλλακτικές βιβλιοθήκες .NET Excel.

### Επόμενα βήματα

* Εξερευνήστε το **ClosedXML** ή το **EPPlus** αν προτιμάτε μια πλήρως ανοιχτού κώδικα στοίβα.  
* Συνδυάστε τη διαγραφή γραμμών με **επαλήθευση δεδομένων** για να καθαρίσετε τα υπολογιστικά φύλλα πριν τα εισάγετε σε βάση δεδομένων.  
* Αυτοματοποιήστε τη διαδικασία για έναν φάκελο βιβλίων εργασίας χρησιμοποιώντας `Directory.GetFiles` και έναν βρόχο.

Μη διστάσετε να πειραματιστείτε με διαφορετικές περιοχές γραμμών, ονόματα πινάκων και λογική συνθηκών. Καλή προγραμματιστική!

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά σχετικές θεματικές που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικά παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Φόρτωση αρχείου Excel C# – Πώς να διαγράψετε γραμμές και να αφαιρέσετε συγκεκριμένες γραμμές](/cells/english/net/row-and-column-management/load-excel-file-c-how-to-delete-rows-and-remove-specific-row/)
- [Πώς να εισάγετε και να διαγράψετε γραμμές στο Excel με Aspose.Cells για .NET: Ένας ολοκληρωμένος οδηγός](/cells/english/net/data-manipulation/aspose-cells-net-insert-delete-excel-rows/)
- [Πώς να διαγράψετε κενές γραμμές στο Excel χρησιμοποιώντας Aspose.Cells .NET για καθαρισμό δεδομένων](/cells/english/net/data-manipulation/delete-blank-rows-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}