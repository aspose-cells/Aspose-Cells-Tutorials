---
category: general
date: 2026-10-26
description: Απενεργοποίηση του autofilter στο Excel χρησιμοποιώντας C#. Αυτό το σεμινάριο
  δείχνει πώς να αφαιρέσετε το autofilter από πίνακα Excel προγραμματιστικά και περιλαμβάνει
  ένα πλήρες λειτουργικό παράδειγμα.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- disable autofilter in excel
- remove autofilter from excel table
- Excel automation C#
- Aspose.Cells filter handling
- programmatic Excel editing
language: el
lastmod: 2026-10-26
og_description: Απενεργοποιήστε γρήγορα το autofilter στο Excel. Ακολουθήστε αυτόν
  τον οδηγό για να αφαιρέσετε το autofilter από πίνακα Excel χρησιμοποιώντας C# και
  Aspose.Cells.
og_image_alt: Screenshot of an Excel worksheet where the autofilter has been disabled
og_title: Απενεργοποίηση του αυτόματου φίλτρου στο Excel με C# – οδηγός βήμα‑προς‑βήμα
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: disable autofilter in Excel using C#. This tutorial shows how to remove
    autofilter from Excel table programmatically and includes a full working example.
  headline: How to disable autofilter in Excel with C# – complete guide
  type: TechArticle
- description: disable autofilter in Excel using C#. This tutorial shows how to remove
    autofilter from Excel table programmatically and includes a full working example.
  name: How to disable autofilter in Excel with C# – complete guide
  steps:
  - name: Open the saved file (`Sample_NoFilter.xlsx`) in Microsoft Excel.
    text: Open the saved file (`Sample_NoFilter.xlsx`) in Microsoft Excel.
  - name: Click any column header – you should **not** see the drop‑down filter arrow.
    text: Click any column header – you should **not** see the drop‑down filter arrow.
  - name: 'If you still see arrows, double‑check that the table you targeted is indeed
      the one with the filter. You can list all tables with:'
    text: 'If you still see arrows, double‑check that the table you targeted is indeed
      the one with the filter. You can list all tables with:'
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: Πώς να απενεργοποιήσετε το autofilter στο Excel με C# – πλήρης οδηγός
url: /el/net/excel-autofilter-validation/how-to-disable-autofilter-in-excel-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να απενεργοποιήσετε το autofilter στο Excel με C# – πλήρης οδηγός

Αν χρειάζεστε να **απενεργοποιήσετε το autofilter στο Excel**, αυτός ο οδηγός σας δείχνει ακριβώς πώς να το κάνετε από C#. Είτε καθαρίζετε μια αναφορά πριν τη δημοσίευση είτε αυτοματοποιείτε μια διαδικασία εξαγωγής δεδομένων, η αφαίρεση του φίλτρου εξασφαλίζει ότι το φύλλο εργασίας εμφανίζει κάθε γραμμή. Θα μάθετε επίσης πώς να **αφαιρέσετε το autofilter από πίνακα Excel** με μία ενιαία, αξιόπιστη κλήση.

Θα χρησιμοποιήσουμε τη δημοφιλή βιβλιοθήκη **Aspose.Cells for .NET** επειδή λειτουργεί χωρίς να απαιτείται η εγκατάσταση του Excel στον διακομιστή. Στο τέλος αυτού του tutorial θα έχετε μια αυτόνομη εφαρμογή κονσόλας που φορτώνει ένα βιβλίο εργασίας, βρίσκει τον πρώτο πίνακα και απενεργοποιεί το autofilter του. Η λύση λειτουργεί με αρχεία .xlsx που δημιουργήθηκαν από το Excel 2007 ή νεότερο.

## Τι θα χρειαστείτε

