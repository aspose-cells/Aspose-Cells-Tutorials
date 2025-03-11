---
title: Extraire le texte du type d'engrenage Smart Art dans Excel
linktitle: Extraire le texte du type d'engrenage Smart Art dans Excel
second_title: API de traitement Excel Aspose.Cells .NET
description: Découvrez comment extraire du texte d'un SmartArt de type engrenage dans Excel à l'aide d'Aspose.Cells pour .NET. Guide étape par étape et exemple de code inclus.
weight: 10
url: /fr/net/excel-shape-text-modifications/extract-text-gear-smart-art-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extraire le texte du type d'engrenage Smart Art dans Excel

## Introduction
Lorsque vous travaillez avec Excel, vous pouvez rencontrer des graphiques SmartArt qui vous aident à transmettre vos messages de manière visuellement attrayante. Parmi ces graphiques, le SmartArt de type engrenage est un favori pour ses flux hiérarchiques et directionnels, souvent utilisés dans la gestion de projet ou la modélisation de systèmes. Mais que faire si vous devez extraire du texte de ces formes par programmation ? C'est là qu'Aspose.Cells pour .NET s'avère utile ! Dans cet article de blog, nous vous expliquerons étape par étape comment extraire du texte à partir de formes SmartArt de type engrenage dans Excel à l'aide d'Aspose.Cells pour .NET.
## Prérequis
Avant de commencer, vous devez avoir mis en place certains prérequis essentiels. Ne vous inquiétez pas, c'est simple et je vais vous guider.
### Environnement .NET
Assurez-vous que vous disposez d'un environnement de développement .NET configuré sur votre ordinateur. Il peut s'agir de Visual Studio ou de tout autre IDE de votre choix prenant en charge le développement .NET.
### Aspose.Cells pour .NET
 Ensuite, vous devrez installer la bibliothèque Aspose.Cells. C'est la centrale qui vous permettra de manipuler les fichiers Excel de manière transparente. Vous pouvez la télécharger à partir du[Page de sortie d'Aspose](https://releases.aspose.com/cells/net/) . Si vous souhaitez l'explorer en premier, profitez de la[essai gratuit](https://releases.aspose.com/).
### Connaissances de base de C#
Une compréhension de base de la programmation C# est exactement ce dont vous avez besoin pour suivre ce tutoriel. Si vous débutez, ne vous inquiétez pas, je concevrai les étapes de manière à ce qu'elles soient aussi conviviales que possible pour les débutants.
### Exemple de fichier Excel
Pour ce tutoriel, vous aurez également besoin d'un exemple de fichier Excel contenant des formes SmartArt de type engrenage. Vous pouvez facilement en créer un ou trouver un modèle en ligne. Assurez-vous simplement que le SmartArt comprend au moins une forme de type engrenage.
## Paquets d'importation
Pour commencer à coder, vous devez importer les packages nécessaires. Voici comment procéder :
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
// Répertoire des sources
string sourceDir = "Your Document Directory";
```
 Assurez-vous de remplacer`"Your Document Directory"` avec le chemin réel vers votre fichier Excel.
## Étape 2 : charger le classeur Excel
Ensuite, nous allons charger le classeur Excel. Voici comment nous pouvons accéder à son contenu :
```csharp
// Charger un exemple de fichier Excel contenant une forme d'art intelligente de type engrenage.
Workbook wb = new Workbook(sourceDir + "sampleExtractTextFromGearTypeSmartArtShape.xlsx");
```
Cet élément chargera votre exemple de classeur Excel.
## Étape 3 : Accéder à la première feuille de travail
Maintenant que nous avons chargé le classeur, accédons à la première feuille de calcul où existe notre SmartArt :
```csharp
// Accéder à la première feuille de calcul.
Worksheet ws = wb.Worksheets[0];
```
Cela récupère la première feuille de calcul pour une manipulation ultérieure.
## Étape 4 : Accéder à la première forme
Ensuite, nous devons accéder à la première forme de notre feuille de calcul. En procédant ainsi, nous pouvons parcourir nos graphiques SmartArt :
```csharp
// Accéder à la première forme.
Aspose.Cells.Drawing.Shape sh = ws.Shapes[0];
```
Ici, nous nous concentrons sur la première forme, que nous supposons être le SmartArt dont nous avons besoin.
## Étape 5 : Obtenir la forme du groupe
Une fois que nous avons notre forme, il est temps d'obtenir le résultat de notre représentation SmartArt :
```csharp
// Obtenez le résultat de la forme d'art intelligente de type engrenage sous la forme d'une forme de groupe.
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
Enfin, nous pouvons parcourir notre tableau de formes et extraire le texte de n’importe quelle forme de type engrenage :
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
## Étape 8 : Confirmation de l'exécution
Enfin, vous souhaiterez peut-être ajouter un message de confirmation une fois le processus terminé avec succès :
```csharp
Console.WriteLine("ExtractTextFromGearTypeSmartArtShape executed successfully.");
```
Avec cela, votre extraction est terminée et vous devriez voir votre sortie texte dans la console !
## Conclusion
 Félicitations ! Vous venez d'apprendre à extraire du texte à partir de formes SmartArt de type engrenage dans Excel à l'aide d'Aspose.Cells pour .NET. Cette technique pratique ouvre la voie à l'automatisation des rapports ou de la documentation qui repose sur la représentation visuelle des données. Que vous soyez un développeur chevronné ou que vous débutiez, le contrôle et l'extraction d'informations à partir de SmartArt peuvent rationaliser votre flux de travail et vous rendre plus efficace. N'oubliez pas d'explorer les détails[Documentation sur Aspose.Cells](https://reference.aspose.com/cells/net/) pour des capacités supplémentaires.
## FAQ
### Qu'est-ce qu'Aspose.Cells ?
Aspose.Cells est une bibliothèque .NET qui permet aux développeurs de créer et de manipuler facilement des fichiers Excel.
### Puis-je utiliser Aspose.Cells avec d’autres langages ?
Oui ! Aspose.Cells est disponible dans plusieurs langages de programmation, dont Java et Python.
### Dois-je acheter Aspose.Cells pour .NET ?
 Aspose.Cells propose un essai gratuit, mais pour une utilisation prolongée, un achat est nécessaire. Vous pouvez trouver des options d'achat[ici](https://purchase.aspose.com/buy).
### Existe-t-il un support disponible pour les utilisateurs d'Aspose.Cells ?
 Absolument ! Vous pouvez trouver du soutien communautaire sur le[Forum Aspose.Cells](https://forum.aspose.com/c/cells/9).
### Puis-je extraire d’autres types de SmartArt en utilisant cette méthode ?
Oui, avec de légères modifications, vous pouvez extraire du texte de diverses formes SmartArt en modifiant les conditions de votre code.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
