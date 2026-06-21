---
category: general
date: 2026-06-21
description: Apprenez à modifier la police d’une zone de texte, à définir la couleur
  de la police par programmation et à ajuster la taille de la police d’une cellule
  dans une grille. Suivez ce tutoriel pratique pour styliser les zones de texte.
draft: false
keywords:
- change textbox font
- change font size cell
- how to style textbox
- set font color programmatically
- change font family grid
language: fr
og_description: Modifiez rapidement la police d’une zone de texte dans une grille.
  Ce guide montre comment styliser la zone de texte, définir la couleur de la police
  de manière programmatique et ajuster la taille des cellules avec un code clair.
og_title: Modifier la police de la zone de texte dans une grille – Guide complet de
  programmation
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
title: Modifier la police du champ texte dans une grille – Guide complet étape par
  étape
url: /fr/net/working-with-fonts-in-spreadsheets/change-textbox-font-in-a-grid-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Modifier la police du champ texte dans une grille – Guide complet étape par étape

Vous avez déjà eu besoin de **changer la police du champ texte** dans une grille de données mais vous ne saviez pas quelle propriété ajuster ? Vous n'êtes pas seul—la plupart des développeurs rencontrent ce problème lorsqu'ils construisent des tables éditables ou des tableaux de bord. Dans ce tutoriel, nous allons vous montrer exactement comment changer la police du champ texte, définir sa couleur de façon programmatique, et même ajuster la taille de la police cellule par cellule.

Nous ajouterons également des astuces sur **comment styliser les champs texte**, couvrirons les scénarios de **changement de taille de police cellule**, et vous montrerons comment **définir la couleur de la police de façon programmatique** sans perdre patience. À la fin, vous disposerez d'un extrait réutilisable qui fonctionne avec n'importe quel composant de grille exposant une API `getCell`.

## Prérequis

- Un navigateur moderne avec prise en charge ES6 (Chrome, Edge, Firefox, Safari)
- Une bibliothèque de grille qui propose `grid.getCell(row, col)` et renvoie un objet cellule contenant une référence `textbox`
- Connaissances de base des objets JavaScript et des propriétés CSS

Aucun package supplémentaire n'est requis—seulement du JavaScript pur et l'API propre de la grille.

## Vue d'ensemble de la solution

L'idée principale est simple : récupérer la cellule cible, saisir son champ texte intégré, puis attribuer un nouvel objet police qui définit la famille, la taille et la couleur. Pensez-y comme donner une nouvelle tenue au champ texte. Voici le flux de haut niveau :

1. **Accéder à la cellule cible** – localiser la ligne/colonne souhaitée.
2. **Récupérer le champ texte** – l'élément UI qui contient le texte.
3. **Créer un objet de style de police** – spécifier la famille, la taille et la couleur.
4. **Appliquer le style** – assigner l'objet à la propriété `font` du champ texte.

C'est tout. Plongeons dans chaque étape, expliquons pourquoi c'est important, et voyons le code en action.

![Screenshot of a grid cell with a styled textbox – change textbox font](/images/change-textbox-font-example.png)

## Étape 1 : Accéder à la cellule cible dans la grille

```javascript
// Step 1: Access the target cell in the grid
const cell = grid.getCell(2, 3);
```

> **Pourquoi c'est important :**  
> Les grilles stockent souvent les lignes et colonnes avec des index à partir de zéro. En appelant `grid.getCell(2, 3)` nous récupérons la cellule à la **ligne 2, colonne 3**. Si vous devez **changer la taille de police d'une cellule** pour un autre emplacement, il suffit d'ajuster les index.

**Astuce :** Si votre grille prend en charge les colonnes nommées, vous pouvez remplacer la colonne numérique par une clé, par ex. `grid.getCell(2, "price")`.

## Étape 2 : Récupérer le champ texte à l'intérieur de cette cellule

```javascript
// Step 2: Get the textbox contained in that cell
const textbox = cell.textbox;
```

> **Ce qui se passe :**  
> La plupart des implémentations de grilles encapsulent le contenu éditable dans un élément `<input>` ou `<textarea>` et l'exposent comme `cell.textbox`. Obtenir la référence nous permet de manipuler directement son style visuel.

Si la grille utilise un nom de propriété différent (comme `cell.editor`), ajustez simplement le code en conséquence—c'est une variation courante lorsque vous **comment styliser les champs texte** pour un composant personnalisé.

## Étape 3 : Définir les propriétés de police souhaitées

```javascript
// Step 3: Define the desired font properties
const fontStyle = {
  family: "Arial",          // change font family grid
  size: 14,                 // change font size cell
  color: "#0066CC"          // set font color programmatically
};
```

### Décomposition de l'objet

| Property | Purpose | Example Values |
|----------|---------|----------------|
| `family` | Famille de police – contrôle le type de caractère. | `"Arial"`, `"Helvetica"`, `"Courier New"` |
| `size`   | Taille de police en pixels (ou points, selon la grille). | `12`, `14`, `16` |
| `color`  | Couleur du texte dans tout format compatible CSS. | `"#0066CC"`, `"rgb(255,0,0)"`, `"navy"` |

