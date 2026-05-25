---
category: general
date: 2026-02-14
description: Αναλύστε τις ημερομηνίες ιαπωνικής εποχής στο Excel με προσαρμοσμένη
  ανάλυση ημερομηνιών. Μάθετε πώς να φορτώνετε το βιβλίο εργασίας από αρχείο χρησιμοποιώντας
  τη λειτουργία load excel με επιλογές και να αποφεύγετε τα κοινά προβλήματα.
draft: false
keywords:
- parse japanese era dates
- load excel with options
- load workbook from file
- custom date parsing excel
language: el
og_description: Αναλύστε ημερομηνίες ιαπωνικής εποχής στο Excel χρησιμοποιώντας το
  Aspose.Cells. Αυτός ο οδηγός δείχνει πώς να φορτώσετε ένα βιβλίο εργασίας από αρχείο
  με προσαρμοσμένες επιλογές ανάλυσης ημερομηνιών.
og_title: Ανάλυση ημερομηνιών ιαπωνικής εποχής – Βήμα‑βήμα C# οδηγός
tags:
- Aspose.Cells
- C#
- Excel automation
title: Ανάλυση ημερομηνιών ιαπωνικής εποχής στο Excel – Πλήρης οδηγός για προγραμματιστές
  C#
url: /el/net/data-loading-and-parsing/parse-japanese-era-dates-in-excel-full-guide-for-c-developer/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ανάλυση Ημερομηνιών Ιαπωνικής Εποχής – Πλήρης Εγχειρίδιο C#

Έχετε ποτέ χρειαστεί να **αναλύσετε ημερομηνίες ιαπωνικής εποχής** από ένα φύλλο Excel και να αναρωτηθήκατε γιατί οι τιμές μετατρέπονται σε περίεργους αριθμούς; Δεν είστε μόνοι. Πολλοί προγραμματιστές αντιμετωπίζουν αυτό το πρόβλημα όταν ο προεπιλεγμένος αναλυτής `DateTime` δεν αναγνωρίζει το στυλ “Reiwa 1/04/01” που χρησιμοποιείται στα ιαπωνικά ημερολόγια.  

Καλή είδηση: μπορείτε να πείτε στο Aspose.Cells να αντιμετωπίζει αυτά τα κελιά ως ημερομηνίες ιαπωνικής εποχής αμέσως από τη στιγμή που **φορτώνετε το Excel με επιλογές**. Σε αυτόν τον οδηγό θα περάσουμε από τη φόρτωση ενός βιβλίου εργασίας από αρχείο, τη διαμόρφωση προσαρμοσμένης ανάλυσης ημερομηνίας και την επαλήθευση ότι οι ημερομηνίες εμφανίζονται ακριβώς όπως περιμένετε.

Στο τέλος αυτού του σεμιναρίου θα μπορείτε να:

* Φορτώσετε ένα βιβλίο εργασίας από αρχείο καθορίζοντας το `DateTimeParsing.JapaneseEra`.
* Πρόσβαση στις τιμές των κελιών ως σωστά αντικείμενα `DateTime`.
* Αντιμετωπίσετε ειδικές περιπτώσεις όπως κενά κελιά ή μεικτά ημερολόγια.
* Επεκτείνετε την προσέγγιση σε οποιοδήποτε σενάριο **custom date parsing excel** που μπορεί να συναντήσετε.

> **Απαιτούμενο** – Χρειάζεστε τη βιβλιοθήκη Aspose.Cells for .NET (v23.9 ή νεότερη) και ένα IDE συμβατό με .NET (Visual Studio, Rider κ.λπ.). Δεν απαιτούνται άλλα πακέτα.

## Βήμα 1: Διαμόρφωση Επιλογών Φόρτωσης Κειμένου για Ανάλυση Ιαπωνικής Εποχής  

