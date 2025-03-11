---
title: Copier le stockage du concepteur de formulaires utilisateur VBAMacro dans le classeur à l'aide d'Aspose.Cells
linktitle: Copier le stockage du concepteur de formulaires utilisateur VBAMacro dans le classeur à l'aide d'Aspose.Cells
second_title: API de traitement Excel Aspose.Cells .NET
description: Apprenez à copier efficacement le concepteur de formulaires utilisateur de macros VBA dans Aspose.Cells pour .NET avec notre didacticiel complet étape par étape ! Libérez le potentiel d'Excel.
weight: 11
url: /fr/net/workbook-vba-project/copy-vbamacro-user-form-designer/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Copier le stockage du concepteur de formulaires utilisateur VBAMacro dans le classeur à l'aide d'Aspose.Cells

## Introduction
Bienvenue ! Si vous cherchez à améliorer votre expérience Excel avec les macros VBA et les formulaires utilisateur, vous êtes au bon endroit ! Dans ce guide, nous vous expliquons comment copier de manière transparente un concepteur de macros VBA UserForm d'un classeur à un autre à l'aide d'Aspose.Cells pour .NET. Que vous soyez un développeur chevronné ou que vous débutiez, nous vous guiderons à travers chaque étape cruciale. Considérez ceci comme votre manuel pour maîtriser l'art de gérer les fichiers Excel par programmation. Prêt à vous lancer ? C'est parti !
## Prérequis
Avant de passer aux choses sérieuses du codage, assurons-nous que vous disposez de tout ce dont vous avez besoin :
1. Environnement de développement C# : vous devez disposer d'un environnement de travail prêt pour le développement C#. Visual Studio est fortement recommandé.
2.  Bibliothèque Aspose.Cells pour .NET : assurez-vous que la bibliothèque Aspose.Cells est intégrée à votre projet. Vous pouvez facilement[téléchargez-le ici](https://releases.aspose.com/cells/net/).
3. Connaissances de base de VBA et des macros Excel : une bonne compréhension de VBA et du fonctionnement des macros Excel vous aidera à parcourir ce didacticiel en toute simplicité.
4. Un fichier Excel avec un formulaire utilisateur : Pour expérimenter, créez ou obtenez un classeur Excel contenant un formulaire utilisateur, de préférence avec des macros activées (comme`.xlsm` fichiers).
## Paquets d'importation
Dans votre projet C#, vous devrez importer certains espaces de noms en haut de votre fichier pour utiliser les fonctionnalités d'Aspose.Cells. Voici comment procéder :
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Vba;
```
L'inclusion de ces espaces de noms vous permet d'accéder à tous les outils puissants intégrés dans la bibliothèque Aspose.Cells. 
Maintenant que nous avons couvert nos prérequis et nos packages, il est temps de passer à la partie amusante : le codage ! Décomposons-le étape par étape.
## Étape 1 : définissez vos répertoires source et de sortie
Tout d’abord, vous devez déterminer où se trouvent vos fichiers :
```csharp
// Répertoire des sources
string sourceDir = "Your Document Directory";
// Répertoire de sortie
string outputDir = "Your Document Directory";
```
 Ici, remplacez`"Your Document Directory"` avec le chemin réel où vos fichiers sont stockés. C'est à partir de là que notre classeur source (avec l'UserForm) sera récupéré et où le nouveau classeur sera enregistré.
## Étape 2 : créer un classeur cible vide
Ensuite, créons notre classeur cible dans lequel nous copierons notre formulaire utilisateur et nos macros :
```csharp
// Créer un classeur cible vide
Workbook target = new Workbook();
```
Cette ligne de code initialise un nouveau classeur vide que nous allons remplir avec des données. Considérez-le comme une toile vierge pour votre chef-d'œuvre !
## Étape 3 : chargez votre classeur modèle
Nous devons charger le classeur qui contient votre formulaire utilisateur et vos macros :
```csharp
// Charger le fichier Excel contenant le formulaire utilisateur VBA-Macro Designer
Workbook templateFile = new Workbook(sourceDir + "sampleDesignerForm.xlsm");
```
 Assurez-vous de changer`"sampleDesignerForm.xlsm"` au nom de votre fichier actuel. Ce classeur est comme votre livre de recettes : c'est de là que nous tirerons nos ingrédients !
## Étape 4 : Copier les feuilles de calcul dans le classeur cible
Maintenant, commençons à copier les feuilles de calcul de notre modèle vers le classeur cible :
```csharp
// Copier toutes les feuilles de calcul du modèle dans le classeur cible
foreach (Worksheet ws in templateFile.Worksheets)
{
    if (ws.Type == SheetType.Worksheet)
    {
        Worksheet s = target.Worksheets.Add(ws.Name);
        s.Copy(ws);
        // Placez le message dans la cellule A2 de la feuille de calcul cible
        s.Cells["A2"].PutValue("VBA Macro and User Form copied from template to target.");
    }
}
```
Dans cette étape, nous parcourons chaque feuille de calcul du modèle et les copions dans notre classeur cible. Si vous y réfléchissez, c'est comme transférer vos meilleures recettes d'un livre de cuisine à un autre !
## Étape 5 : Copier les macros VBA à partir du modèle
Ensuite, nous allons copier les macros VBA, y compris les modules UserForm Designer, dans notre nouveau classeur :
```csharp
// Copier l'UserForm du concepteur de macros VBA du modèle vers la cible
foreach (VbaModule vbaItem in templateFile.VbaProject.Modules)
{
    if (vbaItem.Name == "ThisWorkbook")
    {
        // Copier le code du module ThisWorkbook
        target.VbaProject.Modules["ThisWorkbook"].Codes = vbaItem.Codes;
    }
    else
    {
        // Copier le code et les données d’autres modules
        System.Diagnostics.Debug.Print(vbaItem.Name);
        int vbaMod = 0;
        Worksheet sheet = target.Worksheets.GetSheetByCodeName(vbaItem.Name);
        if (sheet == null)
        {
            vbaMod = target.VbaProject.Modules.Add(vbaItem.Type, vbaItem.Name);
        }
        else
        {
            vbaMod = target.VbaProject.Modules.Add(sheet);
        }
        target.VbaProject.Modules[vbaMod].Codes = vbaItem.Codes;
        if ((vbaItem.Type == VbaModuleType.Designer))
        {
            // Récupérer les données du formulaire utilisateur, c'est-à-dire le stockage du concepteur
            byte[] designerStorage = templateFile.VbaProject.Modules.GetDesignerStorage(vbaItem.Name);
            // Ajoutez le stockage du concepteur au projet Vba cible
            target.VbaProject.Modules.AddDesignerStorage(vbaItem.Name, designerStorage);
        }
    }
}
```
Ce gros morceau de code gère la vérification de chaque module VBA dans le fichier modèle. Nous copions la conception de l'UserForm et ses codes associés. C'est comme s'assurer que vous obtenez non seulement la célèbre recette de tarte de grand-mère, mais aussi ses techniques de cuisson exactes !
## Étape 6 : Enregistrer le classeur cible
Après avoir réalisé toutes nos copies, il est temps de sauvegarder notre dur labeur :
```csharp
// Enregistrer le classeur cible
target.Save(outputDir + "outputDesignerForm.xlsm", SaveFormat.Xlsm);
```
Assurez-vous de modifier le nom du fichier de sortie selon vos besoins. Une fois que vous l'avez enregistré, vous créez en fait votre propre version personnalisée du classeur, remplie de macros et de formulaires utilisateur. N'est-ce pas passionnant ?
## Étape 7 : Confirmer le succès
Enfin, imprimons un message de réussite sur la console :
```csharp
Console.WriteLine("CopyVBAMacroUserFormDesignerStorageToWorkbook executed successfully.\r\n");
```
Cette petite ligne vous rassure sur le fait que votre processus s'est bien déroulé. C'est la cerise sur le gâteau de votre sundae de codage !
## Conclusion
Félicitations ! Vous avez terminé le guide étape par étape pour copier un concepteur de formulaire utilisateur de macro VBA d'un classeur à un autre à l'aide d'Aspose.Cells pour .NET. Cela peut sembler un peu difficile au début, mais avec de la pratique, vous gérerez les manipulations de classeur comme un pro. N'oubliez pas que le codage est une question de pratique, alors n'hésitez pas à essayer différentes choses dans vos fichiers Excel. Si vous avez des questions ou rencontrez des problèmes, n'hésitez pas à consulter les forums ou la documentation Aspose pour obtenir de l'aide !
## FAQ
### Quelles versions d'Excel sont prises en charge par Aspose.Cells ?
Aspose.Cells prend en charge une large gamme de formats Excel, notamment XLSX, XLSM, CSV, etc.
### Puis-je utiliser Aspose.Cells gratuitement ?
 Oui ! Vous pouvez commencer par un essai gratuit, qui vous permet d'évaluer la bibliothèque :[Essai gratuit](https://releases.aspose.com/).
### Ai-je besoin de Visual Studio pour exécuter ce code ?
Bien qu'il soit fortement recommandé en raison de ses fonctionnalités conviviales, n'importe quel IDE C# fera l'affaire à condition qu'il prenne en charge le développement .NET.
### Où puis-je trouver plus d’exemples et de documentation ?
 Vous pouvez explorer le[Documentation sur Aspose.Cells](https://reference.aspose.com/cells/net/) pour plus d'exemples et d'explications détaillées.
### Comment résoudre les problèmes lors de l'utilisation d'Aspose.Cells ?
 Vous devriez visiter le[Forum d'assistance Aspose](https://forum.aspose.com/c/cells/9) pour l'aide de la communauté et du personnel de soutien d'Aspose.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
