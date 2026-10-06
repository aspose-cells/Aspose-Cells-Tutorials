---
category: general
date: 2026-03-25
description: Créer un classeur Excel à partir de JSON et enregistrer le classeur au
  format xlsx. Apprenez comment exporter du JSON en xlsx, générer un Excel à partir
  de JSON et remplir un Excel à partir de JSON en quelques minutes.
draft: false
keywords:
- create excel workbook
- export json to xlsx
- generate excel from json
- populate excel from json
- save workbook as xlsx
language: fr
og_description: Créez un classeur Excel à partir de JSON instantanément. Ce guide
  montre comment exporter le JSON en XLSX, générer un fichier Excel à partir du JSON
  et remplir Excel à partir du JSON avec Aspose.Cells.
og_title: Créer un classeur Excel à partir de JSON – Tutoriel complet C#
tags:
- Aspose.Cells
- C#
- JSON
- Excel automation
title: Créer un classeur Excel à partir de JSON – Guide étape par étape
url: /fr/net/excel-data-import-export/create-excel-workbook-from-json-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un classeur Excel à partir de JSON – Tutoriel complet C#

Vous avez déjà eu besoin de **créer un classeur Excel** à partir d’une charge JSON mais vous ne saviez pas par où commencer ? Vous n’êtes pas seul ; de nombreux développeurs rencontrent ce problème lorsqu’ils essaient de transformer des données d’API en une feuille de calcul propre. La bonne nouvelle ? En quelques lignes de C# et Aspose.Cells, vous pouvez **exporter json en xlsx**, **générer excel à partir de json**, et **remplir excel à partir de json** sans recourir à des convertisseurs tiers.

Dans ce guide, nous parcourrons l’ensemble du processus—en commençant par une chaîne JSON brute, en l’insérant dans un SmartMarker, et enfin **enregistrer le classeur en xlsx** sur le disque. À la fin, vous disposerez d’un fichier Excel prêt à l’emploi qui ressemble à ceci :

| Name | Score |
|------|-------|
| John | 90    |
| Anna | 85    |

> **Astuce :** Si vous utilisez déjà Aspose.Cells ailleurs dans votre projet, vous pouvez réutiliser la même instance `Workbook` pour plusieurs importations JSON—idéal pour le traitement par lots.

---

## Ce dont vous avez besoin

