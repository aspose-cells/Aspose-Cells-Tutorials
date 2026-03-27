---
category: general
date: 2026-03-27
description: Δημιουργήστε βιβλίο εργασίας Excel με C# και Aspose.Cells, εφαρμόστε
  μορφοποίηση υπό όρους, εισάγετε DataTable στο Excel και αποθηκεύστε το βιβλίο εργασίας
  ως xlsx—όλα σε ένα σεμινάριο.
draft: false
keywords:
- create excel workbook c#
- apply conditional formatting
- import datatable to excel
- save workbook as xlsx
- create excel file programmatically
language: el
og_description: Δημιουργήστε βιβλίο εργασίας Excel με C# χρησιμοποιώντας το Aspose.Cells,
  εφαρμόστε μορφοποίηση υπό όρους, εισάγετε datatable στο Excel και αποθηκεύστε το
  βιβλίο εργασίας ως xlsx σε λίγα λεπτά.
og_title: Δημιουργία βιβλίου εργασίας Excel C# – Πλήρης οδηγός με μορφοποίηση υπό
  όρους
tags:
- Aspose.Cells
- C#
- Excel automation
title: Δημιουργία βιβλίου εργασίας Excel C# – Οδηγός βήμα‑προς‑βήμα με μορφοποίηση
  υπό όρους
url: /el/net/excel-conditional-formatting/create-excel-workbook-c-step-by-step-guide-with-conditional/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία Excel Workbook C# – Πλήρη Εκπαιδευτική Οδηγία

Κάποτε χρειάστηκε να **create excel workbook c#** επί τόπου αλλά δεν ήξερες από πού να ξεκινήσεις; Δεν είσαι μόνος σου—πολλοί προγραμματιστές συναντούν αυτό το εμπόδιο όταν αυτοματοποιούν πρώτα τις αναφορές τους. Σε αυτόν τον οδηγό θα σου δείξουμε ακριβώς πώς να δημιουργήσεις excel workbook c# με Aspose.Cells, να εφαρμόσεις conditional formatting, να εισάγεις datatable to excel και τελικά να αποθηκεύσεις το workbook ως xlsx.  

Αυτό που θα πάρεις από αυτό το tutorial είναι μια έτοιμη προς εκτέλεση console εφαρμογή που παράγει ένα πολύχρωμο αρχείο Excel, μαζί με μια σαφή εξήγηση κάθε γραμμής ώστε να το προσαρμόσεις στα δικά σου έργα. Δεν χρειάζονται εξωτερικά έγγραφα· απλώς αντιγράψτε, επικολλήστε και τρέξτε.  

### Προαπαιτούμενα

- .NET 6+ (ή .NET Framework 4.7.2+) εγκατεστημένο  
- Visual Studio 2022 ή οποιοσδήποτε επεξεργαστής C# προτιμάς  
- Aspose.Cells for .NET (μπορείς να πάρεις το δωρεάν trial πακέτο NuGet)  

Αν τα έχεις, ας βουτήξουμε.

## Create Excel Workbook C# – Αρχικοποίηση του Workbook

Το πρώτο που πρέπει να κάνεις είναι **create excel workbook c#** δημιουργώντας ένα αντικείμενο της κλάσης `Workbook`. Αυτό το αντικείμενο αντιπροσωπεύει ολόκληρο το αρχείο Excel στη μνήμη.

```csharp
using Aspose.Cells;
using Aspose.Cells.Tables;
using System.Data;
using System.Drawing;

class SmartMarkerConditionalDemo
{
    static void Main()
    {
        // Step 1: Create a new workbook and grab the first worksheet
        Workbook workbook = new Workbook();                // <-- creates the workbook
        Worksheet worksheet = workbook.Worksheets[0];      // first sheet (Sheet1)
```

> **Γιατί είναι σημαντικό:** Η κλάση `Workbook` αφαιρεί την ανάγκη να ασχοληθείς με χαμηλού επιπέδου XML ή COM interop. Σου δίνει επίσης πρόσβαση σε στυλ, πίνακες και smart markers αμέσως.

## Εφαρμογή Conditional Formatting

Τώρα που υπάρχει το workbook, ας **apply conditional formatting** για να επισημάνουμε τις γραμμές όπου η ποσότητα υπερβαίνει το 100. Το conditional formatting ανήκει στο worksheet, όχι στο κελί, κάτι που το κάνει επαναχρησιμοποιήσιμο.

