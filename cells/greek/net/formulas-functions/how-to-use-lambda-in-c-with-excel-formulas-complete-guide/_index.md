---
category: general
date: 2026-03-22
description: Πώς να χρησιμοποιήσετε λήμμα (lambda) στο C# για εργασία με τύπους του
  Excel. Μάθετε να γράφετε τύπο σε κελί, να μετατρέπετε περιοχή σε πίνακα, να εμφανίζετε
  τον πίνακα στην κονσόλα και να υπολογίζετε τη συνεφαπτομένη στο Excel.
draft: false
keywords:
- how to use lambda
- display array in console
- convert range to array
- write formula to cell
- calculate cotangent in excel
language: el
og_description: Πώς να χρησιμοποιήσετε το lambda σε C# για να χειριστείτε τύπους Excel,
  να μετατρέψετε περιοχή σε πίνακα, να γράψετε τύπο σε κελί, να εμφανίσετε τον πίνακα
  στην κονσόλα και να υπολογίσετε τη συνεφαπτομένη στο Excel.
og_title: Πώς να χρησιμοποιήσετε το Lambda σε C# με τύπους Excel – Βήμα προς βήμα
tags:
- C#
- Aspose.Cells
- Excel Automation
- Lambda Expressions
title: Πώς να χρησιμοποιήσετε το Lambda στη C# με τύπους Excel – Πλήρης οδηγός
url: /el/net/formulas-functions/how-to-use-lambda-in-c-with-excel-formulas-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Χρησιμοποιήσετε Lambda σε C# με Τύπους Excel – Πλήρης Οδηγός

Έχετε αναρωτηθεί ποτέ **πώς να χρησιμοποιήσετε lambda** όταν αυτοματοποιείτε το Excel από C#; Δεν είστε μόνοι. Πολλοί προγραμματιστές συναντούν δυσκολίες όταν πρέπει να συνδυάσουν τη δύναμη των νέων δυναμικών συναρτήσεων πίνακα του Excel με τη δυνατότητα `LAMBDA` του C#. Τα καλά νέα; Είναι στην πραγματικότητα αρκετά απλό μόλις δείτε πώς ταιριάζουν τα κομμάτια.

Σε αυτό το tutorial θα περάσουμε από **γραφή τύπου σε κελί**, **μετατροπή περιοχής σε πίνακα**, **εμφάνιση του πίνακα στην κονσόλα**, και ακόμη **υπολογισμό της συνεφαπτομένης στο Excel**—όλα ενώ σας δείχνουμε **πώς να χρησιμοποιήσετε lambda** μέσα σε κλήση `REDUCE`. Στο τέλος θα έχετε ένα εκτελέσιμο απόσπασμα που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο .NET που αναφέρεται στο Aspose.Cells (ή σε παρόμοια βιβλιοθήκη).

---

## Τι Θα Μάθετε

- Πώς να **γράψετε τύπο σε κελί** χρησιμοποιώντας C#.
- Πώς να **μετατρέψετε περιοχή σε πίνακα** με τη συνάρτηση `EXPAND`.
- Πώς να **εμφανίσετε τον πίνακα στην κονσόλα** μετά τον υπολογισμό.
- Πώς να **υπολογίσετε τη συνεφαπτομένη στο Excel** χρησιμοποιώντας `COT` και `COTH`.
- Η ακριβής σύνταξη για **πώς να χρησιμοποιήσετε lambda** μέσα στη συνάρτηση `REDUCE` του Excel από C#.

> **Προαπαιτούμενο:** Χρειάζεστε μια πρόσφατη έκδοση του .NET (Core 6+ ή .NET Framework 4.7+) και τη βιβλιοθήκη Aspose.Cells for .NET εγκατεστημένη μέσω NuGet.

---

## Βήμα 1: Δημιουργία του Workbook και Γραφή Τύπου σε Κελί

Το πρώτο που κάνουμε είναι να δημιουργήσουμε ένα νέο workbook και να πάρουμε το πρώτο φύλλο εργασίας. Στη συνέχεια **γράφουμε έναν τύπο σε κελί** – σε αυτήν την περίπτωση το `A1` θα κρατήσει το αποτέλεσμα μιας κλήσης `EXPAND`.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Write formula to A1 – we’ll expand B1:C2 into a 4‑by‑5 array later
        worksheet.Cells["A1"].Formula = "=EXPAND(B1:C2, 4, 5)";
