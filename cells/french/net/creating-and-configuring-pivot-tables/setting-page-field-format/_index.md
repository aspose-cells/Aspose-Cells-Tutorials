---
title: Définition du format des champs de page par programmation dans .NET
linktitle: Définition du format des champs de page par programmation dans .NET
second_title: API de traitement Excel Aspose.Cells .NET
description: Découvrez comment définir les formats des champs de page dans les tableaux croisés dynamiques par programmation à l'aide d'Aspose.Cells pour .NET. Suivez notre didacticiel étape par étape pour une gestion transparente des données.
weight: 21
url: /fr/net/creating-and-configuring-pivot-tables/setting-page-field-format/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Définition du format des champs de page par programmation dans .NET

## Introduction
Créer et manipuler des fichiers Excel via du code peut être très utile, surtout lorsque vous devez analyser de grands ensembles de données. L'un des outils fantastiques de votre arsenal est Aspose.Cells pour .NET, qui vous permet d'interagir par programmation avec des fichiers Excel et de créer des structures de rapport complexes. Dans ce didacticiel, nous allons découvrir comment configurer des formats de champ de page dans un tableau croisé dynamique à l'aide de cette puissante bibliothèque. Que vous soyez un développeur expérimenté ou un débutant, à la fin de ce guide, vous aurez une bonne compréhension de la manière d'utiliser les tableaux croisés dynamiques et leurs différents paramètres dans .NET.
## Prérequis
Avant de nous lancer tête baissée dans le codage, assurons-nous que tout est correctement configuré. Vous aurez besoin des éléments suivants :
- Visual Studio : un environnement de travail dans lequel vous pouvez écrire et exécuter votre code .NET.
-  Aspose.Cells : Vous pouvez télécharger la bibliothèque[ici](https://releases.aspose.com/cells/net/).
- Connaissances de base de C# : la familiarité avec la programmation C# vous aidera à mieux comprendre les extraits de code.
-  Fichier Excel : Ayez un fichier Excel prêt (comme`Book1.xls`) contenant des données adaptées à la création de tableaux croisés dynamiques. 
 Si vous ne l'avez pas déjà fait, obtenez votre essai gratuit d'Aspose.Cells[ici](https://releases.aspose.com/).
## Paquets d'importation
Pour commencer, vous devrez importer les bons packages dans votre projet. Commencez par ajouter des références à la bibliothèque Aspose.Cells dans votre projet C#. Voici comment procéder :
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
using Aspose.Cells.Pivot;
```
Cela rassemblera toutes les classes et méthodes nécessaires pour manipuler les fichiers Excel à l'aide d'Aspose.Cells.
## Étape 1 : Configurez votre espace de travail
Commencez par définir votre répertoire de travail dans lequel seront stockés vos fichiers Excel. Vous pouvez par exemple déclarer une variable comme ceci :
```csharp
string dataDir = "Your Document Directory";
```
## Chargement du classeur
Ensuite, nous devons charger notre modèle Excel. Il s’agit d’une étape essentielle car elle établit le contexte de nos opérations :
```csharp
Workbook workbook = new Workbook(dataDir + "Book1.xls");
```
Cette ligne charge le classeur existant à partir du répertoire spécifié.
## Étape 2 : Accéder à la feuille de travail
Une fois votre classeur chargé, il est temps d'accéder à la feuille de calcul qui contient le tableau croisé dynamique ou les données que vous souhaitez analyser. Voici comment procéder :
```csharp
Worksheet worksheet = workbook.Worksheets[0];
```
Cela récupère la première feuille de calcul du classeur chargé. Vous pouvez facilement modifier l'index si vous travaillez avec plusieurs feuilles.
## Étape 3 : Accéder au tableau croisé dynamique
 Continuons, accédons au tableau croisé dynamique dans notre feuille de calcul choisie. Si vous utilisez un seul tableau croisé dynamique, vous pouvez définir son index sur`0`:
```csharp
int pivotindex = 0;
// Accéder au tableau croisé dynamique
PivotTable pivotTable = worksheet.PivotTables[pivotindex];
```
Cet extrait de code sélectionne le premier tableau croisé dynamique de la feuille de calcul. 
## Étape 4 : Configuration du tableau croisé dynamique
Vient maintenant la partie passionnante ! Configurons le tableau croisé dynamique pour afficher les totaux généraux des lignes :
```csharp
pivotTable.RowGrand = true;
```
Cette ligne garantit que votre rapport affichera les totaux généraux qui peuvent constituer un résumé utile pour l'analyse des données.
## Étape 5 : Accéder aux champs de ligne et les configurer
Ensuite, nous devons accéder aux champs de ligne du tableau croisé dynamique :
```csharp
Aspose.Cells.Pivot.PivotFieldCollection pivotFields = pivotTable.RowFields;
```
Cette collection nous permet de manipuler les champs selon les besoins.
## Configurer le champ de la première ligne
Vous souhaitez définir des types de sous-totaux spécifiques ? Accédons au premier champ de notre collection et configurons-le :
```csharp
Aspose.Cells.Pivot.PivotField pivotField = pivotFields[0];
// Définition des sous-totaux.
pivotField.SetSubtotals(Aspose.Cells.Pivot.PivotFieldSubtotalType.Sum, true);
pivotField.SetSubtotals(Aspose.Cells.Pivot.PivotFieldSubtotalType.Count, true);
```
 En activant`Sum` et`Count` sous-totaux, nous pouvons rapidement résumer les données dans notre rapport.
## Étape 6 : Définition des options de tri automatique
Ensuite, mettons en œuvre un tri intelligent. De cette façon, votre tableau croisé dynamique organisera les données dans un ordre significatif :
```csharp
// Définition des options de tri automatique.
pivotField.IsAutoSort = true;
pivotField.IsAscendSort = true;
pivotField.AutoSortField = -5; // Utilisation d'un champ de tri prédéfini.
```
Cet extrait de code permet le tri automatique et spécifie l'ordre croissant. 
## Étape 7 : Définition des options d'affichage automatique
Souhaitez-vous filtrer davantage vos données ? L'option Affichage automatique est utile pour afficher des points de données spécifiques dans des conditions définies :
```csharp
// Définition des options d'affichage automatique.
pivotField.IsAutoShow = true;
pivotField.IsAscendShow = false;
pivotField.AutoShowField = 0; // Spécifiez le champ à afficher automatiquement.
```
Cela garantit que votre tableau croisé dynamique affiche uniquement les données pertinentes, améliorant ainsi la clarté et la concentration.
## Étape 8 : Sauvegarder votre travail
Après toutes ces configurations, vous ne voudriez pas perdre votre travail ! Enregistrez le classeur modifié comme ceci :
```csharp
workbook.Save(dataDir + "output.xls");
```
Vous pouvez maintenant trouver le fichier Excel nouvellement créé dans votre répertoire de documents.
## Conclusion
Et voilà ! Nous avons parcouru une approche complète et pratique pour définir des formats de champ de page par programmation dans un tableau croisé dynamique à l'aide d'Aspose.Cells pour .NET. Grâce aux étapes simples fournies, vous devriez être sûr de pouvoir modifier vos données Excel en fonction de vos besoins de création de rapports. C'est incroyable ce que vous pouvez accomplir lorsque vous combinez la puissance de C# avec Aspose.Cells.
## FAQ
### Qu'est-ce qu'Aspose.Cells ?
Aspose.Cells est une bibliothèque .NET qui permet aux développeurs de créer, manipuler et convertir des fichiers Excel par programmation.
### Comment installer Aspose.Cells ?
 Vous pouvez le télécharger directement depuis le[Site Web d'Aspose](https://releases.aspose.com/cells/net/).
### Puis-je utiliser Aspose.Cells sans installation Excel ?
Oui, Aspose.Cells est une bibliothèque autonome qui ne nécessite pas l'installation de Microsoft Excel.
### Où puis-je trouver une assistance détaillée ?
 Vous pouvez accéder à une assistance détaillée et à des forums sur[Assistance Aspose](https://forum.aspose.com/c/cells/9).
### Comment puis-je obtenir un permis temporaire ?
 Vous pouvez acquérir une licence temporaire auprès de[ici](https://purchase.aspose.com/temporary-license/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
