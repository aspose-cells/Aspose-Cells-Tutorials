---
category: general
date: 2026-03-29
description: Apprenez à exporter des tableaux Excel en texte brut, à écrire une chaîne
  dans un fichier et à convertir un tableau Excel en CSV ou TXT avec C#. Inclut le
  code complet et des astuces.
draft: false
keywords:
- how to export excel
- write string to file
- convert excel table
- export table as csv
- save txt file c#
language: fr
og_description: Comment exporter des tableaux Excel vers des fichiers texte en C#.
  Obtenez la solution complète, le code et les meilleures pratiques pour convertir
  les tableaux Excel et enregistrer des fichiers TXT.
og_title: Comment exporter des données Excel – Tutoriel complet C#
tags:
- C#
- Excel
- File I/O
title: Comment exporter des données Excel – Guide C# étape par étape
url: /fr/net/excel-data-export-retrieval/how-to-export-excel-data-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment exporter des données Excel – Guide complet C#  

Vous vous êtes déjà demandé **comment exporter Excel** sans ouvrir le classeur manuellement ? Peut‑être devez‑vous extraire une table dans un fichier texte simple pour un système hérité, ou vous avez besoin d’une exportation CSV rapide pour des pipelines d’analyse de données. Dans ce tutoriel, nous allons parcourir une solution pratique, de bout en bout, qui **écrit une chaîne dans un fichier** et vous montre exactement comment **convertir une table Excel** en un format texte délimité en utilisant C#.

Nous couvrirons tout, du chargement du classeur, à la sélection de la bonne table, en passant par la configuration des options d’exportation, jusqu’à l’enregistrement du résultat sous forme de fichier `.txt`. À la fin, vous pourrez **exporter une table en CSV** (ou tout autre séparateur de votre choix) et vous découvrirez également quelques astuces pratiques pour **enregistrer un fichier txt C#**. Aucun outil externe requis — seulement quelques packages NuGet et un peu de code.

---

## Ce dont vous avez besoin

- **.NET 6.0+** (ou .NET Framework 4.7.2 si vous préférez le classique)
- **Syncfusion.XlsIO** package NuGet (la classe `ExportTableOptions` se trouve ici)
- Un IDE C# basique (Visual Studio, VS Code, Rider — n’importe lequel fera l’affaire)
- Un classeur Excel contenant au moins une table (nous utiliserons `ws.Tables[0]` dans l’exemple)

> Astuce : Si vous n’avez pas encore la bibliothèque Syncfusion, exécutez  
> `dotnet add package Syncfusion.XlsIO.Net.Core` depuis la ligne de commande.

## Étape 1 – Ouvrir le classeur et récupérer la première table  

La première chose est de charger le fichier Excel et d’obtenir une référence à la feuille qui contient la table. Cette étape est cruciale car l’opération **convert excel table** fonctionne sur un objet `ITable`, pas sur des plages de cellules brutes.

```csharp
using Syncfusion.XlsIO;
using System.IO;

class ExcelExporter
{
    static void Main()
    {
        // Load the workbook (replace with your actual file path)
        using (ExcelEngine excelEngine = new ExcelEngine())
        {
            IApplication application = excelEngine.Excel;
            application.DefaultVersion = ExcelVersion.Xlsx;

            // Open the file
            FileStream stream = new FileStream(@"C:\Data\Sample.xlsx", FileMode.Open, FileAccess.Read);
            IWorkbook workbook = application.Workbooks.Open(stream);
            IWorksheet ws = workbook.Worksheets[0];   // First worksheet
```

*Pourquoi c’est important :* Ouvrir le classeur avec `using` garantit que toutes les ressources non gérées sont libérées, évitant les problèmes de verrouillage de fichier plus tard lorsque vous essayez de **write string to file**.

## Étape 2 – Configurer les options d’exportation (texte brut, pas d’en‑têtes, séparateur point‑virgule)  

Nous indiquons maintenant à Syncfusion comment nous voulons sérialiser la table. Le `ExportTableOptions` vous permet d’activer ou désactiver l’inclusion des en‑têtes, de choisir un séparateur, et de décider si vous obtenez une chaîne ou un tableau d’octets.

```csharp
            // Step 2: Configure export options – plain text, omit headers, ';' delimiter
            var exportOptions = new ExportTableOptions
            {
                ExportAsString = true,      // Returns a string we can write directly
                IncludeHeaders = false,     // Skip column headers if you don’t need them
                Delimiter = ";"             // Change to ',' for classic CSV
            };
```

*Pourquoi c’est important :* Définir `IncludeHeaders = false` correspond souvent aux attentes des systèmes en aval qui connaissent déjà l’ordre des colonnes. Modifier le séparateur est la façon dont vous **export table as CSV** avec un séparateur personnalisé.

## Étape 3 – Exporter la table en chaîne  

Avec les options prêtes, nous appelons `ExportToString`. Cette méthode extrait toute la table (y compris toutes les lignes) et renvoie une chaîne unique prête à être écrite dans un fichier.

```csharp
            // Step 3: Export the first table to a string using the configured options
            ITable firstTable = ws.Tables[0];               // Access the first table
            string tableText = firstTable.ExportToString(exportOptions);
```

*Pourquoi c’est important :* L’appel `ExportToString` effectue le travail lourd de conversion de la grille Excel en un format délimité. Il respecte le `Delimiter` que vous avez défini, vous obtenez ainsi un résultat **export table as csv** propre sans traitement supplémentaire.

## Étape 4 – Écrire le texte exporté dans un fichier  

Enfin, nous persistons la chaîne sur le disque. `File.WriteAllText` est la façon la plus simple de **save txt file C#** ; il crée automatiquement le fichier s’il n’existe pas et le remplace sinon.

