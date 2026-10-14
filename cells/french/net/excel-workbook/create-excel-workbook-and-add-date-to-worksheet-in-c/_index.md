---
category: general
date: 2026-10-13
description: Créer un classeur Excel en C# et écrire la date dans Excel en utilisant
  Aspose.Cells. Apprenez à enregistrer le fichier Excel au format xlsx et à ajouter
  la date à la feuille de calcul avec le code complet.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- save excel file
- write date to excel
- save workbook as xlsx
- add date to worksheet
language: fr
lastmod: 2026-10-13
og_description: Créez un classeur Excel en C# et écrivez la date dans Excel. Suivez
  ce guide complet pour enregistrer le fichier Excel au format xlsx et ajouter la
  date à la feuille de calcul avec Aspose.Cells.
og_image_alt: Excel workbook screenshot showing a Japanese imperial date in cell A1
og_title: Créer un classeur Excel et ajouter une date à la feuille de calcul – C#
  étape par étape
schemas:
- author: Aspose
  dateModified: '2026-10-13'
  description: Create excel workbook in C# and write date to excel using Aspose.Cells.
    Learn to save excel file as xlsx and add date to worksheet with full code.
  headline: Create excel workbook and add date to worksheet in C#
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Créer un classeur Excel et ajouter une date à la feuille de calcul en C#
url: /fr/net/excel-workbook/create-excel-workbook-and-add-date-to-worksheet-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un classeur Excel et ajouter une date à la feuille de calcul en C#

Si vous devez **créer un classeur Excel** de manière programmatique, ce guide vous montre comment **écrire une date dans Excel** et **enregistrer le fichier Excel** en tant que classeur *.xlsx*. Vous verrez un exemple complet et exécutable qui analyse une chaîne d'ère impériale japonaise et stocke le `DateTime` résultant dans la cellule A1.

Travailler avec Excel depuis C# nécessite souvent trois étapes : instancier le classeur, placer des données sur une feuille de calcul, puis enfin persister le fichier. Ce tutoriel couvre chaque étape, explique pourquoi le code est écrit ainsi, et met en évidence les pièges courants tels que l'analyse dépendante de la culture et les autorisations du système de fichiers. À la fin, vous pourrez **ajouter une date à la feuille de calcul**, **enregistrer le classeur au format xlsx**, et adapter le modèle à tout type de données.

> **Prérequis** – L'exemple utilise la bibliothèque **Aspose.Cells for .NET** (version 23.10 ou ultérieure). Installez‑la via NuGet :

```bash
dotnet add package Aspose.Cells
```

Vous avez également besoin d'un SDK .NET 6+ et d'un répertoire accessible en écriture pour le fichier de sortie.

---

## Créer un classeur Excel et configurer la feuille de calcul

La première étape consiste à instancier un classeur vide et à récupérer sa feuille de calcul par défaut. Aspose.Cells crée automatiquement un classeur avec une feuille nommée « Sheet1 ».

```csharp
using Aspose.Cells;
using System;
using System.Globalization;

// Step 1: Create a new workbook
Workbook workbook = new Workbook();

// Step 2: Get the first worksheet (index 0)
Worksheet sheet = workbook.Worksheets[0];
```

**Pourquoi c'est important** – `Workbook` est le point d'entrée pour toutes les opérations Excel. En le créant sans paramètres, vous obtenez un classeur vierge que vous pouvez ensuite **enregistrer le fichier Excel** dans n'importe quel format de votre choix.

---

## Analyser une date impériale japonaise

Les dates impériales japonaises utilisent un symbole d'ère (par ex., « R » pour Reiwa) suivi d'une année à deux chiffres. La méthode .NET `DateTime.ParseExact` peut gérer ce format lorsque vous fournissez un objet `DateTimeParseOptions` personnalisé qui indique à l'analyseur d'utiliser le calendrier de l'Empereur japonais.

```csharp
// Step 3: Define a date string in the Japanese imperial era
string imperialDate = "R3/04/01"; // Reiwa 3, April 1st

// Step 4: Configure parsing options for the Japanese Emperor calendar
var parseOptions = new DateTimeParseOptions
{
    Calendar = DateTimeParseOptions.CalendarType.JapaneseEmperor
};

// Step 5: Parse the string into a .NET DateTime
DateTime parsedDate = DateTime.ParseExact(
    imperialDate,
    "ggyy/MM/dd",
    CultureInfo.InvariantCulture,
    DateTimeStyles.None,
    parseOptions);
```

**Explication** –  
* `gg` lit le désignateur d'ère (`R` pour Reiwa).  
* `yy` lit l'année à deux chiffres dans cette ère.  
* `MM/dd` lit le mois et le jour.  

Si vous omettez `parseOptions`, l'analyseur suppose le calendrier grégorien et lève une `FormatException`. C'est un cas limite fréquent lorsqu'on travaille avec des calendriers non grégoriens.

---

## Écrire la date dans la feuille de calcul

Maintenant que vous avez une valeur `DateTime`, vous pouvez la placer dans une cellule. Aspose.Cells formate automatiquement la cellule en fonction du type de la valeur.

```csharp
// Step 6: Write the parsed date into cell A1
sheet.Cells["A1"].PutValue(parsedDate);

// Optional: Apply a date format for better readability
Style style = workbook.CreateStyle();
style.Custom = "yyyy-mm-dd";
sheet.Cells["A1"].SetStyle(style);
```

**Pourquoi définir un style ?** – Sans style, Excel peut afficher la date en utilisant le format par défaut du système, ce qui peut prêter à confusion pour les utilisateurs d'autres paramètres régionaux. Définir explicitement `"yyyy-mm-dd"` garantit une apparence cohérente.

