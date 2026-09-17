# PRD — Ticket Scanner Event Check-in

## Original Problem Statement

Membangun frontend high-fidelity untuk aplikasi Scanner QR Ticket Event yang digunakan petugas gate. Deliverable harus berupa static HTML, CSS, dan vanilla JavaScript tanpa backend, database, API sungguhan, framework frontend, atau build process. Prototype wajib mobile-first, mudah dipindahkan ke Laravel Blade + Alpine.js, mendukung kamera browser dan hardware scanner, seluruh status tiket, daftar tiket terverifikasi, light/dark theme, accessibility, responsive behavior, serta microinteraction operasional yang cepat.

## User Decisions

- Lokasi project: root `/app`.
- Simulasi kamera: kamera browser sungguhan + tombol demo QR.
- Login sukses: menuju `scanner.html`.
- Data tiket terverifikasi: disimpan menggunakan `localStorage`.

## Architecture Decisions

- Multi-page static frontend: `login.html`, `scanner.html`, dan `verified.html`.
- Shared styling dan behavior melalui `assets/css/styles.css` dan `assets/js/app.js`.
- Semantic HTML dengan section yang dapat dipindahkan menjadi Blade layout/components.
- State prototype, theme, dan verified records menggunakan vanilla JavaScript + `localStorage`.
- Lucide Icons dan Manrope dimuat via CDN; tidak ada dependency build-time.
- Kamera menggunakan `navigator.mediaDevices.getUserMedia`; fallback tetap memungkinkan demo QR dan hardware input.
- Semua elemen interaktif dan informasi penting memiliki `data-testid` unik.

## User Personas

1. **Petugas Gate** — memindai tiket berulang kali melalui smartphone/tablet dan membutuhkan hasil yang dapat dipahami dalam kurang dari satu detik.
2. **Koordinator Gate** — memantau tiket yang sudah masuk dan mencari kode QR tertentu.
3. **Developer Laravel** — memindahkan struktur statis menjadi Blade components dan behavior ke Alpine.js.

## Core Requirements (Static)

- Login operator dengan validasi, loading, error, dan show/hide password.
- Scanner camera/device, manual input, dan demo QR.
- Status: idle, camera/device ready, validating, valid, success, already used, invalid, dan offline.
- Konfirmasi masuk dengan loading dan pencegahan double action.
- Verified list, search, category filters, populated state, dan empty state.
- Theme light/dark persisten, toast reusable, responsive mobile-first, keyboard support, focus states, dan reduced motion.

## Implemented — 2026-09-17

- [x] Tiga halaman static high-fidelity lengkap dengan shared design system.
- [x] Login demo, theme persistence, kamera browser, hardware scanner input, manual QR modal, result bottom sheet, toast, dan connection simulation.
- [x] Demo data `VIP-001`, `REG-001`, `VIP-USED-001`, serta fallback invalid QR.
- [x] Verified ticket persistence, search/filter, empty/restore state, dan responsive desktop/mobile presentation.
- [x] Accessibility labels, keyboard interactions, `data-testid`, safe-area support, dan reduced-motion behavior.
- [x] Idempotent confirmation lock untuk mencegah aksi ganda paksa.
- [x] QA frontend seluruh flow; tidak ada horizontal overflow pada 1920×800 dan 390×844.

## Prioritized Backlog

### P0 — Laravel Integration

- Pecah shell, header, bottom navigation, scanner stage, result sheet, modal, dan toast menjadi Blade components.
- Pindahkan state interaksi vanilla JavaScript ke Alpine.js stores/components.
- Hubungkan validasi tiket dan check-in ke endpoint Laravel dengan idempotency key server-side.
- Integrasikan autentikasi operator dan permission gate.

### P1 — Operational Readiness

- Tambahkan engine pembaca QR kamera yang teruji dan lifecycle permission camera.
- Tambahkan retry queue/offline-safe strategy untuk check-in dengan status sinkronisasi jelas.
- Gunakan event/gate/scanner configuration dari server.
- Tambahkan audit trail operasional tanpa data personal pengunjung.

### P2 — Enhancements

- Tambahkan haptic/audio feedback opsional untuk status sukses, warning, dan invalid.
- Tambahkan mode kepadatan tinggi khusus tablet/laptop kecil.
- Tambahkan metrik sederhana kecepatan scan dan jumlah check-in per gate.

## Next Tasks

1. Mapping markup static ke struktur `resources/views` Laravel.
2. Definisikan kontrak API validate/check-in/list verified.
3. Implementasikan Alpine.js state machine berdasarkan prototype.
4. Uji perangkat nyata: iOS Safari, Android Chrome, tablet, dan hardware scanner USB/Bluetooth.