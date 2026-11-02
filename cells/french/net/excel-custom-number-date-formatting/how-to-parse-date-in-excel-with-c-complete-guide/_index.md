---
category: general
date: 2026-05-23
description: Comment analyser une date à partir d’une cellule Excel en C#. Découvrez
  les astuces de format de nombre personnalisé d’Excel, lisez la date d’une cellule
  et appliquez un format personnalisé pour des résultats précis.
draft: false
keywords:
- how to parse date
- custom number format excel
- read date from cell
- format excel cell date
- apply custom format
language: fr
og_description: Comment analyser une date à partir d’une cellule Excel en C#. Ce tutoriel
  montre comment appliquer un format numérique personnalisé dans Excel, lire la date
  d’une cellule et formater correctement la date d’une cellule Excel.
og_title: Comment analyser une date dans Excel avec C# – Guide complet
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: How to parse date from an Excel cell using C#. Learn custom number
    format Excel tricks, read date from cell, and apply custom format for accurate
    results.
  headline: How to Parse Date in Excel with C# – Complete Guide
  type: TechArticle
- description: How to parse date from an Excel cell using C#. Learn custom number
    format Excel tricks, read date from cell, and apply custom format for accurate
    results.
  name: How to Parse Date in Excel with C# – Complete Guide
  steps:
  - name: Why a Custom Format Works
    text: Excel stores dates as serial numbers internally. By applying a locale‑aware
      format, Excel attempts to *interpret* the underlying text according to the pattern.
      The `[$-ja-JP]` prefix forces the Japanese calendar rules, while the rest of
      the pattern maps the characters to year, month, and day.
  - name: 1. Parsing European Dates (e.g., “12/05/2021” in French)
    text: '```csharp firstCell.PutValue("12/05/2021"); // day/month/year Style frStyle
      = workbook.CreateStyle(); frStyle.Custom = "[$-fr-FR]dd/mm/yyyy"; firstCell.SetStyle(frStyle);
      DateTime frDate = firstCell.DateTimeValue; // 2021-05-12 ```'
  - name: 2. When the Cell Already Contains a Serial Date
    text: 'If the source Excel file already stores a true date value, you can skip
      the custom format entirely:'
  - name: 3. Fallback to Manual Parsing
    text: 'Sometimes data is messy (extra spaces, hidden characters). A safe fallback
      is:'
  type: HowTo
tags:
- Excel
- C#
- Date Parsing
title: Comment analyser une date dans Excel avec C# – Guide complet
url: /fr/net/excel-custom-number-date-formatting/how-to-parse-date-in-excel-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment analyser une date dans Excel avec C# – Guide complet

Vous vous êtes déjà demandé **comment analyser une date** stockée dans une feuille Excel sans devoir manipuler manuellement des conversions de chaînes ? Vous n'êtes pas seul. Que vous récupériez des dates fiscales japonaises, des combinaisons mois‑jour européennes, ou toute chaîne spécifique à une locale, obtenir un `DateTime` fiable en C# peut ressembler à la poursuite d’une cible mouvante.  

Dans ce tutoriel, nous parcourrons un exemple concret, de bout en bout, qui **applique un format numérique personnalisé Excel** à une cellule texte, puis **lit la date depuis la cellule** en tant que `DateTime` correct. À la fin, vous saurez exactement comment **formater la date d’une cellule Excel**, **appliquer un format personnalisé**, et éviter les pièges courants qui bloquent la plupart des développeurs.

## Prérequis

- .NET 6.0 ou ultérieur (le code fonctionne avec .NET Core, .NET Framework et .NET 5+)
- Une référence à une bibliothèque de feuilles de calcul qui prend en charge la manipulation de styles – l’exemple utilise **Aspose.Cells**, mais les concepts s’appliquent à EPPlus, ClosedXML ou NPOI.
- Connaissances de base en C# (vous avez ça, n’est‑ce pas ?)

> **Astuce pro :** Si vous n’avez pas encore Aspose.Cells, vous pouvez obtenir une version d’essai gratuite sur leur site et l’ajouter via NuGet : `dotnet add package Aspose.Cells`.

## Vue d’ensemble de la solution

1. **Créer un classeur** et cibler la première cellule de la première feuille.  
2. **Insérer une chaîne de date spécifique à une locale** (japonaise dans notre cas).  
3. **Appliquer un format numérique personnalisé** qui indique à Excel de traiter la chaîne comme une date.  
4. **Lire la valeur de la cellule** en tant qu’objet `DateTime`.  

