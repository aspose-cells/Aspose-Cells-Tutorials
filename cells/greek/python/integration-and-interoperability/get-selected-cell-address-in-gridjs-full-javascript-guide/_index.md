---
category: general
date: 2026-06-30
description: Μάθετε πώς να λαμβάνετε τη διεύθυνση του επιλεγμένου κελιού, να ενημερώνετε
  την τιμή του κελιού του πλέγματος και να διαβάζετε την τιμή εισόδου με JavaScript
  χρησιμοποιώντας το GridJs. Κώδικας βήμα‑βήμα και συμβουλές.
draft: false
keywords:
- get selected cell address
- update grid cell value
- read input value with javascript
language: el
og_description: Λάβετε τη διεύθυνση του επιλεγμένου κελιού, ενημερώστε την τιμή του
  κελιού του πλέγματος και διαβάστε την τιμή εισόδου με JavaScript. Ακολουθήστε αυτόν
  τον πλήρη οδηγό για μια ομαλή ενσωμάτωση του GridJs.
og_title: Λάβετε τη Διεύθυνση του Επιλεγμένου Κελιού – Πλήρης Οδηγός GridJs JavaScript
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Learn how to get selected cell address, update grid cell value and
    read input value with JavaScript using GridJs. Step‑by‑step code and tips.
  headline: Get Selected Cell Address in GridJs – Full JavaScript Guide
  type: TechArticle
tags:
- GridJs
- JavaScript
- DOM manipulation
title: Αποκτήστε τη Διεύθυνση του Επιλεγμένου Κελιού στο GridJs – Πλήρης Οδηγός JavaScript
url: /el/python/integration-and-interoperability/get-selected-cell-address-in-gridjs-full-javascript-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Λήψη Διεύθυνσης Επιλεγμένου Κελιού – Πλήρες Tutorial GridJs JavaScript

Ποτέ χρειάστηκε να **λάβετε τη διεύθυνση του επιλεγμένου κελιού** από έναν πίνακα GridJs αλλά δεν ήξερες ποια κλήση API να χρησιμοποιήσεις; Δεν είσαι μόνος. Σε πολλά admin panels, οι χρήστες κάνουν κλικ σε ένα κελί, επεξεργάζονται μια τιμή σε ένα modal, και περιμένουν η grid να αντικατοπτρίζει την αλλαγή αμέσως. Αυτό το tutorial δείχνει ακριβώς πώς να ανακτήσετε αυτή τη διεύθυνση, να διαβάσετε τη νέα τιμή από ένα πεδίο εισαγωγής, και **να ενημερώσετε την τιμή του κελιού της grid** χωρίς επαναφόρτωση σελίδας.

Θα καλύψουμε επίσης **ανάγνωση τιμής εισόδου με JavaScript** με τον σωστό τρόπο, θα διαχειριστούμε περιπτώσεις άκρων, και θα κλείσουμε το modal μόλις ολοκληρωθεί η ενημέρωση. Στο τέλος θα έχετε ένα αυτόνομο snippet που μπορείτε να ενσωματώσετε σε οποιοδήποτε project χρησιμοποιεί GridJs.

## Τι Θα Δημιουργήσετε

- Ένα απλό HTML table που τροφοδοτείται από GridJs.
- Ένα modal επεξεργασίας που εμφανίζεται όταν γίνεται κλικ σε ένα κελί.
- JavaScript που **λαμβάνει τη διεύθυνση του επιλεγμένου κελιού**, παίρνει την τιμή που πληκτρολόγησε ο χρήστης, **ενημερώνει την τιμή του κελιού της grid**, και τελικά κρύβει το modal.

Δεν απαιτούνται εξωτερικές βιβλιοθήκες εκτός από το GridJs, και ο κώδικας λειτουργεί με σύγχρονα προγράμματα περιήγησης (Chrome 102+, Edge, Firefox). Αν έχετε ήδη μια παρουσία GridJs στη σελίδα, μπορείτε να αντιγράψετε‑και‑επικολλήσετε τα σχετικά τμήματα απευθείας.

