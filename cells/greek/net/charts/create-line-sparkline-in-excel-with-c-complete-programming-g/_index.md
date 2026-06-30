---
category: general
date: 2026-06-30
description: Δημιουργήστε γραμμική sparkline στο Excel με C# γρήγορα. Μάθετε πώς να
  προσθέσετε sparkline, να δημιουργήσετε βιβλίο εργασίας Excel με C# και να προσθέσετε
  sparkline σε κελί σε λίγα βήματα.
draft: false
keywords:
- create line sparkline
- how to add sparkline
- add line sparkline
- create excel workbook c#
- add sparkline to cell
language: el
og_description: Δημιουργήστε γραμμικό sparkline στο Excel με C#. Αυτό το σεμινάριο
  δείχνει πώς να προσθέσετε sparkline, να δημιουργήσετε βιβλίο εργασίας Excel με C#
  και να ενσωματώσετε το sparkline σε ένα κελί.
og_title: Δημιουργία γραμμικής sparkline στο Excel με C# – Οδηγός βήμα‑βήμα
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Create line sparkline in Excel with C# quickly. Learn how to add sparkline,
    create Excel workbook C#, and add sparkline to cell in a few steps.
  headline: Create line sparkline in Excel with C# – Complete Programming Guide
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Δημιουργία γραμμικής sparkline στο Excel με C# – Πλήρης Οδηγός Προγραμματισμού
url: /el/net/charts/create-line-sparkline-in-excel-with-c-complete-programming-g/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία γραμμικής sparkline στο Excel με C# – Πλήρης Οδηγός Προγραμματισμού

Έχετε αναρωτηθεί ποτέ πώς να **create line sparkline** σε ένα αρχείο Excel χρησιμοποιώντας C#; Δεν είστε οι μόνοι—οι προγραμματιστές ρωτούν συνεχώς, “πώς να προσθέσω sparkline σε μια αναφορά χωρίς να ανοίξω το Excel χειροκίνητα;” Τα καλά νέα είναι ότι με λίγες γραμμές κώδικα μπορείτε να δημιουργήσετε μια κομψή γραμμική sparkline απευθείας μέσα στο βιβλίο εργασίας, χωρίς UI.

Σε αυτό το tutorial θα περάσουμε από όλα όσα χρειάζεται να γνωρίζετε: από τα βασικά του **create Excel workbook C#**, μέσω της συμπλήρωσης δεδομένων, μέχρι τα ακριβή βήματα για **add line sparkline** και **add sparkline to cell**. Στο τέλος θα έχετε ένα έτοιμο *.xlsx* αρχείο που οπτικοποιεί τις μηνιαίες τάσεις πωλήσεων με μια ματιά. Χωρίς περιττές πληροφορίες, μόνο μια πρακτική, εκτελέσιμη λύση.

---

## Τι Θα Δημιουργήσετε

- Ένα νέο βιβλίο εργασίας Excel με όνομα *KPI_Sparklines.xlsx*  
- Ένα φύλλο εργασίας που ονομάζεται **KPI** περιέχοντας δείγμα αριθμών πωλήσεων  
- Μια **line sparkline** τοποθετημένη στο κελί **D2** που αναφέρεται στην περιοχή δεδομένων **B2:B13**  
- Βασική μορφοποίηση (χρώμα, πάχος γραμμής) για να ξεχωρίζει η sparkline  

Προαπαιτούμενα; Απλώς το .NET SDK (3.1+ ή .NET 6) και η δωρεάν βιβλιοθήκη Aspose.Cells for .NET (διαθέσιμη μέσω NuGet). Αν δεν έχετε χρησιμοποιήσει ποτέ το Aspose.Cells, σκεφτείτε το ως μια ισχυρή μηχανή Excel που μπορείτε να καλέσετε από κώδικα—χωρίς COM interop, χωρίς ανάγκη εγκατάστασης του Excel.

