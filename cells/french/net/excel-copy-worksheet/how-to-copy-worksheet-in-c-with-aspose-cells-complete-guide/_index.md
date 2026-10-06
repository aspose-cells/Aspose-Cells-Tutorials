---
category: general
date: 2026-03-30
description: Comment copier une feuille de calcul en C# avec Aspose.Cells – guide
  étape par étape couvrant la copie d’une plage de cellules, la copie de colonnes
  entre feuilles, la copie du tableau croisé dynamique d’une feuille et l’ajout de
  code pour créer une nouvelle feuille.
draft: false
keywords:
- how to copy worksheet
- copy cell range
- copy columns between sheets
- copy worksheet pivot table
- add new worksheet code
language: fr
og_description: Apprenez à copier une feuille de calcul en C# avec Aspose.Cells. Ce
  guide montre comment copier une plage de cellules, préserver les tableaux croisés
  dynamiques, copier des colonnes entre feuilles et ajouter du code pour créer une
  nouvelle feuille.
og_title: Comment copier une feuille de calcul en C# – Tutoriel complet Aspose.Cells
tags:
- Aspose.Cells
- C#
- Excel Automation
title: Comment copier une feuille de calcul en C# avec Aspose.Cells – Guide complet
url: /fr/net/excel-copy-worksheet/how-to-copy-worksheet-in-c-with-aspose-cells-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment copier une feuille de calcul en C# avec Aspose.Cells – Guide complet

Vous vous êtes déjà demandé **comment copier une feuille de calcul** en C# sans perdre un seul tableau croisé dynamique ou formule ? Vous n'êtes pas seul — de nombreux développeurs se heurtent à un mur lorsqu'ils doivent dupliquer une feuille tout en conservant tous les éléments. Dans ce tutoriel, nous parcourrons une solution pratique, de bout en bout, qui non seulement copie les données mais préserve également le **copy worksheet pivot table**, gère le **copy cell range**, et montre le **add new worksheet code** dont vous avez besoin.

Nous couvrirons tout, du chargement du classeur source à l’enregistrement du fichier de destination, afin que vous puissiez copier des colonnes entre feuilles, préserver les objets et garder votre code propre. Pas de références vagues, juste un exemple complet et exécutable que vous pouvez intégrer dès aujourd'hui à votre projet.

## Ce que couvre ce tutoriel

- Chargement d’un fichier Excel existant avec Aspose.Cells  
- Utilisation du **add new worksheet code** pour créer une feuille cible  
- Définition d’un **copy cell range** qui inclut un tableau croisé dynamique  
- Configuration de **CopyOptions** pour conserver les graphiques, formules et tableaux croisés dynamiques intacts  
- Exécution du **copy columns between sheets** avec précision ligne par ligne  
- Enregistrement du résultat et vérification que la feuille a été correctement copiée  

À la fin de ce guide, vous pourrez répondre en toute confiance à la question « how to copy worksheet », que vous automatisiez des rapports ou construisiez une interface utilisateur basée sur des feuilles de calcul.

---

## Comment copier une feuille – Vue d’ensemble

Avant de plonger dans le code, décrivons le flux à haut niveau. Pensez-y comme à une recette :

1. **Load** le classeur source (`Source.xlsx`).  
2. **Add** une nouvelle feuille pour accueillir la copie (`add new worksheet code`).  
3. **Define** la zone que vous souhaitez dupliquer (`copy cell range`).  
4. **Configure** les options de copie afin que le tableau croisé dynamique survive (`copy worksheet pivot table`).  
5. **Copy** les lignes et colonnes (`copy columns between sheets`).  
6. **Save** le nouveau classeur (`Destination.xlsx`).  

Voilà—six étapes, aucune magie. Chaque étape est expliquée ci‑dessous avec des extraits de code et le raisonnement qui les sous-tend.

---

## Étape 1 – Charger le classeur source

Première chose à faire : vous avez besoin d’une instance `Workbook` pointant vers le fichier que vous voulez dupliquer. Cette étape est essentielle car Aspose.Cells travaille directement avec le système de fichiers, pas avec l’interface Office.

