---
category: general
date: 2026-02-21
description: Δημιουργήστε στυλ κελιού σε C# γρήγορα. Μάθετε πώς να εφαρμόζετε στυλ
  σε ένα κελί, να κεντράρετε το κείμενο στο κελί, να ορίσετε την ευθυγράμμιση του
  κελιού και να κατακτήσετε τη μορφοποίηση των κελιών.
draft: false
keywords:
- create cell style
- apply style to cell
- center text in cell
- set cell alignment
- how to center text
language: el
og_description: Δημιουργήστε στυλ κελιού σε C# και μάθετε πώς να εφαρμόζετε το στυλ
  σε ένα κελί, να κεντράρετε το κείμενο στο κελί και να ορίσετε την ευθυγράμμιση του
  κελιού με έναν σαφή, βήμα‑βήμα οδηγό.
og_title: Δημιουργία στυλ κελιού σε C# – Εφαρμογή στυλ σε κελί και κεντράρισμα κειμένου
tags:
- C#
- Aspose.Cells
- Excel automation
title: Δημιουργία στυλ κελιού σε C# – Πώς να εφαρμόσετε στυλ σε ένα κελί και να κεντράρετε
  το κείμενο
url: /el/net/excel-formatting-and-styling/create-cell-style-in-c-how-to-apply-style-to-a-cell-and-cent/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία στυλ κελιού σε C# – Πλήρης Οδηγός για Εφαρμογή Στυλ και Στοίχιση Κειμένου στο Κέντρο

Έχετε ποτέ χρειαστεί να **create cell style** σε ένα φύλλο εργασίας Excel αλλά δεν ήξερατε από πού να ξεκινήσετε; Δεν είστε μόνοι. Σε πολλά έργα αυτοματοποίησης, η δυνατότητα **apply style to cell** αντικειμένων είναι η διαφορά μεταξύ ενός απλού λογιστικού φύλλου και μιας επαγγελματικής αναφοράς.  

Σε αυτό το tutorial θα περάσουμε βήμα-βήμα ένα πλήρες, εκτελέσιμο παράδειγμα που σας δείχνει **how to center text** μέσα σε ένα κελί, να ορίσετε την στοίχιση και να προσθέσετε ένα λεπτό περίγραμμα — όλα σε λίγες μόνο γραμμές C#. Στο τέλος θα γνωρίζετε ακριβώς γιατί κάθε μέρος είναι σημαντικό και πώς να το προσαρμόσετε στις δικές σας περιπτώσεις.

## Τι Θα Αποκομίσετε

- Μια σαφής κατανόηση της ροής εργασίας **create cell style** χρησιμοποιώντας το Aspose.Cells (ή οποιαδήποτε παρόμοια βιβλιοθήκη).
- Ο ακριβής κώδικας που μπορείτε να αντιγράψετε‑επικολλήσετε σε μια εφαρμογή console για **apply style to cell**.
- Κατανόηση του **center text in cell**, **set cell alignment**, και διαχείριση ειδικών περιπτώσεων όπως συγχωνευμένα κελιά ή προσαρμοσμένες μορφές αριθμών.
- Συμβουλές για την επέκταση του στυλ — διαφορετικές γραμματοσειρές, χρώματα φόντου ή υπό συνθήκη μορφοποίηση.

