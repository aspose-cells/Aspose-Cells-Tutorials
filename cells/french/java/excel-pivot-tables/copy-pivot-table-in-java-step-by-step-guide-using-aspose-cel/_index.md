---
category: general
date: 2026-08-04
description: Copier un tableau croisé dynamique avec Aspose.Cells pour Java. Apprenez
  comment copier une plage Excel, dupliquer un tableau croisé dynamique et copier
  une feuille de calcul contenant un tableau croisé dynamique en quelques lignes seulement.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- copy excel range
- copy range java
- duplicate pivot table
- copy worksheet with pivot
language: fr
lastmod: 2026-08-04
og_description: Copier un tableau croisé dynamique avec Aspose.Cells pour Java. Ce
  tutoriel vous guide à travers la copie d’une plage Excel, la duplication d’un tableau
  croisé dynamique et la conservation de toutes les données dans une nouvelle feuille
  de calcul.
og_image_alt: Screenshot of a Java program that copies a pivot table to a new worksheet
og_title: Copier un tableau croisé dynamique en Java – tutoriel complet Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Copy pivot table with Aspose.Cells for Java. Learn how to copy excel
    range, duplicate pivot table, and copy worksheet with pivot in just a few lines.
  headline: Copy pivot table in Java – step‑by‑step guide using Aspose.Cells
  type: TechArticle
- description: Copy pivot table with Aspose.Cells for Java. Learn how to copy excel
    range, duplicate pivot table, and copy worksheet with pivot in just a few lines.
  name: Copy pivot table in Java – step‑by‑step guide using Aspose.Cells
  steps:
  - name: '`CopyWithPivot.xlsx` appears in `YOUR_DIRECTORY`.'
    text: '`CopyWithPivot.xlsx` appears in `YOUR_DIRECTORY`.'
  - name: Opening the file in Excel shows a new sheet named **CopySheet**.
    text: Opening the file in Excel shows a new sheet named **CopySheet**.
  - name: '**CopySheet** contains a fully functional pivot table identical to the
      original, ready to refresh.'
    text: '**CopySheet** contains a fully functional pivot table identical to the
      original, ready to refresh.'
  - name: All formatting, filters, and calculated fields are preserved.
    text: All formatting, filters, and calculated fields are preserved.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
- PivotTable
- Data copying
title: Copier un tableau croisé dynamique en Java – guide étape par étape avec Aspose.Cells
url: /fr/java/excel-pivot-tables/copy-pivot-table-in-java-step-by-step-guide-using-aspose-cel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Copier un tableau croisé dynamique en Java – guide étape par étape avec Aspose.Cells

Si vous devez **copier un tableau croisé dynamique** d’une feuille de calcul à une autre en Java, ce guide vous montre exactement comment le faire avec Aspose.Cells. Que vous génériez des rapports de manière programmatique ou que vous construisiez un outil de migration de données, vous verrez un exemple complet et exécutable qui préserve la définition et les données du tableau croisé dynamique.

Copier un tableau croisé dynamique, c’est plus que copier une plage de cellules ; le cache sous‑jacent et la source de données doivent rester intacts. Dans ce tutoriel, nous abordons également comment **copier une plage Excel**, comment **dupliquer un tableau croisé dynamique** entre feuilles, et comment **copier une feuille avec le tableau croisé dynamique** en utilisant la même API.

## Prérequis

Avant de commencer, assurez‑vous d’avoir :

* Java Development Kit (JDK) 8 ou supérieur.  
* Maven ou Gradle pour gérer les dépendances.  
* Aspose.Cells for Java (la dernière version, par ex., 23.12). Ajoutez la coordonnée Maven suivante à votre `pom.xml` :

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
</dependency>
```

* Un classeur source (`Source.xlsx`) contenant un tableau croisé dynamique sur la première feuille.

## Comment copier un tableau croisé dynamique en Java avec Aspose.Cells

L’idée principale est de copier la *plage source* qui englobe le tableau croisé dynamique, puis de la coller dans une nouvelle feuille. Aspose.Cells copie automatiquement le cache du tableau, de sorte que la feuille résultante contient un **tableau croisé dynamique dupliqué** pleinement fonctionnel.

```java
import com.aspose.cells.*;

public class CopyPivotTableDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the workbook that contains the PivotTable
        Workbook workbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");

        // Step 2: Define the source range (including the PivotTable) to be copied
        // The range must cover the entire pivot table area, e.g., A1:G20
        Range sourceRange = workbook.getWorksheets()
                                    .get(0)                 // first worksheet
                                    .getCells()
                                    .createRange("A1:G20");

        // Step 3: Add a new worksheet that will receive the copied range
        Worksheet destinationSheet = workbook.getWorksheets().add("CopySheet");

        // Step 4: Copy the source range to cell A1 of the new worksheet
        sourceRange.copy(destinationSheet.getCells().createRange("A1"));

        // Step 5: Save the workbook with the copied PivotTable intact
        workbook.save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
    }
}
```

### Pourquoi cela fonctionne

* **La copie de la plage inclut le cache du tableau** – Aspose.Cells traite un tableau croisé dynamique comme un objet spécial intégré à la plage de cellules. Lorsque vous appelez `Range.copy`, la bibliothèque copie à la fois les cellules visibles et le cache caché qui alimente le tableau.  
* **Aucune recréation manuelle nécessaire** – Vous n’avez pas besoin de reconstruire les champs du tableau ou la source de données ; le duplicata est prêt à être actualisé immédiatement.  
* **Compatible avec toutes les versions d’Excel** – Le fichier généré suit la norme Office Open XML (XLSX), de sorte qu’Excel 2007+ peut l’ouvrir sans avertissement.

## Copier une plage Excel – réutiliser le même code pour des données sans tableau croisé dynamique

Si vous avez seulement besoin de **copier une plage Excel** sans tableau croisé dynamique, le même schéma s’applique. Il suffit d’ajuster l’adresse de la plage à la région que vous souhaitez dupliquer.

```java
// Example: copy A1:D10 from Sheet1 to Sheet2
Range dataRange = workbook.getWorksheets()
                          .get(0)
                          .getCells()
                          .createRange("A1:D10");
