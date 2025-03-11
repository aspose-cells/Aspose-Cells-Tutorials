---
title: Μετατόπιση της πρώτης σειράς προς τα κάτω κατά την εισαγωγή γραμμών του πίνακα δεδομένων στο Excel
linktitle: Μετατόπιση της πρώτης σειράς προς τα κάτω κατά την εισαγωγή γραμμών του πίνακα δεδομένων στο Excel
second_title: Aspose.Cells .NET Excel Processing API
description: Μάθετε να εισάγετε σειρές DataTable στο Excel χωρίς να μετακινείτε την πρώτη γραμμή προς τα κάτω χρησιμοποιώντας το Aspose.Cells για .NET. Οδηγός βήμα προς βήμα για αυτοματισμό χωρίς κόπο.
weight: 11
url: /el/net/excel-data-import-export/shift-first-row-down-when-inserting-cells-datatable-rows-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Μετατόπιση της πρώτης σειράς προς τα κάτω κατά την εισαγωγή γραμμών του πίνακα δεδομένων στο Excel

## Εισαγωγή

Έχετε βαρεθεί να αλλάζετε με μη αυτόματο τρόπο σειρές κατά την εισαγωγή νέων δεδομένων στα υπολογιστικά φύλλα του Excel; Λοιπόν, είσαι τυχερός! Σε αυτό το άρθρο, θα εξετάσουμε τον τρόπο αυτοματοποίησης αυτής της διαδικασίας χρησιμοποιώντας το Aspose.Cells για .NET. Μέχρι το τέλος αυτού του σεμιναρίου, όχι μόνο θα μάθετε πώς να εργάζεστε με πίνακες δεδομένων στο Excel, αλλά και πώς να προσαρμόζετε τις επιλογές εισαγωγής ώστε να ανταποκρίνονται καλύτερα στις ανάγκες σας. Πιστέψτε με. αυτό μπορεί να σας εξοικονομήσει πολύ χρόνο και ταλαιπωρία! Λοιπόν, πιείτε ένα φλιτζάνι καφέ και ας ξεκινήσουμε!

## Προαπαιτούμενα

Πριν προχωρήσουμε στην κωδικοποίηση, ας βεβαιωθούμε ότι έχετε ρυθμίσει τα πάντα:

1. Visual Studio: Βεβαιωθείτε ότι έχετε εγκαταστήσει το Visual Studio (2017 ή νεότερο θα πρέπει να λειτουργεί μια χαρά).
2.  Aspose.Cells για .NET: Πρέπει να έχετε τη βιβλιοθήκη Aspose.Cells. Εάν δεν το έχετε κάνει ακόμα, μπορείτε να το κατεβάσετε[εδώ](https://releases.aspose.com/cells/net/).
3. Βασική κατανόηση της C# και του Excel: Η βασική κατανόηση του προγραμματισμού C# και του τρόπου λειτουργίας του Excel σίγουρα θα σας βοηθήσει να ακολουθήσετε πιο αποτελεσματικά.

 Θα θελήσετε επίσης να έχετε πρόχειρο ένα δείγμα αρχείου Excel. Σε αυτόν τον οδηγό, θα χρησιμοποιήσουμε ένα δείγμα που ονομάζεται`sampleImportTableOptionsShiftFirstRowDown.xlsx`. Μπορείτε να δημιουργήσετε αυτό το αρχείο ή να βρείτε ένα πρότυπο που ταιριάζει στις ανάγκες σας.

## Εισαγωγή πακέτων

Πριν ξεκινήσουμε την κωδικοποίηση, πρέπει να βεβαιωθούμε ότι εισάγουμε τα απαραίτητα πακέτα. Στο έργο σας C#, συμπεριλάβετε τους ακόλουθους χώρους ονομάτων:

```csharp
using System;
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

Αυτά τα πακέτα είναι απαραίτητα για την εργασία με το βιβλίο εργασίας, το φύλλο εργασίας και τους πίνακες.

## Βήμα 1: Ρύθμιση του έργου σας

### Δημιουργήστε ένα νέο έργο C#

Ξεκινήστε δημιουργώντας μια νέα εφαρμογή C# Console στο Visual Studio. Δώστε στο έργο σας ένα κατάλληλο όνομα, όπως "ExcelDataImport".

### Προσθέστε το πακέτο Aspose.Cells NuGet

Για να προσθέσετε το πακέτο Aspose.Cells, κάντε δεξί κλικ στο έργο σας στην Εξερεύνηση λύσεων, επιλέξτε Manage NuGet Packages και αναζητήστε το "Aspose.Cells". Εγκαταστήστε το πακέτο για να βεβαιωθείτε ότι έχετε πρόσβαση σε όλες τις λειτουργίες που χρειαζόμαστε.

## Βήμα 2: Ορίστε τον πίνακα δεδομένων

 Στη συνέχεια, θα εφαρμόσουμε το`ICellsDataTable` διεπαφή για τη δημιουργία μιας κλάσης που παρέχει τα προς εισαγωγή δεδομένα. Δείτε πώς μπορείτε να δομήσετε το`CellsDataTable` τάξη:

```csharp
class CellsDataTable : ICellsDataTable
{
    int m_index = -1;
    static String[] colsNames = new String[] { "Pet", "Fruit", "Country", "Color" };
    static String[] col0data = new String[] { "Dog", "Cat", "Duck" };
    static String[] col1data = new String[] { "Apple", "Pear", "Banana" };
    static String[] col2data = new String[] { "UK", "USA", "China" };
    static String[] col3data = new String[] { "Red", "Green", "Blue" };
    static String[][] colsData = new String[][] { col0data, col1data, col2data, col3data };
    
    // ... Εφαρμογή άλλων μελών ...
}
```

Εδώ, ορίζουμε τα ονόματα στηλών και τα δεδομένα για κάθε στήλη, τα οποία θα διευκολύνουν τη δομή του εισαγόμενου πίνακα μας.

## Βήμα 3: Εφαρμογή μελών διεπαφής ICEllsDataTable

 Μέσα στο`CellsDataTable` τάξη, πρέπει να εφαρμόσετε τα μέλη του`ICellsDataTable` διεπαφή. Ακολουθεί η απαιτούμενη υλοποίηση:

```csharp
public object this[string columnName]
{
    get
    {
        throw new NotImplementedException();
    }
}

object ICellsDataTable.this[int columnIndex]
{
    get
    {
        return colsData[columnIndex][m_index];
    }
}

string[] ICellsDataTable.Columns
{
    get { return colsNames; }
}

int ICellsDataTable.Count
{
    get { return col0data.Length; }
}

void ICellsDataTable.BeforeFirst()
{
    m_index = -1;
}

bool ICellsDataTable.Next()
{
    m_index++;
    return (m_index < Count);
}
```

Αυτό το τμήμα της κλάσης χειρίζεται την ανάκτηση δεδομένων, καθορίζει πόσες γραμμές και στήλες υπάρχουν και διαχειρίζεται την τρέχουσα κατάσταση ευρετηρίου.

## Βήμα 4: Γράψτε την κύρια συνάρτηση

 Τώρα, ας δημιουργήσουμε το`Run`μέθοδος για την ενορχήστρωση ολόκληρης της διαδικασίας εισαγωγής πίνακα:

```csharp
public static void Run()
{
    string sourceDir = "Your Document Directory\\";
    string outputDir = "Your Document Directory\\";
    
    CellsDataTable cellsDataTable = new CellsDataTable();
    Workbook wb = new Workbook(sourceDir + "sampleImportTableOptionsShiftFirstRowDown.xlsx");
    Worksheet ws = wb.Worksheets[0];
```

## Βήμα 5: Ορίστε τις επιλογές εισαγωγής

 Για να ελέγξετε τη συμπεριφορά εισαγωγής, θα πρέπει να δημιουργήσετε μια παρουσία του`ImportTableOptions` και ορίστε τις ιδιότητες ανάλογα. Συγκεκριμένα, θέλουμε να ορίσουμε`ShiftFirstRowDown` να`false`.

```csharp
    ImportTableOptions opts = new ImportTableOptions();
    opts.ShiftFirstRowDown = false; // Δεν θέλουμε να μετατοπίσουμε την πρώτη σειρά προς τα κάτω
```

## Βήμα 6: Εισαγάγετε τον πίνακα δεδομένων

 Τώρα μπορούμε να εισάγουμε τα δεδομένα από το δικό μας`CellsDataTable` στο φύλλο εργασίας.

```csharp
    ws.Cells.ImportData(cellsDataTable, 2, 2, opts);
}
```

Αυτή η εντολή θα εισαγάγει απευθείας τον πίνακα δεδομένων σας ξεκινώντας από την καθορισμένη γραμμή και στήλη.

## Βήμα 7: Αποθηκεύστε το βιβλίο εργασίας

Τέλος, θα αποθηκεύσουμε το τροποποιημένο βιβλίο εργασίας σε ένα αρχείο:

```csharp
    wb.Save(outputDir + "outputImportTableOptionsShiftFirstRowDown-False.xlsx");
}
```

## Σύναψη

Και ορίστε το! Έχετε μάθει πώς να εισάγετε σειρές DataTable σε ένα φύλλο Excel χωρίς να μετακινήσετε την πρώτη σειρά χρησιμοποιώντας το Aspose.Cells για .NET. Αυτή η διαδικασία όχι μόνο απλοποιεί τον χειρισμό δεδομένων εντός του Excel, αλλά βελτιώνει επίσης την απόδοση της εφαρμογής σας αυτοματοποιώντας μια συνήθως δυσκίνητη εργασία. Με αυτή τη γνώση στην εργαλειοθήκη σας, είστε καλύτερα εξοπλισμένοι για να χειρίζεστε εργασίες αυτοματισμού του Excel, εξοικονομώντας χρόνο και προσπάθεια.

## Συχνές ερωτήσεις

### Τι είναι το Aspose.Cells για .NET;
Το Aspose.Cells για .NET είναι μια βιβλιοθήκη προγραμματισμού που επιτρέπει στους προγραμματιστές να δημιουργούν, να χειρίζονται και να μετατρέπουν αρχεία Excel σε εφαρμογές .NET.

### Χρειάζομαι άδεια χρήσης για να χρησιμοποιήσω το Aspose.Cells;
Ναι, θα χρειαστείτε έγκυρη άδεια για πλήρη χαρακτηριστικά. Ωστόσο, είναι διαθέσιμη μια δωρεάν δοκιμή για αρχική δοκιμή.

### Μπορώ να χρησιμοποιήσω το Aspose.Cells σε εφαρμογές web;
Απολύτως! Το Aspose.Cells είναι τέλειο για επιτραπέζιους υπολογιστές, web και εφαρμογές που βασίζονται σε cloud που έχουν αναπτυχθεί στο .NET.

### Τι τύπους αρχείων Excel μπορώ να δημιουργήσω με το Aspose.Cells;
Μπορείτε να δημιουργήσετε μια ποικιλία μορφών αρχείων Excel, συμπεριλαμβανομένων των XLSX, XLS, CSV και άλλων.

### Πού μπορώ να λάβω υποστήριξη για το Aspose.Cells;
 Μπορείτε να κάνετε ερωτήσεις ή να βρείτε βοήθεια στο[Aspose φόρουμ](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
