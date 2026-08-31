---
category: general
date: 2026-02-21
description: Créez rapidement un PowerPoint à partir d’Excel. Apprenez à exporter
  Excel vers PowerPoint avec du texte et des graphiques modifiables en utilisant Aspose.Cells
  en seulement quelques lignes de C#.
draft: false
keywords:
- create powerpoint from excel
- export excel to powerpoint
- export editable text
- export excel chart powerpoint
- convert excel chart powerpoint
language: fr
og_description: Créez un PowerPoint à partir d'Excel avec du texte et des graphiques
  modifiables. Suivez ce guide détaillé pour exporter Excel vers PowerPoint à l'aide
  d'Aspose.Cells.
og_title: Créer PowerPoint à partir d'Excel – Guide C# étape par étape
tags:
- C#
- Aspose.Cells
- PowerPoint
- Excel Automation
title: Créer PowerPoint à partir d'Excel – Tutoriel complet C#
url: /fr/net/converting-excel-files-to-other-formats/create-powerpoint-from-excel-complete-c-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer PowerPoint à partir d'Excel – Tutoriel complet C#

Vous avez déjà eu besoin de **créer PowerPoint à partir d'Excel** sans savoir quelle API utiliser ? Vous n'êtes pas seul. De nombreux développeurs se heurtent à un mur lorsqu'ils veulent transformer une feuille de calcul riche en données en un diaporama soigné, surtout lorsqu'ils souhaitent que les zones de texte restent éditables après la conversion.  

Dans ce guide, nous vous montrons comment **exporter Excel vers PowerPoint** tout en conservant le texte éditable, la fidélité des graphiques et la mise en page—le tout avec quelques lignes de C#. À la fin, vous disposerez d’un fichier PPTX prêt à l’emploi que vous pourrez ajuster dans PowerPoint comme n’importe quelle diapositive créée manuellement.

## Ce que vous allez apprendre

- Comment charger un classeur Excel contenant des graphiques et des formes.  
- Comment configurer `PresentationExportOptions` afin que les zones de texte restent éditables (`export editable text`).  
- Comment réellement **exporter Excel chart PowerPoint** et obtenir un diaporama propre.  
- Petites variantes que vous pouvez appliquer lorsque vous devez **convertir Excel chart PowerPoint** pour différentes configurations de page ou plusieurs feuilles de calcul.  

### Prérequis

- Un environnement de développement .NET (Visual Studio 2022 ou version ultérieure).  
- Aspose.Cells for .NET (version d’essai gratuite ou version sous licence).  
- Un fichier Excel (`ChartWithShape.xlsx`) contenant au moins un graphique et une forme que vous souhaitez garder éditable.  

Si vous avez tout cela, plongeons‑y—sans fioritures, juste une solution pratique et exécutable.

## Créer PowerPoint à partir d'Excel – Étape par étape

Après chaque étape, nous présenterons un extrait de code concis, expliquerons **pourquoi** nous le faisons et soulignerons les pièges courants. N’hésitez pas à copier‑coller l’exemple complet en bas de la page.

### Étape 1 : Charger le classeur Excel

Tout d’abord, nous devons charger le classeur source en mémoire. Aspose.Cells lit le fichier et construit un modèle d’objet riche que nous pouvons manipuler.

```csharp
// Step 1: Load the Excel workbook that contains the chart and shape
Workbook workbook = new Workbook("YOUR_DIRECTORY/ChartWithShape.xlsx");

// Quick sanity check – make sure the workbook actually loaded
if (workbook.Worksheets.Count == 0)
    throw new InvalidOperationException("The workbook appears to be empty.");
```

**Pourquoi c’est important :**  
Le chargement du classeur est la base. Si le chemin du fichier est incorrect ou si le classeur est corrompu, toutes les étapes suivantes d’`export excel to powerpoint` échoueront. La vérification de validité vous donne un retour immédiat au lieu d’un vague « file not found » plus tard.

### Étape 2 : Préparer les options d’exportation

Aspose.Cells vous fournit un objet `PresentationExportOptions` qui contrôle l’apparence du PPTX. C’est ici que vous décidez si le texte doit rester éditable.

```csharp
// Step 2: Create export options for PowerPoint conversion
PresentationExportOptions exportOptions = new PresentationExportOptions();

// Optional: tweak the slide size (default is 10in x 7.5in)
exportOptions.SlideSize = new SizeF(10, 7.5f);
```

**Pourquoi c’est important :**  
Sans configurer `PresentationExportOptions`, la bibliothèque utilise ses valeurs par défaut, qui peuvent ne pas correspondre à votre modèle de diapositive d’entreprise. Ajuster la taille de la diapositive dès le départ évite de devoir la redimensionner manuellement plus tard.

### Étape 3 : Activer les zones de texte éditables

Le drapeau magique `ExportEditableTextBoxes` indique à Aspose.Cells de conserver les formes de texte comme des zones de texte PowerPoint, et non comme des images statiques.

```csharp
// Step 3: Enable editability of text boxes in the resulting presentation
exportOptions.ExportEditableTextBoxes = true;
```

**Pourquoi c’est important :**  
Si vous omettez cette ligne, le PPTX résultant contiendra du texte rasterisé—vous ne pourrez donc pas modifier le libellé ou la légende dans PowerPoint. Activer `export editable text` est la clé d’un diaporama réellement réutilisable.

### Étape 4 : Exporter la feuille de calcul vers PPTX

Nous écrivons maintenant le fichier PPTX. Vous pouvez choisir n’importe quelle feuille ; ici nous utilisons la première (`Worksheets[0]`).

