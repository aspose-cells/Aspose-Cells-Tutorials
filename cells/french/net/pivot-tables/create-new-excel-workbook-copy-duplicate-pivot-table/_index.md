---
category: general
date: 2026-02-09
description: Créez un nouveau classeur Excel et apprenez à copier les tableaux croisés
  dynamiques sans effort. Ce guide montre comment dupliquer un tableau croisé dynamique
  et enregistrer le classeur en tant que nouveau.
draft: false
keywords:
- create new excel workbook
- how to copy pivot
- duplicate pivot table
- save workbook as new
- how to copy worksheet
language: fr
og_description: Créez un nouveau classeur Excel en C# et copiez instantanément un
  tableau croisé dynamique. Apprenez comment dupliquer le tableau croisé dynamique
  et enregistrer le classeur en tant que nouveau avec un exemple de code complet.
og_title: Créer un nouveau classeur Excel – Copie de tableau croisé dynamique étape
  par étape
tags:
- excel
- csharp
- aspose.cells
- automation
title: Créer un nouveau classeur Excel – Copier et dupliquer le tableau croisé dynamique
url: /fr/net/pivot-tables/create-new-excel-workbook-copy-duplicate-pivot-table/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un nouveau classeur Excel – Copier & dupliquer un tableau croisé dynamique

Vous avez déjà eu besoin de **créer un nouveau classeur Excel** qui reprend un tableau croisé dynamique complexe d’un fichier existant ? Vous n’êtes pas seul — de nombreux développeurs rencontrent ce problème lorsqu’ils automatisent des pipelines de reporting. La bonne nouvelle, c’est qu’avec quelques lignes de C# et la bibliothèque Aspose.Cells, vous pouvez **comment copier un tableau croisé dynamique** rapidement, **dupliquer le tableau croisé dynamique**, et **enregistrer le classeur comme nouveau** sans ouvrir Excel manuellement.

Dans ce guide, nous parcourrons l’ensemble du processus, du chargement du classeur source à l’enregistrement de la version dupliquée. À la fin, vous disposerez d’un extrait prêt à l’emploi que vous pourrez intégrer à n’importe quel projet .NET. Pas de blabla, juste une solution pratique que vous pouvez tester dès aujourd’hui.

## Ce que couvre ce tutoriel

* **Prérequis** – .NET 6+ (ou .NET Framework 4.6+), Visual Studio et le package NuGet Aspose.Cells for .NET.
* Code étape par étape qui **crée un nouveau classeur Excel**, copie le tableau croisé dynamique et écrit le résultat sur le disque.
* Explications du **pourquoi** de chaque ligne, pas seulement du **quoi**.
* Astuces pour gérer les cas limites comme les feuilles masquées ou les plages de données volumineuses.
* Un aperçu rapide de **comment copier une feuille** si vous avez besoin de toute la feuille au lieu du seul tableau croisé dynamique.

Prêt ? C’est parti.

![illustration de création d’un nouveau classeur excel](image.png "Diagramme montrant le classeur source, la copie du tableau croisé dynamique et le classeur de destination")

## Étape 1 : Configurer le projet et installer Aspose.Cells

Avant de pouvoir **créer un nouveau classeur Excel**, il nous faut un projet qui référence la bonne bibliothèque.

```csharp
// Install the Aspose.Cells package via NuGet:
//   dotnet add package Aspose.Cells
using Aspose.Cells;   // Provides Workbook, Worksheet, Range, etc.
using System;        // For basic .NET types
```

*Pourquoi c’est important :* Aspose.Cells fonctionne entièrement en mémoire, vous n’avez donc jamais besoin de lancer Excel sur le serveur. Il préserve également les informations du cache du tableau croisé dynamique, ce qui est essentiel pour une vraie **duplication du tableau croisé dynamique**.

> **Astuce pro :** Si vous ciblez .NET Core, assurez‑vous que l’identifiant d’exécution (RID) de votre projet correspond à la plateforme sur laquelle vous déploierez ; sinon vous pourriez rencontrer des erreurs de chargement de bibliothèques natives.

## Étape 2 : Charger le classeur source contenant le tableau croisé dynamique

Nous allons maintenant **comment copier un tableau croisé dynamique** depuis un fichier existant. Le classeur source peut se trouver n’importe où sur le disque, dans un flux, ou même sous forme de tableau d’octets.

```csharp
// Step 2: Load the source workbook that contains the pivot table
string sourcePath = @"C:\Reports\source.xlsx";
Workbook sourceWorkbook = new Workbook(sourcePath);

// Grab the first worksheet (adjust the index if your pivot lives elsewhere)
Worksheet sourceSheet = sourceWorkbook.Worksheets[0];

// Define the range that encloses the pivot table – A1:D20 in this example
Range sourceRange = sourceSheet.Cells.CreateRange("A1:D20");
```

*Pourquoi nous choisissons une plage :* Un tableau croisé dynamique vit à l’intérieur d’une plage de cellules ordinaire, mais il possède également des données de cache cachées attachées à la feuille. En copiant la plage **y compris le tableau croisé dynamique**, Aspose.Cells s’assure que le cache l’accompagne, vous offrant ainsi un **tableau croisé dynamique dupliqué** fonctionnel dans le fichier de destination.

## Étape 3 : Créer un nouveau classeur Excel pour recevoir les données copiées

C’est ici que nous **créons un nouveau classeur Excel** qui contiendra le tableau croisé dynamique dupliqué.

```csharp
// Step 3: Create a fresh workbook (empty) for the destination
Workbook destinationWorkbook = new Workbook(); // Starts with a default empty sheet
Worksheet destinationSheet = destinationWorkbook.Worksheets[0];

// Destination starts at A1 – you could offset if you need space for other data
Range destinationRange = destinationSheet.Cells.CreateRange("A1");
```

