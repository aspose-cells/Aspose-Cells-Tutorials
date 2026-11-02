---
category: general
date: 2026-07-03
description: Comment utiliser SEQUENCE en C# pour générer des nombres incrémentiels
  dans Excel. Apprenez à créer un classeur Excel en C# et ASP.NET, créer un fichier
  Excel en quelques lignes de code.
draft: false
keywords:
- how to use sequence
- create excel workbook c#
- asp.net create excel file
- generate incremental numbers excel
language: fr
og_description: Comment utiliser SEQUENCE en C# pour générer des nombres incrémentaux
  dans Excel. Guide étape par étape pour créer un classeur Excel avec C# et ASP.NET
  et générer un fichier Excel.
og_title: Comment utiliser SEQUENCE en C# – Créer un classeur Excel
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: How to use SEQUENCE in C# to generate incremental numbers in Excel.
    Learn to create Excel workbook C# and ASP.NET create Excel file with a few lines
    of code.
  headline: How to Use SEQUENCE in C# – Create Excel Workbook
  type: TechArticle
- description: How to use SEQUENCE in C# to generate incremental numbers in Excel.
    Learn to create Excel workbook C# and ASP.NET create Excel file with a few lines
    of code.
  name: How to Use SEQUENCE in C# – Create Excel Workbook
  steps:
  - name: Why Use SEQUENCE Instead of a Loop?
    text: '- **Performance** – Excel does the math on its own engine, which is highly
      optimized. - **Maintainability** – The formula is self‑documenting; anyone opening
      the sheet instantly knows the intent. - **Dynamic resizing** – Change the `rows`
      argument and the spill range expands automatically.'
  - name: Pro Tip
    text: 'If you need the workbook in memory (e.g., to send it over a web API), use
      a `MemoryStream`:'
  - name: What If the Client Uses an Older Excel Version?
    text: 'Dynamic arrays (including `SEQUENCE`) were introduced in Excel 365/2019.
      If you need backward compatibility, fall back to a manual fill:'
  type: HowTo
- questions:
  - answer: No. `SEQUENCE` is a non‑iterative function; a simple `CalculateFormula()`
      call is enough.
    question: Do I need to enable iterative calculation?
  - answer: 'Change the second argument: `=SEQUENCE(1,5,10,2)` spills across B1:F1.'
    question: What if I want a horizontal spill?
  - answer: Absolutely. For example, `=INDEX(A:A, SEQUENCE(5,1,10,2))` can pull rows
      from another column.
    question: Can I combine SEQUENCE with other functions?
  - answer: The file size impact of a formula is negligible. Only when you start populating
      millions of cells manually does size become an issue.
    question: Is the workbook size a concern?
  type: FAQPage
tags:
- C#
- Excel
- Aspose.Cells
- ASP.NET
title: Comment utiliser SEQUENCE en C# – Créer un classeur Excel
url: /fr/net/formulas-functions/how-to-use-sequence-in-c-create-excel-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment utiliser SEQUENCE en C# – Créer un classeur Excel

Vous vous êtes déjà demandé **comment utiliser SEQUENCE** pour générer une liste de nombres dans une feuille Excel depuis C# ? Vous n'êtes pas le seul. Que vous construisiez un tableau de bord de reporting, alimentiez une grille de données, ou que vous ayez simplement besoin d'une façon rapide de générer des ID, maîtriser cette astuce vous évite de bricoler avec des boucles.

Dans ce tutoriel, nous **créerons un classeur Excel en C#**, insérerons une formule de tableau dynamique `SEQUENCE` dans la cellule A1, et obtiendrons une belle colonne de nombres incrémentiels. Nous verrons également comment servir ce fichier depuis un contrôleur ASP.NET — oui, **ASP.NET create Excel file** est également couvert. À la fin, vous pourrez **générer des nombres incrémentiels à la manière d'Excel** avec une seule ligne de code.

## Ce dont vous aurez besoin

