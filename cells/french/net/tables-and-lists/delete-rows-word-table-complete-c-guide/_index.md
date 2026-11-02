---
category: general
date: 2026-06-08
description: Supprimez des lignes d’un tableau Word avec Aspose.Words. Apprenez à
  supprimer des lignes, à supprimer plusieurs lignes dans Word, et maîtrisez l’édition
  de tableaux en quelques minutes.
draft: false
keywords:
- delete rows word table
- how to delete rows
- delete multiple rows word
language: fr
og_description: Supprimez des lignes d’un tableau Word avec Aspose.Words. Ce tutoriel
  montre comment supprimer des lignes, supprimer plusieurs lignes Word et garder vos
  tableaux bien organisés.
og_title: Supprimer des lignes d’un tableau Word – Guide complet C#
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Delete rows word table using Aspose.Words. Learn how to delete rows,
    delete multiple rows word, and master table editing in minutes.
  headline: Delete rows word table – Complete C# Guide
  type: TechArticle
- description: Delete rows word table using Aspose.Words. Learn how to delete rows,
    delete multiple rows word, and master table editing in minutes.
  name: Delete rows word table – Complete C# Guide
  steps:
  - name: 3.1 How to delete rows (single row)
    text: 'To remove a single row, call `DeleteRows(startIndex, count)` where `startIndex`
      is zero‑based. Skipping the header row (index 0) is common:'
  - name: 3.2 Delete multiple rows word – batch removal
    text: 'When you need to drop a range—say rows 2‑6—you pass the start index and
      the number of rows to erase. This is the **delete multiple rows word** pattern:'
  - name: Expected output
    text: '- `output.docx` contains the original table **without** rows 2‑6. - All
      remaining rows shift up, preserving cell formatting and column widths. - The
      header row stays intact, keeping your column titles visible.'
  type: HowTo
- questions:
  - answer: Absolutely. Loop through `table.Rows`, inspect `row.Cells[i].GetText()`,
      and collect matching indices. Then call `DeleteRows` with the smallest index
      and total count, or delete rows in reverse order to avoid re‑indexing.
    question: Can I delete rows based on cell content instead of index?
  - answer: Yes. Aspose.Words supports both `.doc` and `.docx`. Just change the file
      extension in the `Document` constructor and `Save` call.
    question: Does this work with .doc files?
  - answer: 'Retrieve it via `doc.FirstSection.HeadersFooters` collection, then apply
      the same `DeleteRows` logic. ## Conclusion You now have a solid, end‑to‑end
      solution for **delete rows word table** using C#. The example shows *how to
      delete rows* individually and how to **delete multiple rows word** in a sin'
    question: What if the table is inside a header/footer?
  type: FAQPage
tags:
- C#
- Aspose.Words
- Word automation
title: Supprimer des lignes d'un tableau Word – Guide complet C#
url: /fr/net/tables-and-lists/delete-rows-word-table-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Supprimer des lignes d'un tableau Word – Guide complet C#

Vous avez déjà eu besoin de **delete rows word table** mais vous ne saviez pas par où commencer ? Vous n'êtes pas seul ; de nombreux développeurs rencontrent ce problème lorsqu'ils nettoient des rapports générés ou réduisent des tableaux alimentés par des données. Bonne nouvelle ? En quelques lignes de C# et Aspose.Words, vous pouvez facilement supprimer les lignes indésirables, qu'il s'agisse d'une seule ligne ou d'un lot. Dans ce guide, nous allons parcourir *how to delete rows* et même couvrir le cas plus difficile de **delete multiple rows word** en une seule fois.

Nous couvrirons tout ce que vous devez savoir : le code exact, pourquoi chaque étape est importante, les pièges courants et un exemple prêt à l'exécution. À la fin, vous pourrez supprimer des lignes de n'importe quel tableau Word sans casser la structure du document. Pas de blabla, seulement des techniques pratiques et éprouvées.

## Prérequis

Avant de commencer, assurez‑vous d'avoir :

