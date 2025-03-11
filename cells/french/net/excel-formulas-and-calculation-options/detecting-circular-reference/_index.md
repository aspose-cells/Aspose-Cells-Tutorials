---
title: Détection de référence circulaire dans Excel par programmation
linktitle: Détection de référence circulaire dans Excel par programmation
second_title: API de traitement Excel Aspose.Cells .NET
description: Détectez facilement les références circulaires dans Excel à l'aide d'Aspose.Cells pour .NET. Suivez notre guide étape par étape pour garantir des calculs précis dans vos feuilles de calcul.
weight: 13
url: /fr/net/excel-formulas-and-calculation-options/detecting-circular-reference/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Détection de référence circulaire dans Excel par programmation

## Introduction
Lorsque vous travaillez avec des fichiers Excel, l'un des problèmes les plus frustrants que vous pouvez rencontrer est une référence circulaire. Cela se produit lorsqu'une formule renvoie à sa propre cellule, directement ou indirectement, créant une boucle qui peut perturber le moteur de calcul d'Excel. Mais n'ayez crainte ! Avec Aspose.Cells pour .NET, vous pouvez détecter par programmation ces références circulaires gênantes, garantissant ainsi que vos feuilles de calcul restent fonctionnelles et précises. Dans ce guide, nous vous guiderons pas à pas tout au long du processus, le rendant aussi simple que bonjour.
## Prérequis
Avant de plonger dans le vif du sujet de la détection des références circulaires, assurons-nous que vous disposez de tout ce dont vous avez besoin pour commencer :
1. Visual Studio : assurez-vous que Visual Studio est installé sur votre ordinateur. Il s'agira de votre environnement de développement.
2. .NET Framework : assurez-vous que vous utilisez une version compatible du .NET Framework (au moins .NET Framework 4.0).
3.  Bibliothèque Aspose.Cells : Vous devez disposer de la bibliothèque Aspose.Cells. Vous pouvez la télécharger à partir du[Site Web d'Aspose](https://releases.aspose.com/cells/net/).
4. Connaissances de base de C# : une familiarité avec la programmation C# sera bénéfique, car nous écrirons du code dans ce langage.
5. Fichier Excel : préparez un fichier Excel contenant des références circulaires à tester. Vous pouvez en créer un simple ou télécharger un exemple.
Maintenant que nous avons mis en place nos prérequis, passons à la partie amusante !
## Paquets d'importation
Avant de pouvoir commencer à coder, vous devez importer les packages nécessaires. Voici comment procéder :
### Créer un nouveau projet
- Ouvrez Visual Studio et créez un nouveau projet d’application console C#.
### Ajouter une référence Aspose.Cells
- Faites un clic droit sur votre projet dans l’Explorateur de solutions.
- Sélectionnez « Gérer les packages NuGet ».
- Recherchez « Aspose.Cells » et installez la dernière version.
### Importer les espaces de noms requis
 Au sommet de votre`Program.cs` fichier, importez les espaces de noms nécessaires :
```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Maintenant que nous avons tout configuré, plongeons dans le code pour détecter les références circulaires dans un fichier Excel.
## Étape 1 : définir le répertoire d’entrée
Tout d'abord, vous devez spécifier le répertoire dans lequel se trouve votre fichier Excel. C'est là que vous chargerez votre fichier Excel.
```csharp
// Répertoire d'entrée
string sourceDir = "Your Document Directory";
```
 Remplacer`"Your Document Directory"` avec le chemin réel vers votre fichier Excel.
## Étape 2 : charger le classeur avec LoadOptions
Ensuite, vous chargez votre classeur Excel. C'est là que la magie commence !
```csharp
LoadOptions loadOptions = new LoadOptions();
var objWB = new Aspose.Cells.Workbook(sourceDir + "Circular Formulas.xls", loadOptions);
```
 Ici, nous créons une nouvelle instance de`LoadOptions` et chargez le classeur à partir du chemin spécifié. Assurez-vous que le nom de votre fichier Excel correspond !
## Étape 3 : Activer les paramètres d’itération
Pour autoriser les références circulaires, vous devez activer les paramètres d'itération dans le classeur.
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
 Ici, nous créons une instance de`CalculationOptions` et une coutume`CircularMonitor`Ce moniteur aidera à suivre toutes les références circulaires trouvées lors des calculs.
## Étape 5 : Calculer les formules
Maintenant, il est temps de calculer les formules dans votre classeur.
```csharp
objWB.CalculateFormula(copts);
```
Cette ligne exécute le calcul et vérifie les références circulaires.
## Étape 6 : Compter les références circulaires
Après le calcul, vous pouvez compter combien de références circulaires ont été trouvées.
```csharp
long lngCircularRef = cm.circulars.Count;
Console.WriteLine("Circular References found - " + lngCircularRef);
```
Cela affichera le nombre de références circulaires détectées dans votre fichier Excel.
## Étape 7 : Afficher les résultats
Enfin, affichons les résultats et confirmons que notre méthode a été exécutée avec succès.
```csharp
Console.WriteLine("DetectCircularReference executed successfully.\r\n");
```
## Étape 8 : implémenter la classe CircularMonitor
 Pour terminer le processus, vous devrez mettre en œuvre le`CircularMonitor` classe. Cette classe héritera de`AbstractCalculationMonitor` et gérer la détection des références circulaires.
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
La détection des références circulaires dans Excel à l'aide d'Aspose.Cells pour .NET est un processus simple une fois que vous l'avez décomposé en étapes gérables. En suivant ce guide, vous pouvez facilement identifier et gérer les références circulaires dans vos feuilles de calcul, garantissant ainsi que vos calculs restent précis et fiables. Que vous soyez un développeur chevronné ou que vous débutiez, Aspose.Cells fournit des outils puissants pour améliorer vos capacités de manipulation d'Excel. 
## FAQ
### Qu'est-ce qu'une référence circulaire dans Excel ?
Une référence circulaire se produit lorsqu'une formule renvoie à sa propre cellule, provoquant une boucle sans fin dans les calculs.
### Comment puis-je détecter les références circulaires par programmation ?
Vous pouvez utiliser la bibliothèque Aspose.Cells dans .NET pour détecter par programmation les références circulaires en implémentant un moniteur de calcul personnalisé.
### Quelles sont les conditions préalables à l'utilisation d'Aspose.Cells ?
Vous devez installer Visual Studio, .NET Framework et la bibliothèque Aspose.Cells.
### Puis-je utiliser Aspose.Cells gratuitement ?
Oui, Aspose.Cells propose un essai gratuit que vous pouvez utiliser pour explorer ses fonctionnalités.
### Où puis-je trouver plus d'informations sur Aspose.Cells ?
 Vous pouvez visiter le[Documentation d'Aspose.Cells](https://reference.aspose.com/cells/net/) pour des informations détaillées et des exemples.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
