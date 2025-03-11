---
title: Application de la mise en forme conditionnelle lors de l'exécution dans Excel
linktitle: Application de la mise en forme conditionnelle lors de l'exécution dans Excel
second_title: API de traitement Excel Aspose.Cells .NET
description: Découvrez comment appliquer la mise en forme conditionnelle au moment de l'exécution dans Excel avec Aspose.Cells pour .NET dans ce guide complet, étape par étape.
weight: 11
url: /fr/net/excel-conditional-formatting/applying-conditional-formatting-at-runtime/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Application de la mise en forme conditionnelle lors de l'exécution dans Excel

## Introduction

Ce sont des outils puissants pour l'analyse et la visualisation des données. L'une des fonctionnalités les plus remarquables d'Excel est la mise en forme conditionnelle, qui permet aux utilisateurs d'appliquer des styles de mise en forme spécifiques aux cellules en fonction de leurs valeurs. Cela peut faciliter l'identification des tendances, mettre en évidence des points de données importants ou simplement rendre les données plus lisibles. Si vous cherchez à implémenter la mise en forme conditionnelle dans vos fichiers Excel par programmation, vous êtes au bon endroit ! Dans ce guide, nous vous expliquerons comment appliquer la mise en forme conditionnelle au moment de l'exécution à l'aide d'Aspose.Cells pour .NET.

## Prérequis
Avant de plonger dans le code, assurons-nous que vous disposez de tout ce dont vous avez besoin pour commencer :

