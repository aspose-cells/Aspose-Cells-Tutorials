---
category: general
date: 2026-03-21
description: Δημιουργήστε βιβλίο εργασίας Excel και εισάγετε πίνακα δεδομένων στο
  Excel ορίζοντας το στυλ της στήλης, εξάγετε τα δεδομένα στο Excel και μορφοποιήστε
  την ημερομηνία των κελιών του Excel σε λεπτά.
draft: false
keywords:
- create excel workbook
- import datatable to excel
- set column style
- export data to excel
- format excel cells date
language: el
og_description: Δημιουργήστε γρήγορα ένα βιβλίο εργασίας Excel. Μάθετε να εισάγετε
  πίνακα δεδομένων στο Excel, να ορίσετε το στυλ στήλης, να εξάγετε δεδομένα στο Excel
  και να μορφοποιήσετε τις ημερομηνίες των κελιών του Excel σε έναν οδηγό.
og_title: Δημιουργία βιβλίου εργασίας Excel – Πλήρης οδηγός για το στυλ και την εξαγωγή
tags:
- C#
- Aspose.Cells
- Excel automation
title: Δημιουργία βιβλίου εργασίας Excel με μορφοποιημένο πίνακα – Οδηγός βήμα‑βήμα
url: /el/net/excel-workbook/create-excel-workbook-with-styled-table-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία Excel Workbook – Πλήρης Προγραμματιστική Εκπαίδευση

Κάποτε χρειάστηκε να **δημιουργήσετε excel workbook** που να φαίνεται επαγγελματικό κατευθείαν από τον κώδικα; Ίσως αντλείτε δεδομένα από μια βάση και θέλετε οι ημερομηνίες να εμφανίζονται στη σωστή μορφή χωρίς να παίζετε με το Excel αργότερα. Αυτό είναι ένα συχνό πρόβλημα—ειδικά όταν το αποτέλεσμα φτάνει στο inbox ενός πελάτη και αυτός αναμένει ότι όλα είναι έτοιμα προς χρήση.

Σε αυτόν τον οδηγό θα περάσουμε βήμα‑βήμα από μια αυτόνομη λύση που **εισάγει datatable σε excel**, εφαρμόζει **ρυθμίζει στυλ στήλης**, και τέλος **εξάγει δεδομένα σε excel** ως ένα ωραία μορφοποιημένο αρχείο. Θα δείτε ακριβώς πώς να **μορφοποιήσετε excel cells date** ώστε το φύλλο να διαβάζεται σαν επαγγελματική αναφορά, και θα λάβετε ένα πλήρες, εκτελέσιμο παράδειγμα στο τέλος. Χωρίς ελλείψεις, χωρίς “δείτε την τεκμηρίωση” συντομεύσεις—απλώς καθαρός κώδικας που μπορείτε να ενσωματώσετε στο πρότζεκτ σας σήμερα.

---

## Τι Θα Μάθετε

- Πώς να **δημιουργήσετε excel workbook** χρησιμοποιώντας τη βιβλιοθήκη Aspose.Cells (ή οποιοδήποτε συμβατό API).
- Τον πιο γρήγορο τρόπο για **εισαγωγή datatable σε excel** χωρίς χειροκίνητους βρόχους κελιού‑κατά‑κελί.
- Τεχνικές για **ρύθμιση στυλ στήλης**, συμπεριλαμβανομένης της εφαρμογής μορφής ημερομηνίας σε συγκεκριμένη στήλη.
- Πώς να **εξάγετε δεδομένα σε excel** με μία κλήση `Save`.
- Συνηθισμένα λάθη όταν προσπαθείτε να **μορφοποιήσετε excel cells date** και πώς να τα αποφύγετε.

### Προαπαιτούμενα

- .NET 6+ (ή .NET Framework 4.6+).  
- Aspose.Cells for .NET εγκατεστημένο (`Install-Package Aspose.Cells`).  
- Ένα `DataTable` έτοιμο για εξαγωγή—η πηγή δεδομένων σας μπορεί να είναι SQL, CSV ή οτιδήποτε μπορεί να μετατραπεί σε `DataTable`.

Αν είστε ήδη άνετοι με τη C# και έχετε αυτά τα στοιχεία στη θέση τους, είστε έτοιμοι. Διαφορετικά, η ενότητα “Προαπαιτούμενα” παραπάνω σας δίνει μια γρήγορη λίστα ελέγχου.

