---
category: general
date: 2026-02-09
description: Δημιουργήστε νέο βιβλίο εργασίας Excel και μάθετε πώς να αντιγράφετε
  πίνακες Pivot χωρίς κόπο. Αυτός ο οδηγός δείχνει πώς να διπλασιάζετε έναν πίνακα
  Pivot και να αποθηκεύετε το βιβλίο εργασίας ως νέο.
draft: false
keywords:
- create new excel workbook
- how to copy pivot
- duplicate pivot table
- save workbook as new
- how to copy worksheet
language: el
og_description: Δημιουργήστε νέο βιβλίο εργασίας Excel σε C# και αντιγράψτε αμέσως
  έναν πίνακα Pivot. Μάθετε πώς να αντιγράψετε τον πίνακα Pivot και να αποθηκεύσετε
  το βιβλίο εργασίας ως νέο, με ένα πλήρες παράδειγμα κώδικα.
og_title: Δημιουργία Νέου Φύλλου Εργασίας Excel – Αντιγραφή Pivot Βήμα προς Βήμα
tags:
- excel
- csharp
- aspose.cells
- automation
title: Δημιουργία νέου βιβλίου εργασίας Excel – Αντιγραφή & Διπλασιασμός Πίνακα Pivot
url: /el/net/pivot-tables/create-new-excel-workbook-copy-duplicate-pivot-table/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία Νέου Φύλλου Excel – Αντιγραφή & Διπλασιασμός Πίνακα Pivot

Έχετε χρειαστεί ποτέ να **create new Excel workbook** που μεταφέρει έναν σύνθετο πίνακα pivot από ένα υπάρχον αρχείο; Δεν είστε μόνοι—πολλοί προγραμματιστές αντιμετωπίζουν αυτό το εμπόδιο όταν αυτοματοποιούν τις διαδικασίες αναφοράς. Τα καλά νέα είναι ότι με λίγες γραμμές C# και τη βιβλιοθήκη Aspose.Cells μπορείτε γρήγορα να **how to copy pivot**, **duplicate pivot table**, και **save workbook as new** χωρίς να ανοίξετε το Excel χειροκίνητα.

Σε αυτόν τον οδηγό θα περάσουμε από όλη τη διαδικασία, από τη φόρτωση του πηγαίου φύλλου μέχρι την αποθήκευση της αντιγραφής. Στο τέλος θα έχετε ένα έτοιμο‑για‑εκτέλεση snippet που μπορείτε να ενσωματώσετε σε οποιοδήποτε .NET project. Χωρίς περιττά, μόνο μια πρακτική λύση που μπορείτε να δοκιμάσετε σήμερα.

## Τι Καλύπτει Αυτό το Σεμινάριο

* **Prerequisites** – .NET 6+ (ή .NET Framework 4.6+), Visual Studio, και το πακέτο NuGet Aspose.Cells for .NET.
* Κώδικας βήμα‑βήμα που **creates new Excel workbook**, αντιγράφει το pivot, και γράφει το αποτέλεσμα στο δίσκο.
* Επεξηγήσεις του **why** κάθε γραμμή είναι σημαντική, όχι μόνο του **what** κάνει.
* Συμβουλές για την αντιμετώπιση edge cases όπως κρυφά worksheets ή μεγάλα εύρη δεδομένων.
* Μια γρήγορη ματιά στο **how to copy worksheet** αν χρειαστεί ποτέ να αντιγράψετε ολόκληρο το φύλλο αντί μόνο του pivot.

Έτοιμοι; Ας βουτήξουμε.

![εικόνα δημιουργίας νέου φύλλου Excel](image.png "Διάγραμμα που δείχνει το πηγαίο φύλλο, την αντιγραφή pivot και το προορισμό")

## Step 1: Set Up the Project and Install Aspose.Cells

Πριν μπορέσουμε να **create new Excel workbook**, χρειαζόμαστε ένα project που να αναφέρει τη σωστή βιβλιοθήκη.

```csharp
// Install the Aspose.Cells package via NuGet:
//   dotnet add package Aspose.Cells
using Aspose.Cells;   // Provides Workbook, Worksheet, Range, etc.
using System;        // For basic .NET types
```

*Why this matters:* Η Aspose.Cells λειτουργεί εξ ολοκλήρου στη μνήμη, έτσι δεν χρειάζεται ποτέ να εκκινήσετε το Excel στον server. Διατηρεί επίσης τις πληροφορίες του pivot cache, που είναι απαραίτητες για έναν αληθινό **duplicate pivot table**.

