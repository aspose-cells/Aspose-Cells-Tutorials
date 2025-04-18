---
title: Καταργήστε την ομαδοποίηση γραμμών και στηλών στο Excel με το Aspose.Cells
linktitle: Καταργήστε την ομαδοποίηση γραμμών και στηλών στο Excel με το Aspose.Cells
second_title: Aspose.Cells .NET Excel Processing API
description: Μάθετε πώς να καταργείτε την ομαδοποίηση σειρών και στηλών στο Excel χρησιμοποιώντας το Aspose.Cells για .NET με αυτόν τον αναλυτικό οδηγό. Απλοποιήστε τον χειρισμό δεδομένων του Excel.
weight: 15
url: /el/net/row-and-column-management/ungrouping-rows-and-columns/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Καταργήστε την ομαδοποίηση γραμμών και στηλών στο Excel με το Aspose.Cells

## Εισαγωγή
Όταν πρόκειται για το χειρισμό αρχείων Excel, μπορεί να βρεθείτε σε καταστάσεις όπου πρέπει να καταργήσετε την ομαδοποίηση σειρών και στηλών. Είτε καθαρίζετε ένα υπολογιστικό φύλλο είτε επαναμορφώνετε δεδομένα για καλύτερη παρουσίαση, το Aspose.Cells για .NET είναι ένα φανταστικό εργαλείο που απλοποιεί τη διαδικασία. Σε αυτό το σεμινάριο, θα σας καθοδηγήσω στα βήματα για την κατάργηση ομαδοποίησης σειρών και στηλών στο Excel χρησιμοποιώντας το Aspose.Cells. Στο τέλος, θα έχετε πλήρη κατανόηση του τρόπου εργασίας με αρχεία Excel μέσω προγραμματισμού.
## Προαπαιτούμενα
Πριν βουτήξετε στον κώδικα, ας βεβαιωθούμε ότι έχετε ρυθμίσει τα πάντα. Εδώ είναι τι θα χρειαστείτε:
1.  Visual Studio: Θα πρέπει να έχετε εγκατεστημένη μια λειτουργική έκδοση του Visual Studio στον υπολογιστή σας. Εάν δεν το έχετε ακόμα, μπορείτε να το κατεβάσετε από[Ο ιστότοπος του Visual Studio](https://visualstudio.microsoft.com/).
2. Aspose.Cells για .NET: Θα χρειαστεί να κάνετε λήψη της βιβλιοθήκης Aspose.Cells. Μπορείτε να το αρπάξετε από το[Σελίδα Aspose Releases](https://releases.aspose.com/cells/net/) . Βεβαιωθείτε ότι διαθέτετε τις απαραίτητες άδειες χρήσης, τις οποίες μπορείτε να αγοράσετε ή να αποκτήσετε μέσω α[προσωρινή άδεια](https://purchase.aspose.com/temporary-license/).
3. Βασική γνώση C#: Η βασική κατανόηση του προγραμματισμού C# θα σας βοηθήσει να ακολουθήσετε πιο εύκολα.
Μόλις τα έχετε όλα έτοιμα, μπορούμε να μεταβούμε στο διασκεδαστικό μέρος: τον κώδικα!
## Εισαγωγή πακέτων
Για να ξεκινήσετε, πρέπει να εισαγάγετε τα απαραίτητα πακέτα στο έργο σας C#. Δείτε πώς το κάνετε:
1. Ανοίξτε το έργο σας στο Visual Studio.
2. Προσθέστε μια αναφορά στη βιβλιοθήκη Aspose.Cells. Μπορείτε να το κάνετε αυτό κάνοντας δεξί κλικ στις Αναφορές στο έργο σας και επιλέγοντας Προσθήκη αναφοράς. Μεταβείτε στη θέση όπου αποθηκεύσατε το Aspose.Cells DLL.
3. Στην κορυφή του αρχείου C#, προσθέστε τα ακόλουθα χρησιμοποιώντας οδηγίες:
```csharp
using System.IO;
using Aspose.Cells;
```
Τώρα που όλα έχουν ρυθμιστεί, ας προχωρήσουμε στα βήματα για την κατάργηση ομαδοποίησης σειρών και στηλών στο φύλλο Excel. 
## Βήμα 1: Ορίστε τον Κατάλογο Εγγράφων
Αρχικά, πρέπει να καθορίσετε τον κατάλογο όπου βρίσκεται το αρχείο Excel. Μπορείτε να το ρυθμίσετε ως εξής:
```csharp
// Η διαδρομή προς τον κατάλογο εγγράφων.
string dataDir = "Your Document Directory";
```
 Αντικαθιστώ`"Your Document Directory"` με την πραγματική διαδρομή στον υπολογιστή σας όπου είναι αποθηκευμένο το αρχείο Excel. 
## Βήμα 2: Δημιουργήστε μια ροή αρχείων
Στη συνέχεια, πρέπει να δημιουργήσετε μια ροή αρχείων για να ανοίξετε το αρχείο Excel. Αυτό είναι το πώς μπορείτε να το κάνετε:
```csharp
// Δημιουργία ροής αρχείων που περιέχει το αρχείο Excel που πρόκειται να ανοίξει
FileStream fstream = new FileStream(dataDir + "book1.xls", FileMode.Open);
```
 Εδώ, ανοίγετε το αρχείο με το όνομα`book1.xls`. Βεβαιωθείτε ότι αυτό το αρχείο υπάρχει στον καθορισμένο κατάλογο σας, διαφορετικά θα εμφανιστεί σφάλμα που δεν βρέθηκε.
## Βήμα 3: Δημιουργήστε ένα αντικείμενο βιβλίου εργασίας
Τώρα, ας φορτώσουμε το αρχείο Excel σε ένα αντικείμενο βιβλίου εργασίας. Αυτό σας επιτρέπει να χειριστείτε το βιβλίο εργασίας μέσω προγραμματισμού:
```csharp
// Δημιουργία αντικειμένου βιβλίου εργασίας
// Άνοιγμα του αρχείου Excel μέσω της ροής αρχείων
Workbook workbook = new Workbook(fstream);
```
Με αυτήν τη γραμμή κώδικα, φορτώσατε με επιτυχία το αρχείο Excel στη μνήμη και είστε έτοιμοι να εργαστείτε μαζί του.
## Βήμα 4: Πρόσβαση στο φύλλο εργασίας
Αφού έχετε το βιβλίο εργασίας, το επόμενο βήμα είναι να αποκτήσετε πρόσβαση στο συγκεκριμένο φύλλο εργασίας όπου θέλετε να καταργήσετε την ομαδοποίηση σειρών και στηλών. Δείτε πώς να το κάνετε αυτό:
```csharp
// Πρόσβαση στο πρώτο φύλλο εργασίας στο αρχείο Excel
Worksheet worksheet = workbook.Worksheets[0];
```
Σε αυτήν την περίπτωση, έχουμε πρόσβαση στο πρώτο φύλλο εργασίας. Εάν τα δεδομένα σας βρίσκονται σε διαφορετικό φύλλο, μπορείτε να αλλάξετε το ευρετήριο ανάλογα.
## Βήμα 5: Καταργήστε την ομαδοποίηση σειρών
Τώρα έρχεται το συναρπαστικό μέρος! Ας καταργήσουμε την ομαδοποίηση των πρώτων έξι σειρών (από τη σειρά 0 στη σειρά 5). Χρησιμοποιήστε τον παρακάτω κώδικα:
```csharp
// Κατάργηση ομαδοποίησης πρώτων έξι σειρών (από 0 έως 5)
worksheet.Cells.UngroupRows(0, 5);
```
Αυτή η μέθοδος καταργεί κάθε ομαδοποίηση που έχει εφαρμοστεί στις καθορισμένες σειρές. Είναι τόσο εύκολο!
## Βήμα 6: Κατάργηση ομαδοποίησης στηλών
Ακριβώς όπως οι σειρές, μπορείτε επίσης να καταργήσετε την ομαδοποίηση των στηλών. Δείτε πώς μπορείτε να καταργήσετε την ομαδοποίηση των τριών πρώτων στηλών (από τη στήλη 0 στη στήλη 2):
```csharp
// Κατάργηση ομαδοποίησης των τριών πρώτων στηλών (από 0 έως 2)
worksheet.Cells.UngroupColumns(0, 2);
```
## Βήμα 7: Αποθηκεύστε το τροποποιημένο αρχείο Excel
 Αφού καταργήσετε την ομαδοποίηση των σειρών και των στηλών, το επόμενο βήμα είναι να αποθηκεύσετε τις αλλαγές σε ένα αρχείο Excel. Μπορείτε να το κάνετε αυτό χρησιμοποιώντας το`Save` μέθοδος:
```csharp
// Αποθήκευση του τροποποιημένου αρχείου Excel
workbook.Save(dataDir + "output.xls");
```
 Σε αυτό το παράδειγμα, αποθηκεύουμε το τροποποιημένο αρχείο ως`output.xls`. Μπορείτε να αλλάξετε το όνομα αρχείου σε ό,τι προτιμάτε.
## Βήμα 8: Κλείστε τη ροή αρχείων
Τέλος, για να ελευθερώσετε πόρους, θα πρέπει να κλείσετε τη ροή αρχείων:
```csharp
// Κλείσιμο της ροής αρχείων για να ελευθερωθούν όλοι οι πόροι
fstream.Close();
```
Αυτή είναι μια καλή πρακτική για να βεβαιωθείτε ότι η αίτησή σας δεν θα κρατά τις λαβές αρχείων περισσότερο από όσο χρειάζεται.
## Σύναψη
Και ορίστε το! Μάθατε με επιτυχία πώς να καταργείτε την ομαδοποίηση σειρών και στηλών σε ένα αρχείο Excel χρησιμοποιώντας το Aspose.Cells για .NET. Με λίγες μόνο γραμμές κώδικα, μπορείτε να κάνετε σημαντικές αλλαγές στα αρχεία σας Excel μέσω προγραμματισμού. Είτε αυτοματοποιείτε αναφορές είτε προετοιμάζετε δεδομένα για ανάλυση, η γνώση αυτών των τεχνικών μπορεί να σας εξοικονομήσει πολύ χρόνο.
## Συχνές ερωτήσεις
### Τι είναι το Aspose.Cells;
Το Aspose.Cells είναι μια ισχυρή βιβλιοθήκη για εργασία με αρχεία Excel σε εφαρμογές .NET, επιτρέποντας τον εύκολο χειρισμό, τη μετατροπή και τη δημιουργία υπολογιστικών φύλλων.
### Μπορώ να καταργήσω την ομαδοποίηση σειρών και στηλών στο Excel χρησιμοποιώντας άλλες βιβλιοθήκες;
Ναι, υπάρχουν άλλες βιβλιοθήκες διαθέσιμες για χειρισμό του Excel στο .NET, αλλά το Aspose.Cells προσφέρει εκτεταμένες δυνατότητες και ευκολία στη χρήση.
### Υπάρχει τρόπος να αναιρέσετε τις αλλαγές μετά την αποθήκευση;
Μόλις αποθηκεύσετε ένα αρχείο Excel, δεν είναι δυνατή η επαναφορά της προηγούμενης κατάστασης, εκτός εάν έχετε αντίγραφο ασφαλείας του αρχικού αρχείου.
### Πώς μπορώ να λάβω υποστήριξη για το Aspose.Cells;
 Μπορείτε να βρείτε υποστήριξη επισκεπτόμενοι το[Φόρουμ υποστήριξης Aspose](https://forum.aspose.com/c/cells/9), όπου μπορείτε να κάνετε ερωτήσεις και να βρείτε λύσεις.
### Μπορώ να χρησιμοποιήσω το Aspose.Cells χωρίς άδεια χρήσης;
Ναι, μπορείτε να χρησιμοποιήσετε το Aspose.Cells δωρεάν με ορισμένους περιορισμούς και μπορείτε να ξεκινήσετε με α[προσωρινή άδεια](https://purchase.aspose.com/temporary-license/) για πλήρη λειτουργικότητα.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
