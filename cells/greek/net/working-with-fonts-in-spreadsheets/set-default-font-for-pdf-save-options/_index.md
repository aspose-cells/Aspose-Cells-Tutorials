---
title: Ορίστε την προεπιλεγμένη γραμματοσειρά για τις επιλογές αποθήκευσης PDF
linktitle: Ορίστε την προεπιλεγμένη γραμματοσειρά για τις επιλογές αποθήκευσης PDF
second_title: Aspose.Cells .NET Excel Processing API
description: Μάθετε πώς να ορίζετε προεπιλεγμένες γραμματοσειρές για επιλογές αποθήκευσης PDF χρησιμοποιώντας το Aspose.Cells για .NET, διασφαλίζοντας ότι τα έγγραφά σας φαίνονται τέλεια κάθε φορά.
weight: 11
url: /el/net/working-with-fonts-in-spreadsheets/set-default-font-for-pdf-save-options/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ορίστε την προεπιλεγμένη γραμματοσειρά για τις επιλογές αποθήκευσης PDF

## Εισαγωγή
Όταν πρόκειται για τη δημιουργία αναφορών, τιμολογίων ή οποιωνδήποτε άλλων εγγράφων σε μορφή PDF, η διασφάλιση ότι το περιεχόμενό σας φαίνεται σωστά είναι πρωταρχικής σημασίας. Οι γραμματοσειρές διαδραματίζουν ζωτικό ρόλο στη διατήρηση της οπτικής ελκυστικότητας και της αναγνωσιμότητας των εγγράφων σας. Ωστόσο, τι συμβαίνει όταν η γραμματοσειρά που χρησιμοποιήσατε στο αρχείο Excel δεν είναι διαθέσιμη στο σύστημα όπου δημιουργείτε το PDF σας; Εκεί είναι χρήσιμο το Aspose.Cells για .NET. Αυτή η ισχυρή βιβλιοθήκη σάς επιτρέπει να ορίσετε προεπιλεγμένες γραμματοσειρές για τις επιλογές αποθήκευσης PDF, διασφαλίζοντας ότι τα έγγραφά σας φαίνονται επαγγελματικά και συνεπή, ανεξάρτητα από το πού ανοίγονται.
## Προαπαιτούμενα
Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε τα εξής:
1. Visual Studio: Θα χρειαστείτε ένα περιβάλλον ανάπτυξης όπως το Visual Studio για να γράψετε και να εκτελέσετε τον κώδικά σας.
2.  Aspose.Cells για .NET: Μπορείτε να κάνετε λήψη της πιο πρόσφατης έκδοσης από[αυτόν τον σύνδεσμο](https://releases.aspose.com/cells/net/). Εναλλακτικά, μπορείτε να το εγκαταστήσετε μέσω του NuGet Package Manager στο Visual Studio.
3. Βασική γνώση της C#: Η κατανόηση των βασικών της C# θα σας βοηθήσει να ακολουθήσετε μαζί με τα παραδείγματα κώδικα.
4. Δείγμα αρχείου Excel: Έχετε ένα δείγμα αρχείου Excel έτοιμο για δοκιμή. Μπορείτε να δημιουργήσετε ένα με διάφορες γραμματοσειρές και στυλ για να δείτε πώς το Aspose.Cells χειρίζεται τις γραμματοσειρές που λείπουν.
## Εισαγωγή πακέτων
Για να μπορέσετε να χρησιμοποιήσετε το Aspose.Cells στο έργο σας, πρέπει να εισαγάγετε τα απαραίτητα πακέτα. Δείτε πώς να το κάνετε:
1. Ανοίξτε το έργο σας: Εκκινήστε το Visual Studio και ανοίξτε το υπάρχον έργο σας ή δημιουργήστε ένα νέο.
2. Προσθήκη αναφορών: Κάντε δεξί κλικ στο έργο σας στην Εξερεύνηση λύσεων και επιλέξτε "Διαχείριση πακέτων NuGet".
3. Install Aspose.Cells: Αναζητήστε το "Aspose.Cells" και κάντε κλικ στο κουμπί "Install".
4. Προσθήκη με χρήση οδηγιών: Στην κορυφή του αρχείου C#, συμπεριλάβετε τους ακόλουθους χώρους ονομάτων:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;
```
## Βήμα 1: Ρυθμίστε τους καταλόγους σας
Πριν εργαστείτε με αρχεία, είναι σημαντικό να ορίσετε τους καταλόγους προέλευσης και εξόδου. Αυτό θα διευκολύνει τον εντοπισμό του αρχείου εισόδου Excel και την αποθήκευση των δημιουργηθέντων αρχείων εξόδου.
```csharp
// Κατάλογος πηγής
string sourceDir = "Your Document Directory";
// Κατάλογος εξόδου
string outputDir = "Your Document Directory";
```
 Αντικαθιστώ`"Your Document Directory"` με την πραγματική διαδρομή προς τους καταλόγους σας.
## Βήμα 2: Ανοίξτε το Αρχείο Excel
 Τώρα που έχουμε ρυθμίσει τους καταλόγους μας, ας ανοίξουμε το αρχείο Excel με το οποίο θέλετε να εργαστείτε. Ο`Workbook` Η κλάση στο Aspose.Cells χρησιμοποιείται για τη φόρτωση του εγγράφου του Excel.
```csharp
// Ανοίξτε ένα αρχείο Excel
Workbook workbook = new Workbook(sourceDir + "sampleSetDefaultFontPropertyOfPdfSaveOptionsAndImageOrPrintOptions.xlsx");
```
Βεβαιωθείτε ότι έχετε αντικαταστήσει το όνομα αρχείου με το πραγματικό όνομα του αρχείου σας.
## Βήμα 3: Ρυθμίστε τις επιλογές απόδοσης εικόνας
Στη συνέχεια, πρέπει να διαμορφώσουμε τις επιλογές απόδοσης για τη μετατροπή του φύλλου Excel σε μορφή εικόνας. Θα δημιουργήσουμε ένα παράδειγμα του`ImageOrPrintOptions`, καθορίζοντας τον τύπο εικόνας και την προεπιλεγμένη γραμματοσειρά.
```csharp
// Απόδοση σε μορφή αρχείου PNG
ImageOrPrintOptions imgOpt = new ImageOrPrintOptions();
imgOpt.ImageType = Drawing.ImageType.Png;
imgOpt.CheckWorkbookDefaultFont = false;
imgOpt.DefaultFont = "Times New Roman";
```
 Σε αυτό το απόσπασμα κώδικα, ορίζουμε το`CheckWorkbookDefaultFont` ιδιοκτησία σε`false`, πράγμα που σημαίνει ότι εάν λείπουν γραμματοσειρές, θα χρησιμοποιηθεί η καθορισμένη προεπιλεγμένη γραμματοσειρά ("Times New Roman").
## Βήμα 4: Αποδώστε το φύλλο ως εικόνα
 Τώρα, ας αποδώσουμε το πρώτο φύλλο του βιβλίου εργασίας ως εικόνα PNG. Θα χρησιμοποιήσουμε το`SheetRender` τάξη για να το πετύχει αυτό.
```csharp
// Αποδώστε το πρώτο φύλλο εργασίας σε μια εικόνα
SheetRender sr = new SheetRender(workbook.Worksheets[0], imgOpt);
sr.ToImage(0, outputDir + "out1_imagePNG.png");
```
## Βήμα 5: Αλλάξτε τον τύπο εικόνας και την απόδοση σε TIFF
 Εάν θέλετε να αποδώσετε το ίδιο φύλλο σε διαφορετική μορφή εικόνας, όπως το TIFF, μπορείτε απλώς να το αλλάξετε`ImageType` ιδιοκτησία και επαναλάβετε τη διαδικασία απόδοσης.
```csharp
// Ρυθμίστε σε μορφή TIFF
imgOpt.ImageType = Drawing.ImageType.Tiff;
WorkbookRender wr = new WorkbookRender(workbook, imgOpt);
wr.ToImage(outputDir + "out1_imageTIFF.tiff");
```
## Βήμα 6: Διαμόρφωση επιλογών αποθήκευσης PDF
 Στη συνέχεια, ας ρυθμίσουμε τις επιλογές αποθήκευσης PDF. Θα δημιουργήσουμε ένα παράδειγμα του`PdfSaveOptions`ορίστε την προεπιλεγμένη γραμματοσειρά και καθορίστε ότι θέλουμε να ελέγξουμε για γραμματοσειρές που λείπουν.
```csharp
// Διαμόρφωση επιλογών αποθήκευσης PDF
PdfSaveOptions saveOptions = new PdfSaveOptions();
saveOptions.DefaultFont = "Times New Roman";
saveOptions.CheckWorkbookDefaultFont = false;
```
## Βήμα 7: Αποθηκεύστε το βιβλίο εργασίας ως PDF
Με τις επιλογές αποθήκευσης διαμορφωμένες, ήρθε η ώρα να αποθηκεύσετε το βιβλίο εργασίας του Excel ως αρχείο PDF. 
```csharp
// Αποθηκεύστε το βιβλίο εργασίας σε PDF
workbook.Save(outputDir + "out1_pdf.pdf", saveOptions);
```
## Βήμα 8: Επιβεβαιώστε την εκτέλεση
Τέλος, είναι καλή πρακτική να ενημερώνετε τον χρήστη ότι η διαδικασία ολοκληρώθηκε με επιτυχία. Μπορείτε να το πετύχετε χρησιμοποιώντας ένα απλό μήνυμα κονσόλας.
```csharp
Console.WriteLine("SetDefaultFontPropertyOfPdfSaveOptionsAndImageOrPrintOptions executed successfully.\r\n");
```
## Σύναψη
Το Aspose.Cells παρέχει έναν ευέλικτο και ισχυρό τρόπο χειρισμού αρχείων Excel, διευκολύνοντας τους προγραμματιστές να δημιουργούν οπτικά ελκυστικά έγγραφα που διατηρούν τη μορφοποίησή τους. Είτε εργάζεστε σε αναφορές, οικονομικά έγγραφα ή οποιαδήποτε άλλη μορφή παρουσίασης δεδομένων, ο έλεγχος της απόδοσης γραμματοσειρών μπορεί να βελτιώσει σημαντικά την ποιότητα των αποτελεσμάτων σας.
## Συχνές ερωτήσεις
### Τι είναι το Aspose.Cells;
Το Aspose.Cells είναι μια ισχυρή βιβλιοθήκη .NET που επιτρέπει στους προγραμματιστές να χειρίζονται αρχεία Excel χωρίς να χρειάζεται εγκατάσταση του Microsoft Excel. Υποστηρίζει διάφορες μορφές αρχείων και προσφέρει πλούσιες δυνατότητες για εργασία με υπολογιστικά φύλλα.
### Πώς μπορώ να ορίσω μια προεπιλεγμένη γραμματοσειρά για τα αρχεία μου Excel;
 Μπορείτε να ορίσετε μια προεπιλεγμένη γραμματοσειρά χρησιμοποιώντας το`PdfSaveOptions` τάξη και καθορίστε το επιθυμητό όνομα γραμματοσειράς. Αυτό διασφαλίζει ότι ακόμη και αν λείπει μια γραμματοσειρά, το έγγραφό σας θα χρησιμοποιεί την προεπιλεγμένη γραμματοσειρά που έχετε καθορίσει.
### Μπορώ να μετατρέψω αρχεία Excel σε άλλες μορφές εκτός από το PDF;
Απολύτως! Το Aspose.Cells σάς επιτρέπει να μετατρέπετε αρχεία Excel σε διάφορες μορφές, συμπεριλαμβανομένων εικόνων (PNG, TIFF), HTML, CSV και άλλων.
### Είναι το Aspose.Cells δωρεάν για χρήση;
Το Aspose.Cells είναι ένα εμπορικό προϊόν, αλλά μπορείτε να το δοκιμάσετε δωρεάν με μια περιορισμένη δοκιμαστική έκδοση. Για πλήρη λειτουργικότητα, θα χρειαστεί να αγοράσετε μια άδεια.
### Πού μπορώ να βρω υποστήριξη για το Aspose.Cells;
 Μπορείτε να βρείτε υποστήριξη για το Aspose.Cells μεταβαίνοντας στο[Aspose φόρουμ](https://forum.aspose.com/c/cells/9), όπου μπορείτε να κάνετε ερωτήσεις και να μοιραστείτε πληροφορίες με άλλους χρήστες και προγραμματιστές.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
