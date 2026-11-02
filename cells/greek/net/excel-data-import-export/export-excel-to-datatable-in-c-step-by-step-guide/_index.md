---
category: general
date: 2026-03-25
description: Μάθετε πώς να εξάγετε το Excel σε DataTable σε C# γρήγορα. Αυτό το σεμινάριο
  καλύπτει την εξαγωγή του Excel με ονόματα στηλών και την εξαγωγή των δεδομένων του
  Excel ως συμβολοσειρά για αξιόπιστη διαχείριση δεδομένων.
draft: false
keywords:
- export excel to datatable
- how to export excel to datatable
- export excel with column names
- export excel data as string
language: el
og_description: Εξαγωγή Excel σε DataTable σε C# με ονόματα στηλών και μετατροπή σε
  συμβολοσειρά. Ακολουθήστε αυτόν τον σύντομο οδηγό για μια έτοιμη προς εκτέλεση λύση.
og_title: Εξαγωγή Excel σε DataTable σε C# – Πλήρης Οδηγός
tags:
- C#
- Aspose.Cells
- DataTable
- Excel
title: Εξαγωγή Excel σε DataTable σε C# – Οδηγός βήμα‑βήμα
url: /el/net/excel-data-import-export/export-excel-to-datatable-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή Excel σε DataTable σε C# – Οδηγός βήμα‑βήμα

Έχετε ποτέ χρειαστεί να **εξάγετε Excel σε DataTable** αλλά δεν ήσασταν σίγουροι ποια flags να ενεργοποιήσετε; Δεν είστε μόνοι—πολλοί προγραμματιστές αντιμετωπίζουν το ίδιο πρόβλημα όταν προσπαθούν για πρώτη φορά να μεταφέρουν δεδομένα φύλλου εργασίας σε ένα `DataTable`.  

Τα καλά νέα; Με λίγες μόνο γραμμές κώδικα μπορείτε να **εξάγετε Excel με ονόματα στηλών** και ακόμη **εξάγετε δεδομένα Excel ως string** για να αποφύγετε προβλήματα ασυμφωνίας τύπων. Παρακάτω θα βρείτε ένα πλήρες, εκτελέσιμο παράδειγμα μαζί με το «γιατί» πίσω από κάθε ρύθμιση, ώστε να το προσαρμόσετε σε οποιοδήποτε έργο χωρίς εικασίες.

## Τι καλύπτει αυτό το σεμινάριο

* Πώς να δημιουργήσετε ένα workbook στη μνήμη (χωρίς φυσικό αρχείο).  
* Γέμισμα με μερικές δείγματες γραμμές ώστε να δείτε το αποτέλεσμα άμεσα.  
* Διαμόρφωση του `ExportTableOptions` ώστε κάθε κελί να αντιμετωπίζεται ως string.  
* Εξαγωγή ενός ορθογωνίου εύρους σε `DataTable` διατηρώντας την πρώτη γραμμή ως ονόματα στηλών.  
* Επαλήθευση του αποτελέσματος και εκτύπωση της πρώτης γραμμής στην κονσόλα.  

Δεν απαιτούνται εξωτερικοί σύνδεσμοι τεκμηρίωσης—ό,τι χρειάζεστε είναι εδώ. Εάν έχετε ήδη ένα αρχείο Excel στο δίσκο, απλώς αντικαταστήστε τη γραμμή δημιουργίας του workbook με `new Workbook("path/to/file.xlsx")` και είστε έτοιμοι.

---

## Βήμα 1: Ρύθμιση του έργου και προσθήκη του πακέτου NuGet Aspose.Cells

Πριν γράψουμε οποιονδήποτε κώδικα, βεβαιωθείτε ότι το έργο σας αναφέρει **Aspose.Cells for .NET** (τη βιβλιοθήκη που τροφοδοτεί την κλάση `Workbook`). Μπορείτε να το προσθέσετε μέσω του NuGet Package Manager:

```bash
dotnet add package Aspose.Cells
```

> **Συμβουλή:** Χρησιμοποιήστε την πιο πρόσφατη σταθερή έκδοση (από Μάρτιο 2026, είναι 22.12) για να λάβετε τις τελευταίες διορθώσεις σφαλμάτων και βελτιώσεις απόδοσης.

---

## Βήμα 2: Δημιουργία Workbook και Συμπλήρωση με Δεδομένα Δείγματος

