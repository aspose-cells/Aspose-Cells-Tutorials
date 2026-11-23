---
category: general
date: 2026-11-22
description: Συμπλήρωση προτύπου Excel χρησιμοποιώντας το Aspose.Cells για τη δημιουργία
  πολλαπλών φύλλων, αποθήκευση του βιβλίου εργασίας Aspose και δημιουργία αναφοράς
  master‑detail σε C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- populate excel template
- generate multiple sheets
- save aspose workbook
- generate master detail report
language: el
lastmod: 2026-11-22
og_description: Συμπληρώστε το πρότυπο Excel με το Aspose.Cells, δημιουργήστε πολλαπλά
  φύλλα, αποθηκεύστε το βιβλίο εργασίας Aspose και δημιουργήστε μια αναφορά master‑detail
  σε ένα ενιαίο πρόγραμμα C#.
og_image_alt: Screenshot showing a populated Excel workbook with multiple detail sheets
og_title: Συμπληρώστε το πρότυπο Excel & δημιουργήστε πολλαπλά φύλλα με το Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: populate excel template using Aspose.Cells to generate multiple sheets,
    save aspose workbook, and create a master‑detail report in C#.
  headline: How to populate Excel template and generate multiple sheets with Aspose.Cells
  type: TechArticle
- description: populate excel template using Aspose.Cells to generate multiple sheets,
    save aspose workbook, and create a master‑detail report in C#.
  name: How to populate Excel template and generate multiple sheets with Aspose.Cells
  steps:
  - name: What the resulting workbook looks like
    text: '| Sheet name | Content | |------------|----------| | **Master** | Header
      row with order summary (OrderId, Customer) | | **Details_1** | All `OrderLines`
      where `OrderId = 1` (Pen, Notebook) | | **Details_2** | All `OrderLines` where
      `OrderId = 2` (Pencil) |'
  - name: Expected output
    text: 'Open `MasterDetailResult.xlsx` and you will see:'
  - name: Next steps
    text: '* Explore **SmartMarkerOptions** such as `EnableFormulaCalculation` to
      evaluate formulas after data insertion. * Add charts to the master sheet and
      let the processor update series ranges automatically. * Combine this approach
      with **Aspose.Slides** to export the same data to PowerPoint presentations'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Πώς να συμπληρώσετε πρότυπο Excel και να δημιουργήσετε πολλαπλά φύλλα με το
  Aspose.Cells
url: /el/net/templates-reporting/how-to-populate-excel-template-and-generate-multiple-sheets/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να γεμίσετε πρότυπο Excel και να δημιουργήσετε πολλαπλά φύλλα με το Aspose.Cells

Αν χρειάζεστε να **γεμίσετε πρότυπο Excel** με δυναμικά δεδομένα, αυτός ο οδηγός σας παρουσιάζει μια πλήρη, έτοιμη‑για‑εκτέλεση λύση. Χρησιμοποιώντας τη μηχανή Smart Marker του Aspose.Cells μπορείτε να **δημιουργήσετε πολλαπλά φύλλα**, να αποθηκεύσετε το **Aspose workbook**, και να παραγάγετε μια πλήρη **αναφορά master‑detail** χωρίς χειροκίνητη αντιγραφή ή μακροεντολές VBA.

Ο οδηγός περνάει από κάθε βήμα—από την προετοιμασία των συλλογών master‑detail μέχρι την αποθήκευση του τελικού αρχείου—ώστε να μπορείτε να αντιγράψετε τον κώδικα στο δικό σας έργο και να δείτε άμεσα αποτελέσματα.

## Προαπαιτούμενα

* .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί επίσης με .NET Framework 4.7+)
* Aspose.Cells για .NET εγκατεστημένο (`dotnet add package Aspose.Cells`)
* Ένα βασικό περιβάλλον ανάπτυξης C# (Visual Studio, VS Code, Rider, κ.λπ.)
* Ένα πρότυπο Excel (`MasterDetailTemplate.xlsx`) που περιέχει ετικέτες Smart Marker όπως `&=Orders.OrderId` και έναν πίνακα λεπτομερειών σημειωμένο με `&=OrderLines`.

> **Συμβουλή:** Κρατήστε το πρότυπο στον ίδιο φάκελο με το έργο ή χρησιμοποιήστε απόλυτη διαδρομή για να αποφύγετε το `FileNotFoundException`.

