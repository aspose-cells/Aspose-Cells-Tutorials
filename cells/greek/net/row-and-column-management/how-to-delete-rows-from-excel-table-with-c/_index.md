---
category: general
date: 2026-11-25
description: Μάθετε πώς να διαγράψετε γραμμές από πίνακα Excel σε C# και επίσης να
  διαγράψετε αποδοτικά πολλαπλές γραμμές από φύλλο Excel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- delete rows from excel table
- delete multiple rows from excel sheet
language: el
lastmod: 2026-11-25
og_description: Διαγράψτε γραμμές από πίνακα Excel σε C# και μάθετε πώς να διαγράψετε
  πολλαπλές γραμμές από φύλλο Excel με καθαρό κώδικα.
og_image_alt: Screenshot of C# code deleting rows from an Excel table
og_title: Διαγραφή γραμμών από πίνακα Excel σε C# – πλήρης οδηγός
schemas:
- author: Aspose
  dateModified: '2026-11-25'
  description: Learn how to delete rows from Excel table in C# and also delete multiple
    rows from Excel sheet efficiently.
  headline: How to delete rows from Excel table with C#
  type: TechArticle
- description: Learn how to delete rows from Excel table in C# and also delete multiple
    rows from Excel sheet efficiently.
  name: How to delete rows from Excel table with C#
  steps:
  - name: Add Aspose.Cells to your project
    text: 'Open the **Package Manager Console** and run:'
  - name: Load the workbook and locate the table
    text: '```csharp using Aspose.Cells;'
  - name: Delete the desired data rows
    text: The `DeleteRows` method expects a **zero‑based** row index relative to the
      table, **including** the header row. Because the header cannot be removed, you
      must start at index 1 for the first data row.
  - name: Save the modified workbook
    text: '```csharp // Save the workbook to a new file to preserve the original workbook.Save(@"C:\Data\table_with_header_modified.xlsx");
      } } ```'
  - name: Full working example
    text: '```csharp using Aspose.Cells;'
  - name: Edge cases and best practices
    text: '| Situation | Recommended handling | |----------------------------------------|----------------------|
      | Deleting rows beyond the last row | Check `worksheet.Rows.Count` before calling
      `RemoveAt`. | | Removing all rows except the header | Delete data rows in a
      loop or use `DeleteRows(1, table.DataRa'
  type: HowTo
tags:
- Excel automation
- C#
- Aspose.Cells
- data manipulation
title: Πώς να διαγράψετε γραμμές από πίνακα Excel με C#
url: /el/net/row-and-column-management/how-to-delete-rows-from-excel-table-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να διαγράψετε γραμμές από πίνακα Excel με C#

Αν χρειάζεται να διαγράψετε γραμμές από πίνακα Excel χρησιμοποιώντας C#, αυτός ο οδηγός σας δείχνει ακριβώς πώς να το κάνετε. Θα δείτε επίσης πώς να διαγράψετε πολλαπλές γραμμές από φύλλο Excel χωρίς να επηρεάσετε άλλα δεδομένα.

Η εργασία με το Excel προγραμματιστικά συχνά απαιτεί την αφαίρεση παλαιών ή μη έγκυρων εγγραφών. Η διαγραφή γραμμών απευθείας σε ένα φύλλο εργασίας μπορεί να είναι επικίνδυνη, επειδή η γραμμή κεφαλίδας ενός δομημένου πίνακα πρέπει να παραμείνει αμετάβλητη. Αυτό το tutorial σας καθοδηγεί βήμα-βήμα σε μια ασφαλή προσέγγιση που σέβεται την κεφαλίδα του πίνακα και σας επιτρέπει να διαγράψετε οποιονδήποτε αριθμό γραμμών δεδομένων με μία κλήση.

## Προαπαιτούμενα

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

* .NET 6.0 ή νεότερη έκδοση εγκατεστημένη  
* Visual Studio 2022 (ή οποιοδήποτε συμβατό IDE)  
* Το πακέτο **Aspose.Cells** NuGet (έκδοση 23.10 ή νεότερη) – αυτή η βιβλιοθήκη παρέχει τις κλάσεις `Workbook`, `Worksheet` και `ListObject` που χρησιμοποιούνται στα παραδείγματα  

Δεν χρειάζεται να έχετε εγκατεστημένο το Microsoft Office στον υπολογιστή ανάπτυξης, επειδή το Aspose.Cells λειτουργεί απευθείας με τη μορφή αρχείου.

## Διαγραφή γραμμών από πίνακα Excel – βήμα‑βήμα

Οι παρακάτω ενότητες περιγράφουν κάθε βήμα που απαιτείται για ασφαλή διαγραφή γραμμών από έναν πίνακα Excel. Η κύρια λέξη‑κλειδί εμφανίζεται σε αυτήν την επικεφαλίδα για να ικανοποιήσει τις απαιτήσεις SEO.

### Βήμα 1: Προσθήκη Aspose.Cells στο έργο σας

Ανοίξτε το **Package Manager Console** και εκτελέστε:

```powershell
Install-Package Aspose.Cells
```

Το πακέτο προσθέτει τις απαραίτητες συναρτήσεις και επιλύει τους τύπους `Workbook`, `Worksheet` και `ListObject`.

### Βήμα 2: Φόρτωση του βιβλίου εργασίας και εντοπισμός του πίνακα

```csharp
using Aspose.Cells;

