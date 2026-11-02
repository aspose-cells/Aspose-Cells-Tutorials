---
category: general
date: 2026-08-20
description: Créer un classeur Excel en Java avec Aspose.Cells, définir le format
  monétaire, ajouter une police en gras et importer un tableau de styles pour les
  cellules formatées.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- set currency format
- format cells currency
- how to import style
- add bold font
language: fr
lastmod: 2026-08-20
og_description: Créer un classeur Excel en Java, définir le format monétaire, ajouter
  une police en gras et apprendre comment importer le style avec Aspose.Cells.
og_image_alt: Screenshot of an excel workbook created with currency format and bold
  font using Aspose.Cells
og_title: Créer un classeur Excel avec des cellules monétaires stylisées en Java
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Create excel workbook in Java using Aspose.Cells, set currency format,
    add bold font, and import style array for styled cells.
  headline: How to create excel workbook with currency format and bold font in Java
  type: TechArticle
- description: Create excel workbook in Java using Aspose.Cells, set currency format,
    add bold font, and import style array for styled cells.
  name: How to create excel workbook with currency format and bold font in Java
  steps:
  - name: Initialise the workbook and worksheet
    text: Creating a fresh workbook gives you a clean container for all subsequent
      formatting.
  - name: Build a DataTable with numeric data
    text: A `DataTable` mimics a database table, making it easy to import rows in
      bulk.
  - name: Define a style – currency format and bold font
    text: Here we **set currency format** and **add bold font** to a `Style` object.
  - name: Configure import options to use the style array
    text: Aspose.Cells lets you pass a `Style[]` via `ImportTableOptions`. This is
      the official **how to import style** method.
  - name: Import the DataTable into the worksheet
    text: Now we bring the data into the sheet at cell `A1`, applying the style array
      automatically.
  - name: Save the workbook to disk
    text: Finally, write the in‑memory workbook to a physical file.
  - name: Expected output
    text: 'When you open `DataTableWithStyleArray.xlsx` in Microsoft Excel, you should
      see:'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- Formatting
title: Comment créer un classeur Excel avec un format monétaire et une police en gras
  en Java
url: /fr/java/formatting/how-to-create-excel-workbook-with-currency-format-and-bold-f/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment créer un classeur Excel avec un format monétaire et une police en gras en Java

Si vous devez **créer un classeur Excel** de façon programmatique, ce guide vous montre exactement comment faire. Nous parcourrons la création d’un classeur, l’application d’un format monétaire, l’ajout d’une police en gras, et l’utilisation de la fonctionnalité **how to import style** d’Aspose.Cells afin que chaque cellule importée soit cohérente.

Vous terminerez avec un fichier `DataTableWithStyleArray.xlsx` prêt à l’emploi, affichant les nombres en dollars et les mettant en gras. Aucun formatage manuel dans Excel n’est requis.

## Prérequis

Avant de commencer, assurez‑vous d’avoir :

- Java 17 ou version ultérieure installé.
- Une licence Aspose.Cells for Java (ou une clé d’évaluation gratuite).
- Maven ou Gradle pour gérer la dépendance `aspose-cells`.
- Une connaissance de base des collections Java et de `DataTable`.

```xml
<!-- Maven dependency -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version>
</dependency>
```

> **Astuce :** Si vous rencontrez une `LicenseException`, placez votre fichier de licence dans le classpath et appelez `License license = new License(); license.setLicense("Aspose.Total.Java.lic");` avant de créer le classeur.

## Comment créer un classeur Excel avec des cellules monétaires stylisées

Cette section contient les étapes principales. Chaque étape explique **pourquoi** elle est importante, pas seulement **quoi** taper.

### Étape 1 : Initialiser le classeur et la feuille de calcul

Créer un nouveau classeur vous donne un conteneur vierge pour tout le formatage ultérieur.

```java
// Step 1: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();                     // creates an empty .xlsx file in memory
Worksheet worksheet = workbook.getWorksheets().get(0); // first sheet is index 0
Cells cells = worksheet.getCells();                     // shortcut to work with cells
```

