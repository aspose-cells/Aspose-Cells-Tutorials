---
category: general
date: 2026-03-01
description: Comment créer rapidement un classeur en C# — apprenez à écrire une valeur
  dans une cellule, à définir le format numérique d’une cellule et à formater le nombre
  d’une cellule en quelques étapes simples.
draft: false
keywords:
- how to create workbook
- write value to cell
- format cell number
- set cell number format
- how to write cell
language: fr
og_description: Comment créer un classeur en C# ? Ce guide vous montre comment écrire
  une valeur dans une cellule, définir le format numérique d’une cellule et formater
  le nombre d’une cellule en quelques lignes de code seulement.
og_title: Comment créer un classeur en C# – Écrire une valeur et formater un nombre
tags:
- C#
- Aspose.Cells
- Excel Automation
title: Comment créer un classeur en C# – Écrire une valeur et formater un nombre
url: /fr/net/excel-workbook/how-to-create-workbook-in-c-write-value-format-number/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment créer un Workbook en C# – Écrire une valeur et formater un nombre

Créer un workbook en C# est une tâche courante lorsque vous devez générer des fichiers Excel à la volée. Dans ce guide, nous vous montrerons comment écrire une valeur dans une cellule et formater le nombre d’une cellule afin que la feuille finale soit soignée.

Si vous avez déjà fixé votre regard sur une feuille de calcul vierge et vous êtes demandé pourquoi les nombres affichent trop de décimales, vous n’êtes pas seul. Nous couvrirons tout, depuis l’initialisation de l’objet workbook jusqu’à la définition d’un format de nombre personnalisé, et nous ajouterons quelques astuces pour les cas particuliers que vous pourriez rencontrer plus tard.

## Ce que vous apprendrez

- **Initialiser** une nouvelle instance de `Workbook`.  
- **Écrire une valeur dans une cellule** en utilisant la méthode `PutValue`.  
- **Définir le format de nombre d’une cellule** avec un objet `Style`, obtenant ainsi un affichage propre à deux décimales.  
- Vérifier le résultat en lisant la cellule ou en ouvrant le fichier dans Excel.  

Aucune bibliothèque externe au-delà de l’Aspose.Cells standard (ou toute API similaire) n’est requise, et le code fonctionne sur .NET 6+ sans configuration supplémentaire.

---

## Créer un Workbook – Initialiser l’objet

Tout d’abord : vous avez besoin d’un objet workbook pour contenir vos feuilles. Pensez au `Workbook` comme au fichier Excel complet, tandis que chaque `Worksheet` représente un onglet unique.

```csharp
// Step 1: Create a new workbook instance
Workbook workbook = new Workbook();
```

*Pourquoi c’est important :* Créer le workbook alloue les structures internes qui contiendront plus tard les lignes, colonnes et formats. Sans cet objet, il n’y a nulle part où écrire une valeur dans une cellule.

> **Astuce :** Si vous prévoyez de travailler avec un fichier existant, remplacez `new Workbook()` par `new Workbook("template.xlsx")` pour charger un modèle et conserver ses styles.

## Écrire une valeur dans une cellule

Maintenant que nous avons un workbook, insérons un nombre dans la cellule **A1** de la première feuille.

```csharp
// Step 2: Access cell A1 in the first worksheet
Cell cellA1 = workbook.Worksheets[0].Cells["A1"];

// Step 3: Insert a numeric value into the cell
cellA1.PutValue(123.456789);
```

*Pourquoi nous utilisons `PutValue`* : Cette méthode détecte automatiquement le type de données, vous n’avez donc pas besoin de caster ou de convertir manuellement. Elle respecte également le style existant de la cellule, ce qui est pratique lorsque vous **définissez le format de nombre d’une cellule** plus tard.

### Vérification rapide

Si vous lisez la cellule, vous verrez la valeur brute :

```csharp
double raw = cellA1.DoubleValue; // raw == 123.456789
```

C’est le nombre avant l’application de tout format.

## Définir le format de nombre d’une cellule

Afficher un double brut avec de nombreuses décimales n’est pas toujours convivial. Limitons‑le à deux chiffres significatifs.

```csharp
// Step 4: Apply a style that formats the number with two significant digits
cellA1.SetStyle(new Style() { Number = 2 });
```

La propriété `Number` correspond aux identifiants de formats numériques intégrés d’Excel. `2` signifie « Nombre avec deux décimales ». Si vous avez besoin d’un format différent—par exemple monnaie ou date—vous utiliserez un autre ID ou une chaîne de format personnalisée.

### Alternative : Chaîne de format personnalisée

```csharp
Style customStyle = workbook.CreateStyle();
customStyle.Custom = "#,##0.00"; // forces two decimals with thousand separator
cellA1.SetStyle(customStyle);
```

*Pourquoi choisir un style personnalisé ?* Il vous donne un contrôle total, surtout lorsque les ID intégrés ne couvrent pas vos paramètres régionaux.

