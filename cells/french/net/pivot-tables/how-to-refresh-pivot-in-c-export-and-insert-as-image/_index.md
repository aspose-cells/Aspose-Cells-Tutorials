---
category: general
date: 2026-05-04
description: Comment actualiser le tableau croisé dynamique en C# et l’exporter en
  PNG, puis insérer l’image dans la feuille de calcul. Suivez ce guide étape par étape
  avec le code complet.
draft: false
keywords:
- how to refresh pivot
- how to export pivot
- insert image into worksheet
- refresh pivot table code
- load excel workbook c#
language: fr
og_description: Comment actualiser un tableau croisé dynamique en C# ? Apprenez à
  exporter le tableau croisé dynamique sous forme d’image et à l’insérer dans une
  feuille de calcul avec des exemples de code complets.
og_title: Comment actualiser un tableau croisé dynamique en C# – Exporter et insérer
  en tant qu'image
tags:
- C#
- Aspose.Cells
- Excel Automation
title: Comment rafraîchir le tableau croisé dynamique en C# – Exporter et insérer
  comme image
url: /fr/net/pivot-tables/how-to-refresh-pivot-in-c-export-and-insert-as-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment rafraîchir un tableau croisé dynamique en C# – Exporter et insérer comme image

Comment rafraîchir un tableau croisé dynamique en C# est un obstacle fréquent lorsque vous automatisez des rapports Excel. Dans ce guide, vous verrez exactement **comment rafraîchir le tableau croisé dynamique**, l’exporter en PNG et placer cette image dans un espace réservé d’une feuille de calcul—le tout avec un seul programme exécutable.

Si vous vous demandez aussi *comment exporter un tableau croisé dynamique* ou que vous devez **insérer une image dans une feuille de calcul**, vous êtes au bon endroit. Nous passerons en revue chaque ligne, expliquerons pourquoi elle est importante, et couvrirons même quelques cas limites que vous pourriez rencontrer dans des projets réels.

---

## Ce dont vous avez besoin

Avant de commencer, assurez‑vous d’avoir :

- **Aspose.Cells for .NET** (la bibliothèque qui fournit `Workbook`, `Worksheet`, `ImageOrPrintOptions`, etc.). Vous pouvez l’obtenir via NuGet : `Install-Package Aspose.Cells`.
- .NET 6 ou version ultérieure (le code ci‑dessous cible .NET 6, mais toute version récente fonctionne).
- Une compréhension de base de C# et des entrées/sorties de fichiers—rien de compliqué.

C’est tout. Pas de DLL supplémentaires, pas d’interop COM, juste une application console C# propre.

---

## Étape 1 – Charger le classeur Excel en C# Style

Tout d’abord, nous devons ouvrir le fichier source. C’est ici que se trouve la partie **load excel workbook c#**.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Load the workbook from disk
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(inputPath);

        // Grab the first worksheet (index 0)
        Worksheet worksheet = workbook.Worksheets[0];
```

> **Pourquoi ?**  
> Charger le classeur nous donne accès à ses feuilles de calcul, ses tableaux croisés dynamiques et aux espaces réservés d’images. Si le fichier n’est pas trouvé, Aspose lève une `FileNotFoundException` claire, que vous pouvez intercepter pour une interface plus conviviale.

---

## Étape 2 – Préparer les options d’image pour exporter le tableau croisé dynamique

Nous indiquons maintenant à Aspose comment nous voulons que l’image exportée apparaisse. C’est le cœur de **how to export pivot**.

```csharp
        // Step 2: Set up image export options – PNG is lossless and widely supported
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
        {
            SaveFormat = SaveFormat.Png,
            // Optional: tweak resolution for sharper images
            HorizontalResolution = 300,
            VerticalResolution = 300
        };
```

> **Astuce :**  
> Si vous avez besoin d’un JPEG pour une taille de fichier plus petite, remplacez `SaveFormat.Png` par `SaveFormat.Jpeg` et ajustez `Quality` en conséquence.

---

## Étape 3 – Code de rafraîchissement du tableau croisé dynamique

Un tableau croisé dynamique obsolète montre des données anciennes. Le rafraîchir garantit que l’image reflète les dernières valeurs.

```csharp
        // Step 3: Refresh the first pivot table in the worksheet
        if (worksheet.PivotTables.Count > 0)
        {
            worksheet.PivotTables[0].Refresh();
        }
        else
        {
            Console.WriteLine("No pivot tables found on the first worksheet.");
            return;
        }
```

> **Pourquoi rafraîchir ?**  
> Les tableaux croisés dynamiques mettent en cache les données sources lorsqu’ils sont créés. Si la feuille de calcul sous‑jacente change (par ex. : nouvelles lignes ajoutées), le cache devient périmé. L’appel à `Refresh()` force Aspose à re‑requêter la plage source, assurant que l’image exportée ne reste pas bloquée avec des totaux obsolètes.

---

## Étape 4 – Convertir le tableau croisé dynamique rafraîchi en image

Voici la ligne magique qui **export pivot** réellement vers un tableau d’octets.

```csharp
        // Step 4: Export the refreshed pivot table as an image
        byte[] pivotImage = worksheet.PivotTables[0].ToImage(imageOptions);
