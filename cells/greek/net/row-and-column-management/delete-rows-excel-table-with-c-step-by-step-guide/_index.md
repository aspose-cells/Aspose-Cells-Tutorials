---
category: general
date: 2026-02-28
description: Διαγράψτε γρήγορα γραμμές πίνακα Excel σε C#. Μάθετε πώς να προσθέσετε
  ονομαστικό εύρος στο Excel, να προσπελάσετε φύλλο εργασίας με όνομα και να αποφύγετε
  σφάλματα διπλότυπων ονομάτων.
draft: false
keywords:
- delete rows excel table
- add named range excel
- access worksheet by name
- how to add defined name
- named range on another sheet
language: el
og_description: Διαγραφή γραμμών πίνακα Excel χρησιμοποιώντας C#. Αυτό το σεμινάριο
  δείχνει επίσης πώς να προσθέσετε ονομαστική περιοχή στο Excel και να προσπελάσετε
  το φύλλο εργασίας με το όνομα.
og_title: Διαγραφή γραμμών πίνακα Excel με C# – Πλήρης οδηγός
tags:
- C#
- Excel
- DevExpress Spreadsheet
title: Διαγραφή γραμμών πίνακα Excel με C# – Οδηγός βήμα‑προς‑βήμα
url: /el/net/row-and-column-management/delete-rows-excel-table-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Διαγραφή Γραμμών Πίνακα Excel με C# – Πλήρης Οδηγός Προγραμματισμού

Έχετε ποτέ χρειαστεί να **διαγράψετε γραμμές πίνακα excel** από ένα βιβλίο εργασίας αλλά δεν ήσασταν σίγουροι ποια κλήση API να χρησιμοποιήσετε; Δεν είστε οι μόνοι—οι περισσότεροι προγραμματιστές συναντούν το ίδιο εμπόδιο όταν προσπαθούν για πρώτη φορά να μειώσουν έναν πίνακα προγραμματιστικά.  

Σε αυτόν τον οδηγό θα περάσουμε βήμα‑βήμα από ένα πλήρες, εκτελέσιμο παράδειγμα που όχι μόνο αφαιρεί γραμμές από έναν πίνακα Excel, αλλά δείχνει επίσης **πώς να προσθέσετε ορισμένο όνομα** (γνωστό και ως *named range*), πώς να **προσπελάσετε φύλλο εργασίας με το όνομα του**, και γιατί η προσθήκη διπλότυπου ονόματος σε άλλο φύλλο προκαλεί `InvalidOperationException`.  

Στο τέλος του άρθρου θα μπορείτε να:

* Πάρτε ένα φύλλο εργασίας χρησιμοποιώντας το όνομα της καρτέλας του.  
* Διαγράψετε με ασφάλεια τις γραμμές δεδομένων από τον πρώτο πίνακα σε αυτό το φύλλο.  
* Δημιουργήσετε ένα named range που δείχνει σε συγκεκριμένη διεύθυνση.  
* Κατανοήσετε τις παγίδες των διπλότυπων ονομάτων μεταξύ των φύλλων.

Δεν απαιτείται εξωτερική τεκμηρίωση—ό,τι χρειάζεστε είναι εδώ.

---

## Τι Θα Χρειαστείτε

* **DevExpress Spreadsheet** (ή οποιαδήποτε βιβλιοθήκη που εκθέτει αντικείμενα `Workbook`, `Worksheet`, `ListObject` και `Names`).  
* Ένα .NET project που στοχεύει **.NET 6** ή νεότερο (ο κώδικας μεταγλωττίζεται επίσης με .NET Framework 4.8).  
* Βασική εξοικείωση με C#—αν μπορείτε να γράψετε έναν βρόχο `foreach`, είστε έτοιμοι.

> **Pro tip:** Αν χρησιμοποιείτε την δωρεάν Community Edition του DevExpress, τα API που χρησιμοποιούνται παρακάτω είναι τα ίδια με την εμπορική έκδοση.

---

## Βήμα 1 – Πρόσβαση σε Φύλλο Εργασίας με το Όνομα

Το πρώτο που πρέπει να κάνετε είναι να εντοπίσετε το φύλλο που περιέχει τον πίνακα που θέλετε να τροποποιήσετε.  
Οι περισσότεροι προγραμματιστές τείνουν να χρησιμοποιούν `Worksheets[0]` από συνήθεια, αλλά αυτό συνδέει τον κώδικά σας με τη σειρά των φύλλων και σπάει μόλις κάποιος μετονομάσει μια καρτέλα.

```csharp
using DevExpress.Spreadsheet;

// Assume 'workbook' is an already‑loaded Workbook instance
Worksheet worksheet = workbook.Worksheets["Sheet1"];   // <-- access worksheet by name
```

*Γιατί είναι σημαντικό:* Χρησιμοποιώντας το **όνομα** του φύλλου αντί για το δείκτη του, αποφεύγετε τυχαίες επεμβάσεις στο λάθος φύλλο όταν το βιβλίο εργασίας αλλάζει.  

