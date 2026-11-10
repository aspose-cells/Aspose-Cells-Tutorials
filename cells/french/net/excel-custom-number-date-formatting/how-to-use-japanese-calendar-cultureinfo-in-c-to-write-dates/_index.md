---
category: general
date: 2026-10-26
description: Apprenez à utiliser le CultureInfo du calendrier japonais en C# lors
  de l'analyse des dates d'ère et de leur insertion dans une feuille de calcul Excel
  avec NPOI.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- use japanese calendar cultureinfo
- japanese era date parsing
- cultureinfo with japanese calendar
- datetime parse with cultureinfo
- npoi excel cultureinfo
language: fr
lastmod: 2026-10-26
og_description: Utilisez CultureInfo du calendrier japonais en C# pour analyser les
  dates de l’ère Reiwa et les écrire dans une feuille Excel. Code complet et exécutable
  avec explications.
og_image_alt: Screenshot of C# code parsing a Japanese era date and inserting it into
  an Excel cell
og_title: Utiliser le CultureInfo du calendrier japonais en C# – exemple complet Excel
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to use Japanese calendar CultureInfo in C# when parsing era
    dates and inserting them into an Excel worksheet with NPOI.
  headline: How to use Japanese calendar CultureInfo in C# to write dates to Excel
  type: TechArticle
tags:
- C#
- CultureInfo
- Excel
- NPOI
- Internationalization
title: Comment utiliser le CultureInfo du calendrier japonais en C# pour écrire des
  dates dans Excel
url: /fr/net/excel-custom-number-date-formatting/how-to-use-japanese-calendar-cultureinfo-in-c-to-write-dates/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment utiliser CultureInfo du calendrier japonais en C# pour écrire des dates dans Excel

Si vous devez **utiliser CultureInfo du calendrier japonais** lors de la manipulation de dates en C#, ce guide vous montre exactement comment procéder. Vous apprendrez à analyser une chaîne de date contenant un nom d'ère japonais (par exemple, *Reiwa 2/5/1*) puis à écrire le `DateTime` résultant dans la première cellule d'une feuille de calcul Excel à l'aide de la bibliothèque NPOI.

Analyser des dates basées sur les ères sans le `CultureInfo` correct entraîne une `FormatException` ou des valeurs de mois/jour incorrectes. En configurant `CultureInfo` sur le calendrier japonais, vous garantissez que le runtime .NET interprète correctement l'ère et que la valeur que vous stockez dans Excel correspond à la notation japonaise d'origine.

Dans ce tutoriel, vous allez :

* Créer un objet `CultureInfo` qui utilise le calendrier japonais.
* Analyser une chaîne de date d’ère japonaise avec `DateTime.Parse`.
* Insérer le `DateTime` analysé dans une cellule de feuille de calcul NPOI.
* Voir le programme complet, exécutable et la sortie attendue.

> **Prérequis** – .NET 6.0+ (ou .NET Core 3.1+), le package NuGet **NPOI**, et une compréhension de base de C# et de la manipulation de fichiers Excel.

---

## Ce dont vous aurez besoin

| Élément | Raison |
|------|--------|
| **.NET SDK** (6.0 ou ultérieur) | Fournit le runtime et les bibliothèques pour `CultureInfo`. |
| **NPOI** (package NuGet `NPOI`) | Vous permet de créer et manipuler des fichiers Excel sans Office installé. |
| **Visual Studio Code**, **Visual Studio**, ou tout IDE C# | Pour compiler et exécuter l'exemple. |
| **Chaîne de date d'ère japonaise** (par ex., `"Reiwa 2/5/1"`) | Illustre l'utilisation du calendrier japonais. |

---

## Étape 1 : Installer NPOI

Ouvrez un terminal dans le dossier de votre projet et exécutez :

```bash
dotnet add package NPOI --version 2.6.1
```

Le package fournit les types `IWorkbook`, `ISheet` et `ICell` utilisés plus tard.

---

## Étape 2 : Créer un CultureInfo qui utilise le calendrier japonais

Le calendrier japonais est un calendrier basé sur les ères. Vous devez demander la variante *Japanese* de la locale `ja-JP` et définir explicitement le calendrier sur `JapaneseCalendar`.

