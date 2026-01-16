# connection-mikrotik-project

1. tujuan ini dibuat adalah untuk mempermmudah pengguna untuk melakukan monitoring dan sudah dilengkapi dengan detecton logs

   [h1] Tujuan untuk ini dibuat :

    Monitoring aktivitas jaringan MikroTik

    Mendeteksi trafik/aktivitas mencurigakan

    Melakukan auto‑block IP / client ke MikroTik

    Menyediakan API untuk frontend (nanti)

   
# alur : 

2️⃣ Aktor Sistem

    Admin

        Melihat log & status jaringan

        Mengatur rule / threshold

        Manual block / unblock

    System (Backend Service)

        Menarik data dari MikroTik

        Analisis trafik

        Eksekusi auto‑block

    MikroTik Router

        Sumber data (log, firewall, connection)

        Eksekutor rule (firewall address-list, filter)

3️⃣ Kebutuhan Fungsional
A. Monitoring

    Ambil data:

        Active connections

        Firewall logs

        Address-list

    Simpan ke database (log & histori)

B. Detection

    Rule berbasis:

        Request/connection count

        Port scanning

        Repeated failed access

    Threshold configurable

C. Auto‑Block

    Tambah IP ke:

        firewall address-list

        atau filter rules

    Support:

        Temporary block (timeout)

        Permanent block

D. Management

    Manual block / unblock

    Whitelist IP

    Audit log (siapa, kapan, kenapa)

4️⃣ Kebutuhan Non‑Fungsional

    Aman (API key / token)
    Modular & scalable
    Tidak membebani MikroTik
    Bisa dipakai banyak router (multi‑device)


[MikroTik Router]
       |
   (API / SSH)
       |
[Collector Service]
       |
[Analysis Engine]
       |
[Rule Engine]
       |
[Action Executor]
       |
[MikroTik Firewall]

        |
     [REST API]
        |
   (Frontend nanti)

   
6️⃣ Komponen Backend

    Collector

        Ambil data MikroTik (scheduler / polling)

    Analysis Engine

        Olah log & connection

    Rule Engine

        Evaluasi rule & threshold

    Action Executor

        Push rule ke MikroTik

    API Layer

        Endpoint untuk admin & frontend

    Database

        Log

        Rule

        Blocked IP

        Device

7️⃣ Flow Auto‑Block (Sederhana)

    Backend ambil data koneksi

    Analisis → IP melewati threshold

    Rule Engine valid

    Action Executor:

        Tambah IP ke address-list

    Log dicatat

    Status tersedia via API

8️⃣ Yang BELUM kita bahas (nanti)

    UI / UX

    Auth user detail

    Dashboard visual

    Notifikasi (Telegram/Email)

