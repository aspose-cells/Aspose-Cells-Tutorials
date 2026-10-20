---
category: general
date: 2026-10-20
description: Αποθηκεύστε το βιβλίο εργασίας ως CSV με ακριβή δεκαδικά ψηφία, τιμές
  σε εισαγωγικά και μορφή ημερομηνίας ιαπωνικής εποχής χρησιμοποιώντας το Aspose.Cells
  για .NET.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save workbook as csv
- set excel number format
- export excel to csv
- quote csv values
language: el
lastmod: 2026-10-20
og_description: Αποθηκεύστε το βιβλίο εργασίας ως CSV με πλήρη έλεγχο των δεκαδικών,
  των εισαγωγικών και των ημερομηνιών ιαπωνικής εποχής. Ακολουθήστε αυτόν τον βήμα‑βήμα
  οδηγό C# χρησιμοποιώντας το Aspose.Cells.
og_image_alt: Screenshot illustrating how to save workbook as CSV with custom options
  in C#
og_title: Αποθήκευση βιβλίου εργασίας ως CSV – πλήρης οδηγός για προγραμματιστές C#
schemas:
- author: Aspose
  dateModified: '2026-10-20'
  description: Save workbook as CSV with precise decimal digits, quoted values and
    Japanese era date format using Aspose.Cells for .NET.
  headline: How to save workbook as CSV with custom formatting in C#
  type: TechArticle
tags:
- Aspose.Cells
- C#
- CSV export
- Excel formatting
title: Πώς να αποθηκεύσετε το βιβλίο εργασίας ως CSV με προσαρμοσμένη μορφοποίηση
  σε C#
url: /el/net/csv-file-handling/how-to-save-workbook-as-csv-with-custom-formatting-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να αποθηκεύσετε ένα βιβλίο εργασίας ως CSV με προσαρμοσμένη μορφοποίηση σε C#

Αν χρειάζεστε να **αποθηκεύσετε ένα βιβλίο εργασίας ως CSV** ελέγχοντας την ακρίβεια των δεκαδικών, την παράθεση τιμών και τη διαχείριση ημερομηνιών ιαπωνικής εποχής, αυτό το σεμινάριο σας δείχνει πώς με το Aspose.Cells για .NET. Θα μάθετε να **εξάγετε το Excel σε CSV**, **ορίζετε τη μορφή αριθμού του Excel**, και **παραθέτετε τιμές CSV** ώστε το αποτέλεσμα να ταιριάζει με τις τυπικές απαιτήσεις ανταλλαγής δεδομένων.

Ο οδηγός υποθέτει ότι έχετε περιβάλλον ανάπτυξης .NET (Visual Studio 2022 ή νεότερο) και έγκυρη άδεια Aspose.Cells. Δεν απαιτούνται πρόσθετα πακέτα NuGet πέρα από το `Aspose.Cells`.

## Προαπαιτούμενα

- .NET 6.0 SDK ή νεότερο  
- Aspose.Cells για .NET (εγκατεστημένο μέσω NuGet: `Install-Package Aspose.Cells`)  
- Ένα δείγμα αρχείου Excel (`Data.xlsx`) τοποθετημένο σε φάκελο που μπορείτε να αναφέρετε από τον κώδικα  

## Βήμα 1: Φόρτωση του πηγαίου βιβλίου εργασίας – η βάση για την αποθήκευση του βιβλίου εργασίας ως CSV

Αρχικά δημιουργείτε μια παρουσία `Workbook` που δείχνει στο αρχείο Excel που θέλετε να μετατρέψετε.

```csharp
using Aspose.Cells;
using System;

// Load the source workbook
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\Data.xlsx");
```

*Γιατί αυτό το βήμα είναι σημαντικό*: Το αντικείμενο `Workbook` περιέχει όλα τα φύλλα εργασίας, τα στυλ και τους τύπους. Όλες οι επόμενες λειτουργίες CSV λειτουργούν πάνω σε αυτήν την αναπαράσταση στη μνήμη.

## Βήμα 2: Περιορισμός της ακρίβειας των δεκαδικών όταν αποθηκεύετε το βιβλίο εργασίας ως CSV

Όταν χρειάζεστε ακριβώς τέσσερα ψηφία μετά το δεκαδικό σημείο, διαμορφώστε το `CsvSaveOptions`.

```csharp
// Configure CSV saving options
CsvSaveOptions csvOptions = new CsvSaveOptions
{
    // Keep 4 digits after the decimal point
    SignificantDigits = 4
};

// Save the workbook as CSV with the defined precision
workbook.Save(@"YOUR_DIRECTORY\Data_Sig4.csv", csvOptions);
```