```

**Γιατί είναι σημαντικό:** Η γραφή του τύπου απευθείας από τον κώδικα σημαίνει ότι μπορείτε να δημιουργήσετε σύνθετα υπολογιστικά φύλλα εν κινήσει χωρίς να ανοίξετε ποτέ το Excel. Επίσης προετοιμάζει το επόμενο βήμα, όπου **μετατρέπουμε την περιοχή σε πίνακα**.

---

## Βήμα 2: Μετατροπή Περιοχής σε Πίνακα με EXPAND

Η `EXPAND` είναι ο τρόπος του Excel να μετατρέπει μια μικρή περιοχή σε μεγαλύτερο πίνακα. Τοποθετώντας τον τύπο στο `A1`, το Excel θα «χύσει» ένα μπλοκ 4 × 5 ξεκινώντας από αυτό το κελί. Από το C# δεν χρειάζεται να αντιγράψουμε τις τιμές χειροκίνητα – η βιβλιοθήκη θα κάνει τη βαριά δουλειά όταν καλέσουμε `Calculate`.

```csharp
        // The EXPAND formula will spill into A1:E4 (4 rows × 5 columns)
        // No extra code needed – the workbook will handle the spill.
```

**Πώς να χρησιμοποιήσετε lambda:** Δεν έχουμε φτάσει ακόμη, αλλά μείνετε συντονισμένοι. Πρώτα χρειάζεται τα δεδομένα στο φύλλο, μετά θα τα μειώσουμε με μια lambda.

---

## Βήμα 3: Χρήση LAMBDA Μέσα στο REDUCE – Ο Πυρήνας του “Πώς να Χρησιμοποιήσετε Lambda”

Το Excel 365 εισήγαγε τη `REDUCE`, η οποία δέχεται μια **αρχική τιμή**, μια **περιοχή**, και ένα **LAMBDA** που καθορίζει πώς θα συνδυάσει κάθε στοιχείο. Από το C# απλώς ορίζουμε το string του τύπου· η lambda ζει μέσα στον τύπο του Excel, όχι στον κώδικα C#.

```csharp
        // Reduce the spilled array by summing all its values.
        // This demonstrates how to use lambda inside REDUCE.
        worksheet.Cells["E1"].Formula = "=REDUCE(0, A1:D4, LAMBDA(acc, x, acc + x))";
```

**Εξήγηση:**  
- `0` είναι ο αρχικός συσσωρευτής (`acc`).  
- `A1:D4` είναι η περιοχή που θέλουμε να επεξεργαστούμε (οι πρώτες τέσσερις στήλες του «spill»).  
- `LAMBDA(acc, x, acc + x)` λέει στο Excel να προσθέσει κάθε κελί (`x`) στον συσσωρευτή.  

Αυτή είναι η ουσία του **πώς να χρησιμοποιήσετε lambda** για συγκέντρωση σε ένα υπολογιστικό φύλλο.

---

## Βήμα 4: Υπολογισμός Συνεφαπτομένης στο Excel – Από Μοίρες σε Υπερβολικές

Αν χρειάζεστε τριγωνομετρικά αποτελέσματα, οι συναρτήσεις `COT` και `COTH` του Excel είναι πολύ εύχρηστες. Θα τις τοποθετήσουμε στα `G1` και `G2` αντίστοιχα.

```csharp
        // Demonstrate trigonometric functions – cotangent and hyperbolic cotangent
        worksheet.Cells["G1"].Formula = "=COT(PI()/4)";   // Expected result: 1
        worksheet.Cells["G2"].Formula = "=COTH(1)";      // Hyperbolic cotangent of 1
