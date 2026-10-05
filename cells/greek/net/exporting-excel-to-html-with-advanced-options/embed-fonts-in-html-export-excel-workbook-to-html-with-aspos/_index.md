---
category: general
date: 2026-06-17
description: Ενσωματώστε τις γραμματοσειρές σε HTML όταν αποθηκεύετε το βιβλίο εργασίας
  ως HTML. Μάθετε πώς να μετατρέψετε το βιβλίο εργασίας σε HTML και να εξάγετε το
  Excel HTML με ενσωματωμένες γραμματοσειρές σε λίγα βήματα.
draft: false
keywords:
- embed fonts in html
- save workbook as html
- convert workbook to html
- how to export excel html
language: el
og_description: Ενσωματώστε γραμματοσειρές σε HTML όταν αποθηκεύετε το βιβλίο εργασίας
  ως HTML. Ακολουθήστε αυτόν τον οδηγό για να μετατρέψετε το βιβλίο εργασίας σε HTML
  και μάθετε πώς να εξάγετε το Excel HTML με πλήρη υποστήριξη γραμματοσειρών.
og_title: Ενσωμάτωση γραμματοσειρών σε HTML – Εξαγωγή βιβλίου εργασίας Excel σε HTML
schemas:
- author: Aspose
  dateModified: '2026-06-17'
  description: Embed fonts in HTML while you save workbook as HTML. Learn how to convert
    workbook to HTML and export Excel HTML with embedded fonts in a few steps.
  headline: Embed Fonts in HTML – Export Excel Workbook to HTML with Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- Excel
- HTML export
title: Ενσωμάτωση γραμματοσειρών σε HTML – Εξαγωγή βιβλίου εργασίας Excel σε HTML
  με το Aspose.Cells
url: /el/net/exporting-excel-to-html-with-advanced-options/embed-fonts-in-html-export-excel-workbook-to-html-with-aspos/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ενσωμάτωση Γραμματοσειρών σε HTML – Εξαγωγή Βιβλίου Εργασίας Excel σε HTML με Aspose.Cells

Έχετε αναρωτηθεί ποτέ πώς να **ενσωματώσετε γραμματοσειρές σε HTML** όταν εξάγετε ένα φύλλο Excel; Δεν είστε οι μόνοι. Πολλοί προγραμματιστές συναντούν πρόβλημα όταν το παραγόμενο HTML εμφανίζει μια γενική sans‑serif αντί για το αρχικό στυλ του Excel. Τα καλά νέα; Με μερικές γραμμές κώδικα μπορείτε να **αποθηκεύσετε το βιβλίο εργασίας ως HTML** και να διατηρήσετε κάθε γραμματοσειρά αμετάβλητη.

Σε αυτό το tutorial θα περάσουμε από όλη τη διαδικασία **μετατροπής βιβλίου εργασίας σε HTML** χρησιμοποιώντας το Aspose.Cells για .NET, θα εξηγήσουμε γιατί η ενσωμάτωση γραμματοσειρών είναι σημαντική, και θα σας δείξουμε ακριβώς **πώς να εξάγετε Excel σε HTML** ώστε το αποτέλεσμα να μοιάζει ακριβώς με το αρχικό φύλλο. Χωρίς εξωτερικά εργαλεία, χωρίς χειροκίνητη επεξεργασία — μόνο καθαρός, εκτελέσιμος κώδικας C#.

## Προαπαιτούμενα

- .NET 6.0 ή νεότερο (το παράδειγμα λειτουργεί σε .NET Core, .NET Framework και .NET 5+)
- Aspose.Cells for .NET πακέτο NuGet (`Install-Package Aspose.Cells`)
- Βασική κατανόηση του C# και της διαχείρισης αρχείων Excel
- Προαιρετικά: ένα προσαρμοσμένο αρχείο γραμματοσειράς TrueType που θέλετε να ενσωματώσετε (π.χ., `MyFont.ttf`)

