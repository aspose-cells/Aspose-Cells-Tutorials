---
category: general
date: 2026-10-10
description: Δημιουργήστε βιβλίο εργασίας Excel σε C# και ορίστε την τιμή του κελιού
  με ημερομηνία ιαπωνικής εποχής, στη συνέχεια εφαρμόστε προσαρμοσμένη μορφή και διαβάστε
  το κελί ημερομηνίας χρησιμοποιώντας το Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- set cell value
- apply custom format
- read date cell
- excel date parsing
language: el
lastmod: 2026-10-10
og_description: Δημιουργήστε βιβλίο εργασίας Excel σε C# και αναλύστε ημερομηνίες
  ιαπωνικής εποχής. Μάθετε πώς να ορίζετε τιμή κελιού, να εφαρμόζετε προσαρμοσμένη
  μορφή και να διαβάζετε κελί ημερομηνίας με το Aspose.Cells.
og_image_alt: Screenshot showing a C# program that creates an Excel workbook and parses
  a Japanese era date
og_title: Δημιουργία βιβλίου εργασίας Excel σε C# – πλήρης οδηγός για την ανάλυση
  ημερομηνιών
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Create Excel workbook in C# and set cell value with a Japanese era
    date, then apply custom format and read date cell using Aspose.Cells.
  headline: How to create Excel workbook and parse Japanese dates in C#
  type: TechArticle
tags:
- C#
- Aspose.Cells
- Excel automation
title: Πώς να δημιουργήσετε ένα βιβλίο εργασίας Excel και να αναλύσετε ιαπωνικές ημερομηνίες
  σε C#
url: /el/net/excel-custom-number-date-formatting/how-to-create-excel-workbook-and-parse-japanese-dates-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να δημιουργήσετε βιβλίο εργασίας Excel και να αναλύσετε ιαπωνικές ημερομηνίες σε C#

Αν χρειάζεστε να **create Excel workbook** από το μηδέν, αυτός ο οδηγός σας δείχνει ακριβώς πώς. Θα μάθετε να **set cell value** με μια ημερομηνία ιαπωνικής εποχής, να **apply custom format** που κατανοεί την εποχή, και τελικά να **read date cell** για να αποκτήσετε ένα .NET `DateTime`. Το πλήρες παράδειγμα λειτουργεί με την τελευταία έκδοση του Aspose.Cells for .NET, ώστε να μπορείτε να αντιγράψετε‑επικολλήσετε τον κώδικα σε οποιοδήποτε έργο C#.

Η εργασία με ημερομηνίες που περιλαμβάνουν ιαπωνικές εποχές μπορεί να είναι δύσκολη επειδή ο προεπιλεγμένος parser του Excel δεν αναγνωρίζει τα σύμβολα της εποχής. Χρησιμοποιώντας μια προσαρμοσμένη μορφή αριθμού (`[ja-JP-Era]`) λέτε στο Excel πώς να ερμηνεύσει τη συμβολοσειρά, επιτρέποντας αξιόπιστη **excel date parsing**. Τα παρακάτω βήματα καλύπτουν ολόκληρη τη ροή εργασίας, από τη δημιουργία του βιβλίου εργασίας μέχρι την εξαγωγή της ημερομηνίας.

## Προαπαιτούμενα

- .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί επίσης σε .NET Framework 4.7+)
- Aspose.Cells for .NET (πακέτο NuGet `Aspose.Cells`)
- Βασική εξοικείωση με C# και Visual Studio ή οποιοδήποτε IDE της επιλογής σας

## Βήμα 1: Create Excel workbook και προσθήκη φύλλου εργασίας

Η πρώτη ενέργεια είναι να **create Excel workbook** στη μνήμη. Το Aspose.Cells δημιουργεί αυτόματα ένα προεπιλεγμένο φύλλο εργασίας, αλλά μπορείτε να προσθέσετε περισσότερα αν χρειάζεται.

```csharp
using Aspose.Cells;
using System;

class JapaneseDateExample
{
    static void Main()
    {
        // Step 1: Create a new workbook instance
        Workbook workbook = new Workbook();

        // Optional: rename the default worksheet for clarity
        workbook.Worksheets[0].Name = "Dates";
```

Η δημιουργία του βιβλίου εργασίας εκχωρεί τις εσωτερικές δομές που αργότερα θα περιέχουν κελιά, στυλ και τύπους. Δεν γράφεται κανένα αρχείο σε αυτό το στάδιο, κάτι που διατηρεί τη λειτουργία γρήγορη και δοκιμαστική.

## Βήμα 2: Set cell value με συμβολοσειρά ημερομηνίας ιαπωνικής εποχής

Στη συνέχεια, **set cell value** στην ιαπωνική αναπαράσταση εποχής `"R5-04-01"` (Reiwa 5, Απρίλιος 1). Η συμβολοσειρά ακολουθεί το μοτίβο `EraYear-MM-DD`.

