---
category: general
date: 2026-05-04
description: Créer un Excel à partir d’un modèle et mapper le JSON vers Excel avec
  un nommage dynamique des feuilles de calcul. Apprenez à remplir Excel à partir de
  JSON et à générer un fichier Excel à l’aide de JSON en quelques minutes.
draft: false
keywords:
- create excel from template
- map json to excel
- populate excel from json
- dynamic worksheet naming excel
- generate excel using json
language: fr
og_description: Créez rapidement un Excel à partir d'un modèle. Ce guide montre comment
  mapper le JSON vers Excel, remplir Excel à partir du JSON, utiliser la nomination
  dynamique des feuilles de calcul et générer Excel à l'aide du JSON.
og_title: Créer un fichier Excel à partir d'un modèle – Tutoriel complet .NET
tags:
- C#
- Aspose.Cells
- SmartMarker
- JSON
title: Créer un fichier Excel à partir d’un modèle – Guide étape par étape pour les
  développeurs .NET
url: /fr/net/templates-reporting/create-excel-from-template-step-by-step-guide-for-net-develo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer Excel à partir d'un modèle – Tutoriel complet .NET

Vous avez déjà eu besoin de **créer Excel à partir d'un modèle** mais vous vous êtes retrouvé bloqué à jongler entre les données JSON et les noms de feuilles ? Vous n'êtes pas le seul. Dans de nombreux projets de reporting, le modèle définit la mise en page tandis que la charge JSON fournit les valeurs réelles, et les faire communiquer peut devenir un vrai casse‑tête.  

Bonne nouvelle ? En quelques lignes de C# et avec le moteur SmartMarker d’Aspose Cells, vous pouvez **remplir Excel à partir de JSON**, renommer les feuilles de détail à la volée, et enfin **générer Excel en utilisant JSON** sans jamais toucher à l’interface utilisateur.  

Dans ce tutoriel, nous parcourrons l’ensemble du pipeline : chargement d’un modèle, mappage du JSON vers Excel, configuration du renommage dynamique des feuilles, puis sauvegarde du classeur final. À la fin, vous disposerez d’un extrait réutilisable que vous pourrez intégrer à n’importe quel service .NET. Aucun outil externe, uniquement du code pur.

---

## Ce dont vous avez besoin

- **Aspose.Cells for .NET** (v24.10 ou ultérieur) – la bibliothèque qui alimente SmartMarker.  
- Un fichier **template.xlsx** contenant des balises SmartMarker comme `{Master:Name}` et `{Detail:Item}`.  
- Un fichier **data.json** correspondant à la structure maître‑détail.  
- Visual Studio 2022 (ou tout autre IDE de votre choix) ciblant .NET 6 ou supérieur.

C’est tout. Si vous avez déjà ces éléments, vous êtes prêt à démarrer.

---

## Créer Excel à partir d'un modèle – Vue d’ensemble

L’idée principale est simple : traiter le fichier Excel comme un *modèle* et laisser SmartMarker remplacer les espaces réservés par les valeurs de votre JSON. La bibliothèque vous permet également de renommer la feuille de détail en fonction d’un champ maître, c’est là que **dynamic worksheet naming excel** prend tout son sens.

Voici le code complet, prêt à être exécuté. Copiez‑collez‑le dans une application console et pointez les chemins vers vos propres fichiers.

```csharp
// ------------------------------------------------------------
// Full example: create Excel from template using JSON data
// ------------------------------------------------------------
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelTemplateDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the workbook that contains SmartMarker tags
            //    (e.g., {Master:Name} in the master sheet and {Detail:Item} in the detail sheet)
            string templatePath = @"C:\MyProject\Templates\template.xlsx";
            Workbook wb = new Workbook(templatePath);

            // 2️⃣ Read the JSON data that will populate the markers
            //    The JSON should match the structure expected by the template.
            string jsonPath = @"C:\MyProject\Data\data.json";
            string json = File.ReadAllText(jsonPath);

            // 3️⃣ Configure the SmartMarker processor to rename the detail sheet
            //    dynamically based on the master record’s Name field.
            //    This demonstrates dynamic worksheet naming excel.
            wb.SmartMarkerProcessor.Options.DetailSheetNewName = "Detail_{Master.Name}";

            // 4️⃣ Execute the SmartMarker processing using the JSON data.
            //    This step maps JSON to Excel and populates every marker.
            wb.SmartMarkerProcessor.Execute(json);

            // 5️⃣ Save the processed workbook – now it’s a brand‑new file.
            string outputPath = @"C:\MyProject\Output\output.xlsx";
            wb.Save(outputPath);

            Console.WriteLine("✅ Excel file generated successfully at: " + outputPath);
        }
    }
}
```

