---
category: general
date: 2026-10-04
description: Μάθετε πώς να δημιουργήσετε ένα βιβλίο εργασίας Excel σε C# και να χρησιμοποιήσετε
  το EXPAND, να εξαναγκάσετε τον υπολογισμό των τύπων και να αποθηκεύσετε το βιβλίο
  εργασίας ως XLSX ενώ γεμίζετε μια στήλη με αριθμούς.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- how to use expand
- force formula calculation
- save workbook as xlsx
- populate column with numbers
language: el
lastmod: 2026-10-04
og_description: Δημιουργήστε βιβλίο εργασίας Excel σε C# χρησιμοποιώντας το Aspose.Cells.
  Αυτό το σεμινάριο δείχνει πώς να χρησιμοποιήσετε το EXPAND, να εξαναγκάσετε τον
  υπολογισμό τύπων και να αποθηκεύσετε το βιβλίο εργασίας ως XLSX ενώ γεμίζετε μια
  στήλη με αριθμούς.
og_image_alt: Screenshot of a C# program that creates an Excel workbook and applies
  the EXPAND function
og_title: Δημιουργία βιβλίου εργασίας Excel σε C# – πλήρης οδηγός με EXPAND και αποθήκευση
  σε XLSX
schemas:
- author: Aspose
  dateModified: '2026-10-04'
  description: Learn how to create Excel workbook in C# and use EXPAND, force formula
    calculation, and save workbook as XLSX while populating a column with numbers.
  headline: How to create Excel workbook in C# with the EXPAND function
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
- Automation
title: Πώς να δημιουργήσετε ένα βιβλίο εργασίας Excel σε C# με τη λειτουργία EXPAND
url: /el/net/excel-formulas-and-calculation-options/how-to-create-excel-workbook-in-c-with-the-expand-function/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να δημιουργήσετε βιβλίο εργασίας Excel σε C# με τη λειτουργία EXPAND

Αν χρειάζεστε να **δημιουργήσετε βιβλίο εργασίας Excel** προγραμματιστικά, αυτός ο οδηγός σας παρουσιάζει μια πλήρη, έτοιμη προς εκτέλεση λύση. Θα δείτε πώς να **συμπληρώσετε στήλη με αριθμούς**, να εφαρμόσετε τη λειτουργία **EXPAND** για να διαστέλλετε δεδομένα οριζόντια, να **αναγκάσετε τον υπολογισμό τύπων**, και τέλος να **αποθηκεύσετε το βιβλίο εργασίας ως XLSX**.  

Αυτό το σεμινάριο καλύπτει κάθε βήμα που χρειάζεστε, από την αρχικοποίηση του βιβλίου εργασίας μέχρι την επαλήθευση του αποτελέσματος. Δεν απαιτείται εξωτερική τεκμηρίωση — απλώς αντιγράψτε τον κώδικα, εκτελέστε τον, και θα έχετε ένα πλήρως λειτουργικό αρχείο Excel.

## Προαπαιτούμενα

- .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί επίσης με .NET Framework 4.6+)
- Πακέτο NuGet Aspose.Cells για .NET (`Install-Package Aspose.Cells`)
- Βασική εξοικείωση με τη σύνταξη C#
- Ένα IDE όπως το Visual Studio ή το VS Code

## Βήμα 1: Δημιουργία βιβλίου εργασίας Excel και πρόσβαση στο πρώτο φύλλο εργασίας

Η πρώτη ενέργεια είναι να **δημιουργήσετε βιβλίο εργασίας Excel** και να αποκτήσετε μια αναφορά στο προεπιλεγμένο φύλλο εργασίας του. Το Aspose.Cells προσθέτει αυτόματα ένα φύλλο εργασίας στο ευρετήριο 0, ώστε να μπορείτε να εργαστείτε αμέσως με αυτό.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();          // create Excel workbook
        Worksheet sheet = workbook.Worksheets[0];   // first (default) worksheet
```

*Γιατί είναι σημαντικό:* Η δημιουργία ενός αντικειμένου `Workbook` καταλαμβάνει τη εσωτερική δομή του αρχείου, και η ανάκτηση του `Worksheets[0]` σας παρέχει ένα συγκεκριμένο αντικείμενο `Worksheet` για να χειριστείτε γραμμές, στήλες και κελιά.

## Βήμα 2: Συμπλήρωση στήλης με αριθμούς

Στη συνέχεια, γεμίστε μια κατακόρυφη λίστα στη στήλη A. Αυτό δείχνει τη **συμπλήρωση στήλης με αριθμούς** και παρέχει το εύρος προέλευσης για τη λειτουργία EXPAND.

```csharp
        // Step 2: Fill a vertical list of values in column A
        sheet.Cells["A1"].PutValue(1);
        sheet.Cells["A2"].PutValue(2);
        sheet.Cells["A3"].PutValue(3);
