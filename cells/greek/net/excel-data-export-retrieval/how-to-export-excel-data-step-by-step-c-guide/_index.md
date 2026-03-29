---
category: general
date: 2026-03-29
description: Μάθετε πώς να εξάγετε πίνακες Excel σε απλό κείμενο, να γράψετε συμβολοσειρά
  σε αρχείο και να μετατρέψετε πίνακα Excel σε CSV ή TXT χρησιμοποιώντας C#. Περιλαμβάνει
  πλήρες κώδικα και συμβουλές.
draft: false
keywords:
- how to export excel
- write string to file
- convert excel table
- export table as csv
- save txt file c#
language: el
og_description: Πώς να εξάγετε πίνακες Excel σε αρχεία κειμένου σε C#. Λάβετε τη πλήρη
  λύση, τον κώδικα και τις βέλτιστες πρακτικές για τη μετατροπή πινάκων Excel και
  την αποθήκευση αρχείων TXT.
og_title: Πώς να εξάγετε δεδομένα Excel – Πλήρης οδηγός C#
tags:
- C#
- Excel
- File I/O
title: Πώς να εξάγετε δεδομένα Excel – Οδηγός C# βήμα‑προς‑βήμα
url: /el/net/excel-data-export-retrieval/how-to-export-excel-data-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Εξάγετε Δεδομένα Excel – Πλήρης Οδηγός C#

Έχετε αναρωτηθεί ποτέ **πώς να εξάγετε δεδομένα Excel** χωρίς να ανοίξετε το φύλλο εργασίας χειροκίνητα; Ίσως χρειάζεται να αποβάλετε έναν πίνακα σε ένα απλό αρχείο κειμένου για ένα παλαιό σύστημα, ή θέλετε μια γρήγορη εξαγωγή CSV για αγωγούς ανάλυσης δεδομένων. Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από μια πρακτική, ολοκληρωμένη λύση που **γράφει μια συμβολοσειρά σε αρχείο** και σας δείχνει ακριβώς πώς να **convert Excel table** δεδομένα σε μορφή κειμένου με διαχωριστικό χρησιμοποιώντας C#.

Θα καλύψουμε τα πάντα, από τη φόρτωση του βιβλίου εργασίας, την επιλογή του σωστού πίνακα, τη διαμόρφωση των επιλογών εξαγωγής, και τέλος την αποθήκευση του αποτελέσματος ως αρχείο `.txt`. Στο τέλος θα μπορείτε να **export table as CSV** (ή οποιοδήποτε διαχωριστικό επιλέξετε) και θα δείτε επίσης μερικές χρήσιμες τεχνικές για **save txt file C#** έργα. Δεν απαιτούνται εξωτερικά εργαλεία—μόνο μερικά πακέτα NuGet και λίγος κώδικας.

---

## Τι Θα Χρειαστεί

- **.NET 6.0+** (ή .NET Framework 4.7.2 αν προτιμάτε κλασικό)
- **Syncfusion.XlsIO** πακέτο NuGet (η κλάση `ExportTableOptions` βρίσκεται εδώ)
- Ένα βασικό IDE C# (Visual Studio, VS Code, Rider—οποιοδήποτε είναι εντάξει)
- Ένα βιβλίο εργασίας Excel που περιέχει τουλάχιστον έναν πίνακα (θα χρησιμοποιήσουμε `ws.Tables[0]` στο παράδειγμα)

> Συμβουλή: Αν δεν έχετε ήδη τη βιβλιοθήκη Syncfusion, εκτελέστε  
> `dotnet add package Syncfusion.XlsIO.Net.Core` from the command line.

## Βήμα 1 – Άνοιγμα του Βιβλίου Εργασίας και Λήψη του Πρώτου Πίνακα  

Το πρώτο βήμα είναι να φορτώσετε το αρχείο Excel και να αποκτήσετε μια αναφορά στο φύλλο εργασίας που περιέχει τον πίνακα. Αυτό το βήμα είναι κρίσιμο επειδή η λειτουργία **convert excel table** λειτουργεί σε αντικείμενο `ITable`, όχι σε ακατέργαστες περιοχές κελιών.

```csharp
using Syncfusion.XlsIO;
using System.IO;

class ExcelExporter
{
    static void Main()
    {
        // Load the workbook (replace with your actual file path)
        using (ExcelEngine excelEngine = new ExcelEngine())
        {
            IApplication application = excelEngine.Excel;
            application.DefaultVersion = ExcelVersion.Xlsx;

            // Open the file
            FileStream stream = new FileStream(@"C:\Data\Sample.xlsx", FileMode.Open, FileAccess.Read);
            IWorkbook workbook = application.Workbooks.Open(stream);
            IWorksheet ws = workbook.Worksheets[0];   // First worksheet
```

*Γιατί είναι σημαντικό:* Το άνοιγμα του βιβλίου εργασίας με `using` εξασφαλίζει ότι όλες οι μη διαχειριζόμενες πόροι απελευθερώνονται, αποτρέποντας προβλήματα κλειδώματος αρχείου αργότερα όταν προσπαθείτε να **write string to file**.

