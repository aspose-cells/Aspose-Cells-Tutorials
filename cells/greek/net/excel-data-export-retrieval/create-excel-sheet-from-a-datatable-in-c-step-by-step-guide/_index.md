---
category: general
date: 2026-08-11
description: Δημιουργήστε φύλλο Excel από ένα DataTable σε C# και εξάγετε το DataTable
  σε Excel με αυτόματη ονομασία φύλλου. Μάθετε πώς να προσθέτετε γραμμές σε DataTable
  και να αποθηκεύετε το βιβλίο εργασίας ως xlsx.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel sheet
- export datatable to excel
- add rows to datatable
- create multiple excel sheets
- save workbook as xlsx
language: el
lastmod: 2026-08-11
og_description: Δημιουργήστε φύλλο Excel από ένα DataTable σε C#. Αυτό το σεμινάριο
  δείχνει πώς να εξάγετε το DataTable σε Excel, να προσθέσετε γραμμές στο DataTable,
  να δημιουργήσετε πολλαπλά φύλλα Excel και να αποθηκεύσετε το βιβλίο εργασίας ως
  xlsx.
og_image_alt: Screenshot of an Excel workbook created from a DataTable with automatically
  renamed sheets
og_title: Δημιουργία φύλλου Excel από DataTable σε C# – πλήρης οδηγός προγραμματισμού
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: Create excel sheet from a DataTable in C# and export datatable to excel
    with automatic sheet naming. Learn how to add rows to datatable and save workbook
    as xlsx.
  headline: Create excel sheet from a DataTable in C# – step‑by‑step guide
  type: TechArticle
tags:
- C#
- Excel automation
- Aspose.Cells
title: Δημιουργία φύλλου Excel από DataTable σε C# – βήμα‑βήμα οδηγός
url: /el/net/excel-data-export-retrieval/create-excel-sheet-from-a-datatable-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία φύλλου Excel από DataTable σε C# – οδηγός βήμα‑βήμα

Αν χρειάζεστε **δημιουργία φύλλου Excel** από ένα `DataTable` σε C#, αυτός ο οδηγός σας δείχνει ακριβώς πώς να το κάνετε. Θα δείτε πώς να **εξάγετε datatable σε excel**, να προσθέσετε γραμμές, να διαχειριστείτε διπλά ονόματα φύλλων και, τέλος, να **αποθηκεύσετε το βιβλίο εργασίας ως xlsx**.

Το παράδειγμα χρησιμοποιεί το Aspose.Cells, μια ευρέως χρησιμοποιούμενη βιβλιοθήκη .NET για αυτοματοποίηση Excel. Οι ίδιες έννοιες ισχύουν και για άλλες βιβλιοθήκες που υποστηρίζουν επεξεργασία τύπου SmartMarker, αλλά ο παρακάτω κώδικας λειτουργεί αμέσως με το Aspose.Cells 22.12 ή νεότερο.

## Προαπαιτούμενα

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

* .NET 6.0 SDK ή νεότερο εγκατεστημένο  
* Αναφορά στο πακέτο NuGet **Aspose.Cells** (`Install-Package Aspose.Cells`)  
* Βασική εξοικείωση με `DataTable` και εφαρμογές κονσόλας C#  

Αυτές οι απαιτήσεις διατηρούν το tutorial αυτόνομο και αποφεύγουν εξωτερικά εργαλεία.

## Βήμα 1: Δημιουργία DataTable που θα εξαχθεί σε Excel

Το πρώτο βήμα είναι η δημιουργία ενός `DataTable` που αντικατοπτρίζει τα δεδομένα που θέλετε στο φύλλο εργασίας. Εδώ δημιουργούμε έναν πίνακα με όνομα **Sheet1**, προσθέτουμε μια στήλη `Id` και εισάγουμε δύο γραμμές.

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a DataTable named "Sheet1"
        DataTable dataTable = new DataTable("Sheet1");
        dataTable.Columns.Add("Id", typeof(int));

        // 2️⃣ Add rows to the DataTable
        dataTable.Rows.Add(1);
        dataTable.Rows.Add(2);

        // Subsequent steps are called from here
        ProcessAndSaveWorkbook(dataTable);
    }
```

**Γιατί είναι σημαντικό:**  
`DataTable` είναι μια βολική αναπαράσταση δεδομένων σε μνήμη. Το όνομα του πίνακα `"Sheet1"` λέει στο Aspose.Cells ποιο φύλλο να στοχεύσει κατά την επεξεργασία SmartMarkers.

## Βήμα 2: Προσθήκη γραμμών στο DataTable (προαιρετική επέκταση)

Αν τα πηγαία σας δεδομένα είναι δυναμικά, συχνά θα χρειαστεί να προσθέτετε γραμμές σε βρόχο. Το παρακάτω απόσπασμα δείχνει ένα τυπικό μοτίβο:

```csharp
        // Example: add rows from a collection
        int[] ids = { 3, 4, 5 };
        foreach (int id in ids)
        {
            dataTable.Rows.Add(id);
        }
