---
title: Extraire un objet OLE à partir d'Excel
linktitle: Extraire un objet OLE à partir d'Excel
second_title: API de traitement Excel Aspose.Cells .NET
description: Découvrez comment extraire des objets OLE à partir de fichiers Excel à l'aide d'Aspose.Cells pour .NET. Guide étape par étape pour une extraction facile.
weight: 10
url: /fr/net/excel-ole-picture-objects/extract-ole-object-from-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extraire un objet OLE à partir d'Excel

## Introduction
Dans le monde technophile d'aujourd'hui, la gestion des fichiers Excel est une tâche courante, en particulier pour les professionnels de l'analyse de données, de la finance et de la gestion de projets. Un aspect souvent négligé est la gestion des objets OLE (Object Linking and Embedding) dans les feuilles de calcul Excel. Il peut s'agir de documents intégrés, d'images ou même de types de données complexes qui jouent un rôle crucial dans l'amélioration des fonctionnalités et de la richesse de vos fichiers Excel. Si vous êtes un utilisateur d'Aspose.Cells cherchant à extraire ces objets OLE par programmation à l'aide de .NET, vous êtes au bon endroit ! Ce guide vous guidera tout au long du processus, en vous assurant de comprendre non seulement comment le faire, mais aussi pourquoi chaque partie du processus est importante.
## Prérequis
Avant de plonger dans les détails de l’extraction d’objets OLE, vous devez mettre en place quelques éléments :
1. Connaissances de base de C# : Si vous connaissez C#, vous êtes déjà sur la bonne voie. Sinon, ne vous inquiétez pas ! Nous allons vous simplifier la tâche.
2. Aspose.Cells installé : vous aurez besoin de la bibliothèque Aspose.Cells. Vous pouvez la télécharger depuis le site[ici](https://releases.aspose.com/cells/net/).
3. Un environnement de développement compatible : assurez-vous d’avoir configuré un environnement de développement .NET, tel que Visual Studio, prêt à l’emploi.
4. Un exemple de fichier Excel : vous aurez besoin d’un fichier Excel avec des objets OLE intégrés pour les tests. 
Une fois ces conditions préalables en place, nous pouvons commencer notre voyage dans le monde de l’extraction d’objets OLE.
## Paquets d'importation
Tout d'abord, importons les packages nécessaires que nous utiliserons dans notre tutoriel. Dans votre projet C#, vous devrez inclure l'espace de noms Aspose.Cells. Voici comment procéder :
```csharp
using System.IO;
using Aspose.Cells;
```
## Étape 1 : définir le répertoire du document
Dans cette étape, nous allons définir le chemin où se trouve notre fichier Excel. Vous vous demandez peut-être pourquoi c'est important. C'est comme préparer le terrain pour une représentation : cela aide le script à savoir où trouver les acteurs (dans notre cas, le fichier Excel).
```csharp
string dataDir = "Your Document Directory";
```
 Remplacer`"Your Document Directory"` avec le chemin réel où se trouve votre fichier Excel (`book1.xls`) est stocké.
## Étape 2 : Ouvrir le fichier Excel
Maintenant que notre répertoire de documents est configuré, l'étape suivante consiste à ouvrir le fichier Excel. Considérez cela comme l'ouverture d'un livre avant de commencer à le lire : il est essentiel de voir ce qu'il contient.
```csharp
Workbook workbook = new Workbook(dataDir + "book1.xls");
```
## Étape 3 : Accéder à la collection d'objets OLE
Chaque feuille de calcul d'un classeur Excel peut contenir divers objets, notamment des objets OLE. Ici, nous accédons à la collection d'objets OLE de la première feuille de calcul. Cela revient à sélectionner une page pour extraire des images et des documents intégrés.
```csharp
Aspose.Cells.Drawing.OleObjectCollection oles = workbook.Worksheets[0].OleObjects;
```
## Étape 4 : Parcourir les objets OLE
Vient maintenant la partie amusante : parcourir tous les objets OLE de notre collection. Cette étape est cruciale car elle nous permet de gérer efficacement plusieurs objets OLE. Imaginez fouiller un coffre au trésor pour trouver des objets de valeur !
```csharp
for (int i = 0; i < oles.Count; i++)
{
    Aspose.Cells.Drawing.OleObject ole = oles[i];
    // Logique supplémentaire pour gérer chaque objet
}
```
## Étape 5 : Spécifiez le nom du fichier de sortie
Au fur et à mesure que nous approfondissons chaque objet OLE, nous devons trouver un nom de fichier pour les objets extraits. Pourquoi ? Parce qu'une fois que nous les avons extraits, nous voulons tout garder organisé afin de pouvoir retrouver facilement nos trésors plus tard.
```csharp
string fileName = dataDir + "ole_" + i + ".";
```
## Étape 6 : Déterminer le type de format de fichier
Chaque objet OLE peut être de différents types (par exemple, des documents, des feuilles de calcul, des images). Il est essentiel de déterminer le type de format afin de pouvoir l'extraire correctement. C'est comme connaître la recette d'un plat : il faut connaître les ingrédients !
```csharp
switch (ole.FileFormatType)
{
    case FileFormatType.Doc:
        fileName += "doc";
        break;
    case FileFormatType.Xlsx:
        fileName += "xlsx";
        break;
    case FileFormatType.Ppt:
        fileName += "ppt";
        break;
    case FileFormatType.Pdf:
        fileName += "pdf";
        break;
    case FileFormatType.Unknown:
        fileName += "jpg";
        break;
    default:
        // Gérer d’autres formats de fichiers
        break;
}
```
## Étape 7 : Enregistrer l’objet OLE
 Passons maintenant à l'enregistrement de l'objet OLE. Si l'objet est un fichier Excel, nous l'enregistrerons à l'aide d'un`MemoryStream` ce qui nous permet de manipuler les données en mémoire avant de les écrire. Cette étape s'apparente à l'emballage de votre trésor avant de l'envoyer à un ami.
```csharp
if (ole.FileFormatType == FileFormatType.Xlsx)
{
    MemoryStream ms = new MemoryStream();
    ms.Write(ole.ObjectData, 0, ole.ObjectData.Length);
    Workbook oleBook = new Workbook(ms);
    oleBook.Settings.IsHidden = false;
    oleBook.Save(dataDir + "Excel_File" + i + ".out.xlsx");
}
```
 Pour les autres types de fichiers, nous utiliserons un`FileStream` pour créer le fichier sur le disque.
```csharp
else
{
    FileStream fs = File.Create(fileName);
    fs.Write(ole.ObjectData, 0, ole.ObjectData.Length);
    fs.Close();
}
```

## Conclusion
Et voilà, vous avez réussi à naviguer dans les eaux de l'extraction d'objets OLE avec Aspose.Cells pour .NET ! En suivant ces étapes, vous pouvez facilement extraire et gérer les objets incorporés de vos fichiers Excel. N'oubliez pas que, comme pour toute compétence précieuse, c'est en forgeant qu'on devient forgeron. Alors, prenez votre temps pour expérimenter avec différents fichiers Excel et vous deviendrez bientôt un pro de l'extraction OLE !
## FAQ
### Que sont les objets OLE dans Excel ?
Les objets OLE sont une technologie qui permet d'incorporer et de lier des documents et des données dans d'autres applications au sein d'une feuille de calcul Excel.
### Pourquoi aurais-je besoin d’extraire des objets OLE ?
L'extraction d'objets OLE vous permet d'accéder et de manipuler des documents ou des images incorporés indépendamment du fichier Excel d'origine.
### Aspose.Cells peut-il gérer tous les types de fichiers intégrés ?
Oui, Aspose.Cells peut gérer divers objets OLE, notamment des documents Word, des feuilles Excel, des présentations PowerPoint et des images.
### Comment installer Aspose.Cells pour .NET ?
 Vous pouvez installer Aspose.Cells en le téléchargeant à partir de leur[page de sortie](https://releases.aspose.com/cells/net/).
### Où puis-je trouver du support pour Aspose.Cells ?
Vous pouvez obtenir de l'aide pour Aspose.Cells sur leur[Forum de soutien](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
