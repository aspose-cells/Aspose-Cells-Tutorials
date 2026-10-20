---
category: general
date: 2026-09-24
description: Αναλύστε το DateTime με τη βασιλεία Ιαπωνικού αυτοκράτορα χρησιμοποιώντας
  το Aspose.Cells σε C#. Ενεργοποιήστε το ιαπωνικό ημερολόγιο εποχής, γράψτε αλφαριθμητικά
  εποχής και ανακτήστε ακριβείς τιμές DateTime.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- Parse DateTime with Japanese Emperor Reign
- Aspose.Cells
- C# date parsing
- Japanese era calendar
- Workbook Settings
- DateTimeValue
language: el
lastmod: 2026-09-24
og_description: Ανάλυση DateTime με τη διάρκεια της βασιλείας Ιαπωνικού αυτοκράτορα
  χρησιμοποιώντας το Aspose.Cells σε C#. Αυτό το σεμινάριο δείχνει πώς να ενεργοποιήσετε
  το ιαπωνικό ημερολόγιο εποχής, να γράψετε συμβολοσειρές εποχής και να διαβάσετε
  ξανά ένα σωστό DateTime.
og_image_alt: Screenshot of C# code parsing a Japanese era date with Aspose.Cells
og_title: Ανάλυση DateTime με τη διάρκεια βασιλείας Ιαπωνικού αυτοκράτορα χρησιμοποιώντας
  το Aspose.Cells – Οδηγός C#
schemas:
- author: Aspose
  dateModified: '2026-09-24'
  description: Parse DateTime with Japanese Emperor Reign using Aspose.Cells in C#.
    Enable the Japanese era calendar, write era strings, and retrieve accurate DateTime
    values.
  headline: Parse DateTime with Japanese Emperor Reign using Aspose.Cells
  type: TechArticle
- description: Parse DateTime with Japanese Emperor Reign using Aspose.Cells in C#.
    Enable the Japanese era calendar, write era strings, and retrieve accurate DateTime
    values.
  name: Parse DateTime with Japanese Emperor Reign using Aspose.Cells
  steps:
  - name: Multiple era formats
    text: 'Aspose.Cells recognises several era representations:'
  - name: Invalid strings
    text: 'When the string cannot be parsed (e.g., `"令和99年13月40日"`), `DateTimeValue`
      returns `DateTime.MinValue`. You can check for this condition:'
  - name: Disabling the feature
    text: 'If you later need to store raw era strings without conversion, set the
      flag back to `false`:'
  - name: Performance tip
    text: Enabling the era calendar adds a small overhead to every `PutValue` call
      that involves strings. If you only parse a handful of cells, enable the flag
      right before the operation and disable it afterward to minimise impact.
  type: HowTo
tags:
- Aspose.Cells
- C#
- DateTime
- Japanese era
- .NET
title: Ανάλυση DateTime με την περίοδο βασιλείας Ιαπωνικού αυτοκράτορα χρησιμοποιώντας
  το Aspose.Cells
url: /el/net/excel-custom-number-date-formatting/parse-datetime-with-japanese-emperor-reign-using-aspose-cell/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ανάλυση DateTime με Ιαπωνική Εποχή Αυτοκράτορα χρησιμοποιώντας το Aspose.Cells

Αν χρειάζεστε να **αναλύσετε DateTime με Ιαπωνική Εποχή Αυτοκράτορα** σε μια εφαρμογή .NET, αυτός ο οδηγός σας δείχνει ακριβώς πώς να το κάνετε με το Aspose.Cells. Ενεργοποιώντας το ημερολόγιο της Ιαπωνικής εποχής, γράφοντας μια συμβολοσειρά βασισμένη στην εποχή και διαβάζοντας την προκύπτουσα τιμή `DateTime`, λαμβάνετε αξιόπιστες, πολιτισμικά ενημερωμένες ημερομηνίες χωρίς χειροκίνητη επεξεργασία συμβολοσειρών.

