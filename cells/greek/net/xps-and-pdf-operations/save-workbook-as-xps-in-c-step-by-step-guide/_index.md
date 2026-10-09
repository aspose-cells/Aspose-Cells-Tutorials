---
category: general
date: 2026-06-27
description: Αποθηκεύστε το βιβλίο εργασίας ως XPS γρήγορα με C#. Μάθετε πώς να εξάγετε
  το Excel σε XPS χρησιμοποιώντας το Aspose.Cells και να διαχειριστείτε τους επιλογείς
  παραλλαγής Unicode.
draft: false
keywords:
- save workbook as xps
- export excel to xps
- Aspose.Cells XPS export
- C# Excel to XPS
- Unicode variation selector
language: el
og_description: Αποθήκευση βιβλίου εργασίας ως XPS με το Aspose.Cells. Αυτό το σεμινάριο
  δείχνει πώς να εξάγετε το Excel σε XPS, να διαχειριστείτε τους επιλογείς παραλλαγής
  και να επαληθεύσετε το αποτέλεσμα.
og_title: Αποθήκευση βιβλίου εργασίας ως XPS σε C# – Πλήρης οδηγός προγραμματισμού
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Save workbook as XPS quickly with C#. Learn how to export Excel to
    XPS using Aspose.Cells and handle Unicode variation selectors.
  headline: Save Workbook as XPS in C# – Step‑by‑Step Guide
  type: TechArticle
- description: Save workbook as XPS quickly with C#. Learn how to export Excel to
    XPS using Aspose.Cells and handle Unicode variation selectors.
  name: Save Workbook as XPS in C# – Step‑by‑Step Guide
  steps:
  - name: '**Read the .xlsx** with OpenXML, pull cell values.'
    text: '**Read the .xlsx** with OpenXML, pull cell values.'
  - name: '**Render a bitmap** of each worksheet using `Graphics` (or a third‑party
      renderer).'
    text: '**Render a bitmap** of each worksheet using `Graphics` (or a third‑party
      renderer).'
  - name: '**Create an XPS document** via `XpsDocumentWriter` and draw the bitmap
      onto each page.'
    text: '**Create an XPS document** via `XpsDocumentWriter` and draw the bitmap
      onto each page.'
  type: HowTo
tags:
- C#
- Excel
- XPS
- Aspose.Cells
title: Αποθήκευση φύλλου εργασίας ως XPS σε C# – Οδηγός βήμα‑βήμα
url: /el/net/xps-and-pdf-operations/save-workbook-as-xps-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Αποθήκευση Φύλλου Εργασίας ως XPS σε C# – Πλήρης Οδηγός Προγραμματισμού

Προσπαθήσατε ποτέ να **αποθηκεύσετε ένα φύλλο εργασίας ως XPS** και αντιμετωπίσατε δυσκολίες επειδή η τεκμηρίωση ήταν ασαφής; Δεν είστε οι μόνοι. Είτε χρειάζεστε μια εκτυπώσιμη έκδοση XPS μιας οικονομικής αναφοράς είτε απλώς πειραματίζεστε με μορφές βασισμένες σε διανύσματα, η μετατροπή ενός φύλλου εργασίας Excel σε έγγραφο XPS είναι εκπληκτικά απλή—αφού γνωρίζετε τις σωστές κλήσεις API.

Σε αυτόν τον οδηγό θα περάσουμε από όλη τη διαδικασία, από τη δημιουργία ενός νέου φύλλου εργασίας μέχρι τη διαχείριση επιλογέων παραλλαγής Unicode όπως το παράδειγμα “A️”. Καθ' όλη τη διάρκεια, θα αγγίξουμε και μια συχνή ερώτηση: **πώς εξάγετε Excel σε XPS** χρησιμοποιώντας μια δημοφιλής βιβλιοθήκη .NET. Στο τέλος θα έχετε ένα εκτελέσιμο απόσπασμα, εξηγήσεις κάθε βήματος και μερικές επαγγελματικές συμβουλές για να αποφύγετε τα άκρια σενάρια.

