---
category: general
date: 2026-03-30
description: Créer un classeur Excel en C# avec format monétaire. Apprenez à importer
  un DataTable, à ajouter un format numérique dans Excel et à appliquer le format
  monétaire à une colonne en quelques minutes.
draft: false
keywords:
- create excel workbook c#
- format cells currency
- import datatable to excel
- add number format excel
- apply currency format column
language: fr
og_description: Créez un classeur Excel en C# et formatez instantanément les cellules
  en devise. Ce tutoriel étape par étape montre comment importer un DataTable dans
  Excel et ajouter un format numérique à une colonne.
og_title: Créer un classeur Excel C# – Guide de formatage des devises
tags:
- Aspose.Cells
- C#
- Excel automation
title: Créer un classeur Excel en C# – Appliquer le format monétaire et importer un
  DataTable
url: /fr/net/excel-data-import-export/create-excel-workbook-c-apply-currency-format-and-import-dat/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un classeur Excel C# – Appliquer le format monétaire et importer un DataTable

Vous avez déjà eu besoin de **créer un classeur Excel C#** qui ressemble déjà à un rapport soigné ? Peut‑être récupérez‑vous des chiffres de ventes depuis une base de données et vous voulez que la colonne prix s’affiche en dollars sans devoir bidouiller Excel manuellement. Ça vous parle ? Vous n’êtes pas seul — la plupart des développeurs rencontrent ce problème lorsqu’ils automatisent leurs exportations Excel pour la première fois.

Dans ce guide, nous parcourrons une solution complète, prête à l’emploi, qui **crée un classeur Excel C#**, importe un `DataTable`, et **formate la colonne Price en monnaie**. À la fin, vous disposerez d’un fichier nommé `StyledTable.xlsx` que vous pourrez ouvrir et voir des nombres correctement formatés. Aucun post‑traitement supplémentaire n’est requis.

> **Ce que vous allez apprendre**
> - Comment configurer Aspose.Cells dans un projet .NET  
> - Comment **importer datatable to excel** avec un tableau de styles  
> - Comment **add number format excel** pour une colonne spécifique  
> - Astuces pour gérer davantage de colonnes ou des paramètres régionaux différents  

> **Prérequis**  
> - .NET 6+ (ou .NET Framework 4.6+) installé  
> - Package NuGet Aspose.Cells for .NET (`Install-Package Aspose.Cells`)  
> - Familiarité de base avec C# et les DataTables  

---

## Étape 1 : Préparer le DataTable (import datatable to excel)

Tout d’abord, nous avons besoin de quelques données d’exemple. Dans une application réelle, vous remplirez probablement ce tableau à partir d’une requête DB, mais un exemple codé en dur simplifie les choses.

```csharp
using System.Data;

// Create a DataTable with two columns: Product (string) and Price (double)
DataTable dataTable = new DataTable();
dataTable.Columns.Add("Product", typeof(string));
dataTable.Columns.Add("Price", typeof(double));

// Add a few rows – you can add as many as you like
dataTable.Rows.Add("Apple", 1.23);
dataTable.Rows.Add("Banana", 0.78);
dataTable.Rows.Add("Cherry", 2.50);
```

*Pourquoi c’est important* : le `DataTable` fait le lien entre vos données métier et le fichier Excel. Aspose.Cells peut l’importer directement, en conservant les noms de colonnes et les types de données.

---

## Étape 2 : Créer un nouveau classeur (create excel workbook c#)

Nous créons maintenant l’objet fichier Excel proprement dit. Pensez‑y comme à une toile vierge sur laquelle vous allez peindre.

```csharp
using Aspose.Cells;

// Instantiate a fresh workbook – this is the core of create excel workbook c#
Workbook workbook = new Workbook();

// Grab the first worksheet (index 0). You could also add more sheets later.
Worksheet worksheet = workbook.Worksheets[0];
```

