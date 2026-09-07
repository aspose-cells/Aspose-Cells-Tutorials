---
category: general
date: 2026-02-28
description: Μάθετε πώς να ορίζετε τη μορφή ημερομηνίας στο Excel, να διαβάζετε ημερομηνία/ώρα
  στο Excel, να εξάγετε την ημερομηνία από το Excel και να υπολογίζετε τύπους του
  βιβλίου εργασίας χρησιμοποιώντας το Aspose.Cells σε C#. Πλήρες εκτελέσιμο παράδειγμα.
draft: false
keywords:
- set excel date format
- read excel datetime
- extract date from excel
- calculate workbook formulas
- get datetime cell
language: el
og_description: Μάθετε να ρυθμίζετε τη μορφή ημερομηνίας του Excel, να διαβάζετε ημερομηνίες/ώρα,
  να εξάγετε ημερομηνίες και να υπολογίζετε τύπους βιβλίου εργασίας με πλήρες παράδειγμα
  σε C#.
og_title: Ορισμός μορφής ημερομηνίας Excel σε C# – Πλήρης Οδηγός Βήμα‑προς‑Βήμα
tags:
- Aspose.Cells
- C#
- Excel automation
title: Ορισμός μορφής ημερομηνίας στο Excel με C# – Πλήρης Οδηγός Βήμα‑προς‑Βήμα
url: /el/net/excel-custom-number-date-formatting/set-excel-date-format-in-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ορισμός μορφής ημερομηνίας excel – Πλήρης Οδηγός C#

Έχετε ποτέ δυσκολευτεί να **ορίσετε μορφή ημερομηνίας excel** όταν δημιουργείτε υπολογιστικά φύλλα εν κινήσει; Δεν είστε μόνοι. Πολλοί προγραμματιστές συναντούν πρόβλημα όταν το κελί εμφανίζει μια ακατέργαστη συμβολοσειρά αντί για μια σωστή ημερομηνία, ειδικά με ημερομηνίες ιαπωνικής εποχής ή προσαρμοσμένες συμβολοσειρές τοπικής ρύθμισης.  

Σε αυτό το tutorial θα περάσουμε από ένα πραγματικό παράδειγμα που **ορίζει τη μορφή ημερομηνίας Excel**, στη συνέχεια **διαβάζει το datetime του Excel**, **εξάγει την ημερομηνία από το Excel**, και ακόμη **υπολογίζει τύπους βιβλίου εργασίας** ώστε να μπορείτε τελικά να **λάβετε τιμές κελιού datetime** ως αντικείμενα .NET `DateTime`. Χωρίς εξωτερικές αναφορές, μόνο ένα αυτόνομο, εκτελέσιμο απόσπασμα που μπορείτε να επικολλήσετε στο Visual Studio και να δείτε αμέσως σε λειτουργία.

## Τι Θα Χρειαστείτε

- **Aspose.Cells for .NET** (οποιαδήποτε πρόσφατη έκδοση· το API που χρησιμοποιείται εδώ λειτουργεί με 23.x και νεότερες)  
- .NET 6 ή νεότερο (ο κώδικας μεταγλωττίζεται επίσης με .NET Framework 4.6+)  
- Βασική κατανόηση της σύνταξης C# – αν μπορείτε να γράψετε `Console.WriteLine`, είστε έτοιμοι.

Αυτό είναι όλο. Δεν χρειάζονται επιπλέον πακέτα NuGet πέρα από το Aspose.Cells, δεν απαιτείται εγκατάσταση Excel.

## Πώς να ορίσετε μορφή ημερομηνίας excel σε C#  