- .NET 6+ (le code fonctionne également sur .NET Framework 4.6+)  
- Le package NuGet **Aspose.Cells for .NET** (ou toute bibliothèque exposant des objets `Workbook`/`Worksheet`)  
- Un projet ASP.NET Core ou MVC de base si vous souhaitez essayer la partie téléchargement web  

C’est tout. Aucun interop COM supplémentaire, aucune installation d’Office requise.

---

## Comment utiliser SEQUENCE pour générer des nombres incrémentiels

La fonction Excel `SEQUENCE(rows, [columns], [start], [step])` renvoie une plage **spill**. Dans notre cas, nous voulons 5 lignes, 1 colonne, commencer à 10, pas 2. La formule est la suivante :

```excel
=SEQUENCE(5,1,10,2)
```

Lorsque Excel l’évalue, les cellules A1:A5 contiendront **10, 12, 14, 16, 18**. L’avantage, c’est que nous n’avons pas besoin d’écrire de boucles C# — la formule fait le travail lourd.

Voici le snippet complet en C# qui crée un classeur, insère la formule, force le calcul, et enregistre le fichier.

```csharp
using Aspose.Cells;
using System.IO;

// 1️⃣ Create a new workbook
Workbook workbook = new Workbook();

// 2️⃣ Grab the first worksheet (Aspose creates one by default)
Worksheet sheet = workbook.Worksheets[0];

// 3️⃣ Insert the SEQUENCE formula – this will spill a 5‑row column starting at 10, step 2
sheet.Cells["A1"].Formula = "=SEQUENCE(5,1,10,2)";

// 4️⃣ Force calculation so the spilled range is materialized
workbook.CalculateFormula();

// 5️⃣ Save to disk (you can change the path as needed)
workbook.Save("DynamicArray.xlsx");
```

**Sortie attendue** – ouvrez *DynamicArray.xlsx* et vous verrez :

| A |
|---|
| 10 |
| 12 |
| 14 |
| 16 |
| 18 |

C’est toute l’histoire **how to use sequence** en C#. Simple, non ? Mais approfondissons un peu.

### Pourquoi utiliser SEQUENCE au lieu d’une boucle ?

- **Performance** – Excel effectue les calculs avec son propre moteur, hautement optimisé.  
- **Maintainability** – La formule est auto‑documentante ; quiconque ouvre la feuille comprend immédiatement l’intention.  
- **Dynamic resizing** – Modifier l’argument `rows` fait que la plage spill s’étend automatiquement.

---

## Créer un classeur Excel en C# – Étape par étape

Si vous débutez avec **create excel workbook c#**, la checklist suivante vous aide à éviter les pièges courants.