> **Pro tip:** Αν στοχεύετε σε .NET Core, βεβαιωθείτε ότι το runtime identifier (RID) του project ταιριάζει με την πλατφόρμα στην οποία θα αναπτυχθεί· διαφορετικά μπορεί να αντιμετωπίσετε σφάλματα φόρτωσης εγγενών βιβλιοθηκών.

## Step 2: Load the Source Workbook that Holds the Pivot

Τώρα θα **how to copy pivot** από ένα υπάρχον αρχείο. Το πηγαίο workbook μπορεί να βρίσκεται οπουδήποτε στον δίσκο, σε stream ή ακόμη και σε byte array.

```csharp
// Step 2: Load the source workbook that contains the pivot table
string sourcePath = @"C:\Reports\source.xlsx";
Workbook sourceWorkbook = new Workbook(sourcePath);

// Grab the first worksheet (adjust the index if your pivot lives elsewhere)
Worksheet sourceSheet = sourceWorkbook.Worksheets[0];

// Define the range that encloses the pivot table – A1:D20 in this example
Range sourceRange = sourceSheet.Cells.CreateRange("A1:D20");
```

*Why we pick a range:* Ένας πίνακας pivot ζει μέσα σε ένα κανονικό εύρος κελιών, αλλά έχει επίσης κρυφά δεδομένα cache συνδεδεμένα με το φύλλο. Αντιγράφοντας το εύρος **including the pivot**, η Aspose.Cells εξασφαλίζει ότι το cache μεταφέρεται μαζί του, δίνοντάς σας ένα λειτουργικό **duplicate pivot table** στο αρχείο προορισμού.

## Step 3: Create a New Excel Workbook to Receive the Copied Data

Εδώ είναι που πραγματικά **create new Excel workbook** που θα φιλοξενήσει το αντιγραμμένο pivot.

```csharp
// Step 3: Create a fresh workbook (empty) for the destination
Workbook destinationWorkbook = new Workbook(); // Starts with a default empty sheet
Worksheet destinationSheet = destinationWorkbook.Worksheets[0];

// Destination starts at A1 – you could offset if you need space for other data
Range destinationRange = destinationSheet.Cells.CreateRange("A1");
```

> **Why a fresh workbook?** Ξεκινώντας από ένα καθαρό φύλλο εγγυάται ότι δεν υπάρχουν υπολειπόμενες μορφοποιήσεις ή κρυφά αντικείμενα που να επηρεάζουν το αντιγραμμένο pivot. Επίσης κάνει το τελικό αρχείο μικρότερο, κάτι χρήσιμο για αυτοματοποιημένα email attachments.

## Step 4: Copy the Pivot Range to the New Workbook

Τώρα εκτελούμε την πραγματική λειτουργία **how to copy pivot**.

```csharp
// Step 4: Copy the range (including the pivot) from source to destination
sourceRange.Copy(destinationRange);
```

Αυτή η μοναδική γραμμή κάνει το σκληρό κομμάτι:

* Οι τιμές των κελιών, οι τύποι και η μορφοποίηση μεταφέρονται.
* Το pivot cache διπλασιάζεται, ώστε το νέο pivot να παραμένει πλήρως λειτουργικό.
* Οποιεσδήποτε σχετικές αναφορές μέσα στο pivot προσαρμόζονται αυτόματα στη νέα θέση.

### Handling Edge Cases

* **Hidden worksheets:** Αν το πηγαίο φύλλο είναι κρυφό, το pivot αντιγράφεται κανονικά, αλλά ίσως θέλετε να εμφανίσετε το φύλλο προορισμού για οπτική ευκολία:
  ```csharp
  destinationSheet.IsVisible = true;
  ```
* **Large data sets:** Για εύρη μεγαλύτερα από μερικές χιλιάδες γραμμές, σκεφτείτε να χρησιμοποιήσετε `CopyTo` με `CopyOptions` για να ρέξετε τη λειτουργία και να μειώσετε την πίεση μνήμης.

## Step 5: Save the Destination Workbook as a New File

Τέλος, **save workbook as new** και επαληθεύουμε το αποτέλεσμα.

```csharp
// Step 5: Save the destination workbook with the duplicated pivot table
string destPath = @"C:\Reports\copied.xlsx";
destinationWorkbook.Save(destPath, SaveFormat.Xlsx);

// Quick verification – open the file manually or read a cell value
Console.WriteLine($"Workbook saved to {destPath}");
```

