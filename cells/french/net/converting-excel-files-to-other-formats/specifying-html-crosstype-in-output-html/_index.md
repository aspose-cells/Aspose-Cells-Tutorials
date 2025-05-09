---
"description": "Apprenez à spécifier le CrossType HTML dans Aspose.Cells pour .NET. Suivez notre tutoriel étape par étape pour convertir des fichiers Excel en HTML avec précision."
"linktitle": "Spécification du CrossType HTML dans la sortie HTML par programmation dans .NET"
"second_title": "API de traitement Excel Aspose.Cells .NET"
"title": "Spécification du CrossType HTML dans la sortie HTML par programmation dans .NET"
"url": "/fr/net/converting-excel-files-to-other-formats/specifying-html-crosstype-in-output-html/"
"weight": 17
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Spécification du CrossType HTML dans la sortie HTML par programmation dans .NET

## Introduction
Lors de la conversion de fichiers Excel en HTML dans des applications .NET, vous devrez peut-être spécifier la gestion des références croisées dans la sortie. La classe HtmlSaveOptions d'Aspose.Cells pour .NET propose différents paramètres pour contrôler le processus de conversion, dont l'option HtmlCrossType. Dans ce tutoriel, nous vous expliquerons comment spécifier par programmation le type croisé HTML lors de l'exportation de fichiers Excel au format HTML. 
## Prérequis
Avant de plonger dans le code, assurez-vous de disposer des éléments suivants :
- Aspose.Cells pour .NET : Assurez-vous que la bibliothèque Aspose.Cells est installée dans votre projet. Vous pouvez la télécharger depuis le [Site Web d'Aspose](https://releases.aspose.com/cells/net/).
- Visual Studio : une installation fonctionnelle de Visual Studio ou de tout autre environnement de développement .NET.
- Connaissances de base de C# : une familiarité avec la programmation C# vous aidera à mieux comprendre les exemples.
- Exemple de fichier Excel : Préparez un exemple de fichier Excel. Pour cet exemple, nous utiliserons `sampleHtmlCrossStringType.xlsx`.
## Importer des packages
Pour commencer, vous devez importer les espaces de noms Aspose.Cells nécessaires. Voici comment procéder :
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Décomposons cela étape par étape, afin qu'il vous soit facile de suivre et d'implémenter cette fonctionnalité dans vos propres projets.
## Étape 1 : Définissez vos répertoires source et de sortie
Tout d’abord, vous devez définir les répertoires de votre fichier Excel source et l’endroit où vous souhaitez enregistrer le fichier HTML de sortie.
```csharp
// Répertoire source
string sourceDir = "Your Document Directory";
// Répertoire de sortie
string outputDir = "Your Document Directory";
```
## Étape 2 : Charger l’exemple de fichier Excel
Ensuite, chargez votre exemple de fichier Excel dans un `Workbook` objet. C'est ici que toute la magie commence.
```csharp
// Charger l'exemple de fichier Excel
Workbook wb = new Workbook(sourceDir + "sampleHtmlCrossStringType.xlsx");
```
Ici, remplacez `"Your Document Directory"` avec le chemin d'accès réel de votre fichier Excel. Cette ligne lit le fichier Excel en mémoire pour que vous puissiez le manipuler.
## Étape 3 : Spécifier les options d’enregistrement HTML
Maintenant, nous allons créer une instance de `HtmlSaveOptions`, qui vous permet de configurer la manière dont le fichier Excel sera converti en HTML.
```csharp
// Spécifier le type croisé HTML
HtmlSaveOptions opts = new HtmlSaveOptions();
opts.HtmlCrossStringType = HtmlCrossType.Default;
```
Dans cette étape, nous avons défini le `HtmlCrossStringType` à `HtmlCrossType.Default`, qui est l'une des options disponibles pour gérer les références croisées dans le code HTML de sortie.
## Étape 4 : modifiez le type de croix selon vos besoins
Vous pouvez spécifier différents types pour `HtmlCrossStringType` Selon vos besoins. Voici les différentes options possibles :
- `HtmlCrossType.Default`: Le type de croix par défaut.
- `HtmlCrossType.MSExport`: Exporte le HTML avec un comportement de type MS Excel.
- `HtmlCrossType.Cross`: Crée des références croisées.
- `HtmlCrossType.FitToCell`Ajuste les références croisées aux dimensions de la cellule.
Vous pouvez modifier le `HtmlCrossStringType` comme ça:
```csharp
opts.HtmlCrossStringType = HtmlCrossType.MSExpout;
// ou 
opts.HtmlCrossStringType = HtmlCrossType.Cross;
// or
opts.HtmlCrossStringType = HtmlCrossType.FitToCell;
```
## Étape 5 : Enregistrer le fichier HTML de sortie
Une fois vos options configurées, il est temps d'enregistrer le fichier HTML converti. Utilisez le `Save` méthode sur votre `Workbook` objet:
```csharp
// Sortie HTML
wb.Save(outputDir + "out" + opts.HtmlCrossStringType + ".htm", opts);
```
Ici, nous nommons le fichier de sortie en fonction du `HtmlCrossStringType` Nous avons défini. De cette façon, vous pouvez facilement identifier le type de croix utilisé lors de la conversion.
## Étape 6 : Confirmer l’exécution réussie
Enfin, il est toujours judicieux de confirmer la réussite de l'opération. Vous pouvez afficher un message sur la console :
```csharp
Console.WriteLine("SpecifyHtmlCrossTypeInOutputHTML executed successfully.\r\n");
```
Cela vous permettra de savoir que le processus a été terminé sans aucune erreur.
## Conclusion
Et voilà ! Vous avez correctement spécifié le type croisé HTML pour votre exportation Excel en .NET avec Aspose.Cells. Cette fonctionnalité est particulièrement utile lorsque vous devez conserver une mise en forme ou des références spécifiques dans votre sortie HTML, garantissant ainsi que vos documents convertis répondent à vos exigences.
## FAQ
### Qu'est-ce que HtmlCrossType dans Aspose.Cells ?  
HtmlCrossType définit la gestion des références croisées dans le fichier Excel lors de la conversion HTML. Vous pouvez choisir des options telles que « Par défaut », « Exportation », « Croisé » et « Ajuster à la cellule ».
### Puis-je utiliser Aspose.Cells gratuitement ?  
Aspose.Cells propose une version d'essai gratuite. Vous pouvez la télécharger depuis leur site. [site web](https://releases.aspose.com/).
### Comment installer Aspose.Cells dans mon projet .NET ?  
Vous pouvez installer Aspose.Cells via NuGet Package Manager dans Visual Studio en exécutant la commande : `Install-Package Aspose.Cells`.
### Où puis-je trouver la documentation pour Aspose.Cells ?  
Vous pouvez trouver une documentation complète sur Aspose.Cells [ici](https://reference.aspose.com/cells/net/).
### Que dois-je faire si je rencontre une erreur lors de l’enregistrement du fichier HTML ?  
Assurez-vous que les chemins d'accès aux répertoires sont corrects et que vous disposez des droits d'écriture sur le répertoire de sortie. Si le problème persiste, consultez le forum d'assistance Aspose pour obtenir de l'aide.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}