C’est tout le flux – aucune analyse manuelle, aucun gymnaste `DateTime.ParseExact`. Entrons dans le vif du sujet.

---

## Étape 1 : Configurer le classeur et la cellule cible

Tout d’abord, créez un nouveau classeur et récupérez la cellule avec laquelle nous allons travailler. Cela reproduit le scénario « nouveau classeur » que la plupart des traitements par lots utilisent.

```csharp
using Aspose.Cells;

// Create a new workbook
Workbook workbook = new Workbook();

// Get the first worksheet's first cell (A1)
Cell firstCell = workbook.Worksheets[0].Cells[0, 0];
```

> **Pourquoi c’est important :** Initialiser le classeur par programme garantit que nous contrôlons chaque aspect du fichier – aucune surprise de formatage caché. L’objet `Cell` est notre point d’entrée à la fois pour le contenu et le style.

---

## Étape 2 : Insérer une chaîne de date japonaise

Excel reçoit souvent les dates sous forme de texte, surtout lorsque les données proviennent de systèmes hérités. Ici, nous simulons cela en plaçant directement une date d’ère japonaise dans la cellule.

```csharp
// Insert a Japanese date string (令和3年5月12日 = May 12, 2021)
firstCell.PutValue("令和3年5月12日");
```

> **Note de cas limite :** Si la cellule contenait déjà une vraie date Excel (un nombre sériel), vous pourriez ignorer l’étape du format personnalisé. Ce guide se concentre sur le chemin de conversion *texte‑vers‑date*.

---

## Étape 3 : Appliquer un format numérique personnalisé qui interprète le texte comme une date

Vient maintenant la magie : nous indiquons à Excel de traiter la chaîne à l’aide d’un **custom number format Excel** qui respecte la locale japonaise. La chaîne de format `[$-ja-JP]yyyy` extrait le composant année, mais vous pouvez l’étendre aux mois et aux jours selon vos besoins.

```csharp
// Define a style with a custom number format for Japanese locale
Style style = workbook.CreateStyle();
style.Custom = "[$-ja-JP]yyyy\"年\"m\"月\"d\"日\"";

// Apply the style to the cell
firstCell.SetStyle(style);
```

### Pourquoi un format personnalisé fonctionne

Excel stocke les dates sous forme de nombres sériels en interne. En appliquant un format sensible à la locale, Excel tente *d’interpréter* le texte sous‑jacent selon le modèle. Le préfixe `[$-ja-JP]` impose les règles du calendrier japonais, tandis que le reste du modèle mappe les caractères aux années, mois et jours.

> **Alternative :** Si vous avez besoin d’une approche plus générique, vous pouvez utiliser `[$-en-US]mm/dd/yyyy` pour les dates de style américain, ou tout autre code de culture supporté par Windows.

---

## Étape 4 : Récupérer la date analysée en tant qu’objet `DateTime`

Enfin, nous demandons à la cellule son `DateTimeValue`. Aspose.Cells convertit automatiquement le texte formaté en une instance `DateTime` correcte.

```csharp
// Retrieve the cell value as a DateTime
DateTime parsedDate = firstCell.DateTimeValue;

// Output to console for verification
Console.WriteLine($"Parsed date: {parsedDate:yyyy-MM-dd}");
```

**Sortie console attendue**

```
Parsed date: 2021-05-12
```

> **Et si cela renvoie `DateTime.MinValue` ?** Cela signifie généralement que le format ne correspond pas au contenu de la cellule. Vérifiez la chaîne de format personnalisé et assurez‑vous que le code de locale correspond à la langue source.

---

## Bonus : Gestion d’autres locales et variations du monde réel

### 1. Analyse des dates européennes (ex. : “12/05/2021” en français)

```csharp
firstCell.PutValue("12/05/2021"); // day/month/year
Style frStyle = workbook.CreateStyle();
frStyle.Custom = "[$-fr-FR]dd/mm/yyyy";
firstCell.SetStyle(frStyle);
DateTime frDate = firstCell.DateTimeValue; // 2021-05-12
```

### 2. Lorsque la cellule contient déjà une date sérielle

Si le fichier Excel source stocke déjà une vraie valeur de date, vous pouvez ignorer complètement le format personnalisé :