```csharp
        // Step 2: Reference cell A1 on the first worksheet
        Cell dateCell = workbook.Worksheets[0].Cells["A1"];

        // Put the Japanese era date string into the cell
        dateCell.PutValue("R5-04-01");
```

Η χρήση του `PutValue` αποθηκεύει το ακατέργαστο κείμενο. Το Excel θα το θεωρήσει ως συμβολοσειρά μέχρι μια μορφή αριθμού να του υποδείξει διαφορετικά. Αυτή η προσέγγιση λειτουργεί για οποιαδήποτε προσαρμοσμένη αναπαράσταση ημερολογίου, όχι μόνο για ιαπωνικές εποχές.

## Βήμα 3: Apply a custom number format που κατανοεί την ιαπωνική εποχή

Τώρα **apply custom format** ώστε το Excel να μεταφράσει τη συμβολοσειρά εποχής σε πραγματική σειριακή ημερομηνία. Η μορφή `[ja-JP-Era]yyyy/MM/dd` λέει στη μηχανή να ερμηνεύσει τον αρχικό χαρακτήρα εποχής (`R` για Reiwa) και να υπολογίσει τη Γρηγοριανή ημερομηνία.

```csharp
        // Step 3: Apply a custom number format for Japanese era parsing
        dateCell.Style.Custom = "[ja-JP-Era]yyyy/MM/dd";
```

Η προσαρμοσμένη μορφή αποθηκεύεται στο αντικείμενο στυλ του κελιού. Το Aspose.Cells σέβεται αυτή τη μορφή τόσο κατά την απόδοση όσο και κατά τη μετατροπή τιμής, επιτρέποντας αξιόπιστη **excel date parsing** αργότερα στη διαδικασία.

## Βήμα 4: Retrieve the parsed DateTime value από το κελί

Τέλος, **read date cell** για να αποκτήσετε ένα .NET `DateTime`. Η ιδιότητα `DateTimeValue` επιστρέφει τη μετατρεπόμενη τιμή βάσει της προσαρμοσμένης μορφής που εφαρμόστηκε νωρίτερα.

```csharp
        // Step 4: Retrieve the parsed DateTime value
        DateTime parsedDate = dateCell.DateTimeValue;

        // Output the result to the console for verification
        Console.WriteLine($"Parsed Gregorian date: {parsedDate:yyyy-MM-dd}");
```

Όταν το πρόγραμμα εκτελείται, η κονσόλα εκτυπώνει:

```
Parsed Gregorian date: 2023-04-01
```

Η έξοδος επιβεβαιώνει ότι η συμβολοσειρά ιαπωνικής εποχής `"R5-04-01"` ερμηνεύτηκε σωστά ως 1 Απριλίου 2023.

## Πλήρες, εκτελέσιμο παράδειγμα

Συνδυάζοντας τα κομμάτια προκύπτει ένα αυτόνομο πρόγραμμα που μπορείτε να μεταγλωττίσετε και να εκτελέσετε αμέσως.

```csharp
using Aspose.Cells;
using System;

class JapaneseDateExample
{
    static void Main()
    {
        // Create a new workbook
        Workbook workbook = new Workbook();

        // Reference cell A1
        Cell dateCell = workbook.Worksheets[0].Cells["A1"];

        // Insert Japanese era date string
        dateCell.PutValue("R5-04-01");

        // Apply custom format for Japanese era parsing
        dateCell.Style.Custom = "[ja-JP-Era]yyyy/MM/dd";

        // Retrieve the parsed DateTime
        DateTime parsedDate = dateCell.DateTimeValue;

        // Show the result
        Console.WriteLine($"Parsed Gregorian date: {parsedDate:yyyy-MM-dd}");

        // (Optional) Save the workbook to verify the visual format
        workbook.Save("JapaneseEraDate.xlsx");
    }
}
```

Η εκτέλεση του προγράμματος δημιουργεί το `JapaneseEraDate.xlsx` με το κελί A1 να εμφανίζει `2023/04/01` ενώ η κονσόλα δείχνει την ίδια Γρηγοριανή ημερομηνία. Το αρχείο μπορεί να ανοιχτεί στο Excel για να δείτε τη μορφοποιημένη τιμή.

## Γιατί αυτή η προσέγγιση λειτουργεί

