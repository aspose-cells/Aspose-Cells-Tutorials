---
category: general
date: 2026-03-29
description: Μάθετε πώς να εισάγετε σειρές στο GridJs γρήγορα. Αυτός ο οδηγός καλύπτει
  επίσης πώς να προσθέσετε σειρές και να προσθέσετε πολλές σειρές στο πλέγμα με μια
  λειτουργία δέσμης.
draft: false
keywords:
- how to insert rows
- how to add rows
- add multiple rows grid
- batch row insertion
- large grid performance
language: el
og_description: Μάθετε πώς να εισάγετε γραμμές στο GridJs γρήγορα. Αυτός ο οδηγός
  δείχνει πώς να προσθέτετε γραμμές, να προσθέτετε πολλαπλές γραμμές στο πλέγμα και
  να διαχειρίζεστε μεγάλες παρτίδες εισαγωγών.
og_title: Πώς να εισάγετε γραμμές στο GridJs – Προσθήκη πολλαπλών γραμμών στο πλέγμα
  αποδοτικά
tags:
- GridJs
- C#
- data‑grid
title: Πώς να εισάγετε γραμμές στο GridJs – Προσθήκη πολλαπλών γραμμών στο πλέγμα
  αποδοτικά
url: /el/net/row-and-column-management/how-to-insert-rows-in-gridjs-add-multiple-rows-grid-efficien/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Εισάγετε Γραμμές στο GridJs – Προσθήκη Πολλαπλών Γραμμών στο Grid Αποτελεσματικά

Έχετε αναρωτηθεί ποτέ **πώς να εισάγετε γραμμές** σε έναν τεράστιο πίνακα GridJs χωρίς να παγώνει η διεπαφή χρήστη; Ίσως έχετε συναντήσει πρόβλημα προσπαθώντας να **προσθέσετε γραμμές** μία‑μία και η απόδοση να καταρρέει. Τα καλά νέα είναι ότι το GridJs προσφέρει ένα batch API που σας επιτρέπει να **προσθέσετε πολλαπλές γραμμές grid** σε μία κλήση, διατηρώντας την ταχύτητα ακόμη και όταν εργάζεστε με εκατομμύρια εγγραφές.

Σε αυτό το tutorial θα περάσουμε από ένα πλήρες, εκτελέσιμο παράδειγμα που δείχνει ακριβώς **πώς να εισάγετε γραμμές** χρησιμοποιώντας το `InsertRowsBatch`. Θα δείτε γιατί η ομαδοποίηση (batching) είναι σημαντική, πώς να επαληθεύσετε το αποτέλεσμα, και τι πρέπει να προσέξετε όταν ο δείκτης που στοχεύετε είναι τεράστιος. Στο τέλος θα μπορείτε να προσθέσετε χίλιες νέες εγγραφές σε οποιαδήποτε παρουσία του GridJs με σιγουριά.

## Προαπαιτούμενα

Πριν προχωρήσουμε, βεβαιωθείτε ότι έχετε:

- .NET 6.0 ή νεότερο (ο κώδικας μεταγλωττίζεται με οποιοδήποτε πρόσφατο SDK)
- Αναφορά στο πακέτο NuGet `GridJs` (ή το DLL αν χρησιμοποιείτε προσαρμοσμένη έκδοση)
- Βασικές γνώσεις C# – δεν χρειάζεται να είστε γκουρού, απλώς άνετοι με κλάσεις και μεθόδους
- Ένα IDE ή επεξεργαστή της επιλογής σας (Visual Studio, Rider, VS Code… όλα λειτουργούν)

> **Pro tip:** Αν σκοπεύετε να δουλέψετε με πραγματικά τεράστιες πλέγματα (δέκαδες εκατομμύρια γραμμές), ενεργοποιήστε `gridJs.EnableVirtualization = true;` για να διατηρήσετε το UI ελαφρύ.

## Βήμα 1: Δημιουργία και Διαμόρφωση της Παράστασης GridJs

