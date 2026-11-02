---
category: general
date: 2026-06-27
description: Supprimer plusieurs lignes Word avec C#. Apprenez à supprimer des lignes
  de tableau, à enlever des lignes de tableau et à modifier efficacement les tableaux
  des documents Word.
draft: false
keywords:
- delete multiple rows word
- how to delete table rows
- how to remove table rows
- delete rows from word table
- word document table editing
language: fr
og_description: Supprimez plusieurs lignes Word instantanément. Ce tutoriel montre
  comment supprimer des lignes de tableau, retirer des lignes d’un tableau Word et
  maîtriser l’édition des tableaux dans un document Word.
og_title: Supprimer plusieurs lignes dans Word – Édition de tableau étape par étape
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Delete multiple rows word using C#. Learn how to delete table rows,
    remove table rows and edit Word document tables efficiently.
  headline: Delete Multiple Rows Word – Complete Guide to Removing Table Rows
  type: TechArticle
tags:
- Aspose.Words
- C#
- Word Automation
title: Supprimer plusieurs lignes Word – Guide complet pour supprimer les lignes de
  tableau
url: /fr/net/tables-and-lists/delete-multiple-rows-word-complete-guide-to-removing-table-r/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Supprimer plusieurs lignes Word – Guide complet pour supprimer des lignes de tableau

Vous avez déjà eu besoin de **supprimer plusieurs lignes word** dans des documents mais vous ne saviez pas quelle appel d’API utiliser ? Vous n’êtes pas seul — la plupart des développeurs rencontrent le même problème lorsqu’ils essaient de réduire un tableau tout en conservant l’en‑tête intacte.  

Dans ce tutoriel, nous allons parcourir une solution concise, de bout en bout, qui montre *comment supprimer des lignes de tableau* programmatique, *comment enlever des lignes de tableau* en toute sécurité, et pourquoi cette approche fonctionne pour chaque scénario **supprimer des lignes d’un tableau Word** que vous pourriez rencontrer.

À la fin, vous disposerez d’un extrait réutilisable que vous pourrez intégrer dans n’importe quel projet C#, ainsi que de quelques astuces pour des tâches plus larges d’**édition de tableaux dans des documents Word**.

## Prérequis

- .NET 6.0 ou version ultérieure (le code fonctionne également sur .NET Framework 4.6+)
- Aspose.Words pour .NET installé (`dotnet add package Aspose.Words`)
- Une compréhension de base de la syntaxe C#
- Un fichier d’entrée `.docx` contenant au moins un tableau avec une ligne d’en‑tête

> **Astuce :** Si vous n’avez pas encore de licence, Aspose.Words propose un mode d’évaluation gratuit idéal pour les tests.

## Étape 1 : Configurer le projet et charger le document Word

Tout d’abord, créez une application console (ou intégrez‑la dans un service existant) et ajoutez les directives `using` nécessaires. Puis chargez le document source.

```csharp
using System;
using Aspose.Words;
using Aspose.Words.Tables;

class Program
{
    static void Main()
    {
        // Load the Word document (replace YOUR_DIRECTORY with your actual path)
        Document doc = new Document(@"YOUR_DIRECTORY\input.docx");
        Console.WriteLine("Document loaded successfully.");
```

**Pourquoi c’est important :**  
`Document` est le point d’entrée de chaque opération Aspose.Words. Charger le fichier une seule fois réduit la consommation de mémoire et vous donne une référence pour tous les appels ultérieurs d’édition de tableau.

## Étape 2 : Localiser le premier tableau (ou tout autre tableau dont vous avez besoin)

Si votre document contient plusieurs tableaux, vous pouvez choisir celui que vous voulez par indice ou en recherchant un mot‑clé. Pour simplifier, nous allons récupérer le premier tableau, qui contient généralement les données que nous voulons réduire.

```csharp
        // Retrieve the first table in the document
        Table firstTable = doc.GetChild(NodeType.Table, 0, true) as Table;
        if (firstTable == null)
        {
            Console.WriteLine("No table found in the document.");
            return;
        }
        Console.WriteLine($"Table with {firstTable.Rows.Count} rows found.");
```

**Explication :**  
`GetChild(NodeType.Table, 0, true)` parcourt l’arbre du document en profondeur et renvoie le premier nœud `Table` rencontré. Le cast `as Table` convertit le nœud en toute sécurité, nous permettant de travailler avec les `Rows` par la suite.

## Étape 3 : Supprimer plusieurs lignes tout en préservant l’en‑tête

Nous arrivons maintenant au cœur du sujet : **supprimer plusieurs lignes word** dans des documents. Supposons que l’en‑tête se trouve à la ligne 0 et que vous souhaitiez supprimer les deux lignes suivantes (indices 1 et 2). La méthode `DeleteRows` fait exactement cela.

```csharp
        // Delete two rows starting from the second row (index 1)
        // This keeps the header row untouched while removing the following rows
        firstTable?.DeleteRows(1, 2);
        Console.WriteLine("Specified rows deleted.");
```

### Comment supprimer des lignes de tableau – Variations

- **Supprimer une seule ligne :** `firstTable?.DeleteRows(rowIndex, 1);`
- **Supprimer toutes les lignes sauf l’en‑tête :** `firstTable?.DeleteRows(1, firstTable.Rows.Count - 1);`
- **Supprimer des lignes selon une condition :** parcourir `firstTable.Rows` et appeler `DeleteRows` lorsqu’une cellule correspond à votre critère.

Ces extraits répondent à la question fréquente **comment enlever des lignes de tableau** de manière flexible.

## Étape 4 : Enregistrer le document modifié

