---
category: general
date: 2026-10-01
description: Apprenez à ajouter des propriétés personnalisées à un classeur Excel
  en utilisant Aspose.Cells. Ce guide montre également comment ajouter l’ID du projet
  et lire les propriétés personnalisées.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add custom properties
- how to add custom
- excel custom properties
- add project id
- read custom properties
language: fr
lastmod: 2026-10-01
og_description: Ajoutez des propriétés personnalisées à un classeur Excel avec Aspose.Cells.
  Suivez ce tutoriel complet pour ajouter un ID de projet, définir les informations
  du réviseur et lire les propriétés personnalisées de manière programmatique.
og_image_alt: Screenshot of an Excel worksheet displaying custom properties added
  via Aspose.Cells
og_title: Ajouter des propriétés personnalisées à un classeur Excel – guide étape
  par étape
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to add custom properties to an Excel workbook using Aspose.Cells.
    This guide also shows how to add project ID and read custom properties.
  headline: How to add custom properties to an Excel workbook
  type: TechArticle
- description: Learn how to add custom properties to an Excel workbook using Aspose.Cells.
    This guide also shows how to add project ID and read custom properties.
  name: How to add custom properties to an Excel workbook
  steps:
  - name: Open the saved `DataWithProps.xlsb` file in Microsoft Excel.
    text: Open the saved `DataWithProps.xlsb` file in Microsoft Excel.
  - name: Go to **File → Info → Properties → Advanced Properties**.
    text: Go to **File → Info → Properties → Advanced Properties**.
  - name: Select the **Custom** tab.
    text: Select the **Custom** tab.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Comment ajouter des propriétés personnalisées à un classeur Excel
url: /fr/net/document-properties/how-to-add-custom-properties-to-an-excel-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment ajouter des propriétés personnalisées à un classeur Excel

Si vous devez **ajouter des propriétés personnalisées** à un classeur Excel, ce guide vous montre exactement comment le faire avec Aspose.Cells for .NET. Vous apprendrez également comment ajouter un ID de projet, définir le nom d’un réviseur, et plus tard **lire les propriétés personnalisées** depuis le fichier.

Travailler avec des métadonnées personnalisées vous permet d’intégrer des informations spécifiques à l’entreprise directement dans la feuille de calcul, facilitant le suivi de la propriété, de la version ou de tout autre contexte sans maintenir une base de données séparée. Les étapes ci‑dessous couvrent le flux de travail complet de bout en bout, de la création du classeur à la persistance des nouvelles propriétés.

## Prérequis

Avant de commencer, assurez‑vous d’avoir :

