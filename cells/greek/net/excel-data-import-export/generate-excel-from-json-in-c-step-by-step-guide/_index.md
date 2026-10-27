---
category: general
date: 2026-03-18
description: Μάθετε πώς να δημιουργείτε Excel από JSON με C#, να επιτρέπετε διπλά
  ονόματα φύλλων, να δημιουργείτε φύλλο λεπτομερειών και να αποθηκεύετε το βιβλίο
  εργασίας C# σε λίγα λεπτά.
draft: false
keywords:
- generate excel from json
- allow duplicate sheet names
- how to create detail sheet
- save workbook c#
- smartmarker options
- aspnet cells integration
language: el
og_description: Δημιουργήστε Excel από JSON με χρήση C#. Αυτός ο οδηγός δείχνει πώς
  να επιτρέψετε διπλά ονόματα φύλλων, να δημιουργήσετε ένα φύλλο λεπτομερειών και
  να αποθηκεύσετε το βιβλίο εργασίας C# με το Aspose.Cells.
og_title: Δημιουργία Excel από JSON σε C# – Πλήρης οδηγός
tags:
- C#
- Excel automation
- JSON
- Aspose.Cells
title: Δημιουργία Excel από JSON σε C# – Οδηγός βήμα‑προς‑βήμα
url: /el/net/excel-data-import-export/generate-excel-from-json-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία Excel από JSON σε C# – Οδηγός Βήμα‑βήμα

Κάποτε χρειάστηκε να **δημιουργήσετε Excel από JSON** αλλά δεν ήξερες ποια βιβλιοθήκη μπορεί να αναλάβει τη βαριά δουλειά; Δεν είσαι μόνος. Σε πολλές επιχειρησιακές εφαρμογές λαμβάνουμε payloads ως JSON και πρέπει να τα μεταφέρουμε σε καλά μορφοποιημένα φύλλα εργασίας — σκεφτείτε αναφορές πωλήσεων, αποθέματα ή αρχεία ελέγχου. Τα καλά νέα; Με τη μηχανή SmartMarker του Aspose.Cells μπορείτε να μετατρέψετε μια συμβολοσειρά JSON σε πλήρες αρχείο Excel με λίγες μόνο γραμμές κώδικα.

Σε αυτό το tutorial θα περάσουμε από όλη τη διαδικασία: από την προετοιμασία του JSON payload, τη ρύθμιση του SmartMarker για **να επιτρέπει διπλά ονόματα φύλλων**, τη δημιουργία ενός **φύλλου λεπτομερειών**, και τέλος το **αποθήκευση του workbook C#**. Στο τέλος θα έχετε ένα επαναχρησιμοποιήσιμο snippet που μπορείτε να ενσωματώσετε σε οποιοδήποτε .NET project.

> **Σύντομη ανακεφαλαίωση:**  
> • Κύριος στόχος – δημιουργία Excel από JSON.  
> • Δευτερεύοντες στόχοι – να επιτρέπεται διπλό όνομα φύλλου, δημιουργία φύλλου λεπτομερειών, αποθήκευση workbook C#.  

## Προαπαιτούμενα

Πριν προχωρήσουμε, βεβαιωθείτε ότι έχετε:

- .NET 6.0 SDK (ή οποιαδήποτε πρόσφατη έκδοση .NET).  
- Visual Studio 2022 ή VS Code με την επέκταση C#.  
- Ένα ενεργό license ή δωρεάν δοκιμή του **Aspose.Cells for .NET** (το πακέτο NuGet είναι `Aspose.Cells`).  
- Ένα πρότυπο αρχείο Excel (`template.xlsx`) που περιέχει ήδη SmartMarker tags όπως `&=Name` και ένα placeholder πίνακα λεπτομερειών.

Αν κάτι από αυτά σας είναι άγνωστο, μην ανησυχείτε — η εγκατάσταση του πακέτου NuGet είναι μια εντολή, και το πρότυπο μπορεί να είναι ένα απλό workbook με μερικά κελιά placeholder.

## Επισκόπηση της Λύσης

Σε υψηλό επίπεδο θα:

1. Ορίσουμε μια συμβολοσειρά JSON που αντικατοπτρίζει τα δεδομένα που θέλουμε στο φύλλο.  
2. Ρυθμίσουμε το `SmartMarkerOptions` ώστε να επιτρέπονται διπλά ονόματα φύλλων και να δίνεται ένα προβλέψιμο όνομα σε **φύλλο λεπτομερειών**.  
3. Φορτώσουμε το πρότυπο Excel που περιέχει τα SmartMarker tags.  
4. Εκτελέσουμε τον SmartMarker processor για να συγχωνεύσουμε τα δεδομένα JSON στο workbook.  
5. Αποθηκεύσουμε το τελικό αρχείο με `workbook.Save(...)`.

Κάθε βήμα εξηγείται παρακάτω, με πλήρη αποσπάσματα κώδικα και γιατί είναι σημαντικό.

---

## Βήμα 1 – Προετοιμασία του JSON payload που θα συγχωνεύσετε

Το πρώτο πράγμα που χρειάζεστε είναι ένα έγγραφο JSON που ταιριάζει με τα SmartMarker tags μέσα στο πρότυπό σας. Σκεφτείτε το JSON ως την πηγή αλήθειας· κάθε κλειδί γίνεται placeholder στο αρχείο Excel.

```csharp
// Step 1: Define the JSON data that will be merged into the worksheet
string jsonData = @"{
    ""Name"": ""John"",
    ""Date"": ""2023-01-01"",
    ""Orders"": [
        { ""Item"": ""Laptop"", ""Qty"": 2, ""Price"": 1200 },
        { ""Item"": ""Mouse"",  ""Qty"": 5, ""Price"": 25 }
    ]
}";
```

**Γιατί είναι σημαντικό:**  
Το SmartMarker διαβάζει την ιεραρχία του JSON και αυτόματα επεκτείνει πίνακες για συλλογές όπως `Orders`. Αν η δομή του JSON δεν ευθυγραμμίζεται με τα tags, η συγχώνευση θα παράγει σιωπηλά κενές γραμμές — ένα συχνό λάθος.

---

## Βήμα 2 – Ρύθμιση του SmartMarker για να επιτρέπει διπλά ονόματα φύλλων και ονομασία του φύλλου λεπτομερειών

Από προεπιλογή το Aspose.Cells απαγορεύει διπλά ονόματα φύλλων, κάτι που μπορεί να είναι εμπόδιο όταν δημιουργείτε ένα φύλλο λεπτομερειών για κάθε κύριο record. Η κλάση `SmartMarkerOptions` σας επιτρέπει να χαλαρώσετε αυτόν τον κανόνα και επίσης να ορίσετε ένα μοτίβο ονομασίας για τα νεοδημιουργημένα φύλλα λεπτομερειών.

```csharp
// Step 2: Create SmartMarker options and allow duplicate base names for detail sheets
var smartMarkerOptions = new Aspose.Cells.SmartMarker.SmartMarkerOptions
{
    // When a detail sheet is generated, it will be named "Detail", "Detail (2)", etc.
    DetailSheetNewName = "Detail",

    // This flag tells the engine that duplicate sheet names are acceptable.
    // Useful when you generate multiple detail sheets from a loop.
    AllowDuplicateSheetNames = true
};
```

**Γιατί είναι σημαντικό:**  
Αν κάνετε βρόχο πάνω από πολλούς πελάτες και κάθε επανάληψη δημιουργεί νέο φύλλο, η μηχανή κανονικά θα πετάξει εξαίρεση. Ορίζοντας το `AllowDuplicateSheetNames` σε `true` λέτε στο Aspose.Cells να προσθέτει αυτόματα αριθμητικό επίθημα, διατηρώντας τη διαδικασία ομαλή.

---

## Βήμα 3 – Φόρτωση του πρότυπου Excel που περιέχει SmartMarker tags

Το πρότυπό σας είναι ο καμβάς όπου το SmartMarker θα "ζωγραφίσει" τα δεδομένα. Μπορεί να περιέχει οποιαδήποτε μορφοποίηση — χρώματα, τύπους, γραφήματα — ώστε να μην χρειάζεται να ξαναδημιουργήσετε αυτή τη λογική προγραμματιστικά.

```csharp
// Step 3: Load the workbook that contains SmartMarker tags
using var workbook = new Aspose.Cells.Workbook(@"C:\MyProjects\ExcelDemo\template.xlsx");
```

