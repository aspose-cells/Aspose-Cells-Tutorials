---
category: general
date: 2026-03-18
description: Extraire la date d’Excel et afficher la date au format ISO yyyy‑mm‑dd.
  Apprenez à lire les dates du calendrier japonais, à les convertir et à afficher
  les dates ISO en C#.
draft: false
keywords:
- extract date from excel
- output date yyyy-mm-dd
- display date iso format
language: fr
og_description: Extraire la date d’Excel et afficher la date au format ISO yyyy‑mm‑dd.
  Tutoriel C# étape par étape avec le code complet et des explications.
og_title: Extraire une date depuis Excel – Afficher la date au format aaaa‑mm‑jj en
  C#
tags:
- C#
- Excel
- DateTime
- Aspose.Cells
title: Extraire la date d’Excel et afficher la date au format yyyy‑mm‑dd – Guide complet
  C#
url: /fr/net/data-loading-and-parsing/extract-date-from-excel-and-output-date-yyyy-mm-dd-complete/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extraire une date d'Excel – Comment afficher la date au format yyyy‑mm‑dd en ISO

Vous avez déjà eu besoin d'**extraire une date d'Excel** mais vous ne saviez pas comment gérer les dates d'ère japonaise ou obtenir une chaîne `yyyy‑mm‑dd` propre ? Vous n'êtes pas seul. Dans de nombreux projets de migration de données, le classeur source stocke les dates en utilisant le calendrier de l'Empereur japonais, et le système en aval attend une date conforme à l'ISO comme `2024-04-01`.  

Dans ce guide, nous parcourrons une solution complète et exécutable qui lit une cellule, interprète l'ère japonaise, et **affiche la date yyyy‑mm‑dd**. À la fin, vous saurez exactement comment **afficher la date au format ISO** dans n'importe quelle application .NET, et vous disposerez d'un extrait de code réutilisable que vous pourrez intégrer à votre propre projet.

## Ce dont vous avez besoin

- **.NET 6+** (or .NET Framework 4.7.2+).  
- **Aspose.Cells for .NET** – la bibliothèque qui nous permet de définir un calendrier personnalisé lors du chargement d'un classeur.  
- Un fichier Excel (`japan-date.xlsx`) contenant une date stockée dans une cellule d'ère japonaise (par ex. `令和3年4月1日`).  
- Un IDE préféré – Visual Studio, Rider, ou même VS Code conviendra.

Aucun package NuGet supplémentaire n'est requis au-delà d'Aspose.Cells, et le code fonctionne sous Windows, Linux ou macOS.

## Étape 1 : Configurer le projet et installer Aspose.Cells

```bash
dotnet new console -n ExcelDateDemo
cd ExcelDateDemo
dotnet add package Aspose.Cells
```

> **Conseil pro :** Si vous êtes sur un serveur CI, épinglez la version du package (`Aspose.Cells 23.12`) pour garantir des builds reproductibles.

## Étape 2 : Charger le classeur avec le calendrier de l'Empereur japonais

La clé pour **extraire une date d'Excel** lorsque la source utilise un calendrier non grégorien est d'indiquer à Aspose.Cells quel calendrier appliquer lors du chargement. Nous le faisons avec `LoadOptions.Calendar`.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 2: Create load options and set the Japanese Emperor calendar
        LoadOptions loadOptions = new LoadOptions
        {
            // This tells Aspose.Cells to interpret era dates correctly
            Calendar = new JapaneseEmperorCalendar()
        };

        // Step 3: Open the workbook that contains Japanese era dates
        // Replace the path with the actual location of your Excel file
        string filePath = @"YOUR_DIRECTORY\japan-date.xlsx";
        Workbook workbook = new Workbook(filePath, loadOptions);
```

**Pourquoi c'est important :** Sans le calendrier personnalisé, Aspose.Cells traiterait la cellule comme une simple chaîne, et vous perdriez l'information d'ère. En assignant `JapaneseEmperorCalendar`, la bibliothèque convertit automatiquement `令和3年4月1日` en `2021‑04‑01` en arrière-plan.

## Étape 3 : Récupérer la date d'une cellule spécifique

Maintenant que le classeur sait comment interpréter l'ère, nous pouvons lire la cellule en tant que `DateTime`. Supposons que la date se trouve dans la première feuille de calcul, cellule **A1** (ligne 0, colonne 0).

```csharp
        // Step 4: Retrieve the date value from the first worksheet, first cell
        Worksheet sheet = workbook.Worksheets[0];
        Cell dateCell = sheet.Cells[0, 0]; // A1

        // GetDateTime() returns a System.DateTime object
        DateTime extractedDate = dateCell.GetDateTime();
```

Si la cellule est vide ou contient une valeur non date, `GetDateTime()` lèvera une exception. Une approche défensive ressemble à ceci :

```csharp
        if (dateCell.Type != CellValueType.IsDateTime)
        {
            Console.WriteLine("The target cell does not contain a valid date.");
            return;
        }

        DateTime extractedDate = dateCell.GetDateTime();
