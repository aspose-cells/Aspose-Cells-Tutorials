---
category: general
date: 2026-06-27
description: Intégrez les polices dans le HTML lors de la conversion d’Excel en HTML.
  Apprenez comment enregistrer le classeur au format HTML avec les polices intégrées
  en utilisant du code Java simple.
draft: false
keywords:
- embed fonts in html
- convert excel to html
- save workbook as html
- Java Excel to HTML conversion
- Aspose.Cells HTML export
language: fr
og_description: Intégrez les polices dans le HTML lors de la conversion d’Excel en
  HTML. Ce guide montre comment enregistrer le classeur au format HTML avec les polices
  intégrées à l’aide de Java.
og_title: Intégrer des polices dans HTML – Convertir Excel en HTML et enregistrer
  le classeur
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Embed fonts in HTML when you convert Excel to HTML. Learn how to save
    workbook as HTML with embedded fonts using simple Java code.
  headline: Embed Fonts in HTML – Convert Excel to HTML & Save Workbook
  type: TechArticle
- description: Embed fonts in HTML when you convert Excel to HTML. Learn how to save
    workbook as HTML with embedded fonts using simple Java code.
  name: Embed Fonts in HTML – Convert Excel to HTML & Save Workbook
  steps:
  - name: Right‑click the page → “View Page Source”.
    text: Right‑click the page → “View Page Source”.
  - name: 'Search for `@font-face`. You’ll find a CSS rule that contains a `src: url(data:font/ttf;base64,…)`
      line—this is the Base64‑encoded font data.'
    text: 'Search for `@font-face`. You’ll find a CSS rule that contains a `src: url(data:font/ttf;base64,…)`
      line—this is the Base64‑encoded font data.'
  - name: Load or create the workbook.
    text: Load or create the workbook.
  - name: Create `HtmlSaveOptions` and enable `setEmbedFonts(true)`.
    text: Create `HtmlSaveOptions` and enable `setEmbedFonts(true)`.
  - name: Call `Workbook.save` with those options.
    text: Call `Workbook.save` with those options.
  type: HowTo
tags:
- Java
- Aspose.Cells
- HTML
- Excel
title: Intégrer des polices dans HTML – Convertir Excel en HTML et enregistrer le
  classeur
url: /fr/java/excel-import-export/embed-fonts-in-html-convert-excel-to-html-save-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Intégrer des polices dans HTML – Convertir Excel en HTML & Enregistrer le classeur

Vous avez déjà eu besoin d'**intégrer des polices dans HTML** lorsque vous *convertissez Excel en HTML* ? Peut‑être construisez‑vous un portail de reporting et les polices web par défaut ne sont pas suffisantes. La bonne nouvelle, c’est que vous n’avez pas à vous contenter d’un rendu fade et générique—Aspose.Cells vous permet d’inclure les polices exactes que vous avez utilisées dans la feuille de calcul directement dans le fichier HTML généré.

Dans ce tutoriel, nous parcourrons un exemple complet, prêt à l’exécution en Java, qui **enregistre le classeur au format HTML** avec les polices intégrées, explique pourquoi vous pourriez vouloir le faire, et signale quelques pièges éventuels. À la fin, vous disposerez d’une page HTML autonome qui ressemble exactement à la feuille Excel d’origine, sans glyphes manquants, sans problèmes de CSS externe.

## Ce que vous allez apprendre

- Comment charger un classeur Excel existant (ou en créer un à partir de zéro) en Java.  
- Comment configurer `HtmlSaveOptions` pour intégrer les polices du classeur directement dans la sortie HTML.  
- Comment invoquer `Workbook.save` afin que le fichier soit écrit en **HTML avec polices intégrées**.  
- Astuces pour gérer les gros fichiers de polices, les répertoires de polices personnalisées, et le dépannage des problèmes courants.

> **Prérequis :** Vous avez besoin d’Aspose.Cells for Java (dernière version) dans votre classpath et d’un runtime Java 8+. Aucune autre bibliothèque tierce n’est requise.

---

## Étape 1 : Configurer le projet et importer les classes requises

