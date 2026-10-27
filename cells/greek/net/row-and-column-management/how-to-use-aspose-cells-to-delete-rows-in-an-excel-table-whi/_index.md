---
category: general
date: 2026-10-07
description: Μάθετε πώς το Aspose.Cells διαγράφει γραμμές από έναν πίνακα Excel, αφαιρεί
  όλες τις γραμμές εκτός της κεφαλίδας και διαχειρίζεται τη διαγραφή προστατευμένων
  γραμμών του πίνακα με καθαρό κώδικα C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- aspose cells delete rows
- delete rows excel table
- excel table row deletion
- protect excel table rows
- remove rows except header
language: el
lastmod: 2026-10-07
og_description: Το Aspose.Cells διαγράφει γραμμές από έναν πίνακα Excel διατηρώντας
  την κεφαλίδα. Αυτός ο οδηγός παρουσιάζει τη πλήρη λύση σε C#, αντιμετωπίζοντας προστατευμένους
  πίνακες και κοινές ακραίες περιπτώσεις.
og_image_alt: Aspose.Cells delete rows example showing code and Excel screenshot
og_title: Aspose.Cells διαγραφή γραμμών – αφαίρεση όλων των γραμμών εκτός της κεφαλίδας
  σε C#
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Learn how Aspose.Cells delete rows from an Excel table, remove rows
    except header, and handle protected table row deletion with clean C# code.
  headline: How to use Aspose.Cells to delete rows in an Excel table while keeping
    the header
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Πώς να χρησιμοποιήσετε το Aspose.Cells για τη διαγραφή γραμμών σε έναν πίνακα
  Excel διατηρώντας την κεφαλίδα
url: /el/net/row-and-column-management/how-to-use-aspose-cells-to-delete-rows-in-an-excel-table-whi/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να χρησιμοποιήσετε το Aspose.Cells για διαγραφή γραμμών σε έναν πίνακα Excel διατηρώντας την κεφαλίδα

Αν χρειάζεστε **aspose cells delete rows** από έναν πίνακα αλλά θέλετε να διατηρήσετε τη γραμμή κεφαλίδας, αυτός ο οδηγός παρουσιάζει μια πλήρη, εκτελέσιμη λύση. Θα δείτε γιατί μια άμεση κλήση στο `ListObject.DeleteRows` αποτυγχάνει όταν ο πίνακας είναι προστατευμένος, και πώς να παρακάμψετε αυτόν τον περιορισμό χωρίς να θέσετε σε κίνδυνο την ακεραιότητα των δεδομένων.

Ο οδηγός καλύπτει:

* Φόρτωση ενός βιβλίου εργασίας που περιέχει έναν προστατευμένο πίνακα.  
* Ανίχνευση και προσωρινή άρση της προστασίας του πίνακα.  
* Διαγραφή όλων των γραμμών δεδομένων διατηρώντας την κεφαλίδα.  
* Επαναφορά της αρχικής κατάστασης προστασίας.  

Στο τέλος του άρθρου μπορείτε αξιόπιστα να εκτελείτε λειτουργίες **delete rows excel table** σε οποιοδήποτε έργο Aspose.Cells.

## Προαπαιτούμενα

* .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί επίσης με .NET Framework 4.7.2+).  
* Aspose.Cells for .NET 23.9 ή νεότερο.  
* Βασική εξοικείωση με C# και πίνακες Excel (γνωστοί και ως ListObjects).  

Δεν απαιτούνται πρόσθετα πακέτα NuGet πέρα από το Aspose.Cells.

## Βήμα 1: Ρύθμιση του έργου και εισαγωγή namespaces

Δημιουργήστε μια νέα εφαρμογή console ή προσθέστε τον παρακάτω κώδικα σε ένα υπάρχον έργο. Εισάγετε τα namespaces του Aspose.Cells ώστε ο μεταγλωττιστής να μπορεί να αναγνωρίσει τα `Workbook`, `Worksheet` και `ListObject`.

```csharp
using System;
using Aspose.Cells;

namespace AsposeCellsTableRowDeletion
{
    class Program
    {
        static void Main()
        {
            // The full solution starts in Step 2.
        }
    }
}
```

