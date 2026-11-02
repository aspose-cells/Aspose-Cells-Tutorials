---
category: general
date: 2026-08-07
description: Ορίστε ονομασμένη περιοχή στο Excel με C# και μάθετε πώς να προσθέσετε
  έναν πίνακα σε ένα φύλλο εργασίας, έπειτα αποθηκεύστε το βιβλίο εργασίας σε αρχείο
  προγραμματιστικά.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- define named range excel
- save workbook to file
- add named range excel
- add table to worksheet
- create excel workbook programmatically
language: el
lastmod: 2026-08-07
og_description: Ορίστε μια ονομασμένη περιοχή στο Excel με C# και δείτε πώς να προσθέσετε
  έναν πίνακα, να δημιουργήσετε ένα βιβλίο εργασίας προγραμματιστικά και να αποθηκεύσετε
  το βιβλίο εργασίας σε αρχείο σε μία ενιαία ροή.
og_image_alt: Screenshot of C# code that creates an Excel workbook, adds a table,
  defines a named range, and saves the file
og_title: Ορισμός ονομασμένης περιοχής στο Excel με C# – πλήρης οδηγός βιβλίου εργασίας
schemas:
- author: Aspose
  dateModified: '2026-08-07'
  description: Define named range in Excel with C# and learn how to add a table to
    a worksheet, then save workbook to file programmatically.
  headline: Define named range in Excel with C# – create workbook
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
- named range
- programmatic Excel
title: Ορισμός ονομασμένης περιοχής στο Excel με C# – δημιουργία βιβλίου εργασίας
url: /el/net/excel-working-with-named-ranges/define-named-range-in-excel-with-c-create-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ορισμός ονομαστικής περιοχής στο Excel με C# – δημιουργία βιβλίου εργασίας

Αν χρειάζεστε να **ορίσετε ονομαστική περιοχή στο Excel** από κώδικα C#, αυτό το tutorial σας δείχνει ακριβώς πώς να το κάνετε. Θα δείτε επίσης πώς να **προσθέσετε έναν πίνακα σε ένα φύλλο εργασίας**, να δημιουργήσετε το βιβλίο εργασίας **προγραμματιστικά**, και τέλος **να αποθηκεύσετε το βιβλίο εργασίας σε αρχείο** χωρίς να φύγετε από το IDE.

Η εργασία με αρχεία Excel προγραμματιστικά εξοικονομεί χρόνο, εξαλείφει τα χειροκίνητα σφάλματα και επιτρέπει αυτοματοποιημένες αλυσίδες αναφορών. Σε αυτόν τον οδηγό θα:

* Δημιουργήσετε ένα νέο βιβλίο εργασίας Excel από το μηδέν.  
* Προσθέσετε έναν πίνακα που καλύπτει συγκεκριμένο εύρος κελιών.  
* Ορίσετε μια ονομαστική περιοχή και διαχειριστείτε συγκρούσεις ονομάτων.  
* Αποθηκεύσετε το βιβλίο εργασίας στο δίσκο.

Όλα τα βήματα χρησιμοποιούν τη βιβλιοθήκη **Aspose.Cells for .NET**, η οποία λειτουργεί με .NET 6+ και .NET Framework 4.6+. Δεν απαιτείται πρόσθετο COM interop ή εγκατάσταση του Office.

## Προαπαιτούμενα

* .NET 6 SDK (ή .NET Framework 4.6+).  
* Visual Studio 2022 ή οποιοδήποτε IDE συμβατό με C#.  
* Πακέτο NuGet Aspose.Cells for .NET (`Install-Package Aspose.Cells`).  

> **Pro tip:** Χρησιμοποιήστε την δωρεάν άδεια αξιολόγησης κατά τη δοκιμή· αντικαταστήστε την με παραγωγική άδεια πριν από την ανάπτυξη.

## Βήμα 1: Δημιουργία βιβλίου εργασίας Excel προγραμματιστικά

Η πρώτη ενέργεια είναι η δημιουργία ενός αντικειμένου `Workbook`. Αυτό το αντικείμενο αντιπροσωπεύει ολόκληρο το αρχείο Excel στη μνήμη.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook in memory
        Workbook workbook = new Workbook();               // create an empty workbook
        Worksheet worksheet = workbook.Worksheets[0];    // get the first (default) worksheet
