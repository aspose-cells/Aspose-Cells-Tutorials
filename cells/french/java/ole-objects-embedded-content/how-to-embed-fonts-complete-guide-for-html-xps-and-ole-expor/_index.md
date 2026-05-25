---
category: general
date: 2026-03-01
description: Apprenez à intégrer des polices dans HTML et d’autres formats. Tutoriel
  étape par étape couvrant l’intégration de polices dans HTML, la conversion d’Excel
  en HTML, comment exporter OLE et la conversion d’Excel en XPS.
draft: false
keywords:
- how to embed fonts
- embed fonts in html
- convert excel to html
- how to export ole
- convert excel to xps
language: fr
og_description: Comment intégrer des polices dans les exportations HTML, XPS et OLE.
  Apprenez le flux complet, consultez du code Java exécutable et maîtrisez l’intégration
  de polices dans le HTML pour les conversions Excel.
og_title: Comment intégrer des polices – Tutoriel complet Java
tags:
- Aspose.Cells
- Java
- Document Export
title: Comment intégrer des polices – Guide complet pour l’exportation HTML, XPS et
  OLE
url: /fr/java/ole-objects-embedded-content/how-to-embed-fonts-complete-guide-for-html-xps-and-ole-expor/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment intégrer des polices – Guide complet pour HTML, XPS et export OLE

Vous vous êtes déjà demandé **comment intégrer des polices** lorsque vous transformez un classeur Excel en page web ou en document imprimable ? Vous n'êtes pas seul. De nombreux développeurs se heurtent à un mur lorsque le rendu est correct sur leur machine mais se casse ailleurs parce que les polices requises sont absentes.  

Dans ce tutoriel, nous parcourrons un scénario réel avec Aspose.Cells for Java : nous intégrerons des polices dans le HTML, préserverons les sélecteurs de variation d’emoji lors de la conversion en XPS, et garderons même un objet OLE éditable lors de l’exportation vers PPTX. À la fin, vous disposerez d’une solution prête à copier‑coller qui répond à la question « comment intégrer des polices » et aborde également **embed fonts in html**, **convert excel to html**, **how to export ole**, et **convert excel to xps**.

## Prérequis

- Java 17 (ou tout JDK récent)  
- Aspose.Cells for Java 25.x ou ultérieur  
- Un IDE de développement (IntelliJ IDEA, Eclipse ou VS Code)  
- Une connaissance de base des structures de données Excel  

Aucun service externe n’est requis — tout s’exécute localement.

## Vue d’ensemble de la solution

1. **Créer un classeur** et utiliser la fonction `WRAPCOLS` pour transformer une plage verticale en mise en page à trois colonnes.  
2. **Enregistrer le classeur au format XPS** tout en activant les sélecteurs de variation de police afin que les emoji restent intacts.  
3. **Exporter en HTML** avec des polices intégrées, garantissant que la page apparaît de la même façon partout.  
4. **Exporter un classeur contenant un objet OLE vers PPTX**, en préservant son éditabilité.  
5. **Appliquer un modèle Smart Marker** qui montre la liaison de données maître‑détail.  

Chaque étape est isolée dans sa propre section H2, ce qui rend le guide facile à parcourir tant pour les moteurs de recherche que pour les assistants IA.

![Illustration de comment intégrer des polices](image.png "comment intégrer des polices")

*Texte alternatif de l’image : diagramme montrant le flux de travail d’Excel vers HTML, XPS et PPTX.*

---

## Étape 1 – Créer un classeur et utiliser WRAPCOLS (Pourquoi cela importe pour embed fonts in html)

Avant de parler d’intégration de polices, nous avons besoin d’un classeur contenant réellement des données. La fonction `WRAPCOLS` est un moyen pratique de diviser une seule colonne en plusieurs colonnes, ce qui rend souvent le HTML final plus lisible.

```java
import com.aspose.cells.*;

public class EmbedFontsDemo {
    public static void main(String[] args) throws Exception {
        // Initialize a new workbook
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.getWorksheets().get(0);

        // Populate A2:A10 with sample data
        for (int i = 2; i <= 10; i++) {
            sheet.getCells().get("A" + i).putValue("Item " + (i - 1));
        }

        // Use WRAPCOLS to create a 3‑column block starting at A1
        Cell resultCell = sheet.getCells().get("A1");
        resultCell.setFormula("=WRAPCOLS(A2:A10,3)");
        workbook.calculateFormula();

        System.out.println("WRAPCOLS result: " + resultCell.getStringValue());
        // -----------------------------------------------------------------
        // The rest of the steps are demonstrated after this point.
        // -----------------------------------------------------------------
```

