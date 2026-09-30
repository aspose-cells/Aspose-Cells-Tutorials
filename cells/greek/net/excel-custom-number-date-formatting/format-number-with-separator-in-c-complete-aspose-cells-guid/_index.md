---
category: general
date: 2026-03-30
description: Μάθετε πώς να μορφοποιείτε αριθμούς με διαχωριστικό χρησιμοποιώντας το
  Aspose.Cells σε C#. Περιλαμβάνει ορισμό προσαρμοσμένης μορφής αριθμού, προσθήκη
  διαχωριστικού χιλιάδων, μορφοποίηση δεκαδικών θέσεων και πώς να μορφοποιήσετε το
  κελί.
draft: false
keywords:
- format number with separator
- set custom number format
- add thousands separator
- format decimal places
- how to format cell
language: el
og_description: Μορφοποίηση αριθμού με διαχωριστικό σε C#. Αυτός ο οδηγός δείχνει
  πώς να ορίσετε προσαρμοσμένη μορφή αριθμού, να προσθέσετε διαχωριστικό χιλιάδων,
  να μορφοποιήσετε δεκαδικά ψηφία και πώς να μορφοποιήσετε κελί χρησιμοποιώντας το
  Aspose.Cells.
og_title: Μορφοποίηση αριθμού με διαχωριστικό σε C# – Εκπαίδευση Aspose.Cells
tags:
- C#
- Aspose.Cells
- Number Formatting
title: Μορφοποίηση Αριθμού με Διαχωριστικό σε C# – Πλήρης Οδηγός Aspose.Cells
url: /el/net/excel-custom-number-date-formatting/format-number-with-separator-in-c-complete-aspose-cells-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Μορφοποίηση Αριθμού με Διαχωριστικό σε C# – Πλήρης Οδηγός Aspose.Cells

Έχετε ποτέ χρειαστεί να **μορφοποιήσετε αριθμό με διαχωριστικό** σε ένα φύλλο εργασίας αλλά δεν ήσασταν σίγουροι ποια κλήση API να χρησιμοποιήσετε; Δεν είστε μόνοι—οι προγραμματιστές αντιμετωπίζουν συνεχώς διαχωριστικά χιλιάδων, δεκαδικά ψηφία και προσαρμοσμένα μοτίβα κατά την εξαγωγή δεδομένων.  

Καλή νέα: το Aspose.Cells το κάνει παιχνιδάκι. Σε αυτό το tutorial θα περάσουμε από ένα πραγματικό παράδειγμα που **ορίζει προσαρμοσμένη μορφή αριθμού**, **προσθέτει διαχωριστικό χιλιάδων**, **μορφοποιεί δεκαδικά ψηφία**, και δείχνει **πώς να μορφοποιήσετε το κελί** ώστε η έξοδος να είναι συμβολοσειρά. Στο τέλος θα έχετε ένα έτοιμο κομμάτι κώδικα που μπορείτε να ενσωματώσετε σε οποιοδήποτε .NET project.

## Τι Καλύπτει Αυτός ο Οδηγός

* Το ακριβές πακέτο NuGet που χρειάζεστε και πώς να το εγκαταστήσετε.  
* Κώδικας βήμα‑βήμα που δημιουργεί ένα workbook, γράφει μια αριθμητική τιμή και εφαρμόζει προσαρμοσμένη μορφή.  
* Γιατί το `ExportTableOptions.ExportAsString` είναι η προτιμώμενη μέθοδος για την ανάκτηση μορφοποιημένης τιμής.  
* Συνηθισμένα λάθη—όπως η παράλειψη ενεργοποίησης του `ExportAsString` ή η χρήση λανθασμένης μάσκας μορφής.  
* Πώς να προσαρμόσετε τη μάσκα μορφής αν χρειάζεστε διαφορετικό αριθμό δεκαδικών ή διαφορετικό στυλ διαχωριστικού.

Δεν απαιτούνται εξωτερικοί σύνδεσμοι τεκμηρίωσης· όλα όσα χρειάζεστε είναι εδώ. Ας βουτήξουμε.

---

## Προαπαιτήσεις

