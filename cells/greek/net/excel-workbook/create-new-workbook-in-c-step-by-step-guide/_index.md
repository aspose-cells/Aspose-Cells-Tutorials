---
category: general
date: 2026-02-15
description: Δημιουργήστε νέο βιβλίο εργασίας σε C# και μάθετε πώς να προσθέσετε έναν
  πίνακα, να ενεργοποιήσετε το φίλτρο και να αποθηκεύσετε το βιβλίο εργασίας ως xlsx.
  Γρήγορος, πλήρης οδηγός για αυτοματοποίηση του Excel.
draft: false
keywords:
- create new workbook
- save workbook as xlsx
- how to create workbook
- how to add table
- how to enable filter
language: el
og_description: Δημιουργήστε νέο βιβλίο εργασίας σε C# και αμέσως προσθέστε έναν πίνακα,
  ενεργοποιήστε τα φίλτρα, στη συνέχεια αποθηκεύστε το βιβλίο εργασίας ως xlsx. Ακολουθήστε
  αυτόν τον σύντομο, πρακτικό οδηγό.
og_title: Δημιουργία Νέου Φύλλου Εργασίας σε C# – Πλήρης Οδηγός Προγραμματισμού
tags:
- C#
- Aspose.Cells
- Excel Automation
title: Δημιουργία νέου βιβλίου εργασίας σε C# – Οδηγός βήμα‑προς‑βήμα
url: /el/net/excel-workbook/create-new-workbook-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία Νέου Workbook σε C# – Πλήρης Οδηγός Προγραμματισμού

Έχετε ποτέ χρειαστεί να **create new workbook** σε C# αλλά δεν ήσασταν σίγουροι ποια αντικείμενα να χρησιμοποιήσετε πρώτα; Δεν είστε μόνοι· πολλοί προγραμματιστές αντιμετωπίζουν αυτό το πρόβλημα όταν αυτοματοποιούν αρχεία Excel. Σε αυτό το tutorial θα περάσουμε από τη δημιουργία ενός νέου workbook, την εισαγωγή ενός πίνακα, την ενεργοποίηση/απενεργοποίηση του auto‑filter, και τέλος **save workbook as xlsx**—όλα με σαφή, εκτελέσιμο κώδικα.

Θα απαντήσουμε επίσης στις επίμονες ερωτήσεις “how to add table” και “how to enable filter” που συνήθως εμφανίζονται μετά τη δημιουργία του αρχικού workbook. Στο τέλος, θα έχετε ένα αυτόνομο παράδειγμα που μπορείτε να ενσωματώσετε σε οποιοδήποτε .NET project, χωρίς περιττά πρόσθετα.

## Προαπαιτούμενα & Ρύθμιση

- **.NET 6** (ή οποιαδήποτε πρόσφατη έκδοση .NET) εγκατεστημένο.
- Το **Aspose.Cells for .NET** πακέτο NuGet (`Install-Package Aspose.Cells`) – αυτή η βιβλιοθήκη παρέχει τις κλάσεις `Workbook`, `Worksheet` και `ListObject` που χρησιμοποιούνται παρακάτω.
- Ένα περιβάλλον ανάπτυξης που προτιμάτε (Visual Studio, VS Code, Rider – διαλέξτε το δικό σας).

Δεν απαιτείται καμία επιπλέον ρύθμιση· ο κώδικας εκτελείται αμέσως μόλις γίνει η αναφορά στο πακέτο.

![Screenshot showing a newly created workbook in Excel – create new workbook](image.png)

*Image alt text: “στιγμιότυπο οθόνης δημιουργίας νέου workbook στο Excel”*

## Βήμα 1: Δημιουργία Νέου Workbook και Πρόσβαση στο Πρώτο Worksheet

Το πρώτο πράγμα που πρέπει να κάνετε είναι να δημιουργήσετε ένα αντικείμενο `Workbook`. Σκεφτείτε το ως το άνοιγμα ενός ολοκαίνουργιου αρχείου Excel που αυτή τη στιγμή περιέχει ένα μόνο προεπιλεγμένο φύλλο. Μετά από αυτό, πάρτε μια αναφορά στο worksheet ώστε να μπορείτε να αρχίσετε να το γεμίζετε.

```csharp
using Aspose.Cells;

public class WorkbookDemo
{
    public static void Main()
    {
        // Step 1: Create a new workbook (this is the "create new workbook" part)
        Workbook workbook = new Workbook();

        // Access the first worksheet – by default it is named "Sheet1"
        Worksheet worksheet = workbook.Worksheets[0];
```

**Why this matters:** Η δημιουργία του workbook σας δίνει έναν καθαρό καμβά· η πρόσβαση στο πρώτο worksheet εξασφαλίζει ότι έχετε στόχο για τον επερχόμενο πίνακα. Αν παραλείψετε αυτό το βήμα, τυχόν κλήσεις σε `ListObject` αργότερα θα προκαλέσουν σφάλμα null reference.

