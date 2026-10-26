---
category: general
date: 2026-10-26
description: Apprenez comment définir un format de nombre personnalisé dans un fichier
  Excel en C# en configurant les chiffres significatifs, en créant un classeur Excel
  et en l’enregistrant au format XLSX.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- custom number format excel
- set significant digits
- how to set number format
- create excel workbook c#
- save workbook xlsx
language: fr
lastmod: 2026-10-26
og_description: Le format de nombre personnalisé Excel en C# vous permet de contrôler
  les chiffres significatifs, de créer un classeur Excel et de l’enregistrer au format
  XLSX. Suivez ce tutoriel complet.
og_image_alt: Excel cell A1 displaying a number formatted with 4 significant digits
  using C#
og_title: Format de nombre personnalisé Excel en C# – guide étape par étape
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to set a custom number format excel file in C# by configuring
    significant digits, creating an Excel workbook, and saving it as an XLSX document.
  headline: How to apply a custom number format excel in C#
  type: TechArticle
- description: Learn how to set a custom number format excel file in C# by configuring
    significant digits, creating an Excel workbook, and saving it as an XLSX document.
  name: How to apply a custom number format excel in C#
  steps:
  - name: Using a custom format string instead of global options
    text: 'If you need a format that applies only to a single range, you can assign
      a format string directly:'
  - name: Applying the setting to an entire column
    text: '```csharp // Apply the same significant‑digit rule to column B ws.Cells.Columns[1].ApplyNumberFormatOptions(
      new NumberFormatOptions { SignificantDigits = 4 }); ```'
  - name: Dealing with negative numbers
    text: 'The global `SignificantDigits` option works uniformly for positive and
      negative numbers. If you want a different display for negatives, combine it
      with a custom format:'
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: Comment appliquer un format de nombre personnalisé dans Excel avec C#
url: /fr/net/excel-custom-number-date-formatting/how-to-apply-a-custom-number-format-excel-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment appliquer un format de nombre personnalisé Excel en C#

Si vous avez besoin d’un **format de nombre personnalisé Excel** qui affiche un nombre précis de chiffres significatifs, ce guide vous montre exactement comment le faire en C#. Vous verrez comment définir les chiffres significatifs, créer un classeur Excel et enregistrer le classeur au format XLSX — le tout en quelques lignes de code.

Travailler avec des fichiers Excel de façon programmatique signifie souvent que vous devez contrôler l’apparence des nombres. En utilisant Aspose.Cells pour .NET, vous pouvez définir une option globale de format de nombre qui oblige chaque cellule numérique à respecter un nombre donné de chiffres significatifs. Ce tutoriel couvre le flux complet, de la configuration du projet à la vérification du résultat dans Excel.

## Prérequis

Avant de commencer, assurez-vous d’avoir :

* .NET 6.0 ou version ultérieure installé (le code fonctionne également avec .NET Framework 4.7.2+)
* Visual Studio 2022 ou tout autre IDE C# de votre choix
* Le package NuGet **Aspose.Cells** (`Install-Package Aspose.Cells`) – une bibliothèque entièrement gérée pour la manipulation d’Excel
* Une connaissance de base de la syntaxe C#

## Étape 1 : Créer un classeur Excel en C#

La première opération consiste à instancier un nouvel objet `Workbook`. Cet objet représente l’ensemble du fichier Excel en mémoire.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook instance
        Workbook wb = new Workbook();

        // The workbook now contains a default worksheet named "Sheet1"
        // You can access it via the Worksheets collection.
        Worksheet ws = wb.Worksheets[0];
```

**Pourquoi c’est important :** `Workbook` est le point d’entrée de chaque opération Excel. En le créant d’abord, vous garantissez un fichier propre que vous pourrez ensuite enregistrer au format XLSX.

## Étape 2 : Configurer le format de nombre pour définir les chiffres significatifs

Aspose.Cells fournit un paramètre global appelé `NumberFormatOptions`. En assignant `SignificantDigits = 4`, chaque cellule numérique affichera jusqu’à quatre chiffres significatifs, sauf si un format plus spécifique la remplace.

```csharp
        // Step 2: Set the global number‑format option to 4 significant digits
        WorkbookSettings.SetNumberFormatOptions(
            new NumberFormatOptions { SignificantDigits = 4 });
```

**Pourquoi c’est important :** Utiliser `SetNumberFormatOptions` vous permet de définir un **format de nombre personnalisé Excel** sans écrire une chaîne de format pour chaque cellule. Cela reproduit l’option « Chiffres significatifs » que l’on trouve dans le dialogue *Format de cellule → Nombre → Personnalisé* d’Excel.

## Étape 3 : Écrire des valeurs et vérifier le format de nombre personnalisé

Placez maintenant une valeur numérique dans une cellule. Le paramètre global appliquera automatiquement la règle des 4 chiffres.

```csharp
        // Step 3: Write a numeric value into cell A1 (row 0, column 0)
        ws.Cells[0, 0].PutValue(123.456789);

        // Optional: Add a label so you can see the effect in Excel
        ws.Cells[0, 1].PutValue("Original value:");
        ws.Cells[0, 2].PutValue(123.456789);
```

