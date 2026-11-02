---
category: general
date: 2026-09-08
description: Μάθετε πώς να αποθηκεύσετε το βιβλίο εργασίας ως CSV, ορίζοντας τα σημαντικά
  ψηφία και ρυθμίζοντας λεπτομερώς τις επιλογές εξαγωγής CSV για αριθμητικά δεδομένα.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save workbook as csv
- set significant digits
- csv export options
- save excel as csv
- export numeric csv
language: el
lastmod: 2026-09-08
og_description: Αποθηκεύστε το βιβλίο εργασίας ως CSV με το Aspose.Cells και ορίστε
  τα σημαντικά ψηφία. Κατακτήστε τις επιλογές εξαγωγής CSV για αριθμητικά αρχεία CSV
  σε C#.
og_image_alt: Screenshot of a CSV file generated after saving workbook as CSV with
  four significant digits
og_title: Αποθήκευση βιβλίου εργασίας ως CSV με σημαντικά ψηφία – πλήρης οδηγός Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-09-08'
  description: Learn how to save workbook as CSV while set significant digits and
    fine‑tune CSV export options for numeric data.
  headline: How to save workbook as CSV with precise formatting using Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- CSV export
title: Πώς να αποθηκεύσετε το βιβλίο εργασίας ως CSV με ακριβή μορφοποίηση χρησιμοποιώντας
  το Aspose.Cells
url: /el/net/csv-file-handling/how-to-save-workbook-as-csv-with-precise-formatting-using-as/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να αποθηκεύσετε ένα βιβλίο εργασίας ως CSV με ακριβή μορφοποίηση χρησιμοποιώντας το Aspose.Cells

Εάν χρειάζεστε να **save workbook as CSV** ενώ διατηρείτε μόνο έναν συγκεκριμένο αριθμό σημαντικών ψηφίων, αυτός ο οδηγός σας δείχνει ακριβώς πώς. Θα μάθετε να διαμορφώνετε **CSV export options**, να ορίζετε τον αριθμό **significant digits** και να δημιουργείτε ένα καθαρό αριθμητικό αρχείο CSV με λίγες μόνο γραμμές C#.

Η αποθήκευση ενός βιβλίου εργασίας ως CSV είναι μια κοινή απαίτηση όταν θέλετε να ανταλλάξετε δεδομένα με συστήματα που καταναλώνουν πίνακες απλού κειμένου. Από προεπιλογή, το Aspose.Cells γράφει κάθε δεκαδική θέση, κάτι που μπορεί να αυξήσει το μέγεθος του αρχείου και να προκαλέσει προβλήματα ανάλυσης στο downstream. Η προσαρμογή των ρυθμίσεων εξαγωγής σας επιτρέπει να **save Excel as CSV** που περιέχει μόνο την ακρίβεια που απαιτείτε, καθιστώντας το αρχείο ελαφρύ και πιο εύκολο στην κατανάλωση.

## Τι καλύπτει αυτός ο οδηγός

* Πώς να δημιουργήσετε ένα νέο workbook και να γράψετε αριθμητικά δεδομένα.
* Πώς να **set significant digits** χρησιμοποιώντας το τελευταίο `CsvSaveOptions`.
* Πώς να εφαρμόσετε **CSV export options** για να ελέγξετε τη μορφή εξόδου.
* Πώς να **save workbook as CSV** και να επαληθεύσετε το αποτέλεσμα **export numeric CSV**.
* Συμβουλές για τη διαχείριση edge cases όπως μεγάλοι αριθμοί ή locale‑specific delimiters.

Χρειάζεστε μόνο ένα περιβάλλον ανάπτυξης .NET και μια αναφορά στη βιβλιοθήκη Aspose.Cells (έκδοση 25.10 ή νεότερη). Δεν απαιτούνται επιπλέον πακέτα.

## Βήμα 1: Δημιουργία workbook και προσθήκη αριθμητικών δεδομένων

Το πρώτο βήμα είναι η δημιουργία ενός αντικειμένου `Workbook` και η εγγραφή ενός αριθμού σε ένα κελί. Αυτό αντικατοπτρίζει τη συνήθη ροή εργασίας της συμπλήρωσης ενός φύλλου Excel πριν από την εξαγωγή.

```csharp
using Aspose.Cells;

 // Create a new workbook with a single worksheet
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];

// Write a numeric value into cell A1
Cell cell = worksheet.Cells["A1"];
cell.PutValue(1234.56789);
```

**Γιατί αυτό είναι σημαντικό:**  
Η κλάση `Workbook` αντιπροσωπεύει ολόκληρο το αρχείο Excel στη μνήμη. Η προσθήκη της τιμής στο `A1` μας δίνει έναν συγκεκριμένο αριθμό που μπορούμε αργότερα να μορφοποιήσουμε με **significant digits**. Ο κώδικας λειτουργεί με οποιονδήποτε αριθμητικό τύπο (double, decimal, κ.λπ.) και δεν εξαρτάται από εξωτερικές πηγές δεδομένων.

