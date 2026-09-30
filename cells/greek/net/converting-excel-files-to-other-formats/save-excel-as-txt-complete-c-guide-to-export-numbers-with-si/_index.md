---
category: general
date: 2026-02-21
description: Αποθηκεύστε το Excel ως txt με ακριβή έλεγχο των σημαντικών ψηφίων. Εξάγετε
  το Excel σε txt με C# και ορίστε εύκολα τα σημαντικά ψηφία.
draft: false
keywords:
- save excel as txt
- export excel to txt
- set significant digits
- save workbook as text
- export numbers to txt
language: el
og_description: Αποθηκεύστε το Excel ως txt γρήγορα. Μάθετε πώς να εξάγετε το Excel
  σε txt, να ορίσετε σημαντικά ψηφία και να ελέγχετε την έξοδο κειμένου χρησιμοποιώντας
  C#.
og_title: Αποθήκευση Excel ως txt – Εξαγωγή αριθμών με σημαντικά ψηφία σε C#
tags:
- C#
- Aspose.Cells
- Excel automation
title: Αποθήκευση του Excel ως txt – Πλήρης οδηγός C# για εξαγωγή αριθμών με σημαντικά
  ψηφία
url: /el/net/converting-excel-files-to-other-formats/save-excel-as-txt-complete-c-guide-to-export-numbers-with-si/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Αποθήκευση Excel ως txt – Πλήρης Οδηγός C# για Εξαγωγή Αριθμών με Σημαντικά Ψηφία

Έχετε ποτέ χρειαστεί να **αποθηκεύσετε το Excel ως txt** αλλά ανησυχείτε ότι οι αριθμοί θα χάσουν την ακρίβειά τους; Δεν είστε μόνοι. Πολλοί προγραμματιστές συναντούν πρόβλημα όταν προσπαθούν να εξάγουν το Excel σε txt και καταλήγουν είτε με πάρα πολλά δεκαδικά ψηφία είτε με ένα στρογγυλοποιημένο χάος.  

Σε αυτό το tutorial θα σας δείξουμε έναν απλό τρόπο να **εξάγετε το Excel σε txt** ενώ **ορίζετε τα σημαντικά ψηφία** ώστε το αποτέλεσμα να φαίνεται ακριβώς όπως το θέλετε. Στο τέλος θα έχετε ένα έτοιμο προς εκτέλεση απόσπασμα C# που αποθηκεύει ένα workbook ως κείμενο, εξάγει αριθμούς σε txt και σας δίνει πλήρη έλεγχο πάνω στη μορφή των αριθμών.

## Τι Θα Μάθετε

- Πώς να δημιουργήσετε ένα νέο workbook και να γράψετε αριθμητικά δεδομένα.  
- Τον σωστό τρόπο για **ορισμό σημαντικών ψηφίων** χρησιμοποιώντας `TxtSaveOptions`.  
- Πώς να **αποθηκεύσετε το workbook ως κείμενο** και να επαληθεύσετε το αποτέλεσμα.  
- Διαχείριση ειδικών περιπτώσεων (μεγάλοι αριθμοί, αρνητικές τιμές, προβλήματα τοπικοποίησης).  
- Γρήγορες συμβουλές για περαιτέρω προσαρμογή του αποτελέσματος (αλλαγή διαχωριστικού, κωδικοποίηση).

### Προαπαιτούμενα

- .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί επίσης σε .NET Framework 4.6+).  
- Το πακέτο **Aspose.Cells** από NuGet (`Install-Package Aspose.Cells`).  
- Βασική κατανόηση της σύνταξης C# — δεν απαιτείται βαθιά γνώση του Excel interop.

> **Pro tip:** Αν χρησιμοποιείτε Visual Studio, ενεργοποιήστε *nullable reference types* (`<Nullable>enable</Nullable>`) για να εντοπίζετε πιθανά σφάλματα null νωρίς.

---

## Βήμα 1: Αρχικοποίηση του Workbook και Εγγραφή Αριθμού

Πρώτα, χρειαζόμαστε ένα αντικείμενο workbook. Σκεφτείτε το ως την αναπαράσταση σε μνήμη ενός αρχείου Excel.  

```csharp
using Aspose.Cells;
using System;

// Create a new workbook (starts with one worksheet by default)
var workbook = new Workbook();
var worksheet = workbook.Worksheets[0];

// Write a numeric value into cell A1 (row 0, column 0)
worksheet.Cells[0, 0].PutValue(12345.6789);
```

