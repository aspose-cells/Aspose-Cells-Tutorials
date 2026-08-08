---
category: general
date: 2026-08-08
description: Comment copier un tableau croisé dynamique dans Aspose.Cells et copier
  une plage dans le classeur en utilisant Java. Découvrez les étapes exactes pour
  dupliquer un tableau croisé dynamique avec CopyOptions.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot
- copy range to workbook
- aspose.cells copy range
language: fr
lastmod: 2026-08-08
og_description: Comment copier un tableau croisé dynamique dans Aspose.Cells et copier
  une plage dans le classeur avec Java. Suivez ce guide complet pour dupliquer un
  tableau croisé dynamique à l’aide de CopyOptions.
og_image_alt: Diagram showing how to copy pivot in Aspose.Cells
og_title: Comment copier un tableau croisé dynamique dans Aspose.Cells – copier une
  plage vers le classeur
schemas:
- author: Aspose
  dateModified: '2026-08-08'
  description: How to copy pivot in Aspose.Cells and copy range to workbook using
    Java. Learn the exact steps to duplicate a pivot table with CopyOptions.
  headline: How to copy pivot in Aspose.Cells – copy range to workbook
  type: TechArticle
- description: How to copy pivot in Aspose.Cells and copy range to workbook using
    Java. Learn the exact steps to duplicate a pivot table with CopyOptions.
  name: How to copy pivot in Aspose.Cells – copy range to workbook
  steps:
  - name: Add Aspose.Cells to your project
    text: 'If you use Maven, add the following dependency to your `pom.xml`:'
  - name: Load the source workbook
    text: '```java import com.aspose.cells.*;'
  - name: Configure copy options to include the pivot table
    text: '```java // Define copy options to include the pivot table in the copied
      range CopyOptions copyOptions = new CopyOptions() .setCopyPivotTable(true);
      ```'
  - name: Copy the desired range with the pivot table
    text: '```java // Copy the range A1:H20, preserving the pivot table workbook.getWorksheets().get(0).getCells()
      .copyRange("A1:H20", copyOptions); ```'
  - name: Save the modified workbook
    text: '```java // Save the workbook with the copied pivot table workbook.save("YOUR_DIRECTORY/output.xlsx");
      } } ```'
  - name: Expected result
    text: '* `output.xlsx` contains the same data as `input.xlsx`. * The pivot table
      that originally occupied the source range appears in the destination cells,
      fully functional (filters, refresh capability, etc.). * All cell formatting,
      formulas, and column widths are preserved because `copyRange` copies the '
  type: HowTo
tags:
- Aspose.Cells
- Java
- PivotTable
- CopyRange
title: Comment copier un tableau croisé dynamique dans Aspose.Cells – copier la plage
  vers le classeur
url: /fr/java/excel-pivot-tables/how-to-copy-pivot-in-aspose-cells-copy-range-to-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment copier un tableau croisé dynamique dans Aspose.Cells – copier une plage vers le classeur

Si vous avez besoin de **how to copy pivot** dans un fichier Excel en utilisant Aspose.Cells, ce guide vous montre le processus exact. À la fin du tutoriel, vous serez capable de **copy range to workbook** tout en préservant la définition du tableau croisé dynamique.

L'exemple utilise Java, mais les mêmes concepts s'appliquent à tout langage .NET fonctionnant avec Aspose.Cells. Aucun outil externe n'est requis — seulement la bibliothèque Aspose.Cells for Java et un environnement de développement basique.

## Prérequis

Avant de commencer, assurez‑vous d'avoir :

* Java Development Kit (JDK) 8 ou version ultérieure.
* Maven ou Gradle pour gérer les dépendances (l'exemple utilise Maven).
* Aspose.Cells for Java 23.9 (ou la dernière version) ajouté à votre projet.
* Un classeur d'entrée (`input.xlsx`) contenant au moins un tableau croisé dynamique sur la première feuille.

Avoir ces éléments prêts évite les erreurs d'exécution lorsque le code accède au classeur.

## Comment copier un tableau croisé dynamique avec Aspose.Cells

Cette section décrit chaque étape nécessaire pour **how to copy pivot** d'une partie d'une feuille à une autre, en utilisant la classe `CopyOptions`.

### Étape 1 : Ajouter Aspose.Cells à votre projet

Si vous utilisez Maven, ajoutez la dépendance suivante à votre `pom.xml` :

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier> <!-- adjust JDK version as needed -->
</dependency>
```

*Pourquoi cette étape est importante* : La bibliothèque fournit les classes `Workbook`, `CopyOptions` et d'autres nécessaires aux opérations **aspose.cells copy range**. Sans la dépendance, le compilateur ne peut pas résoudre ces types.

### Étape 2 : Charger le classeur source

```java
import com.aspose.cells.*;

public class CopyPivotTableRange {
    public static void main(String[] args) throws Exception {
        // Load the workbook that contains the pivot table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

Le chargement du fichier crée une représentation en mémoire du tableau. L'objet `Workbook` vous donne accès aux feuilles de calcul, aux cellules et aux tableaux croisés dynamiques.

### Étape 3 : Configurer les options de copie pour inclure le tableau croisé dynamique

```java
        // Define copy options to include the pivot table in the copied range
        CopyOptions copyOptions = new CopyOptions()
                .setCopyPivotTable(true);
