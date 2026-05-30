---
category: general
date: 2026-05-30
description: Μάθετε πώς να δημιουργήσετε μια παρουσία GridJsOptions και να διαμορφώσετε
  τις επιλογές πλέγματος JavaScript για δυναμικούς πίνακες. Οδηγός βήμα‑βήμα με πλήρη
  κώδικα.
draft: false
keywords:
- create gridjsoptions instance
- configure grid options javascript
- gridjs initialization
- javascript data grid settings
- dynamic table configuration
language: el
og_description: Δημιουργήστε ένα αντικείμενο GridJsOptions και διαμορφώστε τις επιλογές
  του πλέγματος JavaScript σε λίγα λεπτά. Πλήρες παράδειγμα, εξηγήσεις και συμβουλές
  βέλτιστων πρακτικών.
og_title: Δημιουργία Αντικειμένου GridJsOptions – Διαμόρφωση Επιλογών Πλέγματος JavaScript
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Learn how to create GridJsOptions instance and configure grid options
    JavaScript for dynamic tables. Step‑by‑step guide with full code.
  headline: Create GridJsOptions Instance – Configure Grid Options JavaScript
  type: TechArticle
- description: Learn how to create GridJsOptions instance and configure grid options
    JavaScript for dynamic tables. Step‑by‑step guide with full code.
  name: Create GridJsOptions Instance – Configure Grid Options JavaScript
  steps:
  - name: Prerequisites
    text: '- A modern browser (Chrome, Edge, Firefox) – no build tools required. -
      Basic familiarity with JavaScript (variables, objects, DOM). - The Grid.js library
      (we’ll pull it from a CDN).'
  - name: Why this matters
    text: Loading the library from a CDN ensures you always get the latest stable
      version without a local install. The `<div id="grid-wrapper">` is the placeholder
      that the Grid.js constructor will target once we **configure grid options JavaScript**.
  - name: What you’re configuring
    text: '- **NumberFormatAlignment** – aligns numeric strings automatically. - **Pagination**
      – controls page size and navigation. - **Sorting** – toggles column sorting.
      - **Columns** – defines headers, data types, and custom renderers.'
  - name: Edge‑case note
    text: If you later supply a custom data source that already returns paginated
      results, you’ll want to disable Grid.js’s built‑in pagination to avoid double‑paging.
      Simply set `gridOptions.Pagination.enabled = false;`.
  - name: Expected Output
    text: 'When you open the HTML file in a browser you should see:'
  type: HowTo
tags:
- gridjs
- javascript
- data‑grid
title: Δημιουργία Αντικειμένου GridJsOptions – Διαμόρφωση Επιλογών Πλέγματος JavaScript
url: /el/net/link-and-configuration-operations/create-gridjsoptions-instance-configure-grid-options-javascr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία GridJsOptions Instance – Configure Grid Options JavaScript

Ever wondered how to **create GridJsOptions instance** without hunting through scattered docs? You’re not the only one. When you need a slick, sortable table on a web page, mastering how to configure grid options JavaScript is the first step toward a polished UI.

Σε αυτό το tutorial θα περάσουμε από τον ακριβή κώδικα που χρειάζεστε, θα εξηγήσουμε γιατί κάθε ρύθμιση είναι σημαντική, και θα σας δείξουμε ένα πλήρες, εκτελέσιμο παράδειγμα. Στο τέλος θα αισθάνεστε άνετα δημιουργώντας GridJsOptions instance, ρυθμίζοντας την ευθυγράμμιση, την σελιδοποίηση και ακόμη προσαρμοσμένους renderers κελιών—όλα με απλό JavaScript.

## Τι Θα Μάθετε

- Πώς να **create GridJsOptions instance** από το μηδέν.
- Οι βασικές ιδιότητες που σας επιτρέπουν να **configure grid options JavaScript** (ταξινόμηση, σελιδοποίηση, μορφοποίηση αριθμών κ.λπ.).
- Κοινά λάθη (π.χ., ανάμειξη συμβολοσειρών και αριθμητικών τύπων) και πώς να τα αποφύγετε.
- Μια πλήρης σελίδα HTML που μπορείτε να αντιγράψετε‑επικολλήσετε σε οποιοδήποτε έργο και να δείτε τα αποτελέσματα άμεσα.

### Προαπαιτούμενα

