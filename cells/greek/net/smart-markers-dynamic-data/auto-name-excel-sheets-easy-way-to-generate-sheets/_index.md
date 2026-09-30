---
category: general
date: 2026-02-23
description: Αυτόματη ονομασία φύλλων Excel και μάθετε πώς να δημιουργείτε φύλλα αυτόματα
  χρησιμοποιώντας SmartMarkers. Οδηγός βήμα‑βήμα σε C# για δυναμικά βιβλία εργασίας.
draft: false
keywords:
- auto name excel sheets
- how to generate sheets
- Aspose.Cells SmartMarkers
- dynamic worksheet naming
- C# Excel automation
language: el
og_description: Αυτόματη ονομασία φύλλων Excel άμεσα. Μάθετε πώς να δημιουργείτε φύλλα
  με SmartMarkers σε C# – πλήρες, εκτελέσιμο παράδειγμα.
og_title: Αυτόματη ονομασία φύλλων Excel – Γρήγορο σεμινάριο C#
tags:
- C#
- Excel
- Aspose.Cells
title: Αυτόματη ονομασία φύλλων Excel – Εύκολος τρόπος δημιουργίας φύλλων
url: /el/net/smart-markers-dynamic-data/auto-name-excel-sheets-easy-way-to-generate-sheets/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Αυτόματη Ονομασία Φύλλων Excel – Πλήρες Tutorial C#

Έχετε αναρωτηθεί ποτέ πώς να **αυτόματα ονομάζετε φύλλα excel** χωρίς να γράψετε έναν βρόχο που μετονομάζει χειροκίνητα κάθε καρτέλα; Δεν είστε οι μόνοι. Σε πολλά έργα αναφορών ο αριθμός των φύλλων αυξάνεται κατά το χρόνο εκτέλεσης, και η διατήρηση των ονομάτων σε τάξη γίνεται πρόβλημα. Τα καλά νέα; Με το **SmartMarkers** του Aspose.Cells μπορείτε να αφήσετε τη βιβλιοθήκη να διαχειριστεί την ονομασία για εσάς, και ακόμη σας επιτρέπει **πώς να δημιουργείτε φύλλα** δυναμικά.

Σε αυτόν τον οδηγό θα περάσουμε από ένα πραγματικό σενάριο: δημιουργία βιβλίου εργασίας, ρύθμιση των επιλογών SmartMarker ώστε τα φύλλα λεπτομερειών να ονομάζονται αυτόματα *Detail*, *Detail1*, *Detail2*, …, και στη συνέχεια επαλήθευση ότι τα φύλλα εμφανίζονται όπως αναμένεται. Στο τέλος θα έχετε μια αυτόνομη, έτοιμη για αντιγραφή‑επικόλληση λύση που μπορείτε να προσαρμόσετε σε οποιοδήποτε έργο χρειάζεται δυναμική δημιουργία φύλλων.

---

## Τι Θα Χρειαστείτε

Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε:

- **.NET 6+** (ή .NET Framework 4.6.2+). Ο κώδικας λειτουργεί σε οποιοδήποτε πρόσφατο runtime.
- **Aspose.Cells for .NET** πακέτο NuGet – `Install-Package Aspose.Cells`.
- Ένα βασικό έργο C# (Console App, WinForms ή ASP.NET – ο ίδιος κώδικας λειτουργεί παντού).
- Visual Studio, VS Code ή το αγαπημένο σας IDE.

Καμία πρόσθετη διασύνδεση Excel, κανένα COM, μόνο καθαρός διαχειριζόμενος κώδικας.

---

## Βήμα 1: Αυτόματη Ονομασία Φύλλων Excel με SmartMarkers

Το πρώτο που πρέπει να κάνετε είναι να πείτε στο Aspose.Cells ποιο βασικό όνομα θέλετε για τα αυτόματα δημιουργημένα φύλλα λεπτομερειών. Αυτό γίνεται μέσω της κλάσης `SmartMarkerOptions`.