Η εργασία με ημερομηνίες της Ιαπωνικής εποχής είναι συχνή στα χρηματοοικονομικά, την κυβέρνηση και τα παλαιά συστήματα που εξακολουθούν να αποθηκεύουν ημερομηνίες όπως “令和3年5月10日”. Αυτό το tutorial καλύπτει τη πλήρη ροή εργασίας, από τη ρύθμιση του έργου μέχρι την ανάκτηση ενός αντικειμένου `DateTime` που μπορείτε να χρησιμοποιήσετε σε υπολογισμούς, καταγραφή ή εμφάνιση UI.

## Τι θα μάθετε

- Πώς να προσθέσετε το πακέτο NuGet Aspose.Cells σε ένα έργο C#.
- Πώς να ενεργοποιήσετε το **Japanese era calendar** μέσω του `Workbook.Settings`.
- Πώς να γράψετε μια συμβολοσειρά ημερομηνίας Ιαπωνικής εποχής σε ένα κελί και να αφήσετε το Aspose.Cells να την αναλύσει αυτόματα.
- Πώς να διαβάσετε το αναλυμένο `DateTime` χρησιμοποιώντας την ιδιότητα `DateTimeValue`.

**Προαπαιτούμενα**  
- .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί επίσης με .NET Framework 4.7+).  
- Βασική εξοικείωση με C# και Visual Studio (ή οποιοδήποτε IDE).  
- Πρόσβαση στο Internet για λήψη του πακέτου Aspose.Cells.

---

## Βήμα 1: Εγκατάσταση Aspose.Cells

Ανοίξτε το φάκελο του έργου σας σε ένα τερματικό ή στην κονσόλα του NuGet Package Manager και εκτελέστε:

```bash
dotnet add package Aspose.Cells
```

Ή, στο Visual Studio, κάντε δεξί κλικ στο έργο → **Manage NuGet Packages** → αναζητήστε το **Aspose.Cells** και κάντε κλικ στο **Install**.  
Αυτό προσθέτει τη συναρμολόγηση `Aspose.Cells`, η οποία παρέχει τις δυνατότητες `Workbook`, `Worksheet` και ανάλυσης που χρειαζόμαστε.

## Βήμα 2: Ενεργοποίηση του ημερολογίου Ιαπωνικής εποχής

Το Aspose.Cells απενεργοποιεί την ανάλυση της Ιαπωνικής εποχής εξ ορισμού. Πρέπει να το ενεργοποιήσετε μέσω της σημαίας `Workbook.Settings.UseJapaneseEraCalendar`.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Create a new workbook instance
        Workbook workbook = new Workbook();

        // Enable parsing of Japanese era dates (e.g., 令和, 平成)
        workbook.Settings.UseJapaneseEraCalendar = true;
```

Ορίζοντας το `UseJapaneseEraCalendar` σε `true` λέει στη βιβλιοθήκη να ερμηνεύει τις συμβολοσειρές που περιέχουν ονόματα εποχών (`令和`, `平成`, `昭和`, κλπ.) σύμφωνα με τους επίσημους κανόνες του Ιαπωνικού ημερολογίου.

## Βήμα 3: Γράψτε μια συμβολοσειρά ημερομηνίας Ιαπωνικής εποχής σε ένα κελί

Στη συνέχεια, πάρτε το πρώτο φύλλο εργασίας και τοποθετήστε μια συμβολοσειρά ημερομηνίας Ιαπωνικής εποχής στο κελί **A1**.

```csharp
        // Access the first worksheet (index 0)
        Worksheet sheet = workbook.Worksheets[0];

        // Write the era‑based date string into cell A1
        sheet.Cells["A1"].PutValue("令和3年5月10日");
