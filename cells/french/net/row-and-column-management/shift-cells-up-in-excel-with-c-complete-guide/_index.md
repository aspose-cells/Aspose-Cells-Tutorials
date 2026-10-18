---
category: general
date: 2026-07-13
description: Déplacez les cellules vers le haut dans Excel avec C#. Découvrez comment
  supprimer les premières lignes, effacer plusieurs lignes et retirer des lignes d’un
  tableau en une seule opération sécurisée.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- shift cells up
- remove first rows
- remove rows from table
- delete multiple rows
- how to delete rows
language: fr
lastmod: 2026-07-13
og_description: Déplacez les cellules vers le haut dans une feuille Excel en utilisant
  C#. Ce tutoriel montre comment supprimer les premières lignes, supprimer plusieurs
  lignes et supprimer en toute sécurité des lignes d’un tableau.
og_image_alt: Screenshot of C# code that shifts cells up after deleting rows in an
  Excel worksheet
og_title: Déplacer les cellules vers le haut dans Excel avec C# – Guide complet de
  programmation
schemas:
- author: Aspose
  dateModified: '2026-07-13'
  description: Shift cells up in Excel using C#. Learn how to remove first rows, delete
    multiple rows, and remove rows from table in a single, safe operation.
  headline: Shift Cells Up in Excel with C# – Complete Guide
  type: TechArticle
- questions:
  - answer: Absolutely. Loop through `sheet.Cells.Rows` and call `DeleteRows(rowIndex,
      1, true)` whenever the condition matches. Just remember to iterate backwards
      to avoid index shifting.
    question: Can I delete rows based on a condition instead of a fixed index?
  - answer: Yes. Aspose.Cells supports both `.xlsx` and legacy `.xls` formats. The
      same API applies.
    question: Does this work with `.xls` files?
  - answer: 'Target the specific table by name: `Table myTable = sheet.Tables["MyTable"];`
      then use `myTable.Range.StartRow` to calculate the rows to delete. --- ## Full
      Working Example Below is the complete, ready‑to‑run program that incorporates
      everything we discussed. Copy‑paste it into a console app, adjust'
    question: What if my workbook contains multiple tables and I only want to affect
      one?
  type: FAQPage
tags:
- Aspose.Cells
- C#
- Excel automation
title: Déplacer les cellules vers le haut dans Excel avec C# – Guide complet
url: /fr/net/row-and-column-management/shift-cells-up-in-excel-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Décaler les cellules vers le haut dans Excel avec C# – Guide complet

Vous êtes-vous déjà demandé comment **déplacer les cellules vers le haut** après avoir supprimé des lignes dans un fichier Excel ? Vous n'êtes pas le seul. Que vous nettoyiez des données importées ou que vous réduisiez un rapport volumineux, la capacité à supprimer les premières lignes sans casser un tableau est une compétence indispensable pour tout développeur C#.

Dans ce tutoriel, nous parcourrons une solution pratique, de bout en bout, qui montre **comment supprimer des lignes**, garder votre en‑tête intacte, et déplacer automatiquement les cellules restantes vers le haut. À la fin, vous pourrez **supprimer des lignes d’un tableau**, **supprimer plusieurs lignes**, et **supprimer les premières lignes** en quelques lignes de code seulement.

---

## Ce dont vous avez besoin

- .NET 6+ (ou .NET Framework 4.7.2 et supérieur)  
- La bibliothèque **Aspose.Cells for .NET** (version d’essai gratuite ou licence)  
- Une compréhension de base du C# et de Visual Studio (ou tout autre IDE de votre choix)  

Aucune autre dépendance — juste le package NuGet et un fichier Excel avec lequel travailler.

---

## Étape 1 : Installer Aspose.Cells

Première chose, ajoutez le package Aspose.Cells à votre projet :

```bash
dotnet add package Aspose.Cells
```

Cette ligne unique récupère tout ce dont vous avez besoin pour travailler avec les classeurs, les feuilles de calcul et les tableaux. Si vous utilisez Visual Studio, vous pouvez également faire un clic droit sur le projet → **Manage NuGet Packages** → rechercher *Aspose.Cells* et cliquer sur **Install**.

*Astuce :* Utilisez la dernière version stable ; en juillet 2026, c’est la **23.9.0**, qui prend en charge les formats de fichiers Excel les plus récents.

