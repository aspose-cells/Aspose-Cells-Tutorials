---
title: Ajouter un contrôle Spinner à une feuille de calcul dans Excel
linktitle: Ajouter un contrôle Spinner à une feuille de calcul dans Excel
second_title: API de traitement Excel Aspose.Cells .NET
description: Découvrez comment ajouter un contrôle Spinner à une feuille de calcul Excel à l'aide d'Aspose.Cells pour .NET dans ce didacticiel étape par étape.
weight: 23
url: /fr/net/excel-shapes-controls/add-spinner-control-to-worksheet-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ajouter un contrôle Spinner à une feuille de calcul dans Excel

## Introduction
Si vous vous lancez dans l'automatisation d'Excel à l'aide de .NET, vous avez probablement constaté le besoin de contrôles plus interactifs dans vos feuilles de calcul. L'un de ces contrôles est le Spinner, qui permet aux utilisateurs d'incrémenter ou de décrémenter facilement une valeur. Dans ce didacticiel, nous verrons comment ajouter un contrôle Spinner à une feuille de calcul Excel à l'aide d'Aspose.Cells pour .NET. Nous le décomposerons en étapes faciles à comprendre afin que vous puissiez suivre la procédure de manière fluide. 
## Prérequis
Avant de passer au code, assurons-nous que tout est configuré pour une expérience fluide :
1.  Aspose.Cells pour .NET : assurez-vous que vous disposez de la bibliothèque Aspose.Cells. Si vous ne l'avez pas encore installée, vous pouvez récupérer la dernière version à partir du[lien de téléchargement](https://releases.aspose.com/cells/net/).
2. Visual Studio : vous devez disposer d’une installation fonctionnelle de Visual Studio ou de tout autre IDE .NET de votre choix.
3. Connaissances de base de C# : une connaissance de la programmation C# vous aidera à comprendre facilement les extraits de code. Si vous débutez, ne vous inquiétez pas ! Je vous guiderai à travers chaque partie.
## Paquets d'importation
Pour utiliser Aspose.Cells dans votre projet, vous devez importer les espaces de noms nécessaires. Voici comment configurer votre environnement :
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
Ces espaces de noms vous permettent d'accéder aux fonctionnalités principales d'Aspose.Cells, notamment la manipulation du classeur et les capacités de dessin pour des formes comme le Spinner.
Maintenant que nous avons couvert les prérequis et importé les packages nécessaires, passons au guide étape par étape. Chaque étape est conçue pour être claire et concise afin que vous puissiez la mettre en œuvre facilement.
## Étape 1 : Configurez votre répertoire de projet
Avant de commencer à coder, il est conseillé d'organiser vos fichiers. Créons un répertoire pour nos fichiers Excel.
```csharp
// Le chemin vers le répertoire des documents.
string dataDir = "Your Document Directory";
// Créez un répertoire s'il n'est pas déjà présent.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Ici, nous spécifions un chemin pour notre répertoire de documents. Si le répertoire n'existe pas, nous le créons. Cela garantit que tous nos fichiers générés ont un répertoire désigné.
## Étape 2 : Créer un nouveau classeur
Il est maintenant temps de créer un classeur Excel dans lequel nous ajouterons notre contrôle Spinner.
```csharp
// Instancier un nouveau classeur.
Workbook excelbook = new Workbook();
```
 Le`Workbook` La classe représente un fichier Excel. En l'instanciant, nous créons un nouveau classeur prêt à être modifié.
## Étape 3 : Accéder à la première feuille de travail
Nous ajouterons notre Spinner à la première feuille de calcul du classeur.
```csharp
// Obtenez la première feuille de travail.
Worksheet worksheet = excelbook.Worksheets[0];
```
Cette ligne permet d'accéder à la première feuille de calcul (index 0) de notre classeur. Vous pouvez avoir plusieurs feuilles de calcul, mais pour cet exemple, nous allons rester simples.
## Étape 4 : Travailler avec des cellules
Travaillons maintenant avec les cellules de notre feuille de calcul. Nous allons définir des valeurs et des styles.
```csharp
// Obtenez les cellules de la feuille de calcul.
Cells cells = worksheet.Cells;
// Saisissez une valeur de chaîne dans la cellule A1.
cells["A1"].PutValue("Select Value:");
// Définissez la couleur de police de la cellule.
cells["A1"].GetStyle().Font.Color = Color.Red;
// Mettre le texte de la police en gras.
cells["A1"].GetStyle().Font.IsBold = true;
// Saisissez la valeur dans la cellule A2.
cells["A2"].PutValue(0);
```
Ici, nous remplissons la cellule A1 avec une invite, en appliquant une couleur rouge et en mettant le texte en gras. Nous définissons également la cellule A2 sur une valeur initiale de 0, qui sera liée à notre Spinner.
## Étape 5 : styliser la cellule A2
Ensuite, appliquons quelques styles à la cellule A2 pour la rendre plus attrayante visuellement.
```csharp
// Définissez la couleur d’ombrage sur noir avec un arrière-plan uni.
cells["A2"].GetStyle().ForegroundColor = Color.Black;
cells["A2"].GetStyle().Pattern = BackgroundType.Solid;
// Définissez la couleur de police de la cellule.
cells["A2"].GetStyle().Font.Color = Color.White;
// Mettre le texte de la police en gras.
cells["A2"].GetStyle().Font.IsBold = true;
```
Nous ajoutons un arrière-plan noir avec un motif uni à la cellule A2 et définissons la couleur de police sur blanc. Ce contraste le fera ressortir sur la feuille de calcul.
## Étape 6 : ajouter le contrôle Spinner
Nous sommes maintenant prêts à ajouter le contrôle Spinner à notre feuille de calcul.
```csharp
// Ajoutez un contrôle de spinner.
Aspose.Cells.Drawing.Spinner spinner = excelbook.Worksheets[0].Shapes.AddSpinner(1, 0, 1, 0, 20, 18);
```
Cette ligne ajoute un contrôle Spinner à la feuille de calcul. Les paramètres spécifient la position et la taille du Spinner (ligne, colonne, largeur, hauteur).
## Étape 7 : Configurer les propriétés du Spinner
Personnalisons le comportement du Spinner en fonction de nos besoins.
```csharp
// Définissez le type de placement du spinner.
spinner.Placement = PlacementType.FreeFloating;
// Définissez la cellule liée pour le contrôle.
spinner.LinkedCell = "A2";
// Définir la valeur maximale.
spinner.Max = 10;
//Définir la valeur minimale.
spinner.Min = 0;
// Définissez le changement d'incrément pour le contrôle.
spinner.IncrementalChange = 2;
// Réglez-le sur un ombrage 3D.
spinner.Shadow = true;
```
Ici, nous définissons les propriétés du Spinner. Nous le lions à la cellule A2, ce qui lui permet de contrôler la valeur qui y est affichée. Les valeurs minimales et maximales définissent la plage dans laquelle le Spinner peut fonctionner, tandis que la modification incrémentielle définit la mesure dans laquelle la valeur change à chaque clic. L'ajout d'un ombrage 3D lui donne un aspect soigné.
## Étape 8 : Enregistrez le fichier Excel
Enfin, sauvegardons notre classeur Excel avec le Spinner inclus.
```csharp
// Enregistrez le fichier Excel.
excelbook.Save(dataDir + "book1.out.xls");
```
Cette commande enregistre le classeur dans le répertoire spécifié. Vous pouvez modifier le nom du fichier selon vos besoins.
## Conclusion
Et voilà ! Vous avez ajouté avec succès un contrôle Spinner à une feuille de calcul Excel à l'aide d'Aspose.Cells pour .NET. Cet élément interactif améliore l'expérience utilisateur en permettant des ajustements rapides des valeurs. Que vous créiez un outil de création de rapports dynamiques ou un formulaire de saisie de données, le contrôle Spinner peut être un ajout précieux. 
## FAQ
### Qu'est-ce qu'un contrôle Spinner dans Excel ?
Un contrôle Spinner permet aux utilisateurs d'incrémenter ou de décrémenter facilement une valeur numérique, offrant ainsi un moyen intuitif d'effectuer des sélections.
### Puis-je personnaliser l'apparence du Spinner ?
Oui, vous pouvez modifier sa taille, sa position et même son ombrage 3D pour un look plus soigné.
### Ai-je besoin d'une licence pour utiliser Aspose.Cells ?
 Aspose.Cells propose un essai gratuit, mais une licence payante est requise pour une utilisation en production. Découvrez le[options d'achat](https://purchase.aspose.com/buy).
### Comment puis-je obtenir de l'aide avec Aspose.Cells ?
 Pour obtenir de l'aide, visitez le[Forum Aspose](https://forum.aspose.com/c/cells/9) où vous pouvez poser des questions et trouver des réponses.
### Est-il possible d'ajouter plusieurs Spinners à la même feuille de calcul ?
Absolument ! Vous pouvez ajouter autant de Spinners que nécessaire en suivant les mêmes étapes pour chaque commande.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
