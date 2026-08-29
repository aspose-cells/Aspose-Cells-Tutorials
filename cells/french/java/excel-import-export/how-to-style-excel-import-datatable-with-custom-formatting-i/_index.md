---
category: general
date: 2026-07-03
description: Comment styliser les fichiers Excel avec Java. Apprenez à formater la
  colonne de date dans Excel, appliquer le format numérique dans Excel, exporter un
  DataTable vers XLSX et importer un DataTable dans Excel avec Aspose Cells.
draft: false
keywords:
- how to style excel
- format column date excel
- apply number format excel
- export datatable to xlsx
- import datatable into excel
language: fr
og_description: Comment styliser les fichiers Excel en Java. Ce tutoriel montre comment
  formater la date d’une colonne Excel, appliquer un format numérique Excel, exporter
  un DataTable vers XLSX et importer un DataTable dans Excel.
og_title: Comment styliser Excel – Guide Java pour le formatage personnalisé des colonnes
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: How to style Excel files using Java. Learn to format column date Excel,
    apply number format Excel, export DataTable to XLSX and import DataTable into
    Excel with Aspose Cells.
  headline: How to Style Excel – Import DataTable with Custom Formatting in Java
  type: TechArticle
tags:
- Java
- Excel
- Aspose.Cells
title: Comment styliser Excel – Importer DataTable avec un formatage personnalisé
  en Java
url: /fr/java/excel-import-export/how-to-style-excel-import-datatable-with-custom-formatting-i/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment styliser Excel – Importer DataTable avec un formatage personnalisé en Java

Vous vous êtes déjà demandé **comment styliser Excel** de façon programmatique sans ouvrir le fichier manuellement ? Vous n'êtes pas seul. De nombreux développeurs doivent générer des rapports où la première colonne est en gras, la deuxième affiche des dates, et le reste suit une mise en page épurée. Dans ce guide, nous parcourrons un exemple complet et exécutable qui **importe un DataTable dans Excel**, applique un en‑tête en gras, formate une colonne de dates, puis **exporte le DataTable vers XLSX**.  

Nous utiliserons Aspose.Cells pour Java, mais les concepts s’appliquent à toute bibliothèque permettant de travailler avec les styles. À la fin, vous disposerez d’un modèle réutilisable pour **apply number format Excel** les cellules, **format column date Excel**, et livrer un classeur soigné à vos utilisateurs.

## Prérequis

- Java 17 (ou toute JDK récente)  
- Aspose.Cells pour Java 23.9 ou plus récent (l’essai gratuit suffit)  
- Une structure de type `DataTable` (l’exemple utilise une simple maquette)  
- Votre IDE préféré (IntelliJ IDEA, Eclipse, VS Code…)

Aucun plugin Maven supplémentaire n’est requis ; il suffit d’ajouter le JAR Aspose.Cells à votre classpath.

---

## Étape 1 : Obtenir le DataTable source – Préparation de « Export DataTable to XLSX »

Avant de pouvoir **import datatable into excel**, nous avons besoin d’un objet `DataTable` qui représente les données que vous souhaitez exporter. Dans les projets réels, vous le récupérerez peut‑être depuis une base de données, un fichier CSV ou une API. Pour ce tutoriel, nous allons simuler une petite table :

```java
import java.util.*;
import com.aspose.cells.*;

public class DemoData {
    public static DataTable getDataTable() {
        // Create a simple table with three columns: ID, Date, Amount
        DataTable dt = new DataTable();
        dt.getColumns().add("ID", DataType.INTEGER);
        dt.getColumns().add("OrderDate", DataType.DATE_TIME);
        dt.getColumns().add("Total", DataType.DOUBLE);

        // Add a few rows
        dt.getRows().add(new Object[]{1, new Date(), 125.50});
        dt.getRows().add(new Object[]{2, new Date(System.currentTimeMillis() - 86400000L), 99.99});
        dt.getRows().add(new Object[]{3, new Date(System.currentTimeMillis() - 2*86400000L), 250.00});
        return dt;
    }
}
```

