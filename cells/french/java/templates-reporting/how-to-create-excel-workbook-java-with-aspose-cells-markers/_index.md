---
category: general
date: 2026-11-25
description: Créer un exemple de code Java pour un classeur Excel utilisant les smart
  markers d’Aspose.Cells afin de lier les tableaux JSON comme valeurs uniques.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook java
- Aspose.Cells smart marker
- Java JSON to Excel
- setSmartMarkerData
- Excel export Java
language: fr
lastmod: 2026-11-25
og_description: Créez un classeur Excel en Java avec Aspose.Cells pour exporter facilement
  des tableaux JSON en cellules uniques. Suivez le guide pas à pas.
og_image_alt: Screenshot of an Excel workbook created in Java using Aspose.Cells smart
  markers
og_title: Créer un classeur Excel en Java – Guide du marqueur intelligent Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-11-25'
  description: Create Excel workbook Java code example using Aspose.Cells smart markers
    to bind JSON arrays as single values.
  headline: How to create Excel workbook Java with Aspose.Cells markers
  type: TechArticle
- description: Create Excel workbook Java code example using Aspose.Cells smart markers
    to bind JSON arrays as single values.
  name: How to create Excel workbook Java with Aspose.Cells markers
  steps:
  - name: '**Creates a fresh workbook** – `new Workbook()` gives you an in‑memory
      Excel file with a default sheet.'
    text: '**Creates a fresh workbook** – `new Workbook()` gives you an in‑memory
      Excel file with a default sheet.'
  - name: '**Places a smart marker in cell A1** – `{{jsonArray:ArrayAsSingle}}` tells
      Aspose.Cells to replace the marker with the *entire* array, joined by commas.'
    text: '**Places a smart marker in cell A1** – `{{jsonArray:ArrayAsSingle}}` tells
      Aspose.Cells to replace the marker with the *entire* array, joined by commas.'
  - name: '**Builds a `Map` data source** – The key `"jsonArray"` matches the marker
      name; the value is a `String[]`.'
    text: '**Builds a `Map` data source** – The key `"jsonArray"` matches the marker
      name; the value is a `String[]`.'
  - name: '**Calls `setSmartMarkerData`** – This binds the map to the marker and performs
      the replacement.'
    text: '**Calls `setSmartMarkerData`** – This binds the map to the marker and performs
      the replacement.'
  - name: '**Saves the file** – `workbook.save(...)` writes `JsonSingleValue.xlsx`
      to disk.'
    text: '**Saves the file** – `workbook.save(...)` writes `JsonSingleValue.xlsx`
      to disk.'
  - name: Open `JsonSingleValue.xlsx` in Microsoft Excel, LibreOffice Calc, or Google
      Sheets.
    text: Open `JsonSingleValue.xlsx` in Microsoft Excel, LibreOffice Calc, or Google
      Sheets.
  - name: Confirm that cell **A1** reads `One, Two, Three`.
    text: Confirm that cell **A1** reads `One, Two, Three`.
  - name: Check that no extra rows or columns were added – the smart marker performed
      an in‑place replacement.
    text: Check that no extra rows or columns were added – the smart marker performed
      an in‑place replacement.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Comment créer un classeur Excel en Java avec des marqueurs Aspose.Cells
url: /fr/java/templates-reporting/how-to-create-excel-workbook-java-with-aspose-cells-markers/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment créer un classeur Excel Java avec les marqueurs Aspose.Cells

Si vous avez besoin de **créer un classeur Excel Java** dont le code écrit un tableau JSON dans une seule cellule, ce tutoriel vous montre exactement comment faire. En utilisant les marqueurs intelligents d'Aspose.Cells, vous pouvez traiter un tableau complet comme une seule valeur, évitant ainsi les boucles manuelles et les écritures cellule par cellule.

Vous apprendrez comment configurer un classeur, définir un marqueur intelligent, lier une source de données `Map` contenant un tableau de type JSON, et enfin enregistrer le fichier. L'exemple fonctionne avec Java 17+, Maven et la bibliothèque d'essai gratuite Aspose.Cells for Java.

