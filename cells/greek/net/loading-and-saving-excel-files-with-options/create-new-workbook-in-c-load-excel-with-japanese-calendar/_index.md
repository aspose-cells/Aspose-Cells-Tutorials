---
category: general
date: 2026-02-26
description: Δημιουργήστε νέο βιβλίο εργασίας σε C# και μάθετε πώς να φορτώνετε αρχεία
  Excel, να ορίσετε το ημερολόγιο στα Ιαπωνικά και να εξάγετε ημερομηνίες από το Excel
  απρόσκοπτα.
draft: false
keywords:
- create new workbook
- how to load excel
- how to set calendar
- extract date from excel
- read japanese dates
language: el
og_description: Δημιουργήστε νέο βιβλίο εργασίας σε C# και μάθετε γρήγορα πώς να φορτώνετε
  το Excel, να ορίζετε ιαπωνικό ημερολόγιο και να εξάγετε ημερομηνίες από αρχεία Excel.
og_title: Δημιουργία νέου βιβλίου εργασίας σε C# – Φόρτωση Excel με Ιαπωνικό ημερολόγιο
tags:
- C#
- Excel
- Aspose.Cells
- DateTime
title: Δημιουργία Νέου Φύλλου Εργασίας σε C# – Φόρτωση Excel με Ιαπωνικό Ημερολόγιο
url: /el/net/loading-and-saving-excel-files-with-options/create-new-workbook-in-c-load-excel-with-japanese-calendar/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία Νέου Φύλλου Εργασίας σε C# – Φόρτωση Excel με Ιαπωνικό Ημερολόγιο

Ποτέ χρειάστηκε να **δημιουργήσετε νέο βιβλίο εργασίας** σε C# αλλά δεν ήσασταν σίγουροι πώς να κάνετε το Excel να σέβεται το Ιαπωνικό ημερολόγιο; Δεν είστε μόνοι. Σε πολλές επιχειρηματικές περιπτώσεις λαμβάνετε υπολογιστικά φύλλα που αποθηκεύουν ημερομηνίες στο σύστημα των Ιαπωνικών εποχών, και η εξαγωγή αυτών των ημερομηνιών σωστά μπορεί να μοιάζει με αποκρυπτογράφηση μυστικού κώδικα.

Το θέμα είναι το εξής: μπορείτε να **δημιουργήσετε νέο βιβλίο εργασίας**, να πείτε στον φορτωτή να ερμηνεύει τις ημερομηνίες χρησιμοποιώντας το Ιαπωνικό ημερολόγιο, και στη συνέχεια να **εξάγετε ημερομηνία από το excel** με λίγες μόνο γραμμές κώδικα. Σε αυτόν τον οδηγό θα περάσουμε βήμα‑βήμα *πώς να φορτώσετε excel*, *πώς να ορίσετε ημερολόγιο* για Ιαπωνικές ημερομηνίες, και τέλος *να διαβάσετε Ιαπωνικές ημερομηνίες* από ένα κελί. Χωρίς περιττές πληροφορίες—απλώς ένα πλήρες, εκτελέσιμο παράδειγμα που μπορείτε να αντιγράψετε‑επικολλήσετε στο έργο σας.

## Προαπαιτούμενα

- .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί επίσης σε .NET Framework 4.6+)  
- Η βιβλιοθήκη **Aspose.Cells** (δωρεάν δοκιμαστική ή αδειοδοτημένη έκδοση). Εγκαταστήστε την μέσω NuGet:

```bash
dotnet add package Aspose.Cells
```

- Ένα αρχείο Excel (`JapanDates.xlsx`) που περιέχει ημερομηνίες Ιαπωνικής εποχής στο κελί A1.

Αυτό είναι όλο. Αν έχετε αυτά, μπορούμε να ξεκινήσουμε αμέσως.

---

## Δημιουργία Νέου Φύλλου Εργασίας και Ορισμός Ιαπωνικού Ημερολογίου

