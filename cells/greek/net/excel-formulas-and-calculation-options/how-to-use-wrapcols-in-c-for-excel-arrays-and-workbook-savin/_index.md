---
category: general
date: 2026-10-01
description: Μάθετε πώς να χρησιμοποιείτε το WRAPCOLS, να εξαναγκάσετε τον υπολογισμό
  τύπων, να γράψετε αρχείο Excel με C# και να αποθηκεύσετε το βιβλίο εργασίας σε αρχείο
  με το Aspose.Cells σε λίγα εύκολα βήματα.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- force formula calculation
- write excel file c#
- save workbook to file
- how to add formula excel
language: el
lastmod: 2026-10-01
og_description: Πώς να χρησιμοποιήσετε το WRAPCOLS σε C# για να προσθέσετε έναν τύπο,
  να εξαναγκάσετε τον υπολογισμό του τύπου, να γράψετε αρχείο Excel σε C# και να αποθηκεύσετε
  το βιβλίο εργασίας σε αρχείο με το Aspose.Cells.
og_image_alt: Screenshot showing how to use WRAPCOLS formula in an Excel worksheet
  with Aspose.Cells
og_title: Πώς να χρησιμοποιήσετε το WRAPCOLS σε C# – προσθήκη τύπων, εξαναγκασμός
  υπολογισμού και αποθήκευση του Excel
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to use WRAPCOLS, force formula calculation, write Excel file
    C# and save workbook to file with Aspose.Cells in a few easy steps.
  headline: How to use WRAPCOLS in C# for Excel arrays and workbook saving
  type: TechArticle
- description: Learn how to use WRAPCOLS, force formula calculation, write Excel file
    C# and save workbook to file with Aspose.Cells in a few easy steps.
  name: How to use WRAPCOLS in C# for Excel arrays and workbook saving
  steps:
  - name: '**Target the cell** – use `Cells["B2"]`, `Cells[1, 1]`, or a range name.'
    text: '**Target the cell** – use `Cells["B2"]`, `Cells[1, 1]`, or a range name.'
  - name: '**Assign the formula string** – remember to start with `=` and use US‑style
      separators (comma for arguments).'
    text: '**Assign the formula string** – remember to start with `=` and use US‑style
      separators (comma for arguments).'
  - name: '**Trigger calculation** if you need the result immediately.'
    text: '**Trigger calculation** if you need the result immediately.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Πώς να χρησιμοποιήσετε το WRAPCOLS σε C# για πίνακες Excel και αποθήκευση βιβλίου
  εργασίας
url: /el/net/excel-formulas-and-calculation-options/how-to-use-wrapcols-in-c-for-excel-arrays-and-workbook-savin/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να χρησιμοποιήσετε το WRAPCOLS σε C# – προσθήκη τύπων, εξαναγκασμός υπολογισμού και αποθήκευση Excel

Αν χρειάζεστε **how to use WRAPCOLS** σε ένα έργο C#, αυτός ο οδηγός σας δείχνει ακριβώς αυτό και γιατί είναι σημαντικό. Θα μάθετε επίσης πώς να **force formula calculation**, **write Excel file C#**, και **save workbook to file** χρησιμοποιώντας τη βιβλιοθήκη Aspose.Cells.

Η εργασία με το Excel προγραμματιστικά συχνά σημαίνει εισαγωγή τύπων, διασφάλιση ότι αξιολογούνται, και τελικά τη διατήρηση του αποτελέσματος. Αυτό το tutorial περνάει από κάθε ένα από αυτά τα βήματα, ώστε να μπορείτε να δημιουργήσετε αποτελέσματα πίνακα όπως `=WRAPCOLS({1,2,3,4},2)` χωρίς να αφήσετε το IDE.

## Τι θα πετύχετε

