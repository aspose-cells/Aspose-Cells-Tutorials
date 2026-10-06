---
category: general
date: 2026-03-29
description: Apprenez à insérer des lignes dans GridJs rapidement. Ce guide couvre
  également comment ajouter des lignes et ajouter plusieurs lignes à la grille avec
  une opération par lot.
draft: false
keywords:
- how to insert rows
- how to add rows
- add multiple rows grid
- batch row insertion
- large grid performance
language: fr
og_description: Apprenez à insérer des lignes dans GridJs rapidement. Ce guide montre
  comment ajouter des lignes, ajouter plusieurs lignes à la grille et gérer de grandes
  insertions par lots.
og_title: Comment insérer des lignes dans GridJs – Ajouter plusieurs lignes à la grille
  efficacement
tags:
- GridJs
- C#
- data‑grid
title: Comment insérer des lignes dans GridJs – Ajouter plusieurs lignes à la grille
  efficacement
url: /fr/net/row-and-column-management/how-to-insert-rows-in-gridjs-add-multiple-rows-grid-efficien/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment insérer des lignes dans GridJs – Ajouter plusieurs lignes de grille efficacement

Vous vous êtes déjà demandé **comment insérer des lignes** dans une table GridJs massive sans bloquer l'interface ? Peut‑être avez‑vous rencontré un mur en essayant de **ajouter des lignes** une par une et les performances se sont effondrées. La bonne nouvelle, c’est que GridJs propose une API batch qui vous permet de **ajouter plusieurs lignes de grille** en un seul appel, gardant les choses rapides même lorsque vous gérez des millions d’enregistrements.

Dans ce tutoriel, nous parcourrons un exemple complet et exécutable qui montre exactement **comment insérer des lignes** en utilisant `InsertRowsBatch`. Vous verrez pourquoi le batching est important, comment vérifier le résultat, et ce à quoi il faut faire attention lorsque l’index ciblé est énorme. À la fin, vous pourrez insérer mille nouveaux enregistrements dans n’importe quelle instance GridJs en toute confiance.

## Prérequis

Avant de commencer, assurez‑vous d’avoir :

- .NET 6.0 ou supérieur (le code se compile avec n’importe quel SDK récent)
- Une référence au package NuGet `GridJs` (ou le DLL si vous utilisez une version personnalisée)
- Des connaissances de base en C# – pas besoin d’être un gourou, juste à l’aise avec les classes et les méthodes
- Un IDE ou éditeur de votre choix (Visual Studio, Rider, VS Code… tout fonctionne)

> **Astuce pro :** Si vous prévoyez de travailler avec des grilles vraiment massives (des dizaines de millions de lignes), activez `gridJs.EnableVirtualization = true;` pour garder le rendu UI léger.

## Étape 1 : Créez et configurez l'instance GridJs

Tout d’abord : vous avez besoin d’un objet `GridJs` vivant. Pensez‑y comme à la toile sur laquelle vous allez peindre des lignes.

```csharp
using System;
using GridJsLibrary;   // Assume this is the namespace for GridJs

namespace GridJsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1 – Initialize the grid
            GridJs gridJs = new GridJs();

            // Optional: turn on virtualization for huge data sets
            gridJs.EnableVirtualization = true;

            // Populate the grid with some dummy data so we can see the effect
            SeedInitialData(gridJs);

            // Now we’re ready to insert rows in bulk
            InsertRowsInBatch(gridJs);
        }

        // Helper: add 2 000 000 rows so our batch lands at index 2 000 001
        static void SeedInitialData(GridJs grid)
        {
            for (int i = 0; i < 2_000_000; i++)
            {
                grid.InsertRow(i, new object[] { $"Row {i + 1}", DateTime.Now });
            }
            Console.WriteLine("Initial seed completed – 2 000 000 rows present.");
        }
```

> **Pourquoi cette étape est importante :** Initialiser la grille et éventuellement semer des données reproduit un scénario réel où la grille contient déjà une grande quantité d’informations. L’insertion batch que nous effectuerons plus tard doit respecter l’index basé à zéro, c’est pourquoi nous pré‑remplissons pour illustrer le point d’insertion exact.