## Vérifier la sortie (Optionnel mais recommandé)

Après avoir appliqué le style, vous pouvez enregistrer le workbook et l’ouvrir dans Excel pour confirmer l’apparence.

```csharp
// Save the workbook to a file
workbook.Save("FormattedWorkbook.xlsx");

// Or, for quick verification in code:
string displayed = cellA1.StringValue; // "123.46"
Console.WriteLine($"Displayed value: {displayed}");
```

Vous devriez voir **123.46** dans la cellule A1—exactement deux décimales, grâce au format que nous avons défini.

---

### Exemple complet fonctionnel

En combinant le tout, voici un programme autonome que vous pouvez copier‑coller dans une application console.

```csharp
using System;
using Aspose.Cells;   // Ensure you have the Aspose.Cells NuGet package

class Program
{
    static void Main()
    {
        // Initialize the workbook
        Workbook workbook = new Workbook();

        // Access the first worksheet and cell A1
        Cell cellA1 = workbook.Worksheets[0].Cells["A1"];

        // Write a numeric value
        cellA1.PutValue(123.456789);

        // Apply a two‑decimal number format
        cellA1.SetStyle(new Style() { Number = 2 });

        // Save to disk (optional)
        workbook.Save("FormattedWorkbook.xlsx");

        // Output the displayed text for verification
        Console.WriteLine($"Cell A1 shows: {cellA1.StringValue}");
    }
}
```

**Sortie attendue lors de l’exécution du programme :**

```
Cell A1 shows: 123.46
```

Ouvrez `FormattedWorkbook.xlsx` dans Excel et vous verrez la même valeur formatée.

---

## Variations courantes & cas particuliers

### 1. Différents formats de nombre

| Objectif | ID de format | Extrait de code |
|----------|--------------|-----------------|
| Devise (deux décimales) | 5 | `cellA1.SetStyle(new Style() { Number = 5 });` |
| Pourcentage (sans décimales) | 10 | `cellA1.SetStyle(new Style() { Number = 10 });` |
| Notation scientifique | 11 | `cellA1.SetStyle(new Style() { Number = 11 });` |

Si aucun des ID intégrés ne convient, revenez à une chaîne personnalisée comme indiqué précédemment.

### 2. Séparateurs décimaux spécifiques à la culture

Certaines locales utilisent des virgules pour les décimales. Vous pouvez imposer un format sensible à la culture :

```csharp
Style cultureStyle = workbook.CreateStyle();
cultureStyle.Custom = "#,##0.00"; // works for most European locales
cellA1.SetStyle(cultureStyle);
```

### 3. Écrire du texte au lieu de nombres

Lorsque vous devez **how to write cell** avec une chaîne, passez simplement une chaîne à `PutValue` :

```csharp
cellA1.PutValue("Total Revenue");
```

Aucun format de nombre n’est requis, mais vous pouvez toujours appliquer un style de police.

### 4. Grands ensembles de données

Si vous remplissez des milliers de lignes, l’insertion par lot (`Cells.ImportArray`) est plus rapide que de boucler avec `PutValue`. L’approche de formatage reste la même ; il suffit d’appliquer le style à une plage :

```csharp
Range range = workbook.Worksheets[0].Cells.CreateRange("B2:B1001");
range.ApplyStyle(new Style() { Number = 2 });
```

---

## Foire aux questions

**Q : Cela fonctionne-t-il avec .NET Core ?**  
R : Absolument. Aspose.Cells prend en charge .NET Standard 2.0 et versions ultérieures, vous pouvez donc cibler .NET 5, .NET 6 ou .NET 7 sans modifications.

**Q : Et si j’ai besoin de plus de deux décimales ?**  
R : Modifiez la propriété `Number` avec l’ID intégré approprié (par ex., `3` pour trois décimales) ou ajustez la chaîne de format personnalisée (`"#,##0.000"`).

**Q : Puis‑je appliquer le format à une colonne entière d’un coup ?**  
R : Oui. Utilisez `Cells["A:A"]` pour obtenir toute la colonne, puis `SetStyle`.

---

## Conclusion

Vous savez maintenant **comment créer des workbook** en C#, **écrire une valeur dans une cellule**, et **définir le format de nombre d’une cellule** afin que les nombres apparaissent exactement comme vous le souhaitez. En maîtrisant ces bases, vous serez capable de générer des rapports Excel, factures ou exportations de données d’aspect professionnel avec un minimum d’effort.

Ensuite, vous pourrez explorer **format cell number** pour les dates, pourcentages ou le formatage conditionnel—chacun s’appuie sur les mêmes principes que nous avons couverts. Plongez dans la documentation d’Aspose.Cells pour des options de style plus avancées, ou essayez de combiner plusieurs feuilles de calcul en un seul workbook pour des rapports plus riches.

Happy coding, and remember: a well‑formatted spreadsheet is just

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}