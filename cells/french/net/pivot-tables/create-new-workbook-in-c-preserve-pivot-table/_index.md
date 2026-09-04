---
category: general
date: 2026-02-15
description: Créer un nouveau classeur en C# et copier un tableau croisé dynamique
  sans perdre sa définition. Apprenez à copier des lignes, à préserver le tableau
  croisé dynamique et à dupliquer facilement le tableau croisé dynamique.
draft: false
keywords:
- create new workbook
- copy pivot table
- preserve pivot table
- how to copy rows
- duplicate pivot table
language: fr
og_description: Créer un nouveau classeur en C# et copier un tableau croisé dynamique
  tout en préservant sa définition. Guide étape par étape pour les développeurs.
og_title: Créer un nouveau classeur en C# – Conserver le tableau croisé dynamique
tags:
- Aspose.Cells
- C#
- Excel automation
title: Créer un nouveau classeur en C# – Conserver le tableau croisé dynamique
url: /fr/net/pivot-tables/create-new-workbook-in-c-preserve-pivot-table/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un nouveau classeur en C# – Conserver le tableau croisé dynamique

Vous avez déjà eu besoin de **créer un nouveau classeur** en C# contenant une copie exacte d’un tableau croisé dynamique provenant d’un autre fichier ? Vous n’êtes pas seul. Dans de nombreux pipelines de reporting, le tableau croisé dynamique est le cœur de l’analyse, et perdre sa définition lorsqu’on déplace les données est un cauchemar.

Bonne nouvelle ? En quelques lignes de code Aspose.Cells, vous pouvez copier des lignes — y compris le tableau croisé dynamique — dans un classeur vierge et tout garder intact. Vous verrez ci‑dessous **comment copier des lignes**, **conserver les paramètres du tableau croisé dynamique**, et même **dupliquer le tableau croisé dynamique** entre fichiers sans casser les formules ou le cache.

## Ce que couvre ce tutoriel

Dans ce guide, nous allons :

1. Charger le classeur source qui possède déjà un tableau croisé dynamique.  
2. **Créer de nouveaux classeurs** pour la destination.  
3. Utiliser `CopyRows` pour transférer la plage qui contient le tableau croisé dynamique.  
4. Enregistrer le résultat tout en veillant à ce que le tableau croisé dynamique reste fonctionnel.  

Aucune documentation externe requise — juste le code, les explications, et quelques astuces pratiques que vous pouvez coller directement dans votre projet.

> **Astuce pro :** Aspose.Cells fonctionne avec .NET Core, .NET Framework, et même Xamarin, donc le même extrait s’exécute où que vous en ayez besoin.

---

![Créer un nouveau classeur avec le tableau croisé dynamique copié](/images/create-new-workbook-pivot.png "créer un nouveau classeur avec le tableau croisé dynamique copié")

## Étape 1 – Créer un nouveau classeur et charger le fichier source

La première chose que nous faisons est de **créer de nouveaux classeurs**. L’un contient les données originales, l’autre recevra la plage copiée.

```csharp
using Aspose.Cells;

// Load the source workbook that already contains a pivot table
var sourceWorkbook = new Workbook(@"C:\Data\source.xlsx");

// Create an empty workbook that will become the destination
var destinationWorkbook = new Workbook();
```

*Pourquoi c’est important :*  
`Workbook` est le point d’entrée pour toute manipulation Excel dans Aspose.Cells. En instanciant un classeur vierge, nous garantissons une ardoise propre — aucune mise en forme cachée ou feuille de calcul superflue qui pourrait interférer plus tard.

## Étape 2 – Comment copier des lignes incluant un tableau croisé dynamique

Voici le cœur du problème : **comment copier des lignes** qui encapsulent le tableau croisé dynamique sans l’aplatir. La méthode `CopyRows` fait exactement cela.

```csharp
// Copy the first 20 rows (adjust as needed) from the source to the destination
// Parameters: startRow, totalRows, targetCells, targetStartRow
sourceWorkbook.Worksheets[0].Cells.CopyRows(
    startRow: 0,
    totalRows: 20,
    targetCells: destinationWorkbook.Worksheets[0].Cells,
    targetStartRow: 0);
```

Quelques points à retenir :

* `startRow` et `totalRows` définissent le bloc qui contient le tableau croisé dynamique.  
* La méthode copie **à la fois** les données brutes et le cache du tableau, de sorte que le classeur de destination sait comment reconstruire le tableau croisé dynamique à la volée.  
* Si votre tableau commence plus bas dans la feuille, il suffit de modifier les indices — aucune autre appel d’API n’est nécessaire.

> **Question fréquente :** *Le tableau copié perdra-t-il la référence à ses données sources ?*  
> Non. Aspose.Cells intègre le cache directement dans la feuille, ainsi le tableau devient autonome dans le nouveau fichier.

## Étape 3 – Conserver le tableau croisé dynamique lors de l’enregistrement de la destination

