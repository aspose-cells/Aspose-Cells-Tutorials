---
category: general
date: 2026-08-14
description: Copier une plage entre classeurs avec Java en utilisant Aspose.Cells.
  Apprenez à copier un classeur de tableau croisé dynamique, à exporter une image
  vers PowerPoint et à supprimer le filtre automatique d’un tableau Excel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy range between workbooks
- copy pivot table workbook
- export picture to powerpoint
- copy excel range to new workbook
- remove autofilter from excel table
language: fr
lastmod: 2026-08-14
og_description: Copier une plage entre classeurs en Java. Ce guide montre comment
  copier un classeur de tableau croisé dynamique, exporter une image vers PowerPoint
  et supprimer le filtre automatique d’un tableau Excel.
og_image_alt: Screenshot of Java code copying range between workbooks with Aspose.Cells
og_title: Copier une plage entre classeurs en Java – tutoriel complet Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: Copy range between workbooks with Java using Aspose.Cells. Learn to
    copy pivot table workbook, export picture to PowerPoint and remove AutoFilter
    from Excel table.
  headline: Copy range between workbooks in Java – step‑by‑step guide
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
- PowerPoint export
title: Copier une plage entre classeurs en Java – guide étape par étape
url: /fr/java/range-management/copy-range-between-workbooks-in-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Copier une plage entre classeurs en Java – guide étape par étape

Si vous devez **copier une plage entre classeurs** en Java, Aspose.Cells fournit une API claire qui gère des objets complexes tels que les tableaux croisés dynamiques et les images. Ce tutoriel montre comment **copier le classeur d’un tableau croisé dynamique**, **exporter une image vers PowerPoint**, et **supprimer l’AutoFilter d’un tableau Excel** tout en gardant le code facile à lire et à maintenir.

Vous apprendrez à :

* Charger un classeur source et définir la plage source.  
* Créer un classeur de destination et copier la plage afin que le tableau croisé dynamique reste intact.  
* Exporter la première image de la feuille en tant qu’objet PowerPoint éditable.  
* Supprimer un AutoFilter du premier tableau Excel.  
* Charger un classeur avec `SmartMarkerOptions` pour traiter les tableaux JSON comme une seule valeur de cellule.

L’exemple utilise Aspose.Cells 23.10 pour Java, mais les concepts s’appliquent également aux versions antérieures.

---

## Prérequis

| Exigence | Pourquoi c’est important |
|----------|---------------------------|
| Java 17 ou version ultérieure | Requis par le runtime le plus récent d’Aspose.Cells. |
| Aspose.Cells pour Java (artefact Maven `com.aspose:aspose-cells`) | Fournit les classes `Workbook`, `Worksheet`, `Range` et les classes associées utilisées dans le code. |
| Un fichier Excel source (`src.xlsx`) contenant un tableau croisé dynamique, une image et un tableau avec un AutoFilter. | Le tutoriel manipule ces objets pour démontrer chaque fonctionnalité. |

Ajoutez la dépendance Maven à votre `pom.xml` :

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

---

## Copier une plage entre classeurs – charger la source et la destination

La première étape consiste à ouvrir le classeur source, sélectionner la plage contenant les données que vous souhaitez copier, et créer un classeur de destination vide.

```java
import com.aspose.cells.*;

public class CopyRangeDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook that holds the pivot table, picture, and table.
        Workbook sourceWb = new Workbook("YOUR_DIRECTORY/src.xlsx");
        Worksheet sourceWs = sourceWb.getWorksheets().get(0);

        // Define the range that includes the pivot table (A1:G20 in this example).
        Range sourceRange = sourceWs.getCells().createRange("A1:G20");

        // Create a new workbook that will receive the copied range.
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);
        Range destRange = destWs.getCells().createRange("A1");
```

> **Pourquoi c’est important :** En utilisant `Range.copy`, Aspose.Cells copie non seulement les valeurs brutes des cellules mais aussi le cache sous-jacent du tableau croisé dynamique, maintenant ainsi la fonctionnalité du tableau croisé dynamique dans le classeur de destination.

---

## Copier le classeur du tableau croisé dynamique lors de la copie de la plage

Maintenant, copiez la plage définie du classeur source vers le classeur de destination. Le tableau croisé dynamique est préservé automatiquement parce que la plage inclut le cache du tableau croisé dynamique.

```java
        // Copy the source range to the destination range.
        destRange.copy(sourceRange);

        // Save the intermediate workbook to verify that the pivot table was copied.
        destWb.save("YOUR_DIRECTORY/destination.xlsx");
```

> **Résultat :** L’ouverture de `destination.xlsx` montre la même disposition du tableau croisé dynamique que `src.xlsx`. Aucun code supplémentaire n’est nécessaire pour reconstruire le cache du tableau croisé dynamique.

---

## Exporter une image vers PowerPoint

Aspose.Cells peut marquer une image pour l’exporter en tant qu’objet PowerPoint éditable. Le code suivant sélectionne la première image de la feuille de destination et définit le drapeau d’exportation.

