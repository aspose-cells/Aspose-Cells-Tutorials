---
category: general
date: 2026-03-22
description: Apprenez à exporter Excel vers PowerPoint, à définir la zone d’impression
  dans Excel et à enregistrer Excel au format PPTX avec des graphiques modifiables
  et des objets OLE en quelques étapes seulement.
draft: false
keywords:
- export excel to powerpoint
- set print area excel
- save excel as pptx
- editable charts PowerPoint
- OLE objects export
language: fr
og_description: Exportez Excel vers PowerPoint rapidement. Ce tutoriel montre comment
  définir la zone d’impression dans Excel et enregistrer le fichier Excel au format
  PPTX avec des graphiques modifiables et des objets OLE.
og_title: Exporter Excel vers PowerPoint – Guide complet C#
tags:
- Aspose.Cells
- C#
- Office Automation
title: Exporter Excel vers PowerPoint – Guide complet C#
url: /fr/net/converting-excel-files-to-other-formats/export-excel-to-powerpoint-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exporter Excel vers PowerPoint – Guide complet C#

Besoin d'**exporter Excel vers PowerPoint** ? Vous êtes au bon endroit. Que vous créiez un deck de ventes hebdomadaire ou que vous automatisiez un pipeline de reporting, transformer une feuille Excel en une présentation PowerPoint peut vous faire gagner des heures de copier‑coller.  

Dans ce tutoriel, nous parcourrons un exemple pratique qui non seulement **export excel to powerpoint**, mais montre aussi comment **set print area Excel** et **save excel as pptx** afin que les diapositives résultantes conservent les graphiques et les objets OLE entièrement modifiables. À la fin, vous disposerez d'un programme C# prêt à l'emploi qui génère un fichier `.pptx` professionnel sans aucune manipulation manuelle.

## Ce dont vous avez besoin

