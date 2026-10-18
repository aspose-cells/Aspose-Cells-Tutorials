---
category: general
date: 2026-06-05
description: Πώς να εξάγετε διαγράμματα από το PowerPoint χρησιμοποιώντας C#. Περιλαμβάνει
  εξαγωγή αντικειμένων OLE και κάνει τα διαγράμματα επεξεργάσιμα στο παραγόμενο PPTX
  – βήμα προς βήμα.
draft: false
keywords:
- how to export charts
- export ole objects
- how to export ole
- make charts editable
language: el
og_description: Πώς να εξάγετε διαγράμματα από το PowerPoint χρησιμοποιώντας C#. Μάθετε
  πώς να εξάγετε αντικείμενα OLE και να κάνετε τα διαγράμματα επεξεργάσιμα στο αποθηκευμένο
  PPTX – βήμα‑βήμα.
og_title: Πώς να εξάγετε διαγράμματα – Πλήρης οδηγός PowerPoint C#
schemas:
- author: Aspose
  dateModified: '2026-06-05'
  description: How to export charts from PowerPoint using C#. Includes export OLE
    objects and make charts editable in the resulting PPTX – step‑by‑step.
  headline: How to Export Charts – Complete PowerPoint C# Guide
  type: TechArticle
- description: How to export charts from PowerPoint using C#. Includes export OLE
    objects and make charts editable in the resulting PPTX – step‑by‑step.
  name: How to Export Charts – Complete PowerPoint C# Guide
  steps:
  - name: Full Working Example
    text: Below is the complete, self‑contained program you can compile and run. It
      includes `using` statements, proper disposal, and comments that explain each
      line.
  - name: What if the source file has no charts?
    text: The code will still run; `ExportEditableCharts` simply has no effect because
      there’s nothing to convert. No error is thrown.
  - name: Can I export only specific charts?
    text: Yes. Instead of using the global `ExportEditableCharts` flag, you can iterate
      through `presentation.Slides` and set `Chart.IsEditable = true` on individual
      chart objects before saving. This gives you granular control.
  - name: Does enabling OLE export increase file size?
    text: A little. The binary OLE streams are stored verbatim, so the resulting PPTX
      can be a few kilobytes larger. In most business scenarios the trade‑off is worth
      it because you retain full editability.
  - name: Which PowerPoint versions can open the resulting file?
    text: Any version that supports the OOXML standard (PowerPoint 2007 and later).
      The editable chart feature relies on the native chart editor introduced in Office
      2007, so older binaries like `.ppt` won’t benefit.
  type: HowTo
tags:
- PowerPoint
- C#
- Aspose.Slides
- OLE
- Charts
title: Πώς να Εξάγετε Διαγράμματα – Πλήρης Οδηγός PowerPoint C#
url: /el/net/chart-rendering-and-conversion/how-to-export-charts-complete-powerpoint-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Εξάγετε Διαγράμματα – Πλήρης Οδηγός PowerPoint C#

Έχετε αναρωτηθεί ποτέ **πώς να εξάγετε διαγράμματα** από μια παρουσίαση PowerPoint χωρίς να χάσετε τη δυνατότητα επεξεργασίας τους αργότερα; Δεν είστε οι μόνοι. Σε πολλές αλυσίδες αναφοράς τα δεδομένα του διαγράμματος βρίσκονται μέσα στο PPTX και, μόλις παραδώσετε το αρχείο, ο παραλήπτης συχνά χρειάζεται να προσαρμόσει μια τιμή ή να αλλάξει μια ετικέτα. Τα καλά νέα είναι ότι με μερικές γραμμές C# μπορείτε να διατηρήσετε την επεξεργασιμότητα και ακόμη και να εξάγετε ενσωματωμένα αντικείμενα OLE ταυτόχρονα.

Σε αυτό το tutorial θα περάσουμε από ένα πρακτικό, έτοιμο‑για‑εκτέλεση παράδειγμα που δείχνει **πώς να εξάγετε διαγράμματα**, **πώς να εξάγετε αντικείμενα OLE**, και **πώς να κάνετε τα διαγράμματα επεξεργάσιμα** στο αρχείο εξόδου. Στο τέλος θα έχετε ένα επαναχρησιμοποιήσιμο snippet που μπορείτε να ενσωματώσετε σε οποιοδήποτε .NET project που χρησιμοποιεί τη βιβλιοθήκη Aspose.Slides.

