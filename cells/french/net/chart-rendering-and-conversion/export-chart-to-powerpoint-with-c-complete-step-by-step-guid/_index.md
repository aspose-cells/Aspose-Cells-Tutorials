---
category: general
date: 2026-02-26
description: Exporter un graphique vers PowerPoint depuis Excel avec C#. Apprenez
  à convertir Excel en PowerPoint, enregistrer Excel en tant que PowerPoint et conserver
  les formes modifiables.
draft: false
keywords:
- export chart to powerpoint
- convert excel to powerpoint
- save excel as powerpoint
- how to convert excel to ppt
- save workbook as pptx
language: fr
og_description: Exporter un graphique vers PowerPoint depuis Excel avec C#. Ce guide
  montre comment convertir Excel en PowerPoint, enregistrer le classeur au format
  PPTX et conserver les formes éditables.
og_title: Exporter un graphique vers PowerPoint avec C# – Tutoriel complet de programmation
tags:
- Aspose.Cells
- C#
- Office Automation
title: Exporter un graphique vers PowerPoint avec C# – Guide complet étape par étape
url: /fr/net/chart-rendering-and-conversion/export-chart-to-powerpoint-with-c-complete-step-by-step-guid/
---

Let's write.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exporter un graphique vers PowerPoint – Tutoriel complet de programmation

Vous êtes-vous déjà demandé comment **exporter un graphique vers PowerPoint** sans perdre la possibilité de le modifier ? Dans de nombreux scénarios de reporting, vous avez besoin d’un graphique dynamique dans une présentation, mais copier‑coller manuellement est fastidieux. La bonne nouvelle, c’est que vous pouvez le faire de façon programmatique avec quelques lignes de C#.

Dans ce guide, nous parcourrons l’ensemble du processus : charger un classeur Excel contenant un graphique avec une zone de texte, configurer l’exportation afin que les zones de texte et les formes restent éditables, puis enregistrer le résultat sous forme de fichier **PowerPoint**. À la fin, vous saurez également comment **convertir Excel en PowerPoint**, **enregistrer Excel en PowerPoint**, et même ajuster les options pour des scénarios particuliers.

## Ce dont vous avez besoin

- **Aspose.Cells for .NET** (version 23.10 ou ultérieure). C’est la bibliothèque qui rend la conversion simple.
- Runtime **.NET 6+** – tout SDK récent convient.
- Un fichier Excel simple (`ChartWithTextbox.xlsx`) contenant au moins un graphique et une zone de texte.
- Visual Studio ou votre IDE préféré.

Aucun package NuGet supplémentaire n’est requis au‑delà d’Aspose.Cells, mais une bonne maîtrise de la syntaxe C# aide toujours.

## Exporter un graphique vers PowerPoint – Étape par étape

Nous décomposons la solution en étapes distinctes et faciles à suivre. Chaque étape comprend le code exact dont vous avez besoin, ainsi qu’un court paragraphe « pourquoi » expliquant la logique.

### Étape 1 : Charger le classeur Excel qui contient le graphique

Tout d’abord, il faut charger le fichier source en mémoire. L’utilisation de `Workbook` d’Aspose.Cells lit l’ensemble de la feuille de calcul, y compris les graphiques, les images et les objets incorporés.

```csharp
using Aspose.Cells;

// Step 1: Load the Excel workbook that contains the chart with a textbox
Workbook workbook = new Workbook(@"C:\Samples\ChartWithTextbox.xlsx");

// Verify that the workbook actually contains a chart
if (workbook.Worksheets[0].Charts.Count == 0)
{
    throw new InvalidOperationException("No chart found in the first worksheet.");
}
```

*Pourquoi c’est important :* Si le classeur est ouvert sans spécifier correctement le chemin, vous obtiendrez une `FileNotFoundException`. Cette vérification rapide vous évite d’exporter une diapositive vide plus tard.

### Étape 2 : Préparer les options de présentation pour garder les formes éditables

Aspose.Cells vous permet de choisir si les zones de texte, les formes et même le graphique restent **éditables** après l’exportation. Mettre `ExportTextBoxes` et `ExportShapes` à `true` préserve ces objets en tant qu’éléments natifs PowerPoint plutôt que de les aplatir en image statique.

