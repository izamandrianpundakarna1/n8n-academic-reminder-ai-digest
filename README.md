# 🤖 n8n Academic Reminder & AI News Digest Bot

![n8n](https://img.shields.io/badge/n8n-Automation-ff6d5a?style=for-the-badge&logo=n8n)
![Telegram](https://img.shields.io/badge/Telegram-Bot-26A5E4?style=for-the-badge&logo=telegram)
![Notion](https://img.shields.io/badge/Notion-Database-000000?style=for-the-badge&logo=notion)
![Google Gemini](https://img.shields.io/badge/Google_Gemini-AI_Summarizer-8E75B2?style=for-the-badge&logo=googlegemini)

Sistem otomatisasi personal berbasis **n8n** yang terintegrasi dengan **Notion API**, **Google Gemini AI**, dan **Telegram Bot**. Sistem ini membantu mahasiswa mengelola tenggat waktu tugas kuliah serta menyajikan ringkasan berita harian seputar **Artificial Intelligence (AI), Teknologi, dan Ekonomi Global** secara konsisten setiap pagi (07:00 WIB) dan malam (20:00 WIB).

---

## 📌 Fitur Utama

- 📚 **Pengingat Tugas Kuliah (Notion Integration):** Mengambil data tugas aktif dari Notion Database dan mengirimkan notifikasi tenggat waktu langsung ke Telegram.
- 📰 **Rangkuman Berita Otomatis (RSS Feed + AI):** Mengumpulkan berita terkini dari RSS Feed terpercaya, merangkum poin-poin penting menggunakan Google Gemini AI, dan mengirimkannya dua kali sehari.
- ⏰ **Penjadwalan Fleksibel (Cron Trigger):** Alur kerja berjalan secara otomatis tanpa intervensi manual pada pukul 07:00 pagi dan 20:00 malam.
- 🔐 **Keamanan Data:** Menggunakan mekanisme kredensial terenkripsi pada n8n tanpa mengekspos API Key ke dalam repositori.

---

## 🏗️ Diagram Arsitektur Sistem

Berikut adalah alur kerja dan komunikasi antar komponen di dalam sistem:

```mermaid
flowchart TD
    subgraph Trigger ["⏰ Penjadwal Otomatis"]
        Cron[Schedule Trigger\n07:00 & 20:00 WIB]
    end

    subgraph DataFetch ["📥 Pengambilan Data"]
        NotionNode["Notion Node\n(Fetch Active Tasks)"]
        RSSNode["RSS Feed Read Node\n(AI, Tech, & Econ News)"]
    end

    subgraph Processing ["🧠 Pemrosesan Data & AI"]
        FilterTask["Filter Due Dates"]
        GeminiNode["Google Gemini AI\n(Summarize Articles to ID)"]
    end

    subgraph Output ["📤 Output Channel"]
        TelegramTask["Telegram Bot\n(Notifikasi Tugas)"]
        TelegramNews["Telegram Bot\n(Daily Executive Digest)"]
    end

    Cron --> NotionNode
    Cron --> RSSNode

    NotionNode --> FilterTask
    FilterTask --> TelegramTask

    RSSNode --> GeminiNode
    GeminiNode --> TelegramNews
