---
category: general
date: 2026-04-07
description: Δημιουργήστε νέο βιβλίο εργασίας σε C# και μάθετε πώς να εξάγετε CSV
  με σημαντικά ψηφία. Περιλαμβάνει αποθήκευση βιβλίου εργασίας ως CSV και συμβουλές
  για εξαγωγή Excel σε CSV.
draft: false
keywords:
- create new workbook
- save workbook as csv
- how to export csv
- save file as csv
- export excel to csv
language: el
og_description: Δημιουργήστε νέο βιβλίο εργασίας σε C# και εξάγετε το σε CSV με πλήρη
  έλεγχο των σημαντικών ψηφίων. Μάθετε πώς να αποθηκεύετε το βιβλίο εργασίας ως CSV
  και να εξάγετε το Excel σε CSV.
og_title: Δημιουργία Νέου Φύλλου Εργασίας και Εξαγωγή σε CSV – Πλήρης Οδηγός C#
tags:
- C#
- Aspose.Cells
- CSV export
- Excel automation
title: Δημιουργία Νέου Φύλλου Εργασίας και Εξαγωγή σε CSV – Οδηγός C# Βήμα‑προς‑Βήμα
url: /el/net/csv-file-handling/create-new-workbook-and-export-to-csv-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία Νέου Workbook και Εξαγωγή σε CSV – Πλήρες Tutorial C#

Έχετε ποτέ χρειαστεί να **δημιουργήσετε νέο workbook** σε C# μόνο για να αναρωτηθείτε *πώς να εξάγετε CSV* χωρίς να χάσετε την ακρίβεια; Δεν είστε ο μόνος. Σε πολλά έργα data‑pipeline το τελικό βήμα είναι ένα καθαρό αρχείο CSV, και η σωστή μορφοποίηση μπορεί να είναι πονοκέφαλο.  

Σε αυτόν τον οδηγό θα διασχίσουμε όλη τη διαδικασία: από τη δημιουργία ενός φρέσκου workbook, την τοποθέτηση μιας αριθμητικής τιμής, τη ρύθμιση των επιλογών εξαγωγής για σημαντικά ψηφία, και τελικά **save workbook as CSV**. Στο τέλος θα έχετε ένα έτοιμο προς χρήση αρχείο CSV και μια σταθερή κατανόηση της ροής εργασίας *export excel to CSV* χρησιμοποιώντας το Aspose.Cells.

## Τι Θα Χρειαστεί

- **Aspose.Cells for .NET** (το πακέτο NuGet `Aspose.Cells` – έκδοση 23.10 ή νεότερη).  
- Ένα περιβάλλον ανάπτυξης .NET (Visual Studio, Rider ή το `dotnet` CLI).  
- Βασικές γνώσεις C#· δεν απαιτούνται προχωρημένα κόλπα Excel interop.  

Αυτό είναι όλο—χωρίς επιπλέον αναφορές COM, χωρίς ανάγκη εγκατάστασης Excel.

## Βήμα 1: Δημιουργία Νέου Αντικειμένου Workbook

Πρώτα απ' όλα: χρειαζόμαστε ένα ολοκαίνουργιο αντικείμενο workbook. Σκεφτείτε το ως ένα κενό φύλλο εργασίας που υπάρχει εξ ολοκλήρου στη μνήμη.

```csharp
using Aspose.Cells;

// Step 1: Create a new workbook
Workbook workbook = new Workbook();
```

> **Γιατί;** Η κλάση `Workbook` είναι το σημείο εισόδου για οποιαδήποτε επεξεργασία Excel στο Aspose.Cells. Η δημιουργία της προγραμματιστικά σημαίνει ότι δεν εξαρτάστε από υπάρχον αρχείο, κάτι που διατηρεί το βήμα **save file as CSV** καθαρό και προβλέψιμο.

## Βήμα 2: Λήψη του Πρώτου Worksheet

Κάθε workbook περιλαμβάνει τουλάχιστον ένα worksheet. Θα πάρουμε το πρώτο και θα του δώσουμε ένα φιλικό όνομα.

```csharp
// Step 2: Get the first worksheet (index 0)
Worksheet worksheet = workbook.Worksheets[0];
worksheet.Name = "Data";
```

> **Συμβουλή:** Η μετονομασία των worksheets βοηθά όταν αργότερα ανοίγετε το CSV σε έναν προβολέα που σέβεται τα ονόματα φύλλων, παρόλο που το CSV από μόνο του δεν τα αποθηκεύει.

