---
category: general
date: 2026-03-01
description: Créer un nouveau classeur et copier la feuille de calcul dans le classeur
  contenant un tableau croisé dynamique. Apprenez comment exporter le tableau croisé
  dynamique, copier la feuille et copier le tableau croisé dynamique en C#.
draft: false
keywords:
- create new workbook
- copy worksheet to workbook
- export pivot table
- how to copy sheet
- how to copy pivot
language: fr
og_description: Créer un nouveau classeur en C# et copier une feuille de calcul dans
  le classeur tout en conservant le tableau croisé dynamique. Guide étape par étape
  avec le code complet.
og_title: Créer un nouveau classeur – Copier la feuille de calcul et le tableau croisé
  dynamique en C#
tags:
- C#
- Aspose.Cells
- Excel automation
title: Créer un nouveau classeur – Comment copier une feuille de calcul avec un tableau
  croisé dynamique
url: /fr/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un nouveau classeur – Copier une feuille de calcul et un tableau croisé dynamique en C#

Vous avez déjà eu besoin de **create new workbook** qui contient un tableau croisé dynamique prêt à l'emploi sans le reconstruire à partir de zéro ? Vous n'êtes pas le seul. Dans de nombreux scénarios de reporting, vous avez un fichier maître (`src.xlsx`) avec un tableau croisé dynamique complexe, et vous souhaitez envoyer une copie propre (`dest.xlsx`) à un client ou à un autre système. Bonne nouvelle ? Vous pouvez le faire en seulement deux lignes de C# — et ce guide vous montrera exactement comment.

Nous parcourrons l'ensemble du processus : charger le classeur source, copier la première feuille de calcul (qui contient le tableau croisé dynamique), et l'enregistrer en tant que nouveau classeur. À la fin, vous saurez **how to copy sheet** qui contient un tableau croisé dynamique, comment **export pivot table** les données si vous en avez besoin, et même quelques astuces pour les cas particuliers comme la copie dans un fichier existant.

## Prérequis