> **Προαπαιτούμενο:** Visual Studio 2022 (ή οποιοδήποτε IDE C#) και το πακέτο NuGet Aspose.Cells για .NET. Δεν απαιτούνται άλλες εξαρτήσεις.

---

## Βήμα 1: Ρύθμιση του Έργου σας και Εισαγωγή Namespaces

Πριν μπορέσουμε να **create cell style**, χρειαζόμαστε ένα έργο που να αναφέρει τη βιβλιοθήκη Excel.

```csharp
// Program.cs – entry point
using System;
using Aspose.Cells;   // Make sure the Aspose.Cells NuGet package is installed

class Program
{
    static void Main()
    {
        // We'll fill in the rest of the steps here.
    }
}
```

*Γιατί είναι σημαντικό:* Η εισαγωγή του `Aspose.Cells` μας δίνει πρόσβαση στις κλάσεις `Workbook`, `Worksheet`, `Style` και `Border`. Αν χρησιμοποιείτε διαφορετική βιβλιοθήκη (π.χ., EPPlus), τα ονόματα των κλάσεων αλλάζουν αλλά η έννοια παραμένει η ίδια.

---

## Βήμα 2: Δημιουργία Workbook και Λήψη του Πρώτου Κελιού

Τώρα **create cell style** παίρνοντας πρώτα μια αναφορά στο κελί που θέλουμε να μορφοποιήσουμε.

```csharp
// Inside Main()
Workbook workbook = new Workbook();           // New, empty workbook
Worksheet ws = workbook.Worksheets[0];        // First worksheet (index 0)

// Step 1: Get a reference to the first cell (row 0, column 0) in the worksheet
Cell firstCell = ws.Cells[0, 0];               // A1 in Excel terms
firstCell.PutValue("Hello, styled world!");
```

Παρατηρήστε ότι χρησιμοποιήσαμε `Cell` αντί για το γενικό `var` — ο ρητός τύπος κάνει τον κώδικα πιο σαφή για τους νέους. Η κλήση στο `PutValue` γράφει μια συμβολοσειρά ώστε να δούμε το αποτέλεσμα του στυλ αργότερα.

---

## Βήμα 3: Ορισμός του Στυλ – Στοίχιση Κειμένου, Προσθήκη Λεπτού Περιγράμματος

Αυτή είναι η καρδιά της λειτουργίας **create cell style**. Θα ορίσουμε την οριζόντια στοίχιση, ένα λεπτό περίγραμμα και μερικές προαιρετικές βελτιώσεις.

```csharp
// Step 2: Define a style that centers the text and adds a thin border
Style cellStyle = workbook.CreateStyle();          // Create a fresh Style object
cellStyle.HorizontalAlignment = TextAlignmentType.Center; // Center text horizontally
cellStyle.VerticalAlignment = TextAlignmentType.Center;   // Center vertically – often forgotten
cellStyle.Borders[BorderType.TopBorder].LineStyle = CellBorderType.Thin;
cellStyle.Borders[BorderType.BottomBorder].LineStyle = CellBorderType.Thin;
cellStyle.Borders[BorderType.LeftBorder].LineStyle = CellBorderType.Thin;
cellStyle.Borders[BorderType.RightBorder].LineStyle = CellBorderType.Thin;

// Optional: set a light gray background to make the border pop
cellStyle.ForegroundColor = System.Drawing.Color.LightGray;
cellStyle.Pattern = BackgroundType.Solid;
```

*Γιατί το κάνουμε:*  
- **HorizontalAlignment** και **VerticalAlignment** μαζί απαντούν στην ερώτηση “**how to center text** σε ένα κελί;”.  
- Η προσθήκη και των τεσσάρων περιγραμμάτων εξασφαλίζει ότι το κελί φαίνεται σαν ετικέτα σε κουτί, χρήσιμο για κεφαλίδες.  
- Το χρώμα φόντου δεν είναι απαραίτητο, αλλά δείχνει πώς μπορείτε να επεκτείνετε το στυλ αργότερα.

---

## Βήμα 4: Εφαρμογή του Ορισμένου Στυλ στο Επιλεγμένο Κελί

Τώρα που το στυλ υπάρχει, **apply style to cell** με μία κλήση μεθόδου.

```csharp
// Step 3: Apply the defined style to the selected cell
firstCell.SetStyle(cellStyle);
```

Αυτό είναι—το Aspose.Cells φροντίζει να αντιγράψει το στυλ στη συλλογή εσωτερικών στυλ του κελιού. Αν χρειάζεστε την ίδια μορφοποίηση σε μια περιοχή, μπορείτε να χρησιμοποιήσετε `ws.Cells.CreateRange("A1:D1").ApplyStyle(cellStyle, new StyleFlag { All = true });`.

---

## Βήμα 5: Αποθήκευση του Workbook και Επαλήθευση του Αποτελέσματος

Μια γρήγορη αποθήκευση σας επιτρέπει να ανοίξετε το αρχείο στο Excel και να επιβεβαιώσετε ότι το κείμενο είναι πραγματικά κεντραρισμένο και το περίγραμμα εμφανίζεται.

```csharp
// Save the workbook to disk
string outputPath = "StyledCell.xlsx";
workbook.Save(outputPath, SaveFormat.Xlsx);
Console.WriteLine($"Workbook saved to {outputPath}. Open it to see the styled cell.");
```

*Αναμενόμενο αποτέλεσμα:* Όταν ανοίξετε το **StyledCell.xlsx**, το κελί **A1** περιέχει το “Hello, styled world!” κεντραρισμένο οριζόντια και κάθετα, περιτριγυρισμένο από ένα λεπτό γκρι περίγραμμα και με φόντο ανοιχτό‑γκρι.

---

## Συνηθισμένες Παραλλαγές & Ειδικές Περιπτώσεις

### 1. Στοίχιση Κειμένου σε Συγχωνευμένη Περιοχή

Αν συγχωνεύσετε τα κελιά **A1:C1** και θέλετε ακόμα το κείμενο κεντραρισμένο, πρέπει να εφαρμόσετε το στυλ στο πάνω‑αριστερό κελί **μετά** τη συγχώνευση:

```csharp
ws.Cells.Merge(0, 0, 1, 3); // Merge A1:C1
firstCell.SetStyle(cellStyle); // Style still works because it’s applied to the anchor cell
```

### 2. Χρήση Αριθμητικής Μορφής

Μερικές φορές χρειάζεται να **set cell alignment** *και* να εμφανίσετε αριθμούς με συγκεκριμένη μορφή:

```csharp
cellStyle.Custom = "#,##0.00"; // Two decimal places
firstCell.PutValue(12345.678);
firstCell.SetStyle(cellStyle);
```

Η στοίχιση παραμένει κεντραρισμένη ενώ ο αριθμός εμφανίζεται ως `12,345.68`.

### 3. Αποδοτική Επανάχρηση Στυλ

Η δημιουργία ενός νέου `Style` για κάθε κελί μπορεί να επηρεάσει την απόδοση. Αντί αυτού, δημιουργήστε ένα αντικείμενο στυλ και επαναχρησιμοποιήστε το σε πολλά κελιά ή περιοχές. Η κλάση `StyleFlag` σας επιτρέπει να εφαρμόσετε μόνο τα μέρη που σας ενδιαφέρουν, εξοικονομώντας μνήμη.

```csharp
StyleFlag flag = new StyleFlag { HorizontalAlignment = true, Borders = true };
ws.Cells.CreateRange("B2:B10").ApplyStyle(cellStyle, flag);
```

---

## Επαγγελματικές Συμβουλές & Πιθανά Πάγια

- **Μην ξεχνάτε την κατακόρυφη στοίχιση** – η κεντραρισμένη μόνο οριζόντια συχνά φαίνεται λανθασμένη, ειδικά σε πιο ψηλές γραμμές.
- **Τύποι περιγραμμάτων**: `CellBorderType.Thin` λειτουργεί για τις περισσότερες αναφορές, αλλά μπορείτε να μεταβείτε σε `Medium` ή `Dashed` για οπτική ιεραρχία.
- **Διαχείριση χρωμάτων**: Όταν στοχεύετε .NET Core, χρησιμοποιήστε το `System.Drawing.Color` από το πακέτο `System.Drawing.Common`; διαφορετικά θα αντιμετωπίσετε σφάλμα χρόνου εκτέλεσης.
- **Μορφή αποθήκευσης**: Αν χρειάζεστε συμβατότητα με παλαιότερες εκδόσεις Excel, αλλάξτε το `SaveFormat.Xlsx` σε `SaveFormat.Xls`.

![Δημιουργία στυλ κελιού παράδειγμα](https://example.com/images/create-cell-style.png "Δημιουργία στυλ κελιού σε C#")

*Κείμενο alt: στιγμιότυπο που δείχνει ένα κελί με κεντραρισμένο κείμενο και λεπτό περίγραμμα, δημιουργημένο από το tutorial create cell style.*

---

## Πλήρες Παράδειγμα Εργασίας (Έτοιμο για Αντιγραφή‑Επικόλληση)

```csharp
using System;
using Aspose.Cells;
using System.Drawing; // For Color

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet ws = workbook.Worksheets[0];

        // 2️⃣ Grab the first cell and put a sample value
        Cell firstCell = ws.Cells[0, 0];
        firstCell.PutValue("Hello, styled world!");

        // 3️⃣ Create the style: center text, thin border, light gray background
        Style cellStyle = workbook.CreateStyle();
        cellStyle.HorizontalAlignment = TextAlignmentType.Center;
        cellStyle.VerticalAlignment   = TextAlignmentType.Center;
        cellStyle.Borders[BorderType.TopBorder].LineStyle    = CellBorderType.Thin;
        cellStyle.Borders[BorderType.BottomBorder].LineStyle = CellBorderType.Thin;
        cellStyle.Borders[BorderType.LeftBorder].LineStyle   = CellBorderType.Thin;
        cellStyle.Borders[BorderType.RightBorder].LineStyle  = CellBorderType.Thin;
        cellStyle.ForegroundColor = Color.LightGray;
        cellStyle.Pattern = BackgroundType.Solid;

        // 4️⃣ Apply the style to the cell
        firstCell.SetStyle(cellStyle);

        // 5️⃣ Save the result
        string outputPath = "StyledCell.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);
        Console.WriteLine($"Workbook saved to {outputPath}. Open it to see the styled cell.");
    }
}
```

Εκτελέστε αυτό το πρόγραμμα, ανοίξτε το **StyledCell.xlsx**, και θα δείτε το ακριβές αποτέλεσμα που περιγράφηκε νωρίτερα. Μπορείτε ελεύθερα να αλλάξετε το κείμενο, το στυλ περιγράμματος ή το χρώμα φόντου ώστε να ταιριάζει με το branding σας.

---

## Συμπέρασμα

Μόλις **created cell style** από το μηδέν, **apply style to cell**, και δείξαμε **how to center text** τόσο οριζόντια όσο και κάθετα. Με την κατάκτηση αυτών των θεμελιωδών στοιχείων μπορείτε τώρα να μορφοποιήσετε κεφαλίδες, να επισημάνετε σύνολα ή να δημιουργήσετε ολόκληρα πρότυπα αναφορών χωρίς να βγείτε ποτέ από το C#.  

Αν είστε περίεργοι για τα επόμενα βήματα, δοκιμάστε:

- **Applying the same style to a whole row** (`ws.Cells.CreateRange("A2:E2").ApplyStyle(cellStyle, new StyleFlag { All = true });`).
- **Adding conditional formatting** για αλλαγή του φόντου βάσει τιμών κελιού.
- **Exporting to PDF** διατηρώντας το στυλ.

Θυμηθείτε, η μορφοποίηση αφορά τόσο την αναγνωσιμότητα όσο και την αισθητική. Πειραματιστείτε, επαναλάβετε, και σύντομα τα λογιστικά σας φύλλα θα φαίνονται τόσο επαγγελματικά όσο και ο κώδικάς σας.

*Καλό κώδικα!*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}