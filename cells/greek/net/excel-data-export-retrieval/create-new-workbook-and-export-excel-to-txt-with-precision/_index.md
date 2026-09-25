---
category: general
date: 2026-02-15
description: Δημιουργήστε νέο βιβλίο εργασίας και εξάγετε το Excel σε TXT ενώ ορίζετε
  την αριθμητική ακρίβεια. Μάθετε πώς να ορίζετε σημαντικά ψηφία και να περιορίζετε
  τα σημαντικά ψηφία σε C#.
draft: false
keywords:
- create new workbook
- export excel to txt
- set significant digits
- limit significant digits
- set numeric precision
language: el
og_description: Δημιουργήστε νέο βιβλίο εργασίας και εξάγετε το Excel σε TXT, ορίζοντας
  σημαντικά ψηφία για την αριθμητική ακρίβεια. Ένας βήμα‑βήμα οδηγός C#.
og_title: Δημιουργία Νέου Φύλλου Εργασίας – Εξαγωγή Excel σε TXT με Ακρίβεια
tags:
- C#
- Aspose.Cells
- Excel automation
title: Δημιουργία νέου βιβλίου εργασίας και εξαγωγή Excel σε TXT με ακρίβεια
url: /el/net/excel-data-export-retrieval/create-new-workbook-and-export-excel-to-txt-with-precision/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία Νέου Workbook – Εξαγωγή Excel σε TXT με Ακριβή Μορφοποίηση Αριθμών

Έχετε αναρωτηθεί ποτέ πώς να **create new workbook** αντικείμενα σε C# και να τα αποθηκεύετε αμέσως σε ένα αρχείο απλού κειμένου; Δεν είστε οι μόνοι. Σε πολλές περιπτώσεις pipelines δεδομένων χρειάζεται να **export Excel to TXT** διατηρώντας τους αριθμούς αναγνώσιμους, πράγμα που σημαίνει περιορισμό του αριθμού των ψηφίων που εμφανίζονται μετά το δεκαδικό σημείο.  

Σε αυτό το tutorial θα περάσουμε από όλη τη διαδικασία: από τη δημιουργία ενός φρέσκου workbook, στη ρύθμιση της εξαγωγής ώστε να **sets significant digits** (δηλαδή περιορισμός σημαντικών ψηφίων), και τέλος τη γραφή του αρχείου στο δίσκο. Στο τέλος θα έχετε ένα έτοιμο κομμάτι κώδικα που σέβεται τις απαιτήσεις **numeric precision**—χωρίς πρόσθετες βιβλιοθήκες, χωρίς μαγεία.

> **Pro tip:** Αν χρησιμοποιείτε ήδη το Aspose.Cells, οι κλάσεις που φαίνονται παρακάτω είναι μέρος αυτής της βιβλιοθήκης. Αν βρίσκεστε σε διαφορετική πλατφόρμα, οι έννοιες παραμένουν ίδιες· απλώς αντικαταστήστε τις κλήσεις API.

---

## What You’ll Need

- .NET 6+ (ο κώδικας μεταγλωττίζεται σε .NET Core και .NET Framework)  
- Aspose.Cells for .NET (δωρεάν δοκιμή ή αδειοδοτημένη έκδοση) – εγκατάσταση μέσω NuGet: `dotnet add package Aspose.Cells`  
- Οποιοδήποτε IDE προτιμάτε (Visual Studio, Rider, VS Code)  

Αυτό είναι όλο. Χωρίς επιπλέον αρχεία ρυθμίσεων, χωρίς κρυφά βήματα.

---

## Step 1: Create a New Workbook

Το πρώτο βήμα είναι να **create new workbook**. Σκεφτείτε την κλάση `Workbook` ως ένα κενό αρχείο Excel που περιμένει φύλλα, κελιά και δεδομένα.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Instantiate a fresh workbook – this is the core of create new workbook logic
        Workbook workbook = new Workbook();

        // (Optional) Add some sample data so you can see the effect of numeric precision later
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].PutValue(12345.678901);
        sheet.Cells["A2"].PutValue(0.000123456);
        sheet.Cells["A3"].PutValue(Math.PI);
