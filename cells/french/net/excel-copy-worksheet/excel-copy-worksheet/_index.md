---
title: Feuille de calcul de copie Excel
linktitle: Feuille de calcul de copie Excel
second_title: Référence de l'API Aspose.Cells pour .NET
description: Découvrez comment copier une feuille de calcul Excel à l'aide d'Aspose.Cells pour .NET grâce à ce guide étape par étape facile à suivre. Idéal pour les développeurs .NET souhaitant automatiser les tâches Excel.
weight: 20
url: /fr/net/excel-copy-worksheet/excel-copy-worksheet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Feuille de calcul de copie Excel

## Introduction

Dans le monde de la gestion des données, les feuilles de calcul sont omniprésentes, de la gestion des chiffres de vente à l'organisation des données de projet. Mais comment gérer ces fichiers lorsque l'automatisation devient nécessaire ? Eh bien, si vous travaillez dans .NET, Aspose.Cells est un excellent outil pour manipuler des fichiers Excel par programmation. Dans cet article, nous vous guiderons dans la copie d'une feuille de calcul dans un fichier Excel à l'aide d'Aspose.Cells pour .NET. Il s'agit d'une tâche courante lorsque vous devez dupliquer des données dans de nouvelles feuilles sans repartir de zéro.

Alors, attachez vos ceintures ! Nous allons nous plonger dans ce processus, mais d'une manière simple, conversationnelle et claire.

## Prérequis

Avant de passer au plaisir, assurons-nous que vous disposez de tout ce dont vous avez besoin pour commencer ce tutoriel.

### Installer Aspose.Cells pour .NET
Tout d'abord, si vous n'avez pas encore installé Aspose.Cells pour .NET, vous devrez le télécharger et l'installer. Vous pouvez récupérer la dernière version sur leur page de publication.

