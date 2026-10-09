---
category: general
date: 2026-05-23
description: Πώς να χρησιμοποιήσετε δείκτες με το Aspose.Cells για να επιτύχετε δυναμική
  ονομασία φύλλων σε αυτοματοποίηση Excel. Μάθετε έξυπνους δείκτες, σύνδεση δεδομένων
  JSON και δημιουργία φύλλων σε λίγα λεπτά.
draft: false
keywords:
- how to use markers
- dynamic sheet naming excel
- aspose.cells smart markers
language: el
og_description: Πώς να χρησιμοποιήσετε δείκτες στο Aspose.Cells για τη δημιουργία
  αρχείων Excel με δυναμική ονομασία φύλλων. Πλήρης οδηγός βήμα‑βήμα με πλήρες παράδειγμα
  C#.
og_title: Πώς να χρησιμοποιήσετε δείκτες – Δυναμική ονομασία φύλλων στο Excel με το
  Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: How to use markers with Aspose.Cells to achieve dynamic sheet naming
    Excel automation. Learn smart markers, JSON data binding, and sheet creation in
    minutes.
  headline: How to Use Markers in Aspose.Cells for Dynamic Sheet Naming in Excel
  type: TechArticle
- description: How to use markers with Aspose.Cells to achieve dynamic sheet naming
    Excel automation. Learn smart markers, JSON data binding, and sheet creation in
    minutes.
  name: How to Use Markers in Aspose.Cells for Dynamic Sheet Naming in Excel
  steps:
  - name: What Happens Under the Hood?
    text: 1. The processor reads the `Orders` array. 2. For each order it creates
      a **master sheet** (using `${Orders.MasterSheetName}`) and a **detail sheet**
      (using the `DetailSheetNewName` pattern). 3. Cell values are replaced with the
      corresponding JSON fields, so the master sheet’s first cell ends up con
  - name: What if I need more than two levels of hierarchy?
    text: You can nest markers inside the newly created detail sheets. Just place
      additional `${...}` tags in the template sheet before processing. The processor
      will cascade through each level automatically.
  - name: Can I use a DataTable instead of JSON?
    text: Absolutely. `SmartMarkerProcessor` has overloads for `DataSet`, `DataTable`,
      and even custom objects. The only change is the call to `ApplyJson` – you’d
      use `ApplyDataSet(myDataSet)` instead.
  - name: How do I control the order of sheet creation?
    text: The order follows the sequence of the source collection. If you need a custom
      sort, simply sort the JSON array (or DataTable) before passing it to the processor.
  - name: Is there a way to hide the template sheet after processing?
    text: Yes. Set `sm.Options.RemoveTemplateSheets = true;` before calling `ApplyJson`.
      The original sheet (index 0) will be removed from the final workbook.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Πώς να χρησιμοποιήσετε δείκτες στο Aspose.Cells για δυναμική ονομασία φύλλων
  στο Excel
url: /el/net/smart-markers-dynamic-data/how-to-use-markers-in-aspose-cells-for-dynamic-sheet-naming/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Χρησιμοποιήσετε Markers στο Aspose.Cells για Δυναμική Ονομασία Φύλλων σε Excel

Έχετε αναρωτηθεί ποτέ **πώς να χρησιμοποιήσετε markers** για να μετατρέψετε ένα στατικό πρότυπο Excel σε ένα πλήρες βιβλίο εργασίας master‑detail; Δεν είστε μόνοι. Πολλοί προγραμματιστές συναντούν δυσκολίες όταν χρειάζονται δυνατότητες *dynamic sheet naming excel*, ειδικά όταν τα ονόματα των φύλλων πρέπει να αντικατοπτρίζουν τιμές δεδομένων που προέρχονται από JSON ή μια βάση δεδομένων.  

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από ένα πλήρες, έτοιμο προς εκτέλεση παράδειγμα C# που δείχνει **πώς να χρησιμοποιήσετε markers** με **Aspose.Cells** smart markers, να δεσμεύσετε δεδομένα JSON, και να αφήσετε τον επεξεργαστή να δημιουργήσει φύλλα των οποίων τα ονόματα αλλάζουν δυναμικά. Χωρίς περιττές εξηγήσεις, μόνο ο ακριβής κώδικας που μπορείτε να ενσωματώσετε στο Visual Studio και να δείτε τα αποτελέσματα αμέσως.

## Τι Θα Μάθετε

