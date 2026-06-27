---
category: general
date: 2026-06-27
description: Μάθετε πώς να αναλύετε ημερομηνίες ιαπωνικής εποχής σε C# και στη συνέχεια
  να μορφοποιείτε datetime yyyy‑mm‑dd για έξοδο ISO. Κώδικας βήμα‑βήμα, ακραίες περιπτώσεις
  και συμβουλές.
draft: false
keywords:
- parse japanese era date
- format datetime yyyy-mm-dd
- C# JapaneseCalendar
- CultureInfo date parsing
- .NET DateTime era handling
language: el
og_description: Αναλύστε ημερομηνία ιαπωνικής εποχής σε C# και μορφοποιήστε datetime
  yyyy‑mm‑dd χωρίς κόπο. Πλήρες παράδειγμα με εξηγήσεις και παγίδες.
og_title: Ανάλυση ημερομηνίας ιαπωνικής εποχής σε C# – Πλήρης οδηγός προγραμματισμού
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Learn how to parse Japanese era date in C# and then format datetime
    yyyy-mm-dd for ISO output. Step‑by‑step code, edge cases, and tips.
  headline: Parse Japanese era date in C# – Complete Guide
  type: TechArticle
- description: Learn how to parse Japanese era date in C# and then format datetime
    yyyy-mm-dd for ISO output. Step‑by‑step code, edge cases, and tips.
  name: Parse Japanese era date in C# – Complete Guide
  steps:
  - name: Multiple Eras
    text: Japan has gone through several eras (Meiji, Taishō, Shōwa, Heisei, Reiwa).
      The `JapaneseCalendar` automatically maps them, so `"H30-12-31"` (Heisei 30)
      becomes `2018-12-31`. Just keep the same parsing logic; the calendar does the
      heavy lifting.
  - name: Invalid Input
    text: 'If a string doesn’t match the expected pattern, `Parse` throws. Use `TryParseExact`
      as shown earlier, or pre‑validate with a regular expression:'
  - name: Time Zones
    text: '`DateTime` objects are “kind‑agnostic” by default. If you need a UTC timestamp,
      call:'
  type: HowTo
tags:
- C#
- .NET
- DateTime
- Localization
title: Ανάλυση ημερομηνίας ιαπωνικής εποχής σε C# – Πλήρης οδηγός
url: /el/net/data-loading-and-parsing/parse-japanese-era-date-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ανάλυση ημερομηνίας ιαπωνικής εποχής σε C# – Πλήρης Οδηγός

Έχετε ποτέ χρειαστεί να **αναλύσετε ημερομηνία ιαπωνικής εποχής** σε μια εφαρμογή .NET και αναρωτηθήκατε γιατί το αποτέλεσμα φαίνεται λανθασμένο; Δεν είστε μόνοι. Σε πολλά παλαιά συστήματα, οι ημερομηνίες εμφανίζονται σε μορφή “R3‑04‑01”, και πρέπει να τις μετατρέψετε σε μια καθαρή συμβολοσειρά **format datetime yyyy-mm-dd** για API ή βάσεις δεδομένων.  

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από τις ακριβείς ενέργειες για να το πετύχετε, θα εξηγήσουμε γιατί κάθε μέρος είναι σημαντικό, και θα σας δείξουμε πώς να αντιμετωπίσετε τις δύσκολες περιπτώσεις που συχνά προκαλούν προβλήματα στους προγραμματιστές.

> **Σημείωση:** Όλος ο κώδικας είναι έτοιμος για αντιγραφή‑επικόλληση σε μια εφαρμογή console που στοχεύει .NET 6 ή νεότερη έκδοση.

## Τι Θα Χρειαστείτε

- .NET 6 SDK (ή οποιαδήποτε πρόσφατη έκδοση)
- Βασική εξοικείωση με τη C# και το namespace `System.Globalization`
- Ένα IDE ή επεξεργαστή – Visual Studio, VS Code, Rider, ό,τι προτιμάτε

Δεν απαιτούνται εξωτερικά πακέτα NuGet· όλα βρίσκονται στη BCL.

## Βήμα 1: Ρύθμιση της Ιαπωνικής Κουλτούρας με το Αυτοκρατορικό Ημερολόγιο

Πρώτα, χρειαζόμαστε ένα `CultureInfo` που γνωρίζει το ιαπωνικό αυτοκρατορικό ημερολόγιο. Από προεπιλογή, το `ja-JP` χρησιμοποιεί το Γρηγοριανό ημερολόγιο, οπότε αντικαθιστούμε το `DateTimeFormat.Calendar` του με μια παρουσία `JapaneseCalendar`.

