---
category: general
date: 2026-07-14
description: Αποθηκεύστε το Excel ως HTML γρήγορα και μάθετε πώς να μετατρέψετε το
  Excel σε HTML με πλήρη μορφοποίηση. Εξάγετε το Excel με μορφοποίηση χρησιμοποιώντας
  το Aspose.Cells σε λίγα λεπτά.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save excel as html
- convert excel to html
- export excel with formatting
- Aspose.Cells HTML export
- Grid.js number formatting
language: el
lastmod: 2026-07-14
og_description: Αποθηκεύστε το Excel ως HTML άμεσα. Αυτός ο οδηγός δείχνει πώς να
  μετατρέψετε το Excel σε HTML διατηρώντας τα στυλ και ενεργοποιώντας τη μορφοποίηση
  αριθμών του Grid.js.
og_image_alt: Screenshot of a spreadsheet saved as HTML using Aspose.Cells – save
  excel as html example
og_title: Αποθήκευση Excel ως HTML – Εξαγωγή βήμα‑βήμα με πλήρη μορφοποίηση
schemas:
- author: Aspose
  dateModified: '2026-07-14'
  description: Save Excel as HTML quickly and learn how to convert Excel to HTML with
    full formatting. Export Excel with formatting using Aspose.Cells in minutes.
  headline: Save Excel as HTML – Complete Guide to Export Excel with Formatting
  type: TechArticle
- description: Save Excel as HTML quickly and learn how to convert Excel to HTML with
    full formatting. Export Excel with formatting using Aspose.Cells in minutes.
  name: Save Excel as HTML – Complete Guide to Export Excel with Formatting
  steps:
  - name: '**Styling intact?** Compare cell background colors and borders to the original
      Excel view.'
    text: '**Styling intact?** Compare cell background colors and borders to the original
      Excel view.'
  - name: '**Number formats preserved?** Look for the `data-format` attribute on `<td>`
      elements.'
    text: '**Number formats preserved?** Look for the `data-format` attribute on `<td>`
      elements.'
  - name: '**Images displayed?** If you exported images as Base64, they should appear
      inline.'
    text: '**Images displayed?** If you exported images as Base64, they should appear
      inline.'
  - name: '**Browser console clean?** No JavaScript errors related to Grid.js.'
    text: '**Browser console clean?** No JavaScript errors related to Grid.js.'
  type: HowTo
tags:
- Excel
- HTML
- Aspose.Cells
title: Αποθήκευση του Excel ως HTML – Πλήρης Οδηγός για Εξαγωγή του Excel με Μορφοποίηση
url: /el/net/exporting-excel-to-html-with-advanced-options/save-excel-as-html-complete-guide-to-export-excel-with-forma/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Αποθήκευση Excel ως HTML – Πλήρης Οδηγός για Εξαγωγή Excel με Μορφοποίηση

Έχετε αναρωτηθεί ποτέ πώς να **αποθηκεύσετε το Excel ως HTML** χωρίς να χάσετε τα χρώματα, τα περιγράμματα ή τις μορφές αριθμών; Δεν είστε ο μόνος. Σε πολλές περιπτώσεις αναφοράς χρειάζεστε μια έτοιμη για web προβολή ενός βιβλίου εργασίας, και ο πιο γρήγορος τρόπος είναι να εξάγετε το αρχείο απευθείας σε HTML.  

Σε αυτόν τον οδηγό θα περάσουμε βήμα προς βήμα τις ακριβείς ενέργειες για **μετατροπή του Excel σε HTML** χρησιμοποιώντας το Aspose.Cells, ενεργοποίηση της μορφοποίησης αριθμών του Grid.js, και διασφάλιση ότι το αποτέλεσμα φαίνεται ακριβώς όπως το αρχικό φύλλο εργασίας. Στο τέλος θα έχετε ένα έτοιμο αρχείο HTML που μπορείτε να σερβίρετε από οποιονδήποτε web server.

## Τι Θα Μάθετε

- Προαπαιτούμενα και εγκατάσταση πακέτου  
- Φόρτωση υπάρχοντος βιβλίου εργασίας (ή δημιουργία εν κινήσει)  
- Διαμόρφωση του `HtmlSaveOptions` για τέλεια οπτική πιστότητα  
- Ενεργοποίηση του `GridJsOptions.EnableNumberFormat` για διατήρηση του στυλ αριθμών  
- Αποθήκευση του αρχείου και επαλήθευση του αποτελέσματος  

