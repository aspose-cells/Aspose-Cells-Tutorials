---
category: general
date: 2026-03-18
description: Εξαγωγή ημερομηνίας από το Excel και εμφάνιση της ημερομηνίας yyyy‑mm‑dd
  σε μορφή ISO. Μάθετε πώς να διαβάζετε ημερομηνίες Ιαπωνικής εποχής, να τις μετατρέπετε
  και να εμφανίζετε ημερομηνίες ISO σε C#.
draft: false
keywords:
- extract date from excel
- output date yyyy-mm-dd
- display date iso format
language: el
og_description: Εξάγετε ημερομηνία από το Excel και εμφανίστε την ημερομηνία yyyy‑mm‑dd
  σε μορφή ISO. Αναλυτικός οδηγός C# βήμα‑βήμα με πλήρη κώδικα και εξηγήσεις.
og_title: Εξαγωγή ημερομηνίας από το Excel – Έξοδος ημερομηνίας yyyy‑mm‑dd σε C#
tags:
- C#
- Excel
- DateTime
- Aspose.Cells
title: Εξαγωγή ημερομηνίας από το Excel και έξοδος ημερομηνίας yyyy‑mm‑dd – Πλήρης
  Οδηγός C#
url: /el/net/data-loading-and-parsing/extract-date-from-excel-and-output-date-yyyy-mm-dd-complete/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή ημερομηνίας από το Excel – Πώς να εμφανίσετε την ημερομηνία yyyy‑mm‑dd σε μορφή ISO

Έχετε ποτέ χρειαστεί να **extract date from Excel** αλλά δεν ήσασταν σίγουροι πώς να διαχειριστείτε ημερομηνίες ιαπωνικής εποχής ή να πάρετε μια καθαρή συμβολοσειρά `yyyy‑mm‑dd`; Δεν είστε μόνοι. Σε πολλά έργα μεταφοράς δεδομένων το πηγαίο βιβλίο εργασίας αποθηκεύει ημερομηνίες χρησιμοποιώντας το ιαπωνικό ημερολογιακό σύστημα του Αυτοκράτορα, και το σύστημα προορισμού αναμένει μια ημερομηνία συμβατή με ISO όπως `2024-04-01`.  

Σε αυτόν τον οδηγό θα περάσουμε βήμα‑βήμα από μια πλήρη, εκτελέσιμη λύση που διαβάζει ένα κελί, ερμηνεύει την ιαπωνική εποχή, και **outputs the date yyyy‑mm‑dd**. Στο τέλος θα ξέρετε ακριβώς πώς να **display date ISO format** σε οποιαδήποτε εφαρμογή .NET, και θα έχετε ένα επαναχρησιμοποιήσιμο απόσπασμα κώδικα που μπορείτε να ενσωματώσετε στο δικό σας έργο.

## Τι θα χρειαστείτε

- **.NET 6+** (ή .NET Framework 4.7.2+).  
- **Aspose.Cells for .NET** – η βιβλιοθήκη που μας επιτρέπει να ορίσουμε προσαρμοσμένο ημερολόγιο κατά τη φόρτωση ενός βιβλίου εργασίας.  
- Ένα αρχείο Excel (`japan-date.xlsx`) που περιέχει μια ημερομηνία αποθηκευμένη σε κελί ιαπωνικής εποχής (π.χ., `令和3年4月1日`).  
- Ένα αγαπημένο IDE – Visual Studio, Rider, ή ακόμη και VS Code αρκεί.

Δεν απαιτούνται πρόσθετα πακέτα NuGet πέρα από το Aspose.Cells, και ο κώδικας λειτουργεί σε Windows, Linux ή macOS.

## Βήμα 1: Ρύθμιση του έργου και εγκατάσταση του Aspose.Cells

```bash
dotnet new console -n ExcelDateDemo
cd ExcelDateDemo
dotnet add package Aspose.Cells
```

> **Pro tip:** Αν τρέχετε σε διακομιστή CI, κλειδώστε την έκδοση του πακέτου (`Aspose.Cells 23.12`) για να εξασφαλίσετε επαναλήψιμες κατασκευές.

## Βήμα 2: Φόρτωση του βιβλίου εργασίας με το ιαπωνικό ημερολογιακό σύστημα του Αυτοκράτορα