```csharp
// Step 4: Export the first worksheet's page setup to a PPTX file
workbook.Worksheets[0].PageSetup.SaveToPptx("YOUR_DIRECTORY/Result.pptx", exportOptions);
```

**Pourquoi c’est important :**  
`SaveToPptx` respecte la configuration de la page (marges, orientation) que vous avez définie dans Excel, de sorte que la diapositive reflète la mise en page que vous avez déjà conçue. C’est le cœur de **export excel chart powerpoint**.

### Étape 5 : Vérifier le résultat (Optionnel mais recommandé)

Après la conversion, ouvrez le `Result.pptx` généré dans PowerPoint et vérifiez :

1. Les graphiques apparaissent nets et conservent les séries de données.  
2. Les zones de texte sont sélectionnables et éditables.  
3. La taille de la diapositive correspond à vos attentes.

Si quelque chose semble incorrect, revenez sur `exportOptions`—par exemple, vous pourriez devoir définir `exportOptions.IncludePrintArea = true` pour respecter une zone d’impression nommée.

```csharp
// Optional: open the PPTX automatically (requires System.Diagnostics)
System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
{
    FileName = "YOUR_DIRECTORY/Result.pptx",
    UseShellExecute = true
});
```

### Étape 6 : Variantes avancées (Exporter plusieurs feuilles)

Souvent, vous voudrez **convertir excel chart powerpoint** pour plusieurs feuilles en même temps. Parcourez la collection et attribuez à chaque diapositive un nom unique :

```csharp
for (int i = 0; i < workbook.Worksheets.Count; i++)
{
    string outputPath = $"YOUR_DIRECTORY/Result_Sheet{i + 1}.pptx";
    workbook.Worksheets[i].PageSetup.SaveToPptx(outputPath, exportOptions);
}
```

**Astuce :** Si vous avez besoin de toutes les feuilles dans un *seul* PPTX, créez un nouvel objet `Presentation`, importez chaque diapositive, puis enregistrez une fois. C’est un peu plus complexe mais vous évite de jongler avec de nombreux fichiers.

## Exemple complet fonctionnel

Voici le programme complet que vous pouvez coller dans une application console et exécuter immédiatement.

```csharp
using System;
using System.Drawing;
using Aspose.Cells;
using Aspose.Cells.Export;

class Program
{
    static void Main()
    {
        // 1️⃣ Load workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/ChartWithShape.xlsx");
        if (workbook.Worksheets.Count == 0)
        {
            Console.WriteLine("Workbook is empty – aborting.");
            return;
        }

        // 2️⃣ Set up export options
        PresentationExportOptions exportOptions = new PresentationExportOptions
        {
            SlideSize = new SizeF(10, 7.5f),          // optional custom size
            ExportEditableTextBoxes = true           // <‑‑ keep text boxes editable
        };

        // 3️⃣ Export first worksheet
        string outputPath = "YOUR_DIRECTORY/Result.pptx";
        workbook.Worksheets[0].PageSetup.SaveToPptx(outputPath, exportOptions);
        Console.WriteLine($"PowerPoint created at: {outputPath}");

        // 4️⃣ Open the result automatically (Windows only)
        try
        {
            System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
            {
                FileName = outputPath,
                UseShellExecute = true
            });
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Could not open PPTX automatically: {ex.Message}");
        }
    }
}
```

**Résultat attendu :**  
Lorsque vous ouvrez `Result.pptx`, vous voyez une diapositive qui reflète la mise en page de la feuille Excel. Tout graphique placé dans Excel apparaît comme un graphique PowerPoint natif, et la légende ajoutée comme forme devient maintenant une zone de texte entièrement éditable.

## Questions fréquentes & cas particuliers

- **Cela fonctionne-t-il avec des classeurs contenant des macros (`.xlsm`)?**  
  Oui. Aspose.Cells lit les macros mais ne les exécute pas. Le processus de conversion ignore le VBA, vous obtenez donc toujours le contenu visuel.

- **Et si ma feuille contient plusieurs graphiques ?**  
  Tous les graphiques visibles sont transférés sur la même diapositive. Si vous avez besoin d’une diapositive par graphique, séparez les feuilles ou utilisez la boucle présentée à l’Étape 6.

- **Puis‑je conserver des thèmes PowerPoint personnalisés ?**  
  Pas directement lors de l’exportation. Après la conversion, vous pouvez appliquer un thème dans PowerPoint ou programmatique via Aspose.Slides.

- **Existe‑t‑il un moyen d’exporter uniquement une plage sélectionnée ?**  
  Définissez une zone d’impression nommée dans Excel (`Mise en page → Zone d’impression`) et activez `exportOptions.IncludePrintArea = true`.

## Conclusion

Vous savez maintenant comment **créer PowerPoint à partir d'Excel** avec Aspose.Cells, en maîtrisant le texte éditable, la fidélité des graphiques et la taille des diapositives. Le court extrait de code que nous avons partagé couvre le scénario le plus courant, et les astuces supplémentaires vous offrent de la flexibilité lorsque vous devez **export excel to powerpoint** pour plusieurs feuilles ou des mises en page personnalisées.  

Prêt pour le prochain défi ? Essayez de combiner cette approche avec **Aspose.Slides** pour ajouter programmatique des transitions, des notes du présentateur, ou même intégrer les diapositives générées dans une présentation plus vaste. Ou expérimentez la conversion d’un classeur entier en un diaporama multi‑diapositives—idéal pour des pipelines de reporting automatisés.

Des questions, ou une astuce ingénieuse à partager ? Laissez un commentaire ci‑dessous, et bon codage !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}