---
category: general
date: 2026-11-19
description: Πώς να επαναλάβετε το φύλλο εργασίας κατά τη συμπλήρωση του Excel με
  δεδομένα πίνακα. Μάθετε να δημιουργείτε πολλαπλά φύλλα εργασίας και να γεμίζετε
  ένα φύλλο εργασίας από λίστα σε λίγα βήματα.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to repeat worksheet
- populate excel with array
- generate multiple worksheets
- populate worksheet from list
language: el
lastmod: 2026-11-19
og_description: Πώς να επαναλάβετε ένα φύλλο εργασίας χρησιμοποιώντας το SmartMarkerProcessor.
  Ακολουθήστε αυτόν τον οδηγό για να γεμίσετε το Excel με δεδομένα πίνακα, να δημιουργήσετε
  πολλαπλά φύλλα εργασίας και να γεμίσετε ένα φύλλο εργασίας από λίστα.
og_image_alt: Screenshot showing repeated worksheets in an Excel workbook after processing
og_title: Πώς να επαναλάβετε το φύλλο εργασίας στο Excel – βήμα‑βήμα οδηγός
schemas:
- author: GroupDocs
  dateModified: '2026-11-19'
  description: How to repeat worksheet while populating Excel with array data. Learn
    to generate multiple worksheets and populate worksheet from list in a few steps.
  headline: How to repeat worksheet in Excel with SmartMarkerProcessor
  type: TechArticle
- description: How to repeat worksheet while populating Excel with array data. Learn
    to generate multiple worksheets and populate worksheet from list in a few steps.
  name: How to repeat worksheet in Excel with SmartMarkerProcessor
  steps:
  - name: Expected output
    text: 'When you open the resulting workbook, you should see:'
  - name: Empty or null arrays
    text: 'If `Dept` is null or empty, the processor will not create any additional
      worksheets. To avoid a completely blank workbook, you can add a guard:'
  - name: Custom worksheet names
    text: 'The default naming scheme may not suit every reporting requirement. After
      processing, rename each sheet using a loop:'
  - name: Populating additional columns
    text: 'If you need to **populate excel with array** values beyond a single marker,
      extend the data object:'
  type: HowTo
tags:
- Excel automation
- SmartMarkerProcessor
- .NET
title: Πώς να επαναλάβετε το φύλλο εργασίας στο Excel με το SmartMarkerProcessor
url: /el/net/smart-markers-dynamic-data/how-to-repeat-worksheet-in-excel-with-smartmarkerprocessor/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να επαναλάβετε φύλλο εργασίας στο Excel με SmartMarkerProcessor

Αν χρειάζεστε **how to repeat worksheet** κατά τη δημιουργία αναφορών Excel, αυτός ο οδηγός σας παρουσιάζει μια πλήρη, εκτελέσιμη λύση. Στο τέλος του tutorial θα μπορείτε να **populate Excel with array** δεδομένα, **generate multiple worksheets**, και **populate worksheet from list** χρησιμοποιώντας τη βιβλιοθήκη SmartMarkerProcessor.

Η επανάληψη ενός φύλλου εργασίας είναι συχνή απαίτηση όταν κάθε τμήμα, περιοχή ή χρονική περίοδος χρειάζεται τη δική του καρτέλα. Το παρακάτω παράδειγμα δείχνει τα ακριβή βήματα, εξηγεί γιατί κάθε ρύθμιση είναι σημαντική και καλύπτει περιπτώσεις όπως κενές λίστες ή προσαρμοσμένη ονομασία.

## Προαπαιτούμενα

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

- .NET 6.0 ή νεότερη έκδοση εγκατεστημένη
- Αναφορά στο πακέτο NuGet **GroupDocs.Viewer** (ή ισοδύναμο) που περιέχει `SmartMarkerProcessor`
- Ένα πρότυπο βιβλίο εργασίας Excel (`.xlsx`) με έναν δείκτη όπως `${repeat:Dept}` τοποθετημένο σε μια γραμμή που θέλετε να επαναληφθεί
- Βασική εξοικείωση με C# και LINQ (προαιρετικό αλλά χρήσιμο)

Δεν απαιτούνται πρόσθετες βιβλιοθήκες τρίτων.

## Βήμα 1: Δημιουργία του αντικειμένου SmartMarkerProcessor