- **.NET 6+** (tout runtime .NET récent fonctionne ; le code utilise la syntaxe C# 10)
- **Aspose.Cells for .NET** – la bibliothèque qui assure l'export. Vous pouvez l'obtenir via NuGet (`Install-Package Aspose.Cells`).
- Un classeur Excel contenant au moins un graphique et/ou un objet OLE (le fichier d'exemple `ChartAndOle.xlsx` est utilisé dans le code).
- Un IDE préféré (Visual Studio, Rider ou VS Code – ce qui vous convient).

C’est tout. Pas d’interop COM, pas d’installation d’Office requise.  

> **Pourquoi passer par une bibliothèque ?**  
> L’Interop Office intégré est fragile, nécessite Office sur le serveur, et produit souvent des images rasterisées alors que vous voulez des formes vectorielles et modifiables. Aspose.Cells prend en charge le travail lourd et garde tout éditable dans PowerPoint.

---

## Étape 1 : Charger le classeur Excel  

Tout d'abord, nous chargeons le fichier source en mémoire. La classe `Workbook` abstrait l’ensemble du fichier Excel, nous donnant accès aux feuilles, graphiques et objets OLE.

```csharp
using Aspose.Cells;

try
{
    // Load the Excel file that contains the chart and OLE object.
    // Adjust the path to point to your own workbook.
    Workbook workbook = new Workbook(@"C:\MyProjects\ChartAndOle.xlsx");
}
catch (Exception ex)
{
    Console.WriteLine($"Failed to load workbook: {ex.Message}");
    return;
}
```

**Pourquoi c’est important :** Le chargement du classeur est la base. Si le chemin est incorrect ou que le fichier est corrompu, le reste du pipeline ne s’exécutera jamais. Le bloc `try…catch` vous fournit une erreur conviviale au lieu d’un plantage.

---

## Étape 2 : Définir la zone d’impression dans Excel  

Avant l’export, vous voulez généralement limiter la sortie à une plage spécifique. C’est là que **set print area excel** entre en jeu. En définissant une zone d’impression, vous indiquez à Aspose.Cells exactement quelles cellules (et quels objets associés) doivent apparaître sur la diapositive.

```csharp
// Assuming we want to export only the range A1:H30 on the first worksheet.
Worksheet sheet = workbook.Worksheets[0];
sheet.PageSetup.PrintArea = "A1:H30";
```

> **Astuce :** Si vous avez plusieurs feuilles, répétez l’affectation `PrintArea` pour chacune de celles que vous prévoyez d’exporter. Laisser la zone d’impression non définie exportera la feuille entière, ce qui peut alourdir le fichier PowerPoint.

---

## Étape 3 : Configurer les options d’export – Conserver les graphiques & OLE éditables  

Aspose.Cells propose un riche objet `ImageOrPrintOptions`. En activant `ExportChartObjects` et `ExportOleObjects`, nous préservons la nature vectorielle des graphiques et l’éditabilité des objets OLE (comme les documents Word ou PDF intégrés).

```csharp
ImageOrPrintOptions pptExportOptions = new ImageOrPrintOptions
{
    SaveFormat = SaveFormat.Pptx,   // We want a PPTX, not a PNG or PDF.
    ExportChartObjects = true,      // Charts stay editable in PowerPoint.
    ExportOleObjects = true         // OLE objects remain live (you can double‑click to edit).
};
```

**Que se passe-t-il en coulisses ?**  
Lorsque `ExportChartObjects` est `true`, Aspose convertit le graphique en une forme native PowerPoint, conservant séries, axes et formatage. Avec `ExportOleObjects` activé, les objets intégrés sont insérés comme cadres OLE, de sorte qu’un double‑clic dans PowerPoint ouvre l’application d’origine (Word, Excel, etc.) pour les modifier.

---

## Étape 4 : Enregistrer la feuille en fichier PowerPoint éditable  

Nous rassemblons maintenant le tout. La méthode `Save` écrit le fichier `.pptx` en utilisant les options que nous avons configurées. Le résultat est un deck où chaque feuille devient une diapositive (ou une série de diapositives si la zone d’impression s’étend sur plusieurs pages).

```csharp
// Save the first worksheet as an editable PowerPoint presentation.
workbook.Save(@"C:\MyProjects\EditableChartOle.pptx", pptExportOptions);
Console.WriteLine("Export completed! Check EditableChartOle.pptx.");
```

### Résultat attendu

- **Emplacement du fichier :** `C:\MyProjects\EditableChartOle.pptx`
- **Contenu :**  
  - Une diapositive affichant la plage `A1:H30` exactement comme elle apparaît dans Excel.  
  - Tous les graphiques sont des objets graphiques PowerPoint — cliquez sur une barre et modifiez les données.  
  - Les objets OLE (par ex., un document Word intégré) peuvent être ouverts et modifiés directement depuis la diapositive.

Si vous ouvrez le PPTX dans PowerPoint, vous devriez voir une diapositive propre avec des composants entièrement éditables—pas de captures d’écran rasterisées.

---

## Cas particuliers & variantes  

### Plusieurs feuilles → Plusieurs diapositives  
Si vous voulez que chaque feuille devienne sa propre diapositive, bouclez simplement sur `workbook.Worksheets` et appelez `Save` avec un `SheetToImageOptions` ciblant un indice de feuille spécifique. Aspose générera automatiquement une nouvelle diapositive pour chaque itération.

```csharp
for (int i = 0; i < workbook.Worksheets.Count; i++)
{
    ImageOrPrintOptions opts = new ImageOrPrintOptions
    {
        SaveFormat = SaveFormat.Pptx,
        ExportChartObjects = true,
        ExportOleObjects = true,
        OnePagePerSheet = true   // Ensures each sheet starts on a new slide.
    };
    workbook.Save($"Sheet{i + 1}.pptx", opts);
}
```

### Grandes plages & performances  
Exporter une zone d’impression massive (par ex., `A1:Z1000`) peut augmenter l’utilisation de mémoire. Pour atténuer le problème, envisagez :  
- De diviser la plage en morceaux plus petits et de les exporter comme diapositives séparées.  
- D’utiliser `WorkbookSettings` pour augmenter le `MemorySetting` si vous rencontrez une `OutOfMemoryException`.

### Problèmes de compatibilité  
Le PPTX généré fonctionne avec PowerPoint 2016 et versions ultérieures. Les versions plus anciennes peuvent tout de même ouvrir le fichier mais perdre certaines fonctionnalités avancées de graphique. Testez toujours sur la version Office cible si vous distribuez largement le deck.

---

## Exemple complet fonctionnel (prêt à copier‑coller)

```csharp
// ---------------------------------------------------------------
// Export Excel to PowerPoint – Complete C# Example
// ---------------------------------------------------------------

using System;
using Aspose.Cells;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the workbook.
            string excelPath = @"C:\MyProjects\ChartAndOle.xlsx";
            Workbook workbook;
            try
            {
                workbook = new Workbook(excelPath);
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Error loading Excel file: {ex.Message}");
                return;
            }

            // 2️⃣ Set the print area (set print area excel).
            Worksheet sheet = workbook.Worksheets[0];
            sheet.PageSetup.PrintArea = "A1:H30";

            // 3️⃣ Configure export options – keep charts & OLE objects editable.
            ImageOrPrintOptions pptExportOptions = new ImageOrPrintOptions
            {
                SaveFormat = SaveFormat.Pptx,
                ExportChartObjects = true,
                ExportOleObjects = true
            };

            // 4️⃣ Save as PPTX (save excel as pptx).
            string pptxPath = @"C:\MyProjects\EditableChartOle.pptx";
            try
            {
                workbook.Save(pptxPath, pptExportOptions);
                Console.WriteLine($"Success! PPTX created at: {pptxPath}");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Failed to save PPTX: {ex.Message}");
            }
        }
    }
}
```

> **Conseil :** Remplacez les chemins codés en dur par des valeurs de configuration ou des arguments en ligne de commande pour un outil plus flexible.

---

## FAQ  

**Q : Puis‑je exporter uniquement un graphique sans les cellules environnantes ?**  
R : Oui. Utilisez uniquement `ExportChartObjects` et définissez la zone d’impression sur la plage englobant le graphique. Le graphique apparaîtra centré sur la diapositive.

**Q : Que se passe‑t‑il si mon classeur contient des macros ?**  
R : Aspose.Cells ignore les macros VBA lors de l’export. Si vous avez besoin de fonctionnalité macro dans PowerPoint, vous devrez la recréer avec VBA PowerPoint ou des add‑ins.

**Q : Cela fonctionne‑t‑il sous Linux/macOS ?**  
R : Absolument. Aspose.Cells est une bibliothèque .NET pure ; tant que le runtime .NET est présent, le code s’exécute multiplateforme.

---

## Conclusion  

Vous venez d’apprendre comment **exporter Excel vers PowerPoint** tout en définissant précisément **set print area excel** et **save excel as pptx** avec des graphiques et objets OLE entièrement éditables. Les étapes clés sont le chargement du classeur, la définition de la zone d’impression, la configuration de `ImageOrPrintOptions`, puis l’enregistrement du PPTX.  

À partir d’ici, vous pouvez explorer :  
- L’exportation de plusieurs feuilles dans un même deck.  
- L’ajout de titres ou de notes de diapositive personnalisés par programme.  
- La conversion du PPTX en PDF pour la distribution (utilisez `SaveFormat.Pdf`).  

Testez le code, ajustez la zone d’impression, et voyez vos données Excel apparaître magiquement dans PowerPoint—sans copier‑coller manuel. En cas de problème, consultez la documentation Aspose.Cells ou laissez un commentaire ci‑dessous. Bon codage !  

![Diagram showing export excel to powerpoint workflow](/images/export-excel-to-powerpoint.png "export excel to powerpoint workflow")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}