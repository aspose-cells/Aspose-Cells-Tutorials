---
"description": "Μάθετε πώς να προσθέτετε εύκολα εικόνες σε γραφήματα Excel χρησιμοποιώντας το Aspose.Cells για .NET. Βελτιώστε τα γραφήματα και τις παρουσιάσεις σας σε λίγα μόνο απλά βήματα."
"linktitle": "Προσθήκη εικόνας σε γράφημα"
"second_title": "API επεξεργασίας Excel Aspose.Cells .NET"
"title": "Προσθήκη εικόνας σε γράφημα"
"url": "/el/net/inserting-controls-in-charts/add-picture-to-chart/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Προσθήκη εικόνας σε γράφημα

## Εισαγωγή

Έχετε κουραστεί από τα βαρετά γραφήματα που δεν έχουν προσωπική πινελιά; Θέλετε να μάθετε πώς να δώσετε μια πιο ζωηρή πινελιά στα γραφήματα του Excel προσθέτοντας εικόνες; Λοιπόν, είστε τυχεροί! Σε αυτό το σεμινάριο, θα βυθιστούμε στον κόσμο του Aspose.Cells για .NET και θα μάθουμε πώς να προσθέτουμε εικόνες σε γραφήματα στο Excel. Πάρτε λοιπόν το αγαπημένο σας φλιτζάνι καφέ και ας ξεκινήσουμε!

## Προαπαιτούμενα

Πριν μπούμε στα πιο απλά πράγματα της κωδικοποίησης, υπάρχουν μερικές προϋποθέσεις που πρέπει να έχετε για να τις ακολουθήσετε ομαλά:

- Visual Studio: Εδώ θα γράψετε και θα εκτελέσετε τον κώδικα .NET. Βεβαιωθείτε ότι τον έχετε εγκαταστήσει.
- Aspose.Cells για .NET: Θα χρειαστείτε αυτήν τη βιβλιοθήκη για να εργαστείτε με αρχεία Excel. Μπορείτε [κατεβάστε το εδώ](https://releases.aspose.com/cells/net/).
- Βασική Κατανόηση της C#: Ενώ θα σας καθοδηγήσω στον κώδικα, η κατανόηση των βασικών στοιχείων της C# θα σας κάνει τα πράγματα πιο ξεκάθαρα.

### Βήματα εγκατάστασης

1. Εγκατάσταση Aspose.Cells: Μπορείτε να προσθέσετε το Aspose.Cells στο έργο σας στο Visual Studio μέσω του NuGet Package Manager. Για να το κάνετε αυτό, μεταβείτε στα Εργαλεία > NuGet Package Manager > Διαχείριση πακέτων NuGet για λύση και αναζητήστε το "Aspose.Cells". Κάντε κλικ στην επιλογή Εγκατάσταση.
2. Ρύθμιση του έργου σας: Δημιουργήστε ένα νέο έργο εφαρμογής κονσόλας C# στο Visual Studio.

## Εισαγωγή πακέτων

Μόλις ολοκληρώσετε τις ρυθμίσεις, το επόμενο βήμα είναι να εισαγάγετε τα απαραίτητα πακέτα στο έργο σας. Δείτε πώς μπορείτε να το κάνετε:

### Εισαγωγή των απαιτούμενων χώρων ονομάτων

Στο επάνω μέρος του αρχείου κώδικα C#, θα χρειαστεί να εισαγάγετε τους ακόλουθους χώρους ονομάτων:

```csharp
using Aspose.Cells;
using Aspose.Cells.Charts;
using Aspose.Cells.Drawing;
using System.IO;
```

Αυτό λέει στο πρόγραμμά σας, "Γεια! Θα χρησιμοποιήσω αυτές τις ωραίες λειτουργίες από το Aspose.Cells."

Τώρα που έχουμε θέσει τις προϋποθέσεις, ας χωρίσουμε τη διαδικασία σε σύντομα βήματα. 

## Βήμα 1: Ορίστε τους καταλόγους σας

Πρώτα απ 'όλα, πρέπει να ορίσουμε τις διαδρομές για τα αρχεία εισόδου και εξόδου. Αυτό το βήμα είναι κρίσιμο επειδή πρέπει να γνωρίζουμε πού θα βρούμε το υπάρχον αρχείο Excel και πού θα αποθηκεύσουμε το τροποποιημένο αρχείο.

```csharp
//Κατάλογος πηγής
string sourceDir = "Your Document Directory/";

//Κατάλογος εξόδου
string outputDir = "Your Output Directory/";
```

Αντικαθιστώ `Your Document Directory` και `Your Output Directory` με πραγματικές διαδρομές στον υπολογιστή σας. 

## Βήμα 2: Φόρτωση του υπάρχοντος βιβλίου εργασίας

Τώρα, ας φορτώσουμε το υπάρχον αρχείο Excel όπου θέλουμε να προσθέσουμε την εικόνα μας στο γράφημα.

```csharp
// Ανοίξτε το υπάρχον αρχείο.
Workbook workbook = new Workbook(sourceDir + "sampleAddingPictureInChart.xls");
```

Αυτός ο κώδικας ανοίγει το βιβλίο εργασίας, καθιστώντας το έτοιμο για επεξεργασία.

## Βήμα 3: Προετοιμασία της ροής εικόνας

Πριν προσθέσουμε την εικόνα, πρέπει να διαβάσουμε την εικόνα που θέλουμε να εισαγάγουμε στο γράφημα. 

```csharp
// Μεταφέρετε ένα αρχείο εικόνας στη ροή.
FileStream stream = new FileStream(sourceDir + "sampleAddingPictureInChart.png", FileMode.Open, FileAccess.Read);
```

Βεβαιωθείτε ότι έχετε αποθηκεύσει την εικόνα στον καθορισμένο κατάλογο.

## Βήμα 4: Στοχεύστε το γράφημα

Τώρα, ας καθορίσουμε σε ποιο γράφημα θα προσθέσουμε την εικόνα μας. Σε αυτό το παράδειγμα, θα στοχεύσουμε το πρώτο γράφημα στο πρώτο φύλλο εργασίας.

```csharp
// Αποκτήστε το διάγραμμα σχεδιαστή στο δεύτερο φύλλο.
Worksheet sheet = workbook.Worksheets[0];
Aspose.Cells.Charts.Chart chart = sheet.Charts[0];
```

Μπορείτε να αποκτήσετε πρόσβαση σε οποιοδήποτε φύλλο εργασίας αλλάζοντας ανάλογα το ευρετήριο.

## Βήμα 5: Προσθήκη της εικόνας στο διάγραμμα

Αφού επιλέξατε το γράφημα, ήρθε η ώρα να προσθέσετε την εικόνα! 

```csharp
// Προσθέστε μια νέα εικόνα στο γράφημα.
Aspose.Cells.Drawing.Picture pic0 = chart.Shapes.AddPictureInChart(50, 50, stream, 200, 200);
```

Εδώ, `50` και `50` είναι οι συντεταγμένες X και Y όπου θα τοποθετηθεί η εικόνα, και `200` είναι το πλάτος και το ύψος της εικόνας.

## Βήμα 6: Προσαρμόστε τη μορφή γραμμής της εικόνας

Θέλετε να προσθέσετε λίγη πινελιά στην εικόνα σας; Μπορείτε να προσαρμόσετε το περίγραμμά της! Δείτε πώς μπορείτε να το κάνετε:

```csharp
// Λάβετε τον τύπο μορφής γραμμής της εικόνας.
Aspose.Cells.Drawing.LineFormat lineformat = pic0.Line; 

// Ορίστε το στυλ παύλας.
lineformat.DashStyle = MsoLineDashStyle.Solid;

// Ορίστε το πάχος της γραμμής.
lineformat.Weight = 4;    
```

Αυτό το απόσπασμα σάς επιτρέπει να επιλέξετε πώς θα φαίνεται το περίγραμμα και πόσο πάχος θα είναι. Επιλέξτε οποιοδήποτε στυλ ταιριάζει με την παρουσίασή σας!

## Βήμα 7: Αποθήκευση του τροποποιημένου βιβλίου εργασίας

Μετά από όλη αυτή τη σκληρή δουλειά, ας αποθηκεύσουμε τις τροποποιήσεις σας εκτελώντας την ακόλουθη γραμμή κώδικα:

```csharp
// Αποθηκεύστε το αρχείο excel.
workbook.Save(outputDir + "outputAddingPictureInChart.xls");
```

Τώρα η εικόνα σας έχει ενσωματωθεί με επιτυχία στο διάγραμμα και το αρχείο εξόδου σας είναι έτοιμο για προβολή!

## Βήμα 8: Υποδείξτε την επιτυχία

Τέλος, μπορείτε να προσθέσετε ένα απλό μήνυμα για να επιβεβαιώσετε ότι η λειτουργία σας ήταν επιτυχής:

```csharp
Console.WriteLine("AddingPictureInChart executed successfully.");
```

## Σύναψη

Σε αυτό το σεμινάριο, εξερευνήσαμε πώς να προσθέσετε λίγη προσωπικότητα στα γραφήματα του Excel σας προσθέτοντας εικόνες χρησιμοποιώντας το Aspose.Cells για .NET. Με λίγα μόνο απλά βήματα, μπορείτε να αναβαθμίσετε τις παρουσιάσεις σας από απλές σε αξέχαστες. Τι περιμένετε, λοιπόν; Δοκιμάστε το και αφήστε τα γραφήματά σας να λάμψουν!

## Συχνές ερωτήσεις

### Μπορώ να προσθέσω πολλές εικόνες σε ένα μόνο διάγραμμα;
Ναι! Μπορείτε να καλέσετε το `AddPictureInChart` μέθοδο πολλές φορές για να προσθέσετε όσες εικόνες επιθυμείτε.

### Ποιες μορφές εικόνας υποστηρίζει το Aspose.Cells;
Το Aspose.Cells υποστηρίζει μια ποικιλία μορφών εικόνας, όπως PNG, JPEG, BMP και GIF.

### Μπορώ να προσαρμόσω τη θέση της εικόνας;
Σίγουρα! Οι συντεταγμένες X και Y στο `AddPictureInChart` Η μέθοδος επιτρέπει την ακριβή τοποθέτηση.

### Είναι το Aspose.Cells δωρεάν στη χρήση;
Το Aspose.Cells προσφέρει δωρεάν δοκιμαστική περίοδο, αλλά για όλες τις λειτουργίες απαιτείται άδεια χρήσης. Μπορείτε να βρείτε την τιμολόγηση. [εδώ](https://purchase.aspose.com/buy).

### Πού μπορώ να βρω περισσότερα παραδείγματα;
Δείτε το [Τεκμηρίωση Aspose.Cells](https://reference.aspose.com/cells/net/) για πιο λεπτομερή παραδείγματα και λειτουργίες.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}