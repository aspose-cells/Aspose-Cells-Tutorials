---
title: Διαίρεση υαλοπινάκων του φύλλου εργασίας
linktitle: Διαίρεση υαλοπινάκων του φύλλου εργασίας
second_title: Aspose.Cells for .NET API Reference
description: Μάθετε πώς να χωρίζετε τα παράθυρα του φύλλου εργασίας στο Aspose.Cells για .NET με τον αναλυτικό οδηγό μας. Βελτιώστε την πλοήγηση αρχείων Excel με αυτό το εύκολο σεμινάριο.
weight: 130
url: /el/net/excel-display-settings-csharp-tutorials/split-panes-of-worksheet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Διαίρεση υαλοπινάκων του φύλλου εργασίας

## Εισαγωγή

Είστε έτοιμοι να χωρίσετε τα παράθυρα ενός φύλλου εργασίας του Excel χρησιμοποιώντας το Aspose.Cells για .NET; Φανταστείτε το εξής: έχετε ένα τεράστιο φύλλο Excel και έχετε βαρεθεί να επιστρέφετε συνεχώς στις κεφαλίδες για να θυμάστε με ποια στήλη εργάζεστε. Εισαγάγετε "Διαίρεση υαλοπινάκων". Αυτή η εύχρηστη λειτουργία σάς επιτρέπει να παγώσετε ένα τμήμα του φύλλου εργασίας σας, καθιστώντας πολύ πιο εύκολη την πλοήγηση. Είτε εργάζεστε με οικονομικά δεδομένα, διαχείριση αποθέματος ή τεράστια σύνολα δεδομένων, ο διαχωρισμός των παραθύρων μπορεί να δεκαπλασιάσει την παραγωγικότητά σας. 

## Προαπαιτούμενα

Πριν αρχίσουμε να χωρίζουμε τα παράθυρα σαν οδηγός υπολογιστικών φύλλων, ας κάνουμε τη σωστή ρύθμιση. Εδώ είναι τι θα χρειαστείτε:

-  Aspose.Cells για .NET: Βεβαιωθείτε ότι το έχετε κατεβάσει και εγκαταστήσει. Αν δεν το έχετε κάνει ακόμα, πιάστε το[εδώ](https://releases.aspose.com/cells/net/).
- .NET Framework: Αυτός ο οδηγός υποθέτει ότι εργάζεστε σε περιβάλλον .NET.
- Ένα βιβλίο εργασίας του Excel: Θα χρησιμοποιήσουμε ένα δείγμα αρχείου Excel για να δείξουμε πώς λειτουργεί αυτή η δυνατότητα.
-  Προσωρινή ή πλήρης άδεια χρήσης: Το Aspose.Cells απαιτεί άδεια χρήσης. Αν απλά το δοκιμάζετε, πάρτε ένα[δωρεάν προσωρινή άδεια](https://purchase.aspose.com/temporary-license/) για την αποφυγή περιορισμών αξιολόγησης.

## Εισαγωγή πακέτων

Πριν προχωρήσουμε στον κώδικα, ας εισάγουμε πρώτα τους απαραίτητους χώρους ονομάτων. Δεν μπορείτε πραγματικά να κάνετε τίποτα στο Aspose.Cells χωρίς να τα συμπεριλάβετε.

```csharp
using System.IO;
using Aspose.Cells;
```

Τώρα που έχουμε καλύψει τα απαραίτητα, ας περάσουμε στο συναρπαστικό μέρος - το διαχωρισμό των τζαμιών!

## Βήμα 1: Δημιουργήστε ένα βιβλίο εργασίας

 Το πρώτο βήμα σε αυτή τη διαδικασία είναι η δημιουργία ενός`Workbook` αντικείμενο, το οποίο θα αντιπροσωπεύει το αρχείο Excel που θέλετε να τροποποιήσετε. Σε αυτήν την περίπτωση, θα φορτώσουμε ένα αρχείο από έναν κατάλογο. Αυτός είναι ο καμβάς σας, το φύλλο Excel στο οποίο θα κάνετε τα μαγικά σας.

Για να μπορέσουμε να χωρίσουμε τα παράθυρα, χρειαζόμαστε ένα βιβλίο εργασίας για να δουλέψουμε! Αυτό το βήμα είναι τόσο απαραίτητο όσο το άνοιγμα ενός βιβλίου πριν ξεκινήσετε να το διαβάζετε.

```csharp
// Η διαδρομή προς τον κατάλογο εγγράφων
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Δημιουργήστε ένα νέο βιβλίο εργασίας και ανοίξτε ένα αρχείο προτύπου
Workbook book = new Workbook(dataDir + "Book1.xls");
```

 Στον παραπάνω κωδικό, αντικαταστήστε`"YOUR DOCUMENT DIRECTORY"` με την πραγματική διαδρομή όπου βρίσκεται το αρχείο σας Excel. Ο`Workbook`class φορτώνει το αρχείο Excel στη μνήμη.

## Βήμα 2: Ρυθμίστε το Ενεργό κελί

 Μετά τη φόρτωση του βιβλίου εργασίας, ήρθε η ώρα να ορίσετε το ενεργό κελί. Με όρους Excel, το ενεργό κελί είναι αυτό που είναι επιλεγμένο ή στο επίκεντρο. Σε αυτό το σεμινάριο, θα επιλέξουμε κελί`A20` στο πρώτο φύλλο εργασίας.

Η ρύθμιση του ενεργού κελιού είναι ζωτικής σημασίας επειδή ο διαχωρισμός του παραθύρου ξεκινά από αυτό το ενεργό κελί. Είναι σαν να επιλέγετε πού θα κάνετε το πρώτο κομμάτι σε μια πίτσα—διαλέξτε τη φέτα σας!

```csharp
// Ρυθμίστε το ενεργό κελί
book.Worksheets[0].ActiveCell = "A20";
```

 Αυτό το κομμάτι κώδικα κάνει`A20` το ενεργό κύτταρο. Είναι σημαντικό γιατί ο διαχωρισμός συμβαίνει γύρω από αυτό το σημείο, όπως ακριβώς και ο τρόπος με τον οποίο η πλοήγησή σας στο Excel επικεντρώνεται συχνά γύρω από ένα συγκεκριμένο κελί.

## Βήμα 3: Διαχωρίστε το φύλλο εργασίας

Τώρα που έχει ρυθμιστεί το ενεργό κελί, ας περάσουμε στο διασκεδαστικό μέρος—διαίρεση του φύλλου εργασίας! Αυτό το βήμα είναι όπου συμβαίνει η μαγεία. Θα μπορείτε να διαιρέσετε το φύλλο εργασίας σε πολλά παράθυρα για ευκολότερη προβολή και πλοήγηση.

Αυτός είναι ο πυρήνας ολόκληρου του σεμιναρίου. Διαχωρίζοντας το φύλλο εργασίας, δημιουργείτε ξεχωριστά παράθυρα που σας επιτρέπουν να κάνετε κύλιση σε διάφορες ενότητες του φύλλου Excel χωρίς να χάνετε τα μάτια σας από κεφαλίδες ή άλλες σημαντικές περιοχές.

```csharp
// Διαχωρίστε το παράθυρο του φύλλου εργασίας
book.Worksheets[0].Split();
```

 Με το`Split()` μέθοδο, λέτε στο Aspose.Cells να χωρίσει το φύλλο εργασίας στο ενεργό κελί (`A20` σε αυτή την περίπτωση). Από αυτό το σημείο, το Excel δημιουργεί μια διαίρεση στο φύλλο που χωρίζει τα παράθυρα για να μπορείτε να πλοηγηθείτε ανεξάρτητα.

## Βήμα 4: Αποθηκεύστε το βιβλίο εργασίας

Αφού χωρίσετε τα τζάμια, το μόνο που μένει είναι να αποθηκεύσετε την εργασία σας. Αυτό το τελευταίο βήμα θα διασφαλίσει ότι οι αλλαγές σας θα αποθηκευτούν στο καθορισμένο αρχείο εξόδου.

Τι ωφελεί όλη η σκληρή δουλειά σου αν δεν τη γλιτώσεις; Η αποθήκευση διασφαλίζει ότι τα όμορφα σπασμένα τζάμια σας διατηρούνται ανέπαφα για μελλοντική χρήση.

```csharp
// Αποθηκεύστε το αρχείο Excel
book.Save(dataDir + "output.xls");
```

 Εδώ, το`Save()` μέθοδος αποθηκεύει το βιβλίο εργασίας με τα πρόσφατα διαχωρισμένα παράθυρά σας σε ένα αρχείο εξόδου Excel. Οι αλλαγές που κάνατε είναι τώρα έτοιμες για χρήση από εσάς —ή οποιονδήποτε άλλον.

## Σύναψη

Και ορίστε το! Μόλις μάθατε πώς να χωρίζετε τα παράθυρα σε ένα φύλλο εργασίας του Excel χρησιμοποιώντας το Aspose.Cells για .NET. Δεν υπάρχει πλέον ατελείωτη κύλιση ή απώλεια παρακολούθησης των δεδομένων σας. Αυτή η μέθοδος καθιστά το χειρισμό μεγάλων αρχείων Excel πολύ λιγότερο συντριπτικό και πολύ πιο αποτελεσματικό. Με τη δυνατότητα διαχωρισμού παραθύρων, μπορείτε τώρα να παρακολουθείτε κρίσιμα σημεία δεδομένων ενώ εργάζεστε με πολύπλοκα υπολογιστικά φύλλα.

## Συχνές ερωτήσεις

### Μπορώ να χωρίσω περισσότερα από δύο τζάμια;  
 Ναι, μπορείτε να χωρίσετε το φύλλο εργασίας σε πολλαπλά παράθυρα καθορίζοντας διαφορετικά ενεργά κελιά και καλώντας το`Split()` μέθοδος.

### Ποια είναι η διαφορά μεταξύ των υαλοπινάκων διαχωρισμού και των υαλοπινάκων κατάψυξης;  
Ο διαχωρισμός των παραθύρων σάς επιτρέπει να πραγματοποιείτε κύλιση και στα δύο παράθυρα ανεξάρτητα. Τα παράθυρα παγώματος κλειδώνουν τις κεφαλίδες ή συγκεκριμένες σειρές/στήλες, ώστε να παραμένουν ορατές κατά την κύλιση.

### Μπορώ να αφαιρέσω το σχίσιμο μετά την εφαρμογή του;  
Ναι, μπορείτε να καταργήσετε τη διαίρεση είτε κλείνοντας και ανοίγοντας ξανά το βιβλίο εργασίας είτε επαναφέροντάς το μέσω προγραμματισμού.

### Τα παράθυρα διαχωρισμού λειτουργούν το ίδιο για διαφορετικές μορφές αρχείων Excel (XLS, XLSX);  
 Ναι, το`Split()` Η μέθοδος λειτουργεί τόσο για μορφές XLS όσο και για XLSX.

### Μπορώ να χρησιμοποιήσω το Aspose.Cells χωρίς άδεια χρήσης;  
 Ναι, αλλά έρχεται με περιορισμούς. Για μια πλήρη εμπειρία, είναι καλύτερο να χρησιμοποιήσετε ένα[προσωρινός](https://purchase.aspose.com/temporary-license/) ή[πληρωμένη άδεια](https://purchase.aspose.com/buy).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
