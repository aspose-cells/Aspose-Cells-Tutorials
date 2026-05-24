---
category: general
date: 2026-05-23
description: Μάθετε πώς να εξάγετε έναν συγκεντρωτικό πίνακα ως εικόνα και να αποθηκεύσετε
  τον συγκεντρωτικό πίνακα ως φωτογραφία χρησιμοποιώντας το Aspose.Cells σε C#. Κώδικας
  βήμα‑βήμα και συμβουλές.
draft: false
keywords:
- export pivot table as image
- save pivot table as picture
language: el
og_description: Εξαγωγή συγκεντρωτικού πίνακα ως εικόνα και αποθήκευση του συγκεντρωτικού
  πίνακα ως εικόνα χρησιμοποιώντας το Aspose.Cells. Πλήρης κώδικας, εξήγηση και βέλτιστες
  πρακτικές.
og_title: Εξαγωγή Πίνακα Pivot ως Εικόνα με C# – Πλήρης Οδηγός
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: Learn how to export pivot table as image and save pivot table as picture
    using Aspose.Cells in C#. Step‑by‑step code and tips.
  headline: Export Pivot Table as Image with C# – Complete Guide
  type: TechArticle
- description: Learn how to export pivot table as image and save pivot table as picture
    using Aspose.Cells in C#. Step‑by‑step code and tips.
  name: Export Pivot Table as Image with C# – Complete Guide
  steps:
  - name: '**.NET 6+** (or .NET Framework 4.6+ if you prefer classic) installed.'
    text: '**.NET 6+** (or .NET Framework 4.6+ if you prefer classic) installed.'
  - name: A **license** for Aspose.Cells — the free evaluation works fine for testing,
      but a license removes the evaluation watermark.
    text: A **license** for Aspose.Cells — the free evaluation works fine for testing,
      but a license removes the evaluation watermark.
  - name: An Excel file (`Sample.xlsx`) that contains at least one pivot table on
      a sheet named *Sheet1* (you can rename it later).
    text: An Excel file (`Sample.xlsx`) that contains at least one pivot table on
      a sheet named *Sheet1* (you can rename it later).
  - name: '**Dispose Resources:** Wrap the `Workbook` in a `using` block or call `workbook.Dispose()`
      to free memory, especially when processing large files.'
    text: '**Dispose Resources:** Wrap the `Workbook` in a `using` block or call `workbook.Dispose()`
      to free memory, especially when processing large files.'
  - name: '**Thread Safety:** Each thread should have its own `Workbook` instance;
      Aspose.Cells objects are not thread‑safe.'
    text: '**Thread Safety:** Each thread should have its own `Workbook` instance;
      Aspose.Cells objects are not thread‑safe.'
  - name: '**Logging:** Log the export path and any exceptions to a central log file
      for easier troubleshooting.'
    text: '**Logging:** Log the export path and any exceptions to a central log file
      for easier troubleshooting.'
  - name: '**Batch Processing:** If you need to generate images for dozens of workbooks,
      consider a queue system (e.g., Azure Queue) to spread the load.'
    text: '**Batch Processing:** If you need to generate images for dozens of workbooks,
      consider a queue system (e.g., Azure Queue) to spread the load.'
  type: HowTo
tags:
- C#
- Aspose.Cells
- Excel automation
- PivotTable
- Image export
title: Εξαγωγή Πίνακα Pivot ως Εικόνα με C# – Πλήρης Οδηγός
url: /el/net/pivot-tables/export-pivot-table-as-image-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή Πίνακα Pivot ως Εικόνα με C# – Πλήρης Οδηγός

Έχετε αναρωτηθεί ποτέ πώς να **εξάγετε πίνακα pivot ως εικόνα** απευθείας από ένα βιβλίο εργασίας του Excel χωρίς να τραβήξετε στιγμιότυπο οθόνης; Δεν είστε οι μόνοι. Σε πολλές περιπτώσεις αναφοράς—σκεφτείτε αυτοματοποιημένα dashboards ή συνημμένα σε email—το να έχετε μια καθαρή εικόνα ενός πίνακα pivot είναι πολύ πιο βολικό από ένα ακατέργαστο αρχείο `.xlsx`.  

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα τις ακριβείς ενέργειες για **εξαγωγή πίνακα pivot ως εικόνα** και επίσης θα καλύψουμε την λεπτή τέχνη του **αποθήκευσης πίνακα pivot ως εικόνα** χρησιμοποιώντας τη δυνατή βιβλιοθήκη Aspose.Cells. Στο τέλος θα έχετε ένα αυτόνομο, εκτελέσιμο πρόγραμμα C# που δημιουργεί ένα αρχείο PNG ακριβώς εκεί που το χρειάζεστε.

