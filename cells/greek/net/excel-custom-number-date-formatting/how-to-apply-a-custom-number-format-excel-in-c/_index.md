---
category: general
date: 2026-10-26
description: Μάθετε πώς να ορίσετε προσαρμοσμένη μορφή αριθμού σε αρχείο Excel με
  C# διαμορφώνοντας τα σημαντικά ψηφία, δημιουργώντας ένα βιβλίο εργασίας Excel και
  αποθηκεύοντάς το ως έγγραφο XLSX.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- custom number format excel
- set significant digits
- how to set number format
- create excel workbook c#
- save workbook xlsx
language: el
lastmod: 2026-10-26
og_description: Η προσαρμοσμένη μορφή αριθμών στο Excel με C# σας επιτρέπει να ελέγχετε
  τα σημαντικά ψηφία, να δημιουργείτε ένα βιβλίο εργασίας Excel και να το αποθηκεύετε
  ως XLSX. Ακολουθήστε αυτό το πλήρες σεμινάριο.
og_image_alt: Excel cell A1 displaying a number formatted with 4 significant digits
  using C#
og_title: Προσαρμοσμένη μορφή αριθμών στο Excel με C# – οδηγός βήμα‑βήμα
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to set a custom number format excel file in C# by configuring
    significant digits, creating an Excel workbook, and saving it as an XLSX document.
  headline: How to apply a custom number format excel in C#
  type: TechArticle
- description: Learn how to set a custom number format excel file in C# by configuring
    significant digits, creating an Excel workbook, and saving it as an XLSX document.
  name: How to apply a custom number format excel in C#
  steps:
  - name: Using a custom format string instead of global options
    text: 'If you need a format that applies only to a single range, you can assign
      a format string directly:'
  - name: Applying the setting to an entire column
    text: '```csharp // Apply the same significant‑digit rule to column B ws.Cells.Columns[1].ApplyNumberFormatOptions(
      new NumberFormatOptions { SignificantDigits = 4 }); ```'
  - name: Dealing with negative numbers
    text: 'The global `SignificantDigits` option works uniformly for positive and
      negative numbers. If you want a different display for negatives, combine it
      with a custom format:'
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: Πώς να εφαρμόσετε προσαρμοσμένη μορφή αριθμού στο Excel με C#
url: /el/net/excel-custom-number-date-formatting/how-to-apply-a-custom-number-format-excel-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να εφαρμόσετε προσαρμοσμένη μορφή αριθμού excel σε C#

Αν χρειάζεστε μια **προσαρμοσμένη μορφή αριθμού excel** που εμφανίζει συγκεκριμένο αριθμό σημαντικών ψηφίων, αυτός ο οδηγός σας δείχνει ακριβώς πώς να το κάνετε σε C#. Θα δείτε πώς να ορίσετε τα σημαντικά ψηφία, να δημιουργήσετε ένα βιβλίο εργασίας Excel και να αποθηκεύσετε το βιβλίο ως αρχείο XLSX — όλα με λίγες γραμμές κώδικα.

Η εργασία με αρχεία Excel προγραμματιστικά συχνά απαιτεί έλεγχο του πώς εμφανίζονται οι αριθμοί. Χρησιμοποιώντας το Aspose.Cells για .NET μπορείτε να ορίσετε μια παγκόσμια επιλογή μορφοποίησης αριθμού που αναγκάζει κάθε αριθμητικό κελί να σέβεται έναν δεδομένο αριθμό σημαντικών ψηφίων. Αυτό το tutorial καλύπτει ολόκληρη τη ροή εργασίας, από τη ρύθμιση του έργου μέχρι την επαλήθευση του αποτελέσματος στο Excel.

## Προαπαιτούμενα

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

* .NET 6.0 ή νεότερη έκδοση εγκατεστημένη (ο κώδικας λειτουργεί επίσης με .NET Framework 4.7.2+)
* Visual Studio 2022 ή οποιοδήποτε IDE C# προτιμάτε
* Το πακέτο **Aspose.Cells** NuGet (`Install-Package Aspose.Cells`) – μια πλήρως διαχειριζόμενη βιβλιοθήκη για επεξεργασία Excel
* Βασική εξοικείωση με τη σύνταξη της C#

## Βήμα 1: Δημιουργία βιβλίου εργασίας Excel σε C#

Η πρώτη ενέργεια είναι η δημιουργία ενός νέου αντικειμένου `Workbook`. Αυτό το αντικείμενο αντιπροσωπεύει ολόκληρο το αρχείο Excel στη μνήμη.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook instance
        Workbook wb = new Workbook();

        // The workbook now contains a default worksheet named "Sheet1"
        // You can access it via the Worksheets collection.
        Worksheet ws = wb.Worksheets[0];
```