**Pourquoi cette étape ?**  
L’appel `WRAPCOLS` génère une plage multi‑colonnes qui apparaît plus tard dans le HTML sous forme de tableau. Lorsque nous **intégrerons des polices dans le HTML**, le style du tableau dépendra des polices que nous intégrons, assurant un rendu cohérent sur tous les navigateurs.

---

## Étape 2 – Enregistrer le classeur au format XPS tout en préservant les emoji (convert excel to xps)

Si vous avez besoin d’un format prêt à l’impression, le XPS est un bon choix. Cependant, les documents modernes contiennent souvent des emoji ou des symboles qui utilisent des sélecteurs de variation. Activer `EnableFontVariationSelectors` garantit que ces caractères survivent à la conversion.

```java
        // --------------------------------------------------------------
        // Step 2: Save as XPS with font variation selectors enabled
        // --------------------------------------------------------------
        WorkbookSettings settings = workbook.getSettings();
        settings.setEnableFontVariationSelectors(true); // crucial for emoji

        String xpsPath = "output/withVariations.xps";
        workbook.save(xpsPath, SaveFormat.XPS);
        System.out.println("Workbook saved as XPS at: " + xpsPath);
```

**Ce que vous obtenez :**  
Un fichier XPS qui affiche tous les emoji intégrés exactement comme dans le classeur source. Cela satisfait le besoin **convert excel to xps** et montre que la gestion des polices ne se limite pas au HTML.

---

## Étape 3 – Exporter en HTML avec des polices intégrées (how to embed fonts & embed fonts in html)

Nous arrivons maintenant au cœur du tutoriel : **comment intégrer des polices** lors de la conversion d’Excel en HTML. Aspose.Cells permet d’intégrer les polices directement dans le fichier HTML généré, éliminant le besoin de fichiers de police externes.

```java
        // --------------------------------------------------------------
        // Step 3: Export to HTML with embedded fonts
        // --------------------------------------------------------------
        HtmlSaveOptions htmlOptions = new HtmlSaveOptions();
        htmlOptions.setEmbedFonts(true); // this is the key line for embed fonts in html
        htmlOptions.setExportImagesAsBase64(true); // optional, keeps all assets in one file

        String htmlPath = "output/embeddedFonts.html";
        workbook.save(htmlPath, htmlOptions);
        System.out.println("HTML with embedded fonts saved at: " + htmlPath);
```

**Comment cela fonctionne :**  
`setEmbedFonts(true)` indique au rendu de lire les fichiers de police utilisés dans le classeur et de les intégrer sous forme de règles `@font-face` encodées en Base64 à l’intérieur de la balise `<style>`. Le HTML résultant est autonome, vous pouvez le déposer sur n’importe quel serveur et les polices s’afficheront correctement — exactement ce que recherchent les développeurs lorsqu’ils tapent **how to embed fonts**.

**Extrait de sortie attendu (dans `embeddedFonts.html`) :**

```html
<style>
@font-face{font-family:"Arial";src:url(data:font/ttf;base64,AAEAAA... ) format('truetype');}
</style>
<table>
  <tr><td>Item 1</td><td>Item 4</td><td>Item 7</td></tr>
  <tr><td>Item 2</td><td>Item 5</td><td>Item 8</td></tr>
  <tr><td>Item 3</td><td>Item 6</td><td>Item 9</td></tr>
</table>
```

Remarquez la règle `@font-face — c’est la réponse concrète à **embed fonts in html**.

---

## Étape 4 – Exporter un classeur contenant un objet OLE vers PPTX (how to export ole)

De nombreux rapports d’entreprise intègrent des documents Word, PDF ou d’autres feuilles Excel comme objets OLE. Lors de l’exportation d’un tel classeur vers PowerPoint, on perd souvent la possibilité d’éditer cet objet. Aspose.Cells préserve l’éditabilité dès le départ.

```java
        // --------------------------------------------------------------
        // Step 4: Export a workbook with an OLE object to PPTX
        // --------------------------------------------------------------
        // Load a workbook that already contains an OLE object.
        Workbook oleWorkbook = new Workbook("input/oleObject.xlsx");

        String pptxPath = "output/oleEditable.pptx";
        oleWorkbook.save(pptxPath, SaveFormat.PPTX);
        System.out.println("PPTX with editable OLE object saved at: " + pptxPath);
