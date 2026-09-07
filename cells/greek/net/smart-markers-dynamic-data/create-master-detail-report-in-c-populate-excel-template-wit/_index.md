---
category: general
date: 2026-02-28
description: Δημιουργήστε αναφορά master‑detail σε C# και μάθετε πώς να γεμίζετε πρότυπο
  Excel, να συγχωνεύετε δεδομένα στο Excel και να φορτώνετε βιβλίο εργασίας Excel
  σε C# σε λίγα μόνο βήματα.
draft: false
keywords:
- create master detail report
- populate excel template
- merge data into excel
- load excel workbook c#
- how to create master detail
language: el
og_description: Δημιουργήστε αναφορά master‑detail σε C# χρησιμοποιώντας το Aspose.Cells
  SmartMarker. Μάθετε πώς να φορτώνετε ένα βιβλίο εργασίας Excel σε C#, να συγχωνεύετε
  δεδομένα στο Excel και να συμπληρώνετε ένα πρότυπο Excel.
og_title: Δημιουργία αναφοράς master‑detail σε C# – Συμπλήρωση προτύπου Excel
tags:
- C#
- Aspose.Cells
- Excel automation
- SmartMarker
title: Δημιουργία αναφοράς master‑detail σε C# – Συμπλήρωση προτύπου Excel με SmartMarker
url: /el/net/smart-markers-dynamic-data/create-master-detail-report-in-c-populate-excel-template-wit/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία αναφοράς master‑detail σε C# – Συμπλήρωση προτύπου Excel με SmartMarker

Έχετε ποτέ χρειαστεί να **δημιουργήσετε αναφορά master‑detail** σε C# αλλά δεν ήσασταν σίγουροι πώς να μεταφέρετε τα δεδομένα σε ένα αρχείο Excel; Δεν είστε μόνοι. Σε αυτόν τον οδηγό θα περάσουμε βήμα‑βήμα τις ακριβείς ενέργειες για να **συμπληρώσετε πρότυπο Excel**, **συγχωνεύσετε δεδομένα στο Excel**, και **φορτώσετε βιβλίο εργασίας Excel σε C#**‑στυλ ώστε να καταλήξετε με μια επαγγελματική αναφορά master‑detail έτοιμη για διανομή.

Θα χρησιμοποιήσουμε το Aspose.Cells SmartMarker, μια ισχυρή μηχανή που κατανοεί σχέσεις master‑detail από την αρχή. Στο τέλος του tutorial θα έχετε ένα πλήρες, εκτελέσιμο παράδειγμα που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο .NET. Χωρίς ασαφείς συντομεύσεις «δείτε τα έγγραφα»—απλώς μια αυτόνομη λύση που μπορείτε να αντιγράψετε‑επικολλήσετε και να εκτελέσετε.

## Τι θα μάθετε

- Πώς να **δημιουργήσετε master‑detail** δομές δεδομένων σε C# που αντιστοιχούν άμεσα σε ένα πρότυπο Excel.
- Ο ακριβής τρόπος για **φόρτωση βιβλίου εργασίας Excel σε C#** κώδικα που ανοίγει ένα αρχείο `.xlsx` που περιέχει ετικέτες SmartMarker.
- Η διαδικασία για **συμπλήρωση προτύπου Excel** εκτελώντας το `SmartMarkerProcessor`.
- Συμβουλές για τη διαχείριση ειδικών περιπτώσεων, όπως ελλιπείς ετικέτες ή μεγάλα σύνολα δεδομένων.
- Πώς να επαληθεύσετε το αποτέλεσμα και πώς φαίνεται η τελική **αναφορά master‑detail**.

### Προαπαιτούμενα

- .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί επίσης σε .NET Framework 4.8).
- Aspose.Cells για .NET (μπορείτε να κατεβάσετε ένα δωρεάν trial πακέτο NuGet: `Install-Package Aspose.Cells`).
- Ένα βασικό αρχείο Excel (`template.xlsx`) που περιέχει ετικέτες SmartMarker (θα δείξουμε το ελάχιστο markup που χρειάζεστε).

