---
category: general
date: 2026-11-25
description: Μάθετε πώς να δημιουργείτε πολλαπλά φύλλα σε ένα αρχείο Excel χρησιμοποιώντας
  C#. Αυτός ο οδηγός καλύπτει την αποθήκευση του βιβλίου εργασίας ως XLSX και τη διαχείριση
  διπλών ονομάτων φύλλων.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create multiple sheets
- create excel file c#
- duplicate sheet names
- save workbook xlsx
language: el
lastmod: 2026-11-25
og_description: Δημιουργήστε πολλαπλά φύλλα σε ένα αρχείο Excel χρησιμοποιώντας C#.
  Ακολουθήστε αυτό το πλήρες σεμινάριο για να αποθηκεύσετε το βιβλίο εργασίας ως XLSX
  και να διαχειριστείτε τα διπλότυπα ονόματα φύλλων.
og_image_alt: Code editor showing C# sample that generates an Excel workbook with
  several detail sheets
og_title: Δημιουργήστε πολλαπλά φύλλα σε ένα αρχείο Excel με C# – οδηγός βήμα‑προς‑βήμα
schemas:
- author: Aspose
  dateModified: '2026-11-25'
  description: Learn how to create multiple sheets in an Excel file using C#. This
    guide covers saving the workbook as XLSX and handling duplicate sheet names.
  headline: How to create multiple sheets in an Excel file using C#
  type: TechArticle
- description: Learn how to create multiple sheets in an Excel file using C#. This
    guide covers saving the workbook as XLSX and handling duplicate sheet names.
  name: How to create multiple sheets in an Excel file using C#
  steps:
  - name: '**Create a new workbook** and name the first worksheet *Master*.'
    text: '**Create a new workbook** and name the first worksheet *Master*.'
  - name: '**Insert a smart marker** that tells Aspose.Cells how to name the detail
      worksheets.'
    text: '**Insert a smart marker** that tells Aspose.Cells how to name the detail
      worksheets.'
  - name: '**Process the smart marker** with a data source that may contain duplicate
      names.'
    text: '**Process the smart marker** with a data source that may contain duplicate
      names.'
  - name: '**Save the workbook** as an XLSX file.'
    text: '**Save the workbook** as an XLSX file.'
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
- Automation
title: Πώς να δημιουργήσετε πολλαπλά φύλλα σε ένα αρχείο Excel χρησιμοποιώντας C#
url: /el/net/worksheet-management/how-to-create-multiple-sheets-in-an-excel-file-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να δημιουργήσετε πολλαπλά φύλλα σε ένα αρχείο Excel χρησιμοποιώντας C#

Αν χρειάζεται να **δημιουργήσετε πολλαπλά φύλλα** σε ένα βιβλίο εργασίας Excel από C#, αυτό το tutorial σας παρέχει μια έτοιμη λύση. Στο τέλος του οδηγού θα έχετε ένα πρόγραμμα που δημιουργεί ένα κύριο φύλλο, δημιουργεί φύλλα λεπτομερειών μέσω smart markers και αποθηκεύει το αποτέλεσμα ως αρχείο **XLSX**—ενώ διαχειρίζεται με ασφάλεια **διπλά ονόματα φύλλων**.

Θα δείτε επίσης πώς να **create excel file c#** έργα με τη βιβλιοθήκη Aspose.Cells, μια δημοφιλής επιλογή για αυτοματοποίηση λογιστικών φύλλων από τον διακομιστή.

## Προαπαιτούμενα

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

* .NET 6.0 SDK ή νεότερο εγκατεστημένο  
* Visual Studio 2022 (ή οποιοδήποτε IDE που υποστηρίζει .NET)  
* Το πακέτο NuGet **Aspose.Cells for .NET** (`Aspose.Cells`) – παρέχει τις κλάσεις `Workbook`, `Worksheet` και `SmartMarkersFactory` που χρησιμοποιούνται στον κώδικα.  

Μπορείτε να προσθέσετε το πακέτο με την ακόλουθη εντολή CLI:

