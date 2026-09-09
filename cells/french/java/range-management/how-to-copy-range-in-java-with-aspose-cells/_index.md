---
category: general
date: 2026-09-08
description: Comment copier une plage en Java avec Aspose.Cells – apprenez à copier
  un tableau croisé dynamique, dupliquer un tableau croisé dynamique et exporter un
  tableau croisé dynamique tout en préservant le formatage.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy range
- copy pivot table
- duplicate pivot table
- export pivot table
- copy range with formatting
language: fr
lastmod: 2026-09-08
og_description: Comment copier une plage en Java avec Aspose.Cells. Ce tutoriel vous
  montre comment copier un tableau croisé dynamique, dupliquer un tableau croisé dynamique
  et exporter un tableau croisé dynamique tout en préservant le formatage.
og_image_alt: Screenshot of Java code copying a pivot table range in Aspose.Cells
og_title: Comment copier une plage en Java – guide complet d’Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-09-08'
  description: How to copy range in Java using Aspose.Cells – learn to copy pivot
    table, duplicate pivot table, and export pivot table while preserving formatting.
  headline: How to copy range in Java with Aspose.Cells
  type: TechArticle
- description: How to copy range in Java using Aspose.Cells – learn to copy pivot
    table, duplicate pivot table, and export pivot table while preserving formatting.
  name: How to copy range in Java with Aspose.Cells
  steps:
  - name: Copy pivot table to an existing workbook
    text: 'If you need to **duplicate pivot table** inside a workbook that already
      has data, use the same `copyRange` call but point to a different destination
      address:'
  - name: Export pivot table only (without surrounding data)
    text: 'Sometimes you want just the pivot table, not the source data. Identify
      the pivot table’s display range via its `getPivotTable` method:'
  - name: Preserve conditional formatting
    text: 'Conditional formatting rules are part of the style collection. The `PasteType.ALL`
      flag already copies them, but you can be explicit:'
  - name: Edge cases and troubleshooting
    text: '| Situation | What to watch for | Recommended fix | |-----------|-------------------|-----------------|
      | Source and destination workbooks use different Excel versions | Some newer
      pivot features (e.g., data model) may not render correctly | Use the latest
      Aspose.Cells version and set `Workbook.setF'
  - name: Next steps
    text: '- Explore **copy range with formatting** for charts and images (use `PasteType.PICTURES`).
      - Automate batch processing: loop over multiple source files and consolidate
      their pivot tables into a summary workbook. - Combine this technique with Aspose.Slides
      to generate PowerPoint reports that embed th'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Comment copier une plage en Java avec Aspose.Cells
url: /fr/java/range-management/how-to-copy-range-in-java-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment copier une plage en Java avec Aspose.Cells

Si vous avez besoin de **comment copier une plage** en Java, Aspose.Cells rend la tâche simple. Que vous déplaciez un bloc de cellules ordinaire ou un tableau croisé dynamique complet, la bibliothèque gère l'opération de copie tout en conservant les formules, les styles et le cache du tableau croisé dynamique. Dans ce guide, vous apprendrez à **copier un tableau croisé dynamique**, **dupliquer un tableau croisé dynamique**, et même **exporter un tableau croisé dynamique** vers un nouveau classeur avec le formatage complet.

Le tutoriel couvre tout, de la configuration du projet à l'étape de vérification finale, afin que vous puissiez exécuter le code immédiatement après la lecture. Aucun outil externe n'est requis au-delà du JAR Aspose.Cells pour Java.

## Prérequis

- Java 17 (ou tout JDK pris en charge) installé et configuré dans votre IDE.
- Maven ou Gradle pour la gestion des dépendances (les exemples utilisent Maven).
- Un fichier Excel source (`source.xlsx`) contenant un tableau croisé dynamique dans la plage `A1:H20`.
- Une connaissance de base de la programmation Java.

## Étape 1 : Ajouter Aspose.Cells à votre projet

Aspose.Cells est une bibliothèque commerciale, mais une version d'évaluation gratuite est disponible. Ajoutez la dépendance à votre `pom.xml` :

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest version -->
</dependency>
```

> **Astuce :** Si vous préférez Gradle, l'entrée équivalente est :
> ```gradle
> implementation 'com.aspose:aspose-cells:24.9'
> ```

L'ajout du JAR vous donne accès aux classes `Workbook`, `Worksheet`, `Range` et `CopyOptions` utilisées tout au long de ce guide.

