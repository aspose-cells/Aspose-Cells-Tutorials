---
category: general
date: 2026-09-21
description: Διαμορφώστε το SmartMarkerOptions ArrayAsSingle σε C# για να εξάγετε
  τους πίνακες JSON ως μία μόνο τιμή κελιού σε ένα βιβλίο εργασίας Excel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- configure smartmarkeroptions arrayassingle
- Aspose.Cells smart markers
- export JSON array
- C# DataTable
- Workbook ProcessSmartMarkers
language: el
lastmod: 2026-09-21
og_description: Διαμορφώστε το SmartMarkerOptions ArrayAsSingle σε C# για να εξάγετε
  πίνακες JSON ως μία τιμή κελιού. Μάθετε τη πλήρη βήμα‑βήμα λύση.
og_image_alt: Screenshot of an Excel sheet showing a JSON array stored in a single
  cell after using SmartMarkerOptions
og_title: Διαμόρφωση SmartMarkerOptions ArrayAsSingle σε C# – πλήρης οδηγός
schemas:
- author: Aspose
  dateModified: '2026-09-21'
  description: Configure SmartMarkerOptions ArrayAsSingle in C# to export JSON arrays
    as a single cell value in an Excel workbook.
  headline: Configure SmartMarkerOptions ArrayAsSingle in C# for JSON arrays
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Διαμόρφωση SmartMarkerOptions ArrayAsSingle σε C# για πίνακες JSON
url: /el/net/smart-markers-dynamic-data/configure-smartmarkeroptions-arrayassingle-in-c-for-json-arr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Διαμόρφωση SmartMarkerOptions ArrayAsSingle σε C# για JSON πίνακες

Αν χρειάζεστε να **configure SmartMarkerOptions ArrayAsSingle** κατά τη δημιουργία αρχείων Excel με Aspose.Cells, αυτός ο οδηγός σας δείχνει ακριβώς πώς να το κάνετε. Θα δείτε πώς να διατηρήσετε έναν JSON πίνακα αμετάβλητο σε ένα κελί αντί να διασπείρετε τα στοιχεία του σε πολλές γραμμές.

Η εργασία με δεδομένα JSON σε υπολογιστικά φύλλα συχνά σημαίνει επιλογή μεταξύ μιας επίπεδης προβολής και μιας συμπαγούς αναπαράστασης. Σε πολλές περιπτώσεις αναφοράς—όπως η αποθήκευση λίστας ετικετών ή συνόλου αναγνωριστικών—θέλετε ολόκληρη τη συμβολοσειρά JSON να παραμένει σε ένα μόνο κελί. Η σημαία **ArrayAsSingle** στο `SmartMarkerOptions` το καθιστά δυνατό.

Σε αυτό το tutorial θα:

* Δημιουργήσετε ένα `DataTable` που περιέχει έναν JSON πίνακα σε μια στήλη.
* Τοποθετήσετε Smart Markers σε ένα φύλλο Excel.
* **Configure SmartMarkerOptions ArrayAsSingle** ώστε ο JSON πίνακας να αντιμετωπίζεται ως τιμή ενός μόνο κελιού.
* Επεξεργαστείτε τα markers και αποθηκεύσετε το βιβλίο εργασίας.
* Επαληθεύσετε το αποτέλεσμα.

> **Prerequisites** – Χρειάζεστε τη βιβλιοθήκη Aspose.Cells for .NET (v23.12 ή νεότερη) και ένα περιβάλλον ανάπτυξης .NET (συνιστάται Visual Studio 2022). Θεωρείται βασική γνώση C# και DataTables.

---

## Step 1: Prepare the data source with a JSON array

Πρώτα, δημιουργήστε ένα `DataTable` που προσομοιώνει τα δεδομένα που θα λάβετε από μια υπηρεσία ή μια βάση δεδομένων. Η στήλη **Names** περιέχει μια συμβολοσειρά κωδικοποιημένη σε JSON που αντιπροσωπεύει έναν πίνακα ονομάτων.

```csharp
using System;
using System.Data;
using Aspose.Cells;

DataTable dataTable = new DataTable();
dataTable.Columns.Add("Id", typeof(int));
dataTable.Columns.Add("Names", typeof(string));

// Store the JSON array as a plain string
dataTable.Rows.Add(1, "[\"Alice\",\"Bob\"]");
```

