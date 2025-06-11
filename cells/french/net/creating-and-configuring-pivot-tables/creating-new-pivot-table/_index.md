---
"description": "Apprenez à créer un tableau croisé dynamique par programmation dans .NET avec Aspose.Cells grâce à notre guide étape par étape. Analysez efficacement vos données."
"linktitle": "Créer un nouveau tableau croisé dynamique par programmation dans .NET"
"second_title": "API de traitement Excel Aspose.Cells .NET"
"title": "Créer un nouveau tableau croisé dynamique par programmation dans .NET"
"url": "/fr/net/creating-and-configuring-pivot-tables/creating-new-pivot-table/"
"weight": 13
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Créer un nouveau tableau croisé dynamique par programmation dans .NET

## Introduction
Créer un tableau croisé dynamique peut sembler intimidant, surtout par programmation. Mais pas d'inquiétude ! Avec Aspose.Cells pour .NET, créer un tableau croisé dynamique est non seulement simple, mais aussi très performant pour l'analyse de données. Dans ce tutoriel, nous vous guiderons pas à pas pour créer un tableau croisé dynamique dans une application .NET. Que vous ajoutiez des données pour les ventes, les statistiques sportives ou tout autre indicateur commercial, ce guide vous aidera à mettre en place vos tableaux croisés dynamiques en un rien de temps.

## Prérequis
Avant de commencer, assurez-vous que tout est prêt. Voici ce que vous devez faire :

