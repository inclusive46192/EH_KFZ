# EH_KFZ Heuss - konsolidierter MVP-Plan

## 1. Ziel und Erfolg

Das System soll den Chef von Routineunterbrechungen entlasten, ohne kritische Faelle zu uebersehen. Erfolg bedeutet:

- jeder relevante Anruf ist nachvollziehbar erfasst
- Routineanfragen landen bei der richtigen Person oder Rueckrufaufgabe
- sicherheitskritische Faelle werden sofort sichtbar und weitergeleitet
- Mitarbeitende sehen im Dashboard, was als Naechstes zu tun ist
- Rueckrufe gehen nicht verloren
- die Loesung kann spaeter um KI und Werkstattsoftware-Integration erweitert werden

## 2. Empfohlener Umfang

### MVP 1: IVR und Vorgangsboard

- Rufumleitung der bestehenden Nummer
- kurze Ansage mit drei bis fuenf Anliegen
- Tastenauswahl als verlaesslicher Start; Sprache optional als begrenzter Test
- Vorgang aus jedem Anruf
- Prioritaet: niedrig, mittel, hoch, kritisch
- Status: offen, in Bearbeitung, wartet auf Kunde, erledigt, geschlossen
- Rueckrufaufgabe mit Zeitfenster
- Mitarbeiter-Dashboard mit Suche nach Kunde, Fahrzeug und Kennzeichen
- E-Mail oder Dashboard-Hinweis; SMS nur fuer kritische Faelle
- direkte Weiterleitung kritischer Faelle waehrend der Geschaeftszeit

### MVP 1 bewusst nicht

- vollautomatische Terminbuchung
- verbindliche automatische Angebote
- vollstaendige Werkstattsoftware-Integration vor geklaerter API
- automatische Sicherheitsbewertung ohne Mensch
- dauerhafte Aufzeichnung aller Gespraeche
- komplette Kundenportal- oder WhatsApp-Plattform

### Stufe 2: kontrollierte KI-Triage

- Speech-to-Text fuer kurze Sprachangaben und optional Anrufzusammenfassungen
- feste Ausgabe: Anliegen, Prioritaet, Sicherheitsflag, Kennzeichenkandidat, Zusammenfassung, Sicherheit
- Backend validiert und entscheidet regelbasiert
- unsichere Kennzeichen werden bestaetigt oder auf SMS/Web-Link umgeleitet
- KI hat keinen direkten SQL- oder Datenbankzugriff
- Mensch bestaetigt sicherheitskritische und unsichere Faelle

### Stufe 3: Status und Website

- Werkstattsoftware per API oder Import anbinden
- Statusabfrage ueber SMS/Web-Link mit Kennzeichen plus zusaetzlichem Nachweis
- moderne, mobile Website mit Leistungen, Kontakt, Oeffnungszeiten, Statusabfrage und Angebotsformular
- Rueckrufzeiten vormittags/nachmittags als feste Auswahl

## 3. Zielprozesse

### Statusabfrage

1. Anrufer waehlt Status.
2. System identifiziert den Vorgang ueber Rufnummer, Kennzeichen oder Rueckrufaufgabe.
3. Bei sicherem Treffer wird ein nicht-sensibler Status ausgegeben oder ein Link versendet.
4. Bei keinem oder mehreren Treffern wird eine Rueckrufaufgabe erzeugt.

Kennzeichen duerfen allein keine vertraulichen Details freigeben. Die genaue Identitaetspruefung wird nach Kenntnis der Werkstattsoftware festgelegt.

### Angebotsanfrage

1. Anrufer waehlt Angebot.
2. System erfasst Fahrzeug, Anliegen und Rueckrufzeitfenster.
3. Fotos oder weitere Angaben koennen per SMS/Webformular nachgefordert werden.
4. Eine Preisspanne ist nur unverbindlich und erst nach fachlicher Freigabe zulaessig.

### Sicherheitskritischer Fall

1. Anrufer waehlt Notfall oder nennt ein sicherheitsrelevantes Problem.
2. Vorgang wird kritisch markiert.
3. Waehrend der Geschaeftszeit erfolgt direkte Weiterleitung bzw. Alarmierung.
4. Ausserhalb der Geschaeftszeit wird eine klare Notfallansage verwendet; das System gibt keine technische Reparaturanweisung.

## 4. Fachliches Datenmodell

- **Kunde**: Name und erlaubte Kontaktwege
- **Fahrzeug**: Kennzeichen, VIN sofern vorhanden, Marke/Modell und Kunde
- **Werkstattauftrag**: Fahrzeug, Beschreibung und Auftragsstatus
- **Anruf**: Rufnummer, Zeit, Kanal und Ergebnis
- **Vorgang**: Anliegen, Prioritaet, Status, Zusammenfassung und Zustaendigkeit
- **Rueckrufaufgabe**: Vorgang, Faelligkeit/Zeitfenster, Status und Bearbeiter
- **Kommunikation**: Anruf, SMS, E-Mail oder Webformular
- **Mitarbeiter**: Rolle und zustaendige Anliegen
- **Statusprotokoll**: nachvollziehbare Aenderungen an Vorgang und Auftrag
- **KI-Ergebnis**: Transkript, Konfidenz und vorgeschlagene Klassifizierung; niemals alleinige Sicherheitsentscheidung