*Γιατί αυτό το βήμα είναι σημαντικό* – Η εισαγωγή των σωστών namespaces αποτρέπει σφάλματα ασαφούς τύπου και κάνει τον υπόλοιπο κώδικα πιο σαφή.

## Βήμα 2: Φόρτωση του βιβλίου εργασίας και εντοπισμός του στόχου πίνακα

Αντικαταστήστε το `"YOUR_DIRECTORY/TableProtection.xlsx"` με τη διαδρομή του αρχείου Excel σας. Το παράδειγμα υποθέτει ότι ο πίνακας που θέλετε να τροποποιήσετε ονομάζεται **Orders**.

```csharp
// Load the workbook that contains the protected table
Workbook workbook = new Workbook("YOUR_DIRECTORY/TableProtection.xlsx");

// Get the first worksheet (index 0) and the ListObject named "Orders"
Worksheet worksheet = workbook.Worksheets[0];
ListObject ordersTable = worksheet.ListObjects["Orders"];
```

*Γιατί αυτό το βήμα είναι σημαντικό* – Η πρόσβαση στο `ListObject` σας παρέχει άμεσο χειριστήριο του πίνακα, το οποίο απαιτείται για οποιαδήποτε λειτουργία **excel table row deletion**.

## Βήμα 3: Έλεγχος αν ο πίνακας είναι προστατευμένος

Το Aspose.Cells εμποδίζει τη μερική διαγραφή πίνακα όταν ο πίνακας είναι προστατευμένος. Η προσπάθεια `ordersTable.DeleteRows` σε αυτήν την κατάσταση προκαλεί εξαίρεση. Εντοπίστε πρώτα την κατάσταση προστασίας.

```csharp
bool wasProtected = ordersTable.IsProtected;
Console.WriteLine($"Table protection status: {(wasProtected ? "protected" : "unprotected")}");
```

*Γιατί αυτό το βήμα είναι σημαντικό* – Η γνώση της κατάστασης προστασίας σας επιτρέπει να αποφασίσετε αν θα αφαιρέσετε προσωρινά την προστασία, διασφαλίζοντας ότι ο κανόνας **protect excel table rows** τηρείται μετά τη λειτουργία.

## Βήμα 4: Προσωρινή άρση προστασίας του πίνακα (αν χρειάζεται)

Αν ο πίνακας είναι προστατευμένος, χρησιμοποιήστε το `Unprotect` με τον κωδικό (αν υπάρχει). Για πίνακες χωρίς κωδικό, απλώς καλέστε το `Unprotect()`.

```csharp
if (wasProtected)
{
    // Provide the password if the table was protected with one; otherwise, pass null.
    ordersTable.Unprotect(null);
    Console.WriteLine("Table temporarily unprotected.");
}
```

*Γιατί αυτό το βήμα είναι σημαντικό* – Η άρση προστασίας του πίνακα επιτρέπει στο Aspose.Cells να εκτελέσει **aspose cells delete rows** χωρίς να προκαλέσει εξαίρεση, ενώ εξακολουθείτε να μπορείτε να επαναφέρετε την προστασία αργότερα.

## Βήμα 5: Διαγραφή όλων των γραμμών εκτός της κεφαλίδας

Η κεφαλίδα καταλαμβάνει την πρώτη γραμμή του πίνακα (`RowCount` περιλαμβάνει την κεφαλίδα). Η διαγραφή από το ευρετήριο 1 αφαιρεί κάθε γραμμή δεδομένων.

```csharp
int dataRows = ordersTable.RowCount - 1; // Exclude the header row
if (dataRows > 0)
{
    ordersTable.DeleteRows(1, dataRows);
    Console.WriteLine($"{dataRows} data rows removed, header preserved.");
}
else
{
    Console.WriteLine("Table contains only the header; nothing to delete.");
}
```

*Γιατί αυτό το βήμα είναι σημαντικό* – Αυτός ο κώδικας εκτελεί τη βασική λειτουργία **remove rows except header** ενώ αποφεύγει την εξαίρεση που προκύπτει με μερικές διαγραφές σε προστατευμένους πίνακες.

## Βήμα 6: Επανάληψη προστασίας (αν είχε οριστεί αρχικά)

