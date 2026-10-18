---
category: general
date: 2026-03-25
description: Δημιουργήστε βιβλίο εργασίας Excel από JSON και αποθηκεύστε το ως xlsx.
  Μάθετε πώς να εξάγετε JSON σε xlsx, να δημιουργήσετε Excel από JSON και να γεμίσετε
  το Excel από JSON σε λίγα λεπτά.
draft: false
keywords:
- create excel workbook
- export json to xlsx
- generate excel from json
- populate excel from json
- save workbook as xlsx
language: el
og_description: Δημιουργήστε άμεσα ένα βιβλίο εργασίας Excel από JSON. Αυτός ο οδηγός
  δείχνει πώς να εξάγετε JSON σε xlsx, να δημιουργήσετε Excel από JSON και να γεμίσετε
  το Excel από JSON με το Aspose.Cells.
og_title: Δημιουργία βιβλίου εργασίας Excel από JSON – Πλήρες σεμινάριο C#
tags:
- Aspose.Cells
- C#
- JSON
- Excel automation
title: Δημιουργία βιβλίου εργασίας Excel από JSON – Οδηγός βήμα‑προς‑βήμα
url: /el/net/excel-data-import-export/create-excel-workbook-from-json-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία Excel Workbook από JSON – Πλήρες C# Tutorial

Κάποτε χρειάστηκε να **δημιουργήσετε excel workbook** από ένα JSON payload αλλά δεν ήξερες από πού να ξεκινήσεις; Δεν είσαι μόνος· πολλοί προγραμματιστές αντιμετωπίζουν το ίδιο πρόβλημα όταν προσπαθούν να μετατρέψουν δεδομένα API σε ένα τακτοποιημένο φύλλο εργασίας. Τα καλά νέα; Με λίγες γραμμές C# και Aspose.Cells μπορείς να **export json to xlsx**, **generate excel from json**, και **populate excel from json** χωρίς να χρησιμοποιήσεις τρίτους μετατροπείς.

Σε αυτόν τον οδηγό θα περάσουμε από όλη τη διαδικασία — ξεκινώντας από μια ακατέργαστη συμβολοσειρά JSON, τοποθετώντας την σε SmartMarker, και τελικά **save workbook as xlsx** στο δίσκο. Στο τέλος θα έχεις ένα έτοιμο Excel αρχείο που φαίνεται ως εξής:

| Name | Score |
|------|-------|
| John | 90    |
| Anna | 85    |

> **Pro tip:** Αν ήδη χρησιμοποιείς Aspose.Cells σε άλλο μέρος του έργου σου, μπορείς να επαναχρησιμοποιήσεις το ίδιο αντικείμενο `Workbook` για πολλαπλές εισαγωγές JSON — ιδανικό για επεξεργασία παρτίδων.

---

## What You’ll Need

