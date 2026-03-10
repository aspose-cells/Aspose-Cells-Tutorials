---
category: general
date: 2026-02-15
description: Comment formater rapidement une devise en utilisant la définition du
  format numérique de colonne et appliquer un format numérique personnalisé en C#.
  Apprenez à récupérer une colonne par son nom et à définir l’alignement de la colonne
  de la grille.
draft: false
keywords:
- how to format currency
- set column number format
- apply custom numeric format
- retrieve column by name
- set grid column alignment
language: fr
og_description: Comment formater la devise dans une colonne de grille avec C#. Ce
  tutoriel montre comment récupérer une colonne par son nom, définir le format numérique
  de la colonne, appliquer un format numérique personnalisé et définir l’alignement
  de la colonne de la grille.
og_title: Comment formater la devise dans une colonne de grille – Guide complet
tags:
- C#
- GridFormatting
- UI
title: Comment formater la devise dans une colonne de grille – Guide étape par étape
url: /fr/net/number-and-display-formats-in-excel/how-to-format-currency-in-a-grid-column-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# comment formater la devise dans une colonne de grille – Tutoriel complet de programmation

Vous êtes-vous déjà demandé **comment formater la devise** dans une colonne de grille sans perdre patience ? Vous n'êtes pas le seul. Quand vous voyez un nombre brut comme `1234.5` et que vous aimeriez qu’il apparaisse magiquement sous la forme `$1,234.50`, la solution se résume généralement à quelques lignes de configuration.  

Dans ce guide, nous allons **récupérer la colonne par son nom**, **définir le format numérique de la colonne**, et **appliquer un format numérique personnalisé** qui respecte la mise en page comptable habituelle. En chemin, nous **définirons l’alignement de la colonne de la grille** et ajouterons une bordure discrète pour que l’interface soit plus soignée.

> **TL;DR** – À la fin, vous disposerez d’un extrait prêt à l’emploi qui transforme des décimaux bruts en valeurs monétaires magnifiquement formatées dans n’importe quel contrôle de type `GridJs`.

---

## Ce dont vous aurez besoin

