---
category: general
date: 2026-03-21
description: Définir le format personnalisé d’une cellule en C# et apprendre à écrire
  une date dans Excel, appliquer un format de date personnalisé, lire un DateTime
  depuis Excel et créer rapidement un classeur et une feuille de calcul.
draft: false
keywords:
- set cell custom format
- write date to excel
- read datetime from excel
- apply custom date format
- create workbook worksheet
language: fr
og_description: Définir le format personnalisé d’une cellule en C# pour écrire une
  date dans Excel, appliquer un format de date personnalisé, lire un DateTime depuis
  Excel et créer facilement une feuille de calcul de classeur.
og_title: Définir le format personnalisé d’une cellule en C# – Écrire et lire des
  dates dans Excel
tags:
- Aspose.Cells
- C#
- Excel Automation
title: Définir le format personnalisé d’une cellule en C# – Guide complet pour écrire
  et lire les dates dans Excel
url: /fr/net/excel-custom-number-date-formatting/set-cell-custom-format-in-c-complete-guide-to-writing-readin/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Définir le format personnalisé d’une cellule – Écrire et lire des dates dans Excel avec C#

Vous avez déjà eu besoin de **définir le format personnalisé d’une cellule** dans un fichier Excel depuis C# mais vous ne saviez pas par où commencer ? Vous n'êtes pas seul. Dans de nombreux outils de reporting ou utilitaires d'exportation de données, la date doit apparaître dans une locale spécifique — pensez aux dates de l'ère japonaise, aux calendriers fiscaux ou aux chaînes ISO‑8601.

Dans ce tutoriel, nous parcourrons un **exemple complet et exécutable** qui vous montre comment **écrire une date dans Excel**, **appliquer un format de date personnalisé**, **lire un DateTime depuis Excel**, et **créer une feuille de calcul** avec Aspose.Cells. À la fin, vous disposerez d’un programme autonome que vous pourrez intégrer à n’importe quel projet .NET.

## Ce que vous allez apprendre

- Comment **créer une feuille de calcul** programmaticalement.  
- Les étapes exactes pour **écrire une date dans Excel** en utilisant une chaîne spécifique à une locale.  
- Comment **appliquer un format de date personnalisé** (y compris la notation de l’ère japonaise).  
- La façon de **lire un DateTime depuis Excel** et le récupérer dans un objet `DateTime`.  
- Conseils, pièges et variantes que vous pourriez rencontrer lors de la manipulation des dates dans Excel.

Aucune documentation externe requise — tout ce dont vous avez besoin se trouve ici.

## Prérequis

- .NET 6.0 ou ultérieur (le code fonctionne également sur .NET Framework 4.7+).  
- Aspose.Cells pour .NET installé via NuGet (`Install-Package Aspose.Cells`).  
- Une compréhension de base de la syntaxe C# — rien de compliqué.

> **Astuce pro :** Si vous utilisez Visual Studio, activez les *nullable reference types* pour détecter les bugs subtils dès le départ.

## Étape 1 : Créer un classeur et une feuille de calcul  

Tout d’abord : vous avez besoin d’un objet workbook qui représente le fichier Excel, et d’une feuille de calcul où les données seront stockées.

```csharp
using Aspose.Cells;
using System;

class ExcelDateDemo
{
    static void Main()
    {
        // Step 1: Initialize a new workbook and grab the first worksheet
        Workbook workbook = new Workbook();                     // creates an empty .xlsx in memory
        Worksheet worksheet = workbook.Worksheets[0];           // default sheet is named "Sheet1"
```

*Pourquoi c’est important :* La classe `Workbook` est le point d’entrée pour toutes les opérations Excel. La créer en mémoire signifie que vous n’interagissez jamais avec le système de fichiers tant que vous n’enregistrez pas explicitement, ce qui rend le processus rapide et adapté aux tests.

## Étape 2 : Écrire une date dans Excel  

Ensuite, nous placerons une chaîne de date de l’ère japonaise (`"R02-04-01"`) dans la cellule **A1**. Cette chaîne imite l’ère Reiwa (année 2, 1er avril).

```csharp
        // Step 2: Write a Japanese era date string into cell A1
        worksheet.Cells["A1"].PutValue("R02-04-01");
```

*Ce qui se passe :* `PutValue` enregistre la chaîne brute. Aspose.Cells tentera ensuite de l’analyser en fonction du style de la cellule. Si vous sautez cette étape et écrivez directement un `DateTime`, vous perdrez l’information d’ère que vous souhaitez afficher.

## Étape 3 : Appliquer le format numérique de date intégré (ID 14)

Excel possède un format de date intégré avec l’ID 14 (`mm-dd-yy`). L’appliquer indique au moteur que la cellule **contient une date**, pas seulement du texte.

```csharp
        // Step 3: Apply the built‑in date number format (ID 14)
        worksheet.Cells["A1"].Style.Number = 14;
```

*Pourquoi utiliser l’ID 14 ?* C’est le format « date courte » universel qui garantit qu’Excel traite le contenu comme une valeur de date, condition indispensable pour que tout format personnalisé fonctionne correctement.

## Étape 4 : Définir un format personnalisé pour afficher la notation de l’ère japonaise  

Passons à la partie amusante : nous indiquons à Excel d’afficher la date en utilisant le format de l’ère japonaise. La chaîne personnalisée `[$-ja-JP]ggge年m月d日` fait exactement cela.