class ExcelRowDeletion
{
    static void Main()
    {
        // Load the workbook that contains the table
        var workbook = new Workbook(@"C:\Data\table_with_header.xlsx");

        // Access the first worksheet (index 0)
        var worksheet = workbook.Worksheets[0];

        // Retrieve the first ListObject (structured table) on the sheet
        var table = worksheet.ListObjects[0];
```

*Γιατί είναι σημαντικό*: Το `ListObject` αντιπροσωπεύει έναν πραγματικό πίνακα Excel, ο οποίος διατηρεί τη δική του γραμμή κεφαλίδας. Εργαζόμενοι με το `ListObject`, αποφεύγετε την τυχαία αφαίρεση της κεφαλίδας.

### Βήμα 3: Διαγραφή των επιθυμητών γραμμών δεδομένων

Η μέθοδος `DeleteRows` αναμένει έναν **μηδενικής βάσης** δείκτη γραμμής σε σχέση με τον πίνακα, **συμπεριλαμβανομένης** της γραμμής κεφαλίδας. Επειδή η κεφαλίδα δεν μπορεί να αφαιρεθεί, πρέπει να ξεκινήσετε από το δείκτη 1 για την πρώτη γραμμή δεδομένων.

```csharp
        // Delete two data rows starting after the header (index 1)
        // Parameters: startRow (relative to the table), numberOfRows
        table.DeleteRows(1, 2);
```

Αν προσπαθήσετε `table.DeleteRows(0, 2)`, το Aspose.Cells θα ρίξει εξαίρεση επειδή η γραμμή κεφαλίδας (δείκτης 0) είναι προστατευμένη. Ξεκινώντας από το δείκτη 1 εξασφαλίζετε ότι αφαιρούνται μόνο γραμμές δεδομένων.

### Βήμα 4: Αποθήκευση του τροποποιημένου βιβλίου εργασίας

```csharp
        // Save the workbook to a new file to preserve the original
        workbook.Save(@"C:\Data\table_with_header_modified.xlsx");
    }
}
```

Η εκτέλεση του προγράμματος αφαιρεί τις δύο γραμμές αμέσως κάτω από την κεφαλίδα, ενώ η δομή του πίνακα παραμένει αμετάβλητη.

### Πλήρες λειτουργικό παράδειγμα

```csharp
using Aspose.Cells;

