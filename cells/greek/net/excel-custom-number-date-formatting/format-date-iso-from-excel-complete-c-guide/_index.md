---
category: general
date: 2026-03-30
description: Μάθετε πώς να μορφοποιείτε την ημερομηνία σε ISO ενώ διαβάζετε τιμές
  ημερομηνίας/ώρας από το Excel και εξάγετε δεδομένα ημερομηνίας/ώρας του Excel χρησιμοποιώντας
  το Aspose.Cells σε C#.
draft: false
keywords:
- format date iso
- read excel datetime
- extract datetime excel
- Aspose.Cells date parsing
- Japanese era dates
language: el
og_description: Διαμορφώστε ημερομηνίες ISO από δεδομένα Excel χρησιμοποιώντας το
  Aspose.Cells. Αυτός ο οδηγός δείχνει πώς να διαβάσετε ημερομηνίες/ώρες Excel, να
  εξάγετε τις τιμές ημερομηνίας/ώρας του Excel και να εξάγετε ημερομηνίες ISO.
og_title: Μορφοποίηση ημερομηνίας ISO από το Excel – Βήμα‑βήμα οδηγός C#
tags:
- C#
- Excel
- DateTime
- Aspose.Cells
title: Μορφοποίηση ημερομηνίας ISO από το Excel – Πλήρης Οδηγός C#
url: /el/net/excel-custom-number-date-formatting/format-date-iso-from-excel-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# μορφοποίηση ημερομηνίας iso από το Excel – Πλήρης Οδηγός C#

Έχετε χρειαστεί ποτέ να **format date iso** όταν εξάγετε ημερομηνίες από ένα φύλλο Excel; Ίσως διαχειρίζεστε ημερομηνίες ιαπωνικής εποχής, ή απλώς θέλετε μια καθαρή συμβολοσειρά `yyyy‑MM‑dd` για ένα payload API. Σε αυτό το tutorial θα δείτε ακριβώς πώς να **read Excel datetime** κελιά, **extract datetime Excel** τιμές, και να τις μετατρέψετε σε μορφή ISO‑8601 — χωρίς εικασίες.

Θα περάσουμε από ένα πραγματικό παράδειγμα που χρησιμοποιεί Aspose.Cells, θα εξηγήσουμε γιατί κάθε γραμμή έχει σημασία, και θα σας δείξουμε το τελικό αποτέλεσμα που μπορείτε να αντιγράψετε‑επικολλήσετε στο πρόγραμμά σας. Στο τέλος, θα μπορείτε να χειριστείτε περίεργες συμβολοσειρές εποχής όπως “令和3年5月1日” και να παραγάγετε μια τυπική ημερομηνία ISO, έτοιμη για βάσεις δεδομένων, JSON ή όπου τη χρειάζεστε.

## Προαπαιτούμενα

- .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί και με .NET Framework)
- Aspose.Cells για .NET (δωρεάν δοκιμή ή έκδοση με άδεια)
- Βασική εξοικείωση με C# και έννοιες του Excel
- Visual Studio ή οποιονδήποτε επεξεργαστή C# προτιμάτε

Δεν απαιτούνται επιπλέον πακέτα NuGet πέρα από το Aspose.Cells, οπότε η ρύθμιση είναι αρκετά απλή.

---

## Βήμα 1: Δημιουργία Workbook και Στόχευση του Πρώτου Worksheet

Το πρώτο πράγμα που κάνετε είναι να δημιουργήσετε ένα νέο αντικείμενο `Workbook`. Αυτό σας δίνει μια αναπαράσταση σε μνήμη ενός αρχείου Excel, την οποία μπορείτε στη συνέχεια να επεξεργαστείτε ή να διαβάσετε.

```csharp
using Aspose.Cells;
using System.Globalization;

// Step 1: Initialize a new workbook and grab the first worksheet
Workbook workbook = new Workbook();                 // creates an empty .xlsx
Worksheet worksheet = workbook.Worksheets[0];      // the default sheet is "Sheet1"
```

*Why this matters:*  
Creating the workbook programmatically lets you avoid dealing with physical files during testing. It also ensures the worksheet reference is always valid—no null‑reference surprises later when you try to **read Excel datetime** values.

## Βήμα 2: Εγγραφή Συμβολοσειράς Ημερομηνίας Ιαπωνικής Εποχής σε Κελί

