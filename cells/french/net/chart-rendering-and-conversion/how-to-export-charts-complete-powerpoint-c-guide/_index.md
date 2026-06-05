---
category: general
date: 2026-06-05
description: Comment exporter des graphiques depuis PowerPoint avec C#. Inclut l’exportation
  des objets OLE et rend les graphiques modifiables dans le PPTX résultant – étape
  par étape.
draft: false
keywords:
- how to export charts
- export ole objects
- how to export ole
- make charts editable
language: fr
og_description: Comment exporter des graphiques depuis PowerPoint avec C#. Apprenez
  à exporter les objets OLE et à rendre les graphiques modifiables dans le PPTX enregistré
  – étape par étape.
og_title: Comment exporter des graphiques – Guide complet PowerPoint C#
schemas:
- author: Aspose
  dateModified: '2026-06-05'
  description: How to export charts from PowerPoint using C#. Includes export OLE
    objects and make charts editable in the resulting PPTX – step‑by‑step.
  headline: How to Export Charts – Complete PowerPoint C# Guide
  type: TechArticle
- description: How to export charts from PowerPoint using C#. Includes export OLE
    objects and make charts editable in the resulting PPTX – step‑by‑step.
  name: How to Export Charts – Complete PowerPoint C# Guide
  steps:
  - name: Full Working Example
    text: Below is the complete, self‑contained program you can compile and run. It
      includes `using` statements, proper disposal, and comments that explain each
      line.
  - name: What if the source file has no charts?
    text: The code will still run; `ExportEditableCharts` simply has no effect because
      there’s nothing to convert. No error is thrown.
  - name: Can I export only specific charts?
    text: Yes. Instead of using the global `ExportEditableCharts` flag, you can iterate
      through `presentation.Slides` and set `Chart.IsEditable = true` on individual
      chart objects before saving. This gives you granular control.
  - name: Does enabling OLE export increase file size?
    text: A little. The binary OLE streams are stored verbatim, so the resulting PPTX
      can be a few kilobytes larger. In most business scenarios the trade‑off is worth
      it because you retain full editability.
  - name: Which PowerPoint versions can open the resulting file?
    text: Any version that supports the OOXML standard (PowerPoint 2007 and later).
      The editable chart feature relies on the native chart editor introduced in Office
      2007, so older binaries like `.ppt` won’t benefit.
  type: HowTo
tags:
- PowerPoint
- C#
- Aspose.Slides
- OLE
- Charts
title: Comment exporter des graphiques – Guide complet PowerPoint C#
url: /fr/net/chart-rendering-and-conversion/how-to-export-charts-complete-powerpoint-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment exporter des graphiques – Guide complet PowerPoint C#

Vous vous êtes déjà demandé **comment exporter des graphiques** d’une présentation PowerPoint sans perdre la possibilité de les modifier plus tard ? Vous n’êtes pas le seul. Dans de nombreux pipelines de reporting, les données du graphique vivent à l’intérieur du PPTX, et une fois le fichier remis, le destinataire doit souvent ajuster une valeur ou changer une étiquette. La bonne nouvelle, c’est qu’avec quelques lignes de C# vous pouvez préserver l’éditabilité, et même exporter les objets OLE intégrés en même temps.

Dans ce tutoriel, nous allons parcourir un exemple pratique, prêt à l’emploi, qui montre **comment exporter des graphiques**, comment **exporter des objets OLE**, et comment **rendre les graphiques éditables** dans le fichier de sortie. À la fin, vous disposerez d’un extrait réutilisable que vous pourrez intégrer à n’importe quel projet .NET utilisant la bibliothèque Aspose.Slides.

> **Astuce :** Si vous débutez avec Aspose.Slides, assurez‑vous d’avoir ajouté le package NuGet `Aspose.Slides.NET` à votre projet—sinon le code ne compilera pas.

## Ce dont vous avez besoin

| Exigence | Pourquoi c'est important |
|----------|---------------------------|
| .NET 6+ (ou .NET Framework 4.7+) | Les runtimes modernes offrent de meilleures performances et une gestion de paquets plus simple. |
| Aspose.Slides for .NET (dernière version) | Cette bibliothèque fournit les classes `Presentation` et `PptxSaveOptions` que nous utiliserons. |
| Un fichier PowerPoint d’exemple contenant au moins un graphique | La démo fonctionne avec n’importe quel `.pptx` contenant un graphique ; vous verrez l’éditabilité après l’export. |
| Un IDE (Visual Studio, Rider ou VS Code) | Pratique pour le débogage rapide et la visualisation du fichier généré. |