Ο επεξεργαστής διαχειρίζεται την αντικατάσταση των δεικτών και την αντιγραφή των φύλλων εργασίας. Η δημιουργία του χωρίς ορίσματα χρησιμοποιεί τις προεπιλεγμένες επιλογές.

```csharp
// Step 1: Create a SmartMarkerProcessor instance
SmartMarkerProcessor processor = new SmartMarkerProcessor();
```

Η δημιουργία του επεξεργαστή νωρίς σας επιτρέπει να ρυθμίσετε παγκόσμιες επιλογές πριν εφαρμοστούν τα δεδομένα. Αυτό αποτελεί τη βάση για **how to repeat worksheet** σωστά.

## Βήμα 2: Ενεργοποίηση επανάληψης φύλλου εργασίας

Από προεπιλογή ο επεξεργαστής αντικαθιστά δείκτες μόνο στο τρέχον φύλλο. Ορίζοντας το `RepeatWorksheet` σε `true` λέτε στη μηχανή να κλωνοποιήσει ολόκληρο το φύλλο για κάθε στοιχείο στη συλλογή δεδομένων.

```csharp
// Step 2: Enable worksheet repetition for the ${repeat:Dept} marker
processor.Options.RepeatWorksheet = true;
```

Η ενεργοποίηση αυτής της επιλογής είναι το κλειδί για **generate multiple worksheets** — ο επεξεργαστής θα δημιουργήσει μια νέα καρτέλα για κάθε στοιχείο του πίνακα `Dept` και θα διατηρήσει την αρχική μορφοποίηση.

## Βήμα 3: Προετοιμασία της πηγής δεδομένων ως πίνακα ή λίστας

Το SmartMarkerProcessor λειτουργεί με οποιοδήποτε enumerable, αλλά η χρήση πίνακα κάνει την πρόθεση σαφή όταν θέλετε να **populate worksheet from list**. Εδώ δημιουργούμε ένα ανώνυμο αντικείμενο που περιέχει μια ιδιότητα `Dept` με έναν πίνακα συμβολοσειρών.

```csharp
// Step 3: Prepare the data source with a list of departments
var data = new { Dept = new[] { "HR", "IT", "Finance" } };
```

Αν έχετε ήδη ένα `List<string>` μπορείτε να το περάσετε απευθείας· ο επεξεργαστής θα το αντιμετωπίσει με τον ίδιο τρόπο. Το σημαντικό είναι το όνομα της ιδιότητας (`Dept`) να ταιριάζει με τον δείκτη `${repeat:Dept}` στο πρότυπο.

## Βήμα 4: Φόρτωση του φύλλου εργασίας προτύπου

Υποθέτοντας ότι έχετε ένα `ExcelPackage` (από EPPlus) ή ένα αντικείμενο `Workbook`, ανακτήστε το φύλλο εργασίας που θέλετε να επαναλάβετε. Η μεταβλητή `ws` αντιπροσωπεύει αυτό το φύλλο.

```csharp
// Example using EPPlus to load the template workbook
using var package = new OfficeOpenXml.ExcelPackage(new FileInfo("Template.xlsx"));
var ws = package.Workbook.Worksheets[0]; // first worksheet
```

Αν προτιμάτε διαφορετική βιβλιοθήκη (π.χ., ClosedXML), ισχύει η ίδια αρχή: αποκτήστε ένα αντικείμενο φύλλου εργασίας που υλοποιεί τη απαιτούμενη διεπαφή.

## Βήμα 5: Επεξεργασία του φύλλου εργασίας με τα δεδομένα

Τώρα εφαρμόστε τα δεδομένα στο πρότυπο. Ο επεξεργαστής κλωνοποιεί το φύλλο για κάθε τμήμα, αντικαθιστά τον δείκτη `${repeat:Dept}` με το πραγματικό όνομα τμήματος και αφήνει το υπόλοιπο φύλλο αμετάβλητο.

```csharp
// Step 5: Apply the data to the template worksheet (ws)
processor.Process(ws, data);
```

Μετά το τέλος του `Process`, το `ws` γίνεται το πρώτο από πολλά φύλλα εργασίας — ένα ανά τμήμα. Το αρχικό όνομα φύλλου διατηρείται, ενώ τα αντίγραφα λαμβάνουν διαδοχικά επίθημα (π.χ., “Sheet1 (1)”, “Sheet1 (2)”). Μπορείτε να τα μετονομάσετε αργότερα αν χρειάζεστε προσαρμοσμένο σχήμα ονοματοδοσίας.

