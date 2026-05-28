---
date: '2026-05-28'
description: Pelajari cara mengatur tampilan halaman tunggal PDF, mengubah preferensi
  penampil, mengedit penanda buku, dan mengonfigurasi pengaturan PDF menggunakan Aspose.PDF
  for Java.
keywords:
- single page view pdf
- aspose pdf maven dependency
- change pdf viewer preference
- configure pdf viewer settings
- set pdf bookmark destination
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: Learn how to set single page view PDF, change viewer preferences, edit
    bookmarks, and configure PDF settings using Aspose.PDF for Java.
  headline: Single Page View PDF in Java – Change Layout & Edit Bookmarks
  type: TechArticle
- description: Learn how to set single page view PDF, change viewer preferences, edit
    bookmarks, and configure PDF settings using Aspose.PDF for Java.
  name: Single Page View PDF in Java – Change Layout & Edit Bookmarks
  steps:
  - name: '**Digital Books** – Ensure each chapter bookmark lands at the top of the
      page for a seamless reading experience.'
    text: '**Digital Books** – Ensure each chapter bookmark lands at the top of the
      page for a seamless reading experience.'
  - name: '**Technical Manuals** – Precise navigation helps engineers find sections
      quickly, especially in large PDFs.'
    text: '**Technical Manuals** – Precise navigation helps engineers find sections
      quickly, especially in large PDFs.'
  - name: '**Product Catalogs** – Single‑page layout makes browsing catalogs on tablets
      more intuitive.'
    text: '**Product Catalogs** – Single‑page layout makes browsing catalogs on tablets
      more intuitive.'
  type: HowTo
- questions:
  - answer: Use `new Document("path/to/file.pdf")`; Aspose.PDF automatically detects
      the file format.
    question: What is the easiest way to load a PDF document in Java?
  - answer: Yes, you can set viewer preferences directly on the `Document` object
      via `pdfDocument.getViewerPreferences().setPageLayout(...)`.
    question: Can I change the page layout without using PdfContentEditor?
  - answer: Viewer layout only influences on‑screen display; it does not alter the
      printed output.
    question: Does changing the viewer layout affect printing?
  - answer: No explicit limit, but extremely large outline trees may impact performance;
      keep them organized.
    question: Are there limits on the number of bookmarks I can create?
  - answer: Re‑calculate destinations using the current page indices after any structural
      changes.
    question: How do I ensure bookmark destinations are accurate after adding or removing
      pages?
  type: FAQPage
title: Tampilan Halaman Tunggal PDF di Java – Ubah Tata Letak & Edit Penanda Buku
url: /id/java/bookmarks-navigation/edit-pdf-bookmarks-viewer-settings-aspose-pdf-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/products-backtop-button >}}
# Tampilan Halaman Tunggal PDF di Java – Ubah Tata Letak & Edit Penanda Buku

## Pendahuluan
Saat pembaca membuka PDF berukuran besar, tata letak penampil default mungkin menggulir secara terus‑menerus, sehingga sulit untuk fokus pada satu halaman. Dengan mengonfigurasi pengaturan **single page view pdf**, Anda memaksa penampil menampilkan satu halaman pada satu waktu, yang ideal untuk laporan, e‑book, dan katalog. Dalam tutorial ini Anda juga akan belajar cara mengedit penanda buku PDF yang ada, mengatur tujuan penanda buku saat membuat dokumen, dan menyesuaikan preferensi penampil lainnya menggunakan Aspose.PDF untuk Java. Pada akhir tutorial Anda akan memiliki kontrol penuh atas navigasi, akurasi penanda buku, dan tata letak di layar.

**Apa yang Akan Anda Pelajari**
- Cara mengedit penanda buku PDF yang ada sehingga mereka mengarah ke awal halaman.  
- Cara mengatur tujuan penanda buku saat membuat PDF.  
- Cara mengubah preferensi penampil seperti tata letak satu halaman.  
- Tips praktis untuk memuat dokumen PDF di Java dan mengoptimalkan kinerja.

