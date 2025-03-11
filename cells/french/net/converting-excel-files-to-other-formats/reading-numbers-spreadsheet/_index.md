---
title: Lecture de feuilles de calcul de nombres par programmation dans .NET
linktitle: Lecture de feuilles de calcul de nombres par programmation dans .NET
second_title: API de traitement Excel Aspose.Cells .NET
description: Apprenez à lire les feuilles de calcul Numbers et à les convertir en PDF à l'aide d'Aspose.Cells pour .NET dans ce didacticiel détaillé.
weight: 18
url: /fr/net/converting-excel-files-to-other-formats/reading-numbers-spreadsheet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Lecture de feuilles de calcul de nombres par programmation dans .NET

## Introduction
Dans le monde numérique d'aujourd'hui, la gestion des données est une compétence essentielle, et les feuilles de calcul sont au premier plan de l'organisation des données. Mais que faire si vous devez travailler avec une feuille de calcul Numbers (ces fichiers créés par l'application Numbers d'Apple) à l'aide de .NET ? Ne vous inquiétez pas, vous n'êtes pas seul ! Dans ce didacticiel, nous allons parcourir le processus de lecture d'une feuille de calcul Numbers par programmation avec Aspose.Cells pour .NET. Vous apprendrez à charger un fichier Numbers et à le convertir en PDF.
## Prérequis
Avant de commencer, vous devez mettre en place quelques éléments :
1. Aspose.Cells pour .NET : assurez-vous que la bibliothèque Aspose.Cells est installée. Vous pouvez la télécharger[ici](https://releases.aspose.com/cells/net/).
2. Visual Studio : il est recommandé d’avoir Visual Studio (ou tout autre IDE compatible .NET) installé sur votre machine.
3. Connaissances de base de C# : une petite familiarité avec la programmation C# vous aidera à suivre en douceur.
4. Votre répertoire de documents : vous aurez besoin d'un répertoire dans lequel votre fichier Numbers est stocké, ainsi que d'un emplacement pour enregistrer le PDF converti.
Une fois ces prérequis couverts, vous êtes prêt à commencer !
## Paquets d'importation
Pour commencer, nous devons importer les packages nécessaires dans notre projet C#. Il s’agit d’une étape cruciale car elle nous permet de tirer parti des fonctionnalités fournies par la bibliothèque Aspose.Cells.
1. Ouvrez votre projet C# dans Visual Studio.
2. Ajoutez une référence à la bibliothèque Aspose.Cells :
   - Si vous utilisez NuGet, exécutez simplement la commande suivante dans la console du gestionnaire de packages :
```
 Install-Package Aspose.Cells
 ```
3. Importez les espaces de noms nécessaires dans votre code :
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Maintenant que nous avons importé les packages nécessaires, passons au guide étape par étape pour lire une feuille de calcul Numbers.
## Étape 1 : Spécifier les répertoires source et de sortie
Dans cette étape, nous allons configurer les répertoires dans lesquels se trouve votre fichier Numbers source et où vous souhaitez enregistrer le PDF de sortie.
```csharp
// Répertoire des sources
string sourceDir = "Your Document Directory"; // Mettez à jour ceci avec votre répertoire actuel
// Répertoire de sortie
string outputDir = "Your Document Directory"; // Mettez à jour ceci avec votre répertoire actuel
```
 Ici, nous définissons deux variables de chaîne,`sourceDir` et`outputDir` , pour spécifier les emplacements des fichiers d'entrée et de sortie. Assurez-vous de remplacer`"Your Document Directory"` avec les chemins réels sur votre système.
## Étape 2 : Configurer les options de chargement pour le format des nombres
Ensuite, nous allons spécifier les options de chargement pour la lecture d'une feuille de calcul Numbers. Cette étape est essentielle car elle indique à Aspose comment interpréter le fichier Numbers.
```csharp
// Spécifiez les options de chargement ; nous voulons charger la feuille de calcul Numbers
LoadOptions opts = new LoadOptions(LoadFormat.Numbers);
```
 Nous créons un`LoadOptions` objet et spécifiez le format comme`LoadFormat.Numbers`Cela indique à la bibliothèque Aspose.Cells que nous travaillons avec un fichier Numbers. 
## Étape 3 : chargez la feuille de calcul Numbers dans un classeur
Maintenant, il est temps de charger la feuille de calcul Numbers réelle dans un`Workbook` objet.
```csharp
// Chargez la feuille de calcul Numbers dans le classeur avec les options de chargement ci-dessus
Workbook wb = new Workbook(sourceDir + "sampleNumbersByAppleInc.numbers", opts);
```
 Nous instancions un`Workbook` objet et transmettez le chemin d'accès du fichier Numbers avec nos options de chargement. Assurez-vous que le nom du fichier (`sampleNumbersByAppleInc.numbers`) correspond au nom réel de votre fichier Numbers.
## Étape 4 : Enregistrer le classeur au format PDF
Une fois le fichier Numbers chargé avec succès, l’étape suivante consiste à l’enregistrer dans un format différent, notamment PDF.
```csharp
// Enregistrer le classeur au format PDF
wb.Save(outputDir + "outputNumbersByAppleInc.pdf", SaveFormat.Pdf);
```
 Ici, nous appelons le`Save` méthode sur le`Workbook` objet, en spécifiant le chemin du fichier de sortie et le format dans lequel nous voulons l'enregistrer. Dans ce cas, nous l'enregistrons au format PDF. Assurez-vous que le nom du fichier de sortie (`outputNumbersByAppleInc.pdf`) est unique et n'écrase aucun fichier existant.
## Étape 5 : Confirmer le succès
Enfin, ajoutons un message pour confirmer que notre opération a réussi.
```csharp
Console.WriteLine("ReadNumbersSpreadsheet executed successfully.\r\n");
```
Cette ligne de code affichera un message de réussite sur la console une fois que tout sera terminé. C'est toujours agréable d'avoir des retours, n'est-ce pas ?
## Conclusion
Et voilà ! Vous avez lu avec succès une feuille de calcul Numbers et l'avez convertie en PDF à l'aide d'Aspose.Cells pour .NET. Cette puissante bibliothèque vous permet de manipuler des feuilles de calcul sans effort, ce qui simplifie vos tâches de gestion des données. Que vous développiez des applications ou que vous ayez simplement besoin de gérer des feuilles de calcul plus efficacement, Aspose.Cells est un outil fantastique à avoir dans votre boîte à outils.
## FAQ
### Quels types de fichiers Aspose.Cells peut-il lire ?  
Aspose.Cells peut lire une variété de formats de fichiers, notamment les fichiers XLS, XLSX, CSV et Numbers. 
### Puis-je modifier des fichiers Numbers à l’aide d’Aspose.Cells ?  
Oui, vous pouvez lire, manipuler et enregistrer des fichiers Numbers avec Aspose.Cells.
### L'utilisation d'Aspose.Cells est-elle gratuite ?  
 Aspose.Cells propose un essai gratuit, mais vous aurez besoin d'une licence pour une utilisation prolongée. Vérifiez les tarifs[ici](https://purchase.aspose.com/buy).
### Que dois-je faire si je rencontre une erreur lors du chargement d'un fichier Numbers ?  
 Assurez-vous que vous utilisez les options de chargement correctes et que le chemin d'accès au fichier est précis. Pour plus d'assistance, visitez le[Forum d'assistance Aspose](https://forum.aspose.com/c/cells/9).
### Comment puis-je obtenir une licence temporaire pour Aspose.Cells ?  
 Vous pouvez demander une licence temporaire[ici](https://purchase.aspose.com/temporary-license/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
