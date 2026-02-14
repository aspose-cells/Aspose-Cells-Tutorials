---
category: general
date: 2026-02-14
description: Créez un classeur Excel avec Aspose.Cells et apprenez à traiter le JSON,
  à convertir le JSON en Excel et à charger le JSON dans Excel en quelques étapes
  simples.
draft: false
keywords:
- create excel workbook
- how to process json
- convert json to excel
- load json into excel
- aspose cells json
language: fr
og_description: Créer un classeur Excel avec Aspose.Cells, apprendre à traiter le
  JSON, convertir le JSON en Excel et charger le JSON dans Excel rapidement et de
  manière fiable.
og_title: Créer un classeur Excel à partir de JSON – Tutoriel Aspose.Cells étape par
  étape
tags:
- Aspose.Cells
- C#
- JSON
- Excel automation
title: Créer un classeur Excel à partir de JSON – Guide complet d'Aspose.Cells
url: /fr/net/data-loading-and-parsing/create-excel-workbook-from-json-complete-aspose-cells-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un classeur Excel à partir de JSON – Guide complet Aspose.Cells

Vous avez déjà eu besoin de **créer un classeur Excel** à partir d'un morceau de JSON mais vous ne saviez pas par où commencer ? Vous n'êtes pas seul. De nombreux développeurs rencontrent le même problème lorsqu'ils disposent d'une charge JSON et ont besoin d'une feuille de calcul propre pour le reporting ou l'échange de données.  

Bonne nouvelle ? Avec **Aspose.Cells**, vous pouvez transformer ce JSON en un fichier Excel complet en seulement quelques lignes. Dans ce tutoriel, nous allons parcourir **comment traiter le JSON**, **convertir le JSON en Excel**, et **charger le JSON dans Excel** en utilisant le puissant `SmartMarkerProcessor`. À la fin, vous disposerez d'un classeur prêt à être enregistré et d'une vision claire des options que vous pouvez ajuster.

## Ce que vous apprendrez

- Comment configurer un projet Aspose.Cells pour la gestion du JSON.  
- Le code exact nécessaire pour **créer un classeur Excel** à partir d'un tableau JSON.  
- Pourquoi l'option `ArrayAsSingle` est importante et quand vous pourriez vouloir la modifier.  
- Conseils pour gérer des structures JSON plus volumineuses, la gestion des erreurs et l'enregistrement du fichier.  

> **Prérequis :** .NET 6+ (ou .NET Framework 4.6+), package NuGet Aspose.Cells pour .NET, et une compréhension de base du C#. Aucune autre bibliothèque n'est requise.

---

## Étape 1 : Installer Aspose.Cells et ajouter l'espace de noms requis

Avant que tout code ne s'exécute, vous devez référencer la bibliothèque Aspose.Cells dans votre projet.

```bash
dotnet add package Aspose.Cells
```

```csharp
using Aspose.Cells;   // Core namespace for workbook manipulation
```

> **Astuce pro :** Si vous utilisez Visual Studio, l'interface du Gestionnaire de packages NuGet fait le même travail — il suffit de rechercher *Aspose.Cells* et de cliquer sur Installer.

---

## Étape 2 : Préparer les données JSON à convertir

Le `SmartMarkerProcessor` fonctionne avec n'importe quelle chaîne JSON, mais vous devez décider comment la bibliothèque doit interpréter les tableaux. Dans cet exemple, nous traiterons un tableau numérique simple comme un **enregistrement unique**, ce qui est pratique lorsque vous avez simplement besoin d'une liste plate de valeurs.

```csharp
// Step 2: Define the JSON payload – an array of three numbers
string jsonData = "[1,2,3]";   // You could also load this from a file or API response
```

> **Pourquoi c'est important :** Par défaut, Aspose.Cells traite chaque élément du tableau comme un enregistrement séparé. En définissant `ArrayAsSingle = true`, tout le tableau est condensé en un seul enregistrement, ce qui correspond à de nombreux scénarios de reporting.

---

## Étape 3 : Créer une nouvelle instance de classeur