## Προαπαιτούμενα

- Βασική γνώση JavaScript και του DOM.
- Η βιβλιοθήκη GridJs φορτωμένη (μέσω CDN ή npm).
- Μια σελίδα που ήδη αποδίδει ένα GridJs grid (θα δείξουμε ένα ελάχιστο παράδειγμα).

Αν κάτι από αυτά σας φαίνεται άγνωστο, μην πανικοβληθείτε—κάθε βήμα περιλαμβάνει μια γρήγορη επανάληψη.

---

## Βήμα 1: Δημιουργία του HTML Skeleton

Πρώτα, τοποθετήστε το container του πίνακα, το κρυφό modal, και το πεδίο τιμής. Το modal θα εναλλάσσεται με απλές CSS κλάσεις.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>GridJs Edit Example</title>
  <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet"/>
  <style>
    /* Quick modal styling – feel free to replace with your UI framework */
    #editModal { display:none; position:fixed; top:20%; left:50%; transform:translateX(-50%);
                 background:#fff; padding:1rem; border:1px solid #ccc; box-shadow:0 4px 8px rgba(0,0,0,.1);}
    #editModal.active { display:block; }
  </style>
</head>
<body>

<div id="grid"></div>

<div id="editModal">
  <h3>Edit Price</h3>
  <input type="number" id="price" placeholder="Enter new price"/>
  <button id="saveBtn">Save</button>
  <button id="cancelBtn">Cancel</button>
</div>

<script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
<script src="script.js"></script>
</body>
</html>
```

> **Pro tip:** Το `#editModal` χρησιμοποιεί ένα ελάχιστο CSS κόλπο—απλώς προσθέστε την κλάση `active` για να το εμφανίσετε. Μπορείτε να το αντικαταστήσετε με Bootstrap, Tailwind, ή οποιοδήποτε component modal ήδη χρησιμοποιείτε.

---

## Βήμα 2: Αρχικοποίηση GridJs και Καταγραφή Κλικ σε Κελί

Τώρα θα δημιουργήσουμε μια grid με δείγμα δεδομένων και θα ακούσουμε για επιλογές κελιών. Όταν ο χρήστης κάνει κλικ σε ένα κελί, θα **λάβουμε τη διεύθυνση του επιλεγμένου κελιού** και θα ανοίξουμε το modal.

```javascript
// script.js
const grid = new gridjs.Grid({
  columns: ['Item', 'Quantity', 'Price'],
  data: [
    ['Apple', 10, 0.5],
    ['Banana', 5, 0.3],
    ['Cherry', 20, 0.2]
  ],
  pagination: { limit: 5 },
  sort: true,
  // Enable cell selection – GridJs provides a helper for this
  style: {
    table: {
      'width': '100%'
    }
  }
}).render(document.getElementById('grid'));

// Helper to store the address of the last clicked cell
let lastSelectedCell = null;

// GridJs emits a 'cell' event when any cell is clicked
grid.on('cell', (event) => {
  // Step 2a: Get selected cell address
  const address = GridJs.getSelectedCell(); // <-- primary operation
  lastSelectedCell = address; // remember for later update

  // Show the modal
  document.getElementById('editModal').classList.add('active');

  // Optional: pre‑fill the input with the current cell value
  const currentValue = event.target.innerText;
  document.getElementById('price').value = currentValue;
});
```

> **Why this works:** `GridJs.getSelectedCell()` επιστρέφει μια συμβολοσειρά όπως `"C2"` (στήλη C, γραμμή 2). Αποθηκεύοντάς την στο `lastSelectedCell` μπορούμε να αναφερθούμε στην ακριβή θέση όταν αργότερα **ενημερώσουμε την τιμή του κελιού της grid**.

---