Το πρώτο που κάνουμε είναι να πούμε στον φορτωτή πώς να ερμηνεύει κείμενο που μοιάζει με ημερομηνία ιαπωνικής εποχής. Αυτό γίνεται μέσω του `TxtLoadOptions` και του enum `DateTimeParsing`.

```csharp
using Aspose.Cells;

// Step 1: Set up load options to understand Japanese era dates
TxtLoadOptions loadOptions = new TxtLoadOptions
{
    // This flag makes the parser treat “R1/04/01” as 2024‑04‑01, etc.
    DateTimeParsing = DateTimeParsing.JapaneseEra
};
```

**Γιατί είναι σημαντικό:** Χωρίς τη σημαία `JapaneseEra`, το Aspose.Cells αντιμετωπίζει το κελί ως απλό κείμενο, αφήνοντάς σας να χωρίσετε χειροκίνητα το όνομα της εποχής και να το μετατρέψετε. Η σημαία κάνει το σκληρό έργο, διατηρώντας τον κώδικά σας καθαρό και λιγότερο επιρρεπή σε σφάλματα.

## Βήμα 2: Φόρτωση Βιβλίου Εργασίας από Αρχείο Χρησιμοποιώντας τις Επιλογές  

Τώρα ανοίγουμε πραγματικά το αρχείο Excel. Παρατηρήστε πώς το αντικείμενο `loadOptions` περνιέται στον κατασκευαστή `Workbook`—αυτό είναι το βήμα **load workbook from file** που σέβεται τους προσαρμοσμένους κανόνες ανάλυσης.

```csharp
// Step 2: Load the workbook with the configured options
string filePath = Path.Combine(Environment.CurrentDirectory, "japan_dates.xlsx");
Workbook workbook = new Workbook(filePath, loadOptions);
```

Αν το αρχείο βρίσκεται κάπου αλλού (π.χ., σε κοινόχρηστο δίκτυο), απλώς προσαρμόστε το `filePath` ανάλογα. Το σημαντικό είναι ότι χρησιμοποιείται η ίδια παρουσία `loadOptions`; διαφορετικά η μετατροπή ιαπωνικής εποχής δεν θα συμβεί.

## Βήμα 3: Πρόσβαση στις Αναλυμένες Ημερομηνίες  

Με το βιβλίο εργασίας φορτωμένο, μπορείτε να ανακτήσετε τις τιμές των κελιών ακριβώς όπως θα κάνατε με οποιαδήποτε κανονική ημερομηνία. Το API επιστρέφει αυτόματα ένα αντικείμενο `DateTime`.

```csharp
// Step 3 (optional): Read a date from the first worksheet, cell A1
Worksheet sheet = workbook.Worksheets[0];
Cell dateCell = sheet.Cells["A1"];

// The Value property is already a DateTime because of our parsing option
DateTime parsedDate = dateCell.DateTimeValue;

// Quick sanity check – print to console
Console.WriteLine($"Parsed date from A1: {parsedDate:yyyy-MM-dd}");
```

**Αναμενόμενη έξοδος** (υποθέτοντας ότι το A1 περιέχει “R1/04/01”):

```
Parsed date from A1: 2024-04-01
```

Αν το κελί περιέχει μια Γρηγοριανή ημερομηνία όπως “2023‑12‑31”, ο αναλυτής λειτουργεί ακόμη—απλώς επιστρέφει την αρχική ημερομηνία αμετάβλητη.

## Βήμα 4: Επαλήθευση Όλων των Ημερομηνιών σε Μια Στήλη  

Συχνά χρειάζεται να σαρώσετε ολόκληρη μια στήλη με ημερομηνίες ιαπωνικής εποχής. Παρακάτω υπάρχει ένας συμπαγής βρόχος που δείχνει πώς να διαχειριστείτε κενά και μεικτό περιεχόμενο με χάρη.

