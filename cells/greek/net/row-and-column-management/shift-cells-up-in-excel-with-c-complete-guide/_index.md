---
category: general
date: 2026-07-13
description: Μετακινήστε τα κελιά προς τα πάνω στο Excel χρησιμοποιώντας C#. Μάθετε
  πώς να αφαιρέσετε τις πρώτες γραμμές, να διαγράψετε πολλαπλές γραμμές και να αφαιρέσετε
  γραμμές από πίνακα σε μια ενιαία, ασφαλή λειτουργία.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- shift cells up
- remove first rows
- remove rows from table
- delete multiple rows
- how to delete rows
language: el
lastmod: 2026-07-13
og_description: Μετακινήστε τα κελιά προς τα πάνω σε ένα φύλλο εργασίας του Excel
  χρησιμοποιώντας C#. Αυτό το σεμινάριο δείχνει πώς να αφαιρέσετε τις πρώτες γραμμές,
  να διαγράψετε πολλαπλές γραμμές και να αφαιρέσετε με ασφάλεια γραμμές από πίνακα.
og_image_alt: Screenshot of C# code that shifts cells up after deleting rows in an
  Excel worksheet
og_title: Μετακίνηση κελιών προς τα πάνω στο Excel με C# – Πλήρης οδηγός προγραμματισμού
schemas:
- author: Aspose
  dateModified: '2026-07-13'
  description: Shift cells up in Excel using C#. Learn how to remove first rows, delete
    multiple rows, and remove rows from table in a single, safe operation.
  headline: Shift Cells Up in Excel with C# – Complete Guide
  type: TechArticle
- questions:
  - answer: Absolutely. Loop through `sheet.Cells.Rows` and call `DeleteRows(rowIndex,
      1, true)` whenever the condition matches. Just remember to iterate backwards
      to avoid index shifting.
    question: Can I delete rows based on a condition instead of a fixed index?
  - answer: Yes. Aspose.Cells supports both `.xlsx` and legacy `.xls` formats. The
      same API applies.
    question: Does this work with `.xls` files?
  - answer: 'Target the specific table by name: `Table myTable = sheet.Tables["MyTable"];`
      then use `myTable.Range.StartRow` to calculate the rows to delete. --- ## Full
      Working Example Below is the complete, ready‑to‑run program that incorporates
      everything we discussed. Copy‑paste it into a console app, adjust'
    question: What if my workbook contains multiple tables and I only want to affect
      one?
  type: FAQPage
tags:
- Aspose.Cells
- C#
- Excel automation
title: Μετακίνηση κελιών προς τα πάνω στο Excel με C# – Πλήρης οδηγός
url: /el/net/row-and-column-management/shift-cells-up-in-excel-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Μετακίνηση Κελιών Πάνω σε Excel με C# – Πλήρης Οδηγός

Έχετε αναρωτηθεί ποτέ πώς να **μετακινήσετε τα κελιά προς τα πάνω** μετά τη διαγραφή γραμμών σε ένα αρχείο Excel; Δεν είστε οι μόνοι. Είτε καθαρίζετε εισαγόμενα δεδομένα είτε περικόπτετε μια τεράστια αναφορά, η δυνατότητα αφαίρεσης των πρώτων γραμμών χωρίς να σπάσει ένας πίνακας είναι απαραίτητη δεξιότητα για κάθε προγραμματιστή C#.

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από μια πρακτική, ολοκληρωμένη λύση που δείχνει **πώς να διαγράψετε γραμμές**, να διατηρήσετε την κεφαλίδα αμετάβλητη και να μετακινήσετε αυτόματα τα υπόλοιπα κελιά προς τα πάνω. Στο τέλος θα μπορείτε να **αφαιρέσετε γραμμές από πίνακα**, **διαγράψετε πολλαπλές γραμμές** και **αφαιρέσετε τις πρώτες γραμμές** με λίγες μόνο γραμμές κώδικα.

---

## Τι Θα Χρειαστείτε

- .NET 6+ (ή .NET Framework 4.7.2 και νεότερο)  
- Η βιβλιοθήκη **Aspose.Cells for .NET** (δωρεάν δοκιμή ή με άδεια)  
- Βασική κατανόηση του C# και του Visual Studio (ή οποιουδήποτε IDE προτιμάτε)  

