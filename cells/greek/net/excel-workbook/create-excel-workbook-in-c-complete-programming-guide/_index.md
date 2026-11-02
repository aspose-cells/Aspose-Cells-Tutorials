---
category: general
date: 2026-06-05
description: Δημιουργήστε γρήγορα ένα βιβλίο εργασίας Excel σε C# και μάθετε πώς να
  ορίσετε τη μορφή αριθμού κελιού, να εξάγετε κελί Excel και να μετατρέψετε την τιμή
  του κελιού σε συμβολοσειρά με ακρίβεια δύο δεκαδικών.
draft: false
keywords:
- create excel workbook
- set cell number format
- format number with two decimals
- how to export excel cell
- convert cell value to string
language: el
og_description: Δημιουργήστε βιβλίο εργασίας Excel σε C# και μάθετε να ρυθμίζετε τη
  μορφή αριθμού κελιού, να εξάγετε το κελί Excel ως συμβολοσειρά και να μορφοποιείτε
  αριθμούς με δύο δεκαδικά.
og_title: Δημιουργία βιβλίου εργασίας Excel σε C# – Πλήρης οδηγός βήμα‑προς‑βήμα
schemas:
- author: Aspose
  dateModified: '2026-06-05'
  description: Create Excel workbook in C# quickly and learn how to set cell number
    format, export Excel cell, and convert cell value to string with two‑decimal precision.
  headline: Create Excel Workbook in C# – Complete Programming Guide
  type: TechArticle
- description: Create Excel workbook in C# quickly and learn how to set cell number
    format, export Excel cell, and convert cell value to string with two‑decimal precision.
  name: Create Excel Workbook in C# – Complete Programming Guide
  steps:
  - name: What if the cell already has a style?
    text: The `GetStyle` method returns a copy of the existing style, so any previous
      formatting (font, color, etc.) is retained. You only overwrite the `Custom`
      property, leaving everything else untouched.
  - name: How does culture affect the decimal separator?
    text: 'Aspose.Cells respects the thread’s `CultureInfo`. If you need a comma instead
      of a dot, set:'
  - name: Can I export a range of cells at once?
    text: Yes—use `Worksheet.ExportDataTable` or `Worksheet.ExportString` with a range
      address. The `ExportTableOptions` you defined for a single cell can be reused
      for the whole range.
  - name: What if I don’t want the value rounded but truncated?
    text: 'Change the custom format to `"0.00"` with a rounding mode, or manually
      truncate before putting the value:'
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
title: Δημιουργία βιβλίου εργασίας Excel σε C# – Πλήρης οδηγός προγραμματισμού
url: /el/net/excel-workbook/create-excel-workbook-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία βιβλίου εργασίας Excel σε C# – Πλήρης Οδηγός Προγραμματισμού

Έχετε αναρωτηθεί ποτέ πώς να **create Excel workbook** σε C# χωρίς να παλεύετε με το COM interop ή ακατάστατες τεχνικές CSV; Δεν είστε μόνοι. Πολλοί προγραμματιστές χρειάζονται έναν καθαρό, .NET‑native τρόπο για να δημιουργήσουν ένα αρχείο .xlsx, να τοποθετήσουν έναν αριθμό σε ένα κελί και στη συνέχεια να εξάγουν αυτήν την τιμή ως μια ωραία μορφοποιημένη συμβολοσειρά.  

Σε αυτό το tutorial θα περάσουμε ακριβώς από αυτό—ξεκινώντας από ένα κενό βιβλίο εργασίας, ορίζοντας τη μορφή αριθμού του κελιού, μορφοποιώντας τον αριθμό με δύο δεκαδικά ψηφία, και τελικά μαθαίνοντας **how to export Excel cell** δεδομένα ως συμβολοσειρά. Στο τέλος θα δείτε επίσης πώς να **convert cell value to string** χωρίς να χάσετε την ακρίβεια.

