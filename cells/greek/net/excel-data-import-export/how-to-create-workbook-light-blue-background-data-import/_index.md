---
category: general
date: 2026-02-09
description: Πώς να δημιουργήσετε βιβλίο εργασίας σε C# με ανοιχτό μπλε φόντο και
  να εισάγετε δεδομένα με κεφαλίδες. Μάθετε πώς να προσθέσετε ανοιχτό μπλε φόντο,
  να χρησιμοποιήσετε το προεπιλεγμένο στυλ του Excel και να εισάγετε DataTable.
draft: false
keywords:
- how to create workbook
- add light blue background
- import data with headers
- excel import datatable c#
- use default style excel
language: el
og_description: Πώς να δημιουργήσετε ένα βιβλίο εργασίας σε C# με ανοιχτό μπλε φόντο,
  να εισάγετε δεδομένα με επικεφαλίδες και να εφαρμόσετε το προεπιλεγμένο στυλ του
  Excel—όλα σε έναν σύντομο οδηγό.
og_title: Πώς να δημιουργήσετε βιβλίο εργασίας – Ανοιχτό μπλε φόντο, εισαγωγή δεδομένων
tags:
- C#
- Excel
- Aspose.Cells
title: Πώς να δημιουργήσετε βιβλίο εργασίας – Ανοιχτό μπλε φόντο, εισαγωγή δεδομένων
url: /el/net/excel-data-import-export/how-to-create-workbook-light-blue-background-data-import/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να δημιουργήσετε ένα Workbook – Φόντο ανοιχτό μπλε, Εισαγωγή δεδομένων

Έχετε αναρωτηθεί ποτέ **πώς να δημιουργήσετε ένα workbook** σε C# που να φαίνεται λίγο πιο ωραίο κατευθείαν από το κουτί; Ίσως έχετε τραβήξει ένα `DataTable` από μια βάση δεδομένων και είστε κουρασμένοι από τα απλά, λευκά κελιά προεπιλογής. Σε αυτό το tutorial θα περάσουμε από τη δημιουργία ενός νέου workbook, την προσθήκη φόντου ανοιχτό μπλε σε μια στήλη, και την εισαγωγή δεδομένων με κεφαλίδες — όλα χρησιμοποιώντας το προεπιλεγμένο στυλ που παρέχει το Excel.

Θα προσθέσουμε επίσης μερικά σενάρια “τι‑αν”, όπως η διαχείριση τιμών null ή η προσαρμογή περισσοτέρων από μία στήλης. Στο τέλος, θα έχετε ένα πλήρως στυλιζαρισμένο αρχείο Excel που μπορείτε να στείλετε σε ενδιαφερόμενους χωρίς καμία επεξεργασία μετά.

## Προαπαιτούμενα

Πριν βουτήξουμε, βεβαιωθείτε ότι έχετε:

* **.NET 6+** (ο κώδικας λειτουργεί επίσης σε .NET Framework 4.6+)  
* **Aspose.Cells for .NET** – η βιβλιοθήκη που τροφοδοτεί τις κλήσεις `Workbook`, `Style` και `ImportDataTable`. Εγκαταστήστε την μέσω NuGet:  

  ```bash
  dotnet add package Aspose.Cells
  ```

* Μια πηγή `DataTable` – θα δημιουργήσουμε ένα ψεύτικο στο παράδειγμα, αλλά μπορείτε να το αντικαταστήσετε με οποιοδήποτε ερώτημα ADO.NET.

Τα έχετε; Τέλεια, ας ξεκινήσουμε.

## Βήμα 1: Αρχικοποίηση ενός νέου Workbook (Primary Keyword)

Το πρώτο που πρέπει να κάνετε είναι **πώς να δημιουργήσετε ένα workbook** – κυριολεκτικά. Η κλάση `Workbook` αντιπροσωπεύει ολόκληρο το αρχείο Excel, και ο κατασκευαστής της σας δίνει ένα καθαρό καμβά.

```csharp
using Aspose.Cells;
using System;
using System.Data;
using System.Drawing;

namespace ExcelStylingDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook (or obtain an existing one)
            Workbook workbook = new Workbook();   // <-- this is how to create workbook
```

