---
category: general
date: 2026-03-27
description: Comment créer un tableau croisé dynamique en C# avec Aspose.Cells – apprenez
  à ajouter des données, activer le rafraîchissement et enregistrer le classeur au
  format xlsx dans un seul tutoriel.
draft: false
keywords:
- how to create pivot
- save workbook as xlsx
- how to enable refresh
- how to add data
- generate excel file c#
language: fr
og_description: Comment créer un tableau croisé dynamique en C# avec Aspose.Cells.
  Ce guide vous montre comment ajouter des données, activer le rafraîchissement et
  enregistrer le classeur au format xlsx.
og_title: Comment créer un tableau croisé dynamique en C# – Tutoriel complet Aspose.Cells
tags:
- Aspose.Cells
- C#
- Excel automation
title: Comment créer un tableau croisé dynamique en C# – Guide complet avec Aspose.Cells
url: /fr/net/creating-and-configuring-pivot-tables/how-to-create-pivot-in-c-full-guide-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment créer un tableau croisé dynamique en C# – Tutoriel complet Aspose.Cells

Vous êtes‑vous déjà demandé **comment créer un tableau croisé dynamique** en C# sans vous battre avec l’interop COM ? Vous n'êtes pas le seul. Dans de nombreuses applications axées sur les données, nous avons besoin d’une méthode rapide pour transformer des chiffres de ventes bruts en un résumé propre, et Aspose.Cells rend cela très simple.  

Dans ce tutoriel, nous passerons en revue chaque étape : ajouter des données, créer le tableau croisé dynamique, activer le rafraîchissement automatique, et enfin **enregistrer le classeur au format xlsx** afin que vos utilisateurs puissent l’ouvrir immédiatement dans Excel. À la fin, vous disposerez d’un fichier `PivotRefresh.xlsx` prêt à l’emploi et d’une compréhension solide de l’importance de chaque ligne.

## Prérequis

- .NET 6+ (ou .NET Framework 4.7.2 et ultérieur) – tout runtime récent fonctionne.
- Aspose.Cells for .NET – vous pouvez le récupérer depuis NuGet (`Install-Package Aspose.Cells`).
- Une connaissance de base de la syntaxe C# – aucune connaissance approfondie d’Excel n’est requise.

> **Astuce :** Si vous travaillez sur une machine d’entreprise, assurez‑vous que la licence Aspose est appliquée ; sinon vous obtiendrez un filigrane sur le fichier généré.

## Étape 1 – Comment ajouter des données à un nouveau classeur

Avant qu’un tableau croisé dynamique puisse exister, il doit y avoir une table source. Nous créerons un nouveau classeur, nommerons la première feuille *SalesData*, et ajouterons quelques lignes qui imitent un véritable jeu de données de ventes.

```csharp
using Aspose.Cells;
using Aspose.Cells.Pivot;

class PivotRefreshTutorial
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and grab the default sheet
        var workbook = new Workbook();
        var salesDataSheet = workbook.Worksheets[0];
        salesDataSheet.Name = "SalesData";

        // 2️⃣ Write column headers
        salesDataSheet.Cells["A1"].PutValue("Region");
        salesDataSheet.Cells["B1"].PutValue("Product");
        salesDataSheet.Cells["C1"].PutValue("Units");
        salesDataSheet.Cells["D1"].PutValue("Revenue");

        // 3️⃣ Insert a sample row – add more rows as your scenario demands
        salesDataSheet.Cells["A2"].PutValue("East");
        salesDataSheet.Cells["B2"].PutValue("Widget");
        salesDataSheet.Cells["C2"].PutValue(120);
        salesDataSheet.Cells["D2"].PutValue(5400);
```

**Pourquoi c’est important :**  
- L’utilisation de `PutValue` définit automatiquement le type de cellule, vous n’avez donc pas à vous soucier des incompatibilités entre chaînes et nombres plus tard.  
- Définir les en‑têtes dans la ligne 1 fournit au moteur du tableau croisé dynamique une référence lors du mappage des champs.

## Étape 2 – Créer une feuille qui hébergera le tableau croisé dynamique

Un tableau croisé dynamique réside sur sa propre feuille, gardant les données source propres et le rapport ordonné.

```csharp
        // 4️⃣ Add a dedicated sheet for the pivot
        var pivotSheet = workbook.Worksheets.Add("PivotReport");
```