---

![Capture d'écran d'un classeur Excel créé en Java à l'aide des marqueurs intelligents Aspose.Cells](excel-workbook-java.png){: .center-image alt="Capture d'écran d'un classeur Excel créé en Java à l'aide des marqueurs intelligents Aspose.Cells"}

## Prérequis

| Exigence | Pourquoi c'est important |
|----------|---------------------------|
| Java 17 ou version ultérieure | Les dernières fonctionnalités du langage et les mises à jour de sécurité |
| Maven 3.6+ | Simplifie la gestion des dépendances |
| Aspose.Cells for Java (v23.12 ou plus récent) | Fournit les API `Workbook`, `Worksheet` et smart‑marker utilisées dans l'exemple |
| Connaissances de base des collections Java | Vous créerez un `Map<String, Object>` qui sert de source de données |

Ajoutez la dépendance Aspose.Cells à votre `pom.xml` :

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
    <classifier>jdk17</classifier>
</dependency>
```

---

## Créer un classeur Excel Java – exemple complet

Le programme suivant est une solution **complète et exécutable**. Copiez‑le dans un fichier nommé `ExcelSmartMarkerDemo.java`, compilez‑le et exécutez‑le.

```java
package com.example.excel;

import com.aspose.cells.*;
import java.util.HashMap;
import java.util.Map;

/**
 * Demonstrates how to create Excel workbook Java using Aspose.Cells smart markers.
 * The smart marker "{{jsonArray:ArrayAsSingle}}" treats the whole array as a single cell value.
 */
public class ExcelSmartMarkerDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();                       // empty workbook
        Worksheet worksheet = workbook.getWorksheets().get(0);    // first (default) sheet

        // Step 2: Define a smart marker that treats a JSON array as a single value
        // The "ArrayAsSingle" option concatenates the array elements with commas.
        String smartMarker = "{{jsonArray:ArrayAsSingle}}";
        worksheet.getCells().get("A1").putValue(smartMarker);

        // Step 3: Prepare the data source – a simple string array
        Map<String, Object> dataSource = new HashMap<>();
        dataSource.put("jsonArray", new String[] { "One", "Two", "Three" });

        // Step 4: Bind the data to the smart marker and save the workbook
        worksheet.getCells().get("A1").setSmartMarkerData(dataSource);
        workbook.save("JsonSingleValue.xlsx");   // workbook saved to project root
        System.out.println("Workbook created successfully.");
    }
}
```

### Ce que fait le code

1. **Crée un nouveau classeur** – `new Workbook()` vous fournit un fichier Excel en mémoire avec une feuille par défaut.  
2. **Place un marqueur intelligent dans la cellule A1** – `{{jsonArray:ArrayAsSingle}}` indique à Aspose.Cells de remplacer le marqueur par le *tableau complet*, joint par des virgules.  
3. **Construit une source de données `Map`** – La clé `"jsonArray"` correspond au nom du marqueur ; la valeur est un `String[]`.  
4. **Appelle `setSmartMarkerData`** – Cela lie la map au marqueur et effectue le remplacement.  
5. **Enregistre le fichier** – `workbook.save(...)` écrit `JsonSingleValue.xlsx` sur le disque.

Lorsque vous ouvrez le fichier Excel généré, la cellule **A1** contient :

```
One, Two, Three
```

Le tableau est rendu comme une chaîne unique séparée par des virgules grâce à l'option `ArrayAsSingle`.

---

## Utiliser le marqueur intelligent Aspose.Cells pour lier des données JSON

Les marqueurs intelligents Aspose.Cells sont un moyen puissant de mapper des objets complexes (y compris des structures de type JSON) directement sur les feuilles de calcul. La syntaxe `{{fieldName:Option}}` fonctionne à la manière d'un moteur de templates :

* **fieldName** – la clé dans votre source de données (`Map`, POJO ou `DataTable`).  
* **Option** – contrôle la façon dont les collections sont gérées. `ArrayAsSingle` traite l'ensemble de la collection comme une seule valeur ; d'autres options comme `Array` étendraient le tableau sur plusieurs lignes.

**Pourquoi utiliser un marqueur intelligent plutôt qu'une boucle ?**  
Une boucle nécessite des calculs manuels d'adresses de cellules, un indexage sujet aux erreurs et du code supplémentaire pour le style. Les marqueurs intelligents vous permettent d'écrire des espaces réservés déclaratifs, de garder votre code Java concis, et la bibliothèque se charge des détails de mise en page.

---

## Configurer la source de données Java Map

Le `Map<String, Object>` est le conteneur de données le plus simple pour Aspose.Cells :

```java
Map<String, Object> dataSource = new HashMap<>();
dataSource.put("jsonArray", new String[] { "One", "Two", "Three" });
```

*La clé (`jsonArray`) doit correspondre exactement au nom du marqueur.*  
Vous pouvez également utiliser un `List<String>`, un POJO personnalisé, ou même un `Map` imbriqué pour des structures JSON plus complexes. Aspose.Cells parcourra automatiquement le graphe d'objets.

**Astuce :** Si vous devez formater la chaîne concaténée différemment (par ex., en utilisant des points‑virgules), prétraitez le tableau en Java avant de l'assigner à la map :

```java
String joined = String.join(";", new String[] {"One","Two","Three"});
dataSource.put("jsonArray", new String[] { joined });
```

---

## Enregistrer le classeur et vérifier la sortie

```java
workbook.save("JsonSingleValue.xlsx");
```

La méthode `save` prend en charge de nombreux formats (`.xlsx`, `.xls`, `.csv`, `.pdf`). Pour ce tutoriel, nous conservons le format Excel Open XML par défaut.

**Étapes de vérification**

1. Ouvrez `JsonSingleValue.xlsx` dans Microsoft Excel, LibreOffice Calc ou Google Sheets.  
2. Vérifiez que la cellule **A1** affiche `One, Two, Three`.  
3. Assurez‑vous qu'aucune ligne ou colonne supplémentaire n'a été ajoutée – le marqueur intelligent a effectué un remplacement sur place.

Si la cellule affiche le texte brut du marqueur (`{{jsonArray:ArrayAsSingle}}`), revérifiez que :

* Le nom du marqueur correspond exactement à la clé de la map (sensible à la casse).  
* `setSmartMarkerData` est appelé **après** que le marqueur ait été placé.  
* La version d'Aspose.Cells prend en charge l'option `ArrayAsSingle` (disponible depuis la v20.3).

---

## Variations courantes et cas limites

| Scénario | Ajustement |
|----------|------------|
| **Délimiteur différent** | Utilisez `ArrayAsSingle` conjointement avec une jointure personnalisée en Java (voir l'astuce ci‑dessus). |
| **Plusieurs tableaux sur une même feuille** | Placez des marqueurs supplémentaires comme `{{anotherArray:ArrayAsSingle}}` dans d'autres cellules et ajoutez les entrées correspondantes à la map. |
| **Objets JSON imbriqués** | Fournissez un `Map<String, Object>` imbriqué ; référencez les champs avec la notation pointée (`{{parent.child}}`). |
| **Ensembles de données volumineux** | Pour des milliers de lignes, privilégiez l'option `Array` afin de laisser Aspose.Cells développer les lignes automatiquement, ce qui |

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités supplémentaires de l'API et explorer des approches d'implémentation alternatives dans vos propres projets.

- [Comment créer et exporter Excel en HTML avec Aspose.Cells Java | Guide des opérations de classeur](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [Exporter un classeur Excel en image avec Aspose.Cells for Java : guide étape par étape](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)
- [Comment créer et enregistrer un classeur Excel au format SVG avec Aspose.Cells for Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}