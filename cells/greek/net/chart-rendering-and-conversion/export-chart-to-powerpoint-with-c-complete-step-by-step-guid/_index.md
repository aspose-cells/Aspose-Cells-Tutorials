---
category: general
date: 2026-02-26
description: Εξαγωγή γραφήματος σε PowerPoint από το Excel χρησιμοποιώντας C#. Μάθετε
  πώς να μετατρέψετε το Excel σε PowerPoint, να αποθηκεύσετε το Excel ως PowerPoint
  και να διατηρήσετε τα σχήματα επεξεργάσιμα.
draft: false
keywords:
- export chart to powerpoint
- convert excel to powerpoint
- save excel as powerpoint
- how to convert excel to ppt
- save workbook as pptx
language: el
og_description: Εξαγωγή γραφήματος στο PowerPoint από το Excel χρησιμοποιώντας C#.
  Αυτός ο οδηγός δείχνει πώς να μετατρέψετε το Excel σε PowerPoint, να αποθηκεύσετε
  το βιβλίο εργασίας ως PPTX και να διατηρήσετε τα σχήματα επεξεργάσιμα.
og_title: Εξαγωγή γραφήματος στο PowerPoint με C# – Πλήρης οδηγός προγραμματισμού
tags:
- Aspose.Cells
- C#
- Office Automation
title: Εξαγωγή γραφήματος στο PowerPoint με C# – Πλήρης οδηγός βήμα‑προς‑βήμα
url: /el/net/chart-rendering-and-conversion/export-chart-to-powerpoint-with-c-complete-step-by-step-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή Διαγράμματος σε PowerPoint – Πλήρης Προγραμματιστική Εκπαίδευση

Έχετε αναρωτηθεί ποτέ πώς να **εξάγετε διάγραμμα σε PowerPoint** χωρίς να χάσετε τη δυνατότητα επεξεργασίας; Σε πολλές περιπτώσεις αναφοράς χρειάζεστε ένα ζωντανό διάγραμμα μέσα σε μια παρουσίαση, αλλά η αντιγραφή‑επικόλληση χειροκίνητα είναι κουραστική. Τα καλά νέα είναι ότι μπορείτε να το κάνετε προγραμματιστικά με λίγες γραμμές C#.

Σε αυτόν τον οδηγό θα περάσουμε από όλη τη διαδικασία: από τη φόρτωση ενός βιβλίου εργασίας Excel που περιέχει διάγραμμα με πλαίσιο κειμένου, τη ρύθμιση της εξαγωγής ώστε τα πλαίσια κειμένου και τα σχήματα να παραμείνουν επεξεργάσιμα, και τέλος την αποθήκευση του αποτελέσματος ως αρχείο **PowerPoint**. Στο τέλος θα γνωρίζετε επίσης πώς να **μετατρέψετε το Excel σε PowerPoint**, **αποθηκεύσετε το Excel ως PowerPoint**, και ακόμη να προσαρμόσετε τις επιλογές για σενάρια άκρων.

## Τι Θα Χρειαστεί

- **Aspose.Cells for .NET** (έκδοση 23.10 ή νεότερη). Είναι η βιβλιοθήκη που κάνει τη μετατροπή απλή.
- **.NET 6+** runtime – οποιοδήποτε πρόσφατο SDK λειτουργεί.
- Ένα απλό αρχείο Excel (`ChartWithTextbox.xlsx`) που περιέχει τουλάχιστον ένα διάγραμμα και ένα πλαίσιο κειμένου.
- Visual Studio ή το αγαπημένο σας IDE.

Δεν απαιτούνται επιπλέον πακέτα NuGet πέρα από το Aspose.Cells, αλλά η βασική γνώση της σύνταξης C# σίγουρα βοηθά.

## Εξαγωγή Διαγράμματος σε PowerPoint – Βήμα‑Βήμα

Παρακάτω χωρίζουμε τη λύση σε διακριτά, εύκολα ακολουθήσιμα βήματα. Κάθε βήμα περιλαμβάνει τον ακριβή κώδικα που χρειάζεστε, καθώς και μια σύντομη παράγραφο «γιατί» που εξηγεί τη λογική πίσω από αυτό.

### Βήμα 1: Φόρτωση του Βιβλίου Εργασίας Excel που Περιέχει το Διάγραμμα

Πρώτα πρέπει να φέρουμε το αρχείο προέλευσης στη μνήμη. Η χρήση του `Workbook` από το Aspose.Cells διαβάζει ολόκληρο το φύλλο, συμπεριλαμβανομένων διαγραμμάτων, εικόνων και ενσωματωμένων αντικειμένων.

