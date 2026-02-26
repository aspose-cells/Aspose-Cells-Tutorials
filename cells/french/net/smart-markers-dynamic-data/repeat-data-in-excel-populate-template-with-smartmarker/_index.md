---
category: general
date: 2026-02-21
description: Répétez rapidement les données dans Excel avec SmartMarker — apprenez
  à remplir un modèle Excel et à répéter les lignes sans effort.
draft: false
keywords:
- repeat data in excel
- populate excel template
- how to repeat rows
- repeat rows in excel
- populate excel from data
language: fr
og_description: Répéter des données dans Excel en utilisant SmartMarker. Apprenez
  à remplir un modèle Excel, à répéter des lignes et à automatiser vos feuilles de
  calcul.
og_title: Répéter des données dans Excel – Remplir le modèle avec SmartMarker
tags:
- excel
- csharp
- smartmarker
- automation
title: Répéter les données dans Excel – Remplir le modèle avec SmartMarker
url: /fr/net/smart-markers-dynamic-data/repeat-data-in-excel-populate-template-with-smartmarker/
---

SmartMarkerProcessor. En définissant un objet de données simple, en chargeant un classeur modèle et en appelant `Process`, vous pouvez **remplir le modèle Excel**, **répéter des lignes dans Excel**, et généralement **"

We keep trailing ** as is.

Now ensure we keep shortcodes at end and beginning unchanged.

Now produce final content with all translations.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# répéter des données dans Excel – Remplir le modèle avec SmartMarker

Vous avez déjà eu besoin de **répéter des données dans Excel** mais vous ne saviez pas comment éviter le copier‑coller manuel ? Vous n'êtes pas seul. Dans de nombreux scénarios de reporting, vous avez une liste d'éléments qui doit s'étendre automatiquement en lignes, et le faire à la main est une source d'erreurs.

Voici le principe — en utilisant le SmartMarkerProcessor de la bibliothèque **GemBox.Spreadsheet**, vous pouvez **remplir un modèle Excel** avec une seule ligne de C# et faire répéter les lignes pour chaque élément de votre collection. Dans ce guide, nous parcourrons les étapes exactes, vous montrerons le code complet et expliquerons pourquoi chaque élément est important, afin que vous puissiez répéter des lignes dans Excel en toute confiance, sans transpirer.

## Ce que vous allez apprendre

* Comment définir la structure de données qui pilote l'opération de répétition.  
* Comment connecter un `SmartMarkerProcessor` à un classeur contenant une feuille de modèle cachée.  
* Comment le marqueur `${Repeat:Item}` se développe en plusieurs lignes automatiquement.  
* Astuces pour gérer les cas limites comme les collections vides ou le formatage personnalisé.  

À la fin de ce tutoriel, vous serez capable de **remplir Excel à partir de données** de manière évolutive, facile à maintenir, et fonctionnant avec n'importe quel projet .NET.

---

## Prérequis