class ExcelRowDeletion
{
    static void Main()
    {
        // 1. Load workbook
        var workbook = new Workbook(@"C:\Data\table_with_header.xlsx");

        // 2. Access first worksheet
        var worksheet = workbook.Worksheets[0];

        // 3. Get the first table (ListObject)
        var table = worksheet.ListObjects[0];

        // 4. Delete two rows after the header (cannot delete header itself)
        table.DeleteRows(1, 2);

        // 5. Save the result
        workbook.Save(@"C:\Data\table_with_header_modified.xlsx");
    }
}
```

**Αναμενόμενο αποτέλεσμα**: Το αρχείο `table_with_header_modified.xlsx` περιέχει την αρχική κεφαλίδα του πίνακα, ακολουθούμενη από όλες τις γραμμές εκτός από τις δύο που αφαιρέθηκαν. Δεν επηρεάζονται άλλα φύλλα εργασίας.

## Διαγραφή πολλαπλών γραμμών από φύλλο Excel

Μερικές φορές χρειάζεται να διαγράψετε γραμμές που **δεν** αποτελούν μέρος ενός δομημένου πίνακα. Η δευτερεύουσα λέξη‑κλειδί εμφανίζεται σε αυτήν την επικεφαλίδα. Η προσέγγιση διαφέρει ελαφρώς επειδή εργάζεστε με τη συλλογή `Rows` του φύλλου εργασίας αντί για ένα `ListObject`.

```csharp
using Aspose.Cells;

