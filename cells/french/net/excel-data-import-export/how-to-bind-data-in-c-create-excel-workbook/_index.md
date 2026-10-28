---
category: general
date: 2026-03-27
description: Comment lier des données en C# avec Aspose.Cells – apprenez à enregistrer
  le classeur au format XLSX, ajouter un graphique et exporter le fichier Excel avec
  le graphique en quelques minutes.
draft: false
keywords:
- how to bind data
- save workbook as xlsx
- create excel workbook c#
- how to add chart
- export excel with chart
language: fr
og_description: Comment lier des données en C# avec Aspose.Cells. Ce guide vous montre
  comment enregistrer le classeur au format XLSX, ajouter un graphique et exporter
  Excel avec le graphique.
og_title: Comment lier des données en C# – Créer un classeur Excel
tags:
- Aspose.Cells
- C#
- Excel Automation
title: Comment lier des données en C# – Créer un classeur Excel
url: /fr/net/excel-data-import-export/how-to-bind-data-in-c-create-excel-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment lier des données en C# – Créer un classeur Excel

Vous vous êtes déjà demandé **comment lier des données** à un graphique en C# sans perdre patience ? Vous n'êtes pas seul. De nombreux développeurs se heurtent à un mur lorsqu'ils doivent générer programmétiquement des fichiers Excel qui ressemblent réellement à ceux qu'ils créeraient manuellement.  

Dans ce tutoriel, nous parcourrons un exemple complet, prêt à l'exécution, qui crée un classeur Excel, le remplit de données, lie ces données à un graphique en cascade (Waterfall), puis enregistre le fichier au format `.xlsx`. À la fin, vous saurez exactement comment **enregistrer un classeur au format XLSX**, **ajouter un graphique** à une feuille de calcul, et **exporter Excel avec graphique** pour les rapports en aval.

> **Prérequis** – Vous avez besoin d’Aspose.Cells pour .NET (la version d’essai gratuite suffit) et d’un environnement de développement .NET tel que Visual Studio 2022. Aucun autre package NuGet n’est requis.

---

## Ce que couvre ce guide

- **Créer un classeur Excel C#** – créer un nouveau `Workbook` et une feuille de calcul.  
- **Comment lier des données** – associer vos séries numériques et libellés de catégorie à la source de données du graphique.  
- **Comment ajouter un graphique** – insérer un graphique Waterfall et configurer son titre.  
- **Enregistrer le classeur au format XLSX** – persister le fichier sur le disque afin que tout le monde puisse l’ouvrir dans Excel.  
- **Exporter Excel avec graphique** – le produit final est un classeur pleinement fonctionnel que vous pouvez partager.

Si vous êtes à l’aise avec la syntaxe de base du C#, vous trouverez cela très simple. Plongeons‑y.

---

## Étape 1 : Créer un classeur Excel en C#  

Première chose à faire – nous avons besoin d’un objet classeur avec lequel travailler. Pensez à la classe `Workbook` comme le cahier vierge que vous remplirez plus tard de pages (feuilles) et de contenu.

```csharp
using Aspose.Cells;
using Aspose.Cells.Charts;

class WaterfallDemo
{
    static void Main()
    {
        // Initialize a new workbook – this is your blank Excel file.
        Workbook workbook = new Workbook();

        // Grab the first worksheet (index 0). It’s already created for us.
        Worksheet worksheet = workbook.Worksheets[0];
```

> **Astuce :** Si vous avez besoin de plusieurs feuilles, appelez simplement `workbook.Worksheets.Add()` et conservez une référence à chaque nouvelle `Worksheet`.

---

## Étape 2 : Remplir la feuille avec les catégories et les valeurs  

Nous allons maintenant **créer des données de type excel workbook c#**. L’exemple utilise un scénario classique de Waterfall : départ, revenu, coût, profit et fin.  

```csharp
        // Add header labels.
        worksheet.Cells["A1"].PutValue("Category");
        worksheet.Cells["B1"].PutValue("Amount");

        // Sample data – you can replace these with your own source (database, API, etc.).
        string[] categoryLabels = { "Start", "Revenue", "Cost", "Profit", "End" };
        double[] values = { 0, 150, -70, 0, 80 };

        // Fill rows 2‑6 with the data.
        for (int i = 0; i < categoryLabels.Length; i++)
        {
            worksheet.Cells[i + 1, 0].PutValue(categoryLabels[i]); // Column A
            worksheet.Cells[i + 1, 1].PutValue(values[i]);       // Column B
        }
```

Pourquoi mettre `0` pour « Start » et « Profit » ? Dans un graphique Waterfall, ces zéros servent de *connecteurs* qui assurent le bon flux visuel. Si vous les omettez, le graphique paraîtra cassé.

---

## Étape 3 : Comment ajouter un graphique – Insérer un graphique Waterfall  

Les données étant en place, il est temps de **comment ajouter un graphique**. Aspose.Cells rend cela aussi simple que d’appeler `Charts.Add`.

