---
title: Protégez les lignes de la feuille de calcul à l'aide d'Aspose.Cells
linktitle: Protégez les lignes de la feuille de calcul à l'aide d'Aspose.Cells
second_title: API de traitement Excel Aspose.Cells .NET
description: Découvrez comment protéger les lignes d'une feuille de calcul Excel à l'aide d'Aspose.Cells pour .NET. Sécurisez vos données avec une protection au niveau des lignes et évitez les modifications accidentelles.
weight: 18
url: /fr/net/worksheet-security/protect-rows/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Protégez les lignes de la feuille de calcul à l'aide d'Aspose.Cells

## Introduction
Travailler avec des fichiers Excel par programmation est souvent une tâche qui nécessite non seulement la manipulation des données, mais également leur protection. Que vous ayez besoin de protéger des données sensibles ou d'empêcher toute modification accidentelle, la protection des lignes d'une feuille de calcul peut être une étape cruciale. Dans ce didacticiel, nous allons découvrir comment protéger des lignes spécifiques dans une feuille de calcul Excel à l'aide d'Aspose.Cells pour .NET. Nous passerons en revue toutes les étapes nécessaires, de la préparation de votre environnement à la mise en œuvre des fonctionnalités de protection de manière simple et facile à suivre.
## Prérequis
Avant de pouvoir commencer à protéger les lignes d'une feuille de calcul, vous devez mettre en place quelques éléments :
1.  Aspose.Cells pour .NET : assurez-vous que Aspose.Cells pour .NET est installé sur votre machine de développement. Si vous ne l'avez pas encore fait, vous pouvez facilement le télécharger à partir du[Page de téléchargement des cellules Aspose](https://releases.aspose.com/cells/net/).
2. Visual Studio ou tout autre IDE .NET : pour implémenter la solution, vous devez disposer d'un environnement de développement configuré. Visual Studio est une excellente option, mais tout IDE compatible .NET fonctionnera.
3. Connaissances de base en C# : comprendre les bases de la programmation C# vous aidera à suivre le didacticiel et à modifier l'exemple de code en fonction de vos besoins.
4.  Documentation de l'API Aspose.Cells : familiarisez-vous avec l'[Documentation d'Aspose.Cells pour .NET](https://reference.aspose.com/cells/net/) pour obtenir un aperçu de la structure de la classe et des méthodes utilisées dans la bibliothèque.
Si vous disposez de tous les prérequis, nous pouvons passer directement à la mise en œuvre.
## Paquets d'importation
Pour commencer, vous devez importer les packages requis. Ces bibliothèques sont essentielles pour interagir avec les fichiers Excel dans votre projet C#.
```csharp
using System.IO;
using Aspose.Cells;
```
Une fois que vous avez importé les packages nécessaires, vous pouvez commencer à coder. 
Décomposons maintenant le processus en étapes plus petites pour que vous puissiez le suivre très facilement. Chaque étape se concentrera sur une partie spécifique de la mise en œuvre, vous permettant ainsi de la comprendre et de l'appliquer rapidement. 
## Étape 1 : Créer un nouveau classeur et une nouvelle feuille de calcul
Avant de pouvoir appliquer des paramètres de protection, vous devez créer un nouveau classeur et sélectionner la feuille de calcul avec laquelle vous souhaitez travailler. Ce sera votre document de travail.
```csharp
// Le chemin vers le répertoire des documents.
string dataDir = "Your Document Directory";
// Créez un répertoire s'il n'est pas déjà présent.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
	System.IO.Directory.CreateDirectory(dataDir);
// Créer un nouveau classeur.
Workbook wb = new Workbook();
// Créez un objet de feuille de calcul et obtenez la première feuille.
Worksheet sheet = wb.Worksheets[0];
```
Dans cet exemple, nous créons un nouveau classeur avec une seule feuille de calcul (qui est la configuration par défaut lorsque vous créez un nouveau classeur à l'aide d'Aspose.Cells). Nous récupérons ensuite la première feuille de calcul du classeur, qui sera la cible de notre protection de ligne.
## Étape 2 : définir les objets Style et StyleFlag
L'étape suivante consiste à définir les objets style et indicateur de style. Ces objets vous permettent de modifier les propriétés de la cellule, par exemple si elle est verrouillée ou déverrouillée.
```csharp
// Définir l'objet de style.
Style style;
// Définissez l'objet styleflag.
StyleFlag flag;
```
Vous utiliserez ces objets dans les étapes ultérieures pour personnaliser les propriétés de la cellule et les appliquer à votre feuille de calcul.
## Étape 3 : déverrouiller toutes les colonnes de la feuille de calcul
Par défaut, toutes les cellules d'une feuille de calcul Excel sont verrouillées. Cependant, lorsque vous protégez une feuille de calcul, le statut verrouillé est appliqué. Pour garantir que seules des lignes ou des cellules spécifiques sont protégées, vous pouvez d'abord déverrouiller toutes les colonnes. Cette étape est essentielle si vous souhaitez protéger uniquement certaines lignes.
```csharp
// Parcourez toutes les colonnes de la feuille de calcul et déverrouillez-les.
for (int i = 0; i <= 255; i++)
{
    style = sheet.Cells.Columns[(byte)i].Style;
    style.IsLocked = false;
    flag = new StyleFlag();
    flag.Locked = true;
    sheet.Cells.Columns[(byte)i].ApplyStyle(style, flag);
}
```
 Dans ce code, nous parcourons les 256 colonnes de la feuille de calcul (les feuilles de calcul Excel ont un maximum de 256 colonnes, indexées de 0 à 255) et définissons leurs`IsLocked` propriété à`false`Cette action garantit que toutes les colonnes sont déverrouillées, mais nous verrouillerons toujours des lignes spécifiques plus tard.
## Étape 4 : Verrouillez la première rangée
Une fois les colonnes déverrouillées, l'étape suivante consiste à verrouiller les lignes spécifiques que vous souhaitez protéger. Dans cet exemple, nous allons verrouiller la première ligne. Cela garantit que les utilisateurs ne peuvent pas la modifier alors que les autres lignes restent déverrouillées.
```csharp
//Obtenez le style de la première rangée.
style = sheet.Cells.Rows[0].Style;
// Verrouille-le.
style.IsLocked = true;
//Instanciez le drapeau.
flag = new StyleFlag();
// Définissez le paramètre de verrouillage.
flag.Locked = true;
// Appliquez le style à la première ligne.
sheet.Cells.ApplyRowStyle(0, style, flag);
```
Ici, nous accédons au style de la première ligne et définissons son`IsLocked` propriété à`true` . Après cela, nous utilisons le`ApplyRowStyle()` méthode pour appliquer le style de verrouillage à la ligne entière. Vous pouvez répéter cette étape pour verrouiller toutes les autres lignes que vous souhaitez protéger.
## Étape 5 : Protégez la feuille
Maintenant que nous avons déverrouillé et verrouillé les lignes nécessaires, il est temps de protéger la feuille de calcul. La protection garantit que personne ne peut modifier les lignes ou les cellules verrouillées à moins de supprimer le mot de passe de protection (si fourni).
```csharp
// Protégez la feuille.
sheet.Protect(ProtectionType.All);
```
 Dans cette étape, nous appliquons une protection à toute la feuille en utilisant`ProtectionType.All`. Ce type de protection signifie que tous les aspects de la feuille, y compris les lignes et les cellules verrouillées, sont protégés. Vous pouvez également personnaliser cette protection en spécifiant différents types de protection si nécessaire.
## Étape 6 : Enregistrer le classeur
Enfin, nous devons enregistrer le classeur après avoir appliqué les styles et la protection nécessaires. Le classeur peut être enregistré dans différents formats, tels qu'Excel 97-2003, Excel 2010, etc.
```csharp
// Enregistrez le fichier Excel.
wb.Save(dataDir + "output.out.xls", SaveFormat.Excel97To2003);
```
Cette ligne de code enregistre le classeur au format Excel 97-2003 avec les modifications appliquées. Vous pouvez modifier le format de fichier selon vos besoins en sélectionnant parmi une variété de`SaveFormat` options.
## Conclusion
Et voilà ! Vous avez appris avec succès à protéger les lignes d'une feuille de calcul à l'aide d'Aspose.Cells pour .NET. En suivant les étapes ci-dessus, vous pouvez déverrouiller ou verrouiller les lignes ou les colonnes selon vos besoins et appliquer une protection pour garantir l'intégrité de vos données.
## FAQ
### Comment puis-je protéger plusieurs lignes à la fois ?  
 Vous pouvez parcourir plusieurs lignes et appliquer le style de verrouillage à chacune d'elles individuellement. Il suffit de remplacer`0` avec l'index de ligne que vous souhaitez verrouiller.
### Puis-je définir un mot de passe pour la protection de la feuille ?  
 Oui ! Vous pouvez transmettre un mot de passe à la`sheet.Protect()` méthode pour renforcer la protection par mot de passe.
### Puis-je déverrouiller des cellules au lieu de colonnes entières ?  
Oui ! Au lieu de déverrouiller les colonnes, vous pouvez déverrouiller les cellules individuelles en modifiant leurs propriétés de style.
### Que se passe-t-il si j’essaie de modifier une ligne protégée ?  
Lorsqu'une ligne est protégée, Excel empêche toute modification des cellules verrouillées, sauf si vous déprotégez la feuille.
### Puis-je protéger des plages spécifiques d’affilée ?  
 Oui ! Vous pouvez verrouiller des plages individuelles dans une rangée en définissant le`IsLocked` propriété pour des cellules spécifiques dans la plage.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
