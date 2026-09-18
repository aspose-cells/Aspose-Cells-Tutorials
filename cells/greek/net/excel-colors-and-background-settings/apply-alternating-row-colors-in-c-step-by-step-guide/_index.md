---
category: general
date: 2026-03-18
description: Μάθετε πώς να εφαρμόζετε εναλλασσόμενα χρώματα γραμμών σε ένα φύλλο εργασίας
  χρησιμοποιώντας C#. Περιλαμβάνει ορισμό χρώματος φόντου γραμμής, προσθήκη ανοιχτόκίτρινο
  φόντο και χρωματισμό γραμμών εναλλασσόμενα.
draft: false
keywords:
- apply alternating row colors
- set row background color
- add light yellow background
- set alternating row shading
- color rows alternately
language: el
og_description: Εφαρμόστε εναλλασσόμενα χρώματα γραμμών σε C# για να βελτιώσετε την
  αναγνωσιμότητα. Αυτός ο οδηγός δείχνει πώς να ορίσετε το χρώμα φόντου της γραμμής,
  να προσθέσετε ανοιχτό κίτρινο φόντο και να χρωματίζετε τις γραμμές εναλλασσόμενα.
og_title: Εφαρμόστε Εναλλασσόμενα Χρώματα Γραμμών σε C# – Πλήρης Οδηγός
tags:
- C#
- DataTable
- Spreadsheet styling
- UI design
title: Εφαρμόστε εναλλασσόμενα χρώματα γραμμών σε C# – Οδηγός βήμα‑προς‑βήμα
url: /el/net/excel-colors-and-background-settings/apply-alternating-row-colors-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εφαρμογή Εναλλασσόμενων Χρωμάτων Γραμμών σε C# – Πλήρης Οδηγός

Έχετε ποτέ χρειαστεί να **εφαρμόσετε εναλλασσόμενα χρώματα γραμμών** σε ένα φύλλο εργασίας που τροφοδοτείται από δεδομένα, αλλά δεν ήξερες από πού να ξεκινήσεις; Δεν είστε ο μόνος — οι περισσότεροι προγραμματιστές αντιμετωπίζουν αυτό το πρόβλημα όταν προσπαθούν για πρώτη φορά να κάνουν τους πίνακες πιο φιλικούς. Τα καλά νέα; Με λίγες μόνο γραμμές C# μπορείτε να **ορίσετε το χρώμα φόντου της γραμμής**, να προσθέσετε ένα **απαλό κίτρινο φόντο**, και να καταλήξετε με ένα επαγγελματικό πλέγμα που βελτιώνει αμέσως την αναγνωσιμότητα.

Σε αυτόν τον οδηγό θα περάσουμε από όλη τη διαδικασία, από την ανάκτηση ενός `DataTable` στη μνήμη μέχρι το στυλ κάθε γραμμής με μια διακριτική κίτρινη‑λευκή λωρίδα. Στο τέλος θα μπορείτε να **χρωματίζετε εναλλασσόμενα τις γραμμές** με σιγουριά, και θα δείτε επίσης μερικές χρήσιμες παραλλαγές για όταν χρειάζεστε διαφορετικές αποχρώσεις ή δυναμική θεματοποίηση.

## Τι Θα Χρειαστεί

- Ένα .NET project που στοχεύει στο .NET 6 ή νεότερο (ο κώδικας λειτουργεί επίσης σε .NET Framework 4.7+).  
- Μια βιβλιοθήκη υπολογιστικών φύλλων που υποστηρίζει αντικείμενα στυλ – το παράδειγμα χρησιμοποιεί ένα γενικό API `Workbook`/`Worksheet` που αντικατοπτρίζει βιβλιοθήκες όπως **Aspose.Cells**, **GemBox.Spreadsheet**, ή **ClosedXML**.  
- Μια πηγή `DataTable` – μπορεί να προέρχεται από ερώτημα βάσης δεδομένων, εισαγωγή CSV, ή οποιαδήποτε συλλογή στη μνήμη.  

Δεν απαιτούνται επιπλέον πακέτα NuGet εκτός από τη βιβλιοθήκη υπολογιστικών φύλλων. Εάν χρησιμοποιείτε Aspose.Cells, το namespace είναι `Aspose.Cells`; για ClosedXML είναι `ClosedXML.Excel`. Αντικαταστήστε τις κλήσεις `CreateStyle` και `ImportDataTable` αναλόγως.

