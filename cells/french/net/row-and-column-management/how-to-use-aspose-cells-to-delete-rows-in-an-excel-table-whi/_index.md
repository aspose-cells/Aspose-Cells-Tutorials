---
category: general
date: 2026-10-07
description: Apprenez comment Aspose.Cells supprime des lignes d’un tableau Excel,
  supprime les lignes sauf l’en‑tête, et gère la suppression de lignes d’un tableau
  protégé avec un code C# propre.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- aspose cells delete rows
- delete rows excel table
- excel table row deletion
- protect excel table rows
- remove rows except header
language: fr
lastmod: 2026-10-07
og_description: Aspose.Cells supprime des lignes d’un tableau Excel tout en conservant
  l’en‑tête. Ce guide présente la solution complète en C#, en gérant les tableaux
  protégés et les cas limites courants.
og_image_alt: Aspose.Cells delete rows example showing code and Excel screenshot
og_title: Aspose.Cells supprimer des lignes – supprimer toutes les lignes sauf l’en‑tête
  en C#
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Learn how Aspose.Cells delete rows from an Excel table, remove rows
    except header, and handle protected table row deletion with clean C# code.
  headline: How to use Aspose.Cells to delete rows in an Excel table while keeping
    the header
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Comment utiliser Aspose.Cells pour supprimer des lignes dans un tableau Excel
  tout en conservant l’en‑tête
url: /fr/net/row-and-column-management/how-to-use-aspose-cells-to-delete-rows-in-an-excel-table-whi/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment utiliser Aspose.Cells pour supprimer des lignes dans un tableau Excel tout en conservant l'en-tête

Si vous devez **aspose cells delete rows** d'un tableau tout en conservant la ligne d'en-tête, ce guide présente une solution complète et exécutable. Vous verrez pourquoi un appel direct à `ListObject.DeleteRows` échoue lorsque le tableau est protégé, et comment contourner cette limitation sans compromettre l'intégrité des données.

Le tutoriel couvre :

* Chargement d'un classeur contenant un tableau protégé.  
* Détection et suppression temporaire de la protection du tableau.  
* Suppression de chaque ligne de données tout en préservant l'en-tête.  
* Restauration de l'état de protection d'origine.  

À la fin de l'article, vous pourrez effectuer de manière fiable des opérations de **delete rows excel table** dans n'importe quel projet Aspose.Cells.

## Prérequis

* .NET 6.0 ou ultérieur (le code fonctionne également avec .NET Framework 4.7.2+).  
* Aspose.Cells pour .NET 23.9 ou plus récent.  
* Bonne connaissance de C# et des tableaux Excel (également appelés ListObjects).  

Aucun package NuGet supplémentaire n'est requis au-delà d'Aspose.Cells.

## Étape 1 : Configurer le projet et importer les espaces de noms

Créez une nouvelle application console ou ajoutez le code suivant à un projet existant. Importez les espaces de noms Aspose.Cells afin que le compilateur puisse résoudre `Workbook`, `Worksheet` et `ListObject`.

```csharp
using System;
using Aspose.Cells;

namespace AsposeCellsTableRowDeletion
{
    class Program
    {
        static void Main()
        {
            // The full solution starts in Step 2.
        }
    }
}
```

*Pourquoi cette étape est importante* – L'importation des espaces de noms corrects évite les erreurs de type ambiguës et rend le reste du code plus clair.

## Étape 2 : Charger le classeur et localiser le tableau cible

Remplacez `"YOUR_DIRECTORY/TableProtection.xlsx"` par le chemin vers votre fichier Excel. L'exemple suppose que le tableau que vous souhaitez modifier s'appelle **Orders**.

```csharp
// Load the workbook that contains the protected table
Workbook workbook = new Workbook("YOUR_DIRECTORY/TableProtection.xlsx");

// Get the first worksheet (index 0) and the ListObject named "Orders"
Worksheet worksheet = workbook.Worksheets[0];
ListObject ordersTable = worksheet.ListObjects["Orders"];
```

*Pourquoi cette étape est importante* – Accéder au `ListObject` vous donne une poignée directe sur le tableau, ce qui est nécessaire pour toute opération de **excel table row deletion**.

## Étape 3 : Vérifier si le tableau est protégé

