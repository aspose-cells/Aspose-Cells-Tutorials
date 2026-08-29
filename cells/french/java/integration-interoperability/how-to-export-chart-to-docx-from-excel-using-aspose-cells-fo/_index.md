---
category: general
date: 2026-08-20
description: Apprenez à exporter un graphique vers un docx et à convertir un classeur
  Excel en docx avec Aspose.Cells en Java. Guide étape par étape avec le code complet.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export chart to docx
- convert excel workbook to docx
- Aspose.Cells Java
- editable chart DOCX
- Excel to Word conversion
language: fr
lastmod: 2026-08-20
og_description: Exportez le graphique au format docx et convertissez le classeur Excel
  en docx en utilisant Aspose.Cells pour Java. Suivez ce tutoriel complet et exécutable.
og_image_alt: Screenshot showing a Java code editor exporting an Excel chart to a
  DOCX file
og_title: Exporter un graphique au format docx avec Aspose.Cells – Guide Java
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Learn how to export chart to docx and convert Excel workbook to docx
    with Aspose.Cells in Java. Step‑by‑step guide with complete code.
  headline: How to export chart to docx from Excel using Aspose.Cells for Java
  type: TechArticle
tags:
- Aspose.Cells
- Java
- DOCX
- Excel
title: Comment exporter un graphique vers un docx depuis Excel en utilisant Aspose.Cells
  pour Java
url: /fr/java/integration-interoperability/how-to-export-chart-to-docx-from-excel-using-aspose-cells-fo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exporter un graphique vers docx depuis un classeur Excel avec Java

Si vous devez **exporter un graphique vers docx** directement depuis un fichier Excel, ce tutoriel vous propose une solution prête à l’emploi. À la fin du guide, vous saurez également comment **convertir un classeur Excel en docx** tout en conservant un graphique éditable, de sorte que le document Word résultant puisse être modifié sans perte de fidélité.

L’exportation de graphiques est courante lorsque vous générez des rapports combinant des calculs de feuille de calcul avec des mises en page Word riches. Aspose.Cells for Java rend la conversion simple, et l’API vous permet de garder le graphique éditable — aucune image statique requise.

## Ce que couvre ce tutoriel

* Chargement d’un classeur existant contenant un graphique.  
* Configuration de `ImageOrPrintOptions` pour cibler le format DOCX.  
* Activation du drapeau `ExportEditableCharts` (disponible depuis la version 25.10).  
* Enregistrement du classeur en tant que fichier DOCX qui conserve un graphique éditable.  

Aucun outil externe n’est nécessaire au-delà du JAR Aspose.Cells. Le code fonctionne avec Java 8+ et toute version récente d’Aspose.Cells.

## Prérequis

| Exigence | Pourquoi c'est important |
|----------|---------------------------|
| **Aspose.Cells for Java** (v25.10 ou ultérieure) | La fonctionnalité `setExportEditableCharts` a été introduite dans cette version. |
| **Java Development Kit (JDK) 8 ou plus récent** | Fournit l’environnement d’exécution pour compiler et exécuter l’exemple. |
| **Un classeur Excel (`.xlsx`) contenant au moins un graphique** | Le graphique est l’objet qui sera exporté vers DOCX. |
| **Un IDE Java ou un outil de construction (par ex., Maven, Gradle)** | Simplifie la gestion des dépendances et l’exécution. |

