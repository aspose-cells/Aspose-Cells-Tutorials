---
category: general
date: 2026-05-23
description: Πώς να μετονομάσετε φύλλο εργασίας σε C# χρησιμοποιώντας το Aspose.Cells
  – μάθετε να δημιουργείτε βιβλίο εργασίας Excel, να ορίζετε το όνομα του φύλλου εργασίας
  και να δημιουργείτε γρήγορα φύλλο αναφοράς.
draft: false
keywords:
- how to rename worksheet
- create excel workbook
- set worksheet name
- change worksheet name
- create report worksheet
language: el
og_description: Πώς να μετονομάσετε ένα φύλλο εργασίας σε C# με το Aspose.Cells. Ακολουθήστε
  αυτόν τον βήμα‑βήμα οδηγό για να δημιουργήσετε βιβλίο εργασίας Excel, να ορίσετε
  το όνομα του φύλλου εργασίας και να δημιουργήσετε ένα φύλλο αναφοράς.
og_title: Πώς να Μετονομάσετε Φύλλο Εργασίας σε C# – Πλήρης Οδηγός
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: How to rename worksheet in C# using Aspose.Cells – learn to create
    Excel workbook, set worksheet name and create report worksheet quickly.
  headline: How to Rename Worksheet in C# – Complete Guide
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel
- Worksheet
title: Πώς να μετονομάσετε φύλλο εργασίας σε C# – Πλήρης οδηγός
url: /el/net/worksheet-operations/how-to-rename-worksheet-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Μετονομάσετε Worksheet σε C# – Πλήρης Οδηγός

Έχετε αναρωτηθεί ποτέ **πώς να μετονομάσετε worksheet** προγραμματιστικά χωρίς να ανοίξετε το Excel; Δεν είστε ο μόνος. Πολλοί προγραμματιστές χρειάζονται να δημιουργούν αναφορές άμεσα, και το πρώτο που ρωτούν είναι πώς να μετονομάσουν worksheet σε κάτι με νόημα όπως “Report”. Σε αυτόν τον οδηγό θα περάσουμε από ένα πλήρες, εκτελέσιμο παράδειγμα που σας δείχνει πώς να μετονομάσετε worksheet, συν λίγες επιπλέον τεχνικές όπως η δημιουργία Excel workbook, ο καθορισμός του ονόματος του worksheet, και ακόμη η δημιουργία ενός report worksheet που μπορεί να επαναχρησιμοποιηθεί αργότερα.

Θα χρησιμοποιήσουμε το Aspose.Cells for .NET επειδή σας επιτρέπει να χειρίζεστε αρχεία Excel χωρίς το Office interop. Στο τέλος αυτού του tutorial θα μπορείτε να:

* **Create Excel workbook** από την αρχή.  
* **Set worksheet name** (ή **change worksheet name**) με ασφάλεια.  
* Δημιουργήστε ένα πρότυπο **create report worksheet** που μπορείτε να ενσωματώσετε σε οποιοδήποτε pipeline αναφορών.

Χωρίς εξωτερικά εργαλεία, χωρίς μαγεία COM—απλώς καθαρός κώδικας C# που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο .NET.

## Προαπαιτούμενα

* .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί επίσης σε .NET Framework 4.7+).  
* Πακέτο NuGet Aspose.Cells for .NET – εγκαταστήστε το με `dotnet add package Aspose.Cells`.  
* Ένα απλό IDE όπως το Visual Studio 2022 ή το VS Code.  

Αυτό είναι όλο. Αν έχετε ήδη ένα έργο, απλώς προσθέστε το πακέτο και είστε έτοιμοι.

---

## Πώς να Μετονομάσετε Worksheet – Βήμα 1: Δημιουργία Excel Workbook

Πριν μπορέσετε να μετονομάσετε οτιδήποτε, χρειάζεστε ένα workbook για να δουλέψετε. Σκεφτείτε το workbook ως το δοχείο που κρατά όλα τα φύλλα σας. Η δημιουργία ενός είναι τόσο απλή όσο η κλήση του κατασκευαστή `Workbook`.

```csharp
using Aspose.Cells;

namespace WorksheetDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new Excel workbook
            Workbook workbook = new Workbook();   // <-- this creates an empty .xlsx file in memory
            // (Optional) you can also load an existing file:
            // Workbook workbook = new Workbook("template.xlsx");
```

**Γιατί είναι σημαντικό:**  
Η δημιουργία ενός νέου workbook σας δίνει ένα καθαρό φύλλο, που είναι τέλειο όταν θέλετε να **create report worksheet** από την αρχή. Αν φορτώσετε ένα πρότυπο, η ίδια λογική μετονομασίας ισχύει—μόνο η πηγή αλλάζει.

---

## Βήμα 2: Ορισμός Ονόματος Worksheet (Μετονομασία του Πρώτου Φύλλου)

Από προεπιλογή, ένα νέο workbook περιέχει ένα μόνο φύλλο με όνομα “Sheet1”. Για να απαντήσετε στην κύρια ερώτηση—**πώς να μετονομάσετε worksheet**—απλώς εκχωρείτε μια νέα συμβολοσειρά στην ιδιότητα `Name` του αντικειμένου `Worksheet`.