```csharp
        // Step 4: Apply conditional formatting to highlight quantities > 100
        int cfIndex = worksheet.ConditionalFormattings.Add();               // add a new CF collection
        var conditionalFormatting = worksheet.ConditionalFormattings[cfIndex];
        var condition = conditionalFormatting.AddCondition(
            FormatConditionType.CellValue, OperatorType.Greater, "100");   // > 100

        // Define the style that will be applied when the condition is true
        condition.Style = workbook.CreateStyle();
        condition.Style.Font.Color = Color.Red;               // red font
        condition.Style.Pattern = BackgroundType.Solid;       // solid background
        condition.Style.ForegroundColor = Color.Yellow;      // yellow fill
```

> **Pro tip:** Αν χρειάζεσαι πιο σύνθετους κανόνες (π.χ. μεταξύ δύο τιμών), απλώς κάλεσε ξανά το `AddCondition` με `OperatorType.Between`.

## Γράψιμο Headers και Smart Markers

Πριν **import datatable to excel**, χρειαζόμαστε κελιά‑placeholder—smart markers—που η βιβλιοθήκη θα αντικαταστήσει με πραγματικά δεδομένα. Σκέψου τα σαν ετικέτες προτύπου.

```csharp
        // Step 2: Write the header row
        worksheet.Cells["A1"].PutValue("Product");
        worksheet.Cells["B1"].PutValue("Quantity");
        worksheet.Cells["C1"].PutValue("Status");

        // Step 3: Define smart markers that will be replaced by data
        worksheet.Cells["A2"].PutValue("&=Products.ProductName");
        worksheet.Cells["B2"].PutValue("&=Products.Quantity");
        worksheet.Cells["C2"].PutValue("&=Products.Quantity > 100 ? \"High\" : \"Low\"");
```

> **Γιατί smart markers;** Σου επιτρέπουν να κρατάς το layout του Excel ξεχωριστό από τον κώδικα. Σχεδιάζεις το φύλλο μία φορά, τροφοδοτείς ένα `DataTable` και η βιβλιοθήκη κάνει τα υπόλοιπα.

## Εισαγωγή DataTable στο Excel

Αυτή είναι η ουσία του **import datatable to excel**. Δημιουργούμε ένα `DataTable` που αντικατοπτρίζει τα πεδία των smart markers και το περνάμε στο `ImportDataTable`.

```csharp
        // Step 5: Build a simple DataTable that matches the smart marker fields
        DataTable products = new DataTable();
        products.Columns.Add("ProductName");
        products.Columns.Add("Quantity", typeof(int));
        products.Rows.Add("Apple", 120);
        products.Rows.Add("Banana", 80);
        products.Rows.Add("Cherry", 150);

        // Step 6: Populate the worksheet with the DataTable via smart markers
        worksheet.Cells.ImportDataTable(products, true, "A2");
```

> **Edge case:** Αν ο πίνακάς σου έχει περισσότερες στήλες από ό,τι χρειάζεσαι, απλώς παραλείπεις τις επιπλέον στήλες στα smart markers· θα αγνοηθούν.

## Αποθήκευση Workbook ως XLSX

Τέλος, **save workbook as xlsx** στο δίσκο. Η μέθοδος `Save` καθορίζει αυτόματα τη μορφή από την επέκταση του αρχείου.

```csharp
        // Step 7: Save the result to an Excel file
        workbook.Save("SmartMarkersConditional.xlsx");   // <-- saves as .xlsx
    }
}
```

Αυτό είναι ολόκληρο το πρόγραμμα. Όταν το τρέξεις, θα δεις ένα αρχείο με όνομα `SmartMarkersConditional.xlsx` στον φάκελο εξόδου.

### Αναμενόμενη Έξοδος

| Product | Quantity | Status |
|---------|----------|--------|
| Apple   | 120      | High   |
| Banana  | 80       | Low    |
| Cherry  | 150      | High   |

Οι γραμμές με **Quantity > 100** (Apple και Cherry) θα έχουν κόκκινο κείμενο σε κίτρινο φόντο χάρη στο conditional formatting που προσθέσαμε νωρίτερα.

## Create Excel File Programmatically – Πλήρης Λίστα Πηγαίου Κώδικα

