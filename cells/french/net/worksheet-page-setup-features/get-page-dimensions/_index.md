---
"description": "Apprenez à obtenir les dimensions d'une page dans une feuille de calcul Excel avec Aspose.Cells pour .NET. Un guide étape par étape pour personnaliser les formats de papier A2, A3, A4 et Lettre."
"linktitle": "Obtenir les dimensions de la page de la feuille de calcul"
"second_title": "API de traitement Excel Aspose.Cells .NET"
"title": "Obtenir les dimensions de la page de la feuille de calcul"
"url": "/fr/net/worksheet-page-setup-features/get-page-dimensions/"
"weight": 13
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Obtenir les dimensions de la page de la feuille de calcul

## Introduction
Si vous travaillez avec des fichiers Excel par programmation avec Aspose.Cells pour .NET, vous aurez peut-être besoin d'accéder aux dimensions de page d'une feuille de calcul et de les définir. Connaître ces dimensions peut faciliter la mise en page, l'impression et la personnalisation des feuilles Excel. Dans cet article, nous allons découvrir comment récupérer et afficher différentes dimensions de page dans Excel avec Aspose.Cells pour .NET. Un tutoriel étape par étape vous permettra de démarrer en toute confiance.
## Prérequis
Avant de plonger, assurons-nous que vous disposez de tout ce dont vous avez besoin pour suivre ce tutoriel.
1. Aspose.Cells pour .NET : Assurez-vous d'avoir installé Aspose.Cells pour .NET. Vous pouvez [téléchargez la bibliothèque ici](https://releases.aspose.com/cells/net/) ou installez-le via NuGet dans votre projet .NET.
2. Environnement .NET : un environnement de développement .NET compatible (par exemple, Visual Studio).
3. Configuration de la licence : Pour bénéficier de toutes les fonctionnalités d'Aspose.Cells, appliquez une licence. Vous pouvez [demander une licence temporaire gratuite](https://purchase.aspose.com/temporary-license/) à des fins d'évaluation.
Commencez par la version d'essai gratuite d'Aspose.Cells si vous l'évaluez pour la première fois.
## Importer des packages
Avant de passer au code, vous devrez importer l'espace de noms Aspose.Cells dans votre projet pour accéder à toutes les classes et méthodes nécessaires.
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Décomposons le processus en étapes simples. Ici, nous allons accéder à différents formats de papier, les appliquer à une feuille de calcul et imprimer les dimensions de chacun.
## Étape 1 : Créer une instance de classeur
La première étape consiste à créer une instance du `Workbook` classe. Cet objet servira de classeur principal contenant des feuilles de calcul manipulables.
```csharp
Workbook book = new Workbook();
```
Pensez à `Workbook` comme conteneur principal de votre fichier Excel. Nous en avons besoin pour accéder et contrôler les feuilles de calcul individuelles.
## Étape 2 : Accéder à la première feuille de travail
Ensuite, accédons à la première feuille du classeur. Par défaut, un nouveau classeur contient une seule feuille ; nous pouvons donc y faire directement référence grâce à un index. `0`.
```csharp
Worksheet sheet = book.Worksheets[0];
```
Le `Worksheets` collecte dans `Workbook` Permet d'accéder à chaque feuille de calcul par index. Ici, nous prenons la première feuille pour commencer à définir les dimensions de la page.
## Étape 3 : définissez le format du papier sur A2 et affichez les dimensions
Maintenant que nous avons accès à notre feuille de calcul, définissons le format de papier sur A2. Ce réglage permet de formater la page avant de l'imprimer ou de l'exporter. Une fois le format défini, nous imprimerons les dimensions de la page en pouces.
```csharp
sheet.PageSetup.PaperSize = PaperSizeType.PaperA2;
Console.WriteLine("PaperA2: " + sheet.PageSetup.PaperWidth + "x" + sheet.PageSetup.PaperHeight);
```
Ici, nous changeons le `PaperSize` propriété à `PaperA2`. Après avoir défini la taille, `PageSetup.PaperWidth` et `PageSetup.PaperHeight` Récupérer la largeur et la hauteur de la feuille en pouces. Cela nous donne un aperçu rapide des dimensions de la page.
## Étape 4 : définissez le format du papier sur A3 et affichez les dimensions
En suivant les mêmes étapes que précédemment, ajustons les dimensions de la page au format A3. Ce changement est utile pour des impressions légèrement plus grandes ou pour insérer davantage de contenu sur une page.
```csharp
sheet.PageSetup.PaperSize = PaperSizeType.PaperA3;
Console.WriteLine("PaperA3: " + sheet.PageSetup.PaperWidth + "x" + sheet.PageSetup.PaperHeight);
```
Le format A3 est deux fois plus grand que le format A4, ce qui en fait un choix idéal pour les grands tableaux ou les graphiques détaillés. Changer le format du papier permet d'adapter la mise en page de la feuille de calcul.
## Étape 5 : définissez le format du papier sur A4 et affichez les dimensions
Définissons maintenant le format de papier sur A4. C'est le format de page le plus couramment utilisé pour l'impression de documents. Nous afficherons les dimensions mises à jour ultérieurement.
```csharp
sheet.PageSetup.PaperSize = PaperSizeType.PaperA4;
Console.WriteLine("PaperA4: " + sheet.PageSetup.PaperWidth + "x" + sheet.PageSetup.PaperHeight);
```
Si votre document cible est un format standard, le format A4 est généralement le plus adapté. Connaître les dimensions peut vous aider à ajuster la mise en page du contenu et à éviter les problèmes d'impression.
## Étape 6 : définissez le format du papier sur Lettre et affichez les dimensions.
Enfin, nous allons définir le format du papier au format Lettre, couramment utilisé en Amérique du Nord. Imprimons les dimensions une dernière fois.
```csharp
sheet.PageSetup.PaperSize = PaperSizeType.PaperLetter;
Console.WriteLine("PaperLetter: " + sheet.PageSetup.PaperWidth + "x" + sheet.PageSetup.PaperHeight);
```
Le format Lettre est largement utilisé pour les documents en Amérique du Nord. La définition de ce format est donc utile lors de la collaboration avec des équipes ou des clients basés dans ce pays.
## Conclusion
Dans ce tutoriel, nous avons expliqué comment définir et récupérer les dimensions de page pour différents formats de papier à l'aide d'Aspose.Cells pour .NET. En configurant des formats de page comme A2, A3, A4 et Lettre, vous pouvez formater des feuilles de calcul Excel pour répondre à vos besoins d'impression et de mise en page. Ce contrôle des dimensions de page est particulièrement utile pour les rapports et présentations professionnels, car il garantit que votre contenu s'adapte parfaitement à chaque format de page.
## FAQ
### Comment puis-je modifier l'orientation de la page dans Aspose.Cells ?  
Vous pouvez modifier l'orientation à l'aide du `PageSetup.Orientation` propriété, en la définissant soit sur `PageOrientationType.Poutrait` or `PageOrientationType.Landscape`.
### Puis-je définir des dimensions de page personnalisées dans Aspose.Cells ?  
Oui, vous pouvez définir des dimensions de page personnalisées en ajustant les marges et les options de mise à l'échelle sous `PageSetup` pour plus de contrôle.
### Quelle est la taille de papier par défaut dans Aspose.Cells ?  
Le format de papier par défaut est généralement le A4. Cependant, ce format peut dépendre des paramètres régionaux et être ajusté selon les besoins.
### Est-il possible de prévisualiser les mises en page dans Aspose.Cells ?  
Bien qu'Aspose.Cells n'offre pas d'aperçu graphique, vous pouvez configurer des mises en page par programmation et utiliser des aperçus avant impression dans Excel.
### Comment installer Aspose.Cells pour .NET ?  
Vous pouvez installer Aspose.Cells à l'aide du gestionnaire de packages NuGet dans Visual Studio ou télécharger la DLL à partir du [Page de téléchargement d'Aspose.Cells](https://releases.aspose.com/cells/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}