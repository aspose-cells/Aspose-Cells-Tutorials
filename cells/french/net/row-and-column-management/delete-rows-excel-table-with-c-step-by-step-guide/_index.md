---
category: general
date: 2026-02-28
description: Supprimez rapidement des lignes d’un tableau Excel en C#. Apprenez à
  ajouter une plage nommée dans Excel, à accéder à une feuille de calcul par son nom
  et à éviter les erreurs de nom en double.
draft: false
keywords:
- delete rows excel table
- add named range excel
- access worksheet by name
- how to add defined name
- named range on another sheet
language: fr
og_description: Supprimer des lignes d'un tableau Excel en C#. Ce tutoriel montre
  également comment ajouter une plage nommée dans Excel et accéder à une feuille de
  calcul par son nom.
og_title: Supprimer des lignes d'un tableau Excel avec C# – Guide complet
tags:
- C#
- Excel
- DevExpress Spreadsheet
title: Supprimer des lignes d’un tableau Excel avec C# – Guide étape par étape
url: /fr/net/row-and-column-management/delete-rows-excel-table-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Supprimer des lignes d'un tableau Excel avec C# – Tutoriel complet de programmation

Vous avez déjà eu besoin de **supprimer des lignes d'un tableau Excel** d'un classeur mais vous ne saviez pas quel appel d'API utiliser ? Vous n'êtes pas le seul—la plupart des développeurs rencontrent le même problème lorsqu'ils essaient pour la première fois de réduire un tableau par programme.  

Dans ce guide, nous parcourrons un exemple complet et exécutable qui non seulement supprime des lignes d'un tableau Excel, mais montre également **comment ajouter un nom défini** (alias une *plage nommée*), comment **accéder à une feuille de calcul par son nom**, et pourquoi l'ajout d'un nom en double sur une autre feuille génère une `InvalidOperationException`.  

À la fin de l'article, vous serez capable de :

* Récupérer une feuille de calcul en utilisant le nom de son onglet.  
* Supprimer en toute sécurité les lignes de données du premier tableau de cette feuille.  
* Créer une plage nommée qui pointe vers une adresse spécifique.  
* Comprendre les pièges des noms en double entre les feuilles.

Aucune documentation externe requise—tout ce dont vous avez besoin se trouve ici.

---

## Ce dont vous aurez besoin

* **DevExpress Spreadsheet** (ou toute bibliothèque exposant les objets `Workbook`, `Worksheet`, `ListObject` et `Names`).  
* Un projet .NET ciblant **.NET 6** ou une version ultérieure (le code compile également avec .NET Framework 4.8).  
* Une connaissance de base du C#—si vous savez écrire une boucle `foreach`, vous êtes prêt.

> **Astuce :** Si vous utilisez l'édition communautaire gratuite de DevExpress, les API utilisées ci‑dessous sont identiques à la version commerciale.

---

## Étape 1 – Accéder à une feuille de calcul par son nom

La première chose à faire est de localiser la feuille contenant le tableau que vous souhaitez modifier.  
La plupart des développeurs utilisent `Worksheets[0]` par habitude, mais cela lie votre code à l'ordre des feuilles et se casse dès que quelqu'un renomme un onglet.

```csharp
using DevExpress.Spreadsheet;

// Assume 'workbook' is an already‑loaded Workbook instance
Worksheet worksheet = workbook.Worksheets["Sheet1"];   // <-- access worksheet by name
```

*Pourquoi c'est important :* En utilisant le **nom** de la feuille au lieu de son indice, vous évitez les modifications accidentelles de la mauvaise feuille lorsque le classeur change.  

Si le nom fourni n'existe pas, la bibliothèque lève une `KeyNotFoundException`, que vous pouvez intercepter pour afficher un message d'erreur convivial.

---

## Étape 2 – Supprimer des lignes d'un tableau Excel (la méthode sûre)

Maintenant que vous avez la bonne feuille, supprimons les lignes de données du premier tableau.  
Une erreur fréquente consiste à appeler `DeleteRows(1, rowCount‑1)`. Depuis **DevExpress 22.2**, cette surcharge est **interdite** et génère une `InvalidOperationException`. La bibliothèque attend que vous supprimiez les lignes **dans la plage de données du tableau**, et non la ligne d’en‑tête.

```csharp
// Grab the first table (ListObject) on the sheet
var table = worksheet.ListObjects[0];

// Calculate how many data rows we actually have (excluding the header)
int dataRowCount = table.DataRange.RowCount;

// Delete only the data rows – keep the header intact
if (dataRowCount > 0)
{
    // DeleteRows(startRow, rowCount) – startRow is zero‑based within the table
    table.DeleteRows(0, dataRowCount);
}
```

> **Et si le tableau est vide ?** La condition `if` empêche un appel avec `rowCount = 0`, ce qui aurait autrement levé une exception.

### Aperçu visuel  

