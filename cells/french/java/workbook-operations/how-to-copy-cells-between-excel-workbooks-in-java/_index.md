---
category: general
date: 2026-11-16
description: Comment copier des cellules entre des classeurs Excel en Java – charger
  un classeur, copier une plage entre les classeurs (y compris un tableau croisé dynamique),
  et enregistrer le fichier du classeur.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy cells
- copy range between workbooks
- copy pivot table workbook
- save workbook file
- load excel workbook java
language: fr
lastmod: 2026-11-16
og_description: Comment copier des cellules entre des classeurs Excel en Java. Apprenez
  à charger un classeur Excel, copier une plage (y compris un tableau croisé dynamique)
  entre les classeurs, et enregistrer le fichier du classeur.
og_image_alt: Screenshot of Java code copying a cell range from one Excel workbook
  to another
og_title: Comment copier des cellules entre des classeurs Excel en Java – guide complet
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: How to copy cells between Excel workbooks in Java – load a workbook,
    copy range between workbooks (including a pivot table), and save the workbook
    file.
  headline: How to copy cells between Excel workbooks in Java
  type: TechArticle
- description: How to copy cells between Excel workbooks in Java – load a workbook,
    copy range between workbooks (including a pivot table), and save the workbook
    file.
  name: How to copy cells between Excel workbooks in Java
  steps:
  - name: Load the source workbook
    text: '```java import com.aspose.cells.*;'
  - name: Define the range that includes the pivot table
    text: '```java // Define the cell range that you want to copy. // Adjust "A1:G20"
      to match the area that contains your data/pivot table. Range srcRange = srcWs.getCells().createRange("A1:G20");
      ```'
  - name: Create the destination workbook
    text: '```java // Create a new, empty workbook that will receive the copied range.
      Workbook destWb = new Workbook(); // defaults to a single empty sheet Worksheet
      destWs = destWb.getWorksheets().get(0); ```'
  - name: Copy the range to the destination workbook
    text: '```java // Copy the source range to cell A1 of the destination worksheet.
      destWs.getCells().copyRange(srcRange, destWs.getCells().get("A1")); ```'
  - name: Save the destination workbook
    text: '```java // Save the new workbook to disk. destWb.save("YOUR_DIRECTORY/dest.xlsx");
      } } ```'
  type: HowTo
tags:
- Java
- Excel
- Aspose.Cells
- Workbook manipulation
title: Comment copier des cellules entre des classeurs Excel en Java
url: /fr/java/workbook-operations/how-to-copy-cells-between-excel-workbooks-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment copier des cellules entre classeurs Excel en Java

Si vous devez **copier des cellules** d’un classeur Excel à un autre en Java, ce guide vous montre une méthode fiable pour le faire. Vous apprendrez comment **charger un classeur Excel avec Java**, copier une plage qui peut contenir un tableau croisé dynamique, puis **enregistrer le fichier du classeur** avec les données copiées.

Ce tutoriel couvre :

* Chargement d’un classeur source et sélection d’une feuille de calcul.  
* Définition de la plage exacte que vous souhaitez déplacer (y compris un tableau croisé dynamique).  
* Création d’un classeur de destination et copie de la plage.  
* Enregistrement du fichier de destination.  

L’exemple utilise la bibliothèque Aspose.Cells for Java, qui travaille avec les fichiers Excel sans nécessiter Microsoft Office. Le code fonctionne avec Java 8+ et tout IDE moderne (IntelliJ IDEA, Eclipse, VS Code, etc.).

---

## Prérequis

Avant de commencer, assurez-vous d’avoir :

| Exigence | Raison |
|----------|--------|
| Java Development Kit (JDK) 8 ou plus récent | Nécessaire pour compiler et exécuter le code. |
| Outil de construction Maven ou Gradle | Simplifie l’ajout de la dépendance Aspose.Cells. |
| Bibliothèque Aspose.Cells for Java (dernière version) | Fournit les classes `Workbook`, `Worksheet` et `Range` utilisées dans l’exemple. |
| Deux fichiers Excel (`source.xlsx` et un dossier vide pour `dest.xlsx`) | Le fichier source doit contenir les données et, éventuellement, le tableau croisé dynamique que vous voulez copier. |

Ajoutez la dépendance Aspose.Cells à votre `pom.xml` (Maven) ou `build.gradle` (Gradle). Exemple pour Maven :

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- use the latest version -->
</dependency>
```

