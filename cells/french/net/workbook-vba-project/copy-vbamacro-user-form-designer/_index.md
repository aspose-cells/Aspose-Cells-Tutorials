---
"description": "Apprenez à copier efficacement le concepteur de formulaires utilisateur de macros VBA dans Aspose.Cells pour .NET grâce à notre tutoriel complet étape par étape ! Libérez le potentiel d'Excel."
"linktitle": "Copier le stockage du concepteur de formulaires utilisateur VBAMacro dans un classeur à l'aide d'Aspose.Cells"
"second_title": "API de traitement Excel Aspose.Cells .NET"
"title": "Copier le stockage du concepteur de formulaires utilisateur VBAMacro dans un classeur à l'aide d'Aspose.Cells"
"url": "/fr/net/workbook-vba-project/copy-vbamacro-user-form-designer/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Copier le stockage du concepteur de formulaires utilisateur VBAMacro dans un classeur à l'aide d'Aspose.Cells

## Introduction
Bienvenue ! Si vous souhaitez améliorer votre expérience Excel avec les macros VBA et les formulaires utilisateur, vous êtes au bon endroit ! Dans ce guide, nous vous expliquons comment copier facilement un concepteur de macros VBA UserForm d'un classeur à un autre grâce à Aspose.Cells pour .NET. Que vous soyez un développeur expérimenté ou débutant, nous vous guiderons à travers chaque étape cruciale. Considérez ceci comme votre guide pour maîtriser l'art de la gestion programmatique des fichiers Excel. Prêt à vous lancer ? C'est parti !
## Prérequis
Avant de passer aux choses sérieuses du codage, assurons-nous que vous disposez de tout ce dont vous avez besoin :
1. Environnement de développement C# : vous devez disposer d'un environnement de travail adapté au développement C#. Visual Studio est fortement recommandé.
2. Bibliothèque Aspose.Cells pour .NET : Assurez-vous d'avoir intégré la bibliothèque Aspose.Cells à votre projet. Vous pouvez facilement [téléchargez-le ici](https://releases.aspose.com/cells/net/).
3. Connaissances de base de VBA et des macros Excel : une bonne compréhension de VBA et du fonctionnement des macros Excel vous aidera à naviguer facilement dans ce didacticiel.
4. Un fichier Excel avec un formulaire utilisateur : Pour expérimenter, créez ou obtenez un classeur Excel contenant un formulaire utilisateur, de préférence avec des macros activées (comme `.xlsm` fichiers).
## Importer des packages
Dans votre projet C#, vous devrez importer certains espaces de noms en haut de votre fichier pour utiliser les fonctionnalités d'Aspose.Cells. Voici comment procéder :
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Vba;
```
L'inclusion de ces espaces de noms vous permet d'accéder à tous les outils puissants intégrés dans la bibliothèque Aspose.Cells. 
Maintenant que nous avons couvert nos prérequis et nos packages, il est temps de passer à la partie amusante : le codage ! Décomposons-le étape par étape.
## Étape 1 : Définissez vos répertoires source et de sortie
Tout d’abord, vous devez déterminer où se trouvent vos fichiers :
```csharp
// Répertoire source
string sourceDir = "Your Document Directory";
// Répertoire de sortie
string outputDir = "Your Document Directory";
```
Ici, remplacez `"Your Document Directory"` avec le chemin d'accès réel où sont stockés vos fichiers. C'est là que notre classeur source (avec l'UserForm) sera récupéré et que le nouveau classeur sera enregistré.
## Étape 2 : créer un classeur cible vide
Ensuite, créons notre classeur cible dans lequel nous copierons notre formulaire utilisateur et nos macros :
```csharp
// Créer un classeur cible vide
Workbook target = new Workbook();
```
Cette ligne de code initialise un nouveau classeur vide que nous allons remplir de données. Imaginez-le comme une toile vierge pour votre chef-d'œuvre !
## Étape 3 : Chargez votre classeur modèle
Nous devons charger le classeur qui contient votre formulaire utilisateur et vos macros :
```csharp
// Charger le fichier Excel contenant le formulaire utilisateur VBA-Macro Designer
Workbook templateFile = new Workbook(sourceDir + "sampleDesignerForm.xlsm");
```
Assurez-vous de changer `"sampleDesignerForm.xlsm"` au nom de votre fichier actuel. Ce classeur est comme votre livre de recettes : c'est de là que nous tirerons nos ingrédients !
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
Dans cette étape, nous parcourons chaque feuille de calcul du modèle et les copions dans notre classeur cible. En y réfléchissant, c'est comme transférer vos meilleures recettes d'un livre de cuisine à un autre !
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
        // Copier le code et les données d'autres modules
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
            // Ajoutez le stockage du concepteur au projet VBA cible
            target.VbaProject.Modules.AddDesignerStorage(vbaItem.Name, designerStorage);
        }
    }
}
```
Ce gros morceau de code vérifie chaque module VBA du fichier modèle. Nous copions la conception de l'UserForm et ses codes associés. C'est comme s'assurer que vous obtenez non seulement la célèbre recette de tarte de grand-mère, mais aussi ses techniques de pâtisserie exactes !
## Étape 6 : Enregistrer le classeur cible
Après avoir réalisé toutes nos copies, il est temps de sauvegarder notre dur labeur :
```csharp
// Enregistrer le classeur cible
target.Save(outputDir + "outputDesignerForm.xlsm", SaveFormat.Xlsm);
```
N'oubliez pas de modifier le nom du fichier de sortie si nécessaire. Une fois enregistré, vous créez votre propre version personnalisée du classeur, regorgeant de macros et de formulaires utilisateur. Incroyable, non ?
## Étape 7 : Confirmer le succès
Enfin, imprimons un message de réussite sur la console :
```csharp
Console.WriteLine("CopyVBAMacroUserFormDesignerStorageToWorkbook executed successfully.\r\n");
```
Cette petite ligne vous rassure sur le bon déroulement de votre processus. C'est la cerise sur le gâteau de votre réussite en codage !
## Conclusion
Félicitations ! Vous avez terminé le guide étape par étape pour copier un concepteur de formulaires utilisateur VBA de macros d'un classeur à un autre avec Aspose.Cells pour .NET. Cela peut paraître un peu complexe au début, mais avec de la pratique, vous maîtriserez les manipulations de classeurs comme un pro. N'oubliez pas que le codage est une question de pratique ; n'hésitez donc pas à essayer différentes méthodes dans vos fichiers Excel. Si vous avez des questions ou rencontrez des problèmes, n'hésitez pas à consulter les forums Aspose ou la documentation pour obtenir de l'aide !
## FAQ
### Quelles versions d'Excel Aspose.Cells prend-il en charge ?
Aspose.Cells prend en charge une large gamme de formats Excel, notamment XLSX, XLSM, CSV, etc.
### Puis-je utiliser Aspose.Cells gratuitement ?
Oui ! Vous pouvez commencer par un essai gratuit, qui vous permettra d'évaluer la bibliothèque : [Essai gratuit](https://releases.aspose.com/).
### Ai-je besoin de Visual Studio pour exécuter ce code ?
Bien qu'il soit fortement recommandé en raison de ses fonctionnalités conviviales, n'importe quel IDE C# fera l'affaire tant qu'il prend en charge le développement .NET.
### Où puis-je trouver plus d'exemples et de documentation ?
Vous pouvez explorer le [Documentation d'Aspose.Cells](https://reference.aspose.com/cells/net/) pour plus d'exemples et d'explications approfondies.
### Comment résoudre les problèmes lors de l’utilisation d’Aspose.Cells ?
Vous devriez visiter le [Forum d'assistance Aspose](https://forum.aspose.com/c/cells/9) pour l'aide de la communauté et du personnel de soutien d'Aspose.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}