*Γιατί αυτό το βήμα;*  
Τα Smart Markers διαβάζουν δεδομένα απευθείας από αντικείμενα .NET. Τοποθετώντας τον JSON πίνακα σε μια στήλη τύπου string, διατηρείτε την ακριβή σύνταξη JSON, η οποία αργότερα μπορεί να γραφτεί σε κελί αμετάβλητη.

---

## Step 2: Insert Smart Markers into a new workbook

Δημιουργήστε ένα νέο βιβλίο εργασίας, επιλέξτε το πρώτο φύλλο και γράψτε Smart Markers που αναφέρονται σε ολόκληρο τον πίνακα και στη συγκεκριμένη στήλη **Names**.

```csharp
// Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];

// Smart marker for the entire table (optional, shown for completeness)
worksheet.Cells["A1"].PutValue("&=dataTable");

// Smart marker that targets only the Names column
worksheet.Cells["A2"].PutValue("&=dataTable.Names");
```

Το marker `&=dataTable.Names` λέει στο Aspose.Cells να αντικαταστήσει το κελί με την τιμή της στήλης **Names** για κάθε γραμμή του `dataTable`. Επειδή έχουμε μόνο μία γραμμή, το marker θα επεξεργαστεί μία φορά.

---

## Step 3: **Configure SmartMarkerOptions ArrayAsSingle**

Από προεπιλογή, το Aspose.Cells επεκτείνει μια συμβολοσειρά που μοιάζει με πίνακα σε ξεχωριστές γραμμές. Ορίζοντας το `ArrayAsSingle` σε `true` παρακάμπτει αυτή τη συμπεριφορά, εξαναγκάζοντας ολόκληρη τη συμβολοσειρά JSON να παραμείνει σε ένα μόνο κελί.

```csharp
SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
{
    // Export the JSON array as a single cell value
    ArrayAsSingle = true
};
```

*Γιατί να ενεργοποιήσετε το `ArrayAsSingle`;*  
Όταν το `ArrayAsSingle` είναι `false`, η μηχανή ερμηνεύει το `["Alice","Bob"]` ως δύο ξεχωριστές τιμές και τις γράφει σε διαδοχικές γραμμές. Ορίζοντάς το σε `true` η συμβολοσειρά αντιμετωπίζεται ως ατομική τιμή, κάτι που είναι απαραίτητο για τη διατήρηση της μορφής JSON μέσα στο Excel.

---

## Step 4: Process the Smart Markers with the configured options

Τώρα εκτελέστε τη μηχανή Smart Marker, περνώντας το αντικείμενο επιλογών που μόλις διαμορφώσατε.

```csharp
// Process smart markers using the custom options
workbook.ProcessSmartMarkers(smartMarkerOptions);
```

Κατά τη διάρκεια της επεξεργασίας, το Aspose.Cells διαβάζει το `dataTable`, εφαρμόζει τα markers και σέβεται τη σημαία `ArrayAsSingle`, αφήνοντας τον JSON πίνακα άθικτο.

---

## Step 5: Save the workbook and verify the result

Τέλος, γράψτε το βιβλίο εργασίας στο δίσκο. Ανοίξτε το παραγόμενο αρχείο στο Excel ή σε οποιονδήποτε προβολέα υπολογιστικών φύλλων για να επιβεβαιώσετε ότι το κελί **A2** περιέχει ακριβώς τη συμβολοσειρά JSON.

