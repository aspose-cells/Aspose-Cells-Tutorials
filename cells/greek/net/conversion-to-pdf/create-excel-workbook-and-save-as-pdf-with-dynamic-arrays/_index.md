---
category: general
date: 2026-09-15
description: Δημιουργήστε βιβλίο εργασίας Excel σε C# και μάθετε πώς να αποθηκεύετε
  το βιβλίο εργασίας ως PDF ενώ εξαπλώνετε δυναμικούς πίνακες χρησιμοποιώντας τη λειτουργία
  EXPAND.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- save workbook as pdf
- spill dynamic array
- use expand function
- how to create dynamic array in excel
language: el
lastmod: 2026-09-15
og_description: Δημιουργήστε βιβλίο εργασίας Excel σε C# και αποθηκεύστε γρήγορα το
  βιβλίο εργασίας ως PDF, χρησιμοποιώντας τη λειτουργία EXPAND για να εξαπλώσετε έναν
  δυναμικό πίνακα.
og_image_alt: Create Excel workbook screenshot showing dynamic array and PDF output
og_title: Δημιουργία βιβλίου εργασίας Excel και αποθήκευση ως PDF με δυναμικούς πίνακες
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Create Excel workbook in C# and learn how to save workbook as PDF while
    spilling dynamic arrays using the EXPAND function.
  headline: Create Excel workbook and save as PDF with dynamic arrays
  type: TechArticle
tags:
- excel
- csharp
- aspose-cells
- pdf
- dynamic-array
title: Δημιουργία βιβλίου εργασίας Excel και αποθήκευση ως PDF με δυναμικούς πίνακες
url: /el/net/conversion-to-pdf/create-excel-workbook-and-save-as-pdf-with-dynamic-arrays/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία βιβλίου εργασίας Excel και αποθήκευση ως PDF με δυναμικούς πίνακες

Αν χρειάζεται να **δημιουργήσετε βιβλίο εργασίας Excel** προγραμματιστικά και στη συνέχεια **αποθηκεύσετε το βιβλίο εργασίας ως PDF**, αυτός ο οδηγός σας παρουσιάζει μια πλήρη, end‑to‑end λύση σε C#. Θα δείτε επίσης πώς να **αναπτύξετε δυναμικούς πίνακες** χρησιμοποιώντας τη **συνάρτηση EXPAND**, που είναι ο σύγχρονος τρόπος δημιουργίας πινάκων χωρίς VBA.  

Είτε δημιουργείτε μια υπηρεσία αναφορών, μια λειτουργία εξαγωγής για σύστημα ERP, είτε έναν πίνακα ελέγχου βασισμένο σε δεδομένα, τα παρακάτω βήματα σας επιτρέπουν να δημιουργήσετε ένα βιβλίο εργασίας, να το γεμίσετε με δεδομένα smart‑marker και να παραγάγετε ένα PDF που διατηρεί προχωρημένα χαρακτηριστικά γραμματοσειράς.

## Προαπαιτούμενα

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

