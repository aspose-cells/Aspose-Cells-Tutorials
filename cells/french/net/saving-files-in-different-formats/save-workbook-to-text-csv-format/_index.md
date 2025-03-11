---
title: Enregistrer le classeur au format texte CSV
linktitle: Enregistrer le classeur au format texte CSV
second_title: API de traitement Excel Aspose.Cells .NET
description: Découvrez comment convertir sans effort des classeurs Excel au format CSV avec Aspose.Cells dans ce didacticiel complet, étape par étape, conçu pour les développeurs .NET.
weight: 17
url: /fr/net/saving-files-in-different-formats/save-workbook-to-text-csv-format/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Enregistrer le classeur au format texte CSV

## Introduction
Lorsque vous traitez des données, le format que vous choisissez peut réellement déterminer la facilité avec laquelle vous pouvez les utiliser. Parmi les formats les plus courants pour la gestion des données tabulaires figure le format CSV (Comma-Separated Values). Si vous êtes un développeur travaillant avec des fichiers Excel et que vous devez convertir des classeurs au format CSV, Aspose.Cells pour .NET est une bibliothèque fantastique qui simplifie cette tâche. Dans ce didacticiel, nous allons décomposer les étapes pour convertir un classeur Excel en un format texte CSV de manière transparente.
## Prérequis
Avant de commencer, assurons-nous que vous avez tout en place pour commencer :
1. Connaissances de base de C# et .NET : Étant donné que nous allons écrire du code en C#, une familiarité avec le langage et le framework .NET est essentielle.
2. Bibliothèque Aspose.Cells : assurez-vous que la bibliothèque Aspose.Cells pour .NET est installée dans votre environnement de développement. Vous pouvez la télécharger[ici](https://releases.aspose.com/cells/net/).
3. Visual Studio ou tout autre IDE C# : vous aurez besoin d'un environnement de développement intégré (IDE) pour écrire et exécuter votre code. Visual Studio est un choix populaire.
4. Classeur Excel : préparez un exemple de classeur Excel (par exemple, « book1.xls ») contenant des données pour tester la conversion.
## Paquets d'importation
Maintenant que nous avons couvert nos prérequis, la première étape du processus consiste à importer les packages nécessaires. Dans votre projet C#, vous devez inclure l'espace de noms suivant en haut de votre fichier de code :
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
Ces espaces de noms vous donneront accès aux classes et méthodes nécessaires pour travailler avec des fichiers Excel et gérer les flux de mémoire.
## Étape 1 : Définir le chemin d’accès au répertoire des documents
La première étape de notre processus consiste à définir où sont stockés nos documents (classeurs Excel). Cela est essentiel car cela permet à notre programme de savoir où trouver les fichiers qu'il doit traiter. 
```csharp
// Le chemin vers le répertoire des documents.
string dataDir = "Your Document Directory";
```
 Assurez-vous de remplacer`"Your Document Directory"` avec le chemin réel où se trouve votre fichier « book1.xls ». Il peut s'agir d'un répertoire sur votre ordinateur ou d'un chemin vers un serveur.
## Étape 2 : chargez votre classeur source
Ensuite, nous devons charger le classeur Excel qui sera converti au format CSV.
```csharp
// Chargez votre classeur source
Workbook workbook = new Workbook(dataDir + "book1.xls");
```
 Le`Workbook` La classe de la bibliothèque Aspose.Cells permet la manipulation et l'accès aux classeurs Excel. En transmettant le chemin du fichier, nous chargeons le classeur spécifié pour le traitement.
## Étape 3 : Initialiser un tableau d'octets pour les données du classeur
Avant de commencer à convertir le classeur en CSV, nous devons initialiser un tableau d’octets vide qui contiendra éventuellement toutes les données de la feuille de calcul.
```csharp
// Tableau de 0 octet
byte[] workbookData = new byte[0];
```
Ce tableau d'octets combinera les données de chaque feuille de calcul en une seule structure que nous pourrons écrire dans un fichier ultérieurement.
## Étape 4 : Configurer les options d’enregistrement du texte
Maintenant, configurons les options pour la façon dont nous souhaitons enregistrer le format de texte. Vous pouvez choisir des délimiteurs personnalisés ou vous en tenir aux tabulations.
```csharp
// Options d'enregistrement du texte. Vous pouvez utiliser n'importe quel type de séparateur
TxtSaveOptions opts = new TxtSaveOptions();
opts.Separator = '\t'; // Définition de l'onglet comme séparateur
```
 Dans cet exemple, nous utilisons un caractère de tabulation comme séparateur. Vous pouvez remplacer`'\t'` avec le caractère de votre choix, comme une virgule (`,`), selon la façon dont vous souhaitez formater votre fichier CSV.
## Étape 5 : Parcourez chaque feuille de calcul
 Ensuite, nous allons parcourir toutes les feuilles de calcul du classeur, en enregistrant chacune d'elles dans notre`workbookData` tableau, mais vous devez d'abord sélectionner la feuille de calcul sur laquelle travailler.
```csharp
// Copiez chaque donnée de la feuille de calcul au format texte dans le tableau de données du classeur
for (int idx = 0; idx < workbook.Worksheets.Count; idx++)
{
    // Enregistrer la feuille de calcul active au format texte
    MemoryStream ms = new MemoryStream();
    workbook.Worksheets.ActiveSheetIndex = idx;
    workbook.Save(ms, opts);
```
 La boucle parcourt chaque feuille de calcul du classeur.`ActiveSheetIndex` est défini de telle sorte qu'à chaque fois que nous parcourons la boucle, nous enregistrons la feuille de calcul actuelle. Les résultats seront enregistrés en mémoire à l'aide d'un`MemoryStream`.
## Étape 6 : Récupérer les données de la feuille de calcul
 Après avoir enregistré une feuille de calcul dans le flux de mémoire, l’étape suivante consiste à récupérer ces données et à les ajouter à notre`workbookData` tableau.
```csharp
    // Enregistrer les données de la feuille de calcul dans un tableau de données de feuille
    ms.Position = 0; // Réinitialiser la position du flux de mémoire
    byte[] sheetData = ms.ToArray(); // Obtenir le tableau d'octets
```
`ms.Position = 0;` réinitialise la position pour la lecture après l'écriture. Ensuite, nous utilisons`ToArray()` pour convertir le flux mémoire en un tableau d'octets contenant les données de la feuille de calcul.
## Étape 7 : combiner les données de la feuille de calcul
 Maintenant, nous allons combiner les données de chaque feuille de calcul en une seule`workbookData` tableau initialisé plus tôt.
```csharp
    // Combinez les données de cette feuille de calcul dans un tableau de données de classeur
    byte[] combinedArray = new byte[workbookData.Length + sheetData.Length];
    Array.Copy(workbookData, 0, combinedArray, 0, workbookData.Length);
    Array.Copy(sheetData, 0, combinedArray, workbookData.Length, sheetData.Length);
    workbookData = combinedArray;
}
```
Nous créons un nouveau tableau suffisamment grand pour contenir à la fois les données existantes du classeur et les données de la nouvelle feuille de calcul. Nous copions ensuite les données existantes et nouvelles dans ce tableau combiné pour une utilisation ultérieure.
## Étape 8 : Enregistrer l'intégralité des données du classeur dans un fichier
 Enfin, avec toutes les données combinées dans notre`workbookData` tableau, nous pouvons enregistrer ce tableau dans un chemin de fichier spécifié.
```csharp
//Enregistrer l'intégralité des données du classeur dans un fichier
File.WriteAllBytes(dataDir + "out.txt", workbookData);
```
`WriteAllBytes` prend le tableau d'octets combiné et l'écrit dans un fichier texte nommé « out.txt » dans le répertoire spécifié.
## Conclusion
Et voilà ! Vous avez converti avec succès un classeur Excel au format CSV à l'aide d'Aspose.Cells pour .NET. Ce processus est non seulement efficace, mais il permet également de manipuler facilement les données Excel pour des analyses ou des rapports plus approfondis. Vous pouvez désormais automatiser vos tâches de traitement de données ou même intégrer cette fonctionnalité dans des applications plus volumineuses.
## FAQ
### Puis-je utiliser différents délimiteurs pour le fichier CSV ?
 Oui, vous pouvez modifier le`opts.Separator` à n'importe quel caractère de votre choix, comme des virgules ou des barres verticales.
### L'utilisation d'Aspose.Cells est-elle gratuite ?
 Aspose.Cells n'est pas gratuit, mais vous pouvez obtenir un essai gratuit[ici](https://releases.aspose.com/).
### Dans quels types de formats puis-je enregistrer en plus du CSV ?
Aspose.Cells permet d'enregistrer dans plusieurs formats, notamment XLSX, PDF, etc.
### Puis-je traiter des fichiers Excel volumineux à l’aide d’Aspose.Cells ?
Oui, Aspose.Cells est conçu pour gérer efficacement les fichiers volumineux, mais les performances peuvent dépendre des ressources système.
### Où puis-je trouver une documentation plus détaillée ?
Vous pouvez trouver une documentation complète et des exemples sur leur[site de référence](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