## Τι Καλύπτει Αυτός ο Οδηγός

- Δημιουργία ενός .NET project με Aspose.Cells  
- Φόρτωση υπάρχοντος βιβλίου εργασίας και εντοπισμός του επιθυμητού πίνακα pivot  
- Διαμόρφωση επιλογών εξαγωγής εικόνας (ανάλυση, μορφή κ.λπ.)  
- Πραγματική εξαγωγή του πίνακα pivot ως αρχείο εικόνας PNG  
- Συνηθισμένα προβλήματα—όπως η διαχείριση κρυφών φύλλων ή πολλαπλών pivot—και πώς να τα αποφύγετε  

Χωρίς εξωτερικά scripts, χωρίς χειροκίνητη παρέμβαση, μόνο καθαρός κώδικας που μπορείτε να αντιγράψετε‑και‑επικολλήσετε και να εκτελέσετε.

## Προαπαιτούμενα

Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε:

1. **.NET 6+** (ή .NET Framework 4.6+ αν προτιμάτε την κλασική έκδοση) εγκατεστημένο.  
2. Μια **άδεια** για το Aspose.Cells — η δωρεάν αξιολόγηση λειτουργεί καλά για δοκιμές, αλλά μια άδεια αφαιρεί το υδατογράφημα αξιολόγησης.  
3. Ένα αρχείο Excel (`Sample.xlsx`) που περιέχει τουλάχιστον έναν πίνακα pivot σε φύλλο με όνομα *Sheet1* (μπορείτε να το μετονομάσετε αργότερα).  

Αν λείπει κάποιο από αυτά, κατεβάστε το πιο πρόσφατο πακέτο Aspose.Cells NuGet:

```bash
dotnet add package Aspose.Cells
```

Τώρα που όλα είναι έτοιμα, ας βάλουμε τα χέρια μας στη δουλειά.

## Βήμα 1: Φόρτωση του Βιβλίου Εργασίας και Λήψη του Φύλλου

Πρώτα απ' όλα: πρέπει να ανοίξουμε το βιβλίο εργασίας και να εντοπίσουμε το φύλλο που φιλοξενεί τον πίνακα pivot. Αυτό το βήμα είναι η βάση για **εξαγωγή πίνακα pivot ως εικόνα** επειδή χωρίς ένα έγκυρο αντικείμενο `Worksheet` η βιβλιοθήκη δεν μπορεί να εντοπίσει το pivot.

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

