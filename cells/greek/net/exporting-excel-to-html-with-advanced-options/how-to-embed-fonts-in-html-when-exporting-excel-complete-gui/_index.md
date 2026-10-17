---
category: general
date: 2026-02-09
description: Μάθετε πώς να ενσωματώνετε γραμματοσειρές σε HTML όταν εξάγετε το Excel
  σε HTML χρησιμοποιώντας το Aspose.Cells. Αυτό το βήμα‑βήμα εκπαιδευτικό υλικό καλύπτει
  επίσης τη μετατροπή του Excel σε HTML και πώς να εξάγετε το Excel με ενσωματωμένες
  γραμματοσειρές.
draft: false
keywords:
- how to embed fonts
- embed fonts in html
- export excel to html
- convert excel to html
- how to export excel
language: el
og_description: Πώς να ενσωματώσετε γραμματοσειρές σε HTML κατά την εξαγωγή του Excel.
  Ακολουθήστε αυτόν τον πλήρη οδηγό για να μετατρέψετε το Excel σε HTML με ενσωματωμένες
  γραμματοσειρές χρησιμοποιώντας το Aspose.Cells.
og_title: Πώς να ενσωματώσετε γραμματοσειρές σε HTML – Οδηγός εξαγωγής Excel σε HTML
tags:
- Aspose.Cells
- C#
- Excel
- HTML
title: Πώς να ενσωματώσετε γραμματοσειρές σε HTML κατά την εξαγωγή από Excel – Πλήρης
  οδηγός
url: /el/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-in-html-when-exporting-excel-complete-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να ενσωματώσετε γραμματοσειρές σε HTML κατά την εξαγωγή Excel – Πλήρης Οδηγός

Έχετε αναρωτηθεί ποτέ **πώς να ενσωματώσετε γραμματοσειρές σε HTML** ενώ μετατρέπετε ένα βιβλίο εργασίας Excel σε μια ιστοσελίδα έτοιμη για web; Δεν είστε οι μόνοι. Πολλοί προγραμματιστές συναντούν πρόβλημα όταν το παραγόμενο HTML φαίνεται σωστό στον υπολογιστή τους, αλλά εμφανίζεται με γενικές εναλλακτικές γραμματοσειρές στον περιηγητή. Τα καλά νέα; Με μερικές γραμμές C# και τις σωστές επιλογές αποθήκευσης, μπορείτε να παραδώσετε ακριβώς την τυπογραφία που σχεδιάσατε στο Excel.

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από την εξαγωγή ενός αρχείου Excel σε HTML **με ενσωματωμένες γραμματοσειρές**, χρησιμοποιώντας το Aspose.Cells for .NET. Καθ’ οδόν θα αγγίξουμε τα βασικά του *export excel to html*, θα σας δείξουμε πώς να *convert excel to html* σε διαφορετικά σενάρια, και θα απαντήσουμε στις ακαριαίες ερωτήσεις “**how to export excel**” που εμφανίζονται σε φόρουμ.

## Τι θα μάθετε

- Μια πλήρως εκτελέσιμη εφαρμογή C# console που αποθηκεύει ένα βιβλίο εργασίας `.xlsx` ως `embedded.html`.
- Μια εξήγηση γιατί η ενσωμάτωση γραμματοσειρών είναι σημαντική για την πιστότητα μεταξύ περιηγητών.
- Συμβουλές για τη διαχείριση αδειών γραμματοσειρών, μεγάλων βιβλίων εργασίας και απόδοσης.
- Γρήγορες ενδείξεις για εναλλακτικούς τρόπους *export excel to html* αν δεν χρησιμοποιείτε Aspose.Cells.

### Προαπαιτούμενα

- .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί επίσης σε .NET Framework 4.7+).
- Aspose.Cells for .NET εγκατεστημένο μέσω NuGet (`Install-Package Aspose.Cells`).
- Βασική κατανόηση της C# και του μοντέλου αντικειμένων του Excel.
- Μια γραμματοσειρά TrueType (`.ttf`) ή OpenType (`.otf`) που έχετε το δικαίωμα να ενσωματώσετε.

Καμία βαριά εγκατάσταση, χωρίς COM interop, μόνο μερικά πακέτα NuGet και έναν επεξεργαστή κειμένου.

---

## Πώς να ενσωματώσετε γραμματοσειρές σε HTML – Βήμα 1: Προετοιμάστε το Βιβλίο Εργασίας

Πριν μπορέσουμε να πούμε στο Aspose.Cells να ενσωματώσει γραμματοσειρές, χρειαζόμαστε ένα βιβλίο εργασίας που πραγματικά χρησιμοποιεί μια προσαρμοσμένη γραμματοσειρά. Ας δημιουργήσουμε ένα μικρό βιβλίο εργασίας στη μνήμη, εφαρμόζοντας μια μη‑συστημική γραμματοσειρά σε ένα κελί, και να το αποθηκεύσουμε.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Saving;   // Needed for HtmlSaveOptions

