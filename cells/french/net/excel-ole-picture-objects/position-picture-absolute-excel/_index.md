---
"description": "Apprenez à positionner des images de manière absolue dans Excel à l'aide d'Aspose.Cells pour .NET avec ce didacticiel complet étape par étape."
"linktitle": "Position de l'image (absolue) dans Excel"
"second_title": "API de traitement Excel Aspose.Cells .NET"
"title": "Position de l'image (absolue) dans Excel"
"url": "/fr/net/excel-ole-picture-objects/position-picture-absolute-excel/"
"weight": 13
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Position de l'image (absolue) dans Excel

## Introduction
Avez-vous déjà eu du mal à positionner correctement des images dans une feuille de calcul Excel ? Vous n'êtes pas seul ! De nombreux utilisateurs rencontrent ce problème, notamment lorsque leurs besoins en visualisation de données nécessitent un positionnement absolu pour une meilleure esthétique ou une meilleure clarté. Ne cherchez plus ! Ce guide vous guidera pas à pas dans le positionnement absolu d'images dans une feuille de calcul Excel avec Aspose.Cells pour .NET. Que vous soyez développeur travaillant sur Excel ou analyste de données cherchant à améliorer vos rapports, notre tutoriel étape par étape est là pour simplifier votre expérience Excel avec les images !
## Prérequis
Avant de plonger dans le code et les détails, vous devez préparer quelques éléments :
1. Bibliothèque Aspose.Cells : Assurez-vous de disposer de la dernière version de la bibliothèque Aspose.Cells pour .NET. Vous pouvez la télécharger depuis le [page des communiqués](https://releases.aspose.com/cells/net/).
2. Environnement de développement : Assurez-vous de disposer d'un environnement de développement .NET fonctionnel. Vous pouvez utiliser Visual Studio ou tout autre IDE de votre choix.
3. Connaissances de base de C# : la familiarité avec le langage de programmation C# sera bénéfique pour comprendre les extraits de code.
4. Fichier image : enregistrez un fichier image (par exemple, « logo.jpg ») dans votre répertoire de documents désigné que vous prévoyez d'insérer dans votre feuille Excel.

## Importer des packages
Pour commencer, nous allons importer les packages nécessaires à notre projet. Votre fichier de projet doit inclure les espaces de noms suivants :
```csharp
using System.IO;
using Aspose.Cells;
```
En important ces espaces de noms, nous garantissons que notre programme peut exploiter les fonctionnalités fournies par Aspose.Cells.
Décomposons cela en étapes gérables pour plus de clarté.
## Étape 1 : Configurez votre répertoire de documents
Lors de cette première étape, vous devez définir le répertoire où se trouvent vos documents. Ceci est essentiel pour que le programme sache où enregistrer ou récupérer les fichiers. Voici comment procéder :
```csharp
string dataDir = "Your Document Directory";
```
Remplacez simplement `"Your Document Directory"` avec le chemin d'accès réel de votre fichier image. Cela pourrait ressembler à ceci : `"C:\\Users\\YourUsername\\Documents\\"`.
## Étape 2 : Instanciation d'un objet de classeur
Ensuite, vous devez créer une nouvelle instance du `Workbook` classe. Cet objet représente votre fichier Excel :
```csharp
Workbook workbook = new Workbook();
```
À ce stade, vous disposez d’un classeur prêt à être rempli de données et d’images.
## Étape 3 : Ajout d'une nouvelle feuille de calcul
Maintenant que vous avez le classeur, vous devez y ajouter une feuille de calcul. C'est ici que la magie de l'ajout et du positionnement des images se produit :
```csharp
int sheetIndex = workbook.Worksheets.Add();
```
Cette ligne crée une nouvelle feuille de calcul dans votre classeur et renvoie son index, que nous stockons dans la variable `sheetIndex`.
## Étape 4 : Obtenir la nouvelle feuille de travail
Référençons-nous à la feuille de calcul nouvellement créée. Grâce à l'index obtenu, nous pouvons accéder à la feuille de calcul et la manipuler :
```csharp
Worksheet worksheet = workbook.Worksheets[sheetIndex];
```
Vous pouvez désormais travailler avec le `worksheet` objet pour ajouter du contenu, y compris des images.
## Étape 5 : Ajout d'une image
Passons maintenant à la partie intéressante ! Nous ajoutons l'image à notre feuille de calcul. Nous spécifions les indices de ligne et de colonne où nous souhaitons ancrer l'image (dans ce cas, la cellule « F6 », qui correspond à la ligne et à la colonne 5) :
```csharp
int pictureIndex = worksheet.Pictures.Add(5, 5, dataDir + "logo.jpg");
```
Cette ligne verrouille l'image à l'emplacement spécifié par rapport à l'ensemble de la feuille de calcul. Cependant, pour l'instant, elle est toujours susceptible d'être redimensionnée, tout comme les cellules.
## Étape 6 : Accéder à la nouvelle image ajoutée
Pour manipuler davantage l'image, vous devez accéder à ses propriétés :
```csharp
Aspose.Cells.Drawing.Picture picture = worksheet.Pictures[pictureIndex];
```
Avec cela, vous accédez aux propriétés de l'image que nous venons d'ajouter !
## Étape 7 : Définition du positionnement absolu de l'image
Pour positionner l'image de manière absolue (en pixels), vous devrez définir sa position à l'aide du `Left` et `Top` Propriétés. C'est ici que vous contrôlerez l'emplacement d'affichage de l'image :
```csharp
picture.Left = 60;
picture.Top = 10;
```
Vous pouvez ajuster les deux valeurs selon vos besoins ; elles représentent respectivement le positionnement horizontal et vertical de l'image.
## Étape 8 : Enregistrement du fichier Excel
Enfin, après avoir effectué toutes vos modifications, il est temps de sauvegarder le classeur :
```csharp
workbook.Save(dataDir + "book1.out.xls");
```
Cela créera un fichier Excel nommé `book1.out.xls` dans votre répertoire de documents précédemment défini, contenant votre feuille de calcul avec l'image placée absolument.

## Conclusion
Et voilà ! Vous avez réussi à positionner une image dans une feuille Excel avec un positionnement absolu grâce à Aspose.Cells pour .NET. Ce processus simple améliore non seulement la présentation visuelle de vos documents Excel, mais garantit également que les images restent exactement là où vous le souhaitez, quelles que soient les modifications apportées à la taille des cellules et à la hauteur des lignes. Que vous prépariez un rapport ou créiez un tableau de bord, vous pouvez désormais garantir un positionnement parfait de vos images à chaque fois.
## FAQ
### Qu'est-ce qu'Aspose.Cells pour .NET ?
Aspose.Cells pour .NET est une bibliothèque .NET qui permet aux développeurs de créer, manipuler et convertir des feuilles de calcul Excel par programmation sans avoir besoin de Microsoft Excel.
### Puis-je effectuer d’autres manipulations d’images à l’aide d’Aspose.Cells ?
Oui, au-delà du positionnement, vous pouvez également redimensionner, faire pivoter et modifier des images dans des feuilles de calcul Excel à l'aide de la bibliothèque Aspose.Cells.
### Aspose.Cells est-il gratuit à utiliser ?
Aspose.Cells est un produit commercial, mais vous pouvez commencer avec un essai gratuit disponible sur leur [page d'essai gratuite](https://releases.aspose.com/).
### Comment obtenir une licence temporaire pour Aspose.Cells ?
Vous pouvez demander une licence temporaire via le [page de licence temporaire](https://purchase.aspose.com/temporary-license/) fourni par Aspose.
### Où puis-je trouver plus d'exemples et de documentation ?
Le [Documentation d'Aspose.Cells](https://reference.aspose.com/cells/net/) contient des ressources complètes, notamment des exemples de code et des fonctionnalités plus détaillées.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}