---
category: general
date: 2026-06-30
description: Créer une mise en forme conditionnelle dans un classeur Excel à l'aide
  d'Aspose.Cells. Apprenez à définir l'arrière‑plan des cellules, à classer les cellules
  et à générer le fichier de façon programmatique.
draft: false
keywords:
- create conditional formatting
- create excel workbook
- set cell background
- how to rank cells
- how to use aspose
language: fr
og_description: Créez une mise en forme conditionnelle dans un classeur Excel en utilisant
  Aspose.Cells. Suivez ce tutoriel complet pour définir le fond des cellules, classer
  les cellules et automatiser Excel.
og_title: Créer une mise en forme conditionnelle dans Excel avec Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Create conditional formatting in an Excel workbook using Aspose.Cells.
    Learn how to set cell background, rank cells, and build the file programmatically.
  headline: Create Conditional Formatting in Excel with Aspose.Cells – Step‑by‑Step
    Guide
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Créer une mise en forme conditionnelle dans Excel avec Aspose.Cells – Guide
  étape par étape
url: /fr/net/excel-conditional-formatting/create-conditional-formatting-in-excel-with-aspose-cells-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer une mise en forme conditionnelle dans Excel avec Aspose.Cells – Guide étape par étape

Vous vous êtes déjà demandé comment **créer une mise en forme conditionnelle** dans un fichier Excel sans ouvrir l'interface utilisateur ? Vous n'êtes pas seul. De nombreux développeurs doivent **créer des classeurs Excel** à la volée, et le faire de façon programmatique fait gagner des heures de travail manuel. Dans ce tutoriel, nous vous montrerons exactement comment **créer une mise en forme conditionnelle**, styliser les cellules, et même classer les meilleures valeurs—tout cela avec la puissante bibliothèque Aspose.Cells pour .NET.

Nous parcourrons un exemple concret : générer une feuille de scores, mettre en évidence les scores élevés en vert clair, et appliquer un arrière‑plan doré aux 3 meilleurs performants. À la fin, vous saurez **comment définir l'arrière‑plan d'une cellule**, **comment classer les cellules**, et **comment utiliser Aspose** pour une automatisation Excel sophistiquée. Pas de superflu, juste une solution complète et exécutable que vous pouvez intégrer à n'importe quel projet C#.

## Ce que vous apprendrez

- Comment **créer des classeurs Excel** en utilisant Aspose.Cells  
- Comment remplir une plage avec des données aléatoires (scores)  
- Comment **définir l'arrière‑plan d'une cellule** avec des couleurs unies  
- Comment appliquer une règle basée sur une formule pour **classer les cellules** et mettre en évidence les trois meilleures  
- Comment enregistrer le résultat sous forme de fichier .xlsx  

