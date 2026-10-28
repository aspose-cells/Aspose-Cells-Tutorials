---
category: general
date: 2026-04-07
description: Δημιουργήστε ένα βιβλίο εργασίας Excel, τυλίξτε τις στήλες στο Excel,
  υπολογίστε τύπους και αποθηκεύστε το βιβλίο εργασίας ως XLSX με βήμα‑βήμα κώδικα
  C#.
draft: false
keywords:
- create excel workbook
- wrap columns in excel
- save workbook as xlsx
- how to calculate formulas
- how to save excel
language: el
og_description: Δημιουργήστε βιβλίο εργασίας Excel, τυλίξτε στήλες στο Excel, υπολογίστε
  τύπους και αποθηκεύστε το βιβλίο εργασίας ως XLSX. Μάθετε τη διαδικασία πλήρως με
  εκτελέσιμο κώδικα.
og_title: Δημιουργία βιβλίου εργασίας Excel – Πλήρης οδηγός C#
tags:
- csharp
- aspnet
- excel
- automation
title: Δημιουργία βιβλίου εργασίας Excel – Αναδίπλωση στηλών και αποθήκευση ως XLSX
url: /el/net/formatting-rows-and-columns-in-excel/create-excel-workbook-wrap-columns-and-save-as-xlsx/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία Excel Workbook – Αναδίπλωση Στηλών και Αποθήκευση ως XLSX

Έχετε χρειαστεί ποτέ να **δημιουργήσετε Excel workbook** προγραμματιστικά και να αναρωτηθήκατε πώς να κάνετε τα δεδομένα να ταιριάζουν όμορφα σε μια διάταξη πολλαπλών στηλών; Δεν είστε μόνοι. Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από τη δημιουργία του workbook, την εφαρμογή του τύπου `WRAPCOLS` για **αναδίπλωση στηλών στο Excel**, την εξαναγκασμένη εκτέλεση του τύπου, και τέλος την **αποθήκευση του workbook ως XLSX** ώστε να μπορείτε να το ανοίξετε σε οποιοδήποτε πρόγραμμα λογιστικών φύλλων.

Θα απαντήσουμε επίσης στις αναπόφευκτες ερωτήσεις: *Πώς υπολογίζω τύπους εν κινήσει;* *Τι γίνεται αν χρειαστώ αλλαγή του αριθμού των στηλών;* και *Υπάρχει γρήγορος τρόπος να αποθηκεύσω το αρχείο;* Στο τέλος θα έχετε ένα αυτόνομο, έτοιμο‑για‑εκτέλεση απόσπασμα C# που κάνει όλα αυτά και μερικές επιπλέον συμβουλές που μπορείτε να αντιγράψετε στα δικά σας έργα.

## Προαπαιτούμενα

- .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί επίσης σε .NET Framework 4.6+)
- Η βιβλιοθήκη **Aspose.Cells** (ή οποιοδήποτε άλλο πακέτο επεξεργασίας Excel που υποστηρίζει `WRAPCOLS`; το παράδειγμα χρησιμοποιεί Aspose.Cells επειδή εκθέτει μια απλή μέθοδο `CalculateFormula`)
- Μια βασική εμπειρία με C# – αν μπορείτε να γράψετε `Console.WriteLine`, είστε έτοιμοι

> **Pro tip:** Αν δεν έχετε ακόμη άδεια για Aspose.Cells, μπορείτε να ζητήσετε ένα δωρεάν κλειδί δοκιμής από την ιστοσελίδα τους· η δοκιμή λειτουργεί τέλεια για εκπαιδευτικούς σκοπούς.

## Βήμα 1: Δημιουργία Excel Workbook

Το πρώτο πράγμα που χρειάζεστε είναι ένα κενό αντικείμενο workbook που αντιπροσωπεύει το αρχείο Excel στη μνήμη. Αυτό είναι ο πυρήνας της λειτουργίας **create Excel workbook**.

```csharp
using Aspose.Cells;

// Step 1: Instantiate a new workbook
Workbook workbook = new Workbook();

// Grab the first worksheet – it’s already there by default
Worksheet worksheet = workbook.Worksheets[0];
```

*Γιατί είναι σημαντικό:* Η κλάση `Workbook` είναι το σημείο εισόδου για οποιαδήποτε επεξεργασία Excel. Δημιουργώντας την πρώτα, ετοιμάζετε έναν καθαρό καμβά όπου οι επόμενες ενέργειες—όπως η αναδίπλωση στηλών—μπορούν να εφαρμοστούν χωρίς ανεπιθύμητες παρενέργειες.