Τα έχετε όλα; Τέλεια—ας ξεκινήσουμε.

## Βήμα 1: Ρύθμιση του Έργου και Φόρτωση Βιβλίου Εργασίας Excel

Πρώτα χρειάζεται ένα αντικείμενο βιβλίου εργασίας. Μπορείτε να δημιουργήσετε ένα από το μηδέν ή να φορτώσετε ένα υπάρχον `.xlsx`. Ακολουθεί μια ελάχιστη ρύθμιση που προσθέτει επίσης μια προσαρμοσμένη γραμματοσειρά στη συλλογή στυλ του βιβλίου εργασίας.

```csharp
using Aspose.Cells;
using System.IO;

// Load an existing workbook (replace with your own path)
Workbook wb = new Workbook("SampleData.xlsx");

// OPTIONAL: Register a custom font if your sheet uses one that isn’t standard
string fontPath = Path.Combine(Directory.GetCurrentDirectory(), "MyFont.ttf");
if (File.Exists(fontPath))
{
    // Register the font with the font manager – this ensures Aspose knows about it
    FontConfigs.AddFontFile(fontPath);
}
```

*Γιατί αυτό το βήμα;* Φορτώνοντας πρώτα το βιβλίο εργασίας δίνουμε στο Aspose.Cells την ευκαιρία να εξετάσει όλα τα στυλ κελιών. Η καταχώρηση μιας προσαρμοσμένης γραμματοσειράς εγγυάται ότι η γραμματοσειρά θα βρεθεί όταν αργότερα την ενσωματώσουμε στο αρχείο HTML.

## Βήμα 2: Διαμόρφωση Επιλογών Αποθήκευσης HTML για **Ενσωμάτωση Γραμματοσειρών σε HTML**

Η μαγεία βρίσκεται στο `HtmlSaveOptions`. Ορίζοντας `EmbedFonts = true` λέει στη βιβλιοθήκη να ενσωματώσει κάθε χρησιμοποιούμενη γραμματοσειρά ως κανόνα `@font-face` κωδικοποιημένο σε Base64 μέσα στο παραγόμενο αρχείο HTML.

```csharp
// Configure HTML save options – this is where we embed fonts in HTML
HtmlSaveOptions saveOptions = new HtmlSaveOptions
{
    // Embed all referenced fonts directly into the HTML output
    EmbedFonts = true,

    // Optional: keep the original layout (useful for complex sheets)
    ExportActiveWorksheetOnly = true,

    // Optional: produce a single HTML file (no external CSS or images)
    ExportImagesAsBase64 = true
};
```

*Γιατί να ενεργοποιήσετε το `EmbedFonts`;* Χωρίς αυτό, το παραγόμενο HTML αναφέρεται σε γραμματοσειρές συστήματος, και όποιος ανοίξει το αρχείο σε μηχάνημα που δεν διαθέτει αυτές τις γραμματοσειρές θα δει εναλλακτική. Η ενσωμάτωση εγγυάται οπτική πιστότητα σε όλα τα προγράμματα περιήγησης και τις συσκευές.

## Βήμα 3: **Αποθήκευση Βιβλίου Εργασίας ως HTML** με τις Διαμορφωμένες Επιλογές

Τώρα τελικά γράφουμε το αρχείο. Η μέθοδος `Save` παίρνει τρία ορίσματα: τη διαδρομή προορισμού, τη μορφή (`SaveFormat.Html`) και τις επιλογές που μόλις διαμορφώσαμε.

```csharp
// Define the output HTML file path
string outputPath = Path.Combine(Directory.GetCurrentDirectory(), "with-fonts.html");

// Save the workbook as HTML with embedded fonts
wb.Save(outputPath, SaveFormat.Html, saveOptions);
```

Αν όλα πάνε ομαλά, θα έχετε ένα μόνο αρχείο `with-fonts.html` που περιέχει ολόκληρη τη διάταξη του υπολογιστικού φύλλου *και* τα δεδομένα της γραμματοσειράς κωδικοποιημένα απευθείας στο markup.

