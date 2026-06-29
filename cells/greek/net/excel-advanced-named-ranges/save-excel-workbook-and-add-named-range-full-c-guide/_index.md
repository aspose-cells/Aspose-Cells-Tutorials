---
category: general
date: 2026-06-27
description: Αποθήκευση βιβλίου εργασίας Excel σε C# με προσθήκη ονομασμένης περιοχής.
  Μάθετε πώς να δημιουργήσετε ορισμένο όνομα και να χρησιμοποιήσετε τύπους ορισμένων
  ονομάτων με το Aspose.Cells.
draft: false
keywords:
- save excel workbook
- add named range
- create defined name
- named range excel
- use defined name formulas
language: el
og_description: Αποθηκεύστε το βιβλίο εργασίας Excel σε C# και μάθετε πώς να προσθέσετε
  μια ονομασμένη περιοχή, να δημιουργήσετε ορισμένο όνομα και να χρησιμοποιήσετε τύπους
  ορισμένων ονομάτων με το Aspose.Cells.
og_title: Αποθήκευση βιβλίου εργασίας Excel και προσθήκη ονομασμένης περιοχής – Οδηγός
  C#
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Save Excel Workbook in C# while adding a named range. Learn to create
    defined name and use defined name formulas with Aspose.Cells.
  headline: Save Excel Workbook and Add Named Range – Full C# Guide
  type: TechArticle
tags:
- C#
- Aspose.Cells
- Excel Automation
title: Αποθήκευση βιβλίου εργασίας Excel και προσθήκη ονομασμένης περιοχής – Πλήρης
  οδηγός C#
url: /el/net/excel-advanced-named-ranges/save-excel-workbook-and-add-named-range-full-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Αποθήκευση Βιβλίου Excel και Προσθήκη Ονομαστικής Περιοχής – Πλήρης Οδηγός C#

Έχετε χρειαστεί ποτέ να **αποθηκεύσετε ένα βιβλίο Excel** μετά από λίγες προσαρμοσμένες ονομασίες στο φύλλο; Δεν είστε μόνοι. Σε πολλά εργαλεία αναφοράς ή εφαρμογές που βασίζονται σε δεδομένα, δημιουργούμε μια ονομαστική περιοχή, την αναφερόμαστε σε τύπους και, τέλος, αποθηκεύουμε τις αλλαγές στο δίσκο.  

Σε αυτό το tutorial θα περάσουμε ακριβώς από αυτό: φόρτωση ενός αρχείου *.xlsx*, **προσθήκη ονομαστικής περιοχής**, **δημιουργία ορισμένου ονόματος**, χρήση του ονόματος μέσα σε τύπο, και τέλος **αποθήκευση βιβλίου Excel** με τις ενημερώσεις. Χωρίς περιττές πληροφορίες—απλώς ένα πλήρες, εκτελέσιμο παράδειγμα που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο .NET.

> **Συμβουλή:** Το Aspose.Cells λειτουργεί χωρίς να χρειάζεται εγκατεστημένο Microsoft Office, καθιστώντας το ιδανικό για αυτοματοποίηση στο διακομιστή.

## Τι Θα Χρειαστείτε

- .NET 6 (ή οποιοδήποτε πρόσφατο .NET runtime)  
- Πακέτο NuGet Aspose.Cells for .NET (`Install-Package Aspose.Cells`)  
- Ένα δείγμα `input.xlsx` (οποιοδήποτε βιβλίο θα δουλέψει, αρκεί το Sheet1 να έχει δεδομένα στο **A1**)  
- Το αγαπημένο σας IDE (Visual Studio, Rider, VS Code…)

Αυτό είναι όλο. Αν έχετε αυτά, μπορούμε να περάσουμε κατευθείαν στον κώδικα.

## Βήμα 1: Ρύθμιση του Έργου

Δημιουργήστε μια εφαρμογή console και προσθέστε το Aspose.Cells:

```bash
dotnet new console -n ExcelNamedRangeDemo
cd ExcelNamedRangeDemo
dotnet add package Aspose.Cells
```

Ανοίξτε το `Program.cs`; θα δείτε τη προεπιλεγμένη μέθοδο `Main`. Θα αντικαταστήσουμε το περιεχόμενό της με το πλήρες workflow στα επόμενα βήματα.

## Βήμα 2: Φόρτωση του Βιβλίου

