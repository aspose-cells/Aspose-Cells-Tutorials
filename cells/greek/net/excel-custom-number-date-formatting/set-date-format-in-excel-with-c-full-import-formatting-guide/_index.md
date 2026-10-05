---
category: general
date: 2026-06-17
description: Ορίστε τη μορφή ημερομηνίας στο Excel χρησιμοποιώντας C# και επίσης ορίστε
  το φόντο του κελιού, εφαρμόστε χρώμα κειμένου και χρωματίστε τη στήλη του Excel
  κατά την εισαγωγή. Μάθετε βήμα‑βήμα.
draft: false
keywords:
- set date format
- set cell background
- apply foreground color
- color excel column
- excel import formatting
language: el
og_description: Ορίστε μορφή ημερομηνίας στο Excel με C# ενώ ορίζετε το φόντο του
  κελιού, εφαρμόζετε χρώμα κειμένου και χρωματίζετε τη στήλη του Excel κατά την εισαγωγή.
  Πλήρης οδηγός.
og_title: Ορισμός μορφής ημερομηνίας στο Excel με C# – Πλήρης οδηγός
schemas:
- author: Aspose
  dateModified: '2026-06-17'
  description: Set date format in Excel using C# and also set cell background, apply
    foreground color, and color Excel column during import. Learn step‑by‑step.
  headline: Set date format in Excel with C# – Full Import Formatting Guide
  type: TechArticle
