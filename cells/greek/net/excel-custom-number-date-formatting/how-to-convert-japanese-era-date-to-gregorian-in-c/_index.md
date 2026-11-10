---
category: general
date: 2026-10-01
description: Μετατρέψτε ημερομηνία ιαπωνικής εποχής σε ημερομηνία Gregorian DateTime
  χρησιμοποιώντας το Aspose.Cells σε C#. Μάθετε πώς να μετατρέπετε γρήγορα το ιαπωνικό
  ημερολόγιο.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert japanese era date
- how to convert japanese calendar
language: el
lastmod: 2026-10-01
og_description: Μετατρέψτε ημερομηνία ιαπωνικής εποχής σε Γρηγοριανή DateTime σε C#.
  Αυτό το σεμινάριο εξηγεί πώς να μετατρέψετε το ιαπωνικό ημερολόγιο με ακρίβεια χρησιμοποιώντας
  το Aspose.Cells.
og_image_alt: Code example converting a Japanese era date string to a Gregorian DateTime
  in a C# console app
og_title: Μετατροπή ημερομηνίας ιαπωνικής εποχής σε Γρηγοριανή σε C# – βήμα‑βήμα οδηγός
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: convert japanese era date to a Gregorian DateTime using Aspose.Cells
    in C#. Learn how to convert japanese calendar quickly.
  headline: How to convert Japanese era date to Gregorian in C#
  type: TechArticle
- description: convert japanese era date to a Gregorian DateTime using Aspose.Cells
    in C#. Learn how to convert japanese calendar quickly.
  name: How to convert Japanese era date to Gregorian in C#
  steps:
  - name: Why each step matters
    text: '| Step | Purpose | How it helps the conversion | |------|---------|-----------------------------|
      | **Create workbook** | Provides a container that understands Excel formulas
      and date systems. | The library’s internal date engine is activated only inside
      a workbook. | | **Insert era string** | Suppl'
  - name: Handling invalid or ambiguous strings
    text: '* **Invalid era name** – Aspose.Cells throws a `FormatException`. Wrap
      the conversion in `try/catch` to provide a friendly error message. * **Missing
      year/month/day** – The library expects a full “Era Year/Month/Day” pattern.
      If you receive partial data, prepend missing parts or reject the input ear'
  - name: Next steps
    text: '* Explore **formatting options** to write the Gregorian date back into
      the worksheet with a custom number format. * Combine this conversion with **data
      import pipelines** (e.g., reading CSV files that contain era dates). * Review
      other Aspose.Cells features such as **date arithmetic** and **regional'
  type: HowTo
tags:
- Aspose.Cells
- C#
- date conversion
title: Πώς να μετατρέψετε ημερομηνία ιαπωνικής εποχής σε Γρηγοριανή στο C#
url: /el/net/excel-custom-number-date-formatting/how-to-convert-japanese-era-date-to-gregorian-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να μετατρέψετε ημερομηνία ιαπωνικής εποχής σε Γρηγοριανή σε C#

Αν χρειάζεστε να **convert Japanese era date** strings σε Γρηγοριανές ημερομηνίες σε C#, αυτός ο οδηγός σας δείχνει ακριβώς πώς. Είτε επεξεργάζεστε παλαιά δεδομένα, διαβάζετε είσοδο χρήστη ή δημιουργείτε αναφορές, η βιβλιοθήκη Aspose.Cells κάνει τη μετατροπή απλή. Επιπλέον, θα ανακαλύψετε τον καλύτερο τρόπο για **how to convert Japanese calendar** τιμές όταν εργάζεστε με λογιστικά φύλλα.

Ο οδηγός καλύπτει κάθε βήμα—από τη δημιουργία ενός βιβλίου εργασίας μέχρι την ανάκτηση μιας τιμής `DateTime`—ώστε να μπορείτε να αντιγράψετε‑και‑επικολλήσετε ένα πλήρες, εκτελέσιμο πρόγραμμα. Δεν απαιτείται εξωτερική τεκμηρίωση· ακολουθήστε απλώς τον κώδικα και τις εξηγήσεις παρακάτω.

## Προαπαιτούμενα

* .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί επίσης με .NET Framework 4.6+)
* Άδεια για **Aspose.Cells** (η δωρεάν δοκιμή λειτουργεί για δοκιμές)
* Περιβάλλον ανάπτυξης όπως Visual Studio 2022 ή VS Code
* Βασική εξοικείωση με εφαρμογές κονσόλας C#

## Μετατροπή ημερομηνίας ιαπωνικής εποχής με Aspose.Cells

