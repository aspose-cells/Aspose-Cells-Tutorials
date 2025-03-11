---
title: Obtenir la liste des polices utilisées dans la feuille de calcul
linktitle: Obtenir la liste des polices utilisées dans la feuille de calcul
second_title: API de traitement Excel Aspose.Cells .NET
description: Apprenez à récupérer et à répertorier les polices à partir de feuilles de calcul Excel à l'aide d'Aspose.Cells pour .NET avec ce didacticiel facile à suivre.
weight: 10
url: /fr/net/working-with-fonts-in-spreadsheets/get-list-of-fonts-used-in-spreadsheet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Obtenir la liste des polices utilisées dans la feuille de calcul

## Introduction
Vous êtes-vous déjà retrouvé à parcourir une feuille de calcul Excel en vous interrogeant sur les polices utilisées dans ses différentes cellules ? Peut-être avez-vous rencontré un ancien document et aimeriez-vous savoir quels choix typographiques ont été effectués ? Eh bien, vous avez de la chance ! Avec Aspose.Cells pour .NET, c'est comme avoir une boîte à outils qui vous permet de passer au crible et de découvrir les secrets des polices cachés dans vos feuilles de calcul. Dans ce guide, nous vous expliquerons comment récupérer facilement une liste de toutes les polices utilisées dans un fichier Excel. Attachez vos ceintures et plongeons dans le monde des feuilles de calcul !
## Prérequis
Avant de nous lancer dans le code, vous aurez besoin de quelques éléments pour commencer. Ne vous inquiétez pas, c'est très simple. Voici une liste de contrôle de ce dont vous avez besoin :
1. Visual Studio : assurez-vous qu'une version de Visual Studio est installée sur votre ordinateur. C'est ici que nous écrirons notre code.
2. Aspose.Cells pour .NET : vous devez disposer de la bibliothèque Aspose.Cells. Si vous ne l'avez pas encore téléchargée, vous pouvez la récupérer à partir du[site](https://releases.aspose.com/cells/net/).
3. Connaissances de base de C# : une petite compréhension de la programmation C# vous aidera certainement à naviguer facilement dans le code.
4. Un exemple de fichier Excel : vous aurez besoin d'un exemple de fichier Excel, comme « sampleGetFonts.xlsx », pour travailler. C'est ici que nous appliquerons notre exploration des polices.
Une fois que vous avez tout réglé, vous êtes prêt à vous lancer dans le codage !
## Paquets d'importation
Pour commencer, importons les espaces de noms nécessaires. Dans .NET, importer des packages revient à inviter les bons invités à votre fête : sans eux, tout ne fonctionnera pas correctement.
Voici comment importer Aspose.Cells :
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.IO;
```
Avec cette simple ligne, nous invitons la fonctionnalité principale d'Aspose.Cells dans notre projet. Passons maintenant au chargement du classeur.
## Étape 1 : définir le répertoire du document
Tout d’abord, avant de nous plonger dans le code, vous devez définir le chemin d’accès à votre répertoire de documents. C’est là que se trouve votre fichier Excel. 
```csharp
string dataDir = "Your Document Directory";
```
Vous allez remplacer « Votre répertoire de documents » par le chemin d'accès réel où se trouve votre fichier Excel. Considérez cela comme une indication au programme : « Hé, voici où j'ai rangé mon fichier Excel ; allez y jeter un œil ! »
## Étape 2 : charger le classeur source
 Il est temps de charger le fichier Excel. Nous allons créer une nouvelle instance du`Workbook` classe et passe le chemin du fichier. 
```csharp
Workbook wb = new Workbook(dataDir + "sampleGetFonts.xlsx");
```
 Que se passe-t-il ici ? Nous ouvrons en fait la porte de notre feuille de calcul.`Workbook` la classe nous permet d'interagir avec le contenu du fichier Excel. 
## Étape 3 : Obtenir toutes les polices
 Vient maintenant le moment magique : récupérons les polices !`GetFonts()` la méthode est notre ticket d'or.
```csharp
Aspose.Cells.Font[] fnts = wb.GetFonts();
```
 Ici, nous demandons au classeur de révéler toutes les polices utilisées à l'intérieur.`fnts` Le tableau contiendra nos trésors.
## Étape 4 : Imprimez les polices
Enfin, prenons ces polices et imprimons-les. Cela nous aidera à vérifier ce que nous avons trouvé.
```csharp
for (int i = 0; i < fnts.Length; i++)
{
	Console.WriteLine(fnts[i]);
}
```
 Cette boucle traverse chaque police de notre`fnts` tableau, en les affichant un par un sur la console. C'est comme montrer tous les choix de typographie intéressants que vous avez dans votre fichier Excel !
## Conclusion
Et voilà ! Avec seulement quelques lignes de code, vous avez réussi à récupérer et à imprimer la liste des polices utilisées dans votre feuille de calcul Excel à l'aide d'Aspose.Cells pour .NET. Il ne s'agit pas seulement de polices ; il s'agit de comprendre les subtilités de vos documents, d'améliorer vos présentations et de maîtriser l'art de la typographie dans vos feuilles de calcul. Que vous soyez un développeur ou quelqu'un qui aime simplement bricoler avec Excel, ce petit extrait pourrait changer la donne. 
## FAQ
### Dois-je installer Aspose.Cells séparément ?
Oui, vous devez télécharger et référencer la bibliothèque dans votre projet. 
### Puis-je utiliser Aspose.Cells pour d’autres formats ?
Absolument ! Aspose.Cells fonctionne avec plusieurs formats Excel, comme XLSX, XLS et CSV.
### Existe-t-il un essai gratuit disponible ?
 Oui, vous pouvez obtenir un essai gratuit à partir du[lien de téléchargement](https://releases.aspose.com/).
### Comment puis-je obtenir un support technique ?
 Si vous avez besoin d'aide, le[Forum d'assistance Aspose](https://forum.aspose.com/c/cells/9) est une excellente ressource.
### Aspose.Cells est-il compatible avec .NET Core ?
Oui, Aspose.Cells est également compatible avec les projets .NET Core.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