Αφού αφαιρεθούν οι γραμμές, επαναφέρετε την αρχική κατάσταση προστασίας ώστε το βιβλίο εργασίας να λειτουργεί ακριβώς όπως πριν.

```csharp
if (wasProtected)
{
    // Re‑apply protection with the same password (null if none was used)
    ordersTable.Protect(null);
    Console.WriteLine("Table protection restored.");
}
```

*Γιατί αυτό το βήμα είναι σημαντικό* – Η επαναφορά της προστασίας σέβεται την απαίτηση **protect excel table rows** και διατηρεί το βιβλίο εργασίας ασφαλές για τους επόμενους χρήστες.

## Βήμα 7: Αποθήκευση του τροποποιημένου βιβλίου εργασίας

Επιλέξτε νέο όνομα αρχείου για να αποφύγετε την αντικατάσταση του αρχικού αρχείου, εκτός αν η αντικατάσταση είναι σκόπιμη.

```csharp
string outputPath = "YOUR_DIRECTORY/TableProtection_Modified.xlsx";
workbook.Save(outputPath);
Console.WriteLine($"Modified workbook saved to: {outputPath}");
```

*Γιατί αυτό το βήμα είναι σημαντικό* – Η αποθήκευση ολοκληρώνει τη λειτουργία **excel table row deletion** και παρέχει ένα απτό αποτέλεσμα που μπορείτε να ανοίξετε στο Excel για επαλήθευση.

## Πλήρες λειτουργικό παράδειγμα

Συνδυάζοντας όλα τα βήματα δημιουργείται ένα αυτόνομο πρόγραμμα που μπορείτε να αντιγράψετε, επικολλήσετε και εκτελέσετε.

```csharp
using System;
using Aspose.Cells;

namespace AsposeCellsTableRowDeletion
{
    class Program
    {
        static void Main()
        {
            // 1. Load workbook
            Workbook workbook = new Workbook("YOUR_DIRECTORY/TableProtection.xlsx");
            Worksheet worksheet = workbook.Worksheets[0];
            ListObject ordersTable = worksheet.ListObjects["Orders"];

            // 2. Remember protection state
            bool wasProtected = ordersTable.IsProtected;
            Console.WriteLine($"Table protection status: {(wasProtected ? "protected" : "unprotected")}");

            // 3. Unprotect if needed
            if (wasProtected)
            {
                ordersTable.Unprotect(null); // use password if applicable
                Console.WriteLine("Table temporarily unprotected.");
            }

            // 4. Delete all rows except header
            int dataRows = ordersTable.RowCount - 1;
            if (dataRows > 0)
            {
                ordersTable.DeleteRows(1, dataRows);
                Console.WriteLine($"{dataRows} data rows removed, header preserved.");
            }
            else
            {
                Console.WriteLine("Table contains only the header; nothing to delete.");
            }

            // 5. Restore protection
            if (wasProtected)
            {
                ordersTable.Protect(null); // re‑apply with original password if any
                Console.WriteLine("Table protection restored.");
            }

            // 6. Save the workbook
            string outputPath = "YOUR_DIRECTORY/TableProtection_Modified.xlsx";
            workbook.Save(outputPath);
            Console.WriteLine($"Modified workbook saved to: {outputPath}");
        }
    }
}
```

### Αναμενόμενο αποτέλεσμα

```
Table protection status: protected
Table temporarily unprotected.
5 data rows removed, header preserved.
Table protection restored.
Modified workbook saved to: YOUR_DIRECTORY/TableProtection_Modified.xlsx
```

Ανοίξτε το `TableProtection_Modified.xlsx` στο Excel. Θα δείτε τον πίνακα **Orders** με μόνο τη γραμμή κεφαλίδας να παραμένει· όλες οι γραμμές δεδομένων έχουν αφαιρεθεί.

## Διαχείριση κοινών παραλλαγών και ειδικών περιπτώσεων

