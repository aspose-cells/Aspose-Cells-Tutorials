---
category: general
date: 2026-02-15
description: πώς να αντιγράψετε τη γραμματοσειρά και να εφαρμόσετε στυλ κελιού σε
  C# με ένα απλό παράδειγμα. Μάθετε πώς να λαμβάνετε το στυλ κελιού και να χρησιμοποιείτε
  τη μορφοποίηση κελιού για να ορίσετε το μέγεθος γραμματοσειράς του πεδίου κειμένου.
draft: false
keywords:
- how to copy font
- apply cell style
- get cell style
- use cell formatting
- set textbox font size
language: el
og_description: πώς να αντιγράψετε τη γραμματοσειρά από ένα κελί φύλλου εργασίας και
  να εφαρμόσετε το στυλ κελιού σε ένα TextBox. Αυτός ο οδηγός δείχνει πώς να λάβετε
  το στυλ κελιού, να χρησιμοποιήσετε τη μορφοποίηση κελιού και να ορίσετε το μέγεθος
  γραμματοσειράς του TextBox.
og_title: πώς να αντιγράψετε τη γραμματοσειρά από ένα κελί του Excel – Πλήρης οδηγός
  C#
tags:
- C#
- EPPlus
- UI‑grid
- Excel‑interop
title: Πώς να αντιγράψετε τη γραμματοσειρά από ένα κελί του Excel σε ένα TextBox –
  Οδηγός βήμα‑προς‑βήμα
url: /el/net/working-with-fonts-in-excel/how-to-copy-font-from-an-excel-cell-to-a-textbox-step-by-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# πώς να αντιγράψετε τη γραμματοσειρά από ένα κελί Excel σε ένα TextBox – Πλήρες C# Tutorial

Έχετε ποτέ χρειαστεί να **αντιγράψετε τη γραμματοσειρά** από ένα κελί λογιστικού φύλλου και να κάνετε ένα UI text box να φαίνεται ακριβώς το ίδιο; Δεν είστε ο μόνος. Σε πολλά εργαλεία αναφοράς ή προσαρμοσμένα dashboards, θα βρείτε τον εαυτό σας να αντλεί δεδομένα από το Excel και στη συνέχεια προσπαθεί να διατηρήσει την οπτική πιστότητα—συγγενή γραμματοσειράς, μέγεθος και χρώμα—ακέραια.  

Τα καλά νέα είναι ότι με λίγες μόνο γραμμές C# μπορείτε να **λάβετε το στυλ του κελιού**, να διαβάσετε τις ιδιότητες της γραμματοσειράς του, και να **εφαρμόσετε το στυλ του κελιού** σε οποιοδήποτε στοιχείο ελέγχου text‑box. Σε αυτό το tutorial θα περάσουμε από ένα πλήρες, εκτελέσιμο παράδειγμα που δείχνει πώς να **χρησιμοποιήσετε τη μορφοποίηση κελιού** και ακόμη **ορίσετε το μέγεθος γραμματοσειράς του textbox** προγραμματιστικά.

---

## Τι Θα Μάθετε

- Πώς να ανακτήσετε ένα αντικείμενο `TextBox` από ένα στοιχείο πλέγματος (`gridJs` στο παράδειγμά μας)
- Πώς να διαβάσετε τη γραμματοσειρά, το μέγεθος και το χρώμα από ένα συγκεκριμένο κελί Excel (`B2`)
- Πώς να αντιγράψετε αυτά τα χαρακτηριστικά γραμματοσειράς στο text box ώστε το UI να αντικατοπτρίζει το λογιστικό φύλλο
- Κοινά προβλήματα (π.χ., μετατροπή χρώματος) και μερικές **pro tips** για να διατηρήσετε τον κώδικά σας ανθεκτικό
- Ένα έτοιμο‑για‑εκτέλεση απόσπασμα κώδικα που μπορείτε να ενσωματώσετε σε μια εφαρμογή console ή WinForms

**Προαπαιτούμενα**  
Θα πρέπει να έχετε:

1. .NET 6+ (ή .NET Framework 4.8) εγκατεστημένο  
2. Το πακέτο EPPlus NuGet (για διαχείριση Excel)  
3. Ένα στοιχείο πλέγματος που εκθέτει ένα λεξικό `TextBoxes` (το παράδειγμα χρησιμοποιεί ένα φανταστικό `gridJs` αλλά η ιδέα λειτουργεί με οποιαδήποτε βιβλιοθήκη UI)

