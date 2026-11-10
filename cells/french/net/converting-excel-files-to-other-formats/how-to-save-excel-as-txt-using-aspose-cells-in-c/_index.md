---
category: general
date: 2026-10-13
description: Apprenez à enregistrer Excel au format TXT avec Aspose.Cells. Ce guide
  couvre l'exportation d'Excel en TXT, l'écriture de valeurs dans une cellule et la
  définition des chiffres significatifs en quelques étapes seulement.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save excel as txt
- export excel to txt
- write value to cell
- set significant digits
- export spreadsheet as txt
language: fr
lastmod: 2026-10-13
og_description: Enregistrez Excel au format TXT avec Aspose.Cells. Apprenez à exporter
  Excel en TXT, à écrire une valeur dans une cellule et à définir les chiffres significatifs
  en quelques lignes de code C#.
og_image_alt: Screenshot showing a workbook saved as a TXT file using save excel as
  txt
og_title: Enregistrer Excel au format TXT – guide pas à pas pour les développeurs
  .NET
schemas:
- author: Aspose
  dateModified: '2026-10-13'
  description: Learn how to save Excel as TXT with Aspose.Cells. This guide covers
    export Excel to TXT, write value to cell, and set significant digits in just a
    few steps.
  headline: How to save Excel as TXT using Aspose.Cells in C#
  type: TechArticle
- questions:
  - answer: It rounds to the nearest value based on the specified number of significant
      digits, ensuring the output is mathematically accurate to that precision.
    question: Does `SignificantDigits` round or truncate?
  - answer: 'Yes. Replace the file path with a `MemoryStream` instance: `workbook.Save(stream,
      txtOptions);`. This is handy for web APIs that need to return the TXT content
      without touching the file system.'
    question: Can I export directly to a memory stream?
  - answer: 'Use `txtOptions.ExportFormattedValues = true`. This forces Aspose.Cells
      to write the cell’s displayed text rather than the raw value. ## Conclusion
      You now know how to **save Excel as TXT** with full control over precision,
      formatting, and output location. By following the four steps—create a workbo'
    question: What if I need to keep the original formatting (e.g., dates)?
  type: FAQPage
tags:
- Excel
- TXT
- Aspose.Cells
- .NET
title: Comment enregistrer un fichier Excel au format TXT avec Aspose.Cells en C#
url: /fr/net/converting-excel-files-to-other-formats/how-to-save-excel-as-txt-using-aspose-cells-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment enregistrer Excel au format TXT avec Aspose.Cells en C#

Si vous devez **enregistrer Excel au format TXT** rapidement, ce tutoriel montre le processus complet en moins de cinq minutes. Vous verrez comment exporter Excel vers TXT, écrire une valeur dans une cellule et définir les chiffres significatifs afin que le fichier texte contienne exactement les données attendues.

Exporter une feuille de calcul au format TXT est utile lorsque les systèmes en aval n'acceptent que des entrées en texte brut, lorsque vous devez générer des journaux, ou lorsque vous souhaitez un vidage lisible par l'homme des calculs. L'exemple ci‑dessous fonctionne avec Aspose.Cells v25.10 ou ultérieur et s'exécute sur n'importe quel runtime .NET 6+.

## Prérequis

* Une copie sous licence de **Aspose.Cells for .NET** (l'essai gratuit fonctionne pour les tests).
* Le SDK .NET 6 ou une version ultérieure installé.
* Un IDE tel que Visual Studio 2022, VS Code ou Rider.
* Des connaissances de base en C# — aucune expérience avancée en automatisation Excel requise.

Vous pouvez installer le package NuGet Aspose.Cells avec :

```bash
dotnet add package Aspose.Cells
```

## Étape 1 : Créer un classeur et accéder à sa première feuille de calcul (enregistrer Excel au format txt)

La première chose à faire lorsque vous souhaitez **enregistrer Excel au format TXT** est de créer un objet `Workbook`. Cet objet représente l'intégralité du fichier Excel en mémoire.

```csharp
using Aspose.Cells;

// Create a new workbook (an empty Excel file)
Workbook workbook = new Workbook();

