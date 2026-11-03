---
category: general
date: 2026-10-01
description: Μάθετε πώς να προσθέτετε προσαρμοσμένες ιδιότητες σε ένα βιβλίο εργασίας
  Excel χρησιμοποιώντας το Aspose.Cells. Αυτός ο οδηγός δείχνει επίσης πώς να προσθέσετε
  το αναγνωριστικό του έργου και να διαβάσετε προσαρμοσμένες ιδιότητες.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add custom properties
- how to add custom
- excel custom properties
- add project id
- read custom properties
language: el
lastmod: 2026-10-01
og_description: Προσθέστε προσαρμοσμένες ιδιότητες σε ένα βιβλίο εργασίας Excel με
  το Aspose.Cells. Ακολουθήστε αυτό το πλήρες σεμινάριο για να προσθέσετε ένα αναγνωριστικό
  έργου, να ορίσετε πληροφορίες αξιολογητή και να διαβάσετε προσαρμοσμένες ιδιότητες
  προγραμματιστικά.
og_image_alt: Screenshot of an Excel worksheet displaying custom properties added
  via Aspose.Cells
og_title: Προσθήκη προσαρμοσμένων ιδιοτήτων σε βιβλίο εργασίας Excel – βήμα‑βήμα οδηγός
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to add custom properties to an Excel workbook using Aspose.Cells.
    This guide also shows how to add project ID and read custom properties.
  headline: How to add custom properties to an Excel workbook
  type: TechArticle
- description: Learn how to add custom properties to an Excel workbook using Aspose.Cells.
    This guide also shows how to add project ID and read custom properties.
  name: How to add custom properties to an Excel workbook
  steps:
  - name: Open the saved `DataWithProps.xlsb` file in Microsoft Excel.
    text: Open the saved `DataWithProps.xlsb` file in Microsoft Excel.
  - name: Go to **File → Info → Properties → Advanced Properties**.
    text: Go to **File → Info → Properties → Advanced Properties**.
  - name: Select the **Custom** tab.
    text: Select the **Custom** tab.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Πώς να προσθέσετε προσαρμοσμένες ιδιότητες σε ένα βιβλίο εργασίας του Excel
url: /el/net/document-properties/how-to-add-custom-properties-to-an-excel-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να προσθέσετε προσαρμοσμένες ιδιότητες σε ένα βιβλίο εργασίας Excel

Αν χρειάζεται να **προσθέσετε προσαρμοσμένες ιδιότητες** σε ένα βιβλίο εργασίας Excel, αυτός ο οδηγός σας δείχνει ακριβώς πώς να το κάνετε με το Aspose.Cells for .NET. Θα μάθετε επίσης πώς να προσθέσετε ένα ID έργου, να ορίσετε το όνομα του ελεγκτή και, αργότερα, **να διαβάσετε τις προσαρμοσμένες ιδιότητες** από το αρχείο.

Η εργασία με προσαρμοσμένα μεταδεδομένα σας επιτρέπει να ενσωματώσετε επιχειρηματικές πληροφορίες απευθείας μέσα στο φύλλο εργασίας, καθιστώντας εύκολο τον εντοπισμό ιδιοκτησίας, έκδοσης ή οποιουδήποτε άλλου πλαισίου χωρίς να διατηρείτε ξεχωριστή βάση δεδομένων. Τα παρακάτω βήματα καλύπτουν τη πλήρη ροή εργασίας από τη δημιουργία του βιβλίου εργασίας μέχρι την αποθήκευση των νέων ιδιοτήτων.

## Προαπαιτούμενα

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

