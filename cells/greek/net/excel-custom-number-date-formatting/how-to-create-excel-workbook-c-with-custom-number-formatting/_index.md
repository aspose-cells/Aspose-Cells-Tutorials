---
category: general
date: 2026-10-01
description: Μάθετε πώς να δημιουργήσετε ένα βιβλίο εργασίας Excel με C# και να εφαρμόσετε
  προσαρμοσμένη μορφή αριθμού, να ορίσετε τα δεκαδικά ψηφία των κελιών και να αποθηκεύσετε
  το βιβλίο εργασίας ως XLSX σε έναν πλήρη οδηγό βήμα‑προς‑βήμα.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook c#
- apply custom number format
- how to format numbers excel
- set cell decimal places
- save workbook as xlsx
language: el
lastmod: 2026-10-01
og_description: Δημιουργήστε βιβλίο εργασίας Excel με C# με προσαρμοσμένη μορφή αριθμού,
  ορίστε τα δεκαδικά ψηφία των κελιών και αποθηκεύστε το βιβλίο εργασίας ως XLSX.
  Ακολουθήστε αυτόν τον πλήρη οδηγό για ακριβή αριθμητική έξοδο.
og_image_alt: Screenshot of an Excel sheet showing numbers rounded to four significant
  digits
og_title: Δημιουργία βιβλίου εργασίας Excel C# – προσαρμοσμένη μορφή αριθμού & εξαγωγή
  XLSX
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to create Excel workbook C# and apply custom number format,
    set cell decimal places, and save workbook as XLSX in a complete step‑by‑step
    guide.
  headline: How to create Excel workbook C# with custom number formatting
  type: TechArticle
- description: Learn how to create Excel workbook C# and apply custom number format,
    set cell decimal places, and save workbook as XLSX in a complete step‑by‑step
    guide.
  name: How to create Excel workbook C# with custom number formatting
  steps:
  - name: Run the program (`dotnet run`).
    text: Run the program (`dotnet run`).
  - name: Open `SigDigits.xlsx`.
    text: Open `SigDigits.xlsx`.
  - name: Confirm that **A1** reads `123.5`.
    text: Confirm that **A1** reads `123.5`.
  - name: If you open the file’s XML (`.xlsx` is a zip archive), you’ll see the custom
      format `"0.######"` stored in the `<c>` element’s `s` attribute.
    text: If you open the file’s XML (`.xlsx` is a zip archive), you’ll see the custom
      format `"0.######"` stored in the `<c>` element’s `s` attribute.
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: Πώς να δημιουργήσετε ένα βιβλίο εργασίας Excel σε C# με προσαρμοσμένη μορφοποίηση
  αριθμών
url: /el/net/excel-custom-number-date-formatting/how-to-create-excel-workbook-c-with-custom-number-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να δημιουργήσετε βιβλίο εργασίας Excel C# με προσαρμοσμένη μορφοποίηση αριθμών

Αν χρειάζεστε **να δημιουργήσετε βιβλίο εργασίας excel c#** που εμφανίζει τους αριθμούς ακριβώς όπως θέλετε, αυτός ο οδηγός σας δείχνει πώς να το κάνετε σε λίγα σαφή βήματα. Θα μάθετε πώς να εφαρμόζετε προσαρμοσμένη μορφή αριθμού, να ορίζετε τα δεκαδικά ψηφία του κελιού και τελικά **να αποθηκεύσετε το βιβλίο εργασίας ως xlsx** για περαιτέρω χρήση.

Η εργασία με αριθμητικά δεδομένα συχνά σημαίνει εξισορρόπηση μεταξύ ακρίβειας και αναγνωσιμότητας. Στο τέλος αυτού του tutorial θα έχετε ένα επαναχρησιμοποιήσιμο μοτίβο που περιορίζει τα εμφανιζόμενα ψηφία σε συγκεκριμένο αριθμό σημαντικών ψηφίων, διατηρώντας την αρχική τιμή στο αρχείο. Δεν απαιτούνται εξωτερικά scripts—μόνο C# και η βιβλιοθήκη Aspose.Cells.

## Προαπαιτήσεις

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

