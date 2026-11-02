---
category: general
date: 2026-09-21
description: Configurez SmartMarkerOptions ArrayAsSingle en C# pour exporter les tableaux
  JSON en tant que valeur unique dans une cellule d’un classeur Excel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- configure smartmarkeroptions arrayassingle
- Aspose.Cells smart markers
- export JSON array
- C# DataTable
- Workbook ProcessSmartMarkers
language: fr
lastmod: 2026-09-21
og_description: Configurez SmartMarkerOptions ArrayAsSingle en C# pour exporter les
  tableaux JSON en une seule valeur de cellule. Découvrez la solution complète, étape
  par étape.
og_image_alt: Screenshot of an Excel sheet showing a JSON array stored in a single
  cell after using SmartMarkerOptions
og_title: Configurer SmartMarkerOptions ArrayAsSingle en C# – guide complet
schemas:
- author: Aspose
  dateModified: '2026-09-21'
  description: Configure SmartMarkerOptions ArrayAsSingle in C# to export JSON arrays
    as a single cell value in an Excel workbook.
  headline: Configure SmartMarkerOptions ArrayAsSingle in C# for JSON arrays
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Configurer SmartMarkerOptions ArrayAsSingle en C# pour les tableaux JSON
url: /fr/net/smart-markers-dynamic-data/configure-smartmarkeroptions-arrayassingle-in-c-for-json-arr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Configurer SmartMarkerOptions ArrayAsSingle en C# pour les tableaux JSON

Si vous devez **configurer SmartMarkerOptions ArrayAsSingle** lors de la génération de fichiers Excel avec Aspose.Cells, ce guide vous montre exactement comment le faire. Vous verrez comment conserver un tableau JSON intact dans une seule cellule au lieu de répartir ses éléments sur plusieurs lignes.

Travailler avec des données JSON dans les feuilles de calcul implique souvent de choisir entre une vue aplatie et une représentation compacte. Dans de nombreux scénarios de reporting—comme le stockage d’une liste de tags ou d’un ensemble d’identifiants—vous souhaitez que la chaîne JSON entière reste dans une seule cellule. Le drapeau **ArrayAsSingle** dans `SmartMarkerOptions` rend cela possible.

Dans ce tutoriel vous allez :

* Créer un `DataTable` contenant un tableau JSON dans une colonne.
* Placer des Smart Markers dans une feuille de calcul Excel.
* **Configurer SmartMarkerOptions ArrayAsSingle** afin que le tableau JSON soit traité comme une valeur de cellule unique.
* Traiter les marqueurs et enregistrer le classeur.
* Vérifier le résultat.

> **Prérequis** – Vous avez besoin de la bibliothèque Aspose.Cells pour .NET (v23.12 ou ultérieure) et d’un environnement de développement .NET (Visual Studio 2022 recommandé). Une connaissance de base du C# et des DataTables est supposée.

---

## Étape 1 : Préparer la source de données avec un tableau JSON

Tout d’abord, créez un `DataTable` qui imite les données que vous recevriez d’un service ou d’une base de données. La colonne **Names** contient une chaîne encodée en JSON représentant un tableau de noms.

```csharp
using System;
using System.Data;
using Aspose.Cells;

DataTable dataTable = new DataTable();
dataTable.Columns.Add("Id", typeof(int));
dataTable.Columns.Add("Names", typeof(string));

// Store the JSON array as a plain string
dataTable.Rows.Add(1, "[\"Alice\",\"Bob\"]");
```

*Pourquoi cette étape ?*  
Les Smart Markers lisent les données directement à partir d’objets .NET. En plaçant le tableau JSON dans une colonne de type chaîne, vous préservez la syntaxe JSON exacte, qui pourra ensuite être écrite dans une cellule sans modification.

---

## Étape 2 : Insérer des Smart Markers dans un nouveau classeur

Créez un nouveau classeur, sélectionnez la première feuille de calcul, et écrivez des Smart Markers qui font référence à l’ensemble du tableau et à la colonne **Names** spécifique.

```csharp
// Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];

// Smart marker for the entire table (optional, shown for completeness)
worksheet.Cells["A1"].PutValue("&=dataTable");

// Smart marker that targets only the Names column
worksheet.Cells["A2"].PutValue("&=dataTable.Names");
```

Le marqueur `&=dataTable.Names` indique à Aspose.Cells de remplacer la cellule par la valeur de la colonne **Names** pour chaque ligne de `dataTable`. Comme nous n’avons qu’une seule ligne, le marqueur sera traité une fois.

---

## Étape 3 : **Configurer SmartMarkerOptions ArrayAsSingle**

Par défaut, Aspose.Cells développe une chaîne de type tableau en lignes séparées. Définir `ArrayAsSingle` à `true` remplace ce comportement, obligeant la chaîne JSON entière à rester dans une seule cellule.

```csharp
SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
{
    // Export the JSON array as a single cell value
    ArrayAsSingle = true
};
```

*Pourquoi activer `ArrayAsSingle` ?*  
Lorsque `ArrayAsSingle` est `false`, le moteur interprète `["Alice","Bob"]` comme deux valeurs séparées et les écrit dans des lignes adjacentes. Le définir à `true` traite la chaîne comme une valeur atomique, ce qui est essentiel pour préserver le format JSON dans Excel.