- [Télécharger Aspose.Cells pour .NET](https://releases.aspose.com/cells/net/)

Vous pouvez utiliser NuGet dans Visual Studio ou le télécharger manuellement. Si vous préférez la solution NuGet, exécutez simplement cette commande :

```bash
Install-Package Aspose.Cells
```

### Obtenir une licence
Pour déverrouiller pleinement les fonctionnalités d'Aspose.Cells, il est préférable d'obtenir une licence.

- [Acheter une licence](https://purchase.aspose.com/buy) ou[Demander une licence temporaire](https://purchase.aspose.com/temporary-license/)

L'utilisation de la bibliothèque sans licence appliquera des filigranes à vos fichiers de sortie, alors assurez-vous d'avoir votre licence prête !

### Configurez votre environnement de développement
Assurez-vous d'avoir installé les éléments suivants :
- Visual Studio (ou tout IDE compatible avec .NET)
- .NET Framework ou .NET Core

Avec tout installé et configuré, commençons à coder !

## Paquets d'importation

Pour travailler avec Aspose.Cells, vous devez d'abord importer les espaces de noms requis dans votre projet. Voici l'extrait de code pour vous assurer que vous disposez des références correctes :

```csharp
using System.IO;
using Aspose.Cells;
using System;
```

Maintenant que nous avons fait le ménage, passons au vrai travail : copier une feuille de calcul dans un classeur Excel.

## Étape 1 : définissez vos chemins d’accès aux répertoires
La première chose dont vous avez besoin est de spécifier le répertoire dans lequel se trouvent vos fichiers Excel. C'est la clé pour charger le fichier dans votre projet et enregistrer le classeur modifié.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
string InputPath = dataDir + "book1.xls";
```

-  Le`dataDir` La variable contient le chemin du répertoire dans lequel se trouvent vos fichiers Excel. Modifier`"YOUR DOCUMENT DIRECTORY"` au chemin du dossier réel.
- `InputPath` stocke l'emplacement du fichier Excel sur lequel nous allons travailler (dans ce cas, « book1.xls »).

C'est une bonne idée d'utiliser des chemins dynamiques afin de pouvoir facilement basculer entre les environnements (développement, préparation, production).

## Étape 2 : Ouvrir le classeur Excel
Ensuite, chargeons le fichier Excel à l’aide de la classe Workbook, qui représente un fichier Excel entier.

```csharp
Workbook wb = new Workbook(InputPath);
```

-  Le`Workbook` l'objet charge le fichier Excel situé à`InputPath`Aspose.Cells s'occupe d'analyser le fichier, vous n'avez donc pas à vous soucier de la complexité du format Excel.

## Étape 3 : Accéder à la collection de feuilles de travail
Chaque classeur contient plusieurs feuilles de calcul (considérez-les comme des onglets dans votre fichier Excel). Pour copier une feuille de calcul, vous devez d'abord accéder à ces feuilles.

```csharp
WorksheetCollection sheets = wb.Worksheets;
```

- `WorksheetCollection` Il s'agit essentiellement d'une liste de toutes les feuilles de calcul du classeur. C'est avec cela que nous allons travailler pour copier notre feuille.

## Étape 4 : Copier une feuille de calcul existante
Passons maintenant à la partie intéressante : dupliquer la feuille de calcul ! Ici, nous allons copier le contenu de « Feuille1 » dans une nouvelle feuille.

```csharp
sheets.AddCopy("Sheet1");
```

-  Le`AddCopy` La méthode duplique une feuille de calcul existante (dans ce cas, « Feuille1 ») et ajoute la nouvelle feuille au classeur.
-  Vous pouvez remplacer`"Sheet1"` avec n'importe quel nom de feuille que vous souhaitez copier.

## Étape 5 : Enregistrer le classeur
Enfin, après avoir copié la feuille de calcul, il est temps d'enregistrer le fichier Excel mis à jour. Nous utiliserons la méthode Save pour enregistrer les modifications dans un nouveau fichier.

```csharp
wb.Save(dataDir + "CopyWithinWorkbook_out.xls");
```

-  Le`Save` la méthode écrit le classeur mis à jour dans un nouveau fichier (`CopyWithinWorkbook_out.xls` ). Vous pouvez choisir n'importe quel nom pour le fichier de sortie, mais n'oubliez pas de l'enregistrer dans le format approprié (par exemple,`.xls`, `.xlsx`).

Et voilà ! Vous avez réussi à dupliquer une feuille de calcul dans un fichier Excel.

## Conclusion

La copie d'une feuille de calcul dans Aspose.Cells pour .NET est non seulement simple mais également très efficace. Avec seulement quelques lignes de code, vous pouvez automatiser les tâches répétitives d'Excel, ce qui vous simplifie grandement la vie lorsque vous traitez de grands ensembles de données ou des rapports basés sur des modèles. Que vous automatisiez des rapports financiers, des journaux d'inventaire ou tout autre élément nécessitant Excel, Aspose.Cells est votre solution de référence.

## FAQ

### Puis-je copier plusieurs feuilles de calcul à la fois à l’aide d’Aspose.Cells pour .NET ?
 Non, vous devrez les copier un par un en utilisant le`AddCopy` méthode. Cependant, vous pouvez facilement parcourir plusieurs feuilles et les copier en séquence.

### Aspose.Cells pour .NET prend-il en charge la copie de feuilles de calcul entre différents classeurs ?
 Oui, vous pouvez copier des feuilles de calcul entre différents classeurs en ouvrant les deux classeurs et en utilisant le`AddCopy` méthode entre eux.

### Quels formats Excel Aspose.Cells prend-il en charge ?
Aspose.Cells prend en charge une large gamme de formats Excel, notamment`.xls`, `.xlsx`, `.csv`, `.html`, et plus encore.

### Ai-je besoin d'une licence pour utiliser Aspose.Cells pour .NET ?
 Oui, pour éviter les filigranes et exploiter tout le potentiel de la bibliothèque, vous avez besoin d'une licence valide. Cependant, vous pouvez demander une[permis temporaire gratuit](https://purchase.aspose.com/temporary-license) pour l'essayer avant d'acheter.

### Puis-je exécuter Aspose.Cells sur .NET Core ?
Oui, Aspose.Cells est entièrement compatible avec .NET Framework et .NET Core, ce qui le rend polyvalent pour les applications multiplateformes.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
