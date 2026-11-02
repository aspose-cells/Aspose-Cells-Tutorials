---
category: general
date: 2026-06-30
description: Apprenez comment obtenir l'adresse de la cellule sélectionnée, mettre
  à jour la valeur d'une cellule de la grille et lire la valeur d'entrée avec JavaScript
  en utilisant GridJs. Code et astuces étape par étape.
draft: false
keywords:
- get selected cell address
- update grid cell value
- read input value with javascript
language: fr
og_description: Obtenez l'adresse de la cellule sélectionnée, mettez à jour la valeur
  de la cellule de la grille et lisez la valeur d'entrée avec JavaScript. Suivez ce
  guide complet pour une intégration fluide de GridJs.
og_title: Obtenir l'adresse de la cellule sélectionnée – Tutoriel complet GridJs JavaScript
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
title: Obtenir l'adresse de la cellule sélectionnée dans GridJs – Guide complet JavaScript
url: /fr/python/integration-and-interoperability/get-selected-cell-address-in-gridjs-full-javascript-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Obtenir l’adresse de la cellule sélectionnée – Tutoriel complet GridJs JavaScript

Vous avez déjà eu besoin d’**obtenir l’adresse de la cellule sélectionnée** d’un tableau GridJs sans savoir quelle fonction appeler ? Vous n’êtes pas seul. Dans de nombreux panneaux d’administration, les utilisateurs cliquent sur une cellule, modifient une valeur dans une fenêtre modale et s’attendent à ce que la grille reflète immédiatement le changement. Ce tutoriel vous montre exactement comment récupérer cette adresse, lire le nouveau prix depuis un champ de saisie, et **mettre à jour la valeur de la cellule de la grille** sans recharger la page.

Nous aborderons également **la lecture de la valeur d’un champ avec JavaScript** de la bonne manière, la gestion des cas limites, et la fermeture de la modale une fois la mise à jour terminée. À la fin, vous disposerez d’un extrait autonome que vous pourrez insérer dans n’importe quel projet utilisant GridJs.

## Ce que vous allez construire

- Un tableau HTML simple alimenté par GridJs.  
- Une fenêtre modale d’édition qui apparaît lorsqu’une cellule est cliquée.  
- Du JavaScript qui **obtient l’adresse de la cellule sélectionnée**, récupère le prix saisi par l’utilisateur, **met à jour la valeur de la cellule de la grille**, puis masque la modale.

Aucune bibliothèque externe en dehors de GridJs n’est requise, et le code fonctionne avec les navigateurs modernes (Chrome 102+, Edge, Firefox). Si vous avez déjà une instance GridJs sur la page, vous pouvez copier‑coller les parties pertinentes directement.

## Prérequis

- Connaissances de base en JavaScript et le DOM.  
- Bibliothèque GridJs chargée (via CDN ou npm).  
- Une page qui rend déjà une grille GridJs (nous montrerons un exemple minimal).

Si l’un de ces points vous semble inconnu, ne paniquez pas — chaque étape comprend un bref rappel.

---

## Étape 1 : Mettre en place le squelette HTML

Commencez par disposer le conteneur du tableau, la modale cachée et le champ de prix. La modale sera affichée grâce à de simples classes CSS.

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

> **Astuce :** Le `#editModal` utilise un petit truc CSS — ajoutez simplement la classe `active` pour l’afficher. Vous pouvez remplacer cela par Bootstrap, Tailwind ou tout autre composant modal que vous utilisez déjà.

---

## Étape 2 : Initialiser GridJs et capturer les clics de cellule

Nous allons créer une grille avec des données d’exemple et écouter les sélections de cellules. Lorsqu’un utilisateur clique sur une cellule, nous **obtiendrons l’adresse de la cellule sélectionnée** et ouvrirons la modale.

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

> **Pourquoi cela fonctionne :** `GridJs.getSelectedCell()` renvoie une chaîne comme `"C2"` (colonne C, ligne 2). La stocker dans `lastSelectedCell` nous permet de référencer l’emplacement exact lorsque nous **mettrons à jour la valeur de la cellule de la grille** plus tard.

---

## Étape 3 : Lire le nouveau prix depuis le champ de saisie

Lorsque l’utilisateur clique sur **Enregistrer**, nous devons **lire la valeur du champ avec JavaScript** de façon sécurisée. Cette étape valide également que le prix saisi est un nombre positif.

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

> **Remarque :** L’utilisation de `parseFloat` permet d’accepter les décimaux (ex. `1.99`). La vérification `isNaN` empêche les soumissions vides accidentelles.

---

## Étape 4 : Mettre à jour la valeur de la cellule sélectionnée

Nous allons enfin **mettre à jour la valeur de la cellule de la grille** en utilisant l’adresse capturée précédemment. La méthode `updateCell` de GridJs renvoie une promesse, ce qui nous permet d’enchaîner une action de fermeture de la modale.

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

> **Pourquoi utiliser une promesse ?** GridJs peut devoir re‑rendre le tableau ou se synchroniser avec un backend. En attendant la résolution de la promesse, nous garantissons que l’interface ne se cache qu’après que la grille ait reflété la nouvelle valeur.

---

## Étape 5 : Gérer l’annulation et les cas limites

Une solution robuste offre toujours une issue à l’utilisateur. Le bouton **Annuler** masque simplement la modale et réinitialise toute adresse stockée.

```javascript
document.getElementById('cancelBtn').addEventListener('click', () => {
  document.getElementById('editModal').classList.remove('active');
  lastSelectedCell = null;
});
```

### Que se passe‑t‑il si aucune cellule n’est sélectionnée ?

Si un utilisateur déclenche le bouton **Enregistrer** sans avoir cliqué sur une cellule au préalable (par exemple, il a ouvert la modale par programme), `lastSelectedCell` sera `null`. Le retour anticipé dans `updateSelectedCell` empêche une erreur d’exécution et consigne un avertissement utile.

### Gestion des grandes grilles

Pour les grilles avec pagination, `GridJs.getSelectedCell()` renvoie toujours l’adresse absolue (ex. `"B12"`), pas seulement la ligne visible. Ainsi, la mise à jour fonctionne même si la ligne éditée se trouve sur une autre page. Notez simplement que l’interface ne changera pas automatiquement de page après la mise à jour — si vous avez besoin de cela, appelez `grid.forceUpdate()` ou naviguez manuellement vers la page appropriée.

---

## Exemple complet fonctionnel

Voici le code complet que vous pouvez copier‑coller dans un fichier HTML unique. Ouvrez‑le dans un navigateur, cliquez sur n’importe quelle cellule, modifiez le prix, et observez la grille se mettre à jour instantanément.

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


## Que devez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser d’autres fonctionnalités de l’API et à explorer des approches d’implémentation alternatives dans vos propres projets.

- [Obtenir l’adresse, le nombre de cellules et le décalage pour toute la plage Excel](/cells/english/net/excel-range-address-calculation/get-address-cell-count-and-offset-for-entire-excel-range/)
- [Obtenir l’adresse, le nombre de cellules et le décalage pour toute la plage Excel](/cells/german/net/excel-range-address-calculation/get-address-cell-count-and-offset-for-entire-excel-range/)
- [Obtenir l’adresse, le nombre de cellules et le décalage pour toute la plage Excel](/cells/french/net/excel-range-address-calculation/get-address-cell-count-and-offset-for-entire-excel-range/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}