## Βήμα 2: Πώς να Προσθέσετε Πίνακα στο Worksheet

Τώρα που έχουμε ένα worksheet, ας εισάγουμε έναν πίνακα που καλύπτει τα κελιά **A1:C5**. Στο Aspose.Cells η συλλογή `ListObjects` διαχειρίζεται τους πίνακες (επίσης γνωστούς ως *list objects*). Η προσθήκη ενός πίνακα είναι μια διαδικασία δύο βημάτων: καλέστε `Add` για να τον δημιουργήσετε, έπειτα τυλίξτε το αποτέλεσμα σε μια μεταβλητή `ListObject` για εύκολη διαχείριση.

```csharp
        // Step 2: Add a table named "MyTable" covering the range A1:C5
        int tableIndex = worksheet.ListObjects.Add("MyTable", "A1:C5", true);
        ListObject table = worksheet.ListObjects[tableIndex];
```

**What’s happening under the hood?** Η μέθοδος `Add` καταχωρεί τον πίνακα στη εσωτερική μηχανή πινάκων του Excel, του αναθέτοντας ένα μοναδικό δείκτη. Αποθηκεύοντας αυτόν τον δείκτη στο `tableIndex` μπορούμε να ανακτήσουμε το πραγματικό αντικείμενο `ListObject`, το οποίο μας δίνει πλήρη έλεγχο στις ιδιότητες του πίνακα.

### Συμβουλή Pro
Αν σκοπεύετε να δημιουργήσετε πολλαπλούς πίνακες, κρατήστε τους δείκτες τους σε μια λίστα – έτσι οι μεταγενέστερες ενημερώσεις γίνονται πολύ πιο εύκολες.

## Βήμα 3: Πώς να Ενεργοποιήσετε το Φίλτρο στον Πίνακα

Οι πίνακες στο Excel έρχονται με μια γραμμή auto‑filter από προεπιλογή, αλλά ανάλογα με το πώς δημιουργήσατε τον πίνακα μπορεί να χρειαστεί να την ενεργοποιήσετε ρητά. Η ιδιότητα `ShowAutoFilter` ενεργοποιεί ή απενεργοποιεί αυτή τη γραμμή.

```csharp
        // Step 3: Enable the auto‑filter for the table
        table.ShowAutoFilter = true;
```

Μόλις ενεργοποιηθεί, οι χρήστες μπορούν να κάνουν κλικ στα βελάκια dropdown στη γραμμή κεφαλίδας για να φιλτράρουν τις γραμμές βάσει τιμών. Αυτό είναι ιδιαίτερα χρήσιμο για μεγάλα σύνολα δεδομένων.

### Τι γίνεται αν δεν θέλετε φίλτρο;
Απλώς ορίστε `ShowAutoFilter` σε `false` και τα βελάκια εξαφανίζονται. Η παρακάτω γραμμή δείχνει την αντίστροφη ενέργεια:

```csharp
        // Disable (remove) the auto‑filter
        table.ShowAutoFilter = false;
```

## Βήμα 4: Αποθήκευση Workbook ως XLSX

Όλη η βαριά δουλειά έχει ολοκληρωθεί· τώρα αποθηκεύουμε το workbook στο δίσκο. Η μέθοδος `Save` δέχεται μια πλήρη διαδρομή και καθορίζει αυτόματα τη μορφή αρχείου από την επέκταση. Εδώ αποθηκεύουμε ρητά **save workbook as xlsx**.

```csharp
        // Step 4: Save the workbook to a file
        string outputPath = @"C:\Temp\NoFilter.xlsx"; // Change to your desired folder
        workbook.Save(outputPath);
    }
}
```

Όταν ανοίξετε το `NoFilter.xlsx` θα δείτε ένα μόνο φύλλο με έναν πίνακα με όνομα **MyTable** που καλύπτει το A1:C5, και—επειδή θέσαμε `ShowAutoFilter` σε `false`—δεν θα εμφανίζονται βελάκια φίλτρου.

### Αναμενόμενο Αποτέλεσμα
- Ένα αρχείο με όνομα `NoFilter.xlsx` τοποθετημένο στον φάκελο που καθορίσατε.
- Το Sheet1 περιέχει έναν πίνακα 5 γραμμών και 3 στηλών με προεπιλεγμένα δεδομένα (κελιά κενά εκτός αν τα γεμίσετε).
- Δεν εμφανίζεται γραμμή auto‑filter.

## Παραλλαγές & Ακραίες Περιπτώσεις

### Διατήρηση του Φίλτρου Ενεργοποιημένου
Αν η περίπτωση χρήσης σας απαιτεί το φίλτρο να παραμείνει ενεργό, απλώς παραλείψτε τη γραμμή που θέτει `ShowAutoFilter = false`. Ο πίνακας θα εμφανιστεί με βελάκια φίλτρου έτοιμα για αλληλεπίδραση χρήστη.

