---
category: general
date: 2026-05-23
description: Comment utiliser les marqueurs avec Aspose.Cells pour obtenir une automatisation
  Excel avec un nommage dynamique des feuilles. Apprenez les marqueurs intelligents,
  la liaison de données JSON et la création de feuilles en quelques minutes.
draft: false
keywords:
- how to use markers
- dynamic sheet naming excel
- aspose.cells smart markers
language: fr
og_description: Comment utiliser les marqueurs dans Aspose.Cells pour générer des
  fichiers Excel avec un nommage dynamique des feuilles. Guide complet étape par étape
  avec un exemple complet en C#.
og_title: Comment utiliser les marqueurs – Nommage dynamique des feuilles dans Excel
  avec Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: How to use markers with Aspose.Cells to achieve dynamic sheet naming
    Excel automation. Learn smart markers, JSON data binding, and sheet creation in
    minutes.
  headline: How to Use Markers in Aspose.Cells for Dynamic Sheet Naming in Excel
  type: TechArticle
- description: How to use markers with Aspose.Cells to achieve dynamic sheet naming
    Excel automation. Learn smart markers, JSON data binding, and sheet creation in
    minutes.
  name: How to Use Markers in Aspose.Cells for Dynamic Sheet Naming in Excel
  steps:
  - name: What Happens Under the Hood?
    text: 1. The processor reads the `Orders` array. 2. For each order it creates
      a **master sheet** (using `${Orders.MasterSheetName}`) and a **detail sheet**
      (using the `DetailSheetNewName` pattern). 3. Cell values are replaced with the
      corresponding JSON fields, so the master sheet’s first cell ends up con
  - name: What if I need more than two levels of hierarchy?
    text: You can nest markers inside the newly created detail sheets. Just place
      additional `${...}` tags in the template sheet before processing. The processor
      will cascade through each level automatically.
  - name: Can I use a DataTable instead of JSON?
    text: Absolutely. `SmartMarkerProcessor` has overloads for `DataSet`, `DataTable`,
      and even custom objects. The only change is the call to `ApplyJson` – you’d
      use `ApplyDataSet(myDataSet)` instead.
  - name: How do I control the order of sheet creation?
    text: The order follows the sequence of the source collection. If you need a custom
      sort, simply sort the JSON array (or DataTable) before passing it to the processor.
  - name: Is there a way to hide the template sheet after processing?
    text: Yes. Set `sm.Options.RemoveTemplateSheets = true;` before calling `ApplyJson`.
      The original sheet (index 0) will be removed from the final workbook.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Comment utiliser les marqueurs dans Aspose.Cells pour nommer dynamiquement
  les feuilles Excel
url: /fr/net/smart-markers-dynamic-data/how-to-use-markers-in-aspose-cells-for-dynamic-sheet-naming/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment utiliser les marqueurs dans Aspose.Cells pour la nomination dynamique des feuilles dans Excel

Vous vous êtes déjà demandé **comment utiliser les marqueurs** pour transformer un modèle Excel statique en un classeur maître‑détail complet ? Vous n'êtes pas seul. De nombreux développeurs se heurtent à un mur lorsqu'ils ont besoin de *dynamic sheet naming excel*, surtout lorsque les noms des feuilles doivent refléter des valeurs provenant de JSON ou d'une base de données.  

Dans ce tutoriel, nous parcourrons un exemple complet, prêt à l’emploi en C#, qui montre **comment utiliser les marqueurs** avec les **smart markers** d’**Aspose.Cells**, comment lier des données JSON, et laisser le processeur créer des feuilles dont les noms changent à la volée. Pas de blabla, juste le code exact que vous pouvez coller dans Visual Studio et voir les résultats immédiatement.

## Ce que vous allez apprendre

- Le concept de **smart markers** et pourquoi ils sont parfaits pour les scénarios maître‑détail.  
- Comment intégrer des balises de marqueur dans un classeur qui seront ensuite remplacées par les vrais noms de feuilles.  
- Configurer le **dynamic sheet naming excel** à l’aide de l’option `DetailSheetNewName`.  
- Exécuter le `SmartMarkerProcessor` sur des données JSON pour générer automatiquement plusieurs feuilles.  
- Vérifier le résultat et quelques astuces pratiques pour éviter les pièges courants.

> **Prérequis** – Vous avez besoin d’un runtime .NET récent (≥ .NET 6 convient), de la bibliothèque Aspose.Cells for .NET (vous pouvez obtenir une version d’essai gratuite sur le site d’Aspose), et d’une connaissance de base du C#.  

---

![how to use markers example in Aspose.Cells](example.png "how to use markers example in Aspose.Cells")

## Comment utiliser les marqueurs pour créer une nomination dynamique des feuilles (Étape 1)

La première chose dont nous avons besoin est un classeur vierge qui servira de modèle. Dans un projet réel, vous commenceriez probablement à partir d’un fichier `.xlsx` existant contenant déjà la mise en page, le formatage et les cellules de substitution. Pour plus de clarté, nous créerons tout programmétiquement.

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarker;

