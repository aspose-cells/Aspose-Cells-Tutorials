---
category: general
date: 2026-10-26
description: Μάθετε πώς να κλειδώνετε τη γραμμή κεφαλίδας του Excel με το Aspose.Cells,
  να προστατεύετε την κεφαλίδα του πίνακα και να αποθηκεύετε το προστατευμένο βιβλίο
  εργασίας σε C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- lock excel header row
- how to lock header
- save protected workbook
- protect table header
- protect header row
language: el
lastmod: 2026-10-26
og_description: Κλειδώστε τη γραμμή κεφαλίδας του Excel χρησιμοποιώντας το Aspose.Cells,
  προστατέψτε την κεφαλίδα του πίνακα και αποθηκεύστε το προστατευμένο βιβλίο εργασίας.
  Ακολουθήστε τον βήμα‑βήμα οδηγό C#.
og_image_alt: Screenshot showing a locked Excel header row in a spreadsheet
og_title: Κλείδωμα της γραμμής κεφαλίδας του Excel σε C# – πλήρης οδηγός Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to lock Excel header row with Aspose.Cells, protect table
    header, and save protected workbook in C#.
  headline: How to lock Excel header row with Aspose.Cells in C#
  type: TechArticle
- description: Learn how to lock Excel header row with Aspose.Cells, protect table
    header, and save protected workbook in C#.
  name: How to lock Excel header row with Aspose.Cells in C#
  steps:
  - name: Click any cell in the first row of the table.
    text: Click any cell in the first row of the table.
  - name: Try to edit the text. Excel should display a message like *“The cell or
      chart you are trying to change is protected.”*
    text: Try to edit the text. Excel should display a message like *“The cell or
      chart you are trying to change is protected.”*
  - name: Click a cell in the body of the table; you should be able to edit it unless
      you protected the entire worksheet.
    text: Click a cell in the body of the table; you should be able to edit it unless
      you protected the entire worksheet.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Πώς να κλειδώσετε τη γραμμή κεφαλίδας του Excel με το Aspose.Cells σε C#
url: /el/net/worksheet-security/how-to-lock-excel-header-row-with-aspose-cells-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να κλειδώσετε τη γραμμή κεφαλίδας του Excel με το Aspose.Cells σε C#

Αν χρειάζεστε **κλείδωμα της γραμμής κεφαλίδας του Excel** ώστε οι χρήστες να μην μπορούν να επεξεργαστούν τους τίτλους των στηλών, αυτός ο οδηγός σας δείχνει τα ακριβή βήματα. Θα δείτε πώς να προστατεύσετε την κεφαλίδα ενός πίνακα, να επαληθεύσετε την προστασία και **να αποθηκεύσετε το προστατευμένο βιβλίο εργασίας** χωρίς πρόσθετη διαμόρφωση.

Το κλείδωμα της γραμμής κεφαλίδας είναι συχνή απαίτηση όταν διανέμετε πρότυπα, δημιουργείτε αναφορές ή χτίζετε φόρμες εισαγωγής δεδομένων. Στο τέλος αυτού του tutorial θα μπορείτε να προστατεύετε προγραμματιστικά την πρώτη γραμμή οποιουδήποτε πίνακα Excel και να αποθηκεύετε το βιβλίο εργασίας με ασφάλεια.

## Τι θα χρειαστείτε

- .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί επίσης με .NET Framework 4.7+)
- Aspose.Cells for .NET 2024 R2 (ή νεότερο) – ένα πακέτο NuGet που διαχειρίζεται αρχεία Excel χωρίς εγκατεστημένο Office
- Ένα αρχείο εισόδου με όνομα `input.xlsx` τοποθετημένο σε φάκελο που ελέγχετε (αντικαταστήστε το `YOUR_DIRECTORY` με την πραγματική διαδρομή)

> **Συμβουλή:** Χρησιμοποιήστε έναν αφιερωμένο φάκελο για αρχεία δοκιμής ώστε να αποφύγετε την αντικατάσταση παραγωγικών δεδομένων.

## Βήμα 1: Εγκατάσταση του Aspose.Cells

Προσθέστε τη βιβλιοθήκη στο έργο σας με το .NET CLI:

```bash
dotnet add package Aspose.Cells
```

Ή εγκαταστήστε την μέσω του Visual Studio NuGet Package Manager. Το πακέτο περιλαμβάνει τις κλάσεις `Workbook`, `Worksheet` και `Table` που χρησιμοποιούνται σε όλο το tutorial.

## Βήμα 2: Φόρτωση του βιβλίου εργασίας

