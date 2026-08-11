---
category: general
date: 2026-08-11
description: Πώς να μετονομάσετε έναν πίνακα στο Excel με C# χρησιμοποιώντας το Aspose.Cells.
  Μάθετε πώς να δημιουργήσετε ένα βιβλίο εργασίας Excel, να προσθέσετε μια ονομαστική
  περιοχή και να αποφύγετε συγκρούσεις ονομασίας.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to rename table
- create excel workbook
- add named range
- how to add range
- rename excel table
language: el
lastmod: 2026-08-11
og_description: Πώς να μετονομάσετε έναν πίνακα στο Excel με C# χρησιμοποιώντας το
  Aspose.Cells. Αυτός ο οδηγός σας δείχνει πώς να δημιουργήσετε ένα βιβλίο εργασίας
  Excel, να προσθέσετε ονομαστική περιοχή και να μετονομάσετε με ασφάλεια έναν πίνακα
  Excel.
og_image_alt: Screenshot of C# code that renames an Excel table
og_title: Πώς να μετονομάσετε πίνακα στο Excel με C# – πλήρης οδηγός προγραμματισμού
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: How to rename table in Excel with C# using Aspose.Cells. Learn to create
    Excel workbook, add named range, and avoid rename conflicts.
  headline: How to rename table in Excel with C# – step‑by‑step guide
  type: TechArticle
- description: How to rename table in Excel with C# using Aspose.Cells. Learn to create
    Excel workbook, add named range, and avoid rename conflicts.
  name: How to rename table in Excel with C# – step‑by‑step guide
  steps:
  - name: '**Create Excel workbook** – instantiate a `Workbook` and add some sample
      data.'
    text: '**Create Excel workbook** – instantiate a `Workbook` and add some sample
      data.'
  - name: '**Add a named range** – use `Worksheets.Names.Add` to create a range called
      `MyRange`.'
    text: '**Add a named range** – use `Worksheets.Names.Add` to create a range called
      `MyRange`.'
  - name: '**Create an Excel table (ListObject)** – convert the data into a table
      so we have something to rename.'
    text: '**Create an Excel table (ListObject)** – convert the data into a table
      so we have something to rename.'
  - name: '**Rename the table** – attempt to set the table’s `Name` property to the
      same identifier as the named range.'
    text: '**Rename the table** – attempt to set the table’s `Name` property to the
      same identifier as the named range.'
  - name: '**Handle name conflicts** – catch the exception, explain why it occurs,
      and show a safe rename strategy.'
    text: '**Handle name conflicts** – catch the exception, explain why it occurs,
      and show a safe rename strategy.'
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
- Automation
title: Πώς να μετονομάσετε πίνακα στο Excel με C# – οδηγός βήμα‑προς‑βήμα
url: /el/net/tables-and-lists/how-to-rename-table-in-excel-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να μετονομάσετε πίνακα στο Excel με C# – οδηγός βήμα‑βήμα

Αν χρειάζεστε **how to rename table** σε ένα αρχείο Excel προγραμματιστικά, αυτό το tutorial σας δείχνει την ακριβή προσέγγιση χρησιμοποιώντας το Aspose.Cells for .NET. Θα δείτε πώς να **create Excel workbook**, να ορίσετε ένα **named range**, και να μετονομάσετε έναν υπάρχοντα πίνακα Excel χωρίς να προκαλέσετε σύγκρουση ονομάτων.

Η λύση λειτουργεί για οποιοδήποτε έργο .NET που στοχεύει στο .NET 6 ή νεότερο και απαιτεί μόνο το πακέτο NuGet του Aspose.Cells. Στο τέλος του οδηγού μπορείτε να μετονομάσετε έναν πίνακα Excel με ασφάλεια και να καταλάβετε γιατί μπορεί να προκύψει σύγκρουση όταν το όνομα ενός πίνακα ταιριάζει με ένα ορισμένο εύρος.

## Προαπαιτούμενα

