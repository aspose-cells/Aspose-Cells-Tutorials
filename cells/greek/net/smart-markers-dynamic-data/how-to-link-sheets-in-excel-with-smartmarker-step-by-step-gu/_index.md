---
category: general
date: 2026-06-08
description: Πώς να συνδέσετε φύλλα στο Excel χρησιμοποιώντας το SmartMarkerProcessor
  για αναφορές master‑detail. Συμπληρώστε το κύριο φύλλο και δημιουργήστε μια αναφορά
  master‑detail στο Excel χωρίς κόπο.
draft: false
keywords:
- how to link sheets
- populate master sheet
- create master detail excel
- generate master detail report
language: el
og_description: Πώς να συνδέσετε φύλλα στο Excel χρησιμοποιώντας το SmartMarkerProcessor.
  Μάθετε πώς να γεμίσετε το κύριο φύλλο και να δημιουργήσετε μια αναφορά master‑detail
  σε λίγα λεπτά.
og_title: Πώς να συνδέσετε φύλλα στο Excel με το SmartMarker – Βήμα‑προς‑βήμα
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: How to link sheets in Excel using SmartMarkerProcessor for master‑detail
    reports. Populate master sheet and generate a master detail Excel report effortlessly.
  headline: How to Link Sheets in Excel with SmartMarker – Step‑by‑Step Guide
  type: TechArticle
- description: How to link sheets in Excel using SmartMarkerProcessor for master‑detail
    reports. Populate master sheet and generate a master detail Excel report effortlessly.
  name: How to Link Sheets in Excel with SmartMarker – Step‑by‑Step Guide
  steps:
  - name: Multiple Detail Rows per Master
    text: If a master row has several related details, SmartMarker repeats the master
      row once and then writes *all* matching detail rows beneath it. No extra code
      is needed—just ensure your `Details` collection contains every row.
  - name: Missing Details
    text: When a master entry has no matching detail rows, the detail sheet simply
      skips that section. If you need a placeholder (e.g., “No items”), you can add
      a calculated column in the template that uses an Excel formula like `=IF(COUNTA(A2:B2)=0,"No
      items","")`.
  - name: Large Datasets
    text: 'Processing tens of thousands of rows can be memory‑intensive. To keep performance
      snappy:'
  - name: Custom Column Mapping
    text: If your property names don’t line up (`MasterKey` vs `Id`), you can use
      the `SmartMarkerProcessor.Map` method to create an alias before processing.
  type: HowTo
tags:
- Excel
- SmartMarker
- C#
- master‑detail
title: Πώς να συνδέσετε φύλλα στο Excel με το SmartMarker – Οδηγός βήμα‑βήμα
url: /el/net/smart-markers-dynamic-data/how-to-link-sheets-in-excel-with-smartmarker-step-by-step-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Συνδέσετε Φύλλα στο Excel με το SmartMarker – Οδηγός Βήμα‑Βήμα

Έχετε αναρωτηθεί ποτέ **πώς να συνδέσετε φύλλα** στο Excel χωρίς να αντιγράφετε χειροκίνητα γραμμές ή να γράφετε ατέλειωτους βρόχους VBA; Δεν είστε μόνοι. Οι περισσότεροι προγραμματιστές συναντούν εμπόδιο όταν χρειάζονται μια καθαρή αναφορά master‑detail που παραμένει συγχρονισμένη καθώς αλλάζουν τα δεδομένα. Τα καλά νέα; Το SmartMarkerProcessor κάνει το σκληρό έργο για εσάς, μετατρέποντας μερικές γραμμές C# σε ένα πλήρως εξοπλισμένο βιβλίο εργασίας master‑detail.

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα τις ακριβείς ενέργειες για να **συμπληρώσετε το master sheet**, να ρυθμίσετε το detail sheet και τελικά να **δημιουργήσετε αναφορά master‑detail** που ενημερώνεται αυτόματα. Στο τέλος θα έχετε ένα επαναχρησιμοποιήσιμο πρότυπο που μπορείτε να ενσωματώσετε σε οποιοδήποτε .NET project.

