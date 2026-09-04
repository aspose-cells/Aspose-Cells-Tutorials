---
category: general
date: 2026-02-14
description: Αντιγράψτε γραμμές στο Excel και διατηρήστε τον Πίνακα Pivot σε μία κίνηση.
  Μάθετε πώς να αντιγράψετε γραμμές, να αντιγράψετε περιοχή σε φύλλο και να διπλασιάσετε
  γραμμές με Pivot χρησιμοποιώντας το Aspose.Cells.
draft: false
keywords:
- copy rows excel
- preserve pivot table
- how to copy rows
- copy range to sheet
- duplicate rows with pivot
language: el
og_description: Αντιγράψτε γραμμές στο Excel και διατηρήστε τον Πίνακα Pivot σε μία
  ενέργεια. Ακολουθήστε αυτόν τον οδηγό βήμα‑βήμα για να αντιγράψετε γραμμές με Pivot
  χρησιμοποιώντας C#.
og_title: Αντιγραφή γραμμών Excel – Διατήρηση του Πίνακα Pivot κατά την Αντιγραφή
  Γραμμών
tags:
- Aspose.Cells
- C#
- Excel automation
title: Αντιγραφή γραμμών Excel – Διατήρηση του Πίνακα Pivot κατά την Αντιγραφή Γραμμών
url: /el/net/pivot-tables/copy-rows-excel-preserve-pivot-table-while-duplicating-rows/
---

or build a temporary worksheet that consolidates the ranges before copying.

Translate but keep code formatting.

## Conclusion

Translate heading.

Paragraph.

We need to translate but keep keywords.

Ready for the next challenge? Try extending the code to:

- Export the duplicated sheet as a PDF.  
- Refresh the pivot programmatically after copying.  
- Loop over a list of source files and batch‑process them.

Translate bullet list.

If you hit any snags, drop a comment below or ping me on GitHub. Happy coding, and enjoy the time you saved by not dragging Excel around manually!  

Image line: keep unchanged.

Finally closing shortcodes.

Now produce final content.

Let's craft Greek translation.

Be careful with bold markup and code formatting.

Proceed.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# copy rows excel – Διατήρηση Πίνακα Pivot Κατά την Αντιγραφή Γραμμών

Έχετε χρειαστεί ποτέ να **copy rows excel** ενώ διατηρείτε τον πίνακα pivot αμετάβλητο; Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα μια πλήρη, εκτελέσιμη λύση που σας δείχνει **πώς να αντιγράψετε γραμμές**, να διατηρήσετε τη λειτουργία **preserve pivot table**, και ακόμη **να αντιγράψετε γραμμές με pivot** σε διαφορετικά φύλλα χρησιμοποιώντας το Aspose.Cells for .NET.

Φανταστείτε ότι δημιουργείτε μια μηνιαία αναφορά πωλήσεων που αντλεί δεδομένα από ένα κύριο φύλλο, εκτελεί έναν pivot και στη συνέχεια πρέπει να στείλετε μια περιορισμένη έκδοση σε έναν συνεργάτη. Η χειροκίνητη αντιγραφή της περιοχής είναι επίπονη και υπάρχει κίνδυνος να σπάσει ο pivot. Τα καλά νέα; Μερικές γραμμές C# μπορούν να κάνουν τη βαριά δουλειά για εσάς—χωρίς κλικ του ποντικιού.

> **What you’ll get:** ένα πλήρες δείγμα κώδικα, εξηγήσεις βήμα‑βήμα, συμβουλές για ακραίες περιπτώσεις και έναν γρήγορο έλεγχο λογικής για να επαληθεύσετε ότι ο pivot επέζησε της αντιγραφής.

---

## What You’ll Need

- **Aspose.Cells for .NET** (το δωρεάν πακέτο NuGet λειτουργεί άψογα για αυτή τη demo).  
- Μια πρόσφατη **.NET runtime** (4.7+ ή .NET 6/7).  
- Ένα αρχείο Excel (`source.xlsx`) που περιέχει έναν πίνακα pivot στο πρώτο φύλλο εργασίας.  
- Visual Studio, Rider ή οποιονδήποτε επεξεργαστή C# προτιμάτε.

Δεν απαιτούνται πρόσθετες βιβλιοθήκες, κανένα COM interop και καμία εγκατάσταση Excel στον διακομιστή. Γι’ αυτό ο τρόπος αυτός είναι τόσο φιλικός προς το **copy range to sheet** όσο και ασφαλής για server.

## Step 1 – Load the Workbook (copy rows excel)

Το πρώτο βήμα είναι να ανοίξετε το πηγαίο workbook. Η χρήση του Aspose.Cells μας παρέχει ένα καθαρό object model που λειτουργεί το ίδιο σε Windows, Linux ή Azure.

```csharp
using Aspose.Cells;

public class PivotCopyDemo
{
    public static void Main()
    {
        // Load the source workbook from disk
        Workbook sourceWorkbook = new Workbook(@"YOUR_DIRECTORY\source.xlsx");
```