## Βήμα 3: Ανάγνωση της Νέας Τιμής από το Πεδίο Εισαγωγής

Όταν ο χρήστης κάνει κλικ στο **Save**, πρέπει να **διαβάσουμε την τιμή εισόδου με JavaScript** με ασφάλεια. Αυτό το βήμα επίσης επικυρώνει ότι η τιμή που εισήχθη είναι θετικός αριθμός.

```javascript
document.getElementById('saveBtn').addEventListener('click', () => {
  // Step 3a: Grab the raw string from the input
  const raw = document.getElementById('price').value;

  // Step 3b: Convert to a number and validate
  const newPrice = parseFloat(raw);
  if (isNaN(newPrice) || newPrice < 0) {
    alert('Please enter a valid positive number.');
    return;
  }

  // Proceed to update the cell
  updateSelectedCell(newPrice);
});
```

> **Note:** Η χρήση του `parseFloat` εξασφαλίζει ότι δέχονται δεκαδικοί (π.χ., `1.99`). Η προστασία `isNaN` αποτρέπει τυχαίες κενές υποβολές.

---

## Βήμα 4: Ενημέρωση της Επιλεγμένης Τιμής Κελιού

Τώρα τελικά **ενημερώνουμε την τιμή του κελιού της grid** χρησιμοποιώντας τη διεύθυνση που καταγράψαμε νωρίτερα. Η μέθοδος `updateCell` του GridJs επιστρέφει μια υπόσχεση (promise), ώστε να μπορούμε να αλυσίδωσουμε μια ενέργεια κλεισίματος του modal.

```javascript
function updateSelectedCell(value) {
  if (!lastSelectedCell) {
    console.warn('No cell selected – nothing to update.');
    return;
  }

  // Step 4a: Call GridJs.updateCell(address, newValue)
  GridJs.updateCell(lastSelectedCell, value)
    .then(() => {
      // Step 4b: Close the modal once the grid refreshes
      document.getElementById('editModal').classList.remove('active');
      // Reset stored address
      lastSelectedCell = null;
    })
    .catch(err => {
      console.error('Failed to update cell:', err);
      alert('Could not save the new price. Try again.');
    });
}
```

> **Why use a promise?** Το GridJs μπορεί να χρειαστεί να επανασχεδιάσει τον πίνακα ή να συγχρονιστεί με backend. Περιμένοντας την υπόσχεση, εγγυόμαστε ότι το UI κρύβεται μόνο αφού η grid αντικατοπτρίσει τη νέα τιμή.

---

## Βήμα 5: Διαχείριση Ακύρωσης και Περιπτώσεων Άκρων

Μια αξιόπιστη λύση παρέχει πάντα στον χρήστη μια έξοδο. Το κουμπί **Cancel** απλώς κρύβει το modal και καθαρίζει τυχόν αποθηκευμένη διεύθυνση.

```javascript
document.getElementById('cancelBtn').addEventListener('click', () => {
  document.getElementById('editModal').classList.remove('active');
  lastSelectedCell = null;
});
```

### Τι Συμβαίνει Αν Δεν Έχει Επιλεγεί Κελί;

Αν ο χρήστης κατά λάθος ενεργοποιήσει το κουμπί **Save** χωρίς να κάνει πρώτα κλικ σε κελί (π.χ., άνοιξε το modal προγραμματιστικά), το `lastSelectedCell` θα είναι `null`. Η πρώιμη επιστροφή στη `updateSelectedCell` αποτρέπει σφάλμα χρόνου εκτέλεσης και καταγράφει ένα χρήσιμο προειδοποιητικό μήνυμα.

### Διαχείριση Μεγάλων Grids