* Εισάγετε τη συνάρτηση `WRAPCOLS` σε ένα κελί (απαντώντας το **how to add formula excel**).
* Ενεργοποιήστε τον υπολογισμό ώστε το αποτέλεσμα του πίνακα να γίνει πραγματικό εύρος κελιών.
* Εξάγετε το βιβλίο εργασίας σε ένα αρχείο `.xlsx` στο δίσκο (**write Excel file C#** και **save workbook to file**).

### Προαπαιτούμενα

* .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί επίσης με .NET Framework 4.6+).
* Ένα έγκυρο άδεια για **Aspose.Cells for .NET** – η δωρεάν αξιολόγηση λειτουργεί για δοκιμές.
* Visual Studio 2022 ή οποιονδήποτε επεξεργαστή συμβατό με C#.

---

## Πώς να χρησιμοποιήσετε το WRAPCOLS με το Aspose.Cells

`WRAPCOLS` δημιουργεί έναν δισδιάστατο πίνακα από μια μονοδιάστατη λίστα. Στο Aspose.Cells το αντιμετωπίζετε όπως οποιονδήποτε άλλο τύπο Excel — το αναθέτετε στην ιδιότητα `Formula` ενός κελιού.

```csharp
using Aspose.Cells;

class WrapColsExample
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();               // creates an empty workbook
        Worksheet sheet = workbook.Worksheets[0];        // first (default) sheet

        // Step 2: Insert the WRAPCOLS formula into cell A1
        // The formula builds a 2‑column array from {1,2,3,4}
        sheet.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4},2)";

        // Step 3: Force calculation so the array result is materialized
        workbook.Calculate();

        // Step 4: Save the workbook to inspect the result
        workbook.Save("output.xlsx");
    }
}
```

**Γιατί αυτό λειτουργεί:**  
*Η ανάθεση του τύπου* αποθηκεύει την κειμενική έκφραση στο κελί. Το βιβλίο εργασίας **δεν** αξιολογεί αυτόματα τους τύπους όταν καλείτε `Save`; πρέπει να καλέσετε `Calculate()` ή να ενεργοποιήσετε τον αυτόματο υπολογισμό. Αυτό είναι ο πυρήνας του **force formula calculation**.

---

## Εξαναγκασμός υπολογισμού τύπου στο βιβλίο εργασίας

Το Aspose.Cells σέβεται τις `CalculationOptions` του βιβλίου εργασίας. Αν παραλείψετε την ρητή κλήση `Calculate()`, το αποθηκευμένο αρχείο θα περιέχει ακόμη τον τύπο, και το Excel θα τον επανυπολογίσει μόνο όταν ανοίξει το αρχείο. Για να εγγυηθείτε ότι ο πίνακας έχει ήδη επεκταθεί (π.χ., για επεξεργασία downstream), εξαναγκάζετε τον υπολογισμό εσείς.

```csharp
// Force full calculation, including array formulas
workbook.Calculate(FormulaCalculationMode.Full);
```

*Συμβουλή:* Αν εργάζεστε με μεγάλα βιβλία εργασίας, χρησιμοποιήστε `FormulaCalculationMode.Manual` και καλέστε `Calculate()` μόνο στα φύλλα που χρειάζεστε. Αυτό μειώνει την κατανάλωση μνήμης.

---

## Γράψτε αρχείο Excel σε C# και αποθηκεύστε το βιβλίο εργασίας σε αρχείο

Η αποθήκευση του βιβλίου εργασίας είναι απλή, αλλά το βήμα **save workbook to file** μπορεί να περιλαμβάνει επιπλέον παραμέτρους:

| Σενάριο                              | Συνιστώμενη μέθοδος                              |
|--------------------------------------|-------------------------------------------------|
| Προεπιλεγμένη θέση (ίδιο φάκελο)      | `workbook.Save("output.xlsx");`                 |
| Συγκεκριμένος φάκελος, διασφάλιση ύπαρξης | `Directory.CreateDirectory(path); workbook.Save(Path.Combine(path, "output.xlsx"));` |
| Έξοδος ροής (π.χ., HTTP response)   | `using var ms = new MemoryStream(); workbook.Save(ms, SaveFormat.Xlsx);` |