- description: Set date format in Excel using C# and also set cell background, apply
    foreground color, and color Excel column during import. Learn step‑by‑step.
  name: Set date format in Excel with C# – Full Import Formatting Guide
  steps:
  - name: 2.1 Set Date Format for the First Column
    text: The first column (`OrderDate`) should display as “MM/dd/yyyy”. Aspose uses
      the built‑in number format index 14 for the short date, but you can also supply
      a custom format string if you prefer.
  - name: 2.2 Set Cell Background for the Second Column
    text: Let’s give the `CustomerName` column a light blue background. This is where
      **set cell background** comes into play.
  - name: 2.3 Apply Foreground (Text) Color – Optional Extra
    text: 'If you also want the text itself to be a contrasting color, you can tweak
      the same style:'
  - name: 3.1 Save the Workbook
    text: '```csharp // Save to a file – change path as needed wb.Save("FormattedReport.xlsx",
      SaveFormat.Xlsx); Console.WriteLine("Excel file created with date format and
      colors."); ```'
  - name: What if I have more than two columns?
    text: Just expand the `columnStyles` array and assign a `Style` to each index
      you care about. Unassigned indexes will fall back to the default style, which
      is perfectly fine.
  - name: How do I format a column as currency?
    text: '```csharp columnStyles[3] = wb.CreateStyle(); columnStyles[3].Number =
      164; // Built‑in currency format (e.g., $#,##0.00) ```'
  - name: Can I change the header row style separately?
    text: 'Yes. After the import, you can grab the first row and apply a distinct
      style:'
  - name: What if the DataTable contains null dates?
    text: 'Aspose will leave those cells blank. If you prefer a placeholder like “N/A”,
      you can preprocess the table:'
  type: HowTo
tags:
- excel
- csharp
- aspnet
- data-import
title: Ορισμός μορφής ημερομηνίας στο Excel με C# – Πλήρης οδηγός μορφοποίησης εισαγωγής
url: /el/net/excel-custom-number-date-formatting/set-date-format-in-excel-with-c-full-import-formatting-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ορισμός μορφής ημερομηνίας στο Excel με C# – Οδηγός πλήρους μορφοποίησης εισαγωγής

Έχετε ποτέ χρειαστεί να **ορίσετε μορφή ημερομηνίας** σε ένα φύλλο Excel που δημιουργείται από κώδικα C#, αλλά επίσης θέλετε η στήλη να έχει προσαρμοσμένο φόντο ή χρώμα κειμένου; Δεν είστε μόνοι. Σε πολλές περιπτώσεις αναφοράς παίρνετε ένα `DataTable` από μια βάση δεδομένων, το τοποθετείτε σε ένα φύλλο εργασίας και μετά τρέχετε να κάνετε τις ημερομηνίες να φαίνονται σωστά και τις στήλες να ξεχωρίζουν με τα σωστά χρώματα.

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα μια καθαρή, ολοκληρωμένη λύση που **ορίζει μορφή ημερομηνίας**, **ορίζει φόντο κελιού**, **εφαρμόζει χρώμα προσκηνίου**, και ακόμη **χρωματίζει μια στήλη Excel** κατά την εισαγωγή δεδομένων. Στο τέλος θα έχετε ένα επαναχρησιμοποιήσιμο μοτίβο που διαχειρίζεται **excel import formatting** χωρίς τα συνηθισμένα trial‑and‑error.

> **Τι θα χρειαστείτε**  
> * .NET 6+ (ή .NET Framework 4.7+)  
> * Aspose.Cells for .NET (η δωρεάν δοκιμή λειτουργεί για δοκιμές)  
> * Μια πηγή `DataTable` – οποιοδήποτε ερώτημα ADO.NET αρκεί  
> * Visual Studio ή το αγαπημένο σας IDE  

Ας ξεκινήσουμε.

---

## Επισκόπηση της Λύσης

Θα χωρίσουμε το πρόβλημα σε τρία λογικά τμήματα:

1. **Ανάκτηση των πηγαίων δεδομένων** – ένα `DataTable` με τις γραμμές που θέλετε να εξάγετε.  
2. **Δημιουργία στυλ ανά στήλη** – ένα στυλ για τη στήλη ημερομηνίας, ένα άλλο για μια στήλη κειμένου, συν τυχόν επιπλέον στυλ που θέλετε.  
3. **Εισαγωγή του πίνακα με στυλ** – χρησιμοποιήστε `Worksheet.Cells.ImportDataTable` ώστε κάθε στήλη να κληρονομεί το στυλ που προετοιμάσατε.

Γιατί αυτή η προσέγγιση; Επειδή το Aspose.Cells σας επιτρέπει να συνδέσετε έναν πίνακα `Style` απευθείας στην κλήση `ImportDataTable`, πράγμα που σημαίνει ότι δεν χρειάζεται δεύτερο πέρασμα για επαναεφαρμογή μορφοποίησης. Είναι πιο γρήγορο, λιγότερο επιρρεπές σε σφάλματα, και κρατά τον κώδικά σας τακτοποιημένο.

## Βήμα 1: Ανάκτηση των Δεδομένων για Εξαγωγή

Πρώτα απ' όλα – χρειάζεστε ένα `DataTable`. Σε ένα πραγματικό έργο πιθανότατα θα καλέσετε μια αποθηκευμένη διαδικασία ή θα χρησιμοποιήσετε το Entity Framework για να το γεμίσετε, αλλά για την επεξήγηση θα δημιουργήσουμε ένα απλό πίνακα με μια στήλη ημερομηνίας και μια στήλη κειμένου.

```csharp
using System;
using System.Data;
using Aspose.Cells;

DataTable GetData()
{
    var table = new DataTable();
    table.Columns.Add("OrderDate", typeof(DateTime));
    table.Columns.Add("CustomerName", typeof(string));

    // Sample rows – replace with your DB call
    table.Rows.Add(DateTime.Today.AddDays(-2), "Acme Corp");
    table.Rows.Add(DateTime.Today.AddDays(-1), "Globex Inc");
    table.Rows.Add(DateTime.Today, "Soylent Co");

    return table;
}
```

> **Συμβουλή:** Εάν η πηγή σας χρησιμοποιεί nullable ημερομηνίες, βεβαιωθείτε ότι ο τύπος της στήλης είναι `typeof(DateTime?)` – το Aspose θα σεβαστεί ακόμη και τη μορφή που θα ορίσετε αργότερα.

## Βήμα 2: Προετοιμασία Πίνακα Στυλ – Ένα ανά Στήλη

Τώρα δημιουργούμε ένα `Style[]` του οποίου το μήκος ταιριάζει με τον αριθμό των στηλών στο `DataTable`. Κάθε στοιχείο θα περιέχει τη μορφοποίηση για τη συγκεκριμένη στήλη.

```csharp
// Create a new workbook and get the first worksheet
Workbook wb = new Workbook();
Worksheet ws = wb.Worksheets[0];

// Pull the data
DataTable dataTable = GetData();

// Allocate the style array
Style[] columnStyles = new Style[dataTable.Columns.Count];
```

### 2.1 Ορισμός Μορφής Ημερομηνίας για την Πρώτη Στήλη

Η πρώτη στήλη (`OrderDate`) πρέπει να εμφανίζεται ως “MM/dd/yyyy”. Το Aspose χρησιμοποιεί τον ενσωματωμένο δείκτη μορφής αριθμού 14 για τη σύντομη ημερομηνία, αλλά μπορείτε επίσης να δώσετε μια προσαρμοσμένη συμβολοσειρά μορφής αν προτιμάτε.

```csharp
// Style for the date column (index 0)
columnStyles[0] = wb.CreateStyle();
columnStyles[0].Number = 14;               // Built‑in short date format
// Or a custom pattern:
// columnStyles[0].Custom = "mm/dd/yyyy";
```

**Γιατί αυτό είναι σημαντικό:** Το Excel αποθηκεύει τις ημερομηνίες ως σειριακούς αριθμούς. Αναθέτοντας μια μορφή αριθμού, λέτε στο Excel να εμφανίζει αυτούς τους σειριακούς αριθμούς ως ανθρώπινα αναγνώσιμες ημερομηνίες αντί για ακατέργαστους αριθμούς.

### 2.2 Ορισμός Φόντου Κελιού για τη Δεύτερη Στήλη

Ας δώσουμε στη στήλη `CustomerName` ένα ανοιχτό μπλε φόντο. Εδώ έρχεται σε εφαρμογή η λειτουργία **set cell background**.

```csharp
// Style for the text column (index 1)
columnStyles[1] = wb.CreateStyle();
columnStyles[1].ForegroundColor = System.Drawing.Color.LightBlue;
columnStyles[1].Pattern = BackgroundType.Solid; // Needed to show the color
```

> **Σημείωση:** Χωρίς να ορίσετε το `Pattern` σε `Solid`, το χρώμα προσκηνίου δεν θα εμφανιστεί επειδή το προεπιλεγμένο μοτίβο είναι “None”.

### 2.3 Εφαρμογή Χρώματος Προσκηνίου (Κειμένου) – Προαιρετικό Επιπλέον

Αν θέλετε επίσης το κείμενο να έχει αντίθετο χρώμα, μπορείτε να τροποποιήσετε το ίδιο στυλ:

```csharp
columnStyles[1].Font.Color = System.Drawing.Color.DarkBlue; // apply foreground color
```

Αυτό ικανοποιεί την απαίτηση **apply foreground color** διατηρώντας το φόντο της στήλης αμετάβλητο.

## Βήμα 3: Εισαγωγή του DataTable με τα Ορισμένα Στυλ

Με τα στυλ έτοιμα, το τελευταίο βήμα είναι μια μόνο γραμμή που εισάγει τα δεδομένα και εφαρμόζει τα στυλ στήλη‑με‑στήλη.

```csharp
// Import the DataTable starting at cell A1 (row 0, column 0)
// includeColumnNames = true to add a header row
ws.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
```

**Πώς λειτουργεί:** Το Aspose διαβάζει τον πίνακα `columnStyles` και αντιστοιχίζει κάθε `Style` στον αντίστοιχο δείκτη στήλης. Η γραμμή κεφαλίδας κληρονομεί το προεπιλεγμένο στυλ εκτός αν παρέχετε ξεχωριστό στυλ για τη γραμμή 0.

### 3.1 Αποθήκευση του Workbook

```csharp
// Save to a file – change path as needed
wb.Save("FormattedReport.xlsx", SaveFormat.Xlsx);
Console.WriteLine("Excel file created with date format and colors.");
```

Εκτελέστε το πρόγραμμα, ανοίξτε το *FormattedReport.xlsx*, και θα δείτε:

- Στήλη **OrderDate** εμφανιζόμενη ως ημερομηνίες (π.χ., `06/15/2026`).  
- Στήλη **CustomerName** με γέμισμα ανοιχτό‑μπλε και κείμενο σκούρο‑μπλε.

Αυτή είναι ολόκληρη η ροή εργασίας **excel import formatting** σε λιγότερο από 30 γραμμές C#.

## Ανασκόπηση Βήμα‑βήμα (με Τις Αιτίες)

| Βήμα | Τι κάνετε | Γιατί είναι σημαντικό |
|------|-----------|------------------------|
| **Retrieve data** | Κλήση `GetData()` για γέμισμα ενός `DataTable`. | Παρέχει μια δομημένη πηγή που το Aspose μπορεί να επεξεργαστεί άμεσα. |
| **Create style array** | Δέσμευση `Style[]` που ταιριάζει με τον αριθμό στηλών. | Επιτρέπει μορφοποίηση ανά στήλη σε μία κλήση εισαγωγής. |
| **Set date format** | `columnStyles[0].Number = 14;` | Διασφαλίζει ότι οι ημερομηνίες εμφανίζονται σωστά στο Excel. |
| **Set background color** | `ForegroundColor = LightBlue; Pattern = Solid;` | Επισημαίνει τη στήλη, ικανοποιώντας το **set cell background**. |
| **Apply foreground color** | `Font.Color = DarkBlue;` | Βελτιώνει την αναγνωσιμότητα και ικανοποιεί το **apply foreground color**. |
| **Import with styles** | `ImportDataTable(..., columnStyles);` | Εισαγωγή με ένα πέρασμα που σέβεται όλη τη μορφοποίηση. |
| **Save workbook** | `wb.Save(...);` | Διατηρεί το αποτέλεσμα για τους επόμενους χρήστες. |

## Διαχείριση Ακραίων Περιπτώσεων & Συχνές Ερωτήσεις

### Τι γίνεται αν έχω περισσότερες από δύο στήλες;

Απλώς επεκτείνετε τον πίνακα `columnStyles` και αναθέστε ένα `Style` σε κάθε δείκτη που σας ενδιαφέρει. Οι μη ανατεθειμένοι δείκτες θα επιστρέψουν στο προεπιλεγμένο στυλ, το οποίο είναι απολύτως εντάξει.

```csharp
columnStyles[2] = wb.CreateStyle();
columnStyles[2].Number = 0; // General format for numeric columns
```

### Πώς μορφοποιώ μια στήλη ως νόμισμα;

```csharp
columnStyles[3] = wb.CreateStyle();
columnStyles[3].Number = 164; // Built‑in currency format (e.g., $#,##0.00)
```

### Μπορώ να αλλάξω το στυλ της γραμμής κεφαλίδας ξεχωριστά;

Ναι. Μετά την εισαγωγή, μπορείτε να πάρετε την πρώτη γραμμή και να εφαρμόσετε ένα ξεχωριστό στυλ:

```csharp
Style headerStyle = wb.CreateStyle();
headerStyle.Font.IsBold = true;
headerStyle.ForegroundColor = System.Drawing.Color.Gold;
headerStyle.Pattern = BackgroundType.Solid;

ws.Cells.Rows[0].ApplyStyle(headerStyle, new StyleFlag { All = true });
```

### Τι γίνεται αν το DataTable περιέχει null ημερομηνίες;

Το Aspose θα αφήσει αυτά τα κελιά κενά. Αν προτιμάτε ένα placeholder όπως “N/A”, μπορείτε να προεπεξεργαστείτε τον πίνακα:

```csharp
foreach (DataRow row in dataTable.Rows)
{
    if (row.IsNull("OrderDate"))
        row["OrderDate"] = DateTime.MinValue; // or any sentinel
}
```

Στη συνέχεια προσαρμόστε το στυλ ώστε να εμφανίζει μια προσαρμοσμένη μορφή που δείχνει “N/A” για την τιμή sentinel.

## Πλήρες Παράδειγμα Εργασίας

Παρακάτω είναι το πλήρες πρόγραμμα, έτοιμο για αντιγραφή‑επικόλληση. Εκτελέστε το ως εφαρμογή κονσόλας και θα λάβετε ένα ωραία μορφοποιημένο αρχείο Excel.



## Τι Θα Πρέπει Να Μάθετε Στη Σύντομη Μελλοντική;

Τα παρακάτω tutorials καλύπτουν στενά σχετικές θεματικές που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Ορισμός Χρώματος Γραμματοσειράς σε Κελιά Excel χρησιμοποιώντας Aspose.Cells για .NET](/cells/english/net/formatting/setting-font-color/)
- [Ορισμός Χρώματος Γραμματοσειράς σε .NET Excel με Aspose.Cells](/cells/english/net/formatting/set-font-color-net-excel-aspose-cells/)
- [Ορισμός Πλάτους Στήλης Excel σε Pixels Χρησιμοποιώντας Aspose.Cells για .NET | Οδηγός Βήμα‑βήμα](/cells/english/net/formatting/set-excel-column-width-pixels-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}