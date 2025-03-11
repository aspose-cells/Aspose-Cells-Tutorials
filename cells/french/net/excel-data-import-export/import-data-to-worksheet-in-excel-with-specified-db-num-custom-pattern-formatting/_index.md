---
title: Importer des données vers Excel avec un formatage de modèle numérique de base de données personnalisé
linktitle: Importer des données vers Excel avec un formatage de modèle numérique de base de données personnalisé
second_title: API de traitement Excel Aspose.Cells .NET
description: Découvrez comment importer des données dans Excel avec un formatage DB Num personnalisé à l'aide d'Aspose.Cells pour .NET dans ce didacticiel facile à suivre.
weight: 10
url: /fr/net/excel-data-import-export/import-data-to-worksheet-in-excel-with-specified-db-num-custom-pattern-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Importer des données vers Excel avec un formatage de modèle numérique de base de données personnalisé

## Introduction

En matière de manipulation de feuilles de calcul, l'importation de données dans Excel et leur formatage correct peuvent sembler une tâche écrasante, en particulier lorsque vous souhaitez utiliser des formats spécifiques basés sur la culture tels que les modèles DB Num. Si vous vous êtes déjà senti embourbé dans les détails techniques du formatage Excel, vous êtes au bon endroit ! Dans ce guide, nous allons décomposer les choses en étapes simples à l'aide d'Aspose.Cells pour .NET, ce qui rend vos importations de données non seulement simples mais aussi esthétiques. Alors, accrochez-vous bien, car nous plongeons directement dans le monde de la programmation .NET, du formatage et de l'exportation de fichiers Excel en toute simplicité !

## Prérequis

Avant de passer aux choses sérieuses, assurons-nous que vous disposez de tout ce dont vous avez besoin. Voici une liste rapide des prérequis pour vous préparer au succès :

