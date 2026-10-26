---
category: general
date: 2026-10-26
description: Μάθετε πώς να χρησιμοποιείτε το CultureInfo του ιαπωνικού ημερολογίου
  σε C# όταν αναλύετε ημερομηνίες εποχής και τις εισάγετε σε ένα φύλλο εργασίας Excel
  με το NPOI.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- use japanese calendar cultureinfo
- japanese era date parsing
- cultureinfo with japanese calendar
- datetime parse with cultureinfo
- npoi excel cultureinfo
language: el
lastmod: 2026-10-26
og_description: Χρησιμοποιήστε το CultureInfo του ιαπωνικού ημερολογίου σε C# για
  να αναλύσετε ημερομηνίες της περιόδου Reiwa και να τις γράψετε σε φύλλο εργασίας
  Excel. Πλήρης, εκτελέσιμος κώδικας με επεξηγήσεις.
og_image_alt: Screenshot of C# code parsing a Japanese era date and inserting it into
  an Excel cell
og_title: Χρήση του CultureInfo του ιαπωνικού ημερολογίου σε C# – πλήρες παράδειγμα
  Excel
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to use Japanese calendar CultureInfo in C# when parsing era
    dates and inserting them into an Excel worksheet with NPOI.
  headline: How to use Japanese calendar CultureInfo in C# to write dates to Excel
  type: TechArticle
tags:
- C#
- CultureInfo
- Excel
- NPOI
- Internationalization
title: Πώς να χρησιμοποιήσετε το CultureInfo του ιαπωνικού ημερολογίου σε C# για να
  γράψετε ημερομηνίες στο Excel
url: /el/net/excel-custom-number-date-formatting/how-to-use-japanese-calendar-cultureinfo-in-c-to-write-dates/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να χρησιμοποιήσετε το Japanese calendar CultureInfo σε C# για να γράψετε ημερομηνίες σε Excel

Αν χρειάζεστε **να χρησιμοποιήσετε το Japanese calendar CultureInfo** ενώ εργάζεστε με ημερομηνίες σε C#, αυτός ο οδηγός σας δείχνει ακριβώς πώς. Θα μάθετε να αναλύετε μια συμβολοσειρά ημερομηνίας που περιέχει ένα όνομα ιαπωνικής περιόδου (π.χ., *Reiwa 2/5/1*) και στη συνέχεια να γράψετε το προκύπτον `DateTime` στο πρώτο κελί ενός φύλλου εργασίας Excel χρησιμοποιώντας τη βιβλιοθήκη NPOI.

Η ανάλυση ημερομηνιών με βάση την εποχή χωρίς το σωστό `CultureInfo` οδηγεί σε `FormatException` ή σε λανθασμένες τιμές μήνα/ημέρας. Με τη ρύθμιση του `CultureInfo` στο Japanese calendar, εξασφαλίζετε ότι το .NET runtime ερμηνεύει σωστά την εποχή και ότι η τιμή που αποθηκεύετε στο Excel ταιριάζει με την αρχική ιαπωνική σημειογραφία.

Σε αυτό το tutorial θα:

* Δημιουργήσετε ένα αντικείμενο `CultureInfo` που χρησιμοποιεί το Japanese calendar.
* Αναλύσετε μια συμβολοσειρά ημερομηνίας με ιαπωνική εποχή χρησιμοποιώντας `DateTime.Parse`.
* Εισάγετε το αναλυμένο `DateTime` σε ένα κελί φύλλου εργασίας NPOI.
* Δείτε το πλήρες, εκτελέσιμο πρόγραμμα και το αναμενόμενο αποτέλεσμα.

> **Prerequisites** – .NET 6.0+ (ή .NET Core 3.1+), το **NPOI** πακέτο NuGet, και βασική κατανόηση του C# και της διαχείρισης αρχείων Excel.

---

## Τι θα χρειαστείτε

