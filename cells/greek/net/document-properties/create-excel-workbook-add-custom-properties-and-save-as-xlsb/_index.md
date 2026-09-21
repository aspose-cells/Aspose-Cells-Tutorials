---
category: general
date: 2026-03-22
description: Δημιουργήστε βιβλίο εργασίας Excel, προσθέστε προσαρμοσμένες ιδιότητες,
  ορίστε το όνομα του φύλλου εργασίας και αποθηκεύστε το ως δυαδικό αρχείο XLSB χρησιμοποιώντας
  C#.
draft: false
keywords:
- create excel workbook
- add custom properties
- save as xlsb
- set worksheet name
- write binary excel file
language: el
og_description: Δημιουργήστε βιβλίο εργασίας Excel, προσθέστε προσαρμοσμένες ιδιότητες,
  ορίστε το όνομα του φύλλου εργασίας και αποθηκεύστε το ως δυαδικό αρχείο XLSB χρησιμοποιώντας
  C#.
og_title: Δημιουργία βιβλίου εργασίας Excel – Προσθήκη προσαρμοσμένων ιδιοτήτων και
  αποθήκευση ως XLSB
tags:
- C#
- Aspose.Cells
- Excel automation
title: Δημιουργία βιβλίου εργασίας Excel – Προσθήκη προσαρμοσμένων ιδιοτήτων και αποθήκευση
  ως XLSB
url: /el/net/document-properties/create-excel-workbook-add-custom-properties-and-save-as-xlsb/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία βιβλίου εργασίας Excel – Προσθήκη προσαρμοσμένων ιδιοτήτων και αποθήκευση ως XLSB

Έχετε ποτέ χρειαστεί να **δημιουργήσετε βιβλίο εργασίας Excel** προγραμματιστικά αλλά και να διατηρήσετε κάποια μεταδεδομένα συνημμένα; Ίσως να χτίζετε μια μηχανή αναφορών που επισημαίνει κάθε αρχείο με ένα αναγνωριστικό αναφοράς, όνομα συγγραφέα ή αριθμό έκδοσης. Σε αυτήν την περίπτωση, η εκμάθηση του πώς να **προσθέσετε προσαρμοσμένες ιδιότητες** ενώ **ορίζετε το όνομα του φύλλου εργασίας** και τελικά **αποθηκεύετε ως XLSB** θα σας εξοικονομήσει πολύ χειροκίνητη επεξεργασία.

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από ένα πλήρες, εκτελέσιμο παράδειγμα που δείχνει ακριβώς πώς να **γράψετε δυαδικό αρχείο Excel** χρησιμοποιώντας C#. Θα δείτε γιατί η μορφή XLSB είναι η σωστή επιλογή για τη μεταφορά προσαρμοσμένων ιδιοτήτων, πώς να αποφύγετε τα πιο κοινά λάθη, και τι να κάνετε αν χρειαστεί να υποστηρίξετε παλαιότερες εκδόσεις του Excel.

---

## Τι θα χρειαστείτε

- **.NET 6+** (ή .NET Framework 4.6+). Ο κώδικας λειτουργεί σε οποιοδήποτε πρόσφατο runtime.
- **Aspose.Cells for .NET** (δωρεάν δοκιμή ή με άδεια). Παρέχει τις κλάσεις `Workbook`, `Worksheet` και `CustomProperties` που χρησιμοποιούνται παρακάτω.
- Ένα IDE που προτιμάτε – Visual Studio, Rider ή ακόμη και VS Code αρκεί.
- Πρόσβαση εγγραφής σε φάκελο όπου θα αποθηκευτεί το παραγόμενο αρχείο.

Δεν απαιτούνται άλλες βιβλιοθήκες τρίτων.

---

## Βήμα 1: Εγκατάσταση Aspose.Cells

Για να ξεκινήσετε, προσθέστε το πακέτο NuGet Aspose.Cells στο έργο σας:

```bash
dotnet add package Aspose.Cells
```

> **Pro tip:** Αν εργάζεστε σε διακομιστή CI, αποθηκεύστε το κλειδί άδειας σε μια μεταβλητή περιβάλλοντος και φορτώστε το κατά την εκτέλεση – αυτό αποτρέπει το υδατογράφημα “evaluation” να εμφανιστεί στο αποτέλεσμα.

---

## Βήμα 2: Δημιουργία βιβλίου εργασίας Excel – Επισκόπηση

Η πρώτη πραγματική ενέργεια είναι να **δημιουργήσετε βιβλίο εργασίας Excel**. Αυτό το αντικείμενο αντιπροσωπεύει ολόκληρο το αρχείο στη μνήμη και σας δίνει πρόσβαση σε φύλλα, στυλ και προσαρμοσμένες ιδιότητες.

