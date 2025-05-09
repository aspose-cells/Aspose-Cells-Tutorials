---
"description": "Apprenez à positionner des images proportionnellement dans Excel avec Aspose.Cells pour .NET. Améliorez l'esthétique de vos feuilles de calcul."
"linktitle": "Position de l'image (proportionnelle) dans Excel"
"second_title": "API de traitement Excel Aspose.Cells .NET"
"title": "Position de l'image (proportionnelle) dans Excel"
"url": "/fr/net/excel-ole-picture-objects/position-picture-proportional-excel/"
"weight": 14
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Position de l'image (proportionnelle) dans Excel

## Introduction
Vous en avez assez de ces images pixelisées qui ne semblent jamais s'intégrer parfaitement dans vos feuilles de calcul Excel ? Imaginez : vous avez un beau logo qui doit être mis en valeur dans votre feuille Excel, mais il finit écrasé, étiré ou mal positionné. Personne ne souhaite cela ! Accrochez-vous bien, car aujourd'hui, vous allez apprendre à positionner des images proportionnellement dans Excel grâce à la bibliothèque Aspose.Cells pour .NET. Cette puissante bibliothèque simplifie la manipulation des fichiers Excel, que ce soit pour la création de rapports, l'analyse de données ou simplement pour embellir vos présentations. Plongeons dans les détails de l'alignement parfait de vos images !
## Prérequis
Avant de plonger dans le codage proprement dit, vous devez configurer quelques éléments sur votre machine :
1. Visual Studio : assurez-vous que Visual Studio est installé, car il fournira un environnement pratique pour votre projet .NET.
2. Bibliothèque Aspose.Cells : Vous aurez besoin de la bibliothèque Aspose.Cells. Vous pouvez l'essayer gratuitement ou l'acheter sur le site. [Site Web d'Aspose](https://purchase.aspose.com/buy).
3. Connaissances de base de C# : une petite familiarité avec la programmation C# contribuera grandement à la compréhension des exemples dont nous allons discuter.
4. Un fichier image : préparez une image (comme votre logo) que vous souhaitez insérer dans la feuille Excel.
Maintenant que tout est en place, passons au codage !
## Importer des packages
Pour commencer à utiliser Aspose.Cells dans votre projet, vous devez importer les espaces de noms spécifiques. Voici comment procéder :
### Créer un nouveau projet
Dans Visual Studio, créez un nouveau projet :
- Ouvrez Visual Studio.
- Cliquez sur « Créer un nouveau projet ».
- Choisissez « Bibliothèque de classes (.NET Framework) » ou « Application console », selon votre préférence.
### Installer Aspose.Cells
Vous pouvez ajouter le package Aspose.Cells à votre projet via NuGet. Voici comment :
- Cliquez avec le bouton droit sur votre projet dans l’Explorateur de solutions.
- Sélectionnez « Gérer les packages NuGet ».
- Recherchez « Aspose.Cells » et cliquez sur « Installer ».
### Ajouter des directives d'utilisation
En haut de votre fichier de code, incluez les directives suivantes :
```csharp
using System.IO;
using Aspose.Cells;
```
Ces directives vous donneront accès aux classes dont vous aurez besoin pour manipuler vos fichiers Excel.
Maintenant, décomposons cela en étapes détaillées pour positionner avec succès une image proportionnellement dans Excel.
## Étape 1 : Configurez votre répertoire
Avant toute chose, assurez-vous de disposer d'un dossier dédié à vos documents. Voici comment créer un répertoire s'il n'existe pas :
```csharp
string dataDir = "Your Document Directory";
// Créez un répertoire s'il n'est pas déjà présent.
bool isExists = System.IO.Directory.Exists(dataDir);
if (!isExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Cet extrait crée un nouveau répertoire (s'il n'existe pas) pour stocker vos fichiers Excel. Il suffit de le remplacer. `"Your Document Directory"` avec le chemin réel où vous souhaitez enregistrer vos fichiers.
## Étape 2 : instancier un classeur
Ensuite, créons un nouveau classeur :
```csharp
Workbook workbook = new Workbook();
```
Cette ligne initialise un nouvel objet de classeur, vous donnant une toile vierge sur laquelle travailler.
## Étape 3 : Ajouter une nouvelle feuille de calcul
Maintenant que notre classeur est configuré, ajoutons-y une nouvelle feuille de calcul :
```csharp
int sheetIndex = workbook.Worksheets.Add();
```
Cela ajoutera une nouvelle feuille de calcul et renverra l'index de cette feuille, que nous pourrons utiliser pour la manipuler plus tard.
## Étape 4 : Accéder à la nouvelle feuille de calcul
Pour manipuler la feuille de calcul nouvellement ajoutée, vous devez y accéder :
```csharp
Worksheet worksheet = workbook.Worksheets[sheetIndex];
```
Maintenant, `worksheet` nous permettra d'ajouter du contenu et des images à cette feuille spécifique.
## Étape 5 : Insérer l'image
Et maintenant, place au plus intéressant ! Ajoutez votre magnifique image. Remplacez `"logo.jpg"` avec le nom de votre fichier image :
```csharp
int pictureIndex = worksheet.Pictures.Add(5, 5, dataDir + "logo.jpg");
```
Cette ligne ajoute l'image à la cellule F6 (puisque les lignes et les colonnes sont indexées à zéro, `5` fait référence à la sixième cellule).
## Étape 6 : Accéder à l'image ajoutée
Une fois l'image insérée, vous pouvez y accéder comme ceci :
```csharp
Aspose.Cells.Drawing.Picture picture = worksheet.Pictures[pictureIndex];
```
Cela vous permet de manipuler les propriétés de l'image.
## Étape 7 : Positionnez l'image proportionnellement
Maintenant, positionnons l'image proportionnellement :
```csharp
picture.UpperDeltaX = 200;
picture.UpperDeltaY = 200;
```
Ici, `UpperDeltaX` et `UpperDeltaY` Ajustez la position de l'image par rapport aux dimensions de la cellule. Vous pouvez ajuster ces valeurs pour obtenir une image parfaite.
## Étape 8 : Enregistrez vos modifications
Enfin, enregistrez votre classeur pour conserver toutes les modifications :
```csharp
workbook.Save(dataDir + "book1.out.xls");
```
Cette ligne enregistre votre classeur sous `book1.out.xls` dans le répertoire désigné.
## Conclusion
Et voilà ! Vous venez d'apprendre à positionner des images proportionnellement dans Excel avec Aspose.Cells pour .NET. Il ne s'agit pas seulement d'insérer des images, mais de les rendre parfaites dans vos feuilles de calcul. N'oubliez pas : une image bien placée peut améliorer considérablement la présentation de vos données.
Amusez-vous à tester différentes images et placements, et n'hésitez pas à explorer les nombreuses fonctionnalités d'Aspose.Cells. Vos feuilles Excel sont sur le point de faire peau neuve !
## FAQ
### Qu'est-ce qu'Aspose.Cells ?
Aspose.Cells est une bibliothèque puissante pour .NET qui permet aux utilisateurs de créer, manipuler et convertir des fichiers Excel sans avoir besoin d'installer Microsoft Excel.
### Puis-je utiliser Aspose.Cells gratuitement ?
Oui, Aspose.Cells propose un essai gratuit, que vous pouvez télécharger [ici](https://releases.aspose.com/).
### Où puis-je trouver la documentation ?
Vous pouvez accéder à l'intégralité [documentation](https://reference.aspose.com/cells/net/) pour Aspose.Cells.
### Aspose.Cells prend-il en charge tous les formats d'image ?
Aspose.Cells prend en charge divers formats, notamment JPEG, PNG, BMP, GIF et TIFF.
### Comment puis-je obtenir de l'aide pour Aspose.Cells ?
Pour toute question, n'hésitez pas à visiter le [forum d'assistance](https://forum.aspose.com/c/cells/9) où vous pouvez poser vos questions.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}