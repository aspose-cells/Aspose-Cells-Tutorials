---
category: general
date: 2026-03-30
description: Apprenez à formater les dates au format ISO tout en lisant les valeurs
  datetime d’Excel et à extraire les données datetime d’Excel à l’aide d’Aspose.Cells
  en C#.
draft: false
keywords:
- format date iso
- read excel datetime
- extract datetime excel
- Aspose.Cells date parsing
- Japanese era dates
language: fr
og_description: formater la date ISO à partir des données Excel avec Aspose.Cells.
  Ce guide montre comment lire les dates/heure Excel, extraire les valeurs datetime
  d’Excel et produire des dates ISO.
og_title: Format de date ISO à partir d’Excel – Tutoriel C# étape par étape
tags:
- C#
- Excel
- DateTime
- Aspose.Cells
title: Format de date ISO depuis Excel – Guide complet C#
url: /fr/net/excel-custom-number-date-formatting/format-date-iso-from-excel-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# formater date iso depuis Excel – Guide complet C#

Vous avez déjà eu besoin de **formater date iso** en extrayant des dates d’une feuille Excel ? Peut‑être que vous devez gérer des dates d’ère japonaise, ou que vous voulez simplement une chaîne `yyyy‑MM‑dd` propre pour le corps d’une API. Dans ce tutoriel, vous verrez exactement comment **read Excel datetime** les cellules, **extract datetime Excel** les valeurs, et les transformer en format ISO‑8601 — sans aucune supposition.

Nous parcourrons un exemple concret qui utilise Aspose.Cells, explique pourquoi chaque ligne est importante, et vous montre le résultat final que vous pouvez copier‑coller dans votre projet. À la fin, vous serez capable de gérer des chaînes d’ère particulières comme « 令和3年5月1日 » et de produire une date ISO standard, prête pour les bases de données, le JSON ou tout autre usage.

## Prérequis

- .NET 6.0 ou version ultérieure (le code fonctionne également avec .NET Framework)  
- Aspose.Cells pour .NET (version d’essai gratuite ou version sous licence)  
- Connaissances de base en C# et en concepts Excel  
- Visual Studio ou tout éditeur C# de votre choix  

Aucun package NuGet supplémentaire n’est requis en dehors d’Aspose.Cells, donc l’installation est très simple.

---

## Étape 1 : Créer un classeur et cibler la première feuille

La première chose à faire est d’instancier un nouvel objet `Workbook`. Cela vous donne une représentation en mémoire d’un fichier Excel, que vous pouvez ensuite manipuler ou lire.

```csharp
using Aspose.Cells;
using System.Globalization;

// Step 1: Initialize a new workbook and grab the first worksheet
Workbook workbook = new Workbook();                 // creates an empty .xlsx
Worksheet worksheet = workbook.Worksheets[0];      // the default sheet is "Sheet1"
```

*Pourquoi c’est important :*  
Créer le classeur par programme vous évite de devoir gérer des fichiers physiques pendant les tests. Cela garantit également que la référence à la feuille est toujours valide — aucune surprise de référence nulle plus tard lorsque vous essayez de **read Excel datetime** les valeurs.

---

## Étape 2 : Écrire une chaîne de date d’ère japonaise dans une cellule

Notre objectif est de démontrer l’analyse d’une date non grégorienne. Nous placerons la chaîne d’ère directement dans la cellule **A1**.

```csharp
// Step 2: Insert a Japanese era date string into cell A1
worksheet.Cells["A1"].PutValue("令和3年5月1日");
```

*Astuce :* Si vous extrayez les données d’un classeur existant, vous sauteriez l’appel `PutValue` et vous référeriez simplement à la cellule qui contient déjà la date. L’essentiel est que la cellule contienne une **string** représentant une date du calendrier lunisolaire japonais.

---

## Étape 3 : Configurer une culture qui comprend le calendrier lunisolaire japonais

La classe `CultureInfo` de .NET vous permet de spécifier comment les dates doivent être interprétées. En remplaçant le calendrier grégorien par défaut par `JapaneseLunisolarCalendar`, vous fournissez au parseur le contexte nécessaire.

```csharp
// Step 3: Set up a culture using the Japanese lunisolar calendar
CultureInfo japaneseCulture = new CultureInfo("ja-JP");
japaneseCulture.DateTimeFormat.Calendar = new JapaneseLunisolarCalendar();
```

*Pourquoi faisons‑nous cela :*  
Si vous essayiez d’analyser « 令和3年5月1日 » avec la culture par défaut, .NET lèverait une `FormatException`. En injectant le calendrier lunisolaire, le runtime sait exactement comment mapper « 令和3年 » (la 3ᵉ année de l’ère Reiwa) à l’année grégorienne 2021.

---

## Étape 4 : Analyser la valeur de la cellule en `DateTime` avec la culture configurée

Voici le cœur de l’opération — transformer cette chaîne d’ère en un véritable objet `DateTime`. Aspose.Cells propose une surcharge pratique de `GetDateTime` qui accepte un `CultureInfo`.

```csharp
// Step 4: Retrieve the cell value as a DateTime, respecting the Japanese culture
DateTime parsedDate = worksheet.Cells["A1"].GetDateTime(japaneseCulture);
```

*Ce qui se passe en coulisses :*  
`GetDateTime` lit la chaîne brute, applique les règles du calendrier de la culture fournie, et renvoie un `DateTime` qui représente le même instant dans le calendrier grégorien. C’est le moment où vous **extract datetime Excel** les données sous une forme exploitable en .NET.