```csharp
using Aspose.Cells;

namespace ExcelDemo
{
    class Program
    {
        static void Main()
        {
            // Step 2.1: Instantiate a new workbook (empty by default)
            Workbook workbook = new Workbook();

            // The rest of the steps follow...
```

Γιατί να δημιουργήσετε ένα νέο `Workbook` αντί να φορτώσετε ένα πρότυπο; Ένα κενό βιβλίο εργασίας εγγυάται ότι δεν υπάρχουν κρυφά στυλ ή υπόλοιπες προσαρμοσμένες ιδιότητες, κάτι που είναι ιδιαίτερα σημαντικό όταν σκοπεύετε να **γράψετε δυαδικό αρχείο excel** για συστήματα downstream που αναμένουν καθαρό περιβάλλον.

---

## Βήμα 3: Ορισμός ονόματος φύλλου εργασίας (και γιατί έχει σημασία)

Τα φύλλα του Excel προεπιλογή είναι “Sheet1”, “Sheet2”, κ.λπ. Η ανάθεση σε ένα φύλλο ενός περιγραφικού ονόματος κάνει την επεξεργασία downstream—όπως Power Query ή μακροεντολές VBA—πολύ πιο ευανάγνωστη.

```csharp
            // Step 3.1: Grab the first worksheet (index 0) and rename it
            Worksheet worksheet = workbook.Worksheets[0];
            worksheet.Name = "Data"; // clear, concise, and self‑describing
```

Αν προσπαθήσετε να ορίσετε ένα διπλό όνομα, το Aspose.Cells θα ρίξει ένα `ArgumentException`. Για να είστε ασφαλείς, μπορείτε να ελέγξετε `Worksheets.Exists("Data")` πριν το μετονομάσετε.

---

## Βήμα 4: Προσθήκη προσαρμοσμένων ιδιοτήτων

Οι προσαρμοσμένες ιδιότητες αποθηκεύονται στο εσωτερικό XML του βιβλίου εργασίας και ταξιδεύουν με το αρχείο ανεξάρτητα από τη μορφή. Είναι ιδανικές για την ενσωμάτωση στοιχείων όπως `ReportId` ή `GeneratedBy`.

```csharp
            // Step 4.1: Add a numeric property
            workbook.CustomProperties.Add("ReportId", 12345);

            // Step 4.2: Add a string property
            workbook.CustomProperties.Add("GeneratedBy", "MyApp");
```

> **Γιατί να χρησιμοποιήσετε προσαρμοσμένες ιδιότητες;**  
> • Είναι προσβάσιμες μέσω του πίνακα “File → Info → Properties” του Excel.  
> • Ο κώδικας που καταναλώνει το βιβλίο εργασίας μπορεί να τις διαβάσει χωρίς να σαρώσει το περιεχόμενο των κελιών.  
> • Επιβιώνουν τις μετατροπές μορφής (XLSX ↔ XLSB) επειδή αποτελούν μέρος των μεταδεδομένων του αρχείου.

Μπορείτε επίσης να αποθηκεύσετε ημερομηνίες, boolean ή ακόμη και δυαδικά blob, αλλά κρατήστε το φορτίο μικρό—το Excel δεν είναι βάση δεδομένων.

---

## Βήμα 5: Αποθήκευση ως XLSB (Γραφή δυαδικού αρχείου Excel)

Η μορφή XLSB αποθηκεύει τα δεδομένα σε δυαδική δομή, κάτι που κάνει το αρχείο μικρότερο και πιο γρήγορο στο άνοιγμα. Πιο σημαντικό για αυτό το tutorial, **οι προσαρμοσμένες ιδιότητες ενσωματώνονται στο δυαδικό ρεύμα**, εξασφαλίζοντας ότι ταξιδεύουν μαζί με το αρχείο.