---

## Βήμα 1 – Δημιουργία του Αντικειμένου Excel Workbook

Το πρώτο πράγμα που κάνετε όταν θέλετε να **δημιουργήσετε excel workbook** προγραμματιστικά είναι να δημιουργήσετε το αντικείμενο workbook. Σκεφτείτε το σαν το άνοιγμα ενός κεντρικού σημειωματάριου όπου θα γράψετε τα δεδομένα σας.

```csharp
using Aspose.Cells;
using System.Data;

// Step 1: Create a new workbook (or load an existing one)
Workbook workbook = new Workbook();
```

> **Γιατί είναι σημαντικό:**  
> Η κλάση `Workbook` είναι το σημείο εισόδου για κάθε λειτουργία στο Aspose.Cells. Η δημιουργία της από την αρχή σας δίνει έναν καθαρό καμβά, και μπορείτε αργότερα να φορτώσετε ένα υπάρχον αρχείο αν χρειαστεί να προσθέσετε δεδομένα αντί να ξεκινήσετε από το μηδέν.

---

## Βήμα 2 – Προετοιμασία του DataTable για Εισαγωγή

Πριν μπορέσουμε να **εισάγουμε datatable σε excel**, χρειαζόμαστε ένα `DataTable`. Σε πραγματικά έργα αυτό συχνά προέρχεται από `SqlDataAdapter.Fill` ή `DataTable.Load`. Για λόγους σαφήνειας θα δημιουργήσουμε μια μέθοδο που επιστρέφει έναν έτοιμο πίνακα.

```csharp
// Step 2: Obtain the data to be written – a DataTable with three columns
DataTable dataTable = GetData();   // assume GetData() returns the required table

// Example implementation (you can replace this with your own data source)
DataTable GetData()
{
    DataTable dt = new DataTable();
    dt.Columns.Add("OrderDate", typeof(DateTime));
    dt.Columns.Add("Product", typeof(string));
    dt.Columns.Add("Quantity", typeof(int));

    dt.Rows.Add(DateTime.Today.AddDays(-2), "Apples", 120);
    dt.Rows.Add(DateTime.Today.AddDays(-1), "Bananas", 85);
    dt.Rows.Add(DateTime.Today, "Cherries", 60);
    return dt;
}
```

> **Συμβουλή:** Αν οι ημερομηνίες σας είναι αποθηκευμένες ως συμβολοσειρές, μετατρέψτε τις σε `DateTime` πρώτα—διαφορετικά το βήμα **μορφοποίησης excel cells date** δεν θα λειτουργήσει όπως αναμένεται.

---

## Βήμα 3 – Ορισμός Στυλ για Κάθε Στήλη (Set Column Style)

Τώρα ήρθε η στιγμή να **ρυθμίσουμε στυλ στήλης**. Θα δημιουργήσουμε έναν πίνακα αντικειμένων `Style`—ένα για κάθε στήλη. Η πρώτη στήλη παίρνει μια ενσωματωμένη μορφή ημερομηνίας (κώδικας 14), ενώ οι άλλες παραμένουν στη γενική μορφή (κώδικας 0).

```csharp
// Step 3: Define a style for each column; apply a date format to the first column
Style[] columnStyles = new Style[3];
for (int i = 0; i < columnStyles.Length; i++)
{
    columnStyles[i] = workbook.CreateStyle();
    columnStyles[i].Number = (i == 0) ? 14 : 0;   // 14 = date format, 0 = general
}
```

> **Γιατί να χρησιμοποιήσετε αντικείμενα στυλ;**  
> Η εφαρμογή ενός στυλ μία φορά και η επαναχρησιμοποίησή του είναι πολύ πιο αποδοτική από το να ορίζετε τη μορφή σε κάθε κελί ξεχωριστά. Επίσης εγγυάται ότι ολόκληρη η στήλη τηρεί τον ίδιο κανόνα **μορφοποίησης excel cells date**, κάτι που είναι κρίσιμο για συνέπεια όταν το αρχείο ανοίγει σε διαφορετικές τοπικές ρυθμίσεις.

---

## Βήμα 4 – Εισαγωγή του DataTable με Στυλ στο Worksheet

