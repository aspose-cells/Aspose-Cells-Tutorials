---
category: general
date: 2026-10-10
description: Apprenez à traiter un modèle Excel en C# tout en nommant automatiquement
  les feuilles. Guide étape par étape avec le code SmartMarkerProcessor et les meilleures
  pratiques.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- process excel template
- automatically name sheets
- SmartMarkerProcessor
- Excel automation C#
- worksheet data binding
language: fr
lastmod: 2026-10-10
og_description: Traitez le modèle Excel en C# et nommez automatiquement les feuilles
  avec SmartMarkerProcessor. Suivez ce tutoriel détaillé pour générer des classeurs
  dynamiques.
og_image_alt: Screenshot showing process excel template with automatically named sheets
  in a C# application
og_title: Traiter le modèle Excel et nommer automatiquement les feuilles en C# – guide
  complet
schemas:
- author: GroupDocs
  dateModified: '2026-10-10'
  description: Learn how to process Excel template in C# while automatically name
    sheets. Step‑by‑step guide with SmartMarkerProcessor code and best practices.
  headline: How to process Excel template and automatically name sheets in C#
  type: TechArticle
- description: Learn how to process Excel template in C# while automatically name
    sheets. Step‑by‑step guide with SmartMarkerProcessor code and best practices.
  name: How to process Excel template and automatically name sheets in C#
  steps:
  - name: Large data sets
    text: 'When the data source contains hundreds of rows, the processor creates a
      separate sheet for each row by default. To keep the workbook from exploding,
      you can:'
  - name: Existing sheet name conflicts
    text: If the template already contains a sheet named `Detail`, the processor appends
      a numeric suffix to avoid collision (`Detail_0`, `Detail_1`, …). To enforce
      a custom conflict‑resolution strategy, inspect `Worksheet.Sheets` before processing
      and rename any conflicting sheets.
  - name: Non‑Excel templates
    text: The same `SmartMarkerProcessor` can process Word, PowerPoint, or PDF templates.
      The only change is the class you instantiate (`Document`, `Presentation`, etc.).
      The **process excel template** pattern stays identical, which means you can
      reuse the code with minimal adjustments.
  type: HowTo
tags:
- Excel
- C#
- SmartMarker
- Automation
title: Comment traiter un modèle Excel et nommer automatiquement les feuilles en C#
url: /fr/net/templates-reporting/how-to-process-excel-template-and-automatically-name-sheets/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment traiter un modèle Excel et nommer automatiquement les feuilles en C#

Si vous devez **traiter un modèle Excel** dans une application .NET, ce guide vous montre une méthode fiable pour générer des classeurs et **nommer automatiquement les feuilles**. En utilisant le `SmartMarkerProcessor` de GroupDocs.Parser, vous pouvez lier des données à un modèle, créer des feuilles de détail à la volée et garder le classeur bien organisé sans renommage manuel.

Vous terminerez le tutoriel avec un exemple complet et exécutable qui lit un modèle, applique une source de données et génère des feuilles nommées `Detail`, `Detail_1`, `Detail_2`, … Tous les espaces de noms requis, les étapes de configuration et les pièges courants sont couverts, afin que vous puissiez copier le code dans votre propre projet en toute confiance.

## Prérequis