```

`CopyOptions.setCopyPivotTable(true)` indique à Aspose.Cells que l'opération doit préserver les métadonnées du tableau croisé dynamique. Si vous omettez ce drapeau, le tableau croisé dynamique serait réduit à des données statiques, perdant son interactivité.

### Étape 4 : Copier la plage souhaitée avec le tableau croisé dynamique

```java
        // Copy the range A1:H20, preserving the pivot table
        workbook.getWorksheets().get(0).getCells()
                .copyRange("A1:H20", copyOptions);
```

La méthode `copyRange` copie les cellules, le formatage et — grâce aux options définies à l'étape précédente — tous les tableaux croisés dynamiques qui intersectent la plage. C'est le cœur de la fonctionnalité **copy range to workbook**.

### Étape 5 : Enregistrer le classeur modifié

```java
        // Save the workbook with the copied pivot table
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

L'enregistrement écrit les modifications dans un nouveau fichier (`output.xlsx`). Vous pouvez maintenant ouvrir ce fichier dans Excel et constater que le tableau croisé dynamique a été dupliqué exactement à l'endroit où la plage a été copiée.

## Exemple complet et exécutable

En assemblant toutes les pièces, voici le programme complet que vous pouvez compiler et exécuter :

```java
import com.aspose.cells.*;

public class CopyPivotTableRange {
    public static void main(String[] args) throws Exception {
        // 1. Load the workbook that contains the pivot table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // 2. Define copy options to include the pivot table
        CopyOptions copyOptions = new CopyOptions()
                .setCopyPivotTable(true);

        // 3. Copy the range A1:H20 with the specified options
        workbook.getWorksheets().get(0).getCells()
                .copyRange("A1:H20", copyOptions);

        // 4. Save the modified workbook
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

### Résultat attendu

* `output.xlsx` contient les mêmes données que `input.xlsx`.
* Le tableau croisé dynamique qui occupait initialement la plage source apparaît dans les cellules de destination, pleinement fonctionnel (filtres, capacité de rafraîchissement, etc.).
* Tout le formatage des cellules, les formules et les largeurs de colonnes sont préservés car `copyRange` copie l'intégralité du bloc de cellules.

## Questions fréquentes et cas limites

**Que se passe-t-il si la plage de destination chevauche un tableau croisé dynamique existant ?**  
Aspose.Cells écrasera les cellules cibles. Pour éviter toute perte de données, assurez‑vous que la zone de destination est vide ou déplacez d'abord le tableau croisé dynamique existant.

**Puis‑je copier un tableau croisé dynamique entre plusieurs feuilles ?**  
Oui. Utilisez `workbook.getWorksheets().get(targetSheetIndex).getCells().copyRange(sourceRange, copyOptions);` où `targetSheetIndex` indique la feuille de destination.

**`setCopyPivotTable(true)` copie‑t‑il la source de données sous‑jacente ?**  
La méthode ne copie que la référence du cache du tableau croisé dynamique. Si les données sources résident dans le même classeur, le tableau croisé dynamique de destination pointera vers le même cache. Pour dupliquer le cache, vous devez créer manuellement un nouveau cache de tableau croisé dynamique.

**Comment copier une grande plage efficacement ?**  
Lors de la copie de très grandes plages, envisagez d'utiliser `CopyOptions.setCopyFormula(true)` et `setCopyDataValidation(true)` uniquement si nécessaire. Réduire le nombre d'options peut améliorer les performances.

## Conseils pour une utilisation fiable de **aspose.cells copy range**

* **Astuce :** Appelez toujours `workbook.calculateFormula()` après la copie si la plage contient des formules dépendant du cache du tableau croisé dynamique.
* **Attention :** Feuilles de calcul cachées. `copyRange` ne fonctionne que sur les feuilles visibles, sauf si vous faites référence explicitement à la feuille cachée par son index.
* **Vérification de version :** Le drapeau `setCopyPivotTable` est disponible à partir d'Aspose.Cells 20.9. Assurez‑vous que votre version de la bibliothèque le prend en charge.

## Conclusion

Vous savez maintenant **how to copy pivot** dans Aspose.Cells et comment **copy range to workbook** tout en préservant la pleine fonctionnalité du tableau croisé dynamique. Les étapes — ajouter la bibliothèque, charger le classeur, configurer `CopyOptions`, effectuer la copie et enregistrer — constituent un modèle réutilisable que vous pouvez adapter à d'autres scénarios de copier‑coller.

Ensuite, explorez des sujets connexes tels que **aspose.cells copy range** pour les graphiques, le formatage conditionnel et la validation des données. Expérimentez la copie entre différents formats de fichiers (XLSX → XLS) pour élargir vos capacités d'automatisation. Bon codage !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités supplémentaires de l'API et explorer des approches d'implémentation alternatives dans vos propres projets.

- [Comment créer des tableaux croisés dynamiques dans Excel en utilisant Aspose.Cells pour Java : Guide complet](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [Comment mettre à jour la source d'un tableau croisé dynamique Excel avec Aspose.Cells pour Java : Guide complet](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Comment implémenter des segments dans les tableaux croisés dynamiques en utilisant Aspose.Cells pour Java : Guide complet](/cells/english/java/data-analysis/implement-slicers-pivot-tables-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}