---

## Étape 4 : Traiter les Smart Markers avec les options configurées

Exécutez maintenant le moteur Smart Marker, en passant l’objet d’options que vous venez de configurer.

```csharp
// Process smart markers using the custom options
workbook.ProcessSmartMarkers(smartMarkerOptions);
```

Pendant le traitement, Aspose.Cells lit le `dataTable`, applique les marqueurs et respecte le drapeau `ArrayAsSingle`, laissant le tableau JSON intact.

---

## Étape 5 : Enregistrer le classeur et vérifier le résultat

Enfin, écrivez le classeur sur le disque. Ouvrez le fichier généré dans Excel ou tout visualiseur de feuilles de calcul pour confirmer que la cellule **A2** contient la chaîne JSON exacte.

```csharp
// Save the resulting workbook
string outputPath = @"C:\Temp\SmartMarkerJson.xlsx";
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

### Résultat attendu

| A   |
|-----|
| **["Alice","Bob"]** |

La cellule **A2** affiche le tableau JSON comme une valeur texte unique, exactement comme stockée dans le `DataTable`. Aucune ligne supplémentaire n’est créée.

---

## Variations courantes et gestion des cas limites

| Situation | Comment s'adapter |
|-----------|--------------------|
| **Lignes multiples avec des tableaux JSON** | Le même paramètre `ArrayAsSingle` fonctionne ; le tableau JSON de chaque ligne reste dans sa propre cellule. |
| **Différentes structures JSON (objets, tableaux imbriqués)** | Tant que le JSON est une chaîne, `ArrayAsSingle` le conservera intact. Pour les objets complexes, il peut être nécessaire d’échapper les guillemets. |
| **Utilisation d’une source de données différente (par ex., List\<T\>)** | Remplacez le `DataTable` par n’importe quelle collection énumérable ; la syntaxe du marqueur (`&=myList.Property`) reste la même. |
| **Exportation vers CSV au lieu de XLSX** | `ArrayAsSingle` s’applique toujours, mais n’oubliez pas que le CSV ne préserve pas le formatage des cellules ; il peut être nécessaire d’entourer le JSON de guillemets. |

**Astuce :** Toujours définir `ArrayAsSingle` *avant* d’appeler `ProcessSmartMarkers`. Modifier le drapeau après le traitement n’a aucun effet sur les cellules déjà générées.

---

## Exemple complet et exécutable

Ci-dessous le programme complet que vous pouvez copier‑coller dans une application console. Il inclut toutes les directives `using` et des commentaires pour plus de clarté.

```csharp
using System;
using System.Data;
using Aspose.Cells;

namespace SmartMarkerDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create the data source with a JSON array
            DataTable dataTable = new DataTable();
            dataTable.Columns.Add("Id", typeof(int));
            dataTable.Columns.Add("Names", typeof(string));
            dataTable.Rows.Add(1, "[\"Alice\",\"Bob\"]");

            // 2️⃣ Build a workbook and place smart markers
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];
            worksheet.Cells["A1"].PutValue("&=dataTable");          // whole table (optional)
            worksheet.Cells["A2"].PutValue("&=dataTable.Names");   // Names column

            // 3️⃣ Configure SmartMarkerOptions to treat arrays as single values
            SmartMarkerOptions options = new SmartMarkerOptions
            {
                ArrayAsSingle = true
            };

            // 4️⃣ Process the markers with the custom options
            workbook.ProcessSmartMarkers(options);

            // 5️⃣ Save the file
            string path = @"C:\Temp\SmartMarkerJson.xlsx";
            workbook.Save(path);
            Console.WriteLine($"Workbook saved to {path}");
        }
    }
}
```

Exécutez le programme, ouvrez `SmartMarkerJson.xlsx`, et vous verrez le tableau JSON préservé dans la cellule **A2**.

---

## Conclusion

Vous savez maintenant comment **configurer SmartMarkerOptions ArrayAsSingle** en C# pour conserver un tableau JSON comme valeur d’une seule cellule lors de l’utilisation des smart markers d’Aspose.Cells. Les étapes—préparer un `DataTable`, insérer des marqueurs, définir le drapeau `ArrayAsSingle`, traiter et enregistrer—forment un modèle réutilisable que vous pouvez appliquer à tout scénario nécessitant une représentation JSON compacte dans Excel.

Ensuite, vous pourriez explorer :

* **Smart markers Aspose.Cells** pour parcourir des collections.  
* Exporter des **objets JSON imbriqués** en personnalisant le format des cellules.  
* Combiner le **formatage conditionnel** avec les smart markers pour des rapports plus riches.  

N’hésitez pas à expérimenter avec différentes structures de données et à partager vos découvertes. Bon codage !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités d’API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Créer un classeur Excel à partir de JSON – Guide complet Aspose.Cells](/cells/english/net/data-loading-and-parsing/create-excel-workbook-from-json-complete-aspose-cells-guide/)
- [Créer et configurer un classeur Excel Aspose Cells Net](/cells/hindi/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)
- [Créer et configurer un classeur Excel Aspose Cells Net](/cells/german/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}