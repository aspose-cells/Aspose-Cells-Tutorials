---
"description": "Découvrez comment mettre à jour les formules Power Query dans Excel avec Aspose.Cells pour .NET dans ce guide complet étape par étape."
"linktitle": "Mettre à jour l'élément de formule Power Query dans le classeur"
"second_title": "API de traitement Excel Aspose.Cells .NET"
"title": "Mettre à jour l'élément de formule Power Query dans le classeur"
"url": "/fr/net/workbook-operations/update-power-query-formula-item/"
"weight": 27
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Mettre à jour l'élément de formule Power Query dans le classeur

## Introduction
Comprendre comment gérer efficacement les données avec Power Query dans Excel est essentiel pour tout analyste de données ou passionné d'Excel. Si vous avez déjà eu besoin de mettre à jour les éléments de formule de votre classeur Power Query, vous êtes au bon endroit. Ce guide est conçu pour vous aider à utiliser Aspose.Cells pour .NET afin de mettre à jour facilement les formules Power Query dans un classeur Excel. En quelques étapes simples, vous pourrez manipuler et rationaliser vos données, garantissant ainsi la dynamique et la centralisation de vos classeurs.
## Prérequis
Avant de commencer à plonger dans l'exemple de code et les étapes, passons en revue ce dont vous aurez besoin :
1. Compréhension de base de C# et .NET : une connaissance des concepts de programmation en C# sera bénéfique car nous écrirons du code.
2. Installer Aspose.Cells pour .NET : la bibliothèque Aspose.Cells doit être intégrée à votre projet .NET. Vous pouvez la télécharger. [ici](https://releases.aspose.com/cells/net/).
3. Un fichier Excel prêt à être modifié : Assurez-vous de disposer d'un fichier Excel contenant une requête Power Query à mettre à jour. Vous devez disposer d'un classeur d'exemple, comme `SamplePowerQueryFormula.xlsx` à votre disposition.
## Importer des packages
Pour commencer, assurez-vous que les espaces de noms suivants sont inclus dans votre fichier C# :
```csharp
using Aspose.Cells.DigitalSignatures;
using Aspose.Cells.QueryTables;
using System;
using System.IO;
```
Cela vous permettra d'accéder aux fonctionnalités fournies par la bibliothèque Aspose.Cells, notamment pour travailler avec des classeurs et des données Power Query.
## Étape 1 : Configurez vos répertoires de travail
Tout d’abord, vous devez définir où se trouvent vos fichiers source et de sortie. 
```csharp
string SourceDir = "Your Document Directory";
string outputDir = "Your Document Directory";
```
Dans cette étape, vous spécifiez les chemins d'accès aux répertoires. Remplacer `"Your Document Directory"` avec le chemin d'accès réel où sont enregistrés vos fichiers Excel. Cela indique au programme où rechercher votre fichier source et où enregistrer le fichier mis à jour.
## Étape 2 : Charger le classeur
Maintenant que vos répertoires de travail sont définis, l’étape suivante consiste à charger votre fichier Excel dans le programme.
```csharp
Workbook workbook = new Workbook(SourceDir + "SamplePowerQueryFormula.xlsx");
```
Ici, vous créez un `Workbook` objet qui charge le fichier Excel spécifié. `Workbook` La classe fait partie de la bibliothèque Aspose.Cells et est essentielle pour toutes les opérations que vous effectuerez sur ce fichier Excel.
## Étape 3 : Accéder aux données Power Query
Une fois le classeur chargé, il est temps d'accéder aux formules Power Query stockées à l'intérieur.
```csharp
DataMashup mashupData = workbook.DataMashup;
```
Dans cette ligne, le `DataMashup` La propriété permet d'accéder aux structures de données Power Query du classeur. Elle vous permet d'interagir avec différents aspects des données Power Query contenues dans votre fichier Excel.
## Étape 4 : Parcourir les formules Power Query
Une fois les données Power Query accessibles, l’étape suivante consiste à parcourir chacune des formules présentes.
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
C'est ici que la magie opère. Nous parcourons chaque `PowerQueryFormula` et puis à travers chaque `PowerQueryFormulaItem`. Le `if` L'instruction recherche l'élément de formule « Source » et met à jour sa valeur pour indiquer le chemin du fichier source auquel Power Query doit faire référence. Cela vous permet de modifier dynamiquement le fichier d'où Power Query extrait les données.
## Étape 5 : Enregistrer le classeur mis à jour
Après avoir mis à jour les éléments de formule nécessaires, votre dernière étape consiste à enregistrer le classeur.
```csharp
workbook.Save(outputDir + "SamplePowerQueryFormula_out.xlsx");
```
Cette ligne enregistre le classeur modifié dans un nouveau fichier, préservant ainsi l'original tout en vous permettant de travailler avec la version mise à jour.
## Étape 6 : Message de confirmation
Enfin, c'est une bonne pratique de vérifier si votre code s'est exécuté correctement.
```csharp
Console.WriteLine("UpdatePowerQueryFormulaItem executed successfully.");
```
Ce simple message vous confirmera dans la console que votre opération a réussi, offrant une fin rassurante au processus.
## Conclusion
Et voilà ! Mettre à jour les éléments de formule Power Query dans Excel avec Aspose.Cells pour .NET se fait en quelques étapes simples. En suivant ce guide, vous pourrez gérer efficacement vos connexions de données Excel et assurer le bon fonctionnement de vos classeurs. Que vous soyez un expert chevronné ou un débutant en manipulation de données, Aspose.Cells offre un moyen puissant d'automatiser et d'optimiser les flux de travail Excel. 
## FAQ
### Puis-je utiliser Aspose.Cells avec n’importe quelle version de .NET ?
Aspose.Cells est compatible avec plusieurs versions de .NET, notamment .NET Framework et .NET Core.
### Aspose.Cells est-il gratuit à utiliser ?
Aspose.Cells propose un essai gratuit, mais une licence est requise pour une utilisation continue. Vous pouvez obtenir une licence temporaire. [ici](https://purchase.aspose.com/temporary-license/).
### Que faire si mon fichier Excel existant ne contient pas Power Query ?
Le processus décrit se concentre sur la mise à jour des éléments Power Query. Par conséquent, si votre fichier en manque, vous devez d'abord intégrer Power Queries.
### Où puis-je trouver plus d'informations sur Aspose.Cells ?
Consultez la documentation pour des conseils complets et des exemples. Visitez le [documentation](https://reference.aspose.com/cells/net/).
### Comment signaler des bugs ou des problèmes avec Aspose.Cells ?
Vous pouvez les contacter sur leur forum pour obtenir de l'aide concernant tout problème que vous rencontrez.


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}