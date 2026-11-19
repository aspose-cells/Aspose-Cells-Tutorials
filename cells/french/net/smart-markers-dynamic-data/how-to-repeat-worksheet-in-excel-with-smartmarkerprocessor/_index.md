---
category: general
date: 2026-11-19
description: Comment répéter une feuille de calcul lors du remplissage d’Excel avec
  des données de tableau. Apprenez à générer plusieurs feuilles de calcul et à remplir
  une feuille à partir d’une liste en quelques étapes.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to repeat worksheet
- populate excel with array
- generate multiple worksheets
- populate worksheet from list
language: fr
lastmod: 2026-11-19
og_description: Comment répéter une feuille de calcul avec SmartMarkerProcessor. Suivez
  ce guide pour remplir Excel avec des données de tableau, générer plusieurs feuilles
  de calcul et remplir une feuille à partir d’une liste.
og_image_alt: Screenshot showing repeated worksheets in an Excel workbook after processing
og_title: Comment répéter une feuille de calcul dans Excel – guide étape par étape
schemas:
- author: GroupDocs
  dateModified: '2026-11-19'
  description: How to repeat worksheet while populating Excel with array data. Learn
    to generate multiple worksheets and populate worksheet from list in a few steps.
  headline: How to repeat worksheet in Excel with SmartMarkerProcessor
  type: TechArticle
- description: How to repeat worksheet while populating Excel with array data. Learn
    to generate multiple worksheets and populate worksheet from list in a few steps.
  name: How to repeat worksheet in Excel with SmartMarkerProcessor
  steps:
  - name: Expected output
    text: 'When you open the resulting workbook, you should see:'
  - name: Empty or null arrays
    text: 'If `Dept` is null or empty, the processor will not create any additional
      worksheets. To avoid a completely blank workbook, you can add a guard:'
  - name: Custom worksheet names
    text: 'The default naming scheme may not suit every reporting requirement. After
      processing, rename each sheet using a loop:'
  - name: Populating additional columns
    text: 'If you need to **populate excel with array** values beyond a single marker,
      extend the data object:'
  type: HowTo
tags:
- Excel automation
- SmartMarkerProcessor
- .NET
title: Comment répéter une feuille de calcul dans Excel avec SmartMarkerProcessor
url: /fr/net/smart-markers-dynamic-data/how-to-repeat-worksheet-in-excel-with-smartmarkerprocessor/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment répéter une feuille de calcul dans Excel avec SmartMarkerProcessor

Si vous devez **how to repeat worksheet** lors de la génération de rapports Excel, ce guide vous montre une solution complète et exécutable. À la fin du tutoriel, vous serez capable de **populate Excel with array** des données, **generate multiple worksheets**, et **populate worksheet from list** en utilisant la bibliothèque SmartMarkerProcessor.

Répéter une feuille de calcul est une exigence courante lorsque chaque département, région ou période doit disposer de son propre onglet. L'exemple ci‑dessous montre les étapes exactes, explique pourquoi chaque paramètre est important, et couvre les cas limites tels que les listes vides ou la nomination personnalisée.

## Prérequis

- .NET 6.0 ou version ultérieure installé
- Une référence au package NuGet **GroupDocs.Viewer** (ou équivalent) qui contient `SmartMarkerProcessor`
- Un classeur modèle Excel (`.xlsx`) avec un marqueur comme `${repeat:Dept}` placé dans la ligne que vous souhaitez répéter
- Une connaissance de base de C# et LINQ (facultatif mais utile)

Aucune bibliothèque tierce supplémentaire n'est requise.

## Étape 1 : Créer l'instance SmartMarkerProcessor

Le processeur orchestre le remplacement des marqueurs et la duplication des feuilles de calcul. L'instancier sans arguments utilise les options par défaut.

```csharp
// Step 1: Create a SmartMarkerProcessor instance
SmartMarkerProcessor processor = new SmartMarkerProcessor();
```

Créer le processeur tôt vous permet de configurer les options globales avant l'application de toute donnée. C’est la base pour **how to repeat worksheet** correctement.

## Étape 2 : Activer la répétition de la feuille de calcul

Par défaut, le processeur remplace les marqueurs uniquement sur la feuille actuelle. Définir `RepeatWorksheet` à `true` indique au moteur de cloner la feuille entière pour chaque élément de la collection de données.