class SheetRowDeletion
{
    static void Main()
    {
        var workbook = new Workbook(@"C:\Data\plain_sheet.xlsx");
        var worksheet = workbook.Worksheets[0];

        // Delete rows 5 through 9 (inclusive) – zero‑based index
        // The second argument is the count of rows to remove
        worksheet.Rows.RemoveAt(4, 5);

        workbook.Save(@"C:\Data\plain_sheet_modified.xlsx");
    }
}
```

**Γιατί λειτουργεί**: Η `Rows.RemoveAt(startIndex, count)` αφαιρεί ένα συνεχόμενο μπλοκ γραμμών απευθείας από το φύλλο εργασίας. Δεν υπάρχει προστασία κεφαλίδας, οπότε μπορείτε να ξεκινήσετε από οποιονδήποτε δείκτη. Η μέθοδος είναι αποδοτική επειδή ενημερώνει τις εσωτερικές δομές δεδομένων σε μία μόνο λειτουργία, κάτι ιδανικό όταν πρέπει να διαγράψετε πολλαπλές γραμμές από ένα φύλλο Excel.

### Ακραίες περιπτώσεις και βέλτιστες πρακτικές

| Κατάσταση                                 | Προτεινόμενη αντιμετώπιση |
|-------------------------------------------|---------------------------|
| Διαγραφή γραμμών πέρα από την τελευταία γραμμή | Ελέγξτε το `worksheet.Rows.Count` πριν καλέσετε το `RemoveAt`. |
| Αφαίρεση όλων των γραμμών εκτός της κεφαλίδας | Διαγράψτε τις γραμμές δεδομένων σε βρόχο ή χρησιμοποιήστε `DeleteRows(1, table.DataRange.RowCount - 1)`. |
| Διατήρηση μορφοποίησης κελιών            | Η διαγραφή μέσω `ListObject` μετατοπίζει αυτόματα τη μορφοποίηση· για ακατέργαστα φύλλα, αντιγράψτε τη μορφοποίηση πριν την αφαίρεση αν χρειάζεται. |
| Μεγάλα φύλλα εργασίας (> 10 000 γραμμές)  | Εκτελέστε τις διαγραφές σε φθίνουσα σειρά για να αποφύγετε την μετατόπιση δεικτών, ή χρησιμοποιήστε `DeleteRows` στον πίνακα αν είναι δυνατόν. |

**Συμβουλή**: Όταν χρειάζεται να διαγράψετε γραμμές βάσει συνθήκης (π.χ., γραμμές όπου η τιμή μιας στήλης είναι κενή), επαναλάβετε το `DataRange` του πίνακα προς τα πίσω και καλέστε `DeleteRows` για κάθε γραμμή που ταιριάζει. Η διαγραφή προς τα πίσω αποτρέπει την ασυμφωνία δεικτών.

## Συχνές ερωτήσεις

*Λειτουργεί αυτό με αρχεία .xlsx που δημιουργήθηκαν από το Excel 365;*  
Ναι. Το Aspose.Cells υποστηρίζει πλήρως την προδιαγραφή Office Open XML, οπότε ο ίδιος κώδικας λειτουργεί για οποιοδήποτε σύγχρονο αρχείο `.xlsx`.

*Τι γίνεται αν το βιβλίο εργασίας περιέχει πολλαπλούς πίνακες;*  
Ανακτήστε τον επιθυμητό πίνακα με όνομα: `var table = worksheet.ListObjects["MyTable"];` και στη συνέχεια εφαρμόστε το `DeleteRows` όπως φαίνεται.

*Μπορώ να διαγράψω γραμμές χωρίς χρήση βιβλιοθήκης τρίτου μέρους;*  
Μπορείτε να χρησιμοποιήσετε το Microsoft.Office.Interop.Excel COM interop, αλλά αυτό απαιτεί εγκατάσταση του Excel στον διακομιστή και προσθέτει κόστος COM. Το Aspose.Cells προσφέρει μια ελαφριά, ασφαλή εναλλακτική λύση για διακομιστές.

## Συμπέρασμα

Τώρα γνωρίζετε πώς να διαγράψετε γραμμές από πίνακα Excel με ασφάλεια και πώς να διαγράψετε πολλαπλές γραμμές από φύλλο Excel χρησιμοποιώντας C#. Η κύρια τεχνική βασίζεται στη μέθοδο `ListObject.DeleteRows`, η οποία σέβεται την κεφαλίδα του πίνακα, ενώ η δευτερεύουσα τεχνική χρησιμοποιεί `Rows.RemoveAt` για απλά φύλλα. Εφαρμόστε αυτά τα πρότυπα για καθαρισμό δεδομένων, αυτοματοποίηση δημιουργίας αναφορών ή υλοποίηση λειτουργιών μαζικής επεξεργασίας στις εφαρμογές σας.

**Επόμενα βήματα**

* Εξερευνήστε άλλες δυνατότητες του Aspose.Cells όπως η εισαγωγή γραμμών, η αντιγραφή στυλ ή το φιλτράρισμα δεδομένων.  
* Δοκιμάστε τις ίδιες λειτουργίες με το **ClosedXML** αν προτιμάτε μια ανοιχτή βιβλιοθήκη· το API είναι παρόμοιο αλλά χρησιμοποιεί `IXLTable` και `IXLRows`.  
* Συνδυάστε τη λογική διαγραφής γραμμών με ερωτήματα LINQ για να δημιουργήσετε πιο σύνθετους σωλήνες καθαρισμού δεδομένων.

Καλή προγραμματιστική δουλειά!

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στην υλοποίηση.

- [πώς να διαγράψετε γραμμές σε Excel με C# – προστασία κεφαλίδας πίνακα](/cells/english/net/row-and-column-management/how-to-delete-rows-in-excel-with-c-protect-table-header/)
- [Πώς να χρησιμοποιήσετε το Aspose.Cells για διαγραφή γραμμών σε πίνακα Excel ενώ διατηρείτε την](/cells/english/net/row-and-column-management/how-to-use-aspose-cells-to-delete-rows-in-an-excel-table-whi/)
- [Φόρτωση αρχείου Excel C# – Πώς να διαγράψετε γραμμές και να αφαιρέσετε συγκεκριμένες γραμμές](/cells/english/net/row-and-column-management/load-excel-file-c-how-to-delete-rows-and-remove-specific-row/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}