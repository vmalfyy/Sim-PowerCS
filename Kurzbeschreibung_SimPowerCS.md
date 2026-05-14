# Kurzbeschreibung: Sim-PowerCS

**Sim-PowerCS** ist ein Java-basierter, minutengenauer Energiemanagementsimulator für Smart-Home-Szenarien. Der Simulator ist bewusst vereinfacht gehalten, um als Testumgebung für Steuerungsalgorithmen (z. B. Reinforcement Learning, genetische Algorithmen) zu dienen.

---

## Modellierte Systemaspekte

| Aspekt | Beschreibung |
|---|---|
| **Energieerzeugung** | Photovoltaikmodul — entweder auf Basis realer Messdaten (CSV) oder prozedural aus stündlichen Einstrahlungsdaten mit Rauschen |
| **Energieverbrauch** | Passive Grundlast (CSV-Modell), dienstbasierte aktive Last (smart/nicht-smart), zufällige Last sowie unerwartete Ereignisse |
| **Energiespeicher** | Batterie mit konfigurierbarer Kapazität (kWh) und maximaler Lade-/Entladeleistung (W) |
| **Netzanbindung** | Bidirektionaler Netzzugang — Zukauf und Verkauf zu stündlich variierenden Preisen (optional mit prozeduralem Rauschen) |
| **Dienste / Services** | Geräte mit fester oder steuerbarer Laufzeit, Priorität und Zeitfenstern (z. B. Poolpumpe, Beleuchtung, Internet) |
| **Steuerungslogik** | Austauschbare Energie- und Serviceregler (`EnergyController`, `ServiceController`) — mehrere Strategien vorgegeben (Greedy, Priority-Based, Dummy) |
| **Zeitliche Auflösung** | Minutengenau über konfigurierbare Anzahl von Simulationstagen |
| **Ergebnisausgabe** | CSV-Export, statistische Kennzahlen, Diagramme (XChart) |

---

## Bewusst abstrahierte / nicht modellierte Aspekte

- **Netzphysik:** Spannung, Stromstärke, Frequenz und Phasen werden nicht modelliert — alle Größen sind skalare Leistungswerte in Watt (Wh/min).
- **Schutzmechanismen:** Überspannungsschutz, Leitungsschutz, Wechselrichterverhalten und Netzsynchronisation sind nicht enthalten.
- **Thermische Effekte:** Wärmeverluste, Temperaturgänge und Degradationseffekte bei Batterie oder PV werden nicht berücksichtigt.
- **Netzwerkkommunikation / Latenz:** Steuerbefehle wirken instantan; Kommunikationsverzögerungen und -ausfälle existieren nicht.
- **Wirtschaftliche Komplexität:** Netzentgelte, Steuern, Einspeisevergütungsregelungen und dynamische Tarifsysteme sind auf einen einfachen stündlichen Kauf-/Verkaufspreis reduziert.
- **Mehrere Gebäude / Mikronetz:** Das Modell beschreibt genau ein System; Interaktionen zwischen mehreren Knoten sind nicht vorgesehen.
