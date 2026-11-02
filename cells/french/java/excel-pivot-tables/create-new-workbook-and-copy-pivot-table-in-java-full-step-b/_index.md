---
category: general
date: 2026-07-16
description: Créez un nouveau classeur et copiez le tableau croisé dynamique à l’aide
  d’Aspose.Cells pour Java. Apprenez à dupliquer le tableau croisé dynamique et à
  copier une plage Excel en quelques minutes.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create new workbook
- copy pivot table
- duplicate pivot table
- how to copy pivot
- copy excel range
language: fr
lastmod: 2026-07-16
og_description: Créer un nouveau classeur et copier le tableau croisé dynamique avec
  Aspose.Cells pour Java. Ce guide montre comment dupliquer le tableau croisé dynamique
  et copier la plage Excel efficacement.
og_image_alt: Screenshot of Java code that creates a new workbook and copies a pivot
  table using Aspose.Cells
og_title: Créer un nouveau classeur et copier le tableau croisé dynamique en Java
  – Tutoriel complet
schemas:
- author: Aspose
  dateModified: '2026-07-16'
  description: Create new workbook and copy pivot table using Aspose.Cells for Java.
    Learn how to duplicate pivot table and copy Excel range in minutes.
  headline: Create New Workbook and Copy Pivot Table in Java – Full Step‑by‑Step Guide
  type: TechArticle
- description: Create new workbook and copy pivot table using Aspose.Cells for Java.
    Learn how to duplicate pivot table and copy Excel range in minutes.
  name: Create New Workbook and Copy Pivot Table in Java – Full Step‑by‑Step Guide
  steps:
  - name: What if the source pivot spans more than one sheet?
    text: Aspose.Cells can only copy ranges within a single worksheet at a time. If
      your pivot stretches across sheets, you’ll need to copy each relevant range
      separately and then re‑link them manually.
  - name: Does this method preserve custom number formats?
    text: Yes. The `copy` method copies cell styles, including number formats, fonts,
      and colors. However, if you have conditional formatting that references external
      ranges, double‑check those references after the copy.
  - name: How to copy a pivot that uses an external data source?
    text: When the pivot pulls data from an external connection (e.g., a SQL query),
      the connection information is **not** transferred by `copy`. You’ll need to
      recreate the data source in the destination workbook or embed the source data
      beforehand.
  - name: Can I copy only the pivot layout without the underlying data?
    text: You can achieve that by first clearing the data cells in the source range,
      then copying only the pivot’s layout. This is a more advanced scenario and usually
      not required for a simple **duplicate pivot table** task.
  type: HowTo
tags:
- Java
- Aspose.Cells
- Excel Automation
title: Créer un nouveau classeur et copier le tableau croisé dynamique en Java – Guide
  complet étape par étape
url: /fr/java/excel-pivot-tables/create-new-workbook-and-copy-pivot-table-in-java-full-step-b/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un nouveau classeur et copier un tableau croisé dynamique en Java – Guide complet étape par étape

Vous vous êtes déjà demandé comment **create new workbook** tout en conservant un tableau croisé dynamique complexe d’un fichier existant ? Si vous avez déjà fixé une feuille Excel, pensé « I need this pivot in another workbook », puis vous êtes gratté la tête, vous n’êtes pas seul. La bonne nouvelle, c’est qu’avec Aspose.Cells for Java, vous pouvez dupliquer un tableau croisé dynamique en quelques lignes seulement.

Dans ce tutoriel, nous parcourrons les étapes exactes pour les données **copy pivot table**, les structures **duplicate pivot table**, et le contenu **copy Excel range** — tout en créant un nouveau classeur à partir de zéro. À la fin, vous disposerez d’un programme Java prêt à l’exécution qui fait exactement ce que vous avez demandé.

## Ce que vous apprendrez

- Comment **create new workbook** programmatique avec Aspose.Cells.
- La façon précise de définir la plage qui contient un tableau croisé dynamique.
- Techniques pour **copy pivot table** et **duplicate pivot table** sans perdre le formatage ou les connexions de données.
- Comment **copy Excel range** efficacement et enregistrer le résultat.
- Pièges courants et astuces pour gérer les tableaux croisés dynamiques de grande taille.

Aucune référence externe n’est nécessaire — tout est autonome, exécutable et expliqué.

---

## Prérequis

Avant de commencer, assurez-vous d’avoir :

1. **Java Development Kit (JDK) 11+** – toute version récente fonctionne.  
2. **Aspose.Cells for Java** library (the latest version as of 2026‑07‑16). You can grab it from Maven Central:

   ```xml
   <dependency>
       <groupId>com.aspose</groupId>
       <artifactId>aspose-cells</artifactId>
       <version>23.12</version>
   </dependency>
   ```

