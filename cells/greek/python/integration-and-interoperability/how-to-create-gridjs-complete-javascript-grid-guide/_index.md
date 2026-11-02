---
category: general
date: 2026-06-30
description: Πώς να δημιουργήσετε το gridjs εύκολα με ένα πλήρες παράδειγμα JavaScript,
  καλύπτοντας τη διαμόρφωση του gridjs, τη ρύθμιση του container και τη διαδικασία
  απόδοσης.
draft: false
keywords:
- how to create gridjs
- gridjs configuration
- gridjs render
- gridjs JavaScript
- gridjs container
language: el
og_description: Πώς να δημιουργήσετε το gridjs εύκολα με ένα πλήρες παράδειγμα JavaScript,
  καλύπτοντας τη διαμόρφωση του gridjs, τη ρύθμιση του container και τη διαδικασία
  απόδοσης.
og_title: Πώς να δημιουργήσετε το Gridjs – Πλήρης οδηγός πλέγματος JavaScript
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: How to create gridjs easily with a full JavaScript example, covering
    gridjs configuration, container setup, and render process.
  headline: How to Create Gridjs – Complete JavaScript Grid Guide
  type: TechArticle
- description: How to create gridjs easily with a full JavaScript example, covering
    gridjs configuration, container setup, and render process.
  name: How to Create Gridjs – Complete JavaScript Grid Guide
  steps:
  - name: Why this configuration matters
    text: '- **Columns** – define the header text and optional width. Without this,
      Gridjs would infer column names from the first data row, which is often less
      readable. - **Data** – an array of rows, each row being an array of cell values.
      You could also supply an async function that fetches data from an API'
  - name: Expected Output
    text: '``` +----+----------------+---------------------+--------+ | ID | Name
      | Email | Role | +----+----------------+---------------------+--------+ | 1
      | Alice Johnson | alice@example.com | Admin | | 2 | Bob Smith | bob@example.com
      | Editor | +----+----------------+---------------------+--------+ [←] [1]'
  - name: Loading Data Asynchronously
    text: 'If your data lives on a server, replace the static `data` array with a
      function that returns a Promise:'
  - name: Custom Cell Rendering
    text: 'Sometimes you need icons, buttons, or formatted dates inside cells. Use
      the `formatter` property on a column:'
  - name: Multiple Grids on One Page
    text: 'Just repeat steps 2‑5 with different container IDs:'
  type: HowTo
tags:
- gridjs
- JavaScript
- web‑development
title: Πώς να δημιουργήσετε το Gridjs – Πλήρης οδηγός πλέγματος JavaScript
url: /el/python/integration-and-interoperability/how-to-create-gridjs-complete-javascript-grid-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Δημιουργήσετε Gridjs – Ολοκληρωμένος Οδηγός JavaScript Grid

Έχετε αναρωτηθεί ποτέ **πώς να δημιουργήσετε gridjs** και να εμφανίσετε αμέσως έναν κομψό πίνακα δεδομένων στη σελίδα σας; Δεν είστε οι μόνοι. Πολλοί προγραμματιστές συναντούν δυσκολίες όταν προσπαθούν για πρώτη φορά να ενσωματώσουν το Gridjs, ειδικά γύρω από το αντικείμενο ρυθμίσεων και την κλήση render. Τα καλά νέα; Είναι πραγματικά εύκολο μόλις γνωρίζετε τα σωστά βήματα.

Σε αυτό το tutorial θα περάσουμε από ένα πραγματικό παράδειγμα που δείχνει **πώς να δημιουργήσετε gridjs** από το μηδέν, πώς να δημιουργήσετε μια σωστή **gridjs configuration**, πώς να συνδέσετε το grid με ένα **gridjs container**, και τέλος πώς να ενεργοποιήσετε το **gridjs render**. Στο τέλος θα έχετε ένα πλήρως λειτουργικό grid που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο—χωρίς μυστήριο, μόνο καθαρός κώδικας.

## Τι Θα Μάθετε

