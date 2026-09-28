---
category: general
date: 2026-03-22
description: Μάθετε πώς να μορφοποιήσετε την ημερομηνία/ώρα σε ISO, εξάγοντας την
  ημερομηνία από το Excel και εμφανίζοντας την ημερομηνία ISO χρησιμοποιώντας το Aspose.Cells
  σε C#.
draft: false
keywords:
- format datetime to iso
- extract date from excel
- display iso date
- Aspose.Cells date parsing
- Japanese era dates
language: el
og_description: Η μορφοποίηση ημερομηνίας/ώρας σε ISO έγινε εύκολη. Αυτός ο οδηγός
  δείχνει πώς να εξάγετε την ημερομηνία από το Excel και να εμφανίσετε την ημερομηνία
  ISO με το Aspose.Cells.
og_title: Μορφοποίηση datetime σε ISO σε C# – Βήμα‑βήμα Εκπαιδευτικό Σεμινάριο
tags:
- C#
- Aspose.Cells
- DateTime
- Excel
- ISO 8601
title: Μορφοποίηση datetime σε ISO σε C# – Πλήρης Οδηγός
url: /el/net/number-and-display-formats-in-excel/format-datetime-to-iso-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Μορφοποίηση datetime σε iso σε C# – Πλήρης Οδηγός

Έχετε χρειαστεί ποτέ να **format datetime to iso** αλλά η πηγή βρίσκεται μέσα σε ένα βιβλίο εργασίας Excel; Ίσως το κελί περιέχει μια ιαπωνική εποχή όπως “令和3年5月1日” και αναρωτιέστε πώς να το μετατρέψετε σε μια καθαρή συμβολοσειρά `2021‑05‑01`. Δεν είστε μόνοι. Σε αυτόν τον οδηγό θα **extract date from excel**, θα αναλύσουμε την ιαπωνική εποχή, και στη συνέχεια θα **display iso date** στην κονσόλα—όλα με μερικές γραμμές C# και Aspose.Cells.

Θα περάσουμε από όλα όσα χρειάζεστε: το απαιτούμενο πακέτο NuGet, τον ακριβή κώδικα που μπορείτε να αντιγράψετε‑και‑επικολλήσετε, γιατί κάθε γραμμή είναι σημαντική, και μια σειρά συμβουλών για σενάρια άκρων. Στο τέλος θα έχετε ένα επαναχρησιμοποιήσιμο απόσπασμα που μορφοποιεί datetime σε iso, ανεξάρτητα από το πόσο ιδιόρρυθμη φαίνεται η αρχική τιμή στο Excel.

## Τι Θα Χρειαστείτε

- .NET 6.0 ή νεότερο (ο κώδικας μεταγλωττίζεται επίσης σε .NET Framework 4.6+)
- Visual Studio 2022 (ή οποιονδήποτε επεξεργαστή προτιμάτε)
- **Aspose.Cells for .NET** πακέτο NuGet – `Install-Package Aspose.Cells`
- Ένα αρχείο Excel (ή ένα νέο βιβλίο εργασίας) που περιέχει μια ημερομηνία σε μορφή ιαπωνικής εποχής

Αυτό είναι όλο. Χωρίς επιπλέον βιβλιοθήκες, χωρίς COM interop, μόνο μια ενιαία, καλά τεκμηριωμένη μέθοδος.

## Βήμα 1: Δημιουργία Workbook και Εισαγωγή Ημερομηνίας σε Ιαπωνική Εποχή  

Πρώτα, χρειαζόμαστε ένα workbook για να δουλέψουμε. Αν έχετε ήδη ένα αρχείο Excel, μπορείτε να το φορτώσετε με `new Workbook("path")`. Για αυτό το παράδειγμα θα δημιουργήσουμε ένα νέο workbook στη μνήμη και θα τοποθετήσουμε μια συμβολοσειρά ιαπωνικής εποχής στο κελί **A1**.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a fresh workbook
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // 2️⃣ Write a Japanese era date (Reiwa 3 = 2021) into A1
        sheet.Cells["A1"].PutValue("令和3年5月1日");
```

> **Γιατί το κάνουμε:** Το Aspose.Cells αντιμετωπίζει τις τιμές των κελιών ως συμβολοσειρές από προεπιλογή. Εισάγοντας το ακατέργαστο κείμενο της εποχής προσομοιώνουμε ένα πραγματικό σενάριο όπου ένας Ιάπωνας πελάτης έχει εισάγει ημερομηνίες στο δικό του ημερολόγιο.

## Βήμα 2: Ενεργοποίηση Ανάλυσης Ιαπωνικής Εποχής και Εξαγωγή Ημερομηνίας  

Το Aspose.Cells μπορεί αυτόματα να μεταφράσει συμβολοσειρές ιαπωνικής εποχής σε αντικείμενα .NET `DateTime`—αρκεί να του το υποδείξετε. Η σημαία `DateTimeParseOptions.EnableJapaneseEra` κάνει το σκληρό έργο.

```csharp
        // 3️⃣ Retrieve the cell value while enabling Japanese era parsing
        CellValue parsed = sheet.Cells["A1"]
            .GetValue(CellValueType.DateTime, DateTimeParseOptions.EnableJapaneseEra);
