---
category: general
date: 2026-06-21
description: Μάθετε πώς να αλλάζετε τη γραμματοσειρά του πεδίου κειμένου, να ορίζετε
  το χρώμα της γραμματοσειράς προγραμματιστικά και να προσαρμόζετε το μέγεθος της
  γραμματοσειράς σε κελί πλέγματος. Ακολουθήστε αυτό το πρακτικό σεμινάριο για το
  στυλ των πεδίων κειμένου.
draft: false
keywords:
- change textbox font
- change font size cell
- how to style textbox
- set font color programmatically
- change font family grid
language: el
og_description: Αλλάξτε γρήγορα τη γραμματοσειρά του πεδίου κειμένου σε ένα πλέγμα.
  Αυτός ο οδηγός δείχνει πώς να μορφοποιήσετε το πεδίο κειμένου, να ορίσετε το χρώμα
  της γραμματοσειράς προγραμματιστικά και να προσαρμόσετε το μέγεθος του κελιού με
  σαφή κώδικα.
og_title: Αλλαγή γραμματοσειράς πεδίου κειμένου σε πλέγμα – Πλήρης οδηγός προγραμματισμού
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Learn how to change textbox font, set font color programmatically and
    adjust font size cell in a grid. Follow this practical tutorial for styling textboxes.
  headline: Change Textbox Font in a Grid – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Learn how to change textbox font, set font color programmatically and
    adjust font size cell in a grid. Follow this practical tutorial for styling textboxes.
  name: Change Textbox Font in a Grid – Complete Step‑by‑Step Guide
  steps:
  - name: Breaking Down the Object
    text: '| Property | Purpose | Example Values | |----------|---------|----------------|
      | `family` | Font family – controls the typeface. | `"Arial"`, `"Helvetica"`,
      `"Courier New"` | | `size` | Font size in pixels (or points, depending on the
      grid). | `12`, `14`, `16` | | `color` | Text color in any CSS‑co'
  - name: Expected Output
    text: '- The textbox located at **row 2, column 3** now displays text in **Arial**,
      **14 px**, and a **#0066CC** blue hue. - Opening the browser console will print
      something like:'
  - name: Can I change only the font size without affecting family or color?
    text: 'Absolutely. Just omit the properties you don’t want to modify:'
  - name: What if my grid uses a different property name for the textbox?
    text: Inspect the cell object in the console (`console.log(cell)`). You’ll likely
      see something like `cell.editor` or `cell.input`. Replace `cell.textbox` with
      the correct reference.
  - name: How do I apply the same style to an entire column?
    text: 'Loop through the rows and set the font for each cell in that column:'
  - name: Is there a way to revert to the original font?
    text: 'Store the original style before overwriting:'
  type: HowTo
tags:
- JavaScript
- UI‑grid
- DOM‑manipulation
title: Αλλαγή γραμματοσειράς πλαισίου κειμένου σε πλέγμα – Πλήρης οδηγός βήμα‑προς‑βήμα
url: /el/net/working-with-fonts-in-spreadsheets/change-textbox-font-in-a-grid-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Αλλαγή Γραμματοσειράς Πεδίου Κειμένου σε Πλέγμα – Οδηγός Βήμα‑βήμα

Έχετε χρειαστεί ποτέ να **αλλάξετε τη γραμματοσειρά του πεδίου κειμένου** μέσα σε ένα πλέγμα δεδομένων αλλά δεν ήξερατε ποια ιδιότητα να τροποποιήσετε; Δεν είστε μόνοι—πολλοί προγραμματιστές αντιμετωπίζουν αυτό το πρόβλημα όταν δημιουργούν επεξεργάσιμους πίνακες ή dashboards. Σε αυτό το tutorial θα περάσουμε από το πώς να αλλάξετε τη γραμματοσειρά του πεδίου κειμένου, να ορίσετε το χρώμα του προγραμματιστικά, και ακόμη να ρυθμίσετε το μέγεθος της γραμματοσειράς κελί‑με‑κελί.

Θα προσθέσουμε επίσης συμβουλές για **πώς να μορφοποιήσετε τα πεδία κειμένου**, θα καλύψουμε σενάρια **αλλαγής μεγέθους γραμματοσειράς κελιού**, και θα σας δείξουμε πώς να **ορίσετε το χρώμα γραμματοσειράς προγραμματιστικά** χωρίς να τρελαίνεστε. Στο τέλος θα έχετε ένα επαναχρησιμοποιήσιμο snippet που λειτουργεί με οποιοδήποτε component πλέγματος που εκθέτει ένα API `getCell`.

## Προαπαιτούμενα