## Étape 2 : Utilisez `InsertRowsBatch` pour **Ajouter plusieurs lignes de grille**

Voici le cœur du tutoriel – l’appel qui **ajoute réellement des lignes** en masse. La signature de la méthode est `InsertRowsBatch(int startIndex, int count)`. Dans notre exemple, nous commencerons à l’index 2 000 000 (qui correspond à la 2 000 001ᵉ ligne) et ajouterons dix lignes.

```csharp
        // Step 2 – Insert a batch of rows
        static void InsertRowsInBatch(GridJs grid)
        {
            int startIndex = 2_000_000; // zero‑based, so this is row 2 000 001
            int rowsToAdd = 10;

            // The batch call creates placeholder rows; you can later populate them
            grid.InsertRowsBatch(startIndex, rowsToAdd);
            Console.WriteLine($"Inserted {rowsToAdd} rows starting at index {startIndex + 1}.");

            // Verify by reading back a few rows
            VerifyInsertion(grid, startIndex, rowsToAdd);
        }
```

> **Comment cela fonctionne :** `InsertRowsBatch` alloue le nombre de lignes demandé en interne et décale les lignes existantes vers le bas. Comme l’opération est réalisée en une seule transaction, l’UI se rafraîchit une seule fois, ce qui explique pourquoi cette méthode est la façon recommandée de **comment ajouter des lignes** efficacement.

## Étape 3 : Vérifiez l’insertion – Les lignes se sont‑elles placées où prévu ?

Après l’opération batch, vous voudrez vous assurer que les lignes sont bien à l’endroit attendu. L’assistant suivant lit la première et la dernière ligne du bloc nouvellement ajouté et les affiche dans la console.

```csharp
        // Step 3 – Simple verification
        static void VerifyInsertion(GridJs grid, int startIdx, int count)
        {
            Console.WriteLine("Verifying inserted rows:");
            for (int i = 0; i < count; i++)
            {
                var row = grid.GetRow(startIdx + i);
                Console.WriteLine($"Row {startIdx + i + 1}: {string.Join(", ", row)}");
            }
        }
    }
}
```

**Sortie attendue**

```
Initial seed completed – 2 000 000 rows present.
Inserted 10 rows starting at index 2000001.
Verifying inserted rows:
Row 2000001: , 
Row 2000002: , 
...
Row 2000010: , 
```

Les cellules vides indiquent que les lignes sont des espaces réservés en attente de données. Vous pouvez maintenant les remplir individuellement ou lancer une autre mise à jour batch.

> **Note de cas limite :** Si `startIndex` dépasse le nombre actuel de lignes, GridJs ajoutera automatiquement les nouvelles lignes à la fin. À l’inverse, un index négatif déclenche une `ArgumentOutOfRangeException`, il faut donc toujours valider les indices fournis par l’utilisateur.

## Étape 4 : Remplir les nouvelles lignes (Optionnel mais fréquent)

Souvent, vous ne voulez pas seulement des lignes vides ; vous devez les remplir avec des valeurs significatives. Vous pouvez parcourir la plage nouvellement créée et appeler `SetCell` ou une API similaire.

```csharp
        // Optional: fill the newly added rows with sample data
        static void PopulateNewRows(GridJs grid, int startIdx, int count)
        {
            for (int i = 0; i < count; i++)
            {
                int rowIdx = startIdx + i;
                grid.SetCell(rowIdx, 0, $"New Item {i + 1}");
                grid.SetCell(rowIdx, 1, DateTime.UtcNow);
            }
            Console.WriteLine("Populated the new rows with sample data.");
        }
```

Vous pourriez appeler `PopulateNewRows(gridJs, startIndex, rowsToAdd);` immédiatement après l’insertion batch si vous avez besoin que les lignes soient prêtes à l’affichage immédiatement.

## Étape 5 : Conseils de performance pour les très grandes grilles

Lorsque vous manipulez **ajouter plusieurs lignes de grille** à l’échelle du million, gardez ces astuces en tête :

