---
"description": "Découvrez comment ajouter une zone de liste déroulante à une feuille de calcul Excel par programmation avec Aspose.Cells pour .NET. Ce guide étape par étape vous guide pas à pas."
"linktitle": "Ajouter une zone de liste déroulante à une feuille de calcul dans Excel"
"second_title": "API de traitement Excel Aspose.Cells .NET"
"title": "Ajouter une zone de liste déroulante à une feuille de calcul dans Excel"
"url": "/fr/net/excel-shapes-controls/add-combo-box-to-worksheet-excel/"
"weight": 21
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Ajouter une zone de liste déroulante à une feuille de calcul dans Excel

## Introduction
Créer des feuilles de calcul Excel interactives peut grandement améliorer l'expérience utilisateur, notamment en ajoutant des éléments de formulaire tels que des zones de liste déroulante. Ces zones permettent aux utilisateurs de sélectionner des options dans une liste prédéfinie, ce qui simplifie et optimise la saisie des données. Avec Aspose.Cells pour .NET, vous pouvez créer des zones de liste déroulante dans des feuilles Excel par programmation, sans utiliser Excel directement. Cette puissante bibliothèque permet aux développeurs de manipuler les fichiers Excel de diverses manières, notamment en automatisant les contrôles de formulaire.
Dans ce tutoriel, nous vous expliquerons comment ajouter une zone de liste déroulante à une feuille de calcul Excel avec Aspose.Cells pour .NET. Si vous souhaitez créer des feuilles de calcul dynamiques et conviviales, ce guide vous aidera à démarrer.
## Prérequis
Avant de plonger dans le code, assurons-nous que vous disposez de tout ce dont vous avez besoin :
- Aspose.Cells pour .NET : téléchargez et installez la bibliothèque Aspose.Cells pour .NET à partir du [page de téléchargement](https://releases.aspose.com/cells/net/).
- .NET Framework : Assurez-vous que .NET Framework est installé sur votre ordinateur. Toute version prise en charge par Aspose.Cells fonctionnera.
- Environnement de développement : utilisez un IDE comme Visual Studio pour gérer votre projet et écrire du code.
- Licence Aspose : Vous pouvez travailler sans licence en mode évaluation, mais pour une version complète, vous devrez appliquer une licence. Obtenez une [permis temporaire](https://purchase.aspose.com/temporary-license/) si nécessaire.
## Importer des packages
Pour commencer, vous devez importer les espaces de noms requis dans votre projet. Voici ce dont vous avez besoin :
```csharp
using System.IO;
using Aspose.Cells;
```
Ils sont essentiels pour interagir avec les fichiers Excel et manipuler les éléments de formulaire comme les zones de liste déroulante dans le classeur.
Décomposons le processus d'ajout d'une zone de liste déroulante en plusieurs étapes simples pour une compréhension facile.
## Étape 1 : Configurer le répertoire de documents
La première étape consiste à créer un répertoire où seront enregistrés vos fichiers Excel. Vous pouvez créer un nouveau dossier s'il n'existe pas déjà.
```csharp
// Le chemin vers le répertoire des documents.
string dataDir = "Your Document Directory";
// Créez un répertoire s'il n'est pas déjà présent.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
- dataDir : spécifie l’emplacement où le fichier de sortie sera enregistré.
- System.IO.Directory.Exists : vérifie si le répertoire existe déjà.
- System.IO.Directory.CreateDirectory : crée le répertoire s'il est manquant.
## Étape 2 : Créer un nouveau classeur
Créez maintenant un nouveau classeur Excel dans lequel vous ajouterez la zone de liste déroulante.

```csharp
// Créer un nouveau classeur.
Workbook workbook = new Workbook();
```

- Classeur classeur : initialise une nouvelle instance de la classe Workbook, représentant un fichier Excel.
## Étape 3 : Obtenir la feuille de calcul et les cellules
Ensuite, accédez à la première feuille de calcul du classeur et récupérez la collection de cellules dans laquelle vous saisirez les données.

```csharp
// Obtenez la première feuille de travail.
Worksheet sheet = workbook.Worksheets[0];
// Obtenez la collection de cellules de la feuille de calcul.
Cells cells = sheet.Cells;
```

- Feuille de calcul : récupère la première feuille de calcul du classeur.
- Cellules cellules : obtient la collection de cellules de la feuille de calcul.
## Étape 4 : Saisir les valeurs de la zone de liste déroulante
Nous devons maintenant saisir des valeurs dans les cellules. Ces valeurs serviront d'options pour la zone de liste déroulante.

```csharp
// Saisissez une valeur.
cells["B3"].PutValue("Employee:");
// Mettez-le en gras.
cells["B3"].GetStyle().Font.IsBold = true;
// Saisissez quelques valeurs qui indiquent la plage de saisie pour la zone de liste déroulante.
cells["A2"].PutValue("Emp001");
cells["A3"].PutValue("Emp002");
cells["A4"].PutValue("Emp003");
cells["A5"].PutValue("Emp004");
cells["A6"].PutValue("Emp005");
cells["A7"].PutValue("Emp006");
```

- cells["B3"].PutValue : place l'étiquette « Employé » dans la cellule B3.
- Font.IsBold = true : met le texte en gras pour le faire ressortir.
- Plage de saisie : saisissez plusieurs identifiants d'employés dans les cellules A2 à A7. Ceux-ci apparaîtront dans la liste déroulante.
## Étape 5 : Ajouter la zone de liste déroulante à la feuille de calcul
L'étape suivante consiste à ajouter la zone de liste déroulante à votre feuille de calcul. Cette zone permettra aux utilisateurs de sélectionner l'un des identifiants d'employé saisis précédemment.

```csharp
// Ajouter une nouvelle zone de liste déroulante.
Aspose.Cells.Drawing.ComboBox comboBox = sheet.Shapes.AddComboBox(2, 0, 2, 0, 22, 100);
```

- AddComboBox : ajoute une zone de liste déroulante à la feuille de calcul. Les nombres (2, 0, 2, 0, 22, 100) représentent la position et les dimensions de la zone de liste déroulante.
## Étape 6 : Liez la zone de liste déroulante à une cellule et définissez la plage de saisie
Pour rendre la zone de liste déroulante fonctionnelle, nous devons la lier à une cellule spécifique et définir la plage de cellules à partir de laquelle elle extraira ses options.

```csharp
// Définir la cellule liée.
comboBox.LinkedCell = "A1";
// Définissez la plage d’entrée.
comboBox.InputRange = "A2:A7";
```

- LinkedCell : lie la sélection de la zone de liste déroulante à la cellule A1. La valeur sélectionnée dans la zone de liste déroulante apparaîtra dans cette cellule.
- InputRange : définit la plage de cellules (A2 : A7) contenant les valeurs qui rempliront les options de la zone de liste déroulante.
## Étape 7 : Personnaliser l’apparence de la zone de liste déroulante
Vous pouvez personnaliser davantage la zone de liste déroulante en spécifiant le nombre de lignes déroulantes et en activant l'ombrage 3D pour une meilleure esthétique.

```csharp
// Définissez le nombre de lignes de liste affichées dans la partie liste de la zone de liste déroulante.
comboBox.DropDownLines = 5;
// Définissez la zone de liste déroulante avec un ombrage 3D.
comboBox.Shadow = true;
```

- DropDownLines : contrôle le nombre d'options qui seront visibles dans la liste déroulante de la zone de liste déroulante à la fois.
- Ombre : ajoute un effet d'ombrage 3D à la zone de liste déroulante.
## Étape 8 : Ajuster automatiquement les colonnes et enregistrer le classeur
Enfin, ajustons automatiquement les colonnes pour une mise en page propre et enregistrons le classeur.

```csharp
// Colonnes d'ajustement automatique
sheet.AutoFitColumns();
// Enregistre le fichier.
workbook.Save(dataDir + "book1.out.xls");
```

- AutoFitColumns : ajuste automatiquement la largeur des colonnes pour s'adapter au contenu.
- Enregistrer : enregistre le classeur sous forme de fichier Excel dans le répertoire spécifié.

## Conclusion
Ajouter une zone de liste déroulante à vos feuilles de calcul Excel avec Aspose.Cells pour .NET est un processus simple qui améliore considérablement la flexibilité de saisie des données. En créant des contrôles de formulaire par programmation, vous pouvez facilement créer des feuilles de calcul interactives. Ce tutoriel vous a montré comment ajouter une zone de liste déroulante, la lier à une cellule et configurer sa plage de saisie, le tout avec Aspose.Cells.
Aspose.Cells offre une vaste gamme de fonctionnalités pour la manipulation de fichiers Excel, ce qui en fait un choix idéal pour les développeurs souhaitant automatiser les tâches liées aux feuilles de calcul. Essayez-le avec un [essai gratuit](https://releases.aspose.com/).
## FAQ
### Puis-je utiliser Aspose.Cells sans Excel installé ?
Oui, Aspose.Cells fonctionne indépendamment d'Excel et ne nécessite pas l'installation d'Excel.
### Comment appliquer une licence dans Aspose.Cells ?
Vous pouvez demander une licence en l'obtenant auprès de [ici](https://purchase.aspose.com/buy) et appelant `License.SetLicense()` dans votre code.
### Quels formats Aspose.Cells prend-il en charge pour l'enregistrement des fichiers ?
Aspose.Cells prend en charge l'enregistrement de fichiers dans plusieurs formats tels que XLSX, XLS, CSV, PDF, etc.
### Y a-t-il une limite au nombre de zones de liste déroulante que je peux ajouter ?
Non, il n'y a pas de limite stricte ; vous pouvez ajouter autant de zones de liste déroulante que votre projet le nécessite.
### Comment obtenir de l'aide pour Aspose.Cells ?
Vous pouvez obtenir du soutien auprès du [Forum Aspose](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}