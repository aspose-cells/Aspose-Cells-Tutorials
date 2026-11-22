---
category: general
date: 2026-11-22
description: Apprenez à créer un fichier Excel à partir de données JSON en C# avec
  Aspose.Cells Smart Marker. Ce guide pas à pas couvre la conception du modèle, la
  gestion du JSON et l'exportation du fichier.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel from json data
- Aspose.Cells
- Smart Marker
- C# Excel generation
- JSON to Excel
- Excel template
language: fr
lastmod: 2026-11-22
og_description: Créer un fichier Excel à partir de données JSON en utilisant Aspose.Cells
  Smart Marker. Suivez ce tutoriel concis pour générer un classeur entièrement formaté
  à partir d’un tableau JSON.
og_image_alt: Screenshot showing Excel workbook created from JSON data using Aspose.Cells
og_title: Créer un fichier Excel à partir de données JSON en C# – guide complet d'Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Learn to create Excel from JSON data in C# using Aspose.Cells Smart
    Marker. Step‑by‑step guide covers template design, JSON handling, and file export.
  headline: How to create Excel from JSON data with Aspose.Cells and Smart Marker
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Comment créer un fichier Excel à partir de données JSON avec Aspose.Cells et
  Smart Marker
url: /fr/net/smart-markers-dynamic-data/how-to-create-excel-from-json-data-with-aspose-cells-and-sma/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment créer un fichier Excel à partir de données JSON avec Aspose.Cells et Smart Marker

Si vous devez **créer un Excel à partir de données JSON** dans une application .NET, ce tutoriel vous montre une solution complète, prête pour la production. Vous verrez comment intégrer un tableau JSON dans une seule cellule, utiliser la fonctionnalité **Smart Marker** d’**Aspose.Cells**, et générer un classeur final sans coder manuellement cellule par cellule.

L’approche fonctionne pour n’importe quelle charge JSON — que vous exportiez des résultats d’API, sérialisiez des objets ou construisiez des rapports. À la fin du guide, vous disposerez d’un projet C# prêt à l’emploi qui lit une chaîne JSON, l’applique à un **modèle Excel**, et enregistre le résultat dans un nouveau fichier.

## Prérequis

