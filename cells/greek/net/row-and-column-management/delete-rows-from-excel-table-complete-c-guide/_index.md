---
category: general
date: 2026-08-07
description: Διαγραφή γραμμών από πίνακα Excel χρησιμοποιώντας C#. Μάθετε πώς να αφαιρείτε
  με ασφάλεια γραμμές δεδομένων στο Excel, προστατεύοντας ταυτόχρονα τη γραμμή κεφαλίδας,
  σε λίγα μόνο βήματα.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- delete rows from excel table
- remove data rows excel
- protect header row excel
language: el
lastmod: 2026-08-07
og_description: Διαγραφή γραμμών από πίνακα Excel προγραμματιστικά. Αυτός ο οδηγός
  δείχνει πώς να αφαιρέσετε με ασφάλεια γραμμές δεδομένων στο Excel και να προστατεύσετε
  τη γραμμή κεφαλίδας στο Excel με το Aspose.Cells.
og_image_alt: Screenshot of C# code that deletes rows from an Excel table while keeping
  the header intact
og_title: Διαγραφή γραμμών από πίνακα Excel – γρήγορη λύση C#
schemas:
- author: Aspose
  dateModified: '2026-08-07'
  description: Delete rows from Excel table using C#. Learn how to remove data rows
    Excel safely while protecting header row Excel in just a few steps.
  headline: Delete rows from Excel table – complete C# guide
  type: TechArticle
- description: Delete rows from Excel table using C#. Learn how to remove data rows
    Excel safely while protecting header row Excel in just a few steps.
  name: Delete rows from Excel table – complete C# guide
  steps:
  - name: Run the program with a sample workbook that has at least five data rows.
    text: Run the program with a sample workbook that has at least five data rows.
  - name: Verify that the console prints “Rows deleted and workbook saved successfully.”
    text: Verify that the console prints “Rows deleted and workbook saved successfully.”
  - name: 'Open `TableHeaderProtected.xlsx` in Excel and confirm:'
    text: 'Open `TableHeaderProtected.xlsx` in Excel and confirm:'
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
- Data manipulation
title: Διαγραφή γραμμών από πίνακα Excel – πλήρης οδηγός C#
url: /el/net/row-and-column-management/delete-rows-from-excel-table-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Διαγραφή γραμμών από πίνακα Excel – πλήρης οδηγός C#

Αν χρειάζεστε να **διαγράψετε γραμμές από πίνακα Excel** σε ένα έργο .NET, αυτό το tutorial σας δείχνει έναν αξιόπιστο τρόπο για να το κάνετε. Είτε καθαρίζετε εισαγόμενα δεδομένα είτε μειώνετε ένα αναφορά, θα δείτε πώς να αφαιρέσετε γραμμές δεδομένων Excel ενώ το API αυτόματα **protect header row excel** από τυχαία διαγραφή.

Στα παρακάτω βήματα θα μάθετε πώς να φορτώσετε ένα βιβλίο εργασίας, να διαγράψετε γραμμές με ασφάλεια και τελικά να αποθηκεύσετε τις αλλαγές. Ο οδηγός καλύπτει επίσης το συνηθισμένο λάθος του προσπαθώντας να διαγράψετε τη γραμμή κεφαλίδας και εξηγεί γιατί η βιβλιοθήκη το αποτρέπει. Στο τέλος θα μπορείτε να **remove data rows excel** με σιγουριά σε οποιαδήποτε λύση βασισμένη στο Aspose.Cells.

## Προαπαιτούμενα

- .NET 6.0 ή νεότερη έκδοση εγκατεστημένη.
- Το πακέτο NuGet **Aspose.Cells for .NET** (έκδοση 23.10 ή νεότερη). Εγκαταστήστε το με:

  ```bash
  dotnet add package Aspose.Cells
  ```

- Ένα αρχείο Excel (`TableWithHeader.xlsx`) που περιέχει έναν δομημένο πίνακα με γραμμή κεφαλίδας στο πρώτο φύλλο εργασίας.
- Βασική εξοικείωση με C# και Visual Studio (ή οποιοδήποτε IDE προτιμάτε).

## Βήμα 1: Φόρτωση του βιβλίου εργασίας που περιέχει πίνακα με γραμμή κεφαλίδας

Η πρώτη ενέργεια είναι το άνοιγμα του βιβλίου εργασίας που περιέχει τον πίνακα που θέλετε να τροποποιήσετε. Το Aspose.Cells διαβάζει το αρχείο στη μνήμη χωρίς να απαιτείται η εγκατάσταση του Excel.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Load the workbook from disk
        Workbook workbook = new Workbook(@"YOUR_DIRECTORY\TableWithHeader.xlsx");

        // Continue with the next steps...
