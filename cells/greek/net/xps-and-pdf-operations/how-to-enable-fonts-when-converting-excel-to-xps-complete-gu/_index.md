---
category: general
date: 2026-07-03
description: Πώς να ενεργοποιήσετε τις γραμματοσειρές κατά τη μετατροπή του Excel
  σε XPS χρησιμοποιώντας το Aspose.Cells. Μάθετε βήμα‑βήμα τη ρύθμιση, τον κώδικα
  και συμβουλές για άψογη διατήρηση των γραμματοσειρών.
draft: false
keywords:
- how to enable fonts
- convert excel to xps
- Aspose.Cells XPS export
- preserve font variations
- C# Excel automation
language: el
og_description: Πώς να ενεργοποιήσετε τις γραμματοσειρές στη μετατροπή Excel‑σε‑XPS.
  Ακολουθήστε αυτόν τον οδηγό για ένα λειτουργικό παράδειγμα C# που διατηρεί αμετάβλητες
  τις παραλλαγές των γραμματοσειρών.
og_title: Πώς να ενεργοποιήσετε τις γραμματοσειρές κατά τη μετατροπή του Excel σε
  XPS – Πλήρης οδηγός
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: How to enable fonts while you convert Excel to XPS using Aspose.Cells.
    Learn step‑by‑step setup, code, and tips for flawless font preservation.
  headline: How to Enable Fonts When Converting Excel to XPS – Complete Guide
  type: TechArticle
- description: How to enable fonts while you convert Excel to XPS using Aspose.Cells.
    Learn step‑by‑step setup, code, and tips for flawless font preservation.
  name: How to Enable Fonts When Converting Excel to XPS – Complete Guide
  steps:
  - name: What Does `FontVariationSelectors = true` Actually Do?
    text: '- **Preserves custom weight & style variations** (e.g., a font that supports
      multiple thicknesses via OpenType features). - **Ensures the XPS viewer renders
      the exact glyphs** you see in Excel, rather than falling back to a generic font.
      - **Adds a small overhead** to the file size because the selec'
  - name: Expected Result
    text: '- The file `WithSelectors.xps` will appear in the target folder. - Open
      it in any XPS viewer (e.g., Windows XPS Viewer or Edge). - You should see the
      same font weights, italics, and any custom OpenType variations that were present
      in the original Excel file.'
  - name: Next Steps
    text: '- Experiment with other `XpsSaveOptions` properties like `Compress` or
      `EmbedStandardFonts`. - Try converting to PDF first, then to XPS, to compare
      file sizes and fidelity. - Dive into Aspose.Cells’ **image handling** (`ImageOrPrintOptions`)
      if your workbook contains charts or pictures you also need'
  type: HowTo
tags:
- Aspose.Cells
- C#
- XPS
- Excel
title: Πώς να ενεργοποιήσετε τις γραμματοσειρές κατά τη μετατροπή του Excel σε XPS
  – Πλήρης οδηγός
url: /el/net/xps-and-pdf-operations/how-to-enable-fonts-when-converting-excel-to-xps-complete-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Ενεργοποιήσετε τις Γραμματοσειρές Κατά τη Μετατροπή του Excel σε XPS – Πλήρης Οδηγός

Έχετε αναρωτηθεί ποτέ **πώς να ενεργοποιήσετε τις γραμματοσειρές** ώστε η μετατροπή σας από Excel σε XPS να φαίνεται ακριβώς όπως το αρχικό βιβλίο εργασίας; Δεν είστε ο μόνος. Πολλοί προγραμματιστές αντιμετωπίζουν πρόβλημα όταν το παραγόμενο αρχείο XPS χάνει τις προσαρμοσμένες παραλλαγές γραμματοσειρών, αφήνοντας το έγγραφο να φαίνεται αφηρημένο.  

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα μια πρακτική λύση που όχι μόνο δείχνει **πώς να ενεργοποιήσετε τις γραμματοσειρές**, αλλά επίσης παρουσιάζει τον καλύτερο τρόπο για **να μετατρέψετε το Excel σε XPS** χρησιμοποιώντας το Aspose.Cells. Στο τέλος θα έχετε ένα έτοιμο προς εκτέλεση απόσπασμα C#, μια σαφή εξήγηση κάθε ρύθμισης, και μερικές επαγγελματικές συμβουλές για να διατηρήσετε το αποτέλεσμα XPS pixel‑perfect.

## Τι Θα Χρειαστείτε

