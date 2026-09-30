---
category: general
date: 2026-03-30
description: Créez rapidement un classeur Excel en C# en insérant des données JSON
  et en enregistrant le classeur au format XLSX. Apprenez comment générer un fichier
  Excel à partir de JSON, écrire du JSON dans Excel et insérer du JSON dans Excel.
draft: false
keywords:
- create excel workbook c#
- save workbook as xlsx
- generate excel from json
- write json to excel
- insert json into excel
language: fr
og_description: Créez rapidement un classeur Excel en C# en insérant des données JSON
  et en l’enregistrant au format XLSX. Suivez ce guide étape par étape pour générer
  un fichier Excel à partir de JSON.
og_title: Créer un classeur Excel C# – Insérer du JSON et enregistrer en XLSX
tags:
- Aspose.Cells
- C#
- Excel automation
title: Créer un classeur Excel C# – Insérer du JSON et enregistrer en XLSX
url: /fr/net/excel-data-import-export/create-excel-workbook-c-insert-json-and-save-as-xlsx/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un classeur Excel C# – Insérer du JSON et enregistrer en XLSX

Vous avez déjà eu besoin de **create Excel workbook C#** et de déposer du JSON directement dans une cellule ? Vous n'êtes pas le seul—les développeurs rencontrent souvent le même problème lorsqu'ils ont des charges utiles d'API ou des fichiers de configuration qui doivent être placés dans une feuille de calcul pour le reporting ou le partage.  

Bonne nouvelle, avec Aspose.Cells vous pouvez le faire en quelques lignes, **save workbook as XLSX**, et garder tout le processus type‑safe. Dans ce tutoriel, nous allons **generate Excel from JSON**, **write JSON to Excel**, et vous montrer les étapes exactes pour **insert JSON into Excel** sans concaténations de chaînes compliquées.

## Ce que couvre ce guide

Nous allons parcourir :

1. Configurer un nouveau classeur vierge.  
2. Ajouter un Smart Marker qui attend du JSON.  
3. Fournir un tableau JSON au marqueur.  
4. Ajuster `SmartMarkerOptions` pour que le JSON reste dans une seule cellule.  
5. Enregistrer le fichier en tant que classeur XLSX.  

À la fin, vous disposerez d'un fichier `JsonSingleCell.xlsx` prêt à l'emploi et d'un modèle solide que vous pourrez réutiliser pour n'importe quel scénario JSON‑to‑Excel. Aucun service externe, juste du C# pur et la bibliothèque Aspose.Cells.

**Prérequis**

