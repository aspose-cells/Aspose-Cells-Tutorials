---
category: general
date: 2026-06-27
description: Πώς να μορφοποιήσετε στήλες Excel σε C# με εναλλασσόμενα χρώματα. Μάθετε
  να δημιουργείτε βιβλίο εργασίας Excel με C#, να εισάγετε DataTable στο Excel και
  να εξάγετε ως .xlsx.
draft: false
keywords:
- how to format excel columns
- create excel workbook c#
- import datatable to excel
- apply alternating column colors
- export datatable as xlsx
language: el
og_description: Πώς να μορφοποιήσετε στήλες Excel σε C# με εναλλασσόμενα χρώματα.
  Ακολουθήστε αυτόν τον βήμα‑βήμα οδηγό για να δημιουργήσετε ένα βιβλίο εργασίας Excel
  σε C#, να εισάγετε DataTable και να εξάγετε ως .xlsx.
og_title: Πώς να μορφοποιήσετε στήλες Excel σε C# – Πλήρης οδηγός
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: How to format Excel columns in C# with alternating colors. Learn to
    create Excel workbook C#, import DataTable to Excel, and export as .xlsx.
  headline: How to Format Excel Columns in C# – Complete Guide
  type: TechArticle
tags:
- C#
- Excel
- DataTable
title: Πώς να μορφοποιήσετε στήλες Excel σε C# – Πλήρης οδηγός
url: /el/net/formatting-rows-and-columns-in-excel/how-to-format-excel-columns-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να μορφοποιήσετε στήλες Excel σε C# – Πλήρης Οδηγός

Έχετε αναρωτηθεί ποτέ **πώς να μορφοποιήσετε στήλες Excel** σε C# χωρίς να τρελαίνεστε; Δεν είστε οι μόνοι. Είτε εκτυπώνετε μια αναφορά πωλήσεων είτε αποθηκεύετε ένα dump βάσης δεδομένων σε ένα φύλλο, η σωστή μορφοποίηση των στηλών μπορεί να κάνει τη διαφορά μεταξύ “meh” και “wow”.

Σε αυτό το tutorial θα περάσουμε από ένα **πλήρες, εκτελέσιμο παράδειγμα** που δείχνει πώς να **δημιουργήσετε Excel workbook C#**, **εισάγετε DataTable σε Excel**, και **εφαρμόσετε εναλλασσόμενα χρώματα στηλών** ώστε κάθε στήλη να ξεχωρίζει. Στο τέλος θα ξέρετε επίσης πώς να **εξάγετε DataTable ως xlsx** με μία μόνο γραμμή κώδικα. Χωρίς περιττές πληροφορίες, μόνο πρακτικός κώδικας που μπορείτε να αντιγράψετε‑και‑επικολλήσετε.

> **Τι θα χρειαστείτε**  
> - .NET 6 ή νεότερη (οποιαδήποτε πρόσφατη έκδοση λειτουργεί)  
> - Το πακέτο NuGet **Aspose.Cells** (ή κάποιο παρόμοιο) – θα το χρησιμοποιήσουμε επειδή είναι καθαρό C# και δεν απαιτεί εγκατεστημένο Excel.  
> - Μια απλή πηγή `DataTable` – θα δημιουργήσουμε μία επί τόπου για σκοπούς επίδειξης.

Ας βουτήξουμε.