Αν έχετε όλα αυτά έτοιμα, ας ξεκινήσουμε.

## Βήμα 1 – Δημιουργία πηγής δεδομένων master‑detail *(πώς να δημιουργήσετε master‑detail)*

Το πρώτο πράγμα που χρειάζεστε είναι ένα αντικείμενο C# που αντιπροσωπεύει τις κύριες γραμμές (παραγγελίες) και τις θυγατρικές γραμμές τους (στοιχεία παραγγελίας). Το SmartMarker θα διαβάσει αυτήν την ιεραρχία αυτόματα όταν το `MasterDetail` είναι ορισμένο σε `true`.

```csharp
using System;

// Step 1: Build the master‑detail data object
var orderData = new
{
    // Master collection – each order is a row in the master table
    Orders = new[]
    {
        new
        {
            Id = 1,
            // Detail collection – items belonging to order 1
            Items = new[] { new { Sku = 101, Qty = 2 }, new { Sku = 102, Qty = 1 } }
        },
        new
        {
            Id = 2,
            Items = new[] { new { Sku = 202, Qty = 1 } }
        }
    }
};
```

**Γιατί είναι σημαντικό:**  
Το SmartMarker ψάχνει για μια ιδιότητα με όνομα `Orders` (ο master) και για κάθε παραγγελία αναζητά μια συλλογή που ονομάζεται `Items`. Συμφωνώντας αυτά τα ονόματα, λαμβάνετε αυτόματα μια **αναφορά master‑detail** χωρίς να γράψετε κανένα βρόχο.

> **Συμβουλή:** Κρατήστε τα ονόματα των ιδιοτήτων σύντομα και περιγραφικά· γίνονται οι placeholders στο πρότυπο Excel σας.

## Βήμα 2 – Διαμόρφωση επιλογών SmartMarker για επεξεργασία master‑detail

Ενημερώστε τη μηχανή ότι αντιμετωπίζετε ένα σενάριο master‑detail και δώστε της το όνομα του φύλλου λεπτομερειών που θα λάβει τις θυγατρικές γραμμές.

```csharp
using Aspose.Cells;

// Step 2: Set up SmartMarker options
SmartMarkerOptions options = new SmartMarkerOptions
{
    // Enables master‑detail processing
    MasterDetail = true,
    // The sheet in the template that holds the detail rows
    DetailSheetName = "OrderDetail"
};
```

**Γιατί είναι σημαντικό:**  
Αν παραλείψετε το `MasterDetail = true`, το SmartMarker θα θεωρήσει τα δεδομένα ως επίπεδη λίστα και οι γραμμές λεπτομερειών δεν θα εμφανιστούν ποτέ. Το `DetailSheetName` πρέπει να ταιριάζει με το όνομα του φύλλου που δημιουργήσατε στο πρότυπο (διάκριση πεζών‑κεφαλαίων).

## Βήμα 3 – Φόρτωση βιβλίου εργασίας Excel σε στυλ C#

Τώρα ανοίγουμε το πρότυπο που περιέχει τις ετικέτες SmartMarker. Αυτό είναι το βήμα **φόρτωσης βιβλίου εργασίας Excel σε C#** που πολλοί προγραμματιστές συναντούν δυσκολίες επειδή ξεχνούν να χρησιμοποιήσουν τη σωστή διαδρομή αρχείου ή να απελευθερώσουν σωστά το βιβλίο εργασίας.

```csharp
using System.IO;

// Step 3: Load the workbook that holds the SmartMarker tags
string templatePath = Path.Combine(Environment.CurrentDirectory, "template.xlsx");
Workbook workbook = new Workbook(templatePath);
```

