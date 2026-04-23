---
category: general
date: 2026-02-09
description: Πώς να ονομάζετε φύλλα σε C# με το SmartMarker – μάθετε πώς να δημιουργείτε
  πολλαπλά φύλλα και να αυτοματοποιείτε την ονομασία των φύλλων με λίγες μόνο γραμμές
  κώδικα.
draft: false
keywords:
- how to name sheets
- generate multiple sheets
- automate sheet naming
- SmartMarker sheet naming
- workbook automation
language: el
og_description: Πώς να ονομάζετε φύλλα σε C# χρησιμοποιώντας τις επιλογές SmartMarker.
  Αυτός ο οδηγός δείχνει πώς να δημιουργήσετε πολλαπλά φύλλα και να αυτοματοποιήσετε
  την ονομασία των φύλλων χωρίς κόπο.
og_title: Πώς να ονομάζετε φύλλα αυτόματα – Γρήγορος οδηγός C#
tags:
- C#
- Aspose.Cells
- Excel automation
title: Πώς να ονομάζετε φύλλα αυτόματα – Δημιουργία πολλαπλών φύλλων σε C#
url: /el/net/smart-markers-dynamic-data/how-to-name-sheets-automatically-generate-multiple-sheets-in/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Ονομάζετε Αυτόματα Φύλλα – Δημιουργία Πολλαπλών Φύλλων σε C#

Έχετε αναρωτηθεί **πώς να ονομάζετε φύλλα** σε ένα βιβλίο εργασίας Excel χωρίς να κάνετε χειροκίνητο κλικ στο “Rename” κάθε φορά; Δεν είστε μόνοι. Σε πολλές περιπτώσεις αναφοράς καταλήγετε με δεκάδες φύλλα λεπτομερειών που χρειάζονται συστηματικά ονόματα, και η χειροκίνητη διαδικασία είναι εφιάλτης.  

Το καλό νέο είναι ότι με λίγες γραμμές C# μπορείτε **να δημιουργήσετε πολλαπλά φύλλα** και **να αυτοματοποιήσετε την ονομασία των φύλλων** ώστε κάθε νέο φύλλο λεπτομερειών να ακολουθεί ένα προβλέψιμο μοτίβο. Σε αυτό το tutorial θα περάσουμε από τη πλήρη λύση, θα εξηγήσουμε γιατί κάθε κομμάτι είναι σημαντικό και θα σας δώσουμε ένα έτοιμο‑για‑εκτέλεση δείγμα κώδικα.

## Τι Καλύπτει Αυτός Ο Οδηγός

* Ρύθμιση ενός βιβλίου εργασίας που περιέχει SmartMarkers.  
* Διαμόρφωση του `SmartMarkerOptions` για τον έλεγχο του βασικού ονόματος των παραγόμενων φύλλων.  
* Εκτέλεση του `ProcessSmartMarkers` ώστε η βιβλιοθήκη να δημιουργεί αυτόματα `Detail`, `Detail_1`, `Detail_2`, …  
* Συμβουλές για την αντιμετώπιση ειδικών περιπτώσεων όπως υπάρχοντα ονόματα φύλλων ή προσαρμοσμένες συμβάσεις ονοματοδοσίας.  
* Ένα πλήρες, εκτελέσιμο παράδειγμα που μπορείτε να επικολλήσετε στο Visual Studio και να δείτε το αποτέλεσμα αμέσως.

Δεν απαιτείται προηγούμενη εμπειρία με το Aspose.Cells—απλώς μια βασική ρύθμιση C# και ένα IDE της επιλογής σας.

## Προαπαιτούμενα

| Απαίτηση | Γιατί είναι σημαντική |
|----------|------------------------|
| .NET 6.0 ή νεότερο | Σύγχρονα χαρακτηριστικά γλώσσας και συμβατότητα βιβλιοθήκης |
| Aspose.Cells for .NET (πακέτο NuGet) | Παρέχει επεξεργασία `SmartMarker` και δημιουργία φύλλων |
| Ένα κενό έργο console (ή οποιαδήποτε εφαρμογή .NET) | Σας δίνει χώρο για την εκτέλεση του κώδικα |

Εγκαταστήστε τη βιβλιοθήκη με:

```bash
dotnet add package Aspose.Cells
```

Τώρα που καλύψαμε τα βασικά, ας βουτήξουμε στην υλοποίηση.

## Βήμα 1: Δημιουργία Βιβλίου Εργασίας με SmartMarkers