1. Visual Studio : assurez-vous que Visual Studio est installé sur votre ordinateur. Vous pouvez utiliser n’importe quelle version prenant en charge le développement .NET.
2.  Aspose.Cells pour .NET : vous devez avoir installé Aspose.Cells pour .NET. Vous pouvez le télécharger à partir du[Site Web d'Aspose](https://releases.aspose.com/cells/net/).
3. Connaissances de base de C# : la familiarité avec la programmation C# vous aidera à mieux comprendre les extraits de code.
4. .NET Framework : assurez-vous que votre projet cible une version compatible du .NET Framework.

Maintenant que nous avons couvert les prérequis, passons à la partie amusante !

## Paquets d'importation
Pour commencer à utiliser Aspose.Cells, vous devez importer les espaces de noms nécessaires dans votre projet C#. Voici comment procéder :

```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

Ces espaces de noms vous donneront accès aux classes et méthodes nécessaires à la manipulation de fichiers Excel et à l'application d'une mise en forme conditionnelle.

Décomposons maintenant le processus d’application de la mise en forme conditionnelle en étapes gérables.

## Étape 1 : Configurez votre projet
Tout d'abord, vous devez créer un nouveau projet C# dans Visual Studio. Voici comment procéder :

1. Ouvrez Visual Studio et sélectionnez Fichier > Nouveau > Projet.
2. Choisissez Application console (.NET Framework) et donnez un nom à votre projet.
3. Cliquez sur Créer.

## Étape 2 : Ajouter la référence Aspose.Cells
Une fois votre projet configuré, vous devez ajouter une référence à la bibliothèque Aspose.Cells :

1. Faites un clic droit sur votre projet dans l’Explorateur de solutions.
2. Sélectionnez Gérer les packages NuGet.
3. Recherchez Aspose.Cells et installez-le.

Cela vous permettra d'utiliser toutes les fonctionnalités fournies par la bibliothèque Aspose.Cells.

## Étape 3 : Créer un objet classeur
Ensuite, créons un nouveau classeur et une feuille de calcul. C'est ici que toute la magie opère :

```csharp
// Le chemin vers le répertoire des documents.
string dataDir = "Your Document Directory";
string filePath = dataDir + "Book1.xlsx";

// Instanciation d'un objet Workbook
Workbook workbook = new Workbook();
Worksheet sheet = workbook.Worksheets[0];
```

Dans cette étape, nous définissons le répertoire dans lequel notre fichier Excel sera enregistré, créons un nouveau classeur et accédons à la première feuille de calcul.

## Étape 4 : ajouter une mise en forme conditionnelle
Maintenant, ajoutons un formatage conditionnel. Nous allons commencer par créer un objet de formatage conditionnel vide :

```csharp
// Ajoute une mise en forme conditionnelle vide
int index = sheet.ConditionalFormattings.Add();
FormatConditionCollection fcs = sheet.ConditionalFormattings[index];
```

Ici, nous ajoutons une nouvelle collection de mise en forme conditionnelle à notre feuille de calcul, qui contiendra nos règles de mise en forme.

## Étape 5 : Définir la plage de format
Ensuite, nous devons spécifier la plage de cellules à laquelle la mise en forme conditionnelle s'appliquera. Supposons que nous souhaitons formater la première ligne et la deuxième colonne :

```csharp
// Définit la plage de format conditionnel.
CellArea ca = new CellArea();
ca.StartRow =0;
ca.EndRow =0;
ca.StartColumn =0;
ca.EndColumn =0;
fcs.AddArea(ca);

ca = new CellArea();
ca.StartRow =1;
ca.EndRow =1;
ca.StartColumn =1;
ca.EndColumn =1;
fcs.AddArea(ca);
```

Dans ce code, nous définissons deux zones pour la mise en forme conditionnelle. La première zone concerne la cellule à (0,0) et la seconde à (1,1). N'hésitez pas à ajuster ces plages en fonction de vos besoins spécifiques !

## Étape 6 : Ajouter des conditions de mise en forme conditionnelle
Il est maintenant temps de définir les conditions de notre mise en forme. Supposons que nous souhaitons mettre en évidence des cellules en fonction de leurs valeurs :

```csharp
// Ajoute une condition.
int conditionIndex = fcs.AddCondition(FormatConditionType.CellValue, OperatorType.Between, "=A2", "100");

// Ajoute une condition.
int conditionIndex2 = fcs.AddCondition(FormatConditionType.CellValue, OperatorType.Between, "50", "100");
```

 Dans cette étape, nous ajoutons deux conditions : une pour les valeurs comprises entre`A2` et`100` , et un autre pour les valeurs comprises entre`50` et`100`Cela vous permet de mettre en évidence dynamiquement les cellules en fonction de leurs valeurs.

## Étape 7 : Définir les styles de formatage
Une fois nos conditions définies, nous pouvons maintenant définir les styles de mise en forme. Modifions la couleur d'arrière-plan de nos conditions :

```csharp
// Définit la couleur d'arrière-plan.
FormatCondition fc = fcs[conditionIndex];
fc.Style.BackgroundColor = Color.Red;
```

Ici, nous définissons la couleur d'arrière-plan de la première condition sur rouge. Vous pouvez personnaliser davantage cette option en modifiant la couleur de la police, les bordures et d'autres styles selon vos besoins !

## Étape 8 : Enregistrez le fichier Excel
Enfin, il est temps de sauvegarder notre travail ! Nous allons enregistrer le classeur dans le répertoire spécifié :

```csharp
// Sauvegarde du fichier Excel
workbook.Save(dataDir + "output.xls");
```

Cette ligne de code enregistre le fichier Excel avec la mise en forme conditionnelle appliquée. Assurez-vous de vérifier le répertoire spécifié pour votre fichier de sortie !

## Conclusion
Et voilà ! Vous avez appliqué avec succès la mise en forme conditionnelle au moment de l'exécution dans Excel à l'aide d'Aspose.Cells pour .NET. Cette puissante bibliothèque facilite la manipulation de fichiers Excel par programmation, vous permettant d'automatiser des tâches fastidieuses et d'améliorer vos présentations de données. Que vous travailliez sur un petit projet ou sur une application à grande échelle, Aspose.Cells peut vous aider à rationaliser votre flux de travail et à améliorer votre productivité.

## FAQ

### Qu'est-ce qu'Aspose.Cells ?
Aspose.Cells est une bibliothèque .NET qui permet aux développeurs de créer, manipuler et convertir des fichiers Excel par programmation.

### Puis-je utiliser Aspose.Cells avec d’autres langages de programmation ?
Oui, Aspose.Cells est disponible pour plusieurs langages de programmation, notamment Java, Python, etc.

### Existe-t-il un essai gratuit disponible pour Aspose.Cells ?
 Oui, vous pouvez télécharger une version d'essai gratuite à partir du[Site Web d'Aspose](https://releases.aspose.com/).

### Comment puis-je obtenir de l'aide pour Aspose.Cells ?
 Vous pouvez obtenir de l'aide en visitant le[Forum d'assistance Aspose](https://forum.aspose.com/c/cells/9).

### Ai-je besoin d'une licence pour utiliser Aspose.Cells ?
 Oui, une licence est requise pour une utilisation commerciale, mais vous pouvez demander une licence temporaire[ici](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
