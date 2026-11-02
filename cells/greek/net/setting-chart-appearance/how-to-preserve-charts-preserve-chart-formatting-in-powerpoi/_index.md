---
category: general
date: 2026-07-03
description: πώς να διατηρήσετε τα διαγράμματα διατηρώντας τη μορφοποίηση των διαγραμμάτων
  χρησιμοποιώντας το Aspose.Slides σε C#. Ακολουθήστε αυτόν τον οδηγό βήμα‑βήμα.
draft: false
keywords:
- how to preserve charts
- preserve chart formatting
language: el
og_description: Πώς να διατηρήσετε τα διαγράμματα και τη μορφοποίηση των διαγραμμάτων
  με το Aspose.Slides σε C#. Πλήρης οδηγός με κώδικα.
og_title: πώς να διατηρήσετε τα διαγράμματα – διατήρηση μορφοποίησης διαγράμματος
  στο PowerPoint (C#)
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: how to preserve charts while keeping preserve chart formatting using
    Aspose.Slides in C#. Follow this step‑by‑step guide.
  headline: how to preserve charts – preserve chart formatting in PowerPoint C#
  type: TechArticle
- description: how to preserve charts while keeping preserve chart formatting using
    Aspose.Slides in C#. Follow this step‑by‑step guide.
  name: how to preserve charts – preserve chart formatting in PowerPoint C#
  steps:
  - name: Open `EditableCharts.pptx` in PowerPoint.
    text: Open `EditableCharts.pptx` in PowerPoint.
  - name: Click any chart → “Edit Data”.
    text: Click any chart → “Edit Data”.
  - name: The Excel‑like data sheet should appear, letting you modify series values.
    text: The Excel‑like data sheet should appear, letting you modify series values.
  type: HowTo
- questions:
  - answer: Directly no—`ExportEditableObjects` only applies to the PPTX format. Convert
      first, then export.
    question: Does this work with PowerPoint 2003 (PPT) files?
  - answer: Absolutely. The same `ExportEditableObjects` flag keeps SmartArt, tables,
      and diagrams editable.
    question: Can I preserve other objects like SmartArt?
  - answer: 'The slide size is stored in the presentation metadata and isn’t affected
      by these options. No extra code needed. --- ## Next steps – keep the momentum
      Now that you’ve nailed **how to preserve charts**, try exploring: - **preserve
      chart formatting** for specific chart types (e.g., stacked bar vs. rad'
    question: What if I need to keep the original slide size?
  type: FAQPage
tags:
- Aspose.Slides
- C#
- PowerPoint
- chart automation
title: πώς να διατηρήσετε τα διαγράμματα – διατήρηση μορφοποίησης διαγράμματος στο
  PowerPoint C#
url: /el/net/setting-chart-appearance/how-to-preserve-charts-preserve-chart-formatting-in-powerpoi/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# πώς να διατηρήσετε τα διαγράμματα – διατήρηση μορφοποίησης διαγράμματος στο PowerPoint C#

Έχετε αναρωτηθεί ποτέ **πώς να διατηρήσετε τα διαγράμματα** όταν χρειάζεται να εξάγετε ή να επεξεργαστείτε ένα αρχείο PowerPoint προγραμματιστικά; Ίσως να έχετε δοκιμάσει μια γρήγορη αποθήκευση και το διάγραμμα να μετατράπηκε σε στατική εικόνα, σπάζοντας την δυνατότητα επεξεργασίας που βασιζόσασταν.

Σε αυτό το tutorial θα σας δείξουμε **πώς να διατηρήσετε τα διαγράμματα** **και** να διατηρήσετε το **preserve chart formatting** αμετάβλητο χρησιμοποιώντας το Aspose.Slides for .NET. Στο τέλος θα έχετε ένα έτοιμο προς εκτέλεση απόσπασμα C# που παράγει ένα PPTX όπου κάθε διάγραμμα παραμένει ένα επεξεργάσιμο αντικείμενο OOXML—χωρίς πλέον επίπεδες εικόνες.

## Τι θα μάθετε

- Τα ακριβή βήματα για τη φόρτωση μιας παρουσίασης, τη διαμόρφωση των επιλογών εξαγωγής και την αποθήκευση ενώ **preserving chart formatting**.  
- Γιατί η σημαία `ExportEditableObjects` είναι σημαντική και πώς εμποδίζει τα διαγράμματα να ραστεροποιηθούν.  
- Κοινά προβλήματα (π.χ., παλαιότερες μορφές PPT, ελλιπείς γραμματοσειρές) και γρήγορες λύσεις.  

Δεν απαιτείται προηγούμενη εμπειρία με το Aspose· απλώς μια βασική ρύθμιση C# και ένα αρχείο PowerPoint που θέλετε να διατηρήσετε φιλικό προς τα διαγράμματα.

## Προαπαιτούμενα

- .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί επίσης με .NET Framework 4.7+).  
- Πακέτο NuGet Aspose.Slides for .NET (`Install-Package Aspose.Slides.NET`).  
- Ένα δείγμα `input.pptx` που περιέχει τουλάχιστον ένα διάγραμμα.  
- Visual Studio, Rider ή οποιονδήποτε επεξεργαστή προτιμάτε.

---

## Βήμα 1: Εγκατάσταση Aspose.Slides και δημιουργία νέου έργου console

Για να ξεκινήσετε, δημιουργήστε μια νέα εφαρμογή console και προσθέστε τη βιβλιοθήκη:

```bash
dotnet new console -n PreserveChartsDemo
cd PreserveChartsDemo
dotnet add package Aspose.Slides.NET
```

> **Pro tip:** Εάν βρίσκεστε πίσω από εταιρικό proxy, προσθέστε τη σημαία `--no-restore` και αποκαταστήστε αργότερα με τις ρυθμίσεις του proxy σας.

## Βήμα 2: Φόρτωση της πηγαίας παρουσίασης – το πρώτο σημείο για την εφαρμογή του **how to preserve charts**

Ανοίξτε το αρχείο PPTX χρησιμοποιώντας την κλάση `Presentation`. Εδώ αρχίζει πραγματικά το ταξίδι προς το **how to preserve charts**.

```csharp
using Aspose.Slides;
using Aspose.Slides.Export;

namespace PreserveChartsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 2: Load the source presentation
            // Replace the path with the location of your PPTX that contains charts.
            Presentation pres = new Presentation(@"YOUR_DIRECTORY\input.pptx");
```

Παρατηρήστε ότι δεν έχουμε αγγίξει ακόμη κανένα αντικείμενο διαγράμματος—αυτό είναι σκόπιμο. Η φόρτωση του αρχείου όπως είναι εξασφαλίζει ότι διατηρούμε την αρχική δομή XML, η οποία είναι κρίσιμη για το **preserve chart formatting** αργότερα.

## Βήμα 3: Διαμόρφωση επιλογών εξαγωγής – η καρδιά του **how to preserve charts**

Το Aspose.Slides προσφέρει μια κλάση `PresentationExportOptions`. Ορίζοντας το `ExportEditableObjects` σε `true` λέει στη μηχανή να διατηρήσει τα διαγράμματα, πίνακες και SmartArt ως εγγενή τμήματα OOXML αντί να τα επίπεδωσε.

```csharp
            // Step 3: Configure export options to keep objects editable
            PresentationExportOptions exportOptions = new PresentationExportOptions
            {
                // This flag is the key to how to preserve charts.
                ExportEditableObjects = true
            };
```

Γιατί λειτουργεί αυτό; Όταν το `ExportEditableObjects` είναι `false` (η προεπιλογή), η βιβλιοθήκη ραστεροποιεί πολύπλοκα αντικείμενα για συμβατότητα, κάτι που καταστρέφει το **preserve chart formatting**. Ενεργοποιώντας το, διατηρείται το αρχικό XML του διαγράμματος, επιτρέποντας στους τελικούς χρήστες να ανοίξουν το PPTX και να επεξεργαστούν τα δεδομένα του διαγράμματος.

## Βήμα 4: Αποθήκευση της παρουσίασης χρησιμοποιώντας τις διαμορφωμένες επιλογές

Τώρα γράφουμε το αρχείο εξόδου. Η ίδια υπερφόρτωση `Save` που δέχεται `SaveFormat` και `exportOptions` εγγυάται ότι το διάγραμμα παραμένει επεξεργάσιμο.

```csharp
            // Step 4: Save the presentation with the configured options
            pres.Save(@"YOUR_DIRECTORY\EditableCharts.pptx", SaveFormat.Pptx, exportOptions);

            // Optional: Inform the user
            Console.WriteLine("Presentation saved with editable charts at: YOUR_DIRECTORY\\EditableCharts.pptx");
        }
    }
}
```

Η εκτέλεση αυτού του προγράμματος παράγει το `EditableCharts.pptx`. Ανοίξτε το στο PowerPoint, κάντε δεξί κλικ σε ένα διάγραμμα και θα δείτε την συνηθισμένη επιλογή «Edit Data»—απόδειξη ότι καταφέραμε με επιτυχία το **how to preserve charts** και το **preserve chart formatting**.

## Βήμα 5: Επαλήθευση του αποτελέσματος και αντιμετώπιση κοινών προβλημάτων

### Επαλήθευση

1. Ανοίξτε το `EditableCharts.pptx` στο PowerPoint.  
2. Κάντε κλικ σε οποιοδήποτε διάγραμμα → «Edit Data».  
3. Θα πρέπει να εμφανιστεί το φύλλο δεδομένων τύπου Excel, επιτρέποντάς σας να τροποποιήσετε τις τιμές των σειρών.

Εάν βλέπετε μόνο μια στατική εικόνα, ελέγξτε ξανά ότι:

- Χρησιμοποιείτε μια πρόσφατη έκδοση του Aspose.Slides (παλαιότερες εκδόσεις είχαν σφάλματα με το `ExportEditableObjects`).  
- Το πηγαίο PPTX περιέχει πραγματικά αντικείμενα διαγράμματος (όχι εικόνες διαγραμμάτων).  
- Καμία προσαρμοσμένη θεματική ή αντικατάσταση γραμματοσειράς δεν προκαλεί το διάγραμμα να αποδοθεί ως εικόνα.

### Ακραίες Περιπτώσεις

- **Older PPT (binary) files:** Μετατρέψτε τα πρώτα σε PPTX (`pres.Save("temp.pptx", SaveFormat.Pptx)`) πριν εφαρμόσετε τις επιλογές εξαγωγής.  
- **Large presentations:** Η χρήση μνήμης μπορεί να αυξηθεί· εξετάστε το πρότυπο `Dispose` της `Presentation` ή τα streaming APIs για τεράστια αρχεία.  
- **Embedded fonts:** Εάν το περιβάλλον προορισμού δεν διαθέτει τις αρχικές γραμματοσειρές, το PowerPoint μπορεί να επανέλθει και να αποδώσει το διάγραμμα ως εικόνα. Ενσωματώστε τις γραμματοσειρές στο πηγαίο αρχείο ή στείλτε τις με την εφαρμογή σας.

---

## Συχνές Ερωτήσεις (FAQ)

**Q: Λειτουργεί αυτό με αρχεία PowerPoint 2003 (PPT);**  
A: Απευθείας όχι—το `ExportEditableObjects` ισχύει μόνο για τη μορφή PPTX. Μετατρέψτε πρώτα, μετά εξάγετε.

**Q: Μπορώ να διατηρήσω άλλα αντικείμενα όπως SmartArt;**  
A: Απόλυτα. Η ίδια σημαία `ExportEditableObjects` διατηρεί τα SmartArt, πίνακες και διαγράμματα επεξεργάσιμα.

**Q: Τι γίνεται αν χρειάζεται να διατηρήσω το αρχικό μέγεθος διαφάνειας;**  
A: Το μέγεθος της διαφάνειας αποθηκεύεται στα μεταδεδομένα της παρουσίασης και δεν επηρεάζεται από αυτές τις επιλογές. Δεν απαιτείται επιπλέον κώδικας.

## Επόμενα βήματα – διατηρήστε το κίνητρο

Τώρα που έχετε κατακτήσει το **how to preserve charts**, δοκιμάστε να εξερευνήσετε:

- **preserve chart formatting** για συγκεκριμένους τύπους διαγραμμάτων (π.χ., στοίβαγμα μπαρών vs. ραντάρ).  
- Χρήση του API `Chart` για προγραμματιστική τροποποίηση των δεδομένων πριν την αποθήκευση.  
- Εξαγωγή σε άλλες μορφές (PDF, HTML) ενώ τα διαγράμματα παραμένουν επεξεργάσιμα στην πηγαία PPTX.  

Κάθε ένα από αυτά βασίζεται στην ίδια αρχή: διατηρήστε το υποκείμενο OOXML αμετάβλητο.

## Συμπέρασμα

Διασχίσαμε το **how to preserve charts** σε ένα αρχείο PowerPoint χρησιμοποιώντας το Aspose.Slides for .NET, και δείξαμε τα ακριβή βήματα **preserve chart formatting** που απαιτούνται για να διατηρηθούν αυτά τα διαγράμματα πλήρως επεξεργάσιμα. Το πλήρες απόσπασμα κώδικα παραπάνω είναι έτοιμο να ενσωματωθεί σε οποιοδήποτε έργο C#, και οι εξηγήσεις καλύπτουν το *γιατί* πίσω από κάθε γραμμή—ώστε να μην κάνετε απλώς copy‑paste, αλλά να καταλάβετε.

Δοκιμάστε το, προσαρμόστε τις επιλογές εξαγωγής, και σύντομα θα αυτοματοποιείτε τις ενημερώσεις παρουσιάσεων χωρίς ποτέ να χάνετε τη δυνατότητα λεπτομερούς ρύθμισης των δεδομένων των διαγραμμάτων. Καλή προγραμματιστική!

## Τι Θα Πρέπει Να Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [How to Export Excel Charts to PDF Using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [How to Convert Excel Charts to SVG Using Aspose.Cells for .NET (Step-by-Step Guide)](/cells/english/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)
- [How to Create Charts in Excel Using Aspose.Cells for .NET&#58; A Developer's Guide](/cells/english/net/charts-graphs/create-charts-excel-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}