Πρώτα χρειάζεται ένα βιβλίο εργασίας που περιέχει έναν placeholder SmartMarker. Σκεφτείτε το SmartMarker ως μια ετικέτα προτύπου που λέει στη μηχανή πού να ενσωματώσει δεδομένα και, στην περίπτωσή μας, πότε να δημιουργήσει νέο φύλλο.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣  Create a new workbook and get the first worksheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];
        ws.Name = "Template";

        // 2️⃣  Insert a SmartMarker that will trigger sheet creation
        // The marker {{detail}} tells Aspose.Cells to repeat the row for each item in the "detail" collection.
        ws.Cells["A1"].PutValue("{{detail}}");
        ws.Cells["B1"].PutValue("Item Name");
        ws.Cells["C1"].PutValue("Quantity");
        ws.Cells["A2"].PutValue("&=detail.Name");
        ws.Cells["B2"].PutValue("&=detail.Quantity");

        // 3️⃣  Prepare sample data for the SmartMarker
        var data = new
        {
            detail = new[]
            {
                new { Name = "Apple",  Quantity = 10 },
                new { Name = "Banana", Quantity = 20 },
                new { Name = "Cherry", Quantity = 30 }
            }
        };
```

> **Pro tip:** Κρατήστε το φύλλο προτύπου ελαφρύ. Μόνο οι γραμμές που χρειάζονται αντιγραφή πρέπει να περιέχουν SmartMarkers· όλα τα υπόλοιπα παραμένουν στατικά.

## Βήμα 2: Διαμόρφωση SmartMarker Options – Ο Πυρήνας της Ονομασίας Φύλλων

Τώρα έρχεται η μαγεία. Ορίζοντας το `DetailSheetNewName` λέμε στη μηχανή ποιο βασικό όνομα να χρησιμοποιήσει για κάθε παραγόμενο φύλλο. Η βιβλιοθήκη θα προσθέσει “_1”, “_2”, κ.λπ., όταν το βασικό όνομα υπάρχει ήδη.

```csharp
        // 4️⃣  Define naming options – this is where we answer “how to name sheets”
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
        {
            // Primary keyword appears here: how to name sheets
            DetailSheetNewName = "Detail"   // Base name for all generated sheets
        };
