---
category: general
date: 2026-07-03
description: Comment conserver les graphiques tout en préservant le formatage des
  graphiques avec Aspose.Slides en C#. Suivez ce guide étape par étape.
draft: false
keywords:
- how to preserve charts
- preserve chart formatting
language: fr
og_description: Comment conserver les graphiques et le formatage des graphiques avec
  Aspose.Slides en C#. Guide complet avec code.
og_title: Comment préserver les graphiques – préserver le format des graphiques dans
  PowerPoint (C#)
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: how to preserve charts while keeping preserve chart formatting using
    Aspose.Slides in C#. Follow this step‑by‑step guide.
  headline: how to preserve charts – preserve chart formatting in PowerPoint C#
  type: TechArticle
- description: how to preserve charts while keeping preserve chart formatting using
    Aspose.Slides in C#. Follow this step‑by‑step guide.
  name: how to preserve charts – preserve chart formatting in PowerPoint C#
  steps:
  - name: Open `EditableCharts.pptx` in PowerPoint.
    text: Open `EditableCharts.pptx` in PowerPoint.
  - name: Click any chart → “Edit Data”.
    text: Click any chart → “Edit Data”.
  - name: The Excel‑like data sheet should appear, letting you modify series values.
    text: The Excel‑like data sheet should appear, letting you modify series values.
  type: HowTo
- questions:
  - answer: Directly no—`ExportEditableObjects` only applies to the PPTX format. Convert
      first, then export.
    question: Does this work with PowerPoint 2003 (PPT) files?
  - answer: Absolutely. The same `ExportEditableObjects` flag keeps SmartArt, tables,
      and diagrams editable.
    question: Can I preserve other objects like SmartArt?
  - answer: 'The slide size is stored in the presentation metadata and isn’t affected
      by these options. No extra code needed. --- ## Next steps – keep the momentum
      Now that you’ve nailed **how to preserve charts**, try exploring: - **preserve
      chart formatting** for specific chart types (e.g., stacked bar vs. rad'
    question: What if I need to keep the original slide size?
  type: FAQPage
tags:
- Aspose.Slides
- C#
- PowerPoint
- chart automation
title: Comment préserver les graphiques – préserver le formatage des graphiques dans
  PowerPoint C#
url: /fr/net/setting-chart-appearance/how-to-preserve-charts-preserve-chart-formatting-in-powerpoi/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# comment préserver les graphiques – conserver le format des graphiques dans PowerPoint C#

Vous êtes-vous déjà demandé **comment préserver les graphiques** lorsque vous devez exporter ou manipuler un fichier PowerPoint de façon programmatique ? Peut‑être avez‑vous effectué un enregistrement rapide et le graphique s’est transformé en image statique, rompant ainsi l’éditabilité dont vous comptiez.  

Dans ce tutoriel, nous allons vous montrer **comment préserver les graphiques** **et** garder leur **format de graphique préservé** intact en utilisant Aspose.Slides for .NET. À la fin, vous disposerez d’un extrait C# prêt à l’emploi qui produit un PPTX où chaque graphique reste un objet OOXML modifiable—plus d’images aplaties.

## Ce que vous allez apprendre

- Les étapes exactes pour charger une présentation, configurer les options d’exportation et enregistrer tout en **préservant le format des graphiques**.  
- Pourquoi le drapeau `ExportEditableObjects` est important et comment il empêche les graphiques d’être rasterisés.  
- Les pièges courants (par ex., anciens formats PPT, polices manquantes) et leurs solutions rapides.  

Aucune expérience préalable avec Aspose n’est requise ; il vous suffit d’une configuration C# de base et d’un fichier PowerPoint que vous souhaitez garder compatible avec les graphiques.

## Prérequis

- .NET 6.0 ou supérieur (le code fonctionne également avec .NET Framework 4.7+).  
- Package NuGet Aspose.Slides for .NET (`Install-Package Aspose.Slides.NET`).  
- Un fichier d’exemple `input.pptx` contenant au moins un graphique.  
- Visual Studio, Rider ou tout autre éditeur de votre choix.

---

## Étape 1 : Installer Aspose.Slides et créer un nouveau projet console

Pour commencer, créez une nouvelle application console et ajoutez la bibliothèque :

```bash
dotnet new console -n PreserveChartsDemo
cd PreserveChartsDemo
dotnet add package Aspose.Slides.NET
```

> **Astuce :** Si vous êtes derrière un proxy d’entreprise, ajoutez le drapeau `--no-restore` et restaurez plus tard avec vos paramètres de proxy.

## Étape 2 : Charger la présentation source – le premier endroit où appliquer **comment préserver les graphiques**

Ouvrez votre fichier PPTX à l’aide de la classe `Presentation`. C’est ici que le voyage vers **comment préserver les graphiques** commence réellement.

```csharp
using Aspose.Slides;
using Aspose.Slides.Export;

namespace PreserveChartsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 2: Load the source presentation
            // Replace the path with the location of your PPTX that contains charts.
            Presentation pres = new Presentation(@"YOUR_DIRECTORY\input.pptx");
```

Notez que nous n’avons pas encore touché aux objets graphiques—c’est intentionnel. Charger le fichier tel quel garantit que nous conservons la structure XML d’origine, ce qui est crucial pour **préserver le format des graphiques** plus tard.

## Étape 3 : Configurer les options d’exportation – le cœur de **comment préserver les graphiques**

Aspose.Slides propose une classe `PresentationExportOptions`. Mettre `ExportEditableObjects` à `true` indique au moteur de conserver les graphiques, tableaux et SmartArt sous forme de parties OOXML natives au lieu de les aplatir.

```csharp
            // Step 3: Configure export options to keep objects editable
            PresentationExportOptions exportOptions = new PresentationExportOptions
            {
                // This flag is the key to how to preserve charts.
                ExportEditableObjects = true
            };
```

Pourquoi cela fonctionne ? Lorsque `ExportEditableObjects` est `false` (valeur par défaut), la bibliothèque rasterise les objets complexes pour des raisons de compatibilité, ce qui détruit **le format de graphique préservé**. L’activer conserve le XML du graphique d’origine, permettant aux utilisateurs finaux d’ouvrir le PPTX et de modifier les données du graphique.

## Étape 4 : Enregistrer la présentation avec les options configurées

Nous écrivons maintenant le fichier de sortie. La surcharge `Save` qui accepte `SaveFormat` et `exportOptions` garantit que le graphique reste modifiable.

```csharp
            // Step 4: Save the presentation with the configured options
            pres.Save(@"YOUR_DIRECTORY\EditableCharts.pptx", SaveFormat.Pptx, exportOptions);

            // Optional: Inform the user
            Console.WriteLine("Presentation saved with editable charts at: YOUR_DIRECTORY\\EditableCharts.pptx");
        }
    }
}
```

L’exécution de ce programme produit `EditableCharts.pptx`. Ouvrez‑le dans PowerPoint, faites un clic droit sur un graphique, et vous verrez l’option habituelle « Edit Data »—la preuve que nous avons maîtrisé **comment préserver les graphiques** et **préserver le format des graphiques**.

## Étape 5 : Vérifier le résultat et dépanner les problèmes courants

### Vérifier

1. Ouvrez `EditableCharts.pptx` dans PowerPoint.  
2. Cliquez sur n’importe quel graphique → « Edit Data ».  
3. La feuille de données de type Excel doit apparaître, vous permettant de modifier les valeurs des séries.

Si vous ne voyez qu’une image statique, vérifiez :

- Vous utilisez une version récente d’Aspose.Slides (les anciennes versions comportaient des bugs avec `ExportEditableObjects`).  
- Le PPTX source contient réellement des objets graphiques (et non des images de graphiques).  
- Aucun thème personnalisé ou substitution de police ne force le rendu du graphique en image.

### Cas particuliers

- **Fichiers PPT (binaires) anciens :** Convertissez‑les d’abord en PPTX (`pres.Save("temp.pptx", SaveFormat.Pptx)`) avant d’appliquer les options d’exportation.  
- **Présentations volumineuses :** L’utilisation de la mémoire peut augmenter ; envisagez le pattern `Dispose` de `Presentation` ou les API de streaming pour les fichiers très gros.  
- **Polices incorporées :** Si l’environnement cible ne possède pas les polices d’origine, PowerPoint peut recourir à un rendu image du graphique. Incorporez les polices dans le fichier source ou livrez‑les avec votre application.

---

## Questions fréquentes (FAQ)

**Q : Cela fonctionne‑t‑il avec les fichiers PowerPoint 2003 (PPT) ?**  
R : Directement non—`ExportEditableObjects` ne s’applique qu’au format PPTX. Convertissez d’abord, puis exportez.

**Q : Puis‑je préserver d’autres objets comme SmartArt ?**  
R : Absolument. Le même drapeau `ExportEditableObjects` garde SmartArt, tableaux et diagrammes modifiables.

**Q : Et si je dois conserver la taille de diapositive d’origine ?**  
R : La taille de la diapositive est stockée dans les métadonnées de la présentation et n’est pas affectée par ces options. Aucun code supplémentaire n’est nécessaire.

---

## Prochaines étapes – garder l’élan

Maintenant que vous avez maîtrisé **comment préserver les graphiques**, explorez :

- **préserver le format des graphiques** pour des types spécifiques (par ex., barres empilées vs radar).  
- Utiliser l’API `Chart` pour modifier les données programmatique avant l’enregistrement.  
- Exporter vers d’autres formats (PDF, HTML) tout en gardant les graphiques modifiables dans le PPTX source.  

Chacune de ces pistes repose sur le même principe : conserver l’OOXML sous‑jacent intact.

---

## Conclusion

Nous avons parcouru **comment préserver les graphiques** dans un fichier PowerPoint en utilisant Aspose.Slides for .NET, et nous avons démontré les étapes exactes de **préserver le format des graphiques** nécessaires pour que ces graphiques restent entièrement éditables. Le fragment de code complet ci‑dessus est prêt à être intégré dans n’importe quel projet C#, et les explications couvrent le *pourquoi* de chaque ligne—vous ne vous contentez donc pas de copier‑coller, vous comprenez.

Testez‑le, ajustez les options d’exportation, et vous automatiserez bientôt les mises à jour de présentations sans jamais perdre la possibilité d’ajuster les données des graphiques. Bon codage !

## Que devez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Comment exporter des graphiques Excel au format PDF avec Aspose.Cells pour .NET&#58; guide étape par étape](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [Comment convertir des graphiques Excel en SVG avec Aspose.Cells pour .NET (guide étape par étape)](/cells/english/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)
- [Comment créer des graphiques dans Excel avec Aspose.Cells pour .NET&#58; guide du développeur](/cells/english/net/charts-graphs/create-charts-excel-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}