## Βήμα 1: Ανάκτηση των Πηγών Δεδομένων ως DataTable

Πρώτα απ' όλα—πάρτε τα δεδομένα που θέλετε να εμφανίσετε. Σε πραγματικές εφαρμογές αυτό συνήθως σημαίνει πρόσβαση σε βάση δεδομένων, αλλά για σαφήνεια θα δημιουργήσουμε μια βοηθητική μέθοδο που ονομάζεται `GetData()` και επιστρέφει ένα γεμάτο `DataTable`.

```csharp
// Step 1: Retrieve the source data as a DataTable
DataTable dataTable = GetData();   // Replace with your actual data retrieval logic
```

> **Γιατί είναι σημαντικό:** Το `DataTable` ορίζει τις γραμμές και τις στήλες που αργότερα θα λάβουν το εναλλασσόμενο σκίασμα. Αν ο πίνακας είναι κενός, δεν υπάρχει τίποτα για στυλιζάρισμα, επομένως πάντα ελέγξτε ότι `Rows.Count` > 0 πριν προχωρήσετε.

### Συμβουλή επαγγελματία
Εάν αντλείτε δεδομένα από Entity Framework, μπορείτε να χρησιμοποιήσετε `DataTable.Load(reader)` μετά την εκτέλεση ενός `SqlCommand`. Αυτό διατηρεί τον κώδικα καθαρό και αποφεύγει τον χειροκίνητο ορισμό στηλών.

## Βήμα 2: Κατανομή Πίνακα για Στυλ Καθεμίας Γραμμής

Στη συνέχεια, χρειαζόμαστε έναν container που ταιριάζει με τον αριθμό των γραμμών. Οι περισσότερες APIs υπολογιστικών φύλλων επιτρέπουν τη μεταβίβαση ενός πίνακα στυλ στη μέθοδο εισαγωγής, οπότε θα δημιουργήσουμε ένα `Style[]` ακριβώς στο μέγεθος του αριθμού γραμμών.

```csharp
// Step 2: Allocate an array to hold a style for each row
Style[] rowStyles = new Style[dataTable.Rows.Count];
```

> **Εξήγηση:** Προκαθορίζοντας τον πίνακα, αποφεύγουμε την επανεκχώρηση νέου αντικειμένου στυλ σε κάθε επανάληψη, κάτι που μπορεί να βελτιώσει την απόδοση όταν διαχειριζόμαστε χιλιάδες γραμμές.

## Βήμα 3: Εφαρμογή Εναλλασσόμενων Χρωμάτων Γραμμών (Απαλό Κίτρινο / Λευκό)

Τώρα έρχεται η ουσία: **εφαρμόστε εναλλασσόμενα χρώματα γραμμών**. Θα κάνουμε βρόχο σε κάθε γραμμή, θα δημιουργήσουμε μια νέα εμφάνιση στυλ από το workbook, και θα ορίσουμε το φόντο της βάσει του δείκτη γραμμής. Οι ζυγές γραμμές παίρνουν ένα απαλό κίτρινο γέμισμα, οι περιττές παραμένουν λευκές.

```csharp
// Step 3: Create alternating background colors (light yellow / white) for the rows
for (int rowIndex = 0; rowIndex < dataTable.Rows.Count; rowIndex++)
{
    // Create a new style instance from the workbook
    rowStyles[rowIndex] = wb.CreateStyle();

    // Apply a light yellow background to even rows, white to odd rows
    rowStyles[rowIndex].ForegroundColor = (rowIndex % 2 == 0)
        ? Color.LightYellow   // add light yellow background
        : Color.White;        // set row background color to white

    rowStyles[rowIndex].Pattern = BackgroundType.Solid; // set alternating row shading
}
```

### Γιατί λειτουργεί αυτό
- **`rowIndex % 2 == 0`** ελέγχει αν η γραμμή είναι ζυγή.  
- **`Color.LightYellow`** παρέχει μια ήπια, μη παρεμβατική απόχρωση που είναι ιδανική για πίνακες δεδομένων.  
- **`BackgroundType.Solid`** εξασφαλίζει ότι το γέμισμα καλύπτει ολόκληρο το κελί, επιτυγχάνοντας το εφέ **set row background color**.  

