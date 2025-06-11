---
"description": "Apprenez à définir les formats des champs de page dans les tableaux croisés dynamiques par programmation avec Aspose.Cells pour .NET. Suivez notre tutoriel étape par étape pour une gestion fluide des données."
"linktitle": "Définition du format des champs de page par programmation dans .NET"
"second_title": "API de traitement Excel Aspose.Cells .NET"
"title": "Définition du format des champs de page par programmation dans .NET"
"url": "/fr/net/creating-and-configuring-pivot-tables/setting-page-field-format/"
"weight": 21
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Définition du format des champs de page par programmation dans .NET

## Introduction
Créer et manipuler des fichiers Excel par code peut s'avérer très utile, surtout pour analyser de grands ensembles de données. Aspose.Cells pour .NET est un outil formidable qui vous permet d'interagir par programmation avec des fichiers Excel et de créer des structures de rapport complexes. Dans ce tutoriel, nous allons découvrir comment configurer les formats de champs de page dans un tableau croisé dynamique grâce à cette puissante bibliothèque. Que vous soyez un développeur expérimenté ou un débutant, à la fin de ce guide, vous maîtriserez parfaitement l'utilisation des tableaux croisés dynamiques et leurs différents paramètres dans .NET.
## Prérequis
Avant de nous lancer tête baissée dans le codage, assurons-nous que tout est correctement configuré. Voici ce dont vous aurez besoin :
- Visual Studio : un environnement de travail dans lequel vous pouvez écrire et exécuter votre code .NET.
- Aspose.Cells : Vous pouvez télécharger la bibliothèque [ici](https://releases.aspose.com/cells/net/).
- Connaissances de base de C# : la familiarité avec la programmation C# vous aidera à mieux comprendre les extraits de code.
- Fichier Excel : Préparez un fichier Excel (comme `Book1.xls`) contenant des données adaptées à la création de tableaux croisés dynamiques. 
Si vous ne l'avez pas déjà fait, obtenez votre essai gratuit d'Aspose.Cells [ici](https://releases.aspose.com/).
## Importer des packages
Pour commencer, vous devrez importer les bons packages dans votre projet. Commencez par ajouter des références à la bibliothèque Aspose.Cells dans votre projet C#. Voici comment procéder :
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
using Aspose.Cells.Pivot;
```
Cela rassemblera toutes les classes et méthodes nécessaires pour manipuler les fichiers Excel à l'aide d'Aspose.Cells.
## Étape 1 : Configurez votre espace de travail
Commencez par définir le répertoire de travail où seront stockés vos fichiers Excel. Par exemple, vous pouvez déclarer une variable comme ceci :
```csharp
string dataDir = "Your Document Directory";
```
## Chargement du classeur
Ensuite, nous devons charger notre modèle Excel. Cette étape est essentielle car elle établit le contexte de nos opérations :
```csharp
Workbook workbook = new Workbook(dataDir + "Book1.xls");
```
Cette ligne charge le classeur existant à partir du répertoire spécifié.
## Étape 2 : Accéder à la feuille de travail
Une fois votre classeur chargé, accédez à la feuille de calcul contenant le tableau croisé dynamique ou les données à analyser. Voici comment procéder :
```csharp
Worksheet worksheet = workbook.Worksheets[0];
```
Cela récupère la première feuille de calcul du classeur chargé. Vous pouvez facilement modifier l'index si vous travaillez avec plusieurs feuilles.
## Étape 3 : Accéder au tableau croisé dynamique
Poursuivons avec l'accès au tableau croisé dynamique de la feuille de calcul choisie. Si vous utilisez un seul tableau croisé dynamique, vous pouvez définir son index à `0`:
```csharp
int pivotindex = 0;
// Accéder au tableau croisé dynamique
PivotTable pivotTable = worksheet.PivotTables[pivotindex];
```
Cet extrait de code sélectionne le premier tableau croisé dynamique dans la feuille de calcul. 
## Étape 4 : Configuration du tableau croisé dynamique
Passons maintenant à la partie passionnante ! Paramétrons le tableau croisé dynamique pour afficher les totaux généraux des lignes :
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
Vous souhaitez définir des types de sous-totaux spécifiques ? Nous allons accéder au premier champ de notre collection et le configurer :
```csharp
Aspose.Cells.Pivot.PivotField pivotField = pivotFields[0];
// Définition des sous-totaux.
pivotField.SetSubtotals(Aspose.Cells.Pivot.PivotFieldSubtotalType.Sum, true);
pivotField.SetSubtotals(Aspose.Cells.Pivot.PivotFieldSubtotalType.Count, true);
```
En activant `Sum` et `Count` sous-totaux, nous pouvons rapidement résumer les données dans notre rapport.
## Étape 6 : Définition des options de tri automatique
Passons maintenant à un tri intelligent. Ainsi, votre tableau croisé dynamique organisera les données dans un ordre pertinent :
```csharp
// Définition des options de tri automatique.
pivotField.IsAutoSort = true;
pivotField.IsAscendSort = true;
pivotField.AutoSortField = -5; // Utilisation d'un champ de tri prédéfini.
```
Cet extrait de code permet le tri automatique et spécifie l'ordre croissant. 
## Étape 7 : Définition des options d'affichage automatique
Souhaitez-vous filtrer davantage vos données ? L'option Affichage automatique permet d'afficher des points de données spécifiques dans des conditions définies :
```csharp
// Définition des options d'affichage automatique.
pivotField.IsAutoShow = true;
pivotField.IsAscendShow = false;
pivotField.AutoShowField = 0; // Spécifiez le champ à afficher automatiquement.
```
Cela garantit que votre tableau croisé dynamique affiche uniquement les données pertinentes, améliorant ainsi la clarté et la concentration.
## Étape 8 : Enregistrer votre travail
Après toutes ces configurations, vous ne voudriez pas perdre votre travail ! Enregistrez le classeur modifié comme ceci :
```csharp
workbook.Save(dataDir + "output.xls");
```
Vous pouvez maintenant trouver le fichier Excel nouvellement créé dans votre répertoire de documents.
## Conclusion
Et voilà ! Nous avons présenté une approche complète et pratique pour définir les formats des champs de page par programmation dans un tableau croisé dynamique avec Aspose.Cells pour .NET. Grâce aux étapes simples fournies, vous pourrez modifier vos données Excel en toute confiance pour répondre à vos besoins de reporting. Les possibilités offertes par la combinaison de la puissance de C# et d'Aspose.Cells sont impressionnantes.
## FAQ
### Qu'est-ce qu'Aspose.Cells ?
Aspose.Cells est une bibliothèque .NET qui permet aux développeurs de créer, manipuler et convertir des fichiers Excel par programmation.
### Comment installer Aspose.Cells ?
Vous pouvez le télécharger directement depuis le [Site Web d'Aspose](https://releases.aspose.com/cells/net/).
### Puis-je utiliser Aspose.Cells sans installation Excel ?
Oui, Aspose.Cells est une bibliothèque autonome qui ne nécessite pas l’installation de Microsoft Excel.
### Où puis-je trouver une assistance détaillée ?
Vous pouvez accéder à une assistance détaillée et à des forums sur [Assistance Aspose](https://forum.aspose.com/c/cells/9).
### Comment puis-je obtenir un permis temporaire ?
Vous pouvez acquérir une licence temporaire auprès de [ici](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}