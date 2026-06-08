---
category: general
date: 2026-06-08
description: Créez un classeur Excel en C# étape par étape et apprenez à utiliser
  la fonction EXPAND dans Excel pour des plages dynamiques. Parfait pour les développeurs .NET.
draft: false
keywords:
- create excel workbook c#
- use expand function in excel
language: fr
og_description: Créer un classeur Excel en C# avec un exemple clair et découvrir comment
  utiliser la fonction EXPAND dans Excel pour générer des tableaux dynamiques.
og_title: Créer un classeur Excel en C# – Guide complet de programmation
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Create Excel workbook C# step‑by‑step and learn how to use expand function
    in Excel for dynamic ranges. Perfect for .NET developers.
  headline: Create Excel Workbook C# – Full Guide with Expand Function
  type: TechArticle
- description: Create Excel workbook C# step‑by‑step and learn how to use expand function
    in Excel for dynamic ranges. Perfect for .NET developers.
  name: Create Excel Workbook C# – Full Guide with Expand Function
  steps:
  - name: '`SEQUENCE(3)` produces a vertical array `{1;2;3}`.'
    text: '`SEQUENCE(3)` produces a vertical array `{1;2;3}`.'
  - name: '`EXPAND(...,5,5)` tells Excel to grow that array to 5 rows and 5 columns.'
    text: '`EXPAND(...,5,5)` tells Excel to grow that array to 5 rows and 5 columns.'
  - name: The result is a 5 × 5 grid where the first three rows contain the numbers
      1‑3 repeated across columns, and the remaining two rows are blank.
    text: The result is a 5 × 5 grid where the first three rows contain the numbers
      1‑3 repeated across columns, and the remaining two rows are blank.
  - name: '**Creates an Excel workbook C#** using Aspose.Cells.'
    text: '**Creates an Excel workbook C#** using Aspose.Cells.'
  - name: '**Uses the EXPAND function in Excel** to turn a 3‑row array into a 5 × 5
      block.'
    text: '**Uses the EXPAND function in Excel** to turn a 3‑row array into a 5 × 5
      block.'
  - name: Adds a cotangent formula (`COT(PI()/4)`).
    text: Adds a cotangent formula (`COT(PI()/4)`).
  - name: Saves the file and optionally auto‑fits columns.
    text: Saves the file and optionally auto‑fits columns.
  type: HowTo
- questions:
  - answer: Absolutely. Aspose.Cells targets .NET Standard 2.0, which is compatible
      with both .NET Core and the classic Framework.
    question: Does this work with .NET Framework 4.8?
  - answer: Use `ws.Protect(ProtectionType.All, "yourPassword");` before saving.
    question: What if I need to protect the sheet?
  - answer: 'Yes—`workbook.Save(stream, SaveFormat.Xlsx);` is handy for web APIs that
      return the file as a download. --- ## TL;DR We built a **complete C# console
      app** that: 1. **Creates an Excel workbook C#** using Aspose.Cells. 2. **Uses
      the EXPAND function in Excel** to turn a 3‑row array into a 5 × 5 block.'
    question: Can I write the workbook directly to a `MemoryStream`?
  type: FAQPage
tags:
- csharp
- excel
- aspose-cells
- .net
title: Créer un classeur Excel en C# – Guide complet avec fonction d'extension
url: /fr/net/excel-workbook/create-excel-workbook-c-full-guide-with-expand-function/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un classeur Excel C# – Guide complet avec la fonction Expand

Vous vous êtes déjà demandé comment **créer un classeur Excel C#** sans vous battre avec l’interop COM ou bricoler du XML ? Vous n’êtes pas le seul. Dans de nombreux projets .NET, nous devons générer une feuille de calcul, la remplir de formules et la remettre à des utilisateurs non techniques. La bonne nouvelle ? Avec une bibliothèque moderne comme **Aspose.Cells**, tout le processus est un jeu d’enfant.

Dans ce tutoriel, nous allons parcourir un exemple complet et exécutable qui **crée un classeur Excel C#**, ajoute quelques formules—y compris comment **utiliser la fonction expand dans Excel**—et enregistre le fichier afin que vous puissiez l’ouvrir immédiatement dans Excel. À la fin, vous saurez non seulement *quoi* taper, mais aussi *pourquoi* chaque ligne est importante, et vous disposerez d’un modèle que vous pourrez copier dans n’importe quel projet.

## Prérequis

Avant de commencer, assurez‑vous d’avoir :

