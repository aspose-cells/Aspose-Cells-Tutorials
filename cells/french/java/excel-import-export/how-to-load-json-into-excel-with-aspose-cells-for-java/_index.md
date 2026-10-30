---
category: general
date: 2026-10-07
description: Apprenez à charger du JSON dans Excel et à générer un fichier XLSX à
  partir du JSON en utilisant Aspose.Cells. Ce guide étape par étape montre également
  comment remplir Excel à partir du JSON et enregistrer le classeur au format XLSX.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- load json into excel
- generate xlsx from json
- populate excel from json
- save workbook as xlsx
- create workbook from json
language: fr
lastmod: 2026-10-07
og_description: Chargez JSON dans Excel et générez un fichier XLSX à partir de JSON
  en utilisant Aspose.Cells pour Java. Suivez ce guide pour remplir Excel à partir
  de JSON et enregistrer le classeur au format XLSX.
og_image_alt: Screenshot of an Excel workbook that was loaded with JSON data using
  Aspose.Cells
og_title: Charger du JSON dans Excel avec Aspose.Cells – guide complet Java
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Learn how to load JSON into Excel and generate XLSX from JSON using
    Aspose.Cells. This step‑by‑step guide also shows how to populate Excel from JSON
    and save workbook as XLSX.
  headline: How to load JSON into Excel with Aspose.Cells for Java
  type: TechArticle
- description: Learn how to load JSON into Excel and generate XLSX from JSON using
    Aspose.Cells. This step‑by‑step guide also shows how to populate Excel from JSON
    and save workbook as XLSX.
  name: How to load JSON into Excel with Aspose.Cells for Java
  steps:
  - name: 'Compile the program:'
    text: 'Compile the program:'
  - name: 'Run it:'
    text: 'Run it:'
  - name: Verify that `JsonSingleCell.xlsx` appears in the working directory and opens
      without errors.
    text: Verify that `JsonSingleCell.xlsx` appears in the working directory and opens
      without errors.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Comment charger du JSON dans Excel avec Aspose.Cells pour Java
url: /fr/java/excel-import-export/how-to-load-json-into-excel-with-aspose-cells-for-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Charger du JSON dans Excel avec Aspose.Cells pour Java

Si vous devez **charger du JSON dans Excel**, ce tutoriel vous montre une méthode fiable pour le faire avec Aspose.Cells pour Java. Vous verrez comment générer un XLSX à partir de JSON, remplir Excel à partir de JSON, et enfin **enregistrer le classeur au format XLSX** — le tout dans un programme unique et autonome.

Travailler avec du JSON dans les feuilles de calcul est courant lorsque vous exportez des données depuis des services web, des API ou des magasins NoSQL. À la fin de ce guide, vous disposerez d’une classe Java prête à l’emploi qui crée un classeur à partir de JSON et écrit le résultat dans un fichier sur le disque.

## Prérequis