---

## Étape 5 : Produire la date analysée au format ISO 8601

Enfin, nous formatons le `DateTime` en chaîne ISO — `yyyy‑MM‑dd` — qui est universellement accepté par les API, les bases de données et les frameworks front‑end.

```csharp
// Step 5: Print the date in ISO format (e.g., 2021-05-01)
Console.WriteLine(parsedDate.ToString("yyyy-MM-dd")); // Output: 2021-05-01
```

*Pourquoi ISO ?*  
ISO 8601 élimine toute ambiguïté. « 05/01/2021 » peut signifier le 1ᵉʳ mai ou le 5 janvier selon la locale. `2021-05-01` est parfaitement clair, c’est pourquoi nous **format date iso** dans presque tous les scénarios d’intégration.

---

## Exemple complet fonctionnel

Voici le programme complet, prêt à être exécuté. Copiez‑le dans un projet console, ajoutez la référence Aspose.Cells, puis appuyez sur **F5**.

```csharp
using Aspose.Cells;
using System;
using System.Globalization;

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook and select the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Write a Japanese era date string into cell A1
        worksheet.Cells["A1"].PutValue("令和3年5月1日");

        // 3️⃣ Set up Japanese lunisolar culture
        CultureInfo japaneseCulture = new CultureInfo("ja-JP");
        japaneseCulture.DateTimeFormat.Calendar = new JapaneseLunisolarCalendar();

        // 4️⃣ Parse the cell value as DateTime using the culture
        DateTime parsedDate = worksheet.Cells["A1"].GetDateTime(japaneseCulture);

        // 5️⃣ Output the date in ISO format
        Console.WriteLine(parsedDate.ToString("yyyy-MM-dd")); // 2021-05-01
    }
}
```

**Sortie attendue**

```
2021-05-01
```

Exécutez‑le une fois, et vous verrez la date formatée en ISO affichée dans la console. C’est toute la chaîne, de **read Excel datetime** à **format date iso**.

---

## Gestion des cas limites courants

### 1. Cellules contenant de vrais nombres de date Excel

Parfois Excel stocke les dates sous forme de nombres sériels (par ex. `44204`). Dans ce cas, aucune culture n’est nécessaire ; il suffit d’appeler `GetDateTime()` sans paramètres :

```csharp
DateTime serialDate = worksheet.Cells["B2"].GetDateTime(); // B2 holds a numeric date
Console.WriteLine(serialDate.ToString("yyyy-MM-dd"));
```

### 2. Cellules vides ou invalides

Si une cellule est vide ou contient une chaîne non analysable, `GetDateTime` lèvera une exception. Enveloppez l’appel dans un `try/catch` ou vérifiez d’abord `IsDateTime` :

```csharp
if (worksheet.Cells["C3"].Type == CellValueType.IsDateTime)
{
    DateTime safeDate = worksheet.Cells["C3"].GetDateTime();
    Console.WriteLine(safeDate.ToString("yyyy-MM-dd"));
}
else
{
    Console.WriteLine("Cell C3 does not contain a valid date.");
}
```

### 3. Formats d’ère différents

Les autres ères japonaises (Heisei, Showa) suivent le même schéma. Le même `JapaneseLunisolarCalendar` les gérera automatiquement, vous n’avez donc pas besoin de logique supplémentaire — il suffit de fournir la chaîne.

---

## Astuces pro & pièges à éviter

- **Performance :** Lors du traitement de gros classeurs, réutilisez une même instance de `CultureInfo` au lieu d’en créer une nouvelle à chaque itération.  
- **Sécurité des threads :** Les objets `CultureInfo` deviennent en lecture‑seule après la définition du calendrier, ils sont donc sûrs à partager entre threads.  
- **Licence Aspose.Cells :** Si vous utilisez la version d’essai gratuite, rappelez‑vous que certaines fonctionnalités peuvent être limitées après l’expiration de la période d’essai. Le parsing de dates présenté ici fonctionne tant en mode essai qu’en mode sous licence.  
- **Fuseaux horaires :** Le `DateTime` obtenu est **unspecified** (sans fuseau). Si vous avez besoin d’UTC, appelez `DateTime.SpecifyKind(parsedDate, DateTimeKind.Utc)` ou convertissez avec `TimeZoneInfo`.

---

## Conclusion

Nous avons couvert tout ce qu’il faut pour **format date iso** à partir d’un classeur Excel avec C#. En partant d’une chaîne d’ère japonaise brute, nous **read Excel datetime**, configurons la culture appropriée, **extract datetime excel**, puis produisons une chaîne ISO‑8601 propre. Cette approche fonctionne pour n’importe quelle représentation de date qu’Excel peut vous fournir, qu’il s’agisse d’un nombre sériel, d’une chaîne locale ou d’un format d’ère traditionnel.

Et après ? Essayez de parcourir toute une colonne de dates, d’écrire les résultats ISO dans une nouvelle feuille, ou de les injecter directement dans un payload JSON pour un service web. Si vous êtes curieux des autres systèmes de calendrier (hébreu, islamique), Aspose.Cells et le `CultureInfo` de .NET rendent ces expériences tout aussi simples.

Des questions ou un format de date récalcitrant ? Laissez un commentaire ci‑dessous, et bon codage !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}