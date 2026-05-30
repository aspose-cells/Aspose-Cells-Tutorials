---
category: general
date: 2026-05-30
description: Activez l'analyse des ères japonaises en C# avec Aspose.Cells. Apprenez
  à définir la culture du classeur, à analyser les dates d’ère et à gérer le calendrier
  japonais dans les feuilles de calcul Excel.
draft: false
keywords:
- enable japanese era parsing
- Aspose.Cells Japanese era
- set workbook culture
- parse era dates
- c# excel date parsing
language: fr
og_description: Activez l'analyse des ères japonaises en C# avec Aspose.Cells. Ce
  guide montre comment définir la culture du classeur, activer la prise en charge
  des ères et travailler avec les dates japonaises.
og_title: Activer l'analyse des ères japonaises en C# – Guide complet
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Enable Japanese era parsing in C# using Aspose.Cells. Learn to set
    workbook culture, parse era dates, and handle Japanese calendar in Excel worksheets.
  headline: Enable Japanese Era Parsing in C# with Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel Automation
title: Activer l'analyse des ères japonaises en C# avec Aspose.Cells
url: /fr/net/workbook-settings/enable-japanese-era-parsing-in-c-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Activer l'analyse des ères japonaises en C# avec Aspose.Cells

Vous avez déjà eu besoin d'**activer l'analyse des ères japonaises** lors de la génération de fichiers Excel pour un client japonais ? Vous n'êtes pas le seul —de nombreux développeurs se heurtent à un mur lorsque le calendrier japonais historique (令和, 平成, etc.) apparaît dans les données. La bonne nouvelle, c'est qu'Aspose.Cells rend cela très simple pour reconnaître ces dates d'ère et les convertir en valeurs grégoriennes standard.

Dans ce tutoriel, nous passerons en revue les étapes exactes pour **activer l'analyse des ères japonaises** avec Aspose.Cells, définir la culture du classeur sur le japonais, et insérer une date formatée en ère dans une cellule. À la fin, vous disposerez d'un extrait C# exécutable qui analyse « 令和3年5月1日 » en l'objet date `2021‑05‑01` correct. Aucun document externe n'est nécessaire — il suffit de copier, coller et exécuter.

## Prérequis

- .NET 6.0 ou version ultérieure (le code fonctionne avec .NET Core, .NET Framework et .NET 5+)
- Aspose.Cells pour .NET (package NuGet `Aspose.Cells`)
- Connaissances de base en C# — si vous pouvez écrire un `Console.WriteLine`, vous êtes prêt
- Un IDE de votre choix (Visual Studio, VS Code, Rider…)

> **Conseil :** Gardez votre version d'Aspose.Cells à jour ; la version 24.10+ inclut les dernières définitions des ères japonaises.

## Pourquoi activer l'analyse des ères japonaises ?

Les calendriers japonais utilisent des ères liées aux règnes impériaux. Pour la plupart des applications modernes, vous souhaiterez stocker les dates au format grégorien habituel, mais les données sources peuvent encore arriver sous la forme « 令和3年5月1日 ». Si vous ne **activez pas l'analyse des ères japonaises**, la chaîne sera traitée comme du texte brut, ce qui perturbera les calculs, le tri et la création de graphiques. En activant la prise en charge des ères, Aspose.Cells convertit automatiquement ces chaînes en valeurs `DateTime` correctes, préservant à la fois la lisibilité pour les utilisateurs japonais et la justesse numérique pour le traitement en aval.

## Étape 1 : Définir la culture du classeur sur le japonais

La première chose à faire est d'indiquer à Aspose.Cells que la locale par défaut du classeur est le japonais (`ja-JP`). Cela garantit que toute analyse dépendante de la culture (y compris les noms d'ère) suit les règles japonaises.

```csharp
using Aspose.Cells;
using System.Globalization;

class Program
{
    static void Main()
    {
        // Create a new workbook instance
        Workbook workbook = new Workbook();

        // Set the workbook culture to Japanese (ja-JP)
        workbook.Settings.Culture = new CultureInfo("ja-JP");
```

> **Pourquoi c’est important :** L'objet `CultureInfo` contrôle les formats numériques, les séparateurs de dates, et surtout pour nous, le système de calendrier utilisé lors de l'analyse des chaînes.

## Étape 2 : Activer l'analyse des ères japonaises

Maintenant que la culture est définie, vous devez activer le commutateur qui indique à Aspose.Cells de reconnaître les dates d'ère. C’est le cœur de **l'activation de l'analyse des ères japonaises**.

```csharp
        // Enable parsing of Japanese era dates (令和, 平成, 昭和, etc.)
        workbook.Settings.UseJapaneseEra = true;
```

> **Erreur fréquente :** Oublier ce drapeau signifie que « 令和3年5月1日 » reste une chaîne littérale. Une fois activé, Aspose.Cells associe automatiquement l'ère à l'année grégorienne correcte.

## Étape 3 : Insérer une date formatée en ère dans une cellule

Avec la culture et la prise en charge des ères prêtes, insérer une chaîne d'ère japonaise est simple. La bibliothèque l'analysera et stockera une vraie valeur `DateTime`.

```csharp
        // Grab the first worksheet (index 0)
        Worksheet sheet = workbook.Worksheets[0];

        // Insert a Japanese era date string into cell A1
        // The string "令和3年5月1日" becomes 2021‑05‑01 internally
        sheet.Cells["A1"].PutValue("令和3年5月1日");

        // Save the workbook to verify the result
        workbook.Save("JapaneseEraDemo.xlsx");
    }
}
```

