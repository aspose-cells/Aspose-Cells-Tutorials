---
category: general
date: 2026-07-03
description: Γράψτε τύπο πίνακα σε C# για να δημιουργήσετε έναν πίνακα 2 στηλών, να
  υπολογίσετε κελί Excel και να αναδιπλώσετε τη λίστα σε στήλες. Ακολουθήστε αυτό
  το βήμα‑προς‑βήμα παράδειγμα χρησιμοποιώντας το Aspose.Cells.
draft: false
keywords:
- write array formula
- calculate excel cell
- wrap list into columns
- create 2‑column array
- generate excel array
language: el
og_description: Γράψτε τύπο πίνακα σε C# για να δημιουργήσετε έναν πίνακα 2 στηλών,
  να υπολογίσετε ένα κελί του Excel και να οργανώσετε τη λίστα σε στήλες. Μάθετε τη
  διαδικασία πλήρως με εκτελέσιμο κώδικα.
og_title: Γράψτε τύπο πίνακα σε C# – Οδηγός βήμα‑προς‑βήμα
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Write array formula in C# to create a 2‑column array, calculate Excel
    cell and wrap list into columns. Follow this step‑by‑step example using Aspose.Cells.
  headline: Write array formula in C# – Complete Programming Guide
  type: TechArticle
- description: Write array formula in C# to create a 2‑column array, calculate Excel
    cell and wrap list into columns. Follow this step‑by‑step example using Aspose.Cells.
  name: Write array formula in C# – Complete Programming Guide
  steps:
  - name: What if I need a dynamic range rather than a hard‑coded list?
    text: 'You can construct the list part of the formula at runtime:'
  - name: Does `WRAPCOLS` work on older Excel versions?
    text: '`WRAPCOLS` is available starting with Excel 365/2019. If you target older
      versions, you’ll need to simulate the behavior with `INDEX` and `MOD` tricks,
      but that quickly becomes messy. Using Aspose.Cells lets you keep the modern
      formula and still produce a compatible file for most users.'
  - name: Can I write the formula to a range instead of a single cell?
    text: 'Yes—assign the same formula to the top‑left cell of the range, then call
      `Calculate()` on the range object:'
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
- automation
title: Γράψτε τύπο πίνακα σε C# – Πλήρης Οδηγός Προγραμματισμού
url: /el/net/formulas-functions/write-array-formula-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Γράψτε τύπο πίνακα σε C# – Πλήρης Οδηγός Προγραμματισμού

Κάποτε χρειάστηκε να **γράψετε τύπο πίνακα** σε C# αλλά δεν ήξερες πώς να κάνεις το Excel να εμφανίσει μια ωραία μορφοποιημένη λίστα; Δεν είσαι μόνος/η. Πολλοί προγραμματιστές συναντούν εμπόδιο όταν προσπαθούν να *δημιουργήσουν αποτελέσματα τύπου πίνακα Excel* χωρίς να ανοίξουν το UI. Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από ένα σύντομο, ολοκληρωμένο παράδειγμα που **γράφει έναν τύπο πίνακα**, **υπολογίζει το κελί του Excel**, και **ομαδοποιεί τη λίστα σε στήλες** για **δημιουργία πίνακα 2‑στηλών** που μπορείτε να αποθηκεύσετε και να ελέγξετε.

Θα χρησιμοποιήσουμε τη δημοφιλή βιβλιοθήκη Aspose.Cells επειδή επιτρέπει τη διαχείριση βιβλιοθηκών εργασίας εξ ολοκλήρου μέσω κώδικα. Στο τέλος θα έχετε ένα έτοιμο κομμάτι κώδικα, μια σαφή εξήγηση κάθε γραμμής, και ιδέες για επέκταση του μοτίβου σε μεγαλύτερα σύνολα δεδομένων. Χωρίς περιττές πληροφορίες—μόνο τα πρακτικά στοιχεία που μπορείτε να αντιγράψετε‑επικολλήσετε σήμερα.