![How to format Excel columns in C# example](excel-columns.png "How to format Excel columns in C#")

## Βήμα 1: Δημιουργία Excel Workbook σε C#  

Το πρώτο που πρέπει να κάνετε είναι να δημιουργήσετε ένα νέο workbook. Σκεφτείτε το σαν ένα ολοκαίνουργιο σημειωματάριο όπου θα γράψετε τα δεδομένα σας.

```csharp
using Aspose.Cells;
using System;
using System.Data;
using System.Drawing;

class ExcelDemo
{
    static void Main()
    {
        // 1️⃣ Create a new workbook – this is the container for all sheets.
        Workbook workbook = new Workbook();

        // 2️⃣ Grab the first worksheet (index 0) – it’s already there.
        Worksheet worksheet = workbook.Worksheets[0];

        // The rest of the steps will fill this sheet with data and styling.
        // …
    }
}
```

**Γιατί είναι σημαντικό:** `Workbook` είναι το σημείο εισόδου για κάθε λειτουργία Excel. Η δημιουργία του **creates excel workbook c#** – δεν χρειάζεται κανένα COM interop, και το αντικείμενο ζει εξ ολοκλήρου στη μνήμη μέχρι να αποφασίσετε να το αποθηκεύσετε.

> **Pro tip:** Αν στοχεύετε σε περιβάλλον server, προτιμήστε μια βιβλιοθήκη που δεν εξαρτάται από την εγκατάσταση του Microsoft Office. Aspose.Cells, EPPlus ή ClosedXML καλύπτουν αυτήν την ανάγκη.

## Βήμα 2: Προετοιμασία Στυλ – Εφαρμογή Εναλλασσόμενων Χρωμάτων Στηλών  

Τώρα έρχεται το διασκεδαστικό μέρος: να κάνετε κάθε δεύτερη στήλη διαφορετικού χρώματος. Αυτό το οπτικό cue βοηθά τους αναγνώστες να διαβάζουν μεγάλους πίνακες πιο γρήγορα.

```csharp
// Assume we already have a DataTable called dataTable (we’ll create it later).
int columnCount = dataTable.Columns.Count;

// Create an array to hold a style per column.
Style[] columnStyles = new Style[columnCount];

for (int i = 0; i < columnCount; i++)
{
    // Each column gets its own Style object.
    columnStyles[i] = workbook.CreateStyle();

    // Alternate between blue and green fonts.
    columnStyles[i].Font.Color = (i % 2 == 0) ? Color.Blue : Color.Green;

    // Optional: make the header bold for extra clarity.
    if (i == 0) // just an example, you could set this for all headers.
        columnStyles[i].Font.IsBold = true;
}
```

**Τι συμβαίνει;**  
- `workbook.CreateStyle()` μας δίνει έναν καθαρό καμβά για κάθε στήλη.  
- Η τριπλέτα `(i % 2 == 0) ? Color.Blue : Color.Green` είναι η καρδιά του **apply alternating column colors** – οι στήλες με άρτιο δείκτη γίνονται μπλε, οι περιττές πράσινες.  
- Μπορείτε να επεκτείνετε αυτό το μπλοκ για να ορίσετε γεμίσματα φόντου, περιγράμματα ή μορφές αριθμών χωρίς να αλλάξετε τον υπόλοιπο κώδικα.

> **Edge case:** Αν ο πίνακάς σας έχει περισσότερες από μερικές δεκάδες στήλες, η δημιουργία στυλ ανά στήλη μπορεί να καταναλώσει μνήμη. Σε αυτήν την περίπτωση, επαναχρησιμοποιήστε δύο αντικείμενα στυλ (blueStyle, greenStyle) και αναθέστε τα βάσει του δείκτη στήλης.

## Βήμα 3: Δημιουργία Δείγματος DataTable (ή χρήση του δικού σας)  

Για μια αυτόνομη επίδειξη θα δημιουργήσουμε ένα `DataTable` με μερικές γραμμές. Σε πραγματικά έργα θα αντικαταστήσετε το `GetSampleData()` με τη λογική ανάκτησης των πραγματικών σας δεδομένων.

```csharp
static DataTable GetSampleData()
{
    DataTable dt = new DataTable();

    // Define columns.
    dt.Columns.Add("ID", typeof(int));
    dt.Columns.Add("Name", typeof(string));
    dt.Columns.Add("Score", typeof(double));
    dt.Columns.Add("Date", typeof(DateTime));

    // Populate rows.
    for (int i = 1; i <= 5; i++)
    {
        dt.Rows.Add(i, $"Student {i}", 75 + i * 2, DateTime.Today.AddDays(-i));
    }

    return dt;
}
```

Τώρα ενσωματώστε το στο κύριο ρεύμα:

```csharp
DataTable dataTable = GetSampleData();   // <-- import datatable to excel
```

## Βήμα 4: Εισαγωγή DataTable σε Worksheet με Στυλ  

Το Aspose.Cells κάνει την εισαγωγή με μία γραμμή κώδικα. Η υπερφόρτωση που χρησιμοποιούμε μας επιτρέπει να περάσουμε τον πίνακα στυλ που δημιουργήσαμε νωρίτερα.

```csharp
// 0️⃣ Row and column offsets – start at A1 (0,0).
int startRow = 0;
int startColumn = 0;

// The 'true' flag tells the method that the first row in the DataTable
// contains column headers, which will be written to the sheet.
worksheet.Cells.ImportDataTable(dataTable, true, startRow, startColumn, columnStyles);
```

**Γιατί να χρησιμοποιήσετε αυτήν την υπερφόρτωση;**  
- Σεβεται τη γραμμή κεφαλίδας, έτσι δεν χρειάζεται να γράψετε χειροκίνητα τα ονόματα των στηλών.  
- Εφαρμόζει τον πίνακα **columnStyles** στήλη‑με‑στήλη, δίνοντάς μας τα εναλλασσόμενα χρώματα χωρίς επιπλέον βρόχους.  
- Είναι γρήγορη – ολόκληρος ο πίνακας φορτώνεται στη μνήμη με μία κλήση.

## Βήμα 5: Αποθήκευση Workbook – Εξαγωγή DataTable ως .xlsx  

Τέλος, αποθηκεύουμε το workbook στο δίσκο. Εδώ συμβαίνει το **export datatable as xlsx**.

```csharp
// Choose a folder that exists on your machine.
string outputPath = Path.Combine(Environment.CurrentDirectory, "output.xlsx");

// Save in the modern Office Open XML format.
workbook.Save(outputPath, SaveFormat.Xlsx);

Console.WriteLine($"Workbook saved to: {outputPath}");
```

Όταν ανοίξετε το `output.xlsx` θα δείτε:

| **ID** | **Name**      | **Score** | **Date**    |
|--------|---------------|-----------|-------------|
| *1* (μπλε) | *Student 1* (πράσινο) | *77* (μπλε) | *2026‑06‑26* (πράσινο) |
| *2* (πράσινο) | *Student 2* (μπλε) | *79* (πράσινο) | *2026‑06‑25* (μπλε) |
| …      | …             | …         | …           |

*Οι γραμματοσειρές μπλε και πράσινο εναλλάσσονται ανά στήλη, ακριβώς όπως κωδικοποιήσαμε.*

## Βήμα 6: Συνηθισμένα Πιθανά Σφάλματα & Πώς να τα Αποφύγετε  

| Πρόβλημα | Γιατί Συμβαίνει | Διόρθωση |
|----------|------------------|----------|
| **Τα στυλ δεν εφαρμόζονται** | Περνάτε `null` ή έναν πίνακα στυλ με διαφορετικό μήκος στην `ImportDataTable`. | Βεβαιωθείτε ότι `columnStyles.Length == dataTable.Columns.Count`. |
| **Το αρχείο κλειδωμένο μετά την αποθήκευση** | Άλλη διεργασία (π.χ. Excel) έχει ανοίξει το αρχείο. | Κλείστε τυχόν προβολείς πριν τρέξετε, ή αποθηκεύστε σε προσωρινό φάκελο και μετακινήστε το αρχείο μετά. |
| **Κατανάλωση μνήμης με τεράστιους πίνακες** | Δημιουργία στυλ ανά στήλη για χιλιάδες στήλες. | Επαναχρησιμοποιήστε δύο αντικείμενα στυλ και αναθέστε τα βάσει `(col % 2)`. |
| **Λανθασμένη μορφή ημερομηνίας** | Το Excel ερμηνεύει το `DateTime` ως αριθμό. | Ορίστε `columnStyles[i].Number = 14; // built‑in date format` για στήλες ημερομηνίας. |

## Βήμα 7: Επόμενα Βήματα – Πέρα από τη Βασική Μορφοποίηση  

Τώρα που έχετε κατακτήσει **πώς να μορφοποιήσετε στήλες Excel** με εναλλασσόμενα χρώματα, μπορείτε να πειραματιστείτε με:

- **Conditional formatting** – επισήμανση κελιών που πληρούν επιχειρηματικούς κανόνες.  
- **Table objects** – μετατροπή της περιοχής σε Excel Table για αυτόματα φίλτρα.  
- **Chart generation** – οπτικοποίηση των δεδομένων απευθείας από το workbook.  
- **Streaming large exports** – χρήση `SaveOptions` για εγγραφή τεράστιων αρχείων χωρίς φόρτωση όλης της μνήμης.

Όλα αυτά βασίζονται στις ίδιες βασικές έννοιες που καλύψαμε: δημιουργία workbook, στυλ κελιών, εισαγωγή δεδομένων και αποθήκευση.

---

### Συμπέρασμα  

Μάθατε **πώς να μορφοποιήσετε στήλες Excel** σε C# από την αρχή μέχρι το τέλος: δημιουργήστε ένα Excel workbook C#, εφαρμόστε εναλλασσόμενα χρώματα στηλών, εισάγετε ένα DataTable σε Excel, και τελικά εξάγετε το DataTable ως αρχείο .xlsx. Ο πλήρης κώδικας που παρέχεται λειτουργεί αμέσως, και οι εξηγήσεις απαντούν στο “γιατί” πίσω από κάθε γραμμή.

Μη διστάσετε να αλλάξετε τα χρώματα, να προσθέσετε περιγράμματα ή να μεταβείτε σε άλλη βιβλιοθήκη αν προτιμάτε. Το μοτίβο παραμένει το ίδιο, και το αποτέλεσμα είναι πάντα ένα καθαρό, επαγγελματικό spreadsheet έτοιμο για τους ενδιαφερόμενους.

Έχετε ερωτήσεις ή θέλετε να μοιραστείτε τις δικές σας τεχνικές μορφοποίησης; Αφήστε ένα σχόλιο παρακάτω και ας συνεχίσουμε τη συζήτηση. Καλό κώδικα!

## Τι Θα Μάθετε Στη Συνέχεια;


Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να κυριαρχήσετε σε επιπλέον δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στην υλοποίηση των δικών σας έργων.

- [How to Import DataTable into Excel Using Aspose.Cells for .NET (Step-by-Step Guide)](/cells/english/net/import-export/import-datatable-excel-aspose-cells-net/)
- [How to Create and Configure Excel Workbooks with Aspose.Cells .NET&#58; A Step-by-Step Guide](/cells/english/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)
- [How to Create and Style Excel Tables Using Aspose.Cells for .NET | Step‑By‑Step Guide](/cells/english/net/tables-structured-references/aspose-cells-net-excel-tables-styling/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}