| Στοιχείο | Λόγος |
|------|--------|
| **.NET SDK** (6.0 ή νεότερο) | Παρέχει το runtime και τις βιβλιοθήκες για το `CultureInfo`. |
| **NPOI** (`NPOI` NuGet package) | Σας επιτρέπει να δημιουργείτε και να διαχειρίζεστε αρχεία Excel χωρίς εγκατεστημένο Office. |
| **Visual Studio Code**, **Visual Studio**, ή οποιοδήποτε IDE C# | Για τη μεταγλώττιση και εκτέλεση του δείγματος. |
| **Japanese era date string** (π.χ., `"Reiwa 2/5/1"`) | Δείχνει τη χρήση του Japanese calendar. |

## Βήμα 1: Εγκατάσταση του NPOI

Ανοίξτε ένα τερματικό στον φάκελο του έργου σας και εκτελέστε:

```bash
dotnet add package NPOI --version 2.6.1
```

Το πακέτο παρέχει τους τύπους `IWorkbook`, `ISheet` και `ICell` που χρησιμοποιούνται αργότερα.

## Βήμα 2: Δημιουργία ενός CultureInfo που χρησιμοποιεί το Japanese calendar

Το Japanese calendar είναι ένα ημερολόγιο βασισμένο σε εποχές. Πρέπει να ζητήσετε την παραλλαγή *Japanese* του τοπικού `ja-JP` και να ορίσετε ρητά το ημερολόγιο σε `JapaneseCalendar`.

```csharp
using System;
using System.Globalization;

// Create a CultureInfo based on Japanese locale and switch its calendar.
CultureInfo japaneseCulture = new CultureInfo("ja-JP");
japaneseCulture.DateTimeFormat.Calendar = new JapaneseCalendar();
```

> **Γιατί είναι σημαντικό** – Η προεπιλεγμένη τοπική ρύθμιση `ja-JP` χρησιμοποιεί το Γρηγοριανό ημερολόγιο. Η επαναανάθεση της ιδιότητας `Calendar` εξασφαλίζει ότι ονόματα εποχών όπως *Reiwa* αναγνωρίζονται κατά την ανάλυση.

## Βήμα 3: Ανάλυση μιας συμβολοσειράς ημερομηνίας με ιαπωνική εποχή

Τώρα που το `CultureInfo` είναι ρυθμισμένο, μπορείτε με ασφάλεια να αναλύσετε μια συμβολοσειρά που περιέχει όνομα εποχής.

```csharp
// Example Japanese era date: Reiwa 2 (2020) year, May 1st.
string eraDate = "Reiwa 2/5/1";

// Parse using the Japanese CultureInfo created earlier.
DateTime reiwaDate = DateTime.Parse(eraDate, japaneseCulture);
Console.WriteLine($"Parsed DateTime (UTC): {reiwaDate:u}");
```

**Έξοδος**

```
Parsed DateTime (UTC): 2020-05-01 00:00:00Z
```

Η μέθοδος `Parse` ερμηνεύει το *Reiwa 2* ως το Γρηγοριανό έτος 2020, μήνα 5, ημέρα 1.

### Περίπτωση άκρης: διαχείριση μη έγκυρων εποχών

Αν ένας χρήστης παρέχει μια μη υποστηριζόμενη εποχή (π.χ., `"Heisei 31/4/30"` μετά το τέλος της εποχής Heisei), το `DateTime.Parse` ρίχνει `FormatException`. Τυλίξτε την κλήση σε μπλοκ try‑catch για να παρέχετε ένα φιλικό μήνυμα σφάλματος:

```csharp
try
{
    DateTime parsed = DateTime.Parse(input, japaneseCulture);
}
catch (FormatException)
{
    Console.Error.WriteLine($"'{input}' is not a valid Japanese era date.");
}
```

## Βήμα 4: Εγγραφή του αναλυμένου DateTime σε ένα φύλλο εργασίας Excel

Με το αντικείμενο `DateTime` έτοιμο, μπορείτε να το αποθηκεύσετε σε ένα κελί Excel. Το NPOI μορφοποιεί αυτόματα τις τιμές `DateTime` ως ημερομηνίες Excel.