## Τι Θα Μάθετε

- Δημιουργήστε ένα φύλλο εργασίας `Aspose.Cells` από την αρχή.  
- Εισάγετε κείμενο που περιέχει έναν επιλογέα παραλλαγής (τον κρυφό χαρακτήρα «στυλ emoji»).  
- Διαμορφώστε τις επιλογές αποθήκευσης XPS (οι προεπιλογές συνήθως είναι επαρκείς).  
- Αποθηκεύστε το φύλλο εργασίας ως αρχείο XPS και επαληθεύστε το αποτέλεσμα.  
- Προαιρετικά: εναλλακτικοί τρόποι **εξαγωγής Excel σε XPS** εάν χρησιμοποιείτε άλλες βιβλιοθήκες ή χρειάζεστε προσαρμοσμένες ρυθμίσεις σελίδας.

### Προαπαιτούμενα

- .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί επίσης σε .NET Framework 4.6+).  
- Ένα έγκυρο άδεια για **Aspose.Cells for .NET** (μπορείτε να ξεκινήσετε με τη δωρεάν δοκιμή).  
- Ένα IDE με το οποίο αισθάνεστε άνετα—Visual Studio, Rider ή ακόμη και VS Code είναι επαρκές.  

Αν έχετε καλύψει αυτά τα βασικά, ας βουτήξουμε.

## Βήμα 1: Δημιουργία Νέου Φύλλου Εργασίας (Αρχικοποίηση του Εγγράφου)

Πρώτα απ' όλα. Χρειαζόμαστε ένα καθαρό αντικείμενο workbook που θα γίνει ο καμβάς μας XPS.

```csharp
// Step 1: Instantiate a fresh workbook
Workbook workbook = new Workbook();
```

Η κλάση `Workbook` είναι το σημείο εισόδου για όλα όσα κάνει το Aspose.Cells. Σκεφτείτε το ως το κενό σημειωματάριο που θα γεμίσετε αργότερα με φύλλα, κελιά και στυλ. Δεν υπάρχει κρυτή μαγεία—απλώς ένα απλό αντικείμενο C# έτοιμο να κρατήσει δεδομένα.

## Βήμα 2: Πρόσβαση στο Πρώτο Φύλλο Εργασίας

Ένα ολοκαίνουργιο workbook έρχεται με ένα προεπιλεγμένο φύλλο εργασίας. Πάρτε το ώστε να αρχίσουμε να γεμίζουμε κελιά.

```csharp
// Step 2: Pull the first (and only) worksheet out of the workbook
Worksheet worksheet = workbook.Worksheets[0];
```

Γιατί ο δείκτης `[0]`; Επειδή το Aspose.Cells αποθηκεύει τα φύλλα εργασίας σε συλλογή με μηδενική βάση. Αν προσθέσετε περισσότερα φύλλα, απλώς προσαρμόστε τον δείκτη ή κάντε επανάληψη στη συλλογή.

## Βήμα 3: Εισαγωγή Κειμένου με Επιλογέα Παραλλαγής

Εδώ το **εξαγωγή Excel σε XPS** παράδειγμα γίνεται λίγο ιδιόρρυθμο. Θα βάλουμε έναν χαρακτήρα ακολουθούμενο από έναν επιλογέα παραλλαγής (`\uFE0F`). Αυτός ο αόρατος κώδικας λέει στους αποτυπωτές Unicode να αντιμετωπίζουν τον προηγούμενο χαρακτήρα ως glyph στυλ emoji όταν είναι δυνατόν.

```csharp
// Step 3: Write a string that includes a variation selector (e.g., "A️")
worksheet.Cells[0, 0].PutValue("A\uFE0F");
```

- `Cells[0, 0]` δείχνει στο κελί **A1** (γραμμή 0, στήλη 0).  
- `PutValue` ανιχνεύει αυτόματα τον τύπο δεδομένων, ώστε να μπορούμε να περάσουμε μια ακατέργαστη συμβολοσειρά.  
- Το `\uFE0F` είναι ο Unicode *variation selector‑16*· οι περισσότεροι σύγχρονοι προβολείς θα εμφανίσουν το “A️” ως ένα στιλιζαρισμένο “A”.

