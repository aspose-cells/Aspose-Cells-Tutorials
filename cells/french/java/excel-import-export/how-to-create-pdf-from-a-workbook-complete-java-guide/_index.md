---
category: general
date: 2026-03-01
description: Comment créer un PDF et enregistrer le classeur au format PDF, exporter
  Excel en HTML, et utiliser la fonction d’extension avec Aspose.Cells pour Java.
  Code étape par étape inclus.
draft: false
keywords:
- how to create pdf
- save workbook as pdf
- export excel to html
- use expand function
language: fr
og_description: Comment créer un PDF à partir d’un classeur avec Aspose.Cells pour
  Java. Apprenez à enregistrer le classeur au format PDF, à exporter Excel en HTML
  et à utiliser la fonction EXPAND.
og_title: Comment créer un PDF à partir d'un classeur – Tutoriel Java
tags:
- Aspose.Cells
- Java
- PDF generation
title: Comment créer un PDF à partir d’un classeur – Guide complet Java
url: /fr/java/excel-import-export/how-to-create-pdf-from-a-workbook-complete-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment créer un PDF à partir d'un classeur – Guide complet Java

Vous vous êtes déjà demandé **comment créer un PDF** directement à partir d'un classeur Excel sans jongler avec des convertisseurs tiers ? Vous n'êtes pas seul. De nombreux développeurs se heurtent à un mur lorsqu'ils ont besoin d'une exportation PDF rapide, d'un aperçu HTML ou de formules de tableau dynamiques—le tout en une seule fois.  

Dans ce tutoriel, nous parcourrons un programme Java autonome qui fait exactement cela. Nous **enregistrerons le classeur au format PDF**, vous montrerons comment **exporter Excel en HTML** tout en conservant les lignes figées, et démontrerons **l'utilisation de la fonction EXPAND** dans une feuille de calcul. À la fin, vous disposerez d'un projet exécutable que vous pourrez intégrer à n'importe quel build Maven ou Gradle.

> **Astuce :** Tout le code ci‑dessus fonctionne avec Aspose.Cells 23.10 (ou plus récent). Si vous utilisez une version antérieure, certains noms de méthodes peuvent différer légèrement.

---

## Prérequis

- **Java 17** (ou toute version LTS) installé et configuré.  
- **Aspose.Cells for Java** library. Ajoutez la dépendance Maven suivante à votre `pom.xml` :

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

- Un IDE ou éditeur de texte de votre choix (IntelliJ IDEA, VS Code, Eclipse…).

Pas d'API externes, pas de services web—juste du Java pur et le SDK Aspose.Cells.

---

## Vue d'ensemble de la solution

Nous diviserons l'implémentation en **sept étapes logiques** :

1. Créer un classeur et démontrer la fonction **EXPAND**.  
2. Activer les sélecteurs de variation de police et **enregistrer le classeur au format PDF**.  
3. Exporter le même classeur en HTML tout en préservant les lignes figées.  
4. Utiliser un Smart Marker avec un paramètre `IF` pour injecter du texte conditionnel.  
5. Appliquer un Smart Marker maître‑détail pour des données hiérarchiques.  
6. Charger un fichier Markdown contenant des images encodées en Base‑64.  
7. Configurer les options GridJs pour l'alignement et les bordures, puis insérer les données.

Chaque étape est encapsulée dans sa propre méthode afin de garder la méthode `main` claire et d'illustrer **pourquoi** nous faisons ce que nous faisons, pas seulement **quoi** nous tapons.

---

## Étape 1 – Créer un classeur et utiliser la fonction EXPAND

La fonction **EXPAND** est une nouvelle formule de tableau dynamique introduite dans Office 365. Elle vous permet de déverser une plage dans une zone plus grande sans copier manuellement les cellules.

```java
import com.aspose.cells.*;

public class WorkbookDemo {

    private static void createWorkbookWithExpand() throws Exception {
        // Initialize a new workbook and grab the first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.getWorksheets().get(0);

        // A1 uses EXPAND to turn a 1×3 array into a 5×2 block
        sheet.getCells().get("A1").setFormula("=EXPAND({1,2,3}, 5, 2)");

        // B1 demonstrates a classic trigonometric function (cotangent)
        sheet.getCells().get("B1").setFormula("=COT(PI()/4)");

        // Force calculation so we can read the results immediately
        workbook.calculateFormula();

        // Print the top‑left value to the console – should be 1
        System.out.println("A1 value after EXPAND: " + sheet.getCells().get("A1").getStringValue());
    }
```