### Jawaban Cepat
- **Apa cara utama untuk mengaktifkan tampilan halaman tunggal PDF?** Panggil `PdfContentEditor.changeViewerPreference()` dengan `ViewerPreference.PAGE_LAYOUT_SINGLE_PAGE`.  
- **Apakah tujuan penanda buku dapat diedit setelah PDF dihasilkan?** Ya – muat dokumen, ambil outline, dan tetapkan `ExplicitDestination` baru.  
- **Apakah saya memerlukan lisensi untuk fitur ini?** Versi percobaan gratis dapat digunakan untuk evaluasi; lisensi penuh menghilangkan semua batasan.  
- **Dependensi Maven mana yang diperlukan?** `com.aspose:aspose-pdf:25.3` (atau yang lebih baru).  
- **Apakah ini kompatibel dengan Java 11 ke atas?** Tentu – Aspose.PDF mendukung Java 8+.

## Apa itu “ubah tata letak halaman PDF”?
Mengubah tata letak halaman PDF mengontrol bagaimana halaman ditampilkan dalam penampil—satu halaman, berkelanjutan, tampilan dua halaman, dll. Mengaktifkan **single page view pdf** meningkatkan keterbacaan untuk dokumen panjang dan memastikan setiap halaman ditampilkan secara terpisah, yang sangat membantu pada perangkat seluler dan tablet.

## Mengapa mengedit penanda buku PDF dan mengatur tujuan penanda buku?
Penanda buku berfungsi seperti daftar isi dinamis. Tujuan yang tepat memungkinkan pembaca melompat langsung ke bagian yang dimaksud, menghilangkan gulir tambahan dan mengurangi frustrasi pengguna. Hal ini menghasilkan pengalaman navigasi yang lebih mulus dan kepuasan lebih tinggi untuk manual teknis, katalog produk, dan buku digital.

## Prasyarat
- **Perpustakaan & Dependensi**: Aspose.PDF untuk Java v25.3 atau lebih baru.  
- **Lingkungan**: JDK 8 atau lebih baru, alat build Maven atau Gradle.  
- **Pengetahuan**: Pemrograman Java dasar dan pemahaman tentang konsep PDF.

## Menyiapkan Aspose.PDF untuk Java
### Instalasi Maven
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-pdf</artifactId>
    <version>25.3</version>
</dependency>
```
### Instalasi Gradle
```gradle
implementation 'com.aspose:aspose-pdf:25.3'
```
**Perolehan Lisensi**: Mulailah dengan versi percobaan gratis atau minta lisensi sementara untuk akses penuh fitur. Pertimbangkan membeli lisensi permanen untuk penggunaan produksi.

### Inisialisasi Dasar
Kelas `Document` adalah objek inti Aspose.PDF yang mewakili file PDF dalam memori. Setelah membuat sebuah instance, semua operasi baca/tulis mengalir melalui objek ini.  
```java
import com.aspose.pdf.Document;

public class PDFSetup {
    public static void main(String[] args) {
        // Initialize document object
        Document pdfDocument = new Document("path/to/your/pdf");
        
        System.out.println("Aspose.PDF for Java initialized successfully.");
    }
}
```

## Panduan Implementasi
### Cara Mengubah Tata Letak Halaman PDF di Java
**Gambaran Umum**: Sesuaikan preferensi penampil untuk menampilkan halaman sesuai keinginan Anda.

#### Menginisialisasi PdfContentEditor
`PdfContentEditor` adalah kelas utilitas yang memungkinkan Anda memodifikasi pengaturan penampil tanpa menulis ulang seluruh dokumen.  
```java
import com.aspose.pdf.facades.PdfContentEditor;
import com.aspose.pdf.facades.ViewerPreference;