> **Pourquoi c’est important :** Obtenir les données dès le départ signifie que le reste de la logique de style peut se concentrer uniquement sur la présentation, pas sur la manipulation des données.

---

## Étape 2 : Créer un tableau pour contenir les définitions de style de chaque colonne

Aspose.Cells vous permet de passer un tableau **Style[]** lors de l’importation d’un `DataTable`. Chaque entrée correspond à une colonne et détermine l’apparence de celle‑ci après l’import. Allouons le tableau en fonction du nombre de colonnes :

```java
DataTable dataTable = DemoData.getDataTable();
Style[] columnStyles = new Style[dataTable.getColumns().size()];
```

> **Astuce :** Si vous avez de nombreuses colonnes, envisagez de construire le tableau dans une boucle et de réutiliser un même objet `Style` lorsque le formatage est identique. Cela réduit la consommation de mémoire.

---

## Étape 3 : Définir les styles – En‑tête en gras & formatage de date

Nous répondons maintenant à la question classique **format column date excel** et démontrons également **apply number format excel** pour d’autres colonnes.

```java
// --- Style for the first column (header bold) ---
columnStyles[0] = new Style();
columnStyles[0].getFont().setBold(true);          // Makes header text bold

// --- Style for the second column (date formatting) ---
columnStyles[1] = new Style();
columnStyles[1].setNumber(StyleNumberFormat.DATE); // Uses the built‑in DATE format

// --- Optional: Style for the third column (currency) ---
columnStyles[2] = new Style();
columnStyles[2].setNumber(StyleNumberFormat.CURRENCY_USD);
```

**Que se passe‑t‑il ici ?**  
- `StyleNumberFormat.DATE` indique à Excel de traiter la valeur de la cellule comme une date courte (ex. : *31/01/2024*).  
- `StyleNumberFormat.CURRENCY_USD` ajoute automatiquement le symbole `$` et deux décimales.  
- Mettre la police en gras sur la première colonne fait ressortir l’en‑tête, ce qui est une exigence fréquente lorsque vous **how to style excel** des feuilles de calcul pour la lisibilité.

> **Cas particulier :** Si vos données source contiennent déjà des chaînes formatées, vous devrez peut‑être les convertir en objets `java.util.Date` avant l’import ; sinon Excel les traitera comme du texte brut.

---

## Étape 4 : Créer un nouveau classeur et accéder à sa première feuille

Un classeur vierge nous offre une toile propre. Nous allons récupérer la première feuille, où l’import sera effectué.

```java
Workbook workbook = new Workbook();               // New empty workbook
Worksheet worksheet = workbook.getWorksheets().get(0); // First sheet (index 0)
```

> **Pourquoi un nouveau classeur ?** Partir de zéro garantit qu’aucun style résiduel ou ligne masquée n’interfère avec le résultat final—essentiel lorsque vous **how to style excel** des fichiers de façon cohérente sur plusieurs exécutions.

---

## Étape 5 : Importer le DataTable avec les styles de colonne

Voici le cœur de l’opération : injecter le `DataTable` dans la feuille tout en appliquant le tableau de styles que nous avons construit.

```java
// The third argument (true) tells Aspose.Cells to include column headers.
worksheet.getCells().importDataTable(dataTable, true, columnStyles);
```

**Explication :**  
- `importDataTable` copie à la fois la ligne d’en‑tête et les lignes de données.  
- Le tableau `columnStyles` s’aligne sur chaque colonne, ainsi la première colonne aura son en‑tête en gras, la deuxième affichera des dates, et la troisième apparaîtra en devise.  
- Cette ligne unique remplace des dizaines d’étapes de formatage cellule par cellule, illustrant une façon propre de **apply number format excel** de façon programmatique.

---

## Étape 6 : Enregistrer le classeur stylisé – Finaliser le « Export DataTable to XLSX »

Enfin, nous persistons le classeur sur le disque. Ajustez le chemin vers un dossier accessible en écriture sur votre machine.

