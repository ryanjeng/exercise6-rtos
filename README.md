# **Eliminasi Kontensi Sumber Daya dengan Menangguhkan Scheduler**

## **Deskripsi**
Repositori ini berisi implementasi dari *Exercise 6 – Demonstrate a Simple Way to Eliminate Resource Contention by Suspending the Scheduler*. Latihan ini menunjukkan cara sederhana untuk menghilangkan masalah kontensi sumber daya bersama dengan menangguhkan scheduler menggunakan fungsi bawaan FreeRTOS. Pendekatan ini memastikan bahwa hanya satu tugas yang dapat mengakses sumber daya bersama pada satu waktu, sehingga mencegah interferensi.

---

## **Konsep Utama**
- **Menangguhkan Scheduler**:
  - Digunakan untuk mencegah akses simultan ke sumber daya bersama selama eksekusi kode kritis.
  - Dilakukan dengan menonaktifkan *interrupt* saat tugas mengakses sumber daya dan mengaktifkannya kembali setelah selesai.
- **Keuntungan**:
  - Teknik ini sederhana dan menjamin keamanan akses sumber daya.
- **Kekurangan**:
  - Menonaktifkan *interrupt* menghentikan sementara eksekusi tugas lain, yang dapat memengaruhi responsivitas sistem.
  - Penting untuk meminimalkan durasi penangguhan scheduler.

---

## **Implementasi**
### **Modifikasi pada Tugas**
1. **Task 1 (FlashGreenLedTask)**:
   - Menyalakan LED hijau.
   - Menonaktifkan *interrupt* menggunakan `taskENTER_CRITICAL()`.
   - Mengakses sumber daya bersama.
   - Mengaktifkan kembali *interrupt* menggunakan `taskEXIT_CRITICAL()`.
   - Mematikan LED hijau.
   - *Delay* selama 0,5 detik.

2. **Task 2 (FlashRedLedTask)**:
   - Menyalakan LED merah.
   - Menonaktifkan *interrupt* menggunakan `taskENTER_CRITICAL()`.
   - Mengakses sumber daya bersama.
   - Mengaktifkan kembali *interrupt* menggunakan `taskEXIT_CRITICAL()`.
   - Mematikan LED merah.
   - *Delay* selama 0,1 detik.

3. **Akses Sumber Daya Bersama**:
   - Seluruh proses dilakukan di dalam blok kritis (antara `taskENTER_CRITICAL()` dan `taskEXIT_CRITICAL()`).
   - Mencegah kontensi sumber daya dengan memastikan hanya satu tugas yang dapat mengakses sumber daya pada satu waktu.

---

## **Langkah Penggunaan**
1. **Persiapkan Hardware**:
   - Mikrokontroler dengan dukungan FreeRTOS.
   - Sambungkan LED hijau, merah, dan biru ke pin yang sesuai.

2. **Implementasi dan Uji Coba**:
   - Modifikasi kode dari latihan sebelumnya dengan menambahkan `taskENTER_CRITICAL()` dan `taskEXIT_CRITICAL()` di sekitar akses sumber daya.
   - Jalankan tugas satu per satu untuk memastikan kode bekerja dengan benar.
   - Jalankan kedua tugas secara bersamaan dan pastikan LED biru tidak menyala, yang menandakan tidak ada kontensi sumber daya.

3. **Optimalisasi Waktu**:
   - Pastikan kode di dalam blok kritis (antara `taskENTER_CRITICAL()` dan `taskEXIT_CRITICAL()`) seminimal mungkin untuk mengurangi dampak penangguhan scheduler.

---

## **Demonstrasi**
![Exercise6](https://github.com/user-attachments/assets/40821d97-b057-4a23-a4c7-882c69fe3652)


---

## **Pelajaran yang Didapat**
- **Mekanisme Penangguhan Scheduler**:
  - Menonaktifkan *interrupt* memastikan keamanan akses pada kode kritis.
  - Teknik ini sederhana dan mudah diimplementasikan.
- **Dampak Penangguhan Scheduler**:
  - Menonaktifkan *interrupt* menghentikan multitasking sementara.
  - Waktu eksekusi di dalam blok kritis harus diminimalkan.
- **Pentingnya Proteksi Sumber Daya**:
  - Proteksi yang tepat sangat penting untuk menghindari masalah dalam sistem multitasking.

---

## **Persyaratan Sistem**
- Mikrokontroler yang mendukung FreeRTOS.
- IDE untuk pengembangan firmware (misalnya STM32CubeIDE).
- Hardware tambahan: LED hijau, merah, dan biru.

---

Dengan memahami dan menerapkan teknik ini, Anda dapat mengelola akses sumber daya bersama secara aman dalam sistem multitasking.