> **Pro tip:** Η προσέγγιση παρακάτω χρησιμοποιεί τη βιβλιοθήκη **Aspose.Cells for .NET**, η οποία είναι δοκιμασμένη, εμπορικής ποιότητας API. Αν ψάχνετε για μια δωρεάν εναλλακτική, το EPPlus ή το ClosedXML λειτουργούν παρόμοια, αλλά τα αποσπάσματα κώδικα θα διαφέρουν ελαφρώς.

## Προαπαιτούμενα

- .NET 6.0 SDK (ή οποιαδήποτε πρόσφατη έκδοση .NET) εγκατεστημένο.
- Visual Studio 2022 ή VS Code με την επέκταση C#.
- Το πακέτο NuGet **Aspose.Cells** (`Install-Package Aspose.Cells`).

Δεν απαιτούνται άλλες εξαρτήσεις—όλα τα υπόλοιπα βρίσκονται μέσα στη βιβλιοθήκη.

## Βήμα 1: Εγκατάσταση Aspose.Cells και Ρύθμιση του Έργου

Ανοίξτε το τερματικό σας (ή το Package Manager Console) και εκτελέστε:

```powershell
dotnet new console -n ExcelDemo
cd ExcelDemo
dotnet add package Aspose.Cells
```

Αυτό δημιουργεί μια νέα εφαρμογή console με όνομα `ExcelDemo` και προσθέτει το assembly `Aspose.Cells`.

Γιατί αυτό το βήμα είναι σημαντικό: χωρίς τη βιβλιοθήκη, δεν μπορείτε να **create Excel workbook** αντικείμενα ή να χειριστείτε κελιά με ασφαλή τύπο.

## Βήμα 2: Δημιουργία του Workbook και Λήψη του Πρώτου Worksheet

Τώρα ανοίξτε το `Program.cs` και αντικαταστήστε τον προεπιλεγμένο κώδικα με το παρακάτω απόσπασμα. Δείχνει το πρώτο πράγμα που κάνετε όταν **create Excel workbook**—δημιουργώντας την κλάση `Workbook` και λαμβάνοντας μια αναφορά στο προεπιλεγμένο φύλλο.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 2: Create a workbook and get the first worksheet
        Workbook workbook = new Workbook();               // creates a new .xlsx in memory
        Worksheet ws = workbook.Worksheets[0];           // first (default) sheet

        // The rest of the steps will follow here...
```

> **Why?** Το αντικείμενο `Workbook` είναι η αναπαράσταση στη μνήμη ενός αρχείου Excel. Από προεπιλογή περιέχει ένα worksheet, το οποίο προσπελαύνουμε μέσω του δείκτη μηδενικής βάσης.

## Βήμα 3: Τοποθέτηση Αριθμητικής Τιμής σε Συγκεκριμένο Κελί

Ας στοχεύσουμε στη γραμμή 5, στήλη 2 (δείκτες μηδενικής βάσης) και εισάγουμε έναν δεκαδικό αριθμό. Αυτό δείχνει το **format number with two decimals** αργότερα.

```csharp
        // Step 3: Access the cell at row 5, column 2 (zero‑based) and insert a number
        Cell cell = ws.Cells[5, 2];          // corresponds to cell C6 in Excel UI
        cell.PutValue(12345.6789);          // raw value with many decimal places
```

Η μέθοδος `PutValue` αποθηκεύει το ακατέργαστο double. Σε αυτό το σημείο, το Excel θα εμφανίσει την πλήρη ακρίβεια εκτός αν εφαρμόσουμε μορφή.

## Βήμα 4: Ορισμός Μορφής Αριθμού Κελιού (Δύο Δεκαδικά Ψηφία)

Εδώ είναι που **set cell number format**. Θα χρησιμοποιήσουμε το αντικείμενο `Style` για να ορίσουμε μια προσαρμοσμένη μορφή αριθμού `"0.00"`—ακριβώς δύο δεκαδικά.

```csharp
        // Step 4: Apply a number format to show only two decimal places
        Style style = cell.GetStyle();               // clone existing style
        style.Custom = "0.00";                       // forces two digits after the dot
        cell.SetStyle(style);                        // apply the style back to the cell
