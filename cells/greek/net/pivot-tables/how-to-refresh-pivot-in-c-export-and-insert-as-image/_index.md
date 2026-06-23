---
category: general
date: 2026-05-04
description: Πώς να ανανεώσετε το pivot σε C# και να το εξάγετε ως PNG, στη συνέχεια
  να εισάγετε την εικόνα στο φύλλο εργασίας. Ακολουθήστε αυτόν τον οδηγό βήμα‑βήμα
  με πλήρη κώδικα.
draft: false
keywords:
- how to refresh pivot
- how to export pivot
- insert image into worksheet
- refresh pivot table code
- load excel workbook c#
language: el
og_description: Πώς να ανανεώσετε το pivot σε C#; Μάθετε πώς να εξάγετε τον πίνακα
  pivot ως εικόνα και να τον εισάγετε σε ένα φύλλο εργασίας με πλήρη παραδείγματα
  κώδικα.
og_title: Πώς να ανανεώσετε το Pivot σε C# – Εξαγωγή και εισαγωγή ως εικόνα
tags:
- C#
- Aspose.Cells
- Excel Automation
title: Πώς να ανανεώσετε το Pivot σε C# – Εξαγωγή και εισαγωγή ως εικόνα
url: /el/net/pivot-tables/how-to-refresh-pivot-in-c-export-and-insert-as-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Ανανεώσετε ένα Pivot σε C# – Εξαγωγή και Εισαγωγή ως Εικόνα

Το πώς να ανανεώσετε ένα pivot σε C# είναι ένα συχνό εμπόδιο όταν αυτοματοποιείτε αναφορές Excel. Σε αυτόν τον οδηγό θα δείτε ακριβώς **πώς να ανανεώσετε ένα pivot**, να το εξάγετε ως PNG και να το τοποθετήσετε σε έναν placeholder φύλλου εργασίας — όλα με ένα μόνο εκτελέσιμο πρόγραμμα.

Αν επίσης αναρωτιέστε *πώς να εξάγετε ένα pivot* ή χρειάζεστε **εισαγωγή εικόνας σε φύλλο εργασίας**, βρίσκεστε στο σωστό σημείο. Θα περάσουμε από κάθε γραμμή, θα εξηγήσουμε γιατί είναι σημαντική και θα καλύψουμε μερικές περιπτώσεις άκρων που μπορεί να συναντήσετε σε πραγματικά έργα.

---

## Τι Θα Χρειαστείτε

Πριν προχωρήσουμε, βεβαιωθείτε ότι έχετε:

- **Aspose.Cells for .NET** (η βιβλιοθήκη που παρέχει `Workbook`, `Worksheet`, `ImageOrPrintOptions`, κ.λπ.). Μπορείτε να την αποκτήσετε από το NuGet: `Install-Package Aspose.Cells`.
- .NET 6 ή νεότερη έκδοση (ο κώδικας παρακάτω στοχεύει στο .NET 6, αλλά οποιαδήποτε πρόσφατη έκδοση λειτουργεί).
- Βασική κατανόηση του C# και της διαχείρισης αρχείων — τίποτα περίπλοκο.

Αυτό είναι όλο. Χωρίς επιπλέον DLLs, χωρίς COM interop, μόνο μια καθαρή εφαρμογή console σε C#.

---

## Βήμα 1 – Φόρτωση Βιβλίου Εργασίας Excel σε Στυλ C#

Πρώτα, πρέπει να ανοίξουμε το αρχείο προέλευσης. Εδώ βρίσκεται το τμήμα **load excel workbook c#**.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Load the workbook from disk
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(inputPath);

        // Grab the first worksheet (index 0)
        Worksheet worksheet = workbook.Worksheets[0];
```

> **Γιατί;**  
> Η φόρτωση του βιβλίου εργασίας μας δίνει πρόσβαση στα φύλλα, στους πίνακες pivot και στα placeholders εικόνων. Αν το αρχείο δεν βρεθεί, το Aspose ρίχνει ένα σαφές `FileNotFoundException`, το οποίο μπορείτε να πιάσετε για πιο φιλικό UI.

---

## Βήμα 2 – Προετοιμασία Επιλογών Εικόνας για Εξαγωγή Pivot

Τώρα λέμε στο Aspose πώς θέλουμε να φαίνεται η εξαγόμενη εικόνα. Αυτό είναι το κεντρικό τμήμα του **how to export pivot**.

```csharp
        // Step 2: Set up image export options – PNG is lossless and widely supported
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
        {
            SaveFormat = SaveFormat.Png,
            // Optional: tweak resolution for sharper images
            HorizontalResolution = 300,
            VerticalResolution = 300
        };
