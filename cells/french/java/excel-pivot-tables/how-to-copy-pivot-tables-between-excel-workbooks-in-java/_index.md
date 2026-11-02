---
category: general
date: 2026-10-01
description: Apprenez à copier des tableaux croisés dynamiques entre des classeurs
  Excel en utilisant Java. Ce guide étape par étape montre également comment copier
  des plages entre des classeurs et dupliquer des plages Excel en toute sécurité.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot
- copy range between workbooks
- how to copy excel
- duplicate excel range
- copy range to workbook
language: fr
lastmod: 2026-10-01
og_description: Comment copier des tableaux croisés dynamiques entre des classeurs
  Excel à l'aide de Java. Suivez ce guide pour copier une plage dans un classeur,
  dupliquer des plages Excel et préserver les données du tableau croisé dynamique.
og_image_alt: Screenshot of Java code that copies a pivot table from one Excel workbook
  to another
og_title: Comment copier des tableaux croisés dynamiques entre des classeurs Excel
  en Java – guide complet
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to copy pivot tables between Excel workbooks using Java.
    This step‑by‑step guide also shows how to copy range between workbooks and duplicate
    Excel ranges safely.
  headline: How to copy pivot tables between Excel workbooks in Java
  type: TechArticle
- description: Learn how to copy pivot tables between Excel workbooks using Java.
    This step‑by‑step guide also shows how to copy range between workbooks and duplicate
    Excel ranges safely.
  name: How to copy pivot tables between Excel workbooks in Java
  steps:
  - name: Expected output
    text: '* Console: `Pivot table copied successfully.` * `destination.xlsx` opens
      in Excel with a pivot table identical to the one in `source.xlsx`. Refreshing
      the pivot shows the same data source, proving that **how to copy pivot** works
      as intended.'
  - name: Copying multiple worksheets
    text: If your project requires copying several sheets, loop through the workbook’s
      worksheets and repeat steps 2‑4 for each sheet. The pivot in each sheet will
      be preserved independently.
  - name: Preserving external data connections
    text: Pivot tables that rely on external data sources keep the connection string
      after copying. However, the destination file must have access to the same data
      source. Verify the connection by opening the pivot and checking the **Data**
      tab.
  - name: Dealing with merged cells
    text: If the source range contains merged cells, Aspose.Cells copies the merge
      layout automatically. Still, validate the result if the destination workbook
      uses a different default column width.
  type: HowTo
tags:
- Excel
- Java
- Aspose.Cells
- Pivot table
- Data manipulation
title: Comment copier des tableaux croisés dynamiques entre des classeurs Excel en
  Java
url: /fr/java/excel-pivot-tables/how-to-copy-pivot-tables-between-excel-workbooks-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment copier des tableaux croisés dynamiques entre des classeurs Excel en Java

Si vous avez besoin de **how to copy pivot** tables d'un fichier Excel à un autre, ce guide vous fournit une solution prête à l'emploi. À la fin des deux premières phrases, vous saurez exactement quels appels d'API préservent la définition du tableau croisé dynamique lors de la copie de la plage de données.

Vous apprendrez également comment **copy range between workbooks**, **duplicate Excel range** objects, et comment **copy range to workbook** en toute sécurité sans perdre les formules ou le formatage. Aucun script externe n'est requis — juste un projet Java unique qui utilise Aspose.Cells for Java.

## Prérequis

* Java Development Kit 17 ou une version ultérieure.
* Maven ou Gradle pour gérer les dépendances.
* Une licence valide d'Aspose.Cells for Java (l'évaluation gratuite fonctionne pour les tests).
* Deux fichiers Excel : `source.xlsx` (contient le tableau croisé dynamique) et un `destination.xlsx` vide (ou laissez le code le créer).

## Étape 1 : Configurer le projet Maven

