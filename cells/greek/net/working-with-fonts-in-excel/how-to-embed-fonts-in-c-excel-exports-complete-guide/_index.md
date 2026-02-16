---
category: general
date: 2026-02-15
description: Μάθετε πώς να ενσωματώνετε γραμματοσειρές κατά την εξαγωγή του Excel
  σε SVG και XPS, να γράφετε σωστά χαρακτήρες Unicode και να ενσωματώνετε γραμματοσειρές
  σε SVG χρησιμοποιώντας το Aspose.Cells.
draft: false
keywords:
- how to embed fonts
- export excel to svg
- how to write unicode
- embed fonts in svg
- how to export xps
language: el
og_description: Πώς να ενσωματώσετε γραμματοσειρές κατά την εξαγωγή του Excel σε SVG
  και XPS, να γράψετε χαρακτήρες Unicode και να ενσωματώσετε γραμματοσειρές σε SVG
  με το Aspose.Cells.
og_title: Πώς να ενσωματώσετε γραμματοσειρές σε εξαγωγές Excel με C# – Βήμα προς βήμα
tags:
- Aspose.Cells
- C#
- Excel Export
- Font Embedding
title: Πώς να ενσωματώσετε γραμματοσειρές σε εξαγωγές Excel με C# – Πλήρης οδηγός
url: /el/net/working-with-fonts-in-excel/how-to-embed-fonts-in-c-excel-exports-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Ενσωματώσετε Γραμματοσειρές σε Εξαγωγές Excel με C# – Πλήρης Οδηγός

Έχετε αναρωτηθεί **πώς να ενσωματώσετε γραμματοσειρές** σε μια εξαγωγή Excel ώστε το αποτέλεσμα να φαίνεται ακριβώς το ίδιο σε κάθε μηχάνημα; Δεν είστε ο μόνος. Όταν στέλνετε ένα φύλλο εργασίας σε έναν πελάτη που δεν έχει εγκατεστημένες τις ίδιες γραμματοσειρές, το έγγραφο μπορεί να εμφανιστεί χαραγμένο, ειδικά αν περιέχει ειδικούς χαρακτήρες Unicode. Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από μια πρακτική λύση που όχι μόνο δείχνει **πώς να ενσωματώσετε γραμματοσειρές**, αλλά καλύπτει επίσης **export excel to svg**, **how to write unicode**, και **how to export xps** χρησιμοποιώντας το Aspose.Cells.

Στο τέλος του οδηγού θα έχετε ένα έτοιμο προς εκτέλεση απόσπασμα C# που γράφει έναν χαρακτήρα Unicode με επιλογέα παραλλαγής, ενσωματώνει τις απαιτούμενες γραμματοσειρές και παράγει τόσο αρχεία XPS όσο και SVG που αποδίδονται τέλεια παντού. Χωρίς εξωτερικά εργαλεία, χωρίς μεταγενέστερα hacks—απλός, αυτόνομος κώδικας.

## Προαπαιτούμενα

- .NET 6.0 ή νεότερο (το API λειτουργεί το ίδιο και σε .NET Framework 4.8)
- Aspose.Cells for .NET (πακέτο NuGet `Aspose.Cells`)
- Ένας φάκελος στο δίσκο όπου θα αποθηκευτούν τα παραγόμενα αρχεία
- Βασική εξοικείωση με τη σύνταξη C# (αν είστε απόλυτος αρχάριος, ο κώδικας είναι εκτενώς σχολιασμένος)

Αν έχετε ήδη όλα αυτά έτοιμα, τέλεια—ας περάσουμε κατευθείαν στην υλοποίηση.

## Βήμα 1: Δημιουργία του Workbook και του Worksheet (How to Embed Fonts – The Starting Point)

Το πρώτο που χρειαζόμαστε είναι ένα νέο αντικείμενο `Workbook`. Σκεφτείτε το workbook ως το δοχείο για όλα τα worksheets, τα στυλ και τους πόρους. Η δημιουργία του είναι τριβιακή, αλλά αποτελεί τη βάση για οποιαδήποτε λειτουργία **embed fonts in svg** επειδή οι πληροφορίες γραμματοσειράς ζουν στο επίπεδο του workbook.

```csharp
using Aspose.Cells;

namespace FontEmbeddingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Create a new workbook and grab the first worksheet
            Workbook workbook = new Workbook();               // fresh workbook
            Worksheet ws = workbook.Worksheets[0];            // default sheet
```

> **Γιατί είναι σημαντικό:** Όταν αργότερα εξάγετε σε SVG ή XPS, το Aspose.Cells κοιτάζει τη συλλογή στυλ του workbook για να αποφασίσει ποιες γραμματοσειρές θα ενσωματώσει. Ξεκινώντας με ένα καθαρό workbook εξασφαλίζετε ότι δεν υπάρχουν ανεπιθύμητες αναφορές γραμματοσειρών που θα «μολύνουν» το αποτέλεσμα.

## Βήμα 2: Γράψιμο ενός Χαρακτήρα Unicode με Επιλογέα Παραλλαγής (How to Write Unicode)