// Step 1: Create a new workbook and access the first worksheet
Workbook workbook = new Workbook();
Worksheet sheet = workbook.Worksheets[0];

// Step 2: Insert some text and apply a custom font (e.g., "Comic Sans MS")
Style style = workbook.CreateStyle();
style.Font.Name = "Comic Sans MS";   // This font is usually not available on all browsers
style.Font.Size = 14;
style.Font.IsBold = true;

// Apply the style to cell A1
Cell cell = sheet.Cells["A1"];
cell.PutValue("Hello, embedded fonts!");
cell.SetStyle(style);

// Save the workbook as an intermediate .xlsx (optional, just for inspection)
workbook.Save("sample.xlsx");
```

**Γιατί είναι σημαντικό:** Αν το βιβλίο εργασίας δεν αναφέρει ποτέ μια προσαρμοσμένη γραμματοσειρά, δεν υπάρχει τίποτα για το Aspose.Cells να ενσωματώσει. Ορίζοντας ρητά το `style.Font.Name`, αναγκάζουμε τον εξαγωγέα να ψάξει το αρχείο γραμματοσειράς στο σύστημα και να το συμπεριλάβει στο HTML αποτέλεσμα.

> **Pro tip:** Δοκιμάστε πάντα με μια γραμματοσειρά που δεν είναι σίγουρο ότι υπάρχει στις μηχανές-στόχο. Συστημικές γραμματοσειρές όπως η Arial δεν θα δείξουν τη λειτουργία ενσωμάτωσης.

## Πώς να ενσωματώσετε γραμματοσειρές σε HTML – Βήμα 2: Διαμορφώστε τις Επιλογές Αποθήκευσης HTML

Τώρα έρχεται η μαγική γραμμή που απαντά στην κύρια ερώτηση: *πώς να ενσωματώσετε γραμματοσειρές σε HTML*.

```csharp
// Step 3: Create HtmlSaveOptions and enable font embedding
HtmlSaveOptions htmlOptions = new HtmlSaveOptions
{
    // Setting this flag tells Aspose.Cells to embed all referenced fonts as base‑64 data URIs
    EmbedFonts = true,

    // Optional: Reduce file size by embedding only the characters actually used
    EmbedFontSubset = true,

    // Optional: Choose a folder for external resources (images, CSS)
    ExportImagesAsBase64 = true
};
```

- `EmbedFonts = true` κάνει το βαρέως εργασίας μέρος· σαρώνει το βιβλίο εργασίας για οποιεσδήποτε αναφορές γραμματοσειρών, εντοπίζει τα αντίστοιχα αρχεία `.ttf`/`.otf` και τα ενσωματώνει απευθείας στο παραγόμενο HTML `<style>` block.
- `EmbedFontSubset = true` είναι ενισχυτής απόδοσης—συμπεριλαμβάνονται μόνο τα γλύφους που χρησιμοποιούνται πραγματικά, κρατώντας το τελικό HTML ελαφρύ.
- `ExportImagesAsBase64` είναι χρήσιμο όταν έχετε επίσης γραφήματα ή εικόνες· όλα καταλήγουν σε ένα μόνο αρχείο, ιδανικό για email ή γρήγορες παρουσιάσεις.

## Πώς να ενσωματώσετε γραμματοσειρές σε HTML – Βήμα 3: Αποθηκεύστε το Βιβλίο Εργασίας

Τέλος, καλούμε το `Save` με τις επιλογές που μόλις διαμορφώσαμε.

```csharp
// Step 4: Export the workbook to HTML with embedded fonts
string outputPath = "embedded.html";
workbook.Save(outputPath, htmlOptions);

