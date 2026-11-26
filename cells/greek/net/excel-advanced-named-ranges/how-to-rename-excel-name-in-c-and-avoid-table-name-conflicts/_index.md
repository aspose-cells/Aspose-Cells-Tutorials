---
category: general
date: 2026-11-25
description: Πώς να μετονομάσετε ένα όνομα Excel σε C# ενώ διαχειρίζεστε συγκρούσεις
  ονομάτων πινάκων. Μάθετε πώς να δημιουργήσετε βιβλίο εργασίας Excel με C# και να
  επιλύετε αποτελεσματικά προβλήματα ονοματοδοσίας.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to rename excel name
- create excel workbook c#
- excel table name conflict
language: el
lastmod: 2026-11-25
og_description: Πώς να μετονομάσετε το όνομα Excel σε C# και να λύσετε τις συγκρούσεις
  ονομάτων πινάκων Excel. Ακολουθήστε αυτόν τον βήμα‑βήμα οδηγό για να δημιουργήσετε
  ένα βιβλίο εργασίας Excel με C# και να διαχειριστείτε με ασφάλεια την ονομασία.
og_image_alt: Screenshot of C# code that renames an Excel name without conflict
og_title: Πώς να μετονομάσετε το όνομα Excel σε C# – αποτρέψτε τις συγκρούσεις ονομάτων
  πινάκων
schemas:
- author: Aspose
  dateModified: '2026-11-25'
  description: How to rename Excel name in C# while handling table name conflicts.
    Learn to create Excel workbook C# and resolve naming issues efficiently.
  headline: How to rename Excel name in C# and avoid table name conflicts
  type: TechArticle
- description: How to rename Excel name in C# while handling table name conflicts.
    Learn to create Excel workbook C# and resolve naming issues efficiently.
  name: How to rename Excel name in C# and avoid table name conflicts
  steps:
  - name: Create Excel workbook in C# (secondary keyword)
    text: 'Start by adding the Aspose.Cells NuGet package to your project:'
  - name: Add a table and a conflicting defined name (secondary keyword)
    text: Next we add a ListObject (Excel table) and deliberately create a defined
      name that would clash.
  - name: Detect and resolve an Excel table name conflict (secondary keyword)
    text: Before renaming, scan the workbook’s `Names` collection and the worksheet’s
      `ListObjects` collection to ensure the target name is free.
  - name: Expected output and verification
    text: 'Running the program produces console output similar to:'
  - name: What the code does
    text: 1. **Creates** a new Excel workbook (`create excel workbook c#`). 2. **Adds**
      a table called *SalesTable* (demonstrating the conflict source). 3. **Attempts**
      to rename a defined name to *SalesTable*. 4. **Detects** the conflict with `IsNameConflict`.
      5. **Renames** the table first, then safely rena
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
title: Πώς να μετονομάσετε το όνομα Excel σε C# και να αποφύγετε τις συγκρούσεις ονομάτων
  πινάκων
url: /el/net/excel-advanced-named-ranges/how-to-rename-excel-name-in-c-and-avoid-table-name-conflicts/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να μετονομάσετε ένα όνομα Excel σε C# και να αποφύγετε συγκρούσεις ονομάτων πινάκων

Αν χρειάζεστε **how to rename excel name** χωρίς να προκαλέσετε σφάλμα, αυτός ο οδηγός σας δείχνει τα ακριβή βήματα. Θα δείτε γιατί ένα όνομα πίνακα μπορεί να συγκρουστεί με ένα όνομα σε επίπεδο βιβλίου εργασίας και πώς να το μετονομάσετε με ασφάλεια όταν **create excel workbook c#** προγράμματα.

Η μετονομασία ενός ονόματος Excel είναι συχνή εργασία όταν δημιουργείτε αναφορές προγραμματιστικά. Ο ενσωματωμένος διαχειριστής ονομάτων αντιμετωπίζει τους πίνακες φύλλων εργασίας (ListObjects) και τα ορισμένα ονόματα ως μέρος του ίδιου ονοματοχώρου, έτσι μια σύγκρουση εμφανίζεται αμέσως μόλις προσπαθήσετε να δώσετε σε ένα ορισμένο όνομα τον ίδιο ταυτοποιητή με έναν πίνακα. Αυτό το tutorial σας καθοδηγεί μέσα από τη πλήρη λύση, από τη δημιουργία του βιβλίου εργασίας μέχρι τη μετονομασία με επίγνωση των συγκρούσεων, χρησιμοποιώντας το Aspose.Cells για .NET.