Οι χαρακτήρες Unicode μπορεί να είναι δύσκολοι, ειδικά όταν χρειάζεστε μια συγκεκριμένη παραλλαγή γλύφου. Ο χαρακτήρας `𝟘` (MATHEMATICAL DOUBLE‑STRUCK ZERO) σε συνδυασμό με τον Variation Selector‑1 (`\uFE00`) αναγκάζει τον renderer να επιλέξει την «απλή» παρουσίαση. Αυτό αποτελεί τέλεια επίδειξη για **how to write unicode** επειδή δείχνει ακριβώς τη συμβολοσειρά που πρέπει να τοποθετήσετε σε ένα κελί.

```csharp
            // Step 2: Write the character '𝟘' followed by Variation Selector-1 into cell A1
            // The literal "\uFE00" is the Variation Selector; it tells the font to use the base glyph.
            ws.Cells["A1"].PutValue("𝟘\uFE00");
```

> **Συμβουλή:** Αν δείτε ποτέ ένα κουτί με «missing‑glyph» (�) στο αποτέλεσμα, ελέγξτε ξανά ότι η επιλεγμένη γραμματοσειρά υποστηρίζει πραγματικά τόσο τον βασικό χαρακτήρα *όσο* και τον επιλογέα παραλλαγής. Δεν το κάνουν όλες οι γραμματοσειρές.

## Βήμα 3: Εξαγωγή του Worksheet σε XPS (How to Export XPS)

Το XPS είναι μια μορφή σταθερής διάταξης παρόμοια με το PDF αλλά εγγενής στα Windows. Η εξαγωγή σε XPS ενώ **ενσωματώνετε γραμματοσειρές** εγγυάται ότι το έγγραφο θα φαίνεται πανομοιότυπο σε οποιοδήποτε μηχάνημα Windows, ακόμη και αν η γραμματοσειρά δεν είναι εγκατεστημένη τοπικά.

```csharp
            // Step 3: Export the worksheet to XPS – fonts are embedded automatically
            string xpsPath = @"C:\Exports\VarSel.xps";
            ws.Cells.ExportToXps(xpsPath);
```

> **Τι θα δείτε:** Ανοίξτε το παραγόμενο `VarSel.xps` με το Windows Reader· το διπλό‑στρογγυλό μηδέν εμφανίζεται ακριβώς όπως στο Excel, με το σωστό στυλ διατηρημένο.

## Βήμα 4: Εξαγωγή του Worksheet σε SVG με Ενσωματωμένες Γραμματοσειρές (Embed Fonts in SVG)

Το SVG είναι μορφή διανυσματικής εικόνας που οι browsers αποδίδουν «on the fly». Από προεπιλογή, το Aspose.Cells θα αναφέρει τη γραμματοσειρά με το όνομά της, κάτι που μπορεί να οδηγήσει σε προβλήματα missing‑glyph αν ο θεατής δεν έχει την γραμματοσειρά εγκατεστημένη. Η κλάση `SvgSaveOptions` μας επιτρέπει να **embed fonts in SVG**, μετατρέποντας το αρχείο σε ένα αυτόνομο πακέτο.

```csharp
            // Step 4: Export to SVG with fonts embedded
            string svgPath = @"C:\Exports\VarSel.svg";
            SvgSaveOptions svgOptions = new SvgSaveOptions
            {
                EmbedFonts = true          // crucial flag – forces font embedding
            };
            ws.Cells.ExportToSvg(svgPath, svgOptions);
```

> **Αποτέλεσμα:** Ανοίξτε το `VarSel.svg` σε οποιονδήποτε σύγχρονο browser (Chrome, Edge, Firefox). Ο χαρακτήρας Unicode αποδίδεται σωστά χωρίς εξωτερικά αρχεία γραμματοσειράς. Αν εξετάσετε την πηγή SVG, θα δείτε ένα μπλοκ `<style>` που περιέχει έναν Base64‑κωδικοποιημένο ορισμό γραμματοσειράς.

## Πλήρες Παράδειγμα Εργασίας (All Steps Combined)

Παρακάτω βρίσκεται το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε‑και‑επικολλήσετε σε μια εφαρμογή console. Περιλαμβάνει όλα τα παραπάνω βήματα, καθώς και ένα τελικό μήνυμα στην κονσόλα ώστε να ξέρετε πότε ολοκληρώθηκε η διαδικασία.

```csharp
using Aspose.Cells;
using System;

namespace FontEmbeddingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Create workbook and worksheet
            Workbook workbook = new Workbook();
            Worksheet ws = workbook.Worksheets[0];

            // Write Unicode character with variation selector
            ws.Cells["A1"].PutValue("𝟘\uFE00");

            // Export to XPS (fonts embedded automatically)
            string xpsPath = @"C:\Exports\VarSel.xps";
            ws.Cells.ExportToXps(xpsPath);
            Console.WriteLine($"XPS exported to: {xpsPath}");

            // Export to SVG with embedded fonts
            string svgPath = @"C:\Exports\VarSel.svg";
            SvgSaveOptions svgOptions = new SvgSaveOptions
            {
                EmbedFonts = true
            };
            ws.Cells.ExportToSvg(svgPath, svgOptions);
            Console.WriteLine($"SVG exported to: {svgPath}");

            Console.WriteLine("All files generated successfully.");
        }
    }
}
```