Παρακάτω βρίσκεται ο πλήρης, έτοιμος για αντιγραφή κώδικας. Περιλαμβάνει κάθε κομμάτι που συζητήσαμε, συν λίγα επιπλέον σχόλια για σαφήνεια.

```csharp
using Aspose.Cells;
using Aspose.Cells.Tables;
using System.Data;
using System.Drawing;

class SmartMarkerConditionalDemo
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Write header cells
        worksheet.Cells["A1"].PutValue("Product");
        worksheet.Cells["B1"].PutValue("Quantity");
        worksheet.Cells["C1"].PutValue("Status");

        // 3️⃣ Insert smart markers – placeholders for our data
        worksheet.Cells["A2"].PutValue("&=Products.ProductName");
        worksheet.Cells["B2"].PutValue("&=Products.Quantity");
        worksheet.Cells["C2"].PutValue("&=Products.Quantity > 100 ? \"High\" : \"Low\"");

        // 4️⃣ Apply conditional formatting (highlight >100)
        int cfIdx = worksheet.ConditionalFormattings.Add();
        var cf = worksheet.ConditionalFormattings[cfIdx];
        var cond = cf.AddCondition(FormatConditionType.CellValue, OperatorType.Greater, "100");
        cond.Style = workbook.CreateStyle();
        cond.Style.Font.Color = Color.Red;
        cond.Style.Pattern = BackgroundType.Solid;
        cond.Style.ForegroundColor = Color.Yellow;

        // 5️⃣ Build a DataTable that matches the markers
        DataTable products = new DataTable();
        products.Columns.Add("ProductName");
        products.Columns.Add("Quantity", typeof(int));
        products.Rows.Add("Apple", 120);
        products.Rows.Add("Banana", 80);
        products.Rows.Add("Cherry", 150);

        // 6️⃣ Import the DataTable – this replaces the smart markers
        worksheet.Cells.ImportDataTable(products, true, "A2");

        // 7️⃣ Save the workbook – this will create an .xlsx file
        workbook.Save("SmartMarkersConditional.xlsx");
    }
}
```

> **Tip:** Αν χρειάζεται να δημιουργήσεις πολλαπλά φύλλα, απλώς επανάλαβε τα βήματα 2‑6 σε ένα νέο αντικείμενο `Worksheet` που παίρνεις μέσω `workbook.Worksheets.Add()`.

## Γιατί να Χρησιμοποιήσεις Aspose.Cells για C# Excel Automation;

- **Performance:** Λειτουργεί εξ ολοκλήρου στη μνήμη, χωρίς COM interop, οπότε είναι γρήγορο ακόμη και με μεγάλα σύνολα δεδομένων.  
- **Feature‑rich:** Υποστηρίζει smart markers, conditional formatting, charts, pivot tables και πολλά άλλα.  
- **Cross‑platform:** Λειτουργεί σε Windows, Linux και macOS με .NET Core/5/6+.  

Αν κολλήσεις σε κάποια λειτουργία—π.χ. προσθήκη chart ή προστασία φύλλου—απλώς ψάξε “asp​ose.cells add chart c#” και θα βρεις παρόμοιο παράδειγμα.

## Επόμενα Βήματα & Σχετικά Θέματα

- **Export to PDF:** Αφού **create excel workbook c#**, μπορείς αμέσως να εξάγεις σε PDF με `workbook.Save("output.pdf")`.  
- **Read existing Excel files:** Χρησιμοποίησε `new Workbook("ExistingFile.xlsx")` για να τροποποιήσεις ένα πρότυπο.  
- **Bulk import:** Για τεράστιες ποσότητες δεδομένων, σκέψου `ImportArray` ή `ImportDataTable` με `ImportOptions` για βελτιωμένη ταχύτητα.  

Πειραματίσου με διαφορετικούς κανόνες conditional, χρώματα ή ακόμα και πρόσθεσε μια γραμμή σύνοψης με τύπους. Ο ουρανός είναι το όριο όταν **create excel file programmatically**.

---

*Έτοιμος να το δοκιμάσεις μόνος σου; Πάρε τον κώδικα, τρέξ' τον και άνοιξε το παραγόμενο `SmartMarkersConditional.xlsx`. Αν συναντήσεις προβλήματα, άφησε ένα σχόλιο παρακάτω—καλή προγραμματιστική!*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}