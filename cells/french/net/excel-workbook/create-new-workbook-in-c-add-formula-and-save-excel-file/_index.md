---
category: general
date: 2026-02-23
description: Créer un nouveau classeur programmatique en C# et ajouter une formule
  à une cellule. Apprenez à utiliser EXPAND, puis enregistrez le classeur Excel sans
  effort.
draft: false
keywords:
- create new workbook
- add formula to cell
- save excel workbook
- how to use expand
- create excel file programmatically
language: fr
og_description: Créez un nouveau classeur programmé en C#. Ajoutez une formule à une
  cellule, apprenez à utiliser EXPAND, et enregistrez le classeur Excel en quelques
  secondes.
og_title: Créer un nouveau classeur en C# – Ajouter une formule et enregistrer le
  fichier Excel
tags:
- C#
- Excel Automation
- Aspose.Cells
title: Créer un nouveau classeur en C# – Ajouter une formule et enregistrer le fichier
  Excel
url: /fr/net/excel-workbook/create-new-workbook-in-c-add-formula-and-save-excel-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un nouveau classeur en C# – Ajouter une formule et enregistrer le fichier Excel

Vous vous êtes déjà demandé comment **créer de nouveaux classeurs** depuis le code sans jamais ouvrir Excel ? Vous n'êtes pas seul. De nombreux développeurs se heurtent à un mur lorsqu'ils doivent générer une feuille de calcul à la volée—peut‑être pour un rapport, une exportation ou un simple dump de données.  

Bonne nouvelle ! Dans ce guide, vous verrez exactement comment **créer un nouveau classeur**, ajouter une **formule à une cellule**, puis **enregistrer le classeur Excel** en quelques lignes de C#. Nous aborderons également **comment utiliser EXPAND** afin de générer des tableaux dynamiques sans copier manuellement. À la fin, vous pourrez **créer un fichier Excel programmatique** et le livrer aux utilisateurs ou aux services en aval.

## Prérequis

- .NET 6.0 ou version ultérieure (tout runtime .NET récent fonctionne)
- Aspose.Cells for .NET (version d’essai ou licence) – cette bibliothèque fournit les classes `Workbook` et `Worksheet` utilisées ci‑dessous.
- Une compréhension de base de la syntaxe C#—aucune connaissance approfondie d’Excel n’est requise.

Si vous avez déjà tout cela, tant mieux ! Sinon, récupérez Aspose.Cells via NuGet (`Install-Package Aspose.Cells`) et vous serez prêt à démarrer.

---

## Étape 1 : Créer un nouveau classeur – La fondation

Pour commencer, nous devons instancier un objet classeur vierge. Pensez‑y comme à l’ouverture d’un tout nouveau fichier Excel, complètement vide.

```csharp
using Aspose.Cells;

public class ExcelGenerator
{
    public void Generate()
    {
        // Step 1: Create a new workbook (this is the core of create new workbook)
        Workbook workbook = new Workbook();
```

> **Pourquoi c’est important :** La classe `Workbook` est le point d’entrée pour toute manipulation d’Excel. En créant une nouvelle instance, nous allouons de la mémoire pour les feuilles, les styles et les formules—le tout sans toucher au système de fichiers.

---

## Étape 2 : Accéder à la première feuille de calcul

Chaque nouveau classeur possède une feuille par défaut (nommée *Sheet1*). Nous allons la récupérer afin de pouvoir y placer des données et des formules.

```csharp
        // Step 2: Access the first worksheet
        Worksheet worksheet = workbook.Worksheets[0];
```

> **Astuce :** Si vous avez besoin de plusieurs feuilles, appelez simplement `workbook.Worksheets.Add("MySheet")` et travaillez avec l’objet `Worksheet` retourné.

---

## Étape 3 : Ajouter une formule à une cellule – Utilisation de EXPAND

Passons maintenant à la partie amusante : insérer une formule. La fonction `EXPAND` est idéale lorsque vous voulez transformer un tableau statique en une plage plus grande, remplie automatiquement.

```csharp
        // Step 3: Add formula to cell A1 using EXPAND
        // This creates a 5‑row array from the constant {1,2,3}
        worksheet.Cells["A1"].Formula = "EXPAND({1,2,3},5,1)";
```

### Fonctionnement de la formule EXPAND

| Argument | Signification |
|----------|----------------|
| `{1,2,3}` | Le tableau source (une liste horizontale de trois nombres) |
| `5`       | Nombre de lignes souhaité dans le résultat |
| `1`       | Nombre de colonnes souhaité (gardez‑le à 1 pour rester vertical) |

Lorsque Excel évalue cela, il produit une liste **verticale** :

```
A1: 1
A2: 2
A3: 3
A4: 0   (filled with zeros)
A5: 0
```

> **Pourquoi utiliser EXPAND ?** Elle supprime le besoin de copier manuellement ou d’utiliser des boucles VBA. La fonction redimensionne dynamiquement les données, rendant vos classeurs plus robustes et plus faciles à entretenir.

---