> **Γιατί είναι σημαντικό:** Ξεκινώντας με ένα φρέσκο `Workbook` εξασφαλίζετε ότι ελέγχετε κάθε στυλ από την αρχή. Αν ανοίγατε ένα υπάρχον αρχείο, θα κληρονόμιζατε τα στυλ που άφησε ο αρχικός δημιουργός, κάτι που μπορεί να οδηγήσει σε ασυνεπή μορφοποίηση.

## Βήμα 2: Προετοιμασία του DataTable που θα εισάγετε

Για λόγους επεξήγησης, ας δημιουργήσουμε ένα απλό `DataTable`. Σε πραγματικές συνθήκες πιθανότατα θα καλέσετε μια αποθηκευμένη διαδικασία ή μια μέθοδο ORM.

```csharp
            // Step 2: Retrieve the data you want to import (e.g., from a database)
            DataTable dataTable = GetSampleData(); // replace with your own GetData()
```

```csharp
        // Helper method that returns a dummy DataTable
        static DataTable GetSampleData()
        {
            DataTable table = new DataTable("Employees");
            table.Columns.Add("ID", typeof(int));
            table.Columns.Add("Name", typeof(string));
            table.Columns.Add("HireDate", typeof(DateTime));
            table.Columns.Add("Salary", typeof(decimal));

            table.Rows.Add(1, "Alice Johnson", new DateTime(2020, 5, 12), 72000);
            table.Rows.Add(2, "Bob Smith", new DateTime(2019, 3, 4), 68000);
            table.Rows.Add(3, "Carol White", DBNull.Value, 75000); // demonstrates a null value
            return table;
        }
```

> **Συμβουλή:** Αν χρειάζεται να διατηρήσετε τη σειρά των στηλών ακριβώς όπως εμφανίζεται στη βάση δεδομένων, ορίστε την παράμετρο `importColumnNames` του `ImportDataTable` σε `true`. Αυτό λέει στο Aspose.Cells να γράψει τις κεφαλίδες των στηλών για εσάς.

## Βήμα 3: Ορισμός Στυλ Στηλών – Προεπιλογή + Φόντο ανοιχτό μπλε

Τώρα απαντάμε στο **add light blue background** μέρος του γρίφου. Το Aspose.Cells σας επιτρέπει να περάσετε έναν πίνακα αντικειμένων `Style` που αντιστοιχούν σε κάθε στήλη που εισάγετε. Η πρώτη καταχώρηση είναι το στυλ για τη στήλη 0, η δεύτερη για τη στήλη 1, κ.ο.κ. Αν έχετε λιγότερα στυλ από τις στήλες, οι υπόλοιπες στήλες θα επιστρέψουν στο προεπιλεγμένο στυλ.

```csharp
            // Step 3: Define column styles – the default style and a custom style with a light‑blue foreground
            Style defaultStyle = workbook.DefaultStyle; // this is the use default style excel
            Style lightBlueStyle = workbook.CreateStyle();
            lightBlueStyle.ForegroundColor = Color.LightBlue;
            lightBlueStyle.Pattern = BackgroundType.Solid; // make sure the color shows

            // Apply default style to the first column, light blue to the second column
            Style[] columnStyles = { defaultStyle, lightBlueStyle };
```

> **Γιατί μόνο δύο στυλ;** Στο δείγμα μας έχουμε τέσσερις στήλες, αλλά θέλουμε μόνο τη δεύτερη στήλη (Name) να ξεχωρίζει. Το μήκος του πίνακα δεν χρειάζεται να ταιριάζει με τον αριθμό των στηλών· τυχόν ελλιπείς καταχωρήσεις κληρονομούν αυτόματα το προεπιλεγμένο στυλ του workbook.

## Βήμα 4: Εισαγωγή του DataTable με Κεφαλίδες και Στυλ

Εδώ φέρνουμε μαζί το **excel import datatable c#** και το **import data with headers**. Η μέθοδος `ImportDataTable` κάνει το σκληρό έργο: γράφει τα ονόματα των στηλών, τις γραμμές, και εφαρμόζει τον πίνακα στυλ που μόλις δημιουργήσαμε.