```

**Γιατί είναι χρήσιμο:** Η γνώση του **υπολογισμού της συνεφαπτομένης στο Excel** μπορεί να σας εξοικονομήσει χρόνο από το να γράψετε προσαρμοσμένο μαθηματικό κώδικα, ειδικά όταν το βιβλίο εργασίας θα μοιραστεί με μη‑προγραμματιστές.

---

## Βήμα 5: Εξαναγκασμός Υπολογισμού και Ανάκτηση του Επεκταμένου Πίνακα

Τώρα λέμε στο workbook να αξιολογήσει κάθε τύπο, μετά εξάγουμε τον «spill» πίνακα από το `A1`. Εδώ είναι που **εμφανίζουμε τον πίνακα στην κονσόλα**.

```csharp
        // Force calculation of all formulas
        workbook.Calculate();

        // Retrieve the spilled array from A1 as a 2‑D object
        var expanded = worksheet.Cells["A1"].Value;

        // Pretty‑print the 2‑D array to the console
        Console.WriteLine("Expanded array from A1 (4×5):");
        if (expanded is object[,] matrix)
        {
            for (int r = 0; r < matrix.GetLength(0); r++)
            {
                for (int c = 0; c < matrix.GetLength(1); c++)
                {
                    Console.Write($"{matrix[r, c]}\t");
                }
                Console.WriteLine();
            }
        }
        else
        {
            Console.WriteLine("Unexpected data type.");
        }

        // Show the result of the REDUCE lambda
        Console.WriteLine($"\nSum of A1:D4 (via REDUCE lambda): {worksheet.Cells["E1"].Value}");

        // Show cotangent results
        Console.WriteLine($"Cotangent of π/4: {worksheet.Cells["G1"].Value}");
        Console.WriteLine($"Hyperbolic cotangent of 1: {worksheet.Cells["G2"].Value}");
    }
}
```

**Τι θα δείτε:**  
- Ένα ωραία μορφοποιημένο πίνακα 4 × 5 εκτυπωμένο γραμμή‑γραμμή.  
- Το άθροισμα που υπολογίστηκε από τη lambda του `REDUCE`.  
- Τις δύο τιμές της συνεφαπτομένης.

Αυτό ολοκληρώνει τη ροή από **γραφή τύπου σε κελί** μέχρι **εμφάνιση του πίνακα στην κονσόλα**.

---

## Πλήρες Παράδειγμα (Έτοιμο για Αντιγραφή‑Επικόλληση)

Παρακάτω είναι ολόκληρο το πρόγραμμα που μπορείτε να ενσωματώσετε σε μια εφαρμογή console. Θυμηθείτε να προσθέσετε πρώτα το πακέτο NuGet `Aspose.Cells` (`dotnet add package Aspose.Cells`).

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Initialize workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Step 2: Write EXPAND formula (convert range to array)
        worksheet.Cells["A1"].Formula = "=EXPAND(B1:C2, 4, 5)";

        // Step 3: Use REDUCE with LAMBDA (how to use lambda)
        worksheet.Cells["E1"].Formula = "=REDUCE(0, A1:D4, LAMBDA(acc, x, acc + x))";

        // Step 4: Calculate cotangent values (calculate cotangent in excel)
        worksheet.Cells["G1"].Formula = "=COT(PI()/4)";   // Expected: 1
        worksheet.Cells["G2"].Formula = "=COTH(1)";

        // Step 5: Force calculation
        workbook.Calculate();

        // Step 6: Retrieve and display the expanded array (display array in console)
        var expanded = worksheet.Cells["A1"].Value;
        Console.WriteLine("Expanded array from A1 (4×5):");
        if (expanded is object[,] matrix)
        {
            for (int r = 0; r < matrix.GetLength(0); r++)
            {
                for (int c = 0; c < matrix.GetLength(1); c++)
                {
                    Console.Write($"{matrix[r, c]}\t");
                }
                Console.WriteLine();
            }
        }
        else
        {
            Console.WriteLine("Unexpected data type.");
        }

        // Show REDUCE result
        Console.WriteLine($"\nSum of A1:D4 (via REDUCE lambda): {worksheet.Cells["E1"].Value}");

        // Show cotangent results
        Console.WriteLine($"Cotangent of π/4: {worksheet.Cells["G1"].Value}");
        Console.WriteLine($"Hyperbolic cotangent of 1: {worksheet.Cells["G2"].Value}");
    }
}
```

**Αναμενόμενη έξοδος στην κονσόλα (τιμές ενδέχεται να διαφέρουν ανάλογα με το προεπιλεγμένο περιεχόμενο των B1:C2, που είναι 0 εξ ορισμού):**

```
Expanded array from A1 (4×5):
0   0   0   0   0
0   0   0   0   0
0   0   0   0   0
0   0   0   0   0

Sum of A1:D4 (via REDUCE lambda): 0
Cotangent of π/4: 1
Hyperbolic cotangent of 1: 1.31303528549933
```

Μη διστάσετε να γεμίσετε τα `B1:C2` με τους δικούς σας αριθμούς πριν τρέξετε – ο πίνακας θα αντικατοπτρίζει αυτές τις τιμές.

---

## Pro Συμβουλές & Συνηθισμένα Πιθανά Σφάλματα

- **Pro tip:** Αν θέλετε η «spill» περιοχή να ξεκινά αλλού, απλώς αλλάξτε το κελί-στόχο (`A1`). Η συνάρτηση `EXPAND` σέβεται το άγκυρο.
- **Προσοχή σε:** Κενά κελιά στην πηγή γίνονται `0` στον «spill» πίνακα, κάτι που μπορεί να επηρεάσει το άθροισμα του `REDUCE`.
- **Edge case:** Όταν το workbook περιέχει τύπους που εξαρτώνται από εθελοντικές συναρτήσεις (π.χ., `NOW()`), καλέστε `workbook.Calculate()` μετά τον ορισμό όλων των τύπων για να διασφαλίσετε ότι όλα είναι ενημερωμένα.
- **Performance note:** Για τεράστιες «spills», σκεφτείτε να περιορίσετε το μέγεθος στην κλήση `EXPAND`; διαφορετικά μπορεί να δεσμευτεί περισσότερη μνήμη από ό,τι χρειάζεται.
- **Compatibility:** The `

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}