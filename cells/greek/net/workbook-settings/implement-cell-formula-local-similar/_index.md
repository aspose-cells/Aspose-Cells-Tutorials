---
title: Εφαρμογή τοπικού τύπου κελιού παρόμοιο με το τοπικό τύπο εύρους
linktitle: Εφαρμογή τοπικού τύπου κελιού παρόμοιο με το τοπικό τύπο εύρους
second_title: Aspose.Cells .NET Excel Processing API
description: Ανακαλύψτε πώς να εφαρμόσετε έναν τύπο κελιού που είναι παρόμοιος με την τοπική λειτουργικότητα του τύπου εύρους στο Aspose.Cells για .NET. Μάθετε να προσαρμόζετε τα ενσωματωμένα ονόματα συναρτήσεων του Excel και πολλά άλλα.
weight: 13
url: /el/net/workbook-settings/implement-cell-formula-local-similar/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εφαρμογή τοπικού τύπου κελιού παρόμοιο με το τοπικό τύπο εύρους

## Εισαγωγή
Το Aspose.Cells για .NET είναι ένα ισχυρό και ευέλικτο API χειρισμού υπολογιστικών φύλλων που σας επιτρέπει να δημιουργείτε, να χειρίζεστε και να μετατρέπετε αρχεία Excel μέσω προγραμματισμού. Μία από τις πολλές δυνατότητες που προσφέρει το Aspose.Cells είναι η δυνατότητα προσαρμογής της συμπεριφοράς των ενσωματωμένων συναρτήσεων του Excel, συμπεριλαμβανομένης της δυνατότητας δημιουργίας των δικών σας ονομάτων τοπικών συναρτήσεων. Σε αυτό το σεμινάριο, θα σας καθοδηγήσουμε στα βήματα για να εφαρμόσετε έναν τύπο κελιού που είναι παρόμοιος με την τοπική λειτουργικότητα του τύπου εύρους στο Aspose.Cells για .NET.
## Προαπαιτούμενα
Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε τα ακόλουθα:
1. Το Microsoft Visual Studio 2010 ή νεότερη έκδοση είναι εγκατεστημένο στο σύστημά σας.
2.  Η πιο πρόσφατη έκδοση της βιβλιοθήκης Aspose.Cells για .NET είναι εγκατεστημένη στο έργο σας. Μπορείτε να κατεβάσετε τη βιβλιοθήκη από το[Σελίδα λήψης Aspose.Cells για .NET](https://releases.aspose.com/cells/net/).
## Εισαγωγή πακέτων
Για να ξεκινήσετε, θα χρειαστεί να εισαγάγετε τα απαραίτητα πακέτα στο έργο σας C#. Προσθέστε τα ακόλουθα χρησιμοποιώντας δηλώσεις στην κορυφή του αρχείου κώδικα:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
## Βήμα 1: Δημιουργήστε μια τάξη προσαρμοσμένων ρυθμίσεων παγκοσμιοποίησης
 Το πρώτο βήμα είναι να δημιουργήσετε ένα έθιμο`GlobalizationSettings`κλάση που θα σας επιτρέψει να παρακάμψετε την προεπιλεγμένη συμπεριφορά των συναρτήσεων του Excel. Σε αυτό το παράδειγμα, θα αλλάξουμε τα ονόματα των`SUM` και`AVERAGE` λειτουργίες για να`UserFormulaLocal_SUM` και`UserFormulaLocal_AVERAGE`, αντίστοιχα.
```csharp
class GS : GlobalizationSettings
{
    public override string GetLocalFunctionName(string standardName)
    {
        //Αλλάξτε το όνομα της συνάρτησης SUM σύμφωνα με τις ανάγκες σας.
        if (standardName == "SUM")
        {
            return "UserFormulaLocal_SUM";
        }
        //Αλλάξτε το όνομα της συνάρτησης AVERAGE σύμφωνα με τις ανάγκες σας.
        if (standardName == "AVERAGE")
        {
            return "UserFormulaLocal_AVERAGE";
        }
        return "";
    }
}
```
## Βήμα 2: Δημιουργήστε ένα νέο βιβλίο εργασίας και ορίστε τις προσαρμοσμένες ρυθμίσεις παγκοσμιοποίησης
 Στη συνέχεια, δημιουργήστε μια νέα παρουσία Βιβλίου εργασίας και εκχωρήστε το προσαρμοσμένο`GlobalizationSettings` κλάση υλοποίησης στο Τετράδιο Εργασίας`Settings.GlobalizationSettings` ιδιοκτησία.
```csharp
//Δημιουργία βιβλίου εργασίας
Workbook wb = new Workbook();
//Εκχώρηση κλάσης υλοποίησης GlobalizationSettings
wb.Settings.GlobalizationSettings = new GS();
```
## Βήμα 3: Πρόσβαση στο πρώτο φύλλο εργασίας και σε ένα κελί
Τώρα, ας αποκτήσουμε πρόσβαση στο πρώτο φύλλο εργασίας στο βιβλίο εργασίας και σε ένα συγκεκριμένο κελί μέσα σε αυτό το φύλλο εργασίας.
```csharp
//Πρόσβαση στο πρώτο φύλλο εργασίας
Worksheet ws = wb.Worksheets[0];
//Πρόσβαση σε κάποιο κελί
Cell cell = ws.Cells["C4"];
```
## Βήμα 4: Εκχωρήστε τύπους και εκτυπώστε το FormulaLocal
 Τέλος, ας αναθέσουμε το`SUM` και`AVERAGE` τύπους στο κελί και εκτυπώστε το προκύπτον`FormulaLocal` αξίες.
```csharp
//Εκχωρήστε τον τύπο SUM και εκτυπώστε το FormulaLocal του
cell.Formula = "SUM(A1:A2)";
Console.WriteLine("Formula Local: " + cell.FormulaLocal);
//Εκχωρήστε τον τύπο AVERAGE και εκτυπώστε το FormulaLocal του
cell.Formula = "=AVERAGE(B1:B2, B5)";
Console.WriteLine("Formula Local: " + cell.FormulaLocal);
```
## Σύναψη
Σε αυτό το σεμινάριο, μάθατε πώς να υλοποιείτε έναν τύπο κελιού που είναι παρόμοιος με την τοπική λειτουργικότητα του τύπου εύρους στο Aspose.Cells για .NET. Δημιουργώντας ένα έθιμο`GlobalizationSettings` class, μπορείτε να παρακάμψετε την προεπιλεγμένη συμπεριφορά των συναρτήσεων του Excel και να προσαρμόσετε τα ονόματα των τοπικών συναρτήσεων ώστε να ταιριάζουν στις ανάγκες σας. Αυτό μπορεί να είναι ιδιαίτερα χρήσιμο όταν εργάζεστε με τοπικά ή διεθνοποιημένα έγγραφα Excel.
## Συχνές ερωτήσεις
###  Ποιος είναι ο σκοπός του`GlobalizationSettings` class in Aspose.Cells?
 Ο`GlobalizationSettings` class στο Aspose.Cells σας επιτρέπει να προσαρμόσετε τη συμπεριφορά των ενσωματωμένων συναρτήσεων του Excel, συμπεριλαμβανομένης της δυνατότητας αλλαγής των ονομάτων των τοπικών συναρτήσεων.
###  Μπορώ να παρακάμψω τη συμπεριφορά άλλων συναρτήσεων εκτός από`SUM` and `AVERAGE`?
 Ναι, μπορείτε να παρακάμψετε τη συμπεριφορά οποιασδήποτε ενσωματωμένης συνάρτησης του Excel τροποποιώντας το`GetLocalFunctionName` μέθοδος κατά το έθιμο σας`GlobalizationSettings` τάξη.
### Υπάρχει τρόπος να επαναφέρετε τα ονόματα των συναρτήσεων στις προεπιλεγμένες τιμές τους;
 Ναι, μπορείτε να επαναφέρετε τα ονόματα των συναρτήσεων είτε αφαιρώντας το προσαρμοσμένο`GlobalizationSettings` κλάση ή επιστρέφοντας μια κενή συμβολοσειρά από το`GetLocalFunctionName` μέθοδος.
### Μπορώ να χρησιμοποιήσω αυτήν τη δυνατότητα για να δημιουργήσω προσαρμοσμένες συναρτήσεις στο Aspose.Cells;
 Όχι, το`GlobalizationSettings`Η κλάση έχει σχεδιαστεί για να παρακάμπτει τη συμπεριφορά των ενσωματωμένων συναρτήσεων του Excel και όχι να δημιουργεί προσαρμοσμένες συναρτήσεις. Εάν χρειάζεται να δημιουργήσετε προσαρμοσμένες λειτουργίες, μπορείτε να χρησιμοποιήσετε το`UserDefinedFunction` τάξη στο Aspose.Cells.
### Είναι αυτή η δυνατότητα διαθέσιμη σε όλες τις εκδόσεις του Aspose.Cells για .NET;
 Ναι, το`GlobalizationSettings` κλάση και η δυνατότητα προσαρμογής ονομάτων συναρτήσεων είναι διαθέσιμη σε όλες τις εκδόσεις του Aspose.Cells για .NET.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
