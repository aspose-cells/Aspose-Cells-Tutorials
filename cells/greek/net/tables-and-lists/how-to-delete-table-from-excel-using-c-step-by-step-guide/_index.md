---
category: general
date: 2026-11-19
description: Μάθετε πώς να διαγράψετε πίνακα από το Excel σε C#. Αυτό το σεμινάριο
  δείχνει επίσης πώς να διαβάσετε αρχείο Excel σε C# και να φορτώσετε βιβλίο εργασίας
  Excel σε C# με ένα πλήρες παράδειγμα κώδικα.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- delete table from excel
- read excel file c#
- how to remove table excel
- load excel workbook c#
- how to delete excel table
language: el
lastmod: 2026-11-19
og_description: Διαγράψτε πίνακα από το Excel σε C# γρήγορα. Ακολουθήστε αυτόν τον
  οδηγό για να διαβάσετε αρχείο Excel σε C# και να φορτώσετε βιβλίο εργασίας Excel
  σε C# με ένα λειτουργικό παράδειγμα.
og_image_alt: Screenshot of C# code that deletes a table from an Excel worksheet
og_title: Διαγραφή πίνακα από το Excel σε C# – πλήρης οδηγός προγραμματισμού
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Learn how to delete table from Excel in C#. This tutorial also shows
    how to read Excel file C# and load Excel workbook C# with a complete code example.
  headline: How to delete table from Excel using C# – step‑by‑step guide
  type: TechArticle
tags:
- C#
- Excel automation
- Aspose.Cells
title: Πώς να διαγράψετε πίνακα από το Excel χρησιμοποιώντας C# – βήμα‑βήμα οδηγός
url: /el/net/tables-and-lists/how-to-delete-table-from-excel-using-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να διαγράψετε πίνακα από το Excel χρησιμοποιώντας C# – οδηγός βήμα‑βήμα

Αν χρειάζεστε να **διαγράψετε πίνακα από το Excel** προγραμματιστικά, αυτός ο οδηγός σας δείχνει ακριβώς πώς να το κάνετε με C#. Θα δείτε ένα πλήρες, εκτελέσιμο παράδειγμα που φορτώνει ένα βιβλίο εργασίας Excel, αφαιρεί τον πρώτο πίνακα και αποθηκεύει το αποτέλεσμα. Το ίδιο μοτίβο καλύπτει επίσης **read excel file c#** και **load excel workbook c#**, ώστε να το προσαρμόσετε σε οποιοδήποτε σενάριο αυτοματοποίησης.

Η εργασία με αρχεία Excel στο .NET συχνά απαιτεί μια αξιόπιστη βιβλιοθήκη. Σε αυτό το tutorial χρησιμοποιούμε το **Aspose.Cells**, ένα πλήρως διαχειριζόμενο API που υποστηρίζει πίνακες, τύπους και πλούσια μορφοποίηση χωρίς να απαιτείται Microsoft Office στον διακομιστή. Τα βήματα είναι σύντομα, ο κώδικας είναι αυτόνομος, και θα καταλάβετε γιατί κάθε γραμμή είναι σημαντική.

## Τι θα πετύχετε

* Φορτώστε ένα υπάρχον αρχείο `.xlsx` στη μνήμη.
* Εντοπίστε και διαγράψτε έναν πίνακα (γνωστό και ως ListObject) από ένα φύλλο εργασίας.
* Αποθηκεύστε το τροποποιημένο βιβλίο εργασίας σε νέο αρχείο.
* Επεκτείνετε την προσέγγιση για να διαχειριστείτε πολλαπλούς πίνακες ή σενάρια όπου λείπουν πίνακες.

Δεν απαιτείται προηγούμενη εμπειρία με το Aspose.Cells — απλώς βασικές γνώσεις C#.

## Προαπαιτούμενα

* .NET 6.0 SDK ή νεότερο (ο κώδικας λειτουργεί επίσης με .NET Core 3.1 και .NET Framework 4.6+).
* Visual Studio 2022 (ή οποιονδήποτε επεξεργαστή που υποστηρίζει έργα .NET).
* Το πακέτο NuGet **Aspose.Cells**. Εγκαταστήστε το με:

```bash
dotnet add package Aspose.Cells
```

* Ένα αρχείο Excel (`input.xlsx`) που περιέχει τουλάχιστον έναν πίνακα. Αν δεν έχετε, δημιουργήστε έναν απλό πίνακα στο Excel και αποθηκεύστε τον στον ίδιο φάκελο με το έργο.

---

## Βήμα 1: Φορτώστε το βιβλίο εργασίας Excel σε C#

Το πρώτο καθήκον είναι να διαβάσετε το βιβλίο εργασίας από το δίσκο. Αυτό είναι ο πυρήνας του **load excel workbook c#**.

