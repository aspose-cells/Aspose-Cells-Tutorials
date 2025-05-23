---
"description": "Apprenez à créer un graphique à secteurs dans Excel avec Aspose.Cells pour .NET grâce à ce guide étape par étape. Visualisez vos données sans effort."
"linktitle": "Créer un graphique à secteurs"
"second_title": "API de traitement Excel Aspose.Cells .NET"
"title": "Créer un graphique à secteurs"
"url": "/fr/net/manipulating-chart-types/create-pie-chart/"
"weight": 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Créer un graphique à secteurs

## Introduction

Créer des graphiques est essentiel pour représenter visuellement les données, et les diagrammes à secteurs sont l'un des moyens les plus populaires d'illustrer la composition d'un tout. Avec Aspose.Cells pour .NET, vous pouvez facilement automatiser la génération de diagrammes à secteurs dans des fichiers Excel. Dans ce tutoriel, nous allons découvrir comment créer un diagramme à secteurs de A à Z avec Aspose.Cells pour .NET, avec un guide étape par étape pour un processus simple et fluide. Que vous soyez novice en matière d'automatisation Excel ou que vous souhaitiez améliorer vos compétences, ce guide est fait pour vous !

## Prérequis

Avant de plonger dans le code, assurez-vous d'avoir la configuration suivante :

