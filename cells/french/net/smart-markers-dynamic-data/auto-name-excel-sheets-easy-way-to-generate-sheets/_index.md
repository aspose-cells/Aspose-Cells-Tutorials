---
category: general
date: 2026-02-23
description: Nommez automatiquement les feuilles Excel et apprenez à générer des feuilles
  automatiquement à l'aide de SmartMarkers. Guide C# pas à pas pour des classeurs
  dynamiques.
draft: false
keywords:
- auto name excel sheets
- how to generate sheets
- Aspose.Cells SmartMarkers
- dynamic worksheet naming
- C# Excel automation
language: fr
og_description: Nommez automatiquement les feuilles Excel instantanément. Apprenez
  à générer des feuilles avec SmartMarkers en C# – exemple complet et exécutable.
og_title: Nommer automatiquement les feuilles Excel – Tutoriel rapide C#
tags:
- C#
- Excel
- Aspose.Cells
title: Nommer automatiquement les feuilles Excel – Méthode simple pour générer des
  feuilles
url: /fr/net/smart-markers-dynamic-data/auto-name-excel-sheets-easy-way-to-generate-sheets/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Nommer automatiquement les feuilles Excel – Tutoriel complet C#

Vous êtes-vous déjà demandé comment **nommer automatiquement les feuilles Excel** sans écrire une boucle qui renomme manuellement chaque onglet ? Vous n'êtes pas le seul. Dans de nombreux projets de reporting, le nombre de feuilles augmente à l'exécution, et garder des noms propres devient un vrai casse‑tête. Bonne nouvelle : avec les **SmartMarkers** d’Aspose.Cells, vous pouvez laisser la bibliothèque gérer le nommage pour vous, et elle vous montre même **comment générer des feuilles** à la volée.

Dans ce guide, nous allons parcourir un scénario réel : créer un classeur, configurer les options SmartMarker afin que les feuilles de détail soient automatiquement nommées *Detail*, *Detail1*, *Detail2*, …, puis vérifier que les feuilles apparaissent comme prévu. À la fin, vous disposerez d’une solution autonome, prête à copier‑coller, que vous pourrez adapter à tout projet nécessitant la création dynamique de feuilles de calcul.

---

## Ce dont vous avez besoin

Avant de commencer, assurez‑vous d’avoir :

- **.NET 6+** (ou .NET Framework 4.6.2+). Le code fonctionne avec n’importe quel runtime récent.  
- **Aspose.Cells for .NET** via le package NuGet – `Install-Package Aspose.Cells`.  
- Un projet C# de base (Console App, WinForms ou ASP.NET – le même code fonctionne partout).  
- Visual Studio, VS Code ou votre IDE préféré.

Pas d’interopérabilité Excel supplémentaire, pas de COM, uniquement du code géré pur.

---

## Étape 1 : Nommer automatiquement les feuilles Excel avec SmartMarkers

La première chose à faire est d’indiquer à Aspose.Cells le nom de base que vous souhaitez pour les feuilles de détail créées automatiquement. Cela se fait via la classe `SmartMarkerOptions`.

```csharp
using Aspose.Cells;
using Aspose.Cells.Tables;   // for SmartMarkers
using System;

class Program
{
    static void Main()
    {
        // Create a new workbook that will hold the master sheet.
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];
        ws.Name = "Master";

        // -----------------------------------------------------------
        // Step 1: Configure SmartMarker options – set the base name
        // -----------------------------------------------------------
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
        {
            // This tells SmartMarkers to create sheets named Detail, Detail1, Detail2, …
            DetailSheetNewName = "Detail"
        };
```

**Pourquoi c’est important :** En définissant `DetailSheetNewName`, vous confiez la logique de nommage à la bibliothèque. Plus besoin d’écrire une boucle `for` qui vérifie les noms existants et incrémente un compteur – l’API le fait pour vous, garantissant des noms uniques même lorsque la source de données contient des dizaines de lignes.

---

## Étape 2 : Préparer la source de données

Les SmartMarkers fonctionnent avec n’importe quelle collection `IEnumerable`, un `DataTable`, ou même une simple liste d’objets. Pour cette démonstration, nous utiliserons une liste d’objets représentant les détails de commande.

