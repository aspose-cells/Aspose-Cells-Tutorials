---
category: general
date: 2026-02-26
description: Appliquez rapidement le format numérique dans Excel et apprenez à formater
  une colonne en devise, à définir le format numérique d’une colonne et à changer
  la couleur de police d’une colonne en quelques lignes de C#.
draft: false
keywords:
- apply number format excel
- format column as currency
- set column number format
- format currency column
- set column font color
language: fr
og_description: Appliquer le format de nombre Excel en C# avec des étapes simples.
  Apprenez à formater une colonne en devise, à définir le format numérique d’une colonne
  et à changer la couleur de police d’une colonne pour des feuilles de calcul professionnelles.
og_title: Appliquer le format de nombre dans Excel – Guide complet du style de colonne
tags:
- C#
- Excel
- Aspose.Cells
- DataTable
- Styling
title: Appliquer le format de nombre Excel – Guide étape par étape pour formater les
  colonnes
url: /fr/net/number-and-display-formats-in-excel/apply-number-format-excel-step-by-step-guide-to-formatting-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# appliquer le format de nombre excel – Comment styliser les colonnes Excel en C#

Vous êtes-vous déjà demandé comment **appliquer le format de nombre excel** tout en parcourant un `DataTable` ? Vous n'êtes pas le seul. La plupart des développeurs se heurtent à un mur lorsqu'ils ont besoin d'un en‑tête à police bleue *et* d'une colonne formatée en devise dans la même opération d'importation. La bonne nouvelle ? Avec quelques lignes de C# et les bons objets de style, vous pouvez le faire sans post‑traitement de la feuille.

Dans ce tutoriel, nous allons parcourir un exemple complet et exécutable qui vous montre comment **formater une colonne en devise**, **définir le format de nombre d’une colonne** pour toute autre colonne, et même **définir la couleur de police d’une colonne** pour les en‑têtes. À la fin, vous disposerez d’un modèle réutilisable que vous pourrez intégrer à n’importe quel projet Aspose.Cells (ou similaire).

## Ce que vous allez apprendre

- Comment récupérer un `DataTable` et associer chaque colonne à un `Style` spécifique.  
- Les étapes exactes pour **appliquer le format de nombre excel** à l’aide de `Worksheet.Cells.ImportDataTable`.  
- Pourquoi créer les styles à l’avance est plus efficace que de formater les cellules une par une.  
- Gestion des cas limites lorsque la table source possède plus de colonnes que vous n’avez stylées.  
- Un exemple complet, prêt à copier‑coller, que vous pouvez exécuter dès aujourd’hui.

> **Prérequis :** Ce guide suppose que vous avez Aspose.Cells for .NET (ou toute bibliothèque exposant les API `Workbook`, `Worksheet`, `Style`) référencée dans votre projet. Si vous utilisez une autre bibliothèque, les concepts se traduisent directement — il suffit de remplacer les noms de types.

---

## Étape 1 : Récupérer les données source sous forme de DataTable

Avant que le style puisse être appliqué, il faut les données brutes. Dans la plupart des scénarios réels, les données résident dans une base de données, un CSV ou une API. Pour plus de clarté, nous allons simuler un simple `DataTable` avec deux colonnes : *Product* (string) et *Price* (decimal).

```csharp
using System;
using System.Data;
using Aspose.Cells;
using System.Drawing;

public static DataTable GetData()
{
    var dt = new DataTable();
    dt.Columns.Add("Product", typeof(string));
    dt.Columns.Add("Price", typeof(decimal));

    dt.Rows.Add("Apple", 1.25m);
    dt.Rows.Add("Banana", 0.75m);
    dt.Rows.Add("Cherry", 2.10m);

    return dt;
}
```

> **Pourquoi c’est important :** Charger les données dans un `DataTable` vous donne une représentation tabulaire en mémoire que `ImportDataTable` peut consommer directement, éliminant ainsi le besoin d’insertion manuelle cellule par cellule.

## Étape 2 : Créer un tableau de styles – Un par colonne