- Η έννοια των **smart markers** και γιατί είναι ιδανικά για σενάρια master‑detail.  
- Πώς να ενσωματώσετε ετικέτες marker σε ένα βιβλίο εργασίας που θα αντικατασταθούν αργότερα με πραγματικά ονόματα φύλλων.  
- Ρύθμιση **dynamic sheet naming excel** χρησιμοποιώντας την επιλογή `DetailSheetNewName`.  
- Εκτέλεση του `SmartMarkerProcessor` με δεδομένα JSON για αυτόματη δημιουργία πολλαπλών φύλλων.  
- Επαλήθευση του αποτελέσματος και μερικές χρήσιμες συμβουλές για την αποφυγή κοινών παγίδων.

> **Prerequisites** – Χρειάζεστε ένα πρόσφατο .NET runtime (≥ .NET 6 είναι εντάξει), τη βιβλιοθήκη Aspose.Cells for .NET (μπορείτε να κατεβάσετε μια δωρεάν δοκιμή από την Aspose) και βασική εξοικείωση με τη γλώσσα C#.  

---

![παράδειγμα χρήσης markers στο Aspose.Cells](example.png "παράδειγμα χρήσης markers στο Aspose.Cells")

## Πώς να Χρησιμοποιήσετε Markers για Δημιουργία Δυναμικής Ονομασίας Φύλλων (Βήμα 1)

Το πρώτο που χρειάζεται είναι ένα κενό βιβλίο εργασίας που θα λειτουργήσει ως πρότυπο. Σε ένα πραγματικό έργο πιθανότατα θα ξεκινούσατε από ένα υπάρχον αρχείο `.xlsx` που περιέχει ήδη διάταξη, μορφοποίηση και κελιά placeholder. Για λόγους σαφήνειας θα δημιουργήσουμε τα πάντα προγραμματιστικά.

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarker;