* .NET 6.0 ou version ultérieure installé  
* Une licence valide d’Aspose.Cells for .NET (ou un essai gratuit)  
* Visual Studio 2022 (ou tout IDE C#)  

Aucun package NuGet supplémentaire n’est requis au-delà de `Aspose.Cells`.

## Étape 1 : Configurer le projet et importer les espaces de noms

Créez une nouvelle application console et ajoutez la référence Aspose.Cells :

```csharp
using System;
using Aspose.Cells;

namespace ExcelCustomPropertiesDemo
{
    class Program
    {
        static void Main()
        {
            // The rest of the code lives here
        }
    }
}
```

L’espace de noms `Aspose.Cells` contient les classes `Workbook`, `Worksheet` et `CustomPropertyCollection` que nous utiliserons.

## Étape 2 : Charger un classeur existant (ou en créer un nouveau)

Vous pouvez commencer avec un fichier `.xlsb` existant ou générer un nouveau classeur. L’exemple ci‑dessous charge un fichier nommé **Data.xlsb** situé dans un dossier appelé `YOUR_DIRECTORY`.

```csharp
// Load the existing workbook
var workbookPath = @"YOUR_DIRECTORY\Data.xlsb";
var workbook = new Workbook(workbookPath);
```

Si le fichier n’existe pas, remplacez le code par `new Workbook();` pour créer un classeur vierge.

## Étape 3 : Ajouter des propriétés personnalisées à la première feuille de calcul

L’opération principale consiste à **ajouter des propriétés personnalisées** à une feuille de calcul. Aspose.Cells stocke les propriétés personnalisées dans une collection qui se comporte comme un dictionnaire.

```csharp
// Get the first worksheet (index 0)
var worksheet = workbook.Worksheets[0];

// Add a numeric ProjectId property
worksheet.CustomProperties.Add("ProjectId", 12345);

// Add a string Reviewer property
worksheet.CustomProperties.Add("Reviewer", "John Doe");

// Optional: add a DateTime property for the creation timestamp
worksheet.CustomProperties.Add("CreatedOn", DateTime.UtcNow);
```

Nous utilisons `CustomProperties.Add` plutôt que `CustomProperties["Name"] = value` car la méthode `Add` crée l’entrée si elle n’existe pas et garantit que le type de données correct est stocké. Cette approche évite les incompatibilités de type accidentelles qui pourraient provoquer des erreurs d’exécution lors de la lecture des valeurs ultérieurement.

## Étape 4 : Enregistrer le classeur avec les nouvelles propriétés

Après avoir injecté les métadonnées, persistez les modifications dans un nouveau fichier afin que l’original reste intact.

```csharp
// Save the workbook with the custom properties
var outputPath = @"YOUR_DIRECTORY\DataWithProps.xlsb";
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

À ce stade, le fichier Excel contient les métadonnées personnalisées que vous avez définies. Vous pouvez vérifier les propriétés en suivant les étapes de la section suivante.

## Étape 5 : Lire les propriétés personnalisées d’un classeur

La lecture des **propriétés personnalisées Excel** suit le même modèle de collection. Cet extrait montre comment récupérer les valeurs que nous venons de stocker.

```csharp
// Load the workbook that contains custom properties
var loadedWorkbook = new Workbook(outputPath);
var loadedWorksheet = loadedWorkbook.Worksheets[0];
var props = loadedWorksheet.CustomProperties;

// Retrieve each property safely
int projectId = props["ProjectId"] != null ? (int)props["ProjectId"].Value : -1;
string reviewer = props["Reviewer"] != null ? props["Reviewer"].Value.ToString() : "Unknown";
DateTime createdOn = props["CreatedOn"] != null ? (DateTime)props["CreatedOn"].Value : DateTime.MinValue;

Console.WriteLine($"ProjectId: {projectId}");
Console.WriteLine($"Reviewer: {reviewer}");
Console.WriteLine($"CreatedOn (UTC): {createdOn:u}");
```

L’indexeur `CustomPropertyCollection` renvoie un objet `CustomProperty` ; accéder à sa propriété `Value` vous donne les données stockées dans leur type d’origine. Vérifier la valeur `null` avant de caster évite une `NullReferenceException` si une propriété est manquante.

### Sortie console attendue

```
ProjectId: 12345
Reviewer: John Doe
CreatedOn (UTC): 2026-10-01 12:34:56Z
```

L’horodatage reflétera le moment exact où vous avez appelé `Add` à l’étape 3.

## Astuce : Mettre à jour une propriété personnalisée existante

Si vous devez **ajouter des informations personnalisées** plus tard (par exemple, changer le réviseur), utilisez le setter de `CustomPropertyCollection` :

```csharp
// Change the reviewer name
if (props["Reviewer"] != null)
{
    props["Reviewer"].Value = "Jane Smith";
}
else
{
    // Property does not exist; add it
    props.Add("Reviewer", "Jane Smith");
}
```

Ce modèle garantit que la propriété est soit mise à jour, soit créée, ce qui est utile dans des flux de travail itératifs comme la génération automatisée de rapports.

## Étape 6 : Vérifier les propriétés dans Excel (optionnel)

Vous pouvez également afficher les propriétés personnalisées directement dans Excel :

1. Ouvrez le fichier `DataWithProps.xlsb` enregistré dans Microsoft Excel.  
2. Accédez à **Fichier → Info → Propriétés → Propriétés avancées**.  
3. Sélectionnez l’onglet **Personnalisées**.  

Vous verrez les entrées `ProjectId`, `Reviewer` et `CreatedOn` listées avec leurs valeurs respectives.

## Exemple complet fonctionnel

Ci‑dessous se trouve le programme complet et autonome qui combine tous les extraits précédents. Copiez‑le dans `Program.cs` et exécutez‑le ; la console affichera les valeurs récupérées.

```csharp
using System;
using Aspose.Cells;

namespace ExcelCustomPropertiesDemo
{
    class Program
    {
        static void Main()
        {
            // Paths (adjust to your environment)
            var sourcePath = @"YOUR_DIRECTORY\Data.xlsb";
            var resultPath = @"YOUR_DIRECTORY\DataWithProps.xlsb";

            // Load or create workbook
            var workbook = new Workbook(sourcePath);
            var worksheet = workbook.Worksheets[0];

            // Add custom properties
            worksheet.CustomProperties.Add("ProjectId", 12345);
            worksheet.CustomProperties.Add("Reviewer", "John Doe");
            worksheet.CustomProperties.Add("CreatedOn", DateTime.UtcNow);

            // Save the workbook
            workbook.Save(resultPath);
            Console.WriteLine($"Saved workbook with custom properties to {resultPath}");

            // Load the saved workbook to read properties
            var loadedWorkbook = new Workbook(resultPath);
            var loadedWorksheet = loadedWorkbook.Worksheets[0];
            var props = loadedWorksheet.CustomProperties;

            // Read properties
            int projectId = props["ProjectId"] != null ? (int)props["ProjectId"].Value : -1;
            string reviewer = props["Reviewer"] != null ? props["Reviewer"].Value.ToString() : "Unknown";
            DateTime createdOn = props["CreatedOn"] != null ? (DateTime)props["CreatedOn"].Value : DateTime.MinValue;

            Console.WriteLine($"ProjectId: {projectId}");
            Console.WriteLine($"Reviewer: {reviewer}");
            Console.WriteLine($"CreatedOn (UTC): {createdOn:u}");
        }
    }
}
```

L’exécution de ce programme produit la sortie console affichée précédemment et crée `DataWithProps.xlsb` contenant les métadonnées intégrées.

## Questions fréquentes et cas particuliers

| Question | Réponse |
|---|---|
| **Puis‑je stocker des types non primitifs ?** | Aspose.Cells prend en charge `string`, `int`, `double`, `DateTime` et `bool`. Pour les objets complexes, sérialisez‑les en JSON ou XML d’abord et stockez la chaîne. |
| **Que se passe‑t‑il si le classeur est protégé par mot de passe ?** | Ouvrez le classeur avec un mot de passe (`new Workbook(path, password)`) avant d’accéder à `CustomProperties`. Les propriétés restent accessibles après le déchiffrement. |
| **Les propriétés personnalisées survivent‑elles à la conversion de format ?** | Lors de l’enregistrement dans un format différent (par ex., `.xlsx`), Aspose.Cells préserve les propriétés personnalisées tant que le format cible les prend en charge. |
| **Comment supprimer une propriété personnalisée ?** | Utilisez `worksheet.CustomProperties.Remove("PropertyName");`. Cela supprime l’entrée de la collection. |

## Prochaines étapes

Maintenant que vous savez **ajouter des propriétés personnalisées**, vous pouvez explorer des sujets connexes tels que :

* **excel custom properties** pour la gestion des versions de documents  
* **read custom properties** depuis plusieurs feuilles de calcul dans un même classeur  
* Utiliser **Aspose.Cells** pour créer des tableaux croisés dynamiques qui référencent des métadonnées personnalisées  
* Exporter le classeur en PDF tout en préservant les propriétés personnalisées  

Expérimentez avec différents types de données, combinez les propriétés personnalisées avec les commentaires de cellules, ou intégrez les métadonnées dans un système de gestion documentaire plus vaste.

---

**Prêt à automatiser vos rapports Excel ?** Ajoutez le code ci‑dessus à votre projet, ajustez les noms des propriétés pour qu’ils correspondent à vos besoins métier, et vous disposerez d’une feuille de calcul auto‑descriptive prête pour le traitement en aval.

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités d’API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Créer un classeur Excel – Ajouter des propriétés personnalisées et enregistrer en XLSB](/cells/english/net/document-properties/create-excel-workbook-add-custom-properties-and-save-as-xlsb/)
- [Comment accéder aux propriétés de document personnalisées dans Excel en utilisant Aspose.Cells for .NET](/cells/english/net/workbook-operations/access-custom-excel-properties-aspose-cells-net/)
- [Maîtriser les propriétés personnalisées Excel avec Aspose.Cells .NET pour une gestion de données améliorée](/cells/english/net/data-manipulation/excel-custom-properties-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}