**Συμβουλή:**  
Κρατήστε το πρότυπο σε φάκελο που αποτελεί μέρος του output του project (π.χ., `Content\Templates`). Με αυτόν τον τρόπο μπορείτε να το αναφέρετε με σχετική διαδρομή και να αποφύγετε το σκληρό κωδικοποίηση απόλυτων διαδρομών.

---

## Βήμα 4 – Εκτέλεση του SmartMarker processor με το JSON και τις επιλογές

Τώρα συμβαίνει η μαγεία. Ο `SmartMarkerProcessor` διαβάζει το JSON, σέβεται τις επιλογές που ορίσατε, και γεμίζει το workbook αναλόγως.

```csharp
// Step 4: Process the SmartMarker tags using the JSON data and the configured options
workbook.SmartMarkerProcessor.Process(jsonData, smartMarkerOptions);
```

**Τι συμβαίνει στο παρασκήνιο;**  
- Ο επεξεργαστής σαρώνει κάθε κελί για markers όπως `&=Name` ή `&=Orders.Item`.  
- Αντικαθιστά απλούς markers με τιμές scalar (`Name`, `Date`).  
- Για συλλογές (`Orders`), δημιουργεί ένα νέο φύλλο λεπτομερειών (ονομαζόμενο “Detail”) και γεμίζει μια γραμμή πίνακα για κάθε στοιχείο.  
- Επειδή επιτρέψαμε διπλά ονόματα φύλλων, αν το πρότυπο είχε ήδη φύλλο με όνομα “Detail”, η μηχανή θα δημιουργήσει “Detail (2)”.

---

## Βήμα 5 – Αποθήκευση του συγχωνευμένου workbook στον δίσκο

Τέλος, γράψτε το γεμάτο workbook σε αρχείο. Μπορείτε να επιλέξετε οποιαδήποτε μορφή υποστηρίζεται από το Aspose.Cells — XLSX, CSV, PDF κ.λπ. Εδώ θα μείνουμε στο σύγχρονο XLSX.

```csharp
// Step 5: Save the workbook with the merged data
workbook.Save(@"C:\MyProjects\ExcelDemo\output.xlsx");
```

**Γιατί είναι σημαντικό:**  
Η αποθήκευση είναι το σημείο όπου πραγματικά **αποθηκεύετε το workbook C#**. Αν χρειαστεί να στείλετε το αρχείο σε web client, μπορείτε να χρησιμοποιήσετε `workbook.Save(Stream, SaveFormat.Xlsx)` αντί.

---

## Πλήρες Παράδειγμα Εργασίας

Συνδυάζοντας τα παραπάνω, εδώ είναι μια πλήρης, έτοιμη‑για‑εκτέλεση console εφαρμογή. Βεβαιωθείτε ότι έχετε εγκαταστήσει το πακέτο NuGet `Aspose.Cells` (`dotnet add package Aspose.Cells`) πριν τη μεταγλώττιση.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.SmartMarker;

