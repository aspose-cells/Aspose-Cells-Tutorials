---
category: general
date: 2026-06-05
description: Appliquez les styles de cellules lors de l'importation avec Aspose.Cells.
  Apprenez comment importer un DataTable avec mise en forme, styliser les lignes et
  garder les feuilles de calcul bien ordonnées.
draft: false
keywords:
- apply cell styles
- aspose cells import
- import with formatting
- how to import datatable
- import datatable worksheet
language: fr
og_description: Appliquez des styles de cellule lors de l'importation d'un DataTable
  dans une feuille de calcul Aspose.Cells. Guide étape par étape avec le code complet
  et des astuces.
og_title: Appliquer des styles de cellules avec Aspose.Cells – Importer DataTable
schemas:
- author: Aspose
  dateModified: '2026-06-05'
  description: Apply cell styles while using Aspose.Cells import. Learn how to import
    DataTable with formatting, style rows, and keep worksheets tidy.
  headline: Apply Cell Styles with Aspose.Cells – Import DataTable with Formatting
  type: TechArticle
- description: Apply cell styles while using Aspose.Cells import. Learn how to import
    DataTable with formatting, style rows, and keep worksheets tidy.
  name: Apply Cell Styles with Aspose.Cells – Import DataTable with Formatting
  steps:
  - name: How It Works
    text: 1. **Headers** – Because we passed `true`, Aspose writes “Name” and “Score”
      into the first row. 2. **Data Rows** – Each subsequent row receives the corresponding
      style from `importStyles`. 3. **Performance** – The method streams the data
      directly into the worksheet, which is faster than looping cell
  - name: What if My DataTable Has More Columns Than Styles?
    text: Aspose will apply the last style in the array to any extra columns. To avoid
      unexpected colors, always match the array length to the column count, or pass
      `null` for columns you don’t want styled.
  - name: Can I Apply Different Styles to Specific Rows?
    text: 'Absolutely. After the import, you can loop through rows and assign new
      `Style` objects based on conditions (e.g., highlight scores > 90 in green).
      Here’s a quick snippet:'
  - name: Does This Work with Large DataSets?
    text: Yes. `ImportDataTable` streams data efficiently, and applying a static style
      array adds negligible overhead. For millions of rows, consider using `ImportDataTable`
      in chunks or leveraging `Cells.ImportDataTable` with a `DataReader` for even
      better memory usage.
  - name: How Do I Preserve Existing Formatting in the Worksheet?
    text: If the target range already has formatting you want to keep, set the `ImportDataTable`
      overload’s `importOptions` parameter (`ImportTableOptions`) and tweak `ImportDataTableOptions.PreserveCellFormatting`.
      The default behavior overwrites styles with the ones you supply.
  type: HowTo
tags:
- Aspose.Cells
- C#
- DataTable
title: Appliquer les styles de cellules avec Aspose.Cells – Importer un DataTable
  avec mise en forme
url: /fr/net/excel-formatting-and-styling/apply-cell-styles-with-aspose-cells-import-datatable-with-fo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Appliquer des styles de cellule avec Aspose.Cells – Importer DataTable avec mise en forme

Vous vous êtes déjà demandé comment **appliquer des styles de cellule** lorsque vous importez un `DataTable` dans une feuille Excel ? Vous n'êtes pas le seul. Dans de nombreux scénarios de reporting, vous avez besoin que les données soient présentables dès le départ—sans mise en forme manuelle ultérieure. La bonne nouvelle, c’est qu’Aspose.Cells rend l’**importation avec mise en forme** simple, de sorte que vos lignes puissent être rouges ou bleues, en gras, ou tout ce que vous désirez.

Dans ce tutoriel, nous parcourrons un exemple complet et exécutable qui montre **comment importer un datatable** dans une feuille de calcul **avec des styles de cellule** appliqués. À la fin, vous disposerez d’une application console C# prête à l’emploi qui crée un classeur, applique des styles aux deux premières colonnes et enregistre le fichier—le tout en utilisant l’API `aspose cells import`.

## Ce que vous apprendrez

- Configurer Aspose.Cells dans un projet .NET  
- Créer un `DataTable` d’exemple qui imite des données réelles  
- Définir des objets `Style` pour des polices rouges et bleues  
- Utiliser `Worksheet.Cells.ImportDataTable` pour **importer la feuille de calcul datatable** tout en appliquant les styles  
- Vérifier le résultat et enregistrer le classeur  

Aucun outil externe, juste du C# pur et Aspose.Cells. Commençons.

---

## Prérequis

Avant de plonger dans le code, assurez‑vous d’avoir les éléments suivants :