```csharp
            // Step 4: Import the DataTable into the first worksheet starting at cell A1, applying the styles
            Worksheet sheet = workbook.Worksheets[0];
            sheet.Cells.ImportDataTable(dataTable, // the source DataTable
                                        true,       // import column names as headers
                                        0,          // start row (0‑based)
                                        0,          // start column (0‑based)
                                        columnStyles);
```

### Αναμενόμενο Αποτέλεσμα

Μετά την εκτέλεση του προγράμματος, το `workbook` θα περιέχει ένα μόνο φύλλο εργασίας που φαίνεται ως εξής:

| **ID** | **Name** (ανοιχτό μπλε) | **HireDate** | **Salary** |
|-------|--------------------------|--------------|------------|
| 1     | Alice Johnson            | 5/12/2020    | 72000      |
| 2     | Bob Smith                | 3/4/2019     | 68000      |
| 3     | Carol White              | *(blank)*   | 75000      |

* Η στήλη **Name** έχει φόντο ανοιχτό μπλε, αποδεικνύοντας ότι ο πίνακας στυλ λειτουργεί.
* Οι κεφαλίδες των στηλών δημιουργούνται αυτόματα επειδή περάσαμε `true` για το `importColumnNames`.
* Οι τιμές null εμφανίζονται ως κενά κελιά, που είναι η προεπιλεγμένη συμπεριφορά του Aspose.Cells.

## Βήμα 5: Αποθήκευση του Workbook (Προαιρετικό αλλά Χρήσιμο)

Πιθανότατα θα θέλετε να γράψετε το αρχείο στο δίσκο ή να το στείλετε ως ροή σε έναν web client. Η αποθήκευση είναι απλή:

```csharp
            // Step 5: Save the workbook to a file
            string outputPath = "StyledEmployees.xlsx";
            workbook.Save(outputPath, SaveFormat.Xlsx);
            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

> **Pro tip:** Αν στοχεύετε σε παλαιότερες εκδόσεις του Excel, αλλάξτε το `SaveFormat.Xlsx` σε `SaveFormat.Xls`. Το API διαχειρίζεται τη μετατροπή για εσάς.

## Περιπτώσεις Άκρων & Παραλλαγές

### Πολλαπλές Στυλιζαρισμένες Στήλες

Αν χρειάζεστε περισσότερες από μία στυλιζαρισμένες στήλες, απλώς επεκτείνετε τον πίνακα `columnStyles`:

```csharp
Style[] columnStyles = { defaultStyle, lightBlueStyle, defaultStyle, lightBlueStyle };
```

Τώρα τόσο η **Name** όσο και η **Salary** θα είναι ανοιχτό μπλε.

### Μορφοποίηση υπό Συνθήκη αντί Στατικών Στυλ

Μερικές φορές θέλετε μια στήλη να γίνεται κόκκινη όταν η τιμή υπερβαίνει ένα όριο. Εκεί είναι που το **use default style excel** συναντά τη μορφοποίηση υπό συνθήκη:

```csharp
int salaryColIdx = 3; // zero‑based index for Salary column
FormatCondition condition = sheet.ConditionalFormattings[0]
    .AddCondition(FormatConditionType.CellValue, OperatorType.GreaterThan, "70000");
condition.Style.ForegroundColor = Color.LightCoral;
condition.Style.Pattern = BackgroundType.Solid;
```

### Εισαγωγή χωρίς Κεφαλίδες

Αν το σύστημα που λαμβάνει τα δεδομένα σας ήδη παρέχει τις δικές του κεφαλίδες, απλώς περάστε `false` για το όρισμα `importColumnNames`. Τα δεδομένα θα αρχίσουν στο `A1` και μπορείτε να γράψετε προσαρμοσμένες κεφαλίδες μετά.

```csharp
sheet.Cells.ImportDataTable(dataTable, false, 1, 0); // start at row 2 (index 1)
```

## Full Working Example (All

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}