Αν έχετε προσπαθήσει ποτέ να **εξάγετε το Excel με μορφοποίηση** χρησιμοποιώντας μια γενική εξαγωγή CSV, ξέρετε πόσο απογοητευτικό μπορεί να είναι όταν οι αριθμοί μετατρέπονται σε απλό κείμενο. Αυτός ο οδηγός αποφεύγει αυτό το πρόβλημα.

---

## Προαπαιτούμενα – Ρύθμιση του Περιβάλλοντος Ανάπτυξης

Πριν βουτήξουμε στον κώδικα, βεβαιωθείτε ότι έχετε:

| Requirement | Why it matters |
|-------------|----------------|
| .NET 6.0 or later (the tutorial uses .NET 6) | Σύγχρονα API και καλύτερη απόδοση |
| Visual Studio 2022 (or VS Code with C# extension) | Άνετη επεξεργασία και αποσφαλμάτωση |
| Aspose.Cells for .NET NuGet package | Η βιβλιοθήκη που παρέχει λειτουργίες στο `HtmlSaveOptions` και `GridJsOptions` |
| A sample Excel file (`sample.xlsx`) or a workbook you generate in code | Η πηγή που θα μετατρέψετε |

Εγκαταστήστε το Aspose.Cells με την ακόλουθη εντολή στην Κονσόλα Διαχειριστή Πακέτων:

```powershell
Install-Package Aspose.Cells
```

> **Συμβουλή:** Αν βρίσκεστε σε CI pipeline, προσθέστε την ίδια γραμμή `dotnet add package` στο script κατασκευής ώστε η εξάρτηση να είναι πάντα παρούσα.

---

## Βήμα 1: Φόρτωση ή Δημιουργία Βιβλίου Εργασίας

Μπορείτε είτε να φορτώσετε ένα υπάρχον αρχείο είτε να δημιουργήσετε ένα προγραμματιστικά. Ακολουθεί ένα ελάχιστο παράδειγμα που δημιουργεί ένα βιβλίο εργασίας με μερικά μορφοποιημένα κελιά ώστε να δείτε τη μορφοποίηση να διατηρείται κατά την εξαγωγή.

```csharp
using Aspose.Cells;
using System.Drawing;

// Create a new workbook
Workbook wb = new Workbook();
Worksheet sheet = wb.Worksheets[0];
sheet.Name = "Report";

// Populate some data
sheet.Cells["A1"].PutValue("Product");
sheet.Cells["B1"].PutValue("Price");
sheet.Cells["A2"].PutValue("Widget");
sheet.Cells["B2"].PutValue(19.99);
sheet.Cells["A3"].PutValue("Gadget");
sheet.Cells["B3"].PutValue(42.5);

// Apply basic styling
Style headerStyle = wb.CreateStyle();
headerStyle.Font.IsBold = true;
headerStyle.ForegroundColor = Color.LightGray;
headerStyle.Pattern = BackgroundType.Solid;
sheet.Cells["A1:B1"].SetStyle(headerStyle);

// Format the price column as currency
Style priceStyle = wb.CreateStyle();
priceStyle.Number = 164; // Built‑in currency format
sheet.Cells["B2:B3"].SetStyle(priceStyle);
```

> **Γιατί είναι σημαντικό:** Ορίζοντας ρητά τις μορφές αριθμών, θα δείτε αργότερα το `GridJsOptions.EnableNumberFormat` να διατηρεί αυτές τις μορφές ζωντανές στο HTML αποτέλεσμα.

---

## Βήμα 2: Διαμόρφωση Επιλογών Αποθήκευσης HTML

Τώρα δημιουργούμε μια παρουσία του `HtmlSaveOptions`. Αυτό το αντικείμενο λέει στο Aspose.Cells ακριβώς πώς θέλετε να αποδοθεί το HTML.

```csharp
// Step 2: Create HTML save options
HtmlSaveOptions htmlOptions = new HtmlSaveOptions
{
    // Export the entire workbook as a single HTML page
    ExportActiveWorksheetOnly = false,

    // Keep the original cell styles (fonts, colors, borders)
    ExportGridLines = true,
    ExportColumnHeaders = true,
    ExportRowHeaders = true
};
```

### Ενεργοποίηση Μορφοποίησης Αριθμών Grid.js

Αν σκοπεύετε να ενσωματώσετε το HTML σε μια σελίδα που χρησιμοποιεί το **Grid.js** για διαδραστικούς πίνακες, θα θέλετε οι αριθμοί να παραμείνουν μορφοποιημένοι (π.χ., σύμβολα νομισμάτων, διαχωριστικά χιλιάδων). Η παρακάτω γραμμή κάνει ακριβώς αυτό:

```csharp
// Step 3: Enable number formatting for Grid.js tables
htmlOptions.GridJsOptions = new GridJsOptions { EnableNumberFormat = true };
```

> **Τι συμβαίνει στο παρασκήνιο;** Το `EnableNumberFormat` ενσωματώνει ένα μικρό απόσπασμα JavaScript που λέει στο Grid.js να ερμηνεύσει το χαρακτηριστικό `data-format` του κελιού, διατηρώντας τη μορφοποίηση τύπου Excel στο πρόγραμμα περιήγησης.

---

## Βήμα 3: Αποθήκευση του Βιβλίου Εργασίας ως Αρχείο HTML

Με το βιβλίο εργασίας έτοιμο και τις επιλογές ρυθμισμένες, η τελική γραμμή γράφει το αρχείο HTML στο δίσκο.

```csharp
// Step 4: Save the workbook as an HTML file with the configured options
string outputPath = @"C:\Temp\gridjs.html";
wb.Save(outputPath, htmlOptions);
Console.WriteLine($"Workbook successfully saved as HTML to: {outputPath}");
```

Η εκτέλεση του προγράμματος παράγει ένα αρχείο `gridjs.html` που φαίνεται ως εξής (απλοποιημένη προβολή):

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />
    <title>Report</title>
    <link rel="stylesheet" href="gridjs.css" />
    <script src="gridjs.js"></script>
</head>
<body>
    <table class="gridjs-table">
        <thead>
            <tr><th>Product</th><th>Price</th></tr>
        </thead>
        <tbody>
            <tr><td>Widget</td><td data-format="$#,##0.00">19.99</td></tr>
            <tr><td>Gadget</td><td data-format="$#,##0.00">42.5</td></tr>
        </tbody>
    </table>
</body>
</html>
```

Ανοίξτε το αρχείο σε οποιονδήποτε περιηγητή και θα δείτε έναν ωραία μορφοποιημένο πίνακα, με φόντο κεφαλίδας ανοιχτό-γκρι και μορφοποίηση νομισμάτων. Αν ενσωματώσετε τη σελίδα σε έναν ιστότοπο που ήδη φορτώνει το Grid.js, οι αριθμοί θα αποδοθούν αυτόματα με τα σωστά κόμματα και σύμβολα.

---

## Συνηθισμένα Πιθανά Προβλήματα Όταν **Μετατρέπετε το Excel σε HTML**

| Issue | Why it occurs | How to avoid it |
|-------|---------------|-----------------|
| **Lost formulas** | Το HTML είναι στατικό· οι τύποι γίνονται απλές τιμές. | Αν χρειάζεστε ζωντανές υπολογιστικές λειτουργίες, διατηρήστε το βιβλίο εργασίας στον διακομιστή και χρησιμοποιήστε βιβλιοθήκες JavaScript όπως το SheetJS. |
| **Missing images** | Οι εικόνες αποθηκεύονται ως ξεχωριστοί πόροι. | Ορίστε `HtmlSaveOptions.ExportImagesAsBase64 = true` για ενσωμάτωση τους απευθείας. |
| **Huge files** | Μεγάλα βιβλία εργασίας παράγουν τεράστιο HTML + JS. | Χρησιμοποιήστε `ExportOnlyVisibleSheets` ή χωρίστε σε πολλαπλές σελίδες μέσω `HtmlSaveOptions.OnePagePerSheet`. |
| **Incorrect number locale** | Το Excel αποθηκεύει αριθμούς σε αμετάβλητο πολιτισμικό περιβάλλον, οι περιηγητές μπορεί να εφαρμόσουν τοπικές ρυθμίσεις. | Ορίστε ρητά `htmlOptions.Encoding = Encoding.UTF8` και χρησιμοποιήστε `GridJsOptions.EnableNumberFormat`. |

---

## Προχωρημένο: Εξαγωγή Πολλαπλών Φύλλων με Ατομικές Στιγμιότυπες Grid.js

Αν το βιβλίο εργασίας σας περιέχει πολλά φύλλα και θέλετε το καθένα να γίνει ο δικός του πίνακας Grid.js, μπορείτε να κάνετε βρόχο στα worksheets και να αποθηκεύσετε το καθένα ξεχωριστά:

```csharp
for (int i = 0; i < wb.Worksheets.Count; i++)
{
    Worksheet ws = wb.Worksheets[i];
    HtmlSaveOptions opt = new HtmlSaveOptions
    {
        ExportActiveWorksheetOnly = true,
        GridJsOptions = new GridJsOptions { EnableNumberFormat = true }
    };
    string sheetPath = $@"C:\Temp\{ws.Name}.html";
    wb.Save(sheetPath, opt);
    Console.WriteLine($"Saved {ws.Name} to {sheetPath}");
}
```

Κάθε αρχείο θα περιέχει το δικό του στοιχείο `<table class="gridjs-table">`, έτοιμο για ανεξάρτητη επεξεργασία.

---

## Επαλήθευση του Αποτελέσματος – Γρήγορη Λίστα Ελέγχου

1. **Διατήρηση στυλ;** Συγκρίνετε τα χρώματα φόντου των κελιών και τα περιγράμματα με την αρχική προβολή του Excel.  
2. **Διατήρηση μορφών αριθμών;** Αναζητήστε το χαρακτηριστικό `data-format` στα στοιχεία `<td>`.  
3. **Εμφάνιση εικόνων;** Αν εξάγατε τις εικόνες ως Base64, θα πρέπει να εμφανίζονται ενσωματωμένες.  
4. **Καθαρή κονσόλα περιηγητή;** Χωρίς σφάλματα JavaScript που σχετίζονται με το Grid.js.  

Αν κάποιος από αυτούς τους ελέγχους αποτύχει, επανεξετάστε την αντίστοιχη ιδιότητα `HtmlSaveOptions`—τα περισσότερα προβλήματα προέρχονται από μια ελλιπή σημαία.

---

## Συμπέρασμα

Τώρα έχετε μια αξιόπιστη, έτοιμη για παραγωγή μέθοδο να **αποθηκεύσετε το Excel ως HTML** διατηρώντας κάθε στυλ, περίγραμμα και αριθμητική αναπαράσταση αμετάβλητη. Διαμορφώνοντας το `HtmlSaveOptions` και ενεργοποιώντας το `GridJsOptions.EnableNumberFormat`, μετατρέψατε ένα στατικό φύλλο εργασίας σε έναν φιλικό προς το web πίνακα που λειτουργεί άψογα με το Grid.js.

Συνοπτικά, αυτός ο οδηγός σας δείχνει πώς να **μετατρέψετε το Excel σε HTML** και να **εξάγετε το Excel με μορφοποίηση** χρησιμοποιώντας το Aspose.Cells. Μη διστάσετε να πειραματιστείτε: δοκιμάστε διαφορετικά θέματα, ενσωματώστε γραφήματα ή ακόμη και σερβίρετε το HTML μέσω ενός endpoint ASP.NET για μετατροπή εν κινήσει.

Αν αντιμετωπίσετε προβλήματα, αφήστε ένα σχόλιο παρακάτω ή ελέγξτε την τεκμηρίωση του Aspose.Cells για πιο προχωρημένες επιλογές διαμόρφωσης. Καλή προγραμματιστική!

## Τι Ακολουθεί;

- **Εξερευνήστε άλλες μορφές εξαγωγής**: PDF, PNG ή CSV μέσω `Workbook.Save`.  
- **Ενσωματώστε με ASP.NET Core**: Επιστρέψτε το HTML string απευθείας από μια ενέργεια ελεγκτή.  
- **Συνδυάστε με SheetJS**: Φορτώστε το παραγόμενο HTML ξανά σε ένα JavaScript βιβλίο εργασίας για επεξεργασία στην πλευρά του πελάτη.  

## Τι Θα Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που βασίζονται στις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να Εξάγετε το Excel σε HTML με Γραμμές Πλέγματος Χρησιμοποιώντας το Aspose.Cells για .NET](/cells/english/net/workbook-operations/export-excel-to-html-grid-lines-aspose-cells-net/)
- [Εξαγωγή Excel σε HTML Διατηρώντας τα Στυλ Περιγραμμάτων Χρησιμοποιώντας το Aspose.Cells για Java](/cells/english/java/workbook-operations/aspose-cells-java-export-excel-html-border-styles/)
- [Μετατροπή HTML σε Excel Χρησιμοποιώντας το Aspose.Cells .NET: Ένας Πλήρης Οδηγός](/cells/english/net/workbook-operations/convert-html-to-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}