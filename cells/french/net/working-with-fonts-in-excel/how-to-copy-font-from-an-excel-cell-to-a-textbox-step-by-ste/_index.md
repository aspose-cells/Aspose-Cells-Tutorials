---
category: general
date: 2026-02-15
description: Comment copier la police et appliquer le style de cellule en C# avec
  un exemple simple. Apprenez comment obtenir le style de cellule et utiliser le formatage
  de cellule pour définir la taille de police d’une zone de texte.
draft: false
keywords:
- how to copy font
- apply cell style
- get cell style
- use cell formatting
- set textbox font size
language: fr
og_description: Comment copier la police d’une cellule de feuille de calcul et appliquer
  le style de cellule à une zone de texte. Ce guide montre comment obtenir le style
  de cellule, utiliser le formatage de cellule et définir la taille de police de la
  zone de texte.
og_title: Comment copier la police d’une cellule Excel – Tutoriel complet C#
tags:
- C#
- EPPlus
- UI‑grid
- Excel‑interop
title: Comment copier la police d’une cellule Excel vers une zone de texte – Guide
  étape par étape
url: /fr/net/working-with-fonts-in-excel/how-to-copy-font-from-an-excel-cell-to-a-textbox-step-by-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# comment copier la police d’une cellule Excel vers une TextBox – Tutoriel complet C#

Vous avez déjà eu besoin de **copier la police** d’une cellule de feuille de calcul et de faire en sorte qu’une zone de texte UI ressemble exactement ? Vous n’êtes pas seul. Dans de nombreux outils de reporting ou tableaux de bord personnalisés, vous vous retrouvez à extraire des données d’Excel puis à essayer de conserver la fidélité visuelle — famille de police, taille et couleur—intactes.  

Bonne nouvelle : avec quelques lignes de C# vous pouvez **obtenir le style de la cellule**, lire ses propriétés de police, et **appliquer le style de la cellule** à n’importe quel contrôle TextBox. Dans ce tutoriel, nous parcourrons un exemple complet et exécutable montrant comment **utiliser le formatage de cellule** et même **définir la taille de police d’une textbox** de façon programmatique.

---

## Ce que vous allez apprendre

- Comment récupérer un objet `TextBox` depuis un composant de grille (`gridJs` dans notre exemple)  
- Comment lire la famille, la taille et la couleur de police d’une cellule Excel spécifique (`B2`)  
- Comment copier ces attributs de police dans la zone de texte afin que l’UI reflète la feuille de calcul  
- Les pièges courants (par ex. conversion de couleur) et quelques **pro tips** pour rendre votre code robuste  
- Un extrait de code prêt à l’emploi que vous pouvez coller dans une application console ou un projet WinForms  

**Prérequis**  
Vous devez disposer de :

1. .NET 6+ (ou .NET Framework 4.8) installé  
2. Le package NuGet EPPlus (pour la manipulation d’Excel)  
3. Un contrôle de grille exposant un dictionnaire `TextBoxes` (l’exemple utilise un fictif `gridJs` mais le principe fonctionne avec n’importe quelle bibliothèque UI)

Passons maintenant à la pratique.

---

## Étape 1 : Configurer le projet et charger la feuille de calcul

Tout d’abord, créez un nouveau projet console ou WinForms et ajoutez EPPlus :

```bash
dotnet add package EPPlus --version 6.*
```

Ensuite, chargez le classeur et récupérez la cellule dont vous voulez copier le style.

```csharp
using OfficeOpenXml;
using OfficeOpenXml.Style;
using System.Drawing;

// ...

// Load the Excel file (make sure the file exists at the given path)
var fileInfo = new FileInfo(@"C:\Data\Sample.xlsx");
using var package = new ExcelPackage(fileInfo);
ExcelWorksheet ws = package.Workbook.Worksheets["Sheet1"]; // adjust sheet name if needed

// Retrieve the style of cell B2
ExcelStyle cellStyle = ws.Cells["B2"].Style;
```

**Pourquoi c’est important :** EPPlus vous donne un accès direct à l’objet `Style`, qui contient l’objet `Font`. Vous pouvez alors lire `Name`, `Size` et `Color`. C’est le cœur de l’opération **get cell style**.

---

## Étape 2 : Récupérer la TextBox cible depuis votre grille