Καμία άλλη εξάρτηση — μόνο το πακέτο NuGet και ένα αρχείο Excel για πειραματισμό.

---

## Βήμα 1: Εγκατάσταση Aspose.Cells

Πρώτα απ’ όλα, προσθέστε το πακέτο Aspose.Cells στο έργο σας:

```bash
dotnet add package Aspose.Cells
```

Αυτή η μιά γραμμή φέρνει όλα όσα χρειάζεστε για εργασία με βιβλία εργασίας, φύλλα εργασίας και πίνακες. Αν χρησιμοποιείτε Visual Studio, μπορείτε επίσης να κάνετε δεξί‑κλικ στο έργο → **Manage NuGet Packages** → αναζητήστε *Aspose.Cells* και κάντε κλικ στο **Install**.

*Συμβουλή:* Χρησιμοποιήστε την πιο πρόσφατη σταθερή έκδοση· από τον Ιούλιο 2026 είναι η **23.9.0**, η οποία υποστηρίζει τις πιο νέες μορφές αρχείων Excel.

---

## Βήμα 2: Φόρτωση του Workbook που Περιέχει τον Πίνακα

Τώρα θα ανοίξουμε το αρχείο Excel που περιέχει τα δεδομένα που θέλετε να καθαρίσετε. Αντικαταστήστε το `YOUR_DIRECTORY` με τη σωστή διαδρομή στον υπολογιστή σας.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load the workbook that contains the table
        Workbook workbook = new Workbook(@"C:\Data\table.xlsx");
        
        // Grab the first worksheet (index 0)
        Worksheet sheet = workbook.Worksheets[0];
        
        // Optional: get a reference to the first table for context
        Table table = sheet.Tables[0];
```

Σε αυτό το σημείο έχουμε ένα αντικείμενο `Worksheet` έτοιμο για επεξεργασία. Παρατηρήστε ότι δεν έχουμε αγγίξει ακόμη τον πίνακα — η διατήρηση της κεφαλίδας είναι κρίσιμη όταν αργότερα **μετακινήσουμε τα κελιά προς τα πάνω**.

---

## Βήμα 3: Διαγραφή των Πρώτων Δύο Γραμμών Με Μετακίνηση Κελιών Πάνω

Αυτή είναι η ουσία: διαγραφή γραμμών *και* αυτόματη μετακίνηση των κελιών που βρίσκονται κάτω. Η Aspose.Cells παρέχει τη μέθοδο `DeleteRows` που κάνει ακριβώς αυτό όταν περάσετε `true` για τη σημαία `shiftCellsUp`.

```csharp
        // Delete the first two rows (row index starts at 0)
        // The third argument ‑‑> true tells Aspose.Cells to shift cells up.
        sheet.Cells.DeleteRows(0, 2, true);
```

### Γιατί είναι σημαντική η σημαία `true`

Αν παραλείψετε τη σημαία `true`, οι γραμμές διαγράφονται αλλά ο χώρος που κατείχαν παραμένει κενός, δημιουργώντας κενά στα δεδομένα σας. Ορίζοντάς την σε **true** λέτε στη βιβλιοθήκη να συμπτύξει την περιοχή, μετακινώντας **τα κελιά προς τα πάνω** έτσι ώστε η γραμμή 3 να γίνει η νέα γραμμή 1. Αυτός είναι ο πιο καθαρός τρόπος για **αφαίρεση των πρώτων γραμμών** χωρίς να σπάσουν τύποι ή δομές πίνακα.

> **Σημαντικό:** Η διαγραφή γραμμών που περιλαμβάνουν την κεφαλίδα του πίνακα θα προκαλέσει εξαίρεση. Διατηρήστε την κεφαλίδα (συνήθως γραμμή 0) αμετάβλητη ή διαγράψτε την ξεχωριστά αφού ξαναδημιουργήσετε την κεφαλίδα του πίνακα.

---

## Βήμα 4: Επαλήθευση ότι ο Πίνακας Παραμένει Σωστός

Μετά τη διαγραφή, είναι καλή ιδέα να ελέγξετε ξανά ότι η αναφορά του πίνακα δείχνει ακόμη στη σωστή περιοχή. Μπορείτε να εκτυπώσετε τη διεύθυνση του πίνακα ή να την ανανεώσετε:

```csharp
        // Refresh the table range to reflect the new data area
        table.Refresh();

        // Output the new range for debugging
        Console.WriteLine($"Table now spans: {table.Ref}");
