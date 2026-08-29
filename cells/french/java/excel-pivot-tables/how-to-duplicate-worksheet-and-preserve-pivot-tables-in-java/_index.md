---
category: general
date: 2026-08-17
description: Comment dupliquer une feuille de calcul en Java avec Aspose.Cells, en
  préservant le tableau croisé dynamique, copier le tableau croisé dynamique dans
  un nouveau classeur, et créer un classeur à partir d’une feuille.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to duplicate worksheet
- how to copy pivot
- how to preserve pivot
- copy pivot to workbook
- create workbook from sheet
language: fr
lastmod: 2026-08-17
og_description: Comment dupliquer une feuille de calcul en Java avec Aspose.Cells,
  en conservant le tableau croisé dynamique, copier le tableau croisé dynamique vers
  un nouveau classeur, et créer un classeur à partir d’une feuille — toutes les étapes
  expliquées.
og_image_alt: Screenshot of Java code duplicating an Excel worksheet with a pivot
  table using Aspose.Cells
og_title: Comment dupliquer une feuille de calcul et conserver les tableaux croisés
  dynamiques – Guide Java
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: How to duplicate worksheet in Java using Aspose.Cells, preserving the
    pivot table, copying pivot to a new workbook, and creating a workbook from a sheet.
  headline: How to duplicate worksheet and preserve pivot tables in Java
  type: TechArticle
- description: How to duplicate worksheet in Java using Aspose.Cells, preserving the
    pivot table, copying pivot to a new workbook, and creating a workbook from a sheet.
  name: How to duplicate worksheet and preserve pivot tables in Java
  steps:
  - name: – Load the workbook that contains the pivot table
    text: '```java import com.aspose.cells.*;'
  - name: – Create a new workbook and duplicate the entire worksheet
    text: '```java // Create an empty destination workbook Workbook destinationWorkbook
      = new Workbook();'
  - name: – Save the new workbook
    text: '```java // Save the duplicated workbook; the pivot remains functional destinationWorkbook.save("YOUR_DIRECTORY/copy_with_pivot.xlsx");
      } } ```'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- Pivot Table
- Workbook
title: Comment dupliquer une feuille de calcul et préserver les tableaux croisés dynamiques
  en Java
url: /fr/java/excel-pivot-tables/how-to-duplicate-worksheet-and-preserve-pivot-tables-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment dupliquer une feuille de calcul et préserver les tableaux croisés dynamiques en Java

Dupliquer une feuille de calcul tout en conservant son tableau croisé dynamique intact est un besoin fréquent lorsque vous automatisez les rapports Excel. Ce guide vous montre comment copier un tableau croisé dynamique vers un nouveau classeur à l'aide d'Aspose.Cells for Java, et couvre également comment préserver le tableau croisé dynamique lorsque vous créez un classeur à partir d'une feuille.

Vous apprendrez comment charger un classeur existant, dupliquer la feuille contenant un tableau croisé dynamique, et enregistrer le résultat dans un nouveau fichier. Le tutoriel suppose que vous disposez d'un environnement de développement Java de base et d'une licence valide Aspose.Cells (l'évaluation gratuite suffit pour les tests). Aucun outil externe n'est requis au-delà du JAR Aspose.Cells.

## Prérequis

* Kit de développement Java (JDK) 8 ou plus récent.
* Maven ou Gradle pour gérer la dépendance Aspose.Cells.
* Un fichier Excel (`source.xlsx`) contenant au moins un tableau croisé dynamique sur la première feuille.
* Un répertoire où vous pouvez lire le fichier source et écrire le classeur dupliqué.

Ajoutez la dépendance Aspose.Cells à votre `pom.xml` (Maven) ou `build.gradle` (Gradle). Pour Maven :

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- use the latest version -->
</dependency>
```

## Comment dupliquer une feuille de calcul avec un tableau croisé dynamique

L'opération principale est un processus en trois étapes : charger, copier et enregistrer. Chaque étape est expliquée ci-dessous.

### Étape 1 – Charger le classeur qui contient le tableau croisé dynamique

```java
import com.aspose.cells.*;

public class CopyPivotTable {
    public static void main(String[] args) throws Exception {
        // Load the source workbook that holds the pivot table
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet sourceWorksheet = sourceWorkbook.getWorksheets().get(0);
```

*Pourquoi cette étape est importante* : L'objet `Workbook` représente le fichier Excel complet. En récupérant la première feuille (`get(0)`), vous ciblez la feuille qui contient le tableau croisé dynamique que vous souhaitez dupliquer.

### Étape 2 – Créer un nouveau classeur et dupliquer la feuille entière

```java
        // Create an empty destination workbook
        Workbook destinationWorkbook = new Workbook();

        // Duplicate the source worksheet, preserving its pivot table
        destinationWorkbook.getWorksheets().addCopy(sourceWorksheet);
```

`addCopy` clone la feuille **y compris** tous les objets incorporés, les formules et les caches de tableau croisé dynamique. C'est la méthode recommandée pour **how to copy pivot** car la définition du tableau croisé dynamique et sa source de données sont transférées ensemble.