PdfContentEditor editor = new PdfContentEditor();
editor.bindPdf("YOUR_DOCUMENT_DIRECTORY/input.pdf");
```
#### Mengubah Preferensi Penampil
Untuk mengaktifkan **single page view pdf**, panggil `changeViewerPreference()` dengan nilai enum yang sesuai. Panggilan ini memperbarui kamus preferensi penampil internal PDF.  
```java
editor.changeViewerPreference(ViewerPreference.PAGE_LAYOUT_SINGLE_PAGE);
```
#### Menyimpan Dokumen yang Diperbarui
Setelah memodifikasi preferensi, panggil `save()` untuk menulis perubahan kembali ke disk.  
```java
String outputDir = "YOUR_OUTPUT_DIRECTORY/settingViewerPreferences.pdf";
editor.save(outputDir);
```

## Cara Mengedit Penanda Buku PDF
**Jawaban**: Untuk memodifikasi penanda buku yang ada, muat PDF dengan `Document`, ambil koleksi outline‑nya, temukan `OutlineItem` yang diinginkan, dan tetapkan `ExplicitDestination` baru yang mengarah ke halaman dan koordinat yang tepat. Setelah memperbarui setiap penanda buku, simpan dokumen untuk mempertahankan perubahan. Ini memastikan pengguna diarahkan secara tepat ke bagian yang dimaksud tanpa gulir tambahan.

#### Mengakses Penanda Buku
`OutlineItemCollection` mewakili pohon penanda buku hierarkis. Ambil dari objek `Document` untuk bekerja dengan entri individual.  
```java
import com.aspose.pdf.Document;
import com.aspose.pdf.ExplicitDestination;
import com.aspose.pdf.OutlineItemCollection;

Document pdfDocument = new Document("YOUR_DOCUMENT_DIRECTORY/input.pdf");
OutlineItemCollection pdfOutline = pdfDocument.getOutlines().get_Item(1);
```
#### Menetapkan Tujuan Baru
`ExplicitDestination` mendefinisikan halaman dan lokasi tepat yang harus dilompat oleh penanda buku. Tetapkan ke properti `Destination` dari item outline.  
```java
pdfOutline.setDestination(
    ExplicitDestination.createDestination(pdfDocument.getPages().get_Item(1),
        ExplicitDestinationType.FitH,
        pdfDocument.getPages().get_Item(1).getMediaBox().getHeight())
);
```
#### Menyimpan Perubahan
Persist pohon penanda buku yang diperbarui dengan memanggil `document.save()`.  
```java
String outputDir = "YOUR_OUTPUT_DIRECTORY/bookmarkShouldPointToStartOfPage.pdf";
pdfDocument.save(outputDir);
```

## Cara Menetapkan Tujuan Penanda Buku Saat Membuat PDF
**Jawaban**: Saat menghasilkan PDF, Anda dapat membuat penanda buku secara dinamis dengan menginstansiasi objek `OutlineItem`, mengatur judulnya, dan mendefinisikan `ExplicitDestination` yang menargetkan halaman dan mode tampilan tertentu. Tambahkan setiap penanda buku ke koleksi outline dokumen sebelum menyimpan, sehingga file yang dihasilkan berisi pohon navigasi siap pakai.

#### Membuat dan Mengonfigurasi Penanda Buku
`OutlineItem` mewakili satu entri penanda buku dalam outline PDF. Saat membangun PDF dari awal, buat instance `OutlineItem` baru dan tambahkan ke koleksi outline dokumen.  
```java
import com.aspose.pdf.GoToAction;
import com.aspose.pdf.FitVExplicitDestination;

OutlineItemCollection pdfOutline_new = new OutlineItemCollection(pdfDocument.getOutlines());
pdfOutline_new.setTitle("Test Bookmark");
pdfOutline_new.setItalic(true);
pdfOutline_new.setBold(true);
```
#### Mendefinisikan Tujuan Penanda Buku
Gunakan `ExplicitDestination.createFitH(page, top)` untuk memposisikan tampilan di bagian atas halaman target.  
```java
pdfOutline_new.setAction(new GoToAction(
    new FitVExplicitDestination(pdfDocument.getPages().get_Item(2), 0)));
```
#### Menambahkan dan Menyimpan PDF
Akhirnya, tambahkan penanda buku ke outline dan simpan dokumen.  
```java
pdfDocument.getOutlines().add(pdfOutline_new);

