---
"description": "Apprenez à ajuster automatiquement les colonnes et les lignes lors du chargement de code HTML dans Excel avec Aspose.Cells pour .NET. Guide étape par étape inclus."
"linktitle": "Ajuster automatiquement les colonnes et les lignes lors du chargement du code HTML dans le classeur"
"second_title": "API de traitement Excel Aspose.Cells .NET"
"title": "Ajuster automatiquement les colonnes et les lignes lors du chargement du code HTML dans le classeur"
"url": "/fr/net/loading-and-saving-excel-files-with-options/auto-fitting-columns-and-rows/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Ajuster automatiquement les colonnes et les lignes lors du chargement du code HTML dans le classeur

## Introduction
Vous êtes-vous déjà demandé comment ajuster automatiquement la taille des colonnes et des lignes lors du chargement de contenu HTML dans un classeur Excel avec Aspose.Cells pour .NET ? Vous êtes au bon endroit ! Dans ce tutoriel, nous allons vous expliquer comment charger un tableau HTML dans un classeur et garantir que les colonnes et les lignes s'ajustent automatiquement au contenu. Si vous travaillez avec des données dynamiques qui changent fréquemment, ce guide sera votre référence pour créer des feuilles Excel bien formatées à partir de HTML.
### Prérequis
Avant de vous lancer dans le code, vous devez configurer quelques éléments sur votre système. Pas d'inquiétude, c'est simple et direct !
1. Visual Studio installé : vous aurez besoin de Visual Studio ou de tout autre environnement de développement .NET.
2. Aspose.Cells pour .NET : vous pouvez [télécharger la dernière version](https://releases.aspose.com/cells/net/) ou utilisez le gestionnaire de packages NuGet pour l'installer.
3. .NET Framework : assurez-vous que .NET Framework 4.0 ou supérieur est installé.
4. Compréhension de base de C# : avoir quelques connaissances en C# rendra ce tutoriel plus fluide pour vous.
5. Données du tableau HTML : préparez du contenu HTML (même un tableau de base) que vous souhaitez charger dans Excel.
## Importer des packages
Commençons par importer les espaces de noms nécessaires. Voici une liste simple des éléments à importer :
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.IO;
```
Ces packages vous permettent de gérer le classeur, de manipuler les données HTML et de les charger de manière transparente dans Excel.
Décomposons ce processus en étapes faciles à suivre. À la fin de cet article, vous disposerez d'un exemple pratique d'ajustement automatique des colonnes et des lignes lors du chargement de code HTML dans un classeur avec Aspose.Cells pour .NET.
## Étape 1 : Configurer le répertoire de documents
Pour faciliter l'enregistrement et la récupération de vos fichiers, nous indiquerons le chemin d'accès à vos documents. Vous pouvez remplacer le chemin d'accès par votre propre dossier.
```csharp
string dataDir = "Your Document Directory";
```
Cette ligne définit le répertoire où seront enregistrés vos fichiers Excel. Il est important de bien organiser vos fichiers lorsque vous travaillez sur plusieurs projets. Imaginez ceci comme le classeur de votre projet !
## Étape 2 : créer des données HTML sous forme de chaîne
Nous allons maintenant définir du contenu HTML de base. Pour cet exemple, nous utiliserons un tableau HTML simple. Vous pouvez le personnaliser selon les besoins de votre projet.
```csharp
string sampleHtml = "<html><body><table><tr><td>This is sample text.</td><td>Some text.</td></tr><tr><td>This is another sample text.</td><td>Some text.</td></tr></table></body></html>";
```
Nous définissons ici une chaîne HTML très basique. Elle contient un tableau composé de quelques lignes et colonnes. Vous pouvez ajouter des lignes ou des colonnes selon vos besoins. Imaginez que vous préparez les ingrédients avant de cuisiner !
## Étape 3 : Charger la chaîne HTML dans MemoryStream
Maintenant que notre contenu HTML est prêt, l’étape suivante consiste à le charger en mémoire en utilisant `MemoryStream`Cela nous permet de manipuler le contenu HTML en mémoire sans l'enregistrer d'abord sur le disque.
```csharp
MemoryStream ms = new MemoryStream(Encoding.UTF8.GetBytes(sampleHtml));
```
En convertissant la chaîne HTML en un tableau d'octets et en l'introduisant dans un `MemoryStream`, nous pouvons travailler avec les données HTML en mémoire. Imaginez cette étape comme la préparation d'un plat dans une casserole avant de le mettre au four !
## Étape 4 : Charger le MemoryStream dans un classeur (sans ajustement automatique)
Une fois que nous avons le contenu HTML en mémoire, nous le chargeons dans un Aspose `Workbook`À ce stade, nous n'ajustons pas encore automatiquement les colonnes et les lignes. Voici notre scénario « avant », à comparer avec la version ajustée automatiquement ultérieurement.
```csharp
Workbook wb = new Workbook(ms);
wb.Save(dataDir + "outputWithout_AutoFitColsAndRows.xlsx");
```
Le classeur contient le contenu HTML, mais les colonnes et les lignes ne sont pas encore ajustées automatiquement au texte. Imaginez que vous prépariez un gâteau en oubliant de vérifier la température : ça marche, mais ce n'est peut-être pas parfait !
## Étape 5 : Spécifier les options de chargement HTML avec l'ajustement automatique activé
Et voilà la magie ! Nous créons une instance de `HtmlLoadOptions` et activer le `AutoFitColsAndRows` propriété. Cela garantit que lorsque le contenu HTML est chargé, les colonnes et les lignes s'ajustent pour s'adapter au contenu qu'elles contiennent.
```csharp
HtmlLoadOptions opts = new HtmlLoadOptions();
opts.AutoFitColsAndRows = true;
```
En définissant cette option, nous demandons à Aspose.Cells de redimensionner automatiquement les lignes et les colonnes. Imaginez que vous régliez le four à la température idéale pour que le gâteau lève parfaitement !
## Étape 6 : Charger le code HTML dans le classeur avec l'ajustement automatique activé
Maintenant, nous chargeons à nouveau le contenu HTML, mais cette fois avec le `AutoFitColsAndRows` Option activée. Cela ajustera la largeur des colonnes et la hauteur des lignes en fonction de leur contenu.
```csharp
wb = new Workbook(ms, opts);
wb.Save(dataDir + "outputWith_AutoFitColsAndRows.xlsx");
```
Cette étape charge le contenu HTML dans un nouveau classeur et l'enregistre au format Excel. Les colonnes et les lignes sont désormais ajustées automatiquement ! Imaginez un gâteau parfaitement cuit, où tout est à la bonne taille.
## Conclusion
En suivant ces étapes simples, vous avez appris à charger du contenu HTML dans un classeur avec Aspose.Cells pour .NET et à ajuster automatiquement les colonnes et les lignes. Vos feuilles Excel sont ainsi toujours nettes, quel que soit le contenu. Cette fonctionnalité simple et puissante vous fera gagner un temps précieux dans la mise en forme et l'organisation de vos données Excel.
Maintenant que vous êtes équipé de ces connaissances, vous pouvez expérimenter avec du contenu HTML plus complexe, ajouter du style et même créer des classeurs Excel entiers à partir de pages Web !
## FAQ
### Puis-je utiliser cette méthode pour charger de grandes tables HTML ?
Oui, Aspose.Cells gère efficacement les grands tableaux HTML, mais pour des performances optimales, il est conseillé de tester avec vos tailles de données.
### Puis-je appliquer manuellement des largeurs de colonnes et des hauteurs de lignes spécifiques après l'ajustement automatique ?
Absolument ! Vous pouvez toujours personnaliser les colonnes et les lignes individuellement, même après avoir utilisé la fonction d'ajustement automatique.
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