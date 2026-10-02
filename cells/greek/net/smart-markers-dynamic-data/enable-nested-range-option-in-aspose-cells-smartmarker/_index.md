---
category: general
date: 2026-06-05
description: Ενεργοποιήστε την επιλογή ένθετης περιοχής στο Aspose.Cells SmartMarkerProcessor
  για να διαχειρίζεστε ιεραρχικά δεδομένα Excel χωρίς κόπο. Μάθετε για τα smart markers,
  τις ένθετες περιοχές και τις βέλτιστες πρακτικές.
draft: false
keywords:
- enable nested range option
- SmartMarkerProcessor
- nested range handling
- Excel smart markers
- Aspose.Cells
language: el
og_description: Ενεργοποιήστε την επιλογή ένθετης περιοχής στο Aspose.Cells SmartMarkerProcessor
  για εργασία με ιεραρχικά δεδομένα. Πλήρης οδηγός με κώδικα, συμβουλές και πιθανά
  προβλήματα.
og_title: Ενεργοποίηση επιλογής ένθετης περιοχής στο Aspose.Cells SmartMarker
schemas:
- author: Aspose
  dateModified: '2026-06-05'
  description: Enable nested range option in Aspose.Cells SmartMarkerProcessor to
    handle hierarchical Excel data effortlessly. Learn smart markers, nested ranges,
    and best practices.
  headline: Enable Nested Range Option in Aspose.Cells SmartMarker
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
- Smart Markers
title: Ενεργοποίηση της επιλογής ένθετου εύρους στο Aspose.Cells SmartMarker
url: /el/net/smart-markers-dynamic-data/enable-nested-range-option-in-aspose-cells-smartmarker/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ενεργοποίηση της επιλογής Nested Range στο Aspose.Cells SmartMarker

Σας έχει ποτέ αναρωτηθεί πώς να **ενεργοποιήσετε την επιλογή nested range** στο Aspose.Cells SmartMarkerProcessor; Η ενεργοποίηση αυτής της δυνατότητας σας επιτρέπει να εργάζεστε με ιεραρχικά δεδομένα όπως παραγγελίες και στοιχεία γραμμής χωρίς προβλήματα.  

Σε αυτό το tutorial θα περάσουμε από ένα πραγματικό σενάριο: τροφοδοτώντας μια λίστα παραγγελιών με ενσωματωμένα στοιχεία σε ένα πρότυπο Excel χρησιμοποιώντας smart markers. Στο τέλος θα έχετε ένα πλήρως λειτουργικό βιβλίο εργασίας, θα κατανοήσετε το **SmartMarkerProcessor** και θα γνωρίζετε γιατί το **nested range handling** flag είναι σημαντικό.

Θα καλύψουμε:

* Προετοιμασία ενός ανώνυμου αντικειμένου C# που μιμείται δεδομένα master‑detail.  
* Ενεργοποίηση της σημαίας **nested range** στον επεξεργαστή.  
* Εκτέλεση του επεξεργαστή σε ένα βιβλίο εργασίας και επαλήθευση του αποτελέσματος.  

Δεν απαιτούνται περίπλοκα frameworks—μόνο .NET 6+ και η βιβλιοθήκη Aspose.Cells for .NET. Αν έχετε αντιμετωπίσει ποτέ προβλήματα με επαναλαμβανόμενες γραμμές μέσα σε επαναλαμβανόμενες γραμμές, αυτός ο οδηγός είναι για εσάς.

---

## Προετοιμασία Ιεραρχικών Δεδομένων για Excel Smart Markers

Πρώτα, χρειάζεται μια πηγή δεδομένων που να αντικατοπτρίζει σχέση γονέα‑παιδιού. Το παρακάτω παράδειγμα δημιουργεί ένα ανώνυμο αντικείμενο με μία παραγγελία που περιέχει δύο στοιχεία.

```csharp
// Step 1: Define hierarchical data with orders and their items
var orderData = new
{
    Orders = new[]
    {
        new
        {
            Id = 1,
            Items = new[]
            {
                new { Name = "A" },
                new { Name = "B" }
            }
        }
    }
};
```

**Γιατί αυτή η δομή;**  
Οι smart markers διαβάζουν τα ονόματα των ιδιοτήτων (`Orders`, `Items`) και αυτόματα δημιουργούν ενσωματωμένα ranges όταν ο επεξεργαστής είναι σωστά ρυθμισμένος. Σκεφτείτε το ως μια μικρή βάση δεδομένων που το πρότυπο Excel θα διατρέξει.

