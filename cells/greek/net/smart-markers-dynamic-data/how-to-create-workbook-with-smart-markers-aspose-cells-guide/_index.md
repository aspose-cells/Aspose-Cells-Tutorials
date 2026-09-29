---
category: general
date: 2026-02-23
description: Πώς να δημιουργήσετε βιβλίο εργασίας χρησιμοποιώντας το Aspose.Cells
  και να προσθέσετε δείκτες με έναν πίνακα JSON. Μάθετε πώς να προσθέτετε δείκτες,
  να χρησιμοποιείτε πίνακα JSON και έξυπνους δείκτες Aspose.Cells σε λίγα λεπτά.
draft: false
keywords:
- how to create workbook
- how to add markers
- use json array
- smart markers aspose.cells
language: el
og_description: Πώς να δημιουργήσετε ένα βιβλίο εργασίας χρησιμοποιώντας το Aspose.Cells,
  να προσθέσετε δείκτες και να χρησιμοποιήσετε έναν πίνακα JSON. Αυτός ο οδηγός βήμα‑βήμα
  σας δείχνει όλα όσα χρειάζεστε.
og_title: Πώς να δημιουργήσετε βιβλίο εργασίας με έξυπνους δείκτες – Aspose.Cells
tags:
- Aspose.Cells
- C#
- Excel Automation
title: Πώς να δημιουργήσετε βιβλίο εργασίας με έξυπνους δείκτες – Οδηγός Aspose.Cells
url: /el/net/smart-markers-dynamic-data/how-to-create-workbook-with-smart-markers-aspose-cells-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να δημιουργήσετε Workbook με Smart Markers – Οδηγός Aspose.Cells

Έχετε αναρωτηθεί ποτέ **πώς να δημιουργήσετε workbook** που γεμίζει αυτόματα δεδομένα από μια πηγή JSON; Δεν είστε ο μόνος—οι προγραμματιστές ρωτούν συνεχώς πώς να προσθέσουν markers που αντλούν τιμές από πίνακες, ειδικά όταν εργάζονται με Aspose.Cells. Τα καλά νέα; Είναι αρκετά απλό μόλις κατανοήσετε την έννοια των smart‑marker. Σε αυτό το tutorial θα περάσουμε από τη δημιουργία ενός workbook, την προσθήκη markers, τη χρήση ενός JSON array, και τη διαμόρφωση smart markers στο Aspose.Cells ώστε να μπορείτε να δημιουργείτε αρχεία Excel άμεσα.

Θα καλύψουμε όλα όσα χρειάζεστε: την αρχικοποίηση του workbook, τη δημιουργία μιας `MarkerCollection`, την παροχή ενός JSON array, την εναλλαγή της σημαίας “ArrayAsSingle”, και τέλος την εφαρμογή των markers. Στο τέλος θα έχετε ένα πλήρως λειτουργικό πρόγραμμα C# που παράγει ένα αρχείο Excel με τις τιμές **A**, **B**, και **C** να γεμίζουν αυτόματα. Χωρίς εξωτερικές υπηρεσίες, μόνο καθαρή μαγεία Aspose.Cells.

## Προαπαιτήσεις

- .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί επίσης με .NET Framework 4.6+)
- Πακέτο NuGet Aspose.Cells for .NET (`Install-Package Aspose.Cells`)
- Βασική κατανόηση της σύνταξης C# (αν είστε από την αρχή, τα αποσπάσματα είναι βαριά σχολιασμένα)
- Visual Studio ή οποιοδήποτε IDE προτιμάτε

Αν έχετε ήδη όλα αυτά, υπέροχα—ας βουτήξουμε.

## Βήμα 1: Πώς να δημιουργήσετε Workbook (Αρχικοποίηση του αρχείου Excel)

Το πρώτο που χρειάζεστε είναι ένα κενό αντικείμενο workbook. Σκεφτείτε το ως έναν λευκό καμβά που το Aspose.Cells θα ζωγραφίσει αργότερα με δεδομένα.

```csharp
using System;
using Aspose.Cells;

class SmartMarkerDemo
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();               // creates an empty .xlsx in memory
        Worksheet worksheet = workbook.Worksheets[0];    // reference to the default sheet
```

> **Why this matters:** `Workbook` είναι το σημείο εισόδου για κάθε λειτουργία Excel. Χωρίς αυτό δεν μπορείτε να συνδέσετε smart markers ή να αποθηκεύσετε το αρχείο. Η δημιουργία του workbook πρώτα εξασφαλίζει επίσης ένα καθαρό περιβάλλον για τα επόμενα βήματα.

## Βήμα 2: Πώς να προσθέσετε Markers – Αρχικοποίηση μιας Marker Collection

Smart markers ζουν μέσα σε μια `MarkerCollection`. Αυτή η συλλογή είναι όπου ορίζετε placeholders (τα markers) και τα δεδομένα που θα τα αντικαταστήσουν.

```csharp
        // Step 2: Initialise a collection for smart markers
        MarkerCollection smartMarkerCollection = new MarkerCollection();
```

