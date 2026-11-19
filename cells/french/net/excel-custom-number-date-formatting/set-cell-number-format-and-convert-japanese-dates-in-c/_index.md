---
category: general
date: 2026-11-19
description: Définissez le format numérique des cellules en C# et apprenez à appliquer
  le format de date Excel pour les dates de l’ère japonaise, permettant une conversion
  fiable des dates Excel en C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set cell number format
- apply excel date format
- c# excel date conversion
- japanese era date excel
- aspose.cells date handling
language: fr
lastmod: 2026-11-19
og_description: Définissez le format numérique des cellules en C# et appliquez le
  format de date Excel aux dates de l'ère japonaise. Suivez ce guide complet pour
  une conversion précise des dates Excel en C#.
og_image_alt: Screenshot showing a C# code editor with set cell number format applied
  to an Excel cell
og_title: Définir le format numérique des cellules et convertir les dates japonaises
  en C# – guide étape par étape
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Set cell number format in C# and learn how to apply Excel date format
    for Japanese era dates, enabling reliable C# Excel date conversion.
  headline: Set cell number format and convert Japanese dates in C#
  type: TechArticle
- description: Set cell number format in C# and learn how to apply Excel date format
    for Japanese era dates, enabling reliable C# Excel date conversion.
  name: Set cell number format and convert Japanese dates in C#
  steps:
  - name: Why this works
    text: '* `Style.Number = 14` maps to Excel’s *Short Date* format (`mm/dd/yyyy`
      by default). * When the cell contains a Japanese era string like `R3/04/01`,
      Aspose.Cells’ internal parser recognises the era and converts it to the corresponding
      Gregorian serial number during `CalculateFormula()`. * After the '
  - name: When to use a custom format
    text: '* Reports intended for Japanese audiences. * When you need to preserve
      the original era information for legal documents. * In dashboards where both
      Gregorian and era dates are shown side‑by‑side.'
  - name: Full end‑to‑end example
    text: Below is a self‑contained program that demonstrates both the Gregorian and
      era outputs in one run.
  - name: Edge cases & common pitfalls
    text: '| Situation | What to watch for | Fix / Recommendation | |----------------------------------------|------------------------------------------------------|----------------------------------------------------------|
      | Empty or malformed era string | `PutValue` stores the literal text; conversion
      fails'
  - name: Automation tip
    text: 'If you need to process a large range of era dates (e.g., column A contains
      many Japanese dates), wrap the conversion logic in a loop:'
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
- Date conversion
title: Définir le format numérique des cellules et convertir les dates japonaises
  en C#
url: /fr/net/excel-custom-number-date-formatting/set-cell-number-format-and-convert-japanese-dates-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Définir le format numérique des cellules et convertir les dates japonaises en C#

Si vous devez **set cell number format** dans un projet d'automatisation Excel en C#, ce guide vous montre comment **apply Excel date format** et effectuer **C# Excel date conversion** pour les dates d'ère japonaise. Vous obtiendrez un exemple complet et exécutable qui convertit une chaîne d'ère Reiwa (par ex., `R3/04/01`) en la date grégorienne `2021‑04‑01`.

## Ce que vous apprendrez

* Comment créer un classeur et accéder à sa première feuille de calcul.  
* Comment **set cell number format** afin qu'Excel traite la valeur comme une date.  
* Comment **apply Excel date format** qui reconnaît les chaînes d'ère japonaise.  
* Comment déclencher **C# Excel date conversion** en recalculant les formules.  
* Résultat attendu et conseils de dépannage pour les cas limites.

**Prérequis**

* .NET 6 ou ultérieur (le code fonctionne également avec .NET Framework 4.6+).  
* Aspose.Cells pour .NET 2024 ou plus récent – installer via NuGet : `dotnet add package Aspose.Cells`.  
* Familiarité de base avec C# et la gestion des dates Excel.

> **Astuce :** Aspose.Cells fonctionne sans Microsoft Office installé, ce qui le rend idéal pour l'automatisation côté serveur.

## Définir le format numérique des cellules avec Aspose.Cells en C#

La première étape consiste à indiquer à Excel que la cellule contient une date. Excel stocke les dates sous forme de nombres sériels, nous devons donc appliquer un format numérique de date intégré (ID 14) à la cellule cible.

```csharp
using System;
using Aspose.Cells;

class JapaneseEraDateDemo
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // 2️⃣ Insert a Japanese era date string (Reiwa 3) into cell A1
        sheet.Cells["A1"].PutValue("R3/04/01");

        // 3️⃣ **Set cell number format** – use built‑in date format ID 14
        //    This tells Excel to treat the string as a date value.
        sheet.Cells["A1"].Style.Number = 14;

        // 4️⃣ Recalculate formulas so the internal date engine converts the era.
        workbook.CalculateFormula();

        // 5️⃣ Output the converted Gregorian date.
        Console.WriteLine(sheet.Cells["A1"].StringValue); // → 2021-04-01
    }
}
```

### Pourquoi cela fonctionne

* `Style.Number = 14` correspond au format *Date courte* d'Excel (`mm/dd/yyyy` par défaut).  
* Lorsque la cellule contient une chaîne d'ère japonaise comme `R3/04/01`, l'analyseur interne d'Aspose.Cells reconnaît l'ère et la convertit en le nombre sériel grégorien correspondant lors de `CalculateFormula()`.  
* Après le calcul, `StringValue` renvoie la date grégorienne formatée.

## Appliquer le format de date Excel pour les dates d'ère japonaise

Si vous souhaitez que la cellule affiche l'ère japonaise au lieu de la date grégorienne, vous pouvez utiliser un format numérique personnalisé qui inclut le code d'ère. Cela démontre la capacité **apply excel date format**.

