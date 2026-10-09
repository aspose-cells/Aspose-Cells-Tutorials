---
category: general
date: 2026-06-05
description: Εφαρμόστε στυλ κελιών κατά τη χρήση της εισαγωγής Aspose.Cells. Μάθετε
  πώς να εισάγετε DataTable με μορφοποίηση, να μορφοποιείτε γραμμές και να διατηρείτε
  τα φύλλα εργασίας τακτικά.
draft: false
keywords:
- apply cell styles
- aspose cells import
- import with formatting
- how to import datatable
- import datatable worksheet
language: el
og_description: Εφαρμόστε στυλ κελιών κατά την εισαγωγή ενός DataTable σε ένα φύλλο
  εργασίας Aspose.Cells. Οδηγός βήμα‑προς‑βήμα με πλήρη κώδικα και συμβουλές.
og_title: Εφαρμογή Στυλ Κελιών με το Aspose.Cells – Εισαγωγή DataTable
schemas:
- author: Aspose
  dateModified: '2026-06-05'
  description: Apply cell styles while using Aspose.Cells import. Learn how to import
    DataTable with formatting, style rows, and keep worksheets tidy.
  headline: Apply Cell Styles with Aspose.Cells – Import DataTable with Formatting
  type: TechArticle
- description: Apply cell styles while using Aspose.Cells import. Learn how to import
    DataTable with formatting, style rows, and keep worksheets tidy.
  name: Apply Cell Styles with Aspose.Cells – Import DataTable with Formatting
  steps:
  - name: How It Works
    text: 1. **Headers** – Because we passed `true`, Aspose writes “Name” and “Score”
      into the first row. 2. **Data Rows** – Each subsequent row receives the corresponding
      style from `importStyles`. 3. **Performance** – The method streams the data
      directly into the worksheet, which is faster than looping cell
  - name: What if My DataTable Has More Columns Than Styles?
    text: Aspose will apply the last style in the array to any extra columns. To avoid
      unexpected colors, always match the array length to the column count, or pass
      `null` for columns you don’t want styled.
  - name: Can I Apply Different Styles to Specific Rows?
    text: 'Absolutely. After the import, you can loop through rows and assign new
      `Style` objects based on conditions (e.g., highlight scores > 90 in green).
      Here’s a quick snippet:'
  - name: Does This Work with Large DataSets?
    text: Yes. `ImportDataTable` streams data efficiently, and applying a static style
      array adds negligible overhead. For millions of rows, consider using `ImportDataTable`
      in chunks or leveraging `Cells.ImportDataTable` with a `DataReader` for even
      better memory usage.
  - name: How Do I Preserve Existing Formatting in the Worksheet?
    text: If the target range already has formatting you want to keep, set the `ImportDataTable`
      overload’s `importOptions` parameter (`ImportTableOptions`) and tweak `ImportDataTableOptions.PreserveCellFormatting`.
      The default behavior overwrites styles with the ones you supply.
  type: HowTo
tags:
- Aspose.Cells
- C#
- DataTable
title: Εφαρμόστε στυλ κελιών με το Aspose.Cells – Εισαγωγή DataTable με μορφοποίηση
url: /el/net/excel-formatting-and-styling/apply-cell-styles-with-aspose-cells-import-datatable-with-fo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εφαρμογή Στυλ Κελιών με Aspose.Cells – Εισαγωγή DataTable με Μορφοποίηση

Έχετε αναρωτηθεί ποτέ πώς να **εφαρμόσετε στυλ κελιών** όταν μεταφέρετε ένα `DataTable` σε ένα φύλλο Excel; Δεν είστε μόνοι. Σε πολλά σενάρια αναφοράς χρειάζεστε τα δεδομένα να φαίνονται καλά αμέσως—χωρίς χειροκίνητη μορφοποίηση αργότερα. Τα καλά νέα είναι ότι το Aspose.Cells κάνει εύκολη τη **εισαγωγή με μορφοποίηση**, ώστε οι γραμμές σας να είναι κόκκινες ή μπλε, έντονες ή ό,τι θέλετε.

Σε αυτό το tutorial θα περάσουμε από ένα πλήρες, εκτελέσιμο παράδειγμα που δείχνει **πώς να εισαγάγετε datatable** σε ένα φύλλο εργασίας **με εφαρμοσμένα στυλ κελιών**. Στο τέλος θα έχετε μια έτοιμη‑για‑εκτέλεση εφαρμογή C# console που δημιουργεί ένα workbook, μορφοποιεί τις δύο πρώτες στήλες και αποθηκεύει το αρχείο—όλα χρησιμοποιώντας το API `aspose cells import`.