> **Résultat attendu** :  
> - La feuille maître affichera le nom provenant de `Master.Name`.  
> - La feuille détail sera renommée en quelque chose comme `Detail_JohnDoe`.  
> - Toutes les lignes `{Detail:Item}` seront remplies avec le tableau d’items du JSON.

---

## Mapper le JSON vers Excel – Chargement des données

Avant que le moteur SmartMarker ne puisse faire sa magie, le JSON doit être **bien formé** et refléter la hiérarchie utilisée dans le modèle. Un JSON maître‑détail typique ressemble à ceci :

```json
{
  "Master": {
    "Name": "John Doe",
    "Date": "2026-05-04"
  },
  "Detail": [
    { "Item": "Widget A", "Qty": 10, "Price": 2.5 },
    { "Item": "Widget B", "Qty": 5,  "Price": 5.0 }
  ]
}
```

**Pourquoi c’est important** :  
- Les clés `Master` et `Detail` correspondent directement aux balises `{Master:…}` et `{Detail:…}`.  
- Si la structure JSON diverge, SmartMarker ne trouvera pas de correspondance et les cellules resteront vides.  

**Astuce** : validez votre JSON avec un validateur en ligne rapide ou avec `System.Text.Json.JsonDocument.Parse(json)` pour détecter les erreurs de syntaxe dès le départ.

---

## Remplir Excel à partir de JSON – Configuration de SmartMarker

SmartMarker fonctionne en parcourant le classeur à la recherche de balises, puis en injectant les données. L’étape **populate excel from json** correspond essentiellement à l’appel `Execute` que nous avons vu plus haut, mais il existe quelques paramètres optionnels utiles :

| Paramètre | Ce que ça fait | Quand l’utiliser |
|-----------|----------------|------------------|
| `Options.CaseSensitive` | Traite les noms de balises comme sensibles à la casse. | Si votre modèle mélange les majuscules/minuscules et que vous avez besoin d’une correspondance stricte. |
| `Options.RemoveEmptyRows` | Supprime les lignes qui n’ont reçu aucune donnée. | Pour garder la feuille finale propre lorsqu’une partie des éléments détail est optionnelle. |
| `Options.EnableHyperlink` | Permet aux hyperliens présents dans le JSON de devenir cliquables. | Lorsque vous avez besoin d’URL cliquables dans le rapport. |

Vous pouvez les chaîner ainsi :

```csharp
wb.SmartMarkerProcessor.Options.CaseSensitive = true;
wb.SmartMarkerProcessor.Options.RemoveEmptyRows = true;
```

---

## Dynamic Worksheet Naming Excel – Configurer le nom de la feuille détail

L’une des exigences les plus délicates dans de nombreux projets est **dynamic worksheet naming excel**. Au lieu d’une feuille « Detail » statique, vous pouvez vouloir que chaque rapport porte le nom du client ou un numéro de commande.

La ligne :

```csharp
wb.SmartMarkerProcessor.Options.DetailSheetNewName = "Detail_{Master.Name}";
```

fait exactement cela. Le placeholder `{Master.Name}` est remplacé *après* le traitement du JSON, de sorte que le nouveau nom de feuille devienne `Detail_JohnDoe`.  