```csharp
// Step 2: Enable worksheet repetition for the ${repeat:Dept} marker
processor.Options.RepeatWorksheet = true;
```

Activer cette option est la clé pour **generate multiple worksheets** — le processeur créera un nouvel onglet pour chaque élément du tableau `Dept` et conservera le formatage original.

## Étape 3 : Préparer la source de données sous forme de tableau ou de liste

SmartMarkerProcessor fonctionne avec n'importe quel enumerable, mais utiliser un tableau rend l'intention claire lorsque vous souhaitez **populate worksheet from list**. Ici, nous créons un objet anonyme qui contient une propriété `Dept` contenant un tableau de chaînes.

```csharp
// Step 3: Prepare the data source with a list of departments
var data = new { Dept = new[] { "HR", "IT", "Finance" } };
```

Si vous avez déjà un `List<string>`, vous pouvez le passer directement ; le processeur le traitera de la même façon. L'élément important est que le nom de la propriété (`Dept`) corresponde au marqueur `${repeat:Dept}` dans le modèle.

## Étape 4 : Charger la feuille de modèle

En supposant que vous disposez d'un `ExcelPackage` (d'EPPlus) ou d'un objet `Workbook`, récupérez la feuille que vous souhaitez répéter. La variable `ws` représente cette feuille.

```csharp
// Example using EPPlus to load the template workbook
using var package = new OfficeOpenXml.ExcelPackage(new FileInfo("Template.xlsx"));
var ws = package.Workbook.Worksheets[0]; // first worksheet
```

Si vous préférez une bibliothèque différente (p. ex., ClosedXML), le même principe s'applique : obtenez un objet feuille qui implémente l'interface requise.

## Étape 5 : Traiter la feuille avec les données

Appliquez maintenant les données au modèle. Le processeur clone la feuille pour chaque département, remplace le marqueur `${repeat:Dept}` par le nom réel du département, et laisse le reste de la feuille intact.

```csharp
// Step 5: Apply the data to the template worksheet (ws)
processor.Process(ws, data);
```

Après l'exécution de `Process`, `ws` devient la première de plusieurs feuilles — une par département. Le nom de la feuille originale est conservé, tandis que les duplicatas reçoivent des suffixes incrémentiels (par ex., « Sheet1 (1) », « Sheet1 (2) »). Vous pouvez les renommer ensuite si vous avez besoin d'un schéma de nommage personnalisé.

### Résultat attendu

Lorsque vous ouvrez le classeur résultant, vous devriez voir :

- **Sheet1** – le modèle original (souvent laissé vide ou utilisé comme maître)
- **Sheet1 (1)** – rempli avec « HR »
- **Sheet1 (2)** – rempli avec « IT »
- **Sheet1 (3)** – rempli avec « Finance »

Chaque feuille contient la même mise en page mais avec le nom du département substitué à l'endroit où `${repeat:Dept}` apparaissait.

## Gestion des cas limites

### Tableaux vides ou nuls

Si `Dept` est nul ou vide, le processeur ne créera aucune feuille supplémentaire. Pour éviter un classeur complètement vide, vous pouvez ajouter une garde :

```csharp
if (data.Dept != null && data.Dept.Any())
{
    processor.Process(ws, data);
}
else
{
    // Optionally write a warning or keep the original sheet unchanged
}
```

### Noms de feuilles personnalisés

Le schéma de nommage par défaut peut ne pas convenir à chaque exigence de reporting. Après le traitement, renommez chaque feuille en utilisant une boucle :

```csharp
for (int i = 1; i <= data.Dept.Length; i++)
{
    var sheet = package.Workbook.Worksheets[i]; // index 0 is the original
    sheet.Name = data.Dept[i - 1]; // use department name as tab title
}
```

### Remplir des colonnes supplémentaires

Si vous devez **populate excel with array** des valeurs au-delà d'un seul marqueur, étendez l'objet de données :

```csharp
var data = new
{
    Dept = new[]
    {
        new { Name = "HR", Headcount = 12 },
        new { Name = "IT", Headcount = 25 },
        new { Name = "Finance", Headcount = 8 }
    }
};
```

Puis ajustez les marqueurs du modèle à `${repeat:Dept.Name}` et `${repeat:Dept.Headcount}`. Le processeur répétera la ligne pour chaque département et remplira les deux colonnes.

## Exemple complet fonctionnel