```csharp
// Step 4: Iterate through column B (index 1) and print each parsed date
int firstRow = 0;
int lastRow = sheet.Cells.MaxDataRow; // last row with data

for (int row = firstRow; row <= lastRow; row++)
{
    Cell cell = sheet.Cells[row, 1]; // column B
    if (cell.Type == CellValueType.IsDateTime)
    {
        Console.WriteLine($"Row {row + 1}: {cell.DateTimeValue:yyyy-MM-dd}");
    }
    else if (!cell.IsNull)
    {
        // Fallback: show raw string for non‑date cells
        Console.WriteLine($"Row {row + 1}: (non‑date) {cell.StringValue}");
    }
}
```

**Συμβουλή:** `CellValueType.IsDateTime` είναι ο πιο ασφαλής τρόπος για να ελέγξετε αν η ανάλυση πέτυχε. Σας προστατεύει από `InvalidCastException` όταν ένα κελί περιέχει απροσδόκητο κείμενο.

## Βήμα 5: Συνηθισμένα Πιθανά Προβλήματα & Πώς να τα Διαχειριστείτε  

| Πρόβλημα | Γιατί συμβαίνει | Διόρθωση |
|----------|----------------|----------|
| **Κενά κελιά επιστρέφουν `DateTime.MinValue`** | Ο αναλυτής αντιμετωπίζει τις κενές συμβολοσειρές ως την ελάχιστη ημερομηνία. | Ελέγξτε `cell.IsNull` πριν προσπελάσετε το `DateTimeValue`. |
| **Μεικτά ημερολόγια (Ιαπωνικό + Γρηγοριανό) στην ίδια στήλη** | Ο αναλυτής διαχειρίζεται και τα δύο, αλλά μπορεί να χρειαστεί να τα διακρίνετε για αναφορές. | Χρησιμοποιήστε `cell.StringValue` για να εξετάσετε το αρχικό κείμενο όταν `cell.Type` είναι `IsString`. |
| **Λανθασμένη εποχή (π.χ., “H30” για Heisei) μετά το 2019** | Η Heisei έληξε το 2019· οι μεταγενέστερες ημερομηνίες πρέπει να χρησιμοποιούν “R”. | Επικυρώστε το πρόθεμα της εποχής πριν εμπιστευτείτε το αναλυμένο αποτέλεσμα. |
| **Μείωση απόδοσης σε μεγάλα αρχεία** | Η φόρτωση με προσαρμοσμένες επιλογές προσθέτει μια μικρή επιβάρυνση. | Φορτώστε μόνο τα απαιτούμενα φύλλα εργασίας (`Workbook.LoadOptions.LoadAllWorksheets = false`). |

## Βήμα 6: Πλήρες Παράδειγμα Εργασίας  

Συνδυάζοντας όλα μαζί, εδώ είναι μια αυτόνομη εφαρμογή κονσόλας που μπορείτε να αντιγράψετε‑επικολλήσετε και να εκτελέσετε. Δείχνει **custom date parsing excel** από την αρχή μέχρι το τέλος.

```csharp
// FullExample.cs
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Configure load options for Japanese era dates
        TxtLoadOptions loadOptions = new TxtLoadOptions
        {
            DateTimeParsing = DateTimeParsing.JapaneseEra
        };

        // 2️⃣ Load the workbook from file with those options
        string filePath = Path.Combine(Environment.CurrentDirectory, "japan_dates.xlsx");
        if (!File.Exists(filePath))
        {
            Console.WriteLine($"File not found: {filePath}");
            return;
        }

        Workbook workbook = new Workbook(filePath, loadOptions);
        Worksheet sheet = workbook.Worksheets[0];

        // 3️⃣ Read a single cell (A1) – demonstrates automatic parsing
        Cell a1 = sheet.Cells["A1"];
        Console.WriteLine($"A1 raw value: {a1.StringValue}");
        Console.WriteLine($"A1 parsed date: {a1.DateTimeValue:yyyy-MM-dd}");

        // 4️⃣ Loop through column B to show batch parsing
        Console.WriteLine("\n--- Column B Dates ---");
        int lastRow = sheet.Cells.MaxDataRow;
        for (int row = 0; row <= lastRow; row++)
        {
            Cell cell = sheet.Cells[row, 1]; // B column
            if (cell.Type == CellValueType.IsDateTime)
                Console.WriteLine($"Row {row + 1}: {cell.DateTimeValue:yyyy-MM-dd}");
            else if (!cell.IsNull)
                Console.WriteLine($"Row {row + 1}: (non‑date) {cell.StringValue}");
        }

        // 5️⃣ Optional: Save a copy with dates converted to ISO format
        // This shows that the workbook now holds proper DateTime objects.
        workbook.Save("japan_dates_converted.xlsx");
        Console.WriteLine("\nWorkbook saved as japan_dates_converted.xlsx");
    }
}
```