**Γιατί είναι σημαντικό:**  
Η δημιουργία του workbook προγραμματιστικά αποφεύγει το βάρος του COM interop, και η μέθοδος `PutValue` ανιχνεύει αυτόματα τον τύπο δεδομένων, διασφαλίζοντας ότι το κελί αντιμετωπίζεται ως αριθμός — όχι ως κείμενο.

---

## Βήμα 2: Διαμόρφωση του TxtSaveOptions για Έλεγχο Σημαντικών Ψηφίων

Η κλάση `TxtSaveOptions` είναι όπου συμβαίνει η μαγεία. Ορίζοντας το `SignificantDigits`, λέτε στο Aspose.Cells πόσα σημαντικά ψηφία θα διατηρηθούν όταν το αρχείο γραφτεί.

```csharp
// Configure text save options – keep only 4 significant digits
var txtSaveOptions = new TxtSaveOptions
{
    // 4 significant digits means 12345.6789 becomes 12350
    SignificantDigits = 4,

    // Optional: change delimiter if you need CSV‑style output
    // Delimiter = ',',

    // Optional: force UTF‑8 encoding for broader character support
    // Encoding = System.Text.Encoding.UTF8
};
```

**Γιατί πρέπει να το ορίσετε:**  
Όταν **εξάγετε αριθμούς σε txt**, συχνά χρειάζεστε μια σύντομη αναπαράσταση (π.χ. για συστήματα αναφοράς που δέχονται μόνο συγκεκριμένη ακρίβεια). Η ιδιότητα `SignificantDigits` εγγυάται συνεπή στρογγυλοποίηση ανεξάρτητα από το αρχικό μήκος του αριθμού.

---

## Βήμα 3: Αποθήκευση του Workbook ως Αρχείο Κειμένου

Τώρα γράφουμε το workbook στο δίσκο χρησιμοποιώντας τις επιλογές που ορίσαμε.

```csharp
// Define the output path – adjust to your environment
string outputPath = @"C:\Temp\Numbers.txt";

// Save the workbook as a .txt file with the configured options
workbook.Save(outputPath, txtSaveOptions);

Console.WriteLine($"Workbook saved as txt at: {outputPath}");
```

**Τι θα δείτε:**  
Ανοίξτε το `Numbers.txt` και θα δείτε μια μόνο γραμμή:

```
12350
```

Ο αρχικός `12345.6789` έχει στρογγυλοποιηθεί σε **τέσσερα σημαντικά ψηφία**, ακριβώς όπως ζητήθηκε.

---

## Βήμα 4: Επαλήθευση του Αποτελέσματος (Προαιρετικό αλλά Συνιστάται)

Οι αυτοματοποιημένες δοκιμές είναι καλή συνήθεια. Εδώ είναι ένας γρήγορος έλεγχος που μπορείτε να τρέξετε αμέσως μετά την αποθήκευση:

```csharp
// Read back the file to confirm the content
string fileContent = System.IO.File.ReadAllText(outputPath).Trim();

if (fileContent == "12350")
{
    Console.WriteLine("✅ Export succeeded – significant digits applied correctly.");
}
else
{
    Console.WriteLine($"⚠️ Unexpected output: {fileContent}");
}
```

Η εκτέλεση αυτού του μπλοκ θα εκτυπώσει ένα πράσινο ✔️ αν όλα ταιριάζουν, δίνοντάς σας εμπιστοσύνη ότι η λειτουργία **save excel as txt** λειτούργησε όπως αναμενόταν.

---

## Συνηθισμένες Παραλλαγές & Edge Cases

### Εξαγωγή Πολλαπλών Κελιών ή Περιοχών

Αν χρειάζεστε να **εξάγετε excel σε txt** για ολόκληρη περιοχή, απλώς γεμίστε περισσότερα κελιά πριν αποθηκεύσετε:

```csharp
worksheet.Cells[0, 1].PutValue(0.000123456);
worksheet.Cells[0, 2].PutValue(-98765.4321);
```

Οι ίδιες `TxtSaveOptions` θα εφαρμόσουν τον κανόνα των 4 ψηφίων σε κάθε τιμή, παράγοντας:

```
12350
0.0001235
-98800
```

### Αλλαγή του Διαχωριστικού

Κάποια downstream συστήματα απαιτούν τιμές διαχωρισμένες με tab. Ρυθμίστε το διαχωριστικό ως εξής:

```csharp
txtSaveOptions.Delimiter = '\t'; // Tab character
```

Τώρα κάθε κελί σε μια σειρά εμφανίζεται χωρισμένο με tab.

### Διαχείριση Τοπικοποιημένων Δεκαδικών Διαχωριστών

