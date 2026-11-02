---
category: general
date: 2026-06-27
description: Διαγραφή πολλαπλών γραμμών σε Word χρησιμοποιώντας C#. Μάθετε πώς να
  διαγράφετε γραμμές πίνακα, να αφαιρείτε γραμμές πίνακα και να επεξεργάζεστε πίνακες
  εγγράφων Word αποδοτικά.
draft: false
keywords:
- delete multiple rows word
- how to delete table rows
- how to remove table rows
- delete rows from word table
- word document table editing
language: el
og_description: Διαγράψτε πολλαπλές σειρές στο Word άμεσα. Αυτό το σεμινάριο δείχνει
  πώς να διαγράψετε σειρές πίνακα, να αφαιρέσετε σειρές από έναν πίνακα στο Word και
  να κυριαρχήσετε στην επεξεργασία πινάκων εγγράφων Word.
og_title: Διαγραφή Πολλαπλών Γραμμών στο Word – Βήμα‑βήμα Επεξεργασία Πίνακα
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Delete multiple rows word using C#. Learn how to delete table rows,
    remove table rows and edit Word document tables efficiently.
  headline: Delete Multiple Rows Word – Complete Guide to Removing Table Rows
  type: TechArticle
tags:
- Aspose.Words
- C#
- Word Automation
title: Διαγραφή Πολλαπλών Γραμμών στο Word – Πλήρης Οδηγός για την Αφαίρεση Γραμμών
  Πίνακα
url: /el/net/tables-and-lists/delete-multiple-rows-word-complete-guide-to-removing-table-r/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Διαγραφή Πολλαπλών Γραμμών Word – Πλήρης Οδηγός για την Αφαίρεση Γραμμών Πίνακα

Έχετε χρειαστεί ποτέ να **διαγράψετε πολλαπλές γραμμές word** σε έγγραφα αλλά δεν ήξερες ποια κλήση API να χρησιμοποιήσεις; Δεν είστε μόνοι—πολλοί προγραμματιστές αντιμετωπίζουν το ίδιο πρόβλημα όταν προσπαθούν να μειώσουν έναν πίνακα διατηρώντας το κεφαλίδα άθικτη.  

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από μια σύντομη, ολοκληρωμένη λύση που δείχνει *πώς να διαγράψετε γραμμές πίνακα* προγραμματιστικά, *πώς να αφαιρέσετε γραμμές πίνακα* με ασφάλεια, και γιατί η προσέγγιση λειτουργεί για κάθε σενάριο **διαγραφής γραμμών από πίνακα word** που μπορεί να συναντήσετε.

Στο τέλος θα έχετε ένα επαναχρησιμοποιήσιμο snippet που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο C#, καθώς και μερικές συμβουλές για ευρύτερες εργασίες **επεξεργασίας πινάκων σε έγγραφα word**.

## Προαπαιτούμενα

- .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί επίσης σε .NET Framework 4.6+)
- Aspose.Words for .NET εγκατεστημένο (`dotnet add package Aspose.Words`)
- Βασική κατανόηση της σύνταξης C#
- Ένα αρχείο `.docx` που περιέχει τουλάχιστον έναν πίνακα με γραμμή κεφαλίδας

> **Pro tip:** Αν δεν έχετε ακόμη άδεια, το Aspose.Words προσφέρει δωρεάν λειτουργία αξιολόγησης που είναι ιδανική για δοκιμές.

## Βήμα 1: Ρύθμιση του Έργου και Φόρτωση του Εγγράφου Word

Πρώτα απ' όλα—δημιουργήστε μια εφαρμογή console (ή ενσωματώστε το σε υπάρχουσα υπηρεσία) και προσθέστε τις απαραίτητες δηλώσεις `using`. Στη συνέχεια φορτώστε το πηγαίο έγγραφο.

```csharp
using System;
using Aspose.Words;
using Aspose.Words.Tables;

class Program
{
    static void Main()
    {
        // Load the Word document (replace YOUR_DIRECTORY with your actual path)
        Document doc = new Document(@"YOUR_DIRECTORY\input.docx");
        Console.WriteLine("Document loaded successfully.");
```

**Γιατί είναι σημαντικό:**  
`Document` είναι το σημείο εισόδου για κάθε λειτουργία του Aspose.Words. Η φόρτωση του αρχείου μία φορά μειώνει τη χρήση μνήμης και σας δίνει ένα χειριστήριο για όλες τις επόμενες κλήσεις επεξεργασίας πίνακα.

## Βήμα 2: Εντοπισμός του Πρώτου Πίνακα (ή οποιουδήποτε Πίνακα Χρειάζεστε)

Αν το έγγραφό σας περιέχει πολλούς πίνακες, μπορείτε να επιλέξετε αυτόν που θέλετε με βάση το δείκτη ή με αναζήτηση λέξης‑κλειδί. Για απλότητα, θα πάρουμε τον πρώτο πίνακα, που συνήθως περιέχει τα δεδομένα που θέλουμε να μειώσουμε.

