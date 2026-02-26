---
category: general
date: 2026-02-21
description: Δημιουργήστε PowerPoint από το Excel γρήγορα. Μάθετε πώς να εξάγετε το
  Excel σε PowerPoint με επεξεργάσιμο κείμενο και γραφήματα χρησιμοποιώντας το Aspose.Cells
  σε λίγες μόνο γραμμές C#.
draft: false
keywords:
- create powerpoint from excel
- export excel to powerpoint
- export editable text
- export excel chart powerpoint
- convert excel chart powerpoint
language: el
og_description: Δημιουργήστε PowerPoint από Excel με επεξεργάσιμο κείμενο και γραφήματα.
  Ακολουθήστε αυτόν τον λεπτομερή οδηγό για να εξάγετε το Excel σε PowerPoint χρησιμοποιώντας
  το Aspose.Cells.
og_title: Δημιουργία PowerPoint από Excel – Οδηγός C# βήμα‑προς‑βήμα
tags:
- C#
- Aspose.Cells
- PowerPoint
- Excel Automation
title: Δημιουργία PowerPoint από Excel – Πλήρες Μάθημα C#
url: /el/net/converting-excel-files-to-other-formats/create-powerpoint-from-excel-complete-c-tutorial/
---

kept all code block placeholders unchanged.

Now produce final output.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία PowerPoint από Excel – Πλήρες C# Tutorial

Έχετε ποτέ χρειαστεί να **δημιουργήσετε PowerPoint από Excel** αλλά δεν ήξερατε ποιο API να χρησιμοποιήσετε; Δεν είστε μόνοι. Πολλοί προγραμματιστές συναντούν πρόβλημα όταν θέλουν να μετατρέψουν ένα φύλλο εργασίας γεμάτο δεδομένα σε μια επαγγελματική παρουσίαση, ειδικά όταν χρειάζονται τα πλαίσια κειμένου να παραμείνουν επεξεργάσιμα μετά τη μετατροπή.  

Σε αυτόν τον οδηγό θα σας δείξουμε πώς να **export Excel to PowerPoint** διατηρώντας επεξεργάσιμο κείμενο, πιστότητα διαγραμμάτων και διάταξη—όλα με λίγες γραμμές C#. Στο τέλος θα έχετε ένα έτοιμο προς χρήση αρχείο PPTX που μπορείτε να προσαρμόσετε στο PowerPoint όπως οποιαδήποτε χειροκίνητα δημιουργημένη διαφάνεια.

## Τι Θα Μάθετε

- Πώς να φορτώσετε ένα βιβλίο εργασίας Excel που περιέχει διαγράμματα και σχήματα.  
- Πώς να διαμορφώσετε το `PresentationExportOptions` ώστε τα πλαίσια κειμένου να παραμένουν επεξεργάσιμα (`export editable text`).  
- Πώς να **export Excel chart PowerPoint** και να αποκτήσετε μια καθαρή παρουσίαση.  
- Μικρές παραλλαγές που μπορείτε να εφαρμόσετε όταν χρειάζεται να **convert Excel chart PowerPoint** για διαφορετικές ρυθμίσεις σελίδας ή πολλαπλά φύλλα εργασίας.  

### Προαπαιτούμενα

- Ένα περιβάλλον ανάπτυξης .NET (Visual Studio 2022 ή νεότερο).  
- Aspose.Cells για .NET (δωρεάν δοκιμή ή έκδοση με άδεια).  
- Ένα αρχείο Excel (`ChartWithShape.xlsx`) που περιλαμβάνει τουλάχιστον ένα διάγραμμα και ένα σχήμα που θέλετε να διατηρήσετε επεξεργάσιμο.  

Αν τα έχετε, ας ξεκινήσουμε—χωρίς περιττές πληροφορίες, μόνο μια πρακτική, εκτελέσιμη λύση.

## Δημιουργία PowerPoint από Excel – Βήμα‑βήμα