| Απαίτηση | Λόγος |
|-------------|--------|
| .NET 6.0 ή νεότερο | Το Aspose.Cells 23.10+ στοχεύει στο .NET Standard 2.0+, οπότε το .NET 6 είναι ασφαλές και σύγχρονο. |
| Visual Studio 2022 (ή οποιοδήποτε IDE C#) | Καθιστά τον εντοπισμό σφαλμάτων και τη διαχείριση πακέτων απλό. |
| Aspose.Cells for .NET NuGet package | Παρέχει τις κλάσεις `Workbook`, `Worksheet` και `ExportTableOptions` που θα χρησιμοποιήσουμε. |

Μπορείτε να εγκαταστήσετε το πακέτο μέσω του Package Manager Console:

```powershell
Install-Package Aspose.Cells
```

Αυτό είναι όλο—χωρίς επιπλέον DLLs, χωρίς COM interop, μόνο μια αναφορά NuGet.

---

## Βήμα 1: Αρχικοποίηση Νέου Workbook (Πώς να Μορφοποιήσετε Κελί)

Το πρώτο που κάνουμε είναι να δημιουργήσουμε μια νέα παρουσία `Workbook`. Σκεφτείτε το ως ένα κενό αρχείο Excel έτοιμο να λάβει δεδομένα.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook – this is where we’ll format the cell.
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];
```

> **Why this matters:** `Workbook` είναι το σημείο εισόδου για κάθε λειτουργία στο Aspose.Cells. Παίρνοντας το πρώτο φύλλο εργασίας (`Worksheets[0]`) έχουμε έναν καθαρό καμβά χωρίς να χρειάζεται να ονομάσουμε το φύλλο.

---

## Βήμα 2: Εγγραφή Αριθμητικής Τιμής στο Στόχο Κελί

Στη συνέχεια, τοποθετούμε έναν ακατέργαστο αριθμό στο κελί **A1**. Η τιμή αυτή δεν είναι ακόμη μορφοποιημένη· είναι απλώς ένα double.

```csharp
        // Step 2: Insert a raw numeric value.
        worksheet.Cells["A1"].PutValue(12345.6789);
```

> **Pro tip:** Χρησιμοποιήστε `PutValue` αντί για `PutString` όταν σκοπεύετε να εφαρμόσετε αριθμητική μορφοποίηση αργότερα. Αυτό διατηρεί τον υποκείμενο τύπο δεδομένων, επιτρέποντας υπολογισμούς συμβατούς με το Excel.

---

## Βήμα 3: Ορισμός Προσαρμοσμένης Μάσκας Αριθμού (Προσθήκη Διαχωριστικού Χιλιάδων & Μορφοποίηση Δεκαδικών)

Τώρα έρχεται η καρδιά του tutorial: ορίζουμε μια μάσκα μορφής που λέει στο Aspose.Cells πώς να εμφανίσει τον αριθμό. Η μάσκα `#,##0.00` κάνει τρία πράγματα:

1. **`#,##0`** – προσθέτει διαχωριστικό χιλιάδων (κόμμα από προεπιλογή).  
2. **`.00`** – εξαναγκάζει ακριβώς δύο δεκαδικά ψηφία.  

Αν χρειάζεστε διαφορετικό αριθμό δεκαδικών, απλώς αλλάξτε τον αριθμό των `0` μετά το δεκαδικό σημείο.

```csharp
        // Step 3: Configure the custom number format.
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,          // Return the value as a formatted string.
            NumberFormat = "#,##0.00"       // Add thousands separator and fix to 2 decimals.
        };
```

> **Why we use `ExportAsString`**: By default, `ExportString` returns the raw value. Setting `ExportAsString = true` forces the API to apply the `NumberFormat` mask before converting to text. This is essential when you need the exact string representation for reports, JSON payloads, or UI display.

---

## Βήμα 4: Εξαγωγή Μορφοποιημένου Κειμένου (Πώς να Μορφοποιήσετε Κελί)

Με τις επιλογές έτοιμες, καλούμε `ExportString` στο ίδιο κελί. Η μέθοδος σέβεται τη μάσκα που ορίσαμε και επιστρέφει μια ωραία μορφοποιημένη συμβολοσειρά.

```csharp
        // Step 4: Export the formatted value.
        string formattedCellText = worksheet.Cells["A1"].ExportString(exportOptions);

        // Step 5: Show the result.
        Console.WriteLine(formattedCellText); // Expected output: 12,345.68
    }
}
```

Η εκτέλεση του προγράμματος εμφανίζει **`12,345.68`** στην κονσόλα—ακριβώς τη μορφή που ζητήσαμε.

> **Edge case:** If the source number has more than two decimal places, the mask rounds it. If you need truncation instead of rounding, you’ll have to pre‑process the value with `Math.Truncate` before calling `PutValue`.

---

## Βήμα 5: Ρύθμιση Μορφής – Συνηθισμένες Παραλλαγές

### 5.1 Αλλαγή Ακρίβειας Δεκαδικών

Θέλετε τρία δεκαδικά ψηφία; Απλώς αντικαταστήστε τη μάσκα:

```csharp
NumberFormat = "#,##0.000"   // → 12,345.679
```

### 5.2 Χρήση Διαφορετικού Διαχωριστικού Χιλιάδων

Ορισμένες περιοχές προτιμούν κενό ή τελεία. Μπορείτε να ενσωματώσετε το χαρακτήρα απευθείας:

```csharp
NumberFormat = "# ##0.00"    // Uses a non‑breaking space as separator.
```