Το πρώτο βήμα είναι να πούμε στο Excel ότι το κελί περιέχει ημερομηνία, όχι απλό κείμενο. Το Aspose.Cells παρέχει ένα ενσωματωμένο ID μορφής αριθμού (`14`) που αντιστοιχεί στο σύντομο πρότυπο ημερομηνίας της τρέχουσας τοπικής ρύθμισης.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // Step 2: Write a Japanese era date string into cell A1
        sheet.Cells["A1"].PutValue("Reiwa 2-04-01");

        // Step 3: Apply the standard date number format (ID 14) to A1
        // This tells Excel to treat the cell as a date.
        sheet.Cells["A1"].Style.Number = 14;

        // Step 4: Force Excel to recalculate formulas so the value is parsed
        workbook.CalculateFormula();

        // Step 5: Retrieve the parsed value as a .NET DateTime
        DateTime parsedDate = sheet.Cells["A1"].GetDateTime();

        // Step 6: Show the result – should be 2020‑04‑01
        Console.WriteLine($"Parsed DateTime: {parsedDate:yyyy-MM-dd}");
    }
}
```

> **Συμβουλή:** Η κλήση `CalculateFormula()` είναι κρίσιμη. Χωρίς αυτή, το κελί παραμένει με την ακατέργαστη συμβολοσειρά και το `GetDateTime()` θα πετάξει εξαίρεση. Αυτή η γραμμή αναγκάζει το Aspose.Cells να εκτελέσει τον εσωτερικό του parser, υπολογίζοντας ουσιαστικά **τους τύπους του βιβλίου εργασίας** για εμάς.

Η έξοδος που θα δείτε όταν εκτελέσετε το πρόγραμμα είναι:

```
Parsed DateTime: 2020-04-01
```

Αυτό επιβεβαιώνει ότι καταφέραμε να **ορίσουμε μορφή ημερομηνίας excel**, και ότι μπορέσαμε να **λάβουμε κελί datetime** ως σωστό `DateTime`.

## Ανάγνωση τιμών datetime από excel  

Τώρα που η ημερομηνία αποθηκεύτηκε σωστά, μπορεί να αναρωτιέστε πώς να την ανακτήσετε αργότερα, ίσως από ένα υπάρχον αρχείο. Η ίδια μέθοδος `GetDateTime()` λειτουργεί σε οποιοδήποτε κελί που ήδη έχει μορφή ημερομηνίας.

```csharp
// Assuming 'sheet' is already loaded from an existing workbook
DateTime existingDate = sheet.Cells["B5"].GetDateTime();
Console.WriteLine($"Cell B5 contains: {existingDate:d}");
```

Αν το κελί δεν είναι μορφοποιημένο ως ημερομηνία, το `GetDateTime()` επιστρέφει `DateTime.MinValue`. Γι’ αυτό πάντα **πρέπει πρώτα να ορίσετε μορφή ημερομηνίας excel**.

## Εξαγωγή ημερομηνίας από κελιά excel  

Μερικές φορές το κελί περιέχει πλήρη χρονική σήμανση (ημερομηνία + ώρα) αλλά χρειάζεστε μόνο το μέρος της ημερομηνίας. Μπορείτε να αποκόψετε το στοιχείο ώρας χρησιμοποιώντας `.Date` στο επιστρεφόμενο `DateTime`.

```csharp
DateTime fullStamp = sheet.Cells["C3"].GetDateTime(); // e.g., 2023-07-15 14:30:00
DateTime onlyDate = fullStamp.Date;                  // 2023-07-15 00:00:00
Console.WriteLine($"Date only: {onlyDate:yyyy-MM-dd}");
```

Αυτή η προσέγγιση λειτουργεί ανεξάρτητα από τη βασική μορφή αριθμού του Excel, εφόσον το κελί αναγνωρίζεται ως ημερομηνία.

## Υπολογισμός τύπων βιβλίου εργασίας  

Τι γίνεται αν η ημερομηνία είναι αποτέλεσμα τύπου, όπως `=TODAY()` ή `=DATE(2022,5,10)`; Το Aspose.Cells θα αξιολογήσει τον τύπο όταν καλέσετε `CalculateFormula()`. Μετά από αυτό, το κελί συμπεριφέρεται ακριβώς όπως μια χειροκίνητα εισαχθείσα ημερομηνία.

```csharp
sheet.Cells["D2"].Formula = "=TODAY()";
workbook.CalculateFormula(); // Re‑evaluate the sheet
DateTime today = sheet.Cells["D2"].GetDateTime();
Console.WriteLine($"Today is: {today:yyyy-MM-dd}");
```

Παρατηρήστε ότι δεν χρειάστηκε να αλλάξουμε το στυλ του κελιού· το Excel ήδη αντιμετωπίζει τα αποτελέσματα τύπων ως ημερομηνίες όταν ο τύπος επιστρέφει έναν σειριακό αριθμό που αντιστοιχεί σε ημερομηνία.

## Λήψη κελιού datetime από υπάρχον βιβλίο εργασίας  

Συνδυάζοντας όλα τα παραπάνω, εδώ είναι μια σύντομη ρουτίνα που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο για να ανοίξετε ένα αρχείο Excel, να διασφαλίσετε ότι όλα τα κελιά ημερομηνίας ερμηνεύονται σωστά, και να επιστρέψετε μια λίστα αντικειμένων `DateTime`.

```csharp
using System.Collections.Generic;
using Aspose.Cells;

