---
category: general
date: 2026-02-28
description: Μάθετε πώς να προσθέσετε προσαρμοσμένη ιδιότητα σε ένα βιβλίο εργασίας
  Excel με C# και να γράψετε γρήγορα έξοδο στην κονσόλα. Περιλαμβάνει τη φόρτωση βιβλίου
  εργασίας Excel με C# και την πρόσβαση σε προσαρμοσμένες ιδιότητες με C#.
draft: false
keywords:
- how to add custom property
- load excel workbook c#
- write console output c#
- access custom properties c#
- get first worksheet c#
language: el
og_description: Πώς να προσθέσετε προσαρμοσμένη ιδιότητα στο Excel χρησιμοποιώντας
  C# με λεπτομερή εξήγηση. Φορτώστε το βιβλίο εργασίας, αποκτήστε πρόσβαση στις προσαρμοσμένες
  ιδιότητες και εμφανίστε την έξοδο στην κονσόλα.
og_title: Πώς να προσθέσετε προσαρμοσμένη ιδιότητα στο Excel με C# – Πλήρης οδηγός
tags:
- C#
- Excel
- Aspose.Cells
- CustomProperties
title: Πώς να προσθέσετε προσαρμοσμένη ιδιότητα στο Excel με C# – Οδηγός βήμα‑βήμα
url: /el/net/document-properties/how-to-add-custom-property-in-excel-with-c-step-by-step-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Προσθέσετε Προσαρμοσμένη Ιδιότητα σε Excel με C# – Οδηγός Βήμα‑βήμα

Έχετε αναρωτηθεί ποτέ **πώς να προσθέσετε προσαρμοσμένη ιδιότητα** σε ένα αρχείο Excel χρησιμοποιώντας C#; Σε αυτό το tutorial θα περάσουμε από τη φόρτωση ενός Excel workbook, την πρόσβαση σε προσαρμοσμένες ιδιότητες και την εκτύπωση του αποτελέσματος στην κονσόλα. Είναι ένα αρκετά κοινό σενάριο όταν χρειάζεται να επισημάνετε ένα φύλλο με μεταδεδομένα όπως “Department” ή “Budget” χωρίς να αλλάξετε τα ορατά δεδομένα.

Αυτό που θα πάρετε από αυτόν τον οδηγό είναι μια πλήρης, έτοιμη για αντιγραφή‑και‑επικόλληση λύση που σας δείχνει πώς να **load excel workbook c#**, να ανακτήσετε το **first worksheet c#**, να προσθέσετε και να διαβάσετε **custom properties c#**, και τέλος να **write console output c#**. Χωρίς ασαφείς αναφορές σε εξωτερικά έγγραφα—όλα όσα χρειάζεστε είναι εδώ, μαζί με μερικές επαγγελματικές συμβουλές για να αποφύγετε τα συνηθισμένα προβλήματα.

---

## Prerequisites

- **.NET 6.0** ή νεότερο (ο κώδικας λειτουργεί επίσης με .NET Framework 4.6+).  
- **Aspose.Cells for .NET** (δωρεάν δοκιμή ή αδειοδοτημένη έκδοση). Αν προτιμάτε μια ανοιχτού κώδικα εναλλακτική, το EPPlus λειτουργεί παρόμοια· απλώς αλλάξτε το namespace και τα ονόματα κλάσεων.  
- Ένα βασικό περιβάλλον ανάπτυξης C# (Visual Studio, VS Code, Rider—οποιοδήποτε).  
- Ένα αρχείο Excel με όνομα `input.xlsx` τοποθετημένο σε φάκελο που μπορείτε να αναφέρετε, π.χ., `C:\Data\input.xlsx`.

> **Pro tip:** Όταν εγκαθιστάτε το Aspose.Cells μέσω NuGet, το πακέτο προσθέτει αυτόματα την απαραίτητη οδηγία `using Aspose.Cells;`, ώστε να μην χρειάζεται να ψάχνετε χειροκίνητα για DLLs.