```csharp
using Aspose.Cells;
using Aspose.Cells.Tables;   // for SmartMarkers
using System;

class Program
{
    static void Main()
    {
        // Create a new workbook that will hold the master sheet.
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];
        ws.Name = "Master";

        // -----------------------------------------------------------
        // Step 1: Configure SmartMarker options – set the base name
        // -----------------------------------------------------------
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
        {
            // This tells SmartMarkers to create sheets named Detail, Detail1, Detail2, …
            DetailSheetNewName = "Detail"
        };
```

**Γιατί είναι σημαντικό:** Ορίζοντας το `DetailSheetNewName`, παραδίδετε τη λογική ονομασίας στη βιβλιοθήκη. Δεν χρειάζεται να γράψετε έναν βρόχο `for` που ελέγχει τα υπάρχοντα ονόματα φύλλων και αυξάνει έναν μετρητή – το API το κάνει για εσάς, εξασφαλίζοντας μοναδικά ονόματα ακόμη και όταν η πηγή δεδομένων περιέχει δεκάδες γραμμές.

---

## Βήμα 2: Προετοιμασία της Πηγής Δεδομένων

Τα SmartMarkers λειτουργούν με οποιαδήποτε συλλογή `IEnumerable`, ένα `DataTable`, ή ακόμη και μια απλή λίστα αντικειμένων. Για αυτή τη demo θα χρησιμοποιήσουμε μια απλή λίστα αντικειμένων που αντιπροσωπεύουν λεπτομέρειες παραγγελίας.

```csharp
        // -----------------------------------------------------------
        // Step 2: Build a sample data source
        // -----------------------------------------------------------
        var orders = new[]
        {
            new { OrderId = 1001, Product = "Laptop", Qty = 2, Price = 1200.00 },
            new { OrderId = 1002, Product = "Mouse",   Qty = 5, Price =  25.99 },
            new { OrderId = 1003, Product = "Keyboard",Qty = 3, Price =  45.50 }
        };
```

**Γιατί είναι σημαντικό:** Η πηγή δεδομένων καθορίζει πόσα φύλλα λεπτομερειών θα δημιουργηθούν. Κάθε στοιχείο στη συλλογή δημιουργεί ένα νέο φύλλο βάσει του προτύπου SmartMarker που θα προσθέσουμε στη συνέχεια.

---

## Βήμα 3: Εισαγωγή Προτύπου SmartMarker στο Κύριο Φύλλο

Ένα πρότυπο SmartMarker είναι απλώς ένα κελί (ή περιοχή) που περιέχει placeholders. Όταν εκτελείται η μέθοδος `Apply`, τα placeholders αντικαθίστανται με πραγματικά δεδομένα, και για κάθε γραμμή δημιουργείται ένα νέο φύλλο.

```csharp
        // -----------------------------------------------------------
        // Step 3: Add a SmartMarker template to the master sheet
        // -----------------------------------------------------------
        // Put a header row
        ws.Cells["A1"].PutValue("Order ID");
        ws.Cells["B1"].PutValue("Product");
        ws.Cells["C1"].PutValue("Quantity");
        ws.Cells["D1"].PutValue("Unit Price");

        // Insert SmartMarker placeholders starting at row 2
        ws.Cells["A2"].PutValue("&=orders.OrderId");
        ws.Cells["B2"].PutValue("&=orders.Product");
        ws.Cells["C2"].PutValue("&=orders.Qty");
        ws.Cells["D2"].PutValue("&=orders.Price");
```

**Γιατί είναι σημαντικό:** Η σύνταξη `&=` λέει στα SmartMarkers «πάρε την τιμή από την πηγή δεδομένων». Όταν τρέξει το `Apply`, το Aspose.Cells θα αντιγράψει αυτή τη γραμμή σε νέο φύλλο για κάθε στοιχείο στο `orders`, ονομάζοντας αυτόματα το φύλλο βάσει της επιλογής που ορίσαμε νωρίτερα.

---

## Βήμα 4: Εφαρμογή Επιλογών SmartMarker – Εδώ Γίνονται τα Φύλλα Αυτόματα Ονομασμένα

Τώρα έρχεται η στιγμή που η βιβλιοθήκη κάνει το σκληρό έργο. Η κλήση `Apply` διαβάζει το πρότυπο, δημιουργεί τα φύλλα λεπτομερειών και τα ονομάζει σύμφωνα με το `DetailSheetNewName`.

