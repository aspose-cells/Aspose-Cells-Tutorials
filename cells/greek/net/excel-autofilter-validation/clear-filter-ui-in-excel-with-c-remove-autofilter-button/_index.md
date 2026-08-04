---
category: general
date: 2026-02-09
description: Καθαρίστε το UI φίλτρου στο Excel με C# αφαιρώντας το κουμπί AutoFilter.
  Μάθετε πώς να κρύψετε το κουμπί φίλτρου, να εμφανίσετε τη γραμμή κεφαλίδας και να
  διατηρήσετε τα φύλλα σας τακτικά.
draft: false
keywords:
- clear filter UI
- remove autofilter excel
- how to remove autofilter
- show header row
- hide filter button
language: el
og_description: Καθαρό UI φίλτρου στο Excel με χρήση C#. Αυτός ο οδηγός δείχνει πώς
  να κρύψετε το κουμπί φίλτρου, να εμφανίσετε τη γραμμή κεφαλίδας και να διατηρήσετε
  τα φύλλα εργασίας καθαρά.
og_title: Καθαρισμός διεπαφής φίλτρου στο Excel με C# – Αφαίρεση του κουμπιού AutoFilter
tags:
- excel
- csharp
- epplus
- automation
title: Καθαρισμός διεπαφής φίλτρου στο Excel με C# – Αφαίρεση του κουμπιού AutoFilter
url: /el/net/excel-autofilter-validation/clear-filter-ui-in-excel-with-c-remove-autofilter-button/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Καθαρισμός UI φίλτρου στο Excel με C# – Αφαίρεση του κουμπιού AutoFilter

Κάποτε χρειάστηκε να **καθαρίσετε το UI του φίλτρου** σε ένα φύλλο Excel αλλά δεν ήξερες ποια γραμμή κώδικα κρύβει το μικρό αυτό βελάκι‑πτωσης; Δεν είσαι μόνος. Το κουμπί φίλτρου μπορεί να είναι ενοχλητικό όταν στέλνεις μια αναφορά σε τελικούς χρήστες που δεν χρειάζεται ποτέ να αλλάξουν την προβολή.

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από ένα πλήρες, εκτελέσιμο παράδειγμα που **αφαιρεί το κουμπί AutoFilter** από έναν πίνακα, διασφαλίζει ότι η γραμμή κεφαλίδας παραμένει ορατή, και ακόμη αγγίζει το πώς να *αποκρύψετε το κουμπί φίλτρου* μόνιμα. Στο τέλος θα ξέρεις ακριβώς **πώς να αφαιρέσεις το AutoFilter** σε C# και γιατί κάθε βήμα είναι σημαντικό.

## Τι θα χρειαστείς

- .NET 6+ (ή .NET Framework 4.7.2+) – οποιαδήποτε πρόσφατη έκδοση του runtime λειτουργεί.
- Το πακέτο **EPPlus** από NuGet (έκδοση 6.x ή νεότερη) – παρέχει τα `ExcelWorksheet`, `ExcelTable`, κ.λπ.
- Ένα απλό αρχείο Excel με έναν πίνακα που ονομάζεται **SalesTable** (δημιούργησέ το σε λίγα κλικ).

Αυτό είναι όλο. Χωρίς COM interop, χωρίς επιπλέον DLLs, μόνο μερικές `using` δηλώσεις και λίγες γραμμές κώδικα.

## Clear filter UI: Αφαίρεση του κουμπιού AutoFilter

Η ουσία της λύσης βρίσκεται σε τρεις μικρές δηλώσεις. Ας τις αναλύσουμε ώστε να καταλάβεις *γιατί* χρειάζονται, όχι μόνο *τι* κάνουν.

### Βήμα 1 – Πάρε μια αναφορά στον πίνακα

```csharp
// Step 1: Get a reference to the "SalesTable" in the first worksheet
ExcelTable salesTable = package.Workbook.Worksheets[0].Tables["SalesTable"];
```