```csharp
using Aspose.Cells.Drawing;

// Step 2: Set up presentation options to keep textboxes and shapes editable in the output
PresentationOptions presentationOptions = new PresentationOptions
{
    ExportTextBoxes = true, // Preserve editable textboxes
    ExportShapes    = true  // Preserve shapes such as the chart itself
};
```

*Pourquoi c’est important :* Si vous laissez ces indicateurs à leurs valeurs par défaut (`false`), la diapositive résultante contiendra une image bitmap du graphique, rendant impossible la modification des séries ou du titre ultérieurement. Activer les deux options vous donne un vrai graphique PowerPoint qui se comporte exactement comme celui que vous créeriez manuellement.

### Étape 3 : Convertir Excel en PowerPoint et enregistrer le fichier

Nous invoquons maintenant la méthode `Save`, en passant l’énumération `SaveFormat.Pptx` et les options que nous venons de configurer. La bibliothèque se charge de traduire l’objet graphique Excel en forme graphique PowerPoint.

```csharp
// Step 3: Save the workbook as a PowerPoint presentation using the configured options
workbook.Save(@"C:\Samples\Result.pptx", SaveFormat.Pptx, presentationOptions);
```

*Pourquoi c’est important :* L’appel `Save` effectue tout le travail lourd — mappage des séries Excel vers les séries PowerPoint, préservation du format des axes, et copie des zones de texte liées. Après l’exécution de cette ligne, vous disposerez d’un fichier `.pptx` entièrement éditable, prêt à être ouvert dans Microsoft PowerPoint.

### Vérifier le résultat

Ouvrez `Result.pptx` dans PowerPoint. Vous devriez voir une diapositive contenant :

- Le graphique original, toujours lié à ses données (double‑clic pour modifier les séries).
- Toute zone de texte présente dans la feuille Excel, désormais une zone de texte native PowerPoint.
- La mise en page de la diapositive est choisie automatiquement (généralement une diapositive vierge).

Si vous remarquez des éléments manquants, revérifiez que le classeur source contenait bien les objets visibles et que `ExportTextBoxes` / `ExportShapes` étaient bien à `true`.

### Convertir Excel en PowerPoint : Gestion de plusieurs feuilles

Souvent, un classeur comporte plusieurs feuilles, chacune avec son propre graphique. Par défaut, Aspose.Cells exporte **tous** les graphiques de **toutes** les feuilles vers des diapositives séparées. Si vous n’avez besoin que d’un sous‑ensemble, vous pouvez les filtrer avant l’enregistrement :

```csharp
// Example: Export only charts from the first worksheet
Worksheet firstSheet = workbook.Worksheets[0];
foreach (Chart chart in firstSheet.Charts)
{
    chart.IsVisible = true; // Ensure visibility
}

// Hide charts from other sheets
for (int i = 1; i < workbook.Worksheets.Count; i++)
{
    foreach (Chart chart in workbook.Worksheets[i].Charts)
    {
        chart.IsVisible = false;
    }
}
```

*Astuce :* Mettre `chart.IsVisible = false` est moins coûteux que de supprimer le graphique entièrement, et cela vous permet de basculer l’inclusion sans modifier le fichier source.

### Enregistrer Excel en PowerPoint – Personnaliser la taille de la diapositive

PowerPoint utilise par défaut une diapositive de 10 po × 5,63 po. Si votre graphique semble à l’étroit, vous pouvez modifier les dimensions via l’objet `PresentationOptions` :

```csharp
presentationOptions.SlideSize = new SizeF(13.33f, 7.5f); // 16:9 widescreen
```

Ainsi, le graphique exporté disposera de plus d’espace, et les zones de texte conserveront leur mise en page d’origine.

### Comment convertir Excel en PPT : Gestion des objets cachés

Des lignes, colonnes ou formes masquées peuvent parfois se glisser dans l’exportation. Pour les éliminer, effectuez un nettoyage rapide avant l’enregistrement :

```csharp
// Remove hidden rows/columns that might affect chart layout
foreach (Worksheet sheet in workbook.Worksheets)
{
    sheet.Cells.HideRows = false;
    sheet.Cells.HideColumns = false;
}
```

Cette étape n’est pas toujours nécessaire, mais elle évite les espaces inattendus dans votre jeu de diapositives final.

### Enregistrer le classeur en PPTX – Exemple complet fonctionnel

