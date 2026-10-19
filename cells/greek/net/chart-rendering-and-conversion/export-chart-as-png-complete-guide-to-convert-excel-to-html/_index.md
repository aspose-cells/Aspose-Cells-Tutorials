---
category: general
date: 2026-06-30
description: Εξαγωγή διαγράμματος ως PNG ενώ μετατρέπετε το Excel σε HTML χρησιμοποιώντας
  το Aspose.Cells. Μάθετε πώς να ενσωματώνετε εικόνες ως Base64 και να αποθηκεύετε
  το βιβλίο εργασίας ως HTML σε λίγα λεπτά.
draft: false
keywords:
- export chart as png
- convert excel to html
- embed images as base64
- save workbook as html
- export excel chart to png
language: el
og_description: Εξαγωγή διαγράμματος ως PNG και ενσωμάτωση εικόνων ως Base64 κατά
  τη μετατροπή του Excel σε HTML. Ακολουθήστε αυτόν τον βήμα‑βήμα οδηγό C# για να
  αποθηκεύσετε το βιβλίο εργασίας ως HTML χωρίς κόπο.
og_title: Εξαγωγή γραφήματος ως PNG – Μετατροπή Excel σε HTML με το Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Export chart as PNG while you convert Excel to HTML using Aspose.Cells.
    Learn to embed images as Base64 and save workbook as HTML in minutes.
  headline: Export Chart as PNG – Complete Guide to Convert Excel to HTML with Aspose.Cells
  type: TechArticle
- description: Export chart as PNG while you convert Excel to HTML using Aspose.Cells.
    Learn to embed images as Base64 and save workbook as HTML in minutes.
  name: Export Chart as PNG – Complete Guide to Convert Excel to HTML with Aspose.Cells
  steps:
  - name: Open Visual Studio and create a new **Console App** (`dotnet new console`).
    text: Open Visual Studio and create a new **Console App** (`dotnet new console`).
  - name: 'Add the Aspose.Cells NuGet package:'
    text: 'Add the Aspose.Cells NuGet package:'
  - name: '(Optional) If you have a license file, place it in the project root and
      activate it at runtime:'
    text: '(Optional) If you have a license file, place it in the project root and
      activate it at runtime:'
  - name: Open the generated HTML in Chrome. Right‑click the chart image and select
      **Open image in new tab**. The URL will still start with `data:image/png;base64,`.
    text: Open the generated HTML in Chrome. Right‑click the chart image and select
      **Open image in new tab**. The URL will still start with `data:image/png;base64,`.
  - name: 'If the image appears blurry, consider increasing the chart’s resolution
      before saving:'
    text: 'If the image appears blurry, consider increasing the chart’s resolution
      before saving:'
  - name: 'For charts that rely on external data sources, make sure the workbook is
      fully refreshed before saving:'
    text: 'For charts that rely on external data sources, make sure the workbook is
      fully refreshed before saving:'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Εξαγωγή διαγράμματος ως PNG – Πλήρης οδηγός για τη μετατροπή του Excel σε HTML
  με το Aspose.Cells
url: /el/net/chart-rendering-and-conversion/export-chart-as-png-complete-guide-to-convert-excel-to-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή Διαγράμματος ως PNG – Πλήρης Οδηγός για τη Μετατροπή Excel σε HTML με το Aspose.Cells

Έχετε αναρωτηθεί ποτέ πώς να **εξάγετε διάγραμμα ως PNG** απευθείας από ένα βιβλίο εργασίας Excel ενώ ταυτόχρονα μετατρέπετε ολόκληρο το φύλλο σε καθαρό, ανταποκρινόμενο HTML; Δεν είστε οι μόνοι. Πολλοί προγραμματιστές συναντούν εμπόδια όταν χρειάζονται μια αναφορά έτοιμη για το web που εμφανίζει διαγράμματα χωρίς να διαχειρίζονται ξεχωριστά αρχεία εικόνας. Τα καλά νέα είναι ότι το Aspose.Cells το κάνει παιχνιδάκι.

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από τα ακριβή βήματα για **μετατροπή Excel σε HTML**, **ενσωμάτωση εικόνων ως Base64**, και τελικά **αποθήκευση βιβλίου εργασίας ως HTML**—όλα ενώ εξασφαλίζουμε ότι κάθε διάγραμμα αποθηκεύεται ως εικόνα PNG. Στο τέλος θα έχετε ένα ενιαίο αρχείο HTML που μπορείτε να ενσωματώσετε σε οποιαδήποτε ιστοσελίδα, και κάθε διάγραμμα θα εμφανίζεται αμέσως, χωρίς επιπλέον πόρους.

