---
category: general
date: 2026-05-23
description: Δημιουργήστε βιβλίο εργασίας Excel σε C# και μάθετε πώς να εφαρμόζετε
  προσαρμοσμένη μορφή αριθμού, να ορίζετε το στυλ κελιού προγραμματιστικά, να μορφοποιείτε
  το κελί σε επιστημονική σημειογραφία και, στη συνέχεια, να αποθηκεύετε το βιβλίο
  εργασίας σε μορφή xlsx.
draft: false
keywords:
- create excel workbook
- apply custom number format
- format cell scientific notation
- set cell style programmatically
- save workbook to xlsx
language: el
og_description: Δημιουργήστε γρήγορα ένα βιβλίο εργασίας Excel σε C#. Μάθετε πώς να
  εφαρμόζετε προσαρμοσμένη μορφή αριθμών, να μορφοποιείτε κελιά προγραμματιστικά,
  να μορφοποιείτε επιστημονική σημειογραφία και να αποθηκεύετε σε μορφή xlsx.
og_title: Δημιουργία βιβλίου εργασίας Excel σε C# – Εφαρμογή προσαρμοσμένης μορφής
  αριθμού
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: Create excel workbook in C# and learn how to apply custom number format,
    set cell style programmatically, format cell scientific notation, then save workbook
    to xlsx.
  headline: Create Excel Workbook in C# – Apply Custom Number Format
  type: TechArticle
tags:
- C#
- Excel
- Aspose.Cells
- Automation
title: Δημιουργία βιβλίου εργασίας Excel σε C# – Εφαρμογή προσαρμοσμένης μορφής αριθμού
url: /el/net/excel-custom-number-date-formatting/create-excel-workbook-in-c-apply-custom-number-format/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία βιβλίου εργασίας Excel σε C# – Εφαρμογή προσαρμοσμένης μορφής αριθμού

Η δημιουργία βιβλίου εργασίας Excel σε C# είναι πιο εύκολη από ό,τι νομίζετε. Σε αυτόν τον οδηγό θα σας δείξουμε πώς να εφαρμόσετε μια προσαρμοσμένη μορφή αριθμού, πώς να μορφοποιήσετε ένα κελί σε επιστημονική σημειογραφία, πώς να ορίσετε το στυλ του κελιού προγραμματιστικά και, τέλος, πώς να αποθηκεύσετε το βιβλίο εργασίας σε αρχείο xlsx.

Αν έχετε ποτέ κοίταξει ένα κενό φύλλο υπολογισμού και αναρωτηθείτε πώς να αυτοματοποιήσετε όλο το διαδικαστικό – από τη συμπλήρωση δεδομένων μέχρι την εμφάνιση των αριθμών ακριβώς όπως θέλετε – αυτό το tutorial είναι για εσάς. Στο τέλος θα έχετε ένα πλήρως λειτουργικό αρχείο Excel που μπορείτε να ανοίξετε σε οποιοδήποτε πρόγραμμα υπολογιστικών φύλλων, και θα καταλάβετε **γιατί** κάθε βήμα είναι σημαντικό, όχι μόνο **πώς** να γράψετε τον κώδικα.

## Τι θα χρειαστείτε

- **.NET 6+** (ή οποιοδήποτε πρόσφατο .NET Framework που υποστηρίζει τη βιβλιοθήκη)  
- **Aspose.Cells for .NET** (ή άλλο API που εκθέτει τις κλάσεις `Workbook`, `Cell` και `CellFormat`)  
- Μια μέτρια εμπειρία με C# – αν μπορείτε να γράψετε ένα `Console.WriteLine`, είστε έτοιμοι.  

Χωρίς επιπλέον αρχεία ρυθμίσεων, χωρίς COM interop και σίγουρα χωρίς ανάγκη χειροκίνητης εγκατάστασης του Excel.

---

## Δημιουργία βιβλίου εργασίας Excel – Αρχικοποίηση του αντικειμένου Workbook

Το πρώτο που πρέπει να κάνουμε είναι να δημιουργήσουμε ένα κενό βιβλίο εργασίας. Σκεφτείτε την κλάση `Workbook` ως τον λευκό καμβά πάνω στον οποίο θα σχεδιάσετε γραμμές, στήλες και στυλ.

```csharp
using Aspose.Cells;   // Make sure the Aspose.Cells namespace is referenced

// Step 1: Create a new workbook instance
Workbook workbook = new Workbook();
```

Απλά—μία γραμμή και έχετε ένα ολοκαίνουργιο αρχείο Excel στη μνήμη. Ο κατασκευαστής `Workbook` δημιουργεί τη συλλογή φύλλων εργασίας προεπιλογής, ώστε να μπορείτε να αρχίσετε να προσθέτετε δεδομένα αμέσως.

> **Συμβουλή:** Αν χρειάζεστε πολλαπλά φύλλα, μπορείτε να καλέσετε `workbook.Worksheets.Add()` πριν αρχίσετε να γεμίζετε τα κελιά.

