---
category: general
date: 2026-02-21
description: Enregistrez Excel au format txt avec un contrôle précis des chiffres
  significatifs. Exportez Excel en txt avec C# et définissez facilement les chiffres
  significatifs.
draft: false
keywords:
- save excel as txt
- export excel to txt
- set significant digits
- save workbook as text
- export numbers to txt
language: fr
og_description: Enregistrez rapidement Excel au format txt. Apprenez à exporter Excel
  en txt, à définir le nombre de chiffres significatifs et à contrôler la sortie texte
  avec C#.
og_title: Enregistrer Excel au format txt – Exporter les nombres avec chiffres significatifs
  en C#
tags:
- C#
- Aspose.Cells
- Excel automation
title: Enregistrer Excel au format txt – Guide complet C# pour exporter les nombres
  avec chiffres significatifs
url: /fr/net/converting-excel-files-to-other-formats/save-excel-as-txt-complete-c-guide-to-export-numbers-with-si/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Enregistrer Excel en txt – Guide complet C# pour exporter les nombres avec chiffres significatifs

Vous avez déjà eu besoin d’**enregistrer Excel en txt** mais vous craigniez que les nombres perdent leur précision ? Vous n’êtes pas seul. De nombreux développeurs se heurtent à un mur lorsqu’ils essaient d’exporter Excel en txt et se retrouvent avec soit trop de décimales, soit un arrondi désordonné.  

Dans ce tutoriel, nous vous montrons une méthode simple pour **exporter Excel en txt** tout en **définissant les chiffres significatifs** afin que le résultat ressemble exactement à ce que vous souhaitez. À la fin, vous disposerez d’un extrait C# prêt à l’emploi qui enregistre un classeur au format texte, exporte les nombres en txt, et vous donne un contrôle total sur le format numérique.

## Ce que vous allez apprendre

- Comment créer un nouveau classeur et écrire des données numériques.  
- La bonne façon de **définir les chiffres significatifs** avec `TxtSaveOptions`.  
- Comment **enregistrer le classeur en texte** et vérifier le résultat.  
- Gestion des cas limites (grands nombres, valeurs négatives, problèmes de locale).  
- Astuces rapides pour affiner davantage la sortie (changement de délimiteur, encodage).

### Prérequis

- .NET 6.0 ou supérieur (le code fonctionne également avec .NET Framework 4.6+).  
- Le package NuGet **Aspose.Cells** (`Install-Package Aspose.Cells`).  
- Une compréhension de base de la syntaxe C# — aucune connaissance approfondie d’Excel interop n’est requise.

> **Pro tip :** Si vous utilisez Visual Studio, activez les *nullable reference types* (`<Nullable>enable</Nullable>`) pour détecter les éventuels bugs de null tôt.

---

## Étape 1 : Initialiser le classeur et écrire un nombre

Tout d’abord, nous avons besoin d’un objet classeur. Pensez‑y comme à la représentation en mémoire d’un fichier Excel.  

```csharp
using Aspose.Cells;
using System;

// Create a new workbook (starts with one worksheet by default)
var workbook = new Workbook();
var worksheet = workbook.Worksheets[0];

// Write a numeric value into cell A1 (row 0, column 0)
worksheet.Cells[0, 0].PutValue(12345.6789);
```

**Pourquoi c’est important :**  
Créer le classeur programmatique évite la surcharge de l’interop COM, et `PutValue` détecte automatiquement le type de donnée, garantissant que la cellule est traitée comme un nombre — pas une chaîne.

---

## Étape 2 : Configurer TxtSaveOptions pour contrôler les chiffres significatifs

La classe `TxtSaveOptions` est l’endroit où la magie opère. En définissant `SignificantDigits`, vous indiquez à Aspose.Cells combien de chiffres significatifs conserver lors de l’écriture du fichier.

```csharp
// Configure text save options – keep only 4 significant digits
var txtSaveOptions = new TxtSaveOptions
{
    // 4 significant digits means 12345.6789 becomes 12350
    SignificantDigits = 4,

    // Optional: change delimiter if you need CSV‑style output
    // Delimiter = ',',

    // Optional: force UTF‑8 encoding for broader character support
    // Encoding = System.Text.Encoding.UTF8
};
```

**Pourquoi vous devez le définir :**  
Lorsque vous **exportez des nombres en txt**, il faut souvent une représentation concise (par ex. pour des systèmes de reporting qui n’acceptent qu’une certaine précision). La propriété `SignificantDigits` garantit un arrondi cohérent quel que soit la longueur du nombre d’origine.

---

## Étape 3 : Enregistrer le classeur en fichier texte

Nous écrivons maintenant le classeur sur le disque en utilisant les options que nous venons de définir.

```csharp
// Define the output path – adjust to your environment
string outputPath = @"C:\Temp\Numbers.txt";

// Save the workbook as a .txt file with the configured options
workbook.Save(outputPath, txtSaveOptions);

Console.WriteLine($"Workbook saved as txt at: {outputPath}");
```

**Ce que vous verrez :**  
Ouvrez `Numbers.txt` et vous obtiendrez une seule ligne :

```
12350
```

Le `12345.6789` d’origine a été arrondi à **quatre chiffres significatifs**, exactement comme demandé.

