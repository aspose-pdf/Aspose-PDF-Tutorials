---
"date": "2025-04-14"
"description": "Pelajari cara memberi anotasi pada file PDF di Java menggunakan Aspose.PDF dengan menambahkan anotasi coretan. Ikuti panduan ini untuk petunjuk langkah demi langkah tentang cara memodifikasi konten PDF."
"title": "Cara Membuat Anotasi pada PDF di Java dengan Anotasi Strike-Out Menggunakan Aspose.PDF"
"url": "/id/java/forms-annotations/annotate-pdfs-java-strikeout-aspose-pdf/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}
# Cara Membuat Anotasi pada PDF di Java dengan Anotasi Strike-Out Menggunakan Aspose.PDF

Manfaatkan sepenuhnya potensi manipulasi PDF menggunakan Aspose.PDF untuk Java dengan mempelajari cara memberi anotasi dan menyimpan file PDF dengan anotasi coretan. Panduan komprehensif ini akan memandu Anda dalam menginisialisasi dokumen, mencari fragmen teks, membuat anotasi, dan menyimpan dokumen yang diberi anotasi.

## Perkenalan

Menjelajahi PDF yang rumit bisa jadi menantang, baik itu mengekstrak data atau memodifikasi konten. Jika Anda ingin menambahkan anotasi visual seperti coretan langsung di dalam aplikasi Java Anda menggunakan Aspose.PDF untuk Java, panduan ini sangatlah tepat. Anda akan mempelajari cara mengintegrasikan fungsionalitas PDF dengan lancar ke dalam proyek Anda.

### Apa yang Akan Anda Pelajari
- Cara menginisialisasi dan memuat dokumen PDF dengan Aspose.PDF
- Teknik untuk mencari fragmen teks tertentu dalam PDF
- Langkah-langkah untuk membuat dan mengonfigurasi anotasi coretan
- Metode untuk menyimpan dokumen PDF yang dimodifikasi

Mari kita bahas prasyarat yang Anda perlukan sebelum memulai.

## Prasyarat

### Pustaka, Versi, dan Ketergantungan yang Diperlukan
Untuk mengikuti tutorial ini, pastikan Anda memiliki:
- Java Development Kit (JDK) 8 atau yang lebih baru terpasang.
- IDE seperti IntelliJ IDEA atau Eclipse untuk mengedit kode Java Anda.

Kami akan menggunakan Aspose.PDF untuk Java versi 25.3. Anda dapat menggabungkannya ke dalam proyek Anda melalui Maven atau Gradle seperti yang ditunjukkan di bawah ini.

### Persyaratan Pengaturan Lingkungan
Pastikan lingkungan Anda diatur untuk menangani dependensi dan Anda memiliki akses ke direktori tempat dokumen PDF masukan Anda disimpan, beserta direktori keluaran untuk menyimpan file yang diberi anotasi.

### Prasyarat Pengetahuan
Kemampuan dalam pemrograman Java dan pemahaman dasar dalam penanganan PDF secara terprogram akan bermanfaat.

## Menyiapkan Aspose.PDF untuk Java
Mengintegrasikan Aspose.PDF ke dalam proyek Java Anda mudah saja. Berikut cara menambahkannya menggunakan Maven atau Gradle:

**Pakar**
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-pdf</artifactId>
    <version>25.3</version>
