# LIW01 Water Guardian Integration

Autor: M4hSzyna (@mackowskim)

Integracja custom_components/liw01 dla Home Assistant dostępna przez HACS.

## Funkcjonalność

- Tworzy wszystkie helpery wymagane przez blueprint **Water Guardian**
- Tworzy sensory poboru wody w L i koszt wody w PLN
- Pobiera dane z MQTT SUPLA (LIW-01)
- Sensory gotowe do podpięcia do blueprinta

## Instalacja przez HACS

1. Dodaj moje repozytorium GitHub w HACS:
   - Settings → Integrations → HACS → Integrations → „+” → Custom repository  
   - Wklej URL: `https://github.com/mackowskim/HA_Blueprints`  
   - Category: Integration

2. Wybierz integrację `liw01` i kliknij „Install”

3. Zrestartuj Home Assistant

4. Integracja automatycznie utworzy helpery i sensory:
   - `input_number.water_leak_streak`
   - `input_number.water_zero_hour_streak`
   - `input_datetime.water_leak_last_alert`
   - `input_number.zuzycie_wody_stat_0` ... `input_number.zuzycie_wody_stat_23`
   - `sensor.water_guardian_pobor_ostatnia_godzina_l`
   - `sensor.water_guardian_koszt_wody`

## Podłączenie do blueprinta

- `water_hour_meter` → `sensor.water_guardian_pobor_ostatnia_godzina_l`
- `notify_device`, `notify_device_secondary`, `media_players` → dowolne encje w HA