Με το workbook έτοιμο και τα στυλ ορισμένα, τώρα **εισάγουμε datatable σε excel**. Η μέθοδος `ImportDataTable` κάνει το βαριά δουλειά: γράφει τις επικεφαλίδες των στηλών, τις γραμμές, και εφαρμόζει τα στυλ που περάσαμε.

```csharp
// Step 4: Access the first worksheet and import the DataTable using the styles
Worksheet worksheet = workbook.Worksheets[0];
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
```

> **Τι συμβαίνει στο παρασκήνιο;**  
> - `true` λέει στο Aspose.Cells να συμπεριλάβει τα ονόματα των στηλών ως πρώτη γραμμή.  
> - `0, 0` είναι οι δείκτες εκκίνησης γραμμής και στήλης (πάνω‑αριστερή γωνία).  
> - `columnStyles` ευθυγραμμίζει κάθε στήλη με το στυλ που προετοιμάσαμε, εξασφαλίζοντας ότι ο κανόνας **μορφοποίησης excel cells date** εφαρμόζεται στη στήλη ημερομηνίας.

---

## Βήμα 5 – Αποθήκευση (Εξαγωγή) του Workbook σε Φυσικό Αρχείο

Τέλος, **εξάγουμε δεδομένα σε excel** αποθηκεύοντας το workbook στο δίσκο. Μπορείτε να αλλάξετε τη διαδρομή σε οποιονδήποτε φάκελο θέλετε, ή ακόμη και να στείλετε το αρχείο απευθείας ως απόκριση HTTP για ένα web API.

```csharp
// Step 5: Save the workbook with the styled table
workbook.Save("YOUR_DIRECTORY/StyledTable.xlsx");
```

> **Pro tip:** Χρησιμοποιήστε `workbook.Save(Stream, SaveFormat.Xlsx)` όταν χρειάζεται να στείλετε το αρχείο μέσω δικτύου χωρίς να το γράψετε στο δίσκο.

---

## Πλήρες Παράδειγμα Εργασίας (Όλα τα Βήματα Συνδυασμένα)