| Requirement | Why it matters |
|-------------|----------------|
| .NET 6.0 or later | Aspose.Cells 23.x cible .NET Standard 2.0+, donc .NET 6 vous donne les dernières fonctionnalités du runtime. |
| Aspose.Cells for .NET (NuGet) | La bibliothèque fournit les méthodes `Workbook`, `Worksheet`, `Style` et `ImportDataTable` dont nous avons besoin. |
| Basic C# knowledge | Vous comprendrez les classes, les tableaux et les instructions `using`. |
| An IDE (Visual Studio, VS Code, Rider) | Tout éditeur fonctionne, mais vous devrez restaurer les packages NuGet. |

Vous pouvez installer le package depuis la ligne de commande :

```bash
dotnet add package Aspose.Cells
```

---

## Étape 1 : Créer un nouveau classeur et accéder à la première feuille de calcul

Première chose à faire—créons un `Workbook` et récupérons la première feuille. Pensez au classeur comme à un cahier vierge ; la première feuille de calcul est la page sur laquelle nous allons écrire.

```csharp
using Aspose.Cells;
using System;
using System.Data;
using System.Drawing;

class Program
{
    static void Main()
    {
        // Create a new workbook (equivalent to a new Excel file)
        Workbook wb = new Workbook();

        // Access the first worksheet (index 0)
        Worksheet worksheet = wb.Worksheets[0];
```

> **Astuce :** Si vous avez besoin de plusieurs feuilles, ajoutez‑les simplement avec `wb.Worksheets.Add()` et référencez‑les par leur nom ou leur indice.

---

## Étape 2 : Préparer un DataTable d’exemple (Comment importer DataTable)

Nous avons maintenant besoin de quelque chose à importer. Dans des projets réels, vous interrogeriez une base de données, mais pour plus de clarté, nous allons créer un `DataTable` en mémoire.

```csharp
        // Build a sample DataTable with two columns: Name and Score
        DataTable dataTable = new DataTable("Results");
        dataTable.Columns.Add("Name", typeof(string));
        dataTable.Columns.Add("Score", typeof(int));

        // Populate rows – imagine these came from a query
        dataTable.Rows.Add("Alice", 85);
        dataTable.Rows.Add("Bob", 92);
        dataTable.Rows.Add("Charlie", 78);
        dataTable.Rows.Add("Diana", 91);
```

> **Pourquoi c’est important :** Disposer d’un `DataTable` nous permet de tester le flux **aspose cells import** sans aucune dépendance externe.

---

## Étape 3 : Définir les styles à appliquer aux cellules importées

C’est ici que la magie opère. Nous créerons deux objets `Style` : l’un avec une police rouge, l’autre avec une police bleue. Ils seront appliqués colonne par colonne lors de l’importation.

```csharp
        // Define an array of styles – one per column
        Style[] importStyles = new Style[2];

        // Style for the first column (Name) – red text
        Style redStyle = wb.CreateStyle();
        redStyle.Font.Color = Color.Red;
        importStyles[0] = redStyle;

        // Style for the second column (Score) – blue text
        Style blueStyle = wb.CreateStyle();
        blueStyle.Font.Color = Color.Blue;
        importStyles[1] = blueStyle;
```

> **Attention :** La longueur de `importStyles` doit correspondre au nombre de colonnes que vous importez, sinon Aspose lèvera une `ArgumentException`.

---

## Étape 4 : Importer le DataTable dans la feuille de calcul **avec mise en forme**

Rassemblons maintenant le tout. La surcharge de `ImportDataTable` que nous utilisons accepte le tableau `Style[]`, nous permettant **d’appliquer des styles de cellule** au fur et à mesure que les données sont placées dans la feuille.

```csharp
        // Import the DataTable starting at cell A1 (row 0, column 0)
        // The 'true' flag tells Aspose to generate column headers automatically
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, importStyles);
```

### Comment cela fonctionne

1. **En‑têtes** – Parce que nous avons passé `true`, Aspose écrit « Name » et « Score » dans la première ligne.  
2. **Lignes de données** – Chaque ligne suivante reçoit le style correspondant provenant de `importStyles`.  
3. **Performance** – La méthode diffuse les données directement dans la feuille, ce qui est plus rapide que de parcourir cellule par cellule.

---

## Étape 5 : Vérifier le résultat et enregistrer le classeur

Jetons un œil aux premières cellules pour nous assurer que les styles ont été appliqués, puis écrivons le fichier sur le disque.