```

> **Why this matters:** Ξεκινώντας με ένα καθαρό workbook αποφεύγετε τυχόν κρυφές μορφοποιήσεις που θα μπορούσαν να επηρεάσουν τις ρυθμίσεις ακρίβειας αργότερα.

---

## Step 2: Configure Text Save Options – Set Significant Digits

Τώρα λέμε στο Aspose.Cells πόσα **significant digits** θέλουμε όταν γράφουμε σε αρχείο `.txt`. Η κλάση `TxtSaveOptions` εκθέτει την ιδιότητα `SignificantDigits` που κάνει ακριβώς αυτό.

```csharp
        // Step 2: Prepare save options – limit numeric precision to 5 significant digits
        TxtSaveOptions txtOptions = new TxtSaveOptions
        {
            // This limits the output to 5 digits that matter, rounding the rest
            SignificantDigits = 5
        };
```

> **Explanation:** `SignificantDigits = 5` σημαίνει ότι ο εξαγωγέας θα διατηρήσει τα πέντε πιο σημαντικά ψηφία οποιουδήποτε αριθμού, ανεξάρτητα από τη θέση του δεκαδικού σημείου. Είναι ένας βολικός τρόπος να **set numeric precision** χωρίς να μορφοποιείτε χειροκίνητα κάθε κελί.

---

## Step 3: Save the Workbook as a Plain‑Text File

Με το workbook και τις επιλογές έτοιμες, τελικά **export Excel to txt**. Η μέθοδος `Save` δέχεται τη διαδρομή του αρχείου και το αντικείμενο επιλογών που μόλις διαμορφώσαμε.

```csharp
        // Step 3: Write the workbook out as a TXT file using our precision settings
        string outputPath = @"C:\Temp\numbers.txt";
        workbook.Save(outputPath, txtOptions);

        System.Console.WriteLine($"Workbook exported to {outputPath} with 5 significant digits.");
    }
}
```

Η εκτέλεση του προγράμματος παράγει ένα αρχείο που φαίνεται ως εξής:

```
12346
0.00012346
3.1416
```

Παρατηρήστε πώς κάθε αριθμός σέβεται τον κανόνα **limit significant digits** που ορίσαμε νωρίτερα.

---

## Step 4: Verify the Result (Optional but Recommended)

Είναι εύκολο να ανοίξετε το παραγόμενο `numbers.txt` σε οποιονδήποτε επεξεργαστή, αλλά ίσως θέλετε να αυτοματοποιήσετε το βήμα επαλήθευσης, ειδικά σε pipelines CI.

```csharp
        // Quick verification – read back the file and print each line
        foreach (var line in System.IO.File.ReadAllLines(outputPath))
        {
            System.Console.WriteLine($"Line: {line}");
        }