| Κατάσταση | Συνιστώμενη τροποποίηση | Αιτία |
|-----------|--------------------------|-------|
| Ο πίνακας χρησιμοποιεί κωδικό πρόσβασης | Περάστε τον κωδικό στο `Unprotect` και `Protect` | Εγγυάται το ίδιο επίπεδο ασφαλείας μετά τη λειτουργία |
| Ο πίνακας δεν έχει γραμμές δεδομένων | Παραλείψτε την κλήση `DeleteRows` | Αποτρέπει ένα `ArgumentOutOfRangeException` |
| Πολλοί πίνακες χρειάζονται καθαρισμό | Επανάληψη μέσω `worksheet.ListObjects` και εφαρμογή της ίδιας λογικής | Κλιμακώνει το πρότυπο **delete rows excel table** σε ολόκληρο το φύλλο |
| Θέλετε να διατηρήσετε την κεφαλίδα και την πρώτη γραμμή δεδομένων | Αλλάξτε `DeleteRows(2, dataRows‑1)` | Ξεκινά τη διαγραφή μετά τη δεύτερη γραμμή, διατηρώντας την πρώτη γραμμή δεδομένων |

Αυτές οι παραλλαγές δείχνουν αξιόπιστη διαχείριση **excel table row deletion** και ενισχύουν το γιατί η προτεινόμενη προσέγγιση είναι η συνιστώμενη.

## Συμβουλές επαγγελματιών

* **Batch processing** – Εάν χρειάζεται να διαγράψετε γραμμές από πολλά βιβλία εργασίας, ενσωματώστε τη λογική σε μια επαναχρησιμοποιήσιμη μέθοδο που δέχεται παραμέτρους `Workbook` και `tableName`.  
* **Performance** – Η διαγραφή γραμμών με μία κλήση (`DeleteRows`) είναι πιο γρήγορη από την αφαίρεση γραμμών μία-μία, επειδή το Aspose.Cells ενημερώνει τις εσωτερικές δομές δεδομένων μόνο μία φορά.  
* **Safety** – Πάντα εργάζεστε πάνω σε αντίγραφο του αρχικού αρχείου ή κρατήστε αντίγραφο ασφαλείας πριν εφαρμόσετε διαγραφές, ειδικά όταν εμπλέκεται το **protect excel table rows**.

## Συμπέρασμα

Τώρα έχετε μια πλήρη, έτοιμη για παραγωγή λύση για **aspose cells delete rows** ενώ διατηρείτε την κεφαλίδα ενός πίνακα Excel. Ο οδηγός κάλυψε τη φόρτωση του βιβλίου εργασίας, τη διαχείριση προστατευμένων πινάκων, την εκτέλεση της λειτουργίας **remove rows except header** και την επαναφορά της προστασίας. Εφαρμόστε το ίδιο μοτίβο σε οποιοδήποτε σενάριο **excel table row deletion**, και προσαρμόστε τον κώδικα ώστε να καλύπτει πρόσθετες απαιτήσεις όπως πίνακες με κωδικό πρόσβασης ή επεξεργασία σε παρτίδες.

---

*Επόμενα βήματα* – Εξερευνήστε συναφή θέματα όπως **delete rows excel table** με φίλτρα, συγχώνευση κελιών μετά τη διαγραφή γραμμών, ή χρήση του Aspose.Cells για αντιγραφή πινάκων μεταξύ βιβλίων εργασίας. Κάθε ένα από αυτά βασίζεται στις βασικές έννοιες που παρουσιάστηκαν εδώ και ενισχύει την εξειδίκευσή σας στην αυτοματοποίηση του Excel με το Aspose.Cells.

## Τι Θα Πρέπει Να Μάθετε Στη Σύντομη Μελλοντική;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Aspose Cells Delete Rows – Προστασία της Γραμμής Κεφαλίδας στο Excel](/cells/english/net/row-and-column-management/aspose-cells-delete-rows-protect-header-row-in-excel/)
- [Πώς να Εισάγετε και να Διαγράψετε Γραμμές στο Excel με Aspose.Cells για .NET: Ένας Πλήρης Οδηγός](/cells/english/net/data-manipulation/aspose-cells-net-insert-delete-excel-rows/)
- [Πώς να Διαγράψετε Κενές Γραμμές στο Excel Χρησιμοποιώντας Aspose.Cells .NET για Καθαρισμό Δεδομένων](/cells/english/net/data-manipulation/delete-blank-rows-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}