Δημιουργήστε ένα νέο αντικείμενο `Workbook` που δείχνει στο πηγαίο αρχείο Excel. Αυτή η λειτουργία διαβάζει το αρχείο στη μνήμη, επιτρέποντάς σας να χειριστείτε το περιεχόμενό του.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Step 2: Load the workbook
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook wb = new Workbook(inputPath);
```

Η φόρτωση του αρχείου δεν το τροποποιεί· απλώς προετοιμάζει το μοντέλο αντικειμένων για περαιτέρω ενέργειες.

## Βήμα 3: Λήψη του πρώτου φύλλου εργασίας

Τα περισσότερα πρότυπα αποθηκεύουν δεδομένα στο πρώτο φύλλο, οπότε το ανακτούμε με βάση το δείκτη. Μπορείτε επίσης να επιλέξετε φύλλο με όνομα αν χρειάζεται.

```csharp
        // Step 3: Get the first worksheet
        Worksheet ws = wb.Worksheets[0];
```

Το αντικείμενο `Worksheet` σας δίνει πρόσβαση σε πίνακες, γραμμές, στήλες και ιδιότητες κελιών.

## Βήμα 4: Προστασία της γραμμής κεφαλίδας του πρώτου πίνακα

Το Aspose.Cells αντιμετωπίζει μια δομημένη περιοχή ως `Table`. Η σημαία `Options.ProtectHeader` κλειδώνει τη γραμμή κεφαλίδας ώστε οι χρήστες να μην μπορούν να την επεξεργαστούν, ενώ εξακολουθούν να επιτρέπεται η αλλαγή των γραμμών του σώματος.

```csharp
        // Step 4: Protect the header row of the first table
        if (ws.Tables.Count > 0)
        {
            // Protect only the header; the rest of the table stays editable
            ws.Tables[0].Options.ProtectHeader = true;
        }
        else
        {
            Console.WriteLine("No tables found on the worksheet.");
            return;
        }
```

**Γιατί λειτουργεί:** Όταν το `ProtectHeader` οριστεί σε `true`, το υποκείμενο XML σηματοδοτεί τη γραμμή κεφαλίδας με χαρακτηριστικό `locked`. Το Excel σέβεται αυτή τη σημαία κατά την κανονική επεξεργασία, αποτρέποντας τυχαίες αλλαγές στους τίτλους των στηλών.

### Προαιρετικό: Προστασία ολόκληρου του φύλλου εργασίας

Αν θέλετε επίσης να αποτρέψετε αλλαγές στις γραμμές δεδομένων, μπορείτε να προστατεύσετε ολόκληρο το φύλλο:

```csharp
        // Optional: protect the entire worksheet with a password
        ws.Protect(ProtectionType.All, "MyStrongPassword");
