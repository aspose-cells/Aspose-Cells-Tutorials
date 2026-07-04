---
category: general
date: 2026-07-03
description: Comment exporter des fichiers Excel vers PowerPoint avec des zones de
  texte éditables en utilisant Aspose.Cells – guide étape par étape pour convertir
  XLSX en PPTX.
draft: false
keywords:
- how to export excel
- create powerpoint from excel
- editable text boxes
- convert xlsx to pptx
- presentation export options
language: fr
og_description: Comment exporter Excel vers PowerPoint avec des zones de texte éditables.
  Apprenez à convertir XLSX en PPTX en utilisant PresentationExportOptions en C#.
og_title: Comment exporter Excel vers PowerPoint – Guide complet
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: How to export Excel files to PowerPoint with editable text boxes using
    Aspose.Cells – step‑by‑step guide for converting XLSX to PPTX.
  headline: How to Export Excel to PowerPoint – Complete Guide
  type: TechArticle
- description: How to export Excel files to PowerPoint with editable text boxes using
    Aspose.Cells – step‑by‑step guide for converting XLSX to PPTX.
  name: How to Export Excel to PowerPoint – Complete Guide
  steps:
  - name: Navigate to a slide that originated from a worksheet.
    text: Navigate to a slide that originated from a worksheet.
  - name: Click on a text box—notice you can edit the text directly.
    text: Click on a text box—notice you can edit the text directly.
  - name: Adjust the shape’s size or color; the changes persist.
    text: Adjust the shape’s size or color; the changes persist.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Office Automation
title: Comment exporter Excel vers PowerPoint – Guide complet
url: /fr/net/converting-excel-files-to-other-formats/how-to-export-excel-to-powerpoint-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment exporter Excel vers PowerPoint – Guide complet

Vous vous êtes déjà demandé **comment exporter excel** des données directement dans une présentation PowerPoint sans perdre la possibilité de les modifier ? Vous n'êtes pas seul. Dans ce tutoriel, nous vous montrerons une méthode pratique pour **créer PowerPoint à partir d'Excel** tout en conservant les zones de texte et les formes entièrement modifiables.

Nous passerons en revue chaque ligne de code, expliquerons pourquoi chaque paramètre est important, et terminerons avec un fichier PowerPoint que vous pourrez ouvrir et ajuster immédiatement. À la fin, vous serez capable de **convertir XLSX en PPTX** en un seul appel de méthode, et vous comprendrez comment les **options d'exportation de présentation** contrôlent le résultat.

## Ce dont vous avez besoin

- **.NET 6.0** (ou toute version .NET récente) installé sur votre machine.  
- Une **licence** pour **Aspose.Cells for .NET** (l’essai gratuit suffit pour les tests).  
- Une connaissance de base du C# — rien de compliqué, juste la capacité de créer une application console ou une petite bibliothèque.  
- Un classeur Excel (`input.xlsx`) que vous souhaitez transformer en jeu de diapositives.

C’est tout. Aucun outil supplémentaire, aucun interop COM, juste du code géré pur.