```java
        // Retrieve the first picture on the destination sheet.
        Shape picture = destWs.getPictures().get(0);

        // Instruct Aspose.Cells to export this picture as a PowerPoint object.
        picture.getPictureFormat().setExportToPptx(true);

        // Optionally, save the workbook as PPTX to see the result.
        destWb.save("YOUR_DIRECTORY/destination.pptx");
```

> **Ce que vous voyez :** L’ouverture de `destination.pptx` dans PowerPoint montre l’image sous forme de forme native que vous pouvez modifier, redimensionner ou animer.

---

## Supprimer l’AutoFilter d’un tableau Excel

Si la feuille source contient un tableau avec un AutoFilter, vous pouvez vouloir le supprimer après la copie. Le code ci‑dessous accède au premier tableau et retire son filtre.

```java
        // Access the first table on the destination sheet.
        Table table = destWs.getTables().get(0);

        // Remove the AutoFilter by assigning null.
        table.setAutoFilter(null);

        // Save the final workbook.
        destWb.save("YOUR_DIRECTORY/final_output.xlsx");
```

> **Effet :** Le tableau reste dans le classeur, mais les flèches de filtrage déroulantes disparaissent, vous offrant une vue de données épurée.

---

## Charger un classeur avec les options SmartMarker – traiter les tableaux JSON comme une seule cellule

Lorsque vous générez un rapport à partir de JSON, Aspose.Cells peut traiter un tableau entier comme une seule valeur de cellule. Ceci est utile pour intégrer des chaînes JSON dans un modèle sans les développer en plusieurs cellules.

```java
        // Configure LoadOptions to enable SmartMarker array handling.
        LoadOptions loadOptions = new LoadOptions();
        SmartMarkerOptions smOptions = new SmartMarkerOptions();
        smOptions.setArrayAsSingle(true);
        loadOptions.setSmartMarkerOptions(smOptions);

        // Load a template workbook using the configured options.
        Workbook smartMarkerWb = new Workbook("YOUR_DIRECTORY/template.xlsx", loadOptions);

        // Continue processing (e.g., populate markers) as needed.
        // ...

        // Save the processed workbook.
        smartMarkerWb.save("YOUR_DIRECTORY/template_filled.xlsx");
    }
}
```

> **Pourquoi vous pourriez l’utiliser :** Si votre charge utile JSON contient un tableau qui doit apparaître comme une chaîne JSON dans une seule cellule, `setArrayAsSingle(true)` empêche Aspose.Cells d’étendre le tableau en lignes ou colonnes séparées.

![Copier une plage entre classeurs en Java – exemple de code Aspose.Cells](copy-range-workbooks.png)

*Texte alternatif de l’image :* **Copier une plage entre classeurs en Java – exemple de code Aspose.Cells** (correspond au mot‑clé principal).

---

## Résultat attendu

| Nom du fichier            | Contient |
|---------------------------|----------|
| `destination.xlsx`       | Plage copiée avec tableau croisé dynamique fonctionnel. |
| `destination.pptx`       | Image exportée sous forme de forme PowerPoint éditable. |
| `final_output.xlsx`      | Tableau sans flèches d’AutoFilter. |
| `template_filled.xlsx`   | Tableau JSON stocké comme valeur d’une seule cellule. |

Ouvrez chaque fichier dans l’application appropriée (Excel ou PowerPoint) pour vérifier que les opérations ont réussi.

---

## Conclusion

Vous savez maintenant comment **copier une plage entre classeurs** en Java en utilisant Aspose.Cells, tout en préservant un tableau croisé dynamique, en exportant une image vers PowerPoint et en supprimant un AutoFilter d’un tableau Excel. Le même schéma peut être étendu pour copier n’importe quelle plage Excel vers un nouveau classeur, gérer les tableaux JSON SmartMarker, ou chaîner des transformations supplémentaires.

Prochaines étapes que vous pourriez explorer :

* **Copy Excel range to new workbook** avec plusieurs feuilles de calcul.  
* Utilisez **export picture to PowerPoint** pour l’extraction d’images en lot.  
* Appliquez **remove autofilter from excel table** dans des pipelines de reporting plus importants.  
* Combinez ces techniques avec Aspose.Slides pour une automatisation complète Excel‑vers‑PowerPoint.

N’hésitez pas à expérimenter avec différentes adresses de plage, plusieurs tableaux croisés dynamiques ou des formats d’image personnalisés. L’API Aspose.Cells est conçue pour une flexibilité programmatique, vous permettant d’adapter les modèles présentés ici à tout scénario d’automatisation Excel d’entreprise.

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Copier des images entre feuilles dans Excel avec Aspose.Cells pour Java : guide complet](/cells/english/java/images-shapes/copy-images-between-sheets-excel-aspose-cells-java/)
- [Copier les paramètres de mise en page entre feuilles de calcul dans Excel avec Aspose.Cells Java](/cells/english/java/headers-footers/copy-page-setup-excel-aspose-cells-java/)
- [Copier des feuilles de calcul Excel entre classeurs](/cells/english/net/excel-copy-worksheet/excel-copy-worksheets-between-workbooks/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}