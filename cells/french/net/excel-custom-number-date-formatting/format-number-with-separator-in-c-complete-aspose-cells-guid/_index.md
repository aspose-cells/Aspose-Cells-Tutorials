---
category: general
date: 2026-03-30
description: Apprenez à formater les nombres avec séparateur en utilisant Aspose.Cells
  en C#. Comprend la définition d’un format numérique personnalisé, l’ajout d’un séparateur
  de milliers, le formatage des décimales et la façon de formater une cellule.
draft: false
keywords:
- format number with separator
- set custom number format
- add thousands separator
- format decimal places
- how to format cell
language: fr
og_description: Formater un nombre avec séparateur en C#. Ce guide montre comment
  définir un format de nombre personnalisé, ajouter un séparateur de milliers, formater
  les décimales et comment formater une cellule à l’aide d’Aspose.Cells.
og_title: Formater un nombre avec séparateur en C# – Tutoriel Aspose.Cells
tags:
- C#
- Aspose.Cells
- Number Formatting
title: Formater les nombres avec séparateur en C# – Guide complet d’Aspose.Cells
url: /fr/net/excel-custom-number-date-formatting/format-number-with-separator-in-c-complete-aspose-cells-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Formater un nombre avec séparateur en C# – Guide complet Aspose.Cells

Vous avez déjà eu besoin de **formater un nombre avec séparateur** dans une feuille de calcul mais vous ne saviez pas quelle appel d'API utiliser ? Vous n'êtes pas le seul—les développeurs luttent constamment avec les séparateurs de milliers, les décimales et les modèles personnalisés lors de l'exportation de données.  

Bonne nouvelle : Aspose.Cells rend cela très simple. Dans ce tutoriel, nous parcourrons un exemple réel qui **définit un format numérique personnalisé**, **ajoute un séparateur de milliers**, **formate les décimales**, et montre **comment formater une cellule** en sortie sous forme de chaîne. À la fin, vous disposerez d’un extrait prêt à l’exécution que vous pourrez intégrer dans n’importe quel projet .NET.

## Ce que couvre ce guide

* Le package NuGet exact dont vous avez besoin et comment l'installer.  
* Code étape par étape qui crée un classeur, écrit une valeur numérique et applique un format personnalisé.  
* Pourquoi `ExportTableOptions.ExportAsString` est la méthode préférée pour récupérer une valeur formatée.  
* Pièges courants—comme oublier d'activer `ExportAsString` ou utiliser le mauvais masque de format.  
* Comment ajuster le masque de format si vous avez besoin d’un nombre différent de décimales ou d’un style de séparateur différent.

Aucun lien vers une documentation externe n’est requis ; tout ce dont vous avez besoin se trouve ici. Plongeons‑y.

---

## Prérequis

| Exigence | Raison |
|-------------|--------|
| .NET 6.0 ou version ultérieure | Aspose.Cells 23.10+ cible .NET Standard 2.0+, donc .NET 6 est sûr et actuel. |
| Visual Studio 2022 (ou tout IDE C#) | Facilite le débogage et la gestion des packages. |
| Package NuGet Aspose.Cells pour .NET | Fournit les classes `Workbook`, `Worksheet` et `ExportTableOptions` que nous utiliserons. |

Vous pouvez installer le package via la console du gestionnaire de packages :

```powershell
Install-Package Aspose.Cells
```

C’est tout—pas de DLL supplémentaires, pas d’interop COM, juste une référence NuGet unique.

## Étape 1 : Initialiser un nouveau classeur (Comment formater une cellule)

La première chose que nous faisons est de créer une nouvelle instance de `Workbook`. Considérez‑la comme un fichier Excel vide prêt à recevoir des données.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook – this is where we’ll format the cell.
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];
```

> **Pourquoi c’est important :** `Workbook` est le point d’entrée de chaque opération dans Aspose.Cells. En récupérant la première feuille de calcul (`Worksheets[0]`) nous obtenons une toile vierge sans avoir à nommer une feuille.

## Étape 2 : Écrire une valeur numérique dans la cellule cible

Ensuite, nous plaçons un nombre brut dans la cellule **A1**. La valeur elle‑même n’est pas encore formatée — c’est simplement un double.

```csharp
        // Step 2: Insert a raw numeric value.
        worksheet.Cells["A1"].PutValue(12345.6789);
```

> **Astuce :** Utilisez `PutValue` au lieu de `PutString` lorsque vous avez l’intention d’appliquer un format numérique ultérieurement. Cela préserve le type de données sous‑jacent, permettant des calculs compatibles Excel.

## Étape 3 : Définir un format numérique personnalisé (Ajouter un séparateur de milliers & formater les décimales)

Voici le cœur du tutoriel : définir un masque de format qui indique à Aspose.Cells comment afficher le nombre. Le masque `#,##0.00` fait trois choses :

1. **`#,##0`** – ajoute un séparateur de milliers (virgule par défaut).  
2. **`.00`** – force exactement deux décimales.  

Si vous avez besoin d’un nombre différent de décimales, il suffit de modifier le nombre de `0` après le point décimal.

```csharp
        // Step 3: Configure the custom number format.
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,          // Return the value as a formatted string.
            NumberFormat = "#,##0.00"       // Add thousands separator and fix to 2 decimals.
        };
```

