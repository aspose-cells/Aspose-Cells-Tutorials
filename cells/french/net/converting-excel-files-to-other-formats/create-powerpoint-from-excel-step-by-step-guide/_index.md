---
category: general
date: 2026-02-09
description: Créez PowerPoint à partir d’Excel en quelques minutes – apprenez comment
  convertir Excel en PowerPoint et exporter Excel vers PPT avec un exemple de code
  C# simple.
draft: false
keywords:
- create powerpoint from excel
- convert excel to powerpoint
- export excel to ppt
- generate ppt from excel
- how to convert excel to pptx
language: fr
og_description: Créez rapidement un PowerPoint à partir d’Excel. Ce guide montre comment
  convertir Excel en PowerPoint, exporter Excel vers PPT et générer un PPT à partir
  d’Excel en utilisant C#.
og_title: Créer PowerPoint à partir d'Excel – Guide complet de programmation
tags:
- C#
- Aspose.Cells
- PowerPoint automation
- Office interop
title: Créer un PowerPoint à partir d’Excel – Guide étape par étape
url: /fr/net/converting-excel-files-to-other-formats/create-powerpoint-from-excel-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer PowerPoint à partir d'Excel – Guide complet de programmation

Vous avez déjà eu besoin de **créer PowerPoint à partir d'Excel** mais vous ne saviez pas quelle API appeler ? Vous n'êtes pas seul. De nombreux développeurs se heurtent à un mur lorsqu'ils souhaitent transformer des feuilles de calcul en présentations sans copier‑coller manuellement.  

Bonne nouvelle : avec quelques lignes de C#, vous pouvez **convertir Excel en PowerPoint**, exporter les formes de la feuille, et obtenir un fichier PPTX prêt à être présenté. Dans ce tutoriel, nous parcourrons l’ensemble du processus, expliquerons pourquoi chaque étape est importante, et vous montrerons comment gérer les problèmes les plus courants.

## Ce que vous apprendrez

- Comment charger un classeur Excel contenant des graphiques, des images ou des SmartArt.
- L’appel exact qui **exporte Excel vers PPT** en utilisant la bibliothèque Aspose.Cells.
- Comment enregistrer la présentation générée et vérifier le résultat.
- Conseils pour gérer les classeurs sans formes, ajuster la taille des diapositives et résoudre les incompatibilités de version.

Pas d'outils externes, pas d'interop COM, juste du code .NET pur qui s'exécute partout où .NET Core ou .NET 5+ est pris en charge.

---

## Prérequis

Avant de commencer, assurez-vous d'avoir :

1. **Aspose.Cells for .NET** (la bibliothèque qui fournit `SaveToPresentation`). Vous pouvez l'obtenir depuis NuGet :  

   ```bash
   dotnet add package Aspose.Cells
   ```
2. Un SDK .NET récent (6.0 ou ultérieur est recommandé).  
3. Un fichier Excel (`shapes.xlsx`) contenant au moins une forme, un graphique ou une image que vous souhaitez voir apparaître sur une diapositive.

C’est tout — aucune installation d’Office, aucune contrainte de licence pour le but de cette démonstration (l’évaluation gratuite fonctionne très bien).

---

## Étape 1 : Charger le classeur Excel (Créer PowerPoint à partir d'Excel)

La première chose dont nous avons besoin est un objet `Workbook` qui pointe vers le fichier source. Cet objet représente l’ensemble du document Excel, y compris toutes les feuilles de calcul, les graphiques et les objets incorporés.

```csharp
using Aspose.Cells;
using Aspose.Slides;

// Step 1: Load the Excel workbook containing the shapes
Workbook workbook = new Workbook(@"C:\MyProjects\ExcelToPpt\shapes.xlsx");

// Why this matters:
// - `Workbook` abstracts the file format, so you don’t have to worry about .xls vs .xlsx.
// - Loading the file early lets you inspect its contents (e.g., count of worksheets) before conversion.
```

> **Astuce :** Si vous n'êtes pas sûr que le fichier existe, encapsulez le constructeur dans un `try/catch` et fournissez un message d’erreur utile. Cela vous évite une `FileNotFoundException` cryptique plus tard.

---

## Étape 2 : Convertir le classeur en présentation PowerPoint (Exporter Excel vers PPT)

Aspose.Cells est fourni avec un exportateur intégré qui transforme l’ensemble du classeur — ou seulement des feuilles sélectionnées — en une présentation PowerPoint. La méthode `SaveToPresentation` fait le travail lourd.

```csharp
// Step 2: Convert the workbook to a PowerPoint presentation (PPTX format)
Presentation presentation = workbook.SaveToPresentation(ExportTo.Pptx);

// How it works:
// - Each worksheet becomes a separate slide.
// - Shapes, charts, and images are rasterized and placed on the slide preserving their layout.
// - You can later tweak the `Presentation` object (e.g., add a title slide) before saving.
```

Si vous avez seulement besoin de **générer un ppt à partir d'Excel** pour un sous‑ensemble de feuilles, vous pouvez utiliser la surcharge qui accepte une collection `SheetOptions`. Pour la plupart des scénarios, la conversion par défaut suffit.

---

## Étape 3 : Enregistrer la présentation générée (Comment convertir Excel en PPTX)

Maintenant que nous disposons d’une instance `Presentation`, la persister sur le disque est simple. Le résultat sera un fichier `.pptx` standard que toute version moderne de PowerPoint peut ouvrir.

