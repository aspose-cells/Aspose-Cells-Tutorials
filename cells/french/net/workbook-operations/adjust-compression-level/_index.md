---
title: Ajuster le niveau de compression dans le classeur
linktitle: Ajuster le niveau de compression dans le classeur
second_title: API de traitement Excel Aspose.Cells .NET
description: Découvrez comment ajuster le niveau de compression des classeurs Excel à l'aide d'Aspose.Cells pour .NET grâce à ce guide étape par étape. Optimisez votre gestion de fichiers.
weight: 14
url: /fr/net/workbook-operations/adjust-compression-level/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ajuster le niveau de compression dans le classeur

## Introduction
Lorsqu'il s'agit de gérer des fichiers Excel volumineux, la compression est un élément clé. Non seulement elle permet d'économiser de l'espace de stockage, mais elle rend également les transferts de fichiers plus rapides et plus efficaces. Si vous travaillez avec Aspose.Cells pour .NET, vous pouvez facilement ajuster le niveau de compression de vos classeurs. Dans ce guide, nous vous guiderons pas à pas tout au long du processus, en veillant à ce que vous compreniez chaque partie du code et son fonctionnement.
## Prérequis
Avant de plonger dans le code, vous devez mettre en place quelques prérequis :
1. Connaissances de base de C# : la familiarité avec la programmation C# vous aidera à mieux comprendre les extraits de code.
2.  Bibliothèque Aspose.Cells : vous devez avoir installé la bibliothèque Aspose.Cells. Vous pouvez la télécharger à partir de[ici](https://releases.aspose.com/cells/net/).
3. Visual Studio : Un environnement de développement comme Visual Studio sera nécessaire pour exécuter le code.
4. .NET Framework : assurez-vous que votre projet est configuré avec une version compatible du .NET Framework.
## Paquets d'importation
Pour commencer, vous devez importer les packages nécessaires dans votre projet C#. Voici comment procéder :
```csharp
using Aspose.Cells.Rendering;
using Aspose.Cells.WebExtensions;
using System;
```
 Ces packages sont essentiels pour travailler avec des fichiers Excel à l'aide de la bibliothèque Aspose.Cells.`Aspose.Cells` L'espace de noms contient toutes les classes dont vous avez besoin pour manipuler les fichiers Excel, tandis que`Aspose.Cells.Xlsb` fournit les options permettant d'enregistrer des fichiers au format XLSB.
Décomposons maintenant le processus de réglage du niveau de compression dans un classeur en étapes gérables.
## Étape 1 : définir les répertoires source et de sortie
Tout d'abord, vous devez spécifier où se trouvent vos fichiers sources et où vous souhaitez enregistrer les fichiers de sortie. Cela est essentiel pour garantir que votre programme sait où trouver les fichiers avec lesquels il doit travailler.
```csharp
// Répertoire des sources
string sourceDir = "Your Document Directory";
string outDir = "Your Document Directory";
```
 Remplacer`"Your Document Directory"` avec le chemin réel vers vos répertoires. Cela aidera le programme à localiser les fichiers que vous souhaitez compresser.
## Étape 2 : charger le classeur
Ensuite, vous chargez le classeur que vous souhaitez compresser. C'est là que la magie commence !
```csharp
Workbook workbook = new Workbook(sourceDir + "LargeSampleFile.xlsx");
```
Dans cette ligne, nous créons une nouvelle instance de la`Workbook` classez et chargez un fichier Excel existant. Assurez-vous que le nom du fichier correspond à celui que vous avez dans votre répertoire source.
## Étape 3 : Configurer les options d’enregistrement
Il est maintenant temps de configurer les options de sauvegarde. Nous allons définir le type de compression pour le fichier de sortie. 
```csharp
XlsbSaveOptions options = new XlsbSaveOptions();
```
 Le`XlsbSaveOptions` La classe vous permet de spécifier diverses options lors de l'enregistrement de votre classeur au format XLSB, y compris les niveaux de compression.
## Étape 4 : Mesurer le temps de compression pour le niveau 1
Commençons par le premier niveau de compression. Nous allons mesurer le temps nécessaire pour enregistrer le classeur avec ce niveau de compression.
```csharp
options.CompressionType = OoxmlCompressionType.Level1;
var watch = Stopwatch.StartNew();
workbook.Save(outDir + "LargeSampleFile_level_1_out.xlsb", options);
watch.Stop();
var elapsedMs = watch.ElapsedMilliseconds;
Console.WriteLine("Level 1 Elapsed Time: " + elapsedMs);
```
Ici, nous définissons le type de compression sur Niveau 1, enregistrons le classeur, puis mesurons le temps écoulé. Cela nous donne une idée de la durée du processus.
## Étape 5 : Mesurer le temps de compression pour le niveau 6
Voyons ensuite comment fonctionne la compression de niveau 6.
```csharp
watch = Stopwatch.StartNew();
options.CompressionType = OoxmlCompressionType.Level6;
workbook.Save(outDir + "LargeSampleFile_level_6_out.xlsb", options);
watch.Stop();
elapsedMs = watch.ElapsedMilliseconds;
Console.WriteLine("Level 6 Elapsed Time: " + elapsedMs);
```
Cette étape est similaire à la précédente, mais nous changeons le niveau de compression au niveau 6. Vous remarquerez que le temps nécessaire peut varier en fonction de la complexité du classeur.
## Étape 6 : Mesurer le temps de compression pour le niveau 9
Enfin, vérifions les performances avec le niveau de compression le plus élevé.
```csharp
watch = Stopwatch.StartNew();
options.CompressionType = OoxmlCompressionType.Level9;
workbook.Save(outDir + "LargeSampleFile_level_9_out.xlsb", options);
watch.Stop();
elapsedMs = watch.ElapsedMilliseconds;
Console.WriteLine("Level 9 Elapsed Time: " + elapsedMs);
```
Dans cette étape, nous définissons le niveau de compression sur le niveau 9. C'est là que vous verrez généralement la réduction la plus significative de la taille du fichier, mais le traitement peut prendre plus de temps.
## Étape 7 : Résultat final
Après avoir exécuté tous les niveaux de compression, vous pouvez afficher un message indiquant que le processus s'est terminé avec succès.
```csharp
Console.WriteLine("AdjustCompressionLevel executed successfully.");
```
Cette simple ligne de code confirme que votre programme a terminé son exécution sans aucun problème.
## Conclusion
Le réglage du niveau de compression de vos classeurs à l'aide d'Aspose.Cells pour .NET est un processus simple qui peut apporter des avantages significatifs en termes de taille de fichier et de performances. En suivant les étapes décrites dans ce guide, vous pouvez facilement implémenter la compression dans vos applications et améliorer l'efficacité de votre gestion de fichiers Excel.
## FAQ
### Qu'est-ce qu'Aspose.Cells ?  
Aspose.Cells est une bibliothèque puissante pour .NET qui permet aux développeurs de créer, manipuler et convertir des fichiers Excel sans avoir besoin de Microsoft Excel.
### Comment installer Aspose.Cells ?  
 Vous pouvez télécharger et installer Aspose.Cells à partir du[Site Web d'Aspose](https://releases.aspose.com/cells/net/).
### Quels niveaux de compression sont disponibles ?  
Aspose.Cells prend en charge plusieurs niveaux de compression allant du niveau 1 (compression la plus faible) au niveau 9 (compression la plus élevée).
### Puis-je tester Aspose.Cells gratuitement ?  
 Oui ! Vous pouvez obtenir un essai gratuit d'Aspose.Cells[ici](https://releases.aspose.com/).
### Où puis-je trouver du support pour Aspose.Cells ?  
 Pour toute question ou assistance, vous pouvez visiter le forum d'assistance Aspose[ici](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
