---
category: general
date: 2026-07-13
description: Πώς να εξάγετε μια περιοχή κελιών ως πίνακα χρησιμοποιώντας C# και ExportTableOptions.
  Μάθετε βήμα‑προς‑βήμα τη ρύθμιση του βιβλίου εργασίας, τη μορφοποίηση και την εξαγωγή
  του πίνακα.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export cell range as table
- ExportTableOptions usage
- Workbook and Worksheet handling
- cell value formatting C#
- scientific notation export
language: el
lastmod: 2026-07-13
og_description: Πώς να εξάγετε μια περιοχή κελιών ως πίνακα σε C# με ExportTableOptions.
  Ακολουθήστε αυτόν τον οδηγό για να μορφοποιήσετε τα κελιά, να δημιουργήσετε ένα
  βιβλίο εργασίας και να εξάγετε έναν πίνακα χωρίς κόπο.
og_image_alt: Diagram illustrating a C# code snippet that exports a single cell range
  as a formatted table
og_title: Πώς να εξάγετε μια περιοχή κελιών ως πίνακα – Πλήρης οδηγός C#
schemas:
- author: Aspose
  dateModified: '2026-07-13'
  description: How to export cell range as table using C# and ExportTableOptions.
    Learn step‑by‑step workbook setup, formatting, and table export.
  headline: How to Export Cell Range as Table – Complete C# Guide
  type: TechArticle
tags:
- C#
- Aspose.Cells
- Excel automation
- data export
title: Πώς να εξάγετε την περιοχή κελιών ως πίνακα – Πλήρης οδηγός C#
url: /el/net/excel-data-export-retrieval/how-to-export-cell-range-as-table-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Εξάγετε Περιοχή Κελιών ως Πίνακα – Πλήρης Οδηγός C#

Έχετε αναρωτηθεί ποτέ **πώς να εξάγετε περιοχή κελιών ως πίνακα** χωρίς να τριβάτε τα μαλλιά σας εξαιτίας των ιδιοτήτων μορφοποίησης; Δεν είστε ο μόνος. Είτε τροφοδοτείτε δεδομένα σε μια αλυσίδα αναφορών είτε χρειάζεστε απλώς μια γρήγορη εξαγωγή τύπου CSV, η εξοικείωση με τη διαδικασία εξαγωγής μπορεί να σας εξοικονομήσει ώρες χειροκίνητης αντιγραφής‑επικόλλησης.

Σε αυτόν τον οδηγό θα περάσουμε βήμα‑βήμα τις ακριβείς ενέργειες για να πάρουμε ένα αριθμητικό κελί, να εφαρμόσουμε επιστημονική σημειογραφία και να το εξάγουμε ως πίνακα χρησιμοποιώντας το **ExportTableOptions**. Στο τέλος θα έχετε ένα εκτελέσιμο απόσπασμα κώδικα, θα κατανοήσετε το *γιατί* κάθε κλήση, και θα ξέρετε πώς να προσαρμόσετε τον κώδικα για μεγαλύτερες περιοχές ή διαφορετικές μορφές.

## Προαπαιτούμενα

- .NET 6 ή νεότερο (το API λειτουργεί το ίδιο στο .NET Framework 4.7+)
- Aspose.Cells for .NET εγκατεστημένο (`Install-Package Aspose.Cells`)
- Βασική κατανόηση της σύνταξης C#· δεν απαιτούνται βαθιές γνώσεις εσωτερικής λειτουργίας του Excel

Τα έχετε; Τέλεια—ας βουτήξουμε.

## Βήμα 1: Ρύθμιση Επιλογών Εξαγωγής – Πώς να Εξάγετε Περιοχή Κελιών ως Πίνακα

Το πρώτο πράγμα που χρειάζεστε είναι μια παρουσία του **ExportTableOptions** που λέει στη βιβλιοθήκη πώς να χειριστεί το περιεχόμενο των κελιών. Χωρίς αυτό, η εξαγωγή προεπιλέγει ακατέργαστες αριθμητικές τιμές, κάτι που μπορεί να διακόψει τους καταναλωτές που αναμένουν κείμενο.

```csharp
// Step 1: Define export options – export the cell value as a formatted string
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,          // Return the cell content as text
    CustomFormat = "0.00E+00"       // Apply scientific notation format
};
```

**Γιατί είναι σημαντικό:**  
- `ExportAsString = true` αναγκάζει τη βιβλιοθήκη να γράψει το εμφανιζόμενο κείμενο του κελιού, όχι το υποκείμενο double.  
- `CustomFormat` σας επιτρέπει να επιβάλετε μια **εξαγωγή επιστημονικής σημειογραφίας**, χρήσιμη όταν εργάζεστε με πολύ μεγάλους ή πολύ μικρούς αριθμούς.

