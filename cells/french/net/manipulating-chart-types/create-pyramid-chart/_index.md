---
title: Créer un graphique pyramidal
linktitle: Créer un graphique pyramidal
second_title: API de traitement Excel Aspose.Cells .NET
description: Découvrez comment créer facilement un graphique pyramidal dans Excel à l'aide d'Aspose.Cells pour .NET grâce à ce guide étape par étape. Idéal pour la visualisation des données.
weight: 13
url: /fr/net/manipulating-chart-types/create-pyramid-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un graphique pyramidal

## Introduction

La création de représentations visuelles de données est essentielle dans de nombreux domaines, de l'analyse de données aux présentations commerciales. Parmi les différents types de graphiques, un graphique pyramidal se distingue par sa capacité unique à transmettre des relations hiérarchiques et des comparaisons proportionnelles. Ce didacticiel vous guidera dans la création d'un graphique pyramidal à l'aide d'Aspose.Cells pour .NET. Que vous soyez un développeur chevronné ou que vous débutiez avec .NET, ce guide simplifie le processus, vous permettant de maîtriser chaque étape tout en utilisant cette bibliothèque robuste.

## Prérequis

Avant de plonger dans le monde passionnant des graphiques pyramidaux, définissons quelques conditions préalables essentielles pour garantir une expérience de navigation fluide.

### Connaissances de base de C# et .NET
Vous devez avoir une compréhension fondamentale du développement C# et .NET. Une connaissance de l'environnement Visual Studio serait également bénéfique.

