---
"description": "Μάθετε να εισάγετε γραμμές DataTable στο Excel χωρίς να μετακινήσετε την πρώτη γραμμή προς τα κάτω χρησιμοποιώντας το Aspose.Cells για .NET. Οδηγός βήμα προς βήμα για εύκολη αυτοματοποίηση."
"linktitle": "Μετατόπιση της πρώτης γραμμής προς τα κάτω κατά την εισαγωγή γραμμών πίνακα δεδομένων στο Excel"
"second_title": "API επεξεργασίας Excel Aspose.Cells .NET"
"title": "Μετατόπιση της πρώτης γραμμής προς τα κάτω κατά την εισαγωγή γραμμών πίνακα δεδομένων στο Excel"
"url": "/el/net/excel-data-import-export/shift-first-row-down-when-inserting-cells-datatable-rows-in-excel/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Μετατόπιση της πρώτης γραμμής προς τα κάτω κατά την εισαγωγή γραμμών πίνακα δεδομένων στο Excel

## Εισαγωγή

Έχετε κουραστεί να μετακινείτε γραμμές χειροκίνητα κατά την εισαγωγή νέων δεδομένων στα υπολογιστικά φύλλα του Excel; Λοιπόν, είστε τυχεροί! Σε αυτό το άρθρο, θα εμβαθύνουμε στον τρόπο αυτοματοποίησης αυτής της διαδικασίας χρησιμοποιώντας το Aspose.Cells για .NET. Μέχρι το τέλος αυτού του σεμιναρίου, όχι μόνο θα μάθετε πώς να εργάζεστε με πίνακες δεδομένων στο Excel, αλλά και πώς να προσαρμόζετε τις επιλογές εισαγωγής ώστε να ταιριάζουν καλύτερα στις ανάγκες σας. Πιστέψτε με, αυτό μπορεί να σας εξοικονομήσει πολύ χρόνο και ταλαιπωρία! Πάρτε λοιπόν ένα φλιτζάνι καφέ και ας ξεκινήσουμε!

## Προαπαιτούμενα

Πριν προχωρήσουμε στην κωδικοποίηση, ας βεβαιωθούμε ότι έχετε ρυθμίσει τα πάντα:

