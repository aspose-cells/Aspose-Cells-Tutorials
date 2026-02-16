---
category: general
date: 2026-02-15
description: Δημιουργήστε νέο βιβλίο εργασίας σε C# και αντιγράψτε έναν συγκεντρωτικό
  πίνακα χωρίς να χάσετε τον ορισμό του. Μάθετε πώς να αντιγράφετε γραμμές, να διατηρείτε
  τον συγκεντρωτικό πίνακα και να τον αντιγράφετε εύκολα.
draft: false
keywords:
- create new workbook
- copy pivot table
- preserve pivot table
- how to copy rows
- duplicate pivot table
language: el
og_description: Δημιουργήστε νέο βιβλίο εργασίας σε C# και αντιγράψτε έναν πίνακα
  Pivot διατηρώντας τον ορισμό του. Οδηγός βήμα‑προς‑βήμα για προγραμματιστές.
og_title: Δημιουργία νέου βιβλίου εργασίας σε C# – Διατήρηση Πίνακα Pivot
tags:
- Aspose.Cells
- C#
- Excel automation
title: Δημιουργία νέου βιβλίου εργασίας σε C# – Διατήρηση του Πίνακα Pivot
url: /el/net/pivot-tables/create-new-workbook-in-c-preserve-pivot-table/
---

later.

- **create new workbook** in conclusion.

- **copy pivot table** maybe appears: "**copy pivot table**". It appears in conclusion: "**copy pivot table**". Translate to "**αντιγράψετε pivot table**"? Actually original phrase: "**copy pivot table**". We'll translate to "**αντιγράψετε pivot table**". Keep bold.

- **preserve pivot table** again.

- **how to copy rows** again.

- **duplicate pivot table** again.

Make sure all bold markers are correct.

Now produce final content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία Νέου Βιβλίου Εργασίας σε C# – Διατήρηση Pivot Table

Έχετε ποτέ χρειαστεί να **δημιουργήσετε νέο βιβλίο εργασίας** σε C# που περιέχει ακριβή αντίγραφο ενός pivot table από άλλο αρχείο; Δεν είστε ο μόνος. Σε πολλές αλυσίδες αναφορών, το pivot table είναι η καρδιά της ανάλυσης, και η απώλεια του ορισμού του όταν μετακινείτε δεδομένα είναι εφιάλτης.

Τα καλά νέα; Με λίγες γραμμές κώδικα Aspose.Cells μπορείτε να αντιγράψετε γραμμές—συμπεριλαμβανομένου του pivot table—σε ένα νέο βιβλίο εργασίας και να διατηρήσετε όλα ανέπαφα. Παρακάτω θα δείτε **πώς να αντιγράψετε γραμμές**, **διατήρηση pivot table** ρυθμίσεων, και ακόμη **αντιγραφή pivot table** σε πολλά αρχεία χωρίς να σπάσουν τύποι ή η μνήμη cache.

## Τι Καλύπτει Αυτό το Εγχειρίδιο

1. Φόρτωση του πηγαίου βιβλίου εργασίας που ήδη περιέχει ένα pivot table.  
2. **Δημιουργήσετε νέο βιβλίο εργασίας** objects for the destination.  
3. Χρήση του `CopyRows` για τη μεταφορά της περιοχής που περιέχει το pivot table.  
4. Αποθήκευση του αποτελέσματος διασφαλίζοντας ότι το pivot table παραμένει λειτουργικό.

Δεν απαιτείται εξωτερική τεκμηρίωση—απλώς ο κώδικας, το γιατί, και μια σειρά πρακτικών συμβουλών που μπορείτε να επικολλήσετε απευθείας στο έργο σας.

> **Pro tip:** Το Aspose.Cells λειτουργεί με .NET Core, .NET Framework, και ακόμη και Xamarin, έτσι το ίδιο απόσπασμα εκτελείται όπου το χρειάζεστε.

![Δημιουργία νέου βιβλίου εργασίας με αντιγραμμένο pivot table](/images/create-new-workbook-pivot.png "Δημιουργία νέου βιβλίου εργασίας με αντιγραμμένο pivot table")

## Βήμα 1 – Δημιουργία Νέου Βιβλίου Εργασίας και Φόρτωση του Πηγαίου Αρχείου

Το πρώτο που κάνουμε είναι να δημιουργήσουμε **δημιουργήσετε νέο βιβλίο εργασίας** objects. Ένα κρατά τα αρχικά δεδομένα, το άλλο θα λάβει την αντιγραμμένη περιοχή.