---

## Comment copier des cellules avec Aspose.Cells

Les étapes suivantes vous guident à travers le processus complet. Chaque étape comprend le code Java, une explication du **pourquoi** de l’étape, et un conseil pour éviter les pièges courants.

### Étape 1 : Charger le classeur source

```java
import com.aspose.cells.*;

public class ExcelCopyDemo {
    public static void main(String[] args) throws Exception {
        // Load the source Excel file (replace with your actual path)
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");

        // Get the first worksheet (index 0)
        Worksheet srcWs = srcWb.getWorksheets().get(0);
```

**Pourquoi ?**  
`Workbook` représente le classeur Excel complet. Le charger vous donne accès à toutes les feuilles, cellules et objets tels que les tableaux croisés dynamiques. Utiliser la première feuille est courant, mais vous pouvez sélectionner n’importe quelle feuille par son nom (`srcWb.getWorksheets().get("Sheet2")`).

**Astuce pro :**  
Si le fichier source est volumineux, envisagez de le charger en mode *mémoire‑efficace* : `new Workbook("file.xlsx", new LoadOptions(LoadFormat.XLSX) {{ setMemorySetting(MemorySetting.MEMORY_PREFERENCE); }})`

### Étape 2 : Définir la plage qui inclut le tableau croisé dynamique

```java
        // Define the cell range that you want to copy.
        // Adjust "A1:G20" to match the area that contains your data/pivot table.
        Range srcRange = srcWs.getCells().createRange("A1:G20");
```

**Pourquoi ?**  
Un objet `Range` abstrait un bloc rectangulaire de cellules. En spécifiant `"A1:G20"` vous indiquez à Aspose.Cells exactement quelles cellules—y compris le tableau croisé dynamique intégré—copier. La bibliothèque copie automatiquement les données sous‑jacentes, les styles et les définitions du tableau.

**Cas particulier :**  
Si le tableau croisé dynamique dépasse la plage définie, élargissez l’adresse (par ex. : `"A1:Z100"`). Vous pouvez également utiliser `srcWs.getCells().getMaxDataColumn()` et `getMaxDataRow()` pour calculer dynamiquement la zone utilisée.

### Étape 3 : Créer le classeur de destination

```java
        // Create a new, empty workbook that will receive the copied range.
        Workbook destWb = new Workbook();               // defaults to a single empty sheet
        Worksheet destWs = destWb.getWorksheets().get(0);
```

**Pourquoi ?**  
Un classeur vierge garantit qu’aucun formatage indésirable ou feuille cachée n’interfère avec le contenu copié. Le classeur par défaut contient déjà une feuille, que nous utiliserons comme cible.

### Étape 4 : Copier la plage vers le classeur de destination

```java
        // Copy the source range to cell A1 of the destination worksheet.
        destWs.getCells().copyRange(srcRange, destWs.getCells().get("A1"));
```

**Pourquoi ?**  
`copyRange` gère tous les attributs des cellules : valeurs, formules, formatage, et même les caches de tableau croisé dynamique. En copiant vers `"A1"` vous placez la plage dans le coin supérieur‑gauche de la feuille de destination, en conservant la disposition originale.

**Question fréquente :** *Le tableau croisé dynamique restera‑t‑il fonctionnel ?*  
Oui. Aspose.Cells copie la définition du tableau croisé dynamique ainsi que son cache, de sorte que le tableau fonctionne exactement comme dans le classeur source.

### Étape 5 : Enregistrer le classeur de destination

```java
        // Save the new workbook to disk.
        destWb.save("YOUR_DIRECTORY/dest.xlsx");
    }
}
```

**Pourquoi ?**  
Appeler `save` écrit le classeur en mémoire dans un fichier physique `.xlsx`. Vous pouvez également enregistrer dans d’autres formats (`.xls`, `.csv`, `.pdf`) en changeant l’extension du fichier ou en utilisant `SaveOptions`.

**Conseil :**  
Si vous devez transmettre le fichier en flux à une réponse web, utilisez `destWb.save(OutputStream, SaveFormat.XLSX);` au lieu d’un chemin de fichier.

---

## Copier une plage entre classeurs – code source complet

Voici la classe Java complète, prête à être exécutée. Remplacez `YOUR_DIRECTORY` par le chemin réel sur votre machine.