![Δημιουργία βιβλίου εργασίας Excel παράδειγμα](image-placeholder.png "Στιγμιότυπο οθόνης δημιουργίας βιβλίου εργασίας Excel")

*Image alt text: παράδειγμα δημιουργίας βιβλίου εργασίας Excel που δείχνει ένα κενό φύλλο Excel στο IDE.*

## Εφαρμογή προσαρμοσμένης μορφής αριθμού σε κελί

Τώρα που υπάρχει το βιβλίο εργασίας, ας τοποθετήσουμε έναν αριθμό στο κελί **A1** και ας του δώσουμε μια προσαρμοσμένη μορφή. Οι προσαρμοσμένες μορφές αριθμού σας επιτρέπουν να ελέγχετε πώς εμφανίζονται οι αριθμοί — νομίσματα, ποσοστά, ημερομηνίες ή, στην περίπτωσή μας, επιστημονική σημειογραφία.

```csharp
// Step 2: Grab the first worksheet and the cell at A1 (row 0, column 0)
Worksheet sheet = workbook.Worksheets[0];
Cell cell = sheet.Cells[0, 0];

// Step 3: Insert a numeric value
cell.PutValue(12345.6789);

// Step 4: Retrieve the current style so we can modify its Number format
Style style = cell.GetStyle();

// Step 5: Define a custom scientific notation format with two decimal places
style.Custom = "0.00E+00";   // This is the “apply custom number format” part

// Step 6: Push the modified style back onto the cell
cell.SetStyle(style);
```

Γιατί να πάρουμε πρώτα το στυλ; Επειδή το αντικείμενο `Cell` αποθηκεύει ένα αντικείμενο **Style** που περιέχει γραμματοσειρές, περιγράμματα, στοίχιση και μορφοποίηση αριθμών όλα σε ένα μέρος. Επεξεργαζόμενοι την ιδιότητα `Custom` λέμε στο Excel: «εμφάνισε αυτήν την τιμή χρησιμοποιώντας επιστημονική σημειογραφία με δύο δεκαδικά».

> **Συχνή ερώτηση:** *Μπορώ να χρησιμοποιήσω μια ενσωματωμένη μορφή αντί για προσαρμοσμένη;*  
> Ναι — ορίστε `style.Number = 10` για μια ενσωματωμένη επιστημονική μορφή, αλλά η προσαρμοσμένη συμβολοσειρά σας δίνει ακριβή έλεγχο των δεκαδικών θέσεων.

## Ορισμός στυλ κελιού προγραμματιστικά (Πέρα από τη μορφή αριθμού)

Συχνά θέλετε κάτι παραπάνω από μια απλή μορφή αριθμού. Ας προσθέσουμε έντονη γραμματοσειρά και ένα ανοιχτό γκρι φόντο ώστε το κελί να ξεχωρίζει.

```csharp
// Optional: Enhance the cell appearance
style.Font.IsBold = true;
style.ForegroundColor = System.Drawing.Color.LightGray;
style.Pattern = BackgroundType.Solid;

// Re‑apply the enriched style
cell.SetStyle(style);
```

Παρατηρήστε ότι επαναχρησιμοποιούμε το ίδιο αντικείμενο `style` που τροποποιήσαμε νωρίτερα. Αυτή είναι η ομορφιά του **ορισμού στυλ κελιού προγραμματιστικά** — παίρνετε το στυλ μία φορά, τροποποιείτε ό,τι χρειάζεστε και το γράφετε πίσω. Δεν χρειάζεται να δημιουργήσετε ξανά αντικείμενα ή να χάσετε τη μορφή αριθμού που έχετε ήδη ορίσει.

## Μορφοποίηση κελιού σε επιστημονική σημειογραφία (Διαχείριση ειδικών περιπτώσεων)

Αν εργάζεστε με πολύ μεγάλους ή πολύ μικρούς αριθμούς, η επιστημονική σημειογραφία είναι απαραίτητη. Η προσαρμοσμένη μορφή που χρησιμοποιήσαμε (`0.00E+00`) εγγυάται δύο ψηφία μετά το δεκαδικό σημείο και προσθέτει το σύμβολο «+» για τον εκθέτη. Εδώ είναι ένας γρήγορος έλεγχος:

```csharp
// Verify the format by inserting another extreme value
Cell extraCell = sheet.Cells[1, 0]; // B2
extraCell.PutValue(0.00001234);
extraCell.SetStyle(style); // Reuse the same style with scientific notation
```

Όταν ανοίξετε το παραγόμενο αρχείο, το B2 θα εμφανιστεί ως `1.23E-05`, επιβεβαιώνοντας ότι η οδηγία **μορφοποίησης κελιού σε επιστημονική σημειογραφία** λειτουργεί τόσο για μεγάλους όσο και για μικρούς αριθμούς.

## Αποθήκευση βιβλίου εργασίας σε XLSX

Όλη η διασκέδαση σταματά όταν γράψετε το αρχείο στο δίσκο. Η μέθοδος `Save` αναλαμβάνει το βαρέως τύπου έργο, μετατρέποντας την αναπαράσταση στη μνήμη σε ένα σωστό πακέτο `.xlsx`.

