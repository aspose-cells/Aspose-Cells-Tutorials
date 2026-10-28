---
category: general
date: 2026-02-15
description: Enregistrez rapidement un classeur Excel en exportant du JSON vers Excel
  à l'aide d'un modèle. Apprenez à générer plusieurs feuilles, à créer des feuilles
  numérotées et à automatiser les rapports.
draft: false
keywords:
- save excel workbook
- export json to excel
- generate excel from template
- generate multiple sheets
- create numbered sheets
language: fr
og_description: Enregistrez le classeur Excel en exportant du JSON vers Excel à l'aide
  d'un modèle. Ce guide montre comment générer plusieurs feuilles et créer des feuilles
  numérotées sans effort.
og_title: Enregistrer un classeur Excel à partir de JSON – Tutoriel étape par étape
tags:
- C#
- Aspose.Cells
- Excel automation
title: Enregistrer un classeur Excel à partir de JSON – Guide complet
url: /fr/net/templates-reporting/save-excel-workbook-from-json-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Enregistrer un classeur Excel à partir de JSON – Guide complet

Vous avez déjà eu besoin de **enregistrer le classeur Excel** qui est alimenté par des données JSON dynamiques ? Vous n’êtes pas le seul. Dans de nombreux scénarios de reporting, les données résident dans un service web, mais les utilisateurs métier souhaitent toujours un fichier Excel soigné — avec une mise en page de modèle et une feuille de détail séparée pour chaque enregistrement.

Voici le point : vous n’avez pas besoin d’écrire un exportateur CSV puis de créer chaque feuille manuellement. Avec le moteur **SmartMarker** d’Aspose Cells, vous pouvez **export JSON to Excel**, laisser la bibliothèque créer autant de feuilles de calcul que nécessaire, et obtenir un fichier propre où les feuilles sont automatiquement nommées « Detail », « Detail_1 », « Detail_2 », … — exactement ce à quoi vous vous attendez lorsque vous **generate multiple sheets** à partir d’un seul modèle.

Dans ce tutoriel, nous allons parcourir :

* La création d’une instance de classeur de base.  
* L’alimentation des données JSON dans le processeur SmartMarker.  
* L’utilisation de **SmartMarkerOptions** pour **create numbered sheets**.  
* L’enregistrement du résultat avec un appel unique à **save excel workbook**.

Aucun service externe, aucune concaténation de chaînes désordonnée — juste du code C# propre que vous pouvez intégrer à n’importe quel projet .NET 6+.

---

## Prérequis

Avant de commencer, assurez‑vous d’avoir :

| Exigence | Raison |
|----------|--------|
| **Aspose.Cells for .NET** (paquet NuGet `Aspose.Cells`) | Fournit `Workbook`, `SmartMarkersProcessor` et `SmartMarkerOptions`. |
| **.NET 6 SDK** (ou version ultérieure) | Fonctionnalités modernes du langage et création facile d’applications console. |
| Un **JSON payload** qui correspond aux smart markers de votre modèle Excel (nous créerons un petit exemple). | Le processeur a besoin de données pour remplacer les marqueurs. |
| Un **Excel template** (`Template.xlsx`) avec des smart markers comme `&=Customers.Name` dans la première feuille. | Le modèle définit la mise en page et l’emplacement des données. |

Si l’un de ces points vous semble inconnu, ne vous inquiétez pas — chaque puce est expliquée dans les étapes suivantes.

---

## Étape 1 : Initialiser le classeur (Save Excel Workbook – Start Here)

La première chose à faire est de créer un objet `Workbook` qui pointe vers votre fichier modèle. Pensez‑y comme à l’ouverture d’un document Word avant de commencer à taper.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