---

## Étape 2 : Charger le classeur contenant le tableau

Nous allons maintenant ouvrir le fichier Excel qui contient les données à nettoyer. Remplacez `YOUR_DIRECTORY` par le chemin réel sur votre machine.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load the workbook that contains the table
        Workbook workbook = new Workbook(@"C:\Data\table.xlsx");
        
        // Grab the first worksheet (index 0)
        Worksheet sheet = workbook.Worksheets[0];
        
        // Optional: get a reference to the first table for context
        Table table = sheet.Tables[0];
```

À ce stade, nous disposons d’un objet `Worksheet` prêt à être manipulé. Notez que nous n’avons pas encore touché au tableau — préserver l’en‑tête est crucial lorsque nous allons **déplacer les cellules vers le haut**.

---

## Étape 3 : Supprimer les deux premières lignes tout en décalant les cellules vers le haut

Voici le cœur du sujet : supprimer des lignes *et* faire monter les cellules en dessous automatiquement. Aspose.Cells fournit une méthode `DeleteRows` qui fait exactement cela lorsque vous passez `true` pour le paramètre `shiftCellsUp`.

```csharp
        // Delete the first two rows (row index starts at 0)
        // The third argument ‑‑> true tells Aspose.Cells to shift cells up.
        sheet.Cells.DeleteRows(0, 2, true);
```

### Pourquoi le drapeau `true` est important

Si vous omettez le drapeau `true`, les lignes sont supprimées mais l’espace qu’elles occupaient reste vide, créant des trous dans vos données. Le mettre à **true** indique à la bibliothèque de compacter la plage, ce qui **déplace les cellules vers le haut** de façon à ce que la ligne 3 devienne la nouvelle ligne 1. C’est la façon la plus propre de **supprimer les premières lignes** sans casser les formules ou la structure du tableau.

> **Important :** Supprimer des lignes qui incluent l’en‑tête du tableau déclenchera une exception. Conservez la ligne d’en‑tête (généralement la ligne 0) intacte, ou supprimez‑la séparément après avoir recréé l’en‑tête du tableau.

---

## Étape 4 : Vérifier que le tableau est toujours correct

Après la suppression, il est judicieux de vérifier que la référence du tableau pointe toujours vers la bonne plage. Vous pouvez afficher l’adresse du tableau ou le rafraîchir :

```csharp
        // Refresh the table range to reflect the new data area
        table.Refresh();

        // Output the new range for debugging
        Console.WriteLine($"Table now spans: {table.Ref}");
```

L’exécution du programme devrait afficher quelque chose comme `Table1!A1:D8` au lieu de l’original `A1:D10`, confirmant que les lignes ont été retirées et que les cellules ont été déplacées vers le haut.

---

## Étape 5 : Enregistrer le classeur modifié

Enfin, écrivez les modifications sur le disque. Vous pouvez écraser le fichier original ou créer une nouvelle copie — c’est à vous de choisir.

```csharp
        // Save the workbook with the changes
        workbook.Save(@"C:\Data\modified_table.xlsx");
    }
}
```

Ouvrez `modified_table.xlsx` dans Excel, et vous verrez les deux premières lignes disparues, les lignes restantes déplacées vers le haut, et le tableau toujours intact. L’opération a effectivement **supprimé plusieurs lignes** tout en préservant l’intégrité des données.

---

## Cas limites & pièges courants

| Situation | Ce qui se passe | Comment le gérer |
|-----------|----------------|------------------|
| **La ligne d’en‑tête fait partie de la plage à supprimer** | Aspose.Cells lève `InvalidOperationException` parce qu’un tableau ne peut pas perdre son en‑tête. | Supprimez uniquement les lignes de données, ou recréez l’en‑tête après la suppression avec `sheet.Cells["A1"].PutValue("Header")`. |
| **Le tableau s’étend sur plusieurs feuilles** | Supprimer des lignes sur une feuille n’affecte pas les autres. | Parcourez les tableaux de chaque feuille si vous avez besoin d’un nettoyage global. |
| **Fichiers volumineux (>100 Mo)** | La consommation de mémoire augmente fortement. | Utilisez `LoadOptions` avec `MemoryPreference` réglé sur `MemoryPreference.MemoryOnly` pour réduire l’empreinte RAM. |
| **Vous devez conserver les formules qui référencent les lignes supprimées** | Les formules peuvent devenir `#REF!`. | Utilisez `sheet.Cells.DeleteRows(startRow, count, true, true)` — le quatrième argument indique à Aspose.Cells de mettre à jour les formules. |

