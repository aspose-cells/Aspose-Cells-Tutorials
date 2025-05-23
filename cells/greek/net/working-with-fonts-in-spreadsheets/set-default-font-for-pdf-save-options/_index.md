---
"description": "Μάθετε πώς να ορίζετε προεπιλεγμένες γραμματοσειρές για τις επιλογές αποθήκευσης PDF χρησιμοποιώντας το Aspose.Cells για .NET, διασφαλίζοντας ότι τα έγγραφά σας φαίνονται τέλεια κάθε φορά."
"linktitle": "Ορισμός προεπιλεγμένης γραμματοσειράς για επιλογές αποθήκευσης PDF"
"second_title": "API επεξεργασίας Excel Aspose.Cells .NET"
"title": "Ορισμός προεπιλεγμένης γραμματοσειράς για επιλογές αποθήκευσης PDF"
"url": "/el/net/working-with-fonts-in-spreadsheets/set-default-font-for-pdf-save-options/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Ορισμός προεπιλεγμένης γραμματοσειράς για επιλογές αποθήκευσης PDF

## Εισαγωγή
Όσον αφορά τη δημιουργία αναφορών, τιμολογίων ή οποιωνδήποτε άλλων εγγράφων σε μορφή PDF, η διασφάλιση της σωστής εμφάνισης του περιεχομένου σας είναι ύψιστης σημασίας. Οι γραμματοσειρές παίζουν ζωτικό ρόλο στη διατήρηση της οπτικής ελκυστικότητας και της αναγνωσιμότητας των εγγράφων σας. Ωστόσο, τι συμβαίνει όταν η γραμματοσειρά που χρησιμοποιήσατε στο αρχείο Excel δεν είναι διαθέσιμη στο σύστημα όπου δημιουργείτε το PDF σας; Εδώ είναι που το Aspose.Cells για .NET είναι χρήσιμο. Αυτή η ισχυρή βιβλιοθήκη σάς επιτρέπει να ορίσετε προεπιλεγμένες γραμματοσειρές για τις επιλογές αποθήκευσης PDF, διασφαλίζοντας ότι τα έγγραφά σας φαίνονται επαγγελματικά και συνεπή, ανεξάρτητα από το πού ανοίγονται.
## Προαπαιτούμενα
Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε τα εξής:
1. Visual Studio: Θα χρειαστείτε ένα περιβάλλον ανάπτυξης όπως το Visual Studio για να γράψετε και να εκτελέσετε τον κώδικά σας.
2. Aspose.Cells για .NET: Μπορείτε να κατεβάσετε την πιο πρόσφατη έκδοση από [αυτός ο σύνδεσμος](https://releases.aspose.com/cells/net/)Εναλλακτικά, μπορείτε να το εγκαταστήσετε μέσω του NuGet Package Manager στο Visual Studio.
3. Βασικές γνώσεις C#: Η κατανόηση των βασικών στοιχείων της C# θα σας βοηθήσει να παρακολουθήσετε τα παραδείγματα κώδικα.
4. Δείγμα αρχείου Excel: Έχετε ένα δείγμα αρχείου Excel έτοιμο για δοκιμή. Μπορείτε να δημιουργήσετε ένα με διάφορες γραμματοσειρές και στυλ για να δείτε πώς το Aspose.Cells χειρίζεται τις γραμματοσειρές που λείπουν.
## Εισαγωγή πακέτων
Πριν μπορέσετε να χρησιμοποιήσετε το Aspose.Cells στο έργο σας, πρέπει να εισαγάγετε τα απαραίτητα πακέτα. Δείτε πώς μπορείτε να το κάνετε:
1. Άνοιγμα του έργου σας: Εκκινήστε το Visual Studio και ανοίξτε το υπάρχον έργο σας ή δημιουργήστε ένα νέο.
2. Προσθήκη αναφορών: Κάντε δεξί κλικ στο έργο σας στην Εξερεύνηση λύσεων και επιλέξτε "Διαχείριση πακέτων NuGet".
3. Εγκατάσταση Aspose.Cells: Αναζητήστε "Aspose.Cells" και κάντε κλικ στο κουμπί "Εγκατάσταση".
4. Προσθήκη οδηγιών χρήσης: Στο επάνω μέρος του αρχείου C#, συμπεριλάβετε τους ακόλουθους χώρους ονομάτων:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;
```
## Βήμα 1: Ρύθμιση των καταλόγων σας
Πριν από την εργασία με αρχεία, είναι σημαντικό να ορίσετε τους καταλόγους προέλευσης και εξόδου. Αυτό θα διευκολύνει τον εντοπισμό του αρχείου εισόδου Excel και την αποθήκευση των δημιουργημένων αρχείων εξόδου.
```csharp
// Κατάλογος πηγής
string sourceDir = "Your Document Directory";
// Κατάλογος εξόδου
string outputDir = "Your Document Directory";
```
Αντικαθιστώ `"Your Document Directory"` με την πραγματική διαδρομή προς τους καταλόγους σας.
## Βήμα 2: Ανοίξτε το αρχείο Excel
Τώρα που έχουμε ρυθμίσει τους καταλόγους μας, ας ανοίξουμε το αρχείο Excel με το οποίο θέλετε να εργαστείτε. `Workbook` Η κλάση στο Aspose.Cells χρησιμοποιείται για τη φόρτωση του εγγράφου Excel.
```csharp
// Άνοιγμα αρχείου Excel
Workbook workbook = new Workbook(sourceDir + "sampleSetDefaultFontPropertyOfPdfSaveOptionsAndImageOrPrintOptions.xlsx");
```
Βεβαιωθείτε ότι έχετε αντικαταστήσει το όνομα αρχείου με το πραγματικό σας όνομα αρχείου.
## Βήμα 3: Ρύθμιση επιλογών απόδοσης εικόνας
Στη συνέχεια, πρέπει να διαμορφώσουμε τις επιλογές απόδοσης για τη μετατροπή του φύλλου Excel σε μορφή εικόνας. Θα δημιουργήσουμε μια παρουσία του `ImageOrPrintOptions`, καθορίζοντας τον τύπο εικόνας και την προεπιλεγμένη γραμματοσειρά.
```csharp
// Απόδοση σε μορφή αρχείου PNG
ImageOrPrintOptions imgOpt = new ImageOrPrintOptions();
imgOpt.ImageType = Drawing.ImageType.Png;
imgOpt.CheckWorkbookDefaultFont = false;
imgOpt.DefaultFont = "Times New Roman";
```
Σε αυτό το απόσπασμα κώδικα, ορίζουμε το `CheckWorkbookDefaultFont` ιδιοκτησία σε `false`πράγμα που σημαίνει ότι εάν λείπουν γραμματοσειρές, θα χρησιμοποιηθεί η καθορισμένη προεπιλεγμένη γραμματοσειρά ("Times New Roman").
## Βήμα 4: Απόδοση του φύλλου ως εικόνας
Τώρα, ας αποδώσουμε το πρώτο φύλλο του βιβλίου εργασίας ως εικόνα PNG. Θα χρησιμοποιήσουμε το `SheetRender` τάξη για να το πετύχει αυτό.
```csharp
// Απόδοση του πρώτου φύλλου εργασίας σε εικόνα
SheetRender sr = new SheetRender(workbook.Worksheets[0], imgOpt);
sr.ToImage(0, outputDir + "out1_imagePNG.png");
```
## Βήμα 5: Αλλαγή τύπου εικόνας και απόδοση σε TIFF
Αν θέλετε να αποδώσετε το ίδιο φύλλο σε διαφορετική μορφή εικόνας, όπως TIFF, μπορείτε απλώς να αλλάξετε το `ImageType` ιδιότητα και επαναλάβετε τη διαδικασία απόδοσης.
```csharp
// Ορισμός σε μορφή TIFF
imgOpt.ImageType = Drawing.ImageType.Tiff;
WorkbookRender wr = new WorkbookRender(workbook, imgOpt);
wr.ToImage(outputDir + "out1_imageTIFF.tiff");
```
## Βήμα 6: Ρύθμιση παραμέτρων επιλογών αποθήκευσης PDF
Στη συνέχεια, ας ρυθμίσουμε τις επιλογές αποθήκευσης PDF. Θα δημιουργήσουμε μια παρουσία του `PdfSaveOptions`, ορίστε την προεπιλεγμένη γραμματοσειρά και καθορίστε ότι θέλουμε να ελέγξουμε για γραμματοσειρές που λείπουν.
```csharp
// Ρύθμιση παραμέτρων επιλογών αποθήκευσης PDF
PdfSaveOptions saveOptions = new PdfSaveOptions();
saveOptions.DefaultFont = "Times New Roman";
saveOptions.CheckWorkbookDefaultFont = false;
```
## Βήμα 7: Αποθήκευση του βιβλίου εργασίας ως PDF
Αφού έχετε ρυθμίσει τις επιλογές αποθήκευσης, ήρθε η ώρα να αποθηκεύσουμε το βιβλίο εργασίας του Excel ως αρχείο PDF. 
```csharp
// Αποθήκευση του βιβλίου εργασίας σε μορφή PDF
workbook.Save(outputDir + "out1_pdf.pdf", saveOptions);
```
## Βήμα 8: Επιβεβαίωση εκτέλεσης
Τέλος, είναι καλή πρακτική να ενημερώνετε τον χρήστη ότι η διαδικασία ολοκληρώθηκε με επιτυχία. Μπορείτε να το πετύχετε αυτό χρησιμοποιώντας ένα απλό μήνυμα κονσόλας.
```csharp
Console.WriteLine("SetDefaultFontPropertyOfPdfSaveOptionsAndImageOrPrintOptions executed successfully.\r\n");
```
## Σύναψη
Το Aspose.Cells παρέχει έναν ευέλικτο και ισχυρό τρόπο χειρισμού των χειρισμών αρχείων Excel, διευκολύνοντας τους προγραμματιστές να δημιουργούν οπτικά ελκυστικά έγγραφα που διατηρούν τη μορφοποίησή τους. Είτε εργάζεστε σε αναφορές, οικονομικά έγγραφα είτε σε οποιαδήποτε άλλη μορφή παρουσίασης δεδομένων, ο έλεγχος της απόδοσης των γραμματοσειρών μπορεί να βελτιώσει σημαντικά την ποιότητα του αποτελέσματος.
## Συχνές ερωτήσεις
### Τι είναι το Aspose.Cells;
Το Aspose.Cells είναι μια ισχυρή βιβλιοθήκη .NET που επιτρέπει στους προγραμματιστές να χειρίζονται αρχεία Excel χωρίς να χρειάζεται να εγκατασταθεί το Microsoft Excel. Υποστηρίζει διάφορες μορφές αρχείων και προσφέρει πλούσιες δυνατότητες για εργασία με υπολογιστικά φύλλα.
### Πώς μπορώ να ορίσω μια προεπιλεγμένη γραμματοσειρά για τα αρχεία Excel μου;
Μπορείτε να ορίσετε μια προεπιλεγμένη γραμματοσειρά χρησιμοποιώντας το `PdfSaveOptions` κλάση και καθορίστε το επιθυμητό όνομα γραμματοσειράς. Αυτό διασφαλίζει ότι ακόμα και αν λείπει μια γραμματοσειρά, το έγγραφό σας θα χρησιμοποιήσει την προεπιλεγμένη γραμματοσειρά που έχετε καθορίσει.
### Μπορώ να μετατρέψω αρχεία Excel σε μορφές εκτός από PDF;
Απολύτως! Το Aspose.Cells σάς επιτρέπει να μετατρέψετε αρχεία Excel σε διάφορες μορφές, όπως εικόνες (PNG, TIFF), HTML, CSV και άλλα.
### Είναι το Aspose.Cells δωρεάν στη χρήση;
Το Aspose.Cells είναι ένα εμπορικό προϊόν, αλλά μπορείτε να το δοκιμάσετε δωρεάν με μια περιορισμένη δοκιμαστική έκδοση. Για πλήρη λειτουργικότητα, θα χρειαστεί να αγοράσετε μια άδεια χρήσης.
### Πού μπορώ να βρω υποστήριξη για το Aspose.Cells;
Μπορείτε να βρείτε υποστήριξη για το Aspose.Cells μεταβαίνοντας στο [Φόρουμ Aspose](https://forum.aspose.com/c/cells/9), όπου μπορείτε να κάνετε ερωτήσεις και να μοιραστείτε πληροφορίες με άλλους χρήστες και προγραμματιστές.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}