Aucun outil tiers supplémentaire n’est requis—tout est géré par l’API Aspose.

## Étape 1 – Charger la présentation source

Tout d’abord, nous devons charger le PPTX original en mémoire. Considérez cela comme l’ouverture d’un document Word avant de commencer à le modifier.

```csharp
using Aspose.Slides;

// Step 1: Load the source presentation
Presentation presentation = new Presentation(@"C:\MyProjects\input.pptx");
```

> **Pourquoi c’est important :** L’objet `Presentation` est le point d’entrée pour toutes les opérations suivantes. Il analyse le fichier, construit un modèle d’objets des diapositives, formes, graphiques et objets OLE, et garde tout dans un état mutable.

## Étape 2 – Créer les options d’enregistrement et activer les graphiques éditables

Par défaut, lorsque vous appelez `Save`, la bibliothèque aplatit les graphiques en images statiques. Pour les garder éditables, vous devez activer le drapeau `ExportEditableCharts`.

```csharp
// Step 2: Create PPTX save options and enable editable charts
PptxSaveOptions saveOptions = new PptxSaveOptions
{
    // This tells Aspose to keep chart data in a format PowerPoint can edit.
    ExportEditableCharts = true
};
```

> **Comment ça fonctionne :** Lorsque `ExportEditableCharts` est `true`, la bibliothèque écrit la définition XML du graphique (`chart.xml`) dans le PPTX au lieu de le rasteriser. PowerPoint lit alors ce XML et permet à l’utilisateur d’ouvrir l’éditeur de graphique.

## Étape 3 – Activer l’exportation des objets OLE intégrés

De nombreuses présentations intègrent des feuilles Excel, des diagrammes Visio ou même des fichiers PDF comme objets OLE. Si vous voulez que ceux‑ci survivent au aller‑retour, activez `ExportOLEObjects`.

```csharp
// Step 3: Enable export of embedded OLE objects
saveOptions.ExportOLEObjects = true;
```

> **Ce que signifie réellement « exporter des objets OLE » :** Le package OLE est stocké comme un blob binaire à l’intérieur du PPTX. Activer ce drapeau préserve le binaire original, permettant au destinataire de double‑cliquer sur l’objet et de l’ouvrir dans son application native (par ex., Excel). Sans cela, l’objet OLE serait supprimé, les liens seraient rompus et les données perdues.

## Étape 4 – Enregistrer la présentation avec les options configurées

Maintenant que les options sont prêtes, il suffit de dire à Aspose d’écrire le fichier.

```csharp
// Step 4: Save the presentation with the configured options
presentation.Save(@"C:\MyProjects\editable.pptx", saveOptions);
```

> **Résultat :** `editable.pptx` contient les mêmes diapositives que `input.pptx`, mais tout graphique peut être modifié directement dans PowerPoint, et tous les objets OLE intégrés restent intacts.

### Exemple complet fonctionnel

Voici le programme complet, autonome, que vous pouvez compiler et exécuter. Il inclut les instructions `using`, la bonne gestion des ressources, et des commentaires expliquant chaque ligne.

```csharp
using System;
using Aspose.Slides;

namespace ExportChartsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Path to the source PPTX
            string sourcePath = @"C:\MyProjects\input.pptx";
            // Path where the edited PPTX will be saved
            string destPath = @"C:\MyProjects\editable.pptx";

            // Load the presentation
            using (Presentation presentation = new Presentation(sourcePath))
            {
                // Configure save options
                PptxSaveOptions options = new PptxSaveOptions
                {
                    ExportEditableCharts = true,   // make charts editable
                    ExportOLEObjects = true        // export OLE objects such as embedded Excel sheets
                };

                // Save the new file
                presentation.Save(destPath, options);
            }

            Console.WriteLine("Presentation saved with editable charts and OLE objects.");
        }
    }
}
```

**Sortie attendue :** Après l’exécution du programme, ouvrez `editable.pptx` dans PowerPoint. Faites un clic droit sur n’importe quel graphique → *Edit Data* → l’éditeur de graphique s’ouvre, confirmant que **rendre les graphiques éditables** a réussi. Double‑cliquez sur une feuille Excel intégrée, et elle s’ouvre dans Excel, prouvant que **l’exportation des objets OLE** a fonctionné.