> **Συμβουλή:** Εάν χρειάζεστε μορφή ημερομηνίας ή νομίσματος, αντικαταστήστε το `"0.00E+00"` με `"yyyy‑MM‑dd"` ή `"$#,##0.00"` αντίστοιχα.

## Βήμα 2: Δημιουργία Workbook και Λήψη του Πρώτου Worksheet – Διαχείριση Workbook και Worksheet

Ένα **Workbook** αντιπροσωπεύει ολόκληρο το αρχείο Excel, ενώ ένα **Worksheet** είναι μια μεμονωμένη καρτέλα. Για μια απλή εξαγωγή θα χρησιμοποιήσουμε το πρώτο φύλλο, το οποίο είναι πάντα παρόν στον δείκτη 0.

```csharp
// Step 2: Create a new workbook and access the first worksheet
Workbook workbook = new Workbook();
Worksheet sheet = workbook.Worksheets[0];
```

**Γιατί είναι σημαντικό:**  
Η δημιουργία ενός νέου `Workbook` εξασφαλίζει καθαρό ξεκίνημα—χωρίς κρυφά στυλ ή υπολειπόμενα δεδομένα που θα σας μπλοκάρουν. Η πρόσβαση στο `Worksheets[0]` είναι ο πιο γρήγορος τρόπος να αποκτήσετε χειριστήριο του ενεργού φύλλου χωρίς να ανησυχείτε για τα ονόματα των φύλλων.

## Βήμα 3: Συμπλήρωση του Στόχου Κελιού – Μορφοποίηση Τιμής Κελιού C#

Τώρα εισάγουμε μια αριθμητική τιμή στο κελί **A1** (γραμμή 0, στήλη 0). Η τιμή που επιλέγουμε είναι σκόπιμα με πολλούς δεκαδικούς ώστε να δείτε τη επιστημονική σημειογραφία σε δράση.

```csharp
// Step 3: Insert a numeric value into cell A1 (row 0, column 0)
sheet.Cells[0, 0].PutValue(12345.6789);
```

**Γιατί είναι σημαντικό:**  
Η κλήση `PutValue` αυτόματα καθορίζει τον τύπο δεδομένων του κελιού. Επειδή αργότερα εξάγουμε ως συμβολοσειρά, το ακατέργαστο double θα μετατραπεί χρησιμοποιώντας τη μορφή που ορίσαμε νωρίτερα, δίνοντάς μας μια καθαρή έξοδο `"1.23E+04"`.

## Βήμα 4: Εξαγωγή της Ορισμένης Περιοχής Κελιών ως Πίνακα – Εξαγωγή της Περιοχής Κελιών ως Πίνακα

Με τις επιλογές και τα δεδομένα στη θέση τους, το τελευταίο βήμα είναι να πούμε στο Aspose.Cells να γράψει την περιοχή. Η μέθοδος `ExportTable` αναμένει τη γραμμή/στήλη εκκίνησης, το μέγεθος της περιοχής και το αντικείμενο επιλογών που δημιουργήσαμε.

```csharp
// Step 4: Export the defined cell range as a table using the options above
// Parameters: startRow, startColumn, totalRows, totalColumns, options
sheet.ExportTable(0, 0, 1, 1, exportOptions);
```

**Γιατί είναι σημαντικό:**  
- `totalRows = 1` και `totalColumns = 1` περιορίζουν την εξαγωγή σε ένα μόνο κελί, αλλά μπορείτε να επεκτείνετε αυτούς τους αριθμούς για μεγαλύτερα μπλοκ (π.χ., `5, 3` για περιοχή 5‑γραμμών × 3‑στηλών).  
- Η μέθοδος γράφει τα δεδομένα σε μια εσωτερική δομή πίνακα που μπορεί να αποθηκευτεί ως CSV, HTML ή ακόμη και να ροή αμέσως σε έναν πελάτη.

### Αποθήκευση του Αποτελέσματος (Προαιρετικό)

Εάν θέλετε να αποθηκεύσετε τον εξαγόμενο πίνακα στο δίσκο, μπορείτε να τον γράψετε σε αρχείο CSV:

```csharp
// Optional: Save the exported table as CSV for verification
using (var stream = new MemoryStream())
{
    sheet.ExportTableToCSV(stream, exportOptions);
    File.WriteAllBytes("ExportedTable.csv", stream.ToArray());
}
```

Η εκτέλεση του παραπάνω θα δημιουργήσει ένα αρχείο που περιέχει:

```
1.23E+04
```

## Περιπτώσεις Άκρων & Συνηθισμένες Παραλλαγές

