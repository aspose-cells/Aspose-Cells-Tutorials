---
category: general
date: 2026-03-01
description: Le tutoriel C# de lecture/écriture Excel montre comment lire la valeur
  d’une cellule Excel et écrire une date/heure dans Excel en utilisant C# et Aspose.Cells
  en quelques étapes simples.
draft: false
keywords:
- read write excel c#
- read excel cell value
- write datetime to excel
- c# excel interop
- aspnet excel automation
language: fr
og_description: Tutoriel C# de lecture et écriture Excel explique comment lire la
  valeur d’une cellule Excel et écrire une date/heure dans Excel avec des exemples
  de code clairs et les meilleures pratiques.
og_title: Lire et écrire Excel C# – Guide étape par étape
tags:
- C#
- Excel
- Aspose.Cells
title: Lire et écrire Excel C# – Guide complet de la lecture et de l’écriture des
  cellules Excel
url: /fr/net/cell-operations/read-write-excel-c-complete-guide-to-reading-and-writing-exc/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Lire‑Écrire Excel C# – Guide complet pour lire et écrire des cellules Excel

Vous avez déjà essayé de **read write Excel C#** et vous êtes retrouvé avec une exception cryptique ou une date incohérente ? Vous n'êtes pas seul. De nombreux développeurs se heurtent lorsqu'ils doivent extraire une date d'ère japonaise d'une feuille de calcul puis enregistrer un `DateTime` correct dans la même cellule.  

Dans ce guide, nous verrons exactement comment **read excel cell value** et **write datetime to excel** en utilisant C# et la puissante bibliothèque Aspose.Cells. À la fin, vous disposerez d'un exemple autonome et exécutable que vous pourrez intégrer à n'importe quel projet .NET.

## Ce que vous allez apprendre

- Comment installer et référencer Aspose.Cells dans un projet .NET 6+.
- Le code exact nécessaire pour récupérer une cellule contenant une chaîne d'ère japonaise comme `"R3/5/12"`.
- Comment analyser cette chaîne en un `DateTime` en utilisant la culture `"ja-JP"`.
- Les étapes pour renvoyer le `DateTime` résultant dans la même cellule de la feuille de calcul.
- Conseils pour gérer les cas limites tels que les cellules vides ou les formats d'ère inattendus.  

Aucune expérience préalable avec l'interopérabilité Excel n'est requise—juste une compréhension de base de C# et .NET. Commençons.