1. Bibliothèque Aspose.Cells pour .NET : Assurez-vous qu'Aspose.Cells est installé dans votre projet. Si ce n'est pas déjà fait, vous pouvez le télécharger ici. [ici](https://releases.aspose.com/cells/net/).
2. Environnement de développement .NET : assurez-vous que votre projet est configuré pour utiliser .NET Framework ou .NET Core.
3. Connaissances de base de C# : vous devez être à l’aise avec la programmation C#, en particulier la programmation orientée objet (POO).

Pour les utilisateurs avancés, une licence temporaire permet d'accéder à toutes les fonctionnalités d'Aspose.Cells. Vous pouvez en faire la demande auprès de [ici](https://purchase.aspose.com/temporary-license/).

## Importer des packages

Pour commencer, importez les espaces de noms et les packages nécessaires à ce tutoriel. Ceux-ci incluent les opérations d'E/S de base et le package Aspose.Cells.

```csharp
using System;
using System.IO;

using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
using Aspose.Cells.Charts;
```

## Étape 1 : Créer un nouveau classeur

Tout d’abord, nous devons créer une instance du `Workbook` classe, qui représente le fichier Excel. Un classeur contient plusieurs feuilles ; dans notre exemple, nous travaillerons avec deux feuilles : une pour les données et une pour le graphique à secteurs.

```csharp
Workbook workbook = new Workbook();
```

Ceci initialise un nouveau classeur Excel. Mais où vont les données ? Nous nous en occuperons à l'étape suivante.

## Étape 2 : Ajouter des données à la feuille de calcul

Une fois le classeur créé, nous devons accéder à la première feuille de calcul et lui donner un nom. C'est ici que nous saisirons les données nécessaires au graphique à secteurs.

```csharp
Worksheet sheet = workbook.Worksheets[0];
sheet.Name = "Data";
Cells cells = sheet.Cells;
```

Nous pouvons maintenant saisir des données de ventes fictives représentant différentes régions :

```csharp
cells["A1"].PutValue("Region");
cells["A2"].PutValue("France");
cells["A3"].PutValue("Germany");
cells["A4"].PutValue("England");
cells["A5"].PutValue("Sweden");
cells["A6"].PutValue("Italy");
cells["A7"].PutValue("Spain");
cells["A8"].PutValue("Portugal");

cells["B1"].PutValue("Sales");
cells["B2"].PutValue(70000);
cells["B3"].PutValue(55000);
cells["B4"].PutValue(30000);
cells["B5"].PutValue(40000);
cells["B6"].PutValue(35000);
cells["B7"].PutValue(32000);
cells["B8"].PutValue(10000);
```

Ici, nous ajoutons deux colonnes : une pour les régions et une autre pour les chiffres de vente. Ces données seront représentées dans le graphique à secteurs.

## Étape 3 : Ajouter une feuille de graphique

Ensuite, ajoutons une feuille de calcul distincte pour contenir le graphique à secteurs.

```csharp
int sheetIndex = workbook.Worksheets.Add(SheetType.Chart);
Worksheet chartSheet = workbook.Worksheets[sheetIndex];
chartSheet.Name = "Chart";
```

Cette nouvelle feuille hébergera le graphique à secteurs. En lui donnant un nom tel que « Graphique », les utilisateurs sauront à quoi s'attendre à l'ouverture du fichier.

## Étape 4 : Créer le graphique à secteurs

Il est maintenant temps de créer le graphique. Nous allons spécifier que nous voulons un graphique à secteurs et définir sa position sur la feuille.

```csharp
int chartIndex = chartSheet.Charts.Add(Aspose.Cells.Charts.ChartType.Pie, 5, 0, 25, 10);
Aspose.Cells.Charts.Chart chart = chartSheet.Charts[chartIndex];
```

La méthode `Add()` accepte les paramètres pour le type de graphique (dans ce cas, `ChartType.Pie`) et son emplacement sur la feuille de calcul. Les nombres représentent les positions des lignes et des colonnes.

## Étape 5 : Personnaliser l’apparence du graphique

Un graphique à secteurs ne serait pas complet sans quelques personnalisations ! Améliorez l'esthétique de votre graphique en modifiant les couleurs, les libellés et le titre.

### Définir le titre du graphique
```csharp
chart.Title.Text = "Sales By Region";
chart.Title.Font.Color = Color.Blue;
chart.Title.Font.IsBold = true;
chart.Title.Font.Size = 12;
```

### Personnaliser la zone de tracé
```csharp
chart.PlotArea.Area.ForegroundColor = Color.Coral;
chart.PlotArea.Area.FillFormat.SetTwoColorGradient(Color.Yellow, Color.White, GradientStyleType.Vertical, 2);
chart.PlotArea.Border.IsVisible = false;
```

Nous définissons le remplissage dégradé pour la zone de tracé et masquons la bordure pour un aspect plus net.

## Étape 6 : Définir les données du graphique

Il est temps de relier le graphique à nos données. `NSeries` La propriété du graphique lie les chiffres de vente et les régions au graphique à secteurs.

```csharp
chart.NSeries.Add("Data!B2:B8", true);
chart.NSeries.CategoryData = "Data!A2:A8";
chart.NSeries.IsColorVaried = true;
```

La première ligne spécifie que nous utilisons les données de vente des cellules `B2:B8`Nous demandons également au graphique d'utiliser les noms de région de `A2:A8` comme étiquettes de catégorie.

## Étape 7 : Ajouter des étiquettes de données

L'ajout d'étiquettes directement aux segments du graphique peut faciliter la compréhension. Intégrons les noms des régions et les valeurs des ventes dans les secteurs du graphique à secteurs.

```csharp
for (int i = 0; i < chart.NSeries.Count; i++)
{
    DataLabels labels = chart.NSeries[i].DataLabels;
    labels.ShowCategoryName = true;
    labels.ShowValue = true;
    labels.Position = LabelPositionType.InsideBase;
}
```

## Étape 8 : Personnaliser la zone du graphique et la légende

Enfin, apportons quelques touches finales à la zone graphique et à la légende. Cela améliorera la présentation générale du graphique.

### Zone graphique
```csharp
ChartArea chartArea = chart.ChartArea;
chartArea.Area.Formatting = FormattingType.Custom;
chartArea.Area.FillFormat.Texture = TextureType.BlueTissuePaper;
```

### Légende
```csharp
Legend legend = chart.Legend;
legend.Position = LegendPositionType.Left;
legend.Font.IsBold = true;
legend.Border.Color = Color.Blue;
legend.Area.FillFormat.Texture = TextureType.Bouquet;
```

## Étape 9 : Enregistrer le classeur

Enfin, nous enregistrons le classeur dans un fichier Excel. Vous pouvez spécifier le répertoire de sortie et le nom du fichier selon vos besoins.

```csharp
workbook.Save(outputDir + "outputHowToCreatePieChart.xlsx");
```

## Conclusion

Créer un graphique à secteurs avec Aspose.Cells pour .NET est un processus simple et personnalisable. En suivant ce guide, vous pouvez générer un graphique professionnel qui transmet des informations précieuses en quelques étapes seulement. Que ce soit pour des rapports d'entreprise ou à des fins pédagogiques, maîtriser la création de graphiques améliorera vos compétences en automatisation Excel. N'oubliez pas qu'Aspose.Cells vous offre la flexibilité nécessaire pour créer facilement des fichiers Excel époustouflants et riches en données.

## FAQ

### Puis-je créer d’autres types de graphiques à l’aide d’Aspose.Cells pour .NET ?
Oui ! Aspose.Cells prend en charge différents types de graphiques, notamment les graphiques à barres, les graphiques linéaires et les nuages de points.

### Ai-je besoin d’une licence payante pour utiliser Aspose.Cells pour .NET ?
Vous pouvez utiliser la version gratuite avec certaines limitations. Pour accéder à toutes les fonctionnalités, une licence est nécessaire, que vous pouvez acheter. [ici](https://purchase.aspose.com/buy).

### Puis-je exporter le graphique vers des formats tels que PDF ou images ?
Absolument ! Aspose.Cells vous permet d'exporter des graphiques vers différents formats, notamment PDF et PNG.

### Est-il possible de styliser chaque part de tarte avec des couleurs différentes ?
Oui, vous pouvez appliquer des couleurs différentes à chaque tranche en définissant le `IsColorVaried` propriété à `true`, comme indiqué dans le tutoriel.

### Puis-je automatiser la génération de plusieurs graphiques dans un seul classeur ?
Oui, vous pouvez créer et personnaliser autant de graphiques que nécessaire dans un seul fichier Excel.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}