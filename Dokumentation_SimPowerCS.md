# Kurzdokumentation: Sim-PowerCS

**Sim-PowerCS** ist ein Java-basierter Energiemanagementsimulator für Smart-Home-Szenarien. Er dient als vereinfachte Testumgebung für Steuerungsalgorithmen (z. B. Reinforcement Learning, regelbasierte Ansätze).

---

## Modellumfang

| Komponente | Modellierung |
|---|---|
| **Erzeugung** | PV-Modul auf Basis stündlicher Einstrahlungsstatistik; minutengenau interpoliert mit Perlin-Rauschen für tägliche Variation |
| **Verbrauch** | Nicht-smarte Geräte (Dauerbetrieb nach Zeitregel) + smarte Geräte (steuerbar, mit Priorität und Zeitfenster) |
| **Speicher** | Batterie mit konfigurierbarer Kapazität (Wh) und Lade-/Entladerate (W) |
| **Netz** | Bidirektional: Zukauf und Verkauf zu stündlich variierenden Preisen |
| **Steuerung** | Zwei unabhängige Regler: `EnergyController` (Batterie/Netz) und `ServiceController` (Geräteschalten), beide austauschbar |
| **Zeitauflösung** | Minutengenau über konfigurierbare Anzahl Tage |

Mitgelieferte Controller: `DummyOn/Off` (Baselines), `Basic`, `PriorityBased`, `Greedy`.

---

## Abstraktionen

- Keine Netzphysik (Spannung, Frequenz, Phasen) — nur skalare Wh-Bilanzen
- Keine Batterie-Degradation, kein Tiefentladeschutz, kein Wirkungsgrad
- Keine Kommunikationslatenz — Steuerbefehle wirken sofort
- Vereinfachte Netzpreise — keine Steuern, Netzentgelte oder Einspeiseregelungen

---

## Setup zur Demonstration

**Voraussetzungen:** Java 8, Maven, IntelliJ

1. Projekt öffnen: *File → Open → `src/`* (enthält `pom.xml`)
2. Working Directory setzen: *Run → Edit Configurations → Working directory → `.../Sim-PowerCS/src`*
3. `src/data/config.xml` anpassen (Controller, Tage, Batteriegröße)
4. `App.java` starten → nach Simulation: 4 Diagrammfenster

**Controller-Vergleich** (gleichen Seed fixieren: `<seed>42</seed>`, `<procedural>false</procedural>`):

| Controller | Erwartetes Verhalten |
|---|---|
| `DummyOff` | Nur Grundlast — untere Verbrauchsbaseline |
| `DummyOn` | Alle Geräte maximal aktiv — obere Verbrauchsbaseline |
| `Basic` | Geräte nur bei Produktionsüberschuss |
| `Priority` | Abschaltung nach Priorität bei niedrigem Batteriestand |
| `Greedy` | Heuristik aus Priorität und Batteriezustand |