En supposant que votre grille UI (`gridJs`) stocke les zones de texte dans un dictionnaire indexé par le nom de colonne, vous pouvez récupérer celle dont vous avez besoin ainsi :

```csharp
// Fake grid class for illustration – replace with your actual grid component
var gridJs = new MyGrid(); // MyGrid is a placeholder for your UI control

// Step 1: Retrieve the "Notes" text box from the grid
var notesTextBox = gridJs.TextBoxes["Notes"];
```

Si vous utilisez WinForms, `notesTextBox` pourrait être un contrôle `TextBox` ; pour WPF ce sera un élément `TextBox`, et pour une grille web‑based cela pourrait être un objet d’interopérabilité JavaScript. L’essentiel est d’avoir une référence manipulable.

---

## Étape 3 : Transférer la famille de police

Maintenant que nous disposons du style source et du contrôle destination, copions la famille de police.

```csharp
// Apply the cell's font family to the text box
notesTextBox.FontFamily = cellStyle.Font.Name;
```

**Pro tip :** Tous les frameworks UI n’exposent pas une propriété `FontFamily` acceptant une simple chaîne. En WinForms vous feriez : `notesTextBox.Font = new Font(cellStyle.Font.Name, notesTextBox.Font.Size);`. Adaptez selon votre environnement.

---

## Étape 4 : Transférer la taille de police

La taille de police est stockée comme `float` dans EPPlus. Appliquez‑la directement :

```csharp
// Apply the cell's font size to the text box
notesTextBox.FontSize = cellStyle.Font.Size;
```

Si votre contrôle utilise des points (ce qui est le cas le plus souvent), vous pouvez assigner la valeur sans conversion. Pour les grilles basées sur CSS, il faudra peut‑être ajouter le suffixe `"pt"`.

---

## Étape 5 : Transférer la couleur de police

La conversion de couleur est la partie la plus délicate car EPPlus stocke les couleurs sous forme d’entiers ARGB, alors que de nombreux frameworks UI attendent un `System.Drawing.Color` ou une chaîne hex CSS.

```csharp
// Apply the cell's font colour to the text box
// EPPlus stores colour as a System.Drawing.Color when using .Color property
var excelColor = cellStyle.Font.Color?.GetColor();

// Fallback to black if the cell has no explicit colour
var safeColor = excelColor ?? Color.Black;

// Convert to the format your UI expects (example for WinForms)
notesTextBox.FontColor = safeColor;
```

> **Pourquoi cela fonctionne :** `GetColor()` résout les couleurs basées sur le thème et renvoie un `System.Drawing.Color` concret. Si la cellule utilise la couleur par défaut (aucune valeur explicite), nous revenons au noir afin d’éviter les exceptions de référence nulle.

---

## Exemple complet fonctionnel

En rassemblant le tout, voici une application console minimale qui lit un fichier Excel, extrait la police de **B2**, et l’applique à une zone de texte factice.

```csharp
using OfficeOpenXml;
using OfficeOpenXml.Style;
using System;
using System.Collections.Generic;
using System.Drawing;

namespace FontCopyDemo
{
    // Mock grid control – replace with your real UI component
    public class MyGrid
    {
        public Dictionary<string, TextBoxMock> TextBoxes { get; } = new()
        {
            { "Notes", new TextBoxMock() }
        };
    }

    // Simple text box representation for demonstration
    public class TextBoxMock
    {
        public string FontFamily { get; set; }
        public float FontSize { get; set; }
        public Color FontColor { get; set; }

        public override string ToString()
        {
            return $"FontFamily: {FontFamily}, FontSize: {FontSize}, FontColor: {FontColor.Name}";
        }
    }

    class Program
    {
        static void Main()
        {
            // 1️⃣ Load Excel worksheet
            var fileInfo = new FileInfo(@"C:\Data\Sample.xlsx");
            using var package = new ExcelPackage(fileInfo);
            var ws = package.Workbook.Worksheets["Sheet1"];
            var cellStyle = ws.Cells["B2"].Style;

            // 2️⃣ Grab the target TextBox from the grid
            var gridJs = new MyGrid();
            var notesTextBox = gridJs.TextBoxes["Notes"];

            // 3️⃣ Apply font family
            notesTextBox.FontFamily = cellStyle.Font.Name;

            // 4️⃣ Apply font size
            notesTextBox.FontSize = cellStyle.Font.Size;

            // 5️⃣ Apply font colour (with safety net)
            var excelColor = cellStyle.Font.Color?.GetColor();
            notesTextBox.FontColor = excelColor ?? Color.Black;

            // Output the result for verification
            Console.WriteLine("TextBox after copying font:");
            Console.WriteLine(notesTextBox);
        }
    }
}
```

