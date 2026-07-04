---
category: general
date: 2026-07-03
description: Μάθετε πώς να εξάγετε έναν πίνακα Excel σε αρχείο .txt και να αποθηκεύσετε
  έναν πίνακα Excel σε αρχείο .txt χρησιμοποιώντας C#. Εξάγετε δεδομένα Excel ως απλό
  κείμενο με πλήρες παράδειγμα κώδικα.
draft: false
keywords:
- how to export excel table
- save excel table to .txt file
- export excel data as plain text
- Aspose.Cells export table
- C# Excel to text
language: el
og_description: Πώς να εξάγετε έναν πίνακα Excel ως απλό κείμενο. Αυτός ο οδηγός σας
  δείχνει πώς να εξάγετε δεδομένα Excel ως απλό κείμενο και να αποθηκεύσετε τον πίνακα
  Excel σε αρχείο .txt με το Aspose.Cells.
og_title: Πώς να εξάγετε πίνακα Excel – Πλήρης οδηγός C#
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Learn how to export Excel table to a .txt file and save Excel table
    to .txt file using C#. Export Excel data as plain text with full code example.
  headline: How to Export Excel Table – Complete Step‑by‑Step Guide
  type: TechArticle
tags:
- C#
- Excel
- Aspose.Cells
- File I/O
title: Πώς να εξάγετε πίνακα Excel – Πλήρης οδηγός βήμα‑προς‑βήμα
url: /el/net/excel-data-export-retrieval/how-to-export-excel-table-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Εξάγετε Πίνακα Excel – Ολοκληρωμένος Οδηγός Βήμα‑Βήμα

Έχετε αναρωτηθεί ποτέ **πώς να εξάγετε πίνακα Excel** χωρίς να φορτώνετε ολόκληρο το βιβλίο εργασίας στη μνήμη; Δεν είστε ο μόνος. Σε πολλές εργασίες αυτοματοποίησης το σύστημα‑προορισμός δέχεται μόνο ένα απλό αρχείο `.txt`, οπότε χρειάζεται να **αποθηκεύσετε πίνακα Excel σε αρχείο .txt** γρήγορα και αξιόπιστα.  

Σε αυτό το σεμινάριο θα περάσουμε βήμα‑βήμα μια καθαρή λύση C# που **εξάγει δεδομένα Excel ως απλό κείμενο** χρησιμοποιώντας το Aspose.Cells. Στο τέλος θα έχετε ένα έτοιμο προς εκτέλεση πρόγραμμα, θα καταλάβετε γιατί κάθε γραμμή είναι σημαντική, και θα δείτε πώς να προσαρμόσετε την εξαγωγή για τις δικές σας ειδικές περιπτώσεις.

## Τι Θα Χρειαστεί

- **Aspose.Cells for .NET** (οποιαδήποτε πρόσφατη έκδοση, π.χ., 23.12).  
- .NET 6 SDK ή νεότερο – ο κώδικας μεταγλωττίζεται και με .NET Core.  
- Ένα δείγμα `input.xlsx` που περιέχει τουλάχιστον έναν πίνακα Excel.  
- Ένα πρόγραμμα επεξεργασίας κειμένου ή IDE (Visual Studio, VS Code, Rider… όπως προτιμάτε).

Δεν απαιτούνται επιπλέον πακέτα NuGet εκτός από το Aspose.Cells, και όλο το σύστημα λειτουργεί σε Windows, Linux ή macOS.

## Βήμα 1: Ρύθμιση του Έργου και Εισαγωγών