```csharp
using System;
using System.Globalization;

// Create a CultureInfo based on Japanese locale and switch its calendar.
CultureInfo japaneseCulture = new CultureInfo("ja-JP");
japaneseCulture.DateTimeFormat.Calendar = new JapaneseCalendar();
```

> **Pourquoi c’est important** – La culture par défaut `ja-JP` utilise le calendrier grégorien. Réaffecter la propriété `Calendar` garantit que les noms d'ères comme *Reiwa* sont reconnus lors de l'analyse.

---

## Étape 3 : Analyser une chaîne de date d'ère japonaise

Maintenant que le `CultureInfo` est configuré, vous pouvez analyser en toute sécurité une chaîne contenant un nom d'ère.

```csharp
// Example Japanese era date: Reiwa 2 (2020) year, May 1st.
string eraDate = "Reiwa 2/5/1";

// Parse using the Japanese CultureInfo created earlier.
DateTime reiwaDate = DateTime.Parse(eraDate, japaneseCulture);
Console.WriteLine($"Parsed DateTime (UTC): {reiwaDate:u}");
```

**Sortie**

```
Parsed DateTime (UTC): 2020-05-01 00:00:00Z
```

La méthode `Parse` interprète *Reiwa 2* comme l'année grégorienne 2020, mois 5, jour 1.

### Cas limite : gestion des ères invalides

Si un utilisateur fournit une ère non prise en charge (par ex., `"Heisei 31/4/30"` après la fin de l’ère Heisei), `DateTime.Parse` lève une `FormatException`. Enveloppez l’appel dans un bloc try‑catch pour fournir un message d’erreur convivial :

```csharp
try
{
    DateTime parsed = DateTime.Parse(input, japaneseCulture);
}
catch (FormatException)
{
    Console.Error.WriteLine($"'{input}' is not a valid Japanese era date.");
}
```

---

## Étape 4 : Écrire le DateTime analysé dans une feuille de calcul Excel

Avec l'objet `DateTime` prêt, vous pouvez le stocker dans une cellule Excel. NPOI formate automatiquement les valeurs `DateTime` en dates Excel.

```csharp
using NPOI.SS.UserModel;
using NPOI.XSSF.UserModel;
using System.IO;

// Create a new workbook and a sheet.
IWorkbook workbook = new XSSFWorkbook();
ISheet sheet = workbook.CreateSheet("Japanese Dates");

// Write the DateTime into cell A1 (row 0, column 0).
IRow row = sheet.CreateRow(0);
ICell cell = row.CreateCell(0);
cell.SetCellValue(reiwaDate);

// Optionally apply a date style that shows the era (Excel does not have a built‑in era format,
// so we keep the Gregorian representation).
ICellStyle dateStyle = workbook.CreateCellStyle();
short dateFormatId = workbook.CreateDataFormat().GetFormat("yyyy-mm-dd");
dateStyle.DataFormat = dateFormatId;
cell.CellStyle = dateStyle;

// Save the workbook to a file.
using (FileStream fs = new FileStream("JapaneseEraDate.xlsx", FileMode.Create, FileAccess.Write))
{
    workbook.Write(fs);
}
Console.WriteLine("Excel file 'JapaneseEraDate.xlsx' created successfully.");
```

**Résultat** – L'ouverture de *JapaneseEraDate.xlsx* affiche la date **2020‑05‑01** dans la cellule A1.

### Pourquoi utiliser NPOI ?

*Fonctionne sur n'importe quelle plateforme* (Windows, Linux, macOS) et ne nécessite **pas** Microsoft Office. Cela rend la solution adaptée aux pipelines CI, aux conteneurs Docker ou au traitement côté serveur.

---

## Étape 5 : Programme complet et exécutable

En réunissant tous les éléments, voici une application console complète qui démontre l’ensemble du flux :

