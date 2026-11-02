---
category: general
date: 2026-09-24
description: Δημιουργήστε προγραμματιστικά ένα βιβλίο εργασίας Excel, μάθετε πώς να
  δημιουργείτε πολλαπλά φύλλα λεπτομερειών και, στη συνέχεια, αποθηκεύστε το ως αρχείο xlsx
  με ένα σαφές παράδειγμα C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook programmatically
- how to create multiple detail sheets
- save workbook as xlsx file
language: el
lastmod: 2026-09-24
og_description: Δημιουργήστε βιβλίο εργασίας Excel προγραμματιστικά, δείτε πώς να
  δημιουργήσετε πολλαπλά φύλλα λεπτομερειών και να αποθηκεύσετε το βιβλίο εργασίας
  ως αρχείο xlsx σε ένα ενιαίο, εκτελέσιμο παράδειγμα.
og_image_alt: Screenshot of an Excel workbook created programmatically in C#
og_title: Δημιουργία βιβλίου εργασίας Excel προγραμματιστικά – πλήρης οδηγός C#
schemas:
- author: Aspose
  dateModified: '2026-09-24'
  description: Create Excel workbook programmatically and learn how to create multiple
    detail sheets, then save workbook as xlsx file with a clear C# example.
  headline: Create Excel workbook programmatically using Smart Markers
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
title: Δημιουργία βιβλίου εργασίας Excel προγραμματιστικά χρησιμοποιώντας Smart Markers
url: /el/net/smart-markers-dynamic-data/create-excel-workbook-programmatically-using-smart-markers/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία βιβλίου εργασίας Excel προγραμματιστικά χρησιμοποιώντας Smart Markers

Αν χρειάζεστε **να δημιουργήσετε προγραμματιστικά ένα βιβλίο εργασίας Excel**, αυτός ο οδηγός σας δείχνει ακριβώς πώς να το κάνετε με το Aspose.Cells .NET. Θα ανακαλύψετε επίσης **πώς να δημιουργήσετε πολλαπλά φύλλα λεπτομερειών** από μια μοναδική πηγή δεδομένων και τελικά **να αποθηκεύσετε το βιβλίο εργασίας ως αρχείο xlsx** χωρίς κανένα χειροκίνητο βήμα.  

Η λύση είναι αυτόνομη: περπατάμε μέσα από κάθε γραμμή κώδικα, εξηγούμε γιατί κάθε ρύθμιση είναι σημαντική και καλύπτουμε κοινά προβλήματα όπως τα διπλότυπα ονόματα φύλλων. Στο τέλος θα έχετε μια έτοιμη για εκτέλεση εφαρμογή console που παράγει ένα βιβλίο εργασίας με ένα κύριο φύλλο και ένα σύνολο φύλλων λεπτομερειών.

## Τι θα χρειαστείτε

| Προαπαιτούμενο | Λόγος |
|--------------|--------|
| .NET 6.0 SDK or later | Παρέχει το runtime για την εφαρμογή console C# |
| Aspose.Cells for .NET (NuGet package `Aspose.Cells`) | Παρέχει τις κλάσεις `Workbook`, `SmartMarkerProcessor` και `SmartMarkerOptions` |
| A simple data source (e.g., `DataTable` or a list of objects) | Παρέχει τις τιμές που θα επεκτείνουν τα Smart Markers |
| Visual Studio 2022 or any editor that supports .NET | Διευκολύνει τη μεταγλώττιση και την εκτέλεση του κώδικα |

> **Pro tip:** Εγκαταστήστε το πακέτο Aspose.Cells μέσω του CLI πριν ξεκινήσετε:  
> `dotnet add package Aspose.Cells`

## Βήμα 1: Ρύθμιση του έργου και εισαγωγή namespaces

Δημιουργήστε ένα νέο έργο console και φέρετε τα απαιτούμενα namespaces στο πεδίο ορατότητας.

```csharp
using System;
using System.Data;               // For DataTable (sample data source)
using Aspose.Cells;              // Core Excel API
using Aspose.Cells.SmartMarkers; // Smart Marker processing
```

