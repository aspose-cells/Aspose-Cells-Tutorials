---
category: general
date: 2026-10-01
description: Apprenez à créer un classeur Excel en C#, à appliquer un format numérique
  personnalisé, à définir le nombre de décimales des cellules et à enregistrer le
  classeur au format XLSX dans un guide complet étape par étape.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook c#
- apply custom number format
- how to format numbers excel
- set cell decimal places
- save workbook as xlsx
language: fr
lastmod: 2026-10-01
og_description: Créez un classeur Excel en C# avec un format numérique personnalisé,
  définissez le nombre de décimales des cellules et enregistrez le classeur au format
  XLSX. Suivez ce guide complet pour obtenir une sortie numérique précise.
og_image_alt: Screenshot of an Excel sheet showing numbers rounded to four significant
  digits
og_title: Créer un classeur Excel en C# – format de nombre personnalisé et exportation
  XLSX
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to create Excel workbook C# and apply custom number format,
    set cell decimal places, and save workbook as XLSX in a complete step‑by‑step
    guide.
  headline: How to create Excel workbook C# with custom number formatting
  type: TechArticle
- description: Learn how to create Excel workbook C# and apply custom number format,
    set cell decimal places, and save workbook as XLSX in a complete step‑by‑step
    guide.
  name: How to create Excel workbook C# with custom number formatting
  steps:
  - name: Run the program (`dotnet run`).
    text: Run the program (`dotnet run`).
  - name: Open `SigDigits.xlsx`.
    text: Open `SigDigits.xlsx`.
  - name: Confirm that **A1** reads `123.5`.
    text: Confirm that **A1** reads `123.5`.
  - name: If you open the file’s XML (`.xlsx` is a zip archive), you’ll see the custom
      format `"0.######"` stored in the `<c>` element’s `s` attribute.
    text: If you open the file’s XML (`.xlsx` is a zip archive), you’ll see the custom
      format `"0.######"` stored in the `<c>` element’s `s` attribute.
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: Comment créer un classeur Excel en C# avec un format de nombre personnalisé
url: /fr/net/excel-custom-number-date-formatting/how-to-create-excel-workbook-c-with-custom-number-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment créer un classeur Excel C# avec un format numérique personnalisé

Si vous devez **créer un classeur Excel c#** qui affiche les nombres exactement comme vous le souhaitez, ce guide vous montre comment le faire en quelques étapes claires. Vous apprendrez à appliquer un format numérique personnalisé, à définir le nombre de décimales d’une cellule, et enfin **enregistrer le classeur au format xlsx** pour une utilisation ultérieure.

Travailler avec des données numériques implique souvent de concilier précision et lisibilité. À la fin de ce tutoriel, vous disposerez d’un modèle réutilisable qui limite les chiffres affichés à un nombre spécifique de chiffres significatifs tout en préservant la valeur originale dans le fichier. Aucun script externe n’est requis — uniquement C# et la bibliothèque Aspose.Cells.

## Prérequis

Avant de commencer, assurez‑vous d’avoir :