> **Why this matters:** η φόρτωση του workbook δημιουργεί μια αναπαράσταση στη μνήμη για κάθε φύλλο εργασίας, συμπεριλαμβανομένων κρυφών αντικειμένων όπως οι pivot caches. Μόλις το αρχείο είναι στη μνήμη, μπορούμε να χειριστούμε τις γραμμές χωρίς να αγγίξουμε ποτέ το UI.

## Step 2 – Identify Destination Worksheet (copy range to sheet)

Θέλουμε οι αντιγραμμένες γραμμές να καταλήξουν σε διαφορετικό φύλλο—`Sheet2` σε αυτό το παράδειγμα. Αν το φύλλο δεν υπάρχει, το Aspose θα το δημιουργήσει για εσάς.

```csharp
        // Get (or create) the destination worksheet where the rows will be placed
        Worksheet destinationWorksheet;
        if (sourceWorkbook.Worksheets.Contains("Sheet2"))
            destinationWorksheet = sourceWorkbook.Worksheets["Sheet2"];
        else
            destinationWorksheet = sourceWorkbook.Worksheets.Add("Sheet2");
```

> **Pro tip:** ελέγχετε πάντα το `Worksheets.Contains` πριν προσθέσετε ένα φύλλο· διαφορετικά θα καταλήξετε με διπλά ονόματα και εξαίρεση χρόνου εκτέλεσης.

## Step 3 – Copy Rows While Preserving the Pivot Table

Τώρα έρχεται η ουσία: αντιγραφή των γραμμών **A1:E20** (που περιλαμβάνουν τον pivot) από το πρώτο φύλλο στο `Sheet2`. Η μέθοδος `CopyRows` αντιγράφει τα ακατέργαστα κελιά *και* την υποκείμενη pivot cache, ώστε ο pivot να παραμείνει λειτουργικός.

```csharp
        // Define the source range: rows 0‑19 (A1:E20) on the first worksheet
        Worksheet sourceWorksheet = sourceWorkbook.Worksheets[0];

        // Copy rows 0‑19 from source to destination, starting at row 0 on the destination sheet
        sourceWorksheet.Cells.CopyRows(
            sourceWorksheet.Cells,   // source cells collection
            0,                       // source start row (0‑based, i.e., row 1)
            0,                       // destination start row on the same sheet (adjust if needed)
            20);                     // total number of rows to copy
```

> **Why it works:** το `CopyRows` σέβεται την εσωτερική pivot cache, έτσι ο πίνακας pivot στο φύλλο προορισμού είναι ένα *ζωντανό* αντίγραφο, όχι ένα στατικό στιγμιότυπο. Αυτό ικανοποιεί την απαίτηση **preserve pivot table** χωρίς επιπλέον κώδικα.

Αν χρειάζεστε οι γραμμές να ξεκινήσουν από διαφορετικό offset στο φύλλο προορισμού—π.χ. γραμμή 10—απλώς αλλάξτε το τρίτο όρισμα σε `9`.

## Step 4 – Save the Workbook (duplicate rows with pivot)

Τέλος, γράψτε το τροποποιημένο workbook πίσω στο δίσκο. Ο πίνακας pivot θα είναι πλήρως λειτουργικός στο νέο αρχείο.

```csharp
        // Save the workbook; the copied pivot remains active automatically
        sourceWorkbook.Save(@"YOUR_DIRECTORY\copyWithPivot.xlsx");
    }
}
```

> **Result verification:** ανοίξτε το `copyWithPivot.xlsx` στο Excel, μεταβείτε στο *Sheet2* και ανανεώστε τον pivot. Θα πρέπει να δείτε την ίδια διάταξη πεδίων και υπολογισμούς όπως στο αρχικό—τίποτα δεν έχει σπάσει.

## Verifying the Copy – Quick sanity check

```csharp
// Optional: programmatically confirm the pivot exists on the destination sheet
Worksheet dest = sourceWorkbook.Worksheets["Sheet2"];
bool pivotExists = dest.PivotTables.Count > 0;
Console.WriteLine($"Pivot table copied? {pivotExists}");
```

Αν η κονσόλα εκτυπώσει `True`, έχετε ολοκληρώσει με επιτυχία το **duplicate rows with pivot** και διατηρήσατε τη μηχανή ανάλυσης δεδομένων ζωντανή.

## Common Edge Cases & How to Handle Them

| Situation | What to watch for | Suggested tweak |
|-----------|-------------------|-----------------|
| **Source range includes merged cells** | Τα συγχωνευμένα κελιά μπορεί να προκαλέσουν λανθασμένη στοίχιση κατά την αντιγραφή. | Χρησιμοποιήστε το `CopyRows` όπως φαίνεται· διατηρεί αυτόματα τις συγχωνεύσεις. |
| **Destination sheet already has data** | Οι νέες γραμμές μπορεί να αντικαταστήσουν υπάρχον περιεχόμενο. | Αλλάξτε τη γραμμή εκκίνησης προορισμού (τρίτο όρισμα) στην πρώτη κενή γραμμή: `destWorksheet.Cells.MaxDataRow + 1`. |
| **Pivot uses external data source** | Οι εξωτερικές συνδέσεις δεν αντιγράφονται. | Βεβαιωθείτε ότι το πηγαίο workbook περιέχει το πλήρες σύνολο δεδομένων· διαφορετικά επανασυνδέστε τη σύνδεση μετά την αντιγραφή. |
| **Large workbook (100k+ rows)** | Η χρήση μνήμης αυξάνεται δραματικά. | Σκεφτείτε να αντιγράψετε σε τμήματα (π.χ. 5.000 γραμμές τη φορά) για να κρατήσετε το GC ήρεμο. |

