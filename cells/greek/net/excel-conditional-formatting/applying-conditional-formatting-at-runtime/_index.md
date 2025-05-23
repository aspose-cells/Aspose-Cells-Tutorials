---
"description": "Μάθετε πώς να εφαρμόζετε μορφοποίηση υπό όρους κατά τον χρόνο εκτέλεσης στο Excel με το Aspose.Cells για .NET σε αυτόν τον ολοκληρωμένο οδηγό βήμα προς βήμα."
"linktitle": "Εφαρμογή μορφοποίησης υπό όρους κατά τον χρόνο εκτέλεσης στο Excel"
"second_title": "API επεξεργασίας Excel Aspose.Cells .NET"
"title": "Εφαρμογή μορφοποίησης υπό όρους κατά τον χρόνο εκτέλεσης στο Excel"
"url": "/el/net/excel-conditional-formatting/applying-conditional-formatting-at-runtime/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Εφαρμογή μορφοποίησης υπό όρους κατά τον χρόνο εκτέλεσης στο Excel

## Εισαγωγή

Είναι ισχυρά εργαλεία για ανάλυση και οπτικοποίηση δεδομένων. Ένα από τα ξεχωριστά χαρακτηριστικά του Excel είναι η μορφοποίηση υπό όρους, η οποία επιτρέπει στους χρήστες να εφαρμόζουν συγκεκριμένα στυλ μορφοποίησης σε κελιά με βάση τις τιμές τους. Αυτό μπορεί να διευκολύνει τον εντοπισμό τάσεων, την επισήμανση σημαντικών σημείων δεδομένων ή απλώς να κάνει τα δεδομένα πιο ευανάγνωστα. Εάν θέλετε να εφαρμόσετε μορφοποίηση υπό όρους στα αρχεία Excel σας μέσω προγραμματισμού, βρίσκεστε στο σωστό μέρος! Σε αυτόν τον οδηγό, θα σας δείξουμε πώς να εφαρμόσετε μορφοποίηση υπό όρους κατά τον χρόνο εκτέλεσης χρησιμοποιώντας το Aspose.Cells για .NET.

## Προαπαιτούμενα
Πριν εμβαθύνουμε στον κώδικα, ας βεβαιωθούμε ότι έχετε όλα όσα χρειάζεστε για να ξεκινήσετε:

1. Visual Studio: Βεβαιωθείτε ότι έχετε εγκαταστήσει το Visual Studio στον υπολογιστή σας. Μπορείτε να χρησιμοποιήσετε οποιαδήποτε έκδοση που υποστηρίζει ανάπτυξη .NET.
2. Aspose.Cells για .NET: Θα χρειαστεί να έχετε εγκατεστημένο το Aspose.Cells για .NET. Μπορείτε να το κατεβάσετε από το [Ιστότοπος Aspose](https://releases.aspose.com/cells/net/).
3. Βασικές γνώσεις C#: Η εξοικείωση με τον προγραμματισμό C# θα σας βοηθήσει να κατανοήσετε καλύτερα τα αποσπάσματα κώδικα.
4. .NET Framework: Βεβαιωθείτε ότι το έργο σας στοχεύει σε μια συμβατή έκδοση του .NET Framework.

Τώρα που καλύψαμε τις προϋποθέσεις, ας περάσουμε στο διασκεδαστικό κομμάτι!

## Εισαγωγή πακέτων
Για να ξεκινήσετε με το Aspose.Cells, θα χρειαστεί να εισαγάγετε τους απαραίτητους χώρους ονομάτων στο έργο C# σας. Δείτε πώς μπορείτε να το κάνετε αυτό:

```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

Αυτοί οι χώροι ονομάτων θα σας δώσουν πρόσβαση στις κλάσεις και τις μεθόδους που απαιτούνται για τον χειρισμό αρχείων Excel και την εφαρμογή μορφοποίησης υπό όρους.

Τώρα, ας αναλύσουμε τη διαδικασία εφαρμογής μορφοποίησης υπό όρους σε διαχειρίσιμα βήματα.

## Βήμα 1: Ρύθμιση του έργου σας
Πρώτα απ 'όλα, πρέπει να δημιουργήσετε ένα νέο έργο C# στο Visual Studio. Δείτε πώς:

1. Ανοίξτε το Visual Studio και επιλέξτε Αρχείο > Νέο > Έργο.
2. Επιλέξτε Εφαρμογή κονσόλας (.NET Framework) και δώστε στο έργο σας ένα όνομα.
3. Κάντε κλικ στην επιλογή Δημιουργία.

## Βήμα 2: Προσθήκη αναφοράς Aspose.Cells
Μόλις ρυθμιστεί το έργο σας, πρέπει να προσθέσετε μια αναφορά στη βιβλιοθήκη Aspose.Cells:

1. Κάντε δεξί κλικ στο έργο σας στην Εξερεύνηση λύσεων.
2. Επιλέξτε Διαχείριση πακέτων NuGet.
3. Αναζητήστε το Aspose.Cells και εγκαταστήστε το.

Αυτό θα σας επιτρέψει να χρησιμοποιήσετε όλες τις λειτουργίες που παρέχονται από τη βιβλιοθήκη Aspose.Cells.

## Βήμα 3: Δημιουργία αντικειμένου βιβλίου εργασίας
Στη συνέχεια, ας δημιουργήσουμε ένα νέο βιβλίο εργασίας και ένα φύλλο εργασίας. Εδώ συμβαίνει όλη η μαγεία:

```csharp
// Η διαδρομή προς τον κατάλογο εγγράφων.
string dataDir = "Your Document Directory";
string filePath = dataDir + "Book1.xlsx";

// Δημιουργία στιγμιαίου αντικειμένου βιβλίου εργασίας
Workbook workbook = new Workbook();
Worksheet sheet = workbook.Worksheets[0];
```

Σε αυτό το βήμα, ορίζουμε τον κατάλογο όπου θα αποθηκευτεί το αρχείο Excel, δημιουργούμε ένα νέο βιβλίο εργασίας και έχουμε πρόσβαση στο πρώτο φύλλο εργασίας.

## Βήμα 4: Προσθήκη μορφοποίησης υπό όρους
Τώρα, ας προσθέσουμε κάποια μορφοποίηση υπό όρους. Θα ξεκινήσουμε δημιουργώντας ένα κενό αντικείμενο μορφοποίησης υπό όρους:

```csharp
// Προσθέτει μια κενή μορφοποίηση υπό όρους
int index = sheet.ConditionalFormattings.Add();
FormatConditionCollection fcs = sheet.ConditionalFormattings[index];
```

Εδώ, προσθέτουμε μια νέα συλλογή μορφοποίησης υπό όρους στο φύλλο εργασίας μας, η οποία θα περιέχει τους κανόνες μορφοποίησης.

## Βήμα 5: Ορίστε το εύρος μορφοποίησης
Στη συνέχεια, πρέπει να καθορίσουμε την περιοχή κελιών στην οποία θα εφαρμοστεί η μορφοποίηση υπό όρους. Ας υποθέσουμε ότι θέλουμε να μορφοποιήσουμε την πρώτη γραμμή και τη δεύτερη στήλη:

```csharp
// Ορίζει το εύρος μορφοποίησης υπό όρους.
CellArea ca = new CellArea();
ca.StartRow =0;
ca.EndRow =0;
ca.StartColumn =0;
ca.EndColumn =0;
fcs.AddArea(ca);

ca = new CellArea();
ca.StartRow =1;
ca.EndRow =1;
ca.StartColumn =1;
ca.EndColumn =1;
fcs.AddArea(ca);
```

Σε αυτόν τον κώδικα, ορίζουμε δύο περιοχές για μορφοποίηση υπό όρους. Η πρώτη περιοχή είναι για το κελί στο (0,0) και η δεύτερη για το (1,1). Μη διστάσετε να προσαρμόσετε αυτά τα εύρη με βάση τις συγκεκριμένες ανάγκες σας!

## Βήμα 6: Προσθήκη συνθηκών μορφοποίησης υπό όρους
Τώρα είναι η ώρα να ορίσουμε τις συνθήκες για τη μορφοποίησή μας. Ας υποθέσουμε ότι θέλουμε να επισημάνουμε κελιά με βάση τις τιμές τους:

```csharp
// Προσθέτει συνθήκη.
int conditionIndex = fcs.AddCondition(FormatConditionType.CellValue, OperatorType.Between, "=A2", "100");

// Προσθέτει συνθήκη.
int conditionIndex2 = fcs.AddCondition(FormatConditionType.CellValue, OperatorType.Between, "50", "100");
```

Σε αυτό το βήμα, προσθέτουμε δύο συνθήκες: μία για τιμές μεταξύ `A2` και `100`και ένα άλλο για τιμές μεταξύ `50` και `100`Αυτό σας επιτρέπει να επισημαίνετε δυναμικά τα κελιά με βάση τις τιμές τους.

## Βήμα 7: Ορισμός στυλ μορφοποίησης
Με τις συνθήκες μας στη θέση τους, μπορούμε τώρα να ορίσουμε τα στυλ μορφοποίησης. Ας αλλάξουμε το χρώμα φόντου για τις συνθήκες μας:

```csharp
// Ορίζει το χρώμα φόντου.
FormatCondition fc = fcs[conditionIndex];
fc.Style.BackgroundColor = Color.Red;
```

Εδώ, ορίζουμε το χρώμα φόντου της πρώτης συνθήκης σε κόκκινο. Μπορείτε να το προσαρμόσετε περαιτέρω αλλάζοντας το χρώμα της γραμματοσειράς, τα περιγράμματα και άλλα στυλ, όπως απαιτείται!

## Βήμα 8: Αποθήκευση του αρχείου Excel
Επιτέλους, ήρθε η ώρα να αποθηκεύσουμε την εργασία μας! Θα αποθηκεύσουμε το βιβλίο εργασίας στον καθορισμένο κατάλογο:

```csharp
// Αποθήκευση του αρχείου Excel
workbook.Save(dataDir + "output.xls");
```

Αυτή η γραμμή κώδικα αποθηκεύει το αρχείο Excel με την εφαρμοσμένη μορφοποίηση υπό όρους. Βεβαιωθείτε ότι έχετε ελέγξει τον καθορισμένο κατάλογο για το αρχείο εξόδου σας!

## Σύναψη
Και να το! Εφαρμόσατε με επιτυχία τη μορφοποίηση υπό όρους κατά τον χρόνο εκτέλεσης στο Excel χρησιμοποιώντας το Aspose.Cells για .NET. Αυτή η ισχυρή βιβλιοθήκη διευκολύνει τον προγραμματισμό αρχείων Excel, επιτρέποντάς σας να αυτοματοποιήσετε κουραστικές εργασίες και να βελτιώσετε τις παρουσιάσεις δεδομένων σας. Είτε εργάζεστε σε ένα μικρό έργο είτε σε μια εφαρμογή μεγάλης κλίμακας, το Aspose.Cells μπορεί να σας βοηθήσει να βελτιστοποιήσετε τη ροή εργασίας σας και να βελτιώσετε την παραγωγικότητά σας.

## Συχνές ερωτήσεις

### Τι είναι το Aspose.Cells;
Το Aspose.Cells είναι μια βιβλιοθήκη .NET που επιτρέπει στους προγραμματιστές να δημιουργούν, να χειρίζονται και να μετατρέπουν αρχεία Excel μέσω προγραμματισμού.

### Μπορώ να χρησιμοποιήσω το Aspose.Cells με άλλες γλώσσες προγραμματισμού;
Ναι, το Aspose.Cells είναι διαθέσιμο για πολλές γλώσσες προγραμματισμού, όπως Java, Python και άλλες.

### Υπάρχει διαθέσιμη δωρεάν δοκιμαστική έκδοση για το Aspose.Cells;
Ναι, μπορείτε να κατεβάσετε μια δωρεάν δοκιμαστική έκδοση από το [Ιστότοπος Aspose](https://releases.aspose.com/).

### Πώς μπορώ να λάβω υποστήριξη για το Aspose.Cells;
Μπορείτε να λάβετε υποστήριξη επισκεπτόμενοι την [Φόρουμ υποστήριξης Aspose](https://forum.aspose.com/c/cells/9).

### Χρειάζομαι άδεια χρήσης για να χρησιμοποιήσω το Aspose.Cells;
Ναι, απαιτείται άδεια για εμπορική χρήση, αλλά μπορείτε να ζητήσετε προσωρινή άδεια [εδώ](https://purchase.aspose.com/temporary-license/).


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}