* SDK .NET 6.0 ou version ultérieure installé  
* Visual Studio 2022 (ou tout IDE C#)  
* Le package NuGet **Aspose.Cells for .NET** (`Install-Package Aspose.Cells`) – cette bibliothèque fournit les classes `Workbook`, `Worksheet` et `ExportTableOptions` utilisées dans les exemples.  

Ces exigences sont minimales ; le même code fonctionne sous .NET Core, .NET Framework, et même dans Azure Functions.

## Étape 1 : Créer un classeur Excel C# – initialiser le fichier

La première opération consiste à instancier un nouvel objet `Workbook`. Cet objet représente l’ensemble du fichier Excel en mémoire et contient automatiquement une feuille de calcul par défaut.

```csharp
using Aspose.Cells;

namespace ExcelDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook and get the first worksheet
            Workbook workbook = new Workbook();               // creates an empty .xlsx container
            Worksheet sheet = workbook.Worksheets[0];         // reference to the default sheet
```

**Pourquoi c’est important :**  
Créer le classeur dès le départ vous fournit une toile vierge. La feuille de calcul par défaut (`Worksheets[0]`) est prête pour la saisie de données, vous n’avez donc pas besoin d’ajouter une nouvelle feuille sauf si votre scénario nécessite plusieurs onglets.

## Étape 2 : Écrire une valeur numérique dans une cellule

Placez maintenant un nombre d’exemple dans la cellule **A1**. La valeur que nous utilisons (`123.456789`) contient plus de décimales que nous ne souhaitons finalement afficher, ce qui nous permet de démontrer l’arrondi plus tard.

```csharp
            // Step 2: Write a numeric value to cell A1
            sheet.Cells[0, 0].PutValue(123.456789); // row 0, column 0 = A1
```

**Astuce :** `PutValue` détecte automatiquement le type de données, vous n’avez donc pas besoin de convertir le nombre en chaîne.

## Étape 3 : Appliquer un format numérique personnalisé – limiter les décimales visibles

Pour contrôler la façon dont Excel affiche le nombre, nous créons un `Style` avec un **format numérique personnalisé**. Le modèle `"0.######"` indique à Excel d’afficher jusqu’à six décimales mais d’omettre les zéros superflus.

```csharp
            // Step 3: Define a custom number format (up to 6 decimal places) and apply it
            Style customStyle = workbook.CreateStyle();
            customStyle.Custom = "0.######";               // up to 6 decimals, no trailing zeros
            sheet.Cells[0, 0].SetStyle(customStyle);
```

**Comment cela fonctionne :**  
La chaîne de format suit la syntaxe des formats personnalisés d’Excel. `0` force l’affichage d’un chiffre, tandis que `#` n’affiche un chiffre que s’il est significatif. En les combinant, vous obtenez un affichage flexible qui respecte toujours la précision originale.

## Étape 4 : Définir le nombre de décimales d’une cellule – en utilisant ExportTableOptions

Si vous devez **définir le nombre de décimales d’une cellule** pour les données exportées (par ex., lors de la conversion en DataTable), Aspose.Cells vous permet de spécifier le nombre de **chiffres significatifs**. Cette étape garantit que le CSV ou le DataTable exporté respecte les mêmes règles d’arrondi que celles appliquées dans le classeur.

```csharp
            // Step 4: Configure export options to limit the output to 4 significant digits
            ExportTableOptions exportOptions = new ExportTableOptions();
            exportOptions.SignificantDigits = 4;           // round to 4 significant figures
```

**Pourquoi utiliser `SignificantDigits` ?**  
Contrairement à un nombre fixe de décimales, les chiffres significatifs conservent l’ordre de grandeur du nombre tout en limitant la précision, ce qui correspond souvent à ce que les analystes attendent lors de la synthèse de données.

## Étape 5 : Exporter les données de la feuille et **enregistrer le classeur au format xlsx**

Enfin, exportez les données (si vous avez besoin d’un DataTable) et enregistrez le classeur sur le disque. L’appel `ExportDataTable` respecte les `ExportTableOptions` que nous avons configurés, et `workbook.Save` écrit un fichier XLSX standard.

```csharp
            // Step 5: Export the worksheet data using the configured options and save the workbook
            sheet.ExportDataTable(sheet.Cells.MaxDisplayRange, true, exportOptions);
            workbook.Save("SigDigits.xlsx");               // saves to the application’s working folder
        }
    }
}
```

**Résultat attendu :**  
Lorsque vous ouvrez *SigDigits.xlsx* dans Excel, la cellule **A1** affiche `123.5`. La valeur sous‑jacente reste `123.456789`, mais le nombre affiché respecte la règle des 4 chiffres significatifs. Si vous exportez la feuille vers un DataTable, la valeur dans le tableau sera également arrondie à `123.5`.

---

## Appliquer le format numérique personnalisé à d’autres cellules

Si vous devez formater une plage plutôt qu’une seule cellule, réutilisez l’objet `Style` :

```csharp
// Apply the same custom style to B2:C5
Range range = sheet.Cells.CreateRange("B2:C5");
range.ApplyStyle(customStyle, new StyleFlag { NumberFormat = true });
```

**Astuce pro :** Réutiliser un objet style réduit la consommation de mémoire et garantit une mise en forme cohérente sur toute la feuille.

## Comment formater les nombres dans Excel avec C# – variations courantes

| Scénario | Chaîne de format | Résultat |
|----------|------------------|----------|
| Fixed two decimal places | `"0.00"` | `123.46` |
| Currency (US) | `"$#,##0.00"` | `$123.46` |
| Percentage with one decimal | `"0.0%"` | `12,346.0%` |
| Scientific notation | `"0.00E+00"` | `1.23E+02` |

Choisissez le modèle qui correspond à vos exigences de reporting. Tous les modèles sont compatibles avec la propriété `Style.Custom` démontrée précédemment.

## Définir le nombre de décimales d’une cellule dynamiquement en fonction de l’entrée utilisateur

Parfois, la précision requise n’est pas connue au moment de la compilation. Vous pouvez construire la chaîne de format à l’exécution :

```csharp
int decimals = 3; // could come from a UI textbox
string format = "0." + new string('#', decimals);
customStyle.Custom = format;
sheet.Cells["A2"].PutValue(987.654321);
sheet.Cells["A2"].SetStyle(customStyle);
```

**Cas limite :** Si `decimals` vaut zéro, le format devient `"0"` (affichage entier). Validez toujours l’entrée utilisateur pour éviter des chaînes de format mal formées.

## Enregistrer le classeur au format XLSX – bonnes pratiques

* **Utilisez des chemins absolus** lors de l’écriture vers un répertoire connu (`Path.Combine(Environment.CurrentDirectory, \"output.xlsx\")`).  
* **Disposez** le `Workbook` si vous le placez dans une instruction `using` afin de libérer rapidement les ressources non gérées :

```csharp
using (Workbook wb = new Workbook())
{
    // ...populate workbook...
    wb.Save(Path.Combine(@"C:\Exports", "Report.xlsx"));
}
```

* **Compatibilité des versions :** Aspose.Cells écrit des fichiers compatibles avec Excel 2010‑2023, de sorte que les utilisateurs en aval ne rencontreront pas de problèmes de format.

---

## Exemple complet fonctionnel

Voici le programme complet que vous pouvez copier, coller et exécuter immédiatement. Il comprend toutes les directives `using` nécessaires, des commentaires et la gestion des erreurs.

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelDemo
{
    class Program
    {
        static void Main()
        {
            try
            {
                // 1️⃣ Create workbook and get the first worksheet
                Workbook workbook = new Workbook();
                Worksheet sheet = workbook.Worksheets[0];

                // 2️⃣ Write a high‑precision number to A1
                sheet.Cells[0, 0].PutValue(123.456789);

                // 3️⃣ Apply a custom number format (up to 6 decimals)
                Style customStyle = workbook.CreateStyle();
                customStyle.Custom = "0.######";
                sheet.Cells[0, 0].SetStyle(customStyle);

                // 4️⃣ Configure export options for 4 significant digits
                ExportTableOptions exportOptions = new ExportTableOptions
                {
                    SignificantDigits = 4
                };

                // 5️⃣ Export data (optional) and save the workbook as XLSX
                sheet.ExportDataTable(sheet.Cells.MaxDisplayRange, true, exportOptions);
                string outputPath = Path.Combine(Environment.CurrentDirectory, "SigDigits.xlsx");
                workbook.Save(outputPath);

                Console.WriteLine($"Workbook saved successfully at: {outputPath}");
                Console.WriteLine("Cell A1 displays: " + sheet.Cells["A1"].StringValue);
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"Error creating workbook: {ex.Message}");
            }
        }
    }
}
```

**Étapes de vérification**

1. Exécutez le programme (`dotnet run`).  
2. Ouvrez `SigDigits.xlsx`.  
3. Vérifiez que **A1** affiche `123.5`.  
4. Si vous ouvrez le XML du fichier (`.xlsx` est une archive zip), vous verrez le format personnalisé `"0.######"` stocké dans l’attribut `s` de l’élément `<c>`.

---

## Conclusion

Dans ce tutoriel, vous avez appris comment **créer un classeur Excel c#**, **appliquer un format numérique personnalisé**, **définir le nombre de décimales d’une cellule**, et **enregistrer le classeur au format xlsx** en utilisant Aspose.Cells. La solution montre à la fois le formatage visuel dans Excel et l’arrondi lors de l’exportation des données via `ExportTableOptions`.

À partir d’ici, vous pouvez :

* Étendre l’approche à des plages ou tables entières.  
* Combiner plusieurs styles (polices, bordures) avec `StyleFlag`.  
* Automatiser la génération de rapports en parcourant les sources de données et en appliquant la même logique de formatage.  

N’hésitez pas à expérimenter avec différentes chaînes de format, nombres de décimales ou options d’exportation pour répondre à vos besoins spécifiques de reporting. Bon codage !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités d’API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Créer un classeur Excel C# – Appliquer le format monétaire et importer DataTable](/cells/english/net/excel-data-import-export/create-excel-workbook-c-apply-currency-format-and-import-dat/)
- [Créer un classeur Excel C# – Guide étape par étape avec mise en forme conditionnelle](/cells/english/net/excel-conditional-formatting/create-excel-workbook-c-step-by-step-guide-with-conditional/)
- [Créer un classeur Excel C# – Ajouter un commentaire & enregistrer au format XLSX](/cells/english/net/excel-comment-annotation/create-excel-workbook-c-add-comment-save-as-xlsx/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}