```

Η εκτέλεση του προγράμματος θα πρέπει να εμφανίσει κάτι όπως `Table1!A1:D8` αντί του αρχικού `A1:D10`, επιβεβαιώνοντας ότι οι γραμμές αφαιρέθηκαν και τα κελιά μετακινήθηκαν προς τα πάνω.

---

## Βήμα 5: Αποθήκευση του Τροποποιημένου Workbook

Τέλος, γράψτε τις αλλαγές πίσω στο δίσκο. Μπορείτε να αντικαταστήσετε το αρχικό αρχείο ή να δημιουργήσετε ένα νέο αντίγραφο — όπως προτιμάτε.

```csharp
        // Save the workbook with the changes
        workbook.Save(@"C:\Data\modified_table.xlsx");
    }
}
```

Ανοίξτε το `modified_table.xlsx` στο Excel και θα δείτε ότι οι πρώτες δύο γραμμές έχουν αφαιρεθεί, οι υπόλοιπες γραμμές έχουν μετακινηθεί προς τα πάνω και ο πίνακας παραμένει αμετάβλητος. Η λειτουργία αυτή έχει ουσιαστικά **διαγράψει πολλαπλές γραμμές** διατηρώντας την ακεραιότητα των δεδομένων.

---

## Ακραίες Περιπτώσεις & Συνηθισμένα Πιθανά Σφάλματα

| Κατάσταση | Τι Συμβαίνει | Πώς να το Διαχειριστείτε |
|-----------|--------------|--------------------------|
| **Η γραμμή κεφαλίδας είναι μέρος της περιοχής διαγραφής** | Η Aspose.Cells ρίχνει `InvalidOperationException` επειδή ένας πίνακας δεν μπορεί να χάσει την κεφαλίδα του. | Διαγράψτε μόνο τις γραμμές δεδομένων ή ξαναδημιουργήστε την κεφαλίδα μετά τη διαγραφή χρησιμοποιώντας `sheet.Cells["A1"].PutValue("Header")`. |
| **Ο πίνακας εκτείνεται σε πολλά φύλλα εργασίας** | Η διαγραφή γραμμών σε ένα φύλλο δεν επηρεάζει τα άλλα. | Επανάληψη (iterate) σε κάθε πίνακα του φύλλου εάν χρειάζεται καθαρισμός σε όλο το βιβλίο. |
| **Μεγάλα αρχεία (>100 MB)** | Η χρήση μνήμης αυξάνεται δραματικά. | Χρησιμοποιήστε `LoadOptions` με `MemoryPreference` ορισμένο σε `MemoryPreference.MemoryOnly` για μείωση του αποτυπώματος RAM. |
| **Πρέπει να διατηρήσετε τύπους που αναφέρονται στις διαγραμμένες γραμμές** | Οι τύποι μπορεί να γίνουν `#REF!`. | Χρησιμοποιήστε `sheet.Cells.DeleteRows(startRow, count, true, true)` — το τέταρτο όρισμα ενημερώνει τις φόρμουλες. |

---

## Συχνές Ερωτήσεις

**Ε: Μπορώ να διαγράψω γραμμές βάσει συνθήκης αντί για σταθερό δείκτη;**  
Α: Φυσικά. Διασχίστε το `sheet.Cells.Rows` και καλέστε `DeleteRows(rowIndex, 1, true)` όποτε η συνθήκη ισχύει. Θυμηθείτε να κάνετε την επανάληψη προς τα πίσω ώστε να μην μετατοπιστούν οι δείκτες.

**Ε: Λειτουργεί αυτό με αρχεία `.xls`;**  
Α: Ναι. Η Aspose.Cells υποστηρίζει τόσο μορφές `.xlsx` όσο και τις παλαιότερες `.xls`. Το ίδιο API ισχύει.

**Ε: Τι γίνεται αν το βιβλίο εργασίας μου περιέχει πολλαπλούς πίνακες και θέλω να επηρεάσω μόνο έναν;**  
Α: Στοχεύστε τον συγκεκριμένο πίνακα με το όνομα: `Table myTable = sheet.Tables["MyTable"];` και χρησιμοποιήστε `myTable.Range.StartRow` για να υπολογίσετε τις γραμμές που θα διαγραφούν.