*Why this matters*: `Aspose.Cells` διαχειρίζεται τον κύκλο ζωής του βιβλίου εργασίας, ενώ `Aspose.Cells.SmartMarkers` σας παρέχει τη δυνατότητα του ισχυρού κινητήρα Smart Marker που μπορεί να δημιουργήσει πολλά φύλλα από ένα μόνο πρότυπο.

## Βήμα 2: Δημιουργία του βιβλίου εργασίας Excel προγραμματιστικά

Η πρώτη συγκεκριμένη ενέργεια είναι η δημιουργία ενός αντικειμένου `Workbook`. Αυτό το αντικείμενο αντιπροσωπεύει ολόκληρο το αρχείο Excel στη μνήμη.

```csharp
// Step 2: Create a new workbook (or load an existing template)
Workbook workbook = new Workbook(); // an empty workbook with one default sheet
```

Αν προτιμάτε να ξεκινήσετε από ένα πρότυπο που ήδη περιέχει γραμμές κεφαλίδας ή μορφοποίηση, αντικαταστήστε το `new Workbook()` με `new Workbook("Template.xlsx")`. Το υπόλοιπο της διαδικασίας λειτουργεί ταυτόσημα.

## Βήμα 3: Προετοιμασία προτύπου Smart Marker

Τα Smart Markers λειτουργούν σε περιεχόμενα κελιών που περιέχουν placeholders όπως `&=Employees.Name`. Για αυτό το tutorial θα προσθέσουμε ένα απλό πρότυπο απευθείας μέσω κώδικα, αλλά μπορείτε επίσης να επεξεργαστείτε το φύλλο χειροκίνητα στο Excel.

```csharp
// Access the first worksheet (index 0)
Worksheet sheet = workbook.Worksheets[0];

// Write a header row
sheet.Cells["A1"].PutValue("Employee Report");

// Insert a Smart Marker that will generate a detail sheet for each employee
sheet.Cells["A3"].PutValue("&=Employees.Name");

// Optional: add column titles for the detail sheet
sheet.Cells["A4"].PutValue("Name");
sheet.Cells["B4"].PutValue("Department");
sheet.Cells["C4"].PutValue("Salary");
```

*Why this matters*: Το placeholder `&=Employees.Name` λέει στον επεξεργαστή Smart Marker να επαναλάβει τη συλλογή `Employees`. Κάθε επανάληψη θα δημιουργήσει ένα νέο φύλλο εργασίας επειδή θα ρυθμίσουμε τον επεξεργαστή να δημιουργεί ένα **detail sheet** για κάθε γραμμή.

## Βήμα 4: Δημιουργία πηγής δεδομένων που περιέχει πολλαπλές γραμμές

Θα χρησιμοποιήσουμε ένα `DataTable` ως γρήγορο τρόπο προσομοίωσης μιας συλλογής εγγραφών υπαλλήλων.

```csharp
// Step 4: Create a DataTable with sample employee data
DataTable employees = new DataTable("Employees");
employees.Columns.Add("Name", typeof(string));
employees.Columns.Add("Department", typeof(string));
employees.Columns.Add("Salary", typeof(decimal));

employees.Rows.Add("Alice Johnson", "Finance", 72000);
employees.Rows.Add("Bob Smith", "Engineering", 95000);
employees.Rows.Add("Carol Lee", "Marketing", 63000);
```

Μπορείτε να το αντικαταστήσετε με οποιοδήποτε `IEnumerable` (π.χ., `List<Employee>`) – τα Smart Markers δέχονται οποιαδήποτε πηγή δεδομένων που υλοποιεί το `IEnumerable`.

## Βήμα 5: Διαμόρφωση επιλογών Smart Marker – πώς να δημιουργήσετε πολλαπλά φύλλα λεπτομερειών

Από προεπιλογή, τα Smart Markers γράφουν δεδομένα πίσω στο ίδιο φύλλο. Για να δημιουργήσετε **multiple detail sheets**, πρέπει να ορίσετε την ιδιότητα `DetailSheetNewName`. Αυτό επίσης δείχνει **πώς να δημιουργήσετε πολλαπλά φύλλα λεπτομερειών** χωρίς συγκρούσεις ονομάτων.

```csharp
// Step 5: Configure Smart Marker options
SmartMarkerOptions smOptions = new SmartMarkerOptions
{
    // Each iteration will create a new sheet named "Detail"
    DetailSheetNewName = "Detail"
};
```

