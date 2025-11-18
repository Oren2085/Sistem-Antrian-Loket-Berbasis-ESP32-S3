# Sistem Antrian Loket Berbasis ESP32-S3
Proyek ini mensimulasikan sistem antrian sederhana untuk loket pelayanan, menggunakan **ESP32-S3**, **rotary encoder**, **OLED**, **LED indikator**, dan **buzzer**.  
Sistem bekerja dengan membuka/menutup loket menggunakan rotary encoder, serta memanggil nomor antrian menggunakan tombol encoder.

Simulasi ini berjalan di **Wokwi** dan dapat diterapkan pada perangkat asli (ESP32-S3).

---

## Tujuan Sistem
- Membangun sistem antrian loket otomatis sederhana.
- Menampilkan nomor antrian pada layar OLED secara real-time.
- Memanggil nomor antrian menggunakan tombol.
- Menampilkan status loket (BUKA / TUTUP) dengan LED.
- Memberikan efek audio (buzzer) dan visual (LED kuning) saat memanggil nomor.

---

## Cara Kerja Sistem
### 1. **Rotary Encoder → Membuka / Menutup Loket**
- Ketika encoder diputar, status loket akan berubah:
  - **BUKA → TUTUP**
  - **TUTUP → BUKA**
- Sistem memberikan feedback berupa:
  - Bunyi beep pendek
  - Log di Serial Monitor

### 2. **Tombol Encoder → Panggil Nomor Antrian**
- Hanya bisa digunakan jika loket **BUKA**.
- Setiap tekan:
  - `lastNumber++`
  - `currentNumber` diperbarui
  - Animasi panggilan berjalan (LED + buzzer)

### 3. **OLED Display**
Menampilkan informasi:
- Status loket (BUKA / TUTUP)
- Nomor yang sedang dipanggil (Now)
- Nomor terakhir (Last)

### 4. **LED Indikator Status Loket**
- **Hijau** → Loket BUKA  
- **Merah** → Loket TUTUP  
- **Kuning** → Hanya menyala saat panggil nomor  

---

# Tugas Komponen / Fungsi Sistem
| Bagian | Fungsi | Detail |
|--------|--------|--------|
| Rotary Encoder | Toggle loket BUKA/TUTUP | Berubah setiap putaran |
| Tombol Encoder (SW) | Memanggil nomor | Hanya aktif di mode BUKA |
| OLED 128x64 | Menampilkan status & nomor | Update setiap loop |
| LED Hijau | Loket BUKA | Menyala penuh |
| LED Merah | Loket TUTUP | Menyala penuh |
| LED Kuning | Efek panggilan | Berkedip 4x |
| Buzzer | Notifikasi audio | Beep saat panggil & toggle |
| LED Pintu | Pengganti servo | Berkedip saat panggil nomor |

---

# Pemetaan Pin ESP32-S3
| Perangkat | Pin ESP32 | Fungsi |
|----------|-----------|--------|
| LED Hijau | GPIO 1 | Indikator loket buka |
| LED Kuning | GPIO 3 | Efek panggilan antrian |
| LED Merah | GPIO 2 | Loket tutup |
| Buzzer | GPIO 4 | Panggilan / Warning |
| LED Pintu | GPIO 15 | Indikator pintu (dummy servo) |
| Rotary CLK | GPIO 6 | Encoder A |
| Rotary DT | GPIO 7 | Encoder B |
| Rotary SW | GPIO 8 | Tombol encoder |
| OLED SDA | GPIO 38 | I2C SDA |
| OLED SCL | GPIO 39 | I2C SCL |

---

# Langkah Percobaan / Pengujian (Simulasi Wokwi)

| No | Langkah Percobaan | Hasil yang Diharapkan |
|----|-------------------|------------------------|
| 1 | Jalankan simulasi di Wokwi | OLED menampilkan “Loket TUTUP” dan LED merah menyala |
| 2 | Putar rotary encoder | Loket toggle BUKA/TUTUP, buzzer beep singkat |
| 3 | Cek LED Indikator | Hijau = Buka, Merah = Tutup |
| 4 | Tekan tombol encoder SW | Jika TUTUP → buzzer warning, nomor tidak bertambah |
| 5 | Buka loket lalu tekan SW | Nomor antrian bertambah + animasi LED kuning & buzzer |
| 6 | Amati OLED | Informasi Now & Last update otomatis |
| 7 | Tekan beberapa kali SW | Nomor antrian naik bertahap (1,2,3,...) |
| 8 | Tutup loket | LED merah menyala, pemanggilan dinonaktifkan |
| 9 | Buka kembali loket | Tetap dapat memanggil nomor selanjutnya |

---

# Tampilan OLED
Informasi pada layar:

Loket: BUKA
Now: 3
Last: 3

Atau jika tutup:

Loket: TUTUP
Now: 0
Last: 0

---

# Animasi Pemanggilan Nomor
Saat tombol ditekan dalam kondisi loket buka:

- LED Kuning berkedip cepat 4x  
- LED Pintu ikut berkedip  
- Buzzer berbunyi beep-beep  
- OLED tetap update nomor terbaru
  
---

# Simulasi Wiring
Wokwi:https://wokwi.com/projects/4478364310176
Rangkaian: <img width="1170" height="789" alt="image" src="https://github.com/user-attachments/assets/d52e2dbd-2779-4d76-af0f-041f395e9f95" />



---

# Author
**Muhammad Irsyad Alkais** 
**Ghori Ghuraishi Mulyadi**
Computer Engineering Student – PENS  
IoT • Embedded Systems • ESP32 • Wokwi Simulation
