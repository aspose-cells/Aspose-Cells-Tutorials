---
category: general
date: 2026-06-21
description: Δημιουργήστε διαδραστικό πλέγμα δεδομένων χρησιμοποιώντας το Grid.js
  και μάθετε πώς να εμφανίζετε πίνακα δεδομένων JSON με ταξινόμηση, σελιδοποίηση και
  αναζήτηση. Ιδανικό για πίνακες ελέγχου ιστού.
draft: false
keywords:
- create interactive data grid
- display json data table
- how to use gridjs
language: el
og_description: Δημιουργήστε διαδραστικό πλέγμα δεδομένων σε λίγα λεπτά. Μάθετε πώς
  να χρησιμοποιείτε το Grid.js για να εμφανίσετε πίνακα δεδομένων JSON με σελιδοποίηση,
  ταξινόμηση και αναζήτηση.
og_title: Δημιουργήστε Διαδραστικό Πλέγμα Δεδομένων με το Grid.js – Πλήρης Εκπαιδευτικό
  Σεμινάριο
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Create interactive data grid using Grid.js and learn how to display
    JSON data table with sorting, pagination, and search. Perfect for web dashboards.
  headline: Create Interactive Data Grid with Grid.js – Full Step‑by‑Step Guide
  type: TechArticle
- description: Create interactive data grid using Grid.js and learn how to display
    JSON data table with sorting, pagination, and search. Perfect for web dashboards.
  name: Create Interactive Data Grid with Grid.js – Full Step‑by‑Step Guide
  steps:
  - name: A modern browser (Chrome, Edge, or Firefox) – Grid.js relies on ES6 features.
    text: A modern browser (Chrome, Edge, or Firefox) – Grid.js relies on ES6 features.
  - name: A local or remote folder containing a `grid_data.json` file (we’ll show
      the format).
    text: A local or remote folder containing a `grid_data.json` file (we’ll show
      the format).
  - name: Basic familiarity with HTML and JavaScript – nothing fancy, just the ability
      to open a `.html` file in a browser.
    text: Basic familiarity with HTML and JavaScript – nothing fancy, just the ability
      to open a `.html` file in a browser.
  type: HowTo
tags:
- JavaScript
- Grid.js
- Data Visualization
title: Δημιουργήστε Διαδραστικό Πλέγμα Δεδομένων με το Grid.js – Πλήρης Οδηγός Βήμα‑βήμα
url: /el/python/import-and-export/create-interactive-data-grid-with-grid-js-full-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία Διαδραστικού Πλέγματος Δεδομένων με Grid.js – Πλήρης Οδηγός Βήμα‑βήμα

Έχετε αναρωτηθεί ποτέ πώς να **δημιουργήσετε διαδραστικό πλέγμα δεδομένων** που επιτρέπει στους χρήστες να ταξινομούν, να αναζητούν και να μετακινούνται μεταξύ των γραμμών χωρίς να γράψετε backend; Δεν είστε μόνοι. Σε πολλά dashboards το μεγαλύτερο πρόβλημα είναι η μετατροπή ενός στατικού αρχείου JSON σε έναν κομψό, αναζητήσιμο πίνακα—κάτι που αισθάνεται τόσο ομαλό όσο ένα λογιστικό φύλλο αλλά εκτελείται εξ ολοκλήρου στον περιηγητή.

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από **πώς να χρησιμοποιήσετε Grid.js** για **εμφάνιση πίνακα δεδομένων JSON** σε μια απλή σελίδα HTML. Στο τέλος θα έχετε ένα λειτουργικό παράδειγμα που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο, καθώς και συμβουλές για προσαρμογή της γραμμής εργαλείων, διαχείριση μεγάλων συνόλων δεδομένων και αποφυγή κοινών παγίδων.

## Τι Θα Μάθετε

- Πώς να φορτώσετε ένα αρχείο JSON που ορίζει στήλες και γραμμές.
- Πώς να αρχικοποιήσετε **Grid.js** με σελιδοποίηση, ταξινόμηση, αναζήτηση και προσαρμοσμένη γραμμή εργαλείων.
- Πώς να αποδώσετε το πλέγμα σε έναν προορισμένο container.
- Προαιρετικές βελτιώσεις: προσαρμοσμένη μορφοποίηση κελιών, αλλαγή θέματος και διαχείριση σφαλμάτων.
- Ένα πλήρες, έτοιμο για αντιγραφή‑επικόλληση δείγμα κώδικα.