Τώρα, ας βάλουμε τα χέρια μας στη δουλειά.

## Βήμα 1: Ρυθμίστε το Έργο και Φορτώστε το Φύλλο Εργασίας

Πρώτα, δημιουργήστε ένα νέο έργο console ή WinForms και προσθέστε το EPPlus:

```bash
dotnet add package EPPlus --version 6.*
```

Στη συνέχεια, φορτώστε το βιβλίο εργασίας και πάρτε το κελί του οποίου το στυλ θέλετε να αντιγράψετε.

```csharp
using OfficeOpenXml;
using OfficeOpenXml.Style;
using System.Drawing;

// ...

// Load the Excel file (make sure the file exists at the given path)
var fileInfo = new FileInfo(@"C:\Data\Sample.xlsx");
using var package = new ExcelPackage(fileInfo);
ExcelWorksheet ws = package.Workbook.Worksheets["Sheet1"]; // adjust sheet name if needed

// Retrieve the style of cell B2
ExcelStyle cellStyle = ws.Cells["B2"].Style;
```

**Γιατί είναι σημαντικό:** Το EPPlus σας δίνει άμεση πρόσβαση στο αντικείμενο `Style`, το οποίο περιέχει το υπο‑αντικείμενο `Font`. Από εκεί μπορείτε να διαβάσετε `Name`, `Size` και `Color`. Αυτό είναι ο πυρήνας της λειτουργίας **get cell style**.

## Βήμα 2: Πάρτε το Στόχο TextBox από το Πλέγμα Σας

Υποθέτοντας ότι το UI πλέγμα σας (`gridJs`) αποθηκεύει τα text boxes σε ένα λεξικό με κλειδί το όνομα της στήλης, μπορείτε να ανακτήσετε αυτό που θέλετε ως εξής:

```csharp
// Fake grid class for illustration – replace with your actual grid component
var gridJs = new MyGrid(); // MyGrid is a placeholder for your UI control

// Step 1: Retrieve the "Notes" text box from the grid
var notesTextBox = gridJs.TextBoxes["Notes"];
```

Αν χρησιμοποιείτε WinForms, το `notesTextBox` μπορεί να είναι ένα στοιχείο ελέγχου `TextBox`; για WPF μπορεί να είναι ένα στοιχείο `TextBox`, και για ένα web‑based πλέγμα μπορεί να είναι ένα αντικείμενο JavaScript interop. Το βασικό σημείο είναι ότι έχετε μια αναφορά που μπορείτε να χειριστείτε.

## Βήμα 3: Μεταφορά της Γραμματοσειράς

Τώρα που έχουμε τόσο το στυλ πηγής όσο και το στοιχείο προορισμού, αντιγράψτε τη γραμματοσειρά.

```csharp
// Apply the cell's font family to the text box
notesTextBox.FontFamily = cellStyle.Font.Name;
```

**Pro tip:** Δεν εκθέτουν όλα τα UI frameworks την ιδιότητα `FontFamily` που δέχεται μια απλή συμβολοσειρά. Στα WinForms θα ορίσετε `notesTextBox.Font = new Font(cellStyle.Font.Name, notesTextBox.Font.Size);`. Προσαρμόστε ανάλογα.

## Βήμα 4: Μεταφορά του Μεγέθους Γραμματοσειράς

Το μέγεθος γραμματοσειράς αποθηκεύεται ως `float` στο EPPlus. Εφαρμόστε το άμεσα:

```csharp
// Apply the cell's font size to the text box
notesTextBox.FontSize = cellStyle.Font.Size;
```

Αν το στοιχείο σας χρησιμοποιεί points (όπως η πλειονότητα), μπορείτε να αναθέσετε την τιμή χωρίς μετατροπή. Για πλέγματα βασισμένα σε CSS μπορεί να χρειαστεί να προσθέσετε το `"pt"`.

## Βήμα 5: Μεταφορά του Χρώματος Γραμματοσειράς

Η μετατροπή χρώματος είναι το πιο δύσκολο μέρος επειδή το EPPlus αποθηκεύει τα χρώματα ως ακέραιους ARGB, ενώ πολλά UI frameworks αναμένουν ένα `System.Drawing.Color` ή μια CSS hex συμβολοσειρά.

