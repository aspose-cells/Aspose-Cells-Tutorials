---
category: general
date: 2026-03-22
description: Apprenez à formater la date/heure au format ISO lors de l'extraction
  d'une date depuis Excel et à afficher la date ISO à l'aide d'Aspose.Cells en C#.
draft: false
keywords:
- format datetime to iso
- extract date from excel
- display iso date
- Aspose.Cells date parsing
- Japanese era dates
language: fr
og_description: Formater la date et l'heure en ISO facilement. Ce guide montre comment
  extraire une date d’Excel et afficher la date ISO avec Aspose.Cells.
og_title: Formater la date/heure en ISO en C# – Tutoriel étape par étape
tags:
- C#
- Aspose.Cells
- DateTime
- Excel
- ISO 8601
title: Formater la date et l'heure au format ISO en C# – Guide complet
url: /fr/net/number-and-display-formats-in-excel/format-datetime-to-iso-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# formater datetime en iso en C# – Guide complet

Vous avez déjà eu besoin de **formater datetime en iso** alors que la source se trouve dans un classeur Excel ? Peut‑être la cellule contient une ère japonaise comme « 令和3年5月1日 » et vous vous demandez comment la transformer en une chaîne propre `2021‑05‑01`. Vous n’êtes pas seul. Dans ce tutoriel nous allons **extraire la date d’Excel**, analyser l’ère japonaise, puis **afficher la date iso** dans la console — le tout avec quelques lignes de C# et Aspose.Cells.

Nous passerons en revue tout ce dont vous avez besoin : le package NuGet requis, le code exact à copier‑coller, pourquoi chaque ligne est importante, et quelques astuces pour les cas limites. À la fin, vous disposerez d’un extrait réutilisable qui formate datetime en iso quel que soit le format original de la valeur Excel.

## Ce dont vous aurez besoin

- .NET 6.0 ou ultérieur (le code compile également sous .NET Framework 4.6+)
- Visual Studio 2022 (ou tout autre éditeur de votre choix)
- **Aspose.Cells for .NET** package NuGet – `Install-Package Aspose.Cells`
- Un fichier Excel (ou un nouveau classeur) contenant une date au format d’ère japonaise

C’est tout. Pas de bibliothèques supplémentaires, pas d’interop COM, juste une méthode unique et bien documentée.

## Étape 1 : Créer un classeur et écrire une date d’ère japonaise  

Tout d’abord, nous avons besoin d’un classeur avec lequel travailler. Si vous avez déjà un fichier Excel, vous pouvez le charger avec `new Workbook("path")`. Pour cet exemple, nous créerons un nouveau classeur en mémoire et y placerons une chaîne d’ère japonaise dans la cellule **A1**.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a fresh workbook
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // 2️⃣ Write a Japanese era date (Reiwa 3 = 2021) into A1
        sheet.Cells["A1"].PutValue("令和3年5月1日");
```

> **Pourquoi faisons‑nous cela :** Aspose.Cells traite les valeurs des cellules comme des chaînes par défaut. En insérant le texte brut de l’ère, nous simulons un scénario réel où un client japonais a saisi des dates dans son calendrier natif.

## Étape 2 : Activer l’analyse d’ère japonaise et extraire la date  

Aspose.Cells peut automatiquement traduire les chaînes d’ère japonaise en objets .NET `DateTime` — à condition de le lui indiquer. Le drapeau `DateTimeParseOptions.EnableJapaneseEra` fait le gros du travail.

```csharp
        // 3️⃣ Retrieve the cell value while enabling Japanese era parsing
        CellValue parsed = sheet.Cells["A1"]
            .GetValue(CellValueType.DateTime, DateTimeParseOptions.EnableJapaneseEra);
```

> **Astuce pro :** Si vous oubliez l’option `EnableJapaneseEra`, la bibliothèque renverra la chaîne originale et votre conversion ultérieure échouera. Vérifiez toujours `parsed.Type` si vous traitez du contenu mixte.

## Étape 3 : Convertir le DateTime analysé en ISO 8601  

Maintenant que nous disposons d’un `DateTime` correct, le transformer en chaîne au format ISO est un jeu d’enfant. Le modèle `"yyyy-MM-dd"` respecte la partie date d’ISO 8601, ce que la plupart des API attendent.

```csharp
        // 4️⃣ Convert to ISO 8601 (yyyy‑MM‑dd) and display it
        string isoDate = parsed.DateTimeValue.ToString("yyyy-MM-dd");
        Console.WriteLine($"ISO date: {isoDate}");
    }
}
```

L’exécution du programme affiche :

```
ISO date: 2021-05-01
```

C’est la **date iso affichée** que vous recherchiez.

## Exemple complet, exécutable  

Voici le bloc de code complet que vous pouvez copier directement dans un projet console. Aucun dépendance cachée, aucune configuration supplémentaire.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Write a Japanese era date into cell A1
        worksheet.Cells["A1"].PutValue("令和3年5月1日");

        // Retrieve the cell value with Japanese era parsing enabled
        CellValue parsedValue = worksheet.Cells["A1"]
            .GetValue(CellValueType.DateTime, DateTimeParseOptions.EnableJapaneseEra);

        // Convert the DateTime to ISO 8601 format and output it
        string isoDate = parsedValue.DateTimeValue.ToString("yyyy-MM-dd");
        Console.WriteLine($"ISO date: {isoDate}");
    }
}
```