```

**Γιατί λειτουργεί αυτό:**  
Όταν το `UseJapaneseEraCalendar` είναι ενεργό, το `PutValue` εξετάζει τη συμβολοσειρά, εντοπίζει το πρόθεμα της εποχής (`令和`) και εσωτερικά τη μετατρέπει στο αντίστοιχο Γρηγοριανό έτος (2021). Η βιβλιοθήκη στη συνέχεια αποθηκεύει την τιμή ως ένα πραγματικό αντικείμενο `DateTime`, όχι απλώς κείμενο.

## Βήμα 4: Ανάκτηση της αναλυμένης τιμής `DateTime`

Τώρα διαβάστε το `DateTimeValue` του κελιού. Το Aspose.Cells επιστρέφει αυτόματα τη Γρηγοριανή ημερομηνία.

```csharp
        // Retrieve the parsed DateTime from cell A1
        DateTime parsedDate = sheet.Cells["A1"].DateTimeValue;

        // Output the result to the console
        Console.WriteLine($"Parsed Gregorian date: {parsedDate:yyyy-MM-dd}");
    }
}
```

Running the program prints:

```
Parsed Gregorian date: 2021-05-10
```

Η έξοδος επιβεβαιώνει ότι η **Parse DateTime with Japanese Emperor Reign** μετέτρεψε σωστά το “令和3年5月10日” σε 10 Μαΐου 2021.

## Βήμα 5: Διαχείριση περιπτώσεων άκρων και κοινών παραλλαγών

### Πολλαπλές μορφές εποχής
Το Aspose.Cells αναγνωρίζει πολλές αναπαραστάσεις εποχής:

| Era (Japanese) | Gregorian year range |
|----------------|----------------------|
| 明治 (Meiji)   | 1868‑1912            |
| 大正 (Taishō)  | 1912‑1926            |
| 昭和 (Shōwa)   | 1926‑1989            |
| 平成 (Heisei)  | 1989‑2019            |
| 令和 (Reiwa)   | 2019‑present         |

Αν τα δεδομένα πηγής σας συνδυάζουν πλήρους πλάτους χαρακτήρες, κενά ή χρησιμοποιούν τα καντζι “年”, “月”, “日”, ο αναλυτής εξακολουθεί να λειτουργεί. Για παράδειγμα, το `"平成31年4月30日"` γίνεται `2019-04-30`.

### Μη έγκυρες συμβολοσειρές
Όταν η συμβολοσειρά δεν μπορεί να αναλυθεί (π.χ., `"令和99年13月40日"`), το `DateTimeValue` επιστρέφει `DateTime.MinValue`. Μπορείτε να ελέγξετε αυτήν την κατάσταση:

```csharp
if (parsedDate == DateTime.MinValue)
{
    Console.WriteLine("The cell does not contain a valid Japanese era date.");
}
```

### Απενεργοποίηση της λειτουργίας
Αν αργότερα χρειαστεί να αποθηκεύσετε ακατέργαστες συμβολοσειρές εποχής χωρίς μετατροπή, ορίστε τη σημαία ξανά σε `false`:

```csharp
workbook.Settings.UseJapaneseEraCalendar = false;
```

### Συμβουλή απόδοσης
Η ενεργοποίηση του ημερολογίου εποχής προσθέτει μικρή επιβάρυνση σε κάθε κλήση `PutValue` που περιλαμβάνει συμβολοσειρές. Εάν αναλύετε μόνο λίγα κελιά, ενεργοποιήστε τη σημαία ακριβώς πριν τη λειτουργία και απενεργοποιήστε την μετά, ώστε να ελαχιστοποιήσετε την επίδραση.

## Πλήρες, εκτελέσιμο παράδειγμα

Παρακάτω είναι το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε, επικολλήσετε και να εκτελέσετε αμέσως.

```csharp
using Aspose.Cells;
using System;