- Ρύθμιση μιας ελάχιστης σελίδας HTML έτοιμης για Gridjs.
- Δημιουργία ενός αντικειμένου **gridjs configuration** που ορίζει στήλες, δεδομένα και επιλογές.
- Σύνδεση της παρουσίας Gridjs με ένα στοιχείο **gridjs container**.
- Κλήση του **gridjs render** για την εμφάνιση του πίνακα.
- Προσαρμογή κοινών ρυθμίσεων (σελιδοποίηση, ταξινόμηση, στυλ) και αποφυγή τυπικών παγίδων.

Δεν απαιτούνται εξωτερικά εργαλεία κατασκευής· όλα εκτελούνται στον περιηγητή με ένα μόνο script tag. Ας ξεκινήσουμε.

## Προαπαιτήσεις

Πριν βουτήξουμε, βεβαιωθείτε ότι έχετε:

1. Έναν σύγχρονο περιηγητή (Chrome, Edge, Firefox, Safari) – οτιδήποτε υποστηρίζει ES6.
2. Βασικές γνώσεις HTML και JavaScript – δεν χρειάζεστε κάποιο framework.
3. Πρόσβαση στη βιβλιοθήκη Gridjs – θα την πάρουμε από CDN, οπότε δεν χρειάζεται εγκατάσταση npm.

Αυτό είναι όλο. Αν έχετε ήδη μια σελίδα που θέλετε να βελτιώσετε, μπορείτε να επικολλήσετε τα αποσπάσματα κατευθείαν.

## Βήμα 1: Προσθήκη Πόρων Gridjs στη Σελίδα Σας

Πρώτα, πρέπει να φορτώσουμε τα αρχεία CSS και JavaScript του Gridjs. Η έκδοση CDN είναι ελαφριά και ιδανική για γρήγορες επιδείξεις.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>How to Create Gridjs Example</title>
  <!-- Gridjs CSS -->
  <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet" />
</head>
<body>
  <!-- The grid will appear inside this div -->
  <div id="grid"></div>

  <!-- Gridjs JS -->
  <script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
```

> **Pro tip:** Το θέμα Mermaid δίνει στον πίνακα μια καθαρή, σύγχρονη εμφάνιση χωρίς επιπλέον CSS. Μπορείτε ελεύθερα να το αντικαταστήσετε με `classic.min.css` αν προτιμάτε διαφορετικό στυλ.

## Βήμα 2: Ορισμός του **gridjs container**

Το **gridjs container** είναι απλώς ένα κανονικό `<div>` που θα φιλοξενήσει τον αποδοθέντα πίνακα. Στο παραπάνω markup έχουμε ήδη δημιουργήσει `<div id="grid"></div>`. Το χαρακτηριστικό `id` είναι κρίσιμο επειδή θα το χρησιμοποιήσουμε για τη σύνδεση της παρουσίας Gridjs αργότερα.

Αν χρειάζεστε πολλαπλά grids στην ίδια σελίδα, δώστε σε κάθε container ένα μοναδικό ID (`grid1`, `grid2`, …) και επαναλάβετε τη λογική σύνδεσης για το καθένα.

## Βήμα 3: Δημιουργία ενός **gridjs configuration** Object

Τώρα έρχεται η καρδιά του **πώς να δημιουργήσετε gridjs** – η ρύθμιση. Αυτό το απλό αντικείμενο JavaScript λέει στο Gridjs ποιες στήλες να εμφανίσει, ποια δεδομένα να γεμίσει και ποιες λειτουργίες να ενεργοποιήσει.

```html
<script>
  // Step 3: Your gridjs configuration (replace with real data)
  const config = {
    columns: [
      { name: 'ID', width: '50px' },
      { name: 'Name' },
      { name: 'Email' },
      { name: 'Role' }
    ],
    data: [
      [1, 'Alice Johnson', 'alice@example.com', 'Admin'],
      [2, 'Bob Smith', 'bob@example.com', 'Editor'],
      [3, 'Carol White', 'carol@example.com', 'Viewer'],
      [4, 'David Brown', 'david@example.com', 'Admin']
    ],
    pagination: {
      limit: 2   // Show 2 rows per page
    },
    search: true,          // Enable client‑side search box
    sort: true,            // Allow column sorting
    language: {
      'search': {
        'placeholder': '🔍 Search…'
      },
      'pagination': {
        'previous': '←',
        'next': '→',
        'showing': 'Showing',
        'results': () => 'records'
      }
    }
  };
