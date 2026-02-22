---
category: general
date: 2026-02-21
description: Μάθετε πώς να κάνετε το κείμενο του TextBox έντονο, να αλλάξετε το μέγεθος
  γραμματοσειράς του TextBox και να φορτώσετε ένα βιβλίο εργασίας Excel σε C# χρησιμοποιώντας
  το Aspose.Cells σε ένα πλήρες, εκτελέσιμο παράδειγμα.
draft: false
keywords:
- make textbox text bold
- change textbox font size
- load excel workbook c#
- format excel shape text
language: el
og_description: Κάντε το κείμενο του TextBox έντονο σε ένα αρχείο Excel χρησιμοποιώντας
  C#. Αυτό το σεμινάριο δείχνει επίσης πώς να αλλάξετε το μέγεθος γραμματοσειράς του
  TextBox και πώς να φορτώσετε ένα βιβλίο εργασίας Excel με C# χρησιμοποιώντας το
  Aspose.Cells.
og_title: Κάντε το κείμενο του TextBox έντονο στο Excel με C# – Πλήρης Οδηγός
tags:
- C#
- Aspose.Cells
- Excel automation
title: Κάντε το κείμενο του TextBox έντονο στο Excel με C# – Οδηγός βήμα‑βήμα
url: /el/net/excel-shape-text-modifications/make-textbox-text-bold-in-excel-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Κάντε το κείμενο του TextBox έντονο στο Excel με C# – Οδηγός βήμα‑βήμα

Θέλετε να **κάνετε το κείμενο του TextBox έντονο** σε ένα αρχείο Excel χρησιμοποιώντας C#; Σε αυτό το tutorial θα σας δείξουμε ακριβώς πώς να *φορτώσετε ένα Excel workbook*, **αλλάξετε το μέγεθος γραμματοσειράς του TextBox** και να μορφοποιήσετε το κείμενο του σχήματος με το Aspose.Cells.  
Αν έχετε ποτέ κοίταξει σε ένα απλό λογιστικό φύλλο και σκεφτείτε «το textbox μου πρέπει να ξεχωρίζει», βρίσκεστε στο σωστό μέρος.

Θα περάσουμε από κάθε γραμμή κώδικα, θα εξηγήσουμε γιατί κάθε κλήση είναι σημαντική, και ακόμη θα καλύψουμε τι να κάνετε όταν το φύλλο εργασίας δεν περιέχει καθόλου text boxes. Στο τέλος θα έχετε ένα επαναχρησιμοποιήσιμο snippet που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο .NET—χωρίς μυστικούς συνδέσμους «δείτε την τεκμηρίωση».

## Τι θα χρειαστείτε

- **Aspose.Cells for .NET** (δωρεάν δοκιμή ή έκδοση με άδεια) – το API που χρησιμοποιούμε για να επεξεργαστούμε σχήματα Excel.  
- .NET 6 ή νεότερο (ο κώδικας λειτουργεί επίσης με .NET Framework 4.7+).  
- Ένα απλό αρχείο Excel (`input.xlsx`) που ήδη περιέχει τουλάχιστον ένα textbox στο πρώτο φύλλο.  

Αυτό είναι όλο. Χωρίς επιπλέον πακέτα NuGet, χωρίς COM interop, μόνο καθαρό C#.

## Κάντε το κείμενο του TextBox έντονο – Φόρτωση Workbook και Πρόσβαση στο Shape

