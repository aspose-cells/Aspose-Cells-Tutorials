---
category: general
date: 2026-02-23
description: Actualisez le tableau croisé dynamique Excel en C# et exportez-le au
  format PNG. Apprenez à charger un classeur Excel en C#, à actualiser le tableau
  croisé dynamique et à enregistrer le résultat.
draft: false
keywords:
- refresh excel pivot table
- load excel workbook c#
- export pivot as image
- export excel pivot image
language: fr
og_description: Actualisez le tableau croisé dynamique Excel en C# et exportez-le
  en image PNG. Guide étape par étape avec le code complet et des conseils pratiques.
og_title: Actualiser le tableau croisé dynamique Excel en C# – Exporter en image PNG
tags:
- C#
- Excel
- Aspose.Cells
- Data Automation
title: Actualiser le tableau croisé dynamique Excel en C# – Exporter en image PNG
url: /fr/net/pivot-tables/refresh-excel-pivot-table-in-c-export-as-png-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Actualiser le tableau croisé dynamique Excel en C# – Exporter en image PNG

Vous avez déjà eu besoin d'**actualiser un tableau croisé dynamique Excel** depuis une application C# et de le transformer en image ? Vous n'êtes pas le seul à vous creuser la tête à ce sujet. Dans ce tutoriel, nous allons vous montrer exactement comment **actualiser un tableau croisé dynamique Excel**, **charger un classeur Excel en C#**, et enfin **exporter le tableau croisé dynamique en image**—le tout dans un extrait de code propre et exécutable.

À la fin, vous obtiendrez un fichier PNG qui ressemble exactement au tableau croisé dynamique que vous voyez dans Excel, prêt à être intégré dans des rapports, des e‑mails ou des tableaux de bord. Pas de copier‑coller manuel, pas d’interop COM compliquée, juste du code .NET simple.

## Prérequis