```csharp
            // Step 4: Write the exported text to a file
            string outputPath = @"C:\Data\ExportedTable.txt";
            File.WriteAllText(outputPath, tableText);
            System.Console.WriteLine($"Table exported successfully to {outputPath}");
        }
    }
}
```

*Pourquoi c’est important :* En écrivant directement la chaîne, vous évitez une étape de conversion supplémentaire. Le fichier contient maintenant des lignes comme `Value1;Value2;Value3`, prêtes pour n’importe quel analyseur en aval.

## Exemple complet fonctionnel (Toutes les étapes en un seul endroit)  

Voici le programme complet, prêt à copier‑coller, qui combine tout ce que nous avons abordé. Il inclut la gestion des erreurs et des commentaires pour plus de clarté.

```csharp
using Syncfusion.XlsIO;
using System;
using System.IO;

class ExcelExporter
{
    static void Main()
    {
        try
        {
            // 1️⃣ Load workbook and get first worksheet
            using (ExcelEngine excelEngine = new ExcelEngine())
            {
                IApplication app = excelEngine.Excel;
                app.DefaultVersion = ExcelVersion.Xlsx;

                string sourcePath = @"C:\Data\Sample.xlsx";
                using (FileStream fs = new FileStream(sourcePath, FileMode.Open, FileAccess.Read))
                {
                    IWorkbook wb = app.Workbooks.Open(fs);
                    IWorksheet ws = wb.Worksheets[0]; // first sheet

                    // 2️⃣ Set export options (plain text, no headers, ';' delimiter)
                    var opts = new ExportTableOptions
                    {
                        ExportAsString = true,
                        IncludeHeaders = false,
                        Delimiter = ";"
                    };

                    // 3️⃣ Export the first table to a string
                    ITable table = ws.Tables[0];
                    string csvText = table.ExportToString(opts);

                    // 4️⃣ Save the string to a .txt file
                    string destPath = @"C:\Data\ExportedTable.txt";
                    File.WriteAllText(destPath, csvText);

                    Console.WriteLine($"✅ Export complete! File saved at: {destPath}");
                }
            }
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"❌ Something went wrong: {ex.Message}");
        }
    }
}
```

**Sortie attendue** (le contenu de `ExportedTable.txt`) :

```
John;Doe;35
Jane;Smith;28
Bob;Brown;42
```

Chaque ligne correspond à une ligne de la table Excel originale, les valeurs étant séparées par des points‑virgules. Si vous changez `Delimiter = ","` vous obtiendrez un fichier CSV classique à la place.

## Questions fréquentes & cas particuliers  

### Et si mon classeur contient plusieurs tables ?  
Vous pouvez simplement changer `ws.Tables[0]` par l’indice approprié, ou parcourir `ws.Tables` :

```csharp
foreach (var tbl in ws.Tables)
{
    string txt = tbl.ExportToString(opts);
    // Save each table to a separate file or concatenate as needed
}
```

### Comment inclure les en‑têtes de colonne ?  
Définissez `IncludeHeaders = true` dans `ExportTableOptions`. Cela est utile lorsque le système en aval attend une ligne d’en‑tête.

### Puis‑je exporter vers un dossier différent de façon dynamique ?  
Absolument. Utilisez `Path.Combine` avec `Environment.GetFolderPath(Environment.SpecialFolder.Desktop)` ou tout chemin fourni par l’utilisateur pour rendre la solution plus flexible.

### Qu’en est‑il des gros fichiers ?  
Pour des tables massives, envisagez de diffuser la sortie au lieu de charger toute la chaîne en mémoire :

```csharp
using (StreamWriter writer = new StreamWriter(outputPath))
{
    writer.Write(table.ExportToString(opts));
}
```

### Cela fonctionne‑t‑il sur .NET Core ?  
Oui — Syncfusion.XlsIO prend en charge .NET 5/6/7. Il suffit de référencer le package NuGet approprié et le tour est joué.

## Astuces pro pour des exportations fiables  

- **Validez le chemin du fichier** avant d’écrire. Un répertoire manquant déclenchera `DirectoryNotFoundException`.  
- **Vérifiez `ExportAsString`** uniquement lorsque la table tient confortablement en mémoire ; sinon, utilisez `ExportToStream` pour les jeux de données volumineux.  
- **Prenez en compte la culture** : si vos données contiennent des virgules comme séparateurs décimaux, choisissez un point‑virgule (`;`) ou une tabulation (`\t`) comme séparateur pour éviter les erreurs d’analyse CSV.  
- **Verrouillage de version** : Syncfusion modifie parfois les signatures d’API. Épinglez la version du package NuGet (`<PackageReference Include="Syncfusion.XlsIO.Net.Core" Version="21.2.0.44" />`) pour garder votre build reproductible.

## Conclusion  

Dans ce guide, nous avons démontré **how to export Excel** tables to plain‑text files using C#. En chargeant le classeur, en configurant `ExportTableOptions`, en exportant la table en chaîne, et enfin en **writing the string to file**, vous disposez désormais d’un modèle robuste pour les tâches **convert excel table**, **export table as csv** et **save txt file C#**.

N’hésitez pas à expérimenter — changez le séparateur, incluez les en‑têtes, ou parcourez plusieurs tables. La même approche fonctionne pour générer des rapports CSV, alimenter des analyseurs hérités, ou simplement archiver le contenu des feuilles de calcul sous forme de fichiers texte légers.

Vous avez d’autres scénarios à aborder ? Peut‑être devez‑vous **write string to file** de façon asynchrone, ou vous souhaitez compresser la sortie à la volée. Consultez nos prochains tutoriels sur *asynchronous file I/O in C#* et *zipping files with .NET* pour poursuivre sur cette lancée.

Bon codage ! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}