## Πώς να μετονομάσετε ένα όνομα Excel σε C# (primary keyword)

Όταν προσπαθείτε να ορίσετε `conflictingName.Name = "SalesTable"` ενώ υπάρχει ήδη ένας πίνακας με το όνομα **SalesTable**, το Aspose.Cells εγείρει μια εξαίρεση. Η λύση είναι:

1. Να εντοπίσετε τη σύγκρουση πριν από τη μετονομασία, **or**  
2. Να μετονομάσετε πρώτα τον πίνακα, στη συνέχεια να αναθέσετε το επιθυμητό όνομα στο ορισμένο όνομα.

### Βήμα 1: Δημιουργία βιβλίου εργασίας Excel σε C# (secondary keyword)

Ξεκινήστε προσθέτοντας το πακέτο NuGet Aspose.Cells στο έργο σας:

```bash
dotnet add package Aspose.Cells
```

Στη συνέχεια γράψτε τον βασικό κώδικα που δημιουργεί ένα βιβλίο εργασίας και ένα φύλλο εργασίας:

```csharp
using System;
using Aspose.Cells;

namespace ExcelRenameDemo
{
    class Program
    {
        static void Main()
        {
            // Create a new workbook and get the first worksheet
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];
```

*Γιατί είναι σημαντικό:* Το αντικείμενο `Workbook` αντιπροσωπεύει ολόκληρο το αρχείο Excel. Από προεπιλογή περιέχει ένα φύλλο εργασίας, το οποίο αναφερόμαστε για περαιτέρω λειτουργίες.

### Βήμα 2: Προσθήκη πίνακα και συγκρουόμενου ορισμένου ονόματος (secondary keyword)

Στη συνέχεια προσθέτουμε ένα ListObject (πίνακας Excel) και δημιουργούμε σκόπιμα ένα ορισμένο όνομα που θα συγκρουστεί.

```csharp
            // Add a table (ListObject) that occupies cells A1:C5
            ListObject salesTable = worksheet.ListObjects.Add(0, 0, 5, 3, TableStyleType.Light1);
            salesTable.Name = "SalesTable";

            // Define a workbook‑level name that initially does NOT conflict
            Name definedName = workbook.Worksheets[0].Names.Add("TempName");
```

*Εξήγηση:* Ο πίνακας λαμβάνει το όνομα **SalesTable**. Το ορισμένο όνομα `TempName` είναι αβλαβές σε αυτό το σημείο, αλλά αργότερα θα προσπαθήσουμε να το μετονομάσουμε σε **SalesTable**, κάτι που θα προκαλέσει σύγκρουση.

### Βήμα 3: Ανίχνευση και επίλυση συγκρούσεων ονόματος πίνακα Excel (secondary keyword)

Πριν από τη μετονομασία, σαρώστε τη συλλογή `Names` του βιβλίου εργασίας και τη συλλογή `ListObjects` του φύλλου εργασίας για να βεβαιωθείτε ότι το επιθυμητό όνομα είναι ελεύθερο.

```csharp
            string desiredName = "SalesTable";

            bool conflict = IsNameConflict(workbook, worksheet, desiredName);

            if (conflict)
            {
                Console.WriteLine($"Cannot rename defined name to \"{desiredName}\" because a table with that name already exists.");
                // Optionally, rename the table first or choose a different name
                salesTable.Name = "SalesTable_Alt";
                Console.WriteLine($"Table renamed to \"{salesTable.Name}\". Now you can reuse \"{desiredName}\" for the defined name.");
                definedName.Name = desiredName; // This now succeeds
            }
            else
            {
                definedName.Name = desiredName; // Safe rename
                Console.WriteLine($"Defined name renamed to \"{desiredName}\" successfully.");
            }

            // Save the workbook to verify the result
            workbook.Save("RenameResult.xlsx");
        }

        /// <summary>
        /// Checks whether the desired name collides with any existing table or defined name.
        /// </summary>
        static bool IsNameConflict(Workbook wb, Worksheet ws, string name)
        {
            // Check table names (ListObjects)
            foreach (ListObject lo in ws.ListObjects)
            {
                if (string.Equals(lo.Name, name, StringComparison.OrdinalIgnoreCase))
                    return true;
            }

            // Check defined names at workbook level
            foreach (Name n in wb.Worksheets[0].Names)
            {
                if (string.Equals(n.Name, name, StringComparison.OrdinalIgnoreCase))
                    return true;
            }

            return false;
        }
    }
}
```