```

*Συμβουλή:* Χρησιμοποιήστε `PutValue` για ακατέργαστους αριθμούς, συμβολοσειρές, ημερομηνίες ή οποιοδήποτε τύπο .NET. Η μέθοδος καθορίζει αυτόματα τον τύπο του κελιού.

## Βήμα 3: Πώς να χρησιμοποιήσετε το EXPAND – διαστέλλοντας τη λίστα οριζόντια

Το τμήμα **πώς να χρησιμοποιήσετε το expand** είναι ο πυρήνας αυτού του σεμιναρίου. Η λειτουργία `EXPAND` επεκτείνει ένα εύρος προέλευσης σε νέο σχήμα. Εδώ επεκτείνουμε το κατακόρυφο εύρος `A1:A3` σε μια μόνο γραμμή που εκτείνεται σε τρεις στήλες, ξεκινώντας από το `B1`.

```csharp
        // Step 3: Apply the EXPAND function to spill the list horizontally starting at B1
        // The formula expands the range A1:A3 into 1 row and 3 columns (B1:D1)
        sheet.Cells["B1"].Formula = "=EXPAND(A1:A3, 1, 3)";
```

*Εξήγηση:*  
- Το πρώτο όρισμα (`A1:A3`) είναι το εύρος προέλευσης.  
- Το δεύτερο όρισμα (`1`) αναγκάζει το αποτέλεσμα να έχει **1** γραμμή.  
- Το τρίτο όρισμα (`3`) αναγκάζει το αποτέλεσμα να έχει **3** στήλες.  

Όταν το βιβλίο εργασίας επαναϋπολογιστεί, τα κελιά `B1`, `C1` και `D1` θα περιέχουν αντίστοιχα `1`, `2` και `3`.

## Βήμα 4: Αναγκαστικός υπολογισμός τύπων

Το Aspose.Cells δεν αξιολογεί αυτόματα τους τύπους μετά την ορισμό τους, επομένως πρέπει να **αναγκάσετε τον υπολογισμό τύπων** πριν την αποθήκευση. Αυτό εξασφαλίζει ότι το αποτέλεσμα του EXPAND θα ενσωματωθεί στο αρχείο.

```csharp
        // Step 4: Force calculation of all formulas in the workbook
        workbook.CalculateFormula();   // triggers calculation engine
```

*Γιατί το χρειάζεστε:* Χωρίς την κλήση του `CalculateFormula()`, το αποθηκευμένο αρχείο θα περιείχε τη μη επεξεργασμένη συμβολοσειρά τύπου, και το Excel θα επανυπολογίσει μόνο όταν το αρχείο ανοιχτεί. Για αυτοματοποιημένες διαδικασίες, συνήθως θέλετε οι τιμές να γραφτούν αμέσως.

## Βήμα 5: Αποθήκευση βιβλίου εργασίας ως XLSX

Τώρα που το βιβλίο εργασίας είναι πλήρως έτοιμο, **αποθηκεύστε το βιβλίο εργασίας ως XLSX** σε μια τοποθεσία της επιλογής σας. Η επέκταση του αρχείου καθορίζει τη μορφή εξόδου· το `.xlsx` δημιουργεί ένα βιβλίο εργασίας Office Open XML.

```csharp
        // Step 5: Save the workbook to a file
        string outputPath = @"C:\Temp\ExpandFunction.xlsx";
        workbook.Save(outputPath);   // save workbook as XLSX
        System.Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

*Συμβουλή:* Αν χρειάζεστε διαφορετική μορφή (CSV, PDF κ.λπ.), απλώς αλλάξτε την επέκταση του αρχείου ή χρησιμοποιήστε `workbook.Save(outputPath, SaveFormat.Xls)` για παλαιότερες εκδόσεις του Excel.

## Πλήρες, εκτελέσιμο παράδειγμα