```csharp
using NPOI.SS.UserModel;
using NPOI.XSSF.UserModel;
using System.IO;

// Create a new workbook and a sheet.
IWorkbook workbook = new XSSFWorkbook();
ISheet sheet = workbook.CreateSheet("Japanese Dates");

// Write the DateTime into cell A1 (row 0, column 0).
IRow row = sheet.CreateRow(0);
ICell cell = row.CreateCell(0);
cell.SetCellValue(reiwaDate);

// Optionally apply a date style that shows the era (Excel does not have a built‑in era format,
// so we keep the Gregorian representation).
ICellStyle dateStyle = workbook.CreateCellStyle();
short dateFormatId = workbook.CreateDataFormat().GetFormat("yyyy-mm-dd");
dateStyle.DataFormat = dateFormatId;
cell.CellStyle = dateStyle;

// Save the workbook to a file.
using (FileStream fs = new FileStream("JapaneseEraDate.xlsx", FileMode.Create, FileAccess.Write))
{
    workbook.Write(fs);
}
Console.WriteLine("Excel file 'JapaneseEraDate.xlsx' created successfully.");
```

**Αποτέλεσμα** – Ανοίγοντας το *JapaneseEraDate.xlsx* εμφανίζεται η ημερομηνία **2020‑05‑01** στο κελί A1.

### Γιατί να χρησιμοποιήσετε το NPOI;

*Works on any platform* (Windows, Linux, macOS) and does **not** require Microsoft Office. This makes the solution suitable for CI pipelines, Docker containers, or server‑side processing.

## Βήμα 5: Πλήρες, εκτελέσιμο πρόγραμμα

Συνδυάζοντας όλα τα παραπάνω, εδώ είναι μια πλήρης εφαρμογή κονσόλας που δείχνει όλη τη ροή:

```csharp
// File: Program.cs
using System;
using System.Globalization;
using System.IO;
using NPOI.SS.UserModel;
using NPOI.XSSF.UserModel;

class Program
{
    static void Main()
    {
        // 1️⃣ Configure CultureInfo for the Japanese calendar.
        CultureInfo japaneseCulture = new CultureInfo("ja-JP");
        japaneseCulture.DateTimeFormat.Calendar = new JapaneseCalendar();

        // 2️⃣ Parse a Japanese era date string.
        string eraDate = "Reiwa 2/5/1";
        DateTime reiwaDate;
        try
        {
            reiwaDate = DateTime.Parse(eraDate, japaneseCulture);
            Console.WriteLine($"Parsed DateTime: {reiwaDate:u}");
        }
        catch (FormatException)
        {
            Console.Error.WriteLine($"'{eraDate}' is not a valid Japanese era date.");
            return;
        }

        // 3️⃣ Create an Excel workbook and write the date.
        IWorkbook workbook = new XSSFWorkbook();
        ISheet sheet = workbook.CreateSheet("Japanese Dates");
        IRow row = sheet.CreateRow(0);
        ICell cell = row.CreateCell(0);
        cell.SetCellValue(reiwaDate);

        // Apply a simple Gregorian date format.
        ICellStyle style = workbook.CreateCellStyle();
        short fmt = workbook.CreateDataFormat().GetFormat("yyyy-mm-dd");
        style.DataFormat = fmt;
        cell.CellStyle = style;

        // 4️⃣ Save the workbook.
        const string fileName = "JapaneseEraDate.xlsx";
        using (FileStream fs = new FileStream(fileName, FileMode.Create, FileAccess.Write))
        {
            workbook.Write(fs);
        }

        Console.WriteLine($"Excel file '{fileName}' created successfully.");
    }
}
```

**How to run**

```bash
dotnet run
```

Μετά την εκτέλεση, θα βρείτε το `JapaneseEraDate.xlsx` στον φάκελο του έργου με τη σωστά αναλυμένη ημερομηνία.

## Συνηθισμένα προβλήματα και συμβουλές βέλτιστων πρακτικών

