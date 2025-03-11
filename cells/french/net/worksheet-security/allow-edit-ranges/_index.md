---
title: Autoriser les utilisateurs à modifier les plages dans la feuille de calcul à l'aide d'Aspose.Cells
linktitle: Autoriser les utilisateurs à modifier les plages dans la feuille de calcul à l'aide d'Aspose.Cells
second_title: API de traitement Excel Aspose.Cells .NET
description: Apprenez à créer des plages modifiables dans des feuilles de calcul Excel à l'aide d'Aspose.Cells pour .NET, permettant à des cellules spécifiques d'être modifiables tout en sécurisant le reste avec la protection de la feuille de calcul.
weight: 10
url: /fr/net/worksheet-security/allow-edit-ranges/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Autoriser les utilisateurs à modifier les plages dans la feuille de calcul à l'aide d'Aspose.Cells

## Introduction
Les documents Excel contiennent souvent des données sensibles ou du contenu structuré que vous souhaitez protéger contre toute modification indésirable. Cependant, il peut y avoir des cellules ou des plages spécifiques que vous souhaitez rendre modifiables pour certains utilisateurs. C'est là qu'intervient Aspose.Cells pour .NET, un outil puissant qui vous permet de protéger une feuille de calcul entière tout en accordant des autorisations de modification à des plages désignées. Imaginez que vous partagiez une feuille de calcul budgétaire dans laquelle seules certaines cellules sont modifiables et d'autres restent sécurisées : Aspose.Cells rend cette opération simple et efficace.
## Prérequis
Avant de plonger dans la partie codage, assurons-nous que vous disposez de tout ce dont vous avez besoin :
-  Aspose.Cells pour .NET : assurez-vous d'avoir installé la bibliothèque Aspose.Cells pour .NET. Vous pouvez la télécharger[ici](https://releases.aspose.com/cells/net/).
- Environnement de développement : Visual Studio ou tout IDE compatible C#.
- .NET Framework : version 4.0 ou ultérieure.
- Licence : Pensez à obtenir une licence pour éviter les limitations d'essai. Vous pouvez obtenir une[licence temporaire ici](https://purchase.aspose.com/temporary-license/).
## Paquets d'importation
Assurez-vous d'inclure l'espace de noms Aspose.Cells nécessaire au début de votre code :
```csharp
using System.IO;
using Aspose.Cells;
```
Cela garantira que vous pourrez accéder à toutes les classes et méthodes requises pour configurer des plages protégées dans les fichiers Excel.
Maintenant que les bases sont en place, parcourons le code en détail, une étape à la fois.
## Étape 1 : Configurer le répertoire
Avant de travailler avec des fichiers, vous devez configurer le répertoire dans lequel vous allez enregistrer le fichier Excel. Cela permet de garantir que vos fichiers sont bien organisés et stockés en toute sécurité.
```csharp
// Définissez le chemin d'accès à votre répertoire de documents
string dataDir = "Your Document Directory";
// Vérifiez si le répertoire existe, sinon créez-le
bool isExists = Directory.Exists(dataDir);
if (!isExists)
{
    Directory.CreateDirectory(dataDir);
}
```
Cette partie du code garantit que votre répertoire est prêt pour les opérations sur les fichiers. Considérez-la comme la pose des bases de tout ce qui suit.
## Étape 2 : Initialiser le classeur et la feuille de calcul
Maintenant, passons à la création d’un nouveau classeur et à l’accès à sa feuille de calcul par défaut.
```csharp
// Initialiser un nouveau classeur
Workbook book = new Workbook();
// Accéder à la première feuille de calcul du classeur
Worksheet sheet = book.Worksheets[0];
```
Ici, nous initialisons un classeur Excel et sélectionnons la première feuille de calcul qu'il contient. Cette feuille de calcul sera la zone de travail sur laquelle nous appliquerons nos paramètres de protection et définirons les plages modifiables.
## Étape 3 : Accéder à la collection Autoriser la modification des plages
 Aspose.Cells possède une fonctionnalité appelée`AllowEditRanges`, qui est une collection de plages modifiables, même lorsque la feuille de calcul est protégée.