Συνδυάζοντας όλα τα κομμάτια παίρνετε ένα αυτόνομο πρόγραμμα που **δημιουργεί βιβλίο εργασίας Excel**, συμπληρώνει μια στήλη, χρησιμοποιεί το **EXPAND**, αναγκάζει τον υπολογισμό και **αποθηκεύει το βιβλίο εργασίας ως XLSX**.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1. Create Excel workbook
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // 2. Populate column with numbers
        sheet.Cells["A1"].PutValue(1);
        sheet.Cells["A2"].PutValue(2);
        sheet.Cells["A3"].PutValue(3);

        // 3. How to use EXPAND – spill horizontally
        sheet.Cells["B1"].Formula = "=EXPAND(A1:A3, 1, 3)";

        // 4. Force formula calculation
        workbook.CalculateFormula();

        // 5. Save workbook as XLSX
        string path = @"C:\Temp\ExpandFunction.xlsx";
        workbook.Save(path);
        System.Console.WriteLine($"Workbook saved to {path}");
    }
}
```

### Αναμενόμενο αποτέλεσμα

Αφού εκτελέσετε το πρόγραμμα, ανοίξτε το `ExpandFunction.xlsx` στο Excel. Θα πρέπει να δείτε:

| A | B | C | D |
|---|---|---|---|
| 1 | 1 | 2 | 3 |
| 2 |   |   |   |
| 3 |   |   |   |

Οι τιμές `1`, `2`, `3` στα κελιά `B1:D1` επιβεβαιώνουν ότι η λειτουργία **EXPAND** λειτούργησε και ότι το βήμα **αναγκαστικού υπολογισμού τύπων** υλοποίησε επιτυχώς τα αποτελέσματα.

## Συνηθισμένες παραλλαγές και ειδικές περιπτώσεις

| Σενάριο | Προσαρμογή |
|----------|------------|
| **Δυναμικό εύρος προέλευσης** | Χρησιμοποιήστε `=EXPAND(A1:INDEX(A:A, COUNTA(A:A)), 1, 0)` για να επεκτείνετε όσες γραμμές έχουν συμπληρωθεί. |
| **Διαφορετικές διαστάσεις εξόδου** | Αλλάξτε το δεύτερο και τρίτο όρισμα της `EXPAND` για να ελέγξετε τις γραμμές και τις στήλες. |
| **Πολλαπλά φύλλα εργασίας** | Επανάληψη μέσω `workbook.Worksheets` και εφαρμογή της ίδιας λογικής σε κάθε φύλλο. |
| **Μεγάλα σύνολα δεδομένων** | Καλέστε το `workbook.CalculateFormula()` μία φορά μετά τον ορισμό όλων των τύπων για να αποφύγετε επαναλαμβανόμενους επαναυπολογισμούς. |
| **Αποθήκευση σε ροή μνήμης** | Αντικαταστήστε το `workbook.Save(path)` με `workbook.Save(stream, SaveFormat.Xlsx)` όταν χρειάζεστε το αρχείο σε απόκριση web API. |

## Λίστα ελέγχου αντιμετώπισης προβλημάτων

- **Ο τύπος δεν επεκτείνεται:** Επαληθεύστε ότι το `CalculateFormula()` καλείται *μετά* τον ορισμό του τύπου.  
- **Αρχείο δεν βρέθηκε κατά την αποθήκευση:** Βεβαιωθείτε ότι ο προορισμός υπάρχει και ότι η διεργασία έχει δικαιώματα εγγραφής.  
- **Λανθασμένος τύπος δεδομένων:** Χρησιμοποιήστε `PutValue` για αριθμούς· για ημερομηνίες, χρησιμοποιήστε `PutValue(DateTime.Now)` ή `PutDateTime`.  
- **Ασυμφωνία έκδοσης:** Η λειτουργία EXPAND απαιτεί μηχανή υπολογισμού συμβατή με Excel 365· το Aspose.Cells 23.9+ την υποστηρίζει.

## Συμπέρασμα

Τώρα γνωρίζετε πώς να **δημιουργήσετε βιβλίο εργασίας Excel** σε C#, **συμπληρώσετε στήλη με αριθμούς**, να εφαρμόσετε τη λειτουργία **EXPAND**, να **αναγκάσετε τον υπολογισμό τύπων**, και να **αποθηκεύσετε το βιβλίο εργασίας ως XLSX**. Αυτό το ολοκληρωμένο παράδειγμα μπορεί να προσαρμοστεί για αναφορές, μετασχηματισμό δεδομένων ή οποιοδήποτε σενάριο αυτοματοποίησης που απαιτεί δυναμική έξοδο Excel.

### Επόμενα βήματα

- Εξερευνήστε άλλες λειτουργίες δυναμικών πινάκων όπως `FILTER`, `SORT` και `UNIQUE`.  
- Ενσωματώστε τη δημιουργία του βιβλίου εργασίας σε ένα ASP.NET Core API για να παρέχετε αρχεία Excel κατόπιν ζήτησης.  
- Αντικαταστήστε τους σκληρά κωδικοποιημένους αριθμούς με δεδομένα που διαβάζονται από βάση δεδομένων ή αρχείο CSV για πραγματικές αναφορές.

Μη διστάσετε να πειραματιστείτε με διαφορετικά εύρη, ονόματα φύλλων και μορφές εξόδου. Καλή προγραμματιστική!

## Τι Θα Πρέπει Να Μάθετε Στη Σειρά;

Τα παρακάτω σεμινάρια καλύπτουν στενά σχετικές θεματικές που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να Υπολογίσετε την Συνεφαπτομένη σε Excel με C# – Δημιουργία Βιβλίου Εργασίας, Χρήση EXPAND,](/cells/english/net/formulas-functions/how-to-calculate-cotangent-in-excel-with-c-create-workbook-u/)
- [Πώς να Χρησιμοποιήσετε το WRAPCOLS σε C# – Δημιουργία Βιβλίου Εργασίας Excel με Συναρτήσεις Περιτύλιξης](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-create-excel-workbook-with-wrap-fun/)
- [Πώς να Δημιουργήσετε και Αποθηκεύσετε ένα Βιβλίο Εργασίας Excel ως ODS Χρησιμοποιώντας το Aspose.Cells για .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}