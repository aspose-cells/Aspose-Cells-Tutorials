---
title: Ρύθμιση αυτόματης μορφής συγκεντρωτικού πίνακα μέσω προγραμματισμού στο .NET
linktitle: Ρύθμιση αυτόματης μορφής συγκεντρωτικού πίνακα μέσω προγραμματισμού στο .NET
second_title: Aspose.Cells .NET Excel Processing API
description: Μάθετε πώς να ορίζετε την αυτόματη μορφοποίηση για πίνακες περιστροφής του Excel μέσω προγραμματισμού χρησιμοποιώντας το Aspose.Cells για .NET σε αυτό το λεπτομερές, βήμα προς βήμα εκμάθηση.
weight: 18
url: /el/net/creating-and-configuring-pivot-tables/setting-auto-format/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ρύθμιση αυτόματης μορφής συγκεντρωτικού πίνακα μέσω προγραμματισμού στο .NET

## Εισαγωγή
Όταν πρόκειται για την ανάλυση δεδομένων, οι συγκεντρωτικοί πίνακες στο Excel μπορούν να αλλάξουν το παιχνίδι. Σας επιτρέπουν να συνοψίζετε και να αναλύετε δεδομένα δυναμικά, βοηθώντας σας να συγκεντρώσετε πληροφορίες που θα ήταν σχεδόν αδύνατο να εξαχθούν με μη αυτόματο τρόπο. Τι γίνεται όμως αν θέλετε να αυτοματοποιήσετε τη διαδικασία μορφοποίησης των συγκεντρωτικών πινάκων σας στο .NET; Εδώ, θα σας δείξω πώς να ορίσετε μέσω προγραμματισμού την αυτόματη μορφή ενός συγκεντρωτικού πίνακα χρησιμοποιώντας την ισχυρή βιβλιοθήκη Aspose.Cells για .NET.
Σε αυτόν τον οδηγό, θα εξερευνήσουμε τα βασικά στοιχεία, θα εξετάσουμε τις προϋποθέσεις, θα εισαγάγουμε τα απαραίτητα πακέτα και, στη συνέχεια, θα βουτήξουμε σε έναν οδηγό βήμα προς βήμα για να σας βοηθήσουμε να μορφοποιήσετε τους συγκεντρωτικούς πίνακες σαν επαγγελματίας. Ακούγεται καλό; Ας πηδήξουμε αμέσως!
## Προαπαιτούμενα
Πριν ξεκινήσουμε, ας βεβαιωθούμε ότι έχετε όλα όσα χρειάζεστε για να ξεκινήσετε:
1. Περιβάλλον ανάπτυξης .NET: Βεβαιωθείτε ότι έχετε μια λειτουργική παρουσία του Visual Studio (ή οποιουδήποτε IDE που υποστηρίζει .NET).
2.  Aspose.Cells Library: Για να εργαστείτε ομαλά με αρχεία Excel, θα χρειαστείτε εγκατεστημένη τη βιβλιοθήκη Aspose.Cells. Εάν δεν το έχετε κάνει ακόμα, μπορείτε να το πάρετε από το[σελίδα λήψης](https://releases.aspose.com/cells/net/).
3. Βασικές γνώσεις C#: Η εξοικείωση με τον προγραμματισμό C# θα σας βοηθήσει να κατανοήσετε καλύτερα τα βήματα.
4.  Αρχείο Excel (Πρότυπο): Θα χρειαστείτε ένα αρχείο προτύπου Excel για να ξεκινήσετε, το οποίο θα επεξεργαστεί στο παράδειγμά μας. Για απλότητα, μπορείτε να δημιουργήσετε ένα δείγμα αρχείου με το όνομα`Book1.xls`.
## Εισαγωγή πακέτων
Για να συνεχίσετε με το Aspose.Cells στο έργο σας, θα χρειαστεί να εισαγάγετε τα απαραίτητα πακέτα. Δείτε πώς μπορείτε να το ρυθμίσετε στο έργο σας .NET:
### Δημιουργία Νέου Έργου
Ξεκινήστε δημιουργώντας ένα νέο έργο .NET στο IDE που προτιμάτε. 
### Προσθήκη Αναφορών
Φροντίστε να προσθέσετε μια αναφορά στη βιβλιοθήκη Aspose.Cells. Εάν κατεβάσατε τη βιβλιοθήκη, προσθέστε τα DLL από την εξαγωγή. Εάν χρησιμοποιείτε το NuGet, μπορείτε απλά να εκτελέσετε:
```bash
Install-Package Aspose.Cells
```
### Εισαγωγή χώρων ονομάτων
Τώρα, στο αρχείο κώδικα, θα πρέπει να εισαγάγετε τον χώρο ονομάτων Aspose.Cells. Μπορείτε να το κάνετε αυτό προσθέτοντας την ακόλουθη γραμμή στο επάνω μέρος του αρχείου C#:
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
using Aspose.Cells.Pivot;
```
Αφού ολοκληρωθούν αυτά τα βήματα, είστε έτοιμοι να γράψετε κάποιο κώδικα!
Τώρα, ας αναλύσουμε τον κώδικα που παρείχατε σε λεπτομερή βήματα με επεξηγήσεις για το τι κάνει κάθε μέρος. 
## Βήμα 1: Ορίστε τον Κατάλογο Εγγράφων σας
Για να ξεκινήσετε, πρέπει να ορίσετε τη διαδρομή προς τον κατάλογο των εγγράφων σας όπου βρίσκονται τα αρχεία Excel. Στο παράδειγμά μας, θα το ορίσουμε ως εξής:
```csharp
string dataDir = "Your Document Directory";  // Τροποποιήστε όπως απαιτείται
```
 Αυτή η γραμμή δημιουργεί μια μεταβλητή συμβολοσειράς`dataDir`που κρατά τη διαδρομή του αρχείου στα έγγραφά σας. Φροντίστε να αντικαταστήσετε`"Your Document Directory"` με την πραγματική διαδρομή στο σύστημά σας.
## Βήμα 2: Φορτώστε το αρχείο προτύπου
Στη συνέχεια, θα θέλετε να φορτώσετε ένα υπάρχον βιβλίο εργασίας που περιέχει τον συγκεντρωτικό σας πίνακα:
```csharp
Workbook workbook = new Workbook(dataDir + "Book1.xls");
```
 Αυτή η γραμμή προετοιμάζει μια νέα`Workbook` αντικείμενο φορτώνοντας το καθορισμένο αρχείο Excel. Το αρχείο θα πρέπει να περιέχει τουλάχιστον έναν συγκεντρωτικό πίνακα για να είναι αποτελεσματικά τα επόμενα βήματα.
## Βήμα 3: Πρόσβαση στο επιθυμητό φύλλο εργασίας
Προσδιορίστε ποιο φύλλο εργασίας πρέπει να εργαστείτε για να αποκτήσετε πρόσβαση στον συγκεντρωτικό πίνακα. Σε αυτήν την περίπτωση, θα πάρουμε μόνο το πρώτο:
```csharp
int pivotIndex = 0;  // Ευρετήριο του Συγκεντρωτικού Πίνακα
Worksheet worksheet = workbook.Worksheets[0];
```
 Εδώ,`worksheet` ανακτά το πρώτο φύλλο εργασίας από το βιβλίο εργασίας. Το ευρετήριο του συγκεντρωτικού πίνακα έχει οριστεί σε`0`, που σημαίνει ότι έχουμε πρόσβαση στον πρώτο συγκεντρωτικό πίνακα σε αυτό το φύλλο εργασίας.
## Βήμα 4: Εντοπίστε τον Συγκεντρωτικό Πίνακα
Έχοντας έτοιμο το φύλλο εργασίας, ήρθε η ώρα να αποκτήσετε πρόσβαση στον συγκεντρωτικό πίνακα:
```csharp
PivotTable pivotTable = worksheet.PivotTables[pivotIndex];
```
 Αυτό εκκινεί ένα νέο`PivotTable` αντικειμένου λαμβάνοντας τον συγκεντρωτικό πίνακα στο καθορισμένο ευρετήριο από το φύλλο εργασίας.
## Βήμα 5: Ορίστε την ιδιότητα αυτόματης μορφοποίησης
Τώρα στο ζουμερό μέρος: ρύθμιση των επιλογών αυτόματης μορφοποίησης για τον συγκεντρωτικό πίνακα.
```csharp
pivotTable.IsAutoFormat = true; // Ενεργοποίηση αυτόματης μορφοποίησης
```
 Αυτή η γραμμή ενεργοποιεί τη δυνατότητα αυτόματης μορφοποίησης για τον συγκεντρωτικό πίνακα. Όταν έχει οριστεί σε`true`, ο συγκεντρωτικός πίνακας θα μορφοποιηθεί αυτόματα με βάση προκαθορισμένα στυλ.
## Βήμα 6: Επιλέξτε έναν συγκεκριμένο τύπο αυτόματης μορφής
Θα θέλαμε επίσης να καθορίσουμε ποιο στυλ αυτόματης μορφής θα πρέπει να υιοθετήσει ο συγκεντρωτικός πίνακας. Το Aspose.Cells έχει διάφορες μορφές από τις οποίες μπορούμε να επιλέξουμε. Δείτε πώς να το ρυθμίσετε:
```csharp
pivotTable.AutoFormatType = Aspose.Cells.Pivot.PivotTableAutoFormatType.Report5;
```
 Με αυτή τη γραμμή, εκχωρούμε έναν συγκεκριμένο τύπο αυτόματης μορφής στον συγκεντρωτικό πίνακα.`Report5` είναι απλώς ένα παράδειγμα ενός στυλ. μπορείτε να επιλέξετε από μια ποικιλία επιλογών ανάλογα με τις ανάγκες σας. 
## Βήμα 7: Αποθηκεύστε το βιβλίο εργασίας
Τέλος, μην ξεχάσετε να αποθηκεύσετε το βιβλίο εργασίας σας αφού κάνετε όλες τις αλλαγές:
```csharp
workbook.Save(dataDir + "output.xls");
```
 Αυτή η γραμμή κώδικα αποθηκεύει το τροποποιημένο βιβλίο εργασίας σε ένα νέο αρχείο που ονομάζεται`output.xls` στον καθορισμένο κατάλογο. Βεβαιωθείτε ότι έχετε ελέγξει αυτό το αρχείο για να δείτε τον όμορφα διαμορφωμένο συγκεντρωτικό πίνακα!
## Σύναψη
Συγχαρητήρια! Μόλις προγραμματίσατε έναν συγκεντρωτικό πίνακα του Excel σε αυτόματη διαμόρφωση χρησιμοποιώντας το Aspose.Cells στο .NET. Αυτή η διαδικασία όχι μόνο σας εξοικονομεί χρόνο κατά την προετοιμασία αναφορών, αλλά διασφαλίζει επίσης τη συνέπεια στην εμφάνιση των δεδομένων σας σε κάθε εκτέλεση. Με λίγες μόνο γραμμές κώδικα, μπορείτε να βελτιώσετε σημαντικά τα αρχεία σας Excel—ακριβώς όπως ένας ψηφιακός μάγος.
## Συχνές ερωτήσεις
### Τι είναι το Aspose.Cells;
Το Aspose.Cells είναι μια ισχυρή βιβλιοθήκη .NET για το χειρισμό αρχείων Excel χωρίς να απαιτείται εγκατάσταση του Microsoft Excel.
### Μπορώ να μορφοποιήσω πολλούς συγκεντρωτικούς πίνακες σε ένα βιβλίο εργασίας;
Ναι, μπορείτε να κάνετε επαναφορά πολλών αντικειμένων συγκεντρωτικού πίνακα στο βιβλίο εργασίας σας για να τα μορφοποιήσετε ένα προς ένα.
### Υπάρχει διαθέσιμη δωρεάν δοκιμή για το Aspose.Cells;
 Απολύτως! Μπορείτε να ξεκινήσετε με μια διαθέσιμη δωρεάν δοκιμαστική έκδοση[εδώ](https://releases.aspose.com/).
### Τι γίνεται αν ο συγκεντρωτικός πίνακας μου δεν μορφοποιείται σωστά;
Βεβαιωθείτε ότι ο συγκεντρωτικός πίνακας αναφέρεται σωστά και ότι υπάρχει ο τύπος αυτόματης μορφοποίησης—διαφορετικά, ενδέχεται να επιστρέψει στις προεπιλεγμένες ρυθμίσεις.
### Μπορώ να αυτοματοποιήσω αυτή τη διαδικασία με προγραμματισμένες εργασίες;
Ναί! Με την ενσωμάτωση αυτού του κώδικα σε μια προγραμματισμένη εργασία, μπορείτε να αυτοματοποιήσετε τη δημιουργία και τη μορφοποίηση αναφορών τακτικά.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
