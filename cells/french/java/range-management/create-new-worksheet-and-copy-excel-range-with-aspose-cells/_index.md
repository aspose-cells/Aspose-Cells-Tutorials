---
category: general
date: 2026-09-11
description: Créer une nouvelle feuille de calcul et copier une plage Excel à l'aide
  d'Aspose.Cells. Apprenez comment copier une plage entre les feuilles tout en préservant
  les tableaux croisés dynamiques.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create new worksheet
- copy excel range
- copy range between sheets
- copy range aspose.cells
language: fr
lastmod: 2026-09-11
og_description: Créer une nouvelle feuille de calcul et copier une plage Excel avec
  Aspose.Cells. Ce tutoriel montre les étapes exactes pour copier une plage entre
  les feuilles tout en conservant les tableaux croisés dynamiques intacts.
og_image_alt: Screenshot of a Java IDE showing code that creates a new worksheet and
  copies an Excel range
og_title: Créer une nouvelle feuille de calcul et copier une plage Excel – Guide Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-09-11'
  description: Create new worksheet and copy Excel range using Aspose.Cells. Learn
    how to copy range between sheets while preserving pivot tables.
  headline: Create new worksheet and copy Excel range with Aspose.Cells
  type: TechArticle
- questions:
  - answer: The `copy` method also copies merge information, so merged cells appear
      unchanged on the destination sheet.
    question: What if the source range contains merged cells?
  - answer: Yes. Load a second `Workbook` instance, create a destination range in
      that workbook, and call `sourceRange.copy(destinationRange)`. The method handles
      cross‑workbook copying automatically.
    question: Can I copy to a different workbook?
  - answer: The copy operation overwrites any existing cells that intersect the destination
      range. To avoid data loss, ensure the destination area is empty or use a different
      start cell (e.g., `"B2"`).
    question: What if the destination sheet already has data?
  - answer: Aspose.Cells reuses the original pivot cache, which means the new pivot
      table remains linked to the same source data. If you need an independent cache,
      you must recreate the pivot table after copying.
    question: Is the pivot cache duplicated?
  type: FAQPage
tags:
- Aspose.Cells
- Excel automation
- Java
title: Créer une nouvelle feuille de calcul et copier une plage Excel avec Aspose.Cells
url: /fr/java/range-management/create-new-worksheet-and-copy-excel-range-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer une nouvelle feuille de calcul et copier une plage Excel avec Aspose.Cells

Si vous devez **créer une nouvelle feuille de calcul** et déplacer des données dans un fichier Excel, Aspose.Cells rend cela simple. Ce guide montre exactement comment copier une plage Excel d’une feuille à une autre tout en préservant les tableaux croisés dynamiques présents dans la plage.

Vous apprendrez comment **copier une plage Excel**, comment **copier une plage entre feuilles**, et pourquoi la méthode `copy` d’Aspose.Cells conserve les définitions des tableaux croisés dynamiques intactes. Aucun outil externe n’est requis — juste un projet Java avec la bibliothèque Aspose.Cells.

## Prérequis

- Java 17 ou version ultérieure installé
- Aspose.Cells pour Java (version 23.12 ou plus récente) ajouté au classpath de votre projet
- Un classeur source (`input.xlsx`) contenant un tableau croisé dynamique dans la plage que vous souhaitez copier
- Une connaissance de base de la syntaxe Java et de la gestion des dépendances Maven/Gradle

## Étape 1 : Configurer le projet et importer Aspose.Cells

