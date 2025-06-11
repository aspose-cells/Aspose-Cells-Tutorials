---
"description": "Découvrez le nombre maximal de lignes et de colonnes prises en charge par les formats XLS et XLSX grâce à Aspose.Cells pour .NET. Optimisez la gestion de vos données Excel grâce à ce tutoriel complet."
"linktitle": "Trouver le nombre maximal de lignes et de colonnes prises en charge par les formats XLS et XLSX"
"second_title": "API de traitement Excel Aspose.Cells .NET"
"title": "Trouver le nombre maximal de lignes et de colonnes prises en charge par les formats XLS et XLSX"
"url": "/fr/net/workbook-settings/find-maximum-supported-rows-columns/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Trouver le nombre maximal de lignes et de colonnes prises en charge par les formats XLS et XLSX

## Introduction
Dans Excel, gérer de grands ensembles de données peut s'avérer complexe, notamment lorsqu'il s'agit de gérer le nombre maximal de lignes et de colonnes pris en charge par les différents formats de fichiers. Ce tutoriel vous guidera dans la recherche du nombre maximal de lignes et de colonnes prises en charge par les formats XLS et XLSX à l'aide de la bibliothèque Aspose.Cells pour .NET. À la fin de cet article, vous maîtriserez parfaitement l'utilisation de cet outil puissant pour gérer efficacement vos tâches Excel.
## Prérequis
Avant de plonger dans le didacticiel, assurez-vous que vous disposez des prérequis suivants :
1. [.NET Framework](https://dotnet.microsoft.com/en-us/download) ou [.NET Core](https://dotnet.microsoft.com/en-us/download) installé sur votre système.
2. [Aspose.Cells pour .NET](https://releases.aspose.com/cells/net/) bibliothèque téléchargée et référencée dans votre projet.
Si vous ne l'avez pas déjà fait, vous pouvez télécharger la bibliothèque Aspose.Cells pour .NET à partir du [site web](https://releases.aspose.com/cells/net/) ou installez-le via [NuGet](https://www.nuget.org/packages/Aspose.Cells/).
## Importer des packages
Pour commencer, vous devez importer les packages nécessaires depuis la bibliothèque Aspose.Cells pour .NET. Ajoutez les instructions using suivantes en haut de votre fichier C# :
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
## Étape 1 : Trouver le nombre maximal de lignes et de colonnes prises en charge par le format XLS
Commençons par explorer le nombre maximal de lignes et de colonnes prises en charge par le format XLS (Excel 97-2003).
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
2. Créer un nouveau `Workbook` exemple en utilisant le `FileFormatType.Excel97To2003` enum, qui représente le format XLS.
3. Récupérez le nombre maximal de lignes et de colonnes prises en charge par le format XLS à l'aide de la `Workbook.Settings.MaxRow` et `Workbook.Settings.MaxColumn` propriétés, respectivement. Nous ajoutons 1 à ces valeurs pour obtenir le nombre maximal réel de lignes et de colonnes (puisqu'elles sont basées sur zéro).
4. Imprimez le nombre maximal de lignes et de colonnes sur la console.
## Étape 2 : Trouver le nombre maximal de lignes et de colonnes prises en charge par le format XLSX
Ensuite, explorons le nombre maximal de lignes et de colonnes prises en charge par le format XLSX (Excel 2007 et versions ultérieures).
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
2. Créer un nouveau `Workbook` exemple en utilisant le `FileFormatType.Xlsx` enum, qui représente le format XLSX.
3. Récupérez le nombre maximal de lignes et de colonnes prises en charge par le format XLSX à l'aide de la `Workbook.Settings.MaxRow` et `Workbook.Settings.MaxColumn` propriétés, respectivement. Nous ajoutons 1 à ces valeurs pour obtenir le nombre maximal réel de lignes et de colonnes (puisqu'elles sont basées sur zéro).
4. Imprimez le nombre maximal de lignes et de colonnes sur la console.
## Étape 3 : afficher un message de réussite
Enfin, affichons un message de réussite pour indiquer que l'exemple « FindMaximumRowsAndColumnsSupportedByXLSAndXLSXFormats » s'est exécuté avec succès.
```csharp
Console.WriteLine("FindMaximumRowsAndColumnsSupportedByXLSAndXLSXFormats executed successfully.");
```
Cette étape imprime simplement un message de réussite sur la console.
## Conclusion
Dans ce tutoriel, vous avez appris à utiliser la bibliothèque Aspose.Cells pour .NET afin de déterminer le nombre maximal de lignes et de colonnes pris en charge par les formats de fichier XLS et XLSX. En comprenant les limites de ces formats, vous pourrez mieux planifier et gérer vos projets Excel, en vous assurant que vos données respectent les plages prises en charge.
## FAQ
### Quel est le nombre maximal de lignes prises en charge par le format XLS ?
Le nombre maximal de lignes prises en charge par le format XLS (Excel 97-2003) est de 65 536.
### Quel est le nombre maximal de colonnes prises en charge par le format XLS ?
Le nombre maximal de colonnes prises en charge par le format XLS (Excel 97-2003) est de 256.
### Quel est le nombre maximal de lignes prises en charge par le format XLSX ?
Le nombre maximal de lignes prises en charge par le format XLSX (Excel 2007 et versions ultérieures) est de 1 048 576.
### Quel est le nombre maximal de colonnes prises en charge par le format XLSX ?
Le nombre maximal de colonnes prises en charge par le format XLSX (Excel 2007 et versions ultérieures) est de 16 384.
### Puis-je utiliser la bibliothèque Aspose.Cells pour .NET pour travailler avec d’autres formats de fichiers Excel ?
Oui, la bibliothèque Aspose.Cells pour .NET prend en charge un large éventail de formats de fichiers Excel, notamment XLS, XLSX, ODS, etc. Vous pouvez explorer [documentation](https://reference.aspose.com/cells/net/) pour en savoir plus sur les fonctionnalités et fonctionnalités disponibles.


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}