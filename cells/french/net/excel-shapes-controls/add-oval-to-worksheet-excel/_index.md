---
"description": "Apprenez à ajouter un ovale à une feuille de calcul Excel avec Aspose.Cells pour .NET. Guide étape par étape avec explications détaillées du code."
"linktitle": "Ajouter un ovale à une feuille de calcul dans Excel"
"second_title": "API de traitement Excel Aspose.Cells .NET"
"title": "Ajouter un ovale à une feuille de calcul dans Excel"
"url": "/fr/net/excel-shapes-controls/add-oval-to-worksheet-excel/"
"weight": 17
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Ajouter un ovale à une feuille de calcul dans Excel

## Introduction
Créer des fichiers Excel attrayants et interactifs ne se limite pas à des chiffres et des formules. Des formes comme les ovales peuvent ajouter un attrait visuel ou des éléments fonctionnels à vos feuilles de calcul. Dans ce tutoriel, nous découvrirons comment utiliser Aspose.Cells pour .NET pour ajouter des ovales à une feuille de calcul Excel par programmation. Que vous cherchiez à ajouter une touche d'originalité ou des fonctionnalités, nous vous proposons un guide étape par étape qui vous explique tout.
## Prérequis
Avant de plonger dans le code, vous devez mettre en place quelques éléments :
1. Bibliothèque Aspose.Cells pour .NET : vous pouvez la télécharger à partir de [ici](https://releases.aspose.com/cells/net/) ou installez-le à l'aide de NuGet dans Visual Studio.
2. Environnement de développement : AC# IDE comme Visual Studio.
3. Compréhension de base de C# : vous devez être familiarisé avec les concepts de codage de base en C#.
N'oubliez pas de configurer votre projet en installant la bibliothèque Aspose.Cells pour .NET. Si vous ne possédez pas encore de licence, vous pouvez en demander une. [permis temporaire](https://purchase.aspose.com/temporary-license/) ou utilisez le [essai gratuit](https://releases.aspose.com/) version.
## Importer des packages
Avant d'écrire du code, assurez-vous d'avoir inclus les espaces de noms requis. Voici l'extrait de code C# pour vous assurer d'utiliser les bonnes bibliothèques :
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
## Étape 1 : Configurez votre répertoire
La première étape pour ajouter un ovale à une feuille Excel consiste à spécifier l'emplacement d'enregistrement de votre fichier Excel. Définissons le chemin d'accès au répertoire et vérifions son existence avant d'enregistrer notre travail.

Nous allons créer un chemin de répertoire et vérifier son existence. Si le dossier n'existe pas, il sera créé.
```csharp
// Le chemin vers le répertoire des documents.
string dataDir = "Your Document Directory";
// Créez un répertoire s'il n'est pas déjà présent.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Cette étape est cruciale car elle garantit que votre fichier est enregistré dans un emplacement approprié et que vous ne rencontrerez pas de problèmes de chemin de fichier plus tard.
## Étape 2 : Initialiser un nouveau classeur
Ensuite, nous devons créer un nouveau classeur dans lequel nous ajouterons nos formes ovales. Ce classeur représente un fichier Excel dans lequel nous pouvons ajouter du contenu ou des formes.

Dans cette étape, nous instancions un nouveau `Workbook` objet qui servira de conteneur à notre fichier Excel.
```csharp
// Instancier un nouveau classeur.
Workbook excelbook = new Workbook();
```
## Étape 3 : ajouter la première forme ovale
Vient maintenant la partie amusante : ajouter une forme ovale à la feuille de calcul. Cet ovale peut représenter un élément visuel, comme un bouton ou un surlignage. Nous allons commencer par ajouter la première forme ovale à la première feuille de calcul de notre classeur.

Ici, nous utilisons le `Shapes.AddOval()` méthode pour créer un ovale sur la feuille de calcul à une ligne et une colonne spécifiques.
```csharp
// Ajoutez une forme ovale.
Aspose.Cells.Drawing.Oval oval1 = excelbook.Worksheets[0].Shapes.AddOval(2, 0, 2, 0, 130, 160);
```
Les paramètres à l'intérieur `AddOval()` sont les suivantes :
- Les deux premiers chiffres représentent la ligne et la colonne du coin supérieur gauche de l'ovale.
- Les deux chiffres suivants représentent la hauteur et la largeur de l'ovale.
## Étape 4 : Définir l'emplacement et le style de l'ovale
Une fois l'ovale créé, nous pouvons définir sa position, son épaisseur de ligne et son style de tiret. `Placement` La propriété détermine le comportement de l'ovale lorsque vous redimensionnez ou déplacez des cellules dans la feuille de calcul.

Nous rendons l'ovale flottant et ajustons son apparence.
```csharp
// Définissez l'emplacement de l'ovale.
oval1.Placement = PlacementType.FreeFloating;
// Définissez l'épaisseur de la ligne.
oval1.Line.Weight = 1;
// Définissez le style de tiret de l'ovale.
oval1.Line.DashStyle = MsoLineDashStyle.Solid;
```
Cela permet à l'ovale de se déplacer librement dans la feuille de calcul, et son épaisseur de ligne et son style sont définis pour une cohérence visuelle.
## Étape 5 : Ajoutez une autre forme ovale (cercle)
Pourquoi s'arrêter à une seule ? Dans cette étape, nous allons ajouter une autre forme ovale, créant cette fois un cercle parfait en égalisant la hauteur et la largeur.

Nous créons un autre ovale, le plaçons à un endroit différent et nous assurons qu'il a une forme circulaire en définissant une hauteur et une largeur égales.
```csharp
// Ajoutez une autre forme ovale (cercle).
Aspose.Cells.Drawing.Oval oval2 = excelbook.Worksheets[0].Shapes.AddOval(9, 0, 2, 15, 130, 130);
```
## Étape 6 : Coiffer le deuxième ovale
Tout comme précédemment, nous ajusterons le placement, le poids et le style de tiret de ce deuxième ovale (ou cercle).

Nous appliquons des propriétés similaires au deuxième ovale pour correspondre au style du premier.
```csharp
// Définissez l'emplacement de l'ovale.
oval2.Placement = PlacementType.FreeFloating;
// Définissez l'épaisseur de la ligne.
oval2.Line.Weight = 1;
// Définissez le style de tiret de l'ovale.
oval2.Line.DashStyle = MsoLineDashStyle.Solid;
```
## Étape 7 : Enregistrer le classeur
Enfin, nous devons enregistrer le classeur avec les ovales que nous venons d'ajouter. Cela garantit que toutes nos modifications sont enregistrées.

Nous enregistrons le classeur dans le chemin du répertoire que nous avons défini précédemment.
```csharp
// Enregistrez le fichier Excel.
excelbook.Save(dataDir + "book1.out.xls");
```
Et voilà ! Vous avez ajouté des ovales à votre feuille de calcul Excel et enregistré le fichier.
## Conclusion
Ajouter des formes comme des ovales à une feuille Excel avec Aspose.Cells pour .NET est non seulement simple, mais aussi une façon ludique d'enrichir vos feuilles de calcul avec des éléments visuels supplémentaires. Que ce soit pour la conception ou pour ajouter des éléments cliquables, les formes peuvent jouer un rôle important dans l'apparence et le fonctionnement de vos fichiers Excel. Alors, la prochaine fois que vous travaillerez sur un projet nécessitant des feuilles Excel interactives ou visuellement attrayantes, vous saurez exactement comment ajouter ces ovales parfaits !
## FAQ
### Puis-je ajouter d’autres formes comme des rectangles ou des lignes à l’aide d’Aspose.Cells pour .NET ?
Oui, vous pouvez ajouter diverses formes comme des rectangles, des lignes et des flèches à l'aide du `Shapes` collection dans Aspose.Cells.
### Est-il possible de redimensionner les ovales après les avoir ajoutés ?
Absolument ! Vous pouvez modifier la hauteur et la largeur des ovales après les avoir ajoutés.
### Dans quels formats de fichiers puis-je enregistrer le classeur en plus de XLS ?
Aspose.Cells prend en charge plusieurs formats tels que XLSX, CSV et PDF, entre autres.
### Puis-je modifier la couleur du contour de l'ovale ?
Oui, vous pouvez modifier la couleur de la ligne de l'ovale en utilisant le `Line.Color` propriété.
### Est-il nécessaire d'avoir une licence pour Aspose.Cells ?
Bien que vous puissiez essayer Aspose.Cells avec un essai gratuit, vous aurez besoin d'un [licence](https://purchase.aspose.com/buy) pour une utilisation à long terme ou pour accéder à des fonctionnalités avancées.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}