```csharp
using Aspose.Cells;
using System;

class ExcelTableRemover
{
    static void Main()
    {
        // Define file paths
        const string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        const string outputPath = @"YOUR_DIRECTORY\output.xlsx";

        // Step 1: Load the workbook
        Workbook workbook = new Workbook(inputPath);
```

**Γιατί είναι σημαντικό:**  
`Workbook` αντιπροσωπεύει ολόκληρο το αρχείο Excel στη μνήμη. Η φόρτωση του μία φορά σας επιτρέπει να εκτελέσετε πολλαπλές λειτουργίες — ανάγνωση κελιών, τροποποίηση πινάκων ή αλλαγή μορφοποίησης — χωρίς να ανοίγετε το αρχείο επανειλημμένα.

---

## Βήμα 2: Πρόσβαση στο πρώτο φύλλο εργασίας (read excel file c#)

Αφού φορτωθεί το βιβλίο εργασίας, χρειάζεστε μια αναφορά στο φύλλο εργασίας που περιέχει τον πίνακα.

```csharp
        // Step 2: Get the first worksheet
        Worksheet worksheet = workbook.Worksheets[0];
```

**Εξήγηση:**  
`Worksheets` είναι μια συλλογή με μηδενική βάση, έτσι το `[0]` επιστρέφει το πρώτο φύλλο. Αν το αρχείο σας έχει διαφορετική διάταξη, αντικαταστήστε το δείκτη ή χρησιμοποιήστε `workbook.Worksheets["SheetName"]`.

---

## Βήμα 3: Διαγραφή του πίνακα από το φύλλο εργασίας

Τώρα εκτελούμε την κύρια λειτουργία **delete table from excel**. Το παράδειγμα αφαιρεί τον πρώτο πίνακα, αλλά η ίδια λογική ισχύει για οποιονδήποτε δείκτη πίνακα.

```csharp
        // Step 3: Delete the first table in the worksheet
        if (worksheet.Tables.Count > 0)
        {
            // Table[0] is the first ListObject on the sheet
            worksheet.Tables[0].Delete();
            Console.WriteLine("Table deleted successfully.");
        }
        else
        {
            Console.WriteLine("No tables found on the worksheet.");
        }
```

**Γιατί αυτό λειτουργεί:**  
`Tables` είναι μια συλλογή αντικειμένων `ListObject`. Η κλήση του `Delete()` αφαιρεί τον ορισμό του πίνακα *και* την υποκείμενη περιοχή δεδομένων, αφήνοντας απλά κελιά. Η συνθήκη `if` εφαρμόζει το **how to remove table excel** με ασφάλεια, αποτρέποντας εξαίρεση όταν το φύλλο δεν περιέχει πίνακες.

**Συμβουλή:**  
Αν χρειάζεται να διαγράψετε έναν πίνακα με όνομα αντί για θέση, χρησιμοποιήστε `worksheet.Tables["TableName"].Delete();`. Αυτό είναι χρήσιμο όταν το βιβλίο εργασίας περιέχει πολλούς πίνακες και θέλετε να στοχεύσετε έναν συγκεκριμένο.

---

## Βήμα 4: Αποθήκευση του τροποποιημένου βιβλίου εργασίας (how to delete excel table)

Τέλος, γράψτε τις αλλαγές πίσω στο δίσκο. Αυτό ολοκληρώνει τη ροή εργασίας **how to delete excel table**.

```csharp
        // Step 4: Save the modified workbook
        workbook.Save(outputPath);
        Console.WriteLine($"Modified workbook saved to {outputPath}");
    }
}
```

**Τι συμβαίνει στο παρασκήνιο:**  
`Save` δημιουργεί ένα νέο αρχείο `.xlsx` που αντικατοπτρίζει όλες τις αλλαγές στη μνήμη. Το αρχικό `input.xlsx` παραμένει αμετάβλητο, κάτι που είναι ασφαλή πρακτική για σενάρια παραγωγής.

---

## Πλήρες, εκτελέσιμο παράδειγμα

Συνδυάζοντας όλα τα κομμάτια, εδώ είναι το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε, επικολλήσετε και να εκτελέσετε:

```csharp
using Aspose.Cells;
using System;

class ExcelTableRemover
{
    static void Main()
    {
        // Paths – adjust to your environment
        const string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        const string outputPath = @"YOUR_DIRECTORY\output.xlsx";

        // Load the workbook (load excel workbook c#)
        Workbook workbook = new Workbook(inputPath);

        // Get the first worksheet (read excel file c#)
        Worksheet worksheet = workbook.Worksheets[0];

        // Delete the first table (delete table from excel)
        if (worksheet.Tables.Count > 0)
        {
            worksheet.Tables[0].Delete();
            Console.WriteLine("Table deleted successfully.");
        }
        else
        {
            Console.WriteLine("No tables found on the worksheet.");
        }

        // Save the changes (how to delete excel table)
        workbook.Save(outputPath);
        Console.WriteLine($"Modified workbook saved to {outputPath}");
    }
}
```

