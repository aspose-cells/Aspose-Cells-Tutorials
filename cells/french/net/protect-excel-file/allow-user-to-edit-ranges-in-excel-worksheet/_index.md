---
title: Autoriser l'utilisateur à modifier les plages dans la feuille de calcul Excel
linktitle: Autoriser l'utilisateur à modifier les plages dans la feuille de calcul Excel
second_title: Référence de l'API Aspose.Cells pour .NET
description: Autorisez les utilisateurs à modifier des plages spécifiques dans une feuille de calcul Excel à l'aide d'Aspose.Cells pour .NET. Guide étape par étape avec code source en C#.
weight: 10
url: /fr/net/protect-excel-file/allow-user-to-edit-ranges-in-excel-worksheet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Autoriser l'utilisateur à modifier les plages dans la feuille de calcul Excel

## Introduction

Lorsqu'il s'agit de travailler avec des feuilles de calcul Excel, la flexibilité est souvent essentielle, en particulier lorsque plusieurs utilisateurs doivent accéder à des zones spécifiques pour modifier sans compromettre l'intégrité des données de la feuille entière. C'est là qu'Aspose.Cells pour .NET brille ! Dans ce didacticiel, nous allons découvrir comment permettre aux utilisateurs de modifier certaines plages dans une feuille de calcul Excel tout en protégeant le reste du document. À la fin de cet article, vous comprendrez non seulement les concepts, mais vous disposerez également d'un exemple concret avec lequel travailler. 

## Prérequis

Avant de passer aux choses sérieuses, assurons-nous que vous disposez de tout ce dont vous avez besoin pour commencer :

