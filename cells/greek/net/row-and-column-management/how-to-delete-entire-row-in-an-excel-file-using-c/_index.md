---
category: general
date: 2026-10-10
description: Μάθετε πώς να διαγράψετε ολόκληρη γραμμή σε ένα βιβλίο εργασίας Excel
  με C#. Αυτός ο οδηγός βήμα‑βήμα καλύπτει επίσης πώς να διαγράψετε γραμμή κατά δείκτη
  και να αφαιρέσετε γραμμή κατά δείκτη χρησιμοποιώντας το Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- delete entire row
- how to delete row
- remove row by index
- delete row excel
- delete row c#
language: el
lastmod: 2026-10-10
og_description: Διαγράψτε ολόκληρη τη γραμμή σε ένα βιβλίο εργασίας Excel χρησιμοποιώντας
  C#. Ακολουθήστε αυτόν τον οδηγό για να μάθετε πώς να διαγράψετε γραμμή με δείκτη,
  να αφαιρέσετε γραμμή με δείκτη και να αποθηκεύσετε το αρχείο με ασφάλεια.
og_image_alt: Screenshot of an Excel worksheet before and after deleting an entire
  row with C# code
og_title: Διαγραφή ολόκληρης γραμμής στο Excel με C# – πλήρης οδηγός προγραμματισμού
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Learn how to delete entire row in an Excel workbook with C#. This step‑by‑step
    guide also covers how to delete row by index and remove row by index using Aspose.Cells.
  headline: How to delete entire row in an Excel file using C#
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
title: Πώς να διαγράψετε ολόκληρη τη γραμμή σε αρχείο Excel χρησιμοποιώντας C#
url: /el/net/row-and-column-management/how-to-delete-entire-row-in-an-excel-file-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Διαγραφή ολόκληρης γραμμής σε αρχείο Excel χρησιμοποιώντας C#

Αν χρειάζεστε **διαγραφή ολόκληρης γραμμής** σε ένα βιβλίο εργασίας Excel, αυτός ο οδηγός σας δείχνει ακριβώς πώς να το κάνετε με C#. Είτε καθαρίζετε εισαγόμενα δεδομένα είτε δημιουργείτε ένα εργαλείο αναφοράς, τα παρακάτω βήματα σας επιτρέπουν να αφαιρέσετε μια γραμμή με βάση το δείκτη της και να αποθηκεύσετε το αποτέλεσμα χωρίς να χάσετε άλλα δεδομένα.

Θα δείτε επίσης πώς η ίδια προσέγγιση απαντά στην ερώτηση **how to delete row** με δείκτη, πώς να **remove row by index**, και γιατί λειτουργεί για σενάρια **delete row excel** σε C#.

## Προαπαιτούμενα

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

* .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί επίσης με .NET Framework 4.6+)
* Η βιβλιοθήκη **Aspose.Cells for .NET** (διαθέσιμη μέσω NuGet: `Install-Package Aspose.Cells`)
* Βασική εξοικείωση με έργα κονσόλας ή επιφάνειας εργασίας C#

Δεν απαιτούνται πρόσθετα Excel interop ή COM components, κάτι που διατηρεί τη λύση ελαφριά και ασφαλή για εκτέλεση στο διακομιστή.

## Βήμα 1: Ρύθμιση του έργου και εισαγωγή namespaces

Δημιουργήστε μια νέα εφαρμογή κονσόλας (ή προσθέστε τον κώδικα σε υπάρχον έργο) και προσθέστε τις απαιτούμενες οδηγίες `using`:

```csharp
using System;
using Aspose.Cells;

namespace ExcelRowDeletion
{
    class Program
    {
        static void Main(string[] args)
        {
            // The rest of the tutorial code lives here.
        }
    }
}
```

*Γιατί είναι σημαντικό*: Η εισαγωγή του `Aspose.Cells` σας δίνει πρόσβαση στα `Workbook`, `Worksheet` και στη μέθοδο `DeleteRows` που εκτελεί την πραγματική διαγραφή της γραμμής.

## Βήμα 2: Φόρτωση του βιβλίου εργασίας και επιλογή του φύλλου εργασίας

Πρέπει να φορτώσετε το αρχείο προέλευσης (`input.xlsx`) και να αποκτήσετε το φύλλο εργασίας που θέλετε να τροποποιήσετε. Το πρώτο φύλλο εργασίας προσπελαύνεται με δείκτη `0`.

```csharp
// Load the workbook from disk
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Get the first worksheet (you can also use workbook.Worksheets["SheetName"])
Worksheet ws = workbook.Worksheets[0];
```

> **Συμβουλή**: Εάν χρειάζεται να εργαστείτε με συγκεκριμένο φύλλο, αντικαταστήστε το δείκτη με το όνομα του φύλλου: `workbook.Worksheets["Data"]`.