- **.NET 6+** (ou tout framework .NET récent qui supporte C# 10)
- **Aspose.Cells for .NET** – installer via NuGet : `dotnet add package Aspose.Cells`
- Une compréhension de base de la syntaxe C# (pas besoin de connaissances approfondies d’Excel)

C’est tout. Aucun service externe, aucune interop COM, juste du code géré pur.

---

## Étape 1 : Initialiser un nouveau classeur Excel

La première chose que nous faisons est de créer un objet workbook vierge. Considérez‑le comme l’ouverture d’un fichier Excel vierge où nous déposerons nos données plus tard.

```csharp
using Aspose.Cells;

// Step 1: Create a new workbook and grab the first worksheet
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];
```

Pourquoi commencer avec un nouveau workbook ? Cela garantit une ardoise propre, empêche les styles résiduels des exécutions précédentes et maintient la taille du fichier minimale—parfait pour les pipelines automatisés.

---

## Étape 2 : Préparer les données JSON à importer

Pour la démonstration, nous utiliserons un petit tableau JSON, mais vous pouvez le remplacer par n’importe quel JSON valide que vous recevez d’un service web, d’un fichier ou d’une requête de base de données.

```csharp
// Step 2: JSON string representing a simple collection of records
string jsonData = "[{\"Name\":\"John\",\"Score\":90},{\"Name\":\"Anna\",\"Score\":85}]";
```

Remarquez les guillemets double‑échappés (`\"`)—c’est simplement la syntaxe des littéraux de chaîne C#. Dans un scénario réel, vous liriez probablement cela depuis un fichier :

```csharp
// string jsonData = File.ReadAllText("data.json");
```

---

## Étape 3 : Dire à SmartMarker de traiter tout le tableau comme un seul enregistrement

Le moteur SmartMarker d’Aspose.Cells peut itérer automatiquement sur les collections. En activant **ArrayAsSingle**, nous traitons l’ensemble du tableau JSON comme un seul enregistrement, ce qui est exactement ce dont nous avons besoin pour une table plate.

```csharp
// Step 3: Configure SmartMarker options – array‑as‑single mode
SmartMarkerOptions options = new SmartMarkerOptions
{
    ArrayAsSingle = true   // This makes the whole JSON array behave like one record
};
```

Si vous oubliez ce drapeau, SmartMarker tenterait de créer une feuille distincte pour chaque élément—ce qui n’est clairement pas ce que vous voulez lors de la génération d’une simple table.

---

## Étape 4 : Placer un token SmartMarker dans la feuille de calcul

Les tokens SmartMarker ressemblent à `${jsonArray}`. Lorsque le processeur s’exécute, il remplace le token par les données provenant de la source JSON. Nous placerons le token dans la cellule **A1** afin que la sortie commence en haut à gauche.

```csharp
// Step 4: Insert the SmartMarker token into cell A1
worksheet.Cells["A1"].PutValue("${jsonArray}");
```

Vous pouvez également pré‑formater la ligne d’en‑tête avant le traitement. Par exemple, mettre la police en gras sur la première ligne :

```csharp
Cell headerCell = worksheet.Cells["A1"];
headerCell.Style.Font.IsBold = true;
```

---

## Étape 5 : Exécuter le processeur SmartMarker

Maintenant, la magie opère. Le processeur lit le JSON, associe chaque propriété à une colonne et écrit les lignes sous le token.

```csharp
// Step 5: Process the SmartMarker with our JSON data and options
worksheet.SmartMarkerProcessor.Process(jsonData, options);
```

En coulisses, Aspose.Cells :

1. Analyse le JSON en un objet .NET.  
2. Fait correspondre les noms de propriétés (`Name`, `Score`) aux en‑têtes de colonnes.  
3. Écrit chaque élément du tableau comme une nouvelle ligne.

Si votre JSON contient des objets imbriqués, vous pouvez y faire référence avec la notation point (`${parent.child}`) — une fonctionnalité pratique pour des rapports plus complexes.

---

## Étape 6 : Enregistrer le classeur au format XLSX

Enfin, persistez le classeur sur le disque. L’extension de fichier `.xlsx` indique à Excel (et à la plupart des autres applications de tableur) qu’il s’agit d’un classeur OpenXML.

```csharp
// Step 6: Save the workbook to a file
string outputPath = Path.Combine(Environment.CurrentDirectory, "json-single.xlsx");
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

Vous pouvez, bien sûr, diffuser le classeur directement dans une réponse HTTP si vous créez une API web :

```csharp
// Example for ASP.NET Core
using (var stream = new MemoryStream())
{
    workbook.Save(stream, SaveFormat.Xlsx);
    stream.Position = 0;
    return File(stream, "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet", "data.xlsx");
}
```

---

## Exemple complet fonctionnel

Voici le programme complet, prêt à être exécuté, qui intègre toutes les étapes ci‑dessus. Copiez‑collez‑le dans un nouveau projet console et appuyez sur **F5**.

```csharp
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ JSON data to be merged into the sheet
        string jsonData = "[{\"Name\":\"John\",\"Score\":90},{\"Name\":\"Anna\",\"Score\":85}]";

        // 3️⃣ Enable array‑as‑single mode so the whole array is one record
        SmartMarkerOptions options = new SmartMarkerOptions
        {
            ArrayAsSingle = true
        };

        // 4️⃣ Put a SmartMarker token in A1 that points to the JSON array
        worksheet.Cells["A1"].PutValue("${jsonArray}");

        // Optional: make the header bold for better readability
        worksheet.Cells["A1"].Style.Font.IsBold = true;

        // 5️⃣ Process the SmartMarker with the JSON payload
        worksheet.SmartMarkerProcessor.Process(jsonData, options);

        // 6️⃣ Save the result as an XLSX file
        string outputPath = Path.Combine(Environment.CurrentDirectory, "json-single.xlsx");
        workbook.Save(outputPath);

        Console.WriteLine($"✅ Workbook created and saved to: {outputPath}");
    }
}
```

**Résultat attendu :** L’ouverture de `json-single.xlsx` montre deux lignes sous l’en‑tête en gras—`John` avec un score de `90` et `Anna` avec `85`. Les noms de colonnes sont automatiquement déduits des noms de propriétés du JSON.

---

## Questions fréquentes & cas particuliers

### Que faire si mes clés JSON contiennent des espaces ou des caractères spéciaux ?

SmartMarker attend des noms d’identificateur valides. Remplacez les espaces par des underscores ou utilisez un mappage personnalisé :

```csharp
// Example JSON: {"First Name":"John"}
string jsonData = "[{\"First_Name\":\"John\",\"Score\":90}]";
// Token stays the same – Aspose.Cells will map "First_Name" to column header "First_Name"
```

### Comment exporter un grand tableau JSON (des milliers de lignes) ?

Le processeur diffuse les données en interne, de sorte que l’utilisation de mémoire reste modeste. Cependant, vous pourriez vouloir :

- Augmenter la limite `MaxRows` de la feuille (`worksheet.Cells.MaxRow = 1_048_576;` – le maximum d’Excel).  
- Désactiver les quadrillages pour améliorer les performances (`worksheet.IsGridlinesVisible = false;`).

### Puis‑je ajouter plusieurs tables JSON au même classeur ?

Oui. Placez simplement différents tokens SmartMarker dans des plages distinctes (par ex., `${orders}` en `A10`, `${customers}` en `D1`) et appelez `Process` une fois par token ou une fois avec un objet JSON composite contenant les deux tableaux.

---

## Bonus : Ajouter un graphique simple (facultatif)

Si vous souhaitez visualiser les scores, ajoutez un rapide graphique en colonnes après que les données aient été peuplées :

```csharp
// Insert a column chart starting at cell E1
int chartIndex = worksheet.Charts.Add(ChartType.Column, 0, 4, 15, 10);
Chart chart = worksheet.Charts[chartIndex];
chart.NSeries.Add("B2:B3", true);
chart.NSeries[0].Name = "Score";
chart.Title.Text = "Scores by Name";
```

Le graphique référencera automatiquement les nouvelles lignes, vous offrant un rapport soigné en une seule étape.

---

## Conclusion

Vous savez maintenant **comment créer un classeur Excel** à partir d’une chaîne JSON, **exporter json en xlsx**, **générer excel à partir de json**, et **remplir excel à partir de json** en utilisant la fonction SmartMarker d’Aspose.Cells. La solution complète—initialisation du classeur, configuration de SmartMarker, traitement du JSON et sauvegarde du fichier—se résume à quelques lignes, tout en restant capable de gérer d’énormes ensembles de données.

Prochaines étapes ? Essayez de remplacer le JSON statique par un appel d’API, ajoutez une mise en forme conditionnelle selon les scores, ou générez plusieurs feuilles pour différents domaines de données. Le même modèle fonctionne pour CSV, XML ou même des jeux de résultats de bases de données—il suffit de changer la chaîne source et d’ajuster le token SmartMarker.

Bon codage, et que vos feuilles de calcul restent toujours impeccables !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}