namespace ExcelFromJsonDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Define the JSON payload
            string jsonData = @"{
                ""Name"": ""John"",
                ""Date"": ""2023-01-01"",
                ""Orders"": [
                    { ""Item"": ""Laptop"", ""Qty"": 2, ""Price"": 1200 },
                    { ""Item"": ""Mouse"",  ""Qty"": 5, ""Price"": 25 }
                ]
            }";

            // 2️⃣ Configure SmartMarker options – allow duplicate sheet names & set detail sheet name
            var smartMarkerOptions = new SmartMarkerOptions
            {
                DetailSheetNewName = "Detail",
                AllowDuplicateSheetNames = true
            };

            // 3️⃣ Load the template workbook (ensure the path is correct)
            var workbookPath = @"C:\MyProjects\ExcelDemo\template.xlsx";
            using var workbook = new Workbook(workbookPath);

            // 4️⃣ Merge JSON data into the workbook
            workbook.SmartMarkerProcessor.Process(jsonData, smartMarkerOptions);

            // 5️⃣ Save the result
            var outputPath = @"C:\MyProjects\ExcelDemo\output.xlsx";
            workbook.Save(outputPath);

            Console.WriteLine($"✅ Excel file generated successfully at: {outputPath}");
        }
    }
}
```

### Αναμενόμενο Αποτέλεσμα

- **Φύλλο 1** (το κύριο φύλλο) θα εμφανίζει “John” στο κελί `Name` και “2023‑01‑01” στο κελί `Date`.  
- Ένα νέο **Φύλλο Detail** θα εμφανιστεί, περιέχοντας έναν πίνακα με δύο γραμμές: μία για την παραγγελία Laptop και μία για την παραγγελία Mouse.  
- Αν το πρότυπο είχε ήδη φύλλο με όνομα “Detail”, το νέο φύλλο θα ονομαστεί “Detail (2)”, χάρη στη σημαία `AllowDuplicateSheetNames`.

![Excel output showing master sheet with name and date, plus a Detail sheet with order rows](excel-output.png "generate excel from json result")

*Image alt text:* **generate excel from json – example workbook with master and detail sheets**

---

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

### Τι γίνεται αν το JSON μου περιέχει ένθετες συλλογές;

Το SmartMarker μπορεί να διαχειριστεί ένθετους πίνακες, αλλά θα χρειαστεί να προσθέσετε επιπλέον φύλλα λεπτομερειών ή να χρησιμοποιήσετε ιεραρχικά markers. Για παράδειγμα, `&=Orders.SubItems.Product` θα δημιουργήσει αυτόματα τρίτο επίπεδο φύλλου.

### Πώς προσαρμόζω το μοτίβο ονομασίας για διπλά φύλλα;

Αντί ενός στατικού `DetailSheetNewName`, μπορείτε να αναθέσετε μια callback μέσω `smartMarkerOptions.DetailSheetNameGenerator`. Αυτό σας επιτρέπει να ενσωματώσετε timestamps ή μοναδικά IDs στο όνομα του φύλλου.

```csharp
smartMarkerOptions.DetailSheetNameGenerator = (baseName, index) =>
    $"{baseName}_{DateTime.Now:yyyyMMdd}_{index}";
```

### Μπορώ να δημιουργήσω CSV αντί για XLSX;

Απολύτως. Αντικαταστήστε την τελική κλήση `Save` με:

```csharp
workbook.Save(outputPath, SaveFormat.Csv);
```

Το υπόλοιπο pipeline παραμένει αμετάβλητο.

### Λειτουργεί αυτό σε ASP.NET Core;

Ναι. Ο ίδιος κώδικας μπορεί να τρέξει μέσα σε μια δράση controller. Απλώς στείλτε το workbook ως ροή στην απόκριση:

```csharp
using var ms = new MemoryStream();
workbook.Save(ms, SaveFormat.Xlsx);
ms.Position = 0;
return File(ms, "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet", "report.xlsx");
```

---

## Pro Συμβουλές & Πιθανά Πάγια

- **Pro tip:** Κρατήστε τα SmartMarker tags σε ξεχωριστό “Template” φύλλο. Έτσι μπορείτε να προστατεύετε το φύλλο από τυχαίες επεμβάσεις ενώ το processor μπορεί να το διαβάσει.  
- **Προσοχή σε:** Κλειδιά JSON που περιέχουν κενά ή ειδικούς χαρακτήρες. Το Aspose.Cells περιμένει έγκυρους JavaScript identifiers· μετονομάστε τα ή χρησιμοποιήστε το attribute `JsonProperty` αν κάνετε deserialization από POCO.  
- **Συμβουλή απόδοσης:** Αν επεξεργάζεστε χιλιάδες γραμμές, ορίστε `smartMarkerOptions.EnableCache = true` για επαναχρησιμοποίηση των compiled markers.  
- **Έλεγχος έκδοσης:** Ο παραπάνω κώδικας στοχεύει στο Aspose.Cells 23.9+. Παλαιότερες εκδόσεις ίσως να μην υποστηρίζουν το `AllowDuplicateSheetNames`.

---

## Συμπέρασμα

Τώρα έχετε μια πλήρη, end‑to‑end συνταγή για **δημιουργία Excel από JSON** σε C#. Ρυθμίζοντας το `SmartMarkerOptions` δείξαμε πώς να **επιτρέπουμε διπλά ονόματα φύλλων**, να ελέγχουμε την ονομασία του **φύλλου λεπτομερειών**, και τέλος να **αποθηκεύουμε το workbook C#**. Η προσέγγιση είναι απολύτως αυτοσχεδιαστική — χωρίς εξωτερικές υπηρεσίες, μόνο ένα πακέτο NuGet.

Τι θα κάνετε μετά; Δοκιμάστε να αντικαταστήσετε την πηγή JSON με ένα πραγματικό API

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}