## Βήμα 3: Εισαγωγή Αριθμητικής Τιμής στο Κελί A1

Τώρα εισάγουμε έναν αριθμό που έχει περισσότερα δεκαδικά ψηφία από όσα τελικά θέλουμε να διατηρήσουμε. Αυτό θα μας επιτρέψει να δείξουμε τη λειτουργία *significant digits*.

```csharp
// Step 3: Write a numeric value into cell A1
worksheet.Cells["A1"].PutValue(12345.6789);
```

> **Τι αν χρειάζεστε περισσότερα δεδομένα;** Απλώς συνεχίστε να χρησιμοποιείτε `PutValue` σε άλλα κελιά (`B2`, `C3`, …) – οι ίδιες ρυθμίσεις εξαγωγής θα ισχύσουν για ολόκληρο το φύλλο όταν **save workbook as CSV**.

## Βήμα 4: Διαμόρφωση Επιλογών Εξαγωγής για Significant Digits

Το Aspose.Cells σας επιτρέπει να ελέγχετε πώς εμφανίζονται οι αριθμοί στην έξοδο CSV. Εδώ ζητάμε τέσσερα significant digits και ενεργοποιούμε τη λειτουργία.

```csharp
// Step 4: Configure export options to use significant digits
ExportOptions exportOptions = new ExportOptions
{
    SignificantDigits = 4,      // keep only 4 significant digits
    UseSignificantDigits = true // enable the feature
};
```

> **Γιατί να χρησιμοποιήσετε significant digits;** Όταν εργάζεστε με επιστημονικά δεδομένα ή οικονομικές αναφορές, συχνά ενδιαφέρεστε για την ακρίβεια αντί για τα ακατέργαστα δεκαδικά ψηφία. Αυτή η ρύθμιση εξασφαλίζει ότι το CSV αντικατοπτρίζει την επιθυμητή ακρίβεια, κάτι που είναι κοινό πρόβλημα όταν *πώς να εξάγετε CSV* για ανάλυση downstream.

## Βήμα 5: Αποθήκευση του Workbook ως Αρχείο CSV

Τέλος, γράφουμε το workbook στο δίσκο χρησιμοποιώντας τη μορφή CSV και τις επιλογές που μόλις ορίσαμε.

```csharp
// Step 5: Save the workbook as a CSV file using the configured options
string outputPath = @"C:\Temp\out.csv";
workbook.Save(outputPath, SaveFormat.Csv, exportOptions);
```

> **Αναμενόμενη έξοδος:** Το αρχείο `out.csv` θα περιέχει μία μόνο γραμμή:

```
12350
```

Παρατηρήστε πώς το `12345.6789` στρογγυλοποιήθηκε σε `12350`—αυτό είναι το αποτέλεσμα της διατήρησης τεσσάρων significant digits.

### Γρήγορη Λίστα Ελέγχου για Αποθήκευση CSV

- **Path exists:** Βεβαιωθείτε ότι ο φάκελος (`C:\Temp` στο παράδειγμα) υπάρχει, διαφορετικά το `Save` θα ρίξει εξαίρεση.
- **File permissions:** Η διαδικασία πρέπει να έχει δικαίωμα εγγραφής· διαφορετικά θα δείτε ένα `UnauthorizedAccessException`.
- **Encoding:** Το Aspose.Cells χρησιμοποιεί UTF‑8 εξ ορισμού, το οποίο λειτουργεί για τις περισσότερες τοπικές ρυθμίσεις. Αν χρειάζεστε διαφορετική κωδικοσελίδα, ορίστε `exportOptions.Encoding` πριν καλέσετε το `Save`.

## Συνηθισμένες Παραλλαγές & Ακραίες Περιπτώσεις

### Εξαγωγή Πολλαπλών Worksheets

Το CSV είναι από τη φύση του μορφή μονο‑sheet. Αν καλέσετε `Save` σε ένα workbook με πολλά φύλλα, το Aspose.Cells θα τα συνενώσει, χωρίζοντας κάθε φύλλο με αλλαγή γραμμής. Για να **save file as CSV** μόνο για ένα συγκεκριμένο φύλλο, κρύψτε προσωρινά τα υπόλοιπα:

```csharp
// Hide all sheets except the one you want to export
foreach (Worksheet ws in workbook.Worksheets)
{
    ws.IsVisible = false;
}
worksheet.IsVisible = true; // the sheet we prepared earlier
workbook.Save(outputPath, SaveFormat.Csv, exportOptions);
```