| Προαπαιτούμενο | Γιατί είναι σημαντικό |
|----------------|-----------------------|
| .NET 6.0 or later | Παρέχει το runtime για τον κώδικα C#. |
| Aspose.Cells for .NET (NuGet package `Aspose.Cells`) | Παρέχει προγραμματισμένη πρόσβαση σε φύλλα εργασίας, πίνακες και autofilters. |
| Ένα δείγμα αρχείου Excel (`Sample.xlsx`) που περιέχει τουλάχιστον έναν πίνακα με ενεργό autofilter | Ο κώδικας λειτουργεί στον πρώτο πίνακα· η ύπαρξη πίνακα μας επιτρέπει να δείξουμε την απενεργοποίηση του φίλτρου. |
| Visual Studio 2022 (or any C# IDE) | Καθιστά την κατασκευή και την αποσφαλμάτωση της εφαρμογής κονσόλας απλή. |

> **Συμβουλή:** Αν προτιμάτε μια δωρεάν εναλλακτική, μπορείτε να προσαρμόσετε τον κώδικα ώστε να χρησιμοποιεί **ClosedXML** ή **EPPlus**· η κύρια ιδέα—ορισμός της ιδιότητας `AutoFilter` του πίνακα σε `null`—παραμένει η ίδια.

## Βήμα 1: Δημιουργήστε ένα νέο έργο κονσόλας

Ανοίξτε ένα τερματικό ή το command prompt του Visual Studio και εκτελέστε:

```bash
dotnet new console -n ExcelFilterDemo
cd ExcelFilterDemo
dotnet add package Aspose.Cells
```

Αυτό δημιουργεί ένα νέο έργο με όνομα `ExcelFilterDemo` και προσθέτει τη βιβλιοθήκη Aspose.Cells.

## Βήμα 2: Φορτώστε το βιβλίο εργασίας και εντοπίστε το πρώτο φύλλο εργασίας

Η πρώτη λογική ενέργεια είναι το άνοιγμα του αρχείου βιβλίου εργασίας. Το Aspose.Cells διαβάζει το αρχείο σε ένα αντικείμενο `Workbook` που σας δίνει άμεση πρόσβαση σε φύλλα εργασίας και πίνακες.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Path to the Excel file you want to modify
        const string inputPath = "Sample.xlsx";

        // Load the workbook into memory
        Workbook wb = new Workbook(inputPath);

        // Access the first worksheet (index 0)
        Worksheet worksheet = wb.Worksheets[0];
```

> **Γιατί αυτό το βήμα;** Η φόρτωση του βιβλίου εργασίας απαιτείται πριν μπορέσετε να χειριστείτε οποιαδήποτε αντικείμενα Excel. Η χρήση του πρώτου φύλλου (`Worksheets[0]`) αντικατοπτρίζει το τυπικό σενάριο όπου τα κύρια δεδομένα βρίσκονται στο πρώτο φύλλο.

## Βήμα 3: Ανακτήστε τον πρώτο πίνακα που ορίζεται στο φύλλο εργασίας

Οι πίνακες Excel (επίσης γνωστοί ως ListObjects) είναι οι δομές που περιέχουν δομημένα δεδομένα. Κάθε πίνακας μπορεί να έχει το δικό του autofilter. Για να αφαιρέσουμε το φίλτρο, χρειάζεται πρώτα μια αναφορά στο αντικείμενο του πίνακα.

```csharp
        // Get the first table on the worksheet.
        // If the worksheet has no tables, this will throw an IndexOutOfRangeException.
        Table table = worksheet.Tables[0];
```

> **Ακρόατο σενάριο:** Εάν το βιβλίο εργασίας μπορεί να περιέχει φύλλα χωρίς πίνακες, τυλίξτε την πρόσβαση σε έναν έλεγχο `if (worksheet.Tables.Count > 0)`. Αυτό αποτρέπει σφάλματα χρόνου εκτέλεσης και κάνει τη λύση πιο ανθεκτική.

## Βήμα 4: Απενεργοποιήστε το autofilter για τον πίνακα

Η πραγματική απενεργοποίηση είναι μια μόνο γραμμή: ορίστε `null` στην ιδιότητα `AutoFilter` του αντικειμένου `Table`. Αυτό αφαιρεί τυχόν κριτήρια φίλτρου και αφαιρεί τα βέλη των αναπτυσσόμενων λιστών από τη γραμμή κεφαλίδας.

```csharp
        // Disable the autofilter – this clears any applied filter.
        table.AutoFilter = null;
```

Αφού εκτελεστεί αυτή η γραμμή, ο πίνακας συμπεριφέρεται σαν ένα κανονικό εύρος χωρίς UI φίλτρου.

## Βήμα 5: Αποθηκεύστε το τροποποιημένο βιβλίο εργασίας

Τέλος, γράψτε τις αλλαγές πίσω στο δίσκο. Μπορείτε να αντικαταστήσετε το αρχικό αρχείο ή να δημιουργήσετε ένα νέο για να διατηρήσετε το αρχικό ανέπαφο.

```csharp
        // Save the workbook. Use a new file name to avoid overwriting the original.
        const string outputPath = "Sample_NoFilter.xlsx";
        wb.Save(outputPath);

        System.Console.WriteLine($"Autofilter disabled. Saved to {outputPath}");
    }
}
```

### Πλήρης κώδικας πηγής

Συνδυάζοντας όλα τα κομμάτια, το πλήρες πρόγραμμα φαίνεται ως εξής:

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Path to the original Excel file
        const string inputPath = "Sample.xlsx";

        // Load the workbook
        Workbook wb = new Workbook(inputPath);

        // Access the first worksheet
        Worksheet worksheet = wb.Worksheets[0];

        // Ensure the worksheet contains at least one table
        if (worksheet.Tables.Count == 0)
        {
            System.Console.WriteLine("No tables found on the first worksheet.");
            return;
        }

        // Get the first table
        Table table = worksheet.Tables[0];

        // Disable the autofilter – clears any applied filter
        table.AutoFilter = null;

        // Save the modified workbook
        const string outputPath = "Sample_NoFilter.xlsx";
        wb.Save(outputPath);

        System.Console.WriteLine($"Autofilter disabled. Saved to {outputPath}");
    }
}
```

