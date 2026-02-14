---
category: general
date: 2026-02-14
description: 'Αυτοματοποιήστε τη δημιουργία τιμολογίων με το SmartMarker: μάθετε πώς
  να επαναλαμβάνετε φύλλα εργασίας, να τα ονομάζετε δυναμικά και να κατακτήσετε τη
  δυναμική ονομασία φύλλων εργασίας σε λίγα λεπτά.'
draft: false
keywords:
- automate invoice generation
- how to name worksheets
- how to repeat worksheet
- dynamic worksheet naming
language: el
og_description: Αυτοματοποιήστε τη δημιουργία τιμολογίων με το SmartMarker. Αυτός
  ο οδηγός δείχνει πώς να επαναλάβετε φύλλα εργασίας, να τα ονομάσετε δυναμικά και
  να κυριαρχήσετε στη δυναμική ονομασία φύλλων εργασίας.
og_title: Αυτοματοποιήστε τη Δημιουργία Τιμολογίων – Δυναμική Ονομασία Φύλλων Εργασίας
  & Επανάληψη
tags:
- C#
- SmartMarker
- Excel Automation
title: Αυτοματοποιήστε τη δημιουργία τιμολογίων – Δυναμική ονομασία φύλλων εργασίας
  & επανάληψη σε C#
url: /el/net/smart-markers-dynamic-data/automate-invoice-generation-dynamic-worksheet-naming-repeati/
---

translate each paragraph.

Will produce Greek text.

Will keep code block placeholders.

Let's write final answer.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Αυτοματοποιήστε τη Δημιουργία Τιμολογίων – Δυναμική Ονομασία Φύλλων Εργασίας & Επανάληψη σε C#

Έχετε αναρωτηθεί ποτέ πώς να **αυτοματοποιήσετε τη δημιουργία τιμολογίων** χωρίς να αντιγράφετε χειροκίνητα φύλλα για κάθε παραγγελία; Δεν είστε μόνοι. Πολλοί προγραμματιστές συναντούν πρόβλημα όταν χρειάζονται ξεχωριστό φύλλο εργασίας ανά τιμολόγιο, αλλά θέλουν επίσης το όνομα του φύλλου να αντανακλά τον αριθμό παραγγελίας. Σε αυτό το tutorial θα λύσουμε το πρόβλημα χρησιμοποιώντας το `SmartMarkerProcessor` του SmartMarker και θα σας δείξουμε **πώς να ονομάζετε δυναμικά τα φύλλα εργασίας**, καλύπτοντας επίσης **πώς να επαναλάβετε το φύλλο εργασίας** για κάθε εγγραφή. Στο τέλος θα έχετε ένα έτοιμο δείγμα C# που παράγει ένα βιβλίο εργασίας όπου κάθε τιμολόγιο βρίσκεται σε δικό του, όμορφα ονομασμένο καρτέλα.

Θα περάσουμε από κάθε βήμα—από την ανάκτηση παραγγελιών από πηγή δεδομένων μέχρι τη διαμόρφωση του `SmartMarkerOptions` για δυναμική ονομασία φύλλων εργασίας. Δεν απαιτούνται εξωτερικά έγγραφα· όλα όσα χρειάζεστε είναι εδώ. Μια μικρή προαπαιτούμενη γνώση του C# και μια αναφορά στη βιβλιοθήκη Aspose.Cells (ή οποιοδήποτε κινητήρα συμβατό με SmartMarker) αρκούν.

---

## Τι Θα Δημιουργήσετε

- Ανάκτηση συλλογής αντικειμένων παραγγελίας.
- Διαμόρφωση του SmartMarker για **επανάληψη ενός φύλλου εργασίας** για κάθε παραγγελία.
- Εφαρμογή **δυναμικής ονομασίας φύλλων εργασίας** χρησιμοποιώντας το placeholder `{OrderId}`.
- Δημιουργία αρχείου Excel όπου κάθε καρτέλα ονομάζεται `Invoice_12345`, `Invoice_67890`, κ.λπ.
- Επαλήθευση του αποτελέσματος ανοίγοντας το βιβλίο εργασίας.

---

## Προαπαιτούμενα

- .NET 6.0 ή νεότερο (ο κώδικας μεταγλωττίζεται και με .NET 5+).
- Aspose.Cells for .NET (ή οποιαδήποτε βιβλιοθήκη που υλοποιεί SmartMarker). Εγκατάσταση μέσω NuGet:

```bash
dotnet add package Aspose.Cells
```

- Μια βασική κλάση `Order` (μπορείτε να την αντικαταστήσετε με το δικό σας DTO).

---

## Βήμα 1: Ρύθμιση του Έργου και του Μοντέλου

Πρώτα, δημιουργήστε μια νέα εφαρμογή console και ορίστε το μοντέλο δεδομένων που αντιπροσωπεύει μια παραγγελία.

```csharp
using System;
using System.Collections.Generic;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace InvoiceAutomation
{
    // Simple POCO representing an order – replace fields as needed
    public class Order
    {
        public int OrderId { get; set; }
        public string Customer { get; set; }
        public DateTime Date { get; set; }
        public decimal Total { get; set; }
    }

    class Program
    {
        static void Main()
        {
            // Retrieve orders (in real life this could be a DB call)
            var orders = GetOrders();

            // The rest of the tutorial continues here...
        }

        // Mock method – in production pull from EF Core, Dapper, etc.
        private static List<Order> GetOrders()
        {
            return new List<Order>
            {
                new Order { OrderId = 1001, Customer = "Acme Corp", Date = DateTime.Today, Total = 1234.56m },
                new Order { OrderId = 1002, Customer = "Beta Ltd.", Date = DateTime.Today.AddDays(-1), Total = 789.00m },
                new Order { OrderId = 1003, Customer = "Gamma LLC", Date = DateTime.Today.AddDays(-2), Total = 456.78m }
            };
        }
    }
}
```

> **Συμβουλή:** Κρατήστε το μοντέλο ελαφρύ για το demo· μπορείτε πάντα να το εμπλουτίσετε αργότερα με στοιχεία γραμμής, λεπτομέρειες φόρου κ.λπ.

---

## Βήμα 2: Προετοιμασία του Προτύπου Excel

Το SmartMarker λειτουργεί πάνω σε ένα πρότυπο βιβλίο εργασίας. Δημιουργήστε ένα αρχείο με όνομα `InvoiceTemplate.xlsx` που περιέχει ένα φύλλο εργασίας με όνομα `InvoiceTemplate`. Στο κελί **A1** τοποθετήστε ένα placeholder SmartMarker όπως:

```
{{OrderId}} – {{Customer}} – {{Date}} – ${{Total}}
```

Μπορείτε να μορφοποιήσετε τα κελιά όπως θέλετε—έντονα κεφαλίδες, μορφοποίηση νομίσματος κ.λπ. Αποθηκεύστε το αρχείο στον ριζικό φάκελο του έργου.

> **Γιατί ένα πρότυπο;** Διαχωρίζει τη διάταξη από τον κώδικα, επιτρέποντας στους σχεδιαστές να τροποποιούν την εμφάνιση χωρίς να αγγίζουν τη λογική.

---

## Βήμα 3: Διαμόρφωση SmartMarker Options – Επανάληψη & Ονομασία Φύλλων

Τώρα θα πούμε στο SmartMarker να *επαναλάβει* το πρότυπο φύλλο εργασίας για κάθε παραγγελία και να δώσει σε κάθε αντίγραφο ένα όνομα που περιλαμβάνει το ID της παραγγελίας. Αυτό αποτελεί τον πυρήνα της **δυναμικής ονομασίας φύλλων εργασίας**.

```csharp
// Inside Main() after retrieving orders
// Load the template workbook
Workbook wb = new Workbook("InvoiceTemplate.xlsx");

// Set up SmartMarker options
var smartMarkerOptions = new SmartMarkerOptions
{
    // Instructs SmartMarker to create a new worksheet per data item
    RepeatWorksheet = true,

    // Naming pattern – {OrderId} will be replaced with the actual value
    RepeatWorksheetName = "Invoice_{OrderId}"
};

// Run the processor
wb.SmartMarkerProcessor.StartSmartMarkerProcessing(orders, smartMarkerOptions);

// Save the result
string outputPath = "GeneratedInvoices.xlsx";
wb.Save(outputPath);

Console.WriteLine($"✅ Invoices generated: {outputPath}");
```

### Πώς Λειτουργεί