---

## Step 1 – Load Excel Workbook C# (Το Σημείο Εκκίνησης)

Πριν μπορέσετε να δουλέψετε με προσαρμοσμένες ιδιότητες, χρειάζεστε το αντικείμενο workbook στη μνήμη.

```csharp
using System;
using Aspose.Cells;   // Make sure the Aspose.Cells NuGet package is installed

// Define the path to your Excel file
string workbookPath = @"C:\Data\input.xlsx";

// Load the workbook – this is the classic way to load excel workbook c#
Workbook wb = new Workbook(workbookPath);
```

**Why this matters:** Η φόρτωση του workbook δημιουργεί ένα πλήρες αντικείμενο `Workbook` που σας δίνει πρόσβαση σε φύλλα, κελιά και στη κρυφή συλλογή `CustomProperties`. Η παράλειψη αυτού του βήματος ή η χρήση λανθασμένης διαδρομής θα προκαλέσει `FileNotFoundException`, γι’ αυτό ορίζουμε ρητά τη διαδρομή από την αρχή.

---

## Step 2 – Get First Worksheet C# (Where the Magic Happens)

Τα περισσότερα φύλλα εργασίας έχουν ένα προεπιλεγμένο φύλλο με το οποίο θέλετε να εργαστείτε. Το Aspose.Cells αποθηκεύει τα worksheets σε μια συλλογή μηδενικής βάσης, οπότε το πρώτο είναι το index `0`.

```csharp
// Retrieve the first worksheet – get first worksheet c# is as simple as this
Worksheet worksheet = wb.Worksheets[0];
```

**What’s the benefit?** Στοχεύοντας απευθείας το πρώτο worksheet, αποφεύγετε το βρόχο διαμέσου της συλλογής όταν χρειάζεστε μόνο ένα φύλλο. Αν το αρχείο σας έχει πολλά φύλλα και χρειάζεστε κάποιο άλλο, απλώς αλλάξτε το index ή χρησιμοποιήστε `Worksheets["SheetName"]`.

---

## Step 3 – Add Custom Property (The Core of How to Add Custom Property)

Τώρα τελικά απαντάμε στην κύρια ερώτηση: **πώς να προσθέσετε προσαρμοσμένη ιδιότητα** σε ένα worksheet.

```csharp
// Add a custom property named "Department" with value "Finance"
worksheet.CustomProperties.Add("Department", "Finance");

// Add a numeric custom property named "Budget" with value 1,250,000
worksheet.CustomProperties.Add("Budget", 1250000);
```

### Behind the scenes

- Το `CustomProperties` είναι μια συλλογή που ανήκει στο αντικείμενο `Worksheet`, όχι στο workbook.  
- Η μέθοδος `Add` δέχεται ένα κλειδί τύπου string και μια τιμή τύπου object, ώστε να μπορείτε να αποθηκεύσετε κείμενο, αριθμούς, ημερομηνίες ή ακόμη και boolean flags.  
- Το Aspose.Cells αποθηκεύει αυτόματα αυτές τις ιδιότητες στο υποκείμενο αρχείο Excel όταν το αποθηκεύετε αργότερα.

> **Watch out:** Αν προσπαθήσετε να προσθέσετε μια ιδιότητα με διπλό όνομα, το Aspose θα ρίξει `ArgumentException`. Για να ενημερώσετε μια υπάρχουσα ιδιότητα, χρησιμοποιήστε `worksheet.CustomProperties["Budget"].Value = newValue;`.

---

## Step 4 – Retrieve and Use Custom Property (Access Custom Properties C#)

Η ανάγνωση μιας ιδιότητας είναι εξίσου εύκολη με τη γραφή της. Αυτό το βήμα δείχνει **access custom properties c#** και επίσης πώς να **write console output c#**.

