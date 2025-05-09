---
"description": "Apprenez à contrôler les ressources externes dans Excel à l’aide d’Aspose.Cells pour .NET avec notre didacticiel complet étape par étape."
"linktitle": "Contrôler les ressources externes à l'aide des paramètres du classeur"
"second_title": "API de traitement Excel Aspose.Cells .NET"
"title": "Contrôler les ressources externes à l'aide des paramètres du classeur"
"url": "/fr/net/workbook-settings/control-external-resources/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Contrôler les ressources externes à l'aide des paramètres du classeur

## Introduction
Dans le domaine de la manipulation et de la présentation des données, gérer efficacement les ressources externes peut changer la donne. Si vous travaillez avec des fichiers Excel et souhaitez gérer vos ressources externes de manière fluide grâce à Aspose.Cells pour .NET, vous êtes au bon endroit ! Dans cet article, nous approfondirons le contrôle des ressources externes dans les classeurs Excel. À la fin de ce guide, vous serez capable de mettre en œuvre une solution personnalisée pour charger facilement des images et des données depuis des sources externes.
## Prérequis
Avant d'entrer dans le vif du sujet, voici quelques prérequis. Assurez-vous de :
1. Avoir Visual Studio : vous aurez besoin d'un IDE pour développer et tester vos applications .NET. Visual Studio est l'option la plus recommandée en raison de sa prise en charge étendue et de sa simplicité d'utilisation.
2. Téléchargez Aspose.Cells pour .NET : si vous ne l'avez pas déjà fait, récupérez la bibliothèque Aspose.Cells à partir du [lien de téléchargement](https://releases.aspose.com/cells/net/). 
3. Compréhension de base de C# : la familiarité avec les concepts de C# et du framework .NET rendra le processus plus fluide pour vous.
4. Configurez votre environnement : assurez-vous que votre projet référence la bibliothèque Aspose.Cells. Vous pouvez le faire via le gestionnaire de packages NuGet dans Visual Studio.
5. Exemples de fichiers : Préparez un exemple de fichier Excel incluant une ressource externe, comme une image liée. Ce fichier illustrera les fonctionnalités présentées.
Une fois que vous avez configuré ces éléments, vous êtes prêt à vous lancer dans le contrôle des ressources externes avec Aspose.Cells.
## Importer des packages
Pour commencer à coder, vous devrez importer les packages nécessaires dans votre fichier C#. Voici ce dont vous avez besoin :
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.IO;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;
```
Ces espaces de noms donnent accès aux fonctionnalités nécessaires à la manipulation de fichiers Excel et à la gestion d'images.
Décomposons-le en étapes gérables pour vous aider à contrôler les ressources externes à l'aide de `Workbook Settings`Nous vous expliquerons comment créer un fournisseur de flux personnalisé, charger un fichier Excel et convertir une feuille de calcul en image. N'hésitez pas à nous suivre !
## Étape 1 : Définir les répertoires source et de sortie
Pour commencer, nous devons spécifier les répertoires où nous lirons nos fichiers et où nous enregistrerons notre sortie. Il est essentiel de définir les chemins corrects pour éviter les erreurs de fichier introuvable.
```csharp
// Répertoire source
static string sourceDir = "Your Document Directory";
// Répertoire de sortie
static string outputDir = "Your Document Directory";
```
Remplacer `"Your Document Directory"` avec le chemin réel où se trouvent vos fichiers.
## Étape 2 : implémenter l'interface IStreamProvider
Ensuite, nous allons créer une classe personnalisée qui implémente le `IStreamProvider` interface. Cette classe gérera la manière dont les ressources externes (comme les images) sont accessibles.
```csharp
class SP : IStreamProvider
{
    public void CloseStream(StreamProviderOptions options)
    {
        // Nettoyez toutes les ressources si nécessaire
    }
    public void InitStream(StreamProviderOptions options)
    {
        // Ouvrir le flux de fichiers de la ressource externe
        FileStream fi = new FileStream(sourceDir + "sampleControlExternalResourcesUsingWorkbookSetting_StreamProvider.png", FileMode.OpenOrCreate, FileAccess.Read);
        options.Stream = fi;
    }
}
```
Dans le `InitStream` méthode, nous ouvrons le fichier qui agit comme notre ressource externe et l'affectons au `Stream` propriété. Cela permet au classeur d'accéder à la ressource lors du rendu.
## Étape 3 : Charger le fichier Excel
Maintenant que notre fournisseur de flux est prêt, chargeons le classeur Excel qui contient la ressource externe.
```csharp
public static void Run()
{
    // Charger un exemple de fichier Excel
    Workbook wb = new Workbook(sourceDir + "sampleControlExternalResourcesUsingWorkbookSetting_StreamProvider.xlsx");
    
    // Fournissez votre implémentation de IStreamProvider
    wb.Settings.StreamProvider = new SP();
```
Dans cet extrait, nous chargeons notre fichier Excel et attribuons notre personnalisation `StreamProvider` mise en œuvre pour gérer les ressources externes.
## Étape 4 : Accéder à la feuille de travail
Après avoir chargé le classeur, nous pouvons facilement accéder à la feuille de calcul souhaitée. Prenons la première.
```csharp
    // Accéder à la première feuille de calcul
    Worksheet ws = wb.Worksheets[0];
```
C'est simple, n'est-ce pas ? Vous pouvez accéder à n'importe quelle feuille de calcul en spécifiant son index.
## Étape 5 : Configurer les options d’image ou d’impression
Nous allons maintenant définir l'apparence de l'image de sortie. Nous allons configurer des options telles que la présence d'une page par feuille et le type d'image de sortie.
```csharp
    // Spécifiez les options d'image ou d'impression
    ImageOrPrintOptions opts = new ImageOrPrintOptions();
    opts.OnePagePerSheet = true;
    opts.ImageType = Drawing.ImageType.Png;
```
Choisir PNG comme format de sortie garantit que la qualité reste nette et claire !
## Étape 6 : Convertir la feuille de calcul en image
Une fois tout configuré, convertissons la feuille de calcul choisie en fichier image ! C'est la partie la plus intéressante : vous verrez votre feuille Excel transformée en une magnifique image.
```csharp
    // Créer un rendu de feuille en transmettant les paramètres requis
    SheetRender sr = new SheetRender(ws, opts);
    // Convertissez l'intégralité de votre feuille de calcul en image png
    sr.ToImage(0, outputDir + "outputControlExternalResourcesUsingWorkbookSetting_StreamProvider.png");
    
    Console.WriteLine("ControlExternalResourcesUsingWorkbookSetting_StreamProvider executed successfully.");
}
```
Le `ToImage` La fonction effectue le gros du travail : elle convertit la feuille en image. Une fois cette étape terminée, l'image sera enregistrée dans votre répertoire de sortie.
## Conclusion
Et voilà ! Vous maîtrisez désormais le contrôle des ressources externes lorsque vous travaillez avec des fichiers Excel grâce à Aspose.Cells dans .NET. Cela améliore non seulement les capacités de votre application, mais simplifie également la gestion des jeux de données et des présentations. En suivant les étapes indiquées, vous pouvez facilement reproduire et adapter cette fonctionnalité aux besoins spécifiques de votre projet.
## FAQ
### Qu'est-ce qu'Aspose.Cells ?
Aspose.Cells est une bibliothèque puissante conçue pour les développeurs C# et .NET pour créer, manipuler et gérer des fichiers Excel sans avoir besoin d'installer Microsoft Excel.
### Comment puis-je télécharger Aspose.Cells pour .NET ?
Vous pouvez le télécharger à partir du [Site Web d'Aspose](https://releases.aspose.com/cells/net/).
### Existe-t-il un essai gratuit disponible ?
Oui ! Vous pouvez accéder à un essai gratuit d'Aspose.Cells depuis leur [page de sortie](https://releases.aspose.com/).
### Quels types de fichiers Aspose.Cells prend-il en charge ?
Aspose.Cells prend en charge divers formats Excel, notamment XLS, XLSX, CSV, etc.
### Où puis-je trouver du support pour Aspose.Cells ?
Vous pouvez visiter le forum d'assistance Aspose à l'adresse [Forum Aspose](https://forum.aspose.com/c/cells/9) pour obtenir de l'aide.


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}