---
category: general
date: 2026-06-30
description: Remplir le modèle Excel avec des données en utilisant SmartMarkerProcessor
  et apprendre comment créer un rapport Excel à partir du modèle en Java – guide étape
  par étape.
draft: false
keywords:
- populate excel template with data
- create excel report from template
- smartmarkerprocessor java
- excel automation java
- java data source excel
language: fr
og_description: Remplissez le modèle Excel avec des données en utilisant SmartMarkerProcessor.
  Ce guide montre comment créer un rapport Excel à partir d’un modèle en Java, avec
  le code complet.
og_title: Remplir le modèle Excel avec des données – Créer un rapport Excel à partir
  du modèle
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Populate Excel template with data using SmartMarkerProcessor and learn
    how to create Excel report from template in Java – step‑by‑step guide.
  headline: Populate Excel Template with Data – Create Excel Report from Template
  type: TechArticle
- description: Populate Excel template with data using SmartMarkerProcessor and learn
    how to create Excel report from template in Java – step‑by‑step guide.
  name: Populate Excel Template with Data – Create Excel Report from Template
  steps:
  - name: Instantiate the SmartMarkerProcessor
    text: The processor is the engine that scans your workbook, finds Smart Markers,
      and replaces them with real values.
  - name: '(Optional): Rename the Detail Sheet'
    text: Smart Markers often generate a hidden “detail” sheet that holds intermediate
      data. Renaming it makes the final workbook easier to navigate.
  - name: Load the Template Workbook
    text: This is where you point the processor at the Excel file that contains the
      markers.
  - name: Prepare a Data Source
    text: SmartMarkerProcessor expects an `IDataSource` implementation that knows
      how to fetch values for each marker. Below is a minimal **in‑memory** data source
      that uses a `Map<String, Object>`.
  - name: Apply the Data to the Workbook
    text: Now the magic happens—Smart Markers are replaced with the values from your
      `IDataSource`.
  - name: Save the Processed Workbook
    text: Finally, write the populated workbook to disk (or stream it directly to
      HTTP response if you’re in a web app).
  - name: 'H3: Handling Collections (Tables)'
    text: If your template contains a repeating block like a sales table, replace
      the marker with an array in your data source.
  - name: 'H3: Formatting Dates and Numbers'
    text: 'Smart Markers respect cell formatting. If you pre‑format a cell as *Currency*
      in the template, the numeric value you push through will automatically display
      with the correct symbol and decimal places. No extra code needed—just make sure
      the data type you return (`Double`, `BigDecimal`, `LocalDate`) '
  - name: 'H3: Performance Considerations'
    text: '- **Reuse the processor** if you generate dozens of reports in a batch;
      just call `processor.clear()` between runs. - **Turn off calculation** (`workbook.getSettings().setRecalcOnLoad(false)`)
      when you only need to write values, not recalculate formulas. - **Stream the
      output** to avoid large tempor'
  type: HowTo
tags:
- excel
- java
- reporting
- smartmarker
title: Remplir le modèle Excel avec des données – Créer un rapport Excel à partir
  du modèle
url: /fr/java/templates-reporting/populate-excel-template-with-data-create-excel-report-from-t/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Remplir un modèle Excel avec des données – Créer un rapport Excel à partir d’un modèle

Vous avez déjà eu besoin de **remplir un modèle Excel avec des données** mais vous ne saviez pas quelle bibliothèque pouvait gérer la tâche lourde ? Vous n’êtes pas seul. Lorsque vous créez des tableaux de bord mensuels, des factures ou tout autre classeur piloté par des données, le faire manuellement devient rapidement un cauchemar.  

La bonne nouvelle, c’est que le **SmartMarkerProcessor** d’Aspose.Cells rend cela indolore — il suffit de lui fournir un modèle et une source de données, et vous obtenez un rapport Excel soigné en quelques secondes. Dans ce tutoriel, nous vous montrerons également **comment créer un rapport Excel à partir d’un modèle** en Java pur, afin que vous puissiez intégrer la solution directement dans votre projet.

## Prérequis (Ce dont vous avez besoin)

- Java 17 ou supérieur (le code se compile avec des versions antérieures, mais 17 vous donne les dernières fonctionnalités du langage).  
- Aspose.Cells for Java (l’artifact Maven `com.aspose:aspose-cells` version 24.9 ou ultérieure).  
- Un fichier Excel contenant des Smart Markers (par ex. `input.xlsx`).  
- Une source de données simple implémentant `IDataSource` (nous en créerons une pour vous).  

Aucun IDE spécial n’est requis — n’importe quel éditeur capable de compiler du Java fera l’affaire.  