* .NET 6.0 ou version ultérieure (le code fonctionne avec .NET Core et .NET Framework)
* Une référence au package NuGet **GroupDocs.Parser** (version 23.5 ou plus récente)
* Un modèle Excel (`Template.xlsx`) contenant des balises SmartMarker telles que `{{Table}}` pour des données maître‑détail
* Un modèle de données simple (par ex., un `DataTable` ou une liste d'objets) qui correspond aux marqueurs du modèle

Si l'un de ces éléments manque, installez le package NuGet avec :

```bash
dotnet add package GroupDocs.Parser
```

## Vue d'ensemble de la solution

La solution suit trois phases logiques :

1. **Créer une instance de `SmartMarkerProcessor`** – cet objet pilote l'ensemble du moteur de modèles.
2. **Configurer le processeur pour nommer automatiquement les feuilles de détail** – l'option `DetailSheetNewName` définit le nom de base et la bibliothèque ajoute des suffixes incrémentiels.
3. **Exécuter `Process`** – la méthode lit le modèle, fusionne la source de données et écrit le résultat dans un nouveau classeur.

Chaque phase est expliquée ci-dessous, accompagnée du code exact dont vous avez besoin.

## Étape 1 : Créer une instance de SmartMarkerProcessor

Le processeur est le point d'entrée de toutes les opérations SmartMarker. Il ne nécessite aucun argument de constructeur, mais vous pouvez passer un objet `SmartMarkerOptions` personnalisé ultérieurement si vous avez besoin de paramètres avancés.

```csharp
using GroupDocs.Parser;
using GroupDocs.Parser.Options;

// ...

// Step 1: Instantiate the processor
SmartMarkerProcessor processor = new SmartMarkerProcessor();
```

*Pourquoi c'est important* : Instancier le processeur une fois par opération maintient une faible utilisation de la mémoire et vous permet de réutiliser le même objet pour plusieurs modèles si nécessaire.

## Étape 2 : Configurer le nommage automatique des feuilles

Lorsque qu'un tableau maître‑détail s'étend sur plusieurs feuilles de calcul, la bibliothèque crée automatiquement de nouvelles feuilles. En définissant `DetailSheetNewName`, vous contrôlez le nom de base utilisé par le moteur. La bibliothèque ajoute un soulignement et un numéro incrémental pour chaque feuille supplémentaire.

```csharp
// Step 2: Define the base name for automatically created detail sheets
processor.Options.DetailSheetNewName = "Detail"; // Sheets become Detail, Detail_1, Detail_2, …
```

*Conseils* :

* Choisissez un nom de base qui ne entre pas en conflit avec les noms de feuilles existants dans le modèle.
* Le schéma de nommage fonctionne pour n'importe quel nombre de lignes de détail ; la bibliothèque cesse d'ajouter des suffixes lorsque la dernière feuille est créée.
* Si vous avez besoin d'un modèle de nommage différent (par ex., préfixe au lieu de suffixe), vous pouvez manipuler `processor.Options.DetailSheetNewName` avant chaque appel.

## Étape 3 : Traiter la feuille de calcul avec une source de données

La méthode `Process` accepte trois arguments :

* La **feuille source** (objet `Worksheet`) – vous l'obtenez en chargeant le fichier modèle.
* Le **flux cible** – où le classeur traité sera écrit.
* La **source de données** – tout objet implémentant `IDataSource` (par ex., `DataTable`, `IEnumerable<T>`).

Voici un exemple complet qui charge `Template.xlsx`, lie un `DataTable` et enregistre le résultat dans `Result.xlsx`.

```csharp
using System.Data;
using System.IO;
using GroupDocs.Parser;
using GroupDocs.Parser.Data;
using GroupDocs.Parser.Options;

// ...

// Load the Excel template into a Worksheet object
using (FileStream templateStream = File.OpenRead("Template.xlsx"))
{
    // Create a Worksheet instance from the template
    Worksheet ws = new Worksheet(templateStream);

    // Prepare a simple DataTable as the data source
    DataTable dt = new DataTable("Employees");
    dt.Columns.Add("Name", typeof(string));
    dt.Columns.Add("Department", typeof(string));
    dt.Columns.Add("Salary", typeof(decimal));

    // Populate the table with sample rows
    dt.Rows.Add("Alice", "Engineering", 95000);
    dt.Rows.Add("Bob", "Marketing", 72000);
    dt.Rows.Add("Charlie", "Sales", 68000);

    // Wrap the DataTable in a DataSource object required by SmartMarker
    IDataSource dataSource = new DataTableSource(dt);

    // Step 1 and Step 2 have already been performed earlier
    // Now process the worksheet
    using (MemoryStream resultStream = new MemoryStream())
    {
        processor.Process(ws, dataSource, resultStream);

        // Write the processed workbook to a physical file
        File.WriteAllBytes("Result.xlsx", resultStream.ToArray());
    }
}
```

*Explication des lignes clés* :

* `new Worksheet(templateStream)` lit le fichier Excel et crée une représentation en mémoire que SmartMarker peut manipuler.
* `DataTableSource` implémente `IDataSource`, permettant au processeur d'énumérer les lignes et de remplacer les marqueurs comme `{{Employees.Name}}`.
* `processor.Process(ws, dataSource, resultStream)` fusionne les données et écrit le classeur final dans `resultStream`. La méthode crée automatiquement des feuilles de détail nommées `Detail`, `Detail_1`, etc., grâce à l'option définie à l'étape 2.
* Après le traitement, le résultat est enregistré sous le nom `Result.xlsx`. Ouvrez le fichier dans Excel pour vérifier que trois feuilles de détail existent, chacune contenant les lignes du tableau `Employees`.

## Vérifier la sortie

Ouvrez `Result.xlsx` et vérifiez ce qui suit :

| Nom de la feuille | Contenu attendu |
|-------------------|-----------------|
| Detail | Ligne d'en-tête (`Name`, `Department`, `Salary`) et première ligne de données (`Alice`) |
| Detail_1 | Deuxième ligne de données (`Bob`) |
| Detail_2 | Troisième ligne de données (`Charlie`) |

Si les feuilles apparaissent avec le nom de base correct et les suffixes incrémentaux, le flux de travail **process excel template** a réussi et la fonctionnalité **automatically name sheets** a fonctionné comme prévu.

## Gestion des cas limites

### Ensembles de données volumineux

Lorsque la source de données contient des centaines de lignes, le processeur crée une feuille distincte pour chaque ligne par défaut. Pour éviter que le classeur ne devienne trop volumineux, vous pouvez :

* **Regrouper les lignes** : modifier le modèle pour utiliser un marqueur de tableau qui se répète dans une seule feuille au lieu de créer une nouvelle feuille par ligne.
* **Limiter la création de feuilles** : définir `processor.Options.MaxDetailSheets` à un nombre raisonnable (par ex., 50) et gérer le dépassement manuellement.

```csharp
processor.Options.MaxDetailSheets = 50; // Prevent more than 50 auto‑generated sheets
```

### Conflits de noms de feuilles existants

Si le modèle contient déjà une feuille nommée `Detail`, le processeur ajoute un suffixe numérique pour éviter la collision (`Detail_0`, `Detail_1`, …). Pour appliquer une stratégie de résolution de conflit personnalisée, inspectez `Worksheet.Sheets` avant le traitement et renommez les feuilles en conflit.

```csharp
foreach (var sheet in ws.Sheets)
{
    if (sheet.Name.Equals("Detail", StringComparison.OrdinalIgnoreCase))
    {
        sheet.Name = "BaseDetail";
    }
}
```

### Modèles non‑Excel

Le même `SmartMarkerProcessor` peut traiter des modèles Word, PowerPoint ou PDF. Le seul changement est la classe que vous instanciez (`Document`, `Presentation`, etc.). Le modèle **process excel template** reste identique, ce qui signifie que vous pouvez réutiliser le code avec des ajustements minimes.

## Conseils pro pour la production

* **Réutiliser le processeur** : créez un singleton `SmartMarkerProcessor` si vous traitez de nombreux modèles dans un service web. Cela réduit la surcharge d'allocation.
* **Flux au lieu de fichier** : dans les scénarios à haut débit, conservez le modèle et le résultat dans des flux mémoire afin d'éviter les E/S disque.
* **Libérer les objets** : toutes les instances de `Worksheet`, `FileStream` et `MemoryStream` implémentent `IDisposable`. Utiliser des blocs `using`, comme illustré, garantit une libération correcte des ressources.
* **Journalisation** : activez `processor.Options.Logging` pour capturer des informations détaillées sur le traitement, ce qui aide à diagnostiquer rapidement les erreurs de modèle.

## Exemple complet et exécutable

Voici le programme complet compilé dans un seul fichier. Copiez-le dans un projet console et exécutez-le ; le classeur de sortie apparaîtra dans le dossier du projet.

```csharp
using System;
using System.Data;
using System.IO;
using GroupDocs.Parser;
using GroupDocs.Parser.Data;
using GroupDocs.Parser.Options;

class ExcelTemplateProcessor
{
    static void Main()
    {
        // 1️⃣ Create the processor
        SmartMarkerProcessor processor = new SmartMarkerProcessor();

        // 2️⃣ Set automatic sheet naming
        processor.Options.DetailSheetNewName = "Detail";

        // Load the template
        using (FileStream templateStream = File.OpenRead("Template.xlsx"))
        {
            Worksheet ws = new Worksheet(templateStream);

            // Build a sample data source
            DataTable dt = new DataTable("Employees");
            dt.Columns.Add("Name", typeof(string));
            dt.Columns.Add("Department", typeof(string));
            dt.Columns.Add("Salary", typeof(decimal));
            dt.Rows.Add("Alice", "Engineering", 95000);
            dt.Rows.Add("Bob", "Marketing", 72000);
            dt.Rows.Add("Charlie", "Sales", 68000);
            IDataSource dataSource = new DataTableSource(dt);

            // 3️⃣ Process the worksheet
            using (MemoryStream resultStream = new MemoryStream())
            {
                processor.Process(ws, dataSource, resultStream);
                File.WriteAllBytes("Result.xlsx", resultStream.ToArray());
            }
        }

        Console.WriteLine("Processing complete. Check Result.xlsx.");
    }
}
```

L'exécution du programme affiche « Processing complete. Check Result.xlsx. » et crée un fichier Excel qui démontre le flux de travail **process excel template** avec **automatically name sheets**.

## Conclusion

Vous savez maintenant comment **process Excel template** des fichiers Excel en C# tout en laissant la bibliothèque **automatically name sheets** en fonction d'un nom de base personnalisé. Le tutoriel a couvert la création du processeur, la configuration des options, la liaison des données et les étapes de vérification, ainsi que la gestion des cas limites et les conseils de production. Appliquez le même modèle à des projets plus importants, intégrez-le aux API web ou étendez-le à d'autres formats Office.

**Prochaines étapes** que vous pourriez explorer :

* Utiliser `processor.Options.DetailSheetNewName` avec des valeurs dynamiques (par ex., inclure une date ou l'ID d'utilisateur).
* Combiner plusieurs sources de données pour générer des hiérarchies maître‑détail sur plusieurs feuilles.
* Expérimenter le style des balises SmartMarker pour contrôler les polices, les couleurs et les formats numériques directement depuis le modèle.

Bon codage, et profitez de l'automatisation Excel simplifiée !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités d'API supplémentaires et à explorer des approches d'implémentation alternatives dans vos propres projets.

- [Create Excel from Template – Step‑by‑Step Guide for .NET Developers](/cells/english/net/templates-reporting/create-excel-from-template-step-by-step-guide-for-net-develo/)
- [How to Merge and Rename Excel Sheets Using Aspose.Cells for .NET: A Step-by-Step Guide](/cells/english/net/worksheet-management/merge-rename-excel-sheets-aspose-cells-net/)
- [How to Link Sheets in Excel with SmartMarker – Step‑by‑Step Guide](/cells/english/net/smart-markers-dynamic-data/how-to-link-sheets-in-excel-with-smartmarker-step-by-step-gu/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}