</dependency>
```

**Bahasa Inggris Gradle**
```gradle
implementation 'com.aspose:aspose-pdf:25.3'
```

### Akuisisi Lisensi
Aspose.PDF adalah pustaka komersial, tetapi Anda dapat memulai dengan mendapatkan uji coba gratis atau lisensi sementara untuk tujuan evaluasi. Kunjungi [Halaman pembelian Aspose](https://purchase.aspose.com/buy) untuk mengeksplorasi pilihan Anda.

## Panduan Implementasi
Kami akan membagi implementasi kami menjadi beberapa bagian berdasarkan fungsionalitas: inisialisasi dokumen, pencarian fragmen teks, pembuatan anotasi, dan penyimpanan dokumen.

### Inisialisasi dan Pemuatan Dokumen
#### Ringkasan
Pertama, kita perlu memuat file PDF menggunakan Aspose.PDF untuk Java. Langkah ini melibatkan inisialisasi `Document` kelas dengan jalur ke PDF Anda.

**Langkah 1**Impor kelas yang diperlukan.
```java
import com.aspose.pdf.Document;
```

**Langkah 2**: Tentukan direktori dokumen Anda dan inisialisasi objek Dokumen.
```java
String dataDir = "YOUR_DOCUMENT_DIRECTORY";
Document document = new Document(dataDir + "/input.pdf");
```
Kode ini memuat PDF dari `dataDir` ke dalam `Document` misalnya, yang memungkinkan operasi lebih lanjut.

### Penyerapan Fragmen Teks
#### Ringkasan
Mencari teks dalam PDF Anda sangat penting sebelum membuat anotasi. Kami akan menggunakan `TextFragmentAbsorber`.

**Langkah 1**: Impor kelas.
```java
import com.aspose.pdf.TextFragmentAbsorber;
```

**Langkah 2**: Buat contoh TextFragmentAbsorber dengan kueri penelusuran.
```java
TextFragmentAbsorber textFragmentAbsorber = new TextFragmentAbsorber("Sample");
```

**Langkah 3**: Terima penyerap pada setiap halaman untuk menemukan semua fragmen teks yang cocok.
```java
for (int i = 1; i <= document.getPages().size(); i++) {
    document.getPages().get_Item(i).accept(textFragmentAbsorber);
}
```
Putaran ini menelusuri setiap halaman, mengumpulkan kecocokan untuk "Sampel".

### Ambil Koleksi Fragmen Teks
#### Ringkasan
Setelah fragmen teks diserap, kami mengambilnya dalam koleksi untuk memproses anotasi.

**Langkah 1**: Impor kelas yang diperlukan.
```java
import com.aspose.pdf.TextFragmentCollection;
```

**Langkah 2**: Ambil koleksi dari penyerap.
```java
TextFragmentCollection textFragmentCollection = textFragmentAbsorber.getTextFragments();
```
Ini memberi kita akses ke semua contoh "Sampel" yang ditemukan.

### Buat Anotasi Coretan
#### Ringkasan
Kami akan menambahkan anotasi coretan pada setiap fragmen teks yang teridentifikasi, menyorot atau menandainya secara visual.

**Langkah 1**Impor kelas yang diperlukan.
```java
import com.aspose.pdf.StrikeOutAnnotation;
import com.aspose.pdf.Rectangle;
import com.aspose.pdf.Border;
import com.aspose.pdf.Color;
import com.aspose.pdf.Page;
```

**Langkah 2**: Ulangi fragmen teks dan buat anotasi.
```java
for (int j = 1; j <= textFragmentCollection.size(); j++) {
    com.aspose.pdf.TextFragment textFragment = textFragmentCollection.get_Item(j);

    // Tentukan area persegi panjang untuk anotasi berdasarkan lokasi fragmen teks.
    Rectangle rect = new Rectangle((float) textFragment.getPosition().getXIndent(),
                                   (float) textFragment.getPosition().getYIndent(),
                                   (float) textFragment.getPosition().getXIndent() + (float) textFragment.getRectangle().getWidth(),
                                   (float) textFragment.getPosition().getYIndent() + (float) textFragment.getRectangle().getHeight());

    // Buat dan konfigurasikan anotasi coretan.
    StrikeOutAnnotation strikeOut = new StrikeOutAnnotation(textFragment.getPage(), rect);
    strikeOut.setOpacity(0.80f);  // Atur opasitas menjadi 80%
    strikeOut.setBorder(new Border(strikeOut));  // Inisialisasi batas untuk anotasi
    strikeOut.setColor(Color.getRed());  // Atur warna anotasi menjadi merah

    // Tambahkan anotasi ke halaman.
    textFragment.getPage().getAnnotations().add(strikeOut);
}
```
Setiap anotasi dikonfigurasikan dengan pengaturan opasitas, batas, dan warna sebelum ditambahkan.

### Simpan Dokumen dengan Anotasi
#### Ringkasan
Setelah membuat anotasi, kita simpan dokumen yang diberi anotasi.

**Langkah 1**: Impor kelas yang diperlukan jika belum dilakukan.
```java
import com.aspose.pdf.Document;
```

**Langkah 2**: Tentukan direktori keluaran dan simpan dokumen.
```java
String outputDir = "YOUR_OUTPUT_DIRECTORY";
document.save(outputDir + "/StrikeOut.pdf");
```
Langkah ini menyelesaikan PDF Anda yang diberi anotasi dengan semua modifikasi utuh.

## Aplikasi Praktis
Aspose.PDF untuk Java dapat digunakan dalam berbagai skenario, seperti:
1. **Proses Peninjauan Dokumen**Otomatisasi proses peninjauan dengan menandai perubahan yang diperlukan secara terprogram.
2. **Penanganan Dokumen Hukum**: Segera beri anotasi pada kontrak atau perjanjian dengan penyuntingan atau pengeditan seperlunya.
3. **Pembuatan Konten Pendidikan**: Tingkatkan materi pembelajaran dengan mencoret informasi yang ketinggalan zaman dan memberi anotasi pada koreksi.

## Pertimbangan Kinerja
Untuk memastikan kinerja yang optimal:
- Gunakan struktur data yang efisien saat menangani kumpulan besar fragmen teks.
- Kelola memori secara efektif, terutama di lingkungan dengan sumber daya terbatas.
- Perbarui secara berkala ke versi Aspose.PDF terbaru untuk mendapatkan fitur dan perbaikan yang lebih baik.

## Kesimpulan
Anda telah berhasil mempelajari cara menggunakan Aspose.PDF untuk Java untuk memberi anotasi pada PDF dengan garis coretan. Dengan mengikuti panduan ini, Anda telah mengambil langkah signifikan menuju otomatisasi proses penanganan PDF. Jelajahi lebih jauh dengan bereksperimen dengan jenis anotasi lain atau mengintegrasikan fungsi tambahan dari pustaka Aspose.

Siap untuk melangkah lebih jauh? Kunjungi [Dokumentasi Aspose](https://reference.aspose.com/pdf/java/) untuk fitur dan kemampuan yang lebih canggih.

## Bagian FAQ
**1. Bagaimana cara menginstal Aspose.PDF di proyek Java saya?**
Anda dapat menambahkannya melalui dependensi Maven atau Gradle seperti yang ditunjukkan dalam tutorial ini. Pastikan IDE Anda dikonfigurasi untuk mengenali pengaturan ini.

**2. Dapatkah saya memberi anotasi pada PDF selain dengan coretan menggunakan Aspose.PDF untuk Java?**
Ya, Anda dapat membuat berbagai anotasi seperti sorotan, garis bawah, dan banyak lagi.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}