1. **La taille du batch compte** – Insérer 10 000 lignes d’un coup peut être plus rapide que dix batches séparés de 1 000 lignes, car chaque batch ne déclenche qu’un seul rafraîchissement UI.
2. **Désactivez les mises à jour UI** – Certaines versions de GridJs exposent `grid.SuspendLayout()` / `grid.ResumeLayout()`. Enveloppez votre batch avec ces appels si vous remarquez du lag.
3. **Utilisez la virtualisation** – Comme montré précédemment, `EnableVirtualization` réduit drastiquement la consommation mémoire et le temps de rendu.
4. **Évitez les copies profondes** – Passez des types valeur simples ou des objets légers à la grille ; les objets lourds obligent la grille à cloner les données, ce qui nuit aux performances.

## Exemple complet fonctionnel

En rassemblant tout, voici le programme complet que vous pouvez copier‑coller dans un nouveau projet console :

```csharp
using System;
using GridJsLibrary;   // Replace with the actual namespace of your GridJs library

namespace GridJsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            GridJs gridJs = new GridJs
            {
                EnableVirtualization = true
            };

            SeedInitialData(gridJs);
            InsertRowsInBatch(gridJs);
        }

        static void SeedInitialData(GridJs grid)
        {
            for (int i = 0; i < 2_000_000; i++)
            {
                grid.InsertRow(i, new object[] { $"Row {i + 1}", DateTime.Now });
            }
            Console.WriteLine("Initial seed completed – 2 000 000 rows present.");
        }

        static void InsertRowsInBatch(GridJs grid)
        {
            int startIndex = 2_000_000; // zero‑based index for row 2 000 001
            int rowsToAdd = 10;

            grid.InsertRowsBatch(startIndex, rowsToAdd);
            Console.WriteLine($"Inserted {rowsToAdd} rows starting at index {startIndex + 1}.");

            // Optional: fill them with data
            PopulateNewRows(grid, startIndex, rowsToAdd);

            VerifyInsertion(grid, startIndex, rowsToAdd);
        }

        static void PopulateNewRows(GridJs grid, int startIdx, int count)
        {
            for (int i = 0; i < count; i++)
            {
                int rowIdx = startIdx + i;
                grid.SetCell(rowIdx, 0, $"New Item {i + 1}");
                grid.SetCell(rowIdx, 1, DateTime.UtcNow);
            }
            Console.WriteLine("Populated the new rows with sample data.");
        }

        static void VerifyInsertion(GridJs grid, int startIdx, int count)
        {
            Console.WriteLine("Verifying inserted rows:");
            for (int i = 0; i < count; i++)
            {
                var row = grid.GetRow(startIdx + i);
                Console.WriteLine($"Row {startIdx + i + 1}: {string.Join(", ", row)}");
            }
        }
    }
}
```

Exécutez le programme, et vous verrez la sortie console confirmant que les dix lignes ont été insérées à l’emplacement correct puis peuplées.

## Conclusion

Nous avons couvert **comment insérer des lignes** dans GridJs en utilisant l’API batch, démontré **comment ajouter des lignes** efficacement, et exploré des façons d’**ajouter plusieurs lignes de grille** sans étouffer l’UI. Les points clés sont :

- Utilisez `InsertRowsBatch(startIndex, count)` pour toute opération en masse.
- Validez les indices et envisagez la virtualisation pour les ensembles de données massifs.
- Remplissez les lignes après le batch si vous avez besoin d’un contenu immédiat.

Ensuite, vous pourriez explorer **comment supprimer des lignes**, implémenter **annuler/restaurer** pour les éditions batch, ou intégrer GridJs avec un service back‑end qui diffuse les données à la demande. Tous ces sujets s’appuient directement sur les concepts que vous venez d’apprendre.

N’hésitez pas à expérimenter — modifiez la taille du batch, essayez d’insérer au tout début de la grille, ou combinez plusieurs batches dans une même transaction. Plus vous jouez, plus vous serez à l’aise avec de grandes

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}