## Βήμα 2 – Διαμόρφωση Επιλογών Εξαγωγής (Απλό Κείμενο, Χωρίς Κεφαλίδες, Διαχωριστικό Επικολλητικού)  

Τώρα λέμε στη Syncfusion πώς θέλουμε να σειριοποιηθεί ο πίνακας. Η `ExportTableOptions` σας επιτρέπει να ενεργοποιήσετε ή όχι την ένταξη κεφαλίδων, να επιλέξετε ένα διαχωριστικό, και να αποφασίσετε αν θα λάβετε μια συμβολοσειρά ή έναν πίνακα byte.

```csharp
            // Step 2: Configure export options – plain text, omit headers, ';' delimiter
            var exportOptions = new ExportTableOptions
            {
                ExportAsString = true,      // Returns a string we can write directly
                IncludeHeaders = false,     // Skip column headers if you don’t need them
                Delimiter = ";"             // Change to ',' for classic CSV
            };
```

*Γιατί είναι σημαντικό:* Ο ορισμός `IncludeHeaders = false` συχνά ταιριάζει με τις προσδοκίες των συστημάτων downstream που ήδη γνωρίζουν τη σειρά των στηλών. Η αλλαγή του διαχωριστικού είναι ο τρόπος με τον οποίο **export table as CSV** με προσαρμοσμένο διαχωριστικό.

## Βήμα 3 – Εξαγωγή του Πίνακα σε Συμβολοσειρά  

Με τις επιλογές έτοιμες, καλούμε τη `ExportToString`. Αυτή η μέθοδος εξάγει ολόκληρο τον πίνακα (συμπεριλαμβανομένων όλων των γραμμών) και επιστρέφει μια μοναδική συμβολοσειρά έτοιμη για έξοδο σε αρχείο.

```csharp
            // Step 3: Export the first table to a string using the configured options
            ITable firstTable = ws.Tables[0];               // Access the first table
            string tableText = firstTable.ExportToString(exportOptions);
```

*Γιατί είναι σημαντικό:* Η κλήση `ExportToString` κάνει τη βαριά δουλειά της μετατροπής του πλέγματος Excel σε μορφή με διαχωριστικό. Σεβεται το `Delimiter` που ορίσατε, έτσι λαμβάνετε ένα καθαρό αποτέλεσμα **export table as csv** χωρίς επιπλέον επεξεργασία.

## Βήμα 4 – Εγγραφή του Εξαγόμενου Κειμένου σε Αρχείο  

Τέλος, αποθηκεύουμε τη συμβολοσειρά στο δίσκο. Η `File.WriteAllText` είναι ο πιο απλός τρόπος για **save txt file C#**· δημιουργεί αυτόματα το αρχείο αν δεν υπάρχει και το αντικαθιστά διαφορετικά.

```csharp
            // Step 4: Write the exported text to a file
            string outputPath = @"C:\Data\ExportedTable.txt";
            File.WriteAllText(outputPath, tableText);
            System.Console.WriteLine($"Table exported successfully to {outputPath}");
        }
    }
}
```

*Γιατί είναι σημαντικό:* Γράφοντας τη συμβολοσειρά απευθείας, αποφεύγετε ένα επιπλέον βήμα μετατροπής. Το αρχείο τώρα περιέχει γραμμές όπως `Value1;Value2;Value3`, έτοιμες για οποιονδήποτε parser downstream.

## Πλήρες Παράδειγμα Εργασίας (Όλα τα Βήματα σε Ένα Σημείο)  

Παρακάτω είναι το πλήρες πρόγραμμα, έτοιμο για αντιγραφή‑επικόλληση, που συνδυάζει όλα όσα συζητήσαμε. Περιλαμβάνει διαχείριση σφαλμάτων και σχόλια για σαφήνεια.

```csharp
using Syncfusion.XlsIO;
using System;
using System.IO;

class ExcelExporter
{
    static void Main()
    {
        try
        {
            // 1️⃣ Load workbook and get first worksheet
            using (ExcelEngine excelEngine = new ExcelEngine())
            {
                IApplication app = excelEngine.Excel;
                app.DefaultVersion = ExcelVersion.Xlsx;

                string sourcePath = @"C:\Data\Sample.xlsx";
                using (FileStream fs = new FileStream(sourcePath, FileMode.Open, FileAccess.Read))
                {
                    IWorkbook wb = app.Workbooks.Open(fs);
                    IWorksheet ws = wb.Worksheets[0]; // first sheet

                    // 2️⃣ Set export options (plain text, no headers, ';' delimiter)
                    var opts = new ExportTableOptions
                    {
                        ExportAsString = true,
                        IncludeHeaders = false,
                        Delimiter = ";"
                    };

                    // 3️⃣ Export the first table to a string
                    ITable table = ws.Tables[0];
                    string csvText = table.ExportToString(opts);

                    // 4️⃣ Save the string to a .txt file
                    string destPath = @"C:\Data\ExportedTable.txt";
                    File.WriteAllText(destPath, csvText);

                    Console.WriteLine($"✅ Export complete! File saved at: {destPath}");
                }
            }
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"❌ Something went wrong: {ex.Message}");
        }
    }
}
```

