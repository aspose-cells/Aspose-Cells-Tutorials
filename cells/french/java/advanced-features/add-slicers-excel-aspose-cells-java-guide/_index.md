---
date: '2026-09-02'
description: Apprenez comment ajouter un segment aux classeurs Excel à l'aide d'Aspose.Cells
  for Java, permettant un filtrage de données puissant, des tableaux de bord interactifs
  et une analyse plus rapide.
keywords:
- how to add slicer
- load excel workbook java
- filter data excel slicer
- insert slicer worksheet
- aspose cells filtering
lastmod: '2026-09-02'
og_description: Comment ajouter un segment à Excel avec Aspose.Cells for Java – un
  guide étape par étape qui vous montre comment charger un classeur, attacher un segment
  interactif et enregistrer le fichier pour un reporting dynamique.
og_image_alt: Developer guide showing Java code that adds an Excel slicer using Aspose.Cells
og_title: Comment ajouter un segment à Excel avec Aspose.Cells for Java
schemas:
- author: Aspose
  dateModified: '2026-09-02'
  description: Learn how to add slicer to Excel workbooks using Aspose.Cells for Java,
    enabling powerful data filtering, interactive dashboards, and faster analysis.
  headline: How to add slicer to Excel with Aspose.Cells for Java
  type: TechArticle