## Βήμα 3: Διαγραφή ολόκληρης γραμμής με βάση τον μηδενικό δείκτη

Το Aspose.Cells χρησιμοποιεί μηδενική αρίθμηση, επομένως η πρώτη γραμμή είναι `0`. Για να διαγράψετε τη γραμμή 5 (η έκτη οπτική γραμμή), καλέστε τη `DeleteRows` με το `DeleteOptions.DeleteEntireRow`.

```csharp
// Delete one row starting at index 5 (zero‑based) and remove the whole row
ws.Cells[5, 0].DeleteRows(1, DeleteOptions.DeleteEntireRow);
```

*Εξήγηση*:

* `ws.Cells[5, 0]` δείχνει στο πρώτο κελί της γραμμής που θέλετε να διαγράψετε.  
* `DeleteRows(1, DeleteOptions.DeleteEntireRow)` λέει στο Aspose.Cells να αφαιρέσει **1** γραμμή, και η σημαία `DeleteEntireRow` εξασφαλίζει ότι **ολόκληρη η γραμμή** εξαφανίζεται, μετακινώντας τις παρακάτω γραμμές προς τα πάνω.

### Πώς να διαγράψετε γραμμή με δείκτη σε άλλες περιπτώσεις

* **Διαγραφή πολλαπλών διαδοχικών γραμμών** – αλλάξτε το πρώτο όρισμα στον αριθμό των γραμμών που θέλετε να διαγράψετε:

  ```csharp
  // Remove rows 5, 6 and 7 (three rows total)
  ws.Cells[5, 0].DeleteRows(3, DeleteOptions.DeleteEntireRow);
  ```

* **Διαγραφή της τελευταίας γραμμής** – χρησιμοποιήστε το `ws.Cells.MaxDataRow` για να λάβετε το δείκτη της πιο κάτω πλημμυρισμένης γραμμής:

  ```csharp
  int lastRow = ws.Cells.MaxDataRow;
  ws.Cells[lastRow, 0].DeleteRows(1, DeleteOptions.DeleteEntireRow);
  ```

Αυτά τα αποσπάσματα απαντούν στην απαίτηση **remove row by index** διατηρώντας τον κώδικα εύκολο στην ανάγνωση.

## Βήμα 4: Αποθήκευση του βιβλίου εργασίας με τη διαγραμμένη γραμμή

Μετά τη διαγραφή, γράψτε το τροποποιημένο βιβλίο εργασίας ξανά στο δίσκο. Μπορείτε να αντικαταστήσετε το αρχικό αρχείο ή να δημιουργήσετε ένα νέο.

```csharp
// Save the workbook to a new file (or overwrite the original)
workbook.Save("YOUR_DIRECTORY/output.xlsx");
```

Εάν χρειάζεται να διατηρήσετε το αρχικό αρχείο αμετάβλητο, απλώς αλλάξτε τη διαδρομή εξόδου. Η μέθοδος `Save` υποστηρίζει πολλές μορφές (`.xls`, `.csv`, `.pdf`, κ.λπ.) – απλώς αλλάξτε την επέκταση του αρχείου.

## Πλήρες λειτουργικό παράδειγμα

Συνδυάζοντας όλα, εδώ είναι ένα πλήρες, έτοιμο‑για‑εκτέλεση πρόγραμμα:

```csharp
using System;
using Aspose.Cells;

namespace ExcelRowDeletion
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the workbook
            Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

            // 2️⃣ Select the first worksheet
            Worksheet ws = workbook.Worksheets[0];

            // 3️⃣ Delete the entire row at index 5 (sixth visual row)
            ws.Cells[5, 0].DeleteRows(1, DeleteOptions.DeleteEntireRow);

            // 4️⃣ Save the result
            workbook.Save("YOUR_DIRECTORY/output.xlsx");

            Console.WriteLine("Row deleted successfully. Output saved to output.xlsx");
        }
    }
}
```

**Αναμενόμενη έξοδος**: Μετά την εκτέλεση του προγράμματος, το `output.xlsx` θα περιέχει όλες τις αρχικές γραμμές εκτός από αυτή που ξεκίνησε στην οπτική γραμμή 6. Όλα τα δεδομένα κάτω από τη διαγραμμένη γραμμή μετακινούνται αυτόματα προς τα πάνω, διατηρώντας τύπους και μορφοποίηση.

## Συνηθισμένα προβλήματα και πώς να τα αποφύγετε