* .NET 6.0 ou ultérieur (le code utilise les fonctionnalités modernes de C#).  
* Le package NuGet **GemBox.Spreadsheet** (la version gratuite fonctionne jusqu'à 150 lignes).  
* Un fichier de modèle Excel de base (`Template.xlsx`) avec une feuille cachée nommée `HiddenTemplate`.  
* Une connaissance des objets C# et de LINQ est utile mais pas obligatoire.

---

## Étape 1 – Définir la structure de données à répéter

Tout d'abord, vous avez besoin d'une source de données que le moteur SmartMarker puisse parcourir. Dans la plupart des applications réelles, cela proviendra d'une base de données, d'une API ou d'un fichier CSV. Pour plus de clarté, nous utiliserons un type anonyme avec une seule propriété appelée `Item` qui contient un tableau de chaînes.

```csharp
// Step 1: Define the data that will be repeated in the template
var repeatData = new { Item = new[] { "A", "B", "C" } };
```

> **Pourquoi c'est important :** Le marqueur `${Repeat:Item}` dans le modèle Excel recherche une propriété nommée `Item`. Si vous renommez la propriété, mettez à jour le marqueur en conséquence. Cette liaison étroite garantit que le modèle reste synchronisé avec votre code, facilitant la **remplir le modèle Excel** sans deviner les noms de colonnes.

### Variantes courantes

* **Objets complexes :** Au lieu d'un simple tableau de chaînes, vous pouvez fournir une liste d'objets (`new[] { new { Name = "A", Qty = 10 } }`). Le marqueur répétera les lignes et vous pourrez référencer `${Item.Name}` et `${Item.Qty}` dans la feuille.  
* **Collections vides :** Si `Item` est vide, SmartMarker supprime simplement le bloc de répétition, laissant le modèle intact—idéal pour les sections optionnelles.

---

## Étape 2 – Créer le SmartMarkerProcessor pour la feuille de modèle cachée

Ensuite, chargez votre classeur et instanciez un `SmartMarkerProcessor`. Pointez-le vers le classeur qui contient la feuille de modèle cachée ; SmartMarker copiera cette feuille vers une feuille visible et développera les marqueurs de répétition.

```csharp
using GemBox.Spreadsheet;

// Load the workbook that holds the hidden template sheet.
var wb = ExcelFile.Load("Template.xlsx");

// Step 2: Create a SmartMarkerProcessor for the workbook that holds the hidden template sheet
var processor = new SmartMarkerProcessor(wb);
```

> **Astuce :** Si vous avez plusieurs modèles dans le même fichier, vous pouvez spécifier le nom de la feuille source lors de l'appel à `processor.Process`. Cela aide lorsque vous devez **répéter des lignes dans Excel** pour différentes sections d'un rapport.

### Gestion des cas limites

* **Feuille de modèle manquante :** Enveloppez le chargement dans un try/catch et consignez une erreur claire — cela évite les échecs silencieux lorsque le chemin du fichier est incorrect.  
* **Ensembles de données volumineux :** Pour des milliers de lignes, envisagez de diffuser la sortie vers un fichier (`processor.Save`) au lieu de tout garder en mémoire.

---

## Étape 3 – Appliquer les données et développer le marqueur `${Repeat:Item}`

Voici maintenant la ligne magique qui répète réellement les lignes. Passez l'objet que vous avez créé à l'Étape 1 à `processor.Process`. SmartMarker localisera chaque marqueur `${Repeat:Item}`, dupliquera la ligne pour chaque élément et remplacera les espaces réservés par les valeurs réelles.

```csharp
// Step 3: Apply the data to the template, expanding the ${Repeat:Item} marker
processor.Process(repeatData);

// Save the resulting workbook.
wb.Save("Result.xlsx");
```

### Ce que vous devriez voir

Lorsque vous ouvrez `Result.xlsx`, la feuille de modèle cachée a été copiée vers une nouvelle feuille visible (nommée par défaut `Sheet1`). La ligne contenant `${Repeat:Item}` apparaît maintenant trois fois, les cellules affichant respectivement **A**, **B** et **C**.

| Article |
|---------|
| A       |
| B       |
| C       |

Si vous avez ajouté d'autres colonnes comme `${Item.Price}`, elles seraient remplies automatiquement à partir de la source de données.

---

## Comment répéter des lignes dans Excel sans SmartMarker (comparaison rapide)

| Approche                | Complexité du code | Maintenance | Performance |
|-------------------------|--------------------|-------------|-------------|
| Copie‑collage manuel    | Élevée             | Faible      | Mauvaise    |
| Macro VBA               | Moyenne            | Moyenne     | Bonne       |
| **SmartMarkerProcessor**| Faible             | Élevée      | Excellente  |

Comme vous pouvez le constater, utiliser SmartMarker pour **répéter des données dans Excel** vous offre la séparation la plus propre entre la conception du modèle et la logique métier. C’est également indépendant du langage — des concepts similaires existent dans les bibliothèques Java, Python et JavaScript.

---

## Conseils avancés & pièges courants

### 1. Formater les lignes répétées

SmartMarker copie la ligne entière—y compris les styles de cellule, les bordures et le formatage conditionnel. Si vous avez besoin d'un style différent pour la première ou la dernière ligne, ajoutez des marqueurs supplémentaires comme `${If:Item.IsFirst}` et utilisez des formules conditionnelles dans Excel.

### 2. Gérer les grands ensembles de données

Lorsque vous travaillez avec > 10 000 lignes, désactivez le calcul automatique d'Excel avant le traitement :

```csharp
wb.WorkbookOptions = new WorkbookOptions { RecalculateAllFormulas = false };
```

Rétablissez-le après l'enregistrement pour maintenir des performances réactives.

### 3. Remplir Excel à partir de données d'une base réelle

```csharp
var orders = dbContext.Orders
    .Where(o => o.Date >= start && o.Date <= end)
    .Select(o => new { o.OrderId, o.CustomerName, o.Total })
    .ToArray();

processor.Process(new { Order = orders });
```

Ensuite, utilisez `${Repeat:Order}` dans le modèle pour lister chaque commande. Ce modèle montre à quel point il est facile de **remplir Excel à partir de données** directement depuis Entity Framework.

### 4. Utiliser plusieurs blocs de répétition

Vous pouvez avoir plusieurs marqueurs `${Repeat:...}` sur la même feuille ou sur des feuilles différentes. SmartMarker les traite séquentiellement, ainsi l'ordre n'a d'importance que si un bloc dépend de la sortie d'un autre.

---

## Exemple complet exécutable

Ci-dessous se trouve une application console autonome que vous pouvez coller dans Visual Studio et exécuter immédiatement. Elle démontre les trois étapes ainsi que l'enregistrement du fichier.

```csharp
using System;
using GemBox.Spreadsheet;

class Program
{
    static void Main()
    {
        // License free version (up to 150 rows). For production use, set your license key.
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 1️⃣ Define the data to repeat.
        var repeatData = new { Item = new[] { "A", "B", "C" } };

        // 2️⃣ Load the template workbook (ensure Template.xlsx exists next to the exe).
        var wb = ExcelFile.Load("Template.xlsx");

        // Create processor bound to the workbook.
        var processor = new SmartMarkerProcessor(wb);

        // 3️⃣ Process the data – this expands the ${Repeat:Item} marker.
        processor.Process(repeatData);

        // Save the populated workbook.
        wb.Save("Result.xlsx");

        Console.WriteLine("Excel file generated successfully – check Result.xlsx");
    }
}
```

**Sortie attendue :** `Result.xlsx` contient une feuille où la ligne avec `${Repeat:Item}` apparaît trois fois, affichant A, B et C. Aucun ajustement manuel n'est nécessaire.

---

## Conclusion

Vous savez maintenant comment **répéter des données dans Excel** efficacement en exploitant le SmartMarkerProcessor. En définissant un objet de données simple, en chargeant un classeur modèle et en appelant `Process`, vous pouvez **remplir le modèle Excel**, **répéter des lignes dans Excel**, et généralement **

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}