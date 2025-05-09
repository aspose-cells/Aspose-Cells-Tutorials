---
"description": "Apprenez à obtenir des points de connexion de formes dans Excel avec Aspose.Cells pour .NET. Suivez notre guide étape par étape pour extraire et afficher facilement des points de forme par programmation."
"linktitle": "Obtenir les points de connexion de la forme dans Excel"
"second_title": "API de traitement Excel Aspose.Cells .NET"
"title": "Obtenir les points de connexion de la forme dans Excel"
"url": "/fr/net/excel-shapes-controls/get-connection-points-shape-excel/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Obtenir les points de connexion de la forme dans Excel

## Introduction
Lorsque vous travaillez avec des fichiers Excel par programmation, vous devez souvent interagir avec des formes intégrées aux feuilles. L'une des tâches les plus avancées consiste à extraire les points de connexion d'une forme. Ces points permettent de relier des formes à des connecteurs et de gérer leur disposition avec plus de précision. Si vous souhaitez obtenir les points de connexion d'une forme dans Excel, Aspose.Cells pour .NET est l'outil qu'il vous faut. Ce tutoriel vous guidera pas à pas pour y parvenir.
## Prérequis
Avant de plonger dans le code, assurez-vous de disposer des prérequis suivants :
- Aspose.Cells pour .NET : Aspose.Cells doit être installé dans votre environnement de développement. Si ce n'est pas déjà fait, vous pouvez le faire. [téléchargez la dernière version ici](https://releases.aspose.com/cells/net/).
- Environnement de développement : assurez-vous de disposer d’une installation fonctionnelle de Visual Studio ou de tout autre IDE compatible .NET.
- Connaissances de base de C# : ce didacticiel suppose que vous avez une compréhension de base de la programmation C# et des principes orientés objet.
Vous pouvez également vous inscrire à un [essai gratuit d'Aspose.Cells](https://releases.aspose.com/) Si ce n'est pas déjà fait, vous aurez accès à toutes les fonctionnalités nécessaires à ce guide.

## Importer des packages
Pour utiliser Aspose.Cells dans votre projet, vous devez inclure les espaces de noms nécessaires. Les instructions d'importation suivantes doivent être placées en haut de votre code :
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
Ces espaces de noms vous donnent accès aux fonctionnalités principales d'Aspose.Cells et vous permettent de manipuler des feuilles de calcul et des formes.

## Guide étape par étape pour obtenir les points de connexion d'une forme
Dans cette section, nous vous expliquerons comment extraire les points de connexion d'une forme dans une feuille de calcul Excel. Suivez attentivement chaque étape pour une compréhension claire.
## Étape 1 : créer un nouveau classeur
Tout d’abord, nous devons créer une instance du `Workbook` classe. Ceci représente un fichier Excel dans Aspose.Cells. Si vous n'avez pas de fichier existant, aucun problème : vous pouvez commencer avec un classeur vierge.
```csharp
// Instancier un nouveau classeur
Workbook workbook = new Workbook();
```
Dans cette étape, nous avons créé un classeur Excel vide, mais vous pouvez également en charger un existant en transmettant le chemin du fichier au `Workbook` constructeur.
## Étape 2 : Accéder à la première feuille de travail
Ensuite, nous devons accéder à la feuille de calcul dans laquelle nous souhaitons travailler avec les formes. Dans ce cas, nous utiliserons la première feuille du classeur.
```csharp
// Obtenez la première feuille de travail du classeur
Worksheet worksheet = workbook.Worksheets[0];
```
Cette ligne accède à la première feuille de calcul du classeur. Si vous travaillez sur une feuille spécifique, vous pouvez remplacer l'index. `0` avec l'index souhaité.
## Étape 3 : Ajouter une nouvelle zone de texte (forme)
Ajoutons maintenant une nouvelle forme à la feuille de calcul. Nous allons créer une zone de texte, qui est un type de forme. Vous pouvez également ajouter d'autres types de formes, mais pour plus de simplicité, nous utiliserons une zone de texte dans ce tutoriel.
```csharp
// Ajouter une nouvelle zone de texte à la collection
int textboxIndex = worksheet.TextBoxes.Add(2, 1, 160, 200);
```
Voici ce que nous avons fait :
- Ajout d'une zone de texte à la ligne `2`, colonne `1`.
- Définissez les dimensions de la zone de texte sur `160` unités de largeur et `200` unités de hauteur.
## Étape 4 : Accéder à la forme à partir de la collection de formes
Une fois la zone de texte ajoutée, elle fait partie de la collection de formes de la feuille de calcul. Nous allons maintenant y accéder grâce à l'icône `Shapes` collection.
```csharp
// Accéder à la forme (zone de texte) à partir de la collection de formes
Shape shape = workbook.Worksheets[0].Shapes[0];
```
Dans cette étape, nous récupérons la première forme (notre zone de texte) de la collection. Si vous avez plusieurs formes, vous pouvez spécifier l'index ou même rechercher la forme par son nom.
## Étape 5 : Récupérer les points de connexion
Maintenant que nous avons notre forme, extrayons ses points de connexion. Ces points servent à fixer les connecteurs à la forme. `ConnectionPoints` la propriété de la forme renvoie tous les points de connexion disponibles.
```csharp
// Obtenez tous les points de connexion dans cette forme
var connectionPoints = shape.ConnectionPoints;
```
Cela nous donne une collection de tous les points de connexion disponibles pour cette forme.
## Étape 6 : Afficher les points de connexion
Enfin, nous souhaitons afficher les coordonnées de chaque point de connexion. C'est ici que nous parcourons les points de connexion et les affichons dans la console.
```csharp
// Afficher tous les points de forme
foreach (var pt in connectionPoints)
{
    System.Console.WriteLine(string.Format("X = {0}, Y = {1}", pt.X, pt.Y));
}
```
Cette boucle parcourt chaque point de connexion et imprime le `X` et `Y` coordonnées. Cela peut être utile pour déboguer ou confirmer visuellement les points de connexion d'une forme.
## Étape 7 : Exécuter et terminer
Une fois toutes les étapes ci-dessus configurées, vous pouvez exécuter le code. Voici la dernière ligne qui garantit le bon déroulement du processus :
```csharp
System.Console.WriteLine("GetShapeConnectionPoints executed successfully.");
```
Cette ligne enregistre simplement un message sur la console indiquant que le processus est terminé.

## Conclusion
Dans ce tutoriel, nous avons expliqué comment récupérer les points de connexion d'une forme dans Excel à l'aide d'Aspose.Cells pour .NET. En décomposant la tâche en étapes simples et faciles à comprendre, nous avons exploré le processus de création d'un classeur, d'ajout d'une forme et d'extraction des points de connexion.
En comprenant comment manipuler les formes par programmation, vous accédez à un monde de possibilités pour créer des feuilles Excel dynamiques et interactives. Que vous créiez des rapports, des tableaux de bord ou des diagrammes, ces connaissances vous seront utiles.
## FAQ
### Qu'est-ce qu'un point de connexion dans une forme ?
Un point de connexion est un point spécifique sur une forme où vous pouvez attacher des connecteurs ou le lier à d'autres formes.
### Puis-je récupérer les points de connexion pour toutes les formes dans une feuille de calcul ?
Oui, Aspose.Cells vous permet de récupérer les points de connexion de toute forme qui les prend en charge. Parcourez simplement la collection de formes dans la feuille de calcul.
### Ai-je besoin d'une licence pour utiliser Aspose.Cells ?
Oui, vous pouvez l'essayer gratuitement, mais une licence est requise pour accéder à toutes les fonctionnalités. Vous pouvez [acheter une licence ici](https://purchase.aspose.com/buy) ou obtenir un [permis temporaire](https://purchase.aspose.com/temporary-license/).
### Comment puis-je ajouter différents types de formes dans Aspose.Cells ?
Vous pouvez utiliser le `Add` Méthode pour les formes telles que les rectangles, les ellipses, etc. Chaque forme possède des paramètres spécifiques personnalisables.
### Comment charger un fichier Excel existant au lieu d'en créer un nouveau ?
Pour charger un fichier existant, transmettez le chemin du fichier à l' `Workbook` constructeur, comme ceci :  
```csharp
Workbook workbook = new Workbook("path_to_file.xlsx");
```

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}