```csharp
            // Step 2: Access the first worksheet (index 0) and rename it
            Worksheet masterSheet = workbook.Worksheets[0];
            masterSheet.Name = "Report";   // <-- this is the new name
```

**Τι συμβαίνει στο παρασκήνιο;**  
`Worksheets[0]` παίρνει το πρώτο φύλλο, και η μέθοδος `Name` ενημερώνει το εσωτερικό XML που αντιπροσωπεύει την καρτέλα του φύλλου. Το Aspose.Cells φροντίζει όλες τις λεπτομέρειες χαμηλού επιπέδου, ώστε να μην χρειάζεται να ανησυχείτε για τη διαφθορά του workbook.

> **Pro tip:** Αν χρειάζεται να **change worksheet name** βάσει εισόδου χρήστη, πάντα επικυρώστε πρώτα τη συμβολοσειρά—το Excel δεν επιτρέπει χαρακτήρες όπως `:` `\` `/` `?` `*` `[` `]`.

---

## Βήμα 3: Διαμόρφωση SmartMarker Processor (Προαιρετικό αλλά Ισχυρό)

Αν δημιουργείτε ένα **create report worksheet** που θα γεμίσει αργότερα με δεδομένα, το SmartMarker είναι μια χρήσιμη λειτουργία. Σας επιτρέπει να ορίσετε placeholders στο φύλλο και στη συνέχεια να τα γεμίσετε με μια πηγή δεδομένων—όλα χωρίς να γράψετε βρόχο.

```csharp
            // Step 3: Initialize SmartMarkerProcessor for advanced templating
            SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);

            // Optional: Allow duplicate detail sheet name if you plan to generate multiple reports
            processor.Options.DetailSheetNewName = "Report"; // ensures the detail sheet also gets the name "Report"
```

**Γιατί να χρησιμοποιήσετε SmartMarker;**  
Όταν έχετε μια αναφορά master‑detail, ο επεξεργαστής μπορεί να κλωνοποιήσει το master sheet, να μετονομάσει το κλώνο, και να εισάγει γραμμές αυτόματα. Αυτό σας εξοικονομεί το χειροκίνητο αντίγραφο στυλ και τύπων.

---

## Βήμα 4: Αποθήκευση του Workbook (Δείτε το Αποτέλεσμα)

Τώρα που το worksheet έχει μετονομαστεί, ας γράψουμε το αρχείο στο δίσκο ώστε να το ανοίξετε στο Excel και να επαληθεύσετε την αλλαγή.

```csharp
            // Step 4: Save the workbook to a file
            string outputPath = "RenamedWorksheetDemo.xlsx";
            workbook.Save(outputPath, SaveFormat.Xlsx);
            System.Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

**Αναμενόμενο αποτέλεσμα:**  
Όταν ανοίξετε το *RenamedWorksheetDemo.xlsx*, η καρτέλα στο κάτω μέρος θα εμφανίζει **Report** αντί για “Sheet1”. Αυτό είναι η οπτική απόδειξη ότι έχετε κατακτήσει το **πώς να μετονομάσετε worksheet**.

---

## Συνηθισμένα Παράπλευρα Προβλήματα & Ακραίες Περιπτώσεις

| Situation | What to Watch Out For | How to Handle |
|-----------|----------------------|---------------|
| **Duplicate sheet name** | Το Excel ρίχνει εξαίρεση αν προσπαθήσετε να ορίσετε όνομα που υπάρχει ήδη. | Χρησιμοποιήστε `processor.Options.DetailSheetNewName` ή ελέγξτε `workbook.Worksheets.Exists("Report")` πριν τη μετονομασία. |
| **Invalid characters** | Οι χαρακτήρες `:*?/\[]` είναι παράνομοι σε ονόματα φύλλων. | Αφαιρέστε ή αντικαταστήστε τα με underscores πριν εκχωρήσετε `masterSheet.Name`. |
| **Very long names** | Το Excel περιορίζει τα ονόματα φύλλων στα 31 χαρακτήρες. | Κόψτε τη συμβολοσειρά: `masterSheet.Name = name.Length > 31 ? name.Substring(0,31) : name;`. |
| **Localization** | Ορισμένες τοπικές ρυθμίσεις χρησιμοποιούν διαφορετικά προεπιλεγμένα ονόματα φύλλων (π.χ., “Feuille1”). | Η προσέγγιση με βάση το δείκτη (`Worksheets[0]`) λειτουργεί ανεξάρτητα από το προεπιλεγμένο όνομα. |

---

## Bonus: Δημιουργία Report Worksheet με Πρότυπο

Συχνά θα ξεκινήσετε από ένα πρότυπο που ήδη περιέχει κεφαλίδες, τύπους και μορφοποίηση. Εδώ είναι ένα γρήγορο πρότυπο για **create report worksheet** από πρότυπο ενώ εξακολουθείτε να μπορείτε να **set worksheet name** δυναμικά.

