---
title: Définition du nom de la police dans Excel
linktitle: Définition du nom de la police dans Excel
second_title: API de traitement Excel Aspose.Cells .NET
description: Découvrez comment définir le nom de la police dans une feuille de calcul Excel à l'aide d'Aspose.Cells pour .NET dans ce didacticiel étape par étape.
weight: 11
url: /fr/net/working-with-fonts-in-excel/setting-font-name/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Définition du nom de la police dans Excel

## Introduction
Lorsque vous travaillez avec des fichiers Excel dans des applications .NET, vous avez besoin d'une solution à la fois puissante et conviviale. Découvrez Aspose.Cells, une bibliothèque fantastique qui permet aux développeurs de créer, de manipuler et de convertir des fichiers Excel de manière transparente. Que vous cherchiez à automatiser des rapports ou à personnaliser la mise en forme d'une feuille de calcul, Aspose.Cells est votre boîte à outils de référence. Dans ce didacticiel, nous verrons comment définir le nom de la police dans une feuille de calcul Excel à l'aide d'Aspose.Cells pour .NET.
## Prérequis
Avant de plonger dans le vif du sujet, assurons-nous que vous disposez de tout ce dont vous avez besoin :
1.  Aspose.Cells pour .NET : vous devez avoir installé cette bibliothèque. Vous pouvez la télécharger à partir du[Site d'Aspose](https://releases.aspose.com/cells/net/).
2. Visual Studio : un environnement de développement dans lequel vous pouvez écrire et tester votre code.
3. Connaissances de base de C# : la familiarité avec la programmation C# vous aidera à mieux comprendre les extraits de code.
4. .NET Framework : assurez-vous que votre projet est configuré pour utiliser le .NET Framework compatible avec Aspose.Cells.
Une fois les prérequis couverts, vous serez prêt à partir !
## Paquets d'importation
Pour travailler avec Aspose.Cells, vous devez d'abord importer les espaces de noms requis dans votre code C#. Voici comment procéder :
```csharp
using System.IO;
using Aspose.Cells;
```
Cela vous permet d'accéder à toutes les classes et méthodes de la bibliothèque Aspose.Cells, qui seront essentielles pour nos tâches de manipulation Excel.
Maintenant que tout est en place, décomposons le processus de définition du nom de la police dans un fichier Excel en étapes faciles à suivre.
## Étape 1 : Spécifiez votre répertoire de documents
Avant de commencer à travailler avec des fichiers Excel, vous devez définir l'emplacement de stockage de vos fichiers. Cette étape est essentielle pour garantir que votre application sache où enregistrer le fichier de sortie.
```csharp
// Le chemin vers le répertoire des documents.
string dataDir = "Your Document Directory";
```
 Remplacer`"Your Document Directory"` avec le chemin réel sur votre système où vous souhaitez enregistrer le fichier Excel. 
## Étape 2 : créer le répertoire s’il n’existe pas
Il est toujours judicieux de vérifier que le répertoire dans lequel vous souhaitez enregistrer votre fichier existe. Si ce n'est pas le cas, nous le créerons.
```csharp
// Créez un répertoire s'il n'est pas déjà présent.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Cet extrait vérifie si le répertoire existe. Si ce n'est pas le cas, il crée un nouveau répertoire au chemin spécifié. 
## Étape 3 : instancier un objet classeur
 Ensuite, vous devez créer un`Workbook`objet, qui représente votre fichier Excel en mémoire.
```csharp
// Instanciation d'un objet Workbook
Workbook workbook = new Workbook();
```
 Pensez à la`Workbook` objet comme une toile vierge sur laquelle vous ajouterez vos données et votre formatage.
## Étape 4 : Ajouter une nouvelle feuille de calcul
Ajoutons maintenant une nouvelle feuille de calcul au classeur. Chaque classeur peut contenir plusieurs feuilles de calcul et vous pouvez en ajouter autant que vous le souhaitez.
```csharp
// Ajout d'une nouvelle feuille de calcul à l'objet Excel
int i = workbook.Worksheets.Add();
```
 Ici, nous ajoutons une nouvelle feuille de calcul et obtenons son index (dans ce cas, l'index est stocké dans`i`).
## Étape 5 : Obtenir une référence à la nouvelle feuille de calcul
Pour travailler avec la feuille de calcul que nous venons d’ajouter, nous devons obtenir une référence à celle-ci en utilisant son index.
```csharp
// Obtention de la référence de la feuille de calcul nouvellement ajoutée en passant son index de feuille
Worksheet worksheet = workbook.Worksheets[i];
```
Avec cette ligne, nous avons référencé avec succès la feuille de calcul nouvellement créée et pouvons maintenant commencer à la manipuler.
## Étape 6 : Accéder à une cellule spécifique
Supposons que vous souhaitiez définir le nom de la police pour une cellule spécifique. Ici, nous allons accéder à la cellule « A1 » de la feuille de calcul.
```csharp
// Accéder à la cellule « A1 » à partir de la feuille de calcul
Aspose.Cells.Cell cell = worksheet.Cells["A1"];
```
En ciblant la cellule « A1 », vous pouvez modifier son contenu et son style.
## Étape 7 : ajouter de la valeur à la cellule
Il est maintenant temps d'insérer du texte dans la cellule sélectionnée. Nous allons le définir comme une salutation amicale !
```csharp
// Ajout de valeur à la cellule « A1 »
cell.PutValue("Hello Aspose!");
```
Cette commande remplit la cellule « A1 » avec le texte « Bonjour Aspose ! » Et voilà, notre feuille de calcul commence à prendre forme !
## Étape 8 : Obtenir le style de cellule
Pour modifier le nom de la police, vous devez travailler avec le style de la cellule. Voici comment récupérer le style actuel de la cellule.
```csharp
// Obtention du style de la cellule
Style style = cell.GetStyle();
```
En obtenant le style de la cellule, vous accédez à ses options de formatage, notamment le nom de la police, la taille, la couleur, etc.
## Étape 9 : Définir le nom de la police
Voici la partie intéressante ! Vous pouvez maintenant définir le nom de la police pour le style de cellule. Modifions-le en « Times New Roman ».
```csharp
// Définir le nom de la police sur « Times New Roman »
style.Font.Name = "Times New Roman";
```
N'hésitez pas à expérimenter avec différents noms de polices pour voir à quoi ils ressemblent dans votre fichier Excel !
## Étape 10 : Appliquer le style à la cellule
Maintenant que vous avez défini le nom de police souhaité, il est temps d'appliquer ce style à la cellule.
```csharp
// Appliquer le style à la cellule
cell.SetStyle(style);
```
Cette commande met à jour la cellule avec le nouveau style que vous venez de créer.
## Étape 11 : Enregistrer le fichier Excel
La dernière étape consiste à enregistrer votre travail. Vous enregistrerez le classeur au format Excel que vous avez spécifié.
```csharp
// Sauvegarde du fichier Excel
workbook.Save(dataDir + "book1.out.xls", SaveFormat.Excel97To2003);
```
Dans cette ligne, nous enregistrons le classeur sous le nom « book1.out.xls » dans le répertoire que nous avons spécifié précédemment. N'oubliez pas que`SaveFormat` peut être ajusté en fonction de vos besoins !
## Conclusion
Et voilà ! Vous avez défini avec succès le nom de la police dans une feuille de calcul Excel à l'aide d'Aspose.Cells pour .NET. Cette bibliothèque simplifie la manipulation des fichiers Excel, permettant un degré élevé de personnalisation. En suivant ces étapes, vous pouvez facilement modifier d'autres aspects de vos feuilles de calcul, créant ainsi des documents d'aspect professionnel adaptés à vos besoins. 
## FAQ
### Puis-je également modifier la taille de la police ?  
 Oui, vous pouvez modifier la taille de la police en définissant`style.Font.Size = newSize;` où`newSize` est la taille de police souhaitée.
### Quels autres styles puis-je appliquer à une cellule ?  
 Vous pouvez modifier la couleur de la police, la couleur d'arrière-plan, les bordures, l'alignement et bien plus encore à l'aide de l'`Style` objet.
### L'utilisation d'Aspose.Cells est-elle gratuite ?  
 Aspose.Cells est un produit commercial, mais vous pouvez commencer avec un[essai gratuit](https://releases.aspose.com/) pour évaluer ses caractéristiques.
### Puis-je manipuler plusieurs feuilles de calcul à la fois ?  
Absolument ! Vous pouvez parcourir`workbook.Worksheets` pour accéder et modifier plusieurs feuilles de calcul dans le même classeur.
### Où puis-je trouver de l’aide si je rencontre des problèmes ?  
 Vous pouvez visiter le[Forum d'assistance Aspose](https://forum.aspose.com/c/cells/9) pour obtenir de l'aide concernant toute question ou tout problème que vous rencontrez.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