```csharp
        // Retrieve the first table in the document
        Table firstTable = doc.GetChild(NodeType.Table, 0, true) as Table;
        if (firstTable == null)
        {
            Console.WriteLine("No table found in the document.");
            return;
        }
        Console.WriteLine($"Table with {firstTable.Rows.Count} rows found.");
```

**Εξήγηση:**  
`GetChild(NodeType.Table, 0, true)` διασχίζει το δέντρο του εγγράφου βάθος‑πρώτο και επιστρέφει τον πρώτο κόμβο `Table` που συναντά. Η μετατροπή `as Table` μετατρέπει με ασφάλεια τον κόμβο, επιτρέποντάς μας να δουλέψουμε με `Rows` αργότερα.

## Βήμα 3: Διαγραφή Πολλαπλών Γραμμών Διατηρώντας την Κεφαλίδα

Τώρα φτάνουμε στην ουσία: **delete multiple rows word** documents. Ας υποθέσουμε ότι η κεφαλίδα βρίσκεται στη γραμμή 0 και θέλετε να αφαιρέσετε τις επόμενες δύο γραμμές (δείκτες 1 και 2). Η μέθοδος `DeleteRows` κάνει ακριβώς αυτό.

```csharp
        // Delete two rows starting from the second row (index 1)
        // This keeps the header row untouched while removing the following rows
        firstTable?.DeleteRows(1, 2);
        Console.WriteLine("Specified rows deleted.");
```

### Πώς να Διαγράψετε Γραμμές Πίνακα – Παραλλαγές

- **Διαγραφή μιας μόνο γραμμής:** `firstTable?.DeleteRows(rowIndex, 1);`
- **Διαγραφή όλων των γραμμών εκτός της κεφαλίδας:** `firstTable?.DeleteRows(1, firstTable.Rows.Count - 1);`
- **Διαγραφή γραμμών βάσει συνθήκης:** επαναλάβετε μέσω `firstTable.Rows` και καλέστε `DeleteRows` όταν ένα κελί ταιριάζει με τα κριτήριά σας.

Αυτά τα snippets απαντούν στην κοινή ερώτηση **πώς να αφαιρέσετε γραμμές πίνακα** με ευέλικτο τρόπο.

## Βήμα 4: Αποθήκευση του Τροποποιημένου Εγγράφου

Αφού οι γραμμές έχουν αφαιρεθεί, απλώς γράψτε το έγγραφο πίσω στο δίσκο. Μπορείτε να αντικαταστήσετε το αρχικό αρχείο ή να δημιουργήσετε ένα νέο αντίγραφο.

```csharp
        // Save the modified document
        doc.Save(@"YOUR_DIRECTORY\output.docx");
        Console.WriteLine("Document saved as output.docx");
    }
}
```

**Τι θα δείτε:**  
Αν ο αρχικός πίνακας είχε, για παράδειγμα, πέντε γραμμές (κεφαλίδα + τέσσερις γραμμές δεδομένων), το αποθηκευμένο `output.docx` θα περιέχει τώρα μόνο τρεις γραμμές (κεφαλίδα + τις δύο υπόλοιπες γραμμές δεδομένων). Ανοίξτε το αρχείο στο Word για να επαληθεύσετε ότι οι ανεπιθύμητες γραμμές εξαφανίστηκαν χωρίς να επηρεαστεί άλλο περιεχόμενο.

![delete multiple rows word example](delete-multiple-rows-word.png)

*Κείμενο alt εικόνας: διαγραφή πολλαπλών γραμμών word – στιγμιότυπο πριν και μετά ενός πίνακα Word.*

## Πλήρες, Έτοιμο‑για‑Εκτέλεση Παράδειγμα

Συνδυάζοντας όλα τα παραπάνω, εδώ είναι το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε‑και‑επικολλήσετε:

```csharp
using System;
using Aspose.Words;
using Aspose.Words.Tables;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the Word document
        Document doc = new Document(@"YOUR_DIRECTORY\input.docx");
        Console.WriteLine("Document loaded.");

        // 2️⃣ Retrieve the first table
        Table firstTable = doc.GetChild(NodeType.Table, 0, true) as Table;
        if (firstTable == null)
        {
            Console.WriteLine("No table found.");
            return;
        }
        Console.WriteLine($"Found table with {firstTable.Rows.Count} rows.");

        // 3️⃣ Delete rows – this is the core of delete rows from word table
        //    Starting at index 1 (second row), delete the next two rows.
        firstTable?.DeleteRows(1, 2);
        Console.WriteLine("Rows deleted.");

        // 4️⃣ Save the result
        doc.Save(@"YOUR_DIRECTORY\output.docx");
        Console.WriteLine("Saved output.docx");
    }
}
```

Τρέξτε το πρόγραμμα, ανοίξτε το `output.docx`, και θα δείτε ότι η κεφαλίδα παραμένει ενώ οι επιλεγμένες γραμμές έχουν εξαφανιστεί. Αυτό είναι **delete multiple rows word** σε δράση.