- .NET 6 SDK (ou toute version .NET récente) installé.
- Un IDE compatible NuGet (Visual Studio, VS Code, Rider, etc.).
- Le package NuGet **Aspose.Cells** – il fournit les classes `Workbook` et `Worksheet` utilisées dans le code.
- Une connaissance de base du C# ; aucune expérience spécifique à Excel n’est requise.

Vous avez tout cela ? Super—commençons.

## Étape 1 : Configurer le projet et ajouter Aspose.Cells

Tout d’abord, créez une application console et importez la bibliothèque.

```bash
dotnet new console -n ExcelDemo
cd ExcelDemo
dotnet add package Aspose.Cells
```

> **Astuce :** Si vous êtes sur un réseau d’entreprise, il se peut que vous deviez configurer un proxy NuGet. Le package Aspose.Cells est léger, donc l’installation se termine en quelques secondes.

Ouvrez maintenant `Program.cs`. Vous verrez la méthode `Main` par défaut—remplacez‑la par le squelette ci‑dessous.

```csharp
using System;
using Aspose.Cells;

namespace ExcelDemo
{
    class Program
    {
        static void Main()
        {
            // All of our Excel logic will go here.
        }
    }
}
```

La ligne `using Aspose.Cells;` fait entrer les classes de feuille de calcul dans le scope. Si vous l’oubliez, le compilateur se plaindra que `Workbook` est indéfini—ce que nous éviterons plus tard.

## Étape 2 : Créer un classeur Excel C# et accéder à la première feuille de calcul

Avec le projet prêt, nous pouvons enfin **créer un classeur Excel C#**. Le constructeur `Workbook` nous donne un classeur vierge, et l’index `Worksheets[0]` renvoie la feuille par défaut (nommée « Sheet1 »).

```csharp
// Step 2: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();               // creates an empty .xlsx file in memory
Worksheet ws = workbook.Worksheets[0];            // reference to the first (default) sheet
```

Pourquoi récupérons‑nous explicitement la première feuille ? Parce que de nombreuses API en aval (comme la définition de formules) nécessitent un objet `Worksheet`, pas seulement le `Workbook`. Cela rend également le code plus clair pour quiconque le lira plus tard.

## Étape 3 : Utiliser la fonction Expand dans Excel pour remplir une plage dynamique

Voici la star du spectacle : **utiliser la fonction expand dans Excel**. La fonction `EXPAND` (disponible à partir d’Excel 365) prend un tableau source et le remplit jusqu’à la taille souhaitée. Dans notre exemple, nous partons d’un tableau vertical de 3 lignes généré par `SEQUENCE(3)` et nous l’étendons en un bloc de 5 × 5.

```csharp
// Step 3: Insert the EXPAND formula into cell A1
ws.Cells["A1"].Formula = "EXPAND(SEQUENCE(3),5,5)";
```

Que se passe‑t‑il réellement ?

1. `SEQUENCE(3)` produit un tableau vertical `{1;2;3}`.
2. `EXPAND(...,5,5)` indique à Excel d’agrandir ce tableau à 5 lignes et 5 colonnes.
3. Le résultat est une grille 5 × 5 où les trois premières lignes contiennent les nombres 1‑3 répétés sur les colonnes, et les deux dernières lignes sont vides.

Comme nous écrivons la formule sous forme de chaîne, Excel l’évalue *lors de l’ouverture du fichier*, pas à l’exécution. Cela signifie que le classeur reste léger, et toute modification du tableau source se répercutera automatiquement.

> **Cas limite :** Si un utilisateur ouvre le classeur avec une version plus ancienne d’Excel qui ne prend pas en charge `EXPAND`, la cellule affichera `#NAME?`. Pour se prémunir, vous pourriez entourer la formule avec `IFERROR`, mais dans les environnements modernes il est sûr de compter sur la fonction.

## Étape 4 : Ajouter une formule de cotangente pour la bonne mesure

Ajoutons une autre formule pour montrer à quel point il est simple d’insérer des expressions mathématiques. Nous calculerons la cotangente de π/4, qui vaut exactement `1`.

```csharp
// Step 4: Insert a cotangent calculation in cell B1
ws.Cells["B1"].Formula = "COT(PI()/4)";
```

La fonction `COT` d’Excel n’est pas aussi courante que `SIN` ou `COS`, mais elle est parfaite pour les flux de travail trigonométriques. Lorsque vous ouvrirez le classeur, la cellule **B1** affichera `1`.

## Étape 5 : Enregistrer le classeur et vérifier le résultat