- Ένα σύγχρονο πρόγραμμα περιήγησης με υποστήριξη ES6 (Chrome, Edge, Firefox, Safari)
- Μια βιβλιοθήκη πλέγματος που προσφέρει `grid.getCell(row, col)` και επιστρέφει ένα αντικείμενο κελιού που περιέχει μια αναφορά `textbox`
- Βασική γνώση αντικειμένων JavaScript και ιδιοτήτων CSS

Δεν απαιτούνται επιπλέον πακέτα—μόνο απλό JavaScript και το δικό του API του πλέγματος.

## Επισκόπηση της Λύσης

Η βασική ιδέα είναι απλή: να εντοπίσετε το στόχο κελιού, να πάρετε το ενσωματωμένο πεδίο κειμένου, και στη συνέχεια να του αναθέσετε ένα νέο αντικείμενο γραμματοσειράς που ορίζει οικογένεια, μέγεθος και χρώμα. Σκεφτείτε το σαν να δίνετε στο πεδίο κειμένου ένα νέο ντύσιμο. Παρακάτω είναι η υψηλού επιπέδου ροή:

1. **Πρόσβαση στο στόχο κελιού** – εντοπίστε τη γραμμή/στήλη που θέλετε.
2. **Ανάκτηση του πεδίου κειμένου** – το UI στοιχείο που κρατά το κείμενο.
3. **Δημιουργία αντικειμένου στυλ γραμματοσειράς** – καθορίστε οικογένεια, μέγεθος και χρώμα.
4. **Εφαρμογή του στυλ** – αναθέστε το αντικείμενο στην ιδιότητα `font` του πεδίου κειμένου.

Αυτό είναι. Ας βουτήξουμε σε κάθε βήμα, να εξηγήσουμε γιατί είναι σημαντικό, και να δούμε τον κώδικα σε δράση.

![Screenshot of a grid cell with a styled textbox – change textbox font](/images/change-textbox-font-example.png)

## Βήμα 1: Πρόσβαση στο Στόχο Κελιού στο Πλέγμα

```javascript
// Step 1: Access the target cell in the grid
const cell = grid.getCell(2, 3);
```

> **Γιατί είναι σημαντικό:**  
> Τα πλέγματα συχνά αποθηκεύουν γραμμές και στήλες ως δείκτες που ξεκινούν από το μηδέν. Καλώντας `grid.getCell(2, 3)` παίρνουμε το κελί στη **γραμμή 2, στήλη 3**. Αν χρειάζεστε να **αλλάξετε το μέγεθος γραμματοσειράς κελιού** για άλλη θέση, απλώς προσαρμόστε τους δείκτες.

**Συμβουλή:** Αν το πλέγμα σας υποστηρίζει ονομαστικές στήλες, μπορείτε να αντικαταστήσετε τη αριθμητική στήλη με ένα κλειδί, π.χ., `grid.getCell(2, "price")`.

## Βήμα 2: Λήψη του Πεδίου Κειμένου Μέσα στο Κελί

```javascript
// Step 2: Get the textbox contained in that cell
const textbox = cell.textbox;
```

> **Τι συμβαίνει:**  
> Οι περισσότερες υλοποιήσεις πλέγματος τυλίγουν το επεξεργάσιμο περιεχόμενο μέσα σε ένα στοιχείο `<input>` ή `<textarea>` και το εκθέτουν ως `cell.textbox`. Η λήψη της αναφοράς μας επιτρέπει να χειριστούμε το στυλ του άμεσα.

Αν το πλέγμα χρησιμοποιεί διαφορετικό όνομα ιδιότητας (π.χ. `cell.editor`), προσαρμόστε τον κώδικα ανάλογα—αυτή είναι μια συνηθισμένη παραλλαγή όταν **πώς να μορφοποιήσετε το πεδίο κειμένου** για ένα προσαρμοσμένο component.

## Βήμα 3: Ορισμός των Επιθυμητών Ιδιοτήτων Γραμματοσειράς

```javascript
// Step 3: Define the desired font properties
const fontStyle = {
  family: "Arial",          // change font family grid
  size: 14,                 // change font size cell
  color: "#0066CC"          // set font color programmatically
};
```

### Ανάλυση του Αντικειμένου

| Ιδιότητα | Σκοπός | Παραδείγματα Τιμών |
|----------|--------|--------------------|
| `family` | Οικογένεια γραμματοσειράς – ελέγχει το στυλ του κειμένου. | `"Arial"`, `"Helvetica"`, `"Courier New"` |
| `size`   | Μέγεθος γραμματοσειράς σε pixels (ή points, ανάλογα με το πλέγμα). | `12`, `14`, `16` |
| `color`  | Χρώμα κειμένου σε οποιαδήποτε μορφή CSS. | `"#0066CC"`, `"rgb(255,0,0)"`, `"navy"` |

