---
title: Spécifier la compatibilité du fichier Excel par programmation dans .NET
linktitle: Spécifier la compatibilité du fichier Excel par programmation dans .NET
second_title: API de traitement Excel Aspose.Cells .NET
description: Apprenez à manipuler les tableaux croisés dynamiques Excel avec Aspose.Cells pour .NET, y compris les mises à jour de données, les paramètres de compatibilité et la mise en forme des cellules.
weight: 23
url: /fr/net/creating-and-configuring-pivot-tables/specifying-compatibility/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Spécifier la compatibilité du fichier Excel par programmation dans .NET

## Introduction

Dans le monde actuel axé sur les données, la gestion et la manipulation de fichiers Excel par programmation sont devenues essentielles pour de nombreux développeurs. Si vous travaillez avec Excel dans .NET, Aspose.Cells est une bibliothèque puissante qui facilite la création, la lecture, la modification et l'enregistrement de fichiers Excel. Une fonctionnalité importante de cette bibliothèque vous permet de spécifier la compatibilité des fichiers Excel par programmation. Dans ce didacticiel, nous allons découvrir comment manipuler les fichiers Excel, en nous concentrant notamment sur la gestion de la compatibilité à l'aide d'Aspose.Cells pour .NET. À la fin, vous comprendrez comment définir la compatibilité des fichiers Excel, en particulier pour les tableaux croisés dynamiques, tout en actualisant et en gérant les données.

## Prérequis

Avant de vous lancer dans la phase de codage, assurez-vous de disposer des éléments suivants :