Κάτω από κάθε βήμα θα προσθέσουμε ένα σύντομο απόσπασμα κώδικα, θα εξηγήσουμε **γιατί** το κάνουμε, και θα επισημάνουμε κοινά προβλήματα. Μπορείτε να αντιγράψετε‑επικολλήσετε το πλήρες παράδειγμα στο τέλος της σελίδας.

### Βήμα 1: Φόρτωση του Excel Workbook

Πρώτα πρέπει να φορτώσουμε το πηγαίο βιβλίο εργασίας στη μνήμη. Το Aspose.Cells διαβάζει το αρχείο και δημιουργεί ένα πλούσιο μοντέλο αντικειμένων που μπορούμε να χειριστούμε.

```csharp
// Step 1: Load the Excel workbook that contains the chart and shape
Workbook workbook = new Workbook("YOUR_DIRECTORY/ChartWithShape.xlsx");

// Quick sanity check – make sure the workbook actually loaded
if (workbook.Worksheets.Count == 0)
    throw new InvalidOperationException("The workbook appears to be empty.");
```

**Γιατί είναι σημαντικό:**  
Η φόρτωση του βιβλίου εργασίας είναι η βάση. Αν η διαδρομή του αρχείου είναι λανθασμένη ή το βιβλίο εργασίας είναι κατεστραμμένο, όλα τα επόμενα βήματα `export excel to powerpoint` θα αποτύχουν. Ο έλεγχος εγκυρότητας σας δίνει άμεση ανατροφοδότηση αντί για ένα ασαφές “file not found” αργότερα.

### Βήμα 2: Προετοιμασία Επιλογών Εξαγωγής

Το Aspose.Cells παρέχει ένα αντικείμενο `PresentationExportOptions` που ελέγχει την εμφάνιση του PPTX. Εδώ αποφασίζετε αν θέλετε το κείμενο να παραμείνει επεξεργάσιμο.

```csharp
// Step 2: Create export options for PowerPoint conversion
PresentationExportOptions exportOptions = new PresentationExportOptions();

// Optional: tweak the slide size (default is 10in x 7.5in)
exportOptions.SlideSize = new SizeF(10, 7.5f);
```

**Γιατί είναι σημαντικό:**  
Χωρίς να ρυθμίσετε το `PresentationExportOptions`, η βιβλιοθήκη χρησιμοποιεί τις προεπιλογές της, οι οποίες μπορεί να μην ταιριάζουν με το εταιρικό σας πρότυπο διαφάνειας. Η προσαρμογή του μεγέθους της διαφάνειας εκ των προτέρων αποτρέπει την ανάγκη χειροκίνητης αλλαγής μεγέθους αργότερα.

### Βήμα 3: Ενεργοποίηση Επεξεργάσιμων Πλαισίων Κειμένου

Η μαγική σημαία `ExportEditableTextBoxes` λέει στο Aspose.Cells να διατηρήσει οποιοδήποτε σχήμα κειμένου ως πλαίσια κειμένου PowerPoint, όχι στατικές εικόνες.

```csharp
// Step 3: Enable editability of text boxes in the resulting presentation
exportOptions.ExportEditableTextBoxes = true;
```

**Γιατί είναι σημαντικό:**  
Αν παραλείψετε αυτή τη γραμμή, το παραγόμενο PPTX θα περιέχει ραστερισμένο κείμενο—δηλαδή δεν μπορείτε να επεξεργαστείτε την ετικέτα ή τη λεζάντα στο PowerPoint. Η ρύθμιση `export editable text` είναι το κλειδί για μια πραγματικά επαναχρησιμοποιήσιμη παρουσίαση.

### Βήμα 4: Εξαγωγή του Φύλλου Εργασίας σε PPTX

Τώρα γράφουμε πραγματικά το αρχείο PPTX. Μπορείτε να επιλέξετε οποιοδήποτε φύλλο εργασίας· εδώ χρησιμοποιούμε το πρώτο (`Worksheets[0]`).