```

**Γιατί είναι σημαντικό:** Η φόρτωση του βιβλίου εργασίας δημιουργεί ένα αντικείμενο `Workbook` που σας δίνει πρόσβαση σε φύλλα εργασίας, πίνακες και κελιά. Χωρίς αυτό το αντικείμενο δεν μπορείτε να χειριστείτε τη δομή του Excel.

## Βήμα 2: Πρόσβαση στο πρώτο φύλλο εργασίας και στον πρώτο του πίνακα

Στα πιο απλά παραδείγματα ο πίνακας βρίσκεται στο πρώτο φύλλο εργασίας και στον δείκτη 0, αλλά μπορείτε να προσαρμόσετε τους δείκτες ανάλογα με την περίπτωσή σας.

```csharp
        // Access the first worksheet (index 0)
        Worksheet worksheet = workbook.Worksheets[0];

        // Retrieve the first ListObject (Excel table) on that worksheet
        ListObject table = worksheet.Tables[0];
```

**Γιατί είναι σημαντικό:** Το `ListObject` αντιπροσωπεύει έναν πίνακα Excel, ο οποίος περιλαμβάνει τη γραμμή κεφαλίδας, τις γραμμές δεδομένων και τυχόν μορφοποίηση. Η εργασία με το αντικείμενο πίνακα εξασφαλίζει ότι τηρείτε τη σημασιολογία των πινάκων του Excel, όπως η προστασία της γραμμής κεφαλίδας.

## Βήμα 3: Προσπάθεια διαγραφής της γραμμής κεφαλίδας (επίδειξη προστασίας)

Το Aspose.Cells ρίχνει εξαίρεση εάν προσπαθήσετε να διαγράψετε τη γραμμή κεφαλίδας επειδή το API **protect header row excel** σχεδιάστηκε έτσι. Η επίδειξη αυτής της συμπεριφοράς σας βοηθά να καταλάβετε γιατί μια άμεση διαγραφή αποτυγχάνει.

```csharp
        try
        {
            // Attempt to delete the header row (index 0) and the row below it
            table.DeleteRows(0, 2);
        }
        catch (Exception ex)
        {
            Console.WriteLine("Deletion prevented: " + ex.Message);
        }
```

**Αναμενόμενη έξοδος**

```
Deletion prevented: Cannot delete the header row of a table.
```

**Εξήγηση:** Η μέθοδος `DeleteRows` λαμβάνει έναν μηδενικό δείκτη έναρξης και έναν αριθμό. Ο δείκτης 0 δείχνει στη γραμμή κεφαλίδας, την οποία η βιβλιοθήκη προστατεύει για να διατηρήσει τη δομή του πίνακα αμετάβλητη.

## Βήμα 4: Διαγραφή μόνο των γραμμών δεδομένων – ο σωστός τρόπος για **remove data rows excel**

Τώρα που γνωρίζετε ότι η κεφαλίδα είναι προστατευμένη, διαγράψτε μόνο τις γραμμές δεδομένων που ξεκινούν μετά τη κεφαλίδα. Στους περισσότερους πίνακες η πρώτη γραμμή δεδομένων βρίσκεται στον δείκτη 1.

```csharp
        // Delete three data rows starting after the header (index 1)
        table.DeleteRows(1, 3); // removes rows 2, 3, and 4 of the worksheet

        // Optionally, you can delete a single row:
        // table.DeleteRows(4, 1);
```

**Γιατί λειτουργεί:** Ξεκινώντας από τον δείκτη 1 παραλείπετε την κεφαλίδα, έτσι η ενέργεια συμμορφώνεται με τον κανόνα **protect header row excel**. Η μέθοδος `DeleteRows` ενημερώνει αυτόματα το εσωτερικό εύρος του πίνακα.

## Βήμα 5: Αποθήκευση του τροποποιημένου βιβλίου εργασίας

Αποθηκεύστε τις αλλαγές σε νέο αρχείο ώστε να διατηρήσετε το αρχικό ανέπαφο.

```csharp
        // Save the workbook with the modified table
        workbook.Save(@"YOUR_DIRECTORY\TableHeaderProtected.xlsx");

        Console.WriteLine("Rows deleted and workbook saved successfully.");
    }
}
```

**Αποτέλεσμα:** Μετά την εκτέλεση του προγράμματος, το `TableHeaderProtected.xlsx` περιέχει την ίδια γραμμή κεφαλίδας, αλλά οι καθορισμένες γραμμές δεδομένων έχουν αφαιρεθεί. Το άνοιγμα του αρχείου στο Excel εμφανίζει έναν καθαρό πίνακα χωρίς τις διαγραμμένες γραμμές.

## Συνηθισμένα λάθη και πώς να τα αποφύγετε

| Πρόβλημα | Γιατί συμβαίνει | Διόρθωση |
|----------|----------------|----------|
| Προσπάθεια διαγραφής της γραμμής κεφαλίδας | Το Aspose.Cells επιβάλλει την ακεραιότητα του πίνακα | Ξεκινάτε πάντα τη διαγραφή από δείκτη 1 ή μεγαλύτερο |
| Διαγραφή περισσότερων γραμμών από όσες υπάρχουν | `DeleteRows` ρίχνει `ArgumentOutOfRangeException` | Ελέγξτε το `table.DataRange.RowCount` πριν καλέσετε το `DeleteRows` |
| Εργασία με περιοχή που δεν είναι πίνακας | Οι μέθοδοι `ListObject` ισχύουν μόνο για δομημένους πίνακες | Μετατρέψτε πρώτα μια περιοχή σε πίνακα (`worksheet.Tables.Add`) εάν χρειάζεται |

**Συμβουλή:** Εάν χρειάζεστε να καθαρίσετε ολόκληρο τον πίνακα αλλά να διατηρήσετε την κεφαλίδα, χρησιμοποιήστε `table.DeleteRows(1, table.DataRange.RowCount - 1);`. Αυτό αφαιρεί κάθε γραμμή δεδομένων ανεξάρτητα από το πόσες γραμμές έχει ο πίνακας αυτή τη στιγμή.

## Εναλλακτικό: Διαγραφή γραμμών με διεύθυνση κελιού

Μερικές φορές μπορεί να γνωρίζετε τη συγκεκριμένη διεύθυνση κελιού αντί για τον δείκτη γραμμής. Μπορείτε να μετατρέψετε μια διεύθυνση σε δείκτη γραμμής με τη συλλογή `Cells`:

```csharp
        // Example: delete rows that contain the value "Obsolete"
        for (int i = table.DataRange.FirstRow; i <= table.DataRange.LastRow; i++)
        {
            if (worksheet.Cells[i, table.DataRange.FirstColumn].StringValue == "Obsolete")
            {
                // Subtract one because DeleteRows expects a zero‑based index relative to the table
                table.DeleteRows(i - table.StartRow + 1, 1);
                i--; // Adjust loop counter after deletion
            }
        }