Η φόρτωση ενός βιβλίου είναι το πρώτο βήμα πριν μπορέσετε να **προσθέσετε ονομαστική περιοχή**. Σκεφτείτε το σαν το άνοιγμα ενός βιβλίου πριν αρχίσετε να γράφετε σημειώσεις στα περιθώρια.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Step 2: Load the workbook
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook wb = new Workbook(inputPath);
        Console.WriteLine("Workbook loaded successfully.");
```

> **Γιατί είναι σημαντικό:** Το αντικείμενο `Workbook` αντιπροσωπεύει ολόκληρο το αρχείο Excel στη μνήμη. Χωρίς αυτό δεν μπορείτε να χειριστείτε κελιά, ονόματα ή τύπους.

## Βήμα 3: Δημιουργία Ορισμένου Ονόματος (Προσθήκη Ονομαστικής Περιοχής)

Τώρα δημιουργούμε πραγματικά **ορισμένο όνομα** που δείχνει σε συγκεκριμένο κελί ή περιοχή. Στο UI του Excel θα πήγαινατε στο *Formulas → Name Manager*· εδώ το κάνουμε προγραμματιστικά.

```csharp
        // Step 3: Add a defined name that points to cell A1 on Sheet1
        // This name can be used in formulas throughout the workbook
        wb.Names.Add("Sales", "=Sheet1!$A$1");
        Console.WriteLine("Defined name 'Sales' added (named range Excel).");
```

> **Εξήγηση:** `wb.Names.Add` καταχωρεί μια *ονομαστική περιοχή* με όνομα **Sales**. Η συμβολοσειρά `=Sheet1!$A$1` είναι ο τύπος αναφοράς—ακριβώς ό,τι θα πληκτρολογούσατε στο διάλογο Name Manager.

## Βήμα 4: Χρήση Ορισμένου Ονόματος σε Τύπο

Το να έχετε ένα όνομα είναι ωραίο, αλλά συνήθως θέλετε να **χρησιμοποιήσετε τύπους με ορισμένο όνομα** κάπου. Ας γράψουμε έναν απλό τύπο που προσθέτει 10 στην τιμή του **Sales** και τοποθετεί το αποτέλεσμα στο **B1**.

```csharp
        // Step 4: Write a formula that uses the defined name
        Worksheet sheet = wb.Worksheets["Sheet1"];
        Cell targetCell = sheet.Cells["B1"];
        targetCell.Formula = "=Sales + 10";
        Console.WriteLine("Formula '=Sales + 10' written to B1.");
```

Όταν το βιβλίο επαναϋπολογιστεί, το `B1` θα εμφανίσει ό,τι περιέχει το `A1` συν δέκα. Αυτό δείχνει τη δύναμη μιας *named range excel*—μπορείτε να αλλάξετε την υποκείμενη αναφορά μία φορά και όλοι οι τύποι ενημερώνονται αυτόματα.

## Βήμα 5: Αποθήκευση του Τροποποιημένου Βιβλίου

Τέλος, **αποθηκεύουμε το βιβλίο Excel** σε νέο αρχείο ώστε οι αλλαγές να παραμείνουν. Μπορείτε να αντικαταστήσετε το αρχικό ή να γράψετε σε διαφορετική θέση· εδώ κρατάμε και τα δύο.

```csharp
        // Step 5: Save the modified workbook
        string outputPath = @"YOUR_DIRECTORY\output.xlsx";
        wb.Save(outputPath);
        Console.WriteLine($"Workbook saved as '{outputPath}'.");
    }
}
```

Η εκτέλεση του προγράμματος εμφανίζει έξοδο κονσόλας παρόμοια με:

```
Workbook loaded successfully.
Defined name 'Sales' added (named range Excel).
Formula '=Sales + 10' written to B1.
Workbook saved as 'YOUR_DIRECTORY\output.xlsx'.
```

Ανοίξτε το `output.xlsx` και θα δείτε ότι το **B1** περιέχει τώρα `=Sales + 10`, ενώ το **A1** παραμένει αμετάβλητο. Το όνομα **Sales** εμφανίζεται στο *Formulas → Name Manager*.

## Ακραίες Περιπτώσεις & Συχνές Ερωτήσεις

| Ερώτηση | Απάντηση |
|----------|--------|
| **Τι γίνεται αν το όνομα του φύλλου περιέχει κενά;** | Τοποθετήστε το σε μονά εισαγωγικά: `= 'My Sheet'!$A$1`. |
| **Μπορώ να συνδέσω ένα όνομα με περιοχή πολλαπλών κελιών;** | Απόλυτα—χρησιμοποιήστε `=Sheet1!$A$1:$A$5` όταν καλείτε `wb.Names.Add`. |
| **Πρέπει να επαναϋπολογίσω χειροκίνητα;** | Το Aspose.Cells επαναϋπολογίζει αυτόματα όταν διαβάζετε τιμή κελιού. Αν χρειάζεστε πλήρη ανανέωση, καλέστε `wb.CalculateFormula()`. |
| **Τι γίνεται με υπάρχοντα ονόματα;** | `wb.Names.Add` θα πετάξει εξαίρεση αν το όνομα υπάρχει ήδη. Χρησιμοποιήστε `wb.Names["Sales"]?.RefersTo = "...";` για ενημέρωση. |

## Πλήρες Παράδειγμα (Όλα τα Βήματα Συνδυασμένα)

Παρακάτω είναι το ολοκληρωμένο πρόγραμμα, έτοιμο για αντιγραφή‑επικόλληση. Αντικαταστήστε το `YOUR_DIRECTORY` με έναν πραγματικό φάκελο στο σύστημά σας.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Load the workbook
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook wb = new Workbook(inputPath);
        Console.WriteLine("Workbook loaded successfully.");

        // Add a defined name (named range) that points to cell A1 on Sheet1
        wb.Names.Add("Sales", "=Sheet1!$A$1");
        Console.WriteLine("Defined name 'Sales' added (named range Excel).");

        // Write a formula that uses the defined name
        Worksheet sheet = wb.Worksheets["Sheet1"];
        Cell targetCell = sheet.Cells["B1"];
        targetCell.Formula = "=Sales + 10";
        Console.WriteLine("Formula '=Sales + 10' written to B1.");

        // Save the modified workbook
        string outputPath = @"YOUR_DIRECTORY\output.xlsx";
        wb.Save(outputPath);
        Console.WriteLine($"Workbook saved as '{outputPath}'.");
    }
}
```