static List<DateTime> ExtractAllDates(string filePath)
{
    Workbook wb = new Workbook(filePath);
    Worksheet ws = wb.Worksheets[0];
    wb.CalculateFormula(); // Make sure formulas are evaluated

    var dates = new List<DateTime>();
    foreach (Cell cell in ws.Cells)
    {
        // Check if the cell has a date number format (ID 14‑22 are common date formats)
        if (cell.GetStyle().Number >= 14 && cell.GetStyle().Number <= 22)
        {
            dates.Add(cell.GetDateTime());
        }
    }
    return dates;
}
```

Η κλήση `ExtractAllDates("Sample.xlsx")` θα σας δώσει κάθε ημερομηνία που **ορίστηκε μορφή ημερομηνίας excel** σωστά στο πρώτο φύλλο.

## Συνηθισμένα Πόδια & Πώς να τα Αποφύγετε  

| Πρόβλημα | Γιατί Συμβαίνει | Διόρθωση |
|----------|----------------|----------|
| `GetDateTime()` πετάει `ArgumentException` | Το κελί δεν αναγνωρίζεται ως ημερομηνία (λείπει η μορφή αριθμού) | Εφαρμόστε `Style.Number = 14` **πριν** καλέσετε `CalculateFormula()` |
| Η ημερομηνία εμφανίζεται ως `1900‑01‑00` | Ο σειριακός αριθμός 0 του Excel ερμηνεύεται ως η αρχή | Βεβαιωθείτε ότι το κελί περιέχει έγκυρο σειριακό (>0) |
| Συμβολοσειρές ιαπωνικής εποχής δεν αναλύονται | Το Aspose.Cells αναλύει συμβολοσειρές εποχής μόνο μετά το `CalculateFormula()` | Διατηρήστε τη ακατέργαστη συμβολοσειρά, ορίστε μορφή ημερομηνίας, μετά καλέστε `CalculateFormula()` |
| Μετατοπίσεις ζώνης ώρας | Το `DateTime` αποθηκεύεται χωρίς πληροφορίες ζώνης, αλλά η εφαρμογή σας μπορεί να το εμφανίζει σε διαφορετική τοπική ρύθμιση | Χρησιμοποιήστε `DateTimeKind.Utc` ή μετατρέψτε ρητά αν χρειάζεται |

## Εικόνα – Οπτική Σύνοψη  

![set excel date format example](excel-date-format.png "set excel date format example")

Το διάγραμμα απεικονίζει τη ροή: **εγγραφή συμβολοσειράς → εφαρμογή μορφής αριθμού → επανυπολογισμός → ανάκτηση DateTime**.

## Συμπέρασμα  

Καλύψαμε όλα όσα χρειάζεστε για να **ορίσετε μορφή ημερομηνίας excel**, **να διαβάσετε datetime από excel**, **να εξάγετε ημερομηνία από excel**, **να υπολογίσετε τύπους βιβλίου εργασίας**, και τελικά να **λάβετε τιμές κελιού datetime** ως εγγενή αντικείμενα .NET. Ο πλήρης, εκτελέσιμος κώδικας είναι έτοιμος για αντιγραφή‑επικόλληση, και οι εξηγήσεις σας δίνουν το «γιατί» πίσω από κάθε βήμα, ώστε να προσαρμόσετε το μοτίβο σε πιο σύνθετα σενάρια.

### Τι Ακολουθεί;

- **Μαζική εισαγωγή/εξαγωγή:** Χρησιμοποιήστε τη βοηθητική `ExtractAllDates` για επεξεργασία μεγάλων αναφορών.  
- **Προσαρμοσμένες μορφές ημερομηνίας:** Αντικαταστήστε το `Style.Number = 14` με `Style.Custom = "yyyy/mm/dd"` για ανεξάρτητη από τοπική ρύθμιση μορφοποίηση.  
- **Ημερομηνίες με γνώση ζώνης ώρας:** Συνδυάστε `DateTimeOffset` με τους σειριακούς αριθμούς του Excel για παγκόσμιες εφαρμογές.

Πειραματιστείτε, προσθέστε υπό-συνθήκες μορφοποίησης ή σπρώξτε τις ημερομηνίες σε βάση δεδομένων. Αν συναντήσετε προβλήματα, αφήστε ένα σχόλιο—καλή προγραμματιστική!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}