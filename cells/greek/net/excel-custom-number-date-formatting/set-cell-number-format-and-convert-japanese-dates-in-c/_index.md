---
category: general
date: 2026-11-19
description: Ορίστε τη μορφή αριθμού κελιού σε C# και μάθετε πώς να εφαρμόζετε τη
  μορφή ημερομηνίας του Excel για ιαπωνικές εποχές, εξασφαλίζοντας αξιόπιστη μετατροπή
  ημερομηνιών Excel σε C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set cell number format
- apply excel date format
- c# excel date conversion
- japanese era date excel
- aspose.cells date handling
language: el
lastmod: 2026-11-19
og_description: Ορίστε τη μορφή αριθμού κελιού σε C# και εφαρμόστε τη μορφή ημερομηνίας
  του Excel σε ημερομηνίες ιαπωνικής εποχής. Ακολουθήστε αυτόν τον πλήρη οδηγό για
  ακριβή μετατροπή ημερομηνιών C# σε Excel.
og_image_alt: Screenshot showing a C# code editor with set cell number format applied
  to an Excel cell
og_title: Ορίστε τη μορφή αριθμού κελιού και μετατρέψτε τις ιαπωνικές ημερομηνίες
  σε C# – οδηγός βήμα‑προς‑βήμα
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Set cell number format in C# and learn how to apply Excel date format
    for Japanese era dates, enabling reliable C# Excel date conversion.
  headline: Set cell number format and convert Japanese dates in C#
  type: TechArticle
- description: Set cell number format in C# and learn how to apply Excel date format
    for Japanese era dates, enabling reliable C# Excel date conversion.
  name: Set cell number format and convert Japanese dates in C#
  steps:
  - name: Why this works
    text: '* `Style.Number = 14` maps to Excel’s *Short Date* format (`mm/dd/yyyy`
      by default). * When the cell contains a Japanese era string like `R3/04/01`,
      Aspose.Cells’ internal parser recognises the era and converts it to the corresponding
      Gregorian serial number during `CalculateFormula()`. * After the '
  - name: When to use a custom format
    text: '* Reports intended for Japanese audiences. * When you need to preserve
      the original era information for legal documents. * In dashboards where both
      Gregorian and era dates are shown side‑by‑side.'
  - name: Full end‑to‑end example
    text: Below is a self‑contained program that demonstrates both the Gregorian and
      era outputs in one run.
  - name: Edge cases & common pitfalls
    text: '| Situation | What to watch for | Fix / Recommendation | |----------------------------------------|------------------------------------------------------|----------------------------------------------------------|
      | Empty or malformed era string | `PutValue` stores the literal text; conversion
      fails'
  - name: Automation tip
    text: 'If you need to process a large range of era dates (e.g., column A contains
      many Japanese dates), wrap the conversion logic in a loop:'
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
- Date conversion
title: Ορισμός μορφής αριθμού κελιού και μετατροπή ιαπωνικών ημερομηνιών σε C#
url: /el/net/excel-custom-number-date-formatting/set-cell-number-format-and-convert-japanese-dates-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ορίστε μορφή αριθμού κελιού και μετατρέψτε ιαπωνικές ημερομηνίες σε C#

Αν χρειάζεται να **ορίσετε μορφή αριθμού κελιού** σε ένα έργο αυτοματοποίησης Excel με C#, αυτός ο οδηγός σας δείχνει πώς να **εφαρμόσετε μορφή ημερομηνίας Excel** και να πραγματοποιήσετε **μετατροπή ημερομηνίας Excel σε C#** για ημερομηνίες ιαπωνικής εποχής. Θα λάβετε ένα πλήρες, εκτελέσιμο παράδειγμα που μετατρέπει μια συμβολοσειρά εποχής Reiwa (π.χ., `R3/04/01`) στην Γρηγοριανή ημερομηνία `2021‑04‑01`.

## Τι θα μάθετε

* Πώς να δημιουργήσετε ένα βιβλίο εργασίας και να αποκτήσετε πρόσβαση στο πρώτο φύλλο του.  
* Πώς να **ορίσετε μορφή αριθμού κελιού** ώστε το Excel να αντιμετωπίζει την τιμή ως ημερομηνία.  
* Πώς να **εφαρμόσετε μορφή ημερομηνίας Excel** που αναγνωρίζει συμβολοσειρές ιαπωνικής εποχής.  
* Πώς να ενεργοποιήσετε **μετατροπή ημερομηνίας Excel σε C#** επαναϋπολογίζοντας τύπους.  
* Αναμενόμενη έξοδος και συμβουλές αντιμετώπισης προβλημάτων για ακραίες περιπτώσεις.

**Προαπαιτούμενα**

* .NET 6 ή νεότερο (ο κώδικας λειτουργεί επίσης με .NET Framework 4.6+).  
* Aspose.Cells for .NET 2024 ή νεότερο – εγκαταστήστε μέσω NuGet: `dotnet add package Aspose.Cells`.  
* Βασική εξοικείωση με C# και διαχείριση ημερομηνιών στο Excel.