**Cas particulier** : si le nom contient des caractères interdits dans les noms de feuille (`:`, `\`, `/`, `?`, `*`, `[`, `]`), Aspose les nettoie automatiquement, mais vous pouvez pré‑nettoyer la chaîne dans le JSON si vous avez besoin d’un format précis.

---

## Générer Excel en utilisant JSON – Exécuter et sauvegarder

Les deux dernières lignes du code (`Execute` et `Save`) sont l’endroit où la **generate excel using json** opère. En coulisses, Aspose analyse le JSON en tableau de données, parcourt le modèle et écrit le fichier de sortie.

Si vous devez générer plusieurs classeurs dans une boucle (par ex., un par client), déplacez simplement l’instanciation de `Workbook` à l’intérieur de la boucle et modifiez le nom de fichier de sortie en conséquence :

```csharp
foreach (var customerJson in customers)
{
    Workbook wb = new Workbook(templatePath);
    wb.SmartMarkerProcessor.Options.DetailSheetNewName = $"Detail_{customerJson.Master.Name}";
    wb.SmartMarkerProcessor.Execute(customerJson);
    wb.Save($@"C:\Reports\Report_{customerJson.Master.Name}.xlsx");
}
```

Ce schéma est courant dans les services de reporting batch.

---

## Pièges courants & Astuces pro

- **Balises manquantes** : si une cellule affiche encore `{Master:Name}`, la balise n’a pas été reconnue. Vérifiez l’orthographe et assurez‑vous que la balise se trouve dans une cellule, pas dans un commentaire.  
- **Charges JSON volumineuses** : pour des jeux de données massifs, envisagez le streaming du JSON ou l’utilisation d’un `DataTable` plutôt qu’une chaîne brute afin de réduire la pression mémoire.  
- **Sécurité des threads** : les instances de `Workbook` ne sont pas thread‑safe. Créez une nouvelle instance par thread si vous exécutez des jobs parallèles.  
- **Verrouillage de fichiers** : assurez‑vous que le modèle n’est pas ouvert dans Excel pendant l’exécution du code ; sinon vous obtiendrez une `IOException`.  

> **Astuce pro** : conservez une copie du modèle original dans un dossier en lecture seule. Cela évite les écrasements accidentels pendant le débogage.

---

## Récapitulatif de l’exemple complet

Voici à nouveau le programme complet, cette fois avec des commentaires en ligne pour chaque ligne non évidente :

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelTemplateDemo
{
    class Program
    {
        static void Main()
        {
            // Path to the Excel template that contains SmartMarker tags.
            string templatePath = @"C:\MyProject\Templates\template.xlsx";

            // Load the workbook – this is the "create excel from template" step.
            Workbook wb = new Workbook(templatePath);

            // Read JSON data that maps directly to the template's tags.
            string jsonPath = @"C:\MyProject\Data\data.json";
            string json = File.ReadAllText(jsonPath);

            // OPTIONAL: tweak SmartMarker behavior (case‑sensitivity, empty rows, etc.).
            wb.SmartMarkerProcessor.Options.CaseSensitive = false;
            wb.SmartMarkerProcessor.Options.RemoveEmptyRows = true;

            // Set up dynamic worksheet naming based on the master record's Name field.
            wb.SmartMarkerProcessor.Options.DetailSheetNewName = "Detail_{Master.Name}";

            // Run the SmartMarker engine – this is where we "populate excel from json".
            wb.SmartMarkerProcessor.Execute(json);

            // Save the newly generated workbook – the final "generate excel using json" step.
            string outputPath = @"C:\MyProject\Output\output.xlsx";
            wb.Save(outputPath);

            Console.WriteLine("✅ Workbook created at: " + outputPath);
        }
    }
}
```

L’exécution de cette application console produira `output.xlsx` avec une feuille détail renommée et toutes les données correctement remplissées.

---

## Prochaines étapes & Sujets associés

- **Export PDF** : après la génération du classeur, vous pouvez appeler `wb.Save("report.pdf", SaveFormat.Pdf);` pour obtenir une version PDF.  
- **Population de graphiques** : SmartMarker prend également en charge les sources de données des graphiques ; il suffit de lier le tableau JSON à la plage de séries du graphique.  
- **Mise en forme conditionnelle** : utilisez les règles intégrées d’Excel dans le modèle ; elles seront conservées après le remplacement SmartMarker.  
- **Optimisation des performances** : pour des scénarios à haut volume, réutilisez une seule instance de `Workbook` avec `Clone` afin d’éviter des I/O de fichiers répétés.  

N’hésitez pas à expérimenter avec différentes structures JSON, modèles de renommage ou même à combiner plusieurs modèles en une seule exécution. La flexibilité de **create excel from template** avec Aspose.Cells vous permet d’adapter la solution à des factures, tableaux de bord ou tout autre besoin de reporting.

---

## Résumé visuel

![Create Excel from Template workflow showing JSON → SmartMarker → Dynamic Sheet Naming](/images/create-excel-from-template-workflow.png "Create Excel from Template workflow diagram")

*(Alt text includes primary keyword for SEO)*

---

### Conclusion

Nous avons couvert tout ce qu’il faut savoir pour **create excel from template**, **map JSON to Excel**, **populate Excel from JSON**, utiliser **dynamic worksheet naming excel**, et enfin **generate Excel using JSON**. Le code est complet, les explications vous indiquent *pourquoi* chaque ligne est importante, et vous disposez maintenant d’une base solide pour construire des pipelines de reporting plus complexes.

Vous avez une variante que vous essayez de mettre en place ? Laissez un commentaire ci‑dessous, et résolvons cela ensemble. Bon codage !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}