> **Γιατί χρησιμοποιούμε αντικείμενο:**  
> Η ομαδοποίηση των τριών χαρακτηριστικών κάνει τον κώδικα πιο καθαρό και αντικατοπτρίζει τον τρόπο που πολλές βιβλιοθήκες UI αναμένουν τις πληροφορίες στυλ. Επιτρέπει επίσης να **αλλάξετε την οικογένεια γραμματοσειράς πλέγματος** ή **να ορίσετε το χρώμα γραμματοσειράς προγραμματιστικά** με μία μόνο ανάθεση.

## Βήμα 4: Εφαρμογή του Στυλ Γραμματοσειράς στο Πεδίο Κειμένου

```javascript
// Step 4: Apply the font style to the textbox
textbox.font = fontStyle;
```

> **Πίσω από τη σκηνή:**  
> Το component πεδίου κειμένου του πλέγματος ερμηνεύει την ιδιότητα `font` και ενημερώνει το CSS του ανάλογα. Αυτή η μοναδική γραμμή αντικαθιστά την προηγούμενη οικογένεια, μέγεθος και χρώμα σε ένα βήμα—ακριβώς ό,τι χρειάζεστε όταν **αλλάζετε τη γραμματοσειρά του πεδίου κειμένου** σε πολλά κελιά.

Αν το component χρησιμοποιεί διαφορετικό API (π.χ. `textbox.style.fontFamily = ...`), προσαρμόστε την ανάθεση αλλά διατηρήστε την ίδια λογική.

## Πλήρες Παράδειγμα Λειτουργίας

