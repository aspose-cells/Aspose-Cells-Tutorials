---
title: Ajouter un arc à une feuille de calcul dans Excel
linktitle: Ajouter un arc à une feuille de calcul dans Excel
second_title: API de traitement Excel Aspose.Cells .NET
description: Apprenez à ajouter des arcs aux feuilles de calcul Excel à l'aide d'Aspose.Cells pour .NET. Suivez notre guide étape par étape pour améliorer la conception de vos feuilles de calcul.
weight: 16
url: /fr/net/excel-shapes-controls/add-arc-to-worksheet-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ajouter un arc à une feuille de calcul dans Excel

## Introduction
La création de feuilles de calcul Excel visuellement attrayantes est essentielle pour la présentation des données, et la bibliothèque Aspose.Cells fournit aux développeurs des outils robustes pour accomplir cette tâche. Une fonctionnalité intéressante que vous souhaiterez peut-être intégrer à vos documents Excel est la possibilité d'ajouter des formes, telles que des arcs. Dans ce didacticiel, nous vous expliquerons étape par étape comment ajouter des arcs à une feuille de calcul Excel à l'aide d'Aspose.Cells pour .NET. À la fin de cet article, vous apprendrez non seulement à ajouter des arcs, mais également à gérer les formes en général.
## Prérequis
Avant de nous plonger dans les subtilités de l'ajout d'arcs à votre feuille de calcul, il est essentiel de vous assurer que vous disposez de quelques éléments. Voici les prérequis dont vous aurez besoin pour commencer :
1. Visual Studio : vous devez avoir Visual Studio installé sur votre ordinateur car nous utiliserons C# comme langage de programmation.
2. .NET Framework : assurez-vous que .NET Framework ou .NET Core est installé. Aspose.Cells prend en charge les deux.
3. Aspose.Cells pour .NET : vous devez disposer de la bibliothèque Aspose.Cells. Vous pouvez la télécharger à partir du[Téléchargements d'Aspose.Cells](https://releases.aspose.com/cells/net/) page.
4. Compréhension de base de C# : la familiarité avec C# vous aidera à suivre les extraits de code sans trop de problèmes.
## Paquets d'importation
Pour commencer à travailler avec Aspose.Cells dans votre projet, vous devez importer les packages nécessaires. Voici comment procéder :
### Créer un nouveau projet
- Ouvrez Visual Studio.
- Choisissez « Créer un nouveau projet ».
- Sélectionnez un modèle qui fonctionne avec .NET (comme une application console).
  
### Ajouter des références Aspose.Cells
- Faites un clic droit sur votre projet dans l’Explorateur de solutions.
- Sélectionnez « Gérer les packages NuGet ».
- Recherchez « Aspose.Cells » et installez-le.
Vous êtes maintenant prêt à commencer à coder l'ajout d'arc.
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
Voici une analyse étape par étape du code qui montre comment ajouter des arcs à une feuille de calcul dans Excel.
## Étape 1 : Configuration du répertoire
La première étape consiste à configurer un répertoire dans lequel vous enregistrerez votre fichier Excel. Cela vous aidera à gérer facilement vos fichiers de sortie.
```csharp
string dataDir = "Your Document Directory";
// Créez un répertoire s'il n'est pas déjà présent.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Dans cet extrait de code, nous spécifions le chemin d'accès au répertoire du document. Nous vérifions également si le répertoire existe ; si ce n'est pas le cas, nous le créons. Cela pose les bases de notre sortie.
## Étape 2 : créer une instance d'un classeur
Ensuite, créons une nouvelle instance de classeur.
```csharp
// Instancier un nouveau classeur.
Workbook excelbook = new Workbook();
```
Cette ligne crée un nouveau classeur Excel. Considérez-le comme une toile vierge sur laquelle nous pouvons ajouter des formes, des données et bien plus encore.
## Étape 3 : ajouter la première forme d’arc
Maintenant, ajoutons notre première forme d’arc à la feuille de calcul.
```csharp
// Ajoutez une forme d’arc.
Aspose.Cells.Drawing.ArcShape arc1 = excelbook.Worksheets[0].Shapes.AddArc(2, 0, 2, 0, 130, 130);
```
 Ici, nous ajoutons un arc à la première feuille de calcul. Les paramètres définissent la position et la taille de l'arc :`(left, top, width, height, startAngle, endAngle)`C'est comme tracer un segment de cercle !
## Étape 4 : Personnaliser le premier arc
Après avoir ajouté l'arc, vous souhaiterez peut-être personnaliser son apparence.
```csharp
// Définir la couleur de la forme de remplissage
arc1.Fill.FillType = FillType.Solid;
arc1.Fill.SolidFill.Color = Color.Blue;
// Définissez le placement de l'arc.
arc1.Placement = PlacementType.FreeFloating;           
// Définissez l'épaisseur de la ligne.
arc1.Line.Weight = 1;      
// Définissez le style de tiret de l'arc.
arc1.Line.DashStyle = MsoLineDashStyle.Solid;
```
Dans cette section, nous personnalisons l'arc. Nous définissons son type de remplissage sur une couleur unie (bleu dans ce cas), définissons son placement, établissons l'épaisseur de la ligne et choisissons un style de tiret. En gros, nous habillons notre arc pour le rendre visuellement attrayant !
## Étape 5 : ajouter une deuxième forme d’arc
Ajoutons une autre forme d’arc pour fournir plus de contexte.
```csharp
// Ajoutez une autre forme d’arc.
Aspose.Cells.Drawing.ArcShape arc2 = excelbook.Worksheets[0].Shapes.AddArc(9, 0, 2, 0, 130, 130);
```
Similairement au premier arc, nous ajoutons un deuxième arc sur la même feuille de calcul. Les coordonnées ici sont légèrement décalées pour le positionner différemment.
## Étape 6 : Personnaliser le deuxième arc
Tout comme nous l'avons fait avec le premier arc, nous allons également personnaliser le deuxième.
```csharp
// Définir la couleur de la ligne
arc2.Line.FillType = FillType.Solid;
arc2.Line.SolidFill.Color = Color.Blue;
// Définissez le placement de l'arc.
arc2.Placement = PlacementType.FreeFloating;          
// Définissez l'épaisseur de la ligne.
arc2.Line.Weight = 1;           
// Définissez le style de tiret de l'arc.
arc2.Line.DashStyle = MsoLineDashStyle.Solid;
```
Ici, nous donnons au deuxième arc le même style que le premier. Vous pouvez modifier la couleur ou le style à votre guise pour des raisons d'originalité ou de thématique.
## Étape 7 : Enregistrer le classeur
Enfin, il est temps de sauvegarder votre classeur nouvellement créé avec les arcs.
```csharp
// Enregistrez le fichier Excel.
excelbook.Save(dataDir + "book1.out.xls");
```
Cette ligne fonctionne comme si vous appuyiez sur le bouton Enregistrer. Nous enregistrons notre travail à l'emplacement spécifié avec un nom de fichier désigné. Assurez-vous de vérifier votre répertoire pour voir votre chef-d'œuvre au format Excel !
## Conclusion
Dans ce didacticiel, nous avons exploré le processus d'ajout de formes d'arc à une feuille de calcul Excel à l'aide d'Aspose.Cells pour .NET. Grâce à un guide simple étape par étape, vous avez appris à créer un nouveau classeur, à ajouter des arcs, à personnaliser leur apparence et à enregistrer votre document. Cette fonctionnalité améliore non seulement l'attrait visuel de vos feuilles de calcul, mais rend également vos présentations de données plus informatives. Que vous créiez des graphiques, des rapports ou que vous fassiez simplement des expériences, l'utilisation de formes telles que des arcs peut ajouter une touche créative à vos projets.
## FAQ
### Qu'est-ce qu'Aspose.Cells ?
Aspose.Cells est une bibliothèque puissante qui permet aux développeurs de créer, manipuler et convertir des fichiers Excel par programmation sans avoir besoin de Microsoft Excel.
### Dois-je installer Microsoft Excel pour utiliser Aspose.Cells ?
Non, Aspose.Cells est totalement indépendant et ne nécessite pas l'installation de Microsoft Excel.
### Puis-je essayer Aspose.Cells gratuitement ?
 Oui, vous pouvez essayer Aspose.Cells en utilisant leur[Essai gratuit](https://releases.aspose.com/).
### Quels langages de programmation Aspose.Cells prend-il en charge ?
Aspose.Cells prend en charge plusieurs langages, notamment C#, VB.NET, etc.
### Où puis-je obtenir de l'aide pour Aspose.Cells ?
 Vous pouvez obtenir de l'aide via le[Forum Aspose](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
