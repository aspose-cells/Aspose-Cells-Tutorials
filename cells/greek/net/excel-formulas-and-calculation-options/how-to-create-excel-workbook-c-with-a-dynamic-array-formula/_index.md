---
category: general
date: 2026-10-01
description: Δημιουργήστε γρήγορα ένα βιβλίο εργασίας Excel με C# και μάθετε ένα παράδειγμα
  δυναμικού τύπου πίνακα για να γράψετε τύπο Excel C# στο Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook c#
- dynamic array formula example
- write excel formula c#
language: el
lastmod: 2026-10-01
og_description: Δημιουργήστε γρήγορα ένα βιβλίο εργασίας Excel με C# και δείτε ένα
  παράδειγμα δυναμικού τύπου πίνακα που δείχνει πώς να γράψετε τύπο Excel σε C# χρησιμοποιώντας
  το Aspose.Cells. Ακολουθήστε τον οδηγό βήμα‑προς‑βήμα για να δημιουργήσετε, υπολογίσετε
  και αποθηκεύσετε το αρχείο.
og_image_alt: Screenshot of C# code creating an Excel workbook and applying a SORT
  dynamic array formula
og_title: Δημιουργία βιβλίου εργασίας Excel C# με δυναμικό τύπο πίνακα
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Create Excel workbook C# quickly and learn a dynamic array formula
    example to write Excel formula C# in Aspose.Cells.
  headline: How to create Excel workbook C# with a dynamic array formula
  type: TechArticle
- description: Create Excel workbook C# quickly and learn a dynamic array formula
    example to write Excel formula C# in Aspose.Cells.
  name: How to create Excel workbook C# with a dynamic array formula
  steps:
  - name: Verifying the result (expected output)
    text: 'You can print the spilled values to the console to confirm the calculation
      succeeded:'
  - name: What if I need to use a different dynamic array function?
    text: 'Replace the formula string with any other dynamic array function, such
      as `=FILTER(A2:A10, B2:B10>10)` or `=UNIQUE(A2:A10)`. The same **write Excel
      formula C#** pattern applies:'
  - name: How do I handle formulas that reference other worksheets?
    text: 'Reference another sheet by its name:'
  - name: Can I suppress automatic calculation and calculate later?
    text: 'Yes. Set the workbook’s calculation mode to manual:'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Πώς να δημιουργήσετε ένα βιβλίο εργασίας Excel σε C# με δυναμικό τύπο πίνακα
url: /el/net/excel-formulas-and-calculation-options/how-to-create-excel-workbook-c-with-a-dynamic-array-formula/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να δημιουργήσετε βιβλίο εργασίας Excel C# με έναν τύπο δυναμικού πίνακα

Αν χρειάζεστε να **create Excel workbook C#** προγραμματιστικά, αυτός ο οδηγός σας δείχνει ακριβώς πώς να το κάνετε χρησιμοποιώντας το Aspose.Cells. Θα λάβετε επίσης ένα **dynamic array formula example** που δείχνει τον καλύτερο τρόπο για **write Excel formula C#** για σύγχρονες λειτουργίες του Excel όπως το `SORT`.

Η δημιουργία ενός αρχείου Excel από C# παλαιότερα απαιτούσε COM interop ή χειροκίνητη δημιουργία XML, τα οποία ήταν ευαίσθητα και δύσκολο να συντηρηθούν. Στο τέλος αυτού του οδηγού θα έχετε ένα πλήρως λειτουργικό βιβλίο εργασίας που υπολογίζει αυτόματα έναν δυναμικό πίνακα, και θα καταλάβετε γιατί αυτή η προσέγγιση είναι αξιόπιστη για αυτοματοποίηση παραγωγικού επιπέδου.

## Προαπαιτούμενα