```csharp
using System;
using System.Globalization;

class Program
{
    static void Main()
    {
        // Step 1: Create a Japanese culture and switch to the Japanese imperial calendar
        CultureInfo japaneseCulture = new CultureInfo("ja-JP");
        japaneseCulture.DateTimeFormat.Calendar = new JapaneseCalendar();

        // (The rest of the code follows...)
```

> **Γιατί είναι σημαντικό:** Το `JapaneseCalendar` μετατρέπει τα σύμβολα εποχής (π.χ. “R” για Reiwa) στο σωστό Γρηγοριανό έτος. Χωρίς αυτό, το `DateTime.Parse` θα ρίξει `FormatException`.

## Βήμα 2: Ανάλυση της Συμβολοσειράς Ημερομηνίας Βασισμένης στην Εποχή

Τώρα μπορούμε να περάσουμε μια συμβολοσειρά όπως `"R3-04-01"` στο `DateTime.Parse`. Η κουλτούρα που μόλις διαμορφώσαμε λέει στον αναλυτή πώς να ερμηνεύσει το τμήμα “R3”.

```csharp
        // Step 2: Parse a date string that uses the Japanese era format (e.g., "R3-04-01")
        string eraDate = "R3-04-01";
        DateTime parsedDate = DateTime.Parse(eraDate, japaneseCulture);
```

Αν προτιμάτε μια πιο ασφαλή προσέγγιση που αποφεύγει εξαιρέσεις σε λανθασμένη είσοδο, αντικαταστήστε το `Parse` με `TryParseExact`:

```csharp
        // Safer alternative with TryParseExact
        if (DateTime.TryParseExact(
                eraDate,
                "ggy-MM-dd",               // ggy = era+year, MM = month, dd = day
                japaneseCulture,
                DateTimeStyles.None,
                out DateTime safeDate))
        {
            parsedDate = safeDate;
        }
        else
        {
            Console.WriteLine("Unable to parse the Japanese era date.");
            return;
        }
```

> **Συμβουλή:** Η προσαρμοσμένη μορφή `"ggy-MM-dd"` λέει ακριβώς στον αναλυτή τι να περιμένει. Το “gg” είναι ο δείκτης εποχής, το “y” το έτος μέσα σε αυτήν την εποχή.

## Βήμα 3: Μετατροπή του Αποτελέσματος σε ISO 8601 (`format datetime yyyy-mm-dd`)

Τέλος, εξάγουμε το `DateTime` σε μια τυπική μορφή ISO. Ο μορφοποιητής `"yyyy-MM-dd"` κάνει ακριβώς αυτό.

```csharp
        // Step 3: Display the parsed date in a standard ISO format
        string isoDate = parsedDate.ToString("yyyy-MM-dd", CultureInfo.InvariantCulture);
        Console.WriteLine(isoDate); // Expected output: 2021-04-01
    }
}
```

Η εκτέλεση του προγράμματος εμφανίζει:

```
2021-04-01
```

Αυτή είναι η **format datetime yyyy-mm-dd** που θέλετε, έτοιμη για JSON payloads, εισαγωγές SQL ή οποιοδήποτε σύστημα downstream.

![παράδειγμα ανάλυσης ημερομηνίας ιαπωνικής εποχής](placeholder.png){alt="παράδειγμα ανάλυσης ημερομηνίας ιαπωνικής εποχής"}

## Διαχείριση Άλλων Εποχών και Ακραίων Περιπτώσεων

### Πολλαπλές Εποχές

Η Ιαπωνία έχει περάσει από πολλές εποχές (Meiji, Taishō, Shōwa, Heisei, Reiwa). Το `JapaneseCalendar` τις αντιστοιχίζει αυτόματα, έτσι το `"H30-12-31"` (Heisei 30) γίνεται `2018-12-31`. Απλώς διατηρήστε την ίδια λογική ανάλυσης· το ημερολόγιο κάνει το σκληρό κομμάτι.

### Μη Έγκυρη Είσοδος

Αν μια συμβολοσειρά δεν ταιριάζει με το αναμενόμενο μοτίβο, το `Parse` ρίχνει εξαίρεση. Χρησιμοποιήστε το `TryParseExact` όπως φαίνεται παραπάνω, ή προ‑επαληθεύστε με κανονική έκφραση:

```csharp
bool IsValidEraDate(string input) =>
    System.Text.RegularExpressions.Regex.IsMatch(
        input, @"^[RHS][0-9]+-\d{2}-\d{2}$", System.Text.RegularExpressions.RegexOptions.IgnoreCase);
```