En rassemblant le tout, voici un programme console prêt à l’emploi qui montre le flux complet :

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing; // For SizeF

class ExportChartDemo
{
    static void Main()
    {
        // Load workbook (Step 1)
        string sourcePath = @"C:\Samples\ChartWithTextbox.xlsx";
        Workbook workbook = new Workbook(sourcePath);

        // Verify chart existence
        if (workbook.Worksheets[0].Charts.Count == 0)
        {
            Console.WriteLine("No chart found. Exiting.");
            return;
        }

        // Configure presentation options (Step 2)
        PresentationOptions options = new PresentationOptions
        {
            ExportTextBoxes = true,
            ExportShapes    = true,
            SlideSize       = new SizeF(13.33f, 7.5f) // optional widescreen
        };

        // Optional: export only first worksheet charts
        for (int i = 1; i < workbook.Worksheets.Count; i++)
        {
            foreach (Chart c in workbook.Worksheets[i].Charts)
                c.IsVisible = false;
        }

        // Save as PowerPoint (Step 3)
        string targetPath = @"C:\Samples\Result.pptx";
        workbook.Save(targetPath, SaveFormat.Pptx, options);

        Console.WriteLine($"Export complete! File saved to {targetPath}");
    }
}
```

L’exécution de ce programme créera `Result.pptx` avec un graphique et une zone de texte éditables, exactement ce que vous attendez en **enregistrant le classeur sous pptx** manuellement.

![Exemple d’exportation de graphique vers PowerPoint](/images/export-chart-to-powerpoint.png "Export chart to PowerPoint – diapositive éditable")

## Questions fréquentes & cas particuliers

**Que se passe‑t‑il si le fichier Excel contient un graphique avec une source de données externe liée ?**  
Aspose.Cells copie les valeurs *actuelles* dans le graphique PowerPoint. Il ne préserve **pas** le lien externe, car PowerPoint ne peut pas référencer une connexion de données Excel de la même façon. Si vous avez besoin de mises à jour en temps réel, envisagez d’insérer le fichier Excel original dans le PPTX comme objet OLE.

**Puis‑je exporter un graphique utilisant un thème personnalisé ?**  
Oui. La bibliothèque tente de mapper les couleurs du thème Excel aux emplacements du thème PowerPoint. Pour des palettes très personnalisées, il peut être nécessaire d’ajuster les couleurs après l’exportation à l’aide de l’API PowerPoint (par ex., Aspose.Slides).

**Existe‑t‑il une limite au nombre de graphiques ?**  
Pratiquement aucune — Aspose.Cells diffuse les données, donc même un classeur contenant des dizaines de graphiques s’exportera, bien que la taille du PPTX résultant augmente linéairement.

**Ai‑je besoin d’une licence pour Aspose.Cells ?**  
Une évaluation gratuite fonctionne, mais elle ajoute un filigrane sur la première diapositive. Pour une utilisation en production, obtenez une licence appropriée afin de supprimer le filigrane et de débloquer les performances complètes.

## Récapitulatif

Nous avons vu comment **exporter un graphique vers PowerPoint** avec C#, présenté le code exact pour charger un classeur Excel, configurer `PresentationOptions` afin que les zones de texte et les formes restent éditables, puis enregistrer le résultat sous forme de `.pptx`. Vous avez également appris à **convertir Excel en PowerPoint**, **enregistrer Excel en PowerPoint**, et à répondre à la question « **comment convertir Excel en ppt** » avec un exemple complet et exécutable.

## Et après ?

- **Enregistrer le classeur en PPTX** avec plusieurs diapositives : bouclez sur chaque feuille et appelez `Save` avec `PresentationOptions` pour chacune.
- Explorez **Aspose.Slides** si vous devez modifier le PPTX généré de façon programmatique (ajouter des transitions, des notes du présentateur, etc.).
- Essayez d’exporter des **graphes croisés dynamiques** ou des **graphes 3D** — les mêmes options s’appliquent, mais vous pourriez devoir ajuster le format des axes par la suite.

Si vous rencontrez le moindre problème, laissez un commentaire ci‑dessous ou consultez la documentation officielle d’Aspose.Cells pour les dernières évolutions de l’API. Bon codage, et profitez de la transformation de vos graphiques Excel en présentations PowerPoint soignées en quelques lignes de C# !

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}