**Γιατί είναι χρήσιμος ο βοηθός:**  
- Το `ListObject.Name` ζει στον ίδιο ονοματοχώρο με το `Name.Name`.  
- Η `IsNameConflict` αφαιρεί την λογική ελέγχου, καθιστώντας τον κώδικα επαναχρησιμοποιήσιμο όποτε χρειάζεται να μετονομάσετε ένα όνομα με ασφάλεια.  
- Μετονομάζοντας πρώτα τον πίνακα (`salesTable.Name = "SalesTable_Alt"`), ελευθερώνετε τον αρχικό ταυτοποιητή, επιτρέποντας στο ορισμένο όνομα να τον υιοθετήσει χωρίς σφάλμα.

### Βήμα 4: Αναμενόμενο αποτέλεσμα και επαλήθευση

Η εκτέλεση του προγράμματος παράγει έξοδο κονσόλας παρόμοια με:

```
Cannot rename defined name to "SalesTable" because a table with that name already exists.
Table renamed to "SalesTable_Alt". Now you can reuse "SalesTable" for the defined name.
```

Μετά την εκτέλεση, το παραγόμενο `RenameResult.xlsx` περιέχει:

- Ένα φύλλο εργασίας με έναν πίνακα που ονομάζεται **SalesTable_Alt** και καλύπτει το εύρος A1:C5.  
- Ένα ορισμένο όνομα σε επίπεδο βιβλίου εργασίας **SalesTable** που δείχνει στο ίδιο εύρος (ή σε οποιοδήποτε εύρος ορίσετε αργότερα).

Ανοίξτε το αρχείο στο Excel → Formulas → Name Manager για να επιβεβαιώσετε ότι και οι δύο καταχωρήσεις υπάρχουν χωρίς σύγκρουση.

## Κατανόηση συγκρούσεων ονόματος πίνακα Excel (secondary keyword)

Το Excel αντιμετωπίζει **tables** (`ListObject`) και **named ranges** (`Name`) ως μέλη ενός ενιαίου ονοματοχώρου. Όταν δημιουργείτε έναν πίνακα με όνομα *SalesTable*, ο διαχειριστής ονομάτων καταχωρεί εσωτερικά το *SalesTable* ως ορισμένο όνομα που δείχνει στο εύρος του πίνακα. Η προσπάθεια προσθήκης άλλου ορισμένου ονόματος με τον ίδιο ταυτοποιητή προκαλεί το `ArgumentException` που είδατε στο αρχικό απόσπασμα.

Σημεία-κλειδιά για να θυμάστε:

- **Scope**: Τα ονόματα πινάκων ισχύουν σε όλο το βιβλίο εργασίας· δεν μπορούν να διπλασιαστούν ακόμη και σε διαφορετικά φύλλα εργασίας.  
- **Case‑insensitivity**: `salesTable` και `SalesTable` θεωρούνται το ίδιο.  
- **Rename order matters**: Η μετονομασία του πίνακα πρώτα (ή η αφαίρεσή του) καθαρίζει τον ονοματοχώρο για το ορισμένο όνομα.

## Υλοποίηση της μετονομασίας με διαχείριση εξαιρέσεων (primary keyword)

Αν προτιμάτε να βασιστείτε στη διαχείριση εξαιρέσεων αντί για προ‑έλεγχο, τυλίξτε τη μετονομασία σε ένα μπλοκ `try/catch` όπως φαίνεται στον αρχικό κώδικα. Ωστόσο, η προληπτική ανίχνευση συγκρούσεων (όπως δείχνει το παράδειγμα) είναι πιο αποδοτική, επειδή αποφεύγει το κόστος απόδοσης της ρίψης και σύλληψης μιας εξαίρεσης.

