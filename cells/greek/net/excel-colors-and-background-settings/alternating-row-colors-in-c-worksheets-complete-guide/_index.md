---
category: general
date: 2026-05-30
description: Μάθετε πώς να προσθέτετε εναλλασσόμενα χρώματα γραμμών σε φύλλα εργασίας
  C#, να ορίζετε το φόντο των κελιών με συμπαγό μοτίβο γεμίσματος και να προσαρμόζετε
  το στυλ των κελιών του φύλλου εργασίας με ευκολία.
draft: false
keywords:
- alternating row colors
- set cell background
- solid fill pattern
- add background color
- worksheet cell style
language: el
og_description: Εναλλασσόμενα χρώματα γραμμών σε φύλλα εργασίας C# με ευκολία. Μάθετε
  πώς να ορίζετε το φόντο των κελιών, να χρησιμοποιείτε στερεό μοτίβο γεμίσματος και
  να κυριαρχείτε στο στυλ κελιών του φύλλου εργασίας.
og_title: Εναλλασσόμενα Χρώματα Γραμμών σε Φύλλα Εργασίας C# – Πλήρης Οδηγός
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Learn how to add alternating row colors in C# worksheets, set cell
    background with a solid fill pattern, and customize worksheet cell style effortlessly.
  headline: Alternating Row Colors in C# Worksheets – Complete Guide
  type: TechArticle
- description: Learn how to add alternating row colors in C# worksheets, set cell
    background with a solid fill pattern, and customize worksheet cell style effortlessly.
  name: Alternating Row Colors in C# Worksheets – Complete Guide
  steps:
  - name: Why Use a **Solid Fill Pattern**?
    text: The `Pattern` property tells the engine how to render the color. A `Solid`
      fill guarantees that the entire cell background is painted, eliminating any
      faint gridlines that might otherwise show through. This is the most common way
      to **set cell background** when you want a clean look.
  - name: Change the Colors
    text: 'If your brand uses different hues, just replace `Color.LightYellow` and
      `Color.LightCyan` with any `System.Drawing.Color` you prefer. For example:'
  - name: Use a Different **Background Type**
    text: While `BackgroundType.Solid` is the most common, you can experiment with
      `BackgroundType.Gray125`, `BackgroundType.Horizontal`, or any pattern that the
      library supports. This changes the visual texture while still **adding background
      color**.
  - name: Apply a **Worksheet Cell Style** to Specific Columns
    text: 'Sometimes you only want the alternating effect on data columns, leaving
      the first column (e.g., IDs) untouched. Create a separate style for that column
      and assign it after the import:'
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
- DataTable
- Styling
title: Εναλλασσόμενα Χρώματα Γραμμών σε Φύλλα Εργασίας C# – Πλήρης Οδηγός
url: /el/net/excel-colors-and-background-settings/alternating-row-colors-in-c-worksheets-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εναλλασσόμενα Χρώματα Γραμμών σε Φύλλα Εργασίας C# – Πλήρης Οδηγός

Έχετε αναρωτηθεί ποτέ πώς να κάνετε την εξαγωγή Excel σας να φαίνεται επαγγελματική χρησιμοποιώντας **εναλλασσόμενα χρώματα γραμμών**; Δεν είστε μόνοι—οι προγραμματιστές ζητούν συνεχώς πώς να *προσθέσουν χρώμα φόντου* σε γραμμές χωρίς να γράψουν εκατομμύρια γραμμές κώδικα.  

Σε αυτό το σεμινάριο θα περάσουμε βήμα-βήμα μια απλή μέθοδο για να **ορίσετε το φόντο των κελιών** σε κάθε γραμμή, να εφαρμόσετε ένα **συμπαγές μοτίβο γεμίσματος**, και να ελέγξετε το **στυλ κελιού φύλλου εργασίας** ώστε το αποτέλεσμα να είναι τόσο αναγνώσιμο όσο και οπτικά ελκυστικό.

## Τι Θα Μάθετε

- Ανακτήστε δεδομένα σε ένα `DataTable` (ή οποιαδήποτε πηγή πινάκων).  
- Δημιουργήστε έναν πίνακα αντικειμένων `Style` που εναλλάσσεται μεταξύ δύο χρωμάτων.  
- Εισάγετε το `DataTable` σε ένα φύλλο εργασίας εφαρμόζοντας αυτά τα στυλ.  
- Επαληθεύστε το αποτέλεσμα και προσαρμόστε τα χρώματα ή τα μοτίβα αν χρειάζεται.  

Δεν απαιτούνται εξωτερικά εργαλεία πέρα από ένα περιβάλλον .NET και μια βιβλιοθήκη λογιστικών φύλλων (θα χρησιμοποιήσουμε το **Aspose.Cells** στα παραδείγματα). Στο τέλος θα έχετε μια επαναχρησιμοποιήσιμη μέθοδο που μπορείτε να ενσωματώσετε σε οποιοδήποτε pipeline αναφορών.

---

## Βήμα 1: Ανακτήστε τα Πηγαία Δεδομένα ως `DataTable`

