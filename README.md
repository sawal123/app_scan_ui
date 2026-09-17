# Ticket Scanner — Static UI Prototype

High-fidelity static frontend untuk aplikasi operasional check-in QR Ticket Event.

## Menjalankan

Tidak ada build process atau dependency lokal.

1. Buka `login.html` langsung di browser, atau jalankan static server sederhana dari folder `/app`.
2. Isi email/username dan password apa saja untuk masuk. Gunakan password `salah` untuk melihat contoh error login.
3. Browser memerlukan secure context (`https` atau `localhost`) agar kamera sungguhan dapat diaktifkan.

Contoh static server lokal:

```bash
python3 -m http.server 8080 --directory /app
```

Lalu buka `http://localhost:8080/login.html`.

## Demo QR

- `VIP-001` — tiket VIP valid
- `REG-001` — tiket Regular valid
- `VIP-USED-001` — tiket sudah pernah digunakan
- Kode lainnya — tiket tidak ditemukan

Pada mode **Scanner Device**, ketik kode lalu tekan Enter. Data tiket yang dikonfirmasi serta preferensi tema tersimpan di `localStorage`.

## Struktur

```text
/app
├── login.html
├── scanner.html
├── verified.html
└── assets
    ├── css/styles.css
    └── js/app.js
```

HTML disusun secara semantik agar mudah dipindahkan menjadi Laravel Blade components dan perilaku JavaScript dapat diadaptasi ke Alpine.js.