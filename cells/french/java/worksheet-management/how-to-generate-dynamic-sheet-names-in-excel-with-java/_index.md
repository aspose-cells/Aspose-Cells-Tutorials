---
category: general
date: 2026-09-27
description: Apprenez à générer des noms de feuilles dynamiques dans Excel avec Java
  tout en remplissant un modèle Excel et en créant des feuilles à partir des données
  pour des rapports robustes.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- dynamic sheet names
- generate multiple sheets
- create sheets from data
- populate excel template java
language: fr
lastmod: 2026-09-27
og_description: Les noms de feuilles dynamiques vous permettent de générer plusieurs
  feuilles à partir d’un ensemble de données. Ce tutoriel montre comment remplir un
  modèle Excel en Java et créer des feuilles à partir de données en utilisant Aspose.Cells.
og_image_alt: Screenshot showing an Excel workbook with dynamically generated sheet
  names using Java
og_title: Générer des noms de feuilles dynamiques dans Excel avec Java
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Learn how to generate dynamic sheet names in Excel with Java while
    you populate an Excel template and create sheets from data for robust reporting.
  headline: How to generate dynamic sheet names in Excel with Java
  type: TechArticle
- description: Learn how to generate dynamic sheet names in Excel with Java while
    you populate an Excel template and create sheets from data for robust reporting.
  name: How to generate dynamic sheet names in Excel with Java
  steps:
  - name: Add the Aspose.Cells for Java JAR to your project’s classpath (available
      from Maven Central or the Aspose website).
    text: Add the Aspose.Cells for Java JAR to your project’s classpath (available
      from Maven Central or the Aspose website).
  - name: Place `MasterDetailTemplate.xlsx` in `templates/` relative to the project
      root.
    text: Place `MasterDetailTemplate.xlsx` in `templates/` relative to the project
      root.
  - name: Execute the `main` method. The `output/` folder will contain the generated
      file.
    text: Execute the `main` method. The `output/` folder will contain the generated
      file.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Comment générer des noms de feuilles dynamiques dans Excel avec Java
url: /fr/java/worksheet-management/how-to-generate-dynamic-sheet-names-in-excel-with-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment générer des noms de feuilles dynamiques dans Excel avec Java

Si vous avez besoin de **noms de feuilles dynamiques** lors du remplissage d’un modèle Excel en Java, ce guide vous accompagne à travers le processus complet. Vous verrez comment *générer plusieurs feuilles* à partir d’une collection de données, et comment chaque feuille reçoit automatiquement un nom unique. À la fin, vous disposerez d’un exemple exécutable qui crée des feuilles à partir des données et enregistre le résultat avec la convention de nommage souhaitée.

Générer des feuilles à la volée est une exigence courante pour les tableaux de bord de reporting, les lots de factures, ou tout scénario où le nombre de sections détaillées n’est pas connu à l’avance. Le moteur Smart Marker d’Aspose.Cells rend cette tâche concise et fiable, et le code ci‑dessous montre l’approche recommandée.

## Utilisation de noms de feuilles dynamiques avec Aspose.Cells

Aspose.Cells for Java fournit un processeur **Smart Marker** qui peut lire les espaces réservés dans un classeur modèle et les développer en lignes, colonnes ou même nouvelles feuilles de calcul. En configurant `SmartMarkerOptions.DetailSheetNewName`, vous contrôlez le nom de chaque feuille générée. L’espace réservé `{0}` est remplacé par l’indice zéro‑based de la ligne de données courante, vous offrant des **noms de feuilles dynamiques** tels que `Detail_0`, `Detail_1`, …​.

> **Astuce :** Conservez le classeur modèle dans un dossier de ressources dédié et utilisez un chemin relatif lorsque c’est possible. Cela évite de coder en dur des chemins absolus qui se cassent sur différents environnements.

## Étape 1 : Charger le modèle Excel (populate excel template java)

Tout d’abord, chargez le classeur qui contient les balises Smart Marker. Le modèle doit comporter une feuille nommée, par exemple, `Detail` avec un marqueur comme `&=Orders!A1` qui indique au processeur où commencer à insérer les lignes.