Πρώτα, δημιουργήστε μια εφαρμογή κονσόλας και φέρετε τα απαραίτητα namespaces στο πεδίο ορατότητας.

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelTableExport
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll place the export logic here.
        }
    }
}
```

> **Συμβουλή επαγγελματία:** Αν χρησιμοποιείτε το .NET CLI, εκτελέστε `dotnet new console -n ExcelTableExport` και στη συνέχεια `dotnet add package Aspose.Cells` πριν επικολλήσετε τον κώδικα παραπάνω.

## Βήμα 2: Φόρτωση του Workbook και Λήψη του Πρώτου Worksheet

Το αντικείμενο workbook αντιπροσωπεύει ολόκληρο το αρχείο Excel. Η φόρτωσή του μία φορά διατηρεί τη χρήση μνήμης χαμηλή.

```csharp
// Step 2: Load the workbook and get the first worksheet
Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");
Worksheet ws = wb.Worksheets[0];
```

Γιατί επιλέγουμε το πρώτο worksheet; Σε πολλές δημιουργημένες αναφορές τα δεδομένα βρίσκονται στο πρώτο φύλλο, αλλά μπορείτε να αλλάξετε το δείκτη ή να χρησιμοποιήσετε `wb.Worksheets["SheetName"]` για ένα ονομαστικό φύλλο.

## Βήμα 3: Ανάκτηση του Πρώτου Πίνακα που Ορίζεται στο Worksheet

Οι πίνακες Excel (ListObjects) μας παρέχουν δομημένα δεδομένα, καθιστώντας την εξαγωγή προβλέψιμη.

```csharp
// Step 3: Retrieve the first table defined on the worksheet
Table tbl = ws.Tables[0];
```

Αν το workbook σας περιέχει πολλούς πίνακες, απλώς επαναλάβετε το `ws.Tables` ή επιλέξτε με `tbl.Name`.

## Βήμα 4: Διαμόρφωση Επιλογών Εξαγωγής – Εξαγωγή Κάθε Κελιού ως String

Το Aspose.Cells σας επιτρέπει να ελέγχετε τη μορφή κάθε κελιού κατά την εξαγωγή. Η ρύθμιση `ExportAsString` εξασφαλίζει ότι αριθμοί, ημερομηνίες και τύποι γίνονται απλό κείμενο.

```csharp
// Step 4: Set up export options – export every cell as a string
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true
};
```

### Προσθήκη Προσαρμοσμένης Ενέργειας Εξαγωγής για Αφαίρεση Κενών Χαρακτήρων

Συχνά τα δεδομένα προέλευσης περιέχουν αρχικά ή τελικά κενά. Η αφαίρεσή τους κάνει το τελικό αρχείο `.txt` πιο καθαρό.

```csharp
// Define a custom export action to trim cell values before writing
exportOptions.CustomExport = (cell, writer) =>
{
    writer.Write(cell.StringValue.Trim());
};
```

Η λήψη (lambda) λαμβάνει το αντικείμενο `Cell` και ένα `TextWriter`. Μπορείτε επίσης να προσθέσετε λογική υπό συνθήκη εδώ—π.χ., να αντικαταστήσετε τα κόμματα με ερωτηματικά για έξοδο τύπου CSV.

## Βήμα 5: Εξαγωγή του Πίνακα Ξεκινώντας από το Κελί A1 σε Αρχείο Κειμένου

Τώρα γράφουμε πραγματικά τον πίνακα στο δίσκο. Η μέθοδος `ExportTable` διασχίζει τον πίνακα γραμμή‑με‑γραμμή, εφαρμόζοντας τις επιλογές που μόλις ορίσαμε.

```csharp
// Step 5: Export the table starting at cell A1 to a text file
using (StreamWriter writer = new StreamWriter("YOUR_DIRECTORY/Table.txt"))
{
    ws.Cells.ExportTable(tbl, "A1", exportOptions, writer);
}
```

**Τι θα δείτε:** Κάθε γραμμή του πίνακα Excel γίνεται μια γραμμή στο `Table.txt`. Οι στήλες χωρίζονται από χαρακτήρα tab (`\t`) εξ ορισμού—τέλεια για επεξεργασία από το σύστημα‑προορισμό.

### Παράδειγμα Αναμενόμενης Εξόδου

Υποθέτοντας ότι το `input.xlsx` περιέχει έναν πίνακα με τρεις στήλες (`ID`, `Name`, `Score`) και δύο γραμμές δεδομένων, το `Table.txt` θα φαίνεται ως εξής:

```
1    Alice    85
2    Bob      92
```

Παρατηρήστε ότι τα κενά έχουν αφαιρεθεί, και όλα είναι απλό κείμενο—ακριβώς αυτό που απαιτεί η απαίτηση **export excel data as plain text**.

## Διαχείριση Συνηθισμένων Ακραίων Περιπτώσεων

| Situation | What to Do | Why |
|-----------|------------|-----|
| **Ο πίνακας έχει κενά κελιά** | Η λήψη (lambda) γράφει `cell.StringValue.Trim()` που επιστρέφει κενή συμβολοσειρά για κενά. | Διατηρεί την ευθυγράμμιση των στηλών χωρίς να προσθέτει ανεπιθύμητους χαρακτήρες. |
| **Χρειάζεστε προσαρμοσμένο διαχωριστικό** | Αντικαταστήστε το `writer.Write(cell.StringValue.Trim());` με `writer.Write($"{cell.StringValue.Trim()},");` και αφαιρέστε το τελικό διαχωριστικό μετά από κάθε γραμμή. | Ορισμένα συστήματα προτιμούν κόμματα ή κάθετες γραμμές αντί για tabs. |
| **Μεγάλα worksheets ( > 100 k γραμμές )** | Χρησιμοποιήστε `ExportTableOptions` με `ExportAsString = true` και ρέξτε το αρχείο όπως φαίνεται· το Aspose.Cells επεξεργάζεται τις γραμμές σε ροή, αποφεύγοντας σφάλματα OOM. | Εγγυάται κλιμακωσιμότητα. |
| **Πολλαπλοί πίνακες σε ένα φύλλο** | Επαναλάβετε το `ws.Tables` και καλέστε `ExportTable` για κάθε έναν, προαιρετικά προσθέτοντας μια γραμμή διαχωριστή μεταξύ των εξαγωγών. | Σας επιτρέπει να **save Excel table to .txt file** για κάθε πίνακα. |

## Πλήρες Παράδειγμα Λειτουργίας

Παρακάτω είναι το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε‑επικολλήσετε στο `Program.cs`. Αντικαταστήστε το `YOUR_DIRECTORY` με μια απόλυτη ή σχετική διαδρομή που υπάρχει στον υπολογιστή σας.

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelTableExport
{
    class Program
    {
        static void Main(string[] args)
        {
            // Load workbook
            Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");
            Worksheet ws = wb.Worksheets[0];

            // Get first table
            if (ws.Tables.Count == 0)
            {
                Console.WriteLine("No tables found on the first worksheet.");
                return;
            }
            Table tbl = ws.Tables[0];

            // Configure export options
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                ExportAsString = true,
                CustomExport = (cell, writer) =>
                {
                    // Trim whitespace and write value
                    writer.Write(cell.StringValue.Trim());
                }
            };

            // Export to text file
            string outputPath = "YOUR_DIRECTORY/Table.txt";
            using (StreamWriter writer = new StreamWriter(outputPath))
            {
                ws.Cells.ExportTable(tbl, "A1", exportOptions, writer);
            }

            Console.WriteLine($"Table exported successfully to {outputPath}");
        }
    }
}
```