> **Et si vous avez déjà une feuille ?** Référez‑vous simplement à elle par son indice (`workbook.Worksheets["MySheet"]`) au lieu d’en ajouter une nouvelle.

## Étape 3 – Définir la plage source (Comment ajouter des données → Définir la plage)

Aspose.Cells a besoin d’un `CellArea` ou d’une chaîne de plage qui englobe à la fois les en‑têtes et les données. Ici, nous supposons un maximum de 100 lignes ; ajustez selon vos besoins.

```csharp
        // 5️⃣ Build the source range (A1:D100 covers headers + up to 99 data rows)
        var sourceRange = salesDataSheet.Cells.CreateRange("A1:D100");
```

**Cas particulier :** Si votre jeu de données est dynamique, vous pouvez calculer la dernière ligne utilisée avec `salesDataSheet.Cells.MaxDataRow` et construire la plage en conséquence.

## Étape 4 – Comment créer un tableau croisé dynamique – Insérer le tableau croisé dynamique

Maintenant la partie amusante : nous demandons à Aspose.Cells de créer un tableau croisé dynamique lié à la plage que nous venons de définir.

```csharp
        // 6️⃣ Insert the pivot table at cell A3 of the pivot sheet
        int pivotIndex = pivotSheet.PivotTables.Add("=SalesData!A1:D100", "A3", "SalesPivot");
        var pivotTable = pivotSheet.PivotTables[pivotIndex];
```

Remarquez la référence de type formule (`=SalesData!A1:D100`). C’est la même syntaxe que vous taperiez dans Excel, ce qui rend l’API intuitive.

## Étape 5 – Configurer les champs de lignes, colonnes et données (Comment ajouter des données → Champs)

Nous placerons *Region* sur les lignes, *Product* sur les colonnes, et sommerons à la fois *Units* et *Revenue*.

```csharp
        // 7️⃣ Set up row, column, and data fields
        pivotTable.RowFields.Add(0); // 0 = first column => Region
        pivotTable.ColumnFields.Add(1); // 1 = second column => Product
        pivotTable.DataFields.Add(2, "Sum of Units", PivotTableDataAggregationType.Sum);
        pivotTable.DataFields.Add(3, "Sum of Revenue", PivotTableDataAggregationType.Sum);
```

**Pourquoi ces indices ?**  
Aspose.Cells indexe les colonnes à partir de 0, donc `0` correspond à *Region*. La méthode `DataFields.Add` vous permet de renommer le champ (par ex., « Sum of Units ») et de choisir un type d’agrégation – `Sum` est le plus courant pour les données numériques.

## Étape 6 – Comment activer le rafraîchissement – Faire en sorte que le tableau croisé dynamique se mette à jour automatiquement à l’ouverture

Si les données source changent plus tard, vous voudrez probablement que le tableau croisé dynamique reflète ces changements automatiquement. C’est là que `RefreshDataOnOpen` brille.

```csharp
        // 8️⃣ Turn on automatic refresh when the file is opened
        pivotTable.RefreshDataOnOpen = true;
```

> **Note :** Ce drapeau ne fonctionne que lorsque le classeur est ouvert dans Excel ; il ne recalculera pas à l’intérieur d’Aspose.Cells sauf si vous appelez manuellement `pivotTable.RefreshData()`.

## Étape 7 – Enregistrer le classeur au format XLSX (Comment enregistrer le classeur au format XLSX)

Enfin, nous persistons le fichier sur le disque. Le format `.xlsx` est le type de fichier Excel moderne, basé sur zip, qui fonctionne partout.

```csharp
        // 9️⃣ Save the workbook – this also satisfies the “save workbook as xlsx” requirement
        workbook.Save("PivotRefresh.xlsx");
    }
}
```

L’exécution du programme génère un fichier nommé **PivotRefresh.xlsx** dans le dossier d’exécution. Ouvrez‑le dans Excel et vous verrez un tableau croisé dynamique bien présenté avec des lignes *Region*, des colonnes *Product*, et les valeurs *Units* et *Revenue* sommées. Comme nous avons activé le rafraîchissement, toute modification que vous apportez à la feuille *SalesData* mettra automatiquement à jour le tableau croisé dynamique la prochaine fois que vous ouvrirez le classeur.

### Résultat attendu

