---
category: general
date: 2026-05-23
description: Créez un tableau Excel dynamique à l'aide d'un modèle et de données JSON.
  Apprenez à charger un modèle Excel, automatiser un rapport Excel et remplir Excel
  à partir de JSON rapidement.
draft: false
keywords:
- create dynamic excel table
- load excel template
- automate excel report
- populate excel from json
- generate excel report json
language: fr
og_description: Créez un tableau Excel dynamique en quelques minutes avec un modèle
  et du JSON. Ce tutoriel montre comment charger le modèle Excel, automatiser le rapport
  Excel et remplir Excel à partir du JSON.
og_title: Créer un tableau Excel dynamique – Guide Smart Marker
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: Create dynamic excel table using a template and JSON data. Learn how
    to load excel template, automate excel report, and populate excel from json quickly.
  headline: Create Dynamic Excel Table – Smart Marker Guide
  type: TechArticle
tags:
- Excel
- Smart Markers
- JSON
- .NET
title: Créer un tableau Excel dynamique – Guide du marqueur intelligent
url: /fr/net/smart-markers-dynamic-data/create-dynamic-excel-table-smart-marker-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un tableau Excel dynamique – Guide Smart Marker

Vous avez déjà eu besoin de **create dynamic excel table** qui s'étend automatiquement pour chaque enregistrement de votre jeu de données ? Vous n'êtes pas le seul. Que vous construisiez un tableau de bord de ventes mensuel ou un pack de factures par client, la capacité de **populate excel from json** sans écrire de boucles infinies peut vous faire gagner des heures.

Dans ce tutoriel, nous parcourrons une solution complète et pratique qui vous montre comment **load excel template**, intégrer un Smart Marker, le nourrir avec du JSON, et enfin générer un **automate excel report**. À la fin, vous disposerez d'un projet .NET prêt à l'exécution qui produit un classeur Excel soigné à partir d'une seule charge JSON.

---

## Ce dont vous aurez besoin

- **Aspose.Cells for .NET** (ou toute bibliothèque qui prend en charge les Smart Markers). L'exemple utilise la version 24.5, mais toute version récente fonctionne.
- Visual Studio 2022 (ou votre IDE C# préféré).
- Un fichier de modèle Excel simple (`template.xlsx`) placé dans un dossier que vous contrôlez.
- Une chaîne JSON contenant une collection nommée `Customers`.

C’est tout—pas de services supplémentaires, pas de connexions à une base de données, juste du code pur.

---

## Étape 1 : Créer un classeur modèle – Load Excel Template

La première chose que nous faisons est de **load excel template** en mémoire. Considérez le modèle comme une toile où un espace réservé spécial indique au processeur où répéter les lignes.

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

// Load the template workbook (make sure the path is correct)
Workbook workbook = new Workbook(@"C:\Reports\template.xlsx");

// Grab the first worksheet – this is where our Smart Marker lives
Worksheet worksheet = workbook.Worksheets[0];
```

> **Pourquoi c'est important :** Charger le modèle une seule fois minimise les entrées/sorties de fichiers et vous permet de réutiliser la même mise en page pour de nombreux rapports. Cela isole également la logique du Smart Marker du reste de votre code, ce qui constitue une séparation claire des responsabilités.

---

## Étape 2 : Insérer un Smart Marker – Create Dynamic Excel Table

Nous intégrons maintenant un **Smart Marker** qui répétera un tableau pour chaque entrée de la collection `Customers`. La syntaxe `${Customers.RepeatWorksheet}` indique à Aspose.Cells de cloner la feuille de calcul entière pour chaque client.

```csharp
// Place the Smart Marker in cell A1 (top‑left corner)
worksheet.Cells[0, 0].PutValue("${Customers.RepeatWorksheet}");
```

> **Astuce :** Si vous avez seulement besoin de répéter des lignes au lieu de feuilles de calcul entières, utilisez `${Customers.Repeat}` sur la première ligne du tableau. La répétition au niveau de la feuille est pratique lorsque chaque client obtient son propre onglet.

---

## Étape 3 : Préparer le SmartMarkerProcessor – Automate Excel Report

Avec le marqueur en place, nous créons un `SmartMarkerProcessor`. Cet objet orchestre la liaison des données entre le JSON et le modèle Excel.

```csharp
// Initialize the processor with the workbook that contains the marker
SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);
```

Le processeur est léger ; vous pouvez le réutiliser pour plusieurs charges JSON si vous le souhaitez.

---

## Étape 4 : Alimenter les données JSON – Populate Excel from JSON

C’est ici que la magie opère. Nous alimentons une chaîne JSON contenant un tableau de clients. Chaque client peut avoir des champs comme `Name`, `Email` et `Total`.

```csharp
// Sample JSON data – in a real scenario you might read this from a file or API
string customersJson = @"
{
  ""Customers"": [
    { ""Name"": ""Acme Corp"", ""Email"": ""contact@acme.com"", ""Total"": 12500 },
    { ""Name"": ""Globex"", ""Email"": ""sales@globex.com"", ""Total"": 9800 },
    { ""Name"": ""Initech"", ""Email"": ""info@initech.com"", ""Total"": 15400 }
  ]
}";

