---
category: general
date: 2026-08-17
description: Enregistrez Excel en PowerPoint avec C# – guide étape par étape pour
  convertir les fichiers XLSX, rendre les zones de texte modifiables et générer une
  sortie PPTX.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save excel as powerpoint
- convert excel to powerpoint
- how to convert xlsx
- make textbox editable
- how to edit textboxes
language: fr
lastmod: 2026-08-17
og_description: Enregistrez Excel en PowerPoint en C# avec un exemple complet de code.
  Apprenez à convertir XLSX, rendre les zones de texte modifiables et exporter en
  PPTX.
og_image_alt: Screenshot showing Excel data saved as a PowerPoint slide
og_title: Enregistrer Excel en PowerPoint avec C# – guide complet de conversion
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: Save Excel as PowerPoint with C# – step‑by‑step guide to convert XLSX
    files, make textboxes editable, and generate PPTX output.
  headline: How to save Excel as PowerPoint using C# and Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel-to-PowerPoint
title: Comment enregistrer un fichier Excel au format PowerPoint avec C# et Aspose.Cells
url: /fr/net/converting-excel-files-to-other-formats/how-to-save-excel-as-powerpoint-using-c-and-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment enregistrer Excel en PowerPoint avec C# et Aspose.Cells

Si vous devez **enregistrer Excel en PowerPoint** dans un projet .NET, ce guide vous propose une solution complète, prête à l’emploi. Vous verrez comment charger un classeur XLSX, rendre chaque zone de texte de la feuille modifiable, et exporter le résultat vers un fichier PPTX — le tout en quelques lignes de C#.

Convertir Excel en PowerPoint est une exigence fréquente pour les tableaux de bord de reporting, les présentations de diapositives ou la génération automatisée de présentations. Ce tutoriel couvre également **comment modifier les zones de texte** par programme, afin que vous puissiez personnaliser le contenu des diapositives avant l’enregistrement.

## Prérequis

Avant de commencer, assurez‑vous d’avoir :