Lorsque vous ouvrez le fichier enregistré, la cellule **A1** affichera `123.5` (arrondi à quatre chiffres significatifs). La valeur d’origine reste inchangée dans les données sous‑jacentes, ce que vous pouvez confirmer en regardant la barre de formule.

**Astuce pour les cas limites :** Si vous stockez un nombre très grand comme `12345678.9`, le même paramètre affichera `1.235E+07` (notation scientifique) parce qu’Excel choisit la représentation la plus compacte tout en conservant quatre chiffres significatifs.

## Étape 4 : Enregistrer le classeur au format XLSX

Enfin, persistez le classeur sur le disque. La méthode `Save` choisit automatiquement le format de fichier en fonction de l’extension.

```csharp
        // Step 4: Save the workbook to an XLSX file
        string outputPath = @"C:\Temp\SigDigits.xlsx";
        wb.Save(outputPath);

        // Inform the user
        System.Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

**Pourquoi c’est important :** Enregistrer au format **XLSX** (`save workbook xlsx`) garantit une compatibilité maximale avec les versions récentes d’Excel, Office 365 et d’autres outils de tableur.

## Résultat attendu

Ouvrez *C:\Temp\SigDigits.xlsx* dans Microsoft Excel. Vous devriez voir :

| A          | B                     | C                |
|------------|-----------------------|------------------|
| **123.5**  | Valeur d'origine :    | **123.456789**   |

*Cellule A1* montre le nombre arrondi à quatre chiffres significatifs, tandis que *C1* conserve la précision complète pour la comparaison.

## Variations courantes et comment définir le format de nombre pour des cellules spécifiques

### Utiliser une chaîne de format personnalisée au lieu d’options globales

Si vous avez besoin d’un format qui ne s’applique qu’à une seule plage, vous pouvez assigner directement une chaîne de format :

```csharp
ws.Cells["D1"].PutValue(0.0012345);
Style style = wb.CreateStyle();
style.Custom = "0.####"; // shows up to 4 decimal places, not significant digits
ws.Cells["D1"].SetStyle(style);
```

### Appliquer le paramètre à une colonne entière

```csharp
// Apply the same significant‑digit rule to column B
ws.Cells.Columns[1].ApplyNumberFormatOptions(
    new NumberFormatOptions { SignificantDigits = 4 });
```

### Gérer les nombres négatifs

L’option globale `SignificantDigits` fonctionne de la même façon pour les nombres positifs et négatifs. Si vous souhaitez un affichage différent pour les négatifs, combinez‑la avec un format personnalisé :

```csharp
Style negStyle = wb.CreateStyle();
negStyle.Custom = "#,##0.###;[Red]-#,##0.###";
ws.Cells["E1"].PutValue(-9876.54321);
ws.Cells["E1"].SetStyle(negStyle);
```

## Astuces professionnelles et pièges

* **Astuce pro :** Définissez les options de format de nombre **avant** d’écrire des données. Modifier l’option après avoir rempli les cellules ne reformate pas rétroactivement les valeurs existantes.
* **Attention à :** Utiliser `PutValue` avec une **chaîne** qui ressemble à un nombre (par ex., `"123.45"`). Excel la traitera comme du texte, et le format personnalisé ne s’appliquera pas.
* **Note de performance :** Les paramètres globaux sont peu coûteux, mais appliquer un style à des millions de cellules peut augmenter l’utilisation de la mémoire. Utilisez le formatage au niveau de la colonne lorsque c’est possible.

## Prochaines étapes

Maintenant que vous pouvez **formater des nombres personnalisés Excel** avec des chiffres significatifs, vous pourriez explorer :

* **Comment définir le format de nombre** pour les dates et les devises avec `Style.Custom`.
* **Créer des graphiques** qui respectent vos formats personnalisés.
* **Exporter en CSV** tout en préservant la précision numérique (`save workbook xlsx` → `wb.Save("file.csv", SaveFormat.Csv)`).

Ces sujets s’appuient sur les mêmes concepts `Workbook` et `Worksheet` présentés ici.

---

**Résumé**

Vous avez appris à **formater des nombres personnalisés Excel** en configurant `NumberFormatOptions` pour **définir les chiffres significatifs**, créer un classeur Excel en C#, écrire des valeurs et **enregistrer le classeur au format XLSX**. Le code complet et exécutable ci‑dessus montre chaque étape, explique pourquoi chaque partie est nécessaire et fournit des conseils pour les variations courantes. N’hésitez pas à adapter les extraits à vos propres projets et à expérimenter d’autres scénarios de formatage.

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants abordent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser d’autres fonctionnalités de l’API et à explorer des approches d’implémentation alternatives dans vos projets.

- [Custom Number Format Excel in C# – Complete Guide](/cells/english/net/excel-custom-number-date-formatting/custom-number-format-excel-in-c-complete-guide/)
- [Create Excel Workbook C# – Limit Significant Digits Excel](/cells/english/net/excel-custom-number-date-formatting/create-excel-workbook-c-limit-significant-digits-excel/)
- [How to apply number format excel with Aspose.Cells](/cells/english/net/excel-custom-number-date-formatting/how-to-apply-number-format-excel-with-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}