- .NET 6+ (ou .NET Framework 4.6+).  
- Visual Studio 2022 ou tout IDE compatible C#.  
- Package NuGet `Aspose.Cells` (version d'essai gratuite ou version sous licence).  

Si vous avez tout cela, plongeons‑y—aucune configuration supplémentaire n'est requise.

---

## Étape 1 : Créer un nouveau classeur en C#

La première chose dont vous avez besoin est un objet workbook vierge. Considérez-le comme un nouveau fichier Excel en attente de données.

```csharp
using Aspose.Cells;

// Initialize a new workbook – this is your empty Excel file
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];
```

**Pourquoi c’est important :**  
`Workbook` est le point d’entrée pour toutes les opérations Excel. En le créant d’abord, vous vous assurez que l’appel suivant **save workbook as xlsx** possède un objet concret à sérialiser.

> **Astuce :** Si vous prévoyez de travailler avec plusieurs feuilles, vous pouvez les ajouter dès maintenant avec `workbook.Worksheets.Add()`.

## Étape 2 : Placer un Smart Marker qui attend du JSON

Les Smart Markers sont des espaces réservés que Aspose.Cells remplace à l’exécution. Ici, nous indiquons qu’il doit rechercher une chaîne JSON nommée `data`.

```csharp
// Put a Smart Marker in cell A1 – {{data:json}} tells Aspose to expect JSON
worksheet.Cells["A1"].PutValue("{{data:json}}");
```

**Pourquoi c’est important :**  
Le suffixe `:json` indique au moteur que la valeur reçue est du JSON, pas du texte brut. C’est la clé pour **write json to excel** sans analyse manuelle.

## Étape 3 : Définir le tableau JSON

Nous créons maintenant le JSON que nous voulons insérer. Pour la démonstration, nous utiliserons une liste simple de personnes.

```csharp
// Sample JSON array – could come from an API, file, or DB
string jsonData = "[{\"Name\":\"John\",\"Age\":30},{\"Name\":\"Jane\",\"Age\":28}]";
```

**Cas particulier :**  
Si votre JSON contient des guillemets doubles, assurez‑vous qu’ils sont échappés (comme montré) ou utilisez une chaîne verbatim (`@"..."`) pour éviter les erreurs de compilation.

## Étape 4 : Configurer les options du Smart Marker – Conserver le tableau entier

Par défaut, Aspose tenterait d’étendre le tableau sur plusieurs lignes. Nous voulons que toute la chaîne JSON reste dans une seule cellule, ce qui est parfait pour les scénarios **insert json into excel** où le consommateur analysera le JSON plus tard.

```csharp
SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
{
    // Treat the whole array as a single cell value
    ArrayAsSingle = true
};
```

**Pourquoi c’est important :**  
`ArrayAsSingle = true` empêche l’expansion des lignes, vous offrant un blob JSON propre dans une seule cellule. C’est essentiel lorsque la feuille de calcul est un format de transport plutôt qu’un rapport.

## Étape 5 : Traiter le Smart Marker avec les données JSON

Nous associons maintenant le JSON au marqueur et laissons Aspose faire le travail lourd.

```csharp
// Process the marker – the anonymous object maps "data" to our JSON string
worksheet.SmartMarkers.Process(new { data = jsonData }, smartMarkerOptions);
```

**Ce qui se passe en coulisses :**  
Aspose évalue l’espace réservé `{{data:json}}`, sérialise la chaîne `jsonData` et l’écrit dans la cellule A1 en respectant les options que nous avons définies.

## Étape 6 : Enregistrer le classeur en fichier XLSX

Enfin, nous écrivons le classeur sur le disque. C’est ici que **save workbook as xlsx** entre en jeu.

```csharp
// Save the workbook – the extension determines the format (XLSX here)
workbook.Save("JsonSingleCell.xlsx");
```

**Résultat :**  
Ouvrez `JsonSingleCell.xlsx` dans Excel, et vous verrez le tableau JSON exactement comme nous l’avons défini, placé proprement dans la cellule A1.

## Exemple complet et exécutable

Ci‑dessous se trouve le programme complet que vous pouvez copier‑coller dans une application console. Il inclut toutes les étapes ci‑dessus et fonctionne immédiatement (en supposant que le package NuGet Aspose.Cells est installé).

```csharp
using System;
using Aspose.Cells;

namespace JsonToExcelDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a new workbook
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];

            // 2️⃣ Add a Smart Marker that expects JSON
            worksheet.Cells["A1"].PutValue("{{data:json}}");

            // 3️⃣ Define the JSON array
            string jsonData = "[{\"Name\":\"John\",\"Age\":30},{\"Name\":\"Jane\",\"Age\":28}]";

            // 4️⃣ Configure options – keep array as a single cell value
            SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
            {
                ArrayAsSingle = true
            };

            // 5️⃣ Process the marker with the JSON payload
            worksheet.SmartMarkers.Process(new { data = jsonData }, smartMarkerOptions);

            // 6️⃣ Save the workbook as XLSX
            workbook.Save("JsonSingleCell.xlsx");

            Console.WriteLine("Excel file created successfully! Check JsonSingleCell.xlsx.");
        }
    }
}
```

**Sortie attendue dans Excel**

| A |
|---|
| `[{"Name":"John","Age":30},{"Name":"Jane","Age":28}]` |

Cette seule cellule contient maintenant un tableau JSON parfaitement valide, prêt pour le traitement en aval.

## Questions fréquentes & cas particuliers

### Et si je veux que le JSON soit réparti sur plusieurs lignes ?

Définissez `ArrayAsSingle = false` (la valeur par défaut). Aspose créera une ligne pour chaque élément du tableau, en mappant les propriétés de l’objet aux colonnes. Cela est pratique lorsque vous souhaitez une vue tabulaire plutôt qu’une chaîne JSON brute.

### Puis‑je utiliser un fichier JSON au lieu d’une chaîne codée en dur ?

Absolument. Lisez le fichier dans une chaîne :

```csharp
string jsonData = File.ReadAllText("people.json");
```

Puis passez `jsonData` au même appel `Process`. Le reste du pipeline reste inchangé.

### Cette méthode fonctionne‑t‑elle avec de gros chargements JSON ?

Oui, mais surveillez l’utilisation de la mémoire. Pour des tableaux massifs, envisagez de diffuser les données ou d’écrire directement dans les lignes (`ArrayAsSingle = false`) afin d’éviter une seule cellule gigantesque que Excel pourrait avoir du mal à gérer.

### Le XLSX généré est‑il compatible avec les anciennes versions d’Excel ?

Le format `.xlsx` est basé sur Office Open XML et fonctionne avec Excel 2007 et versions ultérieures. Si vous avez besoin du format hérité `.xls`, modifiez l’appel d’enregistrement :

```csharp
workbook.Save("JsonSingleCell.xls", SaveFormat.Excel97To2003);
```

## Astuces pro pour travailler avec JSON et Excel

- **Validez le JSON d'abord** – utilisez `System.Text.Json.JsonDocument.Parse(jsonData)` pour détecter tôt les entrées malformées.  
- **Échappez les caractères spéciaux** – si votre JSON contient des sauts de ligne, ils apparaîtront comme le littéral `\n` dans la cellule ; vous pouvez les remplacer par `Environment.NewLine` avant le traitement.  
- **Réutilisez les Smart Markers** – vous pouvez placer plusieurs marqueurs dans la même feuille, chacun pointant vers une propriété JSON différente.  
- **Combinez avec des formules** – une fois le JSON dans une cellule, vous pouvez utiliser `FILTERXML` d’Excel (dans les versions récentes) pour le parser à la volée.

## Conclusion

Vous savez maintenant comment **create excel workbook c#**, intégrer une charge JSON, et **save workbook as xlsx** avec Aspose.Cells. Ce modèle vous permet de **generate excel from json**, **write json to excel**, et **insert json into excel** en quelques lignes de code seulement, rendant l’échange de données entre services et analystes fluide.

Prêt pour l’étape suivante ? Essayez de convertir le tableau JSON en une table propre (définissez `ArrayAsSingle = false`) ou explorez le style de la feuille après l’insertion. La même approche fonctionne pour CSV, XML, ou même des objets personnalisés—il suffit d’ajuster le type de Smart Marker.

Bon codage, et n’hésitez pas à expérimenter ! Si vous rencontrez des problèmes, laissez un commentaire ci‑dessous ou consultez la documentation officielle d’Aspose pour approfondir les Smart Markers.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}