Πρώτα απ' όλα: χρειάζεστε ένα ζωντανό αντικείμενο `GridJs`. Σκεφτείτε το ως τον καμβά πάνω στον οποίο θα σχεδιάσετε τις γραμμές.

```csharp
using System;
using GridJsLibrary;   // Assume this is the namespace for GridJs

namespace GridJsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1 – Initialize the grid
            GridJs gridJs = new GridJs();

            // Optional: turn on virtualization for huge data sets
            gridJs.EnableVirtualization = true;

            // Populate the grid with some dummy data so we can see the effect
            SeedInitialData(gridJs);

            // Now we’re ready to insert rows in bulk
            InsertRowsInBatch(gridJs);
        }

        // Helper: add 2 000 000 rows so our batch lands at index 2 000 001
        static void SeedInitialData(GridJs grid)
        {
            for (int i = 0; i < 2_000_000; i++)
            {
                grid.InsertRow(i, new object[] { $"Row {i + 1}", DateTime.Now });
            }
            Console.WriteLine("Initial seed completed – 2 000 000 rows present.");
        }
```

> **Γιατί είναι σημαντικό αυτό το βήμα:** Η αρχικοποίηση του πλέγματος και η προαιρετική προ-συμπλήρωση δεδομένων αντικατοπτρίζει ένα πραγματικό σενάριο όπου το grid ήδη περιέχει μεγάλο όγκο πληροφοριών. Η ομαδική εισαγωγή που θα κάνουμε αργότερα πρέπει να σέβεται τον μηδενικό δείκτη, γι' αυτό προ-συμπληρώνουμε για να δείξουμε το ακριβές σημείο εισαγωγής.

## Βήμα 2: Χρήση του `InsertRowsBatch` για **Add Multiple Rows Grid**

Τώρα το κύριο μέρος του tutorial – η κλήση που πραγματικά **προσθέτει γραμμές** μαζικά. Η υπογραφή της μεθόδου είναι `InsertRowsBatch(int startIndex, int count)`. Στο παράδειγμά μας θα ξεκινήσουμε στον δείκτη 2 000 000 (που αντιστοιχεί στη 2 000 001η γραμμή) και θα προσθέσουμε δέκα γραμμές.

```csharp
        // Step 2 – Insert a batch of rows
        static void InsertRowsInBatch(GridJs grid)
        {
            int startIndex = 2_000_000; // zero‑based, so this is row 2 000 001
            int rowsToAdd = 10;

            // The batch call creates placeholder rows; you can later populate them
            grid.InsertRowsBatch(startIndex, rowsToAdd);
            Console.WriteLine($"Inserted {rowsToAdd} rows starting at index {startIndex + 1}.");

            // Verify by reading back a few rows
            VerifyInsertion(grid, startIndex, rowsToAdd);
        }
```

> **Πώς λειτουργεί:** Το `InsertRowsBatch` κατανέμει εσωτερικά τον ζητούμενο αριθμό γραμμών και μετατοπίζει τις υπάρχουσες γραμμές προς τα κάτω. Επειδή η λειτουργία εκτελείται σε μία ενιαία συναλλαγή, η ανανέωση του UI γίνεται μόνο μία φορά, γι' αυτό αυτή η μέθοδος είναι ο προτεινόμενος τρόπος για **πώς να προσθέσετε γραμμές** αποδοτικά.

## Βήμα 3: Επαλήθευση της Εισαγωγής – Οι Γραμμές Τοποθετήθηκαν Όπως Αναμενόταν;

Μετά την ομαδική λειτουργία θα θέλετε να βεβαιωθείτε ότι οι γραμμές βρίσκονται εκεί που νομίζετε. Ο παρακάτω βοηθός διαβάζει την πρώτη και την τελευταία γραμμή του νέου μπλοκ και τις εκτυπώνει στην κονσόλα.