Γιατί είναι σημαντικό: Το EPPlus δουλεύει με **πίνακες** (`ExcelTable`), όχι με ακατέργαστες περιοχές. Παίρνοντας το αντικείμενο του πίνακα αποκτούμε πρόσβαση στην ιδιότητα `AutoFilter`, η οποία ελέγχει το στοιχείο UI που βλέπεις στο φύλλο. Αν προσπαθήσεις να χειριστείς το φύλλο εργασίας απευθείας, θα επηρεάσεις μόνο τις τιμές, όχι το κουμπί φίλτρου.

### Βήμα 2 – Αφαίρεση της γραμμής του κουμπιού AutoFilter

```csharp
// Step 2: Remove the AutoFilter button row (clears any applied filter UI)
salesTable.AutoFilter = null;
```

Ορίζοντας το `AutoFilter` σε `null` λέμε στο EPPlus να διαγράψει τη βασική γραμμή φίλτρου. Αυτή είναι η λειτουργία *clear filter UI* που οι περισσότεροι προγραμματιστές ψάχνουν όταν ρωτούν “**πώς να αφαιρέσω το autofilter**”. Είναι μια καθαρή, μονογραμμή προσέγγιση που λειτουργεί σε οποιαδήποτε έκδοση Excel υποστηρίζεται από το EPPlus.

### Βήμα 3 – Διατήρηση της γραμμής κεφαλίδας ορατής

```csharp
// Step 3: Ensure the header row remains visible after removing the filter
salesTable.ShowHeader = true;
```

Όταν αφαιρέσεις το UI φίλτρου, το Excel μερικές φορές κρύβει τη γραμμή κεφαλίδας αν η σημαία `ShowHeader` του πίνακα είναι `false`. Ορίζοντας την ρητά σε `true` εγγυόμαστε ότι οι τίτλοι των στηλών παραμένουν στην οθόνη – μια λεπτή αλλά σημαντική λεπτομέρεια για μια επαγγελματική τελική αναφορά.

### Πλήρες, εκτελέσιμο παράδειγμα

Παρακάτω υπάρχει μια ελάχιστη εφαρμογή console που ανοίγει ένα υπάρχον βιβλίο εργασίας, εκτελεί τα τρία βήματα και αποθηκεύει το αποτέλεσμα. Αντέγραψε‑επικόλλησε, πάτα **F5**, και παρατήρησε το κουμπί φίλτρου να εξαφανίζεται.

```csharp
using System;
using System.IO;
using OfficeOpenXml;
using OfficeOpenXml.Table;

class Program
{
    static void Main()
    {
        // EPPlus requires a license context for non‑commercial use.
        ExcelPackage.LicenseContext = LicenseContext.NonCommercial;

        // 1️⃣ Load the workbook (replace with your own path)
        var filePath = Path.Combine(Environment.CurrentDirectory, "SalesReport.xlsx");
        if (!File.Exists(filePath))
        {
            Console.WriteLine($"File not found: {filePath}");
            return;
        }

        using var package = new ExcelPackage(new FileInfo(filePath));

        // 2️⃣ Get a reference to the table named "SalesTable"
        ExcelTable salesTable = package.Workbook.Worksheets[0].Tables["SalesTable"];
        if (salesTable == null)
        {
            Console.WriteLine("Table 'SalesTable' not found in the first worksheet.");
            return;
        }

        // 3️⃣ Remove the AutoFilter button (clear filter UI)
        salesTable.AutoFilter = null;

        // 4️⃣ Ensure the header row stays visible (show header row)
        salesTable.ShowHeader = true;

        // 5️⃣ Save the changes to a new file so you don’t overwrite the original
        var outputPath = Path.Combine(Environment.CurrentDirectory, "SalesReport_NoFilter.xlsx");
        package.SaveAs(new FileInfo(outputPath));

        Console.WriteLine($"Filter button removed. Saved to {outputPath}");
    }
}
```