Ci‑dessous se trouve une application console autonome qui démontre le flux complet, du chargement du modèle à l'enregistrement du classeur final.

```csharp
using System;
using System.IO;
using OfficeOpenXml;               // Install-Package EPPlus
using GroupDocs.Viewer.Markup;    // SmartMarkerProcessor namespace

class Program
{
    static void Main()
    {
        // 1️⃣ Create processor
        SmartMarkerProcessor processor = new SmartMarkerProcessor();

        // 2️⃣ Enable worksheet repetition
        processor.Options.RepeatWorksheet = true;

        // 3️⃣ Define data source (array of departments)
        var data = new { Dept = new[] { "HR", "IT", "Finance" } };

        // 4️⃣ Load template workbook (ensure Template.xlsx exists)
        var fileInfo = new FileInfo("Template.xlsx");
        using var package = new ExcelPackage(fileInfo);
        var ws = package.Workbook.Worksheets[0]; // first sheet contains ${repeat:Dept}

        // 5️⃣ Process template
        processor.Process(ws, data);

        // Optional: rename generated sheets
        for (int i = 1; i <= data.Dept.Length; i++)
        {
            var sheet = package.Workbook.Worksheets[i];
            sheet.Name = data.Dept[i - 1];
        }

        // Save the result
        var output = new FileInfo("Result.xlsx");
        package.SaveAs(output);

        Console.WriteLine("Workbook generated with repeated worksheets.");
    }
}
```

**Explication des sections clés**

- **Création du processeur** – établit le moteur qui interprétera les marqueurs.
- **Option RepeatWorksheet** – active la fonctionnalité principale qui répond à *how to repeat worksheet*.
- **Source de données** – utilise un tableau (`new[]`) pour satisfaire **populate excel with array**.
- **Chargement du modèle** – montre une façon courante d'obtenir un objet feuille.
- **Traitement** – effectue la duplication et l'insertion des données en un seul appel.
- **Renommage** – montre comment transformer les noms génériques « (1) », « (2) » en titres significatifs, une exigence typique après **generate multiple worksheets**.

L'exécution de ce programme produit `Result.xlsx` avec trois onglets spécifiques aux départements, chacun rempli à partir du tableau.

## Pièges courants et astuces professionnelles

- **Orthographe du marqueur** – le marqueur doit correspondre exactement au nom de la propriété (`${repeat:Dept}`). Une faute de frappe empêche la répétition.
- **Index de la feuille** – après le traitement, la feuille originale reste à l'index 0 ; les feuilles générées suivent séquentiellement. Un mauvais indexage peut conduire à renommer le mauvais onglet.
- **Grandes ensembles de données** – générer des centaines de feuilles peut augmenter la taille du fichier de façon spectaculaire. Envisagez de diviser les rapports ou d'utiliser une seule feuille avec des sections groupées si les performances deviennent un problème.
- **Sécurité des threads** – `SmartMarkerProcessor` n'est pas sûr pour les threads. Créez une instance séparée par thread si vous traitez plusieurs classeurs en parallèle.

## Conclusion

Vous savez maintenant **how to repeat worksheet** dans Excel en utilisant SmartMarkerProcessor, comment **populate excel with array** des données, comment **generate multiple worksheets**, et comment **populate worksheet from list** efficacement. L'exemple complet regroupe tous les concepts, et l'étape de renommage optionnelle vous permet de produire des noms d'onglets propres et conviviaux.

Ensuite, vous pourriez explorer :

- Utiliser **populate worksheet from list** avec des objets complexes (collections imbriquées)
- Appliquer le formatage conditionnel après la duplication de la feuille
- Exporter le classeur généré en PDF ou CSV pour une consommation en aval

N'hésitez pas à adapter le code à vos propres scénarios de reporting, et profitez de l'automatisation des classeurs Excel en toute confiance !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d'implémentation alternatives dans vos propres projets.

- [Comment répéter les feuilles de calcul – Guide complet pour l'automatisation Excel](/cells/english/net/smart-markers-dynamic-data/how-to-repeat-worksheets-complete-guide-for-excel-automation/)
- [Créer une feuille par élément – How to Repeat Worksheet in C#](/cells/english/net/worksheet-operations/create-worksheet-per-item-how-to-repeat-worksheet-in-c/)
- [Comment développer un tableau dans Excel et remplir un modèle](/cells/english/net/templates-reporting/how-to-expand-array-in-excel-and-populate-a-template/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}