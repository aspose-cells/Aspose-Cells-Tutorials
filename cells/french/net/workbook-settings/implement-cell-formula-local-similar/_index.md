---
"description": "Découvrez comment implémenter une formule de cellule similaire à la fonctionnalité locale de formule de plage dans Aspose.Cells pour .NET. Apprenez à personnaliser les noms des fonctions Excel intégrées et bien plus encore."
"linktitle": "Implémenter une formule de cellule locale similaire à une formule de plage locale"
"second_title": "API de traitement Excel Aspose.Cells .NET"
"title": "Implémenter une formule de cellule locale similaire à une formule de plage locale"
"url": "/fr/net/workbook-settings/implement-cell-formula-local-similar/"
"weight": 13
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Implémenter une formule de cellule locale similaire à une formule de plage locale

## Introduction
Aspose.Cells pour .NET est une API de manipulation de feuilles de calcul puissante et flexible qui vous permet de créer, manipuler et convertir des fichiers Excel par programmation. Aspose.Cells offre notamment la possibilité de personnaliser le comportement des fonctions Excel intégrées, notamment de créer vos propres noms de fonctions locales. Dans ce tutoriel, nous vous guiderons pas à pas pour implémenter une formule de cellule similaire à la fonctionnalité locale de formule de plage d'Aspose.Cells pour .NET.
## Prérequis
Avant de commencer, assurez-vous d’avoir les éléments suivants :
1. Microsoft Visual Studio 2010 ou version ultérieure installé sur votre système.
2. La dernière version de la bibliothèque Aspose.Cells pour .NET installée dans votre projet. Vous pouvez la télécharger depuis le [Page de téléchargement d'Aspose.Cells pour .NET](https://releases.aspose.com/cells/net/).
## Importer des packages
Pour commencer, vous devez importer les packages nécessaires dans votre projet C#. Ajoutez les instructions using suivantes en haut de votre fichier de code :
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
## Étape 1 : Créer une classe de paramètres de globalisation personnalisée
La première étape consiste à créer un profil personnalisé `GlobalizationSettings` Cette classe vous permettra de modifier le comportement par défaut des fonctions Excel. Dans cet exemple, nous allons modifier les noms des `SUM` et `AVERAGE` fonctions à `UserFormulaLocal_SUM` et `UserFormulaLocal_AVERAGE`, respectivement.
```csharp
class GS : GlobalizationSettings
{
    public override string GetLocalFunctionName(string standardName)
    {
        //Modifiez le nom de la fonction SOMME selon vos besoins.
        if (standardName == "SUM")
        {
            return "UserFormulaLocal_SUM";
        }
        //Modifiez le nom de la fonction MOYENNE selon vos besoins.
        if (standardName == "AVERAGE")
        {
            return "UserFormulaLocal_AVERAGE";
        }
        return "";
    }
}
```
## Étape 2 : Créer un nouveau classeur et attribuer les paramètres de globalisation personnalisés
Ensuite, créez une nouvelle instance de classeur et attribuez-lui la valeur personnalisée. `GlobalizationSettings` classe d'implémentation du classeur `Settings.GlobalizationSettings` propriété.
```csharp
//Créer un classeur
Workbook wb = new Workbook();
//Attribuer la classe d'implémentation GlobalizationSettings
wb.Settings.GlobalizationSettings = new GS();
```
## Étape 3 : Accéder à la première feuille de calcul et à une cellule
Maintenant, accédons à la première feuille de calcul du classeur et à une cellule spécifique dans cette feuille de calcul.
```csharp
//Accéder à la première feuille de calcul
Worksheet ws = wb.Worksheets[0];
//Accéder à certaines cellules
Cell cell = ws.Cells["C4"];
```
## Étape 4 : Attribuer des formules et imprimer la formule locale
Enfin, attribuons le `SUM` et `AVERAGE` formules dans la cellule et imprimer le résultat `FormulaLocal` valeurs.
```csharp
//Attribuer la formule SUM et imprimer sa formule locale
cell.Formula = "SUM(A1:A2)";
Console.WriteLine("Formula Local: " + cell.FormulaLocal);
//Attribuer la formule MOYENNE et imprimer sa formule locale
cell.Formula = "=AVERAGE(B1:B2, B5)";
Console.WriteLine("Formula Local: " + cell.FormulaLocal);
```
## Conclusion
Dans ce tutoriel, vous avez appris à implémenter une formule de cellule similaire à la fonctionnalité locale de formule de plage dans Aspose.Cells pour .NET. En créant une formule personnalisée, `GlobalizationSettings` Avec la classe, vous pouvez remplacer le comportement par défaut des fonctions Excel et personnaliser les noms de fonctions locales selon vos besoins. Cela peut être particulièrement utile lorsque vous travaillez avec des documents Excel localisés ou internationalisés.
## FAQ
### Quel est le but de la `GlobalizationSettings` classe dans Aspose.Cells ?
Le `GlobalizationSettings` La classe dans Aspose.Cells vous permet de personnaliser le comportement des fonctions Excel intégrées, y compris la possibilité de modifier les noms des fonctions locales.
### Puis-je remplacer le comportement de fonctions autres que `SUM` et `AVERAGE`?
Oui, vous pouvez remplacer le comportement de n’importe quelle fonction Excel intégrée en modifiant le `GetLocalFunctionName` méthode dans votre coutume `GlobalizationSettings` classe.
### Existe-t-il un moyen de réinitialiser les noms de fonction à leurs valeurs par défaut ?
Oui, vous pouvez réinitialiser les noms de fonction en supprimant les noms personnalisés. `GlobalizationSettings` classe ou en renvoyant une chaîne vide à partir de la `GetLocalFunctionName` méthode.
### Puis-je utiliser cette fonctionnalité pour créer des fonctions personnalisées dans Aspose.Cells ?
Non, le `GlobalizationSettings` Cette classe est conçue pour remplacer le comportement des fonctions Excel intégrées, et non pour créer des fonctions personnalisées. Pour créer des fonctions personnalisées, utilisez la classe `UserDefinedFunction` classe dans Aspose.Cells.
### Cette fonctionnalité est-elle disponible dans toutes les versions d'Aspose.Cells pour .NET ?
Oui, le `GlobalizationSettings` la classe et la possibilité de personnaliser les noms de fonctions sont disponibles dans toutes les versions d'Aspose.Cells pour .NET.


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}