```csharp
        // -----------------------------------------------------------
        // Step 4: Apply SmartMarker – auto name excel sheets happens here
        // -----------------------------------------------------------
        ws.SmartMarkers.Apply(smartMarkerOptions, new { orders });

        // Save the workbook to verify the result
        wb.Save("AutoNamedSheets.xlsx");
        Console.WriteLine("Workbook saved. Open AutoNamedSheets.xlsx to see the result.");
    }
}
```

**Γιατί είναι σημαντικό:** Η μέθοδος `Apply` όχι μόνο γεμίζει τα δεδομένα αλλά και σέβεται το μοτίβο ονομασίας που δώσατε. Αν ανοίξετε το *AutoNamedSheets.xlsx* θα δείτε:

- **Detail** – περιέχει την πρώτη παραγγελία.
- **Detail1** – δεύτερη παραγγελία.
- **Detail2** – τρίτη παραγγελία.

Καμία χειροκίνητη μετονομασία δεν απαιτείται.

---

## Βήμα 5: Επαλήθευση του Αποτελέσματος – Πώς να Δημιουργήσετε Φύλλα Σωστά

Αφού τρέξετε το πρόγραμμα, ανοίξτε το παραγόμενο αρχείο. Θα πρέπει να δείτε τρία νέα φύλλα εργασίας ονομασμένα ακριβώς όπως περιγράφηκαν παραπάνω. Αυτό αποδεικνύει ότι έχετε μάθει **πώς να δημιουργείτε φύλλα** αυτόματα.

> **Συμβουλή:** Αν χρειάζεστε προσαρμοσμένο επίθημα (π.χ. “_Report”), απλώς ορίστε `DetailSheetNewName = "Detail_Report"` και η βιβλιοθήκη θα προσθέσει αριθμούς μετά το βασικό κείμενο.

---

## Ακραίες Περιπτώσεις & Συχνές Ερωτήσεις

### Τι γίνεται αν το βασικό όνομα υπάρχει ήδη;

Το Aspose.Cells ελέγχει για υπάρχοντα ονόματα φύλλων και προσθέτει έναν αυξανόμενο αριθμό μέχρι να βρει ένα μοναδικό όνομα. Έτσι, ακόμη και αν υπάρχει ήδη ένα φύλλο με όνομα *Detail*, το επόμενο δημιουργημένο φύλλο θα γίνει *Detail1*.

### Μπορώ να ελέγξω τη σειρά των παραγόμενων φύλλων;

Ναι. Η σειρά ακολουθεί τη σειρά της πηγής δεδομένων. Αν χρειάζεστε συγκεκριμένη σειρά, ταξινομήστε τη συλλογή πριν τη περάσετε στο `Apply`.

### Είναι δυνατόν να δημιουργήσω φύλλα σε διαφορετικό βιβλίο εργασίας;

Απολύτως. Δημιουργήστε ένα δεύτερο αντικείμενο `Workbook`, προσθέστε ένα φύλλο placeholder και καλέστε `Apply` σε αυτό το φύλλο. Η ίδια λογική ονομασίας εφαρμόζεται.

### Πώς λειτουργεί αυτό με μεγάλα σύνολα δεδομένων;

Τα SmartMarkers είναι βελτιστοποιημένα για απόδοση. Ακόμη και με χιλιάδες γραμμές, η βιβλιοθήκη ρέει τα δεδομένα αποδοτικά. Απλώς βεβαιωθείτε ότι έχετε αρκετή μνήμη για το τελικό μέγεθος του βιβλίου εργασίας.

---

## Πλήρες Παράδειγμα Εργασίας (Έτοιμο για Αντιγραφή‑Επικόλληση)

Παρακάτω είναι το πλήρες πρόγραμμα που μπορείτε να ενσωματώσετε σε ένα νέο console project. Δεν λείπουν μέρη – όλα από τις οδηγίες `using` μέχρι την τελική κλήση `Save` περιλαμβάνονται.