Αν ανοίξετε το `copied.xlsx` θα δείτε ένα ακριβές αντίγραφο του αρχικού pivot, έτοιμο για περαιτέρω επεξεργασία ή διανομή.

### Optional: How to Copy Worksheet Instead of Just the Pivot

Μερικές φορές θέλετε ολόκληρο το φύλλο, όχι μόνο το pivot. Το ίδιο API το κάνει τετριμμένο:

```csharp
// Copy the whole worksheet (including all charts, tables, etc.)
sourceSheet.CopyTo(destinationWorkbook, 0); // Inserts at index 0
destinationWorkbook.Save(@"C:\Reports\full_copy.xlsx");
```

Αυτό ικανοποιεί το ερώτημα **how to copy worksheet** και μπορεί να φανεί χρήσιμο όταν χρειάζεται να διατηρήσετε πρόσθετες ρυθμίσεις επιπέδου φύλλου.

## Full Working Example

Συνδυάζοντας όλα τα παραπάνω, εδώ είναι μια αυτόνομη εφαρμογή console που μπορείτε να μεταγλωττίσετε και να τρέξετε:

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Load source workbook
        string sourcePath = @"C:\Reports\source.xlsx";
        Workbook sourceWorkbook = new Workbook(sourcePath);
        Worksheet sourceSheet = sourceWorkbook.Worksheets[0];
        Range sourceRange = sourceSheet.Cells.CreateRange("A1:D20");

        // 2️⃣ Create destination workbook
        Workbook destinationWorkbook = new Workbook();
        Worksheet destinationSheet = destinationWorkbook.Worksheets[0];
        Range destinationRange = destinationSheet.Cells.CreateRange("A1");

        // 3️⃣ Copy the pivot (range)
        sourceRange.Copy(destinationRange);

        // 4️⃣ Save as new file
        string destPath = @"C:\Reports\copied.xlsx";
        destinationWorkbook.Save(destPath, SaveFormat.Xlsx);

        Console.WriteLine($"✅ Successfully created new Excel workbook with duplicated pivot table at {destPath}");
    }
}
```

**Expected output:** Η κονσόλα εκτυπώνει ένα μήνυμα επιτυχίας, και το `copied.xlsx` εμφανίζεται στο `C:\Reports` με ένα λειτουργικό pivot που είναι ταυτόσημο με αυτό του `source.xlsx`.

## Common Questions & Pitfalls

* **Will formulas inside the pivot break?** Όχι—επειδή το pivot cache μεταφέρεται με το εύρος, όλα τα υπολογιζόμενα πεδία παραμένουν αμετάβλητα.
* **What if the source pivot uses external data connections?** Αυτές οι συνδέσεις *δεν* αντιγράφονται. Θα χρειαστεί να τις επαναδημιουργήσετε στο workbook προορισμού ή να μετατρέψετε το pivot σε στατικό πίνακα πρώτα.
* **Can I copy multiple pivots at once?** Απολύτως—απλώς ορίστε ένα μεγαλύτερο εύρος που να περιλαμβάνει όλα τα pivots, ή κάντε βρόχο σε κάθε αντικείμενο `PivotTable` στο `sourceSheet.PivotTables` και αντιγράψτε τα ξεχωριστά.
* **Do I need to dispose of the `Workbook` objects?** Τα αντικείμενα υλοποιούν το `IDisposable`, οπότε η χρήση τους μέσα σε `using` statements είναι καλή πρακτική, ειδικά σε υπηρεσίες υψηλής διακίνησης.

## Conclusion

Τώρα ξέρετε **how to create new Excel workbook**, πώς να αντιγράψετε ένα pivot, **duplicate pivot table**, και **save workbook as new** χρησιμοποιώντας C# και Aspose.Cells. Τα βήματα είναι απλά: φόρτωση, δημιουργία, αντιγραφή και αποθήκευση. Με το προαιρετικό snippet **how to copy worksheet** έχετε επίσης μια εναλλακτική λύση για πλήρη αντιγραφή φύλλου.

Επόμενα βήματα, μπορείτε να εξερευνήσετε:

* Προσθήκη προσαρμοσμένης μορφοποίησης στο αντιγραμμένο pivot.
* Ανανέωση του pivot cache προγραμματιστικά μετά από αλλαγές δεδομένων.
* Εξαγωγή του workbook σε PDF ή CSV για downstream συστήματα.

Δοκιμάστε το, προσαρμόστε το εύρος, και αφήστε την αυτοματοποίηση να αφαιρέσει το βαρετό έργο από τη ροή αναφοράς σας. Καλή προγραμματιστική! 

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}