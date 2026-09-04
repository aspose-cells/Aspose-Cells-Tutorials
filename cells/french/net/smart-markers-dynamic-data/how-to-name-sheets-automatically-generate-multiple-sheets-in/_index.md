---
category: general
date: 2026-02-09
description: Comment nommer les feuilles en C# avec SmartMarker – apprenez à générer
  plusieurs feuilles et à automatiser le nommage des feuilles en quelques lignes de
  code.
draft: false
keywords:
- how to name sheets
- generate multiple sheets
- automate sheet naming
- SmartMarker sheet naming
- workbook automation
language: fr
og_description: Comment nommer les feuilles en C# à l'aide des options SmartMarker.
  Ce guide montre comment générer plusieurs feuilles et automatiser la nomination
  des feuilles sans effort.
og_title: Comment nommer automatiquement les feuilles – Guide rapide C#
tags:
- C#
- Aspose.Cells
- Excel automation
title: Comment nommer automatiquement les feuilles – Générer plusieurs feuilles en
  C#
url: /fr/net/smart-markers-dynamic-data/how-to-name-sheets-automatically-generate-multiple-sheets-in/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment nommer automatiquement les feuilles – Générer plusieurs feuilles en C#

Vous vous êtes déjà demandé **comment nommer les feuilles** dans un classeur Excel sans cliquer manuellement sur « Renommer » à chaque fois ? Vous n'êtes pas seul. Dans de nombreux scénarios de reporting, vous vous retrouvez avec des dizaines de feuilles de détail qui nécessitent des noms systématiques, et le faire à la main est un cauchemar.  

La bonne nouvelle, c’est qu’avec quelques lignes de C#, vous pouvez **générer plusieurs feuilles** et **automatiser le nommage des feuilles** afin que chaque nouvelle feuille de détail suive un modèle prévisible. Dans ce tutoriel, nous parcourrons la solution complète, expliquerons pourquoi chaque élément est important, et vous fournirons un exemple de code prêt à l’exécution.

## Ce que couvre ce guide

* Configurer un classeur contenant des SmartMarkers.
* Configurer `SmartMarkerOptions` pour contrôler le nom de base des feuilles générées.
* Exécuter `ProcessSmartMarkers` afin que la bibliothèque crée `Detail`, `Detail_1`, `Detail_2`, … automatiquement.
* Conseils pour gérer les cas limites tels que les noms de feuilles existants ou les conventions de nommage personnalisées.
* Un exemple complet et exécutable que vous pouvez coller dans Visual Studio et voir le résultat immédiatement.

Aucune expérience préalable avec Aspose.Cells n’est requise — juste une configuration C# de base et un IDE de votre choix.

## Prérequis

| Exigence | Pourquoi c’est important |
|----------|---------------------------|
| .NET 6.0 ou version ultérieure | Fonctionnalités modernes du langage et compatibilité de la bibliothèque |
| Aspose.Cells pour .NET (package NuGet) | Fournit le traitement `SmartMarker` et la création de feuilles |
| Un projet console vierge (ou toute application .NET) | Nous donne un endroit où exécuter le code |

Installez la bibliothèque avec :

```bash
dotnet add package Aspose.Cells
```

Maintenant que les bases sont couvertes, plongeons dans l’implémentation réelle.

## Étape 1 : Créer un classeur avec des SmartMarkers

Tout d'abord, nous avons besoin d'un classeur contenant un espace réservé SmartMarker. Considérez un SmartMarker comme une balise de modèle qui indique au moteur où injecter les données et, dans notre cas, quand créer une nouvelle feuille.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣  Create a new workbook and get the first worksheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];
        ws.Name = "Template";

        // 2️⃣  Insert a SmartMarker that will trigger sheet creation
        // The marker {{detail}} tells Aspose.Cells to repeat the row for each item in the "detail" collection.
        ws.Cells["A1"].PutValue("{{detail}}");
        ws.Cells["B1"].PutValue("Item Name");
        ws.Cells["C1"].PutValue("Quantity");
        ws.Cells["A2"].PutValue("&=detail.Name");
        ws.Cells["B2"].PutValue("&=detail.Quantity");

        // 3️⃣  Prepare sample data for the SmartMarker
        var data = new
        {
            detail = new[]
            {
                new { Name = "Apple",  Quantity = 10 },
                new { Name = "Banana", Quantity = 20 },
                new { Name = "Cherry", Quantity = 30 }
            }
        };
```

> **Astuce :** Gardez la feuille modèle légère. Seules les lignes qui nécessitent une duplication doivent contenir des SmartMarkers ; tout le reste reste statique.

## Étape 2 : Configurer les options SmartMarker – Le cœur du nommage des feuilles

Voici la partie magique. En définissant `DetailSheetNewName`, nous indiquons au moteur quel nom de base utiliser pour chaque feuille générée. La bibliothèque ajoutera « _1 », « _2 », etc., chaque fois que le nom de base existe déjà.

```csharp
        // 4️⃣  Define naming options – this is where we answer “how to name sheets”
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
        {
            // Primary keyword appears here: how to name sheets
            DetailSheetNewName = "Detail"   // Base name for all generated sheets
        };
