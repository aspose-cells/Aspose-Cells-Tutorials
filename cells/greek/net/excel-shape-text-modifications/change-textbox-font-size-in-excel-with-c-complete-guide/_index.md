---
category: general
date: 2026-05-30
description: Αλλάξτε το μέγεθος γραμματοσειράς του πλαισίου κειμένου στο Excel χρησιμοποιώντας
  C#. Μάθετε πώς να τροποποιήσετε γρήγορα τη γραμματοσειρά του πλαισίου κειμένου στο
  Excel με βήμα‑βήμα κώδικα.
draft: false
keywords:
- change textbox font size
- modify excel textbox font
language: el
og_description: Αλλάξτε το μέγεθος γραμματοσειράς του πλαισίου κειμένου στο Excel
  χρησιμοποιώντας C#. Αυτός ο οδηγός δείχνει πώς να τροποποιήσετε τη γραμματοσειρά
  του πλαισίου κειμένου στο Excel με ασφαλή και αποδοτικό τρόπο.
og_title: Αλλαγή Μεγέθους Γραμματοσειράς Πλαισίου Κειμένου στο Excel με C# – Πλήρης
  Οδηγός
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Change textbox font size in Excel using C#. Learn how to modify excel
    textbox font quickly with step‑by‑step code.
  headline: Change Textbox Font Size in Excel with C# – Complete Guide
  type: TechArticle
- description: Change textbox font size in Excel using C#. Learn how to modify excel
    textbox font quickly with step‑by‑step code.
  name: Change Textbox Font Size in Excel with C# – Complete Guide
  steps:
  - name: Why this matters
    text: Opening the workbook via COM gives us a live object model—meaning any change
      we make reflects instantly in the file. Setting `Visible = false` speeds things
      up and avoids popping windows during automation.
  - name: Why we use `TextFrame2`
    text: '`TextFrame2` is the newer object model introduced with Office 2007. It
      supports advanced typographic features and is generally more reliable than the
      older `TextFrame`. Using it ensures our **change textbox font size** operation
      works across modern Excel versions.'
  - name: 1. Change *all* textboxes on a sheet
    text: '```csharp foreach (Excel.Shape s in xlWorksheet.Shapes) { if (s.Type.HasFlag(Excel.MsoShapeType.msoTextBox))
      { var tr = s.TextFrame2.TextRange; tr.Font.Name = fontName; tr.Font.Size = newSize;
      } } ```'
  - name: 2. Identify a textbox by its **Name** instead of index
    text: 'If you gave your textbox a meaningful name (e.g., “TitleBox”), you can
      fetch it directly:'
  type: HowTo
tags:
- Excel Interop
- C#
- Office Automation
title: Αλλαγή Μεγέθους Γραμματοσειράς Πλαισίου Κειμένου στο Excel με C# – Πλήρης Οδηγός
url: /el/net/excel-shape-text-modifications/change-textbox-font-size-in-excel-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Αλλαγή Μεγέθους Γραμματοσειράς Πλαισίου Κειμένου στο Excel με C# – Πλήρης Οδηγός

Χρειάζεστε **αλλαγή μεγέθους γραμματοσειράς πλαισίου κειμένου** σε ένα φύλλο εργασίας του Excel από C#; Βρίσκεστε στο σωστό μέρος. Είτε δημιουργείτε αναφορές, χτίζετε έναν πίνακα ελέγχου, είτε απλώς τροποποιείτε ένα πρότυπο, η προσαρμογή της εμφάνισης ενός πλαισίου κειμένου μπορεί να κάνει το φύλλο σας να φαίνεται πολύ πιο επαγγελματικό.

Σε αυτό το σεμινάριο θα **τροποποιήσουμε τη γραμματοσειρά του πλαισίου κειμένου στο Excel** πέρα από το μέγεθος — σκέψου οικογένεια γραμματοσειράς, έντονη γραφή και ακόμη και διαχείριση πολλαπλών σχημάτων. Στο τέλος θα έχετε ένα έτοιμο‑για‑εκτέλεση απόσπασμα κώδικα που καλύπτει κάθε πτυχή της διαδικασίας, από το άνοιγμα του βιβλίου εργασίας μέχρι τον καθαρισμό των αντικειμένων COM. Χωρίς περιττές πληροφορίες, μόνο πρακτικός κώδικας που μπορείτε να ενσωματώσετε στο έργο σας σήμερα.

## Προαπαιτούμενα — Τι Θα Χρειαστεί

Πριν προχωρήσουμε, βεβαιωθείτε ότι έχετε τα παρακάτω στον υπολογιστή σας:

| Απαίτηση | Γιατί είναι σημαντικό |
|-------------|----------------|
| **.NET 6+** (ή .NET Framework 4.7.2+) | Παρέχει τον μεταγλωττιστή C# και το runtime. |
| **Microsoft.Office.Interop.Excel** πακέτο NuGet | Μας δίνει τους τύπους COM interop που χρειάζονται για την επικοινωνία με το Excel. |
| **Excel εγκατεστημένο** (οποιαδήποτε πρόσφατη έκδοση) | Το επίπεδο Interop λειτουργεί μόνο όταν υπάρχει η εφαρμογή Office. |
| **Βασικές γνώσεις C#** | Θα ακολουθήσετε εύκολα, αλλά θα εξηγήσουμε κάθε γραμμή. |

Αν λείπει κάποιο από αυτά, κάντε παύση τώρα και εγκαταστήστε το· ο υπόλοιπος οδηγός υποθέτει ότι είναι ήδη στη θέση του.

## Βήμα 1: Ρύθμιση του Έργου και Εισαγωγή Χώρων Ονομάτων

Πρώτα απ' όλα—δημιουργήστε μια νέα εφαρμογή κονσόλας (ή ενσωματώστε το σε υπάρχουσα) και προσθέστε το namespace του interop.

```csharp
using System;
using Excel = Microsoft.Office.Interop.Excel;