> **Σημείωση προαπαιτούμενου:** Χρειάζεστε το GrapeCity Documents for Excel (GcExcel) έκδοση 2024 ή νεότερη, ένα .NET περιβάλλον ανάπτυξης (το Visual Studio 2022 λειτουργεί άψογα) και βασική εξοικείωση με C#. Δεν απαιτούνται επιπλέον πακέτα NuGet εκτός του GcExcel.

## Επισκόπηση της Λύσης

Πριν βυθιστούμε στον κώδικα, ας αναλύσουμε τι σημαίνει πραγματικά η «σύνδεση φύλλων» στο πλαίσιο του SmartMarker:

1. **Master sheet** – Περιέχει μία γραμμή ανά οντότητα (π.χ., λίστα πελατών).
2. **Detail sheet** – Περιέχει γραμμές που ανήκουν σε μια master γραμμή (π.χ., παραγγελίες για κάθε πελάτη).
3. **SmartMarker syntax** – Μια μικρή γλώσσα σήμανσης (`{MasterSheet}#master;{DetailSheet}#detail`) που λέει στον επεξεργαστή πώς να συνδέσει τους δύο πίνακες δεδομένων.
4. **Processor options** – Η ενεργοποίηση του `MasterDetail` κάνει τη μηχανή να επαναλαμβάνει αυτόματα τις master γραμμές και να ενσωματώνει τις σχετικές detail γραμμές κάτω από αυτές.

Η κατανόηση αυτών των στοιχείων σας βοηθά να προσαρμόσετε την προσέγγιση αργότερα — ίσως χρειαστείτε τρι‑επίπεδη ένθεση ή υπό συνθήκη μορφοποίηση. Κρατήστε αυτό το νοητικό μοντέλο κοντά σας καθώς προχωρούμε στην υλοποίηση.

## Βήμα 1: Προετοιμασία Ιεραρχικών Δεδομένων για Επεξεργασία Master‑Detail

Το πρώτο που χρειάζεστε είναι μια πηγή δεδομένων που αντικατοπτρίζει τη σχέση master‑detail. Στις περισσότερες πραγματικές περιπτώσεις αυτό προέρχεται από μια βάση δεδομένων, αλλά για σαφήνεια θα χρησιμοποιήσουμε ένα ανώνυμο αντικείμενο literal.

```csharp
// Step 1: Prepare hierarchical data for master‑detail processing
var sampleData = new
{
    // Master collection – one row per category
    Master = new[]
    {
        new { Id = 1, Name = "A" },
        new { Id = 2, Name = "B" }
    },

    // Detail collection – rows reference MasterId
    Details = new[]
    {
        new { MasterId = 1, Item = "Item1" },
        new { MasterId = 2, Item = "Item2" }
    }
};
```

**Γιατί είναι σημαντικό:** Το SmartMarker δεν μαντεύει μαγικά τις σχέσεις· ψάχνει για ταιριαστά ονόματα ιδιοτήτων (`MasterId` → `Id`). Με τη δομή αυτή των δεδομένων δίνουμε στον επεξεργαστή έναν σαφή χάρτη, που αποτελεί τη βάση του **πώς να συνδέσετε φύλλα** αποτελεσματικά.

> **Συμβουλή:** Αν τα δεδομένα σας βρίσκονται σε αντικείμενα `DataTable`, απλώς εκθέστε τα ως ιδιότητες με τα ίδια ονόματα — το SmartMarker λειτουργεί με οποιαδήποτε συλλογή που μπορεί να επαναληφθεί.

## Βήμα 2: Δημιουργία Βιβλίου Εργασίας και Φόρτωση Προτύπου

Το SmartMarker λειτουργεί πάνω σε ένα υπάρχον βιβλίο εργασίας Excel, συνήθως ένα πρότυπο που περιέχει ήδη τα ονόματα των φύλλων και τους δείκτες θέσης. Ας δημιουργήσουμε ένα βιβλίο εργασίας στη μνήμη και να προσθέσουμε δύο κενά φύλλα εργασίας με ονόματα *MasterSheet* και *DetailSheet*.