### Προαπαιτούμενα

Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε:

1. Έναν σύγχρονο περιηγητή (Chrome, Edge ή Firefox) – το Grid.js βασίζεται σε χαρακτηριστικά ES6.
2. Έναν τοπικό ή απομακρυσμένο φάκελο που περιέχει ένα αρχείο `grid_data.json` (θα δείξουμε τη μορφή του).
3. Βασική εξοικείωση με HTML και JavaScript – τίποτα περίπλοκο, μόνο η δυνατότητα να ανοίξετε ένα αρχείο `.html` σε περιηγητή.

Δεν χρειάζονται εργαλεία κατασκευής, npm install ή κώδικας στο διακομιστή. Αυτή είναι η ομορφιά του **δημιουργίας διαδραστικού πλέγματος δεδομένων** με Grid.js: λειτουργεί απευθείας από CDN.

---

## Βήμα 1: Προετοιμάστε το JSON που Ορίζει τον Πίνακά Σας

Το πρώτο που χρειάζεστε είναι ένα JSON payload που λέει στο Grid.js ποιες στήλες υπάρχουν και ποιες γραμμές να εμφανίσει. Σκεφτείτε το ως το σχέδιο για την **εμφάνιση πίνακα δεδομένων JSON**. Ακολουθεί ένα ελάχιστο παράδειγμα που μπορείτε να αποθηκεύσετε ως `grid_data.json` στον ίδιο φάκελο με το αρχείο HTML:

```json
{
  "columns": ["ID", "Name", "Email", "Country"],
  "rows": [
    [1, "Alice Johnson", "alice@example.com", "USA"],
    [2, "Bob Smith", "bob@example.com", "Canada"],
    [3, "Carlos Ruiz", "carlos@example.com", "Mexico"],
    [4, "Diana Lee", "diana@example.com", "UK"]
  ]
}
```

*Γιατί αυτή η μορφή;* Το Grid.js αναμένει το `columns` ως έναν πίνακα από συμβολοσειρές (ή αντικείμενα για προχωρημένες ρυθμίσεις) και το `rows` ως έναν πίνακα από πίνακες όπου κάθε εσωτερικός πίνακας ταιριάζει με τη σειρά των στηλών. Φυσικά μπορείτε να προσθέσετε περισσότερες στήλες ή ενσωματωμένα αντικείμενα – το Grid.js θα τα αποδώσει εφόσον οι δομές ταιριάζουν.

> **Συμβουλή επαγγελματία:** Αν παίρνετε δεδομένα από API, απλώς αντικαταστήστε το στατικό `fetch('grid_data.json')` με το URL του endpoint σας. Το υπόλοιπο του κώδικα παραμένει το ίδιο.

---

## Βήμα 2: Αρχικοποιήστε το Grid.js – Η Καρδιά του **πώς να χρησιμοποιήσετε gridjs**

Τώρα που η πηγή δεδομένων είναι έτοιμη, πρέπει να φέρουμε το Grid.js στη σελίδα και να του πούμε πώς να συμπεριφέρεται. Εδώ δημιουργούμε την λειτουργικότητα **δημιουργίας διαδραστικού πλέγματος δεδομένων** όπως σελιδοποίηση, ταξινόμηση και ένα χρήσιμο κουμπί στη γραμμή εργαλείων.

```html
<!-- Load Grid.js from the CDN -->
<script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
<link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet"/>
```

Το CDN παρέχει την πιο πρόσφατη σταθερή έκδοση, και το θέμα Mermaid προσθέτει μια καθαρή, μοντέρνα εμφάνιση έτοιμη προς χρήση. Μπορείτε να το αντικαταστήσετε με `gridjs.min.css` αν προτιμάτε το προεπιλεγμένο στυλ.

Στη συνέχεια, μέσα σε μια ετικέτα `<script>`, φορτώστε το JSON και αρχικοποιήστε το πλέγμα:

```javascript
// Step 2: Initialise Grid.js with pagination, sorting, searching, and a toolbar
fetch('grid_data.json')
  .then(response => response.json())
  .then(data => {
    const grid = new gridjs.Grid({
      columns: data.columns,      // Pull column headers from JSON
      data: data.rows,            // Pull row data from JSON
      pagination: { enabled: true, limit: 10 }, // Show 10 rows per page
      sort: true,                 // Enable column sorting
      search: true,               // Add a search box above the grid
      toolbar: {
        enabled: true,
        items: [
          {
            type: 'button',
            text: 'Help',
            onClick: () => alert('Use the search box to filter rows or click column headers to sort.')
          }
        ]
      },
      // Optional: custom cell formatter for the Email column
      // This demonstrates a deeper dive into how to use Grid.js
      // and shows you can embed HTML inside cells.
      columns: data.columns.map(col => {
        if (col === 'Email') {
          return {
            name: col,
            formatter: cell => gridjs.html(`<a href="mailto:${cell}">${cell}</a>`)
          };
        }
        return col; // Simple string for other columns
      })
    });

    // Step 3: Render the grid into the target container
    grid.render(document.getElementById('grid-container'));
  })
  .catch(err => console.error('Failed to load grid data:', err));
```

### Ανάλυση των Επιλογών

| Επιλογή | Τι Κάνει | Γιατί Είναι Σημαντικό |
|--------|----------|-----------------------|
| `pagination` | Διαχωρίζει τις γραμμές σε σελίδες (προεπιλογή 10 ανά σελίδα) | Κρατά τους μεγάλους πίνακες ευανάγνωστους χωρίς να υπερφορτώνει το UI. |
| `sort` | Κλικ στις κεφαλίδες των στηλών εναλλάσσει αύξουσα/φθίνουσα σειρά | Οι χρήστες μπορούν γρήγορα να βρουν τις γραμμές με τις υψηλότερες τιμές. |
| `search` | Προσθέτει πεδίο κειμένου που φιλτράρει τις γραμμές σε πραγματικό χρόνο | Ιδανικό για άμεσες αναζητήσεις χωρίς επαναφόρτωση δεδομένων. |
| `toolbar` | Προσθέτει προσαρμοσμένα κουμπιά ή dropdowns πάνω από το πλέγμα | Τέλειο για ενέργειες “Βοήθεια”, “Εξαγωγή” ή “Ανανέωση”. |
| `formatter` | Σας επιτρέπει να επιστρέψετε ακατέργαστο HTML για ένα κελί | Εδώ μετατρέπουμε τις διευθύνσεις email σε κλικ‑αξιόπλαστα link mailto. |

> **Γιατί αυτή η προσέγγιση;** Διατηρώντας τη διαμόρφωση του πλέγματος δηλωτική, μπορείτε εύκολα να τροποποιήσετε τη συμπεριφορά χωρίς να αγγίξετε τη λογική απόδοσης. Αυτή είναι η προτεινόμενη μέθοδος **πώς να χρησιμοποιήσετε Grid.js** για τα περισσότερα έργα.

---

## Βήμα 3: Αποδώστε το Πλέγμα στη Σελίδα Σας

Η τελευταία γραμμή του script—`grid.render(document.getElementById('grid-container'))`—εισάγει τον πλήρως λειτουργικό πίνακα σε ένα `<div>` που έχετε τοποθετήσει κάπου στο σώμα του HTML:

```html
<div id="grid-container"></div>
```

Αυτό είναι όλο. Όταν η σελίδα φορτώνει, ο περιηγητής φορτώνει το JSON, δημιουργεί το αντικείμενο Grid.js και σχεδιάζει τον διαδραστικό πίνακα στην οθόνη. Χωρίς ανανεώσεις, χωρίς κλήσεις στο διακομιστή μετά το αρχικό φόρτωμα.

---

## Προαιρετικό: Προσαρμογές Στυλ και Θέματος

Αν το προεπιλεγμένο θέμα Mermaid δεν σας αρέσει, μπορείτε να το αντικαταστήσετε με οποιοδήποτε από τα ενσωματωμένα θέματα (`gridjs.min.css`) ή να γράψετε το δικό σας CSS. Για παράδειγμα, για να κάνετε το φόντο της κεφαλίδας ένα απαλό γκρι:

```css
.gridjs-th {
  background-color: #f5f5f5;
}
```

Προσθέστε το απόσπασμα μέσα σε μια ετικέτα `<style>` ή σε εξωτερικό stylesheet. Το Grid.js σέβεται τους τυπικούς CSS selectors, οπότε έχετε πλήρη έλεγχο πάνω σε γραμματοσειρές, χρώματα και αποστάσεις.

---

## Συνηθισμένες Παγίδες & Πώς να τις Αποφύγετε