* .NET 6.0 SDK ή νεότερη έκδοση εγκατεστημένη  
* Visual Studio 2022 (ή οποιοδήποτε IDE για C#)  
* Το **Aspose.Cells for .NET** πακέτο NuGet (`Install-Package Aspose.Cells`) – αυτή η βιβλιοθήκη παρέχει τις κλάσεις `Workbook`, `Worksheet` και `ExportTableOptions` που χρησιμοποιούνται στα παραδείγματα.  

Αυτές οι απαιτήσεις είναι ελάχιστες· ο ίδιος κώδικας λειτουργεί σε .NET Core, .NET Framework και ακόμη και σε Azure Functions.

## Βήμα 1: Δημιουργία Excel workbook C# – αρχικοποίηση του αρχείου

Η πρώτη ενέργεια είναι η δημιουργία ενός νέου αντικειμένου `Workbook`. Αυτό το αντικείμενο αντιπροσωπεύει ολόκληρο το αρχείο Excel στη μνήμη και περιέχει αυτόματα ένα προεπιλεγμένο φύλλο εργασίας.

```csharp
using Aspose.Cells;

namespace ExcelDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook and get the first worksheet
            Workbook workbook = new Workbook();               // creates an empty .xlsx container
            Worksheet sheet = workbook.Worksheets[0];         // reference to the default sheet
```

**Γιατί είναι σημαντικό:**  
Η δημιουργία του βιβλίου εργασίας εκ των προτέρων σας δίνει έναν καθαρό καμβά. Το προεπιλεγμένο φύλλο (`Worksheets[0]`) είναι έτοιμο για εισαγωγή δεδομένων, οπότε δεν χρειάζεται να προσθέσετε νέο φύλλο εκτός αν το σενάριό σας απαιτεί πολλαπλές καρτέλες.

## Βήμα 2: Εγγραφή αριθμητικής τιμής σε κελί

Τώρα τοποθετήστε έναν δείγμα αριθμό στο κελί **A1**. Η τιμή που χρησιμοποιούμε (`123.456789`) περιέχει περισσότερα δεκαδικά ψηφία από όσα τελικά θέλουμε να εμφανιστούν, κάτι που μας επιτρέπει να δείξουμε το στρογγυλοποίηση αργότερα.

```csharp
            // Step 2: Write a numeric value to cell A1
            sheet.Cells[0, 0].PutValue(123.456789); // row 0, column 0 = A1
```

**Συμβουλή:** `PutValue` ανιχνεύει αυτόματα τον τύπο δεδομένων, οπότε δεν χρειάζεται να μετατρέψετε τον αριθμό σε συμβολοσειρά.

## Βήμα 3: Εφαρμογή προσαρμοσμένης μορφής αριθμού – περιορισμός ορατών δεκαδικών

Για να ελέγξετε πώς το Excel εμφανίζει τον αριθμό, δημιουργούμε ένα `Style` με **προσαρμοσμένη μορφή αριθμού**. Το μοτίβο `"0.######"` λέει στο Excel να εμφανίζει έως και έξι δεκαδικά ψηφία, αλλά να παραλείπει τα μηδενικά στο τέλος.

```csharp
            // Step 3: Define a custom number format (up to 6 decimal places) and apply it
            Style customStyle = workbook.CreateStyle();
            customStyle.Custom = "0.######";               // up to 6 decimals, no trailing zeros
            sheet.Cells[0, 0].SetStyle(customStyle);
```

**Πώς λειτουργεί:**  
Η συμβολοσειρά μορφής ακολουθεί τη σύνταξη προσαρμοσμένων μορφών του Excel. Το `0` εξαναγκάζει την εμφάνιση ψηφίου, ενώ το `#` εμφανίζει ψηφίο μόνο αν είναι σημαντικό. Συνδυάζοντάς τα, παίρνετε μια ευέλικτη εμφάνιση που διατηρεί την αρχική ακρίβεια.

## Βήμα 4: Ορισμός δεκαδικών ψηφίων κελιού – χρήση ExportTableOptions

Αν χρειάζεται να **ορίσετε δεκαδικά ψηφία κελιού** για εξαγόμενα δεδομένα (π.χ. κατά τη μετατροπή σε DataTable), το Aspose.Cells σας επιτρέπει να καθορίσετε τον αριθμό των **σημαντικών ψηφίων**. Αυτό το βήμα διασφαλίζει ότι το εξαγόμενο CSV ή DataTable σέβεται τους ίδιους κανόνες στρογγυλοποίησης που εφαρμόσατε στο βιβλίο εργασίας.

```csharp
            // Step 4: Configure export options to limit the output to 4 significant digits
            ExportTableOptions exportOptions = new ExportTableOptions();
            exportOptions.SignificantDigits = 4;           // round to 4 significant figures
```

**Γιατί να χρησιμοποιήσετε `SignificantDigits`;**  
Σε αντίθεση με έναν σταθερό αριθμό δεκαδικών, τα σημαντικά ψηφία διατηρούν το μέγεθος του αριθμού ενώ περιορίζουν την ακρίβεια, κάτι που συχνά αναμένουν οι αναλυτές όταν συνοψίζουν δεδομένα.

## Βήμα 5: Εξαγωγή δεδομένων φύλλου και **αποθήκευση βιβλίου εργασίας ως xlsx**

Τέλος, εξάγετε τα δεδομένα (αν χρειάζεστε DataTable) και αποθηκεύστε το βιβλίο εργασίας στο δίσκο. Η κλήση `ExportDataTable` σέβεται τις `ExportTableOptions` που ρυθμίσαμε, και το `workbook.Save` γράφει ένα τυπικό αρχείο XLSX.

```csharp
            // Step 5: Export the worksheet data using the configured options and save the workbook
            sheet.ExportDataTable(sheet.Cells.MaxDisplayRange, true, exportOptions);
            workbook.Save("SigDigits.xlsx");               // saves to the application’s working folder
        }
    }
}
```

**Αναμενόμενο αποτέλεσμα:**  
Όταν ανοίξετε το *SigDigits.xlsx* στο Excel, το κελί **A1** εμφανίζει `123.5`. Η υποκείμενη τιμή παραμένει `123.456789`, αλλά ο εμφανιζόμενος αριθμός ακολουθεί τον κανόνα των 4‑σημαντικών‑ψηφίων. Αν εξάγετε το φύλλο σε DataTable, η τιμή στον πίνακα θα είναι επίσης στρογγυλοποιημένη σε `123.5`.

---

## Εφαρμογή προσαρμοσμένης μορφής αριθμού σε επιπλέον κελιά

Αν χρειάζεται να μορφοποιήσετε μια περιοχή αντί για ένα μόνο κελί, επαναχρησιμοποιήστε το αντικείμενο `Style`:

```csharp
// Apply the same custom style to B2:C5
Range range = sheet.Cells.CreateRange("B2:C5");
range.ApplyStyle(customStyle, new StyleFlag { NumberFormat = true });
```

**Pro tip:** Η επαναχρήση ενός αντικειμένου στυλ μειώνει το φορτίο μνήμης και εγγυάται συνεπή μορφοποίηση σε όλο το φύλλο.

## Πώς να μορφοποιήσετε αριθμούς στο Excel χρησιμοποιώντας C# – κοινές παραλλαγές

| Σενάριο | Συμβολοσειρά μορφής | Αποτέλεσμα |
|----------|-------------------|------------|
| Σταθερά δύο δεκαδικά | `"0.00"` | `123.46` |
| Νομισματικό (US) | `"$#,##0.00"` | `$123.46` |
| Ποσοστό με ένα δεκαδικό | `"0.0%"` | `12,346.0%` |
| Επιστημονική σημειογραφία | `"0.00E+00"` | `1.23E+02` |

Επιλέξτε το μοτίβο που ταιριάζει στις απαιτήσεις αναφοράς σας. Όλα τα μοτίβα είναι συμβατά με την ιδιότητα `Style.Custom` που παρουσιάστηκε νωρίτερα.

## Δυναμικός ορισμός δεκαδικών ψηφίων κελιού βάσει εισόδου χρήστη

Μερικές φορές η απαιτούμενη ακρίβεια δεν είναι γνωστή κατά τη μεταγλώττιση. Μπορείτε να δημιουργήσετε τη συμβολοσειρά μορφής κατά το χρόνο εκτέλεσης:

```csharp
int decimals = 3; // could come from a UI textbox
string format = "0." + new string('#', decimals);
customStyle.Custom = format;
sheet.Cells["A2"].PutValue(987.654321);
sheet.Cells["A2"].SetStyle(customStyle);
```

**Edge case:** Αν το `decimals` είναι μηδέν, η μορφή γίνεται `"0"` (εμφάνιση ακέραιου). Πάντα να επικυρώνετε την είσοδο του χρήστη για να αποφύγετε κατεστραμμένες συμβολοσειρές μορφής.

## Αποθήκευση βιβλίου εργασίας ως XLSX – βέλτιστες πρακτικές

* **Χρησιμοποιήστε απόλυτες διαδρομές** όταν γράφετε σε γνωστό φάκελο (`Path.Combine(Environment.CurrentDirectory, "output.xlsx")`).  
* **Κλείστε** το `Workbook` αν το τυλίξετε σε δήλωση `using` για να ελευθερώσετε άμεσα τους μη διαχειριζόμενους πόρους:

```csharp
using (Workbook wb = new Workbook())
{
    // ...populate workbook...
    wb.Save(Path.Combine(@"C:\Exports", "Report.xlsx"));
}
```

* **Συμβατότητα εκδόσεων:** Το Aspose.Cells γράφει αρχεία συμβατά με Excel 2010‑2023, ώστε οι downstream χρήστες να μην αντιμετωπίζουν προβλήματα μορφοποίησης.

---

## Πλήρες λειτουργικό παράδειγμα

Παρακάτω βρίσκεται το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε, να επικολλήσετε και να τρέξετε αμέσως. Περιλαμβάνει όλες τις απαραίτητες οδηγίες `using`, σχόλια και διαχείριση σφαλμάτων.

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelDemo
{
    class Program
    {
        static void Main()
        {
            try
            {
                // 1️⃣ Create workbook and get the first worksheet
                Workbook workbook = new Workbook();
                Worksheet sheet = workbook.Worksheets[0];

                // 2️⃣ Write a high‑precision number to A1
                sheet.Cells[0, 0].PutValue(123.456789);

                // 3️⃣ Apply a custom number format (up to 6 decimals)
                Style customStyle = workbook.CreateStyle();
                customStyle.Custom = "0.######";
                sheet.Cells[0, 0].SetStyle(customStyle);

                // 4️⃣ Configure export options for 4 significant digits
                ExportTableOptions exportOptions = new ExportTableOptions
                {
                    SignificantDigits = 4
                };

                // 5️⃣ Export data (optional) and save the workbook as XLSX
                sheet.ExportDataTable(sheet.Cells.MaxDisplayRange, true, exportOptions);
                string outputPath = Path.Combine(Environment.CurrentDirectory, "SigDigits.xlsx");
                workbook.Save(outputPath);

                Console.WriteLine($"Workbook saved successfully at: {outputPath}");
                Console.WriteLine("Cell A1 displays: " + sheet.Cells["A1"].StringValue);
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"Error creating workbook: {ex.Message}");
            }
        }
    }
}
```

**Βήματα επαλήθευσης**

1. Εκτελέστε το πρόγραμμα (`dotnet run`).  
2. Ανοίξτε το `SigDigits.xlsx`.  
3. Επιβεβαιώστε ότι το **A1** εμφανίζει `123.5`.  
4. Αν ανοίξετε το XML του αρχείου (`.xlsx` είναι αρχείο zip), θα δείτε τη προσαρμοσμένη μορφή `"0.######"` αποθηκευμένη στο χαρακτηριστικό `s` του στοιχείου `<c>`.

---

## Συμπέρασμα

Σε αυτό το tutorial μάθατε πώς να **δημιουργήσετε excel workbook c#**, **εφαρμόσετε προσαρμοσμένη μορφή αριθμού**, **ορίσετε δεκαδικά ψηφία κελιού**, και **αποθηκεύσετε το βιβλίο εργασίας ως xlsx** χρησιμοποιώντας το Aspose.Cells. Η λύση δείχνει τόσο την οπτική μορφοποίηση μέσα στο Excel όσο και τη στρογγυλοποίηση κατά την εξαγωγή δεδομένων μέσω `ExportTableOptions`.  

Από εδώ μπορείτε:

* Να επεκτείνετε την προσέγγιση σε ολόκληρες περιοχές ή πίνακες.  
* Να συνδυάσετε πολλαπλά στυλ (γραμματοσειρές, περιγράμματα) με το `StyleFlag`.  
* Να αυτοματοποιήσετε τη δημιουργία αναφορών επαναλαμβάνοντας τις πηγές δεδομένων και εφαρμόζοντας την ίδια λογική μορφοποίησης.  

Μη διστάσετε να πειραματιστείτε με διαφορετικές συμβολοσειρές μορφής, αριθμούς δεκαδικών ή επιλογές εξαγωγής ώστε να ταιριάζουν στις συγκεκριμένες ανάγκες αναφοράς σας. Καλή προγραμματιστική!

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κυριαρχήσετε επιπλέον δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στα δικά σας έργα.

- [Create Excel Workbook C# – Apply Currency Format and Import DataTable](/cells/english/net/excel-data-import-export/create-excel-workbook-c-apply-currency-format-and-import-dat/)
- [Create Excel Workbook C# – Step‑by‑Step Guide with Conditional Formatting](/cells/english/net/excel-conditional-formatting/create-excel-workbook-c-step-by-step-guide-with-conditional/)
- [Create Excel Workbook C# – Add Comment & Save as XLSX](/cells/english/net/excel-comment-annotation/create-excel-workbook-c-add-comment-save-as-xlsx/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}