```csharp
// Step 4: Export the first worksheet's page setup to a PPTX file
workbook.Worksheets[0].PageSetup.SaveToPptx("YOUR_DIRECTORY/Result.pptx", exportOptions);
```

**Γιατί είναι σημαντικό:**  
Το `SaveToPptx` σέβεται τις ρυθμίσεις σελίδας (περιθώρια, προσανατολισμό) που ορίσατε στο Excel, έτσι η διαφάνεια αντικατοπτρίζει τη διάταξη που έχετε ήδη σχεδιάσει. Αυτό είναι η ουσία του **export excel chart powerpoint**.

### Βήμα 5: Επαλήθευση του Αποτελέσματος (Προαιρετικό αλλά Συνιστάται)

Μετά τη μετατροπή, ανοίξτε το παραγόμενο `Result.pptx` στο PowerPoint και ελέγξτε:

1. Τα διαγράμματα εμφανίζονται καθαρά και διατηρούν τις σειρές δεδομένων.  
2. Τα πλαίσια κειμένου είναι επιλέξιμα και επεξεργάσιμα.  
3. Το μέγεθος της διαφάνειας ταιριάζει με τις προσδοκίες σας.

Αν κάτι φαίνεται λανθασμένο, επανεξετάστε το `exportOptions`—για παράδειγμα, ίσως χρειαστεί να ορίσετε `exportOptions.IncludePrintArea = true` για να σεβαστείτε μια ονομαστική περιοχή εκτύπωσης.

```csharp
// Optional: open the PPTX automatically (requires System.Diagnostics)
System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
{
    FileName = "YOUR_DIRECTORY/Result.pptx",
    UseShellExecute = true
});
```

### Βήμα 6: Προχωρημένες Παραλλαγές (Εξαγωγή Πολλαπλών Φύλλων)

Συχνά θα θέλετε να **convert excel chart powerpoint** για πολλά φύλλα εργασίας ταυτόχρονα. Κάντε βρόχο πάνω στη συλλογή και δώστε σε κάθε διαφάνεια ένα μοναδικό όνομα:

```csharp
for (int i = 0; i < workbook.Worksheets.Count; i++)
{
    string outputPath = $"YOUR_DIRECTORY/Result_Sheet{i + 1}.pptx";
    workbook.Worksheets[i].PageSetup.SaveToPptx(outputPath, exportOptions);
}
```

**Συμβουλή:** Αν χρειάζεστε όλα τα φύλλα σε ένα *μοναδικό* PPTX, δημιουργήστε ένα νέο αντικείμενο `Presentation`, εισάγετε κάθε διαφάνεια, και αποθηκεύστε μία φορά. Αυτό είναι λίγο πιο πολύπλοκο αλλά σας εξοικονομεί το χειρισμό πολλών αρχείων.

## Πλήρες Παράδειγμα Λειτουργίας

Ακολουθεί ολόκληρο το πρόγραμμα ώστε να το επικολλήσετε σε μια εφαρμογή κονσόλας και να το εκτελέσετε αμέσως.

```csharp
using System;
using System.Drawing;
using Aspose.Cells;
using Aspose.Cells.Export;

class Program
{
    static void Main()
    {
        // 1️⃣ Load workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/ChartWithShape.xlsx");
        if (workbook.Worksheets.Count == 0)
        {
            Console.WriteLine("Workbook is empty – aborting.");
            return;
        }

        // 2️⃣ Set up export options
        PresentationExportOptions exportOptions = new PresentationExportOptions
        {
            SlideSize = new SizeF(10, 7.5f),          // optional custom size
            ExportEditableTextBoxes = true           // <‑‑ keep text boxes editable
        };

        // 3️⃣ Export first worksheet
        string outputPath = "YOUR_DIRECTORY/Result.pptx";
        workbook.Worksheets[0].PageSetup.SaveToPptx(outputPath, exportOptions);
        Console.WriteLine($"PowerPoint created at: {outputPath}");

        // 4️⃣ Open the result automatically (Windows only)
        try
        {
            System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
            {
                FileName = outputPath,
                UseShellExecute = true
            });
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Could not open PPTX automatically: {ex.Message}");
        }
    }
}
```

