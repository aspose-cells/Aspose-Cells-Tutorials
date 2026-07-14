---
category: general
date: 2026-07-13
description: Créer un classeur Excel en C# et apprendre à ajouter une plage nommée,
  attribuer un nom à un tableau et gérer les conflits de noms — le tout dans un exemple
  clair.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- add named range
- assign name to table
- set table name
- how to add range
language: fr
lastmod: 2026-07-13
og_description: Créez un classeur Excel en C# avec Aspose.Cells. Apprenez à ajouter
  une plage nommée, définir le nom d’un tableau et résoudre les conflits de noms dans
  un guide concis et exécutable.
og_image_alt: Screenshot showing an Excel workbook with a named range and a table
  name set using C# code
og_title: Créer un classeur Excel en C# – Ajouter une plage nommée et définir le nom
  du tableau
schemas:
- author: Aspose
  dateModified: '2026-07-13'
  description: Create Excel Workbook in C# and learn how to add named range, assign
    name to table, and handle naming conflicts—all in one clear example.
  headline: Create Excel Workbook in C# – Add Named Range & Set Table Name
  type: TechArticle
- description: Create Excel Workbook in C# and learn how to add named range, assign
    name to table, and handle naming conflicts—all in one clear example.
  name: Create Excel Workbook in C# – Add Named Range & Set Table Name
  steps:
  - name: '**Use a consistent prefix** (`tbl_`, `rng_`, etc.) – it instantly tells
      you what the object is.'
    text: '**Use a consistent prefix** (`tbl_`, `rng_`, etc.) – it instantly tells
      you what the object is.'
  - name: '**Stay within 255 characters** – Excel’s limit for names.'
    text: '**Stay within 255 characters** – Excel’s limit for names.'
  - name: '**Avoid spaces and special characters** – only letters, numbers, and underscores
      are safe.'
    text: '**Avoid spaces and special characters** – only letters, numbers, and underscores
      are safe.'
  - name: '**Validate before assigning** – a quick `if (!sheet.Names.Contains(name))`
      check prevents the clash we demonstrated.'
    text: '**Validate before assigning** – a quick `if (!sheet.Names.Contains(name))`
      check prevents the clash we demonstrated.'
  type: HowTo
- questions:
  - answer: Yes, but you must qualify the address with the sheet name, e.g., `"Sheet1!A1:B5"`.
      The `Names.Add` method accepts that format.
    question: Can I add a named range that spans multiple worksheets?
  - answer: Absolutely. You can pass a formula string instead of a static address,
      such as `"=OFFSET(Sheet1!$A$1,0,0,COUNT(Sheet1!$A:$A),2)"`.
    question: Does Aspose.Cells support dynamic named ranges (like OFFSET formulas)?
  - answer: 'Just set `table.Name = " ## What Should You Learn Next?


      The following tutorials cover closely related topics that build on the techniques
      demonstrated in this guide. Each resource includes complete working code examples
      with step-by-step explanations to help you master additional API features and
      explore alternative implementation approaches in your own projects.

      - [How to Create Workbook Scoped Named Ranges in Excel Using Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)
      - [How to Implement a Named Range with Workbook Scope in Aspose.Cells Java for
      Enhanced Excel Data Management](/cells/english/java/tables-structured-references/implement-named-range-workbook-scope-aspose-cells-java/)
      - [Excel Automation&#58; Create a Workbook and Add a ListBox Using Aspose.Cells
      for .NET](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)

      {{< /blocks/products/pf/tutorial-page-section >}} {{< /blocks/products/pf/main-container
      >}} {{< /blocks/products/pf/main-wrap-class >}} {{< blocks/products/products-backtop-button
      >}}'
    question: What if I need to rename an existing table?
  type: FAQPage
tags:
- C#
- Aspose.Cells
- Excel Automation
- .NET
title: Créer un classeur Excel en C# – Ajouter une plage nommée et définir le nom
  du tableau
url: /fr/net/excel-advanced-named-ranges/create-excel-workbook-in-c-add-named-range-set-table-name/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un classeur Excel en C# – Guide complet pour ajouter des plages nommées et définir les noms de tableau

Vous avez déjà eu besoin de **créer un classeur Excel** à partir de zéro et vous vous êtes demandé où placer une plage nommée ou comment donner à un tableau son propre identifiant ? Vous n'êtes pas le seul. Dans de nombreux scénarios de reporting ou d'exportation de données, vous vous retrouverez à jongler avec des plages, des tableaux et parfois des conflits de noms.