</script>
```

### Γιατί αυτή η ρύθμιση είναι σημαντική

- **Columns** – ορίζουν το κείμενο της κεφαλίδας και προαιρετικό πλάτος. Χωρίς αυτό, το Gridjs θα προσπαθήσει να εξαχθεί τα ονόματα των στηλών από την πρώτη σειρά δεδομένων, κάτι που συχνά είναι λιγότερο αναγνώσιμο.
- **Data** – ένας πίνακας σειρών, κάθε σειρά είναι ένας πίνακας τιμών κελιών. Μπορείτε επίσης να παρέχετε μια ασύγχρονη συνάρτηση που φέρνει δεδομένα από ένα API· η βιβλιοθήκη θα διαχειριστεί τις υποσχέσεις αυτόματα.
- **Pagination** – περιορίζει τις σειρές ανά σελίδα, αποτρέποντας τεράστιους πίνακες από το να κατακλύσουν το UI.
- **Search & Sort** – ενεργοποιεί διαδραστικές λειτουργίες με ένα μόνο boolean, εξοικονομώντας σας την ανάγκη για προσαρμοσμένους χειριστές.
- **Language** – προσαρμόζει τις συμβολοσειρές του UI, ιδανικό για τοπικοποίηση ή branding.

Αισθανθείτε ελεύθεροι να αντικαταστήσετε τον στατικό πίνακα δεδομένων με μια κλήση fetch αργότερα· τα υπόλοιπα βήματα παραμένουν ακριβώς τα ίδια.

## Βήμα 4: Δημιουργία Παρουσίας Gridjs και Σύνδεση με το **gridjs container**

Με τη ρύθμιση έτοιμη, δημιουργούμε ένα νέο `GridJs.Grid` (το όνομα της κλάσης είναι `gridjs.Grid` στην έκδοση UMD) και το συνδέουμε με το στοιχείο container μας.

```html
<script>
  // Step 4: Create a Gridjs instance bound to the container
  const grid = new gridjs.Grid(document.getElementById('grid'), config);
</script>
```

Παρατηρήστε ότι χρησιμοποιήσαμε `document.getElementById('grid')`—αυτό είναι το **gridjs container** που ορίσαμε νωρίτερα. Αν έχετε πολλαπλά **containers**, απλώς επαναλάβετε αυτή τη γραμμή με το αντίστοιχο ID.

## Βήμα 5: Ενεργοποίηση της κλήσης **gridjs render**

Το τελευταίο κομμάτι του παζλ είναι η μέθοδος **gridjs render**. Λαμβάνει τη ρύθμιση που περάσαμε προηγουμένως και ενσωματώνει ένα πλήρως στυλιζαρισμένο `<table>` στο container.

```html
<script>
  // Step 5: Render the grid inside the container
  grid.render();