// Step 1: Create a new workbook and get the first worksheet
Workbook wb = new Workbook();                // fresh workbook, no sheets yet
Worksheet ws = wb.Worksheets[0];             // default first sheet
```

*Γιατί είναι σημαντικό*: Το αντικείμενο `Worksheet` είναι όπου θα τοποθετήσουμε τις ετικέτες **smart marker**. Σκεφτείτε τις ετικέτες ως μικροσκοπικούς placeholders που ο επεξεργαστής θα αντικαταστήσει αργότερα με πραγματικές τιμές από το JSON.  

## Εισαγωγή Smart Marker Tags (Βήμα 2)

Τώρα τοποθετούμε τις ετικέτες marker απευθείας στα κελιά. Η σύνταξη `${...}` λέει στο Aspose.Cells «αυτή είναι μια ετικέτα». Στο παράδειγμά μας χρειαζόμαστε δύο markers: ένα για το όνομα του master φύλλου και ένα για το όνομα του detail φύλλου.

```csharp
// Step 2: Insert Smart Marker tags that will be replaced with sheet names
ws.Cells[0, 0].PutValue("${Orders.MasterSheetName}");   // master sheet placeholder
ws.Cells[1, 0].PutValue("${Orders.DetailSheetName}");   // detail sheet placeholder
```

> **Pro tip** – Κρατήστε τα ονόματα των markers σύντομα και περιγραφικά· γίνονται τα κλειδιά που θα χρησιμοποιήσετε στο JSON payload.  

## Προετοιμασία των Δεδομένων JSON (Βήμα 3)

Ο επεξεργαστής λειτουργεί με οποιαδήποτε πηγή δεδομένων που μπορεί να αναπαρασταθεί ως JSON, `DataSet`, ή ακόμη και απλό αντικείμενο. Ακολουθεί ένα ελάχιστο JSON string που περιέχει μια συλλογή master‑detail. Παρατηρήστε ότι κάθε παραγγελία περιέχει τόσο `MasterSheetName` όσο και `DetailSheetName`.

```csharp
// Step 3: Prepare the JSON data that contains the master‑detail information
string jsonOrders = @"{
    ""Orders"": [
        {
            ""OrderId"": 1,
            ""MasterSheetName"": ""Master_1"",
            ""DetailSheetName"": ""Detail_1""
        },
        {
            ""OrderId"": 2,
            ""MasterSheetName"": ""Master_2"",
            ""DetailSheetName"": ""Detail_2""
        }
    ]
}";
```

*Γιατί JSON?* Είναι ελαφρύ, ανθρώπινα αναγνώσιμο, και λειτουργεί άψογα με web APIs. Θα μπορούσατε εξίσου εύκολα να αντλήσετε αυτά τα δεδομένα από ένα ερώτημα SQL και να τα σειριοποιήσετε με `Newtonsoft.Json`.  

## Αρχικοποίηση του SmartMarkerProcessor (Βήμα 4)

Το `SmartMarkerProcessor` είναι η μηχανή που σαρώνει το βιβλίο εργασίας, εντοπίζει markers και εκτελεί τη δέσμευση δεδομένων. Η δημιουργία του είναι μια γραμμή κώδικα.

```csharp
// Step 4: Initialise the SmartMarkerProcessor with the workbook
SmartMarkerProcessor sm = new SmartMarkerProcessor(wb);
```

## Ορισμός Δυναμικής Ονομασίας Φύλλων (Βήμα 5)

Εδώ το **dynamic sheet naming excel** δείχνει την πραγματική του αξία. Ορίζοντας το `DetailSheetNewName`, λέμε στον επεξεργαστή να δημιουργήσει ένα νέο detail φύλλο για κάθε παραγγελία και να το ονομάσει βάσει του `OrderId`. Η placeholder `${OrderId}` λύνει την τιμή από την τρέχουσα εγγραφή κατά την επεξεργασία.

```csharp
// Step 5: Define how new detail sheets should be named during processing
sm.Options.DetailSheetNewName = "Detail_${OrderId}";
```

> **Watch out** – Αν παραλείψετε τη σύνταξη `${}`, το φύλλο θα ονομαστεί κυριολεκτικά “Detail_${OrderId}” αντί για “Detail_1”, “Detail_2”, κ.λπ.  

## Εφαρμογή JSON και Δημιουργία Φύλλων (Βήμα 6)

Τώρα αφήνουμε τον επεξεργαστή να κάνει το σκληρό έργο. Θα διαβάσει το JSON, θα αντικαταστήσει τα markers και θα δημιουργήσει νέα worksheets όπως απαιτείται.

```csharp
// Step 6: Apply the JSON data to populate the smart markers and generate sheets
sm.ApplyJson(jsonOrders);
```

### Τι Συμβαίνει Πίσω από τις Σκηνές;

1. Ο επεξεργαστής διαβάζει τον πίνακα `Orders`.  
2. Για κάθε παραγγελία δημιουργεί ένα **master sheet** (χρησιμοποιώντας `${Orders.MasterSheetName}`) και ένα **detail sheet** (χρησιμοποιώντας το πρότυπο `DetailSheetNewName`).  
3. Οι τιμές των κελιών αντικαθίστανται με τα αντίστοιχα πεδία JSON, έτσι το πρώτο κελί του master sheet περιέχει “Master_1”, “Master_2”, κ.λπ.  

## Αποθήκευση και Επαλήθευση του Αποτελέσματος (Προαιρετικό)

Τέλος, γράφουμε το βιβλίο εργασίας στο δίσκο. Ανοίξτε το αρχείο στο Excel και θα πρέπει να δείτε δύο master φύλλα (`Master_1`, `Master_2`) και δύο δυναμικά ονομασμένα detail φύλλα (`Detail_1`, `Detail_2`).  

```csharp
// (Optional) Save the result to verify the output
wb.Save("output.xlsx");
```

**Expected output** – Μετά το άνοιγμα του `output.xlsx` θα δείτε:

- Φύλλο **Master_1** με κελί A1 = “Master_1”.  
- Φύλλο **Detail_1** με κελί A1 = “Detail_1”.  
- Φύλλο **Master_2** με κελί A1 = “Master_2”.  
- Φύλλο **Detail_2** με κελί A1 = “Detail_2”.  

Αυτή είναι η πλήρης διαδικασία **πώς να χρησιμοποιήσετε markers** για να επιτύχετε **dynamic sheet naming excel** με **Aspose.Cells smart markers**.

---

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

### Τι γίνεται αν χρειαστώ περισσότερα από δύο επίπεδα ιεραρχίας;

Μπορείτε να ενσωματώσετε markers μέσα στα νεοδημιουργημένα detail φύλλα. Απλώς τοποθετήστε επιπλέον ετικέτες `${...}` στο φύλλο προτύπου πριν την επεξεργασία. Ο επεξεργαστής θα προχωρήσει αυτόματα σε κάθε επίπεδο.

### Μπορώ να χρησιμοποιήσω DataTable αντί για JSON;

Απόλυτα. Το `SmartMarkerProcessor` διαθέτει overloads για `DataSet`, `DataTable` και ακόμη και προσαρμοσμένα αντικείμενα. Η μόνη αλλαγή είναι η κλήση σε `ApplyJson` – θα χρησιμοποιούσατε `ApplyDataSet(myDataSet)` αντί αυτού.

### Πώς ελέγχω τη σειρά δημιουργίας των φύλλων;

Η σειρά ακολουθεί τη σειρά της πηγής συλλογής. Αν χρειάζεστε προσαρμοσμένη ταξινόμηση, απλώς ταξινομήστε τον πίνακα JSON (ή το DataTable) πριν τον περάσετε στον επεξεργαστή.

### Υπάρχει τρόπος να κρύψω το φύλλο προτύπου μετά την επεξεργασία;

Ναι. Ορίστε `sm.Options.RemoveTemplateSheets = true;` πριν καλέσετε `ApplyJson`. Το αρχικό φύλλο (δείκτης 0) θα αφαιρεθεί από το τελικό βιβλίο εργασίας.

---

## Πλήρες Παράδειγμα Εργασίας (Όλα τα Βήματα Συνδυασμένα)

Παρακάτω βρίσκεται το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε‑επικολλήσετε σε ένα νέο C# console project. Βεβαιωθείτε ότι έχετε προσθέσει το πακέτο NuGet `Aspose.Cells`.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.SmartMarker;

namespace DynamicSheetNamingDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook and get the first worksheet
            Workbook wb = new Workbook();
            Worksheet ws = wb.Worksheets[0];

            // Step 2: Insert Smart Marker tags that will be replaced with sheet names
            ws.Cells[0, 0].PutValue("${Orders.MasterSheetName}");
            ws.Cells[1, 0].PutValue("${Orders.DetailSheetName}");

            // Step 3: Prepare the JSON data that contains the master‑detail information
            string jsonOrders = @"{
                ""Orders"": [
                    {
                        ""OrderId"": 1,
                        ""MasterSheetName"": ""Master_1"",
                        ""DetailSheetName"": ""Detail_1""
                    },
                    {
                        ""OrderId"": 2,
                        ""MasterSheetName"": ""Master_2"",
                        ""DetailSheetName"": ""Detail_2""
                    }
                ]
            }";

            // Step 4: Initialise the SmartMarkerProcessor with the workbook
            SmartMarkerProcessor sm = new SmartMarkerProcessor(wb);

            // Step 5: Define how new detail sheets should be named during processing
            sm.Options.DetailSheetNewName = "Detail_${OrderId}";

            // (Optional) Remove the original template sheet after processing
            // sm.Options.RemoveTemplateSheets = true;

            // Step 6: Apply the JSON data to populate the smart markers and generate sheets
            sm.ApplyJson(jsonOrders);

            // Save the result
            wb.Save("output.xlsx");
            Console.WriteLine("Workbook generated successfully. Check output.xlsx.");
        }
    }
}
```