Ο στόχος μας είναι να δείξουμε την ανάλυση μιας μη‑Γρηγοριανής ημερομηνίας. Θα τοποθετήσουμε τη συμβολοσειρά εποχής απευθείας στο κελί **A1**.

```csharp
// Step 2: Insert a Japanese era date string into cell A1
worksheet.Cells["A1"].PutValue("令和3年5月1日");
```

*Pro tip:* If you’re pulling data from an existing workbook, you’d skip the `PutValue` call and just reference the cell that already contains the date. The key is that the cell holds a **string** that represents a date in the Japanese lunisolar calendar.

## Βήμα 3: Διαμόρφωση Culture που Κατανοεί το Ιαπωνικό Λουνισολάριο Ημερολόγιο

Η κλάση `CultureInfo` του .NET σας επιτρέπει να καθορίσετε πώς πρέπει να ερμηνεύονται οι ημερομηνίες. Αντικαθιστώντας το προεπιλεγμένο Γρηγοριανό ημερολόγιο με το `JapaneseLunisolarCalendar`, δίνετε στον αναλυτή το απαραίτητο πλαίσιο.

```csharp
// Step 3: Set up a culture using the Japanese lunisolar calendar
CultureInfo japaneseCulture = new CultureInfo("ja-JP");
japaneseCulture.DateTimeFormat.Calendar = new JapaneseLunisolarCalendar();
```

*Why we do this:*  
If you tried to parse “令和3年5月1日” with the default culture, .NET would throw a `FormatException`. Swapping in the lunisolar calendar tells the runtime exactly how to map “令和3年” (the 3rd year of the Reiwa era) to the Gregorian year 2021.

## Βήμα 4: Ανάλυση Τιμής Κελιού ως `DateTime` Χρησιμοποιώντας το Διαμορφωμένο Culture

Τώρα έρχεται η καρδιά της λειτουργίας—η μετατροπή της συμβολοσειράς εποχής σε ένα έγκυρο αντικείμενο `DateTime`. Το Aspose.Cells παρέχει μια βολική υπερφόρτωση `GetDateTime` που δέχεται ένα `CultureInfo`.

```csharp
// Step 4: Retrieve the cell value as a DateTime, respecting the Japanese culture
DateTime parsedDate = worksheet.Cells["A1"].GetDateTime(japaneseCulture);
```

*What’s happening under the hood:*  
`GetDateTime` reads the raw string, applies the supplied culture’s calendar rules, and returns a `DateTime` that represents the same moment in the Gregorian calendar. This is the moment where you **extract datetime Excel** data in a form you can work with in .NET.

## Βήμα 5: Εξαγωγή της Αναλυμένης Ημερομηνίας σε Μορφή ISO 8601

Τέλος, μορφοποιούμε το `DateTime` ως συμβολοσειρά ISO—`yyyy‑MM‑dd`—που γίνεται ευρέως αποδεκτό από APIs, βάσεις δεδομένων και front‑end frameworks.

```csharp
// Step 5: Print the date in ISO format (e.g., 2021-05-01)
Console.WriteLine(parsedDate.ToString("yyyy-MM-dd")); // Output: 2021-05-01
```

*Why ISO?*  
ISO 8601 eliminates ambiguity. “05/01/2021” could be May 1st or January 5th depending on locale. `2021-05-01` is crystal clear, which is why we **format date iso** in almost every integration scenario.

## Πλήρες Παράδειγμα Εργασίας

Παρακάτω είναι το πλήρες, έτοιμο‑για‑εκτέλεση πρόγραμμα. Αντιγράψτε το σε ένα project console app, προσθέστε την αναφορά Aspose.Cells, και πατήστε **F5**.

```csharp
using Aspose.Cells;
using System;
using System.Globalization;

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook and select the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Write a Japanese era date string into cell A1
        worksheet.Cells["A1"].PutValue("令和3年5月1日");

        // 3️⃣ Set up Japanese lunisolar culture
        CultureInfo japaneseCulture = new CultureInfo("ja-JP");
        japaneseCulture.DateTimeFormat.Calendar = new JapaneseLunisolarCalendar();

        // 4️⃣ Parse the cell value as DateTime using the culture
        DateTime parsedDate = worksheet.Cells["A1"].GetDateTime(japaneseCulture);

        // 5️⃣ Output the date in ISO format
        Console.WriteLine(parsedDate.ToString("yyyy-MM-dd")); // 2021-05-01
    }
}
```

