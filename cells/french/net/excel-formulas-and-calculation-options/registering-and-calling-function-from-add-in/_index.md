---
title: Enregistrement et appel d'une fonction à partir d'un module complémentaire dans Excel
linktitle: Enregistrement et appel d'une fonction à partir d'un module complémentaire dans Excel
second_title: API de traitement Excel Aspose.Cells .NET
description: Découvrez comment enregistrer et appeler des fonctions à partir de modules complémentaires dans Excel à l'aide d'Aspose.Cells pour .NET avec notre didacticiel simple étape par étape.
weight: 20
url: /fr/net/excel-formulas-and-calculation-options/registering-and-calling-function-from-add-in/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Enregistrement et appel d'une fonction à partir d'un module complémentaire dans Excel

## Introduction
Vous souhaitez améliorer votre expérience Excel en appelant des fonctions à partir d'un module complémentaire ? Si oui, vous êtes au bon endroit ! Les modules complémentaires Excel sont comme les fées marraines des feuilles de calcul ; ils étendent les fonctionnalités comme par magie, vous offrant un tas de nouveaux outils à portée de main. Et avec Aspose.Cells pour .NET, il est plus facile que jamais d'enregistrer et d'utiliser ces fonctions complémentaires. 
Dans ce guide, je vais vous expliquer le processus d'enregistrement et d'appel d'une fonction à partir d'un module complémentaire Excel à l'aide d'Aspose.Cells pour .NET. Nous allons tout détailler étape par étape, pour que vous vous sentiez comme un pro en un rien de temps !
## Prérequis
Avant de nous plonger dans la magie du codage, voyons ce que vous devez mettre en place :
1. Visual Studio : assurez-vous que Visual Studio est installé sur votre ordinateur. C'est ici que nous écrirons et exécuterons notre code.
2.  Bibliothèque Aspose.Cells : vous aurez besoin de la bibliothèque Aspose.Cells installée. Vous pouvez la récupérer à partir de leur[page de téléchargement](https://releases.aspose.com/cells/net/).
3. Connaissances de base de C# : une petite compréhension de C# vous sera d'une grande aide ; cela vous aidera à suivre le cours sans problème.
4.  Compléments Excel : vous devez disposer d'un fichier de complément (comme`.xlam`) qui contient les fonctions que vous souhaitez enregistrer et utiliser.
5.  Un exemple de module complémentaire Excel : pour ce didacticiel, nous utiliserons un module complémentaire Excel nommé`TESTUDF.xlam`Assurez-vous donc d’avoir ceci à votre disposition !
Maintenant que vous êtes prêt, retroussons nos manches et passons au codage !
## Importation de paquets
Pour commencer, vous devez importer certains espaces de noms essentiels en haut de votre fichier C#. Voici ce que vous devez inclure :
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Ces espaces de noms vous permettront d'accéder aux classes et méthodes que nous utiliserons dans ce tutoriel.
Décomposons cela en étapes faciles à gérer. À la fin de ce guide, vous aurez une solide compréhension de la manière d'enregistrer des fonctions complémentaires et de les utiliser dans vos classeurs Excel.
## Étape 1 : Configurez vos répertoires source et de sortie
Avant de pouvoir enregistrer votre module complémentaire, vous devez définir où se trouveront votre module complémentaire et vos fichiers de sortie.
```csharp
// Répertoire des sources
string sourceDir = "Your Document Directory";
// Répertoire de sortie
string outputDir = "Your Document Directory";
```
 Remplacer`"Your Document Directory"` avec le chemin réel où votre`.xlam` Le fichier et les fichiers de sortie seront enregistrés. C'est comme préparer le terrain avant le début du spectacle.
## Étape 2 : Créer un classeur vide
Ensuite, vous souhaiterez créer un classeur vierge dans lequel nous pourrons jouer avec les fonctions complémentaires.
```csharp
// Créer un classeur vide
Workbook workbook = new Workbook();
```
Cette ligne de code crée un nouveau classeur qui nous servira de terrain de jeu. Considérez-le comme une nouvelle toile, prête à recevoir vos coups de pinceau créatifs.
## Étape 3 : Enregistrer la fonction complémentaire
Maintenant, passons au vif du sujet ! Il est temps d'enregistrer votre fonction complémentaire. Voici comment procéder :
```csharp
// Enregistrer le module complémentaire prenant en charge les macros avec le nom de la fonction
int id = workbook.Worksheets.RegisterAddInFunction(sourceDir + @"TESTUDF.xlam", "TEST_UDF", false);
```
 Cette ligne enregistre la fonction complémentaire nommée`TEST_UDF` trouvé dans le`TESTUDF.xlam` fichier complémentaire. Le`false`paramètre signifie que le module complémentaire n'est pas chargé en mode « isolé ». 
## Étape 4 : Enregistrer des fonctions supplémentaires (le cas échéant)
Si vous avez plusieurs fonctions enregistrées dans le même fichier complémentaire, vous pouvez également les enregistrer !
```csharp
// Enregistrer plus de fonctions dans le fichier (le cas échéant)
workbook.Worksheets.RegisterAddInFunction(id, "TEST_UDF1");
```
Ici, vous pouvez voir à quel point il est facile d'ajouter d'autres fonctions à partir du même module complémentaire. Il suffit de les empiler comme des blocs de construction !
## Étape 5 : Accéder à la feuille de travail
Passons maintenant à la feuille de calcul où nous utiliserons notre fonction. 
```csharp
// Accéder à la première feuille de calcul
Worksheet worksheet = workbook.Worksheets[0];
```
Nous accédons à la première feuille de calcul du classeur pour y placer notre formule. C'est comme ouvrir la porte de la pièce où se déroule le plaisir.
## Étape 6 : Accéder à une cellule spécifique
Ensuite, nous devons choisir la cellule que nous voulons utiliser pour notre formule. 
```csharp
// Accéder à la première cellule
var cell = worksheet.Cells["A1"];
```
Ici, nous pointons vers la cellule A1. C'est là que nous allons déposer notre formule magique. Vous pouvez considérer cela comme épingler une cible sur votre carte au trésor !
## Étape 7 : Définir la formule
Il est maintenant temps de procéder au grand dévoilement ! Définissons la formule qui appelle notre fonction enregistrée.
```csharp
// Définir le nom de la formule présente dans le complément
cell.Formula = "=TEST_UDF()";
```
Avec cette ligne, nous demandons à Excel d'utiliser notre fonction dans la cellule A1. C'est comme si nous donnions une commande à Excel et lui disions : « Hé, fais ça ! »
## Étape 8 : Enregistrer le classeur
Dernier point, mais non le moindre, il est temps de sauver notre chef-d’œuvre.
```csharp
// Enregistrez le classeur au format de sortie XLSX.
workbook.Save(outputDir + @"test_udf.xlsx", Aspose.Cells.SaveFormat.Xlsx);
```
Ici, nous enregistrons notre classeur sous forme de fichier XLSX. Cette dernière étape revient à encadrer votre tableau et à vous préparer à le mettre en valeur !
## Étape 9 : Confirmer l'exécution
Enfin, terminons le tout en imprimant un message de réussite sur la console.
```csharp
Console.WriteLine("RegisterAndCallFuncFromAddIn executed successfully.");
```
Cette ligne fait office de drapeau de victoire. C'est une petite attention sympathique qui confirme que tout s'est bien passé.
## Conclusion 
Et voilà ! Vous avez non seulement appris à enregistrer et à appeler des fonctions à partir de modules complémentaires Excel à l'aide d'Aspose.Cells pour .NET, mais vous avez également acquis une compréhension plus approfondie de chaque étape impliquée. La vie est un peu plus facile maintenant, n'est-ce pas ? Alors pourquoi ne pas l'essayer par vous-même ? Plongez dans ces modules complémentaires Excel et donnez à vos feuilles de calcul un nouveau niveau d'interactivité et de fonctionnalité.
## FAQ
### Qu'est-ce qu'un module complémentaire Excel ?  
Un module complémentaire Excel est un programme qui ajoute des fonctionnalités, des fonctions ou des commandes personnalisées à Excel, permettant aux utilisateurs d'étendre ses capacités.
### Puis-je utiliser Aspose.Cells sans l'installer localement ?  
Non, vous devez installer la bibliothèque Aspose.Cells pour l'utiliser dans vos applications .NET.
### Comment obtenir une licence temporaire pour Aspose.Cells ?  
 Vous pouvez visiter leur[page de licence temporaire](https://purchase.aspose.com/temporary-license/) pour plus d'informations.
### Est-il possible d'appeler plusieurs fonctions à partir d'un seul module complémentaire ?  
 Oui ! Vous pouvez enregistrer plusieurs fonctions à partir du même fichier complémentaire à l'aide de`RegisterAddInFunction` méthode.
### Où puis-je trouver plus de documentation sur Aspose.Cells ?  
 Vous pouvez explorer leur documentation complète sur le site[ici](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