Tout ce travail serait inutile si nous n’enregistrions pas le fichier. La méthode `Save` écrit le classeur en mémoire sur le disque. Choisissez un dossier où vous avez les droits d’écriture et donnez‑lui un nom convivial.

```csharp
// Step 5: Save the workbook to the output folder
string outputPath = @"./output.xlsx";
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

Exécutez le programme :

```bash
dotnet run
```

Vous devriez voir le message console confirmant l’enregistrement. Ouvrez `output.xlsx` dans Excel, et vous remarquerez :

- Les cellules **A1:E5** remplies avec la séquence étendue (1, 2, 3 sur les trois premières lignes, cellules vides sur les lignes 4‑5).
- La cellule **B1** affichant la valeur `1` provenant de la formule de cotangente.

C’est le cycle complet : **créer un classeur excel c#**, intégrer des formules, et produire une feuille de calcul exploitable.

![Screenshot of the generated Excel workbook showing the expanded array and cotangent result](/images/create-excel-workbook-csharp.png "create excel workbook c# example")
*Texte alternatif de l'image : capture d'écran du classeur Excel généré montrant le tableau étendu et le résultat de la cotangente.*

## Étape 6 : Optionnel – Ajuster automatiquement la largeur des colonnes pour un rendu soigné

Si vous prévoyez de distribuer le fichier aux utilisateurs finaux, un ajustement rapide donne un aspect professionnel.

```csharp
// Optional: Auto‑fit all columns in the used range
ws.AutoFitColumns(0, ws.Cells.MaxColumn);
```

Cette ligne parcourt chaque colonne contenant des données et ajuste sa largeur à l’entrée la plus longue. C’est un petit détail, mais cela évite le débordement « …### » lorsque les nombres sont plus larges que la largeur de colonne par défaut.

## Étape 7 : Conclusion et prochaines étapes

Félicitations—vous venez de maîtriser comment **créer un classeur excel c#** à partir de zéro et avez appris à **utiliser la fonction expand dans excel** pour générer des tableaux dynamiques. Le code est volontairement minimal afin que vous puissiez le copier‑coller dans n’importe quel projet, mais les concepts s’étendent :

- **Sources de données dynamiques :** Remplacez `SEQUENCE(3)` par une référence à une autre plage ou à un tableau nommé.
- **Mise en forme conditionnelle :** Utilisez `ws.Cells["A1:E5"].Style` pour ajouter des couleurs selon les valeurs.
- **Graphiques et images :** Aspose.Cells peut intégrer des graphiques, des images, voire des tableaux croisés dynamiques.

N’hésitez pas à expérimenter—modifiez les dimensions de `EXPAND`, essayez `FILTER` ou `SORT`, ou enchaînez plusieurs formules. La bibliothèque gère tout cela sans que vous ayez à toucher le format OpenXML de bas niveau.

---

### Questions fréquentes

**Q : Cette solution fonctionne‑t‑elle avec .NET Framework 4.8 ?**  
R : Absolument. Aspose.Cells cible .NET Standard 2.0, qui est compatible à la fois avec .NET Core et le Framework classique.

**Q : Et si je dois protéger la feuille ?**  
R : Utilisez `ws.Protect(ProtectionType.All, "yourPassword");` avant d’enregistrer.

**Q : Puis‑je écrire le classeur directement dans un `MemoryStream` ?**  
R : Oui—`workbook.Save(stream, SaveFormat.Xlsx);` est pratique pour les API web qui renvoient le fichier en téléchargement.

---

## TL;DR

Nous avons construit une **application console C# complète** qui :

1. **Crée un classeur Excel C#** en utilisant Aspose.Cells.  
2. **Utilise la fonction EXPAND dans Excel** pour transformer un tableau de 3 lignes en un bloc 5 × 5.  
3. Ajoute une formule de cotangente (`COT(PI()/4)`).  
4. Enregistre le fichier et ajuste éventuellement les colonnes.

Vous disposez maintenant d’une base solide pour toute tâche d’automatisation impliquant la génération de fichiers Excel depuis .NET. Bon codage, et que vos feuilles de calcul restent toujours sans erreur !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Comment créer des plages nommées au niveau du classeur dans Excel avec Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)
- [Comment créer et utiliser des plages d'union dans Excel avec Aspose.Cells .NET (Guide C#)](/cells/english/net/range-management/excel-union-range-aspose-cells-net/)
- [Créer un classeur Excel avec des graphiques en utilisant Aspose.Cells .NET | Guide étape par étape](/cells/english/net/charts-graphs/create-excel-workbook-charts-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}