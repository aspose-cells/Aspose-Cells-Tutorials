---
category: general
date: 2026-03-30
description: Δημιουργήστε PowerPoint από το Excel γρήγορα χρησιμοποιώντας το Aspose.Cells
  και το Aspose.Slides. Μάθετε πώς να εξάγετε το φύλλο εργασίας ως εικόνα και να αποθηκεύσετε
  την παρουσίαση ως PPTX σε C#.
draft: false
keywords:
- create powerpoint from excel
- convert excel to powerpoint
- export worksheet as image
- save presentation as pptx
- export excel chart as picture
language: el
og_description: Δημιουργήστε PowerPoint από το Excel σε C# με το Aspose. Εξάγετε το
  φύλλο εργασίας ως εικόνα, διατηρήστε τα σχήματα επεξεργάσιμα και αποθηκεύστε το
  αποτέλεσμα ως PPTX.
og_title: Δημιουργία PowerPoint από Excel – Πλήρης οδηγός C#
tags:
- Aspose
- C#
- Office Automation
title: Δημιουργία PowerPoint από Excel – Οδηγός C# βήμα‑προς‑βήμα
url: /el/net/converting-excel-files-to-other-formats/create-powerpoint-from-excel-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία PowerPoint από Excel – Πλήρης Οδηγός C#

Έχετε χρειαστεί ποτέ να **δημιουργήσετε PowerPoint από Excel** αλλά δεν ήσασταν σίγουροι ποια βιβλιοθήκη μπορεί να διατηρήσει τα διαγράμματα σας επεξεργάσιμα; Δεν είστε μόνοι. Σε πολλές περιπτώσεις αναφοράς θα θέλετε να μετατρέψετε ένα λογιστικό φύλλο σε μια παρουσίαση χωρίς να χάσετε τη δυνατότητα να προσαρμόσετε τα πλαίσια κειμένου αργότερα. Αυτός ο οδηγός σας δείχνει ακριβώς πώς να **μετατρέψετε το Excel σε PowerPoint** χρησιμοποιώντας Aspose.Cells και Aspose.Slides, καλύπτοντας επίσης πώς να **εξάγετε το φύλλο εργασίας ως εικόνα** και τελικά **αποθηκεύσετε την παρουσίαση ως PPTX**.

Θα περάσουμε από κάθε γραμμή κώδικα, θα εξηγήσουμε *γιατί* κάθε ρύθμιση είναι σημαντική, και ακόμη θα συζητήσουμε τι να κάνετε αν το βιβλίο εργασίας σας περιέχει σύνθετα διαγράμματα που προτιμάτε να εξάγετε ως εικόνα. Στο τέλος θα έχετε μια έτοιμη‑για‑εκτέλεση εφαρμογή C# console που παίρνει το `ShapesDemo.xlsx` και παράγει το `Result.pptx` – όλα με επεξεργάσιμα πλαίσια κειμένου και καθαρές εικόνες.

## Τι Θα Χρειαστεί

- .NET 6.0 ή νεότερο (το API λειτουργεί και με .NET Framework, αλλά το .NET 6 είναι η ιδανική επιλογή).  
- Πακέτα NuGet **Aspose.Cells** και **Aspose.Slides** (δωρεάν δοκιμαστικές άδειες λειτουργούν για δοκιμές).  
- Βασική εξοικείωση με τη σύνταξη C# – αν μπορείτε να γράψετε ένα `Console.WriteLine`, είστε έτοιμοι.

Καμία πρόσθετη COM διασύνδεση, χωρίς εγκατεστημένο Office στον διακομιστή, και χωρίς χειροκίνητη αντιγραφή‑επικόλληση εικόνων. Όλα διαχειρίζονται προγραμματιστικά.

---

## Δημιουργία PowerPoint από Excel – Φόρτωση Βιβλίου Εργασίας και Ορισμός Επιλογών Εξαγωγής

Το πρώτο που κάνουμε είναι να ανοίξουμε το αρχείο Excel και να πούμε στο Aspose.Cells πώς θέλουμε να αποδοθεί το φύλλο. Το αντικείμενο `ImageOrPrintOptions` είναι όπου συμβαίνει η μαγεία: ενεργοποιούμε το `ExportShapes` και το `ExportEditableTextBoxes` ώστε οποιοδήποτε σχήμα (συμπεριλαμβανομένων των διαγραμμάτων) να γίνει μέρος της διαφάνειας **και** να παραμείνει επεξεργάσιμο μετά τη μετατροπή.