```

Γιατί να χρησιμοποιήσουμε στυλ αντί για μετατροπή σε συμβολοσειρά; Διατηρώντας το κελί ως αριθμητικό τύπο διατηρεί τη δυνατότητα υπολογισμού (μπορείτε ακόμη να αθροίζετε, να υπολογίζετε μέσο όρο κ.λπ.) ενώ εμφανίζει ακριβώς ό,τι χρειάζεστε.

## Βήμα 5: Εξαγωγή Τιμής Κελιού ως Μορφοποιημένη Συμβολοσειρά

Μερικές φορές χρειάζεστε την τιμή **how to export excel cell** ως απλό κείμενο—ίσως για να τη γράψετε σε αρχείο καταγραφής ή να τη στείλετε μέσω web API. Το Aspose.Cells σας επιτρέπει να συνδέσετε επιλογές εξαγωγής σε ένα κελί, λέγοντας στη βιβλιοθήκη να αποδώσει την τιμή ως συμβολοσειρά χρησιμοποιώντας την ίδια μορφή αριθμού.

```csharp
        // Step 5: Configure export options to get the formatted string
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,          // forces string output
            NumberFormat = "0.00"           // matches the style we set earlier
        };
        cell.ExportOptions = exportOptions; // attach options to the cell
```

## Βήμα 6: Ανάκτηση της Μορφοποιημένης Συμβολοσειράς (Convert Cell Value to String)

Ας εκτελέσουμε πραγματικά την εξαγωγή και δούμε το αποτέλεσμα. Η μέθοδος `ExportString` επιστρέφει το περιεχόμενο του κελιού ως συμβολοσειρά, εφαρμόζοντας τυχόν `ExportTableOptions` που συνδέσαμε.

```csharp
        // Step 6: Export the cell as a formatted string
        string formattedValue = cell.ExportString();
        Console.WriteLine($"Formatted cell value: {formattedValue}");
```

Όταν εκτελέσετε το πρόγραμμα, η κονσόλα εκτυπώνει:

```
Formatted cell value: 12345.68
```

Παρατηρήστε το στρογγυλοποίηση από `12345.6789` σε `12345.68`—αυτό είναι το αποτέλεσμα του **format number with two decimals**.

## Βήμα 7: (Προαιρετικό) Αποθήκευση του Workbook στο Δίσκο

Αν θέλετε επίσης να δείτε το αποτέλεσμα μέσα σε ένα πραγματικό αρχείο `.xlsx`, απλώς καλέστε `Save`:

```csharp
        // Optional: write the workbook to a file so you can open it in Excel
        workbook.Save("DemoWorkbook.xlsx");
    }
}
```

Ανοίγοντας το `DemoWorkbook.xlsx` εμφανίζεται ο ίδιος αριθμός στο κελί **C6**, μορφοποιημένος με δύο δεκαδικά ψηφία.

## Περιπτώσεις Ορίων & Συχνές Ερωτήσεις

### Τι γίνεται αν το κελί έχει ήδη στυλ;

Η μέθοδος `GetStyle` επιστρέφει ένα αντίγραφο του υπάρχοντος στυλ, έτσι οποιαδήποτε προηγούμενη μορφοποίηση (γραμματοσειρά, χρώμα κ.λπ.) διατηρείται. Εσείς μόνο αντικαθιστάτε την ιδιότητα `Custom`, αφήνοντας τα υπόλοιπα αμετάβλητα.

### Πώς επηρεάζει η πολιτισμική ρύθμιση το διαχωριστικό δεκαδικών;

Το Aspose.Cells σέβεται το `CultureInfo` του νήματος. Αν χρειάζεστε κόμμα αντί για τελεία, ορίστε:

```csharp
System.Threading.Thread.CurrentThread.CurrentCulture = new System.Globalization.CultureInfo("fr-FR");
```

### Μπορώ να εξάγω μια περιοχή κελιών ταυτόχρονα;

Ναι—χρησιμοποιήστε `Worksheet.ExportDataTable` ή `Worksheet.ExportString` με διεύθυνση περιοχής. Οι `ExportTableOptions` που ορίσατε για ένα μόνο κελί μπορούν να επαναχρησιμοποιηθούν για ολόκληρη την περιοχή.

### Τι γίνεται αν δεν θέλω την τιμή στρογγυλοποιημένη αλλά περικομμένη;

Αλλάξτε τη προσαρμοσμένη μορφή σε `"0.00"` με τρόπο στρογγυλοποίησης, ή περικόψτε χειροκίνητα πριν τοποθετήσετε την τιμή:

```csharp
double raw = Math.Truncate(12345.6789 * 100) / 100; // yields 12345.67
cell.PutValue(raw);
```

## Πλήρες Παράδειγμα Εργασίας (Έτοιμο για Αντιγραφή‑Επικόλληση)

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 2: Create a workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet ws = workbook.Worksheets[0];

        // Step 3: Access the cell at row 5, column 2 (zero‑based) and insert a number
        Cell cell = ws.Cells[5, 2];
        cell.PutValue(12345.6789);

        // Step 4: Apply a number format to show only two decimal places
        Style style = cell.GetStyle();
        style.Custom = "0.00";
        cell.SetStyle(style);

        // Step 5: Configure export options to get the formatted string
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            NumberFormat = "0.00"
        };
        cell.ExportOptions = exportOptions;

        // Step 6: Export the cell as a formatted string
        string formattedValue = cell.ExportString();
        Console.WriteLine($"Formatted cell value: {formattedValue}");

        // Optional: save the workbook for visual verification
        workbook.Save("DemoWorkbook.xlsx");
    }
}
```

