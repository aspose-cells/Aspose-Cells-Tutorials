---
title: Ajouter un contrôle rectangulaire à une feuille de calcul dans Excel
linktitle: Ajouter un contrôle rectangulaire à une feuille de calcul dans Excel
second_title: API de traitement Excel Aspose.Cells .NET
description: Découvrez comment ajouter un contrôle rectangle à une feuille de calcul Excel à l'aide d'Aspose.Cells pour .NET avec un guide détaillé étape par étape.
weight: 25
url: /fr/net/excel-shapes-controls/add-rectangle-control-to-worksheet-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ajouter un contrôle rectangulaire à une feuille de calcul dans Excel

## Introduction
En ce qui concerne l'automatisation des tâches Excel, Aspose.Cells pour .NET est un outil puissant qui peut vous aider à atteindre divers objectifs, notamment l'ajout de formes telles que des rectangles à vos feuilles de calcul. Dans ce guide, nous découvrirons comment ajouter un contrôle de rectangle à une feuille de calcul Excel à l'aide d'Aspose.Cells pour .NET. À la fin, vous serez en mesure de créer, de personnaliser et d'enregistrer une feuille de calcul avec un contrôle de rectangle intégré.
Mais avant de plonger, parlons des prérequis.
## Prérequis
Pour suivre ce tutoriel, assurez-vous de disposer des prérequis suivants :
1.  Bibliothèque Aspose.Cells pour .NET : si vous ne l'avez pas déjà fait,[télécharger la bibliothèque](https://releases.aspose.com/cells/net/) ou installez-le à l’aide de NuGet dans Visual Studio.
2. .NET Framework : vous devez avoir l’environnement de développement .NET configuré sur votre machine.
3. Connaissances de base de C# : bien que nous vous guiderons étape par étape, une connaissance de base de C# et de la programmation orientée objet est bénéfique.
4.  Licence : L'utilisation d'Aspose.Cells en mode d'évaluation fonctionne bien pour les tâches de base, mais pour une fonctionnalité complète, envisagez d'obtenir un[permis temporaire](https://purchase.aspose.com/temporary-license/)ou en acheter un chez[ici](https://purchase.aspose.com/buy).
Maintenant, plongeons dans le code !
## Paquets d'importation
Pour commencer à utiliser Aspose.Cells, assurez-vous d'avoir importé les espaces de noms nécessaires dans votre projet. Ces importations permettront d'accéder à diverses classes et méthodes dont vous avez besoin pour interagir avec les fichiers Excel.
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
Ces lignes garantissent que votre projet peut interagir avec les répertoires de fichiers (`System.IO`), classeurs Excel (`Aspose.Cells`), et dessin de forme (`Aspose.Cells.Drawing`).
Maintenant, décomposons le processus en étapes simples afin que vous puissiez facilement le suivre et le reproduire dans vos propres projets.
## Étape 1 : Configuration du chemin d’accès au répertoire
La première chose à faire est de définir le répertoire dans lequel votre fichier Excel sera enregistré. Cette étape permet de garantir que votre projet sait où créer et stocker le fichier de sortie.
### Définition du répertoire de données
```csharp
// Le chemin vers le répertoire des documents.
string dataDir = "Your Document Directory";
```
 Ici, vous spécifiez le chemin du répertoire où le fichier Excel sera stocké. Vous pouvez remplacer`"Your Document Directory"` avec le chemin réel sur votre machine, ou créez dynamiquement un dossier s'il n'existe pas.
### Vérification et création du répertoire
```csharp
// Créez un répertoire s'il n'est pas déjà présent.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Ce bloc vérifie si le répertoire existe. Si ce n'est pas le cas, il en crée un. C'est comme si vous prépariez votre classeur avant de stocker des documents.
## Étape 2 : Instanciation d'un nouveau classeur
 Dans cette étape, vous créez un nouveau classeur Excel à l'aide de`Aspose.Cells.Workbook` classe. Cela servira de conteneur pour votre feuille de travail et vos formes.
```csharp
// Instancier un nouveau classeur.
Workbook excelbook = new Workbook();
```
 En appelant le`Workbook` constructeur, vous disposez désormais d'un classeur Excel vierge prêt à être personnalisé.
## Étape 3 : Ajout d'un contrôle rectangulaire
C'est ici que la magie opère. Vous allez ajouter une forme rectangulaire à la première feuille de calcul de votre classeur.
```csharp
// Ajoutez un contrôle rectangle.
Aspose.Cells.Drawing.RectangleShape rectangle = excelbook.Worksheets[0].Shapes.AddRectangle(3, 0, 2, 0, 70, 130);
```
Décomposons cela :
- `excelbook.Worksheets[0]`:Cela permet d’accéder à la première feuille de calcul de votre classeur.
- `.Shapes.AddRectangle(3, 0, 2, 0, 70, 130)`: Cela ajoute une forme rectangulaire à la feuille de calcul. Les paramètres ici définissent la position (ligne et colonne), ainsi que la largeur et la hauteur du rectangle.
## Étape 4 : Personnalisation du rectangle
Il ne suffit pas d'ajouter un rectangle : vous devez le personnaliser. Dans cette étape, nous allons définir l'emplacement, l'épaisseur de ligne et le style de tiret du rectangle.
### Définition du placement
```csharp
// Définissez l'emplacement du rectangle.
rectangle.Placement = PlacementType.FreeFloating;
```
Cela spécifie que le rectangle est flottant, ce qui signifie qu'il ne sera pas lié par les dimensions de la cellule.
### Réglage de l'épaisseur de la ligne
```csharp
// Définissez l'épaisseur de la ligne.
rectangle.Line.Weight = 4;
```
Ici, nous définissons l'épaisseur de la ligne du rectangle à 4 points. Plus le nombre est élevé, plus la ligne est épaisse.
### Définition du style du tableau de bord
```csharp
// Définissez le style de tiret du rectangle.
rectangle.Line.DashStyle = MsoLineDashStyle.Solid;
```
 Cette ligne définit le style de tiret de la bordure du rectangle sur solide. Vous pouvez expérimenter différents styles comme`Dash` ou`Dot` selon vos besoins.
## Étape 5 : Enregistrer le classeur
Une fois le rectangle ajouté et personnalisé, l’étape finale consiste à enregistrer le classeur dans le répertoire spécifié.
```csharp
// Enregistrez le fichier Excel.
excelbook.Save(dataDir + "book1.out.xls");
```
 Cela enregistre le classeur en tant que`.xls` fichier dans le dossier que vous avez défini précédemment. Vous pouvez modifier le format du fichier en changeant l'extension, par exemple`.xlsx` si vous préférez le nouveau format Excel.
## Conclusion
Et voilà ! L'ajout d'un contrôle rectangle à une feuille de calcul Excel à l'aide d'Aspose.Cells pour .NET est un processus simple une fois que vous l'avez décomposé étape par étape. Que vous ayez besoin d'ajouter des formes pour un attrait visuel, de mettre en évidence des sections de vos données ou de personnaliser vos rapports, Aspose.Cells vous offre la flexibilité de le faire par programmation.
Ce guide devrait vous avoir fourni toutes les connaissances dont vous avez besoin pour commencer à ajouter des formes telles que des rectangles à vos feuilles Excel avec Aspose.Cells. Il est maintenant temps d'expérimenter et de voir ce que vous pouvez réaliser d'autre avec cette puissante bibliothèque !
## FAQ
### Puis-je ajouter d’autres formes comme des cercles ou des lignes à l’aide d’Aspose.Cells pour .NET ?  
Oui, Aspose.Cells vous permet d'ajouter une variété de formes, notamment des cercles, des lignes, des flèches, etc.
### Quelles autres propriétés puis-je définir pour le contrôle rectangle ?  
Vous pouvez personnaliser la couleur de remplissage, la couleur de ligne, la transparence et même ajouter du texte dans le rectangle.
### Aspose.Cells est-il compatible avec .NET Core ?  
Oui, Aspose.Cells prend en charge .NET Core, ainsi que .NET Framework et d'autres plates-formes basées sur .NET.
### Puis-je positionner le rectangle par rapport à une cellule spécifique ?  
 Oui, vous pouvez placer le rectangle dans des lignes et des colonnes spécifiques, ou utiliser le`PlacementType` pour contrôler la manière dont il est ancré.
### Existe-t-il un essai gratuit disponible pour Aspose.Cells ?  
 Oui, vous pouvez obtenir un[essai gratuit](https://releases.aspose.com/) depuis le site pour tester les fonctionnalités de la bibliothèque avant d'acheter.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