```csharp
// Accéder à la collection Autoriser les plages de modification
ProtectedRangeCollection allowRanges = sheet.AllowEditRanges;
```
Cette ligne définit l'accès à un ensemble spécial de plages qui seront modifiables. Considérez-la comme une zone « VIP » dans votre feuille de calcul, où seules des plages spécifiques sont autorisées à contourner la protection.
## Étape 4 : Définir et créer une plage protégée
Maintenant, définissons et créons une plage protégée dans notre feuille de calcul. Nous allons spécifier les cellules de début et de fin de cette plage.
```csharp
// Définir une variable ProtectedRange
ProtectedRange protectedRange;
// Ajouter une nouvelle plage à la collection avec un nom et des positions de cellule spécifiques
int idx = allowRanges.Add("EditableRange", 1, 1, 3, 3);
protectedRange = allowRanges[idx];
```
Dans ce bloc de code :
- `EditableRange` est le nom attribué à la plage.
- Les nombres (1, 1, 3, 3) définissent les coordonnées de la plage, ce qui signifie qu'elle commence à partir de la cellule B2 (ligne 1, colonne 1) jusqu'à la cellule D4 (ligne 3, colonne 3).
## Étape 5 : définir un mot de passe pour la plage protégée
Pour plus de sécurité, vous pouvez définir un mot de passe pour la plage protégée. Cette étape ajoute une couche de protection supplémentaire pour garantir que seuls les utilisateurs autorisés peuvent modifier la plage.
```csharp
// Définir un mot de passe pour la plage modifiable
protectedRange.Password = "123";
```
Ici, nous avons ajouté un mot de passe (`"123"`) à la plage protégée. Cette exigence de mot de passe fournit un niveau de contrôle supplémentaire sur qui peut apporter des modifications.
## Étape 6 : Protégez la feuille de calcul
Une fois notre plage modifiable définie, l'étape suivante consiste à protéger l'intégralité de la feuille de calcul. Ce paramètre de protection garantit que toutes les cellules situées en dehors de la plage définie sont verrouillées et non modifiables.
```csharp
// Appliquer une protection à la feuille de calcul, rendant toutes les autres cellules non modifiables
sheet.Protect(ProtectionType.All);
```
 Le`Protect`La méthode verrouille l'intégralité de la feuille de calcul, à l'exception des plages que nous avons définies comme modifiables. Cette étape crée essentiellement un environnement sécurisé en « lecture seule », avec accès à des cellules spécifiques selon les besoins.
## Étape 7 : Enregistrer le classeur
L’étape finale consiste à enregistrer le classeur afin que vos paramètres soient appliqués et stockés.
```csharp
// Enregistrez le fichier Excel dans le répertoire spécifié
book.Save(dataDir + "protectedrange.out.xls");
```
Dans cette étape, nous enregistrons notre classeur sous le nom « protectedrange.out.xls » dans le répertoire que nous avons configuré à l’étape 1. Vous disposez désormais d’un fichier Excel entièrement fonctionnel et sécurisé dans lequel seules des plages spécifiques sont modifiables !
## Conclusion
Aspose.Cells pour .NET offre un excellent moyen de gérer la protection et les autorisations au sein de vos fichiers Excel. En créant des plages modifiables, vous pouvez sécuriser vos feuilles de calcul tout en permettant à des zones spécifiques de rester accessibles. Cette fonctionnalité est particulièrement utile pour les documents collaboratifs, où seules quelques cellules doivent être ouvertes pour modification tandis que les autres restent verrouillées.
## FAQ
### Puis-je ajouter plusieurs plages modifiables à une feuille de calcul ?
Oui, vous pouvez ajouter plusieurs plages en répétant simplement la`allowRanges.Add()` méthode pour chaque nouvelle gamme.
### Que faire si je souhaite supprimer une plage protégée ultérieurement ?
 Utilisez le`allowRanges.RemoveAt()` méthode avec l'index de la plage que vous souhaitez supprimer.
### Puis-je définir des mots de passe différents pour chaque plage ?
 Absolument. Chacun`ProtectedRange` peut avoir son propre mot de passe unique, vous donnant un contrôle précis.
### Que se passe-t-il si je protège la feuille de calcul sans aucune plage modifiable ?
Si vous ne définissez pas de plages modifiables, la feuille de calcul entière ne sera pas modifiable une fois protégée.
### La plage protégée est-elle visible par les autres utilisateurs ?
Non, la protection est interne. Les utilisateurs ne seront invités à saisir un mot de passe que s'ils tentent de modifier la zone protégée.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