* .NET 6.0 ή νεότερη έκδοση εγκατεστημένη  
* Ένα έγκυρο license του Aspose.Cells for .NET (ή δωρεάν δοκιμή)  
* Visual Studio 2022 (ή οποιοδήποτε IDE για C#)  

Δεν απαιτούνται πρόσθετα πακέτα NuGet εκτός του `Aspose.Cells`.

## Βήμα 1: Ρύθμιση του έργου και εισαγωγή namespaces

Δημιουργήστε μια νέα εφαρμογή console και προσθέστε την αναφορά στο Aspose.Cells:

```csharp
using System;
using Aspose.Cells;

namespace ExcelCustomPropertiesDemo
{
    class Program
    {
        static void Main()
        {
            // The rest of the code lives here
        }
    }
}
```

Το namespace `Aspose.Cells` περιέχει τις κλάσεις `Workbook`, `Worksheet` και `CustomPropertyCollection` που θα χρησιμοποιήσουμε.

## Βήμα 2: Φόρτωση υπάρχοντος βιβλίου εργασίας (ή δημιουργία νέου)

Μπορείτε να ξεκινήσετε με ένα υπάρχον αρχείο `.xlsb` ή να δημιουργήσετε ένα νέο βιβλίο εργασίας. Το παρακάτω παράδειγμα φορτώνει ένα αρχείο με όνομα **Data.xlsb** που βρίσκεται σε φάκελο `YOUR_DIRECTORY`.

```csharp
// Load the existing workbook
var workbookPath = @"YOUR_DIRECTORY\Data.xlsb";
var workbook = new Workbook(workbookPath);
```

Αν το αρχείο δεν υπάρχει, αντικαταστήστε τον κώδικα με `new Workbook();` για να δημιουργήσετε ένα κενό βιβλίο εργασίας.

## Βήμα 3: Προσθήκη προσαρμοσμένων ιδιοτήτων στο πρώτο φύλλο εργασίας

Η κύρια ενέργεια είναι η **προσθήκη προσαρμοσμένων ιδιοτήτων** σε ένα φύλλο εργασίας. Το Aspose.Cells αποθηκεύει τις προσαρμοσμένες ιδιότητες σε μια συλλογή που συμπεριφέρεται όπως ένα λεξικό.

```csharp
// Get the first worksheet (index 0)
var worksheet = workbook.Worksheets[0];

// Add a numeric ProjectId property
worksheet.CustomProperties.Add("ProjectId", 12345);

// Add a string Reviewer property
worksheet.CustomProperties.Add("Reviewer", "John Doe");

// Optional: add a DateTime property for the creation timestamp
worksheet.CustomProperties.Add("CreatedOn", DateTime.UtcNow);
```

Ο λόγος που χρησιμοποιούμε `CustomProperties.Add` αντί για `CustomProperties["Name"] = value` είναι ότι η μέθοδος `Add` δημιουργεί την καταχώρηση αν δεν υπάρχει και εγγυάται ότι αποθηκεύεται ο σωστός τύπος δεδομένων. Αυτή η προσέγγιση αποτρέπει τυχαίες ασυμφωνίες τύπων που θα μπορούσαν να προκαλέσουν σφάλματα χρόνου εκτέλεσης κατά την ανάγνωση των τιμών αργότερα.

## Βήμα 4: Αποθήκευση του βιβλίου εργασίας με τις νέες ιδιότητες

Αφού ενσωματώσετε τα μεταδεδομένα, αποθηκεύστε τις αλλαγές σε νέο αρχείο ώστε το αρχικό να παραμείνει αμετάβλητο.

```csharp
// Save the workbook with the custom properties
var outputPath = @"YOUR_DIRECTORY\DataWithProps.xlsb";
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

Σε αυτό το σημείο το αρχείο Excel περιέχει τα προσαρμοσμένα μεταδεδομένα που ορίσατε. Μπορείτε να επαληθεύσετε τις ιδιότητες ακολουθώντας τα βήματα στην επόμενη ενότητα.

## Βήμα 5: Ανάγνωση προσαρμοσμένων ιδιοτήτων από ένα βιβλίο εργασίας

Η ανάγνωση **excel custom properties** ακολουθεί το ίδιο πρότυπο συλλογής. Το παρακάτω απόσπασμα δείχνει πώς να ανακτήσετε τις τιμές που μόλις αποθηκεύσατε.

```csharp
// Load the workbook that contains custom properties
var loadedWorkbook = new Workbook(outputPath);
var loadedWorksheet = loadedWorkbook.Worksheets[0];
var props = loadedWorksheet.CustomProperties;

// Retrieve each property safely
int projectId = props["ProjectId"] != null ? (int)props["ProjectId"].Value : -1;
string reviewer = props["Reviewer"] != null ? props["Reviewer"].Value.ToString() : "Unknown";
DateTime createdOn = props["CreatedOn"] != null ? (DateTime)props["CreatedOn"].Value : DateTime.MinValue;

Console.WriteLine($"ProjectId: {projectId}");
Console.WriteLine($"Reviewer: {reviewer}");
Console.WriteLine($"CreatedOn (UTC): {createdOn:u}");
```

Ο δείκτης `CustomPropertyCollection` επιστρέφει ένα αντικείμενο `CustomProperty`; η πρόσβαση στην ιδιότητα `Value` σας δίνει τα αποθηκευμένα δεδομένα στον αρχικό τους τύπο. Ο έλεγχος για `null` πριν από την μετατροπή αποτρέπει `NullReferenceException` αν λείπει κάποια ιδιότητα.

### Αναμενόμενη έξοδος κονσόλας

```
ProjectId: 12345
Reviewer: John Doe
CreatedOn (UTC): 2026-10-01 12:34:56Z
```

Η χρονική σήμανση θα αντανακλά την ακριβή στιγμή που κλήθηκε η `Add` στο βήμα 3.

## Συμβουλή: Ενημέρωση υπάρχουσας προσαρμοσμένης ιδιότητας

Αν χρειάζεται να **προσθέσετε προσαρμοσμένες** πληροφορίες αργότερα (π.χ. να αλλάξετε τον ελεγκτή), χρησιμοποιήστε τον setter της `CustomPropertyCollection`:

```csharp
// Change the reviewer name
if (props["Reviewer"] != null)
{
    props["Reviewer"].Value = "Jane Smith";
}
else
{
    // Property does not exist; add it
    props.Add("Reviewer", "Jane Smith");
}
```

Αυτό το πρότυπο εξασφαλίζει ότι η ιδιότητα είτε ενημερώνεται είτε δημιουργείται, κάτι που είναι χρήσιμο σε επαναληπτικές ροές εργασίας όπως η αυτόματη δημιουργία αναφορών.

## Βήμα 6: Επαλήθευση των ιδιοτήτων μέσα στο Excel (προαιρετικό)

Μπορείτε επίσης να δείτε τις προσαρμοσμένες ιδιότητες απευθείας στο Excel:

1. Ανοίξτε το αποθηκευμένο αρχείο `DataWithProps.xlsb` στο Microsoft Excel.  
2. Μεταβείτε σε **File → Info → Properties → Advanced Properties**.  
3. Επιλέξτε την καρτέλα **Custom**.  

Θα δείτε τις καταχωρήσεις `ProjectId`, `Reviewer` και `CreatedOn` με τις αντίστοιχες τιμές τους.

## Πλήρες παράδειγμα λειτουργίας

Παρακάτω βρίσκεται το πλήρες, αυτόνομο πρόγραμμα που συνδυάζει όλα τα προηγούμενα αποσπάσματα. Αντιγράψτε το στο `Program.cs` και τρέξτε το· η κονσόλα θα εμφανίσει τις ανακτημένες τιμές.

```csharp
using System;
using Aspose.Cells;

namespace ExcelCustomPropertiesDemo
{
    class Program
    {
        static void Main()
        {
            // Paths (adjust to your environment)
            var sourcePath = @"YOUR_DIRECTORY\Data.xlsb";
            var resultPath = @"YOUR_DIRECTORY\DataWithProps.xlsb";

            // Load or create workbook
            var workbook = new Workbook(sourcePath);
            var worksheet = workbook.Worksheets[0];

            // Add custom properties
            worksheet.CustomProperties.Add("ProjectId", 12345);
            worksheet.CustomProperties.Add("Reviewer", "John Doe");
            worksheet.CustomProperties.Add("CreatedOn", DateTime.UtcNow);

            // Save the workbook
            workbook.Save(resultPath);
            Console.WriteLine($"Saved workbook with custom properties to {resultPath}");

            // Load the saved workbook to read properties
            var loadedWorkbook = new Workbook(resultPath);
            var loadedWorksheet = loadedWorkbook.Worksheets[0];
            var props = loadedWorksheet.CustomProperties;

            // Read properties
            int projectId = props["ProjectId"] != null ? (int)props["ProjectId"].Value : -1;
            string reviewer = props["Reviewer"] != null ? props["Reviewer"].Value.ToString() : "Unknown";
            DateTime createdOn = props["CreatedOn"] != null ? (DateTime)props["CreatedOn"].Value : DateTime.MinValue;

            Console.WriteLine($"ProjectId: {projectId}");
            Console.WriteLine($"Reviewer: {reviewer}");
            Console.WriteLine($"CreatedOn (UTC): {createdOn:u}");
        }
    }
}
```

Η εκτέλεση αυτού του προγράμματος παράγει την έξοδο κονσόλας που εμφανίστηκε νωρίτερα και δημιουργεί το `DataWithProps.xlsb` που περιέχει τα ενσωματωμένα μεταδεδομένα.

## Συχνές ερωτήσεις και ειδικές περιπτώσεις

| Ερώτηση | Απάντηση |
|---|---|
| **Μπορώ να αποθηκεύσω μη‑πρωτότυπους τύπους;** | Το Aspose.Cells υποστηρίζει `string`, `int`, `double`, `DateTime` και `bool`. Για σύνθετα αντικείμενα, σειριοποιήστε τα σε JSON ή XML πρώτα και αποθηκεύστε το ως string. |
| **Τι γίνεται αν το βιβλίο εργασίας είναι προστατευμένο με κωδικό;** | Ανοίξτε το βιβλίο εργασίας με κωδικό (`new Workbook(path, password)`) πριν αποκτήσετε πρόσβαση στις `CustomProperties`. Οι ιδιότητες παραμένουν προσβάσιμες μετά την αποκρυπτογράφηση. |
| **Διατηρούνται οι προσαρμοσμένες ιδιότητες μετά τη μετατροπή μορφής;** | Κατά την αποθήκευση σε διαφορετική μορφή (π.χ. `.xlsx`), το Aspose.Cells διατηρεί τις προσαρμοσμένες ιδιότητες εφόσον η μορφή-στόχος τις υποστηρίζει. |
| **Πώς διαγράφεται μια προσαρμοσμένη ιδιότητα;** | Χρησιμοποιήστε `worksheet.CustomProperties.Remove("PropertyName");`. Αυτό αφαιρεί την καταχώρηση από τη συλλογή. |

## Επόμενα βήματα

Τώρα που γνωρίζετε **πώς να προσθέσετε προσαρμοσμένες ιδιότητες**, μπορείτε να εξερευνήσετε σχετικά θέματα όπως:

* **excel custom properties** για έκδοση εγγράφων  
* **read custom properties** από πολλαπλά φύλλα εργασίας σε ένα βιβλίο εργασίας  
* Χρήση του **Aspose.Cells** για δημιουργία πινάκων pivot που αναφέρονται σε προσαρμοσμένα μεταδεδομένα  
* Εξαγωγή του βιβλίου εργασίας σε PDF διατηρώντας τις προσαρμοσμένες ιδιότητες  

Πειραματιστείτε με διαφορετικούς τύπους δεδομένων, συνδυάστε τις προσαρμοσμένες ιδιότητες με σχόλια κελιών ή ενσωματώστε τα μεταδεδομένα σε ένα μεγαλύτερο σύστημα διαχείρισης εγγράφων.

---

**Έτοιμοι να αυτοματοποιήσετε τις αναφορές Excel σας;** Προσθέστε τον παραπάνω κώδικα στο έργο σας, προσαρμόστε τα ονόματα ιδιοτήτων ώστε να ταιριάζουν στις επιχειρηματικές σας ανάγκες και θα έχετε ένα αυτο‑περιγραφικό φύλλο εργασίας έτοιμο για επεξεργασία downstream.

## Τι πρέπει να μάθετε στη συνέχεια;

Οι παρακάτω εκπαιδευτικοί οδηγίες καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στην υλοποίηση των δικών σας έργων.

- [Create Excel Workbook – Add Custom Properties and Save as XLSB](/cells/english/net/document-properties/create-excel-workbook-add-custom-properties-and-save-as-xlsb/)
- [How to Access Custom Document Properties in Excel Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/access-custom-excel-properties-aspose-cells-net/)
- [Master Excel Custom Properties Using Aspose.Cells .NET for Enhanced Data Management](/cells/english/net/data-manipulation/excel-custom-properties-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}