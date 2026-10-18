---
category: general
date: 2026-05-23
description: Créer un classeur Excel en C# et apprendre à appliquer un format numérique
  personnalisé, définir le style des cellules par programme, formater les cellules
  en notation scientifique, puis enregistrer le classeur au format xlsx.
draft: false
keywords:
- create excel workbook
- apply custom number format
- format cell scientific notation
- set cell style programmatically
- save workbook to xlsx
language: fr
og_description: Créez rapidement un classeur Excel en C#. Apprenez à appliquer un
  format de nombre personnalisé, à styliser les cellules par programmation, à formater
  la notation scientifique et à enregistrer au format xlsx.
og_title: Créer un classeur Excel en C# – Appliquer un format de nombre personnalisé
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: Create excel workbook in C# and learn how to apply custom number format,
    set cell style programmatically, format cell scientific notation, then save workbook
    to xlsx.
  headline: Create Excel Workbook in C# – Apply Custom Number Format
  type: TechArticle
tags:
- C#
- Excel
- Aspose.Cells
- Automation
title: Créer un classeur Excel en C# – Appliquer un format de nombre personnalisé
url: /fr/net/excel-custom-number-date-formatting/create-excel-workbook-in-c-apply-custom-number-format/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un classeur Excel en C# – Appliquer un format numérique personnalisé

Créer un classeur Excel en C# est plus simple que vous ne le pensez. Dans ce guide, nous vous expliquerons comment appliquer un format numérique personnalisé, formater une cellule en notation scientifique, définir le style de la cellule par programme, puis enregistrer le classeur dans un fichier .xlsx.

Si vous avez déjà regardé une feuille de calcul vierge en vous demandant comment automatiser le tout – de la saisie des données à la mise en forme exacte des nombres – ce tutoriel est pour vous. À la fin, vous disposerez d’un fichier Excel pleinement fonctionnel que vous pourrez ouvrir avec n’importe quel programme de tableur, et vous comprendrez **pourquoi** chaque étape est importante, pas seulement **comment** écrire le code.

## Ce dont vous avez besoin

- **.NET 6+** (ou tout framework .NET récent qui supporte la bibliothèque)  
- **Aspose.Cells for .NET** (ou une autre API exposant les classes `Workbook`, `Cell` et `CellFormat`)  
- Un peu d’expérience en C# – si vous savez écrire un `Console.WriteLine`, vous êtes prêt.  

Pas de fichiers de configuration supplémentaires, pas d’interop COM, et certainement aucune installation manuelle d’Excel requise.

---

## Créer un classeur Excel – Initialiser l’objet Workbook

La première chose à faire est de créer un classeur vide. Considérez la classe `Workbook` comme la toile vierge sur laquelle vous peindrez lignes, colonnes et styles.

```csharp
using Aspose.Cells;   // Make sure the Aspose.Cells namespace is referenced

// Step 1: Create a new workbook instance
Workbook workbook = new Workbook();
```

C’est tout – une ligne et vous avez un tout nouveau fichier Excel en mémoire. Le constructeur `Workbook` crée la collection de feuilles de calcul par défaut, vous pouvez donc commencer à ajouter des données immédiatement.

> **Astuce :** Si vous avez besoin de plusieurs feuilles, vous pouvez appeler `workbook.Worksheets.Add()` avant de commencer à remplir les cellules.

![Exemple de création de classeur Excel](image-placeholder.png "Capture d’écran de création de classeur Excel")

*Texte alternatif de l’image : exemple de création de classeur Excel montrant une feuille Excel vierge dans l’IDE.*

## Appliquer un format numérique personnalisé à une cellule

Maintenant que le classeur existe, insérons un nombre dans la cellule **A1** et appliquons‑lui un format personnalisé. Les formats numériques personnalisés vous permettent de contrôler l’apparence des nombres – monnaie, pourcentages, dates ou, dans notre cas, notation scientifique.

```csharp
// Step 2: Grab the first worksheet and the cell at A1 (row 0, column 0)
Worksheet sheet = workbook.Worksheets[0];
Cell cell = sheet.Cells[0, 0];

// Step 3: Insert a numeric value
cell.PutValue(12345.6789);

// Step 4: Retrieve the current style so we can modify its Number format
Style style = cell.GetStyle();

// Step 5: Define a custom scientific notation format with two decimal places
style.Custom = "0.00E+00";   // This is the “apply custom number format” part

// Step 6: Push the modified style back onto the cell
cell.SetStyle(style);
```

Pourquoi récupérer le style d’abord ? Parce que l’objet `Cell` stocke un objet **Style** qui regroupe polices, bordures, alignement et format numérique en un seul endroit. En modifiant la propriété `Custom`, nous indiquons à Excel « affichez cette valeur en notation scientifique avec deux décimales ».

> **Question fréquente :** *Puis‑je utiliser un format intégré au lieu d’un format personnalisé ?*  
> Oui – définissez `style.Number = 10` pour un format scientifique intégré, mais la chaîne personnalisée vous donne un contrôle précis sur le nombre de décimales.

## Définir le style de la cellule par programme (au‑delà du format numérique)

Souvent, vous voudrez plus qu’un simple format numérique. Ajoutons une police en gras et un fond gris clair pour faire ressortir la cellule.