class ParseJapaneseEraDemo
{
    static void Main()
    {
        // 1️⃣ Create a new workbook
        Workbook workbook = new Workbook();

        // 2️⃣ Turn on Japanese era parsing
        workbook.Settings.UseJapaneseEraCalendar = true;

        // 3️⃣ Access the first worksheet
        Worksheet sheet = workbook.Worksheets[0];

        // 4️⃣ Write an era date string into A1
        sheet.Cells["A1"].PutValue("令和3年5月10日");

        // 5️⃣ Retrieve the parsed DateTime
        DateTime parsedDate = sheet.Cells["A1"].DateTimeValue;

        // Verify the result
        Console.WriteLine($"Parsed Gregorian date: {parsedDate:yyyy-MM-dd}");
        // Expected output: Parsed Gregorian date: 2021-05-10
    }
}
```

**Expected output**

```
Parsed Gregorian date: 2021-05-10
```

Το πρόγραμμα δείχνει τη ροή από την αρχή μέχρι το τέλος για την **Parse DateTime with Japanese Emperor Reign** χρησιμοποιώντας το Aspose.Cells, από τη δημιουργία του βιβλίου εργασίας μέχρι την απόκτηση ενός χρήσιμου αντικειμένου `DateTime`.

---

## Συμπέρασμα

Τώρα γνωρίζετε πώς να **Parse DateTime with Japanese Emperor Reign** σε C# με:

1. Εγκαθιστώντας το **Aspose.Cells**.  
2. Ενεργοποιώντας το **Japanese era calendar** μέσω του `Workbook.Settings`.  
3. Γράφοντας συμβολοσειρές βασισμένες στην εποχή σε κελιά.  
4. Διαβάζοντας το προκύπτον `DateTimeValue`.  

Αυτή η προσέγγιση εξαλείφει την χειροκίνητη λογική ανάλυσης, σέβεται τα επίσημα όρια των εποχών και ενσωματώνεται αβίαστα με τον υπάρχοντα κώδικα διαχείρισης ημερομηνιών .NET.

**Επόμενα βήματα**  
- Εξερευνήστε άλλες λειτουργίες ειδικές για πολιτισμούς του Aspose.Cells, όπως **C# date parsing** για το Hijri ή το Ταϊλανδέζικο Βουδιστικό ημερολόγιο.  
- Συνδυάστε αυτήν την τεχνική με τις **Ρυθμίσεις Workbook** όπως το `CalcEngine` για την αξιολόγηση τύπων που αναφέρονται σε ημερομηνίες εποχής.  
- Χρησιμοποιήστε το αναλυμένο `DateTime` σε αναφορές, αποθήκευση σε βάση δεδομένων ή UI στοιχεία που απαιτούν Γρηγοριανές ημερομηνίες.

Νιώστε ελεύθεροι να πειραματιστείτε με διαφορετικές συμβολοσειρές εποχής, να διαχειριστείτε μη έγκυρες εισόδους και να ενσωματώσετε τη λύση σε μεγαλύτερους αγωγούς εισαγωγής δεδομένων. Καλή προγραμματιστική!

## Τι Θα Πρέπει Να Μάθετε Στη Σύντομη Μελλοντική

Τα παρακάτω tutorials καλύπτουν στενά σχετικές θεματικές που βασίζονται στις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Ανάλυση Ημερομηνιών Ιαπωνικής Εποχής σε Excel – Πλήρης Οδηγός για Προγραμματιστές C#](/cells/english/net/data-loading-and-parsing/parse-japanese-era-dates-in-excel-full-guide-for-c-developer/)
- [Πώς να Αναλύσετε Ιαπωνικές Ημερομηνίες σε C# – Πλήρης Οδηγός](/cells/english/net/data-loading-and-parsing/how-to-parse-japanese-dates-in-c-complete-guide/)
- [Πώς να Εφαρμόσετε Επικύρωση Ημερομηνίας σε .NET Χρησιμοποιώντας το Aspose.Cells: Ένας Εκτενής Οδηγός](/cells/english/net/data-validation/implement-date-validation-net-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}