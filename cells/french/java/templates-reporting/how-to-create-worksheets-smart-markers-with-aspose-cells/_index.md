---
category: general
date: 2026-08-20
description: Créer des marqueurs intelligents de feuilles de calcul en Java à l'aide
  d'Aspose.Cells et contrôler le nommage des feuilles de détail avec SmartMarkerOptions.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create worksheets smart markers
- Aspose.Cells Java
- smart marker options
- duplicate sheet names
- detail sheet naming
language: fr
lastmod: 2026-08-20
og_description: Créez des marqueurs intelligents de feuilles de calcul en Java avec
  Aspose.Cells. Apprenez à nommer les feuilles de détail dynamiquement en utilisant
  SmartMarkerOptions.
og_image_alt: create worksheets smart markers example diagram
og_title: Créer des marqueurs intelligents de feuilles de calcul – Guide Java avec
  Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Create worksheets smart markers in Java using Aspose.Cells and control
    detail sheet naming with SmartMarkerOptions.
  headline: How to create worksheets smart markers with Aspose.Cells
  type: TechArticle
- description: Create worksheets smart markers in Java using Aspose.Cells and control
    detail sheet naming with SmartMarkerOptions.
  name: How to create worksheets smart markers with Aspose.Cells
  steps:
  - name: Set up the Maven project and add Aspose.Cells
    text: 'Create a new Maven module (or Gradle project) and add the Aspose.Cells
      dependency:'
  - name: Load the master workbook that contains smart markers
    text: '```java import com.aspose.cells.*;'
  - name: Configure SmartMarkerOptions for custom detail sheet names
    text: '```java // Define naming pattern for detail sheets. SmartMarkerOptions
      smartMarkerOptions = new SmartMarkerOptions(); // {0} is automatically replaced
      by the row index (starting at 1). smartMarkerOptions.setDetailSheetNewName("DetailSheet_{0}");
      ```'
  - name: Build a DataTable that matches the smart marker fields
    text: '```java // Build a simple DataTable with two columns. DataTable data =
      new DataTable(); data.getColumns().add("Id", DataType.INTEGER); data.getColumns().add("Value",
      DataType.STRING); // Add sample rows. data.getRows().add(new Object[] { 1, "A"
      }); data.getRows().add(new Object[] { 2, "B" }); ```'
  - name: Apply the data to the smart markers with the naming options
    text: '```java // Apply the data to the first worksheet (index 0). workbook.getWorksheets().get(0).getSmartMarkers().apply(data,
      smartMarkerOptions); ```'
  - name: Save the workbook and verify the result
    text: '```java // Save the expanded workbook. workbook.save("YOUR_DIRECTORY/MasterDetailDuplicatedNames.xlsx");
      } } ```'
  - name: Multiple master sheets
    text: 'If your template contains more than one master sheet, iterate over each
      sheet’s smart markers:'
  - name: Custom naming beyond the row index
    text: 'You can embed any data column into the sheet name by using placeholders
      like `{ColumnName}`:'
  - name: Preventing overly long sheet names
    text: 'Excel limits sheet names to 31 characters. If your naming pattern risks
      exceeding this limit, truncate or hash the value:'
  type: HowTo
tags:
- Java
- Aspose.Cells
- Smart Markers
- Excel Automation
title: Comment créer des marqueurs intelligents de feuilles de calcul avec Aspose.Cells
url: /fr/java/templates-reporting/how-to-create-worksheets-smart-markers-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment créer des marqueurs intelligents de feuilles de calcul avec Aspose.Cells

Si vous devez **créer des marqueurs intelligents de feuilles de calcul** dans un classeur Java, ce guide vous montre les étapes exactes pour le faire avec Aspose.Cells. Vous verrez comment configurer `SmartMarkerOptions` afin que chaque feuille de détail reçoive un nom unique et prévisible.

Générer des rapports Excel qui développent un modèle maître‑détail est une exigence courante dans les systèmes financiers, de gestion des stocks et de reporting. L’utilisation de marqueurs intelligents élimine la duplication manuelle des feuilles et vous permet de vous concentrer sur les données plutôt que sur la plomberie.

## Ce que vous allez apprendre

* Comment charger un classeur maître contenant des marqueurs intelligents.  
* Comment définir `SmartMarkerOptions` pour contrôler la dénomination des feuilles de détail générées.  
* Comment fournir un `DataTable` avec des données d'exemple et l'appliquer aux marqueurs intelligents.  
* Comment enregistrer le résultat afin que chaque feuille de détail possède un nom distinct, évitant les noms de feuilles en double.

**Prérequis**  
* Java 17 ou version ultérieure (le code se compile également avec JDK 8+).  
* Aspose.Cells for Java 23.9 ou plus récent – la bibliothèque fournit les classes `Workbook`, `SmartMarkerOptions` et les classes associées.  
* Un IDE tel qu’IntelliJ IDEA, Eclipse ou VS Code.

Les concepts secondaires que vous rencontrerez incluent **Aspose.Cells Java**, **smart marker options**, et la gestion des **noms de feuilles en double** lorsque le modèle se développe.

## Créer des marqueurs intelligents de feuilles de calcul – guide étape par étape

Les sections suivantes décomposent le processus en étapes discrètes et réutilisables. Chaque étape comprend un extrait de code, une explication de son importance et des conseils pratiques pour éviter les pièges courants.

### Étape 1 : Configurer le projet Maven et ajouter Aspose.Cells

Créez un nouveau module Maven (ou un projet Gradle) et ajoutez la dépendance Aspose.Cells :

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
</dependency>
```