```csharp
// Retrieve the "Budget" value from the custom properties collection
var budget = worksheet.CustomProperties["Budget"].Value;

// Optional: Cast to the expected type if you need numeric operations
decimal budgetAmount = Convert.ToDecimal(budget);
```

**Why cast?** Η ιδιότητα `Value` επιστρέφει ένα `object`. Η μετατροπή του σε αριθμητικό τύπο σας επιτρέπει να κάνετε υπολογισμούς—π.χ., να προσθέσετε φόρο ή να συγκρίνετε προϋπολογισμούς—χωρίς επιπλέον overhead boxing/unboxing.

---

## Step 5 – Write Console Output C# (Seeing the Result)

Τέλος, εμφανίζουμε τον ανακτημένο προϋπολογισμό στην κονσόλα. Αυτό ικανοποιεί την απαίτηση **write console output c#**.

```csharp
// Display the budget amount in the console
Console.WriteLine($"Budget: {budgetAmount:C0}");
```

Ο μορφοποιητής `:C0` εκτυπώνει τον αριθμό ως νόμισμα χωρίς δεκαδικά ψηφία, π.χ., `Budget: $1,250,000`. Μπορείτε να προσαρμόσετε το format string ώστε να ταιριάζει στην τοπική σας ρύθμιση.

---

## Step 6 – Save the Workbook (Persisting the Changes)

Αν θέλετε οι προσαρμοσμένες ιδιότητες να παραμείνουν μετά το τρέχον session, πρέπει να αποθηκεύσετε το workbook.

```csharp
// Save the workbook to a new file so you don't overwrite the original
string outputPath = @"C:\Data\output_with_properties.xlsx";
wb.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

**Note:** Παρόλο που οι προσαρμοσμένες ιδιότητες συνδέονται με το worksheet, αποθηκεύονται μέσα στο πακέτο `.xlsx`, οπότε το μέγεθος του αρχείου αυξάνεται μόνο ελαφρώς.

---

## Full Working Example (Copy‑Paste Ready)

Παρακάτω είναι το πλήρες πρόγραμμα που ενώνει όλα τα βήματα. Επικολλήστε το σε ένα νέο console project και πατήστε **F5**.

```csharp
using System;
using Aspose.Cells;

namespace ExcelCustomPropertiesDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the workbook – how to add custom property starts here
            string workbookPath = @"C:\Data\input.xlsx";
            Workbook wb = new Workbook(workbookPath);

            // 2️⃣ Get the first worksheet – get first worksheet c#
            Worksheet worksheet = wb.Worksheets[0];

            // 3️⃣ Add custom properties – this is the core of how to add custom property
            worksheet.CustomProperties.Add("Department", "Finance");
            worksheet.CustomProperties.Add("Budget", 1250000);

            // 4️⃣ Retrieve the budget – access custom properties c#
            var budget = worksheet.CustomProperties["Budget"].Value;
            decimal budgetAmount = Convert.ToDecimal(budget);

            // 5️⃣ Write console output – write console output c#
            Console.WriteLine($"Budget: {budgetAmount:C0}");

            // 6️⃣ Save the workbook so the properties persist
            string outputPath = @"C:\Data\output_with_properties.xlsx";
            wb.Save(outputPath);
            Console.WriteLine($"Workbook saved to {outputPath}");

            // Keep console window open
            Console.WriteLine("Press any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**Expected console output**

```
Budget: $1,250,000
Workbook saved to C:\Data\output_with_properties.xlsx
Press any key to exit...
```

Τρέξτε το πρόγραμμα, ανοίξτε το `output_with_properties.xlsx` στο Excel, μετά πηγαίνετε στο **File → Info → Properties → Advanced Properties → Custom**. Θα δείτε “Department” = “Finance” και “Budget” = 1250000 εκεί.

---

## Common Questions & Edge Cases

### What if the workbook is password‑protected?

Το Aspose.Cells σας επιτρέπει να ανοίξετε ένα προστατευμένο αρχείο περνώντας ένα αντικείμενο `LoadOptions` με τον κωδικό:

```csharp
var loadOptions = new LoadOptions(LoadFormat.Xlsx) { Password = "mySecret" };
Workbook wb = new Workbook(workbookPath, loadOptions);
```

### Can I add custom properties to the workbook itself instead of a single sheet?

Ναι—χρησιμοποιήστε `wb.CustomProperties` αντί για `worksheet.CustomProperties`. Το API είναι το ίδιο, αλλά η εμβέλεια αλλάζει από ανά φύλλο σε ολόκληρο το αρχείο.

### Does this work with .xls (Excel 97‑2003) files?

Απολύτως. Το Aspose.Cells αφαιρεί την διαφορά μορφής, οπότε ο ίδιος κώδικας λειτουργεί με `.xls`, `.xlsx`, `.xlsm` κ.λπ. Απλώς βεβαιωθείτε ότι η επέκταση του αρχείου ταιριάζει με την πραγματική μορφή.

### How do I delete a custom property?

```csharp
worksheet.CustomProperties.Remove("Department");
```

Η αφαίρεση μιας ιδιότητας είναι ασφαλής· αν το κλειδί δεν υπάρχει, δεν συμβαίνει τίποτα.

---

## Pro Tips & Pitfalls

- **Αποφύγετε την σκληρή κωδικοποίηση διαδρομών** σε κώδικα παραγωγής. Χρησιμοποιήστε `Path.Combine` και αρχεία ρυθμίσεων για μεγαλύτερη ευελιξία.  
- **Κλείστε το workbook** αν επεξεργάζεστε πολλά αρχεία σε βρόχο. Τοποθετήστε το σε `using` block ή καλέστε `wb.Dispose()` χειροκίνητα.  
- **Προσοχή στις πολιτισμικές μορφές αριθμών** όταν μετατρέπετε την τιμή `object`. Το `Convert.ToDecimal` σέβεται την τρέχουσα κουλτούρα του νήματος, οπότε ορίστε `CultureInfo.InvariantCulture` αν χρειάζεστε σταθερή ανάλυση.  
- **Προσθήκη ιδιοτήτων μαζικά**: Αν έχετε δεκάδες μεταδεδομένα, σκεφτείτε να κάνετε βρόχο πάνω από ένα dictionary για να κρατήσετε τον κώδικα DRY.

---

## Conclusion

Μόλις καλύψαμε **πώς να προσθέσετε προσαρμοσμένη ιδιότητα** σε ένα worksheet Excel χρησιμοποιώντας C#. Από τη φόρτωση του workbook, την απόκτηση του πρώτου worksheet, την προσθήκη και ανάγνωση προσαρμοσμένων ιδιοτήτων, μέχρι την εκτύπωση του αποτελέσματος στην κονσόλα και την αποθήκευση του αρχείου—έχετε τώρα μια πλήρη, έτοιμη για αντιγραφή λύση.  

Στη συνέχεια, μπορείτε να εξερευνήσετε **access custom properties c#** σε επίπεδο workbook, ή να πειραματιστείτε με πιο σύνθετους τύπους δεδομένων όπως ημερομηνίες και boolean. Αν σας ενδιαφέρει η αυτοματοποίηση δημιουργίας αναφορών, ρίξτε μια ματιά στον οδηγό μας για **write console output c#** για καταγραφή μεγάλων συνόλων δεδομένων, ή βυθιστείτε στη σειρά **load excel workbook c#** για προχωρημένη διαχείριση φύλλων.

Αλλάξτε ελεύθερα τα ονόματα των ιδιοτήτων, προσθέστε τα δικά σας μεταδεδομένα, και ενσωματώστε αυτό το μοτίβο σε μεγαλύτερους pipelines επεξεργασίας δεδομένων. Καλή προγραμματιστική δουλειά, και εύχομαι τα spreadsheets σας να παραμείνουν πλούσια σε σχολιασμό!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}