Μπορείτε να αντικαταστήσετε το `Color.LightYellow` με οποιαδήποτε άλλη απόχρωση (π.χ., `Color.LightCyan`) αν προτιμάτε διαφορετική εμφάνιση. Η ίδια λογική σας επιτρέπει επίσης να **χρωματίζετε εναλλασσόμενα τις γραμμές** βάσει άλλων κριτηρίων, όπως σημαίες κατάστασης.

## Βήμα 4: Εισαγωγή του DataTable στο Worksheet με τα Προετοιμασμένα Στυλ

Τέλος, μεταφέρουμε τα πάντα στο worksheet. Οι περισσότερες βιβλιοθήκες εκθέτουν μια υπερφόρτωση του `ImportDataTable` που δέχεται έναν πίνακα στυλ. Η σημαία `true` λέει στο API να γράψει τις επικεφαλίδες των στηλών, και οι συντεταγμένες `0, 0` ξεκινούν από το πάνω‑αριστερό κελί.

```csharp
// Step 4: Import the DataTable into the worksheet, applying the prepared row styles
ws.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);
```

> **Αποτέλεσμα:** Το worksheet εμφανίζει τώρα τα δεδομένα σας με ένα καθαρό μοτίβο **εναλλασσόμενου σκίασματος γραμμών** — απαλό κίτρινο στις ζυγές γραμμές, λευκό στις περιττές. Οι χρήστες μπορούν να διαβάσουν το πλέγμα χωρίς τα μάτια τους να πηδούν μπρος‑πίσω.

### Αναμενόμενο Αποτέλεσμα
Αν ανοίξετε το παραγόμενο λογιστικό φύλλο, θα δείτε κάτι σαν αυτό:

| ID | Name      | Quantity |
|----|-----------|----------|
| **1** | Apple      | 50       |
| **2** | Banana     | 30       |
| **3** | Cherry     | 20       |
| **4** | Date       | 15       |

Οι γραμμές 1, 3, 5… έχουν ένα **απαλό κίτρινο φόντο**, ενώ οι γραμμές 2, 4, 6… παραμένουν **λευκές**. Η γραμμή κεφαλίδας (γραμμή 0) κληρονομεί το προεπιλεγμένο στυλ εκτός αν το προσαρμόσετε ξεχωριστά.

## Προαιρετικές Παραλλαγές & Ακραίες Περιπτώσεις

### 1. Χρήση Διαφορετικής Παλέτας Χρωμάτων
Αν το απαλό κίτρινο συγκρούεται με το branding σας, απλώς αντικαταστήστε το `Color.LightYellow` με κάποιο άλλο `System.Drawing.Color`. Για ένα μπλε‑γκρι θέμα μπορείτε να χρησιμοποιήσετε:

```csharp
rowStyles[rowIndex].ForegroundColor = (rowIndex % 2 == 0)
    ? Color.FromArgb(220, 235, 247) // soft blue
    : Color.White;
```

### 2. Δυναμικό Σκίασμα Βάσει Δεδομένων
Μερικές φορές θέλετε να επισημάνετε γραμμές που πληρούν μια συνθήκη (π.χ., χαμηλό απόθεμα). Συνδυάστε τον έλεγχο modulo με ένα προσαρμοσμένο τεστ:

```csharp
int quantity = Convert.ToInt32(dataTable.Rows[rowIndex]["Quantity"]);
if (quantity < 20)
{
    rowStyles[rowIndex].ForegroundColor = Color.Salmon; // urgent low‑stock color
}
else
{
    rowStyles[rowIndex].ForegroundColor = (rowIndex % 2 == 0)
        ? Color.LightYellow
        : Color.White;
}
```

### 3. Εφαρμογή Στυλ μόνο σε Συγκεκριμένες Στήλες
Αν χρειάζεστε το **set row background color** μόνο σε ορισμένες στήλες, δημιουργήστε ξεχωριστό στυλ για κάθε στήλη και αναθέστε το μετά την εισαγωγή χρησιμοποιώντας το API περιοχής κελιών του worksheet.

```csharp
// Example for column B only
var colBStyle = wb.CreateStyle();
colBStyle.ForegroundColor = Color.LightYellow;
colBStyle.Pattern = BackgroundType.Solid;

// Apply after import
ws.Cells[$"B2:B{dataTable.Rows.Count + 1}"].SetStyle(colBStyle);
```