> **Pro tip:** Χρησιμοποιήστε περιγραφικά ονόματα ιδιοτήτων που ταιριάζουν με τις ετικέτες που τοποθετήσατε στο πρότυπο (π.χ. `&=Orders.Id&`, `&=Items.Name&`). Τα μη ταιριαστά ονόματα είναι κοινή πηγή σφαλμάτων «δεν υπάρχουν δεδομένα».

---

## Διαμόρφωση SmartMarkerProcessor και Ενεργοποίηση Nested Range

Τώρα δημιουργούμε τον επεξεργαστή και ενεργοποιούμε το **NestedRange**. Αυτή η εντολή λέει στο Aspose.Cells να αντιμετωπίζει τις συλλογές παιδιών ως εσωτερικούς πίνακες.

```csharp
// Step 2: Create a SmartMarkerProcessor and enable nested range handling
SmartMarkerProcessor processor = new SmartMarkerProcessor();
processor.Options.NestedRange = true;   // <‑‑ enable nested range option
```

**Τι κάνει πραγματικά το `NestedRange = true`;**  
Όταν είναι ενεργό, ο επεξεργαστής δημιουργεί ξεχωριστό range για κάθε συλλογή παιδιού και το ενσωματώνει μέσα στο γονικό range. Χωρίς αυτό, θα εμφανιζόταν μόνο η συλλογή ανώτερου επιπέδου (`Orders`) και οι εσωτερικές γραμμές `Items` θα αγνοούνταν.

> **Watch out:** Αν ενεργοποιήσετε τα nested ranges αλλά ξεχάσετε να σημειώσετε το παιδικό range στο πρότυπο (χρησιμοποιώντας `&=Items.Start&` / `&=Items.End&`), ο επεξεργαστής θα πετάξει ένα `SmartMarkerException`. Ελέγξτε πάντα τη σύνταξη των ετικετών.

---

## Φόρτωση ή Δημιουργία του Προτύπου Workbook

Για τη demo θα δημιουργήσουμε ένα απλό workbook εν κινήσει, αλλά στην παραγωγή συνήθως ξεκινάτε από ένα υπάρχον αρχείο `.xlsx` που ήδη περιέχει smart markers.

```csharp
// Step 3: Create a workbook with a simple template
Workbook wb = new Workbook();
Worksheet ws = wb.Worksheets[0];

// Header row
ws.Cells["A1"].PutValue("Order ID");
ws.Cells["B1"].PutValue("Item Name");

// Smart marker row for Orders (parent)
//   &amp;=Orders.Start&amp; and &amp;=Orders.End&amp; define the range for each order.
ws.Cells["A2"].PutValue("&=Orders.Start&");
ws.Cells["A2"].PutValue("&=Orders.Id&");
ws.Cells["B2"].PutValue("&=Orders.End&");

// Smart marker row for Items (child)
//   Nested inside the Orders range.
ws.Cells["A3"].PutValue("&=Items.Start&");
ws.Cells["A3"].PutValue("&=Items.Name&");
ws.Cells["B3"].PutValue("&=Items.End&");
```

Παρατηρήστε τις ετικέτες `&=Orders.Start&` / `&=Orders.End&`—αυτές λένε στον επεξεργαστή πού αρχίζει και πού τελειώνει κάθε μπλοκ παραγγελίας. Το ίδιο μοτίβο ισχύει για το παιδικό range `Items`.

---

## Επεξεργασία Workbook με Smart Markers

Με τα δεδομένα και τον επεξεργαστή έτοιμους, το τελικό βήμα είναι μια γραμμή κώδικα που συγχωνεύει τα πάντα.

```csharp
// Step 4: Apply the data to the workbook using smart markers
processor.Process(wb, orderData);
```

Μετά από αυτή την κλήση, το workbook θα περιέχει:

| Αριθμός Παραγγελίας | Όνομα Είδους |
|---------------------|--------------|
| 1                   | A            |
| 1                   | B            |

Μπορείτε να αποθηκεύσετε το αποτέλεσμα στο δίσκο ή να το μεταφέρετε σε έναν πελάτη:

```csharp
wb.Save("NestedRangeResult.xlsx");
```

---

## Επαλήθευση Αποτελέσματος και Αντιμετώπιση Συνηθισμένων Προβλημάτων

### Αναμενόμενο Αποτέλεσμα

Ανοίξτε το `NestedRangeResult.xlsx` και θα δείτε δύο γραμμές κάτω από την ενιαία κεφαλίδα παραγγελίας, κάθε γραμμή να εμφανίζει το όνομα του στοιχείου (`A` και `B`). Το ID της παραγγελίας επαναλαμβάνεται για κάθε παιδική γραμμή—ακριβώς αυτό που σχεδιάζονται τα nested ranges.