namespace ExcelTextboxDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll call the helper method that does the heavy lifting.
            ChangeTextboxFontSize(@"C:\Temp\Sample.xlsx", "Sheet1", 0, 14, "Calibri");
        }
    }
}
```

> **Pro tip:** Αν στοχεύετε σε .NET 6+, προσθέστε το πακέτο `Microsoft.Office.Interop.Excel` μέσω `dotnet add package Microsoft.Office.Interop.Excel`. Αυτό εξασφαλίζει ότι το ψευδώνυμο `Excel` επιλύεται σωστά.

## Βήμα 2: Άνοιγμα του Βιβλίου Εργασίας και Λήψη του Στόχου Φύλλου

Τώρα πρέπει να εκκινήσουμε το Excel, να ανοίξουμε το αρχείο και να κατευθύνουμε στο φύλλο που περιέχει το πλαίσιο κειμένου. Η τοποθέτηση αυτού σε μπλοκ `try/finally` εγγυάται ότι τα αντικείμενα COM θα απελευθερωθούν ακόμη και αν κάτι πάει στραβά.

```csharp
static void ChangeTextboxFontSize(string workbookPath,
                                  string sheetName,
                                  int textboxIndex,
                                  double newSize,
                                  string fontName)
{
    Excel.Application xlApp = null;
    Excel.Workbook xlWorkbook = null;
    Excel.Worksheet xlWorksheet = null;

    try
    {
        xlApp = new Excel.Application
        {
            // Keep Excel hidden; set to true if you want to watch the changes.
            Visible = false,
            DisplayAlerts = false
        };

        xlWorkbook = xlApp.Workbooks.Open(workbookPath);
        xlWorksheet = xlWorkbook.Worksheets[sheetName] as Excel.Worksheet;
        if (xlWorksheet == null)
            throw new ArgumentException($"Worksheet '{sheetName}' not found.");
```

### Γιατί είναι σημαντικό

Το άνοιγμα του βιβλίου εργασίας μέσω COM μας δίνει ένα ζωντανό μοντέλο αντικειμένων — που σημαίνει ότι κάθε αλλαγή αντικατοπτρίζεται άμεσα στο αρχείο. Ορίζοντας `Visible = false` επιταχύνει τη διαδικασία και αποτρέπει το άνοιγμα παραθύρων κατά την αυτοματοποίηση.

## Βήμα 3: Ανάκτηση του Σχήματος Πλαισίου Κειμένου

Το Excel αντιμετωπίζει τα πλαίσια κειμένου ως αντικείμενα `Shape` στη συλλογή `Shapes`, όχι ως ξεχωριστή συλλογή `TextBox`. Γι' αυτό ο κώδικας παρακάτω φαίνεται λίγο διαφορετικός από το απόσπασμα που ίσως έχετε δει στο διαδίκτυο.

```csharp
        // Excel stores all drawing objects (including textboxes) in the Shapes collection.
        Excel.Shapes shapes = xlWorksheet.Shapes;

        // Guard against an out‑of‑range index.
        if (textboxIndex < 0 || textboxIndex >= shapes.Count)
            throw new IndexOutOfRangeException("Textbox index is out of range.");

        // Grab the specific shape; we assume it’s a textbox.
        Excel.Shape textboxShape = shapes.Item(textboxIndex + 1); // COM collections are 1‑based.
        if (!textboxShape.Type.HasFlag(Excel.MsoShapeType.msoTextBox))
            throw new InvalidOperationException("Selected shape is not a textbox.");
```

> **Watch out:** Η συλλογή `Shapes` είναι 1‑based, γι' αυτό προσθέτουμε `+1` στο μηδενικό `textboxIndex` που περνάτε. Η παράλειψη αυτού οδηγεί σε σφάλματα “index out of range” που μπορεί να είναι εκνευριστικά στην αποσφαλμάτωση.

## Βήμα 4: Αλλαγή Μεγέθους Γραμματοσειράς (και Ονόματος) του Πλαισίου Κειμένου

Εδώ τελικά **αλλάζουμε το μέγεθος γραμματοσειράς του πλαισίου κειμένου**. Η ιδιότητα `TextFrame2` μας δίνει πρόσβαση στις επιλογές μορφοποίησης πλούσιου κειμένου, που περιλαμβάνουν `Font.Name` και `Font.Size`.

```csharp
        // Access the text range inside the textbox.
        Excel.TextRange2 textRange = textboxShape.TextFrame2.TextRange;

        // Change the font name – this also “modifies excel textbox font”.
        textRange.Font.Name = fontName;

        // Change the font size – the core of our tutorial.
        textRange.Font.Size = newSize;

        // Optional: make the text bold for extra emphasis.
        // textRange.Font.Bold = Microsoft.Office.Core.MsoTriState.msoTrue;
```

### Γιατί χρησιμοποιούμε το `TextFrame2`

Το `TextFrame2` είναι το νεότερο μοντέλο αντικειμένων που εισήχθη με το Office 2007. Υποστηρίζει προχωρημένα τυπογραφικά χαρακτηριστικά και είναι γενικά πιο αξιόπιστο από το παλαιότερο `TextFrame`. Η χρήση του εξασφαλίζει ότι η **αλλαγή μεγέθους γραμματοσειράς πλαισίου κειμένου** λειτουργεί σε σύγχρονες εκδόσεις του Excel.

## Βήμα 5: Αποθήκευση, Καθαρισμός και Επαλήθευση

Αφού προσαρμόσουμε τη γραμματοσειρά, πρέπει να αποθηκεύσουμε τις αλλαγές και να απελευθερώσουμε κάθε αναφορά COM. Η παράλειψη του καθαρισμού μπορεί να αφήσει ορφανά διεργασίες Excel να τρέχουν στο παρασκήνιο.

```csharp
        // Save the workbook – you can also use SaveAs to create a copy.
        xlWorkbook.Save();

        Console.WriteLine($"Successfully changed textbox font size to {newSize} pt and font to '{fontName}'.");
    }
    catch (Exception ex)
    {
        Console.Error.WriteLine($"Error: {ex.Message}");
    }
    finally
    {
        // Release COM objects in reverse order of creation.
        if (xlWorksheet != null) System.Runtime.InteropServices.Marshal.ReleaseComObject(xlWorksheet);
        if (xlWorkbook != null)
        {
            xlWorkbook.Close(false);
            System.Runtime.InteropServices.Marshal.ReleaseComObject(xlWorkbook);
        }
        if (xlApp != null)
        {
            xlApp.Quit();
            System.Runtime.InteropServices.Marshal.ReleaseComObject(xlApp);
        }

        // Force garbage collection to clean up any remaining RCWs.
        GC.Collect();
        GC.WaitForPendingFinalizers();
    }
}
```

> **Pro tip:** Αν χρειάζεται να **τροποποιήσετε τη γραμματοσειρά του πλαισίου κειμένου στο Excel** σε πολλά φύλλα, τυλίξτε τη λογική μέσα σε βρόχο που διατρέχει το `Workbook.Worksheets`. Απλώς θυμηθείτε να επαναφέρετε το `textboxIndex` για κάθε φύλλο.

## Διαχείριση Ακραίων Περιπτώσεων — Πολλαπλά Πλαίσια Κειμένου και Ελλιπή Σχήματα

Τα πραγματικά φύλλα εργασίας σπάνια περιέχουν μόνο ένα πλαίσιο κειμένου. Παρακάτω παρουσιάζονται δύο γρήγορες στρατηγικές που μπορείτε να υιοθετήσετε χωρίς να ξαναγράψετε ολόκληρη τη μέθοδο.

### 1. Αλλαγή *όλων* των πλαισίων κειμένου σε ένα φύλλο

```csharp
foreach (Excel.Shape s in xlWorksheet.Shapes)
{
    if (s.Type.HasFlag(Excel.MsoShapeType.msoTextBox))
    {
        var tr = s.TextFrame2.TextRange;
        tr.Font.Name = fontName;
        tr.Font.Size = newSize;
    }
}
```

### 2. Ταυτοποίηση πλαισίου κειμένου με το **Όνομα** του αντί για δείκτη

Αν δώσατε στο πλαίσιο κειμένου ένα περιγραφικό όνομα (π.χ., “TitleBox”), μπορείτε να το ανακτήσετε άμεσα:

```csharp
Excel.Shape namedBox = xlWorksheet.Shapes.Item("TitleBox");
namedBox.TextFrame2.TextRange.Font.Size = newSize;
```

Και οι δύο προσεγγίσεις σας επιτρέπουν να **τροποποιήσετε τη γραμματοσειρά του πλαισίου κειμένου στο Excel** με ακρίβεια, ανεξάρτητα από τη δομή του βιβλίου εργασίας.

## Οπτική Επισκόπηση (Προαιρετικό)

Αν προτιμάτε μια γρήγορη οπτική ενδείξη, φανταστείτε το παρακάτω διάγραμμα:

![Screenshot showing Excel worksheet with a highlighted textbox – demonstrates how to change textbox font size](change-textbox-font-size.png)

*Alt text:* *αλλαγή μεγέθους γραμματοσειράς πλαισίου κειμένου στο Excel – επισημασμένο πλαίσιο κειμένου έτοιμο για τροποποίηση γραμματοσειράς.*

## Πλήρες Παράδειγμα Λειτουργίας

Συνδυάζοντας όλα τα παραπάνω, εδώ είναι ένα αρχείο που μπορείτε να αντιγράψετε‑και‑επικολλήσετε σε ένα έργο κονσόλας και να τρέξετε αμέσως (απλώς ενημερώστε τη διαδρομή του αρχείου και το όνομα του φύλλου).

```csharp
using System;
using Excel = Microsoft.Office.Interop.Excel;

