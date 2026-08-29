---
category: general
date: 2026-08-11
description: Créer un nouveau classeur Aspose en Java, ajouter une propriété personnalisée
  Excel, puis enregistrer le classeur au format XLSB avec un exemple complet étape
  par étape.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create new workbook aspose
- save workbook as xlsb
- add custom property excel
- Aspose.Cells Java
- custom properties Excel
- workbook serialization
language: fr
lastmod: 2026-08-11
og_description: Créez un nouveau classeur Aspose en Java, ajoutez une propriété personnalisée
  Excel, puis enregistrez le classeur au format XLSB avec un exemple complet, prêt
  à l’exécution.
og_image_alt: Java code screenshot that creates a new workbook Aspose, adds a custom
  Excel property, and saves it as an XLSB file
og_title: Créer un nouveau classeur Aspose – ajouter une propriété personnalisée Excel
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: Create new workbook Aspose in Java, add a custom property Excel, then
    save workbook as XLSB with a full step‑by‑step example.
  headline: Create new workbook Aspose – add custom property Excel and save as XLSB
  type: TechArticle
- description: Create new workbook Aspose in Java, add a custom property Excel, then
    save workbook as XLSB with a full step‑by‑step example.
  name: Create new workbook Aspose – add custom property Excel and save as XLSB
  steps:
  - name: What if I need to store a string property?
    text: '```java worksheet.getCustomProperties().add("Owner", "Alice"); ```'
  - name: Can I add multiple custom properties at once?
    text: Yes. Call `add` repeatedly for each name/value pair. Aspose.Cells does not
      limit the number of custom properties, but keep the total size reasonable to
      avoid bloating the file.
  - name: How does the binary format affect performance?
    text: XLSB files load faster because they avoid XML parsing. This is especially
      noticeable for workbooks with many rows, formulas, or embedded images.
  - name: What if I need to work with an existing XLSX file?
    text: Replace the `new Workbook()` constructor with `new Workbook("ExistingFile.xlsx")`.
      The rest of the steps (adding properties, saving as XLSB) remain identical.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- XLSB
- Custom Properties
title: Créer un nouveau classeur Aspose – ajouter une propriété personnalisée Excel
  et enregistrer au format XLSB
url: /fr/java/spreadsheet-automation/create-new-workbook-aspose-add-custom-property-excel-and-sav/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un nouveau classeur Aspose – ajouter une propriété personnalisée Excel et enregistrer au format XLSB

Si vous devez **créer un nouveau classeur Aspose** dans une application Java, ce guide vous montre exactement comment le faire. Vous apprendrez à **ajouter une propriété personnalisée Excel**, récupérer la valeur, et **enregistrer le classeur au format XLSB** sans perdre aucune métadonnée.

Le tutoriel couvre tout, de la configuration du projet à la vérification du fichier enregistré. Aucune documentation externe n’est requise ; suivez simplement les étapes et exécutez le code.

## Prérequis

Avant de commencer, assurez-vous d’avoir :

- Java Development Kit (JDK) 8 ou version supérieure installé.
- Maven ou Gradle pour gérer les dépendances (l’exemple utilise Maven).
- Une licence active d’Aspose.Cells pour Java (ou utilisez le mode d’évaluation gratuit pour les tests).

## Étape 1 : Ajouter Aspose.Cells à votre projet

Ajoutez l’artifact Maven Aspose.Cells à votre `pom.xml`. Cette dépendance fournit les classes nécessaires pour **créer de nouveaux classeurs Aspose**.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- Use the latest stable version -->
</dependency>
```

> **Astuce :** Si vous préférez Gradle, remplacez le fragment Maven par la ligne équivalente `implementation "com.aspose:aspose-cells:23.12"`.

## Étape 2 : Créer un nouveau classeur Aspose

La première étape fonctionnelle consiste à instancier un objet `Workbook`. Cet objet représente un fichier Excel en mémoire et constitue le point d’entrée pour toutes les opérations ultérieures.

```java
import com.aspose.cells.*;

public class CustomPropertiesXlsb {

