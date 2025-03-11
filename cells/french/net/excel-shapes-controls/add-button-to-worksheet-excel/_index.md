---
title: Ajouter un bouton à une feuille de calcul dans Excel
linktitle: Ajouter un bouton à une feuille de calcul dans Excel
second_title: API de traitement Excel Aspose.Cells .NET
description: Découvrez comment ajouter un bouton à une feuille de calcul Excel à l'aide d'Aspose.Cells pour .NET avec ce didacticiel étape par étape. Améliorez les feuilles de calcul Excel avec des boutons interactifs.
weight: 12
url: /fr/net/excel-shapes-controls/add-button-to-worksheet-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ajouter un bouton à une feuille de calcul dans Excel

## Introduction
Les feuilles de calcul Excel sont polyvalentes et couramment utilisées pour gérer les données, mais elles nécessitent parfois une interactivité supplémentaire. L'un des meilleurs moyens d'améliorer l'expérience utilisateur consiste à ajouter des boutons à une feuille de calcul. Ces boutons peuvent déclencher des macros ou diriger les utilisateurs vers des liens utiles. Si vous êtes un développeur .NET travaillant avec des fichiers Excel, Aspose.Cells pour .NET offre un moyen simple de manipuler les classeurs Excel par programmation, notamment en ajoutant des boutons.
Dans ce tutoriel, nous vous expliquerons comment ajouter un bouton à une feuille de calcul dans Excel à l'aide d'Aspose.Cells pour .NET. Nous aborderons tous les détails, de la configuration des prérequis aux instructions étape par étape. Plongeons-nous dans le vif du sujet !
## Prérequis
Avant de pouvoir suivre ce didacticiel, assurez-vous que les outils et packages suivants sont installés :
-  Bibliothèque Aspose.Cells pour .NET : vous pouvez la télécharger à partir de[ici](https://releases.aspose.com/cells/net/).
- Environnement de développement .NET : assurez-vous que vous disposez d’un environnement .NET fonctionnel tel que Visual Studio installé.
- Une compréhension de base de C# : vous devez être familiarisé avec les bases de la programmation C#.
-  Permis : Vous aurez besoin d'un permis valide. Si vous n'en avez pas, vous pouvez en obtenir un[essai gratuit](https://releases.aspose.com/) ou postulez pour un[permis temporaire](https://purchase.aspose.com/temporary-license/).
Passons à l’importation des packages nécessaires.
## Paquets d'importation
Avant de commencer à coder, vous devez importer les packages requis dans votre projet .NET. Voici un extrait de code simple pour vous aider à importer Aspose.Cells dans votre projet :
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
Maintenant que nous avons importé les packages nécessaires, décomposons l'exemple en un guide détaillé étape par étape.
## Étape 1 : Configurer le classeur et la feuille de calcul
Dans cette première étape, nous allons créer un nouveau classeur Excel et obtenir une référence à la première feuille de calcul.
```csharp
// Définissez le chemin vers votre répertoire de documents.
string dataDir = "Your Document Directory";
// Créez un répertoire s'il n'est pas déjà présent.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
	System.IO.Directory.CreateDirectory(dataDir);
// Créer un nouveau classeur.
Workbook workbook = new Workbook();
// Prenez la première feuille de travail du classeur.
Worksheet sheet = workbook.Worksheets[0];
```

-  Création du classeur : Nous commençons par créer un nouveau`Workbook` objet qui représente un fichier Excel.
-  Référence de la feuille de travail : Le`Worksheets[0]` La commande récupère la première feuille de calcul du classeur, que nous allons modifier.
Cette étape définit les bases en créant un fichier Excel vierge avec une seule feuille de calcul.
## Étape 2 : ajouter un bouton à la feuille de calcul
Ensuite, nous allons ajouter un bouton à la feuille de calcul. C'est là que la magie opère !
```csharp
// Ajoutez un nouveau bouton à la feuille de calcul.
Aspose.Cells.Drawing.Button button = sheet.Shapes.AddButton(2, 0, 2, 0, 28, 80);
```

- Méthode AddButton : cette méthode ajoute un bouton à un emplacement spécifié dans la feuille de calcul. Les paramètres définissent la position du bouton (ligne, colonne, décalage x, décalage y) et sa taille (hauteur, largeur).
- Ligne et colonne : le bouton est placé à la ligne 2 et à la colonne 0, sans décalage supplémentaire.
- Taille : La hauteur du bouton est fixée à 28 et la largeur à 80.
Cette étape ajoute avec succès un bouton à la feuille de calcul, mais nous n’avons pas encore terminé : personnalisons-le.
## Étape 3 : définir les propriétés du bouton
Il est maintenant temps de personnaliser l'apparence du bouton en définissant son texte, sa police et son emplacement.
```csharp
// Définissez la légende du bouton.
button.Text = "Aspose";
// Définissez le type de placement, la manière dont le bouton est attaché aux cellules.
button.Placement = PlacementType.FreeFloating;
```

- Texte : Nous avons défini la légende du bouton sur « Aspose ».
-  Placement : nous définissons comment le bouton est positionné par rapport aux cellules de la feuille de calcul.`FreeFloating` permet au bouton de se déplacer indépendamment des cellules.
Cette étape personnalise la légende et le placement du bouton.
## Étape 4 : Personnaliser la police du bouton
Donnons du style au bouton en personnalisant les propriétés de la police.
```csharp
// Définissez le nom de la police.
button.Font.Name = "Tahoma";
// Définissez la chaîne de légende en gras.
button.Font.IsBold = true;
// Réglez la couleur sur bleu.
button.Font.Color = Color.Blue;
```

- Nom de la police : Nous changeons la police en « Tahoma », qui est une police propre et moderne.
- Gras : nous mettons le texte du bouton en gras pour le mettre en valeur.
- Couleur : La couleur de la police est définie sur bleu, ce qui fait ressortir le texte du bouton.
Cette étape améliore l’apparence du bouton, garantissant qu’il est à la fois fonctionnel et visuellement attrayant.
## Étape 5 : ajouter un lien hypertexte au bouton
Vous pouvez rendre le bouton encore plus utile en ajoutant un lien hypertexte.
```csharp
// Définissez le lien hypertexte pour le bouton.
button.AddHyperlink("https://www.aspose.com/");
```

- AddHyperlink : nous utilisons cette méthode pour ajouter un lien hypertexte cliquable au bouton. Une fois cliqué, le bouton redirige vers le site Web Aspose.
Cette étape ajoute de l’interactivité au bouton, le rendant fonctionnel au-delà de la simple esthétique.
## Étape 6 : Enregistrez le fichier Excel
Une fois que tout est configuré, n'oubliez pas de sauvegarder vos modifications !
```csharp
// Enregistre le fichier.
workbook.Save(dataDir + "book1.out.xls");
```

-  Méthode de sauvegarde : Nous utilisons le`Save` méthode permettant d'écrire le classeur modifié dans un nouveau fichier. Le fichier sera enregistré dans le répertoire spécifié.
Félicitations ! Vous avez maintenant ajouté un bouton entièrement personnalisé à une feuille de calcul Excel.
## Conclusion
L'ajout de boutons aux feuilles de calcul Excel peut grandement améliorer la fonctionnalité de vos feuilles de calcul, les rendant plus interactives et conviviales. Avec Aspose.Cells pour .NET, vous pouvez y parvenir avec seulement quelques lignes de code, comme nous l'avons montré dans ce didacticiel.
Aspose.Cells pour .NET est une bibliothèque puissante qui offre des possibilités infinies de manipulation d'Excel. Que vous automatisiez des tâches ou ajoutiez de nouvelles fonctionnalités à vos feuilles de calcul, cette bibliothèque est votre solution de référence.
 Si vous ne l'avez pas déjà fait,[télécharger la bibliothèque Aspose.Cells pour .NET](https://releases.aspose.com/cells/net/) et commencez à améliorer vos fichiers Excel.
## FAQ
### Puis-je utiliser d’autres formes en plus des boutons dans Aspose.Cells pour .NET ?
Oui, Aspose.Cells vous permet d'ajouter diverses formes, notamment des cases à cocher, des boutons radio, etc.
### Puis-je déclencher une macro à partir d'un bouton ajouté via Aspose.Cells ?
Oui, vous pouvez lier le bouton à une macro, mais vous devrez gérer le code de la macro séparément dans Excel.
### Comment puis-je faire en sorte que le bouton se redimensionne automatiquement avec les cellules ?
 Utilisez le`PlacementType.Move` propriété permettant au bouton de se redimensionner avec les cellules.
### Est-il possible d'ajouter plusieurs boutons sur une seule feuille de calcul ?
 Absolument ! Vous pouvez ajouter autant de boutons que vous le souhaitez en appelant le`AddButton` méthode plusieurs fois.
### Puis-je personnaliser davantage l’apparence du bouton ?
Oui, vous pouvez modifier de nombreuses propriétés, notamment la couleur d'arrière-plan, le style de bordure, etc.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
