---
title: Dissocier les lignes et les colonnes dans Excel avec Aspose.Cells
linktitle: Dissocier les lignes et les colonnes dans Excel avec Aspose.Cells
second_title: API de traitement Excel Aspose.Cells .NET
description: Découvrez comment dissocier des lignes et des colonnes dans Excel à l'aide d'Aspose.Cells pour .NET avec ce guide complet. Simplifiez la manipulation de vos données Excel.
weight: 15
url: /fr/net/row-and-column-management/ungrouping-rows-and-columns/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Dissocier les lignes et les colonnes dans Excel avec Aspose.Cells

## Introduction
Lorsque vous manipulez des fichiers Excel, vous pouvez vous retrouver dans des situations où vous devez dissocier des lignes et des colonnes. Que vous souhaitiez nettoyer une feuille de calcul ou reformater des données pour une meilleure présentation, Aspose.Cells pour .NET est un outil fantastique qui simplifie le processus. Dans ce didacticiel, je vous guiderai à travers les étapes permettant de dissocier des lignes et des colonnes dans Excel à l'aide d'Aspose.Cells. À la fin, vous aurez une solide compréhension de la manière de travailler avec des fichiers Excel par programmation.
## Prérequis
Avant de plonger dans le code, assurons-nous que tout est configuré. Voici ce dont vous aurez besoin :
1.  Visual Studio : vous devez avoir une version fonctionnelle de Visual Studio installée sur votre ordinateur. Si vous ne l'avez pas encore, vous pouvez la télécharger à partir de[Site de Visual Studio](https://visualstudio.microsoft.com/).
2. Aspose.Cells pour .NET : vous devrez télécharger la bibliothèque Aspose.Cells. Vous pouvez la récupérer à partir du[Page de sortie d'Aspose](https://releases.aspose.com/cells/net/) Assurez-vous de disposer des licences nécessaires, qui peuvent être achetées ou obtenues via un[permis temporaire](https://purchase.aspose.com/temporary-license/).
3. Connaissances de base de C# : une compréhension fondamentale de la programmation C# vous aidera à suivre plus facilement.
Une fois que tout est prêt, nous pouvons passer à la partie amusante : le code !
## Paquets d'importation
Pour commencer, vous devez importer les packages nécessaires dans votre projet C#. Voici comment procéder :
1. Ouvrez votre projet dans Visual Studio.
2. Ajoutez une référence à la bibliothèque Aspose.Cells. Pour ce faire, cliquez avec le bouton droit sur les références de votre projet et sélectionnez Ajouter une référence. Accédez à l'emplacement où vous avez enregistré la DLL Aspose.Cells.
3. En haut de votre fichier C#, ajoutez les directives using suivantes :
```csharp
using System.IO;
using Aspose.Cells;
```
Maintenant que tout est configuré, passons en revue les étapes à suivre pour dissocier les lignes et les colonnes de votre feuille Excel. 
## Étape 1 : Définir le répertoire des documents
Tout d'abord, vous devez spécifier le répertoire dans lequel se trouve votre fichier Excel. Vous pouvez le configurer comme suit :
```csharp
// Le chemin vers le répertoire des documents.
string dataDir = "Your Document Directory";
```
 Remplacer`"Your Document Directory"` avec le chemin réel sur votre ordinateur où le fichier Excel est enregistré. 
## Étape 2 : Créer un flux de fichiers
Ensuite, vous devez créer un flux de fichiers pour ouvrir le fichier Excel. Voici comment procéder :
```csharp
// Créer un flux de fichiers contenant le fichier Excel à ouvrir
FileStream fstream = new FileStream(dataDir + "book1.xls", FileMode.Open);
```
 Ici, vous ouvrez le fichier nommé`book1.xls`Assurez-vous que ce fichier existe dans le répertoire spécifié, sinon vous rencontrerez une erreur de fichier introuvable.
## Étape 3 : instancier un objet classeur
Chargeons maintenant le fichier Excel dans un objet Workbook. Cela vous permet de manipuler le classeur par programmation :
```csharp
// Instanciation d'un objet Workbook
// Ouverture du fichier Excel via le flux de fichiers
Workbook workbook = new Workbook(fstream);
```
Avec cette ligne de code, vous avez chargé avec succès le fichier Excel en mémoire et êtes prêt à travailler avec lui.
## Étape 4 : Accéder à la feuille de travail
Une fois que vous avez le classeur, l'étape suivante consiste à accéder à la feuille de calcul spécifique dans laquelle vous souhaitez dissocier les lignes et les colonnes. Voici comment procéder :
```csharp
// Accéder à la première feuille de calcul du fichier Excel
Worksheet worksheet = workbook.Worksheets[0];
```
Dans ce cas, nous accédons à la première feuille de calcul. Si vos données se trouvent sur une autre feuille, vous pouvez modifier l'index en conséquence.
## Étape 5 : dissocier les lignes
Vient maintenant la partie passionnante ! Dégroupons les six premières lignes (de la ligne 0 à la ligne 5). Utilisez le code suivant :
```csharp
// Dégrouper les six premières lignes (de 0 à 5)
worksheet.Cells.UngroupRows(0, 5);
```
Cette méthode supprime tout regroupement appliqué aux lignes spécifiées. C'est aussi simple que ça !
## Étape 6 : Dissocier les colonnes
Tout comme les lignes, vous pouvez également dissocier les colonnes. Voici comment dissocier les trois premières colonnes (de la colonne 0 à la colonne 2) :
```csharp
// Dégrouper les trois premières colonnes (de 0 à 2)
worksheet.Cells.UngroupColumns(0, 2);
```
## Étape 7 : Enregistrer le fichier Excel modifié
 Une fois que vous avez dissocié les lignes et les colonnes, l'étape suivante consiste à enregistrer les modifications dans un fichier Excel. Vous pouvez le faire en utilisant l'`Save` méthode:
```csharp
// Sauvegarde du fichier Excel modifié
workbook.Save(dataDir + "output.xls");
```
 Dans cet exemple, nous enregistrons le fichier modifié sous`output.xls`Vous pouvez modifier le nom du fichier comme vous le souhaitez.
## Étape 8 : Fermer le flux de fichiers
Enfin, pour libérer des ressources, vous devez fermer le flux de fichiers :
```csharp
// Fermeture du flux de fichiers pour libérer toutes les ressources
fstream.Close();
```
Il s’agit d’une bonne pratique pour garantir que votre application ne conserve pas les descripteurs de fichiers plus longtemps que nécessaire.
## Conclusion
Et voilà ! Vous avez appris avec succès à dissocier des lignes et des colonnes dans un fichier Excel à l'aide d'Aspose.Cells pour .NET. Avec seulement quelques lignes de code, vous pouvez apporter des modifications importantes à vos fichiers Excel par programmation. Que vous automatisiez des rapports ou prépariez des données pour l'analyse, la maîtrise de ces techniques peut vous faire gagner beaucoup de temps.
## FAQ
### Qu'est-ce qu'Aspose.Cells ?
Aspose.Cells est une bibliothèque puissante permettant de travailler avec des fichiers Excel dans des applications .NET, permettant une manipulation, une conversion et une création faciles de feuilles de calcul.
### Puis-je dissocier des lignes et des colonnes dans Excel à l’aide d’autres bibliothèques ?
Oui, il existe d’autres bibliothèques disponibles pour la manipulation d’Excel dans .NET, mais Aspose.Cells offre des fonctionnalités étendues et une facilité d’utilisation.
### Existe-t-il un moyen d’annuler les modifications après l’enregistrement ?
Une fois que vous avez enregistré un fichier Excel, l'état précédent ne peut pas être restauré à moins que vous ne disposiez d'une sauvegarde du fichier d'origine.
### Comment obtenir de l'aide pour Aspose.Cells ?
 Vous pouvez trouver de l'aide en visitant le[Forum d'assistance Aspose](https://forum.aspose.com/c/cells/9), où vous pouvez poser des questions et trouver des solutions.
### Puis-je utiliser Aspose.Cells sans licence ?
Oui, vous pouvez utiliser Aspose.Cells gratuitement avec certaines limitations, et vous pouvez commencer avec un[permis temporaire](https://purchase.aspose.com/temporary-license/) pour une fonctionnalité complète.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