```csharp
using Aspose.Cells;

// Step 1: Load the Excel workbook that contains the chart with a textbox
Workbook workbook = new Workbook(@"C:\Samples\ChartWithTextbox.xlsx");

// Verify that the workbook actually contains a chart
if (workbook.Worksheets[0].Charts.Count == 0)
{
    throw new InvalidOperationException("No chart found in the first worksheet.");
}
```

*Γιατί είναι σημαντικό:* Αν το βιβλίο εργασίας ανοιχτεί χωρίς να καθοριστεί σωστά η διαδρομή, θα λάβετε `FileNotFoundException`. Η γρήγορη επαλήθευση αποτρέπει την εξαγωγή ενός κενού slide αργότερα.

### Βήμα 2: Προετοιμασία Επιλογών Παρουσίασης για Διατήρηση Επεξεργάσιμων Σχημάτων

Το Aspose.Cells σας επιτρέπει να αποφασίσετε αν τα πλαίσια κειμένου, τα σχήματα και ακόμη και το ίδιο το διάγραμμα θα παραμείνουν **επεξεργάσιμα** μετά την εξαγωγή. Ορίζοντας `ExportTextBoxes` και `ExportShapes` σε `true` διατηρεί αυτά τα αντικείμενα ως εγγενή στοιχεία PowerPoint αντί να τα μετατρέπει σε στατική εικόνα.

```csharp
using Aspose.Cells.Drawing;

// Step 2: Set up presentation options to keep textboxes and shapes editable in the output
PresentationOptions presentationOptions = new PresentationOptions
{
    ExportTextBoxes = true, // Preserve editable textboxes
    ExportShapes    = true  // Preserve shapes such as the chart itself
};
```

*Γιατί είναι σημαντικό:* Αν αφήσετε αυτές τις σημαίες στις προεπιλογές τους (`false`), η διαφάνεια που θα προκύψει θα περιέχει bitmap του διαγράμματος, καθιστώντας αδύνατη την επεξεργασία των σειρών ή την αλλαγή της λεζάντας αργότερα. Η ενεργοποίηση και των δύο επιλογών σας δίνει ένα πραγματικό διάγραμμα PowerPoint που συμπεριφέρεται ακριβώς όπως θα το σχεδιάζατε χειροκίνητα.

### Βήμα 3: Μετατροπή Excel σε PowerPoint και Αποθήκευση του Αρχείου

Τώρα καλούμε τη μέθοδο `Save`, περνώντας το enum `SaveFormat.Pptx` και τις επιλογές που μόλις διαμορφώσαμε. Η βιβλιοθήκη αναλαμβάνει τη μετάφραση του αντικειμένου διαγράμματος Excel σε σχήμα διαγράμματος PowerPoint.

```csharp
// Step 3: Save the workbook as a PowerPoint presentation using the configured options
workbook.Save(@"C:\Samples\Result.pptx", SaveFormat.Pptx, presentationOptions);
```

*Γιατί είναι σημαντικό:* Η κλήση `Save` κάνει όλη τη βαριά δουλειά—αντιστοιχίζει σειρές Excel σε σειρές PowerPoint, διατηρεί τη μορφοποίηση των αξόνων και αντιγράφει τυχόν συνδεδεμένα πλαίσια κειμένου. Μετά την εκτέλεση αυτής της γραμμής, θα έχετε ένα πλήρως‑επεξεργάσιμο αρχείο `.pptx` έτοιμο να ανοιχτεί στο Microsoft PowerPoint.

### Επαλήθευση του Αποτελέσματος

Ανοίξτε το `Result.pptx` στο PowerPoint. Θα πρέπει να δείτε μια διαφάνεια που περιέχει:

- Το αρχικό διάγραμμα, ακόμα συνδεδεμένο με τα δεδομένα του (μπορείτε να κάνετε διπλό‑κλικ για να επεξεργαστείτε τις σειρές).
- Οποιοδήποτε πλαίσιο κειμένου υπήρχε στο φύλλο Excel, τώρα ως εγγενές πλαίσιο κειμένου PowerPoint.
- Η διάταξη της διαφάνειας επιλέγεται αυτόματα (συνήθως μια κενή διαφάνεια).

Αν παρατηρήσετε ελλιπή στοιχεία, ελέγξτε ξανά ότι το βιβλίο εργασίας προέλευσης είχε ορατά αντικείμενα και ότι οι `ExportTextBoxes` / `ExportShapes` ήταν ορισμένες σε `true`.