![Diagramme montrant comment exporter des données Excel vers PowerPoint](https://example.com/placeholder.png "Diagramme montrant le flux d'exportation des données Excel vers PowerPoint")

## Étape 1 : Installer Aspose.Cells et configurer le projet

Pour **comment exporter excel** vous avez d'abord besoin de la bibliothèque qui rend cela possible. Ouvrez un terminal dans le dossier de votre projet et exécutez :

```bash
dotnet add package Aspose.Cells
```

Cela récupère le dernier package Aspose.Cells depuis NuGet. La bibliothèque regroupe tout ce dont vous avez besoin pour les **options d'exportation de présentation**, vous n’aurez donc pas à référencer les assemblages Office Interop.

> **Pro tip :** Si vous ciblez le .NET Framework, utilisez la version NuGet appropriée (par ex., `Aspose.Cells.NET`) pour éviter les surprises de compatibilité.

## Étape 2 : Charger le classeur Excel

Maintenant que la bibliothèque est en place, chargeons le fichier source. La classe `Workbook` représente l’ensemble du document Excel.

```csharp
using Aspose.Cells;

// Step 2: Load the Excel workbook
Workbook workbook = new Workbook(@"C:\Data\input.xlsx");
```

*Pourquoi c’est important :* Charger le classeur est la première étape de tout flux de travail **convertir XLSX en PPTX**. L’objet `Workbook` contient les feuilles, les graphiques et le formatage des cellules, tous susceptibles d’être mappés ultérieurement vers des objets PowerPoint.

## Étape 3 : Configurer les options d'exportation de présentation (zones de texte modifiables)

C’est ici que la magie opère. Par défaut, Aspose.Cells exporte les formes sous forme d’images statiques. Pour les garder en **zones de texte modifiables**, vous devez activer le bon indicateur.

```csharp
// Step 3: Create presentation export options and enable editable shapes
PresentationExportOptions exportOptions = new PresentationExportOptions
{
    ExportEditableObjects = true // Makes text boxes and shapes editable in the PPTX
};
```

> **Pourquoi activer `ExportEditableObjects` ?**  
> Lorsque cette propriété est `true`, Aspose.Cells traduit chaque forme Excel en une forme native PowerPoint. Cela signifie que vous pouvez ouvrir le fichier `.pptx` résultant dans PowerPoint et modifier le texte, redimensionner la zone ou changer les couleurs — exactement ce que vous attendez en **créant PowerPoint à partir d'Excel**.

## Étape 4 : Exporter le classeur vers PowerPoint

Avec le classeur chargé et les options configurées, la ligne finale enregistre le fichier sous forme de présentation PowerPoint.

```csharp
// Step 4: Export the workbook to a PowerPoint file using the configured options
workbook.Save(@"C:\Data\output.pptx", SaveFormat.Pptx, exportOptions);
```

*Ce que vous verrez :* Le fichier `output.pptx` contiendra une diapositive par feuille de calcul (par défaut). Chaque diapositive reflète la mise en page de la feuille d’origine, et chaque zone de texte que vous avez placée dans Excel deviendra une **zone de texte modifiable** dans PowerPoint.

## Étape 5 : Vérifier le résultat et ajuster si nécessaire

Ouvrez `output.pptx` dans Microsoft PowerPoint :

1. Accédez à une diapositive issue d’une feuille de calcul.  
2. Cliquez sur une zone de texte — vous constaterez que vous pouvez modifier le texte directement.  
3. Ajustez la taille ou la couleur de la forme ; les modifications sont conservées.

Si quelque chose semble incorrect, envisagez les ajustements suivants :

- **Exporter uniquement des feuilles spécifiques :** Utilisez `workbook.Worksheets.RemoveAt(index)` avant d’enregistrer.  
- **Contrôler la mise en page des diapositives :** Définissez `exportOptions.ExportAllSheetsAsSlide = false` et ajoutez les diapositives manuellement.  
- **Conserver le format des graphiques :** Assurez‑vous que les graphiques sont placés sur la feuille avant l’exportation ; ils deviendront automatiquement des graphiques PowerPoint.

## Pièges courants et comment les éviter

| Problème | Pourquoi cela se produit | Solution |
|----------|--------------------------|----------|
| Les formes deviennent des images | `ExportEditableObjects` laissé à la valeur par défaut (`false`) | Définissez `ExportEditableObjects = true` comme indiqué à l’étape 3. |
| Feuilles manquantes | `Save` appelé avant de supprimer les feuilles indésirables | Supprimez ou masquez les feuilles dont vous n’avez pas besoin avant l’exportation. |
| Taille de fichier importante | Images haute résolution intégrées en même temps que les formes | Utilisez `exportOptions.ImageResolution = 150` pour réduire le DPI si nécessaire. |
| Avertissements de compatibilité dans PowerPoint | Utilisation d’une ancienne version d’Aspose.Cells | Mettez à jour vers le dernier package NuGet (prise en charge de PPTX 2016+). |

## Exemple complet fonctionnel

Voici le programme complet que vous pouvez copier‑coller dans une application console. Il inclut toutes les étapes, la gestion des erreurs et les commentaires.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            try
            {
                // 1️⃣ Load the Excel workbook (convert XLSX to PPTX starts here)
                string inputPath = @"C:\Data\input.xlsx";
                Workbook workbook = new Workbook(inputPath);
                Console.WriteLine("Workbook loaded successfully.");

                // 2️⃣ Configure export options – make text boxes editable
                PresentationExportOptions exportOptions = new PresentationExportOptions
                {
                    ExportEditableObjects = true,
                    // Optional: tweak image resolution to keep file size reasonable
                    ImageResolution = 150
                };
                Console.WriteLine("Export options configured (editable text boxes enabled).");

                // 3️⃣ Save as PowerPoint
                string outputPath = @"C:\Data\output.pptx";
                workbook.Save(outputPath, SaveFormat.Pptx, exportOptions);
                Console.WriteLine($"File saved as PowerPoint: {outputPath}");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Error during conversion: {ex.Message}");
                // In a real app you might log the stack trace or rethrow.
            }
        }
    }
}
```

**Sortie attendue dans la console :**

```
Workbook loaded successfully.
Export options configured (editable text boxes enabled).
File saved as PowerPoint: C:\Data\output.pptx
```

Ouvrez le `output.pptx` généré — vous verrez chaque feuille de calcul transformée en diapositive, et chaque forme que vous avez ajoutée dans Excel est maintenant une **zone de texte modifiable** que vous pouvez ajuster à la volée.

## Récapitulatif : Comment exporter Excel rapidement et proprement

Nous avons couvert l’ensemble du processus **comment exporter excel** — de l’installation d’Aspose.Cells, en passant par la configuration des **options d'exportation de présentation**, jusqu’à la **conversion XLSX en PPTX** avec du contenu entièrement modifiable. Les points clés à retenir sont :

- Utilisez `PresentationExportOptions.ExportEditableObjects = true` pour garder les formes modifiables.  
- La méthode `Workbook.Save` fait le gros du travail ; aucun interop COM n’est nécessaire.  
- Ajustez les paramètres optionnels (résolution d’image, sélection de feuilles) pour affiner le résultat.

## Et après ?

Si vous avez apprécié transformer des feuilles de calcul en diapositives, vous pourriez également explorer :

- **Intégrer des graphiques** en tant que graphiques PowerPoint natifs (`exportOptions.ExportChartAsShape = false`).  
- **Appliquer un masque de diapositive personnalisé** après l’exportation pour correspondre à l’identité visuelle de votre entreprise.  
- **Automatiser des conversions par lots** pour des dizaines de fichiers à l’aide d’une simple boucle `foreach`.  

Tous ces sujets reposent sur les mêmes fondamentaux que nous venons de couvrir, vous êtes donc déjà sur une base solide.

---

N’hésitez pas à laisser un commentaire si vous rencontrez des difficultés, ou à partager la façon dont vous avez étendu ce modèle dans vos propres projets. Bon codage, et profitez du pont fluide entre Excel et PowerPoint !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Comment convertir Excel en PowerPoint avec Aspose.Cells pour .NET : Guide complet](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [Comment ajouter et accéder aux zones de texte dans Excel avec Aspose.Cells .NET | Guide étape par étape](/cells/english/net/images-shapes/aspose-cells-net-add-text-boxes-excel/)
- [Comment exporter des fichiers Excel en .NET avec Aspose.Cells : Guide complet](/cells/english/net/workbook-operations/export-excel-files-net-aspose-cells-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}