// Step 1: Create a new workbook and get the first worksheet
Workbook wb = new Workbook();                // fresh workbook, no sheets yet
Worksheet ws = wb.Worksheets[0];             // default first sheet
```

*Pourquoi c’est important* : l’objet `Worksheet` est l’endroit où nous déposerons nos balises **smart marker**. Pensez aux balises comme de petits espaces réservés que le processeur remplacera plus tard par les valeurs réelles provenant du JSON.  

## Insérer les balises Smart Marker (Étape 2)

Nous plaçons maintenant les balises de marqueur directement dans les cellules. La syntaxe `${...}` indique à Aspose.Cells « c’est un marqueur ». Dans notre exemple, nous avons besoin de deux marqueurs : un pour le nom de la feuille maître et un autre pour le nom de la feuille détail.

```csharp
// Step 2: Insert Smart Marker tags that will be replaced with sheet names
ws.Cells[0, 0].PutValue("${Orders.MasterSheetName}");   // master sheet placeholder
ws.Cells[1, 0].PutValue("${Orders.DetailSheetName}");   // detail sheet placeholder
```

> **Astuce** – Gardez les noms de marqueur courts et significatifs ; ils deviennent les clés que vous utiliserez dans votre charge utile JSON.

## Préparer les données JSON (Étape 3)

Le processeur fonctionne avec n’importe quelle source de données pouvant être représentée en JSON, un `DataSet`, ou même un objet simple. Voici une chaîne JSON minimale contenant une collection maître‑détail. Notez que chaque commande possède à la fois un `MasterSheetName` et un `DetailSheetName`.

```csharp
// Step 3: Prepare the JSON data that contains the master‑detail information
string jsonOrders = @"{
    ""Orders"": [
        {
            ""OrderId"": 1,
            ""MasterSheetName"": ""Master_1"",
            ""DetailSheetName"": ""Detail_1""
        },
        {
            ""OrderId"": 2,
            ""MasterSheetName"": ""Master_2"",
            ""DetailSheetName"": ""Detail_2""
        }
    ]
}";
```

*Pourquoi JSON ?* Il est léger, lisible par l’homme, et fonctionne très bien avec les API web. Vous pourriez tout aussi facilement extraire ces données d’une requête SQL et les sérialiser avec `Newtonsoft.Json`.

## Initialiser le SmartMarkerProcessor (Étape 4)

Le `SmartMarkerProcessor` est le moteur qui parcourt le classeur, trouve les marqueurs, et effectue la liaison des données. L’instancier ne prend qu’une ligne.

```csharp
// Step 4: Initialise the SmartMarkerProcessor with the workbook
SmartMarkerProcessor sm = new SmartMarkerProcessor(wb);
```

## Définir la nomination dynamique des feuilles (Étape 5)

C’est ici que le **dynamic sheet naming excel** montre tout son potentiel. En définissant `DetailSheetNewName`, nous indiquons au processeur de créer une nouvelle feuille détail pour chaque commande et de la nommer en fonction de `OrderId`. Le placeholder `${OrderId}` est résolu à partir de l’enregistrement courant pendant le traitement.

```csharp
// Step 5: Define how new detail sheets should be named during processing
sm.Options.DetailSheetNewName = "Detail_${OrderId}";
```

> **Attention** – Si vous oubliez d’inclure la syntaxe `${}`, la feuille sera littéralement nommée « Detail_${OrderId} » au lieu de « Detail_1 », « Detail_2 », etc.

## Appliquer le JSON et générer les feuilles (Étape 6)

Nous laissons maintenant le processeur faire le gros du travail. Il lira le JSON, remplacera les marqueurs, et créera de nouvelles feuilles de calcul selon les besoins.

```csharp
// Step 6: Apply the JSON data to populate the smart markers and generate sheets
sm.ApplyJson(jsonOrders);
```

### Que se passe-t-il en coulisses ?

1. Le processeur lit le tableau `Orders`.  
2. Pour chaque commande, il crée une **feuille maître** (en utilisant `${Orders.MasterSheetName}`) et une **feuille détail** (en utilisant le modèle `DetailSheetNewName`).  
3. Les valeurs des cellules sont remplacées par les champs JSON correspondants, de sorte que la première cellule de la feuille maître contiendra « Master_1 », « Master_2 », etc.  

## Enregistrer et vérifier le résultat (Optionnel)

Enfin, écrivez le classeur sur le disque. Ouvrez le fichier dans Excel et vous devriez voir deux feuilles maîtres (`Master_1`, `Master_2`) et deux feuilles détail nommées dynamiquement (`Detail_1`, `Detail_2`).  

```csharp
// (Optional) Save the result to verify the output
wb.Save("output.xlsx");
```

**Sortie attendue** – Après avoir ouvert `output.xlsx`, vous verrez :

- Feuille **Master_1** avec la cellule A1 = « Master_1 ».  
- Feuille **Detail_1** avec la cellule A1 = « Detail_1 ».  
- Feuille **Master_2** avec la cellule A1 = « Master_2 ».  
- Feuille **Detail_2** avec la cellule A1 = « Detail_2 ».  

C’est le cycle complet de **comment utiliser les marqueurs** pour obtenir **dynamic sheet naming excel** avec les **smart markers** d’**Aspose.Cells**.

---

## Questions fréquentes & cas particuliers

### Et si j’ai besoin de plus de deux niveaux de hiérarchie ?

Vous pouvez imbriquer des marqueurs à l’intérieur des feuilles détail nouvellement créées. Il suffit de placer des balises `${...}` supplémentaires dans la feuille modèle avant le traitement. Le processeur enchaînera chaque niveau automatiquement.

### Puis‑je utiliser un DataTable au lieu de JSON ?

Absolument. `SmartMarkerProcessor` propose des surcharges pour `DataSet`, `DataTable`, et même des objets personnalisés. Le seul changement concerne l’appel à `ApplyJson` ; vous utiliseriez `ApplyDataSet(myDataSet)` à la place.

### Comment contrôler l’ordre de création des feuilles ?

L’ordre suit la séquence de la collection source. Si vous avez besoin d’un tri personnalisé, triez simplement le tableau JSON (ou le DataTable) avant de le transmettre au processeur.

### Existe‑t‑il un moyen de masquer la feuille modèle après le traitement ?

Oui. Définissez `sm.Options.RemoveTemplateSheets = true;` avant d’appeler `ApplyJson`. La feuille originale (indice 0) sera alors supprimée du classeur final.

---

## Exemple complet (Toutes les étapes combinées)

Voici le programme complet que vous pouvez copier‑coller dans un nouveau projet console C#. Assurez‑vous d’avoir ajouté la référence au package NuGet `Aspose.Cells`.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.SmartMarker;

namespace DynamicSheetNamingDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook and get the first worksheet
            Workbook wb = new Workbook();
            Worksheet ws = wb.Worksheets[0];

            // Step 2: Insert Smart Marker tags that will be replaced with sheet names
            ws.Cells[0, 0].PutValue("${Orders.MasterSheetName}");
            ws.Cells[1, 0].PutValue("${Orders.DetailSheetName}");

            // Step 3: Prepare the JSON data that contains the master‑detail information
            string jsonOrders = @"{
                ""Orders"": [
                    {
                        ""OrderId"": 1,
                        ""MasterSheetName"": ""Master_1"",
                        ""DetailSheetName"": ""Detail_1""
                    },
                    {
                        ""OrderId"": 2,
                        ""MasterSheetName"": ""Master_2"",
                        ""DetailSheetName"": ""Detail_2""
                    }
                ]
            }";

            // Step 4: Initialise the SmartMarkerProcessor with the workbook
            SmartMarkerProcessor sm = new SmartMarkerProcessor(wb);

            // Step 5: Define how new detail sheets should be named during processing
            sm.Options.DetailSheetNewName = "Detail_${OrderId}";

            // (Optional) Remove the original template sheet after processing
            // sm.Options.RemoveTemplateSheets = true;

            // Step 6: Apply the JSON data to populate the smart markers and generate sheets
            sm.ApplyJson(jsonOrders);

            // Save the result
            wb.Save("output.xlsx");
            Console.WriteLine("Workbook generated successfully. Check output.xlsx.");
        }
    }
}
```