---

## Étape 4 : Vérifier la sortie (optionnel mais recommandé)

Les tests automatisés sont une bonne habitude. Voici une vérification rapide que vous pouvez exécuter juste après l’enregistrement :

```csharp
// Read back the file to confirm the content
string fileContent = System.IO.File.ReadAllText(outputPath).Trim();

if (fileContent == "12350")
{
    Console.WriteLine("✅ Export succeeded – significant digits applied correctly.");
}
else
{
    Console.WriteLine($"⚠️ Unexpected output: {fileContent}");
}
```

L’exécution de ce bloc affichera une coche verte si tout correspond, vous donnant la confiance que l’opération **save excel as txt** s’est déroulée comme prévu.

---

## Variations courantes & cas limites

### Exporter plusieurs cellules ou plages

Si vous devez **exporter excel en txt** pour une plage entière, remplissez simplement plus de cellules avant d’enregistrer :

```csharp
worksheet.Cells[0, 1].PutValue(0.000123456);
worksheet.Cells[0, 2].PutValue(-98765.4321);
```

Les mêmes `TxtSaveOptions` appliqueront la règle des 4 chiffres à chaque valeur, produisant :

```
12350
0.0001235
-98800
```

### Modifier le délimiteur

Certains systèmes en aval attendent des valeurs séparées par des tabulations. Ajustez le délimiteur ainsi :

```csharp
txtSaveOptions.Delimiter = '\t'; // Tab character
```

Chaque cellule d’une ligne apparaît maintenant séparée par une tabulation.

### Gérer les séparateurs décimaux spécifiques à une locale

Si votre audience utilise des virgules pour les décimales, définissez la culture :

```csharp
txtSaveOptions.CultureInfo = new System.Globalization.CultureInfo("fr-FR");
```

La sortie respectera la locale, transformant `12350` en `12 350` (espace comme séparateur de milliers en français).

---

## Exemple complet fonctionnel (prêt à copier‑coller)

```csharp
using Aspose.Cells;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook and write numbers
        var workbook = new Workbook();
        var sheet = workbook.Worksheets[0];
        sheet.Cells[0, 0].PutValue(12345.6789);
        sheet.Cells[0, 1].PutValue(0.000123456);
        sheet.Cells[0, 2].PutValue(-98765.4321);

        // 2️⃣ Configure save options – 4 significant digits
        var txtOptions = new TxtSaveOptions
        {
            SignificantDigits = 4,
            // Delimiter = '\t',               // Uncomment for TSV
            // Encoding = System.Text.Encoding.UTF8,
            // CultureInfo = new System.Globalization.CultureInfo("en-US")
        };

        // 3️⃣ Save to text file
        string path = Path.Combine(Environment.GetFolderPath(Environment.SpecialFolder.Desktop), "Numbers.txt");
        workbook.Save(path, txtOptions);
        Console.WriteLine($"File saved to {path}");

        // 4️⃣ Verify result (optional)
        string result = File.ReadAllText(path).Trim();
        Console.WriteLine($"File content: {result}");
    }
}
```

**Contenu attendu de `Numbers.txt` (délimiteur par défaut, 4 chiffres significatifs) :**

```
12350	0.0001235	-98800
```

La tabulation (`\t`) apparaît parce que nous avons laissé le délimiteur à sa valeur par défaut (tab) dans l’exemple ; changez‑le en virgule si vous préférez le CSV.

---

## Conclusion

Vous savez maintenant exactement **comment enregistrer Excel en txt** tout en contrôlant le nombre de chiffres significatifs. Les étapes — créer un classeur, définir `TxtSaveOptions.SignificantDigits`, et enregistrer — sont tout ce qu’il faut pour **exporter excel en txt** de façon fiable.  

À partir d’ici, vous pouvez :

- **Exporter des nombres en txt** pour des ensembles de données plus volumineux.  
- Ajuster les délimiteurs, l’encodage ou les paramètres de culture pour correspondre à n’importe quel système en aval.  
- Combiner cette approche avec d’autres fonctionnalités d’Aspose.Cells (styles, formules) avant l’export.

Essayez, modifiez `SignificantDigits` à 2 ou 6, et observez comment la sortie change. La flexibilité de **save workbook as text** en fait un outil pratique dans tout pipeline d’échange de données.

---

### Sujets connexes que vous pourriez explorer ensuite

- **Export Excel to CSV** avec ordre de colonnes personnalisé.  
- **Read txt files back into a workbook** (`Workbook.Load` avec `LoadOptions`).  
- **Batch processing** de plusieurs feuilles de calcul et consolidation en un seul fichier txt.  
- **Performance tuning** pour les exportations à grande échelle (streaming vs. en‑mémoire).

N’hésitez pas à laisser un commentaire si vous rencontrez des difficultés, ou à partager comment vous avez personnalisé l’export pour vos propres projets. Bon codage !  

---  

*Image : Une capture d’écran du fichier `Numbers.txt` généré montrant les valeurs arrondies.*  
*Texte alternatif : “Fichier Numbers.txt affichant 12350, 0,0001235 et -98800 après avoir enregistré Excel en txt avec 4 chiffres significatifs.”*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}