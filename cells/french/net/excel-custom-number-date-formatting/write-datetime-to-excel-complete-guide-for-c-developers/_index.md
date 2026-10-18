---
category: general
date: 2026-04-07
description: Écrire une date/heure dans Excel avec C#. Apprenez comment insérer une
  date dans une feuille de calcul, gérer la valeur de date d’une cellule Excel et
  convertir une date du calendrier japonais en quelques étapes seulement.
draft: false
keywords:
- write datetime to excel
- excel cell date value
- insert date into worksheet
- convert japanese calendar date
language: fr
og_description: Écrire une date/heure dans Excel rapidement. Ce guide montre comment
  insérer une date dans une feuille de calcul, gérer la valeur de date d’une cellule
  Excel et convertir une date du calendrier japonais avec C#.
og_title: Écrire une date et une heure dans Excel – Tutoriel C# étape par étape
tags:
- C#
- Excel automation
- Aspose.Cells
title: Écrire une date/heure dans Excel – Guide complet pour les développeurs C#
url: /fr/net/excel-custom-number-date-formatting/write-datetime-to-excel-complete-guide-for-c-developers/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Écrire une date/heure dans Excel – Guide complet pour les développeurs C#

Vous avez déjà eu besoin **d’écrire une date/heure dans Excel** sans savoir quel appel d’API stocke réellement une vraie date Excel ? Vous n’êtes pas seul. Dans de nombreux outils d’entreprise, nous devons placer un `DateTime` C# dans une feuille de calcul, et le résultat doit se comporter comme une vraie date Excel — triable, filtrable et prête pour les tableaux croisés dynamiques.  

Dans ce tutoriel, nous passerons en revue les étapes exactes pour *insérer une date dans une feuille de calcul* à l’aide d’Aspose.Cells, expliquerons pourquoi la définition de la culture est importante, et montrerons même comment **convertir une date du calendrier japonais** en un `DateTime` ordinaire avant de l’écrire. À la fin, vous disposerez d’un extrait autonome que vous pourrez copier‑coller dans n’importe quel projet .NET.

## Ce dont vous avez besoin

- **.NET 6+** (ou toute version récente de .NET ; le code fonctionne également sur .NET Framework)  
- **Aspose.Cells for .NET** – un package NuGet qui permet de manipuler des fichiers Excel sans Office installé.  
- Une compréhension de base du `DateTime` C# et des cultures.  

Aucune bibliothèque supplémentaire, aucun interop COM, et aucune installation d’Excel requise. Si vous avez déjà une instance de feuille de calcul (`ws`), vous êtes prêt.

## Étape 1 : Configurer la culture japonaise (Convertir une date du calendrier japonais)

Lorsque vous recevez une date comme `"R02/05/01"` (Reiwa 2, 1er mai), vous devez indiquer à .NET comment interpréter les symboles d’ère. Le calendrier japonais n’est pas le calendrier grégorien par défaut, nous créons donc un `CultureInfo` qui remplace son calendrier par `JapaneseCalendar`.

```csharp
using System;
using System.Globalization;
using Aspose.Cells;   // Make sure Aspose.Cells is referenced

// Assume you already have a worksheet instance named "ws"
Worksheet ws = /* your worksheet instance */;

// 1️⃣ Configure a Japanese culture that uses the Japanese calendar
CultureInfo japaneseCulture = new CultureInfo("ja-JP");
japaneseCulture.DateTimeFormat.Calendar = new JapaneseCalendar();
```

**Pourquoi c’est important :**  
Si vous analysez la chaîne avec la culture par défaut, .NET lèvera une exception de format parce qu’il ne peut pas associer `R` (l’ère Reiwa) à une année. En substituant `JapaneseCalendar`, l’analyseur comprend les symboles d’ère et les traduit en l’année grégorienne correcte.

## Étape 2 : Analyser la chaîne basée sur l’ère en un `DateTime`

Maintenant que la culture est prête, nous pouvons appeler en toute sécurité `DateTime.ParseExact`. La chaîne de format `"ggyy/MM/dd"` indique à l’analyseur :

- `gg` – désignateur d’ère (ex. `R` pour Reiwa)  
- `yy` – année à deux chiffres dans l’ère  
- `MM/dd` – mois et jour.

```csharp
// 2️⃣ Parse a date string in the Japanese era format (ggyy/MM/dd)
string japaneseDate = "R02/05/01";          // Reiwa 2, May 1st
DateTime parsedDate = DateTime.ParseExact(
    japaneseDate,
    "ggyy/MM/dd",
    japaneseCulture,
    DateTimeStyles.None
);
```

**Astuce :** Si vous pouvez recevoir des dates sous d’autres formats (ex. `"Heisei 30/12/31"`), encapsulez l’analyse dans un `try/catch` et revenez à `DateTime.TryParseExact`. Cela empêche votre tâche d’importation de planter à cause d’une seule ligne incorrecte.

## Étape 3 : Écrire le `DateTime` dans une cellule Excel (Valeur de date de cellule Excel)