```csharp
using Aspose.Cells;
using Aspose.Cells.Tables;
using System;

class AutoNameExcelSheetsDemo
{
    static void Main()
    {
        // 1️⃣ Create workbook and master worksheet
        Workbook workbook = new Workbook();
        Worksheet master = workbook.Worksheets[0];
        master.Name = "Master";

        // 2️⃣ Set up SmartMarker options – this is the key to auto‑naming
        SmartMarkerOptions options = new SmartMarkerOptions
        {
            DetailSheetNewName = "Detail"   // base name for generated sheets
        };

        // 3️⃣ Sample data source – each element will become a new sheet
        var orders = new[]
        {
            new { OrderId = 1001, Product = "Laptop",   Qty = 2, Price = 1200.00 },
            new { OrderId = 1002, Product = "Mouse",    Qty = 5, Price =  25.99 },
            new { OrderId = 1003, Product = "Keyboard", Qty = 3, Price =  45.50 }
        };

        // 4️⃣ Build a simple template on the master sheet
        master.Cells["A1"].PutValue("Order ID");
        master.Cells["B1"].PutValue("Product");
        master.Cells["C1"].PutValue("Quantity");
        master.Cells["D1"].PutValue("Unit Price");

        master.Cells["A2"].PutValue("&=orders.OrderId");
        master.Cells["B2"].PutValue("&=orders.Product");
        master.Cells["C2"].PutValue("&=orders.Qty");
        master.Cells["D2"].PutValue("&=orders.Price");

        // 5️⃣ Apply SmartMarkers – this auto‑creates and auto‑names the sheets
        master.SmartMarkers.Apply(options, new { orders });

        // 6️⃣ Save and inform the user
        workbook.Save("AutoNamedSheets.xlsx");
        Console.WriteLine("Done! Open AutoNamedSheets.xlsx – you’ll see Detail, Detail1, Detail2 …");
    }
}
```

Τρέξτε το πρόγραμμα, ανοίξτε το παραγόμενο *AutoNamedSheets.xlsx* και θα δείτε τη λειτουργία **αυτόματης ονομασίας φύλλων excel** σε δράση.

---

## Συχνές Ερωτήσεις Μετά το Tutorial

- **Μπορώ να το χρησιμοποιήσω με υπάρχον αρχείο προτύπου;**  
  Ναι. Φορτώστε το βιβλίο εργασίας με `new Workbook("Template.xlsx")` και κατευθύνετε το `master` στο φύλλο που περιέχει τα placeholders SmartMarker.

- **Τι γίνεται αν χρειάζομαι διαφορετικές συμβάσεις ονομασίας ανά τύπο φύλλου;**  
  Δημιουργήστε πολλαπλά αντικείμενα `SmartMarkerOptions`, το καθένα με το δικό του `DetailSheetNewName`, και εφαρμόστε τα σε διαφορετικά κύρια φύλλα.

- **Υπάρχει τρόπος να αποκρύψω το βασικό φύλλο (αυτό που περιέχει το πρότυπο);**  
  Μετά το `Apply`, μπορείτε απλώς να διαγράψετε το κύριο φύλλο: `workbook.Worksheets.RemoveAt(0);` – τα φύλλα λεπτομερειών παραμένουν ανέπαφα.

---

## Συμπέρασμα

Τώρα ξέρετε **πώς να αυτόματα ονομάζετε φύλλα excel** χρησιμοποιώντας τα SmartMarkers του Aspose.Cells, και έχετε δει ένα στιβαρό μοτίβο για **πώς να δημιουργείτε φύλλα** δυναμικά σε C#. Η βασική ιδέα είναι απλή: ρυθμίστε το `SmartMarkerOptions.DetailSheetNewName`, δώστε μια συλλογή, και αφήστε τη βιβλιοθήκη να κάνει το υπόλοιπο. Αυτή η προσέγγιση εξαλείφει τους επαναλαμβανόμενους βρόχους, εγγυάται μοναδικά ονόματα και κλιμακώνεται άψογα.

Έτοιμοι για το επόμενο βήμα; Δοκιμάστε να αντικαταστήσετε την πηγή δεδομένων με ένα `Data

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}