```

*Γιατί είναι σημαντικό*: Η δημιουργία του βιβλίου εργασίας μέσω κώδικα σας δίνει πλήρη έλεγχο πάνω στα φύλλα, τα στυλ και τα δεδομένα πριν το αρχείο αγγίξει τον δίσκο.

## Βήμα 2: Προσθήκη πίνακα σε φύλλο εργασίας

Ένας πίνακας (γνωστός και ως ListObject) παρέχει ενσωματωμένο φιλτράρισμα, ταξινόμηση και στυλ. Εδώ δημιουργούμε έναν πίνακα που καλύπτει τα κελιά **A1:B5** και του δίνουμε το όνομα **SalesData**.

```csharp
        // Step 2: Define a range and convert it into a table
        Range tableRange = worksheet.Cells.CreateRange("A1:B5", true);
        ListObject table = worksheet.Tables[worksheet.Tables.Add(tableRange, true)];
        table.Name = "SalesData";

        // Populate the table with sample data
        worksheet.Cells["A1"].PutValue("Product");
        worksheet.Cells["B1"].PutValue("Units");
        worksheet.Cells["A2"].PutValue("Apples");
        worksheet.Cells["B2"].PutValue(120);
        worksheet.Cells["A3"].PutValue("Bananas");
        worksheet.Cells["B3"].PutValue(85);
        worksheet.Cells["A4"].PutValue("Cherries");
        worksheet.Cells["B4"].PutValue(45);
        worksheet.Cells["A5"].PutValue("Dates");
        worksheet.Cells["B5"].PutValue(30);
```

*Γιατί είναι σημαντικό*: Η προσθήκη πίνακα νωρίς σας επιτρέπει να αναφέρεστε στα δεδομένα αργότερα με μια **ονομαστική περιοχή**, και η δομημένη αναφορά του πίνακα μπορεί να χρησιμοποιηθεί σε τύπους.

## Βήμα 3: Ορισμός ονομαστικής περιοχής – διαχείριση συγκρούσεων

Μια **ονομαστική περιοχή** είναι ένας ταυτοποιητής που δείχνει σε ένα κελί ή εύρος, καθιστώντας τους τύπους πιο ευανάγνωστους. Αν το όνομα υπάρχει ήδη (π.χ. το όνομα πίνακα **SalesData**), το Excel προκαλεί σύγκρουση. Ο κώδικας παρακάτω δείχνει πώς να πιάσετε αυτήν την εξαίρεση και να συνεχίσετε με ασφάλεια.

```csharp
        // Step 3: Attempt to define a named range with the same identifier as the table
        try
        {
            // This will raise an exception because "SalesData" is already used by the table
            worksheet.Names.Add("SalesData", "A1");
        }
        catch (Exception ex)
        {
            Console.WriteLine("Name conflict prevented: " + ex.Message);
        }

        // Step 4: Add a different named range – this succeeds
        worksheet.Names.Add("SalesTotal", "B6");
        worksheet.Cells["B6"].Formula = "=SUM(SalesData[Units])";
```

*Γιατί είναι σημαντικό*: Η διαχείριση συγκρούσεων ονομάτων αποτρέπει σφάλματα χρόνου εκτέλεσης σε αυτοματοποιημένες εργασίες. Η δεύτερη ονομαστική περιοχή **SalesTotal** δείχνει πώς να αναφέρετε τη στήλη του πίνακα σε τύπο.

## Βήμα 4: Αποθήκευση βιβλίου εργασίας σε αρχείο

Μετά από όλες τις τροποποιήσεις, αποθηκεύστε το βιβλίο εργασίας στο δίσκο. Η μέθοδος `Save` υποστηρίζει πολλές μορφές· εδώ χρησιμοποιούμε την προεπιλογή `.xlsx`.

```csharp
        // Step 5: Save the workbook to the file system
        string outputPath = @"C:\Temp\NameConflictHandled.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved successfully to {outputPath}");
    }
}
```

*Γιατί είναι σημαντικό*: Η **αποθήκευση βιβλίου εργασίας σε αρχείο** προγραμματιστικά επιτρέπει επεξεργασία παρτίδας, προγραμματισμένη δημιουργία αναφορών και ενσωμάτωση με web APIs.

## Πλήρης κώδικας σε μία προβολή

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Add a table covering A1:B5 and name it "SalesData"
        Range tableRange = worksheet.Cells.CreateRange("A1:B5", true);
        ListObject table = worksheet.Tables[worksheet.Tables.Add(tableRange, true)];
        table.Name = "SalesData";

        // Fill the table with sample data
        worksheet.Cells["A1"].PutValue("Product");
        worksheet.Cells["B1"].PutValue("Units");
        worksheet.Cells["A2"].PutValue("Apples");   worksheet.Cells["B2"].PutValue(120);
        worksheet.Cells["A3"].PutValue("Bananas");  worksheet.Cells["B3"].PutValue(85);
        worksheet.Cells["A4"].PutValue("Cherries"); worksheet.Cells["B4"].PutValue(45);
        worksheet.Cells["A5"].PutValue("Dates");    worksheet.Cells["B5"].PutValue(30);

        // Try to create a defined name with the same identifier – handle the conflict
        try
        {
            worksheet.Names.Add("SalesData", "A1");
        }
        catch (Exception ex)
        {
            Console.WriteLine("Name conflict prevented: " + ex.Message);
        }

        // Add a different defined name – this succeeds
        worksheet.Names.Add("SalesTotal", "B6");
        worksheet.Cells["B6"].Formula = "=SUM(SalesData[Units])";

        // Save the workbook
        string outputPath = @"C:\Temp\NameConflictHandled.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved successfully to {outputPath}");
    }
}
```

