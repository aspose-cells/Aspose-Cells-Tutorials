---
category: general
date: 2026-02-23
description: Comment créer un classeur avec Aspose.Cells et ajouter des marqueurs
  à l’aide d’un tableau JSON. Apprenez à ajouter des marqueurs, à utiliser un tableau
  JSON et les marqueurs intelligents Aspose.Cells en quelques minutes.
draft: false
keywords:
- how to create workbook
- how to add markers
- use json array
- smart markers aspose.cells
language: fr
og_description: Comment créer un classeur avec Aspose.Cells, ajouter des marqueurs
  et utiliser un tableau JSON. Ce guide étape par étape vous montre tout ce dont vous
  avez besoin.
og_title: Comment créer un classeur avec des marqueurs intelligents – Aspose.Cells
tags:
- Aspose.Cells
- C#
- Excel Automation
title: Comment créer un classeur avec des marqueurs intelligents – Guide Aspose.Cells
url: /fr/net/smart-markers-dynamic-data/how-to-create-workbook-with-smart-markers-aspose-cells-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment créer un classeur avec des Smart Markers – Guide Aspose.Cells

Vous vous êtes déjà demandé **comment créer un classeur** qui remplit automatiquement les données à partir d’une source JSON ? Vous n’êtes pas le seul — les développeurs demandent constamment comment ajouter des marqueurs qui extraient des valeurs de tableaux, surtout lorsqu’ils travaillent avec Aspose.Cells. La bonne nouvelle ? C’est assez simple une fois que vous avez compris le concept de smart‑marker. Dans ce tutoriel, nous allons créer un classeur, ajouter des marqueurs, utiliser un tableau JSON, et configurer les smart markers dans Aspose.Cells afin que vous puissiez générer des fichiers Excel à la volée.

Nous couvrirons tout ce que vous devez savoir : initialiser le classeur, construire une `MarkerCollection`, fournir un tableau JSON, activer le drapeau “ArrayAsSingle”, et enfin appliquer les marqueurs. À la fin, vous disposerez d’un programme C# complet qui produit un fichier Excel avec les valeurs **A**, **B** et **C** remplissant automatiquement les cellules. Aucun service externe, juste la magie pure d’Aspose.Cells.

## Prérequis

- .NET 6.0 ou supérieur (le code fonctionne également avec .NET Framework 4.6+)
- Package NuGet Aspose.Cells for .NET (`Install-Package Aspose.Cells`)
- Une compréhension de base de la syntaxe C# (si vous débutez, les extraits sont fortement commentés)
- Visual Studio ou tout autre IDE de votre choix

Si vous avez déjà tout cela, super—plongeons‑y.

## Étape 1 : Comment créer un classeur (Initialiser le fichier Excel)

La première chose dont vous avez besoin est un objet classeur vide. Pensez‑y comme une toile blanche qu’Aspose.Cells remplira ensuite avec des données.

```csharp
using System;
using Aspose.Cells;

class SmartMarkerDemo
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();               // creates an empty .xlsx in memory
        Worksheet worksheet = workbook.Worksheets[0];    // reference to the default sheet
```

> **Pourquoi c’est important :** `Workbook` est le point d’entrée de chaque opération Excel. Sans lui, vous ne pouvez pas attacher de smart markers ni enregistrer le fichier. Créer le classeur en premier garantit également un environnement propre pour les étapes suivantes.

## Étape 2 : Comment ajouter des marqueurs – Initialiser une collection de marqueurs

Les smart markers résident dans une `MarkerCollection`. Cette collection est l’endroit où vous définissez les espaces réservés (les marqueurs) et les données qui les remplaceront.

```csharp
        // Step 2: Initialise a collection for smart markers
        MarkerCollection smartMarkerCollection = new MarkerCollection();
```

> **Astuce :** Vous pouvez réutiliser la même `MarkerCollection` pour plusieurs feuilles, mais en garder une par feuille facilite le débogage.

## Étape 3 : Utiliser un tableau JSON – Ajouter un marqueur avec des données JSON

Nous ajoutons maintenant réellement un marqueur. Le texte de remplacement `{SmartMarker}` sera remplacé par le tableau JSON que nous fournissons. Le JSON doit être une chaîne représentant un tableau, par ex. `["A","B","C"]`.

```csharp
        // Step 3: Add a smart marker and provide replacement data (JSON array)
        smartMarkerCollection.Add("{SmartMarker}", "[\"A\",\"B\",\"C\"]");
```

> **Explication :** La méthode `Add` accepte deux arguments : le texte du marqueur et la source de données. Ici, la source est un tableau JSON, qu’Aspose.Cells peut analyser automatiquement. C’est le cœur de **use json array** avec les smart markers.

## Étape 4 : Configurer le marqueur – Traiter le tableau comme une valeur unique

Par défaut, Aspose.Cells développe un tableau JSON en lignes séparées. Si vous voulez que tout le tableau soit traité comme une seule valeur de cellule (utile pour des listes déroulantes ou des chaînes concaténées), activez le drapeau `ArrayAsSingle`.

```csharp
        // Step 4: Configure the marker to treat the array as a single value
        smartMarkerCollection["ArrayAsSingle"] = true;
```

> **Quand l’utiliser :** Si vous avez besoin que le tableau apparaisse dans une seule cellule (ex. : `"A,B,C"`), activez ce drapeau. Sinon, Aspose.Cells écrira chaque élément dans sa propre ligne.

## Étape 5 : Attacher les marqueurs à la feuille et les appliquer

Enfin, liez la collection de marqueurs à la feuille et indiquez à Aspose.Cells de remplacer les espaces réservés par les données réelles.