La surcharge `ImportDataTable` que nous allons utiliser accepte un tableau d’objets `Style`. Chaque entrée correspond à un indice de colonne. Si vous laissez une entrée à `null`, la colonne hérite du style par défaut du classeur.

```csharp
// Initialize the workbook (Aspose.Cells)
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];

// Prepare the style array based on the number of columns
DataTable dataTable = GetData();
Style[] columnStyles = new Style[dataTable.Columns.Count];
```

> **Astuce :** Déclarer le tableau *après* avoir le `DataTable` garantit que la taille correspond exactement, évitant ainsi une `IndexOutOfRangeException` plus tard.

## Étape 3 : Définir la couleur de police (bleu) pour la première colonne

Une demande fréquente consiste à mettre en évidence les en‑têtes ou les colonnes clés avec une couleur de police distincte. Ici, nous rendons le texte de la première colonne bleu.

```csharp
// Style for the first column – blue font
columnStyles[0] = workbook.CreateStyle();
columnStyles[0].Font.Color = Color.Blue;
```

> **Pourquoi utiliser un objet style ?** Les styles sont réutilisables et appliqués en bloc, ce qui est bien plus rapide que d’itérer sur chaque cellule après l’importation. Le classeur met en cache le style une fois, puis le réutilise pour chaque cellule de cette colonne.

## Étape 4 : Formater la deuxième colonne en devise

Les formats numériques intégrés d’Excel sont identifiés par un indice. `14` correspond au format de devise par défaut (par ex., `$1 234,00`). Si vous avez besoin d’un format personnalisé, vous pouvez attribuer une chaîne de format à la place.

```csharp
// Style for the second column – built‑in currency format (ID 14)
columnStyles[1] = workbook.CreateStyle();
columnStyles[1].Number = 14; // 14 = built‑in currency format
```

> **Cas limite :** Si votre classeur utilise une locale où le symbole monétaire n’est pas `$`, le même indice s’adaptera automatiquement (par ex., `€` pour les locales allemandes).

## Étape 5 : Importer le DataTable avec les styles définis

Nous rassemblons maintenant le tout. La méthode `ImportDataTable` collera les données à partir de la cellule `A1` (ligne 0, colonne 0) et appliquera les styles que nous avons préparés.

```csharp
// Import the DataTable into the worksheet, applying the column styles
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
```

- Le deuxième paramètre `true` indique à Aspose.Cells de traiter la première ligne du `DataTable` comme des en‑têtes de colonne.  
- Les coordonnées `0, 0` spécifient le coin supérieur gauche où commence l’importation.  
- `columnStyles` associe chaque colonne à son style respectif.

## Étape 6 : Enregistrer le classeur (optionnel, mais pratique pour la vérification)

Si vous voulez voir le résultat dans Excel, il suffit d’enregistrer le classeur sur le disque. Cette étape n’est pas requise pour la logique de style, mais elle est utile pour le débogage.

```csharp
// Save the workbook to a file
workbook.Save("StyledReport.xlsx", SaveFormat.Xlsx);
Console.WriteLine("Workbook saved as StyledReport.xlsx");
```

### Résultat attendu

| **Product** (police bleue) | **Price** (devise) |
|----------------------------|--------------------|
| Apple                      | $1.25              |
| Banana                     | $0.75              |
| Cherry                     | $2.10              |

- La colonne *Product* apparaît en bleu, ce qui la fait ressortir.  
- La colonne *Price* affiche les valeurs avec le symbole monétaire par défaut et deux décimales.

---

## Questions fréquentes & Variantes

### Comment **définir le format de nombre d’une colonne** pour plus de deux colonnes ?

Il suffit d’étendre le tableau `columnStyles`. Par exemple, pour afficher un pourcentage dans la troisième colonne :

```csharp
columnStyles[2] = workbook.CreateStyle();
columnStyles[2].Number = 10; // 10 = built‑in percentage format
```

### Et si j’ai besoin d’un format de devise *personnalisé*, comme “USD 1,234.00” ?

Remplacez la propriété `Number` par une chaîne de format :

```csharp
columnStyles[1].Custom = "\"USD\" #,##0.00";
```