## Συνηθισμένα Προβλήματα & Πώς να τα Αποφύγετε

| Πρόβλημα | Γιατί Συμβαίνει | Διόρθωση |
|----------|----------------|----------|
| **NullReferenceException** όταν `firstTable` είναι `null` | Το έγγραφο δεν έχει πίνακες ή ο δείκτης είναι λανθασμένος | Πάντα ελέγχετε `firstTable != null` πριν καλέσετε `DeleteRows`. |
| **Οι γραμμές δεν διαγράφονται** | Χρήση λανθασμένου αρχικού δείκτη (οι πίνακες Word είναι μηδενικής βάσης) | Θυμηθείτε ότι η κεφαλίδα είναι γραμμή 0· ξεκινήστε από 1 για να τη διατηρήσετε. |
| **Αποθήκευση πάνω σε αρχείο μόνο για ανάγνωση** | Τα δικαιώματα αρχείου εμποδίζουν την αντικατάσταση | Αποθηκεύστε σε διαφορετική διαδρομή ή τροποποιήστε τα χαρακτηριστικά του αρχείου. |
| **Απρόσμενες αλλαγές διάταξης** | Διαγραφή γραμμών που περιέχουν συγχωνευμένα κελιά μπορεί να καταστρέψει τον πίνακα | Βεβαιωθείτε ότι τα συγχωνευμένα κελιά έχουν διαχειριστεί—αποσυγχωνεύστε πρώτα ή διαγράψτε ολόκληρες γραμμές προσεκτικά. |

## Επέκταση της Λύσης – Περισσότερη Επεξεργασία Πινάκων σε Έγγραφα Word

Αν σας ενδιαφέρει η ευρύτερη **word document table editing**, σκεφτείτε τα επόμενα βήματα:

- **Εισαγωγή νέων γραμμών**: `firstTable?.Rows.Add(new Row(doc));`
- **Ενημέρωση κειμένου κελιού**: `firstTable.Rows[rowIndex].Cells[colIndex].Paragraphs[0].AppendText("New value");`
- **Εφαρμογή στυλ**: Χρησιμοποιήστε `CellFormat` ή `RowFormat` για να ορίσετε σκίαση, περιγράμματα ή ιδιότητες γραμματοσειράς.
- **Εξαγωγή σε PDF**: `doc.Save("output.pdf", SaveFormat.Pdf);`

Όλες αυτές οι λειτουργίες βασίζονται στο ίδιο μοντέλο αντικειμένων που χρησιμοποιήσαμε για τη διαγραφή γραμμών, διατηρώντας τον κώδικά σας συνεπή.

## Συμπέρασμα

Σας δείξαμε πώς να **delete multiple rows word** documents με λίγες γραμμές κώδικα C#. Η προσέγγιση καλύπτει *πώς να διαγράψετε γραμμές πίνακα*, *πώς να αφαιρέσετε γραμμές πίνακα*, και το ευρύτερο θέμα της **word document table editing**.  

Τώρα έχετε ένα σταθερό, επαναχρησιμοποιήσιμο μοτίβο: φορτώστε το έγγραφο, εντοπίστε τον πίνακα, καλέστε `DeleteRows` με τους σωστούς δείκτες, και αποθηκεύστε. Από εδώ μπορείτε να προσαρμόσετε το εύρος γραμμών, να κάνετε βρόχο σε πολλούς πίνακες, ή να συνδυάσετε με άλλες λειτουργίες επεξεργασίας για οποιοδήποτε έργο αυτοματοποίησης.

Έτοιμοι για το επόμενο βήμα; Δοκιμάστε να αυτοματοποιήσετε τη δημιουργία τιμολογίων, να καθαρίσετε πρότυπα αναφορών, ή να χτίσετε ένα εργαλείο μαζικής ενημέρωσης που επεξεργάζεται δεκάδες αρχεία Word ταυτόχρονα. Ο ουρανός είναι το όριο, και το API το κάνει αβίαστο.

Αν αντιμετωπίσετε δυσκολίες, αφήστε ένα σχόλιο παρακάτω—καλή προγραμματιστική!

## Τι Πρέπει να Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κυριαρχήσετε επιπλέον δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στα δικά σας έργα.

- [Πώς να Εισάγετε και Διαγράψετε Γραμμές σε Excel με Aspose.Cells for .NET: Ένας Πλήρης Οδηγός](/cells/english/net/data-manipulation/aspose-cells-net-insert-delete-excel-rows/)
- [Διαγραφή Πολλαπλών Γραμμών σε Excel με Aspose.Cells .NET: Ένας Πλήρης Οδηγός για τη Διαχείριση Δεδομένων](/cells/english/net/data-manipulation/delete-rows-excel-aspose-cells-net/)
- [Διαγραφή Πολλαπλών Γραμμών σε Aspose.Cells .NET](/cells/english/net/row-and-column-management/delete-multiple-rows-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}