### Étape 3 – Enregistrer le nouveau classeur

```java
        // Save the duplicated workbook; the pivot remains functional
        destinationWorkbook.save("YOUR_DIRECTORY/copy_with_pivot.xlsx");
    }
}
```

Après exécution, `copy_with_pivot.xlsx` contient une copie exacte de la feuille originale, et le tableau croisé dynamique fonctionne sans configuration supplémentaire.

**Résultat attendu** : L'ouverture de `copy_with_pivot.xlsx` dans Excel montre la feuille dupliquée avec la même disposition du tableau croisé dynamique, les mêmes filtres et champs calculés que le fichier source.

## Comment copier un tableau croisé dynamique vers un autre classeur

Si vous devez déplacer un tableau croisé dynamique sans copier toute la feuille, vous pouvez extraire le cache du tableau croisé dynamique et l'attacher à une nouvelle feuille. L'extrait suivant illustre cette approche :

```java
// Assume sourceWorkbook and sourceWorksheet are already loaded
PivotTable pivot = sourceWorksheet.getPivotTables().get(0);

// Create a new workbook and a blank worksheet
Workbook targetWorkbook = new Workbook();
Worksheet targetSheet = targetWorkbook.getWorksheets().add("PivotCopy");

// Import the pivot table definition
targetSheet.getPivotTables().addCopy(pivot);
targetWorkbook.save("YOUR_DIRECTORY/pivot_only_copy.xlsx");
```

Ce code répond à **how to copy pivot** en copiant uniquement l'objet tableau croisé dynamique, pas la feuille entière. La méthode `addCopy` sur la collection `PivotTables` garantit que le cache du tableau croisé dynamique est dupliqué, répondant aux exigences de **how to preserve pivot**.

## Comment préserver le tableau croisé dynamique lors de la création d'un classeur à partir d'une feuille

Parfois, vous commencez avec une feuille qui n'appartient pas à un classeur (par exemple, vous générez une feuille en mémoire). Pour **create workbook from sheet** tout en conservant le tableau croisé dynamique, suivez ces étapes :

```java
// Create a worksheet in memory
Worksheet tempSheet = new Worksheet();
PivotTable pivot = tempSheet.getPivotTables().add("A1", "B10", "MyPivot");

// Configure the pivot source range, rows, columns, data fields, etc.
// (Omitted for brevity – see Aspose.Cells docs for detailed setup)

// Wrap the worksheet in a new workbook
Workbook newWorkbook = new Workbook();
newWorkbook.getWorksheets().addCopy(tempSheet);
newWorkbook.save("YOUR_DIRECTORY/created_from_sheet.xlsx");
```

En ajoutant la feuille à un nouveau `Workbook` après que le tableau croisé dynamique soit entièrement défini, vous garantissez que **how to preserve pivot** fonctionne même lorsque la feuille provient d'un fichier inexistant.

## Conseils pratiques et pièges courants

| Conseil | Pourquoi c'est important |
|-----|----------------|
| Utilisez `addCopy` au lieu de `copy` | `addCopy` clone le cache sous-jacent du tableau croisé dynamique ; un simple `copy` peut perdre la connexion à la source de données. |
| Conservez les fichiers source et destination sur le même système de fichiers | Les chemins relatifs dans la source de données du tableau croisé dynamique sont résolus correctement, réduisant les erreurs « source non trouvée ». |
| Vérifiez le cache du tableau croisé dynamique après la copie | Appelez `pivot.refresh()` si les données source ont changé entre la copie et l'opération d'enregistrement. |
| Libérez les classeurs une fois terminé | `sourceWorkbook.dispose();` libère les ressources natives, ce qui est important pour les gros fichiers. |

## Cas limites que vous pourriez rencontrer

* **Feuilles multiples avec des tableaux croisés dynamiques interdépendants** – Copiez chaque feuille individuellement ; les caches partagés sont dupliqués automatiquement, mais il peut être nécessaire de réaffecter les connexions de données externes.
* **Tableaux croisés dynamiques basés sur des requêtes SQL externes** – Assurez-vous que l'environnement de destination peut accéder à la même base de données ; sinon le tableau croisé dynamique affichera des erreurs « #REF! ».
* **Classeur volumineux (>100 Mo)** – Utilisez `WorkbookSettings.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` pour réduire la pression mémoire pendant l'opération de copie.

## Exemple complet et exécutable

Voici le programme complet qui intègre toutes les étapes décrites. Enregistrez-le sous le nom `CopyPivotTable.java`, ajustez les chemins de fichiers, et exécutez-le avec votre IDE préféré ou via `javac`/`java`.



## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d'implémentation alternatives dans vos propres projets.

- [Comment créer des tableaux croisés dynamiques dans Excel à l'aide d'Aspose.Cells pour Java : guide complet](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [Comment mettre à jour la source d'un tableau croisé dynamique Excel avec Aspose.Cells pour Java : guide complet](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Comment implémenter des segments (slicers) dans les tableaux croisés dynamiques à l'aide d'Aspose.Cells pour Java : guide complet](/cells/english/java/data-analysis/implement-slicers-pivot-tables-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}