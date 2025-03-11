---
title: Ajouter un contrôle d'arc avec des points de connexion
linktitle: Ajouter un contrôle d'arc avec des points de connexion
second_title: API de traitement Excel Aspose.Cells .NET
description: Découvrez comment ajouter des contrôles d'arc avec des points de connexion à l'aide d'Aspose.Cells pour .NET dans ce guide détaillé.
weight: 27
url: /fr/net/excel-shapes-controls/add-arc-control-with-connection-points/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ajouter un contrôle d'arc avec des points de connexion

## Introduction
Lorsqu'il s'agit de créer des rapports Excel visuellement attrayants, les illustrations jouent un rôle essentiel. Que vous rédigiez un rapport financier ou une analyse de projet, l'utilisation de formes telles que des arcs peut ajouter de la profondeur et de la clarté à votre présentation de données. Aujourd'hui, nous allons découvrir comment utiliser Aspose.Cells pour .NET pour ajouter des contrôles d'arc avec des points de connexion dans vos feuilles de calcul Excel. Alors, si vous vous êtes déjà demandé comment pimenter vos feuilles de calcul ou faire chanter vos données, lisez la suite !
## Prérequis
Avant de nous plonger dans l'excitation du codage, assurons-nous que tout est prêt. Voici ce dont vous avez besoin :
1. .NET Framework : assurez-vous d'avoir installé une version compatible. Aspose.Cells fonctionne avec plusieurs versions, y compris .NET Core.
2.  Aspose.Cells pour .NET : vous devrez télécharger et installer la bibliothèque Aspose.Cells. Vous pouvez facilement la récupérer à partir du[lien de téléchargement](https://releases.aspose.com/cells/net/).
3. Un bon IDE : Visual Studio, ce fidèle compagnon de tout développeur .NET, vous aidera à rationaliser votre expérience de codage.
4. Connaissances de base de C# : si vous connaissez bien C#, vous trouverez ce tutoriel fluide.
5. Accédez à votre répertoire de documents : sachez où vous allez enregistrer vos fichiers Excel. C'est essentiel pour organiser efficacement vos résultats.
## Paquets d'importation
L'étape suivante consiste à vérifier que vous avez importé les bons packages dans votre projet. Aspose.Cells pour .NET possède diverses fonctionnalités, nous allons donc faire simple. Voici ce que vous devrez inclure :
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
Ces espaces de noms vous donneront accès à toutes les fonctionnalités de dessin et de gestion des cellules que vous utiliserez tout au long de ce guide.
## Étape 1 : Configurez votre répertoire de documents
Commençons par le commencement : créons un répertoire dans lequel vous enregistrerez ces nouveaux fichiers Excel. Voici comment procéder :
```csharp
string dataDir = "Your Document Directory";
// Créez un répertoire s'il n'est pas déjà présent.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Ce morceau de code vérifie si le dossier spécifié existe. Si ce n'est pas le cas, il en crée un. Simple, non ? Il est toujours bon d'avoir un emplacement spécifique pour vos fichiers afin d'éviter l'encombrement.
## Étape 2 : créer une instance d'un classeur
Maintenant que notre répertoire est prêt, créons un nouveau classeur Excel.
```csharp
Workbook excelbook = new Workbook();
```
 En appelant le`Workbook` constructeur, vous dites essentiellement : « Hé, commençons un nouveau fichier Excel ! » Ce sera le canevas pour toutes vos formes et données.
## Étape 3 : Ajout de la première forme d'arc
C'est ici que le plaisir commence ! Ajoutons notre première forme d'arc.
```csharp
Aspose.Cells.Drawing.ArcShape arc1 = excelbook.Worksheets[0].Shapes.AddArc(2, 0, 2, 0, 130, 130);
```
Cette ligne de code ajoute une forme d'arc à la première feuille de calcul. Les paramètres spécifient les coordonnées de l'arc et les angles qui définissent sa courbure. 
## Étape 4 : Personnaliser l'apparence de l'Arc
Une forme d’arc vierge est comme une toile sans peinture : elle a besoin d’un peu d’originalité !
### Définir la couleur de remplissage de l'arc
```csharp
arc1.Fill.FillType = FillType.Solid;
arc1.Fill.SolidFill.Color = Color.Blue;
```
Cela rend l'arc bleu uni. Vous pouvez changer la couleur en n'importe quelle teinte que vous souhaitez en échangeant`Color.Blue` pour une autre couleur.
### Définir le placement de l'arc
```csharp
arc1.Placement = PlacementType.FreeFloating;
```
Le réglage du placement sur « FreeFloating » permet à l'arc de se déplacer indépendamment des limites des cellules, vous offrant ainsi une flexibilité de positionnement.
### Ajuster l'épaisseur et le style de la ligne
```csharp
arc1.Line.Weight = 1;      
arc1.Line.DashStyle = MsoLineDashStyle.Solid;
```
Ici, vous définissez le poids et le style de la ligne, la rendant plus proéminente et visuellement attrayante.
## Étape 5 : Ajout d'une autre forme d'arc
Pourquoi s'arrêter à une seule forme ? Ajoutons une autre forme d'arc pour enrichir notre visuel Excel.
```csharp
Aspose.Cells.Drawing.ArcShape arc2 = excelbook.Worksheets[0].Shapes.AddArc(9, 0, 2, 0, 130, 130);
```
Comme le premier arc, celui-ci est ajouté à une position différente : c'est là que la magie du design a lieu !
## Étape 6 : Personnaliser le deuxième arc
Donnons aussi un peu de personnalité à notre deuxième arc !
### Changer la couleur de la ligne d'arc
```csharp
arc2.Line.FillType = FillType.Solid;
arc2.Line.SolidFill.Color = Color.Blue;
```
Nous gardons une couleur bleue cohérente, mais vous pouvez toujours mélanger et assortir pour voir ce qui convient le mieux à votre conception !
### Définir des propriétés similaires au premier arc
Assurez-vous de reproduire ces choix esthétiques :
```csharp
arc2.Placement = PlacementType.FreeFloating;
arc2.Line.Weight = 1;           
arc2.Line.DashStyle = MsoLineDashStyle.Solid;
```
Ici, vous vous assurez simplement que le deuxième arc correspond au premier, créant ainsi un aspect cohérent dans toute votre feuille de calcul.
## Étape 7 : Enregistrez votre classeur
Aucun chef-d'œuvre n'est complet sans être sauvegardé, n'est-ce pas ? Il est temps d'écrire vos arcs dans un fichier Excel.
```csharp
excelbook.Save(dataDir + "book1.out.xls");
```
Cette ligne enregistre vos arcs nouvellement créés dans un fichier Excel nommé « book1.out.xls » dans votre répertoire désigné.
## Conclusion
Félicitations ! Vous venez de maîtriser les bases de l'ajout de contrôles d'arc avec des points de connexion dans vos feuilles Excel à l'aide d'Aspose.Cells pour .NET. Cette fonctionnalité embellit non seulement vos feuilles de calcul, mais peut également faciliter la digestion des données complexes. Que vous soyez un développeur chevronné ou que vous débutiez, ces éléments visuels peuvent transformer vos rapports de fades en rapports grandioses.
## FAQ
### Qu'est-ce qu'Aspose.Cells ?
Aspose.Cells est une puissante bibliothèque .NET qui permet aux développeurs de créer et de manipuler des fichiers Excel par programmation.
### Puis-je utiliser Aspose.Cells gratuitement ?
 Oui ! Vous pouvez faire un essai gratuit. Visitez[ce lien](https://releases.aspose.com/) pour commencer.
### Comment ajouter d’autres formes en plus des arcs ?
Vous pouvez utiliser différentes classes disponibles dans l'espace de noms Aspose.Cells.Drawing pour ajouter diverses formes telles que des rectangles, des cercles, etc.
### Quels types de fichiers puis-je créer avec Aspose.Cells ?
Vous pouvez créer et manipuler divers formats Excel, notamment XLS, XLSX, CSV, etc.
### Un support technique est-il disponible pour Aspose.Cells ?
 Absolument ! Vous pouvez accéder à la[Forum d'assistance Aspose](https://forum.aspose.com/c/cells/9) pour obtenir de l'aide.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