**Γιατί είναι σημαντικό:** Το `Workbook` είναι το σημείο εισόδου για κάθε λειτουργία Excel. Δημιουργώντας το πρώτα, εξασφαλίζετε ένα καθαρό αρχείο που μπορείτε αργότερα να αποθηκεύσετε ως XLSX.

## Βήμα 2: Διαμόρφωση της μορφής αριθμού για ορισμό σημαντικών ψηφίων

Το Aspose.Cells παρέχει μια παγκόσμια ρύθμιση που ονομάζεται `NumberFormatOptions`. Ορίζοντας `SignificantDigits = 4`, κάθε αριθμητικό κελί θα εμφανίζει έως και τέσσερα σημαντικά ψηφία, εκτός εάν μια πιο συγκεκριμένη μορφή το παρακάμπτει.

```csharp
        // Step 2: Set the global number‑format option to 4 significant digits
        WorkbookSettings.SetNumberFormatOptions(
            new NumberFormatOptions { SignificantDigits = 4 });
```

**Γιατί είναι σημαντικό:** Η χρήση του `SetNumberFormatOptions` σας επιτρέπει να ορίσετε μια **προσαρμοσμένη μορφή αριθμού excel** χωρίς να γράψετε μια συμβολοσειρά μορφής για κάθε κελί. Αντιστοιχεί στην επιλογή “Significant Digits” που θα βρείτε στο διάλογο *Format Cells → Number → Custom* του Excel.

## Βήμα 3: Εγγραφή τιμών και επαλήθευση της προσαρμοσμένης μορφής αριθμού

Τώρα τοποθετήστε μια αριθμητική τιμή σε ένα κελί. Η παγκόσμια ρύθμιση θα εφαρμόσει αυτόματα τον κανόνα των 4 ψηφίων.

```csharp
        // Step 3: Write a numeric value into cell A1 (row 0, column 0)
        ws.Cells[0, 0].PutValue(123.456789);

        // Optional: Add a label so you can see the effect in Excel
        ws.Cells[0, 1].PutValue("Original value:");
        ws.Cells[0, 2].PutValue(123.456789);
```

Όταν ανοίξετε το αποθηκευμένο αρχείο, το κελί **A1** θα εμφανίσει `123.5` (στρογγυλοποιημένο στα τέσσερα σημαντικά ψηφία). Η αρχική τιμή παραμένει αμετάβλητη στα υποκείμενα δεδομένα, κάτι που μπορείτε να επιβεβαιώσετε κοιτάζοντας τη γραμμή τύπων.

**Συμβουλή για ακραίες περιπτώσεις:** Αν αποθηκεύσετε έναν πολύ μεγάλο αριθμό όπως `12345678.9`, η ίδια ρύθμιση θα εμφανίσει `1.235E+07` (επιστημονική σημειογραφία) επειδή το Excel επιλέγει την πιο συμπαγή αναπαράσταση διατηρώντας τα τέσσερα σημαντικά ψηφία.

## Βήμα 4: Αποθήκευση του βιβλίου εργασίας ως XLSX

Τέλος, αποθηκεύστε το βιβλίο εργασίας στο δίσκο. Η μέθοδος `Save` επιλέγει αυτόματα τη μορφή αρχείου βάσει της επέκτασης.

```csharp
        // Step 4: Save the workbook to an XLSX file
        string outputPath = @"C:\Temp\SigDigits.xlsx";
        wb.Save(outputPath);

        // Inform the user
        System.Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

**Γιατί είναι σημαντικό:** Η αποθήκευση ως **XLSX** (`save workbook xlsx`) εξασφαλίζει μέγιστη συμβατότητα με τις σύγχρονες εκδόσεις του Excel, το Office 365 και άλλα εργαλεία λογιστικών φύλλων.

## Αναμενόμενο αποτέλεσμα

Ανοίξτε το *C:\Temp\SigDigits.xlsx* στο Microsoft Excel. Θα πρέπει να δείτε:

| A          | B               | C               |
|------------|-----------------|-----------------|
| **123.5**  | Αρχική τιμή:    | **123.456789**  |

*Κελί A1* εμφανίζει τον αριθμό στρογγυλοποιημένο στα τέσσερα σημαντικά ψηφία, ενώ το *C1* διατηρεί την πλήρη ακρίβεια για σύγκριση.

## Συχνές παραλλαγές και πώς να ορίσετε μορφή αριθμού για συγκεκριμένα κελιά

### Χρήση συμβολοσειράς προσαρμοσμένης μορφής αντί των παγκόσμιων επιλογών

Αν χρειάζεστε μια μορφή που εφαρμόζεται μόνο σε μια συγκεκριμένη περιοχή, μπορείτε να ορίσετε μια συμβολοσειρά μορφής απευθείας:

```csharp
ws.Cells["D1"].PutValue(0.0012345);
Style style = wb.CreateStyle();
style.Custom = "0.####"; // shows up to 4 decimal places, not significant digits
ws.Cells["D1"].SetStyle(style);
```

### Εφαρμογή της ρύθμισης σε ολόκληρη τη στήλη

```csharp
// Apply the same significant‑digit rule to column B
ws.Cells.Columns[1].ApplyNumberFormatOptions(
    new NumberFormatOptions { SignificantDigits = 4 });