## Τι Θα Χρειαστείτε

Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε:

* .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί και σε .NET Core)  
* Μια αναφορά στη **Aspose.Cells** (μπορείτε να την κατεβάσετε από το NuGet: `Install-Package Aspose.Cells`)  
* Έναν φάκελο στον οποίο μπορείτε να διαβάζετε/γράφετε αρχεία Excel – θα τον ονομάσουμε `YOUR_DIRECTORY` στα παραδείγματα  

Αυτό είναι όλο. Χωρίς πρόσθετο Excel interop, χωρίς COM, μόνο καθαρός διαχειριζόμενος κώδικας.

![Write array formula in C# example](write-array-formula.png "Στιγμιότυπο που δείχνει τον παραγόμενο πίνακα 2‑στηλών στο Excel – write array formula in C#")

## Βήμα 1: Γράψτε τύπο πίνακα με Aspose.Cells

Το πρώτο που πρέπει να κάνουμε είναι **να γράψουμε τύπο πίνακα** σε ένα κελί. Στη σύνταξη του Excel η συνάρτηση `WRAPCOLS` παίρνει μια επίπεδη λίστα και τη μετασχηματίζει σε πίνακα. Να πώς το κάνετε προγραμματιστικά:

```csharp
// Step 1: Load the workbook (or create a new one)
var workbook = new Aspose.Cells.Workbook(); // creates a blank workbook

// Access the first worksheet – this is where we’ll work
var worksheet = workbook.Worksheets[0];

// Write array formula into A1 that wraps {1,2,3,4} into 2 columns
worksheet.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4},2)";
```

**Γιατί είναι σημαντικό:** Η ιδιότητα `Formula` αποθηκεύει το κυριολεκτικό κείμενο του τύπου Excel. Χρησιμοποιώντας το `WRAPCOLS` λέμε στο Excel να πάρει τον γραμμικό πίνακα `{1,2,3,4}` και να τον τοποθετήσει σε διάταξη 2 στηλών, δημιουργώντας ουσιαστικά **πίνακα 2‑στηλών**. Ο τύπος αυτός είναι *τύπος πίνακα*—θα παρατηρήσετε τις αγκύλες γύρω από τους αριθμούς.

## Βήμα 2: Υπολογίστε το κελί του Excel ώστε ο τύπος να αξιολογηθεί

Η εγγραφή του τύπου δεν αρκεί· πρέπει να **υπολογίσουμε το κελί του Excel** ώστε η μηχανή να τον εκτελέσει. Το Aspose.Cells δεν θα κάνει αυτόματα επανυπολογισμό εκτός αν το ζητήσετε:

```csharp
// Step 2: Force calculation of the cell containing the array formula
worksheet.Cells["A1"].Calculate();
```

**Γιατί αυτό το βήμα είναι κρίσιμο:** Χωρίς κλήση του `Calculate()`, το κελί παραμένει σε κατάσταση «εκκρεμότητας» και το βιβλίο εργασίας που αποθηκεύετε θα περιέχει τον ακατέργαστο τύπο, όχι τις υπολογισμένες τιμές. Με την ρητή επαναϋπολογισμό, διασφαλίζουμε ότι ο παραγόμενος πίνακας θα ενσωματωθεί στο αρχείο.

## Βήμα 3: Ομαδοποιήστε τη λίστα σε στήλες – δείτε το αποτέλεσμα

Σε αυτό το σημείο το φύλλο εργασίας περιέχει ένα μπλοκ 2 στηλών που ξεκινά από το `A1`. Αν ανοίξετε το αρχείο, θα δείτε:

| A | B |
|---|---|
| 1 | 2 |
| 3 | 4 |

Αυτή είναι η οπτική αναπαράσταση του **ομαδοποιήστε τη λίστα σε στήλες** χρησιμοποιώντας τη συνάρτηση `WRAPCOLS`. Αν προτιμάτε διαφορετικό αριθμό στηλών, αλλάξτε το δεύτερο όρισμα:

```csharp
worksheet.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4,5,6},3)"; // creates 3 columns
worksheet.Cells["A1"].Calculate();
```

Τώρα ο πίνακας φαίνεται έτσι:

| A | B | C |
|---|---|---|
| 1 | 2 | 3 |
| 4 | 5 | 6 |

**Συμβουλή:** Όταν δουλεύετε με μεγαλύτερα σύνολα δεδομένων, δημιουργήστε το string της λίστας δυναμικά (π.χ., με `string.Join(",", myNumbers)`) ώστε να αποφύγετε την σκληρή κωδικοποίηση τιμών.

## Βήμα 4: Αποθηκεύστε το βιβλίο εργασίας και επαληθεύστε το αποτέλεσμα

Τέλος, αποθηκεύουμε το βιβλίο εργασίας στο δίσκο ώστε να μπορείτε να το ανοίξετε στο Excel και να επιβεβαιώσετε την **δημιουργία excel array**:

```csharp
// Step 4: Save the workbook – you’ll see the calculated array in Excel
workbook.Save("YOUR_DIRECTORY/output.xlsx");
```

Ανοίξτε το `output.xlsx` και θα δείτε τον πίνακα 2 στηλών ακριβώς όπως περιγράφηκε. Αν αλλάξετε τον τύπο και επαναϋπολογίσετε, το αποθηκευμένο αρχείο ενημερώνεται αυτόματα—χωρίς ανάγκη χειροκίνητης ανανέωσης.

## Πλήρες, Εκτελέσιμο Παράδειγμα

Συνδυάζοντας όλα τα παραπάνω, ορίστε το πλήρες πρόγραμμα που μπορείτε να ενσωματώσετε σε μια εφαρμογή κονσόλας:

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Load (or create) a workbook
        var workbook = new Workbook(); // blank workbook

        // 2️⃣ Access the first worksheet
        var worksheet = workbook.Worksheets[0];

        // 3️⃣ Write the array formula that wraps a list into 2 columns
        worksheet.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4},2)";

        // 4️⃣ Calculate the cell so the formula is evaluated
        worksheet.Cells["A1"].Calculate();

        // 5️⃣ (Optional) Save the workbook to view the result
        workbook.Save("YOUR_DIRECTORY/output.xlsx");

        Console.WriteLine("Workbook saved – check output.xlsx to see the 2‑column array.");
    }
}
```

**Αναμενόμενο αποτέλεσμα:** Όταν ανοίξετε το `output.xlsx`, τα κελιά `A1:B2` περιέχουν τους αριθμούς 1‑4 διατεταγμένους σε δύο στήλες. Η κονσόλα εμφανίζει μια φιλική επιβεβαίωση.

## Περιπτώσεις Ορίων & Συχνές Ερωτήσεις

### Τι γίνεται αν χρειάζομαι δυναμικό εύρος αντί για σκληρά κωδικοποιημένη λίστα;

Μπορείτε να κατασκευάσετε το τμήμα λίστας του τύπου κατά την εκτέλεση:

```csharp
int[] values = { 10, 20, 30, 40, 50, 60 };
string list = "{" + string.Join(",", values) + "}";
worksheet.Cells["A1"].Formula = $"=WRAPCOLS({list},3)";
worksheet.Cells["A1"].Calculate();
```

Αυτό εξακολουθεί να **δημιουργεί excel array** αποτελέσματα, αλλά τώρα τα δεδομένα προέρχονται από τη λογική της εφαρμογής σας.

### Λειτουργεί το `WRAPCOLS` σε παλαιότερες εκδόσεις του Excel;

Το `WRAPCOLS` είναι διαθέσιμο από το Excel 365/2019 και μετά. Αν στοχεύετε παλαιότερες εκδόσεις, θα πρέπει να προσομοιώσετε τη λειτουργία με `INDEX` και τεχνικές `MOD`, αλλά αυτό γίνεται γρήγορα πολύπλοκο. Η χρήση του Aspose.Cells σας επιτρέπει να διατηρήσετε τον σύγχρονο τύπο και να παράγετε αρχείο συμβατό με τους περισσότερους χρήστες.

### Μπορώ να γράψω τον τύπο σε μια περιοχή αντί για ένα μόνο κελί;

Ναι—αναθέστε τον ίδιο τύπο στο αριστερό‑πάνω κελί της περιοχής, έπειτα καλέστε `Calculate()` στο αντικείμενο περιοχής:

```csharp
var range = worksheet.Cells.CreateRange("A1", 2, 2); // 2x2 block
range.Formula = "=WRAPCOLS({1,2,3,4},2)";
range.Calculate();
```

Το αποτέλεσμα είναι το ίδιο, αλλά έχετε μεγαλύτερο έλεγχο πάνω στο πού βρίσκεται ο πίνακας.

## Σκέψεις για Απόδοση

Όταν **υπολογίζετε κελί Excel** για πολλούς τύπους, το Aspose.Cells μπορεί να εκτελεί παρτίδες υπολογισμών για ταχύτητα. Αν παράγετε χιλιάδες πίνακες, καλέστε `workbook.CalculateFormula()` μία φορά μετά τον ορισμό όλων των τύπων, αντί για `Calculate()` σε κάθε κελί. Αυτό μειώνει δραστικά το κόστος επεξεργασίας.

## Επόμενα Βήματα

Τώρα που ξέρετε πώς να **γράψετε τύπο πίνακα**, **υπολογίσετε κελί Excel**, και **ομαδοποιήσετε τη λίστα σε στήλες** για **δημιουργία πίνακα 2‑στηλών**, μπορείτε να εξερευνήσετε:

* **Δημιουργία Excel array** για αναφορές πολλαπλών φύλλων  
* Εφαρμογή μορφοποίησης (περιγράμματα, μορφές αριθμών) στην προκύπτουσα περιοχή  
* Εξαγωγή του βιβλίου εργασίας σε PDF ή CSV για επεξεργασία downstream  
* Συνδυασμός με κανόνες επικύρωσης δεδομένων για διαδραστικά φύλλα εργασίας  

Κάθε μία από αυτές τις επιλογές βασίζεται στην κεντρική τεχνική που καλύψαμε, επιτρέποντάς σας να αυτοματοποιήσετε σύνθετες ροές εργασίας Excel εξ ολοκλήρου από το C#.

---

**Συνοπτικά**, αυτός ο οδηγός σας έδειξε πώς να **γράψετε τύπο πίνακα** σε C# χρησιμοποιώντας Aspose.Cells, να ενεργοποιήσετε το βήμα **υπολογισμού κελιού Excel**, και να **ομαδοποιήσετε τη λίστα σε στήλες** για **δημιουργία πίνακα 2‑στηλών** που μπορείτε να **δημιουργήσετε excel array** αρχεία. Ο κώδικας είναι πλήρως εκτελέσιμος, οι εξηγήσεις καλύπτουν το *γιατί* πίσω από κάθε γραμμή, και έχετε συμβουλές για κλιμάκωση και αντιμετώπιση ειδικών περιπτώσεων.

Δοκιμάστε το, αλλάξτε τον αριθμό στηλών, ενσωματώστε τα δικά σας δεδομένα, και αφήστε το Excel να κάνει το σκληρό έργο για εσάς. Καλό κώδικα!

## Τι Θα Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικά παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στα δικά σας έργα.

- [Master Excel Array Formulas with Aspose.Cells Java: Streamline Calculations and Formatting](/cells/english/java/formulas-functions/aspose-cells-java-array-formulas-custom-calculations/)
- [Create Excel List Objects Using Aspose.Cells .NET: A Step-by-Step Guide](/cells/english/net/tables-structured-references/create-excel-list-objects-aspose-cells-net/)
- [Import Multi Dimensional Array Excel Aspose Cells Java](/cells/german/java/import-export/import-multi-dimensional-array-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}