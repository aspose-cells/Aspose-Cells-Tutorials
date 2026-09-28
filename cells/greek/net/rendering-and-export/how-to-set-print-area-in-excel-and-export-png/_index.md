---
category: general
date: 2026-09-27
description: Ορίστε την περιοχή εκτύπωσης στο Excel και μάθετε πώς να εξάγετε εικόνες
  PNG από επιλεγμένα κελιά. Αυτός ο οδηγός καλύπτει επίσης την αποθήκευση περιοχής
  ως εικόνα και την προσθήκη εικόνας στο φύλλο εργασίας.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set print area excel
- how to export png
- save range as image
- add picture to worksheet
- export selected cells image
language: el
lastmod: 2026-09-27
og_description: Ορίστε την περιοχή εκτύπωσης στο Excel και εξάγετε PNG με το Aspose.Cells.
  Ακολουθήστε αυτόν τον οδηγό βήμα‑προς‑βήμα για να αποθηκεύσετε την περιοχή ως εικόνα
  και να προσθέσετε εικόνα στο φύλλο εργασίας.
og_image_alt: Screenshot showing set print area excel and exported PNG file
og_title: Ορισμός περιοχής εκτύπωσης στο Excel – εξαγωγή PNG σε C#
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Set print area in Excel and learn how to export PNG images of selected
    cells. This guide also covers saving range as image and adding picture to worksheet.
  headline: How to set print area in Excel and export PNG
  type: TechArticle
tags:
- Excel automation
- C#
- Aspose.Cells
title: Πώς να ορίσετε την περιοχή εκτύπωσης στο Excel και να εξάγετε PNG
url: /el/net/rendering-and-export/how-to-set-print-area-in-excel-and-export-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να ορίσετε περιοχή εκτύπωσης στο Excel και να εξάγετε PNG

Αν χρειάζεστε να **set print area excel** πριν δημιουργήσετε μια εικόνα, αυτός ο οδηγός σας δείχνει ακριβώς πώς να το κάνετε. Θα μάθετε επίσης **how to export png** αρχεία από συγκεκριμένο εύρος, **save range as image**, και **add picture to worksheet** σε μια ενιαία, επαναλαμβανόμενη ροή εργασίας.

Η προγραμματιστική εργασία με το Excel συχνά σημαίνει ότι θέλετε μόνο ένα υποσύνολο κελιών—π.χ. έναν πίνακα pivot ή ένα γράφημα—to become an image. Ορίζοντας πρώτα μια περιοχή εκτύπωσης, εξασφαλίζετε ότι το εξαγόμενο PNG περιέχει ακριβώς τα κελιά που περιμένετε, ούτε περισσότερα ούτε λιγότερα. Αυτό το tutorial σας καθοδηγεί βήμα προς βήμα, από τη φόρτωση του βιβλίου εργασίας μέχρι την αποθήκευση του τελικού αρχείου PNG, και εξηγεί γιατί κάθε ρύθμιση είναι σημαντική.

## Προαπαιτούμενα