![diagramme d'exportation de graphiques](https://example.com/images/export-charts.png "exportation de graphiques – PowerPoint après exportation")

*(Texte alternatif : exportation de graphiques – capture d'écran de PowerPoint avec graphique éditable et objet OLE)*

## Questions fréquentes & cas particuliers

### Et si le fichier source ne contient aucun graphique ?

Le code s’exécutera quand même ; `ExportEditableCharts` n’a simplement aucun effet parce qu’il n’y a rien à convertir. Aucune erreur n’est levée.

### Puis‑je n’exporter que des graphiques spécifiques ?

Oui. Au lieu d’utiliser le drapeau global `ExportEditableCharts`, vous pouvez parcourir `presentation.Slides` et définir `Chart.IsEditable = true` sur les graphiques individuels avant l’enregistrement. Cela vous donne un contrôle granulaire.

```csharp
foreach (ISlide slide in presentation.Slides)
{
    foreach (IChart chart in slide.Shapes.OfType<IChart>())
    {
        chart.IsEditable = true; // enable editability only for this chart
    }
}
```

### L’activation de l’export OLE augmente‑t‑elle la taille du fichier ?

Un peu. Les flux OLE binaires sont stockés tels quels, donc le PPTX résultant peut être quelques kilo‑octets plus gros. Dans la plupart des scénarios métier, le compromis vaut la peine car vous conservez une pleine éditabilité.

### Quelles versions de PowerPoint peuvent ouvrir le fichier résultant ?

Toute version prenant en charge la norme OOXML (PowerPoint 2007 et ultérieur). La fonctionnalité de graphique éditable repose sur l’éditeur natif introduit dans Office 2007, donc les anciens formats comme `.ppt` n’en bénéficieront pas.

## Astuces pour un code prêt pour la production

| Astuce | Raison |
|--------|--------|
| Utilisez des blocs `using` (comme montré) pour libérer les objets `Presentation`. | Évite les fuites de mémoire, surtout lors du traitement de nombreux fichiers en lot. |
| Validez les chemins de fichiers avant le chargement. | Évite `FileNotFoundException` qui ferait planter un service en arrière‑plan. |
| Enregistrez les paramètres `ExportEditableCharts` et `ExportOLEObjects`. | Utile pour le dépannage lorsqu’un utilisateur signale des graphiques non éditables. |
| Capturez séparément `Aspose.Slides.Exception`. | Fournit des messages d’erreur plus clairs provenant de la bibliothèque (ex. : types de graphiques non pris en charge). |
| Envisagez `PptxCompressionLevel` si la taille du fichier est critique. | Vous pouvez compresser la sortie tout en conservant l’éditabilité. |

## Récapitulatif – Ce que nous avons accompli

Nous avons commencé avec une question claire : **comment exporter des graphiques** d’un fichier PowerPoint tout en les gardant éditables et en préservant les objets OLE intégrés. En chargeant la présentation, en configurant `PptxSaveOptions` (`ExportEditableCharts = true` et `ExportOLEObjects = true`), puis en enregistrant le fichier, nous disposons maintenant d’un PPTX qui satisfait les deux exigences. Le même schéma peut être réutilisé pour des conversions par lots, des pipelines CI, ou tout outil de reporting automatisé.

## Que explorer ensuite ?

- **Exporter les graphiques en images** pour des rapports statiques (`saveOptions.ExportEditableCharts = false`).  
- **Convertir le PPTX en PDF** tout en conservant les graphiques vectoriels (`PdfSaveOptions`).  
- **Manipuler les données de graphique programmatique** (par ex., mettre à jour les valeurs de séries avant l’export).  
- **Intégrer avec Azure Functions** pour fournir une API d’exportation de graphiques à la demande.

N’hésitez pas à expérimenter, et faites‑nous part des cas particuliers que vous rencontrez. Bon codage, et que tous vos graphiques restent éditables !

## Que devez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Comment exporter des graphiques Excel en PDF avec Aspose.Cells pour .NET : Guide étape par étape](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [Comment convertir des graphiques Excel en SVG avec Aspose.Cells pour .NET (Guide étape par étape)](/cells/english/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)
- [Comment appliquer des thèmes aux graphiques Excel avec Aspose.Cells .NET : Guide étape par étape](/cells/english/net/charts-graphs/apply-themes-charts-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}