Ή να βασιστείτε στις ρυθμίσεις πολιτισμού του workbook:

```csharp
workbook.Settings.CultureInfo = new System.Globalization.CultureInfo("de-DE");
NumberFormat = "#.##0,00";   // German style: 12.345,68
```

### 5.3 Πρόθεμα ή Επίθημα (Νόμισμα, Ποσοστό)

Προσθέστε το σύμβολο δολαρίου ή το σύμβολο ποσοστού απευθείας στη μάσκα:

```csharp
NumberFormat = "$#,##0.00";   // → $12,345.68
NumberFormat = "0.00%";       // → 1,234,568.00%
```

> **Note:** The mask is case‑sensitive. `$` and `%` are literal symbols; they don’t affect the underlying numeric value.

---

## Βήμα 6: Πλήρες Παράδειγμα Εργασίας (Έτοιμο για Αντιγραφή‑Επικόλληση)

Παρακάτω είναι το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε σε μια νέα εφαρμογή console. Περιλαμβάνει όλα τα βήματα, σχόλια και την τελική επαλήθευση εξόδου.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialise workbook and worksheet.
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Write raw numeric value to A1.
        worksheet.Cells["A1"].PutValue(12345.6789);

        // 3️⃣ Define custom format: thousands separator + two decimals.
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            NumberFormat = "#,##0.00"
        };

        // 4️⃣ Export the formatted string.
        string result = worksheet.Cells["A1"].ExportString(exportOptions);

        // 5️⃣ Display the outcome.
        Console.WriteLine(result); // Output: 12,345.68

        // Optional: keep console open.
        Console.WriteLine("Press any key to exit...");
        Console.ReadKey();
    }
}
```

Τρέξτε το πρόγραμμα (`dotnet run` από το τερματικό ή πατήστε F5 στο Visual Studio) και θα δείτε τον μορφοποιημένο αριθμό να εκτυπώνεται ακριβώς όπως φαίνεται.

---

## Συχνές Ερωτήσεις (FAQ)

**Q: Λειτουργεί αυτό με παλαιότερες εκδόσεις του Excel;**  
A: Ναι. Η μάσκα μορφής ακολουθεί τη φυσική σύνταξη μορφής αριθμού του Excel, οπότε οποιαδήποτε έκδοση που καταλαβαίνει `#,##0.00` θα αποδώσει την ίδια συμβολοσειρά.

**Q: Τι γίνεται αν χρειαστεί να μορφοποιήσω μια περιοχή κελιών;**  
A: Κάντε βρόχο πάνω στην επιθυμητή περιοχή και εφαρμόστε το ίδιο `ExportTableOptions` σε κάθε κελί, ή ορίστε την ιδιότητα `Style.Custom` στην περιοχή και μετά καλέστε `ExportString` σε ένα μόνο κελί.

**Q: Μπορώ να εξάγω απευθείας σε CSV με αυτές τις μορφές εφαρμοσμένες;**  
A: Απόλυτα. Χρησιμοποιήστε `Workbook.Save("output.csv", SaveFormat.CSV);` μετά τον ορισμό της μορφής σε κάθε κελί. Το Aspose.Cells σέβεται το `Style` του κελιού κατά τη δημιουργία CSV.

---

## Συμπέρασμα

Μόλις δείξαμε πώς να **μορφοποιήσετε αριθμό με διαχωριστικό** σε C# χρησιμοποιώντας το Aspose.Cells, καλύπτοντας τα πάντα από **ορισμό προσαρμοσμένης μορφής αριθμού** μέχρι **προσθήκη διαχωριστικού χιλιάδων**, **μορφοποίηση δεκαδικών**, και το ουσιώδες **πώς να μορφοποιήσετε το κελί** για εξαγωγή ως συμβολοσειρά. Ο κώδικας είναι πλήρως αυτόνομος, λειτουργεί με .NET 6+ και μπορεί να προσαρμοστεί σε οποιοδήποτε πολιτισμό ή απαίτηση ακρίβειας.

Επόμενα βήματα, μπορείτε να εξερευνήσετε:

* Εφαρμογή της ίδιας τεχνικής σε ημερομηνίες και ώρες (`NumberFormat = "dd‑MMM‑yyyy"`).  
* Αυτοματοποίηση μαζικών εξαγωγών όπου κάθε στήλη χρειάζεται διαφορετική μάσκα.  
* Ενσωμάτωση των μορφοποιημένων συμβολοσειρών σε PDF αναφορές με Aspose.Words.

Δοκιμάστε τα και θα γίνετε γρήγορα το άτομο-αναφορά για μορφοποίηση υπολογιστικών φύλλων στην ομάδα σας. Καλή προγραμματιστική!

(Image: ![Screenshot showing formatted number with separator in Aspose.Cells](image-placeholder.png){alt="Formatted number with separator displayed in Aspose.Cells output"} )

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}