### Ζώνες Ώρας

Τα αντικείμενα `DateTime` είναι «αδιάφορα τύπου» (kind‑agnostic) από προεπιλογή. Αν χρειάζεστε χρονική σήμανση UTC, καλέστε:

```csharp
DateTime utc = DateTime.SpecifyKind(parsedDate, DateTimeKind.Utc);
```

Ή χρησιμοποιήστε `DateTimeOffset` για πλήρη ευαισθησία στη ζώνη ώρας.

## Πλήρες Παράδειγμα Λειτουργίας

Ακολουθεί το πλήρες απόσπασμα που μπορείτε να ενσωματώσετε σε ένα νέο project console:

```csharp
using System;
using System.Globalization;

class Program
{
    static void Main()
    {
        // Initialize Japanese culture with the imperial calendar
        CultureInfo japaneseCulture = new CultureInfo("ja-JP");
        japaneseCulture.DateTimeFormat.Calendar = new JapaneseCalendar();

        // The era‑based date you want to convert
        string eraDate = "R3-04-01";

        // Try parsing – safer than Parse when input may be malformed
        if (!DateTime.TryParseExact(
                eraDate,
                "ggy-MM-dd",
                japaneseCulture,
                DateTimeStyles.None,
                out DateTime parsedDate))
        {
            Console.WriteLine("Failed to parse the Japanese era date.");
            return;
        }

        // Convert to ISO 8601 (format datetime yyyy-mm-dd)
        string isoDate = parsedDate.ToString("yyyy-MM-dd", CultureInfo.InvariantCulture);
        Console.WriteLine($"Original era date: {eraDate}");
        Console.WriteLine($"Converted ISO date: {isoDate}");
    }
}
```

**Αναμενόμενη έξοδος console**

```
Original era date: R3-04-01
Converted ISO date: 2021-04-01
```

## Συνοπτική Επισκόπηση

Καλύψαμε πώς να **αναλύσετε ημερομηνία ιαπωνικής εποχής** με:

1. Δημιουργία `CultureInfo` για `ja-JP` και αντικατάσταση του `DateTimeFormat.Calendar` με `JapaneseCalendar`.
2. Χρήση του `DateTime.Parse` ή του πιο ανθεκτικού `TryParseExact` με προσαρμοσμένη μορφή.
3. Μορφοποίηση του προκύπτοντος `DateTime` με `"yyyy-MM-dd"` για να επιτύχετε την επιθυμητή **format datetime yyyy-mm-dd**.

Αυτό είναι ό,τι χρειάζεστε για να γεφυρώσετε τα κληρονομικά δεδομένα ιαπωνικής εποχής σε σύγχρονα συστήματα συμβατά με ISO.

## Τι Ακολουθεί;

- **Επεξεργασία σε παρτίδες:** Επανάληψη πάνω σε CSV με ημερομηνίες εποχής και εγγραφή ISO συμβολοσειρών σε βάση δεδομένων.
- **Τοπικοποίηση:** Μετατροπή ISO ημερομηνιών πίσω σε μορφή εποχής για εμφάνιση UI (`ToString("ggyy年MM月dd日", japaneseCulture)`).
- **Προσαρμοσμένα ημερολόγια:** Εξερευνήστε το `TaiwanCalendar` ή το `HijriCalendar` για άλλες περιφερειακές ανάγκες.

Πειραματιστείτε ελεύθερα—αλλάξτε τη συμβολοσειρά εποχής, δοκιμάστε ακραίες περιπτώσεις, ή ενσωματώστε αυτή τη λογική σε endpoints ASP.NET Core. Αν συναντήσετε πρόβλημα, αφήστε ένα σχόλιο παρακάτω· καλή προγραμματιστική!

## Τι Θα Πρέπει να Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικά παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να Εφαρμόσετε Επικύρωση Ημερομηνίας σε .NET Χρησιμοποιώντας Aspose.Cells: Ένας Πλήρης Οδηγός](/cells/english/net/data-validation/implement-date-validation-net-aspose-cells/)
- [Αλλαγή Συστήματος Ημερομηνίας Excel σε 1904 χρησιμοποιώντας Aspose.Cells .NET](/cells/english/net/calculation-engine/change-excel-date-system-aspose-cells-net/)
- [Πώς να Εφαρμόσετε και Μορφοποιήσετε Σχόλια Excel Χρησιμοποιώντας Aspose.Cells για .NET: Ένας Οδηγός Βήμα‑Βήμα](/cells/english/net/comments-annotations/implement-format-excel-comments-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}