```

> **Συμβουλή επαγγελματία:**  
> Αν χρειάζεστε JPEG για μικρότερο μέγεθος αρχείου, αλλάξτε το `SaveFormat.Png` σε `SaveFormat.Jpeg` και προσαρμόστε το `Quality` ανάλογα.

---

## Βήμα 3 – Κώδικας Ανανέωσης Πίνακα Pivot

Ένας παλιός πίνακας pivot εμφανίζει παλιά δεδομένα. Η ανανέωσή του εγγυάται ότι η εικόνα αντικατοπτρίζει τους πιο πρόσφατους αριθμούς.

```csharp
        // Step 3: Refresh the first pivot table in the worksheet
        if (worksheet.PivotTables.Count > 0)
        {
            worksheet.PivotTables[0].Refresh();
        }
        else
        {
            Console.WriteLine("No pivot tables found on the first worksheet.");
            return;
        }
```

> **Γιατί να το ανανεώσετε;**  
> Οι πίνακες pivot αποθηκεύουν στην cache τα δεδομένα πηγής όταν δημιουργούνται. Αν το υποκείμενο φύλλο εργασίας αλλάξει (π.χ. προστεθούν νέες γραμμές), η cache γίνεται παρωχημένη. Η κλήση `Refresh()` αναγκάζει το Aspose να ξαναζητήσει την περιοχή πηγής, εξασφαλίζοντας ότι η εξαγόμενη εικόνα δεν θα παραμείνει κολλημένη σε παλαιά σύνολα.

---

## Βήμα 4 – Μετατροπή του Ανανεωμένου Pivot σε Εικόνα

Αυτή είναι η μαγική γραμμή που πραγματικά **export pivot** σε έναν πίνακα byte.

```csharp
        // Step 4: Export the refreshed pivot table as an image
        byte[] pivotImage = worksheet.PivotTables[0].ToImage(imageOptions);
```

> **Τι λαμβάνετε:**  
> Το `pivotImage` περιέχει τώρα μια PNG‑κωδικοποιημένη εικόνα του πίνακα pivot, έτοιμη να γραφτεί στο δίσκο ή να ενσωματωθεί αλλού.

---

## Βήμα 5 – Εισαγωγή Εικόνας σε Φύλλο Εργασίας

Εδώ είναι που **insert image into worksheet**. Θα τοποθετήσουμε την εικόνα στον πρώτο placeholder εικόνας (αν υπάρχει).

```csharp
        // Step 5: Insert the image into the first picture placeholder
        if (worksheet.Pictures.Count > 0)
        {
            worksheet.Pictures[0].ImageBytes = pivotImage;
        }
        else
        {
            // If no placeholder exists, add a new picture at cell A1
            int pictureIndex = worksheet.Pictures.Add(0, 0, pivotImage).Index;
            Console.WriteLine($"Added new picture at index {pictureIndex}.");
        }
```

> **Γιατί να χρησιμοποιήσετε placeholder;**  
> Πολλά πρότυπα Excel περιλαμβάνουν ένα προμορφοποιημένο σχήμα εικόνας (μέγεθος, περίγραμμα, θέση). Στοχεύοντας το `Pictures[0]`, διατηρούμε τη διάταξη αμετάβλητη. Αν το πρότυπο δεν έχει placeholder, η εναλλακτική δημιουργεί μια νέα εικόνα αγκυροβολημένη στο κελί A1.

---

## Βήμα 6 – Αποθήκευση του Βιβλίου Εργασίας (Προαιρετικό)

Τέλος, αποθηκεύουμε τις αλλαγές. Μπορείτε να αντικαταστήσετε το αρχικό αρχείο ή να γράψετε σε νέο αρχείο.

```csharp
        // Step 6: Save the updated workbook
        string outputPath = @"YOUR_DIRECTORY\output.xlsx";
        workbook.Save(outputPath);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

> **Αναμενόμενο αποτέλεσμα:**  
> Ανοίξτε το `output.xlsx` και θα δείτε τον πίνακα pivot ανανεωμένο, εξαγόμενο ως καθαρή PNG, και εμφανιζόμενο μέσα στην πρώτη θέση εικόνας. Το υπόλοιπο του βιβλίου παραμένει αμετάβλητο.

---

## Πλήρες Παράδειγμα Εργασίας (Έτοιμο για Αντιγραφή‑Επικόλληση)