* .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί επίσης με .NET Framework 4.8)
* Μια πρόσφατη έκδοση του **Aspose.Cells for .NET** (v25.8 ή νεότερη) – παρέχει `Workbook`, `PdfSaveOptions` και `SmartMarkerProcessor`.
* Ένα IDE όπως το Visual Studio 2022 (οποιοσδήποτε επεξεργαστής που μπορεί να μεταγλωττίσει C# λειτουργεί).

Προσθέστε το πακέτο NuGet στο έργο σας:

```bash
dotnet add package Aspose.Cells --version 25.8
```

## Βήμα 1: Δημιουργία βιβλίου εργασίας Excel και ρύθμιση του πρώτου φύλλου

Το πρώτο καθήκον είναι να **δημιουργήσετε βιβλίο εργασίας Excel** και να αποκτήσετε μια αναφορά στο προεπιλεγμένο φύλλο. Αυτό το φύλλο θα φιλοξενήσει τον δυναμικό πίνακα και το πρότυπο Smart Marker.

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;
using System;

class Program
{
    static void Main()
    {
        // Create a new workbook in memory
        Workbook wb = new Workbook();

        // Get the first (default) worksheet
        Worksheet ws = wb.Worksheets[0];
```

*Γιατί είναι σημαντικό*: Η δημιουργία ενός `Workbook` διανέμει τη δομή του εσωτερικού βιβλίου εργασίας, ενώ η πρόσβαση στο `Worksheets[0]` σας δίνει ένα έτοιμο φύλλο χωρίς να χρειάζεται να προσθέσετε κάποιο χειροκίνητα.

## Βήμα 2: Ανάπτυξη δυναμικού πίνακα με τη συνάρτηση EXPAND

Η **συνάρτηση EXPAND** του Excel μπορεί να μετατρέψει ένα στατικό κυριολεκτικό πίνακα σε μια περιοχή διασποράς οποιουδήποτε μεγέθους. Εδώ ζητάμε από το Excel να επεκτείνει το `{1,2,3}` σε περιοχή 5 γραμμών × 1 στήλης που ξεκινά από το `A1`.

```csharp
        // Write the EXPAND formula into A1
        ws.Cells["A1"].Formula = "=EXPAND({1,2,3},5,1)";

        // Force calculation so the spill occurs immediately
        ws.Calculate();
```

*Γιατί είναι σημαντικό*: Η χρήση του `EXPAND` αποφεύγει χειροκίνητους βρόχους σε C#. Η μηχανή υπολογίζει την περιοχή διασποράς και αποθηκεύει τις τιμές απευθείας στο φύλλο, που αργότερα εμφανίζονται στο PDF.

## Βήμα 3: Αποθήκευση βιβλίου εργασίας ως PDF διατηρώντας επιλογείς παραλλαγής γραμματοσειράς

Όταν χρειάζεται να **αποθηκεύσετε το βιβλίο εργασίας ως PDF**, μπορείτε επίσης να ενεργοποιήσετε προχωρημένα τυπογραφικά χαρακτηριστικά όπως οι επιλογείς παραλλαγής γραμματοσειράς (διαθέσιμοι από το Aspose.Cells v25.8). Αυτό εξασφαλίζει ότι τα PDF αποδίδουν σωστά σύνθετα σενάρια.

```csharp
        // Configure PDF options
        PdfSaveOptions pdfOpts = new PdfSaveOptions
        {
            FontVariationSelectors = true   // keeps variation selectors for OpenType fonts
        };

        // Save the current workbook (with the spilled array) as PDF
        wb.Save(@"YOUR_DIRECTORY\VarSelector.pdf", pdfOpts);
```

*Γιατί είναι σημαντικό*: Ο ορισμός του `FontVariationSelectors` σε `true` είναι κρίσιμος για γλώσσες που βασίζονται σε παραλλαγές γλύφων (π.χ. Κινέζικα, Ιαπωνικά, emoji). Το παραγόμενο PDF αντικατοπτρίζει την προβολή του Excel στην οθόνη.

## Βήμα 4: Εισαγωγή προτύπου Smart Marker που αναφέρεται σε ένθετη πηγή δεδομένων

Τα Smart Markers σας επιτρέπουν να ενσωματώσετε placeholders απευθείας στο φύλλο. Το παρακάτω πρότυπο θα δημιουργήσει μια λίστα παραγγελιών και των στοιχείων τους.

```csharp
        // Define a Smart Marker template in cell A1
        string template = "${Orders.OrderId}\n${Orders.Items:ItemName}\n";
        ws.Cells["A1"].PutValue(template);
```

*Γιατί είναι σημαντικό*: Τοποθετώντας το πρότυπο στο `A1`, λέτε στο Aspose.Cells πού να ξεκινήσει η επέκταση των δεδομένων. Η σύνταξη `:` (`Items:ItemName`) λέει στον επεξεργαστή να επαναλάβει μια ένθετη συλλογή.

## Βήμα 5: Ορισμός της ένθετης πηγής δεδομένων (παραγγελίες με στοιχεία)

Δημιουργούμε έναν ανώνυμο πίνακα παραγγελιών, η κάθε μία από τις οποίες περιέχει τη δική της συλλογή αντικειμένων στοιχείων. Αυτό αντικατοπτρίζει ένα τυπικό σενάριο master‑detail.

```csharp
        // Sample nested data source
        var orders = new[]
        {
            new
            {
                OrderId = 1,
                Items = new[]
                {
                    new { ItemName = "Apple" },
                    new { ItemName = "Banana" }
                }
            },
            new
            {
                OrderId = 2,
                Items = new[]
                {
                    new { ItemName = "Carrot" }
                }
            }
        };
```

*Γιατί είναι σημαντικό*: Η ένθετη δομή δείχνει **πώς να δημιουργήσετε δυναμικό πίνακα στο Excel** μέσω Smart Markers, χωρίς να γράψετε VBA ή χειροκίνητους βρόχους κελιών.

## Βήμα 6: Επεξεργασία των Smart Markers και αποθήκευση του τελικού αρχείου Excel

Τώρα παραδίδουμε το βιβλίο εργασίας και την πηγή δεδομένων στον `SmartMarkerProcessor`. Μετά την επεξεργασία, τα placeholders αντικαθίστανται με πραγματικές γραμμές και αποθηκεύουμε το αποτέλεσμα ως κανονικό αρχείο `.xlsx`.

```csharp
        // Process the Smart Markers
        SmartMarkerProcessor processor = new SmartMarkerProcessor();
        processor.Process(wb, orders);

        // Save the populated workbook
        wb.Save(@"YOUR_DIRECTORY\NestedSmartMarker.xlsx");
    }
}
```

*Γιατί είναι σημαντικό*: Ο `SmartMarkerProcessor` επεκτείνει αυτόματα το πρότυπο, δημιουργεί τις απαραίτητες γραμμές και τις γεμίζει με δεδομένα. Το τελικό βιβλίο εργασίας μπορεί να ανοιχθεί στο Excel για να επαληθευτεί ότι κάθε παραγγελία και τα στοιχεία της εμφανίζονται σωστά.

## Αναμενόμενο αποτέλεσμα

* **VarSelector.pdf** – ένα αρχείο PDF που δείχνει τους αριθμούς 1‑3 να διασπείρονται σε πέντε γραμμές, αποδομένα με τυχόν παραλλαγές OpenType γραμματοσειράς που ενεργοποιήσατε.
* **NestedSmartMarker.xlsx** – ένα αρχείο Excel με τις ακόλουθες γραμμές (αρχίζοντας από το `A1`):

| OrderId | ItemName |
|---------|----------|
| 1       | Apple    |
| 1       | Banana   |
| 2       | Carrot   |

Η έκδοση PDF διατηρεί την ίδια αριθμητική διασπορά επειδή η κατάσταση του φύλλου αποθηκεύτηκε πριν από την επεξεργασία των Smart Marker· μπορείτε να επαναλάβετε την αποθήκευση PDF μετά την επεξεργασία αν χρειάζεστε τα τελικά δεδομένα σε PDF επίσης.

## Pro tips και κοινές παγίδες

| Συμβουλή | Εξήγηση |
|-----|-------------|
| **Επαναχρησιμοποίηση του ίδιου `PdfSaveOptions`** | Η δημιουργία του αντικειμένου επιλογών μία φορά και η επαναχρησιμοποίησή του αποφεύγει λεπτές διαφορές στην απόδοση (π.χ. έλλειψη επιλογέων παραλλαγής). |
| **Κλήση `ws.Calculate()` μετά τον ορισμό τύπων** | Χωρίς ρητό υπολογισμό, η περιοχή διασποράς μπορεί να παραμείνει κενή όταν ελέγχετε το βιβλίο εργασίας προγραμματιστικά. |
| **Τοποθέτηση προτύπων Smart Marker σε καθαρό φύλλο** | Ο συνδυασμός προτύπων με υπάρχοντα δεδομένα μπορεί να προκαλέσει απρόσμενη εισαγωγή γραμμών. Χρησιμοποιήστε αφιερωμένο φύλλο αν είναι δυνατόν. |
| **Προσοχή στις διαδρομές αρχείων** | Χρησιμοποιήστε `Path.Combine(Environment.CurrentDirectory, "output.pdf")` για να αποφύγετε σκληροκωδικοποιημένους φακέλους σε διαφορετικές μηχανές. |
| **Έλεγχος έκδοσης** | Το `FontVariationSelectors` είναι διαθέσιμο μόνο από την έκδοση 25.8· παλαιότερες εκδόσεις θα αγνοήσουν την ιδιότητα χωρίς να ρίξουν εξαίρεση. |

## Επόμενα βήματα

Τώρα που ξέρετε πώς να **δημιουργήσετε βιβλίο εργασίας Excel**, **αναπτύξετε δυναμικό πίνακα** και **αποθηκεύσετε το βιβλίο εργασίας ως PDF**, μπορείτε να εξερευνήσετε:

* Προσθήκη γραφημάτων ή εικόνων πριν τη μετατροπή σε PDF.
* Εξαγωγή του ίδιου βιβλίου εργασίας σε άλλες μορφές (π.χ. HTML, CSV) χρησιμοποιώντας υπερφορτώσεις του `Save`.
* Χρήση **εκφράσεων Smart Marker** (`${Orders.Total:SUM(Items.Price)}`) για υπολογισμό αθροισμάτων εν κινήσει.
* Ενσωμάτωση αυτού του κώδικα σε ένα ASP.NET Core API ώστε οι χρήστες να μπορούν να κατεβάσουν το παραγόμενο PDF απευθείας από ένα web endpoint.

---

**Σύνοψη** – Αυτός ο οδηγός σας έδειξε πώς να **δημιουργήσετε βιβλίο εργασίας Excel**, να χρησιμοποιήσετε τη **συνάρτηση EXPAND** για **ανάπτυξη δυναμικού πίνακα**, να ενσωματώσετε ένα **Smart Marker** που λειτουργεί με ένθετη πηγή δεδομένων, και τελικά να **αποθηκεύσετε το βιβλίο εργασίας ως PDF** διατηρώντας προχωρημένα χαρακτηριστικά γραμματοσειράς. Το πλήρες, εκτελέσιμο παράδειγμα μπορεί να αντιγραφεί σε οποιοδήποτε έργο C# και να προσαρμοστεί στις δικές σας δομές δεδομένων. Καλή προγραμματιστική!

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικά παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε επιπλέον δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στην υλοποίηση των δικών σας έργων.

- [Δημιουργία και αποθήκευση βιβλίου εργασίας Excel ως PDF σε ASP.NET χρησιμοποιώντας Aspose.Cells](/cells/english/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)
- [Πώς να δημιουργήσετε και να αποθηκεύσετε ένα βιβλίο εργασίας Excel ως ODS χρησιμοποιώντας Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [Πώς να δημιουργήσετε και να αποθηκεύσετε ένα βιβλίο εργασίας Excel ως SVG χρησιμοποιώντας Aspose.Cells for Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}