namespace ExcelTextboxDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Adjust these parameters for your environment.
            string workbookPath = @"C:\Temp\Sample.xlsx";
            string sheetName = "Sheet1";
            int textboxIndex = 0;          // First textbox on the sheet.
            double newFontSize = 14;       // Desired font size.
            string newFontName = "Calibri";

            ChangeTextboxFontSize(workbookPath, sheetName, textboxIndex, newFontSize, newFontName);
        }

        static void ChangeTextboxFontSize(string workbookPath,
                                          string sheetName,
                                          int textboxIndex,
                                          double newSize,
                                          string fontName)
        {
            Excel.Application xlApp = null;
            Excel.Workbook xlWorkbook = null;
            Excel.Worksheet xlWorksheet = null;

            try
            {
                xlApp = new Excel.Application { Visible = false, DisplayAlerts = false };
                xlWorkbook = xlApp.Workbooks.Open(workbookPath);
                xlWorksheet = xlWorkbook.Worksheets[sheetName] as Excel.Worksheet;

                if (xlWorksheet == null)


## Τι Θα Μάθετε Στη Σειρά;

- [Changing Font Size in Excel](/cells/english/net/working-with-fonts-in-excel/changing-font-size/)
- [How to Customize Font Size in Excel Cells Using Aspose.Cells .NET | Complete Guide](/cells/english/net/formatting/customize-font-size-excel-aspose-cells-dotnet/)
- [How to Set Font Styles in Excel Using Aspose.Cells for .NET (Step-by-Step Guide)](/cells/english/net/formatting/aspose-cells-dotnet-set-font-styles-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}