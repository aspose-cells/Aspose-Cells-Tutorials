---
category: general
date: 2026-02-14
description: Δημιουργήστε αντικείμενο κύριων δεδομένων σε C# και δημιουργήστε το φύλλο
  λεπτομερειών χωρίς κόπο. Μάθετε τη πλήρη ροή εργασίας του SmartMarker με πρακτικά
  παραδείγματα κώδικα.
draft: false
keywords:
- create master data object
- generate detail sheet
- smartmarker processing
- worksheet automation
- c# data binding
language: el
og_description: Δημιουργήστε αντικείμενο κύριων δεδομένων σε C# και δημιουργήστε φύλλο
  λεπτομερειών με το SmartMarker. Ακολουθήστε το αναλυτικό μας σεμινάριο για μια έτοιμη
  προς εκτέλεση λύση.
og_title: Δημιουργία αντικειμένου κύριων δεδομένων – Πλήρης οδηγός
tags:
- C#
- SmartMarker
- Excel Automation
title: Δημιουργία Αντικειμένου Κύριων Δεδομένων – Οδηγός Βήμα‑Βήμα για τη Δημιουργία
  Φύλλου Λεπτομερειών
url: /el/net/smart-markers-dynamic-data/create-master-data-object-step-by-step-guide-to-generate-det/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία Αντικειμένου Master Data – Πλήρης Οδηγός

Κάποτε χρειάστηκε να **δημιουργήσετε αντικείμενο master data** για ένα φύλλο εργασίας Excel αλλά δεν ήξερες πώς να το συνδέσεις με ένα φύλλο λεπτομερειών SmartMarker; Δεν είσαι μόνος. Σε πολλές περιπτώσεις αναφοράς το master object οδηγεί ένα δυναμικό φύλλο λεπτομερειών, και η σωστή σύνδεση μπορεί να μοιάζει με συναρμολόγηση παζλ χωρίς εικόνα.

Σε αυτόν τον οδηγό θα περάσουμε από όλη τη διαδικασία — δημιουργία του αντικειμένου master data, ρύθμιση των επιλογών SmartMarker για **δημιουργία φύλλου λεπτομερειών**, και τέλος εκτέλεση του επεξεργαστή. Στο τέλος θα έχεις ένα εκτελέσιμο απόσπασμα που μπορείς να επικολλήσεις σε οποιοδήποτε .NET project που χρησιμοποιεί τη βιβλιοθήκη GrapeCity Documents for Excel (GcExcel).

## Τι Θα Χρειαστείς

- .NET 6+ (ή .NET Framework 4.7.2) με αναφορά στο `GcExcel.dll`
- Βασική εξοικείωση με C# (μεταβλητές, ανώνυροι τύποι, αρχικοποιητές αντικειμένων)
- Ένα βιβλίο εργασίας Excel που ήδη περιέχει ετικέτες SmartMarker όπως `{{OrderId}}` και έναν πίνακα για στοιχεία γραμμής
- Visual Studio, Rider ή οποιονδήποτε επεξεργαστή προτιμάς

Αυτό είναι όλο — δεν χρειάζονται επιπλέον πακέτα NuGet εκτός της βασικής διανομής GcExcel.

## Βήμα 1: Δημιουργία του Αντικειμένου Master Data

Το πρώτο που πρέπει να κάνεις είναι **να δημιουργήσεις αντικείμενο master data** που να αντικατοπτρίζει τη δομή που αναμένουν οι ετικέτες SmartMarker. Σκέψου το ως ένα μικρό μοντέλο αναφοράς στη μνήμη.

```csharp
// Step 1: Build the master data object that feeds the SmartMarkers.
// It contains an OrderId and a collection of line items.
var orderData = new
{
    OrderId = 1,
    Items = new[]
    {
        new { Product = "A", Quantity = 2 },
        new { Product = "B", Quantity = 5 }
    }
};
```

Γιατί χρησιμοποιούμε ανώνυμο τύπο εδώ; Επειδή σου επιτρέπει να ορίσεις ένα ελαφρύ container χωρίς να δηλώσεις μια πλήρη κλάση — ιδανικό για γρήγορες επιδείξεις ή όταν το σχήμα είναι απίθανο να αλλάξει. Αν αργότερα χρειαστείς ένα επαναχρησιμοποιήσιμο μοντέλο, απλώς αντικατέστησε το `var` με ένα κατάλληλο POCO.

