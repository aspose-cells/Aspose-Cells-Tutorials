---
title: Lecture et écriture d'une connexion externe d'un fichier XLSB
linktitle: Lecture et écriture d'une connexion externe d'un fichier XLSB
second_title: Référence de l'API Aspose.Cells pour .NET
description: Découvrez comment gérer les connexions externes dans les fichiers XLSB à l'aide d'Aspose.Cells pour .NET dans ce didacticiel complet.
weight: 130
url: /fr/net/excel-workbook/read-and-write-external-connection-of-xlsb-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Lecture et écriture d'une connexion externe d'un fichier XLSB

## Introduction

Bonjour à tous les passionnés d'Excel ! Êtes-vous prêt à plonger dans le monde fascinant des fichiers XLSB et des connexions externes ? Si vous avez déjà travaillé avec Excel, vous savez à quel point il peut être puissant et polyvalent, mais il comporte parfois des bizarreries, en particulier lorsqu'il s'agit de connexions à des bases de données externes. C'est là qu'Aspose.Cells pour .NET vient à la rescousse ! Cette bibliothèque astucieuse vous permet de manipuler des fichiers Excel de manière simple. Dans cet article, nous vous guiderons étape par étape sur la façon de lire et d'écrire des connexions externes dans un fichier XLSB.

## Prérequis

Avant de commencer, voici quelques éléments dont vous aurez besoin :

1. Connaissances de base de C# : connaître le langage de programmation C# vous sera d'une grande aide. Si vous savez écrire du code C#, vous êtes prêt !
2.  Aspose.Cells pour .NET : vous devez avoir installé cette bibliothèque dans votre environnement de développement. Si vous ne l'avez pas encore fait, vous pouvez facilement la télécharger[ici](https://releases.aspose.com/cells/net/). 
3. Un IDE : vous aurez besoin d’un éditeur de code ou d’un environnement de développement intégré (IDE) tel que Visual Studio. 
4. Exemple de fichier XLSB : nous allons travailler avec un exemple de fichier XLSB contenant des connexions externes. Vous pouvez créer votre propre exemple ou télécharger des exemples en ligne. 

Une fois toutes ces conditions préalables réunies, nous sommes prêts à passer au code !

## Paquets d'importation

Pour commencer, importons les packages nécessaires dans notre projet. Assurez-vous d'avoir ajouté une référence à Aspose.Cells dans votre projet. Voici comment procéder en C# :

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Ces importations vous donnent accès aux fonctionnalités dont vous aurez besoin pour manipuler les fichiers Excel et leurs connexions.

## Étape 1 : Configurer les répertoires

Avant de travailler avec votre fichier XLSB, vous devez configurer vos répertoires source et de sortie. Cette étape est essentielle pour garder vos fichiers organisés.

```csharp
// Répertoire des sources
string sourceDir = "Your Document Directory";
// Répertoire de sortie
string outputDir = "Your Output Directory";
```

 Dans cet extrait de code,`"Your Document Directory"` et`"Your Document Directory"` sont censés récupérer les chemins respectifs où résideront vos fichiers d'entrée et de sortie. Vous pouvez remplacer ces méthodes par des chemins codés en dur si vous préférez.

## Étape 2 : charger le fichier XLSB

Il est maintenant temps de charger votre fichier Excel dans un objet Workbook. Cela vous donne la possibilité de manipuler les données qu'il contient.

```csharp
// Charger le fichier source Excel Xlsb
Workbook wb = new Workbook(sourceDir + "sampleExternalConnection_XLSB.xlsb");
```

 Assurez-vous simplement que votre fichier XLSB se trouve dans le répertoire spécifié.`sourceDir`. Si le chemin est correct, votre classeur sera prêt à être manipulé !

## Étape 3 : Accéder aux connexions externes

Une fois le classeur chargé, vous pouvez accéder à ses connexions externes. Dans notre cas, nous allons récupérer la première connexion à la base de données.

