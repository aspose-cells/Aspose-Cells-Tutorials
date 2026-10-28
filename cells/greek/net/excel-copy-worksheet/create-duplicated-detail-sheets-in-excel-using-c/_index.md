---
category: general
date: 2026-10-07
description: Δημιουργήστε διπλότυπα φύλλα λεπτομερειών στο Excel χρησιμοποιώντας C#.
  Μάθετε πώς να δημιουργείτε πολλαπλά φύλλα εργασίας και να συνθέτετε μια αναφορά
  από πίνακες σε μία μόνο εκτέλεση.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create duplicated detail sheets
- how to generate multiple worksheets
- generate excel report from tables
language: el
lastmod: 2026-10-07
og_description: Δημιουργήστε διπλότυπα φύλλα λεπτομερειών στο Excel με C#. Αυτό το
  σεμινάριο δείχνει πώς να δημιουργήσετε πολλαπλά φύλλα εργασίας και να παράγετε μια
  πλήρη αναφορά Excel από πίνακες.
og_image_alt: Screenshot of an Excel file that has create duplicated detail sheets
  output
og_title: Δημιουργία αντιγραφών φύλλων λεπτομερειών στο Excel – βήμα‑βήμα οδηγός C#
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Create duplicated detail sheets in Excel using C#. Learn how to generate
    multiple worksheets and build a report from tables in a single run.
  headline: Create duplicated detail sheets in Excel using C#
  type: TechArticle
- description: Create duplicated detail sheets in Excel using C#. Learn how to generate
    multiple worksheets and build a report from tables in a single run.
  name: Create duplicated detail sheets in Excel using C#
  steps:
  - name: '**Obtain the data source** that contains a master table and two detail
      tables.'
    text: '**Obtain the data source** that contains a master table and two detail
      tables.'
  - name: '**Configure the Smart‑marker processor** so each duplicated detail sheet
      receives a unique name.'
    text: '**Configure the Smart‑marker processor** so each duplicated detail sheet
      receives a unique name.'
  - name: '**Create a new workbook** and place a smart‑marker that references the
      master table.'
    text: '**Create a new workbook** and place a smart‑marker that references the
      master table.'
  - name: '**Run the processor** to generate the master sheet and all detail sheets.'
    text: '**Run the processor** to generate the master sheet and all detail sheets.'
  - name: '**Save the workbook** – each detail sheet now has a distinct name.'
    text: '**Save the workbook** – each detail sheet now has a distinct name.'
  type: HowTo
tags:
- C#
- Excel automation
- Aspose.Cells
title: Δημιουργία αντιγραμμένων φύλλων λεπτομερειών στο Excel με χρήση C#
url: /el/net/excel-copy-worksheet/create-duplicated-detail-sheets-in-excel-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία διπλών φύλλων λεπτομερειών στο Excel με C#

Αν χρειάζεστε **να δημιουργήσετε διπλά φύλλα λεπτομερειών** σε ένα βιβλίο εργασίας του Excel, αυτός ο οδηγός σας καθοδηγεί βήμα προς βήμα στη διαδικασία. Θα δείτε πώς να **δημιουργήσετε πολλαπλά φύλλα εργασίας** από ένα σύνολο δεδομένων master‑detail και να παράγετε μια επαγγελματική αναφορά Excel απευθείας από πίνακες.

Η δημιουργία αναφοράς Excel από πίνακες είναι κοινή απαίτηση για συστήματα τιμολόγησης, πίνακες ελέγχου αποθεμάτων ή οποιοδήποτε σενάριο όπου μια κύρια εγγραφή έχει πολλές σχετικές γραμμές λεπτομερειών. Στο τέλος αυτού του σεμιναρίου θα έχετε ένα εκτελέσιμο πρόγραμμα C# που δημιουργεί ένα βιβλίο εργασίας με ένα κύριο φύλλο και ένα μοναδικά ονομασμένο φύλλο για κάθε ομάδα λεπτομερειών.

## Προαπαιτούμενα

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

* .NET 6.0 (ή νεότερο) εγκατεστημένο  
* Visual Studio 2022 ή οποιοδήποτε IDE συμβατό με C#  
* Το **Aspose.Cells for .NET** πακέτο NuGet (παρέχει `SmartMarkerProcessor`)  