```csharp
using Aspose.Cells;

// Path to the original file
string sourcePath = "YOUR_DIRECTORY/Source.xlsx";
string destinationPath = "YOUR_DIRECTORY/Destination.xlsx";

// Load the workbook – this is the starting point for how to copy worksheet
Workbook workbook = new Workbook(sourcePath);
```

*Pourquoi c’est important :* Le chargement du fichier crée une représentation en mémoire de chaque feuille, cellule et objet. Sans cela, il n’y a rien à copier, et toute tentative d’utiliser le `add new worksheet code` plus tard échouerait parce que les données sources ne sont pas présentes.

---

## Étape 2 – Ajouter une nouvelle feuille (add new worksheet code)

Nous avons maintenant besoin d’un endroit où coller les données copiées. C’est là que le **add new worksheet code** entre en jeu. Vous pouvez nommer la feuille comme vous le souhaitez ; ici nous l’appelons `"Copy"`.

```csharp
// Grab the first worksheet (the one we want to copy)
Worksheet sourceSheet = workbook.Worksheets[0];

// Add a fresh worksheet to receive the copy
Worksheet copySheet = workbook.Worksheets.Add("Copy");
```

*Astuce :* Si vous prévoyez de copier plusieurs feuilles, appelez `Worksheets.Add` dans une boucle et attribuez à chaque feuille un nom unique. Ainsi vous évitez les collisions de noms et gardez votre classeur bien organisé.

---

## Étape 3 – Définir le copy cell range

Un **copy cell range** indique à Aspose.Cells exactement quelles lignes et colonnes dupliquer. Dans de nombreux scénarios réels, la plage comprend un tableau croisé dynamique, il faut donc être précis.

```csharp
// Define the area that contains the pivot table (A1:G20)
CellArea sourceRange = new CellArea
{
    StartRow = 0,      // Row 1 (zero‑based)
    StartColumn = 0,   // Column A
    EndRow = 19,       // Row 20
    EndColumn = 6      // Column G
};

// Destination range – we start at the same top‑left corner
CellArea destinationRange = new CellArea
{
    StartRow = 0,
    StartColumn = 0,
    EndRow = 19,
    EndColumn = 6
};
```

*Pourquoi nous en avons besoin :* En indiquant explicitement la plage, vous évitez de copier toute la feuille (ce qui peut être gourmand) et vous garantissez que le tableau croisé dynamique se trouve bien dans la zone copiée. C’est le cœur du **how to copy worksheet** lorsque vous ne devez copier qu’une partie de la feuille.

---

## Étape 4 – Configurer les options de copie (preserve copy worksheet pivot table)

Aspose.Cells propose un objet `CopyOptions` qui contrôle ce qui est collé. Pour conserver le tableau croisé dynamique, les graphiques et les formules, nous définissons `PasteType.All` et activons `PasteSpecial`.

```csharp
CopyOptions copyOptions = new CopyOptions
{
    PasteType = PasteType.All,   // Copy everything: values, formats, objects
    PasteSpecial = true          // Enable special paste to retain pivot tables
};
```

*Explication :* `PasteType.All` est l’option la plus inclusive, tandis que `PasteSpecial` indique au moteur de traiter correctement les objets complexes—comme les tableaux croisés dynamiques. Omettre cette étape est un piège fréquent ; la feuille copiée perdrait ses fonctionnalités interactives.

---

## Étape 5 – Copier les lignes et colonnes (copy columns between sheets)

Place au travail lourd : déplacer réellement les données. Nous utiliserons `CopyRows` et `CopyColumns` pour gérer le **copy columns between sheets**. Faire les deux garantit que les cellules fusionnées et les largeurs de colonnes sont préservées.

```csharp
// Copy rows from the source to the destination sheet
sourceSheet.Cells.CopyRows(
    sourceRange.StartRow,
    sourceRange.EndRow,
    copySheet.Cells,
    destinationRange.StartRow,
    copyOptions);

// Copy columns from the source to the destination sheet
sourceSheet.Cells.CopyColumns(
    sourceRange.StartColumn,
    sourceRange.EndColumn,
    copySheet.Cells,
    destinationRange.StartColumn,
    copyOptions);
```

*Ce qui se passe :* `CopyRows` déplace les données ligne par ligne, tandis que `CopyColumns` le fait colonne par colonne. Exécuter les deux assure que le bloc rectangulaire complet est dupliqué, ce qui est essentiel lorsque vous devez **copy columns between sheets** avec des largeurs de colonnes différentes ou des colonnes masquées.