```bash
dotnet add package Aspose.Cells
```

> **Pro tip:** Χρησιμοποιήστε ιδιωτικό NuGet feed ή την δωρεάν έκδοση community αν χρειάζεστε μόνο βασικές λειτουργίες.

## Επισκόπηση της λύσης

Η προσέγγιση αποτελείται από τέσσερα λογικά βήματα:

1. **Δημιουργία νέου βιβλίου εργασίας** και ονομασία του πρώτου φύλλου *Master*.  
2. **Εισαγωγή smart marker** που λέει στο Aspose.Cells πώς να ονομάσει τα φύλλα λεπτομερειών.  
3. **Επεξεργασία του smart marker** με μια πηγή δεδομένων που μπορεί να περιέχει διπλά ονόματα.  
4. **Αποθήκευση του βιβλίου εργασίας** ως αρχείο XLSX.

Κάθε βήμα εξηγείται λεπτομερώς παρακάτω, και το πλήρες αρχείο πηγαίου κώδικα παρέχεται στο τέλος του άρθρου.

## Βήμα 1: Δημιουργία νέου βιβλίου εργασίας και προσθήκη κύριου φύλλου

Η κλάση `Workbook` αντιπροσωπεύει ολόκληρο το αρχείο Excel. Όταν την δημιουργείτε χωρίς παραμέτρους, το Aspose.Cells δημιουργεί ένα προεπιλεγμένο βιβλίο εργασίας που περιέχει ήδη ένα φύλλο. Η μετονομασία αυτού του φύλλου σε *Master* κάνει σαφές το σκοπό του.

```csharp
using Aspose.Cells;
using System;
using System.Data;   // For DataTable used as a data source

// 1️⃣ Create a new workbook
Workbook workbook = new Workbook();

// 1️⃣ Retrieve the first worksheet (index 0) and give it a friendly name
Worksheet masterSheet = workbook.Worksheets[0];
masterSheet.Name = "Master";
```

**Γιατί είναι σημαντικό:**  
Η εκκίνηση με ένα καθαρό βιβλίο εργασίας αποφεύγει υπολειπόμενη μορφοποίηση ή κρυφά φύλλα από προηγούμενες εκτελέσεις. Η ονομασία του φύλλου *Master* σας βοηθά να εντοπίσετε το smart marker αργότερα και κρατά το αρχείο αναγνώσιμο για μη‑τεχνικούς χρήστες.

## Βήμα 2: Εισαγωγή smart marker που ορίζει τα ονόματα των φύλλων λεπτομερειών

Τα smart markers είναι placeholders που το Aspose.Cells αντικαθιστά με δεδομένα κατά το χρόνο εκτέλεσης. Η σύνταξη `&=DetailSheetNewName=Detail` λέει στη μηχανή να δημιουργήσει νέο φύλλο για κάθε γραμμή στην πηγή δεδομένων, χρησιμοποιώντας την τιμή της στήλης `Detail` ως όνομα φύλλου.

```csharp
// 2️⃣ Place a smart marker in cell A1 of the master sheet
masterSheet.Cells["A1"].PutValue("&=DetailSheetNewName=Detail");
```

**Γιατί είναι σημαντικό:**  
Το smart marker εξαλείφει την ανάγκη να γράψετε βρόχο που προσθέτει φύλλα χειροκίνητα. Επίσης, αντιγράφει αυτόματα τη διάταξη του κύριου φύλλου σε κάθε νέο φύλλο, εξασφαλίζοντας συνεπή στυλ.

## Βήμα 3: Επεξεργασία του smart marker με πηγή δεδομένων που μπορεί να περιέχει διπλότυπα

Παρακάτω δημιουργούμε ένα `DataTable` που προσομοιώνει πηγή δεδομένων. Παρατηρήστε ότι η στήλη *Detail* περιέχει διπλές τιμές (`"Report"` εμφανίζεται δύο φορές). Η μέθοδος `SmartMarkersFactory.Process` σέβεται τη ρύθμιση `AllowDuplicateSheetNames`, η οποία είναι **true** εξ ορισμού για αυτό το παράδειγμα.