// Access the first worksheet (index 0)
Worksheet worksheet = workbook.Worksheets[0];
```

> **Pourquoi c'est important :** La classe `Workbook` est le point d'entrée pour toutes les opérations de feuille de calcul. En commençant avec un classeur vierge, vous évitez tout formatage caché qui pourrait affecter la sortie en texte brut.

## Étape 2 : Écrire un nombre à haute précision dans une cellule (write value to cell)

Vous devez maintenant **write value to cell** A1. La méthode `PutValue` détecte automatiquement le type de données et le stocke comme une valeur numérique.

```csharp
// Write a high‑precision number into cell A1
worksheet.Cells["A1"].PutValue(12345.6789012345);
```

> **Astuce :** Si vous devez plus tard écrire des chaînes, des dates ou des formules, la même méthode `PutValue` fonctionne — il suffit de passer le type .NET approprié.

## Étape 3 : Configurer les options d'exportation pour ne conserver que la précision nécessaire (set significant digits)

Lors de l'exportation vers un fichier TXT, vous souhaitez souvent limiter le nombre de chiffres afin de réduire la taille du fichier ou de correspondre à une spécification en aval. La classe `TxtSaveOptions` fournit une propriété `SignificantDigits` à cet effet.

```csharp
// Configure TXT save options to retain only 6 significant digits
TxtSaveOptions txtSaveOptions = new TxtSaveOptions(SaveFormat.Txt)
{
    SignificantDigits = 6   // New option in v25.10
};
```

> **Pourquoi vous devez définir les chiffres significatifs :** Sans ce réglage, Aspose.Cells écrit la valeur en double précision complète, ce qui peut produire de longues chaînes comme `12345.6789012345`. En définissant `SignificantDigits = 6`, la sortie est réduite à `12345.7`, ce qui correspond à la plupart des exigences de reporting.

## Étape 4 : Exporter le classeur en fichier TXT (export excel to txt)

Enfin, vous **exportez Excel vers TXT** en appelant `Workbook.Save` avec les options configurées précédemment.

```csharp
// Save the workbook as a TXT file using the configured options
string outputPath = @"C:\Temp\LimitedDigits.txt";
workbook.Save(outputPath, txtSaveOptions);
```

Lorsque le code se termine, `LimitedDigits.txt` contient :

```
12345.7
```

> **Vérification du résultat :** Ouvrez le fichier dans n'importe quel éditeur de texte (Notepad, VS Code) pour confirmer que seules six chiffres significatifs sont présents et qu'aucune virgule ou délimiteur de tabulation supplémentaire n'apparaît.

## Exemple complet, exécutable

Voici une application console autonome que vous pouvez copier, coller et exécuter immédiatement.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToTxtDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create workbook and get the first worksheet
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];

            // 2️⃣ Write a high‑precision number to cell A1
            worksheet.Cells["A1"].PutValue(12345.6789012345);

            // 3️⃣ Set up TXT save options with 6 significant digits
            TxtSaveOptions txtOptions = new TxtSaveOptions(SaveFormat.Txt)
            {
                SignificantDigits = 6
            };

            // 4️⃣ Save as TXT
            string path = @"C:\Temp\LimitedDigits.txt";
            workbook.Save(path, txtOptions);

            Console.WriteLine($"Workbook exported to TXT at: {path}");
        }
    }
}
```

**Explication de chaque bloc**

| Bloc | Objectif |
|------|----------|
| `using Aspose.Cells;` | Importe l'espace de noms Aspose.Cells requis pour `Workbook`, `Worksheet` et `TxtSaveOptions`. |
| `Workbook workbook = new Workbook();` | Instancie un classeur Excel vide en mémoire. |
| `worksheet.Cells["A1"].PutValue(...);` | **write value to cell** A1 avec un nombre en double précision. |
| `TxtSaveOptions` | Configure le comportement **set significant digits** pour l'exportation TXT. |
| `workbook.Save(..., txtOptions);` | Exécute l'opération **export excel to txt**, créant le fichier texte brut. |

## Cas limites et conseils supplémentaires

| Scénario | Comment gérer |
|----------|---------------|
| **Large worksheets** (many rows/columns) | Utilisez `txtOptions.Encoding = Encoding.UTF8` si vous avez besoin du support Unicode, et envisagez de diffuser le fichier avec `Workbook.Save(Stream, txtOptions)` pour éviter une forte consommation de mémoire. |
| **Custom delimiters** (comma‑separated values) | `TxtSaveOptions` expose également `Separator` — réglez-le sur `','` pour produire une sortie de type CSV tout en restant au format TXT. |
| **Preserving formulas** | Définissez `txtOptions.ExportFormulas = true` pour écrire le texte de la formule au lieu de la valeur calculée. |
| **Locale‑specific decimal separators** | Ajustez `txtOptions.DecimalSeparator` à `','` pour les paramètres régionaux européens. |
| **Multiple worksheets** | Parcourez `workbook.Worksheets` et appelez `Save` pour chaque feuille, en ajoutant le nom de la feuille au nom du fichier. |

## Questions fréquemment posées

**Q : `SignificantDigits` arrondit‑il ou tronque‑il ?**  
R : Il arrondit à la valeur la plus proche en fonction du nombre de chiffres significatifs spécifié, garantissant que la sortie est mathématiquement exacte à cette précision.

**Q : Puis‑je exporter directement vers un flux mémoire ?**  
R : Oui. Remplacez le chemin du fichier par une instance `MemoryStream` : `workbook.Save(stream, txtOptions);`. Cela est pratique pour les API web qui doivent renvoyer le contenu TXT sans toucher au système de fichiers.

**Q : Et si je dois conserver le formatage original (par ex., les dates) ?**  
R : Utilisez `txtOptions.ExportFormattedValues = true`. Cela oblige Aspose.Cells à écrire le texte affiché de la cellule plutôt que la valeur brute.

## Conclusion

Vous savez maintenant comment **enregistrer Excel au format TXT** avec un contrôle complet sur la précision, le formatage et l'emplacement de sortie. En suivant les quatre étapes — créer un classeur, **write value to cell**, **set significant digits**, et **export Excel to TXT** — vous pouvez intégrer l'exportation en texte brut dans n'importe quelle application .NET.

Ensuite, explorez des sujets connexes tels que **export spreadsheet as TXT with custom delimiters**, **convert Excel to CSV**, ou **use Aspose.Cells to generate JSON reports**. Chacun de ces sujets s'appuie sur les mêmes concepts de base présentés ici, vous offrant une boîte à outils polyvalente pour l'échange de données entre plateformes.

Bon codage !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d'implémentation alternatives dans vos propres projets.

- [Enregistrer Excel en texte – Guide complet C# pour exporter Excel en TXT](/cells/english/net/converting-excel-files-to-other-formats/save-excel-as-text-complete-c-guide-to-export-excel-to-txt/)
- [Créer un nouveau classeur et exporter Excel en TXT avec précision](/cells/english/net/excel-data-export-retrieval/create-new-workbook-and-export-excel-to-txt-with-precision/)
- [Créer un nouveau classeur – Exporter Excel en TXT avec pleine précision](/cells/english/net/converting-excel-files-to-other-formats/create-new-workbook-export-excel-to-txt-with-full-precision/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}