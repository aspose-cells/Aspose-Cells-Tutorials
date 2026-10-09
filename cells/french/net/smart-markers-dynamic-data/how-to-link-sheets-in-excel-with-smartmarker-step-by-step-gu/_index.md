---
category: general
date: 2026-06-08
description: Comment lier les feuilles dans Excel en utilisant SmartMarkerProcessor
  pour les rapports maître‑détail. Remplissez la feuille maître et générez un rapport
  Excel maître‑détail sans effort.
draft: false
keywords:
- how to link sheets
- populate master sheet
- create master detail excel
- generate master detail report
language: fr
og_description: Comment lier des feuilles dans Excel en utilisant SmartMarkerProcessor.
  Apprenez à remplir la feuille principale et à générer un rapport maître‑détail en
  quelques minutes.
og_title: Comment lier des feuilles dans Excel avec SmartMarker – Étape par étape
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: How to link sheets in Excel using SmartMarkerProcessor for master‑detail
    reports. Populate master sheet and generate a master detail Excel report effortlessly.
  headline: How to Link Sheets in Excel with SmartMarker – Step‑by‑Step Guide
  type: TechArticle
- description: How to link sheets in Excel using SmartMarkerProcessor for master‑detail
    reports. Populate master sheet and generate a master detail Excel report effortlessly.
  name: How to Link Sheets in Excel with SmartMarker – Step‑by‑Step Guide
  steps:
  - name: Multiple Detail Rows per Master
    text: If a master row has several related details, SmartMarker repeats the master
      row once and then writes *all* matching detail rows beneath it. No extra code
      is needed—just ensure your `Details` collection contains every row.
  - name: Missing Details
    text: When a master entry has no matching detail rows, the detail sheet simply
      skips that section. If you need a placeholder (e.g., “No items”), you can add
      a calculated column in the template that uses an Excel formula like `=IF(COUNTA(A2:B2)=0,"No
      items","")`.
  - name: Large Datasets
    text: 'Processing tens of thousands of rows can be memory‑intensive. To keep performance
      snappy:'
  - name: Custom Column Mapping
    text: If your property names don’t line up (`MasterKey` vs `Id`), you can use
      the `SmartMarkerProcessor.Map` method to create an alias before processing.
  type: HowTo
tags:
- Excel
- SmartMarker
- C#
- master‑detail
title: Comment lier des feuilles dans Excel avec SmartMarker – Guide étape par étape
url: /fr/net/smart-markers-dynamic-data/how-to-link-sheets-in-excel-with-smartmarker-step-by-step-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment lier des feuilles dans Excel avec SmartMarker – Guide étape par étape

Vous vous êtes déjà demandé **comment lier des feuilles** dans Excel sans copier manuellement des lignes ou écrire d'innombrables boucles VBA ? Vous n'êtes pas seul. La plupart des développeurs se heurtent à un mur lorsqu'ils ont besoin d'un rapport maître‑détail propre qui reste synchronisé au fur et à mesure que les données changent. Bonne nouvelle ? SmartMarkerProcessor fait le travail lourd pour vous, transformant quelques lignes de C# en un classeur maître‑détail complet.

Dans ce tutoriel, nous parcourrons les étapes exactes pour **remplir la feuille maître**, configurer la feuille de détail, et enfin **générer le rapport maître‑détail** qui se met à jour automatiquement. À la fin, vous disposerez d'un modèle réutilisable que vous pourrez intégrer à n'importe quel projet .NET.

> **Note de prérequis :** Vous avez besoin de GrapeCity Documents for Excel (GcExcel) version 2024 ou ultérieure, d'un environnement de développement .NET (Visual Studio 2022 fonctionne très bien), et d'une connaissance de base du C#. Aucun package NuGet supplémentaire au-delà de GcExcel n'est requis.

---

## Aperçu de la solution

Avant de plonger dans le code, décomposons ce que signifie réellement « lier des feuilles » dans le contexte de SmartMarker :