String outputDir = "YOUR_OUTPUT_DIRECTORY/setDestinationWhileCreatingPDF.pdf";
pdfDocument.save(outputDir);
```

## Aplikasi Praktis
1. **Buku Digital** – Pastikan setiap penanda bab berada di bagian atas halaman untuk pengalaman membaca yang mulus.  
2. **Manual Teknis** – Navigasi yang tepat membantu insinyur menemukan bagian dengan cepat, terutama dalam PDF besar.  
3. **Katalog Produk** – Tata letak satu halaman membuat penelusuran katalog di tablet lebih intuitif.

## Pertimbangan Kinerja
- **Optimizing Resources**: Aspose.PDF dapat memproses PDF hingga 2 GB tanpa memuat seluruh file ke memori, berkat arsitektur streaming‑nya. Gunakan `Document.optimizeResources()` untuk lebih mengurangi jejak memori.  
- **Java Memory Management**: Tutup stream secara eksplisit dan biarkan garbage collector membersihkan objek setelah pemrosesan untuk menghindari kebocoran memori.

## Masalah Umum & Solusi
- **Bookmarks Not Updating**: Verifikasi bahwa Anda memodifikasi indeks outline yang tepat (`get_Item(1)` mengacu pada penanda buku tingkat atas pertama).  
- **Viewer Preference Not Applied**: Pastikan Anda memanggil `editor.save()` setelah mengubah preferensi; jika tidak, perubahan hanya tetap di memori.  
- **License Exceptions**: Lisensi percobaan dapat menambahkan watermark; dapatkan lisensi penuh untuk produksi.

## Pertanyaan yang Sering Diajukan
**Q: Apa cara termudah untuk memuat dokumen PDF di Java?**  
**A:** Gunakan `new Document("path/to/file.pdf")`; Aspose.PDF secara otomatis mendeteksi format file.

**Q: Apakah saya dapat mengubah tata letak halaman tanpa menggunakan PdfContentEditor?**  
**A:** Ya, Anda dapat mengatur preferensi penampil langsung pada objek `Document` melalui `pdfDocument.getViewerPreferences().setPageLayout(...)`.

**Q: Apakah mengubah tata letak penampil memengaruhi pencetakan?**  
**A:** Tata letak penampil hanya memengaruhi tampilan di layar; tidak mengubah output cetak.

**Q: Apakah ada batasan jumlah penanda buku yang dapat saya buat?**  
**A:** Tidak ada batas eksplisit, namun pohon outline yang sangat besar dapat memengaruhi kinerja; tetaplah mengatur dengan rapi.

**Q: Bagaimana cara memastikan tujuan penanda buku akurat setelah menambah atau menghapus halaman?**  
**A:** Hitung ulang tujuan menggunakan indeks halaman saat ini setelah setiap perubahan struktural.

## Sumber Daya
- **Dokumentasi**: [Referensi Aspose.PDF Java](https://reference.aspose.com/pdf/java/)
- **Unduhan**: [Rilis Terbaru untuk Java](https://releases.aspose.com/pdf/java/)
- **Pembelian**: [Beli Lisensi Aspose.PDF](https://purchase.aspose.com/buy)
- **Percobaan Gratis**: [Coba Aspose.PDF Gratis](https://releases.aspose.com/pdf/java/)
- **Lisensi Sementara**: [Minta Lisensi Sementara](https://purchase.aspose.com/temporary-license)

---

**Last Updated:** 2026-05-28  
**Tested With:** Aspose.PDF for Java v25.3  
**Author:** Aspose

## Tutorial Terkait

- [Cara Mengubah Preferensi Penampil PDF Menggunakan Aspose.PDF untuk Java: Panduan Komprehensif](/pdf/java/printing-rendering/modify-pdf-viewer-preferences-aspose-pdf-java/)
- [Cara Membuat Penanda Buku PDF dan Mengelola Navigasi Menggunakan Aspose.PDF untuk Java](/pdf/java/bookmarks-navigation/create-manage-pdf-bookmarks-aspose-java/)
- [Tutorial Penanda Buku PDF dan Navigasi untuk Aspose.PDF Java](/pdf/java/bookmarks-navigation/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}