3. Un fichier Excel source (`SourceWithPivot.xlsx`) qui contient déjà le tableau croisé dynamique que vous souhaitez copier.  
4. Un IDE ou un éditeur de texte simple — IntelliJ IDEA, Eclipse ou VS Code conviennent.

Tout est prêt ? Super — c’est parti.

## Étape 1 : **Create New Workbook** et charger le fichier source

La première chose dont nous avons besoin est un nouvel objet classeur qui contiendra finalement le tableau croisé dynamique dupliqué. En même temps, nous devons charger le classeur original afin de pouvoir référencer la plage de son tableau croisé dynamique.

```java
import com.aspose.cells.*;

public class CopyPivotTableDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook that already contains the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
        // Grab the first worksheet where the pivot lives
        Worksheet srcWs = srcWb.getWorksheets().get(0);
```

> **Why this matters:**  
> Charger le classeur source nous donne accès à l’objet `Range` sous‑jacent qui encapsule le tableau croisé dynamique. Si vous sautez cette étape, vous n’aurez rien à copier, et l’opération **duplicate pivot table** échouera silencieusement.

---

## Étape 2 : Définir le **Copy Excel Range** qui contient le tableau croisé dynamique

Un tableau croisé dynamique n’est pas une seule cellule — il s’étend sur un bloc rectangulaire. Nous devons indiquer à Aspose.Cells exactement quelles cellules copier.

```java
        // Define the cell range that includes the pivot table (adjust as needed)
        Range srcRange = srcWs.getCells().createRange("A1:G20");
```

> **Tip:**  
> Si vous n’êtes pas sûr de la plage exacte, ouvrez le classeur source dans Excel, sélectionnez le tableau croisé dynamique et regardez la zone de nom. Elle affichera quelque chose comme `A1:G20`. Utiliser la plage exacte garantit que tous les paramètres de champ, filtres et calculs sont conservés lorsque nous **copy pivot table** plus tard.

---

## Étape 3 : **Create New Workbook** qui recevra le tableau croisé dynamique copié

Nous créons maintenant un tout nouveau classeur — c’est ici que notre **duplicate pivot table** résidera.

```java
        // Create a completely empty workbook for the destination
        Workbook dstWb = new Workbook(); // this automatically creates one empty worksheet
        Worksheet dstWs = dstWb.getWorksheets().get(0);
```

> **What’s happening under the hood?**  
> Le constructeur par défaut crée un classeur avec une seule feuille vide. C’est la toile vierge dont nous avons besoin pour un scénario **create new workbook**. Aucun style résiduel ou feuille cachée à craindre.

---

## Étape 4 : **Copy Pivot Table** – Copier réellement la plage Excel définie

Avec la source et la destination prêtes, nous exécutons l’opération de copie. Cette étape réalise la partie **how to copy pivot** du puzzle.

```java
        // Copy the defined range (which includes the pivot) to the destination worksheet
        srcRange.copy(dstWs.getCells().createRange("A1"));
```

> **Why `copy` works for pivots:**  
> Aspose.Cells considère le tableau croisé dynamique comme faisant partie de la collection de cellules. Lorsque vous copiez la plage, il transfère le cache du tableau, la liste des champs et la mise en page. Le résultat est un **duplicate pivot table** pleinement fonctionnel dans le nouveau classeur.

---

## Étape 5 : Enregistrer le résultat et vérifier l’opération **Copy Pivot Table**

Enfin, enregistrez le classeur de destination sur le disque. Ouvrez le fichier dans Excel pour confirmer que le tableau croisé dynamique apparaît exactement comme dans la source.

```java
        // Save the destination workbook with the duplicated pivot table
        dstWb.save("YOUR_DIRECTORY/CopyPivotResult.xlsx");
    }
}
```

**Expected outcome:**  
- `CopyPivotResult.xlsx` s’ouvre avec une feuille contenant le même tableau croisé dynamique que celui que vous avez vu dans `SourceWithPivot.xlsx`.  
- Tous les libellés de lignes/colonnes, filtres et champs calculés sont intacts.  
- Vous pouvez maintenant modifier les données source indépendamment, et le nouveau classeur conservera son propre cache de tableau croisé dynamique.

---

## Cas limites et questions fréquentes

### Que faire si le tableau croisé dynamique source s’étend sur plusieurs feuilles ?