1. **Master sheet** – Contient une ligne par entité (par ex., une liste de clients).
2. **Detail sheet** – Contient les lignes qui appartiennent à une ligne maître (par ex., les commandes de chaque client).
3. **SmartMarker syntax** – Un petit langage de balisage (`{MasterSheet}#master;{DetailSheet}#detail`) qui indique au processeur comment lier les deux tables de données.
4. **Processor options** – Activer `MasterDetail` fait que le moteur répète automatiquement les lignes maîtres et intègre les lignes de détail associées en dessous.

Comprendre ces éléments vous aide à ajuster l'approche plus tard — peut-être avez‑vous besoin d'un imbriquement à trois niveaux ou d'un formatage conditionnel. Gardez ce modèle mental à portée de main pendant que nous parcourons l'implémentation.

---

## Étape 1 : Préparer les données hiérarchiques pour le traitement maître‑détail

La première chose dont vous avez besoin est une source de données qui reflète la relation maître‑détail. Dans la plupart des scénarios réels, cela provient d'une base de données, mais pour plus de clarté nous utiliserons un littéral d'objet anonyme.

```csharp
// Step 1: Prepare hierarchical data for master‑detail processing
var sampleData = new
{
    // Master collection – one row per category
    Master = new[]
    {
        new { Id = 1, Name = "A" },
        new { Id = 2, Name = "B" }
    },

    // Detail collection – rows reference MasterId
    Details = new[]
    {
        new { MasterId = 1, Item = "Item1" },
        new { MasterId = 2, Item = "Item2" }
    }
};
```

**Pourquoi c'est important :** SmartMarker ne devine pas magiquement les relations ; il recherche des noms de propriétés correspondants (`MasterId` → `Id`). En structurant les données de cette manière, nous fournissons au processeur une carte claire, ce qui est la pierre angulaire de **comment lier des feuilles** efficacement.

> **Astuce pro :** Si vos données résident dans des objets `DataTable`, exposez‑les simplement comme des propriétés avec les mêmes noms — SmartMarker fonctionne avec n'importe quelle collection énumérable.

---

## Étape 2 : Créer un classeur et charger un modèle

SmartMarker fonctionne sur un classeur Excel existant, généralement un modèle qui contient déjà les noms de feuilles et les marqueurs de substitution. Créons un classeur en mémoire et ajoutons deux feuilles de calcul vierges nommées *MasterSheet* et *DetailSheet*.

```csharp
using GrapeCity.Documents.Excel;

// Step 2: Create a workbook and add template sheets
IWorkbook wb = new Workbook();

// Create the master sheet and add a header row
IWorksheet masterSheet = wb.Worksheets.Add("MasterSheet");
masterSheet.Range["A1"].Value = "ID";
masterSheet.Range["B1"].Value = "Name";

// Create the detail sheet and add its header
IWorksheet detailSheet = wb.Worksheets.Add("DetailSheet");
detailSheet.Range["A1"].Value = "Master ID";
detailSheet.Range["B1"].Value = "Item";
```

Vous pouvez également charger un fichier `.xlsx` depuis le disque (`wb.Open("Template.xlsx")`) si vous préférez concevoir la mise en page d'abord dans Excel. L'important est que les noms des feuilles correspondent à ceux que vous référencerez dans la chaîne SmartMarker.

---

## Étape 3 : Instancier SmartMarkerProcessor et activer le mode maître‑détail

Nous introduisons maintenant le moteur qui lira les marqueurs et collera les données. Le `SmartMarkerProcessor` prend le classeur comme argument du constructeur, et le drapeau `Options.MasterDetail` indique de traiter les marqueurs `#master` et `#detail` comme une paire liée.

```csharp
// Step 3: Create a SmartMarkerProcessor for the workbook
SmartMarkerProcessor processor = new SmartMarkerProcessor(wb);

// Enable master‑detail mode on the processor options
processor.Options.MasterDetail = true;
```

**Pourquoi activer `MasterDetail` ?** Sans ce drapeau, le processeur traiterait `{MasterSheet}#master` et `{DetailSheet}#detail` comme des opérations indépendantes, perdant la relation cruciale entre les lignes. Activer ce drapeau est la seule ligne qui fait réellement fonctionner **comment lier des feuilles**.

---

## Étape 4 : Définir la chaîne SmartMarker et exécuter le processeur

