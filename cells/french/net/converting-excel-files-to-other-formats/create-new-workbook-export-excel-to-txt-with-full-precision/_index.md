---
category: general
date: 2026-03-18
description: Créer un nouveau classeur et exporter Excel en TXT tout en préservant
  la précision numérique. Apprenez à enregistrer une feuille de calcul au format txt
  et à convertir une feuille de calcul en txt efficacement.
draft: false
keywords:
- create new workbook
- export excel to txt
- save excel as txt
- save worksheet as txt
- convert worksheet to txt
language: fr
og_description: Créer un nouveau classeur et exporter Excel en TXT avec précision.
  Ce tutoriel montre comment enregistrer une feuille de calcul au format TXT et convertir
  une feuille de calcul en TXT en utilisant C#.
og_title: Créer un nouveau classeur – Guide d’exportation d’Excel vers TXT
tags:
- Aspose.Cells
- C#
- Excel automation
title: Créer un nouveau classeur – Exporter Excel en TXT avec pleine précision
url: /fr/net/converting-excel-files-to-other-formats/create-new-workbook-export-excel-to-txt-with-full-precision/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un nouveau classeur – Exporter Excel en TXT avec pleine précision

Vous avez déjà eu besoin de **create new workbook** en C# juste pour exporter des données dans un fichier texte ? Peut‑être que vous extrayez un rapport d’un système hérité et que l’outil en aval n’accepte qu’un flux `.txt`. Bonne nouvelle ? Vous n’avez pas à sacrifier la précision numérique, et vous n’avez certainement pas besoin de créer manuellement des chaînes CSV.

Dans ce guide, nous parcourrons l’ensemble du processus d’**export excel to txt**, en couvrant tout, de l’initialisation du classeur à la préservation des zéros finaux lorsque vous **save worksheet as txt**. À la fin, vous disposerez d’un extrait prêt à l’emploi que vous pourrez intégrer dans n’importe quel projet .NET—sans utilitaires supplémentaires.

## Ce dont vous avez besoin

- **ASP.NET/ .NET 6+** (le code fonctionne également sur .NET Framework 4.6+)  
- **Aspose.Cells for .NET** – la bibliothèque qui fournit les classes `Workbook`, `Worksheet` et `TxtSaveOptions`. Vous pouvez l’obtenir via NuGet avec `Install-Package Aspose.Cells`.  
- Une compréhension de base du C# (si vous êtes à l’aise avec les instructions `using`, vous êtes prêt).  

C’est tout—pas d’interopérabilité Excel, pas d’objets COM, et certainement pas de concaténation manuelle de chaînes.

---

## Étape 1 : Initialiser un nouveau classeur (Mot‑clé principal)

La première chose à faire est **create new workbook**. Considérez le classeur comme une toile vierge où vous collerez plus tard des nombres, du texte ou des formules.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToTxtDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Create a new workbook and get the first worksheet
            Workbook workbook = new Workbook();                 // <‑‑ creates new workbook
            Worksheet worksheet = workbook.Worksheets[0];       // first sheet (index 0)
```

> **Pourquoi c’est important :** Instancier `Workbook` sans charger de fichier vous donne une page blanche. Vous pouvez alors ajouter des données par programme, ce qui est parfait pour les scénarios d’**convert worksheet to txt** où vous n’avez pas de fichier `.xlsx` existant.

---

## Étape 2 : Remplir les cellules – Conserver les zéros finaux

Un piège courant lors de l’exportation de nombres en texte est la perte des zéros finaux (`123.45000` devient `123.45`). Si les systèmes en aval dépendent de champs à largeur fixe, cette perte peut tout casser.

```csharp
            // Step 2: Write a numeric value that contains trailing zeros
            // PutValue respects the data type; we’ll later tell the saver to keep precision.
            worksheet.Cells[0, 0].PutValue(123.45000);
```

> **Astuce :** `PutValue` déduit automatiquement le type de données. Si vous avez besoin d’une chaîne qui ressemble à un nombre, utilisez `PutValue("123.45000")` à la place.

---

## Étape 3 : Configurer les options d’enregistrement TXT – Préserver la précision numérique

C’est ici que la magie opère. En activant `PreserveNumericPrecision`, vous indiquez à Aspose.Cells d’écrire la valeur exacte que vous avez saisie, y compris les zéros finaux insignifiants.

```csharp
            // Step 3: Configure TXT save options to keep the original numeric precision
            TxtSaveOptions txtSaveOptions = new TxtSaveOptions(SaveFormat.Txt)
            {
                PreserveNumericPrecision = true   // retain all digits, even trailing zeros
            };