![Capture d'écran de l'opération read write Excel C# montrant la cellule B2 avant et après conversion](read-write-excel-csharp.png "exemple read write excel c#")

## Étape 1 : Configurer le projet – Fondations de Read Write Excel C#

Avant de plonger dans le code, nous avons besoin d'une base solide.

1. **Create a new console app** (ou tout projet .NET) ciblant .NET 6 ou une version ultérieure :

   ```bash
   dotnet new console -n ExcelEraDemo
   cd ExcelEraDemo
   ```

2. **Add the Aspose.Cells NuGet package**. C’est une bibliothèque entièrement gérée qui fonctionne sans interop COM :

   ```bash
   dotnet add package Aspose.Cells
   ```

3. **Copy an Excel file** (`EraDates.xlsx`) dans la racine du projet. Ce classeur doit contenir une feuille nommée `"Sheet1"` avec la cellule **B2** contenant une valeur comme `"R3/5/12"` (Reiwa 3, 12 mai).

C’est tout le scaffolding dont vous avez besoin. Le reste du tutoriel se concentre sur la logique réelle de **read excel cell value** et **write datetime to excel**.

## Étape 2 : Lire la valeur d’une cellule Excel avec C#

Maintenant que le projet est prêt, récupérons la chaîne depuis la feuille de calcul. Le fragment suivant montre la chaîne d'appels exacte :

```csharp
using Aspose.Cells;
using System;
using System.Globalization;

class Program
{
    static void Main()
    {
        // Load the workbook (adjust the path as needed)
        Workbook wb = new Workbook("EraDates.xlsx");
        Worksheet ws = wb.Worksheets["Sheet1"];   // assumes the sheet is named Sheet1

        // Step 2: Get the cell that holds the Japanese era date string
        // B2 contains something like "R3/5/12"
        Cell dateCell = ws.Cells["B2"];  

        // Step 3: Read the string representation from the cell
        string eraDateString = dateCell.StringValue;  

        Console.WriteLine($"Original cell value: {eraDateString}");
        // -------------------------------------------------
        // From here we’ll convert the era string to a DateTime.
        // -------------------------------------------------
    }
}
```

**Pourquoi cela fonctionne :** `Cell.StringValue` renvoie toujours le texte affiché, quel que soit le format numérique sous‑jacent. Cela garantit que nous travaillons avec la chaîne exacte `"R3/5/12"` que l'utilisateur voit.

### Pièges courants

- **Empty cells** – `StringValue` renvoie une chaîne vide. Protégez‑vous contre cela avant l'analyse.  
- **Unexpected formats** – Si la cellule contient `"2023/05/12"` le parseur d'ère lèvera une exception ; vous pourriez avoir besoin d’une solution de repli.  

## Étape 3 : Écrire un DateTime dans Excel avec C#

Avec la chaîne d'ère en main, nous l'analysons maintenant avec `DateTime.ParseExact`. Le format `"ggyy/MM/dd"` indique à .NET d'attendre une ère japonaise (`gg`), une année à deux chiffres (`yy`) et les composants mois/jour.

```csharp
        // Step 4: Convert the era date string to a DateTime using the Japanese culture
        DateTime parsedDate;
        try
        {
            parsedDate = DateTime.ParseExact(
                eraDateString,
                "ggyy/MM/dd",
                new CultureInfo("ja-JP"));
        }
        catch (FormatException)
        {
            Console.WriteLine("The cell value does not match the expected Japanese era format.");
            return;
        }

        Console.WriteLine($"Parsed DateTime (UTC): {parsedDate:u}");

        // Step 5: Store the resulting DateTime back into the same cell
        dateCell.PutValue(parsedDate);

        // Optional: Apply a standard date format so Excel shows it nicely
        dateCell.SetStyle(new Style { Number = 14 }); // 14 = "m/d/yyyy"

        // Save the workbook to a new file so we don’t overwrite the original
        wb.Save("EraDates_Converted.xlsx");
        Console.WriteLine("Workbook saved as EraDates_Converted.xlsx");
```

**Pourquoi nous utilisons `PutValue`** : Aspose.Cells détecte automatiquement le type .NET et écrit le type de cellule Excel approprié. Passer un `DateTime` donne une vraie date Excel, qui peut être formatée ou utilisée dans des formules en aval.

### Cas limites et astuces

- **Time zones** – Les objets `DateTime` sont stockés sans information de zone. Si vous avez besoin d'UTC, appelez `DateTime.SpecifyKind`.  
- **Culture fallback** – Si vous prévoyez d’autres cultures, encapsulez l’analyse dans une fonction d’aide qui teste plusieurs objets `CultureInfo`.  
- **Performance** – Lors du traitement de milliers de lignes, réutilisez une seule instance de `CultureInfo` au lieu d'en créer une nouvelle à chaque boucle.  

## Étape 4 : Exemple complet fonctionnel – Tout assembler

Ci-dessous le programme complet, prêt à être exécuté. Copiez‑collez‑le dans `Program.cs`, assurez‑vous que `EraDates.xlsx` se trouve à côté du binaire compilé, et exécutez `dotnet run`.

```csharp
using Aspose.Cells;
using System;
using System.Globalization;

class Program
{
    static void Main()
    {
        // Load workbook
        Workbook wb = new Workbook("EraDates.xlsx");
        Worksheet ws = wb.Worksheets["Sheet1"];   // Change if your sheet has a different name

        // -------------------------------------------------
        // 1️⃣ Read the Japanese era string from B2
        // -------------------------------------------------
        Cell dateCell = ws.Cells["B2"];
        string eraDateString = dateCell.StringValue?.Trim();

        if (string.IsNullOrEmpty(eraDateString))
        {
            Console.WriteLine("Cell B2 is empty. Nothing to convert.");
            return;
        }

        Console.WriteLine($"Original cell value: {eraDateString}");

        // -------------------------------------------------
        // 2️⃣ Parse the era string into a DateTime
        // -------------------------------------------------
        DateTime parsedDate;
        try
        {
            parsedDate = DateTime.ParseExact(
                eraDateString,
                "ggyy/MM/dd",
                new CultureInfo("ja-JP"));
        }
        catch (FormatException)
        {
            Console.WriteLine("The value does not match the expected Japanese era format (ggyy/MM/dd).");
            return;
        }

        Console.WriteLine($"Parsed DateTime: {parsedDate:u}");

        // -------------------------------------------------
        // 3️⃣ Write the DateTime back into the same cell
        // -------------------------------------------------
        dateCell.PutValue(parsedDate);

        // Apply a friendly date format (e.g., 2023/05/12)
        Style style = wb.CreateStyle();
        style.Number = 14; // Built‑in date format
        dateCell.SetStyle(style);

        // Save the updated workbook
        wb.Save("EraDates_Converted.xlsx");
        Console.WriteLine("Conversion complete – saved as EraDates_Converted.xlsx");
    }
}
```

**Sortie attendue**

```
Original cell value: R3/5/12
Parsed DateTime: 2021-05-12 00:00:00Z
Conversion complete – saved as EraDates_Converted.xlsx
```

Lorsque vous ouvrez `EraDates_Converted.xlsx`, la cellule **B2** affiche maintenant une date normale (par ex., `5/12/2021`) et peut être utilisée dans les calculs Excel comme n'importe quelle autre valeur de date.

## Astuces pro pour un code Read Write Excel C# robuste

- **Validate before you write** – Utilisez `Cell.IsFormula` ou `Cell.Type` pour éviter d'écraser des formules par inadvertance.  
- **Batch processing** – Si vous devez convertir une colonne entière, bouclez sur `ws.Cells.Columns[1]` (colonne B) et appliquez la même logique.  
- **Thread safety** – Les objets Aspose.Cells ne sont pas thread‑safe ; créez des instances `Workbook` séparées par thread lors du parallélisme.  
- **Logging** – Pour les scripts de production, remplacez `Console.WriteLine` par un logger approprié (par ex., Serilog) afin de capturer les échecs d'analyse.  
- **Testing** – Écrivez des tests unitaires qui injectent des chaînes d'ère connues dans une méthode d’aide et vérifient les valeurs `DateTime` résultantes.  

## Conclusion

Vous venez de maîtriser **read write Excel C#** en apprenant comment **read excel cell value**, analyser une chaîne d'ère japonaise, et **write datetime to excel** en toute confiance. L'exemple complet montre un flux de travail propre, de bout en bout, que vous pouvez adapter aux opérations en masse, à différentes cultures, ou même aux pipelines Excel‑vers‑base de données.

Et ensuite ? Essayez d'étendre le script pour traiter une colonne entière de dates d'ère, ou explorez les riches options de formatage d'Aspose.Cells pour styliser les cellules de sortie. Vous pouvez également expérimenter d’autres bibliothèques comme EPPlus ou ClosedXML—la plupart de la logique reste la même, seules les appels d'API diffèrent.

Des questions ou un scénario Excel difficile ? Laissez un commentaire ci‑dessous, et bon codage !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}