### 4. Συμβουλή Απόδοσης για Μεγάλους Πίνακες
Όταν διαχειρίζεστε > 10.000 γραμμές, σκεφτείτε να επαναχρησιμοποιήσετε ένα μόνο αντικείμενο στυλ για κάθε χρώμα αντί να δημιουργείτε νέο για κάθε γραμμή. Ο πίνακας τότε κρατά αναφορές στα δύο κοινά στυλ, μειώνοντας δραστικά τη χρήση μνήμης.

```csharp
Style yellowStyle = wb.CreateStyle();
yellowStyle.ForegroundColor = Color.LightYellow;
yellowStyle.Pattern = BackgroundType.Solid;

Style whiteStyle = wb.CreateStyle();
whiteStyle.ForegroundColor = Color.White;
whiteStyle.Pattern = BackgroundType.Solid;

for (int i = 0; i < dataTable.Rows.Count; i++)
    rowStyles[i] = (i % 2 == 0) ? yellowStyle : whiteStyle;
```

## Πλήρες Παράδειγμα Λειτουργίας

Παρακάτω υπάρχει ένα αυτόνομο πρόγραμμα που μπορείτε να επικολλήσετε σε μια εφαρμογή console. Χρησιμοποιεί ένα φανταστικό API `Workbook`/`Worksheet`; αντικαταστήστε τους τύπους με αυτούς από τη βιβλιοθήκη που έχετε επιλέξει.

```csharp
using System;
using System.Data;
using System.Drawing;          // For Color
using YourSpreadsheetLib;     // Replace with actual namespace

class Program
{
    static void Main()
    {
        // Initialize workbook & worksheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];

        // Step 1: Retrieve data
        DataTable dataTable = GetData();

        // Step 2: Allocate style array
        Style[] rowStyles = new Style[dataTable.Rows.Count];

        // Step 3: Apply alternating row colors
        for (int i = 0; i < dataTable.Rows.Count; i++)
        {
            rowStyles[i] = wb.CreateStyle();
            rowStyles[i].ForegroundColor = (i % 2 == 0)
                ? Color.LightYellow   // add light yellow background
                : Color.White;        // set row background color
            rowStyles[i].Pattern = BackgroundType.Solid; // set alternating row shading
        }

        // Step 4: Import with styles
        ws.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);

        // Save to file
        wb.Save("AlternatingRows.xlsx");
        Console.WriteLine("Workbook saved with alternating row colors.");
    }

    // Sample data generator
    static DataTable GetData()
    {
        var dt = new DataTable();
        dt.Columns.Add("ID", typeof(int));
        dt.Columns.Add("Product", typeof(string));
        dt.Columns.Add("Quantity", typeof(int));

        dt.Rows.Add(1, "Apple", 50);
        dt.Rows.Add(2, "Banana", 30);
        dt.Rows.Add(3, "Cherry", 20);
        dt.Rows.Add(4, "Date", 15);
        dt.Rows.Add(5, "Elderberry", 5);
        return dt;
    }
}
```

**Έξοδος:** Ένα αρχείο με όνομα `AlternatingRows.xlsx` όπου κάθε γραμμή εναλλάσσεται μεταξύ ενός απαλού κίτρινου γέμισης και λευκού, καθιστώντας τον πίνακα πιο ευανάγνωστο.

## Συχνές Ερωτήσεις

**Q: Λειτουργεί αυτή η προσέγγιση με τη μορφοποίηση υπό όρους τύπου Excel;**  
A: Ναι. Εάν η βιβλιοθήκη σας υποστηρίζει κανόνες υπό όρους, μπορείτε να μεταφράσετε την ίδια λογική σε έναν κανόνα που ελέγχει `MOD(ROW(),2)=0`. Η μέθοδος με κώδικα που παρουσιάζεται εδώ είναι πιο φορητή μεταξύ βιβλιοθηκών που δεν διαθέτουν ενσωματωμένη μορφοποίηση υπό όρους.

**Q: Τι γίνεται αν χρειαστεί να **χρωματίζετε εναλλασσόμενα τις γραμμές** σε έναν πίνακα PDF αντί για φύλλο Excel;**  
A: Οι περισσότεροι δημιουργοί πινάκων PDF (π.χ., iTextSharp, PdfSharp) επιτρέπουν τον ορισμό `BackgroundColor` ανά γραμμή. Η ίδια υπολογιστική modulo εφαρμόζεται—

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}