### Αναμενόμενο αποτέλεσμα

Όταν ανοίξετε το παραγόμενο βιβλίο εργασίας, θα δείτε:

- **Sheet1** – το αρχικό πρότυπο (συχνά κενό ή χρησιμοποιείται ως master)
- **Sheet1 (1)** – γεμάτο με “HR”
- **Sheet1 (2)** – γεμάτο με “IT”
- **Sheet1 (3)** – γεμάτο με “Finance”

Κάθε φύλλο περιέχει την ίδια διάταξη, αλλά με το όνομα τμήματος να έχει αντικατασταθεί εκεί που εμφανιζόταν `${repeat:Dept}`.

## Διαχείριση ειδικών περιπτώσεων

### Κενά ή null πίνακες

Αν το `Dept` είναι null ή κενό, ο επεξεργαστής δεν θα δημιουργήσει επιπλέον φύλλα. Για να αποφύγετε ένα εντελώς κενό βιβλίο, μπορείτε να προσθέσετε έναν έλεγχο:

```csharp
if (data.Dept != null && data.Dept.Any())
{
    processor.Process(ws, data);
}
else
{
    // Optionally write a warning or keep the original sheet unchanged
}
```

### Προσαρμοσμένα ονόματα φύλλων

Το προεπιλεγμένο σχήμα ονοματοδοσίας μπορεί να μην ταιριάζει σε κάθε απαίτηση αναφοράς. Μετά την επεξεργασία, μετονομάστε κάθε φύλλο μέσα σε βρόχο:

```csharp
for (int i = 1; i <= data.Dept.Length; i++)
{
    var sheet = package.Workbook.Worksheets[i]; // index 0 is the original
    sheet.Name = data.Dept[i - 1]; // use department name as tab title
}
```

### Συμπλήρωση επιπλέον στηλών

Αν χρειάζεστε **populate excel with array** τιμές πέρα από έναν δείκτη, επεκτείνετε το αντικείμενο δεδομένων:

```csharp
var data = new
{
    Dept = new[]
    {
        new { Name = "HR", Headcount = 12 },
        new { Name = "IT", Headcount = 25 },
        new { Name = "Finance", Headcount = 8 }
    }
};
```

Στη συνέχεια προσαρμόστε τους δείκτες του προτύπου σε `${repeat:Dept.Name}` και `${repeat:Dept.Headcount}`. Ο επεξεργαστής θα επαναλάβει τη γραμμή για κάθε τμήμα και θα γεμίσει και τις δύο στήλες.

## Πλήρες λειτουργικό παράδειγμα

Παρακάτω υπάρχει μια αυτόνομη εφαρμογή κονσόλας που δείχνει ολόκληρη τη ροή από τη φόρτωση του προτύπου μέχρι την αποθήκευση του τελικού βιβλίου εργασίας.

```csharp
using System;
using System.IO;
using OfficeOpenXml;               // Install-Package EPPlus
using GroupDocs.Viewer.Markup;    // SmartMarkerProcessor namespace

class Program
{
    static void Main()
    {
        // 1️⃣ Create processor
        SmartMarkerProcessor processor = new SmartMarkerProcessor();

        // 2️⃣ Enable worksheet repetition
        processor.Options.RepeatWorksheet = true;

        // 3️⃣ Define data source (array of departments)
        var data = new { Dept = new[] { "HR", "IT", "Finance" } };

        // 4️⃣ Load template workbook (ensure Template.xlsx exists)
        var fileInfo = new FileInfo("Template.xlsx");
        using var package = new ExcelPackage(fileInfo);
        var ws = package.Workbook.Worksheets[0]; // first sheet contains ${repeat:Dept}

        // 5️⃣ Process template
        processor.Process(ws, data);

        // Optional: rename generated sheets
        for (int i = 1; i <= data.Dept.Length; i++)
        {
            var sheet = package.Workbook.Worksheets[i];
            sheet.Name = data.Dept[i - 1];
        }

        // Save the result
        var output = new FileInfo("Result.xlsx");
        package.SaveAs(output);

        Console.WriteLine("Workbook generated with repeated worksheets.");
    }
}
```

**Επεξήγηση βασικών τμημάτων**

