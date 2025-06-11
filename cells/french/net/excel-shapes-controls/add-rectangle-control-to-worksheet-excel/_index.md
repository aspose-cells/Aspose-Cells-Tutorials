---
"description": "Découvrez comment ajouter un contrôle rectangle à une feuille de calcul Excel à l’aide d’Aspose.Cells pour .NET avec un guide détaillé étape par étape."
"linktitle": "Ajouter un contrôle rectangulaire à une feuille de calcul dans Excel"
"second_title": "API de traitement Excel Aspose.Cells .NET"
"title": "Ajouter un contrôle rectangulaire à une feuille de calcul dans Excel"
"url": "/fr/net/excel-shapes-controls/add-rectangle-control-to-worksheet-excel/"
"weight": 25
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Ajouter un contrôle rectangulaire à une feuille de calcul dans Excel

## Introduction
Pour automatiser vos tâches Excel, Aspose.Cells pour .NET est un outil puissant qui vous permet d'atteindre divers objectifs, notamment l'ajout de formes rectangulaires à vos feuilles de calcul. Dans ce guide, nous découvrirons comment ajouter un contrôle rectangle à une feuille de calcul Excel avec Aspose.Cells pour .NET. À la fin de ce guide, vous serez capable de créer, personnaliser et enregistrer une feuille de calcul intégrant un contrôle rectangle.
Mais avant de plonger, parlons des prérequis.
## Prérequis
Pour suivre ce tutoriel, assurez-vous de disposer des prérequis suivants :
1. Bibliothèque Aspose.Cells pour .NET : si vous ne l’avez pas déjà fait, [télécharger la bibliothèque](https://releases.aspose.com/cells/net/) ou installez-le à l'aide de NuGet dans Visual Studio.
2. .NET Framework : vous devez avoir l’environnement de développement .NET configuré sur votre machine.
3. Connaissances de base de C# : bien que nous vous guiderons étape par étape, une connaissance de base de C# et de la programmation orientée objet est bénéfique.
4. Licence : L'utilisation d'Aspose.Cells en mode d'évaluation fonctionne bien pour les tâches de base, mais pour une fonctionnalité complète, pensez à obtenir un [permis temporaire](https://purchase.aspose.com/temporary-license/) ou en acheter un auprès de [ici](https://purchase.aspose.com/buy).
Maintenant, plongeons dans le code !
## Importer des packages
Pour démarrer avec Aspose.Cells, assurez-vous d'avoir importé les espaces de noms nécessaires dans votre projet. Ces importations vous permettront d'accéder aux différentes classes et méthodes nécessaires à l'interaction avec les fichiers Excel.
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
Ces lignes garantissent que votre projet peut interagir avec les répertoires de fichiers (`System.IO`), classeurs Excel (`Aspose.Cells`), et le dessin de forme (`Aspose.Cells.Drawing`).
Maintenant, décomposons le processus en étapes simples afin que vous puissiez facilement le suivre et le reproduire dans vos propres projets.
## Étape 1 : Configuration du chemin d'accès au répertoire
La première étape consiste à définir le répertoire où sera enregistré votre fichier Excel. Cette étape permet de garantir que votre projet sait où créer et stocker le fichier de sortie.
### Définition du répertoire de données
```csharp
// Le chemin vers le répertoire des documents.
string dataDir = "Your Document Directory";
```
Ici, vous spécifiez le chemin d'accès au répertoire où sera stocké le fichier Excel. Vous pouvez remplacer `"Your Document Directory"` avec le chemin réel sur votre machine, ou créez dynamiquement un dossier s'il n'existe pas.
### Vérification et création du répertoire
```csharp
// Créez un répertoire s'il n'est pas déjà présent.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Ce bloc vérifie si le répertoire existe. Dans le cas contraire, il en crée un. Imaginez : préparer votre classeur avant de stocker des documents.
## Étape 2 : Instanciation d'un nouveau classeur
Dans cette étape, vous créez un nouveau classeur Excel à l’aide de `Aspose.Cells.Workbook` classe. Cela servira de conteneur pour votre feuille de travail et vos formes.
```csharp
// Instancier un nouveau classeur.
Workbook excelbook = new Workbook();
```
En appelant le `Workbook` constructeur, vous disposez désormais d'un classeur Excel vierge prêt à être personnalisé.
## Étape 3 : Ajout d'un contrôle rectangulaire
C'est ici que la magie opère : vous ajouterez une forme rectangulaire à la première feuille de calcul de votre classeur.
```csharp
// Ajoutez un contrôle rectangle.
Aspose.Cells.Drawing.RectangleShape rectangle = excelbook.Worksheets[0].Shapes.AddRectangle(3, 0, 2, 0, 70, 130);
```
Décomposons cela :
- `excelbook.Worksheets[0]`:Cela permet d'accéder à la première feuille de calcul de votre classeur.
- `.Shapes.AddRectangle(3, 0, 2, 0, 70, 130)`: Ceci ajoute une forme rectangulaire à la feuille de calcul. Les paramètres définissent ici la position (ligne et colonne), ainsi que la largeur et la hauteur du rectangle.
## Étape 4 : Personnalisation du rectangle
Ajouter un rectangle ne suffit pas : il faut le personnaliser. Dans cette étape, nous allons définir l'emplacement, l'épaisseur de trait et le style des tirets du rectangle.
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
Ici, nous définissons l'épaisseur du trait du rectangle à 4 points. Plus le nombre est élevé, plus le trait est épais.
### Définition du style du tableau de bord
```csharp
// Définissez le style de tiret du rectangle.
rectangle.Line.DashStyle = MsoLineDashStyle.Solid;
```
Cette ligne définit le style de tiret de la bordure du rectangle comme plein. Vous pouvez expérimenter différents styles, comme `Dash` ou `Dot` en fonction de vos besoins.
## Étape 5 : Enregistrer le classeur
Une fois le rectangle ajouté et personnalisé, l’étape finale consiste à enregistrer le classeur dans le répertoire spécifié.
```csharp
// Enregistrez le fichier Excel.
excelbook.Save(dataDir + "book1.out.xls");
```
Cela enregistre le classeur en tant que `.xls` dans le dossier défini précédemment. Vous pouvez modifier le format du fichier en changeant son extension, par exemple `.xlsx` si vous préférez le nouveau format Excel.
## Conclusion
Et voilà ! Ajouter un contrôle rectangle à une feuille de calcul Excel avec Aspose.Cells pour .NET est un processus simple, une fois la procédure détaillée. Que vous ayez besoin d'ajouter des formes pour un rendu visuel attrayant, de mettre en évidence des sections de vos données ou de personnaliser vos rapports, Aspose.Cells vous offre la flexibilité nécessaire pour le faire par programmation.
Ce guide devrait vous avoir apporté toutes les connaissances nécessaires pour commencer à ajouter des formes comme des rectangles à vos feuilles Excel avec Aspose.Cells. Il est maintenant temps d'expérimenter et de découvrir les autres possibilités offertes par cette puissante bibliothèque !
## FAQ
### Puis-je ajouter d’autres formes comme des cercles ou des lignes à l’aide d’Aspose.Cells pour .NET ?  
Oui, Aspose.Cells vous permet d'ajouter une variété de formes, notamment des cercles, des lignes, des flèches, etc.
### Quelles autres propriétés puis-je définir pour le contrôle rectangle ?  
Vous pouvez personnaliser la couleur de remplissage, la couleur de ligne, la transparence et même ajouter du texte dans le rectangle.
### Aspose.Cells est-il compatible avec .NET Core ?  
Oui, Aspose.Cells prend en charge .NET Core, ainsi que .NET Framework et d’autres plates-formes basées sur .NET.
### Puis-je positionner le rectangle par rapport à une cellule spécifique ?  
Oui, vous pouvez placer le rectangle dans des lignes et des colonnes spécifiques, ou utiliser le `PlacementType` pour contrôler la façon dont il est ancré.
### Existe-t-il un essai gratuit disponible pour Aspose.Cells ?  
Oui, vous pouvez obtenir un [essai gratuit](https://releases.aspose.com/) depuis le site pour tester les fonctionnalités de la bibliothèque avant d'acheter.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}