Εκτελέστε το πρόγραμμα με `dotnet run`. Μετά την εκτέλεση, ανοίξτε το `Sample_NoFilter.xlsx` στο Excel· θα δείτε ότι τα βέλη φίλτρου έχουν εξαφανιστεί και όλες οι γραμμές είναι ορατές.

## Επαληθεύστε ότι το autofilter έχει πράγματι αφαιρεθεί

1. Ανοίξτε το αποθηκευμένο αρχείο (`Sample_NoFilter.xlsx`) στο Microsoft Excel.  
2. Κάντε κλικ σε οποιαδήποτε κεφαλίδα στήλης – δεν θα πρέπει να δείτε το βέλος του φίλτρου.  
3. Εάν εξακολουθείτε να βλέπετε βέλη, ελέγξτε ξανά ότι ο πίνακας που στοχεύσατε είναι πράγματι αυτός με το φίλτρο. Μπορείτε να εμφανίσετε όλους τους πίνακες με:

```csharp
foreach (var tbl in worksheet.Tables)
{
    System.Console.WriteLine($"Table name: {tbl.Name}, Has AutoFilter: {tbl.AutoFilter != null}");
}
```

Η έξοδος της κονσόλας θα πρέπει να αναφέρει `Has AutoFilter: False` για τον πίνακα που τροποποιήσατε.

## Συνηθισμένα προβλήματα και πώς να τα αποφύγετε

