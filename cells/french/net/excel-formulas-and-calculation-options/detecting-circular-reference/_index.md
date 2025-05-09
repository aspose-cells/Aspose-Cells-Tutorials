---
"description": "Détectez facilement les références circulaires dans Excel grâce à Aspose.Cells pour .NET. Suivez notre guide étape par étape pour garantir des calculs précis dans vos feuilles de calcul."
"linktitle": "Détection de référence circulaire dans Excel par programmation"
"second_title": "API de traitement Excel Aspose.Cells .NET"
"title": "Détection de référence circulaire dans Excel par programmation"
"url": "/fr/net/excel-formulas-and-calculation-options/detecting-circular-reference/"
"weight": 13
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Détection de référence circulaire dans Excel par programmation

## Introduction
Lorsque vous travaillez avec des fichiers Excel, l'un des problèmes les plus frustrants est la référence circulaire. Cela se produit lorsqu'une formule renvoie à sa propre cellule, directement ou indirectement, créant une boucle susceptible de perturber le moteur de calcul d'Excel. Mais pas d'inquiétude ! Avec Aspose.Cells pour .NET, vous pouvez détecter ces références circulaires gênantes par programmation, garantissant ainsi la fonctionnalité et la précision de vos feuilles de calcul. Dans ce guide, nous vous expliquons la procédure étape par étape, en toute simplicité.
## Prérequis
Avant de plonger dans le vif du sujet de la détection des références circulaires, assurons-nous que vous disposez de tout ce dont vous avez besoin pour commencer :
1. Visual Studio : Assurez-vous que Visual Studio est installé sur votre machine. Ce sera votre environnement de développement.
2. .NET Framework : assurez-vous que vous utilisez une version compatible du .NET Framework (au moins .NET Framework 4.0).
3. Bibliothèque Aspose.Cells : vous devez posséder la bibliothèque Aspose.Cells. Vous pouvez la télécharger depuis le [Site Web d'Aspose](https://releases.aspose.com/cells/net/).
4. Connaissances de base de C# : une familiarité avec la programmation C# sera bénéfique, car nous écrirons du code dans ce langage.
5. Fichier Excel : Préparez un fichier Excel contenant des références circulaires pour les tests. Vous pouvez en créer un simple ou télécharger un exemple.
Maintenant que nous avons nos prérequis en place, passons à la partie amusante !
## Importer des packages
Avant de commencer à coder, vous devez importer les packages nécessaires. Voici comment procéder :
### Créer un nouveau projet
- Ouvrez Visual Studio et créez un nouveau projet d’application console C#.
### Ajouter une référence Aspose.Cells
- Cliquez avec le bouton droit sur votre projet dans l’Explorateur de solutions.
- Sélectionnez « Gérer les packages NuGet ».
- Recherchez « Aspose.Cells » et installez la dernière version.
### Importer les espaces de noms requis
Au sommet de votre `Program.cs` fichier, importez les espaces de noms nécessaires :
```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Maintenant que tout est configuré, plongeons dans le code pour détecter les références circulaires dans un fichier Excel.
## Étape 1 : Définir le répertoire d’entrée
Tout d'abord, vous devez spécifier le répertoire où se trouve votre fichier Excel. C'est là que vous le chargerez.
```csharp
// Répertoire d'entrée
string sourceDir = "Your Document Directory";
```
Remplacer `"Your Document Directory"` avec le chemin réel vers votre fichier Excel.
## Étape 2 : Charger le classeur avec LoadOptions
Ensuite, vous chargerez votre classeur Excel. C'est là que la magie opère !
```csharp
LoadOptions loadOptions = new LoadOptions();
var objWB = new Aspose.Cells.Workbook(sourceDir + "Circular Formulas.xls", loadOptions);
```
Ici, nous créons une nouvelle instance de `LoadOptions` et chargez le classeur depuis le chemin spécifié. Assurez-vous que le nom de votre fichier Excel correspond !
## Étape 3 : Activer les paramètres d’itération
Pour autoriser les références circulaires, vous devez activer les paramètres d’itération dans le classeur.
```csharp
objWB.Settings.Iteration = true;
```
Cela indique à Aspose.Cells d'autoriser les références circulaires pendant le calcul.
## Étape 4 : Créer des options de calcul et un moniteur circulaire
Maintenant, créons les options de calcul et notre moniteur circulaire personnalisé.
```csharp
CalculationOptions copts = new CalculationOptions();
CircularMonitor cm = new CircularMonitor();
copts.CalculationMonitor = cm;
```
Ici, nous créons une instance de `CalculationOptions` et une coutume `CircularMonitor`Ce moniteur aidera à suivre toutes les références circulaires trouvées lors des calculs.
## Étape 5 : Calculer les formules
Maintenant, il est temps de calculer les formules dans votre classeur.
```csharp
objWB.CalculateFormula(copts);
```
Cette ligne exécute le calcul et vérifie les références circulaires.
## Étape 6 : Compter les références circulaires
Après le calcul, vous pouvez compter combien de références circulaires ont été trouvées.
```csharp
long lngCircularRef = cm.circulars.Count;
Console.WriteLine("Circular References found - " + lngCircularRef);
```
Cela affichera le nombre de références circulaires détectées dans votre fichier Excel.
## Étape 7 : Afficher les résultats
Enfin, affichons les résultats et confirmons que notre méthode s'est exécutée avec succès.
```csharp
Console.WriteLine("DetectCircularReference executed successfully.\r\n");
```
## Étape 8 : Implémenter la classe CircularMonitor
Pour terminer le processus, vous devrez mettre en œuvre les `CircularMonitor` classe. Cette classe héritera de `AbstractCalculationMonitor` et gérer la détection des références circulaires.
```csharp
public class CircularMonitor : AbstractCalculationMonitor
{
    public ArrayList circulars = new ArrayList();
    public ArrayList Circulars { get { return circulars; } }
    public override bool OnCircular(IEnumerator circularCellsData)
    {
        CalculationCell cc = null;
        ArrayList cur = new ArrayList();
        while (circularCellsData.MoveNext())
        {
            cc = (CalculationCell)circularCellsData.Current;
            cur.Add(cc.Worksheet.Name + "!" + CellsHelper.CellIndexToName(cc.CellRow, cc.CellColumn));
        }
        circulars.Add(cur);
        return true;
    }
}
```
Cette classe capture les détails de chaque référence circulaire trouvée, y compris le nom de la feuille de calcul et l'index de la cellule.
## Conclusion
Détecter les références circulaires dans Excel avec Aspose.Cells pour .NET est un processus simple une fois décomposé en étapes faciles à gérer. En suivant ce guide, vous pourrez facilement identifier et gérer les références circulaires dans vos feuilles de calcul, garantissant ainsi la précision et la fiabilité de vos calculs. Que vous soyez un développeur expérimenté ou débutant, Aspose.Cells offre des outils puissants pour améliorer vos capacités de manipulation dans Excel. 
## FAQ
### Qu'est-ce qu'une référence circulaire dans Excel ?
Une référence circulaire se produit lorsqu'une formule fait référence à sa propre cellule, provoquant une boucle sans fin dans les calculs.
### Comment puis-je détecter les références circulaires par programmation ?
Vous pouvez utiliser la bibliothèque Aspose.Cells dans .NET pour détecter par programmation les références circulaires en implémentant un moniteur de calcul personnalisé.
### Quelles sont les conditions préalables à l’utilisation d’Aspose.Cells ?
Vous devez installer Visual Studio, .NET Framework et la bibliothèque Aspose.Cells.
### Puis-je utiliser Aspose.Cells gratuitement ?
Oui, Aspose.Cells propose un essai gratuit que vous pouvez utiliser pour explorer ses fonctionnalités.
### Où puis-je trouver plus d'informations sur Aspose.Cells ?
Vous pouvez visiter le [Documentation d'Aspose.Cells](https://reference.aspose.com/cells/net/) pour des informations détaillées et des exemples.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}