```csharp
// Apply a custom format that forces the Japanese era display
sheet.Cells["A1"].Style.Custom = "[$-ja-JP]ggge\"年\"m\"月\"d\"日\"";

// Recalculate to apply the custom format
workbook.CalculateFormula();

// Output the era‑styled string
Console.WriteLine(sheet.Cells["A1"].StringValue); // → R3年04月01日
```

* `[$-ja-JP]` force la locale japonaise.  
* `ggg` représente le nom de l'ère (par ex., `R` pour Reiwa).  
* L'ajout de caractères littéraux (`年`, `月`, `日`) crée une mise en page de date japonaise familière.

### Quand utiliser un format personnalisé

* Rapports destinés à un public japonais.  
* Lorsque vous devez conserver l'information d'ère originale pour les documents juridiques.  
* Dans les tableaux de bord où les dates grégoriennes et d'ère sont affichées côte à côte.

## Conversion de date Excel en C# – gestion des ères japonaises

Le processus **c# excel date conversion** peut être décomposé en trois parties logiques :

1. **Parse the era string** – Aspose.Cells reconnaît automatiquement `R` (Reiwa), `H` (Heisei), `S` (Showa), etc.  
2. **Convert to a serial number** – Excel stocke les dates sous forme de jours depuis le 30‑12‑1899.  
3. **Format the serial number** – soit avec un format intégré (ID 14), soit avec un format japonais personnalisé.

### Exemple complet de bout en bout

Voici un programme autonome qui montre à la fois les sorties grégoriennes et d'ère en une seule exécution.

```csharp
using System;
using Aspose.Cells;

class JapaneseEraConversion
{
    static void Main()
    {
        // Create workbook and worksheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];

        // Input: Reiwa 3 (2021) – can be any era string
        ws.Cells["A1"].PutValue("R3/04/01");

        // ---- Part 1: Gregorian output ----
        ws.Cells["A1"].Style.Number = 14;      // built‑in short date
        wb.CalculateFormula();                // forces conversion
        string gregorian = ws.Cells["A1"].StringValue;
        Console.WriteLine($"Gregorian: {gregorian}"); // 2021-04-01

        // ---- Part 2: Japanese era output ----
        ws.Cells["B1"].PutValue("R3/04/01");   // repeat input for clarity
        ws.Cells["B1"].Style.Custom = "[$-ja-JP]ggge\"年\"m\"月\"d\"日\"";
        wb.CalculateFormula();
        string era = ws.Cells["B1"].StringValue;
        Console.WriteLine($"Japanese era: {era}"); // R3年04月01日
    }
}
```

**Sortie console attendue**

```
Gregorian: 2021-04-01
Japanese era: R3年04月01日
```

### Cas limites et pièges courants

| Situation | À surveiller | Correction / Recommandation |
|-----------|--------------|------------------------------|
| Chaîne d'ère vide ou malformée | `PutValue` stocke le texte littéral ; la conversion échoue | Validez l'entrée avec une expression régulière avant d'écrire dans la cellule. |
| Incompatibilité de locale | Le format personnalisé affiche des chiffres occidentaux au lieu des caractères japonais | Assurez‑vous que le format `Custom` inclut `[$-ja-JP]` ou définissez `Workbook.Settings.CultureInfo` sur `ja-JP`. |
| Le classeur contient des formules faisant référence à la cellule de date | Le recalcul peut écraser les résultats des formules | Appelez `CalculateFormula` **après** toutes les étapes de formatage, ou utilisez `Workbook.CalculateFormula(FormulaCalculationOptions.IgnoreError)` si vous devez ignorer les erreurs. |
| Utilisation de versions plus anciennes d'Aspose.Cells | La prise en charge des ères japonaises a été ajoutée au troisième trimestre 2022 | Mettez à jour vers le dernier package NuGet. |

## Tester la solution

1. **Exécutez le programme** depuis Visual Studio ou `dotnet run`.  
2. Vérifiez que la console affiche la date grégorienne `2021‑04‑01` et la chaîne d'ère `R3年04月01日`.  
3. Ouvrez le classeur généré (si vous ajoutez `wb.Save("Demo.xlsx");`) dans Microsoft Excel pour voir le même format appliqué aux cellules.

### Astuce d'automatisation

Si vous devez traiter une grande plage de dates d'ère (par ex., la colonne A contient de nombreuses dates japonaises), encapsulez la logique de conversion dans une boucle :

```csharp
for (int row = 0; row < ws.Cells.MaxDataRow + 1; row++)
{
    var cell = ws.Cells[row, 0]; // column A
    cell.Style.Number = 14;
}
wb.CalculateFormula();
```

Cette approche maintient l'opération **set cell number format** rapide et efficace en mémoire.

## Conclusion

Vous savez maintenant comment **set cell number format** en C# avec Aspose.Cells, comment **apply Excel date format** pour les chaînes d'ère japonaise, et comment effectuer une **C# Excel date conversion** fiable des ères vers les dates grégoriennes. Le code complet et exécutable montre les deux sorties et met en évidence les cas limites courants.  

**Étapes suivantes**

* Explore other built‑in format IDs

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités d'API supplémentaires et explorer des approches d'implémentation alternatives dans vos propres projets.

- [définir le format de date Excel en C# – Guide complet étape par étape](/cells/english/net/excel-custom-number-date-formatting/set-excel-date-format-in-c-complete-step-by-step-guide/)
- [Comment appliquer le format numérique Excel avec Aspose.Cells](/cells/english/net/excel-custom-number-date-formatting/how-to-apply-number-format-excel-with-aspose-cells/)
- [Comment appliquer un format numérique personnalisé Excel en C#](/cells/english/net/excel-custom-number-date-formatting/how-to-apply-a-custom-number-format-excel-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}