```java
String outputPath = "C:/temp/styledImport.xlsx";
workbook.save(outputPath);
System.out.println("Workbook saved to " + outputPath);
```

Ouvrez le fichier dans Excel et vous devriez voir :

- L’en‑tête de la colonne **ID** en gras.  
- La colonne **OrderDate** formatée en dates (ex. : *27/04/2024*).  
- La colonne **Total** affichée avec le symbole dollar et deux décimales.

> **Pro tip :** Si vous devez prendre en charge d’anciennes versions d’Excel, appelez `workbook.save(outputPath, SaveFormat.XLS)` au lieu du format XLSX par défaut.

---

## Étape 7 : Vérifier le résultat & ajustements optionnels

Il est recommandé de revérifier le fichier généré, surtout lorsqu’on automatise des rapports pour des parties prenantes.

```java
// Quick verification: read the first cell's style
Cell firstHeader = worksheet.getCells().get(0, 0);
boolean isBold = firstHeader.getStyle().getFont().isBold();
System.out.println("Header bold? " + isBold);
```

Si `isBold` affiche `true`, votre routine **how to style excel** a fonctionné comme prévu. À partir de là, vous pouvez :

- Ajouter un formatage conditionnel (ex. : mettre en surbrillance les totaux > 200 $).  
- Geler la première ligne pour faciliter le défilement.  
- Insérer un graphique qui référence les données importées.

Toutes ces extensions suivent le même schéma : définir un `Style`, l’appliquer, puis enregistrer.

---

## Questions fréquentes & cas particuliers

| Question | Réponse |
|----------|--------|
| **Puis‑je styliser plusieurs colonnes de la même façon ?** | Oui—réutilisez une même instance `Style` pour toutes les colonnes partageant le même format. |
| **Que se passe‑t‑il si mon DataTable possède plus de colonnes que de styles ?** | Toute colonne sans entrée correspondante dans `columnStyles` utilisera le style par défaut. |
| **Comment changer le format de date en « dd‑MMM‑yyyy » ?** | Utilisez `columnStyles[1].setCustom("#dd-MMM-yyyy#");` à la place du format intégré `DATE`. |
| **Existe‑t‑il un moyen d’ajuster automatiquement la largeur des colonnes après l’import ?** | Appelez `worksheet.autoFitColumns();` après `importDataTable`. |
| **Cela fonctionne‑t‑il sous Linux/macOS ?** | Absolument—Aspose.Cells est indépendant de la plateforme tant que vous disposez d’une JDK compatible. |

---

## Conclusion

Vous disposez maintenant d’un exemple complet, de bout en bout, de **how to style Excel** en **important datatable into excel**, **format column date excel**, et **apply number format excel** avec Java. Le code montre le flux complet, de **export datatable to xlsx** à l’ouverture du fichier dans Excel, en couvrant à la fois le *quoi* et le *pourquoi* de chaque étape.  

Testez‑le : modifiez le tableau de styles, ajoutez d’autres colonnes, ou branchez une vraie requête de base de données. Le même modèle vous permettra de générer des rapports à l’aspect professionnel en un clic, sans aucun formatage manuel.

---

![Styled Excel worksheet generated by the tutorial code](https://example.com/images/styled-worksheet.png "Screenshot of styled Excel worksheet created using Java and Aspose.Cells")

*Texte alternatif de l’image : « Feuille Excel stylisée créée avec Java et Aspose.Cells, montrant un en‑tête en gras et une colonne de dates formatée ». *

## Que devriez‑vous apprendre ensuite ?


Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets et fonctionnels avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [How to Create & Format Excel Cells Using Aspose.Cells for Java: A Step‑By‑Step Guide](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)
- [How to Style Excel Cells and Add Hyperlinks Using Aspose.Cells for Java](/cells/english/java/formatting/style-excel-cells-hyperlinks-aspose-cells-java/)
- [Aspose.Cells for Java: How to Create and Format Excel Workbooks Efficiently](/cells/english/java/getting-started/aspose-cells-java-workbook-creation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}