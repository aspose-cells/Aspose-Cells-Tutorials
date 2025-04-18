---
title: Καταργήστε τη συγχώνευση συγχωνευμένων κελιών στο Excel
linktitle: Καταργήστε τη συγχώνευση συγχωνευμένων κελιών στο Excel
second_title: Aspose.Cells .NET Excel Processing API
description: Καταργήστε εύκολα τη συγχώνευση συγχωνευμένων κελιών στο Excel χρησιμοποιώντας το Aspose.Cells για .NET. Ακολουθήστε τον βήμα προς βήμα οδηγό μας για να δημιουργήσετε καλύτερα υπολογιστικά φύλλα.
weight: 10
url: /el/net/excel-merging-unmerging-cells/unmerge-merged-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Καταργήστε τη συγχώνευση συγχωνευμένων κελιών στο Excel

## Εισαγωγή

Έχετε βαρεθεί να ασχολείστε με συγχωνευμένα κελιά στα υπολογιστικά φύλλα του Excel; Δεν είσαι μόνος! Τα συγχωνευμένα κελιά μπορεί να είναι ένα εύχρηστο χαρακτηριστικό για τη μορφοποίηση, αλλά συχνά μπορεί να οδηγήσουν σε πονοκεφάλους όταν πρόκειται για χειρισμό και ανάλυση δεδομένων. Αλλά μαντέψτε τι; Η αποσύνδεση αυτών των ενοχλητικών κελιών είναι ευκολότερη από ό,τι νομίζετε—ειδικά όταν χρησιμοποιείτε το Aspose.Cells για .NET. Σε αυτό το άρθρο, θα σας καθοδηγήσω στον τρόπο κατάργησης της συγχώνευσης των συγχωνευμένων κελιών βήμα προς βήμα, διασφαλίζοντας ότι τα δεδομένα σας είναι τακτοποιημένα, τακτοποιημένα και έτοιμα για δράση! Λοιπόν, πάρτε το καπέλο κωδικοποίησης και ας βουτήξουμε στον κόσμο του Aspose.Cells.

## Προαπαιτούμενα

Πριν λερώσουμε τα χέρια μας, υπάρχουν μερικά βασικά πράγματα που πρέπει να έχετε στη θέση του:

### Βασικές γνώσεις C# και .NET Framework
Εάν είστε εξοικειωμένοι με τον προγραμματισμό C# και έχετε μια βασική κατανόηση του πλαισίου .NET, έχετε ήδη κάνει μια καλή αρχή. Αν όχι, μην ανησυχείς! Αυτό το σεμινάριο έχει σχεδιαστεί για να είναι απλό, έτσι θα λάβετε τις απαραίτητες έννοιες στην πορεία.

