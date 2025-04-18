---
title: Ανίχνευση κυκλικής αναφοράς στο Excel μέσω προγραμματισμού
linktitle: Ανίχνευση κυκλικής αναφοράς στο Excel μέσω προγραμματισμού
second_title: Aspose.Cells .NET Excel Processing API
description: Εντοπίστε εύκολα κυκλικές αναφορές στο Excel χρησιμοποιώντας το Aspose.Cells για .NET. Ακολουθήστε τον βήμα προς βήμα οδηγό μας για να διασφαλίσετε ακριβείς υπολογισμούς στα υπολογιστικά φύλλα σας.
weight: 13
url: /el/net/excel-formulas-and-calculation-options/detecting-circular-reference/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ανίχνευση κυκλικής αναφοράς στο Excel μέσω προγραμματισμού

## Εισαγωγή
Όσον αφορά την εργασία με αρχεία Excel, ένα από τα πιο απογοητευτικά ζητήματα που μπορεί να αντιμετωπίσετε είναι μια κυκλική αναφορά. Αυτό συμβαίνει όταν ένας τύπος αναφέρεται στο δικό του κελί, είτε άμεσα είτε έμμεσα, δημιουργώντας έναν βρόχο που μπορεί να προκαλέσει σύγχυση στη μηχανή υπολογισμού του Excel. Αλλά μη φοβάσαι! Με το Aspose.Cells για .NET, μπορείτε να εντοπίσετε μέσω προγραμματισμού αυτές τις ενοχλητικές κυκλικές αναφορές, διασφαλίζοντας ότι τα υπολογιστικά φύλλα σας παραμένουν λειτουργικά και ακριβή. Σε αυτόν τον οδηγό, θα σας καθοδηγήσουμε στη διαδικασία βήμα προς βήμα, καθιστώντας την τόσο απλή όσο η πίτα.
## Προαπαιτούμενα
Προτού βουτήξουμε στον έντονο εντοπισμό κυκλικών αναφορών, ας βεβαιωθούμε ότι έχετε όλα όσα χρειάζεστε για να ξεκινήσετε:
1. Visual Studio: Βεβαιωθείτε ότι έχετε εγκαταστήσει το Visual Studio στον υπολογιστή σας. Αυτό θα είναι το περιβάλλον ανάπτυξής σας.
2. .NET Framework: Βεβαιωθείτε ότι χρησιμοποιείτε μια συμβατή έκδοση του .NET Framework (τουλάχιστον .NET Framework 4.0).
3.  Aspose.Cells Library: Πρέπει να έχετε τη βιβλιοθήκη Aspose.Cells. Μπορείτε να το κατεβάσετε από το[Aspose website](https://releases.aspose.com/cells/net/).
4. Βασικές γνώσεις C#: Η εξοικείωση με τον προγραμματισμό C# θα είναι επωφελής, καθώς θα γράφουμε κώδικα σε αυτή τη γλώσσα.
5. Αρχείο Excel: Έχετε έτοιμο ένα αρχείο Excel που περιέχει κυκλικές αναφορές για δοκιμή. Μπορείτε να δημιουργήσετε ένα απλό ή να κατεβάσετε ένα δείγμα.
Τώρα που έχουμε τις προϋποθέσεις μας, ας περάσουμε στο διασκεδαστικό κομμάτι!
## Εισαγωγή πακέτων
Για να ξεκινήσετε την κωδικοποίηση, πρέπει να εισαγάγετε τα απαραίτητα πακέτα. Δείτε πώς να το κάνετε:
### Δημιουργία Νέου Έργου
- Ανοίξτε το Visual Studio και δημιουργήστε ένα νέο έργο εφαρμογής C# Console.
### Προσθήκη αναφοράς Aspose.Cells
- Κάντε δεξί κλικ στο έργο σας στην Εξερεύνηση λύσεων.
- Επιλέξτε "Διαχείριση πακέτων NuGet".
- Αναζητήστε το "Aspose.Cells" και εγκαταστήστε την πιο πρόσφατη έκδοση.
### Εισαγωγή απαιτούμενων χώρων ονομάτων
 Στην κορυφή σου`Program.cs` αρχείο, εισαγάγετε τους απαραίτητους χώρους ονομάτων:
```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Τώρα που έχουμε ρυθμίσει τα πάντα, ας βουτήξουμε στον κώδικα για να εντοπίσουμε κυκλικές αναφορές σε ένα αρχείο Excel.
## Βήμα 1: Ορίστε τον Κατάλογο εισόδου
Αρχικά, πρέπει να καθορίσετε τον κατάλογο όπου βρίσκεται το αρχείο Excel. Εδώ θα φορτώσετε το αρχείο σας Excel.
```csharp
// Κατάλογος εισαγωγής
string sourceDir = "Your Document Directory";
```
 Αντικαθιστώ`"Your Document Directory"` με την πραγματική διαδρομή προς το αρχείο Excel.
## Βήμα 2: Φορτώστε το βιβλίο εργασίας με LoadOptions
Στη συνέχεια, θα φορτώσετε το βιβλίο εργασίας του Excel. Εδώ αρχίζει η μαγεία!
```csharp
LoadOptions loadOptions = new LoadOptions();
var objWB = new Aspose.Cells.Workbook(sourceDir + "Circular Formulas.xls", loadOptions);
```
 Εδώ, δημιουργούμε μια νέα παρουσία του`LoadOptions` και φόρτωση του βιβλίου εργασίας από την καθορισμένη διαδρομή. Βεβαιωθείτε ότι το όνομα του αρχείου σας Excel ταιριάζει!
## Βήμα 3: Ενεργοποιήστε τις ρυθμίσεις επανάληψης
Για να επιτρέψετε κυκλικές αναφορές, πρέπει να ενεργοποιήσετε τις ρυθμίσεις επανάληψης στο βιβλίο εργασίας.
```csharp
objWB.Settings.Iteration = true;
```
Αυτό λέει στο Aspose.Cells να επιτρέπει κυκλικές αναφορές κατά τον υπολογισμό.
## Βήμα 4: Δημιουργήστε επιλογές υπολογισμού και κυκλική οθόνη
Τώρα, ας δημιουργήσουμε τις επιλογές υπολογισμού και την προσαρμοσμένη κυκλική οθόνη μας.
```csharp
CalculationOptions copts = new CalculationOptions();
CircularMonitor cm = new CircularMonitor();
copts.CalculationMonitor = cm;
```
 Εδώ, δημιουργούμε ένα παράδειγμα του`CalculationOptions` και ένα έθιμο`CircularMonitor`Αυτή η οθόνη θα σας βοηθήσει να παρακολουθείτε τυχόν κυκλικές αναφορές που βρέθηκαν κατά τη διάρκεια των υπολογισμών.
## Βήμα 5: Υπολογίστε τους τύπους
Τώρα, ήρθε η ώρα να υπολογίσετε τους τύπους στο βιβλίο εργασίας σας.
```csharp
objWB.CalculateFormula(copts);
```
Αυτή η γραμμή εκτελεί τον υπολογισμό και ελέγχει για κυκλικές αναφορές.
## Βήμα 6: Μετρήστε κυκλικές αναφορές
Μετά τον υπολογισμό, μπορείτε να μετρήσετε πόσες κυκλικές αναφορές βρέθηκαν.
```csharp
long lngCircularRef = cm.circulars.Count;
Console.WriteLine("Circular References found - " + lngCircularRef);
```
Αυτό θα παράγει τον αριθμό των κυκλικών αναφορών που εντοπίστηκαν στο αρχείο σας Excel.
## Βήμα 7: Εμφάνιση αποτελεσμάτων
Τέλος, ας εμφανίσουμε τα αποτελέσματα και ας επιβεβαιώσουμε ότι η μέθοδός μας εκτελέστηκε με επιτυχία.
```csharp
Console.WriteLine("DetectCircularReference executed successfully.\r\n");
```
## Βήμα 8: Υλοποιήστε την κλάση CircularMonitor
 Για να ολοκληρώσετε τη διαδικασία, θα πρέπει να εφαρμόσετε το`CircularMonitor` τάξη. Αυτή η κλάση θα κληρονομήσει από`AbstractCalculationMonitor` και χειρίζεται τον εντοπισμό κυκλικών αναφορών.
```csharp
public class CircularMonitor : AbstractCalculationMonitor
{
    public ArrayList circulars = new ArrayList();
    public ArrayList Circulars { get { return circulars; } }
    public override bool OnCircular(IEnumerator circularCellsData)
    {
        CalculationCell cc = null;
        ArrayList cur = new ArrayList();
        while (circularCellsData.MoveNext())
        {
            cc = (CalculationCell)circularCellsData.Current;
            cur.Add(cc.Worksheet.Name + "!" + CellsHelper.CellIndexToName(cc.CellRow, cc.CellColumn));
        }
        circulars.Add(cur);
        return true;
    }
}
```
Αυτή η κλάση καταγράφει τις λεπτομέρειες κάθε κυκλικής αναφοράς που βρέθηκε, συμπεριλαμβανομένου του ονόματος του φύλλου εργασίας και του ευρετηρίου κελιού.
## Σύναψη
Η ανίχνευση κυκλικών αναφορών στο Excel χρησιμοποιώντας το Aspose.Cells για .NET είναι μια απλή διαδικασία αφού την αναλύσετε σε διαχειρίσιμα βήματα. Ακολουθώντας αυτόν τον οδηγό, μπορείτε εύκολα να αναγνωρίσετε και να χειριστείτε κυκλικές αναφορές στα υπολογιστικά φύλλα σας, διασφαλίζοντας ότι οι υπολογισμοί σας παραμένουν ακριβείς και αξιόπιστοι. Είτε είστε έμπειρος προγραμματιστής είτε μόλις ξεκινάτε, το Aspose.Cells παρέχει ισχυρά εργαλεία για τη βελτίωση των δυνατοτήτων χειρισμού του Excel. 
## Συχνές ερωτήσεις
### Τι είναι μια κυκλική αναφορά στο Excel;
Μια κυκλική αναφορά εμφανίζεται όταν ένας τύπος αναφέρεται στο δικό του κελί, προκαλώντας έναν ατελείωτο βρόχο στους υπολογισμούς.
### Πώς μπορώ να εντοπίσω κυκλικές αναφορές μέσω προγραμματισμού;
Μπορείτε να χρησιμοποιήσετε τη βιβλιοθήκη Aspose.Cells στο .NET για να εντοπίσετε μέσω προγραμματισμού κυκλικές αναφορές εφαρμόζοντας μια προσαρμοσμένη οθόνη υπολογισμού.
### Ποιες είναι οι προϋποθέσεις για τη χρήση του Aspose.Cells;
Χρειάζεστε εγκατεστημένο το Visual Studio, το .NET Framework και τη βιβλιοθήκη Aspose.Cells.
### Μπορώ να χρησιμοποιήσω το Aspose.Cells δωρεάν;
Ναι, το Aspose.Cells προσφέρει μια δωρεάν δοκιμή που μπορείτε να χρησιμοποιήσετε για να εξερευνήσετε τις δυνατότητές του.
### Πού μπορώ να βρω περισσότερες πληροφορίες για το Aspose.Cells;
 Μπορείτε να επισκεφθείτε το[Τεκμηρίωση Aspose.Cells](https://reference.aspose.com/cells/net/) για λεπτομερείς πληροφορίες και παραδείγματα.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
