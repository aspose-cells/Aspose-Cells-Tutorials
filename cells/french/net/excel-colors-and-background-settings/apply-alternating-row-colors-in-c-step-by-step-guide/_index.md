---
category: general
date: 2026-03-18
description: Apprenez à appliquer des couleurs de lignes alternées dans une feuille
  de calcul en C#. Comprend la définition de la couleur d’arrière‑plan des lignes,
  l’ajout d’un arrière‑plan jaune clair et la coloration alternée des lignes.
draft: false
keywords:
- apply alternating row colors
- set row background color
- add light yellow background
- set alternating row shading
- color rows alternately
language: fr
og_description: Appliquez des couleurs de lignes alternées en C# pour améliorer la
  lisibilité. Ce guide montre comment définir la couleur d’arrière‑plan des lignes,
  ajouter un arrière‑plan jaune clair et colorer les lignes de manière alternée.
og_title: Appliquer des couleurs de lignes alternées en C# – Tutoriel complet
tags:
- C#
- DataTable
- Spreadsheet styling
- UI design
title: Appliquer des couleurs de lignes alternées en C# – Guide étape par étape
url: /fr/net/excel-colors-and-background-settings/apply-alternating-row-colors-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Appliquer des Couleurs de Ligne Alternées en C# – Tutoriel Complet

Vous avez déjà eu besoin **d’appliquer des couleurs de ligne alternées** à une feuille de calcul basée sur des données mais vous ne saviez pas par où commencer ? Vous n’êtes pas seul — la plupart des développeurs rencontrent ce problème lorsqu’ils essaient pour la première fois de rendre les tableaux un peu plus agréables. La bonne nouvelle ? En quelques lignes de C# vous pouvez **définir la couleur d’arrière‑plan d’une ligne**, ajouter un **fond jaune clair**, et obtenir une grille soignée qui améliore immédiatement la lisibilité.

Dans ce tutoriel, nous parcourrons l’ensemble du processus, depuis le chargement d’un `DataTable` en mémoire jusqu’à la mise en forme de chaque ligne avec une bande jaune‑blanc subtile. À la fin, vous serez capable **de colorer les lignes alternativement** en toute confiance, et vous verrez également quelques variantes pratiques pour des nuances différentes ou un thème dynamique.

## Ce dont vous avez besoin

Avant de commencer, assurez‑vous d’avoir les éléments suivants :

- Un projet .NET ciblant .NET 6 ou supérieur (le code fonctionne également sur .NET Framework 4.7+).  
- Une bibliothèque de feuilles de calcul qui prend en charge les objets de style – l’exemple utilise une API générique `Workbook`/`Worksheet` qui reflète des bibliothèques comme **Aspose.Cells**, **GemBox.Spreadsheet**, ou **ClosedXML**.  
- Une source `DataTable` – peut provenir d’une requête de base de données, d’une importation CSV, ou de toute collection en mémoire.  

Aucun package NuGet supplémentaire n’est requis au‑delà de la bibliothèque de feuilles de calcul elle‑même. Si vous utilisez Aspose.Cells, l’espace de noms est `Aspose.Cells` ; pour ClosedXML c’est `ClosedXML.Excel`. Remplacez les appels `CreateStyle` et `ImportDataTable` en conséquence.

## Étape 1 : Récupérer les données source sous forme de DataTable

Première chose à faire — récupérer les données que vous souhaitez afficher. Dans les applications réelles, cela signifie généralement interroger une base de données, mais pour plus de clarté nous allons simuler une méthode d’aide appelée `GetData()` qui renvoie un `DataTable` rempli.

```csharp
// Step 1: Retrieve the source data as a DataTable
DataTable dataTable = GetData();   // Replace with your actual data retrieval logic
```

> **Pourquoi c’est important :** Le `DataTable` définit les lignes et les colonnes qui recevront plus tard le remplissage alterné. Si le tableau est vide, il n’y a rien à styliser, donc vérifiez toujours que `Rows.Count` > 0 avant de continuer.

### Astuce pro
Si vous récupérez des données depuis Entity Framework, vous pouvez utiliser `DataTable.Load(reader)` après l’exécution d’un `SqlCommand`. Cela garde le code propre et évite les définitions manuelles de colonnes.

## Étape 2 : Allouer un tableau pour contenir un style par ligne