## Αναμενόμενο Αποτέλεσμα

Ανοίξτε το `with-fonts.html` σε οποιονδήποτε σύγχρονο περιηγητή (Chrome, Edge, Firefox). Θα πρέπει να δείτε:

- Τις ίδιες τιμές κελιών, χρώματα και περιγράμματα όπως στο αρχικό αρχείο Excel.
- Κείμενο που αποδίδεται στην ακριβή γραμματοσειρά που χρησιμοποιήσατε στο Excel, ακόμη και αν αυτή η γραμματοσειρά δεν είναι εγκατεστημένη στον υπολογιστή σας.
- Καμία εξωτερική `.css` ή αρχείο εικόνας — όλα βρίσκονται μέσα στο αρχείο HTML.

Παρακάτω υπάρχει ένα μικρό απόσπασμα του παραγόμενου μπλοκ `<style>` (η συμβολοσειρά Base64 είναι περικομμένη για συντομία):

```html
<style type="text/css">
@font-face{
    font-family:'MyCustomFont';
    src:url(data:font/truetype;charset=utf-8;base64,AAEAAAALAIAAAwAwT1Mv... ) format('truetype');
}
...
</style>
```

## Βήμα 4: Συνηθισμένα Προβλήματα & Πώς να τα Διορθώσετε

| Πρόβλημα | Γιατί Συμβαίνει | Διόρθωση |
|------|----------------|-----|
| **Έλλειψη γραμματοσειράς στο HTML** | Το αρχείο γραμματοσειράς δεν καταχωρήθηκε με `FontConfigs` πριν από την αποθήκευση. | Καλέστε `FontConfigs.AddFontFile` *πριν* δημιουργήσετε το `HtmlSaveOptions`. |
| **Τεράστιο μέγεθος αρχείου HTML** | Η ενσωμάτωση πολλών μεγάλων γραμματοσειρών μπορεί να αυξήσει το μέγεθος του αρχείου. | Ενσωματώστε μόνο τις γραμματοσειρές που χρειάζεστε πραγματικά· χρησιμοποιήστε `saveOptions.FontEmbeddingMode = FontEmbeddingMode.Subset` για να ενσωματώσετε μόνο τα χρησιμοποιούμενα γλύφους (διαθέσιμο σε νεότερες εκδόσεις του Aspose). |
| **Λανθασμένοι χαρακτήρες (π.χ., ασιατικά γλύφα)** | Η γραμματοσειρά δεν περιέχει τις απαιτούμενες περιοχές Unicode. | Βεβαιωθείτε ότι η πηγαία γραμματοσειρά υποστηρίζει τους χαρακτήρες, ή ενσωματώστε μια επιπλέον εφεδρική γραμματοσειρά. |
| **Μείωση απόδοσης σε μεγάλα βιβλία εργασίας** | Η ενσωμάτωση γραμματοσειρών προσθέτει επιπλέον φόρτο επεξεργασίας. | Εξάγετε μόνο το ενεργό φύλλο (`ExportActiveWorksheetOnly = true`) ή χωρίστε το βιβλίο εργασίας σε μικρότερα μέρη. |

## Βήμα 5: Επέκταση της Λύσης – Εξαγωγή Πολλαπλών Φύλλων Εργασίας

Αν χρειάζεστε **μετατροπή βιβλίου εργασίας σε HTML** για όλα τα φύλλα, απλώς απενεργοποιήστε το `ExportActiveWorksheetOnly`:

```csharp
saveOptions.ExportActiveWorksheetOnly = false; // Export every sheet
wb.Save("all-sheets.html", SaveFormat.Html, saveOptions);
```

Κάθε φύλλο εργασίας θα εμφανιστεί ως ξεχωριστό `<div>` στο ίδιο αρχείο HTML, εξακολουθώντας να έχει ενσωματωμένες γραμματοσειρές.

