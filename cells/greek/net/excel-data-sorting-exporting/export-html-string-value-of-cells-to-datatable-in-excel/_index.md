---
title: Εξαγωγή τιμής συμβολοσειράς HTML κελιών στον πίνακα δεδομένων στο Excel
linktitle: Εξαγωγή τιμής συμβολοσειράς HTML κελιών στον πίνακα δεδομένων στο Excel
second_title: Aspose.Cells .NET Excel Processing API
description: Μάθετε πώς να εξάγετε τιμές συμβολοσειράς HTML από κελιά Excel σε DataTable χρησιμοποιώντας το Aspose.Cells για .NET σε έναν απλό οδηγό βήμα προς βήμα.
weight: 11
url: /el/net/excel-data-sorting-exporting/export-html-string-value-of-cells-to-datatable-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή τιμής συμβολοσειράς HTML κελιών στον πίνακα δεδομένων στο Excel

## Εισαγωγή

Όταν εργάζεστε με αρχεία Excel σε περιβάλλον .NET, ενδέχεται να χρειαστεί να εξαγάγετε πληροφορίες από κελιά, όχι μόνο ως απλό κείμενο αλλά μάλλον ως συμβολοσειρές HTML. Αυτό μπορεί να είναι πολύ βολικό όταν έχετε να κάνετε με δεδομένα εμπλουτισμένου κειμένου ή όταν θέλετε να διατηρήσετε τη μορφοποίηση. Σε αυτόν τον οδηγό, θα σας καθοδηγήσω στην εξαγωγή της τιμής συμβολοσειράς HTML των κελιών σε έναν πίνακα δεδομένων χρησιμοποιώντας το Aspose.Cells για .NET. 

## Προαπαιτούμενα

Πριν βουτήξετε στον κώδικα, ας βεβαιωθούμε ότι έχετε όλα όσα χρειάζεστε στη θέση τους. Ακολουθεί μια γρήγορη λίστα ελέγχου:

1. Βασικές γνώσεις C# και .NET: Πριν προχωρήσετε στην κωδικοποίηση, βεβαιωθείτε ότι είστε εξοικειωμένοι με τον προγραμματισμό C# και τα βασικά του πλαισίου .NET.
2.  Aspose.Cells για .NET: Εάν δεν το έχετε κάνει ήδη, πρέπει να εγκαταστήσετε το Aspose.Cells για .NET. Μπορείτε να κάνετε λήψη μιας δωρεάν δοκιμής από[εδώ](https://releases.aspose.com/).
3. Visual Studio ή IDE της επιλογής σας: Ρυθμίστε το περιβάλλον σας για να γράψετε κώδικα C#. Το Visual Studio συνιστάται για το ευρύ φάσμα δυνατοτήτων και την ευκολία χρήσης του.
4. Δείγμα αρχείου Excel: Θα χρειαστείτε ένα δείγμα αρχείου Excel (`sampleExportTableAsHtmlString.xlsx`) για να εργαστείτε. Βεβαιωθείτε ότι βρίσκεται σε έναν κατάλογο που είναι προσβάσιμος.
5. NuGet Package Manager: Βεβαιωθείτε ότι έχετε πρόσβαση στο NuGet Package Manager στο έργο σας για να προσθέσετε εύκολα τη βιβλιοθήκη Aspose.Cells.

Με αυτά τα προαπαιτούμενα υπό έλεγχο, ας λερώσουμε τα χέρια μας με λίγη κωδικοποίηση!

## Εισαγωγή πακέτων

Για να μπορέσουμε να αρχίσουμε να εργαζόμαστε με το Aspose.Cells, πρέπει να εισάγουμε τα απαραίτητα πακέτα. Αυτό συνήθως περιλαμβάνει την προσθήκη του πακέτου Aspose.Cells NuGet στο έργο σας. Δείτε πώς να το κάνετε:

### Ανοίξτε το NuGet Package Manager

Στο Visual Studio, κάντε δεξί κλικ στο έργο σας στην Εξερεύνηση λύσεων και επιλέξτε Διαχείριση πακέτων NuGet.

### Αναζήτηση για Aspose.Cells

 Στο NuGet Package Manager, πληκτρολογήστε`Aspose.Cells` στη γραμμή αναζήτησης.

### Εγκαταστήστε το πακέτο

Μόλις βρείτε το Aspose.Cells, κάντε κλικ στο κουμπί Εγκατάσταση. Αυτό θα προσθέσει τη βιβλιοθήκη στο έργο σας και θα σας επιτρέψει να την εισαγάγετε στον κώδικά σας.

### Εισαγάγετε τον χώρο ονομάτων

Προσθέστε τα ακόλουθα χρησιμοποιώντας την οδηγία στην κορυφή του αρχείου κώδικα:

```csharp
using System;
using System.IO;
using Aspose.Cells;
using System.Data;
```

Τώρα που έχουμε ρυθμίσει τα πάντα, ας βουτήξουμε στη διαδικασία βήμα προς βήμα εξαγωγής τιμών συμβολοσειράς HTML από ένα αρχείο Excel σε έναν πίνακα δεδομένων. 

## Βήμα 1: Ορίστε τον κατάλογο προέλευσης

Θα ξεκινήσετε ορίζοντας τον κατάλογο όπου είναι αποθηκευμένο το δείγμα αρχείου Excel. Αυτό είναι κρίσιμο, καθώς λέει στην εφαρμογή σας πού να βρει το αρχείο. Εδώ είναι ο κωδικός για αυτό:

```csharp
string sourceDir = "Your Document Directory";
```

 Φροντίστε να αντικαταστήσετε`"Your Document Directory"` με την πραγματική διαδρομή προς το αρχείο Excel.

## Βήμα 2: Φορτώστε το δείγμα αρχείου Excel

 Το επόμενο βήμα είναι να φορτώσετε το βιβλίο εργασίας του Excel. Θα χρησιμοποιήσετε το`Workbook` κλάση από το Aspose.Cells για να το κάνετε αυτό. Δείτε πώς μπορείτε να φορτώσετε το αρχείο:

```csharp
Workbook wb = new Workbook(sourceDir + "sampleExportTableAsHtmlString.xlsx");
```

Αυτή η απλή γραμμή κώδικα προετοιμάζει το βιβλίο εργασίας και φορτώνει το καθορισμένο αρχείο Excel.

## Βήμα 3: Πρόσβαση στο Πρώτο φύλλο εργασίας

Μόλις φορτωθεί το βιβλίο εργασίας, θα θέλετε να αποκτήσετε πρόσβαση στο συγκεκριμένο φύλλο εργασίας που περιέχει τα δεδομένα που σας ενδιαφέρουν. Γενικά, θα ξεκινήσετε με το πρώτο φύλλο εργασίας:

```csharp
Worksheet ws = wb.Worksheets[0];
```

Εδώ, εργαζόμαστε με το πρώτο φύλλο εργασίας (ευρετήριο 0). Βεβαιωθείτε ότι τα δεδομένα σας βρίσκονται στο σωστό φύλλο.

## Βήμα 4: Καθορίστε τις Επιλογές πίνακα εξαγωγής

Για να ελέγξετε τον τρόπο εξαγωγής των δεδομένων, πρέπει να ρυθμίσετε`ExportTableOptions`. Σε αυτήν την περίπτωση, θέλετε να διασφαλίσετε ότι τα ονόματα των στηλών δεν εξάγονται και θέλετε τα δεδομένα κελιών να εξαχθούν ως συμβολοσειρές HTML:

```csharp
ExportTableOptions opts = new ExportTableOptions();
opts.ExportColumnName = false;
opts.ExportAsHtmlString = true;
```

Αυτή η διαμόρφωση σάς επιτρέπει να διατηρείτε την πλούσια μορφοποίηση των δεδομένων κυψέλης κατά την εξαγωγή.

## Βήμα 5: Εξαγωγή κελιών σε DataTable

 Τώρα έρχεται το κρίσιμο μέρος όπου εξάγετε πραγματικά τα δεδομένα. Χρησιμοποιώντας το`ExportDataTable` μέθοδο, μπορείτε να τραβήξετε τα δεδομένα από το φύλλο εργασίας σε α`DataTable`. Δείτε πώς να το κάνετε αυτό:

```csharp
DataTable dt = ws.Cells.ExportDataTable(0, 0, 3, 3, opts);
```

Αυτός ο κώδικας εξάγει μια καθορισμένη περιοχή κελιών (από τη σειρά 0, στήλη 0 έως τη σειρά 3, στήλη 3) σε έναν πίνακα δεδομένων χρησιμοποιώντας τις επιλογές που καθορίστηκαν προηγουμένως.

## Βήμα 6: Εκτυπώστε την τιμή συμβολοσειράς HTML

Τέλος, ας εκτυπώσουμε την τιμή συμβολοσειράς HTML από ένα συγκεκριμένο κελί στον πίνακα δεδομένων για να δούμε τι καταφέραμε να εξαγάγουμε. Για παράδειγμα, εάν θέλετε να εκτυπώσετε την τιμή από την τρίτη γραμμή και τη δεύτερη στήλη, θα κάνετε τα εξής:

```csharp
Console.WriteLine(dt.Rows[2][1].ToString());
```

Αυτή η γραμμή εκτυπώνει την επιθυμητή συμβολοσειρά HTML από τον πίνακα δεδομένων στην κονσόλα. 

## Σύναψη 

Και ορίστε το! Εξάγατε με επιτυχία τιμές συμβολοσειράς HTML από κελιά σε αρχείο Excel σε DataTable χρησιμοποιώντας το Aspose.Cells για .NET. Αυτή η δυνατότητα όχι μόνο εμπλουτίζει τις δεξιότητές σας στον χειρισμό δεδομένων, αλλά διευρύνει επίσης τις επιλογές σας όταν ασχολείστε με μορφοποιημένο περιεχόμενο απευθείας από αρχεία Excel. 

## Συχνές ερωτήσεις

### Μπορώ να χρησιμοποιήσω το Aspose.Cells για άλλες μορφές αρχείων εκτός από το Excel;  
Ναι, το Aspose.Cells είναι κυρίως για Excel, αλλά το Aspose προσφέρει άλλες βιβλιοθήκες για διαφορετικές μορφές.

### Χρειάζομαι άδεια για το Aspose.Cells;  
 Ναι, απαιτείται έγκυρη άδεια για παραγωγική χρήση. Μπορείτε να πάρετε μια προσωρινή άδεια[εδώ](https://purchase.aspose.com/temporary-license/).

### Τι γίνεται αν το αρχείο μου Excel περιέχει τύπους; Θα εξάγουν σωστά;  
Ναι, το Aspose.Cells μπορεί να χειριστεί τύπους και κατά την εξαγωγή, θα αξιολογηθούν στις προκύπτουσες τιμές τους.

### Είναι δυνατή η αλλαγή των επιλογών εξαγωγής;  
 Απολύτως! Μπορείτε να προσαρμόσετε`ExportTableOptions` για να ανταποκρίνεται στις συγκεκριμένες ανάγκες σας.

### Πού μπορώ να βρω πιο λεπτομερή τεκμηρίωση για το Aspose.Cells;  
 Μπορείτε να βρείτε εκτενή τεκμηρίωση[εδώ](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
