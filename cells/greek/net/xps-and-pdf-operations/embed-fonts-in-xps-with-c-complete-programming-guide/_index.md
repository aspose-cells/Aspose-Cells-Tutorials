---
category: general
date: 2026-06-17
description: Ενσωματώστε γραμματοσειρές σε XPS χρησιμοποιώντας C# και Aspose.PDF.
  Μάθετε το XpsSaveOptions, την ενσωμάτωση γραμματοσειρών και την εξαγωγή XPS σε λίγα
  λεπτά.
draft: false
keywords:
- embed fonts in xps
- XpsSaveOptions
- Aspose.PDF for .NET
- C# XPS export
- font embedding
language: el
og_description: Ενσωμάτωση γραμματοσειρών σε XPS χρησιμοποιώντας το Aspose.PDF για
  .NET. Αυτό το σεμινάριο δείχνει πώς να διαμορφώσετε το XpsSaveOptions, να ενσωματώσετε
  γραμματοσειρές και να δημιουργήσετε αρχεία XPS σε C#.
og_title: Ενσωμάτωση γραμματοσειρών σε XPS με C# – Οδηγός βήμα‑προς‑βήμα
schemas:
- author: Aspose
  dateModified: '2026-06-17'
  description: Embed fonts in XPS using C# and Aspose.PDF. Learn XpsSaveOptions, font
    embedding, and XPS export in minutes.
  headline: Embed Fonts in XPS with C# – Complete Programming Guide
  type: TechArticle
tags:
- C#
- XPS
- font embedding
- Aspose.PDF
title: Ενσωμάτωση γραμματοσειρών σε XPS με C# – Πλήρης οδηγός προγραμματισμού
url: /el/net/xps-and-pdf-operations/embed-fonts-in-xps-with-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ενσωμάτωση Γραμματοσειρών σε XPS με C# – Πλήρης Οδηγός Προγραμματισμού

Έχετε χρειαστεί ποτέ να **ενσωματώσετε γραμματοσειρές σε XPS** αλλά δεν ήξερες ποια flags του API πρέπει να ενεργοποιήσεις; Δεν είστε μόνοι—πολλοί προγραμματιστές αντιμετωπίζουν αυτό το εμπόδιο όταν εξάγουν PDFs ή άλλα έγγραφα σε μορφή XPS. Τα καλά νέα; Με λίγες γραμμές C# και τις σωστές επιλογές, μπορείτε να κλειδώσετε τις γραμματοσειρές μέσα στο αρχείο XPS και να εξασφαλίσετε συνεπή απόδοση παντού.

Σε αυτόν τον οδηγό θα περάσουμε βήμα‑βήμα τις ακριβείς ρυθμίσεις του **XpsSaveOptions**, θα ενεργοποιήσουμε την **ενσωμάτωση γραμματοσειρών**, και θα αποθηκεύσουμε ένα έγγραφο ως XPS χρησιμοποιώντας **Aspose.PDF for .NET**. Στο τέλος θα έχετε ένα έτοιμο‑για‑εκτέλεση snippet που μπορείτε να ενσωματώσετε σε οποιοδήποτε .NET project.

## Τι Θα Μάθετε

- Γιατί η ενσωμάτωση γραμματοσειρών σε XPS είναι σημαντική για διασταυρούμενη πιστότητα.  
- Πώς να ρυθμίσετε το `XpsSaveOptions` και να ενεργοποιήσετε τη σημαία `EmbedFonts`.  
- Ο πλήρης κώδικας C# που απαιτείται για τη δημιουργία αρχείου XPS με ενσωματωμένες γραμματοσειρές.  
- Συνηθισμένα προβλήματα (γραμματοσειρές με περιορισμούς άδειας, ελλιπείς γλύφους) και πώς να τα αποφύγετε.  

**Προαπαιτούμενα**: .NET 6+ (ή .NET Framework 4.6+), μια αναφορά στο πακέτο NuGet Aspose.PDF for .NET, και βασική κατανόηση της C#. Δεν απαιτούνται άλλα εξωτερικά εργαλεία.

---

## Βήμα 1: Εγκατάσταση Aspose.PDF for .NET

Πριν γράψουμε κώδικα, βεβαιωθείτε ότι η βιβλιοθήκη Aspose.PDF είναι διαθέσιμη στο project σας.

```bash
dotnet add package Aspose.PDF --version 23.12
```

> **Pro tip:** Αν χρησιμοποιείτε Visual Studio, μπορείτε επίσης να χρησιμοποιήσετε το UI του NuGet Package Manager—απλώς ψάξτε για “Aspose.PDF”.

## Βήμα 2: Δημιουργία Απλού PDF Εγγράφου

