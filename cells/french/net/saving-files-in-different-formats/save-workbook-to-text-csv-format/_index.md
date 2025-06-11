---
"description": "Apprenez à convertir sans effort des classeurs Excel au format CSV avec Aspose.Cells dans ce didacticiel complet, étape par étape, conçu pour les développeurs .NET."
"linktitle": "Enregistrer le classeur au format texte CSV"
"second_title": "API de traitement Excel Aspose.Cells .NET"
"title": "Enregistrer le classeur au format texte CSV"
"url": "/fr/net/saving-files-in-different-formats/save-workbook-to-text-csv-format/"
"weight": 17
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Enregistrer le classeur au format texte CSV

## Introduction
Lorsque vous manipulez des données, le format choisi détermine considérablement leur facilité d'utilisation. Parmi les formats les plus courants pour le traitement des données tabulaires figure le format CSV (valeurs séparées par des virgules). Si vous êtes développeur et travaillez avec des fichiers Excel et que vous devez convertir des classeurs au format CSV, Aspose.Cells pour .NET est une bibliothèque formidable qui simplifie cette tâche. Dans ce tutoriel, nous détaillerons les étapes pour convertir facilement un classeur Excel au format texte CSV.
## Prérequis
Avant de commencer, assurons-nous que vous avez tout en place pour commencer :
1. Connaissances de base de C# et .NET : Étant donné que nous allons écrire du code en C#, une familiarité avec le langage et le framework .NET est essentielle.
2. Bibliothèque Aspose.Cells : Assurez-vous que la bibliothèque Aspose.Cells pour .NET est installée dans votre environnement de développement. Vous pouvez la télécharger. [ici](https://releases.aspose.com/cells/net/).
3. Visual Studio ou tout autre IDE C# : vous aurez besoin d'un environnement de développement intégré (IDE) pour écrire et exécuter votre code. Visual Studio est un choix populaire.
4. Classeur Excel : préparez un exemple de classeur Excel (par exemple, « book1.xls ») contenant des données pour tester la conversion.
## Importer des packages
Maintenant que nous avons défini les prérequis, la première étape consiste à importer les packages nécessaires. Dans votre projet C#, vous devez inclure l'espace de noms suivant en haut de votre fichier de code :
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
Ces espaces de noms vous donneront accès aux classes et méthodes nécessaires pour travailler avec des fichiers Excel et gérer les flux de mémoire.
## Étape 1 : Définir le chemin d’accès au répertoire des documents
La première étape de notre processus consiste à définir l'emplacement de stockage de nos documents (classeurs Excel). Cette étape est essentielle car elle permet à notre programme de savoir où trouver les fichiers à traiter. 
```csharp
// Le chemin vers le répertoire des documents.
string dataDir = "Your Document Directory";
```
Assurez-vous de remplacer `"Your Document Directory"` avec le chemin d'accès réel de votre fichier « book1.xls ». Il peut s'agir d'un répertoire sur votre ordinateur ou d'un chemin vers un serveur.
## Étape 2 : Chargez votre classeur source
Ensuite, nous devons charger le classeur Excel qui sera converti au format CSV.
```csharp
// Chargez votre classeur source
Workbook workbook = new Workbook(dataDir + "book1.xls");
```
Le `Workbook` La classe de la bibliothèque Aspose.Cells permet de manipuler et d'accéder aux classeurs Excel. En transmettant le chemin d'accès au fichier, nous chargeons le classeur spécifié pour traitement.
## Étape 3 : Initialiser un tableau d'octets pour les données du classeur
Avant de commencer à convertir le classeur en CSV, nous devons initialiser un tableau d'octets vide qui contiendra éventuellement toutes les données de la feuille de calcul.
```csharp
// tableau de 0 octet
byte[] workbookData = new byte[0];
```
Ce tableau d'octets combinera les données de chaque feuille de calcul dans une structure unique que nous pourrons écrire dans un fichier ultérieurement.
## Étape 4 : Configurer les options d’enregistrement de texte
Maintenant, configurons les options d'enregistrement du format texte. Vous pouvez choisir des délimiteurs personnalisés ou utiliser des tabulations.
```csharp
// Options d'enregistrement du texte. Vous pouvez utiliser n'importe quel type de séparateur.
TxtSaveOptions opts = new TxtSaveOptions();
opts.Separator = '\t'; // Définir l'onglet comme séparateur
```
Dans cet exemple, nous utilisons une tabulation comme séparateur. Vous pouvez la remplacer. `'\t'` avec le caractère de votre choix, comme une virgule (`,`), selon la façon dont vous souhaitez formater votre fichier CSV.
## Étape 5 : Parcourez chaque feuille de calcul
Ensuite, nous allons parcourir toutes les feuilles de calcul du classeur, en enregistrant chacune d'elles dans notre `workbookData` tableau, mais vous devez d'abord sélectionner la feuille de calcul sur laquelle travailler.
```csharp
// Copiez chaque donnée de feuille de calcul au format texte dans le tableau de données du classeur
for (int idx = 0; idx < workbook.Worksheets.Count; idx++)
{
    // Enregistrer la feuille de calcul active au format texte
    MemoryStream ms = new MemoryStream();
    workbook.Worksheets.ActiveSheetIndex = idx;
    workbook.Save(ms, opts);
```
La boucle parcourt chaque feuille de calcul du classeur. `ActiveSheetIndex` est configuré de telle sorte qu'à chaque boucle, la feuille de calcul actuelle est enregistrée. Les résultats seront enregistrés en mémoire à l'aide d'un `MemoryStream`.
## Étape 6 : Récupérer les données de la feuille de calcul
Après avoir enregistré une feuille de calcul dans le flux de mémoire, l’étape suivante consiste à récupérer ces données et à les ajouter à notre `workbookData` tableau.
```csharp
    // Enregistrer les données de la feuille de calcul dans un tableau de données de feuille
    ms.Position = 0; // Réinitialiser la position du flux mémoire
    byte[] sheetData = ms.ToArray(); // Obtenir le tableau d'octets
```
`ms.Position = 0;` réinitialise la position de lecture après écriture. Ensuite, on utilise `ToArray()` pour convertir le flux de mémoire en un tableau d'octets contenant les données de la feuille de calcul.
## Étape 7 : Combiner les données de la feuille de calcul
Maintenant, nous allons combiner les données de chaque feuille de calcul dans une seule `workbookData` tableau initialisé plus tôt.
```csharp
    // Combinez les données de cette feuille de calcul dans un tableau de données de classeur
    byte[] combinedArray = new byte[workbookData.Length + sheetData.Length];
    Array.Copy(workbookData, 0, combinedArray, 0, workbookData.Length);
    Array.Copy(sheetData, 0, combinedArray, workbookData.Length, sheetData.Length);
    workbookData = combinedArray;
}
```
Nous créons un nouveau tableau suffisamment grand pour contenir les données du classeur existant et celles de la nouvelle feuille de calcul. Nous copions ensuite les données existantes et nouvelles dans ce tableau combiné pour une utilisation ultérieure.
## Étape 8 : Enregistrer l’intégralité des données du classeur dans un fichier
Enfin, avec toutes les données combinées dans notre `workbookData` tableau, nous pouvons enregistrer ce tableau dans un chemin de fichier spécifié.
```csharp
// Enregistrer l'intégralité des données du classeur dans un fichier
File.WriteAllBytes(dataDir + "out.txt", workbookData);
```
`WriteAllBytes` prend le tableau d'octets combiné et l'écrit dans un fichier texte nommé « out.txt » dans le répertoire spécifié.
## Conclusion
Et voilà ! Vous avez converti avec succès un classeur Excel au format CSV grâce à Aspose.Cells pour .NET. Ce processus est non seulement efficace, mais il facilite également la manipulation des données Excel pour des analyses ou des rapports plus approfondis. Vous pouvez désormais automatiser vos tâches de traitement de données ou même intégrer cette fonctionnalité à des applications plus volumineuses.
## FAQ
### Puis-je utiliser différents délimiteurs pour le fichier CSV ?
Oui, vous pouvez modifier le `opts.Separator` à n'importe quel caractère que vous voulez, comme des virgules ou des barres verticales.
### Aspose.Cells est-il gratuit à utiliser ?
Aspose.Cells n'est pas gratuit, mais vous pouvez obtenir un essai gratuit [ici](https://releases.aspose.com/).
### Dans quels types de formats puis-je enregistrer en plus du CSV ?
Aspose.Cells permet d'enregistrer dans plusieurs formats, notamment XLSX, PDF, etc.
### Puis-je traiter des fichiers Excel volumineux à l’aide d’Aspose.Cells ?
Oui, Aspose.Cells est conçu pour gérer efficacement les fichiers volumineux, mais les performances peuvent dépendre des ressources système.
### Où puis-je trouver une documentation plus détaillée ?
Vous pouvez trouver une documentation complète et des exemples sur leur [site de référence](https://reference.aspose.com/cells/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}