**Επαγγελματική συμβουλή:** Αν παρατηρήσετε αργότερα ότι η έξοδος XPS δείχνει ένα απλό “A” αντί για την φανταχτερή έκδοση, βεβαιωθείτε ότι ο προβολέας XPS υποστηρίζει επιλογείς παραλλαγής. Δεν το κάνουν όλοι οι παλαιότεροι προβολείς.

## Βήμα 4: Προετοιμασία Επιλογών Αποθήκευσης XPS (Συνήθως οι Προεπιλογές)

Το Aspose.Cells παρέχει μια κλάση `XpsSaveOptions` που σας επιτρέπει να ρυθμίσετε το μέγεθος σελίδας, τα περιθώρια και άλλα. Για μια απλή μετατροπή, οι προεπιλογές είναι απολύτως επαρκείς, αλλά θα δημιουργήσουμε το αντικείμενο για να δείξουμε το μοτίβο.

```csharp
// Step 4: Create XPS save options – default settings are fine for most cases
XpsSaveOptions xpsOptions = new XpsSaveOptions();
```

Αν χρειαστεί ποτέ να προσαρμόσετε τον προσανατολισμό της σελίδας ή να ενσωματώσετε γραμματοσειρές, μπορείτε να ορίσετε ιδιότητες στο `xpsOptions` πριν από την αποθήκευση. Για παράδειγμα:

```csharp
xpsOptions.PageSetup.Orientation = PageOrientation.Landscape;
xpsOptions.EmbedStandardFonts = true;
```

Αυτές οι γραμμές είναι προαιρετικές και παραλείπονται από το βασικό παράδειγμα για συντομία.

## Βήμα 5: Αποθήκευση του Φύλλου Εργασίας ως Έγγραφο XPS

Τώρα η στιγμή της αλήθειας—αποθηκεύουμε το workbook σε αρχείο XPS. Επιλέξτε έναν φάκελο στον οποίο έχετε δικαίωμα εγγραφής· το παράδειγμα χρησιμοποιεί μια θέση‑κρατή (placeholder) που θα αντικαταστήσετε με τη δική σας.

```csharp
// Step 5: Persist the workbook as an XPS file
string outputPath = @"C:\Temp\variation.xps";
workbook.Save(outputPath, xpsOptions);
```

Μετά την εκτέλεση αυτής της γραμμής, θα βρείτε το `variation.xps` στο `C:\Temp`. Ανοίξτε το με οποιονδήποτε προβολέα XPS (π.χ. Windows XPS Viewer) και θα πρέπει να δείτε τον χαρακτήρα “A️” όπως αποδίδεται από τη διαχείριση γραμματοσειρών του συστήματός σας.

### Αναμενόμενο Αποτέλεσμα

- **Τύπος αρχείου:** XPS (XML Paper Specification) – μια μορφή βασισμένη σε διανύσματα, προσανατολισμένη σε σελίδες.  
- **Περιεχόμενο:** Μία σελίδα που περιέχει το κείμενο “A️” στο κελί επάνω‑αριστερά.  
- **Επαλήθευση:** Ανοίξτε το αρχείο· ο χαρακτήρας πρέπει να εμφανίζεται ως ένα στιλιζαρισμένο “A” εάν ο προβολέας σας υποστηρίζει επιλογείς παραλλαγής.

![Στιγμιότυπο μιας απλής XPS εγγράφου που δημιουργήθηκε με την αποθήκευση φύλλου εργασίας ως XPS, εμφανίζοντας τον χαρακτήρα A με επιλογέα παραλλαγής](save-workbook-as-xps.png "Στιγμιότυπο που δείχνει το αρχείο XPS που δημιουργήθηκε με την αποθήκευση φύλλου εργασίας ως XPS")

## Εναλλακτική Προσέγγιση: Εξαγωγή Excel σε XPS Χρησιμοποιώντας OpenXML και System.Drawing