```

**Pourquoi c’est important :**  
Si vous cherchez **how to export ole**, cet extrait montre l’appel d’API exact. La diapositive PowerPoint résultante contient l’objet OLE comme un composant vivant, double‑clic‑pour‑éditer — sans post‑traitement supplémentaire.

---

## Étape 5 – Appliquer un modèle Smart Marker (master‑detail) et terminer la démo

Les Smart Markers vous permettent de lier une source de données (Map, JSON, DataTable) directement à un modèle Excel. Voici un exemple minimal qui imprime des lignes maître‑détail.

```java
        // --------------------------------------------------------------
        // Step 5: Apply Smart Marker template (master‑detail)
        // --------------------------------------------------------------
        String smartMarkerTemplate = "${Orders.Master:OrderID,Customer}\n${Orders.Detail:Product,Qty,Price}";
        // Simulated data source
        java.util.Map<String, Object> dataSource = new java.util.HashMap<>();
        java.util.List<java.util.Map<String, Object>> master = new java.util.ArrayList<>();
        java.util.Map<String, Object> masterRow = new java.util.HashMap<>();
        masterRow.put("OrderID", 1001);
        masterRow.put("Customer", "Acme Corp");
        master.add(masterRow);
        dataSource.put("Orders.Master", master);

        java.util.List<java.util.Map<String, Object>> detail = new java.util.ArrayList<>();
        java.util.Map<String, Object> detailRow = new java.util.HashMap<>();
        detailRow.put("Product", "Widget");
        detailRow.put("Qty", 5);
        detailRow.put("Price", 9.99);
        detail.add(detailRow);
        dataSource.put("Orders.Detail", detail);

        SmartMarkerProcessor processor = new SmartMarkerProcessor(new Workbook());
        processor.apply(smartMarkerTemplate, dataSource);
        processor.getWorkbook().save("output/smartMarkerResult.xlsx");
        System.out.println("Smart Marker workbook saved.");
    }
}
```

**Ce que vous voyez :**  
Un nouveau classeur (`smartMarkerResult.xlsx`) où les espaces réservés du modèle sont remplacés par les données. Cette étape n’est pas directement liée aux polices, mais elle complète le tutoriel en montrant un flux de travail de reporting typique qui précède souvent un export **embed fonts in html**.

---

## Pièges courants & Astuces pro (Assurer une intégration réussie des polices)

| Problème | Pourquoi cela se produit | Solution |
|----------|--------------------------|----------|
| Les polices sont absentes dans le fichier HTML | Le classeur utilise une police système qui n’est pas installée sur le serveur. | Utilisez `Workbook.getSettings().setDefaultFont("Arial")` avant de charger les données, ou intégrez manuellement les fichiers de police requis. |
| Le HTML de sortie est volumineux | L’intégration de nombreuses polices lourdes gonfle la taille du fichier. | Limitez l’intégration aux seules polices réellement utilisées : `htmlOptions.setFontEmbeddingMode(HtmlFontEmbeddingMode.EmbedSubset)`. |
| Les emoji disparaissent après la conversion XPS | Les sélecteurs de variation sont supprimés par défaut. | Activez `settings.setEnableFontVariationSelectors(true)` comme montré à l’Étape 2. |
| L’objet OLE devient une image statique dans le PPTX | Le classeur source a été enregistré avec `setSuppressOLEObjects(true)`. | Assurez‑vous de **ne pas** supprimer les objets OLE lors de l’enregistrement en PPTX. |

---

## Vérification des résultats

1. Ouvrez `embeddedFonts.html` dans Chrome/Firefox. Le tableau doit s’afficher avec la police intégrée (par ex., Arial) même si cette police n’est pas installée sur la machine.  
2. Ouvrez `withVariations.xps` dans le Visionneur XPS de Windows. Les emoji tels que 👍 doivent se rendre correctement.  
3. Ouvrez `oleEditable.pptx` dans PowerPoint. Double‑cliquez la forme OLE ;

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}