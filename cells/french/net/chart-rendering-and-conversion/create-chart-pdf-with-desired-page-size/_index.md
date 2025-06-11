---
"description": "Créez un PDF avec votre graphique Excel avec Aspose.Cells pour .NET. Découvrez comment grâce à ce guide étape par étape."
"linktitle": "Créer un graphique PDF avec la taille de page souhaitée"
"second_title": "API de traitement Excel Aspose.Cells .NET"
"title": "Créer un graphique PDF avec la taille de page souhaitée"
"url": "/fr/net/chart-rendering-and-conversion/create-chart-pdf-with-desired-page-size/"
"weight": 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Créer un graphique PDF avec la taille de page souhaitée

## Introduction

Créer des graphiques attrayants et informatifs est essentiel pour la représentation des données dans divers domaines. Qu'il s'agisse de données de vente, d'indicateurs de performance ou de tout autre type d'information, la production de graphiques de haute qualité apporte profondeur et clarté à vos résultats. Si vous travaillez avec des applications .NET, Aspose.Cells est une bibliothèque puissante qui simplifie la gestion des documents Excel et la création de graphiques. Dans ce tutoriel, nous vous guiderons dans la création d'un graphique au format PDF à partir d'un fichier Excel, au format de page souhaité.

## Prérequis

Avant de plonger dans le code, il y a quelques prérequis que vous devez remplir pour garantir une expérience fluide :

### Connaissances de base de C# et .NET

Vous aurez besoin de connaissances fondamentales en programmation C# et en framework .NET. Cela vous aidera à comprendre la structure du code que vous découvrirez dans ce guide.

### Aspose.Cells pour .NET

Assurez-vous d'avoir installé Aspose.Cells pour .NET. Vous trouverez tous les détails sur le site [Documentation d'Aspose.Cells](https://reference.aspose.com/cells/net/). 

### Environnement de développement

Configurez votre environnement de développement. Il peut s'agir de Visual Studio ou de tout autre IDE prenant en charge C#. Téléchargez et installez la bibliothèque Aspose.Cells depuis le [page de téléchargement](https://releases.aspose.com/cells/net/).

### Exemple de fichier Excel

Vous aurez besoin d'un fichier Excel contenant au moins un graphique. Vous pouvez créer un fichier d'exemple ou en télécharger un pour l'utiliser tout au long de ce tutoriel.

## Importer des packages

Pour commencer à utiliser Aspose.Cells, vous devez importer les espaces de noms nécessaires dans votre application C#. Voici comment procéder :

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

using Aspose.Cells.Charts;
```

Ces espaces de noms vous donnent accès aux classes et méthodes nécessaires pour manipuler les classeurs Excel et leur contenu.

Maintenant que nous avons réglé tous les prérequis, décomposons le processus en étapes détaillées.

## Étape 1 : Configuration des répertoires de sortie et de source

Pour commencer, vous devez définir où le PDF de sortie sera enregistré et où se trouve votre document Excel source.

```csharp
//Répertoire de sortie
string outputDir = "Your Output Directory";

//Répertoire source
string sourceDir = "Your Document Directory";
```

Assurez-vous de remplacer « Votre répertoire de sortie » et « Votre répertoire de documents » par les chemins d'accès réels sur votre système. Cela indique où Aspose enregistrera le PDF généré et où il trouvera le fichier Excel.

## Étape 2 : Charger l’exemple de fichier Excel

Ensuite, vous devez charger le fichier Excel contenant le graphique. Voici comment procéder :

```csharp
//Charger un exemple de fichier Excel contenant le graphique.
Workbook wb = new Workbook(sourceDir + "sampleCreateChartPDFWithDesiredPageSize.xlsx");
```

Le `Workbook` La classe est essentielle à l'interaction avec votre document Excel. Assurez-vous que le chemin pointe correctement vers votre fichier Excel ; une erreur à ce niveau empêchera l'exécution du reste du code.

## Étape 3 : Accéder à la première feuille de travail

Une fois le classeur chargé, l’étape suivante consiste à accéder à la feuille de calcul contenant le graphique souhaité.

```csharp
//Accéder à la première feuille de travail.
Worksheet ws = wb.Worksheets[0];
```

Dans Aspose.Cells, les feuilles de calcul sont indexées à partir de zéro, donc `Worksheets[0]` fait référence à la première feuille.

## Étape 4 : Accéder au premier graphique

Maintenant, accédons au graphique que vous souhaitez exporter au format PDF. Cette étape suppose que votre feuille de calcul contienne au moins un graphique.

```csharp
//Accédez au premier graphique à l'intérieur de la feuille de calcul.
Chart ch = ws.Charts[0];
```

Encore une fois, cela accède au premier graphique de la feuille de calcul ; assurez-vous que la structure de votre feuille de calcul convient à cette approche.

## Étape 5 : Créer un PDF avec la taille de page souhaitée

Enfin, il est temps de créer le PDF à partir du graphique, avec une taille de page spécifique. Voici la ligne de code magique qui fait tout cela :

```csharp
//Créez un graphique PDF avec la taille de page souhaitée.
ch.ToPdf(outputDir + "outputCreateChartPDFWithDesiredPageSize.pdf", 7, 7, PageLayoutAlignmentType.Center, PageLayoutAlignmentType.Center);
```

Dans ce code :
- Le PDF sera enregistré dans le répertoire de sortie que vous avez spécifié précédemment.
- Les chiffres `7, 7` représentent respectivement la largeur et la hauteur de la taille de page souhaitée.
- PageLayoutAlignmentType.Center garantit que le graphique est centré sur la page.

## Étape 6 : Message de confirmation

Pour vous faire savoir (et faire savoir aux autres) que tout s'est bien passé, incluez un message de confirmation à la fin de votre code :

```csharp
Console.WriteLine("CreateChartPDFWithDesiredPageSize executed successfully.");
```

Ce message apparaîtra dans la fenêtre de la console une fois le processus terminé, signalant que votre PDF a été créé sans accroc.

## Conclusion

Félicitations ! Vous venez d'apprendre à utiliser Aspose.Cells pour .NET pour créer un PDF à partir d'un graphique Excel. Cette puissante bibliothèque simplifie la manipulation des documents Excel et la génération de représentations visuelles des données, vous épargnant ainsi des heures de mise en forme manuelle. N'hésitez pas à explorer les nombreuses autres fonctionnalités d'Aspose.Cells, au-delà de la simple génération de PDF : on ne sait jamais ce qui pourrait améliorer encore vos projets !

## FAQ

### À quoi sert Aspose.Cells pour .NET ?  
Aspose.Cells pour .NET est utilisé pour créer, éditer et convertir des documents Excel par programmation dans des applications .NET.

### Puis-je utiliser Aspose.Cells gratuitement ?  
Oui, Aspose.Cells propose un [essai gratuit](https://releases.aspose.com/) à des fins d'évaluation.

### Existe-t-il un moyen de prolonger mon essai au-delà de la période initiale ?  
Vous pouvez postuler pour un [permis temporaire](https://purchase.aspose.com/temporary-license/) pour des tests prolongés.

### Que faire si je rencontre des problèmes ou si j'ai des questions ?  
Vous pouvez demander de l'aide à la communauté Aspose sur leur [forum d'assistance](https://forum.aspose.com/c/cells/9).

### Comment puis-je acheter Aspose.Cells ?  
Vous pouvez acheter Aspose.Cells auprès du [page d'achat](https://purchase.aspose.com/buy).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}