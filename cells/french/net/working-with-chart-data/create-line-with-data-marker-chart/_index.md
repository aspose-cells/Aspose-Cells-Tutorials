---
title: Créer une ligne avec un graphique de marqueurs de données
linktitle: Créer une ligne avec un graphique de marqueurs de données
second_title: API de traitement Excel Aspose.Cells .NET
description: Découvrez comment créer un graphique de type Ligne avec marqueurs de données dans Excel à l'aide d'Aspose.Cells pour .NET. Suivez ce guide étape par étape pour générer et personnaliser facilement des graphiques.
weight: 10
url: /fr/net/working-with-chart-data/create-line-with-data-marker-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer une ligne avec un graphique de marqueurs de données

## Introduction

Vous êtes-vous déjà demandé comment créer de superbes graphiques dans Excel par programmation ? Eh bien, attachez vos ceintures, car aujourd'hui, nous allons nous plonger dans la création d'un graphique en ligne avec marqueur de données à l'aide d'Aspose.Cells pour .NET. Ce didacticiel vous guidera à travers chaque étape, en vous assurant une bonne maîtrise de la génération de graphiques, même si vous débutez avec Aspose.Cells.

## Prérequis

Avant de commencer, assurez-vous que tout est en place pour suivre le processus de manière fluide.