### Αναμενόμενο αποτέλεσμα

* Ένα αρχείο Excel με όνομα **NameConflictHandled.xlsx** εμφανίζεται στο `C:\Temp`.  
* Το Φύλλο 1 περιέχει έναν μορφοποιημένο πίνακα **SalesData** με γραμμές προϊόν‑μονάδα.  
* Το κελί **B6** εμφανίζει το άθροισμα της στήλης **Units**, υπολογισμένο μέσω της ονομαστικής περιοχής **SalesTotal**.  
* Η κονσόλα εκτυπώνει μήνυμα σχετικά με τη σύγκρουση ονόματος (αν υπάρχει) και επιβεβαιώνει τη θέση του αρχείου.

## Συχνές ερωτήσεις & ειδικές περιπτώσεις

| Ερώτηση | Απάντηση |
|----------|--------|
| **Μπορώ να ορίσω ονομαστική περιοχή που καλύπτει πολλαπλά φύλλα εργασίας;** | Ναι. Χρησιμοποιήστε `worksheet.Names.Add("GlobalRange", "'Sheet1'!A1:B5")` και αναφερθείτε σε αυτήν από οποιοδήποτε φύλλο. |
| **Τι γίνεται αν χρειαστεί να αντικαταστήσω ένα υπάρχον αρχείο;** | Καλέστε `workbook.Save(path, SaveFormat.Xlsx, new SaveOptions { Overwrite = true })`. |
| **Πώς να προσθέσω ονομαστική περιοχή χωρίς σύγκρουση όταν το όνομα υπάρχει ήδη;** | Χρησιμοποιήστε `worksheet.Names.Remove("ExistingName")` πριν προσθέσετε τη νέα, ή δημιουργήστε ένα μοναδικό αναγνωριστικό (π.χ. `Guid.NewGuid().ToString("N")`). |
| **Υπάρχει τρόπος να εφαρμόσω στυλ αυτόματα στον πίνακα;** | Ορίστε `table.Style = workbook.Styles[BuiltInStyleId.TableStyleMedium9];` μετά τη δημιουργία του πίνακα. |
| **Λειτουργεί αυτό σε .NET Core;** | Το Aspose.Cells υποστηρίζει .NET Core, .NET 5/6/7 και .NET Framework. Απλώς αναφέρετε το ίδιο πακέτο NuGet. |

## Συμπέρασμα

Τώρα ξέρετε πώς να **ορίσετε ονομαστική περιοχή στο Excel** χρησιμοποιώντας C#, **να προσθέσετε έναν πίνακα σε ένα φύλλο εργασίας**, και **να αποθηκεύσετε το βιβλίο εργασίας σε αρχείο** προγραμματιστικά. Το πλήρες παράδειγμα δείχνει τη δημιουργία ενός βιβλίου εργασίας από το μηδέν, τη διαχείριση συγκρούσεων ονομάτων και τη δημιουργία ενός χρήσιμου αρχείου αναφοράς σε μια ενιαία, επαναλήψιμη ροή.

Στη συνέχεια, εξερευνήστε σχετικά θέματα όπως **προσθήκη γραφημάτων σε φύλλο εργασίας**, **εξαγωγή σε PDF**, ή **ανάγνωση υπαρχόντων βιβλίων εργασίας**. Κάθε ένα από αυτά βασίζεται στις ίδιες θεμελιώδεις αρχές που καλύφθηκαν εδώ, ώστε να είστε έτοιμοι να επεκτείνετε τη λύση σε πιο σύνθετα σενάρια αυτοματοποίησης. Καλή προγραμματιστική!

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να κατακτήσετε πρόσθετα χαρακτηριστικά του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στην δική σας υλοποίηση.

- [Create Named Range of Cells in Excel](/cells/english/net/excel-creating-formatting-named-ranges/create-named-range-of-cells/)
- [How to Implement Named Range Formulas in .NET using Aspose.Cells for Excel Automation](/cells/english/net/formulas-functions/implement-named-range-formulas-net-aspose-cells/)
- [How to Create Workbook Scoped Named Ranges in Excel Using Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}