Μπορείτε να προσθέσετε το πακέτο με την ακόλουθη εντολή:

```bash
dotnet add package Aspose.Cells
```

## Επισκόπηση της λύσης

Η λύση ακολουθεί τα πέντε αυτά βήματα:

1. **Απόκτηση της πηγής δεδομένων** που περιέχει έναν πίνακα master και δύο πίνακες detail.  
2. **Διαμόρφωση του Smart‑marker processor** ώστε κάθε διπλό φύλλο λεπτομερειών να λαμβάνει μοναδικό όνομα.  
3. **Δημιουργία νέου βιβλίου εργασίας** και τοποθέτηση smart‑marker που αναφέρεται στον πίνακα master.  
4. **Εκτέλεση του processor** για τη δημιουργία του κύριου φύλλου και όλων των φύλλων λεπτομερειών.  
5. **Αποθήκευση του βιβλίου εργασίας** – κάθε φύλλο λεπτομερειών τώρα έχει διακριτό όνομα.

Κάθε βήμα εξηγείται λεπτομερώς παρακάτω, με πλήρη κώδικα και αιτιολόγηση.

## Βήμα 1: Απόκτηση της πηγής δεδομένων που περιέχει έναν πίνακα master και δύο πίνακες detail

Η πρώτη εργασία είναι η δημιουργία ενός `DataSet` που μιμείται τα δεδομένα που θα αντλούσατε κανονικά από μια βάση δεδομένων. Το `DataSet` πρέπει να περιέχει έναν πίνακα με όνομα **Master** και έναν ή περισσότερους πίνακες με όνομα **Detail**. Η μηχανή Smart‑marker χρησιμοποιεί αυτά τα ονόματα πινάκων για να γεμίσει το βιβλίο εργασίας.

```csharp
using System.Data;

/// <summary>
/// Returns a DataSet with a master table and two detail tables.
/// In a real application you would fill these tables from a database.
/// </summary>
static DataSet GetReportDataSet()
{
    var ds = new DataSet();

    // Master table – one row per invoice
    var master = new DataTable("Master");
    master.Columns.Add("InvoiceId", typeof(int));
    master.Columns.Add("CustomerName", typeof(string));
    master.Columns.Add("InvoiceDate", typeof(DateTime));
    master.Rows.Add(101, "Acme Corp", new DateTime(2024, 12, 01));
    master.Rows.Add(102, "Beta Ltd.", new DateTime(2024, 12, 03));
    ds.Tables.Add(master);

    // Detail table – multiple rows per invoice
    var detail = new DataTable("Detail");
    detail.Columns.Add("InvoiceId", typeof(int));
    detail.Columns.Add("Product", typeof(string));
    detail.Columns.Add("Quantity", typeof(int));
    detail.Columns.Add("Price", typeof(decimal));

    // Detail rows for Invoice 101
    detail.Rows.Add(101, "Widget A", 5, 9.99m);
    detail.Rows.Add(101, "Widget B", 2, 19.95m);

    // Detail rows for Invoice 102
    detail.Rows.Add(102, "Gadget X", 1, 99.00m);
    detail.Rows.Add(102, "Gadget Y", 3, 49.50m);
    ds.Tables.Add(detail);

    return ds;
}
```

**Γιατί είναι σημαντικό:**  
*Smart‑marker* λειτουργεί με αντικείμενα `DataSet`; κάθε όνομα πίνακα γίνεται ένας marker που η μηχανή μπορεί να αντικαταστήσει. Με τη δομή αυτή ενεργοποιείτε τον επεξεργαστή να δημιουργεί αυτόματα το αντίγραφο του φύλλου λεπτομερειών για κάθε διακριτό `InvoiceId`.

## Βήμα 2: Διαμόρφωση του Smart‑marker processor ώστε κάθε διπλό φύλλο λεπτομερειών να έχει μοναδικό όνομα

Όταν ο επεξεργαστής εντοπίζει έναν marker detail, δημιουργεί ένα νέο φύλλο εργασίας για κάθε ομάδα γραμμών. Από προεπιλογή τα νέα φύλλα έχουν το ίδιο όνομα, κάτι που προκαλεί σύγκρουση ονομάτων. Ορίζοντας το `DetailSheetNewName` λέτε στη μηχανή πώς να μετονομάσει κάθε αντίγραφο.

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