Ο πυρήνας της μετατροπής βρίσκεται σε μερικές απλές κλήσεις API. Η Aspose.Cells ερμηνεύει αυτόματα τις συμβολοσειρές ιαπωνικής εποχής (π.χ., “Reiwa 2/04/01”) και εκθέτει το αποτέλεσμα ως αντικείμενο `DateTime` μόλις επανυπολογιστεί το φύλλο εργασίας.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        var workbook = new Workbook();                // creates an empty Excel file in memory
        var worksheet = workbook.Worksheets[0];       // the default sheet is at index 0

        // Step 2: Insert a Japanese era date string into cell A1
        // The string follows the Japanese calendar format: Era Year/Month/Day
        worksheet.Cells[0, 0].PutValue("Reiwa 2/04/01");

        // Step 3: Apply a default style to the cell (required for proper calculation)
        // Without a style, Aspose.Cells may treat the content as plain text and skip conversion.
        worksheet.Cells[0, 0].SetStyle(workbook.CreateStyle());

        // Step 4: Recalculate the worksheet so the date string is converted to a Gregorian date
        // The Calculate method parses the era string and updates the cell's internal value.
        worksheet.Calculate();

        // Step 5: Retrieve and display the converted DateTime value (2020‑04‑01)
        DateTime gregorian = worksheet.Cells[0, 0].DateTimeValue;
        Console.WriteLine($"Gregorian date: {gregorian:yyyy-MM-dd}");
    }
}
```

### Γιατί κάθε βήμα έχει σημασία

| Βήμα | Σκοπός | Πώς βοηθά τη μετατροπή |
|------|--------|------------------------|
| **Create workbook** | Παρέχει ένα δοχείο που κατανοεί τύπους Excel και συστήματα ημερομηνιών. | Η εσωτερική μηχανή ημερομηνιών της βιβλιοθήκης ενεργοποιείται μόνο μέσα σε ένα βιβλίο εργασίας. |
| **Insert era string** | Παρέχει το ακατέργαστο κείμενο του ιαπωνικού ημερολογίου που θέλετε να μεταφράσετε. | Η Aspose.Cells αναγνωρίζει ονόματα εποχών όπως *Reiwa*, *Heisei*, *Showa* κ.λπ. |
| **Set style** | Αναγκάζει το κελί να αντιμετωπιστεί ως κελί τιμής αντί για κυριολεκτική συμβολοσειρά. | Χωρίς στυλ, η μέθοδος `Calculate` μπορεί να αγνοήσει το κελί, αφήνοντας το κείμενο αμετάβλητο. |
| **Calculate** | Εκκινεί την ανάλυση της συμβολοσειράς εποχής και τη μετατροπή σε εσωτερικό σειριακό αριθμό ημερομηνίας. | Η βιβλιοθήκη μετατρέπει “Reiwa 2/04/01” → σειριακός αριθμός → Γρηγοριανή `DateTime`. |
| **Read `DateTimeValue`** | Επιστρέφει το μετατρεπόμενο αντικείμενο .NET `DateTime`. | Τώρα έχετε ένα τυπικό `DateTime` που μπορείτε να χρησιμοποιήσετε σε οποιοδήποτε API .NET. |

## Πώς να μετατρέψετε ιαπωνικό ημερολόγιο σε άλλες περιπτώσεις

Η ίδια προσέγγιση λειτουργεί για οποιοδήποτε όνομα ιαπωνικής εποχής υποστηρίζεται από την Aspose.Cells:

```csharp
// Example: converting a Heisei era date
worksheet.Cells[0, 0].PutValue("Heisei 30/12/31"); // corresponds to 2018‑12‑31
worksheet.Calculate();
Console.WriteLine(worksheet.Cells[0, 0].DateTimeValue); // 2018-12-31
```

### Διαχείριση μη έγκυρων ή ασαφών συμβολοσειρών

* **Invalid era name** – Η Aspose.Cells ρίχνει ένα `FormatException`. Τυλίξτε τη μετατροπή σε `try/catch` για να παρέχετε ένα φιλικό μήνυμα σφάλματος.
* **Missing year/month/day** – Η βιβλιοθήκη αναμένει ένα πλήρες μοτίβο “Era Year/Month/Day”. Αν λάβετε μερικά δεδομένα, προσθέστε τα ελλιπή μέρη ή απορρίψτε την είσοδο νωρίς.
* **Different locale settings** – Η μετατροπή **δεν** εξαρτάται από την τρέχουσα πολιτισμική ρύθμιση του νήματος· χρησιμοποιεί πάντα τον χάρτη ιαπωνικών εποχών που είναι ενσωματωμένος στην Aspose.Cells. Αυτό κάνει τη μέθοδο ασφαλή για επεξεργασία στο διακομιστή.

```csharp
try
{
    worksheet.Cells[0, 0].PutValue(userInput);
    worksheet.Calculate();
    DateTime result = worksheet.Cells[0, 0].DateTimeValue;
    // Use result...
}
catch (FormatException ex)
{
    Console.WriteLine($"Unable to parse Japanese era date: {ex.Message}");
}
```

## Πρακτικές συμβουλές και κοινά προβλήματα

* **Always call `SetStyle`** πριν από το `Calculate`. Η παράλειψη αυτού του βήματος είναι συχνή πηγή σφαλμάτων επειδή το κελί παραμένει απλός κάτοχος κειμένου.
* **Reuse the same workbook** αν χρειάζεται να μετατρέψετε πολλές ημερομηνίες. Η δημιουργία νέου βιβλίου εργασίας για κάθε μετατροπή προσθέτει περιττό κόστος.
* **Batch conversion** – Συμπληρώστε μια στήλη με συμβολοσειρές εποχής, καλέστε `worksheet.Calculate()` μία φορά, έπειτα διαβάστε ολόκληρη τη στήλη των `DateTimeValue`. Αυτό είναι πολύ πιο αποδοτικό από τον επανυπολογισμό ανά κελί.
* **Version compatibility** – Η λογική μετατροπής εποχής εισήχθη στην Aspose.Cells 22.9. Βεβαιωθείτε ότι χρησιμοποιείτε αυτήν την έκδοση ή νεότερη· παλαιότερες εκδόσεις αντιμετωπίζουν τη συμβολοσειρά ως απλό κείμενο.

## Πλήρες λειτουργικό παράδειγμα (εφαρμογή κονσόλας)

Παρακάτω υπάρχει ένα αυτόνομο πρόγραμμα που μπορείτε να μεταγλωττίσετε και να εκτελέσετε αμέσως. Δείχνει τόσο τη μετατροπή Reiwa όσο και Heisei, διαχειριζόμενο τα σφάλματα με χάρη.

```csharp
using System;
using Aspose.Cells;