```csharp
// 3️⃣ Build a sample data source (DataTable) with duplicate sheet names
DataTable dataSource = new DataTable();
dataSource.Columns.Add("Detail", typeof(string));
dataSource.Columns.Add("Value", typeof(double));

// Add rows – "Report" appears twice to demonstrate duplicate handling
dataSource.Rows.Add("Report", 123.45);
dataSource.Rows.Add("Summary", 67.89);
dataSource.Rows.Add("Report", 101.12);   // Duplicate sheet name

// Register the data source in the workbook's data collection
workbook.Worksheets[0].SmartMarkersFactory.Process(new[] { "dataSource" });
```

> **Important:** Αν χρειάζεται να εγγυηθείτε μοναδικά ονόματα φύλλων, ορίστε `workbook.Settings.CheckDuplicateSheetNames = true;` πριν την επεξεργασία. Η προεπιλεγμένη συμπεριφορά δημιουργεί φύλλα με το ίδιο όνομα, κάτι που το Excel επιτρέπει αλλά μπορεί να προκαλέσει σύγχυση κατά την περιήγηση στο αρχείο.

## Βήμα 4: Αποθήκευση του βιβλίου εργασίας ως αρχείο XLSX

Τέλος, αποθηκεύουμε το παραγόμενο βιβλίο εργασίας στο δίσκο. Η μέθοδος `Save` επιλέγει αυτόματα τον κατάλληλο writer βάσει της επέκτασης του αρχείου.

```csharp
// 4️⃣ Save the workbook – the file will contain the master sheet and two "Report" sheets plus a "Summary" sheet
string outputPath = @"C:\Temp\duplicate_detail_sheets.xlsx";
workbook.Save(outputPath, SaveFormat.Xlsx);

Console.WriteLine($"Workbook saved to {outputPath}");
```

**Αναμενόμενο αποτέλεσμα**

Όταν ανοίξετε το `duplicate_detail_sheets.xlsx` θα δείτε:

| Sheet Name | Content (first row) |
|------------|---------------------|
| Master     | Smart marker placeholder (no data) |
| Report     | Data row 1 (`123.45`) |
| Summary    | Data row 2 (`67.89`) |
| Report (2) | Data row 3 (`101.12`) |

Το δεύτερο φύλλο *Report* μετονομάζεται αυτόματα σε *Report (2)* από το Aspose.Cells για να αποφευχθεί σκληρό σφάλμα, διατηρώντας όμως την αρχική πρόθεση του διπλού ονόματος.

## Πλήρης πηγαίος κώδικας

Αντιγράψτε το παρακάτω αρχείο σε ένα console project (`dotnet new console`) και τρέξτε το. Το πρόγραμμα δείχνει την πλήρη ροή εργασίας για **create multiple sheets** και **save workbook xlsx** ενώ διαχειρίζεται **duplicate sheet names**.