- .NET 6.0 ou version ultérieure (le code fonctionne également avec .NET Framework 4.6+)
- Visual Studio 2022 (ou tout IDE supportant C#)
- **Aspose.Cells for .NET** package NuGet (version 23.10 ou plus récente)
- Un modèle Excel simple contenant la balise Smart Marker `<%=Fruits:ArrayAsSingle%>` dans la cellule cible

> **Astuce :** Conservez le modèle dans un dossier accessible à votre application au moment de l’exécution (par ex., `Resources` ou un chemin configurable).  

## Étape 1 : Préparer la charge JSON

Tout d’abord, définissez le tableau JSON que vous souhaitez insérer dans la feuille de calcul. Dans cet exemple, nous utilisons une liste de noms de fruits.

```csharp
// Step 1 – JSON array that will be placed in a single cell
string fruitsJson = "[\"Apple\",\"Banana\",\"Cherry\"]";
```

La chaîne JSON peut être générée dynamiquement (par ex., `JsonSerializer.Serialize(myList)`) ou lue depuis une source externe telle qu’une API REST. L’important est que la chaîne soit un tableau JSON valide, car **Smart Marker** attend une représentation JSON lorsqu’on utilise l’option `ArrayAsSingle`.

## Étape 2 : Construire la source de données Smart Marker

Le moteur Smart Marker d’Aspose.Cells fonctionne avec n’importe quel objet .NET. Nous créons un objet anonyme qui contient la chaîne JSON sous une propriété nommée `Fruits`. Le nom de la propriété doit correspondre au nom du marqueur utilisé dans le modèle.

```csharp
// Step 2 – Anonymous object serving as the Smart Marker data source
var dataSource = new
{
    Fruits = fruitsJson   // Property name "Fruits" matches the marker <%=Fruits...%>
};
```

> **Pourquoi un objet anonyme ?** Il vous permet de transmettre un conteneur de données léger sans définir de classe dédiée, ce qui accélère le prototypage. Pour des projets plus importants, vous pouvez le remplacer par un DTO fortement typé.

## Étape 3 : Concevoir le modèle Excel avec un espace réservé Smart Marker

Créez un fichier Excel (`SmartMarkerTemplate.xlsx`) contenant l’espace réservé où le JSON apparaîtra. Placez le marqueur suivant dans la cellule souhaitée (par ex., **A1**) :

```
<%=Fruits:ArrayAsSingle%>
```

- `Fruits` – correspond au nom de la propriété dans la source de données.  
- `ArrayAsSingle` – indique à Smart Marker d’écrire tout le tableau JSON comme une chaîne unique, en conservant les crochets et les guillemets.

![Excel template with Smart Marker placeholder](excel-template.png){alt="Modèle Excel contenant <%=Fruits:ArrayAsSingle%> pour créer Excel à partir de données JSON"}

## Étape 4 : Charger le classeur et initialiser le processeur Smart Marker

Chargez maintenant le fichier modèle dans une instance `Aspose.Cells.Workbook` et créez un `SmartMarkerProcessor` qui gérera le remplacement.

```csharp
// Step 4 – Load the template workbook
Workbook workbook = new Workbook("YOUR_DIRECTORY/SmartMarkerTemplate.xlsx");

// Initialise the Smart Marker processor with the loaded workbook
SmartMarkerProcessor smartMarkerProcessor = new SmartMarkerProcessor(workbook);
```

Charger le classeur une fois et réutiliser la même instance de `SmartMarkerProcessor` est plus efficace que de créer un nouveau processeur pour chaque cellule.

## Étape 5 : Appliquer la source de données pour remplacer le marqueur

La méthode `ApplyTemplate` parcourt le classeur à la recherche de tous les marqueurs et les substitue par les valeurs de l’objet fourni.

```csharp
// Step 5 – Replace the Smart Marker with the JSON content
smartMarkerProcessor.ApplyTemplate(dataSource);
```

Comme nous avons utilisé `ArrayAsSingle`, la cellule contient maintenant la chaîne JSON brute :

```
["Apple","Banana","Cherry"]
```

Si vous avez besoin d’un format différent (par ex., une liste séparée par des virgules), vous pouvez utiliser `ArrayAsCommaSeparated` à la place de `ArrayAsSingle`.

## Étape 6 : Enregistrer le classeur traité

Enfin, écrivez le classeur modifié dans un nouveau fichier. Vous pouvez choisir n’importe quel format supporté (`.xlsx`, `.xls`, `.csv`, etc.).

```csharp
// Step 6 – Save the workbook with the JSON inserted
workbook.Save("YOUR_DIRECTORY/JsonExported.xlsx");
```

Le fichier `JsonExported.xlsx` résultant peut être ouvert dans Excel, Google Sheets ou tout visualiseur compatible, et il affichera le tableau JSON exactement tel qu’il a été inséré.

## Exemple complet fonctionnel

Assembler toutes les pièces vous donne un programme console autonome :

```csharp
using Aspose.Cells;

class SmartMarkerJsonDemo
{
    static void Main()
    {
        // 1️⃣ Define the JSON array
        string fruitsJson = "[\"Apple\",\"Banana\",\"Cherry\"]";

        // 2️⃣ Create the data source object
        var dataSource = new
        {
            Fruits = fruitsJson
        };

        // 3️⃣ Load the Excel template that contains <%=Fruits:ArrayAsSingle%>
        Workbook workbook = new Workbook("YOUR_DIRECTORY/SmartMarkerTemplate.xlsx");

        // 4️⃣ Initialise the Smart Marker processor
        SmartMarkerProcessor smartMarkerProcessor = new SmartMarkerProcessor(workbook);

        // 5️⃣ Apply the data source – the marker is replaced with the JSON string
        smartMarkerProcessor.ApplyTemplate(dataSource);

        // 6️⃣ Save the result
        workbook.Save("YOUR_DIRECTORY/JsonExported.xlsx");
    }
}
```

### Résultat attendu

| A                                   |
|-------------------------------------|
| `["Apple","Banana","Cherry"]`       |

Le JSON apparaît exactement comme une chaîne dans la cellule **A1** de `JsonExported.xlsx`.

## Gestion des variations courantes et des cas limites

| Situation                                 | Ajustement recommandé |
|-------------------------------------------|------------------------|
| **Grandes objets JSON** (dictionnaires imbriqués) | Utilisez `ArrayAsJson` pour intégrer toute la hiérarchie d’objets, ou mappez le JSON vers un modèle fortement typé et utilisez des marqueurs imbriqués (`<%=Parent.Child%>`). |
| **Plusieurs tableaux JSON** dans différentes cellules | Ajoutez des propriétés supplémentaires à l’objet anonyme (par ex., `Vegetables = vegJson`) et les marqueurs correspondants (`<%=Vegetables:ArrayAsSingle%>`). |
| **Besoin de répartir le tableau sur des lignes** | Remplacez `ArrayAsSingle` par `Array` – Smart Marker créera une nouvelle ligne pour chaque élément. |
| **Modèle stocké comme ressource incorporée** | Chargez le classeur depuis un flux : `Assembly.GetExecutingAssembly().GetManifestResourceStream("Namespace.Template.xlsx")`. |
| **Exécution sous ASP.NET Core** | Utilisez `IWebHostEnvironment.ContentRootPath` pour construire le chemin complet vers le modèle et les fichiers de sortie. |

## Considérations de performance

- **Réutilisez l’objet `Workbook`** lors du traitement de nombreux enregistrements en lot ; créez le processeur une fois par classeur.  
- **Désactivez le calcul** (`workbook.CalculateFormula = false`) si le modèle contient des formules lourdes qui ne sont pas nécessaires à l’étape d’insertion du JSON.  
- **Enregistrement en flux** (`workbook.Save(stream, SaveFormat.Xlsx)`) réduit la surcharge d’E/S lorsqu’on envoie le fichier directement en réponse client.

## Conclusion

Vous savez maintenant comment **créer un Excel à partir de données JSON** en C# en utilisant **Aspose.Cells** et la fonctionnalité **Smart Marker**. Le tutoriel a couvert la préparation du JSON, la création de la source de données, la conception du modèle, le traitement du marqueur et l’enregistrement du fichier — le tout dans un programme unique et exécutable.

À partir d’ici, vous pouvez :

- Étendre le modèle avec des balises **Smart Marker** supplémentaires pour des rapports plus riches.  
- Passer à `Array` ou `ArrayAsJson` pour sortir le JSON sous forme de lignes ou de structures imbriquées.  
- Combiner cette technique avec des bibliothèques de génération Excel en C# telles qu’EPPlus ou ClosedXML si vous avez besoin d’une alternative gratuite.

Bon codage, et profitez de la transformation du JSON en classeurs Excel soignés !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Import JSON Data into Excel Using Aspose.Cells Java: A Comprehensive Guide](/cells/english/java/import-export/import-json-data-excel-aspose-cells-java/)
- [Aspose Cells GridJs tutorial – Export Excel data to JSON with lazy loading](/cells/english/python/import-and-export/aspose-cells-gridjs-tutorial-export-excel-data-to-json-with/)
- [Crear Excel a partir de JSON con Smart Marker de Aspose.Cells](/cells/spanish/net/smart-markers-dynamic-data/create-excel-from-json-with-aspose-cells-smart-marker/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}