* SDK .NET 6.0 (ou version ultérieure) installé  
* Un environnement de développement tel que Visual Studio 2022 ou VS Code  
* Une licence Aspose.Cells for .NET (ou une clé d’évaluation gratuite) – téléchargez‑la depuis le [site Aspose](https://products.aspose.com/cells/net/)  
* Le fichier `input.xlsx` que vous souhaitez convertir  

> **Astuce :** Si vous utilisez la version d’évaluation gratuite, le PPTX de sortie contiendra un filigrane. Une version sous licence le supprime.

## Étape 1 : Installer le package NuGet Aspose.Cells

Ouvrez un terminal dans le dossier de votre projet et exécutez :

```bash
dotnet add package Aspose.Cells
```

Cela ajoute l’assembly `Aspose.Cells`, qui fournit les classes `Workbook`, `Worksheet` et `Shape` nécessaires à la conversion.

## Étape 2 : Créer la structure d’une application console

Créez un nouveau projet console (si vous n’en avez pas déjà un) :

```bash
dotnet new console -n ExcelToPptxDemo
cd ExcelToPptxDemo
```

Remplacez le fichier `Program.cs` généré par le code présenté dans les étapes suivantes.

## Étape 3 : Charger le classeur et sélectionner la première feuille

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;

class Program
{
    static void Main()
    {
        // Load the workbook from a file – adjust the path to your environment
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(inputPath);

        // Get the first worksheet in the workbook
        Worksheet worksheet = workbook.Worksheets[0];
```

**Pourquoi c’est important :**  
`Workbook` lit le fichier Excel en mémoire, tandis que `Worksheet` vous donne accès aux cellules, graphiques et formes de la feuille. La première feuille est souvent le rapport par défaut que vous voulez présenter.

## Étape 4 : Rendre chaque zone de texte de la feuille modifiable

```csharp
        // Iterate through all shapes on the worksheet
        foreach (Shape shapeItem in worksheet.Shapes)
        {
            // Check if the shape is a textbox (ShapeType.TextBox)
            if (shapeItem.Type == ShapeType.TextBox)
            {
                // The IsEditable property was added in Aspose.Cells 25.11
                shapeItem.TextBox.IsEditable = true;
            }
        }
```

**Pourquoi vous en avez besoin :**  
Par défaut, les zones de texte importées depuis Excel sont en lecture‑seule lorsqu’elles sont rendues dans PowerPoint. Le fait de définir `IsEditable = true` permet à vous (ou aux utilisateurs de PowerPoint ultérieurs) de modifier le texte directement sur la diapositive.

## Étape 5 : Enregistrer le classeur en tant que présentation PowerPoint

```csharp
        // Define the output path for the PPTX file
        string outputPath = @"YOUR_DIRECTORY\output.pptx";

        // Save the workbook as a PowerPoint presentation
        workbook.Save(outputPath, SaveFormat.Pptx);

        Console.WriteLine($"Conversion complete. PPTX saved to: {outputPath}");
    }
}
```

**Ce qui se passe en coulisses :**  
`Workbook.Save` détecte la valeur d’énumération `SaveFormat.Pptx` et traduit la mise en page de la feuille Excel — lignes, colonnes, graphiques et zones de texte désormais modifiables — en objets de diapositive PowerPoint.

## Code source complet (exécutable)

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;

class Program
{
    static void Main()
    {
        // Step 1: Load the workbook from a file
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(inputPath);

        // Step 2: Get the first worksheet in the workbook
        Worksheet worksheet = workbook.Worksheets[0];

        // Step 3: Make every textbox on the sheet editable (property added in version 25.11)
        foreach (Shape shapeItem in worksheet.Shapes)
        {
            if (shapeItem.Type == ShapeType.TextBox)
            {
                shapeItem.TextBox.IsEditable = true;
            }
        }

        // Step 4: Save the workbook as a PowerPoint presentation
        string outputPath = @"YOUR_DIRECTORY\output.pptx";
        workbook.Save(outputPath, SaveFormat.Pptx);

        Console.WriteLine($"Conversion complete. PPTX saved to: {outputPath}");
    }
}
```

### Résultat attendu

Lorsque vous exécutez le programme (`dotnet run`), vous devez voir :

```
Conversion complete. PPTX saved to: YOUR_DIRECTORY\output.pptx
```

L’ouverture de `output.pptx` dans Microsoft PowerPoint affichera une diapositive qui reflète la feuille Excel d’origine. Toutes les zones de texte peuvent être modifiées directement en double‑cliquant dessus.

## Questions fréquentes et cas particuliers

| Question | Réponse |
|----------|--------|
| **Puis‑je convertir une feuille spécifique au lieu de la première ?** | Oui. Remplacez `workbook.Worksheets[0]` par `workbook.Worksheets["SheetName"]` ou tout autre indice dont vous avez besoin. |
| **Que faire si le classeur contient plusieurs feuilles ?** | Appelez `workbook.Save` une fois par feuille, en fournissant un nom de fichier PPTX distinct pour chaque, ou combinez‑les dans une seule présentation en utilisant les objets `Presentation` d’Aspose.Slides. |
| **Les graphiques seront‑ils conservés ?** | Aspose.Cells convertit automatiquement les graphiques Excel en objets de graphique PowerPoint. Aucun code supplémentaire n’est requis. |
| **Comment modifier la taille de la diapositive ?** | Après `workbook.Save`, vous pouvez charger le PPTX généré avec Aspose.Slides et ajuster `Presentation.SlideSize`. |
| **Comment modifier le texte de la zone de texte avant l’enregistrement ?** | Accédez à `shapeItem.TextBox.Text` dans la boucle, modifiez‑le, puis définissez `IsEditable = true`. Exemple : `shapeItem.TextBox.Text = "Nouveau titre";` |

## Conseils de dépannage

* **« ShapeType.TextBox » introuvable** – Assurez‑vous d’utiliser la version 25.11 ou plus récente d’Aspose.Cells ; les versions antérieures ne possèdent pas la propriété `IsEditable`.  
* **Erreurs « File not found »** – Vérifiez que `YOUR_DIRECTORY` est un chemin absolu ou que le chemin relatif pointe bien vers l’emplacement correct.  
* **Licence non appliquée** – Appelez `License license = new License(); license.SetLicense("Aspose.Total.NET.lic");` avant de charger le classeur pour supprimer les filigranes d’évaluation.

## Conclusion

Vous savez maintenant comment **enregistrer Excel en PowerPoint** avec C# en chargeant un classeur XLSX, en rendant chaque zone de texte modifiable, et en exportant vers PPTX. Cette méthode gère automatiquement les graphiques, images et formats de cellules, vous offrant un diaporama prêt à être présenté.

Ensuite, explorez des sujets connexes tels que **convertir Excel en PowerPoint avec Aspose.Slides**, **comment modifier les zones de texte par programme après la conversion**, ou **traiter plusieurs classeurs en lot**. Chacun de ces sujets s’appuie sur les étapes de base présentées ici et peut encore automatiser votre flux de travail de reporting.

## Que devez‑vous apprendre ensuite ?

Les tutoriels suivants traitent de sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités supplémentaires de l’API et à explorer des approches d’implémentation alternatives dans vos propres projets.

- [Comment convertir Excel en PowerPoint avec Aspose.Cells pour .NET : guide complet](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [Comment copier un tableau croisé dynamique en C# – Convertir Excel en PPTX, copier une plage et rendre la zone de texte modifiable](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)
- [Comment enregistrer des fichiers Excel dans plusieurs formats avec Aspose.Cells .NET (guide 2023)](/cells/english/net/workbook-operations/aspose-cells-net-save-excel-formats/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}