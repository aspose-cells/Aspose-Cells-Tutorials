---
title: Ajuster automatiquement les colonnes et les lignes lors du chargement du code HTML dans le classeur
linktitle: Ajuster automatiquement les colonnes et les lignes lors du chargement du code HTML dans le classeur
second_title: API de traitement Excel Aspose.Cells .NET
description: Découvrez comment ajuster automatiquement les colonnes et les lignes lors du chargement de code HTML dans Excel à l'aide d'Aspose.Cells pour .NET. Guide étape par étape inclus.
weight: 10
url: /fr/net/loading-and-saving-excel-files-with-options/auto-fitting-columns-and-rows/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ajuster automatiquement les colonnes et les lignes lors du chargement du code HTML dans le classeur

## Introduction
Vous êtes-vous déjà demandé comment ajuster automatiquement la taille des colonnes et des lignes lors du chargement de contenu HTML dans un classeur Excel à l'aide d'Aspose.Cells pour .NET ? Eh bien, vous êtes au bon endroit ! Dans ce didacticiel, nous allons découvrir comment charger un tableau HTML dans un classeur et garantir que les colonnes et les lignes sont ajustées automatiquement pour correspondre au contenu. Si vous travaillez avec des données dynamiques qui changent fréquemment, ce guide sera votre référence pour créer des feuilles Excel bien formatées à partir de HTML.
### Prérequis
Avant de vous lancer dans le code, vous devez configurer quelques éléments sur votre système. Ne vous inquiétez pas, c'est simple et direct !
1. Visual Studio installé : vous aurez besoin de Visual Studio ou de tout autre environnement de développement .NET.
2.  Aspose.Cells pour .NET : vous pouvez[télécharger la dernière version](https://releases.aspose.com/cells/net/) ou utilisez le gestionnaire de packages NuGet pour l'installer.
3. .NET Framework : assurez-vous que .NET Framework 4.0 ou supérieur est installé.
4. Compréhension de base de C# : avoir quelques connaissances en C# rendra ce tutoriel plus fluide pour vous.
5. Données du tableau HTML : préparez du contenu HTML (même un tableau de base) que vous souhaitez charger dans Excel.
## Paquets d'importation
Tout d'abord, importons les espaces de noms nécessaires pour commencer. Voici une liste simple de ce que vous devez importer :
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.IO;
```
Ces packages vous permettent de gérer le classeur, de manipuler les données HTML et de les charger de manière transparente dans Excel.
Décomposons ce processus en parties faciles à gérer afin que vous puissiez le suivre facilement. À la fin de cet article, vous disposerez d'un exemple pratique de la façon d'ajuster automatiquement les colonnes et les lignes lors du chargement de code HTML dans un classeur à l'aide d'Aspose.Cells pour .NET.
## Étape 1 : Configurer le répertoire de documents
Pour sauvegarder et récupérer facilement vos fichiers, nous allons spécifier le chemin où seront stockés vos documents. Vous pouvez remplacer le chemin du répertoire par votre propre emplacement de dossier.
```csharp
string dataDir = "Your Document Directory";
```
Cette ligne définit le répertoire dans lequel vos fichiers Excel seront enregistrés. Il est important d'organiser correctement vos fichiers lorsque vous travaillez sur plusieurs projets. Imaginez cela comme le classeur de votre projet !
## Étape 2 : créer des données HTML sous forme de chaîne
Ensuite, nous allons définir un contenu HTML de base. Pour cet exemple, nous utiliserons un tableau HTML simple. Vous pouvez le personnaliser en fonction des besoins de votre projet.
```csharp
string sampleHtml = "<html><body><table><tr><td>This is sample text.</td><td>Some text.</td></tr><tr><td>This is another sample text.</td><td>Some text.</td></tr></table></body></html>";
```
Nous définissons ici une chaîne HTML très basique. Elle contient un tableau avec quelques lignes et colonnes. Vous pouvez ajouter plus de lignes ou de colonnes selon vos besoins. Considérez cela comme la préparation des ingrédients avant de cuisiner un repas !
## Étape 3 : charger la chaîne HTML dans MemoryStream
 Maintenant que notre contenu HTML est prêt, l’étape suivante consiste à le charger en mémoire à l’aide de`MemoryStream`Cela nous permet de manipuler le contenu HTML en mémoire sans l'enregistrer au préalable sur le disque.
```csharp
MemoryStream ms = new MemoryStream(Encoding.UTF8.GetBytes(sampleHtml));
```
 En convertissant la chaîne HTML en un tableau d'octets et en l'introduisant dans un`MemoryStream`, nous pouvons travailler avec les données HTML en mémoire. Imaginez cette étape comme la préparation du plat dans une casserole avant de le mettre au four !
## Étape 4 : charger le MemoryStream dans un classeur (sans ajustement automatique)
 Une fois que nous avons le contenu HTML en mémoire, nous le chargeons dans un Aspose`Workbook`À ce stade, nous n'avons pas encore ajusté automatiquement les colonnes et les lignes. Il s'agit de notre scénario « avant », à comparer avec la version ajustée automatiquement ultérieurement.
```csharp
Workbook wb = new Workbook(ms);
wb.Save(dataDir + "outputWithout_AutoFitColsAndRows.xlsx");
```
Le classeur est chargé avec le contenu HTML, mais les colonnes et les lignes ne sont pas encore ajustées automatiquement au texte. Imaginez que vous faites cuire un gâteau mais que vous oubliez de vérifier la température : cela fonctionne, mais ce n'est peut-être pas parfait !
## Étape 5 : Spécifier les options de chargement HTML avec l'ajustement automatique activé
 Et maintenant, voici la magie ! Nous créons une instance de`HtmlLoadOptions` et activer le`AutoFitColsAndRows` propriété. Cela garantit que lorsque le contenu HTML est chargé, les colonnes et les lignes s'ajustent pour s'adapter au contenu qu'elles contiennent.
```csharp
HtmlLoadOptions opts = new HtmlLoadOptions();
opts.AutoFitColsAndRows = true;
```
En définissant cette option, nous demandons à Aspose.Cells de redimensionner automatiquement les lignes et les colonnes. Imaginez que vous régliez le four à la température idéale pour que le gâteau lève parfaitement !
## Étape 6 : charger le code HTML dans le classeur avec l'ajustement automatique activé
 Maintenant, nous chargeons à nouveau le contenu HTML, mais cette fois avec le`AutoFitColsAndRows`option activée. Cela ajustera la largeur des colonnes et la hauteur des lignes en fonction du contenu qu'elles contiennent.
```csharp
wb = new Workbook(ms, opts);
wb.Save(dataDir + "outputWith_AutoFitColsAndRows.xlsx");
```
Cette étape charge le contenu HTML dans un nouveau classeur et l'enregistre sous forme de fichier Excel, mais les colonnes et les lignes sont désormais ajustées automatiquement ! Considérez cela comme un gâteau parfaitement cuit, où tout est exactement à la bonne taille.
## Conclusion
En suivant ces étapes simples, vous avez appris à charger du contenu HTML dans un classeur à l'aide d'Aspose.Cells pour .NET et à ajuster automatiquement les colonnes et les lignes. Cela garantit que vos feuilles Excel sont toujours nettes, quel que soit le dynamisme du contenu. Il s'agit d'une fonctionnalité simple mais puissante qui peut vous faire gagner beaucoup de temps dans la mise en forme et l'organisation de vos données Excel.
Maintenant que vous êtes équipé de ces connaissances, vous pouvez expérimenter du contenu HTML plus complexe, ajouter du style et même créer des classeurs Excel entiers à partir de pages Web !
## FAQ
### Puis-je utiliser cette méthode pour charger de grandes tables HTML ?
Oui, Aspose.Cells gère efficacement les grands tableaux HTML, mais pour des performances optimales, il est conseillé de tester avec vos tailles de données.
### Puis-je appliquer manuellement des largeurs de colonnes et des hauteurs de lignes spécifiques après l'ajustement automatique ?
Absolument ! Vous pouvez toujours personnaliser les colonnes et les lignes individuelles même après avoir utilisé la fonction d'ajustement automatique.
### Comment puis-je styliser le tableau après le chargement du HTML ?
Vous pouvez appliquer des styles à l'aide des options de style étendues d'Aspose.Cells après le chargement du HTML.
### Aspose.Cells pour .NET est-il compatible avec les anciennes versions de .NET Framework ?
Oui, Aspose.Cells pour .NET prend en charge .NET Framework 4.0 et versions ultérieures.
### Puis-je charger d’autres types de contenu en plus du HTML dans Excel à l’aide d’Aspose.Cells ?
Oui, Aspose.Cells prend en charge le chargement de divers formats tels que CSV, JSON et XML dans Excel.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