> **Συμβουλή:** Κράτησε τα ονόματα των ιδιοτήτων (`OrderId`, `Product`, `Quantity`) ακριβώς όπως τα placeholders στο φύλλο εργασίας· το SmartMarker τα ταιριάζει χωρίς διάκριση πεζών‑κεφαλαίων.

## Βήμα 2: Ρύθμιση των Επιλογών SmartMarker για Δημιουργία Φύλλου Λεπτομερειών

Τώρα λέμε στο SmartMarker ότι θέλουμε ένα ξεχωριστό φύλλο για τον πίνακα στοιχείων γραμμής. Εδώ έρχεται σε παίξη η λέξη-κλειδί **generate detail sheet**.

```csharp
// Step 2: Set up SmartMarker options.
// Enabling DetailSheet creates a new sheet for each master record.
var smartMarkerOptions = new SmartMarkerOptions
{
    DetailSheet = true,
    // The new sheet will be named using the OrderId value.
    DetailSheetNewName = "Order_{OrderId}"
};
```

Το πρότυπο `DetailSheetNewName` χρησιμοποιεί placeholders σε αγκύλες που αντικαθίστανται κατά την εκτέλεση. Στο παράδειγμά μας το φύλλο θα ονομαστεί `Order_1`. Αν αργότερα κάνεις βρόχο πάνω σε πολλαπλές παραγγελίες, η καθεμία θα παίρνει τη δική της καρτέλα — ακριβώς αυτό που περιμένουν οι περισσότεροι λογιστές.

## Βήμα 3: Εκτέλεση του Επεξεργαστή SmartMarker

Με τα δεδομένα και τις επιλογές έτοιμες, το τελευταίο βήμα είναι να καλέσεις τον επεξεργαστή στο στοχευόμενο φύλλο εργασίας.

```csharp
// Step 3: Execute SmartMarker processing on the worksheet.
// 'worksheet' is an IWorksheet instance that points to the template sheet.
worksheet.SmartMarkerProcessor.StartSmartMarkerProcessing(orderData, smartMarkerOptions);
```

Στο παρασκήνιο, το SmartMarker σαρώει το φύλλο για ετικέτες, ενσωματώνει τις τιμές του `orderData`, και επειδή το `DetailSheet` είναι `true`, κλωνοποιεί το πρότυπο σε νέο φύλλο με όνομα `Order_1`. Όλα τα στοιχεία γραμμής εμφανίζονται στην περιοχή λεπτομερειών, διατηρώντας οποιαδήποτε μορφοποίηση είχες εφαρμόσει στο πρότυπο.

### Πλήρες Παράδειγμα Λειτουργίας

Παρακάτω υπάρχει ένα αυτόνομο πρόγραμμα κονσόλας που ανοίγει ένα βιβλίο εργασίας προτύπου (`Template.xlsx`), εκτελεί τα τρία βήματα και αποθηκεύει το αποτέλεσμα ως `Result.xlsx`. Μπορείς να το αντιγράψεις‑επικολλήσεις σε ένα νέο project κονσόλας και να πατήσεις **F5**.

```csharp
using System;
using GrapeCity.Documents.Excel;

class Program
{
    static void Main()
    {
        // Load the Excel template that contains SmartMarker tags.
        var workbook = new Workbook();
        workbook.Open("Template.xlsx");

        // -------------------------------------------------
        // Step 1: Create the master data object.
        // -------------------------------------------------
        var orderData = new
        {
            OrderId = 1,
            Items = new[]
            {
                new { Product = "A", Quantity = 2 },
                new { Product = "B", Quantity = 5 }
            }
        };

        // -------------------------------------------------
        // Step 2: Configure SmartMarker options to generate detail sheet.
        // -------------------------------------------------
        var smartMarkerOptions = new SmartMarkerOptions
        {
            DetailSheet = true,
            DetailSheetNewName = "Order_{OrderId}"
        };

        // -------------------------------------------------
        // Step 3: Process the worksheet.
        // -------------------------------------------------
        // Assume the first sheet holds the master template.
        var worksheet = workbook.Worksheets[0];
        worksheet.SmartMarkerProcessor.StartSmartMarkerProcessing(orderData, smartMarkerOptions);

        // Save the populated workbook.
        workbook.Save("Result.xlsx");
        Console.WriteLine("Done! Check Result.xlsx – a new sheet named Order_1 should exist.");
    }
}
```

#### Αναμενόμενο Αποτέλεσμα

