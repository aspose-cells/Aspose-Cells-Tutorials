---
title: Mettre à jour l'élément de formule Power Query dans le classeur
linktitle: Mettre à jour l'élément de formule Power Query dans le classeur
second_title: API de traitement Excel Aspose.Cells .NET
description: Découvrez comment mettre à jour les formules Power Query dans Excel avec Aspose.Cells pour .NET dans ce guide complet étape par étape.
weight: 27
url: /fr/net/workbook-operations/update-power-query-formula-item/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Mettre à jour l'élément de formule Power Query dans le classeur

## Introduction
Il est primordial pour tout analyste de données ou passionné d'Excel de comprendre comment gérer efficacement les données à l'aide de Power Query dans Excel. Si vous avez déjà eu besoin de mettre à jour les éléments de formule dans votre classeur Power Query, vous êtes au bon endroit. Ce guide est conçu pour vous aider à apprendre à utiliser Aspose.Cells pour .NET pour mettre à jour de manière transparente les formules Power Query dans un classeur Excel. En quelques étapes simples, vous pourrez manipuler et rationaliser vos données, en veillant à ce que vos classeurs restent dynamiques et centralisés.
## Prérequis
Avant de commencer à plonger dans l'exemple de code et les étapes, passons en revue ce dont vous aurez besoin :
1. Compréhension de base de C# et .NET : la familiarité avec les concepts de programmation en C# sera bénéfique car nous allons écrire du code.
2.  Installer Aspose.Cells pour .NET : vous devez avoir la bibliothèque Aspose.Cells intégrée à votre projet .NET. Vous pouvez la télécharger[ici](https://releases.aspose.com/cells/net/).
3. Un fichier Excel prêt à être modifié : Assurez-vous que vous disposez d'un fichier Excel contenant une requête Power Query que vous souhaitez mettre à jour. Vous devez disposer d'un classeur d'exemple comme`SamplePowerQueryFormula.xlsx` à votre disposition.
## Paquets d'importation
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
 Dans cette étape, vous spécifiez les chemins d'accès aux répertoires. Remplacez`"Your Document Directory"` avec le chemin réel où vos fichiers Excel sont enregistrés. Cela indique au programme où chercher votre fichier source et où enregistrer le fichier mis à jour.
## Étape 2 : charger le classeur
Maintenant que vous avez défini vos répertoires de travail, l’étape suivante consiste à charger votre fichier Excel dans le programme.
```csharp
Workbook workbook = new Workbook(SourceDir + "SamplePowerQueryFormula.xlsx");
```
 Ici, vous créez un`Workbook` objet qui charge le fichier Excel spécifié.`Workbook`La classe fait partie de la bibliothèque Aspose.Cells et est essentielle pour toutes les opérations que vous effectuerez sur ce fichier Excel.
## Étape 3 : Accéder aux données Power Query
Une fois le classeur chargé, il est temps d’accéder aux formules Power Query qui y sont stockées.
```csharp
DataMashup mashupData = workbook.DataMashup;
```
 Dans cette ligne, le`DataMashup` La propriété permet d'accéder aux structures de données Power Query dans le classeur. Cette propriété vous permet d'interagir avec divers aspects des données Power Query contenues dans votre fichier Excel.
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
 C'est ici que la magie opère. Nous parcourons chaque`PowerQueryFormula` et puis à travers chaque`PowerQueryFormulaItem` . Le`if` L'instruction recherche l'élément de formule nommé « Source » et met à jour sa valeur pour qu'elle corresponde au chemin du fichier source auquel vous souhaitez que Power Query fasse référence. Cela vous permet de modifier de manière dynamique le fichier à partir duquel Power Query extrait les données.
## Étape 5 : Enregistrer le classeur mis à jour
Après avoir mis à jour les éléments de formule nécessaires, votre dernière étape consiste à enregistrer le classeur.
```csharp
workbook.Save(outputDir + "SamplePowerQueryFormula_out.xlsx");
```
Cette ligne enregistre le classeur modifié dans un nouveau fichier, préservant ainsi l'original tout en vous permettant de travailler avec la version mise à jour.
## Étape 6 : Message de confirmation
Enfin, c'est une bonne pratique de vérifier si votre code s'est exécuté correctement.
```csharp
Console.WriteLine("UpdatePowerQueryFormulaItem executed successfully.");
```
Ce simple message vous confirmera dans la console que votre opération a réussi, offrant ainsi une fin rassurante au processus.
## Conclusion
Et voilà ! La mise à jour des éléments de formule Power Query dans Excel à l'aide d'Aspose.Cells pour .NET peut être effectuée en quelques étapes simples. En suivant ce guide, vous pouvez gérer efficacement vos connexions de données Excel et assurer le bon fonctionnement de vos classeurs. Que vous soyez un professionnel chevronné ou que vous débutiez dans la manipulation de données, Aspose.Cells offre un moyen puissant d'automatiser et d'améliorer les flux de travail Excel. 
## FAQ
### Puis-je utiliser Aspose.Cells avec n'importe quelle version de .NET ?
Aspose.Cells est compatible avec plusieurs versions de .NET, notamment .NET Framework et .NET Core.
### L'utilisation d'Aspose.Cells est-elle gratuite ?
 Aspose.Cells propose un essai gratuit, mais pour une utilisation continue, une licence est requise. Vous pouvez obtenir une licence temporaire[ici](https://purchase.aspose.com/temporary-license/).
### Que faire si mon fichier Excel existant ne dispose pas de Power Query ?
Le processus décrit se concentre sur la mise à jour des éléments Power Query. Par conséquent, si votre fichier en manque, vous devez d’abord intégrer Power Queries.
### Où puis-je trouver plus d'informations sur Aspose.Cells ?
 Consultez la documentation pour obtenir des conseils complets et des exemples. Visitez le[documentation](https://reference.aspose.com/cells/net/).
### Comment signaler des bugs ou des problèmes avec Aspose.Cells ?
Vous pouvez les contacter sur leur forum d'assistance pour obtenir de l'aide concernant les problèmes que vous rencontrez.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