```

Αν η κονσόλα εμφανίσει τις τρεις γραμμές παραπάνω, έχετε επιτυχώς **set significant digits** και η εξαγωγή λειτουργεί όπως προβλέπεται.

---

## Common Pitfalls & How to Avoid Them

| Πρόβλημα | Γιατί συμβαίνει | Διόρθωση |
|----------|----------------|----------|
| Οι αριθμοί εμφανίζονται με πάρα πολλά δεκαδικά ψηφία | Η `SignificantDigits` έμεινε στην προεπιλογή (0) | Ορίστε ρητά την `SignificantDigits` στον επιθυμητό αριθμό |
| Δημιουργείται κενό αρχείο | Το workbook δεν έλαβε δεδομένα πριν από την αποθήκευση | Συμπληρώστε κελιά **πριν** καλέσετε το `Save` |
| Η διαδρομή αρχείου προκαλεί `UnauthorizedAccessException` | Προσπάθεια εγγραφής σε προστατευμένο φάκελο | Χρησιμοποιήστε φάκελο με δικαιώματα εγγραφής (π.χ., `C:\Temp` ή `%USERPROFILE%\Documents`) |
| Η ακρίβεια φαίνεται λανθασμένη για πολύ μικρούς αριθμούς | Η μέτρηση σημαντικών ψηφίων περιλαμβάνει μηδενικά μετά το δεκαδικό | Θυμηθείτε ότι το “significant” αγνοεί τα αρχικά μηδενικά· 0.000123456 με 5 ψηφία γίνεται `0.00012346` |

---

## Full Working Example (Copy‑Paste Ready)

Παρακάτω βρίσκεται το πλήρες, αυτόνομο πρόγραμμα. Επικολλήστε το σε ένα νέο console project και πατήστε **Run**.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook
        Workbook workbook = new Workbook();

        // Populate with sample numbers
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].PutValue(12345.678901);
        sheet.Cells["A2"].PutValue(0.000123456);
        sheet.Cells["A3"].PutValue(Math.PI);

        // 2️⃣ Set up export options – limit significant digits to 5
        TxtSaveOptions txtOptions = new TxtSaveOptions
        {
            SignificantDigits = 5
        };

        // 3️⃣ Export to TXT
        string outputPath = @"C:\Temp\numbers.txt";
        workbook.Save(outputPath, txtOptions);

        Console.WriteLine($"✅ Export completed: {outputPath}");
        Console.WriteLine("🔎 Verifying content:");
        foreach (var line in System.IO.File.ReadAllLines(outputPath))
        {
            Console.WriteLine($"   {line}");
        }
    }
}
```

**Αναμενόμενη έξοδος κονσόλας**

```
✅ Export completed: C:\Temp\numbers.txt
🔎 Verifying content:
   12346
   0.00012346
   3.1416
```

Και το αρχείο `numbers.txt` θα περιέχει τις τρεις γραμμές που φαίνονται παραπάνω.

---

## Next Steps: Going Beyond the Basics

- **Export other formats** – Το Aspose.Cells υποστηρίζει επίσης CSV, HTML και PDF. Αντικαταστήστε το `TxtSaveOptions` με `CsvSaveOptions` ή `PdfSaveOptions` ανάλογα με τις ανάγκες.  
- **Dynamic precision** – Μπορείτε να υπολογίσετε το `SignificantDigits` σε χρόνο εκτέλεσης βάσει εισόδου χρήστη ή αρχείων ρυθμίσεων.  
- **Multiple worksheets** – Επανάληψη πάνω στο `workbook.Worksheets` και εξαγωγή του καθενός σε δικό του αρχείο `.txt`.  
- **Localization** – Έλεγχος του διαχωριστή δεκαδικών (`.` vs `,`) μέσω `CultureInfo` αν χρειάζεται να ταιριάζει με τις περιφερειακές ρυθμίσεις.  

Όλες αυτές οι επεκτάσεις βασίζονται στην κεντρική ιδέα που καλύψαμε: **create new workbook**, διαμόρφωση της εξαγωγής, και **set numeric precision** ώστε να ταιριάζει στις απαιτήσεις αναφοράς σας.

---

## Summary

Πήραμε ένα φρέσκο αντικείμενο **create new workbook**, το γεμίσαμε με δεδομένα, και δείξαμε πώς να **export Excel to TXT** ενώ **setting significant digits** περιορίζει την ακρίβεια εξόδου. Το πλήρες παράδειγμα εκτελείται αμέσως, και η εξήγηση κάλυψε το *γιατί* πίσω από κάθε γραμμή ώστε να μπορείτε να το προσαρμόσετε στα δικά σας έργα.

Δοκιμάστε ελεύθερα—αλλάξτε την τιμή `SignificantDigits`, προσθέστε περισσότερα φύλλα, ή αλλάξτε τη μορφή εξόδου. Αν αντιμετωπίσετε πρόβλημα, ελέγξτε την τεκμηρίωση του Aspose.Cells ή αφήστε ένα σχόλιο παρακάτω. Καλό coding!

---

![Create new workbook example](/images/create-new-workbook.png "Screenshot showing a C# IDE with the create new workbook code")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}