**Γιατί είναι σημαντικό:**  
Το Aspose.Cells διαβάζει ολόκληρο το βιβλίο εργασίας στη μνήμη, έτσι το αρχείο μπορεί να βρίσκεται στον δίσκο, ενσωματωμένο ως πόρος, ή ακόμη και να μεταδίδεται από μια υπηρεσία web. Απλώς βεβαιωθείτε ότι η διαδρομή δείχνει σε ένα έγκυρο αρχείο `.xlsx` που περιέχει τις ετικέτες που θα συζητήσουμε στη συνέχεια.

## Βήμα 4 – Εισαγωγή ετικετών SmartMarker στο πρότυπο (συμπλήρωση προτύπου Excel)

Αν ανοίξετε το `template.xlsx` τώρα, θα δείτε δύο φύλλα:

- **Orders** – το κύριο φύλλο με μια γραμμή όπως `&=Orders.Id`.
- **OrderDetail** – το φύλλο λεπτομερειών με γραμμές όπως `&=Items.Sku` και `&=Items.Qty`.

Ακολουθεί μια ελάχιστη προβολή του markup:

| Φύλλο | Κελί A1 | Κελί B1 |
|-------|---------|---------|
| Orders | `&=Orders.Id` | *(empty)* |
| OrderDetail | `&=Items.Sku` | `&=Items.Qty` |

Δεν χρειάζεται να γράψετε κώδικα για τις ετικέτες—ζουν στο αρχείο Excel. Το βήμα **συμπλήρωσης προτύπου Excel** είναι απλώς η κλήση του επεξεργαστή:

```csharp
// Step 4: Run SmartMarker to merge data into Excel
new SmartMarkerProcessor().Process(workbook, orderData, options);
```

**Γιατί είναι σημαντικό:**  
Ο επεξεργαστής σαρώει κάθε φύλλο, αντικαθιστά τα placeholders `&=` με πραγματικές τιμές και επεκτείνει τις γραμμές για κάθε master και detail εγγραφή. Επειδή το `MasterDetail` είναι ενεργό, δημιουργεί αυτόματα μια νέα γραμμή για κάθε στοιχείο κάτω από την αντίστοιχη παραγγελία.

## Βήμα 5 – Αποθήκευση της αναφοράς master‑detail

Τέλος, γράψτε το συμπληρωμένο βιβλίο εργασίας στο δίσκο. Αυτή είναι η στιγμή που έχετε μια έτοιμη‑για‑διανομή **αναφορά master‑detail**.

```csharp
// Step 5: Save the populated workbook
string outputPath = Path.Combine(Environment.CurrentDirectory, "output.xlsx");
workbook.Save(outputPath);

// Optional: open the file automatically (Windows only)
System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
{
    FileName = outputPath,
    UseShellExecute = true
});
```

**Αναμενόμενο αποτέλεσμα:**  

- Το φύλλο **Orders** εμφανίζει δύο γραμμές: `1` και `2` (IDs παραγγελιών).  
- Το φύλλο **OrderDetail** εμφανίζει τρεις γραμμές:  
  - SKU 101 Qty 2  
  - SKU 102 Qty 1  
  - SKU 202 Qty 1  

Αυτή είναι μια πλήρως λειτουργική **δημιουργία αναφοράς master‑detail** που μπορείτε να στείλετε με email, να εκτυπώσετε ή να ενσωματώσετε σε άλλο σύστημα.

## Περιπτώσεις άκρων & συχνές ερωτήσεις

### Τι γίνεται αν το πρότυπο λείπει μια ετικέτα;

Το SmartMarker αγνοεί σιωπηλά τις άγνωστες ετικέτες, αλλά θα καταλήξετε με κενά κελιά. Ελέγξτε ξανά την ορθογραφία της ετικέτας και βεβαιωθείτε ότι τα ονόματα των ιδιοτήτων στο αντικείμενο C# ταιριάζουν ακριβώς.

### Πώς διαχειρίζεται μεγάλα σύνολα δεδομένων;