- description: Learn how to add slicer to Excel workbooks using Aspose.Cells for Java,
    enabling powerful data filtering, interactive dashboards, and faster analysis.
  name: How to add slicer to Excel with Aspose.Cells for Java
  steps:
  - name: '**Free trial:** Download the library and experiment with its capabilities.'
    text: '**Free trial:** Download the library and experiment with its capabilities.'
  - name: '**Temporary license:** Request a temporary license for extended testing
      at [Aspose''s Temporary License Page](https://purchase.aspose.com/temporary-license/).'
    text: '**Temporary license:** Request a temporary license for extended testing
      at [Aspose''s Temporary License Page](https://purchase.aspose.com/temporary-license/).'
  - name: '**Purchase license:** For production use, buy a full license from [Aspose
      Purchase](https://purchase.aspose.com/buy).'
    text: '**Purchase license:** For production use, buy a full license from [Aspose
      Purchase](https://purchase.aspose.com/buy).'
  - name: '**Financial reporting:** Filter quarterly sales figures with a single click
      to spot trends.'
    text: '**Financial reporting:** Filter quarterly sales figures with a single click
      to spot trends.'
  - name: '**Inventory management:** View stock levels by product category without
      rebuilding queries.'
    text: '**Inventory management:** View stock levels by product category without
      rebuilding queries.'
  - name: '**HR analytics:** Quickly compare employee performance across departments.'
    text: '**HR analytics:** Quickly compare employee performance across departments.'
  type: HowTo
- questions:
  - answer: Yes – call `worksheet.getSlicers().add` repeatedly with different column
      indexes or positions.
    question: Can I add multiple slicers to the same table?
  - answer: Absolutely – the same `add` method works with pivot tables as long as
      they exist on the worksheet.
    question: Does Aspose.Cells support slicers for PivotTables?
  - answer: You can modify properties such as `setStyle`, `setCaption`, `setWidth`,
      and `setHeight` after creation.
    question: Is it possible to customize slicer style programmatically?
  - answer: Aspose.Cells for Java 25.3 supports Java 8 and newer, including Java 11,
      17, and later LTS releases.
    question: What Java versions are compatible?
  - answer: Use `worksheet.getSlicers().removeAt(index)`, where `index` corresponds
      to the slicer’s position in the collection.
    question: How do I remove a slicer that is no longer needed?
  type: FAQPage
tags:
- add slicer
- Aspose.Cells
- Java Excel automation
- data filtering
- Excel slicer
title: Comment ajouter un segment à Excel avec Aspose.Cells for Java
url: /fr/java/advanced-features/add-slicers-excel-aspose-cells-java-guide/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment ajouter un slicer à Excel avec Aspose.Cells for Java

## Introduction

Dans les applications modernes axées sur les données, **comment ajouter un slicer** aux classeurs Excel est une exigence fréquente pour les développeurs qui ont besoin de rapports interactifs et prêts à filtrer. Aspose.Cells for Java vous permet d’insérer programmaticalement des slicers dans des tableaux, offrant aux utilisateurs finaux la même expérience de clic‑à‑filtrer qu’ils obtiennent dans l’interface de bureau. Dans ce guide, vous verrez pourquoi les slicers sont importants, comment configurer la bibliothèque, et le code exact nécessaire pour charger un classeur, y attacher un slicer et enregistrer le résultat.

**Ce que vous apprendrez**
- Comment afficher la version actuelle d’Aspose.Cells for Java  
- Comment **charger un classeur Excel Java** et atteindre la feuille cible  
- Comment localiser un tableau spécifique et y attacher un slicer  
- Comment utiliser le slicer pour **filtrer les données style Excel slicer**  
- Comment enregistrer le classeur modifié  

Avant de commencer, assurez‑vous d’avoir les prérequis listés ci‑dessous.

## Réponses rapides
- **Qu’est‑ce qu’un slicer ?** Un filtre visuel interactif qui permet aux utilisateurs de restreindre instantanément les données d’un tableau ou d’un tableau croisé dynamique.  
- **Quelle version d’Aspose.Cells est requise ?** Aspose.Cells for Java 25.3 ou ultérieure.  
- **Ai‑je besoin d’une licence ?** Un essai gratuit suffit pour l’évaluation ; une licence est obligatoire pour les déploiements en production.  
- **Puis‑je charger un classeur existant ?** Oui – instanciez `new Workbook("path/to/file.xlsx")`.  
- **Le slicer se comportera‑t‑il comme le slicer natif d’Excel ?** Absolument – il offre la même interface utilisateur et les mêmes capacités de filtrage.

## Comment ajouter un slicer à Excel en utilisant Aspose.Cells for Java ?

Pour ajouter un slicer, chargez d’abord le classeur cible, puis créez un objet slicer lié à la colonne du tableau souhaitée, positionnez le slicer sur la feuille de calcul, et enfin enregistrez le classeur. Les étapes ci‑dessous détaillent chacune de ces actions, en fournissant des extraits de code pour la configuration du projet, la création du slicer, son placement et la sortie du fichier.

### Prérequis

Avant d’implémenter Aspose.Cells for Java, assurez‑vous d’avoir :

#### Bibliothèques requises et versions

Incluez Aspose.Cells comme dépendance en utilisant Maven ou Gradle :

**Maven :**
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle :**
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

#### Exigences de configuration de l’environnement
- Java Development Kit (JDK) 8 ou version supérieure installé.  
- Un IDE tel qu’IntelliJ IDEA ou Eclipse pour éditer et exécuter le code.

#### Prérequis de connaissances
Des connaissances de base en programmation Java sont requises ; une familiarité avec la structure des fichiers Excel est utile mais pas obligatoire.

### Configuration d’Aspose.Cells for Java

Tout d’abord, obtenez une licence d’essai ou permanente depuis le site officiel :

#### Étapes d’obtention de licence
1. **Essai gratuit :** Téléchargez la bibliothèque et expérimentez ses capacités.  
2. **Licence temporaire :** Demandez une licence temporaire pour des tests prolongés sur [Aspose's Temporary License Page](https://purchase.aspose.com/temporary-license/).  
3. **Licence d’achat :** Pour une utilisation en production, achetez une licence complète sur [Aspose Purchase](https://purchase.aspose.com/buy).

#### Initialisation de base
Initialisez Aspose.Cells dans votre application Java :
```java
import com.aspose.cells.*;

public class SetupAsposeCells {
    public static void main(String[] args) throws Exception {
        // Set license if available
        License license = new License();
        license.setLicense("path/to/your/license/file.lic");

        System.out.println("Aspose.Cells is ready to use!");
    }
}
```
Avec la bibliothèque initialisée, vous êtes prêt à travailler avec des fichiers Excel.

## Pourquoi utiliser des slicers dans Excel ?

Les slicers vous offrent un filtrage instantané, basé sur le clic, sans écrire de formules ou de code VBA. Ils améliorent la lisibilité des tableaux de bord, permettent une exploration rapide des données et réduisent le besoin de multiples rapports statiques. Dans les déploiements à grande échelle, les slicers peuvent réduire le temps d’analyse jusqu’à 70 % car les utilisateurs n’ont plus besoin de reconstruire manuellement les requêtes.

## Filtrer les données avec un slicer

Les slicers sont le moyen visuel de **filtrer les données avec un slicer**. Une fois attachés à un tableau, les utilisateurs cliquent sur les boutons du slicer pour masquer ou afficher instantanément les lignes correspondant aux critères sélectionnés—aucune formule requise. Cette section explique pourquoi les slicers sont une révolution pour les rapports Excel interactifs.

## Guide d’implémentation

Voici un guide pas à pas qui montre exactement comment ajouter un slicer à un tableau Excel.

### Affichage de la version d’Aspose.Cells for Java

La classe `VersionInfo` fournit la version actuelle de la bibliothèque, ce qui est utile pour le débogage et le support.

`VersionInfo` est une classe utilitaire qui renvoie la chaîne de version d’Aspose.Cells.  
```java
System.out.println("Aspose.Cells version: " + com.aspose.cells.VersionInfo.getVersion());
```
Connaître la version vous aide à vérifier que vous utilisez une version qui prend en charge les slicers (disponibles depuis la version 20.9).

### Chargement d’un classeur Excel existant  

Pour manipuler un classeur, créez d’abord un objet `Workbook`.

`Workbook` représente un fichier Excel complet en mémoire, exposant les feuilles de calcul, les tableaux et d’autres composants.  
```java
Workbook workbook = new Workbook("input.xlsx");
```
Cela charge le fichier sans verrouiller la source, permettant des opérations de lecture‑écriture.

### Accès à une feuille de calcul et à un tableau spécifiques  

Après le chargement, localisez la feuille de calcul contenant le tableau cible.

`Worksheet` est l’objet qui contient les lignes, colonnes et tableaux d’une seule feuille.  
```java
Worksheet sheet = workbook.getWorksheets().get("SalesData");
Table table = sheet.getTables().get(0); // assumes the first table is the target
```
Si votre classeur contient plusieurs tableaux, ajustez l’indice ou utilisez le nom du tableau.

### Ajout d’un slicer à un tableau Excel  

Nous allons maintenant **ajouter un slicer** pour filtrer le tableau par la colonne « Region » et le placer dans la cellule `H5`.

`Slicer` est la classe qui crée l’interface de filtre interactive.  
```java
int slicerIndex = sheet.getSlicers().add(table.getIndex(), 2, "H5"); // column index 2 = Region
Slicer slicer = sheet.getSlicers().get(slicerIndex);
slicer.setCaption("Region");
slicer.setStyle(SlicerStyle.Light1);
```
Le slicer apparaît exactement à l’endroit que vous spécifiez, et vous pouvez personnaliser sa légende, son style et sa taille programmatiquement.

### Enregistrement du classeur modifié  

Enfin, écrivez les modifications sur le disque.

`Workbook.save` persiste la représentation en mémoire dans un fichier physique.  
```java
workbook.save("output_with_slicer.xlsx");
```
N’oubliez pas d’appeler `workbook.dispose()` dans les services de longue durée pour libérer les ressources natives.

## Applications pratiques

L’ajout de slicers avec Aspose.Cells for Java améliore l’analyse des données dans de nombreux scénarios :

1. **Rapports financiers :** Filtrez les chiffres de ventes trimestriels d’un simple clic pour repérer les tendances.  
2. **Gestion des stocks :** Visualisez les niveaux de stock par catégorie de produit sans reconstruire les requêtes.  
3. **Analytique RH :** Comparez rapidement les performances des employés entre les départements.  

Vous pouvez combiner la génération de slicers avec des importations de données automatisées depuis des bases de données ou des services web pour des pipelines de reporting de bout en bout.

## Considérations de performance

Lors du traitement de classeurs volumineux, gardez ces conseils à l’esprit :

- **Gestion de la mémoire :** Appelez `workbook.dispose()` après avoir terminé pour libérer la mémoire native.  
- **Traitement par lots :** Divisez les fichiers extrêmement grands en morceaux plus petits afin de maintenir l’empreinte mémoire sous contrôle.  
- **API de streaming :** Pour les fichiers de plus de 200 MB, utilisez le mode streaming de `LoadOptions` pour éviter de charger le classeur complet en mémoire.

Aspose.Cells peut gérer **plus de 100 formats d’entrée et de sortie** et traiter des classeurs de plusieurs centaines de pages avec moins de 200 Mo de RAM lorsque le streaming est activé.

## Problèmes courants et solutions

| Problème | Solution |
|----------|----------|
| **Slicer non visible** | Assurez‑vous que le tableau cible contient au moins une colonne avec des valeurs distinctes ; les slicers ont besoin d’éléments uniques pour s’afficher. |
| **Exception sur la méthode `add`** | Vérifiez que la référence de cellule (par ex., `"H5"`) se trouve dans la plage utilisée de la feuille et que l’indice de colonne correspond à une colonne existante du tableau. |
| **Licence non appliquée** | Confirmez que le chemin du fichier de licence est correct et que `License license = new License(); license.setLicense("Aspose.Total.Java.lic");` s’exécute avant tout appel à Aspose.Cells. |

## Questions fréquemment posées

**Q : Puis‑je ajouter plusieurs slicers au même tableau ?**  
R : Oui – appelez `worksheet.getSlicers().add` à plusieurs reprises avec des index de colonne ou des positions différents.

**Q : Aspose.Cells prend‑il en charge les slicers pour les tableaux croisés dynamiques ?**  
R : Absolument – la même méthode `add` fonctionne avec les tableaux croisés dynamiques tant qu’ils existent sur la feuille.

**Q : Est‑il possible de personnaliser le style du slicer programmatiquement ?**  
R : Vous pouvez modifier des propriétés telles que `setStyle`, `setCaption`, `setWidth` et `setHeight` après la création.

**Q : Quelles versions de Java sont compatibles ?**  
R : Aspose.Cells for Java 25.3 prend en charge Java 8 et les versions ultérieures, y compris Java 11, 17 et les versions LTS suivantes.

**Q : Comment supprimer un slicer qui n’est plus nécessaire ?**  
R : Utilisez `worksheet.getSlicers().removeAt(index)`, où `index` correspond à la position du slicer dans la collection.

---

**Dernière mise à jour :** 2026-09-02  
**Testé avec :** Aspose.Cells 25.3 for Java  
**Auteur :** Aspose  









```java
import com.aspose.cells.*;

public class DisplayAsposeCellsVersion {
    public static void main(String[] args) throws Exception {
        String version = CellsHelper.getVersion();
        System.out.println("Aspose.Cells for Java Version: " + version);
    }
}
```

```java
import com.aspose.cells.*;

public class LoadExcelWorkbook {
    public static void main(String[] args) throws Exception {
        String dataDir = "YOUR_DATA_DIRECTORY";
        Workbook workbook = new Workbook(dataDir + "/sampleCreateSlicerToExcelTable.xlsx");
    }
}
```

```java
import com.aspose.cells.*;

public class AccessWorksheetAndTable {
    public static void main(String[] args) throws Exception {
        String dataDir = "YOUR_DATA_DIRECTORY";
        Workbook workbook = new Workbook(dataDir + "/sampleCreateSlicerToExcelTable.xlsx");
        
        Worksheet worksheet = workbook.getWorksheets().get(0);
        ListObject table = worksheet.getListObjects().get(0);
    }
}
```

```java
import com.aspose.cells.*;

public class AddSlicerToExcelTable {
    public static void main(String[] args) throws Exception {
        String dataDir = "YOUR_DATA_DIRECTORY";
        Workbook workbook = new Workbook(dataDir + "/sampleCreateSlicerToExcelTable.xlsx");
        
        Worksheet worksheet = workbook.getWorksheets().get(0);
        ListObject table = worksheet.getListObjects().get(0);
        
        int idx = worksheet.getSlicers().add(table, 0, "H5");
    }
}
```

```java
import com.aspose.cells.*;

public class SaveExcelWorkbookWithSlicer {
    public static void main(String[] args) throws Exception {
        String dataDir = "YOUR_DATA_DIRECTORY";
        String outDir = "YOUR_OUTPUT_DIRECTORY";
        
        Workbook workbook = new Workbook(dataDir + "/sampleCreateSlicerToExcelTable.xlsx");
        
        Worksheet worksheet = workbook.getWorksheets().get(0);
        ListObject table = worksheet.getListObjects().get(0);
        
        int idx = worksheet.getSlicers().add(table, 0, "H5");
        
        workbook.save(outDir + "/outputCreateSlicerToExcelTable.xlsx", SaveFormat.XLSX);
    }
}
```

## Tutoriels associés

- [Gérer les classeurs Excel et les slicers avec Aspose.Cells for Java&#58; Un guide complet](/cells/java/workbook-operations/manage-excel-workbooks-aspose-cells-java/)
- [Maîtriser les tableaux croisés dynamiques dans Excel avec Aspose.Cells for Java&#58; Un guide complet d'analyse de données](/cells/java/data-analysis/excel-pivot-tables-aspose-cells-java-tutorial/)
- [Comment filtrer efficacement les données lors du chargement de classeurs Excel avec Aspose.Cells en Java](/cells/java/data-analysis/filter-data-excel-aspose-cells-java-tutorial/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}