Αν δεν είστε δεσμευμένοι στο Aspose.Cells, μπορείτε ακόμη να **εξάγετε Excel σε XPS** με έναν συνδυασμό του Open XML SDK και του χώρου ονομάτων `System.Drawing.Printing`. Η ροή εργασίας είναι λίγο πιο χειροκίνητη:

1. **Διαβάστε το .xlsx** με το OpenXML, εξάγετε τις τιμές των κελιών.  
2. **Αποδώστε ένα bitmap** κάθε φύλλου εργασίας χρησιμοποιώντας `Graphics` (ή τρίτο εργαλείο απόδοσης).  
3. **Δημιουργήστε ένα έγγραφο XPS** μέσω `XpsDocumentWriter` και σχεδιάστε το bitmap σε κάθε σελίδα.

Παρακάτω υπάρχει ένα σκελετό που δείχνει την ιδέα—*δεν είναι έτοιμη αντικατάσταση* αλλά σας δίνει ένα χάρτη εάν η άδεια του Aspose δεν είναι διαθέσιμη.

```csharp
using DocumentFormat.OpenXml.Packaging;
using System.Drawing;
using System.Printing;
using System.Windows.Xps;
using System.Windows.Xps.Packaging;

// Load the Excel file
using (SpreadsheetDocument doc = SpreadsheetDocument.Open(@"C:\Temp\source.xlsx", false))
{
    // Extract data (omitted for brevity)
}

// Render to bitmap (pseudo‑code)
Bitmap bitmap = RenderWorksheetToBitmap(); // You need a renderer here

// Write XPS
using (XpsDocument xpsDoc = new XpsDocument(@"C:\Temp\output.xps", FileAccess.Write))
{
    XpsDocumentWriter writer = XpsDocument.CreateXpsDocumentWriter(xpsDoc);
    Visual visual = new DrawingVisual();
    using (DrawingContext dc = ((DrawingVisual)visual).RenderOpen())
    {
        dc.DrawImage(bitmap, new Rect(0, 0, bitmap.Width, bitmap.Height));
    }
    writer.Write(visual);
}
```

**Γιατί να χρησιμοποιήσετε το Aspose.Cells αντί αυτού;**  
- Κλήση αποθήκευσης μίας γραμμής (`workbook.Save`) έναντι δεκάδων γραμμών λογικής απόδοσης.  
- Πλήρης πιστότητα για τύπους, διαγράμματα και χαρακτήρες Unicode.  
- Ενσωματωμένη υποστήριξη για ρυθμίσεις σελίδας, περιθώρια και ενσωμάτωση γραμματοσειρών.

Αν χρειάζεστε μόνο μια γρήγορη εξαγωγή και έχετε ήδη το Aspose, παραμείνετε στη μέθοδο **αποθήκευσης φύλλου εργασίας ως XPS** που παρουσιάστηκε παραπάνω.

## Συνηθισμένα Προβλήματα & Πώς να τα Αποφύγετε

| Σύμπτωμα | Πιθανή Αιτία | Διόρθωση |
|---------|--------------|----------|
| Το αρχείο XPS είναι κενό ή περιέχει μόνο μια κενή σελίδα | Δεν γράφτηκαν κελιά πριν από την αποθήκευση | Βεβαιωθείτε ότι καλείτε το `PutValue` (ή άλλη μέθοδο εγγραφής) πριν το `Save`. |
| Το “A️” εμφανίζεται ως απλό “A” | Ο προβολέας δεν υποστηρίζει επιλογέα παραλλαγής | Δοκιμάστε με το Windows 10 + XPS Viewer ή έναν σύγχρονο μετατροπέα PDF‑σε‑XPS. |
| Η αποθήκευση προκαλεί `UnauthorizedAccessException` | Ο φάκελος εξόδου είναι μόνο για ανάγνωση ή η διαδρομή είναι λανθασμένη | Επαληθεύστε ότι ο φάκελος υπάρχει και ότι η διαδικασία σας έχει δικαιώματα εγγραφής. |
| Οι γραμματοσειρές φαίνονται διαφορετικές στο XPS | Οι γραμματοσειρές δεν ενσωματώθηκαν | Ορίστε `xpsOptions.EmbedStandardFonts = true;` πριν από την αποθήκευση. |