Nous allons maintenant réellement **créer un classeur Excel** en mémoire. Aucun fichier n'est encore écrit ; nous préparons simplement le conteneur.

```csharp
// Step 3: Initialise a fresh workbook – starts with a single empty worksheet
Workbook workbook = new Workbook();
```

À ce stade, `workbook.Worksheets[0]` est une feuille vierge nommée *Sheet1*. Vous pouvez la renommer plus tard si vous le souhaitez.

---

## Étape 4 : Configurer les options SmartMarker pour le traitement du JSON

La classe `SmartMarkerOptions` vous offre un contrôle granulaire sur la façon dont le JSON est interprété. Le drapeau clé pour notre scénario est `ArrayAsSingle`.

```csharp
// Step 4: Set SmartMarker options – treat the JSON array as a single record
SmartMarkerOptions options = new SmartMarkerOptions
{
    ArrayAsSingle = true   // Important when your JSON is a simple list
};
```

> **Quand le modifier :** Si votre JSON représente une collection de lignes (par ex., un tableau d'objets), laissez `ArrayAsSingle` à `false`. Chaque objet deviendra automatiquement une nouvelle ligne.

---

## Étape 5 : Exécuter le traitement Smart Marker sur la feuille de calcul

Avec le classeur et les options prêts, nous injectons le JSON dans le processeur. Le processeur parcourt la feuille à la recherche de smart markers (espaces réservés) et les remplace par les données du JSON. Comme nous n'avons aucun marqueur explicite, le processeur crée simplement une mise en page par défaut.

```csharp
// Step 5: Execute Smart Marker processing on the first worksheet
workbook.Worksheets[0].SmartMarkerProcessor.StartSmartMarkerProcessing(jsonData, options);
```

Si vous souhaitez contrôler la cellule exacte où les données commencent, vous pouvez ajouter un marqueur comme `"${Array}"` à la cellule **A1** avant d'exécuter le processeur. Pour ce tutoriel, nous nous appuyons sur le comportement par défaut, qui écrit les valeurs du tableau dans des cellules consécutives à partir de **A1**.

---

## Étape 6 : Enregistrer le classeur sur le disque (ou dans un flux)

L'étape finale consiste à persister le classeur. Vous pouvez l'enregistrer dans un fichier, un flux mémoire, ou même le renvoyer directement depuis une API web.

```csharp
// Step 6: Save the workbook as an .xlsx file
string outputPath = Path.Combine(Environment.CurrentDirectory, "JsonToExcel.xlsx");
workbook.Save(outputPath, SaveFormat.Xlsx);

Console.WriteLine($"Workbook saved to {outputPath}");
```

L'exécution du programme complet produit un fichier Excel avec les nombres **1**, **2**, et **3** placés respectivement dans les cellules **A1**, **A2**, et **A3**.

---

## Exemple complet fonctionnel

Ci-dessous se trouve l'application console complète, prête à être exécutée, qui regroupe toutes les étapes. Copiez‑collez‑la dans un nouveau projet console C# et appuyez sur **F5**.

```csharp
// ---------------------------------------------------------------
// Complete example: Create Excel workbook from JSON using Aspose.Cells
// ---------------------------------------------------------------
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Prepare JSON data
        string jsonData = "[1,2,3]";

        // 2️⃣ Create a new workbook (empty Excel file)
        Workbook workbook = new Workbook();

        // 3️⃣ Configure SmartMarker options – treat the array as a single record
        SmartMarkerOptions options = new SmartMarkerOptions
        {
            ArrayAsSingle = true
        };

        // 4️⃣ Process the JSON on the first worksheet
        workbook.Worksheets[0].SmartMarkerProcessor.StartSmartMarkerProcessing(jsonData, options);

        // 5️⃣ Optionally, add a header for clarity
        workbook.Worksheets[0].Cells["A1"].PutValue("Numbers");
        // Shift data down one row so the header stays on top
        workbook.Worksheets[0].Cells.InsertRows(1, 1);

        // 6️⃣ Save the workbook
        string outputPath = Path.Combine(Environment.CurrentDirectory, "JsonToExcel.xlsx");
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"✅ Excel workbook created at: {outputPath}");
    }
}
```

**Résultat attendu dans Excel**

| Nombres |
|---------|
| 1       |
| 2       |
| 3       |

La ligne d'en-tête (« Nombres ») est facultative mais montre comment vous pouvez mélanger des modifications manuelles de cellules avec le traitement smart‑marker.

---

## Questions fréquentes & cas particuliers

### Et si mon JSON est un objet, pas un tableau ?

```json
{
  "Name": "Alice",
  "Age": 30,
  "Country": "USA"
}
```

Vous pouvez toujours utiliser `SmartMarkerProcessor`. Placez des marqueurs comme `${Name}`, `${Age}`, `${Country}` dans la feuille, puis appelez `StartSmartMarkerProcessing`. Le processeur remplacera chaque marqueur par la valeur correspondante.

### Comment gérer de gros fichiers JSON (mégaoctets) ?

- **Streamer le JSON** : Au lieu de charger toute la chaîne, lisez le fichier avec un `StreamReader` et transmettez le texte à `StartSmartMarkerProcessing`.  
- **Augmenter la limite de mémoire** : Définissez `WorkbookSettings.MemorySetting = MemorySetting.MemoryPreference;` si vous rencontrez une `OutOfMemoryException`.  
- **Traitement par morceaux** : Divisez le JSON en tableaux plus petits et traitez chaque morceau sur une nouvelle feuille.

### Puis-je exporter en CSV au lieu de XLSX ?

Absolument. Après le traitement, il suffit d'appeler :

```csharp
workbook.Save("output.csv", SaveFormat.Csv);
```

La disposition des données reste la même ; seul le format du fichier change.

### Et si je dois formater les cellules (polices, couleurs) après le chargement du JSON ?

Vous pouvez appliquer le formatage après l'étape smart‑marker :

```csharp
Style style = workbook.CreateStyle();
style.Font.IsBold = true;
workbook.Worksheets[0].Cells["A1"].SetStyle(style);
```

Comme le processeur s'exécute d'abord, tout formatage que vous appliquez ensuite ne sera pas écrasé.

---

## Astuces & bonnes pratiques

- **Toujours définir `ArrayAsSingle` délibérément** – oublier ce drapeau est une cause fréquente de duplication inattendue des lignes.  
- **Valider le JSON avant le traitement** – une chaîne mal formée lance `JsonParseException`. Enveloppez l'appel dans un bloc `try/catch` pour une gestion d'erreur élégante.  
- **Utiliser des smart markers nommés** (`${Orders}`) pour la lisibilité, surtout lorsqu'on travaille avec des objets JSON imbriqués.  
- **Conserver le classeur en mémoire** si vous le renvoyez depuis une API web ; envoyer un `MemoryStream` évite les I/O disque inutiles.  
- **Compatibilité des versions** : Le code ci‑dessus fonctionne avec Aspose.Cells 23.12 et versions ultérieures. Consultez les notes de version si vous utilisez une version antérieure.

---

## Conclusion

Nous venons de vous montrer comment **créer un classeur Excel** à partir de JSON en utilisant Aspose.Cells, couvrant tout, de l'installation de la bibliothèque à l'enregistrement du fichier final. En maîtrisant `SmartMarkerProcessor` et ses options, vous pouvez **charger le JSON dans Excel**, **convertir le JSON en Excel**, et même personnaliser la sortie pour des scénarios de reporting complexes.  

Prêt pour l'étape suivante ? Essayez d'alimenter un tableau JSON imbriqué d'objets, ajoutez un formatage conditionnel, ou exportez le résultat en PDF — tout cela avec la même API Aspose.Cells. Vos pipelines de données vers Excel ne sont plus qu'à quelques lignes.

Si vous avez des questions ou rencontrez un problème, laissez un commentaire ci‑dessous. Bon codage, et profitez de la transformation du JSON en magnifiques feuilles de calcul ! 

![Créer un classeur Excel avec des données JSON](/images/create-excel-workbook-json.png "Illustration d'un tableau JSON transformé en feuille Excel")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}