---
category: general
date: 2026-06-08
description: Διαγράψτε γραμμές πίνακα Word χρησιμοποιώντας το Aspose.Words. Μάθετε
  πώς να διαγράφετε γραμμές, να διαγράφετε πολλαπλές γραμμές σε Word και να κυριαρχήσετε
  στην επεξεργασία πινάκων σε λίγα λεπτά.
draft: false
keywords:
- delete rows word table
- how to delete rows
- delete multiple rows word
language: el
og_description: Διαγραφή γραμμών πίνακα Word με το Aspose.Words. Αυτό το σεμινάριο
  δείχνει πώς να διαγράψετε γραμμές, να διαγράψετε πολλαπλές γραμμές σε Word και να
  διατηρήσετε τους πίνακές σας τακτικούς.
og_title: Διαγραφή γραμμών πίνακα Word – Πλήρης Οδηγός C#
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Delete rows word table using Aspose.Words. Learn how to delete rows,
    delete multiple rows word, and master table editing in minutes.
  headline: Delete rows word table – Complete C# Guide
  type: TechArticle
- description: Delete rows word table using Aspose.Words. Learn how to delete rows,
    delete multiple rows word, and master table editing in minutes.
  name: Delete rows word table – Complete C# Guide
  steps:
  - name: 3.1 How to delete rows (single row)
    text: 'To remove a single row, call `DeleteRows(startIndex, count)` where `startIndex`
      is zero‑based. Skipping the header row (index 0) is common:'
  - name: 3.2 Delete multiple rows word – batch removal
    text: 'When you need to drop a range—say rows 2‑6—you pass the start index and
      the number of rows to erase. This is the **delete multiple rows word** pattern:'
  - name: Expected output
    text: '- `output.docx` contains the original table **without** rows 2‑6. - All
      remaining rows shift up, preserving cell formatting and column widths. - The
      header row stays intact, keeping your column titles visible.'
  type: HowTo
- questions:
  - answer: Absolutely. Loop through `table.Rows`, inspect `row.Cells[i].GetText()`,
      and collect matching indices. Then call `DeleteRows` with the smallest index
      and total count, or delete rows in reverse order to avoid re‑indexing.
    question: Can I delete rows based on cell content instead of index?
  - answer: Yes. Aspose.Words supports both `.doc` and `.docx`. Just change the file
      extension in the `Document` constructor and `Save` call.
    question: Does this work with .doc files?
  - answer: 'Retrieve it via `doc.FirstSection.HeadersFooters` collection, then apply
      the same `DeleteRows` logic. ## Conclusion You now have a solid, end‑to‑end
      solution for **delete rows word table** using C#. The example shows *how to
      delete rows* individually and how to **delete multiple rows word** in a sin'
    question: What if the table is inside a header/footer?
  type: FAQPage
tags:
- C#
- Aspose.Words
- Word automation
title: Διαγραφή γραμμών πίνακα Word – Πλήρης οδηγός C#
url: /el/net/tables-and-lists/delete-rows-word-table-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Διαγραφή γραμμών πίνακα Word – Πλήρης Οδηγός C#

Έχετε ποτέ χρειαστεί να **delete rows word table** αλλά δεν ήξερατε από πού να ξεκινήσετε; Δεν είστε μόνοι· πολλοί προγραμματιστές αντιμετωπίζουν αυτό το πρόβλημα όταν καθαρίζουν δημιουργημένες αναφορές ή περικοπούν πίνακες που βασίζονται σε δεδομένα. Τα καλά νέα; Με λίγες γραμμές C# και Aspose.Words μπορείτε εύκολα να αφαιρέσετε ανεπιθύμητες γραμμές, είτε είναι μία μόνο γραμμή είτε μια δέσμη από αυτές. Σε αυτόν τον οδηγό θα περάσουμε από *how to delete rows* και θα καλύψουμε ακόμη και την πιο δύσκολη περίπτωση του **delete multiple rows word** σε μία ενέργεια.