Dans ce tutoriel, nous parcourrons un exemple entièrement exécutable qui **crée un classeur Excel**, **ajoute une plage nommée**, puis **attribue un nom à un tableau** — vous montrant exactement quoi faire lorsque les noms entrent en conflit. À la fin, vous connaîtrez le « comment » et le « pourquoi » de chaque étape, ainsi que quelques astuces pour garder votre code propre.

> **Gain rapide :** Le code utilise la bibliothèque **Aspose.Cells**, qui fonctionne avec .NET 6+ et ne nécessite aucune installation d’Excel sur le serveur.

## Ce dont vous avez besoin

- **.NET 6 SDK** (ou toute version récente de .NET)  
- **Aspose.Cells for .NET** package NuGet  
- Un IDE décent (Visual Studio, Rider ou VS Code)  
- Connaissances de base en C# — rien de compliqué, juste les déclarations `using` habituelles

Si vous avez tout cela, nous pouvons passer directement au processus de **création d’un classeur Excel**.

## ## Créer un classeur Excel – Vue d’ensemble étape par étape

Voici le programme complet, prêt à copier‑coller. Il montre tout, de la création du classeur à la gestion d’un conflit de nom lorsque vous essayez de **attribuer un nom à un tableau**.

```csharp
using System;
using Aspose.Cells;

namespace ExcelNamingDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook
            Workbook workbook = new Workbook();

            // Step 2: Add some sample data so we have a table to work with
            Worksheet sheet = workbook.Worksheets[0];
            sheet.Cells["A1"].PutValue("Product");
            sheet.Cells["B1"].PutValue("Price");
            sheet.Cells["A2"].PutValue("Apple");
            sheet.Cells["B2"].PutValue(0.99);
            sheet.Cells["A3"].PutValue("Banana");
            sheet.Cells["B3"].PutValue(0.59);
            sheet.Cells["A4"].PutValue("Cherry");
            sheet.Cells["B4"].PutValue(2.99);
            sheet.Cells["A5"].PutValue("Date");
            sheet.Cells["B5"].PutValue(3.49);

            // Step 3: Convert the data range into a table (default name Table1)
            int tableIndex = sheet.Tables.Add(sheet.Cells.CreateRange("A1:B5"), true);
            ListObject table = sheet.Tables[tableIndex];
            // At this point the table name is "Table1"

            // Step 4: Add a named range that covers the same cells
            // This is the "add named range" part of the tutorial
            sheet.Names.Add("MyRange", "A1:B5");

            // Step 5: Try to give the table the same name – this will cause a conflict
            try
            {
                table.Name = "MyRange"; // <-- assign name to table
            }
            catch (Exception ex)
            {
                // Step 6: Handle the naming conflict by outputting the error message
                Console.WriteLine("Naming conflict detected:");
                Console.WriteLine(ex.Message);
            }

            // Optional: Save the workbook to verify everything works
            workbook.Save("DemoWorkbook.xlsx");
        }
    }
}
```

**Sortie attendue** lors de l’exécution du programme :

```
Naming conflict detected:
A name with the same text already exists.
```

Et si vous ouvrez *DemoWorkbook.xlsx*, vous verrez un tableau nommé **Table1** et une plage nommée appelée **MyRange** — exactement ce que nous voulions, sans le conflit.

## ## Ajouter une plage nommée – Pourquoi c’est important

Une **plage nommée** est essentiellement un alias pour un bloc de cellules. Au lieu de référencer constamment `A1:B5`, vous pouvez écrire `MyRange` dans les formules, les validations de données, ou même dans le code. Cela améliore la lisibilité et réduit les risques d’erreurs de frappe.

Dans l’extrait ci‑dessus, nous appelons :

```csharp
sheet.Names.Add("MyRange", "A1:B5");
```

- Le premier argument est le **nom** que vous utiliserez plus tard.  
- Le deuxième argument est l’**adresse** (relative à la feuille de calcul).  

Si vous avez besoin de **comment ajouter une plage** dynamiquement, vous pouvez construire la chaîne d’adresse avec `Cell.GetRefersTo()` ou utiliser `Range refRange = sheet.Cells.CreateRange(startRow, startCol, totalRows, totalCols)`.

## ## Attribuer un nom à un tableau – Gestion des conflits

Les tableaux (également appelés *objets de liste*) possèdent déjà une propriété de nom intégrée. Par défaut, Aspose.Cells les nomme `Table1`, `Table2`, etc. Lorsque vous essayez d’attribuer à un tableau le même identifiant qu’une plage nommée existante, la bibliothèque lève une exception — tout comme Excel le fait.

Pourquoi cela se produit‑il ?

