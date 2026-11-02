---
category: general
date: 2026-05-23
description: Ενσωματώστε γραμματοσειρές σε HTML όταν εξάγετε το Excel σε HTML χρησιμοποιώντας
  το Aspose.Cells. Οδηγός βήμα‑βήμα για τη μετατροπή του υπολογιστικού φύλλου σε HTML
  με ενσωματωμένες γραμματοσειρές.
draft: false
keywords:
- embed fonts in html
- export excel to html
- convert spreadsheet to html
- save workbook as html
- how to embed fonts html
language: el
og_description: Ενσωματώστε γραμματοσειρές σε HTML κατά την εξαγωγή του Excel σε HTML.
  Μάθετε πώς να μετατρέψετε το φύλλο εργασίας σε HTML με ενσωματωμένες γραμματοσειρές
  σε λίγα εύκολα βήματα.
og_title: Ενσωμάτωση γραμματοσειρών σε HTML – Εξαγωγή Excel σε HTML με C#
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: Embed fonts in HTML when you export Excel to HTML using Aspose.Cells.
    Step‑by‑step guide to convert spreadsheet to HTML with embedded fonts.
  headline: Embed fonts in HTML – Export Excel to HTML with C#
  type: TechArticle
- description: Embed fonts in HTML when you export Excel to HTML using Aspose.Cells.
    Step‑by‑step guide to convert spreadsheet to HTML with embedded fonts.
  name: Embed fonts in HTML – Export Excel to HTML with C#
  steps:
  - name: 1️⃣ **What if my workbook uses a custom font that isn’t installed on the
      server?**
    text: Aspose.Cells can only embed fonts that are available to the runtime. Install
      the `.ttf` or `.otf` file on the machine running the conversion, or copy it
      into the project directory and register it via `System.Drawing.Text.PrivateFontCollection`
      before invoking the save operation.
  - name: 2️⃣ **Will embedding increase the file size dramatically?**
    text: Yes, each embedded font is Base64‑encoded, which adds roughly 33 % overhead.
      If the workbook uses many large fonts, consider enabling `EmbedOnlyUsedFonts
      = true` to limit the payload to fonts actually referenced in the sheet.
  - name: 3️⃣ **Can I still export images separately?**
    text: Setting `ExportImagesAsBase64 = true` (as shown above) inlines images, making
      the HTML truly self‑contained. If you prefer external image files, set this
      property to `false` and specify `ExportImagesFolder` to control the output folder.
  - name: 4️⃣ **Is this approach compatible with older browsers?**
    text: Most modern browsers (Chrome, Edge, Firefox, Safari) support Base64‑encoded
      `@font-face`. Internet Explorer 11 also works, but you might need to ensure
      the MIME type is correct. For legacy support, consider providing a fallback
      font stack in your CSS.
  - name: 5️⃣ **How does this differ from a simple “export excel to html” without
      embedding?**
    text: A plain export writes the text using generic web fonts (`Arial`, `Helvetica`,
      etc.). The visual layout may shift, especially for corporate reports that rely
      on a brand‑specific typeface. Embedding removes that uncertainty.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Ενσωμάτωση γραμματοσειρών σε HTML – Εξαγωγή Excel σε HTML με C#
url: /el/net/exporting-excel-to-html-with-advanced-options/embed-fonts-in-html-export-excel-to-html-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ενσωμάτωση γραμματοσειρών σε HTML – Εξαγωγή Excel σε HTML με C#

Αναρωτηθήκατε ποτέ πώς να **ενσωματώσετε γραμματοσειρές σε HTML** ενώ εξάγετε ένα βιβλίο εργασίας Excel; Δεν είστε μόνοι. Όταν μοιράζεστε ένα λογιστικό φύλλο ως ιστοσελίδα, η έλλειψη γραμματοσειρών μπορεί να μετατρέψει μια επαγγελματική αναφορά σε ακατάστατο χάος—ιδιαίτερα αν ο θεατής δεν έχει εγκατεστημένη τη αρχική γραμματοσειρά.

Σε αυτό το σεμινάριο θα περάσουμε βήμα‑βήμα από μια πλήρη, έτοιμη προς εκτέλεση λύση που σας δείχνει ακριβώς **πώς να ενσωματώσετε γραμματοσειρές σε HTML** χρησιμοποιώντας το Aspose.Cells για .NET. Στο τέλος θα μπορείτε να **εξάγετε Excel σε HTML**, **μετατρέψετε λογιστικό φύλλο σε HTML**, και **αποθηκεύσετε το βιβλίο εργασίας ως HTML** με τις γραμματοσειρές ενσωματωμένες απευθείας στο αρχείο.

---

## Τι Θα Μάθετε