| Region | Widget | Gadget | … |
|--------|--------|--------|---|
| East   | 120    | 0      |   |
| West   | 0      | 85     |   |
| **Grand Total** | **120** | **85** |   |

*(Les nombres varieront en fonction des lignes que vous ajoutez.)*

---

## Questions fréquentes & variantes

### Et si j’ai besoin de plusieurs tableaux croisés dynamiques ?

Vous pouvez répéter **l’étape 4** avec un nom et un emplacement différents. Chaque appel à `PivotTables.Add` renvoie un nouvel indice que vous pouvez utiliser pour récupérer l’objet du tableau.

### Comment changer l’agrégation en *Average* au lieu de *Sum* ?

Remplacez `PivotTableDataAggregationType.Sum` par `PivotTableDataAggregationType.Average` dans les appels `DataFields.Add`.

### Puis‑je styliser le tableau croisé dynamique (polices, couleurs) ?

Oui. Après avoir créé le tableau croisé dynamique, vous pouvez accéder à sa propriété `Style` ou appliquer un format de cellule à la plage qui contient le tableau. Par exemple :

```csharp
pivotTable.Style = workbook.Styles[workbook.Styles.Add()];
pivotTable.Style.Font.Color = System.Drawing.Color.DarkBlue;
```

### Est‑il possible d’ajouter plus de lignes après l’enregistrement du classeur ?

Absolument. Chargez le fichier avec `new Workbook("PivotRefresh.xlsx")`, ajoutez des lignes à la feuille *SalesData*, et appelez `pivotTable.RefreshData()` avant de sauvegarder à nouveau.

---

## Exemple complet fonctionnel (prêt à copier‑coller)

```csharp
using Aspose.Cells;
using Aspose.Cells.Pivot;

class PivotRefreshTutorial
{
    static void Main()
    {
        // Step 1: Create workbook & add sample data
        var workbook = new Workbook();
        var salesDataSheet = workbook.Worksheets[0];
        salesDataSheet.Name = "SalesData";

        salesDataSheet.Cells["A1"].PutValue("Region");
        salesDataSheet.Cells["B1"].PutValue("Product");
        salesDataSheet.Cells["C1"].PutValue("Units");
        salesDataSheet.Cells["D1"].PutValue("Revenue");

        // Sample rows – extend as needed
        salesDataSheet.Cells["A2"].PutValue("East");
        salesDataSheet.Cells["B2"].PutValue("Widget");
        salesDataSheet.Cells["C2"].PutValue(120);
        salesDataSheet.Cells["D2"].PutValue(5400);

        salesDataSheet.Cells["A3"].PutValue("West");
        salesDataSheet.Cells["B3"].PutValue("Gadget");
        salesDataSheet.Cells["C3"].PutValue(85);
        salesDataSheet.Cells["D3"].PutValue(4250);

        // Step 2: Add sheet for the pivot
        var pivotSheet = workbook.Worksheets.Add("PivotReport");

        // Step 3: Define source range (covers up to 100 rows)
        var sourceRange = salesDataSheet.Cells.CreateRange("A1:D100");

        // Step 4: Insert pivot table
        int pivotIndex = pivotSheet.PivotTables.Add("=SalesData!A1:D100", "A3", "SalesPivot");
        var pivotTable = pivotSheet.PivotTables[pivotIndex];

        // Step 5: Configure fields
        pivotTable.RowFields.Add(0); // Region
        pivotTable.ColumnFields.Add(1); // Product
        pivotTable.DataFields.Add(2, "Sum of Units", PivotTableDataAggregationType.Sum);
        pivotTable.DataFields.Add(3, "Sum of Revenue", PivotTableDataAggregationType.Sum);

        // Step 6: Enable automatic refresh
        pivotTable.RefreshDataOnOpen = true;

        // Step 7: Save as .xlsx
        workbook.Save("PivotRefresh.xlsx");
    }
}
```

Enregistrez le fichier, exécutez‑le, et ouvrez le **PivotRefresh.xlsx** généré – vous venez de maîtriser **comment créer un tableau croisé dynamique** en C#.

---

## Conclusion

Nous avons couvert **comment créer des tableaux croisés dynamiques** de façon programmatique, comment **ajouter des données**, comment **activer le rafraîchissement**, et enfin comment **enregistrer le classeur au format xlsx** en utilisant Aspose.Cells. Le code

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}