Το πρώτο βήμα είναι να ανοίξετε το workbook και να πάρετε το textbox που θέλετε να επεξεργαστείτε.  
Εκτελούμε επίσης έναν γρήγορο έλεγχο ασφαλείας ώστε ο κώδικας να μην καταρρεύσει αν το φύλλο είναι κενό.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Load the workbook (load excel workbook c#)
        var workbookPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(workbookPath);

        // Step 2: Get the first worksheet
        Worksheet worksheet = workbook.Worksheets[0];

        // Verify that at least one TextBox exists
        if (worksheet.TextBoxes.Count == 0)
        {
            Console.WriteLine("No TextBoxes found on the first sheet.");
            return;
        }

        // Step 3: Access the first TextBox shape
        Shape textBox = worksheet.TextBoxes[0];

        // From here on we can format the shape's text
```

**Γιατί είναι σημαντικό:**  
*Η φόρτωση του workbook* μας δίνει ένα αντικείμενο `Workbook` που αντιπροσωπεύει ολόκληρο το αρχείο στη μνήμη. Η πρόσβαση στο `Worksheets[0]` είναι ασφαλής επειδή κάθε αρχείο Excel έχει τουλάχιστον ένα φύλλο. Η προφυλακτική εντολή (`if (worksheet.TextBoxes.Count == 0)`) αποτρέπει ένα `IndexOutOfRangeException`—ένα κοινό πρόβλημα όταν αυτοματοποιείτε υπάρχοντα αρχεία.

## Αλλαγή μεγέθους γραμματοσειράς του TextBox

Πριν κάνουμε το κείμενο έντονο, ας βεβαιωθούμε ότι το μέγεθος είναι ακριβώς αυτό που χρειάζεστε.  
Η αλλαγή του μεγέθους είναι τόσο απλή όσο η τροποποίηση της ιδιότητας `Font.Size`.

```csharp
        // Step 4: Set the font name (optional but often useful)
        textBox.Font.Name = "Calibri";

        // Step 5: Change the font size (change textbox font size)
        textBox.Font.Size = 12; // 12 points is a comfortable default
```

**Συμβουλή:**  
Αν χρειάζεστε δυναμικό μέγεθος βάσει εισόδου χρήστη, απλώς αντικαταστήστε το `12` με μια μεταβλητή. Το αντικείμενο `Font` μοιράζεται σε όλο το shape, έτσι η αλλαγή μεγέθους επηρεάζει αμέσως κάθε χαρακτήρα μέσα στο textbox.

## Κάντε το κείμενο του TextBox έντονο – Η κύρια ενέργεια

Τώρα για τη βασική λειτουργία: να κάνετε το κείμενο έντονο.  
Η σημαία `IsBold` αλλάζει το βάρος της γραμματοσειράς χωρίς να τροποποιεί άλλα στυλ.

```csharp
        // Step 6: Make the text bold (make textbox text bold)
        textBox.Font.IsBold = true;
```

**Τι συμβαίνει στο παρασκήνιο;**  
Το Aspose.Cells αποθηκεύει τη μορφοποίηση κειμένου σε ένα αντικείμενο `Font` που είναι συνδεδεμένο με το shape. Ορίζοντας `IsBold = true` ενημερώνει το υποκείμενο XML (`<b>1</b>`) που το Excel διαβάζει όταν αποδίδει το φύλλο. Αυτή είναι μια **μη καταστροφική** λειτουργία—αν αργότερα ορίσετε `IsBold = false`, το κείμενο επιστρέφει στο κανονικό βάρος.

## Αποθήκευση του τροποποιημένου Workbook

Αφού ολοκληρωθεί η μορφοποίηση, γράφουμε τις αλλαγές πίσω στο δίσκο.  
Μπορείτε να αντικαταστήσετε το αρχικό αρχείο ή, όπως φαίνεται εδώ, να δημιουργήσετε ένα νέο ώστε να διατηρήσετε το αρχικό ανέπαφο.

```csharp
        // Step 7: Save the modified workbook
        var outputPath = @"YOUR_DIRECTORY\output.xlsx";
        workbook.Save(outputPath);

        Console.WriteLine($"Workbook saved. TextBox is now bold and 12pt Calibri in '{outputPath}'.");
    }
}
```

**Αναμενόμενο αποτέλεσμα:**  
Ανοίξτε το `output.xlsx` στο Excel. Το πρώτο textbox στο πρώτο φύλλο πρέπει να εμφανίζει το κείμενό του σε **Calibri 12 pt, έντονο**. Κανένα άλλο shape δεν επηρεάζεται.

## Μορφοποίηση κειμένου Excel Shape – Επιπλέον επιλογές στυλ (Προαιρετικό)

Ενώ ο κύριος στόχος είναι να **κάνετε το κείμενο του TextBox έντονο**, ίσως θέλετε επίσης:

| Επιλογή | Κώδικας | Πότε να χρησιμοποιηθεί |
|--------|--------------|------------------------|
| Italic | `textBox.Font.IsItalic = true;` | Τονίζοντας υπότιτλο |
| Text color | `textBox.Font.Color = System.Drawing.Color.DarkBlue;` | Χρώματα εταιρείας |
| Alignment | `textBox.AlignmentHorizontal = TextAlignmentType.Center;` | Κεντραρισμένες επικεφαλίδες |
| Multiple TextBoxes | Loop through `worksheet.TextBoxes` | Μαζική μορφοποίηση |

```csharp
// Example: Apply a blue color and center alignment to all textboxes
foreach (Shape tb in worksheet.TextBoxes)
{
    tb.Font.Color = System.Drawing.Color.Blue;
    tb.AlignmentHorizontal = TextAlignmentType.Center;
}
```

Αυτές οι επιπλέον ρυθμίσεις δείχνουν πώς το *format excel shape text* μπορεί να επεκταθεί πέρα από το απλό έντονο.

## Ακραίες περιπτώσεις & Συνηθισμένα προβλήματα

1. **Δεν υπάρχουν TextBoxes στο φύλλο** – Η προφυλακτική εντολή που προσθέσαμε (`if (worksheet.TextBoxes.Count == 0)`) εξέρχεται ήρεμα και ενημερώνει τον χρήστη.  
2. **Κρυφά worksheets** – Τα κρυφά φύλλα είναι ακόμα προσβάσιμα μέσω της συλλογής `Worksheets`; απλώς βεβαιωθείτε ότι αναφέρετε το σωστό δείκτη.  
3. **Μεγάλα αρχεία** – Η φόρτωση ενός τεράστιου workbook μπορεί να καταναλώσει μνήμη. Σκεφτείτε να χρησιμοποιήσετε το `Workbook.LoadOptions` για να φορτώσετε μόνο τα απαραίτητα τμήματα.  
4. **Διαφορετικές εκδόσεις Excel** – Το Aspose.Cells λειτουργεί με `.xls`, `.xlsx` και ακόμη και `.xlsb`. Ο ίδιος κώδικας λειτουργεί σε όλες τις εκδόσεις, αλλά παλαιότερα Excel μπορεί να αγνοούν ορισμένα νεότερα χαρακτηριστικά γραμματοσειράς.

## Πλήρες λειτουργικό παράδειγμα (Έτοιμο για αντιγραφή‑επικόλληση)

```csharp
using System;
using Aspose.Cells;