**Sortie attendue (en supposant que B2 utilise Arial, 12 pt, bleu) :**

```
TextBox after copying font:
FontFamily: Arial, FontSize: 12, FontColor: Blue
```

Exécutez le programme, ouvrez votre UI, et vous verrez la zone de texte « Notes » refléter exactement le style de police de la cellule **B2**. Aucun ajustement manuel requis.

---

## Questions fréquentes & cas particuliers

### Et si la cellule utilise une couleur de thème au lieu d’une valeur RVB explicite ?

`GetColor()` d’EPPlus résout automatiquement les couleurs de thème en un `System.Drawing.Color` concret. Cependant, si vous utilisez une bibliothèque plus ancienne qui ne renvoie que l’indice du thème, vous devrez mapper cet indice à une palette de couleurs vous‑même.

### Puis‑je copier d’autres attributs de style (gras, italique, etc.) ?

Absolument. L’objet `ExcelStyle.Font` expose aussi `Bold`, `Italic`, `Underline` et `Strike`. Il suffit de définir les propriétés correspondantes sur votre contrôle UI :

```csharp
notesTextBox.FontBold = cellStyle.Font.Bold;
notesTextBox.FontItalic = cellStyle.Font.Italic;
```

### Et si le contrôle de grille n’expose pas de propriété `FontColor` ?

La plupart des frameworks modernes le font, mais si le vôtre n’accepte qu’une chaîne CSS, convertissez le `Color` en hex :

```csharp
string hex = $"#{notesTextBox.FontColor.R:X2}{notesTextBox.FontColor.G:X2}{notesTextBox.FontColor.B:X2}";
notesTextBox.Style["color"] = hex; // for web‑based grids
```

### Comment gérer plusieurs cellules simultanément ?

Parcourez la plage souhaitée, récupérez le style de chaque cellule, et appliquez‑le à la zone de texte correspondante. Pensez à mettre en cache les objets de style si vous traitez de nombreuses lignes afin d’éviter des pertes de performances.

---

## Pro tips & pièges courants

- **Mettez en cache l’ExcelPackage** — ouvrir et fermer le fichier pour chaque cellule est coûteux. Chargez le classeur une fois, puis réutilisez l’objet `ExcelWorksheet`.  
- **Surveillez les couleurs nulles** — une cellule qui hérite de la couleur par défaut renvoie `null`. Fournissez toujours une valeur de secours (noir ou la couleur par défaut du contrôle).  
- **Prenez en compte le DPI** — sur des écrans haute‑DPI, les tailles de police peuvent paraître légèrement plus grandes. Ajustez avec `Graphics.DpiX` si besoin.  
- **Sécurité des threads** — EPPlus n’est pas thread‑safe. Si vous traitez plusieurs feuilles en parallèle, créez un `ExcelPackage` distinct par thread.

---

## Conclusion

Vous savez maintenant **comment copier la police** d’une cellule Excel et **appliquer le style de cellule** à n’importe quel contrôle TextBox en C#. En récupérant le `Style` de la cellule, en extrayant ses propriétés `Font`, et en les assignant à l’élément UI, vous préservez la cohérence visuelle sans copier manuellement.  

La solution complète — chargement du classeur, obtention du style de la cellule, et réglage de la famille, de la taille et de la couleur de police de la textbox — couvre le cœur de **use cell formatting** et montre comment **set textbox font size** correctement.  

Ensuite, essayez d’étendre l’exemple pour copier les couleurs d’arrière‑plan, les bordures, ou même le contenu complet des cellules. Si vous travaillez avec une bibliothèque de grille de données supportant le rendu riche, vous pouvez désormais lui fournir exactement les mêmes informations de style que vous avez extraites d’Excel, gardant ainsi votre UI et vos rapports parfaitement synchronisés.

Des questions ? Laissez un commentaire ou explorez des sujets connexes comme « dynamic Excel‑to‑UI binding » et « theme‑aware colour conversion ». Bon codage !

---

![exemple de copie de police](placeholder-image.jpg "comment copier la police d’une cellule Excel vers une TextBox")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}