> **Pourquoi :** L’objet `Workbook` représente le fichier Excel complet. Accéder à la première `Worksheet` vous permet de commencer à remplir les données immédiatement.

### Étape 2 : Construire un DataTable avec des données numériques

Un `DataTable` imite une table de base de données, ce qui facilite l’importation massive de lignes.

```java
// Step 2: Build a DataTable with sample numeric data
DataTable dataTable = new DataTable();
dataTable.getColumns().add("Amount", DataType.DOUBLE); // column type DOUBLE ensures numeric handling
dataTable.getRows().add(new Object[]{1234.56});
dataTable.getRows().add(new Object[]{7890.12});
```

> **Pourquoi :** Utiliser `DOUBLE` garantit que les valeurs conservent leur précision décimale, ce qui est essentiel lorsque vous **format cells currency** plus tard.

### Étape 3 : Définir un style – format monétaire et police en gras

Ici nous **set currency format** et **add bold font** à un objet `Style`.

```java
// Step 3: Define a style (currency format and bold font) for the imported cells
Style currencyStyle = workbook.createStyle();                // create a reusable style instance
currencyStyle.getNumber().setFormat("$#,##0.00");            // set currency format (e.g., $1,234.56)
currencyStyle.getFont().setBold(true);                      // make the font bold
Style[] styleArray = new Style[] { currencyStyle };          // style array required by ImportTableOptions
```

> **Pourquoi :** La chaîne de format `Number` `$#,##0.00` indique à Excel de traiter la cellule comme une valeur monétaire, tandis que `setBold(true)` attire l’attention sur les nombres. Placer le style dans un tableau prépare le **how to import style**.

### Étape 4 : Configurer les options d’importation pour utiliser le tableau de styles

Aspose.Cells vous permet de passer un `Style[]` via `ImportTableOptions`. C’est la méthode officielle **how to import style**.

```java
// Step 4: Set up import options to use the style array
ImportTableOptions importOptions = new ImportTableOptions();
importOptions.setStyleArray(styleArray); // tells the importer to apply our currencyStyle to every column
```

> **Pourquoi :** Sans `ImportTableOptions`, les cellules importées hériteraient du style par défaut, perdant le format monétaire et le gras que nous avons définis.

### Étape 5 : Importer le DataTable dans la feuille de calcul

Nous importons maintenant les données dans la feuille à la cellule `A1`, en appliquant automatiquement le tableau de styles.

```java
// Step 5: Import the DataTable into the worksheet at A1, applying the style
cells.importDataTable(dataTable, true, "A1", importOptions);
```

- `true` indique que la première ligne du `DataTable` contient les en‑têtes de colonne.
- `"A1"` est le coin supérieur gauche où commence l’importation.

> **Pourquoi :** L’importation avec le tableau de styles garantit que chaque cellule importée reçoit le style **format cells currency** que nous avons préparé.

### Étape 6 : Enregistrer le classeur sur le disque

Enfin, écrivez le classeur en mémoire dans un fichier physique.

```java
// Step 6: Save the workbook to a file
String outputPath = "YOUR_DIRECTORY/DataTableWithStyleArray.xlsx";
workbook.save(outputPath);
System.out.println("Workbook saved to: " + outputPath);
```

> **Pourquoi :** L’enregistrement persiste le formatage, permettant à vous ou à des processus en aval d’ouvrir le fichier dans Excel avec l’apparence souhaitée.

## Code source complet

Voici la classe Java complète, prête à être exécutée. Copiez‑la dans votre IDE, remplacez `YOUR_DIRECTORY` par un dossier existant, puis lancez‑la.

