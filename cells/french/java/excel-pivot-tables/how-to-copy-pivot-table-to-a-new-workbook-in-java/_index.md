---
category: general
date: 2026-10-26
description: Apprenez à copier un tableau croisé dynamique dans un nouveau classeur
  en Java, en conservant le formatage et la définition du tableau croisé dynamique
  tout en copiant une plage Excel avec mise en forme via Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- how to copy pivot
- copy excel range
- create empty workbook
- copy range with formatting
language: fr
lastmod: 2026-10-26
og_description: Copiez le tableau croisé dynamique vers un nouveau classeur en Java
  avec Aspose.Cells. Ce guide montre comment copier une plage Excel, préserver le
  formatage et créer efficacement un classeur vide.
og_image_alt: Screenshot of a Java program that copies a pivot table to a new Excel
  workbook
og_title: Copier un tableau croisé dynamique dans un nouveau classeur en Java – guide
  étape par étape
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to copy pivot table to a new workbook using Java, preserving
    formatting and the pivot definition while you copy excel range with formatting
    via Aspose.Cells.
  headline: How to copy pivot table to a new workbook in Java
  type: TechArticle
- description: Learn how to copy pivot table to a new workbook using Java, preserving
    formatting and the pivot definition while you copy excel range with formatting
    via Aspose.Cells.
  name: How to copy pivot table to a new workbook in Java
  steps:
  - name: Prerequisites
    text: '* Java 17 or later. * Aspose.Cells for Java (version 23.10 or newer). *
      Basic familiarity with Java IDEs (IntelliJ IDEA, Eclipse, etc.).'
  - name: Why this works
    text: '* `new Workbook()` **creates empty workbook** with a default sheet, avoiding
      the need to delete existing data. * `CopyOptions` tells Aspose.Cells to copy
      **pivot table** metadata, not just raw values. The `PASTE_ALL` mode also carries
      cell styles, number formats, and conditional formatting—fulfillin'
  - name: Edge cases to consider
    text: '| Situation | Recommended handling | |----------------------------------------|----------------------|
      | Source workbook has multiple pivots | Copy each pivot’s range separately or
      copy the whole sheet. | | Destination already contains data | Choose a non‑conflicting
      start cell (e.g., "H1") when cal'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Comment copier un tableau croisé dynamique dans un nouveau classeur en Java
url: /fr/java/excel-pivot-tables/how-to-copy-pivot-table-to-a-new-workbook-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment copier un tableau croisé dynamique vers un nouveau classeur en Java

Si vous devez **copier un tableau croisé dynamique** d’un fichier Excel à un autre, ce guide vous présente une solution complète et exécutable. Vous verrez comment préserver la définition du tableau croisé dynamique, conserver toute la mise en forme et éviter les pièges courants lors de la copie d’une plage Excel.

Copier un tableau croisé dynamique soulève souvent des questions comme *comment copier un tableau croisé dynamique* sans rompre la source de données ou perdre les styles. À la fin de ce tutoriel, vous disposerez d’un programme Java autonome qui crée un classeur vide, copie la plage souhaitée et enregistre le résultat avec le tableau croisé dynamique intact.

## Ce que vous allez réaliser

* Charger un classeur source contenant un tableau croisé dynamique.  
* **Créer un classeur vide** qui recevra les données copiées.  
* **Copier une plage Excel** incluant le tableau croisé dynamique, en utilisant des options qui conservent le tableau et la mise en forme.  
* Enregistrer le fichier de destination et vérifier que le tableau croisé dynamique fonctionne exactement comme l’original.

### Prérequis

* Java 17 ou version ultérieure.  
* Aspose.Cells for Java (version 23.10 ou plus récente).  
* Familiarité de base avec les IDE Java (IntelliJ IDEA, Eclipse, etc.).  

> **Astuce pro :** Utilisez la licence d’évaluation gratuite d’Aspose.Cells pour des tests rapides ; remplacez‑la par une licence complète avant la mise en production.

## Copier le tableau croisé dynamique vers un nouveau classeur

La première étape consiste à configurer les classeurs source et destination. La destination démarre avec un appel **create empty workbook**, qui vous fournit un fichier propre avec une seule feuille.

```java
import com.aspose.cells.*;

public class CopyPivotExample {
    public static void main(String[] args) throws Exception {
        // Load the source workbook that holds the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");

        // Create an empty workbook that will receive the copied range
        Workbook destWb = new Workbook();

        // Get the first worksheet from each workbook
        Worksheet srcSheet = srcWb.getWorksheets().get(0);
        Worksheet destSheet = destWb.getWorksheets().get(0);

        // Configure copy options to preserve the pivot table and formatting
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.PASTE_ALL); // ensures pivot and styles are kept

        // Copy the range that contains the pivot table
        srcSheet.getCells().copyRange("A1:D20", destSheet.getCells(), "A1", copyOptions);

        // Save the destination workbook
        destWb.save("YOUR_DIRECTORY/destination.xlsx");
    }
}
```

### Pourquoi cela fonctionne