class Program
{
    static void Main()
    {
        // Path to the Excel file containing the pivot table
        string workbookPath = @"C:\Data\Sample.xlsx";

        // Load the workbook
        Workbook workbook = new Workbook(workbookPath);

        // Obtain the worksheet that contains the pivot table
        // Replace "Sheet1" with your actual sheet name if different
        Worksheet ws = workbook.Worksheets["Sheet1"];
```

> **Γιατί είναι σημαντικό:** Το Aspose.Cells διαβάζει ολόκληρο το βιβλίο εργασίας στη μνήμη, έτσι οποιοδήποτε τυπογραφικό λάθος στο όνομα του φύλλου προκαλεί `ArgumentException`. Πάντα βεβαιωθείτε ότι το φύλλο υπάρχει πριν προχωρήσετε.

## Βήμα 2: Πρόσβαση στον Επιθυμητό Πίνακα Pivot

Ένα βιβλίο εργασίας μπορεί να φιλοξενεί πολλαπλά pivots, αλλά για τις περισσότερες απλές περιπτώσεις χρειάζεται μόνο το πρώτο. Αν έχετε πολλά, μπορείτε να κάνετε επανάληψη πάνω στο `ws.PivotTables` και να επιλέξετε με βάση το όνομα.

```csharp
        // Access the first pivot table in the worksheet
        // If you know the pivot's name, you can use ws.PivotTables["MyPivot"]
        PivotTable pivot = ws.PivotTables[0];
```

> **Συμβουλή:** Όταν έχετε περισσότερα από ένα pivots, χρησιμοποιήστε `ws.PivotTables["PivotName"]` για να αποφύγετε την τυχαία εξαγωγή του λάθος πίνακα.

## Βήμα 3: Διαμόρφωση Επιλογών Εξαγωγής Εικόνας

Το Aspose.Cells σας παρέχει λεπτομερή έλεγχο της εξόδου εικόνας. Εδώ θα ορίσουμε τη μορφή σε PNG, αλλά μπορείτε να αλλάξετε σε JPEG ή BMP τροποποιώντας το `ImageFormat`. Μπορείτε επίσης να ρυθμίσετε DPI, κλίμακα και αν θα συμπεριληφθούν οι γραμμές πλέγματος.

```csharp
        // Set up image export options (PNG format)
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
        {
            ImageFormat = ImageFormat.Png,
            // Optional: increase resolution for sharper output
            // HorizontalResolution = 300,
            // VerticalResolution = 300,
            // Transparent = true   // if you need a transparent background
        };
```

> **Γιατί επιλέγουμε PNG:** Το PNG διατηρεί την ευκρίνεια του κειμένου και υποστηρίζει διαφάνεια, καθιστώντας το ιδανικό για ενσωμάτωση σε αναφορές ή ιστοσελίδες.

## Βήμα 4: Εξαγωγή του Πίνακα Pivot ως Αρχείο Εικόνας

Τώρα συμβαίνει η μαγεία. Η μέθοδος `ToImage` γράφει τον πίνακα pivot στο δίσκο στη μορφή που διαμορφώσαμε. Αυτό είναι ο πυρήνας του **αποθήκευσης πίνακα pivot ως εικόνα**.

```csharp
        // Define the output path – make sure the directory exists
        string outputPath = @"C:\Exports\pivot.png";

        // Export the pivot table as an image file
        pivot.ToImage(outputPath, imageOptions);

        System.Console.WriteLine($"Pivot table exported successfully to: {outputPath}");
    }
}
```

> **Ακραία περίπτωση:** Αν ο φάκελος προορισμού δεν υπάρχει, το `ToImage` πετάει `DirectoryNotFoundException`. Δημιουργήστε πρώτα το φάκελο ή χρησιμοποιήστε `Directory.CreateDirectory(Path.GetDirectoryName(outputPath))`.

## Βήμα 5: Επαλήθευση του Αποτελέσματος

Τρέξτε το πρόγραμμα (F5 στο Visual Studio ή `dotnet run` από τη γραμμή εντολών). Μεταβείτε στο `C:\Exports\pivot.png` και θα πρέπει να δείτε ένα καθαρό στιγμιότυπο του πίνακα pivot, ταυτόσημο με αυτό που βλέπετε στο Excel.

![παράδειγμα εξαγωγής πίνακα pivot ως εικόνα](https://example.com/images/pivot-export.png "παράδειγμα εξαγωγής πίνακα pivot ως εικόνα")

*Κείμενο alt εικόνας: παράδειγμα εξαγωγής πίνακα pivot ως εικόνα*

Αν η εικόνα φαίνεται κομμένη, προσαρμόστε τις ιδιότητες `ImageOrPrintOptions` `HorizontalResolution`, `VerticalResolution`, ή `OnePagePerSheet`. Αυτές οι ρυθμίσεις σας επιτρέπουν να **αποθηκεύσετε πίνακα pivot ως εικόνα** με τις ακριβείς διαστάσεις που χρειάζεστε.

## Συχνές Ερωτήσεις & Προβλήματα

| Ερώτηση | Απάντηση |
|----------|--------|
| **Μπορώ να εξάγω πολλαπλά pivots ταυτόχρονα;** | Κάντε επανάληψη στο `ws.PivotTables` και καλέστε `ToImage` για κάθε ένα, αλλάζοντας το όνομα αρχείου εξόδου κάθε φορά. |
| **Τι γίνεται αν το pivot περιέχει γραφήματα;** | Τα γραφήματα δεν αποτελούν μέρος της περιοχής δεδομένων του pivot, επομένως δεν θα εμφανιστούν. Εξάγετε το γράφημα ξεχωριστά χρησιμοποιώντας `Chart.ToImage`. |
| **Λειτουργεί αυτό με βιβλία εργασίας προστατευμένα με κωδικό;** | Ναι—φορτώστε το βιβλίο εργασίας με `Workbook(workbookPath, new LoadOptions { Password = "secret" })`. |
| **Πώς αλλάζω το χρώμα φόντου;** | Ορίστε `imageOptions.BackgroundColor = Color.White;` (ή οποιοδήποτε `System.Drawing.Color`). |
| **Υπάρχει τρόπος εξαγωγής σε JPEG για μικρότερο μέγεθος αρχείου;** | Αλλάξτε `ImageFormat = ImageFormat.Jpeg` και προαιρετικά ορίστε `imageOptions.JpegQuality = 80`. |

## Επαγγελματικές Συμβουλές για Εξαγωγή Έτοιμη για Παραγωγή

1. **Απελευθέρωση Πόρων:** Τυλίξτε το `Workbook` σε ένα μπλοκ `using` ή καλέστε `workbook.Dispose()` για να ελευθερώσετε μνήμη, ειδικά όταν επεξεργάζεστε μεγάλα αρχεία.  
2. **Ασφάλεια Νήματος:** Κάθε νήμα πρέπει να έχει το δικό του αντικείμενο `Workbook`; τα αντικείμενα Aspose.Cells δεν είναι thread‑safe.  
3. **Καταγραφή (Logging):** Καταγράψτε τη διαδρομή εξαγωγής και τυχόν εξαιρέσεις σε ένα κεντρικό αρχείο καταγραφής για ευκολότερη αντιμετώπιση προβλημάτων.  
4. **Επεξεργασία σε Παρτίδες:** Αν χρειάζεται να δημιουργήσετε εικόνες για δεκάδες βιβλία εργασίας, σκεφτείτε ένα σύστημα ουράς (π.χ., Azure Queue) για κατανομή του φορτίου.  

## Πλήρες Παράδειγμα Λειτουργίας

Ακολουθεί το πλήρες πρόγραμμα ξανά, έτοιμο για αντιγραφή‑και‑επικόλληση:

```csharp
using Aspose.Cells;
using System;
using System.Drawing.Imaging;
using System.IO;