```

**Cas particulier :** Certains anciens fichiers Excel stockent les dates sous forme de nombres (dates sérialisées). Aspose.Cells les gère automatiquement, mais vous devriez tout de même vérifier le type de cellule si vous attendez du contenu mixte.

## Étape 4 : Afficher la date yyyy‑mm‑dd (ISO) et vérifier

Avec le `DateTime` en main, le formater en **date au format yyyy‑mm‑dd** se fait en une seule ligne :

```csharp
        // Step 5: Output the date in ISO format (yyyy‑mm‑dd)
        string isoDate = extractedDate.ToString("yyyy-MM-dd");
        Console.WriteLine($"Extracted date (ISO): {isoDate}");
    }
}
```

Exécuter le programme avec un fichier contenant `令和3年4月1日` affichera :

```
Extracted date (ISO): 2021-04-01
```

C’est le **format d'affichage de date ISO** exact que de nombreuses API exigent.

## Exemple complet fonctionnel

En assemblant tous les éléments, voici le programme complet, prêt à copier‑coller :

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load the workbook with Japanese era support
        LoadOptions loadOptions = new LoadOptions
        {
            Calendar = new JapaneseEmperorCalendar()
        };

        string filePath = @"YOUR_DIRECTORY\japan-date.xlsx";
        Workbook workbook = new Workbook(filePath, loadOptions);

        // Access the cell that holds the date (A1)
        Worksheet sheet = workbook.Worksheets[0];
        Cell dateCell = sheet.Cells[0, 0];

        // Validate the cell contains a date
        if (dateCell.Type != CellValueType.IsDateTime)
        {
            Console.WriteLine("The target cell does not contain a valid date.");
            return;
        }

        // Extract the DateTime value
        DateTime extractedDate = dateCell.GetDateTime();

        // Convert to ISO format (yyyy‑mm‑dd)
        string isoDate = extractedDate.ToString("yyyy-MM-dd");
        Console.WriteLine($"Extracted date (ISO): {isoDate}");
    }
}
```

> **Note :** Remplacez `YOUR_DIRECTORY` par le dossier réel contenant `japan-date.xlsx`. Le code fonctionne avec n'importe quelle feuille et n'importe quelle cellule – il suffit d'ajuster les indices.

## Gestion d'autres calendriers (optionnel)

Si vous avez besoin un jour d'**extraire une date d'Excel** qui utilise le calendrier bouddhiste thaïlandais ou le calendrier hébreu, il suffit d'échanger l'instance du calendrier :

```csharp
loadOptions.Calendar = new ThaiBuddhistCalendar();   // for Thai dates
// or
loadOptions.Calendar = new HebrewCalendar();         // for Hebrew dates
```

Le reste de la logique reste inchangé, ce qui montre la flexibilité de l'approche.

## Pièges courants et comment les éviter

| Problème | Pourquoi cela se produit | Solution |
|----------|--------------------------|----------|
| `GetDateTime()` lève `InvalidCastException` | La cellule n'est pas une date (peut-être une chaîne) | Vérifiez `Cell.Type` avant d'appeler, ou utilisez `DateTime.TryParse` sur `Cell.StringValue`. |
| Année incorrecte après conversion | Classeur chargé sans définir `Calendar` | Toujours créer `LoadOptions` avec le calendrier approprié **avant** d'ouvrir le fichier. |
| La sortie ISO affiche la partie temps (`2021-04-01 00:00:00`) | Utilisation de `ToString()` sans spécifier de format | Utilisez le spécificateur de format `"yyyy-MM-dd"` pour forcer **la date au format yyyy‑mm‑dd**. |
| Fichier non trouvé | Le chemin relatif pointe vers le mauvais dossier | Utilisez `Path.Combine(Environment.CurrentDirectory, "japan-date.xlsx")` ou fournissez un chemin absolu. |

## Conseils pro pour un code prêt pour la production

1. **Mettez en cache le classeur** si vous devez lire de nombreuses dates depuis le même fichier – l'ouverture d'un classeur est relativement coûteuse.  
2. **Encapsulez la logique d'extraction** dans une méthode réutilisable :

   ```csharp
   static string ExtractIsoDate(string file, int sheetIdx, int row, int col)
   {
       var opts = new LoadOptions { Calendar = new JapaneseEmperorCalendar() };
       var wb = new Workbook(file, opts);
       var cell = wb.Worksheets[sheetIdx].Cells[row, col];
       if (cell.Type != CellValueType.IsDateTime) return null;
       return cell.GetDateTime().ToString("yyyy-MM-dd");
   }
   ```

3. **Enregistrez la chaîne d'ère originale** (`cell.StringValue`) à côté de la sortie ISO pour les traces d'audit.  
4. **Testez unitairement** la méthode avec quelques fichiers Excel codés en dur couvrant différentes ères (Heisei, Reiwa) pour garantir la justesse.

## Vue d'ensemble visuelle

Below is a quick diagram illustrating the data flow—from Excel cell to ISO string.  

![Exemple d'extraction de date depuis Excel montrant Excel → LoadOptions → DateTime → chaîne ISO]  

*Alt text: “extraction de date depuis excel” diagramme affichant le pipeline de conversion.*

## Conclusion

Nous avons couvert tout ce dont vous avez besoin pour **extraire une date d'Excel**, gérer les valeurs d'ère japonaise, et **afficher la date yyyy‑mm‑dd** afin qu'elle corresponde au **format d'affichage de date ISO** apprécié par les API modernes. La solution est autonome, fonctionne avec n'importe quelle version .NET supportant Aspose.Cells, et peut être étendue à d'autres calendriers avec une simple modification d'une ligne.

Vous avez un autre calendrier en tête ? Ou peut-être récupérez‑vous des dates de plusieurs colonnes ? N'hésitez pas à ajuster la fonction d'aide `ExtractIsoDate` ou à laisser un commentaire ci‑dessous. Bon codage, et que vos dates restent toujours parfaitement synchronisées au format ISO !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}