```csharp
// Example: saving to a custom directory
string outputDir = Path.Combine(Environment.GetFolderPath(Environment.SpecialFolder.Desktop), "AsposeDemo");
Directory.CreateDirectory(outputDir);
string filePath = Path.Combine(outputDir, "wrapcols_result.xlsx");
workbook.Save(filePath);
Console.WriteLine($"Workbook saved to {filePath}");
```

**Γιατί πρέπει να καθορίσετε τη διαδρομή** – Η σκληρή κωδικοποίηση του `"output.xlsx"` λειτουργεί μόνο όταν η διαδικασία έχει δικαίωμα εγγραφής στον τρέχοντα φάκελο. Η χρήση απόλυτης διαδρομής αποφεύγει σφάλματα δικαιωμάτων και κάνει το tutorial επαναλήψιμο σε οποιονδήποτε υπολογιστή.

---

## Πώς να προσθέσετε τύπο σε κελιά Excel προγραμματιστικά

Πέρα από το `WRAPCOLS`, το ίδιο μοτίβο ισχύει για οποιονδήποτε τύπο Excel:

1. **Στοχεύστε το κελί** – χρησιμοποιήστε `Cells["B2"]`, `Cells[1, 1]`, ή ένα όνομα περιοχής.
2. **Αναθέστε τη συμβολοσειρά τύπου** – θυμηθείτε να ξεκινάτε με `=` και να χρησιμοποιείτε διαχωριστές τύπου US (κόμμα για τα ορίσματα).
3. **Ενεργοποιήστε τον υπολογισμό** εάν χρειάζεστε το αποτέλεσμα άμεσα.

```csharp
// Adding a SUM formula to C1 that sums A1:B1
sheet.Cells["C1"].Formula = "=SUM(A1:B1)";
workbook.Calculate(); // ensures C1 now contains the computed sum
```

*Κοινό λάθος:* Ξεχάτε να διαφύγετε τα διπλά εισαγωγικά μέσα σε μια συμβολοσειρά τύπου. Χρησιμοποιήστε `\"` στο C# ή το κυριολεκτικό string `@"..."`.

```csharp
// Correct way to embed a text constant in a formula
sheet.Cells["D1"].Formula = @"=IF(A1>0,""Positive"",""Zero or Negative"")";
```

---

## Περιπτώσεις άκρων και συμβουλές βέλτιστων πρακτικών

| Κατάσταση                              | Συνιστώμενη αντιμετώπιση |
|----------------------------------------|---------------------------|
| **Μεγάλοι τύποι πίνακα** (π.χ., 10 000 στοιχεία) | Χρησιμοποιήστε `worksheet.Cells.SetArrayFormula` για άμεση εγγραφή του πίνακα· αποφύγετε το `WRAPCOLS` για τεράστιες συλλογές δεδομένων. |
| **Απενεργοποιημένη αξιολόγηση τύπου** (σε ορισμένα περιβάλλοντα) | Ορίστε `workbook.Settings.CalcMode = CalculationMode.Manual;` και καλέστε `workbook.Calculate();` ρητά. |
| **Αποθήκευση ως CSV** | Οι τύποι χάνονται· καλέστε `workbook.Save("file.csv", SaveFormat.Csv);` μετά τον υπολογισμό εάν χρειάζεστε τις τιμές. |
| **Εκτέλεση ασφαλής για νήματα** | Μην μοιράζεστε ένα μόνο αντικείμενο `Workbook` μεταξύ νημάτων· δημιουργήστε νέο βιβλίο εργασίας ανά αίτηση. |

---

## Πλήρες εκτελέσιμο παράδειγμα