> **Pourquoi un classeur vierge ?** Partir d’une feuille blanche garantit qu’aucun formatage résiduel ou objet caché n’interfère avec le tableau copié. Cela rend également le fichier final plus léger, ce qui est pratique pour les pièces jointes d’e‑mail automatisées.

## Étape 4 : Copier la plage du tableau croisé dynamique vers le nouveau classeur

Nous effectuons maintenant l’opération réelle de **comment copier un tableau croisé dynamique**.

```csharp
// Step 4: Copy the range (including the pivot) from source to destination
sourceRange.Copy(destinationRange);
```

Cette ligne unique fait le gros du travail :

* Les valeurs de cellules, formules et formats sont transférés.
* Le cache du tableau croisé dynamique est dupliqué, de sorte que le nouveau tableau reste pleinement fonctionnel.
* Toutes les références relatives à l’intérieur du tableau s’ajustent automatiquement à la nouvelle position.

### Gestion des cas limites

* **Feuilles masquées :** Si la feuille source est masquée, le tableau se copie tout de même, mais vous voudrez peut‑être rendre la feuille de destination visible pour l’utilisateur :
  ```csharp
  destinationSheet.IsVisible = true;
  ```
* **Ensembles de données volumineux :** Pour des plages dépassant quelques milliers de lignes, envisagez d’utiliser `CopyTo` avec `CopyOptions` afin de diffuser l’opération et réduire la pression mémoire.

## Étape 5 : Enregistrer le classeur de destination comme nouveau fichier

Enfin, nous **enregistrons le classeur comme nouveau** et vérifions le résultat.

```csharp
// Step 5: Save the destination workbook with the duplicated pivot table
string destPath = @"C:\Reports\copied.xlsx";
destinationWorkbook.Save(destPath, SaveFormat.Xlsx);

// Quick verification – open the file manually or read a cell value
Console.WriteLine($"Workbook saved to {destPath}");
```

Si vous ouvrez `copied.xlsx`, vous verrez une réplique exacte du tableau croisé dynamique original, prête à être manipulée ou distribuée.

### Optionnel : Comment copier une feuille au lieu du seul tableau croisé dynamique

Parfois vous avez besoin de toute la feuille, pas seulement du tableau. La même API rend cela trivial :

```csharp
// Copy the whole worksheet (including all charts, tables, etc.)
sourceSheet.CopyTo(destinationWorkbook, 0); // Inserts at index 0
destinationWorkbook.Save(@"C:\Reports\full_copy.xlsx");
```

Cela répond à la requête **comment copier une feuille** et peut être utile lorsque vous devez conserver des paramètres supplémentaires au niveau de la feuille.

## Exemple complet fonctionnel

En assemblant le tout, voici une application console autonome que vous pouvez compiler et exécuter :

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Load source workbook
        string sourcePath = @"C:\Reports\source.xlsx";
        Workbook sourceWorkbook = new Workbook(sourcePath);
        Worksheet sourceSheet = sourceWorkbook.Worksheets[0];
        Range sourceRange = sourceSheet.Cells.CreateRange("A1:D20");

        // 2️⃣ Create destination workbook
        Workbook destinationWorkbook = new Workbook();
        Worksheet destinationSheet = destinationWorkbook.Worksheets[0];
        Range destinationRange = destinationSheet.Cells.CreateRange("A1");

        // 3️⃣ Copy the pivot (range)
        sourceRange.Copy(destinationRange);

        // 4️⃣ Save as new file
        string destPath = @"C:\Reports\copied.xlsx";
        destinationWorkbook.Save(destPath, SaveFormat.Xlsx);

        Console.WriteLine($"✅ Successfully created new Excel workbook with duplicated pivot table at {destPath}");
    }
}
```

**Sortie attendue :** La console affiche un message de succès, et `copied.xlsx` apparaît dans `C:\Reports` avec un tableau croisé dynamique fonctionnel identique à celui de `source.xlsx`.

## Questions fréquentes & pièges

* **Les formules du tableau croisé dynamique se cassent‑elles ?** Non—le cache du tableau voyage avec la plage, toutes les champs calculés restent intacts.
* **Et si le tableau source utilise des connexions de données externes ?** Ces connexions ne sont **pas** copiées. Vous devrez les recréer dans le classeur de destination ou convertir le tableau en tableau statique d’abord.
* **Puis‑je copier plusieurs tableaux croisés dynamiques en même temps ?** Absolument—définissez simplement une plage plus grande qui englobe tous les tableaux, ou parcourez chaque objet `PivotTable` dans `sourceSheet.PivotTables` et copiez‑les individuellement.
* **Dois‑je disposer des objets `Workbook` ?** Ils implémentent `IDisposable`, il est donc recommandé de les encapsuler dans des instructions `using`, surtout dans des services à haut débit.

## Conclusion

Vous savez maintenant **comment créer un nouveau classeur Excel**, copier un tableau croisé dynamique, **dupliquer le tableau croisé dynamique**, et **enregistrer le classeur comme nouveau** en utilisant C# et Aspose.Cells. Les étapes sont simples : charger, créer, copier et enregistrer. Avec l’extrait optionnel **comment copier une feuille**, vous avez également une solution de secours pour la duplication complète d’une feuille.

Prochaines étapes possibles :

* Ajouter un formatage personnalisé au tableau dupliqué.
* Rafraîchir le cache du tableau programmatique après des modifications de données.
* Exporter le classeur en PDF ou CSV pour les systèmes en aval.

Testez, ajustez la plage, et laissez l’automatisation prendre en charge le travail fastidieux de votre flux de reporting. Bon codage !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}