```csharp
using GrapeCity.Documents.Excel;

// Step 2: Create a workbook and add template sheets
IWorkbook wb = new Workbook();

// Create the master sheet and add a header row
IWorksheet masterSheet = wb.Worksheets.Add("MasterSheet");
masterSheet.Range["A1"].Value = "ID";
masterSheet.Range["B1"].Value = "Name";

// Create the detail sheet and add its header
IWorksheet detailSheet = wb.Worksheets.Add("DetailSheet");
detailSheet.Range["A1"].Value = "Master ID";
detailSheet.Range["B1"].Value = "Item";
```

Μπορείτε επίσης να φορτώσετε ένα αρχείο `.xlsx` από το δίσκο (`wb.Open("Template.xlsx")`) αν προτιμάτε να σχεδιάσετε τη διάταξη πρώτα στο Excel. Το σημαντικό είναι τα ονόματα των φύλλων να ταιριάζουν με αυτά που θα αναφέρετε στη συμβολοσειρά SmartMarker.

## Βήμα 3: Δημιουργία SmartMarkerProcessor και Ενεργοποίηση Λειτουργίας Master‑Detail

Τώρα φέρνουμε τη μηχανή που θα διαβάσει τους δείκτες και θα επικολλήσει τα δεδομένα. Ο `SmartMarkerProcessor` παίρνει το βιβλίο εργασίας ως όρισμα κατασκευής, και η σημαία `Options.MasterDetail` του λέει να αντιμετωπίζει τους δείκτες `#master` και `#detail` ως συνδεδεμένο ζεύγος.

```csharp
// Step 3: Create a SmartMarkerProcessor for the workbook
SmartMarkerProcessor processor = new SmartMarkerProcessor(wb);

// Enable master‑detail mode on the processor options
processor.Options.MasterDetail = true;
```

**Γιατί να ενεργοποιήσετε το `MasterDetail`;** Χωρίς αυτή τη σημαία, ο επεξεργαστής θα αντιμετωπίζει το `{MasterSheet}#master` και το `{DetailSheet}#detail` ως ανεξάρτητες λειτουργίες, χάνοντας τη σημαντική σχέση μεταξύ των γραμμών. Η ρύθμιση της σημαίας είναι η μοναδική γραμμή που κάνει το **πώς να συνδέσετε φύλλα** να λειτουργήσει πραγματικά.

## Βήμα 4: Ορισμός της Συμβολοσειράς SmartMarker και Εκτέλεση του Επεξεργαστή

Η συμβολοσειρά δεικτών λέει στο SmartMarker ποιο φύλλο είναι το master και ποιο το detail. Η σύνταξη είναι απλή: `{SheetName}#master;{SheetName}#detail`. Μπορείτε επίσης να προσθέσετε επιπλέον δείκτες (π.χ., `#header`), αλλά δεν χρειάζονται για μια βασική αναφορά.

```csharp
// Step 4: Execute the smart‑marker processing, linking master and detail sheets
string marker = "{MasterSheet}#master;{DetailSheet}#detail";
processor.Process(marker, sampleData);
```

Όταν `Process` τρέξει, η μηχανή:

1. Γράφει κάθε master γραμμή στο *MasterSheet* ξεκινώντας από την πρώτη κενή γραμμή μετά την κεφαλίδα.
2. Για κάθε master γραμμή, σαρώει τη συλλογή `Details`, επιλέγει τις γραμμές όπου το `MasterId` ταιριάζει με το master `Id`, και τις γράφει στο *DetailSheet* ακριβώς κάτω από την αντίστοιχη master εγγραφή.

## Βήμα 5: Αποθήκευση ή Εξαγωγή του Τελικού Βιβλίου Εργασίας

Σε αυτό το σημείο έχετε ένα πλήρως συμπληρωμένο βιβλίο εργασίας. Μπορείτε να το αποθηκεύσετε στο δίσκο, να το μεταδώσετε πίσω σε έναν web client, ή ακόμη και να το μετατρέψετε σε PDF.

```csharp
// Save the workbook to a file (you could also stream it to a response)
wb.Save("MasterDetailReport.xlsx");
```