**Pourquoi cette étape est importante** – La bibliothèque fournit la classe `Workbook` qui lit et écrit des fichiers Excel, ainsi que le moteur de marqueurs intelligents qui développe automatiquement votre modèle. Sans la dépendance correcte, le compilateur ne peut pas résoudre les appels d'API utilisés plus tard.

> **Astuce :** Si vous travaillez derrière un proxy d’entreprise, configurez le `settings.xml` de Maven pour récupérer le dépôt Aspose de manière sécurisée.

### Étape 2 : Charger le classeur maître contenant des marqueurs intelligents

```java
import com.aspose.cells.*;

public class DuplicateDetailSheetNames {
    public static void main(String[] args) throws Exception {
        // Load the template that holds the smart marker tags.
        Workbook workbook = new Workbook("YOUR_DIRECTORY/MasterDetailTemplate.xlsx");
```

**Pourquoi cette étape est importante** – Le classeur maître définit la mise en page, les formules et les balises d'espace réservé (`«SmartMarker»`) que le moteur remplacera. Charger le fichier une fois maintient une faible utilisation de la mémoire et vous permet de réutiliser le même classeur pour plusieurs ensembles de données.

### Étape 3 : Configurer SmartMarkerOptions pour des noms de feuilles de détail personnalisés

```java
        // Define naming pattern for detail sheets.
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions();
        // {0} is automatically replaced by the row index (starting at 1).
        smartMarkerOptions.setDetailSheetNewName("DetailSheet_{0}");
```

**Pourquoi cette étape est importante** – Par défaut, Aspose.Cells crée des feuilles de détail avec des noms génériques comme «DetailSheet». Lorsque le modèle se développe pour de nombreuses lignes, ces noms entrent en conflit, entraînant des **noms de feuilles en double** et une exception d’exécution. Le modèle `"DetailSheet_{0}"` garantit un nom unique par ligne, résolvant le problème de duplication.

### Étape 4 : Construire un DataTable correspondant aux champs du marqueur intelligent

```java
        // Build a simple DataTable with two columns.
        DataTable data = new DataTable();
        data.getColumns().add("Id", DataType.INTEGER);
        data.getColumns().add("Value", DataType.STRING);
        // Add sample rows.
        data.getRows().add(new Object[] { 1, "A" });
        data.getRows().add(new Object[] { 2, "B" });
```

**Pourquoi cette étape est importante** – Le `DataTable` fournit les valeurs réelles qui remplacent les espaces réservés du marqueur intelligent. Les noms de colonnes doivent correspondre aux noms des marqueurs dans le modèle ; sinon le moteur ignore le remplacement silencieusement.

> **Erreur courante** : Utiliser un nom de colonne qui diffère par la casse (par ex., «id» vs «Id») entraîne des données manquantes dans les feuilles générées.

### Étape 5 : Appliquer les données aux marqueurs intelligents avec les options de nommage

```java
        // Apply the data to the first worksheet (index 0).
        workbook.getWorksheets().get(0).getSmartMarkers().apply(data, smartMarkerOptions);
```

