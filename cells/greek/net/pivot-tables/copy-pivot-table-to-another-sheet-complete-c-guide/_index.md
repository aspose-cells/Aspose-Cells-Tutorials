---
category: general
date: 2026-06-27
description: Αντιγράψτε τον πίνακα Pivot σε άλλο φύλλο σε C# χρησιμοποιώντας το Aspose.Cells.
  Μάθετε βήμα‑βήμα πώς να διατηρήσετε τα δεδομένα και τη μορφοποίηση του Pivot.
draft: false
keywords:
- copy pivot table to another sheet
- Aspose.Cells copy pivot
- Excel pivot duplication
- preserve pivot formatting
- copy range with pivot
language: el
og_description: Αντιγραφή πίνακα Pivot σε άλλο φύλλο σε C# με το Aspose.Cells. Αυτό
  το σεμινάριο δείχνει ακριβώς πώς να αντιγράψετε έναν πίνακα Pivot διατηρώντας το
  μορφοποίημά του αμετάβλητο.
og_title: Αντιγραφή Πίνακα Pivot σε Άλλο Φύλλο – Πλήρης Οδηγός C#
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Copy pivot table to another sheet in C# using Aspose.Cells. Learn step‑by‑step
    how to preserve pivot data and formatting.
  headline: Copy Pivot Table to Another Sheet – Complete C# Guide
  type: TechArticle
tags:
- Excel automation
- C#
- Aspose.Cells
title: Αντιγραφή Πίνακα Pivot σε Άλλο Φύλλο – Πλήρης Οδηγός C#
url: /el/net/pivot-tables/copy-pivot-table-to-another-sheet-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Αντιγραφή Πίνακα Pivot σε Άλλο Φύλλο – Πλήρης Οδηγός C#

Έχετε ποτέ χρειαστεί να **αντιγράψετε έναν πίνακα pivot σε άλλο φύλλο** αλλά ανησυχείτε ότι θα χάσετε τα slicers, τα υπολογιζόμενα πεδία ή τη μορφοποίηση; Δεν είστε μόνοι. Πολλοί προγραμματιστές αντιμετωπίζουν αυτό το πρόβλημα όταν αυτοματοποιούν αναφορές Excel, και η απογοήτευση είναι πραγματική. Σε αυτόν τον οδηγό θα περάσουμε βήμα‑βήμα από μια καθαρή, ολοκληρωμένη λύση που **διατηρεί τον πίνακα pivot** ακριβώς όπως εμφανίζεται.

Θα χρησιμοποιήσουμε το **Aspose.Cells for .NET**, μια ισχυρή βιβλιοθήκη που σας επιτρέπει να χειρίζεστε αρχεία Excel χωρίς να ανοίγετε το ίδιο το Excel. Στο τέλος αυτού του σεμιναρίου θα έχετε ένα έτοιμο προς εκτέλεση απόσπασμα C# που αντιγράφει έναν πίνακα pivot από ένα φύλλο εργασίας σε άλλο, διατηρώντας όλες τις υποκείμενες συνδέσεις δεδομένων ανέπαφες.

## Τι Καλύπτει Αυτός ο Οδηγός

- Ρύθμιση ενός έργου .NET και προσθήκη του πακέτου NuGet Aspose.Cells.  
- Φόρτωση ενός υπάρχοντος βιβλίου εργασίας που περιέχει ήδη έναν πίνακα pivot.  
- Ορισμός τόσο της περιοχής προέλευσης (του αρχικού pivot) όσο και της περιοχής προορισμού σε διαφορετικό φύλλο.  
- Χρήση του `CopyOptions` για **διατήρηση του πίνακα pivot** κατά την αντιγραφή.  
- Αποθήκευση του αποτελέσματος και επαλήθευση ότι ο πίνακας pivot λειτουργεί στη νέα του θέση.  

Χωρίς εξωτερικά εργαλεία, χωρίς χειροκίνητη αντιγραφή‑επικόλληση και χωρίς κρυφή μαγεία—απλώς απλός κώδικας που μπορείτε να ενσωματώσετε σε οποιαδήποτε εφαρμογή κονσόλας C# ή υπηρεσία.

> **Γιατί να σας ενδιαφέρει:** Η αυτοματοποίηση της αντιγραφής pivot εξοικονομεί ώρες χειροκίνητης εργασίας, ειδικά σε νυχτερινές γραμμές αναφοράς όπου δεκάδες βιβλία εργασίας χρειάζονται ταυτόσες δομές pivot σε πολλαπλά φύλλα.

---

## Βήμα 1: Ρύθμιση του Έργου και Προσθήκη του Aspose.Cells

Πρώτα απ' όλα. Αν δεν το έχετε κάνει ήδη, δημιουργήστε ένα νέο έργο κονσόλας .NET:

```bash
dotnet new console -n PivotCopyDemo
cd PivotCopyDemo
```

Τώρα προσθέστε το πακέτο Aspose.Cells:

```bash
dotnet add package Aspose.Cells
```