Aspose.Cells bloque la suppression partielle d'un tableau lorsque celui-ci est protégé. Tenter `ordersTable.DeleteRows` dans cet état génère une exception. Détectez d'abord l'état de protection.

```csharp
bool wasProtected = ordersTable.IsProtected;
Console.WriteLine($"Table protection status: {(wasProtected ? "protected" : "unprotected")}");
```

*Pourquoi cette étape est importante* – Connaître l'état de protection vous permet de décider s'il faut lever temporairement la protection, en veillant à ce que la règle **protect excel table rows** soit respectée après l'opération.

## Étape 4 : Déprotéger temporairement le tableau (si nécessaire)

Si le tableau est protégé, utilisez `Unprotect` avec le mot de passe (le cas échéant). Pour les tableaux sans mot de passe, appelez simplement `Unprotect()`.

```csharp
if (wasProtected)
{
    // Provide the password if the table was protected with one; otherwise, pass null.
    ordersTable.Unprotect(null);
    Console.WriteLine("Table temporarily unprotected.");
}
```

*Pourquoi cette étape est importante* – Déprotéger le tableau permet à Aspose.Cells d'exécuter **aspose cells delete rows** sans lever d'exception, tout en vous permettant de restaurer la protection ultérieurement.

## Étape 5 : Supprimer toutes les lignes sauf l'en-tête

L'en-tête occupe la première ligne du tableau (`RowCount` inclut l'en-tête). Supprimer à partir de l'index 1 supprime toutes les lignes de données.

```csharp
int dataRows = ordersTable.RowCount - 1; // Exclude the header row
if (dataRows > 0)
{
    ordersTable.DeleteRows(1, dataRows);
    Console.WriteLine($"{dataRows} data rows removed, header preserved.");
}
else
{
    Console.WriteLine("Table contains only the header; nothing to delete.");
}
```

*Pourquoi cette étape est importante* – Ce code réalise la fonctionnalité principale de **remove rows except header** tout en évitant l'exception qui survient lors de suppressions partielles sur des tableaux protégés.

## Étape 6 : Réappliquer la protection (si elle était initialement définie)

Après la suppression des lignes, restaurez l'état de protection d'origine afin que le classeur se comporte exactement comme avant.

```csharp
if (wasProtected)
{
    // Re‑apply protection with the same password (null if none was used)
    ordersTable.Protect(null);
    Console.WriteLine("Table protection restored.");
}
```

*Pourquoi cette étape est importante* – La restauration de la protection respecte l'exigence **protect excel table rows** et maintient le classeur sécurisé pour les utilisateurs en aval.

## Étape 7 : Enregistrer le classeur modifié

Choisissez un nouveau nom de fichier pour éviter d'écraser le fichier original, sauf si l'écrasement est intentionnel.

```csharp
string outputPath = "YOUR_DIRECTORY/TableProtection_Modified.xlsx";
workbook.Save(outputPath);
Console.WriteLine($"Modified workbook saved to: {outputPath}");
```

*Pourquoi cette étape est importante* – L'enregistrement finalise l'opération de **excel table row deletion** et fournit un résultat tangible que vous pouvez ouvrir dans Excel pour vérifier.

## Exemple complet fonctionnel

Assembler toutes les étapes donne un programme autonome que vous pouvez copier, coller et exécuter.

```csharp
using System;
using Aspose.Cells;

namespace AsposeCellsTableRowDeletion
{
    class Program
    {
        static void Main()
        {
            // 1. Load workbook
            Workbook workbook = new Workbook("YOUR_DIRECTORY/TableProtection.xlsx");
            Worksheet worksheet = workbook.Worksheets[0];
            ListObject ordersTable = worksheet.ListObjects["Orders"];

            // 2. Remember protection state
            bool wasProtected = ordersTable.IsProtected;
            Console.WriteLine($"Table protection status: {(wasProtected ? "protected" : "unprotected")}");

            // 3. Unprotect if needed
            if (wasProtected)
            {
                ordersTable.Unprotect(null); // use password if applicable
                Console.WriteLine("Table temporarily unprotected.");
            }

            // 4. Delete all rows except header
            int dataRows = ordersTable.RowCount - 1;
            if (dataRows > 0)
            {
                ordersTable.DeleteRows(1, dataRows);
                Console.WriteLine($"{dataRows} data rows removed, header preserved.");
            }
            else
            {
                Console.WriteLine("Table contains only the header; nothing to delete.");
            }

            // 5. Restore protection
            if (wasProtected)
            {
                ordersTable.Protect(null); // re‑apply with original password if any
                Console.WriteLine("Table protection restored.");
            }

            // 6. Save the workbook
            string outputPath = "YOUR_DIRECTORY/TableProtection_Modified.xlsx";
            workbook.Save(outputPath);
            Console.WriteLine($"Modified workbook saved to: {outputPath}");
        }
    }
}
```