Το κλειδί για **extract date from Excel** όταν η πηγή χρησιμοποιεί μη‑Γρηγοριακό ημερολόγιο είναι να πείτε στο Aspose.Cells ποιο ημερολόγιο πρέπει να εφαρμόσει κατά τη φόρτωση. Το κάνουμε αυτό με το `LoadOptions.Calendar`.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 2: Create load options and set the Japanese Emperor calendar
        LoadOptions loadOptions = new LoadOptions
        {
            // This tells Aspose.Cells to interpret era dates correctly
            Calendar = new JapaneseEmperorCalendar()
        };

        // Step 3: Open the workbook that contains Japanese era dates
        // Replace the path with the actual location of your Excel file
        string filePath = @"YOUR_DIRECTORY\japan-date.xlsx";
        Workbook workbook = new Workbook(filePath, loadOptions);
```

**Why this matters:** Χωρίς το προσαρμοσμένο ημερολόγιο, το Aspose.Cells θα θεωρούσε το κελί ως απλό κείμενο και θα χάνατε τις πληροφορίες της εποχής. Αναθέτοντας το `JapaneseEmperorCalendar`, η βιβλιοθήκη μετατρέπει αυτόματα το `令和3年4月1日` σε `2021‑04‑01` στο παρασκήνιο.

## Βήμα 3: Ανάκτηση της ημερομηνίας από ένα συγκεκριμένο κελί

Τώρα που το βιβλίο εργασίας ξέρει πώς να ερμηνεύσει την εποχή, μπορούμε να διαβάσουμε το κελί ως `DateTime`. Ας υποθέσουμε ότι η ημερομηνία βρίσκεται στο πρώτο φύλλο, κελί **A1** (γραμμή 0, στήλη 0).

```csharp
        // Step 4: Retrieve the date value from the first worksheet, first cell
        Worksheet sheet = workbook.Worksheets[0];
        Cell dateCell = sheet.Cells[0, 0]; // A1

        // GetDateTime() returns a System.DateTime object
        DateTime extractedDate = dateCell.GetDateTime();
```

Αν το κελί είναι κενό ή περιέχει μη‑ημερομηνιακή τιμή, το `GetDateTime()` θα ρίξει εξαίρεση. Μια αμυντική προσέγγιση φαίνεται έτσι:

```csharp
        if (dateCell.Type != CellValueType.IsDateTime)
        {
            Console.WriteLine("The target cell does not contain a valid date.");
            return;
        }

        DateTime extractedDate = dateCell.GetDateTime();
```

**Edge case:** Κάποια παλαιότερα αρχεία Excel αποθηκεύουν ημερομηνίες ως αριθμούς (σειριακές ημερομηνίες). Το Aspose.Cells τα διαχειρίζεται αυτόματα, αλλά θα πρέπει να ελέγχετε τον τύπο του κελιού αν περιμένετε μεικτό περιεχόμενο.

## Βήμα 4: Εξαγωγή ημερομηνίας yyyy‑mm‑dd (ISO) και επαλήθευση

Με το `DateTime` στα χέρια, η μορφοποίηση του ως **output date yyyy‑mm‑dd** είναι μια γραμμή κώδικα:

```csharp
        // Step 5: Output the date in ISO format (yyyy‑mm‑dd)
        string isoDate = extractedDate.ToString("yyyy-MM-dd");
        Console.WriteLine($"Extracted date (ISO): {isoDate}");
    }
}
```

Εκτελώντας το πρόγραμμα με ένα αρχείο που περιέχει `令和3年4月1日` θα εμφανίσει:

```
Extracted date (ISO): 2021-04-01
```

Αυτή είναι η ακριβής **display date iso format** που απαιτούν πολλά APIs.

## Παράδειγμα πλήρους λειτουργικού κώδικα

Συνδυάζοντας όλα τα κομμάτια, εδώ είναι το ολοκληρωμένο, έτοιμο για αντιγραφή‑επικόλληση πρόγραμμα:

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load the workbook with Japanese era support
        LoadOptions loadOptions = new LoadOptions
        {
            Calendar = new JapaneseEmperorCalendar()
        };

        string filePath = @"YOUR_DIRECTORY\japan-date.xlsx";
        Workbook workbook = new Workbook(filePath, loadOptions);

        // Access the cell that holds the date (A1)
        Worksheet sheet = workbook.Worksheets[0];
        Cell dateCell = sheet.Cells[0, 0];

        // Validate the cell contains a date
        if (dateCell.Type != CellValueType.IsDateTime)
        {
            Console.WriteLine("The target cell does not contain a valid date.");
            return;
        }

        // Extract the DateTime value
        DateTime extractedDate = dateCell.GetDateTime();

        // Convert to ISO format (yyyy‑mm‑dd)
        string isoDate = extractedDate.ToString("yyyy-MM-dd");
        Console.WriteLine($"Extracted date (ISO): {isoDate}");
    }
}
```

> **Note:** Αντικαταστήστε το `YOUR_DIRECTORY` με το πραγματικό φάκελο που περιέχει το `japan-date.xlsx`. Ο κώδικας λειτουργεί με οποιοδήποτε φύλλο και οποιοδήποτε κελί – απλώς προσαρμόστε τα ευρετήρια.