## Βήμα 2: Διαμόρφωση CSV export options – ορισμός σημαντικών ψηφίων

Το Aspose.Cells εισήγαγε την ιδιότητα `SignificantDigits` στο `CsvSaveOptions` (v 25.10). Στρογγυλοποιεί κάθε αριθμητικό κελί στον καθορισμένο αριθμό ψηφίων πριν γράψει το αρχείο CSV.

```csharp
// Configure CSV export options
CsvSaveOptions csvOptions = new CsvSaveOptions
{
    // Keep only 4 significant digits in the output
    SignificantDigits = 4
};
```

**Γιατί αυτό είναι σημαντικό:**  
Ορίζοντας το `SignificantDigits` σε 4 λέει στον εξαγωγέα να στρογγυλοποιήσει το `1234.56789` σε `1235`. Αυτό μειώνει το μέγεθος του αρχείου και αφαιρεί την περιττή ακρίβεια, κάτι που είναι ιδιαίτερα χρήσιμο όταν το σύστημα-στόχος αναμένει τιμές σταθερού σημείου.

> **Pro tip:** Εάν χρειάζεται να διατηρήσετε τα μηδενικά στο τέλος (π.χ., `1.200`), συνδυάστε το `SignificantDigits` με τις ρυθμίσεις `NumberDecimalSeparator` και `NumberGroupSeparator` για να ελέγξετε την ακριβή κειμενική αναπαράσταση.

## Βήμα 3: Αποθήκευση του workbook ως CSV χρησιμοποιώντας τις διαμορφωμένες επιλογές

Τώρα μπορείτε να γράψετε το workbook σε αρχείο CSV. Η μέθοδος `Save` δέχεται το αντικείμενο `CsvSaveOptions`, διασφαλίζοντας ότι το **export numeric CSV** τηρεί το όριο ψηφίων.

```csharp
// Save the workbook as a CSV file
string outputPath = @"C:\Temp\SignificantDigits.csv";
workbook.Save(outputPath, csvOptions);
```

**Γιατί αυτό είναι σημαντικό:**  
Η κλήση στο `Save` εκτελεί τη μετατροπή σε μία μόνο διεργασία, εφαρμόζοντας όλες τις **CSV export options** που ορίσατε. Το προκύπτον αρχείο περιέχει μόνο την στρογγυλοποιημένη τιμή, έτοιμο για downstream επεξεργασία.

### Αναμενόμενο περιεχόμενο CSV

Αφού εκτελέσετε τον παραπάνω κώδικα, ανοίξτε το `SignificantDigits.csv`. Θα πρέπει να δείτε:

```
1235
```

Η μοναδική γραμμή αντανακλά τον αρχικό αριθμό στρογγυλοποιημένο σε τέσσερα σημαντικά ψηφία, δείχνοντας ότι η επιλογή **set significant digits** λειτούργησε όπως αναμενόταν.

## Βήμα 4: Επαλήθευση του αποτελέσματος προγραμματιστικά (προαιρετικό)

Εάν προτιμάτε έναν αυτοματοποιημένο έλεγχο, διαβάστε το παραγόμενο αρχείο ξανά στη μνήμη και ελέγξτε το περιεχόμενο.

```csharp
string[] lines = System.IO.File.ReadAllLines(outputPath);
if (lines.Length == 1 && lines[0] == "1235")
{
    Console.WriteLine("CSV export succeeded – numeric value correctly rounded.");
}
else
{
    Console.WriteLine("CSV export verification failed.");
}
```

**Γιατί αυτό είναι σημαντικό:**  
Η αυτοματοποιημένη επαλήθευση είναι χρήσιμη σε unit tests ή CI pipelines όπου πρέπει να εγγυηθείτε ότι η λειτουργία **save workbook as csv** παράγει καθοριστικό αποτέλεσμα.

## Βήμα 5: Συνηθισμένες παραλλαγές και διαχείριση edge‑case