1. Installer .NET Framework : assurez-vous que .NET Framework est installé sur votre ordinateur. Aspose.Cells prend en charge plusieurs versions, mais il est préférable de conserver la plus récente.
2. Bibliothèque Aspose.Cells : vous devez disposer de la bibliothèque Aspose.Cells. Vous pouvez [téléchargez-le ici](https://releases.aspose.com/cells/net/) ou obtenir un [permis temporaire](https://purchase.aspose.com/temporary-license/) pour évaluation.
3. Configuration de l'IDE : préparez un IDE compatible C#, comme Visual Studio, où vous pouvez démarrer un nouveau projet.
4. Connaissances de base de C# : la familiarité avec la programmation C# vous aidera à suivre sans trop vous enliser.

Tout est prêt ? Parfait ! Passons maintenant à l'importation des paquets nécessaires.

## Importer des packages
Tout d'abord, vous devez importer les espaces de noms requis dans votre projet C#. Ouvrez votre fichier C# et ajoutez les directives using suivantes :

```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

Ces espaces de noms vous donnent accès aux fonctionnalités de classeur, de feuille de calcul et de tableau croisé dynamique que nous utiliserons tout au long de ce didacticiel.

## Étape 1 : Créer un objet classeur
Créer un classeur est le début de votre aventure. Commençons par créer un nouveau classeur et accéder à la première feuille de calcul.

```csharp
// Le chemin vers le répertoire des documents.
string dataDir = "Your Document Directory";
// Instanciation d'un objet Workbook
Workbook workbook = new Workbook();

// Obtention de la référence de la feuille de calcul nouvellement ajoutée
Worksheet sheet = workbook.Worksheets[0];
```

Dans cette étape, nous créons un `Workbook` instance qui représente notre fichier Excel et récupérez la toute première feuille de calcul, qui sera notre terrain de jeu pour le tableau croisé dynamique.

## Étape 2 : Insérer des données dans les cellules
Ensuite, remplissons notre feuille de calcul avec quelques exemples de données. Nous allons saisir des lignes pour différents sports, trimestres et chiffres de vente afin de synthétiser notre tableau croisé dynamique.

```csharp
Cells cells = sheet.Cells;

// Définition de la valeur des cellules
Cell cell = cells["A1"];
cell.PutValue("Sport");
cell = cells["B1"];
cell.PutValue("Quarter");
cell = cells["C1"];
cell.PutValue("Sales");

// Remplissage de datacell = cells["A2"];
cell.PutValue("Golf");
// ... Plus d'entrées de données
```

Ici, nous définissons nos en-têtes de colonnes et insérons des valeurs sous chaque en-tête. Ces données serviront de source à notre tableau croisé dynamique ; assurez-vous donc qu'elles sont bien organisées ! Suivez ce bloc et vous créerez un ensemble de données complet.

## Étape 3 : Ajout d'un tableau croisé dynamique
Une fois nos données prêtes, il est temps de créer le tableau croisé dynamique. Nous utiliserons la collection de tableaux croisés dynamiques de la feuille de calcul pour ajouter notre nouveau tableau croisé dynamique.

```csharp
Aspose.Cells.Pivot.PivotTableCollection pivotTables = sheet.PivotTables;

// Ajout d'un tableau croisé dynamique à la feuille de calcul
int index = pivotTables.Add("=A1:C8", "E3", "PivotTable2");
```

Dans cet extrait, nous ajoutons un tableau croisé dynamique à la feuille de calcul qui référence notre plage de données (ici, les cellules A1 à C8). Nous plaçons le tableau croisé dynamique à partir de la cellule E3 et le nommons « PivotTable2 ». Plutôt simple, non ?

## Étape 4 : Personnaliser le tableau croisé dynamique
Maintenant que nous avons notre tableau croisé dynamique, personnalisons-le pour afficher des résumés pertinents. Nous pouvons contrôler le contenu des lignes, des colonnes et des zones de données du tableau croisé dynamique.

```csharp
// Accéder à l'instance du tableau croisé dynamique nouvellement ajouté
Aspose.Cells.Pivot.PivotTable pivotTable = pivotTables[index];

// Désaffichage des totaux généraux pour les lignes.
pivotTable.RowGrand = false;

// Faites glisser le premier champ vers la zone de ligne.
pivotTable.AddFieldToArea(Aspose.Cells.Pivot.PivotFieldType.Row, 0);

// Faites glisser le deuxième champ vers la zone de colonne.
pivotTable.AddFieldToArea(Aspose.Cells.Pivot.PivotFieldType.Column, 1);

// Faites glisser le troisième champ vers la zone de données.
pivotTable.AddFieldToArea(Aspose.Cells.Pivot.PivotFieldType.Data, 2);
```

Dans cette étape, nous demandons au tableau croisé dynamique de masquer les totaux généraux des lignes, puis nous spécifions les champs à afficher dans les zones de lignes, de colonnes et de données. Les noms des sports rempliront les lignes, les trimestres les colonnes et les chiffres de ventes fourniront les résumés.

## Étape 5 : Enregistrer le classeur
Enfin, nous souhaitons sauvegarder notre classeur nouvellement créé pour voir les fruits de notre travail.

```csharp
// Sauvegarde du fichier Excel
workbook.Save(dataDir + "pivotTable_test_out.xls");
```

Fournissez simplement un chemin approprié et votre sortie de tableau croisé dynamique sera enregistrée dans un fichier Excel que vous pourrez ouvrir et consulter.

## Conclusion
Créer des tableaux croisés dynamiques par programmation avec Aspose.Cells pour .NET peut vous faire gagner un temps précieux, notamment lorsque vous traitez de grands ensembles de données. Vous avez appris à configurer votre projet, à importer les packages nécessaires, à renseigner les données et à créer un tableau croisé dynamique personnalisable de A à Z. Alors, la prochaine fois que vous serez submergé par les chiffres, souvenez-vous de ce tutoriel et laissez Aspose.Cells s'occuper du reste.

## FAQ
### Qu'est-ce qu'Aspose.Cells ?
Aspose.Cells est une puissante bibliothèque .NET permettant de créer et de gérer des feuilles de calcul Excel par programmation.

### Existe-t-il un essai gratuit pour Aspose.Cells ?
Oui, vous pouvez obtenir un essai gratuit [ici](https://releases.aspose.com/).

### Puis-je personnaliser l’apparence du tableau croisé dynamique ?
Absolument ! Vous pouvez personnaliser la mise en forme, la mise en page et même les styles du tableau croisé dynamique selon vos besoins.

### Où puis-je trouver plus d'exemples et de documentation sur Aspose.Cells ?
Vous pouvez vérifier le [documentation](https://reference.aspose.com/cells/net/) pour des guides et des exemples complets.

### Comment obtenir de l'aide pour Aspose.Cells ?
Vous pouvez obtenir de l'aide via le [Forum Aspose](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}