1. Environnement de développement .NET : vous devez disposer d’un environnement de développement .NET fonctionnel configuré (il peut s’agir de Visual Studio ou de tout autre IDE de votre choix).
2.  Bibliothèque Aspose.Cells pour .NET : Téléchargez et installez la bibliothèque Aspose.Cells. Vous pouvez la trouver[ici](https://releases.aspose.com/cells/net/).
3. Connaissances de base de C# : la familiarité avec la programmation C# vous aidera à parcourir facilement les exemples de code.
4. Comprendre les bases d'Excel : connaître le fonctionnement d'Excel fournira une base pour les fonctionnalités dont nous allons parler.

Une fois ces prérequis triés, vous êtes prêt à partir !

## Paquets d'importation

Avant de commencer à coder, nous devons nous assurer que notre projet reconnaît l'espace de noms Aspose.Cells. Voici comment importer les packages nécessaires :

```csharp
using System.IO;
using Aspose.Cells;
```

Maintenant que nous avons importé ce dont nous avons besoin, plongeons dans notre tutoriel étape par étape.

## Étape 1 : Configurer le répertoire de documents

Pour toute opération sur les fichiers, il est essentiel de définir un emplacement où nos documents seront enregistrés. Configurons notre répertoire de travail pour stocker les fichiers Excel.

```csharp
// Le chemin vers le répertoire des documents.
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Créez un répertoire s'il n'est pas déjà présent.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```

 Tout d’abord, remplacez`"YOUR DOCUMENT DIRECTORY"` avec le chemin où vous souhaitez que vos fichiers soient enregistrés. Ce code vérifie si le répertoire existe ; si ce n'est pas le cas, il en crée un.

## Étape 2 : créer un nouveau classeur

Notre répertoire de travail étant prêt, il est temps de créer notre classeur Excel. 

```csharp
// Instancier un nouveau classeur
Workbook book = new Workbook();
```

 Ici, nous créons une nouvelle instance du`Workbook` classe fournie par Aspose.Cells, qui nous permet de manipuler le fichier Excel.

## Étape 3 : Accéder à la feuille de calcul par défaut

Chaque classeur nouvellement créé est accompagné d'au moins une feuille de calcul. Accédons-y.

```csharp
// Obtenir la première feuille de calcul (par défaut)
Worksheet sheet = book.Worksheets[0];
```

Dans cet extrait de code, nous accédons à la première feuille de calcul de notre classeur, que nous manipulerons dans les étapes suivantes.

## Étape 4 : Obtenir l'autorisation de modifier les plages

 Pour activer des plages spécifiques de la feuille de calcul pour l'édition, nous devons accéder à l'`AllowEditRanges` propriété.

```csharp
// Obtenir les plages de modification autorisées
ProtectedRangeCollection allowRanges = sheet.AllowEditRanges;
```

Cette collection nous permettra de gérer quelles plages sont modifiables dans notre feuille de calcul.

## Étape 5 : Définir la plage protégée

Ensuite, définissons quelle partie de la feuille de calcul nous voulons protéger tout en autorisant les modifications sur une plage spécifiée.

```csharp
// Définir ProtectedRange
ProtectedRange proteced_range;

// Créer la gamme
int idx = allowRanges.Add("r2", 1, 1, 3, 3);
proteced_range = allowRanges[idx];

// Spécifier le mot de passe
proteced_range.Password = "123";
```

Dans cette étape, nous ajoutons une nouvelle plage modifiable appelée « r2 » qui permet d'effectuer des modifications dans les cellules de la ligne 1, colonne 1 à la ligne 3, colonne 3. De plus, nous définissons un mot de passe pour protéger cette plage, garantissant que seuls les utilisateurs autorisés peuvent la modifier.

## Étape 6 : Protégez la feuille de calcul

Maintenant que nous avons configuré notre plage modifiable, nous devons protéger la feuille de calcul.

```csharp
// Protégez la feuille
sheet.Protect(ProtectionType.All);
```

Ce code protégera l’intégralité de la feuille de calcul de toute modification indésirable, à l’exception de la plage que nous venons de spécifier.

## Étape 7 : Enregistrer le fichier Excel

Enregistrons le classeur afin que nous puissions voir nos modifications reflétées dans un fichier Excel.

```csharp
// Enregistrer le fichier Excel
book.Save(dataDir + "protectedrange.out.xls");
```

Assurez-vous d'ajuster le nom du fichier selon vos besoins. Cela créera un fichier Excel dans le répertoire spécifié avec les paramètres que nous avons configurés.

## Conclusion

Et voilà ! Vous avez réussi à créer une feuille de calcul Excel qui limite les modifications à une plage désignée tout en protégeant le reste de la feuille. L'utilisation d'Aspose.Cells pour .NET rend la gestion de ce type de tâches beaucoup plus simple et efficace. Que vous développiez une application complexe ou que vous ayez simplement besoin de gérer des données de manière sécurisée, ces fonctionnalités peuvent améliorer considérablement votre flux de travail.

## FAQ

### Qu'est-ce qu'Aspose.Cells ?
Aspose.Cells est une puissante bibliothèque .NET pour la gestion des fichiers Excel, offrant des fonctionnalités telles que la création, l'édition et la conversion de feuilles de calcul par programmation.

### Puis-je appliquer plusieurs plages modifiables ?
 Absolument ! Vous pouvez appeler le`Add` méthode sur le`allowRanges` collectionner plusieurs fois pour spécifier plusieurs plages modifiables.

### Que se passe-t-il si j'oublie le mot de passe ?
Malheureusement, si vous oubliez le mot de passe d'une plage modifiable, vous devrez supprimer la protection ou accéder au fichier d'une manière prédéfinie qui peut impliquer des informations d'identification.

### Existe-t-il une version gratuite d'Aspose.Cells ?
Oui, Aspose propose un essai gratuit que vous pouvez utiliser pour explorer les fonctionnalités avant d'acheter.

### Où puis-je trouver plus d'informations sur Aspose.Cells ?
 Vous pouvez vérifier le[documentation](https://reference.aspose.com/cells/net/)pour des guides et des références détaillés.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