- **Δημιουργία επεξεργαστή** – καθορίζει τη μηχανή που θα ερμηνεύει τους δείκτες.
- **Επιλογή RepeatWorksheet** – ενεργοποιεί τη βασική λειτουργία που απαντά στο *how to repeat worksheet*.
- **Πηγή δεδομένων** – χρησιμοποιεί πίνακα (`new[]`) για να ικανοποιήσει **populate excel with array**.
- **Φόρτωση προτύπου** – δείχνει έναν κοινό τρόπο απόκτησης αντικειμένου φύλλου εργασίας.
- **Επεξεργασία** – εκτελεί την αντιγραφή και την εισαγωγή δεδομένων με μία κλήση.
- **Μετονομασία** – παρουσιάζει πώς να μετατρέψετε τα γενικά “(1)”, “(2)” ονόματα σε περιγραφικούς τίτλους, μια τυπική απαίτηση μετά το **generate multiple worksheets**.

Η εκτέλεση αυτού του προγράμματος παράγει το `Result.xlsx` με τρεις καρτέλες ειδικές για τμήματα, η καθεμία γεμάτη από τον πίνακα.

## Συνηθισμένα λάθη και συμβουλές

- **Ορθογραφία δείκτη** – ο δείκτης πρέπει να ταιριάζει ακριβώς με το όνομα της ιδιότητας (`${repeat:Dept}`). Λάθος ορθογραφίας εμποδίζει την επανάληψη.
- **Δείκτης φύλλου** – μετά την επεξεργασία, το αρχικό φύλλο παραμένει στη θέση 0· τα παραγόμενα φύλλα ακολουθούν διαδοχικά. Λάθος δείκτης μπορεί να οδηγήσει σε μετονομασία λανθασμένης καρτέλας.
- **Μεγάλα σύνολα δεδομένων** – η δημιουργία εκατοντάδων φύλλων μπορεί να αυξήσει δραματικά το μέγεθος του αρχείου. Σκεφτείτε το διαχωρισμό αναφορών ή τη χρήση ενός μόνο φύλλου με ομαδοποιημένες ενότητες αν η απόδοση γίνει πρόβλημα.
- **Ασφάλεια νήματος** – το `SmartMarkerProcessor` δεν είναι thread‑safe. Δημιουργήστε ξεχωριστό αντικείμενο ανά νήμα αν επεξεργάζεστε πολλά βιβλία εργασίας ταυτόχρονα.

## Συμπέρασμα

Τώρα γνωρίζετε **how to repeat worksheet** στο Excel χρησιμοποιώντας το SmartMarkerProcessor, πώς να **populate excel with array** δεδομένα, πώς να **generate multiple worksheets**, και πώς να **populate worksheet from list** αποδοτικά. Το πλήρες παράδειγμα ενώνει όλα τα concepts, και το προαιρετικό βήμα μετονομασίας σας επιτρέπει να δημιουργήσετε καθαρές, φιλικές προς τον χρήστη ονομασίες καρτελών.

Στη συνέχεια, μπορείτε να εξερευνήσετε:

- Χρήση του **populate worksheet from list** με σύνθετα αντικείμενα (nested collections)
- Εφαρμογή conditional formatting μετά την αντιγραφή των φύλλων
- Εξαγωγή του παραγόμενου βιβλίου εργασίας σε PDF ή CSV για downstream κατανάλωση

Αισθανθείτε ελεύθεροι να προσαρμόσετε τον κώδικα στις δικές σας ανάγκες αναφοράς και να απολαύσετε την αυτοματοποίηση των βιβλίων εργασίας Excel με σιγουριά!

## Τι πρέπει να μάθετε στη συνέχεια;

Οι παρακάτω οδηγίες καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να κυριαρχήσετε επιπλέον δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στην υλοποίηση των δικών σας έργων.

- [How to Repeat Worksheets – Complete Guide for Excel Automation](/cells/english/net/smart-markers-dynamic-data/how-to-repeat-worksheets-complete-guide-for-excel-automation/)
- [Create Worksheet Per Item – How to Repeat Worksheet in C#](/cells/english/net/worksheet-operations/create-worksheet-per-item-how-to-repeat-worksheet-in-c/)
- [How to expand array in Excel and populate a template](/cells/english/net/templates-reporting/how-to-expand-array-in-excel-and-populate-a-template/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}