```

Αυτή η προσέγγιση είναι χρήσιμη όταν οι γραμμές που πρέπει να αφαιρεθούν προσδιορίζονται με βάση το περιεχόμενο αντί για έναν σταθερό αριθμό.

## Δοκιμή της υλοποίησής σας

1. Εκτελέστε το πρόγραμμα με ένα δείγμα βιβλίου εργασίας που έχει τουλάχιστον πέντε γραμμές δεδομένων.  
2. Επαληθεύστε ότι η κονσόλα εκτυπώνει “Rows deleted and workbook saved successfully.”  
3. Ανοίξτε το `TableHeaderProtected.xlsx` στο Excel και επιβεβαιώστε:
   - Η γραμμή κεφαλίδας είναι ακόμη παρούσα.
   - Μόνο οι επιθυμητές γραμμές δεδομένων λείπουν.

Αν η κεφαλίδα εξαφανιστεί, πιθανότατα ξεκινήσατε τη διαγραφή από δείκτη 0—ελέγξτε το **Βήμα 4**.

## Συμπέρασμα

Τώρα ξέρετε πώς να **delete rows from Excel table** με ασφάλεια χρησιμοποιώντας C#. Ο οδηγός κάλυψε τη φόρτωση ενός βιβλίου εργασίας, την πρόσβαση στον πίνακα, τον σεβασμό του κανόνα **protect header row excel**, τη σωστή **remove data rows excel**, και την αποθήκευση του αποτελέσματος. Ακολουθώντας αυτά τα βήματα αποφεύγετε κοινά σφάλματα και διατηρείτε τους πίνακες Excel καλά δομημένους.

### Επόμενα βήματα

- Εξερευνήστε τις δυνατότητες του **Aspose.Cells** όπως η εισαγωγή γραμμών, η εφαρμογή στυλ ή το φιλτράρισμα δεδομένων.  
- Συνδυάστε τη διαγραφή γραμμών με **Excel formulas** για να αυτοματοποιήσετε τον καθαρισμό βάσει των αποτελεσμάτων υπολογισμών.  
- Δείτε συναφή θέματα όπως η **exporting Excel to CSV** ή η **reading large workbooks efficiently**.

Μη διστάσετε να πειραματιστείτε με διαφορετικούς αριθμούς γραμμών, πολλαπλούς πίνακες ή υπό όρους διαγραφές. Εάν αντιμετωπίσετε ειδικές περιπτώσεις, ανατρέξτε ξανά στη διαχείριση σφαλμάτων που φαίνεται στο **Βήμα 3**—η βιβλιοθήκη θα προστατεύει πάντα τη γραμμή κεφαλίδας για εσάς. Καλή προγραμματιστική!

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά σχετικές θεματικές που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Διαγραφή πολλαπλών γραμμών σε Excel με Aspose.Cells .NET: Ένας ολοκληρωμένος οδηγός για τη διαχείριση δεδομένων](/cells/english/net/data-manipulation/delete-rows-excel-aspose-cells-net/)
- [Πώς να εισάγετε και να διαγράψετε γραμμές σε Excel με Aspose.Cells για .NET: Ένας ολοκληρωμένος οδηγός](/cells/english/net/data-manipulation/aspose-cells-net-insert-delete-excel-rows/)
- [Πώς να διαγράψετε κενές γραμμές σε Excel χρησιμοποιώντας Aspose.Cells .NET για καθαρισμό δεδομένων](/cells/english/net/data-manipulation/delete-blank-rows-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}