---

## Étape 6 – Enregistrer le classeur

Enfin, écrivez les modifications sur le disque. Cette étape finalise le processus **how to copy worksheet**.

```csharp
// Save the workbook with the newly copied sheet
workbook.Save(destinationPath);
```

*Conseil de vérification :* Ouvrez `Destination.xlsx` et vérifiez que la feuille `"Copy"` est identique à l’originale, que les tableaux croisés dynamiques fonctionnent et que les largeurs de colonnes correspondent. Si quelque chose semble incorrect, revoyez les paramètres de `CopyOptions`.

---

## Cas particuliers et variantes courantes

### Copier plusieurs feuilles de calcul

Si vous devez dupliquer plusieurs feuilles, encapsulez la logique ci‑dessus dans une boucle `foreach` :

```csharp
foreach (Worksheet ws in workbook.Worksheets)
{
    Worksheet newWs = workbook.Worksheets.Add(ws.Name + "_Copy");
    // Re‑use sourceRange/destinationRange or calculate per sheet
    // Then call CopyRows/CopyColumns as shown earlier
}
```

### Préserver les formules entre différents classeurs

Lorsque les classeurs source et destination possèdent des plages nommées différentes, définissez `copyOptions` sur `PasteType.Formulas` en plus de `All` :

```csharp
copyOptions.PasteType = PasteType.All | PasteType.Formulas;
```

### Grandes plages et performances

Pour des jeux de données massifs (des centaines de milliers de lignes), envisagez d’utiliser uniquement `CopyRows` et d’ignorer `CopyColumns` si les largeurs de colonnes ne sont pas critiques. Cela peut faire gagner quelques secondes.

---

## Exemple complet fonctionnel

Voici le programme complet, prêt à être exécuté, qui regroupe tout ce dont nous avons parlé. Collez‑le dans une application console, ajustez les chemins de fichiers, puis appuyez sur **F5**.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // ---------- Step 1: Load the source workbook ----------
        string sourcePath = "YOUR_DIRECTORY/Source.xlsx";
        string destinationPath = "YOUR_DIRECTORY/Destination.xlsx";
        Workbook workbook = new Workbook(sourcePath);

        // ---------- Step 2: Add a new worksheet (add new worksheet code) ----------
        Worksheet sourceSheet = workbook.Worksheets[0];
        Worksheet copySheet = workbook.Worksheets.Add("Copy");

        // ---------- Step 3: Define the copy cell range ----------
        CellArea sourceRange = new CellArea
        {
            StartRow = 0,
            StartColumn = 0,
            EndRow = 19,
            EndColumn = 6
        };
        CellArea destinationRange = new CellArea
        {
            StartRow = 0,
            StartColumn = 0,
            EndRow = 19,
            EndColumn = 6
        };

        // ---------- Step 4: Set copy options (preserve copy worksheet pivot table) ----------
        CopyOptions copyOptions = new CopyOptions
        {
            PasteType = PasteType.All,
            PasteSpecial = true
        };

        // ---------- Step 5: Copy rows and columns (copy columns between sheets) ----------
        sourceSheet.Cells.CopyRows(
            sourceRange.StartRow,
            sourceRange.EndRow,
            copySheet.Cells,
            destinationRange.StartRow,
            copyOptions);

        sourceSheet.Cells.CopyColumns(
            sourceRange.StartColumn,
            sourceRange.EndColumn,
            copySheet.Cells,
            destinationRange.StartColumn,
            copyOptions);

        // ---------- Step 6: Save the workbook ----------
        workbook.Save(destinationPath);
    }
}
```

**Résultat attendu :** L’ouverture de `Destination.xlsx` montre une feuille nommée **Copy** qui reflète la première feuille de `Source.xlsx`—y compris les tableaux croisés dynamiques, le formatage et les largeurs de colonnes. Le fichier original reste intact.

---

## Questions fréquentes

**Q : Cela fonctionne-t-il avec des fichiers .xlsx créés par Excel 2019 ?**  
R : Absolument. Aspose.Cells prend en charge tous les formats Excel modernes, donc le même code fonctionne pour `.xlsx`, `.xlsm`, et même les anciens fichiers `.xls`.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}