- Ο λόγος για τον οποίο οι ενσωματωμένες γραμματοσειρές είναι σημαντικές για τις εξαγωγές Excel μέσω web.  
- Πώς να ρυθμίσετε το `HtmlSaveOptions` ώστε να ενεργοποιήσετε τη σημαία `EmbedFonts`.  
- Ένα πλήρες πρόγραμμα C# που φορτώνει ένα βιβλίο εργασίας, εφαρμόζει τις ρυθμίσεις και γράφει ένα αρχείο HTML.  
- Συμβουλές για τη διαχείριση προσαρμοσμένων γραμματοσειρών, τη συμβατότητα εκδόσεων και την αντιμετώπιση κοινών προβλημάτων.  

Δεν απαιτείται προηγούμενη εμπειρία με το Aspose.Cells, αλλά θα πρέπει να έχετε βασική κατανόηση της ανάπτυξης σε C# και .NET.

---

## Προαπαιτούμενα

| Απαίτηση | Γιατί είναι σημαντικό |
|----------|------------------------|
| **.NET 6.0 ή νεότερο** | Σύγχρονο runtime· παλαιότερα frameworks μπορεί να μην περιλαμβάνουν τις πιο πρόσφατες δυνατότητες του Aspose.Cells. |
| **Aspose.Cells for .NET** (πακέτο NuGet `Aspose.Cells`) | Παρέχει την κλάση `HtmlSaveOptions` που χρειαζόμαστε. |
| **Μια γραμματοσειρά TrueType ή OpenType** που θέλετε να ενσωματώσετε (π.χ., `Arial.ttf`) | Μόνο αυτές οι μορφές γραμματοσειρών μπορούν να ενσωματωθούν στο αρχείο HTML. |
| **Ένα IDE** (Visual Studio, Rider, VS Code) | Διευκολύνει την εκτέλεση και την αποσφαλμάτωση του παραδείγματος. |

Αν δεν έχετε εγκαταστήσει ακόμη το πακέτο NuGet, εκτελέστε:

```bash
dotnet add package Aspose.Cells
```

---

## Βήμα 1: Φορτώστε το Βιβλίο Εργασίας που Θέλετε να Μετατρέψετε

Πρώτα, χρειαζόμαστε μια παρουσία του `Workbook`. Μπορείτε να φορτώσετε ένα υπάρχον αρχείο `.xlsx`, να δημιουργήσετε ένα από το μηδέν, ή ακόμη και να αντλήσετε δεδομένα από μια βάση δεδομένων. Ακολουθεί ένα ελάχιστο παράδειγμα που ανοίγει ένα αρχείο με όνομα `Sample.xlsx` από το φάκελο του έργου:

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load the source Excel file
        var workbook = new Workbook("Sample.xlsx");
        // Continue with HTML conversion...
```

> **Γιατί αυτό το βήμα;**  
> Το αντικείμενο `Workbook` είναι το σημείο εισόδου για όλες τις λειτουργίες του Aspose.Cells. Χωρίς αυτό δεν μπορείτε να έχετε πρόσβαση στα φύλλα, τα στυλ ή τα δεδομένα που τελικά θα μετατραπούν σε HTML.

---

## Βήμα 2: Διαμορφώστε τις Επιλογές Αποθήκευσης HTML για **Ενσωμάτωση Γραμματοσειρών σε HTML**

Τώρα έρχεται η μαγική γραμμή που απαντά στην ερώτηση «πώς να ενσωματώσετε γραμματοσειρές html». Δημιουργούμε μια παρουσία του `HtmlSaveOptions` και ορίζουμε το `EmbedFonts` σε `true`. Αυτό λέει στη βιβλιοθήκη να ενσωματώνει τα δεδομένα της γραμματοσειράς ως κανόνες CSS `@font-face` κωδικοποιημένους σε Base64.

```csharp
        // Step 2: Set up HTML save options with embedded fonts
        var htmlOptions = new HtmlSaveOptions
        {
            // This flag ensures fonts are written directly into the HTML file
            EmbedFonts = true,

            // Optional: you can control whether to embed only used fonts
            // EmbedOnlyUsedFonts = true,

            // Optional: control the output folder for external resources
            ExportImagesAsBase64 = true
        };