**Αναμενόμενο Αποτέλεσμα:**  

- Το `output.xlsx` περιέχει νέο όνομα **Sales** που δείχνει στο `Sheet1!A1`.  
- Το κελί **B1** εμφανίζει την τιμή του **A1** συν `10`.  
- Το αρχείο είναι πλήρως συμβατό με Excel, Google Sheets ή οποιαδήποτε βιβλιοθήκη που καταλαβαίνει ονομαστικές περιοχές.

## Συμπέρασμα

Τώρα ξέρετε πώς να **αποθηκεύσετε βιβλίο Excel**, **προσθέσετε ονομαστική περιοχή**, **δημιουργήσετε ορισμένο όνομα**, και **χρησιμοποιήσετε τύπους με ορισμένο όνομα** χρησιμοποιώντας το Aspose.Cells σε C#. Τα βήματα είναι απλά: φόρτωση, ονομασία, αναφορά, και αποθήκευση.  

Από εδώ μπορείτε να επεκτείνετε σε:  

- Δημιουργία δυναμικών περιοχών με συναρτήσεις `OFFSET`.  
- Εφαρμογή του ίδιου ονόματος σε πολλαπλά φύλλα (`Scope = Worksheet`).  
- Δημιουργία χιλιάδων ονομαστικών περιοχών για σύνθετα χρηματοοικονομικά μοντέλα.

Δοκιμάστε το, τροποποιήστε την αναφορά, ή τροφοδοτήστε το όνομα σε pivot table—οι δυνατότητες αυτοματοποίησης είναι πρακτικά απεριόριστες.

---

![Save Excel Workbook flowchart](excel-workflow.png){: .align-center alt="Save Excel Workbook flowchart"}

*Έτοιμοι να αυτοματοποιήσετε τις αναφορές Excel σας; Αφήστε σχόλιο, μοιραστείτε τις προσαρμογές σας, ή κάντε fork το repo στο GitHub. Καλό coding!*


## Τι Θα Μάθετε Στη Σύντομη Μελλοντική Σας Διαδρομή;


Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη κώδικα με βήμα‑βήμα επεξηγήσεις για να κυριαρχήσετε επιπλέον δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στα δικά σας έργα.

- [Create Save Excel Workbook Aspose Cells Dotnet](/cells/english/net/workbook-operations/create-save-excel-workbook-aspose-cells-dotnet/)
- [How to Create and Save an Excel Workbook as ODS Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [Create Save Excel Workbook Pdf Aspnet Aspose Cells](/cells/english/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}