Après la copie des lignes, le tableau croisé dynamique vit dans le classeur de destination exactement comme dans la source. L’enregistrement du fichier est simple.

```csharp
// Save the destination workbook; the pivot table remains functional
destinationWorkbook.Save(@"C:\Data\destination.xlsx");
```

Lorsque vous ouvrez `destination.xlsx` dans Excel, vous verrez le tableau croisé dynamique prêt à être actualisé. Le comportement **conserver le tableau croisé dynamique** est automatique parce que le cache a voyagé avec les lignes.

### Vérification du résultat

Ouvrez le fichier et :

1. Cliquez sur le tableau croisé dynamique.  
2. Remarquez que la liste des champs apparaît — cela signifie que le cache est intact.  
3. Essayez d’actualiser ; les données se mettent à jour sans erreur.

Si vous rencontrez une erreur *#REF!* , vérifiez que la plage copiée inclut les lignes de cache cachées (généralement juste après les données visibles).

## Étape 4 – Dupliquer le tableau croisé dynamique dans plusieurs classeurs (Optionnel)

Parfois, vous avez besoin du même tableau dans plusieurs rapports. Le schéma que nous venons d’utiliser s’adapte facilement — il suffit de répéter la copie pour chaque nouveau classeur.

```csharp
string[] targets = {
    @"C:\Reports\Q1.xlsx",
    @"C:\Reports\Q2.xlsx",
    @"C:\Reports\Q3.xlsx"
};

foreach (var path in targets)
{
    var wb = new Workbook(); // fresh workbook each loop
    sourceWorkbook.Worksheets[0].Cells.CopyRows(0, 20, wb.Worksheets[0].Cells, 0);
    wb.Save(path);
}
```

Cet extrait **duplique le tableau croisé dynamique** trois fois avec une seule boucle. Ajustez le tableau `targets` pour correspondre à votre planning de reporting.

### Cas limites à garder à l’esprit

| Situation | Points d'attention | Solution |
|-----------|---------------------|----------|
| Le tableau utilise une source de données externe | Le cache peut référencer une connexion qui n’existe pas sur la nouvelle machine | Intégrer la source de données ou recréer la connexion dans le classeur de destination |
| Tableau très volumineux ( > 100 k lignes ) | `CopyRows` peut être gourmand en mémoire | Utiliser `CopyRows` par morceaux ou envisager `Copy` avec `PasteOptions` pour limiter l’usage mémoire |
| Feuille contenant des lignes/colonnes masquées | Les lignes de cache masquées pourraient être ignorées si vous ne copiez que les lignes visibles | Toujours copier la plage exacte de lignes contenant le cache, pas seulement la zone visible |

## Exemple complet fonctionnel

En réunissant tous les éléments, voici un programme autonome que vous pouvez placer dans une application console.

```csharp
using System;
using Aspose.Cells;

namespace PivotCopyDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load source workbook (contains the original pivot)
            var sourcePath = @"C:\Data\source.xlsx";
            var sourceWorkbook = new Workbook(sourcePath);

            // 2️⃣ Prepare destination workbook
            var destinationWorkbook = new Workbook();

            // 3️⃣ Copy rows that include the pivot (adjust range as needed)
            sourceWorkbook.Worksheets[0].Cells.CopyRows(
                startRow: 0,
                totalRows: 20,
                targetCells: destinationWorkbook.Worksheets[0].Cells,
                targetStartRow: 0);

            // 4️⃣ Save – the pivot table is preserved
            var destPath = @"C:\Data\destination.xlsx";
            destinationWorkbook.Save(destPath);

            Console.WriteLine("Pivot table successfully copied!");
        }
    }
}
```

Exécutez le programme, ouvrez `destination.xlsx`, et vous verrez le même tableau croisé dynamique prêt à découper et analyser vos données. Aucun besoin de recréation manuelle.

---

## Conclusion

Nous venons de montrer comment **créer un nouveau classeur** en C# et **copier un tableau croisé dynamique** tout en conservant chaque paramètre. En utilisant `CopyRows`, vous obtenez une méthode fiable pour **conserver le tableau croisé dynamique**, répondre à la fameuse question « **comment copier des lignes** », et même **dupliquer le tableau croisé dynamique** à travers plusieurs rapports avec un minimum de code.

Prochaines étapes ? Essayez de modifier la plage copiée pour inclure des graphiques qui référencent le même tableau, ou expérimentez avec `PasteOptions` pour conserver exactement le formatage. Le même schéma fonctionne pour d’autres objets Aspose.Cells comme les tables et les plages nommées, alors n’hésitez pas à l’étendre.

Vous avez un cas particulier — peut‑être un tableau qui puise dans une base de données externe, ou un classeur hébergé dans le cloud ? Laissez un commentaire ci‑dessous, et nous le résoudrons ensemble. Bon codage !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}