## Full Working Example (All Steps Together)

Παρακάτω βρίσκεται ολόκληρο το πρόγραμμα που μπορείτε να επικολλήσετε σε μια εφαρμογή console και να τρέξετε αμέσως.

```csharp
using System;
using Aspose.Cells;

public class PivotCopyDemo
{
    public static void Main()
    {
        // 1️⃣ Load the source workbook
        Workbook sourceWorkbook = new Workbook(@"YOUR_DIRECTORY\source.xlsx");

        // 2️⃣ Get (or create) the destination worksheet
        Worksheet destinationWorksheet;
        if (sourceWorkbook.Worksheets.Contains("Sheet2"))
            destinationWorksheet = sourceWorkbook.Worksheets["Sheet2"];
        else
            destinationWorksheet = sourceWorkbook.Worksheets.Add("Sheet2");

        // 3️⃣ Copy rows A1:E20 (includes pivot) from the first sheet
        Worksheet sourceWorksheet = sourceWorkbook.Worksheets[0];
        sourceWorksheet.Cells.CopyRows(
            sourceWorksheet.Cells, // source cells
            0,                     // start at row 0 (A1)
            0,                     // destination start row (adjust as needed)
            20);                   // copy 20 rows

        // 4️⃣ Save the workbook – pivot stays alive
        sourceWorkbook.Save(@"YOUR_DIRECTORY\copyWithPivot.xlsx");

        // Optional verification
        bool pivotExists = destinationWorksheet.PivotTables.Count > 0;
        Console.WriteLine($"Pivot table copied? {pivotExists}");
    }
}
```

Εκτελέστε το πρόγραμμα, ανοίξτε το παραγόμενο `copyWithPivot.xlsx` και θα δείτε ότι ο pivot στο **Sheet2** λειτουργεί ακριβώς όπως το αρχικό. Δεν απαιτείται χειροκίνητη επαναδημιουργία.

## Frequently Asked Questions

**Q: Does this work with Excel 2003‑compatible `.xls` files?**  
A: Ναι. Το Aspose.Cells αφαιρεί την εξάρτηση από τη μορφή αρχείου, έτσι ο ίδιος κώδικας λειτουργεί για `.xls`, `.xlsx` και ακόμη `.xlsb`.

**Q: What if I need to copy *columns* instead of rows?**  
A: Χρησιμοποιήστε το `CopyColumns` με παρόμοιο τρόπο· απλώς ανταλλάξτε τις παραμέτρους γραμμής με δείκτες στήλης.

**Q: Can I copy multiple, non‑contiguous ranges at once?**  
A: Δεν είναι δυνατόν άμεσα με το `CopyRows`. Επαναλάβετε τη διαδικασία για κάθε περιοχή ή δημιουργήστε ένα προσωρινό φύλλο που ενοποιεί τις περιοχές πριν την αντιγραφή.

## Conclusion

Δείξαμε ένα καθαρό μοτίβο **copy rows excel** που διατηρεί την ακεραιότητα του **preserve pivot table**, σας επιτρέπει να **πώς να αντιγράψετε γραμμές** αποδοτικά και δείχνει πώς να **copy range to sheet** χωρίς να χάσετε τη λειτουργικότητα του pivot. Στο τέλος αυτού του οδηγού θα πρέπει να νιώθετε σίγουροι για το **duplicate rows with pivot** σε οποιοδήποτε pipeline αυτοματοποίησης—είτε δημιουργείτε καθημερινές αναφορές είτε χτίζετε μια υπηρεσία εξαγωγής δεδομένων μεγάλης κλίμακας.

Έτοιμοι για την επόμενη πρόκληση; Δοκιμάστε να επεκτείνετε τον κώδικα ώστε:

- Εξαγωγή του αντιγραμμένου φύλλου ως PDF.  
- Ανανέωση του pivot προγραμματιστικά μετά την αντιγραφή.  
- Επανάληψη πάνω σε λίστα πηγαίων αρχείων και επεξεργασία τους σε batch.

Αν συναντήσετε δυσκολίες, αφήστε ένα σχόλιο παρακάτω ή στείλτε μου μήνυμα στο GitHub. Καλή προγραμματιστική δουλειά και απολαύστε τον χρόνο που κερδίσατε χωρίς να «σέρνετε» το Excel χειροκίνητα!  

<img src="copy-rows-excel.png" alt="copy rows excel diagram" style="max-width:100%; height:auto;" />

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}