```java
import com.aspose.cells.*;

public class DynamicSheetNamesExample {

    public static void main(String[] args) throws Exception {
        // Load the template workbook that already contains Smart Markers.
        // Replace "templates/MasterDetailTemplate.xlsx" with the actual path.
        Workbook templateWorkbook = new Workbook("templates/MasterDetailTemplate.xlsx");
```

*Pourquoi cette étape est importante :* Le modèle définit la mise en page (en‑têtes, formules, formatage) qui sera copiée dans chaque feuille générée. Sans un modèle adéquat, la sortie perdrait le style et les formules.

## Étape 2 : Préparer la source de données pour créer des feuilles à partir des données

Ensuite, construisez une source de données que le processeur Smart Marker pourra parcourir. Dans cet exemple nous utilisons un `Map<String, Object>` où la clé `"Orders"` correspond au nom du marqueur dans le modèle.

```java
        // Prepare a data source with multiple detail rows.
        java.util.Map<String, Object> dataSource = new java.util.HashMap<>();

        // Each element of the Object[] array represents one row.
        dataSource.put("Orders", new Object[] {
            new Object[] { 101, "Alice", 250.00 },
            new Object[] { 102, "Bob",   175.50 },
            new Object[] { 103, "Carol", 320.75 }
        });
```

*Pourquoi cette étape est importante :* Le moteur Smart Marker lit le tableau, crée une ligne pour chaque `Object[]` interne, et—puisque nous lui demanderons de générer de nouvelles feuilles—crée une feuille de calcul distincte pour chaque ligne. C’est le cœur de **create sheets from data**.

## Étape 3 : Configurer SmartMarkerOptions pour générer plusieurs feuilles avec des noms uniques

Indiquez maintenant à Aspose.Cells comment nommer chaque nouvelle feuille. L’espace réservé `{0}` est remplacé par l’indice de la ligne courante.

```java
        // Configure options so every generated sheet gets a unique name.
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions();
        // {0} → row index (0‑based). Resulting names: Detail_0, Detail_1, …
        smartMarkerOptions.setDetailSheetNewName("Detail_{0}");
```

*Pourquoi cette étape est importante :* Sans définir `DetailSheetNewName`, le processeur réutiliserait le nom de la feuille d’origine pour chaque ligne, écrasant ainsi les données. Cette option rend possible les **noms de feuilles dynamiques**.

## Étape 4 : Traiter les SmartMarkers et générer le classeur

Exécutez le processeur avec la source de données et les options que nous venons de configurer.

```java
        // Execute the Smart Marker processor.
        templateWorkbook.getSmartMarkerProcessor().process(dataSource, smartMarkerOptions);
```

*Pourquoi cette étape est importante :* Le processeur développe les marqueurs, crée le nombre requis de feuilles, copie la mise en page du modèle, et remplit chaque feuille avec les données de la ligne correspondante.

## Étape 5 : Enregistrer et vérifier le résultat

Enfin, écrivez le classeur sur le disque. Ouvrez le fichier dans Excel pour voir les feuilles créées automatiquement.

```java
        // Save the workbook containing the newly generated sheets.
        templateWorkbook.save("output/MasterDetailResult.xlsx");
    }
}
```

**Résultat attendu**

Lorsque vous ouvrez `MasterDetailResult.xlsx`, vous devez voir trois nouvelles feuilles :

* `Detail_0` – contient la commande 101 (Alice, 250.00)  
* `Detail_1` – contient la commande 102 (Bob, 175.50)  
* `Detail_2` – contient la commande 103 (Carol, 320.75)

Chaque feuille conserve le formatage, les largeurs de colonnes et toutes les formules présentes dans la feuille modèle `Detail` d’origine.

## Exemple complet exécutable

Assembler toutes les sections donne un programme autonome que vous pouvez compiler et exécuter :