Worksheet sheet2 = workbook.getWorksheets().add("DataCopy");
dataRange.copy(sheet2.getCells().createRange("A1"));
```

La méthode `copy` préserve les formules, le formatage et les commentaires, ce qui en fait une solution universelle pour tout bloc de données Excel.

## Dupliquer un tableau croisé dynamique sur plusieurs feuilles

Parfois, vous devez **dupliquer un tableau croisé dynamique** plusieurs fois — par exemple, une fois par département. Parcourez les feuilles de destination et réutilisez le même appel `sourceRange.copy` :

```java
String[] departments = {"Sales", "Marketing", "Finance"};
for (String dept : departments) {
    Worksheet ws = workbook.getWorksheets().add(dept + "Pivot");
    sourceRange.copy(ws.getCells().createRange("A1"));
}
```

Chaque nouvelle feuille contient un tableau indépendant qui peut être actualisé séparément. Le cache est dupliqué, de sorte que les modifications dans une feuille n’affectent pas les autres.

## Copier une feuille avec le tableau croisé dynamique – préservation des paramètres au niveau de la feuille

Si vous voulez **copier une feuille avec le tableau croisé dynamique** tout en conservant la mise en page, les largeurs de colonnes et les plages nommées, utilisez `Worksheet.copy` au lieu de copier manuellement une plage. Cette méthode clone la feuille entière, y compris le tableau croisé dynamique.

```java
Worksheet original = workbook.getWorksheets().get(0);
Worksheet clone = workbook.getWorksheets().addCopy(original);
clone.setName("FullCopy");
workbook.save("YOUR_DIRECTORY/FullCopy.xlsx");
```

`addCopy` est pratique lorsque la feuille contient des graphiques, des images ou des styles personnalisés qui doivent être transportés avec le tableau.

## Pièges courants et comment les éviter

| Problème | Pourquoi cela se produit | Solution |
|----------|--------------------------|----------|
| **Cache du tableau perdu après la copie** | Utilisation de `Cell.copy` sur des cellules individuelles (au lieu d’une plage) qui supprime le cache caché. | Copiez toujours la *plage entière* qui englobe le tableau croisé dynamique, comme indiqué à l’étape 2. |
| **Plage source trop petite** | La plage n’inclut pas la zone de données du tableau, de sorte que la nouvelle feuille n’affiche que des valeurs statiques. | Étendez l’adresse (par ex., `A1:G20`) pour couvrir le tableau complet ainsi que les segments ou filtres éventuels. |
| **Incompatibilité de version du classeur de destination** | Enregistrement au format XLS (hérité) supprime les fonctionnalités modernes du tableau. | Enregistrez au format XLSX (par défaut) ou définissez explicitement `SaveFormat.XLSX`. |
| **Source de données externe cassée** | Le tableau pointe vers une source de données hors du classeur ; la copie ne l’incorpore pas. | Utilisez `PivotTable.refreshData()` après la copie, ou intégrez les données sources dans le même classeur. |

## Résultat attendu

Après l’exécution du programme :

1. `CopyWithPivot.xlsx` apparaît dans `YOUR_DIRECTORY`.  
2. L’ouverture du fichier dans Excel montre une nouvelle feuille nommée **CopySheet**.  
3. **CopySheet** contient un tableau croisé dynamique pleinement fonctionnel, identique à l’original, prêt à être actualisé.  
4. Tout le formatage, les filtres et les champs calculés sont préservés.

Si vous ouvrez `FullCopy.xlsx`, vous verrez une réplique complète de la feuille source, y compris les graphiques ou images qui s’y trouvaient.

## Récapitulatif

* Vous avez appris comment **copier un tableau croisé dynamique** en Java avec Aspose.Cells.  
* La même approche fonctionne pour un simple **copier une plage Excel** ou des scénarios **copier plage java**.  
* Pour des opérations en masse, vous pouvez **dupliquer un tableau croisé dynamique** sur de nombreuses feuilles.  
* Lorsque vous avez besoin de la feuille entière, **copiez une feuille avec le tableau croisé dynamique** en utilisant `addCopy`.

## Prochaines étapes

* Explorez **PivotTable.refreshData()** pour mettre à jour programmétiquement le cache après la copie.  
* Combinez la logique de copie avec le **streaming de fichiers Excel** afin de gérer de gros classeurs sans tout charger en mémoire.  
* Consultez le support d’Aspose.Cells pour les **segments de tableau croisé dynamique** si vos rapports reposent sur des filtres interactifs.

N’hésitez pas à adapter le code à la structure de votre projet, à expérimenter avec différentes tailles de plage, ou à l’intégrer dans un pipeline de traitement de données plus large. Bon codage !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et à explorer des approches d’implémentation alternatives dans vos propres projets.

- [Comment mettre à jour la source du tableau croisé dynamique Excel avec Aspose.Cells pour Java : guide complet](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Manipulation de tableau croisé dynamique Excel avec Aspose Cells Java](/cells/hongkong/java/data-analysis/excel-pivot-table-manipulation-aspose-cells-java/)
- [Créer un nouveau classeur Excel – Copier & dupliquer le tableau croisé dynamique](/cells/english/net/pivot-tables/create-new-excel-workbook-copy-duplicate-pivot-table/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}