- Ένα σύγχρονο πρόγραμμα περιήγησης (Chrome, Edge, Firefox) – χωρίς ανάγκη εργαλείων κατασκευής.
- Βασική εξοικείωση με JavaScript (μεταβλητές, αντικείμενα, DOM).
- Η βιβλιοθήκη Grid.js (θα την πάρουμε από CDN).

Αν κάτι από αυτά σας φαίνεται άγνωστο, μην πανικοβληθείτε—κάθε βήμα περιλαμβάνει μια σύντομη επανάληψη.

---

## Βήμα 1: Φόρτωση Grid.js και Προετοιμασία του Σκελετού HTML

Before we can **create GridJsOptions instance**, we need the library itself. The easiest way is to use the official CDN. Below is a minimal HTML skeleton that also reserves a `<div>` where the grid will render.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Grid.js Demo – Configuring Options</title>
  <!-- Grid.js CSS -->
  <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet" />
</head>
<body>
  <h2>Simple Data Grid</h2>
  <div id="grid-wrapper"></div>

  <!-- Grid.js JS -->
  <script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
  <!-- Our custom script will go here -->
  <script src="grid-config.js"></script>
</body>
</html>
```

> **Pro tip:** Κρατήστε το σύνδεσμο CSS πριν από τα δικά σας στυλ ώστε το προεπιλεγμένο θέμα του grid να φορτώνεται σωστά.

### Γιατί είναι σημαντικό

Loading the library from a CDN ensures you always get the latest stable version without a local install. The `<div id="grid-wrapper">` is the placeholder that the Grid.js constructor will target once we **configure grid options JavaScript**.

## Βήμα 2: Δημιουργία Νέου GridJsOptions Instance

Now comes the heart of the tutorial: the line that actually **creates GridJsOptions instance**. In a separate file called `grid-config.js` (referenced in the HTML above) we’ll write:

```javascript
// grid-config.js

// Step 2: Create a new GridJsOptions instance to configure grid behavior
const gridOptions = new GridJsOptions();
```

That single line gives you a clean object you can start populating with settings. Think of `gridOptions` as the control panel for every feature you’ll later enable.

### Τι διαμορφώνετε

- **NumberFormatAlignment** – ευθυγραμμίζει αυτόματα αριθμητικές συμβολοσειρές.
- **Pagination** – ελέγχει το μέγεθος σελίδας και την πλοήγηση.
- **Sorting** – ενεργοποιεί/απενεργοποιεί την ταξινόμηση στήλης.
- **Columns** – ορίζει κεφαλίδες, τύπους δεδομένων και προσαρμοσμένους renderers.

You can add any of these properties before you finally instantiate the Grid itself.

## Βήμα 3: Ενεργοποίηση Ευθυγράμμισης Αριθμών (Κοινή Απαίτηση)

Most tables contain a mix of text and numbers. By default Grid.js aligns everything left, which looks odd for monetary values. To **configure grid options JavaScript** for proper alignment, set the `NumberFormatAlignment` flag:

```javascript
// Enable left/right alignment for numeric strings
gridOptions.NumberFormatAlignment = true;
```

Why enable this? When the flag is true, Grid.js inspects each cell; if it looks like a number (e.g., “1234”, “12.34%”), it automatically right‑aligns it. This tiny tweak makes reports far more readable.

## Βήμα 4: Προσθήκη Σελιδοποίησης και Ταξινόμησης

A real‑world grid rarely fits on a single screen. Let’s turn on pagination (10 rows per page) and allow users to sort any column.

```javascript
gridOptions.Pagination = {
  limit: 10,          // rows per page
  enabled: true
};

gridOptions.Sort = true;   // enables click‑to‑sort on all columns
```

### Σημείωση Edge‑case

If you later supply a custom data source that already returns paginated results, you’ll want to disable Grid.js’s built‑in pagination to avoid double‑paging. Simply set `gridOptions.Pagination.enabled = false;`.

## Βήμα 5: Ορισμός Στηλών και Δεδομένων Δείγματος

Now we’ll feed the grid some mock data and tell it what each column represents. This is where the **create gridjsoptions instance** pattern really shines—everything lives in one tidy object.

```javascript
// Sample data array of objects
const sampleData = [
  { id: 1, name: "Alice", salary: "54000", department: "Engineering" },
  { id: 2, name: "Bob",   salary: "47000", department: "Marketing" },
  { id: 3, name: "Cara",  salary: "62000", department: "Design" },
  // ...more rows as needed
];

