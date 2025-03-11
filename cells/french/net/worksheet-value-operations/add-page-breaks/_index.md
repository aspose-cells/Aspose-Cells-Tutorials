---
title: Ajouter des sauts de page dans une feuille de calcul à l'aide d'Aspose.Cells
linktitle: Ajouter des sauts de page dans une feuille de calcul à l'aide d'Aspose.Cells
second_title: API de traitement Excel Aspose.Cells .NET
description: Découvrez comment ajouter des sauts de page horizontaux et verticaux dans Excel à l'aide d'Aspose.Cells pour .NET grâce à ce guide étape par étape. Rendez vos fichiers Excel faciles à imprimer.
weight: 10
url: /fr/net/worksheet-value-operations/add-page-breaks/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ajouter des sauts de page dans une feuille de calcul à l'aide d'Aspose.Cells

## Introduction
Dans ce didacticiel, nous vous expliquerons comment ajouter des sauts de page horizontaux et verticaux à votre feuille de calcul Excel. Vous découvrirez également un guide étape par étape sur la façon d'utiliser Aspose.Cells pour .NET pour manipuler facilement les sauts de page. À la fin de ce guide, vous serez à l'aise avec ces techniques dans vos propres projets. C'est parti !
## Prérequis
Avant de nous plonger dans le code, assurons-nous que vous êtes prêt à suivre ce tutoriel. Voici quelques prérequis :
- Visual Studio : vous aurez besoin de Visual Studio installé sur votre système.
-  Aspose.Cells pour .NET : vous devez avoir installé la bibliothèque Aspose.Cells. Si vous ne l'avez pas encore fait, ne vous inquiétez pas ! Vous pouvez télécharger une version d'essai gratuite pour commencer. (Vous pouvez l'obtenir[ici](https://releases.aspose.com/cells/net/)).
- .NET Framework : ce didacticiel suppose que vous travaillez avec .NET Framework ou .NET Core. Si vous utilisez un environnement différent, le processus peut varier légèrement.
De plus, vous devez avoir une certaine connaissance de base de la programmation C# et du concept de sauts de page dans Excel.
## Paquets d'importation
Pour commencer à travailler avec Aspose.Cells, nous devons importer les espaces de noms pertinents dans notre projet. Cela nous permet d'accéder aux fonctionnalités fournies par Aspose.Cells pour manipuler les fichiers Excel.
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
Une fois ces espaces de noms importés, vous pouvez commencer à interagir avec les fichiers Excel et appliquer diverses modifications, notamment l'ajout de sauts de page.
Maintenant que vous êtes prêt, passons en revue les étapes à suivre pour ajouter des sauts de page à votre feuille de calcul. Nous allons décomposer chaque partie du processus, en expliquant chaque ligne de code en détail.
## Étape 1 : Configurez votre classeur
 Tout d'abord, vous devez créer un nouveau classeur.`Workbook` La classe dans Aspose.Cells représente un classeur Excel et constitue le point de départ de la manipulation de fichiers Excel.
```csharp
// Définissez le chemin d'accès au répertoire où votre fichier sera enregistré
string dataDir = "Your Document Directory";
// Créer un nouvel objet Classeur
Workbook workbook = new Workbook();
```
Dans ce code :
- `dataDir` spécifie où votre fichier sera enregistré.
-  Le`Workbook` un objet est créé, qui sera utilisé pour contenir et manipuler votre fichier Excel.
## Étape 2 : ajouter un saut de page horizontal
Ensuite, nous allons ajouter un saut de page horizontal à la feuille de calcul. Un saut de page horizontal divise la feuille de calcul en deux parties horizontalement, ce qui signifie qu'il détermine où le contenu sera divisé verticalement sur une nouvelle page lors de l'impression.
```csharp
//Ajouter un saut de page horizontal à la ligne 30
workbook.Worksheets[0].HorizontalPageBreaks.Add("Y30");
```
Dans cet exemple :
- `Worksheets[0]` fait référence à la première feuille du classeur (rappelez-vous, les feuilles de calcul sont indexées à zéro).
- `HorizontalPageBreaks.Add("Y30")` ajoute un saut de page à la ligne 30. Cela signifie que le contenu avant la ligne 30 apparaîtra sur une page et que tout ce qui se trouve en dessous commencera sur une nouvelle page.
## Étape 3 : ajouter un saut de page vertical
De la même manière, vous pouvez ajouter un saut de page vertical. Cela coupera la feuille de calcul au niveau d'une colonne spécifique, garantissant que le contenu à gauche du saut apparaît sur une page et que le contenu à droite apparaît sur la page suivante.
```csharp
// Ajouter un saut de page vertical à la colonne Y
workbook.Worksheets[0].VerticalPageBreaks.Add("Y30");
```
Ici:
-  Le`VerticalPageBreaks.Add("Y30")` La méthode ajoute un saut de page vertical à la colonne Y (c'est-à-dire après la 25e colonne). Cela créera un saut de page entre les colonnes X et Y.
## Étape 4 : Enregistrer le classeur
Après avoir ajouté vos sauts de page, la dernière étape consiste à enregistrer le classeur dans un fichier. Vous pouvez spécifier le chemin où vous souhaitez enregistrer le fichier Excel.
```csharp
// Enregistrer le fichier Excel
workbook.Save(dataDir + "AddingPageBreaks_out.xls");
```
Cela enregistrera le classeur avec les sauts de page ajoutés dans le chemin de fichier spécifié (`AddingPageBreaks_out.xls`).
## Conclusion
L'ajout de sauts de page dans Excel est une fonctionnalité essentielle lorsque vous travaillez avec de grands ensembles de données ou que vous préparez des documents pour l'impression. Avec Aspose.Cells pour .NET, vous pouvez facilement automatiser le processus d'insertion de sauts de page horizontaux et verticaux dans vos feuilles de calcul Excel, garantissant ainsi que vos documents sont bien organisés et faciles à lire.
## FAQ
### Comment ajouter plusieurs sauts de page dans Aspose.Cells pour .NET ?
 Vous pouvez ajouter plusieurs sauts de page en appelant simplement le`HorizontalPageBreaks.Add()` ou`VerticalPageBreaks.Add()` méthodes plusieurs fois avec différentes références de cellules.
### Puis-je ajouter des sauts de page dans une feuille de calcul spécifique d'un classeur ?
 Oui, vous pouvez spécifier la feuille de calcul en utilisant le`Worksheets[index]` propriété où`index` est l'index de base zéro de la feuille de calcul.
### Comment supprimer un saut de page dans Aspose.Cells pour .NET ?
 Vous pouvez supprimer un saut de page à l'aide de la`HorizontalPageBreaks.RemoveAt()` ou`VerticalPageBreaks.RemoveAt()` méthodes en spécifiant l'index du saut de page que vous souhaitez supprimer.
### Que faire si je souhaite ajouter automatiquement des sauts de page en fonction de la taille du contenu ?
Aspose.Cells ne fournit pas de fonctionnalité automatique pour ajouter des sauts de page en fonction de la taille du contenu, mais vous pouvez calculer par programmation où les sauts doivent se produire en fonction du nombre de lignes/colonnes.
### Puis-je définir des sauts de page en fonction d’une plage spécifique de cellules ?
Oui, vous pouvez spécifier des sauts de page pour n'importe quelle cellule ou plage en fournissant la référence de cellule correspondante, telle que « A1 » ou « B15 ».

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
