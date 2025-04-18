---
title: Συγκεντρωτικός πίνακας Προσαρμοσμένη ταξινόμηση μέσω προγραμματισμού σε .NET
linktitle: Συγκεντρωτικός πίνακας Προσαρμοσμένη ταξινόμηση μέσω προγραμματισμού σε .NET
second_title: Aspose.Cells .NET Excel Processing API
description: Μάθετε πώς να ταξινομείτε μέσω προγραμματισμού Συγκεντρωτικούς Πίνακες στο .NET χρησιμοποιώντας το Aspose.Cells. Ένας οδηγός βήμα προς βήμα που καλύπτει τη ρύθμιση, τη διαμόρφωση, την ταξινόμηση και την αποθήκευση των αποτελεσμάτων ως αρχεία Excel και PDF.
weight: 29
url: /el/net/creating-and-configuring-pivot-tables/pivot-table-custom-sort/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Συγκεντρωτικός πίνακας Προσαρμοσμένη ταξινόμηση μέσω προγραμματισμού σε .NET

## Εισαγωγή
Όταν πρόκειται για εργασία με το Excel σε περιβάλλον .NET, μια βιβλιοθήκη ξεχωρίζει μεταξύ των υπολοίπων: Aspose.Cells. Τώρα, δεν σας αρέσει όταν ένα εργαλείο σας επιτρέπει να χειρίζεστε υπολογιστικά φύλλα μέσω προγραμματισμού; Αυτό ακριβώς κάνει το Aspose.Cells! Στο σημερινό σεμινάριο, βουτάμε βαθιά στον κόσμο των Συγκεντρωτικών πινάκων και σας δείχνουμε πώς να εφαρμόσετε προσαρμοσμένη ταξινόμηση μέσω προγραμματισμού χρησιμοποιώντας αυτήν την ευέλικτη βιβλιοθήκη.
## Προαπαιτούμενα
Πριν σηκώσουμε τα μανίκια και πηδήξουμε στον κωδικό, βεβαιωθείτε ότι έχετε ορισμένα πράγματα στη θέση τους:
1. Visual Studio: Θα χρειαστείτε μια λειτουργική έκδοση του Visual Studio. Είναι η παιδική χαρά όπου συμβαίνει όλη η μαγεία.
2. .NET Framework: Η εξοικείωση με τον προγραμματισμό .NET είναι απαραίτητη. Είτε είστε λάτρης του .NET Core είτε του .NET Framework, είστε έτοιμοι.
3.  Aspose.Cells Library: Πρέπει να εγκαταστήσετε τη βιβλιοθήκη Aspose.Cells. Μπορείτε να το πάρετε από το[Σύνδεσμος λήψης](https://releases.aspose.com/cells/net/) και προσθέστε το στο έργο σας.
4. Βασική κατανόηση των συγκεντρωτικών πινάκων: Αν και δεν χρειάζεται να είστε ειδικός, λίγη γνώση σχετικά με τον τρόπο λειτουργίας των Συγκεντρωτικών πινάκων θα είναι ωφέλιμη καθώς εξετάζουμε αυτό το σεμινάριο.
5.  Δείγμα αρχείου Excel: Έχετε ένα δείγμα αρχείου Excel με το όνομα`SamplePivotSort.xlsx` έτοιμο στον κατάλογο εργασίας σας για δοκιμή.
## Εισαγωγή πακέτων
Αφού ταξινομήσετε όλες τις προϋποθέσεις, το πρώτο βήμα είναι να εισαγάγετε τα απαραίτητα πακέτα. Για να το κάνετε αυτό, συμπεριλάβετε τις ακόλουθες γραμμές στην κορυφή του κώδικά σας:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells;
using Aspose.Cells.Pivot;
```
Αυτό το πακέτο παρέχει όλες τις λειτουργίες που χρειάζεστε για τον χειρισμό αρχείων Excel χρησιμοποιώντας το Aspose.Cells.

Εντάξει, ας μπούμε στο διασκεδαστικό κομμάτι! Θα αναλύσουμε τη διαδικασία δημιουργίας συγκεντρωτικού πίνακα και εφαρμογής προσαρμοσμένης ταξινόμησης σε διαχειρίσιμα βήματα.
## Βήμα 1: Ρυθμίστε το βιβλίο εργασίας
Για να ξεκινήσουμε τα πράγματα, πρέπει να ρυθμίσουμε το βιβλίο εργασίας μας. Δείτε πώς το κάνετε:
```csharp
string sourceDir = "Your Document Directory";
string outputDir = "Your Document Directory";
Workbook wb = new Workbook(sourceDir + "SamplePivotSort.xlsx");
```
 Σε αυτό το βήμα, αρχικοποιούμε ένα νέο`Workbook` παράδειγμα με τη διαδρομή προς το αρχείο μας Excel. Αυτό λειτουργεί ως ο καμβάς όπου το Pivot Table μας θα ζωντανέψει.
## Βήμα 2: Πρόσβαση στο φύλλο εργασίας
Στη συνέχεια, πρέπει να αποκτήσουμε πρόσβαση στο φύλλο εργασίας όπου θα προσθέσουμε τον Συγκεντρωτικό Πίνακα.
```csharp
Worksheet sheet = wb.Worksheets[0];
PivotTableCollection pivotTables = sheet.PivotTables;
```
 Εδώ, αρπάζουμε το πρώτο φύλλο εργασίας στο βιβλίο εργασίας μας και καλούμε το`PivotTableCollection`. Αυτή η συλλογή μας επιτρέπει να διαχειριζόμαστε όλους τους Συγκεντρωτικούς Πίνακες σε αυτό το φύλλο εργασίας.
## Βήμα 3: Δημιουργήστε τον πρώτο σας συγκεντρωτικό πίνακα
Τώρα ήρθε η ώρα να δημιουργήσουμε τον Συγκεντρωτικό Πίνακά μας.
```csharp
int index = pivotTables.Add("=Sheet1!A1:C10", "E3", "PivotTable1");
PivotTable pivotTable = pivotTables[index];
```
Προσθέτουμε έναν νέο Συγκεντρωτικό Πίνακα στο φύλλο εργασίας μας, καθορίζοντας το εύρος δεδομένων και τη θέση του. Το "E3" υποδεικνύει πού θέλουμε να ξεκινήσει ο Συγκεντρωτικός Πίνακάς μας. Στη συνέχεια, αναφερόμαστε σε αυτόν τον νέο Συγκεντρωτικό Πίνακα χρησιμοποιώντας το ευρετήριό του.
## Βήμα 4: Διαμορφώστε τις Ρυθμίσεις Συγκεντρωτικού Πίνακα
Ας διαμορφώσουμε τον Συγκεντρωτικό Πίνακά μας! Αυτό σημαίνει τον έλεγχο πτυχών όπως τα μεγάλα σύνολα και οι διευθετήσεις πεδίου.
```csharp
pivotTable.RowGrand = false;
pivotTable.ColumnGrand = false;
pivotTable.AddFieldToArea(PivotFieldType.Row,1);
PivotField rowField = pivotTable.RowFields[0];
rowField.IsAutoSort = true;
rowField.IsAscendSort = true;
```
Διασφαλίζουμε ότι τα συνολικά σύνολα για γραμμές και στήλες δεν εμφανίζονται, γεγονός που μπορεί να κάνει τα δεδομένα πιο καθαρά. Στη συνέχεια, προσθέτουμε το πρώτο πεδίο στην περιοχή της γραμμής, ενεργοποιώντας την αυτόματη ταξινόμηση και μια αύξουσα ταξινόμηση.
## Βήμα 5: Προσθήκη πεδίων στήλης και δεδομένων
Αφού οριστούν οι σειρές, ας προσθέσουμε τα πεδία στήλης και δεδομένων.
```csharp
pivotTable.AddFieldToArea(PivotFieldType.Column,0);
PivotField colField = pivotTable.ColumnFields[0];
colField.NumberFormat = "dd/mm/yyyy";
colField.IsAutoSort = true;
colField.IsAscendSort = true;
```
Προσθέτουμε το δεύτερο πεδίο ως στήλη και το μορφοποιούμε ως ημερομηνία. Και πάλι, ενεργοποιούμε την αυτόματη ταξινόμηση και αύξουσα σειρά για να κρατάμε τα πράγματα οργανωμένα. Τέλος, πρέπει να προσθέσουμε το τρίτο πεδίο στην περιοχή δεδομένων μας:
```csharp
pivotTable.AddFieldToArea(PivotFieldType.Data,2);
```
## Βήμα 6: Ανανεώστε και υπολογίστε τον Συγκεντρωτικό Πίνακα
Αφού προσθέσουμε όλα τα απαραίτητα πεδία, ας βεβαιωθούμε ότι ο Συγκεντρωτικός Πίνακας είναι φρέσκος και έτοιμος.
```csharp
pivotTable.RefreshData();
pivotTable.CalculateData();
```
Αυτές οι μέθοδοι ανανεώνουν τα δεδομένα και τα υπολογίζουν εκ νέου, διασφαλίζοντας ότι όλα είναι ενημερωμένα και εμφανίζονται σωστά στον Συγκεντρωτικό Πίνακα.
## Βήμα 7: Προσαρμοσμένη ταξινόμηση με βάση τις τιμές πεδίων γραμμής
Ας προσθέσουμε λίγη αίσθηση ταξινομώντας τον Συγκεντρωτικό Πίνακα με βάση συγκεκριμένες τιμές, όπως "Θαλασσινά".
```csharp
index = pivotTables.Add("=Sheet1!A1:C10", "E10", "PivotTable2");
pivotTable = pivotTables[index];
```
Επαναλαμβάνουμε τη διαδικασία δημιουργώντας έναν άλλο Συγκεντρωτικό Πίνακα και ρυθμίζοντας τον παρόμοια με τον πρώτο. Μπορούμε τώρα να το προσαρμόσουμε περαιτέρω:
```csharp
pivotTable.AddFieldToArea(PivotFieldType.Row,1);
rowField = pivotTable.RowFields[0];
rowField.IsAutoSort = true;
rowField.IsAscendSort = true;
```
## Βήμα 8: Πρόσθετη προσαρμογή ταξινόμησης Ας δοκιμάσουμε μια άλλη μέθοδο ταξινόμησης με βάση μια συγκεκριμένη ημερομηνία:
```csharp
// Προσθήκη άλλου Συγκεντρωτικού Πίνακα για ταξινόμηση κατά ημερομηνία
index = pivotTables.Add("=Sheet1!A1:C10", "E18", "PivotTable3");
pivotTable = pivotTables[index];
// Επαναλάβετε τις ρυθμίσεις σειρών και στηλών παρόμοιες με τα προηγούμενα βήματα
```
Απλώς επαναλαμβάνετε την ίδια διαδικασία, δημιουργώντας έναν τρίτο Συγκεντρωτικό Πίνακα με τα κριτήρια ταξινόμησης προσαρμοσμένα στις ανάγκες σας.
## Βήμα 9: Αποθηκεύστε το WorkbookTime για να αποθηκεύσετε όλη τη σκληρή δουλειά που έχουμε καταβάλει!
```csharp
wb.Save(outputDir + "out.xlsx");
PdfSaveOptions options = new PdfSaveOptions();
options.OnePagePerSheet = true;
wb.Save(outputDir + "out.pdf", options);
```
 Εδώ, αποθηκεύετε το βιβλίο εργασίας ως αρχείο Excel και PDF. Ο`PdfSaveOptions` επιτρέπει την καλύτερη μορφοποίηση, διασφαλίζοντας ότι κάθε φύλλο εμφανίζεται σε ξεχωριστή σελίδα κατά τη μετατροπή.
## Βήμα 10: Ολοκλήρωση Αναδιπλώστε τα όλα, ενημερώνοντας τον χρήστη ότι όλα είναι καλά.
```csharp
Console.WriteLine("PivotTableCustomSort executed successfully.");
```
## Σύναψη
Μέχρι τώρα, έχετε μάθει πώς να αξιοποιείτε τη δύναμη του Aspose.Cells για να δημιουργείτε και να προσαρμόζετε Συγκεντρωτικούς Πίνακες στις εφαρμογές σας .NET. Από την αρχική ρύθμιση έως την προσαρμοσμένη ταξινόμηση, κάθε βήμα συνδυάζεται για να προσφέρει μια απρόσκοπτη εμπειρία. Είτε θέλετε να παρουσιάσετε στοιχεία ετήσιων πωλήσεων είτε να παρακολουθείτε στατιστικά αποθέματος, αυτές οι δεξιότητες θα σας εξυπηρετήσουν καλά!
## Συχνές ερωτήσεις
### Τι είναι ο Συγκεντρωτικός Πίνακας;
Ο Συγκεντρωτικός Πίνακας είναι ένα εργαλείο επεξεργασίας δεδομένων στο Excel που σας επιτρέπει να συνοψίζετε και να αναλύετε δεδομένα, παρέχοντας έναν ευέλικτο τρόπο για εύκολη εξαγωγή πληροφοριών.
### Πώς μπορώ να εγκαταστήσω το Aspose.Cells;
 Μπορείτε να το εγκαταστήσετε μέσω του NuGet στο Visual Studio ή να το κατεβάσετε απευθείας από το[Σύνδεσμος λήψης](https://releases.aspose.com/cells/net/).
### Υπάρχει δοκιμαστική έκδοση του Aspose.Cells;
 Ναί! Μπορείτε να το δοκιμάσετε δωρεάν επισκεπτόμενοι το[Δωρεάν δοκιμαστικός σύνδεσμος](https://releases.aspose.com/).
### Μπορώ να ταξινομήσω πολλά πεδία σε έναν Συγκεντρωτικό Πίνακα;
Απολύτως! Μπορείτε να προσθέσετε και να ταξινομήσετε πολλά πεδία με βάση τις απαιτήσεις σας.
### Πού μπορώ να βρω υποστήριξη για το Aspose.Cells;
 Η κοινότητα είναι αρκετά ενεργή και μπορείτε να κάνετε ερωτήσεις στο φόρουμ τους[εδώ](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