## Επισκόπηση της λύσης

1. **Προετοιμάστε συλλογές δεδομένων master‑detail** – τα αντικείμενα προέλευσης που τροφοδοτούν την αναφορά.  
2. **Φορτώστε το πρότυπο Excel** που ήδη περιέχει placeholders Smart Marker.  
3. **Δημιουργήστε ένα `SmartMarkerProcessor`** για την ερμηνεία των markers.  
4. **Εφαρμόστε τα δεδομένα** και αφήστε το Aspose.Cells **να δημιουργήσει πολλαπλά φύλλα** αυτόματα.  
5. **Αποθηκεύστε το Aspose workbook** στο δίσκο.

Κάθε βήμα εξηγείται παρακάτω, με πλήρη κώδικα και το αναμενόμενο αποτέλεσμα.

![παράδειγμα γεμίσματος προτύπου Excel](https://example.com/images/populate-excel-template.png "παράδειγμα γεμίσματος προτύπου Excel")

## Βήμα 1: Προετοιμάστε συλλογές δεδομένων master‑detail

Οι αναφορές master‑detail βασίζονται σε δύο σχετικές συλλογές: μια λίστα παραγγελιών (master) και μια λίστα γραμμών παραγγελίας (detail). Η μηχανή Smart Marker ταιριάζει τις γραμμές με βάση το πεδίο `OrderId`.

```csharp
using System.Collections.Generic;

// Master collection – one record per order
var orders = new List<object>
{
    new { OrderId = 1, Customer = "Alice" },
    new { OrderId = 2, Customer = "Bob" }
};

// Detail collection – multiple rows per order
var orderLines = new List<object>
{
    new { OrderId = 1, Item = "Pen",      Qty = 10 },
    new { OrderId = 1, Item = "Notebook", Qty = 5  },
    new { OrderId = 2, Item = "Pencil",   Qty = 20 }
};
```

**Γιατί είναι σημαντικό:**  
Ο `SmartMarkerProcessor` σαρώνει το πρότυπο για markers όπως `&=Orders.OrderId` και `&=OrderLines.Item`. Παρέχοντας δύο ξεχωριστές συλλογές, το Aspose.Cells δημιουργεί αυτόματα ένα νέο φύλλο για κάθε εγγραφή master και γεμίζει τις γραμμές detail αναλόγως.

## Βήμα 2: Φορτώστε το πρότυπο Excel που περιέχει Smart Markers

Το πρότυπο περιέχει τη διάταξη, τη μορφοποίηση και τις ετικέτες placeholder. Διατηρήστε το όνομα αρχείου και τη διαδρομή ακριβή.

```csharp
using Aspose.Cells;

// Adjust the path to where you stored the template
string templatePath = @"YOUR_DIRECTORY\MasterDetailTemplate.xlsx";
Workbook workbook = new Workbook(templatePath);
```

**Γιατί είναι σημαντικό:**  
Η φόρτωση του προτύπου παρέχει στον επεξεργαστή ένα αντικείμενο workbook που ήδη γνωρίζει πού να εισάγει τα δεδομένα. Όλη η μορφοποίηση (γραμματοσειρές, περιγράμματα, τύποι) παραμένει αμετάβλητη, έτσι η παραγόμενη αναφορά φαίνεται επαγγελματική χωρίς επιπλέον κώδικα στυλ.

## Βήμα 3: Δημιουργήστε ένα SmartMarkerProcessor

Ο επεξεργαστής είναι η μηχανή που αντικαθιστά τα markers με πραγματικές τιμές.

```csharp
// Initialise the processor with the loaded workbook
var processor = new SmartMarkerProcessor(workbook);
```

**Γιατί είναι σημαντικό:**  
Ο `SmartMarkerProcessor` απομονώνει τη λογική Smart Marker από το υπόλοιπο workbook, επιτρέποντάς σας να επαναχρησιμοποιήσετε το ίδιο workbook για άλλες λειτουργίες (π.χ., γραφήματα) μετά την εφαρμογή των δεδομένων.

## Βήμα 4: Εφαρμόστε τα δεδομένα master‑detail και δημιουργήστε πολλαπλά φύλλα

Εδώ συνδέουμε τις δύο συλλογές με τον επεξεργαστή και λέμε στο Aspose.Cells πώς να ονομάσει κάθε παραγόμενο φύλλο.

```csharp
using Aspose.Cells.SmartMarkers;

// Combine the collections into an anonymous object matching the marker names
var data = new { Orders = orders, OrderLines = orderLines };

// Options let you control sheet naming and other behaviours
var options = new SmartMarkerOptions
{
    // {0} will be replaced by the master record index (1‑based)
    DetailSheetNewName = "Details_{0}"
};

// Apply the data – this step creates a new sheet for each order
processor.ApplyTemplate(data, options);
```

**Γιατί είναι σημαντικό:**  
Το πρότυπο `DetailSheetNewName` δημιουργεί φύλλα με ονόματα `Details_1`, `Details_2`, κ.λπ., ταιριάζοντας με κάθε παραγγελία στη συλλογή master. Αυτή η αυτόματη δημιουργία φύλλων είναι ο πυρήνας του **δημιουργίας πολλαπλών φύλλων** χωρίς χειροκίνητο βρόχο στο workbook.

### Πώς φαίνεται το παραγόμενο workbook

| Όνομα φύλλου | Περιεχόμενο |
|--------------|-------------|
| **Master** | Γραμμή κεφαλίδας με σύνοψη παραγγελίας (OrderId, Customer) |
| **Details_1** | Όλα τα `OrderLines` όπου `OrderId = 1` (Pen, Notebook) |
| **Details_2** | Όλα τα `OrderLines` όπου `OrderId = 2` (Pencil) |

Το φύλλο master μπορεί επίσης να γεμίσει προσθέτοντας έναν πίνακα Smart Marker που επαναλαμβάνει το `Orders`. Τα φύλλα detail δημιουργούνται αυτόματα από τον επεξεργαστή.

## Βήμα 5: Αποθηκεύστε το Aspose workbook

Τέλος, γράψτε το γεμάτο workbook σε ένα νέο αρχείο.

```csharp
// Choose the output path – ensure the folder exists
string resultPath = @"YOUR_DIRECTORY\MasterDetailResult.xlsx";
workbook.Save(resultPath);
```

**Γιατί είναι σημαντικό:**  
Καλώντας το `Save` γράφει το workbook στη μνήμη σε ένα φυσικό αρχείο `.xlsx`, ολοκληρώνοντας το βήμα **αποθήκευσης Aspose workbook**. Το αρχείο μπορεί να ανοιχτεί στο Excel, Google Sheets ή οποιονδήποτε προβολέα που υποστηρίζει τη μορφή OpenXML.

### Αναμενόμενο αποτέλεσμα

Ανοίξτε το `MasterDetailResult.xlsx` και θα δείτε:

* **Φύλλο “Master”** – έναν πίνακα που καταγράφει την Παραγγελία 1 (Alice) και την Παραγγελία 2 (Bob).  
* **Φύλλο “Details_1”** – δύο γραμμές: Pen (10) και Notebook (5).  
* **Φύλλο “Details_2”** – μία γραμμή: Pencil (20).

Όλη η μορφοποίηση από το αρχικό πρότυπο (χρώματα κεφαλίδας, πλάτη στηλών, μορφές αριθμών) διατηρείται.

## Διαχείριση κοινών περιπτώσεων άκρων

| Περίπτωση | Συνιστώμενη προσέγγιση |
|-----------|------------------------|
| **Πρότυπο δεν βρέθηκε** | Τυλίξτε την κλήση `new Workbook(...)` σε `try/catch` και καταγράψτε το `FileNotFoundException`. |
| **Μεγάλα σύνολα δεδομένων (10 000+ γραμμές)** | Αυξήστε το `SmartMarkerOptions.MaxRowsPerSheet` εάν χρειάζεστε περισσότερες γραμμές ανά φύλλο, ή κάντε σελιδοποίηση χειροκίνητα. |
| **Προσαρμοσμένη ονομασία φύλλων** | Χρησιμοποιήστε μια συμβολοσειρά μορφής όπως `DetailSheetNewName = "Order_{0}_{1}"` όπου το `{1}` μπορεί να είναι μια ιδιότητα από την εγγραφή master (π.χ., `Customer`). |
| **Μορφοποίηση υπό όρους ανά παραγγελία** | Προσθέστε έναν κανόνα μορφοποίησης υπό όρους στο πρότυπο που αναφέρεται σε marker (π.χ., `&=Orders.Status`) και αφήστε τον επεξεργαστή να το αξιολογήσει. |

## Πλήρες εκτελέσιμο πρόγραμμα

Παρακάτω βρίσκεται η πλήρης εφαρμογή κονσόλας C# που συνδυάζει όλα τα κομμάτια. Αντικαταστήστε το `YOUR_DIRECTORY` με μια πραγματική διαδρομή φακέλου στο μηχάνημά σας.

```csharp
using System;
using System.Collections.Generic;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

class SmartMarkerDetailSheetDemo
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Prepare master‑detail data collections
        // -------------------------------------------------
        var orders = new List<object>
        {
            new { OrderId = 1, Customer = "Alice" },
            new { OrderId = 2, Customer = "Bob" }
        };

        var orderLines = new List<object>
        {
            new { OrderId = 1, Item = "Pen",      Qty = 10 },
            new { OrderId = 1, Item = "Notebook", Qty = 5  },
            new { OrderId = 2, Item = "Pencil",   Qty = 20 }
        };

        // -------------------------------------------------
        // Step 2: Load the template workbook that contains smart markers
        // -------------------------------------------------
        string templatePath = @"YOUR_DIRECTORY\MasterDetailTemplate.xlsx";
        Workbook workbook = new Workbook(templatePath);

        // -------------------------------------------------
        // Step 3: Create a SmartMarkerProcessor to handle the template
        // -------------------------------------------------
        var processor = new SmartMarkerProcessor(workbook);

        // -------------------------------------------------
        // Step 4: Apply the master‑detail data and generate multiple sheets
        // -------------------------------------------------
        var data = new { Orders = orders, OrderLines = orderLines };
        var options = new SmartMarkerOptions
        {
            DetailSheetNewName = "Details_{0}"
        };

        processor.ApplyTemplate(data, options);

        // -------------------------------------------------
        // Step 5: Save the populated Aspose workbook
        // -------------------------------------------------
        string resultPath = @"YOUR_DIRECTORY\MasterDetailResult.xlsx";
        workbook.Save(resultPath);

        Console.WriteLine($"Report generated successfully: {resultPath}");
    }
}
```

Εκτελέστε το πρόγραμμα (`dotnet run` ή `Ctrl+F5` στο Visual Studio). Όταν ολοκληρωθεί, ανοίξτε το `MasterDetailResult.xlsx` για να επαληθεύσετε ότι η **γεμίζοντας πρότυπο Excel** παρήγαγε την αναμενόμενη αναφορά master‑detail με **πολλαπλά φύλλα**.

## Συμπέρασμα

Τώρα ξέρετε πώς να **γεμίσετε πρότυπο Excel** με το Aspose.Cells, **να δημιουργήσετε πολλαπλά φύλλα**, **να αποθηκεύσετε Aspose workbook**, και να δημιουργήσετε μια αξιόπιστη **αναφορά master‑detail** με λίγες μόνο γραμμές C#. Η μηχανή Smart Marker αφαιρεί την ανάγκη για χειροκίνητους βρόχους, διατηρεί τη μορφοποίηση αμετάβλητη και κλιμακώνεται εύκολα σε μεγαλύτερα σύνολα δεδομένων.

### Επόμενα βήματα

* Εξερευνήστε τις **SmartMarkerOptions** όπως `EnableFormulaCalculation` για την αξιολόγηση τύπων μετά την εισαγωγή δεδομένων.  
* Προσθέστε γραφήματα στο φύλλο master και αφήστε τον επεξεργαστή να ενημερώνει αυτόματα τις περιοχές των σειρών.  
* Συνδυάστε αυτήν την προσέγγιση με το **Aspose.Slides** για να εξάγετε τα ίδια δεδομένα σε παρουσιάσεις PowerPoint.

### Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά σχετικά θέματα που βασίζονται στις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Δημιουργία αναφοράς master‑detail σε C# – Γέμισμα προτύπου Excel με SmartMarker](/cells/english/net/smart-markers-dynamic-data/create-master-detail-report-in-c-populate-excel-template-wit/)
- [Πώς να δημιουργήσετε Excel από πρότυπο με C# και Aspose.Cells](/cells/english/net/templates-reporting/how-to-generate-excel-from-template-with-c-and-aspose-cells/)
- [Aspose Cells Smart Markers – Γέμισμα προτύπου Excel](/cells/english/java/templates-reporting/aspose-cells-smart-markers-populate-excel-template/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}