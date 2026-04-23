---
category: general
date: 2026-03-18
description: Δημιουργήστε νέο βιβλίο εργασίας και εξάγετε το Excel σε TXT διατηρώντας
  την αριθμητική ακρίβεια. Μάθετε πώς να αποθηκεύετε ένα φύλλο εργασίας ως txt και
  να μετατρέπετε το φύλλο εργασίας σε txt αποδοτικά.
draft: false
keywords:
- create new workbook
- export excel to txt
- save excel as txt
- save worksheet as txt
- convert worksheet to txt
language: el
og_description: Δημιουργήστε νέο βιβλίο εργασίας και εξαγάγετε το Excel σε TXT με
  ακρίβεια. Αυτό το σεμινάριο δείχνει πώς να αποθηκεύσετε το φύλλο εργασίας ως txt
  και να μετατρέψετε το φύλλο εργασίας σε txt χρησιμοποιώντας C#.
og_title: Δημιουργία νέου βιβλίου εργασίας – Οδηγός εξαγωγής Excel σε TXT
tags:
- Aspose.Cells
- C#
- Excel automation
title: Δημιουργία νέου φύλλου εργασίας – Εξαγωγή Excel σε TXT με πλήρη ακρίβεια
url: /el/net/converting-excel-files-to-other-formats/create-new-workbook-export-excel-to-txt-with-full-precision/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία νέου βιβλίου εργασίας – Εξαγωγή Excel σε TXT με Πλήρη Ακρίβεια

Σας έχει συμβεί ποτέ να χρειάζεται να **create new workbook** σε C# μόνο για να αποθηκεύσετε κάποια δεδομένα σε ένα αρχείο απλού κειμένου; Ίσως να εξάγετε μια αναφορά από ένα παλαιό σύστημα και το επόμενο εργαλείο δέχεται μόνο αρχείο `.txt`. Τα καλά νέα; Δεν χρειάζεται να θυσιάσετε την αριθμητική ακρίβεια και σίγουρα δεν χρειάζεται να δημιουργήσετε χειροκίνητα συμβολοσειρές CSV.

Σε αυτόν τον οδηγό θα περάσουμε από όλη τη διαδικασία του **export excel to txt**, καλύπτοντας τα πάντα από την αρχικοποίηση του βιβλίου εργασίας μέχρι τη διατήρηση των μηδενικών στο τέλος όταν **save worksheet as txt**. Στο τέλος θα έχετε ένα έτοιμο κομμάτι κώδικα που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο .NET—χωρίς επιπλέον βοηθήματα.

## Τι Θα Χρειαστεί

- **ASP.NET/ .NET 6+** (ο κώδικας λειτουργεί επίσης σε .NET Framework 4.6+)  
- **Aspose.Cells for .NET** – η βιβλιοθήκη που τροφοδοτεί τις κλάσεις `Workbook`, `Worksheet` και `TxtSaveOptions`. Μπορείτε να την αποκτήσετε από το NuGet με `Install-Package Aspose.Cells`.  
- Βασική κατανόηση της C# (αν είστε άνετοι με τις δηλώσεις `using`, είστε έτοιμοι).  

Αυτό είναι όλο—χωρίς Excel interop, χωρίς αντικείμενα COM, και σίγουρα χωρίς χειροκίνητη συνένωση συμβολοσειρών.

---

## Βήμα 1: Αρχικοποίηση Νέου Βιβλίου Εργασίας (Primary Keyword)

Το πρώτο πράγμα που πρέπει να κάνετε είναι **create new workbook**. Σκεφτείτε το βιβλίο εργασίας ως έναν κενό καμβά όπου θα επικολλήσετε αργότερα αριθμούς, κείμενο ή τύπους.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToTxtDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Create a new workbook and get the first worksheet
            Workbook workbook = new Workbook();                 // <‑‑ creates new workbook
            Worksheet worksheet = workbook.Worksheets[0];       // first sheet (index 0)
