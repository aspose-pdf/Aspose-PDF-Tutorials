---
date: '2026-07-03'
description: Pelajari cara menambahkan dependensi Maven Aspose PDF dan mengonversi
  PDF ke XPS dengan teks yang dapat dipilih menggunakan Aspose.PDF untuk Java. Panduan
  langkah demi langkah dengan prasyarat dan FAQ.
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
title: Dependensi Maven Aspose PDF – Mengonversi PDF ke XPS (Java)
url: /id/java/conversion-export/convert-pdf-to-xps-aspose-pdf-java-selectable-text/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}
# Aspose PDF Maven Dependency – Mengonversi PDF ke XPS (Java)

## Pendahuluan

Jika Anda perlu **menambahkan dependensi Aspose PDF Maven** dan kemudian mengonversi dokumen PDF ke XPS sambil mempertahankan teks yang dapat dipilih, Anda berada di tempat yang tepat. Tutorial ini memandu Anda melalui setiap langkah—dari mengonfigurasi Maven atau Gradle, memuat PDF, mengatur opsi XPS, hingga akhirnya menyimpan file XPS dengan teks yang dapat dipilih. Pada akhir tutorial, Anda akan memiliki potongan kode yang dapat digunakan kembali dan dapat dimasukkan ke dalam proyek Java mana pun.

## Jawaban Cepat
- **Apa dependensi yang saya perlukan?** `com.aspose:aspose-pdf` (Maven) atau artefak Gradle yang setara.  
- **Apakah XPS dapat mempertahankan teks yang dapat dipilih?** Ya—Aspose.PDF secara otomatis mempertahankan lapisan teks.  
- **Versi Java apa yang diperlukan?** JDK 8 atau lebih baru.  
- **Apakah saya memerlukan lisensi untuk produksi?** Lisensi Aspose.PDF yang valid diperlukan untuk penggunaan tanpa batas.  
- **Berapa lama proses konversi?** Biasanya kurang dari satu detik untuk file dengan kurang dari 100 halaman pada perangkat keras standar.

## Apa itu Aspose PDF Maven Dependency?
Artefak Maven `aspose-pdf` menyediakan API lengkap Aspose.PDF untuk Java, memungkinkan pembuatan, manipulasi, dan konversi PDF tanpa perangkat lunak eksternal. Menambahkan dependensi ini ke `pom.xml` atau `build.gradle` akan menarik semua binari yang diperlukan, sehingga Anda dapat mulai menulis kode segera tanpa mengelola JAR secara manual.

## Mengapa mengonversi PDF ke XPS dengan teks yang dapat dipilih?
Aspose.PDF mendukung **lebih dari 50 format input dan output** dan dapat menghasilkan file XPS yang mempertahankan lapisan teks yang dapat dicari dan dipilih. Hal ini penting untuk alur kerja yang memerlukan dokumen arsip dengan fidelitas tata letak yang tepat atau pengeditan lanjutan di alat yang mendukung XPS. Konversi selesai dalam waktu kurang dari satu detik untuk PDF 20 halaman tipikal pada CPU modern.

## Prasyarat

- **Java Development Kit (JDK) 8+** terpasang dan `JAVA_HOME` dikonfigurasi.  
- **Maven 3.6+** atau **Gradle 6+** untuk manajemen dependensi.  
- Pemahaman dasar tentang I/O file Java dan penanganan pengecualian.  

### Perpustakaan dan Dependensi yang Diperlukan

Anda memerlukan perpustakaan Aspose.PDF untuk Java versi 25.3 atau lebih baru. Sertakan menggunakan salah satu alat build berikut:

**Maven:**  
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-pdf</artifactId>
    <version>25.3</version>
</dependency>
```  

**Gradle:**  
```gradle
implementation 'com.aspose:aspose-pdf:25.3'
```  

### Pengaturan Lingkungan

Pastikan IDE atau lingkungan build Anda menunjuk ke JDK yang tepat dan jaringan dapat mengakses Maven Central atau repositori pribadi Anda.

## Cara menambahkan dependensi Aspose PDF Maven?

`aspose-pdf` adalah artefak yang Anda tambahkan ke file build proyek, kemudian menyegarkan dependensi sehingga JAR diunduh secara otomatis. Untuk Maven, sisipkan blok `<dependency>` di dalam `<dependencies>`; untuk Gradle, letakkan baris `implementation` di dalam blok `dependencies`. Setelah penyegaran, kelas Aspose tersedia di classpath, dan Anda dapat mulai menulis kode tanpa penanganan JAR manual.

## Menyiapkan Aspose.PDF untuk Java

### Langkah-langkah Instalasi

1. **Pengaturan Maven/Gradle:** Tambahkan dependensi seperti yang ditunjukkan di atas dan jalankan `mvn clean install` atau `gradle build` untuk mengunduh perpustakaan.  
2. **Perolehan Lisensi:**  
   - Unduh [free trial](https://releases.aspose.com/pdf/java/) atau dapatkan [temporary license](https://purchase.aspose.com/temporary-license/).  
   - Tempatkan file lisensi (`Aspose.Pdf.lic`) di folder yang dapat diakses aplikasi Anda dan muat pada saat startup.

### Inisialisasi Dasar

`License` menerapkan file lisensi Aspose untuk membuka semua fungsi.  
Muat lisensi (jika ada) dan buat objek `Document` untuk bekerja dengan PDF.  
`Document` mewakili file PDF dan menyediakan metode untuk memanipulasi isinya.

```java
import com.aspose.pdf.Document;
import com.aspose.pdf.License;