## Συμβουλή Επαγγελματία: Συνδυάστε με Προσαρμογή CSS

Μερικές φορές θέλετε πιο στενό έλεγχο του παραγόμενου markup. Το `HtmlSaveOptions` προσφέρει την ιδιότητα `CssClassPrefix` για να αποφύγετε συγκρούσεις ονομάτων κλάσεων όταν συγχωνεύετε πολλαπλές εξαγωγές HTML:

```csharp
saveOptions.CssClassPrefix = "myExcel_";
```

Τώρα κάθε παραγόμενη κλάση CSS θα ξεκινά με `myExcel_`, καθιστώντας πιο εύκολο να εφαρμόσετε το δικό σας stylesheet αργότερα.

## Σύνοψη

- **Ενσωμάτωση γραμματοσειρών σε HTML** ορίζοντας `HtmlSaveOptions.EmbedFonts = true`.
- Χρησιμοποιήστε **αποθήκευση βιβλίου εργασίας ως HTML** (`wb.Save(..., SaveFormat.Html, ...)`) για να παραγάγετε ένα ενιαίο, αυτόνομο αρχείο.
- Αυτή η μέθοδος **μετατρέπει το βιβλίο εργασίας σε HTML** διατηρώντας κάθε οπτική λεπτομέρεια, απαντώντας στην κλασική ερώτηση **πώς να εξάγετε Excel σε HTML** με πλήρη πιστότητα.
- Καταχωρήστε προσαρμοσμένες γραμματοσειρές με `FontConfigs.AddFontFile` ώστε να είναι διαθέσιμες για ενσωμάτωση.
- Ρυθμίστε επιλογές όπως `ExportImagesAsBase64` και `ExportActiveWorksheetOnly` ώστε να ταιριάζουν στις ανάγκες του έργου σας.

## Τι Ακολουθεί;

- Δοκιμάστε την εξαγωγή σε **MHTML** (`SaveFormat.Mhtml`) για ένα ακόμη πιο φορητό πακέτο.
- Εξερευνήστε τη **μετατροπή σε PDF** (`SaveFormat.Pdf`) αν χρειάζεστε μορφή έτοιμη για εκτύπωση.
- Ενσωματώστε την εξαγωγή HTML σε ένα web API ώστε οι χρήστες να μπορούν να κατεβάζουν στυλιζαρισμένα υπολογιστικά φύλλα άμεσα.

Μη διστάσετε να πειραματιστείτε — αλλάξτε γραμματοσειρές, τροποποιήστε τις επιλογές φύλλων εργασίας ή συνδυάστε πολλαπλές μορφές εξαγωγής. Η ευελιξία του Aspose.Cells σημαίνει ότι μπορείτε να προσαρμόσετε το αποτέλεσμα σε οποιοδήποτε σενάριο, από αυτοματοποιημένα dashboards αναφορών μέχρι αποσπάσματα HTML έτοιμα για email.

Καλό κώδικα, και εύχομαι το HTML σας να μοιάζει πάντα ακριβώς με το αρχικό φύλλο Excel!

## Τι Θα Πρέπει Να Μάθετε Στη Σύντομη Μελλοντική Περίοδο;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που βασίζονται στις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να Δημιουργήσετε και να Εξάγετε Excel σε HTML Χρησιμοποιώντας Aspose.Cells Java | Οδηγός Λειτουργιών Βιβλίου Εργασίας](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [Ορισμός Προεπιλεγμένης Γραμματοσειράς στη Μετατροπή Excel σε HTML με Aspose.Cells για .NET | Οδηγός Λειτουργιών Βιβλίου Εργασίας](/cells/english/net/workbook-operations/excel-html-conversion-default-font-aspose-cells-net/)
- [Πώς να Εξάγετε Excel σε HTML με Γραμμές Πλέγματος Χρησιμοποιώντας Aspose.Cells για .NET](/cells/english/net/workbook-operations/export-excel-to-html-grid-lines-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}