```csharp
// Step 3: Save the generated presentation to a file
presentation.Save(@"C:\MyProjects\ExcelToPpt\shapes.pptx");

// Verification:
// Open the file in PowerPoint or use Aspose.Slides to programmatically inspect slide count.
```

> **Et si le classeur n’a aucune forme ?**  
> L’exportateur créera quand même des diapositives, mais elles seront vides. Vous pouvez vérifier `workbook.Worksheets[i].Shapes.Count` avant la conversion et décider de sauter cette feuille.

---

## Optionnel : Affiner la sortie (Exportation avancée d’Excel vers PPT)

Parfois, la taille de diapositive par défaut (standard 4 : 3) n’est pas idéale pour les présentations grand écran. Vous pouvez ajuster les dimensions de la diapositive avant l’enregistrement :

```csharp
// Set slide size to widescreen (16:9)
presentation.SlideSize.SetSize(SlideSizeType.Widescreen, SlideSizeScaleType.DoNotScale);

// Add a custom title slide (optional)
ISlide titleSlide = presentation.Slides.InsertEmptySlide(0, presentation.LayoutSlides[0]);
titleSlide.Shapes.AddAutoShape(ShapeType.Rectangle, 50, 50, 600, 100)
          .TextFrame.Text = "Quarterly Report – Exported from Excel";
```

Ces ajustements démontrent **comment convertir Excel en PowerPoint** avec un rendu professionnel, et non pas simplement un vidage brut de données.

---

## Exemple complet fonctionnel (Toutes les étapes combinées)

Ci‑dessous se trouve le programme complet, prêt à être exécuté. Copiez‑collez‑le dans une application console, ajustez les chemins de fichiers, et appuyez sur **F5**.

```csharp
using System;
using Aspose.Cells;
using Aspose.Slides;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the workbook
            string excelPath = @"C:\MyProjects\ExcelToPpt\shapes.xlsx";
            Workbook workbook = new Workbook(excelPath);

            // 2️⃣ Convert to PPTX
            Presentation presentation = workbook.SaveToPresentation(ExportTo.Pptx);

            // Optional: set widescreen layout
            presentation.SlideSize.SetSize(SlideSizeType.Widescreen, SlideSizeScaleType.DoNotScale);

            // Optional: add a title slide
            ISlide titleSlide = presentation.Slides.InsertEmptySlide(0, presentation.LayoutSlides[0]);
            titleSlide.Shapes.AddAutoShape(ShapeType.Rectangle, 50, 50, 600, 100)
                      .TextFrame.Text = "Quarterly Report – Exported from Excel";

            // 3️⃣ Save the PPTX file
            string pptxPath = @"C:\MyProjects\ExcelToPpt\shapes.pptx";
            presentation.Save(pptxPath);

            Console.WriteLine($"✅ Successfully created PowerPoint from Excel! File saved at: {pptxPath}");
        }
    }
}
```

**Résultat attendu :** Ouvrez `shapes.pptx` dans PowerPoint. Vous verrez une diapositive par feuille de calcul, chacune conservant les graphiques, images et autres formes d’origine. La diapositive de titre optionnelle apparaît au tout début, offrant une introduction soignée au diaporama.

---

## Questions fréquentes & cas particuliers

| Question | Réponse |
|----------|--------|
| *Et si je n’ai besoin que d’une seule feuille ?* | Utilisez `Workbook.Worksheets[0]` et appelez `SaveToPresentation` sur cette feuille via `SheetOptions`. |
| *Puis-je conserver les formules Excel ?* | Non — les formules sont rendues comme des valeurs statiques dans la diapositive. Si vous avez besoin de données en direct, envisagez de lier le PPTX au fichier Excel ultérieurement. |
| *Cela fonctionne-t-il sous Linux/macOS ?* | Oui. Aspose.Cells est indépendant de la plateforme ; il suffit d’installer le runtime .NET et le tour est joué. |
| *Qu’en est‑il des classeurs protégés par mot de passe ?* | Chargez avec `LoadOptions` incluant le mot de passe avant d’appeler `SaveToPresentation`. |
| *Pourquoi obtiens‑je des diapositives vides ?* | Vérifiez que le classeur contient réellement des formes (`Shapes.Count > 0`). Des diapositives vides sont créées pour les feuilles vides. |

---

## Conclusion

Vous disposez maintenant d’une solution claire, de bout en bout, pour **créer PowerPoint à partir d'Excel** en utilisant C#. En chargeant le classeur, en invoquant `SaveToPresentation` et en enregistrant le résultat, vous pouvez **convertir Excel en PowerPoint**, **exporter Excel vers PPT**, et **générer un PPT à partir d'Excel** avec seulement quelques lignes de code.  

À partir d’ici, vous pourriez explorer :

- Ajouter des animations aux diapositives générées avec Aspose.Slides.  
- Automatiser l’ensemble du pipeline (par ex., lire les fichiers d’un dossier, les convertir par lots).  
- Intégrer le code dans une API ASP.NET Core afin que les utilisateurs puissent télécharger un fichier Excel et recevoir instantanément un PPTX.

Essayez-le, ajustez la taille des diapositives, ajoutez un titre personnalisé — il y a largement de la place pour personnaliser le résultat à votre goût. Vous avez des questions ou rencontrez un problème ? Laissez un commentaire ci‑dessous, et bon codage !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}