> **Συμβουλή επαγγελματία:** Χρησιμοποιήστε την πιο πρόσφατη σταθερή έκδοση (από τον Ιούνιο 2026 v23.12). Περιλαμβάνει διορθώσεις σφαλμάτων για τη διαχείριση του `CopyPivotTable`.

## Βήμα 2: Φόρτωση του Βιβλίου Εργασίας και Πρόσβαση στα Φύλλα

Ανοίξτε το βιβλίο εργασίας που περιέχει τον πίνακα pivot προέλευσης. Στις περισσότερες πραγματικές περιπτώσεις το αρχείο βρίσκεται σε κοινόχρηστο δίσκο, αλλά για αυτήν την επίδειξη θα υποθέσουμε ότι βρίσκεται σε τοπικό φάκελο με όνομα `YOUR_DIRECTORY`.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Load the workbook containing the source pivot table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/source.xlsx");

        // Step 2: Access the first worksheet (source sheet)
        Worksheet sourceSheet = workbook.Worksheets[0];

        // We'll also create (or reference) a destination sheet
        Worksheet destSheet = workbook.Worksheets.Add("CopyDestination");
```

Εδώ δημιουργούμε ένα νέο φύλλο με όνομα **CopyDestination** όπου θα τοποθετηθεί ο πίνακας pivot. Αν έχετε ήδη ένα φύλλο προορισμού, απλώς πάρτε το με βάση το δείκτη ή το όνομα.

## Βήμα 3: Ορισμός Περιοχών Προέλευσης και Προορισμού

Ένας πίνακας pivot βρίσκεται μέσα σε ένα ορθογώνιο μπλοκ κελιών. Πρέπει να πείτε στο Aspose.Cells ποιο μπλοκ να αντιγράψει. Σε αυτό το παράδειγμα ο pivot καταλαμβάνει τις γραμμές 0‑20 και τις στήλες 0‑10 (αρίθμηση με μηδενική βάση).

```csharp
        // Step 3: Define the source range that includes the pivot table (rows 0‑20, columns 0‑10)
        CellArea sourceRange = new CellArea(0, 0, 20, 10);

        // Step 4: Define the destination start cell (row 30, column 0) on the destination sheet
        // and calculate the target area size to match the source dimensions
        CellArea destinationRange = new CellArea(
            30,                                 // start row on destination sheet
            0,                                  // start column
            30 + sourceRange.RowCount - 1,     // end row (same height as source)
            sourceRange.ColumnCount - 1        // end column (same width as source)
        );
```

Παρατηρήστε πώς υπολογίζουμε δυναμικά τη γραμμή και τη στήλη λήξης. Με αυτόν τον τρόπο, ακόμη και αν αλλάξετε αργότερα το μέγεθος της περιοχής προέλευσης, ο προορισμός θα προσαρμόζεται αυτόματα.

## Βήμα 4: Εκτέλεση της Αντιγραφής Διατηρώντας τον Pivot

Τώρα συμβαίνει η μαγεία. Με τη μεταβίβαση ενός αντικειμένου `CopyOptions` με `CopyPivotTable = true`, το Aspose.Cells γνωρίζει να διατηρήσει αμετάβλητο τον ορισμό του πίνακα pivot.

```csharp
        // Step 5: Copy the range, preserving the pivot table
        destSheet.Cells.CopyRange(
            sourceRange,
            destinationRange,
            new CopyOptions { CopyPivotTable = true }
        );
```

Στο παρασκήνιο, το Aspose.Cells δημιουργεί ξανά την κρυφή μνήμη του pivot, ανανεώνει την αναφορά της πηγής δεδομένων και επαναεφαρμόζει οποιαδήποτε μορφοποίηση. Αυτή είναι η **αντιγραφή pivot στο Excel** που ψάχνατε.

## Βήμα 5: Αποθήκευση και Επαλήθευση του Αποτελέσματος

Τέλος, γράψτε το βιβλίο εργασίας ξανά στο δίσκο. Μπορείτε να διατηρήσετε το αρχικό αρχείο αμετάβλητο αποθηκεύοντας με νέο όνομα.

```csharp
        // Step 6: Save the workbook with the copied pivot table
        workbook.Save("YOUR_DIRECTORY/copy-pivot.xlsx");

        // Optional: open the file automatically (Windows only)
        System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
        {
            FileName = "YOUR_DIRECTORY/copy-pivot.xlsx",
            UseShellExecute = true
        });
    }
}
```

Ανοίξτε το παραγόμενο `copy-pivot.xlsx` και θα δείτε τον πίνακα pivot να έχει αντιγραφεί τέλεια στο φύλλο **CopyDestination**, με όλα τα slicers, τα υπολογιζόμενα πεδία και τη μορφοποίηση. Η υποκείμενη πηγή δεδομένων εξακολουθεί να δείχνει στον αρχικό πίνακα, έτσι η ανανέωση λειτουργεί ακριβώς όπως πριν.

> **Τι γίνεται αν ο pivot προέλευσης καλύπτει μια δυναμική περιοχή;**  
> Χρησιμοποιήστε το `Worksheet.PivotTables[0].CacheDefinition.SourceData` για να ανακτήσετε τα πραγματικά όρια, και στη συνέχεια δημιουργήστε το `sourceRange` από αυτές τις πληροφορίες. Αυτό αντιμετωπίζει περιπτώσεις όπου οι γραμμές ή οι στήλες μπορεί να επεκταθούν με την πάροδο του χρόνου.

## Bonus: Διατήρηση Μορφοποίησης Pivot Κατά τις Αντιγραφές

Μερικές φορές η προεπιλεγμένη αντιγραφή χάνει τη μορφοποίηση υπό όρους ή προσαρμοσμένες μορφές αριθμών. Για να το αποτρέψετε, επεκτείνετε το `CopyOptions`:

```csharp
        var options = new CopyOptions
        {
            CopyPivotTable = true,
            CopyFormatting = true,      // copies cell styles, colors, fonts
            CopyConditionalFormatting = true
        };
        destSheet.Cells.CopyRange(sourceRange, destinationRange, options);