| Πρόβλημα | Γιατί συμβαίνει | Διόρθωση |
|----------|----------------|----------|
| **Index out of range** | Προσπάθεια διαγραφής δείκτη γραμμής που δεν υπάρχει (π.χ., `ws.Cells[1000,0]` σε φύλλο 200 γραμμών) | Χρησιμοποιήστε το `ws.Cells.MaxDataRow` για να επαληθεύσετε τον υψηλότερο έγκυρο δείκτη πριν καλέσετε τη `DeleteRows`. |
| **Partial row deletion** | Η παράλειψη του `DeleteOptions.DeleteEntireRow` οδηγεί στο καθαρισμό μόνο του περιεχομένου των κελιών | Πάντα περάστε το `DeleteOptions.DeleteEntireRow` όταν χρειάζεται η ολική διαγραφή της γραμμής. |
| **Unexpected formula changes** | Η διαγραφή γραμμών που αποτελούν μέρος μιας περιοχής τύπων μπορεί να σπάσει τις αναφορές | Επανυπολογίστε τους τύπους μετά τη διαγραφή (`workbook.CalculateFormula()`) εάν το βιβλίο εργασίας σας εξαρτάται από δυναμικές περιοχές. |
| **Saving to a read‑only location** | Η κλήση `Save` προκαλεί εξαίρεση εάν ο φάκελος είναι προστατευμένος | Βεβαιωθείτε ότι ο προορισμός είναι εγγράψιμος ή εκτελέστε το πρόγραμμα με τις κατάλληλες άδειες. |

Η αντιμετώπιση αυτών των ζητημάτων κάνει τη λύση ανθεκτική για παραγωγική χρήση και ικανοποιεί τα ερωτήματα **delete row excel** και **delete row c#**.

## Προχωρημένο: Διαγραφή γραμμών βάσει συνθήκης

Μερικές φορές χρειάζεται να αφαιρέσετε γραμμές που πληρούν ένα συγκεκριμένο κριτήριο (π.χ., γραμμές όπου η στήλη A είναι κενή). Ο παρακάτω βρόχος δείχνει έναν ασφαλή τρόπο σάρωσης από το κάτω προς το πάνω και διαγραφής των αντίστοιχων γραμμών:

```csharp
int lastRow = ws.Cells.MaxDataRow;
for (int row = lastRow; row >= 0; row--)
{
    // Check if column A (index 0) is empty
    if (ws.Cells[row, 0].StringValue == string.Empty)
    {
        ws.Cells[row, 0].DeleteRows(1, DeleteOptions.DeleteEntireRow);
    }
}
workbook.Save("YOUR_DIRECTORY/cleaned.xlsx");
```

Η σάρωση προς τα πάνω αποτρέπει το πρόβλημα μετατόπισης του δείκτη που συμβαίνει όταν διαγράφετε γραμμές ενώ διατρέχετε τη λίστα προς τα εμπρός.

## Συμπέρασμα

Τώρα γνωρίζετε πώς να **delete entire row** σε ένα βιβλίο εργασίας Excel χρησιμοποιώντας C#. Ο οδηγός κάλυψε:

* Φόρτωση βιβλίου εργασίας και επιλογή φύλλου εργασίας  
* Χρήση της `DeleteRows` με `DeleteOptions.DeleteEntireRow` για **how to delete row** με δείκτη  
* Ασφαλή αποθήκευση του τροποποιημένου αρχείου  
* Διαχείριση ειδικών περιπτώσεων, συμβουλές απόδοσης, και παράδειγμα διαγραφής βάσει συνθήκης  

Με αυτή τη γνώση μπορείτε με σιγουριά να υλοποιήσετε τη λειτουργικότητα **remove row by index**, να αυτοματοποιήσετε τον καθαρισμό δεδομένων, και να ενσωματώσετε τη διαχείριση Excel σε οποιαδήποτε εφαρμογή C#.  

**Επόμενα βήματα**: εξερευνήστε άλλα χαρακτηριστικά του Aspose.Cells όπως η εισαγωγή γραμμών, η αντιγραφή περιοχών, ή η μετατροπή του βιβλίου εργασίας σε PDF—όλα αυτά βασίζονται στα ίδια αντικείμενα `Workbook` και `Worksheet` που μόλις μάθατε. Καλή προγραμματιστική!

## Τι θα πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [How to Delete an Excel Row Using Aspose.Cells .NET&#58; A Comprehensive Guide](/cells/english/net/worksheet-management/delete-excel-row-aspose-cells-net-tutorial/)
- [Aspose Cells Delete Rows – Protect Header Row in Excel](/cells/english/net/row-and-column-management/aspose-cells-delete-rows-protect-header-row-in-excel/)
- [Efficient Row Management in Excel using Aspose.Cells for Java&#58; Insert and Delete Rows](/cells/english/java/worksheet-management/aspose-cells-java-row-operations-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}