</script>
</body>
</html>
```

Αυτό είναι! Όταν ανοίξετε τη σελίδα σε έναν περιηγητή, θα δείτε έναν αναζητήσιμο, σελιδοποιημένο πίνακα με τις τέσσερις σειρές που ορίσαμε. Το πεδίο αναζήτησης εμφανίζεται αυτόματα στην κορυφή, και οι έλεγχοι σελιδοποίησης βρίσκονται στο κάτω μέρος.

### Αναμενόμενο Αποτέλεσμα

```
+----+----------------+---------------------+--------+
| ID | Name           | Email               | Role   |
+----+----------------+---------------------+--------+
| 1  | Alice Johnson  | alice@example.com   | Admin  |
| 2  | Bob Smith      | bob@example.com     | Editor |
+----+----------------+---------------------+--------+
[←] [1] [2] [→]   Search: 🔍 Search…
```

Το UI θα προσαρμόζεται όταν πληκτρολογείτε στο πεδίο αναζήτησης ή κάνετε κλικ στις κεφαλίδες των στηλών για ταξινόμηση.

## Κοινές Παραλλαγές & Ακραίες Περιπτώσεις

### Φόρτωση Δεδομένων Ασύγχρονα

Αν τα δεδομένα σας βρίσκονται σε διακομιστή, αντικαταστήστε τον στατικό πίνακα `data` με μια συνάρτηση που επιστρέφει ένα Promise:

```js
const config = {
  columns: ['ID', 'Name', 'Email', 'Role'],
  data: () => fetch('/api/users')
                .then(res => res.json())
                .then(users => users.map(u => [u.id, u.name, u.email, u.role])),
  pagination: { limit: 10 },
  search: true,
  sort: true
};
```

Το Gridjs θα εμφανίσει ένα spinner φόρτωσης μέχρι να επιλυθεί η υπόσχεση, και στη συνέχεια θα αποδώσει τον πίνακα αυτόματα.

### Προσαρμοσμένη Απόδοση Κελιών

Μερικές φορές χρειάζεστε εικονίδια, κουμπιά ή μορφοποιημένες ημερομηνίες μέσα σε κελιά. Χρησιμοποιήστε την ιδιότητα `formatter` σε μια στήλη:

```js
{
  name: 'Role',
  formatter: (cell) => {
    const color = cell === 'Admin' ? 'red' : 'gray';
    return gridjs.h('span', { style: { color } }, cell);
  }
}
```

Η βοηθητική συνάρτηση `gridjs.h` δημιουργεί εικονικά στοιχεία DOM χωρίς να απαιτείται React.

### Πολλαπλά Grids σε Μία Σελίδα

Απλώς επαναλάβετε τα βήματα 2‑5 με διαφορετικά IDs container:

```html
<div id="usersGrid"></div>
<div id="ordersGrid"></div>

<script>
  const usersGrid = new gridjs.Grid(document.getElementById('usersGrid'), usersConfig);
  const ordersGrid = new gridjs.Grid(document.getElementById('ordersGrid'), ordersConfig);
  usersGrid.render();
  ordersGrid.render();
</script>
```

Κάθε grid λειτουργεί ανεξάρτητα, ώστε μπορείτε να συνδυάσετε διαφορετικά όρια σελιδοποίησης, σύνολα στηλών και ακόμη και θέματα.

## Pro Tips & Παγίδες που Πρέπει να Αποφύγετε

- **Μην ξεχνάτε το CSS** – χωρίς το stylesheet ο πίνακας θα εμφανιστεί ως απλός HTML πίνακας, χάνοντας όλο το ωραίο στυλ και τους ελέγχους σελιδοποίησης.
- **Αποφύγετε διπλά IDs** – κάθε **gridjs container** πρέπει να έχει μοναδικό ID· διαφορετικά το Gridjs θα αντικαταστήσει την πρώτη παρουσία.
- **Προσέξτε τη δομή των δεδομένων** – ο αριθμός των στηλών πρέπει να ταιριάζει με τον αριθμό των κελιών σε κάθε σειρά· ασυμφωνίες προκαλούν σιωπηλά σφάλματα διάταξης.
- **Χρησιμοποιήστε `gridjs.h` για σύνθετα κελιά** – η εισαγωγή ακατέργαστων HTML strings μπορεί να διακόψει τον αλγόριθμο diff του εικονικού DOM.
- **Προσοχή στην έκδοση** – ο σύνδεσμος CDN παραπάνω δείχνει την τελευταία έκδοση 5.x (ως Ιούνιος 2026). Αν κλειδώσετε σε παλαιότερη έκδοση, ορισμένες επιλογές (όπως `language`) μπορεί να λείπουν.

## Πλήρες Παράδειγμα Λειτουργίας (Copy‑Paste)

Παρακάτω βρίσκεται το πλήρες αρχείο HTML που μπορείτε να αποθηκεύσετε ως `gridjs-demo.html` και να ανοίξετε απευθείας σε έναν περιηγητή.



## Τι Πρέπει Να Μάθετε Στη Σύντομη Μελλοντική

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικά παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Aspose.Cells for Java&#58; How to Create and Format Excel Workbooks Efficiently](/cells/english/java/getting-started/aspose-cells-java-workbook-creation-guide/)
- [How to Create and Export Excel to HTML Using Aspose.Cells Java | Workbook Operations Guide](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [How to Create and Merge Excel Workbooks Using Aspose.Cells for Java | Complete Guide](/cells/english/java/workbook-operations/create-merge-excel-workbooks-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}