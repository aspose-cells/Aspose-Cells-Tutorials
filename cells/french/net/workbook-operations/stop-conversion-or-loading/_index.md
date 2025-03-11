---
title: Arrêter la conversion ou le chargement à l'aide du moniteur d'interruption
linktitle: Arrêter la conversion ou le chargement à l'aide du moniteur d'interruption
second_title: API de traitement Excel Aspose.Cells .NET
description: Apprenez à arrêter la conversion du classeur dans Aspose.Cells pour .NET à l'aide d'Interrupt Monitor, avec un didacticiel détaillé étape par étape.
weight: 26
url: /fr/net/workbook-operations/stop-conversion-or-loading/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Arrêter la conversion ou le chargement à l'aide du moniteur d'interruption

## Introduction
Travailler avec des fichiers Excel volumineux implique souvent des processus longs qui peuvent consommer du temps et des ressources. Mais que se passerait-il si vous pouviez arrêter le processus de conversion à mi-chemin lorsque vous réalisez qu'un élément doit être modifié ? Aspose.Cells pour .NET dispose d'une fonctionnalité appelée Interrupt Monitor, qui vous permet d'interrompre la conversion d'un classeur vers un autre format comme PDF. Cela peut s'avérer très utile, en particulier lorsque vous travaillez avec des fichiers de données volumineux. Dans ce guide, nous vous expliquerons comment interrompre le processus de conversion à l'aide du moniteur d'interruption dans Aspose.Cells pour .NET.
## Prérequis
Avant de vous lancer, assurez-vous d'avoir les éléments suivants en place :
1.  Aspose.Cells pour .NET - Téléchargez-le[ici](https://releases.aspose.com/cells/net/).
2. Environnement de développement .NET - tel que Visual Studio.
3. Connaissances de base de la programmation C# - La familiarité avec la syntaxe C# vous aidera à suivre.
## Paquets d'importation
Pour commencer, importons les paquets nécessaires. Ces importations incluent :
- Aspose.Cells : La bibliothèque principale pour la manipulation de fichiers Excel.
- System.Threading : pour gérer les threads, car cet exemple exécutera deux processus parallèles.
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading;
using System.IO;
```
Décomposons le processus en étapes détaillées. Chaque étape vous aidera à comprendre l'importance de configurer et d'utiliser le moniteur d'interruption pour gérer la conversion des classeurs Excel.
## Étape 1 : créer la classe et définir le répertoire de sortie
Tout d’abord, nous avons besoin d’une classe pour encapsuler nos fonctions, ainsi que d’un répertoire où le fichier de sortie sera enregistré.
```csharp
class StopConversionOrLoadingUsingInterruptMonitor
{
    static string outputDir = "Your Document Directory";
}
```
 Remplacer`"Your Document Directory"` avec le chemin réel où vous souhaitez que le fichier PDF soit enregistré.
## Étape 2 : instancier le moniteur d'interruption
Ensuite, créez un objet InterruptMonitor. Ce moniteur permettra de contrôler le processus en configurant la capacité de l'interrompre à tout moment.
```csharp
InterruptMonitor im = new InterruptMonitor();
```
Ce moniteur d'interruption sera attaché à notre classeur, nous permettant de gérer le processus de conversion.
## Étape 3 : Configurer le classeur pour la conversion
Maintenant, créons un objet classeur, affectons-lui InterruptMonitor, puis accédons à la première feuille de calcul pour insérer un exemple de texte.
```csharp
void CreateWorkbookAndConvertItToPdfFormat()
{
    Workbook wb = new Workbook();
    wb.InterruptMonitor = im;
    Worksheet ws = wb.Worksheets[0];
    Cell cell = ws.Cells["J1000000"];
    cell.PutValue("This is text.");
}
```
Le code ci-dessus crée un classeur, définit l'InterruptMonitor pour celui-ci et place le texte dans une cellule éloignée (`J1000000`). Placer du texte à cette position de cellule garantit que le traitement du classeur prendra plus de temps, ce qui donne à InterruptMonitor suffisamment de temps pour intervenir.
## Étape 4 : Enregistrer le classeur au format PDF et gérer les interruptions
 Essayons maintenant d'enregistrer le classeur au format PDF. Nous utiliserons un`try-catch` bloquer pour gérer toute interruption qui pourrait survenir.
```csharp
try
{
    wb.Save(outputDir + "output_InterruptMonitor.pdf");
}
catch (Aspose.Cells.CellsException ex)
{
    Console.WriteLine("Process Interrupted - Message: " + ex.Message);
}
```
Si le processus est interrompu, l'exception l'interceptera et affichera un message approprié. Sinon, le classeur sera enregistré au format PDF.
## Étape 5 : Interrompre le processus de conversion
 La fonctionnalité principale ici est la possibilité d'interrompre le processus. Nous allons ajouter un délai en utilisant`Thread.Sleep` et puis appelez le`Interrupt()` méthode pour arrêter la conversion après 10 secondes.
```csharp
void WaitForWhileAndThenInterrupt()
{
    Thread.Sleep(1000 * 10);
    im.Interrupt();
}
```
Ce délai donne au classeur le temps de commencer la conversion au format PDF avant que le signal d'interruption ne soit envoyé.
## Étape 6 : Exécuter les threads simultanément
Pour tout mettre ensemble, nous devons démarrer les deux fonctions dans des threads séparés. De cette façon, la conversion du classeur et l'attente d'interruption peuvent se produire simultanément.
```csharp
public void TestRun()
{
    ThreadStart ts1 = new ThreadStart(this.CreateWorkbookAndConvertItToPdfFormat);
    Thread t1 = new Thread(ts1);
    t1.Start();
    ThreadStart ts2 = new ThreadStart(this.WaitForWhileAndThenInterrupt);
    Thread t2 = new Thread(ts2);
    t2.Start();
    t1.Join();
    t2.Join();
}
```
 Le code ci-dessus s'exécute`CreateWorkbookAndConvertItToPdfFormat` et`WaitForWhileAndThenInterrupt` dans des threads parallèles, en les rejoignant une fois les deux processus terminés.
## Étape 7 : Exécution finale
 Enfin, nous ajouterons un`Run()` méthode pour exécuter le code.
```csharp
public static void Run()
{
    new StopConversionOrLoadingUsingInterruptMonitor().TestRun();
    Console.WriteLine("StopConversionOrLoadingUsingInterruptMonitor executed successfully.");
}
```
 Ce`Run` la méthode est le point d'entrée pour démarrer et observer l'interruption de l'action.
## Conclusion
Dans ce didacticiel, nous avons exploré comment interrompre le processus de conversion dans Aspose.Cells pour .NET. Le moniteur d'interruption est un outil utile lorsque vous travaillez avec des fichiers Excel volumineux, vous permettant d'arrêter les processus sans attendre qu'ils se terminent. Cela est particulièrement utile dans les scénarios où le temps et les ressources sont précieux et où un retour d'information rapide est nécessaire.
## FAQ
### Qu'est-ce qu'un moniteur d'interruption dans Aspose.Cells pour .NET ?  
Le moniteur d'interruption vous permet d'arrêter une conversion de classeur ou de charger un processus à mi-chemin.
### Puis-je utiliser Interrupt Monitor pour d’autres formats que PDF ?  
Oui, vous pouvez également interrompre les conversions vers d’autres formats pris en charge.
### Comment Thread.Sleep() affecte-t-il le timing de l'interruption ?  
Thread.Sleep() crée un délai avant de déclencher l'interruption, donnant le temps à la conversion de démarrer.
### Puis-je interrompre le processus avant 10 secondes ?  
 Oui, modifier le délai dans`WaitForWhileAndThenInterrupt()` à un temps plus court.
### Le processus d’interruption aura-t-il un impact sur les performances ?  
L’impact est minime et il est très bénéfique pour la gestion des processus de longue durée.
 Pour plus d'informations, reportez-vous à la[Documentation Aspose.Cells pour .NET](https://reference.aspose.com/cells/net/) . Si vous avez besoin d'aide, consultez le[Forum de soutien](https://forum.aspose.com/c/cells/9)ou obtenir un[Essai gratuit](https://releases.aspose.com/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
