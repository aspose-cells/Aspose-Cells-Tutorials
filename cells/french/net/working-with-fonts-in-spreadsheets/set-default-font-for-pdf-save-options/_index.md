---
title: Définir la police par défaut pour les options d'enregistrement PDF
linktitle: Définir la police par défaut pour les options d'enregistrement PDF
second_title: API de traitement Excel Aspose.Cells .NET
description: Découvrez comment définir les polices par défaut pour les options d'enregistrement PDF à l'aide d'Aspose.Cells pour .NET, garantissant ainsi que vos documents sont parfaits à chaque fois.
weight: 11
url: /fr/net/working-with-fonts-in-spreadsheets/set-default-font-for-pdf-save-options/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Définir la police par défaut pour les options d'enregistrement PDF

## Introduction
Lorsque vous générez des rapports, des factures ou tout autre document au format PDF, il est primordial de veiller à ce que votre contenu soit parfait. Les polices jouent un rôle essentiel dans le maintien de l'attrait visuel et de la lisibilité de vos documents. Cependant, que se passe-t-il lorsque la police que vous avez utilisée dans votre fichier Excel n'est pas disponible sur le système sur lequel vous générez votre PDF ? C'est là qu'Aspose.Cells pour .NET s'avère utile. Cette puissante bibliothèque vous permet de définir des polices par défaut pour vos options d'enregistrement PDF, garantissant ainsi que vos documents ont un aspect professionnel et cohérent, quel que soit l'endroit où ils sont ouverts.
## Prérequis
Avant de commencer, assurez-vous de disposer des éléments suivants :
1. Visual Studio : vous aurez besoin d’un environnement de développement comme Visual Studio pour écrire et exécuter votre code.
2.  Aspose.Cells pour .NET : vous pouvez télécharger la dernière version à partir de[ce lien](https://releases.aspose.com/cells/net/). Vous pouvez également l’installer via le gestionnaire de packages NuGet dans Visual Studio.
3. Connaissances de base de C# : comprendre les bases de C# vous aidera à suivre les exemples de code.
4. Exemple de fichier Excel : préparez un exemple de fichier Excel pour le test. Vous pouvez en créer un avec différentes polices et styles pour voir comment Aspose.Cells gère les polices manquantes.
## Paquets d'importation
Avant de pouvoir utiliser Aspose.Cells dans votre projet, vous devez importer les packages nécessaires. Voici comment procéder :
1. Ouvrez votre projet : lancez Visual Studio et ouvrez votre projet existant ou créez-en un nouveau.
2. Ajouter des références : cliquez avec le bouton droit sur votre projet dans l’Explorateur de solutions et sélectionnez « Gérer les packages NuGet ».
3. Installer Aspose.Cells : Recherchez « Aspose.Cells » et cliquez sur le bouton « Installer ».
4. Ajouter des directives d'utilisation : en haut de votre fichier C#, incluez les espaces de noms suivants :
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;
```
## Étape 1 : Configurez vos répertoires
Avant de travailler avec des fichiers, il est important de définir les répertoires source et de sortie. Cela facilitera la localisation de votre fichier Excel d'entrée et l'enregistrement des fichiers de sortie générés.
```csharp
// Répertoire des sources
string sourceDir = "Your Document Directory";
// Répertoire de sortie
string outputDir = "Your Document Directory";
```
 Remplacer`"Your Document Directory"` avec le chemin réel vers vos répertoires.
## Étape 2 : Ouvrir le fichier Excel
 Maintenant que nos répertoires sont configurés, ouvrons le fichier Excel avec lequel vous souhaitez travailler.`Workbook` la classe dans Aspose.Cells est utilisée pour charger le document Excel.
```csharp
// Ouvrir un fichier Excel
Workbook workbook = new Workbook(sourceDir + "sampleSetDefaultFontPropertyOfPdfSaveOptionsAndImageOrPrintOptions.xlsx");
```
Assurez-vous de remplacer le nom de fichier par votre nom de fichier réel.
## Étape 3 : Configurer les options de rendu d’image
Ensuite, nous devons configurer les options de rendu pour convertir notre feuille Excel en format image. Nous allons créer une instance de`ImageOrPrintOptions`, spécifiant le type d'image et la police par défaut.
```csharp
// Rendu au format de fichier PNG
ImageOrPrintOptions imgOpt = new ImageOrPrintOptions();
imgOpt.ImageType = Drawing.ImageType.Png;
imgOpt.CheckWorkbookDefaultFont = false;
imgOpt.DefaultFont = "Times New Roman";
```
 Dans cet extrait de code, nous définissons le`CheckWorkbookDefaultFont` propriété à`false`, ce qui signifie que si des polices manquent, la police par défaut spécifiée (« Times New Roman ») sera utilisée à la place.
## Étape 4 : Rendre la feuille sous forme d'image
 Maintenant, rendons la première feuille du classeur sous forme d'image PNG. Nous utiliserons le`SheetRender` classe pour y parvenir.
```csharp
// Rendre la première feuille de calcul en image
SheetRender sr = new SheetRender(workbook.Worksheets[0], imgOpt);
sr.ToImage(0, outputDir + "out1_imagePNG.png");
```
## Étape 5 : modifier le type d'image et effectuer le rendu au format TIFF
 Si vous souhaitez restituer la même feuille dans un format d'image différent, comme TIFF, vous pouvez simplement modifier le`ImageType` propriété et répétez le processus de rendu.
```csharp
// Définir sur le format TIFF
imgOpt.ImageType = Drawing.ImageType.Tiff;
WorkbookRender wr = new WorkbookRender(workbook, imgOpt);
wr.ToImage(outputDir + "out1_imageTIFF.tiff");
```
## Étape 6 : Configurer les options d’enregistrement PDF
 Ensuite, configurons les options d'enregistrement PDF. Nous allons créer une instance de`PdfSaveOptions`définissez la police par défaut et spécifiez que nous voulons vérifier les polices manquantes.
```csharp
// Configurer les options d'enregistrement PDF
PdfSaveOptions saveOptions = new PdfSaveOptions();
saveOptions.DefaultFont = "Times New Roman";
saveOptions.CheckWorkbookDefaultFont = false;
```
## Étape 7 : Enregistrer le classeur au format PDF
Une fois les options d’enregistrement configurées, il est temps d’enregistrer notre classeur Excel sous forme de fichier PDF. 
```csharp
// Enregistrer le classeur au format PDF
workbook.Save(outputDir + "out1_pdf.pdf", saveOptions);
```
## Étape 8 : Confirmer l'exécution
Enfin, il est recommandé d'informer l'utilisateur que le processus s'est terminé avec succès. Vous pouvez y parvenir en utilisant un simple message de console.
```csharp
Console.WriteLine("SetDefaultFontPropertyOfPdfSaveOptionsAndImageOrPrintOptions executed successfully.\r\n");
```
## Conclusion
Aspose.Cells offre une méthode flexible et robuste pour gérer les manipulations de fichiers Excel, ce qui permet aux développeurs de créer plus facilement des documents visuellement attrayants qui conservent leur mise en forme. Que vous travailliez sur des rapports, des documents financiers ou toute autre forme de présentation de données, le contrôle du rendu des polices peut améliorer considérablement la qualité de votre sortie.
## FAQ
### Qu'est-ce qu'Aspose.Cells ?
Aspose.Cells est une puissante bibliothèque .NET qui permet aux développeurs de manipuler des fichiers Excel sans avoir besoin d'installer Microsoft Excel. Elle prend en charge divers formats de fichiers et offre de riches fonctionnalités pour travailler avec des feuilles de calcul.
### Comment puis-je définir une police par défaut pour mes fichiers Excel ?
 Vous pouvez définir une police par défaut à l'aide de la`PdfSaveOptions` class et spécifiez le nom de la police souhaitée. Cela garantit que même si une police est manquante, votre document utilisera la police par défaut que vous avez spécifiée.
### Puis-je convertir des fichiers Excel vers d’autres formats que PDF ?
Absolument ! Aspose.Cells vous permet de convertir des fichiers Excel en différents formats, notamment des images (PNG, TIFF), HTML, CSV, etc.
### L'utilisation d'Aspose.Cells est-elle gratuite ?
Aspose.Cells est un produit commercial, mais vous pouvez l'essayer gratuitement avec une version d'essai limitée. Pour bénéficier de toutes les fonctionnalités, vous devrez acheter une licence.
### Où puis-je trouver du support pour Aspose.Cells ?
 Vous pouvez trouver de l'aide pour Aspose.Cells en visitant le[Forum Aspose](https://forum.aspose.com/c/cells/9), où vous pouvez poser des questions et partager des idées avec d'autres utilisateurs et développeurs.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
