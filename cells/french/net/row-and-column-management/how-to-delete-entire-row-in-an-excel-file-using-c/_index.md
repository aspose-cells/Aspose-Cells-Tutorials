---
category: general
date: 2026-10-10
description: Apprenez comment supprimer une ligne entière dans un classeur Excel avec
  C#. Ce guide étape par étape couvre également comment supprimer une ligne par indice
  et la retirer par indice en utilisant Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- delete entire row
- how to delete row
- remove row by index
- delete row excel
- delete row c#
language: fr
lastmod: 2026-10-10
og_description: Supprimez une ligne entière d’un classeur Excel en C#. Suivez ce guide
  pour apprendre comment supprimer une ligne par indice, retirer une ligne par indice
  et enregistrer le fichier en toute sécurité.
og_image_alt: Screenshot of an Excel worksheet before and after deleting an entire
  row with C# code
og_title: Supprimer toute la ligne dans Excel avec C# – guide complet de programmation
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Learn how to delete entire row in an Excel workbook with C#. This step‑by‑step
    guide also covers how to delete row by index and remove row by index using Aspose.Cells.
  headline: How to delete entire row in an Excel file using C#
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
title: Comment supprimer une ligne entière dans un fichier Excel en C#
url: /fr/net/row-and-column-management/how-to-delete-entire-row-in-an-excel-file-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Supprimer une ligne entière dans un fichier Excel avec C#

Si vous devez **supprimer une ligne entière** dans un classeur Excel, ce guide vous montre exactement comment le faire avec C#. Que vous nettoyiez des données importées ou que vous construisiez un outil de reporting, les étapes ci‑dessous vous permettent de supprimer une ligne par son indice et d’enregistrer le résultat sans perdre les autres données.

Vous verrez également comment la même approche répond à la question **how to delete row** par indice, comment **remove row by index**, et pourquoi cela fonctionne pour les scénarios **delete row excel** en C#.

## Prérequis

* .NET 6.0 ou version ultérieure (le code fonctionne également avec .NET Framework 4.6+)  
* La bibliothèque **Aspose.Cells for .NET** (disponible via NuGet : `Install-Package Aspose.Cells`)  
* Familiarité de base avec les projets console ou desktop C#  

Aucun composant Excel interop ou COM supplémentaire n’est requis, ce qui rend la solution légère et sûre pour une exécution côté serveur.

## Étape 1 : Configurer le projet et importer les espaces de noms

Créez une nouvelle application console (ou ajoutez le code à un projet existant) et ajoutez les directives `using` requises :

```csharp
using System;
using Aspose.Cells;

namespace ExcelRowDeletion
{
    class Program
    {
        static void Main(string[] args)
        {
            // The rest of the tutorial code lives here.
        }
    }
}
```

*Pourquoi c’est important* : l’importation de `Aspose.Cells` vous donne accès à `Workbook`, `Worksheet` et à la méthode `DeleteRows` qui effectue réellement la suppression de la ligne.

## Étape 2 : Charger le classeur et sélectionner la feuille de calcul

Vous devez charger le fichier source (`input.xlsx`) et obtenir la feuille de calcul que vous souhaitez modifier. La première feuille est accessible avec l’indice `0`.

```csharp
// Load the workbook from disk
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Get the first worksheet (you can also use workbook.Worksheets["SheetName"])
Worksheet ws = workbook.Worksheets[0];
```

> **Astuce** : Si vous devez travailler avec une feuille spécifique, remplacez l’indice par le nom de la feuille : `workbook.Worksheets["Data"]`.

## Étape 3 : Supprimer la ligne entière par son indice zéro‑basé

Aspose.Cells utilise un indexage zéro‑basé, ainsi la première ligne est `0`. Pour supprimer la ligne 5 (la sixième ligne visible), appelez `DeleteRows` avec `DeleteOptions.DeleteEntireRow`.

```csharp
// Delete one row starting at index 5 (zero‑based) and remove the whole row
ws.Cells[5, 0].DeleteRows(1, DeleteOptions.DeleteEntireRow);
```

*Explication* :

* `ws.Cells[5, 0]` pointe vers la première cellule de la ligne que vous souhaitez supprimer.  
* `DeleteRows(1, DeleteOptions.DeleteEntireRow)` indique à Aspose.Cells de supprimer **1** ligne, et le drapeau `DeleteEntireRow` garantit que **toute la ligne** disparaît, décalant les lignes situées en dessous vers le haut.

### Comment supprimer une ligne par indice dans d’autres scénarios

* **Supprimer plusieurs lignes consécutives** – modifiez le premier argument pour indiquer le nombre de lignes à effacer :

  ```csharp
  // Remove rows 5, 6 and 7 (three rows total)
  ws.Cells[5, 0].DeleteRows(3, DeleteOptions.DeleteEntireRow);
  ```

* **Supprimer la dernière ligne** – utilisez `ws.Cells.MaxDataRow` pour obtenir l’indice de la dernière ligne remplie :

  ```csharp
  int lastRow = ws.Cells.MaxDataRow;
  ws.Cells[lastRow, 0].DeleteRows(1, DeleteOptions.DeleteEntireRow);
  ```

Ces extraits répondent à la nécessité de **remove row by index** tout en conservant un code facile à lire.