Αν το όνομα που δώσετε δεν υπάρχει, η βιβλιοθήκη ρίχνει `KeyNotFoundException`, το οποίο μπορείτε να πιάσετε για να εμφανίσετε ένα φιλικό μήνυμα σφάλματος.

---

## Βήμα 2 – Διαγραφή Γραμμών Πίνακα Excel (Ο Ασφαλής Τρόπος)

Τώρα που έχετε το σωστό φύλλο, ας αφαιρέσουμε τις γραμμές δεδομένων από τον πρώτο πίνακα.  
Ένα συχνό λάθος είναι η κλήση `DeleteRows(1, rowCount‑1)`. Από την **DevExpress 22.2** αυτή η υπερφόρτωση είναι **απαγορευμένη** και ρίχνει `InvalidOperationException`. Η βιβλιοθήκη απαιτεί να διαγράφετε γραμμές **μέσα στο εύρος δεδομένων του πίνακα**, όχι στη γραμμή κεφαλίδας.

```csharp
// Grab the first table (ListObject) on the sheet
var table = worksheet.ListObjects[0];

// Calculate how many data rows we actually have (excluding the header)
int dataRowCount = table.DataRange.RowCount;

// Delete only the data rows – keep the header intact
if (dataRowCount > 0)
{
    // DeleteRows(startRow, rowCount) – startRow is zero‑based within the table
    table.DeleteRows(0, dataRowCount);
}
```

> **Τι γίνεται αν ο πίνακας είναι κενός;** Η προειδοποίηση `if` αποτρέπει κλήση με `rowCount = 0`, η οποία διαφορετικά θα προκαλούσε εξαίρεση.

### Οπτική Επισκόπηση  

![παράδειγμα διαγραφής γραμμών πίνακα excel](image.png "Στιγμιότυπο οθόνης που δείχνει τη διαγραφή γραμμών από έναν πίνακα Excel")  

*Alt text: παράδειγμα διαγραφής γραμμών πίνακα excel σε κώδικα C#*

---

## Βήμα 3 – Πώς να Προσθέσετε Ορισμένο Όνομα (Δημιουργία Named Range)

Αφού καθαρίσετε τον πίνακα, ίσως θέλετε να αναφερθείτε σε ένα συγκεκριμένο εύρος αργότερα—π.χ. για γράφημα ή λίστα επικύρωσης δεδομένων. Εδώ έρχεται η **προσθήκη named range excel**.

```csharp
// Define a name that points to A1:C5 on Sheet1
workbook.Names.Add("MyTable", "Sheet1!$A$1:$C$5");

// Verify that the name exists
Name definedName = workbook.Names["MyTable"];
Console.WriteLine($"Defined name '{definedName.Name}' points to {definedName.RefersTo}");
```

Η μέθοδος `Names.Add` δέχεται δύο παραμέτρους: το αναγνωριστικό και τη διεύθυνση σε μορφή A1.  
Επειδή χρησιμοποιήσαμε **πρόσβαση σε φύλλο εργασίας με το όνομα** νωρίτερα, η συμβολοσειρά διεύθυνσης μπορεί με ασφάλεια να αναφέρεται σε οποιοδήποτε φύλλο χωρίς να ανησυχείτε για αλλαγές δεικτών.

---

## Βήμα 4 – Named Range σε Άλλο Φύλλο – Αποφυγή Σφαλμάτων Διπλότυπου Ονόματος

Μπορεί να σκεφτείτε ότι μπορείτε να επαναχρησιμοποιήσετε το ίδιο αναγνωριστικό σε διαφορετικό φύλλο, όπως παρακάτω:

```csharp
// Attempt to add the same name on Sheet2 – this will throw
workbook.Names.Add("MyTable", "Sheet2!$A$1:$C$5");
```

Δυστυχώς, η εμβέλεια ονομάτων του Excel είναι **σε επίπεδο βιβλίου εργασίας**, όχι ανά φύλλο. Η κλήση παραπάνω προκαλεί `InvalidOperationException` με το μήνυμα *«Υπάρχει ήδη ένα όνομα με το ίδιο αναγνωριστικό.»*  

### Πώς να το Παρακάμψετε

1. **Επιλέξτε ένα μοναδικό όνομα** (`MyTable_Sheet2`).  
2. **Διαγράψτε το υπάρχον όνομα** πριν το προσθέσετε ξανά (μόνο αν θέλετε πραγματικά να το αντικαταστήσετε).  

```csharp
// Option A – use a unique name
workbook.Names.Add("MyTable_Sheet2", "Sheet2!$A$1:$C$5");

// Option B – replace the existing name (use with caution)
if (workbook.Names.Contains("MyTable"))
    workbook.Names.Remove("MyTable");

workbook.Names.Add("MyTable", "Sheet2!$A$1:$C$5");
```

---

## Πλήρες, Εκτελέσιμο Παράδειγμα

Συνδυάζοντας όλα τα παραπάνω, εδώ είναι μια αυτόνομη εφαρμογή κονσόλας που μπορείτε να ενσωματώσετε στο Visual Studio και να τρέξετε εναντίον ενός δείγματος αρχείου `sample.xlsx`.