| Situation | What to Change | Reason |
|-----------|----------------|--------|
| **Εξαγωγή πολλαπλών γραμμών** | Ρυθμίστε το `totalRows` και κάντε βρόχο στις γραμμές αν χρειάζεται | Επιτρέπει εξαγωγή σε παρτίδες χωρίς επαναλαμβανόμενη κλήση του `ExportTable` |
| **Διατήρηση τύπων** | Ορίστε `ExportAsString = false` | Διατηρεί τον αρχικό τύπο αντί για την εμφανιζόμενη τιμή |
| **Διαφορετικοί διαχωριστές** | Χρησιμοποιήστε την υπερφόρτωση `ExportTableToCSV(..., ',', ...)` | Αλλάζει από τιμές διαχωρισμένες με κόμμα σε τιμές διαχωρισμένες με tab ή pipe |
| **Μεγάλα worksheets** | Ροή εξαγωγής για αποφυγή `OutOfMemoryException` | Λειτουργεί καλά για >10 000 γραμμές |

## Πλήρες Παράδειγμα Εργασίας

Παρακάτω βρίσκεται το πλήρες πρόγραμμα, έτοιμο για αντιγραφή‑και‑επικόλληση. Συγκεντρώνεται με οποιοδήποτε .NET κονσολικό έργο που αναφέρει το Aspose.Cells.

```csharp
using System;
using System.IO;
using Aspose.Cells;

class ExportCellRangeDemo
{
    static void Main()
    {
        // 1️⃣ Define export options – how to export cell range as table
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            CustomFormat = "0.00E+00"
        };

        // 2️⃣ Create workbook and get first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // 3️⃣ Put a numeric value into A1
        sheet.Cells[0, 0].PutValue(12345.6789);

        // 4️⃣ Export the single‑cell range as a table
        sheet.ExportTable(0, 0, 1, 1, exportOptions);

        // Optional: write to CSV to see the result
        using (var ms = new MemoryStream())
        {
            sheet.ExportTableToCSV(ms, exportOptions);
            File.WriteAllBytes("ExportedTable.csv", ms.ToArray());
        }

        Console.WriteLine("Export complete! Check ExportedTable.csv");
    }
}
```

**Αναμενόμενη έξοδος:**  
Ένα αρχείο με όνομα `ExportedTable.csv` που περιέχει μια μόνο γραμμή:

```
1.23E+04
```

Αν ανοίξετε το CSV σε έναν επεξεργαστή κειμένου, θα δείτε την επιστημονική σημειογραφία να εφαρμόζεται ακριβώς όπως ορίστηκε.

## Συμπέρασμα

Καλύψαμε **πώς να εξάγετε περιοχή κελιών ως πίνακα** από την αρχή μέχρι το τέλος: ρύθμιση του `ExportTableOptions`, δημιουργία ενός `Workbook`, εισαγωγή δεδομένων και τέλος κλήση του `ExportTable`. Κατανοώντας κάθε μέρος, μπορείτε τώρα να κλιμακώσετε την προσέγγιση σε μεγαλύτερες περιοχές, διαφορετικές μορφές ή ακόμη και να την ενσωματώσετε σε ένα web API που εξυπηρετεί δεδομένα προερχόμενα από Excel σε πραγματικό χρόνο.

Κοιτάζοντας μπροστά, ίσως θέλετε να εξερευνήσετε:

- **ExportTableToHTML** για προεπισκοπήσεις έτοιμες για web  
- **ExportTableToDataTable** για άμεση τροφοδοσία σε pipelines ADO.NET  
- Προηγμένες **custom formats** για ημερομηνίες, νομίσματα ή ποσοστά  

Δοκιμάστε τα, και θα μετατρέψετε μια απλή εξαγωγή κελιού σε μια ευέλικτη μηχανή παροχής δεδομένων. Έχετε ερωτήσεις ή μια ιδιόρρυθμη περίπτωση χρήσης; Αφήστε ένα σχόλιο παρακάτω—καλή προγραμματιστική!

## Τι Θα Πρέπει Να Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να Εξάγετε Ορατές Γραμμές Excel Χρησιμοποιώντας Aspose.Cells για .NET: Οδηγός Βήμα‑Βήμα](/cells/english/net/workbook-operations/export-visible-rows-aspose-cells-dotnet/)
- [Πώς να Εξάγετε Αρχεία Excel σε .NET Χρησιμοποιώντας Aspose.Cells: Αναλυτικός Οδηγός](/cells/english/net/workbook-operations/export-excel-files-net-aspose-cells-guide/)
- [Πώς να Πρόσβαση σε Κελί Excel με Όνομα Χρησιμοποιώντας Aspose.Cells για .NET: Οδηγός Βήμα‑Βήμα](/cells/english/net/cell-operations/access-cell-by-name-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}