### Μετατροπή Excel σε PowerPoint: Διαχείριση Πολλαπλών Φύλλων

Συχνά ένα βιβλίο εργασίας περιέχει περισσότερα από ένα φύλλο, το καθένα με το δικό του διάγραμμα. Από προεπιλογή το Aspose.Cells θα εξάγει **όλα** τα διαγράμματα από **όλα** τα φύλλα σε ξεχωριστές διαφάνειες. Αν χρειάζεστε μόνο ένα υποσύνολο, μπορείτε να τα φιλτράρετε πριν την αποθήκευση:

```csharp
// Example: Export only charts from the first worksheet
Worksheet firstSheet = workbook.Worksheets[0];
foreach (Chart chart in firstSheet.Charts)
{
    chart.IsVisible = true; // Ensure visibility
}

// Hide charts from other sheets
for (int i = 1; i < workbook.Worksheets.Count; i++)
{
    foreach (Chart chart in workbook.Worksheets[i].Charts)
    {
        chart.IsVisible = false;
    }
}
```

*Συμβουλή:* Ορίζοντας `chart.IsVisible = false` είναι φθηνότερο από το να αφαιρέσετε εντελώς το διάγραμμα, και σας επιτρέπει να εναλλάξετε την ένταξή του χωρίς να τροποποιήσετε το αρχείο προέλευσης.

### Αποθήκευση Excel ως PowerPoint – Προσαρμογή Μεγέθους Διαφάνειας

Το PowerPoint προεπιλέγει μια διαφάνεια 10‑inch x 5.63‑inch. Αν το διάγραμμά σας φαίνεται στενεμένο, μπορείτε να αλλάξετε τις διαστάσεις της διαφάνειας μέσω του αντικειμένου `PresentationOptions`:

```csharp
presentationOptions.SlideSize = new SizeF(13.33f, 7.5f); // 16:9 widescreen
```

Τώρα το εξαγόμενο διάγραμμα θα έχει περισσότερο χώρο, και τα πλαίσια κειμένου θα διατηρήσουν την αρχική τους διάταξη.

### Πώς να Μετατρέψετε Excel σε PPT: Διαχείριση Κρυφών Αντικειμένων

Κρυφές γραμμές, στήλες ή σχήματα μπορούν μερικές φορές να διαρρεύσουν στην εξαγωγή. Για να τα αφαιρέσετε, εκτελέστε έναν γρήγορο καθαρισμό πριν την αποθήκευση:

```csharp
// Remove hidden rows/columns that might affect chart layout
foreach (Worksheet sheet in workbook.Worksheets)
{
    sheet.Cells.HideRows = false;
    sheet.Cells.HideColumns = false;
}
```

Αυτό το βήμα δεν είναι πάντα απαραίτητο, αλλά αποτρέπει απρόσμενα κενά στην τελική παρουσίαση.

### Αποθήκευση Βιβλίου Εργασίας ως PPTX – Πλήρες Παράδειγμα Εργασίας

Συνδυάζοντας τα πάντα, εδώ είναι ένα έτοιμο για εκτέλεση πρόγραμμα κονσόλας που δείχνει ολόκληρη τη ροή:

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing; // For SizeF

