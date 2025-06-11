---
"description": "Μάθετε πώς να καθορίζετε HTML CrossType στο Aspose.Cells για .NET. Ακολουθήστε τον αναλυτικό οδηγό μας για να μετατρέψετε αρχεία Excel σε HTML με ακρίβεια."
"linktitle": "Καθορισμός HTML CrossType σε HTML εξόδου μέσω προγραμματισμού στο .NET"
"second_title": "API επεξεργασίας Excel Aspose.Cells .NET"
"title": "Καθορισμός HTML CrossType σε HTML εξόδου μέσω προγραμματισμού στο .NET"
"url": "/el/net/converting-excel-files-to-other-formats/specifying-html-crosstype-in-output-html/"
"weight": 17
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Καθορισμός HTML CrossType σε HTML εξόδου μέσω προγραμματισμού στο .NET

## Εισαγωγή
Όσον αφορά τη μετατροπή αρχείων Excel σε HTML σε εφαρμογές .NET, ίσως χρειαστεί να καθορίσετε τον τρόπο χειρισμού των διασταυρούμενων αναφορών στην έξοδο. Η κλάση HtmlSaveOptions στο Aspose.Cells για .NET παρέχει διάφορες ρυθμίσεις για τον έλεγχο της διαδικασίας μετατροπής και μία από αυτές τις επιλογές είναι το HtmlCrossType. Σε αυτό το σεμινάριο, θα δούμε πώς να καθορίσετε μέσω προγραμματισμού τον διασταυρούμενο τύπο HTML κατά την εξαγωγή αρχείων Excel σε μορφή HTML. 
## Προαπαιτούμενα
Πριν εμβαθύνετε στον κώδικα, βεβαιωθείτε ότι έχετε τα εξής:
- Aspose.Cells για .NET: Βεβαιωθείτε ότι έχετε εγκαταστήσει τη βιβλιοθήκη Aspose.Cells στο έργο σας. Μπορείτε να την κατεβάσετε από το [Ιστότοπος Aspose](https://releases.aspose.com/cells/net/).
- Visual Studio: Μια λειτουργική εγκατάσταση του Visual Studio ή οποιουδήποτε άλλου περιβάλλοντος ανάπτυξης .NET.
- Βασικές γνώσεις C#: Η εξοικείωση με τον προγραμματισμό C# θα σας βοηθήσει να κατανοήσετε καλύτερα τα παραδείγματα.
- Δείγμα αρχείου Excel: Να έχετε έτοιμο ένα δείγμα αρχείου Excel για να εργαστείτε. Για αυτό το παράδειγμα, θα χρησιμοποιήσουμε `sampleHtmlCrossStringType.xlsx`.
## Εισαγωγή πακέτων
Για να ξεκινήσετε, θα χρειαστεί να εισαγάγετε τους απαραίτητους χώρους ονομάτων Aspose.Cells. Δείτε πώς μπορείτε να το κάνετε:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Ας το αναλύσουμε βήμα προς βήμα, ώστε να σας διευκολύνουμε να παρακολουθήσετε και να εφαρμόσετε αυτήν τη λειτουργικότητα στα δικά σας έργα.
## Βήμα 1: Ορίστε τους καταλόγους προέλευσης και εξόδου
Αρχικά, πρέπει να ορίσετε τους καταλόγους για το αρχείο προέλευσης Excel και πού θέλετε να αποθηκεύσετε το αρχείο HTML εξόδου.
```csharp
// Κατάλογος πηγής
string sourceDir = "Your Document Directory";
// Κατάλογος εξόδου
string outputDir = "Your Document Directory";
```
## Βήμα 2: Φόρτωση του δείγματος αρχείου Excel
Στη συνέχεια, φορτώστε το δείγμα αρχείου Excel σε ένα `Workbook` αντικείμενο. Εδώ ξεκινάει όλη η μαγεία.
```csharp
// Φόρτωση του δείγματος αρχείου Excel
Workbook wb = new Workbook(sourceDir + "sampleHtmlCrossStringType.xlsx");
```
Εδώ, αντικαταστήστε `"Your Document Directory"` με την πραγματική διαδρομή όπου βρίσκεται το αρχείο Excel σας. Αυτή η γραμμή διαβάζει το αρχείο Excel στη μνήμη, ώστε να μπορείτε να το χειριστείτε.
## Βήμα 3: Καθορισμός επιλογών αποθήκευσης HTML
Τώρα, θα δημιουργήσουμε μια παρουσία του `HtmlSaveOptions`, το οποίο σας επιτρέπει να ρυθμίσετε τον τρόπο με τον οποίο το αρχείο Excel θα μετατραπεί σε HTML.
```csharp
// Καθορισμός τύπου HTML Cross
HtmlSaveOptions opts = new HtmlSaveOptions();
opts.HtmlCrossStringType = HtmlCrossType.Default;
```
Σε αυτό το βήμα, έχουμε ορίσει το `HtmlCrossStringType` να `HtmlCrossType.Default`, η οποία είναι μία από τις διαθέσιμες επιλογές για τον χειρισμό διασταυρούμενων αναφορών στην HTML εξόδου.
## Βήμα 4: Αλλάξτε τον τύπο σταυρού όπως απαιτείται
Μπορείτε να ορίσετε διαφορετικούς τύπους για `HtmlCrossStringType` με βάση τις απαιτήσεις σας. Ακολουθούν οι διάφορες επιλογές που μπορείτε να χρησιμοποιήσετε:
- `HtmlCrossType.Default`: Ο προεπιλεγμένος τύπος σταυρού.
- `HtmlCrossType.MSExport`Εξάγει τον κώδικα HTML με συμπεριφορά παρόμοια με αυτή του MS Excel.
- `HtmlCrossType.Cross`: Δημιουργεί διασταυρούμενες παραπομπές.
- `HtmlCrossType.FitToCell`Προσαρμόζει τις παραπομπές στις διαστάσεις των κελιών.
Μπορείτε να τροποποιήσετε το `HtmlCrossStringType` τοιουτοτροπώς:
```csharp
opts.HtmlCrossStringType = HtmlCrossType.MSExpήt;
// ή 
opts.HtmlCrossStringType = HtmlCrossType.Cross;
// or
opts.HtmlCrossStringType = HtmlCrossType.FitToCell;
```
## Βήμα 5: Αποθήκευση του αρχείου HTML εξόδου
Αφού διαμορφώσετε τις επιλογές σας, ήρθε η ώρα να αποθηκεύσετε το αρχείο HTML που έχει μετατραπεί. Χρησιμοποιήστε το `Save` μέθοδος στο δικό σας `Workbook` αντικείμενο:
```csharp
// Html εξόδου
wb.Save(outputDir + "out" + opts.HtmlCrossStringType + ".htm", opts);
```
Εδώ, ονομάζουμε το αρχείο εξόδου με βάση το `HtmlCrossStringType` έχουμε ορίσει. Με αυτόν τον τρόπο, μπορείτε εύκολα να προσδιορίσετε ποιος τύπος σταυρού χρησιμοποιήθηκε στη μετατροπή.
## Βήμα 6: Επιβεβαίωση επιτυχούς εκτέλεσης
Τέλος, είναι πάντα καλή πρακτική να επιβεβαιώνετε ότι η λειτουργία σας ήταν επιτυχής. Μπορείτε να εκτυπώσετε ένα μήνυμα στην κονσόλα:
```csharp
Console.WriteLine("SpecifyHtmlCrossTypeInOutputHTML executed successfully.\r\n");
```
Αυτό θα σας ενημερώσει ότι η διαδικασία ολοκληρώθηκε χωρίς σφάλματα.
## Σύναψη
Και να το! Έχετε καθορίσει με επιτυχία τον τύπο HTML για την εξαγωγή σας στο Excel στο .NET χρησιμοποιώντας το Aspose.Cells. Αυτή η λειτουργικότητα είναι ιδιαίτερα χρήσιμη όταν χρειάζεται να διατηρήσετε συγκεκριμένη μορφοποίηση ή αναφορές στην έξοδο HTML, διασφαλίζοντας ότι τα έγγραφα που έχετε μετατρέψει πληρούν τις απαιτήσεις σας.
## Συχνές ερωτήσεις
### Τι είναι το HtmlCrossType στο Aspose.Cells;  
Το HtmlCrossType ορίζει τον τρόπο χειρισμού των διασταυρούμενων αναφορών στο αρχείο Excel κατά τη μετατροπή HTML. Μπορείτε να επιλέξετε επιλογές όπως Default, MSExport, Cross και FitToCell.
### Μπορώ να χρησιμοποιήσω το Aspose.Cells δωρεάν;  
Το Aspose.Cells προσφέρει μια δωρεάν δοκιμαστική έκδοση. Μπορείτε να την κατεβάσετε από το [δικτυακός τόπος](https://releases.aspose.com/).
### Πώς μπορώ να εγκαταστήσω το Aspose.Cells στο έργο .NET μου;  
Μπορείτε να εγκαταστήσετε το Aspose.Cells μέσω του NuGet Package Manager στο Visual Studio εκτελώντας την εντολή: `Install-Package Aspose.Cells`.
### Πού μπορώ να βρω την τεκμηρίωση για το Aspose.Cells;  
Μπορείτε να βρείτε ολοκληρωμένη τεκμηρίωση στο Aspose.Cells [εδώ](https://reference.aspose.com/cells/net/).
### Τι πρέπει να κάνω εάν αντιμετωπίσω σφάλμα κατά την αποθήκευση του αρχείου HTML;  
Βεβαιωθείτε ότι οι διαδρομές καταλόγου είναι σωστές και ότι έχετε δικαιώματα εγγραφής για τον κατάλογο εξόδου. Εάν το πρόβλημα επιμένει, ανατρέξτε στο φόρουμ υποστήριξης του Aspose για βοήθεια.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}