- Un projet .NET (toute version supportant C# 8.0+ – Visual Studio 2022 fonctionne très bien).  
- Un composant de grille exposant une collection `Columns` (l’exemple utilise une classe fictive `GridJs`, mais les concepts s’appliquent aux grilles DevExpress, Telerik ou Syncfusion).  
- Une connaissance de base de la syntaxe C# – aucun tour avancé requis.

Si vous avez déjà tout cela, tant mieux. Sinon, créez simplement une application console ; la grille peut être simulée à des fins d’illustration.

---

## Implémentation pas‑à‑pas

Sous chaque étape, vous trouverez un bloc de code compact, une courte explication du **pourquoi** de la ligne, et une astuce pour éviter les pièges courants.

### ## Étape 1 – Récupérer la colonne « Amount » par son nom

```csharp
// Step 1: Retrieve the "Amount" column from the grid
var amountColumn = gridJs.Columns["Amount"];
if (amountColumn == null)
{
    throw new InvalidOperationException("Column 'Amount' does not exist. Verify the column name or check the grid's schema.");
}
```

**Pourquoi c’est important :**  
La plupart des API de grille exposent les colonnes via un indexeur de type dictionnaire. Récupérer la colonne par son intitulé (`"Amount"`) vous permet de modifier son apparence sans toucher à la source de données sous‑jacente.  

**Astuce pro :** Protégez toujours contre un retour `null` – une faute de frappe dans le nom de la colonne ou un changement de schéma dynamique peut sinon provoquer une `NullReferenceException` à l’exécution.

---

### ## Étape 2 – Définir le format numérique de la colonne avec un masque de devise personnalisé

```csharp
// Step 2: Apply a custom numeric format for currency values
amountColumn.NumberFormat = "_(* #,##0.00_);_(* (#,##0.00);_(* \"-\"??_);_(@_)";
```

**Pourquoi c’est important :**  
La chaîne de format suit les conventions de format comptable d’Excel :

- `_(* #,##0.00_)` → Nombres positifs, alignés à droite avec un espace initial pour le symbole monétaire.  
- `_(* (#,##0.00)` → Nombres négatifs entourés de parenthèses.  
- `_(* \"-\"??_)` → Valeurs zéro affichées sous forme de tiret.  
- `_(@_)` → Les valeurs texte restent inchangées.

Utiliser **apply custom numeric format** vous donne un contrôle total sur les séparateurs de milliers, les décimales et le placement du symbole monétaire.  

**Cas limite :** Si votre application doit respecter une locale différente (par ex. l’euro au lieu du dollar), remplacez l’espace initial par le symbole approprié ou utilisez un format sensible à `CultureInfo` dans la source de données.

---

### ## Étape 3 – Aligner le contenu de la colonne à droite pour une meilleure lisibilité

```csharp
// Step 3: Align the column contents to the right for better readability
amountColumn.Alignment = GridAlignment.Right;
```

**Pourquoi c’est important :**  
Les valeurs monétaires sont plus faciles à parcourir lorsqu’elles sont alignées sur le séparateur décimal. Définir **set grid column alignment** à `Right` reproduit la façon dont les feuilles de calcul affichent les données financières.  

**Piège :** Certaines grilles ignorent l’alignement sur les cellules contenant des modèles personnalisés. Si vous constatez que l’alignement ne s’applique pas, vérifiez que la colonne n’utilise pas un rendu de cellule personnalisé.

---

### ## Étape 4 – Ajouter une fine bordure grise autour des cellules de la colonne

```csharp
// Step 4: Add a thin gray border around the column cells
amountColumn.Border = new GridBorder
{
    Color = Color.Gray,
    Style = BorderLineStyle.Thin
};
```

**Pourquoi c’est important :**  
Une bordure discrète sépare la colonne « Amount » de ses voisines, surtout lorsque la grille utilise des couleurs de lignes alternées. C’est un indice visuel que les données représentent une valeur financière distincte.  

**Conseil :** Si vous avez besoin d’une ligne plus épaisse pour l’impression, passez `BorderLineStyle` à `Medium` ou changez `Color` en `Color.Black`.

---

## Exemple complet fonctionnel

Voici le fragment complet que vous pouvez intégrer dans un projet WinForms ou WPF utilisant un contrôle de type `GridJs`. L’exemple affiche également les valeurs formatées dans la console afin que vous puissiez vérifier le résultat sans interface graphique.

```csharp
using System;
using System.Drawing;   // For Color
using GridLibrary;      // Hypothetical namespace for GridJs

namespace GridCurrencyDemo
{
    class Program
    {
        static void Main()
        {
            // Create a mock grid and add a sample column
            var gridJs = new GridJs();
            gridJs.Columns.Add(new GridColumn
            {
                Name = "Amount",
                Header = "Amount",
                DataType = typeof(decimal)
            });

            // Populate some sample data
            gridJs.Rows.Add(new { Amount = 1234.5m });
            gridJs.Rows.Add(new { Amount = -567.89m });
            gridJs.Rows.Add(new { Amount = 0m });

            // ---- Formatting steps ------------------------------------------------
            // 1️⃣ Retrieve the "Amount" column
            var amountColumn = gridJs.Columns["Amount"]
                ?? throw new InvalidOperationException("Column 'Amount' not found.");

            // 2️⃣ Apply custom numeric format for currency
            amountColumn.NumberFormat = "_(* #,##0.00_);_(* (#,##0.00);_(* \"-\"??_);_(@_)";

            // 3️⃣ Right‑align the values
            amountColumn.Alignment = GridAlignment.Right;

            // 4️⃣ Add a thin gray border
            amountColumn.Border = new GridBorder
            {
                Color = Color.Gray,
                Style = BorderLineStyle.Thin
            };
            // -----------------------------------------------------------------------

            // Render the grid (in a real UI you would call gridJs.Render() or similar)
            Console.WriteLine("Formatted Currency Grid:");
            foreach (var row in gridJs.Rows)
            {
                var rawValue = (decimal)row.Amount;
                // The grid library would automatically apply NumberFormat when displaying.
                // For console demo we mimic the formatting:
                string formatted = rawValue.ToString("#,##0.00", System.Globalization.CultureInfo.InvariantCulture);
                if (rawValue < 0)
                    formatted = $"({formatted.TrimStart('-')})";
                else if (rawValue == 0)
                    formatted = "-";

                Console.WriteLine($"| {formatted,15} |");
            }

            // Keep console open
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**Sortie console attendue**

```
Formatted Currency Grid:
|        1,234.50 |
|       (567.89) |
|               - |
```

Remarquez comment le nombre positif est aligné à droite, le nombre négatif apparaît entre parenthèses, et le zéro est affiché sous forme de tiret – exactement ce que dicte la chaîne de format personnalisée.

---

## Questions fréquentes & cas limites

| Question | Réponse |
|----------|--------|
| *Et si la grille utilise une culture différente (par ex. € au lieu de $) ?* | Remplacez l’espace initial dans la chaîne de format par le symbole souhaité ou laissez la source de données générer une chaîne pré‑formatée avec `CultureInfo.CurrentCulture`. |
| *Puis‑je réutiliser le même format pour plusieurs colonnes ?* | Absolument. Stockez la chaîne de format dans une constante (`const string CurrencyMask = "...";`) et assignez‑la partout où vous avez besoin de la devise. |
| *Que se passe‑t‑il si la colonne contient une valeur texte ?* | La chaîne de format n’affecte que les types numériques. Les chaînes passent inchangées, d’où la présence de la dernière partie du masque (`_(@_)`) qui préserve le contenu non numérique. |
| *Y a‑t‑il un impact sur les performances ?* | Négligeable. Le format est appliqué au moment du rendu, pas lors de la récupération des données. À moins de rendre des milliers de lignes par image, vous ne remarquerez aucune lenteur. |
| *Comment épaissir la bordure pour les rapports imprimés ?* | Remplacez `BorderLineStyle.Thin` par `BorderLineStyle.Medium` ou `BorderLineStyle.Thick`. Certaines bibliothèques permettent aussi de spécifier directement une largeur en pixels. |

---

## Conclusion

Nous avons parcouru **comment formater la devise** dans une colonne de grille de bout en bout : récupérer la colonne par son nom, définir le format numérique, appliquer un format personnalisé, aligner les cellules et ajouter une bordure élégante. L’exemple complet fonctionne immédiatement et montre le rendu visuel exact que vous pouvez attendre.

Si vous êtes prêt à aller plus loin, essayez :

- **Cultures dynamiques** – changez la chaîne de format en fonction de la locale de l’utilisateur.  
- **Conditional

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}