```java
import com.aspose.cells.*;

public class StyleArrayImportTutorial {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);
        Cells cells = worksheet.getCells();

        // Step 2: Build a DataTable with sample numeric data
        DataTable dataTable = new DataTable();
        dataTable.getColumns().add("Amount", DataType.DOUBLE);
        dataTable.getRows().add(new Object[]{1234.56});
        dataTable.getRows().add(new Object[]{7890.12});

        // Step 3: Define a style (currency format and bold font) for the imported cells
        Style currencyStyle = workbook.createStyle();
        currencyStyle.getNumber().setFormat("$#,##0.00");   // set currency format
        currencyStyle.getFont().setBold(true);             // add bold font
        Style[] styleArray = new Style[] { currencyStyle };

        // Step 4: Set up import options to use the style array
        ImportTableOptions importOptions = new ImportTableOptions();
        importOptions.setStyleArray(styleArray);           // how to import style

        // Step 5: Import the DataTable into the worksheet at A1, applying the style
        cells.importDataTable(dataTable, true, "A1", importOptions);

        // Step 6: Save the workbook to a file
        workbook.save("YOUR_DIRECTORY/DataTableWithStyleArray.xlsx");
        System.out.println("Workbook created successfully.");
    }
}
```

### Résultat attendu

Lorsque vous ouvrez `DataTableWithStyleArray.xlsx` dans Microsoft Excel, vous devez voir :

| Montant |
|--------|
| **$1,234.56** |
| **$7,890.12** |

- Les nombres sont affichés avec un **format monétaire** (symbole `$`, deux décimales).
- La police des deux cellules est **en gras**, les faisant ressortir.

## Variations courantes et cas limites

| Scénario | Ce qu’il faut changer | Raison |
|----------|-----------------------|--------|
| **Monnaie différente** | `currencyStyle.getNumber().setFormat("€#,##0.00");` | Utiliser le symbole Euro ou tout format spécifique à une locale. |
| **Plusieurs colonnes avec des styles différents** | Créez plusieurs objets `Style`, remplissez `styleArray` dans le même ordre que les colonnes. | Chaque colonne peut avoir son propre format numérique, police, arrière‑plan, etc. |
| **Ensembles de données volumineux** | Utilisez `cells.importDataTable(dataTable, false, "A1", importOptions);` et définissez `importOptions.setImportDataOptions(ImportDataOptions.DATA_ONLY);` | Améliore les performances en ignorant les lignes d’en‑tête ou les métadonnées inutiles. |
| **Appliquer le style après l’importation** | Appelez `cells.get("A2").setStyle(currencyStyle);` pour des cellules individuelles. | Utile lorsqu’un sous‑ensemble de lignes nécessite un formatage spécial. |

## Conseils pour la mise en production

- **Licencez tôt** : Enregistrez votre licence Aspose.Cells avant de créer le classeur pour éviter le filigrane d’évaluation.
- **Sécurité des threads** : Les instances de `Workbook` **ne sont pas** thread‑safe. Créez une instance distincte par thread si vous générez de nombreux fichiers simultanément.
- **Gestion de la mémoire** : Pour des feuilles très grandes, envisagez d’utiliser l’API de streaming de `Workbook` (`Workbook` → `WorkbookDesigner`) afin de limiter la consommation mémoire.
- **Tests** : Incluez un test unitaire qui ouvre le fichier enregistré avec Apache POI et vérifie que le format numérique du style de cellule correspond à `"$#,##0.00"`.

## Conclusion

Vous savez maintenant comment **créer un classeur Excel** en Java, **définir un format monétaire**, **ajouter une police en gras**, et correctement **how to import style** en utilisant `ImportTableOptions` d’Aspose.Cells. Cette solution de bout en bout élimine les étapes manuelles dans Excel et garantit que chaque cellule importée suit le même style **format cells currency**.

Prêt pour le prochain défi ? Essayez d’ajouter un formatage conditionnel, d’insérer des graphiques, ou d’exporter le classeur en PDF—tout en réutilisant la même technique de tableau de styles. Bon codage !

## Que devez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser d’autres fonctionnalités de l’API et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Create an Excel Workbook using Aspose.Cells in Java: A Step-by-Step Guide](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [How to Create & Format Excel Cells Using Aspose.Cells for Java: A Step-by-Step Guide](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)
- [How to Style Excel Cells and Add Hyperlinks Using Aspose.Cells for Java](/cells/english/java/formatting/style-excel-cells-hyperlinks-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}