class ExportPivotImage
{
    static void Main()
    {
        // 1️⃣ Load workbook
        string workbookPath = @"C:\Data\Sample.xlsx";
        Workbook workbook = new Workbook(workbookPath);

        // 2️⃣ Get worksheet containing the pivot
        Worksheet ws = workbook.Worksheets["Sheet1"]; // adjust if needed

        // 3️⃣ Grab the first pivot table
        if (ws.PivotTables.Count == 0)
        {
            Console.WriteLine("No pivot tables found on the sheet.");
            return;
        }
        PivotTable pivot = ws.PivotTables[0];

        // 4️⃣ Set image export options (PNG is default)
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
        {
            ImageFormat = ImageFormat.Png,
            // Uncomment to increase DPI for sharper images
            // HorizontalResolution = 300,
            // VerticalResolution = 300
        };

        // 5️⃣ Ensure output directory exists
        string outputDir = @"C:\Exports";
        Directory.CreateDirectory(outputDir);
        string outputPath = Path.Combine(outputDir, "pivot.png");

        // 6️⃣ Export pivot table as image
        pivot.ToImage(outputPath, imageOptions);

        Console.WriteLine($"Pivot table exported successfully to: {outputPath}");
    }
}
```

Η εκτέλεση αυτού του κώδικα θα δημιουργήσει ένα αρχείο PNG με όνομα `pivot.png` στο `C:\Exports`. Ανοίξτε το με οποιονδήποτε προβολέα εικόνων και θα δείτε μια ακριβή οπτική αναπαραγωγή του πίνακα pivot—ιδανική για αναφορές, email ή ιστοσελίδες.

## Συμπέρασμα

Μόλις καλύψαμε όλα όσα χρειάζεστε για **εξαγωγή πίνακα pivot ως εικόνα** και **αποθήκευση πίνακα pivot ως εικόνα** χρησιμοποιώντας C# και Aspose.Cells. Από τη φόρτωση του βιβλίου εργασίας μέχρι τη λεπτομερή ρύθμιση των επιλογών εικόνας, η διαδικασία είναι απλή και πλήρως αυτοματοποιήσιμη.  

Επόμενα βήματα; Δοκιμάστε άλλα φορμά (JPEG, BMP), αυξήστε το DPI για γραφικά εκτύπωσης, ή επεξεργαστείτε σε παρτίδες έναν φάκελο βιβλίων εργασίας. Μπορείτε επίσης να εξερευνήσετε την εξαγωγή ολόκληρου του φύλλου ως εικόνα αν χρειάζεστε το περιβάλλον γύρω του.  

Έχετε περισσότερες ερωτήσεις ή ένα δύσκολο σενάριο; Αφήστε ένα σχόλιο παρακάτω, και καλές προγραμματιστικές στιγμές!

## Σχετικά Μαθήματα

- [Δημιουργία Πίνακα Pivot στο Excel Χρησιμοποιώντας Aspose.Cells για .NET](/cells/english/net/pivot-tables/create-pivot-table/)
- [Πώς να Αλλάξετε τα Δεδομένα Πηγής του Πίνακα Pivot Χρησιμοποιώντας Aspose.Cells για .NET | Οδηγός Ανάλυσης Δεδομένων](/cells/english/net/data-analysis/change-pivot-table-source-aspose-cells-net/)
- [Αριστεία Διαμόρφωση Πίνακα Pivot σε .NET Χρησιμοποιώντας Aspose.Cells](/cells/english/net/formatting/format-pivot-tables-dotnet-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}