Ανοίξτε το αρχείο και θα δείτε δύο φύλλα: το *MasterSheet* εμφανίζει `A` και `B`, ενώ το *DetailSheet* δείχνει το `Item1` κάτω από το master `1` και το `Item2` κάτω από το master `2`. Αυτή είναι η ουσία του **συμπλήρωσης master sheet** και της **δημιουργίας αναφοράς master‑detail** σε ένα βήμα.

## Οπτική Επισκόπηση

![Diagram illustrating how to link sheets in Excel using SmartMarkerProcessor](https://example.com/diagram.png "How to link sheets diagram")

The diagram (alt text includes the primary keyword) shows the data flow from C# objects → SmartMarkerProcessor → linked Excel sheets.

## Διαχείριση Συνηθισμένων Περιπτώσεων Άκρων

### Πολλαπλές Γραμμές Detail ανά Master

Αν μια master γραμμή έχει πολλές σχετικές λεπτομέρειες, το SmartMarker επαναλαμβάνει τη master γραμμή μία φορά και στη συνέχεια γράφει *όλες* τις ταιριαστές detail γραμμές κάτω από αυτήν. Δεν απαιτείται επιπλέον κώδικας — απλώς βεβαιωθείτε ότι η συλλογή `Details` περιέχει κάθε γραμμή.

### Ελλιπείς Λεπτομέρειες

Όταν μια master εγγραφή δεν έχει ταιριαστές detail γραμμές, το detail φύλλο απλώς παραλείπει αυτήν την ενότητα. Αν χρειάζεστε έναν δείκτη θέσης (π.χ., “No items”), μπορείτε να προσθέσετε μια υπολογισμένη στήλη στο πρότυπο που χρησιμοποιεί έναν τύπο Excel όπως `=IF(COUNTA(A2:B2)=0,\"No items\",\"\")`.

### Μεγάλα Σύνολα Δεδομένων

Η επεξεργασία δεκάδων χιλιάδων γραμμών μπορεί να είναι απαιτητική σε μνήμη. Για να διατηρήσετε την απόδοση γρήγορη:

- Χρησιμοποιήστε `processor.Options.EnableStreaming = true` (διαθέσιμο στο GcExcel 2025+).
- Διαχωρίστε τα δεδομένα σε τμήματα και επεξεργαστείτε κάθε τμήμα ξεχωριστά, στη συνέχεια συγχωνεύστε τα βιβλία εργασίας.

### Προσαρμοστική Αντιστοίχιση Στηλών

Αν τα ονόματα των ιδιοτήτων σας δεν ταιριάζουν (`MasterKey` vs `Id`), μπορείτε να χρησιμοποιήσετε τη μέθοδο `SmartMarkerProcessor.Map` για να δημιουργήσετε ένα ψευδώνυμο πριν την επεξεργασία.

```csharp
processor.Map("MasterId", "Id"); // tells the engine that MasterId maps to Id
```

## Πλήρες Παράδειγμα Εργασίας

Συνδυάζοντας όλα, εδώ είναι ένα πλήρες, έτοιμο για αντιγραφή‑επικόλληση πρόγραμμα που μπορείτε να εκτελέσετε αμέσως.



## Τι Θα Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετικές θεματικές που επεκτείνουν τις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας projects.

- [Κύρια Εξωτερικά Σύνδεσμοι Συναρτήσεων σε Excel Χρησιμοποιώντας Aspose.Cells για Java](/cells/english/java/formulas-functions/aspose-cells-java-external-link-formulas-excel/)
- [Κύρια Δυναμικά Φύλλα Excel σε Java με Aspose.Cells: Ένας Πλήρης Οδηγός](/cells/english/java/formulas-functions/dynamic-excel-sheets-aspose-cells-java-guide/)
- [Κύρια Δυναμικές Αναφορές Excel Χρησιμοποιώντας Aspose.Cells Java: Ονομαστικές Περιοχές & Πολύπλοκοι Τύποι](/cells/english/java/templates-reporting/dynamic-excel-reports-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}