```csharp
using Aspose.Cells;
using Aspose.Slides;

// 1️⃣ Load the Excel workbook
string excelPath = "YOUR_DIRECTORY/ShapesDemo.xlsx";
Workbook workbook = new Workbook(excelPath);
Worksheet worksheet = workbook.Worksheets[0];   // Grab the first sheet

// 2️⃣ Configure image export – keep shapes editable
ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
{
    OnePagePerSheet = true,          // Export the whole sheet as one slide
    ExportShapes = true,             // Include shapes (charts, drawings)
    ExportEditableTextBoxes = true   // Make text boxes editable in PPTX
};
```

**Γιατί αυτά τα flags;**  
- `OnePagePerSheet` αποτρέπει το φύλλο να χωριστεί σε πολλές διαφάνειες – παίρνετε μια ενιαία, πλήρους‑μεγέθους εικόνα.  
- `ExportShapes` λέει στο Aspose.Cells να ραστεροποιήσει τα διαγράμματα *και* τα διανυσματικά σχήματα, διατηρώντας την εμφάνισή τους.  
- `ExportEditableTextBoxes` είναι το μυστικό συστατικό που σας επιτρέπει να κάνετε διπλό‑κλικ σε ένα πλαίσιο κειμένου στο PowerPoint και να επεξεργαστείτε το κείμενο χωρίς να ανοίξετε ξανά το Excel.

> **Συμβουλή:** Αν χρειάζεστε μόνο μια στατική εικόνα ενός διαγράμματος, ορίστε `ExportShapes = false` και χρησιμοποιήστε τη μέθοδο `ExportExcelChartAsPicture` αργότερα (δείτε την τελική ενότητα).

---

## Μετατροπή Excel σε PowerPoint – Δημιουργία Εικόνας από Φύλλο Εργασίας

Με τις επιλογές έτοιμες, τώρα μετατρέπουμε το φύλλο εργασίας σε ένα `System.Drawing.Image`. Η `WorksheetToImageConverter` κάνει τη βαριά δουλειά, εφαρμόζοντας τις ρυθμίσεις που μόλις ορίσαμε.

```csharp
// 3️⃣ Convert the worksheet to an image using the options above
WorksheetToImageConverter converter = new WorksheetToImageConverter(worksheet);
System.Drawing.Image sheetImage = converter.ConvertToImage(0, imageOptions);
```

Το όρισμα `0` υποδεικνύει την πρώτη σελίδα (έχουμε μόνο μία λόγω του `OnePagePerSheet`). Η προκύπτουσα `sheetImage` διατηρεί το αρχικό DPI, ώστε η διαφάνειά σας να μην φαίνεται pixelated ακόμη και σε οθόνες υψηλής ανάλυσης.

---

## Αποθήκευση Παρουσίασης ως PPTX – Εισαγωγή Εικόνας σε Διαφάνεια

Τώρα δημιουργούμε ένα νέο αρχείο PowerPoint, προσθέτουμε μια διαφάνεια και τοποθετούμε το bitmap σε αυτήν. Το Aspose.Slides αντιμετωπίζει την εικόνα ως σχήμα *picture frame*, το οποίο μπορείτε αργότερα να αλλάξετε σε μέγεθος ή να μετακινήσετε όπως οποιοδήποτε ενσωματωμένο αντικείμενο PowerPoint.

```csharp
// 4️⃣ Create a new PowerPoint presentation
Presentation presentation = new Presentation();
ISlide slide = presentation.Slides[0];   // The default blank slide

// Add the Excel‑derived image as a picture frame
slide.Shapes.AddPictureFrame(
    ShapeType.Rectangle,                 // Simple rectangle container
    0, 0,                                // Top‑left corner (0,0)
    sheetImage.Width,                    // Width of the picture
    sheetImage.Height,                   // Height of the picture
    sheetImage);                         // The bitmap we generated
```

> **Τι γίνεται αν η εικόνα είναι μεγαλύτερη από το μέγεθος της διαφάνειας;**  
> Το PowerPoint θα κόψει αυτόματα οτιδήποτε υπερβαίνει τις διαστάσεις της διαφάνειας. Μια γρήγορη λύση είναι να κλιμακώσετε την εικόνα πριν την εισαγάγετε:

```csharp
float scale = Math.Min(presentation.SlideSize.Size.Width / (float)sheetImage.Width,
                       presentation.SlideSize.Size.Height / (float)sheetImage.Height);
int newWidth  = (int)(sheetImage.Width * scale);
int newHeight = (int)(sheetImage.Height * scale);
```

Στη συνέχεια μπορείτε να περάσετε τα `newWidth` και `newHeight` στη μέθοδο `AddPictureFrame`.

---

## Εξαγωγή Φύλλου Εργασίας ως Εικόνα – Αποθήκευση του Αρχείου PPTX

Τέλος αποθηκεύουμε την παρουσίαση στο δίσκο. Η σημαία `SaveFormat.Pptx` εγγυάται τη σύγχρονη μορφή OpenXML, η οποία λειτουργεί σε όλες τις πρόσφατες εκδόσεις του PowerPoint.

```csharp
// 5️⃣ Save the presentation as a PPTX file
string pptxPath = "YOUR_DIRECTORY/Result.pptx";
presentation.Save(pptxPath, SaveFormat.Pptx);
```

Όταν ανοίξετε το `Result.pptx` θα δείτε μια ενιαία διαφάνεια που φαίνεται ακριβώς όπως το φύλλο Excel σας, αλλά μπορείτε ακόμη να κάνετε κλικ σε οποιοδήποτε πλαίσιο κειμένου και να επεξεργαστείτε το περιεχόμενό του απευθείας στο PowerPoint.

---

## Εξαγωγή Διαγράμματος Excel ως Εικόνα – Όταν Προτιμώνται Raster Εικόνες

Μερικές φορές δεν χρειάζεστε επεξεργάσιμα σχήματα· ένα υψηλής ποιότητας PNG ενός διαγράμματος αρκεί. Το Aspose.Cells μπορεί να εξάγει ένα συγκεκριμένο διάγραμμα σε εικόνα χωρίς να μετατρέπει ολόκληρο το φύλλο:

```csharp
// Example: Export the first chart on the sheet as a PNG
int chartIndex = 0; // Adjust if you have multiple charts
Chart chart = worksheet.Charts[chartIndex];
ImageOrPrintOptions chartOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Png,
    OnePagePerSheet = false
};
chart.ToImage("chart.png", chartOptions);
```

Στη συνέχεια μπορείτε να ενσωματώσετε το `chart.png` σε μια διαφάνεια με τον ίδιο τρόπο που προσθέσαμε το `sheetImage`. Αυτή η προσέγγιση μειώνει το μέγεθος του αρχείου PPTX και είναι χρήσιμη όταν τα περιβάλλοντα δεδομένα δεν χρειάζονται στη διαφάνεια.

---

## Συνηθισμένα Προβλήματα & Πώς να τα Αποφύγετε

| Πρόβλημα | Γιατί συμβαίνει | Διόρθωση |
|----------|----------------|----------|
| **Το κείμενο φαίνεται θολό** | Εξάγεται με χαμηλό DPI (προεπιλογή 96). | Ορίστε `imageOptions.Dpi = 300;` πριν τη μετατροπή. |
| **Τα σχήματα εξαφανίζονται** | `ExportShapes` παραμένει `false`. | Βεβαιωθείτε ότι `ExportShapes = true` όταν χρειάζεστε επεξεργάσιμα γραφικά. |
| **Ασυμφωνία μεγέθους διαφάνειας** | Η εικόνα είναι μεγαλύτερη από τις διαστάσεις της διαφάνειας. | Κλιμακώστε την εικόνα (δείτε το απόσπασμα κώδικα) ή αλλάξτε το μέγεθος της διαφάνειας μέσω του `presentation.SlideSize`. |
| **Εξαίρεση άδειας** | Χρήση δοκιμαστικής έκδοσης χωρίς σωστή ενεργοποίηση. | Καλέστε `License license = new License(); license.SetLicense("Aspose.Total.lic");` νωρίς στο `Main`. |

---

## Πλήρες Παράδειγμα Εργασίας (Έτοιμο για Αντιγραφή‑Επικόλληση)