**Αναμενόμενο αποτέλεσμα:** Άνοιξε το *SalesReport_NoFilter.xlsx* – τα βελάκια φίλτρου έχουν φύγει, αλλά οι επικεφαλίδες των στηλών παραμένουν. Δεν υπάρχει πλέον “κλικ‑για‑φίλτρο” UI που να αποσπά την προσοχή.

> **Pro tip:** Αν έχεις **πολλούς πίνακες** και θέλεις να κρύψεις το κουμπί φίλτρου για όλους, κάνε βρόχο μέσω `worksheet.Tables` και εφάρμοσε τις ίδιες τρεις γραμμές μέσα στον βρόχο.

## Πώς να αφαιρέσεις το AutoFilter στο Excel χρησιμοποιώντας C# – πιο βαθιά ανάλυση

Μπορεί να αναρωτιέσαι, “Τι γίνεται αν το βιβλίο εργασίας έχει ήδη εφαρμοσμένο φίλτρο; Καθορίζει το `AutoFilter = null` επίσης την εκκαθάριση των φιλτραρισμένων γραμμών;”. Η απάντηση είναι **ναι**. Το EPPlus καθαρίζει τόσο το UI όσο και τα κριτήρια του φίλτρου, αφήνοντας τα δεδομένα στην αρχική τους σειρά.

Αν θέλεις μόνο να *κρύψεις* το κουμπί αλλά να διατηρήσεις το φίλτρο ενεργό, μπορείς αντί αυτού να ορίσεις την ιδιότητα `AutoFilter` σε **νέο κενό φίλτρο**:

```csharp
salesTable.AutoFilter = new ExcelAutoFilter(); // hides button, retains filter logic
```

Αυτή η παραλλαγή είναι χρήσιμη όταν θέλεις να *κρύψεις το κουμπί φίλτρου* για πιο καθαρή εμφάνιση, αλλά εξακολουθείς να επιτρέπεις σε προχωρημένους χρήστες να ενεργοποιούν φίλτρα μέσω VBA ή της κορδέλας.

### Ακραία περίπτωση: Πίνακες χωρίς γραμμή κεφαλίδας

Ορισμένες παλαιότερες αναφορές χρησιμοποιούν απλές περιοχές αντί για πίνακες. Σε αυτήν την περίπτωση, το EPPlus δεν θα εκθέσει αντικείμενο `ExcelTable`, οπότε ο παραπάνω κώδικας θα πετάξει εξαίρεση. Η λύση είναι να **μετατρέψεις την περιοχή σε πίνακα** πρώτα:

```csharp
var range = worksheet.Cells["A1:D100"];
var table = worksheet.Tables.Add(range, "TempTable");
table.ShowHeader = true;    // ensure header is visible
table.AutoFilter = null;    // clear filter UI
```

Τώρα έχεις *αφαιρέσει το autofilter excel* UI ακόμη και σε μια περιοχή που ξεκίνησε χωρίς επίσημο πίνακα.

## Εμφάνιση της γραμμής κεφαλίδας μετά το κρύψιμο του κουμπιού φίλτρου – γιατί έχει σημασία

Ένα συχνό παράπονο είναι ότι μετά το κρύψιμο του UI φίλτρου, η γραμμή κεφαλίδας εξαφανίζεται, ειδικά όταν το βιβλίο εργασίας δημιουργήθηκε αρχικά με την επιλογή “Hide Header” ενεργοποιημένη. Ορίζοντας ρητά `salesTable.ShowHeader = true;` αποφεύγουμε αυτήν την έκπληξη.

Αν ποτέ χρειαστεί να **κρύψεις το κουμπί φίλτρου** αλλά να διατηρήσεις την κεφαλίδα κρυφή (π.χ. όταν δημιουργείς ένα ακατέργαστο αρχείο δεδομένων), απλώς όρισε `salesTable.ShowHeader = false;` μετά τον καθαρισμό του φίλτρου. Ο κώδικας είναι συμμετρικός, κάτι που τον κάνει εύκολο να εναλλάσσεται βάσει μιας ρύθμισης.