- .NET 6 SDK ή νεότερο εγκατεστημένο  
- Visual Studio 2022 (ή οποιοδήποτε IDE C#)  
- Πακέτο Aspose.Cells for .NET (`dotnet add package Aspose.Cells`)  

Δεν απαιτούνται πρόσθετες συναρτήσεις interop του Excel επειδή το Aspose.Cells λειτουργεί πλήρως στη μνήμη.

## Επισκόπηση της λύσης

1. **Create Excel workbook** – δημιουργήστε ένα `Workbook` και προσθέστε κάποια δείγμα δεδομένων.  
2. **Add a named range** – χρησιμοποιήστε `Worksheets.Names.Add` για να δημιουργήσετε ένα εύρος με όνομα `MyRange`.  
3. **Create an Excel table (ListObject)** – μετατρέψτε τα δεδομένα σε πίνακα ώστε να έχουμε κάτι για μετονομασία.  
4. **Rename the table** – προσπαθήστε να ορίσετε την ιδιότητα `Name` του πίνακα στο ίδιο αναγνωριστικό με το named range.  
5. **Handle name conflicts** – πιάστε (catch) την εξαίρεση, εξηγήστε γιατί συμβαίνει, και δείξτε μια ασφαλή στρατηγική μετονομασίας.  

Κάθε βήμα εξηγείται λεπτομερώς παρακάτω.

## Βήμα 1: Πώς να δημιουργήσετε Excel workbook και να συμπληρώσετε δεδομένα

Η δημιουργία ενός workbook είναι η βάση για οποιαδήποτε εργασία αυτοματοποίησης Excel. Η κλάση `Workbook` αντιπροσωπεύει ολόκληρο το αρχείο στη μνήμη.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook
        Workbook workbook = new Workbook();

        // Access the first worksheet (index 0)
        Worksheet sheet = workbook.Worksheets[0];

        // Fill some sample data in cells A1:C4
        sheet.Cells["A1"].PutValue("ID");
        sheet.Cells["B1"].PutValue("Name");
        sheet.Cells["C1"].PutValue("Score");

        sheet.Cells["A2"].PutValue(1);
        sheet.Cells["B2"].PutValue("Alice");
        sheet.Cells["C2"].PutValue(85);

        sheet.Cells["A3"].PutValue(2);
        sheet.Cells["B3"].PutValue("Bob");
        sheet.Cells["C3"].PutValue(92);

        sheet.Cells["A4"].PutValue(3);
        sheet.Cells["B4"].PutValue("Carol");
        sheet.Cells["C4"].PutValue(78);
```

**Why this matters:** Το workbook πρέπει να περιέχει δεδομένα πριν μπορέσετε να δημιουργήσετε έναν πίνακα. Το Aspose.Cells αποθηκεύει δεδομένα σε μια συλλογή μηδενικής βάσης, έτσι `Worksheets[0]` πάντα αναφέρεται στο πρώτο φύλλο.

## Βήμα 2: Πώς να προσθέσετε named range στο φύλλο εργασίας

Ένα **named range** σας επιτρέπει να αναφέρεστε σε ένα συγκεκριμένο κελί ή εύρος με ένα φιλικό αναγνωριστικό. Η προσθήκη ενός εύρους είναι απλή:

```csharp
        // 2️⃣ Define a named range called "MyRange" that points to cell A1
        // The range string follows Excel notation: SheetName!$A$1
        workbook.Worksheets.Names.Add("MyRange", "Sheet1!$A$1");
```

**Why this matters:** Τα named ranges αποθηκεύονται στη συλλογή παγκόσμιων ονομάτων του workbook. Εάν ένας πίνακας αργότερα λάβει το ίδιο όνομα, το Aspose.Cells ρίχνει ένα `CellException` επειδή το Excel δεν επιτρέπει διπλότυπα ονόματα.

## Βήμα 3: Πώς να προσθέσετε Excel table (ListObject)

Ένας πίνακας παρέχει δομημένη διαχείριση δεδομένων, φιλτράρισμα και στυλ. Στο Aspose.Cells ονομάζεται **ListObject**.

```csharp
        // 3️⃣ Convert the data range A1:C4 into an Excel table
        // The range string includes the header row.
        int firstRow = 0;   // zero‑based index for row 1
        int firstCol = 0;   // column A
        int totalRows = 4;  // rows 1‑4
        int totalCols = 3;  // columns A‑C

        // Create the ListObject (table) and give it an initial name
        ListObject table = sheet.ListObjects[sheet.ListObjects.Add(firstRow, firstCol, totalRows, totalCols, true)];
        table.Name = "InitialTable";
```

**Why this matters:** Ο πίνακας υπάρχει τώρα με το όνομα `InitialTable`. Η μετονομασία του δείχνει τη διαδικασία **how to rename table**.

## Βήμα 4: Πώς να μετονομάσετε Excel table και να διαχειριστείτε συγκρούσεις

Η προσπάθεια να μετονομάσετε τον πίνακα σε `MyRange` θα συγκρουστεί με το named range που δημιουργήσαμε νωρίτερα. Ο παρακάτω κώδικας δείχνει το σωστό μοτίβο για την ανίχνευση και επίλυση της σύγκρουσης.

```csharp
        // 4️⃣ Try to rename the table to "MyRange"
        try
        {
            table.Name = "MyRange";   // This will raise an exception
            Console.WriteLine("Table renamed successfully.");
        }
        catch (Exception ex)
        {
            // 5️⃣ Handle the name conflict gracefully
            Console.WriteLine("Name conflict detected: " + ex.Message);

            // Resolve by choosing a unique name
            string safeName = GetUniqueTableName(workbook, "MyRange");
            table.Name = safeName;
            Console.WriteLine($"Table renamed to safe identifier: {safeName}");
        }

        // Save the workbook to verify the result
        workbook.Save("RenamedTable.xlsx");
    }

    /// <summary>
    /// Generates a unique table name that does not exist as a named range or another table.
    /// </summary>
    static string GetUniqueTableName(Workbook wb, string baseName)
    {
        int counter = 1;
        string candidate = baseName + "_" + counter;

        // Check against workbook names and existing table names
        while (NameExists(wb, candidate))
        {
            counter++;
            candidate = baseName + "_" + counter;
        }
        return candidate;
    }

    /// <summary>
    /// Returns true if the identifier is already used as a named range or table name.
    /// </summary>
    static bool NameExists(Workbook wb, string name)
    {
        // Check named ranges
        foreach (Name n in wb.Worksheets.Names)
        {
            if (string.Equals(n.TextToRefer, name, StringComparison.OrdinalIgnoreCase))
                return true;
        }

        // Check existing tables
        foreach (Worksheet ws in wb.Worksheets)
        {
            foreach (ListObject lo in ws.ListObjects)
            {
                if (string.Equals(lo.Name, name, StringComparison.OrdinalIgnoreCase))
                    return true;
            }
        }
        return false;
    }
}
```

### Τι κάνει ο κώδικας

| Βήμα | Δράση | Αιτία |
|------|--------|--------|
| **Δοκιμή μετονομασίας** | `table.Name = "MyRange"` | Δείχνει το σενάριο σύγκρουσης. |
| **Πιάνετε εξαίρεση** | Εκτυπώνει το μήνυμα σύγκρουσης. | Σας παρέχει άμεση ανατροφοδότηση για το πρόβλημα. |
| **Δημιουργία ασφαλούς ονόματος** | `GetUniqueTableName` προσθέτει αριθμητικό επίθημα μέχρι το όνομα να είναι ελεύθερο. | Εγγυάται ότι το νέο όνομα πίνακα **δεν** συγκρούεται με κανένα υπάρχον named range ή πίνακα. |
| **Αποθήκευση workbook** | `workbook.Save("RenamedTable.xlsx")` | Διατηρεί τις αλλαγές ώστε να μπορείτε να ανοίξετε το αρχείο στο Excel και να επαληθεύσετε το αποτέλεσμα. |

**Expected output** όταν εκτελείτε το πρόγραμμα:

```
Name conflict detected: A name with the same text already exists.
Table renamed to safe identifier: MyRange_1
```

Ανοίγοντας το `RenamedTable.xlsx` εμφανίζεται ένας πίνακας με όνομα `MyRange_1` και ένα ξεχωριστό named range `MyRange` που δείχνει στο κελί A1.

## Γιατί συμβαίνει η σύγκρουση και βέλτιστες πρακτικές για rename excel table

- Το Excel αποθηκεύει **named ranges** και **table names** στον ίδιο χώρο ονομάτων.  
- Όταν προσπαθείτε να αναθέσετε ένα όνομα πίνακα που υπάρχει ήδη ως range, το Aspose.Cells ρίχνει ένα `CellException`.  
- Η συνιστώμενη προσέγγιση είναι να **ελέγξετε πρώτα για υπάρχοντα ονόματα** (όπως φαίνεται στο `NameExists`) ή να χρησιμοποιήσετε μια σύμβαση ονομασίας που εγγυάται μοναδικότητα (π.χ., προσθέτοντας πρόθεμα `tbl_` στους πίνακες).  

Η εφαρμογή αυτού του μοτίβου αποτρέπει σφάλματα χρόνου εκτέλεσης και κάνει την αυτοματοποίηση σας ανθεκτική.

## Πρόσθετες συμβουλές για εργασία με Aspose.Cells

- **Pro tip:** Χρησιμοποιήστε `Workbook.Worksheets.Names.Remove("MyRange")` εάν θέλετε σκόπιμα να αντικαταστήσετε το range με ένα όνομα πίνακα.  
- **Watch out for case sensitivity:** Το Excel αντιμετωπίζει τα ονόματα χωρίς διάκριση πεζών‑κεφαλαίων· οι βοηθητικές μέθοδοι χρησιμοποιούν `OrdinalIgnoreCase` για να προσομοιώσουν τη συμπεριφορά του Excel.  
- **Performance:** Εάν επεξεργάζεστε πολλά φύλλα εργασίας, αποθηκεύστε στην cache τη συλλογή ονομάτων αντί να επαναλαμβάνετε την επανάληψη.

## Πλήρες παράδειγμα σε ένα μπλοκ

Παρακάτω είναι το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε‑επικολλήσετε σε ένα έργο κονσόλας. Περιλαμβάνει όλα τα βήματα από τη δημιουργία του workbook μέχρι την ασφαλή μετονομασία του πίνακα.



## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά σχετικές θεματικές που βασίζονται στις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να δημιουργήσετε Named Ranges περιορισμένα στο Workbook στο Excel χρησιμοποιώντας Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)
- [Πώς να υλοποιήσετε τύπους Named Range σε .NET χρησιμοποιώντας Aspose.Cells για αυτοματοποίηση Excel](/cells/english/net/formulas-functions/implement-named-range-formulas-net-aspose-cells/)
- [Πώς να προσθέσετε Slicers σε Excel Tables χρησιμοποιώντας Aspose.Cells για .NET: Ένας ολοκληρωμένος οδηγός](/cells/english/net/advanced-features/add-slicers-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}