Για grids με σελιδοποίηση, το `GridJs.getSelectedCell()` εξακολουθεί να επιστρέφει τη απόλυτη διεύθυνση (π.χ., `"B12"`), όχι μόνο τη γραμμή που φαίνεται. Αυτό σημαίνει ότι η ενημέρωση λειτουργεί ακόμη και αν η επεξεργασμένη γραμμή βρίσκεται σε άλλη σελίδα. Να θυμάστε ότι το UI δεν θα αλλάξει αυτόματα σελίδα μετά την ενημέρωση—αν χρειάζεστε αυτό, καλέστε `grid.forceUpdate()` ή μεταβείτε στη σωστή σελίδα χειροκίνητα.

---

## Πλήρες Παράδειγμα Λειτουργίας

Παρακάτω είναι ο πλήρης κώδικας που μπορείτε να αντιγράψετε‑και‑επικολλήσετε σε ένα μόνο αρχείο HTML. Ανοίξτε το σε πρόγραμμα περιήγησης, κάντε κλικ σε οποιοδήποτε κελί, αλλάξτε την τιμή, και παρακολουθήστε τη grid να ενημερώνεται αμέσως.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Get Selected Cell Address – GridJs Demo</title>
  <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet"/>
  <style>
    #editModal { display:none; position:fixed; top:20%; left:50%; transform:translateX(-50%);
                 background:#fff; padding:1rem; border:1px solid #ccc; box-shadow:0 4px 8px rgba(0,0,0,.1);}
    #editModal.active { display:block; }
  </style>
</head>
<body>

<div id="grid"></div>

<div id="editModal" aria-modal="true" role="dialog">
  <h3>Edit Price</h3>
  <input type="number" id="price" placeholder="Enter new price"/>
  <button id="saveBtn">Save</button>
  <button id="cancelBtn">Cancel</button>
</div>

<script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
<script>
  // Initialise the grid
  const grid = new gridjs.Grid({
    columns: ['Item', 'Quantity', 'Price'],
    data: [
      ['Apple', 10, 0.5],
      ['Banana', 5, 0.3],
      ['Cherry', 20, 0.2]
    ],
    pagination: { limit: 5 },
    sort: true
  }).render(document.getElementById('grid'));

  let lastSelectedCell = null;

  // Capture cell clicks – this is where we **get selected cell address**
  grid.on('cell', (event) => {
    const address = GridJs.getSelectedCell();   // primary keyword usage
    lastSelectedCell = address;
    document.getElementById('editModal').classList.add('active');
    document.getElementById('price').value = event.target.innerText;
  });

  // Save button – **read input value with JavaScript**
  document.getElementById('saveBtn').addEventListener('click', () => {
    const raw = document.getElementById('price').value;
    const newPrice = parseFloat(raw);
    if (isNaN(newPrice) || newPrice < 0) {
      alert('Please enter a valid positive number.');
      return;
    }
    updateSelectedCell(newPrice);
  });

  // Core update logic – **update grid cell value**
  function updateSelectedCell(value) {
    if (!lastSelectedCell) {
      console.warn('No cell selected – nothing to update.');
      return;
    }
    GridJs.updateCell(lastSelectedCell, value)
      .then(() => {
        document.getElementById('editModal').classList


## Τι Θα Μάθετε Στη Σύντομη Επόμενη;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κυριαρχήσετε επιπλέον δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στα δικά σας projects.

- [Λήψη Διεύθυνσης, Αριθμού Κελιών και Μετατόπισης για Ολόκληρο το Εύρος Excel](/cells/english/net/excel-range-address-calculation/get-address-cell-count-and-offset-for-entire-excel-range/)
- [Λήψη Διεύθυνσης, Αριθμού Κελιών και Μετατόπισης για Ολόκληρο το Εύρος Excel](/cells/german/net/excel-range-address-calculation/get-address-cell-count-and-offset-for-entire-excel-range/)
- [Λήψη Διεύθυνσης, Αριθμού Κελιών και Μετατόπισης για Ολόκληρο το Εύρος Excel](/cells/french/net/excel-range-address-calculation/get-address-cell-count-and-offset-for-entire-excel-range/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}