* Java 8 ou une version plus récente installée (le code utilise les fonctionnalités standard de Java).
* Bibliothèque Aspose.Cells pour Java (version 23.10 ou ultérieure). Vous pouvez l’obtenir depuis le [site Web d’Aspose](https://downloads.aspose.com/cells/java) ou via Maven Central.
* Un IDE ou un simple éditeur de texte et un terminal pour compiler et exécuter le code Java.
* Une connaissance de base de la syntaxe JSON et des concepts Excel.

> **Astuce :** Si vous utilisez Maven, ajoutez la dépendance suivante à votre `pom.xml` pour éviter la gestion manuelle des JAR :

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
</dependency>
```

## Étape 1 : Configurer le projet et importer les classes requises

Créez une nouvelle classe Java nommée `JsonToExcelDemo`. Importez les classes Aspose.Cells dont vous aurez besoin pour la création de classeur, la gestion des feuilles de calcul et le traitement des Smart Markers.

```java
package com.example.exceljson;

import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
import com.aspose.cells.SmartMarkerProcessor;
import com.aspose.cells.SaveFormat;

public class JsonToExcelDemo {
    public static void main(String[] args) throws Exception {
        // The full implementation starts in the next step.
    }
}
```

*Pourquoi cette étape est importante :* L’importation des bonnes classes garantit que le compilateur peut localiser les API Aspose.Cells. La classe `Workbook` représente le fichier Excel, tandis que `SmartMarkerProcessor` gère la conversion JSON‑vers‑Excel.

## Étape 2 : Définir la source JSON qui sera chargée dans Excel

Pour cet exemple, nous utilisons un petit tableau JSON contenant deux objets. Dans un scénario réel, vous pourriez lire le JSON depuis un fichier, un point d’accès REST ou une base de données.

```java
// Step 2: Define the JSON data that will be used as the smart‑marker source
String jsonData = "[{\"Name\":\"John\",\"Age\":30},{\"Name\":\"Anna\",\"Age\":25}]";
```

*Pourquoi cette étape est importante :* La chaîne JSON est la source de données pour l’opération **remplir Excel à partir de JSON**. Conserver le JSON dans une variable `String` facilite son passage au `SmartMarkerProcessor`.

## Étape 3 : Créer un nouveau classeur et obtenir la première feuille de calcul

Un classeur vierge vous offre une page blanche. La première feuille de calcul (index 0) est celle où nous insérerons le Smart Marker.

```java
// Step 3: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();               // creates an empty XLSX workbook
Worksheet worksheet = workbook.getWorksheets().get(0);
```

*Pourquoi cette étape est importante :* Aspose.Cells travaille avec un objet `Workbook` qui peut être enregistré ultérieurement sous forme de fichier XLSX. Accéder à la première `Worksheet` nous permet de placer le marqueur à une adresse de cellule connue.

## Étape 4 : Insérer un Smart Marker qui indique à Aspose.Cells comment traiter le JSON

Les Smart Markers sont des espaces réservés que Aspose.Cells remplace par des données provenant d’une source. Le marqueur `&=JSONData.ArrayAsSingle` indique à la bibliothèque de traiter l’ensemble du tableau JSON comme une valeur unique de cellule.

```java
// Step 4: Insert a smart‑marker that tells Aspose.Cells to treat the JSON array as a single cell
worksheet.getCells().putValue(0, 0, "&=JSONData.ArrayAsSingle");
```

*Pourquoi cette étape est importante :* L’utilisation de `ArrayAsSingle` évite le comportement par défaut qui consiste à développer chaque élément du tableau en lignes séparées. Ceci est utile lorsque vous souhaitez que le texte JSON apparaisse tel quel dans une cellule, ou lorsque vous prévoyez de le diviser plus tard avec des formules.

## Étape 5 : Configurer le SmartMarkerProcessor avec la source de données JSON

Liez maintenant la chaîne JSON au nom logique `JSONData`. Le processeur remplacera le marqueur par les données réelles.

```java
// Step 5: Configure the SmartMarkerProcessor with the JSON data source
SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);
processor.setDataSource("JSONData", jsonData);
processor.process();   // expands the marker and writes JSON into the worksheet
```

*Pourquoi cette étape est importante :* `setDataSource` associe le nom utilisé dans le marqueur (`JSONData`) avec la charge utile JSON réelle. `process()` effectue le travail lourd : analyse du JSON, application de la logique du marqueur et écriture du résultat dans la feuille de calcul.

## Étape 6 : Enregistrer le classeur résultant au format XLSX

Enfin, écrivez le classeur sur le disque. La constante `SaveFormat.XLSX` garantit le format Office Open XML correct.

```java
// Step 6: Save the resulting workbook
String outputPath = "JsonSingleCell.xlsx";   // adjust the path as needed
workbook.save(outputPath, SaveFormat.XLSX);
System.out.println("Workbook saved to " + outputPath);
```

*Pourquoi cette étape est importante :* L’enregistrement du fichier complète le flux de travail **générer XLSX à partir de JSON**. Le fichier produit peut être ouvert dans Excel, LibreOffice ou tout autre programme de tableur supportant le format XLSX.

### Code source complet

En assemblant toutes les pièces, voici le programme complet et exécutable qui **crée un classeur à partir de JSON**, **remplit Excel à partir de JSON**, et **enregistre le classeur au format XLSX**.

```java
package com.example.exceljson;