```csharp
// Program.cs
using Aspose.Cells;
using System;
using System.Data;

namespace ExcelMultipleSheetsDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook and name the first sheet "Master"
            Workbook workbook = new Workbook();
            Worksheet masterSheet = workbook.Worksheets[0];
            masterSheet.Name = "Master";

            // Step 2: Add a smart marker that will generate detail sheets
            masterSheet.Cells["A1"].PutValue("&=DetailSheetNewName=Detail");

            // Step 3: Prepare a data source with duplicate sheet names
            DataTable dataSource = new DataTable();
            dataSource.Columns.Add("Detail", typeof(string));
            dataSource.Columns.Add("Value", typeof(double));

            dataSource.Rows.Add("Report", 123.45);
            dataSource.Rows.Add("Summary", 67.89);
            dataSource.Rows.Add("Report", 101.12); // duplicate name

            // Bind the data source to the workbook
            workbook.Worksheets[0].SmartMarkersFactory.Process(new[] { "dataSource" });

            // Step 4: Save the workbook as an XLSX file
            string outputPath = @"C:\Temp\duplicate_detail_sheets.xlsx";
            workbook.Save(outputPath, SaveFormat.Xlsx);

            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

Τρέξτε `dotnet run` από το φάκελο του έργου. Μετά την εκτέλεση, ανοίξτε το παραγόμενο αρχείο για να επαληθεύσετε ότι δημιουργήθηκαν τρία φύλλα λεπτομερειών, δύο από τα οποία μοιράζονται το βασικό όνομα **Report**.

## Διαχείριση ειδικών περιπτώσεων και βέλτιστες πρακτικές

| Situation | Recommended approach |
|-----------|----------------------|
| **Very large data sets** ( > 10 000 rows) | Use `WorkbookSettings.MemorySetting = MemorySetting.MemoryPreference;` to reduce memory pressure. |
| **Custom sheet naming rules** | Pre‑process the `Detail` column to replace illegal characters (`/ \ ? * [ ] :`) before calling `Process`. |
| **Need truly unique names** | Set `workbook.Settings.CheckDuplicateSheetNames = true;` and provide a fallback naming scheme (e.g., append a GUID). |
| **Generating PDFs instead of XLSX** | After saving, call `workbook.Save("output.pdf", SaveFormat.Pdf);` – Aspose.Cells can export directly to PDF. |
| **Running in a web service** | Write the workbook to a `MemoryStream` and return it as a file download to avoid disk I/O. |

### Pro tip: reuse the same `Workbook` instance for multiple exports

Αν η εφαρμογή σας δημιουργεί πολλές αναφορές ανά αίτημα, κρατήστε ένα μόνο αντικείμενο `Workbook` στη μνήμη, καθαρίστε τα φύλλα του (`workbook.Worksheets.Clear();`) και επαναλάβετε τα βήματα. Αυτό αποφεύγει το κόστος φόρτωσης του runtime του Aspose.Cells επανειλημμένα.

## Συμπέρασμα

Τώρα ξέρετε πώς να **create multiple sheets** σε ένα βιβλίο εργασίας Excel χρησιμοποιώντας C#, πώς να **create excel file c#** με το Aspose.Cells, πώς να διαχειριστείτε **duplicate sheet names**, και πώς να **save workbook xlsx** αξιόπιστα. Το πλήρες παράδειγμα παρουσιάζει ένα καθαρό, συντηρήσιμο μοτίβο που κλιμακώνεται από γρήγορα σενάρια έως υπηρεσίες παραγωγικής κλίμακας.

### Τι θα ακολουθήσει;

* Εξερευνήστε **conditional formatting** στα παραγόμενα φύλλα για να επισημάνετε κρίσιμες τιμές.  
* Χρησιμοποιήστε **Smart Markers** για αυτόματη συμπλήρωση πινάκων, γραφημάτων ή pivot tables.  
* Ενσωματώστε τον κώδικα σε ένα ASP.NET Core API και επιστρέψτε το αρχείο XLSX ως ροή λήψης.

Μη διστάσετε να πειραματιστείτε με διαφορετικές πηγές δεδομένων (JSON, XML ή βάση δεδομένων) και να προσαρμόσετε τη σύνταξη του smart marker ώστε να ταιριάζει στις ανάγκες αναφοράς σας. Καλό κώδικα!

## Τι πρέπει να μάθετε στη συνέχεια;

Οι παρακάτω οδηγίες καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κυριαρχήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στην υλοποίηση.

- [Create Excel Workbook C# – Step‑by‑Step Guide to Write Dates & Save as XLSX](/cells/english/net/excel-workbook/create-excel-workbook-c-step-by-step-guide-to-write-dates-sa/)
- [Create New Workbook in C# – Add Formula and Save Excel File](/cells/english/net/excel-workbook/create-new-workbook-in-c-add-formula-and-save-excel-file/)
- [Create excel workbook and save it to file in C#](/cells/english/net/excel-workbook/create-excel-workbook-and-save-it-to-file-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}