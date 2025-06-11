---
"description": "Apprenez à ajouter des boutons radio à une feuille de calcul Excel avec Aspose.Cells pour .NET grâce à ce guide simple et détaillé. Idéal pour créer des formulaires Excel interactifs."
"linktitle": "Ajouter un bouton radio à une feuille de calcul dans Excel"
"second_title": "API de traitement Excel Aspose.Cells .NET"
"title": "Ajouter un bouton radio à une feuille de calcul dans Excel"
"url": "/fr/net/excel-shapes-controls/add-radio-button-to-worksheet-excel/"
"weight": 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Ajouter un bouton radio à une feuille de calcul dans Excel

## Introduction
Vous êtes-vous déjà demandé comment agrémenter vos feuilles Excel d'éléments interactifs comme des boutons radio ? Que vous créiez une enquête, un formulaire ou un outil d'analyse, l'ajout de boutons radio peut réellement améliorer l'interaction utilisateur. Dans ce tutoriel, nous vous expliquerons comment ajouter des boutons radio à vos feuilles Excel avec Aspose.Cells pour .NET. Nous détaillerons le processus en étapes faciles à suivre, pour que vous soyez un pro à la fin de cet article. Prêt à vous lancer ? C'est parti !
## Prérequis
Avant de passer à la partie amusante de l'ajout de boutons radio, assurons-nous que tout est configuré pour commencer.
1. Aspose.Cells pour .NET : Tout d’abord, assurez-vous d’avoir téléchargé et installé le [Aspose.Cells pour .NET](https://releases.aspose.com/cells/net/) Bibliothèque. Vous pouvez la télécharger via NuGet dans Visual Studio ou depuis la page de téléchargement.
2. IDE (environnement de développement intégré) : vous aurez besoin d'un IDE comme Visual Studio pour écrire et exécuter votre code C#.
3. .NET Framework : Assurez-vous que .NET Framework 4.0 ou supérieur est installé sur votre ordinateur. Aspose.Cells en a besoin pour fonctionner.
4. Compréhension de base de C# : la familiarité avec la syntaxe C# et la programmation .NET facilitera les choses au fur et à mesure que vous suivrez.
Une fois que tout est en place, nous sommes prêts à démarrer !
## Importer des packages
Avant de coder, il est essentiel d'importer les espaces de noms nécessaires pour éviter toute erreur ultérieure. Ajoutez les éléments suivants à votre code :
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
using Aspose.Cells.Drawing;
```
Ces importations sont essentielles pour accéder aux fonctionnalités du classeur, ajouter des boutons radio et gérer les opérations sur les fichiers.
## Étape 1 : Configuration du classeur
Tout d’abord, créons un nouveau classeur Excel.
Pour commencer, vous devrez instancier un nouveau `Workbook` objet. Cela représentera votre fichier Excel en code.
```csharp
// Instancier un nouveau classeur.
Workbook excelbook = new Workbook();
```
Dans cette étape, vous créez un classeur vierge. Imaginez-le comme une toile vierge sur laquelle vous ajouterez des boutons radio lors des étapes suivantes.
## Étape 2 : Ajout et formatage d'une valeur de cellule
Ensuite, ajoutons un titre à la feuille de calcul. Nous ajouterons du texte à la cellule. `C2` et mettez-le en gras. Cette étape ajoute du contexte à vos boutons radio.
### Insérer du texte dans la cellule
```csharp
// Insérer une valeur dans la cellule C2.
excelbook.Worksheets[0].Cells["C2"].PutValue("Age Groups");
```
### Mettre le texte en gras
```csharp
// Définissez le texte de police dans la cellule C2 en gras.
excelbook.Worksheets[0].Cells["C2"].GetStyle().Font.IsBold = true;
```
Ici, nous avons ajouté un titre simple, « Groupes d'âge », dans la cellule `C2`, et je l'ai mis en gras pour qu'il se démarque. Facile, non ?
## Étape 3 : Ajout du premier bouton radio
Vient maintenant la partie passionnante : ajouter votre premier bouton radio à la feuille de calcul !
### Ajouter un bouton radio
```csharp
// Ajoutez un bouton radio à la première feuille.
Aspose.Cells.Drawing.RadioButton radio1 = excelbook.Worksheets[0].Shapes.AddRadioButton(3, 0, 2, 0, 30, 110);
```
Cette ligne ajoute le bouton radio à un emplacement spécifique de votre feuille de calcul. Les chiffres représentent son emplacement et sa taille. C'est comme définir les coordonnées X et Y du bouton.
### Définir le texte du bouton radio
```csharp
// Définissez sa chaîne de texte.
radio1.Text = "20-29";
```
Ici, nous avons attribué au bouton radio une étiquette, « 20-29 », représentant une tranche d'âge.
### Lier le bouton radio à une cellule
```csharp
// Définissez la cellule A1 comme cellule liée pour le bouton radio.
radio1.LinkedCell = "A1";
```
Ceci relie le bouton radio à la cellule `A1`, ce qui signifie que le résultat de la sélection du bouton sera stocké dans cette cellule.
### Ajouter un effet 3D
```csharp
// Créez le bouton radio en 3D.
radio1.Shadow = true;
```
Parce que nous voulons que ce bouton radio apparaisse, nous avons ajouté un effet 3D.
### Personnaliser la ligne du bouton radio
```csharp
// Définissez le poids de la ligne du bouton radio.
radio1.Line.Weight = 4;
// Définissez le style de tiret de la ligne du bouton radio.
radio1.Line.DashStyle = MsoLineDashStyle.Solid;
```
Ces lignes de code ajustent l'épaisseur et le style de tiret de la bordure du bouton radio pour le rendre plus attrayant visuellement.
## Étape 4 : Ajout de boutons radio supplémentaires
Ajoutons deux cases d'option supplémentaires pour les tranches d'âge restantes : « 30-39 » et « 40-49 ». Les étapes sont identiques, avec seulement quelques variations dans les coordonnées et les libellés.
### Ajouter le deuxième bouton radio
```csharp
// Ajoutez un autre bouton radio à la première feuille.
Aspose.Cells.Drawing.RadioButton radio2 = excelbook.Worksheets[0].Shapes.AddRadioButton(6, 0, 2, 0, 30, 110);
// Définissez sa chaîne de texte.
radio2.Text = "30-39";
// Définissez la cellule A1 comme cellule liée pour le bouton radio.
radio2.LinkedCell = "A1";
// Créez le bouton radio en 3D.
radio2.Shadow = true;
// Définissez le poids du bouton radio.
radio2.Line.Weight = 4;
// Définissez le style de tiret du bouton radio.
radio2.Line.DashStyle = MsoLineDashStyle.Solid;
```
### Ajouter le troisième bouton radio
```csharp
// Ajoutez un autre bouton radio à la première feuille.
Aspose.Cells.Drawing.RadioButton radio3 = excelbook.Worksheets[0].Shapes.AddRadioButton(9, 0, 2, 0, 30, 110);
// Définissez sa chaîne de texte.
radio3.Text = "40-49";
// Définissez la cellule A1 comme cellule liée pour le bouton radio.
radio3.LinkedCell = "A1";
// Créez le bouton radio en 3D.
radio3.Shadow = true;
// Définissez le poids du bouton radio.
radio3.Line.Weight = 4;
// Définissez le style de tiret du bouton radio.
radio3.Line.DashStyle = MsoLineDashStyle.Solid;
```
## Étape 5 : Enregistrement du fichier Excel
Une fois tous vos boutons radio ajoutés et formatés, il est temps d'enregistrer le fichier.
```csharp
// Enregistrez le fichier Excel.
string dataDir = "Your Document Directory";
excelbook.Save(dataDir + "book1.out.xls");
```
À cette étape, le classeur est enregistré dans le répertoire spécifié. C'est aussi simple que ça : votre feuille de calcul interactive est prête !
## Conclusion
Et voilà ! Vous venez d'ajouter des boutons radio à une feuille de calcul Excel avec Aspose.Cells pour .NET. Ce tutoriel a tout expliqué, de la configuration du classeur à l'insertion et au formatage d'une valeur, en passant par l'ajout de plusieurs boutons radio et leur liaison à une cellule. Vous êtes maintenant prêt à créer des feuilles Excel interactives, non seulement esthétiques, mais aussi offrant une expérience utilisateur améliorée. Amusez-vous à explorer les nouvelles possibilités d'Aspose.Cells !
## FAQ
### Puis-je ajouter plus de boutons radio à différentes feuilles ?  
Absolument ! Vous pouvez répéter le processus sur n'importe quelle feuille du classeur en spécifiant l'index correct.
### Puis-je personnaliser davantage l’apparence des boutons radio ?  
Oui, Aspose.Cells fournit une variété d'options de personnalisation, notamment la modification des couleurs, des tailles et d'autres attributs de formatage.
### Comment puis-je détecter quel bouton radio est sélectionné ?  
La cellule liée (par exemple, A1) affichera l'index du bouton radio sélectionné. Vous pouvez vérifier la valeur de la cellule liée pour savoir lequel est sélectionné.
### Y a-t-il une limite au nombre de boutons radio que je peux ajouter ?  
Non, il n'y a pas de limite stricte au nombre de cases d'option que vous pouvez ajouter. Il est toutefois préférable de conserver une interface conviviale.
### Puis-je utiliser Aspose.Cells avec d’autres langages de programmation ?  
Oui, Aspose.Cells prend en charge plusieurs langages de programmation, dont Java. Cependant, ce tutoriel se concentre spécifiquement sur .NET.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}