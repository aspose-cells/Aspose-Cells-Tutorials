---
title: Protéger la ligne dans la feuille de calcul Excel
linktitle: Protéger la ligne dans la feuille de calcul Excel
second_title: Référence de l'API Aspose.Cells pour .NET
description: Découvrez dans ce tutoriel comment protéger les lignes d'une feuille de calcul Excel en utilisant Aspose.Cells pour .NET. Tutoriel étape par étape en C#.
weight: 60
url: /fr/net/protect-excel-file/protect-row-in-excel-worksheet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Protéger la ligne dans la feuille de calcul Excel

## Introduction

Lorsque vous travaillez avec des feuilles Excel, il est souvent nécessaire de protéger des lignes spécifiques pour maintenir l'intégrité des données. Que vous gériez un projet d'équipe, supervisiez un rapport financier ou partagiez de la documentation, restreindre l'accès à certaines lignes peut empêcher des modifications indésirables. Dans ce didacticiel, nous découvrirons comment exploiter Aspose.Cells pour .NET pour protéger des lignes spécifiques dans une feuille de calcul Excel. Alors, prenez votre chapeau de codeur et plongeons dans le monde passionnant de la manipulation d'Excel avec C# !

## Prérequis

Avant de passer à la partie pratique, assurons-nous que tout est configuré. Voici quelques prérequis :