```csharp
// Step 7: Persist the workbook
string outputPath = @"C:\Temp\CustomFormatted.xlsx";
workbook.Save(outputPath, SaveFormat.Xlsx);
```

Αυτή η γραμμή ολοκληρώνει τον στόχο **αποθήκευσης βιβλίου εργασίας σε xlsx**. Αν ο φάκελος δεν υπάρχει, το `Save` θα ρίξει εξαίρεση — γι' αυτό βεβαιωθείτε ότι ο φάκελος δημιουργείται εκ των προτέρων ή τυλίξτε την κλήση σε block `try/catch`.

```csharp
try
{
    workbook.Save(outputPath, SaveFormat.Xlsx);
    Console.WriteLine($"Workbook saved successfully to {outputPath}");
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Failed to save workbook: {ex.Message}");
}
```

Τώρα έχετε ένα έτοιμο προς κοινή χρήση αρχείο Excel με έναν ωραία μορφοποιημένο επιστημονικό αριθμό, έντονο στυλ και ανοιχτό γκρι φόντο.

## Πλήρες λειτουργικό παράδειγμα

Παρακάτω είναι το ολοκληρωμένο πρόγραμμα, έτοιμο για αντιγραφή‑επικόλληση, που ενώνει όλα τα κομμάτια. Συγκεντρώνεται ως εφαρμογή κονσόλας, αλλά μπορείτε να ενσωματώσετε τη λογική σε οποιοδήποτε έργο C#.

```csharp
using System;
using Aspose.Cells;
using System.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook
        Workbook workbook = new Workbook();

        // 2️⃣ Access the first worksheet and target cell A1
        Worksheet sheet = workbook.Worksheets[0];
        Cell cell = sheet.Cells[0, 0];

        // 3️⃣ Insert a numeric value
        cell.PutValue(12345.6789);

        // 4️⃣ Retrieve and customize the cell style
        Style style = cell.GetStyle();
        style.Custom = "0.00E+00";               // apply custom number format (scientific)
        style.Font.IsBold = true;               // set cell style programmatically
        style.ForegroundColor = Color.LightGray;
        style.Pattern = BackgroundType.Solid;

        // 5️⃣ Apply the style back to the cell
        cell.SetStyle(style);

        // 6️⃣ Add another example to prove scientific notation works for tiny numbers
        Cell tinyCell = sheet.Cells[1, 0]; // B2
        tinyCell.PutValue(0.00001234);
        tinyCell.SetStyle(style);

        // 7️⃣ Save the workbook to an XLSX file
        string outputPath = @"C:\Temp\CustomFormatted.xlsx";
        try
        {
            workbook.Save(outputPath, SaveFormat.Xlsx);
            Console.WriteLine($"Workbook saved successfully to {outputPath}");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Failed to save workbook: {ex.Message}");
        }
    }
}
```

**Αναμενόμενο αποτέλεσμα:** Ανοίξτε το `CustomFormatted.xlsx` και θα δείτε:

| A1               | B2            |
|------------------|---------------|
| 1.23E+04         | 1.23E-05      |

Και τα δύο κελιά είναι έντονα, έχουν γκρι γέμισμα και εμφανίζουν αριθμούς σε επιστημονική σημειογραφία με δύο δεκαδικά ψηφία.

---

## Συνοψίζοντας

Μόλις **δημιουργήσαμε βιβλίο εργασίας Excel** από την αρχή, **εφαρμόσαμε προσαρμοσμένη μορφή αριθμού**, **μορφοποιήσαμε κελί σε επιστημονική σημειογραφία**, **ορίσαμε στυλ κελιού προγραμματιστικά**, και **αποθηκεύσαμε το βιβλίο εργασίας σε xlsx** — όλα σε λίγες γραμμές C#. Η προσέγγιση κλιμακώνεται: απλώς κάντε βρόχο στις γραμμές, κλωνοποιήστε το αντικείμενο `style`, και θα έχετε μια πλήρως μορφοποιημένη αναφορά σε δευτερόλεπτα.

### Τι ακολουθεί;

- **Δυναμική μορφοποίηση:** Αλλάξτε μορφές ανάλογα με το μέγεθος της τιμής (π.χ., νόμισμα vs. ποσοστό).  
- **Πολλαπλά φύλλα:** Χρησιμοποιήστε `workbook.Worksheets.Add("Summary")` για να δημιουργήσετε πίνακες ελέγχου.  
- **Προηγμένη μορφοποίηση:** Περιγράμματα, υπό-συνθήκες μορφοποίηση και επικύρωση δεδομένων

## Σχετικά Tutorials

- [How to Create and Save an Excel Workbook as ODS Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [Create Save Excel Workbook Aspose Cells Dotnet](/cells/hongkong/net/workbook-operations/create-save-excel-workbook-aspose-cells-dotnet/)
- [Create Save Excel Workbook Pdf Aspnet Aspose Cells](/cells/hongkong/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}