- **Aspose.Cells for .NET** (latest version as of 2026‑07).  
- Ένα περιβάλλον ανάπτυξης .NET (Visual Studio 2022 ή VS Code με την επέκταση C# λειτουργεί καλά).  
- Ένα βιβλίο εργασίας Excel (`VariationFont.xlsx`) που περιέχει επιλογείς παραλλαγής γραμματοσειρών που θέλετε να διατηρήσετε.  

Αυτό είναι όλο—χωρίς επιπλέον πακέτα NuGet, χωρίς πολύπλοκο COM interop, απλώς απλό C#.

![Diagram showing the flow from Excel workbook to XPS document – how to enable fonts during conversion](https://example.com/images/enable-fonts-xps.png "how to enable fonts in Excel to XPS conversion")

## Βήμα 1: Ρύθμιση του Έργου και Εισαγωγή Ονομάτων Χώρων

Πρώτα, δημιουργήστε μια νέα εφαρμογή console (ή ενσωματώστε την σε υπάρχουσα λύση). Προσθέστε την αναφορά Aspose.Cells μέσω NuGet:

```bash
dotnet add package Aspose.Cells
```

Στη συνέχεια, φέρτε τα απαραίτητα ονόματα χώρων στο πεδίο ορατότητας:

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;   // optional, for advanced graphics handling
```

> **Συμβουλή επαγγελματία:** Εάν στοχεύετε σε .NET 6+, μπορείτε να χρησιμοποιήσετε τη ρητή λειτουργία `global using` για να διατηρήσετε τα αρχεία σας τακτοποιημένα.

## Βήμα 2: Φόρτωση του Βιβλίου Εργασίας Excel

Η φόρτωση του βιβλίου εργασίας είναι η βάση· χωρίς μια σωστή παρουσία `Workbook` δεν μπορείτε να ρυθμίσετε καμία επιλογή αποθήκευσης.

```csharp
// Step 2: Load the Excel workbook you want to convert
Workbook workbook = new Workbook("YOUR_DIRECTORY/VariationFont.xlsx");

// Quick sanity check – make sure at least one worksheet is present
if (workbook.Worksheets.Count == 0)
{
    throw new InvalidOperationException("The workbook contains no worksheets.");
}
```

> **Γιατί είναι σημαντικό:** Όταν αργότερα ενεργοποιήσετε τους επιλογείς παραλλαγής γραμματοσειρών, το Aspose.Cells χρειάζεται ένα πλήρως αρχικοποιημένο βιβλίο εργασίας· διαφορετικά η επιλογή αγνοείται σιωπηρά.

## Βήμα 3: Δημιουργία και Διαμόρφωση των Επιλογών Αποθήκευσης XPS – Εδώ **Ενεργοποιείτε τις Γραμματοσειρές**

Η καρδιά του tutorial βρίσκεται σε αυτό το βήμα. Από προεπιλογή, το Aspose.Cells αφαιρεί τους επιλογείς παραλλαγής γραμματοσειρών για να διατηρήσει το μέγεθος του αρχείου XPS μικρό. Για να τους διατηρήσετε, ορίστε το `FontVariationSelectors` σε `true`.

```csharp
// Step 3: Create XPS save options and enable font variation selectors
XpsSaveOptions xpsOptions = new XpsSaveOptions
{
    // This flag tells Aspose.Cells to keep any OpenType font variation selectors
    FontVariationSelectors = true,

    // Optional: keep the original DPI for sharper rendering (default is 96)
    Dpi = 300
};
```

### Τι Κάνει Πραγματικά το `FontVariationSelectors = true`;

- **Διατηρεί προσαρμοσμένες παραλλαγές βάρους & στυλ** (π.χ., μια γραμματοσειρά που υποστηρίζει πολλαπλά πάχη μέσω λειτουργιών OpenType).  
- **Εξασφαλίζει ότι ο προβολέας XPS αποδίδει τα ακριβή γλύφους** που βλέπετε στο Excel, αντί να επιστρέφει σε μια γενική γραμματοσειρά.  
- **Προσθέτει μια μικρή επιπλέον φόρτωση** στο μέγεθος του αρχείου επειδή τα δεδομένα επιλογέα αποθηκεύονται μέσα στο πακέτο XPS.  

Αν ποτέ χρειαστείτε να **μετατρέψετε το Excel σε XPS** χωρίς να διατηρήσετε αυτούς τους επιλογείς, απλώς ορίστε την ιδιότητα σε `false` (ή παραλείψτε την, καθώς το `false` είναι η προεπιλογή).

## Βήμα 4: Αποθήκευση του Βιβλίου Εργασίας ως XPS Χρησιμοποιώντας τις Διαμορφωμένες Επιλογές

Τώρα που οι επιλογές είναι έτοιμες, καλέστε το `Save` με το enum `SaveFormat.Xps` και περάστε το αντικείμενο επιλογών.

```csharp
// Step 4: Save the workbook as an XPS document with the font‑preserving options
string outputPath = "YOUR_DIRECTORY/WithSelectors.xps";
workbook.Save(outputPath, SaveFormat.Xps, xpsOptions);

Console.WriteLine($"Workbook successfully saved to XPS at: {outputPath}");
```

### Αναμενόμενο Αποτέλεσμα

- Το αρχείο `WithSelectors.xps` θα εμφανιστεί στον φάκελο προορισμού.  
- Ανοίξτε το σε οποιονδήποτε προβολέα XPS (π.χ., Windows XPS Viewer ή Edge).  
- Θα πρέπει να δείτε τα ίδια βάρη γραμματοσειρών, πλάγια και τυχόν προσαρμοσμένες παραλλαγές OpenType που υπήρχαν στο αρχικό αρχείο Excel.  

Αν οι γραμματοσειρές φαίνονται διαφορετικές, ελέγξτε ξανά ότι το πηγαίο Excel χρησιμοποιεί πράγματι μια γραμματοσειρά με επιλογείς παραλλαγής και ότι ο προβολέας που χρησιμοποιείτε τα υποστηρίζει.

## Συνηθισμένα Παράπτωμα & Πώς να τα Αποφύγετε

| Συμπτωμα | Πιθανή Αιτία | Διόρθωση |
|---------|--------------|----------|
| Το κείμενο εμφανίζεται σε γενική γραμματοσειρά εφεδρείας | `FontVariationSelectors` άφησε στην προεπιλογή (`false`) | Ορίστε `xpsOptions.FontVariationSelectors = true`. |
| Το μέγεθος του αρχείου XPS αυξάνεται απροσδόκητα | Ρύθμιση υψηλής DPI σε συνδυασμό με επιλογείς γραμματοσειρών | Μειώστε το `Dpi` σε 150 ή 96 αν το μέγεθος είναι πιο σημαντικό από την πιστότητα. |
| Εξαίρεση “File not found” κατά τη δημιουργία του `Workbook` | Λάθος διαδρομή ή λείπει το αρχείο | Χρησιμοποιήστε απόλυτη διαδρομή ή `Path.Combine(Environment.CurrentDirectory, "VariationFont.xlsx")`. |

## Βήμα 5: Επαλήθευση της Μετατροπής (Προαιρετικό Αυτόματο Τεστ)

Εάν αυτοματοποιείτε τις κατασκευές, ίσως θέλετε να ελέγξετε ότι το αρχείο XPS υπάρχει και δεν είναι κενό:

```csharp
if (!System.IO.File.Exists(outputPath) || new System.IO.FileInfo(outputPath).Length == 0)
{
    throw new Exception("XPS conversion failed – file is missing or empty.");
}
```

Η εκτέλεση αυτού του ελέγχου ως μέρος μιας CI pipeline εγγυάται ότι **πώς να ενεργοποιήσετε τις γραμματοσειρές** λειτουργεί κάθε φορά που σπρώχνετε κώδικα.

## Συμπεράσματα: Τι Καλύψαμε

- **Πώς να ενεργοποιήσετε τις γραμματοσειρές** κατά τη μετατροπή Excel‑σε‑XPS ενεργοποιώντας το `FontVariationSelectors`.  
- Το πλήρες απόσπασμα C# που φορτώνει ένα βιβλίο εργασίας, διαμορφώνει το `XpsSaveOptions` και αποθηκεύει το αποτέλεσμα.  
- Συμβουλές για την αντιμετώπιση προβλημάτων και την επαλήθευση του τελικού εγγράφου.  

Τώρα μπορείτε με σιγουριά να **μετατρέψετε το Excel σε XPS** διατηρώντας κάθε τυπογραφική λεπτομέρεια αμετάβλητη.  

### Επόμενα Βήματα

- Δοκιμάστε άλλες ιδιότητες του `XpsSaveOptions` όπως `Compress` ή `EmbedStandardFonts`.  
- Δοκιμάστε να μετατρέψετε πρώτα σε PDF, μετά σε XPS, για να συγκρίνετε τα μεγέθη αρχείων και την πιστότητα.  
- Εμβαθύνετε στη **διαχείριση εικόνων** του Aspose.Cells (`ImageOrPrintOptions`) εάν το βιβλίο εργασίας σας περιέχει γραφήματα ή εικόνες που επίσης χρειάζεται να διατηρήσετε.  

Έχετε ερωτήσεις για πιο προχωρημένα σενάρια—όπως η ενσωμάτωση προσαρμοσμένων γραμματοσειρών που δεν είναι εγκατεστημένες στον προορισμό; Αφήστε ένα σχόλιο παρακάτω, και καλή προγραμματιστική!

## Τι Θα Πρέπει Να Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε σε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να Ορίσετε Στυλ Γραμματοσειρών στο Excel Χρησιμοποιώντας Aspose.Cells για .NET (Βήμα‑Βήμα Οδηγός)](/cells/english/net/formatting/aspose-cells-dotnet-set-font-styles-excel/)
- [Πώς να Εξάγετε Γραμματοσειρές από Αρχεία Excel Χρησιμοποιώντας Aspose.Cells για .NET](/cells/english/net/formatting/extract-fonts-excel-aspose-cells-dotnet-guide/)
- [Πώς να Μετατρέψετε Φύλλα Excel σε Εικόνες Χρησιμοποιώντας Aspose.Cells .NET (Βήμα‑Βήμα Οδηγός)](/cells/english/net/workbook-operations/convert-excel-sheets-images-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}