```

Si vous avez besoin d’une convention différente (par ex., « Report_2023 »), il suffit de changer la chaîne. Le moteur gère les collisions automatiquement, ce qui explique pourquoi cette approche **automatise le nommage des feuilles** sans code supplémentaire.

## Étape 3 : Traiter les SmartMarkers et générer les feuilles

Avec le classeur, les données et les options prêts, un seul appel de méthode effectue le travail lourd.

```csharp
        // 5️⃣  Run the SmartMarker processor – this will create Detail, Detail_1, Detail_2…
        wb.ProcessSmartMarkers(data, smartMarkerOptions);

        // 6️⃣  Save the result so you can open it in Excel
        wb.Save("GeneratedSheets.xlsx");

        // 7️⃣  Let the user know we’re done
        System.Console.WriteLine("Workbook created – check GeneratedSheets.xlsx");
    }
}
```

### Résultat attendu

Lorsque vous ouvrez *GeneratedSheets.xlsx*, vous verrez :

| Nom de la feuille | Contenu |
|-------------------|---------|
| Template          | La mise en page du marqueur original (conservée pour référence) |
| Detail            | Première série de lignes (Apple, Banana, Cherry) |
| Detail_1          | Deuxième copie – données identiques (utile lorsque vous avez plusieurs collections) |
| Detail_2          | …et ainsi de suite, selon le nombre de groupes SmartMarker distincts que vous avez |

Le modèle de nommage (`Detail`, `Detail_1`, `Detail_2`) montre **comment nommer les feuilles** de façon programmatique tout en **générant plusieurs feuilles** selon les besoins.

## Cas limites & variantes

### 1. Noms de feuilles existants

Si votre classeur contient déjà une feuille nommée « Detail », le moteur commencera avec « Detail_1 ». Cela évite les écrasements accidentels.

### 2. Formats d’incrémentation personnalisés

Vous voulez « Detail‑A », « Detail‑B » au lieu de suffixes numériques ? Vous pouvez post‑traiter les noms après `ProcessSmartMarkers` :

```csharp
for (int i = 0; i < wb.Worksheets.Count; i++)
{
    Worksheet sh = wb.Worksheets[i];
    if (sh.Name.StartsWith("Detail_"))
    {
        string suffix = ((char)('A' + i - 1)).ToString(); // A, B, C…
        sh.Name = $"Detail-{suffix}";
    }
}
```

### 3. Plusieurs groupes SmartMarker

Si votre classeur contient plus d’un groupe SmartMarker (par ex., `{{invoice}}` et `{{detail}}`), chaque groupe générera son propre ensemble de feuilles basé sur le même `DetailSheetNewName`. Pour donner à chaque groupe un préfixe distinct, créez des instances séparées de `SmartMarkerOptions` et appelez `ProcessSmartMarkers` pour chaque collection.

## Conseils pratiques du terrain

* **Astuce :** Désactivez `AllowDuplicateNames` dans `WorkbookSettings` si vous voulez que la bibliothèque lève une exception au lieu de renommer silencieusement les feuilles. Cela aide à détecter les bugs de logique de nommage tôt.
* **Attention :** Noms de base très longs. Excel limite les noms de feuilles à 31 caractères ; la bibliothèque tronque automatiquement, mais vous pourriez vous retrouver avec des noms ambigus.
* **Note de performance :** Générer des centaines de feuilles peut consommer de la mémoire. Libérez le classeur (`wb.Dispose()`) dès que vous avez fini si vous exécutez dans un service de longue durée.

## Vue d’ensemble visuelle

![diagramme comment nommer les feuilles](image.png "Diagramme montrant le flux du modèle SmartMarker aux feuilles générées – comment nommer les feuilles")

*Le texte alternatif inclut le mot‑clé principal pour satisfaire le SEO.*

## Code source complet (prêt à copier‑coller)

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create workbook and template sheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];
        ws.Name = "Template";

        // SmartMarker layout
        ws.Cells["A1"].PutValue("{{detail}}");
        ws.Cells["B1"].PutValue("Item Name");
        ws.Cells["C1"].PutValue("Quantity");
        ws.Cells["A2"].PutValue("&=detail.Name");
        ws.Cells["B2"].PutValue("&=detail.Quantity");

        // Sample data
        var data = new
        {
            detail = new[]
            {
                new { Name = "Apple",  Quantity = 10 },
                new { Name = "Banana", Quantity = 20 },
                new { Name = "Cherry", Quantity = 30 }
            }
        };

        // Configure naming – this answers how to name sheets
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
        {
            DetailSheetNewName = "Detail"
        };

        // Process markers → generates Detail, Detail_1, Detail_2 …
        wb.ProcessSmartMarkers(data, smartMarkerOptions);

        // Save and finish
        wb.Save("GeneratedSheets.xlsx");
        System.Console.WriteLine("Workbook created – open GeneratedSheets.xlsx to see the result.");
    }
}
```

Exécutez le programme, ouvrez le fichier généré, et vous verrez les feuilles nommées automatiquement selon le modèle que nous avons défini.

## Conclusion

Vous savez maintenant **comment nommer les feuilles** dans un classeur C#, comment **générer plusieurs feuilles** avec SmartMarker, et comment **automatiser le nommage des feuilles** afin de ne plus jamais avoir à renommer quoi que ce soit manuellement. L’approche passe d’une poignée de pages de détail à des centaines, et le même modèle fonctionne pour toute collection que vous fournissez à `ProcessSmartMarkers`.

Et ensuite ? Essayez de remplacer la source de données par une requête de base de données, expérimentez des formats de suffixe personnalisés, ou enchaînez plusieurs groupes SmartMarker pour un moteur de reporting complet. Le ciel est la limite lorsque vous laissez la bibliothèque gérer le travail de nommage répétitif.

Si vous avez trouvé ce guide utile, donnez‑lui une étoile sur GitHub, partagez‑le avec vos collègues, ou laissez un commentaire ci‑dessous avec vos propres astuces de nommage. Bon codage !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}