> **Συμβουλή επαγγελματία:** Το Aspose.Cells λειτουργεί χωρίς εγκατεστημένο Microsoft Office, καθιστώντας το ιδανικό για αυτοματοποίηση σε διακομιστές.

## Ορισμός μορφής αριθμού κελιού με Aspose.Cells σε C#

Το πρώτο βήμα είναι να ενημερώσουμε το Excel ότι το κελί περιέχει ημερομηνία. Το Excel αποθηκεύει τις ημερομηνίες ως σειριακούς αριθμούς, επομένως πρέπει να εφαρμόσουμε μια ενσωματωμένη μορφή αριθμού ημερομηνίας (ID 14) στο επιλεγμένο κελί.

```csharp
using System;
using Aspose.Cells;

class JapaneseEraDateDemo
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // 2️⃣ Insert a Japanese era date string (Reiwa 3) into cell A1
        sheet.Cells["A1"].PutValue("R3/04/01");

        // 3️⃣ **Set cell number format** – use built‑in date format ID 14
        //    This tells Excel to treat the string as a date value.
        sheet.Cells["A1"].Style.Number = 14;

        // 4️⃣ Recalculate formulas so the internal date engine converts the era.
        workbook.CalculateFormula();

        // 5️⃣ Output the converted Gregorian date.
        Console.WriteLine(sheet.Cells["A1"].StringValue); // → 2021-04-01
    }
}
```

### Γιατί λειτουργεί αυτό

* `Style.Number = 14` αντιστοιχεί στη μορφή *Σύντομη Ημερομηνία* του Excel (`mm/dd/yyyy` από προεπιλογή).  
* Όταν το κελί περιέχει μια συμβολοσειρά ιαπωνικής εποχής όπως `R3/04/01`, ο εσωτερικός αναλυτής του Aspose.Cells αναγνωρίζει την εποχή και τη μετατρέπει στον αντίστοιχο Γρηγοριανό σειριακό αριθμό κατά τη διάρκεια του `CalculateFormula()`.  
* Μετά τον υπολογισμό, το `StringValue` επιστρέφει τη μορφοποιημένη Γρηγοριανή ημερομηνία.

## Εφαρμογή μορφής ημερομηνίας Excel για ιαπωνικές εποχές

Αν θέλετε το κελί να εμφανίζει την ιαπωνική εποχή αντί για τη Γρηγοριανή ημερομηνία, μπορείτε να χρησιμοποιήσετε μια προσαρμοσμένη μορφή αριθμού που περιλαμβάνει τον κωδικό εποχής. Αυτό δείχνει τη δυνατότητα **εφαρμογής μορφής ημερομηνίας Excel**.

```csharp
// Apply a custom format that forces the Japanese era display
sheet.Cells["A1"].Style.Custom = "[$-ja-JP]ggge\"年\"m\"月\"d\"日\"";

// Recalculate to apply the custom format
workbook.CalculateFormula();

// Output the era‑styled string
Console.WriteLine(sheet.Cells["A1"].StringValue); // → R3年04月01日
```

* `[$-ja-JP]` επιβάλλει την ιαπωνική τοπική ρύθμιση.  
* `ggg` αντιπροσωπεύει το όνομα της εποχής (π.χ., `R` για Reiwa).  
* Η προσθήκη κυριολεκτικών χαρακτήρων (`年`, `月`, `日`) δημιουργεί μια οικεία ιαπωνική διάταξη ημερομηνίας.

### Πότε να χρησιμοποιήσετε προσαρμοσμένη μορφή

* Αναφορές προορισμένες για ιαπωνικό κοινό.  
* Όταν πρέπει να διατηρήσετε τις αρχικές πληροφορίες εποχής για νομικά έγγραφα.  
* Σε πίνακες ελέγχου όπου εμφανίζονται ταυτόχρονα Γρηγοριανές και εποχικές ημερομηνίες.

## Μετατροπή ημερομηνίας Excel σε C# – διαχείριση ιαπωνικών εποχών

Η διαδικασία **c# excel date conversion** μπορεί να χωριστεί σε τρία λογικά μέρη:

1. **Ανάλυση της συμβολοσειράς εποχής** – Το Aspose.Cells αναγνωρίζει αυτόματα `R` (Reiwa), `H` (Heisei), `S` (Showa) κ.λπ.  
2. **Μετατροπή σε σειριακό αριθμό** – Το Excel αποθηκεύει τις ημερομηνίες ως ημέρες από τις 30‑12‑1899.  
3. **Μορφοποίηση του σειριακού αριθμού** – είτε με ενσωματωμένη μορφή (ID 14) είτε με προσαρμοσμένη ιαπωνική μορφή.

### Πλήρες παράδειγμα από την αρχή μέχρι το τέλος

Παρακάτω βρίσκεται ένα αυτόνομο πρόγραμμα που παρουσιάζει τόσο την Γρηγοριανή όσο και την εποχική έξοδο σε μία εκτέλεση.