Το πρώτο βήμα είναι να **δημιουργήσετε νέο βιβλίο εργασίας** αντικείμενο και να ρυθμίσετε το `LoadOptions` ώστε ο αναλυτής να ξέρει ποιο ημερολόγιο να χρησιμοποιήσει.

```csharp
using Aspose.Cells;
using System;

class JapaneseDateReader
{
    static void Main()
    {
        // Step 1: Create a new workbook instance
        Workbook workbook = new Workbook();

        // Step 2: Set load options to interpret dates using the Japanese calendar
        workbook.LoadOptions = new LoadOptions { Calendar = CalendarType.Japanese };

        // Step 3: Load the workbook from a file
        workbook.Load("YOUR_DIRECTORY/JapanDates.xlsx");

        // Step 4: Access cell A1 – it now contains a proper DateTime value
        var cellA1 = workbook.Worksheets[0].Cells["A1"];
        DateTime dateValue = cellA1.GetDateTime();

        Console.WriteLine($"The Japanese date in A1 is: {dateValue:yyyy-MM-dd}");
    }
}
```

> **Pro tip:** Η ιδιότητα `LoadOptions.Calendar` δέχεται αρκετές τιμές enum (`Gregorian`, `Japanese`, `Hijri`, κ.λπ.). Η σωστή επιλογή εξασφαλίζει ότι η βιβλιοθήκη μετατρέπει το κείμενο της εποχής (π.χ. “令和3年”) σε ένα .NET `DateTime`.

![δημιουργία νέου βιβλίου εργασίας – παράδειγμα στιγμιότυπου](image-url.png "Στιγμιότυπο που δείχνει ένα νέο αντικείμενο βιβλίου εργασίας με ρυθμίσεις Ιαπωνικού ημερολογίου"){: .align-center alt="δημιουργία νέου βιβλίου εργασίας – παράδειγμα στιγμιότυπου"}

### Γιατί λειτουργεί αυτό

- **Δημιουργία βιβλίου εργασίας**: `new Workbook()` σας δίνει ένα καθαρό καμβά—χωρίς κρυφά φύλλα, χωρίς προεπιλεγμένα δεδομένα.
- **LoadOptions**: Αναθέτοντας `CalendarType.Japanese` *πριν* καλέσετε `Load`, ο αναλυτής αντιμετωπίζει τυχόν συμβολοσειρές εποχής ως ημερομηνίες αντί για απλό κείμενο.
- **GetDateTime()**: Μετά τη φόρτωση, `cellA1.GetDateTime()` επιστρέφει ένα πραγματικό αντικείμενο `DateTime`, επιτρέποντάς σας να κάνετε αριθμητικές πράξεις, μορφοποίηση ή εισαγωγές στη βάση δεδομένων χωρίς επιπλέον βήματα μετατροπής.

---

## Πώς να Φορτώσετε Σωστά το Αρχείο Excel

Μπορεί να αναρωτιέστε, “Υπάρχει κάποιος ειδικός τρόπος για **πώς να φορτώσετε excel** όταν δουλεύετε με μη‑Γρηγοριανά ημερολόγια?” Η απάντηση είναι ναι—πάντα ορίστε το `LoadOptions` *πριν* καλέσετε το `Load`. Αν φορτώσετε πρώτα και μετά αλλάξετε το ημερολόγιο, οι ημερομηνίες έχουν ήδη αναλυθεί λανθασμένα.

```csharp
// Example of a wrong order – will treat Japanese dates as plain strings
Workbook badWorkbook = new Workbook();
badWorkbook.Load("JapanDates.xlsx");          // Loads with default Gregorian calendar
badWorkbook.LoadOptions.Calendar = CalendarType.Japanese; // Too late!
```