**Αναμενόμενο αποτέλεσμα**

```
2021-05-01
```

Τρέξτε το μία φορά, και θα δείτε την ημερομηνία σε μορφή ISO να εμφανίζεται στην κονσόλα. Αυτό είναι ολόκληρη η αλυσίδα από **read Excel datetime** μέχρι **format date iso**.

## Διαχείριση Συνηθισμένων Edge Cases

### 1. Κελιά που Περιέχουν Πραγματικούς Αριθμούς Ημερομηνίας Excel

Μερικές φορές το Excel αποθηκεύει ημερομηνίες ως σειριακούς αριθμούς (π.χ., `44204`). Σε αυτή την περίπτωση, δεν χρειάζεται culture· απλώς καλέστε `GetDateTime()` χωρίς παραμέτρους:

```csharp
DateTime serialDate = worksheet.Cells["B2"].GetDateTime(); // B2 holds a numeric date
Console.WriteLine(serialDate.ToString("yyyy-MM-dd"));
```

### 2. Κενά ή Μη Έγκυρα Κελιά

Αν ένα κελί είναι κενό ή περιέχει μη αναγνώσιμη συμβολοσειρά, το `GetDateTime` θα ρίξει εξαίρεση. Τυλίξτε την κλήση σε `try/catch` ή ελέγξτε πρώτα το `IsDateTime`:

```csharp
if (worksheet.Cells["C3"].Type == CellValueType.IsDateTime)
{
    DateTime safeDate = worksheet.Cells["C3"].GetDateTime();
    Console.WriteLine(safeDate.ToString("yyyy-MM-dd"));
}
else
{
    Console.WriteLine("Cell C3 does not contain a valid date.");
}
```

### 3. Διαφορετικές Μορφές Εποχής

Άλλες ιαπωνικές εποχές (Heisei, Showa) ακολουθούν το ίδιο μοτίβο. Το ίδιο `JapaneseLunisolarCalendar` θα τις διαχειριστεί αυτόματα, οπότε δεν χρειάζεται επιπλέον λογική· απλώς δώστε τη συμβολοσειρά.

## Pro Tips & Gotchas

- **Performance:** When processing large spreadsheets, reuse a single `CultureInfo` instance instead of creating a new one inside a loop.
- **Thread Safety:** `CultureInfo` objects are read‑only after you set the calendar, so they’re safe to share across threads.
- **Aspose.Cells Licensing:** If you’re using the free trial, remember that some features may be limited after the trial period expires. The date parsing shown here works fine in both trial and licensed modes.
- **Time Zones:** The `DateTime` you get is **unspecified** (no time zone). If you need UTC, call `DateTime.SpecifyKind(parsedDate, DateTimeKind.Utc)` or convert using `TimeZoneInfo`.

## Συμπέρασμα

Καλύψαμε όλα όσα χρειάζεστε για να **format date iso** από ένα βιβλίο εργασίας Excel χρησιμοποιώντας C#. Ξεκινώντας από μια ακατέργαστη συμβολοσειρά ιαπωνικής εποχής, **read Excel datetime**, ρυθμίσαμε το κατάλληλο culture, **extract datetime excel** δεδομένα, και τελικά εξάγαμε μια καθαρή συμβολοσειρά ISO‑8601. Η προσέγγιση λειτουργεί για οποιαδήποτε αναπαράσταση ημερομηνίας που μπορεί να σας πετάξει το Excel, είτε είναι σειριακός αριθμός, συμβολοσειρά εξειδικευμένης τοπικής ρύθμισης ή παραδοσιακή μορφή εποχής.

Τι επόμενα βήματα; Δοκιμάστε να κάνετε βρόχο σε ολόκληρη μια στήλη ημερομηνιών, να γράψετε τα αποτελέσματα ISO πίσω σε νέο φύλλο, ή να τα στείλετε απευθείας σε payload JSON για μια web υπηρεσία. Αν σας ενδιαφέρουν άλλα ημερολογιακά συστήματα (Εβραϊκό, Ισλαμικό), το Aspose.Cells και το `CultureInfo` του .NET κάνουν αυτά τα πειράματα εξίσου εύκολα.

Έχετε ερωτήσεις ή μια δύσκολη μορφή ημερομηνίας που δεν μπορείτε να λύσετε; Αφήστε ένα σχόλιο παρακάτω, και καλή προγραμματιστική!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}