> **Pro tip:** Μπορείτε να επαναχρησιμοποιήσετε την ίδια `MarkerCollection` για πολλαπλά worksheets, αλλά η διατήρηση μίας ανά φύλλο κάνει το debugging πιο εύκολο.

## Βήμα 3: Χρήση JSON Array – Προσθήκη Marker με δεδομένα JSON

Τώρα προσθέτουμε πραγματικά ένα marker. Το placeholder `{SmartMarker}` θα αντικατασταθεί από το JSON array που παρέχουμε. Το JSON πρέπει να είναι ένας stringified πίνακας, π.χ., `["A","B","C"]`.

```csharp
        // Step 3: Add a smart marker and provide replacement data (JSON array)
        smartMarkerCollection.Add("{SmartMarker}", "[\"A\",\"B\",\"C\"]");
```

> **Explanation:** Η μέθοδος `Add` δέχεται δύο ορίσματα: το κείμενο του marker και την πηγή δεδομένων. Εδώ η πηγή δεδομένων είναι ένα JSON array, το οποίο το Aspose.Cells μπορεί να αναλύσει αυτόματα. Αυτό είναι το βασικό στοιχείο του **use json array** με smart markers.

## Βήμα 4: Διαμόρφωση του Marker – Θεωρήστε το Array ως Μία Μοναδική Τιμή

Από προεπιλογή, το Aspose.Cells επεκτείνει ένα JSON array σε ξεχωριστές γραμμές. Αν θέλετε ολόκληρο το array να αντιμετωπίζεται ως μία τιμή κελιού (χρήσιμο για λίστες dropdown ή συνενωμένες συμβολοσειρές), ορίστε τη σημαία `ArrayAsSingle`.

```csharp
        // Step 4: Configure the marker to treat the array as a single value
        smartMarkerCollection["ArrayAsSingle"] = true;
```

> **When to use it:** Αν χρειάζεστε το array να εμφανίζεται σε ένα κελί (π.χ., `"A,B,C"`), ενεργοποιήστε αυτή τη σημαία. Διαφορετικά, το Aspose.Cells θα γράψει κάθε στοιχείο στη δική του γραμμή.

## Βήμα 5: Συζευξτε Markers με το Worksheet και Εφαρμόστε τα

Τέλος, συνδέστε τη συλλογή markers με το worksheet και πείτε στο Aspose.Cells να αντικαταστήσει τα placeholders με τα πραγματικά δεδομένα.

```csharp
        // Step 5: Attach the marker collection to the worksheet and apply it
        worksheet.SmartMarkers.Add(smartMarkerCollection);
        worksheet.SmartMarkers.Apply();

        // Optional: write the placeholder into a cell so you can see the replacement
        worksheet.Cells["A1"].PutValue("{SmartMarker}");

        // Save the workbook to disk
        workbook.Save("SmartMarkerResult.xlsx");
        Console.WriteLine("Workbook created successfully!");
    }
}
```

> **Result:** Μετά την εκτέλεση του προγράμματος, το `SmartMarkerResult.xlsx` περιέχει την τιμή **A** (ή ολόκληρο το array αν το `ArrayAsSingle` είναι true) στο κελί `A1`. Ανοίξτε το αρχείο για να το επαληθεύσετε.

### Αναμενόμενο Αποτέλεσμα

| A |
|---|
| A |   *(αν `ArrayAsSingle` είναι false, το πρώτο στοιχείο γεμίζει το κελί)*

Αν ορίσετε `ArrayAsSingle = true`, το κελί `A1` θα περιέχει τη συμβολοσειρά `["A","B","C"]`.

## Βήμα 6: Πώς να προσθέσετε Markers – Προχωρημένα Σενάρια (Προαιρετικό)

Μπορεί να αναρωτιέστε, *τι γίνεται αν χρειάζομαι περισσότερα από ένα marker;* Η απάντηση είναι απλή: καλέστε ξανά το `Add`.

```csharp
        smartMarkerCollection.Add("{SecondMarker}", "[{\"Name\":\"John\"},{\"Name\":\"Jane\"}]");
        // You can also control each marker individually:
        smartMarkerCollection["SecondMarker"] = false; // expand into rows
```

> **Why this works:** Κάθε marker λειτουργεί ανεξάρτητα, έτσι μπορείτε να συνδυάσετε “array as single” και “expand into rows” στο ίδιο worksheet. Αυτή η ευελιξία είναι χαρακτηριστικό των **smart markers aspose.cells**.

## Συνηθισμένα Πιθανά Σφάλματα & Πώς να τα Αποφύγετε