Το παραπάνω απόσπασμα δείχνει ένα κοινό λάθος. Η σωστή σειρά (όπως φαίνεται στην προηγούμενη ενότητα) εγγυάται ότι η μηχανή ερμηνεύει τα κελιά *ως ημερομηνίες* από την αρχή.

---

## Πώς να Ορίσετε Ημερολόγιο για Ιαπωνικές Ημερομηνίες

Αν χρειάζεται να αλλάζετε ημερολόγια εν κινήσει—π.χ., επεξεργάζεστε μια σειρά αρχείων που χρησιμοποιούν διαφορετικά συστήματα εποχών—μπορείτε να επαναχρησιμοποιήσετε το ίδιο αντικείμενο `Workbook` με ένα νέο `LoadOptions` κάθε φορά.

```csharp
void LoadWithCalendar(string filePath, CalendarType calendar)
{
    Workbook wb = new Workbook
    {
        LoadOptions = new LoadOptions { Calendar = calendar }
    };
    wb.Load(filePath);
    // Now you can read dates according to the chosen calendar
}
```

Καλώντας `LoadWithCalendar("JapanDates.xlsx", CalendarType.Japanese)` παίρνετε το ίδιο αποτέλεσμα με το κύριο παράδειγμά μας, ενώ `CalendarType.Gregorian` θα θεωρούσε το ίδιο κελί ως απλή συμβολοσειρά (ή θα έριχνε εξαίρεση αν η μορφή είναι μη αναγνωρίσιμη).

---

## Εξαγωγή Ημερομηνίας από το Excel – Ανάγνωση Ιαπωνικών Ημερομηνιών

Τώρα που το βιβλίο εργασίας φορτώθηκε με το σωστό ημερολόγιο, η εξαγωγή της ημερομηνίας είναι απλή. Η μέθοδος `Cell.GetDateTime()` επιστρέφει ένα `DateTime` που σέβεται τη μετατροπή εποχής.

```csharp
DateTime ExtractJapaneseDate(Workbook wb, string address)
{
    var cell = wb.Worksheets[0].Cells[address];
    return cell.GetDateTime(); // Returns a .NET DateTime
}

// Usage
DateTime japaneseDate = ExtractJapaneseDate(workbook, "A1");
Console.WriteLine($"Extracted date: {japaneseDate:d}");
```

### Ακραίες Περιπτώσεις & Σενάρια “Τι Αν”

| Κατάσταση                                 | Τι Πρέπει Να Κάνετε                                                                                     |
|-------------------------------------------|----------------------------------------------------------------------------------------------------------|
| Το κελί περιέχει **κείμενο** αντί για ημερομηνία | Καλέστε πρώτα `cell.GetString()`, επικυρώστε με `DateTime.TryParse`, ή επιβάλετε επικύρωση δεδομένων στο Excel. |
| Πολλά φύλλα εργασίας χρειάζονται επεξεργασία | Επανάληψη μέσω `workbook.Worksheets` και εφαρμογή της ίδιας λογικής εξαγωγής σε κάθε φύλλο.               |
| Οι ημερομηνίες είναι αποθηκευμένες ως **αριθμοί** (σειριακό Excel) | `cell.GetDateTime()` λειτουργεί ακόμη επειδή το Aspose.Cells μετατρέπει αυτόματα τους σειριακούς αριθμούς. |
| Το αρχείο είναι **προστατευμένο με κωδικό** | Ορίστε `LoadOptions.Password = "yourPwd"` πριν καλέσετε `Load`.                                         |

---

## Πλήρες Παράδειγμα Εργασίας (Έτοιμο για Αντιγραφή‑Επικόλληση)

Παρακάτω βρίσκεται το πλήρες πρόγραμμα που μπορείτε να ενσωματώσετε σε μια εφαρμογή κονσόλας. Περιλαμβάνει διαχείριση σφαλμάτων και δείχνει όλες τις τέσσερις δευτερεύουσες λέξεις‑κλειδιά σε συμφραζόμενα.