## Étape 2 : Charger le classeur source et sélectionner la première feuille de calcul

La première partie de **comment copier une plage** consiste à ouvrir le classeur qui contient les données que vous souhaitez déplacer.

```java
import com.aspose.cells.*;

public class CopyRangeDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        // Select the first worksheet (index 0)
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);
```

> **Pourquoi c'est important :** L'ouverture du classeur crée une représentation en mémoire que l'API peut manipuler sans toucher au fichier original sur le disque.

## Étape 3 : Définir la plage qui contient le tableau croisé dynamique

Un tableau croisé dynamique se trouve à l'intérieur d'un bloc rectangulaire. Vous devez spécifier ce bloc afin qu'Aspose.Cells sache quoi copier.

```java
        // Define the range that holds the pivot table and its source data
        Range sourceRange = sourceSheet.getCells().createRange("A1:H20");
```

> **Remarque :** La méthode `createRange` ne copie **pas** encore quoi que ce soit ; elle crée uniquement un objet `Range` qui pointe vers les cellules que vous avez l'intention de dupliquer.

## Étape 4 : Créer un nouveau classeur et obtenir sa première feuille de calcul

Créez maintenant le classeur de destination où la plage copiée résidera.

```java
        // Create an empty workbook for the destination
        Workbook destWorkbook = new Workbook();
        // Get its first (and only) worksheet
        Worksheet destSheet = destWorkbook.getWorksheets().get(0);
```

> **Pourquoi un nouveau classeur ?** Utiliser un fichier vierge garantit qu'aucun style caché ou plage nommée n'interfère avec l'opération de copie, ce qui est particulièrement important lorsque vous **exportez un tableau croisé dynamique** vers un fichier séparé.

## Étape 5 : Copier la plage (y compris le tableau croisé dynamique) vers la feuille de destination

Ceci est le cœur de **comment copier une plage avec formatage**. L'objet `CopyOptions` indique à Aspose.Cells de tout préserver : valeurs, formules, styles et cache du tableau croisé dynamique.

```java
        // Prepare copy options – preserve formatting and pivot cache
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.ALL); // copies everything
        copyOptions.setSkipBlanks(false);        // keep blank cells

        // Copy the defined range to cell A1 of the destination sheet
        destSheet.getCells().copyRange(sourceRange, "A1", copyOptions);
```

> **Copier le tableau croisé dynamique :** Comme la plage source inclut le tableau croisé dynamique, l'API duplique automatiquement le cache du tableau, de sorte que la nouvelle feuille de calcul contient un tableau croisé dynamique entièrement fonctionnel qui se comporte exactement comme l'original.

## Étape 6 : Enregistrer le classeur de destination

Enfin, écrivez le résultat sur le disque.

```java
        // Save the destination workbook
        destWorkbook.save("YOUR_DIRECTORY/dest.xlsx");
    }
}
```

Lorsque vous ouvrez `dest.xlsx`, vous verrez une réplique exacte du tableau croisé dynamique original, complet avec son formatage, ses segments et ses champs calculés.

## Résultat attendu

- `dest.xlsx` contient une feuille de calcul nommée **Sheet1**.
- Les cellules `A1:H20` contiennent les mêmes données et le même tableau croisé dynamique que la source.
- Tous les styles de cellule (polices, couleurs, bordures) sont préservés.
- Le tableau croisé dynamique est entièrement interactif ; le rafraîchir reflète les données sous-jacentes dans la plage copiée.

## Comment copier une plage avec formatage – approfondissement

L'exemple précédent montre le scénario le plus simple, mais vous pouvez rencontrer des variantes qui nécessitent une approche légèrement différente.

### Copier le tableau croisé dynamique vers un classeur existant

Si vous devez **dupliquer un tableau croisé dynamique** dans un classeur qui contient déjà des données, utilisez le même appel `copyRange` mais pointez vers une adresse de destination différente :

```java
// Assume destWorkbook already contains other sheets
Worksheet targetSheet = destWorkbook.getWorksheets().get(2);
targetSheet.getCells().copyRange(sourceRange, "B5", copyOptions);
```

### Exporter uniquement le tableau croisé dynamique (sans les données environnantes)

Parfois vous ne voulez que le tableau croisé dynamique, pas les données sources. Identifiez la plage d'affichage du tableau via sa méthode `getPivotTable` :