## Τι Θα Μάθετε

- Ρυθμίστε το Aspose.Cells σε ένα έργο .NET  
- Δημιουργήστε ένα δείγμα `DataTable` που μιμείται δεδομένα πραγματικού κόσμου  
- Ορίστε αντικείμενα `Style` για κόκκινη και μπλε γραμματοσειρά  
- Χρησιμοποιήστε `Worksheet.Cells.ImportDataTable` για **εισαγωγή datatable worksheet** ενώ εφαρμόζετε τα στυλ  
- Επαληθεύστε το αποτέλεσμα και αποθηκεύστε το workbook  

Χωρίς εξωτερικά εργαλεία, μόνο καθαρό C# και Aspose.Cells. Ας ξεκινήσουμε.

---

## Προαπαιτούμενα

Πριν βουτήξουμε στον κώδικα, βεβαιωθείτε ότι έχετε τα παρακάτω:

| Απαίτηση | Γιατί είναι σημαντικό |
|----------|-----------------------|
| .NET 6.0 ή νεότερο | Το Aspose.Cells 23.x στοχεύει στο .NET Standard 2.0+, έτσι το .NET 6 σας παρέχει τις πιο πρόσφατες δυνατότητες χρόνου εκτέλεσης. |
| Aspose.Cells για .NET (NuGet) | Η βιβλιοθήκη παρέχει τις μεθόδους `Workbook`, `Worksheet`, `Style` και `ImportDataTable` που χρειαζόμαστε. |
| Βασικές γνώσεις C# | Θα κατανοήσετε κλάσεις, πίνακες και δηλώσεις `using`. |
| Ένα IDE (Visual Studio, VS Code, Rider) | Οποιοσδήποτε επεξεργαστής λειτουργεί, αλλά θα χρειαστεί να επαναφέρετε τα πακέτα NuGet. |

Μπορείτε να εγκαταστήσετε το πακέτο από τη γραμμή εντολών:

```bash
dotnet add package Aspose.Cells
```

---

## Βήμα 1: Δημιουργία Νέου Workbook και Πρόσβαση στο Πρώτο Worksheet

Πρώτα απ' όλα—ας δημιουργήσουμε ένα `Workbook` και ας πάρουμε το πρώτο φύλλο. Σκεφτείτε το workbook ως ένα κενό σημειωματάριο· το πρώτο worksheet είναι η σελίδα στην οποία θα γράψουμε.

```csharp
using Aspose.Cells;
using System;
using System.Data;
using System.Drawing;

class Program
{
    static void Main()
    {
        // Create a new workbook (equivalent to a new Excel file)
        Workbook wb = new Workbook();

        // Access the first worksheet (index 0)
        Worksheet worksheet = wb.Worksheets[0];
```

> **Συμβουλή:** Αν χρειαστείτε ποτέ πολλαπλά φύλλα, απλώς προσθέστε τα με `wb.Worksheets.Add()` και αναφερθείτε σε αυτά με όνομα ή δείκτη.

---

## Βήμα 2: Προετοιμασία Δείγματος DataTable (Πώς να Εισαγάγετε DataTable)

Τώρα χρειαζόμαστε κάτι για εισαγωγή. Σε πραγματικά έργα θα καλέσετε μια βάση δεδομένων, αλλά για σαφήνεια θα δημιουργήσουμε ένα `DataTable` στη μνήμη.

```csharp
        // Build a sample DataTable with two columns: Name and Score
        DataTable dataTable = new DataTable("Results");
        dataTable.Columns.Add("Name", typeof(string));
        dataTable.Columns.Add("Score", typeof(int));

        // Populate rows – imagine these came from a query
        dataTable.Rows.Add("Alice", 85);
        dataTable.Rows.Add("Bob", 92);
        dataTable.Rows.Add("Charlie", 78);
        dataTable.Rows.Add("Diana", 91);
```

> **Γιατί είναι σημαντικό:** Το να έχετε ένα `DataTable` μας επιτρέπει να δοκιμάσουμε τη ροή **aspose cells import** χωρίς εξωτερικές εξαρτήσεις.

---

## Βήμα 3: Ορισμός των Στυλ που Θα Εφαρμοστούν στα Εισαγόμενα Κελιά

Εδώ συμβαίνει η μαγεία. Θα δημιουργήσουμε δύο αντικείμενα `Style`: ένα με κόκκινη γραμματοσειρά, ένα άλλο με μπλε γραμματοσειρά. Αυτά θα εφαρμοστούν ανά στήλη κατά τη διάρκεια της εισαγωγής.