Aspose.Cells ne peut copier des plages que dans une seule feuille de calcul à la fois. Si votre tableau croisé dynamique s’étend sur plusieurs feuilles, vous devrez copier chaque plage pertinente séparément, puis les relier manuellement.

### Cette méthode préserve‑t‑elle les formats numériques personnalisés ?

Oui. La méthode `copy` copie les styles de cellule, y compris les formats numériques, les polices et les couleurs. Cependant, si vous avez une mise en forme conditionnelle qui référence des plages externes, vérifiez à nouveau ces références après la copie.

### Comment copier un tableau croisé dynamique qui utilise une source de données externe ?

Lorsque le tableau croisé dynamique récupère des données depuis une connexion externe (par ex., une requête SQL), les informations de connexion **ne** sont pas transférées par `copy`. Vous devrez recréer la source de données dans le classeur de destination ou intégrer les données source au préalable.

### Puis‑je copier uniquement la mise en page du tableau croisé dynamique sans les données sous‑jacentes ?

Vous pouvez y parvenir en vidant d’abord les cellules de données dans la plage source, puis en copiant uniquement la mise en page du tableau croisé dynamique. C’est un scénario plus avancé et généralement pas nécessaire pour une tâche simple de **duplicate pivot table**.

---

## Exemple complet fonctionnel (toutes les étapes combinées)

Voici la classe Java complète, prête à être exécutée. Remplacez simplement `YOUR_DIRECTORY` par le chemin réel du dossier sur votre machine.

```java
import com.aspose.cells.*;

public class CopyPivotTableDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the source workbook containing the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // Step 2: Define the exact range that holds the pivot table
        // Adjust "A1:G20" to match your pivot's size
        Range srcRange = srcWs.getCells().createRange("A1:G20");

        // Step 3: Create a brand‑new workbook that will receive the copy
        Workbook dstWb = new Workbook(); // creates an empty workbook with one sheet
        Worksheet dstWs = dstWb.getWorksheets().get(0);

        // Step 4: Copy the pivot (and any surrounding data) to the new workbook
        srcRange.copy(dstWs.getCells().createRange("A1"));

        // Step 5: Save the destination file – now it contains the duplicated pivot table
        dstWb.save("YOUR_DIRECTORY/CopyPivotResult.xlsx");

        System.out.println("Pivot table copied successfully! Check CopyPivotResult.xlsx.");
    }
}
```

Exécutez le programme (`java CopyPivotTableDemo`) et vous verrez le message de console confirmant le succès.

---

## Astuces pro et bonnes pratiques

- **Validate the range** avant de copier. Utilisez `srcWs.getCells().maxDisplayRange` pour découvrir programmatique la zone utilisée si vous ne voulez pas coder en dur `"A1:G20"`.
- **Turn off calculation** temporairement pour les classeurs volumineux afin d’accélérer la copie :

  ```java
  srcWb.getSettings().setCalculateFormulaOnOpen(false);
  ```

- **Dispose of resources** (`srcWb.dispose(); dstWb.dispose();`) dans les services de longue durée pour éviter les fuites de mémoire.
- **Version compatibility:** Le code fonctionne avec Aspose.Cells 23.12 et versions ultérieures. Les versions plus anciennes peuvent nécessiter `srcRange.copyTo` au lieu de `copy`.

---

## Prochaines étapes

Maintenant que vous avez maîtrisé **create new workbook** et **copy pivot table**, vous pouvez explorer :

- **How to copy pivot** à travers plusieurs feuilles de calcul dans un job batch.  
- Ajouter **copy excel range** pour les tableaux de données réguliers en plus du tableau croisé dynamique.  
- Automatiser la création de **duplicate pivot table** pour chaque rapport mensuel en utilisant une boucle.  
- Exporter le tableau croisé dynamique dupliqué en PDF ou HTML avec les rendus intégrés d’Aspose.Cells.

---

## Conclusion

Nous avons parcouru l’ensemble du processus de **create new workbook**, définir la source **copy excel range**, et **copy pivot table** pour produire un **duplicate pivot table** en Java avec Aspose.Cells. La solution est concise, entièrement fonctionnelle et prête à être utilisée en production. N’hésitez pas à ajuster la plage, expérimenter avec différents fichiers source, ou intégrer cette logique dans un pipeline de reporting plus vaste.

Si vous rencontrez des problèmes ou avez des idées pour étendre ce tutoriel, laissez un commentaire ci‑dessous. Bon codage !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [How to Create Pivot Tables in Excel Using Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [How to Update Excel Pivot Table Source with Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Excel Pivot Table Manipulation with Aspose.Cells Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/excel-pivot-table-manipulation-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}