```java
PivotTable pt = sourceSheet.getPivotTables().get(0);
String ptArea = pt.getDisplayRange(); // e.g., "C5:G15"
Range pivotOnly = sourceSheet.getCells().createRange(ptArea);
destSheet.getCells().copyRange(pivotOnly, "A1", copyOptions);
```

### Conserver le formatage conditionnel

Les règles de formatage conditionnel font partie de la collection de styles. Le drapeau `PasteType.ALL` les copie déjà, mais vous pouvez être explicite :

```java
copyOptions.setPasteType(PasteType.FORMATS);
copyOptions.setPasteType(PasteType.ALL); // overrides previous, ensures everything
```

### Cas limites et dépannage

| Situation | Ce qu'il faut surveiller | Correction recommandée |
|-----------|--------------------------|------------------------|
| Les classeurs source et destination utilisent des versions Excel différentes | Certaines fonctionnalités récentes du tableau croisé dynamique (p. ex., modèle de données) peuvent ne pas s'afficher correctement | Utilisez la dernière version d'Aspose.Cells et définissez `Workbook.setFileFormatType(FileFormatType.XLSX)` pour les deux classeurs |
| Les très grands tableaux croisés dynamiques (> 10 000 lignes) provoquent une pression mémoire | Erreurs de type out‑of‑memory lors de la copie | Activez `Workbook.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` avant le chargement |
| La feuille de destination contient déjà une plage nommée portant le même nom que celle de la source | Collision de noms entraînant l'échec de `CopyOptions` | Appelez `copyOptions.setIgnoreNameConflicts(true)` |

## Exemple complet, exécutable

Voici le programme complet que vous pouvez copier‑coller dans une classe Java. Il comprend tous les imports, la gestion des erreurs et les commentaires.

```java
import com.aspose.cells.*;

public class CopyRangeDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the source workbook
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);

        // 2️⃣ Define the range that includes the pivot table
        Range sourceRange = sourceSheet.getCells().createRange("A1:H20");

        // 3️⃣ Create a new destination workbook
        Workbook destWorkbook = new Workbook();
        Worksheet destSheet = destWorkbook.getWorksheets().get(0);

        // 4️⃣ Configure copy options to keep everything (values, formulas, formatting, pivot cache)
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.ALL);
        copyOptions.setSkipBlanks(false);
        copyOptions.setIgnoreNameConflicts(true); // avoid name collisions

        // 5️⃣ Perform the copy
        destSheet.getCells().copyRange(sourceRange, "A1", copyOptions);

        // 6️⃣ Save the result
        destWorkbook.save("YOUR_DIRECTORY/dest.xlsx");
        System.out.println("Copy completed – dest.xlsx now contains the duplicated pivot table.");
    }
}
```

Exécutez le programme, puis ouvrez `dest.xlsx` pour vérifier que le tableau croisé dynamique fonctionne exactement comme l'original.

## Conclusion

Vous savez maintenant **comment copier une plage** en Java avec Aspose.Cells, y compris comment **copier un tableau croisé dynamique**, **dupliquer un tableau croisé dynamique**, et **exporter un tableau croisé dynamique** tout en préservant tout le formatage. La bibliothèque abstrait les détails de bas niveau de la structure XML d'Excel, vous permettant de vous concentrer sur la logique métier.

### Prochaines étapes

- Explorez **copy range with formatting** pour les graphiques et les images (utilisez `PasteType.PICTURES`).
- Automatisez le traitement par lots : parcourez plusieurs fichiers sources et consolidez leurs tableaux croisés dynamiques dans un classeur récapitulatif.
- Combinez cette technique avec Aspose.Slides pour générer des rapports PowerPoint qui intègrent le tableau croisé dynamique copié

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code fonctionnels complets avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités supplémentaires de l'API et explorer des approches d'implémentation alternatives dans vos propres projets.

- [Comment mettre à jour la source du tableau croisé dynamique Excel avec Aspose.Cells pour Java : guide complet](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Optimiser le chargement des tableaux croisés dynamiques en Java avec Aspose.Cells – guide complet](/cells/english/java/data-analysis/optimize-pivot-table-loading-aspose-cells-java/)
- [Comment copier un tableau croisé dynamique en C# – Convertir Excel en PPTX, copier la plage et créer une zone de texte](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}