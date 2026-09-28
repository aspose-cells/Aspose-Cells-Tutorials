---
category: general
date: 2026-02-15
description: Créer un nouveau classeur et exporter Excel en TXT tout en définissant
  la précision numérique. Apprenez à définir les chiffres significatifs et à limiter
  les chiffres significatifs en C#.
draft: false
keywords:
- create new workbook
- export excel to txt
- set significant digits
- limit significant digits
- set numeric precision
language: fr
og_description: Créer un nouveau classeur et exporter Excel en TXT, en définissant
  les chiffres significatifs pour la précision numérique. Un guide C# étape par étape.
og_title: Créer un nouveau classeur – Exporter Excel en TXT avec précision
tags:
- C#
- Aspose.Cells
- Excel automation
title: Créer un nouveau classeur et exporter Excel en TXT avec précision
url: /fr/net/excel-data-export-retrieval/create-new-workbook-and-export-excel-to-txt-with-precision/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un nouveau classeur – Exporter Excel vers TXT avec un format numérique précis

Vous êtes-vous déjà demandé comment **créer un nouveau classeur** en C# et le déposer immédiatement dans un fichier texte ? Vous n'êtes pas le seul. Dans de nombreux scénarios de pipelines de données, nous devons **exporter Excel vers TXT** tout en gardant les nombres lisibles, ce qui signifie limiter le nombre de chiffres après la virgule.  

Dans ce tutoriel, nous parcourrons l’ensemble du processus : de la création d’un classeur vierge, à la configuration de l’exportation pour **définir les chiffres significatifs** (c’est‑à‑dire limiter les chiffres significatifs), jusqu’à l’écriture du fichier sur le disque. À la fin, vous disposerez d’un extrait prêt à l’emploi qui respecte vos exigences de **précision numérique**—sans bibliothèques supplémentaires, sans magie.

> **Astuce :** Si vous utilisez déjà Aspose.Cells, les classes montrées ci‑dessous font partie de cette bibliothèque. Si vous êtes sur une autre plateforme, les concepts restent valables ; il suffit d’échanger les appels d’API.

---

## Ce dont vous avez besoin

- .NET 6+ (le code se compile aussi bien sur .NET Core que sur .NET Framework)  
- Aspose.Cells for .NET (version d’essai gratuite ou licence) – installer via NuGet : `dotnet add package Aspose.Cells`  
- L’IDE de votre choix (Visual Studio, Rider, VS Code)  

C’est tout. Aucun fichier de configuration supplémentaire, aucune étape cachée.

---

## Étape 1 : Créer un nouveau classeur

La toute première chose est de **créer un nouveau classeur**. Considérez la classe `Workbook` comme un fichier Excel vide qui attend des feuilles, des cellules et des données.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Instantiate a fresh workbook – this is the core of create new workbook logic
        Workbook workbook = new Workbook();

        // (Optional) Add some sample data so you can see the effect of numeric precision later
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].PutValue(12345.678901);
        sheet.Cells["A2"].PutValue(0.000123456);
        sheet.Cells["A3"].PutValue(Math.PI);
```

> **Pourquoi c’est important :** En partant d’un classeur vierge, vous évitez tout formatage caché qui pourrait interférer avec les réglages de précision plus tard.

---

## Étape 2 : Configurer les options d’enregistrement texte – Définir les chiffres significatifs

Nous indiquons maintenant à Aspose.Cells combien de **chiffres significatifs** nous voulons lors de l’écriture dans un fichier `.txt`. La classe `TxtSaveOptions` expose une propriété `SignificantDigits` qui **fait exactement cela**.

```csharp
        // Step 2: Prepare save options – limit numeric precision to 5 significant digits
        TxtSaveOptions txtOptions = new TxtSaveOptions
        {
            // This limits the output to 5 digits that matter, rounding the rest
            SignificantDigits = 5
        };
```

> **Explication :** `SignificantDigits = 5` signifie que l’exportateur conservera les cinq chiffres les plus importants de chaque nombre, quel que soit l’endroit où se trouve la virgule décimale. C’est une façon pratique de **définir la précision numérique** sans formater chaque cellule manuellement.

---

## Étape 3 : Enregistrer le classeur en fichier texte

Avec le classeur et les options prêts, nous **exportons enfin Excel vers txt**. La méthode `Save` prend le chemin du fichier et l’objet d’options que nous venons de configurer.

```csharp
        // Step 3: Write the workbook out as a TXT file using our precision settings
        string outputPath = @"C:\Temp\numbers.txt";
        workbook.Save(outputPath, txtOptions);

        System.Console.WriteLine($"Workbook exported to {outputPath} with 5 significant digits.");
    }
}
```

L’exécution du programme produit un fichier qui ressemble à ceci :

```
12346
0.00012346
3.1416
```

Remarquez comment chaque nombre respecte la règle de **limitation des chiffres significatifs** que nous avons définie précédemment.

---

## Étape 4 : Vérifier le résultat (optionnel mais recommandé)

Il est facile d’ouvrir le `numbers.txt` généré dans n’importe quel éditeur, mais vous pouvez vouloir automatiser l’étape de vérification, surtout dans des pipelines CI.

```csharp
        // Quick verification – read back the file and print each line
        foreach (var line in System.IO.File.ReadAllLines(outputPath))
        {
            System.Console.WriteLine($"Line: {line}");
        }
