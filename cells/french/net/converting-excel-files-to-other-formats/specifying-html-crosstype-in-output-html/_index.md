---
title: Spécification du CrossType HTML dans la sortie HTML par programmation dans .NET
linktitle: Spécification du CrossType HTML dans la sortie HTML par programmation dans .NET
second_title: API de traitement Excel Aspose.Cells .NET
description: Découvrez comment spécifier le CrossType HTML dans Aspose.Cells pour .NET. Suivez notre tutoriel étape par étape pour convertir des fichiers Excel en HTML avec précision.
weight: 17
url: /fr/net/converting-excel-files-to-other-formats/specifying-html-crosstype-in-output-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Spécification du CrossType HTML dans la sortie HTML par programmation dans .NET

## Introduction
Lorsqu'il s'agit de convertir des fichiers Excel en HTML dans des applications .NET, vous devrez peut-être spécifier la manière dont les références croisées sont gérées dans la sortie. La classe HtmlSaveOptions dans Aspose.Cells pour .NET fournit divers paramètres pour contrôler le processus de conversion, et l'une de ces options est HtmlCrossType. Dans ce didacticiel, nous verrons comment spécifier par programmation le type croisé HTML lors de l'exportation de fichiers Excel au format HTML. 
## Prérequis
Avant de plonger dans le code, assurez-vous de disposer des éléments suivants :
-  Aspose.Cells pour .NET : assurez-vous que la bibliothèque Aspose.Cells est installée dans votre projet. Vous pouvez la télécharger à partir du[Site Web d'Aspose](https://releases.aspose.com/cells/net/).
- Visual Studio : une installation fonctionnelle de Visual Studio ou de tout autre environnement de développement .NET.
- Connaissances de base de C# : une familiarité avec la programmation C# vous aidera à mieux comprendre les exemples.
-  Exemple de fichier Excel : préparez un exemple de fichier Excel. Pour cet exemple, nous utiliserons`sampleHtmlCrossStringType.xlsx`.
## Paquets d'importation
Pour commencer, vous devez importer les espaces de noms Aspose.Cells nécessaires. Voici comment procéder :
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Décomposons cela étape par étape, afin qu'il vous soit facile de suivre et d'implémenter cette fonctionnalité dans vos propres projets.
## Étape 1 : définissez vos répertoires source et de sortie
Tout d’abord, vous devez définir les répertoires de votre fichier Excel source et où vous souhaitez enregistrer le fichier HTML de sortie.
```csharp
// Répertoire des sources
string sourceDir = "Your Document Directory";
// Répertoire de sortie
string outputDir = "Your Document Directory";
```
## Étape 2 : charger l’exemple de fichier Excel
 Ensuite, chargez votre exemple de fichier Excel dans un`Workbook` objet. C'est ici que toute la magie commence.
```csharp
// Charger l'exemple de fichier Excel
Workbook wb = new Workbook(sourceDir + "sampleHtmlCrossStringType.xlsx");
```
 Ici, remplacez`"Your Document Directory"` avec le chemin réel où se trouve votre fichier Excel. Cette ligne lit le fichier Excel en mémoire afin que vous puissiez le manipuler.
## Étape 3 : Spécifier les options d’enregistrement HTML
 Maintenant, nous allons créer une instance de`HtmlSaveOptions`, qui vous permet de configurer la manière dont le fichier Excel sera converti en HTML.
```csharp
// Spécifier le type croisé HTML
HtmlSaveOptions opts = new HtmlSaveOptions();
opts.HtmlCrossStringType = HtmlCrossType.Default;
```
 Dans cette étape, nous avons défini le`HtmlCrossStringType` à`HtmlCrossType.Default`, qui est l’une des options disponibles pour gérer les références croisées dans le code HTML de sortie.
## Étape 4 : modifiez le type de croix selon vos besoins
 Vous pouvez spécifier différents types pour`HtmlCrossStringType` en fonction de vos besoins. Voici les différentes options que vous pouvez utiliser :
- `HtmlCrossType.Default`: Le type de croix par défaut.
- `HtmlCrossType.MSExport`: Exporte le HTML avec un comportement similaire à celui de MS Excel.
- `HtmlCrossType.Cross`: Crée des références croisées.
- `HtmlCrossType.FitToCell`: Ajuste les références croisées aux dimensions de la cellule.
 Vous pouvez modifier le`HtmlCrossStringType` comme ça:
```csharp
opts.HtmlCrossStringType = HtmlCrossType.MSExport;
// ou
opts.HtmlCrossStringType = HtmlCrossType.Cross;
// ou
opts.HtmlCrossStringType = HtmlCrossType.FitToCell;
```
## Étape 5 : Enregistrer le fichier HTML de sortie
 Une fois vos options configurées, il est temps d'enregistrer le fichier HTML converti. Utilisez le`Save` méthode sur votre`Workbook` objet:
```csharp
// Sortie HTML
wb.Save(outputDir + "out" + opts.HtmlCrossStringType + ".htm", opts);
```
 Ici, nous nommons le fichier de sortie en fonction de la`HtmlCrossStringType` nous avons défini. De cette façon, vous pouvez facilement identifier quel type de croix a été utilisé dans la conversion.
## Étape 6 : Confirmer l’exécution réussie
Enfin, il est toujours judicieux de confirmer que votre opération a réussi. Vous pouvez imprimer un message sur la console :
```csharp
Console.WriteLine("SpecifyHtmlCrossTypeInOutputHTML executed successfully.\r\n");
```
Cela vous permettra de savoir que le processus a été terminé sans aucune erreur.
## Conclusion
Et voilà ! Vous avez spécifié avec succès le type croisé HTML pour votre exportation Excel dans .NET à l'aide d'Aspose.Cells. Cette fonctionnalité est particulièrement utile lorsque vous devez conserver une mise en forme ou des références spécifiques dans votre sortie HTML, garantissant ainsi que vos documents convertis répondent à vos exigences.
## FAQ
### Qu'est-ce que HtmlCrossType dans Aspose.Cells ?  
HtmlCrossType définit la manière dont les références croisées dans le fichier Excel sont gérées lors de la conversion HTML. Vous pouvez choisir des options telles que Default, MSExport, Cross et FitToCell.
### Puis-je utiliser Aspose.Cells gratuitement ?  
 Aspose.Cells propose une version d'essai gratuite. Vous pouvez la télécharger à partir de leur[site web](https://releases.aspose.com/).
### Comment installer Aspose.Cells dans mon projet .NET ?  
 Vous pouvez installer Aspose.Cells via le gestionnaire de packages NuGet dans Visual Studio en exécutant la commande :`Install-Package Aspose.Cells`.
### Où puis-je trouver la documentation d'Aspose.Cells ?  
 Vous pouvez trouver une documentation complète sur Aspose.Cells[ici](https://reference.aspose.com/cells/net/).
### Que dois-je faire si je rencontre une erreur lors de l'enregistrement du fichier HTML ?  
Assurez-vous que les chemins d'accès aux répertoires sont corrects et que vous disposez des autorisations d'écriture pour le répertoire de sortie. Si le problème persiste, consultez le forum d'assistance Aspose pour obtenir de l'aide.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
