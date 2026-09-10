---
date: '2026-07-03'
description: Apprenez comment ajouter la dépendance Maven Aspose PDF et convertir
  le PDF en XPS avec du texte sélectionnable en utilisant Aspose.PDF pour Java. Guide
  étape par étape avec les prérequis et la FAQ.
keywords:
- aspose pdf maven dependency
- how to convert pdf to xps
- java convert pdf xps
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Learn how to add the Aspose PDF Maven dependency and convert PDF to
    XPS with selectable text using Aspose.PDF for Java. Step‑by‑step guide with prerequisites
    and FAQs.
  headline: Aspose PDF Maven Dependency – Convert PDF to XPS (Java)
  type: TechArticle
- description: Learn how to add the Aspose PDF Maven dependency and convert PDF to
    XPS with selectable text using Aspose.PDF for Java. Step‑by‑step guide with prerequisites
    and FAQs.
  name: Aspose PDF Maven Dependency – Convert PDF to XPS (Java)
  steps:
  - name: Load the PDF Document
    text: 'First, load your PDF document from its directory:'
  - name: Configure Save Options
    text: 'Create an instance of `XpsSaveOptions` to set up the XPS conversion options:'
  - name: Save as XPS File
    text: 'Finally, save the document in XPS format to your desired output directory:'
  type: HowTo
- questions:
  - answer: Yes—pass the password to the `Document` constructor or use `Document.open(String
      path, String password)` before conversion.
    question: Can I convert password‑protected PDFs?
  - answer: Absolutely. All vector shapes, images, and text are preserved, and the
      text remains selectable.
    question: Does the XPS retain vector graphics?
  - answer: The trial works without a license but adds a watermark to the output;
      a permanent license removes all restrictions.
    question: Is a license mandatory for the trial version?
  - answer: It processes files in a streaming manner, allowing conversion of PDFs
      with hundreds of pages without loading the entire document into memory.
    question: How does Aspose.PDF handle large files?
  - answer: The library runs on any OS with a compatible JDK, including Windows, Linux,
      and macOS.
    question: Which platforms are supported?
  type: FAQPage
title: Dépendance Maven Aspose PDF – Convertir PDF en XPS (Java)
url: /fr/java/conversion-export/convert-pdf-to-xps-aspose-pdf-java-selectable-text/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}
# Dépendance Maven Aspose PDF – Convertir PDF en XPS (Java)

## Introduction

Si vous devez **ajouter la dépendance Maven Aspose PDF** puis convertir des documents PDF en XPS tout en conservant le texte sélectionnable, vous êtes au bon endroit. Ce tutoriel vous guide à chaque étape — de la configuration de Maven ou Gradle, au chargement d’un PDF, à la configuration des options XPS, jusqu’à l’enregistrement d’un fichier XPS avec texte sélectionnable. À la fin, vous disposerez d’un extrait réutilisable que vous pourrez intégrer à n’importe quel projet Java.

## Réponses rapides
- **Quelle dépendance faut‑il ?** `com.aspose:aspose-pdf` (Maven) ou l’équivalent Gradle.  
- **Le XPS conserve‑t‑il le texte sélectionnable ?** Oui—Aspose.PDF préserve automatiquement les calques de texte.  
- **Quelle version de Java est requise ?** JDK 8 ou supérieur.  
- **Une licence est‑elle nécessaire en production ?** Une licence valide Aspose.PDF est requise pour une utilisation illimitée.  
- **Combien de temps prend la conversion ?** Généralement moins d’une seconde pour des fichiers de moins de 100 pages sur du matériel standard.

## Qu’est‑ce que la dépendance Maven Aspose PDF ?
L’artifact Maven `aspose-pdf` fournit l’API complète Aspose.PDF for Java, permettant la création, la manipulation et la conversion de PDF sans logiciel externe. Ajouter cette dépendance à votre `pom.xml` ou `build.gradle` télécharge toutes les binaires nécessaires, vous permettant de commencer à coder immédiatement sans gestion manuelle des JAR.

## Pourquoi convertir PDF en XPS avec texte sélectionnable ?
Aspose.PDF prend en charge **plus de 50 formats d’entrée et de sortie** et peut générer des fichiers XPS qui conservent une couche de texte recherchable et sélectionnable. C’est essentiel pour les flux de travail nécessitant des documents d’archivage, une fidélité de mise en page exacte ou une édition ultérieure avec des outils compatibles XPS. Les conversions s’effectuent en moins d’une seconde pour des PDF typiques de 20 pages sur un CPU moderne.

## Prérequis

- **Java Development Kit (JDK) 8+** installé et `JAVA_HOME` configuré.  
- **Maven 3.6+** ou **Gradle 6+** pour la gestion des dépendances.  
- Familiarité de base avec les I/O de fichiers Java et la gestion des exceptions.  

### Bibliothèques et dépendances requises

Vous aurez besoin de la bibliothèque Aspose.PDF for Java version 25.3 ou ultérieure. Incluez‑la à l’aide de l’un des outils de construction suivants :

**Maven :**  
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-pdf</artifactId>
    <version>25.3</version>
