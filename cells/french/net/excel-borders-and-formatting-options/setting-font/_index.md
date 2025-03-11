---
title: Définition de la police par programmation dans Excel
linktitle: Définition de la police par programmation dans Excel
second_title: API de traitement Excel Aspose.Cells .NET
description: Découvrez comment définir des polices par programmation dans Excel à l'aide d'Aspose.Cells pour .NET. Améliorez vos feuilles de calcul avec des polices élégantes.
weight: 11
url: /fr/net/excel-borders-and-formatting-options/setting-font/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Définition de la police par programmation dans Excel

## Introduction
Vous cherchez à manipuler des fichiers Excel avec finesse ? Vous êtes au bon endroit ! Aspose.Cells pour .NET est une bibliothèque exceptionnelle qui permet aux développeurs de travailler avec des feuilles de calcul Excel sans effort. Une tâche courante dans Excel consiste à ajuster les styles de police de certaines cellules, en particulier lorsque vous utilisez une mise en forme conditionnelle. Imaginez pouvoir mettre en évidence automatiquement des données importantes, rendant vos rapports non seulement fonctionnels mais également attrayants visuellement. Cela semble génial, n'est-ce pas ? Voyons comment vous pouvez définir des styles de police par programmation à l'aide d'Aspose.Cells pour .NET.
## Prérequis
Avant de nous lancer dans le codage, assurons-nous que tout est en place. Voici ce dont vous aurez besoin :
1. Visual Studio : assurez-vous d’avoir une version de Visual Studio installée (2017 ou une version ultérieure est recommandée).
2.  Aspose.Cells pour .NET : Si vous ne l'avez pas déjà fait, téléchargez la bibliothèque Aspose.Cells. Vous pouvez l'obtenir à partir du[Site Web d'Aspose](https://releases.aspose.com/cells/net/).
3. Connaissances de base de C# : une familiarité avec C# sera utile car nous écrirons du code dans ce langage.
4. .NET Framework : assurez-vous d’avoir installé une version compatible de .NET Framework.
Une fois ces prérequis réglés, vous êtes prêt à commencer à coder !
## Paquets d'importation
Pour commencer à utiliser Aspose.Cells, vous devez importer les packages nécessaires dans votre projet. Voici comment procéder :
1. Ouvrez votre projet Visual Studio.
2. Cliquez avec le bouton droit sur votre projet dans l’Explorateur de solutions et sélectionnez « Gérer les packages NuGet ».
3. Recherchez « Aspose.Cells » et installez-le. Cela ajoutera automatiquement les références nécessaires à votre projet.
Une fois le package installé, vous pouvez commencer à écrire du code pour manipuler des fichiers Excel !
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```
Maintenant, décomposons le processus de définition des styles de police dans une feuille Excel étape par étape.
## Étape 1 : Définir le répertoire des documents
Tout d'abord, vous devez définir le répertoire dans lequel vous souhaitez enregistrer votre fichier Excel. C'est là que tout votre travail acharné sera stocké, alors choisissez judicieusement ! Voici comment procéder :
```csharp
// Le chemin vers le répertoire des documents.
string dataDir = "Your Document Directory";
```
 Remplacer`"Your Document Directory"` avec le chemin d'accès réel sur votre système. Cela pourrait être quelque chose comme`@"C:\Documents\"` si vous travaillez sous Windows.
## Étape 2 : instancier un objet classeur
 Maintenant que le répertoire est configuré, il est temps de créer un nouveau classeur. Pensez à`Workbook` objet comme toile vierge sur laquelle vous peindrez vos données. Voici comment l'instancier :
```csharp
// Instanciation d'un objet Workbook
Workbook workbook = new Workbook();
```
## Étape 3 : Accéder à la première feuille de travail
 Ensuite, nous devons accéder à la feuille de calcul dans laquelle nous allons appliquer notre mise en forme. Dans un nouveau classeur, la première feuille de calcul se trouve généralement à l'index`0`Voici comment procéder :
```csharp
Worksheet sheet = workbook.Worksheets[0];
```
## Étape 4 : ajouter une mise en forme conditionnelle
Maintenant, pimentons un peu les choses en ajoutant une mise en forme conditionnelle. La mise en forme conditionnelle vous permet d'appliquer une mise en forme uniquement lorsque certaines conditions sont remplies. Voici comment l'ajouter :
```csharp
// Ajoute une mise en forme conditionnelle vide
int index = sheet.ConditionalFormattings.Add();
FormatConditionCollection fcs = sheet.ConditionalFormattings[index];
```
En ajoutant une mise en forme conditionnelle, nous nous préparons à appliquer des styles en fonction de critères spécifiques.
## Étape 5 : définir la plage de format conditionnel
Ensuite, nous allons définir la plage de cellules à laquelle nous souhaitons appliquer la mise en forme conditionnelle. C'est comme si vous disiez : « Hé, je veux appliquer mes règles à cette zone. » Voici comment vous pouvez spécifier la plage :
```csharp
// Définit la plage de format conditionnel.
CellArea ca = new CellArea();
ca.StartRow = 0;
ca.EndRow = 5;
ca.StartColumn = 0;
ca.EndColumn = 3;
fcs.AddArea(ca);
```
Dans cet exemple, nous formatons les cellules de A1 à D6 (indexées à 0). Ajustez ces valeurs selon vos besoins pour votre cas d'utilisation spécifique !
## Étape 6 : Ajouter une condition
Maintenant, spécifions la condition dans laquelle la mise en forme sera appliquée. Dans ce cas, nous souhaitons formater les cellules qui ont des valeurs comprises entre 50 et 100. Voici comment ajouter cette condition :
```csharp
// Ajoute une condition.
int conditionIndex = fcs.AddCondition(FormatConditionType.CellValue, OperatorType.Between, "50", "100");
```
Cette ligne indique essentiellement : « Si la valeur de la cellule est comprise entre 50 et 100, appliquez ma mise en forme. »
## Étape 7 : Définir les styles de police
Voici la partie intéressante ! Nous pouvons maintenant définir les styles de police que nous souhaitons appliquer à nos cellules. Nous allons mettre la police en italique, en gras, barrée, soulignée et changer sa couleur. Voici le code pour faire exactement cela :
```csharp
// Définit la couleur d'arrière-plan.
FormatCondition fc = fcs[conditionIndex];
// fc.Style.BackgroundColor = Color.Red; // Supprimez le commentaire pour définir la couleur d'arrière-plan
fc.Style.Font.IsItalic = true;
fc.Style.Font.IsBold = true;
fc.Style.Font.IsStrikeout = true;
fc.Style.Font.Underline = FontUnderlineType.Double;
fc.Style.Font.Color = Color.Black;
```
N'hésitez pas à jouer avec ces styles ! Vous souhaitez peut-être un fond clair ou des couleurs différentes ? Allez-y !
## Étape 8 : Enregistrer le classeur
Enfin, une fois que vous avez terminé tout ce travail difficile, n'oubliez pas de sauvegarder votre chef-d'œuvre ! Voici comment vous pouvez sauvegarder votre classeur :
```csharp
workbook.Save(dataDir + "output.xlsx");
```
 Cette ligne enregistre votre fichier Excel sous`output.xlsx` dans le répertoire spécifié. Assurez-vous que vous disposez des droits d'écriture à cet emplacement !
## Conclusion
Et voilà ! Vous venez d'apprendre à définir des styles de police par programmation dans Excel à l'aide d'Aspose.Cells pour .NET. De la définition de votre répertoire de documents à l'application de la mise en forme conditionnelle et enfin à l'enregistrement de votre travail, vous disposez désormais des outils nécessaires pour rendre vos fichiers Excel visuellement attrayants et fonctionnels.
Que vous génériez des rapports, automatisiez des tâches ou créiez des tableaux de bord, maîtriser l'art de la manipulation des polices peut élever vos feuilles de calcul du niveau de base au niveau de la beauté.
## FAQ
### Puis-je appliquer différents styles de police à différentes conditions ?  
Absolument ! Vous pouvez ajouter plusieurs conditions et spécifier des styles de police différents pour chacune d'elles.
### Quels types de conditions puis-je utiliser dans la mise en forme conditionnelle ?  
Vous pouvez utiliser différents types de conditions, notamment des valeurs de cellule, des formules, etc. Aspose.Cells fournit un riche ensemble d'options.
### L'utilisation d'Aspose.Cells est-elle gratuite ?  
 Aspose.Cells est un produit commercial, mais vous pouvez l'essayer gratuitement avec un essai limité disponible[ici](https://releases.aspose.com/).
### Puis-je formater une ligne entière en fonction de la valeur d’une cellule ?  
Oui ! Vous pouvez définir la mise en forme d'une ligne ou d'une colonne entière en fonction de la valeur d'une cellule spécifique à l'aide de la mise en forme conditionnelle.
### Où puis-je trouver plus d'informations sur Aspose.Cells ?  
 Vous trouverez une documentation et des ressources complètes sur le[Page de documentation d'Aspose.Cells](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