1. Connaissances de base de C# : Étant donné que nous allons écrire du code en C#, une connaissance du langage vous aidera à mieux comprendre le didacticiel.
2.  Bibliothèque Aspose.Cells pour .NET : vous pouvez la télécharger à partir du[Page de sortie d'Aspose Cells](https://releases.aspose.com/cells/net/)Si vous ne l'avez pas déjà fait, pensez à obtenir un essai gratuit pour explorer ses fonctionnalités en premier.
3. Visual Studio : un IDE où vous pouvez écrire et tester efficacement votre code C#.
4.  Exemple de fichier Excel : Assurez-vous d'avoir un exemple de fichier Excel, de préférence un fichier contenant un tableau croisé dynamique pour la démonstration. Pour notre exemple, nous utiliserons`sample-pivot-table.xlsx`.

Une fois ces conditions préalables remplies, commençons le processus de codage.

## Paquets d'importation

Avant de commencer à écrire votre application, vous devez inclure les espaces de noms nécessaires dans votre code pour utiliser efficacement la bibliothèque Aspose.Cells. Voici comment procéder.

### Importer l'espace de noms Aspose.Cells

```csharp
using System.IO;
using System;
using Aspose.Cells;
using Aspose.Cells.Pivot;
using System.Drawing;
```

Cette ligne de code garantit que vous pouvez accéder à toutes les classes et méthodes de la bibliothèque Aspose.Cells.

Maintenant, décomposons le processus en détail pour nous assurer que tout est clair et compréhensible.

## Étape 1 : Configurez votre répertoire

Tout d'abord, définissez le répertoire dans lequel se trouvent vos fichiers Excel. Il est important de fournir le bon chemin d'accès au fichier.

```csharp
// Le chemin vers le répertoire des documents.
string dataDir = "Your Document Directory";
```

 Ici, remplacez`"Your Document Directory"`avec le chemin d'accès réel à vos fichiers Excel. C'est ici que votre fichier d'exemple de tableau croisé dynamique doit résider.

## Étape 2 : charger le fichier Excel source

Ensuite, nous devons charger le fichier Excel qui contient l’exemple de tableau croisé dynamique. 

```csharp
// Charger le fichier source Excel contenant un exemple de tableau croisé dynamique
Workbook wb = new Workbook(dataDir + "sample-pivot-table.xlsx");
```

 Dans cette étape, nous créons une instance de`Workbook` classe, qui charge le fichier Excel spécifié. 

## Étape 3 : Accéder aux feuilles de travail

Maintenant que le classeur est chargé, vous devez accéder à la feuille de calcul qui contient les données du tableau croisé dynamique.

```csharp
// Accédez à la première feuille de calcul contenant les données du tableau croisé dynamique
Worksheet dataSheet = wb.Worksheets[0];
```

Ici, nous accédons à la première feuille de calcul où se trouve le tableau croisé dynamique. Vous pouvez également parcourir ou spécifier d'autres feuilles de calcul en fonction de votre structure Excel.

## Étape 4 : Manipuler les données cellulaires

Ensuite, vous modifierez certaines valeurs de cellules dans la feuille de calcul. 

### Étape 4.1 : Modifier la cellule A3

Commençons par accéder à la cellule A3 et définir sa valeur.

```csharp
// Accéder à la cellule A3 et définir ses données
Cells cells = dataSheet.Cells;
Cell cell = cells["A3"];
cell.PutValue("FooBar");
```

Cet extrait de code met à jour la cellule A3 avec la valeur « FooBar ».

### Étape 4.2 : modifier la cellule B3 avec une longue chaîne

Maintenant, définissons une longue chaîne dans la cellule B3, qui dépasse les limites de caractères standard d'Excel.

```csharp
// Accéder à la cellule B3, définir ses données
string longStr = "Very long text 1. very long text 2.... [continue your long string]";
cell = cells["B3"];
cell.PutValue(longStr);
```

Ce code est important car il définit vos attentes concernant les limites de données, en particulier lorsque vous travaillez avec des paramètres de compatibilité dans Excel.

## Étape 5 : Vérifiez la longueur de la cellule B3

Il est également essentiel de confirmer la longueur de la chaîne que nous avons saisie.

```csharp
// Imprimer la longueur de la chaîne de la cellule B3
Console.WriteLine("Length of original data string: " + cell.StringValue.Length);
```

Il s'agit simplement d'une vérification pour montrer combien de caractères votre cellule contient.

## Étape 6 : définir d’autres valeurs de cellules

Nous allons maintenant accéder à plus de cellules et définir certaines valeurs.

```csharp
// Accéder à la cellule C3 et définir ses données
cell = cells["C3"];
cell.PutValue("closed");

// Accéder à la cellule D3 et définir ses données
cell = cells["D3"];
cell.PutValue("2016/07/21");
```

Chacun de ces extraits met à jour plusieurs cellules supplémentaires dans la feuille de calcul.

## Étape 7 : Accéder au tableau croisé dynamique

Ensuite, vous accéderez à la deuxième feuille de calcul, qui contient les données du tableau croisé dynamique.

```csharp
//Accéder à la deuxième feuille de calcul contenant le tableau croisé dynamique
Worksheet pivotSheet = wb.Worksheets[1];

// Accéder au tableau croisé dynamique
PivotTable pivotTable = pivotSheet.PivotTables[0];
```

Cet extrait vous permet de manipuler le tableau croisé dynamique pour les paramètres de compatibilité.

## Étape 8 : Définir la compatibilité pour Excel 2003

Il est essentiel de définir si votre tableau croisé dynamique est compatible avec Excel 2003 ou non. 

```csharp
// La propriété IsExcel2003Compatible indique si le tableau croisé dynamique est compatible avec Excel 2003 lors de l'actualisation du tableau croisé dynamique
pivotTable.IsExcel2003Compatible = true;
pivotTable.RefreshData();
pivotTable.CalculateData();
```

 C'est ici que commence la véritable transformation. En définissant`IsExcel2003Compatible` à`true`, vous limitez la longueur des caractères à 255 lors de l'actualisation.

## Étape 9 : Vérifier la longueur après le réglage de la compatibilité

Après avoir défini la compatibilité, voyons comment cela affecte les données.

```csharp
// Vérifiez la valeur de la cellule B5 de la feuille pivot.
Cell b5 = pivotSheet.Cells["B5"];
Console.WriteLine("Length of cell B5 after setting IsExcel2003Compatible property to True: " + b5.StringValue.Length);
```

Vous verrez probablement une sortie confirmant l’effet de troncature si les données initiales dépassent 255 caractères.

## Étape 10 : modifier le paramètre de compatibilité

Maintenant, modifions le paramètre de compatibilité et vérifions à nouveau.

```csharp
//Définissez maintenant la propriété IsExcel2003Compatible sur false et actualisez à nouveau
pivotTable.IsExcel2003Compatible = false;
pivotTable.RefreshData();
pivotTable.CalculateData();
```

Cela permet à vos données de refléter leur longueur d'origine sans les restrictions précédentes.

## Étape 11 : Vérifiez à nouveau la longueur 

Vérifions que les données reflètent désormais avec précision leur longueur réelle.

```csharp
// Il va maintenant imprimer la longueur originale des données de la cellule. Les données n'ont pas été tronquées maintenant.
b5 = pivotSheet.Cells["B5"];
Console.WriteLine("Length of cell B5 after setting IsExcel2003Compatible property to False: " + b5.StringValue.Length);
```

Vous devriez voir que la sortie confirme la suppression de la troncature.

## Étape 12 : formater les cellules

Pour améliorer l'expérience visuelle, vous souhaiterez peut-être formater les cellules. 

```csharp
// Définissez la hauteur de ligne et la largeur de colonne de la cellule B5 et ajustez également son texte.
pivotSheet.Cells.SetRowHeight(b5.Row, 100);
pivotSheet.Cells.SetColumnWidth(b5.Column, 65);
Style st = b5.GetStyle();
st.IsTextWrapped = true;
b5.SetStyle(st);
```

Ces lignes de code facilitent la lecture des données en ajustant les dimensions des cellules et en activant le retour à la ligne du texte.

## Étape 13 : Enregistrer le classeur

Enfin, enregistrez votre classeur avec les modifications que vous avez apportées.

```csharp
// Enregistrer le classeur au format xlsx
wb.Save(dataDir + "SpecifyCompatibility_out.xlsx", SaveFormat.Xlsx);
```

 Le choix d'un format de fichier approprié est crucial lors de l'enregistrement de fichiers Excel.`Xlsx`Le format est largement utilisé et compatible avec de nombreuses versions d'Excel.

## Conclusion

Félicitations ! Vous avez maintenant programmé les paramètres de compatibilité des fichiers Excel à l'aide d'Aspose.Cells pour .NET. Ce didacticiel décrit chaque étape, de la configuration de votre environnement à la modification des paramètres de compatibilité des tableaux croisés dynamiques. Si vous avez déjà travaillé avec des données nécessitant des limitations ou une compatibilité spécifiques, il s'agit d'une compétence à ne pas négliger.

## FAQ

### Qu'est-ce qu'Aspose.Cells ?  
Aspose.Cells est une bibliothèque .NET conçue pour aider les développeurs à créer, manipuler et convertir des fichiers Excel de manière transparente.

### Pourquoi la compatibilité Excel est-elle importante ?  
La compatibilité Excel est essentielle pour garantir que les fichiers peuvent être ouverts et utilisés dans les versions prévues d'Excel, en particulier s'ils contiennent des fonctionnalités ou des formats non pris en charge dans les versions antérieures.

### Puis-je créer des tableaux croisés dynamiques par programmation avec Aspose.Cells ?  
Oui, vous pouvez créer et manipuler des tableaux croisés dynamiques par programmation à l'aide d'Aspose.Cells. La bibliothèque fournit diverses méthodes pour ajouter des sources de données, des champs et des fonctionnalités associées aux tableaux croisés dynamiques.

### Comment vérifier la longueur d'une chaîne dans une cellule Excel ?  
Vous pouvez utiliser le`StringValue` propriété d'un`Cell` objet pour obtenir le contenu de la cellule, puis appeler le`.Length` propriété pour connaître la longueur de la chaîne.

### Puis-je personnaliser la mise en forme des cellules au-delà de la hauteur et de la largeur des lignes ?  
 Absolument ! Aspose.Cells permet un formatage complet des cellules. Vous pouvez modifier les styles de police, les couleurs, les bordures, les formats de nombres et bien plus encore via le`Style` classe.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
