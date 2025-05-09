---
"description": "Apprenez à faire pivoter du texte avec des formes dans Excel grâce à Aspose.Cells pour .NET. Suivez ce guide étape par étape pour une présentation Excel parfaite."
"linktitle": "Faire pivoter le texte avec une forme dans Excel"
"second_title": "API de traitement Excel Aspose.Cells .NET"
"title": "Faire pivoter le texte avec une forme dans Excel"
"url": "/fr/net/excel-shape-text-modifications/rotate-text-shape-excel/"
"weight": 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Faire pivoter le texte avec une forme dans Excel

## Introduction
Dans l'univers Excel, la représentation visuelle est tout aussi importante que les données elles-mêmes. Que vous rédigiez un rapport ou conceviez un tableau de bord dynamique, la présentation des informations peut avoir un impact considérable sur leur lisibilité et leur apparence générale. Avez-vous déjà rêvé de faire pivoter du texte pour l'aligner avec élégance sur des formes ? C'est votre jour de chance ! Dans ce tutoriel, nous allons découvrir comment faire pivoter du texte avec des formes à l'aide d'Aspose.Cells pour .NET, pour que vos feuilles de calcul soient non seulement informatives, mais aussi impressionnantes.
## Prérequis
Avant de commencer, assurons-nous que vous avez tout ce dont vous avez besoin :
1. Visual Studio : assurez-vous que Visual Studio est installé sur votre machine, car c'est là que nous écrirons notre code.
2. Aspose.Cells pour .NET : vous aurez besoin de la bibliothèque Aspose.Cells. Vous pouvez [téléchargez la dernière version ici](https://releases.aspose.com/cells/net/) ou essayez-le gratuitement avec un [essai gratuit](https://releases.aspose.com/).
3. Connaissances de base de C# : une familiarité avec C# et l'environnement .NET sera utile, même si nous vous guiderons à chaque étape du processus.
4. Fichier Excel : un exemple de fichier Excel, appelons-le `sampleRotateTextWithShapeInsideWorksheet.xlsx`, est nécessaire pour tester notre code. Vous devez placer ce fichier dans un répertoire facilement accessible.
Tout est prêt ? Fantastique ! Passons à la partie amusante.
## Importer des packages
Pour démarrer, nous devons importer les packages nécessaires dans notre projet. Voici comment procéder :
### Créer un nouveau projet
1. Ouvrez Visual Studio.
2. Sélectionnez « Créer un nouveau projet ».
3. Choisissez « Application console » et sélectionnez C# comme langage de programmation préféré.
### Installer Aspose.Cells
Ajoutons maintenant Aspose.Cells à votre projet. Pour ce faire, utilisez le gestionnaire de packages NuGet :
1. Ouvrez « Outils » dans le menu supérieur.
2. Sélectionnez « Gestionnaire de packages NuGet », puis « Gérer les packages NuGet pour la solution ».
3. Recherchez « Aspose.Cells ».
4. Cliquez sur « Installer » pour l’ajouter à votre projet.
### Ajouter une directive à l'aide de
En haut de votre fichier C# principal, vous devez ajouter la directive suivante :
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Drawing;
```
Nous sommes maintenant tous prêts à commencer à coder !
Décomposons le processus en étapes faciles à comprendre. Voici comment faire pivoter du texte avec des formes dans un fichier Excel :
## Étape 1 : Configurez vos chemins de répertoire
Tout d'abord, vous devez configurer les répertoires source et de sortie où seront stockés vos fichiers Excel. Voici comment :
```csharp
//Répertoire source
string sourceDir = "Your Document Directory"; // Définissez votre répertoire de documents
//Répertoire de sortie
string outputDir = "Your Document Directory"; // Définissez votre répertoire de sortie
```
Remplacer `"Your Document Directory"` avec le chemin réel où votre `sampleRotateTextWithShapeInsideWorksheet.xlsx` le fichier est localisé.
## Étape 2 : Charger l’exemple de fichier Excel
Chargeons maintenant le fichier Excel d'exemple. Cette étape est cruciale, car nous souhaitons manipuler les données existantes.
```csharp
//Charger un exemple de fichier Excel.
Workbook wb = new Workbook(sourceDir + "sampleRotateTextWithShapeInsideWorksheet.xlsx");
```
## Étape 3 : Accéder à la feuille de travail
Une fois le fichier chargé, nous devons accéder à la feuille de calcul que nous souhaitons modifier. Dans notre cas, il s'agit de la première feuille de calcul.
```csharp
//Accéder à la première feuille de travail.
Worksheet ws = wb.Worksheets[0];
```
## Étape 4 : Modifier une cellule
Nous allons ensuite modifier une cellule spécifique pour afficher un message. Dans notre exemple, nous utiliserons la cellule B4.
```csharp
//Accédez à la cellule B4 et ajoutez un message à l'intérieur.
Cell b4 = ws.Cells["B4"];
b4.PutValue("Text is not rotating with shape because RotateTextWithShape is false.");
```
Cette étape est entièrement consacrée à la communication : garantir que quiconque ouvre cette feuille comprenne ce que nous modifions.
## Étape 5 : Accéder à la première forme
Pour faire pivoter du texte, nous avons besoin d'une forme. Nous allons accéder ici à la première forme de la feuille de calcul.
```csharp
//Accéder à la première forme.
Shape sh = ws.Shapes[0];
```
## Étape 6 : Ajuster l'alignement du texte de la forme
C'est ici que la magie opère : nous allons ajuster les propriétés d'alignement du texte de la forme.
```csharp
//Accéder à l'alignement du texte de forme.
Aspose.Cells.Drawing.Texts.ShapeTextAlignment shapeTextAlignment = sh.TextBody.TextAlignment;
//Ne faites pas pivoter le texte avec la forme en définissant RotateTextWithShape sur false.
shapeTextAlignment.RotateTextWithShape = false;
```
En définissant `RotateTextWithShape` pour faux, nous veillons à ce que le texte reste droit et ne tourne pas avec la forme, gardant ainsi tout propre et organisé.
## Étape 7 : Enregistrer le fichier Excel de sortie
Enfin, enregistrons nos modifications dans un nouveau fichier Excel. Cela nous permettra de conserver nos modifications et d'obtenir un résultat net.
```csharp
//Enregistrez le fichier Excel de sortie.
wb.Save(outputDir + "outputRotateTextWithShapeInsideWorksheet.xlsx");
```
Et voilà ! Votre fichier de sortie est maintenant enregistré, y compris le texte de la cellule B4 et les ajustements apportés à la forme.
## Étape 8 : Exécuter le code
Dans votre `Main` Méthode, encapsulez tous les extraits de code ci-dessus et exécutez votre projet. Observez les modifications dans votre fichier de sortie !
```csharp
Console.WriteLine("RotateTextWithShapeInsideWorksheet executed successfully.");
```
## Conclusion
Faire pivoter du texte avec des formes dans Excel avec Aspose.Cells pour .NET peut sembler complexe au premier abord, mais c'est assez simple une fois maîtrisé. En suivant ces étapes simples, vous pouvez personnaliser vos feuilles de calcul pour un rendu plus professionnel et plus attrayant. Que ce soit pour un client ou pour vos projets personnels, la qualité de votre travail sera saluée par tous !
## FAQ
### Puis-je utiliser Aspose.Cells gratuitement ?
Oui ! Vous pouvez utiliser le [essai gratuit](https://releases.aspose.com/) pour essayer la bibliothèque.
### Quelles versions d'Excel Aspose.Cells prend-il en charge ?
Aspose.Cells prend en charge une variété de formats Excel, notamment XLS, XLSX, CSV, etc.
### Est-il possible de faire pivoter du texte avec des formes dans les anciennes versions d'Excel ?
Oui, la fonctionnalité peut être appliquée aux anciens formats pris en charge par Aspose.Cells.
### Où puis-je trouver plus de documentation sur Aspose.Cells ?
Vous pouvez explorer le programme complet [documentation](https://reference.aspose.com/cells/net/) pour plus d'informations.
### Comment obtenir de l'aide pour Aspose.Cells ?
Vous pouvez demander de l'aide en visitant le [Forum Aspose](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}