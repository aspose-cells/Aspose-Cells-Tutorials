---
category: general
date: 2026-08-20
description: Apprenez à écrire du JSON dans Excel et à remplir un classeur Excel à
  partir de JSON en utilisant les smart markers d’Aspose et Java – guide étape par
  étape.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- aspose smart markers
- convert json to excel
- write json to excel
- populate excel from json
- create excel workbook java
language: fr
lastmod: 2026-08-20
og_description: Les Smart Markers d’Aspose vous permettent d’écrire du JSON dans Excel
  et de créer un exemple de code Java pour un classeur Excel. Suivez ce tutoriel pour
  remplir Excel à partir de JSON rapidement.
og_image_alt: Screenshot of an Excel file generated from a JSON array using Aspose.Cells
og_title: 'aspose smart markers : convertir JSON en Excel avec Java – guide complet'
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Learn to write JSON to Excel and populate an Excel workbook from JSON
    using aspose smart markers and Java – step‑by‑step guide.
  headline: How to use aspose smart markers to convert JSON to Excel in Java
  type: TechArticle
- description: Learn to write JSON to Excel and populate an Excel workbook from JSON
    using aspose smart markers and Java – step‑by‑step guide.
  name: How to use aspose smart markers to convert JSON to Excel in Java
  steps:
  - name: Expected output
    text: 'When you open `JsonArraySingleCell.xlsx`, cell **A1** contains:'
  - name: 1. Populating multiple cells with different JSON objects
    text: 'If you need to fill a table rather than a single cell, omit `ArrayAsSingle`
      and use the default array handling:'
  - name: 2. Using a JSON file instead of a hard‑coded string
    text: '```java String jsonPath = "data/people.json"; String jsonArray = new String(Files.readAllBytes(Paths.get(jsonPath)),
      StandardCharsets.UTF_8); ```'
  - name: 3. Handling nested JSON structures
    text: 'For nested objects, reference sub‑properties in the smart marker:'
  - name: 4. License activation
    text: 'To avoid the evaluation watermark, activate your license before creating
      the workbook:'
  type: HowTo
tags:
- Aspose
- Java
- Excel
- JSON
title: Comment utiliser les smart markers d’Aspose pour convertir du JSON en Excel
  en Java
url: /fr/java/excel-import-export/how-to-use-aspose-smart-markers-to-convert-json-to-excel-in/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment utiliser les aspose smart markers pour convertir du JSON en Excel en Java

Si vous avez besoin des **aspose smart markers** pour convertir du JSON en Excel, ce tutoriel présente une solution prête à l’emploi. Vous verrez comment écrire du JSON dans Excel, remplir un classeur Excel à partir de JSON, et générer un fichier avec une seule ligne de code.

L’exemple utilise Aspose.Cells for Java, une bibliothèque qui élimine le besoin de Microsoft Office sur le serveur. À la fin du guide, vous disposerez d’un programme Java complet qui crée un classeur Excel, injecte un tableau JSON dans une seule cellule et enregistre le résultat sous le nom `JsonArraySingleCell.xlsx`.

## Prérequis

* Java Development Kit 17 ou version ultérieure installé.
* Maven ou Gradle pour gérer les dépendances (l’exemple utilise Maven).
* Une licence Aspose.Cells for Java (l’évaluation gratuite fonctionne pour les tests).
* Une connaissance de base de la syntaxe Java et du format JSON.

> **Astuce :** Si vous exécutez le code sans licence, le classeur généré contiendra un petit filigrane d’évaluation sur la première feuille.

## Ajouter Aspose.Cells à votre projet

Ajoutez la dépendance suivante à votre `pom.xml` (Maven) ou l’équivalent dans Gradle :

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest stable version -->
</dependency>
```

La bibliothèque fournit les classes `Workbook`, `Worksheet`, `JsonDataSource` et `SmartMarker` utilisées tout au long de ce tutoriel.

## Étape 1 : Créer un classeur Excel en Java

Tout d’abord, créez une nouvelle instance de l’objet `Workbook`. Cela représente un fichier Excel vide en mémoire.

```java
// Step 1: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();               // Creates a blank .xlsx file
Worksheet worksheet = workbook.getWorksheets().get(0);
Cells cells = worksheet.getCells();
```