Παρακάτω βρίσκεται ολόκληρο το πρόγραμμα, έτοιμο να ενσωματωθεί σε ένα νέο έργο console. Αντικαταστήστε το `YOUR_DIRECTORY` με το φάκελο που περιέχει το αρχείο Excel σας.

```csharp
using System;
using Aspose.Cells;
using Aspose.Slides;
using System.Drawing;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // 1️⃣ Load the Excel workbook
            // -----------------------------------------------------------------
            string excelPath = "YOUR_DIRECTORY/ShapesDemo.xlsx";
            Workbook workbook = new Workbook(excelPath);
            Worksheet worksheet = workbook.Worksheets[0];

            // -----------------------------------------------------------------
            // 2️⃣ Set up export options – keep shapes editable
            // -----------------------------------------------------------------
            ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
            {
                OnePagePerSheet = true,
                ExportShapes = true,
                ExportEditableTextBoxes = true,
                Dpi = 300                 // High‑resolution output
            };

            // -----------------------------------------------------------------
            // 3️⃣ Convert worksheet to an image
            // -----------------------------------------------------------------
            WorksheetToImageConverter converter = new WorksheetToImageConverter(worksheet);
            Image sheetImage = converter.ConvertToImage(0, imageOptions);

            // -----------------------------------------------------------------
            // 4️⃣ Create PowerPoint and add the image as a slide
            // -----------------------------------------------------------------
            Presentation presentation = new Presentation();
            ISlide slide = presentation.Slides[0];
            slide.Shapes.AddPictureFrame(
                ShapeType.Rectangle,
                0, 0,
                sheetImage.Width,
                sheetImage.Height,
                sheetImage);

            // -----------------------------------------------------------------
            // 5️⃣ Save the PPTX file
            // -----------------------------------------------------------------
            string pptxPath = "YOUR_DIRECTORY/Result.pptx";
            presentation.Save(pptxPath, SaveFormat.Pptx);

            Console.WriteLine("✅ PowerPoint created successfully at: " + pptxPath);
        }
    }
}
```

**Αναμενόμενο αποτέλεσμα:**  
Η εκτέλεση του προγράμματος εκτυπώνει `✅ PowerPoint created successfully at: YOUR_DIRECTORY/Result.pptx`. Το άνοιγμα του PPTX εμφανίζει μια ενιαία διαφάνεια που αντικατοπτρίζει το αρχικό φύλλο Excel, με επεξεργάσιμα πλαίσια κειμένου.

---

## Ανακεφαλαίωση & Επόμενα Βήματα

Τώρα ξέρετε πώς να **δημιουργήσετε PowerPoint από Excel** χρησιμοποιώντας τα ισχυρά API της Aspose, πώς να **εξάγετε το φύλλο εργασίας ως εικόνα**, και πώς να **αποθηκεύσετε την παρουσίαση ως PPTX** διατηρώντας την επεξεργασιμότητα. Το ίδιο μοτίβο λειτουργεί για βιβλία εργασίας με πολλά φύλλα — απλώς κάντε βρόχο μέσω του `workbook.Worksheets` και προσθέστε μια νέα διαφάνεια για κάθε ένα.

**Τι να εξερευνήσετε στη συνέχεια;**  

- **Μαζική μετατροπή:** Κάντε βρόχο σε έναν φάκελο Excel αρχείων και δημιουργήστε μια παρουσίαση ανά αρχείο.  
- **Δυναμικές διατάξεις:** Χρησιμοποιήστε το `slide.LayoutSlide` για να εφαρμόσετε προ‑σχεδιασμένα πρότυπα PowerPoint.  
- **Εξαγωγή μόνο διαγράμματος:** Συνδυάστε το απόσπασμα “Export Excel chart as picture” με placeholders διαφάνειας για μια πιο ελαφριά παρουσίαση.  
- **Προηγμένη μορφοποίηση:** Εφαρμόστε προσαρμοσμένα φόντα διαφάνειας, μεταβάσεις ή animation μέσω του Aspose.Slides.

Μη διστάσετε να πειραματιστείτε — αλλάξτε το DPI, αντικαταστήστε το `ShapeType.Ellipse` με ένα κυκλικό picture frame, ή ακόμη ενσωματώστε πολλαπλές εικόνες ανά διαφάνεια. Ο ουρανός είναι το όριο όταν έχετε προγραμματιστικό έλεγχο πάνω σε

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}