Παρακάτω υπάρχει ένα αυτόνομο snippet που μπορείτε να επικολλήσετε σε ένα αρχείο HTML που περιλαμβάνει ένα mock αντικείμενο πλέγματος. Δείχνει ολόκληρη τη ροή από το βήμα 1 έως το βήμα 4, καθώς και μια γρήγορη επαλήθευση ότι το στυλ άλλαξε.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Change Textbox Font Demo</title>
  <style>
    .grid { display: table; border-collapse: collapse; }
    .grid .row { display: table-row; }
    .grid .cell { display: table-cell; border: 1px solid #ccc; padding: 8px; }
    .grid .cell input { width: 100%; border: none; }
  </style>
</head>
<body>

<div id="myGrid" class="grid"></div>

<script>
/* ---------- Mock Grid Implementation ---------- */
class MockGrid {
  constructor(rows, cols) {
    this.rows = rows;
    this.cols = cols;
    this.el = document.getElementById('myGrid');
    this._build();
  }
  _build() {
    for (let r = 0; r < this.rows; r++) {
      const rowDiv = document.createElement('div');
      rowDiv.className = 'row';
      for (let c = 0; c < this.cols; c++) {
        const cellDiv = document.createElement('div');
        cellDiv.className = 'cell';
        const input = document.createElement('input');
        input.type = 'text';
        input.value = `R${r}C${c}`;
        // expose textbox via a custom property
        cellDiv.textbox = input;
        cellDiv.appendChild(input);
        rowDiv.appendChild(cellDiv);
      }
      this.el.appendChild(rowDiv);
    }
  }
  getCell(row, col) {
    const rowDiv = this.el.children[row];
    if (!rowDiv) return null;
    const cellDiv = rowDiv.children[col];
    return cellDiv || null;
  }
}

/* ---------- Use the Grid ---------- */
const grid = new MockGrid(5, 5); // 5x5 grid for demo

// ---- Change Textbox Font (the core tutorial steps) ----
const cell = grid.getCell(2, 3);          // step 1
const textbox = cell.textbox;             // step 2
const fontStyle = {                      // step 3
  family: "Arial",
  size: 14,
  color: "#0066CC"
};
textbox.font = fontStyle;                // step 4

// Verify by logging computed style
setTimeout(() => {
  const cs = window.getComputedStyle(textbox);
  console.log('Applied font family:', cs.fontFamily);
  console.log('Applied font size:', cs.fontSize);
  console.log('Applied color:', cs.color);
}, 0);
</script>
</body>
</html>
```

### Αναμενόμενο Αποτέλεσμα

- Το πεδίο κειμένου στη **γραμμή 2, στήλη 3** εμφανίζει τώρα κείμενο σε **Arial**, **14 px**, και απόχρωση **#0066CC** μπλε.
- Το console του προγράμματος περιήγησης θα εκτυπώσει κάτι σαν:

```
Applied font family: Arial, Helvetica, sans-serif
Applied font size: 14px
Applied color: rgb(0, 102, 204)
```

Αν ανοίξετε τη σελίδα, θα δείτε οπτικά την αλλαγή—χωρίς πια την προεπιλεγμένη γραμματοσειρά του συστήματος.

## Συχνές Ερωτήσεις (FAQ)

### Μπορώ να αλλάξω μόνο το μέγεθος γραμματοσειράς χωρίς να επηρεάσω την οικογένεια ή το χρώμα;
Απολύτως. Απλώς παραλείψτε τις ιδιότητες που δεν θέλετε να τροποποιήσετε:

```javascript
textbox.font = { size: 18 }; // only changes size
```

### Τι γίνεται αν το πλέγμα μου χρησιμοποιεί διαφορετικό όνομα ιδιότητας για το πεδίο κειμένου;
Εξετάστε το αντικείμενο κελιού στην κονσόλα (`console.log(cell)`). Πιθανότατα θα δείτε κάτι όπως `cell.editor` ή `cell.input`. Αντικαταστήστε το `cell.textbox` με τη σωστή αναφορά.

### Πώς εφαρμόζω το ίδιο στυλ σε ολόκληρη μια στήλη;
Κάντε βρόχο στις γραμμές και ορίστε τη γραμματοσειρά για κάθε κελί σε αυτή τη στήλη:

```javascript
for (let r = 0; r < grid.rowCount; r++) {
  const colCell = grid.getCell(r, 3);
  colCell.textbox.font = fontStyle; // reuse the same fontStyle object
}
```

### Υπάρχει τρόπος να επαναφέρω την αρχική γραμματοσειρά;
Αποθηκεύστε το αρχικό στυλ πριν το αντικαταστήσετε:

```javascript
const original = { ...textbox.font };
textbox.font = fontStyle; // apply new style
// later...
textbox.font = original; // revert
```

## Συμβουλές & Καλές Πρακτικές

- **Ομαδοποιημένες ενημερώσεις:** Αν χρειάζεται να μορφοποιήσετε πολλά κελιά, τυλίξτε τις αλλαγές σε `requestAnimationFrame` ή σε μια μέθοδο batch του πλέγματος για να αποφύγετε “layout thrashing”.
- **Ανταποκρινόμενες γραμματοσειρές:** Χρησιμοποιήστε σχετικές μονάδες (`em`, `rem`) αντί για σταθερά pixels αν το UI σας πρέπει να κλιμακώνεται.
- **Προσβασιμότητα:** Εξασφαλίστε επαρκή αντίθεση όταν **ορίζετε το χρώμα γραμματοσειράς προγραμματιστικά**—το ελάχιστο WCAG AA είναι λόγος 4.5:1 για κανονικό κείμενο.
- **Προβλήματα σε παλαιότερα browsers:** Κάποια παλιά πλέγματα μπορεί να απαιτούν την άμεση ρύθμιση `style.fontFamily` στο στοιχείο `<input>` αντί για αντικείμενο `font`.

## Συμπέρασμα

Καλύψαμε πώς να **αλλάξετε τη γραμματοσειρά του πεδίου κειμένου** μέσα σε ένα πλέγμα, από την ανάκτηση του σωστού κελιού μέχρι τον ορισμό ενός επαναχρησιμοποιήσιμου αντικειμένου `fontStyle` και την εφαρμογή του με μία γραμμή κώδικα. Στο δρόμο αυτό, μάθαμε επίσης πώς να **αλλάξετε το μέγεθος γραμματοσειράς κελιού**, **να ορίσετε το χρώμα γραμματοσειράς προγραμματιστικά**, και ακόμη να **αλλάξετε την οικογένεια γραμματοσειράς πλέγματος** για μια συγκεκριμένη στήλη.

Τώρα μπορείτε να προσαρμόσετε αυτό το μοτίβο σε οποιαδήποτε βιβλιοθήκη UI—είτε χτίζετε ένα admin dashboard, έναν επεξεργαστή τύπου spreadsheet, ή ένα προσαρμοσμένο εργαλείο αναφορών. Πειραματιστείτε με διαφορετικές οικογένειες, μεγέθη και χρώματα· ίσως προσθέσετε εφέ hover ή υπό συνθήκες στυλ βάσει τιμών δεδομένων.

Έχετε άλλη πρόκληση στυλ; Αφήστε ένα σχόλιο και ας το αντιμετωπίσουμε μαζί. Καλό coding!

## Τι Θα Μάθεις Στη Σειρά Επόμενη;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετα χαρακτηριστικά API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στην υλοποίηση.

- [How to Change Font Color in Excel Using Aspose.Cells for Java&#58; A Complete Guide](/cells/english/java/formatting/change-font-color-aspose-cells-java-tutorial/)
- [Change Font Color Aspose Cells Java Tutorial](/cells/german/java/formatting/change-font-color-aspose-cells-java-tutorial/)
- [Change Font Color Aspose Cells Java Tutorial](/cells/french/java/formatting/change-font-color-aspose-cells-java-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}