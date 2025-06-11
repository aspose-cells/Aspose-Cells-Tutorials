---
"description": "Apprenez à récupérer et à répertorier les polices à partir de feuilles de calcul Excel à l'aide d'Aspose.Cells pour .NET avec ce didacticiel facile à suivre."
"linktitle": "Obtenir la liste des polices utilisées dans la feuille de calcul"
"second_title": "API de traitement Excel Aspose.Cells .NET"
"title": "Obtenir la liste des polices utilisées dans la feuille de calcul"
"url": "/fr/net/working-with-fonts-in-spreadsheets/get-list-of-fonts-used-in-spreadsheet/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Obtenir la liste des polices utilisées dans la feuille de calcul

## Introduction
Vous est-il déjà arrivé de parcourir une feuille de calcul Excel en vous interrogeant sur les polices utilisées dans ses différentes cellules ? Vous avez peut-être retrouvé un vieux document et aimeriez connaître les choix typographiques effectués ? Eh bien, vous avez de la chance ! Avec Aspose.Cells pour .NET, c'est comme une boîte à outils qui vous permet de fouiller et de découvrir les secrets des polices cachées dans vos feuilles de calcul. Dans ce guide, nous vous expliquerons comment récupérer facilement la liste de toutes les polices utilisées dans un fichier Excel. Attachez vos ceintures et plongeons dans l'univers des feuilles de calcul !
## Prérequis
Avant de nous lancer dans le code, voici quelques éléments essentiels pour commencer. Pas d'inquiétude, c'est très simple. Voici une liste de ce dont vous avez besoin :
1. Visual Studio : Assurez-vous d'avoir installé Visual Studio sur votre ordinateur. C'est ici que nous écrirons notre code.
2. Aspose.Cells pour .NET : la bibliothèque Aspose.Cells est requise. Si vous ne l'avez pas encore téléchargée, vous pouvez la télécharger depuis le [site](https://releases.aspose.com/cells/net/).
3. Connaissances de base de C# : une petite compréhension de la programmation C# vous aidera certainement à naviguer facilement dans le code.
4. Exemple de fichier Excel : Vous aurez besoin d'un exemple de fichier Excel, comme « sampleGetFonts.xlsx », pour travailler. C'est ici que nous allons explorer les polices.
Une fois que vous avez tout réglé, vous êtes prêt à vous lancer dans le codage !
## Importer des packages
Pour commencer, importons les espaces de noms nécessaires. Dans .NET, importer des packages revient à inviter les bons invités : sans eux, tout ne fonctionnera pas correctement.
Voici comment importer Aspose.Cells :
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.IO;
```
Avec cette simple ligne, nous intégrons les fonctionnalités principales d'Aspose.Cells à notre projet. Passons maintenant au chargement du classeur.
## Étape 1 : Définir le répertoire du document
Avant de commencer le code, vous devez définir le chemin d'accès à votre répertoire de documents. C'est là que se trouve votre fichier Excel. 
```csharp
string dataDir = "Your Document Directory";
```
Vous remplacerez « Votre répertoire de documents » par le chemin d'accès réel de votre fichier Excel. Imaginez que vous disiez au programme : « Voici où j'ai rangé mon fichier Excel ; allez y jeter un œil ! »
## Étape 2 : Charger le classeur source
Il est temps de charger le fichier Excel. Nous allons créer une nouvelle instance du fichier `Workbook` classe et passe le chemin du fichier. 
```csharp
Workbook wb = new Workbook(dataDir + "sampleGetFonts.xlsx");
```
Que se passe-t-il ici ? En fait, nous ouvrons la porte à notre feuille de calcul. `Workbook` la classe nous permet d'interagir avec le contenu du fichier Excel. 
## Étape 3 : Obtenir toutes les polices
Vient maintenant le moment magique : récupérons les polices ! `GetFonts()` la méthode est notre ticket d'or.
```csharp
Aspose.Cells.Font[] fnts = wb.GetFonts();
```
Ici, nous demandons au classeur de révéler toutes les polices utilisées. `fnts` Le tableau contiendra nos trésors.
## Étape 4 : Imprimer les polices
Enfin, prenons ces polices et imprimons-les. Cela nous aidera à vérifier nos résultats.
```csharp
for (int i = 0; i < fnts.Length; i++)
{
	Console.WriteLine(fnts[i]);
}
```
Cette boucle traverse chaque police de notre `fnts` Un tableau, qui les affiche un par un dans la console. C'est comme afficher toutes les options typographiques intéressantes de votre fichier Excel !
## Conclusion
Et voilà ! En quelques lignes de code, vous avez récupéré et imprimé la liste des polices utilisées dans votre feuille de calcul Excel grâce à Aspose.Cells pour .NET. Il ne s'agit pas seulement de polices ; il s'agit de comprendre les subtilités de vos documents, d'améliorer vos présentations et de maîtriser l'art de la typographie dans vos feuilles de calcul. Que vous soyez développeur ou simple amateur d'Excel, ce petit extrait pourrait bien changer la donne. 
## FAQ
### Dois-je installer Aspose.Cells séparément ?
Oui, vous devez télécharger et référencer la bibliothèque dans votre projet. 
### Puis-je utiliser Aspose.Cells pour d'autres formats ?
Absolument ! Aspose.Cells fonctionne avec plusieurs formats Excel, comme XLSX, XLS et CSV.
### Existe-t-il un essai gratuit disponible ?
Oui, vous pouvez obtenir un essai gratuit à partir du [lien de téléchargement](https://releases.aspose.com/).
### Comment puis-je obtenir une assistance technique ?
Si vous avez besoin d'aide, le [Forum d'assistance Aspose](https://forum.aspose.com/c/cells/9) est une excellente ressource.
### Aspose.Cells est-il compatible avec .NET Core ?
Oui, Aspose.Cells est également compatible avec les projets .NET Core.


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}