```

### Διαχείριση αρνητικών αριθμών

Η παγκόσμια επιλογή `SignificantDigits` λειτουργεί ομοιόμορφα για θετικούς και αρνητικούς αριθμούς. Αν θέλετε διαφορετική εμφάνιση για τα αρνητικά, συνδυάστε την με μια προσαρμοσμένη μορφή:

```csharp
Style negStyle = wb.CreateStyle();
negStyle.Custom = "#,##0.###;[Red]-#,##0.###";
ws.Cells["E1"].PutValue(-9876.54321);
ws.Cells["E1"].SetStyle(negStyle);
```

## Συμβουλές επαγγελματία και παγίδες

* **Συμβουλή επαγγελματία:** Ορίστε τις επιλογές μορφοποίησης αριθμού **πριν** γράψετε οποιαδήποτε δεδομένα. Η αλλαγή της επιλογής μετά την πληρότητα των κελιών δεν επαναμορφοποιεί τις υπάρχουσες τιμές.
* **Προσοχή για:** Χρήση του `PutValue` με **string** που μοιάζει με αριθμό (π.χ., `"123.45"`). Το Excel θα το αντιμετωπίσει ως κείμενο και η προσαρμοσμένη μορφή δεν θα εφαρμοστεί.
* **Σημείωση απόδοσης:** Οι παγκόσμιες ρυθμίσεις είναι ελαφριές, αλλά η εφαρμογή ενός στυλ σε εκατομμύρια κελιά μπορεί να αυξήσει τη χρήση μνήμης. Χρησιμοποιήστε μορφοποίηση επιπέδου στήλης όταν είναι δυνατόν.

## Επόμενα βήματα

Τώρα που μπορείτε να **προσαρμόσετε τη μορφή αριθμού excel** με σημαντικά ψηφία, μπορείτε να εξερευνήσετε:

* **Πώς να ορίσετε μορφή αριθμού** για ημερομηνίες και νομίσματα χρησιμοποιώντας `Style.Custom`.
* **Δημιουργία γραφημάτων** που σέβονται τις προσαρμοσμένες μορφές σας.
* **Εξαγωγή σε CSV** διατηρώντας την αριθμητική ακρίβεια (`save workbook xlsx` → `wb.Save("file.csv", SaveFormat.Csv)`).

Αυτά τα θέματα βασίζονται στις ίδιες έννοιες `Workbook` και `Worksheet` που παρουσιάστηκαν εδώ.

---

**Σύνοψη**

Μάθατε πώς να **προσαρμόσετε τη μορφή αριθμού excel** διαμορφώνοντας το `NumberFormatOptions` για **ορισμό σημαντικών ψηφίων**, δημιουργώντας ένα βιβλίο εργασίας Excel σε C#, γράφοντας τιμές και **αποθηκεύοντας το βιβλίο ως αρχείο XLSX**. Ο πλήρης, εκτελέσιμος κώδικας παραπάνω δείχνει κάθε βήμα, εξηγεί γιατί κάθε μέρος είναι απαραίτητο και παρέχει συμβουλές για κοινές παραλλαγές. Ελεύθερα προσαρμόστε τα αποσπάσματα στα δικά σας έργα και πειραματιστείτε με άλλες περιπτώσεις μορφοποίησης.

## Τι θα πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να κυριαρχήσετε σε επιπλέον δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στην υλοποίηση.

- [Προσαρμοσμένη μορφή αριθμού Excel σε C# – Πλήρης Οδηγός](/cells/english/net/excel-custom-number-date-formatting/custom-number-format-excel-in-c-complete-guide/)
- [Δημιουργία βιβλίου εργασίας Excel C# – Περιορισμός σημαντικών ψηφίων Excel](/cells/english/net/excel-custom-number-date-formatting/create-excel-workbook-c-limit-significant-digits-excel/)
- [Πώς να εφαρμόσετε μορφή αριθμού excel με Aspose.Cells](/cells/english/net/excel-custom-number-date-formatting/how-to-apply-number-format-excel-with-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}