---
category: general
date: 2026-09-24
description: Analyser DateTime avec le règne de l'empereur japonais en utilisant Aspose.Cells
  en C#. Activer le calendrier des ères japonaises, écrire les chaînes d'ère et récupérer
  des valeurs DateTime précises.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- Parse DateTime with Japanese Emperor Reign
- Aspose.Cells
- C# date parsing
- Japanese era calendar
- Workbook Settings
- DateTimeValue
language: fr
lastmod: 2026-09-24
og_description: Analyser un DateTime avec le règne de l'empereur japonais en utilisant
  Aspose.Cells en C#. Ce tutoriel montre comment activer le calendrier des ères japonaises,
  écrire des chaînes d’ère et récupérer un DateTime correct.
og_image_alt: Screenshot of C# code parsing a Japanese era date with Aspose.Cells
og_title: Analyser DateTime avec le règne de l'empereur japonais en utilisant Aspose.Cells
  – guide C#
schemas:
- author: Aspose
  dateModified: '2026-09-24'
  description: Parse DateTime with Japanese Emperor Reign using Aspose.Cells in C#.
    Enable the Japanese era calendar, write era strings, and retrieve accurate DateTime
    values.
  headline: Parse DateTime with Japanese Emperor Reign using Aspose.Cells
  type: TechArticle
- description: Parse DateTime with Japanese Emperor Reign using Aspose.Cells in C#.
    Enable the Japanese era calendar, write era strings, and retrieve accurate DateTime
    values.
  name: Parse DateTime with Japanese Emperor Reign using Aspose.Cells
  steps:
  - name: Multiple era formats
    text: 'Aspose.Cells recognises several era representations:'
  - name: Invalid strings
    text: 'When the string cannot be parsed (e.g., `"令和99年13月40日"`), `DateTimeValue`
      returns `DateTime.MinValue`. You can check for this condition:'
  - name: Disabling the feature
    text: 'If you later need to store raw era strings without conversion, set the
      flag back to `false`:'
  - name: Performance tip
    text: Enabling the era calendar adds a small overhead to every `PutValue` call
      that involves strings. If you only parse a handful of cells, enable the flag
      right before the operation and disable it afterward to minimise impact.
  type: HowTo
tags:
- Aspose.Cells
- C#
- DateTime
- Japanese era
- .NET
title: Analyser la date et l’heure avec le règne de l’empereur japonais à l’aide d’Aspose.Cells
url: /fr/net/excel-custom-number-date-formatting/parse-datetime-with-japanese-emperor-reign-using-aspose-cell/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Analyser DateTime avec le règne de l'empereur japonais en utilisant Aspose.Cells

Si vous devez **analyser DateTime avec le règne de l'empereur japonais** dans une application .NET, ce guide vous montre exactement comment le faire avec Aspose.Cells. En activant le calendrier des ères japonaises, en écrivant une chaîne basée sur une ère et en lisant la valeur `DateTime` résultante, vous obtenez des dates fiables et sensibles à la culture sans manipulation manuelle de chaînes.

Travailler avec des dates d'ère japonaise est courant dans la finance, le gouvernement et les systèmes hérités qui stockent encore des dates comme « 令和3年5月10日 ». Ce tutoriel couvre le flux de travail complet, de la configuration du projet à la récupération d'un objet `DateTime` que vous pouvez utiliser dans les calculs, la journalisation ou l'affichage UI.

## Ce que vous apprendrez

- Comment ajouter le package NuGet Aspose.Cells à un projet C#.
- Comment activer le **calendrier des ères japonaises** via `Workbook.Settings`.
- Comment écrire une chaîne de date d'ère japonaise dans une cellule et laisser Aspose.Cells l'analyser automatiquement.
- Comment lire le `DateTime` analysé en utilisant la propriété `DateTimeValue`.