## Étape 4 : Enregistrer le classeur avec la ligne supprimée

Après la suppression, écrivez le classeur modifié sur le disque. Vous pouvez écraser le fichier original ou en créer un nouveau.

```csharp
// Save the workbook to a new file (or overwrite the original)
workbook.Save("YOUR_DIRECTORY/output.xlsx");
```

Si vous devez conserver le fichier original inchangé, modifiez simplement le chemin de sortie. La méthode `Save` prend en charge de nombreux formats (`.xls`, `.csv`, `.pdf`, etc.) – il suffit de changer l’extension du fichier.

## Exemple complet fonctionnel

En rassemblant tous les éléments, voici un programme complet, prêt à être exécuté :

```csharp
using System;
using Aspose.Cells;

namespace ExcelRowDeletion
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the workbook
            Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

            // 2️⃣ Select the first worksheet
            Worksheet ws = workbook.Worksheets[0];

            // 3️⃣ Delete the entire row at index 5 (sixth visual row)
            ws.Cells[5, 0].DeleteRows(1, DeleteOptions.DeleteEntireRow);

            // 4️⃣ Save the result
            workbook.Save("YOUR_DIRECTORY/output.xlsx");

            Console.WriteLine("Row deleted successfully. Output saved to output.xlsx");
        }
    }
}
```

**Sortie attendue** : après l’exécution du programme, `output.xlsx` contiendra toutes les lignes originales sauf celle qui commençait à la ligne visuelle 6. Toutes les données situées sous la ligne supprimée sont automatiquement décalées vers le haut, préservant les formules et le formatage.

## Pièges courants et comment les éviter

| Problème | Pourquoi cela se produit | Solution |
|----------|--------------------------|----------|
| **Index hors limites** | Essayer de supprimer un indice de ligne qui n’existe pas (par ex., `ws.Cells[1000,0]` dans une feuille de 200 lignes) | Utilisez `ws.Cells.MaxDataRow` pour vérifier le plus grand indice valide avant d’appeler `DeleteRows`. |
| **Suppression partielle de ligne** | Omettre `DeleteOptions.DeleteEntireRow` ne supprime que le contenu des cellules | Passez toujours `DeleteOptions.DeleteEntireRow` lorsque vous devez supprimer toute la ligne. |
| **Modifications inattendues de formules** | Supprimer des lignes qui font partie d’une plage de formules peut rompre les références | Ré‑évaluez les formules après la suppression (`workbook.CalculateFormula()`) si votre classeur dépend de plages dynamiques. |
| **Enregistrement dans un emplacement en lecture‑seule** | L’appel `Save` lève une exception si le dossier est protégé | Assurez‑vous que le répertoire cible est accessible en écriture ou exécutez le programme avec les permissions appropriées. |

Traiter ces problèmes rend la solution robuste pour une utilisation en production et répond aux requêtes **delete row excel** et **delete row c#**.

## Avancé : Suppression de lignes selon une condition

Parfois, vous devez supprimer des lignes qui répondent à un certain critère (par ex., les lignes où la colonne A est vide). La boucle suivante montre une façon sûre de parcourir de bas en haut et de supprimer les lignes correspondantes :

```csharp
int lastRow = ws.Cells.MaxDataRow;
for (int row = lastRow; row >= 0; row--)
{
    // Check if column A (index 0) is empty
    if (ws.Cells[row, 0].StringValue == string.Empty)
    {
        ws.Cells[row, 0].DeleteRows(1, DeleteOptions.DeleteEntireRow);
    }
}
workbook.Save("YOUR_DIRECTORY/cleaned.xlsx");
```

Parcourir de bas en haut évite le problème de décalage d’indices qui se produit lorsqu’on supprime des lignes tout en itérant vers l’avant.

## Conclusion

Vous savez maintenant comment **supprimer une ligne entière** dans un classeur Excel avec C#. Le guide a couvert :

* Charger un classeur et sélectionner une feuille de calcul  
* Utiliser `DeleteRows` avec `DeleteOptions.DeleteEntireRow` pour **how to delete row** par indice  
* Enregistrer le fichier modifié en toute sécurité  
* Gestion des cas limites, astuces de performance et exemple de suppression conditionnelle  

Avec ces connaissances, vous pouvez implémenter en toute confiance la fonctionnalité **remove row by index**, automatiser le nettoyage des données et intégrer la manipulation d’Excel dans n’importe quelle application C#.

**Prochaines étapes** : explorez d’autres fonctionnalités d’Aspose.Cells telles que l’insertion de lignes, la copie de plages ou la conversion du classeur en PDF—toutes basées sur les mêmes objets `Workbook` et `Worksheet` que vous venez de maîtriser. Bon codage !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Comment supprimer une ligne Excel avec Aspose.Cells .NET : guide complet](/cells/english/net/worksheet-management/delete-excel-row-aspose-cells-net-tutorial/)
- [Aspose Cells Supprimer des lignes – Protéger la ligne d’en‑tête dans Excel](/cells/english/net/row-and-column-management/aspose-cells-delete-rows-protect-header-row-in-excel/)
- [Gestion efficace des lignes dans Excel avec Aspose.Cells pour Java : insérer et supprimer des lignes](/cells/english/java/worksheet-management/aspose-cells-java-row-operations-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}