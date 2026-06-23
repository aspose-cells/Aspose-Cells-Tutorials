---
category: general
date: 2026-03-30
description: Δημιουργήστε το κύριο φύλλο χρησιμοποιώντας το Aspose.Cells σε C#. Μάθετε
  πώς να δημιουργήσετε ένα βιβλίο εργασίας Excel σε C#, να επιτρέψετε διπλότυπα ονόματα
  φύλλων και να αποθηκεύσετε το βιβλίο εργασίας ως XLSX σε λίγα βήματα.
draft: false
keywords:
- create master sheet
- create excel workbook c#
- save workbook as xlsx
- allow duplicate sheet names
language: el
og_description: Δημιουργήστε κύριο φύλλο με το Aspose.Cells σε C#. Αυτός ο οδηγός
  δείχνει πώς να δημιουργήσετε ένα βιβλίο εργασίας Excel σε C#, να επιτρέψετε διπλά
  ονόματα φύλλων και να αποθηκεύσετε το βιβλίο εργασίας ως XLSX.
og_title: Δημιουργία κύριου φύλλου σε C# – Πλήρης οδηγός Aspose.Cells
tags:
- Aspose.Cells
- C#
- Excel automation
title: Δημιουργία κύριου φύλλου σε C# – Πλήρης οδηγός Aspose.Cells
url: /el/net/excel-workbook/create-master-sheet-in-c-complete-aspose-cells-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία κύριου φύλλου σε C# – Πλήρης Οδηγός Aspose.Cells

Έχετε ποτέ χρειαστεί να **create master sheet** σε ένα αρχείο Excel αλλά δεν ήσασταν σίγουροι πώς να διαχειριστείτε μια σειρά από φύλλα λεπτομερειών που μοιράζονται το ίδιο βασικό όνομα; Δεν είστε μόνοι. Σε πολλές περιπτώσεις αναφοράς καταλήγετε με δεκάδες καρτέλες λεπτομερειών, και η προεπιλεγμένη συμπεριφορά των περισσότερων βιβλιοθηκών είναι να πετάξει μια εξαίρεση όταν δύο φύλλα θα έχουν το ίδιο όνομα.  

Ευτυχώς, το Aspose.Cells κάνει πανεύκολο το **create master sheet**, τη διαμόρφωση της μηχανής για **allow duplicate sheet names**, και στη συνέχεια το **save workbook as XLSX**—όλα από καθαρό κώδικα C#. Σε αυτό το tutorial θα περάσουμε από ένα πλήρως εκτελέσιμο παράδειγμα, θα εξηγήσουμε γιατί κάθε γραμμή είναι σημαντική, και θα σας δώσουμε μια σειρά από συμβουλές που μπορείτε να αντιγράψετε απευθείας στα δικά σας έργα.

> **Τι θα αποκομίσετε**  
> * Πώς να **create Excel workbook C#**‑style χρησιμοποιώντας το Aspose.Cells.  
> * Πώς να ενσωματώσετε ένα smart‑marker που δημιουργεί ένα φύλλο λεπτομέρειας για κάθε γραμμή δεδομένων.  
> * Πώς να ορίσετε `DetailSheetNewName = DuplicateAllowed` ώστε η βιβλιοθήκη να προσθέτει αυτόματα αριθμητικό επίθημα.  
> * Πώς να **save workbook as XLSX** στο δίσκο χωρίς επιπλέον βήματα.

Δεν απαιτείται εξωτερική τεκμηρίωση—όλα όσα χρειάζεστε είναι εδώ.

---

## Προαπαιτούμενα

Πριν βουτήξουμε, βεβαιωθείτε ότι έχετε:

| Απαίτηση | Γιατί είναι σημαντικό |
|-------------|----------------|
| .NET 6.0 ή νεότερο (ή .NET Framework 4.7+) | Το Aspose.Cells 23.x+ στοχεύει σε αυτά τα runtime. |
| Visual Studio 2022 (ή οποιοδήποτε IDE C#) | Για εύκολη δημιουργία έργου και αποσφαλμάτωση. |
| Aspose.Cells for .NET NuGet package (`Install-Package Aspose.Cells`) | Η βιβλιοθήκη που τροφοδοτεί όλη τη μαγεία των smart‑marker. |
| Basic C# knowledge | Θα κατανοήσετε τη σύνταξη χωρίς εκπαιδευτικό μάθημα. |

Αν λείπει κάτι από αυτά, προσθέστε τα τώρα—δεν έχει νόημα να συνεχίσετε με ένα ημιτελές περιβάλλον.

---

## Βήμα 1: Δημιουργία κύριου φύλλου με Aspose.Cells

Το πρώτο που κάνουμε είναι **create Excel workbook C#** style δημιουργώντας ένα αντικείμενο `Workbook`. Αυτό το αντικείμενο περιέχει ήδη ένα προεπιλεγμένο φύλλο εργασίας, το οποίο θα μετονομάσουμε σε “Master” και θα το χρησιμοποιήσουμε ως πρότυπο για όλες τις σελίδες λεπτομερειών.

```csharp
using Aspose.Cells;

// Step 1: Initialise a new workbook – this automatically gives us one sheet
Workbook workbook = new Workbook();

// Grab the first (and only) worksheet that comes with a fresh workbook
Worksheet masterSheet = workbook.Worksheets[0];

// Give it a meaningful name – this will be our master sheet
masterSheet.Name = "Master";
```

*Γιατί να μετονομάσουμε το φύλλο;*  
Ένα προεπιλεγμένο όνομα όπως “Sheet1” δεν μεταδίδει πρόθεση, και αργότερα όταν ελέγχετε το αρχείο θα θέλετε την καρτέλα master να είναι άμεσα αναγνωρίσιμη. Η ονομασία επίσης αποτρέπει τυχαίες συγκρούσεις όταν προσθέτετε περισσότερα φύλλα.

## Βήμα 2: Προετοιμασία του smart‑marker που θα δημιουργεί φύλλα λεπτομερειών

Τα smart‑markers είναι placeholders που το Aspose.Cells αντικαθιστά με δεδομένα κατά την εκτέλεση. Τοποθετώντας `{{#detail:DataSheetName}}` στο κελί **A1**, λέμε στη μηχανή: “Για κάθε εγγραφή στην πηγή δεδομένων, δημιουργήστε ένα νέο φύλλο του οποίου το όνομα προέρχεται από το πεδίο `DataSheetName`.”

```csharp
// Step 2: Insert a smart‑marker into cell A1.
// The marker #detail tells Aspose.Cells to generate a new sheet per data row.
masterSheet.Cells["A1"].PutValue("{{#detail:DataSheetName}}");
```

Σκεφτείτε το marker ως μια μικρή κάρτα οδηγιών κολλημένη στο φύλλο εργασίας. Όταν εκτελείται ο επεξεργαστής, διαβάζει την κάρτα, τραβά την κατάλληλη τιμή από την πηγή δεδομένων, και στη συνέχεια κλωνοποιεί το κύριο φύλλο σε μια νέα καρτέλα.

## Βήμα 3: Δημιουργία της πηγής δεδομένων – σκόπιμα διπλότυπα ονόματα φύλλων

Στην πραγματική ζωή μπορεί να το αντλήσετε από μια βάση δεδομένων, αλλά για τη demo θα χρησιμοποιήσουμε έναν πίνακα μνήμης με ανώνυμα αντικείμενα. Παρατηρήστε ότι και τα δύο στοιχεία χρησιμοποιούν το ίδιο βασικό όνομα `"Detail"`· αυτό είναι το σενάριο όπου το **allow duplicate sheet names** γίνεται κρίσιμο.

```csharp
// Step 3: Create a data source with two items that share the same base sheet name.
var dataSource = new[]
{
    new { DataSheetName = "Detail" },
    new { DataSheetName = "Detail" }
};
```

Αν το δοκιμάζατε χωρίς ειδικές επιλογές, το Aspose.Cells θα έριχνε εξαίρεση στη δεύτερη επανάληψη επειδή υπάρχει ήδη ένα φύλλο με το όνομα “Detail”. Γι' αυτό το επόμενο βήμα είναι σημαντικό.

## Βήμα 4: Ενεργοποίηση διπλότυπων ονομάτων φύλλων

Το Aspose.Cells εκθέτει το `SmartMarkerOptions.DetailSheetNewName`. Ορίζοντάς το σε `DetailSheetNewName.DuplicateAllowed` λέτε στη μηχανή να προσθέτει αυτόματα αριθμητικό επίθημα (π.χ., “Detail_1”) όποτε συμβαίνει σύγκρουση ονομάτων.

```csharp
// Step 4: Configure SmartMarker options to permit duplicate sheet names.
var smartMarkerOptions = new SmartMarkerOptions
{
    // This makes the library rename clashes to "Detail_1", "Detail_2", etc.
    DetailSheetNewName = DetailSheetNewName.DuplicateAllowed
};
```

*Γιατί να μην δώσουμε σε κάθε γραμμή ένα μοναδικό όνομα χειροκίνητα;*  
Επειδή συχνά τα δεδομένα πηγής δεν εγγυώνται μοναδικότητα, ειδικά όταν οι χρήστες εισάγουν ελεύθερο κείμενο. Αφήνοντας τη βιβλιοθήκη να διαχειριστεί το επίθημα αφαιρεί μια ολόκληρη κατηγορία σφαλμάτων.

## Βήμα 5: Επεξεργασία των smart‑markers και δημιουργία των φύλλων λεπτομερειών

Τώρα καλούμε το `SmartMarkers.Process`, περνώντας τόσο την πηγή δεδομένων όσο και τις επιλογές που μόλις διαμορφώσαμε. Η μέθοδος περνάει από κάθε στοιχείο, κλωνοποιεί το κύριο φύλλο, και μετονομάζει το κλώνο σύμφωνα με το πεδίο `DataSheetName` (συμπεριλαμβανομένου ενός επιθήματος αν χρειάζεται).

```csharp
// Step 5: Run the smart‑marker processor – this creates the detail sheets.
masterSheet.SmartMarkers.Process(dataSource, smartMarkerOptions);
```

Μετά την εκτέλεση αυτής της γραμμής θα έχετε τρεις καρτέλες στο βιβλίο εργασίας:

1. **Master** – το αρχικό πρότυπο.  
2. **Detail** – το πρώτο παραγόμενο φύλλο (χωρίς επίθημα).  
3. **Detail_1** – το δεύτερο παραγόμενο φύλλο (επίθημα προστέθηκε αυτόματα).

Μπορείτε να το επαληθεύσετε ανοίγοντας το αρχείο στο Excel· θα δείτε τα δύο φύλλα λεπτομερειών δίπλα‑δίπλα.

## Βήμα 6: Αποθήκευση του βιβλίου εργασίας ως αρχείο XLSX

Τέλος, αποθηκεύουμε το αρχείο στο δίσκο. Η μέθοδος `Save` επιλέγει αυτόματα τη μορφή XLSX όταν της δίνετε μια επέκταση `.xlsx`.

```csharp
// Step 6: Persist the workbook – this is the moment we finally “save workbook as XLSX”.
string outputPath = @"C:\Temp\DuplicateDetailSheets.xlsx";
workbook.Save(outputPath);
```

**Pro tip:** Αν χρειάζεται να μεταδώσετε το αρχείο απευθείας σε απάντηση web (π.χ., ASP.NET Core), χρησιμοποιήστε `workbook.Save(stream, SaveFormat.Xlsx)` αντί για διαδρομή αρχείου.

## Πλήρες Παράδειγμα Εργασίας

Παρακάτω βρίσκεται το πλήρες, έτοιμο‑για‑εκτέλεση πρόγραμμα. Αντιγράψτε‑και‑επικολλήστε το σε μια εφαρμογή console, πατήστε F5, και ανοίξτε το παραγόμενο αρχείο για να δείτε το αποτέλεσμα.

```csharp
using System;
using Aspose.Cells;

namespace MasterSheetDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a new workbook and rename the default sheet to "Master"
            Workbook workbook = new Workbook();
            Worksheet masterSheet = workbook.Worksheets[0];
            masterSheet.Name = "Master";

            // 2️⃣ Insert a smart‑marker that will generate a detail sheet per data row
            masterSheet.Cells["A1"].PutValue("{{#detail:DataSheetName}}");

            // 3️⃣ Prepare a data source where two rows share the same sheet name
            var dataSource = new[]
            {
                new { DataSheetName = "Detail" },
                new { DataSheetName = "Detail" }
            };

            // 4️⃣ Allow duplicate sheet names – the library will add "_1", "_2", …
            var smartMarkerOptions = new SmartMarkerOptions
            {
                DetailSheetNewName = DetailSheetNewName.DuplicateAllowed
            };

            // 5️⃣ Process the smart‑markers; this creates the detail sheets
            masterSheet.SmartMarkers.Process(dataSource, smartMarkerOptions);

            // 6️⃣ Save the workbook as an XLSX file
            string outputPath = @"C:\Temp\DuplicateDetailSheets.xlsx";
            workbook.Save(outputPath);

            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

**Expected outcome:** Ανοίξτε το `DuplicateDetailSheets.xlsx` και θα δείτε τρία φύλλα εργασίας—`Master`, `Detail` και `Detail_1`. Κάθε φύλλο λεπτομέρειας είναι ακριβής αντίγραφο του κύριου, έτοιμο για να το γεμίσετε με δεδομένα συγκεκριμένων γραμμών αργότερα.

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

### Τι γίνεται αν χρειαστώ περισσότερα από δύο διπλότυπα φύλλα;

Κανένα πρόβλημα. Η ίδια ρύθμιση `DuplicateAllowed` θα συνεχίσει να προσθέτει αυξανόμενους αριθμούς (`Detail_2`, `Detail_3`, …) μέχρι κάθε γραμμή να έχει τη δική της καρτέλα.

### Μπορώ να προσαρμόσω τη μορφή του επιθήματος;

Από προεπιλογή, το Aspose.Cells χρησιμοποιεί μια υπογράμμιση ακολουθούμενη από αριθμητικό δείκτη. Αν χρειάζεστε διαφορετικό μοτίβο (π.χ., “Detail‑A”, “Detail‑B”), θα πρέπει να επεξεργαστείτε το βιβλίο εργασίας μετά την εκτέλεση του `Process`, διασχίζοντας το `workbook.Worksheets` και μετονομάζοντας όπως κρίνετε κατάλληλο.

### Λειτουργεί αυτή η προσέγγιση με μεγάλα σύνολα δεδομένων (εκατοντάδες γραμμές);

Ναι, αλλά προσέξτε τη χρήση μνήμης. Κάθε παραγόμενο φύλλο είναι πλήρες αντίγραφο του κύριου, έτσι ένας τεράστιος αριθμός γραμμών μπορεί να αυξήσει γρήγορα το μέγεθος του αρχείου. Αν χρειάζεστε μόνο λίγες γραμμές ανά φύλλο, σκεφτείτε τη χρήση του `SmartMarkerOptions.RemoveEmptyRows = true` για να αφαιρέσετε περιττά κελιά.

### Είναι το παραγόμενο αρχείο πραγματικά αρχείο XLSX;

Απόλυτα. Η μέθοδος `Save` γράφει το πακέτο Open XML που περιμένει το Excel. Μπορείτε ακόμη να ανοίξετε το αρχείο με LibreOffice ή Google Sheets χωρίς καμία μετατροπή.

## Συμβουλές για Κώδικα Έτοιμο για Παραγωγή

| Συμβουλή | Γιατί είναι σημαντικό |
|-----|----------------|
| **Dispose `Workbook

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}