1.  Aspose.Cells pour .NET : téléchargez la bibliothèque à partir du[Site Web d'Aspose](https://releases.aspose.com/cells/net/)Assurez-vous d'avoir la dernière version pour toutes les nouvelles fonctionnalités et corrections de bugs.
2. Visual Studio : un environnement de développement intégré (IDE) comme Visual Studio (Community, Professional ou Enterprise) vous aidera à compiler et à exécuter efficacement votre code C#.
3. .NET Framework : vous aurez besoin d'une version compatible de .NET Framework. Aspose.Cells prend en charge plusieurs versions, assurez-vous donc que la vôtre est à jour. 
4. Connaissances de base de C# : une compréhension fondamentale de C# sera bénéfique lorsque nous écrirons notre code tout au long de ce guide.
5.  Documentation de référence : Familiarisez-vous avec la[Documentation d'Aspose.Cells pour .NET](https://reference.aspose.com/cells/net/) pour plus de détails sur les méthodes et les classes utilisées.

## Paquets d'importation

La première étape de notre parcours consiste à importer les packages nécessaires dans notre projet C#. Aspose.Cells fonctionne via un ensemble de classes que nous devons inclure :

```csharp
using System.IO;
using Aspose.Cells;
```

Maintenant que nous avons importé les packages requis, parcourons les étapes pour créer un classeur Excel et protéger une ligne spécifique. 

## Étape 1 : Définir le répertoire

Dans cette étape, nous allons spécifier l'emplacement où notre fichier Excel sera enregistré. Il est important de s'assurer que ce répertoire existe, sinon nous le créerons par programmation si nécessaire.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY"; // Remplacez par le chemin de votre document
bool IsExists = Directory.Exists(dataDir);
if (!IsExists)
{
    Directory.CreateDirectory(dataDir);
}
```
 Dans ce code, remplacez`YOUR DOCUMENT DIRECTORY` avec le chemin réel où vous souhaitez enregistrer votre fichier Excel.

## Étape 2 : Créer un nouveau classeur

Ensuite, nous allons créer un nouveau classeur dans lequel toutes les manipulations auront lieu. Il s'agit d'une étape fondamentale, comme la pose des fondations avant la construction de la maison de vos rêves.

```csharp
Workbook wb = new Workbook();
```
 Cette ligne initialise une nouvelle instance du`Workbook` classe, créant une nouvelle feuille de travail sur laquelle nous pouvons travailler.

## Étape 3 : Accéder à la feuille de travail

Une fois le classeur créé, passons à la première feuille de calcul. N'oubliez pas qu'un fichier Excel peut contenir plusieurs feuilles, il est donc essentiel de choisir la bonne.

```csharp
Worksheet sheet = wb.Worksheets[0]; // Accéder à la première feuille
```

## Étape 4 : déverrouiller toutes les colonnes

Avant de verrouiller une ligne spécifique, il est recommandé de déverrouiller d'abord toutes les colonnes. Cela nous permet de contrôler quelles données restent modifiables ultérieurement.

```csharp
Style style;
StyleFlag flag;

// Parcourez toutes les colonnes et déverrouillez-les
for (int i = 0; i <= 255; i++)
{
    style = sheet.Cells.Columns[(byte)i].Style;
    style.IsLocked = false;
    flag = new StyleFlag();
    flag.Locked = true;
    sheet.Cells.Columns[(byte)i].ApplyStyle(style, flag);
}
```
Cette boucle parcourt les 256 premières colonnes, déverrouillant chacune d'elles pour garantir les autorisations d'édition par défaut.

## Étape 5 : Verrouillage de la ligne spécifique

Nous allons maintenant cibler la première ligne de notre feuille de calcul pour le verrouillage. Cette étape garantit que les utilisateurs ne peuvent pas apporter de modifications non autorisées aux données critiques contenues dans cette ligne.

```csharp
style = sheet.Cells.Rows[0].Style; // Obtenez le style de la première rangée
style.IsLocked = true; // Verrouiller la ligne
flag = new StyleFlag();
flag.Locked = true; // Définir le drapeau de verrouillage
sheet.Cells.ApplyRowStyle(0, style, flag); // Appliquer le style à la première ligne
```
Ici, nous récupérons le style de la première ligne, la marquons comme verrouillée et appliquons le style de verrouillage. Cela revient à mettre un verrou sur un tiroir important, essentiel pour sécuriser les informations sensibles !

## Étape 6 : Protection de la feuille

 Avec notre ligne verrouillée, franchissons cette étape supplémentaire et protégeons entièrement la feuille de calcul. Cela appliquera le verrouillage sur toutes les fonctionnalités définies dans le`ProtectionType`.

```csharp
sheet.Protect(ProtectionType.All); // Protégez la feuille avec toutes les fonctionnalités
```
En appliquant cette protection, les utilisateurs ne peuvent pas modifier la ligne verrouillée ni apporter de modifications susceptibles d'affecter les zones verrouillées.

## Étape 7 : Enregistrer le classeur

La dernière étape consiste à enregistrer le classeur. C'est là que tout notre travail acharné porte ses fruits et que nous pouvons voir notre magnifique feuille de calcul protégée prendre vie !

```csharp
wb.Save(dataDir + "output.out.xls", SaveFormat.Excel97To2003);
```
Assurez-vous que le nom et le format du fichier enregistré correspondent à vos besoins. Dans ce cas, nous l'enregistrons sous un ancien format Excel (Excel 97-2003).

## Conclusion

Et voilà ! Vous avez appris avec succès à protéger une ligne spécifique dans une feuille de calcul Excel à l'aide d'Aspose.Cells pour .NET. Avec seulement quelques lignes de code, vous avez non seulement créé un classeur, mais vous avez également réussi à sécuriser des informations sensibles, garantissant ainsi que vos fichiers Excel restent intacts et fiables. Qu'il s'agisse d'un rapport financier, d'une feuille de présence ou d'un plan de projet collaboratif, la protection des données cruciales est essentielle. 

## FAQ

### Qu'est-ce qu'Aspose.Cells ?
Aspose.Cells est une bibliothèque puissante pour .NET qui permet aux utilisateurs de créer, manipuler et convertir des fichiers Excel par programmation.

### Puis-je protéger plusieurs lignes à la fois avec Aspose.Cells ?
Oui, vous pouvez étendre la technique de verrouillage en parcourant plusieurs lignes et en appliquant des modifications de style similaires à chacune.

### Existe-t-il un moyen de déverrouiller les lignes après la protection ?
 Oui, vous pouvez d'abord déprotéger la feuille, puis ajuster la`IsLocked` propriété des lignes souhaitées, en réappliquant ensuite la protection.

### Aspose.Cells prend-il en charge d’autres formats en plus d’Excel ?
Absolument ! Aspose.Cells peut convertir et enregistrer des classeurs dans différents formats, notamment CSV, PDF et HTML.

### Où puis-je obtenir de l'aide pour Aspose.Cells ?
 Vous pouvez visiter le[Forum d'assistance Aspose](https://forum.aspose.com/c/cells/9) pour obtenir de l'aide et des conseils communautaires.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