Θα ξεκινήσουμε με ένα ολοκαίνουργιο `Workbook` και θα γράψουμε μερικές γραμμές ώστε να δείτε την εξαγωγή σε δράση. Αυτό το βήμα δείχνει επίσης **πώς να εξάγετε excel σε datatable** όταν τα δεδομένα προέρχονται μόνο από τη μνήμη.

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a fresh workbook and grab the first worksheet
        Workbook workbook = new Workbook();                 // in‑memory workbook
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Populate a few cells – this mimics a real Excel file
        worksheet.Cells["A1"].PutValue("Name");   // column header
        worksheet.Cells["B1"].PutValue("Age");    // column header
        worksheet.Cells["A2"].PutValue("Alice");
        worksheet.Cells["B2"].PutValue(30);
        worksheet.Cells["A3"].PutValue("Bob");
        worksheet.Cells["B3"].PutValue(25);
```

*Γιατί είναι σημαντικό:* Εισάγοντας πρώτα τη γραμμή κεφαλίδας (`A1` & `B1`), μπορούμε αργότερα να πούμε στον εξαγωγέα να αντιμετωπίζει την πρώτη γραμμή ως ονόματα στηλών—ακριβώς αυτό που σημαίνει **export excel with column names**.

---

## Βήμα 3: Εντολή στο Aspose.Cells να αντιμετωπίζει κάθε κελί ως String

Όταν εξάγετε αριθμητικά ή ημερομηνιακά κελιά, το Aspose προσπαθεί να καταλάβει τον τύπο .NET. Αυτό μπορεί να προκαλέσει λεπτές σφαλματώδεις καταστάσεις εάν ο κώδικάς σας αναμένει strings. Η σημαία `ExportTableOptions.ExportAsString` επιβάλλει ομοιόμορφη μετατροπή σε string.

```csharp
        // 3️⃣ Configure export options – all values will be strings
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true       // <-- ensures Export Excel Data As String
        };
```

*Γιατί να το χρησιμοποιήσετε;* Φανταστείτε μια στήλη που μερικές φορές περιέχει αριθμούς και μερικές φορές κείμενο (π.χ., “00123” vs. “ABC”). Εξάγοντας τα πάντα ως string αποφεύγετε την απώλεια των αρχικών μηδενικών ή την εμφάνιση εξαιρέσεων μετατροπής τύπου.

---

## Βήμα 4: Εξαγωγή του επιθυμητού εύρους σε DataTable

Τώρα πραγματικά **εξάγουμε excel σε datatable**. Η μέθοδος `ExportDataTable` δέχεται τη γραμμή/στήλη έναρξης, τον αριθμό γραμμών/στηλών, μια σημαία για εξαγωγή ονομάτων στηλών, και τις επιλογές που μόλις δημιουργήσαμε.

```csharp
        // 4️⃣ Export rows 0‑9 and columns 0‑4 (adjust as needed)
        DataTable table = worksheet.Cells.ExportDataTable(
            startRow: 0,
            startColumn: 0,
            totalRows: 10,
            totalColumns: 5,
            exportColumnNames: true,   // <-- uses the first row as headers
            exportOptions: exportOptions);
```

*Τι συμβαίνει στο παρασκήνιο;*  
- `startRow: 0` δείχνει στην πρώτη γραμμή του Excel (τη γραμμή κεφαλίδας).  
- `exportColumnNames: true` λέει στο Aspose να μεταφέρει τα “Name” και “Age” στη συλλογή στηλών του `DataTable`.  
- `totalRows`/`totalColumns` μπορούν να είναι μεγαλύτερα από τα πραγματικά δεδομένα· τα επιπλέον κελιά γίνονται κενές συμβολοσειρές λόγω του `ExportAsString`.

---

## Βήμα 5: Επαλήθευση του Αποτελέσματος – Εκτύπωση της Πρώτης Γραμμής

Μια γρήγορη εκτύπωση στην κονσόλα αποδεικνύει ότι η μετατροπή πέτυχε και ότι τα ονόματα στηλών παραμένουν άθικτα.

```csharp
        // 5️⃣ Show the first data row (if any)
        if (table.Rows.Count > 0)
        {
            Console.WriteLine($"First row: {table.Rows[0]["Name"]}, {table.Rows[0]["Age"]}");
        }
        else
        {
            Console.WriteLine("The exported DataTable is empty.");
        }
    }
}
```

**Αναμενόμενη έξοδος**

```
First row: Alice, 30
```

Εάν αλλάξετε τα δείγματα δεδομένων, η κονσόλα θα αντανακλά αυτές τις αλλαγές αυτόματα—χωρίς επιπλέον κώδικα.

---

## Συχνές Ερωτήσεις & Ειδικές Περιπτώσεις

| Ερώτηση | Απάντηση |
|----------|--------|
| **Μπορώ να εξάγω ένα φύλλο που υπάρχει ήδη στο δίσκο;** | Ναι—αντικαταστήστε το `new Workbook()` με `new Workbook("myFile.xlsx")`. Τα υπόλοιπα βήματα παραμένουν ίδια. |
| **Τι γίνεται αν το αρχείο Excel μου έχει συγχωνευμένα κελιά;** | Τα συγχωνευμένα κελιά αποσυμπιέζονται· η τιμή του πάνω‑αριστερού κελιού χρησιμοποιείται για ολόκληρο το συγχωνευμένο εύρος. |
| **Πρέπει να ανησυχήσω για μορφές αριθμών ειδικές για πολιτισμό;** | Όχι όταν `ExportAsString = true`; όλα φτάνουν ως η ακατέργαστη συμβολοσειρά που εμφανίζεται στο Excel. |
| **Πόσες γραμμές μπορώ να εξάγω ταυτόχρονα;** | Το Aspose.Cells μπορεί να διαχειριστεί εκατομμύρια γραμμές, αλλά η κατανάλωση μνήμης αυξάνεται με το μέγεθος του `DataTable`. Σκεφτείτε τη σελιδοποίηση εάν φτάσετε τα όρια. |
| **Τι γίνεται με τις κρυφές στήλες;** | Οι κρυφές στήλες εξάγονται εκτός εάν ορίσετε `ExportHiddenColumns = false` στο `ExportTableOptions`. |

---

## Επιπλέον: Εξαγωγή σε CSV αντί για DataTable

Μερικές φορές μπορεί να προτιμάτε ένα επίπεδο αρχείο. Τα ίδια `ExportTableOptions` μπορούν να επαναχρησιμοποιηθούν με `ExportDataTableToCSV`:

```csharp
        string csvPath = "output.csv";
        worksheet.Cells.ExportDataTableToCSV(
            startRow: 0,
            startColumn: 0,
            totalRows: 10,
            totalColumns: 5,
            csvPath,
            exportColumnNames: true,
            exportOptions);
        Console.WriteLine($"CSV written to {csvPath}");