`Workbook` est le point d’entrée pour toutes les opérations Excel. Par défaut, il contient une feuille de calcul, que nous récupérons pour une manipulation ultérieure.

## Étape 2 : Préparer le tableau JSON que vous souhaitez écrire dans Excel

La chaîne JSON peut provenir d’un fichier, d’un service web ou être construite programmatiquement. Pour ce tutoriel, nous utilisons un tableau simple en ligne :

```java
// Step 2: Define the JSON array that will be used as the data source
String jsonArray = "[{\"Name\":\"John\"},{\"Name\":\"Jane\"}]";
```

La structure JSON correspond à la forme attendue par les smart markers d’Aspose.Cells : un tableau d’objets où chaque objet possède une propriété `Name`.

## Étape 3 : Insérer un smart marker qui traite le tableau comme une seule cellule

Les smart markers d’Aspose vous permettent d’insérer des espaces réservés directement dans les cellules. L’option `ArrayAsSingle` indique au moteur de placer l’ensemble du tableau JSON dans une seule cellule au lieu de l’étendre en tableau.

```java
// Step 3: Insert a smart marker that tells Aspose.Cells to treat the array as a single cell
cells.putValue("A1", "${jsonArray,ArrayAsSingle}");
```

Lorsque le classeur est traité, `${jsonArray,ArrayAsSingle}` sera remplacé par le texte JSON brut.

## Étape 4 : Enregistrer la source de données JSON avec le nom du smart marker

Liez le nom de l’espace réservé (`jsonArray`) à une instance de `JsonDataSource`. Cette étape associe la chaîne JSON au marqueur.

```java
// Step 4: Register the JSON data source with the smart marker name
JsonDataSource dataSource = new JsonDataSource(jsonArray);
worksheet.getSmartMarkers().setDataSource("jsonArray", dataSource);
```

`JsonDataSource` analyse le JSON et le rend disponible pour le moteur de smart markers. L’appel `setDataSource` l’enregistre sous le nom utilisé dans la cellule (`jsonArray`).

## Étape 5 : Enregistrer le classeur sur le disque

Enfin, écrivez le classeur dans un fichier physique. Vous pouvez choisir n’importe quel répertoire.

```java
// Step 5: Save the workbook to a file
String outputPath = "YOUR_DIRECTORY/JsonArraySingleCell.xlsx";
workbook.save(outputPath);
System.out.println("Workbook saved to " + outputPath);
```

L’exécution du programme produit un fichier Excel contenant le tableau JSON dans la cellule **A1**. Ouvrez le fichier avec Excel, LibreOffice ou tout visualiseur supportant le format `.xlsx` pour vérifier le résultat.

![Classeur Excel créé avec Aspose.Cells affichant des données JSON](/images/json-to-excel.png)

*Texte alternatif de l’image : Capture d’écran d’un fichier Excel généré à partir d’un tableau JSON à l’aide d’Aspose.Cells.*

## Code source complet

En assemblant tous les éléments, voici la classe Java complète et exécutable :

```java
import com.aspose.cells.*;

public class JsonArraySmartMarker {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and access the first worksheet
        Workbook workbook = new Workbook();                       // Empty workbook
        Worksheet worksheet = workbook.getWorksheets().get(0);
        Cells cells = worksheet.getCells();

        // Step 2: Define the JSON array that will be used as the data source
        String jsonArray = "[{\"Name\":\"John\"},{\"Name\":\"Jane\"}]";

        // Step 3: Insert a smart marker that tells Aspose.Cells to treat the array as a single cell
        cells.putValue("A1", "${jsonArray,ArrayAsSingle}");

        // Step 4: Register the JSON data source with the smart marker name
        JsonDataSource dataSource = new JsonDataSource(jsonArray);
        worksheet.getSmartMarkers().setDataSource("jsonArray", dataSource);

        // Step 5: Save the workbook to a file
        String outputPath = "YOUR_DIRECTORY/JsonArraySingleCell.xlsx";
        workbook.save(outputPath);
        System.out.println("Workbook saved to " + outputPath);
    }
}
```

### Résultat attendu

Lorsque vous ouvrez `JsonArraySingleCell.xlsx`, la cellule **A1** contient :

