---
category: general
date: 2026-02-14
description: Δημιουργήστε γρήγορα πρότυπο έκπτωσης και μάθετε πώς να εφαρμόζετε έκπτωση
  σε υπολογιστικό φύλλο, να ενσωματώνετε δεδομένα στο πρότυπο και να ορίζετε μεταβλητό
  πρόθεμα για έξυπνους δείκτες.
draft: false
keywords:
- create discount template
- apply discount in spreadsheet
- inject data into template
- define variable prefix
language: el
og_description: Δημιουργήστε πρότυπο έκπτωσης με C#. Μάθετε πώς να εφαρμόζετε έκπτωση
  σε υπολογιστικό φύλλο, να ενσωματώνετε δεδομένα στο πρότυπο και να ορίζετε μεταβλητό
  πρόθεμα για έξυπνους δείκτες.
og_title: Δημιουργία Προτύπου Έκπτωσης – Πλήρης Οδηγός C#
tags:
- C#
- SmartMarker
- Spreadsheet Automation
title: Δημιουργία προτύπου έκπτωσης σε C# – Οδηγός βήμα‑προς‑βήμα
url: /el/net/smart-markers-dynamic-data/create-discount-template-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία Προτύπου Έκπτωσης – Πλήρης Οδηγός C#

Έχετε ποτέ χρειαστεί να **create discount template** για μια αναφορά πωλήσεων αλλά δεν ήξερες πώς να τροφοδοτήσεις αυτόματα τους αριθμούς σε ένα υπολογιστικό φύλλο; Δεν είστε μόνοι. Σε αυτό το εκπαιδευτικό υλικό θα σας δείξουμε ακριβώς πώς να **create discount template**, στη συνέχεια **apply discount in spreadsheet** στα κελιά, **inject data into template**, και ακόμη **define variable prefix** για τα smart markers σας—όλα με καθαρό κώδικα C#.

Θα ξεκινήσουμε περιγράφοντας το πρόβλημα, μετά θα περάσουμε κατευθείαν σε μια λειτουργική λύση που μπορείτε να αντιγράψετε‑επικολλήσετε. Στο τέλος θα έχετε ένα επαναχρησιμοποιήσιμο μοτίβο που λειτουργεί είτε δημιουργείτε τιμολόγια, λίστες τιμών ή οποιοδήποτε υπολογιστικό φύλλο που χρειάζεται δυναμικές εκπτώσεις.

---

## Τι Θα Μάθετε

- Πώς να σχεδιάσετε ένα πρότυπο υπολογιστικού φύλλου που να υποστηρίζει εκπτώσεις.
- Πώς να διαμορφώσετε ένα προσαρμοσμένο `VariablePrefix` / `VariableSuffix` ώστε οι δείκτες να είναι εύκολο να εντοπίζονται.
- Πώς να περάσετε ένα ανώνυμο αντικείμενο (`discountData`) στον `SmartMarkerProcessor`.
- Πώς ο παραγόμενος τύπος (`=IF(#Discount#>0, A1*(1-#Discount#), A1)`) υπολογίζει αυτόματα την τελική τιμή.
- Συμβουλές για τη διαχείριση ειδικών περιπτώσεων όπως γραμμές με μηδενική έκπτωση ή πολλαπλά επίπεδα έκπτωσης.

**Prerequisites** – ένα πρόσφατο .NET runtime (≥ .NET 6), μια αναφορά στη βιβλιοθήκη `Aspose.Cells` (ή παρόμοια) που παρέχει `SmartMarkerProcessor`, και μια βασική κατανόηση της σύνταξης C#. Τίποτα εξειδικευμένο.

---

## Βήμα 1: Δημιουργήστε ένα Πρότυπο Έκπτωσης στο Υπολογιστικό Φύλλο Σας

Αρχικά, ανοίξτε ένα νέο βιβλίο εργασίας (ή χρησιμοποιήστε ένα υπάρχον) και τοποθετήστε έναν χώρο κράτησης όπου θα εφαρμοστεί η έκπτωση. Σκεφτείτε το πρότυπο ως ένα απλό αρχείο Excel με “smart markers” που ο επεξεργαστής θα αντικαταστήσει.

```csharp
using Aspose.Cells;          // SmartMarkerProcessor lives here
using System;

// Step 1: Load or create a workbook
Workbook wb = new Workbook();               // creates an empty .xlsx in memory
Worksheet ws = wb.Worksheets[0];
ws.Name = "Pricing";

// Put a header
ws.Cells["A1"].PutValue("Original Price");
ws.Cells["B1"].PutValue("Discounted Price");

// Sample data row – the formula will be injected later
ws.Cells["A2"].PutValue(100);               // original price = 100
ws.Cells["B2"].Formula = "=IF(#Discount#>0, A2*(1-#Discount#), A2)";
```