- **Aspose.Words for .NET** (version 23.12 ou plus récente). Vous pouvez l'obtenir depuis NuGet : `Install-Package Aspose.Words`.
- Un environnement de développement .NET (Visual Studio, Rider ou VS Code avec l'extension C#).
- Un fichier Word d'entrée (`input.docx`) contenant au moins un tableau avec une ligne d’en‑tête.

C’est tout — aucune bibliothèque supplémentaire, aucune interop COM, juste du code managé pur.

## Étape 1 : Charger le document Word

La première chose à faire est d'ouvrir le document. Aspose.Words traite un fichier Word comme un objet `Document`, ce qui vous donne un accès complet aux sections, corps, tableaux, etc.

```csharp
using Aspose.Words;

class TableCleaner
{
    static void Main()
    {
        // Load the source .docx file
        Document doc = new Document(@"YOUR_DIRECTORY\input.docx");
        // Continue with table manipulation…
```

*Pourquoi c’est important :* Le chargement du document crée une représentation en mémoire, ainsi toutes les modifications sont rapides et n'affectent le système de fichiers que lorsque vous enregistrez explicitement.

## Étape 2 : Récupérer le tableau cible

Dans la plupart des scénarios, vous savez quel tableau vous voulez modifier — souvent le premier. Aspose.Words rend cela trivial via la propriété `FirstSection`.

```csharp
        // Access the first table in the first section
        Table table = doc.FirstSection.Body.Tables[0];
```

Si votre document contient plusieurs tableaux, vous pouvez parcourir `doc.GetChildNodes(NodeType.Table, true)` et choisir le bon en fonction de l’indice ou d’un marqueur personnalisé.

## Étape 3 : Supprimer des lignes – simple ou multiple

### 3.1 Comment supprimer des lignes (ligne unique)

Pour supprimer une seule ligne, appelez `DeleteRows(startIndex, count)` où `startIndex` est basé sur zéro. Ignorer la ligne d’en‑tête (indice 0) est courant :

```csharp
        // Delete just the second row (index 1)
        table.DeleteRows(1, 1);
```

### 3.2 Supprimer plusieurs lignes word – suppression par lot

Lorsque vous devez supprimer une plage — par exemple les lignes 2‑6 — vous transmettez l’indice de départ et le nombre de lignes à effacer. C’est le modèle **delete multiple rows word** :

```csharp
        // Delete rows 2‑6 (skip header at index 0)
        // startIndex = 1 (second row), count = 5 rows
        table.DeleteRows(1, 5);
```

*Pourquoi utiliser un appel unique ?* Supprimer les lignes une par une oblige le tableau à se ré‑indexer après chaque suppression, ce qui peut entraîner des erreurs et ralentir le processus. La méthode en bloc maintient la structure interne du tableau cohérente.

#### Cas limite : Suppression au‑delà de la taille du tableau

Si `startIndex + count` dépasse le nombre réel de lignes, Aspose.Words lève une `ArgumentOutOfRangeException`. Une garde défensive ressemble à ceci :

```csharp
        int rowsToDelete = Math.Min(5, table.Rows.Count - 1); // never delete the header
        if (rowsToDelete > 0)
            table.DeleteRows(1, rowsToDelete);
```

Ce fragment garantit que vous n’essayez jamais de supprimer plus de lignes qu’il n’en existe.

## Étape 4 : Enregistrer le document modifié

Une fois les lignes supprimées, persister les changements ne nécessite qu’une seule ligne :

```csharp
        // Save the cleaned document
        doc.Save(@"YOUR_DIRECTORY\output.docx");
    }
}
```

La méthode `Save` choisit automatiquement le format en fonction de l’extension du fichier, vous pouvez donc exporter en PDF, HTML ou même ODT avec un suffixe différent.

## Exemple complet fonctionnel

En rassemblant le tout, voici le programme complet, prêt à être exécuté :

```csharp
using System;
using Aspose.Words;

class TableCleaner
{
    static void Main()
    {
        // 1️⃣ Load the Word document
        Document doc = new Document(@"YOUR_DIRECTORY\input.docx");

        // 2️⃣ Access the first table (adjust index if needed)
        Table table = doc.FirstSection.Body.Tables[0];

        // 3️⃣ Delete rows 2‑6 (skip header row at index 0)
        //    This demonstrates delete multiple rows word in one call.
        if (table.Rows.Count > 1) // ensure there is at least a header + one data row
        {
            int rowsToDelete = Math.Min(5, table.Rows.Count - 1);
            table.DeleteRows(1, rowsToDelete);
        }

        // 4️⃣ Save the modified document
        doc.Save(@"YOUR_DIRECTORY\output.docx");

        Console.WriteLine("Rows removed successfully. Output saved to output.docx");
    }
}
```

### Résultat attendu

- `output.docx` contient le tableau original **sans** les lignes 2‑6.
- Toutes les lignes restantes remontent, en préservant le format des cellules et la largeur des colonnes.
- La ligne d’en‑tête reste intacte, gardant vos titres de colonnes visibles.

## Pourquoi cette approche surpasse les alternatives

| Approche | Avantages | Inconvénients |
|----------|-----------|---------------|
| **Aspose.Words `DeleteRows`** | Suppression en bloc d'une ligne, préserve les styles, aucune dépendance COM | Nécessite une bibliothèque commerciale (essai gratuit disponible) |
| Office Interop | Fonctionne avec Word natif | Nécessite Word installé sur le serveur, lent, problèmes de nettoyage COM |
| Open XML SDK | Gratuit, open source | Manipulation XML manuelle ; la suppression sécurisée des lignes est fastidieuse |

## Astuces pro & pièges courants

- **Astuce pro :** Gardez toujours la ligne d’en‑tête (indice 0) intacte, sauf si vous voulez vraiment la supprimer. Supprimer l’en‑tête peut casser les traitements en aval qui s’attendent à des noms de colonnes.
- **Attention aux cellules fusionnées.** Si une ligne contient une cellule fusionnée verticalement qui s’étend sur la ligne que vous supprimez, Aspose.Words ajustera automatiquement la plage de fusion, mais vérifiez le résultat visuel.
- **Note de performance :** Supprimer de nombreuses lignes d’un tableau massif (des milliers de lignes) reste rapide, mais si vous traitez des centaines de documents dans une boucle, envisagez de ré‑utiliser l’objet `Document` lorsque c’est possible afin de réduire la surcharge d’allocation.

## Questions fréquemment posées

**Q : Puis‑je supprimer des lignes en fonction du contenu d’une cellule plutôt que de l’indice ?**  
R : Absolument. Parcourez `table.Rows`, inspectez `row.Cells[i].GetText()`, et collectez les indices correspondants. Puis appelez `DeleteRows` avec le plus petit indice et le nombre total, ou supprimez les lignes en ordre inverse pour éviter le ré‑indexage.

**Q : Cette méthode fonctionne‑t‑elle avec les fichiers .doc ?**  
R : Oui. Aspose.Words prend en charge les fichiers `.doc` et `.docx`. Il suffit de changer l’extension du fichier dans le constructeur `Document` et l’appel `Save`.

**Q : Et si le tableau se trouve dans un en‑tête/pied de page ?**  
R : Récupérez‑le via la collection `doc.FirstSection.HeadersFooters`, puis appliquez la même logique `DeleteRows`.

## Conclusion

Vous disposez maintenant d’une solution complète, de bout en bout, pour **delete rows word table** avec C#. L’exemple montre *how to delete rows* individuellement et comment **delete multiple rows word** en un appel unique et efficace. Avec Aspose.Words, vous bénéficiez d’une API propre, sans tracas COM, et d’un contrôle total sur les documents Word.

Prêt pour le prochain défi ? Essayez d’ajouter une nouvelle ligne avec des totaux calculés, ou exportez le tableau épuré en CSV avec `Table.ToTxt`. Le ciel est la limite quand vous maîtrisez la manipulation des tableaux.

Bon codage, et que vos tableaux Word restent bien rangés !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets et fonctionnels avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Comment supprimer des lignes dans Excel avec Aspose.Cells pour Java | Guide & Tutoriel](/cells/english/java/worksheet-management/delete-row-excel-aspose-cells-java/)
- [Comment supprimer les lignes vides dans Excel avec Aspose.Cells .NET pour le nettoyage de données](/cells/english/net/data-manipulation/delete-blank-rows-aspose-cells-net/)
- [Comment insérer et supprimer des lignes dans Excel avec Aspose.Cells pour .NET&#58; Guide complet](/cells/english/net/data-manipulation/aspose-cells-net-insert-delete-excel-rows/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}