---

## Remplir un modèle Excel avec des données – Étape par étape

Nous décomposons le processus en six étapes logiques. Chaque étape indique **pourquoi** elle est importante, pas seulement **quoi** taper.

### Étape 1 : Instancier le SmartMarkerProcessor  

Le processeur est le moteur qui parcourt votre classeur, trouve les Smart Markers et les remplace par de vraies valeurs.

```java
// Step 1: Create a SmartMarkerProcessor instance
SmartMarkerProcessor processor = new SmartMarkerProcessor();
```

*Pourquoi ?*  
Créer un nouveau processeur garantit un état propre. Si vous réutilisez une ancienne instance, des paramètres résiduels pourraient se répercuter sur l’exécution suivante — ce que vous voulez absolument éviter en production.

### Étape 2 (Optionnelle) : Renommer la feuille de détail  

Les Smart Markers génèrent souvent une feuille « detail » cachée qui contient des données intermédiaires. La renommer rend le classeur final plus facile à parcourir.

```java
// Step 2: (Optional) Set a new name for the detail sheet that will be generated
processor.setDetailSheetNewName("CopyOfDetail");
```

*Astuce :*  
Si votre modèle possède déjà une feuille nommée « Detail », donnez à la feuille générée un suffixe unique (par ex. `CopyOfDetail_2024`) afin d’éviter les collisions de noms.

### Étape 3 : Charger le classeur modèle  

C’est ici que vous indiquez au processeur le fichier Excel contenant les marqueurs.

```java
// Step 3: Load the workbook that contains Smart Markers
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

*Pourquoi ?*  
Charger le classeur en mémoire permet à Aspose.Cells de le manipuler sans toucher au fichier original sur le disque. Vous pouvez réutiliser le même fichier modèle pour plusieurs rapports en toute sécurité.

### Étape 4 : Préparer une source de données  

SmartMarkerProcessor attend une implémentation de `IDataSource` capable de récupérer les valeurs pour chaque marqueur. Voici une source de données **en‑mémoire** minimale qui utilise un `Map<String, Object>`.

```java
// Step 4: Prepare the data source that provides values for the markers
class MapDataSource implements IDataSource {
    private final Map<String, Object> data;

    public MapDataSource(Map<String, Object> data) {
        this.data = data;
    }

    @Override
    public Object getValue(String key) {
        return data.get(key);
    }

    @Override
    public boolean isArray(String key) {
        // For this simple example we never return arrays
        return false;
    }

    @Override
    public int getLength(String key) {
        return 0; // not an array
    }

    @Override
    public Object getValue(String key, int index) {
        return null; // not an array
    }
}

// Example data that matches the markers in input.xlsx
Map<String, Object> values = new HashMap<>();
values.put("EmployeeName", "Jane Doe");
values.put("Department", "Engineering");
values.put("Salary", 95000);
values.put("ReportDate", LocalDate.now().toString());

IDataSource dataSource = new MapDataSource(values);
```

*Pourquoi cette implémentation ?*  
Elle est légère, ne nécessite aucune base de données externe et est parfaite pour les démonstrations ou les tests unitaires. Dans un scénario réel, vous remplaceriez `MapDataSource` par quelque chose qui extrait les données d’un résultat JDBC, d’une API REST ou d’une entité ORM.

### Étape 5 : Appliquer les données au classeur  

Le moment magique arrive — les Smart Markers sont remplacés par les valeurs de votre `IDataSource`.

```java
// Step 5: Apply the data to the workbook, generating the detail sheet
processor.apply(workbook, dataSource);
```

*Que se passe‑t‑il en coulisses ?*  
Aspose.Cells parcourt chaque cellule contenant un marqueur tel que `${EmployeeName}`. Pour chaque marqueur, il appelle `IDataSource.getValue("EmployeeName")` et écrit la valeur retournée dans la cellule. Si vous aviez un marqueur de tableau (`${Employees}`), le processeur étendrait automatiquement les lignes en fonction de la longueur du tableau.

### Étape 6 : Enregistrer le classeur traité  

Enfin, écrivez le classeur rempli sur le disque (ou diffusez‑le directement dans une réponse HTTP si vous êtes dans une application web).

```java
// Step 6: Save the processed workbook
workbook.save("YOUR_DIRECTORY/output.xlsx");
```

*Conseil :*  
Utilisez la surcharge `workbook.save(OutputStream, SaveFormat.XLSX)` lorsque vous devez envoyer le fichier à un client sans toucher au système de fichiers.

---

## Créer un rapport Excel à partir d’un modèle – Conseils avancés

Maintenant que le flux de base fonctionne, explorons quelques améliorations courantes qui rendent votre **rapport Excel à partir d’un modèle** prêt pour la production.

### H3 : Gestion des collections (tables)

Si votre modèle contient un bloc répété comme un tableau de ventes, remplacez le marqueur par un tableau dans votre source de données.

```java
class ListDataSource implements IDataSource {
    private final Map<String, List<Map<String, Object>>> tables = new HashMap<>();