```

> **Pourquoi l’activer ?** Lorsque vous **save excel as txt**, le comportement par défaut supprime les décimales inutiles. Définir `PreserveNumericPrecision = true` garantit que la sortie reflète la valeur affichée dans la cellule, ce qui est crucial pour les rapports financiers ou les données scientifiques.

---

## Étape 4 : Enregistrer la feuille de calcul en TXT – L’export final

Nous allons maintenant réellement **save worksheet as txt**. Vous pouvez indiquer n’importe quel chemin où vous avez les droits d’écriture ; l’exemple utilise un dossier relatif nommé `output`.

```csharp
            // Step 4: Save the worksheet as a TXT file using the configured options
            string outputPath = "output/num-preserve.txt";
            worksheet.Save(outputPath, txtSaveOptions);

            Console.WriteLine($"File saved to {outputPath}");
        }
    }
}
```

> **Sortie attendue** (`num-preserve.txt`) :

```
123.45000
```

Remarquez que les zéros finaux sont conservés—exactement ce que vous avez demandé.

---

## Étape 5 : Vérifier le résultat – Contrôle rapide

Après l’exécution du programme, ouvrez `num-preserve.txt` dans n’importe quel éditeur de texte. Vous devriez voir la ligne unique `123.45000`. Si vous voyez `123.45` à la place, vérifiez que `PreserveNumericPrecision` est bien à `true` et que vous utilisez une version récente d’Aspose.Cells (v23.10+).

---

## Variations courantes et cas limites

### Exporter plusieurs cellules ou plages

Si vous devez **export excel to txt** pour une plage entière, remplissez simplement plus de cellules avant d’enregistrer :

```csharp
worksheet.Cells["A1"].PutValue(100);
worksheet.Cells["A2"].PutValue(200.500);
worksheet.Cells["A3"].PutValue(300.00);
```

Aspose écrira chaque cellule sur une nouvelle ligne par défaut. Vous pouvez également modifier le séparateur (tabulation, virgule) via `txtSaveOptions.Separator`.

### Convertir la feuille de calcul en TXT avec différents encodages

Parfois, les systèmes en aval nécessitent UTF‑8 BOM ou ASCII. Ajustez l’encodage ainsi :

```csharp
txtSaveOptions.Encoding = System.Text.Encoding.UTF8;
```

### Gérer les classeurs volumineux

Lorsque vous traitez des feuilles massives (des centaines de milliers de lignes), envisagez de diffuser la sortie :

```csharp
txtSaveOptions.EnableCache = true; // writes data in chunks to reduce memory footprint
```

---

## Astuces pro & pièges

- **N’oubliez pas de créer le répertoire de sortie** avant d’appeler `Save`, sinon vous obtiendrez une `DirectoryNotFoundException`.  
- **Attention aux séparateurs décimaux spécifiques à la locale**. Si votre environnement utilise des virgules (`1,23`), définissez `txtSaveOptions.DecimalSeparator = '.'` pour imposer un point.  
- **Compatibilité des versions** : le drapeau `PreserveNumericPrecision` a été introduit dans Aspose.Cells 20.6. Si vous utilisez une version antérieure, le drapeau n’existe pas et vous devrez formater la cellule en texte avant d’enregistrer.

![Exemple de création d'un nouveau classeur](excel-to-txt.png "Créer un nouveau classeur")

*Texte alternatif de l’image : « Créer un nouveau classeur et exporter Excel en TXT avec la précision numérique préservée »*

---

## Récapitulatif – Ce que nous avons couvert

- **Create new workbook** avec Aspose.Cells.  
- Remplir une cellule avec un nombre incluant des zéros finaux.  
- Définir `TxtSaveOptions.PreserveNumericPrecision = true` pour **save excel as txt** sans perdre de précision.  
- Écrire le fichier sur le disque, en vérifiant que la sortie correspond à la valeur originale.  

C’est le flux complet de **convert worksheet to txt** en moins de 50 lignes de C#.

---

## Prochaines étapes et sujets associés

Maintenant que vous pouvez **export excel to txt** avec une précision parfaite, vous pourriez vouloir explorer :

- **Exporter en CSV** avec des délimiteurs personnalisés (`TxtSaveOptions.Separator`).  
- **Enregistrer sous d’autres formats texte** comme TSV (`SaveFormat.TabDelimited`).  
- **Traitement par lots** de plusieurs classeurs dans un dossier en utilisant `Directory.GetFiles`.  
- **Intégrer avec Azure Functions** pour la conversion à la demande dans le cloud.  

Chacune de ces options repose sur le même schéma `Workbook` → `Worksheet` → `TxtSaveOptions`, vous vous sentirez donc immédiatement à l’aise.

### Réflexion finale

Si vous avez suivi, vous savez maintenant exactement comment **create new workbook**, le remplir, et **save worksheet as txt** tout en conservant chaque chiffre décimal qui vous importe. C’est un petit morceau de code, mais il résout un problème étonnamment fréquent lorsque les pipelines hérités exigent des entrées texte.

Essayez-le, ajustez les options, et laissez les données circuler exactement comme vous le souhaitez. Bon codage !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}