> **Pourquoi nous utilisons un objet :**  
> Regrouper les trois attributs ensemble rend le code propre et reflète la façon dont de nombreuses bibliothèques UI attendent les informations de style. Cela vous permet également de **changer la famille de police d'une grille** ou de **définir la couleur de la police de façon programmatique** avec une seule assignation.

## Étape 4 : Appliquer le style de police au champ texte

```javascript
// Step 4: Apply the font style to the textbox
textbox.font = fontStyle;
```

> **Dans les coulisses :**  
> Le composant champ texte de la grille interprète la propriété `font` et met à jour son CSS en conséquence. Cette ligne unique remplace la famille, la taille et la couleur de police précédentes en une seule opération—exactement ce dont vous avez besoin lorsque vous **modifiez la police du champ texte** sur plusieurs cellules.

Si le composant utilise une API différente (par ex. `textbox.style.fontFamily = ...`), adaptez l'assignation mais conservez le même principe.

## Exemple complet fonctionnel

Voici un extrait autonome que vous pouvez coller dans un fichier HTML incluant un objet grille factice. Il démontre le flux complet de l'étape 1 à l'étape 4, ainsi qu'une vérification rapide que le style a changé.

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

### Résultat attendu

- Le champ texte situé à la **ligne 2, colonne 3** affiche désormais le texte en **Arial**, **14 px**, et une teinte bleue **#0066CC**.
- Ouvrir la console du navigateur affichera quelque chose comme :

```
Applied font family: Arial, Helvetica, sans-serif
Applied font size: 14px
Applied color: rgb(0, 102, 204)
```

Si vous ouvrez la page, vous verrez visuellement le changement—plus de police système par défaut.

## Questions fréquentes (FAQ)

### Puis-je changer uniquement la taille de la police sans affecter la famille ou la couleur ?

Absolument. Il suffit d'omettre les propriétés que vous ne souhaitez pas modifier :

```javascript
textbox.font = { size: 18 }; // only changes size
```

### Et si ma grille utilise un nom de propriété différent pour le champ texte ?

Inspectez l'objet cellule dans la console (`console.log(cell)`). Vous verrez probablement quelque chose comme `cell.editor` ou `cell.input`. Remplacez `cell.textbox` par la référence correcte.

### Comment appliquer le même style à une colonne entière ?

Parcourez les lignes et définissez la police pour chaque cellule de cette colonne :

```javascript
for (let r = 0; r < grid.rowCount; r++) {
  const colCell = grid.getCell(r, 3);
  colCell.textbox.font = fontStyle; // reuse the same fontStyle object
}
```

### Existe-t-il un moyen de revenir à la police d'origine ?

Enregistrez le style original avant de le remplacer :

```javascript
const original = { ...textbox.font };
textbox.font = fontStyle; // apply new style
// later...
textbox.font = original; // revert
```

## Astuces & bonnes pratiques

- **Mises à jour groupées :** Si vous devez styliser de nombreuses cellules, encapsulez les changements dans `requestAnimationFrame` ou une méthode de lot spécifique à la grille afin d'éviter les rafraîchissements de mise en page excessifs.
- **Polices réactives :** Utilisez des unités relatives (`em`, `rem`) plutôt que des pixels fixes si votre UI doit s'adapter.
- **Accessibilité :** Assurez un contraste suffisant lorsque vous **définissez la couleur de la police de façon programmatique**—le minimum WCAG AA est un ratio de 4,5 : 1 pour le texte normal.
- **Particularités inter‑navigateurs :** Certaines grilles plus anciennes peuvent nécessiter de définir `style.fontFamily` directement sur l'élément `<input>` au lieu d'utiliser un objet `font`.

## Conclusion

Nous venons de couvrir **comment changer la police du champ texte** dans une grille, depuis la récupération de la bonne cellule jusqu'à la définition d'un objet réutilisable `fontStyle` et son application en une ligne. En cours de route, nous avons également appris à **changer la taille de police d'une cellule**, à **définir la couleur de la police de façon programmatique**, et même à ajuster le **changement de famille de police d'une grille** pour une colonne spécifique.

Vous pouvez maintenant prendre ce modèle et l'adapter à n'importe quelle bibliothèque UI—que vous construisiez un tableau de bord admin, un éditeur de type feuille de calcul, ou un outil de reporting personnalisé. Expérimentez avec différentes familles, tailles et couleurs ; ajoutez éventuellement des effets au survol ou un style conditionnel basé sur les valeurs de données.

Vous avez un autre défi de stylisation ? Laissez un commentaire, et résolvons-le ensemble. Bon codage !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités d'API supplémentaires et explorer des approches d'implémentation alternatives dans vos propres projets.

- [How to Change Font Color in Excel Using Aspose.Cells for Java&#58; A Complete Guide](/cells/english/java/formatting/change-font-color-aspose-cells-java-tutorial/)
- [Change Font Color Aspose Cells Java Tutorial](/cells/german/java/formatting/change-font-color-aspose-cells-java-tutorial/)
- [Change Font Color Aspose Cells Java Tutorial](/cells/french/java/formatting/change-font-color-aspose-cells-java-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}