```csharp
using Aspose.Cells;

// Load the source workbook that already contains a pivot table
var sourceWorkbook = new Workbook(@"C:\Data\source.xlsx");

// Create an empty workbook that will become the destination
var destinationWorkbook = new Workbook();
```

*Γιατί είναι σημαντικό:*  
`Workbook` είναι το σημείο εισόδου για οποιαδήποτε επεξεργασία Excel στο Aspose.Cells. Δημιουργώντας ένα νέο workbook εξασφαλίζουμε ένα καθαρό ξεκίνημα—χωρίς κρυφά στυλ ή περιττά φύλλα εργασίας που θα μπορούσαν να παρεμβαλλονται αργότερα.

## Βήμα 2 – Πώς να Αντιγράψετε Γραμμές Συμπεριλαμβανομένου ενός Pivot Table

Τώρα έρχεται ο πυρήνας του προβλήματος: **πώς να αντιγράψετε γραμμές** που περιλαμβάνουν το pivot table χωρίς να το «απλώνουν». Η μέθοδος `CopyRows` κάνει ακριβώς αυτό.

```csharp
// Copy the first 20 rows (adjust as needed) from the source to the destination
// Parameters: startRow, totalRows, targetCells, targetStartRow
sourceWorkbook.Worksheets[0].Cells.CopyRows(
    startRow: 0,
    totalRows: 20,
    targetCells: destinationWorkbook.Worksheets[0].Cells,
    targetStartRow: 0);
```

Μερικά σημεία που πρέπει να σημειώσετε:

* `startRow` και `totalRows` ορίζουν το μπλοκ που περιέχει το pivot table.  
* Η μέθοδος αντιγράφει **και τα δύο** τα ακατέργαστα δεδομένα και την cache του pivot, ώστε το προοριστικό βιβλίο εργασίας να ξέρει πώς να ξαναχτίσει το pivot table άμεσα.  
* Αν το pivot σας ξεκινά πιο βαθιά στο φύλλο, απλώς αλλάξτε τα δείκτες—δεν χρειάζεται διαφορετική κλήση API.

> **Common question:** *Θα χάσει το αντιγραμμένο pivot την αναφορά στα δεδομένα πηγής;*  
> Όχι. Το Aspose.Cells ενσωματώνει την cache απευθείας στο φύλλο εργασίας, έτσι το pivot γίνεται αυτόνομο στο νέο αρχείο.

## Βήμα 3 – Διατήρηση Pivot Table Κατά την Αποθήκευση του Προορισμού

Αφού αντιγραφούν οι γραμμές, το pivot table βρίσκεται στο προοριστικό βιβλίο εργασίας ακριβώς όπως ήταν στο πηγαίο. Η αποθήκευση του αρχείου είναι απλή.

```csharp
// Save the destination workbook; the pivot table remains functional
destinationWorkbook.Save(@"C:\Data\destination.xlsx");
```

Όταν ανοίξετε το `destination.xlsx` στο Excel, θα δείτε το pivot table έτοιμο για ανανέωση. Η συμπεριφορά **διατήρηση pivot table** είναι αυτόματη επειδή η cache μεταφέρθηκε μαζί με τις γραμμές.

### Επαλήθευση του Αποτελέσματος

Ανοίξτε το αρχείο και:

1. Κάντε κλικ στο pivot table.  
2. Παρατηρήστε ότι εμφανίζεται η λίστα πεδίων—αυτό σημαίνει ότι η cache είναι άθικτη.  
3. Δοκιμάστε μια ανανέωση· τα δεδομένα ενημερώνονται χωρίς σφάλματα.

Αν αντιμετωπίσετε σφάλμα *#REF!* , ελέγξτε ξανά ότι η αντιγραμμένη περιοχή περιλαμβάνει τις κρυφές γραμμές cache (συνήθως αμέσως μετά τα ορατά δεδομένα).

## Βήμα 4 – Αντιγραφή Pivot Table σε Πολλαπλά Βιβλία Εργασίας (Προαιρετικό)

Μερικές φορές χρειάζεστε το ίδιο pivot σε πολλές αναφορές. Το μοτίβο που χρησιμοποιήσαμε κλιμακώνεται εύκολα—απλώς επαναλάβετε την αντιγραφή για κάθε νέο βιβλίο εργασίας.

```csharp
string[] targets = {
    @"C:\Reports\Q1.xlsx",
    @"C:\Reports\Q2.xlsx",
    @"C:\Reports\Q3.xlsx"
};

foreach (var path in targets)
{
    var wb = new Workbook(); // fresh workbook each loop
    sourceWorkbook.Worksheets[0].Cells.CopyRows(0, 20, wb.Worksheets[0].Cells, 0);
    wb.Save(path);
}
```