| Συμπτωμα | Πιθανή αιτία | Διόρθωση |
|----------|--------------|----------|
| `IndexOutOfRangeException` στο `worksheet.Tables[0]` | Το φύλλο εργασίας δεν έχει πίνακες. | Προσθέστε έλεγχο `if (worksheet.Tables.Count == 0)` πριν την πρόσβαση. |
| Το αποθηκευμένο αρχείο εξακολουθεί να εμφανίζει φίλτρα | Επεξεργαστήκατε το λάθος φύλλο ή πίνακα. | Χρησιμοποιήστε `wb.Worksheets["SheetName"]` ή επαναλάβετε μέσω `wb.Worksheets` για να εντοπίσετε τον σωστό πίνακα. |
| Το πρόγραμμα καταρρέει σε παλαιότερες εκδόσεις .NET | Το Aspose.Cells απαιτεί .NET 6.0+ για το τελευταίο πακέτο. | Αναβαθμίστε το target framework στο αρχείο `.csproj`. |
| NullReferenceException όταν το `table.AutoFilter` είναι ήδη null | Κλήσατε τον κώδικα δύο φορές στο ίδιο αρχείο χωρίς επαναφόρτωση. | Επαναφορτώστε το βιβλίο εργασίας ή ελέγξτε `if (table.AutoFilter != null)` πριν την ανάθεση. |

## Επεκτείνοντας τη λύση

Τώρα που ξέρετε πώς να **απενεργοποιήσετε το autofilter στο Excel**, ίσως θέλετε να:

* **Αφαιρέστε το autofilter από πίνακα Excel** μόνο όταν πληρούται μια συγκεκριμένη προϋπόθεση (π.χ., όταν έχει οριστεί μια σημαία χρήστη). Προσθέστε μια δήλωση `if` γύρω από το `table.AutoFilter = null;`.
* **Εφαρμόστε νέο φίλτρο** προγραμματιστικά μετά τον καθαρισμό του παλιού, χρησιμοποιώντας `table.AutoFilter.Range` και `table.AutoFilter.AddFilterColumn(...)`.
* **Επεξεργαστείτε πολλαπλούς πίνακες** στο ίδιο βιβλίο εργασίας επαναλαμβάνοντας μέσω `worksheet.Tables` και απενεργοποιώντας κάθε φίλτρο.

Αυτές οι επεκτάσεις ακολουθούν το ίδιο μοτίβο που παρουσιάστηκε παραπάνω και διατηρούν τον κώδικα καθαρό.

## Συμπέρασμα

Τώρα έχετε μια σύντομη, έτοιμη για παραγωγή μέθοδο να **απενεργοποιήσετε το autofilter στο Excel** χρησιμοποιώντας C#. Φορτώνοντας το βιβλίο εργασίας, προσπερνώντας τον πρώτο πίνακα και ορίζοντας `table.AutoFilter = null`, αφαιρείτε αποτελεσματικά **το autofilter από πίνακα Excel** χωρίς χειροκίνητη παρέμβαση. Το πλήρες παράδειγμα μεταγλωττίζεται, εκτελείται και παράγει ένα καθαρό αρχείο έτοιμο για περαιτέρω αυτοματοποίηση ή διανομή.

Μη διστάσετε να πειραματιστείτε με επιπλέον πίνακες, λογική συνθηκών ή εναλλακτικές βιβλιοθήκες. Εάν αντιμετωπίσετε κάποιο ακρόατο σενάριο, επιστρέψτε στην ενότητα αντιμετώπισης προβλημάτων ή εξερευνήστε την εκτενή τεκμηρίωση του Aspose.Cells για προχωρημένη διαχείριση φίλτρων. Καλή προγραμματιστική!

## Τι Θα Μάθετε Στη Σύντομη Μελλοντική

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κυριαρχήσετε σε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [How to remove autofilter from Excel tables using C#](/cells/english/net/excel-autofilter-validation/how-to-remove-autofilter-from-excel-tables-using-c/)
- [Clear filter UI in Excel with C# – Remove AutoFilter Button](/cells/english/net/excel-autofilter-validation/clear-filter-ui-in-excel-with-c-remove-autofilter-button/)
- [How to Use AutoFilter in C# Excel Automation – Full Step‑by‑Step Guide](/cells/english/net/excel-autofilter-validation/how-to-use-autofilter-in-c-excel-automation-full-step-by-ste/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}