Aspose.Cells traite un `DateTime` .NET comme une vraie date Excel lorsque vous utilisez `PutValue`. La bibliothèque convertit automatiquement les ticks en numéro de série Excel (le nombre de jours depuis le 1900‑01‑00). Ainsi, la cellule affichera une **valeur de date de cellule Excel** correcte et vous pourrez la formater ultérieurement avec les styles de date intégrés d’Excel.

```csharp
// 3️⃣ Write the resulting DateTime value into cell C1 of the worksheet
Cell targetCell = ws.Cells["C1"];
targetCell.PutValue(parsedDate);

// Optional: apply a standard date format so users see "yyyy-MM-dd"
targetCell.Style.Number = 14;   // built‑in Excel format ID for "m/d/yy"
```

**Ce que vous verrez dans Excel :**  
La cellule C1 contient maintenant le numéro de série `44796`, que Excel rend sous la forme `2020‑05‑01` (ou le format que vous avez appliqué). La valeur sous‑jacente est une vraie date, pas une chaîne, donc le tri fonctionne comme prévu.

## Étape 4 : Enregistrer le classeur (Conclusion)

Si vous n’avez pas encore enregistré le classeur, faites‑le maintenant. Cette étape n’est pas strictement liée à l’écriture de la date/heure, mais elle finalise le flux de travail.

```csharp
// Save the workbook to a file (or a MemoryStream if you need it in‑memory)
Workbook workbook = ws.Workbook;   // get the parent workbook
workbook.Save("Output.xlsx", SaveFormat.Xlsx);
```

Voilà—quatre étapes concises, et vous avez réussi à **écrire une date/heure dans Excel**, en gérant une date d’ère japonaise en même temps.

---

![write datetime to excel example](/images/write-datetime-to-excel.png "Screenshot showing a C# project writing a DateTime into Excel cell C1")

*L’image ci‑dessus illustre le fichier Excel final avec la date correctement affichée dans la cellule C1.*

## Questions fréquentes & Cas particuliers

### Et si la variable de feuille de calcul n’est pas encore prête ?

Vous pouvez créer un nouveau classeur à la volée :

```csharp
Workbook workbook = new Workbook();
Worksheet ws = workbook.Worksheets[0];   // default first sheet
```

### Comment conserver la chaîne d’ère japonaise d’origine dans la feuille ?

Si vous avez besoin à la fois de la chaîne originale et de la date analysée, écrivez‑les dans des cellules adjacentes :

```csharp
ws.Cells["B1"].PutValue(japaneseDate);   // original text
ws.Cells["C1"].PutValue(parsedDate);     // parsed DateTime
```

### Cela fonctionne‑t‑il avec les versions plus anciennes de .NET ?

Oui. `JapaneseCalendar` existe depuis .NET 2.0, et Aspose.Cells prend en charge .NET Framework 4.5+. Assurez‑vous simplement de référencer l’assembly correct.

### Qu’en est‑il des fuseaux horaires ?

`DateTime.ParseExact` renvoie un **Kind** de `Unspecified`. Si vos dates sources sont en UTC, convertissez‑les d’abord :

```csharp
DateTime utcDate = DateTime.SpecifyKind(parsedDate, DateTimeKind.Utc);
DateTime localDate = utcDate.ToLocalTime();
targetCell.PutValue(localDate);
```

### Puis‑je définir un format de date personnalisé (ex. “yyyy年MM月dd日”) ?

Absolument. Utilisez la propriété `Style.Custom` :

```csharp
targetCell.Style.Custom = "yyyy\"年\"mm\"月\"dd\"日\"";
```

Excel affichera alors `2020年05月01日` tout en stockant une vraie valeur de date.

## Récapitulatif

Nous avons couvert tout ce dont vous avez besoin pour **écrire une date/heure dans Excel** depuis C# :

1. **Configurer** une culture japonaise avec `JapaneseCalendar` pour **convertir une date du calendrier japonais**.  
2. **Analyser** la chaîne basée sur l’ère avec `DateTime.ParseExact`.  
3. **Insérer** le `DateTime` résultant dans une cellule, garantissant une vraie **valeur de date de cellule Excel**.  
4. **Enregistrer** le classeur afin que les données persistent.

Avec ces quatre étapes, vous pouvez en toute sécurité **insérer une date dans une feuille de calcul** quel que soit le format source. Le code est entièrement exécutable, ne nécessite qu’Aspose.Cells, et fonctionne sur n’importe quel runtime .NET moderne.

## Et après ?

- **Importation massive** : bouclez sur les lignes d’un CSV, analysez chaque date japonaise et écrivez‑les dans des cellules consécutives.  
- **Mise en forme** : appliquez une mise en forme conditionnelle pour mettre en évidence les dates d’échéance dépassées.  
- **Performance** : utilisez `WorkbookDesigner` ou la mise en cache de `CellStyle` lorsque vous traitez des milliers de lignes.  

N’hésitez pas à expérimenter — remplacez l’ère japonaise par le calendrier grégorien, changez la cellule cible, ou exportez vers un autre format de fichier (CSV, ODS). L’idée centrale reste la même : analyser, convertir et **écrire une date/heure dans Excel** en toute confiance.

Bon codage, et que vos feuilles de calcul se trient toujours correctement !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}