/// <summary>
/// Configures the SmartMarkerProcessor to rename duplicated detail sheets.
/// The placeholder {0} is replaced with a sequential number (1, 2, …).
/// </summary>
static SmartMarkerProcessor ConfigureProcessor()
{
    var processor = new SmartMarkerProcessor();

    // The pattern "Detail_{0}" becomes Detail_1, Detail_2, …
    processor.Options.DetailSheetNewName = "Detail_{0}";

    // Optional: keep the original sheet as a template (if you have one)
    processor.Options.KeepTemplateSheet = false;

    return processor;
}
```

**Γιατί είναι σημαντικό:**  
Χωρίς ένα μοναδικό μοτίβο ονοματοδοσίας, το βιβλίο εργασίας θα πετάξει εξαίρεση όταν ο επεξεργαστής προσπαθήσει να προσθέσει δεύτερο φύλλο λεπτομερειών. Ο δείκτης `{0}` εξασφαλίζει ότι κάθε φύλλο λαμβάνει ένα διακριτό, προβλέψιμο όνομα.

## Βήμα 3: Δημιουργία νέου βιβλίου εργασίας και τοποθέτηση smart‑marker που αναφέρεται στον πίνακα master

Τώρα δημιουργείτε ένα νέο `Workbook`, προσθέτετε έναν marker που δείχνει στον πίνακα **Master**, και προαιρετικά μορφοποιείτε τη γραμμή κεφαλίδας.

```csharp
/// <summary>
/// Creates a workbook with a single cell that contains the master smart‑marker.
/// </summary>
static Workbook CreateTemplateWorkbook()
{
    var workbook = new Workbook();
    var sheet = workbook.Worksheets[0];

    // Put the master smart‑marker in cell A1.
    // The double braces {{ }} tell SmartMarker to replace the content with the Master table.
    sheet.Cells["A1"].PutValue("{{Master}}");

    // Optional: add a header row for visual clarity.
    sheet.Cells["A2"].PutValue("Invoice ID");
    sheet.Cells["B2"].PutValue("Customer");
    sheet.Cells["C2"].PutValue("Date");
    sheet.Cells["A2:C2"].Style.Font.IsBold = true;

    return workbook;
}
```

**Γιατί είναι σημαντικό:**  
Ο marker `{{Master}}` υποδεικνύει στον επεξεργαστή να επεκτείνει τον πίνακα master ξεκινώντας από το `A1`. Οι επόμενες γραμμές γίνονται οι γραμμές δεδομένων για κάθε εγγραφή master. Αυτό είναι το σημείο εισόδου για **generate excel report from tables**.

## Βήμα 4: Εκτέλεση του smart‑marker processor για τη δημιουργία του κύριου φύλλου και των φύλλων λεπτομερειών

Με την πηγή δεδομένων, τον επεξεργαστή και το πρότυπο έτοιμα, καλείτε το `Process`. Η μηχανή επεκτείνει τον marker master, έπειτα δημιουργεί ξεχωριστό φύλλο λεπτομερειών για κάθε διακριτό `InvoiceId`.

```csharp
static void GenerateReport()
{
    // 1️⃣ Obtain data
    DataSet reportData = GetReportDataSet();

    // 2️⃣ Configure processor
    SmartMarkerProcessor processor = ConfigureProcessor();

    // 3️⃣ Create template workbook
    Workbook workbook = CreateTemplateWorkbook();

    // 4️⃣ Process the smart‑markers – this creates the master sheet and duplicated detail sheets
    processor.Process(workbook, reportData);

    // 5️⃣ Save the file
    string outputPath = Path.Combine(
        Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
        "DuplicatedDetailSheets.xlsx");
    workbook.Save(outputPath);

    Console.WriteLine($"Report generated successfully: {outputPath}");
}
```

**Γιατί είναι σημαντικό:**  
`processor.Process` εκτελεί το βαριά έργο: διαβάζει τις γραμμές master, δημιουργεί ένα φύλλο λεπτομερειών για κάθε μοναδικό κλειδί και μετονομάζει αυτά τα φύλλα σύμφωνα με το μοτίβο που ορίστηκε νωρίτερα. Το αποτέλεσμα είναι ένα βιβλίο εργασίας που ικανοποιεί την απαίτηση **how to generate multiple worksheets**.

## Βήμα 5: Αποθήκευση του παραγόμενου βιβλίου εργασίας – κάθε φύλλο λεπτομερειών τώρα έχει διακριτό όνομα

Η κλήση `Save` γράφει το αρχείο στο δίσκο. Όταν ανοίξετε το βιβλίο εργασίας, θα δείτε:

* **Sheet1** – το κύριο φύλλο που περιέχει τις κεφαλίδες τιμολογίων.  
* **Detail_1**, **Detail_2**, … – κάθε φύλλο περιέχει τις γραμμές από τον πίνακα **Detail** που ανήκουν σε συγκεκριμένο τιμολόγιο.

Παρακάτω υπάρχει ένα mock‑up της αναμενόμενης διάταξης του βιβλίου (η εικόνα είναι εικονογραφική· μπορείτε να την αντικαταστήσετε με πραγματικό στιγμιότυπο εάν το επιθυμείτε).

![Screenshot of an Excel file that has create duplicated detail sheets output](https://example.com/images/duplicated-detail-sheets.png)

### Αναμενόμενο αποτέλεσμα

| Όνομα φύλλου | Περιγραφή περιεχομένου |
|--------------|------------------------|
| **Sheet1**   | Γραμμές Master: InvoiceId, CustomerName, InvoiceDate |
| **Detail_1** | Γραμμές Detail όπου `InvoiceId = 101` |
| **Detail_2** | Γραμμές Detail όπου `InvoiceId = 102` |

Το άνοιγμα του `DuplicatedDetailSheets.xlsx` θα πρέπει να εμφανίζει ακριβώς αυτή τη δομή.

## Πλήρης κώδικας (έτοιμος για αντιγραφή)

```csharp
using System;
using System.Data;
using System.IO;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace ExcelDetailSheetsDemo
{
    class Program
    {
        static void Main()
        {
            GenerateReport();
        }

        // ------------------------------------------------------------
        // Step 1 – data source
        // ------------------------------------------------------------
        static DataSet GetReportDataSet()
        {
            var ds = new DataSet();

            var master = new DataTable("Master");
            master.Columns.Add("InvoiceId", typeof(int));
            master.Columns.Add("CustomerName", typeof(string));
            master.Columns.Add("InvoiceDate", typeof(DateTime));
            master.Rows.Add(101, "Acme Corp", new DateTime(2024, 12, 01));
            master.Rows.Add(102, "Beta Ltd.", new DateTime(2024, 12, 03));
            ds.Tables.Add(master);

            var detail = new DataTable("Detail");
            detail.Columns.Add("InvoiceId", typeof(int));
            detail.Columns.Add("Product", typeof(string));
            detail.Columns.Add("Quantity", typeof(int));
            detail.Columns.Add("Price", typeof(decimal));
            detail.Rows.Add(101, "Widget A", 5, 9.99m);
            detail.Rows.Add(101, "Widget B", 2, 19.95m);
            detail.Rows.Add(102, "Gadget X", 1, 99.00m);
            detail.Rows.Add(102, "Gadget Y", 3, 49.50m);
            ds.Tables.Add(detail);

            return ds;
        }

        // ------------------------------------------------------------
        // Step 2 – processor configuration
        // ------------------------------------------------------------
        static SmartMarkerProcessor ConfigureProcessor()
        {
            var processor = new SmartMarkerProcessor();
            processor.Options.DetailSheetNewName = "Detail_{0}";
            processor.Options.KeepTemplate


## Τι Θα Μάθετε Στη Σειρά;

Οι παρακάτω οδηγοί καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στην υλοποίηση των δικών σας έργων.

- [How to Name Sheets Automatically – Generate Multiple Sheets in C#](/cells/english/net/smart-markers-dynamic-data/how-to-name-sheets-automatically-generate-multiple-sheets-in/)
- [How to Create Worksheets – Step‑by‑Step Guide for Dynamic Excel Generation](/cells/english/net/worksheet-operations/how-to-create-worksheets-step-by-step-guide-for-dynamic-exce/)
- [How to Generate Excel Report in C# – Full Guide Using SmartMarker](/cells/english/net/smart-markers-dynamic-data/how-to-generate-excel-report-in-c-full-guide-using-smartmark/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}