1. **Ajoutez le package Aspose.Cells**  
   ```bash
   dotnet add package Aspose.Cells
   ```
   (Vous pouvez également utiliser ClosedXML ou EPPlus, mais l'API présentée correspond au code ci‑dessus.)

2. **Définissez une licence** (optionnel pour la version d'essai).  
   ```csharp
   var license = new Aspose.Cells.License();
   license.SetLicense("Aspose.Total.NET.lic");
   ```

3. **Instanciez `Workbook`** – cela vous donne un classeur vierge et neuf.

4. **Référencez la feuille de calcul** – `workbook.Worksheets[0]` est la feuille par défaut nommée *Sheet1*.

5. **Appliquez la formule SEQUENCE** – comme montré précédemment.

6. **Calculez** – `workbook.CalculateFormula()` force le spill ; sinon le fichier ne contiendrait que la formule.

7. **Enregistrez** – vous pouvez écrire sur le disque, dans un `MemoryStream`, ou directement dans une réponse HTTP.

### Astuce pro

Si vous avez besoin du classeur en mémoire (par ex., pour l’envoyer via une API web), utilisez un `MemoryStream` :

```csharp
using var ms = new MemoryStream();
workbook.Save(ms, SaveFormat.Xlsx);
byte[] excelBytes = ms.ToArray(); // ready to return or attach
```

---

## ASP.NET Create Excel File – Diffusion vers le navigateur

Maintenant que nous connaissons **create excel workbook c#**, intégrons‑le dans un contrôleur ASP.NET Core afin que les utilisateurs puissent télécharger le fichier à la volée.

```csharp
using Aspose.Cells;
using Microsoft.AspNetCore.Mvc;
using System.IO;

[Route("api/[controller]")]
public class ExcelController : ControllerBase
{
    [HttpGet("download")]
    public IActionResult Download()
    {
        // 1️⃣ Build the workbook (same steps as before)
        var workbook = new Workbook();
        var sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].Formula = "=SEQUENCE(5,1,10,2)";
        workbook.CalculateFormula();

        // 2️⃣ Save to a memory stream
        using var ms = new MemoryStream();
        workbook.Save(ms, SaveFormat.Xlsx);
        ms.Position = 0; // reset stream position

        // 3️⃣ Return the file as a download
        const string fileName = "DynamicArray.xlsx";
        return File(ms, 
                    "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet", 
                    fileName);
    }
}
```

Lorsqu’un utilisateur accède à `/api/excel/download`, le navigateur propose le téléchargement de *DynamicArray.xlsx*. Le fichier contient déjà la colonne **generated incremental numbers excel** grâce à la formule `SEQUENCE`.

### Que faire si le client utilise une version plus ancienne d’Excel ?

Les tableaux dynamiques (y compris `SEQUENCE`) ont été introduits dans Excel 365/2019. Si vous avez besoin de compatibilité descendante, revenez à un remplissage manuel :

```csharp
// Alternative for older Excel: write numbers directly
for (int i = 0; i < 5; i++)
{
    sheet.Cells[i, 0].PutValue(10 + i * 2); // column 0 = A
}
```

Ce snippet montre l’approche classique **generate incremental numbers excel** sans dépendre de la nouvelle fonction.

---

## Questions fréquentes & cas limites

- **Do I need to enable iterative calculation?**  
  Non. `SEQUENCE` est une fonction non itérative ; un simple appel `CalculateFormula()` suffit.

- **What if I want a horizontal spill?**  
  Modifiez le deuxième argument : `=SEQUENCE(1,5,10,2)` déborde sur B1:F1.

- **Can I combine SEQUENCE with other functions?**  
  Absolument. Par exemple, `=INDEX(A:A, SEQUENCE(5,1,10,2))` peut extraire des lignes d’une autre colonne.

- **Is the workbook size a concern?**  
  L’impact sur la taille du fichier d’une formule est négligeable. Ce n’est que lorsque vous commencez à remplir manuellement des millions de cellules que la taille devient un problème.

## Conclusion

Nous avons parcouru **how to use sequence** en C# pour **create excel workbook c#**, servi ce classeur via **ASP.NET create excel file**, et démontré une méthode propre pour **generate incremental numbers excel** sans écrire de boucles. L’idée principale : laissez le moteur de tableau dynamique d’Excel faire le comptage, et laissez votre code .NET se concentrer sur l’orchestration.

N’hésitez pas à expérimenter — changez les arguments `rows`, `start` ou `step`, débordez horizontalement, ou combinez la formule avec `IF` ou `FILTER` pour des rapports plus sophistiqués. Quand vous êtes prêt, essayez de chaîner plusieurs feuilles ou d’exporter le classeur au format CSV pour les systèmes en aval.

Vous avez une variante à partager ? Laissez un commentaire ci‑dessous, ou contactez‑moi sur GitHub. Bon codage !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités d’API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [How to Create and Configure Excel Workbooks with Aspose.Cells .NET: A Step-by-Step Guide](/cells/english/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)
- [How to Create and Save Excel Files with Aspose.Cells for .NET: A Complete Guide](/cells/english/net/workbook-operations/create-save-excel-file-aspose-cells-dotnet/)
- [How to Create and Style Excel Workbooks Using Aspose.Cells for .NET (2023 Guide)](/cells/english/net/formatting/create-style-excel-workbooks-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}