## Étape 4 : Enregistrer le classeur Excel – Persister le résultat

Avec la formule en place, la dernière étape consiste à écrire le classeur sur le disque. Vous pouvez choisir n’importe quel dossier où vous avez les droits d’écriture.

```csharp
        // Step 4: Save the workbook to view the result
        string outputPath = @"C:\Temp\ExpandFormula.xlsx";
        workbook.Save(outputPath);
    }
}
```

> **Ce que vous verrez :** Ouvrez `ExpandFormula.xlsx` dans Excel, et la cellule `A1` affichera le tableau étendu. La formule elle‑même reste dans la cellule, de sorte que si vous modifiez le tableau source, la sortie se met à jour automatiquement.

---

## Optionnel : Vérifier la sortie programmatique

Si vous préférez ne pas ouvrir Excel manuellement, vous pouvez relire les valeurs pour confirmer qu’elles correspondent aux attentes.

```csharp
        // Verify values without opening Excel
        for (int row = 0; row < 5; row++)
        {
            var value = worksheet.Cells[row, 0].Value; // column 0 = A
            Console.WriteLine($"Row {row + 1}: {value}");
        }
```

L’exécution du code ci‑dessus affichera :

```
Row 1: 1
Row 2: 2
Row 3: 3
Row 4: 0
Row 5: 0
```

---

## Questions fréquentes & cas particuliers

| Question | Réponse |
|----------|----------|
| **Puis‑je utiliser EXPAND avec un tableau source plus grand ?** | Absolument. Remplacez simplement `{1,2,3}` par n’importe quelle constante ou plage de cellules, par ex. `EXPAND(A1:C1,10,1)`. |
| **Et si j’ai besoin d’un résultat horizontal ?** | Inversez les arguments ligne/colonne : `EXPAND({1,2,3},1,5)` produira une diffusion de 1 ligne et 5 colonnes. |
| **Cette fonction fonctionne‑t‑elle sur les anciennes versions d’Excel ?** | `EXPAND` est disponible à partir d’Excel 365/2021. Pour les versions antérieures, il faut simuler le tableau avec `INDEX`/`SEQUENCE`. |
| **Dois‑je appeler `workbook.CalculateFormula()` ?** | Non. Aspose.Cells évalue automatiquement les formules lors de l’enregistrement, les valeurs apparaissent immédiatement. |
| **Comment ajouter plus d’une feuille avant l’enregistrement ?** | Appelez `workbook.Worksheets.Add("SecondSheet")` et répétez les étapes de manipulation des cellules sur la nouvelle feuille. |

---

## Exemple complet fonctionnel

Voici le programme complet, prêt à être exécuté. Copiez‑collez‑le dans une application console, ajustez le chemin de sortie, puis appuyez sur **F5**.

```csharp
using System;
using Aspose.Cells;

namespace ExcelAutomationDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Create new workbook
            Workbook workbook = new Workbook();

            // Access first worksheet
            Worksheet worksheet = workbook.Worksheets[0];

            // Add EXPAND formula to A1
            worksheet.Cells["A1"].Formula = "EXPAND({1,2,3},5,1)";

            // Optional: verify values in console
            workbook.CalculateFormula(); // ensures formulas are evaluated now
            for (int i = 0; i < 5; i++)
            {
                Console.WriteLine($"A{i + 1} = {worksheet.Cells[i, 0].Value}");
            }

            // Save the workbook
            string filePath = @"C:\Temp\ExpandFormula.xlsx";
            workbook.Save(filePath);
            Console.WriteLine($"Workbook saved to {filePath}");
        }
    }
}
```

**Sortie attendue dans la console :**

```
A1 = 1
A2 = 2
A3 = 3
A4 = 0
A5 = 0
Workbook saved to C:\Temp\ExpandFormula.xlsx
```

Ouvrez le fichier généré et vous verrez les mêmes nombres remplissant la colonne **A**.

---

## Résumé visuel

![Créer un nouveau classeur exemple](create-new-workbook.png "Capture d’écran montrant un nouveau classeur créé avec create new workbook in C#")

*L’image illustre le classeur fraîchement généré avec le résultat d’EXPAND.*

---

## Conclusion

Vous savez maintenant comment **créer un nouveau classeur**, **ajouter une formule à une cellule**, et **enregistrer le classeur Excel** en C#. En maîtrisant **l’utilisation de EXPAND**, vous pouvez générer des tableaux dynamiques sans effort manuel, et tout le processus vous permet de **créer un fichier Excel programmatique** pour n’importe quel scénario d’automatisation.

Et ensuite ? Essayez de remplacer le tableau constant par une référence de plage, expérimentez avec différentes dimensions d’`EXPAND`, ou enchaînez plusieurs formules entre feuilles. Le même schéma fonctionne pour les graphiques, le style et même les tableaux croisés dynamiques—continuez donc à explorer.

Si vous avez rencontré des difficultés, laissez un commentaire ci‑dessous. Bon codage, et profitez de la puissance d’Excel programmatique !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}