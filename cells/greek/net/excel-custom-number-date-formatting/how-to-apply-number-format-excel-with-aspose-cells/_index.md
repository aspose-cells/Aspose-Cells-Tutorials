---
category: general
date: 2026-10-10
description: Εφαρμόστε γρήγορα μορφοποίηση αριθμών στο Excel εισάγοντας έναν DataTable,
  ορίζοντας μορφές ημερομηνίας και νομίσματος, και διατηρώντας τη γραμμή κεφαλίδας
  σε ένα μόνο βήμα.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- apply number format excel
- set date format excel
- format excel cells date
- set currency format excel
- preserve header row excel
language: el
lastmod: 2026-10-10
og_description: Εφαρμόστε μορφοποίηση αριθμών στο Excel με C# χρησιμοποιώντας το Aspose.Cells.
  Μάθετε πώς να ορίζετε μορφή ημερομηνίας στο Excel, μορφή νομίσματος στο Excel και
  να διατηρείτε τη γραμμή κεφαλίδας στο Excel κατά την εισαγωγή ενός DataTable.
og_image_alt: Excel worksheet showing currency and date columns formatted after import
og_title: Εφαρμογή μορφοποίησης αριθμών στο Excel με C# – οδηγός βήμα‑προς‑βήμα
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: apply number format excel quickly by importing a DataTable, setting
    date and currency formats, and preserving header row excel in a single step.
  headline: How to apply number format excel with Aspose.Cells
  type: TechArticle
tags:
- excel
- aspnet
- csharp
- excel-formatting
title: Πώς να εφαρμόσετε μορφή αριθμού στο Excel με το Aspose.Cells
url: /el/net/excel-custom-number-date-formatting/how-to-apply-number-format-excel-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να εφαρμόσετε μορφή αριθμού στο Excel με Aspose.Cells

Αν χρειάζεστε να **εφαρμόσετε μορφή αριθμού στο Excel** κατά τη φόρτωση δεδομένων από ένα `DataTable`, αυτός ο οδηγός σας δείχνει ακριβώς πώς. Θα μάθετε επίσης πώς να **ορίσετε μορφή ημερομηνίας στο Excel**, **ορίσετε μορφή νομίσματος στο Excel**, και **διατηρήσετε τη γραμμή κεφαλίδας στο Excel** κατά την εισαγωγή, ώστε το τελικό φύλλο εργασίας να φαίνεται επαγγελματικό χωρίς επιπλέον επεξεργασία.

Θα καλύψουμε τα πάντα, από την εγκατάσταση της βιβλιοθήκης μέχρι τη συγγραφή ενός πλήρους, εκτελέσιμου αποσπάσματος κώδικα. Στο τέλος θα μπορείτε να εισάγετε οποιοδήποτε `DataTable` σε ένα βιβλίο εργασίας Excel, να μορφοποιείτε αυτόματα τις αριθμητικές στήλες και να διατηρείτε τη γραμμή κεφαλίδας αμετάβλητη — όλα με λίγες μόνο γραμμές C#.

## Προαπαιτούμενα