---

## Πλήρες Παράδειγμα Εφαρμογής

Παρακάτω βρίσκεται το ολοκληρωμένο, έτοιμο‑για‑εκτέλεση πρόγραμμα που ενσωματώνει όλα όσα συζητήσαμε. Αντιγράψτε‑και‑επικολλήστε το σε μια εφαρμογή console, προσαρμόστε τις διαδρομές αρχείων και πατήστε **F5**.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the workbook
        Workbook workbook = new Workbook(@"C:\Data\table.xlsx");
        Worksheet sheet = workbook.Worksheets[0];

        // 2️⃣ (Optional) Reference the first table for context
        Table table = sheet.Tables[0];

        // 3️⃣ Delete the first two rows and shift cells up
        //    Row index starts at 0, delete 2 rows, shift up = true
        sheet.Cells.DeleteRows(0, 2, true);

        // 4️⃣ Refresh the table range so it reflects the new data area
        table.Refresh();

        // 5️⃣ Show the new table reference (useful for debugging)
        Console.WriteLine($"Table now spans: {table.Ref}");

        // 6️⃣ Save the modified workbook
        workbook.Save(@"C:\Data\modified_table.xlsx");

        Console.WriteLine("Rows removed and cells shifted up successfully!");
    }
}
```

**Αναμενόμενο αποτέλεσμα:**  
- Οι γραμμές 1‑2 εξαφανίζονται από το φύλλο.  
- Η γραμμή 3 γίνεται η νέα γραμμή 1, η γραμμή 4 γίνεται γραμμή 2 κ.ο.κ.  
- Η περιοχή του πίνακα ενημερώνεται αυτόματα, επιβεβαιώνοντας ότι η **μετακίνηση κελιών προς τα πάνω** λειτούργησε όπως προβλέπεται.

---

## Συμπέρασμα

Συζητήσαμε πώς να **μετακινήσετε κελιά προς τα πάνω** σε ένα φύλλο Excel χρησιμοποιώντας C#. Εκμεταλλευόμενοι τη μέθοδο `DeleteRows` της Aspose.Cells με τη σημαία `true`, μπορείτε με ασφάλεια να **αφαιρέσετε τις πρώτες γραμμές**, **διαγράψετε πολλαπλές γραμμές** και **αφαιρέσετε γραμμές από πίνακα** χωρίς να σπάσει το μοντέλο δεδομένων σας. Η προσέγγιση είναι γρήγορη, αξιόπιστη και λειτουργεί σε όλες τις σύγχρονες μορφές Excel.

Έτοιμοι για το επόμενο βήμα; Δοκιμάστε να συνδυάσετε αυτήν την τεχνική με ένα φιλτράρισμα βάσει συνθήκης για να απομακρύνετε γραμμές που περιέχουν κενά ή διπλότυπα. Ή εξερευνήστε τα APIs στυλ της Aspose.Cells για να επαναεφαρμόσετε μορφοποίηση μετά τη μετακίνηση. Ο ουρανός είναι το όριο όταν κυριαρχείτε τη διαχείριση γραμμών στο Excel.

Έχετε ερωτήσεις ή ένα ενδιαφέρον use‑case που θέλετε να μοιραστείτε; Αφήστε ένα σχόλιο παρακάτω, και καλή προγραμματιστική!

## Τι Θα Μάθετε Στη Σειρά;

Οι παρακάτω οδηγίες καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετα χαρακτηριστικά του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στα δικά σας έργα.

- [Διαγραφή Πολλαπλών Γραμμών σε Excel με Aspose.Cells .NET&#58; Ένας Πλήρης Οδηγός για Διαχείριση Δεδομένων](/cells/english/net/data-manipulation/delete-rows-excel-aspose-cells-net/)
- [Πώς να Εισάγετε και να Διαγράψετε Γραμμές σε Excel με Aspose.Cells για .NET&#58; Ένας Πλήρης Οδηγός](/cells/english/net/data-manipulation/aspose-cells-net-insert-delete-excel-rows/)
- [Πώς να Διαγράψετε Κενές Γραμμές σε Excel Χρησιμοποιώντας Aspose.Cells .NET για Καθαρισμό Δεδομένων](/cells/english/net/data-manipulation/delete-blank-rows-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}