```

> **Why this matters:** Η δημιουργία ενός αντικειμένου `Workbook` χωρίς φόρτωση αρχείου σας παρέχει καθαρό καμβά. Μπορείτε στη συνέχεια να προσθέσετε δεδομένα προγραμματιστικά, κάτι που είναι ιδανικό για σενάρια **convert worksheet to txt** όπου δεν έχετε υπάρχον `.xlsx`.

## Βήμα 2: Συμπλήρωση Κελιών – Διατήρηση των Μηδενικών στο Τέλος

Ένα κοινό λάθος όταν αποθηκεύετε αριθμούς σε κείμενο είναι η απώλεια των μηδενικών στο τέλος (`123.45000` γίνεται `123.45`). Αν τα επόμενα συστήματα βασίζονται σε πεδία σταθερού πλάτους, αυτή η απώλεια μπορεί να σπάσει τα πάντα.

```csharp
            // Step 2: Write a numeric value that contains trailing zeros
            // PutValue respects the data type; we’ll later tell the saver to keep precision.
            worksheet.Cells[0, 0].PutValue(123.45000);
```

> **Pro tip:** Η `PutValue` αυτόματα ανιχνεύει τον τύπο δεδομένων. Αν χρειάζεστε μια συμβολοσειρά που μοιάζει με αριθμό, χρησιμοποιήστε `PutValue("123.45000")`.

## Βήμα 3: Διαμόρφωση Επιλογών Αποθήκευσης TXT – Διατήρηση Αριθμητικής Ακρίβειας

Εδώ συμβαίνει η μαγεία. Με την ενεργοποίηση του `PreserveNumericPrecision`, υποδεικνύετε στο Aspose.Cells να γράψει την ακριβή τιμή που εισάγατε, συμπεριλαμβανομένων τυχόν ασήμαντων μηδενικών στο τέλος.

```csharp
            // Step 3: Configure TXT save options to keep the original numeric precision
            TxtSaveOptions txtSaveOptions = new TxtSaveOptions(SaveFormat.Txt)
            {
                PreserveNumericPrecision = true   // retain all digits, even trailing zeros
            };