* .NET 6.0 ή νεότερη έκδοση εγκατεστημένη  
* Visual Studio 2022 (ή οποιοδήποτε IDE C#)  
* Το πακέτο NuGet **Aspose.Cells for .NET** (`Install-Package Aspose.Cells`)  
* Ένα αρχείο Excel (`input.xlsx`) τοποθετημένο σε γνωστό φάκελο  

Αυτές οι απαιτήσεις διασφαλίζουν ότι ο κώδικας εκτελείται χωρίς πρόσθετη διαμόρφωση.

## Βήμα 1: Φορτώστε το βιβλίο εργασίας με το οποίο θέλετε να εργαστείτε

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

// Load the workbook from disk
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");
```

Η κλάση `Workbook` αντιπροσωπεύει ολόκληρο το αρχείο Excel. Φορτώνοντάς το πρώτα, αποκτάτε πρόσβαση σε φύλλα εργασίας, κελιά και επιλογές ρύθμισης σελίδας.

## Βήμα 2: **Set print area excel** για το επιθυμητό εύρος

```csharp
// Define the range you want to capture
string printArea = "A1:G20";

// Apply the range as the print area on the first worksheet
workbook.Worksheets[0].PageSetup.PrintArea = printArea;
```

Ο ορισμός της **print area** λέει στο Excel (και στο Aspose.Cells) ποια κελιά ανήκουν στη σελίδα εκτύπωσης. Όταν αργότερα εξάγετε το φύλλο ως εικόνα, μόνο αυτή η περιοχή αποδίδεται, κάτι που είναι απαραίτητο για μια καθαρή **export selected cells image**.

## Βήμα 3: Διαμορφώστε τις επιλογές εξαγωγής εικόνας – **how to export png**

```csharp
ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Png,   // PNG ensures lossless quality
    OnePagePerSheet = true           // Export the defined print area as a single page
};
```

`ImageOrPrintOptions` ελέγχει τη μορφή εξόδου. Επιλέγοντας `ImageFormat.Png`, εξασφαλίζετε μια εικόνα υψηλής ανάλυσης με διαφανές φόντο που λειτουργεί καλά σε περιβάλλοντα web και desktop.

## Βήμα 4: Δημιουργήστε μια εικόνα από το καθορισμένο εύρος και **add picture to worksheet**

```csharp
// Create a picture object from the selected range
Picture picture = workbook.Worksheets[0].Pictures.Add(
    0,                                     // top‑left row index where the picture will be placed
    0,                                     // top‑left column index where the picture will be placed
    workbook.Worksheets[0].Cells.CreateRange(printArea));
```

Η μέθοδος `Pictures.Add` εισάγει μια νέα εικόνα στο φύλλο εργασίας. Με τη μεταβίβαση του εύρους που δημιουργήθηκε στο Βήμα 2, **save range as image** απευθείας στο φύλλο, κάτι που είναι χρήσιμο αν αργότερα χρειαστείτε να αναφερθείτε στην εικόνα σε άλλα τμήματα του βιβλίου εργασίας.

## Βήμα 5: **Save the picture as an image file** – ολοκληρώνοντας τη ροή εργασίας **export selected cells image**

```csharp
// Save the picture to disk as a PNG file
picture.Save(@"YOUR_DIRECTORY\selected_range.png", imageOptions);
```

Καλώντας το `Save` η εικόνα γράφεται στο σύστημα αρχείων χρησιμοποιώντας τις επιλογές που ορίστηκαν στο Βήμα 3. Το αποτέλεσμα `selected_range.png` περιέχει ακριβώς τα κελιά που ορίστηκαν από την εντολή **set print area excel**.

## Πλήρες, εκτελέσιμο παράδειγμα

Συνδυάζοντας όλα τα κομμάτια μαζί, παίρνετε ένα συμπαγές πρόγραμμα που μπορείτε να ενσωματώσετε σε οποιαδήποτε εφαρμογή κονσόλας:

```csharp
using System;
using Aspose.Cells;
using System.Drawing.Imaging;