> **Astuce :** Si vous avez besoin de plusieurs feuilles, appelez `workbook.Worksheets.Add()` et donnez à chacune un nom significatif.

---

## Étape 3 : Définir un style monétaire (format cells currency)

Aspose.Cells vous permet de créer un objet `Style` qui décrit l’apparence des cellules. Pour la monnaie, nous utilisons l’ID de format numérique intégré 164 (`"$#,##0.00"`).

```csharp
// Create a new style object for the price column
Style priceStyle = workbook.CreateStyle();
priceStyle.Number = 164; // Built‑in currency format "$#,##0.00"
```

*Pourquoi ne pas simplement définir la chaîne de format ?* Utiliser l’ID intégré garantit la compatibilité entre les versions d’Excel et évite les particularités liées aux paramètres régionaux.

---

## Étape 4 : Construire le tableau de styles (apply currency format column)

Lors de l’importation d’un `DataTable`, vous pouvez passer un tableau d’objets `Style` — un par colonne. `null` signifie « utiliser le style par défaut ». Ici, nous appliquons `priceStyle` uniquement à la deuxième colonne.

```csharp
// Column 0 (Product) gets the default style, Column 1 (Price) gets the currency style
Style[] columnStyles = { null, priceStyle };
```

Si vous ajoutez plus tard d’autres colonnes, il suffit d’étendre le tableau en conséquence. La longueur de `columnStyles` doit correspondre au nombre de colonnes que vous importez, sinon Aspose lèvera une exception.

---

## Étape 5 : Importer le DataTable avec les styles (import datatable to excel)

Le moment magique arrive — notre `DataTable` atterrit dans la feuille, et la colonne prix s’affiche immédiatement en monnaie.

```csharp
// Parameters:
//  - dataTable: source data
//  - true: include column headers
//  - startRow: 0 (top of sheet)
//  - startColumn: 0 (first column)
//  - columnStyles: style array defined above
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
```

*Et si vous avez plus de deux colonnes ?* Il suffit d’étendre `columnStyles` afin que chaque colonne reçoive le style approprié (ou `null` pour le style par défaut). C’est la façon la plus propre d’**add number format excel** sélectivement.

---

## Étape 6 : Enregistrer le classeur (create excel workbook c#)

Enfin, nous écrivons le fichier sur le disque. Choisissez n’importe quel dossier où vous avez les droits d’écriture.

```csharp
// Save the workbook as an XLSX file
workbook.Save("YOUR_DIRECTORY/StyledTable.xlsx");
```

Ouvrez `StyledTable.xlsx` dans Excel et vous devriez voir :

| Product | Price |
|---------|-------|
| Apple   | $1.23 |
| Banana  | $0.78 |
| Cherry  | $2.50 |

La colonne **Price** est déjà formatée en monnaie — aucune étape supplémentaire n’est nécessaire.

---

## Cas limites et variantes

### Plus de colonnes, formats différents

Si vous devez **format cells currency** pour plusieurs colonnes (par ex. Cost, Tax, Total), créez un `Style` distinct pour chacune et remplissez `columnStyles` en conséquence :

```csharp
Style costStyle = workbook.CreateStyle();
costStyle.Number = 164; // currency

Style taxStyle = workbook.CreateStyle();
taxStyle.Number = 164;

// Assuming columns: Product, Cost, Tax, Total
Style[] styles = { null, costStyle, taxStyle, priceStyle };
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, styles);
```

### Monnaie spécifique à un paramètre régional

Pour l’euro ou la livre sterling, utilisez d’autres IDs intégrés (par ex. 165 pour `€#,##0.00`). Vous pouvez également définir une chaîne de format personnalisée :

```csharp
priceStyle.Custom = "€#,##0.00";
```

### Jeux de données volumineux

Aspose.Cells peut gérer des millions de lignes, mais la consommation mémoire augmente avec les objets de style. Réutilisez une seule instance de `Style` pour toutes les colonnes monétaires afin de garder l’empreinte faible.