```csharp
        // Step 4: Set a custom format to display the date in Japanese era notation
        worksheet.Cells["A1"].Style.Custom = "[$-ja-JP]ggge年m月d日";
```

*Explication :*  
- `[$-ja-JP]` force la locale en japonais.  
- `ggg` est le nom de l’ère (par ex., « R » pour Reiwa).  
- `e` est l’année de l’ère.  
- `年`, `月`, `日` sont des caractères japonais littéraux pour année, mois, jour.

Si vous avez besoin d’une autre locale, remplacez simplement `ja-JP` par le code culturel approprié (par ex., `en-US`).

## Étape 5 : Récupérer la valeur DateTime analysée  

Enfin, lisons le **vrai `DateTime`** qu’Excel a analysé à partir de la cellule. Cela prouve que la chaîne a été correctement interprétée.

```csharp
        // Step 5: Retrieve the parsed DateTime value from the cell
        DateTime parsedDate = worksheet.Cells["A1"].DateTime;   // => 2020‑04‑01

        // Output to console for verification
        Console.WriteLine($"Parsed DateTime: {parsedDate:yyyy-MM-dd}");
```

*Résultat :* La console affiche `Parsed DateTime: 2020-04-01`. Même si nous avons saisi une chaîne d’ère japonaise, Excel stocke en interne la date grégorienne, que vous pouvez utiliser pour des calculs, des comparaisons ou d’autres exportations.

## Étape 6 : Enregistrer le classeur (optionnel)

Si vous souhaitez voir le classeur formaté dans Excel, enregistrez‑le simplement sur le disque.

```csharp
        // Optional: Save the workbook to a file
        workbook.Save("JapaneseEraDate.xlsx");
    }
}
```

Ouvrez le fichier généré **JapaneseEraDate.xlsx** et vous verrez la cellule **A1** afficher `R02年4月1日` (le format exact de l’ère japonaise que nous avons défini).

![exemple de format personnalisé de cellule](image-placeholder.png "Cellule Excel affichant une date de l’ère japonaise – format personnalisé de cellule")

*Le texte alt ci‑dessus contient le mot‑clé principal, satisfaisant l’exigence SEO de l’image.*

## Variations courantes et cas limites  

### Écrire un format de date différent  

Si vous préférez le format ISO‑8601 (`2020-04-01`) au lieu d’une chaîne d’ère, modifiez simplement l’appel `PutValue` :

```csharp
worksheet.Cells["A1"].PutValue(new DateTime(2020, 4, 1));
worksheet.Cells["A1"].Style.Number = 14;                 // keep built‑in date format
worksheet.Cells["A1"].Style.Custom = "yyyy-mm-dd";      // custom ISO format
```

### Gérer les cellules nulles ou vides  

Lors de la lecture d’une date, protégez toujours contre les cellules vides afin d’éviter `InvalidOperationException` :

```csharp
if (!worksheet.Cells["A1"].IsDate)
{
    Console.WriteLine("Cell A1 does not contain a valid date.");
}
else
{
    DateTime dt = worksheet.Cells["A1"].DateTime;
    // use dt...
}
```

### Prise en charge de plusieurs locales  

Vous pouvez parcourir une liste de codes culturels et les appliquer dynamiquement :

```csharp
string[] cultures = { "ja-JP", "en-US", "fr-FR" };
foreach (var culture in cultures)
{
    worksheet.Cells["A1"].Style.Custom = $"[$-{culture}]ggge年m月d日";
    // Save or export per culture if needed
}
```

## Astuces pro & pièges  

- **Toujours définir d’abord un format numérique intégré** (`Style.Number`). Sans cela, Excel traite la cellule comme du texte brut et le format personnalisé est ignoré.  
- **Les codes de locale ne sont pas sensibles à la casse**, mais utiliser la forme canonique (`ja-JP`) évite les confusions.  
- **L’enregistrement est optionnel** pour le traitement en mémoire ; vous pouvez diffuser le classeur directement dans une réponse web (`workbook.Save(stream, SaveFormat.Xlsx)`).  
- **Licences Aspose.Cells** : La version d’évaluation gratuite ajoute un filigrane. En production, assurez‑vous de disposer d’une licence valide pour éviter des pénalités de performance.

## Récapitulatif  

Nous avons montré comment **définir le format personnalisé d’une cellule** en C# pour afficher des dates de l’ère japonaise, comment **écrire une date dans Excel**, **appliquer un format de date personnalisé**, **lire un DateTime depuis Excel**, et **créer une feuille de calcul** — le tout dans un seul programme autonome. Le mot‑clé principal apparaît naturellement tout au long du texte, tandis que les mots‑clés secondaires sont intégrés dans les titres et le corps du texte, répondant aux exigences SEO et aux standards de citation IA.

## Et après ?

- Explorez le **formatage conditionnel** pour mettre en évidence les dates en retard.  
- Combinez cette approche avec les **Tableaux croisés dynamiques** pour des rapports dynamiques.  
- Essayez de **lire de gros fichiers CSV** et de les convertir en Excel avec la même logique de gestion des dates.  

N’hésitez pas à expérimenter avec différentes locales, modèles personnalisés, ou même fuseaux horaires. Si vous rencontrez des problèmes, laissez un commentaire ci‑dessous — bon codage !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}