- **create excel workbook** – Η δημιουργία ενός `Workbook` χτίζει τη πλήρη δομή αρχείου Excel στη μνήμη χωρίς να αγγίζει το δίσκο.
- **set cell value** – Το `PutValue` αποθηκεύει ακατέργαστο κείμενο, κάτι που είναι απαραίτητο πριν εφαρμοστεί μια μορφή ειδική για την κουλτούρα.
- **apply custom format** – Το token `[ja-JP-Era]` γεφυρώνει το χάσμα μεταξύ της σημειογραφίας εποχής και του εσωτερικού σειριακού συστήματος ημερομηνιών του Excel.
- **read date cell** – Η `DateTimeValue` χρησιμοποιεί αυτόματα το στυλ του κελιού για να εκτελέσει τη μετατροπή, παρέχοντάς σας ένα εγγενές `DateTime`.
- **excel date parsing** – Αναθέτοντας την ανάλυση στο στυλ του κελιού, αποφεύγετε χειροκίνητη επεξεργασία συμβολοσειρών, μειώνοντας σφάλματα και βελτιώνοντας την υποστήριξη τοπικών ρυθμίσεων.

## Περιπτώσεις άκρων και πρακτικές συμβουλές

- **Different eras** – Χρησιμοποιήστε `S` για Showa, `H` για Heisei, `R` για Reiwa. Η ίδια συμβολοσειρά μορφής λειτουργεί για όλες τις εποχές.
- **Invalid strings** – Εάν το κελί περιέχει μια εσφαλμένη ημερομηνία εποχής, η `DateTimeValue` επιστρέφει `DateTime.MinValue`. Ελέγξτε το `dateCell.IsDate` πριν την ανάγνωση.
- **Multiple cells** – Εφαρμόστε τη προσαρμοσμένη μορφή σε ολόκληρο εύρος (`range.ApplyStyle(style)`) όταν χρειάζεται να αναλύσετε πολλές ημερομηνίες.
- **Performance** – Ο ορισμός του στυλ μία φορά ανά στήλη είναι ταχύτερος από ανά‑κελί για μεγάλα φύλλα.
- **Saving options** – Το Aspose.Cells μπορεί να εξάγει σε XLSX, XLS, CSV ή PDF. Επιλέξτε τη μορφή που ταιριάζει στην επεξεργασία downstream.

## Συχνές ερωτήσεις

**Can I use the built‑in .NET culture instead of a custom format?**  
Η κλάση .NET `CultureInfo` δεν καταλαβαίνει τα σύμβολα ιαπωνικής εποχής με τον ίδιο τρόπο όπως το Excel. Η χρήση μιας προσαρμοσμένης μορφής αριθμού είναι η πιο αξιόπιστη μέθοδος για **excel date parsing** συμβολοσειρών εποχής.

**What if I need to write the date back to Excel in era format?**  
Ορίστε την τιμή του κελιού σε ένα `DateTime` και εφαρμόστε την ίδια προσαρμοσμένη μορφή. Το Excel θα εμφανίσει την εποχή αυτόματα.

**Does this work on older versions of Excel?**  
Το token `[ja-JP-Era]` υποστηρίζεται από το Excel 2010 και μεταγενέστερα. Το Aspose.Cells προσομοιώνει τη συμπεριφορά, έτσι το βιβλίο εργασίας εμφανίζεται σωστά ακόμη και όταν ανοίγει σε παλαιότερες εκδόσεις του Excel που δεν έχουν ενσωματωμένη υποστήριξη εποχών.

## Συμπέρασμα

Τώρα ξέρετε πώς να **create Excel workbook**, **set cell value** με μια συμβολοσειρά ιαπωνικής εποχής, **apply custom format**, και **read date cell** για να αποκτήσετε ένα `DateTime`. Αυτό το πρότυπο παρέχει αξιόπιστη **excel date parsing** χωρίς χειροκίνητη επεξεργασία συμβολοσειρών, κάνοντας τον κώδικα αυτοματοποίησης C# σας σύντομο και αξιόπιστο.

Στη συνέχεια, εξερευνήστε συναφή θέματα όπως **formatting multiple date columns**, **working with other cultural calendars**, ή **exporting the workbook to PDF**. Κάθε επέκταση βασίζεται στις ίδιες αρχές που καλύφθηκαν εδώ, ώστε να μπορείτε να προσαρμόσετε τη λύση σε ένα ευρύ φάσμα σεναρίων τοπικοποίησης. Καλή προγραμματιστική!

## Τι Θα Πρέπει Να Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κυριαρχήσετε επιπλέον δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Δημιουργία Excel Workbook σε C# – Εφαρμογή Προσαρμοσμένης Μορφής Αριθμού](/cells/english/net/excel-custom-number-date-formatting/create-excel-workbook-in-c-apply-custom-number-format/)
- [Δημιουργία Excel Workbook με Προσαρμοσμένη Μορφή – Οδηγός C#](/cells/english/net/excel-custom-number-date-formatting/create-excel-workbook-with-custom-format-c-guide/)
- [Αυτοματοποίηση Excel με Aspose.Cells .NET: Δημιουργία Workbook & Ορισμός Εξωτερικών Συνδέσμων](/cells/english/net/automation-batch-processing/excel-automation-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}