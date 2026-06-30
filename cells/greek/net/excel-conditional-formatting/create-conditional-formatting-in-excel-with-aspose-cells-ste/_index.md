---
category: general
date: 2026-06-30
description: Δημιουργήστε μορφοποίηση υπό όρους σε ένα βιβλίο εργασίας Excel χρησιμοποιώντας
  το Aspose.Cells. Μάθετε πώς να ορίζετε το φόντο των κελιών, να ταξινομείτε τα κελιά
  και να δημιουργείτε το αρχείο προγραμματιστικά.
draft: false
keywords:
- create conditional formatting
- create excel workbook
- set cell background
- how to rank cells
- how to use aspose
language: el
og_description: Δημιουργήστε μορφοποίηση υπό όρους σε ένα βιβλίο εργασίας Excel χρησιμοποιώντας
  το Aspose.Cells. Ακολουθήστε αυτό το πλήρες σεμινάριο για να ορίσετε το φόντο των
  κελιών, να ταξινομήσετε τα κελιά και να αυτοματοποιήσετε το Excel.
og_title: Δημιουργήστε Μορφοποίηση υπό Όρους στο Excel με το Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Create conditional formatting in an Excel workbook using Aspose.Cells.
    Learn how to set cell background, rank cells, and build the file programmatically.
  headline: Create Conditional Formatting in Excel with Aspose.Cells – Step‑by‑Step
    Guide
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Δημιουργία Μορφοποίησης υπό Συνθήκες στο Excel με το Aspose.Cells – Οδηγός
  βήμα‑βήμα
url: /el/net/excel-conditional-formatting/create-conditional-formatting-in-excel-with-aspose-cells-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία Μορφοποίησης Υπό Όρους στο Excel με το Aspose.Cells – Οδηγός Βήμα‑βήμα

Έχετε αναρωτηθεί ποτέ πώς να **δημιουργήσετε μορφοποίηση υπό όρους** σε ένα αρχείο Excel χωρίς να ανοίξετε το UI; Δεν είστε μόνοι. Πολλοί προγραμματιστές χρειάζονται να **δημιουργούν βιβλία εργασίας Excel** εν κινήσει, και η προγραμματιστική προσέγγιση εξοικονομεί ώρες χειροκίνητης εργασίας. Σε αυτό το tutorial θα σας δείξουμε ακριβώς πώς να **δημιουργήσετε μορφοποίηση υπό όρους**, να μορφοποιήσετε κελιά και ακόμη να κατατάξετε τις κορυφαίες τιμές—όλα με τη δυνατή βιβλιοθήκη Aspose.Cells για .NET.

Θα περάσουμε από ένα πραγματικό παράδειγμα: δημιουργία φύλλου βαθμολογίας, επισήμανση υψηλών βαθμών με ανοιχτό‑πράσινο χρώμα και τοποθέτηση χρυσού φόντου στους τρεις πρώτους επιδότες. Στο τέλος θα γνωρίζετε **πώς να ορίσετε το φόντο κελιού**, **πώς να κατατάξετε κελιά**, και **πώς να χρησιμοποιήσετε το Aspose** για εξελιγμένη αυτοματοποίηση Excel. Χωρίς περιττές πληροφορίες, μόνο μια πλήρης, εκτελέσιμη λύση που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο C#.

## Τι Θα Μάθετε

- Πώς να **δημιουργήσετε βιβλίο εργασίας excel** χρησιμοποιώντας το Aspose.Cells  
- Πώς να γεμίσετε μια περιοχή με τυχαία δεδομένα (βαθμολογίες)  
- Πώς να **ορίσετε το φόντο κελιού** με συμπαγή χρώματα  
- Πώς να εφαρμόσετε κανόνα βασισμένο σε τύπο για **κατάταξη κελιών** και να επισημάνετε τα τρία καλύτερα  
- Πώς να αποθηκεύσετε το αποτέλεσμα ως αρχείο .xlsx  