## Πλήρες Παράδειγμα Εργασίας (Έτοιμο για Αντιγραφή‑Επικόλληση)

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook
        Workbook workbook = new Workbook();

        // 2️⃣ Grab the first worksheet
        Worksheet worksheet = workbook.Worksheets[0];

        // 3️⃣ Insert text with a variation selector (e.g., "A️")
        worksheet.Cells[0, 0].PutValue("A\uFE0F");

        // 4️⃣ Prepare default XPS save options
        XpsSaveOptions xpsOptions = new XpsSaveOptions();

        // 5️⃣ Define output path and save as XPS
        string outputPath = @"C:\Temp\variation.xps";
        workbook.Save(outputPath, xpsOptions);

        Console.WriteLine($"Workbook successfully saved as XPS at: {outputPath}");
    }
}
```

Τρέξτε το πρόγραμμα, ανοίξτε το `C:\Temp\variation.xps` και θα δείτε τον χαρακτήρα αποδομένο. Το μήνυμα στην κονσόλα επιβεβαιώνει ότι η λειτουργία ολοκληρώθηκε επιτυχώς.

## Σύνοψη

Καλύψαμε όλα όσα χρειάζεστε για να **αποθηκεύσετε ένα φύλλο εργασίας ως XPS** χρησιμοποιώντας το Aspose.Cells σε C#. Ξεκινώντας από ένα κενό workbook, εισάγαμε έναν επιλογέα παραλλαγής Unicode, διαμορφώσαμε (ή αφήσαμε τις προεπιλογές) τις επιλογές XPS και αποθηκεύσαμε το αρχείο. Εξετάσαμε επίσης μια ελαφριά εναλλακτική για **εξαγωγή Excel σε XPS** χωρίς τρίτες βιβλιοθήκες, επισημάναμε κοινά σφάλματα και σας δώσαμε ένα έτοιμο προς εκτέλεση τμήμα κώδικα.

## Τι Να Δοκιμάσετε Στη Σύννεση;

- **Πολλαπλά Φύλλα:** Επανάληψη μέσω `workbook.Worksheets` και προσθήκη του καθενός ως ξεχωριστή σελίδα XPS.  
- **Στυλ:** Εφαρμόστε γραμματοσειρές, χρώματα και περιγράμματα πριν την αποθήκευση για να δείτε πώς μεταφράζονται στη διανυσματική μορφή XPS.  
- **Ενσωμάτωση Εικόνων:** Χρησιμοποιήστε `Pictures.Add` για να τοποθετήσετε ένα λογότυπο, έπειτα εξαγωγή—ιδανικό για δημιουργία εταιρικών αναφορών.  
- **Μαζική Μετατροπή:** Συνδυάστε το απόσπασμα με έναν παρατηρητή συστήματος αρχείων για να μετατρέπετε αυτόματα κάθε νέο `.xlsx` σε φάκελο σε XPS.

Πειραματιστείτε, σπάστε πράγματα και θέστε ερωτήσεις στα σχόλια. Καλή προγραμματιστική δουλειά, και απολαύστε το καθαρό, εκτυπώσιμο αποτέλεσμα που προσφέρει το XPS!

## Τι Θα Πρέπει Να Μάθετε Στη Σύννεση;

Οι παρακάτω εκπαιδευτικές ενότητες καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε επιπλέον δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στην δική σας υλοποίηση.

- [Εξαγωγή Excel σε XPS με Aspose.Cells για Java: Οδηγός Βήμα‑Βήμα](/cells/english/java/workbook-operations/aspose-cells-java-export-excel-xps/)
- [Export Excel Xps Aspose Cells Net](/cells/german/net/workbook-operations/export-excel-xps-aspose-cells-net/)
- [Export Excel Xps Aspose Cells Net](/cells/spanish/net/workbook-operations/export-excel-xps-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}