```csharp
// Load a template file that has a sheet called "Template"
Workbook templateWb = new Workbook("ReportTemplate.xlsx");

// Clone the template sheet
Worksheet templateSheet = templateWb.Worksheets["Template"];
int newIndex = workbook.Worksheets.AddCopy(templateSheet);

// Rename the cloned sheet
Worksheet reportSheet = workbook.Worksheets[newIndex];
reportSheet.Name = "MonthlyReport";   // <-- set worksheet name for the new report
```

**Γιατί κλωνοποίηση;**  
Η κλωνοποίηση διατηρεί όλη τη μορφοποίηση, την επικύρωση δεδομένων και τους τύπους. Χρειάζεται μόνο να μετονομάσετε το κλωνοποιημένο φύλλο, που είναι ουσιαστικά η ίδια λειτουργία **change worksheet name** που εκτελέσαμε νωρίτερα.

---

## Πλήρες Παράδειγμα Εργασίας (Όλα τα Βήματα Συνδυασμένα)

Παρακάτω είναι το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε‑επικολλήσετε σε μια εφαρμογή console. Δείχνει **create excel workbook**, **set worksheet name**, **change worksheet name**, και **create report worksheet** όλα μαζί.

```csharp
using System;
using Aspose.Cells;

namespace WorksheetDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a new workbook
            Workbook workbook = new Workbook();

            // 2️⃣ Rename the default sheet to "Report"
            Worksheet masterSheet = workbook.Worksheets[0];
            masterSheet.Name = "Report";

            // 3️⃣ (Optional) Prepare SmartMarker for future data injection
            SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);
            processor.Options.DetailSheetNewName = "Report";

            // 4️⃣ (Bonus) Clone a template sheet if you have one
            // Uncomment the lines below if you have a template file.
            /*
            Workbook templateWb = new Workbook("ReportTemplate.xlsx");
            Worksheet templateSheet = templateWb.Worksheets["Template"];
            int copyIndex = workbook.Worksheets.AddCopy(templateSheet);
            Worksheet reportSheet = workbook.Worksheets[copyIndex];
            reportSheet.Name = "MonthlyReport";
            */

            // 5️⃣ Save the file
            string outputPath = "RenamedWorksheetDemo.xlsx";
            workbook.Save(outputPath, SaveFormat.Xlsx);
            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

Εκτελέστε το πρόγραμμα, ανοίξτε το παραγόμενο **RenamedWorksheetDemo.xlsx**, και θα δείτε μια καρτέλα με την ετικέτα **Report**. Αν ξεσχολιάσετε την ενότητα bonus και παρέχετε ένα πρότυπο, θα έχετε επίσης ένα φύλλο **MonthlyReport**—τέλειο για αυτοματοποιημένα pipelines αναφορών.

---

## Συμπέρασμα

Έχουμε καλύψει το **πώς να μετονομάσετε worksheet** σε C# από την αρχή: ξεκινήστε με **create excel workbook**, μετά **set worksheet name**, προαιρετικά **change worksheet name** χρησιμοποιώντας SmartMarker, και τέλος **create report worksheet** που μπορεί να επαναχρησιμοποιηθεί. Ο κώδικας είναι αυτόνομος, εκτελείται σε οποιοδήποτε περιβάλλον .NET, και αποφεύγει τα κοινά εμπόδια που συχνά παρενοχλούν τους αρχάριους.

Τι ακολουθεί; Δοκιμάστε να προσθέσετε δεδομένα στο μετονομασμένο φύλλο, πειραματιστείτε με το στυλ των κελιών, ή ενσωματώστε τα placeholders του SmartMarker για αυτόματη συμπλήρωση γραμμών από μια βάση δεδομένων. Οι δυνατότητες δημιουργίας δυναμικών αναφορών Excel είναι πρακτικά απεριόριστες.

Αν αντιμετωπίσατε κάποιο πρόβλημα—ίσως σφάλμα “invalid sheet name” ή πρόβλημα διπλού φύλλου—αφήστε ένα σχόλιο παρακάτω. Καλή κωδικοποίηση, και απολαύστε τη δύναμη του προγραμματιστικού χειρισμού Excel!

## Σχετικά Μαθήματα

- [Πώς να Χωρίσετε τα Pane του Worksheet στο Excel Χρησιμοποιώντας Aspose.Cells .NET για Βελτιωμένη Ανάλυση Δεδομένων](/cells/english/net/worksheet-management/split-worksheet-panes-excel-aspose-cells-dotnet/)
- [Ορισμός Χρωμάτων Καρτέλας Worksheet στο Excel Χρησιμοποιώντας Aspose.Cells .NET - Ένας Πλήρης Οδηγός](/cells/english/net/worksheet-management/set-worksheet-tab-colors-aspose-cells-net/)
- [Πώς να Ελέγξετε την Προστασία Κωδικού Worksheet στο Excel χρησιμοποιώντας Aspose.Cells for .NET](/cells/english/net/security-protection/aspose-cells-dotnet-check-excel-worksheet-password-protection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}