```

> **Ce que vous obtenez :**  
> `pivotImage` contient maintenant une image PNG du tableau croisé dynamique, prête à être écrite sur le disque ou intégrée ailleurs.

---

## Étape 5 – Insérer l’image dans la feuille de calcul

C’est ici que nous **insert image into worksheet**. Nous placerons l’image dans le premier espace réservé d’image (s’il existe).

```csharp
        // Step 5: Insert the image into the first picture placeholder
        if (worksheet.Pictures.Count > 0)
        {
            worksheet.Pictures[0].ImageBytes = pivotImage;
        }
        else
        {
            // If no placeholder exists, add a new picture at cell A1
            int pictureIndex = worksheet.Pictures.Add(0, 0, pivotImage).Index;
            Console.WriteLine($"Added new picture at index {pictureIndex}.");
        }
```

> **Pourquoi utiliser un espace réservé ?**  
> De nombreux modèles Excel sont livrés avec une forme d’image pré‑formatée (taille, bordure, position). En ciblant `Pictures[0]`, nous conservons la mise en page. Si le modèle ne possède pas d’espace réservé, le repli crée une nouvelle image ancrée à la cellule A1.

---

## Étape 6 – Enregistrer le classeur (optionnel)

Enfin, persistez les modifications. Vous pouvez écraser l’original ou écrire dans un nouveau fichier.

```csharp
        // Step 6: Save the updated workbook
        string outputPath = @"YOUR_DIRECTORY\output.xlsx";
        workbook.Save(outputPath);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

> **Résultat attendu :**  
> Ouvrez `output.xlsx` et vous verrez le tableau croisé dynamique rafraîchi, exporté en PNG net, et affiché dans le premier emplacement d’image. Le reste du classeur reste inchangé.

---

## Exemple complet (prêt à copier‑coller)

Ci‑dessous se trouve le bloc de code complet que vous pouvez coller dans un nouveau projet console. Aucun morceau ne manque.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load the workbook
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(inputPath);
        Worksheet worksheet = workbook.Worksheets[0];

        // Configure image export options (PNG, 300 DPI)
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
        {
            SaveFormat = SaveFormat.Png,
            HorizontalResolution = 300,
            VerticalResolution = 300
        };

        // Refresh the first pivot table
        if (worksheet.PivotTables.Count == 0)
        {
            Console.WriteLine("No pivot tables found.");
            return;
        }
        worksheet.PivotTables[0].Refresh();

        // Export pivot to PNG byte array
        byte[] pivotImage = worksheet.PivotTables[0].ToImage(imageOptions);

        // Insert the image into a picture placeholder or add a new picture
        if (worksheet.Pictures.Count > 0)
        {
            worksheet.Pictures[0].ImageBytes = pivotImage;
        }
        else
        {
            worksheet.Pictures.Add(0, 0, pivotImage);
        }

        // Save the workbook
        string outputPath = @"YOUR_DIRECTORY\output.xlsx";
        workbook.Save(outputPath);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

Exécutez le programme, ouvrez le fichier résultant et vérifiez que le tableau croisé dynamique reflète les dernières données et apparaît comme une image haute résolution.

---

## Questions fréquentes & cas limites

| Question | Réponse |
|----------|--------|
| **Et si le classeur possède plusieurs feuilles de calcul ?** | Modifiez `workbook.Worksheets[0]` pour l’index ou le nom approprié (`workbook.Worksheets["Sheet2"]`). |
| **Puis‑je exporter plusieurs tableaux croisés dynamiques ?** | Parcourez `worksheet.PivotTables` et répétez les étapes 3‑4 pour chaque tableau. Stockez chaque image dans un espace réservé distinct ou combinez‑les sur une même feuille. |
| **Que faire des gros tableaux croisés dynamiques qui provoquent une pression mémoire ?** | Utilisez `ImageOrPrintOptions` avec un DPI plus bas ou exportez en JPEG pour réduire la taille du tableau d’octets. |
| **Dois‑je libérer des ressources ?** | Les objets Aspose sont gérés ; l’instruction `using` n’est pas obligatoire, mais vous pouvez envelopper `Workbook` dans un bloc `using` si vous préférez un nettoyage déterministe. |
| **Cette solution est‑elle compatible avec .NET Core ?** | Oui. Aspose.Cells prend en charge .NET Core, .NET 5/6 et .NET Framework. Il suffit de référencer le package NuGet approprié. |

---

## Astuces et bonnes pratiques

- **Validez les chemins** : utilisez `Path.Combine` et `Environment.GetFolderPath` pour éviter les séparateurs codés en dur.
- **Gestion des erreurs** : encapsulez tout le corps de `Main` dans un `try/catch` et consignez `Exception.Message` pour les scripts de production.
- **Conception du modèle** : placez une forme d’image transparente à l’endroit où vous voulez l’image du tableau croisé dynamique ; cela préserve les largeurs de colonnes et hauteurs de lignes.
- **Performance** : si vous avez seulement besoin de l’image, vous pouvez ignorer l’enregistrement du classeur et écrire `pivotImage` dans un fichier PNG séparé.

---

## Conclusion

Vous savez maintenant **comment rafraîchir un tableau croisé dynamique** en C#, exporter cette vue rafraîchie sous forme d’image, et **insérer une image dans une feuille de calcul** sans accroc. La solution complète—chargement du classeur, configuration des options d’export, rafraîchissement du tableau, conversion en PNG et sauvegarde du fichier—couvre l’ensemble du flux de travail demandé.

Prêt pour le prochain défi ? Essayez de combiner **how to export pivot** avec le traitement par lots de plusieurs fichiers, ou explorez le **refresh pivot table code** pour des sources de données dynamiques comme des bases de données ou des flux CSV. Le même schéma s’applique : charger, rafraîchir, exporter, insérer, sauvegarder.

Bon codage, et que vos automatisations Excel restent fraîches et impeccables !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}