    public void addTable(String name, List<Map<String, Object>> rows) {
        tables.put(name, rows);
    }

    @Override
    public boolean isArray(String key) {
        return tables.containsKey(key);
    }

    @Override
    public int getLength(String key) {
        List<Map<String, Object>> rows = tables.get(key);
        return rows == null ? 0 : rows.size();
    }

    @Override
    public Object getValue(String key, int index) {
        List<Map<String, Object>> rows = tables.get(key);
        return rows != null ? rows.get(index) : null;
    }

    @Override
    public Object getValue(String key) {
        // Not used for arrays
        return null;
    }
}

// Sample table data
List<Map<String, Object>> sales = new ArrayList<>();
sales.add(Map.of("Product", "Widget A", "Qty", 120, "Revenue", 4800));
sales.add(Map.of("Product", "Widget B", "Qty", 75,  "Revenue", 3375));

ListDataSource listSource = new ListDataSource();
listSource.addTable("SalesData", sales);

// Apply as before
processor.apply(workbook, listSource);
```

Dans le modèle, vous auriez des marqueurs tels que `${SalesData.Product}`, `${SalesData.Qty}`, etc., à l’intérieur d’une ligne que Aspose dupliquera pour chaque entrée.

### H3 : Mise en forme des dates et des nombres

Les Smart Markers respectent le format de cellule. Si vous pré‑formatez une cellule en *Currency* dans le modèle, la valeur numérique que vous injectez s’affichera automatiquement avec le bon symbole et le bon nombre de décimales. Aucun code supplémentaire n’est nécessaire — assurez‑vous simplement que le type de données retourné (`Double`, `BigDecimal`, `LocalDate`) correspond au format attendu.

### H3 : Considérations de performance

- **Réutilisez le processeur** si vous générez des dizaines de rapports en lot ; appelez simplement `processor.clear()` entre les exécutions.  
- **Désactivez le calcul** (`workbook.getSettings().setRecalcOnLoad(false)`) lorsque vous avez seulement besoin d’écrire des valeurs, pas de recalculer les formules.  
- **Diffusez la sortie** pour éviter de gros fichiers temporaires dans un environnement contraint.

---

## Résultat attendu

Après avoir exécuté l’exemple en six étapes, `output.xlsx` contiendra :

| A               | B          | C            |
|-----------------|------------|--------------|
| EmployeeName    | Jane Doe   |              |
| Department      | Engineering|              |
| Salary          | 95,000     |              |
| ReportDate      | 2026‑06‑30 |              |
| …               | …          | …            |

Si vous avez ajouté l’exemple de tableau, vous verrez un tableau de ventes entièrement renseigné juste sous les lignes d’en‑tête. Toute la mise en forme appliquée dans `input.xlsx` (symboles monétaires, modèles de date, en‑têtes en gras) reste intacte.

---

## Conclusion

Nous venons de parcourir comment **remplir un modèle Excel avec des données** en utilisant le `SmartMarkerProcessor` d’Aspose.Cells, et vous connaissez maintenant les étapes exactes pour **créer un rapport Excel à partir d’un modèle** en Java. L’idée centrale est simple : définissez des Smart Markers dans un classeur réutilisable, fournissez un `IDataSource` conforme, et laissez la bibliothèque faire le gros du travail.  

À partir d’ici, vous pouvez :

- Brancher une vraie base de données à la place du `MapDataSource`.  
- Ajouter des graphiques qui se mettent à jour automatiquement avec les nouvelles données.  
- Déployer le code comme micro‑service renvoyant le fichier Excel généré à la demande.  

Testez, ajustez les marqueurs, et voyez votre flux de reporting se réduire drastiquement. Vous avez des questions ou un scénario de marqueur complexe ? Laissez un commentaire ci‑dessous—bon codage !


## Que devez‑vous apprendre ensuite ?


Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Populate Excel with Nested Data Using Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/data-manipulation/populate-excel-nested-data-aspose-cells-java/)
- [Export XML Data from Excel using Aspose.Cells in Java: Step‑By‑Step Guide](/cells/english/java/import-export/export-excel-xml-data-aspose-cells-java/)
- [How to Create & Format Excel Cells Using Aspose.Cells for Java: A Step‑By‑Step Guide](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}