1. Bibliothèque Aspose.Cells pour .NET – Vous devrez l'installer. Vous pouvez l'obtenir[ici](https://releases.aspose.com/cells/net/).
2. .NET Framework – Assurez-vous que votre environnement de développement est configuré avec la dernière version de .NET.
3. IDE (environnement de développement intégré) – Visual Studio est recommandé.
4.  Une licence Aspose.Cells valide – Si vous n'en avez pas, vous pouvez en demander une[permis temporaire](https://purchase.aspose.com/temporary-license/) ou consultez leur[essai gratuit](https://releases.aspose.com/).

Prêt à partir ? Décomposons tout ça !

## Importer les packages nécessaires

Pour commencer, assurez-vous d'importer les espaces de noms suivants dans votre projet. Ceux-ci fourniront les classes et méthodes nécessaires pour créer votre graphique.

```csharp
using System;
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Charts;
using System.Drawing;
```

Une fois que vous avez compris cela, nous pouvons commencer à coder !

## Étape 1 : Configurez votre classeur et votre feuille de calcul

Tout d’abord, vous devez créer un nouveau classeur et accéder à la première feuille de calcul.

```csharp
//Répertoire de sortie
static string outputDir = "Your Document Directory";
		
// Instancier un classeur
Workbook workbook = new Workbook();

// Accéder à la première feuille de calcul
Worksheet worksheet = workbook.Worksheets[0];
```

Considérez le classeur comme votre fichier Excel et la feuille de calcul comme la feuille spécifique qu'il contient. Dans ce cas, nous travaillons avec la première feuille.

## Étape 2 : Remplir la feuille de calcul avec des données

Maintenant que nous avons notre feuille de calcul, remplissons-la avec des données. Nous créons des points de données aléatoires pour deux séries de valeurs.

```csharp
// Définir le titre des colonnes
worksheet.Cells[0, 0].Value = "X";
worksheet.Cells[0, 1].Value = "Y";

// Données aléatoires pour générer le graphique
Random R = new Random();

// Créez des données aléatoires et enregistrez-les dans les cellules
for (int i = 1; i < 21; i++)
{
    worksheet.Cells[i, 0].Value = i;
    worksheet.Cells[i, 1].Value = 0.8;
}

for (int i = 21; i < 41; i++)
{
    worksheet.Cells[i, 0].Value = i - 20;
    worksheet.Cells[i, 1].Value = 0.9;
}
```

Ici, nous utilisons des nombres aléatoires pour simuler des données, mais dans les applications réelles, vous pouvez les remplir avec des valeurs réelles de votre ensemble de données.

## Étape 3 : Ajoutez le graphique à la feuille de calcul

Ensuite, nous ajoutons le graphique à la feuille de calcul et choisissons le type – dans ce cas, un graphique en ligne avec des marqueurs de données.

```csharp
// Ajouter un graphique à la feuille de calcul
int idx = worksheet.Charts.Add(ChartType.LineWithDataMarkers, 1, 3, 20, 20);

// Accéder au graphique nouvellement créé
Chart chart = worksheet.Charts[idx];
```

Cet extrait ajoute un graphique linéaire avec des marqueurs de données à la feuille de calcul, en le plaçant dans une plage spécifique (1,3 à 20,20). Plutôt simple, non ?

## Étape 4 : Personnaliser l’apparence du graphique

Une fois le graphique créé, vous pouvez le styliser à votre guise. Modifions l'arrière-plan, le titre et le style du graphique.

```csharp
// Définir le style du graphique
chart.Style = 3;

// Définir la valeur de mise à l'échelle automatique sur true
chart.AutoScaling = true;

// Définir la couleur de premier plan sur blanc
chart.PlotArea.Area.ForegroundColor = Color.White;

//Définir les propriétés du titre du graphique
chart.Title.Text = "Sample Chart";

// Définir le type de graphique
chart.Type = ChartType.LineWithDataMarkers;
```

Ici, nous donnons au graphique un aspect épuré en définissant un arrière-plan blanc, une mise à l'échelle automatique et en lui donnant un titre significatif.

## Étape 5 : définir les séries et tracer les points de données

Maintenant que notre graphique est beau, nous devons définir la série de données qui sera tracée.

```csharp
// Définir les propriétés du titre de l'axe des catégories
chart.CategoryAxis.Title.Text = "Units";

// Définir deux séries pour le graphique
int s2_idx = chart.NSeries.Add("A2: A21", true);
int s3_idx = chart.NSeries.Add("A22: A41", true);
```

Ces séries correspondent aux plages de points de données que nous avons renseignées précédemment.

## Étape 6 : ajouter des couleurs et personnaliser les marqueurs de série

Rendons ce graphique encore plus attrayant en ajoutant des couleurs personnalisées à nos marqueurs de données.

```csharp
// Personnaliser la première série
chart.NSeries[s2_idx].Marker.Area.ForegroundColor = Color.Yellow;
chart.NSeries[s2_idx].Marker.Border.IsVisible = false;

// Personnaliser la deuxième série
chart.NSeries[s3_idx].Marker.Area.ForegroundColor = Color.Green;
chart.NSeries[s3_idx].Marker.Border.IsVisible = false;
```

En personnalisant les couleurs, vous rendez le graphique non seulement fonctionnel mais aussi visuellement attrayant !

## Étape 7 : définissez les valeurs X et Y pour chaque série

Enfin, attribuons les valeurs X et Y à chacune de nos séries.

```csharp
// Définir les valeurs X et Y de la première série
chart.NSeries[s2_idx].XValues = "A2: A21";
chart.NSeries[s2_idx].Values = "B2: B21";

// Définir les valeurs X et Y de la deuxième série
chart.NSeries[s3_idx].XValues = "A22: A41";
chart.NSeries[s3_idx].Values = "B22: B41";
```

Les valeurs sont basées sur les données que nous avons renseignées à l’étape 2.

## Étape 8 : Enregistrer le classeur

Maintenant que tout est configuré, enregistrons le classeur afin de pouvoir voir le graphique en action.

```csharp
// Enregistrer le classeur
workbook.Save(outputDir + @"LineWithDataMarkerChart.xlsx", Aspose.Cells.SaveFormat.Xlsx);
```

Et voilà ! Vous venez de créer un graphique linéaire avec des marqueurs de données à l'aide d'Aspose.Cells pour .NET.

## Conclusion

Créer des graphiques par programmation dans Excel peut sembler intimidant, mais avec Aspose.Cells pour .NET, c'est aussi simple que de suivre une recette étape par étape. De la configuration de votre classeur à la personnalisation de l'apparence du graphique, cette puissante bibliothèque gère tout. Que vous créiez des rapports, des tableaux de bord ou des visualisations de données, Aspose.Cells vous permet de le faire en un clin d'œil.

## FAQ

### Puis-je personnaliser davantage le graphique ?  
Absolument ! Aspose.Cells offre de nombreuses options de personnalisation, des polices aux grilles et bien plus encore.

### Ai-je besoin d'une licence pour utiliser Aspose.Cells ?  
 Oui, une licence est requise pour bénéficier de toutes les fonctionnalités. Vous pouvez obtenir une[permis temporaire](https://purchase.aspose.com/temporary-license/) ou commencer par un[essai gratuit](https://releases.aspose.com/).

### Comment puis-je ajouter plus de séries de données ?  
 Ajoutez simplement des séries supplémentaires à l'aide du`NSeries.Add` méthode, spécifiant les plages de cellules pour les nouvelles données.

### Puis-je exporter le graphique sous forme d'image ?  
 Oui, vous pouvez exporter des graphiques directement sous forme d'images à l'aide de l'`Chart.ToImage` méthode.

### Aspose.Cells prend-il en charge les graphiques 3D ?  
Oui, Aspose.Cells prend en charge une large gamme de types de graphiques, y compris les graphiques 3D.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