```csharp
        // -----------------------------------------------------------
        // Step 2: Build a sample data source
        // -----------------------------------------------------------
        var orders = new[]
        {
            new { OrderId = 1001, Product = "Laptop", Qty = 2, Price = 1200.00 },
            new { OrderId = 1002, Product = "Mouse",   Qty = 5, Price =  25.99 },
            new { OrderId = 1003, Product = "Keyboard",Qty = 3, Price =  45.50 }
        };
```

**Pourquoi c’est important :** La source de données détermine le nombre de feuilles de détail qui seront générées. Chaque élément de la collection crée une nouvelle feuille à partir du modèle SmartMarker que nous ajouterons ensuite.

---

## Étape 3 : Insérer un modèle SmartMarker dans la feuille maître

Un modèle SmartMarker n’est qu’une cellule (ou une plage) contenant des espaces réservés. Lorsque la méthode `Apply` s’exécute, les espaces réservés sont remplacés par les données réelles, et pour chaque ligne une nouvelle feuille est créée.

```csharp
        // -----------------------------------------------------------
        // Step 3: Add a SmartMarker template to the master sheet
        // -----------------------------------------------------------
        // Put a header row
        ws.Cells["A1"].PutValue("Order ID");
        ws.Cells["B1"].PutValue("Product");
        ws.Cells["C1"].PutValue("Quantity");
        ws.Cells["D1"].PutValue("Unit Price");

        // Insert SmartMarker placeholders starting at row 2
        ws.Cells["A2"].PutValue("&=orders.OrderId");
        ws.Cells["B2"].PutValue("&=orders.Product");
        ws.Cells["C2"].PutValue("&=orders.Qty");
        ws.Cells["D2"].PutValue("&=orders.Price");
```

**Pourquoi c’est important :** La syntaxe `&=` indique aux SmartMarkers « prenez la valeur dans la source de données ». Lors de l’exécution de `Apply`, Aspose.Cells copiera cette ligne dans une nouvelle feuille pour chaque élément de `orders`, en nommant automatiquement la feuille selon l’option que nous avons définie précédemment.

---

## Étape 4 : Appliquer les options SmartMarker – C’est ici que les feuilles sont auto‑nommées

Vient maintenant le moment où la bibliothèque fait le gros du travail. L’appel `Apply` lit le modèle, crée les feuilles de détail et les nomme selon `DetailSheetNewName`.

```csharp
        // -----------------------------------------------------------
        // Step 4: Apply SmartMarker – auto name excel sheets happens here
        // -----------------------------------------------------------
        ws.SmartMarkers.Apply(smartMarkerOptions, new { orders });

        // Save the workbook to verify the result
        wb.Save("AutoNamedSheets.xlsx");
        Console.WriteLine("Workbook saved. Open AutoNamedSheets.xlsx to see the result.");
    }
}
```

**Pourquoi c’est important :** La méthode `Apply` ne se contente pas de peupler les données ; elle respecte également le modèle de nommage que nous avons fourni. Si vous ouvrez *AutoNamedSheets.xlsx*, vous verrez :

- **Detail** – contient la première commande.  
- **Detail1** – deuxième commande.  
- **Detail2** – troisième commande.

Aucun renommage manuel requis.

---

## Étape 5 : Vérifier le résultat – Comment générer correctement les feuilles

Après avoir exécuté le programme, ouvrez le fichier généré. Vous devez voir trois nouvelles feuilles de calcul nommées exactement comme décrit ci‑dessus. Cela prouve que vous avez bien appris **comment générer des feuilles** automatiquement.

> **Astuce :** Si vous avez besoin d’un suffixe personnalisé (par ex., « _Report »), définissez simplement `DetailSheetNewName = "Detail_Report"` et la bibliothèque ajoutera les numéros après la chaîne de base.

---

## Cas limites et questions fréquentes

### Que se passe‑t‑il si le nom de base existe déjà ?

Aspose.Cells vérifie les noms de feuilles existants et ajoute un numéro incrémental jusqu’à obtenir un nom unique. Ainsi, même si une feuille nommée *Detail* existe déjà dans le classeur, la prochaine feuille générée deviendra *Detail1*.

### Puis‑je contrôler l’ordre des feuilles générées ?

Oui. L’ordre suit la séquence de la source de données. Si vous avez besoin d’un ordre spécifique, triez la collection avant de la passer à `Apply`.