> **Pro tip:** Αν είστε νέοι στο Aspose.Slides, βεβαιωθείτε ότι έχετε προσθέσει το NuGet package `Aspose.Slides.NET` στο project σας—διαφορετικά ο κώδικας δεν θα μεταγλωττιστεί.

## Τι Θα Χρειαστείτε

| Απαίτηση | Γιατί είναι σημαντική |
|----------|------------------------|
| .NET 6+ (ή .NET Framework 4.7+) | Τα σύγχρονα runtime προσφέρουν καλύτερη απόδοση και πιο εύκολη διαχείριση πακέτων. |
| Aspose.Slides for .NET (τελευταία έκδοση) | Αυτή η βιβλιοθήκη παρέχει τις κλάσεις `Presentation` και `PptxSaveOptions` που θα χρησιμοποιήσουμε. |
| Ένα δείγμα αρχείου PowerPoint με τουλάχιστον ένα διάγραμμα | Η demo λειτουργεί με οποιοδήποτε `.pptx` που περιέχει διάγραμμα· θα δείτε την επεξεργασιμότητα μετά την εξαγωγή. |
| Ένα IDE (Visual Studio, Rider ή VS Code) | Χρήσιμο για γρήγορο debugging και για να δείτε το παραγόμενο αρχείο. |

Δεν απαιτούνται πρόσθετα εργαλεία τρίτων—όλα διαχειρίζονται από το Aspose API.

## Βήμα 1 – Φόρτωση της Πηγαίας Παρουσίασης

Πρώτα πρέπει να φέρουμε το αρχικό PPTX στη μνήμη. Σκεφτείτε το σαν το άνοιγμα ενός εγγράφου στο Word πριν αρχίσετε την επεξεργασία.

```csharp
using Aspose.Slides;

// Step 1: Load the source presentation
Presentation presentation = new Presentation(@"C:\MyProjects\input.pptx");
```

> **Γιατί είναι σημαντικό:** Το αντικείμενο `Presentation` είναι το σημείο εισόδου για όλες τις περαιτέρω λειτουργίες. Αναλύει το αρχείο, δημιουργεί ένα μοντέλο αντικειμένων των διαφανειών, σχήματος, διαγραμμάτων και αντικειμένων OLE, και διατηρεί τα πάντα σε μεταβλητή κατάσταση.

## Βήμα 2 – Δημιουργία Επιλογών Αποθήκευσης και Ενεργοποίηση Επεξεργάσιμων Διαγραμμάτων

Από προεπιλογή, όταν καλείτε `Save` η βιβλιοθήκη μετατρέπει τα διαγράμματα σε στατικές εικόνες. Για να τα διατηρήσετε επεξεργάσιμα πρέπει να ενεργοποιήσετε τη σημαία `ExportEditableCharts`.

```csharp
// Step 2: Create PPTX save options and enable editable charts
PptxSaveOptions saveOptions = new PptxSaveOptions
{
    // This tells Aspose to keep chart data in a format PowerPoint can edit.
    ExportEditableCharts = true
};
```

> **Πώς λειτουργεί:** Όταν το `ExportEditableCharts` είναι `true`, η βιβλιοθήκη γράφει τον ορισμό XML του διαγράμματος (`chart.xml`) μέσα στο PPTX αντί να το rasterize. Το PowerPoint διαβάζει αυτό το XML και επιτρέπει στον χρήστη να ανοίξει τον επεξεργαστή διαγράμματος.

## Βήμα 3 – Ενεργοποίηση Εξαγωγής Ενσωματωμένων Αντικειμένων OLE

Πολλές παρουσιάσεις ενσωματώνουν φύλλα Excel, διαγράμματα Visio ή ακόμη και αρχεία PDF ως αντικείμενα OLE. Αν θέλετε αυτά να παραμείνουν μετά το round‑trip, ενεργοποιήστε το `ExportOLEObjects`.

```csharp
// Step 3: Enable export of embedded OLE objects
saveOptions.ExportOLEObjects = true;
```

> **Τι σημαίνει πραγματικά “εξαγωγή αντικειμένων OLE”:** Το πακέτο OLE αποθηκεύεται ως δυαδικό blob μέσα στο PPTX. Ορίζοντας αυτή τη σημαία διατηρείται το αρχικό δυαδικό, επιτρέποντας στον παραλήπτη να κάνει διπλό‑κλικ στο αντικείμενο και να το ανοίξει στην εγγενή του εφαρμογή (π.χ., Excel). Χωρίς αυτή τη ρύθμιση, το αντικείμενο OLE θα αφαιρεθεί, σπάζοντας συνδέσμους και χάνοντας δεδομένα.

