---
title: Implémenter l'en-tête et le pied de page dans la feuille de calcul
linktitle: Implémenter l'en-tête et le pied de page dans la feuille de calcul
second_title: API de traitement Excel Aspose.Cells .NET
description: Découvrez comment configurer des en-têtes et des pieds de page dans des feuilles de calcul Excel à l'aide d'Aspose.Cells pour .NET avec un didacticiel étape par étape, des exemples pratiques et des conseils utiles.
weight: 22
url: /fr/net/worksheet-page-setup-features/implement-header-and-footer/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Implémenter l'en-tête et le pied de page dans la feuille de calcul

## Introduction

Lorsque vous travaillez avec des feuilles de calcul Excel, les en-têtes et les pieds de page jouent un rôle essentiel dans la diffusion d'informations contextuelles importantes, telles que les noms de fichiers, les dates ou les numéros de page, à votre public. Que vous automatisiez des rapports ou que vous génériez des fichiers dynamiques, Aspose.Cells pour .NET simplifie la personnalisation des en-têtes et des pieds de page dans les feuilles de calcul par programmation. Ce guide présente une approche complète, étape par étape, pour ajouter des en-têtes et des pieds de page avec Aspose.Cells pour .NET, donnant à vos fichiers Excel un aspect plus soigné et plus professionnel.

## Prérequis

Avant de commencer, assurez-vous de disposer des éléments suivants :