    public static void main(String[] args) throws Exception {
        // Step 2: Create a new workbook Aspose
        Workbook workbook = new Workbook();               // In‑memory workbook
        Worksheet worksheet = workbook.getWorksheets().get(0); // Default first sheet
```

Créer un nouveau classeur Aspose vous fournit un classeur vierge avec une feuille de calcul par défaut, prêt à être personnalisé.

## Étape 3 : Ajouter une propriété personnalisée Excel

Les propriétés personnalisées vous permettent de stocker des métadonnées arbitraires dans un fichier Excel. Ici, nous **ajoutons une propriété personnalisée Excel** nommée `ProjectId` avec une valeur numérique.

```java
        // Step 3: Add a custom property named "ProjectId" with a numeric value
        worksheet.getCustomProperties().add("ProjectId", 12345);
```

La méthode `add` accepte un nom de propriété et une valeur de tout type pris en charge (chaîne, nombre, date, etc.). Ces métadonnées voyagent avec le fichier où que vous le copiez.

## Étape 4 : Récupérer et afficher la propriété personnalisée

Lire à nouveau la propriété vérifie qu’elle a été stockée correctement. Vous pouvez également utiliser la valeur récupérée dans votre logique métier.

```java
        // Step 4: Retrieve the custom property value and display it
        int projectId = (int) worksheet.getCustomProperties()
                                      .get("ProjectId")
                                      .getValue();
        System.out.println("ProjectId = " + projectId);
```

Le cast en `int` fonctionne parce que nous avons stocké une valeur numérique. Si vous stockez une chaîne, utilisez `(String)` à la place.

## Étape 5 : Enregistrer le classeur au format XLSB

Maintenant, vous **enregistrez le classeur au format XLSB**. Le format XLSB stocke le classeur sous forme binaire, ce qui le rend plus rapide à ouvrir et plus petit sur le disque. Toutes les propriétés personnalisées sont conservées automatiquement.

```java
        // Step 5: Save the workbook as an XLSB file (custom properties are preserved)
        workbook.save("WithCustomProps.xlsb", SaveFormat.XLSB);
    }
}
```

Remplacez `"WithCustomProps.xlsb"` par un chemin absolu si vous avez besoin du fichier dans un répertoire spécifique. L’énumération `SaveFormat.XLSB` indique à Aspose.Cells d’écrire le format binaire.

## Étape 6 : Vérifier la sortie

Exécutez le programme depuis votre IDE ou la ligne de commande :

```bash
mvn compile exec:java -Dexec.mainClass=CustomPropertiesXlsb
```

Vous devriez voir :

```
ProjectId = 12345
```

Ouvrez `WithCustomProps.xlsb` dans Excel. Accédez à **Fichier → Infos → Propriétés → Propriétés avancées → Personnalisées**. L’entrée `ProjectId` avec la valeur `12345` sera affichée, confirmant que l’étape **add custom property excel** a réussi et que l’opération **save workbook as xlsb** a conservé les métadonnées.

## Questions fréquentes et cas particuliers

### Et si je dois stocker une propriété de type chaîne ?

```java
worksheet.getCustomProperties().add("Owner", "Alice");
```

Récupérez‑la avec :

```java
String owner = (String) worksheet.getCustomProperties().get("Owner").getValue();
```

### Puis‑je ajouter plusieurs propriétés personnalisées en même temps ?

Oui. Appelez `add` de façon répétée pour chaque paire nom/valeur. Aspose.Cells ne limite pas le nombre de propriétés personnalisées, mais gardez la taille totale raisonnable afin d’éviter d’alourdir le fichier.

### Comment le format binaire affecte‑t‑il les performances ?

Les fichiers XLSB se chargent plus rapidement car ils évitent l’analyse XML. Cela est particulièrement perceptible pour les classeurs contenant de nombreuses lignes, formules ou images intégrées.

### Et si je dois travailler avec un fichier XLSX existant ?

Remplacez le constructeur `new Workbook()` par `new Workbook("ExistingFile.xlsx")`. Le reste des étapes (ajout de propriétés, enregistrement au format XLSB) reste identique.

## Code source complet

Voici l’exemple complet, prêt à être exécuté. Copiez‑le dans un fichier nommé `CustomPropertiesXlsb.java` à l’intérieur de votre dossier `src/main/java`.

```java
import com.aspose.cells.*;

public class CustomPropertiesXlsb {
    public static void main(String[] args) throws Exception {
        // Step 2: Create a new workbook Aspose
        Workbook workbook = new Workbook();                       // In‑memory workbook
        Worksheet worksheet = workbook.getWorksheets().get(0);    // Default first sheet

        // Step 3: Add a custom property named "ProjectId" with a numeric value
        worksheet.getCustomProperties().add("ProjectId", 12345);

        // Step 4: Retrieve the custom property value and display it
        int projectId = (int) worksheet.getCustomProperties()
                                      .get("ProjectId")
                                      .getValue();
        System.out.println("ProjectId = " + projectId);

        // Step 5: Save the workbook as an XLSB file (custom properties are preserved)
        workbook.save("WithCustomProps.xlsb", SaveFormat.XLSB);
    }
}
```

L’exécution de cette classe produit un fichier XLSB contenant la propriété personnalisée et pouvant être ouvert dans n’importe quelle version moderne de Microsoft Excel.

## Conclusion

Vous savez maintenant comment **créer un nouveau classeur Aspose**, **ajouter une propriété personnalisée Excel**, et **enregistrer le classeur au format XLSB** en Java. L’exemple montre le cycle complet : initialisation, injection de métadonnées, vérification et sérialisation binaire.

Ensuite, explorez des sujets connexes tels que **définir les propriétés du document**, **travailler avec les formules Excel**, ou **convertir entre XLSX et XLSB**. Chacun de ces points s’appuie sur la même API Aspose.Cells que vous venez d’utiliser, vous permettant d’étendre la solution sans apprendre de nouvelles bibliothèques.

N’hésitez pas à expérimenter avec différents types de données, plusieurs feuilles de calcul ou la protection par mot de passe — Aspose.Cells prend en charge tous ces scénarios dès le départ. Bon codage !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités supplémentaires de l’API et à explorer des approches d’implémentation alternatives dans vos propres projets.

- [Créer et enregistrer un classeur Excel Aspose Cells Java](/cells/english/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)
- [Comment créer et enregistrer un classeur Excel au format SVG avec Aspose.Cells pour Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [Créer un classeur Excel et ajouter des libellés avec Aspose.Cells pour Java](/cells/english/java/advanced-excel-charts/data-labeling/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}