- .NET 6.0 ou version ultérieure (toute version récente fonctionne)
- Aspose.Cells for .NET (version d'essai gratuite ou version sous licence) – cette bibliothèque fournit la classe `Workbook` utilisée ci‑dessous.
- Un fichier Excel source (`src.xlsx`) qui contient déjà un tableau croisé dynamique sur sa première feuille.

Si vous n'avez pas encore Aspose.Cells, ajoutez-le via NuGet :

```bash
dotnet add package Aspose.Cells
```

C’est tout — pas d’interop COM supplémentaire, pas d’Excel installé sur le serveur.

## Ce que couvre ce tutoriel

- **Create new workbook** à partir d’une feuille existante qui contient un tableau croisé dynamique.
- **Copy worksheet to workbook** tout en préservant toutes les définitions du tableau croisé dynamique.
- **Export pivot table** les données vers un `DataTable` (optionnel).
- Pièges courants lors de l’utilisation de **how to copy pivot** dans différents environnements.
- Un exemple complet et exécutable que vous pouvez intégrer dans une application console.

---

## Étape 1 : Charger le classeur source (How to Copy Sheet)

La première chose à faire est d'ouvrir le classeur qui contient le tableau croisé dynamique. Utiliser Aspose.Cells rend cela simple car il lit le fichier en mémoire sans lancer Excel.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class Program
{
    static void Main()
    {
        // Path to the source workbook that holds the pivot
        string srcPath = @"YOUR_DIRECTORY\src.xlsx";

        // Load the workbook – this is where we **create new workbook** later
        Workbook sourceWorkbook = new Workbook(srcPath);
```

> **Pourquoi c’est important :** Le chargement du fichier valide que le tableau croisé dynamique existe et vous donne accès à la collection de feuilles de calcul. Si le fichier est corrompu, `Workbook` lève une exception claire, vous évitant ainsi des sorties mystérieuses plus tard.

## Étape 2 : Copier la feuille de calcul dans un nouveau classeur (Copy Worksheet to Workbook)

Nous allons maintenant réellement **copy worksheet to workbook**. La méthode `CopyTo` d’Aspose.Cells clone toute la feuille — y compris les formules, le formatage et le cache du tableau croisé dynamique — dans un nouveau fichier.

```csharp
        // Destination path for the new workbook
        string destPath = @"YOUR_DIRECTORY\dest.xlsx";

        // Copy the first worksheet (index 0) which contains the pivot
        sourceWorkbook.Worksheets[0].CopyTo(destPath);
```

> **Astuce pro :** `CopyTo` crée un tout nouveau classeur en arrière‑plan, vous n’avez donc pas besoin d’instancier un autre objet `Workbook`. Cela maintient une faible utilisation de la mémoire et garantit que la définition du tableau croisé dynamique reste intacte.

## Étape 3 : Vérifier le tableau croisé dynamique copié (How to Copy Pivot)

Après la copie, il est judicieux d'ouvrir le nouveau fichier et de confirmer que le tableau croisé dynamique fonctionne toujours. Vous pouvez le faire programmatiquement ou simplement l'ouvrir dans Excel.

```csharp
        // Optional: Load the destination workbook to verify
        Workbook destWorkbook = new Workbook(destPath);
        Worksheet copiedSheet = destWorkbook.Worksheets[0];

        // Find the first pivot table on the copied sheet
        PivotTable pivot = copiedSheet.PivotTables[0];

        Console.WriteLine($"Pivot name: {pivot.Name}");
        Console.WriteLine($"Data source range: {pivot.DataSource}");
        Console.WriteLine($"Number of rows in pivot cache: {pivot.CacheDefinition.RecordCount}");
    }
}
```

L'exécution du programme affiche quelque chose comme :

```
Pivot name: PivotTable1
Data source range: A1:D100
Number of rows in pivot cache: 100
```

Si vous voyez ces valeurs, l’étape **how to copy pivot** a réussi.

## Étape 4 : (Optionnel) Exporter les données du tableau croisé dynamique vers un DataTable

Parfois vous avez besoin des chiffres bruts du tableau croisé dynamique sans ouvrir Excel. Aspose.Cells vous permet d'extraire les données du tableau croisé dynamique dans un `DataTable` — parfait pour un traitement ultérieur ou des réponses d'API.

```csharp
        // Export pivot data to a DataTable
        DataTable pivotData = pivot.ExportDataTable(pivot.RowFields[0].Name, 
                                                   pivot.ColumnFields[0].Name,
                                                   true);

        // Display a few rows in the console
        foreach (DataRow row in pivotData.Rows)
        {
            Console.WriteLine(string.Join("\t", row.ItemArray));
        }
```

> **Pourquoi vous pourriez vouloir cela :** L'exportation vous permet de **export pivot table** le contenu vers une base de données, une charge JSON, ou tout autre format sans copier‑coller manuel.

## Étape 5 : Cas limites et pièges courants

### Copier dans un classeur existant

Si vous devez **copy worksheet to workbook** qui contient déjà d'autres feuilles, utilisez la surcharge qui prend une instance `Workbook` cible :

```csharp
        Workbook targetWorkbook = new Workbook(); // empty workbook
        sourceWorkbook.Worksheets[0].CopyTo(targetWorkbook);
        targetWorkbook.Save(@"YOUR_DIRECTORY\combined.xlsx");
```

### Conserver les sources de données externes

Les tableaux croisés dynamiques qui tirent des connexions externes (par ex., Power Query) peuvent perdre leur lien après la copie. Dans ces cas, définissez `pivot.RefreshDataOnOpen = true` avant d'enregistrer :

```csharp
        pivot.RefreshDataOnOpen = true;
```

### Gros fichiers et performances

Pour les fichiers de plus de 50 Mo, envisagez d'activer `WorkbookSettings.MemorySetting = MemorySetting.MemoryPreference;` afin de réduire la pression mémoire.

---

![Create new workbook example](https://example.com/images/create-new-workbook.png "Create new workbook")

*Texte alternatif de l'image : créer un nouveau classeur – copier une feuille de calcul avec un tableau croisé dynamique*

## Exemple complet fonctionnel (Toutes les étapes combinées)

Voici l'application console complète, prête à être exécutée. Copiez‑collez‑la dans un nouveau `.csproj` et appuyez sur **F5**.

```csharp
using Aspose.Cells;
using System;
using System.Data;

namespace CopyPivotDemo
{
    class Program
    {
        static void Main()
        {
            // ==============================
            // 1️⃣ Load the source workbook
            // ==============================
            string srcPath = @"YOUR_DIRECTORY\src.xlsx";
            Workbook sourceWorkbook = new Workbook(srcPath);

            // ==============================
            // 2️⃣ Copy the first worksheet (pivot) to a new workbook
            // ==============================
            string destPath = @"YOUR_DIRECTORY\dest.xlsx";
            sourceWorkbook.Worksheets[0].CopyTo(destPath);

            // ==============================
            // 3️⃣ Verify the copied pivot (how to copy pivot)
            // ==============================
            Workbook destWorkbook = new Workbook(destPath);
            Worksheet copiedSheet = destWorkbook.Worksheets[0];
            PivotTable pivot = copiedSheet.PivotTables[0];

            Console.WriteLine($"Pivot name: {pivot.Name}");
            Console.WriteLine($"Data source range: {pivot.DataSource}");
            Console.WriteLine($"Cache rows: {pivot.CacheDefinition.RecordCount}");

            // ==============================
            // 4️⃣ (Optional) Export pivot data
            // ==============================
            if (pivot.RowFields.Count > 0 && pivot.ColumnFields.Count > 0)
            {
                DataTable dt = pivot.ExportDataTable(
                    pivot.RowFields[0].Name,
                    pivot.ColumnFields[0].Name,
                    true);

                Console.WriteLine("\n--- Pivot Data Preview ---");
                foreach (DataRow row in dt.Rows)
                {
                    Console.WriteLine(string.Join("\t", row.ItemArray));
                }
            }

            Console.WriteLine("\nDone! New workbook created at: " + destPath);
        }
    }
}
```

### Résultat attendu

- `dest.xlsx` apparaît dans `YOUR_DIRECTORY`.
- La première feuille ressemble exactement à l'originale, complète avec le tableau croisé dynamique.
- L'exécution de la console imprime les métadonnées du tableau croisé dynamique et un petit aperçu des données, confirmant que la copie a réussi.

## Conclusion

Vous savez maintenant comment **create new workbook** en copiant une feuille de calcul contenant un tableau croisé dynamique, comment **copy worksheet to workbook**, et même comment **export pivot table** les données pour un traitement en aval. Que vous construisiez un service de reporting, automatisiez la distribution d'Excel, ou que vous ayez simplement besoin d’une méthode rapide pour dupliquer un tableau croisé dynamique, les étapes ci‑dessus vous offrent une solution fiable et prête pour la production.

**Prochaines étapes** que vous pourriez explorer :

- Combiner plusieurs feuilles (utilisez `CopyTo` à plusieurs reprises) – idéal pour empaqueter un rapport complet.
- Ajuster les paramètres de rafraîchissement du cache du tableau croisé dynamique lorsque les données source changent.
- Utiliser les techniques **how to copy sheet** pour dupliquer des graphiques, des images ou des modules VBA.
- Plonger dans `WorkbookDesigner` d’Aspose.Cells pour la génération de rapports basée sur des modèles.

Essayez, ajustez les chemins, et voyez à quel point il est facile d’expédier des classeurs propres, prêts pour les tableaux croisés dynamiques. Des questions sur les cas limites ou la licence ? Laissez un commentaire ci‑dessous, et bon codage !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}