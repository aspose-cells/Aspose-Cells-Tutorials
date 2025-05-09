---
"description": "Découvrez comment placer des formes au premier plan ou en arrière-plan dans Excel avec Aspose.Cells pour .NET. Ce guide propose un tutoriel étape par étape avec des conseils."
"linktitle": "Envoyer la forme avant ou arrière dans Excel"
"second_title": "API de traitement Excel Aspose.Cells .NET"
"title": "Envoyer la forme avant ou arrière dans Excel"
"url": "/fr/net/excel-shape-text-modifications/send-shape-front-back-excel/"
"weight": 16
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Envoyer la forme avant ou arrière dans Excel

## Introduction
Lorsque vous travaillez avec des fichiers Excel, vous avez peut-être besoin de mieux contrôler les éléments visuels de votre feuille de calcul. Les formes, comme les images et les graphiques, peuvent améliorer la présentation de vos données. Mais que se passe-t-il lorsque ces formes se chevauchent ou doivent être réorganisées ? C'est là qu'Aspose.Cells pour .NET prend tout son sens. Dans ce tutoriel, nous vous expliquerons comment manipuler des formes dans une feuille de calcul Excel, en les plaçant au premier plan ou au second plan. Si vous êtes prêt à améliorer votre maîtrise d'Excel, c'est parti !
## Prérequis
Avant de commencer, vous devrez mettre en place quelques éléments :
1. Installation de la bibliothèque Aspose.Cells : Assurez-vous d'avoir installé la bibliothèque Aspose.Cells pour .NET. Vous pouvez la trouver. [ici](https://releases.aspose.com/cells/net/).
2. Environnement de développement : assurez-vous d’avoir un environnement de développement configuré avec la prise en charge .NET, tel que Visual Studio.
3. Connaissances de base de C# : la familiarité avec la programmation C# vous aidera à mieux comprendre les extraits de code.
Bien, vous avez coché toutes les cases de la liste des prérequis ? Super ! Passons à la partie amusante : écrire du code !
## Importer des packages
Avant de passer au codage proprement dit, importons les packages nécessaires. Ajoutez simplement la directive using suivante en haut de votre fichier C# :
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System;
```
Ces espaces de noms sont essentiels car ils contiennent les classes et les méthodes que nous utiliserons pour manipuler les fichiers et les formes Excel.
## Étape 1 : Définissez vos chemins de fichiers
Dans cette première étape, nous devons définir les répertoires source et de sortie. C'est là que se trouve votre fichier Excel et que vous souhaitez enregistrer le fichier modifié.
```csharp
//Répertoire source
string sourceDir = "Your Document Directory";
//Répertoire de sortie
string outputDir = "Your Document Directory";
```
Remplacer `"Your Document Directory"` avec le chemin réel où vos fichiers Excel sont stockés.
## Étape 2 : Charger le classeur
Maintenant que nos répertoires sont définis, chargeons le classeur (le fichier Excel) qui contient les formes que nous voulons manipuler.
```csharp
//Charger le fichier Excel source
Workbook wb = new Workbook(sourceDir + "sampleToFrontOrBack.xlsx");
```
Cette ligne de code initialise un nouveau `Workbook` objet, chargeant le fichier Excel spécifié en mémoire afin que nous puissions travailler avec lui.
## Étape 3 : Accéder à la feuille de travail 
Ensuite, nous devons accéder à la feuille de calcul contenant nos formes. Pour cet exemple, nous utiliserons la première feuille de calcul.
```csharp
//Accéder à la première feuille de calcul
Worksheet ws = wb.Worksheets[0];
```
En référençant `Worksheets[0]`Nous ciblons la première feuille de notre classeur. Si vos formes se trouvent sur une autre feuille, ajustez l'index en conséquence.
## Étape 4 : Accéder aux formes
Avec l'accès à la feuille de calcul prêt, récupérons les formes qui nous intéressent. Pour cet exemple, nous accéderons aux première et quatrième formes.
```csharp
//Accéder à la première et à la quatrième forme
Shape sh1 = ws.Shapes[0];
Shape sh4 = ws.Shapes[3];
```
Ces lignes obtiennent les formes spécifiques de la feuille de calcul en fonction de leur index.
## Étape 5 : Imprimer la position des formes dans l'ordre Z
Avant de déplacer des formes, imprimons leur position actuelle selon l'ordre Z. Cela nous permet de suivre leur positionnement avant toute modification.
```csharp
//Imprimer la position de l'ordre Z de la forme
Console.WriteLine("Z-Order Shape 1: " + sh1.ZOrderPosition);
```
En appelant `ZOrderPosition`, nous pouvons voir où chaque forme se trouve dans l'ordre de dessin.
## Étape 6 : Envoyez la première forme vers l'avant
Passons maintenant à l'action ! Envoyons la première forme au début de l'ordre Z.
```csharp
//Envoyez cette forme vers l'avant
sh1.ToFrontOrBack(2);
```
En passant `2` à `ToFrontOrBack`, nous demandons à Aspose.Cells de mettre cette forme au premier plan. 
## Étape 7 : Imprimer la position de l'ordre Z de la deuxième forme
Avant d'envoyer la deuxième forme à l'arrière, vérifions où elle est positionnée.
```csharp
//Imprimer la position de l'ordre Z de la forme
Console.WriteLine("Z-Order Shape 4: " + sh4.ZOrderPosition);
```
Cela nous donne un aperçu de la position de la quatrième forme avant d’apporter des modifications.
## Étape 8 : Envoyez la quatrième forme à l'arrière
Enfin, nous allons envoyer la quatrième forme à l’arrière de la pile Z-Order.
```csharp
//Envoyer cette forme à l'arrière
sh4.ToFrontOrBack(-2);
```
En utilisant `-2` car le paramètre envoie la forme vers l'arrière de la pile, garantissant qu'elle n'obstruera pas d'autres formes ou textes.
## Étape 9 : Enregistrer le classeur 
La dernière étape consiste à enregistrer votre classeur avec les formes nouvellement positionnées.
```csharp
//Enregistrer le fichier Excel de sortie
wb.Save(outputDir + "outputToFrontOrBack.xlsx");
```
Cette commande enregistre le classeur modifié dans le répertoire de sortie spécifié.
## Étape 10 : Message de confirmation
Enfin, fournissons une simple confirmation pour nous faire savoir que notre tâche s'est terminée avec succès.
```csharp
Console.WriteLine("SendShapeFrontOrBackInWorksheet executed successfully.\r\n");
```
Et cela conclut le code de notre tutoriel !
## Conclusion
Manipuler des formes dans Excel avec Aspose.Cells pour .NET est non seulement simple, mais aussi puissant. En suivant ce guide, vous devriez désormais pouvoir placer des formes au premier plan ou en arrière-plan facilement, pour un meilleur contrôle de vos présentations Excel. Grâce à ces outils, vous êtes prêt à améliorer l'esthétique de vos feuilles de calcul.
## FAQ
### De quel langage de programmation ai-je besoin pour Aspose.Cells ?  
Vous devez utiliser C# ou tout autre langage pris en charge par .NET pour travailler avec Aspose.Cells.
### Puis-je essayer Aspose.Cells gratuitement ?  
Oui, vous pouvez commencer avec un essai gratuit d'Aspose.Cells [ici](https://releases.aspose.com/).
### Quels types de formes puis-je manipuler dans Excel ?  
Vous pouvez manipuler diverses formes telles que des rectangles, des cercles, des lignes et des images.
### Comment puis-je obtenir de l'aide pour Aspose.Cells ?  
Vous pouvez visiter leur forum communautaire pour toute assistance ou question [ici](https://forum.aspose.com/c/cells/9).
### Existe-t-il une licence temporaire disponible pour Aspose.Cells ?  
Oui, vous pouvez demander une licence temporaire [ici](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}