class ExportChartDemo
{
    static void Main()
    {
        // Load workbook (Step 1)
        string sourcePath = @"C:\Samples\ChartWithTextbox.xlsx";
        Workbook workbook = new Workbook(sourcePath);

        // Verify chart existence
        if (workbook.Worksheets[0].Charts.Count == 0)
        {
            Console.WriteLine("No chart found. Exiting.");
            return;
        }

        // Configure presentation options (Step 2)
        PresentationOptions options = new PresentationOptions
        {
            ExportTextBoxes = true,
            ExportShapes    = true,
            SlideSize       = new SizeF(13.33f, 7.5f) // optional widescreen
        };

        // Optional: export only first worksheet charts
        for (int i = 1; i < workbook.Worksheets.Count; i++)
        {
            foreach (Chart c in workbook.Worksheets[i].Charts)
                c.IsVisible = false;
        }

        // Save as PowerPoint (Step 3)
        string targetPath = @"C:\Samples\Result.pptx";
        workbook.Save(targetPath, SaveFormat.Pptx, options);

        Console.WriteLine($"Export complete! File saved to {targetPath}");
    }
}
```

Η εκτέλεση αυτού του προγράμματος θα δημιουργήσει το `Result.pptx` με επεξεργάσιμο διάγραμμα και πλαίσιο κειμένου, ακριβώς όπως θα περιμένατε όταν **αποθηκεύετε το βιβλίο εργασίας ως pptx** χειροκίνητα.

![Παράδειγμα εξαγωγής διαγράμματος σε PowerPoint](/images/export-chart-to-powerpoint.png "Εξαγωγή διαγράμματος σε PowerPoint – επεξεργάσιμη διαφάνεια")

## Συχνές Ερωτήσεις & Σενάρια Άκρων

**Τι γίνεται αν το αρχείο Excel περιέχει διάγραμμα με εξωτερική πηγή δεδομένων;**  
Το Aspose.Cells αντιγράφει τις *τρέχουσες* τιμές δεδομένων στο διάγραμμα PowerPoint. **Δεν** διατηρεί τον εξωτερικό σύνδεσμο, επειδή το PowerPoint δεν μπορεί να αναφερθεί σε σύνδεση δεδομένων Excel με τον ίδιο τρόπο. Αν χρειάζεστε ζωντανές ενημερώσεις, σκεφτείτε να ενσωματώσετε το αρχικό αρχείο Excel στο PPTX ως αντικείμενο OLE.

**Μπορώ να εξάγω διάγραμμα που χρησιμοποιεί προσαρμοσμένο θέμα;**  
Ναι. Η βιβλιοθήκη προσπαθεί να αντιστοιχίσει τα χρώματα θέματος του Excel στα slots θέματος του PowerPoint. Για πολύ προσαρμοσμένες παλέτες ίσως χρειαστεί να προσαρμόσετε τα χρώματα μετά την εξαγωγή χρησιμοποιώντας το API του PowerPoint (π.χ., Aspose.Slides).

**Υπάρχει όριο στον αριθμό των διαγραμμάτων;**  
Σ πρακτικό επίπεδο κανένα—το Aspose.Cells κάνει streaming των δεδομένων, οπότε ακόμη και ένα βιβλίο εργασίας με δεκάδες διαγράμματα θα εξαχθεί, αν και το μέγεθος του PPTX αυξάνεται γραμμικά.

**Χρειάζομαι άδεια για το Aspose.Cells;**  
Μια δωρεάν αξιολόγηση λειτουργεί, αλλά προσθέτει υδατογράφημα στην πρώτη διαφάνεια. Για παραγωγική χρήση, αποκτήστε έγκυρη άδεια ώστε να αφαιρέσετε το υδατογράφημα και να ξεκλειδώσετε πλήρη απόδοση.

## Ανακεφαλαίωση

Συζητήσαμε πώς να **εξάγετε διάγραμμα σε PowerPoint** χρησιμοποιώντας C#, παρουσιάζοντας τον ακριβή κώδικα για τη φόρτωση ενός βιβλίου εργασίας Excel, τη διαμόρφωση των `PresentationOptions` ώστε τα πλαίσια κειμένου και τα σχήματα να παραμείνουν επεξεργάσιμα, και τέλος την αποθήκευση του αποτελέσματος ως `.pptx`. Μάθατε επίσης πώς να **μετατρέψετε το Excel σε PowerPoint**, **αποθηκεύσετε το Excel ως PowerPoint**, και πώς να απαντήσετε στην ερώτηση “**πώς να μετατρέψετε το Excel σε ppt**” με ένα πλήρες, εκτελέσιμο παράδειγμα.

## Τι Ακολουθεί;

- **Αποθήκευση βιβλίου εργασίας ως PPTX** με πολλαπλές διαφάνειες: επαναλάβετε τη διαδικασία για κάθε φύλλο και καλέστε `Save` με `PresentationOptions` για το καθένα.
- Εξερευνήστε το **Aspose.Slides** αν χρειάζεστε προγραμματιστική τροποποίηση του παραγόμενου PPTX (προσθήκη μεταβάσεων, σημειώσεων ομιλητή κ.λπ.).
- Δοκιμάστε την εξαγωγή **pivot charts** ή **3‑D charts**—οι ίδιες επιλογές ισχύουν, αλλά ίσως χρειαστεί να προσαρμόσετε τη μορφοποίηση των αξόνων μετά.

Αν αντιμετωπίσετε δυσκολίες, αφήστε ένα σχόλιο παρακάτω ή ελέγξτε την επίσημη τεκμηρίωση του Aspose.Cells για τις τελευταίες αλλαγές API. Καλή προγραμματιστική δουλειά και απολαύστε τη μετατροπή των διαγραμμάτων Excel σε επαγγελματικές παρουσιάσεις PowerPoint με λίγες μόνο γραμμές C#!

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}