Créez un `pom.xml` qui inclut Aspose.Cells. Cette dépendance vous fournit les classes `Workbook`, `Worksheet` et `Range` utilisées dans l'exemple.

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" 
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 
         http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.example</groupId>
    <artifactId>excel-pivot-copy</artifactId>
    <version>1.0.0</version>
    <properties>
        <java.version>17</java.version>
    </properties>

    <dependencies>
        <dependency>
            <groupId>com.aspose</groupId>
            <artifactId>aspose-cells</artifactId>
            <version>24.10</version> <!-- latest at time of writing -->
        </dependency>
    </dependencies>
</project>
```

> **Astuce :** Gardez la version d'Aspose.Cells à jour ; les versions plus récentes offrent un meilleur support pour les structures de cache de tableau croisé dynamique complexes.

## Étape 2 : Charger le classeur source contenant le tableau croisé dynamique

Le premier bloc de code montre comment **how to copy excel** des données en chargeant le fichier source. Le constructeur `Workbook` lit le fichier complet en mémoire, en préservant tous les objets de feuille, y compris les tableaux croisés dynamiques.

```java
import com.aspose.cells.*;

public class PivotCopyDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook containing the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");

        // Access the first worksheet (index 0) where the pivot resides
        Worksheet srcWs = srcWb.getWorksheets().get(0);
```

*Pourquoi c'est important :* Aspose.Cells stocke les tableaux croisés dynamiques comme partie du modèle interne de la feuille de calcul. Charger le classeur garantit que le cache du tableau croisé dynamique est disponible pour la copie ultérieure.

## Étape 3 : Définir la plage qui inclut le tableau croisé dynamique

Un tableau croisé dynamique peut s'étendre sur plusieurs lignes et colonnes. Dans la plupart des cas, vous pouvez copier toute la plage utilisée de la feuille. La méthode `createRange` crée un objet `Range` que l'opération de copie gérera.

```java
        // Define the range to copy – includes the pivot table and its source data
        // Adjust the address if your pivot occupies a different block
        Range srcRange = srcWs.getCells().createRange("A1:H20");
```

Si le tableau croisé dynamique s'étend au-delà de `H20`, modifiez simplement la chaîne d'adresse. Cette étape est le cœur du traitement de **duplicate excel range** ; l'objet range connaît les formules, les styles et les lignes masquées.

## Étape 4 : Créer un nouveau classeur qui recevra la plage copiée

Vous pouvez soit commencer avec un classeur vierge, soit charger un fichier de destination existant. Ici, nous créons un nouveau classeur, ce qui est la façon la plus propre de **copy range to workbook**.

```java
        // Create a new workbook for the destination
        Workbook destWb = new Workbook(); // starts with one default sheet
        Worksheet destWs = destWb.getWorksheets().get(0);
```

> **Remarque :** Si vous devez copier le tableau croisé dynamique dans un nom de feuille spécifique, renommez `destWs` avec `destWs.setName("Report")` avant le collage.

## Étape 5 : Copier la plage – Aspose.Cells préserve automatiquement le tableau croisé dynamique

La méthode `copy` transfère tout le contenu de la plage source, y compris la définition du tableau croisé dynamique, le cache et le formatage. Aucun code supplémentaire n'est nécessaire pour que le tableau croisé dynamique reste fonctionnel.

```java
        // Copy the range to the destination worksheet; pivot tables are preserved automatically
        srcRange.copy(destWs.getCells().createRange("A1"));
```

*Pourquoi cela fonctionne :* Aspose.Cells considère le tableau croisé dynamique comme une collection de cellules cachées et de métadonnées attachées à la plage. Lorsque vous appelez `copy`, la bibliothèque réplique ces métadonnées dans le classeur cible.

## Étape 6 : Enregistrer le classeur de destination

Enfin, écrivez le résultat sur le disque. Le fichier enregistré contient un tableau croisé dynamique identique que vous pouvez actualiser ou modifier comme l'original.

```java
        // Save the destination workbook
        destWb.save("YOUR_DIRECTORY/destination.xlsx");

        System.out.println("Pivot table copied successfully.");
    }
}
```

L'exécution du programme affiche une confirmation et crée `destination.xlsx` avec un tableau croisé dynamique pleinement fonctionnel.

## Exemple complet et exécutable

En regroupant toutes les étapes, la classe Java complète ressemble à ceci :

```java
import com.aspose.cells.*;

