---
"description": "Mettez à jour facilement les éléments de formule Power Query dans Excel grâce à Aspose.Cells pour .NET. Guide étape par étape pour optimiser vos processus de manipulation de données."
"linktitle": "Mettre à jour l'élément de formule Power Query"
"second_title": "Référence de l'API Aspose.Cells pour .NET"
"title": "Mettre à jour l'élément de formule Power Query"
"url": "/fr/net/excel-workbook/update-power-query-formula-item/"
"weight": 160
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Mettre à jour l'élément de formule Power Query

## Introduction

Si vous avez déjà travaillé avec Excel, vous savez à quel point il peut être puissant, surtout lorsque vous vous lancez dans Power Queries. C'est le secret pour transformer, nettoyer et analyser vos données sans effort. Aspose.Cells pour .NET est une méthode astucieuse pour manipuler vos formules Power Query dans Excel. Aujourd'hui, nous vous guidons pas à pas dans la mise à jour des éléments de formule Power Query. Alors, à vos codes !

## Prérequis

Avant de vous plonger dans le code, vous devez configurer quelques éléments :

1. Visual Studio : vous aurez besoin d'un environnement de développement intégré (IDE) pour écrire et exécuter votre code .NET. Visual Studio est la solution idéale.
2. Bibliothèque Aspose.Cells : Assurez-vous que la bibliothèque Aspose.Cells est disponible dans votre projet. Vous pouvez la télécharger depuis le [site](https://releases.aspose.com/cells/net/).
3. Connaissances de base de C# : bien que nous allons parcourir cela ensemble, avoir une compréhension fondamentale de C# sera certainement utile, en particulier lors de la navigation dans différentes classes et méthodes.
4. Exemples de fichiers Excel : Vous aurez besoin des fichiers Excel mentionnés dans l'extrait de code. Assurez-vous d'avoir :
   - `SamplePowerQueryFormula.xlsx`
   - `SamplePowerQueryFormulaSource.xlsx`

5. .NET Framework : assurez-vous que votre projet cible une version compatible du .NET Framework.

Maintenant que notre kit est prêt, nous pouvons passer à la partie amusante : écrire du code !

## Importer des packages

Tout d'abord, vous devez importer les espaces de noms nécessaires. Voici comment procéder :

```csharp
using Aspose.Cells.DigitalSignatures;
using Aspose.Cells.QueryTables;
using System;
using System.IO;
```

En ajoutant ces espaces de noms, vous indiquez au compilateur que vous souhaitez utiliser les classes et méthodes de la bibliothèque Aspose.Cells. Cette étape est cruciale, car elle pose les bases du code qui suit.

Décomposons l'extrait de code que vous avez fourni. Ce tutoriel vous guidera à travers chaque partie, vous permettant de comprendre le fonctionnement.

## Étape 1 : Configurer les répertoires de travail

Dans cette étape, nous allons définir l'emplacement de nos fichiers source et de sortie. Cela permettra à Aspose de savoir où rechercher vos fichiers Excel.

```csharp
// Répertoires de travail
string SourceDir = "Your Document Directory";
string outputDir = "Your Output Directory";
```

## Étape 2 : Charger le classeur

Maintenant, chargeons le fichier Excel dans lequel réside Power Query.

```csharp
Workbook workbook = new Workbook(SourceDir + "SamplePowerQueryFormula.xlsx");
```
Le `Workbook` La classe est le point d'entrée du fichier Excel. En transmettant le chemin d'accès à notre fichier source, nous créons une instance permettant de le manipuler. Imaginez l'ouverture d'un livre : vous vous apprêtez à lire (ou à modifier) son contenu.

## Étape 3 : Accéder au mashup de données

Ensuite, nous accéderons aux formules Power Query stockées dans le Data Mashup du classeur.

```csharp
DataMashup mashupData = workbook.DataMashup;
```
Le `DataMashup` La classe contient toutes les formules Power Query associées à votre classeur. C'est ici que nous allons effectuer le gros du travail, un peu comme lorsque vous ouvrez une boîte à outils pour effectuer des réparations.

## Étape 4 : Parcourir les formules Power Query

Vient maintenant la partie où nous parcourons les formules Power Query pour trouver celle spécifique que nous souhaitons mettre à jour.

```csharp
foreach (PowerQueryFormula formula in mashupData.PowerQueryFormulas)
{
    foreach (PowerQueryFormulaItem item in formula.PowerQueryFormulaItems)
    {
        if (item.Name == "Source")
        {
            item.Value = "Excel.Workbook(File.Contents(\"" + SourceDir + "SamplePowerQueryFormulaSource.xlsx\"), null, true)";
        }
    }
}
```

- Nous parcourons chaque `PowerQueryFormula` dans `mashupData`.
- Dans cette boucle, nous plongeons dans chaque `PowerQueryFormulaItem`.
- Nous vérifions si le nom de l'élément correspond à « Source ». Si c'est le cas, nous mettons à jour sa valeur pour créer un lien vers notre nouveau fichier source.

C'est comme trouver la bonne page dans un manuel et effectuer les mises à jour nécessaires : c'est un processus simple et méticuleux.

## Étape 5 : Enregistrer le classeur mis à jour

Après avoir effectué les mises à jour, il est temps de sauvegarder nos modifications.

```csharp
// Enregistrez le classeur de sortie.
workbook.Save(outputDir + "SamplePowerQueryFormula_out.xlsx");
Console.WriteLine("UpdatePowerQueryFormulaItem executed successfully.");
```
Le `Save` La méthode écrit le classeur mis à jour dans le répertoire de sortie spécifié. C'est comme si vos modifications étaient scellées dans une nouvelle version du manuel, prête à être utilisée par d'autres !

## Conclusion

Félicitations ! Vous avez mis à jour avec succès un élément de formule Power Query avec Aspose.Cells pour .NET. Cette méthode vous permet d'automatiser la modification des formules Power Query dans vos fichiers Excel, vous faisant ainsi gagner un temps précieux.

## FAQ

### Qu'est-ce qu'Aspose.Cells ?
Aspose.Cells est une bibliothèque puissante permettant de manipuler des fichiers Excel dans des applications .NET sans avoir besoin d'installer Microsoft Excel.

### Ai-je besoin de Microsoft Excel pour exécuter Aspose.Cells ?
Non, Aspose.Cells vous permet de créer et de modifier des fichiers Excel par programmation sans avoir besoin d'Excel sur votre serveur ou votre machine de développement.

### Avec quels types de fichiers Excel puis-je travailler à l’aide d’Aspose.Cells ?
Vous pouvez travailler avec .xlsx, .xls, .xlsm et plusieurs autres formats Excel à l'aide d'Aspose.Cells.

### Existe-t-il une version d'essai disponible pour Aspose.Cells ?
Oui, vous pouvez télécharger une version d'essai gratuite à partir du [Page de publication d'Aspose Cells](https://releases.aspose.com/).

### Comment puis-je obtenir de l'aide pour Aspose.Cells ?
Vous pouvez accéder au support via le [Forum Aspose](https://forum.aspose.com/c/cells/9), où vous pouvez poser des questions et trouver des réponses de la communauté et de l'équipe Aspose.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}