**Pourquoi c’est important :**  
- `EXPAND` remplit automatiquement le résultat avec des cellules vides, ce qui est parfait lorsque vous **enregistrez le classeur au format PDF** plus tard—le PDF affichera un tableau propre et rectangulaire.  
- Appeler `calculateFormula()` garantit que le moteur de formules s'exécute avant que nous n'exportions quoi que ce soit.

---

## Étape 2 – Activer les sélecteurs de variation de police et **enregistrer le classeur au format PDF**

Si vous devez prendre en charge une typographie avancée (par ex., les emojis ou les sélecteurs de variation CJK), vous devez activer la fonctionnalité **avant** l’enregistrement.

```java
    private static void saveAsPdf(Workbook workbook) throws Exception {
        // Enable support for variation selectors (useful for emojis, etc.)
        WorkbookSettings settings = workbook.getSettings();
        settings.setEnableFontVariationSelectors(true);

        // Define the output path – adjust to your environment
        String pdfPath = "output/vsPdf.pdf";

        // Save the workbook as a PDF file
        workbook.save(pdfPath, SaveFormat.PDF);
        System.out.println("PDF saved to: " + pdfPath);
    }
```

**Point clé :** le mot‑clé principal **how to create pdf** trouve sa réponse ici—en appelant `workbook.save(..., SaveFormat.PDF)` après avoir configuré les paramètres.

---

## Étape 3 – **Exporter Excel en HTML** tout en conservant les lignes figées

Souvent, les parties prenantes demandent un aperçu web rapide. Aspose.Cells peut exporter en HTML, et avec `setPreserveFrozenRows(true)` nous conservons la même expérience de défilement qu’Excel.

```java
    private static void exportToHtml(Workbook workbook) throws Exception {
        HtmlSaveOptions htmlOptions = new HtmlSaveOptions();
        htmlOptions.setPreserveFrozenRows(true); // keep frozen panes

        String htmlPath = "output/frozenRows.html";
        workbook.save(htmlPath, htmlOptions);
        System.out.println("HTML exported to: " + htmlPath);
    }
```

**Pourquoi cela vous importe :** les lignes figées sont un atout d’utilisabilité ; sans elles, les lignes d’en‑tête disparaissent lorsque les utilisateurs font défiler la page.

---

## Étape 4 – Smart Marker avec un paramètre IF

Les Smart Markers vous permettent de fusionner des données dans un modèle sans écrire de boucles. Le paramètre `if` ajoute une logique conditionnelle directement dans le marqueur.

```java
    private static void applyConditionalSmartMarker() throws Exception {
        String template = "${if(@IsVIP, 'VIP Customer', 'Regular Customer')}: ${CustomerName}";
        Map<String, Object> data = new HashMap<>();
        data.put("IsVIP", true);
        data.put("CustomerName", "Acme Corp");

        // Create a fresh workbook to host the result
        Workbook markerWorkbook = new Workbook();
        SmartMarkerProcessor processor = new SmartMarkerProcessor(markerWorkbook);
        processor.apply(template, data);

        // Save to see the result
        markerWorkbook.save("output/conditionalMarker.pdf", SaveFormat.PDF);
    }
```

Le PDF généré affichera **« VIP Customer : Acme Corp »** parce que `IsVIP` vaut `true`. Changez le drapeau à `false` et vous obtiendrez **« Regular Customer : Acme Corp »**—aucun code supplémentaire nécessaire.

---

## Étape 5 – Smart Marker maître‑détail utilisant une plage hiérarchique

Lorsque vous avez des données parent‑enfant (par ex., des commandes et leurs lignes), un marqueur maître‑détail vous évite d’insérer manuellement des lignes.