### Bibliothèque Aspose.Cells pour .NET
 Assurez-vous que la bibliothèque Aspose.Cells est installée. Vous pouvez la télécharger directement depuis le[Page de publication d'Aspose.Cells pour .NET](https://releases.aspose.com/cells/net/)Suivez les instructions d’installation ou utilisez le gestionnaire de packages NuGet pour l’intégrer facilement à votre projet.

### Visual Studio
Une installation fonctionnelle de Visual Studio est recommandée pour coder notre exemple de programme. 

### Licence (facultatif)
 Bien que vous puissiez expérimenter avec l'essai gratuit disponible via le[Lien d'essai gratuit](https://releases.aspose.com/) , pour une utilisation en production, pensez à visiter le[Lien d'achat](https://purchase.aspose.com/buy) ou optez pour une licence temporaire auprès du[Lien vers la licence temporaire](https://purchase.aspose.com/temporary-license/).

Maintenant que tout est prêt, mettons les mains à la pâte !

## Paquets d'importation

Avant de commencer à coder, importons les espaces de noms nécessaires. Cette étape est essentielle car elle nous permet d'utiliser les classes et les méthodes fournies par la bibliothèque Aspose.Cells.

```csharp
using System;
using System.IO;

using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
using Aspose.Cells.Charts;
```

Ces espaces de noms couvrent les fonctionnalités principales que nous utiliserons dans ce didacticiel, telles que la création de classeurs, la manipulation de feuilles de calcul et l'ajout de graphiques.

Très bien, décomposons le processus de création d'un graphique pyramidal en étapes simples. À la fin de ce guide, vous disposerez d'un exemple fonctionnel complet.

## Étape 1 : définir le répertoire de sortie

Tout d'abord, nous devons définir où notre fichier de sortie (le fichier Excel avec le graphique pyramidal) sera enregistré. C'est comme choisir un espace de travail avant de démarrer un projet.

```csharp
// Répertoire de sortie
string outputDir = "Your Output Directory";
```

 Assurez-vous de remplacer`"Your Output Directory"` avec un chemin valide sur votre ordinateur. C'est dans ce chemin que votre fichier Excel généré sera enregistré.

## Étape 2 : instancier un objet classeur

Ensuite, créons une nouvelle instance d'un classeur. Considérez un classeur comme une toile vierge sur laquelle vous pouvez peindre vos données.

```csharp
// Instanciation d'un objet Workbook
Workbook workbook = new Workbook();
```

Cette ligne initialise un nouveau classeur, prêt pour la saisie et la visualisation des données.

## Étape 3 : Obtenir une référence à la feuille de travail

Chaque classeur contient au moins une feuille de calcul. Nous allons ici faire référence à la première feuille de calcul avec laquelle travailler.

```csharp
// Obtention de la référence de la feuille de calcul nouvellement ajoutée en passant son index de feuille
Worksheet worksheet = workbook.Worksheets[0];
```

 En référençant`Worksheets[0]`, nous interagissons directement avec la première feuille, où nous ajouterons nos données et notre graphique.

## Étape 4 : ajouter des exemples de données aux cellules

Pour créer un graphique, vous aurez besoin de données. Remplissez quelques exemples de valeurs dans notre feuille de calcul.

```csharp
// Ajout de valeurs d'échantillon aux cellules
worksheet.Cells["A1"].PutValue(50);
worksheet.Cells["A2"].PutValue(100);
worksheet.Cells["A3"].PutValue(150);
worksheet.Cells["B1"].PutValue(4);
worksheet.Cells["B2"].PutValue(20);
worksheet.Cells["B3"].PutValue(50);
```

Ici, nous insérons des valeurs dans les cellules A1 à A3 (les étiquettes ou niveaux de la pyramide) et B1 à B3 (les valeurs correspondant à ces niveaux).

## Étape 5 : ajouter un diagramme pyramidal à la feuille de calcul

Ajoutons maintenant notre graphique pyramidal. C'est là que la magie opère !

```csharp
// Ajout d'un graphique à la feuille de calcul
int chartIndex = worksheet.Charts.Add(Aspose.Cells.Charts.ChartType.Pyramid, 5, 0, 25, 10);
```

 Dans cette ligne, nous spécifions le type de graphique comme`Pyramid` et définissez sa position dans la feuille de calcul à l'aide des index de ligne et de colonne. C'est un peu comme encadrer un tableau sur votre mur : vous devez choisir l'endroit où il sera le plus beau !

## Étape 6 : Accéder au graphique nouvellement ajouté

Après avoir ajouté le graphique, nous devons y accéder pour le configurer.

```csharp
// Accéder à l'instance du graphique nouvellement ajouté
Aspose.Cells.Charts.Chart chart = worksheet.Charts[chartIndex];
```

Cette ligne garantit que nous travaillons avec la bonne instance de graphique que nous venons de créer.

## Étape 7 : Ajouter une série de données au graphique

Pour que le graphique affiche des données, nous devons définir sa source de données en fonction des cellules que nous avons remplies précédemment.

```csharp
// Ajout de SeriesCollection (source de données du graphique) au graphique allant de la cellule « A1 » à « B3 »
chart.NSeries.Add("A1:B3", true);
```

Dans cette partie, nous relions les données des cellules A1 à B3, permettant à notre graphique pyramidal de visualiser ces informations.

## Étape 8 : Enregistrez le fichier Excel

Enfin, il est temps de sauvegarder notre chef-d'œuvre. Écrivons le classeur Excel dans un fichier.

```csharp
// Sauvegarde du fichier Excel
workbook.Save(outputDir + "outputHowToCreatePyramidChart.xlsx");
```

 Cette action créera un fichier Excel nommé`outputHowToCreatePyramidChart.xlsx` dans votre répertoire de sortie spécifié.

## Étape 9 : Confirmation de la console

Enfin et surtout, ajoutons quelques commentaires dans la console pour confirmer que tout s'est bien déroulé.

```csharp
Console.WriteLine("HowToCreatePyramidChart executed successfully.");
```

Cette ligne vous avertira que votre tâche de création de graphique pyramidal a été réalisée sans aucun problème.

## Conclusion

Créer un graphique pyramidal dans un fichier Excel n'a jamais été aussi simple avec Aspose.Cells pour .NET. En suivant ces étapes simples, vous pouvez transformer vos données brutes en un récit visuel attrayant qui capte l'attention et communique efficacement les relations. Maintenant que vous êtes armé de ces connaissances, vous pouvez explorer des fonctionnalités plus complexes d'Aspose.Cells, telles que le style avancé et les différents types de graphiques, pour améliorer encore vos rapports.

## FAQ

### Qu'est-ce qu'Aspose.Cells ?
Aspose.Cells est une API puissante pour manipuler des fichiers et des graphiques Excel dans des applications .NET, permettant aux développeurs de créer, modifier et convertir facilement des documents Excel.

### Puis-je utiliser Aspose.Cells gratuitement ?
Oui, Aspose.Cells propose un essai gratuit vous permettant d'explorer ses fonctionnalités. Cependant, pour une utilisation continue, pensez à acheter une licence.

### Quels types de graphiques puis-je créer avec Aspose.Cells ?
Vous pouvez créer différents types de graphiques, notamment des graphiques à barres, à courbes, à secteurs, à aires et en pyramide, pour n'en citer que quelques-uns.

### Dois-je installer autre chose que la bibliothèque Aspose.Cells ?
Assurez-vous que des outils de développement .NET tels que Visual Studio sont configurés sur votre ordinateur pour fonctionner de manière transparente avec Aspose.Cells.

### Comment puis-je obtenir de l'aide pour Aspose.Cells ?
 Pour obtenir de l'aide, vous pouvez visiter le[Forum d'assistance Aspose.Cells](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