**Prérequis**  
- .NET 6.0 ou ultérieur (le code fonctionne également avec .NET Framework 4.7+).  
- Familiarité de base avec C# et Visual Studio (ou tout IDE).  
- Accès à Internet pour télécharger le package Aspose.Cells.

---

## Étape 1 : Installer Aspose.Cells

Ouvrez le dossier de votre projet dans un terminal ou la console du Gestionnaire de packages NuGet et exécutez :

```bash
dotnet add package Aspose.Cells
```

Ou, dans Visual Studio, faites un clic droit sur le projet → **Manage NuGet Packages** → recherchez **Aspose.Cells** et cliquez sur **Install**.  
Cela ajoute l'assembly `Aspose.Cells`, qui fournit les fonctionnalités `Workbook`, `Worksheet` et d'analyse dont nous avons besoin.

## Étape 2 : Activer le calendrier des ères japonaises

Aspose.Cells désactive l'analyse des ères japonaises par défaut. Vous devez l'activer via le drapeau `Workbook.Settings.UseJapaneseEraCalendar`.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Create a new workbook instance
        Workbook workbook = new Workbook();

        // Enable parsing of Japanese era dates (e.g., 令和, 平成)
        workbook.Settings.UseJapaneseEraCalendar = true;
```

Définir `UseJapaneseEraCalendar` sur `true` indique à la bibliothèque d'interpréter les chaînes contenant des noms d'ère (`令和`, `平成`, `昭和`, etc.) selon les règles officielles du calendrier japonais.

## Étape 3 : Écrire une chaîne de date d'ère japonaise dans une cellule

Ensuite, récupérez la première feuille de calcul et placez une chaîne de date d'ère japonaise dans la cellule **A1**.

```csharp
        // Access the first worksheet (index 0)
        Worksheet sheet = workbook.Worksheets[0];

        // Write the era‑based date string into cell A1
        sheet.Cells["A1"].PutValue("令和3年5月10日");
```

**Pourquoi cela fonctionne :**  
Lorsque `UseJapaneseEraCalendar` est actif, `PutValue` examine la chaîne, détecte le préfixe d'ère (`令和`) et la convertit en interne en l'année grégorienne correspondante (2021). La bibliothèque stocke alors la valeur comme un véritable objet `DateTime`, pas seulement du texte.

## Étape 4 : Récupérer la valeur `DateTime` analysée

Lisez maintenant la `DateTimeValue` de la cellule. Aspose.Cells renvoie automatiquement la date grégorienne.

```csharp
        // Retrieve the parsed DateTime from cell A1
        DateTime parsedDate = sheet.Cells["A1"].DateTimeValue;

        // Output the result to the console
        Console.WriteLine($"Parsed Gregorian date: {parsedDate:yyyy-MM-dd}");
    }
}
```

Running the program prints:

```
Parsed Gregorian date: 2021-05-10
```

La sortie confirme que **Parse DateTime with Japanese Emperor Reign** a correctement converti « 令和3年5月10日 » en 10 mai 2021.

## Étape 5 : Gérer les cas limites et les variations courantes

### Formats d'ère multiples

Aspose.Cells reconnaît plusieurs représentations d'ère :

| Era (Japanese) | Plage d'années grégoriennes |
|----------------|-----------------------------|
| 明治 (Meiji)   | 1868‑1912                   |
| 大正 (Taishō)  | 1912‑1926                   |
| 昭和 (Shōwa)   | 1926‑1989                   |
| 平成 (Heisei)  | 1989‑2019                   |
| 令和 (Reiwa)   | 2019‑present                |

Si vos données sources mélangent des caractères pleine largeur, des espaces, ou utilisent les kanjis « 年 », « 月 », « 日 », l'analyseur réussit toujours. Par exemple, `"平成31年4月30日"` devient `2019-04-30`.

### Chaînes invalides

Lorsque la chaîne ne peut pas être analysée (par ex., `"令和99年13月40日"`), `DateTimeValue` renvoie `DateTime.MinValue`. Vous pouvez vérifier cette condition :

```csharp
if (parsedDate == DateTime.MinValue)
{
    Console.WriteLine("The cell does not contain a valid Japanese era date.");
}
```

### Désactiver la fonctionnalité

Si vous avez plus tard besoin de stocker des chaînes d'ère brutes sans conversion, réinitialisez le drapeau à `false` :

```csharp
workbook.Settings.UseJapaneseEraCalendar = false;
```

### Astuce de performance

Activer le calendrier des ères ajoute un léger surcoût à chaque appel `PutValue` impliquant des chaînes. Si vous ne parsez que quelques cellules, activez le drapeau juste avant l'opération et désactivez-le ensuite pour minimiser l'impact.

## Exemple complet et exécutable

Below is the full program you can copy, paste, and run instantly.

```csharp
using Aspose.Cells;
using System;