## Τι Θα Μάθετε

- Πώς να φορτώσετε ένα υπάρχον βιβλίο εργασίας που ήδη περιέχει διαγράμματα.  
- Ποια σημαία του `HtmlSaveOptions` ελέγχει την εξαγωγή εικόνας, τη μορφή διαγράμματος και την ανταπόκριση.  
- Τον ακριβή κώδικα που απαιτείται για **εξαγωγή διαγράμματος ως PNG** και ενσωμάτωση αυτών των PNG ως συμβολοσειρές Base64.  
- Πώς να **αποθηκεύσετε το βιβλίο εργασίας ως HTML** με μία μόνο κλήση μεθόδου.  
- Συμβουλές για την αντιμετώπιση κοινών προβλημάτων, όπως ελλιπείς εικόνες διαγράμματος ή υπερβολικά μεγάλες συμβολοσειρές Base64.  

**Προαπαιτούμενα:**  
- .NET 6+ (ή .NET Framework 4.6+) εγκατεστημένο.  
- Ένα έγκυρο license του Aspose.Cells (ή ένα προσωρινό κλειδί αξιολόγησης).  
- Βασική εξοικείωση με C# και Visual Studio (ή το αγαπημένο σας IDE).  

Αν κάποιο από αυτά δεν σας είναι γνωστό, κάντε ένα διάλειμμα και ρυθμίστε το· το υπόλοιπο του οδηγού υποθέτει ότι είναι έτοιμο.

---

## Βήμα 1: Ρύθμιση Έργου και Εγκατάσταση Aspose.Cells

Προτού μπορέσουμε να **εξάγουμε διάγραμμα ως PNG**, χρειαζόμαστε ένα έργο C# που να αναφέρεται στη βιβλιοθήκη Aspose.Cells.

1. Ανοίξτε το Visual Studio και δημιουργήστε μια νέα **Console App** (`dotnet new console`).  
2. Προσθέστε το πακέτο NuGet Aspose.Cells:

```bash
dotnet add package Aspose.Cells
```

3. (Προαιρετικό) Αν έχετε αρχείο license, τοποθετήστε το στη ρίζα του έργου και ενεργοποιήστε το κατά το χρόνο εκτέλεσης:

```csharp
// Activate license – skip this line if you’re using the trial version
Aspose.Cells.License license = new Aspose.Cells.License();
license.SetLicense("Aspose.Cells.lic");
```

> **Pro tip:** Κρατήστε το αρχείο license εκτός ελέγχου πηγαίου κώδικα. Χρησιμοποιήστε μεταβλητές περιβάλλοντος ή ασφαλείς αποθήκες μυστικών για παραγωγή.

---

## Βήμα 2: Φόρτωση του Βιβλίου Εργασίας που Περιέχει το Διάγραμμα

Τώρα θα φορτώσουμε το αρχείο Excel που ήδη έχει το διάγραμμα που θέλουμε να **εξάγουμε διάγραμμα ως PNG**.

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;   // Needed for ImageFormat enum

// Path to the source workbook – change this to your actual file location
string sourcePath = @"C:\Reports\ReportWithChart.xlsx";