### Συνηθισμένα Προβλήματα

| Σύμπτωμα | Πιθανή Αιτία | Διόρθωση |
|----------|--------------|----------|
| Δεν εμφανίζονται γραμμές παιδιού | `NestedRange` έμεινε ως `false` | Ορίστε `processor.Options.NestedRange = true`. |
| Οι ετικέτες εμφανίζονται ως απλό κείμενο | Λάθος σύνταξη ετικέτας (`&=Orders.Start&` vs `&=Orders.Start`) | Βεβαιωθείτε ότι υπάρχουν και τα `&=` και το τελικό `&`. |
| Διπλότυπες γραμμές για κάθε παραγγελία | Λείπει η ετικέτα `&=Orders.End&` | Προσθέστε την κλείσιμο ετικέτα για να ορίσετε το εύρος του γονέα. |

---

## Πλήρες Παράδειγμα Εργασίας (Έτοιμο για Αντιγραφή‑Επικόλληση)

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Define hierarchical data
        var orderData = new
        {
            Orders = new[]
            {
                new
                {
                    Id = 1,
                    Items = new[]
                    {
                        new { Name = "A" },
                        new { Name = "B" }
                    }
                }
            }
        };

        // 2️⃣ Create processor and enable nested range option
        SmartMarkerProcessor processor = new SmartMarkerProcessor();
        processor.Options.NestedRange = true;   // enable nested range option

        // 3️⃣ Build a simple workbook template with smart markers
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];

        ws.Cells["A1"].PutValue("Order ID");
        ws.Cells["B1"].PutValue("Item Name");

        // Parent range markers
        ws.Cells["A2"].PutValue("&=Orders.Start&");
        ws.Cells["A2"].PutValue("&=Orders.Id&");
        ws.Cells["B2"].PutValue("&=Orders.End&");

        // Child range markers (nested)
        ws.Cells["A3"].PutValue("&=Items.Start&");
        ws.Cells["A3"].PutValue("&=Items.Name&");
        ws.Cells["B3"].PutValue("&=Items.End&");

        // 4️⃣ Process the workbook
        processor.Process(wb, orderData);

        // 5️⃣ Save the result
        wb.Save("NestedRangeResult.xlsx");
        Console.WriteLine("Workbook generated – check NestedRangeResult.xlsx");
    }
}
```

Τρέξτε το πρόγραμμα, ανοίξτε το παραγόμενο αρχείο και θα δείτε τις ενσωματωμένες γραμμές να έχουν γεμίσει ακριβώς όπως φαίνεται στον παραπάνω πίνακα.

---

## Συμπέρασμα

Μόλις μάθατε πώς να **ενεργοποιήσετε την επιλογή nested range** στο Aspose.Cells SmartMarkerProcessor, μετατρέποντας ένα επίπεδο πρότυπο Excel σε έναν ισχυρό δημιουργό master‑detail αναφορών. Με την εναλλαγή `processor.Options.NestedRange = true`, η βιβλιοθήκη δημιουργεί αυτόματα εσωτερικούς πίνακες για συλλογές παιδιών, εξοικονομώντας σας χρόνο από χειροκίνητες βρόχους εισαγωγής γραμμών.

Τι ακολουθεί; Δοκιμάστε να προσθέσετε ένα δεύτερο επίπεδο ενσωμάτωσης (π.χ. παραγγελία → στοιχεία → υπο‑συστατικά), πειραματιστείτε με το στυλ των παραγόμενων γραμμών, ή μεταβείτε σε ένα προ‑σχεδιασμένο πρότυπο που περιλαμβάνει γραφήματα και τύπους. Ο συνδυασμός **Excel smart markers** και **nested range handling** αποτελεί μια σταθερή βάση για οποιαδήποτε αυτοματοποιημένη λύση αναφορών.

Έχετε ερωτήσεις ή ένα δύσκολο σενάριο; Αφήστε ένα σχόλιο παρακάτω, και καλή προγραμματιστική!

## Τι Πρέπει Να Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Διαχείριση Στοιχείων με Ενσωματωμένα Αντικείμενα με Smart Markers Aspose.Cells](/cells/english/net/smart-markers-dynamic-data/nested-objects-smart-markers/)
- [Γέμισμα Excel με Ενσωματωμένα Δεδομένα Χρησιμοποιώντας Aspose.Cells για Java: Ένας Πλήρης Οδηγός](/cells/english/java/data-manipulation/populate-excel-nested-data-aspose-cells-java/)
- [Γέμισμα Excel Ενσωματωμένων Δεδομένων Aspose Cells Java](/cells/german/java/data-manipulation/populate-excel-nested-data-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}