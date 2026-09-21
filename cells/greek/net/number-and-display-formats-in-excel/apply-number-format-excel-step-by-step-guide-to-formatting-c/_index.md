---
category: general
date: 2026-02-26
description: Εφαρμόστε γρήγορα μορφοποίηση αριθμών στο Excel και μάθετε πώς να μορφοποιήσετε
  μια στήλη ως νόμισμα, να ορίσετε τη μορφοποίηση αριθμών της στήλης και να ορίσετε
  το χρώμα γραμματοσειράς της στήλης με λίγες μόνο γραμμές C#.
draft: false
keywords:
- apply number format excel
- format column as currency
- set column number format
- format currency column
- set column font color
language: el
og_description: Εφαρμόστε μορφή αριθμού στο Excel με C# με εύκολα βήματα. Μάθετε πώς
  να μορφοποιήσετε μια στήλη ως νόμισμα, να ορίσετε τη μορφή αριθμού της στήλης και
  να ορίσετε το χρώμα γραμματοσειράς της στήλης για επαγγελματικά φύλλα εργασίας.
og_title: Εφαρμογή μορφοποίησης αριθμών στο Excel – Πλήρης οδηγός στυλ στηλών
tags:
- C#
- Excel
- Aspose.Cells
- DataTable
- Styling
title: Εφαρμογή μορφοποίησης αριθμών στο Excel – Οδηγός βήμα-βήμα για τη μορφοποίηση
  στηλών
url: /el/net/number-and-display-formats-in-excel/apply-number-format-excel-step-by-step-guide-to-formatting-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εφαρμογή μορφής αριθμού στο Excel – Πώς να μορφοποιήσετε στήλες Excel σε C#

Έχετε αναρωτηθεί ποτέ πώς να **apply number format excel** ενώ ήδη κάνετε επανάληψη σε ένα `DataTable`; Δεν είστε ο μόνος. Οι περισσότεροι προγραμματιστές συναντούν πρόβλημα όταν χρειάζονται μια κεφαλίδα με μπλε γραμματοσειρά *και* μια στήλη μορφοποιημένη ως νόμισμα στην ίδια λειτουργία εισαγωγής. Τα καλά νέα; Με λίγες γραμμές C# και τα σωστά αντικείμενα στυλ, μπορείτε να το κάνετε χωρίς μετα‑επεξεργασία του φύλλου.

Σε αυτό το tutorial θα περάσουμε από ένα πλήρες, εκτελέσιμο παράδειγμα που σας δείχνει πώς να **format column as currency**, **set column number format** για οποιαδήποτε άλλη στήλη, και ακόμη **set column font color** για τις κεφαλίδες. Στο τέλος θα έχετε ένα επαναχρησιμοποιήσιμο μοτίβο που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο Aspose.Cells (ή παρόμοιο).

## Τι θα μάθετε

- Πώς να ανακτήσετε ένα `DataTable` και να αντιστοιχίσετε κάθε στήλη σε ένα συγκεκριμένο `Style`.
- Τα ακριβή βήματα για **apply number format excel** χρησιμοποιώντας το `Worksheet.Cells.ImportDataTable`.
- Γιατί η δημιουργία στυλ εκ των προτέρων είναι πιο αποδοτική από τη μορφοποίηση των κελιών ένα‑ένα.
- Διαχείριση edge‑case όταν ο πίνακας προέλευσης έχει περισσότερες στήλες από αυτές που στυλιζάτε.
- Ένα πλήρες, έτοιμο για αντιγραφή‑και‑επικόλληση δείγμα κώδικα που μπορείτε να εκτελέσετε σήμερα.

> **Προαπαιτούμενο:** Αυτός ο οδηγός υποθέτει ότι έχετε το Aspose.Cells για .NET (ή οποιαδήποτε βιβλιοθήκη που εκθέτει τα API `Workbook`, `Worksheet`, `Style`) αναφορά στο έργο σας. Εάν χρησιμοποιείτε διαφορετική βιβλιοθήκη, οι έννοιες μεταφράζονται άμεσα—απλώς αντικαταστήστε τα ονόματα τύπων.

---