```

> **Γιατί να ενεργοποιήσετε το `EmbedFonts`;**  
> Όταν το παραγόμενο HTML ανοίξει σε μηχάνημα που δεν διαθέτει την αρχική γραμματοσειρά, το πρόγραμμα περιήγησης θα επιστρέψει σε μια γενική γραμματοσειρά. Η ενσωμάτωση εγγυάται οπτική πιστότητα σε όλες τις πλατφόρμες.

---

## Βήμα 3: Αποθηκεύστε το Βιβλίο Εργασίας ως HTML

Με τις επιλογές έτοιμες, καλούμε το `Workbook.Save`, περνώντας το επιθυμητό όνομα αρχείου και το αντικείμενο `HtmlSaveOptions`. Η βιβλιοθήκη κάνει το σκληρό έργο—μετατρέπει τα κελιά, τους τύπους και τα στυλ σε HTML markup, και στη συνέχεια τοποθετεί τα δεδομένα της γραμματοσειράς μέσα σε ετικέτες `<style>`.

```csharp
        // Step 3: Export the workbook to HTML with embedded fonts
        workbook.Save("output.html", htmlOptions);

        // Inform the user
        Console.WriteLine("Workbook successfully saved as HTML with embedded fonts.");
    }
}
```

> **Τι θα δείτε:**  
> Ανοίξτε το `output.html` σε οποιοδήποτε σύγχρονο πρόγραμμα περιήγησης και θα παρατηρήσετε την ακριβώς ίδια τυπογραφία όπως στο αρχικό αρχείο Excel, ακόμη και αν ο θεατής δεν έχει εγκατεστημένη τη γραμματοσειρά τοπικά.

---

## Πλήρες Παράδειγμα Λειτουργίας

Συνδυάζοντας όλα τα παραπάνω, εδώ είναι το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε‑επικολλήσετε σε ένα κονσολικό έργο:

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source workbook
        var workbook = new Workbook("Sample.xlsx");

        // 2️⃣ Configure HTML save options to embed fonts
        var htmlOptions = new HtmlSaveOptions
        {
            EmbedFonts = true,
            ExportImagesAsBase64 = true,
            // You can also set ExportActiveWorksheetOnly = true if you only need one sheet
        };

        // 3️⃣ Save the workbook as HTML
        workbook.Save("output.html", htmlOptions);

        Console.WriteLine("✅ Workbook saved as HTML with embedded fonts.");
    }
}
```

Εκτελέστε το πρόγραμμα (`dotnet run`), μετά ανοίξτε το `output.html`. Θα πρέπει να δείτε ένα πιστό αντίγραφο του αρχικού λογιστικού φύλλου, με τις ακριβείς γραμματοσειρές που χρησιμοποιήσατε.

![Παράδειγμα εξόδου ενσωματωμένων γραμματοσειρών σε HTML](embed-fonts-html.png "Στιγμιότυπο οθόνης που δείχνει το αρχείο HTML με ενσωματωμένες γραμματοσειρές")

*Κείμενο alt εικόνας: ενσωμάτωση γραμματοσειρών σε html – στιγμιότυπο της παραγόμενης σελίδας HTML που διατηρεί τις αρχικές γραμματοσειρές του λογιστικού φύλλου.*

---

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

### 1️⃣ **Τι γίνεται αν το βιβλίο εργασίας μου χρησιμοποιεί προσαρμοσμένη γραμματοσειρά που δεν είναι εγκατεστημένη στον διακομιστή;**  
Το Aspose.Cells μπορεί να ενσωματώσει μόνο γραμματοσειρές που είναι διαθέσιμες στο runtime. Εγκαταστήστε το αρχείο `.ttf` ή `.otf` στο μηχάνημα που εκτελεί τη μετατροπή, ή αντιγράψτε το στον κατάλογο του έργου και καταχωρίστε το μέσω του `System.Drawing.Text.PrivateFontCollection` πριν καλέσετε τη λειτουργία αποθήκευσης.

### 2️⃣ **Θα αυξήσει η ενσωμάτωση το μέγεθος του αρχείου σημαντικά;**  
Ναι, κάθε ενσωματωμένη γραμματοσειρά κωδικοποιείται σε Base64, προσθέτοντας περίπου 33 % επιπλέον βάρος. Αν το βιβλίο εργασίας χρησιμοποιεί πολλές μεγάλες γραμματοσειρές, σκεφτείτε να ενεργοποιήσετε το `EmbedOnlyUsedFonts = true` για να περιορίσετε το φορτίο μόνο στις γραμματοσειρές που χρησιμοποιούνται πραγματικά στο φύλλο.

### 3️⃣ **Μπορώ ακόμη να εξάγω τις εικόνες ξεχωριστά;**  
Ορίζοντας το `ExportImagesAsBase64 = true` (όπως φαίνεται παραπάνω) ενσωματώνει τις εικόνες, κάνοντας το HTML πραγματικά αυτόνομο. Αν προτιμάτε εξωτερικά αρχεία εικόνας, ορίστε αυτήν την ιδιότητα σε `false` και καθορίστε το `ExportImagesFolder` για να ελέγξετε το φάκελο εξόδου.

