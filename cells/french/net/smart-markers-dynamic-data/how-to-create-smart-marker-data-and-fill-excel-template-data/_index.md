---
category: general
date: 2026-10-10
description: Créez des données de marqueurs intelligents et remplissez le modèle Excel
  à l'aide des marqueurs intelligents Aspose.Cells. Suivez ce guide étape par étape
  pour automatiser les rapports Excel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create smart marker data
- fill excel template data
- use aspose.cells smart markers
language: fr
lastmod: 2026-10-10
og_description: Créez des données de marqueurs intelligents avec les marqueurs intelligents
  Aspose.Cells et remplissez les données du modèle Excel en quelques minutes. Ce guide
  vous accompagne à travers un exemple complet et exécutable.
og_image_alt: Screenshot showing the process of creating smart marker data in an Excel
  worksheet
og_title: Créer des données de marqueur intelligent et remplir les données du modèle
  Excel
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Create smart marker data and fill Excel template data using Aspose.Cells
    smart markers. Follow this step‑by‑step guide to automate Excel reports.
  headline: How to create smart marker data and fill Excel template data
  type: TechArticle
- description: Create smart marker data and fill Excel template data using Aspose.Cells
    smart markers. Follow this step‑by‑step guide to automate Excel reports.
  name: How to create smart marker data and fill Excel template data
  steps:
  - name: '**Loading the workbook** gives the processor a concrete file to work on.'
    text: '**Loading the workbook** gives the processor a concrete file to work on.'
  - name: '**Selecting the worksheet** ensures the processor scans the correct sheet;
      you can target any sheet by index or name.'
    text: '**Selecting the worksheet** ensures the processor scans the correct sheet;
      you can target any sheet by index or name.'
  - name: '**The data source** is an array of anonymous objects. Each property name
      (`fieldName`) must match the marker name inside `${Comment:fieldName}`.'
    text: '**The data source** is an array of anonymous objects. Each property name
      (`fieldName`) must match the marker name inside `${Comment:fieldName}`.'
  - name: '**`SmartMarkerProcessor`** is the engine that parses tags and performs
      the replacement.'
    text: '**`SmartMarkerProcessor`** is the engine that parses tags and performs
      the replacement.'
  - name: '**`Process`** performs the heavy lifting: it reads every `${...}` tag,
      looks up the matching property in the data source, and writes the value into
      the cell.'
    text: '**`Process`** performs the heavy lifting: it reads every `${...}` tag,
      looks up the matching property in the data source, and writes the value into
      the cell.'
  - name: '**Saving the workbook** writes the updated file to disk, ready for downstream
      consumption.'
    text: '**Saving the workbook** writes the updated file to disk, ready for downstream
      consumption.'
  - name: Open a new Excel workbook.
    text: Open a new Excel workbook.
  - name: 'In any cell where you want dynamic content, type a Smart Marker tag, for
      example:'
    text: 'In any cell where you want dynamic content, type a Smart Marker tag, for
      example:'
  - name: Save the file as `Template.xlsx`.
    text: Save the file as `Template.xlsx`.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Comment créer des données de smart marker et remplir les données d’un modèle
  Excel
url: /fr/net/smart-markers-dynamic-data/how-to-create-smart-marker-data-and-fill-excel-template-data/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment créer des données de smart marker et remplir les données du modèle Excel

Si vous devez **créer des données de smart marker** pour un classeur Excel, les smart markers d'Aspose.Cells le rendent facile. Ce tutoriel montre comment **remplir les données du modèle Excel** en utilisant les smart markers en quelques lignes de code C#.

Vous apprendrez comment intégrer des balises Smart Marker dans un modèle, fournir une source de données, exécuter le processeur et enregistrer le fichier rempli. Aucun outil externe n'est requis — seulement Aspose.Cells pour .NET et un projet C# de base.

## Ce dont vous aurez besoin

- .NET 6.0 ou ultérieur (le code fonctionne également avec .NET Framework 4.7+)
- Aspose.Cells pour .NET (package NuGet `Aspose.Cells`)
- Un classeur Excel contenant des balises Smart Marker telles que `${Comment:fieldName}`
- Un IDE C# (Visual Studio, Rider ou VS Code)

> **Astuce :** Conservez le classeur dans le même dossier que le projet ou utilisez un chemin absolu pour éviter les erreurs de fichier introuvable.