// Load the workbook
Workbook workbook = new Workbook(sourcePath);
```

> **Γιατί είναι σημαντικό:** Η φόρτωση του βιβλίου εργασίας νωρίς μας δίνει πρόσβαση σε όλα τα φύλλα, τα διαγράμματα και τα ενσωματωμένα αντικείμενα. Αν η φόρτωση αποτύχει, το επόμενο βήμα **εξαγωγής διαγράμματος σε PNG** δεν θα εκτελεστεί ποτέ.

---

## Βήμα 3: Διαμόρφωση των Ρυθμίσεων Αποθήκευσης HTML

Η καρδιά της λύσης βρίσκεται στο `HtmlSaveOptions`. Με την εναλλαγή μερικών ιδιοτήτων μπορούμε να:

- **ExportChartImageFormat = ImageFormat.Png** → εξασφαλίζει ότι κάθε διάγραμμα γίνεται PNG.  
- **ExportImagesAsBase64 = true** → ενσωματώνει τα δεδομένα PNG απευθείας στο HTML, εξαλείφοντας τα εξωτερικά αρχεία.  
- **IsResponsive = true** → κάνει τους παραγόμενους πίνακες προσαρμόσιμους σε κινητές οθόνες.  
- **ExportPrintingHeadersFooters = false** → αφαιρεί περιττά μεταδεδομένα εκτύπωσης.  

Ακολουθεί η πλήρης διαμόρφωση:

```csharp
// Create HTML save options and fine‑tune them
HtmlSaveOptions htmlOptions = new HtmlSaveOptions
{
    // 1️⃣ Embed PNG/JPEG images directly as Base64 strings
    ExportImagesAsBase64 = true,

    // 2️⃣ Force chart images to be saved as PNG files
    ExportChartImageFormat = ImageFormat.Png,

    // 3️⃣ Omit printing headers/footers for a cleaner web view
    ExportPrintingHeadersFooters = false,

    // 4️⃣ Generate responsive tables for mobile friendliness
    IsResponsive = true,

    // 5️⃣ Target modern browsers with HTML5
    HtmlVersion = HtmlVersion.Html5
};
```

### Γιατί Αυτές οι Ρυθμίσεις;

- **ExportChartImageFormat = ImageFormat.Png** είναι ο μοναδικός τρόπος να εγγυηθείτε μια απώλεια‑απλή, web‑ασφαλή εικόνα διαγράμματος.  
- **ExportImagesAsBase64 = true** σημαίνει ότι μπορείτε να **ενσωματώσετε εικόνες ως Base64**, ιδανικό για αναφορές email ή ανάπτυξη σε ένα μόνο αρχείο.  
- **IsResponsive = true** λύνει ένα συχνό παράπονο: πίνακες που ξεχειλίζουν σε smartphones.  
- **ExportPrintingHeadersFooters = false** κρατά το HTML ελαφρύ—χωρίς κρυφές πληροφορίες εκτύπωσης που δεν χρησιμοποιούνται στο web.  

---

## Βήμα 4: Αποθήκευση του Βιβλίου Εργασίας ως HTML

Με τις ρυθμίσεις έτοιμες, η τελική γραμμή είναι μια ενιαία κλήση που τόσο **μετατρέπει το Excel σε HTML** όσο και **εξάγει το διάγραμμα ως PNG** στο παρασκήνιο.

```csharp
// Destination HTML file – adjust the folder as needed
string outputPath = @"C:\Reports\Report.html";

// Save the workbook using the configured options
workbook.Save(outputPath, htmlOptions);
```

Όταν αυτή η γραμμή ολοκληρωθεί, θα έχετε ένα αρχείο που ονομάζεται `Report.html`. Ανοίξτε το σε οποιονδήποτε περιηγητή και θα δείτε:

- Όλα τα δεδομένα των φύλλων ως καθαρούς HTML πίνακες.  
- Κάθε διάγραμμα εμφανιζόμενο ως ενσωματωμένη PNG εικόνα (ευχαριστώντας την ενσωμάτωση Base64).  
- Καμία επιπλέον εικόνα δίπλα στο HTML.  

### Αναμενόμενο Αποτέλεσμα

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>Report</title>
    <style>
        /* Aspose.Cells generated responsive CSS */
    </style>
</head>
<body>
    <table class="aspose">
        <!-- Table rows here -->
    </table>

    <!-- Example of an embedded chart image -->
    <img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAA..." alt="Chart 1" />
</body>
</html>
```