### Puis‑je appliquer un **set column font color** à une colonne numérique sans affecter son format de nombre ?

Absolument. Les styles sont composables. Vous pouvez définir à la fois `Font.Color` et `Number` sur la même instance `Style` :

```csharp
columnStyles[3] = workbook.CreateStyle();
columnStyles[3].Font.Color = Color.Green;
columnStyles[3].Number = 2; // 2 = built‑in date format (just an example)
```

### Que se passe‑t‑il si le `DataTable` possède plus de colonnes que de styles ?

Toute colonne sans style explicite (`null`) héritera du style par défaut du classeur. Pour éviter les `null` accidentels, vous pouvez initialiser tout le tableau avec un style de base d’abord :

```csharp
Style defaultStyle = workbook.CreateStyle();
defaultStyle.Font.Size = 11;
for (int i = 0; i < columnStyles.Length; i++)
    columnStyles[i] = defaultStyle;
```

Puis ne remplacer que les colonnes qui vous intéressent.

### Cette approche fonctionne‑t‑elle avec de grands ensembles de données (10 k+ lignes) ?

Oui. Comme le style est appliqué *une fois par colonne* avant l’importation, l’opération reste O(N) par rapport aux lignes, et la consommation mémoire reste faible. Évitez de boucler sur chaque cellule après l’importation — c’est là que les performances se dégradent.

---

## Exemple complet (prêt à copier‑coller)

```csharp
using System;
using System.Data;
using System.Drawing;
using Aspose.Cells;

class ExcelStyler
{
    static void Main()
    {
        // 1️⃣ Retrieve data
        DataTable dataTable = GetData();

        // 2️⃣ Create workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 3️⃣ Prepare style array (one per column)
        Style[] columnStyles = new Style[dataTable.Columns.Count];

        // 4️⃣ Style first column – blue font
        columnStyles[0] = workbook.CreateStyle();
        columnStyles[0].Font.Color = Color.Blue;

        // 5️⃣ Style second column – built‑in currency format (ID 14)
        columnStyles[1] = workbook.CreateStyle();
        columnStyles[1].Number = 14;

        // 6️⃣ (Optional) Add more styles here – e.g., percentage, custom formats

        // 7️⃣ Import the DataTable with styles
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

        // 8️⃣ Save to file for verification
        workbook.Save("StyledReport.xlsx", SaveFormat.Xlsx);
        Console.WriteLine("Excel file created: StyledReport.xlsx");
    }

    // Helper method to mock data
    public static DataTable GetData()
    {
        var dt = new DataTable();
        dt.Columns.Add("Product", typeof(string));
        dt.Columns.Add("Price", typeof(decimal));

        dt.Rows.Add("Apple", 1.25m);
        dt.Rows.Add("Banana", 0.75m);
        dt.Rows.Add("Cherry", 2.10m);
        return dt;
    }
}
```

Exécutez le programme, ouvrez `StyledReport.xlsx`, et vous verrez immédiatement le résultat de **appliquer le format de nombre excel**.

---

## Conclusion

Nous venons de démontrer une méthode propre et efficace pour **appliquer le format de nombre excel** à un `DataTable` importé. En préparant un tableau `Style[]` à l’avance, vous pouvez **formater une colonne en devise**, **définir le format de nombre d’une colonne**, et **définir la couleur de police d’une colonne** en un seul appel—sans post‑traitement.

N’hésitez pas à étendre le modèle : ajouter du style conditionnel, fusionner des cellules pour les titres, ou même injecter des formules. Les mêmes principes s’appliquent, gardant votre code ordonné et vos feuilles de calcul professionnelles.

---

### Et après ?

- Explorez le **formatage conditionnel** pour mettre en évidence les valeurs dépassant un seuil.  
- Combinez cette technique avec la **génération de tableaux croisés dynamiques** pour des rapports dynamiques.  
- Essayez de **définir le format de nombre d’une colonne** pour les dates, les pourcentages ou la notation scientifique personnalisée.

Vous avez une variante à partager ? Publiez‑la dans les commentaires—continuons à enrichir la communauté.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}