// Column definitions
gridOptions.Columns = [
  { id: "id",   name: "ID",          width: "5%" },
  { id: "name", name: "Employee",    width: "35%" },
  { id: "salary", name: "Salary ($)", width: "20%" },
  { id: "department", name: "Dept.",  width: "40%" }
];

// Attach data source
gridOptions.Data = sampleData;
```

Notice we keep the column `id` values identical to the keys in each data object. This convention lets Grid.js map values automatically, saving you from writing a custom formatter for every column.

## Βήμα 6: Δημιουργία του Grid με τις Επιλογές μας

We finally **configure grid options javascript** by passing the `gridOptions` object to the Grid constructor. The grid will render inside the `<div id="grid-wrapper">` we prepared earlier.

```javascript
// Create the Grid instance using the previously built options
const grid = new Grid(gridOptions);

// Render the grid into the page
grid.render(document.getElementById("grid-wrapper"));
```

That’s it. The whole process—from **create gridjsoptions instance** to rendering—takes less than a minute of coding.

### Αναμενόμενο Αποτέλεσμα

When you open the HTML file in a browser you should see:

- Μια γραμμή κεφαλίδας με “ID”, “Employee”, “Salary ($)”, “Dept.”.
- Αριθμούς μισθών ευθυγραμμισμένους δεξιά (ευχαριστώντας το `NumberFormatAlignment`).
- Έλεγχους σελιδοποίησης στο κάτω μέρος (αν προσθέσατε περισσότερες από δέκα γραμμές).
- Κεφαλίδες στηλών που μπορούν να κλικάρουν για ταξινόμηση αύξουσα/φθίνουσα.

If anything looks off, open the browser console (F12) and look for error messages—most bugs stem from mismatched column IDs or missing library scripts.

## Βήμα 7: Προχωρημένες Ρυθμίσεις (Προαιρετικό)

Below are a few quick ideas you can experiment with once the basic grid works.

| Δυνατότητα | Πώς να ενεργοποιηθεί | Γιατί βοηθά |
|------------|----------------------|--------------|
| **Προσαρμοσμένος renderer κελιού** | `gridOptions.Columns[2].formatter = (cell) => \`<b>$${cell}</b>\`;` | Τονίζει τους μισθούς με έντονη γραφή. |
| **Γραμμή αναζήτησης** | `gridOptions.Search = true;` | Επιτρέπει στους χρήστες να φιλτράρουν τις γραμμές άμεσα. |
| **Δεδομένα από τον server** | Set `gridOptions.Server = { url: "/api/employees", then: data => data.items };` | Κλιμακώνεται σε χιλιάδες γραμμές. |
| **Αλλαγή θέματος** | Add `gridOptions.ClassName = "gridjs-theme-dark";` | Ταιριάζει με σχέδια σε σκοτεινή λειτουργία. |

Feel free to mix and match—Grid.js is deliberately flexible. Just remember to keep the original **create gridjsoptions instance** line at the top; all later tweaks rely on that single object.

## Συμπέρασμα

We’ve just walked through a complete workflow to **create GridJsOptions instance** and **configure grid options JavaScript** for a functional, sortable, and paginated data table. Starting with a plain HTML page, we loaded the library, built an options object, enabled numeric alignment, added pagination, defined columns, and finally rendered the grid.

From here you can:

- Replace the static `sampleData` with an AJAX call.
- Add custom formatters for dates, currencies, or icons.
- Integrate the grid into a framework like React or Vue (the same `gridOptions` object works there too).

The possibilities are practically endless, and the pattern we used—centralizing all settings in a single `GridJsOptions` instance—keeps your code clean and maintainable.

Got a use‑case you’re unsure about? Drop a comment, and we’ll explore it together. Happy coding, and enjoy building dynamic tables with Grid.js!

## Τι Θα Μάθετε Στη Σειρά;

- [Πώς να Δημιουργήσετε και Διαμορφώσετε Excel Workbooks με Aspose.Cells .NET: Οδηγός Βήμα‑Βήμα](/cells/english/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)
- [Πώς να Δημιουργήσετε και Στυλιζάρετε Excel Πίνακες Χρησιμοποιώντας Aspose.Cells για .NET | Οδηγός Βήμα‑Βήμα](/cells/english/net/tables-structured-references/aspose-cells-net-excel-tables-styling/)
- [Πώς να Δημιουργήσετε & Διαμορφώσετε Excel Κελιά Χρησιμοποιώντας Aspose.Cells για Java: Οδηγός Βήμα‑Βήμα](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}