Αν η πηγή δεδομένων περιέχει διπλότυπα ονόματα, ο επεξεργαστής προσθέτει αυτόματα ένα αριθμητικό επίθημα (π.χ., `Detail_1`, `Detail_2`). Αυτό αποτρέπει σφάλματα χρόνου εκτέλεσης και διασφαλίζει ότι όλα τα φύλλα λεπτομερειών αποθηκεύονται.

## Βήμα 6: Επεξεργασία των Smart Markers

Τώρα καλούμε τον επεξεργαστή, περνώντας τη πηγή δεδομένων και τις επιλογές που μόλις ορίσαμε.

```csharp
// Step 6: Process Smart Markers
workbook.Worksheets[0].SmartMarkerProcessor.Process(employees, smOptions);
```

*Why this matters*: Ο επεξεργαστής διαβάζει το placeholder `&=Employees.Name`, επαναλαμβάνει κάθε γραμμή του `employees`, δημιουργεί ένα νέο φύλλο με όνομα “Detail” και γράφει τα δεδομένα της γραμμής σε αυτό το φύλλο. Το αρχικό φύλλο παραμένει ως σύνοψη ή κύριο φύλλο.

## Βήμα 7: Αποθήκευση βιβλίου εργασίας ως αρχείο xlsx

Τέλος, αποθηκεύστε το βιβλίο εργασίας στο δίσκο χρησιμοποιώντας το πρότυπο **save workbook as xlsx file**.

```csharp
// Step 7: Save the resulting workbook
string outputPath = @"./output/detail.xlsx";
workbook.Save(outputPath, SaveFormat.Xlsx);
Console.WriteLine($"Workbook saved to {outputPath}");
```

Η παράμετρος `SaveFormat.Xlsx` εγγυάται ότι το αρχείο αποθηκεύεται στη σύγχρονη μορφή Office Open XML, η οποία είναι συμβατή με το Excel 2007+ και τις περισσότερες υπηρεσίες cloud.

## Πλήρες, εκτελέσιμο παράδειγμα

Αντιγράψτε τον παρακάτω κώδικα στο `Program.cs` ενός .NET console project και εκτελέστε το. Το πρόγραμμα θα δημιουργήσει το `detail.xlsx` στο φάκελο `output`, περιέχοντας ένα κύριο φύλλο και τρία φύλλα λεπτομερειών (ένα ανά υπάλληλο).

```csharp
using System;
using System.Data;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace ExcelSmartMarkerDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create an empty workbook
            Workbook workbook = new Workbook();

            // 2️⃣ Build a simple template with a Smart Marker
            Worksheet sheet = workbook.Worksheets[0];
            sheet.Cells["A1"].PutValue("Employee Report");
            sheet.Cells["A3"].PutValue("&=Employees.Name");
            sheet.Cells["A4"].PutValue("Name");
            sheet.Cells["B4"].PutValue("Department");
            sheet.Cells["C4"].PutValue("Salary");

            // 3️⃣ Prepare the data source
            DataTable employees = new DataTable("Employees");
            employees.Columns.Add("Name", typeof(string));
            employees.Columns.Add("Department", typeof(string));
            employees.Columns.Add("Salary", typeof(decimal));

            employees.Rows.Add("Alice Johnson", "Finance", 72000);
            employees.Rows.Add("Bob Smith", "Engineering", 95000);
            employees.Rows.Add("Carol Lee", "Marketing", 63000);

            // 4️⃣ Configure Smart Marker options (how to create multiple detail sheets)
            SmartMarkerOptions smOptions = new SmartMarkerOptions
            {
                DetailSheetNewName = "Detail"
            };

            // 5️⃣ Process the markers
            workbook.Worksheets[0].SmartMarkerProcessor.Process(employees, smOptions);

            // 6️⃣ Save workbook as xlsx file
            string outPath = "./output/detail.xlsx";
            workbook.Save(outPath, SaveFormat.Xlsx);
            Console.WriteLine($"Workbook saved to {outPath}");
        }
    }
}
```

**Αναμενόμενο αποτέλεσμα**