* `new Workbook()` **creates empty workbook** avec une feuille par défaut, évitant ainsi de devoir supprimer des données existantes.  
* `CopyOptions` indique à Aspose.Cells de copier les métadonnées du **pivot table**, pas seulement les valeurs brutes. Le mode `PASTE_ALL` transporte également les styles de cellule, les formats numériques et la mise en forme conditionnelle—satisfaisant ainsi l’exigence de **copy range with formatting**.  
* `copyRange` effectue une opération de **copy excel range** qui respecte les structures internes de la source, de sorte que le tableau croisé dynamique reste fonctionnel après la copie.

## Comment copier le tableau croisé dynamique sans perdre la mise en forme

Si vous utilisez uniquement les `CopyOptions` par défaut, certaines informations de style peuvent être omises sur les versions plus anciennes d’Aspose.Cells. Définir explicitement le type de collage garantit que le **copy range with formatting** est respecté.

```java
CopyOptions copyOptions = new CopyOptions();
copyOptions.setPasteType(PasteType.PASTE_ALL);          // copy values, formulas, formats
copyOptions.setPasteSpecialType(PasteSpecialType.ALL); // include column widths and row heights
```

L’ajout de `setPasteSpecialType` assure que les largeurs de colonnes, hauteurs de lignes et même les règles de validation des données voyagent avec la plage. Ceci est particulièrement utile lorsque le tableau croisé dynamique s’étend sur plusieurs colonnes avec des largeurs personnalisées.

## Créer un classeur vide avant la copie

Parfois, les développeurs tentent de copier dans un classeur existant contenant déjà des données. Cela peut entraîner des chevauchements de plages ou des écrasements inattendus. Commencer par un appel **create empty workbook** isole l’opération :

```java
Workbook destWb = new Workbook(); // fresh file with one sheet
Worksheet destSheet = destWb.getWorksheets().get(0); // reference the clean sheet
```

Si vous avez besoin de plusieurs feuilles dans la destination, vous pouvez les ajouter après la copie :

```java
destWb.getWorksheets().add("Summary");
```

## Copier une plage Excel avec mise en forme à l’aide de CopyOptions

Au‑delà des tableaux croisés dynamiques, le même schéma fonctionne pour toute **copy excel range** nécessitant la préservation de la mise en forme — graphes, tableaux ou formats conditionnels.

```java
// Example: copy a styled table from A1 to G15
srcSheet.getCells().copyRange("A1:G15", destSheet.getCells(), "A1", copyOptions);
```

L’instance `CopyOptions` reste la même, vous obtenez donc un comportement cohérent sur différentes plages.

### Cas limites à prendre en compte

| Situation                              | Gestion recommandée |
|----------------------------------------|----------------------|
| Le classeur source possède plusieurs tableaux croisés dynamiques | Copier chaque plage de tableau croisé dynamique séparément ou copier la feuille entière. |
| La destination contient déjà des données | Choisir une cellule de départ non conflictuelle (par ex., "H1") lors de l’appel à `copyRange`. |
| La source du tableau croisé dynamique est externe (par ex., DB) | S’assurer que le classeur de destination pointe vers la même source externe, ou rafraîchir le tableau après la copie. |
| Grand classeur ( > 10 Mo )             | Augmenter la taille du tas Java (`-Xmx2g`) pour éviter `OutOfMemoryError`. |

## Vérifier le résultat

Après l’exécution du programme, ouvrez `destination.xlsx`. Vous devriez voir :

* La même disposition du tableau croisé dynamique que dans `source.xlsx`.  
* Toutes les couleurs de cellules, formats numériques et largeurs de colonnes conservés.  
* La source de données du tableau croisé dynamique pointe toujours vers la plage de données originale à l’intérieur du nouveau fichier, de sorte que le rafraîchissement du tableau met à jour les valeurs correctement.

Si le tableau apparaît comme une table statique, vérifiez que `CopyOptions.setPasteType(PasteType.PASTE_ALL)` est bien défini. Sans cette option, Aspose.Cells traite le tableau comme des données simples.

## Conclusion

Vous savez maintenant comment **copy pivot table** vers un nouveau classeur en Java tout en préservant la mise en forme, les connexions de données et la disposition des feuilles. La solution complète montre comment charger un fichier source, **create empty workbook**, configurer les options de **copy excel range**, puis enregistrer le résultat.  

À partir d’ici, vous pouvez explorer des sujets connexes tels que **how to copy pivot** entre différentes feuilles, intégrer des graphiques à côté des tableaux croisés dynamiques, ou automatiser le traitement par lots de plusieurs classeurs. Expérimentez avec les paramètres de `CopyOptions` pour les adapter à vos besoins d’automatisation spécifiques, et vous disposerez d’une boîte à outils robuste pour manipuler Excel.

## Que devez‑vous apprendre ensuite ?


Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications pas à pas pour vous aider à maîtriser d’autres fonctionnalités de l’API et à explorer des approches d’implémentation alternatives dans vos propres projets.

- [Create New Workbook in Java – Full Guide to Copy Pivot Table](/cells/english/java/excel-pivot-tables/create-new-workbook-in-java-full-guide-to-copy-pivot-table/)
- [Copy Pivot Table Between Workbooks – Step‑by‑Step Java Guide](/cells/english/java/excel-pivot-tables/copy-pivot-table-between-workbooks-step-by-step-java-guide/)
- [How to copy range and preserve a pivot table in Java](/cells/english/java/excel-pivot-tables/how-to-copy-range-and-preserve-a-pivot-table-in-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}