```
[{"Name":"John"},{"Name":"Jane"}]
```

Aucune ligne ou colonne supplémentaire n’est ajoutée — cela montre comment les **aspose smart markers** vous permettent de **écrire du JSON dans Excel** tout en conservant la charge utile JSON intacte.

## Variantes courantes et cas limites

### 1. Remplir plusieurs cellules avec différents objets JSON

Si vous devez remplir un tableau plutôt qu’une seule cellule, omettez `ArrayAsSingle` et utilisez le traitement de tableau par défaut :

```java
cells.putValue("A1", "${jsonArray}");
```

Aspose.Cells développera le tableau en lignes, créant une colonne pour chaque propriété (`Name` dans ce cas). Ceci est utile lorsque vous souhaitez une vue tabulaire traditionnelle.

### 2. Utiliser un fichier JSON au lieu d’une chaîne codée en dur

```java
String jsonPath = "data/people.json";
String jsonArray = new String(Files.readAllBytes(Paths.get(jsonPath)), StandardCharsets.UTF_8);
```

Lisez le contenu du fichier dans une chaîne, puis suivez les Étapes 3‑5 sans modification. Cette approche fonctionne pour de grandes charges utiles ou des données provenant d’API externes.

### 3. Gérer les structures JSON imbriquées

Pour les objets imbriqués, faites référence aux sous‑propriétés dans le smart marker :

```java
cells.putValue("B2", "${jsonArray.Address.City}");
```

Aspose.Cells parcourt automatiquement la hiérarchie, vous permettant de remplir des rapports complexes sans analyse manuelle.

### 4. Activation de la licence

Pour éviter le filigrane d’évaluation, activez votre licence avant de créer le classeur :

```java
License license = new License();
license.setLicense("Aspose.Total.Java.lic");
```

Placez ce code au tout début de `main`. Le fichier de licence peut être intégré en tant que ressource ou chargé depuis un emplacement sécurisé.

## Conseils pour une utilisation en production

* **Réutiliser l’objet workbook** – Si vous générez de nombreux rapports en une seule exécution, créez un `Workbook` et clonez les feuilles de calcul au lieu d’instancier un nouveau classeur à chaque fois.
* **Diffuser la sortie** – Pour les gros fichiers, utilisez `workbook.save(OutputStream, SaveFormat.XLSX)` afin d’écrire directement dans un flux de réponse dans les applications web.
* **Valider le JSON** – Avant de transmettre les données à `JsonDataSource`, validez le format JSON afin d’éviter les erreurs d’exécution.
* **Performance** – Les smart markers sont optimisés pour les opérations en masse ; évitez de mélanger des écritures cellule par cellule avec le traitement des smart markers dans la même feuille.

## Conclusion

Vous savez maintenant comment utiliser les **aspose smart markers** pour **convertir du JSON en Excel**, **écrire du JSON dans Excel** et **remplir Excel à partir de JSON** avec Java. L’exemple complet crée un classeur Excel, injecte un tableau JSON dans une seule cellule et enregistre le fichier—le tout en seulement cinq étapes concises.

Ensuite, vous pourriez explorer :

* Générer des rapports multi‑feuilles à partir de structures JSON complexes.
* Combiner les smart markers avec les formules Excel pour des calculs dynamiques.
* Utiliser `JsonDataSource` conjointement avec `DataTable` pour des exportations au format CSV.

N’hésitez pas à expérimenter avec différents chargements JSON, plages de cellules et options de formatage. Avec Aspose.Cells, transformer des données JSON en classeurs Excel soignés devient un processus simple, centré sur le code. Bon codage !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et à explorer des approches d’implémentation alternatives dans vos propres projets.

- [Créer un classeur Excel avec Aspose.Cells en Java : guide étape par étape](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [Créer des rapports Excel dynamiques avec Aspose.Cells Java et les Smart Markers](/cells/english/java/templates-reporting/dynamic-excel-reports-aspose-cells-java-smart-markers/)
- [Maîtriser Aspose.Cells Java : implémenter les Smart Markers et les formules pour l’automatisation Excel](/cells/english/java/formulas-functions/aspose-cells-java-smart-markers-formulas/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}