### Προσθήκη Πολλαπλών Πινάκων
Μπορείτε να επαναλάβετε **Step 2** με διαφορετικά εύρη και ονόματα:

```csharp
int secondTableIdx = worksheet.ListObjects.Add("SecondTable", "E1:G10", true);
ListObject secondTable = worksheet.ListObjects[secondTableIdx];
secondTable.ShowAutoFilter = true;
```

### Συμπλήρωση Δεδομένων Πίνακα
Το Aspose.Cells σας επιτρέπει να γράψετε απευθείας στα κελιά πριν ή μετά τη δημιουργία του πίνακα. Για παράδειγμα, για να γεμίσετε την πρώτη στήλη με αριθμούς:

```csharp
for (int i = 0; i < 5; i++)
{
    worksheet.Cells[i, 0].PutValue(i + 1); // A1‑A5 = 1‑5
}
```

### Σημείωση Συμβατότητας
Ο κώδικας λειτουργεί με **Aspose.Cells 23.9** και νεότερες εκδόσεις. Αν χρησιμοποιείτε παλαιότερη έκδοση, η υπογραφή της μεθόδου `Add` μπορεί να διαφέρει ελαφρώς—ελέγξτε τις σημειώσεις έκδοσης της βιβλιοθήκης.

## Συνηθισμένα Πίπτα & Πώς να τα Αποφύγετε

- **Forgot to reference Aspose.Cells** – ο μεταγλωττιστής θα παραπονιστεί για άγνωστους τύπους. Βεβαιωθείτε ότι το πακέτο NuGet είναι εγκατεστημένο και ότι το `using Aspose.Cells;` βρίσκεται στην κορυφή του αρχείου.
- **Incorrect range string** – τα εύρη του Excel δεν είναι ευαίσθητα σε πεζά/κεφαλαία, αλλά πρέπει να είναι έγκυρα (π.χ., `"A1:C5"` όχι `"A1:C"`). Ένα τυπογραφικό λάθος θα προκαλέσει `CellsException`.
- **File path permissions** – η προσπάθεια αποθήκευσης σε προστατευμένο φάκελο (π.χ., `C:\Program Files`) θα προκαλέσει `UnauthorizedAccessException`. Χρησιμοποιήστε έναν φάκελο με δικαιώματα εγγραφής όπως `%TEMP%` ή το προφίλ χρήστη σας.

## Πλήρες Παράδειγμα Εργασίας (Έτοιμο για Αντιγραφή‑Επικόλληση)

```csharp
using Aspose.Cells;

public class WorkbookDemo
{
    public static void Main()
    {
        // 1️⃣ Create new workbook
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Add a table named "MyTable" covering A1:C5
        int tableIdx = worksheet.ListObjects.Add("MyTable", "A1:C5", true);
        ListObject table = worksheet.ListObjects[tableIdx];

        // 3️⃣ Enable auto‑filter (you can skip this if you don't need it)
        table.ShowAutoFilter = true;

        // OPTIONAL: Disable the filter if you don't want it visible
        // table.ShowAutoFilter = false;

        // 4️⃣ Save workbook as xlsx
        string outputPath = @"C:\Temp\NoFilter.xlsx";
        workbook.Save(outputPath);
    }
}
```

Εκτελέστε το πρόγραμμα, ανοίξτε το παραγόμενο αρχείο και θα δείτε το ακριβές αποτέλεσμα που περιγράφηκε παραπάνω.

## Ανακεφαλαίωση

Ξεκινήσαμε με **create new workbook**, έπειτα μάθαμε **how to add table**, ενεργοποιήσαμε τη λειτουργία **how to enable filter**, και τέλος **save workbook as xlsx**. Κάθε βήμα εξηγήθηκε με *γιατί* είναι σημαντικό, όχι μόνο με *τι* πρέπει να γράψετε, ώστε να μπορείτε να προσαρμόσετε το μοτίβο σε πιο σύνθετα σενάρια.

## Τι Ακολουθεί;

- **Style the table** – εξερευνήστε το `TableStyleType` για να δώσετε στα δεδομένα σας επαγγελματική εμφάνιση.
- **Insert formulas** – χρησιμοποιήστε `Cells[i, j].Formula = "=SUM(A2:A5)"` για να προσθέσετε υπολογισμούς.
- **Export to PDF** – το Aspose.Cells μπορεί επίσης να αποδώσει το workbook ως PDF με μια μόνο κλήση στο `Save`.
- **Read existing workbooks** – αντικαταστήστε το `new Workbook()` με `new Workbook("ExistingFile.xlsx")` για να τροποποιήσετε υπάρχοντα αρχεία εν κινήσει.

Μη διστάσετε να πειραματιστείτε με αυτές τις ιδέες και να αφήσετε ένα σχόλιο αν κάτι δεν είναι σαφές. Καλή προγραμματιστική και καλή διασκέδαση με την αυτοματοποίηση του Excel σε C#!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}