---
"description": "Apprenez à ajouter facilement des images à vos graphiques Excel avec Aspose.Cells pour .NET. Améliorez vos graphiques et présentations en quelques étapes simples."
"linktitle": "Ajouter une image au graphique"
"second_title": "API de traitement Excel Aspose.Cells .NET"
"title": "Ajouter une image au graphique"
"url": "/fr/net/inserting-controls-in-charts/add-picture-to-chart/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Ajouter une image au graphique

## Introduction

Vous en avez assez des graphiques ennuyeux et sans touche personnelle ? Vous souhaitez apprendre à dynamiser vos visuels Excel en ajoutant des images ? Ça tombe bien ! Dans ce tutoriel, nous allons plonger dans l'univers d'Aspose.Cells pour .NET et apprendre à ajouter des images aux graphiques dans Excel. Alors, prenez votre café préféré et c'est parti !

## Prérequis

Avant de passer aux choses sérieuses du codage, il y a quelques prérequis que vous devez avoir pour suivre en douceur :

- Visual Studio : c'est ici que vous écrirez et exécuterez votre code .NET. Assurez-vous qu'il est installé.
- Aspose.Cells pour .NET : vous aurez besoin de cette bibliothèque pour travailler avec des fichiers Excel. Vous pouvez [téléchargez-le ici](https://releases.aspose.com/cells/net/).
- Compréhension de base de C# : même si je vous guiderai à travers le code, avoir une bonne compréhension des bases de C# rendra les choses plus claires.

### Étapes d'installation

1. Installer Aspose.Cells : Vous pouvez ajouter Aspose.Cells à votre projet Visual Studio via le Gestionnaire de packages NuGet. Pour ce faire, accédez à Outils > Gestionnaire de packages NuGet > Gérer les packages NuGet pour la solution et recherchez « Aspose.Cells ». Cliquez sur « Installer ».
2. Configuration de votre projet : créez un nouveau projet d’application console C# dans Visual Studio.

## Importer des packages

Une fois tout configuré, l'étape suivante consiste à importer les packages nécessaires dans votre projet. Voici comment procéder :

### Importer les espaces de noms requis

En haut de votre fichier de code C#, vous devrez importer les espaces de noms suivants :

```csharp
using Aspose.Cells;
using Aspose.Cells.Charts;
using Aspose.Cells.Drawing;
using System.IO;
```

Cela indique à votre programme : « Hé ! Je vais utiliser ces fonctionnalités intéressantes d'Aspose.Cells. »

Maintenant que nous avons mis en place nos prérequis, décomposons le processus en étapes de la taille d'une bouchée. 

## Étape 1 : Définissez vos répertoires

Tout d'abord, nous devons définir les chemins d'accès à nos fichiers d'entrée et de sortie. Cette étape est cruciale car nous devons savoir où trouver notre fichier Excel existant et où enregistrer le fichier modifié.

```csharp
//Répertoire source
string sourceDir = "Your Document Directory/";

//Répertoire de sortie
string outputDir = "Your Output Directory/";
```

Remplacer `Your Document Directory` et `Your Output Directory` avec les chemins réels sur votre ordinateur. 

## Étape 2 : Charger le classeur existant

Maintenant, chargeons le fichier Excel existant dans lequel nous voulons ajouter notre image au graphique.

```csharp
// Ouvrez le fichier existant.
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

## Étape 4 : Cibler le graphique

Maintenant, précisons le graphique auquel nous allons ajouter notre image. Dans cet exemple, nous ciblerons le premier graphique de la première feuille de calcul.

```csharp
// Obtenez le tableau du concepteur dans la deuxième feuille.
Worksheet sheet = workbook.Worksheets[0];
Aspose.Cells.Charts.Chart chart = sheet.Charts[0];
```

Vous pouvez accéder à n’importe quelle feuille de calcul en modifiant l’index en conséquence.

## Étape 5 : Ajouter l’image au graphique

Une fois le graphique sélectionné, il est temps d'ajouter l'image ! 

```csharp
// Ajoutez une nouvelle image au graphique.
Aspose.Cells.Drawing.Picture pic0 = chart.Shapes.AddPictureInChart(50, 50, stream, 200, 200);
```

Ici, `50` et `50` sont les coordonnées X et Y où l'image sera placée, et `200` est la largeur et la hauteur de l'image.

## Étape 6 : Personnaliser le format de ligne de l'image

Envie d'ajouter une touche d'originalité à votre photo ? Personnalisez sa bordure ! Voici comment procéder :

```csharp
// Obtenez le type de format de ligne de l'image.
Aspose.Cells.Drawing.LineFormat lineformat = pic0.Line; 

// Définissez le style du tableau de bord.
lineformat.DashStyle = MsoLineDashStyle.Solid;

// Définissez l'épaisseur de la ligne.
lineformat.Weight = 4;    
```

Cet extrait vous permet de choisir l'apparence et l'épaisseur de la bordure. Choisissez le style qui correspond à votre présentation !

## Étape 7 : Enregistrer le classeur modifié

Après tout ce travail acharné, sauvegardons vos modifications en exécutant la ligne de code suivante :

```csharp
// Enregistrez le fichier Excel.
workbook.Save(outputDir + "outputAddingPictureInChart.xls");
```

Votre image est maintenant intégrée avec succès dans le graphique et votre fichier de sortie est prêt à être visualisé !

## Étape 8 : Indiquer le succès

Enfin, vous pouvez ajouter un message simple pour confirmer que votre opération a réussi :

```csharp
Console.WriteLine("AddingPictureInChart executed successfully.");
```

## Conclusion

Dans ce tutoriel, nous avons découvert comment personnaliser vos graphiques Excel en ajoutant des images grâce à Aspose.Cells pour .NET. En quelques étapes simples, vous pouvez transformer vos présentations banales en présentations mémorables. Alors, n'attendez plus ! Lancez-vous et sublimez vos graphiques !

## FAQ

### Puis-je ajouter plusieurs images à un seul graphique ?
Oui ! Vous pouvez appeler le `AddPictureInChart` méthode plusieurs fois pour ajouter autant d'images que vous le souhaitez.

### Quels formats d'image Aspose.Cells prend-il en charge ?
Aspose.Cells prend en charge une variété de formats d'image, notamment PNG, JPEG, BMP et GIF.

### Puis-je personnaliser la position de l'image ?
Certainement ! Les coordonnées X et Y dans le `AddPictureInChart` méthode permettant un positionnement précis.

### Aspose.Cells est-il gratuit à utiliser ?
Aspose.Cells propose un essai gratuit, mais une licence est requise pour accéder à toutes les fonctionnalités. Consultez les tarifs. [ici](https://purchase.aspose.com/buy).

### Où puis-je trouver plus d’exemples ?
Découvrez le [Documentation d'Aspose.Cells](https://reference.aspose.com/cells/net/) pour des exemples et des fonctionnalités plus détaillés.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}