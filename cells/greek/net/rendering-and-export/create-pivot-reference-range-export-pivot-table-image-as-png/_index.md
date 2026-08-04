---
category: general
date: 2026-02-09
description: Δημιουργήστε περιοχή αναφοράς Pivot σε C# και εξάγετε την εικόνα του
  πίνακα Pivot. Μάθετε πώς να αποθηκεύσετε μια περιοχή Excel ως PNG χρησιμοποιώντας
  το Aspose.Cells – γρήγορος, πλήρης οδηγός.
draft: false
keywords:
- create pivot reference range
- export pivot table image
- save excel range as png
- Aspose.Cells C#
- Excel automation C#
language: el
og_description: Δημιουργήστε περιοχή αναφοράς συγκεντρωτικού πίνακα σε C# και εξάγετε
  την εικόνα του συγκεντρωτικού πίνακα σε PNG. Πλήρης οδηγός βήμα‑προς‑βήμα για την
  αποθήκευση μιας περιοχής Excel ως png.
og_title: Δημιουργία περιοχής αναφοράς Pivot – Εξαγωγή εικόνας πίνακα Pivot ως PNG
tags:
- Aspose.Cells
- C#
- Excel
title: Δημιουργία περιοχής αναφοράς συγκεντρωτικού πίνακα – Εξαγωγή εικόνας συγκεντρωτικού
  πίνακα ως PNG
url: /el/net/rendering-and-export/create-pivot-reference-range-export-pivot-table-image-as-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία περιοχής αναφοράς Pivot – Εξαγωγή εικόνας πίνακα Pivot ως PNG

Χρειάζεστε **να δημιουργήσετε περιοχή αναφοράς pivot** σε ένα βιβλίο εργασίας Excel χρησιμοποιώντας C#; Μπορείτε επίσης **να εξάγετε εικόνα πίνακα pivot** και **να αποθηκεύσετε περιοχή Excel ως png** με λίγες μόνο γραμμές κώδικα. Από την εμπειρία μου, η μετατροπή ενός ζωντανού pivot σε στατική εικόνα είναι ένας πρακτικός τρόπος να ενσωματώσετε αναλύσεις σε αναφορές, email ή dashboards χωρίς να μεταφέρετε ολόκληρο το βιβλίο εργασίας.

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από όλα όσα χρειάζεστε: τις απαιτούμενες βιβλιοθήκες, τον ακριβή κώδικα, γιατί κάθε κλήση είναι σημαντική, και μερικά “gotchas” που μπορεί να συναντήσετε. Στο τέλος θα μπορείτε να δημιουργήσετε ένα αρχείο PNG οποιουδήποτε πίνακα pivot με σιγουριά, και θα καταλάβετε πώς να προσαρμόσετε το μοτίβο για πολλαπλά φύλλα ή προσαρμοσμένες μορφές εικόνας.

## Προαπαιτούμενα

Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε:

- **Aspose.Cells for .NET** (η δωρεάν δοκιμή λειτουργεί άψογα για δοκιμές).  
- **.NET 6.0** ή νεότερη – το API που χρησιμοποιούμε είναι πλήρως συμβατό με .NET Standard 2.0+, οπότε παλαιότερα frameworks θα συνθέσουν επίσης.  
- Ένα βασικό έργο C# (Console App, WinForms ή ASP.NET – οτιδήποτε μπορεί να κάνει reference σε πακέτο NuGet).  

Αν δεν έχετε εγκαταστήσει ακόμη το Aspose.Cells, εκτελέστε:

```bash
dotnet add package Aspose.Cells
```

Αυτό είναι όλο – χωρίς COM interop, χωρίς εγκατεστημένο Excel στον server.

## Βήμα 1: Άνοιγμα του βιβλίου εργασίας και πρόσβαση στο πρώτο φύλλο

Το πρώτο που κάνετε είναι να φορτώσετε το αρχείο του βιβλίου εργασίας και να πάρετε το φύλλο που περιέχει τον πίνακα pivot. Επιλέγουμε σκόπιμα το **πρώτο φύλλο** (`Worksheets[0]`) επειδή τα περισσότερα demo αρχεία το τοποθετούν εκεί, αλλά μπορείτε να αντικαταστήσετε το index με ένα όνομα αν προτιμάτε.

```csharp
using Aspose.Cells;
using System;

// Load an existing Excel file (replace with your own path)
Workbook wb = new Workbook("YOUR_DIRECTORY/source.xlsx");

// Access the first worksheet – this is where our pivot lives
Worksheet worksheet = wb.Worksheets[0];
```

*Γιατί είναι σημαντικό:* Το `Worksheet` είναι το σημείο εισόδου για οποιαδήποτε λειτουργία βασισμένη σε περιοχή. Αν δείξετε στο λάθος φύλλο, η επόμενη κλήση `PivotTables[0]` θα ρίξει `IndexOutOfRangeException`.

## Βήμα 2: Δημιουργία περιοχής αναφοράς Pivot