| Πρόβλημα | Γιατί Συμβαίνει | Διόρθωση |
|----------|----------------|----------|
| Marker δεν αντικαθίσταται | Λείπει το κείμενο του placeholder ή υπάρχει τυπογραφικό λάθος | Βεβαιωθείτε ότι το κελί περιέχει ακριβώς τη συμβολοσειρά marker (`{SmartMarker}`) |
| JSON δεν αναλύεται | Μη έγκυρη σύνταξη JSON (λείπουν εισαγωγικά) | Χρησιμοποιήστε έναν validator JSON ή διπλό‑escape τα εισαγωγικά στις συμβολοσειρές C# |
| Το array επεκτείνεται απροσδόκητα | Η `ArrayAsSingle` παραμένει στην προεπιλογή `false` | Ορίστε `["ArrayAsSingle"] = true` για το συγκεκριμένο marker |
| Το workbook αποθηκεύεται κενό | Η `Apply()` δεν κλήθηκε πριν το `Save()` | Πάντα καλέστε `worksheet.SmartMarkers.Apply()` πριν αποθηκεύσετε |

## Πλήρες Παράδειγμα Εργασίας (Έτοιμο για Αντιγραφή‑Επικόλληση)

Παρακάτω είναι το πλήρες πρόγραμμα που μπορείτε να ενσωματώσετε σε μια εφαρμογή console. Δεν απαιτούνται επιπλέον αρχεία.

```csharp
using System;
using Aspose.Cells;

class SmartMarkerDemo
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Initialise a collection for smart markers
        MarkerCollection smartMarkerCollection = new MarkerCollection();

        // Add a smart marker and provide replacement data (JSON array)
        smartMarkerCollection.Add("{SmartMarker}", "[\"A\",\"B\",\"C\"]");

        // Configure the marker to treat the array as a single value
        smartMarkerCollection["ArrayAsSingle"] = true;

        // Attach the marker collection to the worksheet and apply it
        worksheet.SmartMarkers.Add(smartMarkerCollection);
        worksheet.SmartMarkers.Apply();

        // Place the marker in a cell so we can see the replacement
        worksheet.Cells["A1"].PutValue("{SmartMarker}");

        // Save the workbook
        workbook.Save("SmartMarkerResult.xlsx");
        Console.WriteLine("Workbook created successfully!");
    }
}
```

Εκτελέστε το πρόγραμμα, ανοίξτε το `SmartMarkerResult.xlsx`, και θα δείτε το JSON array (ή το πρώτο του στοιχείο) να τοποθετείται κομψά στο κελί **A1**.

## Επόμενα Βήματα: Επέκταση της Λύσης

Τώρα που ξέρετε **πώς να δημιουργήσετε workbook**, **πώς να προσθέσετε markers**, και **πώς να χρησιμοποιήσετε json array** με Aspose.Cells, σκεφτείτε τις παρακάτω ιδέες:

1. **Πολλαπλά Worksheets** – Επανάληψη μέσω λίστας worksheets και σύνδεση διαφορετικών συλλογών markers σε καθένα.
2. **Δυναμικό JSON** – Λήψη JSON από web API (`HttpClient`) και άμεση τροφοδοσία στο `smartMarkerCollection.Add`.
3. **Στυλ εξόδου** – Μετά την εφαρμογή των markers, μορφοποιήστε τα κελιά (γραμματοσειρές, χρώματα) για πιο επαγγελματική εμφάνιση της αναφοράς.
4. **Μορφές εξαγωγής** – Αποθηκεύστε το workbook ως PDF, CSV ή HTML αλλάζοντας `workbook.Save("file.pdf")`.

Κάθε ένα από αυτά τα θέματα εμπλέκει φυσικά **smart markers aspose.cells**, οπότε θα επεκτείνετε τις ίδιες βασικές έννοιες που μόλις μάθατε.

## Συμπέρασμα

Διασχίσαμε **πώς να δημιουργήσετε workbook** από το μηδέν, **πώς να προσθέσετε markers**, και **πώς να χρησιμοποιήσετε json array** με smart markers του Aspose.Cells. Το πλήρες, εκτελέσιμο παράδειγμα δείχνει ολόκληρη τη ροή εργασίας, από την αρχικοποίηση του `Workbook` μέχρι την αποθήκευση του τελικού αρχείου. Με την εναλλαγή της σημαίας `ArrayAsSingle` αποκτάτε λεπτομερή έλεγχο του πώς εμφανίζονται τα δεδομένα JSON στο Excel, καθιστώντας τη λύση προσαρμόσιμη σε ένα ευρύ φάσμα σεναρίων αναφοράς.

Δοκιμάστε τον κώδικα, τροποποιήστε το JSON, και πειραματιστείτε με επιπλέον markers. Όταν κυριαρχήσετε αυτά τα δομικά στοιχεία, η δημιουργία σύνθετων αναφορών Excel γίνεται παιχνιδάκι. Έχετε ερωτήσεις ή θέλετε να μοιραστείτε μια ενδιαφέρουσα περίπτωση χρήσης; Αφήστε ένα σχόλιο παρακάτω—καλή προγραμματιστική!

![Διάγραμμα που δείχνει πώς να δημιουργήσετε workbook με smart markers στο Aspose.Cells](https://example.com/images/create-workbook-smart-markers.png "πώς να δημιουργήσετε workbook με smart markers στο Aspose.Cells")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}