```csharp
// File: Program.cs
using System;
using System.Globalization;
using System.IO;
using NPOI.SS.UserModel;
using NPOI.XSSF.UserModel;

class Program
{
    static void Main()
    {
        // 1️⃣ Configure CultureInfo for the Japanese calendar.
        CultureInfo japaneseCulture = new CultureInfo("ja-JP");
        japaneseCulture.DateTimeFormat.Calendar = new JapaneseCalendar();

        // 2️⃣ Parse a Japanese era date string.
        string eraDate = "Reiwa 2/5/1";
        DateTime reiwaDate;
        try
        {
            reiwaDate = DateTime.Parse(eraDate, japaneseCulture);
            Console.WriteLine($"Parsed DateTime: {reiwaDate:u}");
        }
        catch (FormatException)
        {
            Console.Error.WriteLine($"'{eraDate}' is not a valid Japanese era date.");
            return;
        }

        // 3️⃣ Create an Excel workbook and write the date.
        IWorkbook workbook = new XSSFWorkbook();
        ISheet sheet = workbook.CreateSheet("Japanese Dates");
        IRow row = sheet.CreateRow(0);
        ICell cell = row.CreateCell(0);
        cell.SetCellValue(reiwaDate);

        // Apply a simple Gregorian date format.
        ICellStyle style = workbook.CreateCellStyle();
        short fmt = workbook.CreateDataFormat().GetFormat("yyyy-mm-dd");
        style.DataFormat = fmt;
        cell.CellStyle = style;

        // 4️⃣ Save the workbook.
        const string fileName = "JapaneseEraDate.xlsx";
        using (FileStream fs = new FileStream(fileName, FileMode.Create, FileAccess.Write))
        {
            workbook.Write(fs);
        }

        Console.WriteLine($"Excel file '{fileName}' created successfully.");
    }
}
```

**Comment exécuter**

```bash
dotnet run
```

Après l’exécution, vous trouverez `JapaneseEraDate.xlsx` dans le dossier du projet avec la date correctement analysée.

---

## Pièges courants et conseils de bonnes pratiques

| Piège | Correction / Recommandation |
|---------|----------------------|
| Oublier de définir `japaneseCulture.DateTimeFormat.Calendar` | Assignez toujours une instance de `JapaneseCalendar` ; sinon le nom de l’ère n’est pas reconnu. |
| Utiliser `DateTime.TryParse` sans le `CultureInfo` personnalisé | Passez le même `japaneseCulture` à `TryParse` pour garder un comportement cohérent. |
| S’attendre à ce qu’Excel affiche le nom de l’ère | Les formats de date intégrés d’Excel sont uniquement grégoriens. Si vous avez besoin d’afficher l’ère, stockez la chaîne originale dans une colonne séparée ou créez un format texte personnalisé. |
| Ne pas libérer le `FileStream` | Utilisez un bloc `using` (comme indiqué) pour garantir que le handle du fichier est libéré rapidement. |
| Mélanger des objets `CultureInfo` entre threads | `CultureInfo` est sûr pour les lectures simultanées, mais évitez de modifier sa propriété `Calendar` après la configuration initiale. |

---

## Conclusion

Vous savez maintenant comment **utiliser CultureInfo du calendrier japonais** en C# pour analyser avec précision des dates d’ère japonaise et écrire le `DateTime` résultant dans une feuille de calcul Excel avec NPOI. L’exemple complet couvre la configuration, l’analyse, la gestion des erreurs et la sortie Excel, vous offrant une base solide pour tout scénario de reporting ou d’échange de données internationalisé.

Ensuite, vous pourriez explorer :

* **Formater les dates avec du texte personnalisé** pour conserver le nom de l’ère dans Excel.
* **Lire les dates depuis Excel** en utilisant `cell.DateCellValue` tout en respectant le calendrier japonais.
* **Appliquer la même technique** à d’autres calendriers basés sur les ères (par ex., le calendrier bouddhiste thaï) en remplaçant `JapaneseCalendar` par la sous‑classe `Calendar` appropriée.

N’hésitez pas à expérimenter avec différentes chaînes d’ère, des ensembles de données plus volumineux, ou à intégrer cette logique dans des API ASP.NET Core qui génèrent des rapports Excel à la volée. Bon codage !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités d’API supplémentaires et à explorer des approches d’implémentation alternatives dans vos propres projets.

- [Créer un classeur Excel avec des dates du calendrier japonais – Guide complet](/cells/english/net/excel-custom-number-date-formatting/create-excel-workbook-with-japanese-calendar-dates-full-guid/)
- [Analyser les dates d’ère japonaise dans Excel – Guide complet pour les développeurs C#](/cells/english/net/data-loading-and-parsing/parse-japanese-era-dates-in-excel-full-guide-for-c-developer/)
- [Comment créer un classeur Excel et analyser des dates japonaises en C#](/cells/english/net/excel-custom-number-date-formatting/how-to-create-excel-workbook-and-parse-japanese-dates-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}