**Αναμενόμενο αποτέλεσμα** (το περιεχόμενο του `ExportedTable.txt`):

```
John;Doe;35
Jane;Smith;28
Bob;Brown;42
```

Κάθε γραμμή αντιστοιχεί σε μια σειρά από τον αρχικό πίνακα Excel, με τιμές χωρισμένες με ερωτηματικά. Αν αλλάξετε `Delimiter = ","` θα έχετε ένα κλασικό αρχείο CSV.

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις  

### Τι γίνεται αν το βιβλίο εργασίας μου έχει πολλαπλούς πίνακες;  
Μπορείτε απλώς να αλλάξετε το `ws.Tables[0]` στο κατάλληλο ευρετήριο, ή να κάνετε βρόχο μέσω `ws.Tables`:

```csharp
foreach (var tbl in ws.Tables)
{
    string txt = tbl.ExportToString(opts);
    // Save each table to a separate file or concatenate as needed
}
```

### Πώς να Συμπεριλάβω Κεφαλίδες Στηλών;  
Ορίστε `IncludeHeaders = true` στην `ExportTableOptions`. Αυτό είναι χρήσιμο όταν το σύστημα downstream αναμένει μια γραμμή κεφαλίδας.

### Μπορώ να Εξάγω σε Διαφορετικό Φάκελο Δυναμικά;  
Απόλυτα. Χρησιμοποιήστε `Path.Combine` με `Environment.GetFolderPath(Environment.SpecialFolder.Desktop)` ή οποιοδήποτε μονοπάτι παρέχεται από τον χρήστη για να κάνετε τη λύση πιο ευέλικτη.

### Τι γίνεται με Μεγάλα Αρχεία;  
Για τεράστιους πίνακες, σκεφτείτε τη ροή εξόδου αντί να φορτώσετε ολόκληρη τη συμβολοσειρά στη μνήμη:

```csharp
using (StreamWriter writer = new StreamWriter(outputPath))
{
    writer.Write(table.ExportToString(opts));
}
```

### Λειτουργεί Αυτό σε .NET Core;  
Ναι—η Syncfusion.XlsIO υποστηρίζει .NET 5/6/7. Απλώς αναφέρετε το κατάλληλο πακέτο NuGet και είστε έτοιμοι.

## Συμβουλές Pro για Αξιόπιστες Εξαγωγές  

- **Επικυρώστε τη διαδρομή του αρχείου** πριν την εγγραφή. Ένας ελλιπής φάκελος θα προκαλέσει `DirectoryNotFoundException`.  
- **Ελέγξτε το `ExportAsString`** μόνο όταν ο πίνακας χωράει άνετα στη μνήμη· διαφορετικά, χρησιμοποιήστε `ExportToStream` για τεράστια σύνολα δεδομένων.  
- **Λάβετε υπόψη την πολιτισμική ρύθμιση**: αν τα δεδομένα σας περιέχουν κόμματα ως δεκαδικούς διαχωριστές, επιλέξτε ερωτηματικό (`;`) ή tab (`\t`) ως διαχωριστικό για να αποφύγετε σφάλματα ανάλυσης CSV.  
- **Κλείδωμα έκδοσης**: η Syncfusion περιστασιακά αλλάζει τις υπογραφές API. Καρφώστε την έκδοση του NuGet (`<PackageReference Include="Syncfusion.XlsIO.Net.Core" Version="21.2.0.44" />`) για να διατηρήσετε την αναπαραγωγιμότητα της κατασκευής.

## Συμπέρασμα  

Σε αυτόν τον οδηγό δείξαμε **πώς να εξάγετε Excel** πίνακες σε αρχεία απλού κειμένου χρησιμοποιώντας C#. Φορτώνοντας το βιβλίο εργασίας, διαμορφώνοντας την `ExportTableOptions`, εξάγοντας τον πίνακα σε συμβολοσειρά, και τελικά **γράφοντας τη συμβολοσειρά σε αρχείο**, έχετε τώρα ένα αξιόπιστο μοτίβο για εργασίες **convert excel table**, **export table as csv**, και **save txt file C#**.

Μη διστάσετε να πειραματιστείτε—αντικαταστήστε το διαχωριστικό, συμπεριλάβετε κεφαλίδες, ή επαναλάβετε για πολλαπλούς πίνακες. Η ίδια προσέγγιση λειτουργεί για τη δημιουργία αναφορών CSV, την τροφοδοσία δεδομένων σε παλαιά parsers, ή απλώς την αρχειοθέτηση του περιεχομένου των λογιστικών φύλλων ως ελαφριά αρχεία κειμένου.

Έχετε περισσότερα σενάρια που θέλετε να αντιμετωπίσετε; Ίσως χρειάζεστε να **write string to file** ασύγχρονα, ή θέλετε να συμπιέσετε το αποτέλεσμα άμεσα. Ρίξτε μια ματιά στα επόμενα tutorials μας για *asynchronous file I/O in C#* και *zipping files with .NET* για να συνεχίσετε.

Καλό κώδικα! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}