- La portée des noms dans Excel est **à l’échelle du classeur** pour les plages et les tableaux.  
- Des noms dupliqués rendraient les formules ambiguës, donc le moteur les bloque.

### Astuce pro

Si vous avez vraiment besoin qu’un tableau partage un nom logique avec une plage, envisagez de **préfixer** l’un d’eux, par exemple :

```csharp
table.Name = "tbl_MyRange";   // safe, no conflict
```

Ou renommez d’abord la plage :

```csharp
sheet.Names["MyRange"].Name = "DataRange";
```

Les deux approches maintiennent l’espace de noms propre et évitent les erreurs d’exécution.

## ## Définir le nom du tableau – Bonnes pratiques

Lorsque vous **définissez le nom d’un tableau** par programme, gardez ces directives à l’esprit :

1. **Utilisez un préfixe cohérent** (`tbl_`, `rng_`, etc.) – il indique immédiatement quel est l’objet.  
2. **Restez dans la limite de 255 caractères** – la limite d’Excel pour les noms.  
3. **Évitez les espaces et les caractères spéciaux** – seules les lettres, les chiffres et les underscores sont sûrs.  
4. **Validez avant d’attribuer** – une vérification rapide `if (!sheet.Names.Contains(name))` empêche le conflit que nous avons démontré.  

Voici une méthode d’aide que vous pouvez intégrer à n’importe quel projet :

```csharp
static void SafeSetTableName(Worksheet sheet, ListObject table, string desiredName)
{
    string finalName = desiredName;
    int suffix = 1;
    while (sheet.Names.Contains(finalName) || sheet.Tables.Contains(finalName))
    {
        finalName = $"{desiredName}_{suffix}";
        suffix++;
    }
    table.Name = finalName;
}
```

Appeler `SafeSetTableName(sheet, table, "MyRange")` transformera automatiquement `MyRange` en `MyRange_1` s’il existe un conflit, garantissant que l’opération de **création d’un classeur Excel** ne s’interrompt jamais de façon inattendue.

## ## Exemple complet fonctionnel – Tout assembler

Voici une version compacte que vous pouvez copier directement dans une application console. Elle inclut la routine de sécurité et montre le flux complet de bout en bout.

```csharp
using System;
using Aspose.Cells;

namespace ExcelNamingDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create the workbook
            Workbook wb = new Workbook();
            Worksheet ws = wb.Worksheets[0];

            // Populate a simple dataset
            ws.Cells["A1"].PutValue("Item");
            ws.Cells["B1"].PutValue("Quantity");
            ws.Cells["A2"].PutValue("Pen");
            ws.Cells["B2"].PutValue(10);
            ws.Cells["A3"].PutValue("Notebook");
            ws.Cells["B3"].PutValue(5);

            // Turn data into a table
            int tblIdx = ws.Tables.Add(ws.Cells.CreateRange("A1:B3"), true);
            ListObject tbl = ws.Tables[tblIdx];

            // Add a named range covering the same cells
            ws.Names.Add("MyRange", "A1:B3");

            // Safely assign a name to the table
            SafeSetTableName(ws, tbl, "MyRange");

            // Save to verify
            wb.Save("FinalDemo.xlsx");
            Console.WriteLine($"Table name set to: {tbl.Name}");
        }

        static void SafeSetTableName(Worksheet sheet, ListObject table, string desiredName)
        {
            string candidate = desiredName;
            int i = 1;
            while (sheet.Names.Contains(candidate) || sheet.Tables.Contains(candidate))
            {
                candidate = $"{desiredName}_{i}";
                i++;
            }
            table.Name = candidate;
        }
    }
}
```

L’exécution de ce script produit `FinalDemo.xlsx` où le tableau s’appelle `MyRange_1` (ou un autre suffixe unique) et la plage reste `MyRange`. Pas d’exception, pas de mystère — juste un nommage propre et déterministe.

## ## Questions fréquemment posées (FAQ)

**Q : Puis‑je ajouter une plage nommée qui s’étend sur plusieurs feuilles de calcul ?**  
R : Oui, mais vous devez qualifier l’adresse avec le nom de la feuille, par exemple, `"Sheet1!A1:B5"`. La méthode `Names.Add` accepte ce format.

**Q : Aspose.Cells prend‑il en charge les plages nommées dynamiques (comme les formules OFFSET) ?**  
R : Absolument. Vous pouvez passer une chaîne de formule au lieu d’une adresse statique, telle que `"=OFFSET(Sheet1!$A$1,0,0,COUNT(Sheet1!$A:$A),2)"`.

**Q : Que faire si je dois renommer un tableau existant ?**  
R : Il suffit de définir `table.Name = "

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}