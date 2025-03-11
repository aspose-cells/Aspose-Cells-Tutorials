---
title: Position de l'image (absolue) dans Excel
linktitle: Position de l'image (absolue) dans Excel
second_title: API de traitement Excel Aspose.Cells .NET
description: Apprenez à positionner des images de manière absolue dans Excel à l'aide d'Aspose.Cells pour .NET avec ce didacticiel complet étape par étape.
weight: 13
url: /fr/net/excel-ole-picture-objects/position-picture-absolute-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Position de l'image (absolue) dans Excel

## Introduction
Avez-vous déjà eu du mal à positionner correctement des images dans une feuille de calcul Excel ? Vous n'êtes pas seul ! De nombreux utilisateurs sont confrontés à ce défi, en particulier lorsque leurs besoins de visualisation de données nécessitent un positionnement absolu pour une meilleure esthétique ou clarté. Eh bien, ne cherchez pas plus loin ; ce guide vous guidera tout au long du processus simple de positionnement absolu d'images dans une feuille de calcul Excel à l'aide d'Aspose.Cells pour .NET. Que vous soyez un développeur travaillant sur la manipulation d'Excel ou un analyste de données cherchant à améliorer vos rapports, notre didacticiel étape par étape est là pour simplifier vos expériences Excel avec les images !
## Prérequis
Avant de plonger dans le code et les détails, vous devez préparer quelques éléments :
1.  Bibliothèque Aspose.Cells : assurez-vous que vous disposez de la dernière version de la bibliothèque Aspose.Cells pour .NET. Vous pouvez la télécharger à partir du[page des communiqués](https://releases.aspose.com/cells/net/).
2. Environnement de développement : assurez-vous que vous disposez d'un environnement de développement .NET fonctionnel. Vous pouvez utiliser Visual Studio ou tout autre IDE de votre choix.
3. Connaissances de base de C# : La familiarité avec le langage de programmation C# sera bénéfique pour comprendre les extraits de code.
4. Fichier image : ayez un fichier image (par exemple, « logo.jpg ») enregistré dans votre répertoire de documents désigné que vous prévoyez d'insérer dans votre feuille Excel.

## Paquets d'importation
Pour commencer, nous allons nous assurer que nous importons les packages nécessaires à notre projet. Votre fichier de projet doit inclure les espaces de noms suivants :
```csharp
using System.IO;
using Aspose.Cells;
```
En important ces espaces de noms, nous garantissons que notre programme peut exploiter les fonctionnalités fournies par Aspose.Cells.
Décomposons cela en étapes gérables pour plus de clarté.
## Étape 1 : Configurez votre répertoire de documents
Dans cette première étape, vous devez définir le répertoire dans lequel se trouvent vos documents. Cela est essentiel pour que le programme sache où enregistrer ou récupérer les fichiers. Voici comment vous pouvez le configurer :
```csharp
string dataDir = "Your Document Directory";
```
 Remplacez simplement`"Your Document Directory"` avec le chemin réel où se trouve votre fichier image. Cela pourrait ressembler à`"C:\\Users\\YourUsername\\Documents\\"`.
## Étape 2 : Instanciation d'un objet de classeur
 Ensuite, vous devez créer une nouvelle instance de`Workbook` classe. Cet objet représente votre fichier Excel :
```csharp
Workbook workbook = new Workbook();
```
À ce stade, vous disposez d’un classeur prêt à être rempli de données et d’images.
## Étape 3 : Ajout d’une nouvelle feuille de calcul
Maintenant que vous avez le classeur, vous devez y ajouter une feuille de calcul. C'est ici que la magie de l'ajout et du positionnement des images va se produire :
```csharp
int sheetIndex = workbook.Worksheets.Add();
```
 Cette ligne crée une nouvelle feuille de calcul dans votre classeur et renvoie son index, que nous stockons dans la variable`sheetIndex`.
## Étape 4 : Obtenir la nouvelle feuille de travail
Faisons référence à la feuille de calcul nouvellement créée. En utilisant l'index que nous venons d'obtenir, nous pouvons accéder à la feuille de calcul et la manipuler :
```csharp
Worksheet worksheet = workbook.Worksheets[sheetIndex];
```
 Vous pouvez désormais travailler avec le`worksheet` objet pour ajouter du contenu, y compris des images.
## Étape 5 : Ajout d'une image
Passons maintenant à la partie intéressante ! C'est ici que nous ajoutons l'image à notre feuille de calcul. Nous spécifions les indices de ligne et de colonne où nous voulons que l'image soit ancrée (dans ce cas, à la cellule « F6 », qui correspond à la ligne 5 et à la colonne 5) :
```csharp
int pictureIndex = worksheet.Pictures.Add(5, 5, dataDir + "logo.jpg");
```
Cette ligne verrouille efficacement l'image à l'emplacement spécifié par rapport à l'ensemble de la feuille de calcul. Cependant, pour l'instant, elle est toujours sujette au redimensionnement en même temps que les cellules.
## Étape 6 : Accéder à la nouvelle image ajoutée
Pour manipuler davantage l'image, vous devez accéder à ses propriétés :
```csharp
Aspose.Cells.Drawing.Picture picture = worksheet.Pictures[pictureIndex];
```
Avec cela, vous accédez aux propriétés de l’image que nous venons d’ajouter !
## Étape 7 : Définition du positionnement absolu de l'image
 Pour positionner l'image de manière absolue (en pixels), vous devrez définir sa position à l'aide de la`Left` et`Top` propriétés. C'est ici que vous aurez le contrôle sur l'endroit où l'image apparaît :
```csharp
picture.Left = 60;
picture.Top = 10;
```
Vous pouvez ajuster les deux valeurs selon vos besoins ; elles représentent respectivement le positionnement horizontal et vertical de l'image.
## Étape 8 : enregistrement du fichier Excel
Enfin, après avoir effectué toutes vos modifications, il est temps de sauvegarder le classeur :
```csharp
workbook.Save(dataDir + "book1.out.xls");
```
 Cela créera un fichier Excel nommé`book1.out.xls` dans votre répertoire de documents précédemment défini, contenant votre feuille de calcul avec l'image placée absolument.

## Conclusion
Et voilà ! Vous avez positionné avec succès une image dans une feuille Excel avec un positionnement absolu à l'aide d'Aspose.Cells pour .NET. Ce processus simple améliore non seulement la présentation visuelle de vos documents Excel, mais garantit également que les images restent exactement là où vous le souhaitez, quelles que soient les modifications apportées aux tailles de cellules et aux hauteurs de lignes. Désormais, que vous prépariez un rapport ou créiez un tableau de bord, vous pouvez vous assurer que vos images sont parfaitement placées à chaque fois.
## FAQ
### Qu'est-ce qu'Aspose.Cells pour .NET ?
Aspose.Cells pour .NET est une bibliothèque .NET qui permet aux développeurs de créer, manipuler et convertir des feuilles de calcul Excel par programmation sans avoir besoin de Microsoft Excel.
### Puis-je effectuer d’autres manipulations d’images à l’aide d’Aspose.Cells ?
Oui, au-delà du positionnement, vous pouvez également redimensionner, faire pivoter et modifier des images dans des feuilles de calcul Excel à l'aide de la bibliothèque Aspose.Cells.
### L'utilisation d'Aspose.Cells est-elle gratuite ?
 Aspose.Cells est un produit commercial, mais vous pouvez commencer avec un essai gratuit disponible sur leur[page d'essai gratuite](https://releases.aspose.com/).
### Comment obtenir une licence temporaire pour Aspose.Cells ?
 Vous pouvez demander une licence temporaire via le[page de licence temporaire](https://purchase.aspose.com/temporary-license/) fourni par Aspose.
### Où puis-je trouver plus d’exemples et de documentation ?
 Le[Documentation d'Aspose.Cells](https://reference.aspose.com/cells/net/) contient de nombreuses ressources, notamment des exemples de code et des fonctionnalités plus détaillées.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