```csharp
        // Step 3 – Simple verification
        static void VerifyInsertion(GridJs grid, int startIdx, int count)
        {
            Console.WriteLine("Verifying inserted rows:");
            for (int i = 0; i < count; i++)
            {
                var row = grid.GetRow(startIdx + i);
                Console.WriteLine($"Row {startIdx + i + 1}: {string.Join(", ", row)}");
            }
        }
    }
}
```

**Αναμενόμενη έξοδος**

```
Initial seed completed – 2 000 000 rows present.
Inserted 10 rows starting at index 2000001.
Verifying inserted rows:
Row 2000001: , 
Row 2000002: , 
...
Row 2000010: , 
```

Τα κενά κελιά υποδεικνύουν ότι οι γραμμές είναι placeholders που περιμένουν δεδομένα. Μπορείτε τώρα να τις συμπληρώσετε ξεχωριστά ή να εκτελέσετε μια άλλη ομαδική ενημέρωση.

> **Σημείωση για ειδικές περιπτώσεις:** Αν το `startIndex` υπερβαίνει τον τρέχοντα αριθμό γραμμών, το GridJs θα προσθέσει αυτόματα τις νέες γραμμές στο τέλος. Αντίθετα, ένας αρνητικός δείκτης προκαλεί `ArgumentOutOfRangeException`, οπότε πάντα επικυρώνετε τους δείκτες που παρέχονται από τον χρήστη.

## Βήμα 4: Συμπλήρωση των Νέων Γραμμών (Προαιρετικό αλλά Συνηθισμένο)

Συχνά δεν θέλετε απλώς κενές γραμμές· χρειάζεται να τις γεμίσετε με ουσιαστικές τιμές. Μπορείτε να κάνετε βρόχο πάνω στο νέο εύρος και να καλέσετε `SetCell` ή κάποιο παρόμοιο API.

```csharp
        // Optional: fill the newly added rows with sample data
        static void PopulateNewRows(GridJs grid, int startIdx, int count)
        {
            for (int i = 0; i < count; i++)
            {
                int rowIdx = startIdx + i;
                grid.SetCell(rowIdx, 0, $"New Item {i + 1}");
                grid.SetCell(rowIdx, 1, DateTime.UtcNow);
            }
            Console.WriteLine("Populated the new rows with sample data.");
        }
```

Μπορείτε να καλέσετε `PopulateNewRows(gridJs, startIndex, rowsToAdd);` αμέσως μετά την ομαδική εισαγωγή αν χρειάζεστε τις γραμμές έτοιμες για εμφάνιση αμέσως.

## Βήμα 5: Συμβουλές Απόδοσης για Πολύ Μεγάλα Grids

Όταν δουλεύετε με **add multiple rows grid** σε εκατομμύρια, κρατήστε αυτές τις τεχνικές στο μυαλό:

1. **Το μέγεθος του batch μετρά** – Η εισαγωγή 10 000 γραμμών ταυτόχρονα μπορεί να είναι γρηγορότερη από δέκα ξεχωριστά batch των 1 000 γραμμών, επειδή κάθε batch προκαλεί μόνο μία ανανέωση UI.
2. **Απενεργοποιήστε τις ενημερώσεις UI** – Ορισμένες εκδόσεις του GridJs εκθέτουν `grid.SuspendLayout()` / `grid.ResumeLayout()`. Τυλίξτε το batch σας μέσα σε αυτές τις κλήσεις αν παρατηρήσετε καθυστέρηση.
3. **Χρησιμοποιήστε virtualization** – Όπως δείξαμε νωρίτερα, το `EnableVirtualization` μειώνει δραστικά τη χρήση μνήμης και τον χρόνο απόδοσης.
4. **Αποφύγετε τα βαριά αντίγραφα** – Περάστε απλούς τύπους τιμών ή ελαφριά αντικείμενα στο grid· τα βαριά αντικείμενα αναγκάζουν το grid να κλωνοποιήσει τα δεδομένα, μειώνοντας την απόδοση.