Τώρα ζητάμε από τον ίδιο τον πίνακα pivot να μας δώσει μια **περιοχή αναφοράς**. Αυτή η περιοχή αντιπροσωπεύει τα ακριβή κελιά που σχηματίζουν το pivot – κεφαλίδες, σειρές δεδομένων και σύνολα. Η μέθοδος `CreateReferenceRange()` κάνει το σκληρό κομμάτι εσωτερικά, διαχειριζόμενη συγχωνευμένα κελιά και κρυφές σειρές για εσάς.

```csharp
// Grab the first pivot table on the worksheet
PivotTable pivot = worksheet.PivotTables[0];

// Build a reference range that covers the whole pivot
Range pivotReferenceRange = pivot.CreateReferenceRange();
```

> **Pro tip:** Αν το βιβλίο εργασίας σας περιέχει πολλαπλά pivots, επαναλάβετε την `worksheet.PivotTables` και επιλέξτε αυτό που χρειάζεστε με βάση την ιδιότητα `Name`.

## Βήμα 3: Απόδοση της περιοχής αναφοράς ως εικόνα

Το Aspose.Cells μπορεί να αποδώσει οποιοδήποτε `Range` σε εικόνα. Το αντικείμενο που επιστρέφεται υποστηρίζει τόσο raster (PNG, JPEG) όσο και vector (SVG) μορφές. Εδώ ζητάμε την προεπιλεγμένη raster εικόνα, η οποία είναι συμβατή με `System.Drawing.Image`.

```csharp
// Convert the pivot reference range into an image object
ImageOrVector pivotImage = pivotReferenceRange.ToImage();
```

*Τι συμβαίνει στο παρασκήνιο;* Το API «σφραγίζει» την οπτική διάταξη της περιοχής, σεβόμενος τα στυλ κελιών, τις γραμματοσειρές και το conditional formatting. Είναι ουσιαστικά το ίδιο με το να πάρετε ένα screenshot, αλλά προγραμματιστικά και χωρίς UI.

## Βήμα 4: Αποθήκευση της παραγόμενης εικόνας σε αρχείο

Τέλος, αποθηκεύουμε την εικόνα. Η μέθοδος `Save` επιλέγει αυτόματα PNG όταν της δίνετε επέκταση “.png”. Μπορείτε επίσης να περάσετε ένα αντικείμενο `SaveOptions` αν χρειάζεστε έλεγχο DPI ή διαφορετική μορφή.

```csharp
// Save the image as PNG – the extension drives the format
pivotImage.Save("YOUR_DIRECTORY/pivot.png");
```

Μετά την εκτέλεση αυτής της γραμμής, ανοίξτε το `pivot.png` και θα δείτε μια τέλεια λήψη του πίνακα pivot, έτοιμη να ενσωματωθεί οπουδήποτε.

## Πλήρες λειτουργικό παράδειγμα

Συνδυάζοντας όλα τα παραπάνω, εδώ είναι ένα αυτόνομο πρόγραμμα console που μπορείτε να αντιγράψετε‑επικολλήσετε και να τρέξετε:

```csharp
using Aspose.Cells;
using System;

namespace PivotExportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load workbook
            Workbook wb = new Workbook("YOUR_DIRECTORY/source.xlsx");

            // 2️⃣ Access first worksheet
            Worksheet worksheet = wb.Worksheets[0];

            // 3️⃣ Get first pivot table
            if (worksheet.PivotTables.Count == 0)
            {
                Console.WriteLine("No pivot tables found on the first sheet.");
                return;
            }
            PivotTable pivot = worksheet.PivotTables[0];

            // 4️⃣ Create a reference range that covers the whole pivot
            Range pivotReferenceRange = pivot.CreateReferenceRange();

            // 5️⃣ Render the range to an image
            ImageOrVector pivotImage = pivotReferenceRange.ToImage();

            // 6️⃣ Save as PNG
            string outputPath = "YOUR_DIRECTORY/pivot.png";
            pivotImage.Save(outputPath);

            Console.WriteLine($"Pivot table image saved to {outputPath}");
        }
    }
}
```

**Αναμενόμενο αποτέλεσμα:** ένα αρχείο με όνομα `pivot.png` στο `YOUR_DIRECTORY`. Ανοίξτε το με οποιονδήποτε προβολέα εικόνων – θα πρέπει να δείτε την ακριβή διάταξη του αρχικού pivot, συμπεριλαμβανομένων των επικεφαλίδων στηλών, των σειρών δεδομένων και των συνολικών.

## Εξαγωγή εικόνας πίνακα Pivot – Προσαρμογή μεγέθους και DPI

Μερικές φορές η προεπιλεγμένη εικόνα είναι πολύ μικρή για μια διαφάνεια παρουσίασης. Μπορείτε να ελέγξετε την ανάλυση περνώντας ένα αντικείμενο `ImageOrVectorSaveOptions`:

```csharp
using Aspose.Cells.Drawing;

// Define PNG options – 300 DPI for high‑quality print
ImageOrVectorSaveOptions options = new ImageOrVectorSaveOptions
{
    ImageFormat = ImageFormat.Png,
    Resolution = 300 // DPI
};

pivotImage.Save("YOUR_DIRECTORY/pivot_highres.png", options);
```

