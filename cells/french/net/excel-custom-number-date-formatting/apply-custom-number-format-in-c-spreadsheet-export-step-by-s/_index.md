---
category: general
date: 2026-04-07
description: Appliquez un format de nombre personnalisé à une cellule de feuille de
  calcul et apprenez comment formater les nombres dans une feuille de calcul lors
  de l'exportation de la valeur de la cellule avec C#. Guide rapide et complet.
draft: false
keywords:
- apply custom number format
- format number in spreadsheet
- how to format numeric cell
- how to export cell value
language: fr
og_description: Appliquez un format numérique personnalisé à une cellule de feuille
  de calcul et exportez‑la sous forme de chaîne formatée. Apprenez à formater les
  nombres dans une feuille de calcul et à exporter la valeur de la cellule.
og_title: Appliquer un format de nombre personnalisé – Tutoriel complet d'exportation
  C#
tags:
- C#
- Spreadsheet
- Number Formatting
title: Appliquer un format de nombre personnalisé dans l'exportation de feuille de
  calcul C# – Guide étape par étape
url: /fr/net/excel-custom-number-date-formatting/apply-custom-number-format-in-c-spreadsheet-export-step-by-s/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Appliquer un format numérique personnalisé dans l'exportation de feuille de calcul C# – Tutoriel complet

Vous avez déjà eu besoin d'**appliquer un format numérique personnalisé** à une cellule puis d'extraire cette chaîne formatée d'une feuille de calcul ? Vous n'êtes pas seul. De nombreux développeurs se heurtent à un mur lorsqu'ils découvrent que la valeur brute est renvoyée au lieu de la chaîne jolie et adaptée à la locale qu'ils attendent. Dans ce guide, nous vous montrerons exactement comment **formater un nombre dans une feuille de calcul** et comment exporter la valeur d'une cellule en tant que chaîne formatée en utilisant une bibliothèque de feuilles de calcul C# populaire.

À la fin de ce tutoriel, vous serez capable d'**appliquer un format numérique personnalisé** à n'importe quelle cellule numérique, d'exporter le résultat avec `ExportTable`, et de voir la sortie exacte que vous vous attendriez à afficher dans une interface utilisateur ou un rapport. Aucun document externe n'est nécessaire—tout est ici.

## Prérequis