*Κύριο σημείο*: Το `SignificantDigits` στρογγυλοποιεί κάθε αριθμητικό κελί στον καθορισμένο αριθμό δεκαδικών θέσεων πριν την εγγραφή του αρχείου CSV. Αυτό αποτρέπει το θόρυβο κινητής υποδιαστολής σε συστήματα που λαμβάνουν τα δεδομένα.

## Βήμα 3: Εξαγωγή Excel σε CSV με παρατιθέμενες τιμές

Ορισμένοι επεξεργαστές που λαμβάνουν τα δεδομένα απαιτούν κάθε πεδίο να είναι περιτυλιγμένο σε διπλά εισαγωγικά, ειδικά όταν οι τιμές περιέχουν κόμματα ή αλλαγές γραμμής. Η κλάση `ExportTableOptions` σας επιτρέπει να αντιμετωπίζετε κάθε κελί ως συμβολοσειρά και να εφαρμόζετε προσαρμοσμένη παράθεση.

```csharp
// Prepare export options that treat every cell as a string
ExportTableOptions tableOptions = new ExportTableOptions
{
    ExportAsString = true, // Force string export for all cells
    // Custom delegate to wrap each value in double quotes
    CustomExport = (cell, writer) =>
    {
        writer.Write('"' + cell.StringValue + '"');
    }
};

// Export the first worksheet as a CSV file with quoted values
workbook.Save(@"YOUR_DIRECTORY\TableExport.csv", tableOptions);
```

*Γιατί πρέπει να παραθέτετε τις τιμές*: Η παράθεση προστατεύει τα κόμματα, τις αλλαγές γραμμής και τα κενά στην αρχή/τέλος από το να ερμηνευτούν ως διαχωριστικά, κάτι που είναι ουσιώδες για αξιόπιστη εισαγωγή δεδομένων.

## Βήμα 4: Ορισμός μορφής αριθμού Excel για ημερομηνίες ιαπωνικής εποχής

Το Excel μπορεί να αποθηκεύει ημερομηνίες χρησιμοποιώντας ημερολόγια συγκεκριμένων εποχών. Για να το δείξουμε, εισάγετε μια συμβολοσειρά ημερομηνίας ιαπωνικής εποχής και εφαρμόστε την κατάλληλη μορφή αριθμού.

```csharp
// Create a new workbook for the era‑date example
Workbook eraWorkbook = new Workbook();
Worksheet sheet = eraWorkbook.Worksheets[0];

// Insert a Japanese‑era date string (Reiwa 3‑04‑01)
sheet.Cells["A1"].PutValue("R3-04-01");

// Apply the Japanese locale number format
sheet.Cells["A1"].SetNumberFormat("[$-ja-JP]yyyy-mm-dd");

// Retrieve the parsed DateTime value
DateTime parsedDate = sheet.Cells["A1"].GetDateTime();
Console.WriteLine(parsedDate); // Outputs: 2021-04-01
```

*Εξήγηση*: Η κλήση `SetNumberFormat` ενημερώνει το Aspose.Cells να ερμηνεύσει τη συμβολοσειρά χρησιμοποιώντας το ιαπωνικό ημερολόγιο. Όταν καλείτε το `GetDateTime()`, η βιβλιοθήκη μετατρέπει αυτόματα τη σημειογραφία εποχής στην ημερομηνία Γρηγοριανού.

## Βήμα 5: Επαλήθευση των παραγόμενων αρχείων CSV

Μετά την εκτέλεση του κώδικα, θα πρέπει να δείτε τρία αρχεία στο `YOUR_DIRECTORY`:

| Όνομα αρχείου            | Σημεία κλειδιά |
|--------------------------|----------------|
| `Data_Sig4.csv`          | Αριθμοί στρογγυλοποιημένοι σε 4 δεκαδικά ψηφία |
| `TableExport.csv`        | Κάθε κελί περιτυλιγμένο σε διπλά εισαγωγικά |
| `Data.xlsx` (αμετάβλητο) | Δείχνει διαχείριση ημερομηνιών ιαπωνικής εποχής (δείτε στο Excel) |

Ανοίξτε το `Data_Sig4.csv` σε έναν επεξεργαστή απλού κειμένου για να επιβεβαιώσετε την ακρίβεια, και ανοίξτε το `TableExport.csv` για να δείτε τις παρατιθέμενες τιμές, π.χ.:

```
"Name","Score","Comment"
"Alice","95.1234","Excellent"
"Bob","88.0000","Good"
```

Η έξοδος της κονσόλας για την ημερομηνία εποχής θα είναι:

```
2021-04-01 00:00:00
```

## Συνηθισμένα προβλήματα και πώς να τα αποφύγετε

