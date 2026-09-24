---
category: general
date: 2026-04-07
description: Apprenez à actualiser un tableau croisé dynamique, insérer une image
  dans Excel et enregistrer le classeur Excel avec un espace réservé pour l'image
  en quelques étapes seulement.
draft: false
keywords:
- how to refresh pivot
- insert image into excel
- save excel workbook
- add picture placeholder
- refresh pivot table
language: fr
og_description: Comment actualiser un tableau croisé dynamique dans Excel, insérer
  une image dans Excel et enregistrer le classeur Excel à l’aide de C# avec un espace
  réservé pour l’image. Exemple de code pas à pas.
og_title: Comment actualiser un tableau croisé dynamique et insérer une image dans
  Excel – Guide complet
tags:
- Aspose.Cells
- C#
- Excel automation
title: Comment actualiser le tableau croisé dynamique et insérer une image dans Excel
  – Guide complet
url: /fr/net/pivot-tables/how-to-refresh-pivot-and-insert-image-into-excel-complete-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment rafraîchir un tableau croisé dynamique et insérer une image dans Excel – Guide complet

Vous vous êtes déjà demandé **comment rafraîchir un tableau croisé dynamique** lorsque les données source changent, puis insérer une nouvelle image de graphique ou de tableau directement dans la même feuille ? Vous n'êtes pas le seul. Dans de nombreux pipelines de reporting, les données résident dans une base de données, le tableau croisé dynamique les récupère, et le fichier Excel final doit afficher les derniers chiffres sous forme d'image — afin que les utilisateurs en aval ne puissent pas modifier accidentellement la source.  

Dans ce tutoriel, nous allons passer en revue exactement cela : **comment rafraîchir un tableau croisé dynamique**, **insérer une image dans Excel**, et enfin **enregistrer le classeur Excel** en utilisant un **espace réservé pour image**. À la fin, vous disposerez d’un programme C# unique et exécutable qui fait tout cela, et vous comprendrez pourquoi chaque ligne est importante.

> **Astuce :** Cette approche fonctionne avec Aspose.Cells 2024 ou ultérieur, ce qui signifie que vous n’avez pas besoin d’Excel installé sur le serveur.

---

## Ce dont vous aurez besoin

- **Aspose.Cells for .NET** (package NuGet `Aspose.Cells`).  
- SDK .NET 6.0 ou ultérieur (le code se compile également avec .NET 8).  
- Un fichier Excel de base (`input.xlsx`) qui contient déjà un tableau croisé dynamique et un espace réservé pour image (le premier objet image de la feuille).  
- Un peu de curiosité sur les modèles d’objets Excel.

Pas d’interop COM supplémentaire, pas d’installation d’Office, juste du pur C#.

---

## Comment rafraîchir le tableau croisé dynamique et capturer les dernières données

La première chose à faire est d’indiquer à Excel (ou plutôt à Aspose.Cells) que le tableau croisé dynamique doit se recalculer en fonction de la nouvelle plage source. Ignorer cette étape vous laisse avec des chiffres obsolètes, ce qui annule tout l’intérêt de l’automatisation.

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

// 1️⃣ Load the workbook and grab the first worksheet
Workbook workbook = new Workbook(@"C:\MyProjects\ExcelDemo\input.xlsx");
Worksheet worksheet = workbook.Worksheets[0];

// 2️⃣ Refresh the first pivot table so it reflects the latest data
worksheet.PivotTables[0].Refresh();
```

**Pourquoi c’est important :**  
Lorsque vous appelez `Refresh()`, le moteur du tableau croisé dynamique réexécute sa logique d’agrégation. Si vous exportez ensuite le tableau croisé dynamique sous forme d’image, l’image affichera les totaux *actuels*, et non ceux de la dernière sauvegarde du fichier.

---

## Insérer une image dans Excel en utilisant un espace réservé pour image

Maintenant que le tableau croisé dynamique est à jour, nous devons le transformer en image statique. Cela est pratique lorsque vous souhaitez verrouiller le visuel pour la distribution ou l’intégrer plus tard dans une diapositive PowerPoint.

```csharp
// 3️⃣ Set up image options – we want a PNG image
ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Png
};

// 4️⃣ Render the refreshed pivot table to an image using the options
Image pivotImage = worksheet.PivotTables[0].ToImage(imageOptions);
```

L’objet `ImageOrPrintOptions` vous permet de contrôler la résolution, l’arrière‑plan et le format. Le PNG est sans perte et convient parfaitement à la plupart des rapports d’entreprise.

---

## Ajouter un espace réservé pour image à une feuille de calcul

La plupart des modèles Excel contiennent déjà une forme ou une image qui sert de « emplacement » pour les graphiques dynamiques. Si vous n’en avez pas, insérez simplement une image vide dans Excel et enregistrez le modèle — Aspose.Cells l’exposera sous la forme `Pictures[0]`.

```csharp
// 5️⃣ Place the rendered image into the first picture placeholder on the sheet
worksheet.Pictures[0].Image = pivotImage;
```

**Et si vous avez plusieurs espaces réservés ?**  
Il suffit de changer l’indice (`Pictures[1]`, `Pictures[2]`, …) ou de parcourir `worksheet.Pictures` pour en trouver un par son nom.

---

## Enregistrer le classeur Excel après les modifications

Enfin, nous persistons les modifications. Le classeur contient maintenant un tableau croisé dynamique rafraîchi, un PNG fraîchement généré, et l’espace réservé pour image mis à jour avec cette image.

```csharp
// 6️⃣ Save the workbook to see the result
workbook.Save(@"C:\MyProjects\ExcelDemo\output.xlsx");
```

Lorsque vous ouvrez `output.xlsx`, vous verrez l’emplacement d’image rempli avec le dernier instantané du tableau croisé dynamique. Aucune étape manuelle n’est requise.

---

## Exemple complet fonctionnel (Toutes les étapes ensemble)

Ci‑dessous se trouve le programme complet, prêt à copier‑coller. Il inclut les instructions `using` nécessaires, la gestion des erreurs, et des commentaires expliquant chaque ligne non évidente.

```csharp
using Aspose.Cells;
using System;
using System.Drawing.Imaging;