```

**Συμβουλή:** Όταν προσθέτετε πολλές γραμμές, σκεφτείτε να απενεργοποιήσετε τους περιορισμούς (`dataTable.Constraints.Clear()`) για να βελτιώσετε την απόδοση.

## Βήμα 3: Ρύθμιση επιλογών SmartMarker για αυτόματη δημιουργία πολλαπλών φύλλων Excel

Οι επιλογές SmartMarker σας επιτρέπουν να ελέγχετε πώς διαχειρίζονται τα διπλά ονόματα φύλλων. Ορίζοντας το `DetailSheetNewName` σε `"Sheet1_{0}"` λέτε στο Aspose.Cells να μετονομάζει τα επόμενα φύλλα ως `Sheet1_1`, `Sheet1_2` κ.λπ.

```csharp
    private static void ProcessAndSaveWorkbook(DataTable dataTable)
    {
        // 3️⃣ Set SmartMarker options for automatic sheet renaming
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
        {
            // New sheets will be named Sheet1_1, Sheet1_2, etc.
            DetailSheetNewName = "Sheet1_{0}"
        };
```

**Γιατί είναι σημαντικό:**  
Όταν επεξεργάζεστε πολλά αντικείμενα `DataTable` που έχουν το ίδιο όνομα, το Excel κανονικά θα πετάξει σφάλμα επειδή τα ονόματα φύλλων πρέπει να είναι μοναδικά. Το πρότυπο `DetailSheetNewName` εξαλείφει αυτό το πρόβλημα αυτόματα.

## Βήμα 4: Επεξεργασία SmartMarkers και εξαγωγή datatable σε excel

Τώρα δημιουργούμε ένα νέο `Workbook`, εκτελούμε `ProcessSmartMarkers` και αφήνουμε το Aspose.Cells να γεμίσει το(α) φύλλο(α) εργασίας βάσει του `DataTable`.

```csharp
        // 4️⃣ Create a workbook and process SmartMarkers
        Workbook workbook = new Workbook();
        workbook.ProcessSmartMarkers(dataTable, smartMarkerOptions);
```

**Εξήγηση:**  
`ProcessSmartMarkers` σαρώει το βιβλίο εργασίας για δείκτες όπως `&=Sheet1!A1` (δεν φαίνονται εδώ) και τους αντικαθιστά με τα δεδομένα από το `dataTable`. Επειδή ξεκινήσαμε με ένα κενό βιβλίο εργασίας, το Aspose.Cells δημιουργεί ένα νέο φύλλο που ταιριάζει με το όνομα του πίνακα και το γεμίζει με τις γραμμές που προσθέσαμε.

## Βήμα 5: Αποθήκευση βιβλίου εργασίας ως xlsx

Τέλος, γράψτε το βιβλίο εργασίας στο δίσκο με τη σύγχρονη μορφή OpenXML (`.xlsx`). Μπορείτε να αλλάξετε τη διαδρομή ώστε να ταιριάζει στο περιβάλλον σας.

```csharp
        // 5️⃣ Save the workbook as an .xlsx file
        string outputPath = @"YOUR_DIRECTORY\DuplicateSheets.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

**Αποτέλεσμα:**  
Η εκτέλεση του προγράμματος παράγει ένα αρχείο Excel που περιέχει:

| Όνομα φύλλου | Γραμμές |
|--------------|--------|
| Sheet1       | 1, 2, 3, 4, 5 |
| Sheet1_1     | (αν επεξεργαστείτε άλλο DataTable με το ίδιο όνομα) |

Η λογική μετονομασίας φύλλων εξασφαλίζει **δημιουργία πολλαπλών φύλλων Excel** χωρίς χειροκίνητη διαχείριση ονομάτων.

## Συνηθισμένες παραλλαγές και ειδικές περιπτώσεις

| Κατάσταση | Πώς να το αντιμετωπίσετε |
|-----------|--------------------------|
| **Πολύ μεγάλοι πίνακες** (≥ 100 000 γραμμές) | Χρησιμοποιήστε `WorkbookSettings.MemorySetting = MemorySetting.MemoryOptimized` πριν την επεξεργασία για χαμηλή χρήση μνήμης. |
| **Προσαρμοσμένη σειρά στηλών** | Αναδιατάξτε τα αντικείμενα `DataColumn` στο `DataTable` πριν καλέσετε `ProcessSmartMarkers`. |
| **Πολλαπλά DataTables με διαφορετικά ονόματα** | Καλέστε `ProcessSmartMarkers` για κάθε πίνακα· το Aspose.Cells θα δημιουργήσει αυτόματα ξεχωριστό φύλλο για κάθε όνομα. |
| **Απαιτείται γραμμή κεφαλίδας με στυλ** | Μετά την επεξεργασία, προσπελάστε `Worksheet.Cells["A1"]` και εφαρμόστε ιδιότητες `Style` (γραμματοσειρά, φόντο). |
| **Αποθήκευση σε ροή αντί για αρχείο** | Αντικαταστήστε `workbook.Save(outputPath, SaveFormat.Xlsx)` με `workbook.Save(stream, SaveFormat.Xlsx)`. |

**Pro tip:** Πάντα τυλίξτε τις λειτουργίες συστήματος αρχείων σε μπλοκ `try…catch` για να εντοπίζετε γρήγορα προβλήματα δικαιωμάτων.

## Πλήρης κώδικας (έτοιμος για αντιγραφή)

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create the DataTable that will be exported
        DataTable dataTable = new DataTable("Sheet1");
        dataTable.Columns.Add("Id", typeof(int));

        // Add rows – you can replace this with your own data source
        dataTable.Rows.Add(1);
        dataTable.Rows.Add(2);
        int[] extraIds = { 3, 4, 5 };
        foreach (int id in extraIds)
        {
            dataTable.Rows.Add(id);
        }

        // Process SmartMarkers and save the workbook
        ProcessAndSaveWorkbook(dataTable);
    }

    private static void ProcessAndSaveWorkbook(DataTable dataTable)
    {
        // Configure SmartMarkerOptions to rename duplicate sheets automatically
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
        {
            DetailSheetNewName = "Sheet1_{0}"
        };

        // Create a new workbook and populate it from the DataTable
        Workbook workbook = new Workbook();
        workbook.ProcessSmartMarkers(dataTable, smartMarkerOptions);

        // Save the workbook as an .xlsx file
        string outputPath = @"YOUR_DIRECTORY\DuplicateSheets.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

### Αναμενόμενη έξοδος

Η εκτέλεση του προγράμματος εμφανίζει:

```
Workbook saved to YOUR_DIRECTORY\DuplicateSheets.xlsx
```

Ανοίγοντας το `DuplicateSheets.xlsx` βλέπετε ένα φύλλο με όνομα **Sheet1** που περιέχει τη στήλη `Id` με τις τιμές `1, 2, 3, 4, 5`. Αν αργότερα επεξεργαστείτε άλλο `DataTable` με όνομα `"Sheet1"` στο ίδιο βιβλίο εργασίας, το Aspose.Cells θα δημιουργήσει αυτόματα **Sheet1_1**, **Sheet1_2**, κ.λπ.

## Συμπέρασμα

Τώρα ξέρετε πώς να **δημιουργήσετε φύλλο Excel** από ένα `DataTable` σε C#, **εξάγετε datatable σε excel**, **προσθέσετε γραμμές σε datatable**, να δημιουργήσετε **πολλαπλά φύλλα Excel** με αυτόματη ονομασία, και να **αποθηκεύσετε το βιβλίο εργασίας ως xlsx**. Το πλήρες, εκτελέσιμο παράδειγμα δείχνει τη ροή από άκρη σε άκρη και παρέχει πρακτικές συμβουλές για μεγάλα σύνολα δεδομένων και προσαρμοσμένο στυλ.

### Τι θα ακολουθήσει;

* Εξερευνήστε **μορφοποίηση κελιών** (γραμματοσειρές, χρώματα, περιγράμματα) προσπελάζοντας `Worksheet.Cells` μετά το `ProcessSmartMarkers`.  
* Χρησιμοποιήστε **βρόχους SmartMarker** για δημιουργία αναφορών master‑detail σε ένα μόνο βιβλίο εργασίας.  
* Μεταβείτε σε **εξαγωγή CSV** αλλάζοντας σε `SaveFormat.Csv` αν χρειάζεστε απλό κείμενο.  

Αισθανθείτε ελεύθεροι να προσαρμόσετε τον κώδικα στις δικές σας πηγές δεδομένων—είτε είναι ερώτημα βάσης, απόκριση API ή συλλογή στη μνήμη. Καλή προγραμματιστική!

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να κατακτήσετε επιπλέον δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στην υλοποίηση.

- [How to Create and Save an Excel Workbook as ODS Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [How to Create and Save an Excel Workbook as SVG using Aspose.Cells for Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [How to Create and Export Excel to HTML Using Aspose.Cells Java | Workbook Operations Guide](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}