### Έλεγχος Διαχωριστών

Από προεπιλογή, το Aspose.Cells χρησιμοποιεί κόμμα (`,`) ως διαχωριστικό. Αν χρειάζεστε ελληνικό ερωτηματικό (`;`) για ευρωπαϊκές τοπικές ρυθμίσεις, προσαρμόστε το `CsvSaveOptions`:

```csharp
CsvSaveOptions csvOptions = new CsvSaveOptions
{
    Separator = ';',
    ExportOptions = exportOptions
};
workbook.Save(outputPath, csvOptions);
```

### Μεγάλα Σύνολα Δεδομένων

Κατά την εξαγωγή εκατομμυρίων γραμμών, σκεφτείτε τη ροή (streaming) του CSV για να αποφύγετε την υψηλή κατανάλωση μνήμης. Το Aspose.Cells προσφέρει υπερφορτώσεις του `Workbook.Save` που δέχονται ένα `Stream`, επιτρέποντάς σας να γράψετε απευθείας σε αρχείο, τοποθεσία δικτύου ή αποθήκη cloud.

## Πλήρες Παράδειγμα Εργασίας

Παρακάτω βρίσκεται το πλήρες, έτοιμο‑να‑εκτελεστεί πρόγραμμα που ενώνει όλα τα παραπάνω. Αντιγράψτε‑και‑επικολλήστε το σε ένα project console app και πατήστε **F5**.

```csharp
using System;
using Aspose.Cells;

namespace CsvExportDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a new workbook
            Workbook workbook = new Workbook();

            // 2️⃣ Get the first worksheet and give it a name
            Worksheet worksheet = workbook.Worksheets[0];
            worksheet.Name = "Data";

            // 3️⃣ Insert a numeric value (more precision than we need)
            worksheet.Cells["A1"].PutValue(12345.6789);

            // 4️⃣ Set up export options – 4 significant digits
            ExportOptions exportOptions = new ExportOptions
            {
                SignificantDigits = 4,
                UseSignificantDigits = true
            };

            // 5️⃣ Define where the CSV will be saved
            string outputPath = @"C:\Temp\out.csv";

            // 6️⃣ Save as CSV using the configured options
            workbook.Save(outputPath, SaveFormat.Csv, exportOptions);

            Console.WriteLine($"CSV file created at: {outputPath}");
        }
    }
}
```

Εκτελέστε το πρόγραμμα, έπειτα ανοίξτε το `C:\Temp\out.csv` στο Notepad ή το Excel. Θα πρέπει να δείτε την στρογγυλοποιημένη τιμή `12350`, επιβεβαιώνοντας ότι **export excel to CSV** με significant digits λειτουργεί όπως αναμένεται.

## Συμπέρασμα

Καλύψαμε όλα όσα χρειάζεστε για **create new workbook**, να το γεμίσετε, να ρυθμίσετε την ακρίβεια εξαγωγής, και τελικά **save workbook as CSV**. Τα βασικά σημεία:

- Χρησιμοποιήστε `ExportOptions` για να ελέγξετε τη μορφοποίηση αριθμών όταν *πώς να εξάγετε CSV*.
- Η μέθοδος `Save` με `SaveFormat.Csv` είναι ο πιο απλός τρόπος για **save file as CSV**.
- Προσαρμόστε τα διαχωριστικά, την ορατότητα ή τη ροή (stream) της εξόδου για προχωρημένα σενάρια.

### Τι Ακολουθεί;

- **Batch processing:** Επανάληψη πάνω σε μια συλλογή πινάκων δεδομένων και δημιουργία ξεχωριστών CSV σε μία εκτέλεση.
- **Custom formatting:** Συνδυάστε `NumberFormat` με `ExportOptions` για μορφές νομισμάτων ή ημερομηνιών.
- **Integration:** Σπρώξτε το CSV απευθείας στο Azure Blob Storage ή σε ένα S3 bucket χρησιμοποιώντας την υπερφόρτωση stream.

Μη διστάσετε να πειραματιστείτε με αυτές τις ιδέες, και αφήστε ένα σχόλιο αν αντιμετωπίσετε προβλήματα. Καλή προγραμματιστική, και εύχομαι οι εξαγωγές CSV σας πάντα να διατηρούν τον σωστό αριθμό significant digits! 

![Illustration of a C# workbook being saved as a CSV file – create new workbook](/images/create-new-workbook-csv.png "create new workbook illustration")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}