```csharp
using System;
using DevExpress.Spreadsheet;

class Program
{
    static void Main()
    {
        // Load an existing workbook (replace with your file path)
        Workbook workbook = new Workbook();
        workbook.LoadDocument("sample.xlsx");

        // -------------------------------------------------
        // Step 1 – Access the worksheet by its tab name
        // -------------------------------------------------
        Worksheet worksheet = workbook.Worksheets["Sheet1"]; // primary sheet

        // -------------------------------------------------
        // Step 2 – Delete rows excel table (safe method)
        // -------------------------------------------------
        var table = worksheet.ListObjects[0];
        int dataRows = table.DataRange.RowCount;
        if (dataRows > 0)
            table.DeleteRows(0, dataRows); // removes only data rows

        // -------------------------------------------------
        // Step 3 – Add a defined name (named range) on Sheet1
        // -------------------------------------------------
        workbook.Names.Add("MyTable", "Sheet1!$A$1:$C$5");

        // -------------------------------------------------
        // Step 4 – Demonstrate duplicate‑name handling
        // -------------------------------------------------
        try
        {
            workbook.Names.Add("MyTable", "Sheet2!$A$1:$C$5");
        }
        catch (InvalidOperationException ex)
        {
            Console.WriteLine("Duplicate name error: " + ex.Message);
            // Use a unique identifier instead
            workbook.Names.Add("MyTable_Sheet2", "Sheet2!$A$1:$C$5");
        }

        // Save the modified workbook
        workbook.SaveDocument("sample_modified.xlsx");
        Console.WriteLine("Workbook updated successfully.");
    }
}
```

**Αναμενόμενο αποτέλεσμα**

* Όλες οι γραμμές δεδομένων από τον πρώτο πίνακα στο **Sheet1** εξαφανίζονται, αφήνοντας μόνο τη γραμμή κεφαλίδας.  
* Το όνομα **MyTable** δείχνει πλέον στο `Sheet1!$A$1:$C$5`.  
* Ένα δεύτερο όνομα **MyTable_Sheet2** αναφέρεται με ασφάλεια σε εύρος στο **Sheet2** χωρίς να προκαλεί εξαίρεση.

---

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

| Ερώτηση | Απάντηση |
|----------|--------|
| *Τι γίνεται αν το βιβλίο εργασίας έχει πολλαπλούς πίνακες;* | Πάρτε το σωστό `ListObject` με δείκτη (`worksheet.ListObjects[1]`) ή με όνομα (`worksheet.ListObjects["MyTable"]`). |
| *Μπορώ να διαγράψω γραμμές από πίνακα που εκτείνεται σε πολλά φύλλα;* | Όχι—οι πίνακες περιορίζονται σε ένα μόνο φύλλο. Πρέπει να επαναλάβετε τη λογική διαγραφής για κάθε φύλλο. |
| *Υπάρχει τρόπος να διαγράψω μόνο ένα υποσύνολο γραμμών;* | Ναι—χρησιμοποιήστε `table.DeleteRows(startRow, count)` όπου το `startRow` είναι μηδενική βάση μέσα στην περιοχή δεδομένων του πίνακα. |
| *Διατηρούνται τα named ranges μετά την αποθήκευση;* | Απόλυτα. Μόλις καλέσετε `SaveDocument`, τα ονόματα γίνονται μέρος του XML του βιβλίου εργασίας. |
| *Πώς μπορώ να απαριθμήσω όλα τα ορισμένα ονόματα στο βιβλίο εργασίας;* | Κάντε `foreach (var name in workbook.Names) Console.WriteLine(name.Name);`. |

---

## Συμπέρασμα

Καλύψαμε **διαγραφή γραμμών πίνακα excel** με C#, παρουσιάσαμε **προσθήκη named range excel**, και δείξαμε τον σωστό τρόπο **πρόσβασης σε φύλλο εργασίας με το όνομα** αποφεύγοντας την ενοχλητική εξαίρεση διπλότυπου ονόματος.  

Η πλήρης λύση βρίσκεται στο παραπάνω απόσπασμα κώδικα—αντιγράψτε, επικολλήστε και τρέξτε το εναντίον των δικών σας αρχείων. Από εδώ μπορείτε να επεκτείνετε τη λογική για να διαχειριστείτε πολλαπλούς πίνακες, δυναμικούς υπολογισμούς περιοχών, ή ακόμη και να το ενσωματώσετε σε UI.

**Επόμενα βήματα** που μπορείτε να εξερευνήσετε:

* Χρησιμοποιήστε **named range σε άλλο φύλλο** για να τροφοδοτήσετε σειρές γραφήματος.  
* Συνδυάστε τη λογική διαγραφής με **ExcelDataReader** για εισαγωγή δεδομένων πριν τον καθαρισμό.  
* Αυτοματοποιήστε μαζικές ενημερώσεις σε δεκάδες βιβλία εργασίας με έναν απλό βρόχο `foreach (var file in Directory.GetFiles(...))`.

Έχετε περισσότερες ερωτήσεις σχετικά με την αυτοματοποίηση Excel σε C#; Αφήστε ένα σχόλιο και ας συνεχίσουμε τη συζήτηση. Καλή προγραμματιστική!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}