Εκτελέστε το πρόγραμμα με `dotnet run`. Αν όλα έχουν ρυθμιστεί σωστά, θα δείτε το μήνυμα επιβεβαίωσης και ένα φρέσκο δημιουργημένο `Table.txt` που περιέχει το **export excel data as plain text**.

## Μπόνους: Οπτική Επιβεβαίωση (Προαιρετικό)

Αν θέλετε να δείτε μια γρήγορη λήψη οθόνης του τελικού αρχείου, μπορείτε να το ανοίξετε σε οποιονδήποτε επεξεργαστή κειμένου. Παρακάτω είναι μια εικόνα κράτησης θέσης που δείχνει την αναμενόμενη διάταξη.

![πώς να εξάγετε πίνακα excel screenshot](https://example.com/images/export-excel-table.png "πώς να εξάγετε πίνακα excel")

*Alt text:* **πώς να εξάγετε πίνακα excel** – δείχνει έξοδο απλού κειμένου ενός εξαγόμενου πίνακα Excel.

## Ανακεφαλαίωση & Επόμενα Βήματα

Έχουμε καλύψει όλα όσα χρειάζεται να γνωρίζετε **πώς να εξάγετε πίνακα Excel** χρησιμοποιώντας το Aspose.Cells, από τη φόρτωση του workbook μέχρι την αφαίρεση κενών τιμών κελιών και τελικά τη δημιουργία ενός καθαρού αρχείου `.txt`.  

- Τώρα καταλαβαίνετε **save Excel table to .txt file** με προσαρμοσμένη λογική.  
- Μπορείτε να προσαρμόσετε τη λήψη (lambda) για να διαχειρίζεται ημερομηνίες, αριθμούς ή προσαρμοσμένα διαχωριστικά.  
- Για μεγαλύτερα έργα, σκεφτείτε να ενσωματώσετε τη λογική σε μια επαναχρησιμοποιήσιμη μέθοδο ή κλάση.

**Τι ακολουθεί;** Δοκιμάστε την εξαγωγή πολλαπλών πινάκων, ή αλλάξτε τη μορφή εξόδου σε CSV αλλάζοντας το διαχωριστικό. Μπορείτε επίσης να εξερευνήσετε το **export excel data as plain text** απευθείας σε ροή δικτύου για ενσωματώσεις σε πραγματικό χρόνο.

Έχετε ερωτήσεις ή αντιμετωπίζετε πρόβλημα; Αφήστε ένα σχόλιο, και καλή προγραμματιστική!

## Τι Θα Μάθετε Στη Σύντομη Μελλοντική;

Τα παρακάτω σεμινάρια καλύπτουν στενά συναφή θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να Εξάγετε Αρχεία Excel σε .NET Χρησιμοποιώντας το Aspose.Cells: Ένας Πλήρης Οδηγός](/cells/english/net/workbook-operations/export-excel-files-net-aspose-cells-guide/)
- [Πώς να Εξάγετε Ορατές Γραμμές Excel Χρησιμοποιώντας το Aspose.Cells για .NET: Οδηγός Βήμα‑Βήμα](/cells/english/net/workbook-operations/export-visible-rows-aspose-cells-dotnet/)
- [Πώς να Συνδυάσετε Φύλλα Excel σε Ένα Αρχείο Κειμένου Χρησιμοποιώντας το Aspose.Cells για .NET](/cells/english/net/workbook-operations/combine-excel-sheets-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}