### Résultat attendu

- **Cellule A1** du fichier `JapaneseEraDemo.xlsx` généré affichera **2021‑05‑01** (ou le format de date japonais localisé si vous l'ouvrez dans Excel avec la locale japonaise).
- La valeur sous‑jacente est un vrai `DateTime`, vous pouvez donc l'utiliser en toute sécurité dans des formules, des tableaux croisés dynamiques ou d'autres calculs C#.

## Étape 4 : Vérifier la date analysée programmatiquement (facultatif)

Si vous souhaitez vérifier que l'analyse a réussi avant d'enregistrer, vous pouvez relire la cellule :

```csharp
        // Retrieve the value as a DateTime
        DateTime parsedDate = sheet.Cells["A1"].GetDateTime();

        Console.WriteLine($"Parsed date: {parsedDate:yyyy-MM-dd}");
        // Output: Parsed date: 2021-05-01
```

Cette petite étape de vérification est pratique dans les tests unitaires ou lors du traitement de fichiers Excel fournis par les utilisateurs.

## Cas limites et variantes

| Scénario | Que faire |
|----------|-----------|
| **Plusieurs ères dans un même classeur** | Conservez `UseJapaneseEra = true` ; Aspose.Cells reconnaîtra toutes les ères prises en charge (令和, 平成, 昭和, 大正, 明治). |
| **Chaînes mixtes grégoriennes et d'ère** | L'analyseur distingue automatiquement ; les chaînes grégoriennes restent inchangées. |
| **Exigences de calendrier personnalisé** | Vous pouvez toujours définir `Workbook.Settings.Calendar` sur une instance `Calendar` spécifique si vous avez besoin de plus de contrôle. |
| **Versions .NET plus anciennes** | Le même code fonctionne sur .NET Framework 4.6+ ; assurez‑vous simplement que le constructeur `System.Globalization.CultureInfo` est disponible. |

## Conseils pratiques pour les projets réels

- **Mettez en cache le `CultureInfo`** si vous créez de nombreux classeurs dans une boucle ; le créer à chaque fois ajoute une surcharge.
- **Validez l'entrée** avant d'appeler `PutValue` ; les chaînes d'ère mal formées lanceront une exception.
- **Désactivez l'analyse des ères** (`UseJapaneseEra = false`) lorsque vous êtes certain que les données ne contiennent jamais de dates d'ère — cela peut légèrement améliorer les performances.
- **Utilisez `Workbook.SaveOptions`** pour contrôler le format de sortie (XLSX, XLS, CSV) tout en préservant la date analysée.

## Exemple complet fonctionnel (prêt à copier‑coller)

```csharp
using Aspose.Cells;
using System;
using System.Globalization;

class EnableJapaneseEraParsingDemo
{
    static void Main()
    {
        // 1️⃣ Create a new workbook
        Workbook workbook = new Workbook();

        // 2️⃣ Set workbook culture to Japanese (ja-JP)
        workbook.Settings.Culture = new CultureInfo("ja-JP");

        // 3️⃣ Enable Japanese era parsing
        workbook.Settings.UseJapaneseEra = true;

        // 4️⃣ Access the first worksheet
        Worksheet sheet = workbook.Worksheets[0];

        // 5️⃣ Insert an era‑formatted date
        sheet.Cells["A1"].PutValue("令和3年5月1日");

        // Optional: read back the parsed value
        DateTime dt = sheet.Cells["A1"].GetDateTime();
        Console.WriteLine($"Parsed date: {dt:yyyy-MM-dd}");

        // Save the workbook
        workbook.Save("EnableJapaneseEraParsing.xlsx");
    }
}
```

Exécutez le programme, ouvrez le fichier généré, et vous verrez **2021‑05‑01** dans la cellule A1—preuve que nous avons bien **activé l'analyse des ères japonaises**.

## Conclusion

Nous venons de démontrer comment **activer l'analyse des ères japonaises** en C# avec Aspose.Cells, définir la culture du classeur, et convertir sans effort des dates d'ère comme « 令和3年5月1日 » en valeurs grégoriennes standard. Les étapes sont minimes, le code est autonome, et le résultat fonctionne parfaitement dans Excel.

Prêt pour le prochain défi ? Essayez de combiner **définir la culture du classeur** avec le formatage des nombres pour le yen japonais, ou générez un rapport multi‑feuilles qui mélange dates grégoriennes et dates d'ère. Vous avez maintenant les bases pour gérer toutes les particularités du calendrier japonais dans vos projets d’automatisation Excel en .NET.

---

*Si ce guide vous a été utile, pensez à mettre une étoile au dépôt GitHub d'Aspose.Cells ou à partager vos propres astuces dans les commentaires. Bon codage !*

## Que devriez‑vous apprendre ensuite ?

- [Charger des classeurs Excel avec des dates spécifiques à la culture en utilisant Aspose.Cells pour .NET](/cells/english/net/formatting/load-workbook-culture-specific-dates-aspose-cells-net/)
- [Comment définir la langue dans les fichiers Excel en utilisant Aspose.Cells .NET pour la prise en charge multilingue](/cells/english/net/formulas-functions/specify-language-excel-aspose-cells-net/)
- [Charger des dates spécifiques à la culture du classeur avec Aspose Cells .NET](/cells/chinese/net/formatting/load-workbook-culture-specific-dates-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}