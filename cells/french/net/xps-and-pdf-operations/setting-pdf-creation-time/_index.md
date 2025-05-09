---
"description": "Apprenez à définir l'heure de création d'un PDF dans .NET avec Aspose.Cells. Suivez notre guide étape par étape pour une conversion fluide d'Excel en PDF."
"linktitle": "Définition de l'heure de création du PDF dans .NET"
"second_title": "API de traitement Excel Aspose.Cells .NET"
"title": "Définition de l'heure de création du PDF dans .NET"
"url": "/fr/net/xps-and-pdf-operations/setting-pdf-creation-time/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Définition de l'heure de création du PDF dans .NET

## Introduction
À l'ère du numérique, la conversion de documents en différents formats est essentielle pour de nombreuses applications. Convertir des feuilles de calcul Excel en PDF est un besoin courant. Non seulement cela préserve la mise en forme, mais cela simplifie également grandement le partage et l'impression. Si vous êtes développeur et travaillez avec .NET, Aspose.Cells est une bibliothèque formidable qui simplifie ce processus. Dans ce tutoriel, nous allons découvrir comment définir l'heure de création d'un PDF lors de la conversion d'un fichier Excel en PDF avec Aspose.Cells pour .NET.
## Prérequis
Avant de passer aux détails du code, assurons-nous que vous disposez de tout ce dont vous avez besoin pour commencer.
### Ce dont vous avez besoin
1. Visual Studio : Assurez-vous que Visual Studio est installé sur votre machine. Ce sera votre environnement de développement.
2. Aspose.Cells pour .NET : téléchargez la bibliothèque Aspose.Cells depuis le [site web](https://releases.aspose.com/cells/net/). Vous pouvez également commencer par un essai gratuit pour tester ses fonctionnalités.
3. Connaissances de base de C# : la familiarité avec la programmation C# vous aidera à mieux comprendre les extraits de code.
4. Fichier Excel : Préparez un fichier Excel pour la conversion. Pour cet exemple, nous utiliserons un fichier nommé `Book1.xlsx`.
Maintenant que vous avez réglé les prérequis, passons à la partie amusante : importer les packages nécessaires et écrire le code !
## Importer des packages
Pour commencer, vous devez importer les espaces de noms requis dans votre fichier C#. Ceci est essentiel car cela vous permet d'accéder aux classes et méthodes fournies par la bibliothèque Aspose.Cells.
### Ouvrez votre projet C#
Ouvrez Visual Studio et créez un nouveau projet ou ouvrez-en un existant dans lequel vous souhaitez implémenter la fonctionnalité de conversion PDF.
### Ajouter une référence Aspose.Cells
Vous pouvez ajouter la bibliothèque Aspose.Cells à votre projet en cliquant avec le bouton droit sur votre projet dans l'Explorateur de solutions, en sélectionnant « Gérer les packages NuGet » et en recherchant « Aspose.Cells ». Installez le package.
### Importer des espaces de noms
En haut de votre fichier C#, incluez les espaces de noms suivants :
```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Charts;
```
Ces espaces de noms vous donneront accès à la classe Workbook et à d'autres fonctionnalités essentielles.

Maintenant que nos packages sont importés, décomposons le processus de conversion d'un fichier Excel en PDF tout en définissant l'heure de création.
## Étape 1 : Définir le répertoire des documents
Tout d'abord, vous devez spécifier le répertoire où sont stockés vos documents. C'est là que se trouve votre fichier Excel et où sera enregistré le PDF de sortie.
```csharp
string dataDir = "Your Document Directory"; // Spécifiez votre répertoire de documents
```
Remplacer `"Your Document Directory"` avec le chemin réel où votre `Book1.xlsx` Le fichier est localisé. Ce chemin permettra à l'application de localiser le fichier à traiter.
## Étape 2 : Charger le fichier Excel
Ensuite, vous chargerez le fichier Excel dans un `Workbook` objet. C'est là qu'Aspose.Cells brille, car il vous permet de travailler avec des fichiers Excel sans effort.
```csharp
string inputPath = dataDir + "Book1.xlsx"; // Chemin d'accès à votre fichier Excel
Workbook workbook = new Workbook(inputPath); // Charger le fichier Excel
```
Le `Workbook` La classe permet de charger et de manipuler des fichiers Excel. En transmettant le chemin d'entrée, vous indiquez à l'application le fichier à utiliser.
## Étape 3 : Créer PdfSaveOptions
Maintenant, il est temps de créer une instance de `PdfSaveOptions`Cette classe vous permet de spécifier différentes options pour enregistrer votre classeur au format PDF, y compris l'heure de création.
```csharp
PdfSaveOptions options = new PdfSaveOptions(); // Créer une instance PdfSaveOptions
options.CreatedTime = DateTime.Now; // Définir l'heure de création sur maintenant
```
En définissant `options.CreatedTime` à `DateTime.Now`, vous vous assurez que le PDF reflétera la date et l'heure actuelles de sa création.
## Étape 4 : Enregistrer le classeur au format PDF
Enfin, vous enregistrerez le classeur sous forme de fichier PDF en utilisant les options que vous venez de définir.
```csharp
workbook.Save(dataDir + "output.pdf", options); // Enregistrer au format PDF
```
Cette ligne de code prend le classeur et l'enregistre au format PDF à l'emplacement spécifié. `options` le paramètre est passé pour inclure l'heure de création dans les métadonnées PDF.

## Conclusion
Et voilà ! Vous avez réussi à convertir un fichier Excel en PDF avec Aspose.Cells pour .NET, avec horodatage de création. Cette fonctionnalité peut s'avérer très utile pour suivre les versions d'un document ou fournir aux destinataires des informations sur la date de création du document.
Si vous souhaitez explorer davantage de fonctionnalités d'Aspose.Cells, n'hésitez pas à consulter le [documentation](https://reference.aspose.com/cells/net/).
## FAQ
### Qu'est-ce qu'Aspose.Cells ?
Aspose.Cells est une bibliothèque puissante pour .NET qui permet aux développeurs de créer, manipuler et convertir des fichiers Excel.
### Puis-je utiliser Aspose.Cells gratuitement ?
Oui, vous pouvez commencer avec un essai gratuit disponible sur le [Site Web d'Aspose](https://releases.aspose.com/).
### Comment définir d’autres propriétés PDF ?
Vous pouvez définir diverses propriétés PDF à l’aide de l’ `PdfSaveOptions` classe, comme la taille de la page, la compression, etc.
### Est-il possible de convertir plusieurs fichiers Excel à la fois ?
Oui, vous pouvez parcourir une liste de fichiers et appliquer le même processus de conversion à chacun d'eux.
### Où puis-je obtenir de l'aide pour Aspose.Cells ?
Vous pouvez obtenir du soutien de la communauté Aspose sur leur [forum d'assistance](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}