```

Si la console affiche les trois lignes ci‑dessus, vous avez **défini les chiffres significatifs** avec succès et l’exportation fonctionne comme prévu.

---

## Pièges courants & comment les éviter

| Problème | Pourquoi cela se produit | Solution |
|----------|--------------------------|----------|
| Les nombres apparaissent avec trop de décimales | `SignificantDigits` est resté à la valeur par défaut (0) | Définissez explicitement `SignificantDigits` au nombre souhaité |
| Un fichier vide est créé | Le classeur n’a jamais reçu de données avant l’enregistrement | Remplissez les cellules **avant** d’appeler `Save` |
| Le chemin du fichier lève `UnauthorizedAccessException` | Tentative d’écriture dans un dossier protégé | Utilisez un dossier où vous avez les droits d’écriture (ex. `C:\Temp` ou `%USERPROFILE%\Documents`) |
| La précision semble incorrecte pour des nombres très petits | Le compte des chiffres significatifs inclut les zéros précédant la virgule | Rappelez‑vous que “significatif” ignore les zéros initiaux ; 0.000123456 avec 5 chiffres devient `0.00012346` |

---

## Exemple complet fonctionnel (prêt à copier‑coller)

Voici le programme complet, autonome. Copiez‑le dans un nouveau projet console et cliquez sur **Run**.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook
        Workbook workbook = new Workbook();

        // Populate with sample numbers
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].PutValue(12345.678901);
        sheet.Cells["A2"].PutValue(0.000123456);
        sheet.Cells["A3"].PutValue(Math.PI);

        // 2️⃣ Set up export options – limit significant digits to 5
        TxtSaveOptions txtOptions = new TxtSaveOptions
        {
            SignificantDigits = 5
        };

        // 3️⃣ Export to TXT
        string outputPath = @"C:\Temp\numbers.txt";
        workbook.Save(outputPath, txtOptions);

        Console.WriteLine($"✅ Export completed: {outputPath}");
        Console.WriteLine("🔎 Verifying content:");
        foreach (var line in System.IO.File.ReadAllLines(outputPath))
        {
            Console.WriteLine($"   {line}");
        }
    }
}
```

**Sortie console attendue**

```
✅ Export completed: C:\Temp\numbers.txt
🔎 Verifying content:
   12346
   0.00012346
   3.1416
```

Et le fichier `numbers.txt` contiendra les trois lignes affichées ci‑dessus.

---

## Étapes suivantes : aller au-delà des bases

- **Exporter d’autres formats** – Aspose.Cells prend également en charge CSV, HTML et PDF. Remplacez `TxtSaveOptions` par `CsvSaveOptions` ou `PdfSaveOptions` selon vos besoins.  
- **Précision dynamique** – vous pouvez calculer `SignificantDigits` à l’exécution en fonction d’une entrée utilisateur ou d’un fichier de configuration.  
- **Multiples feuilles** – parcourez `workbook.Worksheets` et exportez chacune dans son propre fichier `.txt`.  
- **Localisation** – contrôlez le séparateur décimal (`.` vs `,`) via `CultureInfo` si vous devez respecter les paramètres régionaux.  

Toutes ces extensions reposent toujours sur l’idée centrale présentée : **créer un nouveau classeur**, configurer l’exportation, et **définir la précision numérique** pour répondre à vos exigences de reporting.

---

## Résumé

Nous avons pris une instance fraîche de **créer un nouveau classeur**, l’avons remplie de données, et montré comment **exporter Excel vers TXT** tout en **définissant les chiffres significatifs** afin de limiter la précision de sortie. L’exemple complet fonctionne immédiatement, et l’explication a couvert le *pourquoi* de chaque ligne afin que vous puissiez l’adapter à vos propres projets.

N’hésitez pas à expérimenter — modifiez la valeur de `SignificantDigits`, ajoutez d’autres feuilles, ou changez le format de sortie. En cas de problème, consultez la documentation d’Aspose.Cells ou laissez un commentaire ci‑dessous. Bon codage !

---

![Create new workbook example](/images/create-new-workbook.png "Screenshot showing a C# IDE with the create new workbook code")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}