Ensuite, nous avons besoin d’un conteneur dont la taille correspond au nombre de lignes. La plupart des API de feuilles de calcul vous permettent de passer un tableau de styles à la méthode d’importation, nous allons donc créer un `Style[]` dimensionné exactement au nombre de lignes.

```csharp
// Step 2: Allocate an array to hold a style for each row
Style[] rowStyles = new Style[dataTable.Rows.Count];
```

> **Explication :** En pré‑allouant le tableau, nous évitons de recréer un nouvel objet style à chaque itération, ce qui peut constituer un gain de performance lorsqu’on traite des milliers de lignes.

## Étape 3 : Appliquer des couleurs de ligne alternées (Jaune clair / Blanc)

Voici le cœur du sujet : **appliquer des couleurs de ligne alternées**. Nous parcourrons chaque ligne, créerons une nouvelle instance de style à partir du classeur, et définirons son arrière‑plan en fonction de l’indice de ligne. Les lignes paires recevront un remplissage jaune clair, les lignes impaires resteront blanches.

```csharp
// Step 3: Create alternating background colors (light yellow / white) for the rows
for (int rowIndex = 0; rowIndex < dataTable.Rows.Count; rowIndex++)
{
    // Create a new style instance from the workbook
    rowStyles[rowIndex] = wb.CreateStyle();

    // Apply a light yellow background to even rows, white to odd rows
    rowStyles[rowIndex].ForegroundColor = (rowIndex % 2 == 0)
        ? Color.LightYellow   // add light yellow background
        : Color.White;        // set row background color to white

    rowStyles[rowIndex].Pattern = BackgroundType.Solid; // set alternating row shading
}
```

### Pourquoi cela fonctionne
- **`rowIndex % 2 == 0`** vérifie si la ligne est paire.  
- **`Color.LightYellow`** fournit une teinte douce et non intrusive, parfaite pour les tableaux de données.  
- **`BackgroundType.Solid`** garantit que le remplissage couvre toute la cellule, obtenant ainsi l’effet **set row background color**.  

Vous pouvez remplacer `Color.LightYellow` par n’importe quelle autre nuance (par ex. `Color.LightCyan`) si vous préférez un rendu différent. La même logique vous permet également **de colorer les lignes alternativement** selon d’autres critères, comme des indicateurs d’état.

## Étape 4 : Importer le DataTable dans la feuille avec les styles préparés

Enfin, nous injectons le tout dans la feuille. La plupart des bibliothèques exposent une surcharge `ImportDataTable` qui accepte un tableau de styles. Le drapeau `true` indique à l’API d’écrire les en‑têtes de colonnes, et les coordonnées `0, 0` démarrent à la cellule en haut à gauche.

```csharp
// Step 4: Import the DataTable into the worksheet, applying the prepared row styles
ws.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);
```

> **Résultat :** La feuille affiche maintenant vos données avec un motif propre d’**alternating row shading** — jaune clair sur les lignes paires, blanc sur les lignes impaires. Les utilisateurs peuvent parcourir la grille sans que leurs yeux sautent d’une ligne à l’autre.

### Résultat attendu
Si vous ouvrez le classeur généré, vous verrez quelque chose comme :

| ID | Nom       | Quantité |
|----|-----------|----------|
| **1** | Apple      | 50       |
| **2** | Banana     | 30       |
| **3** | Cherry     | 20       |
| **4** | Date       | 15       |

Les lignes 1, 3, 5… ont un **fond jaune clair**, tandis que les lignes 2, 4, 6… restent **blanches**. La ligne d’en‑tête (ligne 0) hérite du style par défaut sauf si vous la personnalisez séparément.

## Variantes optionnelles & Cas limites

### 1. Utiliser une palette de couleurs différente
Si le jaune clair ne correspond pas à votre charte graphique, remplacez simplement `Color.LightYellow` par une autre `System.Drawing.Color`. Pour un thème bleu‑gris, vous pourriez utiliser :

```csharp
rowStyles[rowIndex].ForegroundColor = (rowIndex % 2 == 0)
    ? Color.FromArgb(220, 235, 247) // soft blue
    : Color.White;
```

### 2. Ombrage dynamique selon les données
Parfois, vous voulez mettre en évidence les lignes qui remplissent une condition (par ex. stock faible). Combinez le test modulo avec une vérification personnalisée :