Αυτό το απόσπασμα **αντιγράφει pivot table** τρεις φορές με έναν βρόχο. Προσαρμόστε τον πίνακα `targets` ώστε να ταιριάζει με το πρόγραμμα αναφορών σας.

### Περιπτώσεις Όρια που Πρέπει να Λάβετε Υπόψη

| Κατάσταση | Σε τι Πρέπει να Προσέξετε | Διόρθωση |
|-----------|---------------------------|----------|
| Το Pivot χρησιμοποιεί εξωτερική πηγή δεδομένων | Η cache μπορεί να αναφέρεται σε σύνδεση που δεν υπάρχει στο νέο μηχάνημα | Ενσωματώστε την πηγή δεδομένων ή δημιουργήστε ξανά τη σύνδεση στο προοριστικό βιβλίο εργασίας |
| Πολύ μεγάλο pivot ( > 100 k γραμμές ) | Η `CopyRows` μπορεί να απαιτεί πολύ μνήμη | Χρησιμοποιήστε την `CopyRows` σε τμήματα ή εξετάστε το `Copy` με `PasteOptions` για περιορισμό της χρήσης μνήμης |
| Το φύλλο εργασίας έχει κρυφές γραμμές/στήλες | Οι κρυφές γραμμές cache μπορεί να παραλειφθούν αν αντιγράψετε μόνο τις ορατές γραμμές | Πάντα αντιγράψτε την ακριβή περιοχή γραμμών που περιέχει την cache, όχι μόνο την ορατή περιοχή |

## Πλήρες Παράδειγμα Λειτουργίας

Συνδυάζοντας όλα, εδώ είναι ένα αυτόνομο πρόγραμμα που μπορείτε να ενσωματώσετε σε μια εφαρμογή κονσόλας.

```csharp
using System;
using Aspose.Cells;

namespace PivotCopyDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load source workbook (contains the original pivot)
            var sourcePath = @"C:\Data\source.xlsx";
            var sourceWorkbook = new Workbook(sourcePath);

            // 2️⃣ Prepare destination workbook
            var destinationWorkbook = new Workbook();

            // 3️⃣ Copy rows that include the pivot (adjust range as needed)
            sourceWorkbook.Worksheets[0].Cells.CopyRows(
                startRow: 0,
                totalRows: 20,
                targetCells: destinationWorkbook.Worksheets[0].Cells,
                targetStartRow: 0);

            // 4️⃣ Save – the pivot table is preserved
            var destPath = @"C:\Data\destination.xlsx";
            destinationWorkbook.Save(destPath);

            Console.WriteLine("Pivot table successfully copied!");
        }
    }
}
```

Εκτελέστε το πρόγραμμα, ανοίξτε το `destination.xlsx`, και θα δείτε το ίδιο pivot table έτοιμο να διαχωρίσει και να αναλύσει τα δεδομένα σας. Δεν απαιτείται χειροκίνητη δημιουργία.

---

## Συμπέρασμα

Μόλις δείξαμε πώς να **δημιουργήσετε νέο βιβλίο εργασίας** σε C# και **αντιγράψετε pivot table** διατηρώντας όλες τις ρυθμίσεις ζωντανές. Χρησιμοποιώντας την `CopyRows` αποκτάτε έναν αξιόπιστο τρόπο για **διατήρηση pivot table** λειτουργικότητας, απαντώντας στην παλιά ερώτηση “**πώς να αντιγράψετε γραμμές**”, και ακόμη **αντιγράψτε pivot table** σε πολλαπλές αναφορές με ελάχιστο κώδικα.

Επόμενα βήματα; Δοκιμάστε να αλλάξετε την αντιγραμμένη περιοχή ώστε να περιλαμβάνει γραφήματα που αναφέρονται στο ίδιο pivot, ή πειραματιστείτε με το `PasteOptions` για ακριβή διατήρηση μορφοποίησης. Το ίδιο μοτίβο λειτουργεί για άλλα αντικείμενα Aspose.Cells όπως πίνακες και ονομασμένες περιοχές, οπότε αισθανθείτε ελεύθεροι να το επεκτείνετε.

Έχετε κάποιο πρόβλημα που προσπαθείτε να λύσετε—ίσως ένα pivot που αντλεί από εξωτερική βάση δεδομένων, ή ένα βιβλίο εργασίας που βρίσκεται στο cloud; Αφήστε ένα σχόλιο παρακάτω και θα το αντιμετωπίσουμε μαζί. Καλή προγραμματιστική!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}