**Αναμενόμενη έξοδος**

```
Table deleted successfully.
Modified workbook saved to YOUR_DIRECTORY\output.xlsx
```

Ανοίξτε το `output.xlsx` στο Excel· ο πίνακας που αφαιρέσατε θα εμφανιστεί τώρα ως κανονικά κελιά που περιέχουν τα αρχικά δεδομένα.

---

## Διαχείριση κοινών περιπτώσεων άκρων

| Κατάσταση | Συνιστώμενη προσέγγιση |
|-----------|----------------------|
| **Πολλαπλοί πίνακες** | Επανάληψη μέσω `worksheet.Tables` και διαγραφή του καθενός, ή διαγραφή με όνομα χρησιμοποιώντας `worksheet.Tables["MyTable"].Delete();`. |
| **Ο πίνακας δεν υπάρχει** | Η συνθήκη `if (worksheet.Tables.Count > 0)` ήδη αποτρέπει ένα `NullReferenceException`. Μπορείτε επίσης να καταγράψετε μια προειδοποίηση για έλεγχο. |
| **Μεγάλα αρχεία** | Χρησιμοποιήστε `Workbook.LoadOptions` για να ανοίξετε το αρχείο σε λειτουργία **memory‑efficient** (π.χ., `LoadOptions { MemorySetting = MemorySetting.MemoryPreference };`). |
| **Διατήρηση μορφοποίησης** | Η διαγραφή ενός πίνακα αφαιρεί το στυλ του. Αν χρειάζεται να διατηρήσετε το οπτικό στυλ, αντιγράψτε το στυλ στην περιοχή-στόχο πριν καλέσετε `Delete()`. |

---

## Συμβουλή απόδοσης: λειτουργίες παρτίδας

Αν χρειάζεται να διαγράψετε πολλούς πίνακες σε διάφορα φύλλα εργασίας, τυλίξτε τις αλλαγές σε μία μόνο παρουσία `Workbook` και καλέστε `workbook.CalculateFormula()` μόνο μία φορά μετά από όλες τις διαγραφές. Αυτό μειώνει το φορτίο CPU σε σύγκριση με τον επανυπολογισμό μετά από κάθε διαγραφή πίνακα.

---

## Επόμενα βήματα

Τώρα που γνωρίζετε **how to remove table excel** και **delete table from excel**, ίσως θέλετε να:

* **Read Excel file C#** για εξαγωγή δεδομένων μετά την αφαίρεση του πίνακα. Η συλλογή `Cells` σας επιτρέπει να διατρέχετε σειρές και στήλες.
* Δημιουργήσετε νέους πίνακες προγραμματιστικά με `worksheet.Tables.Add()` — χρήσιμο για σενάρια αναφορών.
* Εξερευνήσετε άλλα χαρακτηριστικά του Aspose.Cells όπως η διαχείριση διαγραμμάτων, οι συγκεντρωτικοί πίνακες ή η υπό συνθήκη μορφοποίηση.

---

## Συμπέρασμα

Μάθατε πώς να **διαγράψετε πίνακα από το Excel** χρησιμοποιώντας C#. Ο οδηγός κάλυψε τη φόρτωση του βιβλίου εργασίας, την πρόσβαση στο φύλλο εργασίας, την ασφαλή αφαίρεση του πίνακα και την αποθήκευση του ενημερωμένου αρχείου — όλα με ένα πλήρες, εκτελέσιμο παράδειγμα. Με αυτή τη βάση μπορείτε να αυτοματοποιήσετε οποιαδήποτε ροή εργασίας βασισμένη σε Excel, είτε χρειάζεστε **read excel file c#**, **load excel workbook c#**, ή **how to delete excel table** σε πιο σύνθετα σενάρια.

Μη διστάσετε να πειραματιστείτε με πολλαπλούς πίνακες, διαφορετικά φύλλα εργασίας ή εναλλακτικές βιβλιοθήκες όπως το EPPlus αν προτιμάτε μια ανοιχτού κώδικα λύση. Καλή προγραμματιστική!

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετα χαρακτηριστικά του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Διαβάστε αρχείο Excel C# – Πώς να φορτώσετε βιβλίο εργασίας Excel C# αποδοτικά](/cells/english/net/loading-and-saving-excel-files-with-options/read-excel-file-c-how-to-load-excel-workbook-c-efficiently/)
- [Πώς να διαγράψετε γραμμές από έναν πίνακα Excel και να αλλάξετε το όνομά του σε C#](/cells/english/net/tables-and-lists/how-to-delete-rows-from-an-excel-table-and-change-its-name-i/)
- [Πώς να μετονομάσετε πίνακα στο Excel με C# – Οδηγός βήμα‑βήμα](/cells/english/net/tables-and-lists/how-to-rename-table-in-excel-with-c-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}