## Βήμα 1: Ανάκτηση των Πηγαίων Δεδομένων ως DataTable

Πριν γίνει οποιαδήποτε μορφοποίηση, χρειάζεστε τα ακατέργαστα δεδομένα. Στις περισσότερες πραγματικές περιπτώσεις τα δεδομένα βρίσκονται σε μια βάση δεδομένων, CSV ή API. Για λόγους σαφήνειας θα δημιουργήσουμε ένα απλό `DataTable` με δύο στήλες: *Product* (string) και *Price* (decimal).

```csharp
using System;
using System.Data;
using Aspose.Cells;
using System.Drawing;

public static DataTable GetData()
{
    var dt = new DataTable();
    dt.Columns.Add("Product", typeof(string));
    dt.Columns.Add("Price", typeof(decimal));

    dt.Rows.Add("Apple", 1.25m);
    dt.Rows.Add("Banana", 0.75m);
    dt.Rows.Add("Cherry", 2.10m);

    return dt;
}
```

> **Γιατί είναι σημαντικό:** Η μεταφορά των δεδομένων σε ένα `DataTable` σας παρέχει μια πινάκωση, αναπαράσταση στη μνήμη που το `ImportDataTable` μπορεί να καταναλώσει απευθείας, εξαλείφοντας την ανάγκη για χειροκίνητη εισαγωγή κελιού‑κατά‑κελί.

## Βήμα 2: Δημιουργία Πίνακα Στυλ – Ένα ανά Στήλη

Η υπερφόρτωση `ImportDataTable` που θα χρησιμοποιήσουμε δέχεται έναν πίνακα αντικειμένων `Style`. Κάθε στοιχείο αντιστοιχεί σε έναν δείκτη στήλης. Εάν αφήσετε ένα στοιχείο ως `null`, η στήλη κληρονομεί το προεπιλεγμένο στυλ του βιβλίου εργασίας.

```csharp
// Initialize the workbook (Aspose.Cells)
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];

// Prepare the style array based on the number of columns
DataTable dataTable = GetData();
Style[] columnStyles = new Style[dataTable.Columns.Count];
```

> **Συμβουλή:** Η δήλωση του πίνακα *μετά* το `DataTable` εξασφαλίζει ότι το μέγεθος ταιριάζει ακριβώς, αποτρέποντας `IndexOutOfRangeException` αργότερα.

## Βήμα 3: Ορισμός Χρώματος Γραμματοσειράς Στήλης (Μπλε) για την Πρώτη Στήλη

Ένα συχνό αίτημα είναι η επισήμανση των κεφαλίδων ή βασικών στηλών με ξεχωριστό χρώμα γραμματοσειράς. Εδώ κάνουμε το κείμενο της πρώτης στήλης μπλε.

```csharp
// Style for the first column – blue font
columnStyles[0] = workbook.CreateStyle();
columnStyles[0].Font.Color = Color.Blue;
```

> **Γιατί να χρησιμοποιήσετε αντικείμενο στυλ;** Τα στυλ είναι επαναχρησιμοποιήσιμα και εφαρμόζονται μαζικά, κάτι που είναι πολύ πιο γρήγορο από το να επαναλαμβάνετε κάθε κελί μετά την εισαγωγή. Το βιβλίο εργασίας αποθηκεύει το στυλ μία φορά και το επαναχρησιμοποιεί για κάθε κελί σε αυτή τη στήλη.

## Βήμα 4: Μορφοποίηση της Δεύτερης Στήλης ως Νόμισμα

Οι ενσωματωμένες μορφές αριθμών του Excel προσδιορίζονται με έναν δείκτη. Το `14` αντιστοιχεί στην προεπιλεγμένη μορφή νομίσματος (π.χ., `$1,234.00`). Εάν χρειάζεστε προσαρμοσμένη μορφή, μπορείτε να ορίσετε μια συμβολοσειρά μορφής αντί αυτού.

```csharp
// Style for the second column – built‑in currency format (ID 14)
columnStyles[1] = workbook.CreateStyle();
columnStyles[1].Number = 14; // 14 = built‑in currency format
```

