---
category: general
date: 2026-09-27
description: Copier un tableau croisé dynamique en Java avec Aspose.Cells – un guide
  étape par étape qui montre comment copier une plage et préserver les définitions
  du tableau croisé dynamique.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- how to copy pivot table
- copy range aspose cells
language: fr
lastmod: 2026-09-27
og_description: Copier un tableau croisé dynamique en Java avec Aspose.Cells. Suivez
  ce tutoriel complet pour copier une plage avec Aspose.Cells et conserver les définitions
  du tableau croisé dynamique intactes.
og_image_alt: Screenshot of copy pivot table operation in Aspose.Cells Java
og_title: Copier un tableau croisé dynamique en Java – Guide rapide d’Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Copy pivot table in Java with Aspose.Cells – a step‑by‑step guide that
    shows how to copy range and preserve pivot definitions.
  headline: How to copy a pivot table in Java using Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
title: Comment copier un tableau croisé dynamique en Java avec Aspose.Cells
url: /fr/java/excel-pivot-tables/how-to-copy-a-pivot-table-in-java-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment copier un tableau croisé dynamique en Java avec Aspose.Cells

Si vous devez **copy pivot table** d'un classeur à un autre, ce guide vous montre exactement comment le faire avec Aspose.Cells for Java. La solution fonctionne pour tout tableau croisé dynamique que vous avez créé, et elle préserve la définition du tableau sans recréation manuelle.

Vous apprendrez comment charger le fichier source, définir la plage qui contient le tableau croisé dynamique, copier cette plage dans un nouveau classeur, puis enregistrer le résultat. Le tutoriel couvre également les pièges courants, comme la préservation des sources de données et la gestion de classeurs volumineux.

## Ce dont vous aurez besoin

* Java 17 ou version ultérieure (le code se compile également avec JDK 8+)
* Aspose.Cells for Java 23.9 ou plus récent – la dernière version offre le support le plus fiable de **copy range aspose cells**
* Un fichier Excel source contenant un tableau croisé dynamique (par ex., `SourceWithPivot.xlsx`)
* Un IDE ou un outil de construction (Maven/Gradle) capable de référencer le JAR Aspose.Cells

## Étape 1 : Charger le classeur source qui contient le tableau croisé dynamique

La première action consiste à ouvrir le classeur qui contient le tableau que vous souhaitez dupliquer. Le chargement du fichier crée une représentation en mémoire de toutes les feuilles, cellules et caches de tableau croisé dynamique.

```java
import com.aspose.cells.*;

public class CopyPivotTable {
    public static void main(String[] args) throws Exception {
        // Load the source workbook
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
        // Access the first worksheet (adjust the index if needed)
        Worksheet srcWs = srcWb.getWorksheets().get(0);
```

**Pourquoi cela importe :**  
Aspose.Cells lit l'intégralité du classeur, y compris les feuilles de cache de tableau croisé dynamique masquées. Si vous sautez cette étape, l'opération suivante de **copy pivot table** perdrait la source de données sous‑jacente.

## Étape 2 : Créer un classeur de destination vide

Ensuite, créez une nouvelle instance de classeur qui recevra le tableau copié. Partir d’un classeur vierge évite les écrasements accidentels.

```java
        // Create an empty destination workbook
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);
```

**Astuce :** Le classeur par défaut contient une feuille vide, ce qui est parfait pour une copie simple. Si vous devez copier dans une feuille nommée spécifiquement, renommez `destWs` avec `destWs.setName("TargetSheet")`.

## Étape 3 : Définir la plage source qui inclut le tableau croisé dynamique

Un tableau croisé dynamique occupe un bloc rectangulaire de cellules. Vous devez spécifier la plage exacte ; sinon seules les données brutes seront copiées. Dans cet exemple, nous supposons que le tableau occupe **A1:G20**, mais vous pouvez ajuster l’adresse pour correspondre à votre fichier.

```java
        // Define the range that includes the pivot table
        Range srcRange = srcWs.getCells().createRange("A1:G20");
```

**Pourquoi cela fonctionne :**  
Lorsque vous appelez `createRange` sur la collection `Cells` de la feuille, Aspose.Cells inclut la définition du tableau, son cache et tout le formatage. C’est le cœur du **how to copy pivot table** correctement.

## Étape 4 : Copier la plage définie vers la feuille de destination

Utilisez maintenant la méthode `copy` pour dupliquer la plage. La méthode copie tout ce qui se trouve dans la plage, y compris la définition du tableau, les formules et les styles.

```java
        // Copy the range (pivot table definition is included) to the destination sheet
        srcRange.copy(destWs.getCells().createRange("A1"));
```