```csharp
// Apply the cell's font colour to the text box
// EPPlus stores colour as a System.Drawing.Color when using .Color property
var excelColor = cellStyle.Font.Color?.GetColor();

// Fallback to black if the cell has no explicit colour
var safeColor = excelColor ?? Color.Black;

// Convert to the format your UI expects (example for WinForms)
notesTextBox.FontColor = safeColor;
```

> **Γιατί λειτουργεί:** Η `GetColor()` επιλύει χρώματα βασισμένα σε θέμα και επιστρέφει ένα συγκεκριμένο `System.Drawing.Color`. Αν το κελί χρησιμοποιεί το προεπιλεγμένο χρώμα (χωρίς ρητή ρύθμιση), ορίζουμε προεπιλογή σε μαύρο για να αποφύγουμε εξαιρέσεις null reference.

## Πλήρες Παράδειγμα Λειτουργίας

Συνδυάζοντας όλα, εδώ είναι μια ελάχιστη εφαρμογή console που διαβάζει ένα αρχείο Excel, εξάγει τη γραμματοσειρά από το **B2**, και την εφαρμόζει σε ένα ψεύτικο text box.

```csharp
using OfficeOpenXml;
using OfficeOpenXml.Style;
using System;
using System.Collections.Generic;
using System.Drawing;

namespace FontCopyDemo
{
    // Mock grid control – replace with your real UI component
    public class MyGrid
    {
        public Dictionary<string, TextBoxMock> TextBoxes { get; } = new()
        {
            { "Notes", new TextBoxMock() }
        };
    }

    // Simple text box representation for demonstration
    public class TextBoxMock
    {
        public string FontFamily { get; set; }
        public float FontSize { get; set; }
        public Color FontColor { get; set; }

        public override string ToString()
        {
            return $"FontFamily: {FontFamily}, FontSize: {FontSize}, FontColor: {FontColor.Name}";
        }
    }

    class Program
    {
        static void Main()
        {
            // 1️⃣ Load Excel worksheet
            var fileInfo = new FileInfo(@"C:\Data\Sample.xlsx");
            using var package = new ExcelPackage(fileInfo);
            var ws = package.Workbook.Worksheets["Sheet1"];
            var cellStyle = ws.Cells["B2"].Style;

            // 2️⃣ Grab the target TextBox from the grid
            var gridJs = new MyGrid();
            var notesTextBox = gridJs.TextBoxes["Notes"];

            // 3️⃣ Apply font family
            notesTextBox.FontFamily = cellStyle.Font.Name;

            // 4️⃣ Apply font size
            notesTextBox.FontSize = cellStyle.Font.Size;

            // 5️⃣ Apply font colour (with safety net)
            var excelColor = cellStyle.Font.Color?.GetColor();
            notesTextBox.FontColor = excelColor ?? Color.Black;

            // Output the result for verification
            Console.WriteLine("TextBox after copying font:");
            Console.WriteLine(notesTextBox);
        }
    }
}
```

**Αναμενόμενη έξοδος (υπόθεση ότι το B2 χρησιμοποιεί Arial, 12 pt, μπλε):**

```
TextBox after copying font:
FontFamily: Arial, FontSize: 12, FontColor: Blue
```

Εκτελέστε το πρόγραμμα, ανοίξτε το UI σας, και θα δείτε ότι το text box “Notes” τώρα αντικατοπτρίζει ακριβώς το στυλ γραμματοσειράς του κελιού **B2**. Δεν απαιτείται χειροκίνητη ρύθμιση.

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

### Τι γίνεται αν το κελί χρησιμοποιεί χρώμα θέματος αντί για ρητή τιμή RGB;

Η `GetColor()` του EPPlus επιλύει αυτόματα τα χρώματα θέματος σε ένα συγκεκριμένο `System.Drawing.Color`. Ωστόσο, αν χρησιμοποιείτε μια παλαιότερη βιβλιοθήκη που επιστρέφει μόνο τον δείκτη θέματος, θα πρέπει να αντιστοιχίσετε αυτόν τον δείκτη σε μια παλέτα χρωμάτων μόνοι σας.

### Μπορώ να αντιγράψω άλλα χαρακτηριστικά στυλ (π.χ., έντονη, πλάγια);

Απόλυτα. Το αντικείμενο `ExcelStyle.Font` εκθέτει επίσης `Bold`, `Italic`, `Underline` και `Strike`. Απλώς ορίστε τις αντίστοιχες ιδιότητες στο UI στοιχείο σας:

```csharp
notesTextBox.FontBold = cellStyle.Font.Bold;
notesTextBox.FontItalic = cellStyle.Font.Italic;
```

### Τι γίνεται αν το στοιχείο πλέγματος δεν εκθέτει ιδιότητα `FontColor`;

Τα περισσότερα σύγχρονα UI frameworks το κάνουν, αλλά αν το δικό σας δέχεται μόνο μια CSS συμβολοσειρά, μετατρέψτε το `Color` σε hex:

```csharp
string hex = $"#{notesTextBox.FontColor.R:X2}{notesTextBox.FontColor.G:X2}{notesTextBox.FontColor.B:X2}";
notesTextBox.Style["color"] = hex; // for web‑based grids
```

### Πώς να διαχειριστώ πολλαπλά κελιά ταυτόχρονα;

Κάντε βρόχο πάνω στην επιθυμητή περιοχή, ανακτήστε το στυλ κάθε κελιού και εφαρμόστε το στο αντίστοιχο text box. Θυμηθείτε να αποθηκεύετε τα αντικείμενα στυλ στην κρυφή μνήμη αν επεξεργάζεστε πολλές γραμμές για να αποφύγετε επιπτώσεις στην απόδοση.

## Pro Tips & Συχνά Πιθανά Σφάλματα

- **Cache the ExcelPackage** – το άνοιγμα και κλείσιμο του αρχείου για κάθε κελί είναι δαπανηρό. Φορτώστε το βιβλίο εργασίας μία φορά, μετά επαναχρησιμοποιήστε το αντικείμενο `ExcelWorksheet`.
- **Watch out for null colours** – ένα κελί που κληρονομεί το προεπιλεγμένο χρώμα επιστρέφει `null`. Πάντα παρέχετε εναλλακτική (μαύρο ή το προεπιλεγμένο του ελέγχου).
- **Mind DPI scaling** – αν στοχεύετε σε οθόνες υψηλής DPI, τα μεγέθη γραμματοσειράς μπορεί να φαίνονται ελαφρώς μεγαλύτερα. Προσαρμόστε χρησιμοποιώντας `Graphics.DpiX` αν χρειάζεται.
- **Thread safety** – το EPPlus δεν είναι thread‑safe. Αν επεξεργάζεστε πολλά φύλλα παράλληλα, δημιουργήστε ξεχωριστό `ExcelPackage` ανά νήμα.

## Συμπέρασμα

Τώρα γνωρίζετε **πώς να αντιγράψετε τη γραμματοσειρά** από ένα κελί Excel και **να εφαρμόσετε το στυλ κελιού** σε οποιοδήποτε στοιχείο ελέγχου text‑box χρησιμοποιώντας C#. Ανακτώντας το `Style` του κελιού, εξάγοντας τις ιδιότητες `Font` του, και αναθέτοντάς τες στο UI στοιχείο, διατηρείτε την οπτική συνέπεια χωρίς χειροκίνητη αντιγραφή.  

Η πλήρης λύση—φόρτωση του βιβλίου εργασίας, λήψη του στυλ κελιού, και ορισμός της γραμματοσειράς, του μεγέθους και του χρώματος του textbox—καλύπτει τον πυρήνα της **use cell formatting** και δείχνει πώς να **set textbox font size** σωστά.  

Στη συνέχεια, δοκιμάστε να επεκτείνετε το παράδειγμα για να αντιγράψετε χρώματα φόντου, περιθώρια ή ακόμη και ολόκληρο το περιεχόμενο των κελιών. Αν εργάζεστε με μια βιβλιοθήκη data‑grid που υποστηρίζει πλούσια απόδοση κελιών, μπορείτε τώρα να της παρέχετε τις ακριβώς ίδιες πληροφορίες στυλ που εξάγατε από το Excel, διατηρώντας το UI και τις αναφορές σας τέλεια συγχρονισμένες.  

Έχετε περισσότερες ερωτήσεις; Αφήστε ένα σχόλιο ή εξερευνήστε συναφή θέματα όπως “dynamic Excel‑to‑UI binding” και “theme‑aware colour conversion”. Καλή προγραμματιστική!

![παράδειγμα αντιγραφής γραμματοσειράς](placeholder-image.jpg "πώς να αντιγράψετε τη γραμματοσειρά από κελί Excel σε TextBox")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}