public class PivotCopyDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load source workbook with pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // 2️⃣ Define the range that contains the pivot and its source data
        Range srcRange = srcWs.getCells().createRange("A1:H20");

        // 3️⃣ Prepare destination workbook (blank by default)
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);

        // 4️⃣ Copy range – pivot table is kept intact
        srcRange.copy(destWs.getCells().createRange("A1"));

        // 5️⃣ Save the new file
        destWb.save("YOUR_DIRECTORY/destination.xlsx");
        System.out.println("Pivot table copied successfully.");
    }
}
```

### Résultat attendu

* Console : `Pivot table copied successfully.`
* `destination.xlsx` s'ouvre dans Excel avec un tableau croisé dynamique identique à celui de `source.xlsx`. Actualiser le tableau montre la même source de données, prouvant que **how to copy pivot** fonctionne comme prévu.

## Gestion des variations courantes

### Copier plusieurs feuilles de calcul

Si votre projet nécessite de copier plusieurs feuilles, parcourez les feuilles du classeur et répétez les étapes 2‑4 pour chaque feuille. Le tableau croisé dynamique de chaque feuille sera préservé indépendamment.

```java
for (int i = 0; i < srcWb.getWorksheets().getCount(); i++) {
    Worksheet src = srcWb.getWorksheets().get(i);
    Worksheet dest = destWb.getWorksheets().add();
    src.getCells().copy(dest.getCells());
}
```

### Conserver les connexions de données externes

Les tableaux croisés dynamiques qui s'appuient sur des sources de données externes conservent la chaîne de connexion après la copie. Cependant, le fichier de destination doit avoir accès à la même source de données. Vérifiez la connexion en ouvrant le tableau croisé dynamique et en consultant l'onglet **Data**.

### Gérer les cellules fusionnées

Si la plage source contient des cellules fusionnées, Aspose.Cells copie automatiquement la disposition des fusions. Néanmoins, validez le résultat si le classeur de destination utilise une largeur de colonne par défaut différente.

## Bonnes pratiques pour une copie fiable

| Pratique | Raison |
|----------|--------|
| Utiliser la plage réellement utilisée (`srcWs.getCells().getMaxDisplayRange()`) au lieu d'une adresse codée en dur | Garantit que le tableau croisé dynamique complet et ses données sources sont inclus. |
| Appliquer une licence avant les opérations lourdes | Évite le filigrane d'évaluation et améliore les performances. |
| Actualiser le tableau croisé dynamique après la copie (`pivotTable.refresh()`) si les données sources ont changé | Assure que la destination reflète les dernières valeurs. |
| Écrire des tests unitaires qui ouvrent le classeur de destination et vérifient que `pivotTable.getPivotFields().size()` correspond à celui de la source | Détecte la perte accidentelle de champs lors de futures modifications du code. |

## Conclusion

Vous savez maintenant comment **how to copy pivot** des tableaux croisés dynamiques entre des classeurs Excel en Java, ainsi que comment **copy range between workbooks**, **duplicate excel range**, et **copy range to workbook** tout en préservant le formatage et les formules. L'exemple utilise Aspose.Cells, qui abstrait la gestion XML de bas niveau requise par le SDK OpenXML.

Ensuite, explorez des sujets connexes tels que **updating pivot cache programmatically**, **exporting pivot data to CSV**, ou **creating pivot tables from scratch**. Chacun de ces sujets s'appuie sur les mêmes concepts présentés ici.

Bon codage, et n'hésitez pas à expérimenter avec des plages plus grandes, plusieurs tableaux croisés dynamiques ou des styles personnalisés – le même schéma s'applique à tous les scénarios.

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d'implémentation alternatives dans vos propres projets.

- [How to Create Pivot Tables in Excel Using Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [How to Copy Multiple Columns in Excel Using Aspose.Cells Java: A Complete Guide](/cells/english/java/range-management/copy-multiple-columns-excel-aspose-cells-java/)
- [Copy Images Between Sheets in Excel Using Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/images-shapes/copy-images-between-sheets-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}