**Αναμενόμενη έξοδος κονσόλας**

```
Formatted cell value: 12345.68
```

Ανοίξτε το `DemoWorkbook.xlsx` → μεταβείτε στο κελί **C6** → θα δείτε τον ίδιο αριθμό με δύο δεκαδικά ψηφία.

## Συμπέρασμα

Μόλις καλύψαμε όλα όσα χρειάζεστε για να **create Excel workbook** σε C#, **set cell number format**, **format number with two decimals**, να κατανοήσετε **how to export Excel cell** δεδομένα, και **convert cell value to string** για επεξεργασία μεταγενέστερα.

Τα κύρια σημεία είναι:

1. Χρησιμοποιήστε `Workbook` και `Worksheet` για να δημιουργήσετε ένα αρχείο Excel στη μνήμη.  
2. Εφαρμόστε ένα προσαρμοσμένο στυλ (`"0.00"`) για να επιβάλλετε εμφάνιση δύο δεκαδικών.  
3. Συνδέστε `ExportTableOptions` σε ένα κελί όταν χρειάζεστε μια αναπαράσταση συμβολοσειράς που σέβεται την ίδια μορφή.

Από εδώ μπορείτε να πειραματιστείτε—προσθέστε περισσότερα κελιά, εφαρμόστε conditional formatting, ή ακόμη και δημιουργήστε γραφήματα. Αν σας ενδιαφέρει η μορφοποίηση γραμματοσειρών ή η προσθήκη τύπων, ρίξτε μια ματιά στην τεκμηρίωση του Aspose.Cells για **cell styling** και **formula evaluation**.

Έχετε περισσότερες ερωτήσεις σχετικά με την αυτοματοποίηση Excel σε C#; Αφήστε ένα σχόλιο, και καλή προγραμματιστική!

## Τι Θα Πρέπει Να Μάθετε Στη Σύντομη Μελλοντική Περίοδο;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Master Workbook Operations in Aspose.Cells .NET&#58; Load Excel Files and Trace Cell Precedents Effectively](/cells/english/net/workbook-operations/aspose-cells-net-master-workbook-operations/)
- [Master Excel Cell Formatting and Workbook Management with Aspose.Cells for .NET](/cells/english/net/formatting/excel-formatting-aspose-cells-net/)
- [Master Aspose.Cells for .NET&#58; Advanced Excel Workbook and Cell Management](/cells/english/net/advanced-features/excel-aspose-cells-net-create-manage/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}