*Γιατί να ρυθμίσετε DPI;* Υψηλότερο DPI προσφέρει πιο οξείς άκρες, ειδικά όταν το PNG κλιμακώνεται σε PowerPoint ή PDF.

## Αποθήκευση περιοχής Excel ως PNG – Διαχείριση πολλαπλών φύλλων

Αν χρειαστεί να εξάγετε pivots από αρκετά φύλλα, κάντε βρόχο μέσω `Workbook.Worksheets` και επαναλάβετε τα βήματα. Εδώ είναι ένα σύντομο snippet:

```csharp
foreach (Worksheet ws in wb.Worksheets)
{
    foreach (PivotTable pt in ws.PivotTables)
    {
        Range refRange = pt.CreateReferenceRange();
        ImageOrVector img = refRange.ToImage();
        string fileName = $"pivot_{ws.Name}_{pt.Name}.png";
        img.Save($"YOUR_DIRECTORY/{fileName}");
        Console.WriteLine($"Saved {fileName}");
    }
}
```

Αυτό το μοτίβο **export pivot table image** για κάθε pivot σε όλο το βιβλίο εργασίας, και κάθε αρχείο ονομάζεται με βάση το φύλλο και το pivot – ιδανικό για μαζική επεξεργασία.

## Συνηθισμένα προβλήματα & Πώς να τα αποφύγετε

| Πρόβλημα | Γιατί συμβαίνει | Διόρθωση |
|----------|----------------|----------|
| `IndexOutOfRangeException` στο `PivotTables[0]` | Το φύλλο δεν έχει πίνακες pivot. | Ελέγξτε `worksheet.PivotTables.Count` πριν την πρόσβαση. |
| Κενή εικόνα | Το pivot είναι φιλτραρισμένο ώστε να κρύβει όλες τις σειρές. | Βεβαιωθείτε ότι το pivot έχει ορατά δεδομένα, ή καλέστε `pivot.RefreshData();` πριν δημιουργήσετε την περιοχή. |
| PNG χαμηλής ανάλυσης | Το προεπιλεγμένο DPI είναι 96. | Χρησιμοποιήστε `ImageOrVectorSaveOptions.Resolution` όπως φαίνεται παραπάνω. |
| Σφάλματα διαδρομής αρχείου | Μη έγκυροι χαρακτήρες στο `YOUR_DIRECTORY`. | Χρησιμοποιήστε `Path.Combine` και `Path.GetInvalidPathChars()` για καθαρισμό. |

## Επαλήθευση – Γρήγορο τεστ

Μετά την εκτέλεση του πλήρους παραδείγματος:

1. Ανοίξτε το `pivot.png` στο Windows Photo Viewer.  
2. Επαληθεύστε ότι οι επικεφαλίδες στηλών, οι σειρές δεδομένων και οι συνολικές σειρές ταιριάζουν με την προβολή στο Excel.  
3. Αν παρατηρήσετε ελλιπείς σειρές, ελέγξτε ξανά ότι η μέθοδος **RefreshData** του pivot κλήθηκε πριν το `CreateReferenceRange()`.

## Bonus: Ενσωμάτωση του PNG σε έγγραφο Word

Επειδή η εικόνα είναι ήδη PNG, μπορείτε να τη δώσετε κατευθείαν στο Aspose.Words:

```csharp
using Aspose.Words;
Document doc = new Document();
DocumentBuilder builder = new DocumentBuilder(doc);
builder.InsertImage("YOUR_DIRECTORY/pivot.png");
doc.Save("YOUR_DIRECTORY/report.docx");
```

Τώρα έχετε μια αναφορά Word που περιέχει την ακριβή λήψη του pivot – χωρίς χειροκίνητη αντιγραφή‑επικόλληση.

## Συμπέρασμα

Μόλις μάθατε πώς να **create pivot reference range**, **export pivot table image**, και **save Excel range as png** χρησιμοποιώντας το Aspose.Cells σε C#. Τα βασικά σημεία είναι:

- Χρησιμοποιήστε `PivotTable.CreateReferenceRange()` για να απομονώσετε την οπτική περιοχή ενός pivot.  
- Μετατρέψτε αυτήν την περιοχή σε εικόνα με `Range.ToImage()`.  
- Αποθηκεύστε την εικόνα ως PNG, προσαρμόζοντας προαιρετικά το DPI για εκτύπωση.  

Από εδώ μπορείτε να εξερευνήσετε μαζική εξαγωγή, διαφορετικές μορφές εικόνας (SVG, JPEG), ή ακόμη και ενσωμάτωση του PNG σε PDF ή Word. Ο ουρανός είναι το όριο μόλις έχετε το pivot ως στατικό γραφικό.

Έχετε ερωτήσεις ή κάποιο δύσκολο σενάριο; Αφήστε ένα σχόλιο παρακάτω, και καλή προγραμματιστική δουλειά!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}