namespace ExcelPivotImageDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Paths – adjust to your environment
            string inputPath = @"C:\MyProjects\ExcelDemo\input.xlsx";
            string outputPath = @"C:\MyProjects\ExcelDemo\output.xlsx";

            try
            {
                // Load workbook
                Workbook workbook = new Workbook(inputPath);
                Worksheet sheet = workbook.Worksheets[0];

                // -------------------------------------------------
                // Refresh pivot table – this is the core of "how to refresh pivot"
                // -------------------------------------------------
                if (sheet.PivotTables.Count == 0)
                {
                    Console.WriteLine("No pivot tables found on the first worksheet.");
                    return;
                }
                sheet.PivotTables[0].Refresh();

                // -------------------------------------------------
                // Convert refreshed pivot to PNG image
                // -------------------------------------------------
                ImageOrPrintOptions imgOpts = new ImageOrPrintOptions
                {
                    ImageFormat = ImageFormat.Png,
                    // Optional: higher DPI for sharper images
                    HorizontalResolution = 150,
                    VerticalResolution = 150
                };
                Image pivotImg = sheet.PivotTables[0].ToImage(imgOpts);

                // -------------------------------------------------
                // Insert the image into the first picture placeholder
                // -------------------------------------------------
                if (sheet.Pictures.Count == 0)
                {
                    // If the template lacks a placeholder, we create one on the fly
                    int picIdx = sheet.Pictures.Add(0, 0, pivotImg);
                    sheet.Pictures[picIdx].Name = "PivotSnapshot";
                }
                else
                {
                    sheet.Pictures[0].Image = pivotImg;
                }

                // -------------------------------------------------
                // Save the updated workbook – this fulfills "save excel workbook"
                // -------------------------------------------------
                workbook.Save(outputPath);
                Console.WriteLine($"Workbook saved successfully to {outputPath}");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Error: {ex.Message}");
                // In production you might log the stack trace or rethrow
            }
        }
    }
}
```

**Résultat attendu :**  
Ouvrez `output.xlsx`. Le premier objet image affiche maintenant un PNG du tableau croisé dynamique rafraîchi. Si vous modifiez les données source dans `input.xlsx` et exécutez à nouveau le programme, l’image se met à jour automatiquement — aucune copie‑collage manuelle n’est nécessaire.

---

## Variations courantes et cas limites

| Situation | Ce qu’il faut changer |
|-----------|-----------------------|
| **Multiple pivot tables** | Parcourir `sheet.PivotTables` et rafraîchir chacun, puis choisir celui dont vous avez besoin pour l’image. |
| **Different image format** | Définir `ImageFormat = ImageFormat.Jpeg` (ou `Bmp`) dans `ImageOrPrintOptions`. |
| **Dynamic placeholder selection** | Utiliser `sheet.Pictures["MyPlaceholderName"]` au lieu d’un indice. |
| **Large workbooks** | Augmenter `Workbook.Settings.CalculateFormulaEngine` à `EngineType.Fast` pour des rafraîchissements plus rapides. |
| **Running on a headless server** | Aspose.Cells fonctionne entièrement sans interface utilisateur, aucune configuration supplémentaire n’est requise. |

---

## Questions fréquentes

**Q : Cette méthode fonctionne‑t‑elle avec les classeurs activés macro (`.xlsm` ) ?**  
R : Oui. Aspose.Cells les traite comme n’importe quel autre classeur ; les macros sont conservées mais ne sont pas exécutées pendant le rafraîchissement.

**Q : Et si le tableau croisé dynamique utilise une source de données externe ?**  
R : Vous devez vous assurer que la chaîne de connexion est valide sur la machine exécutant le code. Appelez `pivotTable.CacheDefinition.ConnectionInfo` pour la modifier programmatique.

**Q : Puis‑je placer l’image dans une plage de cellules spécifique au lieu d’un espace réservé pour image ?**  
R : Bien sûr. Utilisez `sheet.Pictures.Add(row, column, pivotImg)` où `row` et `column` sont des indices zéro‑based.

---

## Conclusion

Nous avons couvert **comment rafraîchir un tableau croisé dynamique**, **insérer une image dans Excel**, **ajouter un espace réservé pour image**, et enfin **enregistrer le classeur Excel** — le tout dans un extrait C# concis. En rafraîchissant d’abord le tableau croisé dynamique, vous vous assurez que l’image reflète les derniers chiffres, et en utilisant un espace réservé, vous gardez vos modèles propres et réutilisables.

Ensuite, vous pourriez explorer :

- Exporter la même image vers un rapport PDF (`PdfSaveOptions`).  
- Automatiser un lot de fichiers avec des données source différentes.  
- Utiliser Aspose.Slides pour coller le PNG directement dans une diapositive PowerPoint.

N’hésitez pas à expérimenter — remplacer le PNG par un JPEG, modifier le DPI, ou ajouter plusieurs images. L’idée principale reste la même : garder les données à jour, les capturer sous forme d’image, et les intégrer où vous en avez besoin.

Bon codage ! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}