Vous pouvez télécharger le dernier JAR Aspose.Cells depuis le [site Aspose](https://products.aspose.com/cells/java/).

## Étape 1 : Configurer le projet et ajouter la dépendance Aspose.Cells

Si vous utilisez Maven, ajoutez la dépendance suivante à votre `pom.xml` :

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.10</version> <!-- use the latest version -->
</dependency>
```

Pour Gradle, ajoutez :

```gradle
implementation 'com.aspose:aspose-cells:25.10'
```

> **Astuce :** Utilisez la version exacte qui a introduit `ExportEditableCharts` (25.10) ou toute version plus récente. Les versions antérieures ignoreront le drapeau et produiront une image statique à la place.

## Étape 2 : Charger le classeur qui contient le graphique

La classe `Workbook` représente le fichier Excel complet. Le charger ne nécessite qu’une ligne :

```java
import com.aspose.cells.*;

public class ExportEditableChartToDocx {
    public static void main(String[] args) throws Exception {
        // Load the workbook with the chart you want to export
        Workbook workbook = new Workbook("YOUR_DIRECTORY/ChartWorkbook.xlsx");
```

> **Pourquoi c’est important :** Le classeur doit être entièrement chargé avant de pouvoir appliquer des options d’exportation. Si le chemin du fichier est incorrect, Aspose.Cells lève une `FileNotFoundException`.

## Étape 3 : Configurer les options d’image/impression pour la sortie DOCX

`ImageOrPrintOptions` contrôle la façon dont le classeur est rendu. Définir le format d’enregistrement sur `DOCX` indique à Aspose.Cells de produire un document Word au lieu d’une image.

```java
        // Create options and specify DOCX as the target format
        ImageOrPrintOptions options = new ImageOrPrintOptions();
        options.setSaveFormat(SaveFormat.DOCX);
```

Vous pouvez également ajuster la taille de page, le DPI ou la qualité d’image ici, mais ces paramètres sont optionnels pour l’exportation de graphiques.

## Étape 4 : Activer l’exportation de graphiques éditables

À partir de la version 25.10, Aspose.Cells peut intégrer les graphiques en tant qu’objets graphiques natifs de Word. Cela les rend entièrement éditables dans Microsoft Word.

```java
        // Turn on the editable chart export flag
        options.setExportEditableCharts(true);
```

> **Cas limite :** Si vous définissez ce drapeau sur `false` (ou l’omettez), le graphique sera rendu comme une image statique. Utilisez `true` uniquement lorsque le public cible doit pouvoir modifier le graphique après la conversion.

## Étape 5 : Enregistrer le classeur en tant que fichier DOCX

Enfin, appelez `Workbook.save` avec les options configurées :

```java
        // Save the workbook as a DOCX document that contains an editable chart
        workbook.save("YOUR_DIRECTORY/ChartEditable.docx", options);
    }
}
```

Lorsque le programme se termine, ouvrez `ChartEditable.docx` dans Microsoft Word. Vous devriez voir le graphique d’origine, et si vous faites un clic droit dessus, l’option **Edit Data** sera disponible — confirmant que le graphique est réellement éditable.

## Exemple complet, exécutable

Voici le fichier source complet. Copiez‑le dans votre IDE, remplacez `YOUR_DIRECTORY` par un chemin absolu ou relatif, puis exécutez‑le.

```java
import com.aspose.cells.*;

public class ExportEditableChartToDocx {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the workbook that contains the chart
        Workbook workbook = new Workbook("YOUR_DIRECTORY/ChartWorkbook.xlsx");

        // Step 2: Create image/print options and set the target format to DOCX
        ImageOrPrintOptions options = new ImageOrPrintOptions();
        options.setSaveFormat(SaveFormat.DOCX);

        // Step 3: Enable exporting of editable charts (available from version 25.10)
        options.setExportEditableCharts(true);

        // Step 4: Save the workbook as a DOCX document with the configured options
        workbook.save("YOUR_DIRECTORY/ChartEditable.docx", options);
    }
}
```

**Résultat attendu**

* Un fichier nommé `ChartEditable.docx` dans le répertoire spécifié.  
* L’ouverture du fichier dans Word affiche le graphique exactement comme il apparaissait dans Excel, et vous pouvez double‑cliquer le graphique pour modifier ses séries de données.

## Problèmes courants et comment les éviter

| Symptom | Cause | Fix |
|---------|-------|-----|
| Word affiche une **image statique** au lieu d’un graphique éditable | `setExportEditableCharts` non appelé ou version < 25.10 | Assurez‑vous que le drapeau est réglé sur `true` et que vous utilisez Aspose.Cells 25.10 ou plus récent. |
| Le DOCX généré est **vide** | Chemin du classeur source incorrect ou permissions insuffisantes | Vérifiez le chemin du classeur et que l’application dispose des droits de lecture/écriture. |
| La mise en page du graphique apparaît **déformée** | Configuration de page dans Excel (ex. : lignes/colonnes masquées) différente des paramètres par défaut de Word | Ajustez `ImageOrPrintOptions` (ex. : `setOnePagePerSheet(true)`) pour contrôler le redimensionnement. |
| **Performance** dégradée sur de gros classeurs | Exportation de nombreux graphiques ou de grands ensembles de données | Exportez uniquement les feuilles nécessaires ou utilisez `setSheetIndex` pour limiter le traitement. |

## Extension de la solution

* **Plusieurs graphiques :** Parcourez toutes les feuilles de calcul et appelez `worksheet.getCharts()` pour exporter chaque graphique individuellement.  
* **Style DOCX personnalisé :** Après l’enregistrement, utilisez Aspose.Words pour appliquer des en‑têtes, pieds de page ou styles au document généré.  
* **Conversion par lots :** Enveloppez le code dans une boucle qui traite un répertoire de fichiers `.xlsx`, produisant un DOCX pour chacun.

## Conclusion

Vous disposez maintenant d’une méthode fiable pour **exporter un graphique vers docx** et **convertir un classeur Excel en docx** tout en conservant la pleine éditabilité du graphique. Les étapes clés sont le chargement du classeur, la configuration de `ImageOrPrintOptions` pour DOCX, l’activation de `ExportEditableCharts`, puis l’enregistrement du résultat.

Expérimentez avec des options supplémentaires — comme la définition des marges de page ou l’incorporation des formules du classeur — pour adapter la sortie à votre flux de travail de reporting. Lorsque vous devez générer des rapports Word à partir de données Excel de façon programmatique, cette approche offre une solution propre et maintenable.

--- 

*Prêt à l’essayer ? Clonez l’exemple, mettez à jour les chemins de fichiers, et lancez le programme. Si vous rencontrez des problèmes, consultez la documentation Aspose.Cells for Java ou explorez les sujets connexes ci‑dessous.*  

### Sujets liés que vous pourriez explorer ensuite

* **convert excel workbook to pdf** – générez des rapports PDF à partir du même classeur.  
* **Aspose.Cells chart formatting** – personnalisez les couleurs, marqueurs et axes avant l’exportation.  
* **Embedding images in DOCX with Aspose.Words** – combinez graphiques et autres contenus Word.  

Bonne programmation !

## Que devez‑vous apprendre ensuite ?


Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités API supplémentaires et à explorer des approches d’implémentation alternatives dans vos propres projets.

- [How to Create Excel Chart with Trendline and Export to Image using Aspose.Cells for Java](/cells/english/java/advanced-excel-charts/trendline-analysis/)
- [Automate Excel Chart Access Using Aspose.Cells Java: A Step-by-Step Guide](/cells/english/java/charts-graphs/excel-charts-access-aspose-cells-java/)
- [Customize Excel Chart Data Labels Using Aspose.Cells for Java: A Step-by-Step Guide](/cells/english/java/charts-graphs/customize-chart-data-labels-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}