// Apply the JSON to the processor – this populates the workbook
processor.ApplyJson(customersJson);
```

> **Pourquoi le JSON ?** Le JSON est indépendant du langage et facile à générer à partir d'API, de bases de données ou même d'une saisie manuelle. Utiliser `ApplyJson` signifie que vous n’avez pas besoin de mapper les objets manuellement ; le processeur fait le travail lourd.

---

## Étape 5 : Enregistrer le résultat – Generate Excel Report JSON

Enfin, nous écrivons le classeur rempli sur le disque. Le fichier de sortie contient maintenant une feuille de calcul distincte pour chaque client, chacune remplie avec les données de notre JSON.

```csharp
// Save the filled workbook – choose a path that makes sense for your app
workbook.Save(@"C:\Reports\output.xlsx");
```

### Résultat attendu

- **output.xlsx** contiendra trois feuilles de calcul nommées `Sheet1`, `Sheet2`, `Sheet3` (ou toute convention de nommage utilisée par votre modèle).
- Chaque feuille affichera les valeurs `Name`, `Email` et `Total` pour un seul client.
- La mise en page que vous avez conçue dans `template.xlsx` (en-têtes, styles, formules) est préservée sur toutes les feuilles générées.

---

## Exemple complet fonctionnel

Ci-dessous le programme complet, prêt à l'exécution. Copiez‑collez‑le dans une application console, ajustez les chemins de fichiers, et appuyez sur **F5**.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace DynamicExcelDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the template workbook
            string templatePath = @"C:\Reports\template.xlsx";
            Workbook workbook = new Workbook(templatePath);
            Worksheet worksheet = workbook.Worksheets[0];

            // 2️⃣ Insert the Smart Marker that repeats the worksheet per customer
            worksheet.Cells[0, 0].PutValue("${Customers.RepeatWorksheet}");

            // 3️⃣ Create the SmartMarkerProcessor
            SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);

            // 4️⃣ JSON data containing a collection of customers
            string customersJson = @"
            {
                ""Customers"": [
                    { ""Name"": ""Acme Corp"", ""Email"": ""contact@acme.com"", ""Total"": 12500 },
                    { ""Name"": ""Globex"", ""Email"": ""sales@globex.com"", ""Total"": 9800 },
                    { ""Name"": ""Initech"", ""Email"": ""info@initech.com"", ""Total"": 15400 }
                ]
            }";

            // Apply the JSON – this populates the workbook dynamically
            processor.ApplyJson(customersJson);

            // 5️⃣ Save the generated report
            string outputPath = @"C:\Reports\output.xlsx";
            workbook.Save(outputPath);

            Console.WriteLine($"✅ Dynamic Excel report generated at: {outputPath}");
        }
    }
}
```

Exécutez le programme, ouvrez `output.xlsx`, et vous verrez un **create dynamic excel table** en action—chaque client obtient sa propre feuille, entièrement formatée comme vous l’avez conçue.

---

## Questions fréquentes & cas limites

| Question | Réponse |
|----------|--------|
| *Et si mon JSON contient des objets imbriqués ?* | Les Smart Markers prennent en charge la notation point (`${Customers.Address.City}`) tant que la hiérarchie JSON correspond. |
| *Puis-je nommer les feuilles de calcul générées d'après le client ?* | Oui—ajoutez un marqueur comme `${Customers.Name}` dans la cellule du nom de la feuille ou utilisez `processor.ApplyJson(customersJson, "Customers")` avec un modèle de nommage. |
| *Qu'en est-il des grands ensembles de données (plus de 10 k lignes) ?* | Le processeur diffuse les données efficacement, mais surveillez la mémoire. Envisagez de diviser le rapport en plusieurs fichiers si vous atteignez les limites de performances. |
| *Ai-je besoin d'une licence pour Aspose.Cells ?* | Une évaluation gratuite suffit pour les tests, mais une version sous licence supprime les filigranes d'évaluation et donne accès à toutes les fonctionnalités. |
| *Puis-je utiliser cette approche avec .NET Core ?* | Absolument—Aspose.Cells prend en charge .NET 6/7/8. Il suffit de référencer le package NuGet et le code reste identique. |

---

## Conseils pour des implémentations prêtes pour la production

- **Validate JSON** avant de le fournir à `ApplyJson`. Une charge mal formée déclenchera une `JsonParseException`.
- **Cache the template** si vous générez de nombreux rapports en peu de temps ; charger depuis le disque à plusieurs reprises entraîne des I/O inutiles.
- **Lock the workbook** pendant le traitement si vous exécutez cela dans un service web multithread afin d'éviter les conditions de concurrence.
- **Add error handling** autour de `workbook.Save` pour gérer gracieusement les problèmes de permissions ou les fichiers verrouillés.
- **Customize styling** dans le modèle (mise en forme conditionnelle, formules) afin que les feuilles générées conservent la logique métier sans code supplémentaire.

---

## Conclusion

Vous disposez maintenant d’un modèle complet, de bout en bout, pour **create dynamic excel table** en utilisant un modèle, des Smart Markers et des données JSON. En **load excel template**, en insérant un marqueur de répétition, et en **populate excel from json**, vous pouvez **automate excel report** avec seulement quelques lignes de C#.

Prochaines étapes ? Essayez d’ajouter des graphiques qui font référence aux tableaux dynamiques, ou d’exporter le même JSON en PDF avec Aspose.Words. Vous pourriez également expérimenter avec **generate excel report json** à partir d’une requête de base de données pour boucler la boucle.

## Tutoriels associés

- [Create a Pivot Table in Excel Using Aspose.Cells for .NET](/cells/english/net/pivot-tables/create-pivot-table/)
- [Create Dynamic Line Charts in Excel Using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/charts-graphs/create-line-charts-excel-aspose-cells-dotnet/)
- [How to Create Checkboxes in Excel using Aspose.Cells for .NET | Data Validation Tutorial](/cells/english/net/data-validation/create-checkboxes-net-excel-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}