> **Sortie attendue :** `ISO date: 2021-05-01`

## Décomposition étape par étape (Pourquoi chaque partie est importante)

| Étape | Ce qui se passe | Pourquoi c’est important |
|------|----------------|---------------------------|
| **Créer le classeur** | Initialise un conteneur Excel en mémoire. | Vous offre un bac à sable pour tester sans toucher au système de fichiers. |
| **PutValue** | Stocke la chaîne brute d’ère japonaise dans **A1**. | Reproduit une saisie réelle ; garantit que le parseur voit le texte exact. |
| **GetValue avec `EnableJapaneseEra`** | Convertit la chaîne d’ère en un .NET `DateTime`. | Gère automatiquement la conversion de calendrier — aucune table de correspondance manuelle nécessaire. |
| **`ToString("yyyy-MM-dd")`** | Formate le `DateTime` en ISO 8601. | Assure une chaîne de date indépendante de la culture, triable et acceptée par les API REST, bases de données, etc. |
| **Console.WriteLine** | Affiche la date ISO finale. | Confirme que toute la chaîne fonctionne de bout en bout. |

## Gestion des variations courantes  

### 1. Emplacements de cellule différents  

Si votre date se trouve en **B2** ou dans une plage nommée, remplacez simplement `"A1"` par l’adresse appropriée :

```csharp
worksheet.Cells["B2"].PutValue("令和2年12月31日");
var value = worksheet.Cells["B2"]
    .GetValue(CellValueType.DateTime, DateTimeParseOptions.EnableJapaneseEra);
```

### 2. Plusieurs dates dans une colonne  

Lorsque vous devez **extraire la date d’Excel** pour de nombreuses lignes, parcourez la plage utilisée :

```csharp
int lastRow = worksheet.Cells.MaxDataRow;
for (int i = 0; i <= lastRow; i++)
{
    var cell = worksheet.Cells[i, 0]; // column A
    var cv = cell.GetValue(CellValueType.DateTime, DateTimeParseOptions.EnableJapaneseEra);
    string iso = cv.DateTimeValue.ToString("yyyy-MM-dd");
    Console.WriteLine($"Row {i + 1}: {iso}");
}
```

### 3. Solution de secours pour les dates non‑ère  

Si une cellule contient déjà une chaîne de date standard, le parseur fonctionne toujours, mais vous pouvez ajouter une sécurité :

```csharp
CellValue cv = cell.GetValue(CellValueType.DateTime,
    DateTimeParseOptions.EnableJapaneseEra | DateTimeParseOptions.TryParse);
```

Le drapeau `TryParse` empêche les exceptions et renvoie la valeur originale si la conversion échoue.

### 4. Composante temporelle  

Si vous avez besoin de la partie heure également, utilisez `"yyyy-MM-ddTHH:mm:ss"` :

```csharp
string isoDateTime = parsedValue.DateTimeValue.ToString("yyyy-MM-ddTHH:mm:ss");
```

Cela produit un horodatage ISO 8601 complet (`2021-05-01T00:00:00`).

## Aide visuelle  

![exemple de formatage datetime en iso](image.png "Un exemple de formatage datetime en iso en C#")

*Texte alternatif :* *exemple de formatage datetime en iso montrant la sortie console*

## Questions fréquentes  

- **Puis‑je l’utiliser avec des fichiers .xls ?**  
  Oui. Aspose.Cells prend en charge `.xls`, `.xlsx`, `.csv` et de nombreux autres formats dès le départ.

- **Que faire si le classeur est protégé par mot de passe ?**  
  Chargez‑le avec `new Workbook("file.xlsx", new LoadOptions { Password = "secret" })`.

- **Le format ISO dépend‑il de la locale ?**  
  Non. Le modèle `"yyyy-MM-dd"` est indépendant de la culture, garantissant la même chaîne sur n’importe quelle machine.

- **Cela fonctionne‑t‑il sur .NET Core ?**  
  Absolument — Aspose.Cells est compatible avec .NET Standard 2.0.

## Conclusion  

Nous avons vu comment **formater datetime en iso** en **extraitant la date d’Excel**, en analysant les chaînes d’ère japonaise, puis en **affichant la date iso** dans la console. Les étapes essentielles — créer un classeur, écrire ou charger le texte d’ère, activer l’analyse d’ère japonaise, et formater avec `ToString("yyyy-MM-dd")` — sont tout ce dont vous avez besoin dans la plupart des scénarios.

Ensuite, vous pourriez :

- Écrire les dates ISO dans une autre colonne pour un traitement en aval.
- Exporter le classeur transformé en CSV pour une importation massive.
- Combiner cette logique avec une API web qui accepte les téléchargements Excel et renvoie des dates ISO encodées en JSON.

N’hésitez pas à expérimenter avec différents formats de date, fuseaux horaires, ou même des calendriers personnalisés. La flexibilité d’Aspose.Cells vous évite rarement les impasses.

Bon codage, et que toutes vos dates soient parfaitement conformes à l’ISO !  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}