```csharp
        // Insert a Waterfall chart starting at row 7, column 0 and spanning to row 25, column 10.
        int chartIndex = worksheet.Charts.Add(ChartType.Waterfall, 7, 0, 25, 10);
        Chart waterfallChart = worksheet.Charts[chartIndex];

        // Give the chart a meaningful title.
        waterfallChart.Title.Text = "Quarterly Waterfall";
```

Les coordonnées `(7,0,25,10)` définissent la cellule en haut à gauche et la cellule en bas à droite de la boîte englobante du graphique. Ajustez‑les selon votre mise en page.

---

## Étape 4 : Comment lier des données – Connecter les séries et les catégories  

Voici le cœur du tutoriel : **comment lier des données** au graphique. La méthode `NSeries.Add` prend la plage des valeurs Y, tandis que `CategoryData` pointe vers les libellés de l’axe X.

```csharp
        // Bind the numeric series (values) – the second parameter “true” tells Aspose to treat it as a series.
        waterfallChart.NSeries.Add("B2:B6", true);

        // Bind the category (X‑axis) labels.
        waterfallChart.NSeries.CategoryData = "A2:A6";
```

Remarquez que nous référons aux mêmes cellules que nous avons remplies précédemment (`A2:A6` pour les catégories, `B2:B6` pour les montants). Si vous modifiez la disposition des données, mettez simplement à jour ces plages en conséquence.

---

## Étape 5 : Enregistrer le classeur au format XLSX – Persister le fichier  

Enfin, nous **enregistrons le classeur au format XLSX**. La méthode `Save` choisit automatiquement le bon format en fonction de l’extension du fichier.

```csharp
        // Save the workbook to disk. Replace YOUR_DIRECTORY with an actual path.
        workbook.Save("YOUR_DIRECTORY/WaterfallChart.xlsx");
    }
}
```

Lorsque vous ouvrirez `WaterfallChart.xlsx` dans Excel, vous verrez un graphique Waterfall correctement rendu qui reflète les données saisies. C’est la partie **exporter excel avec graphique** terminée.

---

## Résultat attendu  

- **Fichier Excel :** `WaterfallChart.xlsx` situé dans le dossier que vous avez spécifié.  
- **Disposition de la feuille :** la colonne A contient les catégories, la colonne B les montants, et le graphique se trouve sous le tableau.  
- **Aspect du graphique :** un graphique Waterfall intitulé « Quarterly Waterfall » avec cinq colonnes représentant Start, Revenue, Cost, Profit et End.  

![exemple de graphique waterfall lié aux données](waterfall_chart.png "Graphique Waterfall généré par Aspose.Cells")

*Le texte alternatif de l’image inclut le mot‑clé principal, aidant à la fois le SEO et la citation par l’IA.*

---

## Questions fréquentes & cas particuliers  

### Et si ma source de données est dynamique ?  
Remplacez les tableaux statiques par une boucle qui lit depuis une base de données ou une API. Tant que vous écrivez les valeurs dans la même plage de cellules, le code de liaison reste identique.

### Puis‑je changer le type de graphique ?  
Absolument. Remplacez `ChartType.Waterfall` par `ChartType.Column`, `ChartType.Line`, etc. N’oubliez pas d’ajuster les données de la série si le nouveau graphique attend une disposition différente.

### Comment définir les couleurs du graphique ?  
Utilisez `waterfallChart.NSeries[0].Format.Fill.ForeColor = Color.Yellow;` (ou n’importe quelle `System.Drawing.Color`). Cela est utile pour faire ressortir la colonne « Profit ».

### Et si je dois exporter en PDF au lieu de XLSX ?  
Appelez `workbook.Save("Report.pdf", SaveFormat.Pdf);`. Le graphique sera rendu automatiquement dans le PDF.

---

## Conseils pour un code prêt pour la production  

- **Libérer les objets** – Enveloppez `Workbook` dans un bloc `using` si vous êtes sous .NET Core afin de libérer rapidement les ressources.  
- **Gestion des chemins** – Utilisez `Path.Combine(Environment.CurrentDirectory, "WaterfallChart.xlsx")` pour éviter les séparateurs codés en dur.  
- **Gestion des erreurs** – Capturez `Exception` autour de `Save` pour détecter tôt les problèmes de permission ou d’espace disque.  
- **Vérification de version** – Aspose.Cells 23.10+ a introduit une prise en charge améliorée des graphiques Waterfall ; assurez‑vous d’utiliser une version récente pour de meilleurs résultats.

---

## Conclusion  

Vous disposez maintenant d’un exemple complet, de bout en bout, qui montre **comment lier des données** en C#, **créer excel workbook c#**, **comment ajouter un graphique**, **enregistrer le classeur au format xlsx**, et **exporter excel avec graphique**. Le code est prêt à être intégré dans n’importe quel projet .NET, et les concepts s’étendent à des ensembles de données plus volumineux et à d’autres types de graphiques.

Prêt pour l’étape suivante ? Essayez d’ajouter plusieurs séries, expérimentez les graphiques empilés, ou automatisez la génération de rapports mensuels à envoyer par e‑mail aux parties prenantes. Le ciel est la limite une fois que vous avez maîtrisé les bases de l’automatisation Excel avec Aspose.Cells.

Bon codage, et que vos feuilles de calcul s’affichent toujours parfaitement !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}