Τρέξτε το πρόγραμμα, ανοίξτε το `output.xlsx` και θα δείτε τα δυναμικά φύλλα ακριβώς όπως περιγράφηκε παραπάνω.

---

## Συμπεράσματα

Μόλις καλύψαμε **πώς να χρησιμοποιήσετε markers** στο Aspose.Cells για να μετατρέψετε ένα απλό βιβλίο εργασίας σε μια λύση master‑detail με **dynamic sheet naming excel**. Τα βασικά σημεία είναι:

1. Τοποθετήστε smart markers `${...}` όπου θέλετε να εμφανιστούν τα δεδομένα.  
2. Παρέχετε JSON (ή οποιαδήποτε υποστηριζόμενη πηγή δεδομένων) στο `SmartMarkerProcessor`.  
3. Χρησιμοποιήστε `DetailSheetNewName` για να επιτρέψετε στον επεξεργαστή να ονομάζει νέα φύλλα δυναμικά.  

Από εδώ μπορείτε να εξερευνήσετε πιο προχωρημένα σενάρια—πρόσθεση πινάκων, μορφοποίηση κελιών, ή ακόμη και ενσωμάτωση γραφημάτων—όλα καθοδηγούμενα από τα markers.

## Σχετικά Tutorials

- [Πώς να Εφαρμόσετε τα Aspose.Cells Smart Markers σε C# για Δυναμική Αναφορά Excel](/cells/english/net/automation-batch-processing/implement-aspose-cells-smart-markers-with-csharp/)
- [Δημιουργία Δυναμικών Αναφορών Excel Χρησιμοποιώντας Aspose.Cells .NET Smart Markers](/cells/english/net/templates-reporting/generate-excel-reports-aspose-cells-net-smart-markers/)
- [Κατάκτηση Aspose.Cells .NET: Εφαρμογή Smart Markers και Προσαρμοσμένων Ετικετών για Δυναμικές Αναφορές Excel](/cells/english/net/advanced-features/aspose-cells-net-smart-markers-custom-labels/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}