class Program
{
    static void Main()
    {
        // Load the Excel template that contains SmartMarkers.
        // Replace the path with the location of your own template.
        var workbook = new Workbook("Template.xlsx");
```

> **Why this matters:** Charger un modèle préserve toute votre mise en forme, vos formules et le texte statique. Si vous partiez d’un classeur vierge, vous devriez recréer cette mise en page manuellement — définitivement pas la façon la plus efficace de **generate excel from template**.

---

## Étape 2 : Préparer les données JSON (Export JSON to Excel – The Source)

Ensuite, nous avons besoin d’une chaîne JSON qui reflète les marqueurs du modèle. Pour cette démo, nous utiliserons une petite collection de clients.

```csharp
        // Sample JSON data – normally this would come from an API or a file.
        string jsonData = @"
        {
            ""Customers"": [
                { ""Name"": ""Alice"", ""Country"": ""USA"", ""Orders"": 5 },
                { ""Name"": ""Bob"",   ""Country"": ""Canada"", ""Orders"": 3 },
                { ""Name"": ""Carlos"", ""Country"": ""Mexico"", ""Orders"": 7 }
            ]
        }";
```

> **Pro tip:** Si vous récupérez du JSON depuis un service web, encapsulez l’appel dans un bloc `try / catch` et validez la charge utile avant de la transmettre au processeur. Un JSON incorrect déclenchera une `JsonParseException` et interrompra l’opération **save excel workbook**.

---

## Étape 3 : Configurer les options SmartMarker (Generate Multiple Sheets & Create Numbered Sheets)

Nous indiquons maintenant à Aspose comment nous voulons que les feuilles de sortie apparaissent. La propriété `DetailSheetNewName` contrôle le nom de base ; la bibliothèque ajoute un suffixe incrémental pour chaque feuille supplémentaire.

```csharp
        // Define SmartMarker options – set the base name for generated detail sheets.
        var smartMarkerOptions = new SmartMarkerOptions
        {
            DetailSheetNewName = "Detail"   // Resulting sheets: Detail, Detail_1, Detail_2, …
        };
```

> **Why this works:** `DetailSheetNewName` est la graine de l’algorithme de nommage. Si vous l’omettez, le processeur réutilisera le nom de feuille original, ce qui peut entraîner l’écrasement de données lorsqu’il y a plus d’un jeu d’enregistrements.

---

## Étape 4 : Traiter le JSON avec SmartMarkers (Generate Excel from Template)

Voici la ligne centrale qui fait le gros du travail. Elle analyse le JSON, remplace chaque smart marker et crée automatiquement les feuilles supplémentaires.

```csharp
        // Process the JSON data with SmartMarkers on the first worksheet.
        // The processor will read the markers, populate rows, and clone sheets as needed.
        workbook.Worksheets[0].SmartMarkersProcessor.Process(jsonData, smartMarkerOptions);
```

> **Common question:** *What if my template has multiple worksheets with different markers?*  
> **Answer:** Appelez `Process` sur chaque feuille que vous souhaitez remplir, ou utilisez la surcharge qui traite tout le classeur en une fois (`workbook.SmartMarkersProcessor.Process(jsonData, smartMarkerOptions);`). Cette flexibilité vous permet de **generate multiple sheets** à partir d’une source JSON unique ou de plusieurs sources indépendantes.

---

## Étape 5 : Enregistrer le classeur (Save Excel Workbook – Final Step)

Enfin, écrivez le fichier sur le disque. La méthode `Save` détermine le format à partir de l’extension du fichier, donc `.xlsx` vous donne le classeur OpenXML moderne.

```csharp
        // Save the workbook; the processor will create sheets named Detail, Detail_1, Detail_2, …
        string outputPath = @"C:\Temp\DetailSheets.xlsx";
        workbook.Save(outputPath);

        Console.WriteLine($"Workbook saved successfully to {outputPath}");
    }
}
```

> **Expected result:** Ouvrez `DetailSheets.xlsx` et vous verrez :
> 
> * **Feuille “Detail”** – contient les données du premier client.  
> * **Feuille “Detail_1”** – deuxième client.  
> * **Feuille “Detail_2”** – troisième client.
> 
> Toute la mise en forme de `Template.xlsx` est préservée, et chaque feuille est automatiquement numérotée.

---

## Cas particuliers et variantes

| Situation | Comment gérer |
|-----------|----------------|
| **Large JSON (10 k+ records)** | Augmentez `SmartMarkerOptions.MaxRecordsPerSheet` si vous souhaitez limiter le nombre de lignes par feuille, ou diffusez le JSON avec `JsonReader` pour éviter les pics de mémoire. |
| **Custom sheet naming** | Définissez `smartMarkerOptions.DetailSheetNewName = "CustomerDetail"` et utilisez éventuellement `DetailSheetNamePrefix`/`DetailSheetNameSuffix` pour plus de contrôle. |
| **Multiple master‑detail relationships** | Traitez chaque liste maître sur une feuille modèle distincte, ou combinez‑les en appelant `Process` sur différentes feuilles de calcul séquentiellement. |
| **Error handling** | Encapsulez les appels `Process` et `Save` dans `try { … } catch (Exception ex) { Console.Error.WriteLine(ex.Message); }` pour exposer les problèmes tels que les marqueurs manquants ou les erreurs de permission d’écriture. |
| **Saving to a stream (e.g., HTTP response)** | Utilisez `workbook.Save(stream, SaveFormat.Xlsx);` au lieu d’un chemin de fichier. Cela est pratique pour les API web qui renvoient directement le fichier Excel au navigateur. |

---

## Exemple complet fonctionnel (Copier‑coller prêt)

```csharp
// ---------------------------------------------------------------
// Save Excel Workbook – Export JSON to Excel with SmartMarkers
// ---------------------------------------------------------------
using System;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the template that contains SmartMarkers.
        var workbook = new Workbook("Template.xlsx");

        // 2️⃣ JSON payload – replace with your real data source.
        string jsonData = @"
        {
            ""Customers"": [
                { ""Name"": ""Alice"", ""Country"": ""USA"", ""Orders"": 5 },
                { ""Name"": ""Bob"",   ""Country"": ""Canada"", ""Orders"": 3 },
                { ""Name"": ""Carlos"", ""Country"": ""Mexico"", ""Orders"": 7 }
            ]
        }";

        // 3️⃣ Options – tell Aspose how to name generated sheets.
        var smartMarkerOptions = new SmartMarkerOptions
        {
            DetailSheetNewName = "Detail"
        };

        // 4️⃣ Process the JSON – this creates Detail, Detail_1, …
        workbook.Worksheets[0].SmartMarkersProcessor.Process(jsonData, smartMarkerOptions);

        // 5️⃣ Save the result – this is the final **save excel workbook** call.
        string outputPath = @"C:\Temp\DetailSheets.xlsx";
        workbook.Save(outputPath);

        Console.WriteLine($"✅ Workbook saved to {outputPath}");
    }
}
```

Exécutez le programme (`dotnet run` si vous utilisez un projet console) et ouvrez le fichier généré. Vous verrez trois feuilles de calcul joliment formatées, chacune remplie avec l’enregistrement client correspondant.

---

## Conclusion

Vous savez maintenant comment **save Excel workbook** en **exporting JSON to Excel**, en tirant parti d’un modèle pour **generate excel from template**, et en générant automatiquement **multiple sheets** avec la logique **create numbered sheets** intégrée. L’approche passe de quelques lignes à des milliers, fonctionne dans n’importe quel environnement .NET, et ne nécessite que quelques lignes de code.

Et après ? Essayez de remplacer la source JSON par une API en direct, ajoutez une mise en forme conditionnelle dans le modèle, ou intégrez des graphiques qui se mettent à jour par feuille. Les possibilités sont infinies, et le même schéma s’applique que vous construisiez un rapport quotidien, un générateur de factures ou un utilitaire d’exportation de données.

Des questions ou envie de partager vos propres variantes ? Laissez un commentaire ci‑dessous—bon codage ! 

![Diagramme du flux de travail SmartMarker montrant JSON → Processeur → Feuilles numérotées (enregistrer le classeur Excel)](image-placeholder.png){alt="exemple d’enregistrement du classeur Excel"}

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}