```

> **Why enable this?** Όταν **save excel as txt**, η προεπιλεγμένη συμπεριφορά αφαιρεί τα περιττά δεκαδικά. Ορίζοντας `PreserveNumericPrecision = true` εξασφαλίζει ότι η έξοδος αντικατοπτρίζει την τιμή που εμφανίζεται στο κελί, κάτι κρίσιμο για οικονομικές αναφορές ή επιστημονικά δεδομένα.

## Βήμα 4: Αποθήκευση του Φύλλου Εργασίας ως TXT – Η Τελική Εξαγωγή

Τώρα πραγματικά **save worksheet as txt**. Μπορείτε να ορίσετε τη διαδρομή οπουδήποτε έχετε δικαίωμα εγγραφής· το παράδειγμα χρησιμοποιεί έναν σχετικό φάκελο που ονομάζεται `output`.

```csharp
            // Step 4: Save the worksheet as a TXT file using the configured options
            string outputPath = "output/num-preserve.txt";
            worksheet.Save(outputPath, txtSaveOptions);

            Console.WriteLine($"File saved to {outputPath}");
        }
    }
}
```

> **Expected output** (`num-preserve.txt`):

```
123.45000
```

Παρατηρήστε ότι τα μηδενικά στο τέλος παραμένουν—ακριβώς όπως ζητήσατε.

## Βήμα 5: Επαλήθευση του Αποτελέσματος – Γρήγορος Έλεγχος

Μετά την εκτέλεση του προγράμματος, ανοίξτε το `num-preserve.txt` σε οποιονδήποτε επεξεργαστή κειμένου. Θα πρέπει να δείτε τη μοναδική γραμμή `123.45000`. Αν δείτε `123.45` αντί αυτού, ελέγξτε ξανά ότι το `PreserveNumericPrecision` είναι ορισμένο σε `true` και ότι χρησιμοποιείτε πρόσφατη έκδοση του Aspose.Cells (v23.10+).

## Κοινές Παραλλαγές & Ακραίες Περιπτώσεις

### Εξαγωγή Πολλαπλών Κελιών ή Περιοχών

Αν χρειάζεστε **export excel to txt** για ολόκληρη περιοχή, απλώς γεμίστε περισσότερα κελιά πριν την αποθήκευση:

```csharp
worksheet.Cells["A1"].PutValue(100);
worksheet.Cells["A2"].PutValue(200.500);
worksheet.Cells["A3"].PutValue(300.00);
```

Το Aspose θα γράψει κάθε κελί σε νέα γραμμή εξ ορισμού. Μπορείτε επίσης να αλλάξετε το διαχωριστικό (tab, κόμμα) μέσω του `txtSaveOptions.Separator`.

### Μετατροπή Φύλλου Εργασίας σε TXT με Διαφορετικές Κωδικοποιήσεις

Μερικές φορές τα επόμενα συστήματα απαιτούν UTF‑8 BOM ή ASCII. Ρυθμίστε την κωδικοποίηση ως εξής:

```csharp
txtSaveOptions.Encoding = System.Text.Encoding.UTF8;
```

### Διαχείριση Μεγάλων Βιβλίων Εργασίας

Όταν εργάζεστε με τεράστιες φύλλα (εκατοντάδες χιλιάδες γραμμές), σκεφτείτε τη ροή εξόδου:

```csharp
txtSaveOptions.EnableCache = true; // writes data in chunks to reduce memory footprint
```

---

## Συμβουλές & Προβλήματα

- **Don’t forget to create the output directory** πριν καλέσετε το `Save`, διαφορετικά θα λάβετε ένα `DirectoryNotFoundException`.  
- **Watch out for locale‑specific decimal separators**. Αν το περιβάλλον σας χρησιμοποιεί κόμματα (`1,23`), ορίστε `txtSaveOptions.DecimalSeparator = '.'` για να επιβάλετε τελεία.  
- **Version compatibility**: Η σημαία `PreserveNumericPrecision` εισήχθη στο Aspose.Cells 20.6. Αν χρησιμοποιείτε παλαιότερη έκδοση, η σημαία δεν υπάρχει και θα πρέπει να μορφοποιήσετε το κελί ως κείμενο πριν την αποθήκευση.

![Παράδειγμα δημιουργίας νέου βιβλίου εργασίας](excel-to-txt.png "Δημιουργία νέου βιβλίου εργασίας")

*Image alt text: "Δημιουργία νέου βιβλίου εργασίας και εξαγωγή Excel σε TXT με διατηρημένη αριθμητική ακρίβεια"*

## Ανακεφαλαίωση – Τι Καλύψαμε

- **Create new workbook** χρησιμοποιώντας Aspose.Cells.  
- Συμπληρώστε ένα κελί με αριθμό που περιλαμβάνει μηδενικά στο τέλος.  
- Ορίστε `TxtSaveOptions.PreserveNumericPrecision = true` για **save excel as txt** χωρίς απώλεια ακρίβειας.  
- Γράψτε το αρχείο στο δίσκο, επαληθεύοντας ότι η έξοδος ταιριάζει με την αρχική τιμή.  

Αυτή είναι η πλήρης ροή εργασίας **convert worksheet to txt** σε λιγότερο από 50 γραμμές C#.

## Επόμενα Βήματα & Σχετικά Θέματα

Τώρα που μπορείτε να **export excel to txt** με τέλεια ακρίβεια, ίσως θέλετε να εξερευνήσετε:

- **Exporting to CSV** με προσαρμοσμένα διαχωριστικά (`TxtSaveOptions.Separator`).  
- **Saving as other plain‑text formats** όπως TSV (`SaveFormat.TabDelimited`).  
- **Batch processing** πολλαπλά βιβλία εργασίας σε φάκελο χρησιμοποιώντας `Directory.GetFiles`.  
- **Integrating with Azure Functions** για μετατροπή κατόπιν ζήτησης στο cloud.  

Κάθε ένα από αυτά βασίζεται στο ίδιο μοτίβο `Workbook` → `Worksheet` → `TxtSaveOptions`, ώστε να αισθάνεστε άνετα.

---

### Τελική Σκέψη

Αν ακολουθήσατε τα βήματα, τώρα ξέρετε ακριβώς πώς να **create new workbook**, να το συμπληρώσετε και να **save worksheet as txt** διατηρώντας κάθε δεκαδικό ψηφίο που σας ενδιαφέρει. Είναι ένα μικρό κομμάτι κώδικα, αλλά λύνει ένα απροσδόκητα κοινό πρόβλημα όταν οι παλαιές γραμμές παραγωγής απαιτούν εισόδους απλού κειμένου.

Δοκιμάστε το, προσαρμόστε τις επιλογές, και αφήστε τα δεδομένα να ρέουν ακριβώς όπως χρειάζεστε. Καλό προγραμματισμό!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}