class ExportExcelRangeAsPng
{
    static void Main()
    {
        // 1️⃣ Load the workbook
        Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

        // 2️⃣ Set print area excel
        string printArea = "A1:G20";
        workbook.Worksheets[0].PageSetup.PrintArea = printArea;

        // 3️⃣ Configure how to export png
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
        {
            ImageFormat = ImageFormat.Png,
            OnePagePerSheet = true
        };

        // 4️⃣ Add picture to worksheet (save range as image)
        Picture picture = workbook.Worksheets[0].Pictures.Add(
            0,
            0,
            workbook.Worksheets[0].Cells.CreateRange(printArea));

        // 5️⃣ Export selected cells image
        picture.Save(@"YOUR_DIRECTORY\selected_range.png", imageOptions);

        Console.WriteLine("PNG exported successfully to YOUR_DIRECTORY\\selected_range.png");
    }
}
```

### Αναμενόμενη έξοδος

```
PNG exported successfully to YOUR_DIRECTORY\selected_range.png
```

Και θα βρείτε ένα αρχείο `selected_range.png` που εμφανίζει μόνο τα κελιά A1 έως G20 από το `input.xlsx`.

## Συνηθισμένα προβλήματα και πώς να τα αποφύγετε

| Πρόβλημα | Γιατί συμβαίνει | Διόρθωση |
|----------|----------------|----------|
| Η εξαγόμενη εικόνα περιέχει ολόκληρο το φύλλο | Δεν ορίστηκε περιοχή εκτύπωσης | Βεβαιωθείτε ότι έχετε **set print area excel** πριν δημιουργήσετε την εικόνα |
| Το PNG είναι θολό | Η προεπιλεγμένη ανάλυση DPI είναι χαμηλή | Ορίστε `imageOptions.DpiX` και `imageOptions.DpiY` σε υψηλότερη τιμή (π.χ., 300) |
| Σφάλμα αρχείου δεν βρέθηκε | Λανθασμένη διαδρομή φακέλου | Χρησιμοποιήστε `Path.Combine` ή ελέγξτε ξανά ότι ο φάκελος υπάρχει |
| Η εικόνα εμφανίζεται μετατοπισμένη | Λανθασμένοι δείκτες γραμμής/στήλης | Οι δύο πρώτες παράμετροι του `Pictures.Add` είναι το κελί επάνω‑αριστερά όπου τοποθετείται η εικόνα· κρατήστε τις στο `0,0` για καθαρή εξαγωγή |

## Συμβουλή επαγγελματία: Εξαγωγή πολλαπλών περιοχών σε μία εκτέλεση

Αν χρειάζεστε **export selected cells image** για πολλές περιοχές, επαναλάβετε τα Βήματα 2‑5 μέσα σε βρόχο, αλλάζοντας το `printArea` σε κάθε επανάληψη. Θυμηθείτε να δώσετε σε κάθε εικόνα μοναδικό όνομα αρχείου, διαφορετικά η επόμενη αποθήκευση θα αντικαταστήσει το προηγούμενο αρχείο.

## Συμπέρασμα

Τώρα ξέρετε πώς να **set print area excel**, να διαμορφώσετε **how to export png**, **save range as image**, και **add picture to worksheet** χρησιμοποιώντας το Aspose.Cells. Αυτή η ολοκληρωμένη λύση σας επιτρέπει να μετατρέψετε οποιοδήποτε μπλοκ κελιών σε PNG υψηλής ποιότητας με λίγες μόνο γραμμές κώδικα C#.

Στη συνέχεια, μπορείτε να εξερευνήσετε:

* Προσθήκη περιγραμμάτων ή υδατογραφήματος στην εξαγόμενη PNG (αναζητήστε *add picture to worksheet* με στυλ)
* Άμεση εξαγωγή σε PDF για εκτυπώσιμες αναφορές (*export selected cells image* → ροή εργασίας PDF)
* Αυτοματοποίηση της διαδικασίας για πολλά βιβλία εργασίας σε εργασία batch

Μη διστάσετε να πειραματιστείτε με διαφορετικά εύρη, ρυθμίσεις DPI ή μορφές εικόνας ώστε να ταιριάζουν στις ανάγκες του έργου σας. Καλή προγραμματιστική!

## Τι Θα Πρέπει Να Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που βασίζονται στις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Set Print Area in Excel and Export to PowerPoint – Step‑by‑Step Guide](/cells/english/net/converting-excel-files-to-other-formats/set-print-area-in-excel-and-export-to-powerpoint-step-by-ste/)
- [Export Excel Print Area to HTML with Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-print-area-html-aspose-cells-java/)
- [How to Set a Print Area in Excel Using Aspose.Cells for .NET](/cells/english/net/headers-footers/set-print-area-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}