- **`RepeatWorksheet = true`** λέει στη μηχανή να αντιγράψει το πηγαίο φύλλο για κάθε στοιχείο στη συλλογή `orders`. Αυτό ικανοποιεί την απαίτηση **πώς να επαναλάβετε το φύλλο εργασίας**.
- **`RepeatWorksheetName = "Invoice_{OrderId}"`** είναι μια συμβολοσειρά προτύπου όπου το `{OrderId}` είναι placeholder που το SmartMarker αντικαθιστά με το τρέχον ID παραγγελίας. Αυτό είναι η απάντηση στο **πώς να ονομάζετε φύλλα εργασίας** και στην **δυναμική ονομασία φύλλων εργασίας**.
- Ο επεξεργαστής ενσωματώνει τα πεδία κάθε παραγγελίας (`{{OrderId}}`, `{{Customer}}`, κ.λπ.) στο αντιγραφόμενο φύλλο, παράγοντας ένα πλήρως συμπληρωμένο τιμολόγιο.

---

## Βήμα 4: Εκτέλεση της Εφαρμογής και Επαλήθευση του Αποτελέσματος

Μεταγλωττίστε και τρέξτε την εφαρμογή console:

```bash
dotnet run
```

Θα πρέπει να δείτε το μήνυμα επιτυχίας στην κονσόλα. Ανοίξτε το `GeneratedInvoices.xlsx` και θα βρείτε τρεις καρτέλες:

- **Invoice_1001**
- **Invoice_1002**
- **Invoice_1003**

Κάθε φύλλο περιέχει τα δεδομένα της παραγγελίας που έχουν αντικαταστήσει τα placeholders. Η διάταξη που σχεδιάσατε στο πρότυπο διατηρείται, αποδεικνύοντας ότι η **αυτοματοποιημένη δημιουργία τιμολογίων** λειτουργεί από άκρη σε άκρη.

### Αναμενόμενη Στιγμιότυπο (alt text για SEO)

![παράδειγμα αυτοματοποιημένης δημιουργίας τιμολογίων που δείχνει τρία δυναμικά ονομασμένα φύλλα εργασίας](/images/invoice-automation.png)

> *Το κείμενο alt περιλαμβάνει τη βασική λέξη-κλειδί για να ικανοποιήσει το SEO.*

---

## Βήμα 5: Ακραίες Περιπτώσεις & Συνηθισμένες Παραλλαγές

### Τι γίνεται αν το OrderId περιέχει μη επιτρεπτούς χαρακτήρες;

Τα ονόματα φύλλων Excel δεν μπορούν να περιέχουν `\ / ? * [ ] :`. Αν τα IDs σας μπορεί να περιέχουν τέτοιους χαρακτήρες, κάντε καθαρισμό:

```csharp
RepeatWorksheetName = "Invoice_{SanitizedOrderId}"
```

Προσθέστε μια υπολογιζόμενη ιδιότητα στην κλάση `Order`:

```csharp
public string SanitizedOrderId => OrderId.ToString().Replace("/", "-").Replace("\\", "-");
```

### Θέλετε να διατηρήσετε το αρχικό φύλλο προτύπου;

Ορίστε `smartMarkerOptions.RemoveTemplate = false;` (η προεπιλογή είναι `true`). Αυτό αφήνει το αρχικό `InvoiceTemplate` ανέπαφο ως αναφορά.

### Θέλετε να ομαδοποιήσετε τα τιμολόγια ανά πελάτη;

Μπορείτε να ενσωματώσετε **ομάδες επανάληψης**. Πρώτα επαναλάβετε ανά πελάτη, μετά ανά παραγγελίες μέσα σε κάθε φύλλο πελάτη. Η σύνταξη γίνεται λίγο πιο πολύπλοκη, αλλά η αρχή παραμένει η ίδια—χρησιμοποιήστε `RepeatWorksheet` και ένα μοτίβο ονομασίας που αντικατοπτρίζει την ιεραρχία.

---

## Πλήρες Παράδειγμα Λειτουργίας (Όλος ο Κώδικας σε Ένα Σημείο)