```java
import com.aspose.cells.*;

public class ExcelCopyDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // Define the range that includes the data and pivot table
        Range srcRange = srcWs.getCells().createRange("A1:G20");

        // Create a new destination workbook
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);

        // Copy the defined range to the destination workbook
        destWs.getCells().copyRange(srcRange, destWs.getCells().get("A1"));

        // Save the destination workbook
        destWb.save("YOUR_DIRECTORY/dest.xlsx");
    }
}
```

**Résultat attendu :**  
`dest.xlsx` contient une réplique exacte de la plage `A1:G20` provenant de `source.xlsx`. Si la plage source contenait un tableau croisé dynamique, le fichier de destination affiche le même tableau avec sa source de données correctement liée aux cellules copiées.

Vous pouvez ouvrir `dest.xlsx` avec Excel, LibreOffice ou tout visualiseur supportant le format `.xlsx` pour vérifier que les valeurs, le formatage et la fonctionnalité du tableau sont préservés.

---

## Copier un classeur de tableau croisé dynamique – ce qu’il faut savoir

* **Le cache du tableau croisé dynamique est copié automatiquement.** La bibliothèque transfère le cache sous‑jacent, de sorte que le tableau n’a pas besoin d’être rafraîchi manuellement.
* **Les sources de données externes ne sont pas transférées.** Si le tableau puise ses données dans une base externe, vous devez vous assurer que le classeur de destination peut accéder à la même source, ou recréer le cache localement.
* **Les grands tableaux croisés dynamiques peuvent augmenter l’utilisation de mémoire.** Pour des classeurs très volumineux, envisagez d’augmenter le tas JVM (`-Xmx2g`) afin d’éviter les `OutOfMemoryError`.

---

## Enregistrer le classeur dans différents formats

Aspose.Cells vous permet d’enregistrer le résultat dans de nombreux formats sans modifier le code :

```java
// Save as XLS (Excel 97-2003)
destWb.save("dest.xls");

// Save as CSV (first worksheet only)
destWb.save("dest.csv");

// Save as PDF (visual representation)
destWb.save("dest.pdf");
```

Choisissez le format qui correspond à votre processus en aval. La même logique `copyRange` fonctionne quel que soit le format final.

---

## Charger un classeur Excel avec Java – conseils supplémentaires

* **Chargement de fichiers chiffrés :** Utilisez `LoadOptions` avec un mot de passe :  
  ```java
  LoadOptions opt = new LoadOptions(LoadFormat.XLSX);
  opt.setPassword("myPassword");
  Workbook wb = new Workbook("encrypted.xlsx", opt);
  ```
* **Lire uniquement des feuilles spécifiques :**  
  ```java
  LoadOptions opt = new LoadOptions(LoadFormat.XLSX);
  opt.setLoadDataOnly(true); // faster if you only need values
  Workbook wb = new Workbook("file.xlsx", opt);
  ```

Ces options peuvent accélérer l’étape **load excel workbook java**, surtout pour les fichiers volumineux.

---

## Conclusion

Vous savez maintenant **comment copier des cellules** entre classeurs Excel en Java, comment **copier une plage entre classeurs** contenant un **tableau croisé dynamique**, et comment **enregistrer le fichier du classeur** dans le format souhaité. En suivant les étapes ci‑dessus, vous pouvez intégrer la manipulation de données Excel dans n’importe quelle application Java—que vous construisiez un moteur de reporting, un pipeline ETL, ou un simple utilitaire de conversion de fichiers.

**Prochaines étapes** que vous pourriez explorer :

* Utiliser **copy range between workbooks** pour fusionner plusieurs rapports en

## Que devriez‑vous apprendre ensuite ?


Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques présentées dans ce guide. Chaque ressource comprend des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser d’autres fonctionnalités de l’API et à explorer des approches d’implémentation alternatives dans vos projets.

- [Enregistrer un nouveau classeur en Java – Tutoriel Copier une plage entre classeurs](/cells/english/java/workbook-operations/save-new-workbook-in-java-copy-range-between-workbooks-tutor/)
- [Comment copier des tableaux croisés dynamiques entre classeurs Excel en Java](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-tables-between-excel-workbooks-in-java/)
- [Comment copier une plage en Java – Copier un tableau croisé dynamique avec Aspose.Cells](/cells/english/java/excel-pivot-tables/how-to-copy-range-in-java-copy-pivot-table-with-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}