### Styles manquants

Si `columnStyles` est plus court que le nombre de colonnes, Aspose appliquera le style par défaut aux colonnes restantes. Cela est pratique lorsque vous ne vous souciez que de quelques colonnes.

---

## Exemple complet (Toutes les étapes combinées)

Voici le programme complet que vous pouvez copier‑coller dans une application console. Il regroupe tous les éléments présentés, avec quelques commentaires utiles.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Build sample DataTable (import datatable to excel)
        // -------------------------------------------------
        DataTable dataTable = new DataTable();
        dataTable.Columns.Add("Product", typeof(string));
        dataTable.Columns.Add("Price", typeof(double));
        dataTable.Rows.Add("Apple", 1.23);
        dataTable.Rows.Add("Banana", 0.78);
        dataTable.Rows.Add("Cherry", 2.50);
        // You can add as many rows as you like here.

        // -------------------------------------------------
        // Step 2: Create a new workbook (create excel workbook c#)
        // -------------------------------------------------
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // -------------------------------------------------
        // Step 3: Define a currency style (format cells currency)
        // -------------------------------------------------
        Style priceStyle = workbook.CreateStyle();
        priceStyle.Number = 164; // "$#,##0.00" – built‑in currency format

        // -------------------------------------------------
        // Step 4: Build the style array (apply currency format column)
        // -------------------------------------------------
        // First column gets default style (null), second column uses priceStyle.
        Style[] columnStyles = { null, priceStyle };

        // -------------------------------------------------
        // Step 5: Import the DataTable with the style array
        // -------------------------------------------------
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

        // -------------------------------------------------
        // Step 6: Save the workbook to disk
        // -------------------------------------------------
        string outputPath = @"YOUR_DIRECTORY\StyledTable.xlsx";
        workbook.Save(outputPath);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

**Résultat attendu** : l’ouverture de `StyledTable.xlsx` montre la colonne `Price` avec le symbole dollar et deux décimales, exactement comme l’instruction **format cells currency** le demandait.

---

## Foire aux questions

**Q : Cela fonctionne‑t‑il avec .NET Core ?**  
R : Absolument. Aspose.Cells est compatible .NET‑standard, vous pouvez donc cibler .NET 5, .NET 6 ou une version ultérieure sans modification.

**Q : Et si mon DataTable possède 10 colonnes mais que je ne veux formater que la colonne 5 ?**  
R : Créez un `Style[]` de longueur 10, remplissez les positions 0‑4 et 6‑9 avec `null`, et placez votre style personnalisé à l’indice 4 (index zéro‑based). Aspose respectera chaque entrée.

**Q : Puis‑je masquer la ligne d’en‑tête ?**  
R : Après l’importation, définissez `worksheet.Cells.Rows[0].Hidden = true;` ou passez simplement `false` au paramètre `includeColumnNames` de `ImportDataTable`.

---

## Conclusion

Nous venons de **créer un classeur Excel C#**, d’importer un `DataTable`, et d’**appliquer un format monétaire à une colonne** grâce à Aspose.Cells. Les étapes principales — préparation des données, définition d’un style, construction du tableau de styles, importation avec `ImportDataTable`, et sauvegarde — couvrent le cœur de la plupart des tâches d’automatisation Excel.

À partir d’ici, vous pourriez explorer :

- **add number format excel** pour les dates ou les pourcentages  
- Exporter plusieurs feuilles dans un même fichier  
- Utiliser **format cells currency** avec des symboles spécifiques à un paramètre régional  
- Automatiser la création de graphiques à partir des mêmes données  

Essayez ces pistes, et vous deviendrez rapidement la référence Excel de votre équipe. Vous avez une variante à partager ? Laissez un commentaire ci‑dessous—bon codage !  

![create excel workbook c# screenshot](image.png "create excel workbook c#")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}