1. .NET Framework : assurez-vous que .NET Framework est installé sur votre ordinateur. Aspose.Cells fonctionne parfaitement avec différentes versions de .NET.
2.  Aspose.Cells pour .NET : vous devez télécharger et installer la bibliothèque Aspose.Cells. Vous pouvez la récupérer à partir du[lien de téléchargement](https://releases.aspose.com/cells/net/).
3. Environnement de développement intégré (IDE) : utilisez un IDE comme Visual Studio dans lequel vous pouvez écrire et exécuter votre code C#.
4. Connaissances de base de C# : avoir une compréhension fondamentale de C# vous aidera à suivre les pratiques de codage que nous utiliserons dans ce guide.

Vous avez tout reçu ? Super ! Passons à l'importation des paquets nécessaires.

## Paquets d'importation

Pour travailler efficacement avec Aspose.Cells, vous devez importer les espaces de noms requis au début de votre fichier C#. Décomposons-le étape par étape.

### Créez votre fichier C#

 Ouvrez votre IDE (Visual Studio est recommandé) et créez un nouveau projet C#. Nommez-le de manière pertinente, par exemple`ExcelDataImport`.

### Référence Aspose.Cells

Vous devez inclure la bibliothèque Aspose.Cells dans votre projet. Cliquez avec le bouton droit de la souris sur votre projet dans l'Explorateur de solutions et sélectionnez « Ajouter une référence ». Accédez à l'emplacement où vous avez installé Aspose.Cells et sélectionnez-le.

### Importer les espaces de noms nécessaires

En haut de votre fichier C#, importez les espaces de noms suivants :

```csharp
using System;
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

Cette simple ligne est votre passerelle vers toutes les fonctionnalités qu'Aspose.Cells a à offrir. 

Maintenant que nous avons couvert tous les prérequis et importé les packages nécessaires, plongeons dans le processus étape par étape d'importation de données vers Excel et d'application d'un formatage de modèle DB Num personnalisé. Nous allons procéder méthodiquement pour garantir la clarté et la compréhension.

## Étape 1 : définir le répertoire de données

Tout d'abord, vous devez spécifier le chemin d'accès au répertoire de vos documents où la sortie sera enregistrée. Ajustez-le en fonction de la structure de votre fichier.

```csharp
string dataDir = "Your Document Directory";
```

 Dans cet exemple, remplacez`Your Document Directory` avec ton chemin actuel, comme`C:\\Users\\YourName\\Documents\\`.

## Étape 2 : Créer un classeur

Ensuite, vous allez créer un nouveau classeur, qui est essentiellement votre fichier Excel.

```csharp
Workbook wb = new Workbook();
```

 Ici, nous instancions un nouveau`Workbook` objet. Ceci est votre toile vierge !

## Étape 3 : Accéder à la première feuille de travail

Chaque classeur contient plusieurs feuilles de calcul. Vous devez accéder à la première feuille de calcul pour commencer à saisir des données.

```csharp
Worksheet ws = wb.Worksheets[0];
```

Tout comme lorsque vous ouvrez un livre à la première page, vous accédez à la première feuille de calcul pour ajouter vos données.

## Étape 4 : Entrer les données dans une cellule

 Maintenant, remplissons une cellule avec des données. Pour cet exemple, nous allons saisir la valeur`123` dans la cellule A1.

```csharp
Cell cell = ws.Cells["A1"];
cell.PutValue(123);
```

Vous parlez ici directement à Excel : vous placez les données directement dans la cellule A1 ! 

## Étape 5 : Accéder au style de cellule

Chaque cellule possède un style et vous pouvez personnaliser son apparence. Pour appliquer un format personnalisé, vous devez d'abord accéder au style de la cellule.

```csharp
Style st = cell.GetStyle();
```

En vous emparant du style de la cellule, vous vous préparez à ajouter votre touche unique !

## Étape 6 : Spécifier le formatage du modèle personnalisé DBNum

C'est ici que la magie opère. Vous pouvez spécifier un modèle de format personnalisé à l'aide du style de formatage DBNum.

```csharp
st.Custom = "[DBNum2][$-804]General";
```

 Cette ligne indique à Excel de formater le nombre`123`selon le modèle DBNum correspondant à la langue chinoise. Plutôt sympa, non ?

## Étape 7 : définir le style de cellule mis à jour

Maintenant que vous avez défini votre style personnalisé, il est temps de l'appliquer à la cellule.

```csharp
cell.SetStyle(st);
```

C'est comme habiller votre téléphone portable avec une nouvelle tenue élégante !

## Étape 8 : Ajuster la largeur de la colonne

Assurons-nous que tout est bien net et bien organisé. Vous pouvez ajuster la largeur de la première colonne pour mieux l'adapter à vos données.

```csharp
ws.Cells.SetColumnWidth(0, 30);
```

Ici, nous élargissons la largeur des colonnes, afin que vos données ne soient pas à l'étroit. Considérez cela comme si vous donniez à vos données un espace pour respirer !

## Étape 9 : Enregistrer le classeur

Enfin, sauvegardons ce chef-d'œuvre au format PDF. C'est la grande finale !

```csharp
wb.Save(dataDir + "outputDBNumCustomFormatting.pdf", SaveFormat.Pdf);
```

Félicitations ! Vous venez de créer un fichier PDF présentant votre numéro formaté avec les styles DB Num.

## Conclusion

Et voilà ! Vous avez réussi à importer des données dans Excel, à appliquer un formatage DB Num personnalisé et à les enregistrer au format PDF. Avec Aspose.Cells pour .NET, ce processus devient non seulement plus simple, mais aussi beaucoup plus flexible et puissant. Ne vous débattez plus avec les options de formatage intégrées d'Excel : vous disposez désormais d'une ligne de contrôle directe via le code !

Que vous prépariez des rapports de données ou créiez des états financiers, exploiter la puissance d'Aspose.Cells élèvera votre jeu de feuille de calcul à un tout autre niveau. Alors, qu'attendez-vous ? Plongez dans vos projets en toute confiance et laissez vos données briller !

## FAQ

### Qu'est-ce qu'Aspose.Cells ?  
Aspose.Cells est une bibliothèque puissante pour .NET qui permet aux développeurs de créer, manipuler et convertir des fichiers Excel par programmation.

### Puis-je formater d’autres types de cellules ?  
Oui ! Vous pouvez appliquer différents styles, formats et même formules à n’importe quelle cellule de vos feuilles de calcul.

### Existe-t-il un essai gratuit disponible ?  
 Absolument ! Vous pouvez essayer une version d'essai gratuite[ici](https://releases.aspose.com/).

### Dans quels formats puis-je enregistrer les fichiers Excel ?  
Aspose.Cells prend en charge une variété de formats, notamment XLSX, XLS, CSV, PDF et bien d'autres.

### Où puis-je trouver plus d’aide ?  
 Si vous avez besoin d'aide, visitez leur[Forum de soutien](https://forum.aspose.com/c/cells/9) pour l'aide de la communauté et des experts.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
