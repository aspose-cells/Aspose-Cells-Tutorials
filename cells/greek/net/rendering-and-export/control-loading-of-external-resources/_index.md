---
title: Ελέγξτε τους εξωτερικούς πόρους στο Excel σε PDF στο Aspose.Cells
linktitle: Ελέγξτε τους εξωτερικούς πόρους στο Excel σε PDF στο Aspose.Cells
second_title: Aspose.Cells .NET Excel Processing API
description: Ανακαλύψτε πώς να ελέγχετε εξωτερικούς πόρους στη μετατροπή Excel σε PDF χρησιμοποιώντας το Aspose.Cells για .NET με τον εύκολο στην παρακολούθηση οδηγό μας.
weight: 12
url: /el/net/rendering-and-export/control-loading-of-external-resources/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ελέγξτε τους εξωτερικούς πόρους στο Excel σε PDF στο Aspose.Cells

## Εισαγωγή
Στη σημερινή ψηφιακή εποχή, η μετατροπή υπολογιστικών φύλλων του Excel σε έγγραφα PDF είναι μια συνηθισμένη εργασία. Είτε προετοιμάζετε αναφορές, οικονομικά δεδομένα ή υλικό παρουσίασης, θέλετε να βεβαιωθείτε ότι τα PDF σας φαίνονται ακριβώς όπως τα σκοπεύετε. Το Aspose.Cells για .NET είναι μια ισχυρή βιβλιοθήκη που σας επιτρέπει να ελέγχετε αυτήν τη διαδικασία μετατροπής μέχρι την τελευταία λεπτομέρεια, ειδικά όταν χειρίζεστε εξωτερικούς πόρους, όπως εικόνες που συνοδεύουν τα αρχεία σας Excel. Σε αυτόν τον οδηγό, εξετάζουμε τον τρόπο ελέγχου εξωτερικών πόρων κατά τη διαδικασία μετατροπής Excel σε PDF χρησιμοποιώντας το Aspose.Cells. Πάρτε, λοιπόν, το αγαπημένο σας ρόφημα και ας ξεκινήσουμε!
## Προαπαιτούμενα
Προτού πηδήξουμε στο νήμα, ας βεβαιωθούμε ότι έχετε ό,τι χρειάζεστε για να το κάνετε. Ακολουθεί μια γρήγορη λίστα ελέγχου:
1. Visual Studio ή οποιοδήποτε IDE συμβατό με .NET: Θα θέλετε ένα περιβάλλον για να γράψετε και να δοκιμάσετε τον κώδικά σας.
2.  Aspose.Cells για .NET: Εάν δεν το έχετε εγκαταστήσει ακόμα, μεταβείτε στο[Υποβολή λήψεων](https://releases.aspose.com/cells/net/) σελίδα και πάρτε την πιο πρόσφατη έκδοση.
3. Βασικές γνώσεις C#: Η εξοικείωση με τη γλώσσα προγραμματισμού C# θα είναι χρήσιμη. Εάν δεν είστε σίγουροι για κάποιες έννοιες, μη διστάσετε να τις αναζητήσετε.
4. Ένα δείγμα αρχείου Excel: Προετοιμάστε ένα αρχείο Excel με οποιουσδήποτε εξωτερικούς πόρους θέλετε να μετατρέψετε. Μπορείτε να χρησιμοποιήσετε το παρεχόμενο δείγμα αρχείου "samplePdfSaveOptions_StreamProvider.xlsx".
5. Ένα αρχείο εικόνας για δοκιμή: Αυτό θα χρησιμοποιηθεί ως εξωτερικός πόρος κατά τη μετατροπή. Το αρχείο εικόνας "newPdfSaveOptions_StreamProvider.png" είναι ένα καλό σύμβολο κράτησης θέσης.
## Εισαγωγή πακέτων
Για να ξεκινήσετε τα πράγματα, θα χρειαστεί να εισαγάγετε τους απαραίτητους χώρους ονομάτων από τη βιβλιοθήκη Aspose.Cells. Αυτό είναι κρίσιμο για την πρόσβαση στις λειτουργίες του. Βεβαιωθείτε ότι έχετε προσθέσει τα ακόλουθα χρησιμοποιώντας οδηγίες στην κορυφή του αρχείου σας:
```csharp
using System.IO;
using System.Drawing;
using System.Drawing.Imaging;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using Aspose.Cells.Rendering;
using System;
```
Αυτά τα πακέτα θα παρέχουν όλες τις βασικές κλάσεις και μεθόδους που θα χρειαστείτε για να εκτελέσετε τις εργασίες σας.
## Βήμα 1: Δημιουργήστε την τάξη του παρόχου ροής σας
 Η πρώτη σειρά εργασιών είναι να δημιουργήσετε μια κλάση παρόχου ροής που θα υλοποιεί το`IStreamProvider` διεπαφή. Αυτή η κλάση θα σας επιτρέψει να ελέγξετε τον τρόπο φόρτωσης εξωτερικών πόρων.
```csharp
class MyStreamProvider : IStreamProvider
{
    public void CloseStream(StreamProviderOptions options)
    {
        Debug.WriteLine("-----Close Stream-----");
    }
    public void InitStream(StreamProviderOptions options)
    {
        string sourceDir = "Your Document Directory";
        Debug.WriteLine("-----Init Stream-----");
        // Διαβάστε τη νέα εικόνα σε μια ροή μνήμης και αντιστοιχίστε την στην ιδιότητα Ροή
        byte[] bts = File.ReadAllBytes(sourceDir + "newPdfSaveOptions_StreamProvider.png");
        MemoryStream ms = new MemoryStream(bts);
        options.Stream = ms;
    }
}
```
Σε αυτή την τάξη:
- CloseStream: Αυτή η μέθοδος θα κληθεί όταν κλείσει η ροή. Προς το παρόν, γράφουμε απλώς ένα μήνυμα εντοπισμού σφαλμάτων για παρακολούθηση.
-  InitStream: Εδώ αρχίζει η μαγεία. Εδώ, θα διαβάσετε την εξωτερική σας εικόνα ως πίνακα byte, θα τη μετατρέψετε σε μια ροή μνήμης και θα την αντιστοιχίσετε στο`options.Stream` ιδιοκτησία.
## Βήμα 2: Ρύθμιση καταλόγων προέλευσης και εξόδου
Τώρα που ο πάροχος ροής σας είναι έτοιμος, ήρθε η ώρα να καθορίσετε πού βρίσκεται το αρχείο Excel και πού θέλετε να αποθηκεύσετε το PDF σας.
```csharp
// Κατάλογος πηγής
string sourceDir = "Your Document Directory";
// Κατάλογος εξόδου
string outputDir = "Your Document Directory";
```
 Απλώς αντικαταστήστε`"Your Document Directory"` με την πραγματική διαδρομή στον υπολογιστή σας όπου βρίσκονται τα αρχεία σας. Το να διατηρείτε τα αρχεία σας οργανωμένα είναι το κλειδί!
## Βήμα 3: Φορτώστε το αρχείο σας Excel
Στη συνέχεια, θα φορτώσετε το αρχείο Excel από το οποίο θέλετε να δημιουργήσετε το PDF.
```csharp
// Φορτώστε το αρχείο προέλευσης Excel που περιέχει εξωτερικές εικόνες
Workbook wb = new Workbook(sourceDir + "samplePdfSaveOptions_StreamProvider.xlsx");
```
 Χρησιμοποιούμε το`Workbook` κλάση από το Aspose.Cells, το οποίο αντιπροσωπεύει το αρχείο σας Excel. Το αρχείο μπορεί να περιλαμβάνει διάφορους εξωτερικούς πόρους, όπως εικόνες που θέλετε να ελέγξετε κατά τη μετατροπή.
## Βήμα 4: Ορίστε τις επιλογές αποθήκευσης PDF
Προτού αποθηκεύσετε το βιβλίο εργασίας ως PDF, ας καθορίσουμε πώς θέλετε να αποθηκευτεί. Μπορείτε να προσαρμόσετε αυτές τις επιλογές σύμφωνα με τις απαιτήσεις σας.
```csharp
// Καθορίστε Επιλογές αποθήκευσης Pdf - Πάροχος ροής
PdfSaveOptions opts = new PdfSaveOptions();
opts.OnePagePerSheet = true; // Αποθηκεύστε κάθε φύλλο σε μια νέα σελίδα
```
 Εδώ, δημιουργούμε μια νέα παρουσία του`PdfSaveOptions` , το οποίο σας επιτρέπει να προσαρμόσετε τον τρόπο με τον οποίο θα μορφοποιείται το PDF σας. Ο`OnePagePerSheet`Η επιλογή είναι εύχρηστη για να διασφαλίσετε ότι κάθε φύλλο Excel έχει τη δική του σελίδα στο τελικό PDF.
## Βήμα 5: Αναθέστε τον πάροχο ροής σας
Με τις επιλογές PDF που έχετε ορίσει, πρέπει να πείτε στην Aspose να χρησιμοποιήσει τον πάροχο προσαρμοσμένης ροής για εξωτερικούς πόρους.
```csharp
wb.Settings.StreamProvider = new MyStreamProvider();
```
 Αυτή η γραμμή σας συνδέει`Workbook` παράδειγμα με το`MyStreamProvider` τάξη που δημιουργήσατε νωρίτερα. Αυτό σημαίνει ότι κάθε φορά που συναντώνται εξωτερικοί πόροι κατά τη μετατροπή, ο πάροχος θα τους χειρίζεται όπως καθορίζεται.
## Βήμα 6: Αποθηκεύστε το βιβλίο εργασίας ως PDF
Έχοντας όλα έτοιμα, ήρθε επιτέλους η ώρα να αποθηκεύσετε το βιβλίο εργασίας του Excel ως PDF.
```csharp
// Αποθηκεύστε το βιβλίο εργασίας σε Pdf
wb.Save(outputDir + "outputPdfSaveOptions_StreamProvider.pdf", opts);
```
 Καλώντας το`Save` μέθοδο στο αντικείμενο του βιβλίου εργασίας και περνώντας στον κατάλογο εξόδου σας μαζί με τις επιλογές PDF, μετατρέπετε το αρχείο Excel σε ένα όμορφα διαμορφωμένο PDF.
## Βήμα 7: Επιβεβαιώστε την επιτυχή εκτέλεση
Για να ολοκληρώσουμε τα πράγματα, είναι πάντα ωραίο να επιβεβαιώνεις ότι η διαδικασία σου ήταν επιτυχής!
```csharp
Console.WriteLine("ControlLoadingOfExternalResourcesInExcelToPDF executed successfully.\r\n");
```
Η εκτύπωση ενός μηνύματος επιτυχίας στην κονσόλα σας βοηθά να κρατάτε ενήμερους για την κατάσταση της λειτουργίας σας. Είναι καλή συνήθεια να συμπεριλαμβάνετε αυτές τις μικρές επιβεβαιώσεις στον κώδικά σας.
## Σύναψη
Ορίστε το! Ακολουθώντας αυτά τα απλά βήματα, μπορείτε να ελέγχετε με έμπειρο τρόπο τον χειρισμό των εξωτερικών πόρων κατά τις μετατροπές Excel σε PDF χρησιμοποιώντας το Aspose.Cells. Αυτό σημαίνει ότι τα έγγραφά σας μπορούν πλέον να περιλαμβάνουν εικόνες και άλλα εξωτερικά στοιχεία με ακρίβεια, διασφαλίζοντας ένα γυαλισμένο τελικό προϊόν κάθε φορά.
## Συχνές ερωτήσεις
### Τι είναι το Aspose.Cells;  
Το Aspose.Cells είναι μια ισχυρή βιβλιοθήκη για προγραμματιστές .NET που σας επιτρέπει να δημιουργείτε, να χειρίζεστε, να μετατρέπετε και να αποδίδετε αρχεία Excel σε διάφορες μορφές.
### Πώς μπορώ να κατεβάσω το Aspose.Cells;  
 Μπορείτε να κάνετε λήψη της πιο πρόσφατης έκδοσης του Aspose.Cells από το[Σύνδεσμος λήψης](https://releases.aspose.com/cells/net/).
### Μπορώ να δοκιμάσω το Aspose.Cells δωρεάν;  
 Ναί! Μπορείτε να λάβετε μια δωρεάν δοκιμή επισκεπτόμενοι το[Δωρεάν δοκιμαστική σελίδα](https://releases.aspose.com/).
### Πού μπορώ να βρω υποστήριξη για το Aspose.Cells;  
 Για οποιαδήποτε απορία σχετικά με την υποστήριξη, μπορείτε να επισκεφθείτε τη διεύθυνση[Φόρουμ υποστήριξης Aspose](https://forum.aspose.com/c/cells/9).
### Πώς μπορώ να αποκτήσω μια προσωρινή άδεια για το Aspose.Cells;  
 Μπορείτε να κάνετε αίτηση για προσωρινή άδεια[εδώ](https://purchase.aspose.com/temporary-license/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