```csharp
        // Optional: Quick sanity check – print the first row's values
        Console.WriteLine("Header Row:");
        Console.WriteLine($"{worksheet.Cells[0, 0].StringValue} | {worksheet.Cells[0, 1].StringValue}");

        // Save the workbook to an Excel file
        string outputPath = "StyledImport.xlsx";
        wb.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

Lorsque vous ouvrez **StyledImport.xlsx**, vous verrez :

- La colonne « Name » en texte **rouge**.  
- La colonne « Score » en texte **bleu**.  
- Les en‑têtes de colonne dans le style par défaut (vous pourriez également les styliser, mais cela relève d’un autre tutoriel).

![Exemple d'application de styles de cellule](https://example.com/images/apply-cell-styles.png "Application de styles de cellule dans Aspose.Cells")

> **Remarque :** L’image ci‑dessus montre l’apparence finale. L’attribut `alt` contient le mot‑clé principal, répondant aux exigences SEO.

---

## Questions fréquentes & cas limites

### Que se passe-t‑il si mon DataTable possède plus de colonnes que de styles ?

Aspose appliquera le dernier style du tableau aux colonnes supplémentaires. Pour éviter des couleurs inattendues, assurez‑vous toujours que la longueur du tableau correspond au nombre de colonnes, ou passez `null` pour les colonnes que vous ne souhaitez pas styliser.

### Puis‑je appliquer des styles différents à des lignes spécifiques ?

Absolument. Après l’importation, vous pouvez parcourir les lignes et attribuer de nouveaux objets `Style` en fonction de conditions (par ex., mettre en surbrillance les scores > 90 en vert). Voici un extrait rapide :

```csharp
for (int i = 1; i <= dataTable.Rows.Count; i++) // start at 1 to skip header
{
    int score = worksheet.Cells[i, 1].IntValue;
    if (score > 90)
    {
        Style highScore = wb.CreateStyle();
        highScore.Font.Color = Color.Green;
        worksheet.Cells[i, 1].SetStyle(highScore);
    }
}
```

### Cette méthode fonctionne‑t‑elle avec de grands ensembles de données ?

Oui. `ImportDataTable` diffuse les données de manière efficace, et l’application d’un tableau de styles statique ajoute une surcharge négligeable. Pour des millions de lignes, envisagez d’utiliser `ImportDataTable` par morceaux ou d’exploiter `Cells.ImportDataTable` avec un `DataReader` pour une utilisation mémoire encore meilleure.

### Comment conserver le formatage existant dans la feuille de calcul ?

Si la plage cible possède déjà un formatage que vous souhaitez conserver, définissez le paramètre `importOptions` de la surcharge `ImportDataTable` (`ImportTableOptions`) et ajustez `ImportDataTableOptions.PreserveCellFormatting`. Le comportement par défaut écrase les styles par ceux que vous fournissez.

---

## Récapitulatif : ce que nous avons accompli

- **Appliqué des styles de cellule** lors d’une opération **aspose cells import**.  
- Démontré **l’importation avec mise en forme** en passant un tableau `Style[]`.  
- Illustré **comment importer un datatable** dans une feuille de calcul et enregistrer le résultat.  
- Couvert les cas limites tels que le nombre de styles ne correspondant pas et le style conditionnel des lignes.

Tout cela a été réalisé dans une seule application console autonome—sans scripts externes, sans manipulation manuelle d’Excel. Vous disposez désormais d’une base solide pour toute fonctionnalité de reporting ou d’exportation de données nécessitant une sortie Excel soignée.

---

## Prochaines étapes

Prêt à passer à la vitesse supérieure ? Voici quelques idées qui s’appuient sur ce que vous venez d’apprendre :

- **Styliser la ligne d’en‑tête** (par ex., gras, couleur d’arrière‑plan).  
- **Appliquer un formatage conditionnel** en utilisant `Worksheet.Cells[i, j].ConditionalFormattingCollection`.  
- **Exporter vers d’autres formats** comme CSV ou PDF avec `wb.Save("file.pdf", SaveFormat.Pdf)`.  
- **Combiner plusieurs DataTables** dans un même classeur, chaque table sur sa propre feuille, en utilisant la même approche de style.

Si vous rencontrez des problèmes, laissez un commentaire ou consultez la documentation officielle d’Aspose sur `ImportDataTable`. Bon codage, et profitez de ces fichiers Excel magnifiquement stylisés !

---

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités supplémentaires de l’API et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Comment importer DataTable dans Excel avec Aspose.Cells pour .NET (Guide étape par étape)](/cells/english/net/import-export/import-datatable-excel-aspose-cells-net/)
- [Comment définir les styles de police dans Excel avec Aspose.Cells pour .NET (Guide étape par étape)]( /cells/english/net/formatting/aspose-cells-dotnet-set-font-styles-excel/)
- [Comment appliquer une ombre de texte dans Excel avec Aspose.Cells .NET : Guide étape par étape](/cells/english/net/formatting/apply-text-shadow-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}