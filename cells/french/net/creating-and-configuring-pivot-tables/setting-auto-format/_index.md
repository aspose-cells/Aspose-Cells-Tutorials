---
title: Définition du formatage automatique du tableau croisé dynamique par programmation dans .NET
linktitle: Définition du formatage automatique du tableau croisé dynamique par programmation dans .NET
second_title: API de traitement Excel Aspose.Cells .NET
description: Découvrez comment définir la mise en forme automatique des tableaux croisés dynamiques Excel par programmation à l'aide d'Aspose.Cells pour .NET dans ce didacticiel détaillé étape par étape.
weight: 18
url: /fr/net/creating-and-configuring-pivot-tables/setting-auto-format/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Définition du formatage automatique du tableau croisé dynamique par programmation dans .NET

## Introduction
En matière d'analyse de données, les tableaux croisés dynamiques dans Excel peuvent changer la donne. Ils vous permettent de résumer et d'analyser les données de manière dynamique, vous aidant ainsi à obtenir des informations qu'il serait presque impossible d'extraire manuellement. Mais que faire si vous souhaitez automatiser le processus de mise en forme de vos tableaux croisés dynamiques dans .NET ? Ici, je vais vous montrer comment définir par programmation le formatage automatique d'un tableau croisé dynamique à l'aide de la puissante bibliothèque Aspose.Cells pour .NET.
Dans ce guide, nous allons explorer les éléments essentiels, parcourir les prérequis, importer les packages nécessaires, puis plonger dans un didacticiel étape par étape pour vous permettre de formater des tableaux croisés dynamiques comme un pro. Cela vous convient ? Allons-y !
## Prérequis
Avant de commencer, assurons-nous que vous disposez de tout ce dont vous avez besoin pour commencer :
1. Un environnement de développement .NET : assurez-vous de disposer d’une instance fonctionnelle de Visual Studio (ou de tout IDE prenant en charge .NET).
2.  Bibliothèque Aspose.Cells : pour travailler avec des fichiers Excel sans problème, vous devez avoir installé la bibliothèque Aspose.Cells. Si vous ne l'avez pas encore fait, vous pouvez la récupérer à partir du[page de téléchargement](https://releases.aspose.com/cells/net/).
3. Connaissances de base de C# : la familiarité avec la programmation C# vous aidera à mieux comprendre les étapes.
4.  Fichier Excel (modèle) : vous aurez besoin d'un fichier modèle Excel pour commencer, qui sera traité dans notre exemple. Pour plus de simplicité, vous pouvez créer un fichier exemple nommé`Book1.xls`.
## Paquets d'importation
Pour démarrer avec Aspose.Cells dans votre projet, vous devez importer les packages nécessaires. Voici comment vous pouvez configurer cela dans votre projet .NET :
### Créer un nouveau projet
Commencez par créer un nouveau projet .NET dans votre IDE préféré. 
### Ajouter des références
Assurez-vous d'ajouter une référence à la bibliothèque Aspose.Cells. Si vous avez téléchargé la bibliothèque, ajoutez les DLL issues de l'extraction. Si vous utilisez NuGet, vous pouvez simplement exécuter :
```bash
Install-Package Aspose.Cells
```
### Importer des espaces de noms
Maintenant, dans votre fichier de code, vous devez importer l'espace de noms Aspose.Cells. Vous pouvez le faire en ajoutant la ligne suivante en haut de votre fichier C# :
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
using Aspose.Cells.Pivot;
```
Une fois ces étapes terminées, vous êtes prêt à écrire du code !
Maintenant, décomposons le code que vous avez fourni en étapes détaillées avec des explications sur ce que fait chaque partie. 
## Étape 1 : Définissez votre répertoire de documents
Pour commencer, vous devez définir le chemin d'accès à votre répertoire de documents où se trouvent vos fichiers Excel. Dans notre exemple, nous le définirons ainsi :
```csharp
string dataDir = "Your Document Directory";  // Modifier selon les besoins
```
 Cette ligne crée une variable de chaîne`dataDir`qui contient le chemin d'accès au fichier de vos documents. Assurez-vous de remplacer`"Your Document Directory"` avec le chemin réel sur votre système.
## Étape 2 : charger le fichier modèle
Ensuite, vous souhaiterez charger un classeur existant contenant votre tableau croisé dynamique :
```csharp
Workbook workbook = new Workbook(dataDir + "Book1.xls");
```
 Cette ligne initialise une nouvelle`Workbook` objet en chargeant le fichier Excel spécifié. Le fichier doit contenir au moins un tableau croisé dynamique pour que les étapes suivantes soient efficaces.
## Étape 3 : Accéder à la feuille de travail souhaitée
Identifiez la feuille de calcul sur laquelle vous devez travailler pour accéder au tableau croisé dynamique. Dans ce cas, nous obtiendrons simplement la première :
```csharp
int pivotIndex = 0;  // Index du tableau croisé dynamique
Worksheet worksheet = workbook.Worksheets[0];
```
 Ici,`worksheet` récupère la première feuille de calcul du classeur. L'index du tableau croisé dynamique est défini sur`0`, ce qui signifie que nous accédons au premier tableau croisé dynamique de cette feuille de calcul.
## Étape 4 : Localisez le tableau croisé dynamique
Une fois la feuille de calcul prête, il est temps d'accéder à votre tableau croisé dynamique :
```csharp
PivotTable pivotTable = worksheet.PivotTables[pivotIndex];
```
 Ceci initialise un nouveau`PivotTable` objet en obtenant le tableau croisé dynamique à l'index spécifié à partir de la feuille de calcul.
## Étape 5 : définir la propriété de formatage automatique
Passons maintenant à la partie intéressante : définir les options de formatage automatique pour votre tableau croisé dynamique.
```csharp
pivotTable.IsAutoFormat = true; // Activer le formatage automatique
```
 Cette ligne active la fonction de formatage automatique pour le tableau croisé dynamique. Lorsqu'elle est définie sur`true`, le tableau croisé dynamique se formatera automatiquement en fonction de styles prédéfinis.
## Étape 6 : Choisissez un type de format automatique spécifique
Nous voudrons également spécifier quel style de format automatique le tableau croisé dynamique doit adopter. Aspose.Cells propose différents formats parmi lesquels nous pouvons choisir. Voici comment le définir :
```csharp
pivotTable.AutoFormatType = Aspose.Cells.Pivot.PivotTableAutoFormatType.Report5;
```
 Avec cette ligne, nous attribuons un type de format automatique spécifique au tableau croisé dynamique.`Report5` ce n'est qu'un exemple d'un style ; vous pouvez choisir parmi une variété d'options en fonction de vos besoins. 
## Étape 7 : Enregistrer le classeur
Enfin, n'oubliez pas de sauvegarder votre classeur après avoir effectué toutes les modifications :
```csharp
workbook.Save(dataDir + "output.xls");
```
 Cette ligne de code enregistre le classeur modifié dans un nouveau fichier appelé`output.xls` dans le répertoire spécifié. Assurez-vous de vérifier ce fichier pour voir votre tableau croisé dynamique magnifiquement formaté !
## Conclusion
Félicitations ! Vous venez de programmer un tableau croisé dynamique Excel pour le formater automatiquement à l'aide d'Aspose.Cells dans .NET. Ce processus vous permet non seulement de gagner du temps lors de la préparation des rapports, mais garantit également la cohérence de l'apparence de vos données à chaque exécution. Avec seulement quelques lignes de code, vous pouvez améliorer considérablement vos fichiers Excel, comme un magicien numérique.
## FAQ
### Qu'est-ce qu'Aspose.Cells ?
Aspose.Cells est une puissante bibliothèque .NET permettant de gérer des fichiers Excel sans nécessiter l'installation de Microsoft Excel.
### Puis-je formater plusieurs tableaux croisés dynamiques dans un classeur ?
Oui, vous pouvez parcourir plusieurs objets de tableau croisé dynamique dans votre classeur pour les formater un par un.
### Existe-t-il un essai gratuit disponible pour Aspose.Cells ?
 Absolument ! Vous pouvez commencer avec une version d'essai gratuite disponible[ici](https://releases.aspose.com/).
### Que faire si mon tableau croisé dynamique n’est pas formaté correctement ?
Assurez-vous que le tableau croisé dynamique est correctement référencé et que le type de formatage automatique existe, sinon il risque de revenir aux paramètres par défaut.
### Puis-je automatiser ce processus avec des tâches planifiées ?
Oui ! En incorporant ce code dans une tâche planifiée, vous pouvez automatiser la génération et la mise en forme régulière des rapports.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