```

Αφήστε τον κωδικό πρόσβασης κενό για να εφαρμόσετε την προστασία χωρίς προτροπή, ή ορίστε έναν ισχυρό κωδικό για αυστηρότερη ασφάλεια.

## Βήμα 5: Αποθήκευση του βιβλίου εργασίας με την εφαρμοσμένη προστασία

Τέλος, γράψτε το τροποποιημένο βιβλίο εργασίας σε νέο αρχείο. Αυτό το βήμα δημιουργεί ένα **αποθηκευμένο προστατευμένο βιβλίο εργασίας** που διατηρεί τη κλειδωμένη κεφαλίδα όταν ανοίγει στο Excel.

```csharp
        // Step 5: Save the protected workbook
        string outputPath = @"YOUR_DIRECTORY\output.xlsx";
        wb.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath} with locked header row.");
    }
}
```

Η μέθοδος `Save` γράφει όλες τις αλλαγές, συμπεριλαμβανομένης της σημαίας προστασίας κεφαλίδας, στο αρχείο εξόδου.

## Επαλήθευση ότι η γραμμή κεφαλίδας είναι κλειδωμένη

Ανοίξτε το `output.xlsx` στο Microsoft Excel:

1. Κάντε κλικ σε οποιοδήποτε κελί της πρώτης γραμμής του πίνακα.  
2. Προσπαθήστε να επεξεργαστείτε το κείμενο. Το Excel θα πρέπει να εμφανίσει ένα μήνυμα όπως *«Το κελί ή το διάγραμμα που προσπαθείτε να αλλάξετε είναι προστατευμένο.»*  
3. Κάντε κλικ σε κελί του σώματος του πίνακα· θα πρέπει να μπορείτε να το επεξεργαστείτε εκτός αν προστατεύσατε ολόκληρο το φύλλο εργασίας.

Αν η κεφαλίδα παραμένει επεξεργάσιμη, ελέγξτε ξανά ότι το `ws.Tables[0].Options.ProtectHeader` είχε οριστεί πριν καλέσετε το `Save`.

## Συνηθισμένα προβλήματα και πώς να τα αποφύγετε

| Συμπτωμα | Πιθανή αιτία | Διόρθωση |
|---|---|---|
| Η γραμμή κεφαλίδας είναι ακόμα επεξεργάσιμη | Λάθος δείκτης πίνακα ή ο πίνακας δεν υπάρχει | Επαληθεύστε το `ws.Tables.Count` και χρησιμοποιήστε το σωστό δείκτη (`ws.Tables[0]` υποθέτει τον πρώτο πίνακα). |
| Ολόκληρο το φύλλο είναι κλειδωμένο, όχι μόνο η κεφαλίδα | Κλήση `ws.Protect` χωρίς καθορισμό `ProtectionType` | Χρησιμοποιήστε `ProtectionType.All` μόνο όταν θέλετε να κλειδώσετε ολόκληρο το φύλλο· διαφορετικά παραλείψτε αυτήν την κλήση. |
| Το αρχείο δεν μπορεί να ανοιχθεί μετά την αποθήκευση | Λάθος διαδρομή αρχείου ή έλλειψη δικαιωμάτων εγγραφής | Βεβαιωθείτε ότι το `YOUR_DIRECTORY` υπάρχει και ότι η διαδικασία έχει δικαιώματα εγγραφής. |
| Η προστασία εξαφανίζεται μετά την επανεγγραφή στο Excel | Ο χρήστης αφαίρεσε την προστασία χειροκίνητα | Υπενθυμίστε στους χρήστες να μην αφαιρούν την προστασία, ή επαναεφαρμόστε την προστασία προγραμματιστικά κάθε φορά που δημιουργείται το αρχείο. |

## Επέκταση της λύσης

Μπορείτε να κλειδώσετε πολλαπλές γραμμές κεφαλίδας ή να προστατεύσετε αρκετούς πίνακες στο ίδιο βιβλίο εργασίας:

```csharp
foreach (Table tbl in ws.Tables)
{
    tbl.Options.ProtectHeader = true;
}
```

Αν το βιβλίο εργασίας σας περιέχει πολλά φύλλα, κάντε βρόχο πάνω τους και εφαρμόστε την ίδια λογική. Αυτό το μοτίβο κλιμακώνεται σε μεγάλες λύσεις αναφορών όπου κάθε εξαγόμενο φύλλο πρέπει να διατηρεί τους τίτλους των στηλών του.

## Ανακεφαλαίωση

- **Κλείδωμα της γραμμής κεφαλίδας του Excel** ορίζοντας `Table.Options.ProtectHeader = true`.  
- Χρησιμοποιήστε το Aspose.Cells για φόρτωση, τροποποίηση και **αποθήκευση προστατευμένου βιβλίου εργασίας** χωρίς την ανάγκη Microsoft Office.  
- Επαληθεύστε την προστασία στο Excel και αντιμετωπίστε περιπτώσεις όπως έλλειψη πινάκων ή ανεπιθύμητη πλήρη προστασία φύλλου.  
- Επεκτείνετε την προσέγγιση σε πολλαπλούς πίνακες ή φύλλα όπως απαιτείται.

Τώρα έχετε έναν αξιόπιστο, προγραμματιστικό τρόπο για **προστασία της κεφαλίδας του πίνακα** και τη διασφάλιση των προτύπων Excel από τυχαίες επεμβάσεις. Πειραματιστείτε με πρόσθετες επιλογές όπως ρυθμίσεις `Worksheet.Protection` ή προσαρμοσμένους κωδικούς πρόσβασης για να ταιριάζουν στις απαιτήσεις ασφαλείας σας.

--- 

*Έτοιμοι να αυτοματοποιήσετε περισσότερες εργασίες Excel; Εξερευνήστε τα tutorials μας για **πώς να κλειδώσετε κεφαλίδες**, να εφαρμόσετε επικύρωση δεδομένων και να δημιουργήσετε γραφήματα απευθείας από C#.*


## Τι πρέπει να μάθετε στη συνέχεια;


Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κυριαρχήσετε επιπλέον δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στα δικά σας έργα.

- [Aspose Cells Delete Rows – Protect Header Row in Excel](/cells/english/net/row-and-column-management/aspose-cells-delete-rows-protect-header-row-in-excel/)
- [how to delete rows in Excel with C# – protect table header](/cells/english/net/row-and-column-management/how-to-delete-rows-in-excel-with-c-protect-table-header/)
- [How to Lock Cells and Protect Sheets in Excel using Aspose.Cells for .NET](/cells/english/net/security-protection/secure-excel-cell-lock-sheet-protection-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}