## Comment créer des données de smart marker avec Aspose.Cells

Le cœur de la solution est le `SmartMarkerProcessor`. Il analyse une feuille de calcul à la recherche de balises, récupère les valeurs correspondantes depuis une source de données et écrit les résultats dans la feuille.

```csharp
using Aspose.Cells;
using System;

// 1️⃣ Load the workbook that contains Smart Marker tags.
Workbook workbook = new Workbook("Template.xlsx");

// 2️⃣ Get the worksheet where the tags reside.
Worksheet ws = workbook.Worksheets[0];

// 3️⃣ Prepare the data source that supplies values for the markers.
var dataSource = new[]
{
    new { fieldName = "Sample comment text generated by C#." }
};

// 4️⃣ Create a SmartMarkerProcessor instance.
SmartMarkerProcessor processor = new SmartMarkerProcessor();

// 5️⃣ Process the worksheet, replacing Smart Marker tags with data from the source.
processor.Process(ws, dataSource);

// 6️⃣ Save the populated workbook.
workbook.Save("Result.xlsx");
```

### Pourquoi chaque ligne est importante

1. **Chargement du classeur** fournit au processeur un fichier concret sur lequel travailler.  
2. **Sélection de la feuille de calcul** garantit que le processeur analyse la bonne feuille ; vous pouvez cibler n'importe quelle feuille par index ou par nom.  
3. **La source de données** est un tableau d'objets anonymes. Chaque nom de propriété (`fieldName`) doit correspondre au nom du marqueur dans `${Comment:fieldName}`.  
4. **`SmartMarkerProcessor`** est le moteur qui analyse les balises et effectue le remplacement.  
5. **`Process`** effectue le travail lourd : il lit chaque balise `${...}`, recherche la propriété correspondante dans la source de données et écrit la valeur dans la cellule.  
6. **Enregistrement du classeur** écrit le fichier mis à jour sur le disque, prêt pour une utilisation en aval.

## Préparer le modèle Excel pour **remplir les données du modèle Excel**

1. Ouvrez un nouveau classeur Excel.  
2. Dans n'importe quelle cellule où vous souhaitez du contenu dynamique, saisissez une balise Smart Marker, par exemple :

   ```
   ${Comment:fieldName}
   ```

3. Enregistrez le fichier sous le nom `Template.xlsx`.  

La syntaxe de la balise suit le modèle `${<CollectionName>:<PropertyName>}`. Dans cet exemple simple, nous omettons le nom de collection et nous nous appuyons sur la collection par défaut, qui est la source de données transmise à `Process`.

> **Cas limite :** Si la balise fait référence à une propriété qui n'existe pas dans la source de données, Aspose.Cells laisse la cellule inchangée. Vérifiez toujours que les noms de propriétés correspondent exactement, y compris la sensibilité à la casse.

## Construire la source de données pour **utiliser les smart markers d'Aspose.Cells**

Vous pouvez fournir n'importe quelle collection énumérable — tableaux, `List<T>`, `DataTable` ou même des objets personnalisés. Le processeur parcourt la collection et répète les lignes pour chaque élément lorsqu'un marqueur de type tableau est utilisé.

```csharp
// Example with a List<T>
var comments = new List<Comment>
{
    new Comment { fieldName = "First comment." },
    new Comment { fieldName = "Second comment." }
};

processor.Process(ws, comments);
```

```csharp
public class Comment
{
    public string fieldName { get; set; }
}
```

Lorsque vous fournissez plusieurs lignes, Aspose.Cells étend automatiquement la région du modèle pour accueillir tous les éléments, ce qui est utile pour générer des rapports, des factures ou des tableaux basés sur des données.

## Traiter la feuille de calcul en utilisant les **smart markers d'Aspose.Cells**

La méthode `Process` peut accepter des paramètres optionnels, tels que :

- `SmartMarkerOptions` pour contrôler la façon dont les cellules vides sont gérées.
- `DataSourceOptions` pour spécifier un nom de collection différent.

```csharp
SmartMarkerOptions options = new SmartMarkerOptions
{
    // Preserve empty cells as blanks instead of removing them.
    PreserveEmptyCells = true
};

processor.Process(ws, dataSource, options);
```

Ces options vous offrent un contrôle granulaire sur l'opération de **remplir les données du modèle Excel**, garantissant que la sortie correspond à vos exigences de formatage.

## Enregistrer le résultat et vérifier la sortie