### Aspose.Cells Library
Βεβαιωθείτε ότι έχετε εγκαταστήσει τη βιβλιοθήκη Aspose.Cells στο περιβάλλον σας .NET. Μπορείτε να το αποκτήσετε εύκολα επισκεπτόμενοι το[Σελίδα λήψης Aspose.Cells](https://releases.aspose.com/cells/net/).

### Ρύθμιση IDE
Θα πρέπει να έχετε ρυθμίσει ένα περιβάλλον ανάπτυξης, όπως το Visual Studio, όπου μπορείτε να γράψετε και να εκτελέσετε τον κώδικα C#.

### Δείγμα αρχείου Excel
Πάρτε ένα δείγμα αρχείου Excel που περιέχει ορισμένα συγχωνευμένα κελιά—θα χρησιμοποιήσετε αυτό το αρχείο για να εξασκήσετε την αποσυγχώνευση.

Με όλα αυτά τα προαπαιτούμενα ταξινομημένα, μπορούμε τώρα να μεταβούμε στο συναρπαστικό μέρος - κωδικοποίηση της λύσης μας!

## Εισαγωγή πακέτων

Πρώτα πρώτα, ας εισάγουμε τα απαραίτητα πακέτα. Με το Aspose.Cells, θα αλληλεπιδράτε με διάφορες κλάσεις για να διαχειρίζεστε αποτελεσματικά τα αρχεία Excel. Δείτε τι πρέπει να συμπεριλάβετε στην κορυφή του αρχείου C#:

```csharp
using System;
using System.IO;

using Aspose.Cells;
```

Συμπεριλαμβάνοντας αυτό το πακέτο, θα έχετε πρόσβαση σε όλες τις δυνατότητες που προσφέρει το Aspose.Cells.

Ας αναλύσουμε τη διαδικασία αποσύνδεσης σε διαχειρίσιμα βήματα. Κάθε βήμα θα καθοριστεί με σαφήνεια, ώστε να μπορείτε να το ακολουθείτε εύκολα.

## Βήμα 1: Ορισμός καταλόγων

Το πρώτο βήμα είναι να ορίσετε τους καταλόγους όπου βρίσκονται το αρχείο εισόδου Excel (αυτό με τα συγχωνευμένα κελιά) και το αρχείο εξόδου (αυτός όπου θα αποθηκευτούν τα μη συγχωνευμένα δεδομένα). Δείτε πώς μπορείτε να το ρυθμίσετε:

```csharp
// Κατάλογος πηγής
string sourceDir = "Your Document Directory"; 

// Κατάλογος εξόδου
string outputDir = "Your Document Directory"; 
```

 Φροντίστε να αντικαταστήσετε`"Your Document Directory"` με την πραγματική διαδρομή προς τα αρχεία σας.

## Βήμα 2: Δημιουργήστε ένα βιβλίο εργασίας

Τώρα που έχετε ορίσει τους καταλόγους, ήρθε η ώρα να δημιουργήσετε ένα αντικείμενο βιβλίου εργασίας. Αυτό το αντικείμενο θα σας επιτρέψει να χειριστείτε το αρχείο Excel. Μπορείτε να το κάνετε αυτό με τον παρακάτω κώδικα:

```csharp
// Δημιουργήστε ένα βιβλίο εργασίας
Workbook wbk = new Aspose.Cells.Workbook(sourceDir + "sampleUnMergingtheMergedCells.xlsx");
```

Αυτή η γραμμή κώδικα διαβάζει το δείγμα αρχείου Excel και το προετοιμάζει για επεξεργασία. 

## Βήμα 3: Πρόσβαση στο φύλλο εργασίας

Κάθε βιβλίο εργασίας αποτελείται από φύλλα. Πρέπει να αποκτήσετε πρόσβαση στο συγκεκριμένο φύλλο εργασίας όπου θέλετε να καταργήσετε τη συγχώνευση των κελιών. Δείτε πώς να το κάνετε αυτό:

```csharp
// Δημιουργήστε ένα φύλλο εργασίας και λάβετε το πρώτο φύλλο
Worksheet worksheet = wbk.Worksheets[0];
```

Αυτός ο κώδικας παίρνει το πρώτο φύλλο εργασίας. Εάν τα συγχωνευμένα κελιά σας βρίσκονται σε διαφορετικό φύλλο, ενημερώστε το ευρετήριο ανάλογα.

## Βήμα 4: Πρόσβαση σε κελιά στο φύλλο εργασίας

Στη συνέχεια, θα χρειαστεί να λάβετε μια αναφορά στα κελιά στο φύλλο εργασίας σας. Αυτό μπορεί να επιτευχθεί χρησιμοποιώντας:

```csharp
//Δημιουργήστε ένα αντικείμενο Cells για να ανακτήσετε όλα τα κελιά
Cells cells = worksheet.Cells;
```

Με αυτήν τη γραμμή, έχετε πλέον πρόσβαση σε όλα τα κελιά του φύλλου εργασίας, επιτρέποντάς σας να τα χειριστείτε όπως απαιτείται.

## Βήμα 5: Καταργήστε τη συγχώνευση των κελιών

Εδώ έρχεται το κρίσιμο βήμα - η αποσύνδεση των κυττάρων! Θα θελήσετε να καθορίσετε το εύρος των συγχωνευμένων κελιών που θέλετε να καταργήσετε τη συγχώνευση. Χρησιμοποιήστε τον παρακάτω κώδικα:

```csharp
// Καταργήστε τη συγχώνευση των κελιών
cells.UnMerge(5, 2, 2, 3);
```

 Σε αυτό το παράδειγμα, το`UnMerge` Η μέθοδος παίρνει τέσσερις παραμέτρους: τον δείκτη αρχικής σειράς (5), τον δείκτη αρχικής στήλης (2), τον αριθμό των γραμμών προς αποσυγχώνευση (2) και τον αριθμό των στηλών προς κατάργηση συγχώνευσης (3). Προσαρμόστε αυτές τις παραμέτρους ώστε να ταιριάζουν με τα συγκεκριμένα συγχωνευμένα κελιά στο αρχείο σας Excel.

## Βήμα 6: Αποθηκεύστε το βιβλίο εργασίας

Μετά την αποσυγχώνευση, θα θέλετε να αποθηκεύσετε τις αλλαγές σας σε ένα νέο αρχείο Excel. Δείτε πώς να το κάνετε αυτό:

```csharp
// Αποθηκεύστε το αρχείο
wbk.Save(outputDir + "outputUnMergingtheMergedCells.xlsx");
```

Αυτή η γραμμή αποθηκεύει τα μη συγχωνευμένα δεδομένα σας στον καθορισμένο κατάλογο εξόδου. Τόσο απλό!

## Βήμα 7: Επιβεβαιώστε τη διαδικασία

Τέλος, καλό είναι να επιβεβαιώσουμε ότι όλα κύλησαν ομαλά. Μπορείτε να εκτυπώσετε ένα μήνυμα στην κονσόλα για να σας ενημερώσει ότι η λειτουργία εκτελέστηκε με επιτυχία:

```csharp
Console.WriteLine("UnMerging the Cells executed successfully.");
```

Και ορίστε το! Καταργήσατε επιτυχώς τα κελιά σε ένα αρχείο Excel χρησιμοποιώντας το Aspose.Cells για .NET.

## Σύναψη

Η αποσύνδεση κελιών μπορεί να φαίνεται κουραστική, ειδικά αν έχετε να κάνετε με μεγάλα υπολογιστικά φύλλα, αλλά με τα Aspose.Cells για .NET, είναι παιχνιδάκι! Αυτό το σεμινάριο σας καθοδήγησε σε όλα, από τη ρύθμιση του περιβάλλοντός σας έως την εκτέλεση του κώδικα που απαιτείται για την αποτελεσματική αποσύνδεση κελιών. Η ευελιξία που προσφέρει η βιβλιοθήκη Aspose.Cells σάς επιτρέπει να επεξεργάζεστε υπολογιστικά φύλλα αποτελεσματικά, καθιστώντας την ιδανική επιλογή για προγραμματιστές που εργάζονται με αρχεία Excel. Βουτήξτε, λοιπόν, και αρχίστε να απολαμβάνετε πιο καθαρά, πιο διαχειρίσιμα υπολογιστικά φύλλα.

## Συχνές ερωτήσεις

### Τι είναι το Aspose.Cells;  
Το Aspose.Cells είναι μια ισχυρή βιβλιοθήκη για τη δημιουργία, τον χειρισμό και τη μετατροπή εγγράφων Excel σε εφαρμογές .NET.

### Χρειάζομαι άδεια χρήσης για να χρησιμοποιήσω το Aspose.Cells;  
 Ενώ το Aspose.Cells προσφέρει δωρεάν δοκιμή, απαιτείται άδεια χρήσης για πλήρη χρήση. Μπορείτε να πάρετε ένα[προσωρινή άδεια εδώ](https://purchase.aspose.com/temporary-license/).

### Μπορώ να καταργήσω τη συγχώνευση κελιών σε πολλά φύλλα ταυτόχρονα;  
Ναι, μπορείτε να κάνετε επαναφορά πολλών φύλλων εργασίας σε ένα βιβλίο εργασίας και να καταργήσετε τη συγχώνευση κελιών, όπως απαιτείται.

### Είναι το Aspose.Cells συμβατό με .NET Core;  
Ναι, το Aspose.Cells είναι συμβατό με .NET Core, καθιστώντας το ευέλικτο για διάφορες εφαρμογές .NET.

### Πού μπορώ να βρω περισσότερη τεκμηρίωση για το Aspose.Cells;  
 Μπορείτε να εξερευνήσετε την πλήρη τεκμηρίωση στο[Σελίδα αναφοράς Aspose.Cells](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
