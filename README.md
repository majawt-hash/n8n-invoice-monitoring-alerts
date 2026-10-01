# 🧾 Multi-Tenant Invoice Monitoring & Automated Alert System (n8n + GPT-4o)

Automatyczny system przetwarzania i monitorowania faktur kosztowych oraz poboru energii dla wielu podmiotów (12 niezależnych instancji/klientów). System pobiera pliki PDF z dedykowanych folderów Google Drive, wykonuje ekstrakcję danych za pomocą OCR i modeli LLM z ustrukturyzowanym parserem wyjściowym, weryfikuje warunki alertowe (m.in. po identyfikatorach PPE) oraz generuje i wysyła raporty HTML e-mailem.

```mermaid
graph TD
    A[Manual / Schedule Trigger] --> B[Set Mode & Configuration]
    B --> C[Google Drive: Search Invoice Files]
    C --> D[Loop Over Items]
    D --> E[HTTP Request / Fetch File]
    E --> F[Extract Text from PDF]
    F --> G[AI Agent: GPT-4o + Structured Output Parser]
    G --> H[Calculate Alert Conditions]
    H --> I[Split Out & Prepare Sheet Data]
    I --> J[Append to Google Sheets]
    J --> K{If: All Items Processed?}
    K -->|False| D
    K -->|True| L[Get Historical Data & Pick Latest PPE Period]
    L --> M[Aggregate Alerts for Email]
    M --> N[Generate HTML Email Template]
    N --> O[Gmail API: Send Approval / Alert Email]
'''
## 📌 Problem Biznesowy
Ręczne weryfikowanie i przepisywanie danych z dziesiątek faktur za energię i usługi operacyjne dla 12 podmiotów generuje wysokie ryzyko błędów oraz opóźnienia w wykrywaniu nieprawidłowości w zużyciu energii (PPE) i przekroczeniach budżetowych.

## 🔑 Kluczowe Funkcjonalności
* **Multi-Tenant Architecture:** Skalowalny schemat n8n wdrożony i dostosowany dla 12 osobnych podmiotów.
* **Automatyczna Ekstrakcja Danych (OCR + LLM):** Odczyt danych z faktur PDF i precyzyjne mapowanie pól poprzez `GPT-4o` i `Structured Output Parser`.
* **Kalkulacja Alertów & Analiza PPE:** Automatyczne przeliczanie odchyleń i warunków alertowych dla punktów poboru energii.
* **Centralizacja w Google Sheets:** Automatyczny dopis nowych rekordów i porządkowanie historii wg PPE oraz dat.
* **Agregacja i Raportowanie E-mail:** Tworzenie zbiorczego raportu HTML z wygenerowanym podsumowaniem i podglądem do zatwierdzenia.

## 🛠️ Architektura i Struktura Projektu

```text
n8n-invoice-monitoring-alerts/
├── .gitignore
└── README.md