1.  Aspose.Cells pour .NET : vous aurez besoin d'Aspose.Cells pour .NET installé.[Téléchargez-le ici](https://releases.aspose.com/cells/net/).
2. Configuration de l'IDE : Visual Studio (ou votre IDE préféré) avec .NET Framework installé.
3.  Licence : Bien que vous puissiez commencer avec l'essai gratuit, l'obtention d'une licence complète ou temporaire débloquera tout le potentiel d'Aspose.Cells.[Obtenir un permis temporaire](https://purchase.aspose.com/temporary-license/).

La documentation d'Aspose.Cells est une ressource pratique pour référence tout au long de ce processus. Vous pouvez la trouver[ici](https://reference.aspose.com/cells/net/).

## Importation de paquets

Dans votre projet, importez les espaces de noms requis :

```csharp
using System.IO;
using Aspose.Cells;
using System;
```

En important ce package, vous aurez accès aux classes et méthodes nécessaires pour travailler avec les en-têtes, les pieds de page et d'autres fonctionnalités Excel dans Aspose.Cells.

Dans ce guide, nous décomposerons chaque étape afin que vous puissiez facilement suivre, même si vous êtes nouveau sur Aspose.Cells ou .NET.

## Étape 1 : Configurez votre classeur et la mise en page

Tout d'abord, créez un nouveau classeur et accédez à la mise en page de la feuille de calcul. Vous disposerez ainsi des outils nécessaires pour modifier l'en-tête et le pied de page de la feuille de calcul.

```csharp
// Définissez le chemin pour enregistrer votre document
string dataDir = "Your Document Directory";

// Instancier un objet Workbook
Workbook excel = new Workbook();
```

 Ici, nous avons créé un`Workbook` objet, qui représente notre fichier Excel.`PageSetup` de la feuille de calcul est l'endroit où nous pouvons modifier les options d'en-tête et de pied de page.


## Étape 2 : Accéder aux propriétés de la feuille de calcul et de la mise en page

 Dans Aspose.Cells, chaque feuille de calcul a une`PageSetup`propriété qui contrôle les fonctionnalités de mise en page, y compris les en-têtes et les pieds de page. Obtenons le`PageSetup` objet pour notre feuille de travail.

```csharp
// Obtenir la référence à la mise en page de la première feuille de calcul
PageSetup pageSetup = excel.Worksheets[0].PageSetup;
```

 Avec cela,`pageSetup` contient désormais tous les paramètres nécessaires pour personnaliser les en-têtes et les pieds de page.


## Étape 3 : définir la section gauche de l'en-tête

Les en-têtes dans Excel sont divisés en trois sections : gauche, centre et droite. Commençons par définir la section de gauche pour afficher le nom de la feuille de calcul.

```csharp
// Définir le nom de la feuille de calcul dans la section gauche de l'en-tête
pageSetup.SetHeader(0, "&A");
```

 En utilisant`&A` vous permet d'afficher dynamiquement le nom de la feuille de calcul. Ceci est particulièrement utile si vous avez plusieurs feuilles dans un classeur et que vous souhaitez que chaque en-tête reflète le titre de sa feuille.


## Étape 4 : ajouter la date et l’heure au centre de l’en-tête

Ensuite, ajoutons la date et l'heure actuelles dans la section centrale de l'en-tête. De plus, nous utiliserons une police personnalisée pour le style.

```csharp
// Définissez la date et l'heure dans la section centrale de l'en-tête avec une police en gras
pageSetup.SetHeader(1, "&\"Times New Roman,Bold\"&D-&T");
```

Dans ce code :
- `&D`insère la date du jour.
- `&T` insère l'heure actuelle.
- `"Times New Roman,Bold"` applique Times New Roman en gras à ces éléments.


## Étape 5 : Afficher le nom du fichier dans la partie droite de l'en-tête

Pour compléter l'en-tête, affichons le nom du fichier sur le côté droit, ainsi qu'un ajustement de police.

```csharp
// Afficher le nom du fichier dans la section droite de l'en-tête avec une taille de police personnalisée
pageSetup.SetHeader(2, "&\"Times New Roman,Bold\"&12&F");
```

- `&F` représente le nom du fichier, indiquant clairement à quel fichier appartiennent les pages imprimées.
- `&12` modifie la taille de la police à 12 pour cette section.


## Étape 6 : ajouter du texte avec une police personnalisée à la section du pied de page gauche

Passons maintenant aux pieds de page ! Nous commencerons par configurer la section de pied de page gauche avec un texte personnalisé et un style de police spécifié.

```csharp
// Ajoutez un texte personnalisé avec un style de police dans la section gauche du pied de page
pageSetup.SetFooter(0, "Hello World! &\"Courier New\"&14 123");
```

 Le`&\"Courier New\"&14` le paramètre dans le code ci-dessus applique la police « Courier New » avec la taille 14 au texte spécifié (`123`). Le reste du texte reste dans la police de pied de page par défaut.


## Étape 7 : insérer le numéro de page au centre du pied de page

Inclure des numéros de page dans le pied de page est un excellent moyen d’aider les lecteurs à suivre des documents de plusieurs pages.

```csharp
// Insérer le numéro de page dans la section centrale du pied de page
pageSetup.SetFooter(1, "&P");
```

 Ici,`&P` ajoute le numéro de page actuel à la section centrale du pied de page. C'est un petit détail, mais crucial pour des documents d'aspect professionnel.


## Étape 8 : Afficher le nombre total de pages dans la section de pied de page de droite

Enfin, complétons le pied de page en affichant le nombre total de pages dans la section de droite.

```csharp
// Afficher le nombre total de pages dans la section droite du pied de page
pageSetup.SetFooter(2, "&N");
```

- `&N` fournit le nombre total de pages, permettant aux lecteurs de savoir quelle est la longueur du document.


## Étape 9 : Enregistrer le classeur

Une fois que vous avez configuré vos en-têtes et pieds de page, il est temps d'enregistrer le classeur. Il s'agit de l'étape finale pour générer un fichier Excel avec des en-têtes et pieds de page entièrement personnalisés.

```csharp
// Enregistrer le classeur
excel.Save(dataDir + "SetHeadersAndFooters_out.xls");
```

Cette ligne enregistre le fichier dans votre répertoire désigné avec les en-têtes et pieds de page personnalisés en place.


## Conclusion

L'ajout d'en-têtes et de pieds de page aux feuilles de calcul Excel est une compétence précieuse pour créer des documents organisés et professionnels. Avec Aspose.Cells pour .NET, vous avez un contrôle total sur les en-têtes et les pieds de page de vos fichiers Excel, de l'affichage du nom de la feuille de calcul à l'insertion de texte personnalisé, de date, d'heure et même de numéros de page dynamiques. Maintenant que vous avez vu chaque étape en action, vous pouvez faire passer votre automatisation Excel au niveau supérieur.

## FAQ

### Puis-je utiliser différentes polices pour différentes sections d’en-têtes et de pieds de page ?  
Oui, Aspose.Cells pour .NET vous permet de spécifier les polices pour chaque section de l'en-tête et du pied de page à l'aide de balises de police spécifiques.

### Comment supprimer les en-têtes et les pieds de page ?  
 Vous pouvez effacer les en-têtes et les pieds de page en définissant le texte de l'en-tête ou du pied de page sur une chaîne vide avec`SetHeader` ou`SetFooter`.

### Puis-je insérer des images dans les en-têtes ou les pieds de page avec Aspose.Cells pour .NET ?  
Actuellement, Aspose.Cells prend principalement en charge le texte dans les en-têtes et les pieds de page. Les images peuvent nécessiter une solution de contournement, comme l'insertion d'images dans la feuille de calcul elle-même.

### Aspose.Cells prend-il en charge les données dynamiques dans les en-têtes et les pieds de page ?  
 Oui, vous pouvez utiliser différents codes dynamiques (comme`&D` pour la date ou`&P` (pour le numéro de page) pour ajouter du contenu dynamique.

### Comment puis-je ajuster la hauteur de l’en-tête ou du pied de page ?  
 Aspose.Cells fournit des options dans le`PageSetup` classe pour ajuster les marges d'en-tête et de pied de page, vous donnant le contrôle de l'espacement.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