import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
import com.aspose.cells.SmartMarkerProcessor;
import com.aspose.cells.SaveFormat;

public class JsonToExcelDemo {
    public static void main(String[] args) throws Exception {
        // 1. JSON source – replace with your own data if needed
        String jsonData = "[{\"Name\":\"John\",\"Age\":30},{\"Name\":\"Anna\",\"Age\":25}]";

        // 2. Create a fresh workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 3. Place a smart‑marker that treats the JSON array as a single cell
        worksheet.getCells().putValue(0, 0, "&=JSONData.ArrayAsSingle");

        // 4. Bind the JSON string to the marker name and process it
        SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);
        processor.setDataSource("JSONData", jsonData);
        processor.process();

        // 5. Save the workbook as an XLSX file
        String outputPath = "JsonSingleCell.xlsx";
        workbook.save(outputPath, SaveFormat.XLSX);
        System.out.println("Workbook saved to " + outputPath);
    }
}
```

### Résultat attendu

Lorsque vous ouvrez `JsonSingleCell.xlsx`, vous verrez le tableau JSON affiché dans la cellule **A1** exactement comme la chaîne d’origine :

```
[{"Name":"John","Age":30},{"Name":"Anna","Age":25}]
```

Si vous préférez chaque objet sur une ligne séparée, remplacez le marqueur par `&=JSONData` (sans `.ArrayAsSingle`). Le processeur développera alors le tableau en lignes individuelles, démontrant une technique différente de **remplir Excel à partir de JSON**.

## Variations courantes et cas limites

| Situation | Ajustement |
|-----------|------------|
| **Grande charge JSON ( > 10 Mo )** | Augmentez la taille du tas JVM (`-Xmx2g`) et envisagez le streaming du JSON pour éviter `OutOfMemoryError`. |
| **Objets imbriqués** | Utilisez des marqueurs hiérarchiques comme `&=JSONData.Name` et `&=JSONData.Age` dans un tableau pour mapper chaque propriété à une colonne. |
| **Fichier JSON au lieu d’une chaîne** | Lisez le fichier dans une `String` avec `java.nio.file.Files.readString(Path.of("data.json"))` et passez‑le à `setDataSource`. |
| **Besoin de conserver le format JSON original** | Conservez le suffixe `.ArrayAsSingle`, ou encapsulez le JSON dans CDATA si vous prévoyez d’utiliser des formules Excel qui analysent le JSON ultérieurement. |
| **Feuilles de calcul multiples** | Créez des feuilles de calcul supplémentaires (`workbook.getWorksheets().add("Sheet2")`) et répétez l’insertion du marqueur sur chaque feuille. |

> **Avertissement :** Les Smart Markers sont sensibles à la casse. Assurez‑vous que le nom logique (`JSONData`) correspond exactement entre le marqueur et `setDataSource`.

## Tester la solution

1. Compilez le programme :

   ```bash
   javac -cp ".:aspose-cells-23.10.jar" com/example/exceljson/JsonToExcelDemo.java
   ```

2. Exécutez‑le :

   ```bash
   java -cp ".:aspose-cells-23.10.jar" com.example.exceljson.JsonToExcelDemo
   ```

3. Vérifiez que `JsonSingleCell.xlsx` apparaît dans le répertoire de travail et s’ouvre sans erreur.

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Créer un classeur Excel à partir de JSON – Guide complet Aspose.Cells](/cells/english/net/data-loading-and-parsing/create-excel-workbook-from-json-complete-aspose-cells-guide/)
- [Créer un classeur Excel C# – Insérer du JSON et enregistrer au format XLSX](/cells/english/net/excel-data-import-export/create-excel-workbook-c-insert-json-and-save-as-xlsx/)
- [Enregistrer un classeur Excel à partir de JSON – Guide complet](/cells/english/net/templates-reporting/save-excel-workbook-from-json-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}