Créez un projet Maven simple (ou Gradle, si vous préférez) et ajoutez la dépendance Aspose.Cells :

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
</dependency>
```

Ensuite, importez les classes requises dans votre fichier source Java :

```java
import com.aspose.cells.*;
import java.io.IOException;
```

*Pourquoi cette étape est importante* : L’importation des classes correctes vous donne accès à `Workbook`, `Worksheet`, `Range` et à la méthode `copy` qui gérera le transfert de la plage.

## Étape 2 : Charger le classeur source

Ouvrez le classeur qui contient les données que vous souhaitez copier. Le code suivant charge `input.xlsx` depuis un répertoire que vous spécifiez :

```java
public class ExcelRangeCopy {
    public static void main(String[] args) throws IOException {
        // Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

*Explication* : `Workbook` représente le fichier Excel complet. Le charger une fois vous donne un accès en lecture/écriture à chaque feuille et à la collection de cellules.

## Étape 3 : Identifier la plage source qui inclut le tableau croisé dynamique

Sélectionnez la feuille qui contient le tableau croisé dynamique et définissez le bloc de cellules exact que vous souhaitez copier. Dans cet exemple, nous copions les cellules A1 à D20 :

```java
        // Get the first worksheet (index 0) that contains the pivot table
        Worksheet sourceSheet = workbook.getWorksheets().get(0);

        // Define the source range – this range includes the pivot table
        Range sourceRange = sourceSheet.getCells().createRange("A1:D20");
```

*Pourquoi c’est important* : En créant un objet `Range`, vous indiquez à Aspose.Cells exactement quelles cellules (y compris les objets intégrés comme les tableaux croisés dynamiques) doivent être dupliquées.

## Étape 4 : **Créer une nouvelle feuille de calcul** qui recevra les données copiées

Nous ajoutons maintenant une nouvelle feuille au même classeur. C’est à ce moment que le mot‑clé principal apparaît :

```java
        // Create a new worksheet named "Copy"
        Worksheet destinationSheet = workbook.getWorksheets().add("Copy");

        // Define the top‑left cell of the destination range
        Range destinationRange = destinationSheet.getCells().createRange("A1");
```

*Explication* : Ajouter une nouvelle feuille isole les données copiées, ce qui facilite la vérification que l’opération **copy excel range** a réussi sans affecter la feuille originale.

## Étape 5 : Copier la plage – le tableau croisé dynamique est préservé automatiquement

Utilisez la méthode `copy` pour déplacer la plage de la feuille source vers la feuille de destination. Aspose.Cells copie les formules, le formatage et les définitions des tableaux croisés dynamiques :

```java
        // Copy the range – the pivot table inside the range is preserved
        sourceRange.copy(destinationRange);
```

*Pourquoi cela fonctionne* : La méthode `copy` effectue une copie profonde des cellules sources. Elle ne copie pas seulement les valeurs ; elle réplique toute la structure des cellules, y compris le cache du tableau croisé dynamique. C’est pourquoi vous pouvez **copy range aspose.cells** et voir toujours un tableau croisé dynamique fonctionnel sur la nouvelle feuille.

## Étape 6 : Enregistrer le classeur avec la nouvelle feuille de calcul

Enfin, écrivez le classeur modifié sur le disque :

```java
        // Save the workbook with the copied data
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

*Résultat* : `output.xlsx` contient maintenant la feuille originale ainsi qu’une nouvelle feuille nommée **Copy** qui possède exactement la même plage, tableau croisé dynamique inclus.

## Exemple complet fonctionnel

En assemblant tous les éléments, voici le programme complet et exécutable :

```java
import com.aspose.cells.*;
import java.io.IOException;

public class ExcelRangeCopy {
    public static void main(String[] args) throws IOException {
        // Step 1: Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Step 2: Get the worksheet that contains the pivot table and define the source range
        Worksheet sourceSheet = workbook.getWorksheets().get(0);
        Range sourceRange = sourceSheet.getCells().createRange("A1:D20");

        // Step 3: Create a new worksheet that will receive the copied range
        Worksheet destinationSheet = workbook.getWorksheets().add("Copy");
        Range destinationRange = destinationSheet.getCells().createRange("A1");

        // Step 4: Copy the range – the pivot table inside the range is preserved
        sourceRange.copy(destinationRange);

        // Step 5: Save the workbook with the copied data
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

**Sortie attendue** : Ouvrez `output.xlsx` dans Excel. Vous verrez une feuille nommée **Copy** dont les cellules A1:D20 contiennent les mêmes données, le même formatage et un tableau croisé dynamique actif identique à l’original.

## Questions fréquentes et cas particuliers

- **Et si la plage source contient des cellules fusionnées ?**  
  La méthode `copy` copie également les informations de fusion, de sorte que les cellules fusionnées restent inchangées sur la feuille de destination.

- **Puis-je copier vers un classeur différent ?**  
  Oui. Chargez une seconde instance de `Workbook`, créez une plage de destination dans ce classeur, et appelez `sourceRange.copy(destinationRange)`. La méthode gère automatiquement la copie entre classeurs.

- **Et si la feuille de destination contient déjà des données ?**  
  L’opération de copie écrase toutes les cellules existantes qui intersectent la plage de destination. Pour éviter la perte de données, assurez‑vous que la zone de destination est vide ou utilisez une cellule de départ différente (par ex., `"B2"`).

- **Le cache du tableau croisé dynamique est‑il dupliqué ?**  
  Aspose.Cells réutilise le cache original, ce qui signifie que le nouveau tableau croisé dynamique reste lié aux mêmes données source. Si vous avez besoin d’un cache indépendant, vous devez recréer le tableau croisé dynamique après la copie.

## Astuces et bonnes pratiques

- **Astuce pro** : Utilisez `Workbook.setForceFormulaRecalculation(true)` avant d’enregistrer si votre plage contient des formules dépendant de données situées en dehors du bloc copié.
- **Attention aux** grandes plages : copier des feuilles massives peut consommer beaucoup de mémoire. Envisagez de copier par morceaux plus petits si vous rencontrez une `OutOfMemoryError`.
- **Astuce de performance** : Désactivez la mise à jour de l’écran (`workbook.getSettings().setCalculateFormulaOnOpen(false)`) lorsque vous travaillez avec des fichiers très volumineux afin d’accélérer le processus de copie.

## Conclusion

Vous savez maintenant comment **créer une nouvelle feuille de calcul** et **copier une plage Excel** entre feuilles en utilisant Aspose.Cells, en préservant les tableaux croisés dynamiques et toutes les attributs des cellules. Cette technique vous permet de dupliquer programmétiquement des blocs de données, de créer des modèles de rapports ou de restructurer des classeurs sans copier‑coller manuel.

Ensuite, explorez les sujets connexes tels que **copy range aspose.cells** pour les opérations entre classeurs, l’automatisation du rafraîchissement des tableaux croisés dynamiques, ou l’exportation de la feuille copiée en PDF. Expérimentez avec différentes plages sources et noms de feuilles pour répondre à votre scénario d’automatisation spécifique. Bon codage !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités supplémentaires de l’API et à explorer des approches d’implémentation alternatives dans vos propres projets.

- [Copier des formes entre feuilles Excel avec Aspose.Cells pour .NET : Guide complet](/cells/english/net/images-shapes/copy-shapes-between-sheets-aspose-cells-dotnet/)
- [Copier des images entre feuilles dans Excel avec Aspose.Cells pour Java : Guide complet](/cells/english/java/images-shapes/copy-images-between-sheets-excel-aspose-cells-java/)
- [Excel Aspose Cells .NET Copier des données de plage](/cells/hindi/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}