```csharp
using System;
using System.Collections.Generic;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace InvoiceAutomation
{
    public class Order
    {
        public int OrderId { get; set; }
        public string Customer { get; set; }
        public DateTime Date { get; set; }
        public decimal Total { get; set; }

        // Helper for safe sheet names
        public string SanitizedOrderId => OrderId.ToString();
    }

    class Program
    {
        static void Main()
        {
            var orders = GetOrders();

            // Load template
            Workbook wb = new Workbook("InvoiceTemplate.xlsx");

            // Configure SmartMarker for repeating and naming worksheets
            var smartMarkerOptions = new SmartMarkerOptions
            {
                RepeatWorksheet = true,
                RepeatWorksheetName = "Invoice_{OrderId}" // dynamic worksheet naming
                // RemoveTemplate = true; // default behavior
            };

            // Process the data
            wb.SmartMarkerProcessor.StartSmartMarkerProcessing(orders, smartMarkerOptions);

            // Save the final workbook
            string outputPath = "GeneratedInvoices.xlsx";
            wb.Save(outputPath);

            Console.WriteLine($"✅ Invoices generated: {outputPath}");
        }

        private static List<Order> GetOrders()
        {
            return new List<Order>
            {
                new Order { OrderId = 1001, Customer = "Acme Corp", Date = DateTime.Today, Total = 1234.56m },
                new Order { OrderId = 1002, Customer = "Beta Ltd.", Date = DateTime.Today.AddDays(-1), Total = 789.00m },
                new Order { OrderId = 1003, Customer = "Gamma LLC", Date = DateTime.Today.AddDays(-2), Total = 456.78m }
            };
        }
    }
}
```

Αντιγράψτε‑και‑επικολλήστε αυτό στο `Program.cs`, τοποθετήστε το `InvoiceTemplate.xlsx` δίπλα του, και είστε έτοιμοι.

---

## Συχνές Ερωτήσεις

**Ε: Λειτουργεί αυτή η προσέγγιση με μεγάλα σύνολα δεδομένων (χίλιες τιμολόγια);**  
Α: Ναι. Το SmartMarker μεταδίδει τα δεδομένα αποδοτικά, αλλά παρακολουθήστε τη χρήση μνήμης. Αν φτάσετε τα όρια, σκεφτείτε επεξεργασία σε παρτίδες και εγγραφή κάθε παρτίδας σε ξεχωριστό βιβλίο εργασίας.

**Ε: Μπορώ να προσθέσω λογότυπο σε κάθε τιμολόγιο αυτόματα;**  
Α: Απόλυτα. Τοποθετήστε την εικόνα λογότυπου στο φύλλο προτύπου. Εφόσον το φύλλο αντιγράφεται, το λογότυπο εμφανίζεται σε κάθε παραγόμενο τιμολόγιο χωρίς επιπλέον κώδικα.

**Ε: Τι γίνεται αν χρειαστεί να προστατεύσω τα φύλλα εργασίας;**  
Α: Μετά την επεξεργασία, διασχίστε το `wb.Worksheets` και καλέστε `ws.Protect(Password, ProtectionType.All)`.

---

## Συμπέρασμα

Μόλις **αυτοματοποιήσαμε τη δημιουργία τιμολογίων** αξιοποιώντας τη δυνατότητα επανάληψης φύλλων του SmartMarker και ένα έξυπνο μοτίβο ονομασίας. Το tutorial κάλυψε **πώς να ονομάζετε φύλλα εργασίας**, έδειξε **πώς να επαναλάβετε το φύλλο εργασίας** για κάθε παραγγελία, και παρουσίασε **δυναμική ονομασία φύλλων εργασίας** που διατηρεί το βιβλίο εργασίας σας τακτοποιημένο και εύκολα αναζητήσιμο.  

Από την ανάκτηση δεδομένων, τη δημιουργία προτύπου, τη διαμόρφωση του `SmartMarkerOptions`, μέχρι τη διαχείριση ακραίων περιπτώσεων, έχετε τώρα μια πλήρη, εκτελέσιμη λύση. Στο επόμενο βήμα, δοκιμάστε να προσθέσετε πίνακες γραμμών, να εφαρμόσετε μορφοποίηση υπό όρους, ή να εξάγετε τα ίδια δεδομένα σε PDF για μια πλήρως αυτοματοποιημένη διαδικασία τιμολόγησης.

Έτοιμοι για επόμενα βήματα; Εξερευνήστε συναφή θέματα όπως “μαζική εξαγωγή Excel με Aspose.Cells”, “μετατροπή φύλλων εργασίας σε PDF”, ή “αποστολή παραγόμενων τιμολογίων μέσω email απευθείας από C#”. Ο ουρανός είναι το όριο—καλή προγραμματιστική!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}