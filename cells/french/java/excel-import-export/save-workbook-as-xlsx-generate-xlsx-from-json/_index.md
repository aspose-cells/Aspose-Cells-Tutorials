---
category: general
date: 2026-06-21
description: Enregistrez le classeur au format XLSX en utilisant SmartMarkerProcessor
  pour générer un XLSX à partir de JSON et remplissez facilement Excel avec des données
  JSON.
draft: false
keywords:
- save workbook as xlsx
- generate xlsx from json
- populate excel from json
language: fr
og_description: Enregistrez le classeur au format XLSX avec un seul extrait Java.
  Apprenez à générer un XLSX à partir de JSON et à remplir Excel depuis JSON en utilisant
  SmartMarker.
og_title: Enregistrer le classeur au format XLSX – Générer un XLSX à partir de JSON
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Save workbook as XLSX using SmartMarkerProcessor to generate XLSX from
    JSON and easily populate Excel from JSON data.
  headline: Save Workbook as XLSX – Generate XLSX from JSON
  type: TechArticle
- description: Save workbook as XLSX using SmartMarkerProcessor to generate XLSX from
    JSON and easily populate Excel from JSON data.
  name: Save Workbook as XLSX – Generate XLSX from JSON
  steps:
  - name: Expected Result
    text: 'After you run the program, open `output.xlsx`. You’ll see a sheet named
      **Sheet1** with two rows of data:'
  - name: Customizing the Template
    text: 'If you’d rather control column order or add a header row, create a tiny
      template before running the code:'
  - name: 1. Nested JSON Objects
    text: SmartMarker can dive into nested structures using dot notation (`${jsonArray.Address.City}`).
      Just ensure your JSON string reflects that hierarchy.
  - name: 2. Large Datasets
    text: 'When dealing with thousands of rows, disable workbook calculation before
      processing:'
  - name: 3. Data Types
    text: 'Dates, numbers, and booleans are inferred automatically, but you can force
      a format:'
  - name: 4. Multiple Placeholders
    text: You can feed several JSON arrays into the same workbook by using distinct
      placeholder names (`${orders}`, `${customers}`) and calling `processor.apply`
      for each.
  type: HowTo
- questions:
  - answer: No. The library is self‑contained; just add the JAR (or Maven dependency)
      and you’re ready to **save workbook as xlsx**.
    question: Do I need to install anything besides the Aspose Cells JAR?
  - answer: 'Absolutely. Replace `workbook.save("output.xlsx", SaveFormat.XLSX);`
      with: ```java try (FileOutputStream out = new FileOutputStream("output.xlsx"))
      { workbook.save(out, SaveFormat.XLSX); } ```'
    question: Can I write directly to a stream instead of a file?
  - answer: 'Use the `SmartMarkerProcessor.setCustomFieldNames` method to map JSON
      keys to placeholder names. ## Conclusion We’ve covered everything you need to
      **save workbook as xlsx** while **generating XLSX from JSON** and **populating
      Excel from JSON** using Aspose Cells’ SmartMarker. The short program show'
    question: What if my JSON keys don’t match Excel column names?
  type: FAQPage
tags:
- Aspose.Cells
- Java
- Excel Automation
title: Enregistrer le classeur au format XLSX – Générer un XLSX à partir de JSON
url: /fr/java/excel-import-export/save-workbook-as-xlsx-generate-xlsx-from-json/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Enregistrer le classeur au format XLSX – Générer un XLSX à partir de JSON

Vous avez déjà eu besoin de **save workbook as xlsx** mais vous ne disposiez que de données JSON ? Vous n'êtes pas le seul à rencontrer ce problème. Que vous récupériez des réponses d'API, lisiez un fichier de configuration, ou que vous expérimentiez simplement des rapports Excel pilotés par des données, transformer du JSON en une feuille de calcul propre est une demande fréquente.