Θα ξεκινήσουμε με ένα μικρό PDF που περιέχει μια μόνο γραμμή κειμένου. Αυτό το έγγραφο θα αποθηκευτεί αργότερα ως XPS με ενσωματωμένες γραμματοσειρές.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Create a new PDF document
Document pdfDoc = new Document();

// Add a page
Page page = pdfDoc.Pages.Add();

// Add a TextFragment with a custom font (e.g., Arial)
TextFragment tf = new TextFragment("Hello, XPS world!")
{
    // Use a TrueType font that you know is installed
    TextState = { Font = FontRepository.FindFont("Arial") }
};
page.Paragraphs.Add(tf);
```

*Γιατί είναι σημαντικό*: Η χρήση μιας γνωστής γραμματοσειράς TrueType εξασφαλίζει ότι οι γλύφοι είναι διαθέσιμοι για ενσωμάτωση. Αν επιλέξετε γραμματοσειρά που δεν είναι εγκατεστημένη στο σύστημα, το Aspose θα επιστρέψει σε προεπιλογή, και το XPS μπορεί να μην περιέχει το επιθυμητό στυλ.

## Βήμα 3: Ρύθμιση XpsSaveOptions για Ενσωμάτωση Γραμματοσειρών

Αυτή είναι η καρδιά του tutorial—το αντικείμενο `XpsSaveOptions`. Ορίζοντας `EmbedFonts = true` λέτε στο Aspose να συμπεριλάβει κάθε αναφερόμενη γραμματοσειρά απευθείας στο πακέτο XPS.

```csharp
using Aspose.Pdf.XpsConversion;

// Configure XPS save options
XpsSaveOptions saveOptions = new XpsSaveOptions
{
    // This flag performs the actual font embedding
    EmbedFonts = true,

    // Optional: compress the XPS for smaller size
    Compression = CompressionType.Zip,

    // Optional: preserve the original PDF's layout
    PreserveFormFields = true
};
```

> **Γιατί να ενεργοποιήσετε τη συμπίεση;** Ένα αρχείο XPS είναι ουσιαστικά ένα αρχείο ZIP που περιέχει XML και πόρους. Η ενεργοποίηση του `Compression` μπορεί να μειώσει το τελικό μέγεθος έως και 30 % χωρίς να επηρεάσει την ενσωμάτωση γραμματοσειρών.

## Βήμα 4: Αποθήκευση του Εγγράφου ως XPS με Ενσωματωμένες Γραμματοσειρές

Τώρα συνδέουμε όλα τα παραπάνω—αποθηκεύουμε το PDF ως XPS χρησιμοποιώντας τις επιλογές που ορίσαμε.

```csharp
// Define the output path (make sure the directory exists)
string outputPath = Path.Combine(Environment.CurrentDirectory, "EmbeddedFontExample.xps");

// Save the PDF as XPS, embedding all fonts
pdfDoc.Save(outputPath, SaveFormat.Xps, saveOptions);