**Αναμενόμενο αποτέλεσμα:**  
Όταν ανοίξετε το `Result.pptx`, θα δείτε μια διαφάνεια που αντικατοπτρίζει τη διάταξη του φύλλου εργασίας Excel. Οποιοδήποτε διάγραμμα έχετε τοποθετήσει στο Excel εμφανίζεται ως εγγενές διάγραμμα PowerPoint, και η λεζάντα που προσθέσατε ως σχήμα είναι τώρα ένα πλήρως επεξεργάσιμο πλαίσιο κειμένου.

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

- **Λειτουργεί αυτό με βιβλία εργασίας που υποστηρίζουν μακροεντολές (`.xlsm`);**  
  Ναι. Το Aspose.Cells διαβάζει τις μακροεντολές αλλά δεν τις εκτελεί. Η διαδικασία μετατροπής αγνοεί το VBA, έτσι θα λάβετε ακόμη το οπτικό περιεχόμενο.

- **Τι γίνεται αν το φύλλο εργασίας μου περιέχει πολλαπλά διαγράμματα;**  
  Όλα τα ορατά διαγράμματα μεταφέρονται στην ίδια διαφάνεια. Αν χρειάζεστε κάθε διάγραμμα σε ξεχωριστή διαφάνεια, χωρίστε το φύλλο εργασίας ή χρησιμοποιήστε το βρόχο που φαίνεται στο Βήμα 6.

- **Μπορώ να διατηρήσω προσαρμοσμένα θέματα PowerPoint;**  
  Δεν είναι δυνατόν άμεσα κατά την εξαγωγή. Μετά τη μετατροπή μπορείτε να εφαρμόσετε ένα θέμα στο PowerPoint ή προγραμματιστικά μέσω Aspose.Slides.

- **Υπάρχει τρόπος να εξάγετε μόνο μια επιλεγμένη περιοχή;**  
  Ορίστε μια ονομασμένη περιοχή εκτύπωσης στο Excel (`Page Layout → Print Area`) και ενεργοποιήστε `exportOptions.IncludePrintArea = true`.

## Συμπέρασμα

Τώρα ξέρετε πώς να **create PowerPoint from Excel** χρησιμοποιώντας το Aspose.Cells, με πλήρη έλεγχο πάνω στο επεξεργάσιμο κείμενο, την πιστότητα των διαγραμμάτων και το μέγεθος των διαφανειών. Το σύντομο απόσπασμα κώδικα που μοιραστήκαμε καλύπτει το πιο κοινό σενάριο, και οι επιπλέον συμβουλές σας δίνουν ευελιξία όταν χρειάζεται να **export excel to powerpoint** για πολλαπλά φύλλα ή προσαρμοσμένες διατάξεις.  

Είστε έτοιμοι για την επόμενη πρόκληση; Δοκιμάστε να συνδυάσετε αυτήν την προσέγγιση με το **Aspose.Slides** για να προσθέσετε προγραμματιστικά μεταβάσεις, σημειώσεις ομιλητή, ή ακόμη και να ενσωματώσετε τις παραγόμενες διαφάνειες σε μια μεγαλύτερη παρουσίαση. Ή πειραματιστείτε με τη μετατροπή ολόκληρου βιβλίου εργασίας σε ένα πολυ‑διαφάνειας deck—ιδανικό για αυτοματοποιημένες ροές αναφοράς.

Έχετε ερωτήσεις ή ανακαλύψατε κάποιο έξυπνο κόλπο; Αφήστε ένα σχόλιο παρακάτω, και καλή προγραμματιστική!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}