### Αναμενόμενο Αποτέλεσμα

- **`VarSel.xps`** – ένα μονοσέλιδο αρχείο XPS που εμφανίζει το διπλό‑στρογγυλό μηδέν στην ακριβή γραμματοσειρά που χρησιμοποιεί το Excel.
- **`VarSel.svg`** – ένα αρχείο SVG που περιέχει ενσωματωμένο ρεύμα γραμματοσειράς· ανοίξτε το σε browser και θα δείτε το ίδιο γλύφο, χωρίς κουτιά «missing character».

## Συνηθισμένα Προβλήματα & Pro Tips (How to Embed Fonts Effectively)

| Πρόβλημα | Γιατί συμβαίνει | Διόρθωση |
|----------|----------------|----------|
| Το γλύφο εμφανίζεται ως τετράγωνο στο SVG | Η γραμματοσειρά δεν ενσωματώθηκε (`EmbedFonts = false`) | Ορίστε `EmbedFonts = true` στο `SvgSaveOptions`. |
| Ο επιλογέας παραλλαγής αγνοείται | Η γραμματοσειρά δεν διαθέτει το αντίστοιχο γλύφο παραλλαγής | Επιλέξτε γραμματοσειρά που υποστηρίζει ρητά τον επιλογέα, π.χ. **Cambria Math** ή **Arial Unicode MS**. |
| Η εξαγωγή αποτυγχάνει με “Access denied” | Ο φάκελος προορισμού είναι μόνο για ανάγνωση ή δεν υπάρχει | Βεβαιωθείτε ότι ο φάκελος (`C:\Exports\`) υπάρχει και ότι η διεργασία έχει δικαιώματα εγγραφής. |
| Το αρχείο XPS είναι τεράστιο | Ενσωματώνονται μεγάλα αρχεία γραμματοσειρών άσκοπα | Χρησιμοποιήστε ελαφριά γραμματοσειρά (π.χ. **Calibri**) αν χρειάζεστε μόνο βασικούς λατινικούς χαρακτήρες. |

> **Pro tip:** Αν εξάγετε πολλά worksheets, επαναχρησιμοποιήστε ένα ενιαίο αντικείμενο `SvgSaveOptions` ώστε να αποφύγετε τη δημιουργία διπλότυπων ρευμάτων γραμματοσειράς, κάτι που μπορεί να φουσκώσει το μέγεθος του SVG.

## Επέκταση της Λύσης (What If You Need More?)

- **Batch Export:** Επανάληψη πάνω από `workbook.Worksheets` και κλήση `ExportToSvg` για κάθε φύλλο, δίνοντας μοναδικό όνομα αρχείου.
- **Προσαρμοσμένη Αντικατάσταση Γραμματοσειράς:** Χρησιμοποιήστε `Style.Font.Name` για να επιβάλλετε συγκεκριμένη γραμματοσειρά πριν την εξαγωγή. Αυτό είναι χρήσιμο όταν το αρχικό workbook χρησιμοποιεί γραμματοσειρά που δεν είναι φιλική προς την άδεια χρήσης.
- **Εικόνες Υψηλότερης Ανάλυσης:** Για μορφές βασισμένες σε raster (PNG, JPEG) μπορείτε να ορίσετε `Resolution` στο `ImageOrPrintOptions` – δεν χρειάζεται για SVG, αλλά είναι καλό να το ξέρετε αν αργότερα αποφασίσετε να δημιουργήσετε προεπισκοπήσεις PNG.

## Συμπέρασμα

Καλύψαμε **πώς να ενσωματώσετε γραμματοσειρές** τόσο σε εξαγωγές XPS όσο και SVG, δείξαμε **πώς να γράψετε Unicode** χαρακτήρες με επιλογείς παραλλαγής, και σας δείξαμε **πώς να εξάγετε excel to svg** διασφαλίζοντας ότι οι γραμματοσειρές παραμένουν μέσα στο αρχείο. Ακολουθώντας τα παραπάνω βήματα, εξαλείφετε το εφιαλτικό πρόβλημα «missing font» και εγγυάστε ότι όποιος—ανεξαρτήτως των εγκατεστημένων γραμματοσειρών—θα δει ακριβώς αυτό που προοριζόσασταν.

Έτοιμοι για την επόμενη πρόκληση; Δοκιμάστε να ενσωματώσετε μια προσαρμοσμένη TrueType γραμματοσειρά που δεν είναι εγκατεστημένη στον server, ή πειραματιστείτε με εξαγωγή σε PDF διατηρώντας τις ενσωματωμένες γραμματοσειρές. Και οι δύο διαδρομές βασίζονται στις ίδιες αρχές που εξερευνήσαμε εδώ.

Καλή προγραμματιστική δουλειά, και ας είναι τα εξαγόμενα έγγραφά σας πάντα pixel‑perfect!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}