Console.WriteLine($"XPS file saved to: {outputPath}");
```

Όταν ανοίξετε το `EmbeddedFontExample.xps` στο Windows XPS Viewer, θα δείτε το κείμενο να αποδίδεται ακριβώς όπως εμφανιζόταν στο PDF, ανεξάρτητα από το αν το σύστημα του θεατή έχει εγκατεστημένη τη γραμματοσειρά Arial.

## Βήμα 5: Επαλήθευση Ενσωμάτωσης Γραμματοσειρών (Προαιρετικό αλλά Συνιστάται)

Αν θέλετε να ελέγξετε ξανά ότι οι γραμματοσειρές είναι πραγματικά ενσωματωμένες, μπορείτε να αποσυμπιέσετε το αρχείο XPS (είναι απλώς ένα αρχείο ZIP) και να εξετάσετε το φάκελο `Resources/Fonts`.

```powershell
# PowerShell one‑liner to list embedded fonts
Expand-Archive -Path .\EmbeddedFontExample.xps -DestinationPath .\tempXps
Get-ChildItem .\tempXps\Resources\Fonts
```

Θα πρέπει να δείτε αρχεία `.ttf` ή `.otf` που αντιστοιχούν στις γραμματοσειρές που χρησιμοποιήσατε. Αν ο φάκελος είναι κενός, ελέγξτε ξανά το `saveOptions.EmbedFonts` και βεβαιωθείτε ότι η πηγή γραμματοσειράς δεν περιορίζεται από άδεια.

## Συνηθισμένες Περιπτώσεις & Πώς να τις Διαχειριστείτε

| Κατάσταση | Τι Συμβαίνει | Λύση |
|-----------|--------------|------|
| **Η γραμματοσειρά έχει άδεια “no‑embed”** | Το Aspose αντικαθιστά σιωπηλά τη γραμματοσειρά, με αποτέλεσμα ελλιπείς γλύφους. | Χρησιμοποιήστε διαφορετική γραμματοσειρά ή αποκτήστε άδεια που επιτρέπει ενσωμάτωση. |
| **Το αρχείο προσαρμοσμένης γραμματοσειράς δεν είναι εγκατεστημένο** | `FontRepository.FindFont` επιστρέφει `null` → εξαίρεση χρόνου εκτέλεσης. | Φορτώστε τη γραμματοσειρά χειροκίνητα: `FontRepository.AddFont("path/to/font.ttf");` πριν δημιουργήσετε το `TextFragment`. |
| **Μεγάλα αρχεία XPS** | Η ενσωμάτωση πολλών γραμματοσειρών μπορεί να αυξήσει το μέγεθος του αρχείου. | Ενεργοποιήστε `Compression = CompressionType.Zip` ή υποσύνολο γραμματοσειρών μέσω `saveOptions.SubsetFonts = true`. |
| **Μη εμφανιζόμενοι Unicode χαρακτήρες** | Ελλιπείς γλύφοι για ορισμένα σενάρια. | Βεβαιωθείτε ότι η επιλεγμένη γραμματοσειρά υποστηρίζει το απαιτούμενο εύρος Unicode, ή ενσωματώστε πολλαπλές εναλλακτικές γραμματοσειρές. |

---

## Πλήρες Παράδειγμα (Έτοιμο για Αντιγραφή‑Επικόλληση)

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.XpsConversion;

class EmbedFontsInXpsDemo
{
    static void Main()
    {
        // 1️⃣ Create a simple PDF with custom text
        Document pdfDoc = new Document();
        Page page = pdfDoc.Pages.Add();

        // Load a TrueType font (Arial) – replace with your font if needed
        FontRepository.AddFont(@"C:\Windows\Fonts\arial.ttf");
        TextFragment tf = new TextFragment("Hello, XPS world!")
        {
            TextState = { Font = FontRepository.FindFont("Arial") }
        };
        page.Paragraphs.Add(tf);

        // 2️⃣ Set up XpsSaveOptions to embed fonts
        XpsSaveOptions saveOptions = new XpsSaveOptions
        {
            EmbedFonts = true,
            Compression = CompressionType.Zip,
            PreserveFormFields = true
        };

        // 3️⃣ Save as XPS
        string outputPath = Path.Combine(
            Environment.CurrentDirectory,
            "EmbeddedFontExample.xps");

        pdfDoc.Save(outputPath, SaveFormat.Xps, saveOptions);

        Console.WriteLine($"✅ XPS saved with embedded fonts at: {outputPath}");
    }
}
```

**Αναμενόμενο αποτέλεσμα** (κονσόλα):

```
✅ XPS saved with embedded fonts at: C:\YourProject\EmbeddedFontExample.xps
```

Ανοίξτε το παραγόμενο αρχείο XPS· το κείμενο θα εμφανίζεται ακριβώς όπως μορφοποιήθηκε, ακόμη και σε μηχάνημα χωρίς εγκατεστημένη τη γραμματοσειρά Arial.

---

## Συμπέρασμα

Δείξαμε πώς να **ενσωματώσετε γραμματοσειρές σε XPS** χρησιμοποιώντας C# και **Aspose.PDF for .NET**. Ρυθμίζοντας το `XpsSaveOptions` με `EmbedFonts = true`, εξασφαλίζετε ότι κάθε γλύφος ταξιδεύει μαζί με το πακέτο XPS, εξαλείφοντας ανεπιθύμητες εκπλήξεις σε υπολογιστές πελατών.  

Από τη ρύθμιση του project μέχρι την επαλήθευση των ενσωματωμένων πόρων, έχετε τώρα μια πλήρη, έτοιμη για αντιγραφή λύση. Στη συνέχεια, δοκιμάστε διαφορετικές γραμματοσειρές, προσθέστε εικόνες ή δημιουργήστε πολυσελίδες XPS—όλα θα ωφεληθούν από την ίδια στρατηγική ενσωμάτωσης.

Έχετε ερωτήσεις σχετικά με άδειες, υποσύνολα ή απόδοση; Αφήστε ένα σχόλιο, και καλή προγραμματιστική δουλειά!

## Τι Θα Μάθετε Στη Σειρά Επόμενη;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να κατακτήσετε επιπλέον δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στα δικά σας έργα.

- [Export Excel to XPS with Aspose.Cells .NET](/cells/english/net/workbook-operations/export-excel-xps-aspose-cells-net/)
- [How to Extract Fonts from Excel Files Using Aspose.Cells for .NET](/cells/english/net/formatting/extract-fonts-excel-aspose-cells-dotnet-guide/)
- [Render Excel to PNG, TIFF, PDF with Custom Fonts in .NET Using Aspose.Cells](/cells/english/net/workbook-operations/render-excel-custom-fonts-aspose-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}