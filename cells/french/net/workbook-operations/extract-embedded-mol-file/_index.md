---
title: Extraire le fichier Mol intégré du classeur
linktitle: Extraire le fichier Mol intégré du classeur
second_title: API de traitement Excel Aspose.Cells .NET
description: Découvrez comment extraire des fichiers MOL intégrés à partir de classeurs Excel à l'aide d'Aspose.Cells pour .NET dans ce didacticiel détaillé étape par étape.
weight: 18
url: /fr/net/workbook-operations/extract-embedded-mol-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extraire le fichier Mol intégré du classeur

## Introduction
Lorsque vous gérez des données dans des classeurs Excel, vous rencontrez parfois divers objets intégrés qui ne sont pas dans un format standard. L'un de ces formats est le fichier de structure moléculaire (MOL), couramment utilisé en chimie pour représenter des informations moléculaires. Si vous cherchez à extraire ces fichiers MOL d'un classeur Excel à l'aide d'Aspose.Cells pour .NET, vous êtes tombé sur le bon guide. Dans cet article, nous vous guiderons pas à pas tout au long du processus, en démystifiant chaque partie.
## Prérequis
Avant de vous plonger dans le code, il est essentiel de vous assurer que vous disposez des compétences et des outils nécessaires. Voici ce dont vous aurez besoin :
1. Compréhension de base de la programmation .NET : vous devez être familiarisé avec C# et le framework .NET.
2.  Aspose.Cells pour .NET : assurez-vous que vous disposez de la bibliothèque Aspose.Cells. Vous pouvez[téléchargez-le ici](https://releases.aspose.com/cells/net/).
3. Un IDE : vous pouvez utiliser Visual Studio ou tout autre IDE compatible .NET.
4. Classeur Excel avec fichiers MOL intégrés : pour ce didacticiel, vous avez besoin d'un fichier Excel contenant des objets MOL. Vous pouvez créer le vôtre ou utiliser n'importe quel fichier d'exemple.
## Paquets d'importation
Pour commencer, vous devez importer les espaces de noms nécessaires dans votre projet. Cela est essentiel pour accéder aux fonctionnalités d'Aspose.Cells. Voici comment procéder :

```csharp
using Aspose.Cells.Drawing;
using Aspose.Cells.WebExtensions;
using System;
using System.IO;
```

Ces espaces de noms vous permettront de manipuler des classeurs, d'accéder à des feuilles de calcul et de travailler avec des fichiers en général.
Maintenant que nous avons réglé nos prérequis, plongeons dans le code et comprenons chaque étape impliquée dans l'extraction de fichiers MOL intégrés à partir d'un classeur Excel. 
## Étape 1 : Configuration de vos répertoires
La première étape consiste à définir où se trouve votre document source et où vous souhaitez enregistrer les fichiers MOL extraits. Configurons ces répertoires.
```csharp
string SourceDir = "Your Document Directory"; // Remplacez par le chemin de votre répertoire
string outputDir = "Your Document Directory"; // Remplacez par votre chemin de sortie
```
 Ici, vous remplacez`"Your Document Directory"`avec le chemin vers vos répertoires actuels. Il est important que les répertoires source et de sortie soient accessibles à votre application.
## Étape 2 : chargement du classeur
Une fois vos répertoires configurés, la tâche suivante consiste à charger le classeur Excel. Faisons-le maintenant.

```csharp
Workbook workbook = new Workbook(SourceDir + "EmbeddedMolSample.xlsx");
```

 Nous créons une instance de`Workbook` classe et en passant le chemin vers notre fichier Excel nommé`EmbeddedMolSample.xlsx`Cette étape initialise le classeur, vous permettant d’accéder à son contenu.
## Étape 3 : Itération sur les feuilles de calcul
Maintenant que votre classeur est chargé, vous devez parcourir chaque feuille de calcul du classeur. Cela vous permet d'examiner chaque feuille à la recherche d'objets incorporés.

```csharp
var index = 1; // Utilisé pour nommer les fichiers MOL extraits
foreach (Worksheet sheet in workbook.Worksheets)
{
    OleObjectCollection oles = sheet.OleObjects;
    // La logique d'extraction ultérieure se déroule ici
}
```

 Ici, vous utilisez un`foreach` boucle pour naviguer dans les feuilles de calcul. Pour chaque feuille de calcul, vous accédez à la`OleObjects` collection, qui contient tous les objets incorporés.
## Étape 4 : Extraction des fichiers MOL
Vient maintenant la partie critique : l'extraction des fichiers MOL à partir des objets OLE. Cela nécessite une autre boucle à l'intérieur de la boucle de la feuille de calcul.

```csharp
foreach (OleObject ole in oles)
{
    string fileName = outputDir + "OleObject" + index + ".mol ";
    FileStream fs = File.Create(fileName);
    fs.Write(ole.ObjectData, 0, ole.ObjectData.Length);
    fs.Close();
    index++;
}
```

 Pour chaque objet OLE que vous avez trouvé, vous créez un nouveau fichier dans le répertoire de sortie.`ObjectData` propriété de la`OleObject` contient les données de l'objet incorporé, que vous écrivez dans un fichier nouvellement créé à l'aide d'un`FileStream`. Le fichier est nommé séquentiellement (`OleObject1.mol`, `OleObject2.mol` , etc.) en fonction de la`index` variable.
## Étape 5 : Confirmation de l'achèvement du processus
Enfin, une fois tous les fichiers MOL extraits, il est recommandé d'informer l'utilisateur que le processus s'est terminé avec succès.

```csharp
Console.WriteLine("ExtractEmbeddedMolFile executed successfully.");
```

Cette ligne affiche simplement un message sur la console vous informant que l'extraction a réussi. C'est une bonne idée pour recueillir les commentaires des utilisateurs.
## Conclusion
Et voilà ! Vous avez extrait avec succès des fichiers MOL intégrés d'un classeur Excel à l'aide d'Aspose.Cells pour .NET. Ce processus intègre quelques étapes essentielles, garantissant une approche structurée de la gestion des objets intégrés. Que vous travailliez dans la recherche scientifique, l'analyse chimique ou que vous traitiez simplement des ensembles de données complexes, la capacité d'extraire et de manipuler ces types de fichiers peut faire une différence significative dans la façon dont vous gérez vos informations. 
## FAQ
### Puis-je extraire d’autres types de fichiers en plus de MOL à partir d’Excel ?
Oui, vous pouvez extraire divers autres types de fichiers intégrés avec des techniques similaires.
### L'utilisation d'Aspose.Cells est-elle gratuite ?
 Aspose.Cells est une bibliothèque commerciale, mais vous pouvez[essayez-le gratuitement pendant une période limitée](https://releases.aspose.com/).
### Cette méthode fonctionne-t-elle avec toutes les versions d’Excel ?
Oui, tant que le format de fichier est pris en charge par Aspose.Cells.
### Puis-je automatiser ce processus d’extraction ?
Absolument ! Vous pouvez automatiser ce processus en plaçant le code dans une tâche planifiée ou un script.
### Où puis-je trouver plus de documentation sur Aspose.Cells ?
 Vous pouvez consulter le[Documentation d'Aspose.Cells](https://reference.aspose.com/cells/net/) pour plus de détails et d'exemples.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
