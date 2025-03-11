---
title: Décaler la première ligne vers le bas lors de l'insertion de lignes de tableau de données dans Excel
linktitle: Décaler la première ligne vers le bas lors de l'insertion de lignes de tableau de données dans Excel
second_title: API de traitement Excel Aspose.Cells .NET
description: Apprenez à insérer des lignes DataTable dans Excel sans décaler la première ligne vers le bas à l'aide d'Aspose.Cells pour .NET. Guide étape par étape pour une automatisation sans effort.
weight: 11
url: /fr/net/excel-data-import-export/shift-first-row-down-when-inserting-cells-datatable-rows-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Décaler la première ligne vers le bas lors de l'insertion de lignes de tableau de données dans Excel

## Introduction

Vous en avez assez de déplacer manuellement les lignes lorsque vous insérez de nouvelles données dans vos feuilles de calcul Excel ? Eh bien, vous avez de la chance ! Dans cet article, nous allons découvrir comment automatiser ce processus à l'aide d'Aspose.Cells pour .NET. À la fin de ce didacticiel, vous apprendrez non seulement à travailler avec des tableaux de données dans Excel, mais également à personnaliser les options d'importation pour mieux répondre à vos besoins. Croyez-moi, cela peut vous faire gagner beaucoup de temps et vous éviter bien des tracas ! Alors, prenez une tasse de café et commençons !

## Prérequis

Avant de passer au codage, assurons-nous que tout est configuré :

1. Visual Studio : assurez-vous d’avoir installé Visual Studio (2017 ou une version ultérieure devrait fonctionner correctement).
2.  Aspose.Cells pour .NET : vous devez disposer de la bibliothèque Aspose.Cells. Si vous ne l'avez pas encore fait, vous pouvez la télécharger[ici](https://releases.aspose.com/cells/net/).
3. Compréhension de base de C# et d'Excel : une compréhension de base de la programmation C# et du fonctionnement d'Excel vous aidera certainement à suivre plus efficacement.

 Vous aurez également besoin d'un exemple de fichier Excel à portée de main. Dans ce guide, nous utiliserons un exemple appelé`sampleImportTableOptionsShiftFirstRowDown.xlsx`. Vous pouvez créer ce fichier ou trouver un modèle adapté à vos besoins.

## Paquets d'importation

Avant de nous lancer dans le codage, nous devons nous assurer d'importer les packages nécessaires. Dans votre projet C#, incluez les espaces de noms suivants :

```csharp
using System;
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

Ces packages sont essentiels pour travailler avec le classeur, la feuille de calcul et les tableaux.

## Étape 1 : Configurez votre projet

### Créer un nouveau projet C#

Commencez par créer une nouvelle application console C# dans Visual Studio. Donnez à votre projet un nom approprié, comme « ExcelDataImport ».

### Ajouter le package NuGet Aspose.Cells

Pour ajouter le package Aspose.Cells, faites un clic droit sur votre projet dans l'Explorateur de solutions, sélectionnez Gérer les packages NuGet et recherchez « Aspose.Cells ». Installez le package pour vous assurer de pouvoir accéder à toutes les fonctionnalités dont nous avons besoin.

## Étape 2 : Définir le tableau de données

 Ensuite, nous allons mettre en œuvre le`ICellsDataTable` interface pour créer une classe qui fournit les données à importer. Voici comment vous pouvez structurer l'`CellsDataTable` classe:

```csharp
class CellsDataTable : ICellsDataTable
{
    int m_index = -1;
    static String[] colsNames = new String[] { "Pet", "Fruit", "Country", "Color" };
    static String[] col0data = new String[] { "Dog", "Cat", "Duck" };
    static String[] col1data = new String[] { "Apple", "Pear", "Banana" };
    static String[] col2data = new String[] { "UK", "USA", "China" };
    static String[] col3data = new String[] { "Red", "Green", "Blue" };
    static String[][] colsData = new String[][] { col0data, col1data, col2data, col3data };
    