**Note importante :**  
Si vous ne avez besoin que des données sans le tableau, vous pourriez utiliser `srcRange.copyData`. Cependant, pour un vrai **copy pivot table**, vous devez copier la plage entière comme indiqué ci‑dessus.

## Étape 5 : Enregistrer le classeur de destination

Enfin, écrivez le nouveau classeur sur le disque. Le fichier résultant contiendra un tableau croisé dynamique pleinement fonctionnel, identique à celui de la source.

```java
        // Save the destination workbook
        destWb.save("YOUR_DIRECTORY/CopyPivotResult.xlsx");
    }
}
```

L’exécution du programme produit `CopyPivotResult.xlsx` avec la même mise en page, les mêmes filtres et les mêmes calculs que le fichier original.

## Résultat attendu

Lorsque vous ouvrez `CopyPivotResult.xlsx` dans Excel :

* Le tableau croisé dynamique apparaît en **A1:G20** sur la première feuille.
* Tous les champs de lignes/colonnes, filtres et champs de valeurs sont intacts.
* Actualiser le tableau met à jour la même source de données que le classeur source (si les données source sont intégrées).

## Cas limites et conseils pratiques

| Situation | Comment le gérer |
|-----------|------------------|
| **Pivot spans more columns than anticipated** | Utilisez `srcWs.getPivotTables().get(0).getPivotTableArea()` pour obtenir l’adresse exacte de façon programmatique. |
| **Source workbook contains multiple pivots** | Parcourez `srcWs.getPivotTables()` et copiez chaque plage individuellement, en ajustant les adresses de destination. |
| **Large workbooks cause memory pressure** | Activez `WorkbookSettings.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` avant de charger la source. |
| **You need to copy only the pivot definition, not the data** | Après la copie, supprimez les lignes de données sources dans la destination avec `destWs.getCells().deleteRows(startRow, count)`. |
| **Destination file must keep original formatting** | Définissez `CopyOptions` avec `options.setPasteType(PasteType.ALL)` pour une copie à pleine fidélité. |

**Conseil pro :** Vérifiez toujours le tableau copié en appelant `destWs.getPivotTables().get(0).refresh()` de façon programmatique. Cela garantit que le cache est à jour, surtout lorsque les données source résident dans une connexion externe.

## Exemple complet exécutable

Voici le programme complet que vous pouvez copier‑coller dans votre IDE. Remplacez `YOUR_DIRECTORY` par le chemin réel sur votre machine.

```java
import com.aspose.cells.*;

public class CopyPivotTable {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the source workbook that contains the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // Step 2: Create an empty destination workbook
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);

        // Step 3: Define the range that includes the pivot table in the source sheet
        // Adjust the address if your pivot occupies a different area
        Range srcRange = srcWs.getCells().createRange("A1:G20");

        // Step 4: Copy the defined range (pivot table definition is included) to the destination sheet
        srcRange.copy(destWs.getCells().createRange("A1"));

        // Step 5: Save the destination workbook with the copied pivot table
        destWb.save("YOUR_DIRECTORY/CopyPivotResult.xlsx");
    }
}
```

L’exécution de ce code **copy pivot table** exactement comme décrit, et il montre la manière la plus simple de **copy range aspose cells** tout en préservant la fonctionnalité du tableau.

## Conclusion

Vous savez maintenant comment **copy pivot table** en Java avec Aspose.Cells, depuis le chargement du classeur source jusqu’à l’enregistrement du fichier de destination. Le guide a couvert les étapes essentielles, expliqué pourquoi chaque étape est importante, et abordé les cas limites courants.  

Ensuite, vous pourriez explorer :

* **how to copy pivot table** entre différentes feuilles du même classeur
* Utiliser **copy range aspose cells** pour dupliquer des graphiques ou du formatage conditionnel
* Automatiser le rafraîchissement du tableau après la copie pour garder les données à jour

N’hésitez pas à expérimenter avec des plages plus grandes, plusieurs tableaux, ou à intégrer cette logique dans un pipeline de traitement Excel plus vaste. Bon codage !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications pas à pas pour vous aider à maîtriser d’autres fonctionnalités de l’API et explorer des approches d’implémentation alternatives dans vos projets.

- [Copier un tableau croisé dynamique en Java – Le préserver, l’exporter en PPTX](/cells/english/java/excel-pivot-tables/copy-pivot-table-in-java-preserve-it-export-to-pptx/)
- [Comment mettre à jour la source d’un tableau croisé dynamique Excel avec Aspose.Cells for Java : Guide complet](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Manipulation de tableaux croisés dynamiques Excel avec Aspose.Cells Java : Guide complet](/cells/english/java/data-analysis/excel-pivot-table-manipulation-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}