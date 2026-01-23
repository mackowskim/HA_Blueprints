# Water Guardian – Monitor wycieków i zalania w Home Assistant

Ten zestaw plików umożliwia monitorowanie wycieków wody i zalania w domu z uwzględnieniem:

- średniego zużycia wody godzinowo w litrach,
- wykrywania podejrzenia wycieku w dzień i w nocy,
- powiadomień na urządzenia mobilne,
- obsługi regeneracji złoża zmiękczacza z tolerancją ±25 L/h,
- integracji z czujnikami zalania,
- wyboru sensora wody w litrach lub m³.

---

## Struktura repozytorium

/config/
├─ blueprints/
│ └─ automation/
│ └─ water_guardian_monitor_wyciekow_i_zalania.yaml
├─ input_number.yaml
├─ input_boolean.yaml

---

## Wymagania

- Home Assistant 2023.10 lub nowszy  
- Sensor zużycia wody (m³ lub L)  
- Opcjonalnie czujniki zalania  
- Urządzenia mobilne do powiadomień (np. M4hSzyna, Samsung Pati)  

---

## Instalacja

1. Skopiuj pliki do katalogu `/config/` w Home Assistant:

/config/input_number.yaml
/config/input_boolean.yaml
/config/blueprints/automation/water_guardian_monitor_wyciekow_i_zalania.yaml

yaml
Copy code

2. W `configuration.yaml` dodaj:

```yaml
input_boolean: !include input_boolean.yaml
input_number: !include input_number.yaml
Zrestartuj Home Assistant.

Sprawdź w Developer Tools → States, czy pojawiły się encje:

input_number.zuzycie_wody_stat_0 … 23

input_boolean.dzienny_wyciek_podejrzenie

input_boolean.nocny_wyciek_podejrzenie

Konfiguracja Blueprintu
Przejdź do Automations → Blueprints → Import i wybierz plik:
water_guardian_monitor_wyciekow_i_zalania.yaml

Tworząc nową automatykę z blueprintu, ustaw:

Sensor wody – w L lub m³

Jednostka sensora – L lub m³ (konwersja na litry w blueprint)

Urządzenia powiadomień – np. M4hSzyna, Samsung Pati

Przedział godzin monitorowania – np. 0–23, lub osobno dla nocy

Opcjonalnie uwzględnij zmiękczacz – jeśli włączony, blueprint uwzględnia regenerację złoża

Opcjonalnie czujniki zalania – powiadomienia w przypadku wykrycia wody

Jak działa automatyzacja
Aktualizuje średnie zużycie wody w godzinach (input_number.zuzycie_wody_stat_X)

Sprawdza anomalie względem średniej (przekroczenie progu wycieku)

Wysyła powiadomienia do wybranych urządzeń mobilnych

W przypadku zmiękczacza: uwzględnia średni pobór w czasie regeneracji ±25 L/h i wysyła ostrzeżenie, że to prawdopodobnie regeneracja

Czujniki zalania wyzwalają natychmiast powiadomienie i ustawiają flagi wycieku

Struktura encji
Input Number – średnie zużycie godzinowe w litrach
Copy code
input_number.zuzycie_wody_stat_0 … input_number.zuzycie_wody_stat_23
Input Boolean – flagi wycieku
Copy code
input_boolean.dzienny_wyciek_podejrzenie
input_boolean.nocny_wyciek_podejrzenie
Uwagi praktyczne
Sensor wody w m³ jest automatycznie przeliczany na litry

Możesz dostosować godziny monitorowania, urządzenia powiadomień i uwzględnienie zmiękczacza

Blueprint działa zarówno w dzień, jak i w nocy

Powiadomienia zawierają informację, czy pobór w normie regeneracji złoża zmiękczacza

Licencja
MIT License