```csharp
            // Step 5.1: Define the output path
            string outputPath = Path.Combine(
                Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
                "WithCustomProps.xlsb");

            // Step 5.2: Save the workbook as a binary XLSB file
            workbook.Save(outputPath, SaveFormat.Xlsb);

            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

### Αναμενόμενο αποτέλεσμα

Μετά την εκτέλεση του προγράμματος, θα βρείτε το `WithCustomProps.xlsb` στην επιφάνεια εργασίας σας. Ανοίξτε το στο Excel, μεταβείτε σε **File → Info → Properties**, και θα δείτε τα `ReportId` και `GeneratedBy` να εμφανίζονται κάτω από *Custom*.

---

## Βήμα 6: Ακραίες περιπτώσεις & Συχνές ερωτήσεις

### Τι γίνεται αν ο φάκελος προορισμού είναι μόνο για ανάγνωση;

Τυλίξτε την κλήση `Save` σε ένα `try/catch` block και επιστρέψτε σε μια τοποθεσία εγγραφής από τον χρήστη, όπως `%TEMP%`. Αυτό αποτρέπει την κατάρρευση της εφαρμογής λόγω σφαλμάτων δικαιωμάτων.

```csharp
try
{
    workbook.Save(outputPath, SaveFormat.Xlsb);
}
catch (UnauthorizedAccessException)
{
    string fallback = Path.GetTempFileName().Replace(".tmp", ".xlsb");
    workbook.Save(fallback, SaveFormat.Xlsb);
    Console.WriteLine($"Saved to fallback location: {fallback}");
}
```

### Μπορώ να **αποθηκεύσω ως XLSX** και να διατηρήσω τις προσαρμοσμένες ιδιότητες;

Ναι—απλώς αλλάξτε το `SaveFormat.Xlsb` σε `SaveFormat.Xlsx`. Οι ιδιότητες αποθηκεύονται στο ίδιο τμήμα XML, οπότε επιβιώνουν την αλλαγή μορφής. Ωστόσο, τα αρχεία XLSX είναι μεγαλύτερα επειδή είναι συμπιεσμένο XML, ενώ το XLSB προσφέρει καλύτερη απόδοση για μεγάλα σύνολα δεδομένων.

### Πώς μπορώ να διαβάσω τις προσαρμοσμένες ιδιότητες αργότερα;

```csharp
Workbook loaded = new Workbook(outputPath);
foreach (CustomProperty prop in loaded.CustomProperties)
{
    Console.WriteLine($"{prop.Name} = {prop.Value}");
}
```

Αυτό το απόσπασμα κώδικα εκτυπώνει κάθε προσαρμοσμένη ιδιότητα, κάνοντας εύκολο για τις υπηρεσίες downstream να επαληθεύσουν την προέλευση του αρχείου.

---

## Παράδειγμα πλήρους λειτουργικού κώδικα

Παρακάτω βρίσκεται το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε‑και‑επικολλήσετε σε ένα νέο έργο κονσόλας. Δεν λείπουν κομμάτια—όλα, από τις δηλώσεις `using` μέχρι το τελικό `Console.WriteLine`, περιλαμβάνονται.

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a new workbook instance
            Workbook workbook = new Workbook();

            // 2️⃣ Access the first worksheet and give it a meaningful name
            Worksheet worksheet = workbook.Worksheets[0];
            worksheet.Name = "Data";

            // 3️⃣ Add custom properties (they travel with the file)
            workbook.CustomProperties.Add("ReportId", 12345);
            workbook.CustomProperties.Add("GeneratedBy", "MyApp");

            // 4️⃣ Define where to save the binary XLSB file
            string outputPath = Path.Combine(
                Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
                "WithCustomProps.xlsb");

            // 5️⃣ Save the workbook as a binary XLSB file
            try
            {
                workbook.Save(outputPath, SaveFormat.Xlsb);
                Console.WriteLine($"✅ Workbook saved to {outputPath}");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"❌ Failed to save workbook: {ex.Message}");
            }
        }
    }
}
```

Εκτελέστε το πρόγραμμα, ανοίξτε το παραγόμενο αρχείο και επαληθεύστε τις προσαρμοσμένες ιδιότητες. Αυτή είναι η ολόκληρη διαδικασία **create excel workbook**, **add custom properties**, **set worksheet name**, και **save as xlsb** σε μια καθαρή ροή.

---

## Συμπέρασμα

Τώρα ξέρετε ακριβώς πώς να **create Excel workbook**, να δώσετε στο φύλλο του ένα σαφές **set worksheet name**, να ενσωματώσετε χρήσιμα μεταδεδομένα με **add custom properties**, και τελικά να **save as XLSB** για να παραγάγετε ένα συμπαγές, δυαδικό αρχείο Excel. Αυτή η ροή εργασίας είναι αξιόπιστη, λειτουργεί σε διάφορες εκδόσεις .NET και κλιμακώνεται άψογα είτε δημιουργείτε μία αναφορά είτε χίλιες.

Τι ακολουθεί; Δοκιμάστε να προσθέσετε έναν πίνακα δεδομένων στο φύλλο “Data”, πειραματιστείτε με διαφορετικούς τύπους ιδιοτήτων (ημερομηνίες, boolean), ή αλλάξτε την έξοδο σε **save as xlsb** για τεράστια σύνολα δεδομένων. Μπορείτε επίσης να εξερευνήσετε την προστασία του βιβλίου εργασίας με κωδικό πρόσβασης—το Aspose.Cells το κάνει με μία μόνο γραμμή κώδικα.

Μη διστάσετε να αφήσετε ένα σχόλιο αν συναντήσετε δυσκολίες, ή να μοιραστείτε πώς έχετε επεκτείνει αυτό το μοτίβο στα δικά σας έργα. Καλή προγραμματιστική!  

---  

![Create Excel workbook screenshot](image.png){alt="Δημιουργία βιβλίου εργασίας Excel με προσαρμοσμένες ιδιότητες"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}