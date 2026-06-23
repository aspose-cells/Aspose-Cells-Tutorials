---
category: general
date: 2026-06-08
description: Αναλύστε ημερομηνία ιαπωνικής εποχής σε C# χρησιμοποιώντας το Aspose.Cells.
  Μάθετε πώς το CultureInfo ja-JP και η μορφή ιαπωνικής εποχής επιτρέπουν ακριβή μετατροπή
  ημερομηνιών στο Excel.
draft: false
keywords:
- parse japanese era date
- Aspose.Cells
- CultureInfo ja-JP
- Japanese era format
- Excel date conversion
- C# DateTime parsing
language: el
og_description: Αναλύστε γρήγορα ημερομηνίες ιαπωνικής εποχής σε C#. Αυτό το σεμινάριο
  δείχνει πώς το CultureInfo ja-JP και το Aspose.Cells μετατρέπουν τις συμβολοσειρές
  εποχής σε σωστά αντικείμενα DateTime.
og_title: Ανάλυση ημερομηνίας ιαπωνικής εποχής σε C# – Οδηγός Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Parse Japanese era date in C# using Aspose.Cells. Learn how CultureInfo
    ja-JP and Japanese era format enable accurate Excel date conversion.
  headline: Parse Japanese Era Date in C# with Aspose.Cells – Full Guide
  type: TechArticle