Avant de plonger dans le code, assurons‑nous que l’environnement de développement est prêt. Si vous utilisez Maven, ajoutez la dépendance Aspose.Cells à votre `pom.xml` :

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- Use the newest version available -->
</dependency>
```

Si vous préférez Gradle, l’équivalent est :

```gradle
implementation 'com.aspose:aspose-cells:23.12'
```

> **Astuce :** Gardez la bibliothèque à jour. Les nouvelles versions améliorent souvent la gestion des polices et réduisent la taille des données intégrées.

Importons maintenant les classes dont nous aurons besoin :

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.HtmlSaveOptions;
import com.aspose.cells.SaveFormat;
import java.io.File;
```

Ces imports nous donnent accès au modèle de classeur, aux options d’exportation HTML, et à quelques classes utilitaires.

---

## Étape 2 : Charger (ou créer) le classeur Excel

Vous pouvez soit charger un fichier `.xlsx` existant, soit créer un classeur à la volée. À titre d’exemple, supposons que nous disposons d’un fichier nommé `Sample.xlsx` dans le dossier `resources` du projet.

```java
// Load an existing workbook
String inputPath = "resources/Sample.xlsx";
Workbook wb = new Workbook(inputPath);
```

Si vous n’avez pas de fichier source, vous pouvez générer rapidement un classeur :

```java
// Create a workbook from scratch (optional)
Workbook wb = new Workbook();               // creates a new empty workbook
wb.getWorksheets().get(0).getCells().putValue("A1", "Hello, world!");
```

> **Pourquoi c’est important :** Lorsque vous intégrez des polices, Aspose.Cells extrait les définitions exactes des polices utilisées dans le classeur. Si le classeur contient des polices personnalisées, elles seront transportées avec le HTML, garantissant une fidélité visuelle.

---

## Étape 3 : Configurer HtmlSaveOptions pour intégrer les polices

C’est le cœur du tutoriel. Par défaut, `HtmlSaveOptions` génère du CSS qui référence les polices système. Pour changer ce comportement, nous activons le drapeau `setEmbedFonts(true)`.

```java
// Step 1: Create HTML save options
HtmlSaveOptions htmlOpts = new HtmlSaveOptions(SaveFormat.HTML);

// Step 2: Enable embedding of fonts in the HTML output
htmlOpts.setEmbedFonts(true);

// (Optional) Reduce the size of embedded fonts by subsetting only used glyphs
htmlOpts.setSubsetFonts(true);
```

### Ce que font les options

| Option | Valeur par défaut | Effet lorsqu’elle est modifiée |
|--------|-------------------|--------------------------------|
| `setEmbedFonts(true)` | `false` | Intègre les fichiers de police complets (généralement sous forme d’URIs de données Base64) dans le HTML généré. |
| `setSubsetFonts(true)` | `false` | Restreint la police intégrée aux seuls caractères réellement utilisés, réduisant considérablement la taille du fichier. |
| `setFontEmbeddingMode(HtmlSaveOptions.FontEmbeddingMode.EMBED_ALL)` | `EMBED_ALL` | Vous pouvez choisir d’intégrer uniquement des polices spécifiques si vous avez des contraintes de licence. |

> **Cas particulier :** Si le classeur utilise une police qui n’est pas installée sur le serveur, Aspose.Cells revient à une police système par défaut. Pour éviter les surprises, assurez‑vous que toutes les polices personnalisées sont disponibles dans le répertoire de polices du runtime Java ou enregistrez‑les manuellement via `FontConfig`.

---

## Étape 4 : Enregistrer le classeur en HTML avec les polices intégrées

Une fois les options configurées, il suffit d’appeler `save`. Le résultat sera un seul fichier `.html` contenant les données du classeur **et** les fichiers de police encodés directement dans le balisage.

```java
// Step 3: Save the workbook as an HTML file with embedded fonts
String outputDir = "output";
new File(outputDir).mkdirs(); // Ensure the folder exists

String outputPath = outputDir + File.separator + "page.html";
wb.save(outputPath, htmlOpts);

System.out.println("HTML file with embedded fonts created at: " + outputPath);
```

Lorsque vous ouvrez `page.html` dans n’importe quel navigateur moderne, la page s’affiche avec exactement la même typographie que dans Excel—pas de fichiers de police externes, pas de caractères manquants.

---

## Étape 5 : Vérifier le résultat et comprendre la sortie

Ouvrez le fichier HTML généré dans un navigateur (Chrome, Firefox, Edge—celui qui vous convient). Vous devriez voir la feuille rendue fidèlement. Pour vérifier que les polices sont réellement intégrées :

