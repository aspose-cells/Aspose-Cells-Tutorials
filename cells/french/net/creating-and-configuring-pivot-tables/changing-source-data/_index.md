---
title: Modifier les données sources d'un tableau croisé dynamique par programmation dans .NET
linktitle: Modifier les données sources d'un tableau croisé dynamique par programmation dans .NET
second_title: API de traitement Excel Aspose.Cells .NET
description: Découvrez comment modifier les données sources du tableau croisé dynamique par programmation à l'aide d'Aspose.Cells pour .NET avec notre didacticiel complet étape par étape.
weight: 10
url: /fr/net/creating-and-configuring-pivot-tables/changing-source-data/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Modifier les données sources d'un tableau croisé dynamique par programmation dans .NET

## Introduction
Dans le monde de l'analyse de données, peu d'outils brillent autant que Microsoft Excel. Chaque jour, d'innombrables utilisateurs dépendent d'Excel pour gérer et analyser des données, mais en coulisses, c'est bien plus complexe que de simplement cliquer et faire glisser. Si vous avez toujours voulu manipuler des fichiers Excel par programmation, en particulier pour modifier les données sources d'un tableau croisé dynamique, vous êtes au bon endroit ! Dans ce guide, nous allons découvrir comment vous pouvez y parvenir en utilisant Aspose.Cells pour .NET. Que vous soyez un développeur chevronné ou que vous vous lanciez simplement dans la mer de la programmation, vous trouverez dans ce didacticiel des informations précieuses et faciles à suivre.
## Prérequis
Avant de commencer notre voyage de modification des données sources d'un tableau croisé dynamique, assurons-nous que tout est configuré et prêt à fonctionner :
1. Visual Studio : assurez-vous d’avoir une copie de Microsoft Visual Studio installée, car nous allons écrire notre code ici.
2. Bibliothèque Aspose.Cells : vous devez avoir téléchargé et référencé la bibliothèque Aspose.Cells dans votre projet. Vous pouvez la télécharger[ici](https://releases.aspose.com/cells/net/).
3. Connaissances de base de C# : bien que ce didacticiel soit simplifié, une bonne compréhension de C# vous aidera à mieux comprendre le code.
4. Fichier Excel : vous devriez avoir un exemple de fichier Excel (comme « Book1.xlsx ») contenant un tableau croisé dynamique que nous pouvons manipuler.
Très bien, avec ces prérequis vérifiés, nous pouvons procéder à l’importation des packages nécessaires et commencer à coder !
## Paquets d'importation
Tout d'abord, importons les packages dont nous aurons besoin. Ouvrez votre projet C# dans Visual Studio et ajoutez les directives using suivantes en haut de votre fichier de code :
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```
Ces espaces de noms vous donneront accès aux classes essentielles nécessaires pour travailler avec des fichiers Excel et manipuler leur contenu à l'aide d'Aspose.Cells.

Décomposons maintenant le processus en étapes faciles à gérer. Nous allons voir comment ouvrir un fichier Excel, modifier la feuille de calcul, changer la source de données du tableau croisé dynamique et enregistrer les résultats.
## Étape 1 : Définissez votre répertoire de documents
 Tout d'abord, vous devez spécifier où se trouve votre fichier Excel. Modifiez le`dataDir` variable pour pointer vers le dossier contenant votre "Book1.xlsx".
```csharp
// Le chemin vers le répertoire des documents.
string dataDir = "Your Document Directory";
```
Cette ligne définit le répertoire dans lequel votre fichier Excel est stocké, ce qui facilite son accès ultérieur.
## Étape 2 : Spécifier le chemin d’entrée
Ensuite, créons une chaîne pour spécifier le chemin complet vers votre fichier Excel d'entrée :
```csharp
string InputPath = dataDir + "Book1.xlsx";
```
Cela permet de rationaliser l'accès à vos fichiers ; vous n'aurez pas à continuer à saisir le même chemin plusieurs fois dans votre code.
## Étape 3 : Créer un flux de fichiers
 Il est maintenant temps d'ouvrir le fichier Excel. Nous allons créer un`FileStream` qui vous permet de lire le contenu du fichier Excel :
```csharp
// Créer un flux de fichiers contenant le fichier Excel à ouvrir
FileStream fstream = new FileStream(InputPath, FileMode.Open);
```
Cette ligne ouvre le fichier en mode lecture, nous permettant d'accéder à ses données.
## Étape 4 : Charger le classeur
Une fois le flux de fichiers en place, l’étape suivante consiste à charger le classeur :
```csharp
// Ouverture du fichier Excel via le flux de fichiers
Workbook workbook = new Workbook(fstream);
```
 Cette commande prend votre fichier Excel et le charge dans un`Workbook` objet. Une fois chargé, vous pouvez manipuler le fichier selon vos besoins.
## Étape 5 : Accéder à la feuille de travail
Il est temps de plonger dans les détails. Nous allons accéder à la première feuille de calcul du classeur :
```csharp
// Accéder à la première feuille de calcul du fichier Excel
Worksheet worksheet = workbook.Worksheets[0];
```
Cela vous donne un accès direct aux données de la première feuille de calcul, ce qui facilite leur modification.
## Étape 6 : Renseigner les nouvelles données
Ensuite, nous souhaitons insérer de nouvelles données dans les cellules. Dans cet exemple, nous allons ajouter quelques données d'échantillon :
```csharp
// Remplissage de nouvelles données dans les cellules de la feuille de calcul
worksheet.Cells["A9"].PutValue("Golf");
worksheet.Cells["B9"].PutValue("Qtr4");
worksheet.Cells["C9"].PutValue(7000);
```
 Ici, nous mettons les valeurs « Golf », « Qtr4 » et`7000` dans des cellules spécifiques. Vous pouvez modifier ces valeurs selon vos besoins.
## Étape 7 : modifier la plage nommée
Nous allons maintenant modifier la plage nommée à laquelle le tableau croisé dynamique fait référence. Cela implique de créer ou de mettre à jour une plage :
```csharp
// Modification de la plage nommée « DataSource »
Range range = worksheet.Cells.CreateRange(0,0,9,3);
range.Name = "DataSource";
```
En définissant une nouvelle plage, nous garantissons que le tableau croisé dynamique utilise ces nouvelles données lors de son actualisation.
## Étape 8 : Enregistrer le fichier Excel modifié
Après toutes ces modifications, il est essentiel de sauvegarder votre travail ! Sauvegardons le classeur modifié :
```csharp
// Sauvegarde du fichier Excel modifié
workbook.Save(dataDir + "output.xls");
```
Cette commande enregistre le classeur dans un nouveau fichier, de sorte que vous n'écrasez pas votre fichier d'origine à moins que vous ne le souhaitiez !
## Étape 9 : Fermer le flux de fichiers
Enfin, il est essentiel de fermer le flux de fichiers pour libérer toutes les ressources que vous utilisez :
```csharp
// Fermeture du flux de fichiers pour libérer toutes les ressources
fstream.Close();
```
Cette étape garantit que votre application ne perd pas de mémoire et reste efficace.
## Conclusion
Félicitations ! Vous venez de modifier avec succès les données sources d'un tableau croisé dynamique par programmation dans .NET à l'aide d'Aspose.Cells. Cette fonctionnalité ouvre de nombreuses possibilités pour automatiser les tâches Excel et améliorer votre flux de travail. Que vous mettiez à jour des rapports financiers, suiviez des données de vente ou que vous jouiez simplement avec des ensembles de données, avoir la possibilité de le faire par programmation peut vous faire gagner beaucoup de temps et réduire le risque d'erreurs.

## FAQ
### Qu'est-ce qu'Aspose.Cells ?
Aspose.Cells est une puissante bibliothèque .NET permettant de travailler avec des fichiers Excel, permettant aux utilisateurs de créer, modifier et manipuler des documents Excel par programmation.
### Puis-je modifier les données sources des tableaux croisés dynamiques existants à l’aide de cette méthode ?
Absolument ! Cette méthode vous permet de mettre à jour la source de données des tableaux croisés dynamiques existants dans votre classeur Excel.
### Dois-je avoir Office installé pour utiliser Aspose.Cells ?
Non ! Aspose.Cells est une bibliothèque autonome, ce qui signifie que vous n'avez pas besoin d'installer Microsoft Office pour travailler avec des fichiers Excel.
### L'utilisation d'Aspose.Cells est-elle gratuite ?
Aspose.Cells propose une version d'essai gratuite, mais pour bénéficier de toutes les fonctionnalités, vous devrez acheter une licence. Vous pouvez trouver les détails[ici](https://purchase.aspose.com/buy).
### Où puis-je trouver plus d’exemples et de support ?
 Pour plus d'exemples et de support, consultez le[Documentation d'Aspose.Cells](https://reference.aspose.com/cells/net/) et leur forum communautaire[ici](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
