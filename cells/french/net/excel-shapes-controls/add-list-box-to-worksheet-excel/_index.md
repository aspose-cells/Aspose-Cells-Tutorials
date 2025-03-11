---
title: Ajouter une zone de liste à une feuille de calcul dans Excel
linktitle: Ajouter une zone de liste à une feuille de calcul dans Excel
second_title: API de traitement Excel Aspose.Cells .NET
description: Découvrez comment ajouter une zone de liste à une feuille de calcul Excel à l'aide d'Aspose.Cells pour .NET. Suivez notre guide simple et étape par étape et rendez vos feuilles Excel interactives.
weight: 20
url: /fr/net/excel-shapes-controls/add-list-box-to-worksheet-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ajouter une zone de liste à une feuille de calcul dans Excel

## Introduction
L'ajout d'éléments interactifs à vos feuilles de calcul Excel, comme une zone de liste, peut améliorer considérablement la gestion et la présentation des données. Que vous créiez un formulaire interactif ou un outil de saisie de données personnalisé, la possibilité de contrôler la saisie de l'utilisateur avec une zone de liste est inestimable. Aspose.Cells pour .NET offre un moyen efficace d'ajouter et de gérer ces contrôles dans vos fichiers Excel. Dans ce guide, nous vous expliquerons le processus d'ajout d'une zone de liste à une feuille de calcul à l'aide d'Aspose.Cells pour .NET.
## Prérequis
Avant de vous lancer dans le codage, assurez-vous de disposer des outils et ressources suivants :
-  Bibliothèque Aspose.Cells pour .NET : vous pouvez la télécharger à partir du[Page de téléchargement d'Aspose.Cells pour .NET](https://releases.aspose.com/cells/net/).
- Environnement de développement : tout IDE prenant en charge le développement .NET, tel que Visual Studio.
- .NET Framework : assurez-vous que votre projet cible une version prise en charge du .NET Framework.
 Pensez également à vous procurer un[permis temporaire](https://purchase.aspose.com/temporary-license/) si vous souhaitez explorer toutes les fonctionnalités sans limitations.
## Paquets d'importation
Avant de commencer, assurez-vous d'avoir importé les espaces de noms Aspose.Cells nécessaires. Voici comment procéder :
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
```
Dans ce tutoriel, nous allons décomposer le processus d'ajout d'une liste déroulante en plusieurs étapes simples. Suivez attentivement chaque étape pour vous assurer que tout fonctionne comme prévu.
## Étape 1 : Configuration de votre répertoire de documents
Avant de créer un fichier Excel, vous devez définir un emplacement pour l'enregistrer. Voici comment configurer le répertoire :
```csharp
// Le chemin vers le répertoire des documents.
string dataDir = "Your Document Directory";
// Créez un répertoire s'il n'existe pas déjà.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Dans cette étape, vous définissez l'emplacement de stockage de votre fichier. Le code vérifie si le répertoire existe et, si ce n'est pas le cas, il en crée un pour vous. Cela garantit que vous ne rencontrerez pas d'erreurs de type « fichier introuvable » par la suite.
## Étape 2 : créer un nouveau classeur et accéder à la première feuille de calcul
Ensuite, nous allons créer un nouveau classeur et accéder à la première feuille de calcul où nous ajouterons notre liste déroulante.
```csharp
// Créer un nouveau classeur.
Workbook workbook = new Workbook();
// Obtenez la première feuille de travail.
Worksheet sheet = workbook.Worksheets[0];
```
Un classeur est essentiellement votre fichier Excel. Ici, nous créons un nouveau classeur et accédons à la première feuille de calcul, dans laquelle nous placerons notre zone de liste. Considérez cela comme la création d'une toile vierge sur laquelle vous peindrez les contrôles.
## Étape 3 : Saisir les données pour la zone de liste
Avant d’ajouter la liste déroulante, nous devons renseigner certaines données auxquelles la liste déroulante fera référence.
```csharp
// Obtenez la collection de cellules de la feuille de calcul.
Cells cells = sheet.Cells;
// Saisissez une valeur pour l’étiquette.
cells["B3"].PutValue("Choose Dept:");
// Mettez l'étiquette en gras.
cells["B3"].GetStyle().Font.IsBold = true;
// Saisissez les valeurs pour la liste déroulante.
cells["A2"].PutValue("Sales");
cells["A3"].PutValue("Finance");
cells["A4"].PutValue("MIS");
cells["A5"].PutValue("R&D");
cells["A6"].PutValue("Marketing");
cells["A7"].PutValue("HRA");
```
Ici, nous ajoutons du texte dans la feuille de calcul. L'étiquette « Choisir un service : » est placée dans la cellule B3 et sa police est définie en gras. Dans la colonne A, nous insérons des valeurs qui serviront de plage de saisie pour notre liste déroulante, représentant différents services. Cette plage de saisie correspond à celle que les utilisateurs choisiront lorsqu'ils interagiront avec la liste déroulante.
## Étape 4 : ajouter la zone de liste à la feuille de calcul
Maintenant que nous avons configuré les données, ajoutons le contrôle de zone de liste lui-même.
```csharp
// Ajouter une nouvelle liste déroulante.
Aspose.Cells.Drawing.ListBox listBox = sheet.Shapes.AddListBox(2, 0, 3, 0, 122, 100);
```
Ce code ajoute la zone de liste à la feuille de calcul. Les paramètres définissent la position et la taille de la zone de liste. La zone de liste est placée à la ligne 2, colonne 0 avec une largeur de 122 et une hauteur de 100. Ce sont les coordonnées et la taille qui déterminent l'emplacement de la zone de liste dans la feuille de calcul.
## Étape 5 : définir les propriétés de la zone de liste
Ensuite, nous allons définir diverses propriétés pour la liste déroulante afin de la rendre pleinement fonctionnelle.
```csharp
// Définissez le type de placement.
listBox.Placement = PlacementType.FreeFloating;
// Définir la cellule liée.
listBox.LinkedCell = "A1";
// Définissez la plage d’entrée.
listBox.InputRange = "A2:A7";
// Définissez le type de sélection.
listBox.SelectionType = SelectionType.Single;
// Définissez la liste déroulante avec un ombrage 3D.
listBox.Shadow = true;
```
- PlacementType.FreeFloating : cette propriété garantit que la zone de liste reste à sa position quelle que soit la manière dont la feuille de calcul est modifiée.
- LinkedCell : cela définit une cellule (dans ce cas, A1) dans laquelle la valeur sélectionnée dans la liste déroulante sera affichée.
- InputRange : cela indique à la zone de liste où rechercher sa liste d'options (A2 à A7, que nous avons définies précédemment).
- SelectionType.Single : cela limite l'utilisateur à la sélection d'un seul élément dans la liste.
- Ombre : L’effet d’ombre donne à la zone de liste une apparence plus tridimensionnelle, la rendant visuellement attrayante.
## Étape 6 : Enregistrez le fichier Excel
Enfin, sauvegardons notre classeur avec la liste déroulante incluse.
```csharp
// Sauvegarder le classeur.
workbook.Save(dataDir + "book1.out.xls");
```
Cette ligne de code enregistre le classeur dans le répertoire que nous avons configuré précédemment. Le fichier est nommé « book1.out.xls » mais vous pouvez choisir n'importe quel nom qui convient à votre projet.
## Conclusion
Et voilà ! Vous avez ajouté avec succès une zone de liste à une feuille de calcul Excel à l'aide d'Aspose.Cells pour .NET. Avec seulement quelques lignes de code, nous avons créé une zone de liste entièrement fonctionnelle, rendant la feuille de calcul plus interactive et dynamique. Ce didacticiel devrait vous donner une base solide pour explorer d'autres contrôles et fonctionnalités dans Aspose.Cells pour .NET. Continuez à expérimenter et bientôt, vous maîtriserez les vastes fonctionnalités de la bibliothèque !
## FAQ
### Puis-je autoriser plusieurs sélections dans la liste déroulante ?  
 Oui, vous pouvez modifier le`SelectionType` à`SelectionType.Multi` pour permettre des sélections multiples.
### Puis-je modifier l’apparence de la liste déroulante ?  
Absolument ! Aspose.Cells vous permet de personnaliser l'apparence de la liste déroulante, y compris sa taille, sa police et même sa couleur.
### Que faire si je dois supprimer la liste déroulante plus tard ?  
 Vous pouvez accéder à la liste déroulante et la supprimer à partir de la`Shapes` collecte utilisant`sheet.Shapes.RemoveAt(index)`.
### Puis-je lier la liste déroulante à une cellule différente ?  
 Oui, changez simplement le`LinkedCell` propriété à toute autre cellule dans laquelle vous souhaitez afficher la valeur sélectionnée.
### Comment ajouter plus d’éléments à la liste déroulante ?  
Mettez simplement à jour la plage d'entrée en insérant plus de valeurs dans les cellules spécifiées et la zone de liste sera automatiquement mise à jour.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
