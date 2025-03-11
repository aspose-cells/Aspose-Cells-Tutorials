---
title: Envoyer la forme vers l'avant ou vers l'arrière dans Excel
linktitle: Envoyer la forme vers l'avant ou vers l'arrière dans Excel
second_title: API de traitement Excel Aspose.Cells .NET
description: Découvrez comment envoyer des formes vers l'avant ou vers l'arrière dans Excel à l'aide d'Aspose.Cells pour .NET. Ce guide fournit un didacticiel étape par étape avec des conseils.
weight: 16
url: /fr/net/excel-shape-text-modifications/send-shape-front-back-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Envoyer la forme vers l'avant ou vers l'arrière dans Excel

## Introduction
Lorsque vous travaillez avec des fichiers Excel, vous pouvez avoir besoin de plus de contrôle sur les éléments visuels de votre feuille de calcul. Les formes, comme les images et les graphiques, peuvent améliorer la présentation de vos données. Mais que se passe-t-il lorsque ces formes se chevauchent ou doivent être réorganisées ? C'est là qu'Aspose.Cells pour .NET brille. Dans ce didacticiel, nous vous guiderons à travers les étapes de manipulation des formes dans une feuille de calcul Excel, en particulier en envoyant des formes au premier plan ou à l'arrière-plan d'autres formes. Si vous êtes prêt à améliorer votre jeu Excel, plongeons-nous directement dans le vif du sujet !
## Prérequis
Avant de commencer, vous devez mettre en place quelques éléments :
1.  Installation de la bibliothèque Aspose.Cells : Assurez-vous que la bibliothèque Aspose.Cells est installée pour .NET. Vous pouvez la trouver[ici](https://releases.aspose.com/cells/net/).
2. Environnement de développement : assurez-vous que vous disposez d’un environnement de développement configuré avec la prise en charge .NET, tel que Visual Studio.
3. Connaissances de base de C# : la familiarité avec la programmation C# vous aidera à mieux comprendre les extraits de code.
Très bien, vous avez coché toutes les cases de la liste des prérequis ? Super ! Passons à la partie amusante : écrire du code !
## Paquets d'importation
Avant de nous plonger dans le codage proprement dit, importons les packages nécessaires. Ajoutez simplement la directive using suivante en haut de votre fichier C# :
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System;
```
Ces espaces de noms sont cruciaux car ils contiennent les classes et les méthodes que nous utiliserons pour manipuler les fichiers et les formes Excel.
## Étape 1 : définissez vos chemins d’accès aux fichiers
Dans cette première étape, nous devons établir les répertoires source et de sortie. C'est là que se trouve votre fichier Excel et où vous souhaitez enregistrer le fichier modifié.
```csharp
//Répertoire des sources
string sourceDir = "Your Document Directory";
//Répertoire de sortie
string outputDir = "Your Document Directory";
```
 Remplacer`"Your Document Directory"` avec le chemin réel où vos fichiers Excel sont stockés.
## Étape 2 : charger le classeur
Maintenant que nos répertoires sont définis, chargeons le classeur (le fichier Excel) qui contient les formes que nous souhaitons manipuler.
```csharp
//Charger le fichier source Excel
Workbook wb = new Workbook(sourceDir + "sampleToFrontOrBack.xlsx");
```
 Cette ligne de code initialise une nouvelle`Workbook` objet, chargeant le fichier Excel spécifié en mémoire afin que nous puissions travailler avec lui.
## Étape 3 : Accéder à la feuille de travail 
Ensuite, nous devons accéder à la feuille de calcul spécifique où se trouvent nos formes. Pour cet exemple, nous utiliserons la première feuille de calcul.
```csharp
//Accéder à la première feuille de calcul
Worksheet ws = wb.Worksheets[0];
```
 En référençant`Worksheets[0]`, nous ciblons la première feuille de notre classeur. Si vos formes se trouvent sur une autre feuille, ajustez l'index en conséquence.
## Étape 4 : Accéder aux formes
Maintenant que nous avons accès à la feuille de calcul, prenons les formes qui nous intéressent. Pour cet exemple, nous accéderons aux première et quatrième formes.
```csharp
//Accéder à la première et à la quatrième forme
Shape sh1 = ws.Shapes[0];
Shape sh4 = ws.Shapes[3];
```
Ces lignes obtiennent les formes spécifiques de la feuille de calcul en fonction de leur index.
## Étape 5 : Imprimer la position de l'ordre Z des formes
Avant de déplacer des formes, imprimons leur position actuelle dans l'ordre Z. Cela nous aide à suivre leur positionnement avant d'effectuer des modifications.
```csharp
//Imprimer la position de l'ordre Z de la forme
Console.WriteLine("Z-Order Shape 1: " + sh1.ZOrderPosition);
```
 En appelant`ZOrderPosition`, nous pouvons voir où chaque forme se trouve dans l'ordre de dessin.
## Étape 6 : Envoyez la première forme vers l'avant
Il est maintenant temps de passer à l'action ! Envoyons la première forme à l'avant de l'ordre Z.
```csharp
//Envoyez cette forme vers l'avant
sh1.ToFrontOrBack(2);
```
 En passant`2` à`ToFrontOrBack`, nous demandons à Aspose.Cells de placer cette forme au premier plan. 
## Étape 7 : Imprimez la position de l'ordre Z de la deuxième forme
Avant d'envoyer la deuxième forme à l'arrière, vérifions où elle est positionnée.
```csharp
//Imprimer la position de l'ordre Z de la forme
Console.WriteLine("Z-Order Shape 4: " + sh4.ZOrderPosition);
```
Cela nous donne un aperçu de la position de la quatrième forme avant d’effectuer des modifications.
## Étape 8 : Envoyez la quatrième forme à l'arrière
Enfin, nous allons envoyer la quatrième forme à l’arrière de la pile Z-Order.
```csharp
//Envoyer cette forme à l'arrière
sh4.ToFrontOrBack(-2);
```
 En utilisant`-2` car le paramètre envoie la forme vers l'arrière de la pile, garantissant qu'elle n'obstruera pas d'autres formes ou textes.
## Étape 9 : Enregistrer le classeur 
La dernière étape consiste à enregistrer votre classeur avec les formes nouvellement positionnées.
```csharp
//Enregistrer le fichier Excel de sortie
wb.Save(outputDir + "outputToFrontOrBack.xlsx");
```
Cette commande enregistre le classeur modifié dans le répertoire de sortie spécifié.
## Étape 10 : Message de confirmation
Enfin, fournissons une simple confirmation pour nous faire savoir que notre tâche s'est terminée avec succès.
```csharp
Console.WriteLine("SendShapeFrontOrBackInWorksheet executed successfully.\r\n");
```
Et cela conclut le code de notre tutoriel !
## Conclusion
La manipulation de formes dans Excel à l'aide d'Aspose.Cells pour .NET est non seulement simple mais également puissante. En suivant ce guide, vous devriez maintenant pouvoir envoyer des formes vers l'avant ou vers l'arrière en toute simplicité, ce qui vous permettra de mieux contrôler vos présentations Excel. Avec ces outils à votre disposition, vous êtes prêt à améliorer l'attrait visuel de vos feuilles de calcul.
## FAQ
### De quel langage de programmation ai-je besoin pour Aspose.Cells ?  
Vous devez utiliser C# ou tout autre langage pris en charge par .NET pour travailler avec Aspose.Cells.
### Puis-je essayer Aspose.Cells gratuitement ?  
 Oui, vous pouvez commencer avec un essai gratuit d'Aspose.Cells[ici](https://releases.aspose.com/).
### Quels types de formes puis-je manipuler dans Excel ?  
Vous pouvez manipuler diverses formes telles que des rectangles, des cercles, des lignes et des images.
### Comment puis-je obtenir de l'aide pour Aspose.Cells ?  
 Vous pouvez visiter leur forum communautaire pour toute assistance ou question[ici](https://forum.aspose.com/c/cells/9).
### Existe-t-il une licence temporaire disponible pour Aspose.Cells ?  
 Oui, vous pouvez demander une licence temporaire[ici](https://purchase.aspose.com/temporary-license/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