```csharp
        // Define an array of styles – one per column
        Style[] importStyles = new Style[2];

        // Style for the first column (Name) – red text
        Style redStyle = wb.CreateStyle();
        redStyle.Font.Color = Color.Red;
        importStyles[0] = redStyle;

        // Style for the second column (Score) – blue text
        Style blueStyle = wb.CreateStyle();
        blueStyle.Font.Color = Color.Blue;
        importStyles[1] = blueStyle;
```

> **Προσοχή:** Το μήκος του `importStyles` πρέπει να ταιριάζει με τον αριθμό των στηλών που εισάγετε, διαφορετικά το Aspose θα ρίξει ένα `ArgumentException`.

---

## Βήμα 4: Εισαγωγή του DataTable στο Worksheet **με Μορφοποίηση**

Τώρα φέρνουμε όλα μαζί. Η υπερφόρτωση `ImportDataTable` που χρησιμοποιούμε δέχεται τον πίνακα `Style[]`, επιτρέποντάς μας να **εφαρμόσουμε στυλ κελιών** καθώς τα δεδομένα τοποθετούνται στο φύλλο.

```csharp
        // Import the DataTable starting at cell A1 (row 0, column 0)
        // The 'true' flag tells Aspose to generate column headers automatically
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, importStyles);
```

### Πώς Λειτουργεί

1. **Κεφαλίδες** – Επειδή περάσαμε `true`, το Aspose γράφει “Name” και “Score” στην πρώτη γραμμή.  
2. **Γραμμές Δεδομένων** – Κάθε επόμενη γραμμή λαμβάνει το αντίστοιχο στυλ από το `importStyles`.  
3. **Απόδοση** – Η μέθοδος μεταδίδει τα δεδομένα απευθείας στο worksheet, κάτι που είναι πιο γρήγορο από το βρόχο κελί‑ανά‑κελί.

---

## Βήμα 5: Επαλήθευση του Αποτελέσματος και Αποθήκευση του Workbook

Ας ρίξουμε μια ματιά στα πρώτα μερικά κελιά για να βεβαιωθούμε ότι τα στυλ εφαρμόστηκαν, και στη συνέχεια γράψτε το αρχείο στο δίσκο.