```csharp
        // Step 5: Attach the marker collection to the worksheet and apply it
        worksheet.SmartMarkers.Add(smartMarkerCollection);
        worksheet.SmartMarkers.Apply();

        // Optional: write the placeholder into a cell so you can see the replacement
        worksheet.Cells["A1"].PutValue("{SmartMarker}");

        // Save the workbook to disk
        workbook.Save("SmartMarkerResult.xlsx");
        Console.WriteLine("Workbook created successfully!");
    }
}
```

> **Résultat :** Après l’exécution du programme, `SmartMarkerResult.xlsx` contient la valeur **A** (ou le tableau complet si `ArrayAsSingle` est vrai) dans la cellule `A1`. Ouvrez le fichier pour vérifier.

### Résultat attendu

| A |
|---|
| A |   *(si `ArrayAsSingle` est false, le premier élément remplit la cellule)*

Si vous définissez `ArrayAsSingle = true`, la cellule `A1` contiendra la chaîne `["A","B","C"]`.

## Étape 6 : Comment ajouter des marqueurs – Scénarios avancés (Optionnel)

Vous vous demandez peut‑être, *et si j’ai besoin de plusieurs marqueurs ?* La réponse est simple : appelez simplement `Add` à nouveau.

```csharp
        smartMarkerCollection.Add("{SecondMarker}", "[{\"Name\":\"John\"},{\"Name\":\"Jane\"}]");
        // You can also control each marker individually:
        smartMarkerCollection["SecondMarker"] = false; // expand into rows
```

> **Pourquoi cela fonctionne :** Chaque marqueur fonctionne indépendamment, vous pouvez donc mélanger “array as single” et “expand into rows” dans la même feuille. Cette flexibilité est une caractéristique des **smart markers aspose.cells**.

## Pièges courants & comment les éviter

| Problème | Pourquoi cela se produit | Solution |
|----------|--------------------------|----------|
| Le marqueur n’est pas remplacé | Texte du marqueur manquant ou faute de frappe | Vérifiez que la cellule contient exactement la chaîne du marqueur (`{SmartMarker}`) |
| JSON non analysé | Syntaxe JSON invalide (guillemets manquants) | Utilisez un validateur JSON ou double‑échappez les guillemets dans les chaînes C# |
| Le tableau s’étend de façon inattendue | `ArrayAsSingle` laissé à la valeur par défaut `false` | Définissez `["ArrayAsSingle"] = true` pour le marqueur concerné |
| Classeur enregistré vide | `Apply()` non appelé avant `Save()` | Appelez toujours `worksheet.SmartMarkers.Apply()` avant d’enregistrer |

## Exemple complet fonctionnel (Copier‑coller)

Voici le programme complet que vous pouvez placer dans une application console. Aucun fichier supplémentaire n’est requis.

```csharp
using System;
using Aspose.Cells;

class SmartMarkerDemo
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Initialise a collection for smart markers
        MarkerCollection smartMarkerCollection = new MarkerCollection();

        // Add a smart marker and provide replacement data (JSON array)
        smartMarkerCollection.Add("{SmartMarker}", "[\"A\",\"B\",\"C\"]");

        // Configure the marker to treat the array as a single value
        smartMarkerCollection["ArrayAsSingle"] = true;

        // Attach the marker collection to the worksheet and apply it
        worksheet.SmartMarkers.Add(smartMarkerCollection);
        worksheet.SmartMarkers.Apply();

        // Place the marker in a cell so we can see the replacement
        worksheet.Cells["A1"].PutValue("{SmartMarker}");

        // Save the workbook
        workbook.Save("SmartMarkerResult.xlsx");
        Console.WriteLine("Workbook created successfully!");
    }
}
```

Exécutez le programme, ouvrez `SmartMarkerResult.xlsx`, et vous verrez le tableau JSON (ou son premier élément) proprement placé dans la cellule **A1**.

## Prochaines étapes : Étendre la solution

Maintenant que vous savez **comment créer un classeur**, **comment ajouter des marqueurs**, et **utiliser json array** avec Aspose.Cells, envisagez ces idées complémentaires :

1. **Multiples feuilles** – Parcourez une liste de feuilles et attachez différentes collections de marqueurs à chacune.
2. **JSON dynamique** – Récupérez du JSON depuis une API web (`HttpClient`) et alimentez‑le directement dans `smartMarkerCollection.Add`.
3. **Mise en forme du résultat** – Après l’application des marqueurs, formatez les cellules (polices, couleurs) pour rendre le rapport plus élégant.
4. **Formats d’exportation** – Enregistrez le classeur en PDF, CSV ou HTML en modifiant `workbook.Save("file.pdf")`.

Chacun de ces sujets implique naturellement les **smart markers aspose.cells**, vous permettant d’étendre les mêmes concepts de base que vous venez d’apprendre.

## Conclusion

Nous avons parcouru **comment créer un classeur** à partir de zéro, **comment ajouter des marqueurs**, et **comment utiliser json array** avec les smart markers d’Aspose.Cells. L’exemple complet et exécutable montre l’ensemble du flux de travail, de l’initialisation du `Workbook` à l’enregistrement du fichier final. En basculant le drapeau `ArrayAsSingle`, vous obtenez un contrôle fin sur la façon dont les données JSON apparaissent dans Excel, rendant la solution adaptable à de nombreux scénarios de reporting.

Testez le code, modifiez le JSON, et expérimentez avec d’autres marqueurs. Une fois ces blocs de construction maîtrisés, la génération de rapports Excel sophistiqués devient un jeu d’enfant. Des questions ou un cas d’usage à partager ? Laissez un commentaire ci‑dessous—bon codage !

![Diagram showing how to create workbook with smart markers in Aspose.Cells](https://example.com/images/create-workbook-smart-markers.png "how to create workbook with Aspose.Cells smart markers")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}