Exécutez le programme, ouvrez `output.xlsx`, et vous verrez les feuilles dynamiques exactement comme décrit précédemment.

---

## Conclusion

Nous venons de couvrir **comment utiliser les marqueurs** dans Aspose.Cells pour transformer un classeur simple en une solution maître‑détail avec **dynamic sheet naming excel**. Les points clés à retenir sont :

1. Placez des marqueurs `${...}` là où vous voulez que les données apparaissent.  
2. Fournissez du JSON (ou toute source de données prise en charge) au `SmartMarkerProcessor`.  
3. Utilisez `DetailSheetNewName` pour laisser le processeur nommer les nouvelles feuilles à la volée.  

À partir d’ici, vous pouvez explorer des scénarios plus avancés — ajout de tableaux, mise en forme des cellules, ou même insertion de graphiques — tout cela piloté par les smart markers.

## Tutoriels associés

- [How to Implement Aspose.Cells Smart Markers in C# for Dynamic Excel Reporting](/cells/english/net/automation-batch-processing/implement-aspose-cells-smart-markers-with-csharp/)
- [Generate Dynamic Excel Reports Using Aspose.Cells .NET Smart Markers](/cells/english/net/templates-reporting/generate-excel-reports-aspose-cells-net-smart-markers/)
- [Mastering Aspose.Cells .NET: Implement Smart Markers and Custom Labels for Dynamic Excel Reports](/cells/english/net/advanced-features/aspose-cells-net-smart-markers-custom-labels/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}