| Πρόβλημα | Διόρθωση / Σύσταση |
|---------|----------------------|
| Ξεχάνοντας να ορίσετε `japaneseCulture.DateTimeFormat.Calendar` | Πάντα να εκχωρείτε μια παρουσία `JapaneseCalendar`; διαφορετικά το όνομα της εποχής δεν αναγνωρίζεται. |
| Χρήση `DateTime.TryParse` χωρίς το προσαρμοσμένο `CultureInfo` | Περνάτε το ίδιο `japaneseCulture` στο `TryParse` για να διατηρήσετε τη συνέπεια της συμπεριφοράς. |
| Αναμονή το Excel να εμφανίσει το όνομα της εποχής | Οι ενσωματωμένες μορφές ημερομηνίας του Excel είναι μόνο Γρηγοριανές. Αν χρειάζεστε την εποχή, αποθηκεύστε την αρχική συμβολοσειρά σε ξεχωριστή στήλη ή δημιουργήστε προσαρμοσμένη μορφή κειμένου. |
| Μη απελευθέρωση του `FileStream` | Χρησιμοποιήστε ένα μπλοκ `using` (όπως φαίνεται) για να διασφαλίσετε ότι το αρχείο κλείνει άμεσα. |
| Ανάμειξη αντικειμένων `CultureInfo` μεταξύ νημάτων | Το `CultureInfo` είναι ασφαλές για ανάγνωση μεταξύ νημάτων, αλλά αποφύγετε την τροποποίηση της ιδιότητας `Calendar` μετά την αρχική ρύθμιση. |

## Συμπέρασμα

Τώρα ξέρετε πώς να **χρησιμοποιήσετε το Japanese calendar CultureInfo** σε C# για να αναλύετε με ακρίβεια ημερομηνίες με ιαπωνική εποχή και να γράφετε το προκύπτον `DateTime` σε ένα φύλλο εργασίας Excel με το NPOI. Το πλήρες παράδειγμα καλύπτει τη διαμόρφωση, την ανάλυση, τη διαχείριση σφαλμάτων και την έξοδο σε Excel, παρέχοντάς σας μια σταθερή βάση για οποιοδήποτε διεθνές σενάριο αναφοράς ή ανταλλαγής δεδομένων.

Στη συνέχεια, μπορείτε να εξερευνήσετε:

* **Μορφοποίηση ημερομηνιών με προσαρμοσμένο κείμενο** για να διατηρήσετε το όνομα της εποχής μέσα στο Excel.
* **Ανάγνωση ημερομηνιών από Excel** χρησιμοποιώντας `cell.DateCellValue` ενώ σέβεστε το Japanese calendar.
* **Εφαρμογή της ίδιας τεχνικής** για άλλα ημερολόγια βασισμένα σε εποχές (π.χ., Thai Buddhist calendar) αντικαθιστώντας το `JapaneseCalendar` με το κατάλληλο υποκλάδο `Calendar`.

Μη διστάσετε να πειραματιστείτε με διαφορετικές συμβολοσειρές εποχών, μεγαλύτερα σύνολα δεδομένων ή να ενσωματώσετε αυτή τη λογική σε ASP.NET Core APIs που δημιουργούν αναφορές Excel σε πραγματικό χρόνο. Καλή προγραμματιστική διασκέδαση!

## Τι πρέπει να μάθετε στη συνέχεια;

Οι παρακάτω οδηγίες καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικά παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Δημιουργία Excel Workbook με ημερομηνίες Japanese Calendar – Πλήρης Οδηγός](/cells/english/net/excel-custom-number-date-formatting/create-excel-workbook-with-japanese-calendar-dates-full-guid/)
- [Ανάλυση Japanese Era Dates σε Excel – Πλήρης Οδηγός για Προγραμματιστές C#](/cells/english/net/data-loading-and-parsing/parse-japanese-era-dates-in-excel-full-guide-for-c-developer/)
- [Πώς να δημιουργήσετε Excel workbook και να αναλύσετε Japanese dates σε C#](/cells/english/net/excel-custom-number-date-formatting/how-to-create-excel-workbook-and-parse-japanese-dates-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}