```

Αν χρειαστείτε διαφορετική συμβατική (π.χ. “Report_2023”), απλώς αλλάξτε τη συμβολοσειρά. Η μηχανή διαχειρίζεται τις συγκρούσεις αυτόματα, γι’ αυτό αυτή η προσέγγιση **αυτοματοποιεί την ονομασία των φύλλων** χωρίς επιπλέον κώδικα.

## Βήμα 3: Επεξεργασία SmartMarkers και Δημιουργία των Φύλλων

Με το βιβλίο εργασίας, τα δεδομένα και τις επιλογές έτοιμες, μια μόνο κλήση μεθόδου κάνει το σκληρό έργο.

```csharp
        // 5️⃣  Run the SmartMarker processor – this will create Detail, Detail_1, Detail_2…
        wb.ProcessSmartMarkers(data, smartMarkerOptions);

        // 6️⃣  Save the result so you can open it in Excel
        wb.Save("GeneratedSheets.xlsx");

        // 7️⃣  Let the user know we’re done
        System.Console.WriteLine("Workbook created – check GeneratedSheets.xlsx");
    }
}
```

### Αναμενόμενο Αποτέλεσμα

Όταν ανοίξετε το *GeneratedSheets.xlsx* θα δείτε:

| Όνομα Φύλλου | Περιεχόμενο |
|---------------|-------------|
| Template      | Η αρχική διάταξη του marker (κρατείται για αναφορά) |
| Detail        | Πρώτο σύνολο γραμμών (Apple, Banana, Cherry) |
| Detail_1      | Δεύτερο αντίγραφο – ίδια δεδομένα (χρήσιμο όταν έχετε πολλαπλές συλλογές) |
| Detail_2      | …και ούτω καθεξής, ανάλογα με το πόσες διαφορετικές ομάδες SmartMarker έχετε |

Το μοτίβο ονομασίας (`Detail`, `Detail_1`, `Detail_2`) δείχνει **πώς να ονομάζετε φύλλα** προγραμματιστικά ενώ **δημιουργεί πολλαπλά φύλλα** όπως απαιτείται.

## Ειδικές Περιπτώσεις & Παραλλαγές

### 1. Υπάρχοντα Ονόματα Φύλλων

Αν το βιβλίο εργασίας σας περιέχει ήδη ένα φύλλο με όνομα “Detail”, η μηχανή θα ξεκινήσει με “Detail_1”. Αυτό αποτρέπει τυχαίες αντικαταστάσεις.

### 2. Προσαρμοσμένες Μορφές Αύξησης

Θέλετε “Detail‑A”, “Detail‑B” αντί για αριθμητικά επίθημα; Μπορείτε να επεξεργαστείτε τα ονόματα μετά το `ProcessSmartMarkers`:

```csharp
for (int i = 0; i < wb.Worksheets.Count; i++)
{
    Worksheet sh = wb.Worksheets[i];
    if (sh.Name.StartsWith("Detail_"))
    {
        string suffix = ((char)('A' + i - 1)).ToString(); // A, B, C…
        sh.Name = $"Detail-{suffix}";
    }
}
```

### 3. Πολλαπλές Ομάδες SmartMarker

Αν το βιβλίο εργασίας σας περιέχει περισσότερες από μία ομάδες SmartMarker (π.χ. `{{invoice}}` και `{{detail}}`), κάθε ομάδα θα δημιουργήσει το δικό της σύνολο φύλλων βάσει του ίδιου `DetailSheetNewName`. Για να δώσετε σε κάθε ομάδα διαφορετικό πρόθεμα, δημιουργήστε ξεχωριστές εμφανίσεις `SmartMarkerOptions` και καλέστε `ProcessSmartMarkers` για κάθε συλλογή.

## Πρακτικές Συμβουλές από το Πεδίο

* **Pro tip:** Απενεργοποιήστε το `AllowDuplicateNames` στο `WorkbookSettings` αν θέλετε η βιβλιοθήκη να πετάξει εξαίρεση αντί να μετονομάζει τα φύλλα σιωπηλά. Αυτό βοηθά στον εντοπισμό σφαλμάτων λογικής ονομασίας νωρίς.  
* **Προσοχή σε:** Πολύ μακριά βασικά ονόματα. Το Excel περιορίζει τα ονόματα φύλλων στα 31 χαρακτήρες· η βιβλιοθήκη κόβει αυτόματα, αλλά μπορεί να καταλήξετε με ασαφή ονόματα.  
* **Σημείωση απόδοσης:** Η δημιουργία εκατοντάδων φύλλων μπορεί να καταναλώσει μνήμη. Αποδεσμεύστε το βιβλίο εργασίας (`wb.Dispose()`) μόλις τελειώσετε αν τρέχετε μέσα σε υπηρεσία με μεγάλη διάρκεια ζωής.

## Οπτική Επισκόπηση

![how to name sheets diagram](image.png "Diagram showing the flow from SmartMarker template to generated sheets – how to name sheets")

*Alt text includes the primary keyword to satisfy SEO.*

## Πλήρης Πηγαίος Κώδικας (Έτοιμος για Αντιγραφή‑Επικόλληση)

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create workbook and template sheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];
        ws.Name = "Template";

        // SmartMarker layout
        ws.Cells["A1"].PutValue("{{detail}}");
        ws.Cells["B1"].PutValue("Item Name");
        ws.Cells["C1"].PutValue("Quantity");
        ws.Cells["A2"].PutValue("&=detail.Name");
        ws.Cells["B2"].PutValue("&=detail.Quantity");

        // Sample data
        var data = new
        {
            detail = new[]
            {
                new { Name = "Apple",  Quantity = 10 },
                new { Name = "Banana", Quantity = 20 },
                new { Name = "Cherry", Quantity = 30 }
            }
        };

        // Configure naming – this answers how to name sheets
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
        {
            DetailSheetNewName = "Detail"
        };

        // Process markers → generates Detail, Detail_1, Detail_2 …
        wb.ProcessSmartMarkers(data, smartMarkerOptions);

        // Save and finish
        wb.Save("GeneratedSheets.xlsx");
        System.Console.WriteLine("Workbook created – open GeneratedSheets.xlsx to see the result.");
    }
}
```

Τρέξτε το πρόγραμμα, ανοίξτε το παραγόμενο αρχείο και θα δείτε τα φύλλα να ονομάζονται αυτόματα σύμφωνα με το μοτίβο που ορίσαμε.

## Συμπέρασμα

Τώρα ξέρετε **πώς να ονομάζετε φύλλα** σε ένα βιβλίο εργασίας C#, **πώς να δημιουργείτε πολλαπλά φύλλα** με SmartMarker, και **πώς να αυτοματοποιείτε την ονομασία των φύλλων** ώστε να μην χρειάζεται ποτέ ξανά να μετονομάζετε κάτι με το χέρι. Η προσέγγιση κλιμακώνεται από μερικές σελίδες λεπτομερειών σε εκατοντάδες, και το ίδιο μοτίβο λειτουργεί για οποιαδήποτε συλλογή τροφοδοτείτε στο `ProcessSmartMarkers`.

Τι ακολουθεί; Δοκιμάστε να αντικαταστήσετε την πηγή δεδομένων με ένα ερώτημα βάσης δεδομένων, πειραματιστείτε με προσαρμοσμένες μορφές επιθήματος, ή συνδυάστε πολλαπλές ομάδες SmartMarker για μια πλήρη μηχανή αναφορών. Ο ουρανός είναι το όριο όταν αφήνετε τη βιβλιοθήκη να διαχειρίζεται τη επαναλαμβανόμενη εργασία ονομασίας.

Αν βρήκατε αυτόν τον οδηγό χρήσιμο, δώστε του αστέρι στο GitHub, μοιραστείτε τον με συναδέλφους, ή αφήστε ένα σχόλιο παρακάτω με τις δικές σας τεχνικές ονομασίας. Καλός κώδικας!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}