---

## Enregistrer le fichier Excel au format xlsx

Enfin, persistez le classeur sur le disque. La méthode `Save` détermine le format de sortie à partir de l'extension du fichier, donc l'utilisation de « .xlsx » déclenche automatiquement le format Office Open XML.

```csharp
// Step 7: Define the output path (adjust to your environment)
string outputPath = Path.Combine(
    Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
    "JapaneseDate.xlsx");

// Step 8: Save the workbook
workbook.Save(outputPath, SaveFormat.Xlsx);
```

**Astuce** – Si le répertoire cible n'existe pas ou si vous n'avez pas les permissions d'écriture, `Save` lève une `IOException`. Vérifiez toujours le chemin avant d'appeler `Save`.

---

## Exemple complet exécutable

Voici le programme complet que vous pouvez copier, coller et exécuter. Il inclut toutes les directives `using`, la gestion des erreurs, et des commentaires qui clarifient chaque opération.

```csharp
using Aspose.Cells;
using System;
using System.Globalization;
using System.IO;

class Program
{
    static void Main()
    {
        try
        {
            // 1️⃣ Create a new workbook and get the first worksheet
            Workbook workbook = new Workbook();
            Worksheet sheet = workbook.Worksheets[0];

            // 2️⃣ Define the Japanese imperial date string
            string imperialDate = "R3/04/01"; // Reiwa 3, April 1st

            // 3️⃣ Set up parsing options for the Japanese Emperor calendar
            var parseOptions = new DateTimeParseOptions
            {
                Calendar = DateTimeParseOptions.CalendarType.JapaneseEmperor
            };

            // 4️⃣ Parse the string into a .NET DateTime
            DateTime parsedDate = DateTime.ParseExact(
                imperialDate,
                "ggyy/MM/dd",
                CultureInfo.InvariantCulture,
                DateTimeStyles.None,
                parseOptions);

            // 5️⃣ Write the date to cell A1
            sheet.Cells["A1"].PutValue(parsedDate);

            // Apply a consistent date format
            Style dateStyle = workbook.CreateStyle();
            dateStyle.Custom = "yyyy-mm-dd";
            sheet.Cells["A1"].SetStyle(dateStyle);

            // 6️⃣ Determine the output file location
            string outputPath = Path.Combine(
                Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
                "JapaneseDate.xlsx");

            // 7️⃣ Save the workbook as an .xlsx file
            workbook.Save(outputPath, SaveFormat.Xlsx);

            Console.WriteLine($"Workbook saved successfully to: {outputPath}");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error: {ex.Message}");
        }
    }
}
```

**Résultat attendu**

Lorsque vous ouvrez `JapaneseDate.xlsx`, la cellule A1 contient la date **2021‑04‑01** (l'équivalent grégorien de Reiwa 3 / 04 / 01) affichée au format `yyyy‑mm‑dd`.

![Classeur Excel avec date dans la cellule A1](excel-date-screenshot.png){alt="Capture d'écran d'un classeur Excel affichant une date impériale japonaise dans la cellule A1"}

---

## Questions fréquentes et cas limites

| Question | Answer |
|----------|--------|
| *Et si l'ère change (par ex., Heisei à Reiwa) ?* | Le calendrier `JapaneseEmperor` mappe automatiquement les symboles d'ère (`H`, `R`, etc.) à la plage grégorienne correcte, vous n'avez donc qu'à mettre à jour la chaîne d'entrée. |
| *Puis-je écrire plusieurs dates dans une colonne ?* | Oui. Parcourez vos données et appelez `sheet.Cells[row, column].PutValue(dateValue)` pour chaque ligne. |
| *Et si j'ai besoin d'un format de date différent ?* | Modifiez `dateStyle.Custom` avec n'importe quelle chaîne de format de date Excel, comme `"dd-mmm-yyyy"` ou `"mm/dd/yyyy"`. |
| *Existe-t-il un moyen de protéger la feuille après avoir écrit la date ?* | Utilisez `sheet.Protect(ProtectOptions.All, "password")` avant d'enregistrer. |
| *Comment gérer les fuseaux horaires ?* | `DateTime` stocke l'heure UTC ou locale. Convertissez en utilisant `DateTime.SpecifyKind` ou `TimeZoneInfo.ConvertTime` avant d'appeler `PutValue`. |

---

## Conclusion

Vous savez maintenant comment **créer un classeur Excel**, **écrire une date dans Excel**, **ajouter une date à la feuille de calcul**, et **enregistrer le classeur au format xlsx** en utilisant Aspose.Cells en C#. L'exemple complet montre comment analyser une chaîne de calendrier impérial japonais, appliquer un style cohérent, et gérer les problèmes liés au système de fichiers.  

À partir d'ici, vous pouvez

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités d'API supplémentaires et explorer des approches d'implémentation alternatives dans vos propres projets.

- [Créer un classeur Excel C# – Ajouter un commentaire & enregistrer en XLSX](/cells/english/net/excel-comment-annotation/create-excel-workbook-c-add-comment-save-as-xlsx/)
- [Créer un nouveau classeur en C# – Ajouter une formule et enregistrer le fichier Excel](/cells/english/net/excel-workbook/create-new-workbook-in-c-add-formula-and-save-excel-file/)
- [Créer un classeur Excel – Envelopper les colonnes et enregistrer en XLSX](/cells/english/net/formatting-rows-and-columns-in-excel/create-excel-workbook-wrap-columns-and-save-as-xlsx/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}