---
"description": "Apprenez à trier par programmation des tableaux croisés dynamiques dans .NET avec Aspose.Cells. Un guide étape par étape couvre l'installation, la configuration, le tri et l'enregistrement des résultats au format Excel et PDF."
"linktitle": "Tri personnalisé des tableaux croisés dynamiques par programmation dans .NET"
"second_title": "API de traitement Excel Aspose.Cells .NET"
"title": "Tri personnalisé des tableaux croisés dynamiques par programmation dans .NET"
"url": "/fr/net/creating-and-configuring-pivot-tables/pivot-table-custom-sort/"
"weight": 29
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Tri personnalisé des tableaux croisés dynamiques par programmation dans .NET

## Introduction
Pour travailler avec Excel dans un environnement .NET, une bibliothèque se démarque : Aspose.Cells. N'est-ce pas un plaisir de pouvoir manipuler des feuilles de calcul par programmation ? C'est précisément ce que fait Aspose.Cells ! Dans le tutoriel d'aujourd'hui, nous plongeons dans l'univers des tableaux croisés dynamiques et vous montrons comment implémenter un tri personnalisé par programmation grâce à cette bibliothèque polyvalente.
## Prérequis
Avant de retrousser nos manches et de nous plonger dans le code, assurez-vous d'avoir mis en place quelques éléments :
1. Visual Studio : vous aurez besoin d'une version fonctionnelle de Visual Studio. C'est là que toute la magie opère.
2. .NET Framework : une connaissance de la programmation .NET est essentielle. Que vous soyez un adepte de .NET Core ou de .NET Framework, vous êtes prêt à vous lancer.
3. Bibliothèque Aspose.Cells : vous devez installer la bibliothèque Aspose.Cells. Vous pouvez l'obtenir depuis le [Lien de téléchargement](https://releases.aspose.com/cells/net/) et ajoutez-le à votre projet.
4. Compréhension de base des tableaux croisés dynamiques : bien que vous n’ayez pas besoin d’être un expert, quelques connaissances sur le fonctionnement des tableaux croisés dynamiques seront utiles au cours de ce didacticiel.
5. Exemple de fichier Excel : avoir un exemple de fichier Excel nommé `SamplePivotSort.xlsx` prêt dans votre répertoire de travail pour les tests.
## Importer des packages
Une fois tous les prérequis définis, la première étape consiste à importer les packages nécessaires. Pour ce faire, ajoutez les lignes suivantes au début de votre code :
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells;
using Aspose.Cells.Pivot;
```
Ce package fournit toutes les fonctionnalités dont vous avez besoin pour manipuler des fichiers Excel à l'aide d'Aspose.Cells.

Très bien, passons à la partie amusante ! Nous allons décomposer le processus de création d'un tableau croisé dynamique et d'application d'un tri personnalisé en étapes faciles à gérer.
## Étape 1 : Configurer le classeur
Pour commencer, nous devons configurer notre classeur. Voici comment procéder :
```csharp
string sourceDir = "Your Document Directory";
string outputDir = "Your Document Directory";
Workbook wb = new Workbook(sourceDir + "SamplePivotSort.xlsx");
```
Dans cette étape, nous initialisons un nouveau `Workbook` avec le chemin d'accès à notre fichier Excel. Ce chemin servira de toile de fond à notre tableau croisé dynamique.
## Étape 2 : Accéder à la feuille de travail
Ensuite, nous devons accéder à la feuille de calcul dans laquelle nous ajouterons notre tableau croisé dynamique.
```csharp
Worksheet sheet = wb.Worksheets[0];
PivotTableCollection pivotTables = sheet.PivotTables;
```
Ici, nous prenons la première feuille de travail de notre classeur et faisons appel à la `PivotTableCollection`. Cette collection nous permet de gérer tous les tableaux croisés dynamiques de cette feuille de calcul.
## Étape 3 : Créez votre premier tableau croisé dynamique
Il est maintenant temps de créer notre tableau croisé dynamique.
```csharp
int index = pivotTables.Add("=Sheet1!A1:C10", "E3", "PivotTable1");
PivotTable pivotTable = pivotTables[index];
```
Nous ajoutons un nouveau tableau croisé dynamique à notre feuille de calcul, en spécifiant la plage de données et son emplacement. « E3 » indique le début du tableau croisé dynamique. Nous référençons ensuite ce nouveau tableau croisé dynamique à l'aide de son index.
## Étape 4 : Configurer les paramètres du tableau croisé dynamique
Configurons notre tableau croisé dynamique ! Cela implique de contrôler des aspects tels que les totaux généraux et la disposition des champs.
```csharp
pivotTable.RowGrand = false;
pivotTable.ColumnGrand = false;
pivotTable.AddFieldToArea(PivotFieldType.Row,1);
PivotField rowField = pivotTable.RowFields[0];
rowField.IsAutoSort = true;
rowField.IsAscendSort = true;
```
Nous veillons à ce que les totaux généraux des lignes et des colonnes ne soient pas affichés, ce qui permet de clarifier les données. Nous ajoutons ensuite le premier champ à la zone de ligne, permettant ainsi le tri automatique et le tri croissant.
## Étape 5 : Ajouter des colonnes et des champs de données
Une fois les lignes définies, ajoutons la colonne et les champs de données.
```csharp
pivotTable.AddFieldToArea(PivotFieldType.Column,0);
PivotField colField = pivotTable.ColumnFields[0];
colField.NumberFormat = "dd/mm/yyyy";
colField.IsAutoSort = true;
colField.IsAscendSort = true;
```
Nous ajoutons le deuxième champ comme colonne et le formatons comme date. Nous activons à nouveau le tri automatique et l'ordre croissant pour une meilleure organisation. Enfin, nous devons ajouter le troisième champ à notre zone de données :
```csharp
pivotTable.AddFieldToArea(PivotFieldType.Data,2);
```
## Étape 6 : Actualiser et calculer le tableau croisé dynamique
Après avoir ajouté tous les champs nécessaires, assurons-nous que notre tableau croisé dynamique est à jour et prêt.
```csharp
pivotTable.RefreshData();
pivotTable.CalculateData();
```
Ces méthodes actualisent les données et les recalculent, garantissant que tout est à jour et affiché correctement dans notre tableau croisé dynamique.
## Étape 7 : Tri personnalisé basé sur les valeurs des champs de ligne
Ajoutons un peu de style en triant le tableau croisé dynamique en fonction de valeurs spécifiques, comme « Fruits de mer ».
```csharp
index = pivotTables.Add("=Sheet1!A1:C10", "E10", "PivotTable2");
pivotTable = pivotTables[index];
```
Nous répétons le processus en créant un autre tableau croisé dynamique et en le configurant de la même manière que le premier. Nous pouvons maintenant le personnaliser davantage :
```csharp
pivotTable.AddFieldToArea(PivotFieldType.Row,1);
rowField = pivotTable.RowFields[0];
rowField.IsAutoSort = true;
rowField.IsAscendSort = true;
```
## Étape 8 : Personnalisation supplémentaire du triEssayons une autre méthode de tri basée sur une date spécifique :
```csharp
// Ajout d'un autre tableau croisé dynamique pour le tri par date
index = pivotTables.Add("=Sheet1!A1:C10", "E18", "PivotTable3");
pivotTable = pivotTables[index];
// Répétez les paramètres de ligne et de colonne de manière similaire aux étapes précédentes
```
Vous parcourez simplement le même processus, en créant un troisième tableau croisé dynamique avec ses critères de tri adaptés à vos besoins.
## Étape 9 : Enregistrez le classeurIl est temps de sauvegarder tout le travail acharné que nous avons accompli !
```csharp
wb.Save(outputDir + "out.xlsx");
PdfSaveOptions options = new PdfSaveOptions();
options.OnePagePerSheet = true;
wb.Save(outputDir + "out.pdf", options);
```
Ici, vous enregistrez le classeur sous forme de fichier Excel et de PDF. `PdfSaveOptions` permet un meilleur formatage, garantissant que chaque feuille apparaît sur une page distincte lors de la conversion.
## Étape 10 : TerminerConcluez le tout en faisant savoir à l'utilisateur que tout va bien.
```csharp
Console.WriteLine("PivotTableCustomSort executed successfully.");
```
## Conclusion
Vous savez désormais exploiter la puissance d'Aspose.Cells pour créer et personnaliser des tableaux croisés dynamiques dans vos applications .NET. De la configuration initiale au tri personnalisé, chaque étape se combine pour offrir une expérience fluide. Que vous ayez besoin de présenter des données de ventes annuelles ou de suivre des statistiques de stock, ces compétences vous seront utiles !
## FAQ
### Qu'est-ce qu'un tableau croisé dynamique ?
Un tableau croisé dynamique est un outil de traitement de données dans Excel qui vous permet de résumer et d'analyser des données, offrant un moyen flexible d'extraire facilement des informations.
### Comment installer Aspose.Cells ?
Vous pouvez l'installer via NuGet dans Visual Studio ou le télécharger directement depuis le [Lien de téléchargement](https://releases.aspose.com/cells/net/).
### Existe-t-il une version d'essai d'Aspose.Cells ?
Oui ! Vous pouvez l'essayer gratuitement en visitant le [Lien d'essai gratuit](https://releases.aspose.com/).
### Puis-je trier plusieurs champs dans un tableau croisé dynamique ?
Absolument ! Vous pouvez ajouter et trier plusieurs champs selon vos besoins.
### Où puis-je trouver du support pour Aspose.Cells ?
La communauté est assez active et vous pouvez poser des questions sur leur forum [ici](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}