Une fois les lignes supprimées, il suffit d’écrire le document sur le disque. Vous pouvez écraser le fichier original ou créer une nouvelle copie.

```csharp
        // Save the modified document
        doc.Save(@"YOUR_DIRECTORY\output.docx");
        Console.WriteLine("Document saved as output.docx");
    }
}
```

**Ce que vous verrez :**  
Si le tableau d’origine contenait, par exemple, cinq lignes (en‑tête + quatre lignes de données), le `output.docx` enregistré contiendra maintenant seulement trois lignes (en‑tête + deux lignes de données restantes). Ouvrez le fichier dans Word pour vérifier que les lignes indésirables ont disparu sans affecter le reste du contenu.

![delete multiple rows word example](delete-multiple-rows-word.png)

*Texte alternatif de l’image : supprimer plusieurs lignes word – capture avant et après d’un tableau Word.*

## Exemple complet, prêt à l’exécution

En rassemblant le tout, voici le programme complet que vous pouvez copier‑coller :

```csharp
using System;
using Aspose.Words;
using Aspose.Words.Tables;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the Word document
        Document doc = new Document(@"YOUR_DIRECTORY\input.docx");
        Console.WriteLine("Document loaded.");

        // 2️⃣ Retrieve the first table
        Table firstTable = doc.GetChild(NodeType.Table, 0, true) as Table;
        if (firstTable == null)
        {
            Console.WriteLine("No table found.");
            return;
        }
        Console.WriteLine($"Found table with {firstTable.Rows.Count} rows.");

        // 3️⃣ Delete rows – this is the core of delete rows from word table
        //    Starting at index 1 (second row), delete the next two rows.
        firstTable?.DeleteRows(1, 2);
        Console.WriteLine("Rows deleted.");

        // 4️⃣ Save the result
        doc.Save(@"YOUR_DIRECTORY\output.docx");
        Console.WriteLine("Saved output.docx");
    }
}
```

Exécutez le programme, ouvrez `output.docx`, et vous verrez que l’en‑tête est toujours présent tandis que les lignes sélectionnées ont disparu. Voilà le **delete multiple rows word** en action.

## Problèmes courants & comment les éviter

| Problème | Pourquoi cela se produit | Solution |
|----------|--------------------------|----------|
| **NullReferenceException** lorsque `firstTable` est `null` | Le document ne contient aucun tableau ou l’indice est incorrect | Vérifiez toujours `firstTable != null` avant d’appeler `DeleteRows`. |
| **Lignes non supprimées** | Utilisation d’un mauvais indice de départ (les tableaux Word sont indexés à zéro) | Souvenez‑vous que l’en‑tête est la ligne 0 ; commencez à 1 pour la conserver. |
| **Écrasement d’un fichier en lecture‑seule** | Les permissions du fichier empêchent la réécriture | Enregistrez vers un autre chemin ou modifiez les attributs du fichier. |
| **Modifications inattendues de la mise en page** | Supprimer des lignes contenant des cellules fusionnées peut corrompre le tableau | Gérez les cellules fusionnées — dé‑fusionnez d’abord ou supprimez les lignes entières avec précaution. |

## Étendre la solution – Plus d’édition de tableaux dans les documents Word

Si vous êtes intéressé par une **édition de tableaux dans des documents Word** plus large, envisagez les étapes suivantes :

- **Insérer de nouvelles lignes** : `firstTable?.Rows.Add(new Row(doc));`
- **Mettre à jour le texte d’une cellule** : `firstTable.Rows[rowIndex].Cells[colIndex].Paragraphs[0].AppendText("New value");`
- **Appliquer des styles** : utilisez `CellFormat` ou `RowFormat` pour définir l’ombrage, les bordures ou les propriétés de police.
- **Exporter en PDF** : `doc.Save("output.pdf", SaveFormat.Pdf);`

Toutes ces opérations s’appuient sur le même modèle d’objet que celui utilisé pour la suppression de lignes, ce qui maintient la cohérence de votre base de code.

## Conclusion

Nous venons de vous montrer comment **supprimer plusieurs lignes word** dans des documents avec quelques lignes de code C#. L’approche couvre *comment supprimer des lignes de tableau*, *comment enlever des lignes de tableau*, ainsi que le sujet plus large de **l’édition de tableaux dans des documents Word**.  

Vous disposez désormais d’un modèle solide et réutilisable : chargez le document, localisez le tableau, appelez `DeleteRows` avec les bons indices, puis enregistrez. À partir de là, vous pouvez ajuster la plage de lignes, parcourir plusieurs tableaux ou combiner d’autres fonctionnalités d’édition pour répondre à n’importe quelle tâche d’automatisation.

Prêt à aller plus loin ? Essayez d’automatiser la génération de factures, de nettoyer des modèles de rapports, ou de créer un outil de mise à jour massive qui traite des dizaines de fichiers Word en une fois. Le ciel est la limite, et l’API rend cela sans effort.

Si vous rencontrez des difficultés, laissez un commentaire ci‑dessous—bon codage !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Comment insérer et supprimer des lignes dans Excel avec Aspose.Cells pour .NET : guide complet](/cells/english/net/data-manipulation/aspose-cells-net-insert-delete-excel-rows/)
- [Supprimer plusieurs lignes dans Excel avec Aspose.Cells .NET : guide complet pour la manipulation de données](/cells/english/net/data-manipulation/delete-rows-excel-aspose-cells-net/)
- [Supprimer plusieurs lignes dans Aspose.Cells .NET](/cells/english/net/row-and-column-management/delete-multiple-rows-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}