Πρώτα απ' όλα—χωρίς δεδομένα δεν υπάρχει τίποτα για στυλιζάρετε. Παρακάτω υπάρχει ένας μικρός βοηθός που δημιουργεί ένα `DataTable` με δείγμα γραμμών. Σε ένα πραγματικό έργο θα το αντικαταστήσετε με κλήση σε βάση δεδομένων ή αναλυτή CSV.

```csharp
using System;
using System.Data;

static DataTable GetData()
{
    // Create a simple table with three columns
    DataTable table = new DataTable("Report");
    table.Columns.Add("ID", typeof(int));
    table.Columns.Add("Name", typeof(string));
    table.Columns.Add("Score", typeof(double));

    // Populate with dummy rows
    for (int i = 1; i <= 10; i++)
    {
        table.Rows.Add(i, $"Item {i}", Math.Round(new Random().NextDouble() * 100, 2));
    }

    return table;
}
```

> **Γιατί είναι σημαντικό:** Η ύπαρξη των δεδομένων σε ένα `DataTable` επιτρέπει στη μηχανή του φύλλου εργασίας να τα *εισάγει* με μία κλήση, διατηρώντας αυτόματα τα ονόματα των στηλών και τους τύπους δεδομένων.

## Βήμα 2: Δημιουργήστε Στυλ **Εναλλασσόμενων Χρωμάτων Γραμμών**

Τώρα θα δημιουργήσουμε έναν πίνακα αντικειμένων `Style`—ένα ανά γραμμή—ώστε οι ζυγές γραμμές να λαμβάνουν μια ανοιχτό κίτρινη απόχρωση ενώ οι περιττές γραμμές θα έχουν ένα απαλό κυανό. Αυτό είναι ο πυρήνας της τεχνικής **εναλλασσόμενων χρωμάτων γραμμών**.

```csharp
using Aspose.Cells;
using System.Drawing;

// Assume workbook and worksheet are already instantiated
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];

// Retrieve data
DataTable dataTable = GetData();

// Prepare an array of styles – one for each row in the table
Style[] rowStyles = new Style[dataTable.Rows.Count];

for (int i = 0; i < rowStyles.Length; i++)
{
    // Create a fresh style for the current row
    rowStyles[i] = workbook.CreateStyle();

    // **Add background color**: LightYellow for even rows, LightCyan for odd rows
    rowStyles[i].ForegroundColor = (i % 2 == 0)
        ? Color.LightYellow
        : Color.LightCyan;

    // **Set cell background** using a **solid fill pattern**
    rowStyles[i].Pattern = BackgroundType.Solid;

    // Optional: you could also set font color, borders, etc., here
}
```

### Γιατί να Χρησιμοποιήσετε ένα **Συμπαγές Μοτίβο Γέμισης**;

Η ιδιότητα `Pattern` λέει στη μηχανή πώς να αποδώσει το χρώμα. Ένα `Solid` γέμισμα εγγυάται ότι ολόκληρο το φόντο του κελιού θα χρωματιστεί, εξαλείφοντας τυχόν αχνές γραμμές πλέγματος που θα μπορούσαν να φανούν. Αυτή είναι η πιο κοινή μέθοδος για να **ορίσετε το φόντο των κελιών** όταν θέλετε μια καθαρή εμφάνιση.

## Βήμα 3: Εισάγετε το `DataTable` με τα Προετοιμασμένα Στυλ

Με τον πίνακα στυλ έτοιμο, η κλήση εισαγωγής γίνεται μια γραμμή κώδικα. Το Aspose.Cells θα εφαρμόσει αυτόματα το αντίστοιχο στυλ σε κάθε γραμμή.

```csharp
// Import the DataTable into the worksheet, applying the prepared styles
worksheet.Cells.ImportDataTable(
    dataTable,                     // source
    true,                          // include column names
    0,                             // start row (0‑based)
    0,                             // start column (0‑based)
    rowStyles);                    // array of styles
```

> **Τι συμβαίνει στο παρασκήνιο;**  
> Η βιβλιοθήκη διατρέχει κάθε γραμμή, αντιγράφει τις τιμές στα κελιά και στη συνέχεια εφαρμόζει το αντίστοιχο `Style` από το `rowStyles`. Επειδή έχουμε ήδη ορίσει ένα **συμπαγές μοτίβο γέμισης**, κάθε κελί σε μια γραμμή κληρονομεί το ίδιο χρώμα φόντου, παρέχοντάς σας τέλεια **εναλλασσόμενα χρώματα γραμμών**.

## Βήμα 4: Αποθηκεύστε το Workbook και Επαληθεύστε το Αποτέλεσμα

Μια γρήγορη αποθήκευση σας επιτρέπει να ανοίξετε το αρχείο στο Excel (ή σε οποιονδήποτε συμβατό προβολέα) και να δείτε το αποτέλεσμα.

```csharp
// Save to disk – you can change the format to .xlsx, .xls, .csv, etc.
workbook.Save("AlternatingRowsReport.xlsx", SaveFormat.Xlsx);
Console.WriteLine("Workbook saved. Open 'AlternatingRowsReport.xlsx' to see the result.");
```