### Résultat attendu

```
Table protection status: protected
Table temporarily unprotected.
5 data rows removed, header preserved.
Table protection restored.
Modified workbook saved to: YOUR_DIRECTORY/TableProtection_Modified.xlsx
```

Ouvrez `TableProtection_Modified.xlsx` dans Excel. Vous verrez le tableau **Orders** avec uniquement la ligne d'en-tête restante ; toutes les lignes de données ont été supprimées.

## Gestion des variations courantes et des cas limites

| Situation | Ajustement recommandé | Raison |
|-----------|-----------------------|--------|
| Le tableau utilise un mot de passe | Passez le mot de passe à `Unprotect` et `Protect` | Garantit le même niveau de sécurité après l'opération |
| Le tableau n'a aucune ligne de données | Ignorez l'appel à `DeleteRows` | Évite une `ArgumentOutOfRangeException` |
| Plusieurs tableaux nécessitent un nettoyage | Bouclez sur `worksheet.ListObjects` et appliquez la même logique | Étend le modèle **delete rows excel table** à toute la feuille |
| Vous voulez conserver l'en-tête et la première ligne de données | Changez `DeleteRows(2, dataRows‑1)` | Commence la suppression après la deuxième ligne, en préservant la première ligne de données |

Ces variations démontrent une gestion robuste de **excel table row deletion** et renforcent pourquoi l'approche présentée est la recommandée.

## Astuces professionnelles

* **Traitement par lots** – Si vous devez supprimer des lignes de nombreux classeurs, encapsulez la logique dans une méthode réutilisable qui accepte les paramètres `Workbook` et `tableName`.
* **Performance** – Supprimer des lignes en un seul appel (`DeleteRows`) est plus rapide que de supprimer les lignes une par une car Aspose.Cells met à jour les structures de données internes une seule fois.
* **Sécurité** – Travaillez toujours sur une copie du fichier original ou conservez une sauvegarde avant d'appliquer des suppressions, surtout lorsque **protect excel table rows** est impliqué.

## Conclusion

Vous disposez maintenant d'une solution complète, prête pour la production, pour **aspose cells delete rows** tout en préservant l'en-tête d'un tableau Excel. Le guide a couvert le chargement du classeur, la gestion des tableaux protégés, l'exécution de l'opération **remove rows except header**, et la restauration de la protection. Appliquez le même schéma à tout scénario de **excel table row deletion**, et adaptez le code aux exigences supplémentaires telles que les tableaux protégés par mot de passe ou le traitement par lots.

---

*Prochaines étapes* – Explorez des sujets connexes tels que **delete rows excel table** avec filtres, la fusion de cellules après suppression de lignes, ou l'utilisation d'Aspose.Cells pour copier des tableaux entre classeurs. Chacun de ces sujets s'appuie sur les concepts de base démontrés ici et approfondit votre maîtrise de l'automatisation Excel avec Aspose.Cells.

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités supplémentaires de l'API et explorer des approches d'implémentation alternatives dans vos propres projets.

- [Aspose Cells Delete Rows – Protéger la ligne d'en‑tête dans Excel](/cells/english/net/row-and-column-management/aspose-cells-delete-rows-protect-header-row-in-excel/)
- [Comment insérer et supprimer des lignes dans Excel avec Aspose.Cells pour .NET : guide complet](/cells/english/net/data-manipulation/aspose-cells-net-insert-delete-excel-rows/)
- [Comment supprimer les lignes vides dans Excel en utilisant Aspose.Cells .NET pour le nettoyage de données](/cells/english/net/data-manipulation/delete-blank-rows-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}