```csharp
// Lisez la première connexion externe qui est en fait une connexion DB
Aspose.Cells.ExternalConnections.DBConnection dbCon = wb.DataConnections[0] as Aspose.Cells.ExternalConnections.DBConnection;
```

 Ici,`DataConnections[0]` fait référence à la première connexion dans le classeur. Nous la présentons comme une`DBConnection` type pour une manipulation ultérieure.

## Étape 4 : Extraire les informations de connexion

Maintenant que vous avez accès à la connexion à la base de données, extrayons et imprimons ses détails sur la console. Cela nous aidera à voir exactement avec quoi nous travaillons.

```csharp
// Imprimer le nom, la commande et les informations de connexion de la connexion DB
Console.WriteLine("Connection Name: " + dbCon.Name);
Console.WriteLine("Command: " + dbCon.Command);
Console.WriteLine("Connection Info: " + dbCon.ConnectionInfo);
```

Cette étape vous permet de vérifier l'état actuel de votre connexion externe. Vous verrez le nom de la connexion, la commande utilisée et les informations de connexion imprimées sur la console.

## Étape 5 : Modifier la connexion

Parfois, un changement de nom suffit pour clarifier les choses ou pour correspondre à de nouvelles conventions de dénomination. Modifions le nom de connexion existant par quelque chose de plus pertinent.

```csharp
// Modifier le nom de la connexion
dbCon.Name = "NewCust";
```

Cette ligne de code renomme efficacement votre connexion de son nom d'origine en « NewCust ». C'est un changement simple mais efficace !

## Étape 6 : Enregistrez vos modifications

Après avoir effectué des modifications, vous souhaiterez enregistrer vos modifications dans le fichier XLSB. Voici comment procéder :

```csharp
// Enregistrer le fichier Excel Xlsb
wb.Save(outputDir + "outputExternalConnection_XLSB.xlsb");
```

Cette ligne de code enregistre votre classeur mis à jour, en conservant toutes vos modifications, y compris le nouveau nom de connexion.

## Étape 7 : Confirmer l'exécution

Enfin, confirmons que tout s'est bien passé. Un simple message à la fin vous le fera comprendre.

```csharp
Console.WriteLine("ReadAndWriteExternalConnectionOfXLSBFile executed successfully.\r\n");
```

Ce message vous rassurera que votre code a été exécuté avec succès et que toutes les modifications ont été enregistrées comme prévu.

## Conclusion

Et voilà ! Vous avez appris avec succès à lire et à écrire des connexions externes dans des fichiers XLSB à l'aide d'Aspose.Cells pour .NET. En suivant ces étapes, vous pouvez gérer efficacement vos connexions de données Excel, ce qui rend votre travail avec Excel beaucoup plus simple et moins frustrant. N'oubliez pas que, que vous manipuliez des ensembles de données volumineux ou que vous organisiez simplement vos informations, Aspose.Cells dispose des outils dont vous avez besoin.

## FAQ

### Qu'est-ce qu'un fichier XLSB ?  
Un fichier XLSB est un format de fichier Excel binaire qui stocke les données d'une feuille de calcul dans un format binaire, ce qui la rend plus compacte et plus rapide à ouvrir.

### Comment installer Aspose.Cells pour .NET ?  
 Vous pouvez facilement le télécharger depuis le site Web d'Aspose[ici](https://releases.aspose.com/cells/net/).

### Puis-je utiliser Aspose.Cells gratuitement ?  
 Oui ! Vous pouvez commencer avec un essai gratuit, qui est disponible[ici](https://releases.aspose.com/).

### Aspose.Cells prend-il en charge d’autres formats de fichiers ?  
Absolument ! Aspose.Cells prend en charge une variété de formats de fichiers, notamment XLSX, CSV, etc.

### Où puis-je demander de l’aide si je rencontre des problèmes ?  
Vous pouvez obtenir de l'aide sur les forums Aspose[ici](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