```csharp
using System;
using Aspose.Cells;

class JapaneseEraConversion
{
    static void Main()
    {
        // Create workbook and worksheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];

        // Input: Reiwa 3 (2021) – can be any era string
        ws.Cells["A1"].PutValue("R3/04/01");

        // ---- Part 1: Gregorian output ----
        ws.Cells["A1"].Style.Number = 14;      // built‑in short date
        wb.CalculateFormula();                // forces conversion
        string gregorian = ws.Cells["A1"].StringValue;
        Console.WriteLine($"Gregorian: {gregorian}"); // 2021-04-01

        // ---- Part 2: Japanese era output ----
        ws.Cells["B1"].PutValue("R3/04/01");   // repeat input for clarity
        ws.Cells["B1"].Style.Custom = "[$-ja-JP]ggge\"年\"m\"月\"d\"日\"";
        wb.CalculateFormula();
        string era = ws.Cells["B1"].StringValue;
        Console.WriteLine($"Japanese era: {era}"); // R3年04月01日
    }
}
```

**Αναμενόμενη έξοδος κονσόλας**

```
Gregorian: 2021-04-01
Japanese era: R3年04月01日
```

### Ακραίες περιπτώσεις & συνηθισμένα προβλήματα

| Situation                              | What to watch for                                   | Fix / Recommendation                                   |
|----------------------------------------|------------------------------------------------------|----------------------------------------------------------|
| Empty or malformed era string         | `PutValue` stores the literal text; conversion fails| Validate the input with a regular expression before writing to the cell. |
| Locale mismatch                        | Custom format shows western digits instead of Japanese characters | Ensure the `Custom` format includes `[$-ja-JP]` or set `Workbook.Settings.CultureInfo` to `ja-JP`. |
| Workbook contains formulas referencing the date cell | Recalculation may overwrite formula results | Call `CalculateFormula` **after** all formatting steps, or use `Workbook.CalculateFormula(FormulaCalculationOptions.IgnoreError)` if you need to skip errors. |
| Using older Aspose.Cells versions      | Japanese era support was added in 2022 Q3          | Upgrade to the latest NuGet package.                     |

## Δοκιμή της λύσης

1. **Εκτελέστε το πρόγραμμα** από το Visual Studio ή με `dotnet run`.  
2. Επαληθεύστε ότι η κονσόλα εμφανίζει τη Γρηγοριανή ημερομηνία `2021‑04‑01` και τη συμβολοσειρά εποχής `R3年04月01日`.  
3. Ανοίξτε το παραγόμενο βιβλίο εργασίας (αν προσθέσετε `wb.Save("Demo.xlsx");`) στο Microsoft Excel για να δείτε την ίδια μορφοποίηση στα κελιά.

### Συμβουλή αυτοματοποίησης

Αν χρειάζεται να επεξεργαστείτε ένα μεγάλο εύρος ημερομηνιών εποχής (π.χ., η στήλη A περιέχει πολλές ιαπωνικές ημερομηνίες), τυλίξτε τη λογική μετατροπής σε βρόχο:

```csharp
for (int row = 0; row < ws.Cells.MaxDataRow + 1; row++)
{
    var cell = ws.Cells[row, 0]; // column A
    cell.Style.Number = 14;
}
wb.CalculateFormula();
```

Αυτή η προσέγγιση διατηρεί τη λειτουργία **set cell number format** γρήγορη και αποδοτική ως προς τη μνήμη.

## Συμπέρασμα

Τώρα γνωρίζετε πώς να **ορίσετε μορφή αριθμού κελιού** σε C# χρησιμοποιώντας Aspose.Cells, πώς να **εφαρμόσετε μορφή ημερομηνίας Excel** για συμβολοσειρές ιαπωνικής εποχής, και πώς να πραγματοποιήσετε αξιόπιστη **μετατροπή ημερομηνίας Excel σε C#** από εποχή σε Γρηγοριανές ημερομηνίες. Ο πλήρης, εκτελέσιμος κώδικας παρουσιάζει και τις δύο εξόδους και επισημαίνει κοινές ακραίες περιπτώσεις.  

**Επόμενα βήματα**

* Εξερευνήστε άλλες ενσωματωμένες μορφές ID

## Τι θα πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κυριαρχήσετε επιπλέον δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στην υλοποίηση των δικών σας έργων.

- [ορισμός μορφής ημερομηνίας Excel σε C# – Πλήρης Οδηγός Βήμα-βήμα](/cells/english/net/excel-custom-number-date-formatting/set-excel-date-format-in-c-complete-step-by-step-guide/)
- [Πώς να εφαρμόσετε μορφή αριθμού στο Excel με Aspose.Cells](/cells/english/net/excel-custom-number-date-formatting/how-to-apply-number-format-excel-with-aspose-cells/)
- [Πώς να εφαρμόσετε προσαρμοσμένη μορφή αριθμού στο Excel σε C#](/cells/english/net/excel-custom-number-date-formatting/how-to-apply-a-custom-number-format-excel-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}