class ParseJapaneseEraDemo
{
    static void Main()
    {
        // 1️⃣ Create a new workbook
        Workbook workbook = new Workbook();

        // 2️⃣ Turn on Japanese era parsing
        workbook.Settings.UseJapaneseEraCalendar = true;

        // 3️⃣ Access the first worksheet
        Worksheet sheet = workbook.Worksheets[0];

        // 4️⃣ Write an era date string into A1
        sheet.Cells["A1"].PutValue("令和3年5月10日");

        // 5️⃣ Retrieve the parsed DateTime
        DateTime parsedDate = sheet.Cells["A1"].DateTimeValue;

        // Verify the result
        Console.WriteLine($"Parsed Gregorian date: {parsedDate:yyyy-MM-dd}");
        // Expected output: Parsed Gregorian date: 2021-05-10
    }
}
```

**Sortie attendue**

```
Parsed Gregorian date: 2021-05-10
```

Le programme démontre le flux de bout en bout pour **Parse DateTime with Japanese Emperor Reign** avec Aspose.Cells, depuis la création du classeur jusqu'à l'obtention d'un objet `DateTime` utilisable.

---

## Conclusion

Vous savez maintenant comment **Parse DateTime with Japanese Emperor Reign** en C# en :

1. Installant **Aspose.Cells**.  
2. Activant le **calendrier des ères japonaises** via `Workbook.Settings`.  
3. Écrivant des chaînes basées sur les ères dans les cellules.  
4. Lisant la `DateTimeValue` résultante.  

Cette approche élimine la logique d'analyse manuelle, respecte les limites officielles des ères et s'intègre parfaitement au code .NET existant de gestion des dates.

**Prochaines étapes**  
- Explorez d'autres fonctionnalités spécifiques aux cultures d'Aspose.Cells, comme le **parsing de dates C#** pour les calendriers Hijri ou bouddhiste thaïlandais.  
- Combinez cette technique avec les **Workbook Settings** comme `CalcEngine` pour évaluer les formules qui font référence aux dates d'ère.  
- Utilisez le `DateTime` analysé dans les rapports, le stockage en base de données ou les composants UI qui nécessitent des dates grégoriennes.

N'hésitez pas à expérimenter avec différentes chaînes d'ère, à gérer les entrées invalides et à intégrer la solution dans des pipelines d'importation de données plus vastes. Bon codage !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d'implémentation alternatives dans vos propres projets.

- [Analyser les dates d'ère japonaise dans Excel – Guide complet pour les développeurs C#](/cells/english/net/data-loading-and-parsing/parse-japanese-era-dates-in-excel-full-guide-for-c-developer/)
- [Comment analyser les dates japonaises en C# – Guide complet](/cells/english/net/data-loading-and-parsing/how-to-parse-japanese-dates-in-c-complete-guide/)
- [Comment implémenter la validation de dates en .NET avec Aspose.Cells : Guide complet](/cells/english/net/data-validation/implement-date-validation-net-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}