- .NET 6+ (ou .NET Framework 4.7+)
- Aspose.Cells pour .NET (version d'essai gratuite ou version sous licence) – vous pouvez l'obtenir depuis NuGet avec `Install-Package Aspose.Cells`.
- Un fichier `input.xlsx` existant contenant au moins un tableau croisé dynamique.
- Un dossier où vous avez les droits d'écriture pour l'image de sortie.

> **Astuce :** Si vous utilisez Visual Studio, activez les **types de référence nullable** (`<Nullable>enable</Nullable>`) pour détecter les bugs liés aux nulls dès le départ.

---

## Étape 1 : Charger le classeur Excel en C#

La première chose dont nous avons besoin est un objet `Workbook` qui pointe vers notre fichier source. Considérez cela comme l'ouverture du fichier Excel de manière programmatique.

```csharp
using System;
using Aspose.Cells;

class PivotExportDemo
{
    static void Main()
    {
        // 👉 Step 1: Load the workbook and obtain the first worksheet
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook wb = new Workbook(inputPath);
        Worksheet worksheet = wb.Worksheets[0];

        // The rest of the steps follow…
```

**Pourquoi c’est important :** Charger le classeur nous donne accès aux feuilles de calcul, aux cellules et—plus important—aux tableaux croisés dynamiques que vous avez créés. Si le fichier n’est pas trouvé, Aspose lève une `FileNotFoundException` claire, que vous pouvez intercepter pour gérer le problème de façon élégante.

## Étape 2 : Configurer les options d’exportation d’image (Exporter le tableau croisé dynamique en image)

Aspose.Cells vous permet de définir comment le tableau croisé dynamique doit être rendu. Ici, nous demandons un PNG car il est sans perte et largement supporté.

```csharp
        // 👉 Step 2: Configure image export options to use PNG format
        ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
        {
            ImageFormat = ImageFormat.Png,
            // Optional: set resolution for sharper output
            HorizontalResolution = 300,
            VerticalResolution = 300
        };
```

**Pourquoi le PNG ?** Contrairement au JPEG, le PNG conserve les lignes de grille nettes et les ombrages de texte dont les tableaux croisés dynamiques dépendent. Si vous avez besoin d’un fichier plus petit, vous pouvez passer à `ImageFormat.Jpeg` et ajuster la qualité, mais vous perdrez un peu de netteté.

## Étape 3 : Actualiser le tableau croisé dynamique

Avant de capturer l’image, nous devons nous assurer que le tableau croisé dynamique reflète les dernières données. C’est le cœur de **actualiser le tableau croisé dynamique Excel**.

```csharp
        // 👉 Step 3: Refresh the first pivot table so it reflects the latest data
        PivotTable pivot = worksheet.PivotTables[0];
        pivot.Refresh();
```

**Que se passe-t-il en coulisses ?** `Refresh()` recalcule le tableau croisé dynamique à partir de la plage source. Si vous avez ajouté des lignes aux données source après l’enregistrement du classeur, cet appel les intègre. Ignorer cette étape produit une image obsolète qui ne correspond pas aux données actuelles.

## Étape 4 : Rendre le tableau croisé dynamique en PNG (Exporter le tableau croisé dynamique Excel en image)

Maintenant que tout est à jour, nous pouvons rendre le tableau croisé dynamique directement dans un fichier image.

```csharp
        // 👉 Step 4: Export the refreshed pivot table as a PNG image
        string outputPath = @"YOUR_DIRECTORY\pivot.png";
        pivot.RenderToImage(imgOptions, outputPath);

        Console.WriteLine($"Pivot table exported successfully to: {outputPath}");
    }
}
```

**Résultat :** Ouvrez `pivot.png` et vous verrez un instantané pixel‑parfait du tableau croisé dynamique actualisé. Ce fichier peut être joint à un e‑mail, intégré dans une page web ou alimenter un moteur de reporting.

### Résultat attendu

```
Pivot table exported successfully to: YOUR_DIRECTORY\pivot.png
```

Si vous parcourez le dossier, le PNG devrait afficher les mêmes lignes, colonnes et filtres que vous verriez dans Excel.

## Gestion des cas limites courants

| Situation | Que faire |
|-----------|-----------|
| **Multiple pivot tables** | Parcourez `worksheet.PivotTables` et appelez `Refresh()` / `RenderToImage()` pour chacun. |
| **Dynamic sheet names** | Utilisez `wb.Worksheets[wb.Worksheets.IndexOf("SheetName")]` ou recherchez par `worksheet.Name`. |
| **Large datasets** | Augmentez `imgOptions.OnePagePerSheet = false` et définissez `imgOptions.PageWidth`/`PageHeight` pour contrôler la pagination. |
| **Missing Aspose.Cells license** | La version d’essai ajoute un filigrane. Procurez‑vous une licence et appelez `License license = new License(); license.SetLicense("Aspose.Total.NET.lic");` avant de charger le classeur. |
| **File‑path issues** | Utilisez `Path.Combine(Environment.CurrentDirectory, "input.xlsx")` pour éviter les séparateurs codés en dur. |

## Astuces & bonnes pratiques

- **Libérer correctement** – Enveloppez le `Workbook` dans un bloc `using` ou appelez `wb.Dispose()` une fois terminé pour libérer les ressources natives.
- **Mettre en cache les images rendues** – Si vous avez besoin de la même image de tableau croisé dynamique à plusieurs reprises, mettez le PNG en cache sur le disque et réutilisez‑le au lieu de le re‑rendre à chaque fois.
- **Sécurité des threads** – Chaque thread doit travailler avec sa propre instance de `Workbook` ; les objets Aspose.Cells ne sont pas thread‑safe.
- **Performance** – Rendre de grands tableaux croisés dynamiques peut être gourmand en mémoire. Ajustez `imgOptions.ImageFormat` à `Bmp` pour une exécution plus rapide mais des fichiers plus volumineux, ou réduisez le DPI pour des rendus plus rapides.

## Exemple complet fonctionnel (prêt à copier‑coller)

```csharp
using System;
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Rendering;

class PivotExportDemo
{
    static void Main()
    {
        // 👉 Step 1: Load the workbook and obtain the first worksheet
        string inputPath = Path.Combine(Environment.CurrentDirectory, "input.xlsx");
        if (!File.Exists(inputPath))
        {
            Console.Error.WriteLine($"File not found: {inputPath}");
            return;
        }

        Workbook wb = new Workbook(inputPath);
        Worksheet worksheet = wb.Worksheets[0];

        // 👉 Step 2: Configure image export options to use PNG format
        ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
        {
            ImageFormat = ImageFormat.Png,
            HorizontalResolution = 300,
            VerticalResolution = 300
        };

        // 👉 Step 3: Refresh the first pivot table so it reflects the latest data
        if (worksheet.PivotTables.Count == 0)
        {
            Console.Error.WriteLine("No pivot tables found on the first worksheet.");
            return;
        }

        PivotTable pivot = worksheet.PivotTables[0];
        pivot.Refresh();

        // 👉 Step 4: Export the refreshed pivot table as a PNG image
        string outputPath = Path.Combine(Environment.CurrentDirectory, "pivot.png");
        pivot.RenderToImage(imgOptions, outputPath);

        Console.WriteLine($"Pivot table exported successfully to: {outputPath}");

        // Clean up
        wb.Dispose();
    }
}
```

Exécutez le programme, ouvrez `pivot.png` et vous verrez le tableau croisé dynamique actualisé exactement comme il apparaît dans Excel.

## Questions fréquentes

**Q : Cette méthode fonctionne‑t‑elle avec des fichiers .xlsx créés par LibreOffice ?**  
R : Oui. Aspose.Cells lit le format Open XML quel que soit l’application d’origine, vous pouvez donc **charger un classeur Excel en C#** depuis LibreOffice, l’exportation Google Sheets, ou toute autre source.

**Q : Puis‑je exporter plusieurs feuilles de calcul en même temps ?**  
R : Absolument. Parcourez `wb.Worksheets` et appliquez la même logique `RenderToImage` pour chaque feuille. N’oubliez pas d’attribuer à chaque sortie un nom de fichier unique.

**Q : Que faire si le tableau croisé dynamique utilise une source de données externe ?**  
R : Aspose.Cells peut actualiser les connexions externes si elles sont intégrées dans le fichier, mais vous devrez fournir la chaîne de connexion et les identifiants par programme. Consultez la documentation Aspose pour `DataSourceOptions`.

## Conclusion

Vous disposez maintenant d’une solution complète, de bout en bout, pour **actualiser le tableau croisé dynamique Excel** depuis C# et **exporter le tableau croisé dynamique Excel en image** au format PNG. Le code montre comment **charger un classeur Excel en C#**, configurer les paramètres d’image, garantir que le tableau reflète les dernières données, puis le rendre dans un fichier.

Ensuite, vous pourriez explorer **exporter le tableau croisé dynamique en image** dans d’autres formats (PDF, SVG) ou automatiser le processus pour plusieurs classeurs dans un travail par lots. Vous souhaitez intégrer le PNG dans un rapport Word ? La même classe `ImageOrPrintOptions` fonctionne avec Aspose.Words.

N’hésitez pas à expérimenter, à casser des choses, et à poser des questions dans les commentaires—bon codage !

![Capture d'écran du tableau croisé dynamique Excel](image.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}