### 4️⃣ **Είναι αυτή η προσέγγιση συμβατή με παλαιότερα προγράμματα περιήγησης;**  
Τα περισσότερα σύγχρονα προγράμματα περιήγησης (Chrome, Edge, Firefox, Safari) υποστηρίζουν `@font-face` κωδικοποιημένο σε Base64. Το Internet Explorer 11 λειτουργεί επίσης, αλλά ίσως χρειαστεί να διασφαλίσετε ότι ο τύπος MIME είναι σωστός. Για υποστήριξη παλαιών εκδόσεων, σκεφτείτε να παρέχετε μια εναλλακτική στοίβα γραμματοσειρών στο CSS σας.

### 5️⃣ **Πώς διαφέρει αυτό από μια απλή «εξαγωγή excel σε html» χωρίς ενσωμάτωση;**  
Μια απλή εξαγωγή γράφει το κείμενο χρησιμοποιώντας γενικές γραμματοσειρές web (`Arial`, `Helvetica`, κ.λπ.). Η οπτική διάταξη μπορεί να μετατοπιστεί, ειδικά για εταιρικές αναφορές που βασίζονται σε μια γραμματοσειρά συγκεκριμένης μάρκας. Η ενσωμάτωση αφαιρεί αυτήν την αβεβαιότητα.

---

## Επαγγελματικές Συμβουλές & Καλές Πρακτικές

- **Κάντε caching το HTML** αν δημιουργείτε την ίδια αναφορά επανειλημμένα. Η διαδικασία μετατροπής, αν και γρήγορη, καταναλώνει ακόμη κύκλους CPU.  
- **Επικυρώστε το αποτέλεσμα** με έναν επικυρωτή HTML (π.χ., W3C validator) για να εντοπίσετε τυχόν ανεπιθύμητο markup που θα μπορούσε να διακόψει πελάτες email.  
- **Συνδυάστε με ελαχιστοποίηση CSS** αν σκοπεύετε να σερβίρετε το HTML μέσω web. Τα ενσωματωμένα δεδομένα γραμματοσειράς είναι ήδη συμπιεσμένα, αλλά το περιβάλλον CSS μπορεί να περικοπεί.  
- **Προσοχή στην άδεια**: Το Aspose.Cells απαιτεί έγκυρη άδεια για χρήση σε παραγωγή· διαφορετικά, θα εμφανιστεί υδατογράφημα στην έξοδο HTML.  
- **Δοκιμάστε σε πολλαπλές συσκευές**—ιδιαίτερα σε κινητά προγράμματα περιήγησης—για να διασφαλίσετε ότι οι ενσωματωμένες γραμματοσειρές αποδίδουν σωστά σε διαφορετικές πυκνότητες οθόνης.

---

## Συμπέρασμα

Τώρα έχετε μια πλήρη, αντιγραφή‑επικόλληση λύση για **ενσωμάτωση γραμματοσειρών σε HTML** όταν **εξάγετε Excel σε HTML**, **μετατρέπετε λογιστικό φύλλο σε HTML**, ή απλώς **αποθηκεύετε το βιβλίο εργασίας ως HTML** με πλήρη τυπογραφική πιστότητα. Με την ενεργοποίηση της σημαίας `EmbedFonts` στο `HtmlSaveOptions`, εξαλείφετε το εφιαλτικό πρόβλημα «έλλειψης γραμματοσειράς» και παραδίδετε μια επαγγελματική, αυτόνομη ιστοσελίδα σε οποιονδήποτε κοινό.

Έτοιμοι για την επόμενη πρόκληση; Δοκιμάστε να προσθέσετε **διαδραστικά διαγράμματα** στην εξαγωγή HTML, ή πειραματιστείτε με **μετατροπή σε PDF** για να δείτε πώς συμπεριφέρονται οι ενσωματωμένες γραμματοσειρές σε άλλη μορφή. Το ίδιο μοτίβο `HtmlSaveOptions` ισχύει—απλώς αλλάξτε τον τύπο εξόδου.

Καλή προγραμματιστική δουλειά, και εύχομαι τα λογιστικά σας φύλλα να φαίνονται πάντα ακριβώς όπως τα θέλετε—ανεξάρτητα από το πού προβάλλονται!

## Σχετικά Μαθήματα

- [Μετατροπή Excel σε HTML σε Java χρησιμοποιώντας Aspose.Cells: Οδηγός βήμα‑βήμα](/cells/english/java/workbook-operations/convert-excel-html-aspose-cells-java/)
- [Εξαγωγή Excel σε HTML χρησιμοποιώντας Aspose.Cells Java: Οδηγός βήμα‑βήμα](/cells/english/java/workbook-operations/export-excel-html-aspose-cells-java/)
- [Μετατροπή Excel σε HTML με Tooltips χρησιμοποιώντας Aspose.Cells Java: Αναλυτικός Οδηγός](/cells/english/java/workbook-operations/excel-to-html-conversion-with-tooltips-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}