- description: Parse Japanese era date in C# using Aspose.Cells. Learn how CultureInfo
    ja-JP and Japanese era format enable accurate Excel date conversion.
  name: Parse Japanese Era Date in C# with Aspose.Cells – Full Guide
  steps:
  - name: 5.1 Invalid or Empty Strings
    text: '```csharp string maybeDate = workbook.Worksheets[0].Cells["B1"].GetString();
      // could be empty if (string.IsNullOrWhiteSpace(maybeDate)) { Console.WriteLine("Cell
      B1 is empty – skipping."); } else { // Attempt to parse; catch format exceptions
      try { DateTime dt = DateTime.Parse(maybeDate, new Cultur'
  - name: 5.2 Older Eras (Showa, Taisho)
    text: 'The same `CultureInfo ja-JP` works for older eras automatically:'
  - name: 5.3 Using `DateTime.ParseExact` for Strict Validation
    text: 'If you want to enforce the exact Japanese era pattern, use a custom format
      string:'
  type: HowTo
- questions:
  - answer: Yes. As long as the workbook’s `Settings.CultureInfo` is set to `ja-JP`
      *before* you call `GetDateTime()`, Aspose.Cells will interpret the existing
      strings correctly.
    question: Does this work with .xlsx files that already contain era dates?
  - answer: The parsing returns a `DateTime` with `Kind = Unspecified`. If you need
      UTC or local time, apply `DateTime.SpecifyKind` or convert after parsing.
    question: What about time zones?
  - answer: Absolutely. Loop through the desired range and call `GetDateTime()` on
      each cell—just remember to handle exceptions for malformed entries.
    question: Can I parse multiple cells at once?
  type: FAQPage
tags:
- C#
- Excel
- DateTime
- Localization
title: Ανάλυση ημερομηνίας ιαπωνικής εποχής σε C# με το Aspose.Cells – Πλήρης οδηγός
url: /el/net/excel-custom-number-date-formatting/parse-japanese-era-date-in-c-with-aspose-cells-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ανάλυση ημερομηνίας ιαπωνικής εποχής σε C# με Aspose.Cells – Πλήρης Οδηγός

Ποτέ χρειάστηκε να **αναλύσετε ημερομηνίες ιαπωνικής εποχής** απευθείας από ένα φύλλο Excel; Ίσως εξάγετε δεδομένα από ένα παλαιό σύστημα που εξακολουθεί να χρησιμοποιεί «令和3年5月12日» και θέλετε ένα καθαρό `DateTime` για να τρέξετε αναφορές. Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από ένα πλήρες, έτοιμο‑για‑εκτέλεση παράδειγμα που μετατρέπει αυτές τις συμβολοσειρές σε σωστές ημερομηνίες C# — χωρίς εικασίες.

Θα χρησιμοποιήσουμε **Aspose.Cells**, τη δυνατή βιβλιοθήκη .NET για διαχείριση Excel, μαζί με τη ρύθμιση **CultureInfo ja-JP** που γνωρίζει πώς να διαβάζει τις ιαπωνικές εποχές. Στο τέλος θα έχετε ένα επαναχρησιμοποιήσιμο snippet που διαχειρίζεται «令和», «平成», και ακόμη παλαιότερες εποχές χωρίς προβλήματα.

## Προαπαιτούμενα

- .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί επίσης σε .NET Framework 4.6+)  
- Aspose.Cells for .NET (μπορείτε να κατεβάσετε το δωρεάν trial πακέτο NuGet: `Install-Package Aspose.Cells`)  
- Βασική εξοικείωση με C# — τίποτα περίπλοκο, ένα console app αρκεί  
- Ένα IDE της επιλογής σας (Visual Studio, Rider, VS Code, κ.λπ.)

Αυτό είναι όλο. Χωρίς επιπλέον υπηρεσίες, χωρίς σπάνιους τρίτους parser.

## Βήμα 1: Ρύθμιση του έργου και προσθήκη Aspose.Cells

Πρώτα, δημιουργήστε ένα νέο console project:

```bash
dotnet new console -n JapaneseEraParser
cd JapaneseEraParser
dotnet add package Aspose.Cells
```

Τώρα ανοίξτε το **Program.cs** και προσθέστε τα απαιτούμενα namespaces:

```csharp
using System;
using System.Globalization;
using Aspose.Cells;
```

> **Pro tip:** Αν χρησιμοποιείτε Visual Studio, το IDE θα προτείνει αυτόματα την προσθήκη των `using` δηλώσεων μετά την πληκτρολόγηση των ονομάτων των κλάσεων.

## Βήμα 2: Δημιουργία Workbook και εφαρμογή Ιαπωνικού πολιτισμού

Το κλειδί για **parse japanese era date** σωστά είναι να πείτε στο Aspose.Cells ποιον πολιτισμό να χρησιμοποιήσει. Ορίζοντας το `CultureInfo` σε `ja-JP` ενεργοποιείται η ανάλυση με γνώση εποχών.

```csharp
// Step 2: Initialize a new workbook and set Japanese culture
Workbook workbook = new Workbook();
workbook.Settings.CultureInfo = new CultureInfo("ja-JP");
```

Γιατί είναι σημαντικό; Το ιαπωνικό ημερολόγιο έχει πολλές εποχές (π.χ., *Reiwa* (令和), *Heisei* (平成)). Το αντικείμενο `CultureInfo` περιέχει ένα `JapaneseCalendar` που γνωρίζει τις ημερομηνίες έναρξης κάθε εποχής, ώστε οποιαδήποτε συμβολοσειρά ακολουθεί τη μορφή ιαπωνικής εποχής να μπορεί να ερμηνευθεί σωστά.

## Βήμα 3: Εγγραφή συμβολοσειράς ημερομηνίας ιαπωνικής εποχής σε κελί

Ας βάλουμε ένα δείγμα ημερομηνίας εποχής στο κελί **A1**. Αλλάξτε τη συμβολοσειρά ελεύθερα για να δοκιμάσετε διαφορετικές εποχές.

```csharp
// Step 3: Put a Japanese era date string into A1
string japaneseDate = "令和3年5月12日"; // Reiwa 3, May 12, 2021
workbook.Worksheets[0].Cells["A1"].PutValue(japaneseDate);
```

Αν προτιμάτε να δουλέψετε με υπάρχον workbook, μπορείτε να το φορτώσετε με `new Workbook("path/to/file.xlsx")` και να παραλείψετε το βήμα δημιουργίας.

## Βήμα 4: Ανάκτηση της τιμής ως αντικείμενο C# DateTime

Τώρα συμβαίνει η μαγεία. Καλώντας το `GetDateTime()`, το Aspose.Cells διαβάζει το κελί χρησιμοποιώντας το προηγουμένως ορισμένο `CultureInfo` και επιστρέφει ένα σωστό `DateTime`.

```csharp
// Step 4: Parse the cell value into a DateTime
DateTime parsedDate = workbook.Worksheets[0].Cells["A1"].GetDateTime();
Console.WriteLine($"Parsed DateTime: {parsedDate:yyyy-MM-dd}");
```

**Αναμενόμενη έξοδος**

```
Parsed DateTime: 2021-05-12
```

Αυτή είναι η πλήρης ροή **parse japanese era date** — τέσσερις σύντομες γραμμές κώδικα.

## Βήμα 5: Διαχείριση περιπτώσεων άκρων και εναλλακτικών εποχών

Τα πραγματικά δεδομένα δεν είναι πάντα καθαρά. Εδώ είναι μερικά σενάρια που μπορεί να συναντήσετε και πώς να τα αντιμετωπίσετε.

### 5.1 Μη έγκυρες ή κενές συμβολοσειρές

```csharp
string maybeDate = workbook.Worksheets[0].Cells["B1"].GetString(); // could be empty
if (string.IsNullOrWhiteSpace(maybeDate))
{
    Console.WriteLine("Cell B1 is empty – skipping.");
}
else
{
    // Attempt to parse; catch format exceptions
    try
    {
        DateTime dt = DateTime.Parse(maybeDate, new CultureInfo("ja-JP"));
        Console.WriteLine($"B1 parsed as {dt:yyyy-MM-dd}");
    }
    catch (FormatException)
    {
        Console.WriteLine($"Unable to parse '{maybeDate}' as a Japanese era date.");
    }
}
```

### 5.2 Παλαιότερες εποχές (Showa, Taisho)

Το ίδιο `CultureInfo ja-JP` λειτουργεί αυτόματα και για παλαιότερες εποχές:

```csharp
string showaDate = "昭和45年12月31日"; // Showa 45 = 1970-12-31
DateTime showaParsed = DateTime.Parse(showaDate, new CultureInfo("ja-JP"));
Console.WriteLine(showaParsed.ToString("yyyy-MM-dd")); // 1970-12-31
```

### 5.3 Χρήση `DateTime.ParseExact` για αυστηρή επικύρωση

Αν θέλετε να επιβάλλετε το ακριβές μοτίβο ιαπωνικής εποχής, χρησιμοποιήστε μια προσαρμοσμένη μορφή:

```csharp
string pattern = "ggggy年M月d日"; // gggg = era name, y = year in era
DateTime strictDate = DateTime.ParseExact(japaneseDate, pattern, new CultureInfo("ja-JP"));
Console.WriteLine(strictDate); // 2021-05-12 00:00:00
```

Αυτή η προσέγγιση ρίχνει `FormatException` όταν η συμβολοσειρά αποκλίνει, κάτι που μπορεί να είναι χρήσιμο για ελέγχους ποιότητας δεδομένων.

## Πλήρες λειτουργικό παράδειγμα

Παρακάτω είναι το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε‑και‑επικολλήσετε στο **Program.cs** και να τρέξετε.

```csharp
using System;
using System.Globalization;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook and set Japanese culture
        Workbook workbook = new Workbook();
        workbook.Settings.CultureInfo = new CultureInfo("ja-JP");

        // 2️⃣ Insert a Japanese era date string
        string japaneseDate = "令和3年5月12日";
        workbook.Worksheets[0].Cells["A1"].PutValue(japaneseDate);

        // 3️⃣ Parse the cell value into DateTime
        DateTime parsedDate = workbook.Worksheets[0].Cells["A1"].GetDateTime();
        Console.WriteLine($"Parsed DateTime: {parsedDate:yyyy-MM-dd}");

        // 4️⃣ Demonstrate handling an older era
        string showaDate = "昭和45年12月31日";
        DateTime showaParsed = DateTime.Parse(showaDate, new CultureInfo("ja-JP"));
        Console.WriteLine($"Showa parsed: {showaParsed:yyyy-MM-dd}");

        // 5️⃣ Strict parsing with ParseExact
        string pattern = "gggy年M月d日";
        try
        {
            DateTime strict = DateTime.ParseExact(japaneseDate, pattern, new CultureInfo("ja-JP"));
            Console.WriteLine($"Strict parse: {strict:yyyy-MM-dd}");
        }
        catch (FormatException ex)
        {
            Console.WriteLine($"Strict parse failed: {ex.Message}");
        }
    }
}
```

Τρέξτε το με `dotnet run` και θα δείτε:

```
Parsed DateTime: 2021-05-12
Showa parsed: 1970-12-31
Strict parse: 2021-05-12
```

Boom—**parse japanese era date** ολοκληρώθηκε, και έχετε ένα πρότυπο για οποιαδήποτε εποχή μπορεί να συναντήσετε.

![Parse Japanese Era Date workflow – shows workbook creation, culture setting, cell write, and GetDateTime call](parse-japanese-era-date.png "Diagram illustrating how to parse japanese era date using Aspose.Cells and CultureInfo ja-JP")

## Συχνές ερωτήσεις

- **Λειτουργεί αυτό με αρχεία .xlsx που ήδη περιέχουν ημερομηνίες εποχής;**  
  Ναι. Όσο το `Settings.CultureInfo` του workbook είναι ορισμένο σε `ja-JP` *πριν* καλέσετε το `GetDateTime()`, το Aspose.Cells θα ερμηνεύσει σωστά τις υπάρχουσες συμβολοσειρές.

- **Τι γίνεται με τις ζώνες ώρας;**  
  Η ανάλυση επιστρέφει ένα `DateTime` με `Kind = Unspecified`. Αν χρειάζεστε UTC ή τοπική ώρα, εφαρμόστε `DateTime.SpecifyKind` ή μετατρέψτε μετά την ανάλυση.

- **Μπορώ να αναλύσω πολλαπλά κελιά ταυτόχρονα;**  
  Απόλυτα. Κάντε βρόχο στην επιθυμητή περιοχή και καλέστε `GetDateTime()` σε κάθε κελί — απλώς θυμηθείτε να διαχειριστείτε εξαιρέσεις για κακοδιατυπωμένες καταχωρήσεις.

## Συμπέρασμα

Καλύψαμε όλα όσα χρειάζεστε για να **parse japanese era date** σε C# χρησιμοποιώντας Aspose.Cells και το ενσωματωμένο `CultureInfo ja-JP`. Από τη ρύθμιση του workbook, την εγγραφή συμβολοσειρών εποχής, την ανάκτηση ενός καθαρού `DateTime`, μέχρι τη διαχείριση περιπτώσεων άκρων όπως παλαιότερες εποχές και αυστηρή επικύρωση — αυτός ο οδηγός σας παρέχει μια λύση έτοιμη για παραγωγή.

Στη συνέχεια, μπορείτε να εξερευνήσετε **Excel date conversion** για αριθμητικές σειριακές ημερομηνίες, ή να εμβαθύνετε στο **C# DateTime parsing** με προσαρμοσμένα ημερολόγια για άλλες τοπικές ρυθμίσεις. Το ίδιο μοτίβο λειτουργεί για το Ταϊλανδικό Βουδιστικό ημερολόγιο, το Εβραϊκό ημερολόγιο, και άλλα — απλώς αλλάξτε το `CultureInfo`.

Έχετε κάποιο πρόβλημα που σας ενοχλεί; Αφήστε ένα σχόλιο και ας το λύσουμε μαζί. Καλή κωδικοποίηση!

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στην δική σας υλοποίηση.

- [How to Implement Date Validation in .NET Using Aspose.Cells: A Comprehensive Guide](/cells/english/net/data-validation/implement-date-validation-net-aspose-cells/)
- [Change Excel Date System to 1904 using Aspose.Cells .NET](/cells/english/net/calculation-engine/change-excel-date-system-aspose-cells-net/)
- [Efficiently Convert Excel to PDF with Custom Date Formats Using Aspose.Cells for Java](/cells/english/java/workbook-operations/render-excel-custom-date-formats-pdf-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}