Prérequis : .NET 6+ (ou .NET Framework 4.6+), Visual Studio (ou tout IDE C#), et une référence au package NuGet Aspose.Cells. Si vous n’avez jamais utilisé Aspose auparavant, ne vous inquiétez pas — nous couvrirons **comment utiliser Aspose** depuis le début.

---

![Create conditional formatting example](https://example.com/images/create-conditional-formatting.png "Screenshot showing conditional formatting in the generated Excel file")

*Texte alternatif de l'image : exemple de mise en forme conditionnelle dans un classeur Excel généré avec Aspose.Cells.*

## Comment créer un classeur Excel avec Aspose.Cells

Tout d'abord : vous avez besoin d'un objet workbook avec lequel travailler. Aspose.Cells rend cela possible en une seule ligne.

```csharp
using Aspose.Cells;
using System.Drawing;

void CreateConditionalFormattingWorkbook()
{
    // Step 1: Instantiate a new workbook and give the first sheet a friendly name
    Workbook workbook = new Workbook();                 // creates an empty workbook
    Worksheet sheet = workbook.Worksheets[0];           // grab the default worksheet
    sheet.Name = "Scores";                              // rename it to something meaningful
```

Pourquoi renommer la feuille ? Un nom clair (comme **Scores**) facilite les références ultérieures, surtout lorsque vous partagez le fichier avec des utilisateurs non techniques.  

Maintenant que le classeur existe, remplissons la colonne A avec des scores aléatoires.

## Comment remplir les données – Créer des scores aléatoires

```csharp
    // Step 2: Populate A2:A21 with random values between 40 and 99
    Random random = new Random();
    for (int i = 0; i < 20; i++)               // 20 rows of data
    {
        sheet.Cells[i + 1, 0].PutValue(random.Next(40, 100));
    }
```

Une petite note : `PutValue` détecte automatiquement le type de données, vous n’avez donc pas besoin de le convertir en `int`. La boucle commence à `i = 0` mais écrit dans la ligne `i + 1` car les lignes d’Excel sont indexées à partir de 1 alors que la collection `Cells` commence à 0.

## Comment définir l'arrière‑plan d'une cellule pour les scores élevés

Nous allons maintenant **créer une mise en forme conditionnelle** qui colore tout score ≥ 80 en vert clair.

```csharp
    // Step 3: Define a conditional formatting range (A2:A21)
    int firstRow = 1, lastRow = 20;                     // zero‑based indices for rows 2‑21
    int cfIndex = sheet.ConditionalFormattings.Add(firstRow, 0, lastRow, 0);
    ConditionalFormatting cf = sheet.ConditionalFormattings[cfIndex];

    // Add a rule: cell value >= 80 → light‑green background
    FormatCondition highScoreCondition = cf.AddCondition(
        FormatConditionType.CellValue,
        OperatorType.GreaterOrEqual,
        "80");

    highScoreCondition.Style.ForegroundColor = Color.LightGreen;
    highScoreCondition.Style.Pattern = BackgroundType.Solid;
```

La propriété `ForegroundColor` contrôle la couleur de remplissage, tandis que `Pattern = BackgroundType.Solid` indique à Excel d’utiliser un remplissage uni plutôt qu’un dégradé ou un motif. C’est le cœur de **comment définir l'arrière‑plan d'une cellule** en fonction d’un seuil numérique.

## Comment classer les cellules et mettre en évidence les 3 meilleurs

Le classement est un peu plus compliqué car nous avons besoin d’une formule qui évalue chaque cellule par rapport à l’ensemble de la plage. Aspose.Cells vous permet d’utiliser la même syntaxe de formule Excel que vous taperiez dans l’interface.

```csharp
    // Step 4: Add a formula‑based rule to color the top‑3 scores gold
    FormatCondition topThreeCondition = cf.AddCondition(
        FormatConditionType.Formula,
        null,
        null);

    // The formula uses the RANK function; note the absolute references ($) lock the range
    topThreeCondition.Formula1 = "=RANK(A2,$A$2:$A$21)<=3";

    topThreeCondition.Style.ForegroundColor = Color.Gold;
    topThreeCondition.Style.Pattern = BackgroundType.Solid;
```

Pourquoi `A2` dans la formule ? Aspose évalue la formule de façon relative à chaque cellule de la plage, ainsi `A2` se décale automatiquement vers `A3`, `A4`, etc., au fur et à mesure que la règle est appliquée ligne par ligne. La fonction `RANK` renvoie la position d’une valeur dans la plage spécifiée, et la partie `<=3` garantit que seules les trois meilleures scores obtiennent le remplissage doré.

## Comment enregistrer le classeur

```csharp
    // Step 5: Persist the workbook to disk
    workbook.Save("YOUR_DIRECTORY/Scores_ConditionalFormatting.xlsx");
}
```

Remplacez `YOUR_DIRECTORY` par un chemin absolu ou relatif où votre application peut écrire. Après avoir exécuté la méthode, ouvrez le fichier dans Excel et vous verrez :

- Cellules vert clair pour tout score ≥ 80  
- Cellules dorées pour les trois scores les plus élevés, qu’ils soient ou non ≥ 80  

C’est le pipeline complet de **création de mise en forme conditionnelle**.

---

## Exemple complet et exécutable

Voici à nouveau la méthode complète, prête à être copiée‑collée dans une application console ou toute classe C# :

```csharp
using Aspose.Cells;
using System.Drawing;

void CreateConditionalFormattingWorkbook()
{
    // Step 1: Create a new workbook and name the first worksheet
    Workbook workbook = new Workbook();
    Worksheet sheet = workbook.Worksheets[0];
    sheet.Name = "Scores";

    // Step 2: Fill column A (A2:A21) with random scores between 40 and 99
    Random random = new Random();
    for (int i = 0; i < 20; i++)
    {
        sheet.Cells[i + 1, 0].PutValue(random.Next(40, 100));
    }

    // Step 3: Highlight scores >= 80 with a light‑green background
    int firstRow = 1, lastRow = 20;
    int cfIndex = sheet.ConditionalFormattings.Add(firstRow, 0, lastRow, 0);
    ConditionalFormatting cf = sheet.ConditionalFormattings[cfIndex];
    FormatCondition highScoreCondition = cf.AddCondition(
        FormatConditionType.CellValue,
        OperatorType.GreaterOrEqual,
        "80");
    highScoreCondition.Style.ForegroundColor = Color.LightGreen;
    highScoreCondition.Style.Pattern = BackgroundType.Solid;

    // Step 4: Color the top‑3 scores with a gold background using a formula rule
    FormatCondition topThreeCondition = cf.AddCondition(
        FormatConditionType.Formula,
        null,
        null);
    topThreeCondition.Formula1 = "=RANK(A2,$A$2:$A$21)<=3";
    topThreeCondition.Style.ForegroundColor = Color.Gold;
    topThreeCondition.Style.Pattern = BackgroundType.Solid;

    // Step 5: Save the workbook
    workbook.Save("YOUR_DIRECTORY/Scores_ConditionalFormatting.xlsx");
}
```

### Résultat attendu

Lorsque vous ouvrez `Scores_ConditionalFormatting.xlsx` :

- Les cellules avec des valeurs **80** ou plus brillent en vert clair.  
- Les trois plus grands nombres (même s’ils sont inférieurs à 80) apparaissent avec un arrière‑plan **doré**.  
- Toutes les autres cellules conservent l’arrière‑plan blanc par défaut.

Cet indice visuel indique instantanément à un manager qui sont les meilleurs performants, sans aucun tri manuel.

---

## Questions fréquentes et cas limites

**Et si j’ai besoin de plus de trois meilleurs scores ?**  
Il suffit de changer la partie `<=3` de la formule en `<=5` (ou tout autre nombre). La règle s’adaptera automatiquement.

**Puis‑je appliquer plusieurs plages de mise en forme ?**  
Absolument. Appelez à nouveau `sheet.ConditionalFormattings.Add` avec une plage différente, puis ajoutez des conditions à ce nouvel objet `ConditionalFormatting`.

**Qu’en est‑il des versions plus anciennes d’Excel ?**  
Aspose.Cells enregistre par défaut au format moderne `.xlsx`, compatible avec Excel 2007 et versions ultérieures. Si vous avez besoin du format `.xls`, passez `SaveFormat.Excel97To2003` à la méthode `Save`.

**Y a‑t‑il un impact sur les performances pour les grandes feuilles ?**  
La mise en forme conditionnelle est stockée comme métadonnées, elle n’affecte donc pas significativement la taille du fichier. Cependant, générer des centaines de milliers de lignes peut augmenter l’utilisation de la mémoire — envisagez de traiter par lots.

---

## Prochaines étapes

Maintenant que vous avez maîtrisé **comment créer une mise en forme conditionnelle**, vous pourriez vouloir explorer :

- **Comment créer des graphiques Excel** programmatique (un autre bijou d’Aspose.Cells)  
- **Comment définir l'arrière‑plan d'une cellule** en fonction de valeurs textuelles (par ex., « Pass/Fail »)  
- **Comment utiliser Aspose.Cells pour la validation des données** et les listes déroulantes  

Chacun de ces sujets s’appuie sur les mêmes fondamentaux que vous venez d’apprendre, vous vous sentirez donc immédiatement à l’aise.

---

## Conclusion

Nous venons de parcourir un exemple complet, de bout en bout, de comment **créer une mise en forme conditionnelle** dans un classeur Excel en utilisant Aspose.Cells. De l’initialisation du classeur, le remplissage des données, **définir l’arrière‑plan d’une cellule**, classer les meilleurs performants, jusqu’à l’enregistrement final du fichier, chaque étape a été couverte en gardant à l’esprit **comment classer les cellules** et **comment utiliser Aspose**.

Exécutez le code, ajustez les seuils, et voyez à quel point vous pouvez rapidement générer des rapports soignés pour n’importe quel scénario d’entreprise. Vous avez une variante à partager ? Laissez un commentaire ci‑dessous—bon codage !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités supplémentaires de l’API et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Automatiser la mise en forme conditionnelle Excel avec Aspose.Cells pour Java : Guide complet](/cells/english/java/formatting/automate-conditional-formatting-excel-aspose-cells-java/)
- [Comment créer et formater des cellules Excel avec Aspose.Cells pour Java : Guide étape par étape](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)
- [Créer un classeur Excel avec Aspose.Cells en Java : Guide étape par étape](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}