```

Η ενεργοποίηση του `CopyFormatting` εξασφαλίζει ότι η απαίτηση **διατήρησης μορφοποίησης pivot** ικανοποιείται, παρέχοντάς σας ένα αντίγραφο pixel‑perfect.

## Αναμενόμενο Αποτέλεσμα

Όταν εκτελέσετε το πρόγραμμα, η κονσόλα θα κλείσει σιωπηλά (εκτός αν προσθέσετε καταγραφή). Το άνοιγμα του `copy-pivot.xlsx` θα πρέπει να εμφανίζει:

- Φύλλο 1: Τα αρχικά δεδομένα και ο πίνακας pivot αμετάβλητα.  
- **CopyDestination**: Ένα ακριβές αντίγραφο του pivot, τοποθετημένο ξεκινώντας από τη γραμμή 31 (επειδή οι γραμμές είναι 1‑βασισμένες στη διεπαφή του Excel).  
- Όλα τα slicers και τα φίλτρα λειτουργούν· κάνοντας κλικ στο “Refresh” ενημερώνει και τους δύο pivots ταυτόχρονα.

## Συμπέρασμα

Μόλις δείξαμε πώς να **αντιγράψετε έναν πίνακα pivot σε άλλο φύλλο** χρησιμοποιώντας το Aspose.Cells σε C#. Τα βήματα—ρύθμιση του έργου, φόρτωση του βιβλίου εργασίας, ορισμός περιοχών, αντιγραφή με `CopyPivotTable = true` και αποθήκευση—αποτελούν ένα αξιόπιστο πρότυπο που μπορείτε να επαναχρησιμοποιήσετε σε οποιοδήποτε pipeline αυτοματοποίησης.

Αν θέλετε να προχωρήσετε παραπέρα, σκεφτείτε:

- **Αντιγραφή pivot στο Excel** μεταξύ πολλαπλών βιβλίων εργασίας (βρόχος μέσω αρχείων).  
- Χρήση της επιλογής **Aspose.Cells copy range with pivot** για μετακίνηση pivots μεταξύ διαφορετικών βιβλίων εργασίας.  
- Αυτοματοποίηση των ανανεώσεων με `PivotTable.RefreshData()` μετά την αντιγραφή.

Νιώστε ελεύθεροι να πειραματιστείτε με διαφορετικές περιοχές προέλευσης, ή να συνδυάσετε αυτήν την τεχνική με δημιουργία γραφημάτων για πλήρως αυτοματοποιημένα dashboards αναφορών. Έχετε ερωτήσεις; Αφήστε ένα σχόλιο και καλή προγραμματιστική!

![Στιγμιότυπο οθόνης που δείχνει τον αντιγραμμένο πίνακα pivot σε νέο φύλλο](copy-pivot-screenshot.png "παράδειγμα αντιγραφής πίνακα pivot σε άλλο φύλλο")

## Τι Θα Πρέπει Να Μάθετε Στη Σειρά;

Τα παρακάτω σεμινάρια καλύπτουν στενά σχετιζόμενα θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε σε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να Αλλάξετε τα Δεδομένα Πηγής του Πίνακα Pivot Χρησιμοποιώντας το Aspose.Cells για .NET | Οδηγός Ανάλυσης Δεδομένων](/cells/english/net/data-analysis/change-pivot-table-source-aspose-cells-net/)
- [Κατακτήστε τη Μορφοποίηση Πίνακα Pivot σε .NET Χρησιμοποιώντας το Aspose.Cells](/cells/english/net/formatting/format-pivot-tables-dotnet-aspose-cells/)
- [Πρόσβαση σε Εξωτερικές Πηγές Δεδομένων Πίνακα Pivot σε .NET χρησιμοποιώντας το Aspose.Cells](/cells/english/net/data-analysis/access-pivot-table-data-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}