La chaîne de marqueurs indique à SmartMarker quelle feuille est la maître et laquelle est la détail. La syntaxe est simple : `{SheetName}#master;{SheetName}#detail`. Vous pouvez également ajouter des marqueurs supplémentaires (par ex., `#header`) mais ils ne sont pas nécessaires pour un rapport de base.

```csharp
// Step 4: Execute the smart‑marker processing, linking master and detail sheets
string marker = "{MasterSheet}#master;{DetailSheet}#detail";
processor.Process(marker, sampleData);
```

Lorsque `Process` s'exécute, le moteur :

1. Écrit chaque ligne maître dans *MasterSheet* en commençant à la première ligne vide après l'en-tête.
2. Pour chaque ligne maître, il parcourt la collection `Details`, sélectionne les lignes où `MasterId` correspond à l'`Id` maître, et les écrit dans *DetailSheet* directement sous l'entrée maître correspondante.

---

## Étape 5 : Enregistrer ou exporter le classeur résultant

À ce stade, vous avez un classeur entièrement rempli. Vous pouvez l'enregistrer sur le disque, le diffuser vers un client web, ou même le convertir en PDF.

```csharp
// Save the workbook to a file (you could also stream it to a response)
wb.Save("MasterDetailReport.xlsx");
```

Ouvrez le fichier et vous verrez deux feuilles : *MasterSheet* répertorie `A` et `B`, tandis que *DetailSheet* affiche `Item1` sous le maître `1` et `Item2` sous le maître `2`. C’est l’essence de **remplir la feuille maître** et **générer le rapport maître‑détail** en une seule fois.

---

## Vue d'ensemble visuelle

![Diagramme illustrant comment lier des feuilles dans Excel avec SmartMarkerProcessor](https://example.com/diagram.png "Diagramme de liaison des feuilles")

Le diagramme (le texte alternatif inclut le mot‑clé principal) montre le flux de données des objets C# → SmartMarkerProcessor → feuilles Excel liées.

---

## Gestion des cas limites courants

### Plusieurs lignes de détail par maître

Si une ligne maître possède plusieurs détails associés, SmartMarker répète la ligne maître une fois puis écrit *toutes* les lignes de détail correspondantes en dessous. Aucun code supplémentaire n'est nécessaire — assurez‑vous simplement que votre collection `Details` contient chaque ligne.

### Détails manquants

Lorsqu'une entrée maître n'a aucune ligne de détail correspondante, la feuille de détail saute simplement cette section. Si vous avez besoin d'un espace réservé (par ex., « No items »), vous pouvez ajouter une colonne calculée dans le modèle qui utilise une formule Excel comme `=IF(COUNTA(A2:B2)=0,"No items","")`.

### Grands ensembles de données

Le traitement de dizaines de milliers de lignes peut être gourmand en mémoire. Pour garder des performances optimales :

- Utilisez `processor.Options.EnableStreaming = true` (disponible dans GcExcel 2025+).
- Divisez les données en morceaux et traitez chaque morceau séparément, puis fusionnez les classeurs.

### Mappage de colonnes personnalisé

Si les noms de vos propriétés ne correspondent pas (`MasterKey` vs `Id`), vous pouvez utiliser la méthode `SmartMarkerProcessor.Map` pour créer un alias avant le traitement.

```csharp
processor.Map("MasterId", "Id"); // tells the engine that MasterId maps to Id
```

---

## Exemple complet fonctionnel

En réunissant tous les éléments, voici un programme complet, prêt à copier‑coller, que vous pouvez exécuter immédiatement.



## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités supplémentaires de l'API et à explorer des approches d'implémentation alternatives dans vos propres projets.

- [Formules de liens externes maîtres dans Excel avec Aspose.Cells pour Java](/cells/english/java/formulas-functions/aspose-cells-java-external-link-formulas-excel/)
- [Feuilles Excel dynamiques maîtres en Java avec Aspose.Cells&#58; Guide complet](/cells/english/java/formulas-functions/dynamic-excel-sheets-aspose-cells-java-guide/)
- [Rapports Excel dynamiques maîtres avec Aspose.Cells Java&#58; Plages nommées & Formules complexes](/cells/english/java/templates-reporting/dynamic-excel-reports-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}