    // ... Mettre en œuvre d'autres membres ...
}
```

Ici, nous définissons les noms des colonnes et les données de chaque colonne, ce qui facilitera la structure de notre table importée.

## Étape 3 : implémenter les membres de l'interface ICellsDataTable

 Dans le cadre de`CellsDataTable` classe, vous devez implémenter les membres de la`ICellsDataTable` interface. Voici l'implémentation requise :

```csharp
public object this[string columnName]
{
    get
    {
        throw new NotImplementedException();
    }
}

object ICellsDataTable.this[int columnIndex]
{
    get
    {
        return colsData[columnIndex][m_index];
    }
}

string[] ICellsDataTable.Columns
{
    get { return colsNames; }
}

int ICellsDataTable.Count
{
    get { return col0data.Length; }
}

void ICellsDataTable.BeforeFirst()
{
    m_index = -1;
}

bool ICellsDataTable.Next()
{
    m_index++;
    return (m_index < Count);
}
```

Cette partie de la classe gère la récupération des données, en définissant le nombre de lignes et de colonnes et en gérant l'état actuel de l'index.

## Étape 4 : Écrire la fonction principale

 Maintenant, créons le`Run`méthode pour orchestrer l'ensemble du processus d'importation de table :

```csharp
public static void Run()
{
    string sourceDir = "Your Document Directory\\";
    string outputDir = "Your Document Directory\\";
    
    CellsDataTable cellsDataTable = new CellsDataTable();
    Workbook wb = new Workbook(sourceDir + "sampleImportTableOptionsShiftFirstRowDown.xlsx");
    Worksheet ws = wb.Worksheets[0];
```

## Étape 5 : définir les options d’importation

 Pour contrôler le comportement d'importation, vous devez créer une instance de`ImportTableOptions` et définissez les propriétés en conséquence. Plus précisément, nous voulons définir`ShiftFirstRowDown` à`false`.

```csharp
    ImportTableOptions opts = new ImportTableOptions();
    opts.ShiftFirstRowDown = false; // Nous ne voulons pas décaler la première ligne vers le bas
```

## Étape 6 : Importer la table de données

 Nous pouvons maintenant importer les données de notre`CellsDataTable` dans la feuille de calcul.

```csharp
    ws.Cells.ImportData(cellsDataTable, 2, 2, opts);
}
```

Cette commande insérera directement votre table de données en commençant par la ligne et la colonne spécifiées.

## Étape 7 : Enregistrer le classeur

Enfin, nous allons enregistrer le classeur modifié dans un fichier :

```csharp
    wb.Save(outputDir + "outputImportTableOptionsShiftFirstRowDown-False.xlsx");
}
```

## Conclusion

Et voilà ! Vous avez appris à insérer des lignes DataTable dans une feuille Excel sans déplacer la première ligne à l'aide d'Aspose.Cells pour .NET. Ce processus simplifie non seulement la manipulation des données dans Excel, mais améliore également les performances de votre application en automatisant une tâche généralement fastidieuse. Grâce à ces connaissances, vous êtes mieux équipé pour gérer les tâches d'automatisation d'Excel, ce qui vous permet d'économiser du temps et des efforts.

## FAQ

### Qu'est-ce qu'Aspose.Cells pour .NET ?
Aspose.Cells pour .NET est une bibliothèque de programmation qui permet aux développeurs de créer, manipuler et convertir des fichiers Excel dans des applications .NET.

### Ai-je besoin d'une licence pour utiliser Aspose.Cells ?
Oui, vous aurez besoin d'une licence valide pour bénéficier de toutes les fonctionnalités. Cependant, un essai gratuit est disponible pour un premier test.

### Puis-je utiliser Aspose.Cells dans des applications Web ?
Absolument ! Aspose.Cells est parfait pour les applications de bureau, Web et cloud développées en .NET.

### Quels types de fichiers Excel puis-je créer avec Aspose.Cells ?
Vous pouvez créer une variété de formats de fichiers Excel, notamment XLSX, XLS, CSV, etc.

### Où puis-je obtenir de l'aide pour Aspose.Cells ?
 Vous pouvez poser des questions ou trouver de l'aide dans le[Forums Aspose](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