> **Pourquoi nous utilisons `ExportAsString`** : Par défaut, `ExportString` renvoie la valeur brute. Définir `ExportAsString = true` oblige l’API à appliquer le masque `NumberFormat` avant de convertir en texte. C’est essentiel lorsque vous avez besoin de la représentation exacte en chaîne pour les rapports, les charges JSON ou l’affichage UI.

## Étape 4 : Exporter le texte formaté (Comment formater une cellule)

Avec les options prêtes, nous appelons `ExportString` sur la même cellule. La méthode respecte le masque que nous venons de définir et renvoie une chaîne correctement formatée.

```csharp
        // Step 4: Export the formatted value.
        string formattedCellText = worksheet.Cells["A1"].ExportString(exportOptions);

        // Step 5: Show the result.
        Console.WriteLine(formattedCellText); // Expected output: 12,345.68
    }
}
```

L’exécution du programme affiche **`12,345.68`** dans la console—exactement le format que nous avons demandé.

> **Cas limite :** Si le nombre source possède plus de deux décimales, le masque l’arrondit. Si vous avez besoin d’une troncature au lieu d’un arrondi, vous devrez pré‑traiter la valeur avec `Math.Truncate` avant d’appeler `PutValue`.

## Étape 5 : Ajuster le format – Variations courantes

### 5.1 Modifier la précision décimale

Vous voulez trois décimales ? Remplacez simplement le masque :

```csharp
NumberFormat = "#,##0.000"   // → 12,345.679
```

### 5.2 Utiliser un séparateur de milliers différent

Certaines locales préfèrent un espace ou un point. Vous pouvez insérer le caractère directement :

```csharp
NumberFormat = "# ##0.00"    // Uses a non‑breaking space as separator.
```

Ou vous appuyer sur les paramètres de culture du classeur :

```csharp
workbook.Settings.CultureInfo = new System.Globalization.CultureInfo("de-DE");
NumberFormat = "#.##0,00";   // German style: 12.345,68
```

### 5.3 Préfixe ou suffixe (Monnaie, Pourcentage)

Ajoutez un signe dollar ou un signe pourcentage directement dans le masque :

```csharp
NumberFormat = "$#,##0.00";   // → $12,345.68
NumberFormat = "0.00%";       // → 1,234,568.00%
```

> **Remarque :** Le masque est sensible à la casse. `$` et `%` sont des symboles littéraux ; ils n’affectent pas la valeur numérique sous‑jacente.

## Étape 6 : Exemple complet fonctionnel (Prêt à copier‑coller)

Voici le programme complet que vous pouvez copier dans une nouvelle application console. Il inclut toutes les étapes, les commentaires et la vérification de la sortie finale.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialise workbook and worksheet.
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Write raw numeric value to A1.
        worksheet.Cells["A1"].PutValue(12345.6789);

        // 3️⃣ Define custom format: thousands separator + two decimals.
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            NumberFormat = "#,##0.00"
        };

        // 4️⃣ Export the formatted string.
        string result = worksheet.Cells["A1"].ExportString(exportOptions);

        // 5️⃣ Display the outcome.
        Console.WriteLine(result); // Output: 12,345.68

        // Optional: keep console open.
        Console.WriteLine("Press any key to exit...");
        Console.ReadKey();
    }
}
```

Exécutez le programme (`dotnet run` depuis le terminal ou appuyez sur F5 dans Visual Studio) et vous verrez le nombre formaté affiché exactement comme indiqué.

## Questions fréquemment posées (FAQ)

**Q : Cette méthode fonctionne‑t‑elle avec les versions plus anciennes d’Excel ?**  
R : Oui. Le masque de format suit la syntaxe native des formats numériques d’Excel, donc toute version qui comprend `#,##0.00` rendra la même chaîne.

**Q : Et si je dois formater une plage de cellules ?**  
R : Parcourez la plage souhaitée et appliquez le même `ExportTableOptions` à chaque cellule, ou définissez la propriété `Style.Custom` sur la plage puis appelez `ExportString` sur une seule cellule.

**Q : Puis‑je exporter directement en CSV avec ces formats appliqués ?**  
R : Absolument. Utilisez `Workbook.Save("output.csv", SaveFormat.CSV);` après avoir défini le format sur chaque cellule. Aspose.Cells respecte le `Style` de la cellule lors de la génération du CSV.

## Conclusion

Nous venons de montrer comment **formater un nombre avec séparateur** en C# avec Aspose.Cells, couvrant tout, de **définir un format numérique personnalisé** à **ajouter un séparateur de milliers**, **formater les décimales**, et l’essentiel **comment formater une cellule** pour l’exportation en chaîne. Le code est entièrement autonome, fonctionne avec .NET 6+, et peut être adapté à n’importe quelle locale ou exigence de précision.

Ensuite, vous pourriez explorer :

* Appliquer la même technique aux dates et heures (`NumberFormat = "dd‑MMM‑yyyy"`).  
* Automatiser les exportations en masse où chaque colonne nécessite un masque différent.  
* Intégrer les chaînes formatées dans des rapports PDF avec Aspose.Words.

Essayez-les, et vous deviendrez rapidement la référence en matière de formatage de feuilles de calcul dans votre équipe. Bon codage !   (Image: ![Capture d’écran montrant un nombre formaté avec séparateur dans Aspose.Cells](image-placeholder.png){alt="Nombre formaté avec séparateur affiché dans la sortie d’Aspose.Cells"} )

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}