Ο επεξεργαστής μεταδίδει σειρές, έτσι ακόμη και χιλιάδες εγγραφές λεπτομερειών δεν θα εξαντλήσουν τη μνήμη. Ωστόσο, για εξαιρετικά μεγάλα αρχεία ίσως θελήσετε να αυξήσετε το `MemorySetting` στο `LoadOptions`.

```csharp
var loadOptions = new LoadOptions(LoadFormat.Xlsx)
{
    MemorySetting = MemorySetting.MemoryPreference
};
Workbook largeWorkbook = new Workbook(templatePath, loadOptions);
```

### Μπορώ να χρησιμοποιήσω διαφορετικό όνομα φύλλου για το master;

Ναι—απλώς μετονομάστε το φύλλο στο πρότυπο και προσαρμόστε το `DetailSheetName` αν έχετε φύλλο λεπτομερειών. Το όνομα του master φύλλου προκύπτει από το placeholder (`&=Orders.Id`).

### Τι κάνω αν χρειαστεί να προσθέσω μια γραμμή συνόλων;

Προσθέστε έναν κανονικό τύπο Excel στο πρότυπο (π.χ., `=SUM(B2:B{#})`). Το SmartMarker θα διατηρήσει τον τύπο μετά την εισαγωγή των δεδομένων.

## Πλήρες εκτελέσιμο παράδειγμα

Παρακάτω βρίσκεται το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε‑επικολλήσετε σε μια εφαρμογή console. Περιλαμβάνει όλες τις οδηγίες `using`, το μοντέλο δεδομένων, τις επιλογές και τη διαχείριση αρχείων.

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace MasterDetailReportDemo
{
    class Program
    {
        static void Main()
        {
            // ---------- Step 1: Create master‑detail data ----------
            var orderData = new
            {
                Orders = new[]
                {
                    new
                    {
                        Id = 1,
                        Items = new[]
                        {
                            new { Sku = 101, Qty = 2 },
                            new { Sku = 102, Qty = 1 }
                        }
                    },
                    new
                    {
                        Id = 2,
                        Items = new[]
                        {
                            new { Sku = 202, Qty = 1 }
                        }
                    }
                }
            };

            // ---------- Step 2: SmartMarker options ----------
            SmartMarkerOptions options = new SmartMarkerOptions
            {
                MasterDetail = true,
                DetailSheetName = "OrderDetail"
            };

            // ---------- Step 3: Load the template ----------
            string templatePath = Path.Combine(Environment.CurrentDirectory, "template.xlsx");
            Workbook workbook = new Workbook(templatePath);

            // ---------- Step 4: Process the template ----------
            new SmartMarkerProcessor().Process(workbook, orderData, options);

            // ---------- Step 5: Save the result ----------
            string outputPath = Path.Combine(Environment.CurrentDirectory, "output.xlsx");
            workbook.Save(outputPath);

            Console.WriteLine($"Master detail report generated at: {outputPath}");
        }
    }
}
```

Εκτελέστε το πρόγραμμα, ανοίξτε το `output.xlsx` και θα δείτε τα δεδομένα master‑detail να έχουν συμπληρωθεί όμορφα.

## Οπτική αναφορά

![Στιγμιότυπο εξόδου αναφοράς master‑detail](https://example.com/images/master-detail-report.png "Παράδειγμα αναφοράς master‑detail")

*Η εικόνα δείχνει το φύλλο Orders με IDs 1 και 2, και το φύλλο OrderDetail με τις τρεις γραμμές SKU‑Qty.*

## Συμπέρασμα

Τώρα ξέρετε **πώς να δημιουργήσετε αναφορά master‑detail** σε C# χρησιμοποιώντας το Aspose.Cells SmartMarker, από τη δημιουργία της πηγής δεδομένων μέχρι το **φόρτωμα βιβλίου εργασίας Excel σε C#**, **συμπλήρωση προτύπου Excel**, και τέλος

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}