**Γιατί είναι σημαντικό:** Ενσωματώνοντας το `#Discount#` μέσα στον τύπο, λέμε στον επεξεργαστή ακριβώς πού ανήκει η τιμή της έκπτωσης. Ο `SmartMarkerProcessor` θα αντικαταστήσει το `#Discount#` με τον αριθμό που θα δώσετε αργότερα, αφήνοντας το υπόλοιπο του τύπου αμετάβλητο.

---

## Βήμα 2: Ορίστε Πρόθεμα Μεταβλητής για τα Smart Markers

Από προεπιλογή, πολλές βιβλιοθήκες ψάχνουν για `${Variable}` ή `{{Variable}}`. Στην περίπτωσή μας θέλουμε έναν καθαρό, ανθρώπινα αναγνώσιμο δείκτη, οπότε **ορίζουμε πρόθεμα μεταβλητής** και επίθημα ρητά.

```csharp
// Step 2: Configure how markers are identified
var smartMarkerOptions = new SmartMarkerOptions
{
    VariablePrefix = "#",   // start marker
    VariableSuffix = "#"    // end marker
};
```

**Pro tip:** Η χρήση του `#` κρατά τους δείκτες σύντομους και εύκολους στην αναγνώριση στη γραμμή τύπων του Excel. Αν χρειαστεί ποτέ να αποφύγετε συγκρούσεις με υπάρχουσες συναρτήσεις του Excel, επιλέξτε ένα διαφορετικό ζεύγος (π.χ. `[[` και `]]`).

---

## Βήμα 3: Εισάγετε Δεδομένα στο Πρότυπο Χρησιμοποιώντας SmartMarkerProcessor

Τώρα τροφοδοτούμε την πραγματική τιμή της έκπτωσης. Ο επεξεργαστής θα σαρώσει το φύλλο, θα βρει κάθε `#Discount#` και θα το αντικαταστήσει με την τιμή από το ανώνυμο αντικείμενο που περνάμε.

```csharp
// Step 3: Prepare the data that will be injected
var discountData = new { Discount = 0.10, Total = 100 };

// Run the processor – it mutates the workbook in‑place
ws.SmartMarkerProcessor.StartSmartMarkerProcessing(discountData, smartMarkerOptions);
```

Μετά από αυτήν την κλήση, ο τύπος στο `B2` γίνεται:

```
=IF(0.1>0, A2*(1-0.1), A2)
```

Όταν το βιβλίο εργασίας υπολογίσει, το `B2` εμφανίζει **90**, δηλαδή μια έκπτωση 10 % στην αρχική τιμή των 100.

**Γιατί λειτουργεί:** Η `StartSmartMarkerProcessing` περνάει από κάθε κελί, ψάχνει το διακριτικό `#Discount#` και αντικαθιστά την αριθμητική τιμή. Επειδή το διακριτικό βρίσκεται μέσα σε μια δήλωση `IF`, το υπολογιστικό φύλλο εξακολουθεί να διαχειρίζεται περιπτώσεις όπου η έκπτωση μπορεί να είναι μηδέν.

---

## Βήμα 4: Εφαρμόστε την Έκπτωση στο Υπολογιστικό Φύλλο – Επαληθεύστε το Αποτέλεσμα

Ας ενεργοποιήσουμε τον υπολογισμό και να εμφανίσουμε την τελική τιμή στην κονσόλα. Αυτό το βήμα αποδεικνύει ότι η ροή **apply discount in spreadsheet** ολοκληρώθηκε με επιτυχία.

```csharp
// Step 4: Force calculation and read the result
wb.CalculateFormula();                     // ensures all formulas are up‑to‑date
double discountedPrice = ws.Cells["B2"].DoubleValue;

Console.WriteLine($"Original: {ws.Cells["A2"].DoubleValue}");
Console.WriteLine($"Discounted (10%): {discountedPrice}");
```

**Αναμενόμενη έξοδος**

```
Original: 100
Discounted (10%): 90
```

Αν αλλάξετε το `discountData.Discount` σε `0.25` και ξανατρέξετε τον επεξεργαστή, η έξοδος θα αντικατοπτρίζει αυτόματα μια έκπτωση 25 %—χωρίς επιπλέον κώδικα.

---

## Βήμα 5: Διαχείριση Ειδικών Περιπτώσεων & Πολλαπλών Εκπτώσεων

### Γραμμές Μηδενικής Έκπτωσης