## Βήμα 4 – Αποθήκευση της Παρουσίασης με τις Διαμορφωμένες Επιλογές

Τώρα που έχουμε προετοιμάσει τις επιλογές, απλώς λέμε στο Aspose να γράψει το αρχείο.

```csharp
// Step 4: Save the presentation with the configured options
presentation.Save(@"C:\MyProjects\editable.pptx", saveOptions);
```

> **Αποτέλεσμα:** Το `editable.pptx` περιέχει τις ίδιες διαφάνειες με το `input.pptx`, αλλά οποιοδήποτε διάγραμμα μπορεί να επεξεργαστεί απευθείας στο PowerPoint, και όλα τα ενσωματωμένα αντικείμενα OLE παραμένουν αμετάβλητα.

### Πλήρες Παράδειγμα Εργασίας

Παρακάτω βρίσκεται το πλήρες, αυτόνομο πρόγραμμα που μπορείτε να μεταγλωττίσετε και να εκτελέσετε. Περιλαμβάνει δηλώσεις `using`, σωστή διαχείριση πόρων και σχόλια που εξηγούν κάθε γραμμή.

```csharp
using System;
using Aspose.Slides;

namespace ExportChartsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Path to the source PPTX
            string sourcePath = @"C:\MyProjects\input.pptx";
            // Path where the edited PPTX will be saved
            string destPath = @"C:\MyProjects\editable.pptx";

            // Load the presentation
            using (Presentation presentation = new Presentation(sourcePath))
            {
                // Configure save options
                PptxSaveOptions options = new PptxSaveOptions
                {
                    ExportEditableCharts = true,   // make charts editable
                    ExportOLEObjects = true        // export OLE objects such as embedded Excel sheets
                };

                // Save the new file
                presentation.Save(destPath, options);
            }

            Console.WriteLine("Presentation saved with editable charts and OLE objects.");
        }
    }
}
```

**Αναμενόμενο αποτέλεσμα:** Μετά την εκτέλεση του προγράμματος, ανοίξτε το `editable.pptx` στο PowerPoint. Δεξί‑κλικ σε οποιοδήποτε διάγραμμα → *Edit Data* → ανοίγει ο επεξεργαστής διαγράμματος, επιβεβαιώνοντας ότι **η δυνατότητα επεξεργασίας διαγραμμάτων** λειτούργησε. Διπλό‑κλικ σε ενσωματωμένο φύλλο Excel, και ανοίγει στο Excel, αποδεικνύοντας ότι **η εξαγωγή αντικειμένων OLE** λειτουργεί.

