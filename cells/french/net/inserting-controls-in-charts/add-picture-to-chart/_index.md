---
title: Ajouter une image au graphique
linktitle: Ajouter une image au graphique
second_title: API de traitement Excel Aspose.Cells .NET
description: Découvrez comment ajouter facilement des images aux graphiques Excel à l'aide d'Aspose.Cells pour .NET. Améliorez vos graphiques et vos présentations en quelques étapes simples.
weight: 11
url: /fr/net/inserting-controls-in-charts/add-picture-to-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ajouter une image au graphique

## Introduction

Vous en avez assez des graphiques ennuyeux qui manquent de touche personnelle ? Vous voulez apprendre à pimenter vos visuels Excel en ajoutant des images ? Eh bien, vous avez de la chance ! Dans ce tutoriel, nous allons plonger dans le monde d'Aspose.Cells pour .NET et apprendre à ajouter des images aux graphiques dans Excel. Alors, prenez votre tasse de café préférée et commençons !

## Prérequis

Avant de passer aux choses sérieuses du codage, vous devez respecter quelques conditions préalables pour pouvoir suivre le processus en douceur :

- Visual Studio : c'est ici que vous écrirez et exécuterez votre code .NET. Assurez-vous qu'il est installé.
-  Aspose.Cells pour .NET : vous aurez besoin de cette bibliothèque pour travailler avec des fichiers Excel. Vous pouvez[téléchargez-le ici](https://releases.aspose.com/cells/net/).
- Compréhension de base de C# : même si je vous guiderai à travers le code, avoir une idée des bases de C# rendra les choses plus claires.

### Étapes d'installation

1. Installer Aspose.Cells : vous pouvez ajouter Aspose.Cells à votre projet Visual Studio via le gestionnaire de packages NuGet. Pour ce faire, accédez à Outils > Gestionnaire de packages NuGet > Gérer les packages NuGet pour la solution et recherchez « Aspose.Cells ». Cliquez sur Installer.
2. Configuration de votre projet : créez un nouveau projet d’application console C# dans Visual Studio.

## Paquets d'importation

Une fois que vous avez tout configuré, l'étape suivante consiste à importer les packages nécessaires dans votre projet. Voici comment procéder :

### Importer les espaces de noms requis

En haut de votre fichier de code C#, vous devrez importer les espaces de noms suivants :

```csharp
using Aspose.Cells;
using Aspose.Cells.Charts;
using Aspose.Cells.Drawing;
using System.IO;
```

Cela indique à votre programme : « Hé ! Je vais utiliser ces fonctionnalités intéressantes d'Aspose.Cells. »

Maintenant que nos prérequis sont en place, décomposons le processus en étapes de la taille d'une bouchée. 

## Étape 1 : Définissez vos répertoires

Tout d’abord, nous devons définir les chemins d’accès à nos fichiers d’entrée et de sortie. Cette étape est cruciale car nous devons savoir où trouver notre fichier Excel existant et où enregistrer le fichier modifié.

```csharp
//Répertoire des sources
string sourceDir = "Your Document Directory/";

//Répertoire de sortie
string outputDir = "Your Output Directory/";
```

 Remplacer`Your Document Directory` et`Your Output Directory` avec les chemins réels sur votre ordinateur. 

## Étape 2 : charger le classeur existant

Maintenant, chargeons le fichier Excel existant dans lequel nous souhaitons ajouter notre image au graphique.

```csharp
// Ouvrir le fichier existant.
Workbook workbook = new Workbook(sourceDir + "sampleAddingPictureInChart.xls");
```

Ce code ouvre le classeur, le rendant prêt à être modifié.

## Étape 3 : préparer le flux d’images

Avant d’ajouter l’image, nous devons lire l’image que nous voulons insérer dans le graphique. 

```csharp
// Obtenez un fichier image dans le flux.
FileStream stream = new FileStream(sourceDir + "sampleAddingPictureInChart.png", FileMode.Open, FileAccess.Read);
```

Assurez-vous que l'image est enregistrée dans le répertoire spécifié.

## Étape 4 : Cibler le graphique

Maintenant, précisons à quel graphique nous allons ajouter notre image. Dans cet exemple, nous ciblerons le premier graphique de la première feuille de calcul.

```csharp
// Obtenez le tableau du concepteur dans la deuxième feuille.
Worksheet sheet = workbook.Worksheets[0];
Aspose.Cells.Charts.Chart chart = sheet.Charts[0];
```

Vous pouvez accéder à n’importe quelle feuille de calcul en modifiant l’index en conséquence.

## Étape 5 : Ajoutez l'image au graphique

Une fois le graphique sélectionné, il est temps d’ajouter l’image ! 

```csharp
// Ajoutez une nouvelle image au graphique.
Aspose.Cells.Drawing.Picture pic0 = chart.Shapes.AddPictureInChart(50, 50, stream, 200, 200);
```

 Ici,`50` et`50` sont les coordonnées X et Y où l'image sera placée, et`200` est la largeur et la hauteur de l'image.

## Étape 6 : Personnaliser le format de ligne de l'image

Vous souhaitez ajouter une touche d'originalité à votre image ? Vous pouvez personnaliser sa bordure ! Voici comment procéder :

```csharp
// Obtenir le type de format de ligne de l'image.
Aspose.Cells.Drawing.LineFormat lineformat = pic0.Line; 

// Définissez le style du tiret.
lineformat.DashStyle = MsoLineDashStyle.Solid;

// Définissez l'épaisseur de la ligne.
lineformat.Weight = 4;    
```

Cet extrait vous permet de choisir l'apparence et l'épaisseur de la bordure. Choisissez le style qui correspond à votre présentation !

## Étape 7 : Enregistrer le classeur modifié

Après tout ce travail acharné, sauvegardons vos modifications en exécutant la ligne de code suivante :

```csharp
// Enregistrez le fichier Excel.
workbook.Save(outputDir + "outputAddingPictureInChart.xls");
```

Votre image est maintenant intégrée avec succès dans le graphique et votre fichier de sortie est prêt à être visualisé !

## Étape 8 : Indiquer la réussite

Enfin, vous pouvez ajouter un message simple pour confirmer que votre opération a réussi :

```csharp
Console.WriteLine("AddingPictureInChart executed successfully.");
```

## Conclusion

Dans ce tutoriel, nous avons exploré comment ajouter un peu de personnalité à vos graphiques Excel en ajoutant des images à l'aide d'Aspose.Cells pour .NET. En quelques étapes simples, vous pouvez faire passer vos présentations de banales à mémorables. Alors, qu'attendez-vous ? Lancez-vous et laissez vos graphiques briller !

## FAQ

### Puis-je ajouter plusieurs images à un seul graphique ?
 Oui ! Vous pouvez appeler le`AddPictureInChart` Répétez la méthode plusieurs fois pour ajouter autant d'images que vous le souhaitez.

### Quels formats d’image sont pris en charge par Aspose.Cells ?
Aspose.Cells prend en charge une variété de formats d'image, notamment PNG, JPEG, BMP et GIF.

### Puis-je personnaliser la position de l'image ?
 Bien sûr ! Les coordonnées X et Y dans le`AddPictureInChart` méthode permet un positionnement précis.

### L'utilisation d'Aspose.Cells est-elle gratuite ?
Aspose.Cells propose un essai gratuit, mais pour bénéficier de toutes les fonctionnalités, une licence est requise. Vous pouvez trouver les tarifs[ici](https://purchase.aspose.com/buy).

### Où puis-je trouver plus d’exemples ?
 Découvrez le[Documentation d'Aspose.Cells](https://reference.aspose.com/cells/net/) pour des exemples et des fonctionnalités plus détaillés.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
