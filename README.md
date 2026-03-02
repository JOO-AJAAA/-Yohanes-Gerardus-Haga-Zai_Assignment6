# Analisis Spasial Area Potensial dan Berisiko di Kota Medan

Analisis ini bertujuan untuk mengidentifikasi area-area di Kota Medan yang memiliki potensi untuk dikunjungi (area rekomendasi) dan area yang memiliki risiko bencana (area berisiko) bagi wisatawan maupun penduduk lokal.

### Nama Analis

- **Yohanes Gerardus Haga Zai**

### Tema Analisis

- Area/daerah rekomendasi dan berisiko bagi wisatawan ataupun penduduk lokal di Kota Medan.

---

### Daftar File

- `Task 6 Spatial Analytics Python.ipynb`: Notebook utama yang berisi semua proses analisis, mulai dari pengambilan data, pemrosesan, hingga visualisasi.
- `area administratif kota medan.geojson`: Data GeoJSON yang berisi batas administratif per kecamatan di Kota Medan.
- `area_potensialMedan.geojson`: Hasil analisis berupa data GeoJSON yang menandai area-area potensial.
- `area_risikoMedan.geojson`: Hasil analisis berupa data GeoJSON yang menandai area-area berisiko.
- `README.md`: File ini.

---

### Pustaka yang Digunakan

Untuk menjalankan notebook ini, Anda memerlukan pustaka Python berikut:

- `requests`
- `folium`
- `geopandas`
- `shapely`
- `pyproj`
- `matplotlib`
- `branca`
- `json`
- `os`

Anda dapat menginstalnya menggunakan pip:

```bash
pip install requests folium geopandas shapely pyproj matplotlib branca
```

---

### Sumber Data

Analisis ini menggunakan beberapa sumber data spasial:

1.  **Data Lokal**:
    - `area administratif kota medan.geojson`: Batas wilayah administratif Kota Medan.

2.  **Data Eksternal (API)**:
    Data diambil dari API publik yang variabelnya disimpan sebagai _environment variables_. Variabel-variabel yang digunakan antara lain:
    - Wilayah terancam tsunami
    - Wilayah risiko banjir
    - Restoran
    - Makanan dan minuman
    - Fasilitas olahraga
    - Area Lapangan
    - Wisata alam
    - Pariwisata

---

### Langkah-langkah Analisis

1.  **Impor Pustaka**: Mengimpor semua pustaka yang diperlukan untuk analisis.
2.  **Pengambilan Data**: Membaca data GeoJSON dari file lokal dan mengambil data dari berbagai endpoint API.
3.  **Pembersihan dan Penyesuaian Data**:
    - Mengisi nilai yang hilang (_null_).
    - Menyesuaikan Sistem Referensi Koordinat (CRS) ke `EPSG:4326`.
    - Melakukan _buffering_ pada data titik (Point) untuk mengubahnya menjadi poligon.
4.  **Analisis Terpisah**: Karena tidak ada irisan langsung antara data area berisiko dan area potensial, analisis dilakukan secara terpisah.
    - **Analisis Area Risiko**:
      - Melakukan _overlay_ (intersect) pada data wilayah rawan banjir dan tsunami.
      - Memberikan skor risiko berdasarkan tingkat bahaya.
      - Membuat visualisasi peta area berisiko dengan `folium`.
      - Menyimpan hasilnya ke `area_risikoMedan.geojson`.
    - **Analisis Area Potensial**:
      - Melakukan _overlay_ pada data pariwisata, fasilitas, kuliner, dan wisata alam.
      - Memberikan skor potensi berdasarkan kelengkapan dan jenis fasilitas.
      - Membuat visualisasi peta area potensial dengan `folium`.
      - Menyimpan hasilnya ke `area_potensialMedan.geojson`.

---

### Cara Menjalankan

1.  Pastikan semua pustaka yang diperlukan telah terinstal.
2.  Siapkan _environment variables_ untuk mengakses data dari API sesuai dengan yang didefinisikan di dalam notebook.
3.  Buka dan jalankan sel-sel di dalam file `Task 6 Spatial Analytics Python.ipynb` secara berurutan.

### Hasil

Analisis ini menghasilkan dua file output utama:

- `area_potensialMedan.geojson`: Berisi poligon area-area yang direkomendasikan, diklasifikasikan sebagai 'Berpotensi', 'Sedang', atau 'Tidak berpotensi'.
- `area_risikoMedan.geojson`: Berisi poligon area-area berisiko, diklasifikasikan sebagai 'Tinggi', 'Sedang', atau 'Rendah'.