- **.NET 6+** (ή οποιοδήποτε πρόσφατο .NET Framework που υποστηρίζει C# 10)
- **Aspose.Cells for .NET** – εγκατάσταση μέσω NuGet: `dotnet add package Aspose.Cells`
- Μια βασική κατανόηση της σύνταξης C# (δεν απαιτείται βαθιά γνώση του Excel)

Αυτό είναι όλο. Χωρίς εξωτερικές υπηρεσίες, χωρίς COM interop, μόνο καθαρός διαχειριζόμενος κώδικας.

---

## Step 1: Initialize a New Excel Workbook

Το πρώτο βήμα είναι να δημιουργήσουμε ένα νέο αντικείμενο workbook. Σκέψου το σαν το άνοιγμα ενός κεντρικού αρχείου Excel όπου θα ρίξουμε αργότερα τα δεδομένα μας.

```csharp
using Aspose.Cells;

// Step 1: Create a new workbook and grab the first worksheet
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];
```

Γιατί ξεκινάμε με νέο workbook; Εξασφαλίζει καθαρό ξεκίνημα, αποτρέπει την κληρονομιά στυλ από προηγούμενες εκτελέσεις και διατηρεί το μέγεθος του αρχείου ελάχιστο — ιδανικό για αυτοματοποιημένες γραμμές παραγωγής.

---

## Step 2: Prepare the JSON Data You Want to Import

Για την επίδειξη θα χρησιμοποιήσουμε έναν μικρό πίνακα JSON, αλλά μπορείς να τον αντικαταστήσεις με οποιοδήποτε έγκυρο JSON λαμβάνεις από web service, αρχείο ή ερώτημα βάσης δεδομένων.

```csharp
// Step 2: JSON string representing a simple collection of records
string jsonData = "[{\"Name\":\"John\",\"Score\":90},{\"Name\":\"Anna\",\"Score\":85}]";
```

Παρατήρησε τα διπλά‑escaped εισαγωγικά (`\"`) — είναι απλώς η σύνταξη string literal της C#. Σε πραγματικό σενάριο πιθανότατα θα διαβάζατε αυτό από αρχείο:

```csharp
// string jsonData = File.ReadAllText("data.json");
```

---

## Step 3: Tell SmartMarker to Treat the Whole Array as One Record

Η μηχανή SmartMarker του Aspose.Cells μπορεί να επαναλαμβάνει συλλογές αυτόματα. Ενεργοποιώντας το **ArrayAsSingle**, αντιμετωπίζουμε ολόκληρο τον πίνακα JSON ως ένα μόνο record, κάτι που χρειαζόμαστε για έναν επίπεδο πίνακα.

```csharp
// Step 3: Configure SmartMarker options – array‑as‑single mode
SmartMarkerOptions options = new SmartMarkerOptions
{
    ArrayAsSingle = true   // This makes the whole JSON array behave like one record
};
```

Αν ξεχάσεις αυτή τη σημαία, το SmartMarker θα προσπαθήσει να δημιουργήσει ξεχωριστό φύλλο για κάθε στοιχείο — σίγουρα όχι αυτό που θέλεις όταν παράγεις έναν απλό πίνακα.

---

## Step 4: Place a SmartMarker Token in the Worksheet

Τα tokens του SmartMarker έχουν μορφή `${jsonArray}`. Όταν εκτελείται ο επεξεργαστής, αντικαθιστά το token με τα δεδομένα από την πηγή JSON. Θα τοποθετήσουμε το token στο κελί **A1** ώστε η έξοδος να ξεκινά στην πάνω‑αριστερή γωνία.

```csharp
// Step 4: Insert the SmartMarker token into cell A1
worksheet.Cells["A1"].PutValue("${jsonArray}");
```

Μπορείς επίσης να μορφοποιήσεις εκ των προτέρων τη γραμμή κεφαλίδας πριν την επεξεργασία. Για παράδειγμα, ορισμός έντονου (bold) γραμματοσειράς στην πρώτη γραμμή:

```csharp
Cell headerCell = worksheet.Cells["A1"];
headerCell.Style.Font.IsBold = true;
```

---

## Step 5: Run the SmartMarker Processor

Τώρα συμβαίνει η μαγεία. Ο επεξεργαστής διαβάζει το JSON, αντιστοιχίζει κάθε ιδιότητα σε στήλη και γράφει τις γραμμές κάτω από το token.

```csharp
// Step 5: Process the SmartMarker with our JSON data and options
worksheet.SmartMarkerProcessor.Process(jsonData, options);
```

Πίσω από τις σκηνές, το Aspose.Cells:

1. Αναλύει το JSON σε αντικείμενο .NET.
2. Ταιριάζει τα ονόματα ιδιοτήτων (`Name`, `Score`) με τις κεφαλίδες των στηλών.
3. Γράφει κάθε στοιχείο του πίνακα ως νέα γραμμή.

Αν το JSON σου περιέχει ένθετα αντικείμενα, μπορείς να τα αναφέρεις με σημειογραφία τελείας (`${parent.child}`) — μια χρήσιμη δυνατότητα για πιο σύνθετες αναφορές.

---

## Step 6: Save the Workbook as an XLSX File

Τέλος, αποθήκευσε το workbook στο δίσκο. Η κατάληξη αρχείου `.xlsx` ενημερώνει το Excel (και τις περισσότερες άλλες εφαρμογές λογιστικών φύλλων) ότι πρόκειται για ένα OpenXML workbook.

```csharp
// Step 6: Save the workbook to a file
string outputPath = Path.Combine(Environment.CurrentDirectory, "json-single.xlsx");
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

Φυσικά, μπορείς να μεταφέρεις το workbook απευθείας σε HTTP response αν δημιουργείς web API:

```csharp
// Example for ASP.NET Core
using (var stream = new MemoryStream())
{
    workbook.Save(stream, SaveFormat.Xlsx);
    stream.Position = 0;
    return File(stream, "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet", "data.xlsx");
}
```

---

## Full Working Example

Παρακάτω βρίσκεται το πλήρες, έτοιμο‑για‑εκτέλεση πρόγραμμα που ενσωματώνει κάθε βήμα που περιγράφηκε παραπάνω. Αντέγραψε‑επικόλλησε το σε ένα νέο console project και πάτα **F5**.

```csharp
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ JSON data to be merged into the sheet
        string jsonData = "[{\"Name\":\"John\",\"Score\":90},{\"Name\":\"Anna\",\"Score\":85}]";

        // 3️⃣ Enable array‑as‑single mode so the whole array is one record
        SmartMarkerOptions options = new SmartMarkerOptions
        {
            ArrayAsSingle = true
        };

        // 4️⃣ Put a SmartMarker token in A1 that points to the JSON array
        worksheet.Cells["A1"].PutValue("${jsonArray}");

        // Optional: make the header bold for better readability
        worksheet.Cells["A1"].Style.Font.IsBold = true;

        // 5️⃣ Process the SmartMarker with the JSON payload
        worksheet.SmartMarkerProcessor.Process(jsonData, options);

        // 6️⃣ Save the result as an XLSX file
        string outputPath = Path.Combine(Environment.CurrentDirectory, "json-single.xlsx");
        workbook.Save(outputPath);

        Console.WriteLine($"✅ Workbook created and saved to: {outputPath}");
    }
}
```

**Expected result:** Το άνοιγμα του `json-single.xlsx` εμφανίζει δύο γραμμές κάτω από τη έντονη κεφαλίδα — `John` με σκορ `90` και `Anna` με `85`. Τα ονόματα των στηλών προκύπτουν αυτόματα από τα ονόματα ιδιοτήτων του JSON.

---

## Common Questions & Edge Cases

### What if my JSON keys contain spaces or special characters?

Το SmartMarker απαιτεί έγκυρα ονόματα αναγνωριστών. Αντικατέστησε τα κενά με underscores ή χρησιμοποίησε προσαρμοσμένο mapping:

```csharp
// Example JSON: {"First Name":"John"}
string jsonData = "[{\"First_Name\":\"John\",\"Score\":90}]";
// Token stays the same – Aspose.Cells will map "First_Name" to column header "First_Name"
```

### How do I export a large JSON array (thousands of rows)?

Ο επεξεργαστής μεταδίδει δεδομένα εσωτερικά, οπότε η χρήση μνήμης παραμένει μέτρια. Ωστόσο, μπορεί να θέλεις να:

- Αυξήσεις το όριο `MaxRows` του φύλλου (`worksheet.Cells.MaxRow = 1_048_576;` – το μέγιστο του Excel).
- Απενεργοποιήσεις τις γραμμές πλέγματος για απόδοση (`worksheet.IsGridlinesVisible = false;`).

### Can I add multiple JSON tables to the same workbook?

Βεβαίως. Απλώς τοποθέτησε διαφορετικά SmartMarker tokens σε ξεχωριστές περιοχές (π.χ., `${orders}` στο `A10`, `${customers}` στο `D1`) και κάλεσε `Process` μία φορά ανά token ή μία φορά με ένα σύνθετο JSON αντικείμενο που περιέχει και τους δύο πίνακες.

---

## Bonus: Adding a Simple Chart (Optional)

Αν θέλεις να οπτικοποιήσεις τα σκορ, πρόσθεσε ένα γρήγορο column chart μετά το γέμισμα των δεδομένων:

```csharp
// Insert a column chart starting at cell E1
int chartIndex = worksheet.Charts.Add(ChartType.Column, 0, 4, 15, 10);
Chart chart = worksheet.Charts[chartIndex];
chart.NSeries.Add("B2:B3", true);
chart.NSeries[0].Name = "Score";
chart.Title.Text = "Scores by Name";
```

Το διάγραμμα θα αναφερθεί αυτόματα στις νεοσυμπληρωμένες γραμμές, παρέχοντάς σου μια επαγγελματική αναφορά με ένα μόνο βήμα.

---

## Conclusion

Τώρα γνωρίζεις **πώς να δημιουργήσεις excel workbook** από μια συμβολοσειρά JSON, **export json to xlsx**, **generate excel from json**, και **populate excel from json** χρησιμοποιώντας τη δυνατότητα SmartMarker του Aspose.Cells. Η πλήρης λύση — αρχικοποίηση workbook, ρύθμιση SmartMarker, επεξεργασία JSON και αποθήκευση αρχείου — χωράει σε λίγες γραμμές κώδικα, αλλά κλιμακώνεται σε τεράστιες ποσότητες δεδομένων.

Τι θα κάνεις μετά; Δοκίμασε να αντικαταστήσεις το στατικό JSON με κλήση API, πρόσθεσε conditional formatting βάσει των σκορ, ή δημιούργησε πολλαπλά φύλλα για διαφορετικούς τομείς δεδομένων. Το ίδιο μοτίβο λειτουργεί για CSV, XML ή ακόμη και σύνολα αποτελεσμάτων βάσεων δεδομένων — απλώς άλλαξε τη συμβολοσειρά προέλευσης και προσαρμόζε το SmartMarker token.

Καλή προγραμματιστική δουλειά, και οι λογιστικές σου φύλλα να παραμένουν πάντα τακτοποιημένα!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}