| Κατάσταση | Συνιστώμενη ρύθμιση | Απόσπασμα κώδικα |
|-----------|---------------------|------------------|
| **Μεγάλοι αριθμοί** (π.χ., `9.87654321E+12`) | Αυξήστε το `SignificantDigits` ή χρησιμοποιήστε `NumberDecimalSeparator = ""` για να αποφύγετε τη επιστημονική σημειογραφία | `csvOptions.SignificantDigits = 6;` |
| **Διαχωριστές ειδικές για locale** (κόμμα ως δεκαδικό) | Ορίστε `NumberDecimalSeparator = ","` και `Separator = ";"` | `csvOptions.NumberDecimalSeparator = ","; csvOptions.Separator = ";";` |
| **Διατήρηση αρχικών μηδενικών** (π.χ., ταχυδρομικοί κώδικες) | Εξάγετε τη στήλη ως κείμενο πριν την αποθήκευση | `cell.PutValue("'00123");` |
| **Πολλαπλά φύλλα εργασίας** | Επανάληψη σε κάθε φύλλο και αποθήκευση ξεχωριστά ή συνένωση | `foreach (var sheet in workbook.Worksheets) { /* save each */ }` |

Αυτές οι παραλλαγές δείχνουν ότι το **save excel as csv** είναι αρκετά ευέλικτο ώστε να καλύψει διάφορες απαιτήσεις ανταλλαγής δεδομένων.

## Βήμα 6: Πλήρες, εκτελέσιμο παράδειγμα

Παρακάτω βρίσκεται το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε‑επικολλήσετε σε ένα νέο έργο C# console. Περιλαμβάνει όλα τα βήματα, τη διαχείριση σφαλμάτων και τη λογική επαλήθευσης.

```csharp
using System;
using Aspose.Cells;

namespace CsvExportDemo
{
    class Program
    {
        static void Main()
        {
            try
            {
                // 1️⃣ Create workbook and write a numeric value
                Workbook workbook = new Workbook();
                Worksheet worksheet = workbook.Worksheets[0];
                Cell cell = worksheet.Cells["A1"];
                cell.PutValue(1234.56789);

                // 2️⃣ Configure CSV export options – set significant digits
                CsvSaveOptions csvOptions = new CsvSaveOptions
                {
                    SignificantDigits = 4   // Keep only 4 significant digits
                };

                // 3️⃣ Save workbook as CSV
                string outputPath = @"C:\Temp\SignificantDigits.csv";
                workbook.Save(outputPath, csvOptions);
                Console.WriteLine($"Workbook saved as CSV to: {outputPath}");

                // 4️⃣ Verify the exported content
                string[] lines = System.IO.File.ReadAllLines(outputPath);
                if (lines.Length == 1 && lines[0] == "1235")
                {
                    Console.WriteLine("CSV export succeeded – numeric value correctly rounded.");
                }
                else
                {
                    Console.WriteLine("CSV export verification failed. Content:");
                    foreach (var line in lines) Console.WriteLine(line);
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Error during CSV export: {ex.Message}");
            }
        }
    }
}
```

**Running the program** δημιουργεί το `C:\Temp\SignificantDigits.csv` που περιέχει τη στρογγυλοποιημένη τιμή `1235`. Προσαρμόστε το `outputPath` όπως χρειάζεται για το περιβάλλον σας.

## Συμπέρασμα

Τώρα ξέρετε πώς να **save workbook as CSV** ενώ ελέγχετε με ακρίβεια τον αριθμό των σημαντικών ψηφίων. Διαμορφώνοντας τις **CSV export options**—συγκεκριμένα την ιδιότητα `SignificantDigits`—μπορείτε να δημιουργήσετε καθαρά, ελαφριά αρχεία **export numeric CSV** που ικανοποιούν τις προσδοκίες των downstream συστημάτων.  

Από εδώ μπορείτε να:

* Δοκιμάσετε διαφορετικές τιμές `SignificantDigits` για πιο ακριβή ή πιο αδρή στρογγυλοποίηση.  
* Συνδυάσετε άλλες `CsvSaveOptions` (π.χ., `Separator`, `Encoding`) για να ταιριάξετε με τα τοπικά πρότυπα CSV.  
* Ενσωματώσετε αυτή τη ροή εργασίας σε μεγαλύτερους pipelines επεξεργασίας δεδομένων που απαιτούν αυτοματοποιημένη μετατροπή Excel‑to‑CSV.

Καλή προγραμματιστική δουλειά, και απολαύστε την απλότητα της εξαγωγής ακριβών αριθμητικών δεδομένων με το Aspose.Cells!

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που βασίζονται στις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Αποθήκευση Workbook σε μορφή Text CSV](/cells/english/net/saving-files-in-different-formats/save-workbook-to-text-csv-format/)
- [Πώς να φορτώσετε και να αποθηκεύσετε Excel ως CSV χρησιμοποιώντας Aspose.Cells για Java: Ένας ολοκληρωμένος οδηγός](/cells/english/java/workbook-operations/aspose-cells-java-load-save-excel-csv/)
- [Περικοπή & Αποθήκευση αρχείων Excel ως CSV χρησιμοποιώντας Aspose.Cells σε Java](/cells/english/java/workbook-operations/excel-aspose-cells-java-trim-save-csv/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}