```csharp
using Aspose.Cells;
using System;

class JapaneseDateReader
{
    static void Main()
    {
        // --------------------------------------------------------------------
        // 1️⃣  Create new workbook and configure calendar (primary keyword)
        // --------------------------------------------------------------------
        Workbook workbook = new Workbook
        {
            LoadOptions = new LoadOptions { Calendar = CalendarType.Japanese }
        };

        // --------------------------------------------------------------------
        // 2️⃣  How to load excel – correct order matters (secondary keyword)
        // --------------------------------------------------------------------
        try
        {
            workbook.Load("YOUR_DIRECTORY/JapanDates.xlsx");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Failed to load Excel file: {ex.Message}");
            return;
        }

        // --------------------------------------------------------------------
        // 3️⃣  How to set calendar – already done before loading (secondary)
        // --------------------------------------------------------------------
        // (If you need to change it later, see the LoadWithCalendar method above.)

        // --------------------------------------------------------------------
        // 4️⃣  Extract date from excel – read Japanese dates (secondary keywords)
        // --------------------------------------------------------------------
        try
        {
            var cell = workbook.Worksheets[0].Cells["A1"];
            DateTime japaneseDate = cell.GetDateTime(); // Proper DateTime thanks to the calendar setting
            Console.WriteLine($"Japanese date in A1 → {japaneseDate:yyyy-MM-dd}");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Error extracting date: {ex.Message}");
        }
    }
}
```

**Αναμενόμενη έξοδος** (υπόθεση ότι το A1 περιέχει “令和3年5月12日”):

```
Japanese date in A1 → 2021-05-12
```

Αν το κελί περιέχει μια Γρηγοριανή ημερομηνία όπως “2021‑05‑12”, ο ίδιος κώδικας λειτουργεί ακόμη επειδή η βιβλιοθήκη επιστρέφει αυτόματα τη Γρηγοριανή ερμηνεία.

---

## Συμπέρασμα

Τώρα ξέρετε πώς να **δημιουργήσετε νέο βιβλίο εργασίας**, να **φορτώσετε σωστά το excel**, να **ορίσετε το κατάλληλο ημερολόγιο**, και τελικά να **εξάγετε ημερομηνία από το excel** ενώ **διαβάζετε Ιαπωνικές ημερομηνίες** χωρίς καμία χειροκίνητη επεξεργασία. Το βασικό συμπέρασμα είναι ότι το ημερολόγιο πρέπει να ορίζεται *πριν* τη φόρτωση· μόλις το βιβλίο εργασίας είναι στη μνήμη, οι ημερομηνίες έχουν ήδη μετατραπεί σε σωστά αντικείμενα `DateTime`.

### Τι ακολουθεί;

- **Επεξεργασία παρτίδας**: Επανάληψη σε φάκελο αρχείων, καλώντας `LoadWithCalendar` για το καθένα.  
- **Εξαγωγή σε άλλες μορφές**: Χρησιμοποιήστε `workbook.Save("output.csv")` μετά τη μετατροπή.  
- **Τοπικοποίηση**: Συνδυάστε `CultureInfo` με `DateTime.ToString` για να εμφανίσετε τις ημερομηνίες στη γλώσσα προτίμησης του χρήστη.

Πειραματιστείτε—αντικαταστήστε το `CalendarType.Japanese` με `CalendarType.Hijri` ή `CalendarType.Gregorian` και παρακολουθήστε τον ίδιο κώδικα να προσαρμόζεται αυτόματα. Αν αντιμετωπίσετε προβλήματα, αφήστε ένα σχόλιο παρακάτω ή ελέγξτε την τεκμηρίωση του Aspose.Cells για πιο βαθιές πληροφορίες API.

Καλό κώδικα, και απολαύστε τη μετατροπή των μυστηριωδών Ιαπωνικών ημερομηνιών εποχής σε καθαρές τιμές .NET `DateTime`!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}