```java
import com.aspose.cells.*;

public class DynamicSheetNamesExample {

    public static void main(String[] args) throws Exception {
        // 1. Load the template workbook that contains Smart Markers.
        Workbook templateWorkbook = new Workbook("templates/MasterDetailTemplate.xlsx");

        // 2. Prepare the data source with multiple detail rows.
        java.util.Map<String, Object> dataSource = new java.util.HashMap<>();
        dataSource.put("Orders", new Object[] {
            new Object[] { 101, "Alice", 250.00 },
            new Object[] { 102, "Bob",   175.50 },
            new Object[] { 103, "Carol", 320.75 }
        });

        // 3. Configure SmartMarkerOptions to give each generated sheet a unique name.
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions();
        smartMarkerOptions.setDetailSheetNewName("Detail_{0}");

        // 4. Process the Smart Markers using the data source and the configured options.
        templateWorkbook.getSmartMarkerProcessor().process(dataSource, smartMarkerOptions);

        // 5. Save the resulting workbook with the newly created sheets.
        templateWorkbook.save("output/MasterDetailResult.xlsx");
    }
}
```

### Comment exécuter

1. Ajoutez le JAR Aspose.Cells for Java à votre classpath (disponible sur Maven Central ou le site Aspose).  
2. Placez `MasterDetailTemplate.xlsx` dans `templates/` relatif à la racine du projet.  
3. Exécutez la méthode `main`. Le dossier `output/` contiendra le fichier généré.

## Variantes courantes et cas limites

| Situation | Ce qu’il faut modifier |
|-----------|------------------------|
| **Modèle de nommage différent** | Utilisez `"OrderSheet_{0}_v{1}"` et incluez des espaces réservés supplémentaires comme `{1}` pour un second indice (par ex., un numéro de page). |
| **Ensembles de données volumineux** | Augmentez le tas JVM (`-Xmx2g`) pour éviter `OutOfMemoryError` lors de la génération de centaines de feuilles. |
| **Création conditionnelle de feuilles** | Avant d’appeler `process`, filtrez le tableau de données afin que les lignes ne remplissant pas un critère soient omises, évitant ainsi des feuilles inutiles. |
| **Conservation des formules référant d’autres feuilles** | Conservez le nom de la feuille d’origine comme espace réservé caché (par ex., `DetailTemplate`) et utilisez `SmartMarkerOptions.setDetailSheetNewName` uniquement pour le nom visible ; les formules qui font référence au nom caché seront toujours résolues correctement. |

## Conseils pour une automatisation Excel robuste

* **Valider la source de données** – Assurez‑vous que chaque tableau interne possède le même nombre d’éléments que les colonnes définies dans le modèle ; des longueurs incompatibles entraînent des erreurs d’exécution.  
* **Utiliser des plages nommées** dans le modèle pour une syntaxe Smart Marker plus claire (`&=Orders!A1`).  
* **Fermer les ressources** – Bien qu’Aspose.Cells gère les flux en interne, appeler explicitement `templateWorkbook.dispose()` dans un bloc `finally` peut libérer la mémoire native plus rapidement.  
* **Tester avec des valeurs limites** – Zéro ligne doit produire un classeur ne contenant que la feuille modèle d’origine ; une source de données vide vérifie que votre code gère correctement le cas « pas de données ».  

## Conclusion

Vous savez maintenant comment **générer des noms de feuilles dynamiques** dans Excel avec Java, comment **remplir un modèle Excel** et **créer des feuilles à partir de données**, ainsi que comment **générer plusieurs feuilles** automatiquement avec les Smart Markers d’Aspose.Cells. En suivant les étapes ci‑dessus, vous pouvez adapter le modèle à n’importe quel scénario de reporting — que vous ayez besoin de dizaines de feuilles détaillées, de conventions de nommage personnalisées ou de création conditionnelle de feuilles.

Prêt à étendre cette solution ? Essayez d’ajouter des graphiques à chaque feuille générée, ou exportez le classeur en PDF avec `Workbook.save("result.pdf", SaveFormat.PDF)`. Les deux techniques s’appuient sur la même base de feuilles dynamiques que vous venez de maîtriser. Bon codage !

## Que devez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser d’autres fonctionnalités de l’API et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Master Dynamic Excel Sheets in Java with Aspose.Cells: A Comprehensive Guide](/cells/english/java/formulas-functions/dynamic-excel-sheets-aspose-cells-java-guide/)
- [Dynamic Excel Sheets Aspose Cells Java Guide](/cells/german/java/formulas-functions/dynamic-excel-sheets-aspose-cells-java-guide/)
- [Dynamic Excel Sheets Aspose Cells Java Guide](/cells/french/java/formulas-functions/dynamic-excel-sheets-aspose-cells-java-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}