1. Faites un clic droit sur la page → « View Page Source ».  
2. Recherchez `@font-face`. Vous trouverez une règle CSS contenant une ligne `src: url(data:font/ttf;base64,…)`—c’est la police encodée en Base64.  

Si vous voyez cela, l’étape **intégrer des polices dans HTML** a réussi.

### Questions fréquentes

- **« Pourquoi le fichier HTML est‑il plus volumineux que prévu ? »**  
  L’intégration de polices complètes peut ajouter plusieurs centaines de kilo‑octets. Utilisez `setSubsetFonts(true)` pour le réduire, ou envisagez de convertir uniquement les feuilles nécessaires.

- **« Puis‑je intégrer uniquement une police spécifique ? »**  
  Oui. Appelez `htmlOpts.setFontEmbeddingMode(HtmlSaveOptions.FontEmbeddingMode.EMBED_SPECIFIED)` puis spécifiez les noms de police via `htmlOpts.getSpecifiedFontNames().add("MyCustomFont")`.

- **« Et si la police est sous licence et que je ne peux pas l’intégrer ? »**  
  Désactivez le drapeau (`setEmbedFonts(false)`) et fournissez une alternative web‑safe via CSS, ou hébergez la police sur un CDN où vous avez les droits.

---

## Étape 6 : Gestion des classeurs volumineux et conseils de performance

L’intégration des polices fonctionne bien pour des feuilles modestes, mais un classeur contenant des dizaines de polices personnalisées peut gonfler la taille du HTML. Voici quelques recommandations orientées performance :

- **Sous‑ensemble de polices** (déjà montré) pour ne garder que les glyphes utilisés.  
- **Exporter uniquement les feuilles nécessaires** avec `htmlOpts.setExportActiveWorksheetOnly(true)`.  
- **Compresser le HTML** après génération (par ex., gzip côté serveur) pour réduire la latence réseau.  
- **Mettre en cache le HTML généré** si le même fichier Excel est demandé fréquemment.

---

## Étape 7 : Prochaines étapes – Aller au‑delà de l’exportation de base

Maintenant que vous avez maîtrisé **l’intégration des polices dans HTML**, vous pouvez explorer des fonctionnalités connexes :

- **Convertir Excel en HTML avec images** (`htmlOpts.setExportImagesAsBase64(true)`).  
- **Générer un PDF à la place du HTML** (`wb.save("output.pdf", SaveFormat.PDF)`).  
- **Créer du HTML réactif** en ajustant `htmlOpts.setExportActiveWorksheetOnly` et `htmlOpts.setExportGridLines`.  

Toutes ces fonctionnalités suivent le même schéma : configurer un objet `*SaveOptions`, activer les drapeaux appropriés, puis appeler `Workbook.save`.

---

## Conclusion

Vous venez d’apprendre comment **intégrer des polices dans HTML** tout en **convertissant Excel en HTML** et **en enregistrant le classeur au format HTML** avec Aspose.Cells for Java. Les étapes clés sont :

1. Charger ou créer le classeur.  
2. Créer `HtmlSaveOptions` et activer `setEmbedFonts(true)`.  
3. Appeler `Workbook.save` avec ces options.

Le résultat est un fichier HTML unique et portable qui ressemble exactement à votre feuille de calcul d’origine—pas de polices manquantes, pas de fichiers CSS supplémentaires, et aucune dépendance aux polices installées chez le client.

N’hésitez pas à expérimenter le sous‑ensemble de polices, l’intégration sélective, ou même à combiner cela avec une mise en cache côté serveur pour des scénarios à fort trafic. Si vous rencontrez des anomalies (fichiers trop gros, glyphes manquants), revenez sur les paramètres optionnels présentés et ajustez‑les en conséquence.

Bon codage, et profitez du rendu HTML pixel‑perfect que vous pouvez désormais servir directement depuis vos applications Java !

## Ce que vous devriez apprendre ensuite

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser d’autres fonctionnalités de l’API et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Convert Excel to HTML in Java Using Aspose.Cells: A Step‑By‑Step Guide](/cells/english/java/workbook-operations/convert-excel-html-aspose-cells-java/)
- [Export Excel to HTML Using Aspose.Cells for Java: A Complete Guide](/cells/english/java/workbook-operations/export-excel-to-html-aspose-cells-java/)
- [Export Excel to HTML using IStreamProvider & Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/workbook-operations/export-excel-html-streamprovider-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}