1. Visual Studio: Βεβαιωθείτε ότι έχετε εγκατεστημένο το Visual Studio (το 2017 ή νεότερο θα πρέπει να λειτουργεί μια χαρά).
2. Aspose.Cells για .NET: Χρειάζεται να έχετε τη βιβλιοθήκη Aspose.Cells. Αν δεν το έχετε κάνει ακόμα, μπορείτε να την κατεβάσετε. [εδώ](https://releases.aspose.com/cells/net/).
3. Βασική Κατανόηση της C# και του Excel: Μια βασική κατανόηση του προγραμματισμού C# και του τρόπου λειτουργίας του Excel σίγουρα θα σας βοηθήσει να παρακολουθείτε πιο αποτελεσματικά.

Θα πρέπει επίσης να έχετε πρόχειρο ένα δείγμα αρχείου Excel. Σε αυτόν τον οδηγό, θα χρησιμοποιήσουμε ένα δείγμα που ονομάζεται `sampleImportTableOptionsShiftFirstRowDown.xlsx`Μπορείτε να δημιουργήσετε αυτό το αρχείο ή να βρείτε ένα πρότυπο που ταιριάζει στις ανάγκες σας.

## Εισαγωγή πακέτων

Πριν εμβαθύνουμε στον προγραμματισμό, πρέπει να βεβαιωθούμε ότι έχουμε εισάγει τα απαραίτητα πακέτα. Στο έργο σας σε C#, συμπεριλάβετε τους ακόλουθους χώρους ονομάτων:

```csharp
using System;
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

Αυτά τα πακέτα είναι απαραίτητα για την εργασία με το βιβλίο εργασίας, το φύλλο εργασίας και τους πίνακες.

## Βήμα 1: Ρύθμιση του έργου σας

### Δημιουργία νέου έργου C#

Ξεκινήστε δημιουργώντας μια νέα εφαρμογή κονσόλας C# στο Visual Studio. Δώστε στο έργο σας ένα κατάλληλο όνομα, όπως "ExcelDataImport".

### Προσθήκη πακέτου Aspose.Cells NuGet

Για να προσθέσετε το πακέτο Aspose.Cells, κάντε δεξί κλικ στο έργο σας στην Εξερεύνηση λύσεων, επιλέξτε Διαχείριση πακέτων NuGet και αναζητήστε το "Aspose.Cells". Εγκαταστήστε το πακέτο για να βεβαιωθείτε ότι έχετε πρόσβαση σε όλες τις λειτουργίες που χρειαζόμαστε.

## Βήμα 2: Ορισμός του Πίνακα Δεδομένων

Στη συνέχεια, θα εφαρμόσουμε το `ICellsDataTable` διεπαφή για να δημιουργήσετε μια κλάση που παρέχει τα δεδομένα που θα εισαχθούν. Δείτε πώς μπορείτε να δομήσετε την `CellsDataTable` τάξη:

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
    
    // ... Υλοποίηση άλλων μελών ...
}
```

Εδώ, ορίζουμε τα ονόματα των στηλών και τα δεδομένα για κάθε στήλη, κάτι που θα διευκολύνει τη δομή του εισαγόμενου πίνακά μας.

## Βήμα 3: Υλοποίηση μελών διεπαφής ICellsDataTable

Εντός του `CellsDataTable` κλάσης, πρέπει να εφαρμόσετε τα μέλη της `ICellsDataTable` διεπαφή. Ακολουθεί η απαιτούμενη υλοποίηση:

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

Αυτό το μέρος της κλάσης χειρίζεται την ανάκτηση δεδομένων, καθορίζοντας τον αριθμό των γραμμών και των στηλών που υπάρχουν και διαχειριζόμενο την τρέχουσα κατάσταση του ευρετηρίου.

## Βήμα 4: Γράψτε την κύρια συνάρτηση

Τώρα, ας δημιουργήσουμε το `Run` μέθοδος για την ενορχήστρωση ολόκληρης της διαδικασίας εισαγωγής πίνακα:

```csharp
public static void Run()
{
    string sourceDir = "Your Document Directory\\";
    string outputDir = "Your Document Directory\\";
    
    CellsDataTable cellsDataTable = new CellsDataTable();
    Workbook wb = new Workbook(sourceDir + "sampleImportTableOptionsShiftFirstRowDown.xlsx");
    Worksheet ws = wb.Worksheets[0];
```

## Βήμα 5: Ορισμός επιλογών εισαγωγής

Για να ελέγξετε τη συμπεριφορά εισαγωγής, θα πρέπει να δημιουργήσετε μια παρουσία του `ImportTableOptions` και ορίστε τις ιδιότητες ανάλογα. Συγκεκριμένα, θέλουμε να ορίσουμε `ShiftFirstRowDown` να `false`.

```csharp
    ImportTableOptions opts = new ImportTableOptions();
    opts.ShiftFirstRowDown = false; // Δεν θέλουμε να μετακινήσουμε την πρώτη σειρά προς τα κάτω
```

## Βήμα 6: Εισαγωγή του Πίνακα Δεδομένων

Τώρα μπορούμε να εισάγουμε τα δεδομένα από το `CellsDataTable` στο φύλλο εργασίας.

```csharp
    ws.Cells.ImportData(cellsDataTable, 2, 2, opts);
}
```

Αυτή η εντολή θα εισαγάγει απευθείας τον πίνακα δεδομένων σας ξεκινώντας από την καθορισμένη γραμμή και στήλη.

## Βήμα 7: Αποθήκευση του βιβλίου εργασίας

Τέλος, θα αποθηκεύσουμε το τροποποιημένο βιβλίο εργασίας σε ένα αρχείο:

```csharp
    wb.Save(outputDir + "outputImportTableOptionsShiftFirstRowDown-False.xlsx");
}
```

## Σύναψη

Και να το! Μάθατε πώς να εισάγετε γραμμές DataTable σε ένα φύλλο Excel χωρίς να μετακινήσετε την πρώτη γραμμή χρησιμοποιώντας το Aspose.Cells για .NET. Αυτή η διαδικασία όχι μόνο βελτιστοποιεί τον χειρισμό δεδομένων μέσα στο Excel, αλλά βελτιώνει και την απόδοση της εφαρμογής σας αυτοματοποιώντας μια συνήθως περίπλοκη εργασία. Με αυτές τις γνώσεις στο κιτ εργαλείων σας, είστε καλύτερα εξοπλισμένοι για να χειρίζεστε εργασίες αυτοματοποίησης του Excel, εξοικονομώντας σας χρόνο και προσπάθεια.

## Συχνές ερωτήσεις

### Τι είναι το Aspose.Cells για .NET;
Το Aspose.Cells για .NET είναι μια βιβλιοθήκη προγραμματισμού που επιτρέπει στους προγραμματιστές να δημιουργούν, να χειρίζονται και να μετατρέπουν αρχεία Excel σε εφαρμογές .NET.

### Χρειάζομαι άδεια χρήσης για να χρησιμοποιήσω το Aspose.Cells;
Ναι, θα χρειαστείτε μια έγκυρη άδεια χρήσης για όλες τις λειτουργίες. Ωστόσο, διατίθεται μια δωρεάν δοκιμαστική περίοδος για την αρχική δοκιμή.

### Μπορώ να χρησιμοποιήσω το Aspose.Cells σε εφαρμογές web;
Απολύτως! Το Aspose.Cells είναι ιδανικό για εφαρμογές για υπολογιστές, web και cloud που έχουν αναπτυχθεί σε .NET.

### Τι τύπους αρχείων Excel μπορώ να δημιουργήσω με το Aspose.Cells;
Μπορείτε να δημιουργήσετε μια ποικιλία μορφών αρχείων Excel, όπως XLSX, XLS, CSV και άλλα.

### Πού μπορώ να λάβω υποστήριξη για το Aspose.Cells;
Μπορείτε να κάνετε ερωτήσεις ή να βρείτε βοήθεια στο [Φόρουμ Aspose](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}