Παρακάτω είναι το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε‑επικολλήσετε σε μια εφαρμογή κονσόλας. Περιλαμβάνει όλα τα βήματα—**how to use WRAPCOLS**, **force formula calculation**, **write Excel file C#**, και **save workbook to file**—σε μια ενιαία ροή.

```csharp
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // 2️⃣ Add WRAPCOLS formula (answers how to add formula excel)
        sheet.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4},2)";

        // 3️⃣ Force calculation so the array expands to A1:B2
        workbook.Calculate(FormulaCalculationMode.Full);

        // 4️⃣ Save the file (demonstrates write Excel file C# and save workbook to file)
        string outDir = Path.Combine(Environment.GetFolderPath(Environment.SpecialFolder.Desktop), "AsposeDemo");
        Directory.CreateDirectory(outDir);
        string outPath = Path.Combine(outDir, "wrapcols_demo.xlsx");
        workbook.Save(outPath);
        Console.WriteLine($"Workbook with WRAPCOLS saved to: {outPath}");
    }
}
```

**Αναμενόμενη έξοδος στο Excel**

| A | B |
|---|---|
| 1 | 3 |
| 2 | 4 |

Η συνάρτηση `WRAPCOLS` πήρε τη επίπεδη λίστα `{1,2,3,4}` και την περιέβαλε σε δύο στήλες, ακριβώς όπως ορίζει ο τύπος.

---

## Συμπέρασμα

Τώρα γνωρίζετε **how to use WRAPCOLS** σε C#, πώς να **force formula calculation**, πώς να **write Excel file C#**, και τον σωστό τρόπο για **save workbook to file** με το Aspose.Cells. Ακολουθώντας τα παραπάνω βήματα, μπορείτε να ενσωματώσετε οποιονδήποτε τύπο Excel, να λάβετε άμεσα αποτελέσματα και να διατηρήσετε το βιβλίο εργασίας για επεξεργασία downstream ή λήψη από τον χρήστη.

### Τι ακολουθεί;

* Εξερευνήστε άλλες συναρτήσεις πίνακα όπως `WRAPROWS` ή `SEQUENCE`.
* Συνδυάστε το `WRAPCOLS` με δυναμικές περιοχές χρησιμοποιώντας `OFFSET` ή `INDEX`.
* Μεταβείτε στη δωρεάν βιβλιοθήκη **ClosedXML** εάν χρειάζεστε μια ανοιχτού κώδικα εναλλακτική (το API διαφέρει αλλά οι έννοιες του ορισμού τύπου και της κλήσης `Calculate()` παραμένουν οι ίδιες).

Μη διστάσετε να πειραματιστείτε με μεγαλύτερα σύνολα δεδομένων, διαφορετικές ρυθμίσεις βιβλίου εργασίας ή εξαγωγή σε PDF/CSV. Εάν αντιμετωπίσετε προβλήματα, ελέγξτε ξανά ότι κάλεσατε `workbook.Calculate()` πριν την αποθήκευση — αυτό είναι το κλειδί για αξιόπιστο **force formula calculation**.

Καλό κώδικα!

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά σχετικό θέματα που βασίζονται στις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Δημιουργία νέου βιβλίου εργασίας σε C# – Προσθήκη τύπου και αποθήκευση αρχείου Excel](/cells/english/net/excel-workbook/create-new-workbook-in-c-add-formula-and-save-excel-file/)
- [Πώς να υπολογίσετε το συνημίτονο σε Excel με C# – Δημιουργία βιβλίου εργασίας, χρήση EXPAND,](/cells/english/net/formulas-functions/how-to-calculate-cotangent-in-excel-with-c-create-workbook-u/)
- [Πώς να αποθηκεύσετε συγκεκριμένες σελίδες αρχείου Excel ως PDF χρησιμοποιώντας το Aspose.Cells για .NET](/cells/english/net/workbook-operations/save-specific-excel-pages-pdf-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}