![how to export charts diagram](https://example.com/images/export-charts.png "how to export charts – PowerPoint after export")

*(Alt text: πώς να εξάγετε διαγράμματα – στιγμιότυπο οθόνης PowerPoint με επεξεργάσιμο διάγραμμα και αντικείμενο OLE)*

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

### Τι γίνεται αν το πηγαίο αρχείο δεν περιέχει διαγράμματα;

Ο κώδικας θα τρέξει κανονικά· το `ExportEditableCharts` απλώς δεν έχει καμία επίδραση επειδή δεν υπάρχει τίποτα προς μετατροπή. Δεν θα προκληθεί σφάλμα.

### Μπορώ να εξάγω μόνο συγκεκριμένα διαγράμματα;

Ναι. Αντί να χρησιμοποιήσετε τη γενική σημαία `ExportEditableCharts`, μπορείτε να διασχίσετε το `presentation.Slides` και να ορίσετε `Chart.IsEditable = true` σε μεμονωμένα αντικείμενα διαγράμματος πριν την αποθήκευση. Αυτό προσφέρει λεπτομερή έλεγχο.

```csharp
foreach (ISlide slide in presentation.Slides)
{
    foreach (IChart chart in slide.Shapes.OfType<IChart>())
    {
        chart.IsEditable = true; // enable editability only for this chart
    }
}
```

### Η ενεργοποίηση της εξαγωγής OLE αυξάνει το μέγεθος του αρχείου;

Λίγο. Τα δυαδικά ρεύματα OLE αποθηκεύονται ακριβώς όπως είναι, οπότε το τελικό PPTX μπορεί να είναι μερικά kilobytes μεγαλύτερο. Στις περισσότερες επιχειρησιακές περιπτώσεις η ανταλλαγή αξίζει τον κόπο επειδή διατηρείτε πλήρη επεξεργασιμότητα.

### Ποιες εκδόσεις του PowerPoint μπορούν να ανοίξουν το παραγόμενο αρχείο;

Οποιαδήποτε έκδοση που υποστηρίζει το πρότυπο OOXML (PowerPoint 2007 και μεταγενέστερα). Η δυνατότητα επεξεργάσιμου διαγράμματος βασίζεται στον ενσωματωμένο επεξεργαστή διαγραμμάτων που εισήχθη στο Office 2007, οπότε παλαιότερα binaries όπως `.ppt` δεν θα επωφεληθούν.

## Συμβουλές για Κώδικα Έτοιμο για Παραγωγή

| Συμβουλή | Αιτία |
|----------|-------|
| Χρησιμοποιήστε μπλοκ `using` (όπως φαίνεται) για την απελευθέρωση αντικειμένων `Presentation`. | Αποτρέπει διαρροές μνήμης, ειδικά όταν επεξεργάζεστε πολλά αρχεία σε batch. |
| Επικυρώστε τις διαδρομές αρχείων πριν τη φόρτωση. | Αποτρέπει `FileNotFoundException` που θα έσπαγε μια υπηρεσία στο παρασκήνιο. |
| Καταγράψτε τις ρυθμίσεις `ExportEditableCharts` και `ExportOLEObjects`. | Χρήσιμο για troubleshooting όταν ένας χρήστης αναφέρει μη επεξεργάσιμα διαγράμματα. |
| Πιάστε το `Aspose.Slides.Exception` ξεχωριστά. | Παρέχει πιο σαφή μηνύματα σφάλματος από τη βιβλιοθήκη (π.χ., μη υποστηριζόμενοι τύποι διαγραμμάτων). |
| Σκεφτείτε το `PptxCompressionLevel` αν το μέγεθος του αρχείου μετράει. | Μπορείτε να συμπιέσετε το αποτέλεσμα ενώ διατηρείτε την επεξεργασιμότητα. |

## Ανακεφαλαίωση – Τι Καταφέραμε

Ξεκινήσαμε με μια σαφή ερώτηση: **πώς να εξάγουμε διαγράμματα** από αρχείο PowerPoint διατηρώντας την επεξεργασιμότητα και διατηρώντας τα ενσωματωμένα αντικείμενα OLE. Φορτώνοντας την παρουσίαση, διαμορφώνοντας τις `PptxSaveOptions` (`ExportEditableCharts = true` και `ExportOLEObjects = true`) και αποθηκεύοντας το αρχείο, έχουμε τώρα ένα PPTX που ικανοποιεί και τις δύο απαιτήσεις. Το ίδιο μοτίβο μπορεί να επαναχρησιμοποιηθεί για batch μετατροπές, pipelines CI ή οποιοδήποτε αυτοματοποιημένο εργαλείο αναφοράς.

## Τι Να Εξερευνήσετε Στη Σύντομη Μελλοντική

- **Εξαγωγή διαγραμμάτων ως εικόνες** για στατικές αναφορές (`saveOptions.ExportEditableCharts = false`).  
- **Μετατροπή PPTX σε PDF** διατηρώντας διανυσματικά γραφικά (`PdfSaveOptions`).  
- **Προγραμματιστική τροποποίηση δεδομένων διαγράμματος** (π.χ., ενημέρωση τιμών σειράς πριν την εξαγωγή).  
- **Ενσωμάτωση με Azure Functions** για παροχή API on‑demand εξαγωγής διαγραμμάτων.

Πειραματιστείτε ελεύθερα και ενημερώστε μας για τυχόν edge cases που συναντήσατε. Καλή προγραμματιστική και να παραμείνουν όλα τα διαγράμματά σας επεξεργάσιμα!

## Τι Θα Μάθετε Στη Σειρά;

Οι παρακάτω οδηγίες καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε επιπλέον δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στα δικά σας έργα.

- [How to Export Excel Charts to PDF Using Aspose.Cells for .NET: A Step-by-Step Guide](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [How to Convert Excel Charts to SVG Using Aspose.Cells for .NET (Step-by-Step Guide)](/cells/english/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)
- [How to Apply Themes to Excel Charts Using Aspose.Cells .NET: A Step-by-Step Guide](/cells/english/net/charts-graphs/apply-themes-charts-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}