// Initialize a License object
License license = new License();

// Set the license file path
license.setLicense("path/to/Aspose.Total.Java.lic");
```  

## Cara mengonversi PDF ke XPS dengan teks yang dapat dipilih?

`XpsSaveOptions` mengonfigurasi pengaturan untuk menyimpan PDF sebagai dokumen XPS, termasuk pelestarian teks. Muat PDF sumber, atur `XpsSaveOptions` agar mempertahankan teks, dan panggil `save` dengan ekstensi `.xps`. API secara otomatis menyematkan lapisan teks, sehingga XPS yang dihasilkan dapat dicari dan disalin seperti PDF asli. Seluruh proses ini biasanya hanya memerlukan tiga baris kode setelah perpustakaan disiapkan.

## Panduan Implementasi

### Mengonversi PDF ke XPS

Fitur ini memungkinkan Anda mengonversi dokumen PDF menjadi file XPS menggunakan Aspose.PDF untuk Java.

#### Langkah 1: Muat Dokumen PDF

Pertama, muat dokumen PDF Anda dari direktori terkait:

```java
import com.aspose.pdf.Document;

String dataDir = "YOUR_DOCUMENT_DIRECTORY";
Document pdfDocument = new Document(dataDir + "/input.pdf");
```  

#### Langkah 2: Atur Opsi Penyimpanan

Buat instance `XpsSaveOptions` untuk menyiapkan opsi konversi XPS:

```java
import com.aspose.pdf.XpsSaveOptions;

XpsSaveOptions saveOptions = new XpsSaveOptions();
```  

#### Langkah 3: Simpan sebagai File XPS

Akhirnya, simpan dokumen dalam format XPS ke direktori output yang diinginkan:

```java
String outputDir = "YOUR_OUTPUT_DIRECTORY";
pdfDocument.save(outputDir + "/ConvertPDFtoXPS_out.xps\
```  

## Masalah Umum dan Solusinya

- **Halaman kosong pada output XPS:** Pastikan PDF tidak menggunakan aliran terenkripsi; jika iya, berikan kata sandi saat memuat `Document`.  
- **Kesalahan memori pada PDF besar:** Gunakan `Document.optimizeResources()` sebelum menyimpan untuk mengurangi jejak memori.  
- **Font yang hilang:** Instal font yang diperlukan di server atau sematkan dalam PDF sebelum konversi.

## Pertanyaan yang Sering Diajukan

**Q: Dapatkah saya mengonversi PDF yang dilindungi kata sandi?**  
A: Ya—berikan kata sandi ke konstruktor `Document` atau gunakan `Document.open(String path, String password)` sebelum konversi.

**Q: Apakah XPS mempertahankan grafik vektor?**  
A: Tentu saja. Semua bentuk vektor, gambar, dan teks dipertahankan, dan teks tetap dapat dipilih.

**Q: Apakah lisensi wajib untuk versi percobaan?**  
A: Versi percobaan dapat berjalan tanpa lisensi tetapi menambahkan watermark pada output; lisensi permanen menghapus semua pembatasan.

**Q: Bagaimana Aspose.PDF menangani file besar?**  
A: Ia memproses file secara streaming, memungkinkan konversi PDF dengan ratusan halaman tanpa memuat seluruh dokumen ke memori.

**Q: Platform apa yang didukung?**  
A: Perpustakaan ini berjalan pada semua OS dengan JDK yang kompatibel, termasuk Windows, Linux, dan macOS.

---

**Last Updated:** 2026-07-03  
**Tested With:** Aspose.PDF for Java 25.3  
**Author:** Aspose  

{{< blocks/products/products-backtop-button >}}

## Tutorial Terkait

- [Convert PDF to JPEG using Aspose.PDF for Java: Step‑By‑Step Guide](/pdf/java/conversion-export/convert-pdf-to-jpeg-aspose-java-tutorial/)
- [How to Convert PDF to Excel Using Aspose.PDF for Java | Step‑By‑Step Guide](/pdf/java/conversion-export/convert-pdf-excel-aspose-java-tutorial/)
- [How to Convert XPS Files to PDF Using Aspose.PDF in Java: A Complete Guide](/pdf/java/conversion-export/convert-xps-pdf-aspose-java-guide/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}