- **Διαχωριστές δεκαδικών εξαρτημένες από την τοπική ρύθμιση**: Το `CsvSaveOptions` σέβεται την τρέχουσα πολιτισμική ρύθμιση. Αν χρειάζεστε τελεία (`.`) ως διαχωριστικό ανεξάρτητα από την τοπική ρύθμιση, ορίστε `csvOptions.Separator = ',';`.
- **Μεγάλα φύλλα εργασίας**: Η εξαγωγή ενός βιβλίου εργασίας με εκατομμύρια γραμμές μπορεί να καταναλώσει σημαντική μνήμη. Χρησιμοποιήστε `ExportTableOptions.StartRow` και `EndRow` για να περιορίσετε το εύρος εξαγωγής.
- **Ειδικοί χαρακτήρες μέσα σε συμβολοσειρές**: Ο προσαρμοσμένος συγγραφέας στο Βήμα 3 προσθέτει μόνο τα περιβάλλοντα εισαγωγικά. Αν ένα κελί περιέχει ήδη εισαγωγικό, διπλασιάστε το (`""`) για να διατηρήσετε την εγκυρότητα του CSV.

## Συμβουλή επαγγελματία: Συνδυάστε επιλογές για μέγιστο έλεγχο

Μπορείτε να συνδυάσετε το `CsvSaveOptions` και το `ExportTableOptions` πρώτα μετατρέποντας το βιβλίο εργασίας σε `MemoryStream` με ένα σύνολο επιλογών, έπειτα γράφοντας το ρεύμα στο δίσκο με άλλο. Αυτή η προσέγγιση σας επιτρέπει, για παράδειγμα, να εφαρμόσετε τόσο στρογγυλοποίηση δεκαδικών **και** παράθεση σε μία μόνο διαδικασία:

```csharp
using (MemoryStream ms = new MemoryStream())
{
    // Apply rounding
    workbook.Save(ms, csvOptions);
    ms.Position = 0; // Reset stream

    // Load the intermediate CSV into a new workbook for quoting
    Workbook temp = new Workbook(ms, new LoadOptions(LoadFormat.Csv));
    temp.Save(@"YOUR_DIRECTORY\RoundedAndQuoted.csv", tableOptions);
}
```

## Συμπέρασμα

Τώρα γνωρίζετε πώς να **αποθηκεύσετε ένα βιβλίο εργασίας ως CSV** με ακριβή διαχείριση δεκαδικών, παρατιθέμενες τιμές και προσαρμοσμένη μορφοποίηση ημερομηνιών. Η πλήρης λύση καλύπτει τη φόρτωση ενός βιβλίου εργασίας, τη διαμόρφωση του `CsvSaveOptions`, τη χρήση του `ExportTableOptions` για **παράθεση τιμών CSV**, και την εφαρμογή **ορισμού μορφής αριθμού Excel** για ημερομηνίες ιαπωνικής εποχής. Από εδώ μπορείτε να εξερευνήσετε πρόσθετες επιλογές όπως προσαρμοσμένα διαχωριστικά, διαφορετικές κωδικοποιήσεις ή εξαγωγή επιλεγμένων φύλλων εργασίας.

---

*Επόμενα βήματα*  
- Εξερευνήστε το `CsvSaveOptions.Encoding` για να γράψετε αρχεία UTF‑8 BOM ή UTF‑16.  
- Χρησιμοποιήστε το `ExportTableOptions.StartColumn` / `EndColumn` για να εξάγετε μόνο ένα υποσύνολο στηλών.  
- Συνδυάστε αυτές τις τεχνικές με το `DataFormatter` του Aspose.Cells για μορφοποίηση αριθμών με γνώμονα την τοπική ρύθμιση.  

Καλή προγραμματιστική!

## Τι Θα Πρέπει Να Μάθετε Στη Σύντομη Μελλοντική

Τα παρακάτω σεμινάρια καλύπτουν στενά σχετικούς τομείς που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Αποθήκευση βιβλίου εργασίας ως CSV – Πλήρης Οδηγός για Εξαγωγή Excel σε CSV με Ελεγχόμενη](/cells/english/net/csv-file-handling/save-workbook-as-csv-complete-guide-to-export-excel-to-csv-w/)
- [Αποθήκευση βιβλίου εργασίας ως CSV σε C# – Εξαγωγή Excel σε CSV](/cells/english/net/csv-file-handling/save-workbook-as-csv-in-c-export-excel-to-csv/)
- [Δημιουργία και Αποθήκευση βιβλίου εργασίας Excel ως PDF σε ASP.NET χρησιμοποιώντας Aspose.Cells](/cells/english/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}