class JapaneseEraConverter
{
    static void Main()
    {
        // Initialize workbook once
        var workbook = new Workbook();
        var sheet = workbook.Worksheets[0];
        var style = workbook.CreateStyle();
        sheet.Cells[0, 0].SetStyle(style);
        sheet.Cells[1, 0].SetStyle(style);

        // Sample inputs
        string[] eraDates = { "Reiwa 2/04/01", "Heisei 30/12/31", "InvalidEra 1/01/01" };

        for (int i = 0; i < eraDates.Length; i++)
        {
            sheet.Cells[i, 0].PutValue(eraDates[i]);
        }

        // Perform conversion for all populated cells
        sheet.Calculate();

        // Output results
        for (int i = 0; i < eraDates.Length; i++)
        {
            try
            {
                DateTime dt = sheet.Cells[i, 0].DateTimeValue;
                Console.WriteLine($"{eraDates[i]} → {dt:yyyy-MM-dd}");
            }
            catch (Exception)
            {
                Console.WriteLine($"{eraDates[i]} → conversion failed");
            }
        }
    }
}
```

**Αναμενόμενη έξοδος κονσόλας**

```
Reiwa 2/04/01 → 2020-04-01
Heisei 30/12/31 → 2018-12-31
InvalidEra 1/01/01 → conversion failed
```

Η εκτέλεση αυτού του προγράμματος επιβεβαιώνει ότι η βιβλιοθήκη σωστά **convert japanese era date** strings και αναφέρει με χάρη τις μη υποστηριζόμενες τιμές.

## Συμπέρασμα

Τώρα γνωρίζετε πώς να **convert Japanese era date** strings σε τυπικά Γρηγοριανά αντικείμενα `DateTime` χρησιμοποιώντας την Aspose.Cells σε C#. Η διαδικασία περιορίζεται στην εισαγωγή του κειμένου εποχής, την εφαρμογή στυλ, τον επανυπολογισμό του φύλλου εργασίας και την ανάγνωση του `DateTimeValue`. Ακολουθώντας τα παραπάνω βήματα μπορείτε επίσης να απαντήσετε στην ευρύτερη ερώτηση του **how to convert Japanese calendar** δεδομένων μαζικά, να διαχειριστείτε σφάλματα και να βελτιστοποιήσετε την απόδοση.

### Επόμενα βήματα

* Εξερευνήστε **formatting options** για να γράψετε την Γρηγοριανή ημερομηνία πίσω στο φύλλο εργασίας με προσαρμοσμένη μορφή αριθμού.
* Συνδυάστε αυτήν τη μετατροπή με **data import pipelines** (π.χ., ανάγνωση αρχείων CSV που περιέχουν ημερομηνίες εποχής).
* Εξετάστε άλλες δυνατότητες της Aspose.Cells όπως **date arithmetic** και **regional settings** για πιο σύνθετα σενάρια ημερολογίου.

Καλή προγραμματιστική, και μη διστάσετε να προσαρμόσετε το παράδειγμα στα δικά σας ροές επεξεργασίας δεδομένων!

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικά παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε επιπλέον δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Ανάλυση ημερομηνίας ιαπωνικής εποχής σε C# με Aspose.Cells – Πλήρης Οδηγός](/cells/english/net/excel-custom-number-date-formatting/parse-japanese-era-date-in-c-with-aspose-cells-full-guide/)
- [Ενεργοποίηση ανάλυσης ιαπωνικής εποχής σε C# με Aspose.Cells](/cells/english/net/workbook-settings/enable-japanese-era-parsing-in-c-with-aspose-cells/)
- [Πώς να δημιουργήσετε βιβλίο εργασίας και να μετατρέψετε συμβολοσειρά σε ημερομηνία σε C#](/cells/english/net/excel-custom-number-date-formatting/how-to-create-workbook-and-convert-string-to-date-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}