![Δημιουργία γραμμικής sparkline στο Excel χρησιμοποιώντας C#](https://example.com/images/create-line-sparkline.png "Δημιουργία γραμμικής sparkline στο Excel με C#")

*Κείμενο εναλλακτικής εικόνας: δημιουργία γραμμικής sparkline στο Excel χρησιμοποιώντας κώδικα C#*

---

## Βήμα 1: **Create Excel workbook C#** – Ρύθμιση του αρχείου και του φύλλου εργασίας

Πρώτα απ' όλα. Χρειαζόμαστε ένα αντικείμενο workbook και ένα φύλλο εργασίας όπου θα αποθηκευτούν τα δεδομένα. Αυτή είναι η βάση για οποιονδήποτε αυτοματισμό Excel, είτε αργότερα **add line sparkline** είτε γράψετε τύπους.

```csharp
using Aspose.Cells;
using System.Drawing;

// Initialize a new workbook
Workbook workbook = new Workbook();

// Grab the first worksheet (index 0) and give it a meaningful name
Worksheet worksheet = workbook.Worksheets[0];
worksheet.Name = "KPI";   // “KPI” will hold our key performance indicators
```

> **Γιατί είναι σημαντικό:** Η κλάση `Workbook` αντιπροσωπεύει ολόκληρο το αρχείο, ενώ το `Worksheet` είναι ο καμβάς για γραμμές, στήλες και, τελικά, τη δική μας sparkline. Η προγενέστερη ονομασία του φύλλου διατηρεί το αρχείο τακτοποιημένο και αυτο‑τεκμηριωμένο.

---

## Βήμα 2: Συμπλήρωση δεδομένων – Η πηγή δεδομένων για τη sparkline

Μια sparkline χρειάζεται δεδομένα για να σχεδιάσει. Ας προσομοιώσουμε 12 μήνες αριθμών πωλήσεων. Θα μπορούσατε να τα αντλήσετε από μια βάση δεδομένων, αλλά για σαφήνεια θα τα δημιουργήσουμε άμεσα.

```csharp
// Fill column B (index 1) with monthly sales numbers
for (int month = 0; month < 12; month++)
{
    // Example pattern: start at 5,000 and increase by 750 each month
    worksheet.Cells[month + 1, 1].PutValue(5000 + month * 750);
}
```

> **Συμβουλή:** Η `PutValue` ανιχνεύει αυτόματα τον τύπο δεδομένων, οπότε δεν χρειάζεται να μετατρέψετε σε `double` ή `int`. Αν χρειαστεί ποτέ να μορφοποιήσετε τα κελιά (νόμισμα, διαχωριστικά χιλιάδων), μπορείτε να εφαρμόσετε ένα αντικείμενο `Style` αργότερα.

---

## Βήμα 3: **Create line sparkline** – Προσθήκη της sparkline σε συγκεκριμένο κελί

Τώρα έρχεται το αστέρι της παράστασης: η **line sparkline**. Το Aspose.Cells ομαδοποιεί τις sparklines, έτσι πρώτα δημιουργούμε ένα `SparklineGroup` τύπου `Line`, μετά του λέμε πού να τοποθετήσει το οπτικό στοιχείο.

```csharp
// Add a new SparklineGroup of type Line
int groupIndex = worksheet.SparklineGroups.Add(SparklineType.Line);
SparklineGroup sparklineGroup = worksheet.SparklineGroups[groupIndex];

// Add a sparkline that lives in D2 (row 1, column 3) and reads data from B2:B13
// Parameters: firstRow, firstColumn, lastRow, lastColumn, firstDataRow, lastDataRow
sparklineGroup.Add(1, 3, 1, 3, 1, 12);   // D2 ↔ B2:B13
```

> **Πώς λειτουργεί:**  
> - `firstRow/firstColumn` και `lastRow/lastColumn` ορίζουν το *κελί-στόχο* (όπου εμφανίζεται η sparkline).  
> - `firstDataRow/lastDataRow` δείχνουν στην περιοχή πηγής.  
> Επειδή χρησιμοποιούμε μια **line sparkline**, το οπτικό στοιχείο θα είναι μια απλή λεπτή γραμμή που ακολουθεί την τάση των αριθμών.

### Προαιρετικό: **How to add sparkline** με προσαρμοσμένο στυλ

Αν θέλετε η sparkline να ξεχωρίζει, προσαρμόστε μερικές ιδιότητες:

```csharp
sparklineGroup.LineWeight = 1.0;               // Thickness of the line
sparklineGroup.SeriesColor = Color.DarkBlue;  // Color of the sparkline line
sparklineGroup.ShowMarkers = true;             // Show data markers (optional)
sparklineGroup.MarkerColor = Color.OrangeRed;  // Marker color
```

> **Γιατί να τη μορφοποιήσετε;** Μια σκούρα μπλε γραμμή πάνω σε λευκό φόντο είναι ήπια για τα μάτια, ενώ τα markers παρέχουν γρήγορη ένδειξη για τα μεμονωμένα σημεία δεδομένων—χρήσιμο για παρουσιάσεις.

---

## Βήμα 4: Αποθήκευση του βιβλίου εργασίας – Επαλήθευση του αποτελέσματος

Με τη sparkline στη θέση της, χρειάζεται μόνο να γράψουμε το αρχείο στο δίσκο. Επιλέξτε έναν φάκελο στον οποίο έχετε δικαίωμα εγγραφής· το παράδειγμα χρησιμοποιεί μια διαδρομή placeholder που πρέπει να αντικαταστήσετε.

```csharp
// Save the workbook as an .xlsx file
string outputPath = @"C:\Temp\KPI_Sparklines.xlsx";
workbook.Save(outputPath);
```

> **Επαλήθευση:** Ανοίξτε το παραγόμενο αρχείο στο Excel (ή σε οποιονδήποτε προβολέα που υποστηρίζει .xlsx). Θα πρέπει να δείτε μια **line sparkline** στο κελί **D2** που αντικατοπτρίζει την αύξηση των αριθμών πωλήσεων στη στήλη **B**. Με το ποντίκι πάνω στη sparkline θα εμφανιστεί ένα tooltip με τις υποκείμενες τιμές.

---

## Βήμα 5: Συνηθισμένα προβλήματα όταν **add sparkline to cell**

Ακόμη και ένα απλό παράδειγμα μπορεί να προκαλέσει προβλήματα σε νέους χρήστες. Εδώ είναι μερικά πράγματα στα οποία πρέπει να προσέξετε:

| Πρόβλημα | Γιατί συμβαίνει | Διόρθωση |
|----------|----------------|----------|
| Λάθος συντεταγμένες κελιού | Ο στόχος της sparkline χρησιμοποιεί δείκτη στήλης μηδενικής βάσης αλλά δείκτη γραμμής βάσης 1. | Θυμηθείτε `Cells[row, column]` όπου το `row` είναι μηδενικής βάσης, το `column` επίσης μηδενικής βάσης. Στο `SparklineGroup.Add`, οι γραμμές και στήλες είναι **βάσης 1**. |
| Δεν εμφανίζονται δεδομένα | Η περιοχή πηγής είναι κενή ή περιέχει μη‑αριθμητικές τιμές. | Βεβαιωθείτε ότι η περιοχή (π.χ., `B2:B13`) περιέχει αριθμούς. Χρησιμοποιήστε `PutValue` με αριθμητικούς τύπους. |
| Η sparkline εξαφανίζεται μετά την αποθήκευση | Ασυμφωνία έκδοσης βιβλιοθήκης ή έλλειψη άδειας. | Χρησιμοποιήστε την πιο πρόσφατη έκδοση του πακέτου Aspose.Cells και παρέχετε έγκυρη άδεια εάν έχετε υπερβεί τα όρια αξιολόγησης. |
| Η μορφοποίηση δεν εφαρμόζεται | Οι αλλαγές στυλ έγιναν πριν την προσθήκη της sparkline. | Ορίστε το στυλ **μετά** τη δημιουργία της ομάδας, όπως φαίνεται παραπάνω. |

---

## Πλήρης Κώδικας Πηγής – Αντιγραφή‑και‑επικόλληση σε ένα βήμα

Παρακάτω είναι το πλήρες, έτοιμο‑για‑εκτέλεση πρόγραμμα. Επικολλήστε το σε ένα νέο πρότζεκτ κονσόλας, προσθέστε το πακέτο NuGet Aspose.Cells, και πατήστε **F5**.

```csharp
using Aspose.Cells;
using System.Drawing;

namespace SparklineDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Create Excel workbook C#
            // -------------------------------------------------
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];
            worksheet.Name = "KPI";

            // -------------------------------------------------
            // Step 2: Populate monthly sales data (B2:B13)
            // -------------------------------------------------
            for (int month = 0; month < 12; month++)
            {
                worksheet.Cells[month + 1, 1].PutValue(5000 + month * 750);
            }

            // -------------------------------------------------
            // Step 3: Create line sparkline and add it to D2
            // -------------------------------------------------
            int groupIdx = worksheet.SparklineGroups.Add(SparklineType.Line);
            SparklineGroup sparklineGroup = worksheet.SparklineGroups[groupIdx];
            sparklineGroup.Add(1, 3, 1, 3, 1, 12); // D2 ↔ B2:B13

            // -------------------------------------------------
            // Step 4: Optional formatting (how to add sparkline with style)
            // -------------------------------------------------
            sparklineGroup.LineWeight = 1.0;
            sparklineGroup.SeriesColor = Color.DarkBlue;
            sparklineGroup.ShowMarkers = true;
            sparklineGroup.MarkerColor = Color.OrangeRed;

            // -------------------------------------------------
            // Step 5: Save the workbook
            // -------------------------------------------------
            string outputPath = @"C:\Temp\KPI_Sparklines.xlsx";
            workbook.Save(outputPath);

            System.Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

**Αναμενόμενο αποτέλεσμα:** Όταν ανοίξετε το *KPI_Sparklines.xlsx*, η στήλη **B** εμφανίζει δώδεκα αριθμούς (5.000 → 13.250) και το κελί **D2** περιέχει μια ομαλή σκούρα‑μπλε line sparkline που ανεβαίνει σταθερά. Τα markers εμφανίζονται ως μικροσκοπικά πορτοκαλο‑κόκκινα σημεία αν ενεργοποιήσατε το `ShowMarkers`.

---

## Τι Έρχεται Στη Σειρά; Επέκταση των Δεξιοτήτων σας με Sparkline

Τώρα που έχετε κατακτήσει το **create line sparkline** με το Aspose.Cells, σκεφτείτε να εξερευνήσετε τα παρακάτω συναφή θέματα:

- **Add column sparkline** – ιδανικό για εμφάνιση στοιβαγμένων δεδομένων.  
- **Create multi‑sparkline groups** στο ίδιο φύλλο για σύγκριση πλάι‑πλάι.  
- **Export to PDF** διατηρώντας τις sparklines (το Aspose.Cells υποστηρίζει μετατροπή σε PDF).  
- **Dynamic data sources** – αντλήστε πραγματικούς αριθμούς πωλήσεων από μια βάση δεδομένων SQL αντί για στατικές τιμές.  

Κάθε ένα από αυτά βασίζεται στις ίδιες βασικές έννοιες: **create Excel workbook C#**, συμπλήρωση δεδομένων, και **add sparkline to cell** στο επιθυμητό στυλ.

### TL;DR

Σας δείξαμε πώς να **create line sparkline** σε ένα βιβλίο εργασίας Excel χρησιμοποιώντας C#. Τα βήματα—*create workbook, fill data, add sparkline, style it, and save*—είναι όλα ενσωματωμένα σε ένα ενιαίο, αυτόνομο πρόγραμμα. Μπορείτε να προσαρμόσετε τα χρώματα, το πάχος της γραμμής ή την περιοχή πηγής ώστε να ταιριάζουν στις ανάγκες αναφοράς σας.

Έχετε μια παραλλαγή που θέλετε να μοιραστείτε; Αφήστε ένα σχόλιο παρακάτω, και καλή προγραμματιστική!

## Τι Θα Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Αυτοματοποίηση Excel: Δημιουργία Βιβλίου Εργασίας και Προσθήκη ListBox Χρησιμοποιώντας Aspose.Cells για .NET](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)
- [Αυτοματοποίηση Excel: Δημιουργία Βιβλίου Εργασίας και Προσθήκη ListBox Aspose Cells](/cells/german/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)
- [Αυτοματοποίηση Excel: Δημιουργία Βιβλίου Εργασίας και Προσθήκη ListBox Aspose Cells](/cells/french/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}