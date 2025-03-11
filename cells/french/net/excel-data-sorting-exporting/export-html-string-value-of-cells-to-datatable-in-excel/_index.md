---
title: Exporter la valeur de la chaîne HTML des cellules vers DataTable dans Excel
linktitle: Exporter la valeur de la chaîne HTML des cellules vers DataTable dans Excel
second_title: API de traitement Excel Aspose.Cells .NET
description: Découvrez comment exporter des valeurs de chaîne HTML à partir de cellules Excel vers un DataTable à l'aide d'Aspose.Cells pour .NET dans un didacticiel simple étape par étape.
weight: 11
url: /fr/net/excel-data-sorting-exporting/export-html-string-value-of-cells-to-datatable-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exporter la valeur de la chaîne HTML des cellules vers DataTable dans Excel

## Introduction

Lorsque vous travaillez avec des fichiers Excel dans un environnement .NET, vous pouvez avoir besoin d'extraire des informations des cellules, non seulement sous forme de texte brut, mais plutôt sous forme de chaînes HTML. Cela peut s'avérer très pratique lorsque vous traitez des données de texte enrichi ou lorsque vous souhaitez conserver la mise en forme. Dans ce guide, je vous expliquerai comment exporter la valeur de chaîne HTML des cellules vers un DataTable à l'aide d'Aspose.Cells pour .NET. 

## Prérequis

Avant de plonger dans le code, assurons-nous que vous disposez de tout ce dont vous avez besoin. Voici une liste de contrôle rapide :

