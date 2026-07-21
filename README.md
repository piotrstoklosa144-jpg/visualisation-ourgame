# 🎮 Power BI Dashboard: Wizualizacja – Nasza Gra

![Power BI](https://img.shields.io/badge/Power_BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![DAX](https://img.shields.io/badge/DAX-Data_Analysis_Expressions-blue?style=for-the-badge)
![Power Query](https://img.shields.io/badge/Power_Query-ETL-green?style=for-the-badge)

## 📌 O Projekcie
Kompleksowy raport analityczny wykonany w środowisku **Power BI Desktop**, służący do monitorowania wskaźników biznesowych, sprzedaży oraz zachowań użytkowników / graczy w projekcie **„Nasza gra”**. 

Celem projektu było przekształcenie surowych danych w interaktywne narzędzie menedżerskie, pozwalające na podejmowanie decyzji w oparciu o twarde dane (Data-Driven Decision Making).

---

## 🖼️ Podgląd Raportu (Dashboard Preview)

> *Wskazówka: Dodaj poniżej zrzut ekranu lub dynamicznego GIF-a z działającym raportem.*

![Podgląd Raportu](screenshots/dashboard_main.png)

---

## 🏗️ Architektura i Model Danych (Star Schema)

Dane zostały ustrukturyzowane w zalecanym modelu **Gwiazdy (Star Schema)**, co zapewnia wysoką wydajność zapytań DAX oraz przejrzystość relacji:

* **Tabela Faktów (`Fact_Sales` / `Fact_Gameplay`):** Zawiera kluczowe zdarzenia, transakcje oraz metryki ilościowe.
* **Tabele Wymiarów (`Dim_Players`, `Dim_Products`, `Dim_Platforms`):** Słowniki przechowujące dane kontekstowe (klient/gracz, kategorie, platformy).
* **Tabela Czasu (`Dim_Calendar`):** Dedykowana, auto-kalendarzowa tabela wymiaru czasu powiązana relacją jednokierunkową `1:N` z tabelą faktów, umożliwiająca zaawansowaną analizę Time Intelligence.

![Model Danych](screenshots/data_model.png)

---

## 🛠️ Proces ETL & Przetwarzanie Danych (Power Query / M)

Wszystkie dane źródłowe zostały poddane procesowi ETL w środowisku **Power Query**:
1. **Czyszczenie i Unifikacja:** Usunięcie wartości pustych (nulls), zmiana typów danych oraz poprawa spójności nazw kolumn.
2. **Przekształcenia:** Scalanie tabel (Merge/Append), rozbijanie unikalnych identyfikatorów oraz tworzenie kolumn warunkowych.
3. **M Language:** Optymalizacja kroków zapytania w języku M w celu przyspieszenia odświeżania raportu.

---

## 🧮 Logika Biznesowa & Zaawansowany DAX

W projekcie zaimplementowano szereg miar napisanych w języku **DAX** (od podstawowych kalkulacji po zaawansowane modyfikacje kontekstu i Time Intelligence):

### Przykład 1: Sumaryczna Sprzedaż (Total Revenue)
```dax
Total Revenue = 
SUMX(
    Fact_Sales,
    Fact_Sales[Quantity] * Fact_Sales[UnitPrice]
)
```

### Przykład 2: Analiza Rok-do-Roku (YoY Growth)
```dax
Revenue YoY % = 
VAR CurrentPeriod = [Total Revenue]
VAR PreviousPeriod = CALCULATE([Total Revenue], SAMEPERIODLASTYEAR(Dim_Calendar[Date]))
RETURN
DIVIDE(CurrentPeriod - PreviousPeriod, PreviousPeriod, 0)
```

### Przykład 3: Dynamiczne Filtrowanie / Modyfikacja Kontekstu
```dax
Active Players (All Time) = 
CALCULATE(
    DISTINCTCOUNT(Fact_Gameplay[PlayerID]),
    ALL(Dim_Calendar)
)
```

---

## 🎨 UX/UI & Interaktywność Raportu

Raport został zaprojektowany zgodnie z dobrymi praktykami wizualizacji danych (Data Storytelling):
* **Nawigacja (Bookmarks & Buttons):** Możliwość przełączania się między widokami ogólnymi a szczegółowymi za pomocą zakładek.
* **Drill-Through & Custom Tooltips:** Płynne przechodzenie od ogólnych KPI do szczegółowej analizy konkretnego segmentu lub gracza.
* **Kaskadowe Filtry (Slicers):** Synchronizacja filtrów na wszystkich stronach raportu przy zachowaniu czytelnego układu strony.

---

## 📂 Struktura Repozytorium

```text
├── 📄 README.md                        <- Dokumentacja projektu
├── 📊 Wizualizacja - Nasza gra.pbix   <- Główny plik Power BI Desktop
├── 📁 Data/                            <- Surowe pliki danych (CSV/Excel)
└── 📁 screenshots/                     <- Zrzuty ekranu raportu i modelu danych
```

---

## 🚀 Jak uruchomić projekt?

1. Pobierz plik **`Wizualizacja - Nasza gra.pbix`** z tego repozytorium.
2. Zainstaluj najnowszą wersję programu [Power BI Desktop](https://powerbi.microsoft.com/desktop/) (darmowy).
3. Otwórz pobrany plik w programie Power BI Desktop, aby w pełni wchodzić w interakcję z dashboardem, przeglądać miary DAX oraz model danych.

---

## 💼 Gotowy wpis do Twojego CV (Sekcja „Projekty”)

Możesz wkleić poniższy opis bezpośrednio do swojego CV, podpinając pod niego link do tego repozytorium:

> **Wizualizacja Analityczna – Nasza Gra | Power BI & DAX** *(Link do GitHuba)*
> * **Modelowanie Danych:** Zaprojektowanie i wdrożenie wydajnego modelu danych w architekturze **Star Schema** ze specjalną tabelą wymiaru czasu (`Dim_Calendar`).
> * **Transformacja ETL:** Czyszczenie, unifikacja i optymalizacja surowych danych źródłowych przy użyciu **Power Query** (M Language).
> * **Logika Biznesowa:** Zaawansowane kalkulacje KPI oraz analizy porównawcze (Time Intelligence, YoY, dynamiczny kontekst) z wykorzystaniem języka **DAX**.
> * **UX/UI & Raportowanie:** Stworzenie interaktywnego dashboardu z wykorzystaniem spersonalizowanych podpowiedzi (Custom Tooltips), zakładek nawigacyjnych (Bookmarks) oraz drill-through.