```csharp
try
{
    definedName.Name = "SalesTable"; // May throw if conflict exists
    Console.WriteLine("Rename succeeded.");
}
catch (Exception ex)
{
    Console.WriteLine($"Rename blocked: {ex.Message}");
    // Resolve conflict here, e.g., rename the table first
}
```

**Καλύτερη πρακτική:** Χρησιμοποιήστε τη μέθοδο `IsNameConflict` πριν επιχειρήσετε τη μετονομασία. Αυτό το μοτίβο ακολουθεί την αρχή “fail‑fast” και κάνει τον κώδικά σας πιο εύκολο στη συντήρηση.

## Πλήρες εκτελέσιμο παράδειγμα (primary keyword)

Παρακάτω βρίσκεται το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε‑επικολλήσετε σε ένα νέο .NET console project. Δείχνει πώς να **how to rename excel name** με ασφάλεια, διαχειρίζεται **excel table name conflict**, και δείχνει πώς να **create excel workbook c#** από την αρχή.

```csharp
using System;
using Aspose.Cells;

namespace ExcelRenameDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create workbook and worksheet
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];

            // 2️⃣ Add a table named "SalesTable"
            ListObject salesTable = worksheet.ListObjects.Add(0, 0, 5, 3, TableStyleType.Light1);
            salesTable.Name = "SalesTable";

            // 3️⃣ Add a temporary defined name
            Name definedName = workbook.Worksheets[0].Names.Add("TempName");

            // 4️⃣ Desired rename target
            string desiredName = "SalesTable";

            // 5️⃣ Check for conflict
            if (IsNameConflict(workbook, worksheet, desiredName))
            {
                Console.WriteLine($"Conflict detected: a table named \"{desiredName}\" already exists.");

                // Resolve by renaming the table first
                salesTable.Name = $"{desiredName}_Alt";
                Console.WriteLine($"Table renamed to \"{salesTable.Name}\".");

                // Now rename the defined name
                definedName.Name = desiredName;
                Console.WriteLine($"Defined name renamed to \"{desiredName}\".");
            }
            else
            {
                definedName.Name = desiredName;
                Console.WriteLine($"Defined name renamed to \"{desiredName}\" without conflict.");
            }

            // 6️⃣ Save the workbook
            workbook.Save("RenameResult.xlsx");
            Console.WriteLine("Workbook saved as RenameResult.xlsx");
        }

        /// <summary>
        /// Determines whether the target name collides with any existing table or defined name.
        /// </summary>
        static bool IsNameConflict(Workbook wb, Worksheet ws, string name)
        {
            foreach (ListObject lo in ws.ListObjects)
                if (string.Equals(lo.Name, name, StringComparison.OrdinalIgnoreCase))
                    return true;

            foreach (Name n in wb.Worksheets[0].Names)
                if (string.Equals(n.Name, name, StringComparison.OrdinalIgnoreCase))
                    return true;

            return false;
        }
    }
}
```

### Τι κάνει ο κώδικας

1. **Creates** ένα νέο βιβλίο εργασίας Excel (`create excel workbook c#`).  
2. **Adds** έναν πίνακα με όνομα *SalesTable* (δείχνοντας την πηγή της σύγκρουσης).  
3. **Attempts** να μετονομάσει ένα ορισμένο όνομα σε *SalesTable*.  
4. **Detects** τη σύγκρουση με τη `IsNameConflict`.  
5. **Renames** πρώτα τον πίνακα, στη συνέχεια μετονομάζει με ασφάλεια το ορισμένο όνομα.

## Τι πρέπει να μάθετε στη συνέχεια;

Οι παρακάτω οδηγίες καλύπτουν στενά σχετικές θεματικές που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε επιπλέον δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Assign name to Excel table and avoid naming conflicts](/cells/english/net/excel-advanced-named-ranges/assign-name-to-excel-table-and-avoid-naming-conflicts/)
- [How to Rename Table in Excel with C# – Step‑by‑Step Guide](/cells/english/net/tables-and-lists/how-to-rename-table-in-excel-with-c-step-by-step-guide/)
- [Create Excel Workbook in C# – Add Named Range & Set Table Name](/cells/english/net/excel-advanced-named-ranges/create-excel-workbook-in-c-add-named-range-set-table-name/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}