class MakeTextboxBoldDemo
{
    static void Main()
    {
        // Load the workbook (load excel workbook c#)
        var inputFile = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(inputFile);

        // Get the first worksheet
        Worksheet sheet = workbook.Worksheets[0];

        // Ensure a textbox exists
        if (sheet.TextBoxes.Count == 0)
        {
            Console.WriteLine("No textbox found on the first sheet.");
            return;
        }

        // Access the first textbox
        Shape txtBox = sheet.TextBoxes[0];

        // Set font name and size (change textbox font size)
        txtBox.Font.Name = "Calibri";
        txtBox.Font.Size = 12;

        // Make the text bold (make textbox text bold)
        txtBox.Font.IsBold = true;

        // Optional: extra styling (format excel shape text)
        txtBox.Font.Color = System.Drawing.Color.DarkGreen;
        txtBox.AlignmentHorizontal = TextAlignmentType.Center;

        // Save the result
        var outputFile = @"YOUR_DIRECTORY\output.xlsx";
        workbook.Save(outputFile);

        Console.WriteLine($"Saved: {outputFile}");
    }
}
```

Εκτελέστε το πρόγραμμα, ανοίξτε το δημιουργημένο `output.xlsx` και θα δείτε το έντονο κείμενο Calibri 12 pt μέσα στο textbox. Απλό, έτσι δεν είναι;

## Συμπέρασμα

Τώρα ξέρετε **πώς να κάνετε το κείμενο του TextBox έντονο** σε ένα Excel workbook χρησιμοποιώντας C#, πώς να **αλλάξετε το μέγεθος γραμματοσειράς του TextBox**, και τα βασικά της **φόρτωσης ενός Excel workbook με C#** με το Aspose.Cells. Το πλήρες παράδειγμα παραπάνω είναι έτοιμο να ενσωματωθεί σε οποιοδήποτε έργο, και έχετε επίσης δει τρόπους για **μορφοποίηση κειμένου Excel shape** για πιο πλούσιο στυλ.

Τι θα ακολουθήσει; Δοκιμάστε να κάνετε βρόχο σε κάθε worksheet για να κάνετε έντονα όλα τα textboxes, ή συνδυάστε το με δημιουργία περιεχομένου βάσει δεδομένων—ίσως να γεμίσετε το textbox με τιμές από μια βάση δεδομένων. Οι ίδιες αρχές ισχύουν και ο κώδικας παραμένει καθαρός.

Έχετε κάποια παραλλαγή που θέλετε να μοιραστείτε, ή αντιμετωπίσατε κάποιο απρόσμενο σφάλμα; Αφήστε ένα σχόλιο και ας συνεχίσουμε τη συζήτηση. Καλή προγραμματιστική! 

![make textbox text bold in Excel using C#](/images/make-textbox-text-bold-csharp.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}