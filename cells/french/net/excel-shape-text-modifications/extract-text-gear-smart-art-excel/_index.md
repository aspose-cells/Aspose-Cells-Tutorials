---
"description": "Apprenez à extraire du texte d'un SmartArt de type engrenage dans Excel avec Aspose.Cells pour .NET. Guide étape par étape et exemple de code inclus."
"linktitle": "Extraire du texte à partir d'un Smart Art de type engrenage dans Excel"
"second_title": "API de traitement Excel Aspose.Cells .NET"
"title": "Extraire du texte à partir d'un Smart Art de type engrenage dans Excel"
"url": "/fr/net/excel-shape-text-modifications/extract-text-gear-smart-art-excel/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Extraire du texte à partir d'un Smart Art de type engrenage dans Excel

## Introduction
Lorsque vous travaillez avec Excel, vous pouvez rencontrer des graphiques SmartArt qui vous aident à transmettre vos messages de manière visuellement attrayante. Parmi ces graphiques, les SmartArt de type engrenage sont très appréciés pour leurs flux hiérarchiques et directionnels, souvent utilisés en gestion de projet ou en modélisation de systèmes. Mais que faire si vous devez extraire du texte de ces formes par programmation ? C'est là qu'Aspose.Cells pour .NET entre en jeu ! Dans cet article de blog, nous vous expliquerons étape par étape comment extraire du texte de formes SmartArt de type engrenage dans Excel à l'aide d'Aspose.Cells pour .NET.
## Prérequis
Avant de commencer, voici quelques prérequis essentiels. Pas d'inquiétude, c'est simple et je vais vous guider.
### Environnement .NET
Assurez-vous d'avoir un environnement de développement .NET configuré sur votre ordinateur. Il peut s'agir de Visual Studio ou de tout autre IDE de votre choix prenant en charge le développement .NET.
### Aspose.Cells pour .NET
Ensuite, vous devrez installer la bibliothèque Aspose.Cells. C'est la solution idéale pour manipuler facilement vos fichiers Excel. Vous pouvez la télécharger depuis le site [Page des versions d'Aspose](https://releases.aspose.com/cells/net/). Si vous souhaitez l'explorer en premier, profitez de la [essai gratuit](https://releases.aspose.com/).
### Connaissances de base de C#
Une compréhension de base de la programmation C# est essentielle pour suivre ce tutoriel. Si vous débutez, pas de souci : les étapes seront conçues pour être aussi faciles à suivre que possible.
### Exemple de fichier Excel
Pour ce tutoriel, vous aurez également besoin d'un fichier Excel d'exemple contenant des formes SmartArt de type engrenage. Vous pouvez facilement en créer un ou trouver un modèle en ligne. Assurez-vous simplement que le SmartArt contient au moins une forme de type engrenage.
## Importer des packages
Pour commencer à coder, vous devrez importer les packages nécessaires. Voici comment procéder :
### Créer un nouveau projet
1. Ouvrez votre IDE .NET.
2. Créez un nouveau projet. Par exemple, sélectionnez « Application console » dans les options .NET.
3. Donnez un nom à votre projet et définissez le cadre souhaité. 
### Ajouter des références
Pour utiliser Aspose.Cells, vous devrez ajouter les références de bibliothèque à votre projet :
1. Cliquez avec le bouton droit sur le nom de votre projet dans l’Explorateur de solutions.
2. Choisissez « Gérer les packages NuGet ».
3. Recherchez « Aspose.Cells » et installez-le.
Une fois installé, vous êtes prêt à coder !
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Maintenant, décomposons le code que vous utiliserez pour extraire le texte. Nous procéderons étape par étape.
## Étape 1 : Configurer le répertoire source
Commencez par définir le répertoire où se trouve votre fichier Excel :
```csharp
// Répertoire source
string sourceDir = "Your Document Directory";
```
Assurez-vous de remplacer `"Your Document Directory"` avec le chemin réel vers votre fichier Excel.
## Étape 2 : Charger le classeur Excel
Nous allons ensuite charger le classeur Excel. Voici comment accéder à son contenu :
```csharp
// Charger un exemple de fichier Excel contenant une forme d'art intelligente de type engrenage.
Workbook wb = new Workbook(sourceDir + "sampleExtractTextFromGearTypeSmartArtShape.xlsx");
```
Cette pièce chargera votre exemple de classeur Excel.
## Étape 3 : Accéder à la première feuille de travail
Maintenant que nous avons chargé le classeur, accédons à la première feuille de calcul où se trouve notre SmartArt :
```csharp
// Accéder à la première feuille de travail.
Worksheet ws = wb.Worksheets[0];
```
Cela récupère la première feuille de calcul pour une manipulation ultérieure.
## Étape 4 : Accéder à la première forme
Ensuite, nous devons accéder à la première forme de notre feuille de calcul. Cela nous permettra de parcourir nos graphiques SmartArt :
```csharp
// Accéder à la première forme.
Aspose.Cells.Drawing.Shape sh = ws.Shapes[0];
```
Ici, nous nous concentrons sur la première forme, que nous supposons être le SmartArt dont nous avons besoin.
## Étape 5 : Obtenir la forme du groupe
Une fois que nous avons notre forme, il est temps d'obtenir le résultat de notre représentation SmartArt :
```csharp
// Obtenez le résultat de la forme d'art intelligent de type engrenage sous la forme d'une forme de groupe.
Aspose.Cells.Drawing.GroupShape gs = sh.GetResultOfSmartArt();
```
Cela récupère notre SmartArt de type engrenage sous forme de forme groupée.
## Étape 6 : Extraire les formes individuelles
Maintenant, extrayons les formes individuelles qui composent notre SmartArt :
```csharp
// Obtenez la liste des formes individuelles constituées de formes de groupe.
Aspose.Cells.Drawing.Shape[] shps = gs.GetGroupedShapes();
```
Ce tableau contiendra toutes les formes individuelles que nous devons parcourir.
## Étape 7 : Extraire et imprimer le texte
Enfin, nous pouvons parcourir notre tableau de formes et extraire le texte de n'importe quelle forme de type engrenage :
```csharp
// Extrayez le texte des formes de type engrenage et imprimez-les sur la console.
for (int i = 0; i < shps.Length; i++)
{
    Aspose.Cells.Drawing.Shape s = shps[i];
    if (s.Type == Aspose.Cells.Drawing.AutoShapeType.Gear9 || s.Type == Aspose.Cells.Drawing.AutoShapeType.Gear6)
    {
        Console.WriteLine("Gear Type Shape Text: " + s.Text);
    }
}
```
Dans cette boucle, nous vérifions le type de forme et imprimons le texte s'il s'agit d'une forme de type engrenage.
## Étape 8 : Confirmation d'exécution
Enfin, vous souhaiterez peut-être ajouter un message de confirmation une fois le processus terminé avec succès :
```csharp
Console.WriteLine("ExtractTextFromGearTypeSmartArtShape executed successfully.");
```
Avec cela, votre extraction est terminée et vous devriez voir votre sortie texte dans la console !
## Conclusion
Félicitations ! Vous venez d'apprendre à extraire du texte de formes SmartArt de type engrenage dans Excel avec Aspose.Cells pour .NET. Cette technique pratique ouvre la voie à l'automatisation des rapports et de la documentation qui reposent sur une représentation visuelle des données. Que vous soyez un développeur expérimenté ou débutant, contrôler et extraire des informations de SmartArt peut optimiser votre flux de travail et vous rendre plus efficace. N'oubliez pas d'explorer les détails. [Documentation d'Aspose.Cells](https://reference.aspose.com/cells/net/) pour des capacités supplémentaires.
## FAQ
### Qu'est-ce qu'Aspose.Cells ?
Aspose.Cells est une bibliothèque .NET qui permet aux développeurs de créer et de manipuler facilement des fichiers Excel.
### Puis-je utiliser Aspose.Cells avec d'autres langages ?
Oui ! Aspose.Cells est disponible dans plusieurs langages de programmation, notamment Java et Python.
### Dois-je acheter Aspose.Cells pour .NET ?
Aspose.Cells propose un essai gratuit, mais un achat est requis pour une utilisation prolongée. Vous trouverez des options d'achat. [ici](https://purchase.aspose.com/buy).
### Existe-t-il un support disponible pour les utilisateurs d'Aspose.Cells ?
Absolument ! Vous trouverez du soutien communautaire sur [Forum Aspose.Cells](https://forum.aspose.com/c/cells/9).
### Puis-je extraire d’autres types de SmartArt en utilisant cette méthode ?
Oui, avec de légères modifications, vous pouvez extraire du texte de diverses formes SmartArt en modifiant les conditions de votre code.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}