> **Edge case:** Εάν το βιβλίο εργασίας σας χρησιμοποιεί μια τοπική ρύθμιση όπου το σύμβολο νομίσματος δεν είναι `$`, ο ίδιος δείκτης θα προσαρμοστεί αυτόματα (π.χ., `€` για γερμανικές τοπικές ρυθμίσεις).

## Βήμα 5: Εισαγωγή του DataTable με τα Ορισμένα Στυλ

Τώρα φέρνουμε όλα μαζί. Η μέθοδος `ImportDataTable` θα επικολλήσει τα δεδομένα ξεκινώντας από το κελί `A1` (γραμμή 0, στήλη 0) και θα εφαρμόσει τα στυλ που προετοιμάσαμε.

```csharp
// Import the DataTable into the worksheet, applying the column styles
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
```

- Η δεύτερη παράμετρος `true` λέει στο Aspose.Cells να θεωρήσει την πρώτη γραμμή του `DataTable` ως κεφαλίδες στηλών.
- Οι συντεταγμένες `0, 0` καθορίζουν την πάνω‑αριστερή γωνία όπου ξεκινά η εισαγωγή.
- `columnStyles` αντιστοιχίζει κάθε στήλη στο αντίστοιχο στυλ της.

## Βήμα 6: Αποθήκευση του Workbook (Προαιρετικό, αλλά Χρήσιμο για Επαλήθευση)

Εάν θέλετε να δείτε το αποτέλεσμα στο Excel, απλώς αποθηκεύστε το βιβλίο εργασίας στο δίσκο. Αυτό το βήμα δεν απαιτείται για τη λογική μορφοποίησης, αλλά είναι χρήσιμο για εντοπισμό σφαλμάτων.

```csharp
// Save the workbook to a file
workbook.Save("StyledReport.xlsx", SaveFormat.Xlsx);
Console.WriteLine("Workbook saved as StyledReport.xlsx");
```

### Αναμενόμενο Αποτέλεσμα

| **Προϊόν** (μπλε γραμματοσειρά) | **Τιμή** (νόμισμα) |
|--------------------------------|--------------------|
| Apple                          | $1.25              |
| Banana                         | $0.75              |
| Cherry                         | $2.10              |

- Η στήλη *Προϊόν* εμφανίζεται σε μπλε, κάνοντάς την να ξεχωρίζει.
- Η στήλη *Τιμή* εμφανίζει τις τιμές με το προεπιλεγμένο σύμβολο νομίσματος και δύο δεκαδικά ψηφία.

---

## Συχνές Ερωτήσεις & Παραλλαγές

### Πώς μπορώ να **set column number format** για περισσότερες από δύο στήλες;

Απλώς επεκτείνετε τον πίνακα `columnStyles`. Για παράδειγμα, για να εμφανίσετε ποσοστό στην τρίτη στήλη:

```csharp
columnStyles[2] = workbook.CreateStyle();
columnStyles[2].Number = 10; // 10 = built‑in percentage format
```

### Τι γίνεται αν χρειάζομαι μια *custom* μορφή νομίσματος, όπως “USD 1,234.00”?

Αντικαταστήστε την ιδιότητα `Number` με μια συμβολοσειρά μορφής:

```csharp
columnStyles[1].Custom = "\"USD\" #,##0.00";
```

### Μπορώ να εφαρμόσω ένα **set column font color** σε αριθμητική στήλη χωρίς να επηρεάσω τη μορφή αριθμού;

Απολύτως. Τα στυλ είναι συνδυάσιμα. Μπορείτε να ορίσετε τόσο `Font.Color` όσο και `Number` στην ίδια παρουσία `Style`:

```csharp
columnStyles[3] = workbook.CreateStyle();
columnStyles[3].Font.Color = Color.Green;
columnStyles[3].Number = 2; // 2 = built‑in date format (just an example)
```

### Τι συμβαίνει αν το `DataTable` έχει περισσότερες στήλες από τα στυλ;

Οποιαδήποτε στήλη χωρίς ρητό στυλ (`null` στοιχείο) θα κληρονομήσει το προεπιλεγμένο στυλ του βιβλίου εργασίας. Για να αποφύγετε τυχαία `null`, μπορείτε πρώτα να αρχικοποιήσετε ολόκληρο τον πίνακα με ένα βασικό στυλ:

```csharp
Style defaultStyle = workbook.CreateStyle();
defaultStyle.Font.Size = 11;
for (int i = 0; i < columnStyles.Length; i++)
    columnStyles[i] = defaultStyle;
```

Στη συνέχεια, αντικαταστήστε μόνο τις στήλες που σας ενδιαφέρουν.

### Λειτουργεί αυτή η προσέγγιση με μεγάλα σύνολα δεδομένων (10k+ γραμμές);

Ναι. Επειδή η μορφοποίηση εφαρμόζεται *μία φορά ανά στήλη* πριν την εισαγωγή, η λειτουργία παραμένει O(N) ως προς τις γραμμές και η χρήση μνήμης παραμένει χαμηλή. Αποφύγετε την επανάληψη σε κάθε κελί μετά την εισαγωγή—εκεί μειώνεται η απόδοση.

---

## Πλήρες Παράδειγμα Εργασίας (Έτοιμο για Αντιγραφή‑Επικόλληση)

```csharp
using System;
using System.Data;
using System.Drawing;
using Aspose.Cells;

class ExcelStyler
{
    static void Main()
    {
        // 1️⃣ Retrieve data
        DataTable dataTable = GetData();

        // 2️⃣ Create workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 3️⃣ Prepare style array (one per column)
        Style[] columnStyles = new Style[dataTable.Columns.Count];

        // 4️⃣ Style first column – blue font
        columnStyles[0] = workbook.CreateStyle();
        columnStyles[0].Font.Color = Color.Blue;

        // 5️⃣ Style second column – built‑in currency format (ID 14)
        columnStyles[1] = workbook.CreateStyle();
        columnStyles[1].Number = 14;

        // 6️⃣ (Optional) Add more styles here – e.g., percentage, custom formats

        // 7️⃣ Import the DataTable with styles
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

        // 8️⃣ Save to file for verification
        workbook.Save("StyledReport.xlsx", SaveFormat.Xlsx);
        Console.WriteLine("Excel file created: StyledReport.xlsx");
    }

    // Helper method to mock data
    public static DataTable GetData()
    {
        var dt = new DataTable();
        dt.Columns.Add("Product", typeof(string));
        dt.Columns.Add("Price", typeof(decimal));

        dt.Rows.Add("Apple", 1.25m);
        dt.Rows.Add("Banana", 0.75m);
        dt.Rows.Add("Cherry", 2.10m);
        return dt;
    }
}
```

Εκτελέστε το πρόγραμμα, ανοίξτε το `StyledReport.xlsx`, και θα δείτε άμεσα το αποτέλεσμα του **apply number format excel**.

---

## Συμπέρασμα

Δείξαμε μόλις μια καθαρή, αποδοτική μέθοδο για **apply number format excel** σε ένα εισαγόμενο `DataTable`. Προετοιμάζοντας έναν πίνακα `Style[]` εκ των προτέρων, μπορείτε να **format column as currency**, **set column number format**, και **set column font color** με μία κλήση—χωρίς ανάγκη μετα‑επεξεργασίας.  

Μη διστάσετε να επεκτείνετε το μοτίβο: προσθέστε υπό‑συνθήκη μορφοποίηση, συγχωνεύστε κελιά για κεφαλίδες, ή ακόμη ενσωματώστε τύπους. Οι ίδιες αρχές ισχύουν, διατηρώντας τον κώδικά σας τακτικό και τα φύλλα εργασίας σας επαγγελματικά.

### Τι θα ακολουθήσει;

- Εξερευνήστε **conditional formatting** για να επισημάνετε τιμές που υπερβαίνουν ένα όριο.
- Συνδυάστε αυτήν την τεχνική με **pivot table generation** για δυναμική αναφορά.
- Δοκιμάστε **setting column number format** για ημερομηνίες, ποσοστά ή προσαρμοσμένη επιστημονική σημειογραφία.

Έχετε μια παραλλαγή που δοκιμάσατε; Μοιραστείτε τη στα σχόλια—ας κρατήσουμε το

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}