**Τι θα πρέπει να δείτε** όταν το `japan_dates.xlsx` περιέχει:

| A | B |
|---|---|
| R1/04/01 | 2023‑12‑31 |
| H30/12/31 | R2/01/01 |
| (κενό) | R2/02/15 |

Console output:

```
A1 raw value: R1/04/01
A1 parsed date: 2024-04-01

--- Column B Dates ---
Row 1: 2023-12-31
Row 2: 2025-01-01
Row 3: (non-date) 
Row 4: 2025-02-15
Workbook saved as japan_dates_converted.xlsx
```

Το αποθηκευμένο αρχείο τώρα αποθηκεύει σωστά κελιά ημερομηνίας, τα οποία μπορείτε να ανοίξετε στο Excel και να δείτε τη συνήθη μορφοποίηση ημερομηνίας.

## Συμπέρασμα  

Μόλις δείξαμε πώς να **αναλύσετε ημερομηνίες ιαπωνικής εποχής** στο Excel διαμορφώνοντας το `TxtLoadOptions`, **load workbook from file** με αυτές τις επιλογές, και να εργαστείτε με τις προκύπτουσες τιμές `DateTime`. Το ίδιο μοτίβο—ορισμός προσαρμοσμένων σημαιών ανάλυσης και στη συνέχεια φόρτωση του βιβλίου εργασίας—εφαρμόζεται σε οποιαδήποτε απαίτηση **custom date parsing excel**, είτε ασχολείστε με οικονομικά τρίμηνα, αριθμούς ISO εβδομάδων ή ιδιόκτητες μορφές.

Έχετε διαφορετική εποχή ή ένα μεικτό‑ημερολόγιο φύλλο εργασίας; Απλώς αντικαταστήστε το `DateTimeParsing.JapaneseEra` με μια άλλη τιμή enum (π.χ., `DateTimeParsing.Custom`) και παρέχετε μια συμβολοσειρά μορφής. Η ευελιξία του Aspose.Cells σημαίνει ότι σπάνια χρειάζεται να γράψετε ξανά χειροκίνητο κώδικα μετατροπής.

**Επόμενα βήματα** που μπορείτε να εξερευνήσετε:

* **Load Excel with options** για αρχεία CSV (`CsvLoadOptions`) ώστε να διαχειρίζεστε διαχωριστές ειδικές για την τοπική ρύθμιση.
* Χρησιμοποιήστε `Workbook.Save` με `SaveFormat.Xxlsx` για εξαγωγή καθαρισμένων δεδομένων.
* Συνδυάστε αυτήν την προσέγγιση με **Aspose.Slides** ή **Aspose.Words** για αγωγούς αναφορών.

Δοκιμάστε το, προσαρμόστε τις επιλογές, και αφήστε τη βιβλιοθήκη να κάνει τη σκληρή δουλειά. Καλό κώδικα!  

![Στιγμιότυπο οθόνης με αναλυμένες ημερομηνίες ιαπωνικής εποχής σε παράθυρο κονσόλας – παράδειγμα parse japanese era dates](/images/parse-japanese-era-dates.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}