- .NET 6.0 ou ultérieur (le code fonctionne également sur .NET Framework 4.7+)
- Une référence à la bibliothèque de feuilles de calcul qui fournit `Workbook`, `Worksheet` et `ExportTableOptions` (par ex., **Aspose.Cells** ou **GemBox.Spreadsheet** ; l'API présentée correspond à Aspose.Cells)
- Connaissances de base en C#—si vous pouvez écrire un `Console.WriteLine`, vous êtes prêt à partir

> **Astuce :** Si vous utilisez une bibliothèque différente, les noms de propriétés sont généralement similaires (`NumberFormat`, `ExportAsString`). Il suffit de les mapper en conséquence.

## Ce que couvre le tutoriel

1. Créer un classeur et sélectionner la première feuille de calcul.  
2. Insérer une valeur numérique dans une cellule.  
3. Configurer `ExportTableOptions` pour **appliquer un format numérique personnalisé** et renvoyer une chaîne.  
4. Exporter la cellule et afficher le résultat formaté.  
5. Gestion des cas limites – que se passe-t-il si la cellule contient une formule ou une valeur nulle ?

Allons-y.

![exemple d'application d'un format numérique personnalisé](https://example.com/image.png "application d'un format numérique personnalisé")

## Étape 1 – Créer un classeur et obtenir la première feuille de calcul

La première chose dont vous avez besoin est un objet workbook. Considérez-le comme le fichier Excel que vous ouvririez dans l'application Office. Une fois que vous l'avez, récupérez la première feuille—la plupart des tutoriels commencent ainsi car cela rend l'exemple concis.

```csharp
// Step 1: Initialize the workbook and fetch the first worksheet
Workbook workbook = new Workbook();                 // creates an in‑memory workbook
Worksheet worksheet = workbook.Worksheets[0];      // first sheet (index 0)
```

**Pourquoi c'est important :** Un classeur vierge vous donne une page blanche, garantissant qu'aucun formatage caché n'interfère avec notre format numérique personnalisé plus tard.

## Étape 2 – Placer une valeur numérique dans la cellule B2 (la cellule que nous allons exporter)

Nous avons maintenant besoin de quelque chose à formater. La cellule **B2** est un emplacement pratique—facile à référencer et suffisamment éloignée du coin par défaut A1 pour éviter les écrasements accidentels.

```csharp
// Step 2: Insert a raw numeric value
worksheet.Cells["B2"].Value = 1234.56;   // raw double, no formatting yet
```

**Et si la valeur est une formule ?**  
Si vous remplacez plus tard la valeur brute par une formule (par ex., `=SUM(A1:A10)`), la routine d'exportation respectera toujours le format numérique que nous appliquons à l'étape suivante, car le formatage est attaché à la cellule, pas au type de valeur.

## Étape 3 – Configurer les options d'exportation pour recevoir la valeur sous forme de chaîne formatée

Voici le cœur du tutoriel : nous indiquons à la bibliothèque d'**appliquer un format numérique personnalisé** lors de l'exportation. La chaîne `NumberFormat` suit le même modèle que celui que vous utiliseriez dans la catégorie « Personnalisée » d'Excel.

```csharp
// Step 3: Set up options for exporting as a formatted string
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,                         // forces string output
    NumberFormat = "#,##0.00;(#,##0.00)"           // custom format: 1,234.56 or (1,234.56) for negatives
};
```

- `ExportAsString = true` garantit que la méthode renvoie une `string` au lieu d'un double brut.  
- `NumberFormat = "#,##0.00;(#,##0.00)"` reproduit le modèle d'Excel : virgules pour les milliers, deux décimales, et parenthèses pour les nombres négatifs.

> **Pourquoi utiliser un format personnalisé ?** Il garantit la cohérence entre les cultures (par ex., séparateurs de nombres US vs. européens) et vous permet d'intégrer un style propre à l'entreprise comme les parenthèses comptables.

## Étape 4 – Exporter la cellule en utilisant les options configurées

Nous extrayons maintenant réellement la valeur de la feuille de calcul, laissant la bibliothèque faire le travail lourd d'appliquer le format que nous avons défini.

```csharp
// Step 4: Export the formatted value from B2
string formattedResult = worksheet.Cells.ExportTable(
    worksheet.Cells["B2"],   // the source cell
    exportOptions);         // our custom options
```

**Cas limite – cellule vide :** Si `B2` était vide, `formattedResult` serait `null`. Vous pouvez vous en prémunir avec une simple vérification de null avant d'afficher.

## Étape 5 – Afficher la chaîne formatée

Enfin, nous écrivons le résultat dans la console. Dans une application réelle, vous pourriez injecter cette chaîne dans un PDF, un e‑mail ou une étiquette d'interface utilisateur.

```csharp
// Step 5: Show the result
Console.WriteLine(formattedResult);   // Expected output: 1,234.56
```

**Sortie attendue**

```
1,234.56
```

Si vous changez la valeur brute en `-9876.54`, le même format vous donnera `(9,876.54)`—exactement ce que de nombreux rapports comptables exigent.

## Exemple complet, exécutable

Ci-dessous le programme complet que vous pouvez copier‑coller dans un nouveau projet console. Il compile et s'exécute tel quel, en supposant que vous avez ajouté le package NuGet approprié pour la bibliothèque de feuilles de calcul.

```csharp
using System;
using Aspose.Cells;   // Replace with your library’s namespace if different

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook and get first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Insert numeric value into B2
        worksheet.Cells["B2"].Value = 1234.56;

        // 3️⃣ Set export options – apply custom number format
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            NumberFormat = "#,##0.00;(#,##0.00)"   // custom format
        };

        // 4️⃣ Export the cell as a formatted string
        string formattedResult = worksheet.Cells.ExportTable(
            worksheet.Cells["B2"], exportOptions);

        // 5️⃣ Output the result
        Console.WriteLine(formattedResult);   // → 1,234.56
    }
}
```

### Vérification rapide

- **Ça compile ?** Oui—assurez‑vous simplement que la DLL `Aspose.Cells` (ou équivalente) est référencée.
- **Fonctionnera‑t‑il avec d'autres cultures ?** La chaîne de format est indépendante de la culture ; la bibliothèque respecte le modèle que vous lui fournissez. Si vous avez besoin de séparateurs spécifiques à une locale, vous pouvez préfixer la gestion `CultureInfo` avant l'exportation.

## Questions fréquentes & variations

### Comment **formater un nombre dans une feuille de calcul** en utilisant un modèle différent ?

Remplacez la chaîne `NumberFormat`. Par exemple, pour afficher un pourcentage avec une décimale :

```csharp
NumberFormat = "0.0%";
```

### Et si j'ai besoin de **comment exporter la valeur d'une cellule** en HTML plutôt qu'en texte brut ?

La plupart des bibliothèques possèdent une surcharge qui accepte un type d'exportation. Vous définiriez `ExportAsString = true` et ajouteriez `ExportHtml = true` (ou similaire). Le principe reste le même : définir le format, puis choisir la représentation de sortie.

### Puis‑je appliquer le format à toute une plage, pas seulement à une cellule ?

Absolument. Vous pouvez assigner `NumberFormat` à un objet `Style` puis appliquer ce style à un `Range`. L'appel d'exportation reste inchangé ; il récupérera automatiquement le style.

```csharp
Style style = workbook.CreateStyle();
style.Custom = "#,##0.00;(#,##0.00)";
Range range = worksheet.Cells.CreateRange("A1:C10");
range.ApplyStyle(style, new StyleFlag { NumberFormat = true });
```

### Que se passe‑t‑il lorsque la cellule contient une formule ?

La routine d'exportation évalue d'abord la formule, puis formate la valeur numérique résultante. Aucun code supplémentaire n'est nécessaire—assurez‑vous simplement que `Calculate` a été appelé si vous avez désactivé le calcul automatique.

```csharp
worksheet.Cells["B2"].Formula = "=SUM(A1:A5)";
worksheet.Calculate();   // forces evaluation
```

## Conclusion

Vous savez maintenant comment **appliquer un format numérique personnalisé** à une cellule de feuille de calcul, **formater un nombre dans une feuille de calcul** et **comment exporter la valeur d'une cellule** sous forme de chaîne prête à l'affichage. L'exemple de code concis ci‑dessus couvre chaque étape—de la création du classeur à la sortie finale—vous permettant de l'intégrer directement dans un projet de production.

Prêt pour le prochain défi ? Essayez de combiner cette technique avec **comment formater une cellule numérique** pour les dates, les symboles monétaires ou le formatage conditionnel. Ou explorez l'exportation de plusieurs cellules en CSV tout en conservant le format personnalisé de chaque cellule. Le ciel est la limite, et avec ces bases vous avez une fondation solide.

Bon codage, et n'oubliez pas d'expérimenter—parfois les meilleures réponses apparaissent lorsque vous ajustez légèrement la chaîne de format !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}