- `output/detail.xlsx` contains:
  - **Sheet1** – το αρχικό πρότυπο με την κεφαλίδα “Employee Report”.
  - **Detail** – πρώτο φύλλο λεπτομερειών με την εγγραφή της Alice.
  - **Detail_1** – δεύτερο φύλλο λεπτομερειών με την εγγραφή του Bob.
  - **Detail_2** – τρίτο φύλλο λεπτομερειών με την εγγραφή της Carol.

Ανοίξτε το αρχείο στο Excel και θα δείτε κάθε υπάλληλο σε δικό του φύλλο, αποδεικνύοντας ότι δημιουργήσαμε επιτυχώς **create multiple detail sheets** και **save workbook as xlsx file**.

## Συχνές ερωτήσεις & διαχείριση ειδικών περιπτώσεων

| Ερώτηση | Απάντηση |
|----------|--------|
| *Τι γίνεται αν χρειάζομαι προσαρμοσμένο όνομα για κάθε φύλλο λεπτομερειών;* | Ορίστε `DetailSheetNewName = "Employee_"` και συμπεριλάβετε μια στήλη με όνομα `SheetName` στην πηγή δεδομένων. Ο επεξεργαστής θα προσθέσει την τιμή του `SheetName` στο βασικό όνομα. |
| *Μπορώ να διατηρήσω το αρχικό φύλλο ως σύνοψη όλων των λεπτομερειών;* | Ναι. Το κύριο φύλλο παραμένει αμετάβλητο· μπορείτε να προσθέσετε τύπους που αναφέρονται στα παραγόμενα φύλλα λεπτομερειών. |
| *Τι συμβαίνει όταν η πηγή δεδομένων είναι κενή;* | Δεν δημιουργούνται φύλλα λεπτομερειών, αλλά το βιβλίο εργασίας αποθηκεύεται. Σκεφτείτε να ελέγξετε το `employees.Rows.Count` πριν την επεξεργασία αν χρειάζεστε ειδική διαχείριση. |
| *Μπορεί να χρησιμοποιηθεί υπάρχον αρχείο προτύπου;* | Αντικαταστήστε το `new Workbook()` με `new Workbook("Template.xlsx")`. Όλη η λογική Smart Marker λειτουργεί με τον ίδιο τρόπο. |

## Συμπέρασμα

Τώρα γνωρίζετε **πώς να δημιουργήσετε Excel workbook προγραμματιστικά**, πώς να **δημιουργήσετε πολλαπλά φύλλα λεπτομερειών** χρησιμοποιώντας Smart Markers, και πώς να **αποθηκεύσετε το βιβλίο εργασίας ως αρχείο xlsx** με το Aspose.Cells. Το πλήρες παράδειγμα μπορεί να προσαρμοστεί για τιμολόγια, αναφορές ή οποιοδήποτε σενάριο όπου απαιτείται έξοδος Excel master‑detail.

### Επόμενα βήματα

- Εξερευνήστε άλλες δυνατότητες Smart Marker όπως **group markers** και **conditional formatting**.
- Αντικαταστήστε το `DataTable` με ένα πραγματικό ερώτημα βάσης δεδομένων για τη δημιουργία μεγάλων αναφορών.
- Χρησιμοποιήστε `Workbook.Save("output.pdf", SaveFormat.Pdf)` για να εξάγετε τα ίδια δεδομένα σε PDF για διανομή.

Μη διστάσετε να πειραματιστείτε με διαφορετικά σχήματα ονοματοδοσίας, στυλ ή επιπλέον φύλλα εργασίας—οι νέες σας δεξιότητες προγραμματιστικής δημιουργίας Excel είναι έτοιμες για παραγωγική χρήση. Καλή προγραμματιστική!

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που βασίζονται στις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικά παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Create Excel Workbook C# – Add Comment & Save as XLSX](/cells/english/net/excel-comment-annotation/create-excel-workbook-c-add-comment-save-as-xlsx/)
- [Create New Workbook in C# – Add Formula and Save Excel File](/cells/english/net/excel-workbook/create-new-workbook-in-c-add-formula-and-save-excel-file/)
- [Create Excel Workbook C# – Insert JSON and Save as XLSX](/cells/english/net/excel-data-import-export/create-excel-workbook-c-insert-json-and-save-as-xlsx/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}