Παρακάτω βρίσκεται το πλήρες τμήμα κώδικα που μπορείτε να ενσωματώσετε σε ένα νέο έργο console. Δεν λείπει τίποτα.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load the workbook
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(inputPath);
        Worksheet worksheet = workbook.Worksheets[0];

        // Configure image export options (PNG, 300 DPI)
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
        {
            SaveFormat = SaveFormat.Png,
            HorizontalResolution = 300,
            VerticalResolution = 300
        };

        // Refresh the first pivot table
        if (worksheet.PivotTables.Count == 0)
        {
            Console.WriteLine("No pivot tables found.");
            return;
        }
        worksheet.PivotTables[0].Refresh();

        // Export pivot to PNG byte array
        byte[] pivotImage = worksheet.PivotTables[0].ToImage(imageOptions);

        // Insert the image into a picture placeholder or add a new picture
        if (worksheet.Pictures.Count > 0)
        {
            worksheet.Pictures[0].ImageBytes = pivotImage;
        }
        else
        {
            worksheet.Pictures.Add(0, 0, pivotImage);
        }

        // Save the workbook
        string outputPath = @"YOUR_DIRECTORY\output.xlsx";
        workbook.Save(outputPath);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

Τρέξτε το πρόγραμμα, ανοίξτε το παραγόμενο αρχείο και επαληθεύστε ότι ο πίνακας pivot αντανακλά τα πιο πρόσφατα δεδομένα και εμφανίζεται ως εικόνα υψηλής ανάλυσης.

---

## Συχνές Ερωτήσεις & Περιπτώσεις Άκρων

| Ερώτηση | Απάντηση |
|----------|--------|
| **Τι γίνεται αν το βιβλίο εργασίας έχει πολλαπλά φύλλα;** | Προσαρμόστε το `workbook.Worksheets[0]` στον κατάλληλο δείκτη ή όνομα (`workbook.Worksheets["Sheet2"]`). |
| **Μπορώ να εξάγω πολλαπλούς πίνακες pivot;** | Κάντε βρόχο μέσω `worksheet.PivotTables` και επαναλάβετε τα βήματα 3‑4 για καθέναν. Αποθηκεύστε κάθε εικόνα σε ξεχωριστό placeholder ή συνδυάστε τις σε ένα φύλλο. |
| **Τι γίνεται με μεγάλους πίνακες pivot που προκαλούν πίεση μνήμης;** | Χρησιμοποιήστε `ImageOrPrintOptions` με χαμηλότερο DPI ή εξάγετε σε JPEG για να μειώσετε το μέγεθος του πίνακα byte. |
| **Πρέπει να διαγράψω κάτι;** | Τα αντικείμενα Aspose διαχειρίζονται αυτόματα· η δήλωση `using` δεν είναι απαραίτητη, αλλά μπορείτε να τυλίξετε το `Workbook` σε `using` αν προτιμάτε καθαρό καθορισμό πόρων. |
| **Είναι συμβατό με .NET Core;** | Ναι. Το Aspose.Cells υποστηρίζει .NET Core, .NET 5/6 και .NET Framework. Απλώς αναφερθείτε στο κατάλληλο πακέτο NuGet. |

---

## Συμβουλές & Καλές Πρακτικές

- **Επικυρώστε διαδρομές**: Χρησιμοποιήστε `Path.Combine` και `Environment.GetFolderPath` για να αποφύγετε σκληρά κωδικοποιημένους διαχωριστές.
- **Διαχείριση σφαλμάτων**: Τυλίξτε όλο το σώμα του `Main` σε `try/catch` και καταγράψτε το `Exception.Message` για σενάρια παραγωγής.
- **Σχεδίαση προτύπου**: Τοποθετήστε ένα διαφανές σχήμα εικόνας όπου θέλετε την εικόνα του pivot· αυτό διατηρεί τα πλάτη των στηλών και τα ύψη των γραμμών.
- **Απόδοση**: Αν χρειάζεστε μόνο την εικόνα, μπορείτε να παραλείψετε εντελώς την αποθήκευση του βιβλίου εργασίας και να γράψετε το `pivotImage` σε ξεχωριστό αρχείο PNG.

---

## Συμπέρασμα

Τώρα ξέρετε **πώς να ανανεώσετε ένα pivot** σε C#, να εξάγετε αυτήν τη φρεσκάδα ως εικόνα και να **εισάγετε εικόνα σε φύλλο εργασίας** χωρίς προβλήματα. Η πλήρης λύση — φόρτωση του βιβλίου, ρύθμιση επιλογών εξαγωγής, ανανέωση του pivot, μετατροπή σε PNG και αποθήκευση του αρχείου — καλύπτει όλη τη ροή εργασίας που ζητήσατε.

Έτοιμοι για την επόμενη πρόκληση; Δοκιμάστε να συνδυάσετε το **how to export pivot** με επεξεργασία πολλαπλών αρχείων σε batch, ή εξερευνήστε το **refresh pivot table code** για δυναμικές πηγές δεδομένων όπως βάσεις ή CSV. Το ίδιο μοτίβο ισχύει: φόρτωση, ανανέωση, εξαγωγή, εισαγωγή, αποθήκευση.

Καλή προγραμματιστική δουλειά, και οι αυτοματοποιήσεις Excel σας να παραμένουν φρέσκιες και τέλειες σε εικόνα!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}