```csharp
int quantity = Convert.ToInt32(dataTable.Rows[rowIndex]["Quantity"]);
if (quantity < 20)
{
    rowStyles[rowIndex].ForegroundColor = Color.Salmon; // urgent low‑stock color
}
else
{
    rowStyles[rowIndex].ForegroundColor = (rowIndex % 2 == 0)
        ? Color.LightYellow
        : Color.White;
}
```

### 3. Appliquer des styles uniquement à certaines colonnes
Si vous ne devez appliquer le **set row background color** que sur certaines colonnes, créez un style séparé pour chaque colonne et assignez‑le après l’importation en utilisant l’API de plage de cellules de la feuille.

```csharp
// Example for column B only
var colBStyle = wb.CreateStyle();
colBStyle.ForegroundColor = Color.LightYellow;
colBStyle.Pattern = BackgroundType.Solid;

// Apply after import
ws.Cells[$"B2:B{dataTable.Rows.Count + 1}"].SetStyle(colBStyle);
```

### 4. Astuce de performance pour les grandes tables
Lorsque vous traitez plus de 10 000 lignes, envisagez de réutiliser un seul objet style pour chaque couleur au lieu d’en créer un nouveau par ligne. Le tableau contiendra alors des références aux deux styles partagés, réduisant considérablement la consommation mémoire.

```csharp
Style yellowStyle = wb.CreateStyle();
yellowStyle.ForegroundColor = Color.LightYellow;
yellowStyle.Pattern = BackgroundType.Solid;

Style whiteStyle = wb.CreateStyle();
whiteStyle.ForegroundColor = Color.White;
whiteStyle.Pattern = BackgroundType.Solid;

for (int i = 0; i < dataTable.Rows.Count; i++)
    rowStyles[i] = (i % 2 == 0) ? yellowStyle : whiteStyle;
```

## Exemple complet fonctionnel

Voici un programme autonome que vous pouvez coller dans une application console. Il utilise une API fictive `Workbook`/`Worksheet` ; remplacez les types par ceux de la bibliothèque que vous avez choisie.

```csharp
using System;
using System.Data;
using System.Drawing;          // For Color
using YourSpreadsheetLib;     // Replace with actual namespace

class Program
{
    static void Main()
    {
        // Initialize workbook & worksheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];

        // Step 1: Retrieve data
        DataTable dataTable = GetData();

        // Step 2: Allocate style array
        Style[] rowStyles = new Style[dataTable.Rows.Count];

        // Step 3: Apply alternating row colors
        for (int i = 0; i < dataTable.Rows.Count; i++)
        {
            rowStyles[i] = wb.CreateStyle();
            rowStyles[i].ForegroundColor = (i % 2 == 0)
                ? Color.LightYellow   // add light yellow background
                : Color.White;        // set row background color
            rowStyles[i].Pattern = BackgroundType.Solid; // set alternating row shading
        }

        // Step 4: Import with styles
        ws.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);

        // Save to file
        wb.Save("AlternatingRows.xlsx");
        Console.WriteLine("Workbook saved with alternating row colors.");
    }

    // Sample data generator
    static DataTable GetData()
    {
        var dt = new DataTable();
        dt.Columns.Add("ID", typeof(int));
        dt.Columns.Add("Product", typeof(string));
        dt.Columns.Add("Quantity", typeof(int));

        dt.Rows.Add(1, "Apple", 50);
        dt.Rows.Add(2, "Banana", 30);
        dt.Rows.Add(3, "Cherry", 20);
        dt.Rows.Add(4, "Date", 15);
        dt.Rows.Add(5, "Elderberry", 5);
        return dt;
    }
}
```

**Sortie :** Un fichier nommé `AlternatingRows.xlsx` où chaque ligne alterne entre un remplissage jaune clair et blanc, rendant le tableau plus agréable à lire.

## Questions fréquentes

**Q : Cette approche fonctionne‑t‑elle avec le formatage conditionnel de type Excel ?**  
R : Oui. Si votre bibliothèque prend en charge les règles conditionnelles, vous pouvez traduire la même logique en une règle qui vérifie `MOD(ROW(),2)=0`. La méthode basée sur le code présentée ici est plus portable entre les bibliothèques qui ne disposent pas de formatage conditionnel intégré.

**Q : Et si je dois **colorer les lignes alternativement** dans un tableau PDF au lieu d’une feuille Excel ?**  
R : La plupart des générateurs de tables PDF (par ex. iTextSharp, PdfSharp) vous permettent de définir une `BackgroundColor` par ligne. Le même calcul modulo s’applique—

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}