## 5. Technische Zielarchitektur

Telefonieanbieter/IVR -> Webhook/API -> Backend -> PostgreSQL -> Dashboard

Optional ab Stufe 2:

Anruf/Sprache -> Speech-to-Text -> validiertes KI-Ergebnis -> Backend-Regeln -> Vorgang/Alarm

Empfohlener Start:

- Backend: Python/FastAPI
- Datenbank: PostgreSQL, fuer den MVP bevorzugt verwaltet
- Frontend: Next.js/React
- Datenzugriff: SQLAlchemy und Alembic oder ein gleichwertiger, gepflegter Ansatz
- Deployment: einfacher Managed- oder Docker-Betrieb statt Microservices
- Authentifizierung und Rollen fuer Mitarbeitende

## 6. API-Fundament

- `POST /webhooks/phone/incoming`
- `POST /api/v1/calls`
- `POST /api/v1/tickets`
- `GET /api/v1/tickets`
- `GET /api/v1/tickets/{id}`
- `PATCH /api/v1/tickets/{id}`
- `GET /api/v1/customers/{id}`
- `GET /api/v1/vehicles/{id}`
- `POST /api/v1/callbacks`
- `POST /api/v1/communications`
- `POST /api/v1/auth/login`

Webhook-Eingaben werden authentifiziert, idempotent verarbeitet und protokolliert. Provider-spezifische Daten bleiben an der Integrationsgrenze; die fachlichen Vorgänge bleiben providerunabhaengig.

## 7. Dashboard

- offene Vorgänge nach Prioritaet
- kritische Faelle prominent und nicht nur farblich markiert
- Filter nach Status, Anliegen, Mitarbeiter und Faelligkeit
- Suche nach Kunde, Fahrzeug und Kennzeichen
- Detailansicht mit Zusammenfassung, Kommunikationsverlauf und Notizen
- Aktion: uebernehmen, weiterleiten, Rueckruf planen, erledigen
- Live-Aktualisierung oder kurze automatische Aktualisierung

## 8. Umsetzung in Phasen

### Phase 1 - Ist-Zustand und Freigabe

Betriebsdaten, Werkstattsoftware, Telefonie, Anrufmuster, Verantwortlichkeiten, Sicherheitsregeln und Budget erheben. Ergebnis: freigegebener MVP-Scope.

### Phase 2 - Technisches Fundament

Repository, Umgebungen, Authentifizierung, Datenmodell, Migrationen, API-Grundgeruest und Testdaten einrichten.

### Phase 3 - IVR und Vorgangserfassung

Provider anbinden, Webhook absichern, Anrufe und Vorgänge speichern, Prioritaeten und Rueckrufaufgaben abbilden.

### Phase 4 - Dashboard und Benachrichtigungen

Dashboard, Rollen, Filter, Statuswechsel und Eskalationen umsetzen. Mit realistischen Testfaellen pruefen.

### Phase 5 - Pilotbetrieb

Zunaechst parallel oder mit begrenzter Rufumleitung testen. Falschzuordnungen, verpasste Rueckrufe und Reaktionszeiten messen.

### Phase 6 - KI-Spike und Integration

Erst nach stabiler Basis kurze Speech-to-Text- und Kennzeichen-Tests durchfuehren. KI nur mit festem Schema, Konfidenz, Fallback und menschlicher Freigabe einsetzen.

### Phase 7 - Statusabfrage und Website-Relaunch

Nach Klaerung der Werkstattsoftware Statusintegration und Web-Link/SMS umsetzen; die Website mobil, klar und conversion-orientiert modernisieren.

## 9. Kostenrahmen

Als grobe laufende Infrastruktur fuer die erste Stufe sind etwa 30-120 EUR pro Monat realistisch, abhaengig von Telefonie, Hosting, SMS und Datenvolumen. Entwicklung, Einrichtung und Providerwechsel sind davon getrennt zu kalkulieren.

## 10. Betrieb und Datenschutz

- nur notwendige Kundendaten speichern
- Aufbewahrungsfristen fuer Anrufe, Transkripte und Notizen festlegen
- Aufzeichnungen nur nach rechtlicher Pruefung und transparenter Information
- Zugriffe nach Rolle begrenzen
- kritische Regeln deterministisch im Backend halten
- externe Speech-/KI-Dienste vor Einsatz datenschutzrechtlich und vertraglich pruefen
- Protokollierung ohne unnötige Klartextdaten

## 11. Abnahmekriterien fuer den Pilot

- Testanruf erzeugt genau einen Vorgang
- doppelte Provider-Webhooks erzeugen keinen zweiten Vorgang
- jeder Vorgang hat Anliegen, Prioritaet und Status
- kritische Testfaelle alarmieren die definierte Person
- Standardanfragen landen nicht beim Chef
- Rueckrufaufgaben sind faelligkeitsbezogen sichtbar
- Mitarbeiter koennen einen Vorgang ohne technische Hilfe abschliessen
- bei unsicherem Kennzeichen oder KI-Ergebnis wird nicht geraten, sondern bestaetigt oder eskaliert
