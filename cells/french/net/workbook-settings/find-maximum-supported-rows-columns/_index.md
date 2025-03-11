---
title: Rechercher le nombre maximal de lignes et de colonnes prises en charge par les formats XLS et XLSX
linktitle: Rechercher le nombre maximal de lignes et de colonnes prises en charge par les formats XLS et XLSX
second_title: API de traitement Excel Aspose.Cells .NET
description: Découvrez le nombre maximal de lignes et de colonnes prises en charge par les formats XLS et XLSX à l'aide d'Aspose.Cells pour .NET. Optimisez la gestion de vos données Excel avec ce didacticiel complet.
weight: 11
url: /fr/net/workbook-settings/find-maximum-supported-rows-columns/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Rechercher le nombre maximal de lignes et de colonnes prises en charge par les formats XLS et XLSX

## Introduction
Dans le monde d'Excel, la gestion de grands ensembles de données peut être une tâche ardue, en particulier lorsqu'il s'agit de gérer le nombre maximal de lignes et de colonnes prises en charge par différents formats de fichier. Ce didacticiel vous guidera tout au long du processus de recherche du nombre maximal de lignes et de colonnes prises en charge par les formats XLS et XLSX à l'aide de la bibliothèque Aspose.Cells pour .NET. À la fin de cet article, vous aurez une compréhension complète de la manière d'utiliser cet outil puissant pour gérer efficacement vos tâches liées à Excel.
## Prérequis
Avant de plonger dans le didacticiel, assurez-vous que vous disposez des prérequis suivants :
1. [Cadre .NET](https://dotnet.microsoft.com/en-us/download) ou[.NET Core](https://dotnet.microsoft.com/en-us/download) installé sur votre système.
2. [Aspose.Cells pour .NET](https://releases.aspose.com/cells/net/) bibliothèque téléchargée et référencée dans votre projet.
 Si vous ne l'avez pas déjà fait, vous pouvez télécharger la bibliothèque Aspose.Cells pour .NET à partir du[site web](https://releases.aspose.com/cells/net/) ou installez-le via[NuGet](https://www.nuget.org/packages/Aspose.Cells/).
## Paquets d'importation
Pour commencer, vous devez importer les packages nécessaires à partir de la bibliothèque Aspose.Cells pour .NET. Ajoutez les instructions using suivantes en haut de votre fichier C# :
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
## Étape 1 : recherchez le nombre maximal de lignes et de colonnes prises en charge par le format XLS
Commençons par explorer les lignes et colonnes maximales prises en charge par le format XLS (Excel 97-2003).
```csharp
// Imprimer un message sur le format XLS.
Console.WriteLine("Maximum Rows and Columns supported by XLS format.");
// Créer un classeur au format XLS.
Workbook wb = new Workbook(FileFormatType.Excel97To2003);
// Imprimez le nombre maximal de lignes et de colonnes prises en charge par le format XLS.
int maxRows = wb.Settings.MaxRow + 1;
int maxCols = wb.Settings.MaxColumn + 1;
Console.WriteLine("Maximum Rows: " + maxRows);
Console.WriteLine("Maximum Columns: " + maxCols);
Console.WriteLine();
```
Dans cette étape, nous :
1. Imprimez un message pour indiquer que nous travaillons avec le format XLS.
2.  Créer un nouveau`Workbook` exemple utilisant le`FileFormatType.Excel97To2003` enum, qui représente le format XLS.
3.  Récupérez le nombre maximal de lignes et de colonnes prises en charge par le format XLS à l'aide de la`Workbook.Settings.MaxRow` et`Workbook.Settings.MaxColumn`propriétés, respectivement. Nous ajoutons 1 à ces valeurs pour obtenir les nombres de lignes et de colonnes maximum réels (puisqu'ils sont basés sur zéro).
4. Imprimez le nombre maximal de lignes et de colonnes sur la console.
## Étape 2 : recherchez le nombre maximal de lignes et de colonnes prises en charge par le format XLSX
Ensuite, explorons les lignes et colonnes maximales prises en charge par le format XLSX (Excel 2007 et versions ultérieures).
```csharp
// Imprimer un message sur le format XLSX.
Console.WriteLine("Maximum Rows and Columns supported by XLSX format.");
// Créer un classeur au format XLSX.
wb = new Workbook(FileFormatType.Xlsx);
// Imprimez le nombre maximal de lignes et de colonnes prises en charge par le format XLSX.
maxRows = wb.Settings.MaxRow + 1;
maxCols = wb.Settings.MaxColumn + 1;
Console.WriteLine("Maximum Rows: " + maxRows);
Console.WriteLine("Maximum Columns: " + maxCols);
```
Dans cette étape, nous :
1. Imprimez un message pour indiquer que nous travaillons avec le format XLSX.
2.  Créer un nouveau`Workbook` exemple utilisant le`FileFormatType.Xlsx` enum, qui représente le format XLSX.
3.  Récupérez le nombre maximal de lignes et de colonnes prises en charge par le format XLSX à l'aide de la`Workbook.Settings.MaxRow` et`Workbook.Settings.MaxColumn`propriétés, respectivement. Nous ajoutons 1 à ces valeurs pour obtenir les nombres de lignes et de colonnes maximum réels (puisqu'ils sont basés sur zéro).
4. Imprimez le nombre maximal de lignes et de colonnes sur la console.
## Étape 3 : afficher un message de réussite
Enfin, affichons un message de réussite pour indiquer que l'exemple « FindMaximumRowsAndColumnsSupportedByXLSAndXLSXFormats » s'est exécuté avec succès.
```csharp
Console.WriteLine("FindMaximumRowsAndColumnsSupportedByXLSAndXLSXFormats executed successfully.");
```
Cette étape imprime simplement un message de réussite sur la console.
## Conclusion
Dans ce didacticiel, vous avez appris à utiliser la bibliothèque Aspose.Cells pour .NET pour rechercher le nombre maximal de lignes et de colonnes prises en charge par les formats de fichier XLS et XLSX. En comprenant les limites de ces formats, vous pouvez mieux planifier et gérer vos projets basés sur Excel, en vous assurant que vos données s'inscrivent dans les plages prises en charge.
## FAQ
### Quel est le nombre maximal de lignes pris en charge par le format XLS ?
Le nombre maximal de lignes prises en charge par le format XLS (Excel 97-2003) est de 65 536.
### Quel est le nombre maximal de colonnes prises en charge par le format XLS ?
Le nombre maximal de colonnes prises en charge par le format XLS (Excel 97-2003) est de 256.
### Quel est le nombre maximal de lignes pris en charge par le format XLSX ?
Le nombre maximal de lignes prises en charge par le format XLSX (Excel 2007 et versions ultérieures) est de 1 048 576.
### Quel est le nombre maximal de colonnes prises en charge par le format XLSX ?
Le nombre maximal de colonnes prises en charge par le format XLSX (Excel 2007 et versions ultérieures) est de 16 384.
### Puis-je utiliser la bibliothèque Aspose.Cells pour .NET pour travailler avec d’autres formats de fichiers Excel ?
 Oui, la bibliothèque Aspose.Cells pour .NET prend en charge une large gamme de formats de fichiers Excel, notamment XLS, XLSX, ODS, etc. Vous pouvez explorer le[documentation](https://reference.aspose.com/cells/net/) pour en savoir plus sur les fonctionnalités et fonctionnalités disponibles.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