## Βήμα 2: Συμπλήρωση Δειγματικών Δεδομένων (Προαιρετικό αλλά Χρήσιμο)

Πριν αναδιπλώσουμε τις στήλες, ας τοποθετήσουμε ένα μικρό σύνολο δεδομένων στην περιοχή `A1:D10`. Αυτό αντικατοπτρίζει μια πραγματική κατάσταση όπου έχετε έναν ακατέργαστο πίνακα που χρειάζεται αναδιαμόρφωση.

```csharp
// Fill A1:D10 with sample numbers for demonstration
for (int row = 0; row < 10; row++)
{
    for (int col = 0; col < 4; col++)
    {
        worksheet.Cells[row, col].PutValue(row * 4 + col + 1);
    }
}
```

Μπορείτε να παραλείψετε αυτό το μπλοκ αν έχετε ήδη δεδομένα στο φύλλο εργασίας· η λογική αναδίπλωσης λειτουργεί σε οποιαδήποτε υπάρχουσα περιοχή.

## Βήμα 3: Αναδίπλωση Στηλών στο Excel

Τώρα έρχεται το αστέρι της παράστασης: η συνάρτηση `WRAPCOLS`. Παίρνει μια πηγή περιοχής και έναν αριθμό στηλών, και στη συνέχεια «χύνεται» τα δεδομένα στη νέα διάταξη. Δείτε πώς να την εφαρμόσετε στο κελί **A1** ώστε το αποτέλεσμα να καταλαμβάνει τρεις στήλες.

```csharp
// Apply WRAPCOLS to A1 – the result will spill into a 3‑column layout
worksheet.Cells["A1"].Formula = "=WRAPCOLS(A1:D10,3)";
```

**Τι συμβαίνει στο παρασκήνιο;**  
`WRAPCOLS(A1:D10,3)` λέει στο Excel να διαβάσει τα 40 κελιά στο `A1:D10` και να τα γράψει γραμμή‑με‑γραμμή σε τρεις στήλες, δημιουργώντας αυτόματα όσες γραμμές χρειάζονται. Αυτό είναι ιδανικό για να μετατρέψετε μια μακριά λίστα σε μια πιο συμπαγή, στυλ εφημερίδας.

## Βήμα 4: Πώς να Υπολογίσετε Τύπους

Η τοποθέτηση ενός τύπου είναι μόνο το ήμισυ· το Excel δεν θα υπολογίσει το αποτέλεσμα μέχρι να ενεργοποιήσετε μια διαδικασία υπολογισμού. Στο Aspose.Cells το κάνετε με `CalculateFormula()`.

```csharp
// Force the workbook to evaluate all pending formulas
workbook.CalculateFormula();
```

> **Γιατί το χρειάζεστε:** Χωρίς την κλήση `CalculateFormula`, το κελί `A1` θα περιέχει μόνο τη συμβολοσειρά του τύπου όταν ανοίξετε το αρχείο, και η αναδιατεταγμένη διάταξη δεν θα εμφανιστεί μέχρι ο χρήστης να επανυπολογίσει χειροκίνητα.

## Βήμα 5: Αποθήκευση Workbook ως XLSX

Τέλος, αποθηκεύστε το workbook στο δίσκο. Η μέθοδος `Save` ανιχνεύει αυτόματα τη μορφή από την επέκταση του αρχείου, οπότε η χρήση του **.xlsx** εξασφαλίζει ότι θα λάβετε τη σύγχρονη μορφή Open XML.

```csharp
// Choose a folder you have write access to and save the file
string outputPath = @"C:\Temp\output.xlsx";
workbook.Save(outputPath);
```

Όταν ανοίξετε το `output.xlsx` στο Excel, θα δείτε τα αρχικά δεδομένα να είναι όμορφα αναδιπλωμένα σε τρεις στήλες, ξεκινώντας από το κελί **A1**. Το υπόλοιπο φύλλο παραμένει αμετάβλητο, κάτι που είναι χρήσιμο αν χρειάζεται να διατηρήσετε τον αρχικό πίνακα ως αναφορά.

### Αναμενόμενη Στιγμιότυπο Αποτελέσματος

<img src="images/wrapcols-result.png" alt="παράδειγμα δημιουργίας excel workbook" />

Η παραπάνω εικόνα απεικονίζει την τελική διάταξη: οι αριθμοί από το `A1:D10` εμφανίζονται πλέον σε τρεις στήλες, με γραμμές που δημιουργούνται αυτόματα για να φιλοξενήσουν όλες τις τιμές.

## Συνηθισμένες Παραλλαγές & Ακραίες Περιπτώσεις

### Αλλαγή του Αριθμού Στηλών