Θα καλύψουμε όλα όσα χρειάζεστε: τον ακριβή κώδικα, γιατί κάθε βήμα είναι σημαντικό, κοινά λάθη και ένα έτοιμο‑για‑εκτέλεση παράδειγμα. Στο τέλος θα μπορείτε να αφαιρέσετε γραμμές από οποιονδήποτε πίνακα Word χωρίς να διασπάτε τη δομή του εγγράφου. Χωρίς περιττές πληροφορίες, μόνο πρακτικές, δοκιμασμένες τεχνικές.

## Προαπαιτούμενα

- **Aspose.Words for .NET** (έκδοση 23.12 ή νεότερη). Μπορείτε να το αποκτήσετε από το NuGet: `Install-Package Aspose.Words`.
- Ένα περιβάλλον ανάπτυξης .NET (Visual Studio, Rider ή VS Code με την επέκταση C#).
- Ένα αρχείο Word εισόδου (`input.docx`) που περιέχει τουλάχιστον έναν πίνακα με γραμμή κεφαλίδας.

Αυτό είναι όλο—χωρίς πρόσθετες βιβλιοθήκες, χωρίς COM interop, μόνο καθαρός διαχειριζόμενος κώδικας.

## Βήμα 1: Φόρτωση του εγγράφου Word

Το πρώτο που κάνετε είναι να ανοίξετε το έγγραφο. Το Aspose.Words αντιμετωπίζει ένα αρχείο Word ως αντικείμενο `Document`, το οποίο σας δίνει πλήρη πρόσβαση σε ενότητες, σώματα, πίνακες και πολλά άλλα.

```csharp
using Aspose.Words;

class TableCleaner
{
    static void Main()
    {
        // Load the source .docx file
        Document doc = new Document(@"YOUR_DIRECTORY\input.docx");
        // Continue with table manipulation…
```

*Γιατί είναι σημαντικό:* Η φόρτωση του εγγράφου δημιουργεί μια αναπαράσταση στη μνήμη, έτσι οι αλλαγές που κάνετε είναι γρήγορες και δεν αγγίζουν το σύστημα αρχείων μέχρι να αποθηκεύσετε ρητά.

## Βήμα 2: Λήψη του στόχου πίνακα

Στις περισσότερες περιπτώσεις γνωρίζετε ποιος πίνακας θέλετε να επεξεργαστείτε—συχνά ο πρώτος. Το Aspose.Words το κάνει τεράστια εύκολο μέσω της ιδιότητας `FirstSection`.

```csharp
        // Access the first table in the first section
        Table table = doc.FirstSection.Body.Tables[0];
```

Αν το έγγραφό σας έχει πολλούς πίνακες, μπορείτε να κάνετε βρόχο στο `doc.GetChildNodes(NodeType.Table, true)` και να επιλέξετε τον σωστό βάσει δείκτη ή προσαρμοσμένου δείκτη.

## Βήμα 3: Διαγραφή γραμμών – μονή ή πολλαπλή

### 3.1 Πώς να διαγράψετε γραμμές (μονή γραμμή)

Για να αφαιρέσετε μία γραμμή, καλέστε `DeleteRows(startIndex, count)` όπου το `startIndex` είναι μηδενικής βάσης. Η παράλειψη της γραμμής κεφαλίδας (δείκτης 0) είναι συνηθισμένη:

```csharp
        // Delete just the second row (index 1)
        table.DeleteRows(1, 1);
```

### 3.2 Delete multiple rows word – μαζική αφαίρεση

Όταν χρειάζεται να αφαιρέσετε μια περιοχή—π.χ. γραμμές 2‑6—περνάτε το αρχικό δείκτη και τον αριθμό των γραμμών προς διαγραφή. Αυτό είναι το πρότυπο **delete multiple rows word**:

```csharp
        // Delete rows 2‑6 (skip header at index 0)
        // startIndex = 1 (second row), count = 5 rows
        table.DeleteRows(1, 5);
```

*Γιατί να χρησιμοποιήσετε μία κλήση;* Η διαγραφή γραμμών μία‑με‑μία αναγκάζει τον πίνακα να επαναδείξει μετά από κάθε αφαίρεση, κάτι που μπορεί να προκαλέσει σφάλματα και να είναι πιο αργό. Η μαζική μέθοδος διατηρεί τη δομή του πίνακα συνεπή.

#### Edge case: Διαγραφή πέρα από το μέγεθος του πίνακα

Αν `startIndex + count` υπερβαίνει τον πραγματικό αριθμό γραμμών, το Aspose.Words ρίχνει `ArgumentOutOfRangeException`. Μια αμυντική προστασία φαίνεται έτσι:

```csharp
        int rowsToDelete = Math.Min(5, table.Rows.Count - 1); // never delete the header
        if (rowsToDelete > 0)
            table.DeleteRows(1, rowsToDelete);
```

Αυτό το απόσπασμα κώδικα εξασφαλίζει ότι δεν θα προσπαθήσετε ποτέ να διαγράψετε περισσότερες γραμμές από όσες υπάρχουν.

## Βήμα 4: Αποθήκευση του τροποποιημένου εγγράφου

Μόλις οι γραμμές αφαιρεθούν, η αποθήκευση των αλλαγών γίνεται με μία γραμμή:

```csharp
        // Save the cleaned document
        doc.Save(@"YOUR_DIRECTORY\output.docx");
    }
}
```

Η μέθοδος `Save` επιλέγει αυτόματα τη μορφή βάσει της επέκτασης του αρχείου, οπότε μπορείτε να εξάγετε σε PDF, HTML ή ακόμη και ODT με διαφορετικό κατάληξη.

## Πλήρες Παράδειγμα Εργασίας

Συνδυάζοντας όλα τα παραπάνω, εδώ είναι το πλήρες, έτοιμο‑για‑εκτέλεση πρόγραμμα:

```csharp
using System;
using Aspose.Words;

class TableCleaner
{
    static void Main()
    {
        // 1️⃣ Load the Word document
        Document doc = new Document(@"YOUR_DIRECTORY\input.docx");

        // 2️⃣ Access the first table (adjust index if needed)
        Table table = doc.FirstSection.Body.Tables[0];

        // 3️⃣ Delete rows 2‑6 (skip header row at index 0)
        //    This demonstrates delete multiple rows word in one call.
        if (table.Rows.Count > 1) // ensure there is at least a header + one data row
        {
            int rowsToDelete = Math.Min(5, table.Rows.Count - 1);
            table.DeleteRows(1, rowsToDelete);
        }

        // 4️⃣ Save the modified document
        doc.Save(@"YOUR_DIRECTORY\output.docx");

        Console.WriteLine("Rows removed successfully. Output saved to output.docx");
    }
}
```

### Αναμενόμενο αποτέλεσμα

- Το `output.docx` περιέχει τον αρχικό πίνακα **χωρίς** τις γραμμές 2‑6.
- Όλες οι υπόλοιπες γραμμές μετατοπίζονται προς τα πάνω, διατηρώντας τη μορφοποίηση των κελιών και το πλάτος των στηλών.
- Η γραμμή κεφαλίδας παραμένει αμετάβλητη, διατηρώντας τους τίτλους των στηλών ορατούς.

## Γιατί αυτή η προσέγγιση ξεπερνά τις εναλλακτικές

| Προσέγγιση | Πλεονεκτήματα | Μειονεκτήματα |
|------------|---------------|---------------|
| **Aspose.Words `DeleteRows`** | Διαγραφή μαζική με μία γραμμή, διατηρεί στυλ, χωρίς εξαρτήσεις COM | Απαιτεί εμπορική βιβλιοθήκη (διατίθεται δωρεάν δοκιμή) |
| Office Interop | Λειτουργεί με το εγγενές Word | Απαιτεί εγκατεστημένο Word στον διακομιστή, αργό, προβλήματα καθαρισμού COM |
| Open XML SDK | Δωρεάν, ανοιχτού κώδικα | Χειροκίνητη διαχείριση XML· η ασφαλής διαγραφή γραμμών είναι επίπονη |

Αν ήδη χρησιμοποιείτε το Aspose.Words για άλλες εργασίες εγγράφων, η παραμονή στο `DeleteRows` διατηρεί τον κώδικά σας καθαρό και συνεπή.

## Pro συμβουλές & κοινά προβλήματα

- **Pro tip:** Κρατήστε πάντα τη γραμμή κεφαλίδας (δείκτης 0) αμετάβλητη, εκτός αν θέλετε πραγματικά να την αφαιρέσετε. Η διαγραφή της κεφαλίδας μπορεί να σπάσει επεξεργασίες που αναμένουν ονόματα στηλών.
- **Προσοχή σε συγχωνευμένα κελιά.** Αν μια γραμμή περιέχει κατακόρυφα συγχωνευμένο κελί που εκτείνεται στη γραμμή που διαγράφετε, το Aspose.Words θα προσαρμόσει αυτόματα το εύρος συγχώνευσης, αλλά ελέγξτε το οπτικό αποτέλεσμα.
- **Σημείωση απόδοσης:** Η διαγραφή πολλών γραμμών από έναν τεράστιο πίνακα (χιλιάδες γραμμές) παραμένει γρήγορη, όμως αν επεξεργάζεστε εκατοντάδες έγγραφα σε βρόχο, σκεφτείτε την επαναχρησιμοποίηση του αντικειμένου `Document` όπου είναι δυνατόν για μείωση του κόστους κατανομής μνήμης.

## Συχνές ερωτήσεις

**Q: Μπορώ να διαγράψω γραμμές βάσει του περιεχομένου των κελιών αντί του δείκτη;**  
A: Απόλυτα. Κάντε βρόχο στο `table.Rows`, ελέγξτε το `row.Cells[i].GetText()`, και συλλέξτε τους δείκτες που ταιριάζουν. Στη συνέχεια καλέστε `DeleteRows` με τον μικρότερο δείκτη και το συνολικό πλήθος, ή διαγράψτε τις γραμμές με αντίστροφη σειρά για να αποφύγετε την επαναδείξη.

**Q: Λειτουργεί αυτό με αρχεία .doc;**  
A: Ναι. Το Aspose.Words υποστηρίζει τόσο `.doc` όσο και `.docx`. Απλώς αλλάξτε την επέκταση του αρχείου στον κατασκευαστή `Document` και στην κλήση `Save`.

**Q: Τι γίνεται αν ο πίνακας βρίσκεται σε κεφαλίδα/υποσέλιδο;**  
A: Ανακτήστε τον μέσω της συλλογής `doc.FirstSection.HeadersFooters`, έπειτα εφαρμόστε την ίδια λογική `DeleteRows`.

## Συμπέρασμα

Τώρα έχετε μια ισχυρή, ολοκληρωμένη λύση για **delete rows word table** χρησιμοποιώντας C#. Το παράδειγμα δείχνει *how to delete rows* μεμονωμένα και πώς να **delete multiple rows word** με μία αποδοτική κλήση. Με το Aspose.Words έχετε ένα καθαρό API, χωρίς προβλήματα COM, και πλήρη έλεγχο πάνω στα έγγραφα Word.

Έτοιμοι για την επόμενη πρόκληση; Δοκιμάστε να προσθέσετε μια νέα γραμμή με υπολογισμένα σύνολα, ή εξάγετε τον περιορισμένο πίνακα σε CSV χρησιμοποιώντας `Table.ToTxt`. Ο ουρανός είναι το όριο όταν κυριαρχείτε στη διαχείριση πινάκων.

Καλή προγραμματιστική, και ας παραμείνουν οι πίνακες Word σας τακτοποιημένοι!

## Τι Θα Πρέπει Να Μάθετε Στη Σύντομη Επόμενη

Οι παρακάτω εκπαιδευτικές οδηγίες καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [How to Delete Rows in Excel Using Aspose.Cells for Java | Guide & Tutorial](/cells/english/java/worksheet-management/delete-row-excel-aspose-cells-java/)
- [How to Delete Blank Rows in Excel Using Aspose.Cells .NET for Data Cleanup](/cells/english/net/data-manipulation/delete-blank-rows-aspose-cells-net/)
- [How to Insert and Delete Rows in Excel with Aspose.Cells for .NET&#58; A Comprehensive Guide](/cells/english/net/data-manipulation/aspose-cells-net-insert-delete-excel-rows/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}