Απαιτήσεις: .NET 6+ (ή .NET Framework 4.6+), Visual Studio (ή οποιοδήποτε IDE C#), και μια αναφορά στο πακέτο NuGet Aspose.Cells. Αν δεν έχετε χρησιμοποιήσει ποτέ το Aspose, μην ανησυχείτε—θα καλύψουμε **πώς να χρησιμοποιήσετε το Aspose** από την αρχή.

![create conditional formatting example](https://example.com/images/create-conditional-formatting.png "Στιγμιότυπο οθόνης που δείχνει τη μορφοποίηση υπό όρους στο παραγόμενο αρχείο Excel")
*Image alt text: παράδειγμα δημιουργίας μορφοποίησης υπό όρους σε βιβλίο εργασίας Excel που δημιουργήθηκε με το Aspose.Cells.*

## Πώς να Δημιουργήσετε Βιβλίο Εργασίας Excel με το Aspose.Cells

Πρώτα απ' όλα: χρειάζεστε ένα αντικείμενο workbook για να εργαστείτε. Το Aspose.Cells το κάνει αυτό με μία γραμμή κώδικα.

```csharp
using Aspose.Cells;
using System.Drawing;

void CreateConditionalFormattingWorkbook()
{
    // Step 1: Instantiate a new workbook and give the first sheet a friendly name
    Workbook workbook = new Workbook();                 // creates an empty workbook
    Worksheet sheet = workbook.Worksheets[0];           // grab the default worksheet
    sheet.Name = "Scores";                              // rename it to something meaningful
```

Γιατί μετονομάζουμε το φύλλο; Ένα σαφές όνομα (όπως **Scores**) το καθιστά πιο εύκολο να αναφερθεί αργότερα, ειδικά όταν μοιράζεστε το αρχείο με μη‑τεχνικούς χρήστες.

Τώρα που υπάρχει το βιβλίο εργασίας, ας γεμίσουμε τη στήλη A με τυχαίες βαθμολογίες.

## Πώς να Συμπληρώσετε Δεδομένα – Δημιουργία Τυχαίων Βαθμολογιών

```csharp
    // Step 2: Populate A2:A21 with random values between 40 and 99
    Random random = new Random();
    for (int i = 0; i < 20; i++)               // 20 rows of data
    {
        sheet.Cells[i + 1, 0].PutValue(random.Next(40, 100));
    }
```

Μια γρήγορη σημείωση: η `PutValue` ανιχνεύει αυτόματα τον τύπο δεδομένων, έτσι δεν χρειάζεται να μετατρέψετε σε `int`. Η βρόχος ξεκινά από `i = 0` αλλά γράφει στη γραμμή `i + 1` επειδή οι γραμμές του Excel είναι 1‑based ενώ η συλλογή `Cells` είναι 0‑based.

## Πώς να Ορίσετε το Φόντο Κελιού για Υψηλές Βαθμολογίες

Τώρα θα **δημιουργήσουμε μορφοποίηση υπό όρους** που χρωματίζει οποιαδήποτε βαθμολογία ≥ 80 με ανοιχτό‑πράσινο χρώμα.

```csharp
    // Step 3: Define a conditional formatting range (A2:A21)
    int firstRow = 1, lastRow = 20;                     // zero‑based indices for rows 2‑21
    int cfIndex = sheet.ConditionalFormattings.Add(firstRow, 0, lastRow, 0);
    ConditionalFormatting cf = sheet.ConditionalFormattings[cfIndex];

    // Add a rule: cell value >= 80 → light‑green background
    FormatCondition highScoreCondition = cf.AddCondition(
        FormatConditionType.CellValue,
        OperatorType.GreaterOrEqual,
        "80");

    highScoreCondition.Style.ForegroundColor = Color.LightGreen;
    highScoreCondition.Style.Pattern = BackgroundType.Solid;
```

Η ιδιότητα `ForegroundColor` ελέγχει το χρώμα γεμίσματος, ενώ `Pattern = BackgroundType.Solid` λέει στο Excel να χρησιμοποιήσει συμπαγές γέμισμα αντί για διαβάθμιση ή μοτίβο. Αυτό είναι ο πυρήνας του **πώς να ορίσετε το φόντο κελιού** βάσει αριθμητικού ορίου.

## Πώς να Κατατάξετε Κελιά και να Επισημάνετε τα Πρώτα‑3

Η κατάταξη είναι λίγο πιο δύσκολη επειδή χρειάζεται ένας τύπος που αξιολογεί κάθε κελί σε σχέση με ολόκληρη την περιοχή. Το Aspose.Cells σας επιτρέπει να χρησιμοποιήσετε την ίδια σύνταξη τύπων του Excel που θα πληκτρολογούσατε στο UI.

```csharp
    // Step 4: Add a formula‑based rule to color the top‑3 scores gold
    FormatCondition topThreeCondition = cf.AddCondition(
        FormatConditionType.Formula,
        null,
        null);

    // The formula uses the RANK function; note the absolute references ($) lock the range
    topThreeCondition.Formula1 = "=RANK(A2,$A$2:$A$21)<=3";

    topThreeCondition.Style.ForegroundColor = Color.Gold;
    topThreeCondition.Style.Pattern = BackgroundType.Solid;
```

Γιατί το `A2` στον τύπο; Το Aspose αξιολογεί τον τύπο σχετικά με κάθε κελί στην περιοχή, έτσι το `A2` μετατοπίζεται αυτόματα σε `A3`, `A4`, κλπ., καθώς ο κανόνας εφαρμόζεται γραμμή‑με‑γραμμή. Η συνάρτηση `RANK` επιστρέφει τη θέση μιας τιμής μέσα στην καθορισμένη περιοχή, και το τμήμα `<=3` εξασφαλίζει ότι μόνο οι τρεις υψηλότερες βαθμολογίες λαμβάνουν το χρυσό γέμισμα.

## Πώς να Αποθηκεύσετε το Βιβλίο Εργασίας

```csharp
    // Step 5: Persist the workbook to disk
    workbook.Save("YOUR_DIRECTORY/Scores_ConditionalFormatting.xlsx");
}
```

Αντικαταστήστε το `YOUR_DIRECTORY` με μια απόλυτη ή σχετική διαδρομή στην οποία η εφαρμογή σας μπορεί να γράψει. Μετά την εκτέλεση της μεθόδου, ανοίξτε το αρχείο στο Excel και θα δείτε:

- Κελιά ανοιχτό‑πράσινα για οποιαδήποτε βαθμολογία ≥ 80  
- Κελιά χρυσά για τις τρεις υψηλότερες βαθμολογίες, ανεξάρτητα από το αν είναι επίσης ≥ 80  

Αυτή είναι η πλήρης αλυσίδα **δημιουργίας μορφοποίησης υπό όρους**.

---

## Πλήρες, Εκτελέσιμο Παράδειγμα

Ακολουθεί η πλήρης μέθοδος ξανά, έτοιμη για αντιγραφή‑επικόλληση σε μια εφαρμογή κονσόλας ή οποιαδήποτε κλάση C#:

```csharp
using Aspose.Cells;
using System.Drawing;

void CreateConditionalFormattingWorkbook()
{
    // Step 1: Create a new workbook and name the first worksheet
    Workbook workbook = new Workbook();
    Worksheet sheet = workbook.Worksheets[0];
    sheet.Name = "Scores";

    // Step 2: Fill column A (A2:A21) with random scores between 40 and 99
    Random random = new Random();
    for (int i = 0; i < 20; i++)
    {
        sheet.Cells[i + 1, 0].PutValue(random.Next(40, 100));
    }

    // Step 3: Highlight scores >= 80 with a light‑green background
    int firstRow = 1, lastRow = 20;
    int cfIndex = sheet.ConditionalFormattings.Add(firstRow, 0, lastRow, 0);
    ConditionalFormatting cf = sheet.ConditionalFormattings[cfIndex];
    FormatCondition highScoreCondition = cf.AddCondition(
        FormatConditionType.CellValue,
        OperatorType.GreaterOrEqual,
        "80");
    highScoreCondition.Style.ForegroundColor = Color.LightGreen;
    highScoreCondition.Style.Pattern = BackgroundType.Solid;

    // Step 4: Color the top‑3 scores with a gold background using a formula rule
    FormatCondition topThreeCondition = cf.AddCondition(
        FormatConditionType.Formula,
        null,
        null);
    topThreeCondition.Formula1 = "=RANK(A2,$A$2:$A$21)<=3";
    topThreeCondition.Style.ForegroundColor = Color.Gold;
    topThreeCondition.Style.Pattern = BackgroundType.Solid;

    // Step 5: Save the workbook
    workbook.Save("YOUR_DIRECTORY/Scores_ConditionalFormatting.xlsx");
}
```

### Αναμενόμενο Αποτέλεσμα

Όταν ανοίξετε το `Scores_ConditionalFormatting.xlsx`:

- Κελιά με τιμές **80** ή μεγαλύτερες λάμπουν ανοιχτό‑πράσινα.  
- Οι τρεις υψηλότεροι αριθμοί (ακόμη και αν είναι κάτω από 80) εμφανίζονται με φόντο **χρυσό**.  
- Όλα τα άλλα κελιά διατηρούν το προεπιλεγμένο λευκό φόντο.

Αυτή η οπτική ένδειξη ενημερώνει αμέσως έναν διαχειριστή ποιοι είναι οι κορυφαίοι επιδότες, χωρίς καμία χειροκίνητη ταξινόμηση.

---

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

**Τι γίνεται αν χρειάζομαι περισσότερους από τρεις κορυφαίους βαθμούς;**  
Απλώς αλλάξτε το τμήμα `<=3` του τύπου σε `<=5` (ή οποιονδήποτε αριθμό θέλετε). Ο κανόνας θα προσαρμοστεί αυτόματα.

**Μπορώ να εφαρμόσω πολλαπλές περιοχές μορφοποίησης;**  
Απόλυτα. Καλέστε ξανά το `sheet.ConditionalFormattings.Add` με διαφορετική περιοχή, και στη συνέχεια προσθέστε συνθήκες σε αυτό το νέο αντικείμενο `ConditionalFormatting`.

**Τι γίνεται με παλαιότερες εκδόσεις του Excel;**  
Το Aspose.Cells αποθηκεύει εξ ορισμού σε μορφή `.xlsx`, η οποία είναι συμβατή με το Excel 2007 και μεταγενέστερα. Αν χρειάζεστε `.xls`, περάστε το `SaveFormat.Excel97To2003` στη μέθοδο `Save`.

**Υπάρχει επίπτωση στην απόδοση για μεγάλα φύλλα;**  
Η μορφοποίηση υπό όρους αποθηκεύεται ως μεταδεδομένα, έτσι δεν επηρεάζει σημαντικά το μέγεθος του αρχείου. Ωστόσο, η δημιουργία εκατοντάδων χιλιάδων γραμμών μπορεί να αυξήσει τη χρήση μνήμης—σκεφτείτε την επεξεργασία σε παρτίδες.

---

## Επόμενα Βήματα

Τώρα που έχετε κατακτήσει **πώς να δημιουργήσετε μορφοποίηση υπό όρους**, ίσως θέλετε να εξερευνήσετε:

- **Πώς να δημιουργήσετε γραφήματα Excel** προγραμματιστικά (ένα ακόμη διαμάντι του Aspose.Cells)  
- **Πώς να ορίσετε το φόντο κελιού** βάσει κειμενικών τιμών (π.χ., “Pass/Fail”)  
- **Πώς να χρησιμοποιήσετε το Aspose.Cells για επικύρωση δεδομένων** και λίστες επιλογής  

Κάθε ένα από αυτά τα θέματα βασίζεται στα ίδια θεμέλια που μόλις μάθατε, έτσι θα νιώσετε άνετα.

---

## Συμπέρασμα

Μόλις περάσαμε από ένα πλήρες, ολοκληρωμένο παράδειγμα του πώς να **δημιουργήσετε μορφοποίηση υπό όρους** σε ένα βιβλίο εργασίας Excel χρησιμοποιώντας το Aspose.Cells. Από την αρχικοποίηση του βιβλίου εργασίας, τη συμπλήρωση δεδομένων, **τον ορισμό του φόντου κελιού**, την κατάταξη των κορυφαίων επιδότων, μέχρι την τελική αποθήκευση του αρχείου, κάθε βήμα καλύφθηκε με έμφαση τόσο στο **πώς να κατατάξετε κελιά** όσο και στο **πώς να χρησιμοποιήσετε το Aspose**.  

Δοκιμάστε τον κώδικα, προσαρμόστε τα όρια, και δείτε πόσο γρήγορα μπορείτε να δημιουργήσετε επαγγελματικές αναφορές για οποιοδήποτε επιχειρηματικό σενάριο. Έχετε μια παραλλαγή που θέλετε να μοιραστείτε; Αφήστε ένα σχόλιο παρακάτω—καλή προγραμματιστική!

## Τι Θα Πρέπει Να Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Αυτοματοποιήστε τη Μορφοποίηση Υπό Όρους του Excel χρησιμοποιώντας το Aspose.Cells για Java: Ένας Πλήρης Οδηγός](/cells/english/java/formatting/automate-conditional-formatting-excel-aspose-cells-java/)
- [Πώς να Δημιουργήσετε & Μορφοποιήσετε Κελιά Excel χρησιμοποιώντας το Aspose.Cells για Java: Οδηγός Βήμα‑βήμα](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)
- [Δημιουργήστε ένα Βιβλίο Εργασίας Excel χρησιμοποιώντας το Aspose.Cells σε Java: Οδηγός Βήμα‑βήμα](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}