## Πλήρες Παράδειγμα Λειτουργίας

Συνδυάζοντας όλα τα παραπάνω, εδώ είναι το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε‑και‑επικολλήσετε σε ένα νέο έργο console:

```csharp
using System;
using GridJsLibrary;   // Replace with the actual namespace of your GridJs library

namespace GridJsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            GridJs gridJs = new GridJs
            {
                EnableVirtualization = true
            };

            SeedInitialData(gridJs);
            InsertRowsInBatch(gridJs);
        }

        static void SeedInitialData(GridJs grid)
        {
            for (int i = 0; i < 2_000_000; i++)
            {
                grid.InsertRow(i, new object[] { $"Row {i + 1}", DateTime.Now });
            }
            Console.WriteLine("Initial seed completed – 2 000 000 rows present.");
        }

        static void InsertRowsInBatch(GridJs grid)
        {
            int startIndex = 2_000_000; // zero‑based index for row 2 000 001
            int rowsToAdd = 10;

            grid.InsertRowsBatch(startIndex, rowsToAdd);
            Console.WriteLine($"Inserted {rowsToAdd} rows starting at index {startIndex + 1}.");

            // Optional: fill them with data
            PopulateNewRows(grid, startIndex, rowsToAdd);

            VerifyInsertion(grid, startIndex, rowsToAdd);
        }

        static void PopulateNewRows(GridJs grid, int startIdx, int count)
        {
            for (int i = 0; i < count; i++)
            {
                int rowIdx = startIdx + i;
                grid.SetCell(rowIdx, 0, $"New Item {i + 1}");
                grid.SetCell(rowIdx, 1, DateTime.UtcNow);
            }
            Console.WriteLine("Populated the new rows with sample data.");
        }

        static void VerifyInsertion(GridJs grid, int startIdx, int count)
        {
            Console.WriteLine("Verifying inserted rows:");
            for (int i = 0; i < count; i++)
            {
                var row = grid.GetRow(startIdx + i);
                Console.WriteLine($"Row {startIdx + i + 1}: {string.Join(", ", row)}");
            }
        }
    }
}
```

Εκτελέστε το πρόγραμμα και θα δείτε την έξοδο της κονσόλας που επιβεβαιώνει ότι οι δέκα γραμμές εισήχθησαν στη σωστή θέση και στη συνέχεια συμπληρώθηκαν.

## Συμπέρασμα

Καλύψαμε **πώς να εισάγετε γραμμές** στο GridJs χρησιμοποιώντας το batch API, δείξαμε **πώς να προσθέσετε γραμμές** αποδοτικά, και εξετάσαμε τρόπους για **add multiple rows grid** χωρίς να “πνίγουμε” το UI. Τα κύρια σημεία είναι:

- Χρησιμοποιήστε `InsertRowsBatch(startIndex, count)` για οποιαδήποτε μαζική λειτουργία.
- Επικυρώστε τους δείκτες και σκεφτείτε virtualization για τεράστιες βάσεις δεδομένων.
- Συμπληρώστε τις γραμμές μετά το batch αν χρειάζεστε άμεσο περιεχόμενο.

Στη συνέχεια, ίσως θέλετε να εξερευνήσετε **πώς να διαγράψετε γραμμές**, να υλοποιήσετε **undo/redo** για ομαδικές επεξεργασίες, ή να ενσωματώσετε το GridJs με μια back‑end υπηρεσία που ρέει δεδομένα κατ' απαίτηση. Όλα αυτά τα θέματα βασίζονται άμεσα στις έννοιες που μόλις μάθατε.

Μη διστάσετε να πειραματιστείτε—αλλάξτε το μέγεθος του batch, δοκιμάστε εισαγωγή στην αρχή του grid, ή συνδυάστε πολλαπλά batches σε μία συναλλαγή. Όσο περισσότερο παίζετε, τόσο πιο άνετα θα νιώθετε με μεγάλα

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}