* .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί επίσης με .NET Framework 4.6+)
* Visual Studio 2022 (ή οποιοδήποτε IDE C# προτιμάτε)
* **Aspose.Cells for .NET** – εγκατάσταση μέσω NuGet:

```bash
dotnet add package Aspose.Cells
```

* Μια πηγή `DataTable` – το παράδειγμα χρησιμοποιεί μια βοηθητική μέθοδο `GetTable()` που επιστρέφει δείγμα δεδομένων.

> **Pro tip:** Το Aspose.Cells είναι εμπορική βιβλιοθήκη, αλλά προσφέρει δωρεάν λειτουργία αξιολόγησης που απενεργοποιεί το υδατογράφημα για έως και 30 ημέρες.

## Βήμα 1: Δημιουργία βιβλίου εργασίας και πρόσβαση στο πρώτο φύλλο εργασίας

Το αντικείμενο workbook είναι το σημείο εισόδου για όλες τις λειτουργίες του Excel. Η δημιουργία ενός νέου βιβλίου εργασίας σας παρέχει ένα προεπιλεγμένο φύλλο εργασίας στο δείκτη 0.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class Program
{
    static void Main()
    {
        // Create a new workbook
        Workbook wb = new Workbook();

        // Obtain reference to the first worksheet
        Worksheet sheet = wb.Worksheets[0];
```

*Γιατί αυτό το βήμα;*  
`Workbook` διαχειρίζεται τη μορφή αρχείου, τη μηχανή υπολογισμών και το αποθετήριο στυλ. Η πρόσβαση στο `Worksheet` νωρίς μας επιτρέπει να περάσουμε το στόχο φύλλου στη μέθοδο εισαγωγής αργότερα.

## Βήμα 2: Ανάκτηση των πηγαίων δεδομένων ως DataTable

Σε πραγματικά έργα, τα δεδομένα συχνά προέρχονται από ερώτημα βάσης δεδομένων, αναλυτή CSV ή απόκριση API. Για παράδειγμα, δημιουργούμε ένα απλό `DataTable` με τρεις στήλες: **Product**, **Price**, και **ReleaseDate**.

```csharp
        // Step 2: Retrieve the source data as a DataTable
        DataTable sourceTable = GetTable();
```

```csharp
        // Helper method that builds a sample DataTable
        static DataTable GetTable()
        {
            DataTable dt = new DataTable();
            dt.Columns.Add("Product", typeof(string));
            dt.Columns.Add("Price", typeof(decimal));
            dt.Columns.Add("ReleaseDate", typeof(DateTime));

            dt.Rows.Add("Widget A", 12.99m, new DateTime(2023, 5, 1));
            dt.Rows.Add("Widget B", 23.50m, new DateTime(2023, 6, 15));
            dt.Rows.Add("Widget C", 7.75m, new DateTime(2023, 7, 30));
            return dt;
        }
```

*Γιατί αυτό το βήμα;*  
Ένα `DataTable` παρέχει μια πινάκωση αναπαράστασης στη μνήμη που το Aspose.Cells μπορεί να εισάγει απευθείας, διατηρώντας τη σειρά των στηλών και τους τύπους δεδομένων.

## Βήμα 3: Προετοιμασία πίνακα `Style` – ένα στυλ ανά στήλη

Το Aspose.Cells σας επιτρέπει να εφαρμόζετε διαφορετικό στυλ σε κάθε στήλη κατά την εισαγωγή, περνώντας έναν πίνακα αντικειμένων `Style`. Το μήκος του πίνακα πρέπει να ταιριάζει με τον αριθμό των στηλών στον πηγαίο πίνακα.

```csharp
        // Step 3: Prepare an array of Style objects – one for each column
        Style[] columnStyles = new Style[sourceTable.Columns.Count];
        for (int i = 0; i < columnStyles.Length; i++)
        {
            // Each entry must be instantiated before we can set properties
            columnStyles[i] = wb.CreateStyle();
        }
```

*Γιατί αυτό το βήμα;*  
Αν παραλείψετε τη ρητή δημιουργία (`CreateStyle()`), η προσπάθεια ορισμού του `Number` θα προκαλέσει `NullReferenceException`. Η αρχικοποίηση κάθε `Style` εξασφαλίζει ότι οι επόμενες εκχωρήσεις θα επιτύχουν.

## Βήμα 4: Ανάθεση μορφών αριθμού – νόμισμα και ημερομηνία

Το Excel αναγνωρίζει ενσωματωμένες μορφές αριθμού με βάση το ID.  
* **14** – Νόμισμα (π.χ., `$1,234.00`)  
* **22** – Σύντομη ημερομηνία (`mm/dd/yyyy`)

```csharp
        // Step 4: Assign number formats to the desired columns
        // Column 0 – Product name (no format needed)
        // Column 1 – Currency format (Number format ID 14)
        columnStyles[1].Number = 14;   // set currency format excel

        // Column 2 – Date format (Number format ID 22)
        columnStyles[2].Number = 22;   // set date format excel
```

> **Σημείωση:** Αν χρειάζεστε προσαρμοσμένη μορφή (π.χ., `"¥#,##0.00"`), χρησιμοποιήστε `Style.Custom = "¥#,##0.00"` αντί για ενσωματωμένο ID.

*Γιατί αυτό το βήμα;*  
Η εφαρμογή της σωστής **μορφής αριθμού** κατά τη στιγμή της εισαγωγής εξαλείφει την ανάγκη για δεύτερο πέρασμα που θα διατρέχει τα κελιά για αλλαγή μορφοποίησης. Επίσης εγγυάται ότι το **format excel cells date** και το **set currency format excel** είναι συνεπή σε όλες τις γραμμές.

## Βήμα 5: Εισαγωγή του DataTable διατηρώντας τη γραμμή κεφαλίδας

Η μέθοδος `ImportDataTable` μπορεί να αντιγράψει δεδομένα, να διατηρήσει την πρώτη γραμμή ως κεφαλίδα και να εφαρμόσει τα στυλ στηλών που προετοιμάσαμε.

```csharp
        // Step 5: Import the DataTable into the worksheet
        // Parameters:
        //   sourceTable – the DataTable to import
        //   true        – preserve the header row (preserve header row excel)
        //   "A1"        – start cell
        //   columnStyles – array of styles for each column
        sheet.Cells.ImportDataTable(sourceTable, true, "A1", columnStyles);
```

```csharp
        // Save the workbook to disk
        wb.Save("FormattedReport.xlsx");
        Console.WriteLine("Workbook created successfully.");
    }
}
```

**Αναμενόμενο αποτέλεσμα** – Ανοίξτε το `FormattedReport.xlsx` και θα δείτε:

| Προϊόν | Τιμή (νόμισμα) | Ημερομηνία (ημερομηνία) |
|--------|----------------|--------------------------|
| Widget A| $12.99         | 05/01/2023               |
| Widget B| $23.50         | 06/15/2023               |
| Widget C| $7.75          | 07/30/2023               |

Η γραμμή κεφαλίδας παραμένει αμετάβλητη, η στήλη **Price** εμφανίζει το σύμβολο του νομίσματος, και η στήλη **ReleaseDate** δείχνει σύντομη μορφή ημερομηνίας — όλα χωρίς επιπλέον κώδικα μορφοποίησης.

### Διαχείριση κοινών περιπτώσεων άκρων

| Κατάσταση                               | Λύση |
|----------------------------------------|----------|
| **Περισσότερες στήλες από στυλ**           | Βεβαιωθείτε ότι το `columnStyles.Length` ισούται με το `sourceTable.Columns.Count`. Τα ελλιπή στοιχεία χρησιμοποιούν το προεπιλεγμένο στυλ του βιβλίου εργασίας. |
| **Τιμές null σε αριθμητικές στήλες**     | Το Excel θεωρεί το `null` ως κενό κελί· η μορφή αριθμού παραμένει εφαρμόσιμη όταν εισαχθεί τιμή αργότερα. |
| **Προσαρμοσμένο νόμισμα ανά τοπική ρύθμιση**    | Χρησιμοποιήστε `columnStyles[i].Custom = "\"€\"#,##0.00"` και ορίστε `columnStyles[i].Number = -1` για να απενεργοποιήσετε το ενσωματωμένο ID. |
| **Μεγάλοι πίνακες ( > 100 000 γραμμές )**    | Σκεφτείτε να χρησιμοποιήσετε την υπερφόρτωση `ImportDataTable` με `ImportTableOptions` για ροή δεδομένων και μείωση της πίεσης μνήμης. |
| **Εφαρμογή του ίδιου στυλ σε πολλές στήλες** | Επαναχρησιμοποιήστε το ίδιο αντικείμενο `Style` στον πίνακα (π.χ., `columnStyles[1] = columnStyles[2] = dateStyle;`). |

## Bonus: Χρήση προσαρμοσμένης συμβολοσειράς μορφής

Αν τα ενσωματωμένα IDs δεν καλύπτουν τις ανάγκες σας, μπορείτε να ορίσετε προσαρμοσμένη μορφή αριθμού:

```csharp
// Example: display Euro currency with no decimal places
Style euroStyle = wb.CreateStyle();
euroStyle.Custom = "\"€\"#,##0";
columnStyles[1] = euroStyle;   // replace the built‑in currency style
```

Αυτή η προσέγγιση σας δίνει πλήρη έλεγχο πάνω στο **format excel cells date** και το **set currency format excel** πέρα από τα προκαθορισμένα IDs.

## Συμπέρασμα

Τώρα γνωρίζετε πώς να **εφαρμόσετε μορφή αριθμού στο Excel** αποδοτικά κατά την εισαγωγή ενός `DataTable` με το Aspose.Cells. Δημιουργώντας έναν πίνακα `Style` ανά στήλη, ορίζοντας ενσωματωμένα ή προσαρμοσμένα IDs αριθμού, και χρησιμοποιώντας την υπερφόρτωση `ImportDataTable` που **διατηρεί τη γραμμή κεφαλίδας στο Excel**, μπορείτε να δημιουργήσετε φύλλα εργασίας έτοιμα για δημοσίευση με μια μόνο ενέργεια.

### Τι θα ακολουθήσει;

* Εξερευνήστε το **set date format excel** με προσαρμοσμένα μοτίβα όπως `"dddd, mmmm dd, yyyy"`.
* Συνδυάστε αυτήν την τεχνική με **conditional formatting** για να επισημάνετε τιμές εκτός εύρους.
* Χρησιμοποιήστε το **format excel cells date** σε συγκεντρωτικούς πίνακες ή γραφήματα για δυναμική αναφορά.

Μη διστάσετε να πειραματιστείτε με διαφορετικά IDs αριθμού ή προσαρμοσμένες συμβολοσειρές ώστε να ταιριάζουν με το στυλ του οργανισμού σας. Καλή προγραμματιστική!

## Τι Θα Πρέπει Να Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετικές θεματικές που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [εφαρμογή μορφής αριθμού excel – Οδηγός βήμα‑βήμα για τη μορφοποίηση στηλών](/cells/english/net/number-and-display-formats-in-excel/apply-number-format-excel-step-by-step-guide-to-formatting-c/)
- [Δημιουργία βιβλίου εργασίας Excel C# – Εφαρμογή μορφής νομίσματος και εισαγωγή DataTable](/cells/english/net/excel-data-import-export/create-excel-workbook-c-apply-currency-format-and-import-dat/)
- [Ορισμός μορφής ημερομηνίας στο Excel με C# – Πλήρης οδηγός μορφοποίησης εισαγωγής](/cells/english/net/excel-custom-number-date-formatting/set-date-format-in-excel-with-c-full-import-formatting-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}