Dans ce guide, nous parcourrons un exemple Java complet, prêt à l'exécution, qui **generates XLSX from JSON** et vous montre exactement comment **populate Excel from JSON** en utilisant le processeur SmartMarker d'Aspose Cells. Pas de références vagues – juste du code que vous pouvez copier, coller et exécuter.

## Ce dont vous aurez besoin

- Java 17 (ou tout JDK récent)  
- Bibliothèque Aspose Cells for Java (l'essai gratuit fonctionne)  
- Un IDE simple ou un outil de construction en ligne de commande (Maven/Gradle)  
- L'extrait JSON que nous injecterons dans le classeur  

C’est tout – pas de services supplémentaires, pas d'étapes cachées. Plongeons‑y.

## Enregistrer le classeur au format XLSX – Processus complet

Ci-dessous se trouve le programme complet, depuis l'importation de la bibliothèque jusqu'à la persistance du fichier sur disque. Faites très attention aux commentaires ; ils expliquent **why** chaque ligne est importante, pas seulement **what** elle fait.

```java
// ---------------------------------------------------------------
// Save Workbook as XLSX – Complete Java Example
// ---------------------------------------------------------------
import com.aspose.cells.*;
import com.google.gson.JsonArray; // For parsing raw JSON string

public class JsonToExcelDemo {

    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook that will receive the data
        Workbook workbook = new Workbook();

        // Step 2: Initialize the SmartMarker processor for the workbook
        SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);

        // Step 3: Enable the flag to treat an array as a single record.
        // This tells SmartMarker to iterate over each element in the JSON array.
        processor.setArrayAsSingle(true);

        // Step 4: Prepare the JSON array source.
        // In a real‑world scenario you might read this from a file or API.
        String json = "[{\"Name\":\"John\",\"Age\":30},{\"Name\":\"Anna\",\"Age\":25}]";

        // Step 5: Apply the JSON data to the SmartMarker using the placeholder ${jsonArray}
        // The JsonArray class from Aspose wraps the raw string so SmartMarker can understand it.
        processor.apply("${jsonArray}", new JsonArray(json));

        // OPTIONAL: Save the workbook to see the result.
        // This is the line that actually **save workbook as xlsx**.
        workbook.save("output.xlsx", SaveFormat.XLSX);

        System.out.println("Workbook saved successfully as output.xlsx");
    }
}
```

> **Pro tip:** Si vous utilisez Maven, ajoutez les dépendances suivantes à votre `pom.xml` :

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- check for the latest version -->
</dependency>
<dependency>
    <groupId>com.google.code.gson</groupId>
    <artifactId>gson</artifactId>
    <version>2.10.1</version>
</dependency>
```

### Résultat attendu

Après avoir exécuté le programme, ouvrez `output.xlsx`. Vous verrez une feuille nommée **Sheet1** contenant deux lignes de données :

| Name | Age |
|------|-----|
| John | 30  |
| Anna | 25  |

C’est toute l’expérience **populate excel from json** en moins de 30 lignes de Java.

![save workbook as xlsx example](example.png)

*Texte alternatif de l'image : “save workbook as xlsx example”*

## Générer un XLSX à partir de JSON – Comment fonctionne SmartMarker

SmartMarker est essentiellement un moteur de modèles pour Excel. En plaçant `${jsonArray}` dans n'importe quelle cellule (ou plage) d'un classeur vierge, vous indiquez au processeur « remplacer ce placeholder par les données du tableau JSON ». Lorsque `processor.apply` s'exécute, il :

1. Analyse le JSON en une collection d’enregistrements.  
2. Associe chaque propriété (`Name`, `Age`) à une colonne selon le contexte du placeholder.  
3. Insère les lignes automatiquement, en gérant les types de données pour vous.

Parce que nous avons appelé `processor.setArrayAsSingle(true)`, l'ensemble du tableau est traité comme un seul jeu d'enregistrements logique, ce qui est le schéma le plus courant lors de **generating XLSX from JSON**.

### Personnalisation du modèle

Si vous préférez contrôler l'ordre des colonnes ou ajouter une ligne d'en-tête, créez un petit modèle avant d'exécuter le code :

| A            | B   |
|--------------|-----|
| **Name**     | **Age** |
| ${jsonArray.Name} | ${jsonArray.Age} |

Enregistrez-le sous le nom `template.xlsx` et chargez‑le à la place d'un classeur vide :

```java
Workbook workbook = new Workbook("template.xlsx");
```

Le reste des étapes reste identique, et la sortie conservera la ligne d'en-tête que vous avez définie.

## Remplir Excel à partir de JSON – Cas limites et astuces

### 1. Objets JSON imbriqués  
SmartMarker peut plonger dans des structures imbriquées en utilisant la notation point (`${jsonArray.Address.City}`). Assurez‑vous simplement que votre chaîne JSON reflète cette hiérarchie.

### 2. Jeux de données volumineux  
Lors du traitement de milliers de lignes, désactivez le calcul du classeur avant le traitement :

```java
workbook.getSettings().setCalculateFormula(false);
```

Réactivez-le après la sauvegarde pour maintenir des performances rapides.

### 3. Types de données  
Les dates, nombres et booléens sont déduits automatiquement, mais vous pouvez forcer un format :

```java
processor.apply("${jsonArray.BirthDate}", new JsonArray(json));
workbook.getWorksheets().get(0).getCells().get("C2").setNumberFormat("mm/dd/yyyy");
```

### 4. Plusieurs placeholders  
Vous pouvez injecter plusieurs tableaux JSON dans le même classeur en utilisant des noms de placeholders distincts (`${orders}`, `${customers}`) et en appelant `processor.apply` pour chacun.

## Questions fréquentes

**Q : Dois‑je installer autre chose que le JAR Aspose Cells ?**  
R : Non. La bibliothèque est autonome ; il suffit d’ajouter le JAR (ou la dépendance Maven) et vous êtes prêt à **save workbook as xlsx**.

**Q : Puis‑je écrire directement dans un flux au lieu d’un fichier ?**  
R : Absolument. Remplacez `workbook.save("output.xlsx", SaveFormat.XLSX);` par :

```java
try (FileOutputStream out = new FileOutputStream("output.xlsx")) {
    workbook.save(out, SaveFormat.XLSX);
}
```

**Q : Que faire si mes clés JSON ne correspondent pas aux noms de colonnes Excel ?**  
R : Utilisez la méthode `SmartMarkerProcessor.setCustomFieldNames` pour mapper les clés JSON aux noms de placeholders.

## Conclusion

Nous avons couvert tout ce dont vous avez besoin pour **save workbook as xlsx** tout en **generating XLSX from JSON** et **populating Excel from JSON** en utilisant le SmartMarker d'Aspose Cells. Le petit programme montre le cycle complet : créer un classeur, configurer SmartMarker, fournir un tableau JSON, puis persister le fichier.

Ensuite, essayez d'étendre le modèle avec des formules, du style, ou plusieurs feuilles de calcul — chaque concept s’appuie directement sur la base que vous venez de maîtriser. Si vous rencontrez des particularités, revisiter la section « Cas limites et astuces » clarifie souvent les choses.

Bon codage, et que vos feuilles de calcul soient toujours aussi propres que votre JSON !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets et fonctionnels avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Comment enregistrer des fichiers XLSX avec Aspose.Cells pour .NET : guide étape par étape](/cells/english/net/workbook-operations/save-xlsx-files-aspose-cells-dotnet/)
- [Comment enregistrer un classeur Excel en Java avec Aspose.Cells](/cells/english/java/automation-batch-processing/excel-automation-java-aspose-cells-guide/)
- [Comment créer et enregistrer un classeur Excel au format SVG avec Aspose.Cells pour Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}