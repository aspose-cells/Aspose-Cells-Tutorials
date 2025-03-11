---
title: Remplacer la balise par du texte dans la zone de texte dans Excel
linktitle: Remplacer la balise par du texte dans la zone de texte dans Excel
second_title: API de traitement Excel Aspose.Cells .NET
description: Remplacez facilement le texte des zones de texte de vos feuilles Excel à l'aide d'Aspose.Cells pour .NET. Un guide étape par étape pour l'automatisation d'Excel.
weight: 11
url: /fr/net/excel-shape-text-modifications/replace-tag-text-textbox-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Remplacer la balise par du texte dans la zone de texte dans Excel

## Introduction
Dans cet article, nous allons nous plonger dans une tâche spécifique : remplacer des balises par du texte dans des zones de texte dans une feuille Excel à l'aide d'Aspose.Cells. Nous vous guiderons tout au long du processus, étape par étape, en veillant à ce que vous saisissiez tous les détails. À la fin de ce didacticiel, vous améliorerez non seulement votre compréhension d'Aspose.Cells, mais vous rationaliserez également vos tâches liées à Excel !
## Prérequis
Avant de pouvoir commencer, vous aurez besoin de quelques éléments prêts :
1. Visual Studio : assurez-vous d'avoir installé Visual Studio. Il s'agit d'un IDE flexible qui simplifie le codage en C#.
2.  Bibliothèque Aspose.Cells : si vous ne l'avez pas encore fait, téléchargez la bibliothèque Aspose.Cells pour .NET à partir du[page](https://releases.aspose.com/cells/net/)Vous pouvez également obtenir une version d'essai gratuite pour découvrir ses fonctionnalités.
3. Connaissances de base de C# : une compréhension de base de la programmation C# vous aidera grandement à suivre ce guide facilement.
Maintenant que vous êtes prêt, passons à la partie amusante : écrire le code !
## Paquets d'importation
Tout d'abord, importons les packages nécessaires. Cette étape est cruciale car sans les importations appropriées, votre code ne reconnaîtra pas les classes et les méthodes que nous utiliserons.
## Démarrez votre projet C#
Ouvrez Visual Studio et créez un nouveau projet C#, de préférence une application console, car cela vous permettra de voir facilement le résultat.
## Ajouter une référence Aspose.Cells
- Faites un clic droit sur votre projet dans l’Explorateur de solutions.
- Sélectionnez « Ajouter » > « Référence ».
- Accédez à l’emplacement où vous avez téléchargé la bibliothèque Aspose.Cells et incluez-la dans votre projet.
## Importer les espaces de noms nécessaires
 Une fois que vous avez ajouté la référence, ajoutez ce qui suit`using` directive en haut de votre fichier principal :
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Drawing;
```
Cela vous donne accès aux classes dans l'espace de noms Aspose.Cells.
Maintenant que nous avons configuré notre environnement, passons à la partie intéressante : le codage ! Notre objectif est de trouver des balises spécifiques dans les zones de texte d'un fichier Excel et de les remplacer par le texte fourni.
## Étape 1 : définir le répertoire source et le répertoire de sortie
Tout d’abord, nous devons spécifier où se trouve notre fichier Excel source et où nous souhaitons enregistrer la version modifiée.
```csharp
// Répertoire source et de sortie
string sourceDir = "Your Document Directory"; // Changer votre répertoire
string outputDir = "Your Document Directory"; // Changer votre répertoire
```
## Étape 2 : charger le classeur
C'est ici que nous allons charger notre classeur Excel. Si le fichier n'existe pas, une erreur est générée. Assurez-vous donc que le chemin d'accès au fichier est correct !
```csharp
Workbook wb = new Workbook(sourceDir + "sampleReplaceTagWithText.xlsx");
```
 Ici, nous chargeons un fichier Excel existant appelé`sampleReplaceTagWithText.xlsx`.
## Étape 3 : Définir les balises et le texte de remplacement
Ensuite, nous devons définir les balises que nous recherchons et par quoi nous voulons les remplacer.
```csharp
string tag = "TAG_2$TAG_1";
string replace = "1$ys";
```
 Dans cet exemple, les balises sont divisées à l'aide de`$`Vous pouvez le remplacer par n'importe quel délimiteur de votre choix.
## Étape 4 : Bouclez sur les balises et remplacez
Nous allons créer une boucle pour parcourir chaque balise que nous souhaitons remplacer. C'est ici que la magie opère !
```csharp
for (int i = 0; i < tag.Split('$').Length; i++)
{
    sheetReplace(wb, "<" + tag.Split('$')[i] + ">", replace.Split('$')[i]);
}
```
## Étape 5 : Enregistrer le classeur
Maintenant que nous avons effectué nos remplacements, il est temps d'enregistrer le classeur modifié dans le format souhaité. Voici comment le convertir en PDF.
```csharp
PdfSaveOptions opts = new PdfSaveOptions();
wb.Save(outputDir + "outputReplaceTagWithText.pdf", opts);
```
Vous pouvez également l'enregistrer dans divers autres formats, notamment XLSX.
## Étape 6 : Mettre en œuvre la logique de remplacement
 C'est ici que réside le cœur de notre fonctionnalité.`sheetReplace` la méthode gérera le remplacement réel dans les feuilles de calcul Excel.
```csharp
public static void sheetReplace(Workbook workbook, string sFind, string sReplace)
{
    string finding = sFind;
    foreach (Worksheet sheet in workbook.Worksheets)
    {
        sheet.Replace(finding, sReplace);
        for (int j = 0; j < 3; j++)
        {
            if (sheet.PageSetup.GetHeader(j) != null)
                sheet.PageSetup.SetHeader(j, sheet.PageSetup.GetHeader(j).Replace(finding, sReplace));
                
            if (sheet.PageSetup.GetFooter(j) != null)
                sheet.PageSetup.SetFooter(j, sheet.PageSetup.GetFooter(j).Replace(finding, sReplace));
        }
    }
    foreach (Worksheet sheet in workbook.Worksheets)
    {
        sFind = sFind.Replace("<", "&lt;");
        sFind = sFind.Replace(">", "&gt;");
        foreach (Aspose.Cells.Drawing.TextBox mytextbox in sheet.TextBoxes)
        {
            if (mytextbox.HtmlText != null)
            {
                if (mytextbox.HtmlText.IndexOf(sFind) >= 0)
                {
                    mytextbox.HtmlText = mytextbox.HtmlText.Replace(sFind, sReplace);
                }
            }
        }
    }
}
```
- Tout d’abord, nous parcourons chaque feuille de calcul du classeur.
- Nous remplaçons la balise principale non seulement dans le contenu de la cellule mais également dans les en-têtes et les pieds de page (s'ils existent).
- Enfin, nous vérifions chaque zone de texte de la feuille et remplaçons le texte qu'elle contient, en fonction de la balise que nous recherchons.
## Conclusion
Et voilà ! Vous savez désormais comment remplacer les balises par du texte dans les zones de texte de vos documents Excel à l'aide d'Aspose.Cells pour .NET. Cela peut vous faire gagner du temps, en particulier lorsque vous effectuez des tâches répétitives dans des feuilles de calcul.
## FAQ
### Puis-je remplacer des balises dans plusieurs fichiers Excel à la fois ?
Oui, en parcourant une liste de fichiers, vous pouvez appliquer la même logique à plusieurs fichiers Excel.
### Ai-je besoin d'une licence payante pour utiliser Aspose.Cells ?
 Vous pouvez commencer avec un essai gratuit, mais pour bénéficier de toutes les fonctionnalités, vous devrez acheter une licence.[Options d'achat d'Aspose](https://purchase.aspose.com/buy).
### Puis-je remplacer des images dans des zones de texte à l’aide d’Aspose.Cells ?
Aspose.Cells traite principalement du texte. Cependant, vous pouvez manipuler les images séparément si nécessaire.
### Dans quels formats puis-je enregistrer mon fichier Excel modifié ?
Vous pouvez l'enregistrer dans différents formats, notamment XLSX, PDF, CSV, etc.
### Où puis-je trouver du support pour Aspose.Cells ?
 Vous pouvez trouver de l'aide et poser des questions sur le[Forum Aspose](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