Παρακάτω είναι το πλήρες, έτοιμο‑για‑εκτέλεση πρόγραμμα. Αντιγράψτε‑και‑επικολλήστε το σε μια εφαρμογή console, προσαρμόστε τη διαδρομή εξόδου, και θα έχετε ένα ωραία μορφοποιημένο αρχείο Excel σε δευτερόλεπτα.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class Program
{
    static void Main()
    {
        // 1️⃣ Create the workbook
        Workbook workbook = new Workbook();

        // 2️⃣ Get the data (replace GetData with your own source if needed)
        DataTable dataTable = GetData();

        // 3️⃣ Prepare column styles – date format for the first column
        Style[] columnStyles = new Style[3];
        for (int i = 0; i < columnStyles.Length; i++)
        {
            columnStyles[i] = workbook.CreateStyle();
            columnStyles[i].Number = (i == 0) ? 14 : 0;   // 14 = date, 0 = general
        }

        // 4️⃣ Import the DataTable with the styles
        Worksheet worksheet = workbook.Worksheets[0];
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

        // 5️⃣ Save the file
        workbook.Save("StyledTable.xlsx");

        Console.WriteLine("Excel workbook created successfully!");
    }

    // Sample data generator – replace with real data source
    static DataTable GetData()
    {
        DataTable dt = new DataTable();
        dt.Columns.Add("OrderDate", typeof(DateTime));
        dt.Columns.Add("Product", typeof(string));
        dt.Columns.Add("Quantity", typeof(int));

        dt.Rows.Add(DateTime.Today.AddDays(-2), "Apples", 120);
        dt.Rows.Add(DateTime.Today.AddDays(-1), "Bananas", 85);
        dt.Rows.Add(DateTime.Today, "Cherries", 60);
        return dt;
    }
}
```

**Αναμενόμενη έξοδος:**  
Όταν ανοίξετε το `StyledTable.xlsx`, η στήλη A δείχνει ημερομηνίες όπως `03/19/2026` (ανάλογα με την τοπική ρύθμιση), ενώ οι στήλες B και C εμφανίζουν τα ονόματα προϊόντων και τις ποσότητες ως απλό κείμενο/αριθμούς. Δεν απαιτούνται επιπλέον βήματα μορφοποίησης—η διαδικασία **δημιουργίας excel workbook** ολοκληρώθηκε.

---

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

### 1️⃣ Τι γίνεται αν το DataTable μου έχει περισσότερες από τρεις στήλες;
Προσθέστε περισσότερα αντικείμενα `Style` στον πίνακα `columnStyles` και προσαρμόστε την ιδιότητα `Number` για κάθε στήλη που χρειάζεται ειδική μορφή (π.χ. νόμισμα, ποσοστά). Η μέθοδος `ImportDataTable` θα ταιριάξει κάθε στυλ με τη θέση του.

### 2️⃣ Μπορώ να εφαρμόσω προσαρμοσμένη μορφή ημερομηνίας αντί του ενσωματωμένου 14;
Απολύτως. Αντικαταστήστε το `columnStyles[i].Number = 14;` με:

```csharp
columnStyles[i].Number = 22;               // built‑in custom format ID
columnStyles[i].Custom = "dd‑MMM‑yyyy";    // or any .NET date pattern you like
```

### 3️⃣ Πώς **εξάγω δεδομένα σε excel** σε ένα web API χωρίς να γράψω στο δίσκο;
Χρησιμοποιήστε ένα `MemoryStream`:

```csharp
using (var ms = new MemoryStream())
{
    workbook.Save(ms, SaveFormat.Xlsx);
    ms.Position = 0;
    // return File(ms.ToArray(), "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet", "Report.xlsx");
}
```

### 4️⃣ Τι γίνεται αν η τοπική ρύθμιση του χρήστη απαιτεί διαφορετικό διαχωριστικό ημερομηνίας;
Η ενσωματωμένη μορφή ημερομηνίας (ID 14) σέβεται τις ρυθμίσεις τοπικότητας του workbook. Αν χρειάζεστε σταθερή μορφή ανεξάρτητα από την τοπική ρύθμιση, χρησιμοποιήστε την ιδιότητα `Custom` όπως φαίνεται παραπάνω.

### 5️⃣ Λειτουργεί αυτό με .NET Core;
Ναι—το Aspose.Cells υποστηρίζει .NET Standard 2.0 και νεότερα, οπότε ο ίδιος κώδικας τρέχει σε .NET 6, .NET 7 ή οποιοδήποτε συμβατό runtime.

---

## Συμβουλές Καλών Πρακτικών (Pro Tips)

- **Επαναχρησιμοποίηση στυλ**: Η δημιουργία ενός στυλ ανά στήλη είναι φθηνή, αλλά η χρήση του ίδιου αντικειμένου στυλ για παρόμοιες στήλες εξοικονομεί μνήμη.
- **Αποφύγετε βρόχους κελιού‑κατά‑κελί**: Η `ImportDataTable` είναι εξαιρετικά βελτιστοποιημένη· οι χειροκίνητοι βρόχοι είναι πιο αργοί και επιρρεπείς σε σφάλματα.
- **Ορίστε την πολιτισμική ρύθμιση του workbook νωρίς** αν χρειάζεστε συνεπείς διαχωριστές αριθμών/ημερομηνιών σε όλα τα περιβάλλοντα:

```csharp
workbook.Settings.CultureInfo = new System.Globalization.CultureInfo("en-US");
```

- **Επικυρώστε το DataTable** πριν την εισαγωγή—μηδενικές ημερομηνίες θα προκαλέσουν εξαίρεση όταν εφαρμόζεται το στυλ ημερομηνίας.
- **Ενεργοποιήστε τον υπολογισμό** αν προσθέσετε τύπους μετά την εισαγωγή:

```csharp
workbook.CalculateFormula();
```

---

## Συμπέρασμα

Τώρα έχετε μια πλήρη, άκρη‑σε‑άκρη συνταγή για **δημιουργία excel workbook**, **εισαγωγή datatable σε excel**, **ρύθμιση στυλ στήλης**, **εξαγωγή δεδομένων σε excel**, και **μορφοποίηση excel cells date**—όλα σε λιγότερο από μια δέκα γραμμές κώδικα C#. Η προσέγγιση είναι γρήγορη, αξιόπιστη και κρατά τις ανησυχίες μορφοποίησης μέσα στον κώδικα, ώστε το τελικό φύλλο να είναι έτοιμο για τους επιχειρηματικούς χρήστες τη στιγμή που το ανοίγουν.

Έτοιμοι για την επόμενη πρόκληση; Δοκιμάστε να προσθέσετε conditional formatting, να ενσωματώσετε γραφήματα, ή να μετατρέψετε το

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}