Après le traitement, vous pouvez enregistrer le classeur dans n'importe quel format pris en charge par Aspose.Cells, tel que XLSX, CSV ou PDF.

```csharp
workbook.Save("Result.pdf", SaveFormat.Pdf);
```

Ouvrez `Result.xlsx` (ou `Result.pdf`) pour vérifier que le texte de substitution `${Comment:fieldName}` a été remplacé par **Sample comment text generated by C#**. Si la cellule affiche toujours la balise d'origine, revérifiez le nom de la propriété dans la source de données.

## Pièges courants et comment les éviter

| Problème | Cause | Solution |
|----------|-------|----------|
| Balise non remplacée | Incohérence du nom de propriété (par ex., `fieldname` vs `fieldName`) | Assurez-vous d'une correspondance exacte sensible à la casse |
| Lignes non dupliquées | La source de données ne contient qu'un seul objet alors que le modèle attend un tableau | Fournissez une collection avec plusieurs éléments |
| Le classeur plante lors de l'enregistrement | Utilisation d'une version obsolète d'Aspose.Cells | Mettez à jour vers le dernier package NuGet |
| Mise en forme perdue | Le processeur écrase le style de la cellule | Conservez le style avec `SmartMarkerOptions.PreserveCellFormatting = true` |

## Exemple complet fonctionnel

Voici un programme autonome que vous pouvez copier, coller et exécuter.

```csharp
using Aspose.Cells;
using System;
using System.Collections.Generic;

namespace SmartMarkerDemo
{
    class Program
    {
        static void Main()
        {
            // Load the template that contains the Smart Marker tag ${Comment:fieldName}
            Workbook workbook = new Workbook("Template.xlsx");
            Worksheet ws = workbook.Worksheets[0];

            // Create a list of data objects – each object maps to the marker property.
            var data = new List<Comment>
            {
                new Comment { fieldName = "First generated comment." },
                new Comment { fieldName = "Second generated comment." },
                new Comment { fieldName = "Third generated comment." }
            };

            // Initialise the processor and run it.
            SmartMarkerProcessor processor = new SmartMarkerProcessor();
            processor.Process(ws, data);

            // Save the populated workbook.
            workbook.Save("Result.xlsx");
            Console.WriteLine("Smart marker processing complete. Check Result.xlsx.");
        }
    }

    public class Comment
    {
        public string fieldName { get; set; }
    }
}
```

**Résultat attendu :** Dans `Result.xlsx`, la cellule qui contenait initialement `${Comment:fieldName}` s'étend sur trois lignes, chacune remplie avec le texte de commentaire correspondant de la liste `data`.

## Conclusion

Vous savez maintenant comment **créer des données de smart marker**, **remplir les données du modèle Excel**, et **utiliser les smart markers d'Aspose.Cells** pour automatiser la génération de rapports Excel. Le processus se résume à trois actions : intégrer des balises Smart Marker, fournir une source de données correspondante, et invoquer `SmartMarkerProcessor.Process`. À partir de là, vous pouvez explorer des scénarios plus avancés tels que les collections imbriquées, le formatage conditionnel ou l'exportation en PDF.

### Prochaines étapes

- Expérimentez avec les **smart markers de type tableau** pour générer automatiquement des tables à plusieurs lignes.  
- Combinez les smart markers avec le **formatage conditionnel** pour mettre en évidence les lignes qui répondent à certains critères.  
- Consultez la documentation d'Aspose.Cells sur les **options Smart Marker** pour l'optimisation des performances.

Bon codage, et profitez du temps gagné en automatisant vos flux de travail Excel !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques présentées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités supplémentaires de l'API et explorer des approches d'implémentation alternatives dans vos propres projets.

- [Automatiser les classeurs Excel avec Aspose.Cells .NET : Utiliser les Smart Markers pour un traitement efficace des données](/cells/english/net/automation-batch-processing/automate-excel-aspose-cells-workbook-smart-markers/)
- [Maîtriser les Smart Markers d'Aspose.Cells .NET & l'intégration DataTable pour une gestion efficace des données dans Excel](/cells/english/net/import-export/aspose-cells-net-smart-markers-data-table-integration/)
- [Fusion de données Excel en C# – Guide complet des Smart Markers](/cells/english/net/smart-markers-dynamic-data/excel-data-merging-in-c-complete-smart-marker-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}