---

## Questions fréquentes

**Q : Puis‑je supprimer des lignes en fonction d’une condition plutôt que d’un indice fixe ?**  
R : Bien sûr. Parcourez `sheet.Cells.Rows` et appelez `DeleteRows(rowIndex, 1, true)` chaque fois que la condition est remplie. N’oubliez pas d’itérer à l’envers pour éviter le décalage d’indices.

**Q : Cette méthode fonctionne‑t‑elle avec les fichiers `.xls` ?**  
R : Oui. Aspose.Cells prend en charge les formats `.xlsx` et les anciens `.xls`. L’API est la même.

**Q : Et si mon classeur contient plusieurs tableaux et que je ne veux en affecter qu’un ?**  
R : Ciblez le tableau spécifique par son nom : `Table myTable = sheet.Tables["MyTable"];` puis utilisez `myTable.Range.StartRow` pour calculer les lignes à supprimer.

---

## Exemple complet fonctionnel

Voici le programme complet, prêt à être exécuté, qui intègre tout ce dont nous avons parlé. Copiez‑collez‑le dans une application console, ajustez les chemins de fichiers, et appuyez sur **F5**.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the workbook
        Workbook workbook = new Workbook(@"C:\Data\table.xlsx");
        Worksheet sheet = workbook.Worksheets[0];

        // 2️⃣ (Optional) Reference the first table for context
        Table table = sheet.Tables[0];

        // 3️⃣ Delete the first two rows and shift cells up
        //    Row index starts at 0, delete 2 rows, shift up = true
        sheet.Cells.DeleteRows(0, 2, true);

        // 4️⃣ Refresh the table range so it reflects the new data area
        table.Refresh();

        // 5️⃣ Show the new table reference (useful for debugging)
        Console.WriteLine($"Table now spans: {table.Ref}");

        // 6️⃣ Save the modified workbook
        workbook.Save(@"C:\Data\modified_table.xlsx");

        Console.WriteLine("Rows removed and cells shifted up successfully!");
    }
}
```

**Résultat attendu :**  
- Les lignes 1‑2 disparaissent de la feuille.  
- La ligne 3 devient la nouvelle ligne 1, la ligne 4 devient la ligne 2, etc.  
- La plage du tableau se met à jour automatiquement, confirmant que le **déplacement des cellules vers le haut** a fonctionné comme prévu.

---

## Conclusion

Nous venons de voir comment **déplacer les cellules vers le haut** dans une feuille Excel en utilisant C#. En tirant parti de la méthode `DeleteRows` d’Aspose.Cells avec le drapeau `true`, vous pouvez supprimer en toute sécurité les **premières lignes**, **supprimer plusieurs lignes**, et **supprimer des lignes d’un tableau** sans compromettre votre modèle de données. Cette approche est rapide, fiable, et fonctionne avec tous les formats Excel modernes.

Prêt pour l’étape suivante ? Essayez de combiner cette technique avec un filtre conditionnel pour purger les lignes contenant des cellules vides ou des doublons. Ou explorez les API de style d’Aspose.Cells pour réappliquer la mise en forme après le décalage. Le ciel est la limite quand vous maîtrisez la manipulation des lignes dans Excel.

Des questions ou un cas d’usage intéressant à partager ? Laissez un commentaire ci‑dessous, et bon codage !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Delete Multiple Rows in Excel with Aspose.Cells .NET&#58; A Comprehensive Guide for Data Manipulation](/cells/english/net/data-manipulation/delete-rows-excel-aspose-cells-net/)
- [How to Insert and Delete Rows in Excel with Aspose.Cells for .NET&#58; A Comprehensive Guide](/cells/english/net/data-manipulation/aspose-cells-net-insert-delete-excel-rows/)
- [How to Delete Blank Rows in Excel Using Aspose.Cells .NET for Data Cleanup](/cells/english/net/data-manipulation/delete-blank-rows-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}