Αν το κοινό σας χρησιμοποιεί κόμματα για δεκαδικά, ορίστε την πολιτισμική ρύθμιση:

```csharp
txtSaveOptions.CultureInfo = new System.Globalization.CultureInfo("fr-FR");
```

Η έξοδος θα σεβαστεί την τοπική ρύθμιση, μετατρέποντας το `12350` σε `12 350` (διάστημα ως διαχωριστικό χιλιάδων στα γαλλικά).

---

## Πλήρες Παράδειγμα (Έτοιμο για Αντιγραφή‑Επικόλληση)

```csharp
using Aspose.Cells;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook and write numbers
        var workbook = new Workbook();
        var sheet = workbook.Worksheets[0];
        sheet.Cells[0, 0].PutValue(12345.6789);
        sheet.Cells[0, 1].PutValue(0.000123456);
        sheet.Cells[0, 2].PutValue(-98765.4321);

        // 2️⃣ Configure save options – 4 significant digits
        var txtOptions = new TxtSaveOptions
        {
            SignificantDigits = 4,
            // Delimiter = '\t',               // Uncomment for TSV
            // Encoding = System.Text.Encoding.UTF8,
            // CultureInfo = new System.Globalization.CultureInfo("en-US")
        };

        // 3️⃣ Save to text file
        string path = Path.Combine(Environment.GetFolderPath(Environment.SpecialFolder.Desktop), "Numbers.txt");
        workbook.Save(path, txtOptions);
        Console.WriteLine($"File saved to {path}");

        // 4️⃣ Verify result (optional)
        string result = File.ReadAllText(path).Trim();
        Console.WriteLine($"File content: {result}");
    }
}
```

**Αναμενόμενο περιεχόμενο του `Numbers.txt` (προεπιλεγμένο διαχωριστικό, 4 σημαντικά ψηφία):**

```
12350	0.0001235	-98800
```

Το tab (`\t`) εμφανίζεται επειδή αφήσαμε το διαχωριστικό στην προεπιλογή (tab) στο παράδειγμα· αλλάξτε το σε κόμμα αν προτιμάτε CSV.

---

## Συμπέρασμα

Τώρα ξέρετε ακριβώς **πώς να αποθηκεύσετε το Excel ως txt** ενώ ελέγχετε τον αριθμό των σημαντικών ψηφίων. Τα βήματα — δημιουργία workbook, ορισμός `TxtSaveOptions.SignificantDigits` και αποθήκευση — είναι ό,τι χρειάζεστε για αξιόπιστη **εξαγωγή excel σε txt**.  

Από εδώ μπορείτε:

- **Εξάγετε αριθμούς σε txt** για μεγαλύτερα σύνολα δεδομένων.  
- Προσαρμόσετε διαχωριστικά, κωδικοποίηση ή ρυθμίσεις πολιτισμού ώστε να ταιριάζουν σε οποιοδήποτε downstream σύστημα.  
- Συνδυάστε αυτήν την προσέγγιση με άλλες δυνατότητες του Aspose.Cells (στυλ, τύπους) πριν την εξαγωγή.

Δοκιμάστε το, αλλάξτε το `SignificantDigits` σε 2 ή 6 και δείτε πώς αλλάζει η έξοδος. Η ευελιξία του **save workbook as text** το καθιστά χρήσιμο εργαλείο σε κάθε pipeline ανταλλαγής δεδομένων.

---

### Σχετικά Θέματα που Μπορείτε να Εξερευνήσετε Στη Σειρά

- **Export Excel to CSV** με προσαρμοσμένη σειρά στηλών.  
- **Read txt files back into a workbook** (`Workbook.Load` με `LoadOptions`).  
- **Batch processing** πολλαπλών φύλλων και ενοποίηση τους σε ένα αρχείο txt.  
- **Performance tuning** για εξαγωγές μεγάλης κλίμακας (streaming vs. in‑memory).

Μη διστάσετε να αφήσετε ένα σχόλιο αν αντιμετωπίσετε δυσκολίες, ή να μοιραστείτε πώς προσαρμόσατε την εξαγωγή στα δικά σας έργα. Καλό coding!  

---  

*Image: Ένα στιγμιότυπο του παραγόμενου αρχείου `Numbers.txt` που εμφανίζει στρογγυλοποιημένες τιμές.*  
*Alt text: “Αρχείο Numbers.txt που εμφανίζει 12350, 0.0001235, και -98800 μετά την αποθήκευση του Excel ως txt με 4 σημαντικά ψηφία.”*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}