1. Connaissances de base de C# et .NET : avant de vous lancer dans le codage, assurez-vous de bien connaître la programmation C# et les bases du framework .NET.
2.  Aspose.Cells pour .NET : si vous ne l'avez pas déjà fait, vous devez installer Aspose.Cells pour .NET. Vous pouvez télécharger une version d'essai gratuite à partir de[ici](https://releases.aspose.com/).
3. Visual Studio ou IDE de votre choix : configurez votre environnement pour écrire du code C#. Visual Studio est recommandé pour sa large gamme de fonctionnalités et sa simplicité d'utilisation.
4. Exemple de fichier Excel : vous aurez besoin d’un exemple de fichier Excel (`sampleExportTableAsHtmlString.xlsx`) pour travailler avec. Assurez-vous qu'il se trouve dans un répertoire accessible.
5. Gestionnaire de packages NuGet : assurez-vous d’avoir accès au Gestionnaire de packages NuGet dans votre projet pour ajouter facilement la bibliothèque Aspose.Cells.

Ces prérequis étant vérifiés, mettons-nous à la tâche avec un peu de codage !

## Paquets d'importation

Avant de pouvoir commencer à travailler avec Aspose.Cells, nous devons importer les packages nécessaires. Cela implique généralement d'ajouter le package NuGet Aspose.Cells à votre projet. Voici comment procéder :

### Ouvrir le gestionnaire de packages NuGet

Dans Visual Studio, cliquez avec le bouton droit sur votre projet dans l’Explorateur de solutions et sélectionnez Gérer les packages NuGet.

### Rechercher Aspose.Cells

 Dans le gestionnaire de packages NuGet, saisissez`Aspose.Cells` dans la barre de recherche.

### Installer le paquet

Une fois que vous avez trouvé Aspose.Cells, cliquez sur le bouton Installer. Cela ajoutera la bibliothèque à votre projet et vous permettra de l'importer dans votre code.

### Importer l'espace de noms

Ajoutez la directive using suivante en haut de votre fichier de code :

```csharp
using System;
using System.IO;
using Aspose.Cells;
using System.Data;
```

Maintenant que nous avons tout configuré, plongeons dans le processus étape par étape d'exportation des valeurs de chaîne HTML d'un fichier Excel vers un DataTable. 

## Étape 1 : Définir le répertoire source

Vous commencerez par définir le répertoire dans lequel votre fichier Excel d'exemple est stocké. Ceci est crucial car cela indique à votre application où trouver le fichier. Voici le code pour cela :

```csharp
string sourceDir = "Your Document Directory";
```

 Assurez-vous de remplacer`"Your Document Directory"` avec le chemin réel vers votre fichier Excel.

## Étape 2 : charger l’exemple de fichier Excel

 L'étape suivante consiste à charger le classeur Excel. Vous utiliserez le`Workbook` classe de Aspose.Cells pour faire cela. Voici comment vous pouvez charger le fichier :

```csharp
Workbook wb = new Workbook(sourceDir + "sampleExportTableAsHtmlString.xlsx");
```

Cette simple ligne de code initialise le classeur et charge le fichier Excel spécifié.

## Étape 3 : Accéder à la première feuille de travail

Une fois le classeur chargé, vous souhaiterez accéder à la feuille de calcul spécifique qui contient les données qui vous intéressent. En général, vous commencerez par la première feuille de calcul :

```csharp
Worksheet ws = wb.Worksheets[0];
```

Ici, nous travaillons avec la première feuille de calcul (index 0). Assurez-vous que vos données se trouvent sur la bonne feuille.

## Étape 4 : Spécifier les options du tableau d’exportation

Pour contrôler la manière dont les données sont exportées, vous devez configurer`ExportTableOptions`. Dans ce cas, vous souhaitez vous assurer que les noms de colonnes ne sont pas exportés et que les données de cellule sont exportées sous forme de chaînes HTML :

```csharp
ExportTableOptions opts = new ExportTableOptions();
opts.ExportColumnName = false;
opts.ExportAsHtmlString = true;
```

Cette configuration vous permet de conserver la mise en forme riche de vos données cellulaires lors de l'exportation.

## Étape 5 : Exporter les cellules vers DataTable

 Vient maintenant la partie cruciale où vous exportez réellement les données. À l'aide de`ExportDataTable` méthode, vous pouvez extraire les données de la feuille de calcul dans un`DataTable`Voici comment procéder :

```csharp
DataTable dt = ws.Cells.ExportDataTable(0, 0, 3, 3, opts);
```

Ce code exporte une plage de cellules spécifiée (de la ligne 0, colonne 0 à la ligne 3, colonne 3) dans un DataTable en utilisant les options spécifiées précédemment.

## Étape 6 : imprimer la valeur de la chaîne HTML

Enfin, imprimons la valeur de la chaîne HTML d'une cellule spécifique du DataTable pour voir ce que nous avons réussi à exporter. Par exemple, si vous souhaitez imprimer la valeur de la troisième ligne et de la deuxième colonne, procédez comme suit :

```csharp
Console.WriteLine(dt.Rows[2][1].ToString());
```

Cette ligne imprime la chaîne HTML souhaitée du DataTable dans la console. 

## Conclusion 

Et voilà ! Vous avez exporté avec succès des valeurs de chaîne HTML à partir de cellules d'un fichier Excel vers un DataTable à l'aide d'Aspose.Cells pour .NET. Cette fonctionnalité enrichit non seulement vos compétences en matière de manipulation de données, mais élargit également vos options lorsque vous traitez du contenu formaté directement à partir de fichiers Excel. 

## FAQ

### Puis-je utiliser Aspose.Cells pour d’autres formats de fichiers en plus d’Excel ?  
Oui, Aspose.Cells est principalement destiné à Excel, mais Aspose propose d'autres bibliothèques pour différents formats.

### Ai-je besoin d'une licence pour Aspose.Cells ?  
 Oui, une licence valide est requise pour une utilisation en production. Vous pouvez obtenir une licence temporaire[ici](https://purchase.aspose.com/temporary-license/).

### Que se passe-t-il si mon fichier Excel contient des formules ? Sont-elles exportées correctement ?  
Oui, Aspose.Cells peut gérer les formules et, lors de l'exportation, elles seront évaluées en fonction de leurs valeurs résultantes.

### Est-il possible de modifier les options d'exportation ?  
 Absolument ! Vous pouvez personnaliser`ExportTableOptions` pour répondre à vos besoins spécifiques.

### Où puis-je trouver une documentation plus détaillée sur Aspose.Cells ?  
 Vous trouverez une documentation complète[ici](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