## Διαχείριση άλλων ημερολογίων (Προαιρετικό)

Αν ποτέ χρειαστείτε να **extract date from Excel** που χρησιμοποιεί το Ταϊλανδικό Βουδιστικό ημερολόγιο ή το Εβραϊκό ημερολόγιο, απλώς αντικαταστήστε την παρουσία του ημερολογίου:

```csharp
loadOptions.Calendar = new ThaiBuddhistCalendar();   // for Thai dates
// or
loadOptions.Calendar = new HebrewCalendar();         // for Hebrew dates
```

Το υπόλοιπο της λογικής παραμένει αμετάβλητο, κάτι που δείχνει την ευελιξία της προσέγγισης.

## Κοινά προβλήματα και πώς να τα αποφύγετε

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| `GetDateTime()` throws `InvalidCastException` | Το κελί δεν είναι ημερομηνία (ίσως κείμενο) | Ελέγξτε το `Cell.Type` πριν το καλέσετε, ή χρησιμοποιήστε `DateTime.TryParse` στο `Cell.StringValue`. |
| Wrong year after conversion | Το βιβλίο εργασίας φορτώθηκε χωρίς να οριστεί το `Calendar` | Πάντα δημιουργείτε `LoadOptions` με το κατάλληλο ημερολόγιο **πριν** ανοίξετε το αρχείο. |
| ISO output shows time part (`2021-04-01 00:00:00`) | Χρησιμοποιήσατε `ToString()` χωρίς μορφοποίηση | Χρησιμοποιήστε το format specifier `"yyyy-MM-dd"` για να εξαναγκάσετε **output date yyyy‑mm‑dd**. |
| File not found | Η σχετική διαδρομή δείχνει σε λάθος φάκελο | Χρησιμοποιήστε `Path.Combine(Environment.CurrentDirectory, "japan-date.xlsx")` ή δώστε απόλυτη διαδρομή. |

## Συμβουλές για κώδικα έτοιμο για παραγωγή

1. **Cache the workbook** αν χρειάζεται να διαβάσετε πολλές ημερομηνίες από το ίδιο αρχείο – το άνοιγμα ενός βιβλίου εργασίας είναι σχετικά ακριβό.  
2. **Wrap the extraction logic** σε μια επαναχρησιμοποιήσιμη μέθοδο:

   ```csharp
   static string ExtractIsoDate(string file, int sheetIdx, int row, int col)
   {
       var opts = new LoadOptions { Calendar = new JapaneseEmperorCalendar() };
       var wb = new Workbook(file, opts);
       var cell = wb.Worksheets[sheetIdx].Cells[row, col];
       if (cell.Type != CellValueType.IsDateTime) return null;
       return cell.GetDateTime().ToString("yyyy-MM-dd");
   }
   ```

3. **Log the original era string** (`cell.StringValue`) μαζί με το ISO output για σκοπούς ελέγχου.  
4. **Unit test** τη μέθοδο με μερικά σκληρά κωδικοποιημένα αρχεία Excel που καλύπτουν διαφορετικές εποχές (Heisei, Reiwa) για να εγγυηθείτε τη σωστή λειτουργία.

## Οπτική επισκόπηση

Παρακάτω υπάρχει ένα γρήγορο διάγραμμα που απεικονίζει τη ροή δεδομένων—from Excel cell to ISO string.  

![Extract date from Excel example showing Excel → LoadOptions → DateTime → ISO string]  

*Alt text: “extract date from excel” diagram displaying the conversion pipeline.*

## Συμπέρασμα

Καλύψαμε όλα όσα χρειάζεστε για να **extract date from Excel**, να διαχειριστείτε τιμές ιαπωνικής εποχής, και να **output date yyyy‑mm‑dd** ώστε να συμμορφώνεται με την **display date iso format** που αγαπούν τα σύγχρονα APIs. Η λύση είναι αυτόνομη, λειτουργεί με οποιαδήποτε έκδοση .NET που υποστηρίζει το Aspose.Cells, και μπορεί να επεκταθεί σε άλλα ημερολόγια με μια μόνο αλλαγή γραμμής.

Έχετε κάποιο άλλο ημερολόγιο στο μυαλό σας; Ή ίσως εξάγετε ημερομηνίες από πολλές στήλες; Μη διστάσετε να τροποποιήσετε το βοηθητικό `ExtractIsoDate` ή να αφήσετε ένα σχόλιο παρακάτω. Καλό coding, και εύχομαι οι ημερομηνίες σας να παραμένουν πάντα σε τέλεια ISO συγχρονισμό!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}