</dependency>
```  

**Gradle :**  
```gradle
implementation 'com.aspose:aspose-pdf:25.3'
```  

### Configuration de l’environnement

Assurez‑vous que votre IDE ou votre environnement de construction pointe vers le JDK correct et que le réseau puisse accéder à Maven Central ou à votre dépôt privé.

## Comment ajouter la dépendance Maven Aspose PDF ?

`aspose-pdf` est l’artifact que vous **ajoutez** à votre fichier de construction, puis **rafraîchissez** les dépendances afin que les JAR soient téléchargés automatiquement. Pour Maven, insérez le bloc `<dependency>` à l’intérieur de `<dependencies>` ; pour Gradle, placez la ligne `implementation` dans le bloc `dependencies`. Après le rafraîchissement, les classes Aspose sont disponibles sur le classpath, et vous pouvez commencer à coder sans manipulation manuelle des JAR.

## Configuration d’Aspose.PDF for Java

### Étapes d’installation

1. **Configuration Maven/Gradle :** Ajoutez la dépendance comme indiqué ci‑dessus et exécutez `mvn clean install` ou `gradle build` pour récupérer la bibliothèque.  
2. **Acquisition de licence :**  
   - Téléchargez un [essai gratuit](https://releases.aspose.com/pdf/java/) ou obtenez une [licence temporaire](https://purchase.aspose.com/temporary-license/).  
   - Placez le fichier de licence (`Aspose.Pdf.lic`) dans un dossier accessible à votre application et chargez‑le au démarrage.

### Initialisation de base

`License` applique un fichier de licence Aspose pour débloquer toutes les fonctionnalités.  
Chargez la licence (si vous en avez une) et créez un objet `Document` pour travailler avec les PDF.  
`Document` représente un fichier PDF et fournit des méthodes pour manipuler son contenu.

```java
import com.aspose.pdf.Document;
import com.aspose.pdf.License;

// Initialize a License object
License license = new License();

// Set the license file path
license.setLicense("path/to/Aspose.Total.Java.lic");
```  

## Comment convertir PDF en XPS avec texte sélectionnable ?

`XpsSaveOptions` configure les paramètres d’enregistrement d’un PDF au format XPS, y compris la préservation du texte.  
Chargez le PDF source, configurez `XpsSaveOptions` pour conserver le texte, puis invoquez `save` avec l’extension `.xps`. L’API intègre automatiquement une couche de texte, de sorte que le XPS résultant puisse être recherché et copié comme le PDF original. Ce **processus** nécessite généralement seulement trois lignes de code après la mise en place de la bibliothèque.

## Guide d’implémentation

### Convertir PDF en XPS

Cette fonctionnalité vous permet de convertir un document PDF en fichier XPS à l’aide d’Aspose.PDF for Java.

#### Étape 1 : Charger le document PDF

Tout d’abord, **chargez** votre document PDF **depuis** son **répertoire** :

```java
import com.aspose.pdf.Document;

String dataDir = "YOUR_DOCUMENT_DIRECTORY";
Document pdfDocument = new Document(dataDir + "/input.pdf");
```  

#### Étape 2 : Configurer les options d’enregistrement

Créez une instance de `XpsSaveOptions` pour définir les options de conversion XPS :

```java
import com.aspose.pdf.XpsSaveOptions;

XpsSaveOptions saveOptions = new XpsSaveOptions();
```  

#### Étape 3 : Enregistrer en fichier XPS

Enfin, enregistrez le document au format XPS dans le répertoire de sortie souhaité :

```java
String outputDir = "YOUR_OUTPUT_DIRECTORY";
pdfDocument.save(outputDir + "/ConvertPDFtoXPS_out.xps\
```  

## Problèmes courants et solutions

- **Pages blanches dans la sortie XPS :** Assurez‑vous que le PDF n’utilise pas de flux chiffrés ; le cas échéant, fournissez le mot de passe lors du chargement du `Document`.  
- **Erreurs de mémoire sur de gros PDF :** Utilisez `Document.optimizeResources()` avant l’enregistrement pour réduire l’empreinte mémoire.  
- **Polices manquantes :** Installez les polices requises sur le serveur ou intégrez‑les dans le PDF avant la conversion.

## Questions fréquemment posées

**Q : Puis‑je convertir des PDF protégés par mot de passe ?**  
R : Oui—passez le mot de passe au constructeur `Document` ou utilisez `Document.open(String path, String password)` avant la conversion.

**Q : Le XPS conserve‑t‑il les graphiques vectoriels ?**  
R : Absolument. Toutes les formes vectorielles, images et textes sont préservés, et le texte reste sélectionnable.

**Q : Une licence est‑elle obligatoire pour la version d’essai ?**  
R : L’essai fonctionne sans licence mais ajoute un filigrane à la sortie ; une licence permanente supprime toutes les restrictions.

**Q : Comment Aspose.PDF gère‑t‑il les gros fichiers ?**  
R : Il traite les fichiers de manière flux, permettant la conversion de PDF de plusieurs centaines de pages sans charger l’ensemble du document en mémoire.

**Q : Quelles plateformes sont prises en charge ?**  
R : La bibliothèque fonctionne sur tout OS disposant d’un JDK compatible, y compris Windows, Linux et macOS.

---

**Dernière mise à jour :** 2026-07-03  
**Testé avec :** Aspose.PDF for Java 25.3  
**Auteur :** Aspose  

{{< blocks/products/products-backtop-button >}}

## Tutoriels associés

- [Convert PDF to JPEG using Aspose.PDF for Java: Step‑By‑Step Guide](/pdf/java/conversion-export/convert-pdf-to-jpeg-aspose-java-tutorial/)
- [How to Convert PDF to Excel Using Aspose.PDF for Java | Step‑By‑Step Guide](/pdf/java/conversion-export/convert-pdf-excel-aspose-java-tutorial/)
- [How to Convert XPS Files to PDF Using Aspose.PDF in Java: A Complete Guide](/pdf/java/conversion-export/convert-xps-pdf-aspose-java-guide/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}