```csharp
// Save the resulting workbook
string outputPath = @"C:\Temp\SmartMarkerJson.xlsx";
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

### Expected output

| A   |
|-----|
| **["Alice","Bob"]** |

Το κελί **A2** εμφανίζει τον JSON πίνακα ως μια ενιαία τιμή κειμένου, ακριβώς όπως αποθηκεύτηκε στο `DataTable`. Δεν δημιουργούνται επιπλέον γραμμές.

---

## Common variations and edge‑case handling

| Situation | How to adapt |
|-----------|--------------|
| **Multiple rows with JSON arrays** | Η ίδια ρύθμιση `ArrayAsSingle` λειτουργεί· ο JSON πίνακας κάθε γραμμής παραμένει στο δικό του κελί. |
| **Different JSON structures (objects, nested arrays)** | Εφόσον το JSON είναι συμβολοσειρά, το `ArrayAsSingle` θα το κρατήσει αμετάβλητο. Για σύνθετα αντικείμενα ίσως χρειαστεί να διαφύγετε τα εισαγωγικά. |
| **Using a different data source (e.g., List\<T\>)** | Αντικαταστήστε το `DataTable` με οποιαδήποτε συλλογή που μπορεί να επαναληφθεί· η σύνταξη του marker (`&=myList.Property`) παραμένει η ίδια. |
| **Exporting to CSV instead of XLSX** | Το `ArrayAsSingle` ισχύει και εδώ, αλλά θυμηθείτε ότι το CSV δεν διατηρεί μορφοποίηση κελιών· ίσως χρειαστεί να τυλίξετε το JSON σε εισαγωγικά. |

**Pro tip:** Πάντα ορίστε το `ArrayAsSingle` *πριν* καλέσετε το `ProcessSmartMarkers`. Η αλλαγή της σημαίας μετά την επεξεργασία δεν επηρεάζει τα ήδη δημιουργημένα κελιά.

---

## Full, runnable example

Παρακάτω βρίσκεται το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε‑επικολλήσετε σε μια εφαρμογή κονσόλας. Περιλαμβάνει όλες τις οδηγίες `using` και σχόλια για σαφήνεια.

```csharp
using System;
using System.Data;
using Aspose.Cells;

namespace SmartMarkerDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create the data source with a JSON array
            DataTable dataTable = new DataTable();
            dataTable.Columns.Add("Id", typeof(int));
            dataTable.Columns.Add("Names", typeof(string));
            dataTable.Rows.Add(1, "[\"Alice\",\"Bob\"]");

            // 2️⃣ Build a workbook and place smart markers
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];
            worksheet.Cells["A1"].PutValue("&=dataTable");          // whole table (optional)
            worksheet.Cells["A2"].PutValue("&=dataTable.Names");   // Names column

            // 3️⃣ Configure SmartMarkerOptions to treat arrays as single values
            SmartMarkerOptions options = new SmartMarkerOptions
            {
                ArrayAsSingle = true
            };

            // 4️⃣ Process the markers with the custom options
            workbook.ProcessSmartMarkers(options);

            // 5️⃣ Save the file
            string path = @"C:\Temp\SmartMarkerJson.xlsx";
            workbook.Save(path);
            Console.WriteLine($"Workbook saved to {path}");
        }
    }
}
```

Εκτελέστε το πρόγραμμα, ανοίξτε το `SmartMarkerJson.xlsx` και θα δείτε τον JSON πίνακα διατηρημένο στο κελί **A2**.

---

## Conclusion

Τώρα γνωρίζετε πώς να **configure SmartMarkerOptions ArrayAsSingle** σε C# για να διατηρήσετε έναν JSON πίνακα ως τιμή ενός μόνο κελιού όταν χρησιμοποιείτε smart markers του Aspose.Cells. Τα βήματα—προετοιμασία `DataTable`, εισαγωγή markers, ρύθμιση της σημαίας `ArrayAsSingle`, επεξεργασία και αποθήκευση—αποτελούν ένα επαναχρησιμοποιήσιμο μοτίβο που μπορείτε να εφαρμόσετε σε οποιοδήποτε σενάριο απαιτεί συμπαγή αναπαράσταση JSON μέσα στο Excel.

Στη συνέχεια, μπορείτε να εξερευνήσετε:

* **Aspose.Cells smart markers** για επανάληψη πάνω σε συλλογές.
* Εξαγωγή **nested JSON objects** προσαρμόζοντας τη μορφοποίηση κελιών.
* Συνδυασμό **conditional formatting** με smart markers για πιο πλούσιες αναφορές.

Μη διστάσετε να πειραματιστείτε με διαφορετικές δομές δεδομένων και να μοιραστείτε τα ευρήματά σας. Καλή κωδικοποίηση!

## What Should You Learn Next?

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κυριαρχήσετε πρόσθετες λειτουργίες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Create Excel Workbook from JSON – Complete Aspose.Cells Guide](/cells/english/net/data-loading-and-parsing/create-excel-workbook-from-json-complete-aspose-cells-guide/)
- [Create Configure Excel Workbook Aspose Cells Net](/cells/hindi/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)
- [Create Configure Excel Workbook Aspose Cells Net](/cells/german/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}