```java
    private static void applyMasterDetailSmartMarker() throws Exception {
        // Simulated hierarchical data
        Map<String, Object> hierarchicalData = new HashMap<>();
        List<Map<String, Object>> orders = new ArrayList<>();

        Map<String, Object> order1 = new HashMap<>();
        order1.put("OrderID", 1001);
        order1.put("Date", "2024‑12‑01");
        List<Map<String, Object>> details1 = new ArrayList<>();
        details1.add(Map.of("Product", "Widget A", "Qty", 5));
        details1.add(Map.of("Product", "Widget B", "Qty", 2));
        order1.put("Detail", details1);
        orders.add(order1);

        hierarchicalData.put("Orders", orders);

        String masterDetailTemplate =
                "${Orders.Master:OrderID,Date}\n" +
                "${Orders.Detail:Product,Qty}";

        Workbook mdWorkbook = new Workbook();
        SmartMarkerProcessor mdProcessor = new SmartMarkerProcessor(mdWorkbook);
        mdProcessor.apply(masterDetailTemplate, hierarchicalData);

        mdWorkbook.save("output/masterDetail.pdf", SaveFormat.PDF);
    }
```

**Ce que vous gagnez :** le moteur développe les lignes maîtres pour chaque commande et imbrique automatiquement les lignes de détail en dessous—idéal pour les factures ou les rapports d’achats.

---

## Étape 6 – Charger un document Markdown avec des images encodées en Base‑64

Si vos données sources sont en Markdown (courant dans les pipelines de documentation), Aspose.Cells peut les rendre directement dans un classeur.

```java
    private static void loadMarkdownWithBase64() throws Exception {
        MarkdownLoadOptions mdOptions = new MarkdownLoadOptions();
        mdOptions.setEnableBase64Images(true); // decode inline images

        // Assume doc.md lives in the project root
        Workbook mdWorkbook = new Workbook("input/doc.md", mdOptions);
        mdWorkbook.save("output/markdownExport.pdf", SaveFormat.PDF);
        System.out.println("Markdown loaded and saved as PDF.");
    }
```

**Note de cas limite :** si la chaîne Base‑64 est malformée, Aspose ignorera l’image mais continuera à traiter le reste du document—pas de plantage.

---

## Étape 7 – Configurer les options GridJs et insérer des données

GridJs est une grille JavaScript légère qu’Aspose peut rendre en HTML. Aligner les nombres et appliquer des bordures améliore la lisibilité.

```java
    private static void configureGridJs() throws Exception {
        GridJsOptions gridOptions = new GridJsOptions();
        gridOptions.setNumberFormatAlignment(Alignment.Center); // center numbers
        gridOptions.setNumberFormatBorder(BorderLineStyle.Thin); // thin border

        GridJsEngine gridEngine = new GridJsEngine(gridOptions);
        gridEngine.insertRows(0, 10); // create 10 empty rows
        gridEngine.setCellValue(0, 0, "123"); // first cell gets a value

        // Export the GridJs view to HTML for quick inspection
        String htmlPath = "output/gridJs.html";
        gridEngine.save(htmlPath);
        System.out.println("GridJs HTML saved to: " + htmlPath);
    }
```

**Pourquoi cela compte :** un alignement correct et des bordures donnent à l’HTML généré l’aspect d’une feuille de calcul soignée—utile pour les tableaux de bord.

---

## Rassembler le tout – La méthode `main`

```java
    public static void main(String[] args) {
        try {
            // Step 1 – create workbook with EXPAND
            Workbook workbook = new Workbook();
            Worksheet sheet = workbook.getWorksheets().get(0);
            sheet.getCells().get("A1").setFormula("=EXPAND({1,2,3}, 5, 2)");
            sheet.getCells().get("B1").setFormula("=COT(PI()/4)");
            workbook.calculateFormula();
            System.out.println("A1 after EXPAND: " + sheet.getCells().get("A1").getStringValue());

            // Step 2 – save as PDF
            saveAsPdf(workbook);

            // Step 3 – export to HTML
            exportToHtml(workbook);

            // Step 4 – conditional Smart Marker
            applyConditionalSmartMarker();

            // Step 5 – master‑detail Smart Marker
            applyMasterDetailSmartMarker();

            // Step 6 – load Markdown with Base‑64 images
            loadMarkdownWithBase64();

            // Step 7 – GridJs configuration
            configureGridJs();

            System.out.println("All tasks completed successfully.");
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}