Όταν ανοίξετε το αρχείο, οι γραμμές 1, 3, 5… θα είναι ανοιχτό κίτρινες, ενώ οι γραμμές 2, 4, 6… θα είναι ανοιχτό κυανές. Οι επικεφαλίδες των στηλών παραμένουν λευκές, κάνοντας τα δεδομένα να ξεχωρίζουν.

![Φύλλο εργασίας που εμφανίζει εναλλασσόμενα χρώματα γραμμών](/images/alternating-row-colors.png "Στιγμιότυπο οθόνης του φύλλου εργασίας με εναλλασσόμενα χρώματα γραμμών")

*Κείμενο εναλλακτικής εικόνας:* **εναλλασσόμενα χρώματα γραμμών** στιγμιότυπο οθόνης ενός φύλλου εργασίας όπου το φόντο κάθε γραμμής εναλλάσσεται μεταξύ ανοιχτό κίτρινου και ανοιχτό κυανού.

## Βήμα 5: Προσαρμογή Περαιτέρω (Προαιρετικό)

### Αλλαγή των Χρωμάτων

Αν η μάρκα σας χρησιμοποιεί διαφορετικές αποχρώσεις, απλώς αντικαταστήστε τα `Color.LightYellow` και `Color.LightCyan` με οποιοδήποτε `System.Drawing.Color` προτιμάτε. Για παράδειγμα:

```csharp
rowStyles[i].ForegroundColor = (i % 2 == 0) ? Color.FromArgb(255, 235, 205) // Peach
                                            : Color.FromArgb(205, 235, 255); // Soft blue
```

### Χρησιμοποιήστε Διαφορετικό **Τύπο Φόντου**

Ενώ το `BackgroundType.Solid` είναι το πιο κοινό, μπορείτε να πειραματιστείτε με `BackgroundType.Gray125`, `BackgroundType.Horizontal`, ή οποιοδήποτε μοτίβο υποστηρίζει η βιβλιοθήκη. Αυτό αλλάζει την οπτική υφή ενώ εξακολουθεί να **προσθέτει χρώμα φόντου**.

### Εφαρμόστε ένα **Στυλ Κελιού Φύλλου Εργασίας** σε Συγκεκριμένες Στήλες

Μερικές φορές θέλετε μόνο το εναλλασσόμενο εφέ στις στήλες δεδομένων, αφήνοντας την πρώτη στήλη (π.χ., IDs) αμετάβλητη. Δημιουργήστε ένα ξεχωριστό στυλ για αυτή τη στήλη και αντιστοιχίστε το μετά την εισαγωγή:

```csharp
Style idStyle = workbook.CreateStyle();
idStyle.ForegroundColor = Color.White;
idStyle.Pattern = BackgroundType.Solid;

// Apply to the first column (A)
for (int row = 0; row < dataTable.Rows.Count + 1; row++) // +1 for header
{
    worksheet.Cells[row, 0].SetStyle(idStyle);
}
```

---

## Συμπέρασμα

Τώρα έχετε μια πλήρη, επαναχρησιμοποιήσιμη λύση για **εναλλασσόμενα χρώματα γραμμών** σε φύλλα εργασίας C#. Δημιουργώντας έναν πίνακα αντικειμένων `Style`, **ορίζοντας το φόντο των κελιών** με ένα **συμπαγές μοτίβο γέμισης**, και εισάγοντας ένα `DataTable` με μία κλήση, μπορείτε να παράγετε επαγγελματικές αναφορές με ελάχιστο κώδικα.  

Από εδώ μπορείτε:

- **Προσθέστε χρώμα φόντου** στις γραμμές κεφαλίδας για επιπλέον έμφαση.  
- Συνδυάστε την τεχνική με μορφοποίηση υπό όρους για δυναμικές οπτικές ενδείξεις.  
- Εξερευνήστε άλλες ιδιότητες **στυλ κελιού φύλλου εργασίας** όπως γραμματοσειρές, περιγράμματα ή μορφές αριθμών.

Δοκιμάστε το στην επόμενη διαδικασία εξαγωγής—οι χρήστες σας θα σας ευχαριστήσουν για τα πιο καθαρά, πιο αναγνώσιμα λογιστικά φύλλα. Καλή προγραμματιστική!

## Τι Θα Μάθετε Στη Σειρά;

- [Ορισμός Ύψους Γραμμής σε Φύλλο Εργασίας με Aspose.Cells για .NET](/cells/english/net/size-and-spacing-customization/setting-height-of-all-rows-in-worksheet/)
- [Μετατροπή Ονομάτων Κελιών Excel σε Δείκτες Γραμμής και Στήλης Χρησιμοποιώντας Aspose.Cells για .NET](/cells/english/net/cell-operations/convert-excel-cell-names-to-indices-aspose-cells-dotnet/)
- [Ορισμός Χρωμάτων Καρτέλας Φύλλου Εργασίας στο Excel Χρησιμοποιώντας Aspose.Cells .NET - Ένας Πλήρης Οδηγός](/cells/english/net/worksheet-management/set-worksheet-tab-colors-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}