```csharp
// Optional: Enhance the cell appearance
style.Font.IsBold = true;
style.ForegroundColor = System.Drawing.Color.LightGray;
style.Pattern = BackgroundType.Solid;

// Re‑apply the enriched style
cell.SetStyle(style);
```

Remarquez que nous réutilisons le même objet `style` que nous avons ajusté précédemment. C’est la beauté de **définir le style de la cellule par programme** : vous ne récupérez le style qu’une fois, modifiez les propriétés dont vous avez besoin, puis le réappliquez. Pas besoin de recréer des objets ou de perdre le format numérique déjà défini.

## Formater la cellule en notation scientifique (gestion des cas limites)

Si vous travaillez avec des nombres très grands ou très petits, la notation scientifique est un vrai sauveur. Le format personnalisé que nous avons utilisé (`0.00E+00`) garantit deux chiffres après le point décimal et impose un signe plus pour l’exposant. Voici une petite vérification de bon sens :

```csharp
// Verify the format by inserting another extreme value
Cell extraCell = sheet.Cells[1, 0]; // B2
extraCell.PutValue(0.00001234);
extraCell.SetStyle(style); // Reuse the same style with scientific notation
```

Lorsque vous ouvrez le fichier résultant, B2 apparaîtra sous la forme `1.23E-05`, confirmant que la directive **format cell scientific notation** fonctionne aussi bien pour les grands que pour les petits nombres.

## Enregistrer le classeur au format XLSX

Tout le plaisir s’arrête lorsque vous écrivez réellement le fichier sur le disque. La méthode `Save` effectue le travail lourd, convertissant la représentation en mémoire en un vrai package `.xlsx`.

```csharp
// Step 7: Persist the workbook
string outputPath = @"C:\Temp\CustomFormatted.xlsx";
workbook.Save(outputPath, SaveFormat.Xlsx);
```

Cette ligne réalise l’objectif **save workbook to xlsx**. Si le répertoire n’existe pas, `Save` lèvera une exception – assurez‑vous donc que le dossier est créé au préalable ou encapsulez l’appel dans un bloc try/catch.

```csharp
try
{
    workbook.Save(outputPath, SaveFormat.Xlsx);
    Console.WriteLine($"Workbook saved successfully to {outputPath}");
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Failed to save workbook: {ex.Message}");
}
```

Vous avez maintenant un fichier Excel prêt à être partagé, avec un nombre scientifique joliment formaté, du texte en gras et un fond gris clair.

## Exemple complet fonctionnel

Voici le programme complet, prêt à copier‑coller, qui assemble toutes les pièces. Il se compile comme une application console, mais vous pouvez intégrer la logique dans n’importe quel projet C#.

```csharp
using System;
using Aspose.Cells;
using System.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook
        Workbook workbook = new Workbook();

        // 2️⃣ Access the first worksheet and target cell A1
        Worksheet sheet = workbook.Worksheets[0];
        Cell cell = sheet.Cells[0, 0];

        // 3️⃣ Insert a numeric value
        cell.PutValue(12345.6789);

        // 4️⃣ Retrieve and customize the cell style
        Style style = cell.GetStyle();
        style.Custom = "0.00E+00";               // apply custom number format (scientific)
        style.Font.IsBold = true;               // set cell style programmatically
        style.ForegroundColor = Color.LightGray;
        style.Pattern = BackgroundType.Solid;

        // 5️⃣ Apply the style back to the cell
        cell.SetStyle(style);

        // 6️⃣ Add another example to prove scientific notation works for tiny numbers
        Cell tinyCell = sheet.Cells[1, 0]; // B2
        tinyCell.PutValue(0.00001234);
        tinyCell.SetStyle(style);

        // 7️⃣ Save the workbook to an XLSX file
        string outputPath = @"C:\Temp\CustomFormatted.xlsx";
        try
        {
            workbook.Save(outputPath, SaveFormat.Xlsx);
            Console.WriteLine($"Workbook saved successfully to {outputPath}");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Failed to save workbook: {ex.Message}");
        }
    }
}
```

**Résultat attendu :** Ouvrez `CustomFormatted.xlsx` et vous verrez :

| A1               | B2            |
|------------------|---------------|
| 1.23E+04         | 1.23E-05      |

Les deux cellules sont en gras, ont un remplissage gris clair et affichent les nombres en notation scientifique avec deux décimales.

---

## Conclusion

Nous venons de **create excel workbook** à partir de zéro, **apply custom number format**, **format cell scientific notation**, **set cell style programmatically**, et **save workbook to xlsx** – le tout en quelques lignes de C#. L’approche est évolutive : il suffit de boucler sur les lignes, de cloner l’objet `style`, et vous obtiendrez un rapport entièrement stylisé en quelques secondes.

### Et après ?

- **Mise en forme dynamique :** changer le format selon la magnitude de la valeur (par ex., monnaie vs. pourcentage).  
- **Feuilles multiples :** utilisez `workbook.Worksheets.Add("Summary")` pour créer des tableaux de bord.  
- **Styling avancé :** bordures, mise en forme conditionnelle et validation des données


## Tutoriels associés

- [Comment créer et enregistrer un classeur Excel au format ODS avec Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [Créer et enregistrer un classeur Excel avec Aspose Cells Dotnet](/cells/hongkong/net/workbook-operations/create-save-excel-workbook-aspose-cells-dotnet/)
- [Créer et enregistrer un classeur Excel en PDF avec Aspnet Aspose Cells](/cells/hongkong/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}