```

Αυτή η μία γραμμή σας δίνει ένα έτοιμο για εισαγωγή CSV ενώ εξακολουθεί να **εξάγει δεδομένα excel ως string**.

---

## Πλήρες Παράδειγμα Εργασίας (Έτοιμο για Αντιγραφή‑Επικόλληση)

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Populate sample data (header + two rows)
        worksheet.Cells["A1"].PutValue("Name");
        worksheet.Cells["B1"].PutValue("Age");
        worksheet.Cells["A2"].PutValue("Alice");
        worksheet.Cells["B2"].PutValue(30);
        worksheet.Cells["A3"].PutValue("Bob");
        worksheet.Cells["B3"].PutValue(25);

        // Export everything as strings
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true
        };

        // Export range to DataTable (first row = column names)
        DataTable table = worksheet.Cells.ExportDataTable(
            startRow: 0,
            startColumn: 0,
            totalRows: 10,
            totalColumns: 5,
            exportColumnNames: true,
            exportOptions: exportOptions);

        // Display first row
        if (table.Rows.Count > 0)
        {
            Console.WriteLine($"First row: {table.Rows[0]["Name"]}, {table.Rows[0]["Age"]}");
        }
        else
        {
            Console.WriteLine("The exported DataTable is empty.");
        }
    }
}
```

Εκτελέστε το πρόγραμμα (`dotnet run`) και θα δείτε το αποτέλεσμα του **export excel to datatable** να εκτυπώνεται στην κονσόλα. Αντικαταστήστε τα δείγματα δεδομένων, αλλάξτε `totalRows`/`totalColumns`, ή δείξτε το workbook σε ένα πραγματικό αρχείο—όλα κλιμακώνονται.

---

## Συμπέρασμα

Τώρα έχετε μια **πλήρη, αυτόνομη λύση για την εξαγωγή Excel σε DataTable** σε C#. Με τη διαμόρφωση του `ExportTableOptions.ExportAsString` εξασφαλίζετε ότι **εξάγετε δεδομένα excel ως string**, και με τη ρύθμιση `exportColumnNames: true` λαμβάνετε τις γνωστές κεφαλίδες στηλών που περιμένετε όταν **εξάγετε excel με ονόματα στηλών**.  

Από εδώ μπορείτε:

* Τροφοδοτήστε το `DataTable` στο Entity Framework ή Dapper για μαζικές εισαγωγές.  
* Περάστε το σε μια μηχανή αναφορών όπως **FastReport** ή **RDLC**.  
* Μετατρέψτε το σε JSON για απάντηση API (`JsonConvert.SerializeObject(table)`).  

Νιώστε ελεύθεροι να πειραματιστείτε—ίσως δοκιμάσετε την εξαγωγή ενός μεγαλύτερου φύλλου, ή συνδυάστε αυτό με **how to export excel to datatable** από κοινόχρηστο δίκτυο. Το μοτίβο παραμένει το ίδιο, και ο κώδικας είναι έτοιμος για παραγωγή.

![Διάγραμμα ροής μετατροπής Excel → DataTable – export excel to datatable](https://example.com/placeholder.png "διάγραμμα export excel to datatable")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}