```

> **Συμβουλή:** Αν ξεχάσετε την επιλογή `EnableJapaneseEra`, η βιβλιοθήκη θα επιστρέψει την αρχική συμβολοσειρά και η επόμενη μετατροπή σας θα αποτύχει. Πάντα ελέγχετε το `parsed.Type` αν διαχειρίζεστε μεικτό περιεχόμενο.

## Βήμα 3: Μετατροπή του Αναλυμένου DateTime σε ISO 8601  

Τώρα που έχουμε ένα έγκυρο `DateTime`, η μετατροπή του σε συμβολοσειρά μορφοποιημένη σε ISO είναι παιχνιδάκι. Το μοτίβο `"yyyy-MM-dd"` συμμορφώνεται με το τμήμα ημερομηνίας του ISO 8601, το οποίο είναι αυτό που απαιτούν τα περισσότερα APIs.

```csharp
        // 4️⃣ Convert to ISO 8601 (yyyy‑MM‑dd) and display it
        string isoDate = parsed.DateTimeValue.ToString("yyyy-MM-dd");
        Console.WriteLine($"ISO date: {isoDate}");
    }
}
```

Τρέχοντας το πρόγραμμα εμφανίζει:

```
ISO date: 2021-05-01
```

Αυτή είναι η **display iso date** που ζητούσατε.

## Πλήρες, Εκτελέσιμο Παράδειγμα  

Παρακάτω είναι το πλήρες μπλοκ κώδικα που μπορείτε να αντιγράψετε απευθείας σε ένα έργο κονσόλας. Χωρίς κρυφές εξαρτήσεις, χωρίς επιπλέον ρυθμίσεις.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Write a Japanese era date into cell A1
        worksheet.Cells["A1"].PutValue("令和3年5月1日");

        // Retrieve the cell value with Japanese era parsing enabled
        CellValue parsedValue = worksheet.Cells["A1"]
            .GetValue(CellValueType.DateTime, DateTimeParseOptions.EnableJapaneseEra);

        // Convert the DateTime to ISO 8601 format and output it
        string isoDate = parsedValue.DateTimeValue.ToString("yyyy-MM-dd");
        Console.WriteLine($"ISO date: {isoDate}");
    }
}
```

> **Αναμενόμενη έξοδος:** `ISO date: 2021-05-01`

## Ανάλυση Βήμα‑βήμα (Γιατί Κάθε Τμήμα Είναι Σημαντικό)

| Βήμα | Τι Συμβαίνει | Γιατί Είναι Σημαντικό |
|------|--------------|--------------------|
| **Create workbook** | Αρχικοποιεί ένα Excel container στη μνήμη. | Σας παρέχει ένα sandbox για δοκιμές χωρίς να αγγίξετε το σύστημα αρχείων. |
| **PutValue** | Αποθηκεύει τη ακατέργαστη συμβολοσειρά ιαπωνικής εποχής στο **A1**. | Μιμείται πραγματική εισαγωγή δεδομένων· εξασφαλίζει ότι ο αναλυτής βλέπει το ακριβές κείμενο. |
| **GetValue with `EnableJapaneseEra`** | Μετατρέπει τη συμβολοσειρά της εποχής σε .NET `DateTime`. | Διαχειρίζεται αυτόματα τη μετατροπή ημερολογίου—χωρίς ανάγκη χειροκίνητων πινάκων αναζήτησης. |
| **`ToString("yyyy-MM-dd")`** | Μορφοποιεί το `DateTime` σε ISO 8601. | Εγγυάται μια πολιτισμικά ανεξάρτητη, ταξινομήσιμη συμβολοσειρά ημερομηνίας που δέχεται από REST APIs, βάσεις δεδομένων κ.λπ. |
| **Console.WriteLine** | Εμφανίζει την τελική ISO ημερομηνία. | Επιβεβαιώνει ότι ολόκληρη η αλυσίδα λειτουργεί από άκρη σε άκρη. |

## Διαχείριση Συνηθισμένων Παραλλαγών  

### 1. Διαφορετικές Θέσεις Κελιών  

Αν η ημερομηνία σας βρίσκεται σε **B2** ή σε μια ονομαστική περιοχή, απλώς αντικαταστήστε το `"A1"` με τη σωστή διεύθυνση:

```csharp
worksheet.Cells["B2"].PutValue("令和2年12月31日");
var value = worksheet.Cells["B2"]
    .GetValue(CellValueType.DateTime, DateTimeParseOptions.EnableJapaneseEra);
```

### 2. Πολλαπλές Ημερομηνίες σε Στήλη  

Όταν χρειάζεται να **extract date from excel** για πολλές γραμμές, κάντε βρόχο μέσω του χρησιμοποιημένου εύρους:

```csharp
int lastRow = worksheet.Cells.MaxDataRow;
for (int i = 0; i <= lastRow; i++)
{
    var cell = worksheet.Cells[i, 0]; // column A
    var cv = cell.GetValue(CellValueType.DateTime, DateTimeParseOptions.EnableJapaneseEra);
    string iso = cv.DateTimeValue.ToString("yyyy-MM-dd");
    Console.WriteLine($"Row {i + 1}: {iso}");
}
```

### 3. Εναλλακτική για Μη‑Εποχικές Ημερομηνίες  

Αν ένα κελί περιέχει ήδη μια τυπική συμβολοσειρά ημερομηνίας, ο αναλυτής λειτουργεί ακόμη, αλλά ίσως θέλετε ένα δίχτυ ασφαλείας:

```csharp
CellValue cv = cell.GetValue(CellValueType.DateTime,
    DateTimeParseOptions.EnableJapaneseEra | DateTimeParseOptions.TryParse);
```

Η σημαία `TryParse` αποτρέπει εξαιρέσεις και επιστρέφει την αρχική τιμή αν η μετατροπή αποτύχει.

### 4. Στοιχείο Ώρας  

Αν χρειάζεστε επίσης το μέρος της ώρας, χρησιμοποιήστε `"yyyy-MM-ddTHH:mm:ss"`:

```csharp
string isoDateTime = parsedValue.DateTimeValue.ToString("yyyy-MM-ddTHH:mm:ss");
```

Αυτό δίνει ένα πλήρες χρονικό σήμα ISO 8601 (`2021-05-01T00:00:00`).

## Οπτική Βοήθεια  

![παράδειγμα format datetime to iso](image.png "Παράδειγμα μορφοποίησης datetime σε iso σε C#")

*Alt text:* *παράδειγμα format datetime to iso που δείχνει την έξοδο της κονσόλας*

## Συχνές Ερωτήσεις  

- **Μπορώ να το χρησιμοποιήσω με αρχεία .xls;**  
  Ναι. Το Aspose.Cells υποστηρίζει `.xls`, `.xlsx`, `.csv` και πολλές άλλες μορφές αμέσως.

- **Τι γίνεται αν το workbook είναι προστατευμένο με κωδικό;**  
  Φορτώστε το με `new Workbook("file.xlsx", new LoadOptions { Password = "secret" })`.

- **Είναι η μορφή ISO εξαρτημένη από την τοπική ρύθμιση;**  
  Όχι. Το μοτίβο `"yyyy-MM-dd"` είναι ανεξάρτητο από την κουλτούρα, εγγυώμενο το ίδιο αποτέλεσμα σε οποιονδήποτε υπολογιστή.

- **Λειτουργεί αυτό σε .NET Core;**  
  Απόλυτα—το Aspose.Cells είναι συμβατό με .NET Standard 2.0.

## Συμπέρασμα  

Συζητήσαμε πώς να **format datetime to iso** με **extracting date from excel**, αναλύοντας συμβολοσειρές ιαπωνικής εποχής, και τελικά **displaying iso date** στην κονσόλα. Τα βασικά βήματα—δημιουργία workbook, εγγραφή ή φόρτωση του κειμένου της εποχής, ενεργοποίηση ανάλυσης ιαπωνικής εποχής, και μορφοποίηση με `ToString("yyyy-MM-dd")`—είναι όλα όσα χρειάζεστε για τις περισσότερες περιπτώσεις.

Επόμενα, ίσως θελήσετε να:

- Εγγραφή των ISO ημερομηνιών πίσω σε άλλη στήλη για επεξεργασία downstream.
- Εξαγωγή του μετασχηματισμένου workbook σε CSV για μαζική εισαγωγή.
- Συνδυασμός αυτής της λογικής με ένα web API που δέχεται μεταφορτώσεις Excel και επιστρέφει ISO ημερομηνίες κωδικοποιημένες σε JSON.

Μη διστάσετε να πειραματιστείτε με διαφορετικές μορφές ημερομηνίας, ζώνες ώρας, ή ακόμη και προσαρμοσμένα ημερολόγια. Η ευελιξία του Aspose.Cells σημαίνει ότι σπάνια θα συναντήσετε εμπόδια.

Καλό προγραμματισμό, και εύχομαι όλες οι ημερομηνίες σας να είναι τέλεια συμβατές με ISO!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}