Παρατηρήστε το χαρακτηριστικό `src="data:image/png;base64,..."`—αυτή είναι η **μαγεία ενσωμάτωσης εικόνων ως base64**. Δεν δημιουργούνται ξεχωριστά αρχεία `.png` στο δίσκο.

---

## Βήμα 5: Επαλήθευση της Εξαγωγής PNG και Ρύθμιση Αν Χρειαστεί

Μερικές φορές ένα διάγραμμα μπορεί να φαίνεται ελαφρώς αλλοιωμένο μετά τη μετατροπή, ειδικά αν χρησιμοποιεί προσαρμοσμένες γραμματοσειρές ή πολύπλοκα διαβαθμίσεις. Να πώς να το ελέγξετε:

1. Ανοίξτε το παραγόμενο HTML στο Chrome. Κάντε δεξί‑κλικ στην εικόνα του διαγράμματος και επιλέξτε **Open image in new tab**. Η διεύθυνση θα εξακολουθεί να ξεκινά με `data:image/png;base64,`.  
2. Αν η εικόνα φαίνεται θολή, σκεφτείτε να αυξήσετε την ανάλυση του διαγράμματος πριν την αποθήκευση:

```csharp
htmlOptions.ImageResolution = 300; // DPI – higher values = sharper PNGs
```

3. Για διαγράμματα που εξαρτώνται από εξωτερικές πηγές δεδομένων, βεβαιωθείτε ότι το βιβλίο εργασίας είναι πλήρως ενημερωμένο πριν την αποθήκευση:

```csharp
workbook.CalculateFormula(); // Force recalculation
```

Αυτές οι προσαρμογές διασφαλίζουν ότι το βήμα **εξαγωγής διαγράμματος Excel σε PNG** παράγει καθαρά, έτοιμα για παραγωγή γραφικά.

---

## Βήμα 6: Ανάπτυξη του HTML Οπουδήποτε

Επειδή όλες οι εικόνες είναι ενσωματωμένες, μπορείτε τώρα:

- Να στείλετε το HTML ως ένα ενιαίο συνημμένο email.  
- Να επικολλήσετε το HTML σε ένα CMS που δέχεται ακατέργαστο κώδικα.  
- Να το φιλοξενήσετε σε έναν στατικό ιστότοπο χωρίς να ανησυχείτε για ελλείπουσες PNG εικόνες.  

Αν ποτέ χρειαστείτε τα αρχεία PNG ως ξεχωριστά στοιχεία (ίσως για PDF αργότερα), μπορείτε να αλλάξετε το `ExportImagesAsBase64` σε `false` και να ορίσετε το `HtmlSaveOptions` σε φάκελο εξόδου για εικόνες.

```csharp
htmlOptions.ExportImagesAsBase64 = false;
htmlOptions.ImageFolder = @"C:\Reports\Images";
```

Τώρα το HTML θα αναφέρεται σε εξωτερικά αρχεία PNG, διατηρώντας την **εξαγωγή διαγράμματος ως PNG** αλλά παρέχοντας ξεχωριστές εικόνες για άλλες χρήσεις.

---

## Συνηθισμένα Προβλήματα & Πώς να τα Αποφύγετε