## Hide filter button – πρακτικές συμβουλές και παγίδες

- **Συμβατότητα εκδόσεων:** Το EPPlus 6+ λειτουργεί μόνο με αρχεία `.xlsx`. Αν δουλεύεις με παλαιότερη μορφή `.xls`, θα χρειαστείς διαφορετική βιβλιοθήκη (π.χ. NPOI) επειδή το API *clear filter UI* δεν είναι διαθέσιμο.
- **Απόδοση:** Η φόρτωση ενός τεράστιου βιβλίου εργασίας μόνο για να κρύψεις ένα κουμπί μπορεί να είναι αργή. Σκέψου να χρησιμοποιήσεις `ExcelPackage.Load(stream, true)` για άνοιγμα σε **read‑only** λειτουργία, κάνε την αλλαγή, και μετά αποθήκευσε.
- **Δοκιμές:** Πάντα να επαληθεύεις το παραγόμενο αρχείο χειροκίνητα την πρώτη φορά. Αυτόματα UI tests μπορούν να ελέγξουν ότι τα βελάκια φίλτρου έχουν πράγματι αφαιρεθεί (`worksheet.Tables[0].AutoFilter == null`).
- **Άδεια χρήσης:** Το EPPlus πέρασε σε διπλή άδεια στην έκδοση 5. Για εμπορικά έργα θα χρειαστείς πληρωμένη άδεια ή εναλλακτική βιβλιοθήκη.

## Πλήρες αρχείο πηγαίου κώδικα για αντιγραφή‑επικόλληση

Παρακάτω είναι το ακριβές αρχείο που μπορείς να προσθέσεις σε ένα νέο project console. Δεν υπάρχουν κρυφές εξαρτήσεις, όλα είναι ενσωματωμένα.

```csharp
// File: Program.cs
using System;
using System.IO;
using OfficeOpenXml;
using OfficeOpenXml.Table;

namespace ExcelFilterCleaner
{
    class Program
    {
        static void Main()
        {
            // License context – required for EPPlus 5+
            ExcelPackage.LicenseContext = LicenseContext.NonCommercial;

            // Path to the original workbook (adjust as needed)
            string sourcePath = Path.Combine(Environment.CurrentDirectory, "SalesReport.xlsx");
            if (!File.Exists(sourcePath))
            {
                Console.WriteLine($"Source file not found: {sourcePath}");
                return;
            }

            // Load workbook
            using var package = new ExcelPackage(new FileInfo(sourcePath));

            // Assume the first worksheet contains the table
            var worksheet = package.Workbook.Worksheets[0];
            const string tableName = "SalesTable";

            // Grab the table; abort if missing
            var salesTable = worksheet.Tables[tableName];
            if (salesTable == null)
            {
                Console.WriteLine($"Table '{tableName}' not found.");
                return;
            }

            // ---- Clear filter UI ----
            salesTable.AutoFilter = null;   // removes the filter button row
            salesTable.ShowHeader = true;   // guarantees the header row stays visible

            // Save to a new file so the original stays untouched
            string destPath = Path.Combine(Environment.CurrentDirectory, "SalesReport_NoFilter.xlsx");
            package.SaveAs(new FileInfo(destPath));

            Console.WriteLine($"Successfully cleared filter UI. Output: {destPath}");
        }
    }
}
```

Τρέξε `dotnet add package EPPlus --version 6.0.8` (ή την πιο πρόσφατη) πριν κάνεις build, και θα έχεις ένα καθαρό φύλλο έτοιμο για διανομή.

## Συμπέρασμα

Σου δείξαμε **πώς να αφαιρέσεις το AutoFilter** και **να καθαρίσεις το UI φίλτρου** σε ένα βιβλίο εργασίας Excel χρησιμοποιώντας C#. Ο πυρήνας των τριών γραμμών (`AutoFilter = null;`, `ShowHeader = true;`) κάνει το κύριο έργο, ενώ το υπόλοιπο boilerplate κάνει τη λύση πλήρη.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}