Αν χρειάζεστε διαφορετικό αριθμό στηλών, απλώς προσαρμόστε το δεύτερο όρισμα του `WRAPCOLS`:

```csharp
worksheet.Cells["A1"].Formula = "=WRAPCOLS(A1:D10,5)"; // five‑column layout
```

Θυμηθείτε να ξανατρέξετε το `CalculateFormula()` μετά από κάθε αλλαγή.

### Αναδίπλωση Μη Συνεχόμενων Περιοχών

Το `WRAPCOLS` λειτουργεί μόνο με συνεχόμενες περιοχές. Αν τα δεδομένα σας είναι κατανεμημένα σε πολλαπλές περιοχές, ενοποιήστε τα πρώτα (π.χ., χρησιμοποιώντας `UNION` σε μια βοηθητική στήλη) πριν την αναδίπλωση.

### Μεγάλα Σύνολα Δεδομένων

Για πολύ μεγάλους πίνακες, ο υπολογισμός μπορεί να διαρκέσει μερικά δευτερόλεπτα. Μπορείτε να βελτιώσετε την απόδοση απενεργοποιώντας τον αυτόματο υπολογισμό πριν ορίσετε τον τύπο και ενεργοποιώντας τον ξανά μετά:

```csharp
workbook.Settings.CalcMode = CalcMode.Manual;
worksheet.Cells["A1"].Formula = "=WRAPCOLS(A1:D1000,4)";
workbook.CalculateFormula();
workbook.Settings.CalcMode = CalcMode.Automatic;
```

### Αποθήκευση σε Stream

Αν δημιουργείτε ένα web API και θέλετε να επιστρέψετε το αρχείο απευθείας στον πελάτη, μπορείτε να γράψετε σε ένα `MemoryStream` αντί για φυσικό αρχείο:

```csharp
using var ms = new MemoryStream();
workbook.Save(ms, SaveFormat.Xlsx);
ms.Position = 0; // reset for reading
// return ms as a FileResult in ASP.NET Core, for example
```

## Πλήρες Παράδειγμα Λειτουργίας

Συνδυάζοντας όλα τα παραπάνω, εδώ είναι το πλήρες, έτοιμο‑για‑αντιγραφή πρόγραμμα:

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Fill A1:D10 with sample data (optional)
        for (int row = 0; row < 10; row++)
        {
            for (int col = 0; col < 4; col++)
            {
                worksheet.Cells[row, col].PutValue(row * 4 + col + 1);
            }
        }

        // 3️⃣ Apply WRAPCOLS to produce a 3‑column layout
        worksheet.Cells["A1"].Formula = "=WRAPCOLS(A1:D10,3)";

        // 4️⃣ Force calculation so the formula result is materialized
        workbook.CalculateFormula();

        // 5️⃣ Save the workbook as XLSX
        string outputPath = @"C:\Temp\output.xlsx";
        workbook.Save(outputPath);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

Εκτελέστε αυτό το πρόγραμμα, ανοίξτε το παραγόμενο `output.xlsx`, και θα δείτε τα δεδομένα αναδιπλωμένα ακριβώς όπως περιγράφηκε.

## Συμπέρασμα

Τώρα ξέρετε **πώς να δημιουργήσετε Excel workbook** αντικείμενα σε C#, να εφαρμόζετε τη δυναμική συνάρτηση `WRAPCOLS` για **αναδίπλωση στηλών στο Excel**, να **υπολογίζετε τύπους** κατά απαίτηση, και να **αποθηκεύετε το workbook ως XLSX** για περαιτέρω χρήση. Αυτή η ολοκληρωμένη ροή καλύπτει τα πιο κοινά σενάρια, από απλές επιδείξεις μέχρι παραγωγική αυτοματοποίηση.

### Τι Ακολουθεί;

- Πειραματιστείτε με άλλες δυναμικές συναρτήσεις όπως `FILTER`, `SORT` ή `UNIQUE`.
- Συνδυάστε το `WRAPCOLS` με μορφοποίηση υπό όρους για να επισημάνετε συγκεκριμένες γραμμές.
- Ενσωματώστε αυτή τη λογική σε ένα endpoint ASP.NET Core ώστε οι χρήστες να μπορούν να κατεβάσουν μια προσαρμοσμένη αναφορά με ένα κλικ.

Νιώστε ελεύθεροι να προσαρμόσετε τον αριθμό στηλών, την πηγή περιοχής ή τη διαδρομή εξόδου ώστε να ταιριάζει στις ανάγκες του έργου σας. Αν συναντήσετε δυσκολίες, αφήστε ένα σχόλιο παρακάτω—καλή προγραμματιστική!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}