**Pourquoi cette étape est importante** – La méthode `apply` déclenche le moteur de marqueurs intelligents. Elle lit chaque ligne, crée une nouvelle feuille de détail en utilisant le modèle de nommage de `SmartMarkerOptions`, et remplit la feuille avec les données de la ligne. Cet appel unique remplace des dizaines de lignes de clonage manuel de feuilles et de remplissage de cellules.

### Étape 6 : Enregistrer le classeur et vérifier le résultat

```java
        // Save the expanded workbook.
        workbook.save("YOUR_DIRECTORY/MasterDetailDuplicatedNames.xlsx");
    }
}
```

Après exécution, ouvrez `MasterDetailDuplicatedNames.xlsx`. Vous devriez voir :

* La feuille maître originale inchangée.  
* Deux nouvelles feuilles nommées `DetailSheet_1` et `DetailSheet_2`.  
* Chaque feuille de détail contient les valeurs de la ligne correspondante du `DataTable`.

**Pourquoi cette étape est importante** – La persistance du classeur finalise l’expansion du marqueur intelligent. Le fichier peut maintenant être envoyé aux systèmes en aval, joint à des e‑mails, ou ouvert dans Excel pour une analyse supplémentaire.

## Gestion des cas limites et des variations

### Plusieurs feuilles maîtres

Si votre modèle contient plus d’une feuille maître, itérez sur les marqueurs intelligents de chaque feuille :

```java
for (int i = 0; i < workbook.getWorksheets().getCount(); i++) {
    workbook.getWorksheets().get(i).getSmartMarkers().apply(data, smartMarkerOptions);
}
```

### Nom personnalisé au‑delà de l’indice de ligne

Vous pouvez intégrer n’importe quelle colonne de données dans le nom de la feuille en utilisant des espaces réservés comme `{ColumnName}` :

```java
smartMarkerOptions.setDetailSheetNewName("Order_{OrderId}");
```

Assurez‑vous que la colonne `OrderId` existe dans le `DataTable` fourni.

### Prévenir les noms de feuilles trop longs

Excel limite les noms de feuilles à 31 caractères. Si votre modèle de nommage risque de dépasser cette limite, tronquez ou hachez la valeur :

```java
String pattern = "Detail_{0}_{1}";
smartMarkerOptions.setDetailSheetNewName(pattern);
```

Puis post‑traitez le nom généré avec `StringUtils.abbreviate` avant de le transmettre à Aspose.

## Exemple complet exécutable

Voici le fichier source complet que vous pouvez copier, ajuster les chemins de fichiers, et exécuter directement :

```java
import com.aspose.cells.*;

public class DuplicateDetailSheetNames {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the master workbook that contains smart markers
        Workbook workbook = new Workbook("YOUR_DIRECTORY/MasterDetailTemplate.xlsx");

        // 2️⃣ Define how detail sheets will be named when they are created
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions();
        // {0} is replaced by the row index (starting at 1)
        smartMarkerOptions.setDetailSheetNewName("DetailSheet_{0}");

        // 3️⃣ Prepare sample data to populate the smart markers
        DataTable data = new DataTable();
        data.getColumns().add("Id", DataType.INTEGER);
        data.getColumns().add("Value", DataType.STRING);
        data.getRows().add(new Object[] { 1, "A" });
        data.getRows().add(new Object[] { 2, "B" });

        // 4️⃣ Apply the data to the smart markers using the naming options
        workbook.getWorksheets().get(0).getSmartMarkers().apply(data, smartMarkerOptions);

        // 5️⃣ Save the workbook – each detail sheet now has a unique name
        workbook.save("YOUR_DIRECTORY/MasterDetailDuplicatedNames.xlsx");
    }
}
```

**Sortie attendue**

* `MasterDetailDuplicatedNames.xlsx` contient :

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Mastering Aspose.Cells Java: Utilize Smart Markers for Dynamic Data in Worksheets](/cells/english/java/worksheet-management/aspose-cells-java-smart-markers-worksheets/)
- [Create Dynamic Charts with Smart Markers in Aspose.Cells for Java | Step-by-Step Guide](/cells/english/java/charts-graphs/dynamic-charts-smart-markers-aspose-cells-java/)
- [Aspose Cells Java Smart Markers Worksheets](/cells/german/java/worksheet-management/aspose-cells-java-smart-markers-worksheets/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}