```csharp
DateTime existingDate = firstCell.DateTimeValue; // works out‑of‑the‑box
```

### 3. Repli sur l’analyse manuelle

Parfois les données sont désordonnées (espaces supplémentaires, caractères invisibles). Un repli sûr consiste à :

```csharp
string raw = firstCell.StringValue?.Trim();
if (DateTime.TryParseExact(raw, "yyyy/MM/dd", CultureInfo.InvariantCulture,
                           DateTimeStyles.None, out DateTime fallback))
{
    // use fallback
}
```

Mais l’approche **appliquer un format personnalisé** est généralement plus rapide et moins sujette aux erreurs car elle exploite le moteur d’analyse d’Excel.

---

## Pièges courants et comment les éviter

| Piège | Symptom | Solution |
|-------|---------|----------|
| Code de locale incorrect (`[$-ja-JP]` vs `[$-ja]`) | `DateTimeValue` reste à `1/1/1900` | Vérifiez la chaîne LCID exacte ; utilisez `CultureInfo.GetCultureInfo("ja-JP").LCID` pour être sûr. |
| Guillemets manquants autour du texte statique | Excel traite `"年"` comme un espace réservé et échoue | Entourez les caractères statiques de guillemets doubles, ex. `\"年\"`. |
| Cellule déjà formatée en *Texte* | Format personnalisé ignoré | Effacez d’abord le `NumberFormat` de la cellule : `firstCell.SetStyle(workbook.CreateStyle());` |
| Bibliothèque ne supportant pas la propriété `Custom` | Erreur de compilation | Passez à une bibliothèque qui expose les formats numériques personnalisés (Aspose.Cells, EPPlus, ClosedXML). |

---

## Exemple complet fonctionnel (prêt à copier‑coller)

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook and get target cell
        Workbook workbook = new Workbook();
        Cell firstCell = workbook.Worksheets[0].Cells[0, 0];

        // 2️⃣ Insert Japanese date string
        firstCell.PutValue("令和3年5月12日");

        // 3️⃣ Apply custom number format for Japanese locale
        Style style = workbook.CreateStyle();
        style.Custom = "[$-ja-JP]yyyy\"年\"m\"月\"d\"日\"";
        firstCell.SetStyle(style);

        // 4️⃣ Retrieve parsed DateTime
        DateTime parsedDate = firstCell.DateTimeValue;

        // Verify the result
        Console.WriteLine($"Parsed date: {parsedDate:yyyy-MM-dd}");
        // Expected: Parsed date: 2021-05-12

        // Optional: Save the workbook to see the formatted cell in Excel
        workbook.Save("ParsedDateExample.xlsx");
    }
}
```

Exécutez le programme, ouvrez `ParsedDateExample.xlsx`, et vous verrez la cellule **A1** afficher `2021年5月12日` tandis que la valeur sous‑jacente est une vraie date Excel.

---

## Conclusion

Nous avons couvert **comment analyser des chaînes de date** dans Excel avec C# en **appliquant un custom number format Excel** puis en **lisant la date depuis la cellule** en tant que `DateTime` natif. Points clés :

- Utilisez un format personnalisé sensible à la locale (`[$-ja-JP]…`) pour laisser Excel faire le gros du travail.  
- Accédez à `Cell.DateTimeValue` pour obtenir un `DateTime` propre, sans analyse manuelle.  
- Adaptez la chaîne de format pour d’autres cultures, et vérifiez toujours avec un petit dump console.  

À partir d’ici, vous pouvez **formater la date d’une cellule Excel** pour des rapports, injecter le `DateTime` dans des bases de données, ou effectuer des calculs directement dans votre application C#. Expérimentez avec différentes locales, combinez plusieurs cellules, ou traitez par lots des feuilles entières – les mêmes principes s’appliquent.

Vous avez un format de date étrange que vous n’arrivez pas à décoder ? Laissez un commentaire, et nous résoudrons le problème ensemble. Bon codage !


## Tutoriels associés

- [Excel Custom Number and Date Formatting](/cells/english/net/excel-custom-number-date-formatting/)
- [Mastering Data Presentation in Excel: Number and Custom Date Formatting with Aspose.Cells for Java](/cells/english/java/formatting/aspose-cells-java-data-formatting-excel/)
- [Excel Custom Number Date Formatting](/cells/german/net/excel-custom-number-date-formatting/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}