- .NET 6.0 ή νεότερο εγκατεστημένο (ο κώδικας λειτουργεί επίσης με .NET Core και .NET Framework)
- Ένα έγκυρο άδεια Aspose.Cells ή ένα δωρεάν κλειδί αξιολόγησης
- Visual Studio 2022 (ή οποιοδήποτε IDE που υποστηρίζει C#)
- Βασική εξοικείωση με τη σύνταξη C# και τους τύπους Excel

Δεν απαιτούνται επιπλέον πακέτα NuGet πέρα από το `Aspose.Cells`, το οποίο μπορείτε να προσθέσετε με:

```bash
dotnet add package Aspose.Cells
```

## Βήμα 1: Ρύθμιση του έργου C# και αναφορά στο Aspose.Cells

Δημιουργήστε μια νέα εφαρμογή κονσόλας και προσθέστε την αναφορά Aspose.Cells. Αυτό το βήμα είναι απαραίτητο επειδή η βιβλιοθήκη παρέχει τα `Workbook`, `Worksheet` και τη μηχανή υπολογισμού που χρειάζεστε για κώδικα **write Excel formula C#**.

```csharp
// Program.cs
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // The rest of the tutorial code lives inside this method.
    }
}
```

> **Γιατί είναι σημαντικό:** Aspose.Cells αφαιρεί τις λεπτομέρειες χαμηλού επιπέδου του OpenXML, επιτρέποντάς σας να εστιάσετε στη λογική της επιχείρησης αντί στις ιδιαιτερότητες του μορφότυπου αρχείου.

## Βήμα 2: Δημιουργία του βιβλίου εργασίας Excel και λήψη του πρώτου φύλλου εργασίας

Τώρα **create Excel workbook C#** δημιουργώντας ένα αντικείμενο `Workbook`. Το προεπιλεγμένο βιβλίο εργασίας περιέχει ένα μόνο φύλλο εργασίας, το οποίο ανακτούμε για περαιτέρω λειτουργίες.

```csharp
// Step 2: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();               // creates a blank .xlsx file in memory
Worksheet worksheet = workbook.Worksheets[0];    // first (and only) sheet by default
```

> **Συμβουλή:** Αν χρειάζεστε πολλαπλά φύλλα, καλέστε `workbook.Worksheets.Add()` πριν τα προσπελάσετε.

## Βήμα 3: Συμπλήρωση δεδομένων πηγής για τον δυναμικό πίνακα

Οι λειτουργίες δυναμικού πίνακα όπως το `SORT` απαιτούν μια περιοχή πηγής. Ας γεμίσουμε τα κελιά *A2:A10* με μη ταξινομημένους αριθμούς ώστε ο τύπος `SORT` να δείξει τη συμπεριφορά του.

```csharp
// Step 3: Fill A2:A10 with sample data
int[] numbers = { 42, 7, 19, 33, 5, 27, 14, 8, 21 };
for (int i = 0; i < numbers.Length; i++)
{
    worksheet.Cells[i + 1, 0].PutValue(numbers[i]); // Row i+2, Column A (0‑based index)
}
```

> **Γιατί το κάνουμε:** Παρέχοντας συγκεκριμένα δεδομένα, μπορείτε να δείτε το **dynamic array formula example** σε δράση χωρίς να χρειάζεστε εξωτερικά αρχεία εισόδου.

## Βήμα 4: Εγγραφή του τύπου δυναμικού πίνακα στο κελί A1

Αυτή είναι η καρδιά του τμήματος **write Excel formula C#**. Αναθέτουμε έναν τύπο `SORT` στο κελί *A1*. Επειδή το `SORT` είναι μια λειτουργία δυναμικού πίνακα, το Excel θα εξαπλώσει αυτόματα τα ταξινομημένα αποτελέσματα στα κελιά κάτω.

```csharp
// Step 4: Insert a dynamic array formula (SORT) into cell A1
worksheet.Cells[0, 0].Formula = "=SORT(A2:A10)";
```

> **Επεξήγηση:**  
> - `worksheet.Cells[0, 0]` στοχεύει στο κελί **A1** (γραμμή 0, στήλη 0).  
> - Η συμβολοσειρά `=SORT(A2:A10)` είναι ένας τυπικός τύπος Excel. Το Aspose.Cells το αναλύει με τον ίδιο τρόπο όπως το Excel, επιτρέποντας πλήρη υποστήριξη για σύγχρονες λειτουργίες δυναμικού πίνακα.

## Βήμα 5: Επανάληψη υπολογισμού του βιβλίου εργασίας ώστε ο τύπος να γεμίσει αυτόματα

Το Aspose.Cells δεν επαναϋπολογίζει τους τύπους αυτόματα κατά την εγγραφή. Πρέπει να ενεργοποιήσετε ρητά τον υπολογισμό για να δείτε τα εξαπλωμένα αποτελέσματα.

```csharp
// Step 5: Recalculate the workbook so the formula evaluates
workbook.Calculate();   // runs the calculation engine once
```

Μετά από αυτήν την κλήση, τα κελιά **A1:A9** θα περιέχουν τη ταξινομημένη λίστα: 5, 7, 8, 14, 19, 21, 27, 33, 42.

### Επαλήθευση του αποτελέσματος (αναμενόμενη έξοδος)

Μπορείτε να εκτυπώσετε τις εξαπλωμένες τιμές στην κονσόλα για να επιβεβαιώσετε ότι ο υπολογισμός πέτυχε:

```csharp
Console.WriteLine("Sorted values from A1 down:");
for (int row = 0; row < 9; row++)
{
    Console.WriteLine(worksheet.Cells[row, 0].StringValue);
}
```

**Αναμενόμενη έξοδος κονσόλας**

```
Sorted values from A1 down:
5
7
8
14
19
21
27
33
42
```

> **Σημείωση για ειδικές περιπτώσεις:** Αν η περιοχή πηγής περιέχει μη αριθμητικά δεδομένα, το `SORT` θα ταξινομήσει λεκτικά. Πάντα να επικυρώνετε τους τύπους δεδομένων πριν εφαρμόσετε συναρτήσεις μόνο για αριθμούς.

## Βήμα 6: Αποθήκευση του βιβλίου εργασίας στο δίσκο (προαιρετικό)

Η αποθήκευση του αρχείου σας επιτρέπει να το ανοίξετε στο Excel και να δείτε τον δυναμικό πίνακα οπτικά. Αυτό το βήμα δεν απαιτείται για τον ίδιο τον υπολογισμό, αλλά είναι χρήσιμο για εντοπισμό σφαλμάτων και διανομή.

```csharp
// Step 6: Save the workbook as an .xlsx file
string outputPath = "SortedNumbers.xlsx";
workbook.Save(outputPath, SaveFormat.Xlsx);
Console.WriteLine($"Workbook saved to {outputPath}");
```

Όταν ανοίξετε το *SortedNumbers.xlsx* στο Excel 365 ή νεότερο, θα δείτε τη ταξινομημένη λίστα να εξαπλώνεται αυτόματα από το **A1** προς τα κάτω—ακριβώς αυτό που παρήγαγε το **dynamic array formula example** από C#.

## Πλήρες λειτουργικό παράδειγμα

Συνδυάζοντας όλα τα μέρη, εδώ είναι το πλήρες, εκτελέσιμο πρόγραμμα:

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1. Create workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2. Fill source data (A2:A10)
        int[] numbers = { 42, 7, 19, 33, 5, 27, 14, 8, 21 };
        for (int i = 0; i < numbers.Length; i++)
        {
            worksheet.Cells[i + 1, 0].PutValue(numbers[i]); // A2:A10
        }

        // 3. Write dynamic array formula (SORT) into A1
        worksheet.Cells[0, 0].Formula = "=SORT(A2:A10)";

        // 4. Force calculation so the array spills
        workbook.Calculate();

        // 5. Display the spilled values in the console
        Console.WriteLine("Sorted values from A1 down:");
        for (int row = 0; row < 9; row++)
        {
            Console.WriteLine(worksheet.Cells[row, 0].StringValue);
        }

        // 6. Save the workbook (optional)
        string outputPath = "SortedNumbers.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

Εκτελέστε το πρόγραμμα (`dotnet run`) και θα δείτε τους ταξινομημένους αριθμούς να εκτυπώνονται, ακολουθούμενοι από μια επιβεβαίωση ότι το αρχείο αποθηκεύτηκε.

## Συχνές ερωτήσεις και παραλλαγές

### Τι γίνεται αν χρειαστώ να χρησιμοποιήσω διαφορετική λειτουργία δυναμικού πίνακα;

Αντικαταστήστε τη συμβολοσειρά τύπου με οποιαδήποτε άλλη λειτουργία δυναμικού πίνακα, όπως `=FILTER(A2:A10, B2:B10>10)` ή `=UNIQUE(A2:A10)`. Το ίδιο πρότυπο **write Excel formula C#** ισχύει:

```csharp
worksheet.Cells[0, 0].Formula = "=UNIQUE(A2:A10)";
```

### Πώς να διαχειριστώ τύπους που αναφέρονται σε άλλα φύλλα εργασίας;

Αναφερθείτε σε άλλο φύλλο με το όνομά του:

```csharp
worksheet.Cells[0, 0].Formula = "=SORT('Sheet2'!A2:A10)";
```

Το Aspose.Cells επιλύει αυτόματα τις αναφορές μεταξύ φύλλων κατά την εκτέλεση του `workbook.Calculate()`.

### Μπορώ να απενεργοποιήσω τον αυτόματο υπολογισμό και να υπολογίσω αργότερα;

Ναι. Ορίστε τη λειτουργία υπολογισμού του βιβλίου εργασίας σε χειροκίνητη:

```csharp
workbook.Settings.CalcMode = CalcMode.Manual;
// ... make many changes ...
workbook.Calculate(); // call once when ready
```

Αυτό βελτιώνει την απόδοση όταν ενημερώνετε χιλιάδες κελιά πριν από τον τελικό υπολογισμό.

## Συμπέρασμα

Τώρα ξέρετε πώς να **create Excel workbook C#** χρησιμοποιώντας το Aspose.Cells, να εισάγετε ένα **dynamic array formula example**, και **write Excel formula C#** που εξαπλώνει αυτόματα τα αποτελέσματα. Η πλήρης λύση καλύπτει τη ρύθμιση του έργου, την προετοιμασία δεδομένων, την εισαγωγή τύπων, την εξαναγκαστική εκτέλεση υπολογισμού, την επαλήθευση και την προαιρετική αποθήκευση αρχείου.

Από εδώ μπορείτε να εξερευνήσετε πιο προχωρημένα σενάρια: αλυσίδωση πολλαπλών λειτουργιών δυναμικού πίνακα, εφαρμογή προσαρμοσμένων μορφών αριθμών, ή ενσωμάτωση της δημιουργίας βιβλίου εργασίας σε ένα web API. Θυμηθείτε πάντα να επικυρώνετε τα δεδομένα εισόδου πριν εφαρμόσετε τύπους, και να εκμεταλλεύεστε τη πλούσια μηχανή υπολογισμού του Aspose.Cells για αξιόπιστη επεξεργασία Excel από τον διακομιστή. Καλή προγραμματιστική!

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που βασίζονται στις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Δημιουργία νέου βιβλίου εργασίας σε C# – Προσθήκη τύπου και αποθήκευση αρχείου Excel](/cells/english/net/excel-workbook/create-new-workbook-in-c-add-formula-and-save-excel-file/)
- [Αυτοματοποίηση Excel με Aspose.Cells .NET: Κατακτώντας το βιβλίο εργασίας & τους υπολογισμούς τύπων](/cells/english/net/formulas-functions/excel-automation-aspose-cells-net-workbook-formulas/)
- [Δημιουργία βιβλίου εργασίας Excel C# – Πλήρης οδηγός με Aspose.Cells](/cells/english/net/excel-workbook/create-excel-workbook-c-complete-guide-with-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}