Μερικές φορές ένα προϊόν δεν είναι σε προσφορά. Για να κρατήσουμε τον τύπο ανθεκτικό, το `IF` που τοποθετήσατε νωρίτερα καλύπτει ήδη αυτό το σενάριο: όταν το `#Discount#` είναι `0`, η αρχική τιμή περνάει αμετάβλητη.

```csharp
var noDiscountData = new { Discount = 0.0 };
ws.SmartMarkerProcessor.StartSmartMarkerProcessing(noDiscountData, smartMarkerOptions);
wb.CalculateFormula();
Console.WriteLine($"No discount applied: {ws.Cells["B2"].DoubleValue}");
```

### Πολλαπλές Στήλες Έκπτωσης

Αν χρειάζεστε ξεχωριστές εκπτώσεις ανά γραμμή, δώστε σε κάθε γραμμή το δικό της δείκτη, π.χ. `#Discount1#`, `#Discount2#`, και περάστε μια συλλογή:

```csharp
var multiDiscountData = new[]
{
    new { Discount = 0.05 },   // row 2
    new { Discount = 0.15 }    // row 3
};

ws.SmartMarkerProcessor.StartSmartMarkerProcessing(multiDiscountData, smartMarkerOptions);
```

Ο επεξεργαστής ταιριάζει τους δείκτες διαδοχικά, έτσι ώστε κάθε γραμμή να λαμβάνει τη σωστή τιμή.

---

## Πλήρες Παράδειγμα Λειτουργίας

Παρακάτω είναι το πλήρες, έτοιμο για αντιγραφή πρόγραμμα που ενσωματώνει όλα τα παραπάνω βήματα. Αποθηκεύστε το ως `Program.cs`, προσθέστε μια αναφορά στο `Aspose.Cells`, και τρέξτε το.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook & template
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];
        ws.Name = "Pricing";
        ws.Cells["A1"].PutValue("Original Price");
        ws.Cells["B1"].PutValue("Discounted Price");
        ws.Cells["A2"].PutValue(100);
        ws.Cells["B2"].Formula = "=IF(#Discount#>0, A2*(1-#Discount#), A2)";

        // 2️⃣ Define marker delimiters
        var smartMarkerOptions = new SmartMarkerOptions
        {
            VariablePrefix = "#",
            VariableSuffix = "#"
        };

        // 3️⃣ Inject a 10 % discount
        var discountData = new { Discount = 0.10 };
        ws.SmartMarkerProcessor.StartSmartMarkerProcessing(discountData, smartMarkerOptions);

        // 4️⃣ Calculate and display result
        wb.CalculateFormula();
        double original = ws.Cells["A2"].DoubleValue;
        double discounted = ws.Cells["B2"].DoubleValue;

        Console.WriteLine($"Original: {original}");
        Console.WriteLine($"Discounted (10%): {discounted}");

        // Optional: Save the workbook to verify manually
        wb.Save("DiscountedPricing.xlsx");
    }
}
```

Η εκτέλεση εκτυπώνει τους αναμενόμενους αριθμούς και δημιουργεί ένα αρχείο `DiscountedPricing.xlsx` που μπορείτε να ανοίξετε στο Excel για να δείτε τον τύπο ήδη επιλυμένο.

---

## Συμπέρασμα

Τώρα ξέρετε πώς να **create discount template**, **apply discount in spreadsheet**, **inject data into template**, και **define variable prefix** για smart markers—όλα με μερικές σύντομες γραμμές κώδικα C#. Το μοτίβο κλιμακώνεται—απλώς αλλάξτε το ανώνυμο αντικείμενο ή τροφοδοτήστε μια συλλογή για μαζικές ενημερώσεις, και το ίδιο πρότυπο θα διαχειριστεί οποιοδήποτε σενάριο έκπτωσης.

Έτοιμοι για το επόμενο επίπεδο; Δοκιμάστε:

- Προσθήκη υπολογισμών φόρου παράλληλα με τις εκπτώσεις.
- Ανάκτηση ποσοστών έκπτωσης από μια βάση δεδομένων αντί για σκληρή κωδικοποίηση.
- Χρήση υπό συνθήκη μορφοποίησης για να επισημάνετε γραμμές με υψηλές εκπτώσεις.

Αυτές οι επεκτάσεις διατηρούν την κύρια ιδέα αμετάβλητη ενώ επεκτείνουν τη χρηστικότητα του προτύπου έκπτωσης.

Έχετε ερωτήσεις ή ένα ενδιαφέρον use‑case; Αφήστε ένα σχόλιο παρακάτω, και καλή προγραμματιστική!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}