| Σύμπτωμα | Πιθανή Αιτία | Διόρθωση |
|----------|--------------|----------|
| Το διάγραμμα λείπει από το HTML | `ExportChartImageFormat` παραμένει στην προεπιλογή (`Jpeg`) και ο περιηγητής μπλοκάρει μεικτό περιεχόμενο. | Ορίστε `ExportChartImageFormat = ImageFormat.Png`. |
| Το αρχείο HTML είναι τεράστιο (πολλές MB) | Μεγάλες εικόνες ή πολλές υψηλής ανάλυσης εικόνες ενσωματωμένες ως Base64. | Μειώστε το `htmlOptions.ImageResolution` ή συμπιέστε το διάγραμμα στο Excel πριν τη μετατροπή. |
| Οι πίνακες ξεχειλούν σε κινητά | `IsResponsive` δεν είναι ενεργοποιημένο. | Βεβαιωθείτε ότι `IsResponsive = true` στο `HtmlSaveOptions`. |
| Οι συμβολοσειρές Base64 περιέχουν χαρακτήρες νέας γραμμής | Παλαιότερες εκδόσεις .NET μπορεί να τυλίγουν μεγάλες συμβολοσειρές. | Αναβαθμίστε σε .NET 6+ ή ορίστε `htmlOptions.ExportBase64StringInOneLine = true`. |

---

## Bonus: Συσκευασία Όλων σε Μία Επαναχρησιμοποιήσιμη Μέθοδο

Αν θα κάνετε αυτή τη μετατροπή επανειλημμένα, τυλίξτε τη λογική σε μια μέθοδο:

```csharp
public static void ConvertExcelToHtmlWithPngCharts(string excelPath, string htmlPath)
{
    // Load workbook
    Workbook wb = new Workbook(excelPath);

    // Prepare options
    HtmlSaveOptions opts = new HtmlSaveOptions
    {
        ExportImagesAsBase64 = true,
        ExportChartImageFormat = ImageFormat.Png,
        ExportPrintingHeadersFooters = false,
        IsResponsive = true,
        HtmlVersion = HtmlVersion.Html5,
        ImageResolution = 150 // reasonable default DPI
    };

    // Force recalculation for up‑to‑date charts
    wb.CalculateFormula();

    // Save as HTML
    wb.Save(htmlPath, opts);
}
```

Τώρα μπορείτε να καλέσετε `ConvertExcelToHtmlWithPngCharts(@"C:\Reports\MyFile.xlsx", @"C:\Reports\MyFile.html");` από οπουδήποτε στον κώδικά σας.

---

## Συμπέρασμα

Μόλις κατακτήσατε πώς να **εξάγετε διάγραμμα ως PNG** ενώ **μετατρέπετε Excel σε HTML**, **ενσωματώνετε εικόνες ως Base64**, και **αποθηκεύετε βιβλίο εργασίας ως HTML** χρησιμοποιώντας το Aspose.Cells. Το βασικό συμπέρασμα είναι ότι μερικές καλά επιλεγμένες ρυθμίσεις του `HtmlSaveOptions` σας δίνουν ένα ενιαίο, αυτόνομο αρχείο HTML που λειτουργεί σε οποιαδήποτε συσκευή—χωρίς επιπλέον αρχεία PNG, χωρίς ακατάστατους φακέλους.

Έτοιμοι για την επόμενη πρόκληση; Δοκιμάστε να συνδυάσετε αυτήν την προσέγγιση με **εξαγωγή διαγράμματος Excel σε PNG** για δημιουργία PDF, ή πειραματιστείτε με προσαρμοσμένο CSS για περαιτέρω στυλιζάρισμα των πινάκων. Ο ουρανός είναι το όριο όταν ελέγχετε τόσο τα δεδομένα όσο και την παρουσίαση προγραμματιστικά.

Μη διστάσετε να αφήσετε ένα σχόλιο αν αντιμετωπίσετε δυσκολίες, ή να μοιραστείτε πώς προσαρμόσατε αυτό το μοτίβο στα δικά σας έργα. Καλή προγραμματιστική!

## Τι Θα Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κυριαρχήσετε επιπλέον δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στην υλοποίηση.

- [Export Excel to HTML Using Aspose.Cells for .NET: A Complete Guide](/cells/english/net/workbook-operations/export-excel-html-aspose-cells-net/)  
- [Export Excel to HTML Without Frame Scripts Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/export-excel-to-html-aspose-cells-net/)  
- [How to Export an Excel Worksheet to PNG Using Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}