- **Result.xlsx** περιέχει ένα φύλλο που ονομάζεται `Order_1`.
- Το κελί `A1` (ή όπου τοποθέτησες το `{{OrderId}}`) τώρα δείχνει `1`.
- Ένας πίνακας που ξεκινά από το μπλοκ SmartMarker εμφανίζει δύο γραμμές:
  | Product | Quantity |
  |---------|----------|
  | A       | 2        |
  | B       | 5        |

Αν ανοίξεις το αρχείο, θα δεις τη μορφοποίηση από το πρότυπο διατηρημένη — περιγράμματα, γραμματοσειρές, μορφοποίηση υπό όρους — όλα άθικτα.

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

### Τι γίνεται αν έχω πολλαπλές παραγγελίες;

Τυλίγεις το αντικείμενο master σε μια συλλογή και αφήνεις το SmartMarker να επαναλάβει αυτόματα:

```csharp
var orders = new[]
{
    new {
        OrderId = 1,
        Items = new[] { new { Product = "A", Quantity = 2 } }
    },
    new {
        OrderId = 2,
        Items = new[] { new { Product = "C", Quantity = 3 } }
    }
};

worksheet.SmartMarkerProcessor.StartSmartMarkerProcessing(orders, smartMarkerOptions);
```

Κάθε παραγγελία δημιουργεί το δικό της φύλλο (`Order_1`, `Order_2`, …). Ο επεξεργαστής αντιμετωπίζει τον εξωτερικό πίνακα ως τη κύρια συλλογή.

### Πώς ελέγχω τη θέση του φύλλου;

Ορίζεις `smartMarkerOptions.DetailSheetInsertIndex = 2;` για να τοποθετήσεις το νέο φύλλο μετά τη δεύτερη καρτέλα, ή χρησιμοποιείς `DetailSheetInsertAfter = "Summary"` για να το εισάγεις μετά από ένα φύλλο με όνομα.

### Μπορώ να απενεργοποιήσω το φύλλο λεπτομερειών για μια συγκεκριμένη εκτέλεση;

Απλώς θέσε `DetailSheet = false;`. Το SmartMarker τότε θα γράψει τα στοιχεία γραμμής στο ίδιο φύλλο όπου βρίσκονται οι κύριες ετικέτες.

### Τι γίνεται με μεγάλα σύνολα δεδομένων;

Το SmartMarker ρέει τα δεδομένα αποδοτικά, αλλά αν ξεπεράσεις μερικές εκατοντάδες χιλιάδες γραμμές μπορείς να φτάσεις το όριο των 1.048.576 γραμμών του Excel. Σε αυτήν την περίπτωση διαίρεσε τα δεδομένα σε πολλαπλές εγγραφές master ή σκέψου εξαγωγή σε CSV.

## Οπτική Επισκόπηση

![Διάγραμμα που απεικονίζει πώς να δημιουργήσετε αντικείμενο master data και να δημιουργήσετε φύλλο λεπτομερειών χρησιμοποιώντας το SmartMarker](/images/smartmarker-flow.png)

*Η εικονογράφηση δείχνει τη ροή από το αντικείμενο master C# → επιλογές SmartMarker → επεξεργασία φύλλου εργασίας → νέο φύλλο λεπτομερειών.*

## Συμπέρασμα

Τώρα ξέρεις πώς να **δημιουργήσεις αντικείμενο master data** σε C# και να ρυθμίσεις το SmartMarker ώστε να **δημιουργεί αυτόματα φύλλο λεπτομερειών**. Το μοτίβο τριών βημάτων — δεδομένα, επιλογές, επεξεργαστής — καλύπτει την πλειονότητα των σεναρίων αυτοματοποίησης Excel με το GcExcel.

Από εδώ μπορείς να εξερευνήσεις:

- Προσθήκη δεδομένων κεφαλίδας/υποσέλιδου σε κάθε φύλλο λεπτομερειών
- Χρήση μορφοποίησης υπό όρους βάσει κατάστασης παραγγελίας
- Εξαγωγή του παραγόμενου βιβλίου εργασίας σε PDF με `workbook.SaveAsPdf(...)`

Νιώσε ελεύθερος/η να πειραματιστείς, να σπάσεις πράγματα και μετά να τα επανασυνδέσεις. Αυτός είναι ο πιο γρήγορος τρόπος να κυριαρχήσεις στην αυτοματοποίηση φύλλων εργασίας. Καλό κώδικα!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}