| Παγίδα | Συμπτωμα | Διόρθωση |
|--------|----------|----------|
| **Σφάλματα CORS** όταν φορτώνετε JSON από διαφορετικό domain | Η κονσόλα του περιηγητή δείχνει “Blocked by CORS policy” | Φιλοξενήστε το JSON στην ίδια προέλευση ή ενεργοποιήστε CORS στον διακομιστή. |
| **Μεγάλα σύνολα δεδομένων προκαλούν καθυστέρηση** | Η κύλιση γίνεται τρεμάλα, η σελιδοποίηση αργή | Χρησιμοποιήστε `server` pagination (`pagination: { server: { url: (prev, page, limit) => … } }`) ή lazy‑load γραμμές. |
| **Το κουμπί της γραμμής εργαλείων δεν εμφανίζεται** | Δεν φαίνεται κανένα κουμπί παρόλο που `toolbar.enabled: true` | Βεβαιωθείτε ότι χρησιμοποιείτε Grid.js έκδοση 2.0+· οι παλαιότερες εκδόσεις είχαν διαφορετικό API για τη γραμμή εργαλείων. |
| **Οι σύνδεσμοι email δεν είναι κλικ‑αξιόπλαστοι** | Ο formatter επιστρέφει απλό κείμενο | Επιστρέψτε `gridjs.html(...)` αντί για απλή συμβολοσειρά, όπως φαίνεται στο παράδειγμα. |

Η αντιμετώπιση αυτών των ζητημάτων νωρίς σας εξοικονομεί ώρες ενδεχόμενης αποσφαλμάτωσης.

---

## Πλήρες Παράδειγμα (Έτοιμο για Αντιγραφή‑Επικόλληση)

Παρακάτω βρίσκεται το πλήρες αρχείο HTML που μπορείτε να αποθηκεύσετε ως `index.html`. Ανοίξτε το σε περιηγητή και θα δείτε μια πλήρως λειτουργική επίδειξη **δημιουργίας διαδραστικού πλέγματος δεδομένων** που **εμφανίζει πίνακα δεδομένων JSON** με ταξινόμηση, αναζήτηση και κουμπί βοήθειας.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Create Interactive Data Grid with Grid.js</title>
  <!-- Grid.js core library -->
  <script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
  <!-- Optional theme – Meri­maid -->
  <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet"/>
  <style>
    /* Simple custom styling */
    body { font-family: Arial, sans-serif; margin: 20px; }
    .gridjs-container { max-width: 900px; margin: auto; }
    .gridjs-th { background-color: #f0f8ff; }
  </style>
</head>
<body>
  <h1>Create Interactive Data Grid with Grid.js</h1>
  <p>This page demonstrates how to <strong>display JSON data table</strong> using Grid.js. Feel free to edit <code>grid_data.json</code> and refresh.</p>

  <!-- Grid will be rendered here -->
  <div id="grid-container"></div>

  <script>
    // Load JSON data and initialise Grid.js
    fetch('grid_data.json')
      .then(r => r.json())
      .then(data => {
        const grid = new gridjs.Grid({
          columns: data.columns.map(col => {
            // Custom formatter for Email column
            if (col === 'Email') {
              return {
                name: col,
                formatter: cell => gridjs.html(`<a href="mailto:${cell}">${cell}</a>`)
              };
            }
            return col;
          }),
          data: data.rows,
          pagination: { enabled: true, limit: 5 },
          sort: true,
          search: true,
          toolbar: {
            enabled: true,
            items: [
              {
                type: 'button',
                text: 'Formula Help',
                onClick: () => alert('Hover over a cell to see its formula description.')
              }
            ]
          }
        });

        // Render the grid
        grid.render(document.getElementById('grid-container'));
      })
      .catch(err => console.error('Error loading grid data:', err));
  </script>
</body>
</html


## Τι Θα Μάθετε Στη Σειρά;

Οι παρακάτω οδηγίες καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κυριαρχήσετε επιπλέον δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στα δικά σας έργα.

- [How to Create an Excel Data Validation List with Aspose.Cells for Java: A Step-by-Step Guide](/cells/english/java/data-validation/excel-data-validation-aspose-cells-java/)
- [How to Create Checkboxes in Excel using Aspose.Cells for .NET | Data Validation Tutorial](/cells/english/net/data-validation/create-checkboxes-net-excel-aspose-cells/)
- [Create & Import XML Data into Excel Using Aspose.Cells for Java](/cells/english/java/import-export/create-import-xml-data-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}