### Est‑il possible de générer les feuilles dans un classeur différent ?

Absolument. Créez une seconde instance `Workbook`, ajoutez une feuille de substitution, puis appelez `Apply` sur cette feuille. La même logique de nommage s’applique.

### Comment cela fonctionne‑t‑il avec de gros ensembles de données ?

Les SmartMarkers sont optimisés pour les performances. Même avec des milliers de lignes, la bibliothèque diffuse les données efficacement. Veillez simplement à disposer de suffisamment de mémoire pour la taille finale du classeur.

---

## Exemple complet fonctionnel (prêt à copier‑coller)

Voici le programme complet que vous pouvez placer dans un nouveau projet console. Aucun morceau n’est manquant – tout, des directives `using` à l’appel final `Save`, est inclus.

```csharp
using Aspose.Cells;
using Aspose.Cells.Tables;
using System;

class AutoNameExcelSheetsDemo
{
    static void Main()
    {
        // 1️⃣ Create workbook and master worksheet
        Workbook workbook = new Workbook();
        Worksheet master = workbook.Worksheets[0];
        master.Name = "Master";

        // 2️⃣ Set up SmartMarker options – this is the key to auto‑naming
        SmartMarkerOptions options = new SmartMarkerOptions
        {
            DetailSheetNewName = "Detail"   // base name for generated sheets
        };

        // 3️⃣ Sample data source – each element will become a new sheet
        var orders = new[]
        {
            new { OrderId = 1001, Product = "Laptop",   Qty = 2, Price = 1200.00 },
            new { OrderId = 1002, Product = "Mouse",    Qty = 5, Price =  25.99 },
            new { OrderId = 1003, Product = "Keyboard", Qty = 3, Price =  45.50 }
        };

        // 4️⃣ Build a simple template on the master sheet
        master.Cells["A1"].PutValue("Order ID");
        master.Cells["B1"].PutValue("Product");
        master.Cells["C1"].PutValue("Quantity");
        master.Cells["D1"].PutValue("Unit Price");

        master.Cells["A2"].PutValue("&=orders.OrderId");
        master.Cells["B2"].PutValue("&=orders.Product");
        master.Cells["C2"].PutValue("&=orders.Qty");
        master.Cells["D2"].PutValue("&=orders.Price");

        // 5️⃣ Apply SmartMarkers – this auto‑creates and auto‑names the sheets
        master.SmartMarkers.Apply(options, new { orders });

        // 6️⃣ Save and inform the user
        workbook.Save("AutoNamedSheets.xlsx");
        Console.WriteLine("Done! Open AutoNamedSheets.xlsx – you’ll see Detail, Detail1, Detail2 …");
    }
}
```

Exécutez le programme, ouvrez le fichier *AutoNamedSheets.xlsx* généré, et vous verrez la fonctionnalité **nommer automatiquement les feuilles Excel** en action.

---

## Questions fréquentes complémentaires

- **Puis‑je utiliser cela avec un fichier modèle existant ?**  
  Oui. Chargez le classeur avec `new Workbook("Template.xlsx")` et pointez `master` vers la feuille qui contient vos espaces réservés SmartMarker.

- **Et si j’ai besoin de conventions de nommage différentes selon le type de feuille ?**  
  Créez plusieurs objets `SmartMarkerOptions`, chacun avec son propre `DetailSheetNewName`, et appliquez‑les aux différentes feuilles maîtres.

- **Existe‑t‑il un moyen de supprimer la feuille de base (celle contenant le modèle) ?**  
  Après `Apply`, vous pouvez simplement supprimer la feuille maître : `workbook.Worksheets.RemoveAt(0);` – les feuilles de détail restent intactes.

---

## Conclusion

Vous savez maintenant **comment nommer automatiquement les feuilles Excel** en utilisant les SmartMarkers d’Aspose.Cells, et vous avez également découvert un modèle solide pour **comment générer des feuilles** dynamiquement en C#. L’idée centrale est simple : configurez `SmartMarkerOptions.DetailSheetNewName`, fournissez une collection, et laissez la bibliothèque faire le reste. Cette approche élimine les boucles répétitives, garantit des noms uniques et s’adapte facilement à grande échelle.

Prêt pour l’étape suivante ? Essayez de remplacer la source de données par un `Data

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}