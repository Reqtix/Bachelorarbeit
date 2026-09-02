# SAP-basierte Scanlösung zur Sicherstellung der Rückverfolgbarkeit im Verpackungs- und Versandprozess für BMW-Lieferungen

## Bachelorarbeit

### Arbeitstitel

**Konzeption und Implementierung einer SAP-basierten Scanlösung zur Sicherstellung der Rückverfolgbarkeit von Verpackungsprozessen in der Automobilzulieferindustrie**

---

# Projektbeschreibung

Im Rahmen dieser Arbeit wird ein bestehender Verpackungs- und Versandprozess für BMW-Lieferungen analysiert, konzipiert und digitalisiert.

Der aktuelle Prozess sieht vor, dass interne Produktionslabels vor dem Versand entfernt und durch BMW-spezifische Transportlabels ersetzt werden. Dabei werden:

- pro Palette ein GLT-Label (Großladungsträger)
- pro Packstück bzw. Materialeinheit ein KLT-Label (Kleinladungsträger)

angebracht.

Die Durchführung erfolgt aktuell weitgehend manuell und ist nur eingeschränkt nachvollziehbar. Um die Anforderungen von BMW hinsichtlich Rückverfolgbarkeit, Dokumentation und Qualitätssicherung zu erfüllen, soll eine SAP-basierte Scanlösung entwickelt werden.

---

# Problemstellung

Der aktuelle Prozess birgt folgende Risiken:

- Fehlzuordnung von KLTs zu GLTs
- Fehlende digitale Dokumentation
- Keine lückenlose Rückverfolgbarkeit
- Erhöhte Fehleranfälligkeit durch manuelle Tätigkeiten
- Aufwendige Audit- und Nachweisführung
- Fehlende Transparenz bei Reklamationen

BMW fordert eine digitale Absicherung des Verpackungsprozesses durch Scan- und Prüfmechanismen.

---

# Zielsetzung

Ziel der Arbeit ist die Entwicklung einer SAP-basierten Anwendung zur:

- digitalen Erfassung aller Verpackungsvorgänge
- Validierung von Lieferungen und Packstücken
- Sicherstellung der Vollständigkeit
- Rückverfolgbarkeit aller Scanvorgänge
- Vermeidung von Fehlverpackungen
- revisionssicheren Dokumentation

Die Lösung soll als SAP Fiori Anwendung mit SAP RAP Backend umgesetzt werden.

---

# Forschungsfrage

> Wie kann durch eine SAP-basierte Scanlösung die Rückverfolgbarkeit und Fehlervermeidung im Verpackungs- und Versandprozess eines Automobilzulieferers verbessert werden?

Alternativ:

> Welche Auswirkungen hat die Einführung einer mobilen SAP-gestützten Scanlösung auf die Prozessqualität und Nachvollziehbarkeit von Verpackungsvorgängen im Versandprozess?

---

# Ausgangssituation (IST-Prozess)

## Aktueller Ablauf

1. Produktion erzeugt interne Labels.
2. Interne Labels werden an den Teilen angebracht.
3. Versandvorbereitung beginnt.
4. Interne Labels werden entfernt.
5. BMW-KLT-Labels werden angebracht.
6. BMW-GLT-Labels werden angebracht.
7. Versand erfolgt.

## Schwachstellen

- Keine digitale Bestätigung des Verpackungsvorgangs
- Manuelle Prüfungen
- Fehler erst bei BMW erkennbar
- Begrenzte Nachvollziehbarkeit
- Fehlende Protokollierung

---

# Zielprozess (SOLL-Prozess)

## Scanablauf

### Schritt 1 – Lieferung scannen

Prüfung:

- Lieferung vorhanden
- Lieferung offen
- Lieferung noch nicht vollständig verarbeitet

---

### Schritt 2 – Material scannen

Prüfung:

- Material gehört zur Lieferung
- Material ist noch nicht vollständig verpackt
- Material entspricht den Lieferpositionen

---

### Schritt 3 – KLT scannen

Prüfung:

- KLT existiert
- KLT wurde noch nicht verarbeitet
- KLT gehört zum gescannten Material
- KLT ist eindeutig

---

### Schritt 4 – GLT scannen

Prüfung:

- GLT existiert
- GLT wurde noch nicht verarbeitet
- KLT kann dem GLT zugeordnet werden

---

### Schritt 5 – Abschlussprüfung

Prüfung:

- Alle erwarteten KLTs vorhanden
- Alle Materialien vollständig verpackt
- Keine Doppelzuordnungen
- Keine offenen Positionen

---

### Schritt 6 – Protokollierung

Speicherung von:

- Liefernummer
- Materialnummer
- KLT
- GLT
- Benutzer
- Zeitstempel
- Abschlussstatus

---

# Fachliches Datenmodell

## Header

Verarbeitung einer Lieferung

### Attribute

- Liefernummer
- Benutzer
- Startdatum
- Enddatum
- Status

---

## Positionen

Gespeicherte Scanvorgänge

### Attribute

- Liefernummer
- Materialnummer
- KLT
- GLT
- Warenbegleitschein
- Scanzeitpunkt
- Benutzer

---

# Technische Architektur

```text
Scanner
    ↓
SAP Fiori App
    ↓
OData V4 Service
    ↓
SAP RAP Business Object
    ↓
SAP HANA Datenbank
```

---

# Verwendete SAP-Objekte

## Standardtabellen

### Lieferungen

- LIKP
- LIPS

### Handling Units

- VEKP
- VEPO

### Materialstamm

- MARA

---

## Eigene Objekte

### CDS Views

- ZI_BMW_SCAN_DELIVERY
- ZI_BMW_SCAN_MATERIAL
- ZI_BMW_SCAN_PACKAGE

### RAP Business Object

- ZI_BMW_SCAN_DELIVERY

### Datenbanktabellen

- ZBMW_SCAN_HDR
- ZBMW_SCAN_ITEM

---

# Implementierung

## Frontend

SAP Fiori Elements / SAPUI5

### Funktionen

- Barcode-Scan
- Validierungen
- Benutzerführung
- Fehlermeldungen
- Erfolgsrückmeldungen

---

## Backend

SAP RAP

### Actions

- ScanDelivery
- ScanMaterial
- ScanKLT
- ScanGLT
- CompleteProcess

### Prüfungen

- Existenzprüfungen
- Statusprüfungen
- Vollständigkeitsprüfungen
- Dublettenprüfung

---

# Evaluation

## Messgrößen

### Prozessqualität

- Fehlerquote vorher
- Fehlerquote nachher

### Nachvollziehbarkeit

- Manuell
- Vollständig digital

### Bearbeitungszeit

- Ist-Prozess
- Soll-Prozess

### Auditfähigkeit

- Vorher
- Nachher

---

# Erwarteter Nutzen

## Für BMW

- Höhere Nachverfolgbarkeit
- Verbesserte Qualität
- Nachweisbare Prozesssicherheit

## Für das Unternehmen

- Weniger Verpackungsfehler
- Schnellere Ursachenanalyse
- Höhere Prozesssicherheit
- Digitale Dokumentation
- Bessere Auditfähigkeit

---

# Gliederung der Bachelorarbeit

## 1. Einleitung

- Problemstellung
- Zielsetzung
- Forschungsfrage
- Aufbau der Arbeit

## 2. Theoretische Grundlagen

- SAP Versandprozess
- Rückverfolgbarkeit
- Barcode-Systeme
- Handling Units
- Qualitätsmanagement in der Automobilindustrie

## 3. Analyse des Ist-Zustands

- Prozessaufnahme
- Schwachstellenanalyse
- Anforderungen von BMW

## 4. Konzeption der Lösung

- Fachkonzept
- Prozessmodell
- Datenmodell
- Prüfkonzept

## 5. Implementierung

- SAP Architektur
- CDS Views
- RAP Business Object
- Fiori Anwendung
- Datenhaltung

## 6. Evaluation

- Testfälle
- Validierung
- Nutzenanalyse
- Vergleich Ist/Soll

## 7. Fazit und Ausblick

- Zusammenfassung
- Bewertung der Ergebnisse
- Mögliche Erweiterungen

---

# Technologien

- SAP S/4HANA
- ABAP RESTful Application Programming Model (RAP)
- CDS Views
- OData V4
- SAP Fiori
- SAPUI5
- SAP HANA

---

# Autor

Johannes Kuebler

SAP Application Development
