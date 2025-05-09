---
"description": "Découvrez comment extraire des fichiers MOL intégrés à partir de classeurs Excel à l'aide d'Aspose.Cells pour .NET dans ce didacticiel détaillé étape par étape."
"linktitle": "Extraire le fichier Mol intégré du classeur"
"second_title": "API de traitement Excel Aspose.Cells .NET"
"title": "Extraire le fichier Mol intégré du classeur"
"url": "/fr/net/workbook-operations/extract-embedded-mol-file/"
"weight": 18
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Extraire le fichier Mol intégré du classeur

## Introduction
Lors de la gestion des données dans des classeurs Excel, on rencontre parfois des objets incorporés au format non standard. L'un de ces formats est le fichier de structure moléculaire (MOL), couramment utilisé en chimie pour représenter les informations moléculaires. Si vous souhaitez extraire ces fichiers MOL d'un classeur Excel avec Aspose.Cells pour .NET, vous êtes au bon endroit. Dans cet article, nous vous guiderons pas à pas, en démystifiant chaque étape.
## Prérequis
Avant de vous lancer dans le code, il est essentiel de vous assurer de posséder les compétences et les outils nécessaires. Voici ce dont vous aurez besoin :
1. Compréhension de base de la programmation .NET : vous devez être familiarisé avec C# et le framework .NET.
2. Aspose.Cells pour .NET : Assurez-vous de disposer de la bibliothèque Aspose.Cells. Vous pouvez [téléchargez-le ici](https://releases.aspose.com/cells/net/).
3. Un IDE : vous pouvez utiliser Visual Studio ou tout autre IDE compatible .NET.
4. Classeur Excel avec fichiers MOL intégrés : Pour ce tutoriel, vous avez besoin d'un fichier Excel contenant des objets MOL. Vous pouvez créer le vôtre ou utiliser un fichier d'exemple.
## Importer des packages
Pour commencer, vous devez importer les espaces de noms nécessaires dans votre projet. Ceci est essentiel pour accéder aux fonctionnalités d'Aspose.Cells. Voici comment procéder :

```csharp
using Aspose.Cells.Drawing;
using Aspose.Cells.WebExtensions;
using System;
using System.IO;
```

Ces espaces de noms vous permettront de manipuler des classeurs, d'accéder à des feuilles de calcul et de travailler avec des fichiers en général.
Maintenant que nous avons réglé nos prérequis, plongeons dans le code et comprenons chaque étape impliquée dans l'extraction de fichiers MOL intégrés à partir d'un classeur Excel. 
## Étape 1 : Configuration de vos répertoires
La première étape consiste à définir l'emplacement de votre document source et celui où vous souhaitez enregistrer les fichiers MOL extraits. Configurez ces répertoires.
```csharp
string SourceDir = "Your Document Directory"; // Remplacez par le chemin de votre répertoire
string outputDir = "Your Document Directory"; // Remplacez par votre chemin de sortie
```
Ici, vous remplacez `"Your Document Directory"` avec le chemin d'accès à vos répertoires actuels. Il est important que les répertoires source et de sortie soient accessibles à votre application.
## Étape 2 : chargement du classeur
Une fois vos répertoires configurés, l'étape suivante consiste à charger le classeur Excel. C'est parti !

```csharp
Workbook workbook = new Workbook(SourceDir + "EmbeddedMolSample.xlsx");
```

Nous créons une instance du `Workbook` classe et en passant le chemin vers notre fichier Excel nommé `EmbeddedMolSample.xlsx`Cette étape initialise le classeur, vous permettant d’accéder à son contenu.
## Étape 3 : Itération sur les feuilles de calcul
Maintenant que votre classeur est chargé, parcourez chaque feuille de calcul. Cela vous permet d'examiner chaque feuille à la recherche d'objets incorporés.

```csharp
var index = 1; // Utilisé pour nommer les fichiers MOL extraits
foreach (Worksheet sheet in workbook.Worksheets)
{
    OleObjectCollection oles = sheet.OleObjects;
    // La logique d'extraction ultérieure va ici
}
```

Ici, vous utilisez un `foreach` boucle pour naviguer dans les feuilles de calcul. Pour chaque feuille de calcul, vous accédez à la `OleObjects` collection, qui contient tous les objets intégrés.
## Étape 4 : Extraction des fichiers MOL
Vient maintenant l'étape cruciale : l'extraction des fichiers MOL des objets OLE. Cela nécessite une autre boucle dans la boucle de la feuille de calcul.

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

Pour chaque objet OLE que vous avez trouvé, vous créez un nouveau fichier dans le répertoire de sortie. `ObjectData` propriété de la `OleObject` contient les données de l'objet incorporé, que vous écrivez dans un fichier nouvellement créé à l'aide d'un `FileStream`. Le fichier est nommé séquentiellement (`OleObject1.mol`, `OleObject2.mol`, etc.) en fonction de la `index` variable.
## Étape 5 : Confirmation de l’achèvement du processus
Enfin, une fois tous les fichiers MOL extraits, il est recommandé d'informer l'utilisateur que le processus s'est terminé avec succès.

```csharp
Console.WriteLine("ExtractEmbeddedMolFile executed successfully.");
```

Cette ligne affiche simplement un message sur la console vous informant que l'extraction a réussi. C'est une fonctionnalité intéressante pour recueillir les commentaires des utilisateurs.
## Conclusion
Et voilà ! Vous avez extrait avec succès des fichiers MOL incorporés d'un classeur Excel avec Aspose.Cells pour .NET. Ce processus intègre quelques étapes clés, garantissant une approche structurée de la gestion des objets incorporés. Que vous soyez dans la recherche scientifique, l'analyse chimique ou que vous manipuliez simplement des ensembles de données complexes, savoir extraire et manipuler ces types de fichiers peut faire toute la différence dans la gestion de vos informations. 
## FAQ
### Puis-je extraire d’autres types de fichiers en plus de MOL à partir d’Excel ?
Oui, vous pouvez extraire divers autres types de fichiers intégrés avec des techniques similaires.
### Aspose.Cells est-il gratuit à utiliser ?
Aspose.Cells est une bibliothèque commerciale, mais vous pouvez [essayez-le gratuitement pendant une période limitée](https://releases.aspose.com/).
### Cette méthode fonctionne-t-elle avec toutes les versions d’Excel ?
Oui, tant que le format de fichier est pris en charge par Aspose.Cells.
### Puis-je automatiser ce processus d’extraction ?
Absolument ! Vous pouvez automatiser ce processus en plaçant le code dans une tâche planifiée ou un script.
### Où puis-je trouver plus de documentation sur Aspose.Cells ?
Vous pouvez consulter le [Documentation d'Aspose.Cells](https://reference.aspose.com/cells/net/) pour plus de détails et d'exemples.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}