Console.WriteLine($"Workbook exported with embedded fonts to: {outputPath}");
```

Μετά την ολοκλήρωση της εκτέλεσης, ανοίξτε το `embedded.html` σε οποιονδήποτε σύγχρονο περιηγητή. Θα πρέπει να δείτε το κείμενο να αποδίδεται σε *Comic Sans MS* ακόμη και αν η γραμματοσειρά δεν είναι εγκατεστημένη τοπικά. Ο περιηγητής διαβάζει το `<style>` block που περιέχει έναν κανόνα `@font-face` με ένα payload `data:font/ttf;base64,...`—ακριβώς αυτό που θέλαμε.

![HTML output with embedded fonts](embed-fonts-html.png "Screenshot showing how to embed fonts in HTML")

*Image alt text:* **πώς να ενσωματώσετε γραμματοσειρές σε HTML** – στιγμιότυπο της παραγόμενης σελίδας με την προσαρμοσμένη γραμματοσειρά εφαρμοσμένη.

---

## Export Excel to HTML – Εναλλακτικές Προσεγγίσεις

Αν δεν είστε δεσμευμένοι στο Aspose.Cells, υπάρχουν και άλλοι τρόποι *export excel to html*:

| Library / Tool | Font Embedding Support | Quick Note |
|----------------|-----------------------|------------|
| **ClosedXML** | No built‑in font embedding | Δημιουργεί απλό HTML· πρέπει να προσθέσετε χειροκίνητα `@font-face`. |
| **EPPlus**    | No font embedding | Κατάλληλο για πίνακες δεδομένων, αλλά χάνει το στυλ. |
| **Office Interop** | Can embed fonts via `SaveAs` with `xlHtmlStatic` | Απαιτεί εγκατεστημένο Excel στον server—συνήθως αποθαρρύνεται. |
| **LibreOffice CLI** | Can embed fonts with `--embed-fonts` flag | Λειτουργεί δια-πλατφόρμα αλλά προσθέτει βαριά εξάρτηση. |

Όταν χρειάζεστε μια αξιόπιστη λύση server‑side χωρίς εγκατεστημένο Office, το Aspose.Cells παραμένει η πιο απλή διαδρομή για *convert excel to html* με ενσωματωμένες γραμματοσειρές.

## Πώς να Εξάγετε Excel – Συνηθισμένα Πιθανά Σφάλματα & Πώς να τα Διορθώσετε

1. **Missing Font Files** – Αν η στοχευμένη γραμματοσειρά δεν υπάρχει στη μηχανή που εκτελεί τον κώδικα, το Aspose.Cells παραλείπει σιωπηρά την ενσωμάτωση και το HTML επιστρέφει σε γενική γραμματοσειρά.  
   *Διόρθωση:* Εγκαταστήστε τη γραμματοσειρά στον server ή αντιγράψτε τα αρχεία `.ttf`/`.otf` δίπλα στο εκτελέσιμο σας και ορίστε το `FontSources` χειροκίνητα:

   ```csharp
   FontSources.AddFolder(@"C:\MyFonts");
   ```

2. **License Restrictions** – Ορισμένες εμπορικές γραμματοσειρές απαγορεύουν την ενσωμάτωση.  
   *Διόρθωση:* Ελέγξτε το EULA της γραμματοσειράς. Αν η ενσωμάτωση απαγορεύεται, επιλέξτε άλλη γραμματοσειρά ή φιλοξενήστε το αρχείο γραμματοσειράς με τη σωστή άδεια.

3. **Large Workbooks** – Η ενσωμάτωση πολλών γραμματοσειρών μπορεί να αυξήσει δραματικά το μέγεθος του HTML.  
   *Διόρθωση:* Χρησιμοποιήστε `EmbedFontSubset = true` (όπως δείξαμε παραπάνω) ή περιορίστε το βιβλίο εργασίας μόνο στα φύλλα που χρειάζεστε πριν την εξαγωγή.

4. **Browser Compatibility** – Παλαιοί περιηγητές (IE 8 και κάτω) δεν υποστηρίζουν base‑64 `@font-face`.  
   *Διόρθωση:* Παρέχετε έναν εναλλακτικό κανόνα CSS που αναφέρεται σε μια web‑διαθέσιμη έκδοση `.woff` της γραμματοσειράς.

---

## Convert Excel to HTML – Επαλήθευση του Αποτελέσματος

Αφού τρέξετε το παράδειγμα, ανοίξτε το `embedded.html` και ψάξτε για ένα `<style>` block που αρχίζει ως εξής:

```html
<style type="text/css">
@font-face {
    font-family: 'Comic Sans MS';
    src: url('data:font/ttf;base64,AAEAAAALAIAAAwAwT1MvMg8S...') format('truetype');
}
...
</style>
```

Αν δείτε το URL `data:`, η ενσωμάτωση πέτυχε. Το σώμα της σελίδας θα περιέχει κάτι παρόμοιο με:

```html
<div class="c0">Hello, embedded fonts!</div>
```

Το κείμενο θα πρέπει να αποδίδεται ακριβώς όπως στο Excel, ανεξάρτητα από τις εγκατεστημένες γραμματοσειρές του πελάτη.

---

## Συχνές Ερωτήσεις (FAQs)

**Q: Λειτουργεί αυτό με τύπους του Excel;**  
A: Απόλυτα. Οι τύποι αξιολογούνται πριν δημιουργηθεί το HTML, έτσι οι εμφανιζόμενες τιμές είναι στατικές συμβολοσειρές—όπως σε μια κανονική εξαγωγή.

**Q: Μπορώ να ενσωματώσω γραμματοσειρές όταν εξάγω σε πακέτο ZIP αντί για ένα μόνο αρχείο HTML;**  
A: Ναι. Ορίστε `htmlOptions.ExportToSingleFile = false` και το Aspose.Cells θα δημιουργήσει έναν φάκελο με ξεχωριστά CSS και αρχεία γραμματοσειρών, κάτι που προτιμούν ορισμένες ομάδες για έλεγχο εκδόσεων.

**Q: Τι γίνεται αν χρειαστεί να ενσωματώσω

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}