```csharp
        // Optional: Quick sanity check – print the first row's values
        Console.WriteLine("Header Row:");
        Console.WriteLine($"{worksheet.Cells[0, 0].StringValue} | {worksheet.Cells[0, 1].StringValue}");

        // Save the workbook to an Excel file
        string outputPath = "StyledImport.xlsx";
        wb.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

Όταν ανοίξετε το **StyledImport.xlsx**, θα δείτε:

- Τη στήλη “Name” με κείμενο **κόκκινο**.  
- Τη στήλη “Score” με κείμενο **μπλε**.  
- Τις κεφαλίδες στηλών στο προεπιλεγμένο στυλ (μπορείτε επίσης να τις μορφοποιήσετε, αλλά αυτό είναι άλλο tutorial).

![Παράδειγμα εφαρμογής στυλ κελιών](https://example.com/images/apply-cell-styles.png "Εφαρμογή στυλ κελιών στο Aspose.Cells")

> **Σημείωση:** Η παραπάνω εικόνα δείχνει την τελική εμφάνιση. Το χαρακτηριστικό `alt` περιέχει τη βασική λέξη-κλειδί, ικανοποιώντας τις απαιτήσεις SEO.

---

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

### Τι γίνεται αν το DataTable μου έχει περισσότερες στήλες από τα Στυλ;

Το Aspose θα εφαρμόσει το τελευταίο στυλ στον πίνακα σε οποιεσδήποτε επιπλέον στήλες. Για να αποφύγετε απρόσμενα χρώματα, ταιριάξτε πάντα το μήκος του πίνακα με τον αριθμό των στηλών, ή περάστε `null` για στήλες που δεν θέλετε να μορφοποιηθούν.

### Μπορώ να Εφαρμόσω Διαφορετικά Στυλ σε Συγκεκριμένες Γραμμές;

Απόλυτα. Μετά την εισαγωγή, μπορείτε να κάνετε βρόχο στις γραμμές και να εκχωρήσετε νέα αντικείμενα `Style` βάσει συνθηκών (π.χ., να επισημάνετε σκορ > 90 σε πράσινο). Εδώ είναι ένα σύντομο απόσπασμα:

```csharp
for (int i = 1; i <= dataTable.Rows.Count; i++) // start at 1 to skip header
{
    int score = worksheet.Cells[i, 1].IntValue;
    if (score > 90)
    {
        Style highScore = wb.CreateStyle();
        highScore.Font.Color = Color.Green;
        worksheet.Cells[i, 1].SetStyle(highScore);
    }
}
```

### Λειτουργεί Αυτό με Μεγάλα DataSets;

Ναι. Το `ImportDataTable` μεταδίδει τα δεδομένα αποδοτικά, και η εφαρμογή ενός στατικού πίνακα στυλ προσθέτει αμελητέο κόστος. Για εκατομμύρια γραμμές, σκεφτείτε να χρησιμοποιήσετε το `ImportDataTable` σε τμήματα ή να αξιοποιήσετε το `Cells.ImportDataTable` με `DataReader` για ακόμη καλύτερη χρήση μνήμης.

### Πώς Διατηρώ την Υπάρχουσα Μορφοποίηση στο Worksheet;

Αν η περιοχή-στόχος έχει ήδη μορφοποίηση που θέλετε να διατηρήσετε, ορίστε την παράμετρο `importOptions` της υπερφόρτωσης `ImportDataTable` (`ImportTableOptions`) και ρυθμίστε το `ImportDataTableOptions.PreserveCellFormatting`. Η προεπιλεγμένη συμπεριφορά αντικαθιστά τα στυλ με αυτά που παρέχετε.

---

## Ανακεφαλαίωση: Τι Καταφέραμε

- **Εφαρμόστηκαν στυλ κελιών** κατά τη διάρκεια μιας λειτουργίας **aspose cells import**.  
- Δείξαμε **εισαγωγή με μορφοποίηση** περνώντας έναν πίνακα `Style[]`.  
- Δείξαμε **πώς να εισαγάγετε datatable** σε ένα worksheet και να αποθηκεύσετε το αποτέλεσμα.  
- Καλύψαμε ακραίες περιπτώσεις όπως μη ταιριασμένοι αριθμοί στυλ και υπό συνθήκες μορφοποίηση γραμμών.

Όλα αυτά έγιναν σε μια ενιαία, αυτόνομη εφαρμογή console—χωρίς εξωτερικά scripts, χωρίς χειροκίνητη επεξεργασία Excel. Τώρα έχετε μια ισχυρή βάση για οποιοδήποτε χαρακτηριστικό αναφοράς ή εξαγωγής δεδομένων που χρειάζεται επεξεργασμένο Excel output.

---

## Επόμενα Βήματα

Έτοιμοι να ανεβάσετε επίπεδο; Εδώ είναι μερικές ιδέες που βασίζονται σε ό,τι μάθατε:

- **Μορφοποίηση της γραμμής κεφαλίδας** (π.χ., έντονη, χρώμα φόντου).  
- **Εφαρμογή υπό συνθήκες μορφοποίησης** χρησιμοποιώντας `Worksheet.Cells[i, j].ConditionalFormattingCollection`.  
- **Εξαγωγή σε άλλες μορφές** όπως CSV ή PDF με `wb.Save("file.pdf", SaveFormat.Pdf)`.  
- **Συνδυασμός πολλαπλών DataTables** σε ένα ενιαίο workbook, το καθένα σε δικό του φύλλο, χρησιμοποιώντας την ίδια προσέγγιση στυλ.

Αν αντιμετωπίσετε προβλήματα, αφήστε ένα σχόλιο ή ελέγξτε την επίσημη τεκμηρίωση του Aspose για το `ImportDataTable`. Καλή προγραμματιστική, και απολαύστε αυτά τα όμορφα μορφοποιημένα αρχεία Excel!

---

## Τι Πρέπει Να Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να Εισάγετε DataTable στο Excel Χρησιμοποιώντας Aspose.Cells για .NET (Βήμα‑Βήμα Οδηγός)](/cells/english/net/import-export/import-datatable-excel-aspose-cells-net/)
- [Πώς να Ορίσετε Στυλ Γραμματοσειράς στο Excel Χρησιμοποιώντας Aspose.Cells για .NET (Βήμα‑Βήμα Οδηγός)](/cells/english/net/formatting/aspose-cells-dotnet-set-font-styles-excel/)
- [Πώς να Εφαρμόσετε Σκιά Κειμένου στο Excel Χρησιμοποιώντας Aspose.Cells .NET: Βήμα‑Βήμα Οδηγός](/cells/english/net/formatting/apply-text-shadow-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}