![exemple de suppression de lignes d'un tableau Excel](image.png "Capture d'écran montrant la suppression de lignes d'un tableau Excel")  

*Texte alternatif : exemple de suppression de lignes d'un tableau Excel en code C#*

---

## Étape 3 – Comment ajouter un nom défini (Créer une plage nommée)

Après avoir nettoyé le tableau, vous pourriez vouloir faire référence à une plage spécifique plus tard—par exemple pour un graphique ou une liste de validation de données. C’est là que **add named range excel** intervient.

```csharp
// Define a name that points to A1:C5 on Sheet1
workbook.Names.Add("MyTable", "Sheet1!$A$1:$C$5");

// Verify that the name exists
Name definedName = workbook.Names["MyTable"];
Console.WriteLine($"Defined name '{definedName.Name}' points to {definedName.RefersTo}");
```

La méthode `Names.Add` prend deux paramètres : l’identifiant et l’adresse au format A1.  
Comme nous avons utilisé **access worksheet by name** précédemment, la chaîne d’adresse peut référencer en toute sécurité n’importe quelle feuille sans se soucier des changements d’indice.

---

## Étape 4 – Plage nommée sur une autre feuille – Éviter les erreurs de nom en double

Vous pourriez penser que vous pouvez réutiliser le même identifiant sur une autre feuille, comme ceci :

```csharp
// Attempt to add the same name on Sheet2 – this will throw
workbook.Names.Add("MyTable", "Sheet2!$A$1:$C$5");
```

Malheureusement, la portée des noms dans Excel est **à l’échelle du classeur**, pas par feuille. L’appel ci‑dessus déclenche une `InvalidOperationException` avec le message *« Un nom avec le même identifiant existe déjà. »*  

### Comment contourner le problème

1. **Choisissez un nom unique** (`MyTable_Sheet2`).  
2. **Supprimez le nom existant** avant de le ré‑ajouter (uniquement si vous souhaitez réellement le remplacer).  

```csharp
// Option A – use a unique name
workbook.Names.Add("MyTable_Sheet2", "Sheet2!$A$1:$C$5");

// Option B – replace the existing name (use with caution)
if (workbook.Names.Contains("MyTable"))
    workbook.Names.Remove("MyTable");

workbook.Names.Add("MyTable", "Sheet2!$A$1:$C$5");
```

---

## Exemple complet et exécutable

En assemblant le tout, voici une application console autonome que vous pouvez placer dans Visual Studio et exécuter sur un fichier d’exemple `sample.xlsx`.

```csharp
using System;
using DevExpress.Spreadsheet;

class Program
{
    static void Main()
    {
        // Load an existing workbook (replace with your file path)
        Workbook workbook = new Workbook();
        workbook.LoadDocument("sample.xlsx");

        // -------------------------------------------------
        // Step 1 – Access the worksheet by its tab name
        // -------------------------------------------------
        Worksheet worksheet = workbook.Worksheets["Sheet1"]; // primary sheet

        // -------------------------------------------------
        // Step 2 – Delete rows excel table (safe method)
        // -------------------------------------------------
        var table = worksheet.ListObjects[0];
        int dataRows = table.DataRange.RowCount;
        if (dataRows > 0)
            table.DeleteRows(0, dataRows); // removes only data rows

        // -------------------------------------------------
        // Step 3 – Add a defined name (named range) on Sheet1
        // -------------------------------------------------
        workbook.Names.Add("MyTable", "Sheet1!$A$1:$C$5");

        // -------------------------------------------------
        // Step 4 – Demonstrate duplicate‑name handling
        // -------------------------------------------------
        try
        {
            workbook.Names.Add("MyTable", "Sheet2!$A$1:$C$5");
        }
        catch (InvalidOperationException ex)
        {
            Console.WriteLine("Duplicate name error: " + ex.Message);
            // Use a unique identifier instead
            workbook.Names.Add("MyTable_Sheet2", "Sheet2!$A$1:$C$5");
        }

        // Save the modified workbook
        workbook.SaveDocument("sample_modified.xlsx");
        Console.WriteLine("Workbook updated successfully.");
    }
}
```

**Résultat attendu**

* Toutes les lignes de données du premier tableau sur **Sheet1** disparaissent, ne laissant que la ligne d’en‑tête.  
* Le nom **MyTable** pointe maintenant vers `Sheet1!$A$1:$C$5`.  
* Un second nom **MyTable_Sheet2** référence en toute sécurité une plage sur **Sheet2** sans lever d’exception.

---

## Questions fréquentes & cas limites

| Question | Réponse |
|----------|--------|
| *Et si le classeur contient plusieurs tableaux ?* | Récupérez le `ListObject` correct par indice (`worksheet.ListObjects[1]`) ou par nom (`worksheet.ListObjects["MyTable"]`). |
| *Puis-je supprimer des lignes d’un tableau qui s’étend sur plusieurs feuilles ?* | Non—les tableaux sont confinés à une seule feuille. Vous devez répéter la logique de suppression pour chaque feuille. |
| *Existe‑t‑il un moyen de supprimer uniquement un sous‑ensemble de lignes ?* | Oui—utilisez `table.DeleteRows(startRow, count)` où `startRow` est indexé à zéro dans la zone de données du tableau. |
| *Les plages nommées survivent‑elles après l’enregistrement ?* | Absolument. Une fois que vous appelez `SaveDocument`, les noms font partie du XML du classeur. |
| *Comment lister tous les noms définis dans le classeur ?* | Itérez `foreach (var name in workbook.Names) Console.WriteLine(name.Name);`. |

---

## Conclusion

Nous avons couvert **delete rows excel table** avec C#, démontré **add named range excel**, et montré la bonne façon d’**access worksheet by name** tout en évitant la redoutable exception de nom en double.  

La solution complète se trouve dans l’extrait de code ci‑dessus—copiez, collez et exécutez‑la sur vos propres fichiers. À partir de là, vous pouvez étendre la logique pour gérer plusieurs tableaux, des calculs de plages dynamiques, ou même l’intégrer à une interface utilisateur.

**Prochaines étapes** que vous pourriez explorer :

* Utilisez **named range on another sheet** pour alimenter les séries de graphiques.  
* Combinez la logique de suppression avec **ExcelDataReader** pour importer des données avant de les nettoyer.  
* Automatisez les mises à jour en masse sur des dizaines de classeurs en utilisant une simple boucle `foreach (var file in Directory.GetFiles(...))`.

Vous avez d’autres questions sur l’automatisation d’Excel en C# ? Laissez un commentaire, et continuons la discussion. Bon codage !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}